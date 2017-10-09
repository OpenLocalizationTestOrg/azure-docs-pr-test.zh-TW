---
title: "aaaMonitor 及管理串流分析工作，使用 PowerShell |Microsoft 文件"
description: "深入了解如何 toouse Azure PowerShell 及指令程式 toomonitor 及管理串流分析工作。"
keywords: "azure powershell, azure powershell cmdlet, powershell 命令, powershell 指令碼"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 44abc82f1c44a5ebc1701badd6547b84dac239b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a><span data-ttu-id="c00fe-104">透過 Azure PowerShell Cmdlet 監視和管理串流分析工作</span><span class="sxs-lookup"><span data-stu-id="c00fe-104">Monitor and manage Stream Analytics jobs with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="c00fe-105">深入了解如何 toomonitor 和管理執行基本的資料流分析工作的資料流分析資源使用 Azure PowerShell cmdlet 和 powershell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="c00fe-105">Learn how toomonitor and manage Stream Analytics resources with Azure PowerShell cmdlets and powershell scripting that execute basic Stream Analytics tasks.</span></span>

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="c00fe-106">執行 Azure PowerShell Cmdlet 進行串流分析的必要條件</span><span class="sxs-lookup"><span data-stu-id="c00fe-106">Prerequisites for running Azure PowerShell cmdlets for Stream Analytics</span></span>
* <span data-ttu-id="c00fe-107">在您的訂用帳戶中建立「Azure 資源群組」。</span><span class="sxs-lookup"><span data-stu-id="c00fe-107">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="c00fe-108">hello 以下是範例 Azure PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="c00fe-108">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="c00fe-109">如需 Azure PowerShell 資訊，請參閱 [安裝並設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="c00fe-109">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

<span data-ttu-id="c00fe-110">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-110">Azure PowerShell 0.9.8:</span></span>  

         # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

<span data-ttu-id="c00fe-111">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-111">Azure PowerShell 1.0:</span></span>  

         # Log in tooyour Azure account
        Login-AzureRmAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> <span data-ttu-id="c00fe-112">以程式控制方式建立的串流分析工作預設不會啟用監視功能。</span><span class="sxs-lookup"><span data-stu-id="c00fe-112">Stream Analytics jobs created programmatically do not have monitoring enabled by default.</span></span>  <span data-ttu-id="c00fe-113">您可以手動啟用 hello Azure 入口網站，瀏覽 toohello 作業的 [監視] 頁面中的監視和 hello [啟用] 按鈕，或按一下 [可執行這項操作以程式設計方式位於 hello 步驟[Azure Stream Analytics 監視資料流分析作業以程式設計方式控制程式](stream-analytics-monitor-jobs.md)。</span><span class="sxs-lookup"><span data-stu-id="c00fe-113">You can manually enable monitoring in hello Azure Portal by navigating toohello job’s Monitor page and clicking hello Enable button or you can do this programmatically by following hello steps located at [Azure Stream Analytics - Monitor Stream Analytics Jobs Programatically](stream-analytics-monitor-jobs.md).</span></span>
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="c00fe-114">用於串流分析的 Azure PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="c00fe-114">Azure PowerShell cmdlets for Stream Analytics</span></span>
<span data-ttu-id="c00fe-115">hello 下列 Azure PowerShell 指令程式可以是使用的 toomonitor 及管理 Azure Stream Analytics 工作。</span><span class="sxs-lookup"><span data-stu-id="c00fe-115">hello following Azure PowerShell cmdlets can be used toomonitor and manage Azure Stream Analytics jobs.</span></span> <span data-ttu-id="c00fe-116">請注意，Azure PowerShell 有不同的版本。</span><span class="sxs-lookup"><span data-stu-id="c00fe-116">Note that Azure PowerShell has different versions.</span></span> 
<span data-ttu-id="c00fe-117">**在 hello 範例中所列的 hello 第一個命令是適用於 Azure PowerShell 為 0.9.8，hello 第二個命令會為 Azure PowerShell 1.0。**</span><span class="sxs-lookup"><span data-stu-id="c00fe-117">**In hello examples listed hello first command is for Azure PowerShell 0.9.8, hello second command is for Azure PowerShell 1.0.**</span></span> <span data-ttu-id="c00fe-118">hello Azure PowerShell 1.0 命令永遠會 「 AzureRM"hello 命令。</span><span class="sxs-lookup"><span data-stu-id="c00fe-118">hello Azure PowerShell 1.0 commands will always have "AzureRM" in hello command.</span></span>

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a><span data-ttu-id="c00fe-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="c00fe-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="c00fe-120">列出在 hello Azure 訂用帳戶或指定的資源群組中定義的所有串流分析工作，或取得資源群組內的特定作業的作業資訊。</span><span class="sxs-lookup"><span data-stu-id="c00fe-120">Lists all Stream Analytics jobs defined in hello Azure subscription or specified resource group, or gets job information about a specific job within a resource group.</span></span>

<span data-ttu-id="c00fe-121">**範例 1**</span><span class="sxs-lookup"><span data-stu-id="c00fe-121">**Example 1**</span></span>

<span data-ttu-id="c00fe-122">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-122">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob

<span data-ttu-id="c00fe-123">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-123">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob

<span data-ttu-id="c00fe-124">這個 PowerShell 命令會傳回 hello Azure 訂用帳戶中的 hello 的所有資料流分析工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c00fe-124">This PowerShell command returns information about all hello Stream Analytics jobs in hello Azure subscription.</span></span>

<span data-ttu-id="c00fe-125">**範例 2**</span><span class="sxs-lookup"><span data-stu-id="c00fe-125">**Example 2**</span></span>

<span data-ttu-id="c00fe-126">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-126">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="c00fe-127">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-127">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="c00fe-128">這個 PowerShell 命令會傳回 hello StreamAnalytics 預設中央-美國的資源群組中所有 hello 資料流分析工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c00fe-128">This PowerShell command returns information about all hello Stream Analytics jobs in hello resource group StreamAnalytics-Default-Central-US.</span></span>

<span data-ttu-id="c00fe-129">**範例 3**</span><span class="sxs-lookup"><span data-stu-id="c00fe-129">**Example 3**</span></span>

<span data-ttu-id="c00fe-130">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-130">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="c00fe-131">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-131">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="c00fe-132">這個 PowerShell 命令傳回 hello StreamAnalytics 預設中央-美國的資源群組中的 hello StreamingJob 的資料流分析工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c00fe-132">This PowerShell command returns information about hello Stream Analytics job StreamingJob in hello resource group StreamAnalytics-Default-Central-US.</span></span>

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a><span data-ttu-id="c00fe-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="c00fe-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="c00fe-134">列出所有 hello 輸入定義中指定的資料流分析工作，或取得特定的輸入的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c00fe-134">Lists all of hello inputs that are defined in a specified Stream Analytics job, or gets information about a specific input.</span></span>

<span data-ttu-id="c00fe-135">**範例 1**</span><span class="sxs-lookup"><span data-stu-id="c00fe-135">**Example 1**</span></span>

<span data-ttu-id="c00fe-136">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-136">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="c00fe-137">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-137">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="c00fe-138">此 PowerShell 命令會傳回所有 hello 輸入 hello 作業 StreamingJob 中定義的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c00fe-138">This PowerShell command returns information about all hello inputs defined in hello job StreamingJob.</span></span>

<span data-ttu-id="c00fe-139">**範例 2**</span><span class="sxs-lookup"><span data-stu-id="c00fe-139">**Example 2**</span></span>

<span data-ttu-id="c00fe-140">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-140">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="c00fe-141">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-141">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="c00fe-142">這個 PowerShell 命令會傳回名為 EntryStream hello 作業 StreamingJob 中定義的 hello 輸入相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c00fe-142">This PowerShell command returns information about hello input named EntryStream defined in hello job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a><span data-ttu-id="c00fe-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="c00fe-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="c00fe-144">列出所有 hello 輸出中指定的資料流分析工作，所定義，或取得有關特定輸出的資訊。</span><span class="sxs-lookup"><span data-stu-id="c00fe-144">Lists all of hello outputs that are defined in a specified Stream Analytics job, or gets information about a specific output.</span></span>

<span data-ttu-id="c00fe-145">**範例 1**</span><span class="sxs-lookup"><span data-stu-id="c00fe-145">**Example 1**</span></span>

<span data-ttu-id="c00fe-146">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-146">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="c00fe-147">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-147">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="c00fe-148">此 PowerShell 命令會傳回 hello 輸出 hello 作業 StreamingJob 中定義的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c00fe-148">This PowerShell command returns information about hello outputs defined in hello job StreamingJob.</span></span>

<span data-ttu-id="c00fe-149">**範例 2**</span><span class="sxs-lookup"><span data-stu-id="c00fe-149">**Example 2**</span></span>

<span data-ttu-id="c00fe-150">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-150">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="c00fe-151">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-151">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="c00fe-152">此 PowerShell 命令會傳回名為 hello 作業 StreamingJob 中定義的輸出 hello 輸出的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c00fe-152">This PowerShell command returns information about hello output named Output defined in hello job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a><span data-ttu-id="c00fe-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span><span class="sxs-lookup"><span data-stu-id="c00fe-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span></span>
<span data-ttu-id="c00fe-154">取得資料流處理單位，指定區域中的 hello 配額的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c00fe-154">Gets information about hello quota of streaming units in a specified region.</span></span>

<span data-ttu-id="c00fe-155">**範例 1**</span><span class="sxs-lookup"><span data-stu-id="c00fe-155">**Example 1**</span></span>

<span data-ttu-id="c00fe-156">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-156">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="c00fe-157">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-157">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="c00fe-158">這個 PowerShell 命令會傳回 hello 美國中部地區中的 hello 配額和使用量的資料流處理單位的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c00fe-158">This PowerShell command returns information about hello quota and usage of streaming units in hello Central US region.</span></span>

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a><span data-ttu-id="c00fe-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="c00fe-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="c00fe-160">取得在串流分析工作中定義之特定轉換的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c00fe-160">Gets information about a specific transformation defined in a Stream Analytics job.</span></span>

<span data-ttu-id="c00fe-161">**範例 1**</span><span class="sxs-lookup"><span data-stu-id="c00fe-161">**Example 1**</span></span>

<span data-ttu-id="c00fe-162">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-162">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="c00fe-163">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-163">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="c00fe-164">此 PowerShell 命令會傳回呼叫 StreamingJob hello 作業 StreamingJob 中的 hello 轉換的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c00fe-164">This PowerShell command returns information about hello transformation called StreamingJob in hello job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a><span data-ttu-id="c00fe-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="c00fe-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="c00fe-166">在串流分析工作內建立新的輸入，或更新現有的指定輸入。</span><span class="sxs-lookup"><span data-stu-id="c00fe-166">Creates a new input within a Stream Analytics job, or updates an existing specified input.</span></span>

<span data-ttu-id="c00fe-167">hello hello 輸入名稱可以指定在 hello.json 檔案或 hello 命令列。</span><span class="sxs-lookup"><span data-stu-id="c00fe-167">hello name of hello input can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="c00fe-168">如果同時指定 hello hello 命令列上的名稱必須 hello 與 hello 檔案中的 hello 一個相同。</span><span class="sxs-lookup"><span data-stu-id="c00fe-168">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="c00fe-169">如果您指定已存在的輸入，並沒有指定 hello – Force 參數，hello cmdlet 會詢問是否 tooreplace hello 現有輸入。</span><span class="sxs-lookup"><span data-stu-id="c00fe-169">If you specify an input that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing input.</span></span>

<span data-ttu-id="c00fe-170">如果您指定 hello – Force 參數，並指定現有的輸入名稱、 hello 輸入將會被取代，但不用確認。</span><span class="sxs-lookup"><span data-stu-id="c00fe-170">If you specify hello –Force parameter and specify an existing input name, hello input will be replaced without confirmation.</span></span>

<span data-ttu-id="c00fe-171">如需 hello JSON 檔案的結構與內容的詳細資訊，請參閱 toohello[建立輸入 (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-input]區段 hello[資料流分析管理 REST API參考文件庫][stream.analytics.rest.api.reference]。</span><span class="sxs-lookup"><span data-stu-id="c00fe-171">For detailed information on hello JSON file structure and contents, refer toohello [Create Input (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-input] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="c00fe-172">**範例 1**</span><span class="sxs-lookup"><span data-stu-id="c00fe-172">**Example 1**</span></span>

<span data-ttu-id="c00fe-173">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-173">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="c00fe-174">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-174">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="c00fe-175">這個 PowerShell 命令會從 hello 檔案 Input.json 建立新的輸入。</span><span class="sxs-lookup"><span data-stu-id="c00fe-175">This PowerShell command creates a new input from hello file Input.json.</span></span> <span data-ttu-id="c00fe-176">如果已經定義 hello hello 輸入的定義檔中指定的名稱與現有的輸入，hello cmdlet 會詢問是否 tooreplace 它。</span><span class="sxs-lookup"><span data-stu-id="c00fe-176">If an existing input with hello name specified in hello input definition file is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="c00fe-177">**範例 2**</span><span class="sxs-lookup"><span data-stu-id="c00fe-177">**Example 2**</span></span>

<span data-ttu-id="c00fe-178">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-178">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="c00fe-179">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-179">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="c00fe-180">這個 PowerShell 命令呼叫 EntryStream hello 作業中建立新的輸入。</span><span class="sxs-lookup"><span data-stu-id="c00fe-180">This PowerShell command creates a new input in hello job called EntryStream.</span></span> <span data-ttu-id="c00fe-181">如果已定義具有此名稱的現有輸入，hello cmdlet 會詢問是否 tooreplace 它。</span><span class="sxs-lookup"><span data-stu-id="c00fe-181">If an existing input with this name is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="c00fe-182">**範例 3**</span><span class="sxs-lookup"><span data-stu-id="c00fe-182">**Example 3**</span></span>

<span data-ttu-id="c00fe-183">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-183">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="c00fe-184">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-184">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="c00fe-185">這個 PowerShell 命令會取代現有 hello 與 hello 檔案中的 hello 定義稱為 EntryStream 輸入來源的 hello 定義。</span><span class="sxs-lookup"><span data-stu-id="c00fe-185">This PowerShell command replaces hello definition of hello existing input source called EntryStream with hello definition from hello file.</span></span>

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a><span data-ttu-id="c00fe-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="c00fe-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="c00fe-187">在 Microsoft Azure 中建立新的資料流分析工作，或更新現有的指定工作的 hello 定義。</span><span class="sxs-lookup"><span data-stu-id="c00fe-187">Creates a new Stream Analytics job in Microsoft Azure, or updates hello definition of an existing specified job.</span></span>

<span data-ttu-id="c00fe-188">hello.json 檔案中或 hello 命令列上，可以指定 hello hello 作業名稱。</span><span class="sxs-lookup"><span data-stu-id="c00fe-188">hello name of hello job can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="c00fe-189">如果同時指定 hello hello 命令列上的名稱必須 hello 與 hello 檔案中的 hello 一個相同。</span><span class="sxs-lookup"><span data-stu-id="c00fe-189">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="c00fe-190">如果您指定工作名稱已存在且未指定 hello – Force 參數，hello cmdlet 會詢問是否 tooreplace hello 現有的工作。</span><span class="sxs-lookup"><span data-stu-id="c00fe-190">If you specify a job name that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing job.</span></span>

<span data-ttu-id="c00fe-191">如果您指定 hello – Force 參數，並指定現有的作業名稱，將取代 hello 工作定義，但不用確認。</span><span class="sxs-lookup"><span data-stu-id="c00fe-191">If you specify hello –Force parameter and specify an existing job name, hello job definition will be replaced without confirmation.</span></span>

<span data-ttu-id="c00fe-192">如需 hello JSON 檔案的結構與內容的詳細資訊，請參閱 toohello[建立串流分析工作][ msdn-rest-api-create-stream-analytics-job]區段 hello [Stream Analytics Management REST API 參考程式庫][stream.analytics.rest.api.reference]。</span><span class="sxs-lookup"><span data-stu-id="c00fe-192">For detailed information on hello JSON file structure and contents, refer toohello [Create Stream Analytics Job][msdn-rest-api-create-stream-analytics-job] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="c00fe-193">**範例 1**</span><span class="sxs-lookup"><span data-stu-id="c00fe-193">**Example 1**</span></span>

<span data-ttu-id="c00fe-194">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-194">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="c00fe-195">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-195">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="c00fe-196">這個 PowerShell 命令會從 JobDefinition.json 中的 hello 定義建立新的工作。</span><span class="sxs-lookup"><span data-stu-id="c00fe-196">This PowerShell command creates a new job from hello definition in JobDefinition.json.</span></span> <span data-ttu-id="c00fe-197">如果已經定義 hello hello 工作定義檔中指定的名稱與現有的工作，hello cmdlet 會詢問是否 tooreplace 它。</span><span class="sxs-lookup"><span data-stu-id="c00fe-197">If an existing job with hello name specified in hello job definition file is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="c00fe-198">**範例 2**</span><span class="sxs-lookup"><span data-stu-id="c00fe-198">**Example 2**</span></span>

<span data-ttu-id="c00fe-199">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-199">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="c00fe-200">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-200">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="c00fe-201">這個 PowerShell 命令會取代 StreamingJob 的 hello 工作定義。</span><span class="sxs-lookup"><span data-stu-id="c00fe-201">This PowerShell command replaces hello job definition for StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a><span data-ttu-id="c00fe-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="c00fe-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="c00fe-203">在串流分析工作內建立新的輸出，或更新現有的輸出。</span><span class="sxs-lookup"><span data-stu-id="c00fe-203">Creates a new output within a Stream Analytics job, or updates an existing output.</span></span>  

<span data-ttu-id="c00fe-204">hello.json 檔案中或 hello 命令列上，可以指定 hello hello 輸出名稱。</span><span class="sxs-lookup"><span data-stu-id="c00fe-204">hello name of hello output can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="c00fe-205">如果同時指定 hello hello 命令列上的名稱必須 hello 與 hello 檔案中的 hello 一個相同。</span><span class="sxs-lookup"><span data-stu-id="c00fe-205">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="c00fe-206">如果您指定已存在的輸出，且未指定 hello – Force 參數，hello cmdlet 會詢問是否 tooreplace hello 現有的輸出。</span><span class="sxs-lookup"><span data-stu-id="c00fe-206">If you specify an output that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing output.</span></span>

<span data-ttu-id="c00fe-207">如果您指定 hello – Force 參數，並指定現有的輸出名稱、 hello 輸出將會被取代，但不用確認。</span><span class="sxs-lookup"><span data-stu-id="c00fe-207">If you specify hello –Force parameter and specify an existing output name, hello output will be replaced without confirmation.</span></span>

<span data-ttu-id="c00fe-208">如需 hello JSON 檔案的結構與內容的詳細資訊，請參閱 toohello[建立輸出 (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-output]區段 hello[資料流分析管理 REST API參考文件庫][stream.analytics.rest.api.reference]。</span><span class="sxs-lookup"><span data-stu-id="c00fe-208">For detailed information on hello JSON file structure and contents, refer toohello [Create Output (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-output] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="c00fe-209">**範例 1**</span><span class="sxs-lookup"><span data-stu-id="c00fe-209">**Example 1**</span></span>

<span data-ttu-id="c00fe-210">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-210">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="c00fe-211">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-211">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="c00fe-212">這個 PowerShell 命令建立新的輸出 hello 作業 StreamingJob 中稱為 「 輸出 」。</span><span class="sxs-lookup"><span data-stu-id="c00fe-212">This PowerShell command creates a new output called "output" in hello job StreamingJob.</span></span> <span data-ttu-id="c00fe-213">如果已定義具有此名稱的現有輸出，hello cmdlet 會詢問是否 tooreplace 它。</span><span class="sxs-lookup"><span data-stu-id="c00fe-213">If an existing output with this name is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="c00fe-214">**範例 2**</span><span class="sxs-lookup"><span data-stu-id="c00fe-214">**Example 2**</span></span>

<span data-ttu-id="c00fe-215">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-215">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="c00fe-216">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-216">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="c00fe-217">這個 PowerShell 命令會取代 「 輸出 」 hello 作業 StreamingJob 中的 hello 定義。</span><span class="sxs-lookup"><span data-stu-id="c00fe-217">This PowerShell command replaces hello definition for "output" in hello job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a><span data-ttu-id="c00fe-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="c00fe-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="c00fe-219">建立新的轉換資料流分析工作內，或更新現有 hello 的轉換。</span><span class="sxs-lookup"><span data-stu-id="c00fe-219">Creates a new transformation within a Stream Analytics job, or updates hello existing transformation.</span></span>

<span data-ttu-id="c00fe-220">hello.json 檔案中或 hello 命令列上，則可以指定 hello 轉換 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="c00fe-220">hello name of hello transformation can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="c00fe-221">如果同時指定 hello hello 命令列上的名稱必須 hello 與 hello 檔案中的 hello 一個相同。</span><span class="sxs-lookup"><span data-stu-id="c00fe-221">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="c00fe-222">如果您指定的轉換已經存在，且未指定 hello – Force 參數，hello cmdlet 會詢問是否 tooreplace hello 現有的轉換。</span><span class="sxs-lookup"><span data-stu-id="c00fe-222">If you specify a transformation that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing transformation.</span></span>

<span data-ttu-id="c00fe-223">如果您指定 hello – Force 參數，並指定現有的轉換名稱，將取代 hello 轉換，但不用確認。</span><span class="sxs-lookup"><span data-stu-id="c00fe-223">If you specify hello –Force parameter and specify an existing transformation name, hello transformation will be replaced without confirmation.</span></span>

<span data-ttu-id="c00fe-224">如需 hello JSON 檔案的結構與內容的詳細資訊，請參閱 toohello[建立轉換 (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-transformation] hello 區段[資料流分析管理REST API 參考文件庫][stream.analytics.rest.api.reference]。</span><span class="sxs-lookup"><span data-stu-id="c00fe-224">For detailed information on hello JSON file structure and contents, refer toohello [Create Transformation (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-transformation] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="c00fe-225">**範例 1**</span><span class="sxs-lookup"><span data-stu-id="c00fe-225">**Example 1**</span></span>

<span data-ttu-id="c00fe-226">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-226">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="c00fe-227">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-227">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="c00fe-228">這個 PowerShell 命令建立新的轉換稱為 StreamingJobTransform hello 作業 StreamingJob 中。</span><span class="sxs-lookup"><span data-stu-id="c00fe-228">This PowerShell command creates a new transformation called StreamingJobTransform in hello job StreamingJob.</span></span> <span data-ttu-id="c00fe-229">如果現有的轉換已經定義此名稱，hello cmdlet 會詢問是否 tooreplace 它。</span><span class="sxs-lookup"><span data-stu-id="c00fe-229">If an existing transformation is already defined with this name, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="c00fe-230">**範例 2**</span><span class="sxs-lookup"><span data-stu-id="c00fe-230">**Example 2**</span></span>

<span data-ttu-id="c00fe-231">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-231">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

<span data-ttu-id="c00fe-232">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-232">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 <span data-ttu-id="c00fe-233">這個 PowerShell 命令會取代在 hello 工作 StreamingJob StreamingJobTransform hello 定義。</span><span class="sxs-lookup"><span data-stu-id="c00fe-233">This PowerShell command replaces hello definition of StreamingJobTransform in hello job StreamingJob.</span></span>

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a><span data-ttu-id="c00fe-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="c00fe-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="c00fe-235">以非同步方式從 Microsoft Azure 中的 Stream Analytics 作業刪除特定的輸入。</span><span class="sxs-lookup"><span data-stu-id="c00fe-235">Asynchronously deletes a specific input from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="c00fe-236">如果您指定 hello – Force 參數，輸入 hello 將會刪除但不用確認。</span><span class="sxs-lookup"><span data-stu-id="c00fe-236">If you specify hello –Force parameter, hello input will be deleted without confirmation.</span></span>

<span data-ttu-id="c00fe-237">**範例 1**</span><span class="sxs-lookup"><span data-stu-id="c00fe-237">**Example 1**</span></span>

<span data-ttu-id="c00fe-238">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-238">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="c00fe-239">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-239">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="c00fe-240">這個 PowerShell 命令，移除 hello 輸入的 EventStream hello 作業 StreamingJob 中。</span><span class="sxs-lookup"><span data-stu-id="c00fe-240">This PowerShell command removes hello input EventStream in hello job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a><span data-ttu-id="c00fe-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="c00fe-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="c00fe-242">以非同步方式從 Microsoft Azure 中刪除特定的 Stream Analytics 作業。</span><span class="sxs-lookup"><span data-stu-id="c00fe-242">Asynchronously deletes a specific Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="c00fe-243">如果您指定 hello – Force 參數，hello 作業將會刪除但不用確認。</span><span class="sxs-lookup"><span data-stu-id="c00fe-243">If you specify hello –Force parameter, hello job will be deleted without confirmation.</span></span>

<span data-ttu-id="c00fe-244">**範例 1**</span><span class="sxs-lookup"><span data-stu-id="c00fe-244">**Example 1**</span></span>

<span data-ttu-id="c00fe-245">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-245">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="c00fe-246">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-246">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="c00fe-247">這個 PowerShell 命令移除 hello 作業 StreamingJob。</span><span class="sxs-lookup"><span data-stu-id="c00fe-247">This PowerShell command removes hello job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a><span data-ttu-id="c00fe-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="c00fe-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="c00fe-249">以非同步方式從 Microsoft Azure 中的 Stream Analytics 作業刪除特定的輸出。</span><span class="sxs-lookup"><span data-stu-id="c00fe-249">Asynchronously deletes a specific output from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="c00fe-250">如果您指定 hello – Force 參數，hello 輸出將會刪除但不用確認。</span><span class="sxs-lookup"><span data-stu-id="c00fe-250">If you specify hello –Force parameter, hello output will be deleted without confirmation.</span></span>

<span data-ttu-id="c00fe-251">**範例 1**</span><span class="sxs-lookup"><span data-stu-id="c00fe-251">**Example 1**</span></span>

<span data-ttu-id="c00fe-252">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-252">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="c00fe-253">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-253">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="c00fe-254">此 PowerShell 命令移除 hello hello 作業 StreamingJob 中輸出輸出。</span><span class="sxs-lookup"><span data-stu-id="c00fe-254">This PowerShell command removes hello output Output in hello job StreamingJob.</span></span>  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a><span data-ttu-id="c00fe-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="c00fe-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="c00fe-256">以非同步方式部署和啟動 Microsoft Azure 中的 Stream Analytics 作業。</span><span class="sxs-lookup"><span data-stu-id="c00fe-256">Asynchronously deploys and starts a Stream Analytics job in Microsoft Azure.</span></span>

<span data-ttu-id="c00fe-257">**範例 1**</span><span class="sxs-lookup"><span data-stu-id="c00fe-257">**Example 1**</span></span>

<span data-ttu-id="c00fe-258">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-258">Azure PowerShell 0.9.8:</span></span>  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="c00fe-259">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-259">Azure PowerShell 1.0:</span></span>  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="c00fe-260">這個 PowerShell 命令，開始 hello 的作業 StreamingJob 自訂輸出的開始時間設定 tooDecember 12，2012，12:12:12 UTC。</span><span class="sxs-lookup"><span data-stu-id="c00fe-260">This PowerShell command starts hello job StreamingJob with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC.</span></span>

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a><span data-ttu-id="c00fe-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="c00fe-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="c00fe-262">以非同步方式停止在 Microsoft Azure 中執行 Stream Analytics 作業，並取消配置正在使用的資源。</span><span class="sxs-lookup"><span data-stu-id="c00fe-262">Asynchronously stops a Stream Analytics job from running in Microsoft Azure and de-allocates resources that were that were being used.</span></span> <span data-ttu-id="c00fe-263">hello 工作定義和中繼資料依然會有效 hello Azure 入口網站和管理 Api，透過您訂用帳戶內，hello 作業可以編輯和重新啟動。</span><span class="sxs-lookup"><span data-stu-id="c00fe-263">hello job definition and metadata will remain available within your subscription through both hello Azure portal and management APIs, such that hello job can be edited and restarted.</span></span> <span data-ttu-id="c00fe-264">您不被支付 hello 停止狀態中的工作。</span><span class="sxs-lookup"><span data-stu-id="c00fe-264">You will not be charged for a job in hello stopped state.</span></span>

<span data-ttu-id="c00fe-265">**範例 1**</span><span class="sxs-lookup"><span data-stu-id="c00fe-265">**Example 1**</span></span>

<span data-ttu-id="c00fe-266">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-266">Azure PowerShell 0.9.8:</span></span>  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="c00fe-267">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-267">Azure PowerShell 1.0:</span></span>  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="c00fe-268">這個 PowerShell 命令停止 hello 工作 StreamingJob。</span><span class="sxs-lookup"><span data-stu-id="c00fe-268">This PowerShell command stops hello job StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a><span data-ttu-id="c00fe-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="c00fe-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="c00fe-270">測試資料流分析 tooconnect tooa hello 能力指定輸入。</span><span class="sxs-lookup"><span data-stu-id="c00fe-270">Tests hello ability of Stream Analytics tooconnect tooa specified input.</span></span>

<span data-ttu-id="c00fe-271">**範例 1**</span><span class="sxs-lookup"><span data-stu-id="c00fe-271">**Example 1**</span></span>

<span data-ttu-id="c00fe-272">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-272">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="c00fe-273">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-273">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="c00fe-274">此 PowerShell 命令測試 hello 連線狀態的 hello 輸入 EntryStream StreamingJob 中的。</span><span class="sxs-lookup"><span data-stu-id="c00fe-274">This PowerShell command tests hello connection status of hello input EntryStream in StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a><span data-ttu-id="c00fe-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="c00fe-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="c00fe-276">測試資料流分析 tooconnect tooa hello 能力指定輸出。</span><span class="sxs-lookup"><span data-stu-id="c00fe-276">Tests hello ability of Stream Analytics tooconnect tooa specified output.</span></span>

<span data-ttu-id="c00fe-277">**範例 1**</span><span class="sxs-lookup"><span data-stu-id="c00fe-277">**Example 1**</span></span>

<span data-ttu-id="c00fe-278">Azure PowerShell 0.9.8：</span><span class="sxs-lookup"><span data-stu-id="c00fe-278">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="c00fe-279">Azure PowerShell 1.0：</span><span class="sxs-lookup"><span data-stu-id="c00fe-279">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="c00fe-280">此 PowerShell 命令測試 hello 連線狀態的 hello 輸出 StreamingJob 中的輸出。</span><span class="sxs-lookup"><span data-stu-id="c00fe-280">This PowerShell command tests hello connection status of hello output Output in StreamingJob.</span></span>  

## <a name="get-support"></a><span data-ttu-id="c00fe-281">取得支援</span><span class="sxs-lookup"><span data-stu-id="c00fe-281">Get support</span></span>
<span data-ttu-id="c00fe-282">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="c00fe-282">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c00fe-283">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c00fe-283">Next steps</span></span>
* [<span data-ttu-id="c00fe-284">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="c00fe-284">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c00fe-285">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c00fe-285">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="c00fe-286">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="c00fe-286">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="c00fe-287">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="c00fe-287">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c00fe-288">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="c00fe-288">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

