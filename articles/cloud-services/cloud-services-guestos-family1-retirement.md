---
title: "客體 OS 系列 1 淘汰通知 | Microsoft Docs"
description: "提供客體作業系統系列 1 淘汰時間及如何自行判斷是否受影響等相關資訊"
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 37b422e9-0713-4a81-a942-f553ef478064
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/21/2017
ms.author: raiye
ms.openlocfilehash: 3178a09dab1cb972a3460d54dc9908fb95cce68b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="guest-os-family-1-retirement-notice"></a><span data-ttu-id="08da9-103">客體作業系統系列 1 淘汰通知</span><span class="sxs-lookup"><span data-stu-id="08da9-103">Guest OS Family 1 retirement notice</span></span>
<span data-ttu-id="08da9-104">我們早在 2013 年 6 月 1 日宣佈客體作業系統系列 1 的淘汰資訊。</span><span class="sxs-lookup"><span data-stu-id="08da9-104">The retirement of OS Family 1 was first announced on June 1, 2013.</span></span>

<span data-ttu-id="08da9-105">**2014 年 9 月 2 日** 以 Windows Server 2008 作業系統為基礎的 Azure 客體作業系統 (客體 OS) 系列 1.x 已正式淘汰。</span><span class="sxs-lookup"><span data-stu-id="08da9-105">**Sept 2, 2014** The Azure Guest operating system (Guest OS) Family 1.x, which is based on the Windows Server 2008 operating system, was officially retired.</span></span> <span data-ttu-id="08da9-106">所有使用系列 1 部署新服務或升級現有服務的嘗試均會失敗並且會出現錯誤訊息，通知您客體作業系統系列 1 已遭到淘汰。</span><span class="sxs-lookup"><span data-stu-id="08da9-106">All attempts to deploy new services or upgrade existing services using Family 1 will fail with an error message informing you that the Guest OS Family 1 has been retired.</span></span>

<span data-ttu-id="08da9-107">**2014 年 11 月 3 日** 客體 OS 系列 1 的延伸支援已結束，並且已完全淘汰。</span><span class="sxs-lookup"><span data-stu-id="08da9-107">**November 3, 2014** Extended support for Guest OS Family 1 ended and it is fully retired.</span></span> <span data-ttu-id="08da9-108">所有仍以系列 1 為基礎的服務都將受到影響。</span><span class="sxs-lookup"><span data-stu-id="08da9-108">All services still on Family 1 will be impacted.</span></span> <span data-ttu-id="08da9-109">我們可能會隨時停止這些服務。</span><span class="sxs-lookup"><span data-stu-id="08da9-109">We may stop those services at any time.</span></span> <span data-ttu-id="08da9-110">除非您以手動方式自行升級服務，否則我們不保證您的服務能繼續運作。</span><span class="sxs-lookup"><span data-stu-id="08da9-110">There is no guarantee your services will continue to run unless you manually upgrade them yourself.</span></span>

<span data-ttu-id="08da9-111">如果您有其他問題，請前往[雲端服務論壇](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc)或[連絡 Azure 支援](https://azure.microsoft.com/support/options/)。</span><span class="sxs-lookup"><span data-stu-id="08da9-111">If you have additional questions, visit the [Cloud Services Forums](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) or [contact Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="are-you-affected"></a><span data-ttu-id="08da9-112">您受到影響了嗎？</span><span class="sxs-lookup"><span data-stu-id="08da9-112">Are you affected?</span></span>
<span data-ttu-id="08da9-113">如果以下任一情況成立，表示您的雲端服務已受到影響：</span><span class="sxs-lookup"><span data-stu-id="08da9-113">Your Cloud Services are affected if any one of the following applies:</span></span>

1. <span data-ttu-id="08da9-114">雲端服務之 ServiceConfiguration.cscfg 檔案明確地指定 "osFamily = "1" 值。</span><span class="sxs-lookup"><span data-stu-id="08da9-114">You have a value of "osFamily = "1" explicitly specified in the ServiceConfiguration.cscfg file for your Cloud Service.</span></span>
2. <span data-ttu-id="08da9-115">雲端服務之 ServiceConfiguration.cscfg 檔案未明確指定 osFamily 的值。</span><span class="sxs-lookup"><span data-stu-id="08da9-115">You do not have a value for osFamily explicitly specified in the ServiceConfiguration.cscfg file for your Cloud Service.</span></span> <span data-ttu-id="08da9-116">在本案例中，系統目前使用預設值 "1" 。</span><span class="sxs-lookup"><span data-stu-id="08da9-116">Currently, the system uses the default value of "1" in this case.</span></span>
3. <span data-ttu-id="08da9-117">Azure 入口網站會將您的客體作業系統系列值列為 "Windows Server 2008"。</span><span class="sxs-lookup"><span data-stu-id="08da9-117">The Azure portal lists your Guest Operating System family value as "Windows Server 2008".</span></span>

<span data-ttu-id="08da9-118">若要找出每個雲端服務執行的作業系統系列，您可以在 Azure PowerShell 中執行下列程式碼，但請先[設定 Azure PowerShell](/powershell/azureps-cmdlets-docs) 。</span><span class="sxs-lookup"><span data-stu-id="08da9-118">To find which of your cloud services are running which OS Family, you can run the following script in Azure PowerShell, though you must [set up Azure PowerShell](/powershell/azureps-cmdlets-docs) first.</span></span> <span data-ttu-id="08da9-119">如需指令碼的詳細資訊，請參閱 [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx) (Azure 客體 OS 系列 1 生命週期結束：2014 年 6 月)。</span><span class="sxs-lookup"><span data-stu-id="08da9-119">For more information on the script, see [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span></span>

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

<span data-ttu-id="08da9-120">如果指令碼輸出中 osFamily 資料行為空白或含有 "1"，代表您的雲端服務將受到作業系統系列 1 淘汰所影響。</span><span class="sxs-lookup"><span data-stu-id="08da9-120">Your cloud services will be impacted by OS Family 1 retirement if the osFamily column in the script output is empty or contains a "1".</span></span>

## <a name="recommendations-if-you-are-affected"></a><span data-ttu-id="08da9-121">受影響時的建議</span><span class="sxs-lookup"><span data-stu-id="08da9-121">Recommendations if you are affected</span></span>
<span data-ttu-id="08da9-122">我們建議您將雲端服務角色移轉到任一個受支援的客體作業系統系列：</span><span class="sxs-lookup"><span data-stu-id="08da9-122">We recommend you migrate your Cloud Service roles to one of the supported Guest OS Families:</span></span>

<span data-ttu-id="08da9-123">**客體 OS 系列 4.x** - Windows Server 2012 R2 *(建議選項)*</span><span class="sxs-lookup"><span data-stu-id="08da9-123">**Guest OS family 4.x** - Windows Server 2012 R2 *(recommended)*</span></span>

1. <span data-ttu-id="08da9-124">請確認您的應用程式使用 SDK 2.1 或更新版本，搭配 .NET Framework 4.0、4.5 或 4.5.1。</span><span class="sxs-lookup"><span data-stu-id="08da9-124">Ensure that your application is using SDK 2.1 or later with .NET framework 4.0, 4.5 or 4.5.1.</span></span>
2. <span data-ttu-id="08da9-125">在 ServiceConfiguration.cscfg 檔案中將 osFamily 屬性設定為 "4" 的，然後重新部署雲端服務。</span><span class="sxs-lookup"><span data-stu-id="08da9-125">Set the osFamily attribute to “4” in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="08da9-126">**客體 OS 系列 3.x** - Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="08da9-126">**Guest OS family 3.x** - Windows Server 2012</span></span>

1. <span data-ttu-id="08da9-127">請確認您的應用程式使用 SDK 1.8 或更新版本，搭配 .NET Framework 4.0 或 4.5。</span><span class="sxs-lookup"><span data-stu-id="08da9-127">Ensure that your application is using SDK 1.8 or later with .NET framework 4.0 or 4.5.</span></span>
2. <span data-ttu-id="08da9-128">在 ServiceConfiguration.cscfg 檔案中將 osFamily 屬性設定為「3」，然後重新部署雲端服務。</span><span class="sxs-lookup"><span data-stu-id="08da9-128">Set the osFamily attribute to “3” in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="08da9-129">**客體 OS 系列 2.x** - Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="08da9-129">**Guest OS family 2.x** - Windows Server 2008 R2</span></span>

1. <span data-ttu-id="08da9-130">請確認您的應用程式使用 SDK 1.3 和更新版本，搭配 .NET Framework 3.5 或 4.0。</span><span class="sxs-lookup"><span data-stu-id="08da9-130">Ensure that your application is using SDK 1.3 and above with .NET framework 3.5 or 4.0.</span></span>
2. <span data-ttu-id="08da9-131">在 ServiceConfiguration.cscfg 檔案中將 osFamily 屬性設定為 "2" 的，然後重新部署雲端服務。</span><span class="sxs-lookup"><span data-stu-id="08da9-131">Set the osFamily attribute to "2" in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a><span data-ttu-id="08da9-132">客體作業系統系列 1 的延長支援已在 2014 年 11 月 3 日結束。</span><span class="sxs-lookup"><span data-stu-id="08da9-132">Extended Support for Guest OS Family 1 ended Nov 3, 2014</span></span>
<span data-ttu-id="08da9-133">以客體作業系統系列 1 為基礎的雲端服務將不再受到支援。</span><span class="sxs-lookup"><span data-stu-id="08da9-133">Cloud services on Guest OS family 1 are no longer supported.</span></span> <span data-ttu-id="08da9-134">請儘早移轉系列 1 以避免服務中斷。</span><span class="sxs-lookup"><span data-stu-id="08da9-134">Migrate off family 1 as soon as possible to avoid service disruption.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="08da9-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="08da9-135">Next steps</span></span>
<span data-ttu-id="08da9-136">檢閱最新的 [客體作業系統版本](cloud-services-guestos-update-matrix.md)。</span><span class="sxs-lookup"><span data-stu-id="08da9-136">Review the latest [Guest OS releases](cloud-services-guestos-update-matrix.md).</span></span>
