---
title: "使用 Node.js 建立 Azure IoT Edge 模組 | Microsoft 文件"
description: "本教學課程示範如何使用最新的 Azure IoT Edge NPM 套件和 Yeoman 產生器撰寫 BLE 資料轉換器模組。"
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
ms.openlocfilehash: ba466f47e157d805600c41fa3d84ed5a0363969c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a><span data-ttu-id="3eb0e-103">使用 Node.js 建立 Azure IoT Edge 模組</span><span class="sxs-lookup"><span data-stu-id="3eb0e-103">Create an Azure IoT Edge Module with Node.js</span></span>

<span data-ttu-id="3eb0e-104">本教學課程示範如何使用 JS 建立 Azure IoT Edge 的模組。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-104">This tutorial showcases how to create a module for Azure IoT Edge in JS.</span></span>

<span data-ttu-id="3eb0e-105">在本教學課程中，我們會逐步說明環境設定，以及如何使用最新的 Azure IoT Edge NPM 套件撰寫 [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) 資料轉換器模組。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-105">In this tutorial, we walk through environment setup and how to write a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using the latest Azure IoT Edge NPM packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3eb0e-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="3eb0e-106">Prerequisites</span></span>

<span data-ttu-id="3eb0e-107">在本節中，您會針對 IoT Edge 模組設定您的環境。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-107">In this section, you set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="3eb0e-108">它同時適用於「64 位元 Windows」和「64 位元 Linux (Ubuntu 14+)」作業系統。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-108">It applies to both *64-bit Windows* and *64-bit Linux (Ubuntu 14+)* operating systems.</span></span>

<span data-ttu-id="3eb0e-109">需要下列軟體：</span><span class="sxs-lookup"><span data-stu-id="3eb0e-109">The following software is required:</span></span>
* <span data-ttu-id="3eb0e-110">[Git 用戶端](https://git-scm.com/downloads)。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="3eb0e-111">[Node LTS](https://nodejs.org)。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-111">[Node LTS](https://nodejs.org).</span></span>
* <span data-ttu-id="3eb0e-112">`npm install -g yo`。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-112">`npm install -g yo`.</span></span>
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a><span data-ttu-id="3eb0e-113">架構</span><span class="sxs-lookup"><span data-stu-id="3eb0e-113">Architecture</span></span>

<span data-ttu-id="3eb0e-114">Azure IoT Edge 平台大量採用 [Von Neumann 架構](https://en.wikipedia.org/wiki/Von_Neumann_architecture)。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-114">The Azure IoT Edge platform heavily adopts the [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="3eb0e-115">這表示整個 Azure IoT Edge 架構是用來處理輸入及產生輸出的系統，而每個個別模組也是小型輸入-輸出子系統。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-115">Which means that the entire Azure IoT Edge architecture is a system that processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="3eb0e-116">在本教學課程中，我們會介紹下列兩個模組︰</span><span class="sxs-lookup"><span data-stu-id="3eb0e-116">In this tutorial, we introduce the following two modules:</span></span>

1. <span data-ttu-id="3eb0e-117">可接收模擬 [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) 訊號，並將它轉換為格式化 [JSON](https://en.wikipedia.org/wiki/JSON) 訊息的模組。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-117">A module that receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="3eb0e-118">可列印已接收 [JSON](https://en.wikipedia.org/wiki/JSON) 訊息的模組。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-118">A module that prints the received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="3eb0e-119">下圖顯示這個專案的典型端對端資料流程：</span><span class="sxs-lookup"><span data-stu-id="3eb0e-119">The following image displays the typical end to end dataflow for this project:</span></span>

<span data-ttu-id="3eb0e-120">![三個模組之間的資料流程](media/iot-hub-iot-edge-create-module/dataflow.png "輸入：模擬 BLE 模組；處理器：轉換器模組；輸出：印表機模組")</span><span class="sxs-lookup"><span data-stu-id="3eb0e-120">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="set-up-the-environment"></a><span data-ttu-id="3eb0e-121">設定 Azure 環境</span><span class="sxs-lookup"><span data-stu-id="3eb0e-121">Set up the environment</span></span>
<span data-ttu-id="3eb0e-122">我們在下面示範如何快速設定環境，以便開始使用 JS 撰寫第一個 BLE 轉換器模組。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-122">Below we show you how to quickly set up environment to start to write your first BLE converter module with JS.</span></span>

### <a name="create-module-project"></a><span data-ttu-id="3eb0e-123">建立模組專案</span><span class="sxs-lookup"><span data-stu-id="3eb0e-123">Create module project</span></span>
1. <span data-ttu-id="3eb0e-124">開啟命令列視窗，執行 `yo az-iot-gw-module`。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-124">Open a command-line window, run `yo az-iot-gw-module`.</span></span>
2. <span data-ttu-id="3eb0e-125">遵循畫面上的步驟，完成模組專案的初始化。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-125">Follow the steps on the screen to finish the initialization of your module project.</span></span>

### <a name="project-structure"></a><span data-ttu-id="3eb0e-126">專案結構</span><span class="sxs-lookup"><span data-stu-id="3eb0e-126">Project structure</span></span>
<span data-ttu-id="3eb0e-127">JS 模組專案由下列元件組成：</span><span class="sxs-lookup"><span data-stu-id="3eb0e-127">A JS module project consists of the following components:</span></span>

<span data-ttu-id="3eb0e-128">`modules` - 自訂的 JS 模組原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-128">`modules` - The customized JS module source files.</span></span> <span data-ttu-id="3eb0e-129">以您自己的模組檔案取代預設 `sensor.js` 和 `printer.js`。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-129">Replace the default `sensor.js` and `printer.js` with your own module files.</span></span>

<span data-ttu-id="3eb0e-130">`app.js` - 用來啟動 Edge 執行個體的輸入檔案。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-130">`app.js` - The entry file to start the Edge instance.</span></span>

<span data-ttu-id="3eb0e-131">`gw.config.json` - 自訂由 Edge 所要載入之模組的組態檔。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-131">`gw.config.json` - The configuration file to customize the modules to be loaded by Edge.</span></span>

<span data-ttu-id="3eb0e-132">`package.json` - 模組專案的中繼資料資訊。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-132">`package.json` - The metadata information for module project.</span></span>

<span data-ttu-id="3eb0e-133">`README.md` - 模組專案的基本文件。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-133">`README.md` - The basic documentation for module project.</span></span>


### <a name="package-file"></a><span data-ttu-id="3eb0e-134">套件檔案</span><span class="sxs-lookup"><span data-stu-id="3eb0e-134">Package file</span></span>

<span data-ttu-id="3eb0e-135">此 `package.json` 會宣告模組專案需要的所有中繼資料資訊，包括名稱、版本、項目、指令碼、執行階段及開發相依性。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-135">This `package.json` declares all the metadata information needed by a module project that includes the name, version, entry, scripts, runtime, and development dependencies.</span></span>

<span data-ttu-id="3eb0e-136">下列程式碼片段示範如何設定 BLE 轉換器範例專案。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-136">Following code snippet shows how to configure for BLE converter sample project.</span></span>
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


### <a name="entry-file"></a><span data-ttu-id="3eb0e-137">輸入檔案</span><span class="sxs-lookup"><span data-stu-id="3eb0e-137">Entry file</span></span>
<span data-ttu-id="3eb0e-138">`app.js` 定義初始化邊緣執行個體的方式。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-138">The `app.js` defines the way to initialize the edge instance.</span></span> <span data-ttu-id="3eb0e-139">我們在此不需要進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-139">Here we don't need to make any change.</span></span>

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

### <a name="interface-of-module"></a><span data-ttu-id="3eb0e-140">模組的介面</span><span class="sxs-lookup"><span data-stu-id="3eb0e-140">Interface of module</span></span>
<span data-ttu-id="3eb0e-141">您可以將 Azure IoT Edge 模組視為資料處理器，其作業是：接收輸入、加以處理，以及產生輸出。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-141">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="3eb0e-142">輸入可能是來自硬體 (例如動作偵測器) 的資料、來自其他模組的訊息，或任何其他資料 (例如計時器定期產生的隨機數字)。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-142">The input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="3eb0e-143">輸出類似於輸入，它可能會觸發硬體行為 (例如閃爍的 LED)、給其他模組的訊息，或任何其他作業 (例如列印至主控台)。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-143">The output is similar to the input, it could trigger hardware behavior (like the blinking LED), a message to other modules, or anything else (like printing to the console).</span></span>

<span data-ttu-id="3eb0e-144">模組會使用 `message` 物件彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-144">Modules communicate with each other using `message` object.</span></span> <span data-ttu-id="3eb0e-145">`message` 的 [內容] 是一個位元組陣列，其可代表任一種您想要的資料。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-145">The **content** of a `message` is a byte array that is capable of representing any kind of data you like.</span></span> <span data-ttu-id="3eb0e-146">[屬性] 也適用於 `message`，且只是字串與字串的對應。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-146">**Properties** are also available in the `message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="3eb0e-147">您可以將 [屬性] 視為 HTTP 要求中的標頭或檔案的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-147">You may think of **properties** as the headers in an HTTP request, or the metadata of a file.</span></span>

<span data-ttu-id="3eb0e-148">若要使用 JS 開發 Azure IoT Edge 模組，您必須建立新的模組物件，以實作必要的方法 `receive()`。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-148">In order to develop an Azure IoT Edge module in JS, you need to create a new module object that implements the required methods `receive()`.</span></span> <span data-ttu-id="3eb0e-149">此時，您也可以選擇實作選擇性 `create()``start()` 或 `destroy()` 方法。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-149">At this point, you may also choose to implement the optional `create()` or `start()`, or `destroy()` methods as well.</span></span> <span data-ttu-id="3eb0e-150">下列程式碼片段顯示 JS 模組物件的 Scaffolding。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-150">The following code snippet shows you the scaffolding of JS module object.</span></span>

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

### <a name="converter-module"></a><span data-ttu-id="3eb0e-151">轉換器模組</span><span class="sxs-lookup"><span data-stu-id="3eb0e-151">Converter module</span></span>
| <span data-ttu-id="3eb0e-152">輸入</span><span class="sxs-lookup"><span data-stu-id="3eb0e-152">Input</span></span>                    | <span data-ttu-id="3eb0e-153">處理器</span><span class="sxs-lookup"><span data-stu-id="3eb0e-153">Processor</span></span>                              | <span data-ttu-id="3eb0e-154">輸出</span><span class="sxs-lookup"><span data-stu-id="3eb0e-154">Output</span></span>                 | <span data-ttu-id="3eb0e-155">來源檔案</span><span class="sxs-lookup"><span data-stu-id="3eb0e-155">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="3eb0e-156">溫度資料訊息</span><span class="sxs-lookup"><span data-stu-id="3eb0e-156">Temperature data message</span></span> | <span data-ttu-id="3eb0e-157">剖析並建構新的 JSON 訊息</span><span class="sxs-lookup"><span data-stu-id="3eb0e-157">Parse and construct a new JSON message</span></span> | <span data-ttu-id="3eb0e-158">建構 JSON 訊息</span><span class="sxs-lookup"><span data-stu-id="3eb0e-158">Structure JSON message</span></span> | `converter.js` |

<span data-ttu-id="3eb0e-159">此模組是典型的 Azure IoT Edge 模組。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-159">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="3eb0e-160">它可接受來自其他模組 (硬體模組，或此情況下我們的模擬 BLE 模組) 的溫度訊息，然後將溫度訊息正常化成為結構化 JSON 訊息 (包括附加訊息識別碼、設定我們是否需要觸發溫度警示的屬性等等)。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-160">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes the temperature message in to a structured JSON message (including appending the message ID, setting the property of whether we need to trigger the temperature alert, and so on).</span></span>

```javascript
receive: function (message) {
  // Initialize the messageCount in global object at first time.
  if (!global.messageCount) {
    global.messageCount = 0;
  }

  // Read the content and properties objects from message.
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

  // Publish the new message to broker.
  this.broker.publish(
    {
      properties: newProperties,
      content: new Uint8Array(Buffer.from(JSON.stringify(newContent), 'utf8'))
    }
  );
},
```

### <a name="printer-module"></a><span data-ttu-id="3eb0e-161">印表機模組</span><span class="sxs-lookup"><span data-stu-id="3eb0e-161">Printer module</span></span>
| <span data-ttu-id="3eb0e-162">輸入</span><span class="sxs-lookup"><span data-stu-id="3eb0e-162">Input</span></span>                          | <span data-ttu-id="3eb0e-163">處理器</span><span class="sxs-lookup"><span data-stu-id="3eb0e-163">Processor</span></span> | <span data-ttu-id="3eb0e-164">輸出</span><span class="sxs-lookup"><span data-stu-id="3eb0e-164">Output</span></span>                     | <span data-ttu-id="3eb0e-165">來源檔案</span><span class="sxs-lookup"><span data-stu-id="3eb0e-165">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="3eb0e-166">來自其他模組的任何訊息</span><span class="sxs-lookup"><span data-stu-id="3eb0e-166">Any message from other modules</span></span> | <span data-ttu-id="3eb0e-167">N/A</span><span class="sxs-lookup"><span data-stu-id="3eb0e-167">N/A</span></span>       | <span data-ttu-id="3eb0e-168">將訊息記錄至主控台</span><span class="sxs-lookup"><span data-stu-id="3eb0e-168">Log the message to console</span></span> | `printer.js` |

<span data-ttu-id="3eb0e-169">這是簡單、不言而喻的模組，它會將收到的訊息 (屬性、內容) 輸出至終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-169">This module is simple, self-explanatory, which outputs the received messages(property, content) to the terminal window.</span></span>

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a><span data-ttu-id="3eb0e-170">組態</span><span class="sxs-lookup"><span data-stu-id="3eb0e-170">Configuration</span></span>
<span data-ttu-id="3eb0e-171">執行模組之前的最後一個步驟是設定 Azure IoT Edge 並建立模組之間的連線。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-171">The final step before running the modules is to configure the Azure IoT Edge and to establish the connections between modules.</span></span>

<span data-ttu-id="3eb0e-172">我們必須先宣告 `node` 載入器 (因為 Azure IoT Edge 支援不同語言的載入器)，以在後續各節中依照其 `name` 予以參照。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-172">First we need to declare our `node` loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in the sections afterward.</span></span>

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

<span data-ttu-id="3eb0e-173">宣告載入器後，我們也必須宣告我們的模組。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-173">Once we have declared our loaders, we also need to declare our modules as well.</span></span> <span data-ttu-id="3eb0e-174">類似於宣告載入器，也可以依照其 `name` 屬性予以參照。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-174">Similar to declaring the loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="3eb0e-175">宣告模組時，我們需要指定它應使用的載入器 (這應該是我們先前定義的載入器) 和每個模組的進入點 (應該是我們模組的正常化類別名稱)。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-175">When declaring a module, we need to specify the loader it should use (which should be the one we defined before) and the entry-point (should be the normalized class name of our module) for each module.</span></span> <span data-ttu-id="3eb0e-176">`simulated_device` 模組是 Azure IoT Edge 核心執行階段套件內含的原生模組。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-176">The `simulated_device` module is a native module that is included in the Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="3eb0e-177">將 `args` 包含在 JSON 檔案中 (即使它是 `null`)。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-177">Include `args` in the JSON file even if it is `null`.</span></span>

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

<span data-ttu-id="3eb0e-178">在設定結束時，我們會建立連線。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-178">At the end of the configuration, we establish the connections.</span></span> <span data-ttu-id="3eb0e-179">每個連線是以 `source` 和 `sink` 表示。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-179">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="3eb0e-180">它們應會參照預先定義的模組。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-180">They should both reference a pre-defined module.</span></span> <span data-ttu-id="3eb0e-181">`source` 模組的輸出訊息會轉送至 `sink` 模組的輸入。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-181">The output message of `source` module is forwarded to the input of `sink` module.</span></span>

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

## <a name="running-the-modules"></a><span data-ttu-id="3eb0e-182">執行模組</span><span class="sxs-lookup"><span data-stu-id="3eb0e-182">Running the modules</span></span>
1. `npm install`
2. `npm start`

<span data-ttu-id="3eb0e-183">如果您想要終止應用程式，請按 `<Enter>` 鍵。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-183">If you want to terminate the application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3eb0e-184">不建議使用 Ctrl + C 來終止 IoT Edge 應用程式，</span><span class="sxs-lookup"><span data-stu-id="3eb0e-184">It is not recommended to use Ctrl + C to terminate the IoT Edge application.</span></span> <span data-ttu-id="3eb0e-185">因為這可能會造成程序異常終止。</span><span class="sxs-lookup"><span data-stu-id="3eb0e-185">As this way may cause the process to terminate abnormally.</span></span>
