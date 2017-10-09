---
title: "Linux RDMA 叢集 toorun MPI 應用程式總 aaaSet |Microsoft 文件"
description: "建立 Linux 叢集的大小 H16r 的 H16mr、 A8、 A9 Vm toouse hello Azure RDMA 網路 toorun MPI 應用程式"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 01834bad-c8e6-48a3-b066-7f1719047dd2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.openlocfilehash: 3199317a37b095e80718d6724954687d30aea3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-linux-rdma-cluster-toorun-mpi-applications"></a><span data-ttu-id="b99b3-103">設定 Linux RDMA 叢集 toorun MPI 應用程式</span><span class="sxs-lookup"><span data-stu-id="b99b3-103">Set up a Linux RDMA cluster toorun MPI applications</span></span>
<span data-ttu-id="b99b3-104">了解 tooset Linux RDMA 註冊在 Azure 中的叢集化[高效能計算 VM 大小](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)toorun 平行訊息傳遞介面 (MPI) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b99b3-104">Learn how tooset up a Linux RDMA cluster in Azure with [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun parallel Message Passing Interface (MPI) applications.</span></span> <span data-ttu-id="b99b3-105">本文提供步驟 tooprepare Linux HPC 映像 toorun Intel MPI 叢集上。</span><span class="sxs-lookup"><span data-stu-id="b99b3-105">This article provides steps tooprepare a Linux HPC image toorun Intel MPI on a cluster.</span></span> <span data-ttu-id="b99b3-106">準備工作之後, 您部署的 Vm 使用此映像和一個 hello 具備 RDMA 功能的 Azure VM 大小 （目前 H16r、 H16mr、 A8、 或 A9） 的叢集。</span><span class="sxs-lookup"><span data-stu-id="b99b3-106">After preparation, you deploy a cluster of VMs using this image and one of hello RDMA-capable Azure VM sizes (currently H16r, H16mr, A8, or A9).</span></span> <span data-ttu-id="b99b3-107">使用 hello 叢集 toorun MPI 應用程式，透過遠端直接記憶體存取 (RDMA) 技術為基礎的低延遲、 高輸送量網路有效地進行通訊。</span><span class="sxs-lookup"><span data-stu-id="b99b3-107">Use hello cluster toorun MPI applications that communicate efficiently over a low-latency, high-throughput network based on remote direct memory access (RDMA) technology.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b99b3-108">Azure 建立和處理資源的部署模型有兩種：[Azure Resource Manager](../../../resource-manager-deployment-model.md) 和傳統。</span><span class="sxs-lookup"><span data-stu-id="b99b3-108">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="b99b3-109">本文說明如何使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="b99b3-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="b99b3-110">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="b99b3-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

## <a name="cluster-deployment-options"></a><span data-ttu-id="b99b3-111">叢集部署選項</span><span class="sxs-lookup"><span data-stu-id="b99b3-111">Cluster deployment options</span></span>
<span data-ttu-id="b99b3-112">以下是方法，不論作業排程器，您可以使用 toocreate RDMA Linux 叢集。</span><span class="sxs-lookup"><span data-stu-id="b99b3-112">Following are methods you can use toocreate a Linux RDMA cluster with or without a job scheduler.</span></span>

* <span data-ttu-id="b99b3-113">**Azure CLI 指令碼**： 如本文稍後所示，使用 hello [Azure 命令列介面](../../../cli-install-nodejs.md)(CLI) tooscript hello 部署具備 RDMA 功能的 Vm 的叢集。</span><span class="sxs-lookup"><span data-stu-id="b99b3-113">**Azure CLI scripts**: As shown later in this article, use hello [Azure command-line interface](../../../cli-install-nodejs.md) (CLI) tooscript hello deployment of a cluster of RDMA-capable VMs.</span></span> <span data-ttu-id="b99b3-114">服務管理模式中的 hello CLI hello 叢集節點建立循序在 hello 傳統部署模型中，以便部署多個計算節點可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="b99b3-114">hello CLI in Service Management mode creates hello cluster nodes serially in hello classic deployment model, so deploying many compute nodes might take several minutes.</span></span> <span data-ttu-id="b99b3-115">tooenable hello RDMA 網路連線，當您使用 hello 傳統部署模型，將 hello Vm 部署在 hello 相同雲端服務。</span><span class="sxs-lookup"><span data-stu-id="b99b3-115">tooenable hello RDMA network connection when you use hello classic deployment model, deploy hello VMs in hello same cloud service.</span></span>
* <span data-ttu-id="b99b3-116">**Azure 資源管理員範本**： 您也可以使用 hello 資源管理員部署模型 toodeploy toohello RDMA 網路連線的 RDMA 功能的 Vm 的叢集。</span><span class="sxs-lookup"><span data-stu-id="b99b3-116">**Azure Resource Manager templates**: You can also use hello Resource Manager deployment model toodeploy a cluster of RDMA-capable VMs that connects toohello RDMA network.</span></span> <span data-ttu-id="b99b3-117">您可以[建立您自己的範本](../../../resource-group-authoring-templates.md)，或檢查 hello [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/)Microsoft 或 hello 社群 toodeploy hello 您想的方案所提供的範本。</span><span class="sxs-lookup"><span data-stu-id="b99b3-117">You can [create your own template](../../../resource-group-authoring-templates.md), or check hello [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/) for templates contributed by Microsoft or hello community toodeploy hello solution you want.</span></span> <span data-ttu-id="b99b3-118">資源管理員範本可提供快速且可靠的方式 toodeploy Linux 叢集。</span><span class="sxs-lookup"><span data-stu-id="b99b3-118">Resource Manager templates can provide a fast and reliable way toodeploy a Linux cluster.</span></span> <span data-ttu-id="b99b3-119">tooenable hello RDMA 網路連線，當您使用 hello Resource Manager 部署模型，部署在 hello hello Vm 相同可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="b99b3-119">tooenable hello RDMA network connection when you use hello Resource Manager deployment model, deploy hello VMs in hello same availability set.</span></span>
* <span data-ttu-id="b99b3-120">**HPC Pack**： 在 Azure 中建立 Microsoft HPC Pack 叢集並加入具備 RDMA 功能的計算節點執行支援的 Linux 發佈 tooaccess hello RDMA 網路。</span><span class="sxs-lookup"><span data-stu-id="b99b3-120">**HPC Pack**: Create a Microsoft HPC Pack cluster in Azure and add RDMA-capable compute nodes that run a supported Linux distribution tooaccess hello RDMA network.</span></span> <span data-ttu-id="b99b3-121">如需詳細資訊，請參閱[開始在 Azure 中的 HPC Pack 叢集使用 Linux 計算節點](hpcpack-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="b99b3-121">For more information, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="sample-deployment-steps-in-hello-classic-model"></a><span data-ttu-id="b99b3-122">Hello 傳統模型中的範例部署步驟</span><span class="sxs-lookup"><span data-stu-id="b99b3-122">Sample deployment steps in hello classic model</span></span>
<span data-ttu-id="b99b3-123">hello 下列步驟說明如何 toouse hello Azure CLI toodeploy 從 hello Azure Marketplace 的 SUSE Linux Enterprise Server (SLES) 12 SP1 HPC VM 自訂方法，及建立自訂的 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="b99b3-123">hello following steps show how toouse hello Azure CLI toodeploy a SUSE Linux Enterprise Server (SLES) 12 SP1 HPC VM from hello Azure Marketplace, customize it, and create a custom VM image.</span></span> <span data-ttu-id="b99b3-124">然後您可以使用 hello 映像，請 tooscript hello 部署具備 RDMA 功能的 Vm 的叢集。</span><span class="sxs-lookup"><span data-stu-id="b99b3-124">Then you can use hello image tooscript hello deployment of a cluster of RDMA-capable VMs.</span></span>

> [!TIP]
> <span data-ttu-id="b99b3-125">使用類似步驟 toodeploy CentOS 架構 HPC hello Azure Marketplace 中的影像為基礎的 RDMA 功能的 Vm 的叢集。</span><span class="sxs-lookup"><span data-stu-id="b99b3-125">Use similar steps toodeploy a cluster of RDMA-capable VMs based on CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="b99b3-126">如所述，某些步驟會稍有不同。</span><span class="sxs-lookup"><span data-stu-id="b99b3-126">Some steps differ slightly, as noted.</span></span> 
>
>

### <a name="prerequisites"></a><span data-ttu-id="b99b3-127">必要條件</span><span class="sxs-lookup"><span data-stu-id="b99b3-127">Prerequisites</span></span>
* <span data-ttu-id="b99b3-128">**用戶端電腦**： 需要 Mac、 Linux 或 Windows 用戶端電腦 toocommunicate 與 Azure。</span><span class="sxs-lookup"><span data-stu-id="b99b3-128">**Client computer**: You need a Mac, Linux, or Windows client computer toocommunicate with Azure.</span></span> <span data-ttu-id="b99b3-129">這些步驟假設您使用 Linux 用戶端。</span><span class="sxs-lookup"><span data-stu-id="b99b3-129">These steps assume you are using a Linux client.</span></span>
* <span data-ttu-id="b99b3-130">**Azure 訂用帳戶**：如果您沒有訂用帳戶，只需要幾分鐘就可以建立[免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="b99b3-130">**Azure subscription**: If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span> <span data-ttu-id="b99b3-131">針對較大的叢集，請考慮隨用隨付訂用帳戶或其他購買選項。</span><span class="sxs-lookup"><span data-stu-id="b99b3-131">For larger clusters, consider a pay-as-you-go subscription or other purchase options.</span></span>
* <span data-ttu-id="b99b3-132">**VM 大小可用性**: hello 遵循大小的執行個體都具有 RDMA 功能： H16r，H16mr、 A8、 A9。</span><span class="sxs-lookup"><span data-stu-id="b99b3-132">**VM size availability**: hello following instance sizes are RDMA capable: H16r, H16mr, A8, and A9.</span></span> <span data-ttu-id="b99b3-133">如需了解 Azure 區域中的可用性，請查看 [依區域提供的產品](https://azure.microsoft.com/regions/services/) 。</span><span class="sxs-lookup"><span data-stu-id="b99b3-133">Check [Products available by region](https://azure.microsoft.com/regions/services/) for availability in Azure regions.</span></span>
* <span data-ttu-id="b99b3-134">**核心配額**： 您可能需要 tooincrease hello 配額的核心 toodeploy 是需要大量計算 Vm 的叢集。</span><span class="sxs-lookup"><span data-stu-id="b99b3-134">**Cores quota**: You might need tooincrease hello quota of cores toodeploy a cluster of compute-intensive VMs.</span></span> <span data-ttu-id="b99b3-135">比方說，您需要至少 128 個核心，如果您想 toodeploy 8 A9 Vm 這篇文章中所示。</span><span class="sxs-lookup"><span data-stu-id="b99b3-135">For example, you need at least 128 cores if you want toodeploy 8 A9 VMs as shown in this article.</span></span> <span data-ttu-id="b99b3-136">您的訂閱也可能會限制 hello 特定 VM 大小系列，包括 hello H 序列中，您可以部署的核心數目。</span><span class="sxs-lookup"><span data-stu-id="b99b3-136">Your subscription might also limit hello number of cores you can deploy in certain VM size families, including hello H-series.</span></span> <span data-ttu-id="b99b3-137">toorequest 配額增加[開啟線上客戶支援要求](../../../azure-supportability/how-to-create-azure-support-request.md)不收費。</span><span class="sxs-lookup"><span data-stu-id="b99b3-137">toorequest a quota increase, [open an online customer support request](../../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
* <span data-ttu-id="b99b3-138">**Azure CLI**:[安裝](../../../cli-install-nodejs.md)hello Azure CLI 和[連接 tooyour Azure 訂用帳戶](../../../xplat-cli-connect.md)從 hello 用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="b99b3-138">**Azure CLI**: [Install](../../../cli-install-nodejs.md) hello Azure CLI and [connect tooyour Azure subscription](../../../xplat-cli-connect.md) from hello client computer.</span></span>

### <a name="provision-an-sles-12-sp1-hpc-vm"></a><span data-ttu-id="b99b3-139">佈建 SLES 12 SP1 HPC VM</span><span class="sxs-lookup"><span data-stu-id="b99b3-139">Provision an SLES 12 SP1 HPC VM</span></span>
<span data-ttu-id="b99b3-140">登入以 hello Azure CLI tooAzure 之後，執行`azure config list`hello 輸出的 tooconfirm 顯示服務管理模式。</span><span class="sxs-lookup"><span data-stu-id="b99b3-140">After signing in tooAzure with hello Azure CLI, run `azure config list` tooconfirm that hello output shows Service Management mode.</span></span> <span data-ttu-id="b99b3-141">如果不存在，請執行此命令設定 hello 模式：</span><span class="sxs-lookup"><span data-stu-id="b99b3-141">If it does not, set hello mode by running this command:</span></span>

    azure config mode asm


<span data-ttu-id="b99b3-142">輸入下列 toolist hello 所有 hello 訂用帳戶已授權的 toouse:</span><span class="sxs-lookup"><span data-stu-id="b99b3-142">Type hello following toolist all hello subscriptions you are authorized toouse:</span></span>

    azure account list

<span data-ttu-id="b99b3-143">hello 目前的作用中訂用帳戶會用來識別`Current`設定得`true`。</span><span class="sxs-lookup"><span data-stu-id="b99b3-143">hello current active subscription is identified with `Current` set too`true`.</span></span> <span data-ttu-id="b99b3-144">如果此訂用帳戶不 hello 一個要 toouse toocreate hello 叢集中，設定 hello 適當的訂用帳戶 ID 與 hello 作用中訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="b99b3-144">If this subscription isn't hello one you want toouse toocreate hello cluster, set hello appropriate subscription ID as hello active subscription:</span></span>

    azure account set <subscription-Id>

<span data-ttu-id="b99b3-145">toosee hello 公開可用的 SLES 12 SP1 HPC 映像，在 Azure 中，執行類似，hello 命令假設您的殼層環境支援**grep**:</span><span class="sxs-lookup"><span data-stu-id="b99b3-145">toosee hello publicly available SLES 12 SP1 HPC images in Azure, run a command like hello following, assuming your shell environment supports **grep**:</span></span>

    azure vm image list | grep "suse.*hpc"

<span data-ttu-id="b99b3-146">執行命令，像 hello 下列佈建的 RDMA 功能的 VM 與 SLES 12 SP1 HPC 映像：</span><span class="sxs-lookup"><span data-stu-id="b99b3-146">Provision an RDMA-capable VM with a SLES 12 SP1 HPC image by running a command like hello following:</span></span>

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

<span data-ttu-id="b99b3-147">其中：</span><span class="sxs-lookup"><span data-stu-id="b99b3-147">Where:</span></span>

* <span data-ttu-id="b99b3-148">hello 大小 (在此範例中 A9) 是其中一個 hello 具備 RDMA 功能的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="b99b3-148">hello size (A9 in this example) is one of hello RDMA-capable VM sizes.</span></span>
* <span data-ttu-id="b99b3-149">外部 SSH 連接埠號碼 hello (在此範例中，也就是 hello SSH 預設 22) 是任何有效的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="b99b3-149">hello external SSH port number (22 in this example, which is hello SSH default) is any valid port number.</span></span> <span data-ttu-id="b99b3-150">hello 內部 SSH 連接埠號碼設定 too22。</span><span class="sxs-lookup"><span data-stu-id="b99b3-150">hello internal SSH port number is set too22.</span></span>
* <span data-ttu-id="b99b3-151">新的雲端服務中建立 hello hello 位置所指定的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="b99b3-151">A new cloud service is created in hello Azure region specified by hello location.</span></span> <span data-ttu-id="b99b3-152">指定在哪個 hello VM 大小您選擇可用的位置。</span><span class="sxs-lookup"><span data-stu-id="b99b3-152">Specify a location in which hello VM size you choose is available.</span></span>
* <span data-ttu-id="b99b3-153">如需 SUSE 優先順序的支援 （這會產生額外費用），hello SLES 12 SP1 映像名稱目前可以在這兩個選項的其中一個：</span><span class="sxs-lookup"><span data-stu-id="b99b3-153">For SUSE priority support (which incurs additional charges), hello SLES 12 SP1 image name currently can be one of these two options:</span></span> 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-hello-vm"></a><span data-ttu-id="b99b3-154">自訂 hello VM</span><span class="sxs-lookup"><span data-stu-id="b99b3-154">Customize hello VM</span></span>
<span data-ttu-id="b99b3-155">Hello VM 完成佈建之後，使用 SSH toohello VM hello VM 的外部 IP 位址 （或 DNS 名稱），而且 hello 外部連接埠號碼設定，，，然後加以自訂。</span><span class="sxs-lookup"><span data-stu-id="b99b3-155">After hello VM finishes provisioning, SSH toohello VM by using hello VM's external IP address (or DNS name) and hello external port number you configured, and then customize it.</span></span> <span data-ttu-id="b99b3-156">連接的詳細資訊，請參閱[如何 tooa 執行 Linux 的虛擬機器上的 toolog](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b99b3-156">For connection details, see [How toolog on tooa virtual machine running Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b99b3-157">Hello hello VM 所設定的使用者身分執行命令，除非根目錄存取必要的 toocomplete 步驟。</span><span class="sxs-lookup"><span data-stu-id="b99b3-157">Perform commands as hello user you configured on hello VM, unless root access is required toocomplete a step.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b99b3-158">Microsoft Azure 不提供根目錄存取 tooLinux Vm。</span><span class="sxs-lookup"><span data-stu-id="b99b3-158">Microsoft Azure does not provide root access tooLinux VMs.</span></span> <span data-ttu-id="b99b3-159">toogain 系統管理存取權，使用者 toohello VM，使用執行命令的身分連接時`sudo`。</span><span class="sxs-lookup"><span data-stu-id="b99b3-159">toogain administrative access when connected as a user toohello VM, run commands by using `sudo`.</span></span>
>
>

* <span data-ttu-id="b99b3-160">**更新**：使用 zypper 安裝更新。</span><span class="sxs-lookup"><span data-stu-id="b99b3-160">**Updates**: Install updates by using zypper.</span></span> <span data-ttu-id="b99b3-161">您也可以 tooinstall NFS 公用程式。</span><span class="sxs-lookup"><span data-stu-id="b99b3-161">You might also want tooinstall NFS utilities.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="b99b3-162">在 SLES 12 SP1 HPC VM 中，我們建議您不要套用核心更新，可能會導致問題以 hello Linux RDMA 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="b99b3-162">In a SLES 12 SP1 HPC VM, we recommend that you don't apply kernel updates, which can cause issues with hello Linux RDMA drivers.</span></span>
  >
  >
* <span data-ttu-id="b99b3-163">**Intel MPI**: hello 上完成的安裝 Intel MPI hello SLES 12 SP1 HPC VM 執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b99b3-163">**Intel MPI**: Complete hello installation of Intel MPI on hello SLES 12 SP1 HPC VM by running hello following command:</span></span>

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* <span data-ttu-id="b99b3-164">**鎖定記憶體**: MPI 代碼 toolock hello 可用記憶體的 RDMA，新增或變更 hello 遵循 hello /etc/security/limits.conf 檔案中的設定。</span><span class="sxs-lookup"><span data-stu-id="b99b3-164">**Lock memory**: For MPI codes toolock hello memory available for RDMA, add or change hello following settings in hello /etc/security/limits.conf file.</span></span> <span data-ttu-id="b99b3-165">您需要根存取 tooedit 這個檔案。</span><span class="sxs-lookup"><span data-stu-id="b99b3-165">You need root access tooedit this file.</span></span>

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > <span data-ttu-id="b99b3-166">為了測試用途，您也可以設定 memlock toounlimited。</span><span class="sxs-lookup"><span data-stu-id="b99b3-166">For testing purposes, you can also set memlock toounlimited.</span></span> <span data-ttu-id="b99b3-167">例如： `<User or group name>    hard    memlock unlimited`。</span><span class="sxs-lookup"><span data-stu-id="b99b3-167">For example: `<User or group name>    hard    memlock unlimited`.</span></span> <span data-ttu-id="b99b3-168">如需詳細資訊，請參閱[設定鎖定的記憶體大小的最佳已知方法](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size)。</span><span class="sxs-lookup"><span data-stu-id="b99b3-168">For more information, see [Best known methods for setting locked memory size](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span></span>
  >
  >
* <span data-ttu-id="b99b3-169">**SLES Vm 的 SSH 金鑰**： 產生 SSH 金鑰 tooestablish 信任您的使用者帳戶在 hello 之間執行 MPI 工作時，計算 hello SLES 叢集中的節點。</span><span class="sxs-lookup"><span data-stu-id="b99b3-169">**SSH keys for SLES VMs**: Generate SSH keys tooestablish trust for your user account among hello compute nodes in hello SLES cluster when running MPI jobs.</span></span> <span data-ttu-id="b99b3-170">如果您部署 CentOS 型 HPC VM，請勿遵循此步驟。</span><span class="sxs-lookup"><span data-stu-id="b99b3-170">If you deployed a CentOS-based HPC VM, don't follow this step.</span></span> <span data-ttu-id="b99b3-171">您擷取 hello 映像並部署 hello 叢集之後，請參閱稍後 hello 的叢集節點之間的 passwordless SSH 信任此發行項 tooset 的指示。</span><span class="sxs-lookup"><span data-stu-id="b99b3-171">See instructions later in this article tooset up passwordless SSH trust among hello cluster nodes after you capture hello image and deploy hello cluster.</span></span>

    <span data-ttu-id="b99b3-172">toocreate SSH 金鑰，執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="b99b3-172">toocreate SSH keys, run hello following command.</span></span> <span data-ttu-id="b99b3-173">當提示您輸入時時，請選取**Enter** toogenerate hello 金鑰在 hello 預設位置，如果未設定密碼。</span><span class="sxs-lookup"><span data-stu-id="b99b3-173">When you are prompted for input, select **Enter** toogenerate hello keys in hello default location without setting a password.</span></span>

        ssh-keygen

    <span data-ttu-id="b99b3-174">附加 hello 公用金鑰 toohello authorized_keys 檔為已知的公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="b99b3-174">Append hello public key toohello authorized_keys file for known public keys.</span></span>

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    <span data-ttu-id="b99b3-175">在 hello ~/.ssh 目錄中，編輯或建立 hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="b99b3-175">In hello ~/.ssh directory, edit or create hello config file.</span></span> <span data-ttu-id="b99b3-176">提供您計劃在 Azure 中 (在此範例中 10.32.0.0/16) toouse hello IP 位址範圍的 hello 私人網路：</span><span class="sxs-lookup"><span data-stu-id="b99b3-176">Provide hello IP address range of hello private network that you plan toouse in Azure (10.32.0.0/16 in this example):</span></span>

        host 10.32.0.*
        StrictHostKeyChecking no

    <span data-ttu-id="b99b3-177">或者，列出在叢集中的每個 VM hello 私人網路 IP 位址，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b99b3-177">Alternatively, list hello private network IP address of each VM in your cluster as follows:</span></span>

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > <span data-ttu-id="b99b3-178">未指定特定 IP 位址或範圍時，設定 `StrictHostKeyChecking no` 可能會造成潛在的安全性風險。</span><span class="sxs-lookup"><span data-stu-id="b99b3-178">Configuring `StrictHostKeyChecking no` can create a potential security risk when a specific IP address or range is not specified.</span></span>
  >
  >
* <span data-ttu-id="b99b3-179">**應用程式**： 安裝任何應用程式，您需要或執行其他自訂，然後擷取 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="b99b3-179">**Applications**: Install any applications you need or perform other customizations before you capture hello image.</span></span>

### <a name="capture-hello-image"></a><span data-ttu-id="b99b3-180">擷取 hello 映像</span><span class="sxs-lookup"><span data-stu-id="b99b3-180">Capture hello image</span></span>
<span data-ttu-id="b99b3-181">toocapture hello 映像，先執行下列命令在 hello Linux VM 上的 hello。</span><span class="sxs-lookup"><span data-stu-id="b99b3-181">toocapture hello image, first run hello following command on hello Linux VM.</span></span> <span data-ttu-id="b99b3-182">此命令 deprovisions hello VM，但會維護使用者帳戶和 SSH 金鑰設定。</span><span class="sxs-lookup"><span data-stu-id="b99b3-182">This command deprovisions hello VM but maintains user accounts and SSH keys that you set up.</span></span>

```
sudo waagent -deprovision
```

<span data-ttu-id="b99b3-183">從用戶端電腦，執行下列 Azure CLI 命令 toocapture hello 映像的 hello。</span><span class="sxs-lookup"><span data-stu-id="b99b3-183">From your client computer, run hello following Azure CLI commands toocapture hello image.</span></span> <span data-ttu-id="b99b3-184">如需詳細資訊，請參閱[如何 toocapture 傳統 Linux 虛擬機器做為映像](capture-image.md)。</span><span class="sxs-lookup"><span data-stu-id="b99b3-184">For more information, see [How toocapture a classic Linux virtual machine as an image](capture-image.md).</span></span>  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

<span data-ttu-id="b99b3-185">執行這些命令之後，您可以使用擷取 hello VM 映像，並且刪除 hello VM。</span><span class="sxs-lookup"><span data-stu-id="b99b3-185">After you run these commands, hello VM image is captured for your use and hello VM is deleted.</span></span> <span data-ttu-id="b99b3-186">現在您會有您的自訂映像準備 toodeploy 叢集。</span><span class="sxs-lookup"><span data-stu-id="b99b3-186">Now you have your custom image ready toodeploy a cluster.</span></span>

### <a name="deploy-a-cluster-with-hello-image"></a><span data-ttu-id="b99b3-187">叢集與 hello 映像部署</span><span class="sxs-lookup"><span data-stu-id="b99b3-187">Deploy a cluster with hello image</span></span>
<span data-ttu-id="b99b3-188">修改下列 Bash 指令碼，以適當的值，為您的環境的 hello，並從用戶端電腦執行。</span><span class="sxs-lookup"><span data-stu-id="b99b3-188">Modify hello following Bash script with appropriate values for your environment and run it from your client computer.</span></span> <span data-ttu-id="b99b3-189">因為 Azure 會將部署 hello 傳統部署模型中的循序 hello Vm，花幾分鐘的時間，toodeploy hello 八個 A9 的 Vm，建議的指令碼中。</span><span class="sxs-lookup"><span data-stu-id="b99b3-189">Because Azure deploys hello VMs serially in hello classic deployment model, it takes a few minutes toodeploy hello eight A9 VMs suggested in this script.</span></span>

```
#!/bin/bash -x
# Script toocreate a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where hello VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All hello compute-intensive instances need toobe in hello same cloud service for Linux RDMA toowork across InfiniBand.
# Note: hello current maximum number of VMs in a cloud service is 50. If you need tooprovision more than 50 VMs in hello same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want tooturn off external ports and use only internal ports toocommunicate between compute nodes via port 22, don’t use this option. Since port numbers up too10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 toocluster18. Specify your captured image in <image-name>. Specify hello username and password you used when creating hello SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment tooprovision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a><span data-ttu-id="b99b3-190">CentOS HPC 叢集的考量</span><span class="sxs-lookup"><span data-stu-id="b99b3-190">Considerations for a CentOS HPC cluster</span></span>
<span data-ttu-id="b99b3-191">如果您想 tooset 根據其中一個 hello 而不是 SLES 12 的 Azure Marketplace 中的 hello CentOS 架構 HPC 映像的 HPC 叢集，請遵循 hello hello 前面一節中的一般步驟。</span><span class="sxs-lookup"><span data-stu-id="b99b3-191">If you want tooset up a cluster based on one of hello CentOS-based HPC images in hello Azure Marketplace instead of SLES 12 for HPC, follow hello general steps in hello preceding section.</span></span> <span data-ttu-id="b99b3-192">請注意下列差異，當您佈建並設定 hello VM hello:</span><span class="sxs-lookup"><span data-stu-id="b99b3-192">Note hello following differences when you provision and configure hello VM:</span></span>

- <span data-ttu-id="b99b3-193">已經在從 CentOS 型 HPC 映像佈建的 VM 上安裝 Intel MPI。</span><span class="sxs-lookup"><span data-stu-id="b99b3-193">Intel MPI is already installed on a VM provisioned from a CentOS-based HPC image.</span></span>
- <span data-ttu-id="b99b3-194">已加入 hello VM /etc/security/limits.conf 檔案鎖定的記憶體設定。</span><span class="sxs-lookup"><span data-stu-id="b99b3-194">Lock memory settings are already added in hello VM's /etc/security/limits.conf file.</span></span>
- <span data-ttu-id="b99b3-195">不會產生 hello 您佈建的 VM 上的 SSH 金鑰擷取。</span><span class="sxs-lookup"><span data-stu-id="b99b3-195">Do not generate SSH keys on hello VM you provision for capture.</span></span> <span data-ttu-id="b99b3-196">相反地，我們建議使用者為基礎的驗證設定，部署 hello 叢集之後。</span><span class="sxs-lookup"><span data-stu-id="b99b3-196">Instead, we recommend setting up user-based authentication after you deploy hello cluster.</span></span> <span data-ttu-id="b99b3-197">如需詳細資訊，請參閱下列章節的 hello。</span><span class="sxs-lookup"><span data-stu-id="b99b3-197">For more information, see hello following section.</span></span>  

### <a name="set-up-passwordless-ssh-trust-on-hello-cluster"></a><span data-ttu-id="b99b3-198">設定 passwordless hello 叢集上的 SSH 信任</span><span class="sxs-lookup"><span data-stu-id="b99b3-198">Set up passwordless SSH trust on hello cluster</span></span>
<span data-ttu-id="b99b3-199">在 CentOS 為基礎的 HPC 叢集上，有兩種方法來建立 hello 計算節點之間的信任： 主控件為基礎的驗證和以使用者為基礎的驗證。</span><span class="sxs-lookup"><span data-stu-id="b99b3-199">On a CentOS-based HPC cluster, there are two methods for establishing trust between hello compute nodes: host-based authentication and user-based authentication.</span></span> <span data-ttu-id="b99b3-200">主機型驗證 hello 這篇文章的範圍內，和通常在部署期間就必須透過 擴充功能指令碼來完成。</span><span class="sxs-lookup"><span data-stu-id="b99b3-200">Host-based authentication is outside of hello scope of this article and generally must be done through an extension script during deployment.</span></span> <span data-ttu-id="b99b3-201">使用者為基礎的驗證相當方便部署之後建立信任，而且需要 hello 產生和 SSH 金鑰在 hello 之間共用運算 hello 叢集中的節點。</span><span class="sxs-lookup"><span data-stu-id="b99b3-201">User-based authentication is convenient for establishing trust after deployment and requires hello generation and sharing of SSH keys among hello compute nodes in hello cluster.</span></span> <span data-ttu-id="b99b3-202">此命令通常稱為無密碼 SSH 登入，執行 MPI 工作時必須使用此命令。</span><span class="sxs-lookup"><span data-stu-id="b99b3-202">This method is commonly known as passwordless SSH login and is required when running MPI jobs.</span></span>

<span data-ttu-id="b99b3-203">Hello 社群貢獻的範例指令碼位於[GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) tooenable CentOS 為基礎的 HPC 叢集上的簡單使用者驗證。</span><span class="sxs-lookup"><span data-stu-id="b99b3-203">A sample script contributed from hello community is available on [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) tooenable easy user authentication on a CentOS-based HPC cluster.</span></span> <span data-ttu-id="b99b3-204">下載並使用下列步驟的 hello 使用此指令碼。</span><span class="sxs-lookup"><span data-stu-id="b99b3-204">Download and use this script by using hello following steps.</span></span> <span data-ttu-id="b99b3-205">您也可以修改此指令碼，或使用任何其他方法 tooestablish passwordless SSH 驗證 hello 叢集計算節點之間。</span><span class="sxs-lookup"><span data-stu-id="b99b3-205">You can also modify this script or use any other method tooestablish passwordless SSH authentication between hello cluster compute nodes.</span></span>

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

<span data-ttu-id="b99b3-206">toorun hello 指令碼，您會需要 tooknow hello 前置詞的子網路 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b99b3-206">toorun hello script, you need tooknow hello prefix for your subnet IP addresses.</span></span> <span data-ttu-id="b99b3-207">執行下列命令，其中一個 hello 叢集節點上的 hello 取得 hello 前置詞。</span><span class="sxs-lookup"><span data-stu-id="b99b3-207">Get hello prefix by running hello following command on one of hello cluster nodes.</span></span> <span data-ttu-id="b99b3-208">您的輸出看起來應該像 10.1.3.5，和 hello 前置詞是 hello 10.1.3 部分。</span><span class="sxs-lookup"><span data-stu-id="b99b3-208">Your output should look something like 10.1.3.5, and hello prefix is hello 10.1.3 portion.</span></span>

    ifconfig eth0 | grep -w inet | awk '{print $2}'

<span data-ttu-id="b99b3-209">現在執行 hello 指令碼使用三個參數： hello 一般使用者名稱 hello 計算節點，hello 一般密碼 hello 該使用者計算節點，而且 hello 子網路首碼，從傳回 hello 前一個命令。</span><span class="sxs-lookup"><span data-stu-id="b99b3-209">Now run hello script using three parameters: hello common user name on hello compute nodes, hello common password for that user on hello compute nodes, and hello subnet prefix that was returned from hello previous command.</span></span>

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

<span data-ttu-id="b99b3-210">此指令碼未 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="b99b3-210">This script does hello following:</span></span>

* <span data-ttu-id="b99b3-211">建立名為.ssh，所需之 passwordless 登入的 hello 主機節點上的目錄。</span><span class="sxs-lookup"><span data-stu-id="b99b3-211">Creates a directory on hello host node named .ssh, which is required for passwordless login.</span></span>
* <span data-ttu-id="b99b3-212">指示 passwordless 登入 tooallow 登入，從 hello 叢集中任何節點的 hello.ssh 目錄中建立組態檔。</span><span class="sxs-lookup"><span data-stu-id="b99b3-212">Creates a configuration file in hello .ssh directory that instructs passwordless login tooallow login from any node in hello cluster.</span></span>
* <span data-ttu-id="b99b3-213">建立檔案，其中包含 hello 節點名稱與節點 hello 叢集中的所有 hello 節點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b99b3-213">Creates files containing hello node names and node IP addresses for all hello nodes in hello cluster.</span></span> <span data-ttu-id="b99b3-214">這些檔案會保留供日後參考執行 hello 指令碼之後。</span><span class="sxs-lookup"><span data-stu-id="b99b3-214">These files are left after hello script is run for later reference.</span></span>
* <span data-ttu-id="b99b3-215">建立私人和公用金鑰組，每個叢集節點 （包括 hello 主機節點） 與 hello authorized_keys 檔案中建立項目。</span><span class="sxs-lookup"><span data-stu-id="b99b3-215">Creates a private and public key pair for each cluster node (including hello host node) and creates entries in hello authorized_keys file.</span></span>

> [!WARNING]
> <span data-ttu-id="b99b3-216">執行這個指令碼可能會建立潛在的安全性風險。</span><span class="sxs-lookup"><span data-stu-id="b99b3-216">Running this script can create a potential security risk.</span></span> <span data-ttu-id="b99b3-217">請確定未發佈的 hello 公開金鑰資訊 ~/.ssh。</span><span class="sxs-lookup"><span data-stu-id="b99b3-217">Ensure that hello public key information in ~/.ssh is not distributed.</span></span>
>
>

## <a name="configure-intel-mpi"></a><span data-ttu-id="b99b3-218">設定 Intel MPI</span><span class="sxs-lookup"><span data-stu-id="b99b3-218">Configure Intel MPI</span></span>
<span data-ttu-id="b99b3-219">在 Azure Linux RDMA toorun MPI 應用程式，您需要 tooconfigure 某些環境變數特定 tooIntel MPI。</span><span class="sxs-lookup"><span data-stu-id="b99b3-219">toorun MPI applications on Azure Linux RDMA, you need tooconfigure certain environment variables specific tooIntel MPI.</span></span> <span data-ttu-id="b99b3-220">以下是範例 Bash 指令碼 tooconfigure hello 變數需要 toorun 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b99b3-220">Here is a sample Bash script tooconfigure hello variables needed toorun an application.</span></span> <span data-ttu-id="b99b3-221">Hello 路徑 toompivars.sh 視需要變更設定的 Intel MPI。</span><span class="sxs-lookup"><span data-stu-id="b99b3-221">Change hello path toompivars.sh as needed for your installation of Intel MPI.</span></span>

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting hello variable tooshm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line toorun hello job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path toohello application exe> <arguments specific toohello application>

#end
```

<span data-ttu-id="b99b3-222">如下所示為 hello hello 主機檔案格式。</span><span class="sxs-lookup"><span data-stu-id="b99b3-222">hello format of hello host file is as follows.</span></span> <span data-ttu-id="b99b3-223">針對叢集中的每個節點加入一行指令碼。</span><span class="sxs-lookup"><span data-stu-id="b99b3-223">Add one line for each node in your cluster.</span></span> <span data-ttu-id="b99b3-224">指定從 hello 虛擬網路的私人 IP 位址定義更早版本，不是 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="b99b3-224">Specify private IP addresses from hello virtual network defined earlier, not DNS names.</span></span> <span data-ttu-id="b99b3-225">例如，對於兩個具有 10.32.0.1 和 10.32.0.2 的 IP 位址的主機，hello 檔案包含 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="b99b3-225">For example, for two hosts with IP addresses 10.32.0.1 and 10.32.0.2, hello file contains hello following:</span></span>

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a><span data-ttu-id="b99b3-226">在基本的雙節點叢集上執行 MPI</span><span class="sxs-lookup"><span data-stu-id="b99b3-226">Run MPI on a basic two-node cluster</span></span>
<span data-ttu-id="b99b3-227">如果您尚未這樣做，請先設定 hello 環境 Intel MPI。</span><span class="sxs-lookup"><span data-stu-id="b99b3-227">If you haven't already done so, first set up hello environment for Intel MPI.</span></span>

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a><span data-ttu-id="b99b3-228">執行 MPI 命令</span><span class="sxs-lookup"><span data-stu-id="b99b3-228">Run an MPI command</span></span>
<span data-ttu-id="b99b3-229">MPI 上執行命令 hello 計算節點 tooshow MPI 已正確安裝，而且可以進行通訊，其中至少兩個計算節點之間。</span><span class="sxs-lookup"><span data-stu-id="b99b3-229">Run an MPI command on one of hello compute nodes tooshow that MPI is installed properly and can communicate between at least two compute nodes.</span></span> <span data-ttu-id="b99b3-230">hello 下列**mpirun**命令執行 hello **hostname**命令在兩個節點上。</span><span class="sxs-lookup"><span data-stu-id="b99b3-230">hello following **mpirun** command runs hello **hostname** command on two nodes.</span></span>

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
<span data-ttu-id="b99b3-231">您的輸出應該會列出所有 hello 節點做為輸入傳遞的 hello 名稱`-hosts`。</span><span class="sxs-lookup"><span data-stu-id="b99b3-231">Your output should list hello names of all hello nodes that you passed as input for `-hosts`.</span></span> <span data-ttu-id="b99b3-232">例如， **mpirun**包含兩個節點的命令會傳回類似 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="b99b3-232">For example, an **mpirun** command with two nodes returns output like hello following:</span></span>

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a><span data-ttu-id="b99b3-233">執行 MPI 基準測試</span><span class="sxs-lookup"><span data-stu-id="b99b3-233">Run an MPI benchmark</span></span>
<span data-ttu-id="b99b3-234">hello 下列 Intel MPI 命令執行 pingpong 基準 tooverify hello 叢集設定和連線 toohello RDMA 網路。</span><span class="sxs-lookup"><span data-stu-id="b99b3-234">hello following Intel MPI command runs a pingpong benchmark tooverify hello cluster configuration and connection toohello RDMA network.</span></span>

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

<span data-ttu-id="b99b3-235">在使用叢集包含兩個節點上，您應該會看到類似 hello 下列輸出。</span><span class="sxs-lookup"><span data-stu-id="b99b3-235">On a working cluster with two nodes, you should see output like hello following.</span></span> <span data-ttu-id="b99b3-236">在 hello Azure RDMA 網路上，預期或低於 too512 位元組組成的訊息大小為 3 百萬分之一秒為單位的延遲。</span><span class="sxs-lookup"><span data-stu-id="b99b3-236">On hello Azure RDMA network, expect latency at or below 3 microseconds for message sizes up too512 bytes.</span></span>

```
#------------------------------------------------------------
#    Intel (R) MPI Benchmarks 4.0 Update 1, MPI-1 part
#------------------------------------------------------------
# Date                  : Fri Jul 17 23:16:46 2015
# Machine               : x86_64
# System                : Linux
# Release               : 3.12.39-44-default
# Version               : #5 SMP Thu Jun 25 22:45:24 UTC 2015
# MPI Version           : 3.0
# MPI Thread Environment:
# New default behavior from Version 3.2 on:
# hello number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected toobe exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through hello flag => -time

# Calling sequence was:
# /opt/intel/impi_latest/bin64/IMB-MPI1 pingpong
# Minimum message length in bytes:   0
# Maximum message length in bytes:   4194304
#
# MPI_Datatype                   :   MPI_BYTE
# MPI_Datatype for reductions    :   MPI_FLOAT
# MPI_Op                         :   MPI_SUM
#
#
# List of Benchmarks toorun:
# PingPong
#---------------------------------------------------
# Benchmarking PingPong
# #processes = 2
#---------------------------------------------------
       #bytes #repetitions      t[usec]   Mbytes/sec
            0         1000         2.23         0.00
            1         1000         2.26         0.42
            2         1000         2.26         0.85
            4         1000         2.26         1.69
            8         1000         2.26         3.38
           16         1000         2.36         6.45
           32         1000         2.57        11.89
           64         1000         2.36        25.81
          128         1000         2.64        46.19
          256         1000         2.73        89.30
          512         1000         3.09       157.99
         1024         1000         3.60       271.53
         2048         1000         4.46       437.57
         4096         1000         6.11       639.23
         8192         1000         7.49      1043.47
        16384         1000         9.76      1600.76
        32768         1000        14.98      2085.77
        65536          640        25.99      2405.08
       131072          320        50.68      2466.64
       262144          160        80.62      3101.01
       524288           80       145.86      3427.91
      1048576           40       279.06      3583.42
      2097152           20       543.37      3680.71
      4194304           10      1082.94      3693.63

# All processes entering MPI_Finalize

```



## <a name="next-steps"></a><span data-ttu-id="b99b3-237">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b99b3-237">Next steps</span></span>
* <span data-ttu-id="b99b3-238">在 Linux 叢集上部署並執行 Linux MPI 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b99b3-238">Deploy and run your Linux MPI applications on your Linux cluster.</span></span>
* <span data-ttu-id="b99b3-239">請參閱 hello [Intel MPI 程式庫文件](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/)如 Intel MPI 的指引。</span><span class="sxs-lookup"><span data-stu-id="b99b3-239">See hello [Intel MPI Library documentation](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) for guidance on Intel MPI.</span></span>
* <span data-ttu-id="b99b3-240">再試一次[快速入門範本](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos)toocreate Intel Lustre 叢集使用 CentOS 架構 HPC 映像。</span><span class="sxs-lookup"><span data-stu-id="b99b3-240">Try a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate an Intel Lustre cluster by using a CentOS-based HPC image.</span></span> <span data-ttu-id="b99b3-241">如需詳細資訊，請參閱[在 Microsoft Azure 上部署 Lustre 的 Intel 雲端版本](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/)。</span><span class="sxs-lookup"><span data-stu-id="b99b3-241">For details, see [Deploying Intel Cloud Edition for Lustre on Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).</span></span>
