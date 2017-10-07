---
title: "aaaCreate Node.js 的 Azure IoT 邊緣模組 |Microsoft 文件"
description: "本教學課程示範如何 toowrite b 資料轉換器模組使用 hello 最新的 Azure IoT 邊緣 NPM 封裝和 Yeoman 產生器。"
services: iot-hub
author: sushi
manager: timlt
ms.service: iot-hub
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: article
ms.date: 06/28/2017
ms.author: sushi
ms.openlocfilehash: d3e696b5a310377ffb8e99998ff0714bf7c0bb41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a>使用 Node.js 建立 Azure IoT Edge 模組

本教學課程示範如何 toocreate JS 中的 Azure IoT 邊緣的模組。

在本教學課程中，我們將逐步檢視環境設定以及如何 toowrite [b](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy)資料轉換器模組使用 hello 最新的 Azure IoT 邊緣 NPM 封裝。

## <a name="prerequisites"></a>必要條件

在本節中，您會針對 IoT Edge 模組設定您的環境。 它會套用 tooboth *64 位元 Windows*和*64 位元 Linux (Ubuntu 14 +)*作業系統。

hello 下列軟體，則需要：
* [Git 用戶端](https://git-scm.com/downloads)。
* [Node LTS](https://nodejs.org)。
* `npm install -g yo`。
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a>架構

hello Azure IoT 邊緣平台大量採用 hello[莫 Neumann 架構](https://en.wikipedia.org/wiki/Von_Neumann_architecture)。 這表示該 hello 整個 Azure IoT 邊緣架構是系統處理輸入和產生輸出。與每個個別的模組也是很小的輸入輸出子系統。 在本教學課程中，我們引進下列兩個模組的 hello:

1. 可接收模擬 [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) 訊號，並將它轉換為格式化 [JSON](https://en.wikipedia.org/wiki/JSON) 訊息的模組。
2. 模組會列印收到 hello [JSON](https://en.wikipedia.org/wiki/JSON)訊息。

hello 下列影像顯示 hello 一般 tooend dataflow 結束這個專案：

![三個模組之間的資料流程](media/iot-hub-iot-edge-create-module/dataflow.png "輸入：模擬 BLE 模組；處理器：轉換器模組；輸出：印表機模組")

## <a name="set-up-hello-environment"></a>設定 hello 環境
以下我們會示範如何 tooquickly 設定環境 toostart toowrite JS 您第一次 b 轉換器模組。

### <a name="create-module-project"></a>建立模組專案
1. 開啟命令列視窗，執行 `yo az-iot-gw-module`。
2. 步驟 hello hello 螢幕 toofinish hello 初始化模組專案。

### <a name="project-structure"></a>專案結構
JS 模組專案包含下列元件的 hello:

`modules`-hello 自訂 JS 模組來源檔案。 取代 hello 預設`sensor.js`和`printer.js`與模組檔案。

`app.js`-hello 項目檔案 toostart hello 邊緣執行個體。

`gw.config.json`-hello 設定檔 toocustomize hello 模組 toobe 載入的邊緣。

`package.json`-hello 模組專案的中繼資料資訊。

`README.md`-hello 模組專案的基本文件。


### <a name="package-file"></a>套件檔案

這`package.json`宣告包含 hello 名稱、 版本、 項目、 指令碼中，執行階段，以及開發相依性的模組專案所需的所有 hello 中繼資料資訊。

下列程式碼片段會示範如何 tooconfigure b 轉換器的範例專案。
```json
{
  "name": "converter",
  "version": "1.0.0",
  "description": "BLE data converter sample for Azure IoT Edge.",
  "repository": {
    "type": "git",
    "url": "https://github.com/Azure-Samples/iot-edge-samples"
  },
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "author": "Microsoft Corporation",
  "license": "MIT",
  "dependencies": {
  },
  "devDependencies": {
    "azure-iot-gateway": "~1.1.3"
  }
}
```


### <a name="entry-file"></a>輸入檔案
hello`app.js`定義 hello 方式 tooinitialize hello 邊緣執行個體。 我們不需要在這裡 toomake 任何變更。

```javascript
(function() {
  'use strict';

  const Gateway = require('azure-iot-gateway');
  let config_path = './gw.config.json';

  // node app.js
  if (process.argv.length < 2) {
    throw 'Calling pattern should be node app.js.';
  }

  const gw = new Gateway(config_path);
  gw.run();
})();
```

### <a name="interface-of-module"></a>模組的介面
您可以將 Azure IoT Edge 模組視為資料處理器，其作業是：接收輸入、加以處理，以及產生輸出。

hello 輸入可能是硬體 （例如動作偵測器） 的資料、 將訊息從其他模組，或任何其他 （例如，計時器會定期產生一個隨機數字）。

hello 輸出類似 toohello 輸入，它可能會觸發硬體 （例如 LED 閃爍不停 hello) 的行為、 訊息 tooother 模組或任何其他 （例如列印 toohello 主控台）。

模組會使用 `message` 物件彼此通訊。 hello**內容**的`message`是可以代表任何一種您想要的資料的位元組陣列。 **屬性**也會提供在 hello `message` ，而只是字串的字串對應。 您可以把**屬性**為 hello 標頭的 HTTP 要求或 hello 中繼資料的檔案。

在順序 toodevelop JS 中的 Azure IoT 邊緣模組，您需要 toocreate 實作所需的 hello 方法的新模組物件`receive()`。 此時，您也可以選擇 tooimplement hello 選擇性`create()`或`start()`，或`destroy()`以及方法。 下列程式碼片段的 hello 顯示 hello JS 模組物件的 scaffolding。

```javascript
'use strict';

module.exports = {
  broker: null,
  configuration: null,

  create: function (broker, configuration) {
    // Default implementation.
    this.broker = broker;
    this.configuration = configuration;

    return true;
  },

  start: function () {
    // Produce
  },

  receive: function (message) {
    // Consume
  },

  destroy: function () {
  }
};
```

### <a name="converter-module"></a>轉換器模組
| 輸入                    | 處理器                              | 輸出                 | 來源檔案            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| 溫度資料訊息 | 剖析並建構新的 JSON 訊息 | 建構 JSON 訊息 | `converter.js` |

此模組是典型的 Azure IoT Edge 模組。 它可接受從其他模組溫度訊息 (硬體模組，或在此情況下我們模擬的 b 模組)。然後再正規化結構化的 tooa JSON 訊息 （包括附加 hello 訊息識別碼，我們是否需要 tootrigger hello 溫度警示，hello 屬性設定等） 中的 hello 溫度訊息。

```javascript
receive: function (message) {
  // Initialize hello messageCount in global object at first time.
  if (!global.messageCount) {
    global.messageCount = 0;
  }

  // Read hello content and properties objects from message.
  let rawContent = JSON.parse(Buffer.from(message.content).toString('utf8'));
  let rawProperties = message.properties;

  // Generate new properties object.
  let newProperties = {
    source: rawProperties.source,
    macAddress: rawProperties.macAddress,
    temperatureAlert: rawContent.temperature > 30 ? 'true' : 'false'
  };

  // Generate new content object.
  let newContent = {
    deviceId: 'Intel NUC Gateway',
    messageId: ++global.messageCount,
    temperature: rawContent.temperature
  };

  // Publish hello new message toobroker.
  this.broker.publish(
    {
      properties: newProperties,
      content: new Uint8Array(Buffer.from(JSON.stringify(newContent), 'utf8'))
    }
  );
},
```

### <a name="printer-module"></a>印表機模組
| 輸入                          | 處理器 | 輸出                     | 來源檔案          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| 來自其他模組的任何訊息 | N/A       | 記錄 hello 訊息 tooconsole | `printer.js` |

此模組是簡單、 一目了然，輸出收到 hello 訊息 （屬性、 內容） toohello 終端機視窗。

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a>組態
hello 執行 hello 模組之前的最後一個步驟是 tooconfigure hello Azure IoT 邊緣和 tooestablish hello 模組之間的連線。

首先我們需要 toodeclare 我們`node`載入器 （從不同語言的 Azure IoT 邊緣支援載入器） 無法透過參考其`name`之後 hello 各節中。

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

一旦我們宣告我們載入器，我們也需要 toodeclare 以及我們的模組。 類似 toodeclaring hello 載入器，它們也可以參考由其`name`屬性。 當您宣告的模組，我們需要 toospecify hello 載入器應該使用 （這應該是的 hello 一個我們之前所定義） 和 hello 進入點 （應為我們模組 hello 正規化的類別名稱） 針對每個模組。 hello`simulated_device`模組為 hello Azure IoT 邊緣核心執行階段封裝中包含的原生模組。 包含`args`hello JSON 檔案，即使它是在`null`。

```json
"modules": [
  {
    "name": "simulated_device",
    "loader": {
      "name": "native",
      "entrypoint": {
        "module.path": "simulated_device"
      }
    },
    "args": {
      "macAddress": "01:02:03:03:02:01",
      "messagePeriod": 500
    }
  },
  {
    "name": "converter",
    "loader": {
      "name": "node",
      "entrypoint": {
        "main.path": "modules/converter.js"
      }
    },
    "args": null
  },
  {
    "name": "printer",
    "loader": {
      "name": "node",
      "entrypoint": {
        "main.path": "modules/printer.js"
      }
    },
    "args": null
  }
]
```

結尾 hello hello 組態，我們建立 hello 連線。 每個連線是以 `source` 和 `sink` 表示。 它們應會參照預先定義的模組。 hello 輸出訊息的`source`模組轉送 toohello 輸入`sink`模組。

```json
"links": [
  {
    "source": "simulated_device",
    "sink": "converter"
  },
  {
    "source": "converter",
    "sink": "printer"
  }
]
```

## <a name="running-hello-modules"></a>執行 hello 模組
1. `npm install`
2. `npm start`

如果您想 tooterminate hello 應用程式，請按`<Enter>`索引鍵。

> [!IMPORTANT]
> 建議您不要 toouse Ctrl + C tooterminate hello IoT 邊緣應用程式。 為這種方式可能會導致 hello 程序 tooterminate 異常。
