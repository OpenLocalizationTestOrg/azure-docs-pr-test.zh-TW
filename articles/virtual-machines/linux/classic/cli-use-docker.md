---
title: "aaaUsing hello Linux on Azure 的 Docker VM 延伸模組"
description: "描述 Docker 和 hello Azure 虛擬機器擴充功能，並示範 tooprogrammatically Azure 的 docker 主機使用 Azure CLI hello hello 命令列上所建立的虛擬機器。"
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: eaff75e3-d929-4931-a4a1-8c377a8e7302
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/29/2016
ms.author: rasquill
ms.openlocfilehash: 1e192ad7c273aa9c997ea7bfa53b7de0b41a43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-from-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="95c8e-103">使用從 hello Azure 命令列介面 (Azure CLI) hello Docker VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="95c8e-103">Using hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="95c8e-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="95c8e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="95c8e-105">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="95c8e-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="95c8e-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="95c8e-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="95c8e-107">如需搭配 hello 資源管理員模型使用 hello Docker VM 擴充功能資訊，請參閱[這裡](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="95c8e-107">For information about using hello Docker VM extension with hello Resource Manager model, see [here](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="95c8e-108">本主題描述如何 toocreate 具有從 hello hello Docker VM 擴充功能的 VM 服務在 Azure CLI 任何平台上的管理 (asm) 模式。</span><span class="sxs-lookup"><span data-stu-id="95c8e-108">This topic describes how toocreate a VM with hello Docker VM Extension from hello service management (asm) mode in Azure CLI on any platform.</span></span> <span data-ttu-id="95c8e-109">[Docker](https://www.docker.com/)是 hello 的其中一個最普遍使用的虛擬化方法[Linux 容器](http://en.wikipedia.org/wiki/LXC)而不是虛擬機器做為隔離資料，並在共用資源上運算的方式。</span><span class="sxs-lookup"><span data-stu-id="95c8e-109">[Docker](https://www.docker.com/) is one of hello most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="95c8e-110">您可以使用 hello Docker VM 擴充功能和 hello [Azure Linux 代理程式](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)toocreate 裝載任何數目的容器應用程式在 Azure 上的 Docker VM。</span><span class="sxs-lookup"><span data-stu-id="95c8e-110">You can use hello Docker VM extension and hello [Azure Linux Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate a Docker VM that hosts any number of containers for your applications on Azure.</span></span> <span data-ttu-id="95c8e-111">toosee 高層級容器和 lamdba 的優點的討論，請參閱 「 hello [Docker 高的層級抄寫](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard)。</span><span class="sxs-lookup"><span data-stu-id="95c8e-111">toosee a high-level discussion of containers and their advantages, see hello [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>

## <a name="how-toouse-hello-docker-vm-extension-with-azure"></a><span data-ttu-id="95c8e-112">如何 toouse hello 與 Azure 的 Docker VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="95c8e-112">How toouse hello Docker VM Extension with Azure</span></span>
<span data-ttu-id="95c8e-113">toouse 與 Azure 的 hello Docker VM 擴充功能，您必須安裝新版 hello [Azure 命令列介面](https://github.com/Azure/azure-sdk-tools-xplat)(Azure CLI) 高於 0.8.6 （如這個寫入 hello 的目前版本是 0.10.0）。</span><span class="sxs-lookup"><span data-stu-id="95c8e-113">toouse hello Docker VM extension with Azure, you must install a version of hello [Azure Command-Line Interface](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) higher than 0.8.6 (as of this writing hello current version is 0.10.0).</span></span> <span data-ttu-id="95c8e-114">您可以安裝 hello Azure CLI Mac、 Linux 及 Windows 上。</span><span class="sxs-lookup"><span data-stu-id="95c8e-114">You can install hello Azure CLI on Mac, Linux, and Windows.</span></span>

<span data-ttu-id="95c8e-115">hello 完整程序 toouse Azure 上的 Docker 很簡單：</span><span class="sxs-lookup"><span data-stu-id="95c8e-115">hello complete process toouse Docker on Azure is simple:</span></span>

* <span data-ttu-id="95c8e-116">要從中 toocontrol Azure 的 hello 電腦上安裝 hello Azure CLI 和其相依性 （在 Windows 中，這將會執行為虛擬機器的 Linux 散發套件）</span><span class="sxs-lookup"><span data-stu-id="95c8e-116">Install hello Azure CLI and its dependencies on hello computer from which you want toocontrol Azure (on Windows, this will be a Linux distribution running as a virtual machine)</span></span>
* <span data-ttu-id="95c8e-117">在 Azure 中使用 hello Azure CLI Docker 命令 toocreate VM Docker 主機</span><span class="sxs-lookup"><span data-stu-id="95c8e-117">Use hello Azure CLI Docker commands toocreate a VM Docker host in Azure</span></span>
* <span data-ttu-id="95c8e-118">在您的 Docker VM 在 Azure 中使用本機 Docker 命令 toomanage hello Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="95c8e-118">Use hello local Docker commands toomanage your Docker containers in your Docker VM in Azure.</span></span>

### <a name="install-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="95c8e-119">安裝 Azure 命令列介面 (Azure CLI) hello</span><span class="sxs-lookup"><span data-stu-id="95c8e-119">Install hello Azure Command-Line Interface (Azure CLI)</span></span>
<span data-ttu-id="95c8e-120">tooinstall 和設定 hello Azure CLI，請參閱[tooinstall hello Azure 命令列介面的方式](../../../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="95c8e-120">tooinstall and configure hello Azure CLI, see [How tooinstall hello Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span> <span data-ttu-id="95c8e-121">tooconfirm hello 安裝類型`azure`hello 的命令提示字元，並在短時間之後您應該會看見 hello Azure CLI ASCII 封面，列出 hello basic 命令可用 tooyou。</span><span class="sxs-lookup"><span data-stu-id="95c8e-121">tooconfirm hello installation, type `azure` at hello command prompt and after a short moment you should see hello Azure CLI ASCII art, which lists hello basic commands available tooyou.</span></span> <span data-ttu-id="95c8e-122">如果 hello 安裝正確運作，您應該能夠 tootype`azure help vm`看到其中一個列出的 hello 命令為"docker"。</span><span class="sxs-lookup"><span data-stu-id="95c8e-122">If hello installation worked correctly, you should be able tootype `azure help vm` and see that one of hello listed commands is "docker".</span></span>

> [!NOTE]
> <span data-ttu-id="95c8e-123">Docker 有工具適用於 Windows、 [Docker 機器](https://docs.docker.com/installation/windows/)，而您也可以使用 docker 用戶端，您可以為 docker 主機與 Azure Vm 搭配使用 toowork tooautomate hello 建立。</span><span class="sxs-lookup"><span data-stu-id="95c8e-123">Docker has tools for Windows, [Docker Machine](https://docs.docker.com/installation/windows/), which you can also use tooautomate hello creation of a docker client that you can use toowork with Azure VMs as docker hosts.</span></span>
> 
> 

### <a name="connect-hello-azure-cli-tootooyour-azure-account"></a><span data-ttu-id="95c8e-124">連接 hello Azure CLI tootooyour Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="95c8e-124">Connect hello Azure CLI tootooyour Azure Account</span></span>
<span data-ttu-id="95c8e-125">您可以使用 Azure CLI hello 之前必須以 hello Azure CLI 平台上對您的 Azure 帳戶的認證進行關聯。</span><span class="sxs-lookup"><span data-stu-id="95c8e-125">Before you can use hello Azure CLI you must associate your Azure account credentials with hello Azure CLI on your platform.</span></span> <span data-ttu-id="95c8e-126">hello 區段[如何 tooconnect tooyour Azure 訂用帳戶](../../../xplat-cli-connect.md)說明 tooeither 如何下載和匯入您**.publishsettings**檔案，或將 Azure CLI 與組織識別碼產生關聯。</span><span class="sxs-lookup"><span data-stu-id="95c8e-126">hello section [How tooconnect tooyour Azure subscription](../../../xplat-cli-connect.md) explains how tooeither download and import your **.publishsettings** file or associate your Azure CLI with an organizational id.</span></span>

> [!NOTE]
> <span data-ttu-id="95c8e-127">有一些行為差異時使用其中一種或 hello 其他方法的驗證，因此務必確定上述 toounderstand hello 不同功能的 tooread hello 文件。</span><span class="sxs-lookup"><span data-stu-id="95c8e-127">There are some differences in behavior when using one or hello other methods of authentication, so do be sure tooread hello document above toounderstand hello different functionality.</span></span>
> 
> 

### <a name="install-docker-and-use-hello-docker-vm-extension-for-azure"></a><span data-ttu-id="95c8e-128">將 Docker 安裝和使用 Azure 的 hello Docker VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="95c8e-128">Install Docker and use hello Docker VM Extension for Azure</span></span>
<span data-ttu-id="95c8e-129">請遵循 hello [Docker 安裝指示](https://docs.docker.com/installation/#installation)tooinstall Docker 在本機電腦上的。</span><span class="sxs-lookup"><span data-stu-id="95c8e-129">Follow hello [Docker installation instructions](https://docs.docker.com/installation/#installation) tooinstall Docker locally on your computer.</span></span>

<span data-ttu-id="95c8e-130">toouse Docker 的 Azure 虛擬機器，用於 hello VM 的 hello Linux 映像必須已在 hello [Azure Linux VM 代理程式](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)安裝。</span><span class="sxs-lookup"><span data-stu-id="95c8e-130">toouse Docker with an Azure Virtual Machine, hello Linux image used for hello VM must have hello [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) installed.</span></span> <span data-ttu-id="95c8e-131">目前來說，只有兩種映像類型提供此安裝：</span><span class="sxs-lookup"><span data-stu-id="95c8e-131">Currently, there are only two types of images that provide this:</span></span>

* <span data-ttu-id="95c8e-132">Ubuntu 從 hello Azure 映像庫映像或</span><span class="sxs-lookup"><span data-stu-id="95c8e-132">An Ubuntu image from hello Azure Image Gallery or</span></span>
* <span data-ttu-id="95c8e-133">自訂的 Linux 映像，您已建立以 hello Azure Linux VM 代理程式安裝和設定。</span><span class="sxs-lookup"><span data-stu-id="95c8e-133">A custom Linux image that you have created with hello Azure Linux VM Agent installed and configured.</span></span> <span data-ttu-id="95c8e-134">請參閱[Azure Linux VM 代理程式](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)如需有關如何 toobuild 自訂 Linux VM 以 hello Azure VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="95c8e-134">See [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about how toobuild a custom Linux VM with hello Azure VM Agent.</span></span>

### <a name="using-hello-azure-image-gallery"></a><span data-ttu-id="95c8e-135">使用 hello Azure 映像庫</span><span class="sxs-lookup"><span data-stu-id="95c8e-135">Using hello Azure Image Gallery</span></span>
<span data-ttu-id="95c8e-136">從 Bash 或終端機工作階段中，使用下列 Azure CLI 命令 toolocate 輸入 hello hello VM 圖庫 toouse 中的最新 Ubuntu 映像的 hello</span><span class="sxs-lookup"><span data-stu-id="95c8e-136">From a Bash or Terminal session, use hello following Azure CLI command toolocate hello most recent Ubuntu image in hello VM gallery toouse by typing</span></span>

`azure vm image list | grep Ubuntu-14_04`

<span data-ttu-id="95c8e-137">選取其中一個 hello 映像名稱，例如`b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`，並使用 hello 下列命令 toocreate 使用該映像的新 VM。</span><span class="sxs-lookup"><span data-stu-id="95c8e-137">and select one of hello image names, such as `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, and use hello following command toocreate a new VM using that image.</span></span>

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

<span data-ttu-id="95c8e-138">其中：</span><span class="sxs-lookup"><span data-stu-id="95c8e-138">where:</span></span>

* <span data-ttu-id="95c8e-139">*&lt;vm cloudservice 名稱&gt;* hello hello 會變成 hello Docker 容器主機電腦在 Azure 中的 VM 名稱</span><span class="sxs-lookup"><span data-stu-id="95c8e-139">*&lt;vm-cloudservice name&gt;* is hello name of hello VM that will become hello Docker container host computer in Azure</span></span>
* <span data-ttu-id="95c8e-140">*&lt;使用者名稱&gt;* hello hello 預設根使用者的 hello VM 的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="95c8e-140">*&lt;username&gt;* is hello username of hello default root user of hello VM</span></span>
* <span data-ttu-id="95c8e-141">*&lt;密碼&gt;* hello 密碼的 hello *username*帳戶符合 azure 的 hello 標準的複雜性</span><span class="sxs-lookup"><span data-stu-id="95c8e-141">*&lt;password&gt;* is hello password of hello *username* account that meets hello standards of complexity for Azure</span></span>

> [!NOTE]
> <span data-ttu-id="95c8e-142">目前的密碼必須至少為 8 個字元、 包含一個小寫和一個大寫字元、 數字和特殊字元，例如其中一個 hello 下列字元： `!@#$%^&+=`。</span><span class="sxs-lookup"><span data-stu-id="95c8e-142">Currently, a password must be at least 8 characters, contain one lower case and one upper case character, a number, and a special character such as one of hello following characters: `!@#$%^&+=`.</span></span> <span data-ttu-id="95c8e-143">否，hello 期間在 hello hello 前面句子的結尾不是特殊字元。</span><span class="sxs-lookup"><span data-stu-id="95c8e-143">No, hello period at hello end of hello preceding sentence is NOT a special character.</span></span>
> 
> 

<span data-ttu-id="95c8e-144">如果 hello 命令執行成功，您應該會看到類似 hello 下列程式碼，根據 hello 精確引數和您所使用的選項：</span><span class="sxs-lookup"><span data-stu-id="95c8e-144">If hello command was successful, you should see something like hello following, depending on hello precise arguments and options you used:</span></span>

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> <span data-ttu-id="95c8e-145">建立虛擬機器可能需要幾分鐘的時間，但已佈建它之後 (hello 狀態值是`ReadyRole`) hello Docker daemon (hello Docker 服務) 啟動，而且您可以連線 toohello Docker 容器主機。</span><span class="sxs-lookup"><span data-stu-id="95c8e-145">Creating a virtual machine can take a few minutes, but after it has been provisioned (hello state value is `ReadyRole`) hello Docker daemon (hello Docker service) starts and you can connect toohello Docker container host.</span></span>
> 
> 

<span data-ttu-id="95c8e-146">tootest hello Docker VM，您已建立在 Azure 中，類型</span><span class="sxs-lookup"><span data-stu-id="95c8e-146">tootest hello Docker VM you have created in Azure, type</span></span>

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

<span data-ttu-id="95c8e-147">其中 *&lt;vm--您為使用名稱&gt;* hello hello 過您的呼叫中使用的虛擬機器名稱`azure vm docker create`。</span><span class="sxs-lookup"><span data-stu-id="95c8e-147">where *&lt;vm-name-you-used&gt;* is hello name of hello virtual machine that you used in your call too`azure vm docker create`.</span></span> <span data-ttu-id="95c8e-148">您應該會看到類似 toohello 下列程式碼，這表示您的 Docker 主機 VM 已啟動並在 Azure 中執行並等候命令。</span><span class="sxs-lookup"><span data-stu-id="95c8e-148">You should see something similar toohello following, which indicates that your Docker Host VM is up and running in Azure and waiting for your commands.</span></span> 

<span data-ttu-id="95c8e-149">現在您可以嘗試使用您的 docker 用戶端 tooobtain 資訊 tooconnect (在某些 Docker 用戶端設定，例如，在 Mac 上，您可能會有 toouse `sudo`):</span><span class="sxs-lookup"><span data-stu-id="95c8e-149">Now you can try tooconnect using your docker client tooobtain information (in some Docker client setups, such as that on Mac, you may have toouse `sudo`):</span></span>

    sudo docker --tls -H tcp://testsshasm.cloudapp.net:2376 info
    Password:
    Containers: 0
    Images: 0
    Storage Driver: devicemapper
    Pool Name: docker-8:1-131781-pool
    Pool Blocksize: 65.54 kB
    Backing Filesystem: extfs
    Data file: /dev/loop0
    Metadata file: /dev/loop1
    Data Space Used: 1.821 GB
    Data Space Total: 107.4 GB
    Data Space Available: 28 GB
    Metadata Space Used: 1.479 MB
    Metadata Space Total: 2.147 GB
    Metadata Space Available: 2.146 GB
    Udev Sync Supported: true
    Deferred Removal Enabled: false
    Data loop file: /var/lib/docker/devicemapper/devicemapper/data
    Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
    Library Version: 1.02.77 (2012-10-15)
    Execution Driver: native-0.2
    Logging Driver: json-file
    Kernel Version: 3.19.0-28-generic
    Operating System: Ubuntu 14.04.3 LTS
    CPUs: 1
    Total Memory: 1.637 GiB
    Name: testsshasm
    WARNING: No swap limit support

<span data-ttu-id="95c8e-150">只要 toobe 確定它是所有工作，您可以檢查 hello VM hello Docker 擴充功能：</span><span class="sxs-lookup"><span data-stu-id="95c8e-150">Just toobe certain that it's all working, you can examine hello VM for hello Docker extension:</span></span>

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a><span data-ttu-id="95c8e-151">Docker 主機 VM 驗證</span><span class="sxs-lookup"><span data-stu-id="95c8e-151">Docker Host VM Authentication</span></span>
<span data-ttu-id="95c8e-152">此外 toocreating hello Docker VM hello`azure vm docker create`命令也會自動建立 hello 必要的憑證 tooallow Docker 用戶端電腦 tooconnect toohello Azure 容器主機使用 HTTPS，和 hello 憑證儲存在兩者hello 用戶端和主機電腦，視需要。</span><span class="sxs-lookup"><span data-stu-id="95c8e-152">In addition toocreating hello Docker VM, hello `azure vm docker create` command also automatically creates hello necessary certificates tooallow your Docker client computer tooconnect toohello Azure container host using HTTPS, and hello certificates are stored on both hello client and host machines, as appropriate.</span></span> <span data-ttu-id="95c8e-153">在後續的嘗試，會重複使用 hello 現有憑證，並將其與 hello 新主機共用中。</span><span class="sxs-lookup"><span data-stu-id="95c8e-153">On subsequent attempts, hello existing certificates are reused and shared with hello new host.</span></span>

<span data-ttu-id="95c8e-154">根據預設，憑證會放在`~/.docker`，Docker 將會在連接埠上的設定的 toorun **2376年**。</span><span class="sxs-lookup"><span data-stu-id="95c8e-154">By default, certificates are placed in `~/.docker`, and Docker will be configured toorun on port **2376**.</span></span> <span data-ttu-id="95c8e-155">如果您想要不同的通訊埠 toouse 或目錄，則您可以使用 hello 下列其中一種`azure vm docker create`命令列選項 tooconfigure，您的 Docker 容器主機 VM toouse 不同的通訊埠或不同的憑證，來連接用戶端：</span><span class="sxs-lookup"><span data-stu-id="95c8e-155">If you would like toouse a different port or directory, then you may use one of hello following `azure vm docker create` command line options tooconfigure your Docker container host VM toouse a different port or different certificates for connecting clients:</span></span>

```
-dp, --docker-port [port]              Port toouse for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

<span data-ttu-id="95c8e-156">hello hello 主機上的 Docker 精靈是設定為 toolisten 和驗證用戶端 hello 上的連接指定通訊埠使用 hello 憑證產生 hello`azure vm docker create`命令。</span><span class="sxs-lookup"><span data-stu-id="95c8e-156">hello Docker daemon on hello host is configured toolisten for and authenticate client connections on hello specified port using hello certificates generated by hello `azure vm docker create` command.</span></span> <span data-ttu-id="95c8e-157">hello 用戶端電腦必須具有這些憑證 toogain 存取 toohello Docker 主機。</span><span class="sxs-lookup"><span data-stu-id="95c8e-157">hello client machine must have these certificates toogain access toohello Docker host.</span></span>

> [!NOTE]
> <span data-ttu-id="95c8e-158">網路的主機執行時並沒有這些憑證將會很容易遭受 tooanyone 可以 tooconnect toohello 機器。</span><span class="sxs-lookup"><span data-stu-id="95c8e-158">A networked host running without these certificates will be vulnerable tooanyone that can tooconnect toohello machine.</span></span> <span data-ttu-id="95c8e-159">修改 hello 預設組態之前，請確定您已了解 hello 風險 tooyour 電腦和應用程式。</span><span class="sxs-lookup"><span data-stu-id="95c8e-159">Before you modify hello default configuration, ensure that you understand hello risks tooyour computers and applications.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="95c8e-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="95c8e-160">Next steps</span></span>
* <span data-ttu-id="95c8e-161">您已準備好 toogo toohello [Docker 使用者指南]並使用您的 Docker VM。</span><span class="sxs-lookup"><span data-stu-id="95c8e-161">You are ready toogo toohello [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="95c8e-162">toocreate Docker 功能中的 VM hello 新入口網站，請參閱[toouse hello Docker VM 擴充功能以 hello 入口網站的方式]。</span><span class="sxs-lookup"><span data-stu-id="95c8e-162">toocreate a Docker-enabled VM in hello new portal, see [How toouse hello Docker VM Extension with hello Portal].</span></span>
* <span data-ttu-id="95c8e-163">hello Azure Docker VM 擴充功能也支援 Docker Compose，其在任何環境中使用宣告式 YAML 檔案 tootake 開發人員建立模型的應用程式，並產生一致的部署。</span><span class="sxs-lookup"><span data-stu-id="95c8e-163">hello Azure Docker VM extension also supports Docker Compose, which uses a declarative YAML file tootake a developer-modeled application across any environment and generate a consistent deployment.</span></span> <span data-ttu-id="95c8e-164">請參閱[開始使用 Docker 和撰寫 toodefine 和 Azure 虛擬機器上執行多個容器應用程式]。</span><span class="sxs-lookup"><span data-stu-id="95c8e-164">See [Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine].</span></span>  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How toouse hello Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 tooanother azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 tooanother azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md
[toouse hello Docker VM 擴充功能以 hello 入口網站的方式]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/

[Docker 使用者指南]:https://docs.docker.com/userguide/

[開始使用 Docker 和撰寫 toodefine 和 Azure 虛擬機器上執行多個容器應用程式]:../docker-compose-quickstart.md
