---
title: "利用 PowerShell 管理 Azure Media Services 帳戶"
description: "瞭解如何管理 PowerShell cmdlet 與 Azure Media Services 帳戶。"
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
ms.openlocfilehash: 3d999d9e27844bc0164cc3572522b9ec022118a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a><span data-ttu-id="4ec3a-103">利用 PowerShell 管理 Azure Media Services 帳戶</span><span class="sxs-lookup"><span data-stu-id="4ec3a-103">Manage Azure Media Services Accounts with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4ec3a-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="4ec3a-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="4ec3a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ec3a-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="4ec3a-106">REST</span><span class="sxs-lookup"><span data-stu-id="4ec3a-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="4ec3a-107">若要建立 Azure 媒體服務帳戶，您必須擁有 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-107">To be able to create an Azure Media Services account, you must have an Azure account.</span></span> <span data-ttu-id="4ec3a-108">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4ec3a-109">如需詳細資料，請參閱 <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure 免費試用</a>。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-109">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="4ec3a-110">Overview</span><span class="sxs-lookup"><span data-stu-id="4ec3a-110">Overview</span></span>
<span data-ttu-id="4ec3a-111">本文列出 Azure 媒體服務 (AMS) 在 Azure Resource Manager 架構中的 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-111">This article lists the Azure PowerShell cmdlets for Azure Media Services (AMS) in the Azure Resource Manager framework.</span></span> <span data-ttu-id="4ec3a-112">Cmdlet 存在於 **Microsoft.Azure.Commands.Media** 命名空間。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-112">The cmdlets exist in the **Microsoft.Azure.Commands.Media** namespace.</span></span>

## <a name="versions"></a><span data-ttu-id="4ec3a-113">版本</span><span class="sxs-lookup"><span data-stu-id="4ec3a-113">Versions</span></span>
<span data-ttu-id="4ec3a-114">**ApiVersion**："2015-10-01"</span><span class="sxs-lookup"><span data-stu-id="4ec3a-114">**ApiVersion**:   "2015-10-01"</span></span>

## <a name="new-azurermmediaservice"></a><span data-ttu-id="4ec3a-115">New-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="4ec3a-115">New-AzureRmMediaService</span></span>
<span data-ttu-id="4ec3a-116">建立媒體服務。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-116">Creates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="4ec3a-117">語法</span><span class="sxs-lookup"><span data-stu-id="4ec3a-117">Syntax</span></span>
<span data-ttu-id="4ec3a-118">參數集︰StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="4ec3a-118">Parameter Set: StorageAccountIdParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

<span data-ttu-id="4ec3a-119">參數集︰StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="4ec3a-119">Parameter Set: StorageAccountsParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="4ec3a-120">參數</span><span class="sxs-lookup"><span data-stu-id="4ec3a-120">Parameters</span></span>
<span data-ttu-id="4ec3a-121">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-121">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="4ec3a-122">指定此媒體服務所屬資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-122">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="4ec3a-123">別名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-123">Aliases</span></span> | <span data-ttu-id="4ec3a-124">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ec3a-125">必要？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-125">Required?</span></span> |<span data-ttu-id="4ec3a-126">true</span><span class="sxs-lookup"><span data-stu-id="4ec3a-126">true</span></span> |
| <span data-ttu-id="4ec3a-127">位置？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-127">Position?</span></span> |<span data-ttu-id="4ec3a-128">0</span><span class="sxs-lookup"><span data-stu-id="4ec3a-128">0</span></span> |
| <span data-ttu-id="4ec3a-129">預設值</span><span class="sxs-lookup"><span data-stu-id="4ec3a-129">Default value</span></span> |<span data-ttu-id="4ec3a-130">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-130">none</span></span> |
| <span data-ttu-id="4ec3a-131">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-131">Accept pipeline input?</span></span> |<span data-ttu-id="4ec3a-132">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="4ec3a-132">true(ByPropertyName)</span></span> |
| <span data-ttu-id="4ec3a-133">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-133">Accept wildcard characters?</span></span> |<span data-ttu-id="4ec3a-134">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-134">false</span></span> |

<span data-ttu-id="4ec3a-135">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-135">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="4ec3a-136">指定媒體服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-136">Specifies the name of the media service.</span></span>

| <span data-ttu-id="4ec3a-137">別名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-137">Aliases</span></span> | <span data-ttu-id="4ec3a-138">Name</span><span class="sxs-lookup"><span data-stu-id="4ec3a-138">Name</span></span> |
| --- | --- |
| <span data-ttu-id="4ec3a-139">必要？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-139">Required?</span></span> |<span data-ttu-id="4ec3a-140">true</span><span class="sxs-lookup"><span data-stu-id="4ec3a-140">true</span></span> |
| <span data-ttu-id="4ec3a-141">位置？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-141">Position?</span></span> |<span data-ttu-id="4ec3a-142">1</span><span class="sxs-lookup"><span data-stu-id="4ec3a-142">1</span></span> |
| <span data-ttu-id="4ec3a-143">預設值</span><span class="sxs-lookup"><span data-stu-id="4ec3a-143">Default value</span></span> |<span data-ttu-id="4ec3a-144">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-144">none</span></span> |
| <span data-ttu-id="4ec3a-145">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-145">Accept pipeline input?</span></span> |<span data-ttu-id="4ec3a-146">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-146">false</span></span> |
| <span data-ttu-id="4ec3a-147">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-147">Accept wildcard characters?</span></span> |<span data-ttu-id="4ec3a-148">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-148">false</span></span> |

<span data-ttu-id="4ec3a-149">**-Location &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-149">**-Location &lt;String&gt;**</span></span>

<span data-ttu-id="4ec3a-150">指定媒體服務的資源位置。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-150">Specifies the resource location of the media service.</span></span>

| <span data-ttu-id="4ec3a-151">別名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-151">Aliases</span></span> | <span data-ttu-id="4ec3a-152">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-152">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ec3a-153">必要？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-153">Required?</span></span> |<span data-ttu-id="4ec3a-154">true</span><span class="sxs-lookup"><span data-stu-id="4ec3a-154">true</span></span> |
| <span data-ttu-id="4ec3a-155">位置？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-155">Position?</span></span> |<span data-ttu-id="4ec3a-156">2</span><span class="sxs-lookup"><span data-stu-id="4ec3a-156">2</span></span> |
| <span data-ttu-id="4ec3a-157">預設值</span><span class="sxs-lookup"><span data-stu-id="4ec3a-157">Default value</span></span> |<span data-ttu-id="4ec3a-158">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-158">none</span></span> |
| <span data-ttu-id="4ec3a-159">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-159">Accept pipeline input?</span></span> |<span data-ttu-id="4ec3a-160">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="4ec3a-160">true(ByPropertyName)</span></span> |
| <span data-ttu-id="4ec3a-161">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-161">Accept wildcard characters?</span></span> |<span data-ttu-id="4ec3a-162">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-162">false</span></span> |

<span data-ttu-id="4ec3a-163">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-163">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="4ec3a-164">指定與媒體服務相關聯的主要儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-164">Specifies a primary storage account that associated with the media service.</span></span>

* <span data-ttu-id="4ec3a-165">只支援新的儲存體帳戶 (使用 Resource Manager API 所建立)。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-165">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="4ec3a-166">儲存體帳戶必須存在，而且具有與媒體服務相同的位置。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-166">The storage account must exist and has the same location with the media service.</span></span>

| <span data-ttu-id="4ec3a-167">別名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-167">Aliases</span></span> | <span data-ttu-id="4ec3a-168">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-168">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ec3a-169">必要？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-169">Required?</span></span> |<span data-ttu-id="4ec3a-170">true</span><span class="sxs-lookup"><span data-stu-id="4ec3a-170">true</span></span> |
| <span data-ttu-id="4ec3a-171">位置？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-171">Position?</span></span> |<span data-ttu-id="4ec3a-172">3</span><span class="sxs-lookup"><span data-stu-id="4ec3a-172">3</span></span> |
| <span data-ttu-id="4ec3a-173">預設值</span><span class="sxs-lookup"><span data-stu-id="4ec3a-173">Default value</span></span> |<span data-ttu-id="4ec3a-174">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-174">none</span></span> |
| <span data-ttu-id="4ec3a-175">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-175">Accept pipeline input?</span></span> |<span data-ttu-id="4ec3a-176">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="4ec3a-176">true(ByPropertyName)</span></span> |
| <span data-ttu-id="4ec3a-177">參數集名稱</span><span class="sxs-lookup"><span data-stu-id="4ec3a-177">Parameter set name</span></span> |<span data-ttu-id="4ec3a-178">StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="4ec3a-178">StorageAccountIdParamSet</span></span> |
| <span data-ttu-id="4ec3a-179">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-179">Accept wildcard characters?</span></span> |<span data-ttu-id="4ec3a-180">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-180">false</span></span> |

<span data-ttu-id="4ec3a-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="4ec3a-182">指定與媒體服務相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-182">Specifies storage accounts that associated with the media service.</span></span>

* <span data-ttu-id="4ec3a-183">只支援新的儲存體帳戶 (使用 Resource Manager API 所建立)。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-183">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="4ec3a-184">儲存體帳戶必須存在，而且具有與媒體服務相同的位置。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-184">The storage account must exist and has the same location with the media service.</span></span>
* <span data-ttu-id="4ec3a-185">只可以指定一個主要儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-185">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="4ec3a-186">別名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-186">Aliases</span></span> | <span data-ttu-id="4ec3a-187">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-187">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ec3a-188">必要？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-188">Required?</span></span> |<span data-ttu-id="4ec3a-189">true</span><span class="sxs-lookup"><span data-stu-id="4ec3a-189">true</span></span> |
| <span data-ttu-id="4ec3a-190">位置？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-190">Position?</span></span> |<span data-ttu-id="4ec3a-191">3</span><span class="sxs-lookup"><span data-stu-id="4ec3a-191">3</span></span> |
| <span data-ttu-id="4ec3a-192">預設值</span><span class="sxs-lookup"><span data-stu-id="4ec3a-192">Default value</span></span> |<span data-ttu-id="4ec3a-193">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-193">none</span></span> |
| <span data-ttu-id="4ec3a-194">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-194">Accept pipeline input?</span></span> |<span data-ttu-id="4ec3a-195">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="4ec3a-195">true(ByPropertyName)</span></span> |
| <span data-ttu-id="4ec3a-196">參數集名稱</span><span class="sxs-lookup"><span data-stu-id="4ec3a-196">Parameter set name</span></span> |<span data-ttu-id="4ec3a-197">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="4ec3a-197">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="4ec3a-198">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-198">Accept wildcard characters?</span></span> |<span data-ttu-id="4ec3a-199">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-199">false</span></span> |

<span data-ttu-id="4ec3a-200">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-200">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="4ec3a-201">指定與媒體服務相關聯之標記的雜湊表。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-201">Specifies a hash table of the tags that are associated with the media service.</span></span>

* <span data-ttu-id="4ec3a-202">範例: @{"標籤 1"="value1";"標籤 2 」 =: value2"}</span><span class="sxs-lookup"><span data-stu-id="4ec3a-202">Example: @{"tag1"="value1";"tag2"=:value2"}</span></span>

| <span data-ttu-id="4ec3a-203">別名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-203">Aliases</span></span> | <span data-ttu-id="4ec3a-204">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-204">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ec3a-205">必要？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-205">Required?</span></span> |<span data-ttu-id="4ec3a-206">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-206">false</span></span> |
| <span data-ttu-id="4ec3a-207">位置？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-207">Position?</span></span> |<span data-ttu-id="4ec3a-208">已命名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-208">named</span></span> |
| <span data-ttu-id="4ec3a-209">預設值</span><span class="sxs-lookup"><span data-stu-id="4ec3a-209">Default value</span></span> |<span data-ttu-id="4ec3a-210">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-210">none</span></span> |
| <span data-ttu-id="4ec3a-211">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-211">Accept pipeline input?</span></span> |<span data-ttu-id="4ec3a-212">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-212">false</span></span> |
| <span data-ttu-id="4ec3a-213">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-213">Accept wildcard characters?</span></span> |<span data-ttu-id="4ec3a-214">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-214">false</span></span> |

<span data-ttu-id="4ec3a-215">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-215">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="4ec3a-216">這個 Cmdlet 支援一般參數：-Debug、-ErrorAction、-ErrorVariable、-InformationAction、-InformationVariable、-OutVariable、-OutBuffer、-PipelineVariable、-Verbose、-WarningAction 和 -WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-216">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="4ec3a-217">輸入</span><span class="sxs-lookup"><span data-stu-id="4ec3a-217">Inputs</span></span>
<span data-ttu-id="4ec3a-218">輸入類型是可以透過管線傳送至 Cmdlet 的物件類型。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-218">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="4ec3a-219">輸出</span><span class="sxs-lookup"><span data-stu-id="4ec3a-219">Outputs</span></span>
<span data-ttu-id="4ec3a-220">輸出類型是 Cmdlet 所發出的物件類型。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-220">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="set-azurermmediaservice"></a><span data-ttu-id="4ec3a-221">Set-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="4ec3a-221">Set-AzureRmMediaService</span></span>
<span data-ttu-id="4ec3a-222">更新媒體服務。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-222">Updates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="4ec3a-223">語法</span><span class="sxs-lookup"><span data-stu-id="4ec3a-223">Syntax</span></span>
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="4ec3a-224">參數</span><span class="sxs-lookup"><span data-stu-id="4ec3a-224">Parameters</span></span>
<span data-ttu-id="4ec3a-225">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-225">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="4ec3a-226">指定此媒體服務所屬資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-226">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="4ec3a-227">別名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-227">Aliases</span></span> | <span data-ttu-id="4ec3a-228">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-228">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ec3a-229">必要？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-229">Required?</span></span> |<span data-ttu-id="4ec3a-230">true</span><span class="sxs-lookup"><span data-stu-id="4ec3a-230">true</span></span> |
| <span data-ttu-id="4ec3a-231">位置？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-231">Position?</span></span> |<span data-ttu-id="4ec3a-232">0</span><span class="sxs-lookup"><span data-stu-id="4ec3a-232">0</span></span> |
| <span data-ttu-id="4ec3a-233">預設值</span><span class="sxs-lookup"><span data-stu-id="4ec3a-233">Default Value</span></span> |<span data-ttu-id="4ec3a-234">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-234">none</span></span> |
| <span data-ttu-id="4ec3a-235">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-235">Accept Pipeline Input?</span></span> |<span data-ttu-id="4ec3a-236">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="4ec3a-236">true(ByPropertyName)</span></span> |
| <span data-ttu-id="4ec3a-237">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-237">Accept wildcard characters?</span></span> |<span data-ttu-id="4ec3a-238">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-238">false</span></span> |

<span data-ttu-id="4ec3a-239">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-239">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="4ec3a-240">指定媒體服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-240">Specifies the name of the media service.</span></span>

| <span data-ttu-id="4ec3a-241">別名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-241">Aliases</span></span> | <span data-ttu-id="4ec3a-242">Name</span><span class="sxs-lookup"><span data-stu-id="4ec3a-242">Name</span></span> |
| --- | --- |
| <span data-ttu-id="4ec3a-243">必要？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-243">Required?</span></span> |<span data-ttu-id="4ec3a-244">true</span><span class="sxs-lookup"><span data-stu-id="4ec3a-244">True</span></span> |
| <span data-ttu-id="4ec3a-245">位置？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-245">Position?</span></span> |<span data-ttu-id="4ec3a-246">1</span><span class="sxs-lookup"><span data-stu-id="4ec3a-246">1</span></span> |
| <span data-ttu-id="4ec3a-247">預設值</span><span class="sxs-lookup"><span data-stu-id="4ec3a-247">Default value</span></span> |<span data-ttu-id="4ec3a-248">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-248">None</span></span> |
| <span data-ttu-id="4ec3a-249">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-249">Accept pipeline input?</span></span> |<span data-ttu-id="4ec3a-250">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="4ec3a-250">true(ByPropertyName)</span></span> |
| <span data-ttu-id="4ec3a-251">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-251">Accept wildcard characters?</span></span> |<span data-ttu-id="4ec3a-252">False</span><span class="sxs-lookup"><span data-stu-id="4ec3a-252">False</span></span> |

<span data-ttu-id="4ec3a-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="4ec3a-254">指定與媒體服務相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-254">Specifies storage accounts that associated with the media service.</span></span>

* <span data-ttu-id="4ec3a-255">只支援新的儲存體帳戶 (使用 Resource Manager API 所建立)。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-255">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="4ec3a-256">儲存體帳戶必須存在，而且具有與媒體服務相同的位置。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-256">The storage account must exist and has the same location with the media service.</span></span>
* <span data-ttu-id="4ec3a-257">只可以指定一個主要儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-257">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="4ec3a-258">別名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-258">Aliases</span></span> | <span data-ttu-id="4ec3a-259">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-259">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ec3a-260">必要？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-260">Required?</span></span> |<span data-ttu-id="4ec3a-261">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-261">false</span></span> |
| <span data-ttu-id="4ec3a-262">位置？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-262">Position?</span></span> |<span data-ttu-id="4ec3a-263">已命名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-263">Named</span></span> |
| <span data-ttu-id="4ec3a-264">預設值</span><span class="sxs-lookup"><span data-stu-id="4ec3a-264">Default value</span></span> |<span data-ttu-id="4ec3a-265">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-265">none</span></span> |
| <span data-ttu-id="4ec3a-266">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-266">Accept pipeline input?</span></span> |<span data-ttu-id="4ec3a-267">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="4ec3a-267">true(ByPropertyName)</span></span> |
| <span data-ttu-id="4ec3a-268">參數集名稱</span><span class="sxs-lookup"><span data-stu-id="4ec3a-268">Parameter set name</span></span> |<span data-ttu-id="4ec3a-269">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="4ec3a-269">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="4ec3a-270">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-270">Accept wildcard characters?</span></span> |<span data-ttu-id="4ec3a-271">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-271">false</span></span> |

<span data-ttu-id="4ec3a-272">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-272">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="4ec3a-273">指定與此媒體服務相關聯之標記的雜湊表。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-273">Specifies a hash table of the tags that are associated with this media service.</span></span>

* <span data-ttu-id="4ec3a-274">與媒體服務相關聯的標記會取代為客戶指定的值。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-274">The tags that are associated with the media service are replaced with value specified by the customer.</span></span>

| <span data-ttu-id="4ec3a-275">別名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-275">Aliases</span></span> | <span data-ttu-id="4ec3a-276">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-276">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ec3a-277">必要？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-277">Required?</span></span> |<span data-ttu-id="4ec3a-278">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-278">False</span></span> |
| <span data-ttu-id="4ec3a-279">位置？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-279">Position?</span></span> |<span data-ttu-id="4ec3a-280">已命名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-280">Named</span></span> |
| <span data-ttu-id="4ec3a-281">預設值</span><span class="sxs-lookup"><span data-stu-id="4ec3a-281">Default value</span></span> |<span data-ttu-id="4ec3a-282">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-282">None</span></span> |
| <span data-ttu-id="4ec3a-283">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-283">Accept pipeline input?</span></span> |<span data-ttu-id="4ec3a-284">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="4ec3a-284">true(ByPropertyName)</span></span> |
| <span data-ttu-id="4ec3a-285">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-285">Accept wildcard characters?</span></span> |<span data-ttu-id="4ec3a-286">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-286">false</span></span> |

<span data-ttu-id="4ec3a-287">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-287">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="4ec3a-288">這個 Cmdlet 支援一般參數：-Debug、-ErrorAction、-ErrorVariable、-InformationAction、-InformationVariable、-OutVariable、-OutBuffer、-PipelineVariable、-Verbose、-WarningAction 和 -WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-288">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="4ec3a-289">輸入</span><span class="sxs-lookup"><span data-stu-id="4ec3a-289">Inputs</span></span>
<span data-ttu-id="4ec3a-290">輸入類型是可以透過管線傳送至 Cmdlet 的物件類型。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-290">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="4ec3a-291">輸出</span><span class="sxs-lookup"><span data-stu-id="4ec3a-291">Outputs</span></span>
<span data-ttu-id="4ec3a-292">輸出類型是 Cmdlet 所發出的物件類型。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-292">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="remove-azurermmediaservice"></a><span data-ttu-id="4ec3a-293">Remove-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="4ec3a-293">Remove-AzureRmMediaService</span></span>
<span data-ttu-id="4ec3a-294">移除媒體服務。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-294">Removes a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="4ec3a-295">語法</span><span class="sxs-lookup"><span data-stu-id="4ec3a-295">Syntax</span></span>
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="4ec3a-296">參數</span><span class="sxs-lookup"><span data-stu-id="4ec3a-296">Parameters</span></span>
<span data-ttu-id="4ec3a-297">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-297">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="4ec3a-298">指定此媒體服務所屬資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-298">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="4ec3a-299">別名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-299">Aliases</span></span> | <span data-ttu-id="4ec3a-300">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-300">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ec3a-301">必要？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-301">Required?</span></span> |<span data-ttu-id="4ec3a-302">true</span><span class="sxs-lookup"><span data-stu-id="4ec3a-302">true</span></span> |
| <span data-ttu-id="4ec3a-303">位置？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-303">Position?</span></span> |<span data-ttu-id="4ec3a-304">0</span><span class="sxs-lookup"><span data-stu-id="4ec3a-304">0</span></span> |
| <span data-ttu-id="4ec3a-305">預設值</span><span class="sxs-lookup"><span data-stu-id="4ec3a-305">Default value</span></span> |<span data-ttu-id="4ec3a-306">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-306">none</span></span> |
| <span data-ttu-id="4ec3a-307">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-307">Accept pipeline input?</span></span> |<span data-ttu-id="4ec3a-308">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="4ec3a-308">true(ByPropertyName)</span></span> |
| <span data-ttu-id="4ec3a-309">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-309">Accept wildcard characters?</span></span> |<span data-ttu-id="4ec3a-310">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-310">false</span></span> |

<span data-ttu-id="4ec3a-311">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-311">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="4ec3a-312">指定媒體服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-312">Specifies the name of the media service.</span></span>

| <span data-ttu-id="4ec3a-313">別名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-313">Aliases</span></span> | <span data-ttu-id="4ec3a-314">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-314">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ec3a-315">必要？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-315">Required?</span></span> |<span data-ttu-id="4ec3a-316">true</span><span class="sxs-lookup"><span data-stu-id="4ec3a-316">true</span></span> |
| <span data-ttu-id="4ec3a-317">位置？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-317">Position?</span></span> |<span data-ttu-id="4ec3a-318">2</span><span class="sxs-lookup"><span data-stu-id="4ec3a-318">2</span></span> |
| <span data-ttu-id="4ec3a-319">預設值</span><span class="sxs-lookup"><span data-stu-id="4ec3a-319">Default value</span></span> |<span data-ttu-id="4ec3a-320">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-320">None</span></span> |
| <span data-ttu-id="4ec3a-321">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-321">Accept pipeline input?</span></span> |<span data-ttu-id="4ec3a-322">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="4ec3a-322">true(ByPropertyName)</span></span> |
| <span data-ttu-id="4ec3a-323">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-323">Accept wildcard characters?</span></span> |<span data-ttu-id="4ec3a-324">False</span><span class="sxs-lookup"><span data-stu-id="4ec3a-324">False</span></span> |

<span data-ttu-id="4ec3a-325">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-325">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="4ec3a-326">這個 Cmdlet 支援一般參數：-Debug、-ErrorAction、-ErrorVariable、-InformationAction、-InformationVariable、-OutVariable、-OutBuffer、-PipelineVariable、-Verbose、-WarningAction 和 -WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-326">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="4ec3a-327">輸入</span><span class="sxs-lookup"><span data-stu-id="4ec3a-327">Inputs</span></span>
<span data-ttu-id="4ec3a-328">輸入類型是可以透過管線傳送至 Cmdlet 的物件類型。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-328">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="4ec3a-329">輸出</span><span class="sxs-lookup"><span data-stu-id="4ec3a-329">Outputs</span></span>
<span data-ttu-id="4ec3a-330">輸出類型是 Cmdlet 所發出的物件類型。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-330">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="get-azurermmediaservice"></a><span data-ttu-id="4ec3a-331">Get-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="4ec3a-331">Get-AzureRmMediaService</span></span>
<span data-ttu-id="4ec3a-332">取得資源群組中的所有媒體服務或取得指定名稱的媒體服務。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-332">Gets all media services in a resource group or a media service with a given name.</span></span>

### <a name="syntax"></a><span data-ttu-id="4ec3a-333">語法</span><span class="sxs-lookup"><span data-stu-id="4ec3a-333">Syntax</span></span>
<span data-ttu-id="4ec3a-334">參數集：ResourceGroupParameterSet</span><span class="sxs-lookup"><span data-stu-id="4ec3a-334">ParameterSet: ResourceGroupParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

<span data-ttu-id="4ec3a-335">參數集：AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="4ec3a-335">ParameterSet: AccountNameParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="4ec3a-336">參數</span><span class="sxs-lookup"><span data-stu-id="4ec3a-336">Parameters</span></span>
<span data-ttu-id="4ec3a-337">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-337">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="4ec3a-338">指定此媒體服務所屬資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-338">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="4ec3a-339">別名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-339">Aliases</span></span> | <span data-ttu-id="4ec3a-340">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-340">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ec3a-341">必要？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-341">Required?</span></span> |<span data-ttu-id="4ec3a-342">true</span><span class="sxs-lookup"><span data-stu-id="4ec3a-342">true</span></span> |
| <span data-ttu-id="4ec3a-343">位置？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-343">Position?</span></span> |<span data-ttu-id="4ec3a-344">0</span><span class="sxs-lookup"><span data-stu-id="4ec3a-344">0</span></span> |
| <span data-ttu-id="4ec3a-345">預設值</span><span class="sxs-lookup"><span data-stu-id="4ec3a-345">Default value</span></span> |<span data-ttu-id="4ec3a-346">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-346">none</span></span> |
| <span data-ttu-id="4ec3a-347">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-347">Accept pipeline input?</span></span> |<span data-ttu-id="4ec3a-348">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="4ec3a-348">true(ByPropertyName)</span></span> |
| <span data-ttu-id="4ec3a-349">參數集名稱</span><span class="sxs-lookup"><span data-stu-id="4ec3a-349">Parameter set name</span></span> |<span data-ttu-id="4ec3a-350">ResourceGroupParameterSet、AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="4ec3a-350">ResourceGroupParameterSet, AccountNameParameterSet</span></span> |

<span data-ttu-id="4ec3a-351">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-351">Accept wildcard characters?</span></span>   <span data-ttu-id="4ec3a-352">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-352">false</span></span>

<span data-ttu-id="4ec3a-353">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-353">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="4ec3a-354">指定媒體服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-354">Specifies the name of the media service.</span></span>

| <span data-ttu-id="4ec3a-355">別名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-355">Aliases</span></span> | <span data-ttu-id="4ec3a-356">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-356">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ec3a-357">必要？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-357">Required?</span></span> |<span data-ttu-id="4ec3a-358">true</span><span class="sxs-lookup"><span data-stu-id="4ec3a-358">true</span></span> |
| <span data-ttu-id="4ec3a-359">位置？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-359">Position?</span></span> |<span data-ttu-id="4ec3a-360">1</span><span class="sxs-lookup"><span data-stu-id="4ec3a-360">1</span></span> |
| <span data-ttu-id="4ec3a-361">預設值</span><span class="sxs-lookup"><span data-stu-id="4ec3a-361">Default value</span></span> |<span data-ttu-id="4ec3a-362">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-362">none</span></span> |
| <span data-ttu-id="4ec3a-363">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-363">Accept pipeline input?</span></span> |<span data-ttu-id="4ec3a-364">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="4ec3a-364">true(ByPropertyName)</span></span> |
| <span data-ttu-id="4ec3a-365">參數集名稱</span><span class="sxs-lookup"><span data-stu-id="4ec3a-365">Parameter set name</span></span> |<span data-ttu-id="4ec3a-366">AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="4ec3a-366">AccountNameParameterSet</span></span> |
| <span data-ttu-id="4ec3a-367">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-367">Accept wildcard characters?</span></span> |<span data-ttu-id="4ec3a-368">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-368">false</span></span> |

<span data-ttu-id="4ec3a-369">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-369">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="4ec3a-370">這個 Cmdlet 支援一般參數：-Debug、-ErrorAction、-ErrorVariable、-InformationAction、-InformationVariable、-OutVariable、-OutBuffer、-PipelineVariable、-Verbose、-WarningAction 和 -WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-370">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="4ec3a-371">輸入</span><span class="sxs-lookup"><span data-stu-id="4ec3a-371">Inputs</span></span>
<span data-ttu-id="4ec3a-372">輸入類型是可以透過管線傳送至 Cmdlet 的物件類型。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-372">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="4ec3a-373">輸出</span><span class="sxs-lookup"><span data-stu-id="4ec3a-373">Outputs</span></span>
<span data-ttu-id="4ec3a-374">輸出類型是 Cmdlet 所發出的物件類型。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-374">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="get-azurermmediaservicekeys"></a><span data-ttu-id="4ec3a-375">Get-AzureRmMediaServiceKeys</span><span class="sxs-lookup"><span data-stu-id="4ec3a-375">Get-AzureRmMediaServiceKeys</span></span>
<span data-ttu-id="4ec3a-376">取得媒體服務的金鑰。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-376">Gets keys of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="4ec3a-377">語法</span><span class="sxs-lookup"><span data-stu-id="4ec3a-377">Syntax</span></span>
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="4ec3a-378">參數</span><span class="sxs-lookup"><span data-stu-id="4ec3a-378">Parameters</span></span>
<span data-ttu-id="4ec3a-379">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-379">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="4ec3a-380">指定此媒體服務所屬資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-380">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="4ec3a-381">別名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-381">Aliases</span></span> | <span data-ttu-id="4ec3a-382">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-382">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ec3a-383">必要？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-383">Required?</span></span> |<span data-ttu-id="4ec3a-384">true</span><span class="sxs-lookup"><span data-stu-id="4ec3a-384">true</span></span> |
| <span data-ttu-id="4ec3a-385">位置？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-385">Position?</span></span> |<span data-ttu-id="4ec3a-386">0</span><span class="sxs-lookup"><span data-stu-id="4ec3a-386">0</span></span> |
| <span data-ttu-id="4ec3a-387">預設值</span><span class="sxs-lookup"><span data-stu-id="4ec3a-387">Default value</span></span> |<span data-ttu-id="4ec3a-388">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-388">none</span></span> |
| <span data-ttu-id="4ec3a-389">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-389">Accept pipeline input?</span></span> |<span data-ttu-id="4ec3a-390">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="4ec3a-390">true(ByPropertyName)</span></span> |
| <span data-ttu-id="4ec3a-391">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-391">Accept wildcard characters?</span></span> |<span data-ttu-id="4ec3a-392">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-392">false</span></span> |

<span data-ttu-id="4ec3a-393">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-393">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="4ec3a-394">指定媒體服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-394">Specifies the name of the media service.</span></span>

| <span data-ttu-id="4ec3a-395">別名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-395">Aliases</span></span> | <span data-ttu-id="4ec3a-396">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-396">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ec3a-397">必要？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-397">Required?</span></span> |<span data-ttu-id="4ec3a-398">true</span><span class="sxs-lookup"><span data-stu-id="4ec3a-398">true</span></span> |
| <span data-ttu-id="4ec3a-399">位置？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-399">Position?</span></span> |<span data-ttu-id="4ec3a-400">1</span><span class="sxs-lookup"><span data-stu-id="4ec3a-400">1</span></span> |
| <span data-ttu-id="4ec3a-401">預設值</span><span class="sxs-lookup"><span data-stu-id="4ec3a-401">Default value</span></span> |<span data-ttu-id="4ec3a-402">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-402">none</span></span> |
| <span data-ttu-id="4ec3a-403">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-403">Accept pipeline input?</span></span> |<span data-ttu-id="4ec3a-404">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="4ec3a-404">true(ByPropertyName)</span></span> |
| <span data-ttu-id="4ec3a-405">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-405">Accept wildcard characters?</span></span> |<span data-ttu-id="4ec3a-406">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-406">false</span></span> |

<span data-ttu-id="4ec3a-407">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-407">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="4ec3a-408">這個 Cmdlet 支援一般參數：-Debug、-ErrorAction、-ErrorVariable、-InformationAction、-InformationVariable、-OutVariable、-OutBuffer、-PipelineVariable、-Verbose、-WarningAction 和 -WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-408">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="4ec3a-409">輸入</span><span class="sxs-lookup"><span data-stu-id="4ec3a-409">Inputs</span></span>
<span data-ttu-id="4ec3a-410">輸入類型是可以透過管線傳送至 Cmdlet 的物件類型。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-410">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="4ec3a-411">輸出</span><span class="sxs-lookup"><span data-stu-id="4ec3a-411">Outputs</span></span>
<span data-ttu-id="4ec3a-412">輸出類型是 Cmdlet 所發出的物件類型。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-412">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="set-azurermmediaservicekey"></a><span data-ttu-id="4ec3a-413">Set-AzureRmMediaServiceKey</span><span class="sxs-lookup"><span data-stu-id="4ec3a-413">Set-AzureRmMediaServiceKey</span></span>
<span data-ttu-id="4ec3a-414">重新產生媒體服務的主要或次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-414">Regenerates a primary or secondary key of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="4ec3a-415">語法</span><span class="sxs-lookup"><span data-stu-id="4ec3a-415">Syntax</span></span>
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="4ec3a-416">參數</span><span class="sxs-lookup"><span data-stu-id="4ec3a-416">Parameters</span></span>
<span data-ttu-id="4ec3a-417">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-417">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="4ec3a-418">指定此媒體服務所屬資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-418">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="4ec3a-419">別名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-419">Aliases</span></span> | <span data-ttu-id="4ec3a-420">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-420">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ec3a-421">必要？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-421">Required?</span></span> |<span data-ttu-id="4ec3a-422">true</span><span class="sxs-lookup"><span data-stu-id="4ec3a-422">true</span></span> |
| <span data-ttu-id="4ec3a-423">位置？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-423">Position?</span></span> |<span data-ttu-id="4ec3a-424">0</span><span class="sxs-lookup"><span data-stu-id="4ec3a-424">0</span></span> |
| <span data-ttu-id="4ec3a-425">預設值</span><span class="sxs-lookup"><span data-stu-id="4ec3a-425">Default value</span></span> |<span data-ttu-id="4ec3a-426">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-426">none</span></span> |
| <span data-ttu-id="4ec3a-427">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-427">Accept pipeline input?</span></span> |<span data-ttu-id="4ec3a-428">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="4ec3a-428">true(ByPropertyName)</span></span> |
| <span data-ttu-id="4ec3a-429">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-429">Accept wildcard characters?</span></span> |<span data-ttu-id="4ec3a-430">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-430">false</span></span> |

<span data-ttu-id="4ec3a-431">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-431">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="4ec3a-432">指定媒體服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-432">Specifies the name of the media service.</span></span>

| <span data-ttu-id="4ec3a-433">別名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-433">Aliases</span></span> | <span data-ttu-id="4ec3a-434">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-434">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ec3a-435">必要？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-435">Required?</span></span> |<span data-ttu-id="4ec3a-436">true</span><span class="sxs-lookup"><span data-stu-id="4ec3a-436">true</span></span> |
| <span data-ttu-id="4ec3a-437">位置？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-437">Position?</span></span> |<span data-ttu-id="4ec3a-438">1</span><span class="sxs-lookup"><span data-stu-id="4ec3a-438">1</span></span> |
| <span data-ttu-id="4ec3a-439">預設值</span><span class="sxs-lookup"><span data-stu-id="4ec3a-439">Default value</span></span> |<span data-ttu-id="4ec3a-440">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-440">none</span></span> |
| <span data-ttu-id="4ec3a-441">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-441">Accept pipeline input?</span></span> |<span data-ttu-id="4ec3a-442">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="4ec3a-442">true(ByPropertyName)</span></span> |
| <span data-ttu-id="4ec3a-443">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-443">Accept wildcard characters?</span></span> |<span data-ttu-id="4ec3a-444">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-444">false</span></span> |

<span data-ttu-id="4ec3a-445">**-KeyType &lt;KeyType&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-445">**-KeyType &lt;KeyType&gt;**</span></span>

<span data-ttu-id="4ec3a-446">指定媒體服務的金鑰類型。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-446">Specifies the key type of the media service.</span></span>

* <span data-ttu-id="4ec3a-447">主要或次要</span><span class="sxs-lookup"><span data-stu-id="4ec3a-447">Primary or Secondary</span></span>

| <span data-ttu-id="4ec3a-448">別名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-448">Aliases</span></span> | <span data-ttu-id="4ec3a-449">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-449">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ec3a-450">必要？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-450">Required?</span></span> |<span data-ttu-id="4ec3a-451">true</span><span class="sxs-lookup"><span data-stu-id="4ec3a-451">true</span></span> |
| <span data-ttu-id="4ec3a-452">位置？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-452">Position?</span></span> |<span data-ttu-id="4ec3a-453">2</span><span class="sxs-lookup"><span data-stu-id="4ec3a-453">2</span></span> |
| <span data-ttu-id="4ec3a-454">預設值</span><span class="sxs-lookup"><span data-stu-id="4ec3a-454">Default value</span></span> |<span data-ttu-id="4ec3a-455">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-455">none</span></span> |
| <span data-ttu-id="4ec3a-456">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-456">Accept pipeline input?</span></span> |<span data-ttu-id="4ec3a-457">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-457">false</span></span> |
| <span data-ttu-id="4ec3a-458">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-458">Accept wildcard characters?</span></span> |<span data-ttu-id="4ec3a-459">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-459">false</span></span> |

<span data-ttu-id="4ec3a-460">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-460">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="4ec3a-461">這個 Cmdlet 支援一般參數：-Debug、-ErrorAction、-ErrorVariable、-InformationAction、-InformationVariable、-OutVariable、-OutBuffer、-PipelineVariable、-Verbose、-WarningAction 和 -WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-461">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="4ec3a-462">輸入</span><span class="sxs-lookup"><span data-stu-id="4ec3a-462">Inputs</span></span>
<span data-ttu-id="4ec3a-463">輸入類型是可以透過管線傳送至 Cmdlet 的物件類型。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-463">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="4ec3a-464">輸出</span><span class="sxs-lookup"><span data-stu-id="4ec3a-464">Outputs</span></span>
<span data-ttu-id="4ec3a-465">輸出類型是 Cmdlet 所發出的物件類型。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-465">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="sync-azurermmediaservicestoragekeys"></a><span data-ttu-id="4ec3a-466">Sync-AzureRmMediaServiceStorageKeys</span><span class="sxs-lookup"><span data-stu-id="4ec3a-466">Sync-AzureRmMediaServiceStorageKeys</span></span>
<span data-ttu-id="4ec3a-467">同步處理與媒體服務相關聯之儲存體帳戶的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-467">Synchronizes storage account keys for a storage account associated with the media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="4ec3a-468">語法</span><span class="sxs-lookup"><span data-stu-id="4ec3a-468">Syntax</span></span>
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="4ec3a-469">參數</span><span class="sxs-lookup"><span data-stu-id="4ec3a-469">Parameters</span></span>
<span data-ttu-id="4ec3a-470">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-470">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="4ec3a-471">指定此媒體服務所屬資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-471">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="4ec3a-472">別名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-472">Aliases</span></span> | <span data-ttu-id="4ec3a-473">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-473">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ec3a-474">必要？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-474">Required?</span></span> |<span data-ttu-id="4ec3a-475">true</span><span class="sxs-lookup"><span data-stu-id="4ec3a-475">true</span></span> |
| <span data-ttu-id="4ec3a-476">位置？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-476">Position?</span></span> |<span data-ttu-id="4ec3a-477">0</span><span class="sxs-lookup"><span data-stu-id="4ec3a-477">0</span></span> |
| <span data-ttu-id="4ec3a-478">預設值</span><span class="sxs-lookup"><span data-stu-id="4ec3a-478">Default value</span></span> |<span data-ttu-id="4ec3a-479">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-479">none</span></span> |
| <span data-ttu-id="4ec3a-480">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-480">Accept pipeline input?</span></span> |<span data-ttu-id="4ec3a-481">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="4ec3a-481">true(ByPropertyName)</span></span> |
| <span data-ttu-id="4ec3a-482">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-482">Accept wildcard characters?</span></span> |<span data-ttu-id="4ec3a-483">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-483">false</span></span> |

<span data-ttu-id="4ec3a-484">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-484">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="4ec3a-485">指定媒體服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-485">Specifies the name of the media service.</span></span>

| <span data-ttu-id="4ec3a-486">別名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-486">Aliases</span></span> | <span data-ttu-id="4ec3a-487">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-487">none</span></span> |
| --- | --- |
| <span data-ttu-id="4ec3a-488">必要？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-488">Required?</span></span> |<span data-ttu-id="4ec3a-489">true</span><span class="sxs-lookup"><span data-stu-id="4ec3a-489">true</span></span> |
| <span data-ttu-id="4ec3a-490">位置？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-490">Position?</span></span> |<span data-ttu-id="4ec3a-491">1</span><span class="sxs-lookup"><span data-stu-id="4ec3a-491">1</span></span> |
| <span data-ttu-id="4ec3a-492">預設值</span><span class="sxs-lookup"><span data-stu-id="4ec3a-492">Default value</span></span> |<span data-ttu-id="4ec3a-493">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-493">none</span></span> |
| <span data-ttu-id="4ec3a-494">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-494">Accept pipeline input?</span></span> |<span data-ttu-id="4ec3a-495">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="4ec3a-495">true(ByPropertyName)</span></span> |
| <span data-ttu-id="4ec3a-496">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-496">Accept wildcard characters?</span></span> |<span data-ttu-id="4ec3a-497">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-497">false</span></span> |

<span data-ttu-id="4ec3a-498">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-498">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="4ec3a-499">指定與媒體服務相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-499">Specifies the storage account associated with the media service.</span></span>

| <span data-ttu-id="4ec3a-500">別名</span><span class="sxs-lookup"><span data-stu-id="4ec3a-500">Aliases</span></span> | <span data-ttu-id="4ec3a-501">識別碼</span><span class="sxs-lookup"><span data-stu-id="4ec3a-501">Id</span></span> |
| --- | --- |
| <span data-ttu-id="4ec3a-502">必要？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-502">Required?</span></span> |<span data-ttu-id="4ec3a-503">true</span><span class="sxs-lookup"><span data-stu-id="4ec3a-503">true</span></span> |
| <span data-ttu-id="4ec3a-504">位置？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-504">Position?</span></span> |<span data-ttu-id="4ec3a-505">2</span><span class="sxs-lookup"><span data-stu-id="4ec3a-505">2</span></span> |
| <span data-ttu-id="4ec3a-506">預設值</span><span class="sxs-lookup"><span data-stu-id="4ec3a-506">Default value</span></span> |<span data-ttu-id="4ec3a-507">無</span><span class="sxs-lookup"><span data-stu-id="4ec3a-507">none</span></span> |
| <span data-ttu-id="4ec3a-508">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-508">Accept pipeline input?</span></span> |<span data-ttu-id="4ec3a-509">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="4ec3a-509">true(ByPropertyName)</span></span> |
| <span data-ttu-id="4ec3a-510">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="4ec3a-510">Accept wildcard characters?</span></span> |<span data-ttu-id="4ec3a-511">false</span><span class="sxs-lookup"><span data-stu-id="4ec3a-511">false</span></span> |

<span data-ttu-id="4ec3a-512">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="4ec3a-512">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="4ec3a-513">這個 Cmdlet 支援一般參數：-Debug、-ErrorAction、-ErrorVariable、-InformationAction、-InformationVariable、-OutVariable、-OutBuffer、-PipelineVariable、-Verbose、-WarningAction 和 -WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-513">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="4ec3a-514">輸入</span><span class="sxs-lookup"><span data-stu-id="4ec3a-514">Inputs</span></span>
<span data-ttu-id="4ec3a-515">輸入類型是可以透過管線傳送至 Cmdlet 的物件類型。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-515">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="4ec3a-516">輸出</span><span class="sxs-lookup"><span data-stu-id="4ec3a-516">Outputs</span></span>
<span data-ttu-id="4ec3a-517">輸出類型是 Cmdlet 所發出的物件類型。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-517">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="next-step"></a><span data-ttu-id="4ec3a-518">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4ec3a-518">Next step</span></span>
<span data-ttu-id="4ec3a-519">查看媒體服務學習途徑。</span><span class="sxs-lookup"><span data-stu-id="4ec3a-519">Check out Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4ec3a-520">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="4ec3a-520">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

