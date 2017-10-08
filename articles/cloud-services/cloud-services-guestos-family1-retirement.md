---
title: "請注意 aaaGuest OS 系列 1 淘汰 |Microsoft 文件"
description: "提供下列相關資訊以及 hello Azure 客體作業系統系列 1 淘汰發生時如何 toodetermine 如果影響"
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
ms.openlocfilehash: fa8b904c6560dbbe4982c301f818c7a5cbc4eacb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="guest-os-family-1-retirement-notice"></a><span data-ttu-id="94e43-103">客體作業系統系列 1 淘汰通知</span><span class="sxs-lookup"><span data-stu-id="94e43-103">Guest OS Family 1 retirement notice</span></span>
<span data-ttu-id="94e43-104">2013 年 6 月 1 日首次宣佈淘汰作業系統系列 1 hello。</span><span class="sxs-lookup"><span data-stu-id="94e43-104">hello retirement of OS Family 1 was first announced on June 1, 2013.</span></span>

<span data-ttu-id="94e43-105">**2014 年 9 月 2 日**hello Azure 客體作業系統 (客體 OS) 系列 1.x 以 hello Windows Server 2008 作業系統為基礎，正式淘汰。</span><span class="sxs-lookup"><span data-stu-id="94e43-105">**Sept 2, 2014** hello Azure Guest operating system (Guest OS) Family 1.x, which is based on hello Windows Server 2008 operating system, was officially retired.</span></span> <span data-ttu-id="94e43-106">所有嘗試 toodeploy 新服務或升級現有的服務使用系列 1 已淘汰客體 OS 系列 1 的錯誤訊息通知您該 hello 將會都失敗。</span><span class="sxs-lookup"><span data-stu-id="94e43-106">All attempts toodeploy new services or upgrade existing services using Family 1 will fail with an error message informing you that hello Guest OS Family 1 has been retired.</span></span>

<span data-ttu-id="94e43-107">**2014 年 11 月 3 日** 客體 OS 系列 1 的延伸支援已結束，並且已完全淘汰。</span><span class="sxs-lookup"><span data-stu-id="94e43-107">**November 3, 2014** Extended support for Guest OS Family 1 ended and it is fully retired.</span></span> <span data-ttu-id="94e43-108">所有仍以系列 1 為基礎的服務都將受到影響。</span><span class="sxs-lookup"><span data-stu-id="94e43-108">All services still on Family 1 will be impacted.</span></span> <span data-ttu-id="94e43-109">我們可能會隨時停止這些服務。</span><span class="sxs-lookup"><span data-stu-id="94e43-109">We may stop those services at any time.</span></span> <span data-ttu-id="94e43-110">沒有保證您的服務將繼續 toorun，除非您自行手動升級它們。</span><span class="sxs-lookup"><span data-stu-id="94e43-110">There is no guarantee your services will continue toorun unless you manually upgrade them yourself.</span></span>

<span data-ttu-id="94e43-111">如果您有其他問題，請瀏覽 hello[雲端服務論壇](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc)或[連絡 Azure 支援](https://azure.microsoft.com/support/options/)。</span><span class="sxs-lookup"><span data-stu-id="94e43-111">If you have additional questions, visit hello [Cloud Services Forums](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) or [contact Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="are-you-affected"></a><span data-ttu-id="94e43-112">您受到影響了嗎？</span><span class="sxs-lookup"><span data-stu-id="94e43-112">Are you affected?</span></span>
<span data-ttu-id="94e43-113">您的雲端服務會受到影響，如果 hello 下列任何一個適用於：</span><span class="sxs-lookup"><span data-stu-id="94e43-113">Your Cloud Services are affected if any one of hello following applies:</span></span>

1. <span data-ttu-id="94e43-114">值為"osFamily ="1"為您的雲端服務 hello ServiceConfiguration.cscfg 檔案中明確指定。</span><span class="sxs-lookup"><span data-stu-id="94e43-114">You have a value of "osFamily = "1" explicitly specified in hello ServiceConfiguration.cscfg file for your Cloud Service.</span></span>
2. <span data-ttu-id="94e43-115">您沒有為您的雲端服務 hello ServiceConfiguration.cscfg 檔案中明確指定的 osFamily 的值。</span><span class="sxs-lookup"><span data-stu-id="94e43-115">You do not have a value for osFamily explicitly specified in hello ServiceConfiguration.cscfg file for your Cloud Service.</span></span> <span data-ttu-id="94e43-116">目前，hello 系統會在此情況下使用 hello 預設值為"1"。</span><span class="sxs-lookup"><span data-stu-id="94e43-116">Currently, hello system uses hello default value of "1" in this case.</span></span>
3. <span data-ttu-id="94e43-117">hello Azure 入口網站列出的客體作業系統系列值為"Windows Server 2008"。</span><span class="sxs-lookup"><span data-stu-id="94e43-117">hello Azure portal lists your Guest Operating System family value as "Windows Server 2008".</span></span>

<span data-ttu-id="94e43-118">toofind 正在執行哪個作業系統系列的雲端服務，您可以執行下列指令碼在 Azure PowerShell 中的 hello，但您必須[設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)第一次。</span><span class="sxs-lookup"><span data-stu-id="94e43-118">toofind which of your cloud services are running which OS Family, you can run hello following script in Azure PowerShell, though you must [set up Azure PowerShell](/powershell/azureps-cmdlets-docs) first.</span></span> <span data-ttu-id="94e43-119">如需有關 hello 指令碼的詳細資訊，請參閱[Azure 客體 OS 系列 1 生命週期結束： 2014 年 6 月](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx)。</span><span class="sxs-lookup"><span data-stu-id="94e43-119">For more information on hello script, see [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span></span>

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

<span data-ttu-id="94e43-120">您的雲端服務將受到作業系統系列 1 淘汰如果 hello 指令碼輸出中的 hello osFamily 資料行是空的或包含"1"。</span><span class="sxs-lookup"><span data-stu-id="94e43-120">Your cloud services will be impacted by OS Family 1 retirement if hello osFamily column in hello script output is empty or contains a "1".</span></span>

## <a name="recommendations-if-you-are-affected"></a><span data-ttu-id="94e43-121">受影響時的建議</span><span class="sxs-lookup"><span data-stu-id="94e43-121">Recommendations if you are affected</span></span>
<span data-ttu-id="94e43-122">我們建議您移轉您的 hello 支援的客體作業系統系列的雲端服務角色 tooone:</span><span class="sxs-lookup"><span data-stu-id="94e43-122">We recommend you migrate your Cloud Service roles tooone of hello supported Guest OS Families:</span></span>

<span data-ttu-id="94e43-123">**客體 OS 系列 4.x** - Windows Server 2012 R2 *(建議選項)*</span><span class="sxs-lookup"><span data-stu-id="94e43-123">**Guest OS family 4.x** - Windows Server 2012 R2 *(recommended)*</span></span>

1. <span data-ttu-id="94e43-124">請確認您的應用程式使用 SDK 2.1 或更新版本，搭配 .NET Framework 4.0、4.5 或 4.5.1。</span><span class="sxs-lookup"><span data-stu-id="94e43-124">Ensure that your application is using SDK 2.1 or later with .NET framework 4.0, 4.5 or 4.5.1.</span></span>
2. <span data-ttu-id="94e43-125">設定 hello osFamily 屬性太"4 的 「 在 hello ServiceConfiguration.cscfg 檔案，並重新部署雲端服務。</span><span class="sxs-lookup"><span data-stu-id="94e43-125">Set hello osFamily attribute too“4” in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="94e43-126">**客體 OS 系列 3.x** - Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="94e43-126">**Guest OS family 3.x** - Windows Server 2012</span></span>

1. <span data-ttu-id="94e43-127">請確認您的應用程式使用 SDK 1.8 或更新版本，搭配 .NET Framework 4.0 或 4.5。</span><span class="sxs-lookup"><span data-stu-id="94e43-127">Ensure that your application is using SDK 1.8 or later with .NET framework 4.0 or 4.5.</span></span>
2. <span data-ttu-id="94e43-128">設定 hello osFamily 屬性太"3 的"中的 hello ServiceConfiguration.cscfg 檔案，並重新部署雲端服務。</span><span class="sxs-lookup"><span data-stu-id="94e43-128">Set hello osFamily attribute too“3” in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="94e43-129">**客體 OS 系列 2.x** - Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="94e43-129">**Guest OS family 2.x** - Windows Server 2008 R2</span></span>

1. <span data-ttu-id="94e43-130">請確認您的應用程式使用 SDK 1.3 和更新版本，搭配 .NET Framework 3.5 或 4.0。</span><span class="sxs-lookup"><span data-stu-id="94e43-130">Ensure that your application is using SDK 1.3 and above with .NET framework 3.5 or 4.0.</span></span>
2. <span data-ttu-id="94e43-131">設定 hello osFamily 屬性太"2 的"中的 hello ServiceConfiguration.cscfg 檔案，並重新部署雲端服務。</span><span class="sxs-lookup"><span data-stu-id="94e43-131">Set hello osFamily attribute too"2" in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a><span data-ttu-id="94e43-132">客體作業系統系列 1 的延長支援已在 2014 年 11 月 3 日結束。</span><span class="sxs-lookup"><span data-stu-id="94e43-132">Extended Support for Guest OS Family 1 ended Nov 3, 2014</span></span>
<span data-ttu-id="94e43-133">以客體作業系統系列 1 為基礎的雲端服務將不再受到支援。</span><span class="sxs-lookup"><span data-stu-id="94e43-133">Cloud services on Guest OS family 1 are no longer supported.</span></span> <span data-ttu-id="94e43-134">速移轉系列 1 儘速可能 tooavoid 服務中斷。</span><span class="sxs-lookup"><span data-stu-id="94e43-134">Migrate off family 1 as soon as possible tooavoid service disruption.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="94e43-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="94e43-135">Next steps</span></span>
<span data-ttu-id="94e43-136">最新檢閱 hello[客體 OS 版本](cloud-services-guestos-update-matrix.md)。</span><span class="sxs-lookup"><span data-stu-id="94e43-136">Review hello latest [Guest OS releases](cloud-services-guestos-update-matrix.md).</span></span>
