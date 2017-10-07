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
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a><span data-ttu-id="28f63-103">使用 Node.js 建立 Azure IoT Edge 模組</span><span class="sxs-lookup"><span data-stu-id="28f63-103">Create an Azure IoT Edge Module with Node.js</span></span>

<span data-ttu-id="28f63-104">本教學課程示範如何 toocreate JS 中的 Azure IoT 邊緣的模組。</span><span class="sxs-lookup"><span data-stu-id="28f63-104">This tutorial showcases how toocreate a module for Azure IoT Edge in JS.</span></span>

<span data-ttu-id="28f63-105">在本教學課程中，我們將逐步檢視環境設定以及如何 toowrite [b](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy)資料轉換器模組使用 hello 最新的 Azure IoT 邊緣 NPM 封裝。</span><span class="sxs-lookup"><span data-stu-id="28f63-105">In this tutorial, we walk through environment setup and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest Azure IoT Edge NPM packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28f63-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="28f63-106">Prerequisites</span></span>

<span data-ttu-id="28f63-107">在本節中，您會針對 IoT Edge 模組設定您的環境。</span><span class="sxs-lookup"><span data-stu-id="28f63-107">In this section, you set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="28f63-108">它會套用 tooboth *64 位元 Windows*和*64 位元 Linux (Ubuntu 14 +)*作業系統。</span><span class="sxs-lookup"><span data-stu-id="28f63-108">It applies tooboth *64-bit Windows* and *64-bit Linux (Ubuntu 14+)* operating systems.</span></span>

<span data-ttu-id="28f63-109">hello 下列軟體，則需要：</span><span class="sxs-lookup"><span data-stu-id="28f63-109">hello following software is required:</span></span>
* <span data-ttu-id="28f63-110">[Git 用戶端](https://git-scm.com/downloads)。</span><span class="sxs-lookup"><span data-stu-id="28f63-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="28f63-111">[Node LTS](https://nodejs.org)。</span><span class="sxs-lookup"><span data-stu-id="28f63-111">[Node LTS](https://nodejs.org).</span></span>
* <span data-ttu-id="28f63-112">`npm install -g yo`。</span><span class="sxs-lookup"><span data-stu-id="28f63-112">`npm install -g yo`.</span></span>
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a><span data-ttu-id="28f63-113">架構</span><span class="sxs-lookup"><span data-stu-id="28f63-113">Architecture</span></span>

<span data-ttu-id="28f63-114">hello Azure IoT 邊緣平台大量採用 hello[莫 Neumann 架構](https://en.wikipedia.org/wiki/Von_Neumann_architecture)。</span><span class="sxs-lookup"><span data-stu-id="28f63-114">hello Azure IoT Edge platform heavily adopts hello [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="28f63-115">這表示該 hello 整個 Azure IoT 邊緣架構是系統處理輸入和產生輸出。與每個個別的模組也是很小的輸入輸出子系統。</span><span class="sxs-lookup"><span data-stu-id="28f63-115">Which means that hello entire Azure IoT Edge architecture is a system that processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="28f63-116">在本教學課程中，我們引進下列兩個模組的 hello:</span><span class="sxs-lookup"><span data-stu-id="28f63-116">In this tutorial, we introduce hello following two modules:</span></span>

1. <span data-ttu-id="28f63-117">可接收模擬 [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) 訊號，並將它轉換為格式化 [JSON](https://en.wikipedia.org/wiki/JSON) 訊息的模組。</span><span class="sxs-lookup"><span data-stu-id="28f63-117">A module that receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="28f63-118">模組會列印收到 hello [JSON](https://en.wikipedia.org/wiki/JSON)訊息。</span><span class="sxs-lookup"><span data-stu-id="28f63-118">A module that prints hello received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="28f63-119">hello 下列影像顯示 hello 一般 tooend dataflow 結束這個專案：</span><span class="sxs-lookup"><span data-stu-id="28f63-119">hello following image displays hello typical end tooend dataflow for this project:</span></span>

<span data-ttu-id="28f63-120">![三個模組之間的資料流程](media/iot-hub-iot-edge-create-module/dataflow.png "輸入：模擬 BLE 模組；處理器：轉換器模組；輸出：印表機模組")</span><span class="sxs-lookup"><span data-stu-id="28f63-120">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="set-up-hello-environment"></a><span data-ttu-id="28f63-121">設定 hello 環境</span><span class="sxs-lookup"><span data-stu-id="28f63-121">Set up hello environment</span></span>
<span data-ttu-id="28f63-122">以下我們會示範如何 tooquickly 設定環境 toostart toowrite JS 您第一次 b 轉換器模組。</span><span class="sxs-lookup"><span data-stu-id="28f63-122">Below we show you how tooquickly set up environment toostart toowrite your first BLE converter module with JS.</span></span>

### <a name="create-module-project"></a><span data-ttu-id="28f63-123">建立模組專案</span><span class="sxs-lookup"><span data-stu-id="28f63-123">Create module project</span></span>
1. <span data-ttu-id="28f63-124">開啟命令列視窗，執行 `yo az-iot-gw-module`。</span><span class="sxs-lookup"><span data-stu-id="28f63-124">Open a command-line window, run `yo az-iot-gw-module`.</span></span>
2. <span data-ttu-id="28f63-125">步驟 hello hello 螢幕 toofinish hello 初始化模組專案。</span><span class="sxs-lookup"><span data-stu-id="28f63-125">Follow hello steps on hello screen toofinish hello initialization of your module project.</span></span>

### <a name="project-structure"></a><span data-ttu-id="28f63-126">專案結構</span><span class="sxs-lookup"><span data-stu-id="28f63-126">Project structure</span></span>
<span data-ttu-id="28f63-127">JS 模組專案包含下列元件的 hello:</span><span class="sxs-lookup"><span data-stu-id="28f63-127">A JS module project consists of hello following components:</span></span>

<span data-ttu-id="28f63-128">`modules`-hello 自訂 JS 模組來源檔案。</span><span class="sxs-lookup"><span data-stu-id="28f63-128">`modules` - hello customized JS module source files.</span></span> <span data-ttu-id="28f63-129">取代 hello 預設`sensor.js`和`printer.js`與模組檔案。</span><span class="sxs-lookup"><span data-stu-id="28f63-129">Replace hello default `sensor.js` and `printer.js` with your own module files.</span></span>

<span data-ttu-id="28f63-130">`app.js`-hello 項目檔案 toostart hello 邊緣執行個體。</span><span class="sxs-lookup"><span data-stu-id="28f63-130">`app.js` - hello entry file toostart hello Edge instance.</span></span>

<span data-ttu-id="28f63-131">`gw.config.json`-hello 設定檔 toocustomize hello 模組 toobe 載入的邊緣。</span><span class="sxs-lookup"><span data-stu-id="28f63-131">`gw.config.json` - hello configuration file toocustomize hello modules toobe loaded by Edge.</span></span>

<span data-ttu-id="28f63-132">`package.json`-hello 模組專案的中繼資料資訊。</span><span class="sxs-lookup"><span data-stu-id="28f63-132">`package.json` - hello metadata information for module project.</span></span>

<span data-ttu-id="28f63-133">`README.md`-hello 模組專案的基本文件。</span><span class="sxs-lookup"><span data-stu-id="28f63-133">`README.md` - hello basic documentation for module project.</span></span>


### <a name="package-file"></a><span data-ttu-id="28f63-134">套件檔案</span><span class="sxs-lookup"><span data-stu-id="28f63-134">Package file</span></span>

<span data-ttu-id="28f63-135">這`package.json`宣告包含 hello 名稱、 版本、 項目、 指令碼中，執行階段，以及開發相依性的模組專案所需的所有 hello 中繼資料資訊。</span><span class="sxs-lookup"><span data-stu-id="28f63-135">This `package.json` declares all hello metadata information needed by a module project that includes hello name, version, entry, scripts, runtime, and development dependencies.</span></span>

<span data-ttu-id="28f63-136">下列程式碼片段會示範如何 tooconfigure b 轉換器的範例專案。</span><span class="sxs-lookup"><span data-stu-id="28f63-136">Following code snippet shows how tooconfigure for BLE converter sample project.</span></span>
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


### <a name="entry-file"></a><span data-ttu-id="28f63-137">輸入檔案</span><span class="sxs-lookup"><span data-stu-id="28f63-137">Entry file</span></span>
<span data-ttu-id="28f63-138">hello`app.js`定義 hello 方式 tooinitialize hello 邊緣執行個體。</span><span class="sxs-lookup"><span data-stu-id="28f63-138">hello `app.js` defines hello way tooinitialize hello edge instance.</span></span> <span data-ttu-id="28f63-139">我們不需要在這裡 toomake 任何變更。</span><span class="sxs-lookup"><span data-stu-id="28f63-139">Here we don't need toomake any change.</span></span>

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

### <a name="interface-of-module"></a><span data-ttu-id="28f63-140">模組的介面</span><span class="sxs-lookup"><span data-stu-id="28f63-140">Interface of module</span></span>
<span data-ttu-id="28f63-141">您可以將 Azure IoT Edge 模組視為資料處理器，其作業是：接收輸入、加以處理，以及產生輸出。</span><span class="sxs-lookup"><span data-stu-id="28f63-141">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="28f63-142">hello 輸入可能是硬體 （例如動作偵測器） 的資料、 將訊息從其他模組，或任何其他 （例如，計時器會定期產生一個隨機數字）。</span><span class="sxs-lookup"><span data-stu-id="28f63-142">hello input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="28f63-143">hello 輸出類似 toohello 輸入，它可能會觸發硬體 （例如 LED 閃爍不停 hello) 的行為、 訊息 tooother 模組或任何其他 （例如列印 toohello 主控台）。</span><span class="sxs-lookup"><span data-stu-id="28f63-143">hello output is similar toohello input, it could trigger hardware behavior (like hello blinking LED), a message tooother modules, or anything else (like printing toohello console).</span></span>

<span data-ttu-id="28f63-144">模組會使用 `message` 物件彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="28f63-144">Modules communicate with each other using `message` object.</span></span> <span data-ttu-id="28f63-145">hello**內容**的`message`是可以代表任何一種您想要的資料的位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="28f63-145">hello **content** of a `message` is a byte array that is capable of representing any kind of data you like.</span></span> <span data-ttu-id="28f63-146">**屬性**也會提供在 hello `message` ，而只是字串的字串對應。</span><span class="sxs-lookup"><span data-stu-id="28f63-146">**Properties** are also available in hello `message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="28f63-147">您可以把**屬性**為 hello 標頭的 HTTP 要求或 hello 中繼資料的檔案。</span><span class="sxs-lookup"><span data-stu-id="28f63-147">You may think of **properties** as hello headers in an HTTP request, or hello metadata of a file.</span></span>

<span data-ttu-id="28f63-148">在順序 toodevelop JS 中的 Azure IoT 邊緣模組，您需要 toocreate 實作所需的 hello 方法的新模組物件`receive()`。</span><span class="sxs-lookup"><span data-stu-id="28f63-148">In order toodevelop an Azure IoT Edge module in JS, you need toocreate a new module object that implements hello required methods `receive()`.</span></span> <span data-ttu-id="28f63-149">此時，您也可以選擇 tooimplement hello 選擇性`create()`或`start()`，或`destroy()`以及方法。</span><span class="sxs-lookup"><span data-stu-id="28f63-149">At this point, you may also choose tooimplement hello optional `create()` or `start()`, or `destroy()` methods as well.</span></span> <span data-ttu-id="28f63-150">下列程式碼片段的 hello 顯示 hello JS 模組物件的 scaffolding。</span><span class="sxs-lookup"><span data-stu-id="28f63-150">hello following code snippet shows you hello scaffolding of JS module object.</span></span>

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

### <a name="converter-module"></a><span data-ttu-id="28f63-151">轉換器模組</span><span class="sxs-lookup"><span data-stu-id="28f63-151">Converter module</span></span>
| <span data-ttu-id="28f63-152">輸入</span><span class="sxs-lookup"><span data-stu-id="28f63-152">Input</span></span>                    | <span data-ttu-id="28f63-153">處理器</span><span class="sxs-lookup"><span data-stu-id="28f63-153">Processor</span></span>                              | <span data-ttu-id="28f63-154">輸出</span><span class="sxs-lookup"><span data-stu-id="28f63-154">Output</span></span>                 | <span data-ttu-id="28f63-155">來源檔案</span><span class="sxs-lookup"><span data-stu-id="28f63-155">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="28f63-156">溫度資料訊息</span><span class="sxs-lookup"><span data-stu-id="28f63-156">Temperature data message</span></span> | <span data-ttu-id="28f63-157">剖析並建構新的 JSON 訊息</span><span class="sxs-lookup"><span data-stu-id="28f63-157">Parse and construct a new JSON message</span></span> | <span data-ttu-id="28f63-158">建構 JSON 訊息</span><span class="sxs-lookup"><span data-stu-id="28f63-158">Structure JSON message</span></span> | `converter.js` |

<span data-ttu-id="28f63-159">此模組是典型的 Azure IoT Edge 模組。</span><span class="sxs-lookup"><span data-stu-id="28f63-159">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="28f63-160">它可接受從其他模組溫度訊息 (硬體模組，或在此情況下我們模擬的 b 模組)。然後再正規化結構化的 tooa JSON 訊息 （包括附加 hello 訊息識別碼，我們是否需要 tootrigger hello 溫度警示，hello 屬性設定等） 中的 hello 溫度訊息。</span><span class="sxs-lookup"><span data-stu-id="28f63-160">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes hello temperature message in tooa structured JSON message (including appending hello message ID, setting hello property of whether we need tootrigger hello temperature alert, and so on).</span></span>

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

### <a name="printer-module"></a><span data-ttu-id="28f63-161">印表機模組</span><span class="sxs-lookup"><span data-stu-id="28f63-161">Printer module</span></span>
| <span data-ttu-id="28f63-162">輸入</span><span class="sxs-lookup"><span data-stu-id="28f63-162">Input</span></span>                          | <span data-ttu-id="28f63-163">處理器</span><span class="sxs-lookup"><span data-stu-id="28f63-163">Processor</span></span> | <span data-ttu-id="28f63-164">輸出</span><span class="sxs-lookup"><span data-stu-id="28f63-164">Output</span></span>                     | <span data-ttu-id="28f63-165">來源檔案</span><span class="sxs-lookup"><span data-stu-id="28f63-165">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="28f63-166">來自其他模組的任何訊息</span><span class="sxs-lookup"><span data-stu-id="28f63-166">Any message from other modules</span></span> | <span data-ttu-id="28f63-167">N/A</span><span class="sxs-lookup"><span data-stu-id="28f63-167">N/A</span></span>       | <span data-ttu-id="28f63-168">記錄 hello 訊息 tooconsole</span><span class="sxs-lookup"><span data-stu-id="28f63-168">Log hello message tooconsole</span></span> | `printer.js` |

<span data-ttu-id="28f63-169">此模組是簡單、 一目了然，輸出收到 hello 訊息 （屬性、 內容） toohello 終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="28f63-169">This module is simple, self-explanatory, which outputs hello received messages(property, content) toohello terminal window.</span></span>

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a><span data-ttu-id="28f63-170">組態</span><span class="sxs-lookup"><span data-stu-id="28f63-170">Configuration</span></span>
<span data-ttu-id="28f63-171">hello 執行 hello 模組之前的最後一個步驟是 tooconfigure hello Azure IoT 邊緣和 tooestablish hello 模組之間的連線。</span><span class="sxs-lookup"><span data-stu-id="28f63-171">hello final step before running hello modules is tooconfigure hello Azure IoT Edge and tooestablish hello connections between modules.</span></span>

<span data-ttu-id="28f63-172">首先我們需要 toodeclare 我們`node`載入器 （從不同語言的 Azure IoT 邊緣支援載入器） 無法透過參考其`name`之後 hello 各節中。</span><span class="sxs-lookup"><span data-stu-id="28f63-172">First we need toodeclare our `node` loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in hello sections afterward.</span></span>

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

<span data-ttu-id="28f63-173">一旦我們宣告我們載入器，我們也需要 toodeclare 以及我們的模組。</span><span class="sxs-lookup"><span data-stu-id="28f63-173">Once we have declared our loaders, we also need toodeclare our modules as well.</span></span> <span data-ttu-id="28f63-174">類似 toodeclaring hello 載入器，它們也可以參考由其`name`屬性。</span><span class="sxs-lookup"><span data-stu-id="28f63-174">Similar toodeclaring hello loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="28f63-175">當您宣告的模組，我們需要 toospecify hello 載入器應該使用 （這應該是的 hello 一個我們之前所定義） 和 hello 進入點 （應為我們模組 hello 正規化的類別名稱） 針對每個模組。</span><span class="sxs-lookup"><span data-stu-id="28f63-175">When declaring a module, we need toospecify hello loader it should use (which should be hello one we defined before) and hello entry-point (should be hello normalized class name of our module) for each module.</span></span> <span data-ttu-id="28f63-176">hello`simulated_device`模組為 hello Azure IoT 邊緣核心執行階段封裝中包含的原生模組。</span><span class="sxs-lookup"><span data-stu-id="28f63-176">hello `simulated_device` module is a native module that is included in hello Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="28f63-177">包含`args`hello JSON 檔案，即使它是在`null`。</span><span class="sxs-lookup"><span data-stu-id="28f63-177">Include `args` in hello JSON file even if it is `null`.</span></span>

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

<span data-ttu-id="28f63-178">結尾 hello hello 組態，我們建立 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="28f63-178">At hello end of hello configuration, we establish hello connections.</span></span> <span data-ttu-id="28f63-179">每個連線是以 `source` 和 `sink` 表示。</span><span class="sxs-lookup"><span data-stu-id="28f63-179">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="28f63-180">它們應會參照預先定義的模組。</span><span class="sxs-lookup"><span data-stu-id="28f63-180">They should both reference a pre-defined module.</span></span> <span data-ttu-id="28f63-181">hello 輸出訊息的`source`模組轉送 toohello 輸入`sink`模組。</span><span class="sxs-lookup"><span data-stu-id="28f63-181">hello output message of `source` module is forwarded toohello input of `sink` module.</span></span>

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

## <a name="running-hello-modules"></a><span data-ttu-id="28f63-182">執行 hello 模組</span><span class="sxs-lookup"><span data-stu-id="28f63-182">Running hello modules</span></span>
1. `npm install`
2. `npm start`

<span data-ttu-id="28f63-183">如果您想 tooterminate hello 應用程式，請按`<Enter>`索引鍵。</span><span class="sxs-lookup"><span data-stu-id="28f63-183">If you want tooterminate hello application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="28f63-184">建議您不要 toouse Ctrl + C tooterminate hello IoT 邊緣應用程式。</span><span class="sxs-lookup"><span data-stu-id="28f63-184">It is not recommended toouse Ctrl + C tooterminate hello IoT Edge application.</span></span> <span data-ttu-id="28f63-185">為這種方式可能會導致 hello 程序 tooterminate 異常。</span><span class="sxs-lookup"><span data-stu-id="28f63-185">As this way may cause hello process tooterminate abnormally.</span></span>
