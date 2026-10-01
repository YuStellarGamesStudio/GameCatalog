# GameCatalog

**YSGS 遊戲資料網站 / YSGS Game Data Website**

GameCatalog 提供可直接取用的靜態遊戲資料、參照索引與三語分類字典，讓網站、應用程式與工具共用一致的遊戲資訊及分類識別碼。

GameCatalog provides static game records, a reference index, and a multilingual category dictionary so websites, applications, and tools can share consistent game metadata and category identifiers.

[繁體中文](#traditional-chinese) · [English](#english)

| 資源 / Resource | 連結 / Link |
| --- | --- |
| 網站 / Website | [data.ysgs.app](https://data.ysgs.app/) |
| 分類資料 / Category data | [categories.json](https://data.ysgs.app/categories.json) |
| 遊戲參照索引 / Game reference index | [allgames.json](allgames.json) |
| 單一遊戲範例 / Individual game example | [games/hiddenshade.json](games/hiddenshade.json) |
| 原始碼 / Source repository | [YuStellarGamesStudio/GameCatalog](https://github.com/YuStellarGamesStudio/GameCatalog) |
| 安全政策 / Security policy | [SECURITY.md](SECURITY.md) |
| 授權 / License | [Apache License 2.0](LICENSE) |

<a id="traditional-chinese"></a>

## 繁體中文

### 1. 網站定位

GameCatalog 是 YuStellarGamesStudio 的遊戲資料倉庫與靜態發布網站。它提供可供程式讀取、版本控制的遊戲紀錄與分類字典，而不是透過後端動態查詢遊戲資料。

目前的主要資料為 [`categories.json`](categories.json)，包含 **47 種常見遊戲分類**。每個分類都提供英文、繁體中文與日文名稱，適合用於：

- 遊戲目錄或商店的分類名稱顯示。
- 前端分類選單、標籤與篩選器的資料來源。
- 遊戲管理工具中的分類欄位與多語文字映射。
- 不同網站或應用程式之間共用的分類識別碼。
- 靜態網站、資料處理腳本及本地工具的分類參照表。

上述選單與篩選器是**資料的使用情境**，並不是本倉庫已實作的互動介面。

另外提供來自 [官方遊戲首頁](https://gh.ysgs.app/) 的 **7 款遊戲紀錄**，存放於 `games/`。根目錄 [`allgames.json`](allgames.json) 只列出遊戲 `id` 與資料檔案 `path`，詳細名稱、描述、封面、分類及啟動網址由單一遊戲檔案提供。

### 2. 目前提供的功能與範圍

| 功能 | 說明 |
| --- | --- |
| 靜態分類資料 | 以單一 JSON 檔案提供完整分類字典，可以下載或透過 HTTP 讀取。 |
| 單一遊戲資料 | `games/<id>.json` 提供三語名稱與描述、入口、原始封面連結、分類、tags 與發布狀態。 |
| 輕量參照索引 | `allgames.json` 只列出 `id` 與 `path`，不複製遊戲詳細欄位；使用端可按需載入。 |
| 三語分類名稱 | 每個分類包含 `en`、`zh-TW`、`ja` 三個語言欄位，由使用端選擇顯示語言。 |
| 共用分類識別碼 | 使用不依賴顯示語言的 key，例如 `strategy`、`action_rpg`。 |
| 多種類型覆蓋 | 涵蓋動作、冒險、角色扮演、策略、模擬、射擊、益智、運動等常見類型及部分子類型。 |
| 靜態網站設定 | 使用 Jekyll 的 `jekyll-theme-tactile` 主題，並設定 `jekyll-readme-index` 外掛。 |
| 自訂網域設定 | 根目錄 `CNAME` 指定 `data.ysgs.app`，實際發布仍取決於 GitHub Pages 與 DNS 設定。 |
| 公開版本控制 | 資料與文件維護於 GitHub，變更可以透過 commit 歷史追蹤。 |
| 安全與授權文件 | 提供安全通報政策與 Apache License 2.0 授權條款。 |

**目前沒有提供：**互動式遊戲詳細頁、搜尋或推薦引擎、帳號系統、收藏功能、線上資料編輯器，以及動態查詢 API。遊戲紀錄與三語欄位是靜態資料，不代表網站已有遊戲瀏覽介面或語言切換按鈕。

網站根路徑與 JSON 資料路徑是不同資源。某個頁面尚未部署或顯示 404，不一定表示分類檔案也無法使用；應分別檢查。

### 3. 分類涵蓋內容

以下為便於理解的分組，**不是 JSON 中的階層結構**。完整識別碼與名稱請以 `categories.json` 為準。

| 分組 | 代表分類 |
| --- | --- |
| 動作與冒險 | 動作、冒險、動作冒險、平台動作、清版動作、潛行、類銀河戰士惡魔城 |
| 角色扮演 | 角色扮演、動作角色扮演、戰術角色扮演、大型多人線上角色扮演 |
| 策略 | 策略、即時策略、回合制策略、塔防 |
| 模擬與建造 | 模擬、生活模擬、模擬經營、城市建造、農場模擬、沙盒 |
| 生存與恐怖 | 生存、恐怖、生存恐怖 |
| 射擊與競技 | 射擊、第一人稱射擊、第三人稱射擊、清版射擊、大逃殺、多人線上戰鬥競技場、格鬥 |
| 隨機探索 | Roguelike、Roguelite |
| 休閒與解謎 | 益智解謎、休閒、街機、放置 |
| 音樂與運動 | 音樂節奏、競速、運動 |
| 卡牌與桌上遊戲 | 卡牌、牌組構築、桌上遊戲、派對 |
| 敘事與其他 | 視覺小說、戀愛模擬、教育 |

分類可能重疊，例如一款遊戲可能同時是 `action_rpg` 與 `survival`。本檔案沒有規定遊戲只能屬於一個分類，也沒有建立父子分類關係、排序優先權或遊戲與分類之間的對應資料。

### 4. JSON 結構與語言欄位

資料根節點是一個 JSON object，**不是 array**。每個屬性名稱是分類識別碼，其值是三語名稱物件：

```json
{
  "strategy": {
    "en": "Strategy",
    "zh-TW": "策略",
    "ja": "ストラテジー"
  },
  "casual": {
    "en": "Casual",
    "zh-TW": "休閒",
    "ja": "カジュアル"
  }
}
```

這是完整檔案的節錄，不代表資料只有兩種分類。

| 欄位 | 型別 | 用途 |
| --- | --- | --- |
| 分類 key | String，作為根物件的屬性名稱 | 識別分類，例如 `strategy` 或 `turn_based_strategy`。 |
| `en` | String | 英文顯示名稱。 |
| `zh-TW` | String | 繁體中文顯示名稱。 |
| `ja` | String | 日文顯示名稱。 |

使用時請注意：

- 分類 key 使用小寫英文字母，複合名稱以底線分隔；不要用翻譯後的名稱當作資料識別碼。
- 三種語言的名稱位於同一份檔案，不需要分別請求語言專用 URL。
- 欄位名稱區分大小寫；繁體中文欄位為 `zh-TW`，不是 `zh` 或 `zh-tw`。
- JavaScript 存取 `zh-TW` 時應使用中括號，例如 `categories.strategy["zh-TW"]`。
- 名稱是顯示文字，應當作純文字處理，而不是 HTML 或可執行內容。
- JSON 屬性順序不代表排名、推薦程度或穩定排序；需要排序時由使用端處理。
- 分類 key 與顯示名稱都可能隨維護調整，本專案目前沒有另外公布版本化 API 或相容性保證。

### 5. 如何取用資料

#### 5.1. 直接讀取

- 發布後的網站資料：[https://data.ysgs.app/categories.json](https://data.ysgs.app/categories.json)。
- GitHub 上的原始資料：[categories.json](https://github.com/YuStellarGamesStudio/GameCatalog/blob/main/categories.json)。
- 本地 clone 後的資料：倉庫根目錄 `categories.json`。

這是靜態 JSON 資源，不是接受查詢參數的搜尋服務。使用端應下載字典後自行選擇分類與語言；目前沒有定義分頁、登入、API key、寫入端點或伺服器端篩選規則。

#### 5.2. JavaScript 範例

以下示範讀取資料、列出分類數量，以及取得策略分類的繁體中文名稱：

```javascript
async function main() {
  const response = await fetch("https://data.ysgs.app/categories.json");
  if (!response.ok) {
    throw new Error(`HTTP ${response.status}`);
  }

  const categories = await response.json();
  const categoryId = "strategy";
  const language = "zh-TW";
  const category = categories[categoryId];

  if (!category || typeof category[language] !== "string") {
    throw new Error(`Unknown category or language: ${categoryId}/${language}`);
  }

  console.log(Object.keys(categories).length);
  console.log(category[language]);
}

main().catch(console.error);
```

以目前資料執行時，輸出為 `47` 與 `策略`。這個數字不是固定限制；新增分類後會改變。

若要將字典轉成選單資料，可在取得 `categories` 後使用：

```javascript
const options = Object.entries(categories).map(([id, names]) => ({
  id,
  label: names["zh-TW"]
}));
```

第二段需要前一段解析出的 `categories` 物件；它不是單獨發出請求的完整程式。插入網頁時應使用 `textContent` 或框架的文字繫結，不要直接將名稱放進 `innerHTML`。

跨網域瀏覽器請求仍受 CORS 與使用端 Content Security Policy 限制。若遇到限制，請檢查回應標頭及使用端設定，不要關閉瀏覽器安全機制。伺服器端讀取或建置時下載是另外的使用方式。

#### 5.3. Python 範例

此範例使用 Python 3 標準函式庫，不需要安裝額外套件，並明確指定應用程式的 `User-Agent` 與 JSON 接受標頭。若收到 HTTP 403，請確認託管服務對請求的限制；不要關閉 TLS 驗證或繞過存取控制。

```python
import json
from urllib.request import Request, urlopen

request = Request(
    "https://data.ysgs.app/categories.json",
    headers={"User-Agent": "GameCatalog-README/1.0", "Accept": "application/json"},
)
with urlopen(request, timeout=15) as response:
    categories = json.load(response)

print(len(categories))
print(categories["strategy"]["en"])
print(categories["strategy"]["zh-TW"])
print(categories["strategy"]["ja"])
```

以目前資料執行時，輸出依序為 `47`、`Strategy`、`策略`、`ストラテジー`。

#### 5.4. 整合建議

- 儲存分類 key，顯示時再依語言取得名稱，避免翻譯修正影響儲存資料。
- 對未知的分類 key、語言代碼、網路錯誤與 JSON 解析錯誤提供明確處理。
- 可以快取分類字典，避免在每個分類標籤顯示時重複下載；快取更新策略由使用端決定。
- 如需可重現的建置，使用固定 commit 中的資料，不要假設 `main` 或網站檔案永遠不變。
- 從其他網站或 GitHub 讀取時，遵守服務供應者的使用條款；本專案不承諾固定速率限制或可用性 SLA。

#### 5.5. 使用 `allgames.json` 查找遊戲資料

[`allgames.json`](allgames.json) 是參照索引，不是完整紀錄的集合。根物件有 `schemaVersion: 1` 與 `games` 陣列；陣列每項**只有 `id`、`path`**，例如：

```json
{
  "id": "hiddenshade",
  "path": "/games/hiddenshade.json"
}
```

這是索引中的一個元素，不是整份索引。`path` 指向資料網站上的 JSON 檔案，不是遊戲啟動網址；實際遊玩入口要再讀取遊戲紀錄的 `url` 或已提供的 `launchUrls`。

取用流程：

1. 讀取 `/allgames.json`，查看 `games` 中的參照。
2. 以 `id` 找到需要的遊戲；索引按 `id` 升冪排序，排序不代表推薦順序。
3. 用資料網站的 origin 解析 `path`，並載入對應 JSON。
4. 從 `locales["zh-TW"]`、`locales.en` 或 `locales.ja` 取得名稱與描述，分類名稱另由 `categories.json` 查找。
5. 啟動時使用 `launchUrls[所選語言]`；未提供則使用 `url`，不要自行推測語言參數。

目前的七款紀錄：

| ID | 遊戲名稱 | 資料檔案 |
| --- | --- | --- |
| `airhive` | 蜂群戰線 / Airhive | [airhive.json](games/airhive.json) |
| `bunnydoom` | 兔兔末日 / Bunny Doom: Last Pomeranian | [bunnydoom.json](games/bunnydoom.json) |
| `bushwhack` | 草叢突擊 / Bushwhack | [bushwhack.json](games/bushwhack.json) |
| `hiddenshade` | 藏影迷城 / HiddenShade | [hiddenshade.json](games/hiddenshade.json) |
| `nightreap` | 永夜收割 / Nightreap | [nightreap.json](games/nightreap.json) |
| `slimegarden` | 史萊姆花園 / Slimegarden | [slimegarden.json](games/slimegarden.json) |
| `starwardbastion` | 星域防線 / Starward Bastion | [starwardbastion.json](games/starwardbastion.json) |

以下範例搭配第 7 節的本地檔案伺服器，只請求索引與所選的藏影迷城紀錄，不一次下載所有遊戲：

```javascript
async function main() {
  const baseUrl = "http://127.0.0.1:8000/";
  const indexResponse = await fetch(new URL("/allgames.json", baseUrl));
  if (!indexResponse.ok) {
    throw new Error(`Index HTTP ${indexResponse.status}`);
  }

  const index = await indexResponse.json();
  const reference = index.games.find(({ id }) => id === "hiddenshade");
  if (!reference) {
    throw new Error("Game not found: hiddenshade");
  }

  const gameResponse = await fetch(new URL(reference.path, baseUrl));
  if (!gameResponse.ok) {
    throw new Error(`Game HTTP ${gameResponse.status}`);
  }

  const game = await gameResponse.json();
  if (game.id !== reference.id) {
    throw new Error("Game ID does not match the index reference");
  }

  console.log(index.games.length);
  console.log(game.locales["zh-TW"].name);
}

main().catch(console.error);
```

目前輸出為 `7` 與 `藏影迷城`。等這批資料成功部署後，可將 `baseUrl` 改為 `https://data.ysgs.app/`；僅存在於本地的檔案不表示公開端點已更新。

封面 `cover` 直接引用各遊戲原始網站的 HTTPS 圖片連結，不在本倉庫下載或重新託管。資料文案依來源介紹翻譯；資料支援某個語言不代表遊戲本身必然提供該語言介面。需要時應檢查已提供的 `launchUrls` 與遊戲實際功能。

新增、刪除或重新命名遊戲時同步維護索引；只修改文案、封面或分類時，只更新 `games/<id>.json`，不把詳細內容加入 `allgames.json`。

### 6. 倉庫檔案說明

```text
GameCatalog/
├── AGENTS.md
├── CLAUDE.md
├── CNAME
├── LICENSE
├── README.md
├── SECURITY.md
├── _config.yml
├── allgames.json
├── categories.json
└── games/
    ├── airhive.json
    ├── bunnydoom.json
    ├── bushwhack.json
    ├── hiddenshade.json
    ├── nightreap.json
    ├── slimegarden.json
    └── starwardbastion.json
```

| 檔案 | 說明 |
| --- | --- |
| `categories.json` | 分類識別碼與英文、繁體中文、日文名稱。 |
| `allgames.json` | 只有 `id` 與 `path` 的遊戲參照索引。 |
| `games/*.json` | 七款遊戲的完整紀錄，是詳細內容的唯一維護來源。 |
| `README.md` | 本文件，提供中英雙語的網站與資料使用說明。 |
| `AGENTS.md` | 分類與遊戲資料撰寫規範，含 `games/*.json` 完整文件範例。 |
| `CLAUDE.md` | 直接引用 `AGENTS.md` 的 Claude Code 指引入口。 |
| `_config.yml` | Jekyll 主題與外掛設定。 |
| `CNAME` | GitHub Pages 自訂網域設定。 |
| `SECURITY.md` | 安全問題範圍、私密通報方法與協調揭露政策。 |
| `LICENSE` | Apache License 2.0 完整授權條款。 |

目前沒有提供應用程式後端、資料庫、套件安裝清單或自訂部署 workflow；不需要假設有 `npm install`、`npm run build` 或其他本專案專用的建置命令。

### 7. 網站發布與本地查看

#### 7.1. Jekyll 設定

目前 `_config.yml` 內容為：

```yaml
theme: jekyll-theme-tactile
plugins:
  - jekyll-readme-index
```

`jekyll-theme-tactile` 提供網站主題；`jekyll-readme-index` 可在符合外掛條件且沒有其他首頁時，將 README 作為首頁來源。實際結果取決於選定的 GitHub Pages 建置方式是否載入該外掛，不是僅新增 README 就保證網站立即更新。

#### 7.2. GitHub Pages 發布注意事項

管理者應確認：

1. GitHub Pages 已在倉庫設定中啟用，並選定正確的發布來源。
2. 若採用從分支發布，來源分支與資料夾包含根目錄的 `_config.yml`、`README.md` 與 `categories.json`。
3. 自訂網域設定為 `data.ysgs.app`，且 DNS 依 GitHub Pages 的要求正確設定。
4. HTTPS 憑證與強制 HTTPS 選項在平台支援時已正確設定。
5. 建置與發布成功，並分別確認 `/` 與 `/categories.json` 的結果。

`CNAME` 不會自行修改 DNS，也不會替你啟用 GitHub Pages。Git push 與網站部署完成是不同事件，發布及快取更新可能需要時間。

官方設定文件：[GitHub Pages documentation](https://docs.github.com/en/pages)。

#### 7.3. 本地閱讀與靜態檔案查看

```sh
git clone https://github.com/YuStellarGamesStudio/GameCatalog.git
cd GameCatalog
python3 -m json.tool categories.json
```

最後一行會解析並格式化輸出 JSON，可用來檢查基本語法，但不會驗證翻譯品質或所有資料規則。

若已安裝 Python 3，可在倉庫根目錄啟動僅限本機存取的檔案伺服器：

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

然後開啟 `http://127.0.0.1:8000/categories.json`。使用 `Ctrl+C` 結束。

**此命令不會執行 Jekyll，也不會把 README 轉成網站首頁。** 它只提供原始檔案。請在沒有私密檔案的工作目錄執行；不要將這個開發伺服器用於正式發布。本倉庫目前沒有提供完整的本地 Jekyll 依賴鎖定設定。

### 8. 資料維護與貢獻

一般分類新增、翻譯修正與文件改善可透過 GitHub issue 或 pull request 討論。

修改分類時建議遵循：

1. 先確認沒有同義或重複分類，避免因顯示名稱不同建立多個相同概念。
2. 新 key 採用小寫英文與底線，並確認對現有使用端的影響。
3. 同時提供 `en`、`zh-TW`、`ja` 三個非空字串。
4. 繁體中文使用繁體字，日文採常見遊戲類型表達，專有名詞保留合理的慣用寫法。
5. 保持既有 JSON 縮排與結構，不加入註解、尾隨逗號或重複 key。
6. 若重新命名或刪除 key，在變更說明中交代原因及使用端可能需要的調整。
7. 執行 JSON 語法檢查，並確認受影響的語言查找仍能取得正確名稱。
8. 如分類數量、資料結構或操作方式改變，同步更新 README 的中英說明與範例。

這些是貢獻指引，不代表倉庫已安裝自動驗證或 CI 檢查。

完整的分類、遊戲資料與參照索引撰寫契約請參閱 [AGENTS.md](AGENTS.md)，其中的 `games/hiddenshade.json` 範例與實際紀錄一致。`CLAUDE.md` 使用 `@AGENTS.md` 共用同一份規範。

### 9. 安全與授權

若發現漏洞、憑證外洩或惡意內容，請先閱讀 [`SECURITY.md`](SECURITY.md)。不要在公開 issue、pull request 或 commit 中發布敏感資訊與未修復漏洞的利用細節。GitHub private reporting 是否可用，取決於管理者是否另外啟用。

本專案採用 [Apache License 2.0](LICENSE)。使用、修改或再散布時，請遵守授權與通知要求。分類資料不是對任何第三方遊戲、商店或下載內容的安全保證或背書。

<a id="english"></a>

## English

### 1. Website Purpose

GameCatalog is YuStellarGamesStudio's game data repository and static publication website. It provides machine-readable, version-controlled game records and a category dictionary rather than querying game records through a dynamic backend.

The primary dataset is [`categories.json`](categories.json), which currently contains **47 common game categories**. Every category includes English, Traditional Chinese, and Japanese labels. The data can be used for:

- Category labels in game catalogs or storefronts.
- Category menus, tags, and filter controls in frontend applications.
- Category fields and localized label mappings in game management tools.
- Shared category identifiers across websites and applications.
- Reference data for static sites, data-processing scripts, and local tools.

Menus and filters are **consumer use cases**, not interactive interfaces implemented in this repository.

It also includes **7 game records** from the [official game listing](https://gh.ysgs.app/) under `games/`. The root [`allgames.json`](allgames.json) contains only each game's `id` and data file `path`; individual records supply names, descriptions, covers, categories, and launch URLs.

### 2. Available Features and Scope

| Feature | Description |
| --- | --- |
| Static category data | A complete dictionary in one JSON file, available for download or HTTP retrieval. |
| Individual game records | `games/<id>.json` supplies localized names and descriptions, entry points, original cover links, categories, tags, and publication status. |
| Lightweight reference index | `allgames.json` contains only `id` and `path`, without duplicating detailed fields; consumers can load records on demand. |
| Three-language labels | Every category includes `en`, `zh-TW`, and `ja`; the consuming application chooses the display language. |
| Shared category identifiers | Language-independent keys such as `strategy` and `action_rpg`. |
| Broad genre coverage | Common genres and selected subgenres, including action, adventure, role-playing, strategy, simulation, shooters, puzzles, and sports. |
| Static site configuration | Jekyll configuration using `jekyll-theme-tactile` and `jekyll-readme-index`. |
| Custom domain configuration | The root `CNAME` specifies `data.ysgs.app`; publication still depends on GitHub Pages and DNS configuration. |
| Public version history | Data and documentation are maintained on GitHub with changes traceable through commits. |
| Security and licensing documents | A security reporting policy and Apache License 2.0 terms. |

**Not currently provided:** interactive game detail pages, a search or recommendation engine, accounts, favorites, an online data editor, or a dynamic query API. Game records and multilingual labels are static data; they do not imply that a game browsing interface or language-switching control exists.

The website root and the JSON path are separate resources. An unpublished page or a 404 at one path does not necessarily mean the category file is unavailable; check each resource independently.

### 3. Category Coverage

The groups below are for readability and **are not a hierarchy in the JSON file**. Use `categories.json` as the authoritative list of identifiers and labels.

| Group | Representative categories |
| --- | --- |
| Action and adventure | Action, Adventure, Action Adventure, Platformer, Beat 'em Up, Stealth, Metroidvania |
| Role-playing | Role-Playing, Action RPG, Tactical RPG, Massively Multiplayer Online RPG |
| Strategy | Strategy, Real-Time Strategy, Turn-Based Strategy, Tower Defense |
| Simulation and building | Simulation, Life Simulation, Management, City Building, Farming, Sandbox |
| Survival and horror | Survival, Horror, Survival Horror |
| Shooters and competitive genres | Shooter, First-Person Shooter, Third-Person Shooter, Shoot 'em Up, Battle Royale, Multiplayer Online Battle Arena, Fighting |
| Randomized exploration | Roguelike, Roguelite |
| Casual and puzzles | Puzzle, Casual, Arcade, Idle |
| Music and sports | Rhythm, Racing, Sports |
| Cards and tabletop | Card, Deckbuilding, Board, Party |
| Narrative and other | Visual Novel, Dating Simulation, Educational |

Categories can overlap: a game might fit both `action_rpg` and `survival`. The dictionary does not enforce one category per game, define parent-child relationships or ranking, or contain game-to-category assignments.

### 4. JSON Structure and Language Fields

The root is a JSON object, **not an array**. Each property name is a category identifier, and its value is an object containing three labels:

```json
{
  "strategy": {
    "en": "Strategy",
    "zh-TW": "策略",
    "ja": "ストラテジー"
  },
  "casual": {
    "en": "Casual",
    "zh-TW": "休閒",
    "ja": "カジュアル"
  }
}
```

This is an excerpt of the full dictionary, showing only two categories.

| Field | Type | Purpose |
| --- | --- | --- |
| Category key | String used as a root object property | Identifies the category, for example `strategy` or `turn_based_strategy`. |
| `en` | String | English display label. |
| `zh-TW` | String | Traditional Chinese display label. |
| `ja` | String | Japanese display label. |

Usage considerations:

- Keys use lowercase English letters and underscores for compound names. Do not use translated labels as identifiers.
- All three languages are in the same file; separate language-specific URLs are unnecessary.
- Field names are case-sensitive. The Traditional Chinese field is `zh-TW`, not `zh` or `zh-tw`.
- Use bracket notation for `zh-TW` in JavaScript, such as `categories.strategy["zh-TW"]`.
- Treat labels as plain text, not HTML or executable content.
- Property order does not define ranking, recommendations, or a stable sort order. Consumers should apply their own sorting.
- Identifiers and labels may change during maintenance. No separately versioned API or compatibility guarantee is currently published.

### 5. Accessing the Data

#### 5.1. Direct access

- Published website data: [https://data.ysgs.app/categories.json](https://data.ysgs.app/categories.json).
- Repository source: [categories.json](https://github.com/YuStellarGamesStudio/GameCatalog/blob/main/categories.json).
- Local clone: `categories.json` in the repository root.

This is a static JSON resource, not a search service accepting query parameters. Download the dictionary and select categories and languages in your application. Pagination, authentication, API keys, write endpoints, and server-side filtering are not defined.

#### 5.2. JavaScript example

This example retrieves the dictionary, prints the category count, and reads the Traditional Chinese label for Strategy:

```javascript
async function main() {
  const response = await fetch("https://data.ysgs.app/categories.json");
  if (!response.ok) {
    throw new Error(`HTTP ${response.status}`);
  }

  const categories = await response.json();
  const categoryId = "strategy";
  const language = "zh-TW";
  const category = categories[categoryId];

  if (!category || typeof category[language] !== "string") {
    throw new Error(`Unknown category or language: ${categoryId}/${language}`);
  }

  console.log(Object.keys(categories).length);
  console.log(category[language]);
}

main().catch(console.error);
```

With the current dataset, the output is `47` and `策略`. The count is not a fixed limit and will change when categories are added.

To convert the dictionary into menu options after loading `categories`:

```javascript
const options = Object.entries(categories).map(([id, names]) => ({
  id,
  label: names["zh-TW"]
}));
```

This second snippet requires the parsed `categories` object; it is not a standalone retrieval program. Render labels using `textContent` or framework text bindings instead of inserting them into `innerHTML`.

Cross-origin browser requests remain subject to CORS and the consuming application's Content Security Policy. Check response headers and application settings if access is blocked; do not disable browser protections. Server-side retrieval or downloading data during a build are alternative integration approaches.

#### 5.3. Python example

This example uses the Python 3 standard library and requires no additional packages. It explicitly identifies the application through `User-Agent` and requests JSON. If you receive HTTP 403, check the hosting service's request restrictions; do not disable TLS verification or bypass access controls.

```python
import json
from urllib.request import Request, urlopen

request = Request(
    "https://data.ysgs.app/categories.json",
    headers={"User-Agent": "GameCatalog-README/1.0", "Accept": "application/json"},
)
with urlopen(request, timeout=15) as response:
    categories = json.load(response)

print(len(categories))
print(categories["strategy"]["en"])
print(categories["strategy"]["zh-TW"])
print(categories["strategy"]["ja"])
```

The current output is `47`, `Strategy`, `策略`, and `ストラテジー`, in that order.

#### 5.4. Integration guidance

- Store identifiers and resolve labels at display time so translation changes do not alter stored references.
- Handle unknown identifiers, unsupported language codes, network failures, and JSON parsing errors explicitly.
- Cache the dictionary rather than downloading it for every label; consumers choose their own refresh strategy.
- For reproducible builds, use data from a fixed commit instead of assuming that `main` or the website file is immutable.
- Follow hosting providers' terms when retrieving data. This project does not promise fixed rate limits or an availability SLA.

#### 5.5. Finding game records through `allgames.json`

[`allgames.json`](allgames.json) is a reference index, not a collection of complete records. Its root contains `schemaVersion: 1` and a `games` array. Each array element has **only `id` and `path`**, for example:

```json
{
  "id": "hiddenshade",
  "path": "/games/hiddenshade.json"
}
```

This is one index entry, not the entire index. `path` locates a JSON file on the data website, not a game launch page. Load the referenced record to obtain the actual `url` or supported `launchUrls`.

Retrieval workflow:

1. Load `/allgames.json` and inspect its `games` references.
2. Find the desired `id`. Entries are sorted by `id`, not by recommendation.
3. Resolve `path` against the data website's origin and retrieve that JSON file.
4. Read names and descriptions from `locales["zh-TW"]`, `locales.en`, or `locales.ja`. Resolve category labels separately through `categories.json`.
5. Launch using `launchUrls[selectedLanguage]` when provided; otherwise use `url` without inventing language parameters.

Current records:

| ID | Game name | Data file |
| --- | --- | --- |
| `airhive` | 蜂群戰線 / Airhive | [airhive.json](games/airhive.json) |
| `bunnydoom` | 兔兔末日 / Bunny Doom: Last Pomeranian | [bunnydoom.json](games/bunnydoom.json) |
| `bushwhack` | 草叢突擊 / Bushwhack | [bushwhack.json](games/bushwhack.json) |
| `hiddenshade` | 藏影迷城 / HiddenShade | [hiddenshade.json](games/hiddenshade.json) |
| `nightreap` | 永夜收割 / Nightreap | [nightreap.json](games/nightreap.json) |
| `slimegarden` | 史萊姆花園 / Slimegarden | [slimegarden.json](games/slimegarden.json) |
| `starwardbastion` | 星域防線 / Starward Bastion | [starwardbastion.json](games/starwardbastion.json) |

Run this example with the local file server in Section 7. It requests the index and the selected HiddenShade record, not every game:

```javascript
async function main() {
  const baseUrl = "http://127.0.0.1:8000/";
  const indexResponse = await fetch(new URL("/allgames.json", baseUrl));
  if (!indexResponse.ok) {
    throw new Error(`Index HTTP ${indexResponse.status}`);
  }

  const index = await indexResponse.json();
  const reference = index.games.find(({ id }) => id === "hiddenshade");
  if (!reference) {
    throw new Error("Game not found: hiddenshade");
  }

  const gameResponse = await fetch(new URL(reference.path, baseUrl));
  if (!gameResponse.ok) {
    throw new Error(`Game HTTP ${gameResponse.status}`);
  }

  const game = await gameResponse.json();
  if (game.id !== reference.id) {
    throw new Error("Game ID does not match the index reference");
  }

  console.log(index.games.length);
  console.log(game.locales["zh-TW"].name);
}

main().catch(console.error);
```

The current output is `7` and `藏影迷城`. After this data has been successfully deployed, change `baseUrl` to `https://data.ysgs.app/` if desired. Local files alone do not establish that the public endpoints have been updated.

Each `cover` directly references an HTTPS image on the original game website. Images are not downloaded or rehosted in this repository. Descriptions are translated from source material; localized catalog metadata does not guarantee that the game itself offers the same interface language. Check the supplied `launchUrls` and the actual game's capabilities.

Update the index when adding, deleting, or renaming a game. Changes to descriptions, covers, or categories belong only in `games/<id>.json`; do not copy those fields into `allgames.json`.

### 6. Repository Files

```text
GameCatalog/
├── AGENTS.md
├── CLAUDE.md
├── CNAME
├── LICENSE
├── README.md
├── SECURITY.md
├── _config.yml
├── allgames.json
├── categories.json
└── games/
    ├── airhive.json
    ├── bunnydoom.json
    ├── bushwhack.json
    ├── hiddenshade.json
    ├── nightreap.json
    ├── slimegarden.json
    └── starwardbastion.json
```

| File | Description |
| --- | --- |
| `categories.json` | Category identifiers with English, Traditional Chinese, and Japanese labels. |
| `allgames.json` | Game reference index containing only `id` and `path` per entry. |
| `games/*.json` | Complete records for seven games, the sole maintenance source for detailed content. |
| `README.md` | This bilingual website and data usage guide. |
| `AGENTS.md` | Category and game data authoring rules, including a complete documented `games/*.json` example. |
| `CLAUDE.md` | Claude Code instruction entry point directly importing `AGENTS.md`. |
| `_config.yml` | Jekyll theme and plugin configuration. |
| `CNAME` | Custom domain configuration for GitHub Pages. |
| `SECURITY.md` | Security scope, private reporting guidance, and coordinated disclosure policy. |
| `LICENSE` | Full Apache License 2.0 terms. |

There is currently no application backend, database, package installation manifest, or custom deployment workflow. Do not assume that `npm install`, `npm run build`, or another project-specific build command exists.

### 7. Publication and Local Inspection

#### 7.1. Jekyll configuration

The current `_config.yml` contains:

```yaml
theme: jekyll-theme-tactile
plugins:
  - jekyll-readme-index
```

`jekyll-theme-tactile` supplies the site theme. When its conditions are met and no competing index exists, `jekyll-readme-index` can use the README as the homepage source. The selected GitHub Pages build process must load the plugin; adding a README alone does not guarantee an immediate website update.

#### 7.2. GitHub Pages publication checklist

Repository administrators should confirm that:

1. GitHub Pages is enabled with the correct publication source.
2. For branch-based publication, the selected branch and directory contain the root `_config.yml`, `README.md`, and `categories.json`.
3. The custom domain is `data.ysgs.app`, with DNS configured according to GitHub Pages requirements.
4. HTTPS certificate provisioning and HTTPS enforcement are correctly configured where supported.
5. The build and deployment complete successfully, and both `/` and `/categories.json` are checked separately.

`CNAME` does not modify DNS or enable GitHub Pages by itself. Pushing a commit and completing a deployment are separate events; publication and cache refreshes may take time.

Official setup reference: [GitHub Pages documentation](https://docs.github.com/en/pages).

#### 7.3. Reading and serving files locally

```sh
git clone https://github.com/YuStellarGamesStudio/GameCatalog.git
cd GameCatalog
python3 -m json.tool categories.json
```

The last command parses and pretty-prints the JSON. It checks basic syntax, not translation quality or every data constraint.

With Python 3 installed, start a loopback-only file server from the repository root:

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

Open `http://127.0.0.1:8000/categories.json`, and stop the server with `Ctrl+C`.

**This does not run Jekyll or turn the README into a homepage.** It serves raw files only. Run it from a directory without private files, and do not use this development server for production publication. The repository does not currently provide a complete, locked local Jekyll dependency setup.

### 8. Data Maintenance and Contributions

Use GitHub issues or pull requests to discuss ordinary category additions, translation corrections, and documentation improvements.

When changing categories:

1. Check for existing equivalent categories before introducing a duplicate concept under a different name.
2. Use lowercase English keys with underscores, and consider the impact on existing consumers.
3. Supply non-empty string values for `en`, `zh-TW`, and `ja` together.
4. Use Traditional Chinese characters and customary Japanese genre terminology, retaining established technical names where appropriate.
5. Preserve the JSON structure and indentation; do not add comments, trailing commas, or duplicate keys.
6. Explain identifier renames or removals and any consumer changes they require.
7. Check JSON syntax and confirm affected language lookups still return the intended labels.
8. Update both language sections and examples when category counts, data structure, or usage changes.

These are contribution guidelines, not a claim that automated validation or CI checks are configured.

See [AGENTS.md](AGENTS.md) for the complete category, game record, and reference index authoring contract. Its `games/hiddenshade.json` example matches the actual record. `CLAUDE.md` imports the same rules through `@AGENTS.md`.

### 9. Security and License

For vulnerabilities, exposed credentials, or malicious content, read [`SECURITY.md`](SECURITY.md) first. Do not publish sensitive information or unpatched exploit details in public issues, pull requests, or commits. GitHub private reporting is available only if administrators separately enable it.

The project uses the [Apache License 2.0](LICENSE). Follow its license and notice requirements when using, modifying, or redistributing project content. Category data is not a security guarantee or endorsement of third-party games, stores, or downloads.
