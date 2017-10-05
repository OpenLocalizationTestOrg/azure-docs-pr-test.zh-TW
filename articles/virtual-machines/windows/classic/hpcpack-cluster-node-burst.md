---
title: "將高載節點新增至 HPC Pack 叢集 | Microsoft Docs"
description: "了解如何新增在雲端服務中執行的背景工作角色執行個體，以隨選擴充 Azure 中的 HPC Pack 叢集"
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
ms.openlocfilehash: 9336743b92130e37b1df2992aab806696f8276aa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="add-on-demand-burst-nodes-to-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="887ee-103">將隨選「高載」節點新增至 Azure 中的 HPC Pack 叢集</span><span class="sxs-lookup"><span data-stu-id="887ee-103">Add on-demand "burst" nodes to an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="887ee-104">如果您在 Azure 中設定 [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) 叢集，您可能想迅速相應增加或相應減少叢集容量，而不用維護一組預先設定的計算節點 VM。</span><span class="sxs-lookup"><span data-stu-id="887ee-104">If you set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure, you might want a way to quickly scale the cluster capacity up or down, without maintaining a set of preconfigured compute node VMs.</span></span> <span data-ttu-id="887ee-105">本文說明如何將隨選「高載」節點 (在雲端服務中執行的背景工作角色執行個體) 新增至 Azure 中的前端節點作為運算資源。</span><span class="sxs-lookup"><span data-stu-id="887ee-105">This article shows you how to add on-demand "burst" nodes (worker role instances running in a cloud service) as compute resources to a head node in Azure.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="887ee-106">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="887ee-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="887ee-107">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="887ee-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="887ee-108">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="887ee-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

![高載節點][burst]

<span data-ttu-id="887ee-110">本文中的步驟可協助您將 Azure 節點快速新增至雲端型 HPC Pack 前端節點 VM，以進行測試或概念驗證部署。</span><span class="sxs-lookup"><span data-stu-id="887ee-110">The steps in this article help you add Azure nodes quickly to a cloud-based HPC Pack head node VM for a test or proof-of-concept deployment.</span></span> <span data-ttu-id="887ee-111">高階步驟與將雲端計算能力新增至內部部署 HPC Pack 叢集的「將暴增的工作負載移至 Azure」步驟相同。</span><span class="sxs-lookup"><span data-stu-id="887ee-111">The high-level steps are the same as the steps to “burst to Azure” to add cloud compute capacity to an on-premises HPC Pack cluster.</span></span> <span data-ttu-id="887ee-112">如需教學課程，請參閱 [使用 Microsoft HPC Pack 設定混合式計算叢集](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="887ee-112">For a tutorial, see [Set up a hybrid compute cluster with Microsoft HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md).</span></span> <span data-ttu-id="887ee-113">如需生產部署的詳細指引和考量，請參閱 [使用 Microsoft HPC Pack 將暴增的工作負載移至 Azure](https://technet.microsoft.com/library/gg481749.aspx)。</span><span class="sxs-lookup"><span data-stu-id="887ee-113">For detailed guidance and considerations for production deployments, see [Burst to Azure with Microsoft HPC Pack](https://technet.microsoft.com/library/gg481749.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="887ee-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="887ee-114">Prerequisites</span></span>
* <span data-ttu-id="887ee-115">**部署在 Azure VM 中的 HPC Pack 前端節點** -您可以使用獨立的前端節點 VM 或屬於較大叢集的節點。</span><span class="sxs-lookup"><span data-stu-id="887ee-115">**HPC Pack head node deployed in an Azure VM** - You can use a stand-alone head node VM or one that is part of a larger cluster.</span></span> <span data-ttu-id="887ee-116">若要建立獨立的前端節點，請參閱 [在 Azure VM 中部署 HPC Pack 前端節點](../../virtual-machines-windows-hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="887ee-116">To create a stand-alone head node, see [Deploy an HPC Pack Head Node in an Azure VM](../../virtual-machines-windows-hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="887ee-117">如需自動化的 HPC Pack 叢集部署選項，請參閱 [使用 Microsoft HPC Pack 在 Azure 中建立及管理 Windows HPC 叢集的選項](../../virtual-machines-windows-hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="887ee-117">For automated HPC Pack cluster deployment options, see [Options to create and manage a Windows HPC cluster in Azure with Microsoft HPC Pack](../../virtual-machines-windows-hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
  > [!TIP]
  > <span data-ttu-id="887ee-118">如果您使用 [HPC Pack IaaS 部署指令碼](hpcpack-cluster-powershell-script.md) 在 Azure 中建立叢集，則可以在自動化部署中包含 Azure 高載節點。</span><span class="sxs-lookup"><span data-stu-id="887ee-118">If you use the [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) to create the cluster in Azure, you can include Azure burst nodes in your automated deployment.</span></span> <span data-ttu-id="887ee-119">請參閱該文件中的範例。</span><span class="sxs-lookup"><span data-stu-id="887ee-119">See the examples in that article.</span></span>
  > 
  > 
* <span data-ttu-id="887ee-120">**Azure 訂用帳戶** - 若要新增 Azure 節點，您可以選擇與用來部署前端節點 VM 相同的訂用帳戶，或選擇一或多個不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="887ee-120">**Azure subscription** - To add Azure nodes, you can choose the same subscription used to deploy the head node VM, or a different subscription (or subscriptions).</span></span>
* <span data-ttu-id="887ee-121">**核心配額** - 您可能需要增加核心的配額，特別是當您選擇部署數個具有多核心大小的 Azure 節點時。</span><span class="sxs-lookup"><span data-stu-id="887ee-121">**Cores quota** - You might need to increase the quota of cores, especially if you choose to deploy several Azure nodes with multicore sizes.</span></span> <span data-ttu-id="887ee-122">若要增加配額，請 [開立線上客戶支援要求](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) (免費)。</span><span class="sxs-lookup"><span data-stu-id="887ee-122">To increase a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>

## <a name="step-1-create-a-cloud-service-and-a-storage-account-for-the-azure-nodes"></a><span data-ttu-id="887ee-123">步驟 1：為 Azure 節點建立雲端服務和儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="887ee-123">Step 1: Create a cloud service and a storage account for the Azure nodes</span></span>
<span data-ttu-id="887ee-124">使用 Azure 傳統入口網站或對等工具，以設定下列在部署 Azure 節點時所需的資源：</span><span class="sxs-lookup"><span data-stu-id="887ee-124">Use the Azure classic portal or equivalent tools to configure the following resources that are needed to deploy your Azure nodes:</span></span>

* <span data-ttu-id="887ee-125">新的 Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="887ee-125">A new Azure cloud service</span></span>
* <span data-ttu-id="887ee-126">新的 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="887ee-126">A new Azure storage account</span></span>

> [!NOTE]
> <span data-ttu-id="887ee-127">請勿重複使用您訂用帳戶中現有的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="887ee-127">Don't reuse an existing cloud service in your subscription.</span></span> 
> 
> 

<span data-ttu-id="887ee-128">**考量**</span><span class="sxs-lookup"><span data-stu-id="887ee-128">**Considerations**</span></span>

* <span data-ttu-id="887ee-129">您打算建立的每個 Azure 節點範本設定個別的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="887ee-129">Configure a separate cloud service for each Azure node template that you plan to create.</span></span> <span data-ttu-id="887ee-130">不過，您可以將同一個儲存體帳戶用於多個節點範本。</span><span class="sxs-lookup"><span data-stu-id="887ee-130">However, you can use the same storage account for multiple node templates.</span></span>
* <span data-ttu-id="887ee-131">建議您將用於部署的雲端服務和儲存體帳戶放置在相同的 Azure 區域中。</span><span class="sxs-lookup"><span data-stu-id="887ee-131">We recommend that you locate the cloud service and the storage account for the deployment in the same Azure region.</span></span>

## <a name="step-2-configure-an-azure-management-certificate"></a><span data-ttu-id="887ee-132">步驟 2：設定 Azure 管理憑證</span><span class="sxs-lookup"><span data-stu-id="887ee-132">Step 2: Configure an Azure management certificate</span></span>
<span data-ttu-id="887ee-133">若要將 Azure 節點新增為運算資源，您在前端節點上必須要有管理憑證，且必須將對應的憑證上傳至用於部署的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="887ee-133">To add Azure nodes as compute resources, you need a management certificate on the head node and upload a corresponding certificate to the Azure subscription used for the deployment.</span></span>

<span data-ttu-id="887ee-134">針對這個案例，您可以選擇 HPC Pack 在前端節點上自動安裝及設定的 **預設 HPC Azure 管理憑證** 。</span><span class="sxs-lookup"><span data-stu-id="887ee-134">For this scenario, you can choose the **Default HPC Azure Management Certificate** that HPC Pack installs and configures automatically on the head node.</span></span> <span data-ttu-id="887ee-135">此憑證可用於測試及概念證明部署。</span><span class="sxs-lookup"><span data-stu-id="887ee-135">This certificate is useful for testing purposes and proof-of-concept deployments.</span></span> <span data-ttu-id="887ee-136">若要使用此憑證，請將檔案 C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer 從前端節點 VM 上傳至訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="887ee-136">To use this certificate, upload the file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer from the head node VM to the subscription.</span></span> <span data-ttu-id="887ee-137">若要上傳憑證，請在 [Azure 傳統入口網站](https://manage.windowsazure.com)中，按一下 [設定] > [管理憑證]。</span><span class="sxs-lookup"><span data-stu-id="887ee-137">To upload the certificate in the [Azure classic portal](https://manage.windowsazure.com), click **Settings** > **Management Certificates**.</span></span>

<span data-ttu-id="887ee-138">如需設定管理憑證的其他選項，請參閱 [為 Azure 高載部署設定 Azure 管理憑證的案例](http://technet.microsoft.com/library/gg481759.aspx)。</span><span class="sxs-lookup"><span data-stu-id="887ee-138">For additional options to configure the management certificate, see [Scenarios to Configure the Azure Management Certificate for Azure Burst Deployments](http://technet.microsoft.com/library/gg481759.aspx).</span></span>

## <a name="step-3-deploy-azure-nodes-to-the-cluster"></a><span data-ttu-id="887ee-139">步驟 3：將 Azure 節點部署至叢集</span><span class="sxs-lookup"><span data-stu-id="887ee-139">Step 3: Deploy Azure nodes to the cluster</span></span>
<span data-ttu-id="887ee-140">在此案例中新增及啟動 Azure 節點的步驟，與用於內部部署前端節點的步驟大致相同。</span><span class="sxs-lookup"><span data-stu-id="887ee-140">The steps to add and start Azure nodes in this scenario are generally the same as the steps with an on-premises head node.</span></span> <span data-ttu-id="887ee-141">如需詳細資訊，請參閱 [使用 Microsoft HPC Pack 部署 Azure 節點的步驟](https://technet.microsoft.com/library/gg481758.aspx)中的下列小節：</span><span class="sxs-lookup"><span data-stu-id="887ee-141">For more information, see the following sections in [Steps to Deploy Azure Nodes with Microsoft HPC Pack](https://technet.microsoft.com/library/gg481758.aspx):</span></span>

* <span data-ttu-id="887ee-142">建立 Azure 節點範本</span><span class="sxs-lookup"><span data-stu-id="887ee-142">Create an Azure node template</span></span>
* <span data-ttu-id="887ee-143">將 Azure 節點新增至 Windows HPC 叢集</span><span class="sxs-lookup"><span data-stu-id="887ee-143">Add Azure nodes to the Windows HPC cluster</span></span>
* <span data-ttu-id="887ee-144">啟動 (佈建) Azure 節點</span><span class="sxs-lookup"><span data-stu-id="887ee-144">Start (provision) the Azure nodes</span></span>

<span data-ttu-id="887ee-145">節點新增並啟動之後，即可供您用來執行叢集工作。</span><span class="sxs-lookup"><span data-stu-id="887ee-145">After you add and start the nodes, they are ready for you to use to run cluster jobs.</span></span>

<span data-ttu-id="887ee-146">如果您在部署 Azure 節點時遇到問題，請參閱 [使用 Microsoft HPC Pack 部署 Azure 節點時的疑難排解](http://technet.microsoft.com/library/jj159097.aspx)。</span><span class="sxs-lookup"><span data-stu-id="887ee-146">If you encounter problems when deploying Azure nodes, see [Troubleshoot Deployments of Azure Nodes with Microsoft HPC Pack](http://technet.microsoft.com/library/jj159097.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="887ee-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="887ee-147">Next steps</span></span>
* <span data-ttu-id="887ee-148">若要對高載節點使用密集計算的執行個體大小，請參閱[高效能運算 VM 大小](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中的考量。</span><span class="sxs-lookup"><span data-stu-id="887ee-148">To use a compute-intensive instance size for the burst nodes, see the considerations in [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="887ee-149">如果您想要根據叢集工作負載自動擴增或縮減 Azure 計算資源，請參閱 [在 HPC Pack 叢集中自動擴增和縮減 Azure 運算資源](hpcpack-cluster-node-autogrowshrink.md)。</span><span class="sxs-lookup"><span data-stu-id="887ee-149">If you want to automatically grow or shrink the Azure computing resources according to the cluster workload, see [Automatically grow and shrink Azure compute resources in an HPC Pack cluster](hpcpack-cluster-node-autogrowshrink.md).</span></span>

<!--Image references-->
[burst]: ./media/hpcpack-cluster-node-burst/burst.png
