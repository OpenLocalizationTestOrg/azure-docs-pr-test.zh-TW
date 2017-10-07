---
title: "aaaCreate 第一個 Azure microservices 上的應用程式使用 C# 的 Linux |Microsoft 文件"
description: "使用 C# 建立和部署 Service Fabric 應用程式"
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/21/2017
ms.author: subramar
ms.openlocfilehash: 68d685e130be338ebcdb2f1af24b66d1e14f580a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a>建立第一個 Azure Service Fabric 應用程式
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

Service Fabric 提供了在 Linux 上建置服務的 .NET Core 和 Java SDK。 在本教學課程中，我們看看 toocreate 適用於 Linux 和組建服務，使用 C# (.NET Core) 的應用程式。

## <a name="prerequisites"></a>必要條件
開始之前，請確定您已 [設定 Linux 開發環境](service-fabric-get-started-linux.md)。 如果您使用 Mac OS X，您可以 [使用 Vagrant 在虛擬機器中設定 Linux 一整體環境](service-fabric-get-started-mac.md)。

您也想 tooinstall hello[服務網狀架構 CLI](service-fabric-cli.md)

### <a name="install-and-set-up-hello-generators-for-csharp"></a>安裝和設定 CSharp hello 產生器
Service Fabric 提供的 Scaffolding 工具可協助您從終端機使用 Yeoman 範本產生器建立 Service Fabric CSharp 應用程式。 請遵循下列 tooensure 您尚未使用您的電腦上的 CSharp hello Service Fabric yeoman 範本產生器的 hello 步驟。
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
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-hello-application"></a>建立 hello 應用程式
Service Fabric 應用程式可以包含一或多個服務，每個都有特定角色中傳送嗨應用程式的功能。 hello Service Fabric [Yeoman](http://yeoman.io/) CSharp，您安裝最後一個步驟中，產生器可讓您輕鬆 toocreate 第一個服務和 tooadd 多更新的版本。 讓我們 Yeoman toocreate 應用程式使用單一的服務。

1. 在終端機中，輸入下列命令 toostart 建置 hello scaffolding hello:`yo azuresfcsharp`
2. 為您的應用程式命名。
3. 選擇您的第一個服務的 hello 類型並將它命名。 基於 hello 本教學課程中，我們選擇可靠的動作項目服務。

   ![適用於 C# 的 Service Fabric Yeoman 產生器][sf-yeoman]

> [!NOTE]
> 如需 hello 選項的詳細資訊，請參閱[Service Fabric 程式設計模型概觀](service-fabric-choose-framework.md)。
>
>

## <a name="build-hello-application"></a>建置 hello 應用程式
hello 服務網狀架構 Yeoman 範本包含建置指令碼，您可以使用從終端機 hello toobuild hello 應用程式 （之後瀏覽 toohello 應用程式資料夾）。

  ```sh
 cd myapp
 ./build.sh
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

一旦部署的 hello 應用程式，開啟瀏覽器並瀏覽至[Service Fabric 總管](service-fabric-visualizing-your-cluster.md)在[http://localhost:19080/總管](http://localhost:19080/Explorer)。 然後，展開 hello**應用程式**節點，請注意，現在您的應用程式類型的項目，另一個用於 hello 該類型的第一個執行個體。

## <a name="start-hello-test-client-and-perform-a-failover"></a>啟動 hello 測試用戶端，然後執行容錯移轉
動作項目專案沒有任何屬於自己的項目。 它們需要另一個服務或用戶端 toosend 這些訊息。 hello 動作項目範本包含簡單的測試指令碼，您可以搭配 toointeract hello 動作項目服務。

1. 執行使用 hello 監看式公用程式 toosee hello 輸出 hello 行動服務的 hello 指令碼。

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. 在 Service Fabric 總管 中，找出裝載 hello hello 行動服務的主要複本的節點。 在 hello 以下螢幕擷取畫面，它可以是節點 3。

    ![Service Fabric 總管中尋找 hello 主要複本][sfx-primary]
3. 按一下您在 hello 先前步驟中，找到並選取 hello 節點**停用 （重新啟動）**從 hello 動作 功能表。 這個動作會在您強制容錯移轉 tooa 次要複本執行另一個節點上的本機叢集，重新啟動一個節點。 當您執行此動作，請注意 toohello 輸出 hello 測試用戶端與 hello 計數器繼續 tooincrement 儘管 hello 容錯移轉附註。

## <a name="adding-more-services-tooan-existing-application"></a>新增更多服務 tooan 現有應用程式

tooadd 另一個 tooan 建立服務應用程式已經使用`yo`，執行下列步驟的 hello:
1. 變更 hello 現有應用程式的根目錄 toohello。  例如， `cd ~/YeomanSamples/MyApplication`，如果`MyApplication`是 hello Yeoman 所建立的應用程式。
2. 執行 `yo azuresfcsharp:AddService`

## <a name="migrating-from-projectjson-toocsproj"></a>從 project.json too.csproj 移轉
1. 執行 'dotnet 移轉' 在專案根目錄中，會將移轉所有 hello project.json toocsproj 格式。
2. 更新 hello 專案據以參考專案檔中的 toocsproj 檔案。
3. 更新 hello 中的專案檔案名稱 toocsproj 檔 build.sh。

## <a name="next-steps"></a>後續步驟

* [深入了解 Reliable Actors](service-fabric-reliable-actors-introduction.md)
* [互動使用 hello 服務網狀架構 CLI Service Fabric 叢集](service-fabric-cli.md)
* 了解 [Service Fabric 支援選項](service-fabric-support.md)
* [開始使用 Service Fabric CLI](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
