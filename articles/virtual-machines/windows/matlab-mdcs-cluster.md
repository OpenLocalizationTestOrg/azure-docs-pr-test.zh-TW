---
title: "虛擬機器上的 MATLAB 叢集 | Microsoft Docs"
description: "使用 Microsoft Azure 虛擬機器建立 MATLAB Distributed Computing Server 叢集，以執行需密集計算的平行 MATLAB 工作負載。"
services: virtual-machines-windows
documentationcenter: 
author: mscurrell
manager: timlt
editor: 
ms.assetid: e9980ce9-124a-41f1-b9ec-f444c8ea5c72
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Windows
ms.workload: infrastructure-services
ms.date: 05/09/2016
ms.author: markscu
ms.openlocfilehash: b302c6b3c6acbb8552796e7fb1bfd153d23dceb3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-matlab-distributed-computing-server-clusters-on-azure-vms"></a><span data-ttu-id="69cbb-103">在 Azure VM 上建立 MATLAB Distributed Computing Server 叢集</span><span class="sxs-lookup"><span data-stu-id="69cbb-103">Create MATLAB Distributed Computing Server clusters on Azure VMs</span></span>
<span data-ttu-id="69cbb-104">使用 Microsoft Azure 虛擬機器建立一或多個 MATLAB Distributed Computing Server 叢集，以執行需密集計算的平行 MATLAB 工作負載。</span><span class="sxs-lookup"><span data-stu-id="69cbb-104">Use Microsoft Azure virtual machines to create one or more MATLAB Distributed Computing Server clusters to run your compute-intensive parallel MATLAB workloads.</span></span> <span data-ttu-id="69cbb-105">在 VM 上安裝 MATLAB Distributed Computing Server 軟體來作為基礎映像，並使用 Azure 快速入門範本或 Azure PowerShell 指令碼 (可在 [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster)上取得) 來部署和管理叢集。</span><span class="sxs-lookup"><span data-stu-id="69cbb-105">Install your MATLAB Distributed Computing Server software on a VM to use as a base image and use an Azure quickstart template or Azure PowerShell script (available on [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster)) to deploy and manage the cluster.</span></span> <span data-ttu-id="69cbb-106">在部署之後，連接到叢集以執行工作負載。</span><span class="sxs-lookup"><span data-stu-id="69cbb-106">After deployment, connect to the cluster to run your workloads.</span></span>

## <a name="about-matlab-and-matlab-distributed-computing-server"></a><span data-ttu-id="69cbb-107">關於 MATLAB 和 MATLAB Distributed Computing Server</span><span class="sxs-lookup"><span data-stu-id="69cbb-107">About MATLAB and MATLAB Distributed Computing Server</span></span>
<span data-ttu-id="69cbb-108">[MATLAB](http://www.mathworks.com/products/matlab/) 平台最適合解決工程及科學問題。</span><span class="sxs-lookup"><span data-stu-id="69cbb-108">The [MATLAB](http://www.mathworks.com/products/matlab/) platform is optimized for solving engineering and scientific problems.</span></span> <span data-ttu-id="69cbb-109">MATLAB 使用者如需要進行大規模的模擬和資料處理工作，可以使用 MathWorks 平行計算產品，利用計算叢集與計算格線服務來加快其密集計算工作負載的執行速度。</span><span class="sxs-lookup"><span data-stu-id="69cbb-109">MATLAB users with large-scale simulations and data processing tasks can use MathWorks parallel computing products to speed up their compute-intensive workloads by taking advantage of compute clusters and grid services.</span></span> <span data-ttu-id="69cbb-110">[Parallel Computing Toolbox](http://www.mathworks.com/products/parallel-computing/) 可讓 MATLAB 使用者平行處理應用程式，並利用多核心處理器、GPU 和計算叢集。</span><span class="sxs-lookup"><span data-stu-id="69cbb-110">[Parallel Computing Toolbox](http://www.mathworks.com/products/parallel-computing/) lets MATLAB users parallelize applications and take advantage of multi-core processors, GPUs, and compute clusters.</span></span> <span data-ttu-id="69cbb-111">[MATLAB Distributed Computing Server](http://www.mathworks.com/products/distriben/) 則可讓 MATLAB 使用者利用計算叢集內的許多電腦。</span><span class="sxs-lookup"><span data-stu-id="69cbb-111">[MATLAB Distributed Computing Server](http://www.mathworks.com/products/distriben/) enables MATLAB users to utilize many computers in a compute cluster.</span></span>

<span data-ttu-id="69cbb-112">藉由使用 Azure 虛擬機器，您可以建立 MATLAB Distributed Computing Server 叢集，讓其擁有所有可供提交平行工作的相同機制以作為內部部署叢集，例如互動式作業、批次作業、獨立的工作和通訊工作。</span><span class="sxs-lookup"><span data-stu-id="69cbb-112">By using Azure virtual machines, you can create MATLAB Distributed Computing Server clusters that have all the same mechanisms available to submit parallel work as on-premises clusters, such as interactive jobs, batch jobs, independent tasks, and communicating tasks.</span></span> <span data-ttu-id="69cbb-113">相較於佈建和使用傳統內部部署硬體，搭配使用 Azure 與 MATLAB 平台有許多好處︰能因應各種虛擬機器大小、可隨選建立叢集以便只針對使用的計算資源付費，以及能夠大規模測試模型。</span><span class="sxs-lookup"><span data-stu-id="69cbb-113">Using Azure in conjunction with the MATLAB platform has many benefits compared to provisioning and using traditional on-premises hardware: a range of virtual machine sizes, creation of clusters on-demand so you pay only for the compute resources you use, and the ability to test models at scale.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="69cbb-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="69cbb-114">Prerequisites</span></span>
* <span data-ttu-id="69cbb-115">**用戶端電腦** - 您將需要以 Windows 為基礎的用戶端電腦，以便在部署之後與 Azure 和 MATLAB Distributed Computing Server 叢集通訊。</span><span class="sxs-lookup"><span data-stu-id="69cbb-115">**Client computer** - You'll need a Windows-based client computer to communicate with Azure and the MATLAB Distributed Computing Server cluster after deployment.</span></span>
* <span data-ttu-id="69cbb-116">**Azure PowerShell** - 請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview) 以將其安裝在您的用戶端電腦上。</span><span class="sxs-lookup"><span data-stu-id="69cbb-116">**Azure PowerShell** - See [How to install and configure Azure PowerShell](/powershell/azure/overview) to install it on your client computer.</span></span>
* <span data-ttu-id="69cbb-117">**Azure 訂用帳戶** - 如果您沒有訂用帳戶，只需要幾分鐘就可以建立 [免費帳戶](https://azure.microsoft.com/free/) 。</span><span class="sxs-lookup"><span data-stu-id="69cbb-117">**Azure subscription** - If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span> <span data-ttu-id="69cbb-118">針對較大的叢集，請考慮隨用隨付訂用帳戶或其他購買選項。</span><span class="sxs-lookup"><span data-stu-id="69cbb-118">For larger clusters, consider a pay-as-you-go subscription or other purchase options.</span></span>
* <span data-ttu-id="69cbb-119">**核心配額** -您可能需要增加核心配額，以部署大型叢集或多個 MATLAB Distributed Computing Server 叢集。</span><span class="sxs-lookup"><span data-stu-id="69cbb-119">**Cores quota** - You might need to increase the core quota to deploy a large cluster or more than one MATLAB Distributed Computing Server cluster.</span></span> <span data-ttu-id="69cbb-120">若要增加配額，請 [開立線上客戶支援要求](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) (免費)。</span><span class="sxs-lookup"><span data-stu-id="69cbb-120">To increase a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>
* <span data-ttu-id="69cbb-121">**MATLAB、Parallel Computing Toolbox 和 MATLAB Distributed Computing Server 授權** - 指令碼假設所有授權皆使用 [MathWorks Hosted License Manager](http://www.mathworks.com/products/parallel-computing/mathworks-hosted-license-manager/) 。</span><span class="sxs-lookup"><span data-stu-id="69cbb-121">**MATLAB, Parallel Computing Toolbox, and MATLAB Distributed Computing Server licenses** - The scripts assume that the [MathWorks Hosted License Manager](http://www.mathworks.com/products/parallel-computing/mathworks-hosted-license-manager/) is used for all licenses.</span></span>  
* <span data-ttu-id="69cbb-122">**MATLAB Distributed Computing Server 軟體** - 將會安裝在作為叢集 VM 之基礎 VM 映像的 VM 上。</span><span class="sxs-lookup"><span data-stu-id="69cbb-122">**MATLAB Distributed Computing Server software** - Will be installed on a VM that will be used as the base VM image for the cluster VMs.</span></span>

## <a name="high-level-steps"></a><span data-ttu-id="69cbb-123">高階步驟</span><span class="sxs-lookup"><span data-stu-id="69cbb-123">High level steps</span></span>
<span data-ttu-id="69cbb-124">若要對 MATLAB Distributed Computing Server 叢集使用 Azure 虛擬機器，必須執行下列高階步驟。</span><span class="sxs-lookup"><span data-stu-id="69cbb-124">To use Azure virtual machines for your MATLAB Distributed Computing Server clusters, the following high-level steps are required.</span></span> <span data-ttu-id="69cbb-125">[GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster)上的快速入門範本和指令碼所隨附的文件會有詳細指示。</span><span class="sxs-lookup"><span data-stu-id="69cbb-125">Detailed instructions are in the documentation accompanying the quickstart template and scripts on [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster).</span></span>

1. <span data-ttu-id="69cbb-126">**建立基礎 VM 映像**</span><span class="sxs-lookup"><span data-stu-id="69cbb-126">**Create a base VM image**</span></span>  

   * <span data-ttu-id="69cbb-127">在此 VM 上下載並安裝 MATLAB Distributed Computing Server 軟體。</span><span class="sxs-lookup"><span data-stu-id="69cbb-127">Download and install MATLAB Distributed Computing Server software onto this VM.</span></span>

     > [!NOTE]
     > <span data-ttu-id="69cbb-128">此程序可能需要幾個小時，但您所使用的每個 MATLAB 版本只需執行此作業一次。</span><span class="sxs-lookup"><span data-stu-id="69cbb-128">This process can take a couple of hours, but you only have to do it once for each version of MATLAB you use.</span></span>   
     >
     >
2. <span data-ttu-id="69cbb-129">**建立一或多個叢集**</span><span class="sxs-lookup"><span data-stu-id="69cbb-129">**Create one or more clusters**</span></span>  

   * <span data-ttu-id="69cbb-130">使用提供的 PowerShell 指令碼或使用快速入門範本，透過基礎 VM 映像建立叢集。</span><span class="sxs-lookup"><span data-stu-id="69cbb-130">Use the supplied PowerShell script or use the quickstart template to create a cluster from the base VM image.</span></span>   
   * <span data-ttu-id="69cbb-131">使用提供的 PowerShell 指令碼管理叢集，此指令碼可讓您列出、暫停、繼續和刪除叢集。</span><span class="sxs-lookup"><span data-stu-id="69cbb-131">Manage the clusters using the supplied PowerShell script which allows you to list, pause, resume, and delete clusters.</span></span>

## <a name="cluster-configurations"></a><span data-ttu-id="69cbb-132">叢集組態</span><span class="sxs-lookup"><span data-stu-id="69cbb-132">Cluster configurations</span></span>
<span data-ttu-id="69cbb-133">目前，叢集建立指令碼和範本可讓您建立單一的 MATLAB Distributed Computing Server 拓撲。</span><span class="sxs-lookup"><span data-stu-id="69cbb-133">Currently, the cluster creation script and template enable you to create a single MATLAB Distributed Computing Server topology.</span></span> <span data-ttu-id="69cbb-134">如果您想要的話，請另外建立一或多個叢集，讓每個叢集擁有不同數量的背景工作 VM、使用不同的 VM 大小等等。</span><span class="sxs-lookup"><span data-stu-id="69cbb-134">If you want, create one or more additional clusters, with each cluster having a different number of worker VMs, using different VM sizes, and so on.</span></span>

### <a name="matlab-client-and-cluster-in-azure"></a><span data-ttu-id="69cbb-135">Azure 中的 MATLAB 用戶端和叢集</span><span class="sxs-lookup"><span data-stu-id="69cbb-135">MATLAB client and cluster in Azure</span></span>
<span data-ttu-id="69cbb-136">MATLAB 用戶端節點、MATLAB 作業排程器節點和 MATLAB Distributed Computing Server「背景工作」節點全都會設定為虛擬網路中的 Azure VM，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="69cbb-136">The MATLAB client node, MATLAB Job Scheduler node, and MATLAB Distributed Computing Server "worker" nodes are all configured as Azure VMs in a virtual network, as shown in the following figure.</span></span>


* <span data-ttu-id="69cbb-137">若要使用叢集，請透過遠端桌面連接到用戶端節點。</span><span class="sxs-lookup"><span data-stu-id="69cbb-137">To use the cluster, connect by Remote Desktop to the client node.</span></span> <span data-ttu-id="69cbb-138">用戶端節點會執行 MATLAB 用戶端。</span><span class="sxs-lookup"><span data-stu-id="69cbb-138">The client node runs the MATLAB client.</span></span>
* <span data-ttu-id="69cbb-139">用戶端節點具有可供所有背景工作角色存取的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="69cbb-139">The client node has a file share that can be accessed by all workers.</span></span>
* <span data-ttu-id="69cbb-140">所有 MATLAB 軟體的授權檢查都會使用 MathWorks Hosted License Manager。</span><span class="sxs-lookup"><span data-stu-id="69cbb-140">MathWorks Hosted License Manager is used for the license checks for all MATLAB software.</span></span>
* <span data-ttu-id="69cbb-141">在背景工作角色 VM 上，預設會為每個核心建立一個 MATLAB Distributed Computing Server 背景工作角色，但您可以指定任意數目。</span><span class="sxs-lookup"><span data-stu-id="69cbb-141">By default, one MATLAB Distributed Computing Server worker per core is created on the worker VMs, but you can specify any number.</span></span>

## <a name="use-an-azure-based-cluster"></a><span data-ttu-id="69cbb-142">使用以 Azure 為基礎的叢集</span><span class="sxs-lookup"><span data-stu-id="69cbb-142">Use an Azure-based Cluster</span></span>
<span data-ttu-id="69cbb-143">和其他類型的 MATLAB Distributed Computing Server 叢集一樣，您必須在 MATLAB 用戶端 (位於用戶端 VM 上) 中使用 Cluster Profile Manager，以建立 MATLAB 作業排程器叢集設定檔。</span><span class="sxs-lookup"><span data-stu-id="69cbb-143">As with other types of MATLAB Distributed Computing Server clusters, you need to use the Cluster Profile Manager in the MATLAB client (on the client VM) to create a MATLAB Job Scheduler cluster profile.</span></span>

![Cluster Profile Manager](./media/matlab-mdcs-cluster/cluster_profile_manager.png)

## <a name="next-steps"></a><span data-ttu-id="69cbb-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="69cbb-145">Next steps</span></span>
* <span data-ttu-id="69cbb-146">如需在 Azure 中部署和管理 MATLAB Distributed Computing Server 叢集的詳細指示，請參閱包含範本和指令碼的 [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster) 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="69cbb-146">For detailed instructions to deploy and manage MATLAB Distributed Computing Server clusters in Azure, see the [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster) repository containing the templates and scripts.</span></span>
* <span data-ttu-id="69cbb-147">如需 MATLAB 和 MATLAB Distributed Computing Server 的詳細文件，請移至 [MathWorks 網站](http://www.mathworks.com/) 。</span><span class="sxs-lookup"><span data-stu-id="69cbb-147">Go to the [MathWorks site](http://www.mathworks.com/) for detailed documentation for MATLAB and MATLAB Distributed Computing Server.</span></span>
