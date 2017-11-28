---
title: "Excel 和 SOA 適用的 HPC Pack 叢集 | Microsoft Docs"
description: "開始在 Azure 中的 HPC Pack 叢集上執行大規模 Excel 和 SOA 工作負載"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: cb6a9abe-caf3-44da-b911-849a50f6cfb3
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 63babd94fdab15217cfb0757e4cd6efe458a628d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="5ac8e-103">開始在 Azure 中的 HPC Pack 叢集上執行 Excel 和 SOA 工作負載</span><span class="sxs-lookup"><span data-stu-id="5ac8e-103">Get started running Excel and SOA workloads on an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="5ac8e-104">此文章說明如何在 Azure 虛擬機器上使用 Azure 快速入門範本或 Azure PowerShell 部署指令碼 (選擇性) 部署 Microsoft HPC Pack 2012 R2 叢集。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-104">This article shows you how to deploy a Microsoft HPC Pack 2012 R2 cluster on Azure virtual machines by using an Azure quickstart template, or optionally an Azure PowerShell deployment script.</span></span> <span data-ttu-id="5ac8e-105">此叢集使用 Azure Marketplace VM 映像，其設計目的為使用 HPC Pack 執行 Microsoft Excel 或服務導向架構 (SOA) 工作負載。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-105">The cluster uses Azure Marketplace VM images designed to run Microsoft Excel or service-oriented architecture (SOA) workloads with HPC Pack.</span></span> <span data-ttu-id="5ac8e-106">您可以從內部部署用戶端電腦使用叢集來執行 Excel HPC 和 SOA 服務。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-106">You can use the cluster to run Excel HPC and SOA services from an on-premises client computer.</span></span> <span data-ttu-id="5ac8e-107">Excel HPC 服務包括 Excel 活頁簿卸載和 Excel 使用者定義函數或 UDF。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-107">The Excel HPC services include Excel workbook offloading and Excel user-defined functions, or UDFs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="5ac8e-108">此文章是以 HPC Pack 2012 R2 的功能、範本與指令碼為基礎。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-108">This article is based on features, templates, and scripts for HPC Pack 2012 R2.</span></span> <span data-ttu-id="5ac8e-109">HPC Pack 2016 目前不支援此案例。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-109">This scenario is not currently supported in HPC Pack 2016.</span></span>
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="5ac8e-110">在較高層級上，下圖顯示您建立的 HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-110">At a high level, the following diagram shows the HPC Pack cluster you create.</span></span>

![HPC 叢集與執行 Excel 工作負載的節點][scenario]

## <a name="prerequisites"></a><span data-ttu-id="5ac8e-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="5ac8e-112">Prerequisites</span></span>
* <span data-ttu-id="5ac8e-113">**用戶端電腦** - 您需要 Windows 用戶端電腦，以將範例 Excel 和 SOA 工作提交至叢集。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-113">**Client computer** - You need a Windows-based client computer to submit sample Excel and SOA jobs to the cluster.</span></span> <span data-ttu-id="5ac8e-114">您也需要 Windows 電腦來執行 Azure PowerShell 叢集部署指令碼 (如果您選擇該部署方法)。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-114">You also need a Windows computer to run the Azure PowerShell cluster deployment script (if you choose that deployment method).</span></span>
* <span data-ttu-id="5ac8e-115">**Azure 訂用帳戶** - 如果您沒有 Azure 訂用帳戶，只需要幾分鐘就可以建立 [免費帳戶](https://azure.microsoft.com/pricing/free-trial/) 。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-115">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="5ac8e-116">**核心配額** - 您可能需要增加核心的配額，特別是如果您部署多核心 VM 大小的數個叢集節點。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-116">**Cores quota** - You might need to increase the quota of cores, especially if you deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="5ac8e-117">如果您使用 Azure 快速入門範本，則 Resource Manager 中的核心配額是根據 Azure 區域而定。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-117">If you are using an Azure quickstart template, the cores quota in Resource Manager is per Azure region.</span></span> <span data-ttu-id="5ac8e-118">在此情況下，您可能需要增加特定區域中的配額。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-118">In that case, you might need to increase the quota in a specific region.</span></span> <span data-ttu-id="5ac8e-119">請參閱 [Azure 訂用帳戶限制、配額與限制](../../azure-subscription-service-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-119">See [Azure subscription limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="5ac8e-120">若要增加配額，請 [開立線上客戶支援要求](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) (免費)。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-120">To increase a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>
* <span data-ttu-id="5ac8e-121">**Microsoft Office 授權** - 如果您使用包含 Microsoft Excel 的 Marketplace HPC Pack 2012 R2 VM 映像部署計算節點，會安裝 Microsoft Excel Professional Plus 2013 的 30 天評估版。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-121">**Microsoft Office license** - If you deploy compute nodes using a Marketplace HPC Pack 2012 R2 VM image with Microsoft Excel, a 30-day evaluation version of Microsoft Excel Professional Plus 2013 is installed.</span></span> <span data-ttu-id="5ac8e-122">評估期過後，您需要提供有效的 Microsoft Office 授權來啟用 Excel，才能繼續執行工作負載。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-122">After the evaluation period, you need to provide a valid Microsoft Office license to activate Excel to continue to run workloads.</span></span> <span data-ttu-id="5ac8e-123">請參閱在本文章稍候的 [啟用 Excel](#excel-activation) 。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-123">See [Excel activation](#excel-activation) later in this article.</span></span> 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="5ac8e-124">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="5ac8e-124">Step 1.</span></span> <span data-ttu-id="5ac8e-125">在 Azure 中設定 HPC Pack 叢集</span><span class="sxs-lookup"><span data-stu-id="5ac8e-125">Set up an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="5ac8e-126">我們將說明設定 HPC Pack 2012 R2 叢集的兩種選項：第一，使用 Azure 快速入門範本和 Azure 入口網站；第二，使用 Azure PowerShell 部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-126">We show two options to set up the HPC Pack 2012 R2 cluster: first, using an Azure quickstart template and the Azure portal; and second, using an Azure PowerShell deployment script.</span></span>

### <a name="option-1-use-a-quickstart-template"></a><span data-ttu-id="5ac8e-127">選項 1。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-127">Option 1.</span></span> <span data-ttu-id="5ac8e-128">使用快速入門範本</span><span class="sxs-lookup"><span data-stu-id="5ac8e-128">Use a quickstart template</span></span>
<span data-ttu-id="5ac8e-129">使用 Azure 快速入門範本在 Azure 入口網站中快速地部署 HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-129">Use an Azure quickstart template to quickly deploy an HPC Pack cluster in the Azure portal.</span></span> <span data-ttu-id="5ac8e-130">當您在入口網站中開啟範本時，您會取得一個簡單的 UI 讓您在其中輸入叢集的設定。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-130">When you open the template in the portal, you get a simple UI where you enter the settings for your cluster.</span></span> <span data-ttu-id="5ac8e-131">步驟如下：</span><span class="sxs-lookup"><span data-stu-id="5ac8e-131">Here are the steps.</span></span> 

> [!TIP]
> <span data-ttu-id="5ac8e-132">如果您願意的話，可以使用 [Azure Marketplace 範本](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) 來專為 Excel 工作負載建立類似的叢集。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-132">If you want, use an [Azure Marketplace template](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) that creates a similar cluster specifically for Excel workloads.</span></span> <span data-ttu-id="5ac8e-133">其步驟與下文中的內容稍有不同。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-133">The steps differ slightly from the following.</span></span>
> 
> 

1. <span data-ttu-id="5ac8e-134">造訪 [在 GitHub 上建立 HPC 叢集範本頁面](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-134">Visit the [Create HPC Cluster template page on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span></span> <span data-ttu-id="5ac8e-135">您可根據意願檢視範本和原始碼的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-135">If you want, review information about the template and the source code.</span></span>
2. <span data-ttu-id="5ac8e-136">按一下 [部署至 Azure]  ，以在 Azure 入口網站中利用範本開始部署。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-136">Click **Deploy to Azure** to start a deployment with the template in the Azure portal.</span></span>
   
   ![將範本部署到 Azure][github]
3. <span data-ttu-id="5ac8e-138">在入口網站中，遵循下列步驟輸入 HPC 叢集範本的參數。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-138">In the portal, follow these steps to enter the parameters for the HPC cluster template.</span></span>
   
   <span data-ttu-id="5ac8e-139">a.</span><span class="sxs-lookup"><span data-stu-id="5ac8e-139">a.</span></span> <span data-ttu-id="5ac8e-140">在 [參數] 頁面上，輸入或修改範本參數的值。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-140">On the **Parameters** page, enter or modify values for the template parameters.</span></span> <span data-ttu-id="5ac8e-141">(按一下說明資訊的每個設定旁邊的圖示。)下列畫面顯示範例值。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-141">(Click the icon next to each setting for help information.) Sample values are shown in the following screen.</span></span> <span data-ttu-id="5ac8e-142">此範例會在 *hpc.local* 網域中建立名為 *hpc01* 的叢集，由一個前端節點和 2 個計算節點組成。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-142">This example creates a cluster named *hpc01* in the *hpc.local* domain consisting of a head node and 2 compute nodes.</span></span> <span data-ttu-id="5ac8e-143">計算節點是從包括 Microsoft Excel 的 HPC Pack VM 映像建立。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-143">The compute nodes are created from an HPC Pack VM image that includes Microsoft Excel.</span></span>
   
   ![輸入參數][parameters-new-portal]
   
   > [!NOTE]
   > <span data-ttu-id="5ac8e-145">前端節點 VM 會在 Windows Server 2012 R2 上從 HPC Pack 2012 R2 的 [最新 Marketplace 映像](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) 自動建立。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-145">The head node VM is created automatically from the [latest Marketplace image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) of HPC Pack 2012 R2 on Windows Server 2012 R2.</span></span> <span data-ttu-id="5ac8e-146">目前此映像以 HPC Pack 2012 R2 Update 3 為基礎。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-146">Currently the image is based on HPC Pack 2012 R2 Update 3.</span></span>
   > 
   > <span data-ttu-id="5ac8e-147">計算節點 VM 會從選取之計算節點系列的最新映像建立。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-147">Compute node VMs are created from the latest image of the selected compute node family.</span></span> <span data-ttu-id="5ac8e-148">選取 [ComputeNodeWithExcel] 選項做為最新的 HPC Pack 計算節點映像，包含評估版 Microsoft Excel Professional Plus 2013。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-148">Select the **ComputeNodeWithExcel** option for the latest HPC Pack compute node image that includes an evaluation version of Microsoft Excel Professional Plus 2013.</span></span> <span data-ttu-id="5ac8e-149">如果要部署一般 SOA 工作階段或 Excel UDF 卸載的叢集，請選擇 **ComputeNode** 選項 (不需安裝 Excel)。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-149">To deploy a cluster for general SOA sessions or for Excel UDF offloading, choose the **ComputeNode** option (without Excel installed).</span></span>
   > 
   > 
   
   <span data-ttu-id="5ac8e-150">b.</span><span class="sxs-lookup"><span data-stu-id="5ac8e-150">b.</span></span> <span data-ttu-id="5ac8e-151">選擇訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-151">Choose the subscription.</span></span>
   
   <span data-ttu-id="5ac8e-152">c.</span><span class="sxs-lookup"><span data-stu-id="5ac8e-152">c.</span></span> <span data-ttu-id="5ac8e-153">建立叢集的資源群組，例如 *hpc01RG*。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-153">Create a resource group for the cluster, such as *hpc01RG*.</span></span>
   
   <span data-ttu-id="5ac8e-154">d.</span><span class="sxs-lookup"><span data-stu-id="5ac8e-154">d.</span></span> <span data-ttu-id="5ac8e-155">選擇資源群組的位置，例如美國中部。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-155">Choose a location for the resource group, such as Central US.</span></span>
   
   <span data-ttu-id="5ac8e-156">e.</span><span class="sxs-lookup"><span data-stu-id="5ac8e-156">e.</span></span> <span data-ttu-id="5ac8e-157">在 [法律條款] 頁面上檢閱條款。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-157">On the **Legal terms** page, review the terms.</span></span> <span data-ttu-id="5ac8e-158">如果您同意，請按一下 [購買]。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-158">If you agree, click **Purchase**.</span></span> <span data-ttu-id="5ac8e-159">接著，當您完成範本值的設定時，請按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-159">Then, when you are finished setting the values for the template, click **Create**.</span></span>
4. <span data-ttu-id="5ac8e-160">當部署完成時 (通常需要約 30 分鐘)，從叢集前端節點匯出叢集憑證檔。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-160">When the deployment completes (it typically takes around 30 minutes), export the cluster certificate file from the cluster head node.</span></span> <span data-ttu-id="5ac8e-161">在稍後的步驟中，您要在用戶端電腦上匯入此公開憑證以提供安全 HTTP 繫結的伺服器端驗證。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-161">In a later step, you import this public certificate on the client computer to provide the server-side authentication for secure HTTP binding.</span></span>
   
   <span data-ttu-id="5ac8e-162">a.</span><span class="sxs-lookup"><span data-stu-id="5ac8e-162">a.</span></span> <span data-ttu-id="5ac8e-163">在 Azure 入口網站中，依序移至儀表板，選取前端節點，然後按一下頁面頂端的 [連線]，即可使用遠端桌面連線。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-163">In the Azure portal, go to the dashboard, select the head node, and click **Connect** at the top of the page to connect using Remote Desktop.</span></span>
   
    <!-- ![Connect to the head node][connect] -->
   
   <span data-ttu-id="5ac8e-164">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-164">b.</span></span> <span data-ttu-id="5ac8e-165">在憑證管理員中，使用標準程序來匯出前端節點憑證 (位於 Cert: \LocalMachine\My 之下) 而不需私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-165">Use standard procedures in Certificate Manager to export the head node certificate (located under Cert:\LocalMachine\My) without the private key.</span></span> <span data-ttu-id="5ac8e-166">在此範例中，匯出 *CN = hpc01.eastus.cloudapp.azure.com*。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-166">In this example, export *CN = hpc01.eastus.cloudapp.azure.com*.</span></span>
   
   ![匯出憑證][cert]

### <a name="option-2-use-the-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="5ac8e-168">選項 2。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-168">Option 2.</span></span> <span data-ttu-id="5ac8e-169">使用 HPC Pack IaaS 部署指令碼</span><span class="sxs-lookup"><span data-stu-id="5ac8e-169">Use the HPC Pack IaaS Deployment script</span></span>
<span data-ttu-id="5ac8e-170">HPC Pack IaaS 部署指令碼提供靈活的另一種方式部署 HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-170">The HPC Pack IaaS deployment script provides another versatile way to deploy an HPC Pack cluster.</span></span> <span data-ttu-id="5ac8e-171">它會在傳統部署模型中建立叢集，而範本則會使用 Azure Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-171">It creates a cluster in the classic deployment model, whereas the template uses the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="5ac8e-172">指令碼也和 Azure 全域或 Azure China 服務中的訂用帳戶相容。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-172">Also, the script is compatible with a subscription in either the Azure Global or Azure China service.</span></span>

<span data-ttu-id="5ac8e-173">**其他必要條件**</span><span class="sxs-lookup"><span data-stu-id="5ac8e-173">**Additional prerequisites**</span></span>

* <span data-ttu-id="5ac8e-174">**Azure PowerShell** - [安裝和設定 Azure PowerShell](/powershell/azure/overview) (0.8.10 版或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-174">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="5ac8e-175">**HPC Pack IaaS 部署指令碼** - 從 [Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=44949)下載並解壓縮最新版的指令碼。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-175">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="5ac8e-176">執行 `New-HPCIaaSCluster.ps1 –Version`以檢查指令碼的版本。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-176">Check the version of the script by running `New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="5ac8e-177">這篇文章根據 4.5.0 版或更新版本的指令碼。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-177">This article is based on version 4.5.0 or later of the script.</span></span>

<span data-ttu-id="5ac8e-178">**建立組態檔**</span><span class="sxs-lookup"><span data-stu-id="5ac8e-178">**Create the configuration file**</span></span>

 <span data-ttu-id="5ac8e-179">HPC Pack IaaS 部署指令碼會使用 XML 組態檔做為輸入，可描述 HPC 叢集的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-179">The HPC Pack IaaS deployment script uses an XML configuration file as input that describes the infrastructure of the HPC cluster.</span></span> <span data-ttu-id="5ac8e-180">若要部署由一個前端節點和從包含 Microsoft Excel 之運算節點映像所建立的 18 個運算節點組成的叢集，請將環境的值取代為下列範例組態檔。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-180">To deploy a cluster consisting of a head node and 18 compute nodes created from the compute node image that includes Microsoft Excel, substitute values for your environment into the following sample configuration file.</span></span> <span data-ttu-id="5ac8e-181">如需組態檔的詳細資訊，請參閱指令碼資料夾中的 Manual.rtf 檔案和 [使用 HPC Pack IaaS 部署指令碼建立 HPC 叢集](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-181">For more information about the configuration file, see the Manual.rtf file in the script folder and [Create an HPC cluster with the HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

```
<?xml version="1.0" encoding="utf-8"?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>MySubscription</SubscriptionName>
    <StorageAccount>hpc01</StorageAccount>
  </Subscription>
  <Location>West US</Location>
  <VNet>
    <VNetName>hpc-vnet01</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>HPCExcelDC01</VMName>
      <ServiceName>HPCExcelDC01</ServiceName>
      <VMSize>Medium</VMSize>
    </DomainController>
  </Domain>
   <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>HPCExcelHN01</VMName>
    <ServiceName>HPCExcelHN01</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI/>
    <EnableWebPortal/>
    <PostConfigScript>C:\tests\PostConfig.ps1</PostConfigScript>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>HPCExcelCN%00%</VMNamePattern>
    <ServiceName>HPCExcelCN01</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>18</NodeCount>
    <ImageName>HPCPack2012R2_ComputeNodeWithExcel</ImageName>
  </ComputeNodes>
</IaaSClusterConfig>
```

<span data-ttu-id="5ac8e-182">**組態檔的相關注意事項**</span><span class="sxs-lookup"><span data-stu-id="5ac8e-182">**Notes about the configuration file**</span></span>

* <span data-ttu-id="5ac8e-183">前端節點的 **VMName** **必須**和 **ServiceName** 相同，否則 SOA 工作會無法執行。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-183">The **VMName** of the head node **MUST** be the same as the **ServiceName**, or SOA jobs fail to run.</span></span>
* <span data-ttu-id="5ac8e-184">請確定您會指定 **EnableWebPortal** ，所以已經產生並匯出前端節點憑證。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-184">Make sure you specify **EnableWebPortal** so that the head node certificate is generated and exported.</span></span>
* <span data-ttu-id="5ac8e-185">這個檔案會指定在前端節點上執行的後續組態 PowerShell 指令碼 PostConfig.ps1。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-185">The file specifies a post-configuration PowerShell script PostConfig.ps1 that runs on the head node.</span></span> <span data-ttu-id="5ac8e-186">下列範例指令碼會設定 Azure 儲存體連接字串、從前端節點中移除計算節點角色，並在所有節點部署後讓所有節點上線。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-186">THe following sample script configures the Azure storage connection string, removes the compute node role from the head node, and brings all nodes online when they are deployed.</span></span> 

```
    # add the HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set the Azure storage connection string for the cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove the compute node role for head node to make sure the Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in the deployment including the head node and compute nodes, which should match the number specified in the XML configuration file
        $TotalNumOfNodes = 19

        $ErrorActionPreference = 'SilentlyContinue'

    # bring nodes online when they are deployed until all nodes are online
        while ($true)
        {
          Get-HpcNode -State Offline | Set-HpcNodeState -State Online -Confirm:$false
          $OnlineNodes = @(Get-HpcNode -State Online)
          if ($OnlineNodes.Count -eq $TotalNumOfNodes)
          {
             break
          }
          sleep 60
        }
```

<span data-ttu-id="5ac8e-187">**執行指令碼**</span><span class="sxs-lookup"><span data-stu-id="5ac8e-187">**Run the script**</span></span>

1. <span data-ttu-id="5ac8e-188">在用戶端電腦上以系統管理員身分開啟 PowerShell 主控台。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-188">Open the PowerShell console on the client computer as an administrator.</span></span>
2. <span data-ttu-id="5ac8e-189">將目錄變更為指令碼資料夾 (在本範例中為 E:\IaaSClusterScript)。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-189">Change directory to the script folder (E:\IaaSClusterScript in this example).</span></span>
   
   ```
   cd E:\IaaSClusterScript
   ```
3. <span data-ttu-id="5ac8e-190">若要部署 HPC Pack 叢集，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-190">To deploy the HPC Pack cluster, run the following command.</span></span> <span data-ttu-id="5ac8e-191">這個範例假設組態檔位於 E:\HPCDemoConfig.xml。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-191">This example assumes that the configuration file is located in E:\HPCDemoConfig.xml.</span></span>
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

<span data-ttu-id="5ac8e-192">HPC Pack 部署指令碼會執行一段時間。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-192">The HPC Pack deployment script runs for some time.</span></span> <span data-ttu-id="5ac8e-193">指令碼會匯出和下載叢集憑證，並將它儲存在用戶端電腦上目前使用者的文件資料夾中。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-193">One thing the script does is to export and download the cluster certificate and save it in the current user’s Documents folder on the client computer.</span></span> <span data-ttu-id="5ac8e-194">指令碼會產生類似下方的訊息。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-194">The script generates a message similar to the following.</span></span> <span data-ttu-id="5ac8e-195">在下列步驟中，您將在適當的憑證存放區中匯入憑證。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-195">In a following step, you import the certificate in the appropriate certificate store.</span></span>    

    You have enabled REST API or web portal on HPC Pack head node. Please import the following certificate in the Trusted Root Certification Authorities certificate store on the computer where you are submitting job or accessing the HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a><span data-ttu-id="5ac8e-196">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="5ac8e-196">Step 2.</span></span> <span data-ttu-id="5ac8e-197">卸載 Excel 活頁簿並從內部部署用戶端執行 UDF</span><span class="sxs-lookup"><span data-stu-id="5ac8e-197">Offload Excel workbooks and run UDFs from an on-premises client</span></span>
### <a name="excel-activation"></a><span data-ttu-id="5ac8e-198">啟用 Excel</span><span class="sxs-lookup"><span data-stu-id="5ac8e-198">Excel activation</span></span>
<span data-ttu-id="5ac8e-199">使用 ComputeNodeWithExcel VM 映像做為生產工作負載時，您需要提供有效的 Microsoft Office 授權金鑰才能啟用計算節點上的 Excel。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-199">When using the ComputeNodeWithExcel VM image for production workloads, you need to provide a valid Microsoft Office license key to activate Excel on the compute nodes.</span></span> <span data-ttu-id="5ac8e-200">否則，Excel 評估版會在 30 天後到期，且執行 Excel 活頁簿會失敗並出現 COMException (0x800AC472)。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-200">Otherwise, the evaluation version of Excel expires after 30 days, and running Excel workbooks will fail with the COMException (0x800AC472).</span></span> 

<span data-ttu-id="5ac8e-201">您可以重新取得額外 30 天的 Excel 評估時間：登入前端節點，並透過 HPC 叢集管理員在所有 Excel 計算節點上執行 `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` 。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-201">You can rearm Excel for another 30 days of evaluation time: Log on to the head node and clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` on all Excel compute nodes via HPC Cluster Manager.</span></span> <span data-ttu-id="5ac8e-202">您最多可以重新取得兩次。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-202">You can rearm a maximum of two times.</span></span> <span data-ttu-id="5ac8e-203">之後，您就必須提供有效的 Office 授權金鑰。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-203">After that, you must provide a valid Office license key.</span></span>

<span data-ttu-id="5ac8e-204">安裝在 VM 映像上的 Office Professional Plus 2013 是含有一般大量授權金鑰 (GVLK) 的大量授權版本。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-204">The Office Professional Plus 2013 installed on the VM image is a volume edition with a Generic Volume License Key (GVLK).</span></span> <span data-ttu-id="5ac8e-205">您可以透過金鑰管理服務 (KMS)/Active Directory 型啟用 (AD-BA) 或多重啟用金鑰 (MAK) 來啟用它。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-205">You can activate it via Key Management Service (KMS)/Active Directory-Based Activation (AD-BA) or Multiple Activation Key (MAK).</span></span> 

    * <span data-ttu-id="5ac8e-206">若要使用 KMS/AD-BA，請使用現有的 KMS 伺服器，或使用 Microsoft Office 2013 大量授權套件設定新伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-206">To use KMS/AD-BA, use an existing KMS server or set up a new one by using the Microsoft Office 2013 Volume License Pack.</span></span> <span data-ttu-id="5ac8e-207">(您可視需要設定前端節點上伺服器。)接著，透過網際網路或電話啟用 KMS 主機金鑰。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-207">(If you want to, set up the server on the head node.) Then, activate the KMS host key via the Internet or telephone.</span></span> <span data-ttu-id="5ac8e-208">然後再 clusrun `ospp.vbs` 以設定 KMS 伺服器和連接埠，以及啟用所有 Excel 計算節點上的 Office。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-208">Then clusrun `ospp.vbs` to set the KMS server and port and activate Office on all the Excel compute nodes.</span></span> 

    * <span data-ttu-id="5ac8e-209">若要使用 MAK，請先 clusrun `ospp.vbs` 以輸入金鑰，然後再透過網際網路或電話啟用所有 Excel 計算節點。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-209">To use MAK, first clusrun `ospp.vbs` to input the key and then activate all the Excel compute nodes via the Internet or telephone.</span></span> 

> [!NOTE]
> <span data-ttu-id="5ac8e-210">Office Professsional Plus 2013 的零售產品金鑰不適用於此 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-210">Retail product keys for Office Professional Plus 2013 cannot be used with this VM image.</span></span> <span data-ttu-id="5ac8e-211">如果您擁有非此 Office Professional Plus 2013 大量授權版本之 Office 或 Excel 版本的有效金鑰和安裝媒體，您也可以改用它們。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-211">If you have valid keys and installation media for Office or Excel editions other than this Office Professional Plus 2013 volume edition, you can use them instead.</span></span> <span data-ttu-id="5ac8e-212">先解除安裝此大量授權版本，然後安裝您所擁有的版本。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-212">First uninstall this volume edition and install the edition that you have.</span></span> <span data-ttu-id="5ac8e-213">您可以將重新安裝的 Excel 計算節點擷取成自訂 VM 映像，以在大規模部署時使用。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-213">The reinstalled Excel compute node can be captured as a customized VM image to use in a deployment at scale.</span></span>
> 
> 

### <a name="offload-excel-workbooks"></a><span data-ttu-id="5ac8e-214">卸載 Excel 活頁簿</span><span class="sxs-lookup"><span data-stu-id="5ac8e-214">Offload Excel workbooks</span></span>
<span data-ttu-id="5ac8e-215">遵循下列步驟來卸載 Excel 活頁簿，以在 Azure 的 HPC Pack 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-215">Follow these steps to offload an Excel workbook so that it runs on the HPC Pack cluster in Azure.</span></span> <span data-ttu-id="5ac8e-216">若要這樣做，您必須在用戶端電腦上安裝 Excel 2010 或 2013。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-216">To do this, you must have Excel 2010 or 2013 already installed on the client computer.</span></span>

1. <span data-ttu-id="5ac8e-217">使用步驟 1 中的其中一個選項，來部署具有 Excel 計算節點映像的 HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-217">Use one of the options in Step 1 to deploy an HPC Pack cluster with the Excel compute node image.</span></span> <span data-ttu-id="5ac8e-218">取得叢集憑證檔 (.cer) 以及叢集的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-218">Obtain the cluster certificate file (.cer) and cluster username and password.</span></span>
2. <span data-ttu-id="5ac8e-219">在用戶端電腦上，在 Cert:\CurrentUser\Root 下匯入叢集憑證。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-219">On the client computer, import the cluster certificate under Cert:\CurrentUser\Root.</span></span>
3. <span data-ttu-id="5ac8e-220">請確定已安裝 Excel。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-220">Make sure Excel is installed.</span></span> <span data-ttu-id="5ac8e-221">在與用戶端電腦上的 Excel.exe 相同的資料夾中，建立包含下列內容的 Excel.exe.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-221">Create an Excel.exe.config file with the following contents in the same folder as Excel.exe on the client computer.</span></span> <span data-ttu-id="5ac8e-222">這樣可確保 HPC Pack 2012 R2 Excel COM 增益集順利載入。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-222">This step ensures that the HPC Pack 2012 R2 Excel COM add-in loads successfully.</span></span>
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. <span data-ttu-id="5ac8e-223">設定用戶端以將工作提交到 HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-223">Set up the client to submit jobs to the HPC Pack cluster.</span></span> <span data-ttu-id="5ac8e-224">其中一個選項是下載完整的 [HPC Pack 2012 R2 Update 3 安裝](http://www.microsoft.com/download/details.aspx?id=49922) ，並安裝 HPC Pack 用戶端。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-224">One option is to download the full [HPC Pack 2012 R2 Update 3 installation](http://www.microsoft.com/download/details.aspx?id=49922) and install the HPC Pack client.</span></span> <span data-ttu-id="5ac8e-225">或者，為您的電腦 ([x64](http://www.microsoft.com/download/details.aspx?id=14632)、[x86](https://www.microsoft.com/download/details.aspx?id=5555)) 下載並安裝 [HPC Pack 2012 R2 Update 3 用戶端公用程式](https://www.microsoft.com/download/details.aspx?id=49923)及適當的 Visual C++ 2010 可轉散發套件。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-225">Alternatively, download and install the [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923) and the appropriate Visual C++ 2010 redistributable for your computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span></span>
5. <span data-ttu-id="5ac8e-226">在此範例中，我們使用名為 ConvertiblePricing_Complete.xlsb 的範例 Excel 活頁簿。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-226">In this example, we use a sample Excel workbook named ConvertiblePricing_Complete.xlsb.</span></span> <span data-ttu-id="5ac8e-227">您可以從 [這裡](https://www.microsoft.com/en-us/download/details.aspx?id=2939)下載。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-227">You can download it [here](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span></span>
6. <span data-ttu-id="5ac8e-228">將 Excel 活頁簿複製到工作資料夾，例如 D:\Excel\Run。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-228">Copy the Excel workbook to a working folder such as D:\Excel\Run.</span></span>
7. <span data-ttu-id="5ac8e-229">開啟 Excel 活頁簿。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-229">Open the Excel workbook.</span></span> <span data-ttu-id="5ac8e-230">在 [開發] 功能區上，按一下 [COM 增益集] 並確認 HPC Pack Excel COM 增益集已成功載入。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-230">On the **Develop** ribbon, click **COM Add-Ins** and confirm that the HPC Pack Excel COM add-in is loaded successfully.</span></span>
   
   ![HPC Pack 的 Excel 增益集][addin]
8. <span data-ttu-id="5ac8e-232">藉由變更加上註解的行，編輯 Excel 中的 VBA 巨集 HPCControlMacros，如下列指令碼所示。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-232">Edit the VBA macro HPCControlMacros in Excel by changing the commented lines as shown in the following script.</span></span> <span data-ttu-id="5ac8e-233">請將您的環境取代為適當的值。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-233">Substitute appropriate values for your environment.</span></span>
   
   ![HPC Pack 的 Excel 巨集][macro]
   
   ```
   'Private Const HPC_ClusterScheduler = "HEADNODE_NAME"
   Private Const HPC_ClusterScheduler = "hpc01.eastus.cloudapp.azure.com"
   
   'Private Const HPC_NetworkShare = "\\PATH\TO\SHARE\DIRECTORY"
   Private Const HPC_DependFiles = "D:\Excel\Upload\ConvertiblePricing_Complete.xlsb=ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.Initialize ActiveWorkbook
   HPCExcelClient.Initialize ActiveWorkbook, HPC_DependFiles
   
   'HPCWorkbookPath = HPC_NetworkShare & Application.PathSeparator & ActiveWorkbook.name
   HPCWorkbookPath = "ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath
   HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath, UserName:="hpc\azureuser", Password:="<YourPassword>"
   ```
9. <span data-ttu-id="5ac8e-235">將 Excel 活頁簿複製到上傳目錄，例如 D:\Excel\Upload。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-235">Copy the Excel workbook to an upload directory such as D:\Excel\Upload.</span></span> <span data-ttu-id="5ac8e-236">此目錄是在 VBA 巨集的 HPC_DependsFiles 常數中指定。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-236">This directory is specified in the HPC_DependsFiles constant in the VBA macro.</span></span>
10. <span data-ttu-id="5ac8e-237">若要在 Azure 的叢集中執行活頁簿，請按一下工作表上的 [叢集]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-237">To run the workbook on the cluster in Azure, click the **Cluster** button on the worksheet.</span></span>

### <a name="run-excel-udfs"></a><span data-ttu-id="5ac8e-238">執行 Excel UDF</span><span class="sxs-lookup"><span data-stu-id="5ac8e-238">Run Excel UDFs</span></span>
<span data-ttu-id="5ac8e-239">若要執行 Excel UDF，請遵循上述的步驟 1 - 3 來設定用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-239">To run Excel UDFs, follow the preceding steps 1 – 3 to set up the client computer.</span></span> <span data-ttu-id="5ac8e-240">對於 Excel UDF，您不需在計算節點上安裝 Excel 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-240">For Excel UDFs, you don't need to have the Excel application installed on compute nodes.</span></span> <span data-ttu-id="5ac8e-241">因此，在建立您的叢集計算節點時，您可以選擇一般計算節點映像，而不是含有 Excel 的計算節點映像。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-241">So, when creating your cluster compute nodes, you could choose a normal compute node image instead of the compute node image with Excel.</span></span>

> [!NOTE]
> <span data-ttu-id="5ac8e-242">[Excel 2010 和 2013 叢集連接器] 對話方塊中有 34 個字元的限制。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-242">There is a 34 character limit in the Excel 2010 and 2013 cluster connector dialog box.</span></span> <span data-ttu-id="5ac8e-243">您可以使用此對話方塊來指定執行 UDF 的叢集。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-243">You use this dialog box to specify the cluster that runs the UDFs.</span></span> <span data-ttu-id="5ac8e-244">如果完整的叢集名稱過長 (例如 hpcexcelhn01.southeastasia.cloudapp.azure.com)，該名稱就無法放入對話方塊中。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-244">If the full cluster name is longer (for example, hpcexcelhn01.southeastasia.cloudapp.azure.com), it does not fit in the dialog box.</span></span> <span data-ttu-id="5ac8e-245">解決方法是使用完整叢集名稱的值設定電腦全域變數，例如 *CCP_IAASHN*。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-245">The workaround is to set a machine-wide variable such as *CCP_IAASHN* with the value of the long cluster name.</span></span> <span data-ttu-id="5ac8e-246">然後，在對話方塊中輸入 *%CCP_IAASHN%* 做為叢集前端節點名稱。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-246">Then, enter *%CCP_IAASHN%* in the dialog box as the cluster head node name.</span></span> 
> 
> 

<span data-ttu-id="5ac8e-247">成功部署叢集之後，繼續進行下列步驟來執行內建的範例 Excel UDF。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-247">After the cluster is successfully deployed, continue with the following steps to run a sample built-in Excel UDF.</span></span> <span data-ttu-id="5ac8e-248">關於自訂的 Excel UDF，請參閱這些 [資源](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) 以建置 XLL 並將其部署在 IaaS 叢集上。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-248">For customized Excel UDFs, see these [resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) to build the XLLs and deploy them on the IaaS cluster.</span></span>

1. <span data-ttu-id="5ac8e-249">開啟新的 Excel 活頁簿。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-249">Open a new Excel workbook.</span></span> <span data-ttu-id="5ac8e-250">在 [開發] 功能區上，按一下 [增益集]。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-250">On the **Develop** ribbon, click **Add-Ins**.</span></span> <span data-ttu-id="5ac8e-251">然後在對話方塊中按一下 [瀏覽]、瀏覽至 %CCP_HOME%Bin\XLL32 資料夾並選取範例 ClusterUDF32.xll。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-251">Then, in the dialog box, click **Browse**, navigate to the %CCP_HOME%Bin\XLL32 folder, and select the sample ClusterUDF32.xll.</span></span> <span data-ttu-id="5ac8e-252">如果 ClusterUDF32 不存在於用戶端電腦上，您可以從前端節點上的 %CCP_HOME%Bin\XLL32 資料夾複製它。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-252">If the ClusterUDF32 doesn't exist on the client machine, copy it from the %CCP_HOME%Bin\XLL32 folder on the head node.</span></span>
   
   ![選取 UDF][udf]
2. <span data-ttu-id="5ac8e-254">按一下 [檔案] > [選項] > [進階]。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-254">Click **File** > **Options** > **Advanced**.</span></span> <span data-ttu-id="5ac8e-255">在 [公式] 下，核取 [允許使用者定義的 XLL 函數執行計算叢集]。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-255">Under **Formulas**, check **Allow user-defined XLL functions to run a compute cluster**.</span></span> <span data-ttu-id="5ac8e-256">然後按一下 [選項] 並在 [叢集前端節點名稱] 中輸入完整叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-256">Then click **Options** and enter the full cluster name in **Cluster head node name**.</span></span> <span data-ttu-id="5ac8e-257">(如先前所述，這個輸入方塊限制為 34 個字元，因此較長的叢集名稱可能不適合。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-257">(As noted previously this input box is limited to 34 characters, so a long cluster name may not fit.</span></span> <span data-ttu-id="5ac8e-258">您在這裡可以對完整叢集名稱使用電腦全域變數。)</span><span class="sxs-lookup"><span data-stu-id="5ac8e-258">You may use a machine-wide variable here for a long cluster name.)</span></span>
   
   ![設定 UDF][options]
3. <span data-ttu-id="5ac8e-260">若要在叢集上執行 UDF 運算，請按一下值 =XllGetComputerNameC() 的儲存格並按 Enter。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-260">To run the UDF calculation on the cluster, click the cell with value =XllGetComputerNameC() and press Enter.</span></span> <span data-ttu-id="5ac8e-261">函數只會擷取 UDF 執行所在的計算節點名稱。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-261">The function simply retrieves the name of the compute node on which the UDF runs.</span></span> <span data-ttu-id="5ac8e-262">初次執行時，認證對話方塊會提示輸入使用者名稱和密碼以連接到 IaaS 叢集。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-262">For the first run, a credentials dialog box prompts for the username and password to connect to the IaaS cluster.</span></span>
   
   ![執行 UDF][run]
   
   <span data-ttu-id="5ac8e-264">有大量儲存格要計算時，請按 Alt-Shift-Ctrl + F9 以在所有儲存格上執行計算。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-264">When there are many cells to calculate, press Alt-Shift-Ctrl + F9 to run the calculation on all cells.</span></span>

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a><span data-ttu-id="5ac8e-265">步驟 3.</span><span class="sxs-lookup"><span data-stu-id="5ac8e-265">Step 3.</span></span> <span data-ttu-id="5ac8e-266">從內部部署用戶端執行 SOA 工作負載</span><span class="sxs-lookup"><span data-stu-id="5ac8e-266">Run a SOA workload from an on-premises client</span></span>
<span data-ttu-id="5ac8e-267">若要在 HPC Pack IaaS 叢集上執行一般 SOA 應用程式，請先使用步驟 1 的其中一個方法部署叢集。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-267">To run general SOA applications on the HPC Pack IaaS cluster, first use one of the methods in Step 1 to deploy the cluster.</span></span> <span data-ttu-id="5ac8e-268">在此案例中請指定一般計算節點映像，因為在計算節點上您不需要 Excel。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-268">Specify a generic compute node image in this case, because you do not need Excel on the compute nodes.</span></span> <span data-ttu-id="5ac8e-269">接著，遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-269">Then follow these steps.</span></span>

1. <span data-ttu-id="5ac8e-270">擷取叢集憑證之後，在 Cert:\CurrentUser\Root 下的用戶端電腦上匯入叢集憑證。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-270">After retrieving the cluster certificate, import it on the client computer under Cert:\CurrentUser\Root.</span></span>
2. <span data-ttu-id="5ac8e-271">安裝 [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) 和 [HPC Pack 2012 R2 Update 3 用戶端公用程式](https://www.microsoft.com/download/details.aspx?id=49923)。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-271">Install the [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) and [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923).</span></span> <span data-ttu-id="5ac8e-272">這些工具可讓您開發和執行 SOA 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-272">These tools enable you to develop and run SOA client applications.</span></span>
3. <span data-ttu-id="5ac8e-273">下載 HelloWorldR2 [範例程式碼](https://www.microsoft.com/download/details.aspx?id=41633)。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-273">Download the HelloWorldR2 [sample code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span> <span data-ttu-id="5ac8e-274">在 Visual Studio 2010 或 2012 中開啟 HelloWorldR2.sln。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-274">Open the HelloWorldR2.sln in Visual Studio 2010 or 2012.</span></span> <span data-ttu-id="5ac8e-275">(此範例目前與較新的 Visual Studio 版本不相容。)</span><span class="sxs-lookup"><span data-stu-id="5ac8e-275">(This sample is not currently compatible with more recent versions of Visual Studio.)</span></span>
4. <span data-ttu-id="5ac8e-276">首先建置 EchoService 專案。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-276">Build the EchoService project first.</span></span> <span data-ttu-id="5ac8e-277">接著以您部署至內部部署叢集的相同方式，將服務部署到 IaaS 叢集。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-277">Then, deploy the service to the IaaS cluster in the same way you deploy to an on-premises cluster.</span></span> <span data-ttu-id="5ac8e-278">如需詳細步驟，請參閱 HelloWordR2 中的 Readme.doc。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-278">For detailed steps, see the Readme.doc in HelloWordR2.</span></span> <span data-ttu-id="5ac8e-279">以下一節所述的方式修改並建置 HelloWorldR2 和其他專案，以產生執行於 Azure IaaS 叢集上的 SOA 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-279">Modify and build the HellWorldR2 and other projects as described in the following section to generate the SOA client applications that run on an Azure IaaS cluster.</span></span>

### <a name="use-http-binding-with-azure-storage-queue"></a><span data-ttu-id="5ac8e-280">搭配使用 Http 繫結和 Azure 儲存體佇列</span><span class="sxs-lookup"><span data-stu-id="5ac8e-280">Use Http binding with Azure storage queue</span></span>
<span data-ttu-id="5ac8e-281">若要搭配使用 Http 繫結與 Azure 儲存體佇列，請對範例程式碼進行一些變更。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-281">To use Http binding with an Azure storage queue, make a few changes to the sample code.</span></span>

* <span data-ttu-id="5ac8e-282">更新叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-282">Update the cluster name.</span></span>
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* <span data-ttu-id="5ac8e-283">(選擇性) 在 SessionStartInfo 中使用預設 TransportScheme 或明確地將它設為 Http。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-283">Optionally, use the default TransportScheme in SessionStartInfo or explicitly set it to Http.</span></span>

```
    info.TransportScheme = TransportScheme.Http;
```

* <span data-ttu-id="5ac8e-284">使用預設繫結做為 BrokerClient。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-284">Use default binding for the BrokerClient.</span></span>
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    <span data-ttu-id="5ac8e-285">或者明確使用 basicHttpBinding 設定。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-285">Or set explicitly using the basicHttpBinding.</span></span>
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* <span data-ttu-id="5ac8e-286">選擇性地，在 SessionStartInfo 中將 UseAzureQueue 旗標設為 true。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-286">Optionally, set the UseAzureQueue flag to true in SessionStartInfo.</span></span> <span data-ttu-id="5ac8e-287">如果未設定，它會根據預設，在叢集名稱具有 Azure 網域尾碼且 TransportScheme 為 Http 時設為 true。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-287">If not set, it will be set to true by default when the cluster name has Azure domain suffixes and the TransportScheme is Http.</span></span>
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a><span data-ttu-id="5ac8e-288">使用 Http 繫結而不使用 Azure 儲存體佇列</span><span class="sxs-lookup"><span data-stu-id="5ac8e-288">Use Http binding without Azure storage queue</span></span>
<span data-ttu-id="5ac8e-289">若要使用不含 Azure 儲存體佇列的 Http 繫結，請在 SessionStartInfo 中將 UseAzureQueue 旗標明確設為 false。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-289">To use Http binding without an Azure storage queue, explicitly set the UseAzureQueue flag to false in the SessionStartInfo.</span></span>

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a><span data-ttu-id="5ac8e-290">使用 NetTcp 繫結</span><span class="sxs-lookup"><span data-stu-id="5ac8e-290">Use NetTcp binding</span></span>
<span data-ttu-id="5ac8e-291">若要使用 NetTcp 繫結，組態就像是連接至內部部署叢集。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-291">To use NetTcp binding, the configuration is similar to connecting to an on-premises cluster.</span></span> <span data-ttu-id="5ac8e-292">您必須在前端節點 VM 上開啟幾個端點。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-292">You need to open a few endpoints on the head node VM.</span></span> <span data-ttu-id="5ac8e-293">舉例來說，如果您使用 HPC Pack IaaS 部署指令碼來建立叢集，請依下列方式在 Azure 入口網站中設定端點。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-293">If you used the HPC Pack IaaS deployment script to create the cluster, for example, set the endpoints in the Azure portal as follows.</span></span>

1. <span data-ttu-id="5ac8e-294">停止 VM。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-294">Stop the VM.</span></span>
2. <span data-ttu-id="5ac8e-295">新增 TCP 連接埠 9090、9087、9091、9094 分別做為工作階段、訊息代理程式、訊息代理程式背景工作和資料服務</span><span class="sxs-lookup"><span data-stu-id="5ac8e-295">Add the TCP ports 9090, 9087, 9091, 9094 for the Session, Broker, Broker worker, and Data services, respectively</span></span>
   
    ![設定端點][endpoint-new-portal]
3. <span data-ttu-id="5ac8e-297">啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-297">Start the VM.</span></span>

<span data-ttu-id="5ac8e-298">SOA 用戶端應用程式不需要變更，除了將標頭名稱改變為 IaaS 叢集的完整名稱。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-298">The SOA client application requires no changes except altering the head name to the IaaS cluster full name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ac8e-299">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5ac8e-299">Next steps</span></span>
* <span data-ttu-id="5ac8e-300">請參閱 [這些資源](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) 以取得使用 HPC Pack 執行 Excel 工作負載的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-300">See [these resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) for more information about running Excel workloads with HPC Pack.</span></span>
* <span data-ttu-id="5ac8e-301">請參閱 [管理 Microsoft HPC Pack 中的 SOA 服務](https://technet.microsoft.com/library/ff919412.aspx) 以取得使用 HPC Pack 部署和管理 SOA 服務的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5ac8e-301">See [Managing SOA Services in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) for more about deploying and managing SOA services with HPC Pack.</span></span>

<!--Image references-->
[scenario]: ./media/excel-cluster-hpcpack/scenario.png
[github]: ./media/excel-cluster-hpcpack/github.png
[template]: ./media/excel-cluster-hpcpack/template.png
[parameters]: ./media/excel-cluster-hpcpack/parameters.png
[parameters-new-portal]: ./media/excel-cluster-hpcpack/parameters-new-portal.png
[create]: ./media/excel-cluster-hpcpack/create.png
[connect]: ./media/excel-cluster-hpcpack/connect.png
[cert]: ./media/excel-cluster-hpcpack/cert.png
[addin]: ./media/excel-cluster-hpcpack/addin.png
[macro]: ./media/excel-cluster-hpcpack/macro.png
[options]: ./media/excel-cluster-hpcpack/options.png
[run]: ./media/excel-cluster-hpcpack/run.png
[endpoint]: ./media/excel-cluster-hpcpack/endpoint.png
[endpoint-new-portal]: ./media/excel-cluster-hpcpack/endpoint-new-portal.png
[udf]: ./media/excel-cluster-hpcpack/udf.png
