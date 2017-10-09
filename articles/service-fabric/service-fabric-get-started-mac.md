---
title: "開發環境上與 Azure Service Fabric 的 Mac OS X toowork aaaSet |Microsoft 文件"
description: "安裝 hello 執行階段、 SDK 和工具，並建立本機開發叢集。 完成此安裝之後，您將準備 toobuild Mac OS X 上的應用程式。"
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2017
ms.author: saysa
ms.openlocfilehash: 0b8a6c1fc1871fa76f3e21cefbc7f66f79072797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a>在 Mac OS X 上設定開發環境
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

您可以建立 Service Fabric 應用程式 toorun 上使用 Mac OS X 的 Linux 叢集。本文件涵蓋如何註冊您的 Mac 開發 tooset。

## <a name="prerequisites"></a>必要條件
Service Fabric 不會執行原生 OS X toorun 在本機的 Service Fabric 叢集，我們會提供預先設定的 Ubuntu 虛擬機器使用 Vagrant 和 VirtualBox。 開始之前，您需要：

* [Vagrant (v1.8.4 或更新版本)](http://www.vagrantup.com/downloads.html)
* [VirtualBox](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> 您需要 Vagrant 和 VirtualBox toouse 互相支援版本。 Vagrant 在不支援的 VirtualBox 版本上的行為可能不穩定。
>

## <a name="create-hello-local-vm"></a>建立 hello 本機 VM
toocreate hello 本機 VM 包含 5 個節點 Service Fabric 叢集，請執行下列步驟的 hello:

1. 複製 hello`Vagrantfile`儲存機制

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    此步驟將清單 hello 檔案`Vagrantfile`包含 hello VM 組態以及 hello 位置 hello VM 從內部網路下載。

2. 瀏覽 toohello 的 hello 儲存機制的本機複本

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. （選擇性）修改 hello 預設 VM 設定

    根據預設，hello 本機 VM 設定，如下所示：

   * 配置 3 GB 的記憶體
   * 私用的主機網路設定於 IP 192.168.50.50 啟用 hello Mac 主機中的流量通過

     您可以變更這些設定之一，或在 hello 中加入其他組態 toohello VM `Vagrantfile`。 請參閱 hello [Vagrant 文件](http://www.vagrantup.com/docs)hello 的組態選項的完整清單。
4. 建立 hello VM

    ```bash
    vagrant up
    ```

   此步驟中下載預先設定的 hello VM 映像，它在本機，然後設定本機的 Service Fabric 叢集它的開機。 您應該預期它 tootake 幾分鐘的時間。 如果安裝程式順利完成，您會看到訊息指出該 hello 叢集啟動 hello 輸出中。

    ![在 VM 佈建後啟動的叢集安裝程式][cluster-setup-script]

    >[!TIP]
    > 如果 hello VM 下載花很長的時間，您可以下載它使用 wget 或 curl 或透過瀏覽 toohello 連結所指定瀏覽器**config.vm.box_url** hello 檔案中`Vagrantfile`。 在本機下載之後, 編輯`Vagrantfile`toopoint toohello 本機路徑下載 hello 映像的位置。 範例下載 hello 映像 too/home/users/test/azureservicefabric.tp8.box，然後設定**config.vm.box_url** toothat 路徑。
    >

5. 測試該 hello 叢集是否已正確設定瀏覽 http://192.168.50.50:19080/總管 （假設您保留 hello 預設的私人網路的 IP） 在 tooService Fabric 總管。

    ![Service Fabric 總管檢視從 hello 主機 Mac][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a>在 Mac 上使用 Yeoman 建立應用程式
Service Fabric 提供的 Scaffolding 工具可協助您從終端機使用 Yeoman 範本產生器建立 Service Fabric 應用程式。 請遵循下列 tooensure 您尚未使用您的電腦上的 hello Service Fabric yeoman 範本產生器的 hello 步驟。

1. 您需要 toohave Node.js 及 NPM 安裝在您 mac 上。 如果沒有您可以安裝 Node.js 及 NPM 使用 Homebrew 使用 hello 下列。 toocheck hello 版本的 Node.js 及 NPM 安裝在您的 Mac 上，您可以使用 hello``-v``選項。

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. 在電腦上從 NPM 安裝 [Yeoman](http://yeoman.io/) 範本產生器

  ```bash
  npm install -g yo
  ```
3. 安裝 hello Yeoman 產生器要 toouse，hello 快速入門中的 hello 步驟[文件](service-fabric-get-started-linux.md)。 toocreate 服務網狀架構應用程式使用 Yeoman，步驟 hello-

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. toobuild Mac 上的服務網狀架構 Java 應用程式，您必須為 JDK 1.8 和 Gradle hello 電腦上安裝。


## <a name="install-hello-service-fabric-plugin-for-eclipse-neon"></a>安裝適用於 Eclipse Neon hello Service Fabric 外掛程式

Service Fabric 會提供外掛程式的 hello **IDE Java 的 Eclipse Neon** ，可簡化建立、 建置和部署 Java 服務 hello 程序。 您可以遵循 hello 這個一般中所述的安裝步驟[文件](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon)有關安裝或更新服務網狀架構 Eclipse 外掛程式。

>[!TIP]
> 根據預設我們支援 hello 預設 IP hello 中所述``Vagrantfile``在 hello ``Local.json`` hello 產生應用程式。 如果您進行變更，並部署 Vagrant 與不同的 ip 位址時，請更新中的 hello 對應 IP``Local.json``您應用程式。

## <a name="next-steps"></a>後續步驟
<!-- Links -->
* [使用 Yeoman 在 Linux 上建立和部署第一個 Service Fabric Java 應用程式](service-fabric-create-your-first-linux-application-with-java.md)
* [在 Linux 上使用適用於 Eclipse 的 Service Fabric 外掛程式建立和部署第一個 Service Fabric Java 應用程式](service-fabric-get-started-eclipse.md)
* [在 hello Azure 入口網站中建立 Service Fabric 叢集](service-fabric-cluster-creation-via-portal.md)
* [建立 Service Fabric 叢集使用 hello Azure 資源管理員](service-fabric-cluster-creation-via-arm.md)
* [了解 hello Service Fabric 應用程式模型](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
