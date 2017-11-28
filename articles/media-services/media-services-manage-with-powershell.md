---
title: "aaaManage 使用 PowerShell 的 Azure 媒體服務帳戶"
description: "了解如何 toomanage Azure Media Services 帳戶的 PowerShell cmdlet。"
author: Juliako
manager: erikre
editor: 
services: media-services
documentationcenter: 
ms.assetid: 17a10c25-d94f-421c-b6bc-ae0958e2ac96
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: juliako
ms.openlocfilehash: e8f97bb2393343e45fabf9c437b4fc09f2525dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a><span data-ttu-id="b817a-103">利用 PowerShell 管理 Azure Media Services 帳戶</span><span class="sxs-lookup"><span data-stu-id="b817a-103">Manage Azure Media Services Accounts with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b817a-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="b817a-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="b817a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b817a-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="b817a-106">REST</span><span class="sxs-lookup"><span data-stu-id="b817a-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="b817a-107">toobe 無法 toocreate Azure Media Services 帳戶，您必須有 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b817a-107">toobe able toocreate an Azure Media Services account, you must have an Azure account.</span></span> <span data-ttu-id="b817a-108">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b817a-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b817a-109">如需詳細資料，請參閱 <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure 免費試用</a>。</span><span class="sxs-lookup"><span data-stu-id="b817a-109">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="b817a-110">概觀</span><span class="sxs-lookup"><span data-stu-id="b817a-110">Overview</span></span>
<span data-ttu-id="b817a-111">本文列出 hello Azure PowerShell cmdlet 的 Azure 媒體服務 (AMS) hello Azure Resource Manager 架構中。</span><span class="sxs-lookup"><span data-stu-id="b817a-111">This article lists hello Azure PowerShell cmdlets for Azure Media Services (AMS) in hello Azure Resource Manager framework.</span></span> <span data-ttu-id="b817a-112">hello cmdlet 存在於 hello **Microsoft.Azure.Commands.Media**命名空間。</span><span class="sxs-lookup"><span data-stu-id="b817a-112">hello cmdlets exist in hello **Microsoft.Azure.Commands.Media** namespace.</span></span>

## <a name="versions"></a><span data-ttu-id="b817a-113">版本</span><span class="sxs-lookup"><span data-stu-id="b817a-113">Versions</span></span>
<span data-ttu-id="b817a-114">**ApiVersion**："2015-10-01"</span><span class="sxs-lookup"><span data-stu-id="b817a-114">**ApiVersion**:   "2015-10-01"</span></span>

## <a name="new-azurermmediaservice"></a><span data-ttu-id="b817a-115">New-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="b817a-115">New-AzureRmMediaService</span></span>
<span data-ttu-id="b817a-116">建立媒體服務。</span><span class="sxs-lookup"><span data-stu-id="b817a-116">Creates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="b817a-117">語法</span><span class="sxs-lookup"><span data-stu-id="b817a-117">Syntax</span></span>
<span data-ttu-id="b817a-118">參數集︰StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="b817a-118">Parameter Set: StorageAccountIdParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

<span data-ttu-id="b817a-119">參數集︰StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="b817a-119">Parameter Set: StorageAccountsParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="b817a-120">參數</span><span class="sxs-lookup"><span data-stu-id="b817a-120">Parameters</span></span>
<span data-ttu-id="b817a-121">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-121">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="b817a-122">指定此媒體服務所屬的 hello 資源群組 toowhich hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="b817a-122">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="b817a-123">別名</span><span class="sxs-lookup"><span data-stu-id="b817a-123">Aliases</span></span> | <span data-ttu-id="b817a-124">無</span><span class="sxs-lookup"><span data-stu-id="b817a-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="b817a-125">必要？</span><span class="sxs-lookup"><span data-stu-id="b817a-125">Required?</span></span> |<span data-ttu-id="b817a-126">true</span><span class="sxs-lookup"><span data-stu-id="b817a-126">true</span></span> |
| <span data-ttu-id="b817a-127">位置？</span><span class="sxs-lookup"><span data-stu-id="b817a-127">Position?</span></span> |<span data-ttu-id="b817a-128">0</span><span class="sxs-lookup"><span data-stu-id="b817a-128">0</span></span> |
| <span data-ttu-id="b817a-129">預設值</span><span class="sxs-lookup"><span data-stu-id="b817a-129">Default value</span></span> |<span data-ttu-id="b817a-130">無</span><span class="sxs-lookup"><span data-stu-id="b817a-130">none</span></span> |
| <span data-ttu-id="b817a-131">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="b817a-131">Accept pipeline input?</span></span> |<span data-ttu-id="b817a-132">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b817a-132">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b817a-133">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="b817a-133">Accept wildcard characters?</span></span> |<span data-ttu-id="b817a-134">false</span><span class="sxs-lookup"><span data-stu-id="b817a-134">false</span></span> |

<span data-ttu-id="b817a-135">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-135">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="b817a-136">指定 hello hello 媒體服務名稱。</span><span class="sxs-lookup"><span data-stu-id="b817a-136">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="b817a-137">別名</span><span class="sxs-lookup"><span data-stu-id="b817a-137">Aliases</span></span> | <span data-ttu-id="b817a-138">Name</span><span class="sxs-lookup"><span data-stu-id="b817a-138">Name</span></span> |
| --- | --- |
| <span data-ttu-id="b817a-139">必要？</span><span class="sxs-lookup"><span data-stu-id="b817a-139">Required?</span></span> |<span data-ttu-id="b817a-140">true</span><span class="sxs-lookup"><span data-stu-id="b817a-140">true</span></span> |
| <span data-ttu-id="b817a-141">位置？</span><span class="sxs-lookup"><span data-stu-id="b817a-141">Position?</span></span> |<span data-ttu-id="b817a-142">1</span><span class="sxs-lookup"><span data-stu-id="b817a-142">1</span></span> |
| <span data-ttu-id="b817a-143">預設值</span><span class="sxs-lookup"><span data-stu-id="b817a-143">Default value</span></span> |<span data-ttu-id="b817a-144">無</span><span class="sxs-lookup"><span data-stu-id="b817a-144">none</span></span> |
| <span data-ttu-id="b817a-145">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="b817a-145">Accept pipeline input?</span></span> |<span data-ttu-id="b817a-146">false</span><span class="sxs-lookup"><span data-stu-id="b817a-146">false</span></span> |
| <span data-ttu-id="b817a-147">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="b817a-147">Accept wildcard characters?</span></span> |<span data-ttu-id="b817a-148">false</span><span class="sxs-lookup"><span data-stu-id="b817a-148">false</span></span> |

<span data-ttu-id="b817a-149">**-Location &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-149">**-Location &lt;String&gt;**</span></span>

<span data-ttu-id="b817a-150">指定 hello 媒體服務的 hello 資源的位置。</span><span class="sxs-lookup"><span data-stu-id="b817a-150">Specifies hello resource location of hello media service.</span></span>

| <span data-ttu-id="b817a-151">別名</span><span class="sxs-lookup"><span data-stu-id="b817a-151">Aliases</span></span> | <span data-ttu-id="b817a-152">無</span><span class="sxs-lookup"><span data-stu-id="b817a-152">none</span></span> |
| --- | --- |
| <span data-ttu-id="b817a-153">必要？</span><span class="sxs-lookup"><span data-stu-id="b817a-153">Required?</span></span> |<span data-ttu-id="b817a-154">true</span><span class="sxs-lookup"><span data-stu-id="b817a-154">true</span></span> |
| <span data-ttu-id="b817a-155">位置？</span><span class="sxs-lookup"><span data-stu-id="b817a-155">Position?</span></span> |<span data-ttu-id="b817a-156">2</span><span class="sxs-lookup"><span data-stu-id="b817a-156">2</span></span> |
| <span data-ttu-id="b817a-157">預設值</span><span class="sxs-lookup"><span data-stu-id="b817a-157">Default value</span></span> |<span data-ttu-id="b817a-158">無</span><span class="sxs-lookup"><span data-stu-id="b817a-158">none</span></span> |
| <span data-ttu-id="b817a-159">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="b817a-159">Accept pipeline input?</span></span> |<span data-ttu-id="b817a-160">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b817a-160">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b817a-161">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="b817a-161">Accept wildcard characters?</span></span> |<span data-ttu-id="b817a-162">false</span><span class="sxs-lookup"><span data-stu-id="b817a-162">false</span></span> |

<span data-ttu-id="b817a-163">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-163">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="b817a-164">指定與 hello 媒體服務相關聯的主要儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b817a-164">Specifies a primary storage account that associated with hello media service.</span></span>

* <span data-ttu-id="b817a-165">新建立儲存體帳戶 （以 hello 資源管理員 API） 才支援。</span><span class="sxs-lookup"><span data-stu-id="b817a-165">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="b817a-166">hello 儲存體帳戶必須存在，且具有 hello 與 hello 媒體服務的相同位置。</span><span class="sxs-lookup"><span data-stu-id="b817a-166">hello storage account must exist and has hello same location with hello media service.</span></span>

| <span data-ttu-id="b817a-167">別名</span><span class="sxs-lookup"><span data-stu-id="b817a-167">Aliases</span></span> | <span data-ttu-id="b817a-168">無</span><span class="sxs-lookup"><span data-stu-id="b817a-168">none</span></span> |
| --- | --- |
| <span data-ttu-id="b817a-169">必要？</span><span class="sxs-lookup"><span data-stu-id="b817a-169">Required?</span></span> |<span data-ttu-id="b817a-170">true</span><span class="sxs-lookup"><span data-stu-id="b817a-170">true</span></span> |
| <span data-ttu-id="b817a-171">位置？</span><span class="sxs-lookup"><span data-stu-id="b817a-171">Position?</span></span> |<span data-ttu-id="b817a-172">3</span><span class="sxs-lookup"><span data-stu-id="b817a-172">3</span></span> |
| <span data-ttu-id="b817a-173">預設值</span><span class="sxs-lookup"><span data-stu-id="b817a-173">Default value</span></span> |<span data-ttu-id="b817a-174">無</span><span class="sxs-lookup"><span data-stu-id="b817a-174">none</span></span> |
| <span data-ttu-id="b817a-175">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="b817a-175">Accept pipeline input?</span></span> |<span data-ttu-id="b817a-176">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b817a-176">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b817a-177">參數集名稱</span><span class="sxs-lookup"><span data-stu-id="b817a-177">Parameter set name</span></span> |<span data-ttu-id="b817a-178">StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="b817a-178">StorageAccountIdParamSet</span></span> |
| <span data-ttu-id="b817a-179">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="b817a-179">Accept wildcard characters?</span></span> |<span data-ttu-id="b817a-180">false</span><span class="sxs-lookup"><span data-stu-id="b817a-180">false</span></span> |

<span data-ttu-id="b817a-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="b817a-182">指定與 hello 媒體服務相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b817a-182">Specifies storage accounts that associated with hello media service.</span></span>

* <span data-ttu-id="b817a-183">新建立儲存體帳戶 （以 hello 資源管理員 API） 才支援。</span><span class="sxs-lookup"><span data-stu-id="b817a-183">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="b817a-184">hello 儲存體帳戶必須存在，且具有 hello 與 hello 媒體服務的相同位置。</span><span class="sxs-lookup"><span data-stu-id="b817a-184">hello storage account must exist and has hello same location with hello media service.</span></span>
* <span data-ttu-id="b817a-185">只可以指定一個主要儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b817a-185">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="b817a-186">別名</span><span class="sxs-lookup"><span data-stu-id="b817a-186">Aliases</span></span> | <span data-ttu-id="b817a-187">無</span><span class="sxs-lookup"><span data-stu-id="b817a-187">none</span></span> |
| --- | --- |
| <span data-ttu-id="b817a-188">必要？</span><span class="sxs-lookup"><span data-stu-id="b817a-188">Required?</span></span> |<span data-ttu-id="b817a-189">true</span><span class="sxs-lookup"><span data-stu-id="b817a-189">true</span></span> |
| <span data-ttu-id="b817a-190">位置？</span><span class="sxs-lookup"><span data-stu-id="b817a-190">Position?</span></span> |<span data-ttu-id="b817a-191">3</span><span class="sxs-lookup"><span data-stu-id="b817a-191">3</span></span> |
| <span data-ttu-id="b817a-192">預設值</span><span class="sxs-lookup"><span data-stu-id="b817a-192">Default value</span></span> |<span data-ttu-id="b817a-193">無</span><span class="sxs-lookup"><span data-stu-id="b817a-193">none</span></span> |
| <span data-ttu-id="b817a-194">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="b817a-194">Accept pipeline input?</span></span> |<span data-ttu-id="b817a-195">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b817a-195">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b817a-196">參數集名稱</span><span class="sxs-lookup"><span data-stu-id="b817a-196">Parameter set name</span></span> |<span data-ttu-id="b817a-197">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="b817a-197">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="b817a-198">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="b817a-198">Accept wildcard characters?</span></span> |<span data-ttu-id="b817a-199">false</span><span class="sxs-lookup"><span data-stu-id="b817a-199">false</span></span> |

<span data-ttu-id="b817a-200">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-200">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="b817a-201">指定雜湊表的 hello 與 hello 媒體服務相關聯的標記。</span><span class="sxs-lookup"><span data-stu-id="b817a-201">Specifies a hash table of hello tags that are associated with hello media service.</span></span>

* <span data-ttu-id="b817a-202">範例: @{"標籤 1"="value1";"標籤 2 」 =: value2"}</span><span class="sxs-lookup"><span data-stu-id="b817a-202">Example: @{"tag1"="value1";"tag2"=:value2"}</span></span>

| <span data-ttu-id="b817a-203">別名</span><span class="sxs-lookup"><span data-stu-id="b817a-203">Aliases</span></span> | <span data-ttu-id="b817a-204">無</span><span class="sxs-lookup"><span data-stu-id="b817a-204">none</span></span> |
| --- | --- |
| <span data-ttu-id="b817a-205">必要？</span><span class="sxs-lookup"><span data-stu-id="b817a-205">Required?</span></span> |<span data-ttu-id="b817a-206">false</span><span class="sxs-lookup"><span data-stu-id="b817a-206">false</span></span> |
| <span data-ttu-id="b817a-207">位置？</span><span class="sxs-lookup"><span data-stu-id="b817a-207">Position?</span></span> |<span data-ttu-id="b817a-208">已命名</span><span class="sxs-lookup"><span data-stu-id="b817a-208">named</span></span> |
| <span data-ttu-id="b817a-209">預設值</span><span class="sxs-lookup"><span data-stu-id="b817a-209">Default value</span></span> |<span data-ttu-id="b817a-210">無</span><span class="sxs-lookup"><span data-stu-id="b817a-210">none</span></span> |
| <span data-ttu-id="b817a-211">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="b817a-211">Accept pipeline input?</span></span> |<span data-ttu-id="b817a-212">false</span><span class="sxs-lookup"><span data-stu-id="b817a-212">false</span></span> |
| <span data-ttu-id="b817a-213">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="b817a-213">Accept wildcard characters?</span></span> |<span data-ttu-id="b817a-214">false</span><span class="sxs-lookup"><span data-stu-id="b817a-214">false</span></span> |

<span data-ttu-id="b817a-215">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-215">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="b817a-216">這個 cmdlet 支援 hello 一般參數:-偵錯、-ErrorAction、-ErrorVariable、-InformationAction、-InformationVariable、-OutVariable、-OutBuffer、-PipelineVariable、-Verbose、-WarningAction 以及-WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="b817a-216">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="b817a-217">輸入</span><span class="sxs-lookup"><span data-stu-id="b817a-217">Inputs</span></span>
<span data-ttu-id="b817a-218">hello 輸入型別是 hello hello 型別物件，您可以使用管線傳送 toohello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b817a-218">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="b817a-219">輸出</span><span class="sxs-lookup"><span data-stu-id="b817a-219">Outputs</span></span>
<span data-ttu-id="b817a-220">hello 輸出類型是 hello hello cmdlet 的 hello 物件型別會發出。</span><span class="sxs-lookup"><span data-stu-id="b817a-220">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="set-azurermmediaservice"></a><span data-ttu-id="b817a-221">Set-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="b817a-221">Set-AzureRmMediaService</span></span>
<span data-ttu-id="b817a-222">更新媒體服務。</span><span class="sxs-lookup"><span data-stu-id="b817a-222">Updates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="b817a-223">語法</span><span class="sxs-lookup"><span data-stu-id="b817a-223">Syntax</span></span>
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="b817a-224">參數</span><span class="sxs-lookup"><span data-stu-id="b817a-224">Parameters</span></span>
<span data-ttu-id="b817a-225">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-225">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="b817a-226">指定此媒體服務所屬的 hello 資源群組 toowhich hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="b817a-226">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="b817a-227">別名</span><span class="sxs-lookup"><span data-stu-id="b817a-227">Aliases</span></span> | <span data-ttu-id="b817a-228">無</span><span class="sxs-lookup"><span data-stu-id="b817a-228">none</span></span> |
| --- | --- |
| <span data-ttu-id="b817a-229">必要？</span><span class="sxs-lookup"><span data-stu-id="b817a-229">Required?</span></span> |<span data-ttu-id="b817a-230">true</span><span class="sxs-lookup"><span data-stu-id="b817a-230">true</span></span> |
| <span data-ttu-id="b817a-231">位置？</span><span class="sxs-lookup"><span data-stu-id="b817a-231">Position?</span></span> |<span data-ttu-id="b817a-232">0</span><span class="sxs-lookup"><span data-stu-id="b817a-232">0</span></span> |
| <span data-ttu-id="b817a-233">預設值</span><span class="sxs-lookup"><span data-stu-id="b817a-233">Default Value</span></span> |<span data-ttu-id="b817a-234">無</span><span class="sxs-lookup"><span data-stu-id="b817a-234">none</span></span> |
| <span data-ttu-id="b817a-235">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="b817a-235">Accept Pipeline Input?</span></span> |<span data-ttu-id="b817a-236">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b817a-236">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b817a-237">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="b817a-237">Accept wildcard characters?</span></span> |<span data-ttu-id="b817a-238">false</span><span class="sxs-lookup"><span data-stu-id="b817a-238">false</span></span> |

<span data-ttu-id="b817a-239">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-239">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="b817a-240">指定 hello hello 媒體服務名稱。</span><span class="sxs-lookup"><span data-stu-id="b817a-240">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="b817a-241">別名</span><span class="sxs-lookup"><span data-stu-id="b817a-241">Aliases</span></span> | <span data-ttu-id="b817a-242">Name</span><span class="sxs-lookup"><span data-stu-id="b817a-242">Name</span></span> |
| --- | --- |
| <span data-ttu-id="b817a-243">必要？</span><span class="sxs-lookup"><span data-stu-id="b817a-243">Required?</span></span> |<span data-ttu-id="b817a-244">true</span><span class="sxs-lookup"><span data-stu-id="b817a-244">True</span></span> |
| <span data-ttu-id="b817a-245">位置？</span><span class="sxs-lookup"><span data-stu-id="b817a-245">Position?</span></span> |<span data-ttu-id="b817a-246">1</span><span class="sxs-lookup"><span data-stu-id="b817a-246">1</span></span> |
| <span data-ttu-id="b817a-247">預設值</span><span class="sxs-lookup"><span data-stu-id="b817a-247">Default value</span></span> |<span data-ttu-id="b817a-248">無</span><span class="sxs-lookup"><span data-stu-id="b817a-248">None</span></span> |
| <span data-ttu-id="b817a-249">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="b817a-249">Accept pipeline input?</span></span> |<span data-ttu-id="b817a-250">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b817a-250">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b817a-251">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="b817a-251">Accept wildcard characters?</span></span> |<span data-ttu-id="b817a-252">False</span><span class="sxs-lookup"><span data-stu-id="b817a-252">False</span></span> |

<span data-ttu-id="b817a-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="b817a-254">指定與 hello 媒體服務相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b817a-254">Specifies storage accounts that associated with hello media service.</span></span>

* <span data-ttu-id="b817a-255">新建立儲存體帳戶 （以 hello 資源管理員 API） 才支援。</span><span class="sxs-lookup"><span data-stu-id="b817a-255">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="b817a-256">hello 儲存體帳戶必須存在，且具有 hello 與 hello 媒體服務的相同位置。</span><span class="sxs-lookup"><span data-stu-id="b817a-256">hello storage account must exist and has hello same location with hello media service.</span></span>
* <span data-ttu-id="b817a-257">只可以指定一個主要儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b817a-257">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="b817a-258">別名</span><span class="sxs-lookup"><span data-stu-id="b817a-258">Aliases</span></span> | <span data-ttu-id="b817a-259">無</span><span class="sxs-lookup"><span data-stu-id="b817a-259">none</span></span> |
| --- | --- |
| <span data-ttu-id="b817a-260">必要？</span><span class="sxs-lookup"><span data-stu-id="b817a-260">Required?</span></span> |<span data-ttu-id="b817a-261">false</span><span class="sxs-lookup"><span data-stu-id="b817a-261">false</span></span> |
| <span data-ttu-id="b817a-262">位置？</span><span class="sxs-lookup"><span data-stu-id="b817a-262">Position?</span></span> |<span data-ttu-id="b817a-263">已命名</span><span class="sxs-lookup"><span data-stu-id="b817a-263">Named</span></span> |
| <span data-ttu-id="b817a-264">預設值</span><span class="sxs-lookup"><span data-stu-id="b817a-264">Default value</span></span> |<span data-ttu-id="b817a-265">無</span><span class="sxs-lookup"><span data-stu-id="b817a-265">none</span></span> |
| <span data-ttu-id="b817a-266">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="b817a-266">Accept pipeline input?</span></span> |<span data-ttu-id="b817a-267">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b817a-267">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b817a-268">參數集名稱</span><span class="sxs-lookup"><span data-stu-id="b817a-268">Parameter set name</span></span> |<span data-ttu-id="b817a-269">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="b817a-269">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="b817a-270">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="b817a-270">Accept wildcard characters?</span></span> |<span data-ttu-id="b817a-271">false</span><span class="sxs-lookup"><span data-stu-id="b817a-271">false</span></span> |

<span data-ttu-id="b817a-272">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-272">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="b817a-273">指定雜湊表的 hello 與此媒體服務相關聯的標記。</span><span class="sxs-lookup"><span data-stu-id="b817a-273">Specifies a hash table of hello tags that are associated with this media service.</span></span>

* <span data-ttu-id="b817a-274">hello 媒體服務相關聯的 hello 標記會取代 hello 客戶所指定的值。</span><span class="sxs-lookup"><span data-stu-id="b817a-274">hello tags that are associated with hello media service are replaced with value specified by hello customer.</span></span>

| <span data-ttu-id="b817a-275">別名</span><span class="sxs-lookup"><span data-stu-id="b817a-275">Aliases</span></span> | <span data-ttu-id="b817a-276">無</span><span class="sxs-lookup"><span data-stu-id="b817a-276">none</span></span> |
| --- | --- |
| <span data-ttu-id="b817a-277">必要？</span><span class="sxs-lookup"><span data-stu-id="b817a-277">Required?</span></span> |<span data-ttu-id="b817a-278">false</span><span class="sxs-lookup"><span data-stu-id="b817a-278">False</span></span> |
| <span data-ttu-id="b817a-279">位置？</span><span class="sxs-lookup"><span data-stu-id="b817a-279">Position?</span></span> |<span data-ttu-id="b817a-280">已命名</span><span class="sxs-lookup"><span data-stu-id="b817a-280">Named</span></span> |
| <span data-ttu-id="b817a-281">預設值</span><span class="sxs-lookup"><span data-stu-id="b817a-281">Default value</span></span> |<span data-ttu-id="b817a-282">無</span><span class="sxs-lookup"><span data-stu-id="b817a-282">None</span></span> |
| <span data-ttu-id="b817a-283">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="b817a-283">Accept pipeline input?</span></span> |<span data-ttu-id="b817a-284">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b817a-284">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b817a-285">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="b817a-285">Accept wildcard characters?</span></span> |<span data-ttu-id="b817a-286">false</span><span class="sxs-lookup"><span data-stu-id="b817a-286">false</span></span> |

<span data-ttu-id="b817a-287">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-287">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="b817a-288">這個 cmdlet 支援 hello 一般參數:-偵錯、-ErrorAction、-ErrorVariable、-InformationAction、-InformationVariable、-OutVariable、-OutBuffer、-PipelineVariable、-Verbose、-WarningAction 以及-WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="b817a-288">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="b817a-289">輸入</span><span class="sxs-lookup"><span data-stu-id="b817a-289">Inputs</span></span>
<span data-ttu-id="b817a-290">hello 輸入型別是 hello hello 型別物件，您可以使用管線傳送 toohello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b817a-290">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="b817a-291">輸出</span><span class="sxs-lookup"><span data-stu-id="b817a-291">Outputs</span></span>
<span data-ttu-id="b817a-292">hello 輸出類型是 hello hello cmdlet 的 hello 物件型別會發出。</span><span class="sxs-lookup"><span data-stu-id="b817a-292">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="remove-azurermmediaservice"></a><span data-ttu-id="b817a-293">Remove-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="b817a-293">Remove-AzureRmMediaService</span></span>
<span data-ttu-id="b817a-294">移除媒體服務。</span><span class="sxs-lookup"><span data-stu-id="b817a-294">Removes a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="b817a-295">語法</span><span class="sxs-lookup"><span data-stu-id="b817a-295">Syntax</span></span>
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="b817a-296">參數</span><span class="sxs-lookup"><span data-stu-id="b817a-296">Parameters</span></span>
<span data-ttu-id="b817a-297">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-297">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="b817a-298">指定此媒體服務所屬的 hello 資源群組 toowhich hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="b817a-298">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="b817a-299">別名</span><span class="sxs-lookup"><span data-stu-id="b817a-299">Aliases</span></span> | <span data-ttu-id="b817a-300">無</span><span class="sxs-lookup"><span data-stu-id="b817a-300">none</span></span> |
| --- | --- |
| <span data-ttu-id="b817a-301">必要？</span><span class="sxs-lookup"><span data-stu-id="b817a-301">Required?</span></span> |<span data-ttu-id="b817a-302">true</span><span class="sxs-lookup"><span data-stu-id="b817a-302">true</span></span> |
| <span data-ttu-id="b817a-303">位置？</span><span class="sxs-lookup"><span data-stu-id="b817a-303">Position?</span></span> |<span data-ttu-id="b817a-304">0</span><span class="sxs-lookup"><span data-stu-id="b817a-304">0</span></span> |
| <span data-ttu-id="b817a-305">預設值</span><span class="sxs-lookup"><span data-stu-id="b817a-305">Default value</span></span> |<span data-ttu-id="b817a-306">無</span><span class="sxs-lookup"><span data-stu-id="b817a-306">none</span></span> |
| <span data-ttu-id="b817a-307">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="b817a-307">Accept pipeline input?</span></span> |<span data-ttu-id="b817a-308">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b817a-308">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b817a-309">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="b817a-309">Accept wildcard characters?</span></span> |<span data-ttu-id="b817a-310">false</span><span class="sxs-lookup"><span data-stu-id="b817a-310">false</span></span> |

<span data-ttu-id="b817a-311">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-311">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="b817a-312">指定 hello hello 媒體服務名稱。</span><span class="sxs-lookup"><span data-stu-id="b817a-312">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="b817a-313">別名</span><span class="sxs-lookup"><span data-stu-id="b817a-313">Aliases</span></span> | <span data-ttu-id="b817a-314">無</span><span class="sxs-lookup"><span data-stu-id="b817a-314">none</span></span> |
| --- | --- |
| <span data-ttu-id="b817a-315">必要？</span><span class="sxs-lookup"><span data-stu-id="b817a-315">Required?</span></span> |<span data-ttu-id="b817a-316">true</span><span class="sxs-lookup"><span data-stu-id="b817a-316">true</span></span> |
| <span data-ttu-id="b817a-317">位置？</span><span class="sxs-lookup"><span data-stu-id="b817a-317">Position?</span></span> |<span data-ttu-id="b817a-318">2</span><span class="sxs-lookup"><span data-stu-id="b817a-318">2</span></span> |
| <span data-ttu-id="b817a-319">預設值</span><span class="sxs-lookup"><span data-stu-id="b817a-319">Default value</span></span> |<span data-ttu-id="b817a-320">無</span><span class="sxs-lookup"><span data-stu-id="b817a-320">None</span></span> |
| <span data-ttu-id="b817a-321">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="b817a-321">Accept pipeline input?</span></span> |<span data-ttu-id="b817a-322">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b817a-322">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b817a-323">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="b817a-323">Accept wildcard characters?</span></span> |<span data-ttu-id="b817a-324">False</span><span class="sxs-lookup"><span data-stu-id="b817a-324">False</span></span> |

<span data-ttu-id="b817a-325">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-325">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="b817a-326">這個 cmdlet 支援 hello 一般參數:-偵錯、-ErrorAction、-ErrorVariable、-InformationAction、-InformationVariable、-OutVariable、-OutBuffer、-PipelineVariable、-Verbose、-WarningAction 以及-WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="b817a-326">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="b817a-327">輸入</span><span class="sxs-lookup"><span data-stu-id="b817a-327">Inputs</span></span>
<span data-ttu-id="b817a-328">hello 輸入型別是 hello hello 型別物件，您可以使用管線傳送 toohello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b817a-328">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="b817a-329">輸出</span><span class="sxs-lookup"><span data-stu-id="b817a-329">Outputs</span></span>
<span data-ttu-id="b817a-330">hello 輸出類型是 hello hello cmdlet 的 hello 物件型別會發出。</span><span class="sxs-lookup"><span data-stu-id="b817a-330">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="get-azurermmediaservice"></a><span data-ttu-id="b817a-331">Get-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="b817a-331">Get-AzureRmMediaService</span></span>
<span data-ttu-id="b817a-332">取得資源群組中的所有媒體服務或取得指定名稱的媒體服務。</span><span class="sxs-lookup"><span data-stu-id="b817a-332">Gets all media services in a resource group or a media service with a given name.</span></span>

### <a name="syntax"></a><span data-ttu-id="b817a-333">語法</span><span class="sxs-lookup"><span data-stu-id="b817a-333">Syntax</span></span>
<span data-ttu-id="b817a-334">參數集：ResourceGroupParameterSet</span><span class="sxs-lookup"><span data-stu-id="b817a-334">ParameterSet: ResourceGroupParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

<span data-ttu-id="b817a-335">參數集：AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="b817a-335">ParameterSet: AccountNameParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="b817a-336">參數</span><span class="sxs-lookup"><span data-stu-id="b817a-336">Parameters</span></span>
<span data-ttu-id="b817a-337">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-337">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="b817a-338">指定此媒體服務所屬的 hello 資源群組 toowhich hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="b817a-338">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="b817a-339">別名</span><span class="sxs-lookup"><span data-stu-id="b817a-339">Aliases</span></span> | <span data-ttu-id="b817a-340">無</span><span class="sxs-lookup"><span data-stu-id="b817a-340">none</span></span> |
| --- | --- |
| <span data-ttu-id="b817a-341">必要？</span><span class="sxs-lookup"><span data-stu-id="b817a-341">Required?</span></span> |<span data-ttu-id="b817a-342">true</span><span class="sxs-lookup"><span data-stu-id="b817a-342">true</span></span> |
| <span data-ttu-id="b817a-343">位置？</span><span class="sxs-lookup"><span data-stu-id="b817a-343">Position?</span></span> |<span data-ttu-id="b817a-344">0</span><span class="sxs-lookup"><span data-stu-id="b817a-344">0</span></span> |
| <span data-ttu-id="b817a-345">預設值</span><span class="sxs-lookup"><span data-stu-id="b817a-345">Default value</span></span> |<span data-ttu-id="b817a-346">無</span><span class="sxs-lookup"><span data-stu-id="b817a-346">none</span></span> |
| <span data-ttu-id="b817a-347">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="b817a-347">Accept pipeline input?</span></span> |<span data-ttu-id="b817a-348">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b817a-348">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b817a-349">參數集名稱</span><span class="sxs-lookup"><span data-stu-id="b817a-349">Parameter set name</span></span> |<span data-ttu-id="b817a-350">ResourceGroupParameterSet、AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="b817a-350">ResourceGroupParameterSet, AccountNameParameterSet</span></span> |

<span data-ttu-id="b817a-351">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="b817a-351">Accept wildcard characters?</span></span>   <span data-ttu-id="b817a-352">false</span><span class="sxs-lookup"><span data-stu-id="b817a-352">false</span></span>

<span data-ttu-id="b817a-353">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-353">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="b817a-354">指定 hello hello 媒體服務名稱。</span><span class="sxs-lookup"><span data-stu-id="b817a-354">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="b817a-355">別名</span><span class="sxs-lookup"><span data-stu-id="b817a-355">Aliases</span></span> | <span data-ttu-id="b817a-356">無</span><span class="sxs-lookup"><span data-stu-id="b817a-356">none</span></span> |
| --- | --- |
| <span data-ttu-id="b817a-357">必要？</span><span class="sxs-lookup"><span data-stu-id="b817a-357">Required?</span></span> |<span data-ttu-id="b817a-358">true</span><span class="sxs-lookup"><span data-stu-id="b817a-358">true</span></span> |
| <span data-ttu-id="b817a-359">位置？</span><span class="sxs-lookup"><span data-stu-id="b817a-359">Position?</span></span> |<span data-ttu-id="b817a-360">1</span><span class="sxs-lookup"><span data-stu-id="b817a-360">1</span></span> |
| <span data-ttu-id="b817a-361">預設值</span><span class="sxs-lookup"><span data-stu-id="b817a-361">Default value</span></span> |<span data-ttu-id="b817a-362">無</span><span class="sxs-lookup"><span data-stu-id="b817a-362">none</span></span> |
| <span data-ttu-id="b817a-363">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="b817a-363">Accept pipeline input?</span></span> |<span data-ttu-id="b817a-364">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b817a-364">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b817a-365">參數集名稱</span><span class="sxs-lookup"><span data-stu-id="b817a-365">Parameter set name</span></span> |<span data-ttu-id="b817a-366">AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="b817a-366">AccountNameParameterSet</span></span> |
| <span data-ttu-id="b817a-367">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="b817a-367">Accept wildcard characters?</span></span> |<span data-ttu-id="b817a-368">false</span><span class="sxs-lookup"><span data-stu-id="b817a-368">false</span></span> |

<span data-ttu-id="b817a-369">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-369">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="b817a-370">這個 cmdlet 支援 hello 一般參數:-偵錯、-ErrorAction、-ErrorVariable、-InformationAction、-InformationVariable、-OutVariable、-OutBuffer、-PipelineVariable、-Verbose、-WarningAction 以及-WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="b817a-370">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="b817a-371">輸入</span><span class="sxs-lookup"><span data-stu-id="b817a-371">Inputs</span></span>
<span data-ttu-id="b817a-372">hello 輸入型別是 hello hello 型別物件，您可以使用管線傳送 toohello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b817a-372">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="b817a-373">輸出</span><span class="sxs-lookup"><span data-stu-id="b817a-373">Outputs</span></span>
<span data-ttu-id="b817a-374">hello 輸出類型是 hello hello cmdlet 的 hello 物件型別會發出。</span><span class="sxs-lookup"><span data-stu-id="b817a-374">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="get-azurermmediaservicekeys"></a><span data-ttu-id="b817a-375">Get-AzureRmMediaServiceKeys</span><span class="sxs-lookup"><span data-stu-id="b817a-375">Get-AzureRmMediaServiceKeys</span></span>
<span data-ttu-id="b817a-376">取得媒體服務的金鑰。</span><span class="sxs-lookup"><span data-stu-id="b817a-376">Gets keys of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="b817a-377">語法</span><span class="sxs-lookup"><span data-stu-id="b817a-377">Syntax</span></span>
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="b817a-378">參數</span><span class="sxs-lookup"><span data-stu-id="b817a-378">Parameters</span></span>
<span data-ttu-id="b817a-379">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-379">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="b817a-380">指定此媒體服務所屬的 hello 資源群組 toowhich hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="b817a-380">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="b817a-381">別名</span><span class="sxs-lookup"><span data-stu-id="b817a-381">Aliases</span></span> | <span data-ttu-id="b817a-382">無</span><span class="sxs-lookup"><span data-stu-id="b817a-382">none</span></span> |
| --- | --- |
| <span data-ttu-id="b817a-383">必要？</span><span class="sxs-lookup"><span data-stu-id="b817a-383">Required?</span></span> |<span data-ttu-id="b817a-384">true</span><span class="sxs-lookup"><span data-stu-id="b817a-384">true</span></span> |
| <span data-ttu-id="b817a-385">位置？</span><span class="sxs-lookup"><span data-stu-id="b817a-385">Position?</span></span> |<span data-ttu-id="b817a-386">0</span><span class="sxs-lookup"><span data-stu-id="b817a-386">0</span></span> |
| <span data-ttu-id="b817a-387">預設值</span><span class="sxs-lookup"><span data-stu-id="b817a-387">Default value</span></span> |<span data-ttu-id="b817a-388">無</span><span class="sxs-lookup"><span data-stu-id="b817a-388">none</span></span> |
| <span data-ttu-id="b817a-389">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="b817a-389">Accept pipeline input?</span></span> |<span data-ttu-id="b817a-390">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b817a-390">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b817a-391">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="b817a-391">Accept wildcard characters?</span></span> |<span data-ttu-id="b817a-392">false</span><span class="sxs-lookup"><span data-stu-id="b817a-392">false</span></span> |

<span data-ttu-id="b817a-393">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-393">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="b817a-394">指定 hello hello 媒體服務名稱。</span><span class="sxs-lookup"><span data-stu-id="b817a-394">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="b817a-395">別名</span><span class="sxs-lookup"><span data-stu-id="b817a-395">Aliases</span></span> | <span data-ttu-id="b817a-396">無</span><span class="sxs-lookup"><span data-stu-id="b817a-396">none</span></span> |
| --- | --- |
| <span data-ttu-id="b817a-397">必要？</span><span class="sxs-lookup"><span data-stu-id="b817a-397">Required?</span></span> |<span data-ttu-id="b817a-398">true</span><span class="sxs-lookup"><span data-stu-id="b817a-398">true</span></span> |
| <span data-ttu-id="b817a-399">位置？</span><span class="sxs-lookup"><span data-stu-id="b817a-399">Position?</span></span> |<span data-ttu-id="b817a-400">1</span><span class="sxs-lookup"><span data-stu-id="b817a-400">1</span></span> |
| <span data-ttu-id="b817a-401">預設值</span><span class="sxs-lookup"><span data-stu-id="b817a-401">Default value</span></span> |<span data-ttu-id="b817a-402">無</span><span class="sxs-lookup"><span data-stu-id="b817a-402">none</span></span> |
| <span data-ttu-id="b817a-403">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="b817a-403">Accept pipeline input?</span></span> |<span data-ttu-id="b817a-404">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b817a-404">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b817a-405">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="b817a-405">Accept wildcard characters?</span></span> |<span data-ttu-id="b817a-406">false</span><span class="sxs-lookup"><span data-stu-id="b817a-406">false</span></span> |

<span data-ttu-id="b817a-407">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-407">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="b817a-408">這個 cmdlet 支援 hello 一般參數:-偵錯、-ErrorAction、-ErrorVariable、-InformationAction、-InformationVariable、-OutVariable、-OutBuffer、-PipelineVariable、-Verbose、-WarningAction 以及-WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="b817a-408">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="b817a-409">輸入</span><span class="sxs-lookup"><span data-stu-id="b817a-409">Inputs</span></span>
<span data-ttu-id="b817a-410">hello 輸入型別是 hello hello 型別物件，您可以使用管線傳送 toohello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b817a-410">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="b817a-411">輸出</span><span class="sxs-lookup"><span data-stu-id="b817a-411">Outputs</span></span>
<span data-ttu-id="b817a-412">hello 輸出類型是 hello hello cmdlet 的 hello 物件型別會發出。</span><span class="sxs-lookup"><span data-stu-id="b817a-412">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="set-azurermmediaservicekey"></a><span data-ttu-id="b817a-413">Set-AzureRmMediaServiceKey</span><span class="sxs-lookup"><span data-stu-id="b817a-413">Set-AzureRmMediaServiceKey</span></span>
<span data-ttu-id="b817a-414">重新產生媒體服務的主要或次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="b817a-414">Regenerates a primary or secondary key of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="b817a-415">語法</span><span class="sxs-lookup"><span data-stu-id="b817a-415">Syntax</span></span>
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="b817a-416">參數</span><span class="sxs-lookup"><span data-stu-id="b817a-416">Parameters</span></span>
<span data-ttu-id="b817a-417">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-417">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="b817a-418">指定此媒體服務所屬的 hello 資源群組 toowhich hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="b817a-418">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="b817a-419">別名</span><span class="sxs-lookup"><span data-stu-id="b817a-419">Aliases</span></span> | <span data-ttu-id="b817a-420">無</span><span class="sxs-lookup"><span data-stu-id="b817a-420">none</span></span> |
| --- | --- |
| <span data-ttu-id="b817a-421">必要？</span><span class="sxs-lookup"><span data-stu-id="b817a-421">Required?</span></span> |<span data-ttu-id="b817a-422">true</span><span class="sxs-lookup"><span data-stu-id="b817a-422">true</span></span> |
| <span data-ttu-id="b817a-423">位置？</span><span class="sxs-lookup"><span data-stu-id="b817a-423">Position?</span></span> |<span data-ttu-id="b817a-424">0</span><span class="sxs-lookup"><span data-stu-id="b817a-424">0</span></span> |
| <span data-ttu-id="b817a-425">預設值</span><span class="sxs-lookup"><span data-stu-id="b817a-425">Default value</span></span> |<span data-ttu-id="b817a-426">無</span><span class="sxs-lookup"><span data-stu-id="b817a-426">none</span></span> |
| <span data-ttu-id="b817a-427">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="b817a-427">Accept pipeline input?</span></span> |<span data-ttu-id="b817a-428">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b817a-428">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b817a-429">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="b817a-429">Accept wildcard characters?</span></span> |<span data-ttu-id="b817a-430">false</span><span class="sxs-lookup"><span data-stu-id="b817a-430">false</span></span> |

<span data-ttu-id="b817a-431">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-431">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="b817a-432">指定 hello hello 媒體服務名稱。</span><span class="sxs-lookup"><span data-stu-id="b817a-432">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="b817a-433">別名</span><span class="sxs-lookup"><span data-stu-id="b817a-433">Aliases</span></span> | <span data-ttu-id="b817a-434">無</span><span class="sxs-lookup"><span data-stu-id="b817a-434">none</span></span> |
| --- | --- |
| <span data-ttu-id="b817a-435">必要？</span><span class="sxs-lookup"><span data-stu-id="b817a-435">Required?</span></span> |<span data-ttu-id="b817a-436">true</span><span class="sxs-lookup"><span data-stu-id="b817a-436">true</span></span> |
| <span data-ttu-id="b817a-437">位置？</span><span class="sxs-lookup"><span data-stu-id="b817a-437">Position?</span></span> |<span data-ttu-id="b817a-438">1</span><span class="sxs-lookup"><span data-stu-id="b817a-438">1</span></span> |
| <span data-ttu-id="b817a-439">預設值</span><span class="sxs-lookup"><span data-stu-id="b817a-439">Default value</span></span> |<span data-ttu-id="b817a-440">無</span><span class="sxs-lookup"><span data-stu-id="b817a-440">none</span></span> |
| <span data-ttu-id="b817a-441">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="b817a-441">Accept pipeline input?</span></span> |<span data-ttu-id="b817a-442">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b817a-442">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b817a-443">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="b817a-443">Accept wildcard characters?</span></span> |<span data-ttu-id="b817a-444">false</span><span class="sxs-lookup"><span data-stu-id="b817a-444">false</span></span> |

<span data-ttu-id="b817a-445">**-KeyType &lt;KeyType&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-445">**-KeyType &lt;KeyType&gt;**</span></span>

<span data-ttu-id="b817a-446">指定 hello hello 媒體服務金鑰類型。</span><span class="sxs-lookup"><span data-stu-id="b817a-446">Specifies hello key type of hello media service.</span></span>

* <span data-ttu-id="b817a-447">主要或次要</span><span class="sxs-lookup"><span data-stu-id="b817a-447">Primary or Secondary</span></span>

| <span data-ttu-id="b817a-448">別名</span><span class="sxs-lookup"><span data-stu-id="b817a-448">Aliases</span></span> | <span data-ttu-id="b817a-449">無</span><span class="sxs-lookup"><span data-stu-id="b817a-449">none</span></span> |
| --- | --- |
| <span data-ttu-id="b817a-450">必要？</span><span class="sxs-lookup"><span data-stu-id="b817a-450">Required?</span></span> |<span data-ttu-id="b817a-451">true</span><span class="sxs-lookup"><span data-stu-id="b817a-451">true</span></span> |
| <span data-ttu-id="b817a-452">位置？</span><span class="sxs-lookup"><span data-stu-id="b817a-452">Position?</span></span> |<span data-ttu-id="b817a-453">2</span><span class="sxs-lookup"><span data-stu-id="b817a-453">2</span></span> |
| <span data-ttu-id="b817a-454">預設值</span><span class="sxs-lookup"><span data-stu-id="b817a-454">Default value</span></span> |<span data-ttu-id="b817a-455">無</span><span class="sxs-lookup"><span data-stu-id="b817a-455">none</span></span> |
| <span data-ttu-id="b817a-456">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="b817a-456">Accept pipeline input?</span></span> |<span data-ttu-id="b817a-457">false</span><span class="sxs-lookup"><span data-stu-id="b817a-457">false</span></span> |
| <span data-ttu-id="b817a-458">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="b817a-458">Accept wildcard characters?</span></span> |<span data-ttu-id="b817a-459">false</span><span class="sxs-lookup"><span data-stu-id="b817a-459">false</span></span> |

<span data-ttu-id="b817a-460">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-460">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="b817a-461">這個 cmdlet 支援 hello 一般參數:-偵錯、-ErrorAction、-ErrorVariable、-InformationAction、-InformationVariable、-OutVariable、-OutBuffer、-PipelineVariable、-Verbose、-WarningAction 以及-WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="b817a-461">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="b817a-462">輸入</span><span class="sxs-lookup"><span data-stu-id="b817a-462">Inputs</span></span>
<span data-ttu-id="b817a-463">hello 輸入型別是 hello hello 型別物件，您可以使用管線傳送 toothe cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b817a-463">hello input type is hello type of hello objects that you can pipe toothe cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="b817a-464">輸出</span><span class="sxs-lookup"><span data-stu-id="b817a-464">Outputs</span></span>
<span data-ttu-id="b817a-465">hello 輸出類型是 hello hello cmdlet 的 hello 物件型別會發出。</span><span class="sxs-lookup"><span data-stu-id="b817a-465">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="sync-azurermmediaservicestoragekeys"></a><span data-ttu-id="b817a-466">Sync-AzureRmMediaServiceStorageKeys</span><span class="sxs-lookup"><span data-stu-id="b817a-466">Sync-AzureRmMediaServiceStorageKeys</span></span>
<span data-ttu-id="b817a-467">同步處理與 hello 媒體服務相關聯的儲存體帳戶的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="b817a-467">Synchronizes storage account keys for a storage account associated with hello media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="b817a-468">語法</span><span class="sxs-lookup"><span data-stu-id="b817a-468">Syntax</span></span>
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="b817a-469">參數</span><span class="sxs-lookup"><span data-stu-id="b817a-469">Parameters</span></span>
<span data-ttu-id="b817a-470">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-470">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="b817a-471">指定此媒體服務所屬的 hello 資源群組 toowhich hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="b817a-471">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="b817a-472">別名</span><span class="sxs-lookup"><span data-stu-id="b817a-472">Aliases</span></span> | <span data-ttu-id="b817a-473">無</span><span class="sxs-lookup"><span data-stu-id="b817a-473">none</span></span> |
| --- | --- |
| <span data-ttu-id="b817a-474">必要？</span><span class="sxs-lookup"><span data-stu-id="b817a-474">Required?</span></span> |<span data-ttu-id="b817a-475">true</span><span class="sxs-lookup"><span data-stu-id="b817a-475">true</span></span> |
| <span data-ttu-id="b817a-476">位置？</span><span class="sxs-lookup"><span data-stu-id="b817a-476">Position?</span></span> |<span data-ttu-id="b817a-477">0</span><span class="sxs-lookup"><span data-stu-id="b817a-477">0</span></span> |
| <span data-ttu-id="b817a-478">預設值</span><span class="sxs-lookup"><span data-stu-id="b817a-478">Default value</span></span> |<span data-ttu-id="b817a-479">無</span><span class="sxs-lookup"><span data-stu-id="b817a-479">none</span></span> |
| <span data-ttu-id="b817a-480">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="b817a-480">Accept pipeline input?</span></span> |<span data-ttu-id="b817a-481">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b817a-481">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b817a-482">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="b817a-482">Accept wildcard characters?</span></span> |<span data-ttu-id="b817a-483">false</span><span class="sxs-lookup"><span data-stu-id="b817a-483">false</span></span> |

<span data-ttu-id="b817a-484">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-484">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="b817a-485">指定 hello hello 媒體服務名稱。</span><span class="sxs-lookup"><span data-stu-id="b817a-485">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="b817a-486">別名</span><span class="sxs-lookup"><span data-stu-id="b817a-486">Aliases</span></span> | <span data-ttu-id="b817a-487">無</span><span class="sxs-lookup"><span data-stu-id="b817a-487">none</span></span> |
| --- | --- |
| <span data-ttu-id="b817a-488">必要？</span><span class="sxs-lookup"><span data-stu-id="b817a-488">Required?</span></span> |<span data-ttu-id="b817a-489">true</span><span class="sxs-lookup"><span data-stu-id="b817a-489">true</span></span> |
| <span data-ttu-id="b817a-490">位置？</span><span class="sxs-lookup"><span data-stu-id="b817a-490">Position?</span></span> |<span data-ttu-id="b817a-491">1</span><span class="sxs-lookup"><span data-stu-id="b817a-491">1</span></span> |
| <span data-ttu-id="b817a-492">預設值</span><span class="sxs-lookup"><span data-stu-id="b817a-492">Default value</span></span> |<span data-ttu-id="b817a-493">無</span><span class="sxs-lookup"><span data-stu-id="b817a-493">none</span></span> |
| <span data-ttu-id="b817a-494">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="b817a-494">Accept pipeline input?</span></span> |<span data-ttu-id="b817a-495">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b817a-495">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b817a-496">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="b817a-496">Accept wildcard characters?</span></span> |<span data-ttu-id="b817a-497">false</span><span class="sxs-lookup"><span data-stu-id="b817a-497">false</span></span> |

<span data-ttu-id="b817a-498">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-498">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="b817a-499">指定 hello 與 hello 媒體服務相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b817a-499">Specifies hello storage account associated with hello media service.</span></span>

| <span data-ttu-id="b817a-500">別名</span><span class="sxs-lookup"><span data-stu-id="b817a-500">Aliases</span></span> | <span data-ttu-id="b817a-501">識別碼</span><span class="sxs-lookup"><span data-stu-id="b817a-501">Id</span></span> |
| --- | --- |
| <span data-ttu-id="b817a-502">必要？</span><span class="sxs-lookup"><span data-stu-id="b817a-502">Required?</span></span> |<span data-ttu-id="b817a-503">true</span><span class="sxs-lookup"><span data-stu-id="b817a-503">true</span></span> |
| <span data-ttu-id="b817a-504">位置？</span><span class="sxs-lookup"><span data-stu-id="b817a-504">Position?</span></span> |<span data-ttu-id="b817a-505">2</span><span class="sxs-lookup"><span data-stu-id="b817a-505">2</span></span> |
| <span data-ttu-id="b817a-506">預設值</span><span class="sxs-lookup"><span data-stu-id="b817a-506">Default value</span></span> |<span data-ttu-id="b817a-507">無</span><span class="sxs-lookup"><span data-stu-id="b817a-507">none</span></span> |
| <span data-ttu-id="b817a-508">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="b817a-508">Accept pipeline input?</span></span> |<span data-ttu-id="b817a-509">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b817a-509">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b817a-510">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="b817a-510">Accept wildcard characters?</span></span> |<span data-ttu-id="b817a-511">false</span><span class="sxs-lookup"><span data-stu-id="b817a-511">false</span></span> |

<span data-ttu-id="b817a-512">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="b817a-512">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="b817a-513">這個 cmdlet 支援 hello 一般參數:-偵錯、-ErrorAction、-ErrorVariable、-InformationAction、-InformationVariable、-OutVariable、-OutBuffer、-PipelineVariable、-Verbose、-WarningAction 以及-WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="b817a-513">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="b817a-514">輸入</span><span class="sxs-lookup"><span data-stu-id="b817a-514">Inputs</span></span>
<span data-ttu-id="b817a-515">hello 輸入型別是 hello hello 型別物件，您可以使用管線傳送 toohello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b817a-515">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="b817a-516">輸出</span><span class="sxs-lookup"><span data-stu-id="b817a-516">Outputs</span></span>
<span data-ttu-id="b817a-517">hello 輸出類型是 hello hello cmdlet 的 hello 物件型別會發出。</span><span class="sxs-lookup"><span data-stu-id="b817a-517">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="next-step"></a><span data-ttu-id="b817a-518">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b817a-518">Next step</span></span>
<span data-ttu-id="b817a-519">查看媒體服務學習途徑。</span><span class="sxs-lookup"><span data-stu-id="b817a-519">Check out Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b817a-520">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="b817a-520">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

