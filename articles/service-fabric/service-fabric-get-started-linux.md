---
title: "您在 Linux 上的開發環境 aaaSet |Microsoft 文件"
description: "安裝 hello 執行階段和 SDK，並在 Linux 上建立本機開發叢集。 完成此安裝之後，您將準備 toobuild 應用程式。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/23/2017
ms.author: subramar
ms.openlocfilehash: 9d82c2015f9e2c6fb55f2052c7cdb1e906c5deeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment-on-linux"></a>在 Linux 上準備您的開發環境
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

toodeploy 並執行[Azure Service Fabric 應用程式](service-fabric-application-model.md)Linux 開發電腦上安裝 hello 執行階段和通用的 SDK。 您也可以安裝 Java 和 .NET Core 的選擇性 SDK。

## <a name="prerequisites"></a>必要條件

開發可支援下列作業系統版本的 hello:

* Ubuntu 16.04 (`Xenial Xerus`)

## <a name="update-your-apt-sources"></a>更新 APT 來源
tooinstall hello SDK 和 hello 相關聯的執行階段封裝透過 hello apt get 命令列工具，您必須先更新進階封裝工具 (APT) 來源。

1. 開啟終端機。
2. 加入 hello Service Fabric 儲存機制 tooyour 來源清單。

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. 新增 hello`dotnet`儲存機制 tooyour 來源清單。

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. 新增 hello 新 Gnu 隱私防護 （GnuPG 或 GPG） 索引鍵 tooyour APT keyring。

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. 新增 hello 官方 Docker GPG 金鑰 tooyour APT keyring。

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. 設定 hello Docker 儲存機制。

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. 重新整理您的封裝列出 hello 新加入的儲存機制。

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-hello-sdk-for-local-cluster-setup"></a>安裝並設定好 hello SDK 本機叢集安裝程式

您已更新您的來源之後，您可以安裝 hello SDK。 安裝 hello Service Fabric SDK 封裝並確認 hello 安裝同意 toohello 授權合約。

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   hello 下列命令自動接受 hello 授權 Service Fabric 封裝：
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a>設定本機叢集
  如果 hello 安裝成功，您應該能夠 toostart 本機叢集。

  1. 執行 hello 叢集安裝指令碼。

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. 開啟網頁瀏覽器並移過[Service Fabric 總管](http://localhost:19080/Explorer)。 如果啟動 hello 叢集後，您應該會看到 hello Service Fabric 總管儀表板。

      ![Linux 上的 Service Fabric Explorer][sfx-linux]

  此時，您可以根據客體容器或來賓可執行檔，部署預先建置的 Service Fabric 應用程式套件或新的套件。 toobuild 新服務使用 hello Java 或.NET Core Sdk，請遵循 hello 後續各節提供的選用設定步驟。


  > [!NOTE]
  > Linux 不支援獨立叢集。 hello 預覽支援只有一個方塊，而且 Azure Linux 多電腦叢集。
  >

## <a name="set-up-hello-service-fabric-cli"></a>設定服務網狀架構 CLI hello

hello[服務網狀架構 CLI](service-fabric-cli.md)有 Service Fabric 實體，包括叢集和應用程式與互動的命令。 它根據 python，因此請務必確定 toohave python 和 pip 安裝才能繼續進行 hello 下列命令：

```bash
pip install sfctl
```

## <a name="install-and-set-up-hello-generators-for-containers-and-guest-executables"></a>安裝並設定好 hello 容器和客體可執行檔的產生器
Service Fabric 提供的 Scaffolding 工具可協助您從終端機使用 Yeoman 範本產生器建立 Service Fabric 應用程式。 請遵循下列 tooensure 您擁有 hello Service Fabric yeoman 範本產生器，用於您的電腦上的 hello 步驟。

1. 在電腦上安裝 nodejs 和 NPM

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. 在電腦上從 NPM 安裝 [Yeoman](http://yeoman.io/) 範本產生器

  ```bash
  sudo npm install -g yo
  ```
3. 從 NPM 安裝 hello 服務網狀架構 Yeo 容器產生器和來賓 execuatble 產生器

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

產生器上方 hello 安裝之後，您應該能夠 toocreate 客體可執行檔或容器服務的應用程式執行`yo azuresfguest`或`yo azuresfcontainer`分別。

## <a name="install-hello-necessary-java-artifacts-optional-if-you-want-toouse-hello-java-programming-models"></a>安裝 hello 必要 Java 成品 （選擇性，如果您想 toouse hello Java 程式設計模型）

toobuild Service Fabric 服務使用 Java，請確定您有隨用來執行建置工作的 Gradle 一起安裝的 JDK 1.8。 下列程式碼片段的 hello 安裝以及 Gradle 的 Open JDK 1.8。 hello 服務網狀架構 Java 文件庫會從 Maven 提取。

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-hello-eclipse-neon-plug-in-optional"></a>安裝 hello Eclipse Neon 外掛程式 （選擇性）

您可以在 hello 適用於從 Service Fabric 安裝 hello Eclipse 外掛程式**Eclipse IDE for Java 開發人員**。 您可以使用 Eclipse toocreate Service Fabric 客體可執行應用程式和容器應用程式中加入 tooService 網狀架構 Java 應用程式。

1. 在 Eclipse 中，確定您有最新的 Eclipse Neon hello Buildship 新版 (1.0.17 或更新版本) 安裝。 您可以選取來查看 hello 版本已安裝的元件**協助** > **安裝詳細資料**。 您可以使用 hello 指示來更新 Buildship [Eclipse Buildship: Eclipse 外掛程式 Gradle][buildship-update]。

2. tooinstall hello Service Fabric 外掛程式，請選取**協助** > **安裝新軟體**。

3. 在 hello**搭配**方塊中，輸入**http://dl.microsoft.com/eclipse**。

4. 按一下 [新增] 。

    ![hello 可用的軟體 頁面][sf-eclipse-plugin]

5. 選取 hello **ServiceFabric**外掛程式，然後按一下**下一步**。

6. 完成 hello 安裝步驟，並接受 hello 使用者授權合約。

如果您已經有 hello 服務網狀架構 Eclipse 外掛程式安裝，請確定您已擁有 hello 最新版本。 您可以選取查看**協助** > **安裝詳細資料**和 hello 清單中搜尋適用於 Service Fabric 安裝外掛程式。如果有可用的較新版本，請選取 [更新]。

如需詳細資訊，請參閱[適用於 Eclipse Java 應用程式開發的 Service Fabric 外掛程式](service-fabric-get-started-eclipse.md)。


## <a name="install-hello-net-core-sdk-optional-if-you-want-toouse-hello-net-core-programming-models"></a>安裝 hello.NET Core SDK （選擇性，如果您想 toouse hello.NET Core 的程式設計模型）
hello.NET Core SDK 提供 hello 程式庫和.NET core 必要的 toobuild Service Fabric 服務的範本。 安裝執行 hello 以下 hello.NET Core SDK 封裝

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-hello-sdk-and-runtime"></a>更新 hello SDK 和執行階段

tooupdate toohello 最新版本的 hello SDK 和執行階段中，執行下列命令的 hello （取消選取您不想 hello Sdk）：

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
tooupdate 從 Maven 的 hello Java SDK 二進位檔，您需要 tooupdate hello 版本的詳細資訊的 hello 中的 hello 對應二進位檔``build.gradle``檔案 toopoint toohello 最新版本。 tooknow 確實需要 tooupdate hello 版本，您可以使用參照 tooany ``build.gradle`` Service Fabric 快速入門範例中的檔案[這裡](https://github.com/Azure-Samples/service-fabric-java-getting-started)。

> [!NOTE]
> 更新 hello 封裝可能會導致您執行的本機開發叢集 toostop。 下列 hello 指示此頁面上升級後重新啟動本機叢集。

## <a name="next-steps"></a>後續步驟

* [使用 Yeoman 在 Linux 上建立和部署第一個 Service Fabric Java 應用程式](service-fabric-create-your-first-linux-application-with-java.md)
* [在 Linux 上使用適用於 Eclipse 的 Service Fabric 外掛程式建立和部署第一個 Service Fabric Java 應用程式](service-fabric-get-started-eclipse.md)
* [在 Linux 上建立第一個 CSharp 應用程式](service-fabric-create-your-first-linux-application-with-csharp.md)
* [在 OSX 上準備您的開發環境](service-fabric-get-started-mac.md)
* [使用 hello 服務網狀架構 CLI toomanage 您應用程式](service-fabric-application-lifecycle-sfctl.md)
* [Service Fabric Windows/Linux 的差異](service-fabric-linux-windows-differences.md)
* [開始使用 Service Fabric CLI](service-fabric-cli.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
