---
title: "aaaCreate Linux 上的 Azure Service Fabric 可靠執行者 Java 應用程式 |Microsoft 文件"
description: "深入了解如何 toocreate 和部署 Java Service Fabric 可靠執行者應用程式在五分鐘。"
services: service-fabric
documentationcenter: java
author: rwike77
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: ryanwi
ms.openlocfilehash: 11496b767811c89969c65d1682d843448eb6a922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a>在 Linux 上建立第一個 Java Service Fabric Reliable Actors 應用程式
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

本快速入門可協助您在短短幾分鐘內在 Linux 開發環境中建立第一個 Azure Service Fabric Java 應用程式。  當您完成時，您必須在 hello 本機開發叢集上執行簡單 Java 單一服務應用程式。  

## <a name="prerequisites"></a>必要條件
開始之前，安裝 hello Service Fabric SDK、 hello 服務網狀架構 CLI，並設定開發叢集，在您[Linux 開發環境](service-fabric-get-started-linux.md)。 如果您使用 Mac OS X，您可以[使用 Vagrant 在虛擬機器中設定 Linux 開發環境](service-fabric-get-started-mac.md)。

您也想 tooinstall hello[服務網狀架構 CLI](service-fabric-cli.md)。

### <a name="install-and-set-up-hello-generators-for-java"></a>安裝及設定 java hello 產生器
Service Fabric 提供的 Scaffolding 工具可協助您從終端機使用 Yeoman 範本產生器建立 Service Fabric Java 應用程式。 請遵循下列 tooensure 您尚未在電腦上使用 for Java 的 hello Service Fabric yeoman 範本產生器的 hello 步驟。
1. 在電腦上安裝 nodejs 和 NPM

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. 在電腦上從 NPM 安裝 [Yeoman](http://yeoman.io/) 範本產生器

  ```bash
  sudo npm install -g yo
  ```
3. 從 NPM 安裝 hello 服務網狀架構 Yeo Java 應用程式產生器

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-hello-application"></a>建立 hello 應用程式
Service Fabric 應用程式包含一個或多個服務，每個都有特定角色中傳送嗨應用程式的功能。 hello 產生器安裝在 hello 最後一個區段中，可讓您輕鬆 toocreate 第一個服務和 tooadd 多更新的版本。  您也可以使用適用於 Eclipse 的外掛程式，建立、建置及部署 Service Fabric Java 應用程式。 請參閱[使用 Eclipse 建立和部署第一個 Java 應用程式](service-fabric-get-started-eclipse.md)。 這個快速入門中，使用 Yeoman toocreate 應用程式的單一服務，用來儲存和取得計數器值。

1. 在終端機中，輸入 ``yo azuresfjava``。
2. 為您的應用程式命名。
3. 選擇您的第一個服務的 hello 類型並將它命名。 在本教學課程中，選擇 Reliable Actor 服務。 如需有關 hello 其他類型的服務，請參閱[Service Fabric 程式設計模型概觀](service-fabric-choose-framework.md)。
   ![適用於 Java 的 Service Fabric Yeoman 產生器][sf-yeoman]

## <a name="build-hello-application"></a>建置 hello 應用程式
hello 服務網狀架構 Yeoman 範本包括的組建指令碼[Gradle](https://gradle.org/)，而您可以使用從終端機 hello toobuild hello 應用程式。
從 Maven 擷取的 Service Fabric Java 相依性。 toobuild 及 hello 服務網狀架構 Java 應用程式上的工作，您必須確認您有 JDK 且 Gradle 安裝 tooensure。 如果尚未安裝，您可以執行 hello 下列 tooinstall JDK(openjdk-8-jdk) 和 Gradle-

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

toobuild 和套件 hello 應用程式，執行下列 hello:

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-hello-application"></a>部署 hello 應用程式
建置 hello 應用程式之後，您可以將它部署 toohello 本機叢集。

1. Toohello 本機 Service Fabric 叢集連線。

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. 提供在 hello 範本 toocopy hello 應用程式封裝 toohello 叢集映像存放區、 註冊 hello 應用程式類型，以及建立 hello 應用程式的執行個體，請執行 hello 安裝指令碼。

    ```bash
    ./install.sh
    ```

部署的 hello 建置應用程式是相同 hello 做為任何其他的 Service Fabric 應用程式。 請參閱 hello 說明文件[管理 Service Fabric 應用程式以 hello 服務網狀架構 CLI](service-fabric-application-lifecycle-sfctl.md)如需詳細指示。

參數 toothese 命令可以在 hello 應用程式封裝內的 hello 產生資訊清單中找到。

一旦部署的 hello 應用程式，開啟瀏覽器並瀏覽至[Service Fabric 總管](service-fabric-visualizing-your-cluster.md)在[http://localhost:19080/總管](http://localhost:19080/Explorer)。
然後，展開 hello**應用程式**節點，請注意，現在您的應用程式類型的項目，另一個用於 hello 該類型的第一個執行個體。

## <a name="start-hello-test-client-and-perform-a-failover"></a>啟動 hello 測試用戶端，然後執行容錯移轉
動作項目不會進行任何各自獨立的但需要其他服務或用戶端 toosend 這些訊息。 hello 動作項目範本包含簡單的測試指令碼，您可以搭配 toointeract hello 動作項目服務。

1. 執行使用 hello 監看式公用程式 toosee hello 輸出 hello 行動服務的 hello 指令碼。  hello 測試指令碼會呼叫 hello `setCountAsync()` hello 執行者 tooincrement 計數器，方法會呼叫 hello `getCountAsync()` hello 執行者 tooget hello 新計數器的值，並顯示該值 toohello 主控台上的方法。

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. 在 Service Fabric 總管中，找出 hello 節點裝載 hello 主要複本 hello 動作項目服務。 在 hello 以下螢幕擷取畫面，它可以是節點 3。 hello 主要服務複本控點會讀取和寫入作業。  Toohello 次要複本，0 和 1 hello 下列螢幕擷取畫面中的節點上執行時，會再複寫服務狀態的變更。

    ![Service Fabric 總管中尋找 hello 主要複本][sfx-primary]

3. 在**節點**，按一下您在 hello 先前步驟中，找到並選取 hello 節點**停用 （重新啟動）**從 hello 動作 功能表。 這個動作會重新啟動執行 hello 主要服務複本的 hello 節點，並強制 hello 另一個節點上執行的次要複本的容錯移轉 tooone。  該次要複本會提升的 tooprimary、 另一個次要複本上建立另一個節點，而 hello 主要複本就會開始 tootake 讀取/寫入作業。 Hello 節點重新啟動時，觀賞 hello 輸出 hello 測試用戶端與 hello 計數器繼續 tooincrement 儘管 hello 容錯移轉附註。

## <a name="remove-hello-application"></a>移除 hello 應用程式
使用提供 hello 範本 toodelete hello 應用程式執行個體中的 hello 解除安裝指令碼、 取消登錄 hello 應用程式封裝，並移除 hello 應用程式套件 hello 叢集映像存放區。

```bash
./uninstall.sh
```

Service Fabric 總管 中看到的 hello 應用程式和應用程式類型不會再出現在 hello**應用程式**節點。

## <a name="service-fabric-java-libraries-on-maven"></a>Maven 上的 Service Fabric Java 程式庫
Service Fabric Java 程式庫已裝載於 Maven 中。 您可以在 hello 新增 hello 相依性``pom.xml``或``build.gradle``從您專案 toouse 服務網狀架構 Java 程式庫**mavenCentral**。

### <a name="actors"></a>動作項目

您應用程式的 Service Fabric Reliable Actor 支援。

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a>服務

您應用程式的 Service Fabric 無狀態服務支援。

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a>其他
#### <a name="transport"></a>傳輸

Service Fabric Java 應用程式的傳輸層支援。 您不需要 tooexplicitly 將此相依性 tooyour Reliable Actor 或服務應用程式，除非您在 hello 傳輸層級進行程式設計。

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a>網狀架構支援

系統層級支援適用於 Service Fabric，交談 toonative Service Fabric 執行階段。 您不需要 tooexplicitly 加入此相依性 tooyour Reliable Actor 或服務應用程式。 從 Maven 自動擷取這取得，當您包含 hello 上述其他相依性。

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a>移轉舊服務網狀架構 Java 應用程式 toobe 搭配 Maven 使用
我們最近已從 Service Fabric Java SDK tooMaven 儲存機制移服務網狀架構 Java 文件庫。 雖然 hello 新應用程式，您可以產生使用 Yeoman 或 Eclipse 中，將會產生 （這會是可以與 Maven toowork） 最新版本更新的專案，您可以更新您現有的 Service Fabric 無狀態或執行者 Java 應用程式，而且已使用 hello 服務網狀架構 Java SDK 更早版本，從 Maven toouse hello 服務網狀架構 Java 相依性。 請遵循所述的 hello 步驟[這裡](service-fabric-migrate-old-javaapp-to-use-maven.md)tooensure Maven 適用於較舊的應用程式。

## <a name="next-steps"></a>後續步驟

* [使用 Eclipse 在 Linux 上建立第一個 Service Fabric Java 應用程式](service-fabric-get-started-eclipse.md)
* [深入了解 Reliable Actors](service-fabric-reliable-actors-introduction.md)
* [互動使用 hello 服務網狀架構 CLI Service Fabric 叢集](service-fabric-cli.md)
* 了解 [Service Fabric 支援選項](service-fabric-support.md)
* [開始使用 Service Fabric CLI](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
