---
title: "Azure 雲端中的 Batch 和 HPC 資源 | Microsoft Docs"
description: "列出技術資源協助您在 Azure 中執行大規模平行、批次和高效能運算 (HPC) 工作負載。"
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
ms.openlocfilehash: 18be9f503b57117a7e8f5f0a4e9c93614cc7755b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="big-compute-in-azure-technical-resources-for-batch-and-high-performance-computing"></a><span data-ttu-id="b6287-103">Azure 中的大量運算：批次和高效能運算的技術資源</span><span class="sxs-lookup"><span data-stu-id="b6287-103">Big Compute in Azure: Technical resources for batch and high-performance computing</span></span>
<span data-ttu-id="b6287-104">本文章是技術資源指南，旨在協助您於 Azure 中執行大規模平行、批次和高效能運算 (HPC) 工作負載。</span><span class="sxs-lookup"><span data-stu-id="b6287-104">This is a guide to technical resources to help you run your large-scale parallel, batch, and high-performance computing (HPC) workloads in Azure.</span></span> <span data-ttu-id="b6287-105">使用各種 Azure 服務擴充您現有的批次或 HPC 工作負載至 Azure 雲端，或建置新的大量計算解決方案。</span><span class="sxs-lookup"><span data-stu-id="b6287-105">Extend your existing batch or HPC workloads to the Azure cloud, or build new Big Compute solutions using a range of Azure services.</span></span>

## <a name="solutions-options"></a><span data-ttu-id="b6287-106">方案選項</span><span class="sxs-lookup"><span data-stu-id="b6287-106">Solutions options</span></span>
<span data-ttu-id="b6287-107">了解在 Azure 中的大量計算選項，並為您的工作負載和商務需求選擇正確的方法。</span><span class="sxs-lookup"><span data-stu-id="b6287-107">Learn about Big Compute options in Azure, and choose the right approach for your workload and business need.</span></span>

* [<span data-ttu-id="b6287-108">批次和 HPC 解決方案</span><span class="sxs-lookup"><span data-stu-id="b6287-108">Batch and HPC solutions</span></span>](batch-hpc-solutions.md)
* [<span data-ttu-id="b6287-109">影片：Azure 和 HPC 在雲端的大量運算</span><span class="sxs-lookup"><span data-stu-id="b6287-109">Video: Big Compute in the cloud with Azure and HPC</span></span>](https://azure.microsoft.com/documentation/videos/teched-europe-2014-big-compute-in-the-cloud-with-high-performance-computing-on-azure/)

## <a name="azure-batch"></a><span data-ttu-id="b6287-110">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="b6287-110">Azure Batch</span></span>
<span data-ttu-id="b6287-111">[Batch](https://azure.microsoft.com/services/batch/) 是一種平台服務，可以輕鬆地從雲端啟用 Linux 和 Windows 應用程式，不必設定和管理叢集及工作排程器即可執行工作。</span><span class="sxs-lookup"><span data-stu-id="b6287-111">[Batch](https://azure.microsoft.com/services/batch/) is a platform service that makes it easy to cloud-enable your Linux and Windows applications and run jobs without setting up and managing a cluster and job scheduler.</span></span> <span data-ttu-id="b6287-112">使用 SDK 透過各種不同語言、接移資料至 Azure和建立工作執行管線，將用戶端應用程式與 Azure 批次整合。</span><span class="sxs-lookup"><span data-stu-id="b6287-112">Use the SDK to integrate client applications with Azure Batch through various languages, stage data to Azure, and build job execution pipelines.</span></span>

* [<span data-ttu-id="b6287-113">文件</span><span class="sxs-lookup"><span data-stu-id="b6287-113">Documentation</span></span>](https://azure.microsoft.com/documentation/services/batch/)
* <span data-ttu-id="b6287-114">[.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx)、[Python](http://azure-sdk-for-python.readthedocs.io/latest/)、[Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/)、[Java](http://azure.github.io/azure-sdk-for-java/) 和 [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API 參考</span><span class="sxs-lookup"><span data-stu-id="b6287-114">[.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/), and [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API reference</span></span>
* <span data-ttu-id="b6287-115">[Batch 管理 .NET 程式庫](https://msdn.microsoft.com/library/mt463120.aspx) 參考</span><span class="sxs-lookup"><span data-stu-id="b6287-115">[Batch management .NET library](https://msdn.microsoft.com/library/mt463120.aspx) reference</span></span>
* <span data-ttu-id="b6287-116">教學課程：開始使用[適用於 .NET 的 Azure Batch 程式庫](batch-dotnet-get-started.md)和 [Batch Python 用戶端](batch-python-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="b6287-116">Tutorials: Get started with [Azure Batch library for .NET](batch-dotnet-get-started.md) and [Batch Python client](batch-python-tutorial.md)</span></span>
* [<span data-ttu-id="b6287-117">批次論壇</span><span class="sxs-lookup"><span data-stu-id="b6287-117">Batch forum</span></span>](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch)
* [<span data-ttu-id="b6287-118">批次影片</span><span class="sxs-lookup"><span data-stu-id="b6287-118">Batch videos</span></span>](https://azure.microsoft.com/documentation/videos/index/?services=batch)

## <a name="hpc-cluster-solutions"></a><span data-ttu-id="b6287-119">HPC 叢集解決方案</span><span class="sxs-lookup"><span data-stu-id="b6287-119">HPC cluster solutions</span></span>
<span data-ttu-id="b6287-120">部署或擴充您現有的 Windows 或 Linux HPC 叢集至 Azure，以執行您的計算密集工作負載。</span><span class="sxs-lookup"><span data-stu-id="b6287-120">Deploy or extend your existing Windows or Linux HPC cluster to Azure to run your compute intensive workloads.</span></span>  

### <a name="microsoft-hpc-pack"></a><span data-ttu-id="b6287-121">Microsoft HPC Pack</span><span class="sxs-lookup"><span data-stu-id="b6287-121">Microsoft HPC Pack</span></span>
<span data-ttu-id="b6287-122">HPC Pack 是建置在 Microsoft Azure 和 Windows Server 技術上的 Microsoft 免費 HPC 解決方案，可執行 Windows 和 Linux HPC 工作負載。</span><span class="sxs-lookup"><span data-stu-id="b6287-122">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies, capable of running Windows and Linux HPC workloads.</span></span>  

* [<span data-ttu-id="b6287-123">下載 HPC Pack 2016</span><span class="sxs-lookup"><span data-stu-id="b6287-123">Download HPC Pack 2016</span></span>](https://www.microsoft.com/download/details.aspx?id=54507)
* [<span data-ttu-id="b6287-124">下載 HPC Pack 2012 R2 Update 3</span><span class="sxs-lookup"><span data-stu-id="b6287-124">Download HPC Pack 2012 R2 Update 3</span></span>](https://www.microsoft.com/download/details.aspx?id=49922)
* [<span data-ttu-id="b6287-125">Documentation</span><span class="sxs-lookup"><span data-stu-id="b6287-125">Documentation</span></span>](https://technet.microsoft.com/library/jj899572.aspx)
* <span data-ttu-id="b6287-126">Azure 中的 HPC Pack 叢集選項：[Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 和 [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="b6287-126">HPC Pack cluster options in Azure: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span> 
* [<span data-ttu-id="b6287-127">使用 HPC Pack 將暴增的工作負載移至 Azure 背景工作執行個體</span><span class="sxs-lookup"><span data-stu-id="b6287-127">Burst to Azure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="b6287-128">使用 HPC Pack 將暴增的工作負載移至 Azure Batch</span><span class="sxs-lookup"><span data-stu-id="b6287-128">Burst to Azure  Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)
* [<span data-ttu-id="b6287-129">Windows HPC 論壇</span><span class="sxs-lookup"><span data-stu-id="b6287-129">Windows HPC forums</span></span>](https://social.microsoft.com/Forums/home?category=windowshpc)

### <a name="linux-and-oss-cluster-solutions"></a><span data-ttu-id="b6287-130">Linux 與 OSS 叢集解決方案</span><span class="sxs-lookup"><span data-stu-id="b6287-130">Linux and OSS cluster solutions</span></span>
<span data-ttu-id="b6287-131">使用這些 Azure 範本來部署 Linux HPC 叢集。</span><span class="sxs-lookup"><span data-stu-id="b6287-131">Use these Azure templates to deploy Linux HPC clusters.</span></span>

* <span data-ttu-id="b6287-132">[加速 SLURM 叢集](https://azure.microsoft.com/documentation/templates/slurm/)和[部落格文章](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="b6287-132">[Spin up a SLURM cluster](https://azure.microsoft.com/documentation/templates/slurm/) and [blog post](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span></span>
* [<span data-ttu-id="b6287-133">加速扭力叢集</span><span class="sxs-lookup"><span data-stu-id="b6287-133">Spin up a Torque cluster</span></span>](https://azure.microsoft.com/documentation/templates/torque-cluster/)
* [<span data-ttu-id="b6287-134">使用 PBS Professional 計算格線範本 (英文)</span><span class="sxs-lookup"><span data-stu-id="b6287-134">Compute grid templates with PBS Professional</span></span>](https://github.com/xpillons/azure-hpc/tree/master/Compute-Grid-Infra)

## <a name="hpc-storage"></a><span data-ttu-id="b6287-135">HPC 儲存體</span><span class="sxs-lookup"><span data-stu-id="b6287-135">HPC storage</span></span>
* [<span data-ttu-id="b6287-136">Azure 上 HPC 儲存體的平行檔案系統 (英文)</span><span class="sxs-lookup"><span data-stu-id="b6287-136">Parallel file systems for HPC storage on Azure</span></span>](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
* [<span data-ttu-id="b6287-137">Intel Cloud Edition for Lustre Software - Eval</span><span class="sxs-lookup"><span data-stu-id="b6287-137">Intel Cloud Edition for Lustre Software - Eval</span></span>](https://azure.microsoft.com/marketplace/partners/intel/lustre-cloud-edition-evaleval-lustre-2-7/)
* [<span data-ttu-id="b6287-138">CentOS 7.2 範本上的 BeeGFS (英文)</span><span class="sxs-lookup"><span data-stu-id="b6287-138">BeeGFS on CentOS 7.2 template</span></span>](https://github.com/smith1511/hpc/tree/master/beegfs-shared-on-centos7.2)




## <a name="microsoft-mpi"></a><span data-ttu-id="b6287-139">Microsoft MPI</span><span class="sxs-lookup"><span data-stu-id="b6287-139">Microsoft MPI</span></span>
<span data-ttu-id="b6287-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) 是為了在 Windows 平台上開發及執行平行應用程式，Microsoft 實作的訊息傳遞介面標準。</span><span class="sxs-lookup"><span data-stu-id="b6287-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) is a Microsoft implementation of the Message Passing Interface standard for developing and running parallel applications on the Windows platform.</span></span>

* [<span data-ttu-id="b6287-141">下載 MS-MPI</span><span class="sxs-lookup"><span data-stu-id="b6287-141">Download MS-MPI</span></span>](http://go.microsoft.com/FWLink/p/?LinkID=389556)
* [<span data-ttu-id="b6287-142">MS-MPI 參考資料</span><span class="sxs-lookup"><span data-stu-id="b6287-142">MS-MPI reference</span></span>](https://msdn.microsoft.com/library/dn473458.aspx)
* [<span data-ttu-id="b6287-143">MPI 論壇</span><span class="sxs-lookup"><span data-stu-id="b6287-143">MPI forum</span></span>](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## <a name="compute-intensive-instances"></a><span data-ttu-id="b6287-144">計算密集型執行個體</span><span class="sxs-lookup"><span data-stu-id="b6287-144">Compute-intensive instances</span></span>
<span data-ttu-id="b6287-145">Azure 提供[各種大小的 VM](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (包括能夠連接到後端 RDMA 網路的[計算密集型 H 系列](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)執行個體) 來執行您的 Linux 和 Windows HPC 工作負載。</span><span class="sxs-lookup"><span data-stu-id="b6287-145">Azure offers a [range of VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), including [compute-intensive H-series](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) instances capable of connecting to a back-end RDMA network, to run your Linux and Windows HPC workloads.</span></span> 

* [<span data-ttu-id="b6287-146">設定 Linux RDMA 叢集以執行 MPI 應用程式</span><span class="sxs-lookup"><span data-stu-id="b6287-146">Set up a Linux RDMA cluster to run MPI applications</span></span>](../virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="b6287-147">使用 Microsoft HPC Pack 設定 Windows RDMA 叢集以執行 MPI 應用程式</span><span class="sxs-lookup"><span data-stu-id="b6287-147">Set up a Windows RDMA cluster with Microsoft HPC Pack to run MPI applications</span></span>](../virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

<span data-ttu-id="b6287-148">針對 GPU 密集的工作負載，請參閱 [NC 和 NV 大小 (英文)](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/)。</span><span class="sxs-lookup"><span data-stu-id="b6287-148">For GPU-intensive workloads, check out [NC and NV sizes](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).</span></span>

## <a name="samples-and-demos"></a><span data-ttu-id="b6287-149">範例和示範</span><span class="sxs-lookup"><span data-stu-id="b6287-149">Samples and demos</span></span>
* [<span data-ttu-id="b6287-150">Azure Batch C# 和 Python 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="b6287-150">Azure Batch C# and Python code samples</span></span>](https://github.com/Azure/azure-batch-samples)
* <span data-ttu-id="b6287-151">[Batch Shipyard](https://azure.github.io/batch-shipyard/) 工具組，以便將批次樣式 Dockerized 工作負載輕鬆部署至 Azure Batch</span><span class="sxs-lookup"><span data-stu-id="b6287-151">[Batch Shipyard](https://azure.github.io/batch-shipyard/) toolkit for easy deployment of batch-style Dockerized workloads to Azure Batch</span></span>
* <span data-ttu-id="b6287-152">[doAzureParallel (英文)](http://www.github.com/Azure/doAzureParallel) R 套件 (以 Azure Batch 為基礎而建置)</span><span class="sxs-lookup"><span data-stu-id="b6287-152">[doAzureParallel](http://www.github.com/Azure/doAzureParallel) R package, built on top of Azure Batch</span></span>
* [<span data-ttu-id="b6287-153">測試磁碟機 SUSE Linux Enterprise Server for HPC</span><span class="sxs-lookup"><span data-stu-id="b6287-153">Test drive SUSE Linux Enterprise Server for HPC</span></span>](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)

## <a name="related-azure-services"></a><span data-ttu-id="b6287-154">相關的 Azure 服務</span><span class="sxs-lookup"><span data-stu-id="b6287-154">Related Azure services</span></span>
* [<span data-ttu-id="b6287-155">Data Factory</span><span class="sxs-lookup"><span data-stu-id="b6287-155">Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)
* [<span data-ttu-id="b6287-156">機器學習服務</span><span class="sxs-lookup"><span data-stu-id="b6287-156">Machine Learning</span></span>](https://azure.microsoft.com/documentation/services/machine-learning/)
* [<span data-ttu-id="b6287-157">HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6287-157">HDInsight</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="b6287-158">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b6287-158">Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="b6287-159">虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="b6287-159">Virtual Machine Scale Sets</span></span>](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)
* [<span data-ttu-id="b6287-160">雲端服務</span><span class="sxs-lookup"><span data-stu-id="b6287-160">Cloud Services</span></span>](https://azure.microsoft.com/documentation/services/cloud-services/)
* [<span data-ttu-id="b6287-161">App Service</span><span class="sxs-lookup"><span data-stu-id="b6287-161">App Service</span></span>](https://azure.microsoft.com/documentation/services/app-service/)
* [<span data-ttu-id="b6287-162">媒體服務</span><span class="sxs-lookup"><span data-stu-id="b6287-162">Media Services</span></span>](https://azure.microsoft.com/documentation/services/media-services/)
* [<span data-ttu-id="b6287-163">函式</span><span class="sxs-lookup"><span data-stu-id="b6287-163">Functions</span></span>](https://azure.microsoft.com/documentation/services/functions/)

## <a name="architecture-blueprints"></a><span data-ttu-id="b6287-164">架構藍圖</span><span class="sxs-lookup"><span data-stu-id="b6287-164">Architecture blueprints</span></span>
* <span data-ttu-id="b6287-165">[用 Azure Batch 和 Azure Data Factory 的 HPC 及資料協調](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) 和[文章](../data-factory/data-factory-data-processing-using-batch.md)</span><span class="sxs-lookup"><span data-stu-id="b6287-165">[HPC and data orchestration using Azure Batch and Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) and [article](../data-factory/data-factory-data-processing-using-batch.md)</span></span>

## <a name="industry-solutions"></a><span data-ttu-id="b6287-166">產業方案</span><span class="sxs-lookup"><span data-stu-id="b6287-166">Industry solutions</span></span>
* [<span data-ttu-id="b6287-167">銀行與資本市場</span><span class="sxs-lookup"><span data-stu-id="b6287-167">Banking and capital markets</span></span>](https://finance.azure.com/)
* [<span data-ttu-id="b6287-168">工程模擬</span><span class="sxs-lookup"><span data-stu-id="b6287-168">Engineering simulations</span></span>](https://simulation.azure.com/) 

## <a name="customer-stories"></a><span data-ttu-id="b6287-169">客戶案例</span><span class="sxs-lookup"><span data-stu-id="b6287-169">Customer stories</span></span>
* [<span data-ttu-id="b6287-170">ANEO</span><span class="sxs-lookup"><span data-stu-id="b6287-170">ANEO</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=4168) 
* [<span data-ttu-id="b6287-171">d3View</span><span class="sxs-lookup"><span data-stu-id="b6287-171">d3View</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)
* [<span data-ttu-id="b6287-172">Ludwig Institute of Cancer Research</span><span class="sxs-lookup"><span data-stu-id="b6287-172">Ludwig Institute of Cancer Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5830)
* [<span data-ttu-id="b6287-173">Microsoft Research</span><span class="sxs-lookup"><span data-stu-id="b6287-173">Microsoft Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=15634)
* [<span data-ttu-id="b6287-174">明德精算顧問有限公司</span><span class="sxs-lookup"><span data-stu-id="b6287-174">Milliman</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=14967)
* [<span data-ttu-id="b6287-175">Mitsubishi UFJ Securities International</span><span class="sxs-lookup"><span data-stu-id="b6287-175">Mitsubishi UFJ Securities International</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=26266)
* [<span data-ttu-id="b6287-176">Schlumberger</span><span class="sxs-lookup"><span data-stu-id="b6287-176">Schlumberger</span></span>](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [<span data-ttu-id="b6287-177">Towers Watson</span><span class="sxs-lookup"><span data-stu-id="b6287-177">Towers Watson</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)
* [<span data-ttu-id="b6287-178">UberCloud</span><span class="sxs-lookup"><span data-stu-id="b6287-178">UberCloud</span></span>](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

## <a name="next-steps"></a><span data-ttu-id="b6287-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b6287-179">Next steps</span></span>
* <span data-ttu-id="b6287-180">如需最新公告，請參閱 [Microsoft HPC 和 Batch 小組部落格](http://blogs.technet.com/b/windowshpc/)以及[Azure 部落格](https://azure.microsoft.com/blog/tag/hpc/)。</span><span class="sxs-lookup"><span data-stu-id="b6287-180">For the latest announcements, see the [Microsoft HPC and Batch team blog](http://blogs.technet.com/b/windowshpc/) and the [Azure blog](https://azure.microsoft.com/blog/tag/hpc/).</span></span>
* <span data-ttu-id="b6287-181">另請參閱 [Batch 的新功能](https://azure.microsoft.com/updates/?service=batch)或訂閱 [RSS 摘要](https://azure.microsoft.com/updates/feed/?service=batch)。</span><span class="sxs-lookup"><span data-stu-id="b6287-181">Also see [what's new in Batch](https://azure.microsoft.com/updates/?service=batch) or subscribe to the [RSS feed](https://azure.microsoft.com/updates/feed/?service=batch).</span></span>

