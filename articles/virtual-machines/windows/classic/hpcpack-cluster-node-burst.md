---
title: "aaaAdd 高載節點 tooan HPC Pack 叢集 |Microsoft 文件"
description: "了解如何 tooexpand HPC Pack 叢集隨 Azure 中加入雲端服務中執行的背景工作角色執行個體"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 24b79a8a-24ad-4002-ae76-75abc9b28c83
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 7ec40ffe76485742c9e458ec49e11805990974e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-on-demand-burst-nodes-tooan-hpc-pack-cluster-in-azure"></a><span data-ttu-id="b99af-103">在 Azure 中新增隨 「 高載 」 節點 tooan HPC Pack 叢集</span><span class="sxs-lookup"><span data-stu-id="b99af-103">Add on-demand "burst" nodes tooan HPC Pack cluster in Azure</span></span>
<span data-ttu-id="b99af-104">如果您設定[Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029)叢集在 Azure 中，您可能想 tooquickly 標尺 hello 叢集容量向上或向下而不會維護一組預先設定計算節點 Vm 的方式。</span><span class="sxs-lookup"><span data-stu-id="b99af-104">If you set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure, you might want a way tooquickly scale hello cluster capacity up or down, without maintaining a set of preconfigured compute node VMs.</span></span> <span data-ttu-id="b99af-105">本文章將示範如何 tooadd 隨 「 高載 」 節點 （背景工作角色執行個體執行中雲端服務） 做為 Azure 中的計算資源 tooa 前端節點。</span><span class="sxs-lookup"><span data-stu-id="b99af-105">This article shows you how tooadd on-demand "burst" nodes (worker role instances running in a cloud service) as compute resources tooa head node in Azure.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="b99af-106">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="b99af-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b99af-107">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="b99af-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="b99af-108">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="b99af-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

![高載節點][burst]

<span data-ttu-id="b99af-110">這篇文章中的 hello 步驟可協助您快速加入 Azure 節點 tooa 雲端 HPC Pack 前端節點 VM 進行測試或概念證明部署。</span><span class="sxs-lookup"><span data-stu-id="b99af-110">hello steps in this article help you add Azure nodes quickly tooa cloud-based HPC Pack head node VM for a test or proof-of-concept deployment.</span></span> <span data-ttu-id="b99af-111">hello 概要步驟如下 hello 與 hello 步驟太 「 高載 tooAzure 」 相同 tooadd 雲端運算容量 tooan 在內部部署 HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="b99af-111">hello high-level steps are hello same as hello steps too“burst tooAzure” tooadd cloud compute capacity tooan on-premises HPC Pack cluster.</span></span> <span data-ttu-id="b99af-112">如需教學課程，請參閱 [使用 Microsoft HPC Pack 設定混合式計算叢集](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="b99af-112">For a tutorial, see [Set up a hybrid compute cluster with Microsoft HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md).</span></span> <span data-ttu-id="b99af-113">詳細指導方針和生產環境部署的考量，請參閱[tooAzure 使用 Microsoft HPC Pack 高載](https://technet.microsoft.com/library/gg481749.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b99af-113">For detailed guidance and considerations for production deployments, see [Burst tooAzure with Microsoft HPC Pack](https://technet.microsoft.com/library/gg481749.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b99af-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="b99af-114">Prerequisites</span></span>
* <span data-ttu-id="b99af-115">**部署在 Azure VM 中的 HPC Pack 前端節點** -您可以使用獨立的前端節點 VM 或屬於較大叢集的節點。</span><span class="sxs-lookup"><span data-stu-id="b99af-115">**HPC Pack head node deployed in an Azure VM** - You can use a stand-alone head node VM or one that is part of a larger cluster.</span></span> <span data-ttu-id="b99af-116">toocreate 獨立的前端節點，請參閱[部署 HPC Pack 前端節點的 Azure VM 中](../../virtual-machines-windows-hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b99af-116">toocreate a stand-alone head node, see [Deploy an HPC Pack Head Node in an Azure VM](../../virtual-machines-windows-hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="b99af-117">如需自動化 HPC Pack 叢集部署選項，請參閱[選項 toocreate 和管理 Windows HPC 叢集，在 Azure 中使用 Microsoft HPC Pack](../../virtual-machines-windows-hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b99af-117">For automated HPC Pack cluster deployment options, see [Options toocreate and manage a Windows HPC cluster in Azure with Microsoft HPC Pack](../../virtual-machines-windows-hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
  > [!TIP]
  > <span data-ttu-id="b99af-118">如果您使用 hello [HPC Pack IaaS 部署指令碼](hpcpack-cluster-powershell-script.md)toocreate hello 叢集在 Azure 中，您可以在自動化部署中包含 Azure 高載節點。</span><span class="sxs-lookup"><span data-stu-id="b99af-118">If you use hello [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) toocreate hello cluster in Azure, you can include Azure burst nodes in your automated deployment.</span></span> <span data-ttu-id="b99af-119">請參閱文件中的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="b99af-119">See hello examples in that article.</span></span>
  > 
  > 
* <span data-ttu-id="b99af-120">**Azure 訂用帳戶**-tooadd Azure 節點，您可以選擇 hello 相同訂用帳戶使用 toodeploy hello 前端節點 VM，或不同的訂用帳戶 （或訂閱）。</span><span class="sxs-lookup"><span data-stu-id="b99af-120">**Azure subscription** - tooadd Azure nodes, you can choose hello same subscription used toodeploy hello head node VM, or a different subscription (or subscriptions).</span></span>
* <span data-ttu-id="b99af-121">**核心配額**-您可能需要 tooincrease hello 配額的核心，特別是當您選擇 toodeploy 具有多核心大小的數個 Azure 節點。</span><span class="sxs-lookup"><span data-stu-id="b99af-121">**Cores quota** - You might need tooincrease hello quota of cores, especially if you choose toodeploy several Azure nodes with multicore sizes.</span></span> <span data-ttu-id="b99af-122">tooincrease 配額限制時，[開啟線上客戶支援要求](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)不收費。</span><span class="sxs-lookup"><span data-stu-id="b99af-122">tooincrease a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>

## <a name="step-1-create-a-cloud-service-and-a-storage-account-for-hello-azure-nodes"></a><span data-ttu-id="b99af-123">步驟 1： 建立雲端服務和儲存體帳戶的 hello Azure 節點</span><span class="sxs-lookup"><span data-stu-id="b99af-123">Step 1: Create a cloud service and a storage account for hello Azure nodes</span></span>
<span data-ttu-id="b99af-124">使用您的 Azure 節點 hello Azure 傳統入口網站或對等的工具 tooconfigure hello 遵循 toodeploy 所需的資源：</span><span class="sxs-lookup"><span data-stu-id="b99af-124">Use hello Azure classic portal or equivalent tools tooconfigure hello following resources that are needed toodeploy your Azure nodes:</span></span>

* <span data-ttu-id="b99af-125">新的 Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="b99af-125">A new Azure cloud service</span></span>
* <span data-ttu-id="b99af-126">新的 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="b99af-126">A new Azure storage account</span></span>

> [!NOTE]
> <span data-ttu-id="b99af-127">請勿重複使用您訂用帳戶中現有的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="b99af-127">Don't reuse an existing cloud service in your subscription.</span></span> 
> 
> 

<span data-ttu-id="b99af-128">**考量**</span><span class="sxs-lookup"><span data-stu-id="b99af-128">**Considerations**</span></span>

* <span data-ttu-id="b99af-129">設定每個 Azure 節點範本您計劃 toocreate 個別的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="b99af-129">Configure a separate cloud service for each Azure node template that you plan toocreate.</span></span> <span data-ttu-id="b99af-130">不過，您可以使用 hello 多個節點範本相同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b99af-130">However, you can use hello same storage account for multiple node templates.</span></span>
* <span data-ttu-id="b99af-131">我們建議您在 hello 中尋找 hello 雲端服務和 hello 部署的 hello 儲存體帳戶相同的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="b99af-131">We recommend that you locate hello cloud service and hello storage account for hello deployment in hello same Azure region.</span></span>

## <a name="step-2-configure-an-azure-management-certificate"></a><span data-ttu-id="b99af-132">步驟 2：設定 Azure 管理憑證</span><span class="sxs-lookup"><span data-stu-id="b99af-132">Step 2: Configure an Azure management certificate</span></span>
<span data-ttu-id="b99af-133">tooadd Azure 節點當做計算資源，您需要對應憑證 toohello 用於 hello 部署的 Azure 訂用帳戶上 hello 前端節點和上傳管理憑證。</span><span class="sxs-lookup"><span data-stu-id="b99af-133">tooadd Azure nodes as compute resources, you need a management certificate on hello head node and upload a corresponding certificate toohello Azure subscription used for hello deployment.</span></span>

<span data-ttu-id="b99af-134">針對此案例中，您可以選擇 hello**預設 HPC Azure 管理憑證**的 HPC Pack 自動安裝與設定前端節點上。</span><span class="sxs-lookup"><span data-stu-id="b99af-134">For this scenario, you can choose hello **Default HPC Azure Management Certificate** that HPC Pack installs and configures automatically on the head node.</span></span> <span data-ttu-id="b99af-135">此憑證可用於測試及概念證明部署。</span><span class="sxs-lookup"><span data-stu-id="b99af-135">This certificate is useful for testing purposes and proof-of-concept deployments.</span></span> <span data-ttu-id="b99af-136">此憑證 toouse 上, 傳從 hello 前端節點 VM toothe 訂用帳戶檔案 C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer。</span><span class="sxs-lookup"><span data-stu-id="b99af-136">toouse this certificate, upload the file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer from hello head node VM toothe subscription.</span></span> <span data-ttu-id="b99af-137">在 hello tooupload hello 憑證[Azure 傳統入口網站](https://manage.windowsazure.com)，按一下 **設定** > **管理憑證**。</span><span class="sxs-lookup"><span data-stu-id="b99af-137">tooupload hello certificate in hello [Azure classic portal](https://manage.windowsazure.com), click **Settings** > **Management Certificates**.</span></span>

<span data-ttu-id="b99af-138">其他選項 tooconfigure hello 管理憑證，請參閱[案例 tooConfigure hello Azure 高載部署的 Azure 管理憑證](http://technet.microsoft.com/library/gg481759.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b99af-138">For additional options tooconfigure hello management certificate, see [Scenarios tooConfigure hello Azure Management Certificate for Azure Burst Deployments](http://technet.microsoft.com/library/gg481759.aspx).</span></span>

## <a name="step-3-deploy-azure-nodes-toohello-cluster"></a><span data-ttu-id="b99af-139">步驟 3： 部署 Azure 節點 toohello 叢集</span><span class="sxs-lookup"><span data-stu-id="b99af-139">Step 3: Deploy Azure nodes toohello cluster</span></span>
<span data-ttu-id="b99af-140">hello 步驟 tooadd 和啟動 Azure 節點，在此案例中是通常 hello 相同 hello 與內部部署前端節點的步驟。</span><span class="sxs-lookup"><span data-stu-id="b99af-140">hello steps tooadd and start Azure nodes in this scenario are generally hello same as hello steps with an on-premises head node.</span></span> <span data-ttu-id="b99af-141">如需詳細資訊，請參閱下列各節中的 hello[步驟 tooDeploy Azure 節點使用 Microsoft HPC Pack](https://technet.microsoft.com/library/gg481758.aspx):</span><span class="sxs-lookup"><span data-stu-id="b99af-141">For more information, see hello following sections in [Steps tooDeploy Azure Nodes with Microsoft HPC Pack](https://technet.microsoft.com/library/gg481758.aspx):</span></span>

* <span data-ttu-id="b99af-142">建立 Azure 節點範本</span><span class="sxs-lookup"><span data-stu-id="b99af-142">Create an Azure node template</span></span>
* <span data-ttu-id="b99af-143">新增 Azure 節點 toohello Windows HPC 叢集</span><span class="sxs-lookup"><span data-stu-id="b99af-143">Add Azure nodes toohello Windows HPC cluster</span></span>
* <span data-ttu-id="b99af-144">啟動 （佈建） Azure 節點的 hello</span><span class="sxs-lookup"><span data-stu-id="b99af-144">Start (provision) hello Azure nodes</span></span>

<span data-ttu-id="b99af-145">您加入及啟動 hello 節點之後，他們就可以為您 toouse toorun 叢集作業。</span><span class="sxs-lookup"><span data-stu-id="b99af-145">After you add and start hello nodes, they are ready for you toouse toorun cluster jobs.</span></span>

<span data-ttu-id="b99af-146">如果您在部署 Azure 節點時遇到問題，請參閱 [使用 Microsoft HPC Pack 部署 Azure 節點時的疑難排解](http://technet.microsoft.com/library/jj159097.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b99af-146">If you encounter problems when deploying Azure nodes, see [Troubleshoot Deployments of Azure Nodes with Microsoft HPC Pack](http://technet.microsoft.com/library/jj159097.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b99af-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b99af-147">Next steps</span></span>
* <span data-ttu-id="b99af-148">toouse hello 的大量計算執行個體大小高載節點，請參閱中的 hello 考量[高效能計算 VM 大小](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b99af-148">toouse a compute-intensive instance size for hello burst nodes, see hello considerations in [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="b99af-149">如果您想要自動成長或壓縮 hello Azure 運算資源，根據 hello 叢集工作負載，請參閱[自動擴增和縮減 HPC Pack 叢集中的 Azure 計算資源](hpcpack-cluster-node-autogrowshrink.md)。</span><span class="sxs-lookup"><span data-stu-id="b99af-149">If you want to automatically grow or shrink hello Azure computing resources according to hello cluster workload, see [Automatically grow and shrink Azure compute resources in an HPC Pack cluster](hpcpack-cluster-node-autogrowshrink.md).</span></span>

<!--Image references-->
[burst]: ./media/hpcpack-cluster-node-burst/burst.png
