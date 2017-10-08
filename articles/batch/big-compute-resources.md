---
title: "在 hello Azure 雲端中的批次和 HPC aaaResources |Microsoft 文件"
description: "列出您執行大規模的平行、 批次和高效能運算 (HPC) 工作負載在 Azure 中的技術資源 toohelp。"
services: batch, cloud-services, virtual-machines
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 6f8be911-c841-41ae-88d3-3bcfc029eb7f
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 03/17/2017
ms.author: danlep
ms.openlocfilehash: ab8ba24678bd7ec090306b501d29ca63c4fb83ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="big-compute-in-azure-technical-resources-for-batch-and-high-performance-computing"></a><span data-ttu-id="2f987-103">Azure 中的大量運算：批次和高效能運算的技術資源</span><span class="sxs-lookup"><span data-stu-id="2f987-103">Big Compute in Azure: Technical resources for batch and high-performance computing</span></span>
<span data-ttu-id="2f987-104">這是您在 Azure 中執行大規模的平行、 批次和高效能運算 (HPC) 工作負載指南 tootechnical 資源 toohelp。</span><span class="sxs-lookup"><span data-stu-id="2f987-104">This is a guide tootechnical resources toohelp you run your large-scale parallel, batch, and high-performance computing (HPC) workloads in Azure.</span></span> <span data-ttu-id="2f987-105">擴充您現有的批次或 HPC 工作負載 toohello Azure 的雲端，或建立新 Big Compute 解決方案使用的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="2f987-105">Extend your existing batch or HPC workloads toohello Azure cloud, or build new Big Compute solutions using a range of Azure services.</span></span>

## <a name="solutions-options"></a><span data-ttu-id="2f987-106">方案選項</span><span class="sxs-lookup"><span data-stu-id="2f987-106">Solutions options</span></span>
<span data-ttu-id="2f987-107">了解在 Azure 中 Big Compute 的選項，然後選擇 hello 正確的方法，針對您的工作負載和商務需求。</span><span class="sxs-lookup"><span data-stu-id="2f987-107">Learn about Big Compute options in Azure, and choose hello right approach for your workload and business need.</span></span>

* [<span data-ttu-id="2f987-108">批次和 HPC 解決方案</span><span class="sxs-lookup"><span data-stu-id="2f987-108">Batch and HPC solutions</span></span>](batch-hpc-solutions.md)
* [<span data-ttu-id="2f987-109">影片： 使用 Azure 和 HPC hello 雲端中的 Big Compute</span><span class="sxs-lookup"><span data-stu-id="2f987-109">Video: Big Compute in hello cloud with Azure and HPC</span></span>](https://azure.microsoft.com/documentation/videos/teched-europe-2014-big-compute-in-the-cloud-with-high-performance-computing-on-azure/)

## <a name="azure-batch"></a><span data-ttu-id="2f987-110">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="2f987-110">Azure Batch</span></span>
<span data-ttu-id="2f987-111">[批次](https://azure.microsoft.com/services/batch/)是平台服務，可讓您輕鬆 toocloud 啟用您的 Linux 和 Windows 應用程式和執行的工作，而不設定和管理叢集和作業的排程器。</span><span class="sxs-lookup"><span data-stu-id="2f987-111">[Batch](https://azure.microsoft.com/services/batch/) is a platform service that makes it easy toocloud-enable your Linux and Windows applications and run jobs without setting up and managing a cluster and job scheduler.</span></span> <span data-ttu-id="2f987-112">使用 Azure 批次中的 hello SDK toointegrate 用戶端應用程式，透過不同的語言，階段資料 tooAzure，並建立工作執行管線檔案。</span><span class="sxs-lookup"><span data-stu-id="2f987-112">Use hello SDK toointegrate client applications with Azure Batch through various languages, stage data tooAzure, and build job execution pipelines.</span></span>

* [<span data-ttu-id="2f987-113">Documentation</span><span class="sxs-lookup"><span data-stu-id="2f987-113">Documentation</span></span>](https://azure.microsoft.com/documentation/services/batch/)
* <span data-ttu-id="2f987-114">[.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx)、[Python](http://azure-sdk-for-python.readthedocs.io/latest/)、[Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/)、[Java](http://azure.github.io/azure-sdk-for-java/) 和 [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API 參考</span><span class="sxs-lookup"><span data-stu-id="2f987-114">[.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/), and [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API reference</span></span>
* <span data-ttu-id="2f987-115">[Batch 管理 .NET 程式庫](https://msdn.microsoft.com/library/mt463120.aspx) 參考</span><span class="sxs-lookup"><span data-stu-id="2f987-115">[Batch management .NET library](https://msdn.microsoft.com/library/mt463120.aspx) reference</span></span>
* <span data-ttu-id="2f987-116">教學課程：開始使用[適用於 .NET 的 Azure Batch 程式庫](batch-dotnet-get-started.md)和 [Batch Python 用戶端](batch-python-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="2f987-116">Tutorials: Get started with [Azure Batch library for .NET](batch-dotnet-get-started.md) and [Batch Python client](batch-python-tutorial.md)</span></span>
* [<span data-ttu-id="2f987-117">批次論壇</span><span class="sxs-lookup"><span data-stu-id="2f987-117">Batch forum</span></span>](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch)
* [<span data-ttu-id="2f987-118">批次影片</span><span class="sxs-lookup"><span data-stu-id="2f987-118">Batch videos</span></span>](https://azure.microsoft.com/documentation/videos/index/?services=batch)

## <a name="hpc-cluster-solutions"></a><span data-ttu-id="2f987-119">HPC 叢集解決方案</span><span class="sxs-lookup"><span data-stu-id="2f987-119">HPC cluster solutions</span></span>
<span data-ttu-id="2f987-120">部署或擴充您現有 Windows 或 Linux HPC 叢集 tooAzure toorun 您大量計算的工作負載。</span><span class="sxs-lookup"><span data-stu-id="2f987-120">Deploy or extend your existing Windows or Linux HPC cluster tooAzure toorun your compute intensive workloads.</span></span>  

### <a name="microsoft-hpc-pack"></a><span data-ttu-id="2f987-121">Microsoft HPC Pack</span><span class="sxs-lookup"><span data-stu-id="2f987-121">Microsoft HPC Pack</span></span>
<span data-ttu-id="2f987-122">HPC Pack 是建置在 Microsoft Azure 和 Windows Server 技術上的 Microsoft 免費 HPC 解決方案，可執行 Windows 和 Linux HPC 工作負載。</span><span class="sxs-lookup"><span data-stu-id="2f987-122">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies, capable of running Windows and Linux HPC workloads.</span></span>  

* [<span data-ttu-id="2f987-123">下載 HPC Pack 2016</span><span class="sxs-lookup"><span data-stu-id="2f987-123">Download HPC Pack 2016</span></span>](https://www.microsoft.com/download/details.aspx?id=54507)
* [<span data-ttu-id="2f987-124">下載 HPC Pack 2012 R2 Update 3</span><span class="sxs-lookup"><span data-stu-id="2f987-124">Download HPC Pack 2012 R2 Update 3</span></span>](https://www.microsoft.com/download/details.aspx?id=49922)
* [<span data-ttu-id="2f987-125">Documentation</span><span class="sxs-lookup"><span data-stu-id="2f987-125">Documentation</span></span>](https://technet.microsoft.com/library/jj899572.aspx)
* <span data-ttu-id="2f987-126">Azure 中的 HPC Pack 叢集選項：[Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 和 [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="2f987-126">HPC Pack cluster options in Azure: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span> 
* [<span data-ttu-id="2f987-127">TooAzure 背景工作執行個體使用 HPC Pack 高載</span><span class="sxs-lookup"><span data-stu-id="2f987-127">Burst tooAzure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="2f987-128">TooAzure 批次使用 HPC Pack 高載</span><span class="sxs-lookup"><span data-stu-id="2f987-128">Burst tooAzure  Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)
* [<span data-ttu-id="2f987-129">Windows HPC 論壇</span><span class="sxs-lookup"><span data-stu-id="2f987-129">Windows HPC forums</span></span>](https://social.microsoft.com/Forums/home?category=windowshpc)

### <a name="linux-and-oss-cluster-solutions"></a><span data-ttu-id="2f987-130">Linux 與 OSS 叢集解決方案</span><span class="sxs-lookup"><span data-stu-id="2f987-130">Linux and OSS cluster solutions</span></span>
<span data-ttu-id="2f987-131">使用這些 Linux HPC 叢集的 Azure 範本 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="2f987-131">Use these Azure templates toodeploy Linux HPC clusters.</span></span>

* <span data-ttu-id="2f987-132">[加速 SLURM 叢集](https://azure.microsoft.com/documentation/templates/slurm/)和[部落格文章](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="2f987-132">[Spin up a SLURM cluster](https://azure.microsoft.com/documentation/templates/slurm/) and [blog post](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span></span>
* [<span data-ttu-id="2f987-133">加速扭力叢集</span><span class="sxs-lookup"><span data-stu-id="2f987-133">Spin up a Torque cluster</span></span>](https://azure.microsoft.com/documentation/templates/torque-cluster/)
* [<span data-ttu-id="2f987-134">使用 PBS Professional 計算格線範本 (英文)</span><span class="sxs-lookup"><span data-stu-id="2f987-134">Compute grid templates with PBS Professional</span></span>](https://github.com/xpillons/azure-hpc/tree/master/Compute-Grid-Infra)

## <a name="hpc-storage"></a><span data-ttu-id="2f987-135">HPC 儲存體</span><span class="sxs-lookup"><span data-stu-id="2f987-135">HPC storage</span></span>
* [<span data-ttu-id="2f987-136">Azure 上 HPC 儲存體的平行檔案系統 (英文)</span><span class="sxs-lookup"><span data-stu-id="2f987-136">Parallel file systems for HPC storage on Azure</span></span>](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
* [<span data-ttu-id="2f987-137">Intel Cloud Edition for Lustre Software - Eval</span><span class="sxs-lookup"><span data-stu-id="2f987-137">Intel Cloud Edition for Lustre Software - Eval</span></span>](https://azure.microsoft.com/marketplace/partners/intel/lustre-cloud-edition-evaleval-lustre-2-7/)
* [<span data-ttu-id="2f987-138">CentOS 7.2 範本上的 BeeGFS (英文)</span><span class="sxs-lookup"><span data-stu-id="2f987-138">BeeGFS on CentOS 7.2 template</span></span>](https://github.com/smith1511/hpc/tree/master/beegfs-shared-on-centos7.2)




## <a name="microsoft-mpi"></a><span data-ttu-id="2f987-139">Microsoft MPI</span><span class="sxs-lookup"><span data-stu-id="2f987-139">Microsoft MPI</span></span>
<span data-ttu-id="2f987-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) 是 Microsoft 實作的 hello 標準開發和 hello Windows 平台上執行平行應用程式訊息傳遞介面。</span><span class="sxs-lookup"><span data-stu-id="2f987-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) is a Microsoft implementation of hello Message Passing Interface standard for developing and running parallel applications on hello Windows platform.</span></span>

* [<span data-ttu-id="2f987-141">下載 MS-MPI</span><span class="sxs-lookup"><span data-stu-id="2f987-141">Download MS-MPI</span></span>](http://go.microsoft.com/FWLink/p/?LinkID=389556)
* [<span data-ttu-id="2f987-142">MS-MPI 參考資料</span><span class="sxs-lookup"><span data-stu-id="2f987-142">MS-MPI reference</span></span>](https://msdn.microsoft.com/library/dn473458.aspx)
* [<span data-ttu-id="2f987-143">MPI 論壇</span><span class="sxs-lookup"><span data-stu-id="2f987-143">MPI forum</span></span>](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## <a name="compute-intensive-instances"></a><span data-ttu-id="2f987-144">計算密集型執行個體</span><span class="sxs-lookup"><span data-stu-id="2f987-144">Compute-intensive instances</span></span>
<span data-ttu-id="2f987-145">Azure 提供[範圍的 VM 大小](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)，包括[需要大量計算 H 數列](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)能夠連線 tooa 後端 RDMA 網路，toorun Linux 和 Windows HPC 工作負載的執行個體。</span><span class="sxs-lookup"><span data-stu-id="2f987-145">Azure offers a [range of VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), including [compute-intensive H-series](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) instances capable of connecting tooa back-end RDMA network, toorun your Linux and Windows HPC workloads.</span></span> 

* [<span data-ttu-id="2f987-146">設定 Linux RDMA 叢集 toorun MPI 應用程式</span><span class="sxs-lookup"><span data-stu-id="2f987-146">Set up a Linux RDMA cluster toorun MPI applications</span></span>](../virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="2f987-147">設定 Windows RDMA 叢集使用 Microsoft HPC Pack toorun MPI 應用程式</span><span class="sxs-lookup"><span data-stu-id="2f987-147">Set up a Windows RDMA cluster with Microsoft HPC Pack toorun MPI applications</span></span>](../virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

<span data-ttu-id="2f987-148">針對 GPU 密集的工作負載，請參閱 [NC 和 NV 大小 (英文)](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/)。</span><span class="sxs-lookup"><span data-stu-id="2f987-148">For GPU-intensive workloads, check out [NC and NV sizes](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).</span></span>

## <a name="samples-and-demos"></a><span data-ttu-id="2f987-149">範例和示範</span><span class="sxs-lookup"><span data-stu-id="2f987-149">Samples and demos</span></span>
* [<span data-ttu-id="2f987-150">Azure Batch C# 和 Python 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="2f987-150">Azure Batch C# and Python code samples</span></span>](https://github.com/Azure/azure-batch-samples)
* <span data-ttu-id="2f987-151">[批次造船廠](https://azure.github.io/batch-shipyard/)工具組，以便於部署的批次樣式 Dockerized 工作負載 tooAzure 批次</span><span class="sxs-lookup"><span data-stu-id="2f987-151">[Batch Shipyard](https://azure.github.io/batch-shipyard/) toolkit for easy deployment of batch-style Dockerized workloads tooAzure Batch</span></span>
* <span data-ttu-id="2f987-152">[doAzureParallel (英文)](http://www.github.com/Azure/doAzureParallel) R 套件 (以 Azure Batch 為基礎而建置)</span><span class="sxs-lookup"><span data-stu-id="2f987-152">[doAzureParallel](http://www.github.com/Azure/doAzureParallel) R package, built on top of Azure Batch</span></span>
* [<span data-ttu-id="2f987-153">測試磁碟機 SUSE Linux Enterprise Server for HPC</span><span class="sxs-lookup"><span data-stu-id="2f987-153">Test drive SUSE Linux Enterprise Server for HPC</span></span>](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)

## <a name="related-azure-services"></a><span data-ttu-id="2f987-154">相關的 Azure 服務</span><span class="sxs-lookup"><span data-stu-id="2f987-154">Related Azure services</span></span>
* [<span data-ttu-id="2f987-155">Data Factory</span><span class="sxs-lookup"><span data-stu-id="2f987-155">Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)
* [<span data-ttu-id="2f987-156">機器學習服務</span><span class="sxs-lookup"><span data-stu-id="2f987-156">Machine Learning</span></span>](https://azure.microsoft.com/documentation/services/machine-learning/)
* [<span data-ttu-id="2f987-157">HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f987-157">HDInsight</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="2f987-158">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2f987-158">Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="2f987-159">虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="2f987-159">Virtual Machine Scale Sets</span></span>](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)
* [<span data-ttu-id="2f987-160">雲端服務</span><span class="sxs-lookup"><span data-stu-id="2f987-160">Cloud Services</span></span>](https://azure.microsoft.com/documentation/services/cloud-services/)
* [<span data-ttu-id="2f987-161">App Service</span><span class="sxs-lookup"><span data-stu-id="2f987-161">App Service</span></span>](https://azure.microsoft.com/documentation/services/app-service/)
* [<span data-ttu-id="2f987-162">媒體服務</span><span class="sxs-lookup"><span data-stu-id="2f987-162">Media Services</span></span>](https://azure.microsoft.com/documentation/services/media-services/)
* [<span data-ttu-id="2f987-163">函式</span><span class="sxs-lookup"><span data-stu-id="2f987-163">Functions</span></span>](https://azure.microsoft.com/documentation/services/functions/)

## <a name="architecture-blueprints"></a><span data-ttu-id="2f987-164">架構藍圖</span><span class="sxs-lookup"><span data-stu-id="2f987-164">Architecture blueprints</span></span>
* <span data-ttu-id="2f987-165">[用 Azure Batch 和 Azure Data Factory 的 HPC 及資料協調](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) 和[文章](../data-factory/data-factory-data-processing-using-batch.md)</span><span class="sxs-lookup"><span data-stu-id="2f987-165">[HPC and data orchestration using Azure Batch and Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) and [article](../data-factory/data-factory-data-processing-using-batch.md)</span></span>

## <a name="industry-solutions"></a><span data-ttu-id="2f987-166">產業方案</span><span class="sxs-lookup"><span data-stu-id="2f987-166">Industry solutions</span></span>
* [<span data-ttu-id="2f987-167">銀行與資本市場</span><span class="sxs-lookup"><span data-stu-id="2f987-167">Banking and capital markets</span></span>](https://finance.azure.com/)
* [<span data-ttu-id="2f987-168">工程模擬</span><span class="sxs-lookup"><span data-stu-id="2f987-168">Engineering simulations</span></span>](https://simulation.azure.com/) 

## <a name="customer-stories"></a><span data-ttu-id="2f987-169">客戶案例</span><span class="sxs-lookup"><span data-stu-id="2f987-169">Customer stories</span></span>
* [<span data-ttu-id="2f987-170">ANEO</span><span class="sxs-lookup"><span data-stu-id="2f987-170">ANEO</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=4168) 
* [<span data-ttu-id="2f987-171">d3View</span><span class="sxs-lookup"><span data-stu-id="2f987-171">d3View</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)
* [<span data-ttu-id="2f987-172">Ludwig Institute of Cancer Research</span><span class="sxs-lookup"><span data-stu-id="2f987-172">Ludwig Institute of Cancer Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5830)
* [<span data-ttu-id="2f987-173">Microsoft Research</span><span class="sxs-lookup"><span data-stu-id="2f987-173">Microsoft Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=15634)
* [<span data-ttu-id="2f987-174">明德精算顧問有限公司</span><span class="sxs-lookup"><span data-stu-id="2f987-174">Milliman</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=14967)
* [<span data-ttu-id="2f987-175">Mitsubishi UFJ Securities International</span><span class="sxs-lookup"><span data-stu-id="2f987-175">Mitsubishi UFJ Securities International</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=26266)
* [<span data-ttu-id="2f987-176">Schlumberger</span><span class="sxs-lookup"><span data-stu-id="2f987-176">Schlumberger</span></span>](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [<span data-ttu-id="2f987-177">Towers Watson</span><span class="sxs-lookup"><span data-stu-id="2f987-177">Towers Watson</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)
* [<span data-ttu-id="2f987-178">UberCloud</span><span class="sxs-lookup"><span data-stu-id="2f987-178">UberCloud</span></span>](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

## <a name="next-steps"></a><span data-ttu-id="2f987-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2f987-179">Next steps</span></span>
* <span data-ttu-id="2f987-180">最新的 hello 公告，請參閱 hello [Microsoft HPC 和批次小組部落格](http://blogs.technet.com/b/windowshpc/)和 hello [Azure 部落格](https://azure.microsoft.com/blog/tag/hpc/)。</span><span class="sxs-lookup"><span data-stu-id="2f987-180">For hello latest announcements, see hello [Microsoft HPC and Batch team blog](http://blogs.technet.com/b/windowshpc/) and hello [Azure blog](https://azure.microsoft.com/blog/tag/hpc/).</span></span>
* <span data-ttu-id="2f987-181">另請參閱[批次中最新消息](https://azure.microsoft.com/updates/?service=batch)或訂閱 toohello [RSS 摘要](https://azure.microsoft.com/updates/feed/?service=batch)。</span><span class="sxs-lookup"><span data-stu-id="2f987-181">Also see [what's new in Batch](https://azure.microsoft.com/updates/?service=batch) or subscribe toohello [RSS feed](https://azure.microsoft.com/updates/feed/?service=batch).</span></span>

