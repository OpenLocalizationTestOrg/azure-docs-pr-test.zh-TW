---
title: "for Excel 和 SOA 叢集 aaaHPC 組件 |Microsoft 文件"
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
ms.openlocfilehash: 55b4b2c25fe65d06b75025cc23c3c13b8b764238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="63e27-103">開始在 Azure 中的 HPC Pack 叢集上執行 Excel 和 SOA 工作負載</span><span class="sxs-lookup"><span data-stu-id="63e27-103">Get started running Excel and SOA workloads on an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="63e27-104">本文章將示範如何 toodeploy Microsoft HPC Pack 2012 R2 上叢集化 Azure 虛擬機器使用的 Azure 快速入門範本，或選擇性的 Azure PowerShell 部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="63e27-104">This article shows you how toodeploy a Microsoft HPC Pack 2012 R2 cluster on Azure virtual machines by using an Azure quickstart template, or optionally an Azure PowerShell deployment script.</span></span> <span data-ttu-id="63e27-105">hello 叢集會使用 Azure Marketplace VM 映像設計 toorun Microsoft Excel 或服務導向架構 (SOA) 工作負載使用 HPC Pack。</span><span class="sxs-lookup"><span data-stu-id="63e27-105">hello cluster uses Azure Marketplace VM images designed toorun Microsoft Excel or service-oriented architecture (SOA) workloads with HPC Pack.</span></span> <span data-ttu-id="63e27-106">您可以使用 hello 叢集 toorun Excel HPC 及 SOA 服務從內部部署用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="63e27-106">You can use hello cluster toorun Excel HPC and SOA services from an on-premises client computer.</span></span> <span data-ttu-id="63e27-107">hello Excel HPC 服務包括 Excel 活頁簿卸載和 Excel 使用者定義函數或 Udf。</span><span class="sxs-lookup"><span data-stu-id="63e27-107">hello Excel HPC services include Excel workbook offloading and Excel user-defined functions, or UDFs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="63e27-108">此文章是以 HPC Pack 2012 R2 的功能、範本與指令碼為基礎。</span><span class="sxs-lookup"><span data-stu-id="63e27-108">This article is based on features, templates, and scripts for HPC Pack 2012 R2.</span></span> <span data-ttu-id="63e27-109">HPC Pack 2016 目前不支援此案例。</span><span class="sxs-lookup"><span data-stu-id="63e27-109">This scenario is not currently supported in HPC Pack 2016.</span></span>
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="63e27-110">在高層級，hello 下列圖表顯示 hello HPC Pack 叢集您所建立。</span><span class="sxs-lookup"><span data-stu-id="63e27-110">At a high level, hello following diagram shows hello HPC Pack cluster you create.</span></span>

![HPC 叢集與執行 Excel 工作負載的節點][scenario]

## <a name="prerequisites"></a><span data-ttu-id="63e27-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="63e27-112">Prerequisites</span></span>
* <span data-ttu-id="63e27-113">**用戶端電腦**-您需要 Windows 架構的用戶端電腦 toosubmit 範例 Excel 和 SOA 工作 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="63e27-113">**Client computer** - You need a Windows-based client computer toosubmit sample Excel and SOA jobs toohello cluster.</span></span> <span data-ttu-id="63e27-114">您也需要 Windows 電腦 toorun hello Azure PowerShell 叢集部署指令碼 （如果您選擇的部署方法）。</span><span class="sxs-lookup"><span data-stu-id="63e27-114">You also need a Windows computer toorun hello Azure PowerShell cluster deployment script (if you choose that deployment method).</span></span>
* <span data-ttu-id="63e27-115">**Azure 訂用帳戶** - 如果您沒有 Azure 訂用帳戶，只需要幾分鐘就可以建立 [免費帳戶](https://azure.microsoft.com/pricing/free-trial/) 。</span><span class="sxs-lookup"><span data-stu-id="63e27-115">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="63e27-116">**核心配額**-您可能需要的核心，tooincrease hello 配額，特別是當您部署具有多核心的 VM 大小的數個叢集節點。</span><span class="sxs-lookup"><span data-stu-id="63e27-116">**Cores quota** - You might need tooincrease hello quota of cores, especially if you deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="63e27-117">如果您使用 Azure 快速入門範本，資源管理員 中的 hello 核心配額為每個 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="63e27-117">If you are using an Azure quickstart template, hello cores quota in Resource Manager is per Azure region.</span></span> <span data-ttu-id="63e27-118">在此情況下，您可能需要在特定地區的 tooincrease hello 配額。</span><span class="sxs-lookup"><span data-stu-id="63e27-118">In that case, you might need tooincrease hello quota in a specific region.</span></span> <span data-ttu-id="63e27-119">請參閱 [Azure 訂用帳戶限制、配額與限制](../../azure-subscription-service-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="63e27-119">See [Azure subscription limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="63e27-120">tooincrease 配額限制時，[開啟線上客戶支援要求](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)不收費。</span><span class="sxs-lookup"><span data-stu-id="63e27-120">tooincrease a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>
* <span data-ttu-id="63e27-121">**Microsoft Office 授權** - 如果您使用包含 Microsoft Excel 的 Marketplace HPC Pack 2012 R2 VM 映像部署計算節點，會安裝 Microsoft Excel Professional Plus 2013 的 30 天評估版。</span><span class="sxs-lookup"><span data-stu-id="63e27-121">**Microsoft Office license** - If you deploy compute nodes using a Marketplace HPC Pack 2012 R2 VM image with Microsoft Excel, a 30-day evaluation version of Microsoft Excel Professional Plus 2013 is installed.</span></span> <span data-ttu-id="63e27-122">之後 hello 評估期間，您需要 tooprovide 有效 Microsoft Office 授權 tooactivate Excel toocontinue toorun 工作負載。</span><span class="sxs-lookup"><span data-stu-id="63e27-122">After hello evaluation period, you need tooprovide a valid Microsoft Office license tooactivate Excel toocontinue toorun workloads.</span></span> <span data-ttu-id="63e27-123">請參閱在本文章稍候的 [啟用 Excel](#excel-activation) 。</span><span class="sxs-lookup"><span data-stu-id="63e27-123">See [Excel activation](#excel-activation) later in this article.</span></span> 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="63e27-124">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="63e27-124">Step 1.</span></span> <span data-ttu-id="63e27-125">在 Azure 中設定 HPC Pack 叢集</span><span class="sxs-lookup"><span data-stu-id="63e27-125">Set up an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="63e27-126">我們顯示 hello HPC Pack 2012 R2 叢集的兩個選項 tooset： 首先，使用 Azure 快速入門的範本和 hello Azure 入口網站。與第二個，使用 Azure PowerShell 部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="63e27-126">We show two options tooset up hello HPC Pack 2012 R2 cluster: first, using an Azure quickstart template and hello Azure portal; and second, using an Azure PowerShell deployment script.</span></span>

### <a name="option-1-use-a-quickstart-template"></a><span data-ttu-id="63e27-127">選項 1。</span><span class="sxs-lookup"><span data-stu-id="63e27-127">Option 1.</span></span> <span data-ttu-id="63e27-128">使用快速入門範本</span><span class="sxs-lookup"><span data-stu-id="63e27-128">Use a quickstart template</span></span>
<span data-ttu-id="63e27-129">使用 Azure 快速入門範本 tooquickly 部署 HPC Pack 叢集 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="63e27-129">Use an Azure quickstart template tooquickly deploy an HPC Pack cluster in hello Azure portal.</span></span> <span data-ttu-id="63e27-130">當您開啟 hello 範本 hello 入口網站中時，您會取得您輸入 hello 設定叢集的簡單 UI。</span><span class="sxs-lookup"><span data-stu-id="63e27-130">When you open hello template in hello portal, you get a simple UI where you enter hello settings for your cluster.</span></span> <span data-ttu-id="63e27-131">以下是 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="63e27-131">Here are hello steps.</span></span> 

> [!TIP]
> <span data-ttu-id="63e27-132">如果您願意的話，可以使用 [Azure Marketplace 範本](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) 來專為 Excel 工作負載建立類似的叢集。</span><span class="sxs-lookup"><span data-stu-id="63e27-132">If you want, use an [Azure Marketplace template](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) that creates a similar cluster specifically for Excel workloads.</span></span> <span data-ttu-id="63e27-133">hello 步驟稍有不同 hello 下列。</span><span class="sxs-lookup"><span data-stu-id="63e27-133">hello steps differ slightly from hello following.</span></span>
> 
> 

1. <span data-ttu-id="63e27-134">請瀏覽 hello [GitHub 上的建立 HPC 叢集 [範本] 頁面](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)。</span><span class="sxs-lookup"><span data-stu-id="63e27-134">Visit hello [Create HPC Cluster template page on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span></span> <span data-ttu-id="63e27-135">如果您想，檢閱 hello 範本和 hello 原始程式碼的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="63e27-135">If you want, review information about hello template and hello source code.</span></span>
2. <span data-ttu-id="63e27-136">按一下**部署 tooAzure** toostart hello Azure 入口網站中的 hello 範本部署。</span><span class="sxs-lookup"><span data-stu-id="63e27-136">Click **Deploy tooAzure** toostart a deployment with hello template in hello Azure portal.</span></span>
   
   ![部署範本 tooAzure][github]
3. <span data-ttu-id="63e27-138">在 hello 入口網站中，遵循這些步驟 tooenter hello 參數的 hello HPC 叢集的範本。</span><span class="sxs-lookup"><span data-stu-id="63e27-138">In hello portal, follow these steps tooenter hello parameters for hello HPC cluster template.</span></span>
   
   <span data-ttu-id="63e27-139">a.</span><span class="sxs-lookup"><span data-stu-id="63e27-139">a.</span></span> <span data-ttu-id="63e27-140">在 hello**參數**頁面上，輸入或修改 hello 範本參數的值。</span><span class="sxs-lookup"><span data-stu-id="63e27-140">On hello **Parameters** page, enter or modify values for hello template parameters.</span></span> <span data-ttu-id="63e27-141">（按一下 hello 圖示下一個 tooeach 設定的說明資訊）。Hello 遵循畫面中會顯示範例值。</span><span class="sxs-lookup"><span data-stu-id="63e27-141">(Click hello icon next tooeach setting for help information.) Sample values are shown in hello following screen.</span></span> <span data-ttu-id="63e27-142">這個範例會建立名為叢集*hpc01*在 hello *hpc.local*前端節點和 2 組成網域的計算節點。</span><span class="sxs-lookup"><span data-stu-id="63e27-142">This example creates a cluster named *hpc01* in hello *hpc.local* domain consisting of a head node and 2 compute nodes.</span></span> <span data-ttu-id="63e27-143">hello 運算節點會建立從 HPC Pack VM 映像，其中包含 Microsoft Excel。</span><span class="sxs-lookup"><span data-stu-id="63e27-143">hello compute nodes are created from an HPC Pack VM image that includes Microsoft Excel.</span></span>
   
   ![輸入參數][parameters-new-portal]
   
   > [!NOTE]
   > <span data-ttu-id="63e27-145">hello 前端節點 VM 會自動建立從 hello[最新的 Marketplace 映像](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)的 HPC Pack 2012 R2，Windows Server 2012 R2 上。</span><span class="sxs-lookup"><span data-stu-id="63e27-145">hello head node VM is created automatically from hello [latest Marketplace image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) of HPC Pack 2012 R2 on Windows Server 2012 R2.</span></span> <span data-ttu-id="63e27-146">目前 hello 映像為基礎 HPC Pack 2012 R2 更新 3。</span><span class="sxs-lookup"><span data-stu-id="63e27-146">Currently hello image is based on HPC Pack 2012 R2 Update 3.</span></span>
   > 
   > <span data-ttu-id="63e27-147">運算節點 Vm 會建立從 hello hello 選取計算節點系列的最新映像。</span><span class="sxs-lookup"><span data-stu-id="63e27-147">Compute node VMs are created from hello latest image of hello selected compute node family.</span></span> <span data-ttu-id="63e27-148">選取 hello **ComputeNodeWithExcel** hello 最新 HPC Pack 計算節點映像，其中包含 Microsoft Excel Professional Plus 2013 評估版的選項。</span><span class="sxs-lookup"><span data-stu-id="63e27-148">Select hello **ComputeNodeWithExcel** option for hello latest HPC Pack compute node image that includes an evaluation version of Microsoft Excel Professional Plus 2013.</span></span> <span data-ttu-id="63e27-149">toodeploy 叢集一般 SOA 工作階段或 Excel UDF 卸載，選擇 hello **ComputeNode**選項 （不需安裝 Excel）。</span><span class="sxs-lookup"><span data-stu-id="63e27-149">toodeploy a cluster for general SOA sessions or for Excel UDF offloading, choose hello **ComputeNode** option (without Excel installed).</span></span>
   > 
   > 
   
   <span data-ttu-id="63e27-150">b.</span><span class="sxs-lookup"><span data-stu-id="63e27-150">b.</span></span> <span data-ttu-id="63e27-151">選擇 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="63e27-151">Choose hello subscription.</span></span>
   
   <span data-ttu-id="63e27-152">c.</span><span class="sxs-lookup"><span data-stu-id="63e27-152">c.</span></span> <span data-ttu-id="63e27-153">建立 hello 叢集資源群組，例如*hpc01RG*。</span><span class="sxs-lookup"><span data-stu-id="63e27-153">Create a resource group for hello cluster, such as *hpc01RG*.</span></span>
   
   <span data-ttu-id="63e27-154">d.</span><span class="sxs-lookup"><span data-stu-id="63e27-154">d.</span></span> <span data-ttu-id="63e27-155">選擇 hello 資源群組，例如美國中部的位置。</span><span class="sxs-lookup"><span data-stu-id="63e27-155">Choose a location for hello resource group, such as Central US.</span></span>
   
   <span data-ttu-id="63e27-156">e.</span><span class="sxs-lookup"><span data-stu-id="63e27-156">e.</span></span> <span data-ttu-id="63e27-157">在 hello**法律條款**頁面上，檢閱 hello 條款。</span><span class="sxs-lookup"><span data-stu-id="63e27-157">On hello **Legal terms** page, review hello terms.</span></span> <span data-ttu-id="63e27-158">如果您同意，請按一下 [購買]。</span><span class="sxs-lookup"><span data-stu-id="63e27-158">If you agree, click **Purchase**.</span></span> <span data-ttu-id="63e27-159">當您完成設定 hello hello 範本的值，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="63e27-159">Then, when you are finished setting hello values for hello template, click **Create**.</span></span>
4. <span data-ttu-id="63e27-160">Hello 部署完成時 （通常可以花大約 30 分鐘），從 hello 叢集前端節點匯出 hello 叢集憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="63e27-160">When hello deployment completes (it typically takes around 30 minutes), export hello cluster certificate file from hello cluster head node.</span></span> <span data-ttu-id="63e27-161">在稍後步驟中，您匯入這個 hello 的用戶端電腦 tooprovide hello 伺服器端驗證安全的 HTTP 繫結上的公開憑證。</span><span class="sxs-lookup"><span data-stu-id="63e27-161">In a later step, you import this public certificate on hello client computer tooprovide hello server-side authentication for secure HTTP binding.</span></span>
   
   <span data-ttu-id="63e27-162">a.</span><span class="sxs-lookup"><span data-stu-id="63e27-162">a.</span></span> <span data-ttu-id="63e27-163">在 hello Azure 入口網站，移 toohello 儀表板，選取 hello 前端節點，然後按一下 **連接**頂端 hello hello 頁面 tooconnect 使用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="63e27-163">In hello Azure portal, go toohello dashboard, select hello head node, and click **Connect** at hello top of hello page tooconnect using Remote Desktop.</span></span>
   
    <!-- ![Connect toohello head node][connect] -->
   
   <span data-ttu-id="63e27-164">b.</span><span class="sxs-lookup"><span data-stu-id="63e27-164">b.</span></span> <span data-ttu-id="63e27-165">使用具 hello 私密金鑰的憑證管理員 tooexport hello 前端節點憑證 （位於 Cert: \LocalMachine\My） 中的標準程序。</span><span class="sxs-lookup"><span data-stu-id="63e27-165">Use standard procedures in Certificate Manager tooexport hello head node certificate (located under Cert:\LocalMachine\My) without hello private key.</span></span> <span data-ttu-id="63e27-166">在此範例中，匯出 *CN = hpc01.eastus.cloudapp.azure.com*。</span><span class="sxs-lookup"><span data-stu-id="63e27-166">In this example, export *CN = hpc01.eastus.cloudapp.azure.com*.</span></span>
   
   ![匯出 hello 憑證][cert]

### <a name="option-2-use-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="63e27-168">選項 2。</span><span class="sxs-lookup"><span data-stu-id="63e27-168">Option 2.</span></span> <span data-ttu-id="63e27-169">使用 hello HPC Pack IaaS 部署指令碼</span><span class="sxs-lookup"><span data-stu-id="63e27-169">Use hello HPC Pack IaaS Deployment script</span></span>
<span data-ttu-id="63e27-170">hello HPC Pack IaaS 部署指令碼會提供其他的靈活方式 toodeploy HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="63e27-170">hello HPC Pack IaaS deployment script provides another versatile way toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="63e27-171">建立叢集的 hello 傳統部署模型，而 hello 範本使用 hello Azure Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="63e27-171">It creates a cluster in hello classic deployment model, whereas hello template uses hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="63e27-172">此外，hello 指令碼是與 hello Azure Global 或 Azure China 服務中的訂閱。</span><span class="sxs-lookup"><span data-stu-id="63e27-172">Also, hello script is compatible with a subscription in either hello Azure Global or Azure China service.</span></span>

<span data-ttu-id="63e27-173">**其他必要條件**</span><span class="sxs-lookup"><span data-stu-id="63e27-173">**Additional prerequisites**</span></span>

* <span data-ttu-id="63e27-174">**Azure PowerShell** - [安裝和設定 Azure PowerShell](/powershell/azure/overview) (0.8.10 版或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="63e27-174">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="63e27-175">**HPC Pack IaaS 部署指令碼**-下載及解壓縮 hello 最新版 hello 指令碼從 hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949)。</span><span class="sxs-lookup"><span data-stu-id="63e27-175">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="63e27-176">執行檢查 hello hello 指令碼版本`New-HPCIaaSCluster.ps1 –Version`。</span><span class="sxs-lookup"><span data-stu-id="63e27-176">Check hello version of hello script by running `New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="63e27-177">這篇文章根據 4.5.0 版本或更新版本的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="63e27-177">This article is based on version 4.5.0 or later of hello script.</span></span>

<span data-ttu-id="63e27-178">**建立 hello 設定檔**</span><span class="sxs-lookup"><span data-stu-id="63e27-178">**Create hello configuration file**</span></span>

 <span data-ttu-id="63e27-179">hello HPC Pack IaaS 部署指令碼會使用 XML 組態檔，做為輸入描述 hello hello HPC 叢集基礎結構。</span><span class="sxs-lookup"><span data-stu-id="63e27-179">hello HPC Pack IaaS deployment script uses an XML configuration file as input that describes hello infrastructure of hello HPC cluster.</span></span> <span data-ttu-id="63e27-180">toodeploy 前端節點和 18 所組成的叢集計算節點建立 hello 計算節點映像，包括 Microsoft Excel 中，替換成下列範例組態檔的 hello 環境的值。</span><span class="sxs-lookup"><span data-stu-id="63e27-180">toodeploy a cluster consisting of a head node and 18 compute nodes created from hello compute node image that includes Microsoft Excel, substitute values for your environment into hello following sample configuration file.</span></span> <span data-ttu-id="63e27-181">如需 hello 設定檔的詳細資訊，請參閱 hello 指令碼資料夾中的 hello Manual.rtf 檔案和[以 hello HPC Pack IaaS 部署指令碼建立 HPC 叢集](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="63e27-181">For more information about hello configuration file, see hello Manual.rtf file in hello script folder and [Create an HPC cluster with hello HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

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

<span data-ttu-id="63e27-182">**Hello 設定檔的相關注意事項**</span><span class="sxs-lookup"><span data-stu-id="63e27-182">**Notes about hello configuration file**</span></span>

* <span data-ttu-id="63e27-183">hello **VMName** hello 前端節點的**必須**是為 hello hello 相同**ServiceName**，SOA 工作失敗 toorun 或。</span><span class="sxs-lookup"><span data-stu-id="63e27-183">hello **VMName** of hello head node **MUST** be hello same as hello **ServiceName**, or SOA jobs fail toorun.</span></span>
* <span data-ttu-id="63e27-184">請確定您指定**EnableWebPortal**以便 hello 前端節點的憑證會產生並匯出。</span><span class="sxs-lookup"><span data-stu-id="63e27-184">Make sure you specify **EnableWebPortal** so that hello head node certificate is generated and exported.</span></span>
* <span data-ttu-id="63e27-185">hello 檔案會指定組態後 PowerShell 指令碼 PostConfig.ps1 hello 前端節點上執行。</span><span class="sxs-lookup"><span data-stu-id="63e27-185">hello file specifies a post-configuration PowerShell script PostConfig.ps1 that runs on hello head node.</span></span> <span data-ttu-id="63e27-186">下列範例指令碼的 hello 設定 hello Azure 儲存體連接字串、 hello 運算節點角色移除 hello 前端節點之後，並在部署時，使所有節點上線。</span><span class="sxs-lookup"><span data-stu-id="63e27-186">hello following sample script configures hello Azure storage connection string, removes hello compute node role from hello head node, and brings all nodes online when they are deployed.</span></span> 

```
    # add hello HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set hello Azure storage connection string for hello cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove hello compute node role for head node toomake sure hello Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in hello deployment including hello head node and compute nodes, which should match hello number specified in hello XML configuration file
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

<span data-ttu-id="63e27-187">**執行 hello 指令碼**</span><span class="sxs-lookup"><span data-stu-id="63e27-187">**Run hello script**</span></span>

1. <span data-ttu-id="63e27-188">系統管理員身分開啟 hello hello 用戶端電腦上的 PowerShell 主控台。</span><span class="sxs-lookup"><span data-stu-id="63e27-188">Open hello PowerShell console on hello client computer as an administrator.</span></span>
2. <span data-ttu-id="63e27-189">變更目錄 toohello 指令碼資料夾 (在此範例中 E:\IaaSClusterScript)。</span><span class="sxs-lookup"><span data-stu-id="63e27-189">Change directory toohello script folder (E:\IaaSClusterScript in this example).</span></span>
   
   ```
   cd E:\IaaSClusterScript
   ```
3. <span data-ttu-id="63e27-190">toodeploy hello HPC Pack 叢集，請執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="63e27-190">toodeploy hello HPC Pack cluster, run hello following command.</span></span> <span data-ttu-id="63e27-191">這個範例假設 hello 設定檔位於 E:\HPCDemoConfig.xml。</span><span class="sxs-lookup"><span data-stu-id="63e27-191">This example assumes that hello configuration file is located in E:\HPCDemoConfig.xml.</span></span>
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

<span data-ttu-id="63e27-192">hello HPC Pack 部署指令碼會執行一些時間。</span><span class="sxs-lookup"><span data-stu-id="63e27-192">hello HPC Pack deployment script runs for some time.</span></span> <span data-ttu-id="63e27-193">一件事 hello 指令碼會執行為 tooexport 和下載 hello 叢集憑證並將它儲存在 hello 目前使用者的文件 資料夾中 hello 用戶端電腦上。</span><span class="sxs-lookup"><span data-stu-id="63e27-193">One thing hello script does is tooexport and download hello cluster certificate and save it in hello current user’s Documents folder on hello client computer.</span></span> <span data-ttu-id="63e27-194">hello 指令碼會產生類似 toohello 後的訊息。</span><span class="sxs-lookup"><span data-stu-id="63e27-194">hello script generates a message similar toohello following.</span></span> <span data-ttu-id="63e27-195">在下列步驟中，您匯入 hello 適當的憑證存放區中的 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="63e27-195">In a following step, you import hello certificate in hello appropriate certificate store.</span></span>    

    You have enabled REST API or web portal on HPC Pack head node. Please import hello following certificate in hello Trusted Root Certification Authorities certificate store on hello computer where you are submitting job or accessing hello HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a><span data-ttu-id="63e27-196">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="63e27-196">Step 2.</span></span> <span data-ttu-id="63e27-197">卸載 Excel 活頁簿並從內部部署用戶端執行 UDF</span><span class="sxs-lookup"><span data-stu-id="63e27-197">Offload Excel workbooks and run UDFs from an on-premises client</span></span>
### <a name="excel-activation"></a><span data-ttu-id="63e27-198">啟用 Excel</span><span class="sxs-lookup"><span data-stu-id="63e27-198">Excel activation</span></span>
<span data-ttu-id="63e27-199">當使用 hello ComputeNodeWithExcel VM 映像以生產工作負載時，您需要 tooprovide 有效 Microsoft Office 授權金鑰 tooactivate Excel hello 計算節點上。</span><span class="sxs-lookup"><span data-stu-id="63e27-199">When using hello ComputeNodeWithExcel VM image for production workloads, you need tooprovide a valid Microsoft Office license key tooactivate Excel on hello compute nodes.</span></span> <span data-ttu-id="63e27-200">否則，Excel hello 評估版到期後 30 天，並執行 Excel 活頁簿以 hello COMException (0x800AC472) 將會失敗。</span><span class="sxs-lookup"><span data-stu-id="63e27-200">Otherwise, hello evaluation version of Excel expires after 30 days, and running Excel workbooks will fail with hello COMException (0x800AC472).</span></span> 

<span data-ttu-id="63e27-201">您可以重設授權狀態 Excel 的評估時間延長 30 天： 登入 toohello 前端節點和 clusrun`%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe`上所有的 Excel 計算節點透過 HPC 叢集管理員。</span><span class="sxs-lookup"><span data-stu-id="63e27-201">You can rearm Excel for another 30 days of evaluation time: Log on toohello head node and clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` on all Excel compute nodes via HPC Cluster Manager.</span></span> <span data-ttu-id="63e27-202">您最多可以重新取得兩次。</span><span class="sxs-lookup"><span data-stu-id="63e27-202">You can rearm a maximum of two times.</span></span> <span data-ttu-id="63e27-203">之後，您就必須提供有效的 Office 授權金鑰。</span><span class="sxs-lookup"><span data-stu-id="63e27-203">After that, you must provide a valid Office license key.</span></span>

<span data-ttu-id="63e27-204">hello Office Professional Plus 2013 hello VM 映像上安裝為的大量授權版本含一般大量授權金鑰 (GVLK)。</span><span class="sxs-lookup"><span data-stu-id="63e27-204">hello Office Professional Plus 2013 installed on hello VM image is a volume edition with a Generic Volume License Key (GVLK).</span></span> <span data-ttu-id="63e27-205">您可以透過金鑰管理服務 (KMS)/Active Directory 型啟用 (AD-BA) 或多重啟用金鑰 (MAK) 來啟用它。</span><span class="sxs-lookup"><span data-stu-id="63e27-205">You can activate it via Key Management Service (KMS)/Active Directory-Based Activation (AD-BA) or Multiple Activation Key (MAK).</span></span> 

    * <span data-ttu-id="63e27-206">toouse KMS/AD-BA 使用現有的 KMS 伺服器，或設定一個新使用 hello Microsoft Office 2013 的磁碟區的授權封包。</span><span class="sxs-lookup"><span data-stu-id="63e27-206">toouse KMS/AD-BA, use an existing KMS server or set up a new one by using hello Microsoft Office 2013 Volume License Pack.</span></span> <span data-ttu-id="63e27-207">（如果您要設定 hello 伺服器 hello 前端節點上。）然後，啟用 hello KMS 主機金鑰透過 hello 網際網路或電話。</span><span class="sxs-lookup"><span data-stu-id="63e27-207">(If you want to, set up hello server on hello head node.) Then, activate hello KMS host key via hello Internet or telephone.</span></span> <span data-ttu-id="63e27-208">然後 clusrun `ospp.vbs` tooset hello KMS 伺服器和連接埠，並在所有 hello Excel 計算節點上啟用 Office。</span><span class="sxs-lookup"><span data-stu-id="63e27-208">Then clusrun `ospp.vbs` tooset hello KMS server and port and activate Office on all hello Excel compute nodes.</span></span> 

    * <span data-ttu-id="63e27-209">toouse MAK，第一個 clusrun `ospp.vbs` tooinput hello 索引鍵，然後啟用 透過 hello 網際網路或電話所有 hello Excel 計算節點。</span><span class="sxs-lookup"><span data-stu-id="63e27-209">toouse MAK, first clusrun `ospp.vbs` tooinput hello key and then activate all hello Excel compute nodes via hello Internet or telephone.</span></span> 

> [!NOTE]
> <span data-ttu-id="63e27-210">Office Professsional Plus 2013 的零售產品金鑰不適用於此 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="63e27-210">Retail product keys for Office Professional Plus 2013 cannot be used with this VM image.</span></span> <span data-ttu-id="63e27-211">如果您擁有非此 Office Professional Plus 2013 大量授權版本之 Office 或 Excel 版本的有效金鑰和安裝媒體，您也可以改用它們。</span><span class="sxs-lookup"><span data-stu-id="63e27-211">If you have valid keys and installation media for Office or Excel editions other than this Office Professional Plus 2013 volume edition, you can use them instead.</span></span> <span data-ttu-id="63e27-212">第一次解除安裝這個磁碟區版本並安裝您所擁有的 hello 版本。</span><span class="sxs-lookup"><span data-stu-id="63e27-212">First uninstall this volume edition and install hello edition that you have.</span></span> <span data-ttu-id="63e27-213">hello 重新安裝計算節點可以擷取成自訂 VM 映像 toouse 大規模的部署中的 Excel。</span><span class="sxs-lookup"><span data-stu-id="63e27-213">hello reinstalled Excel compute node can be captured as a customized VM image toouse in a deployment at scale.</span></span>
> 
> 

### <a name="offload-excel-workbooks"></a><span data-ttu-id="63e27-214">卸載 Excel 活頁簿</span><span class="sxs-lookup"><span data-stu-id="63e27-214">Offload Excel workbooks</span></span>
<span data-ttu-id="63e27-215">請遵循這些步驟 toooffload Excel 活頁簿，使其在 Azure 中的 hello HPC Pack 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="63e27-215">Follow these steps toooffload an Excel workbook so that it runs on hello HPC Pack cluster in Azure.</span></span> <span data-ttu-id="63e27-216">toodo，您必須擁有 Excel 2010 或 2013 hello 用戶端電腦上已安裝。</span><span class="sxs-lookup"><span data-stu-id="63e27-216">toodo this, you must have Excel 2010 or 2013 already installed on hello client computer.</span></span>

1. <span data-ttu-id="63e27-217">使用步驟 1 toodeploy HPC Pack 叢集以 hello Excel 中的 hello 選項的其中一個計算節點映像。</span><span class="sxs-lookup"><span data-stu-id="63e27-217">Use one of hello options in Step 1 toodeploy an HPC Pack cluster with hello Excel compute node image.</span></span> <span data-ttu-id="63e27-218">取得 hello 叢集憑證檔案 (.cer) 以及叢集使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="63e27-218">Obtain hello cluster certificate file (.cer) and cluster username and password.</span></span>
2. <span data-ttu-id="63e27-219">Hello 用戶端電腦上，匯入憑證： \CurrentUser\Root hello 叢集憑證。</span><span class="sxs-lookup"><span data-stu-id="63e27-219">On hello client computer, import hello cluster certificate under Cert:\CurrentUser\Root.</span></span>
3. <span data-ttu-id="63e27-220">請確定已安裝 Excel。</span><span class="sxs-lookup"><span data-stu-id="63e27-220">Make sure Excel is installed.</span></span> <span data-ttu-id="63e27-221">建立具有下列內容在 hello hello 位檔案與 Excel.exe hello 用戶端電腦上相同的資料夾。</span><span class="sxs-lookup"><span data-stu-id="63e27-221">Create an Excel.exe.config file with hello following contents in hello same folder as Excel.exe on hello client computer.</span></span> <span data-ttu-id="63e27-222">這個步驟可確保該 hello HPC Pack 2012 R2 Excel COM 增益集成功載入。</span><span class="sxs-lookup"><span data-stu-id="63e27-222">This step ensures that hello HPC Pack 2012 R2 Excel COM add-in loads successfully.</span></span>
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. <span data-ttu-id="63e27-223">設定 hello 用戶端 toosubmit 作業 toohello HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="63e27-223">Set up hello client toosubmit jobs toohello HPC Pack cluster.</span></span> <span data-ttu-id="63e27-224">其中一個選項是完整的 toodownload hello [HPC Pack 2012 R2 Update 3 安裝](http://www.microsoft.com/download/details.aspx?id=49922)並安裝 hello HPC Pack 用戶端。</span><span class="sxs-lookup"><span data-stu-id="63e27-224">One option is toodownload hello full [HPC Pack 2012 R2 Update 3 installation](http://www.microsoft.com/download/details.aspx?id=49922) and install hello HPC Pack client.</span></span> <span data-ttu-id="63e27-225">或者，下載並安裝 hello [HPC Pack 2012 R2 更新 3 用戶端公用程式](https://www.microsoft.com/download/details.aspx?id=49923)和 hello 適當 Visual c + + 2010 可轉散發套件為您的電腦 ([x64](http://www.microsoft.com/download/details.aspx?id=14632)， [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span><span class="sxs-lookup"><span data-stu-id="63e27-225">Alternatively, download and install hello [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923) and hello appropriate Visual C++ 2010 redistributable for your computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span></span>
5. <span data-ttu-id="63e27-226">在此範例中，我們使用名為 ConvertiblePricing_Complete.xlsb 的範例 Excel 活頁簿。</span><span class="sxs-lookup"><span data-stu-id="63e27-226">In this example, we use a sample Excel workbook named ConvertiblePricing_Complete.xlsb.</span></span> <span data-ttu-id="63e27-227">您可以從 [這裡](https://www.microsoft.com/en-us/download/details.aspx?id=2939)下載。</span><span class="sxs-lookup"><span data-stu-id="63e27-227">You can download it [here](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span></span>
6. <span data-ttu-id="63e27-228">將複製 hello Excel 活頁簿 tooa 工作資料夾 D:\Excel\Run 等。</span><span class="sxs-lookup"><span data-stu-id="63e27-228">Copy hello Excel workbook tooa working folder such as D:\Excel\Run.</span></span>
7. <span data-ttu-id="63e27-229">開啟 hello Excel 活頁簿。</span><span class="sxs-lookup"><span data-stu-id="63e27-229">Open hello Excel workbook.</span></span> <span data-ttu-id="63e27-230">在 hello**開發**功能區中，按一下  **COM 增益集**並確認該 hello HPC Pack Excel COM 增益集已順利載入。</span><span class="sxs-lookup"><span data-stu-id="63e27-230">On hello **Develop** ribbon, click **COM Add-Ins** and confirm that hello HPC Pack Excel COM add-in is loaded successfully.</span></span>
   
   ![HPC Pack 的 Excel 增益集][addin]
8. <span data-ttu-id="63e27-232">編輯 hello VBA 巨集會在 Excel 中 HPCControlMacros 藉由變更 hello 註解行 hello 下列指令碼所示。</span><span class="sxs-lookup"><span data-stu-id="63e27-232">Edit hello VBA macro HPCControlMacros in Excel by changing hello commented lines as shown in hello following script.</span></span> <span data-ttu-id="63e27-233">請將您的環境取代為適當的值。</span><span class="sxs-lookup"><span data-stu-id="63e27-233">Substitute appropriate values for your environment.</span></span>
   
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
9. <span data-ttu-id="63e27-235">將複製 hello Excel 活頁簿 tooan 上載目錄例如 D:\Excel\Upload。</span><span class="sxs-lookup"><span data-stu-id="63e27-235">Copy hello Excel workbook tooan upload directory such as D:\Excel\Upload.</span></span> <span data-ttu-id="63e27-236">Hello HPC_DependsFiles 常數中 hello VBA 巨集會指定這個目錄。</span><span class="sxs-lookup"><span data-stu-id="63e27-236">This directory is specified in hello HPC_DependsFiles constant in hello VBA macro.</span></span>
10. <span data-ttu-id="63e27-237">在 Azure 中的 hello 叢集上 toorun hello 活頁簿按一下 hello**叢集**hello 工作表上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="63e27-237">toorun hello workbook on hello cluster in Azure, click hello **Cluster** button on hello worksheet.</span></span>

### <a name="run-excel-udfs"></a><span data-ttu-id="63e27-238">執行 Excel UDF</span><span class="sxs-lookup"><span data-stu-id="63e27-238">Run Excel UDFs</span></span>
<span data-ttu-id="63e27-239">toorun Excel Udf 遵循 hello 先前步驟 1-3 tooset hello 用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="63e27-239">toorun Excel UDFs, follow hello preceding steps 1 – 3 tooset up hello client computer.</span></span> <span data-ttu-id="63e27-240">對於 Excel Udf，您不需要計算節點上安裝的 toohave hello Excel 應用程式。</span><span class="sxs-lookup"><span data-stu-id="63e27-240">For Excel UDFs, you don't need toohave hello Excel application installed on compute nodes.</span></span> <span data-ttu-id="63e27-241">因此，當建立您的叢集計算節點，您可以選擇標準的計算節點映像，而不是 hello 計算節點映像與 Excel。</span><span class="sxs-lookup"><span data-stu-id="63e27-241">So, when creating your cluster compute nodes, you could choose a normal compute node image instead of hello compute node image with Excel.</span></span>

> [!NOTE]
> <span data-ttu-id="63e27-242">沒有 34 字元限制在 hello Excel 2010 和 2013年叢集連接器 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="63e27-242">There is a 34 character limit in hello Excel 2010 and 2013 cluster connector dialog box.</span></span> <span data-ttu-id="63e27-243">您使用這個對話方塊方塊 toospecify hello 叢集來執行 hello Udf。</span><span class="sxs-lookup"><span data-stu-id="63e27-243">You use this dialog box toospecify hello cluster that runs hello UDFs.</span></span> <span data-ttu-id="63e27-244">如果 hello 完整的叢集名稱的長度 (例如，hpcexcelhn01.southeastasia.cloudapp.azure.com)，無法容納在 hello 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="63e27-244">If hello full cluster name is longer (for example, hpcexcelhn01.southeastasia.cloudapp.azure.com), it does not fit in hello dialog box.</span></span> <span data-ttu-id="63e27-245">hello 因應措施是 tooset 全機器變數，例如*CCP_IAASHN* hello 的 hello 長叢集名稱的值。</span><span class="sxs-lookup"><span data-stu-id="63e27-245">hello workaround is tooset a machine-wide variable such as *CCP_IAASHN* with hello value of hello long cluster name.</span></span> <span data-ttu-id="63e27-246">然後，輸入*%ccp_iaashn* hello 對話方塊中做為 hello 叢集前端節點名稱。</span><span class="sxs-lookup"><span data-stu-id="63e27-246">Then, enter *%CCP_IAASHN%* in hello dialog box as hello cluster head node name.</span></span> 
> 
> 

<span data-ttu-id="63e27-247">Hello 叢集已成功部署之後，繼續執行下列步驟 toorun hello 範例內建 Excel UDF。</span><span class="sxs-lookup"><span data-stu-id="63e27-247">After hello cluster is successfully deployed, continue with hello following steps toorun a sample built-in Excel UDF.</span></span> <span data-ttu-id="63e27-248">自訂 Excel Udf，請參閱這些[資源](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx)toobuild hello Xll，並將其部署 hello IaaS 叢集上。</span><span class="sxs-lookup"><span data-stu-id="63e27-248">For customized Excel UDFs, see these [resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild hello XLLs and deploy them on hello IaaS cluster.</span></span>

1. <span data-ttu-id="63e27-249">開啟新的 Excel 活頁簿。</span><span class="sxs-lookup"><span data-stu-id="63e27-249">Open a new Excel workbook.</span></span> <span data-ttu-id="63e27-250">在 hello**開發**功能區中，按一下 **增益集**。然後，在 hello 對話方塊中，按一下**瀏覽**，瀏覽 toohello %CCP_HOME%Bin\XLL32 資料夾，並選取 hello 範例 ClusterUDF32.xll。</span><span class="sxs-lookup"><span data-stu-id="63e27-250">On hello **Develop** ribbon, click **Add-Ins**. Then, in hello dialog box, click **Browse**, navigate toohello %CCP_HOME%Bin\XLL32 folder, and select hello sample ClusterUDF32.xll.</span></span> <span data-ttu-id="63e27-251">如果 hello ClusterUDF32 不存在 hello 用戶端電腦上，請將其複製 hello 前端節點上的 hello %CCP_HOME%Bin\XLL32 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="63e27-251">If hello ClusterUDF32 doesn't exist on hello client machine, copy it from hello %CCP_HOME%Bin\XLL32 folder on hello head node.</span></span>
   
   ![選取 hello UDF][udf]
2. <span data-ttu-id="63e27-253">按一下 [檔案] > [選項] > [進階]。</span><span class="sxs-lookup"><span data-stu-id="63e27-253">Click **File** > **Options** > **Advanced**.</span></span> <span data-ttu-id="63e27-254">在下**公式**，檢查**運算叢集可讓使用者定義 XLL 函式 toorun**。</span><span class="sxs-lookup"><span data-stu-id="63e27-254">Under **Formulas**, check **Allow user-defined XLL functions toorun a compute cluster**.</span></span> <span data-ttu-id="63e27-255">然後按一下 **選項**，然後輸入 hello 完整的叢集名稱中**叢集前端節點名稱**。</span><span class="sxs-lookup"><span data-stu-id="63e27-255">Then click **Options** and enter hello full cluster name in **Cluster head node name**.</span></span> <span data-ttu-id="63e27-256">（如所述先前這個輸入的方塊是有限的 too34 字元，因此長叢集名稱可能不適合。</span><span class="sxs-lookup"><span data-stu-id="63e27-256">(As noted previously this input box is limited too34 characters, so a long cluster name may not fit.</span></span> <span data-ttu-id="63e27-257">您在這裡可以對完整叢集名稱使用電腦全域變數。)</span><span class="sxs-lookup"><span data-stu-id="63e27-257">You may use a machine-wide variable here for a long cluster name.)</span></span>
   
   ![設定 hello UDF][options]
3. <span data-ttu-id="63e27-259">toorun hello UDF 計算 hello 在叢集上，按一下值 =XllGetComputerNameC() hello 儲存格，然後按 Enter。</span><span class="sxs-lookup"><span data-stu-id="63e27-259">toorun hello UDF calculation on hello cluster, click hello cell with value =XllGetComputerNameC() and press Enter.</span></span> <span data-ttu-id="63e27-260">hello 函式只會擷取 hello UDF 執行哪些 hello hello 運算節點名稱。</span><span class="sxs-lookup"><span data-stu-id="63e27-260">hello function simply retrieves hello name of hello compute node on which hello UDF runs.</span></span> <span data-ttu-id="63e27-261">第一次執行的 hello，認證對話方塊會提示輸入 hello 使用者名稱和密碼 tooconnect toohello IaaS 叢集中。</span><span class="sxs-lookup"><span data-stu-id="63e27-261">For hello first run, a credentials dialog box prompts for hello username and password tooconnect toohello IaaS cluster.</span></span>
   
   ![執行 UDF][run]
   
   <span data-ttu-id="63e27-263">當有許多儲存格 toocalculate 時，按下 Alt Shift Ctrl + F9 toorun hello 計算所有資料格上。</span><span class="sxs-lookup"><span data-stu-id="63e27-263">When there are many cells toocalculate, press Alt-Shift-Ctrl + F9 toorun hello calculation on all cells.</span></span>

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a><span data-ttu-id="63e27-264">步驟 3.</span><span class="sxs-lookup"><span data-stu-id="63e27-264">Step 3.</span></span> <span data-ttu-id="63e27-265">從內部部署用戶端執行 SOA 工作負載</span><span class="sxs-lookup"><span data-stu-id="63e27-265">Run a SOA workload from an on-premises client</span></span>
<span data-ttu-id="63e27-266">toorun 一般 SOA 應用程式在 hello HPC Pack IaaS 叢集中，先使用其中一種 hello 方法步驟 1 toodeploy hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="63e27-266">toorun general SOA applications on hello HPC Pack IaaS cluster, first use one of hello methods in Step 1 toodeploy hello cluster.</span></span> <span data-ttu-id="63e27-267">在此情況下，指定泛型計算節點映像，因為您不需要 Excel hello 計算節點上。</span><span class="sxs-lookup"><span data-stu-id="63e27-267">Specify a generic compute node image in this case, because you do not need Excel on hello compute nodes.</span></span> <span data-ttu-id="63e27-268">接著，遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="63e27-268">Then follow these steps.</span></span>

1. <span data-ttu-id="63e27-269">擷取後 hello 叢集憑證，請將它匯入憑證： \CurrentUser\Root hello 用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="63e27-269">After retrieving hello cluster certificate, import it on hello client computer under Cert:\CurrentUser\Root.</span></span>
2. <span data-ttu-id="63e27-270">安裝 hello [HPC Pack 2012 R2 更新 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921)和[HPC Pack 2012 R2 更新 3 用戶端公用程式](https://www.microsoft.com/download/details.aspx?id=49923)。</span><span class="sxs-lookup"><span data-stu-id="63e27-270">Install hello [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) and [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923).</span></span> <span data-ttu-id="63e27-271">這些工具讓您 toodevelop，並執行 SOA 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="63e27-271">These tools enable you toodevelop and run SOA client applications.</span></span>
3. <span data-ttu-id="63e27-272">下載 hello HelloWorldR2[範例程式碼](https://www.microsoft.com/download/details.aspx?id=41633)。</span><span class="sxs-lookup"><span data-stu-id="63e27-272">Download hello HelloWorldR2 [sample code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span> <span data-ttu-id="63e27-273">開啟 Visual Studio 2010 中的 HelloWorldR2.sln hello 或 2012年。</span><span class="sxs-lookup"><span data-stu-id="63e27-273">Open hello HelloWorldR2.sln in Visual Studio 2010 or 2012.</span></span> <span data-ttu-id="63e27-274">(此範例目前與較新的 Visual Studio 版本不相容。)</span><span class="sxs-lookup"><span data-stu-id="63e27-274">(This sample is not currently compatible with more recent versions of Visual Studio.)</span></span>
4. <span data-ttu-id="63e27-275">第一次建置 hello EchoService 專案。</span><span class="sxs-lookup"><span data-stu-id="63e27-275">Build hello EchoService project first.</span></span> <span data-ttu-id="63e27-276">接著，將部署 hello 服務 toohello IaaS 叢集中 hello 中相同的方式部署 tooan 內部部署叢集。</span><span class="sxs-lookup"><span data-stu-id="63e27-276">Then, deploy hello service toohello IaaS cluster in hello same way you deploy tooan on-premises cluster.</span></span> <span data-ttu-id="63e27-277">如需詳細步驟，請參閱 hello Readme.doc HelloWordR2 中。</span><span class="sxs-lookup"><span data-stu-id="63e27-277">For detailed steps, see hello Readme.doc in HelloWordR2.</span></span> <span data-ttu-id="63e27-278">修改及建置 hello HellWorldR2 和其他專案中下列區段 toogenerate hello SOA 用戶端應用程式在 Azure IaaS 叢集中執行的 hello 所述。</span><span class="sxs-lookup"><span data-stu-id="63e27-278">Modify and build hello HellWorldR2 and other projects as described in hello following section toogenerate hello SOA client applications that run on an Azure IaaS cluster.</span></span>

### <a name="use-http-binding-with-azure-storage-queue"></a><span data-ttu-id="63e27-279">搭配使用 Http 繫結和 Azure 儲存體佇列</span><span class="sxs-lookup"><span data-stu-id="63e27-279">Use Http binding with Azure storage queue</span></span>
<span data-ttu-id="63e27-280">使用 Azure 儲存體佇列，toouse Http 繫結進行一些變更 toohello 範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="63e27-280">toouse Http binding with an Azure storage queue, make a few changes toohello sample code.</span></span>

* <span data-ttu-id="63e27-281">更新 hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="63e27-281">Update hello cluster name.</span></span>
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* <span data-ttu-id="63e27-282">選擇性地用於 SessionStartInfo hello 預設 TransportScheme 或明確設定 tooHttp。</span><span class="sxs-lookup"><span data-stu-id="63e27-282">Optionally, use hello default TransportScheme in SessionStartInfo or explicitly set it tooHttp.</span></span>

```
    info.TransportScheme = TransportScheme.Http;
```

* <span data-ttu-id="63e27-283">Hello BrokerClient 使用預設繫結。</span><span class="sxs-lookup"><span data-stu-id="63e27-283">Use default binding for hello BrokerClient.</span></span>
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    <span data-ttu-id="63e27-284">或明確地使用 hello basicHttpBinding 設定。</span><span class="sxs-lookup"><span data-stu-id="63e27-284">Or set explicitly using hello basicHttpBinding.</span></span>
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* <span data-ttu-id="63e27-285">（選擇性） 設定 hello UseAzureQueue 旗標 tootrue SessionStartInfo 中。</span><span class="sxs-lookup"><span data-stu-id="63e27-285">Optionally, set hello UseAzureQueue flag tootrue in SessionStartInfo.</span></span> <span data-ttu-id="63e27-286">如果沒有設定，它就會設定 tootrue 預設 hello 叢集名稱已 Azure 網域尾碼和 hello TransportScheme 是 Http 時。</span><span class="sxs-lookup"><span data-stu-id="63e27-286">If not set, it will be set tootrue by default when hello cluster name has Azure domain suffixes and hello TransportScheme is Http.</span></span>
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a><span data-ttu-id="63e27-287">使用 Http 繫結而不使用 Azure 儲存體佇列</span><span class="sxs-lookup"><span data-stu-id="63e27-287">Use Http binding without Azure storage queue</span></span>
<span data-ttu-id="63e27-288">沒有 Azure 儲存體佇列中，明確地設定 hello UseAzureQueue 旗標 toofalse 在 hello SessionStartInfo toouse Http 繫結。</span><span class="sxs-lookup"><span data-stu-id="63e27-288">toouse Http binding without an Azure storage queue, explicitly set hello UseAzureQueue flag toofalse in hello SessionStartInfo.</span></span>

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a><span data-ttu-id="63e27-289">使用 NetTcp 繫結</span><span class="sxs-lookup"><span data-stu-id="63e27-289">Use NetTcp binding</span></span>
<span data-ttu-id="63e27-290">toouse NetTcp 繫結，hello 組態是類似 tooconnecting tooan 在內部部署叢集。</span><span class="sxs-lookup"><span data-stu-id="63e27-290">toouse NetTcp binding, hello configuration is similar tooconnecting tooan on-premises cluster.</span></span> <span data-ttu-id="63e27-291">您需要 tooopen hello 前端節點 VM 上的幾個端點。</span><span class="sxs-lookup"><span data-stu-id="63e27-291">You need tooopen a few endpoints on hello head node VM.</span></span> <span data-ttu-id="63e27-292">如果您使用 hello HPC Pack IaaS 部署指令碼 toocreate hello 叢集時，例如，集合中的 hello 端點 hello Azure 入口網站，如下所示。</span><span class="sxs-lookup"><span data-stu-id="63e27-292">If you used hello HPC Pack IaaS deployment script toocreate hello cluster, for example, set hello endpoints in hello Azure portal as follows.</span></span>

1. <span data-ttu-id="63e27-293">停止 hello VM。</span><span class="sxs-lookup"><span data-stu-id="63e27-293">Stop hello VM.</span></span>
2. <span data-ttu-id="63e27-294">將 hello TCP 連接埠 9090，9087，9091，9094 hello 工作階段中，為 Broker，分別 Broker 背景工作與資料服務</span><span class="sxs-lookup"><span data-stu-id="63e27-294">Add hello TCP ports 9090, 9087, 9091, 9094 for hello Session, Broker, Broker worker, and Data services, respectively</span></span>
   
    ![設定端點][endpoint-new-portal]
3. <span data-ttu-id="63e27-296">啟動 hello VM。</span><span class="sxs-lookup"><span data-stu-id="63e27-296">Start hello VM.</span></span>

<span data-ttu-id="63e27-297">hello SOA 用戶端應用程式不需要變更除了改變 hello 前端名稱 toohello IaaS 叢集完整名稱。</span><span class="sxs-lookup"><span data-stu-id="63e27-297">hello SOA client application requires no changes except altering hello head name toohello IaaS cluster full name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63e27-298">後續步驟</span><span class="sxs-lookup"><span data-stu-id="63e27-298">Next steps</span></span>
* <span data-ttu-id="63e27-299">請參閱 [這些資源](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) 以取得使用 HPC Pack 執行 Excel 工作負載的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="63e27-299">See [these resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) for more information about running Excel workloads with HPC Pack.</span></span>
* <span data-ttu-id="63e27-300">請參閱 [管理 Microsoft HPC Pack 中的 SOA 服務](https://technet.microsoft.com/library/ff919412.aspx) 以取得使用 HPC Pack 部署和管理 SOA 服務的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="63e27-300">See [Managing SOA Services in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) for more about deploying and managing SOA services with HPC Pack.</span></span>

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
