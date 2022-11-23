# OpenAerialMap Frontend [![Build Status](https://travis-ci.org/hotosm/oam-browser.svg?branch=develop)](https://travis-ci.org/hotosm/oam-browser) ![BrowserStack Status](https://www.browserstack.com/automate/badge.svg?badge_key=cXlaWlgyeEhmUUlISEpjTU9OQTg3RzdLVUlqUWo0V0JsOG5sMGJ4MlNnYz0tLWhtNFRWMnBlYWJnQUd6TFFZVzJxK3c9PQ==--955a5de2e9ea1506cdeb8cebdcbca07435613863)

OpenAerialMap (OAM) 是一組用於搜索、共享和使用公開許可的衛星和無人機 (UAV) 圖像的工具。

OAM 建立在Built on top of the [Open Imagery Network](https://openimagerynetwork.github.io/) (OIN),  之上，是一項提供搜索和連結該影像的服務。
![](./contrib/oam_screenshot.jpg)

## Local setup

[Create React App](https://github.com/facebookincubator/create-react-app) 用於搭建、編譯和構建項目。

因此，您首先需要在系統上安裝最新版本的 Node 和 Yarn。然後，在項目的根目錄下，運行；
```bash
yarn install
yarn start
```

你應在你的網站上看到 `http://localhost:3000`

但是，要取得所有功能，你還需要將其指向正在運行的 [Catalog API](https://github.com/hotosm/oam-catalog)。在默認情況下，將使用 API 暫存預設的端點，但是可以在 `src/config/local.js` 中將端點更改為本主機運行的API。

## Deployment

這是一個 Single Page Application，只需要一個網頁伺服器來提供服務。因此它可以託管(?)在 S3 上，也可以僅作為 Nginx 下的文件夾。

後端API URI可以在`src/config.js`中更改

準備檔案:

`yarn build`

複製`build/`資料夾到你的伺服器上S3

## Testing
2 distinct test suites exist.

**Unit-like tests**, 在 `test/specs`下    
這些應該是隔離的和快速的，盡可能多的模擬/存根，適合 TDD。運行:
`mocha --opts test/specs/mocha.opts test/specs` 或 `npm test`

**Integration tests**, under `test/integration`    
這些是端到端的跨瀏覽器測試，應該測試盡可能多的堆棧。目前，它們在針對各種瀏覽器的瀏覽器堆棧上運行。它們可以針對 Web Driver 兼容的瀏覽器客戶端在本地運行，例如[chromedriver](https://sites.google.com/a/chromium.org/chromedriver/) 或 [geckodriver](https://github.com/mozilla/geckodriver). 
需運行 [Catalog API](https://github.com/hotosm/oam-catalog), repo 有一個 Dockerfile 可以快速獲取
正在運行的 API 的本地版本。. 接著可測試;
`wdio test/integration/wdio.local.conf.js`.

請注意，Browserstack 測試 API 的固定版本 (defined in `package.json` and the latest version of the API).

由於 `wdio` 綁定 `mocha`，您可以通過 `wdio.default.conf.js` 的 `mochaOpts` 字段發送 `mocha` 參數。例如 `grep` 已被添加，因此您可以使用以下命令隔離單個測試運行：
`MOCHA_MATCH='should find imagery' wdio test/integration/wdio.local.conf.js`

## Contributing

歡迎投稿. 請參閱 [CONTRIBUTING.md](./CONTRIBUTING.md).

## License
OAM 瀏覽器根據 **BSD 3-Clause License** 獲得許可，請參閱 [LICENSE](LICENSE) 文件了解更多詳細信息。
