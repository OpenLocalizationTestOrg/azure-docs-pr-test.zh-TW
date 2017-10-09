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
# <a name="create-an-azure-iot-edge-module-with-java"></a>使用 Java 建立 Azure IoT Edge 模組

本教學課程示範如何使用 Java 建置 Azure IoT Edge 的模組。

在本教學課程中，我們將逐步引導環境設定以及如何 toowrite [b](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy)資料轉換器模組使用 hello 最新的 Azure IoT 邊緣 Maven 封裝。

## <a name="prerequisites"></a>必要條件

在本節中，您將針對 IoT Edge 模組設定您的環境。 它會套用 tooboth *64 位元 Windows*和*64 位元 Linux (Ubuntu/Debian 8)*作業系統。

hello 下列軟體，則需要：

* [Git 用戶端](https://git-scm.com/downloads)。
* [**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)。
* [Maven](https://maven.apache.org/install.html).

開啟命令列終端機視窗，並複製 hello 下列儲存機制：

1. `git clone https://github.com/Azure-Samples/iot-edge-samples.git`。
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a>整體架構

hello Azure IoT 邊緣平台大量採用 hello[莫 Neumann 架構](https://en.wikipedia.org/wiki/Von_Neumann_architecture)。 這表示該 hello 整個 Azure IoT 邊緣架構是一種系統用來處理輸入和產生輸出。與每個個別的模組也是很小的輸入輸出子系統。 在本教學課程中，我們將介紹下列兩個模組的 hello:

1. 可接收模擬 [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) 訊號，並將它轉換為格式化 [JSON](https://en.wikipedia.org/wiki/JSON) 訊息的模組。
2. 模組可列印收到 hello [JSON](https://en.wikipedia.org/wiki/JSON)訊息。

hello 下列影像顯示 hello 這個專案的一般端對端資料流程：

![三個模組之間的資料流程](media/iot-hub-iot-edge-create-module/dataflow.png "輸入：模擬 BLE 模組；處理器：轉換器模組；輸出：印表機模組")

## <a name="understanding-hello-code"></a>了解 hello 程式碼

### <a name="maven-project-structure"></a>Maven 專案結構

Azure IoT 邊緣封裝會依據 Maven，因為我們需要 toocreate 一般 Maven 專案結構，包含`pom.xml`檔案。

hello POM 繼承自 hello`com.microsoft.azure.gateway.gateway-module-base`封裝，會宣告所有 hello 模組專案包括 hello runtime 二進位檔、 hello 閘道器組態檔路徑和 hello 執行行為所需的相依性。 這可節省我們很多時間，消除 hello 需要 toowrite 而且不斷地重寫好幾百行程式碼。

我們藉由宣告 hello 所需的相依性/外掛程式與 hello hello 下列程式碼片段所示，我們模組所使用的組態檔 toobe hello 名稱需要 tooupdate pom.xml 檔案。

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

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a>Azure IoT Edge 模組的基本認識

您可以將 Azure IoT Edge 模組視為資料處理器，其作業是：接收輸入、加以處理，以及產生輸出。

hello 輸入可能是硬體 （例如動作偵測器） 的資料、 將訊息從其他模組，或任何其他 （例如，計時器會定期產生一個隨機數字）。

hello 輸出類似 toohello 輸入，它可能會觸發硬體 （例如 LED 閃爍不停 hello) 的行為、 訊息 tooother 模組或任何其他 （例如列印 toohello 主控台）。

模組會使用 `com.microsoft.azure.gateway.messaging.Message` 類別彼此通訊。 hello**內容**的`Message`也就是可以代表任何一種您想要的資料的位元組陣列。 **屬性**也會提供在 hello `Message` ，而只是字串的字串對應。 您可以把**屬性**為 hello 標頭的 HTTP 要求或 hello 中繼資料的檔案。

順序 toodevelop java 的 Azure IoT 邊緣模組，您需要新的模組類別繼承自 toocreate`com.microsoft.azure.gateway.core.GatewayModule`實作所需的 hello 抽象方法和`receive()`和`destroy()`。 此時，您也可以選擇 tooimplement hello 選擇性`start()`或`create()`以及方法。 下列程式碼片段的 hello 顯示 tooget 啟動撰寫 Azure IoT 邊緣模組的方式。

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

### <a name="converter-module"></a>轉換器模組

| 輸入                    | 處理器                              | 輸出                 | 來源檔案            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| 溫度資料訊息 | 剖析並建構新的 JSON 訊息 | 建構 JSON 訊息 | `ConverterModule.java` |

此模組是典型的 Azure IoT Edge 模組。 它可接受從其他模組溫度訊息 (硬體模組，或在此情況下我們模擬的 b 模組)。然後再正規化結構化的 tooa JSON 訊息 （包括附加 hello 訊息識別碼，我們是否需要 tootrigger hello 溫度警示，hello 屬性設定等） 中的 hello 溫度訊息。

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

### <a name="printer-module"></a>印表機模組

| 輸入                          | 處理器 | 輸出                     | 來源檔案          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| 來自其他模組的任何訊息 | N/A       | 記錄 hello 訊息 tooconsole | `PrinterModule.java` |

這是簡單的一目了然，模組，它會輸出收到 hello 訊息 toohello 終端機視窗。

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a>Azure IoT Edge 組態

hello 執行 hello 模組之前的最後一個步驟是 tooconfigure hello Azure IoT 邊緣和 tooestablish hello 模組之間的連線。

首先我們需要 toodeclare 我們 Java 載入器 （從不同語言的 Azure IoT 邊緣支援載入器） 無法透過參考其`name`之後 hello 各節中。

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

一旦我們宣告我們載入器，我們也需要 toodeclare 以及我們的模組。 類似 toodeclaring hello 載入器，它們也可以參考由其`name`屬性。 當您宣告的模組，我們需要 toospecify hello 載入器應該使用 （這應該是的 hello 一個我們之前所定義） 和 hello 進入點 （應為我們模組 hello 正規化的類別名稱） 針對每個模組。 hello`simulated_device`模組是原生模組隨附於 hello Azure IoT 邊緣核心執行階段封裝。 您應該永遠包含`args`hello JSON 檔案，即使它是在`null`。

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

結尾 hello hello 組態，我們建立 hello 連線。 每個連線是以 `source` 和 `sink` 表示。 它們應會參照預先定義的模組。 hello 輸出訊息的`source`模組將會轉送 toohello 輸入`sink`模組。

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

## <a name="running-hello-modules"></a>執行 hello 模組

使用`mvn package`toobuild hello 到的所有項目`target/`資料夾。 也建議將 `mvn clean package` 用於全新組建。

使用`mvn exec:exec`toorun hello Azure IoT 邊緣，您應該會看到 hello 溫度資料和所有 hello 屬性會以固定費率列印的 toohello 主控台。

如果您想 tooterminate hello 應用程式，請按`<Enter>`索引鍵。

> [!IMPORTANT]
> 建議您不要 toouse Ctrl + C tooterminate hello IoT 邊緣閘道應用程式。 因為這將造成 hello 程序 tooterminate 異常。

