# GameCatalog 資料撰寫規範

本文件供 AI coding agents 與資料維護者使用，適用於整個倉庫。修改前先閱讀相關資料及 [README.md](README.md)；安全問題依 [SECURITY.md](SECURITY.md) 處理。`CLAUDE.md` 直接引用本文件，規則只在此處維護。

## 1. 系統定位與修改原則

- 本專案是以 GitHub Pages／Jekyll 發布的靜態遊戲資料系統，不是遊戲執行環境或後端服務。
- `categories.json` 是共用分類字典；`games/<id>.json` 是單一遊戲完整紀錄；根目錄 `allgames.json` 只記錄全部遊戲的 `id` 與 `path` 參照。
- 目前已依 [官方遊戲首頁](https://gh.ysgs.app/) 建立七個遊戲紀錄與參照索引。本文件定義版本 1 資料契約；尚未提供 JSON Schema、自動驗證器、搜尋介面或資料載入程式。
- 未經要求，不新增後端、資料庫、套件依賴、建置工具或動態 API。
- 僅修改任務涉及的資料與文件，保留使用者既有變更，不順便重排其他紀錄。
- 不捏造遊戲功能、網址、發行狀態、翻譯、封面來源或授權。缺少必要事實時，先查證；無法查證就明確指出缺少的資訊。
- 新增資料不等於部署完成；不得將未檢查的公開網址描述為已上線。

## 2. 檔案分工與格式

| 路徑 | 用途 |
| --- | --- |
| `categories.json` | 分類 key 與 `en`、`zh-TW`、`ja` 三語名稱。 |
| `games/<id>.json` | 每個遊戲一個 JSON object；檔名須與紀錄 `id` 一致，是遊戲內容的維護來源。 |
| `allgames.json` | 根目錄的遊戲參照索引；每項只有 `id` 與 `/games/<id>.json` 的 `path`，按 `id` 升冪排序。 |
| `README.md` | 中英雙語功能、資料取用與網站操作說明，須與實際內容保持一致。 |
| `AGENTS.md` | 本資料系統的撰寫契約與 agent 工作規範。 |
| `CLAUDE.md` | 僅引用 `AGENTS.md`，不複製本文件內容或建立第二套規則。 |
| `_config.yml`、`CNAME` | Jekyll 與自訂網域設定；資料更新不應順便修改它們。 |

JSON 檔案統一使用 UTF-8、兩個空白縮排、LF 換行，並保留檔尾換行。不得加入註解、尾隨逗號、重複 key、`NaN` 或 `Infinity`。文字不得有無意義的前後空白。

資料值須符合下列型別，不以空字串、`null` 或錯誤型別代替缺漏的必要資料。JSON 物件欄位順序不具業務意義，但修改既有資料時應保留原有順序，避免無關 diff。

## 3. `categories.json` 規範

- 根節點是 object，不是分類陣列。
- 分類 key 使用小寫英文字母與數字；複合名稱以底線分隔，例如 `strategy`、`action_rpg`、`turn_based_strategy`。
- 每個分類必須包含 `en`、`zh-TW`、`ja` 三個非空字串，欄位大小寫必須完全一致。
- 先搜尋既有分類再新增，避免同義分類與只因翻譯不同產生的重複項目。
- 遊戲 `categories` 引用這裡的 key，不使用翻譯名稱、顯示文字或自行拼出的替代 key。
- 類型可能重疊；分類字典沒有父子結構、排序權重或互斥規則。不要自行推導這些關係。
- 修改翻譯時保留 key；重新命名或移除 key 時須同步處理所有 `games/*.json` 分類引用與文件範例，並說明對外部使用端的影響。參照索引不存放分類欄位。
- 不因新增遊戲就無條件新增分類。若 `strategy`、`puzzle` 等既有分類足夠，直接引用。

## 4. `games/*.json` 版本 1 契約

每個檔案只存放一個遊戲 object。以下是本文件採用的欄位與作者要求，不是既有程式已自動強制的檢查。

| 欄位 | 型別／必要性 | 撰寫規則 |
| --- | --- | --- |
| `schemaVersion` | Integer，必填 | 目前為 `1`，不能寫成字串 `"1"`。 |
| `id` | String，必填 | 全倉庫唯一；使用小寫英文字母、數字及分隔用連字號，例如 `hiddenshade`、`my-game`。不得有路徑分隔符號，且須與檔名去除 `.json` 後一致。 |
| `defaultLocale` | String，必填 | 預設顯示語言；須是 `locales` 中實際存在的 key，例如 `zh-TW`。 |
| `locales` | Object，必填 | 完整提供 `zh-TW`、`en`、`ja` 三種語言，每種語言均有非空字串 `name`、`description`。 |
| `url` | String，必填 | 官方通用入口的絕對 HTTPS URL，也是未指定語言啟動網址時的入口。 |
| `launchUrls` | Object，選填 | 語言代碼到絕對 HTTPS 啟動網址的映射；只放真正支援且已確認的網址。沒有語言專用網址時省略此欄位。 |
| `cover` | String，必填 | 原始遊戲網站提供的絕對 HTTPS 圖片 URL。只取得並記錄連結，不下載圖檔、不建立本地封面路徑；發布前檢查連結能回傳圖片。 |
| `categories` | Array of strings，必填 | 至少一個、不可重複；每項必須存在於 `categories.json`。 |
| `tags` | Array of strings，必填 | 可為空陣列；非空項目使用小寫英文、數字與連字號，不重複，用來補充機制或遊玩特徵。 |
| `status` | String，必填 | 本版公開紀錄使用 `published`。其他狀態尚未定義，不自行創造 `draft`、`hidden` 等值或假設它們能阻止公開。 |

### 語言與文案

- 使用 `zh-TW`，不要改成 `zh`、`zh-tw` 或 `zh-CN`；`en`、`ja` 也須維持一致。
- 三語描述應表達相同的遊戲內容，不在某個語言版本加入未經確認的玩法或功能。
- 繁體中文使用繁體字；日文採自然表達。專有名稱無官方譯名時可保留原名。
- `name` 是遊戲顯示名稱；`description` 是簡潔玩法介紹。兩者皆為純文字，不加入 HTML、Markdown 標籤或可執行腳本。
- `defaultLocale` 不代表可以省略其他兩語資料，也不會自動補齊翻譯。
- 本版固定三語；若要增加語言，先同步擴充資料契約與使用端規則，不只在單一檔案臨時加入。

### 分類與 tags 的差別

`categories` 是共用類型，例如 `strategy`。`tags` 是補充特徵，例如 `stealth`、`maze`、`single-player`。tag 即使剛好與分類 key 相同，也不代表兩者有自動關聯。

tags 目前沒有另設中央字典。新增前應比對其他遊戲用詞，避免 `single-player` 與 `singleplayer` 表達同一概念卻混用。不得只從遊戲名稱猜測特徵。

## 5. 語言啟動網址的含義

`locales` 的 key 是本站資料語言代碼；目標遊戲的 query parameter 則由該遊戲自行定義，兩者不必相同。

例如 `launchUrls["zh-TW"]` 可以是 `https://hiddenshade.ysgs.app/?lang=zh`。不得自動將網址改成 `?lang=zh-TW`，也不得自行補上 `?lang=en` 或 `?lang=ja`，除非確認遊戲確實支援。

使用端若實作啟動網址解析，應遵循本契約：

1. 若 `launchUrls` 有使用者選擇語言的已提供網址，使用該網址。
2. 若沒有，使用 `url`，不要替缺漏語言推測 query parameter。
3. 不因缺少某語言的啟動網址就改用另一語言專用網址；文字的預設語言與啟動網址的 fallback 是不同概念。

`launchUrls` 的 key 須存在於 `locales`，但不必包含全部三語。這是供未來使用端遵循的資料語意，不代表倉庫已存在實作此流程的程式。

## 6. 完整遊戲資料範例

下列為實際紀錄 **[games/hiddenshade.json](games/hiddenshade.json)** 的完整範例。簡介依官方遊戲首頁、封面來自原始遊戲網站，日文名稱與 `?lang=zh|en|ja` 語言參數依 [已部署的語言模組](https://hiddenshade.ysgs.app/src/systems/i18n.js)：

```json
{
  "schemaVersion": 1,
  "id": "hiddenshade",
  "defaultLocale": "zh-TW",
  "locales": {
    "zh-TW": {
      "name": "藏影迷城",
      "description": "避開巡邏者的視線，躲進暗處，找到暖光出口。迷宮型躲貓貓。"
    },
    "en": {
      "name": "HiddenShade",
      "description": "Avoid the patrols' gaze, hide in the shadows, and find the warmly lit exit in a maze-based game of hide-and-seek."
    },
    "ja": {
      "name": "影隠れの迷城",
      "description": "巡回者の視線を避け、暗がりに身を隠して、暖かな光の出口を探そう。迷路を舞台にしたかくれんぼゲーム。"
    }
  },
  "url": "https://hiddenshade.ysgs.app/",
  "launchUrls": {
    "zh-TW": "https://hiddenshade.ysgs.app/?lang=zh",
    "en": "https://hiddenshade.ysgs.app/?lang=en",
    "ja": "https://hiddenshade.ysgs.app/?lang=ja"
  },
  "cover": "https://hiddenshade.ysgs.app/assets/og.png",
  "categories": [
    "stealth",
    "puzzle"
  ],
  "tags": [
    "stealth",
    "maze",
    "isometric"
  ],
  "status": "published"
}
```

這是倉庫中的實際資料範例。封面只記錄原始遊戲網站的 HTTPS 圖片連結，不下載圖片，也不建立 `covers/` 目錄。紀錄與參照索引仍需 commit、push 及成功部署後才會在資料網站發布。

- 名稱與描述依選定語言讀取；若使用端收到不支援的顯示語言，可依 `defaultLocale` 顯示完整的預設語言文案。
- `stealth` 與 `puzzle` 來自既有分類字典，不以顯示名稱代替 key。
- 三語啟動網址分別使用已確認的 `?lang=zh`、`?lang=en` 與 `?lang=ja`；其他遊戲不可照抄這些參數。
- 封面使用 `https://hiddenshade.ysgs.app/assets/og.png`，由原始遊戲網站託管；外部資產可用性須另外檢查。

## 7. 網址、封面與公開資料安全

- 外部遊戲入口、語言專用入口與外部封面使用 HTTPS；不放入 `javascript:`、`data:`、`file:`、私有管理入口或含帳密的 URL。
- 檢查網址中的 query parameter，不儲存 token、session、臨時簽章或其他秘密。
- 封面以原始遊戲首頁標準的 `<meta property="og:image" content="...">` 連結為準，不使用其他尺寸的分享卡、任意官方資產或工作室首頁轉存圖。缺少 `og:image` 時先回報，不自行猜測替代圖片。
- 「抓取封面」在本專案指取得 URL，不是下載檔案；除非使用者另外明確要求，不能建立 `covers/` 或複製、轉檔、重新託管圖片。
- 不依檔名猜測格式或更改副檔名；例如 Bunny Doom 原始封面為 `og.jpg`，不能改成不存在的 `og.png`。使用圖片連結仍須尊重來源權利與條款。
- `published` 是紀錄標記，不是 GitHub Pages 的隱私控制。提交到公開倉庫的內容即可能被讀取，不能依賴某個欄位隱藏資料。
- 不提交憑證、個資、未公開遊戲內容或未修復漏洞的利用細節。遇到安全問題依 `SECURITY.md` 私密通報。

## 8. 修改與驗證流程

1. 查看實際檔案及相關引用，確認任務是改分類、改遊戲資料，還是改文件。
2. 新增遊戲前核對 `id`、三語內容、官方網址、封面與發布狀態；不要複製範例後留下不屬於該遊戲的值。
3. 依契約修改最少必要資料；分類 key 變動須同步遷移所有引用。新增、重新命名或刪除遊戲時同步更新 `allgames.json` 的參照；只修改遊戲文案、分類或封面時，不把內容複製到索引。
4. 執行 JSON 解析與重複 key 檢查，再檢查必要欄位、型別、三語完整性、分類存在性、陣列去重與檔名／`id` 一致性。
5. 實際讀取修改後的資料，確認名稱、描述及分類映射符合預期；若涉及語言啟動網址，分別檢查有專用網址與只有通用網址的情況。
6. 正式發布紀錄前檢查封面連結回傳成功且 Content-Type 為圖片，並在安全、獲授權的情況下檢查遊戲入口。驗證可讀取回應，但不將圖片保存到倉庫；不能確認的外部條件須回報。
7. 對資料契約、功能或取用方式的變更，同步更新 README 中英說明及本文件；單純新增紀錄不需要無關重寫文件。
8. 回報修改檔案、實際完成的驗證，以及未確認的事項。除非使用者要求，不自動 commit、push 或部署。

### 可用的基本語法檢查

在倉庫根目錄使用 Python 3 標準工具：

```sh
python3 -m json.tool categories.json
```

檢查單一遊戲與根目錄參照索引：

```sh
python3 -m json.tool games/hiddenshade.json
python3 -m json.tool allgames.json
```

`json.tool` 只檢查基本解析，不會阻止所有重複 key，也不會檢查三語欄位、網址可用性、分類引用或封面內容。不能將語法檢查成功當成完整資料驗證。

本倉庫目前沒有專用測試、lint、JSON Schema 或 CI 驗證命令。不得捏造 `npm test`、`npm run validate` 等腳本，或為單次資料更新引入不必要工具。需要更完整檢查時，使用既有能力或一次性驗證，並明確報告實際檢查範圍。

## 9. 契約演進與文件同步

- 不自行加入價格、平台、評分、上市日期等未定義欄位；需要時先確認需求、來源與所有使用端影響。
- `schemaVersion` 不是一般編輯次數；文字修正與符合版本 1 的新增紀錄維持 `1`。
- 改變欄位含義、必要性、型別或狀態語意時，先設計資料及使用端的整體遷移，確認是否需要新版本，不能只改版本號。
- 不為了相容性猜測而加入舊欄位 alias、重複輸出或靜默轉換；明確遷移受影響資料與呼叫端。
- 區分「文件規範」、「實際檔案」與「已部署功能」；遊戲資料與參照索引已提供，但沒有實作的驗證器或互動介面不可描述為已提供。
- `CLAUDE.md` 保持單行 `@AGENTS.md` 引用。修改本文件即更新共用規則，不另外複製內容。

## 10. `allgames.json` 參照契約與現有遊戲

根目錄 [allgames.json](allgames.json) 是發現遊戲紀錄的輕量索引，**不重複存放完整遊戲欄位**：

| 欄位 | 型別 | 規則 |
| --- | --- | --- |
| `schemaVersion` | Integer | 目前為 `1`，表示索引容器的版本。各遊戲另保留自己的版本。 |
| `games` | Array of objects | 每個元素只有 `id` 與 `path`；所有 `games/*.json` 各參照一次。 |
| `games[].id` | String | 與目標紀錄的 `id` 及檔名一致，全索引唯一。 |
| `games[].path` | String | 網站根路徑 `/games/<id>.json`；不存放本機絕對路徑或遊戲的啟動網址。 |

- `games/*.json` 是遊戲詳細內容唯一的維護來源；索引只負責找到它們。
- 不把 `locales`、`url`、`launchUrls`、`cover`、`categories`、`tags`、`status` 或其他遊戲欄位複製到索引。
- 按 `id` 的字典序升冪排列，不沿用檔案系統列舉順序，也不把順序當作推薦排名。
- 新增或移除紀錄時同步新增或移除參照；重新命名時同步更新 `id`、檔名與 `path`。
- 只修改遊戲描述、分類或封面等詳細內容，不需要改索引。
- 不手動維護 `count` 或時間戳欄位；筆數由 `games.length` 取得，版本歷史由 Git 追蹤。
- 目前公開紀錄皆為 `published`，全部收錄。若未來擴充狀態，先確認公開契約；不得把索引是否列出當成檔案的隱私控制。
- 驗證索引與檔案的 ID 集合完全相等、每個 `path` 能找到檔案，且載入後的紀錄 `id` 一致；只檢查筆數不足以證明完整。
- 本倉庫尚未提供自動產生腳本；不假設 commit 或 Jekyll 會自動更新參照。
- 使用端先讀取 `/allgames.json`，再用 `new URL(reference.path, siteOrigin)` 載入需要的紀錄；`path` 是資料網站的位置，不是遊戲 `url` 的相對位置。
- README 中英兩段須保留索引用法與資料查找範例，不把索引描述成完整遊戲清單的內容快照。

目前七款來源遊戲如下；後續新增紀錄時同步維護此表及 README：

| ID／檔案 | 繁體中文名稱 | 官方遊戲入口 |
| --- | --- | --- |
| [airhive](games/airhive.json) | 蜂群戰線 | [airhive.ysgs.app](https://airhive.ysgs.app/) |
| [bunnydoom](games/bunnydoom.json) | 兔兔末日 | [bunnydoom.ysgs.app](https://bunnydoom.ysgs.app/) |
| [bushwhack](games/bushwhack.json) | 草叢突擊 | [bushwhack.ysgs.app](https://bushwhack.ysgs.app/) |
| [hiddenshade](games/hiddenshade.json) | 藏影迷城 | [hiddenshade.ysgs.app](https://hiddenshade.ysgs.app/) |
| [nightreap](games/nightreap.json) | 永夜收割 | [nightreap.ysgs.app](https://nightreap.ysgs.app/) |
| [slimegarden](games/slimegarden.json) | 史萊姆花園 | [slimegarden.ysgs.app](https://slimegarden.ysgs.app/) |
| [starwardbastion](games/starwardbastion.json) | 星域防線 | [starwardbastion.ysgs.app](https://starwardbastion.ysgs.app/) |

### 來源與翻譯維護

- 以 `https://gh.ysgs.app/` 的遊戲清單、官方遊戲頁面及其公開原始碼查證名稱、玩法、入口與封面。
- 分類使用既有字典，依來源類型映射；不要為來源宣傳用詞一律新增分類。
- 英文與日文描述可忠實翻譯來源介紹，但不得加上來源未支持的功能；這些資料文案不宣稱是遊戲本身的官方譯文。
- 有已確認的官方在地化名稱時優先採用；沒有時保留既有英文遊戲名，不自行創造正式日文名稱。
- `launchUrls` 只能使用該遊戲已確認的語言切換方式。沒有證據時省略，使用端回到通用 `url`。
- 七款封面皆引用各遊戲原始網站的圖片 URL，不下載檔案。外部圖片不受本倉庫授權重新授權，使用仍須遵循來源權利與條款。
- 資料網站預定路徑為 `/allgames.json` 與 `/games/<id>.json`；只有實際部署後才可聲稱這些新端點已公開可用。

### 原始封面連結

更新封面時重新查證原始遊戲頁面，不從工作室首頁的 `assets/` 圖片建立轉存依賴：

| ID | `cover` |
| --- | --- |
| `airhive` | `https://airhive.ysgs.app/assets/social/og-image.png` |
| `bunnydoom` | `https://bunnydoom.ysgs.app/assets/icons/og.jpg` |
| `bushwhack` | `https://bushwhack.ysgs.app/assets/og-cover.png` |
| `hiddenshade` | `https://hiddenshade.ysgs.app/assets/og.png` |
| `nightreap` | `https://nightreap.ysgs.app/assets/social/nightreap-social.png` |
| `slimegarden` | `https://slimegarden.ysgs.app/assets/og-image.png` |
| `starwardbastion` | `https://starwardbastion.ysgs.app/icons/og-image.png` |
