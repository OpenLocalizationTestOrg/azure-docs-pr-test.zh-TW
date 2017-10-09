---
title: "使用 Java 的 Azure IoT 邊緣模組 aaaCreate |Microsoft 文件"
description: "本教學課程會示範如何 toowrite b 資料轉換器模組使用 hello 最新的 Azure IoT 邊緣 Maven 封裝。"
services: iot-hub
author: junyi
manager: timlt
ms.service: iot-hub
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: junyi
ms.openlocfilehash: abb560933d13d133ae9a1da08b503d5735b230e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-java"></a><span data-ttu-id="a66ce-103">使用 Java 建立 Azure IoT Edge 模組</span><span class="sxs-lookup"><span data-stu-id="a66ce-103">Create an Azure IoT Edge Module with Java</span></span>

<span data-ttu-id="a66ce-104">本教學課程示範如何使用 Java 建置 Azure IoT Edge 的模組。</span><span class="sxs-lookup"><span data-stu-id="a66ce-104">This tutorial showcases how one might build a module for Azure IoT Edge in Java.</span></span>

<span data-ttu-id="a66ce-105">在本教學課程中，我們將逐步引導環境設定以及如何 toowrite [b](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy)資料轉換器模組使用 hello 最新的 Azure IoT 邊緣 Maven 封裝。</span><span class="sxs-lookup"><span data-stu-id="a66ce-105">In this tutorial, we will walk through environment setup and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest Azure IoT Edge Maven packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a66ce-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="a66ce-106">Prerequisites</span></span>

<span data-ttu-id="a66ce-107">在本節中，您將針對 IoT Edge 模組設定您的環境。</span><span class="sxs-lookup"><span data-stu-id="a66ce-107">In this section, you will set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="a66ce-108">它會套用 tooboth *64 位元 Windows*和*64 位元 Linux (Ubuntu/Debian 8)*作業系統。</span><span class="sxs-lookup"><span data-stu-id="a66ce-108">It applies tooboth *64-bit Windows* and *64-bit Linux (Ubuntu/Debian 8)* operating systems.</span></span>

<span data-ttu-id="a66ce-109">hello 下列軟體，則需要：</span><span class="sxs-lookup"><span data-stu-id="a66ce-109">hello following software is required:</span></span>

* <span data-ttu-id="a66ce-110">[Git 用戶端](https://git-scm.com/downloads)。</span><span class="sxs-lookup"><span data-stu-id="a66ce-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="a66ce-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)。</span><span class="sxs-lookup"><span data-stu-id="a66ce-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="a66ce-112">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="a66ce-112">[Maven](https://maven.apache.org/install.html).</span></span>

<span data-ttu-id="a66ce-113">開啟命令列終端機視窗，並複製 hello 下列儲存機制：</span><span class="sxs-lookup"><span data-stu-id="a66ce-113">Open a command-line terminal window and clone hello following repository:</span></span>

1. <span data-ttu-id="a66ce-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`。</span><span class="sxs-lookup"><span data-stu-id="a66ce-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a><span data-ttu-id="a66ce-115">整體架構</span><span class="sxs-lookup"><span data-stu-id="a66ce-115">Overall architecture</span></span>

<span data-ttu-id="a66ce-116">hello Azure IoT 邊緣平台大量採用 hello[莫 Neumann 架構](https://en.wikipedia.org/wiki/Von_Neumann_architecture)。</span><span class="sxs-lookup"><span data-stu-id="a66ce-116">hello Azure IoT Edge platform heavily adopts hello [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="a66ce-117">這表示該 hello 整個 Azure IoT 邊緣架構是一種系統用來處理輸入和產生輸出。與每個個別的模組也是很小的輸入輸出子系統。</span><span class="sxs-lookup"><span data-stu-id="a66ce-117">Which means that hello entire Azure IoT Edge architecture is a system which processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="a66ce-118">在本教學課程中，我們將介紹下列兩個模組的 hello:</span><span class="sxs-lookup"><span data-stu-id="a66ce-118">In this tutorial, we will introduce hello following two modules:</span></span>

1. <span data-ttu-id="a66ce-119">可接收模擬 [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) 訊號，並將它轉換為格式化 [JSON](https://en.wikipedia.org/wiki/JSON) 訊息的模組。</span><span class="sxs-lookup"><span data-stu-id="a66ce-119">A module which receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="a66ce-120">模組可列印收到 hello [JSON](https://en.wikipedia.org/wiki/JSON)訊息。</span><span class="sxs-lookup"><span data-stu-id="a66ce-120">A module which prints hello received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="a66ce-121">hello 下列影像顯示 hello 這個專案的一般端對端資料流程：</span><span class="sxs-lookup"><span data-stu-id="a66ce-121">hello following image displays hello typical end-to-end dataflow for this project:</span></span>

<span data-ttu-id="a66ce-122">![三個模組之間的資料流程](media/iot-hub-iot-edge-create-module/dataflow.png "輸入：模擬 BLE 模組；處理器：轉換器模組；輸出：印表機模組")</span><span class="sxs-lookup"><span data-stu-id="a66ce-122">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="understanding-hello-code"></a><span data-ttu-id="a66ce-123">了解 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="a66ce-123">Understanding hello code</span></span>

### <a name="maven-project-structure"></a><span data-ttu-id="a66ce-124">Maven 專案結構</span><span class="sxs-lookup"><span data-stu-id="a66ce-124">Maven project structure</span></span>

<span data-ttu-id="a66ce-125">Azure IoT 邊緣封裝會依據 Maven，因為我們需要 toocreate 一般 Maven 專案結構，包含`pom.xml`檔案。</span><span class="sxs-lookup"><span data-stu-id="a66ce-125">Since Azure IoT Edge packages are based on Maven, we need toocreate a typical Maven project structure, which contains a `pom.xml` file.</span></span>

<span data-ttu-id="a66ce-126">hello POM 繼承自 hello`com.microsoft.azure.gateway.gateway-module-base`封裝，會宣告所有 hello 模組專案包括 hello runtime 二進位檔、 hello 閘道器組態檔路徑和 hello 執行行為所需的相依性。</span><span class="sxs-lookup"><span data-stu-id="a66ce-126">hello POM inherits from hello `com.microsoft.azure.gateway.gateway-module-base` package, which declares all of hello dependencies needed by a module project which includes hello runtime binaries, hello gateway configuration file path, and hello execution behavior.</span></span> <span data-ttu-id="a66ce-127">這可節省我們很多時間，消除 hello 需要 toowrite 而且不斷地重寫好幾百行程式碼。</span><span class="sxs-lookup"><span data-stu-id="a66ce-127">This saves us lots of time and eliminate hello need toowrite and rewrite hundreds of lines of code over and over again.</span></span>

<span data-ttu-id="a66ce-128">我們藉由宣告 hello 所需的相依性/外掛程式與 hello hello 下列程式碼片段所示，我們模組所使用的組態檔 toobe hello 名稱需要 tooupdate pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="a66ce-128">We need tooupdate the pom.xml file by declaring hello required dependencies/plugins and hello name of hello configuration file toobe used by our module as shown in hello following code snippet.</span></span>

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <!-- Inherit from parent -->
  <parent>
    <groupId>com.microsoft.azure.gateway</groupId>
    <artifactId>gateway-module-base</artifactId>
    <version>1.0.1</version>
  </parent>
  
  <groupId>com.microsoft.azure.gateway</groupId>
  <artifactId>ble-converter</artifactId>
  <version>1.0</version>
  <packaging>jar</packaging>

  <!-- Set hello filename of hello Azure IoT Edge configuration located
       under ./src/main/resources/gateway/ which is used in parent -->
  <properties>
    <gw.config.fileName>gw-config.json</gw.config.fileName>
  </properties>

  <!-- Re-declare dependencies used in parent -->
  <dependencies>
    <dependency>
      <groupId>com.microsoft.azure.gateway</groupId>
      <artifactId>gateway-java-binding</artifactId>
    </dependency>
    <dependency>
      <groupId>${dependency.runtime.group}</groupId>
      <artifactId>${dependency.runtime.name}</artifactId>
    </dependency>
  </dependencies>

  <!-- Re-declare plugins used in parent -->
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-dependency-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-resources-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
      </plugin>
    </plugins>
  </build>
</project>
```

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a><span data-ttu-id="a66ce-129">Azure IoT Edge 模組的基本認識</span><span class="sxs-lookup"><span data-stu-id="a66ce-129">Basic understanding of an Azure IoT Edge module</span></span>

<span data-ttu-id="a66ce-130">您可以將 Azure IoT Edge 模組視為資料處理器，其作業是：接收輸入、加以處理，以及產生輸出。</span><span class="sxs-lookup"><span data-stu-id="a66ce-130">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="a66ce-131">hello 輸入可能是硬體 （例如動作偵測器） 的資料、 將訊息從其他模組，或任何其他 （例如，計時器會定期產生一個隨機數字）。</span><span class="sxs-lookup"><span data-stu-id="a66ce-131">hello input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="a66ce-132">hello 輸出類似 toohello 輸入，它可能會觸發硬體 （例如 LED 閃爍不停 hello) 的行為、 訊息 tooother 模組或任何其他 （例如列印 toohello 主控台）。</span><span class="sxs-lookup"><span data-stu-id="a66ce-132">hello output is similar toohello input, it could trigger hardware behavior (like hello blinking LED), a message tooother modules, or anything else (like printing toohello console).</span></span>

<span data-ttu-id="a66ce-133">模組會使用 `com.microsoft.azure.gateway.messaging.Message` 類別彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="a66ce-133">Modules communicate with each other using `com.microsoft.azure.gateway.messaging.Message` class.</span></span> <span data-ttu-id="a66ce-134">hello**內容**的`Message`也就是可以代表任何一種您想要的資料的位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="a66ce-134">hello **Content** of a `Message` is a byte array which is capable of representing any kind of data you like.</span></span> <span data-ttu-id="a66ce-135">**屬性**也會提供在 hello `Message` ，而只是字串的字串對應。</span><span class="sxs-lookup"><span data-stu-id="a66ce-135">**Properties** are also available in hello `Message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="a66ce-136">您可以把**屬性**為 hello 標頭的 HTTP 要求或 hello 中繼資料的檔案。</span><span class="sxs-lookup"><span data-stu-id="a66ce-136">You may think of **Properties** as hello headers in an HTTP request, or hello metadata of a file.</span></span>

<span data-ttu-id="a66ce-137">順序 toodevelop java 的 Azure IoT 邊緣模組，您需要新的模組類別繼承自 toocreate`com.microsoft.azure.gateway.core.GatewayModule`實作所需的 hello 抽象方法和`receive()`和`destroy()`。</span><span class="sxs-lookup"><span data-stu-id="a66ce-137">In order toodevelop an Azure IoT Edge module in Java, you need toocreate a new module class which inherits from `com.microsoft.azure.gateway.core.GatewayModule` and implement hello required abstract methods `receive()` and `destroy()`.</span></span> <span data-ttu-id="a66ce-138">此時，您也可以選擇 tooimplement hello 選擇性`start()`或`create()`以及方法。</span><span class="sxs-lookup"><span data-stu-id="a66ce-138">At this point, you may also choose tooimplement hello optional `start()` or `create()` methods as well.</span></span> <span data-ttu-id="a66ce-139">下列程式碼片段的 hello 顯示 tooget 啟動撰寫 Azure IoT 邊緣模組的方式。</span><span class="sxs-lookup"><span data-stu-id="a66ce-139">hello following code snippet shows you how tooget started authoring an Azure IoT Edge module.</span></span>

```java
import com.microsoft.azure.gateway.core.Broker;
import com.microsoft.azure.gateway.core.GatewayModule;
import com.microsoft.azure.gateway.messaging.Message;

public class MyEdgeModule extends GatewayModule {
  public MyEdgeModule(long address, Broker broker, String configuration) {
    /* Let hello GatewayModule do hello dirty work of initialization. It's also
       a good time tooparse your own configuration defined in Azure IoT Edge
       configuration file (typically ./src/main/resources/gateway/gw-config.json) */
    super(address, broker, configuration);
  }

  @Override
  public void start() {
    /* Acquire hello resources you need. If you don't
       need any resources, you may omit this method. */
  }

  @Override
  public void destroy() {
    /* It's time toorelease all resources. This method is required. */
  }

  @Override
  public void receive(Message message) {
    /* Logic tooprocess hello input message. This method is required. */
    // ...
    /* Use publish() method toodo hello output. You are
       allowed toopublish your new Message instance. */
    this.publish(message);
  }
}
```

### <a name="converter-module"></a><span data-ttu-id="a66ce-140">轉換器模組</span><span class="sxs-lookup"><span data-stu-id="a66ce-140">Converter module</span></span>

| <span data-ttu-id="a66ce-141">輸入</span><span class="sxs-lookup"><span data-stu-id="a66ce-141">Input</span></span>                    | <span data-ttu-id="a66ce-142">處理器</span><span class="sxs-lookup"><span data-stu-id="a66ce-142">Processor</span></span>                              | <span data-ttu-id="a66ce-143">輸出</span><span class="sxs-lookup"><span data-stu-id="a66ce-143">Output</span></span>                 | <span data-ttu-id="a66ce-144">來源檔案</span><span class="sxs-lookup"><span data-stu-id="a66ce-144">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="a66ce-145">溫度資料訊息</span><span class="sxs-lookup"><span data-stu-id="a66ce-145">Temperature data message</span></span> | <span data-ttu-id="a66ce-146">剖析並建構新的 JSON 訊息</span><span class="sxs-lookup"><span data-stu-id="a66ce-146">Parse and construct a new JSON message</span></span> | <span data-ttu-id="a66ce-147">建構 JSON 訊息</span><span class="sxs-lookup"><span data-stu-id="a66ce-147">Structure JSON message</span></span> | `ConverterModule.java` |

<span data-ttu-id="a66ce-148">此模組是典型的 Azure IoT Edge 模組。</span><span class="sxs-lookup"><span data-stu-id="a66ce-148">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="a66ce-149">它可接受從其他模組溫度訊息 (硬體模組，或在此情況下我們模擬的 b 模組)。然後再正規化結構化的 tooa JSON 訊息 （包括附加 hello 訊息識別碼，我們是否需要 tootrigger hello 溫度警示，hello 屬性設定等） 中的 hello 溫度訊息。</span><span class="sxs-lookup"><span data-stu-id="a66ce-149">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes hello temperature message in tooa structured JSON message (including appending hello message ID, setting hello property of whether we need tootrigger hello temperature alert, and so on).</span></span>

```java
@Override
public void receive(Message message) {
  try {
    JSONObject messageFromBle = new JSONObject(new String(message.getContent()));
    double temperature = messageFromBle.getDouble("temperature");
    Map<String, String> inputProperties = message.getProperties();

    HashMap<String, String> properties = new HashMap<>();
    properties.put("source", inputProperties.get("source"));
    properties.put("macAddress", inputProperties.get("macAddress"));
    properties.put("temperatureAlert", temperature > 30 ? "true" : "false");

    String content = String.format(
        "{ \"deviceId\": \"Intel NUC Gateway\", \"messageId\": %d, \"temperature\": %f }",
        ++this.messageCount, temperature);

    this.publish(new Message(content.getBytes(), properties));
  } catch (Exception ex) {
    ex.printStackTrace();
  }
}
```

### <a name="printer-module"></a><span data-ttu-id="a66ce-150">印表機模組</span><span class="sxs-lookup"><span data-stu-id="a66ce-150">Printer module</span></span>

| <span data-ttu-id="a66ce-151">輸入</span><span class="sxs-lookup"><span data-stu-id="a66ce-151">Input</span></span>                          | <span data-ttu-id="a66ce-152">處理器</span><span class="sxs-lookup"><span data-stu-id="a66ce-152">Processor</span></span> | <span data-ttu-id="a66ce-153">輸出</span><span class="sxs-lookup"><span data-stu-id="a66ce-153">Output</span></span>                     | <span data-ttu-id="a66ce-154">來源檔案</span><span class="sxs-lookup"><span data-stu-id="a66ce-154">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="a66ce-155">來自其他模組的任何訊息</span><span class="sxs-lookup"><span data-stu-id="a66ce-155">Any message from other modules</span></span> | <span data-ttu-id="a66ce-156">N/A</span><span class="sxs-lookup"><span data-stu-id="a66ce-156">N/A</span></span>       | <span data-ttu-id="a66ce-157">記錄 hello 訊息 tooconsole</span><span class="sxs-lookup"><span data-stu-id="a66ce-157">Log hello message tooconsole</span></span> | `PrinterModule.java` |

<span data-ttu-id="a66ce-158">這是簡單的一目了然，模組，它會輸出收到 hello 訊息 toohello 終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="a66ce-158">This is a simple, self-explanatory, module which outputs hello received messages toohello terminal window.</span></span>

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a><span data-ttu-id="a66ce-159">Azure IoT Edge 組態</span><span class="sxs-lookup"><span data-stu-id="a66ce-159">Azure IoT Edge configuration</span></span>

<span data-ttu-id="a66ce-160">hello 執行 hello 模組之前的最後一個步驟是 tooconfigure hello Azure IoT 邊緣和 tooestablish hello 模組之間的連線。</span><span class="sxs-lookup"><span data-stu-id="a66ce-160">hello final step before running hello modules is tooconfigure hello Azure IoT Edge and tooestablish hello connections between modules.</span></span>

<span data-ttu-id="a66ce-161">首先我們需要 toodeclare 我們 Java 載入器 （從不同語言的 Azure IoT 邊緣支援載入器） 無法透過參考其`name`之後 hello 各節中。</span><span class="sxs-lookup"><span data-stu-id="a66ce-161">First we need toodeclare our Java loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in hello sections afterward.</span></span>

```json
"loaders": [{
  "type": "java",
  "name": "java",
  "configuration": {
    "jvm.options": {
      "library.path": "./"
    }
  }
}]
```

<span data-ttu-id="a66ce-162">一旦我們宣告我們載入器，我們也需要 toodeclare 以及我們的模組。</span><span class="sxs-lookup"><span data-stu-id="a66ce-162">Once we have declared our loaders, we will also need toodeclare our modules as well.</span></span> <span data-ttu-id="a66ce-163">類似 toodeclaring hello 載入器，它們也可以參考由其`name`屬性。</span><span class="sxs-lookup"><span data-stu-id="a66ce-163">Similar toodeclaring hello loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="a66ce-164">當您宣告的模組，我們需要 toospecify hello 載入器應該使用 （這應該是的 hello 一個我們之前所定義） 和 hello 進入點 （應為我們模組 hello 正規化的類別名稱） 針對每個模組。</span><span class="sxs-lookup"><span data-stu-id="a66ce-164">When declaring a module, we need toospecify hello loader it should use (which should be hello one we defined before) and hello entry-point (should be hello normalized class name of our module) for each module.</span></span> <span data-ttu-id="a66ce-165">hello`simulated_device`模組是原生模組隨附於 hello Azure IoT 邊緣核心執行階段封裝。</span><span class="sxs-lookup"><span data-stu-id="a66ce-165">hello `simulated_device` module is a native module which is included in hello Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="a66ce-166">您應該永遠包含`args`hello JSON 檔案，即使它是在`null`。</span><span class="sxs-lookup"><span data-stu-id="a66ce-166">You should always include `args` in hello JSON file even if it is `null`.</span></span>

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
      "name": "java",
      "entrypoint": {
        "class.name": "com/microsoft/azure/gateway/ConverterModule",
        "class.path": "./ble-converter-1.0-with-deps.jar"
      }
    },
    "args": null
  },
  {
    "name": "print",
    "loader": {
      "name": "java",
      "entrypoint": {
        "class.name": "com/microsoft/azure/gateway/PrinterModule",
        "class.path": "./ble-converter-1.0-with-deps.jar"
      }
    },
    "args": null
  }
]
```

<span data-ttu-id="a66ce-167">結尾 hello hello 組態，我們建立 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="a66ce-167">At hello end of hello configuration, we establish hello connections.</span></span> <span data-ttu-id="a66ce-168">每個連線是以 `source` 和 `sink` 表示。</span><span class="sxs-lookup"><span data-stu-id="a66ce-168">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="a66ce-169">它們應會參照預先定義的模組。</span><span class="sxs-lookup"><span data-stu-id="a66ce-169">They should both reference a pre-defined module.</span></span> <span data-ttu-id="a66ce-170">hello 輸出訊息的`source`模組將會轉送 toohello 輸入`sink`模組。</span><span class="sxs-lookup"><span data-stu-id="a66ce-170">hello output message of `source` module will be forwarded toohello input of `sink` module.</span></span>

```json
"links": [
  {
    "source": "simulated_device",
    "sink": "converter"
  },
  {
    "source": "converter",
    "sink": "print"
  }
]
```

## <a name="running-hello-modules"></a><span data-ttu-id="a66ce-171">執行 hello 模組</span><span class="sxs-lookup"><span data-stu-id="a66ce-171">Running hello modules</span></span>

<span data-ttu-id="a66ce-172">使用`mvn package`toobuild hello 到的所有項目`target/`資料夾。</span><span class="sxs-lookup"><span data-stu-id="a66ce-172">Use `mvn package` toobuild everything into hello `target/` folder.</span></span> <span data-ttu-id="a66ce-173">也建議將 `mvn clean package` 用於全新組建。</span><span class="sxs-lookup"><span data-stu-id="a66ce-173">`mvn clean package` is also recommended for a clean build.</span></span>

<span data-ttu-id="a66ce-174">使用`mvn exec:exec`toorun hello Azure IoT 邊緣，您應該會看到 hello 溫度資料和所有 hello 屬性會以固定費率列印的 toohello 主控台。</span><span class="sxs-lookup"><span data-stu-id="a66ce-174">Use `mvn exec:exec` toorun hello Azure IoT Edge and you should observe that hello temperature data and all hello properties are printed toohello console at a fixed rate.</span></span>

<span data-ttu-id="a66ce-175">如果您想 tooterminate hello 應用程式，請按`<Enter>`索引鍵。</span><span class="sxs-lookup"><span data-stu-id="a66ce-175">If you want tooterminate hello application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a66ce-176">建議您不要 toouse Ctrl + C tooterminate hello IoT 邊緣閘道應用程式。</span><span class="sxs-lookup"><span data-stu-id="a66ce-176">It is not recommended toouse Ctrl + C tooterminate hello IoT Edge gateway application.</span></span> <span data-ttu-id="a66ce-177">因為這將造成 hello 程序 tooterminate 異常。</span><span class="sxs-lookup"><span data-stu-id="a66ce-177">As this may cause hello process tooterminate abnormally.</span></span>

