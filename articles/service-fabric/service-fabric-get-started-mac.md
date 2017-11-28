---
title: "在 Mac OS X 上設定開發環境以搭配 Azure Service Fabric 運作 | Microsoft Docs"
description: "安裝執行階段、SDK 和工具，並建立本機開發叢集。 完成此設定之後，您就可以開始在 Mac OS X 上建置應用程式。"
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
ms.openlocfilehash: 8b4fc0ab9034263418cac42ced203035e0a8fcad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a><span data-ttu-id="7e153-104">在 Mac OS X 上設定開發環境</span><span class="sxs-lookup"><span data-stu-id="7e153-104">Set up your development environment on Mac OS X</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7e153-105">Windows</span><span class="sxs-lookup"><span data-stu-id="7e153-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="7e153-106">Linux</span><span class="sxs-lookup"><span data-stu-id="7e153-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="7e153-107">OSX</span><span class="sxs-lookup"><span data-stu-id="7e153-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="7e153-108">您可以建置 Service Fabric 應用程式以在使用 Mac OS X 的 Linux 叢集上執行。本文涵蓋如何設定您的 Mac 進行開發。</span><span class="sxs-lookup"><span data-stu-id="7e153-108">You can build Service Fabric applications to run on Linux clusters using Mac OS X. This article covers how to set up your Mac for development.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e153-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="7e153-109">Prerequisites</span></span>
<span data-ttu-id="7e153-110">Service Fabric 不會在 OS X 上以原生方式執行。若要執行本機 Service Fabric 叢集，我們提供使用 Vagrant 和 VirtualBox 的預先設定 Ubuntu 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7e153-110">Service Fabric does not run natively on OS X. To run a local Service Fabric cluster, we provide a pre-configured Ubuntu virtual machine using Vagrant and VirtualBox.</span></span> <span data-ttu-id="7e153-111">開始之前，您需要：</span><span class="sxs-lookup"><span data-stu-id="7e153-111">Before you get started, you need:</span></span>

* [<span data-ttu-id="7e153-112">Vagrant (v1.8.4 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="7e153-112">Vagrant (v1.8.4 or later)</span></span>](http://www.vagrantup.com/downloads.html)
* [<span data-ttu-id="7e153-113">VirtualBox</span><span class="sxs-lookup"><span data-stu-id="7e153-113">VirtualBox</span></span>](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> <span data-ttu-id="7e153-114">您需要使用互相支援的 Vagrant 和 VirtualBox 版本。</span><span class="sxs-lookup"><span data-stu-id="7e153-114">You need to use mutually supported versions of Vagrant and VirtualBox.</span></span> <span data-ttu-id="7e153-115">Vagrant 在不支援的 VirtualBox 版本上的行為可能不穩定。</span><span class="sxs-lookup"><span data-stu-id="7e153-115">Vagrant might behave erratically on an unsupported VirtualBox version.</span></span>
>

## <a name="create-the-local-vm"></a><span data-ttu-id="7e153-116">建立本機 VM</span><span class="sxs-lookup"><span data-stu-id="7e153-116">Create the local VM</span></span>
<span data-ttu-id="7e153-117">若要建立包含 5 個節點 Service Fabric 叢集的本機 VM，請執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="7e153-117">To create the local VM containing a 5-node Service Fabric cluster, perform the following steps:</span></span>

1. <span data-ttu-id="7e153-118">複製 `Vagrantfile` 存放庫</span><span class="sxs-lookup"><span data-stu-id="7e153-118">Clone the `Vagrantfile` repo</span></span>

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    <span data-ttu-id="7e153-119">此步驟會帶來包含 VM 組態的 `Vagrantfile` 檔案，以及下載 VM 的來源位置。</span><span class="sxs-lookup"><span data-stu-id="7e153-119">This steps bring downs the file `Vagrantfile` containing the VM configuration along with the location the VM is downloaded from.</span></span>

2. <span data-ttu-id="7e153-120">瀏覽至儲存機制的本機複本</span><span class="sxs-lookup"><span data-stu-id="7e153-120">Navigate to the local clone of the repo</span></span>

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. <span data-ttu-id="7e153-121">(選擇性) 修改預設 VM 設定</span><span class="sxs-lookup"><span data-stu-id="7e153-121">(Optional) Modify the default VM settings</span></span>

    <span data-ttu-id="7e153-122">根據預設，本機 VM 的設定如下所示︰</span><span class="sxs-lookup"><span data-stu-id="7e153-122">By default, the local VM is configured as follows:</span></span>

   * <span data-ttu-id="7e153-123">配置 3 GB 的記憶體</span><span class="sxs-lookup"><span data-stu-id="7e153-123">3 GB of memory allocated</span></span>
   * <span data-ttu-id="7e153-124">在 IP 192.168.50.50 設定且能夠傳遞 Mac 主機流量的私用主機網路</span><span class="sxs-lookup"><span data-stu-id="7e153-124">Private host network configured at IP 192.168.50.50 enabling passthrough of traffic from the Mac host</span></span>

     <span data-ttu-id="7e153-125">您可以變更上述任何一項設定或將其他組態新增至 `Vagrantfile` 中的 VM。</span><span class="sxs-lookup"><span data-stu-id="7e153-125">You can change either of these settings or add other configuration to the VM in the `Vagrantfile`.</span></span> <span data-ttu-id="7e153-126">如需設定選項的完整清單，請參閱 [Vagrant 文件](http://www.vagrantup.com/docs) 。</span><span class="sxs-lookup"><span data-stu-id="7e153-126">See the [Vagrant documentation](http://www.vagrantup.com/docs) for the full list of configuration options.</span></span>
4. <span data-ttu-id="7e153-127">建立 VM</span><span class="sxs-lookup"><span data-stu-id="7e153-127">Create the VM</span></span>

    ```bash
    vagrant up
    ```

   <span data-ttu-id="7e153-128">這個步驟可下載預先設定的 VM 映像、讓它在本機開機，然後在其中設定一個本機 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="7e153-128">This step downloads the preconfigured VM image, boot it locally, and then set up a local Service Fabric cluster in it.</span></span> <span data-ttu-id="7e153-129">您預計需花幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="7e153-129">You should expect it to take a few minutes.</span></span> <span data-ttu-id="7e153-130">如果安裝程式順利完成，您會在輸出中看到一則訊息，表示叢集正在啟動中。</span><span class="sxs-lookup"><span data-stu-id="7e153-130">If setup completes successfully, you see a message in the output indicating that the cluster is starting up.</span></span>

    ![在 VM 佈建後啟動的叢集安裝程式][cluster-setup-script]

    >[!TIP]
    > <span data-ttu-id="7e153-132">如果 VM 下載花費很長的時間，您可以使用 wget 或 curl 來下載它，或者透過瀏覽器瀏覽至 `Vagrantfile` 檔案中 **config.vm.box_url** 所指定的連結。</span><span class="sxs-lookup"><span data-stu-id="7e153-132">If the VM download is taking a long time, you can download it using wget or curl or through a browser by navigating to the link specified by **config.vm.box_url** in the file `Vagrantfile`.</span></span> <span data-ttu-id="7e153-133">在本機下載之後，編輯 `Vagrantfile` 以指向已下載映像的本機路徑。</span><span class="sxs-lookup"><span data-stu-id="7e153-133">After downloading it locally, edit `Vagrantfile` to point to the local path where you downloaded the image.</span></span> <span data-ttu-id="7e153-134">例如，如果您將映像下載至 /home/users/test/azureservicefabric.tp8.box，則將 **config.vm.box_url** 設定為該路徑。</span><span class="sxs-lookup"><span data-stu-id="7e153-134">For example if you downloaded the image to /home/users/test/azureservicefabric.tp8.box, then set **config.vm.box_url** to that path.</span></span>
    >

5. <span data-ttu-id="7e153-135">瀏覽至位於 http://192.168.50.50:19080/Explorer 的 Service Fabric Explorer (假設您保留預設的私人網路 IP)，測試是否已正確設定叢集。</span><span class="sxs-lookup"><span data-stu-id="7e153-135">Test that the cluster has been set up correctly by navigating to Service Fabric Explorer at http://192.168.50.50:19080/Explorer (assuming you kept the default private network IP).</span></span>

    ![從主機 Mac 檢視的 Service Fabric Explorer][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a><span data-ttu-id="7e153-137">在 Mac 上使用 Yeoman 建立應用程式</span><span class="sxs-lookup"><span data-stu-id="7e153-137">Create application on Mac using Yeoman</span></span>
<span data-ttu-id="7e153-138">Service Fabric 提供的 Scaffolding 工具可協助您從終端機使用 Yeoman 範本產生器建立 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7e153-138">Service Fabric provides scaffolding tools which will help you create a Service Fabric application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="7e153-139">請遵循下列步驟來確保您有 Service Fabric yeoman 範本產生器可在電腦上運作。</span><span class="sxs-lookup"><span data-stu-id="7e153-139">Please follow the steps below to ensure you have the Service Fabric yeoman template generator working on your machine.</span></span>

1. <span data-ttu-id="7e153-140">您必須在 Mac 上安裝 Node.js 和 NPM。</span><span class="sxs-lookup"><span data-stu-id="7e153-140">You need to have Node.js and NPM installed on you mac.</span></span> <span data-ttu-id="7e153-141">若未這麼做，您可以使用 Homebrew 安裝 Node.js 和 NPM。</span><span class="sxs-lookup"><span data-stu-id="7e153-141">If not you can install Node.js and NPM using Homebrew using the following.</span></span> <span data-ttu-id="7e153-142">若要檢查 Mac 上安裝的 Node.js 和 NPM 版本，您可以使用 ``-v`` 選項。</span><span class="sxs-lookup"><span data-stu-id="7e153-142">To check the versions of Node.js and NPM installed on your Mac, you can use the ``-v`` option.</span></span>

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. <span data-ttu-id="7e153-143">在電腦上從 NPM 安裝 [Yeoman](http://yeoman.io/) 範本產生器</span><span class="sxs-lookup"><span data-stu-id="7e153-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  npm install -g yo
  ```
3. <span data-ttu-id="7e153-144">遵循快速入門[文件](service-fabric-get-started-linux.md)中的步驟，安裝您要使用的 Yeoman 產生器。</span><span class="sxs-lookup"><span data-stu-id="7e153-144">Install the Yeoman generator you want to use, following the steps in the getting started [documentation](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="7e153-145">若要使用 Yeoman 建立 Service Fabric 應用程式，請遵循下列步驟 -</span><span class="sxs-lookup"><span data-stu-id="7e153-145">To create Service Fabric Applications using Yeoman, follow the steps -</span></span>

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. <span data-ttu-id="7e153-146">若要在 Mac 上建置 Service Fabric Java 應用程式，您必須在電腦上安裝 JDK 1.8 和 Gradle。</span><span class="sxs-lookup"><span data-stu-id="7e153-146">To build a Service Fabric Java application on Mac, you would need - JDK 1.8 and Gradle installed on the machine.</span></span>


## <a name="install-the-service-fabric-plugin-for-eclipse-neon"></a><span data-ttu-id="7e153-147">安裝適用於 Eclipse Neon 的 Service Fabric 外掛程式</span><span class="sxs-lookup"><span data-stu-id="7e153-147">Install the Service Fabric plugin for Eclipse Neon</span></span>

<span data-ttu-id="7e153-148">Service Fabric 為**適用於 Java IDE 的 Eclipse Neon** 提供了外掛程式，可簡化建立、建置和部署 Java 服務的程序。</span><span class="sxs-lookup"><span data-stu-id="7e153-148">Service Fabric provides a plugin for the **Eclipse Neon for Java IDE** that can simplify the process of creating, building, and deploying Java services.</span></span> <span data-ttu-id="7e153-149">您可以遵循這個有關安裝或更新 Service Fabric Eclipse 外掛程式的一般[文件](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon)中所述的安裝步驟。</span><span class="sxs-lookup"><span data-stu-id="7e153-149">You can follow the installation steps mentioned in this general [documentation](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) about installing or updating Service Fabric Eclipse plugin.</span></span>

>[!TIP]
> <span data-ttu-id="7e153-150">根據預設，我們支援如所產生應用程式之 ``Local.json`` 中的 ``Vagrantfile`` 所提交之預設 IP。</span><span class="sxs-lookup"><span data-stu-id="7e153-150">By default we support the default IP as mentioned in the ``Vagrantfile`` in the ``Local.json`` of the generated application.</span></span> <span data-ttu-id="7e153-151">如果您進行變更並使用不同的 IP 來部署 Vagrant，請在您應用程式的 ``Local.json`` 中更新對應的 IP。</span><span class="sxs-lookup"><span data-stu-id="7e153-151">In case you change that and deploy Vagrant with a different IP, please update the corresponding IP in ``Local.json`` of your application as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e153-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7e153-152">Next steps</span></span>
<!-- Links -->
* [<span data-ttu-id="7e153-153">使用 Yeoman 在 Linux 上建立和部署第一個 Service Fabric Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="7e153-153">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="7e153-154">在 Linux 上使用適用於 Eclipse 的 Service Fabric 外掛程式建立和部署第一個 Service Fabric Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="7e153-154">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="7e153-155">在 Azure 入口網站中建立 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="7e153-155">Create a Service Fabric cluster in the Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="7e153-156">使用 Azure Resource Manager 建立 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="7e153-156">Create a Service Fabric cluster using the Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
* [<span data-ttu-id="7e153-157">了解 Service Fabric 應用程式模型</span><span class="sxs-lookup"><span data-stu-id="7e153-157">Understand the Service Fabric application model</span></span>](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
