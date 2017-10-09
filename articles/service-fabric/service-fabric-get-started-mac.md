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
# <a name="set-up-your-development-environment-on-mac-os-x"></a><span data-ttu-id="ac3c6-104">在 Mac OS X 上設定開發環境</span><span class="sxs-lookup"><span data-stu-id="ac3c6-104">Set up your development environment on Mac OS X</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ac3c6-105">Windows</span><span class="sxs-lookup"><span data-stu-id="ac3c6-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="ac3c6-106">Linux</span><span class="sxs-lookup"><span data-stu-id="ac3c6-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="ac3c6-107">OSX</span><span class="sxs-lookup"><span data-stu-id="ac3c6-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="ac3c6-108">您可以建立 Service Fabric 應用程式 toorun 上使用 Mac OS X 的 Linux 叢集。本文件涵蓋如何註冊您的 Mac 開發 tooset。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-108">You can build Service Fabric applications toorun on Linux clusters using Mac OS X. This article covers how tooset up your Mac for development.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac3c6-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="ac3c6-109">Prerequisites</span></span>
<span data-ttu-id="ac3c6-110">Service Fabric 不會執行原生 OS X toorun 在本機的 Service Fabric 叢集，我們會提供預先設定的 Ubuntu 虛擬機器使用 Vagrant 和 VirtualBox。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-110">Service Fabric does not run natively on OS X. toorun a local Service Fabric cluster, we provide a pre-configured Ubuntu virtual machine using Vagrant and VirtualBox.</span></span> <span data-ttu-id="ac3c6-111">開始之前，您需要：</span><span class="sxs-lookup"><span data-stu-id="ac3c6-111">Before you get started, you need:</span></span>

* [<span data-ttu-id="ac3c6-112">Vagrant (v1.8.4 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="ac3c6-112">Vagrant (v1.8.4 or later)</span></span>](http://www.vagrantup.com/downloads.html)
* [<span data-ttu-id="ac3c6-113">VirtualBox</span><span class="sxs-lookup"><span data-stu-id="ac3c6-113">VirtualBox</span></span>](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> <span data-ttu-id="ac3c6-114">您需要 Vagrant 和 VirtualBox toouse 互相支援版本。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-114">You need toouse mutually supported versions of Vagrant and VirtualBox.</span></span> <span data-ttu-id="ac3c6-115">Vagrant 在不支援的 VirtualBox 版本上的行為可能不穩定。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-115">Vagrant might behave erratically on an unsupported VirtualBox version.</span></span>
>

## <a name="create-hello-local-vm"></a><span data-ttu-id="ac3c6-116">建立 hello 本機 VM</span><span class="sxs-lookup"><span data-stu-id="ac3c6-116">Create hello local VM</span></span>
<span data-ttu-id="ac3c6-117">toocreate hello 本機 VM 包含 5 個節點 Service Fabric 叢集，請執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ac3c6-117">toocreate hello local VM containing a 5-node Service Fabric cluster, perform hello following steps:</span></span>

1. <span data-ttu-id="ac3c6-118">複製 hello`Vagrantfile`儲存機制</span><span class="sxs-lookup"><span data-stu-id="ac3c6-118">Clone hello `Vagrantfile` repo</span></span>

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    <span data-ttu-id="ac3c6-119">此步驟將清單 hello 檔案`Vagrantfile`包含 hello VM 組態以及 hello 位置 hello VM 從內部網路下載。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-119">This steps bring downs hello file `Vagrantfile` containing hello VM configuration along with hello location hello VM is downloaded from.</span></span>

2. <span data-ttu-id="ac3c6-120">瀏覽 toohello 的 hello 儲存機制的本機複本</span><span class="sxs-lookup"><span data-stu-id="ac3c6-120">Navigate toohello local clone of hello repo</span></span>

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. <span data-ttu-id="ac3c6-121">（選擇性）修改 hello 預設 VM 設定</span><span class="sxs-lookup"><span data-stu-id="ac3c6-121">(Optional) Modify hello default VM settings</span></span>

    <span data-ttu-id="ac3c6-122">根據預設，hello 本機 VM 設定，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ac3c6-122">By default, hello local VM is configured as follows:</span></span>

   * <span data-ttu-id="ac3c6-123">配置 3 GB 的記憶體</span><span class="sxs-lookup"><span data-stu-id="ac3c6-123">3 GB of memory allocated</span></span>
   * <span data-ttu-id="ac3c6-124">私用的主機網路設定於 IP 192.168.50.50 啟用 hello Mac 主機中的流量通過</span><span class="sxs-lookup"><span data-stu-id="ac3c6-124">Private host network configured at IP 192.168.50.50 enabling passthrough of traffic from hello Mac host</span></span>

     <span data-ttu-id="ac3c6-125">您可以變更這些設定之一，或在 hello 中加入其他組態 toohello VM `Vagrantfile`。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-125">You can change either of these settings or add other configuration toohello VM in hello `Vagrantfile`.</span></span> <span data-ttu-id="ac3c6-126">請參閱 hello [Vagrant 文件](http://www.vagrantup.com/docs)hello 的組態選項的完整清單。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-126">See hello [Vagrant documentation](http://www.vagrantup.com/docs) for hello full list of configuration options.</span></span>
4. <span data-ttu-id="ac3c6-127">建立 hello VM</span><span class="sxs-lookup"><span data-stu-id="ac3c6-127">Create hello VM</span></span>

    ```bash
    vagrant up
    ```

   <span data-ttu-id="ac3c6-128">此步驟中下載預先設定的 hello VM 映像，它在本機，然後設定本機的 Service Fabric 叢集它的開機。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-128">This step downloads hello preconfigured VM image, boot it locally, and then set up a local Service Fabric cluster in it.</span></span> <span data-ttu-id="ac3c6-129">您應該預期它 tootake 幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-129">You should expect it tootake a few minutes.</span></span> <span data-ttu-id="ac3c6-130">如果安裝程式順利完成，您會看到訊息指出該 hello 叢集啟動 hello 輸出中。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-130">If setup completes successfully, you see a message in hello output indicating that hello cluster is starting up.</span></span>

    ![在 VM 佈建後啟動的叢集安裝程式][cluster-setup-script]

    >[!TIP]
    > <span data-ttu-id="ac3c6-132">如果 hello VM 下載花很長的時間，您可以下載它使用 wget 或 curl 或透過瀏覽 toohello 連結所指定瀏覽器**config.vm.box_url** hello 檔案中`Vagrantfile`。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-132">If hello VM download is taking a long time, you can download it using wget or curl or through a browser by navigating toohello link specified by **config.vm.box_url** in hello file `Vagrantfile`.</span></span> <span data-ttu-id="ac3c6-133">在本機下載之後, 編輯`Vagrantfile`toopoint toohello 本機路徑下載 hello 映像的位置。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-133">After downloading it locally, edit `Vagrantfile` toopoint toohello local path where you downloaded hello image.</span></span> <span data-ttu-id="ac3c6-134">範例下載 hello 映像 too/home/users/test/azureservicefabric.tp8.box，然後設定**config.vm.box_url** toothat 路徑。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-134">For example if you downloaded hello image too/home/users/test/azureservicefabric.tp8.box, then set **config.vm.box_url** toothat path.</span></span>
    >

5. <span data-ttu-id="ac3c6-135">測試該 hello 叢集是否已正確設定瀏覽 http://192.168.50.50:19080/總管 （假設您保留 hello 預設的私人網路的 IP） 在 tooService Fabric 總管。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-135">Test that hello cluster has been set up correctly by navigating tooService Fabric Explorer at http://192.168.50.50:19080/Explorer (assuming you kept hello default private network IP).</span></span>

    ![Service Fabric 總管檢視從 hello 主機 Mac][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a><span data-ttu-id="ac3c6-137">在 Mac 上使用 Yeoman 建立應用程式</span><span class="sxs-lookup"><span data-stu-id="ac3c6-137">Create application on Mac using Yeoman</span></span>
<span data-ttu-id="ac3c6-138">Service Fabric 提供的 Scaffolding 工具可協助您從終端機使用 Yeoman 範本產生器建立 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-138">Service Fabric provides scaffolding tools which will help you create a Service Fabric application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="ac3c6-139">請遵循下列 tooensure 您尚未使用您的電腦上的 hello Service Fabric yeoman 範本產生器的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-139">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator working on your machine.</span></span>

1. <span data-ttu-id="ac3c6-140">您需要 toohave Node.js 及 NPM 安裝在您 mac 上。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-140">You need toohave Node.js and NPM installed on you mac.</span></span> <span data-ttu-id="ac3c6-141">如果沒有您可以安裝 Node.js 及 NPM 使用 Homebrew 使用 hello 下列。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-141">If not you can install Node.js and NPM using Homebrew using hello following.</span></span> <span data-ttu-id="ac3c6-142">toocheck hello 版本的 Node.js 及 NPM 安裝在您的 Mac 上，您可以使用 hello``-v``選項。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-142">toocheck hello versions of Node.js and NPM installed on your Mac, you can use hello ``-v`` option.</span></span>

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. <span data-ttu-id="ac3c6-143">在電腦上從 NPM 安裝 [Yeoman](http://yeoman.io/) 範本產生器</span><span class="sxs-lookup"><span data-stu-id="ac3c6-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  npm install -g yo
  ```
3. <span data-ttu-id="ac3c6-144">安裝 hello Yeoman 產生器要 toouse，hello 快速入門中的 hello 步驟[文件](service-fabric-get-started-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-144">Install hello Yeoman generator you want toouse, following hello steps in hello getting started [documentation](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="ac3c6-145">toocreate 服務網狀架構應用程式使用 Yeoman，步驟 hello-</span><span class="sxs-lookup"><span data-stu-id="ac3c6-145">toocreate Service Fabric Applications using Yeoman, follow hello steps -</span></span>

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. <span data-ttu-id="ac3c6-146">toobuild Mac 上的服務網狀架構 Java 應用程式，您必須為 JDK 1.8 和 Gradle hello 電腦上安裝。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-146">toobuild a Service Fabric Java application on Mac, you would need - JDK 1.8 and Gradle installed on hello machine.</span></span>


## <a name="install-hello-service-fabric-plugin-for-eclipse-neon"></a><span data-ttu-id="ac3c6-147">安裝適用於 Eclipse Neon hello Service Fabric 外掛程式</span><span class="sxs-lookup"><span data-stu-id="ac3c6-147">Install hello Service Fabric plugin for Eclipse Neon</span></span>

<span data-ttu-id="ac3c6-148">Service Fabric 會提供外掛程式的 hello **IDE Java 的 Eclipse Neon** ，可簡化建立、 建置和部署 Java 服務 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-148">Service Fabric provides a plugin for hello **Eclipse Neon for Java IDE** that can simplify hello process of creating, building, and deploying Java services.</span></span> <span data-ttu-id="ac3c6-149">您可以遵循 hello 這個一般中所述的安裝步驟[文件](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon)有關安裝或更新服務網狀架構 Eclipse 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-149">You can follow hello installation steps mentioned in this general [documentation](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) about installing or updating Service Fabric Eclipse plugin.</span></span>

>[!TIP]
> <span data-ttu-id="ac3c6-150">根據預設我們支援 hello 預設 IP hello 中所述``Vagrantfile``在 hello ``Local.json`` hello 產生應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-150">By default we support hello default IP as mentioned in hello ``Vagrantfile`` in hello ``Local.json`` of hello generated application.</span></span> <span data-ttu-id="ac3c6-151">如果您進行變更，並部署 Vagrant 與不同的 ip 位址時，請更新中的 hello 對應 IP``Local.json``您應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-151">In case you change that and deploy Vagrant with a different IP, please update hello corresponding IP in ``Local.json`` of your application as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac3c6-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ac3c6-152">Next steps</span></span>
<!-- Links -->
* [<span data-ttu-id="ac3c6-153">使用 Yeoman 在 Linux 上建立和部署第一個 Service Fabric Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="ac3c6-153">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="ac3c6-154">在 Linux 上使用適用於 Eclipse 的 Service Fabric 外掛程式建立和部署第一個 Service Fabric Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="ac3c6-154">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="ac3c6-155">在 hello Azure 入口網站中建立 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="ac3c6-155">Create a Service Fabric cluster in hello Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="ac3c6-156">建立 Service Fabric 叢集使用 hello Azure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="ac3c6-156">Create a Service Fabric cluster using hello Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
* [<span data-ttu-id="ac3c6-157">了解 hello Service Fabric 應用程式模型</span><span class="sxs-lookup"><span data-stu-id="ac3c6-157">Understand hello Service Fabric application model</span></span>](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
