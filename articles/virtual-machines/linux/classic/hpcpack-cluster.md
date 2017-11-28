---
title: "aaaLinux HPC Pack 叢集中計算 Vm |Microsoft 文件"
description: "了解如何 toocreate 並使用 HPC Pack 叢集在 Azure 中的 Linux 高效能運算 (HPC) 工作負載"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 4d080fdd-5ffe-4f54-a78d-4c818f6eb3fb
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/12/2016
ms.author: danlep
ms.openlocfilehash: 9ed20d6cd69a6472a00666caf8965e9d022698a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="45b8c-103">開始在 Azure 中的 HPC Pack 叢集使用 Linux 運算節點</span><span class="sxs-lookup"><span data-stu-id="45b8c-103">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="45b8c-104">在 Azure 中設定 [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) 叢集，其中包含一個執行 Windows Server 的前端節點，以及數個執行支援之 Linux 散發套件的計算節點。</span><span class="sxs-lookup"><span data-stu-id="45b8c-104">Set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) cluster in Azure that contains a head node running Windows Server and several compute nodes running a supported Linux distribution.</span></span> <span data-ttu-id="45b8c-105">瀏覽選項 toomove 資料 hello Linux 節點與 hello Windows 叢集前端節點 hello 之間。</span><span class="sxs-lookup"><span data-stu-id="45b8c-105">Explore options toomove data among hello Linux nodes and hello Windows head node of hello cluster.</span></span> <span data-ttu-id="45b8c-106">了解如何 toosubmit Linux HPC 作業 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="45b8c-106">Learn how toosubmit Linux HPC jobs toohello cluster.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="45b8c-107">在高層級，hello 下列圖表顯示 hello HPC Pack 叢集您建立及使用。</span><span class="sxs-lookup"><span data-stu-id="45b8c-107">At a high level, hello following diagram shows hello HPC Pack cluster you create and work with.</span></span>

![具有 Linux 節點的 HPC Pack 叢集][scenario]

<span data-ttu-id="45b8c-109">針對其他選項 toorun Linux HPC 工作負載在 Azure 中，請參閱[技術資源，批次和高效能運算](../../../batch/big-compute-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="45b8c-109">For other options toorun Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/big-compute-resources.md).</span></span>

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a><span data-ttu-id="45b8c-110">部署具有 Linux 運算節點的 HPC Pack 叢集</span><span class="sxs-lookup"><span data-stu-id="45b8c-110">Deploy an HPC Pack cluster with Linux compute nodes</span></span>
<span data-ttu-id="45b8c-111">本文將說明兩個選項 toodeploy HPC Pack 叢集在 Azure 中 Linux 計算節點。</span><span class="sxs-lookup"><span data-stu-id="45b8c-111">This article shows you two options toodeploy an HPC Pack cluster in Azure with Linux compute nodes.</span></span> <span data-ttu-id="45b8c-112">這兩種方法使用 Marketplace 映像的 Windows Server 與 HPC Pack toocreate hello 前端節點。</span><span class="sxs-lookup"><span data-stu-id="45b8c-112">Both methods use a Marketplace image of Windows Server with HPC Pack toocreate hello head node.</span></span> 

* <span data-ttu-id="45b8c-113">**Azure Resource Manager 範本**-使用 hello Azure Marketplace 中的範本或快速入門中的範本 hello 社群，tooautomate 建立 hello Resource Manager 部署模型中的 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="45b8c-113">**Azure Resource Manager template** - Use a template from hello Azure Marketplace, or a quickstart template from hello community, tooautomate creation of hello cluster in hello Resource Manager deployment model.</span></span> <span data-ttu-id="45b8c-114">例如，hello [Linux 工作負載的 HPC Pack 叢集](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)hello Azure Marketplace 中的範本會建立完整的 HPC Pack 叢集基礎結構的 Linux HPC 工作負載。</span><span class="sxs-lookup"><span data-stu-id="45b8c-114">For example, hello [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in hello Azure Marketplace creates a complete HPC Pack cluster infrastructure for Linux HPC workloads.</span></span>
* <span data-ttu-id="45b8c-115">**PowerShell 指令碼**-使用 hello [Microsoft HPC Pack IaaS 部署指令碼](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)(**New-hpciaascluster.ps1**) tooautomate hello 傳統部署模型中完整的叢集部署。</span><span class="sxs-lookup"><span data-stu-id="45b8c-115">**PowerShell script** - Use hello [Microsoft HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) tooautomate a complete cluster deployment in hello classic deployment model.</span></span> <span data-ttu-id="45b8c-116">此 Azure PowerShell 指令碼使用 HPC Pack VM 映像 hello Azure Marketplace 中快速部署，並提供一組完整的組態參數 toodeploy Linux 計算節點。</span><span class="sxs-lookup"><span data-stu-id="45b8c-116">This Azure PowerShell script uses an HPC Pack VM image in hello Azure Marketplace for fast deployment and provides a comprehensive set of configuration parameters toodeploy Linux compute nodes.</span></span>

<span data-ttu-id="45b8c-117">如需有關在 Azure 中的 HPC Pack 叢集部署選項的詳細資訊，請參閱[選項 toocreate 及管理高效能運算 (HPC) 叢集，在 Azure 中使用 Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="45b8c-117">For more information about HPC Pack cluster deployment options in Azure, see [Options toocreate and manage a high-performance computing (HPC) cluster in Azure with Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="45b8c-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="45b8c-118">Prerequisites</span></span>
* <span data-ttu-id="45b8c-119">**Azure 訂用帳戶**-您可以使用任一 hello Azure Global 或 Azure China 服務中的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="45b8c-119">**Azure subscription** - You can use a subscription in either hello Azure Global or Azure China service.</span></span> <span data-ttu-id="45b8c-120">如果您沒有帳戶，只需要幾分鐘的時間就可以建立 [免費帳戶](https://azure.microsoft.com/pricing/free-trial/) 。</span><span class="sxs-lookup"><span data-stu-id="45b8c-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="45b8c-121">**核心配額**-特別是當您選擇 toodeploy 具有多核心的 VM 大小的數個叢集節點，您可能需要的核心，tooincrease hello 配額。</span><span class="sxs-lookup"><span data-stu-id="45b8c-121">**Cores quota** - You might need tooincrease hello quota of cores, especially if you choose toodeploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="45b8c-122">tooincrease 配額限制時，會開啟免費線上客戶支援要求。</span><span class="sxs-lookup"><span data-stu-id="45b8c-122">tooincrease a quota, open an online customer support request at no charge.</span></span>
* <span data-ttu-id="45b8c-123">**Linux 散發套件**-目前 HPC Pack 支援 hello 下列計算節點的 Linux 散發套件。</span><span class="sxs-lookup"><span data-stu-id="45b8c-123">**Linux distributions** - Currently HPC Pack supports hello following Linux distributions for compute nodes.</span></span> <span data-ttu-id="45b8c-124">您可以使用這些發佈的 Marketplace 版本，或提供您自己的版本。</span><span class="sxs-lookup"><span data-stu-id="45b8c-124">You can use Marketplace versions of these distributions where available, or supply your own.</span></span>
  
  * <span data-ttu-id="45b8c-125">**CentOS 型**：6.5、6.6、6.7、7.0、7.1、7.2、6.5 HPC、7.1 HPC</span><span class="sxs-lookup"><span data-stu-id="45b8c-125">**CentOS-based**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span></span>
  * <span data-ttu-id="45b8c-126">**Red Hat Enterprise Linux**：6.7、6.8、7.2</span><span class="sxs-lookup"><span data-stu-id="45b8c-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span></span>
  * <span data-ttu-id="45b8c-127">**SUSE Linux Enterprise Server**：SLES 12、SLES 12 (Premium)、SLES 12 SP1、SLES 12 SP1 (Premium)、SLES 12 for HPC、SLES 12 for HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="45b8c-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 for HPC, SLES 12 for HPC (Premium)</span></span>
  * <span data-ttu-id="45b8c-128">**Ubuntu Server**：14.04 LTS、16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="45b8c-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span></span>
    
    > [!TIP]
    > <span data-ttu-id="45b8c-129">toouse hello Azure RDMA 網路與 hello 具備 RDMA 功能的 VM 大小，其中指定從 hello Azure Marketplace 的 SUSE Linux Enterprise Server 12 HPC 或 CentOS 架構 HPC 映像。</span><span class="sxs-lookup"><span data-stu-id="45b8c-129">toouse hello Azure RDMA network with one of hello RDMA-capable VM sizes, specify a SUSE Linux Enterprise Server 12 HPC or CentOS-based HPC image from hello Azure Marketplace.</span></span> <span data-ttu-id="45b8c-130">如需詳細資訊，請參閱[高效能運算 VM 大小](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="45b8c-130">For more information, see [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

<span data-ttu-id="45b8c-131">使用 hello HPC Pack IaaS 部署指令碼的其他必要條件 toodeploy hello 叢集：</span><span class="sxs-lookup"><span data-stu-id="45b8c-131">Additional prerequisites toodeploy hello cluster by using hello HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="45b8c-132">**用戶端電腦**-您需要的 Windows 架構的用戶端電腦 toorun hello 叢集部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="45b8c-132">**Client computer** - You need a Windows-based client computer toorun hello cluster deployment script.</span></span>
* <span data-ttu-id="45b8c-133">**Azure PowerShell** - [安裝和設定 Azure PowerShell](/powershell/azure/overview) (0.8.10 版或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="45b8c-133">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="45b8c-134">**HPC Pack IaaS 部署指令碼**-下載及解壓縮 hello 最新版 hello 指令碼從 hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949)。</span><span class="sxs-lookup"><span data-stu-id="45b8c-134">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="45b8c-135">您可以執行檢查 hello hello 指令碼版本`.\New-HPCIaaSCluster.ps1 –Version`。</span><span class="sxs-lookup"><span data-stu-id="45b8c-135">You can check hello version of hello script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="45b8c-136">這篇文章根據 4.4.1 版本或更新版本的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="45b8c-136">This article is based on version 4.4.1 or later of hello script.</span></span>

### <a name="deployment-option-1-use-a-resource-manager-template"></a><span data-ttu-id="45b8c-137">部署選項 1。</span><span class="sxs-lookup"><span data-stu-id="45b8c-137">Deployment option 1.</span></span> <span data-ttu-id="45b8c-138">使用 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="45b8c-138">Use a Resource Manager template</span></span>
1. <span data-ttu-id="45b8c-139">移 toohello [Linux 工作負載的 HPC Pack 叢集](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)hello Azure Marketplace 中的範本，然後按一下**部署**。</span><span class="sxs-lookup"><span data-stu-id="45b8c-139">Go toohello [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in hello Azure Marketplace, and click **Deploy**.</span></span>
2. <span data-ttu-id="45b8c-140">在 hello Azure 入口網站，請檢閱 hello 資訊，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="45b8c-140">In hello Azure portal, review hello information and then click **Create**.</span></span>
   
    ![建立入口網站][portal]
3. <span data-ttu-id="45b8c-142">在 hello**基本概念**刀鋒視窗中，輸入 hello 叢集，也會命名 hello 前端節點 VM 的名稱。</span><span class="sxs-lookup"><span data-stu-id="45b8c-142">On hello **Basics** blade, enter a name for hello cluster, which also names hello head node VM.</span></span> <span data-ttu-id="45b8c-143">您可以選擇現有的資源群組，或可用 tooyou 的位置中建立 hello 部署群組。</span><span class="sxs-lookup"><span data-stu-id="45b8c-143">You can choose an existing resource group or create a group for hello deployment in a location that's available tooyou.</span></span> <span data-ttu-id="45b8c-144">hello 位置會影響特定 VM 大小和其他 Azure 服務的 hello 可用性 (請參閱[依地區可用的產品](https://azure.microsoft.com/regions/services/))。</span><span class="sxs-lookup"><span data-stu-id="45b8c-144">hello location affects hello availability of certain VM sizes and other Azure services (see [Products available by region](https://azure.microsoft.com/regions/services/)).</span></span>
4. <span data-ttu-id="45b8c-145">在 hello**前端節點設定**刀鋒視窗中，針對第一個部署，您通常可以接受 hello 預設設定。</span><span class="sxs-lookup"><span data-stu-id="45b8c-145">On hello **Head node settings** blade, for a first deployment, you can generally accept hello default settings.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="45b8c-146">hello**後組態指令碼 URL**這選擇性設定 toospecify 公開可用 Windows PowerShell 指令碼之後, 您想要 toorun hello 前端節點 VM 上的執行。</span><span class="sxs-lookup"><span data-stu-id="45b8c-146">hello **Post-configuration script URL** is an optional setting toospecify a publicly available Windows PowerShell script that you want toorun on hello head node VM after it is running.</span></span> 
   > 
   > 
5. <span data-ttu-id="45b8c-147">在 hello**計算節點設定**刀鋒視窗中，選取的 hello 節點、 hello 數目和大小的 hello 節點的命名模式，然後 hello Linux 發佈 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="45b8c-147">On hello **Compute node settings** blade, select a naming pattern for hello nodes, hello number and size of hello nodes, and hello Linux distribution toodeploy.</span></span>
6. <span data-ttu-id="45b8c-148">在 hello**基礎結構設定**刀鋒視窗中，輸入名稱 hello 虛擬網路和 Active Directory 網域、 網域和 VM 系統管理員認證和 hello 儲存體帳戶的命名模式。</span><span class="sxs-lookup"><span data-stu-id="45b8c-148">On hello **Infrastructure settings** blade, enter names for hello virtual network and Active Directory domain, domain and VM administrator credentials, and a naming pattern for hello storage accounts.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="45b8c-149">HPC Pack 會使用 hello Active Directory 網域 tooauthenticate 叢集使用者。</span><span class="sxs-lookup"><span data-stu-id="45b8c-149">HPC Pack uses hello Active Directory domain tooauthenticate cluster users.</span></span> 
   > 
   > 
7. <span data-ttu-id="45b8c-150">以執行 hello 驗證測試，並檢閱 hello 使用條款之後，按**購買**。</span><span class="sxs-lookup"><span data-stu-id="45b8c-150">After hello validation tests run and you review hello terms of use, click **Purchase**.</span></span>

### <a name="deployment-option-2-use-hello-iaas-deployment-script"></a><span data-ttu-id="45b8c-151">部署選項 2。</span><span class="sxs-lookup"><span data-stu-id="45b8c-151">Deployment option 2.</span></span> <span data-ttu-id="45b8c-152">使用 hello IaaS 部署指令碼</span><span class="sxs-lookup"><span data-stu-id="45b8c-152">Use hello IaaS deployment script</span></span>
<span data-ttu-id="45b8c-153">以下是使用 hello HPC Pack IaaS 部署指令碼的其他必要條件 toodeploy hello 叢集：</span><span class="sxs-lookup"><span data-stu-id="45b8c-153">Following are additional prerequisites toodeploy hello cluster by using hello HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="45b8c-154">**用戶端電腦**-您需要的 Windows 架構的用戶端電腦 toorun hello 叢集部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="45b8c-154">**Client computer** - You need a Windows-based client computer toorun hello cluster deployment script.</span></span>
* <span data-ttu-id="45b8c-155">**Azure PowerShell** - [安裝和設定 Azure PowerShell](/powershell/azure/overview) (0.8.10 版或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="45b8c-155">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="45b8c-156">**HPC Pack IaaS 部署指令碼**-下載及解壓縮 hello 最新版 hello 指令碼從 hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949)。</span><span class="sxs-lookup"><span data-stu-id="45b8c-156">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="45b8c-157">您可以執行檢查 hello hello 指令碼版本`.\New-HPCIaaSCluster.ps1 –Version`。</span><span class="sxs-lookup"><span data-stu-id="45b8c-157">You can check hello version of hello script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="45b8c-158">這篇文章根據 4.4.1 版本或更新版本的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="45b8c-158">This article is based on version 4.4.1 or later of hello script.</span></span>

<span data-ttu-id="45b8c-159">**XML 組態檔**</span><span class="sxs-lookup"><span data-stu-id="45b8c-159">**XML configuration file**</span></span>

<span data-ttu-id="45b8c-160">hello HPC Pack IaaS 部署指令碼會使用 XML 組態檔當做輸入的 toodescribe hello HPC 叢集。</span><span class="sxs-lookup"><span data-stu-id="45b8c-160">hello HPC Pack IaaS deployment script uses an XML configuration file as input toodescribe hello  HPC cluster.</span></span> <span data-ttu-id="45b8c-161">hello 下列範例組態檔指定 HPC Pack 前端節點和兩個大小 A7 CentOS 7.0 Linux 運算節點組成的小叢集。</span><span class="sxs-lookup"><span data-stu-id="45b8c-161">hello following sample configuration file specifies a small cluster consisting of an HPC Pack head node and two size A7 CentOS 7.0 Linux compute nodes.</span></span> 

<span data-ttu-id="45b8c-162">視需要針對您的環境和所需的叢集組態中，修改 hello 檔案，並將它儲存例如 HPCDemoConfig.xml 的名稱。</span><span class="sxs-lookup"><span data-stu-id="45b8c-162">Modify hello file as needed for your environment and desired cluster configuration, and save it with a name such as HPCDemoConfig.xml.</span></span> <span data-ttu-id="45b8c-163">例如，您需要 toosupply 訂用帳戶名稱和唯一的儲存體帳戶名稱和雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="45b8c-163">For example, you need toosupply your subscription name and a unique storage account name and cloud service name.</span></span> <span data-ttu-id="45b8c-164">此外，您可能想 toochoose 不同 hello 計算節點支援 Linux 映像。</span><span class="sxs-lookup"><span data-stu-id="45b8c-164">Additionally, you might want toochoose a different supported Linux image for hello compute nodes.</span></span> <span data-ttu-id="45b8c-165">Hello hello 組態檔中的項目相關的詳細資訊，請參閱 hello 指令碼資料夾中的 hello Manual.rtf 檔案和[以 hello HPC Pack IaaS 部署指令碼建立 HPC 叢集](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="45b8c-165">For more information about hello elements in hello configuration file, see hello Manual.rtf file in hello script folder and [Create an HPC cluster with hello HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>centos7rdmavnetje</VNetName>
    <SubnetName>CentOS7RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS7RDMA-HN</VMName>
    <ServiceName>centos7rdma-je</ServiceName>
  <VMSize>ExtraLarge</VMSize>
  <EnableRESTAPI />
  <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS7RDMA-LN%1%</VMNamePattern>
    <ServiceName>centos7rdma-je</ServiceName>
    <VMSize>A7</VMSize>
    <NodeCount>2</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

<span data-ttu-id="45b8c-166">**toorun hello HPC Pack IaaS 部署指令碼**</span><span class="sxs-lookup"><span data-stu-id="45b8c-166">**toorun hello HPC Pack IaaS deployment script**</span></span>

1. <span data-ttu-id="45b8c-167">系統管理員身分開啟 hello 用戶端電腦上的 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="45b8c-167">Open Windows PowerShell on hello client computer as an administrator.</span></span>
2. <span data-ttu-id="45b8c-168">變更 hello 指令碼所在的目錄 toohello 資料夾安裝 (E:\IaaSClusterScript 在此範例中)。</span><span class="sxs-lookup"><span data-stu-id="45b8c-168">Change directory toohello folder where hello script is installed (E:\IaaSClusterScript in this example).</span></span>
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. <span data-ttu-id="45b8c-169">執行下列命令 toodeploy hello HPC Pack 叢集 hello。</span><span class="sxs-lookup"><span data-stu-id="45b8c-169">Run hello following command toodeploy hello HPC Pack cluster.</span></span> <span data-ttu-id="45b8c-170">這個範例假設 hello 設定檔位於 E:\HPCDemoConfig.xml</span><span class="sxs-lookup"><span data-stu-id="45b8c-170">This example assumes that hello configuration file is located in E:\HPCDemoConfig.xml</span></span>
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    <span data-ttu-id="45b8c-171">a.</span><span class="sxs-lookup"><span data-stu-id="45b8c-171">a.</span></span> <span data-ttu-id="45b8c-172">因為 hello **AdminPassword**未指定 hello 上述命令，在中，您是使用者的提示的 tooenter hello 密碼*MyAdminName*。</span><span class="sxs-lookup"><span data-stu-id="45b8c-172">Because hello **AdminPassword** is not specified in hello preceding command, you are prompted tooenter hello password for user *MyAdminName*.</span></span>
   
    <span data-ttu-id="45b8c-173">b.</span><span class="sxs-lookup"><span data-stu-id="45b8c-173">b.</span></span> <span data-ttu-id="45b8c-174">hello 指令碼，然後啟動 toovalidate hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="45b8c-174">hello script then starts toovalidate hello configuration file.</span></span> <span data-ttu-id="45b8c-175">它可能會佔用 tooseveral 分鐘，取決於 hello 的網路連線。</span><span class="sxs-lookup"><span data-stu-id="45b8c-175">It can take up tooseveral minutes depending on hello network connection.</span></span>
   
    ![驗證][validate]
   
    <span data-ttu-id="45b8c-177">c.</span><span class="sxs-lookup"><span data-stu-id="45b8c-177">c.</span></span> <span data-ttu-id="45b8c-178">通過驗證之後，hello 指令碼會列出 hello 叢集資源 toocreate。</span><span class="sxs-lookup"><span data-stu-id="45b8c-178">After validations pass, hello script lists hello cluster resources toocreate.</span></span> <span data-ttu-id="45b8c-179">輸入*Y* toocontinue。</span><span class="sxs-lookup"><span data-stu-id="45b8c-179">Enter *Y* toocontinue.</span></span>
   
    ![資源][resources]
   
    <span data-ttu-id="45b8c-181">d.</span><span class="sxs-lookup"><span data-stu-id="45b8c-181">d.</span></span> <span data-ttu-id="45b8c-182">hello 指令碼會啟動 toodeploy hello HPC Pack 叢集，並完成 hello 組態，而不需要進一步手動步驟。</span><span class="sxs-lookup"><span data-stu-id="45b8c-182">hello script starts toodeploy hello HPC Pack cluster and completes hello configuration without further manual steps.</span></span> <span data-ttu-id="45b8c-183">hello 指令碼可以執行數分鐘。</span><span class="sxs-lookup"><span data-stu-id="45b8c-183">hello script can run for several minutes.</span></span>
   
    ![部署][deploy]
   
   > [!NOTE]
   > <span data-ttu-id="45b8c-185">在此範例中，hello 指令碼記錄檔會自動產生自 hello **-LogFile**未指定參數。</span><span class="sxs-lookup"><span data-stu-id="45b8c-185">In this example, hello script generates a log file automatically since hello **-LogFile** parameter isn't specified.</span></span> <span data-ttu-id="45b8c-186">hello 記錄不即時寫入，但會收集在 hello 驗證和 hello 部署的 hello 結尾處。</span><span class="sxs-lookup"><span data-stu-id="45b8c-186">hello logs aren't written in real time, but are collected at hello end of hello validation and hello deployment.</span></span> <span data-ttu-id="45b8c-187">如果 hello PowerShell 處理程序已停止執行 hello 指令碼時，某些記錄檔將會遺失。</span><span class="sxs-lookup"><span data-stu-id="45b8c-187">If hello PowerShell process is stopped while hello script is running, some logs are lost.</span></span>
   > 
   > 

## <a name="connect-toohello-head-node"></a><span data-ttu-id="45b8c-188">連接 toohello 前端節點</span><span class="sxs-lookup"><span data-stu-id="45b8c-188">Connect toohello head node</span></span>
<span data-ttu-id="45b8c-189">部署在 Azure 中的 hello HPC Pack 叢集之後[遠端桌面連線](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)toohello 前端節點 VM 使用 hello 部署 hello 叢集時所提供的網域認證 (例如， *hpc\\clusteradmin*)。</span><span class="sxs-lookup"><span data-stu-id="45b8c-189">After you deploy hello HPC Pack cluster in Azure, [connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello head node VM using hello domain credentials you provided when you deployed hello cluster (for example, *hpc\\clusteradmin*).</span></span> <span data-ttu-id="45b8c-190">您可以管理 hello 叢集從 hello 前端節點。</span><span class="sxs-lookup"><span data-stu-id="45b8c-190">You manage hello cluster from hello head node.</span></span>

<span data-ttu-id="45b8c-191">Hello 前端節點上，啟動 hello HPC Pack 叢集的 HPC 叢集管理員 toocheck hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="45b8c-191">On hello head node, start HPC Cluster Manager toocheck hello status of hello HPC Pack cluster.</span></span> <span data-ttu-id="45b8c-192">您可以管理和監視 Linux 計算節點 hello Windows 使用的相同方式計算節點。</span><span class="sxs-lookup"><span data-stu-id="45b8c-192">You can manage and monitor Linux compute nodes hello same way you work with Windows compute nodes.</span></span> <span data-ttu-id="45b8c-193">例如，請參閱 hello Linux 節點中所列**資源管理**(這些節點會隨著 hello 部署**LinuxNode**範本)。</span><span class="sxs-lookup"><span data-stu-id="45b8c-193">For example, you see hello Linux nodes listed in **Resource Management** (these nodes are deployed with hello **LinuxNode** template).</span></span>

![節點管理][management]

<span data-ttu-id="45b8c-195">另請參閱在 hello hello Linux 節點**熱度圖**檢視。</span><span class="sxs-lookup"><span data-stu-id="45b8c-195">You also see hello Linux nodes in hello **Heat Map** view.</span></span>

![熱圖][heatmap]

## <a name="how-toomove-data-in-a-cluster-with-linux-nodes"></a><span data-ttu-id="45b8c-197">如何在 Linux 節點叢集中的 toomove 資料</span><span class="sxs-lookup"><span data-stu-id="45b8c-197">How toomove data in a cluster with Linux nodes</span></span>
<span data-ttu-id="45b8c-198">您必須在 Linux 節點和 hello Windows 叢集前端節點 hello 之間的數個選項 toomove 資料。</span><span class="sxs-lookup"><span data-stu-id="45b8c-198">You have several choices toomove data among Linux nodes and hello Windows head node of hello cluster.</span></span> <span data-ttu-id="45b8c-199">以下是三種常見的方法，在 hello 下列各節中詳細說明：</span><span class="sxs-lookup"><span data-stu-id="45b8c-199">Here are three common methods, described in more detail in hello following sections:</span></span>

* <span data-ttu-id="45b8c-200">**Azure 檔案**-會公開受管理的 SMB 檔案共用 toostore 資料檔案，在 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="45b8c-200">**Azure File** - Exposes a managed SMB file share toostore data files in Azure storage.</span></span> <span data-ttu-id="45b8c-201">Windows 節點與 Linux 節點可以裝載為磁碟機或資料夾的 hello Azure 檔案共用相同的時間，即使它們部署在不同的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="45b8c-201">Windows nodes and Linux nodes can mount an Azure File share as a drive or folder at hello same time, even if they're deployed in different virtual networks.</span></span>
* <span data-ttu-id="45b8c-202">**前端節點 SMB 共用**-Linux 節點上裝載的 hello 前端節點的標準 Windows 共用的資料夾。</span><span class="sxs-lookup"><span data-stu-id="45b8c-202">**Head node SMB share** - Mounts a standard Windows shared folder of hello head node on Linux nodes.</span></span>
* <span data-ttu-id="45b8c-203">**前端節點 NFS 伺服器** - 為混合式 Windows 與 Linux 環境提供檔案共用解決方案。</span><span class="sxs-lookup"><span data-stu-id="45b8c-203">**Head node NFS server**  - Provides a file-sharing solution for a mixed Windows and Linux environment.</span></span>

### <a name="azure-file-storage"></a><span data-ttu-id="45b8c-204">Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="45b8c-204">Azure File storage</span></span>
<span data-ttu-id="45b8c-205">hello [Azure 檔案](https://azure.microsoft.com/services/storage/files/)服務會公開使用 hello 標準 SMB 2.1 通訊協定的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="45b8c-205">hello [Azure File](https://azure.microsoft.com/services/storage/files/) service exposes file shares using hello standard SMB 2.1 protocol.</span></span> <span data-ttu-id="45b8c-206">Azure Vm 和雲端服務可以透過掛接共用，應用程式元件之間共用檔案資料，並在內部部署應用程式可以透過 hello 檔案儲存體 API 存取檔案共用中的資料。</span><span class="sxs-lookup"><span data-stu-id="45b8c-206">Azure VMs and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share through hello File storage API.</span></span> 

<span data-ttu-id="45b8c-207">如需詳細的步驟 toocreate Azure 檔案共用，並將其裝載 hello 前端節點上，請參閱[開始使用 Azure 檔案儲存在 Windows 上](../../../storage/files/storage-how-to-use-files-windows.md)。</span><span class="sxs-lookup"><span data-stu-id="45b8c-207">For detailed steps toocreate an Azure File share and mount it on hello head node, see [Get started with Azure File storage on Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span></span> <span data-ttu-id="45b8c-208">toomount hello Azure 檔案共用 hello Linux 節點上，請參閱[如何 toouse Linux 的 Azure 檔案儲存體](../../../storage/files/storage-how-to-use-files-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="45b8c-208">toomount hello Azure File share on hello Linux nodes, see [How toouse Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="45b8c-209">tooset 持續連線，請參閱[Persisting 連線 tooMicrosoft Azure 檔案](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)。</span><span class="sxs-lookup"><span data-stu-id="45b8c-209">tooset up persisting connections, see [Persisting connections tooMicrosoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span></span>

<span data-ttu-id="45b8c-210">下列範例的 hello，在 Azure 上建立檔案共用儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="45b8c-210">In hello following example, create an Azure File share on a storage account.</span></span> <span data-ttu-id="45b8c-211">toomount hello 共用 hello 前端節點上，開啟命令提示字元，並輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="45b8c-211">toomount hello share on hello head node, open a Command Prompt and enter hello following commands:</span></span>

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

<span data-ttu-id="45b8c-212">在此範例中，allvhdsje 是您的儲存體帳戶名稱、 storageaccountkey 是儲存體帳戶金鑰，而 rdma 是 hello Azure 檔案共用名稱。</span><span class="sxs-lookup"><span data-stu-id="45b8c-212">In this example, allvhdsje is your storage account name, storageaccountkey is your storage account key, and rdma is hello Azure File share name.</span></span> <span data-ttu-id="45b8c-213">hello Azure 檔案共用做為 z: hello 前端節點上裝載。</span><span class="sxs-lookup"><span data-stu-id="45b8c-213">hello Azure File share is mounted as Z: on hello head node.</span></span>

<span data-ttu-id="45b8c-214">Linux 節點上，執行 toomount hello Azure 檔案共用**clusrun** hello 前端節點上的命令。</span><span class="sxs-lookup"><span data-stu-id="45b8c-214">toomount hello Azure File share on Linux nodes, run a **clusrun** command on hello head node.</span></span> <span data-ttu-id="45b8c-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** 是有用的 HPC Pack 工具 toocarry 多個節點上的系統管理工作。</span><span class="sxs-lookup"><span data-stu-id="45b8c-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** is a useful HPC Pack tool toocarry out administrative tasks on multiple nodes.</span></span> <span data-ttu-id="45b8c-216">(同時請參閱本文中的 [適用於 Linux 節點的 CLusrun](#Clusrun-for-Linux-nodes) )。</span><span class="sxs-lookup"><span data-stu-id="45b8c-216">(See also [Clusrun for Linux nodes](#Clusrun-for-Linux-nodes) in this article.)</span></span>

<span data-ttu-id="45b8c-217">開啟 Windows PowerShell 視窗並輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="45b8c-217">Open a Windows PowerShell window and enter hello following commands:</span></span>

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

<span data-ttu-id="45b8c-218">hello 第一個命令會建立名為 /rdma hello LinuxNodes 群組中的所有節點上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="45b8c-218">hello first command creates a folder named /rdma on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="45b8c-219">hello 第二個命令會掛接到目錄和檔案模式位元組 too777 hello /rdma 資料夾 hello Azure 檔案共用 allvhdsjw.file.core.windows.net/rdma。</span><span class="sxs-lookup"><span data-stu-id="45b8c-219">hello second command mounts hello Azure File share allvhdsjw.file.core.windows.net/rdma onto hello /rdma folder with dir and file mode bits set too777.</span></span> <span data-ttu-id="45b8c-220">在 hello 第二個命令中，allvhdsje 是您的儲存體帳戶名稱，且 storageaccountkey 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="45b8c-220">In hello second command, allvhdsje is your storage account name and storageaccountkey is your storage account key.</span></span>

> [!NOTE]
> <span data-ttu-id="45b8c-221">hello"\\`"hello 第二個命令中的符號是 PowerShell 的逸出符號。</span><span class="sxs-lookup"><span data-stu-id="45b8c-221">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="45b8c-222">「\\`，」 表示該 hello"，"（逗號字元） 是 hello 命令的一部分。</span><span class="sxs-lookup"><span data-stu-id="45b8c-222">“\\`,” means that hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

### <a name="head-node-share"></a><span data-ttu-id="45b8c-223">前端節點共用</span><span class="sxs-lookup"><span data-stu-id="45b8c-223">Head node share</span></span>
<span data-ttu-id="45b8c-224">或者，在 Linux 節點上裝載共用的資料夾的 hello 前端節點。</span><span class="sxs-lookup"><span data-stu-id="45b8c-224">Alternatively, mount a shared folder of hello head node on Linux nodes.</span></span> <span data-ttu-id="45b8c-225">共用提供最簡單方式 tooshare 檔案 hello，但在 hello，則必須部署 hello 前端節點和所有 Linux 節點相同的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="45b8c-225">A share provides hello simplest way tooshare files, but hello head node and all Linux nodes must be deployed in hello same virtual network.</span></span> <span data-ttu-id="45b8c-226">以下是 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="45b8c-226">Here are hello steps.</span></span>

1. <span data-ttu-id="45b8c-227">Hello 前端節點上建立資料夾，並共用它 tooEveryone 具有讀取/寫入權限。</span><span class="sxs-lookup"><span data-stu-id="45b8c-227">Create a folder on hello head node and share it tooEveryone with Read/Write permissions.</span></span> <span data-ttu-id="45b8c-228">例如，hello 與前端節點上的共用 D:\OpenFOAM \\CentOS7RDMA HN\OpenFOAM。</span><span class="sxs-lookup"><span data-stu-id="45b8c-228">For example, share D:\OpenFOAM on hello head node as \\CentOS7RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="45b8c-229">CentOS7RDMA HN 如下的 hello 前端節點的 hello 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="45b8c-229">Here CentOS7RDMA-HN is hello hostname of hello head node.</span></span>
   
    ![檔案共用權限][fileshareperms]
   
    ![檔案共用][filesharing]
2. <span data-ttu-id="45b8c-232">開啟 Windows PowerShell 視窗並執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="45b8c-232">Open a Windows PowerShell window and run hello following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="45b8c-233">hello 第一個命令會建立名為 /openfoam hello LinuxNodes 群組中的所有節點上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="45b8c-233">hello first command creates a folder named /openfoam on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="45b8c-234">hello 第二個命令會掛接到目錄和檔案模式位元組 too777 hello 資料夾 hello 共用資料夾 //CentOS7RDMA-HN/OpenFOAM。</span><span class="sxs-lookup"><span data-stu-id="45b8c-234">hello second command mounts hello shared folder //CentOS7RDMA-HN/OpenFOAM onto hello folder with dir and file mode bits set too777.</span></span> <span data-ttu-id="45b8c-235">hello 使用者名稱和密碼在 hello 命令應該 hello 使用者名稱和 hello 前端節點上的叢集使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="45b8c-235">hello username and password in hello command should be hello username and password of a cluster user on hello head node.</span></span> <span data-ttu-id="45b8c-236">(請參閱 [Add or remove cluster users (新增或移除叢集使用者)](https://technet.microsoft.com/library/ff919330.aspx)。)</span><span class="sxs-lookup"><span data-stu-id="45b8c-236">(See [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).)</span></span>

> [!NOTE]
> <span data-ttu-id="45b8c-237">hello"\\`"hello 第二個命令中的符號是 PowerShell 的逸出符號。</span><span class="sxs-lookup"><span data-stu-id="45b8c-237">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="45b8c-238">「\\`，」 表示該 hello"，"（逗號字元） 是 hello 命令的一部分。</span><span class="sxs-lookup"><span data-stu-id="45b8c-238">“\\`,” means that hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

### <a name="nfs-server"></a><span data-ttu-id="45b8c-239">NFS 伺服器</span><span class="sxs-lookup"><span data-stu-id="45b8c-239">NFS server</span></span>
<span data-ttu-id="45b8c-240">hello NFS 服務可讓您 tooshare 和移轉執行使用 hello SMB 通訊協定的 hello Windows Server 2012 作業系統的電腦和 linux 電腦使用 hello NFS 通訊協定之間的檔案。</span><span class="sxs-lookup"><span data-stu-id="45b8c-240">hello NFS service enables you tooshare and migrate files between computers running hello Windows Server 2012 operating system using hello SMB protocol and Linux-based computers using hello NFS protocol.</span></span> <span data-ttu-id="45b8c-241">hello NFS 伺服器和所有其他節點已部署在 hello toobe 相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="45b8c-241">hello NFS server and all other nodes have toobe deployed in hello same virtual network.</span></span> <span data-ttu-id="45b8c-242">與 SMB 共用相比，它提供更好的 Linux 節點相容性。</span><span class="sxs-lookup"><span data-stu-id="45b8c-242">It provides better compatibility with Linux nodes compared with an SMB share.</span></span> <span data-ttu-id="45b8c-243">例如，它支援檔案連結。</span><span class="sxs-lookup"><span data-stu-id="45b8c-243">For example, it supports file links.</span></span>

1. <span data-ttu-id="45b8c-244">tooinstall 並設定 NFS 伺服器，請依照下列中的 hello 步驟[伺服器的網路檔案系統的第一個共用端對端](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx)。</span><span class="sxs-lookup"><span data-stu-id="45b8c-244">tooinstall and set up an NFS server, follow hello steps in [Server for Network File System First Share End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span></span>
   
    <span data-ttu-id="45b8c-245">例如，建立名為下列屬性的 hello nfs 的 NFS 共用：</span><span class="sxs-lookup"><span data-stu-id="45b8c-245">For example, create an NFS share named nfs with hello following properties:</span></span>
   
    ![NFS 授權][nfsauth]
   
    ![NFS 共用權限][nfsshare]
   
    ![NFS NTFS 權限][nfsperm]
   
    ![NFS 管理屬性][nfsmanage]
2. <span data-ttu-id="45b8c-250">開啟 Windows PowerShell 視窗並執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="45b8c-250">Open a Windows PowerShell window and run hello following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   <span data-ttu-id="45b8c-251">hello 第一個命令會建立名為 /nfsshared hello LinuxNodes 群組中的所有節點上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="45b8c-251">hello first command creates a folder named /nfsshared on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="45b8c-252">hello 第二個命令掛接 hello NFS 共用 CentOS7RDMA HN: / nfs 到 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="45b8c-252">hello second command mounts hello NFS share CentOS7RDMA-HN:/nfs onto hello folder.</span></span> <span data-ttu-id="45b8c-253">這裡 CentOS7RDMA HN: / nfs 的 NFS 共用的 hello 遠端路徑。</span><span class="sxs-lookup"><span data-stu-id="45b8c-253">Here CentOS7RDMA-HN:/nfs is hello remote path of your NFS share.</span></span>

## <a name="how-toosubmit-jobs"></a><span data-ttu-id="45b8c-254">如何 toosubmit 工作</span><span class="sxs-lookup"><span data-stu-id="45b8c-254">How toosubmit jobs</span></span>
<span data-ttu-id="45b8c-255">有數種方式 toosubmit 作業 toohello HPC Pack 叢集：</span><span class="sxs-lookup"><span data-stu-id="45b8c-255">There are several ways toosubmit jobs toohello HPC Pack cluster:</span></span>

* <span data-ttu-id="45b8c-256">HPC 叢集管理員或 HPC 工作管理員 GUI</span><span class="sxs-lookup"><span data-stu-id="45b8c-256">HPC Cluster Manager or HPC Job Manager GUI</span></span>
* <span data-ttu-id="45b8c-257">HPC Web 入口網站</span><span class="sxs-lookup"><span data-stu-id="45b8c-257">HPC web portal</span></span>
* <span data-ttu-id="45b8c-258">REST API</span><span class="sxs-lookup"><span data-stu-id="45b8c-258">REST API</span></span>

<span data-ttu-id="45b8c-259">Azure HPC Pack GUI 工具和 hello HPC web 入口網站透過 toohello 叢集會將相同 hello 與 Windows 計算節點提交作業。</span><span class="sxs-lookup"><span data-stu-id="45b8c-259">Job submission toohello cluster in Azure via HPC Pack GUI tools and hello HPC web portal are hello same as for Windows compute nodes.</span></span> <span data-ttu-id="45b8c-260">請參閱[HPC Pack 作業管理員](https://technet.microsoft.com/library/ff919691.aspx)和[toosubmit 從內部部署用戶端電腦的工作](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="45b8c-260">See [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) and [How toosubmit jobs from an on-premises client computer](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="45b8c-261">透過 REST API hello toosubmit 作業，請參閱太[建立和提交工作使用 hello Microsoft HPC Pack 中的 REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx)。</span><span class="sxs-lookup"><span data-stu-id="45b8c-261">toosubmit jobs via hello REST API, refer too[Creating and Submitting Jobs by Using hello REST API in Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span> <span data-ttu-id="45b8c-262">toosubmit 工作，從 Linux 用戶端，也會參照 hello toohello Python 範例[HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756)。</span><span class="sxs-lookup"><span data-stu-id="45b8c-262">toosubmit jobs from a Linux client, also refer toohello Python sample in hello [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span></span>

## <a name="clusrun-for-linux-nodes"></a><span data-ttu-id="45b8c-263">適用於 Linux 節點的 CLusrun</span><span class="sxs-lookup"><span data-stu-id="45b8c-263">Clusrun for Linux nodes</span></span>
<span data-ttu-id="45b8c-264">hello HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx)工具都可以透過命令提示字元或 HPC 叢集管理員 Linux 節點上的使用的 tooexecute 命令。</span><span class="sxs-lookup"><span data-stu-id="45b8c-264">hello HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) tool can be used tooexecute commands on Linux nodes either through a Command Prompt or HPC Cluster Manager.</span></span> <span data-ttu-id="45b8c-265">以下有一些基本範例。</span><span class="sxs-lookup"><span data-stu-id="45b8c-265">Following are some basic examples.</span></span>

* <span data-ttu-id="45b8c-266">Hello 叢集中所有節點上顯示目前的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="45b8c-266">Show current user names on all nodes in hello cluster.</span></span>
  
    ```command
    clusrun whoami
    ```
* <span data-ttu-id="45b8c-267">安裝 hello **gdb**偵錯工具與**yum** hello linuxnodes 群組，並在 10 分鐘後重新啟動 hello 節點中的所有節點上。</span><span class="sxs-lookup"><span data-stu-id="45b8c-267">Install hello **gdb** debugger tool with **yum** on all nodes in hello linuxnodes group and then restart hello nodes after 10 minutes.</span></span>
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* <span data-ttu-id="45b8c-268">建立顯示 hello 叢集中的每個數字 1 到 10 的每個 Linux 節點上一秒的殼層指令碼執行，然後立即顯示輸出來源 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="45b8c-268">Create a shell script displaying each number 1 through 10 for one second on each Linux node in hello cluster, run it, and show output from hello nodes immediately.</span></span>
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> <span data-ttu-id="45b8c-269">您可能需要 toouse 某些逸出字元**clusrun**命令。</span><span class="sxs-lookup"><span data-stu-id="45b8c-269">You might need toouse certain escape characters in **clusrun** commands.</span></span> <span data-ttu-id="45b8c-270">此範例所示，使用 ^ 在命令提示字元 tooescape hello">"符號。</span><span class="sxs-lookup"><span data-stu-id="45b8c-270">As shown in this example, use ^ in a Command Prompt tooescape hello ">" symbol.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="45b8c-271">後續步驟</span><span class="sxs-lookup"><span data-stu-id="45b8c-271">Next steps</span></span>
* <span data-ttu-id="45b8c-272">請嘗試向上擴充 hello 叢集 tooa 較大節點數目，或在 hello 叢集上執行 Linux 的工作負載。</span><span class="sxs-lookup"><span data-stu-id="45b8c-272">Try scaling up hello cluster tooa larger number of nodes, or try running a Linux workload on hello cluster.</span></span> <span data-ttu-id="45b8c-273">如需範例，請參閱 [在 Azure 中的 Linux 計算節點以 Microsoft HPC Pack 執行 NAMD](hpcpack-cluster-namd.md)。</span><span class="sxs-lookup"><span data-stu-id="45b8c-273">For an example, see [Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure](hpcpack-cluster-namd.md).</span></span>
* <span data-ttu-id="45b8c-274">再試一次與叢集[具備 RDMA 功能，需要大量計算 Vm](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI 工作負載。</span><span class="sxs-lookup"><span data-stu-id="45b8c-274">Try a cluster with [RDMA-capable, compute-intensive VMs](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI workloads.</span></span> <span data-ttu-id="45b8c-275">如需範例，請參閱 [在 Azure 中的 Linux RDMA 叢集以 Microsoft HPC Pack 執行 OpenFOAM](hpcpack-cluster-openfoam.md)。</span><span class="sxs-lookup"><span data-stu-id="45b8c-275">For an example, see [Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure](hpcpack-cluster-openfoam.md).</span></span>
* <span data-ttu-id="45b8c-276">如果您有興趣使用 Linux 在內部部署 HPC Pack 叢集中的節點，請參閱 hello [TechNet 指引](https://technet.microsoft.com/library/mt595803.aspx)。</span><span class="sxs-lookup"><span data-stu-id="45b8c-276">If you are interested in working with Linux nodes in an on-premises HPC Pack cluster, see hello [TechNet guidance](https://technet.microsoft.com/library/mt595803.aspx).</span></span>

<!--Image references-->
[scenario]:media/hpcpack-cluster/scenario.png
[portal]:media/hpcpack-cluster/portal.png
[validate]:media/hpcpack-cluster/validate.png
[resources]:media/hpcpack-cluster/resources.png
[deploy]:media/hpcpack-cluster/deploy.png
[management]:media/hpcpack-cluster/management.png
[heatmap]:media/hpcpack-cluster/heatmap.png
[fileshareperms]:media/hpcpack-cluster/fileshare1.png
[filesharing]:media/hpcpack-cluster/fileshare2.png
[nfsauth]:media/hpcpack-cluster/nfsauth.png
[nfsshare]:media/hpcpack-cluster/nfsshare.png
[nfsperm]:media/hpcpack-cluster/nfsperm.png
[nfsmanage]:media/hpcpack-cluster/nfsmanage.png
