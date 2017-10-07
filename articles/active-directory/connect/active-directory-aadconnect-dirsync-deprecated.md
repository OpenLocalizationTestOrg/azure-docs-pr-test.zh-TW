---
title: "從 DirSync 和 Azure AD Sync aaaUpgrade |Microsoft 文件"
description: "描述如何從 DirSync 和 Azure AD Sync tooAzure AD tooupgrade 連接。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: bd68fb88-110b-4d76-978a-233e15590803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d465b137fb54f0c6e28ccf73429c4bd3aafd8698
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-windows-azure-active-directory-sync-and-azure-active-directory-sync"></a><span data-ttu-id="23d6d-103">升級 Windows Azure Active Directory Sync 和 Azure Active Directory Sync</span><span class="sxs-lookup"><span data-stu-id="23d6d-103">Upgrade Windows Azure Active Directory Sync and Azure Active Directory Sync</span></span>
<span data-ttu-id="23d6d-104">Azure AD Connect 是 hello 最佳方式 tooconnect 在內部部署目錄與 Azure AD 和 Office 365。</span><span class="sxs-lookup"><span data-stu-id="23d6d-104">Azure AD Connect is hello best way tooconnect your on-premises directory with Azure AD and Office 365.</span></span> <span data-ttu-id="23d6d-105">這是很好的時間 tooupgrade tooAzure AD Connect，從 Windows Azure Active Directory 同步作業 (DirSync) 或 Azure AD Sync 因為這些工具現在已被取代，並會到達結束在 2017 年 4 月 13，支援。</span><span class="sxs-lookup"><span data-stu-id="23d6d-105">This is a great time tooupgrade tooAzure AD Connect from Windows Azure Active Directory Sync (DirSync) or Azure AD Sync as these tools are now deprecated and will reach end of support on April 13, 2017.</span></span>

<span data-ttu-id="23d6d-106">已被取代的 hello 兩個身分識別同步處理工具所提供的單一樹系的客戶 (DirSync) 和多樹系和其他進階的客戶 （Azure AD 同步處理）。</span><span class="sxs-lookup"><span data-stu-id="23d6d-106">hello two identity synchronization tools that are deprecated were offered for single forest customers (DirSync) and for multi-forest and other advanced customers (Azure AD Sync).</span></span> <span data-ttu-id="23d6d-107">這些較舊的工具已經取代為適用於所有案例的單一解決方案︰Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="23d6d-107">These older tools have been replaced with a single solution that is available for all scenarios: Azure AD Connect.</span></span> <span data-ttu-id="23d6d-108">它提供新的功能、增強功能和新案例的支援。</span><span class="sxs-lookup"><span data-stu-id="23d6d-108">It offers new functionality, feature enhancements, and support for new scenarios.</span></span> <span data-ttu-id="23d6d-109">toobe 無法 toocontinue toosynchronize 您的內部部署身分識別資料 tooAzure AD 和 Office 365，我們強烈建議您升級 tooAzure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="23d6d-109">toobe able toocontinue toosynchronize your on-premises identity data tooAzure AD and Office 365, we strongly recommend that you upgrade tooAzure AD Connect.</span></span>

<span data-ttu-id="23d6d-110">DirSync hello 最後一個版本已於 2014 年 7 月發行和 hello 的 Azure AD Sync 的最後一個版本已於 2015 年發行。</span><span class="sxs-lookup"><span data-stu-id="23d6d-110">hello last release of DirSync was released in July 2014 and hello last release of Azure AD Sync was released in May 2015.</span></span>

## <a name="what-is-azure-ad-connect"></a><span data-ttu-id="23d6d-111">何謂 Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="23d6d-111">What is Azure AD Connect</span></span>
<span data-ttu-id="23d6d-112">Azure AD Connect 是 hello 後續 tooDirSync 和 Azure AD Sync。它結合了兩者支援的所有案例。</span><span class="sxs-lookup"><span data-stu-id="23d6d-112">Azure AD Connect is hello successor tooDirSync and Azure AD Sync. It combines all scenarios these two supported.</span></span> <span data-ttu-id="23d6d-113">您可以在 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)中進一步了解。</span><span class="sxs-lookup"><span data-stu-id="23d6d-113">You can read more about it in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="deprecation-schedule"></a><span data-ttu-id="23d6d-114">淘汰排程</span><span class="sxs-lookup"><span data-stu-id="23d6d-114">Deprecation schedule</span></span>
| <span data-ttu-id="23d6d-115">Date</span><span class="sxs-lookup"><span data-stu-id="23d6d-115">Date</span></span> | <span data-ttu-id="23d6d-116">註解</span><span class="sxs-lookup"><span data-stu-id="23d6d-116">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="23d6d-117">2016 年 4 月 13 日</span><span class="sxs-lookup"><span data-stu-id="23d6d-117">April 13, 2016</span></span> |<span data-ttu-id="23d6d-118">Windows Azure Active Directory Sync (“DirSync”) 和 Microsoft Azure Active Directory Sync (“Azure AD Sync”) 已宣布淘汰。</span><span class="sxs-lookup"><span data-stu-id="23d6d-118">Windows Azure Active Directory Sync (“DirSync”) and Microsoft Azure Active Directory Sync (“Azure AD Sync”) are announced as deprecated.</span></span> |
| <span data-ttu-id="23d6d-119">2017 年 4 月 13 日</span><span class="sxs-lookup"><span data-stu-id="23d6d-119">April 13, 2017</span></span> |<span data-ttu-id="23d6d-120">支援結束。</span><span class="sxs-lookup"><span data-stu-id="23d6d-120">Support ends.</span></span> <span data-ttu-id="23d6d-121">客戶將不再能夠 tooopen 支援案例，而不升級 tooAzure AD 先連線。</span><span class="sxs-lookup"><span data-stu-id="23d6d-121">Customers will no longer be able tooopen a support case without upgrading tooAzure AD Connect first.</span></span> |
|<span data-ttu-id="23d6d-122">2017 年 12 月 31 日</span><span class="sxs-lookup"><span data-stu-id="23d6d-122">December 31, 2017</span></span>|<span data-ttu-id="23d6d-123">Azure AD 已不再接受來自 Windows Azure Active Directory Sync (“DirSync”) 和 Microsoft Azure Active Directory Sync (“Azure AD Sync”) 的通訊。</span><span class="sxs-lookup"><span data-stu-id="23d6d-123">Azure AD will no longer accept communications from Windows Azure Active Directory Sync (“DirSync”) and Microsoft Azure Active Directory Sync (“Azure AD Sync”).</span></span>

## <a name="how-tootransition-tooazure-ad-connect"></a><span data-ttu-id="23d6d-124">如何 tootransition tooAzure AD Connect</span><span class="sxs-lookup"><span data-stu-id="23d6d-124">How tootransition tooAzure AD Connect</span></span>
<span data-ttu-id="23d6d-125">如果您正在執行 DirSync，有兩種方式可以升級︰就地升級和平行部署。</span><span class="sxs-lookup"><span data-stu-id="23d6d-125">If you are running DirSync, there are two ways you can upgrade: In-place upgrade and parallel deployment.</span></span> <span data-ttu-id="23d6d-126">對大多數的客戶，以及如果您擁有最新的作業系統和少於 50,000 個物件，建議採用就地升級。</span><span class="sxs-lookup"><span data-stu-id="23d6d-126">An in-place upgrade is recommended for most customers and if you have a recent operating system and less than 50,000 objects.</span></span> <span data-ttu-id="23d6d-127">在其他情況下，建議您使用 toodo 平行部署，其中是您的 DirSync 組態移動 tooa 執行 Azure AD Connect 的新伺服器。</span><span class="sxs-lookup"><span data-stu-id="23d6d-127">In other cases, it is recommended toodo a parallel deployment where your DirSync configuration is moved tooa new server running Azure AD Connect.</span></span>

<span data-ttu-id="23d6d-128">如果您使用 Azure AD Sync，則建議採用就地升級。</span><span class="sxs-lookup"><span data-stu-id="23d6d-128">If you use Azure AD Sync, then an in-place upgrade is recommended.</span></span> <span data-ttu-id="23d6d-129">如果您想要它是可能 tooinstall 新的 Azure AD Connect 伺服器，以平行方式，和執行來自您 Azure AD 同步伺服器 tooAzure AD 迴旋移轉連接。</span><span class="sxs-lookup"><span data-stu-id="23d6d-129">If you want to, it is possible tooinstall a new Azure AD Connect server in parallel and do a swing migration from your Azure AD Sync server tooAzure AD Connect.</span></span>

| <span data-ttu-id="23d6d-130">方案</span><span class="sxs-lookup"><span data-stu-id="23d6d-130">Solution</span></span> | <span data-ttu-id="23d6d-131">案例</span><span class="sxs-lookup"><span data-stu-id="23d6d-131">Scenario</span></span> |
| --- | --- |
| [<span data-ttu-id="23d6d-132">從 DirSync 升級</span><span class="sxs-lookup"><span data-stu-id="23d6d-132">Upgrade from DirSync</span></span>](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li><span data-ttu-id="23d6d-133">如果您有已在執行中的現有 DirSync 伺服器。</span><span class="sxs-lookup"><span data-stu-id="23d6d-133">If you have an existing DirSync server already running.</span></span></li> |
| [<span data-ttu-id="23d6d-134">從 Azure AD Sync 升級</span><span class="sxs-lookup"><span data-stu-id="23d6d-134">Upgrade from Azure AD Sync</span></span>](active-directory-aadconnect-upgrade-previous-version.md) |<li><span data-ttu-id="23d6d-135">如果您要從 Azure AD Sync 移動。</span><span class="sxs-lookup"><span data-stu-id="23d6d-135">If you are moving from Azure AD Sync.</span></span></li> |

<span data-ttu-id="23d6d-136">如果您想如何 toosee toodo 就地升級 AD Connect 目錄同步 tooAzure 然後看到這個 Channel 9 影片：</span><span class="sxs-lookup"><span data-stu-id="23d6d-136">If you want toosee how toodo an in-place upgrade from DirSync tooAzure AD Connect, then see this Channel 9 video:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-in-place-upgrade-from-legacy-tools/player]
>
>

## <a name="faq"></a><span data-ttu-id="23d6d-137">常見問題集</span><span class="sxs-lookup"><span data-stu-id="23d6d-137">FAQ</span></span>
<span data-ttu-id="23d6d-138">**問： 我已從 hello Azure 團隊和/或將訊息從 hello Office 365 訊息中心，收到電子郵件通知，但我正在使用連接。**</span><span class="sxs-lookup"><span data-stu-id="23d6d-138">**Q: I have received an email notification from hello Azure Team and/or a message from hello Office 365 message center, but I am using Connect.**</span></span>  
<span data-ttu-id="23d6d-139">hello 通知也會傳送 toocustomers 組建編號 1.0 搭配使用 Azure AD Connect。\*.0 （使用前 1.1 版本）。</span><span class="sxs-lookup"><span data-stu-id="23d6d-139">hello notification was also sent toocustomers using Azure AD Connect with a build number 1.0.\*.0 (using a pre-1.1 release).</span></span> <span data-ttu-id="23d6d-140">Microsoft 建議的客戶使用 Azure AD Connect 目前 toostay 釋放。</span><span class="sxs-lookup"><span data-stu-id="23d6d-140">Microsoft recommends customers toostay current with Azure AD Connect releases.</span></span> <span data-ttu-id="23d6d-141">hello[自動升級](active-directory-aadconnect-feature-automatic-upgrade.md)1.1 版中引進的功能可讓您輕鬆 tooalways 已安裝的 Azure AD Connect 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="23d6d-141">hello [automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) feature introduced in 1.1 makes it easy tooalways have a recent version of Azure AD Connect installed.</span></span>

<span data-ttu-id="23d6d-142">**問︰DirSync/Azure AD Sync 會在 2017 年 4 月 13 日停止運作嗎？**</span><span class="sxs-lookup"><span data-stu-id="23d6d-142">**Q: Will DirSync/Azure AD Sync stop working on April 13, 2017?**</span></span>  
<span data-ttu-id="23d6d-143">DirSync/Azure AD 同步處理會繼續 toowork 年 4 月 13 2017年上。</span><span class="sxs-lookup"><span data-stu-id="23d6d-143">DirSync/Azure AD Sync will continue toowork on April 13th 2017.</span></span>  <span data-ttu-id="23d6d-144">不過，Azure AD 在 2017 年 12 月 31 日將不再接受來自 DirSync/Azure AD Sync 的通訊。</span><span class="sxs-lookup"><span data-stu-id="23d6d-144">However, Azure AD will no longer accept communications from DirSync/Azure AD Sync on December 31st 2017.</span></span>

<span data-ttu-id="23d6d-145">**問：哪些 DirSync 版本可以進行升級？**</span><span class="sxs-lookup"><span data-stu-id="23d6d-145">**Q: Which DirSync versions can I upgrade from?**</span></span>  
<span data-ttu-id="23d6d-146">支援的 tooupgrade 從任何目錄同步版本，目前正在使用它。</span><span class="sxs-lookup"><span data-stu-id="23d6d-146">It is supported tooupgrade from any DirSync release currently being used.</span></span>

<span data-ttu-id="23d6d-147">**問： 該如何 hello Azure AD Connector FIM/MIM？**</span><span class="sxs-lookup"><span data-stu-id="23d6d-147">**Q: What about hello Azure AD Connector for FIM/MIM?**</span></span>  
<span data-ttu-id="23d6d-148">hello 適用於 FIM/MIM Azure AD 連接器具有**不**已被取代。</span><span class="sxs-lookup"><span data-stu-id="23d6d-148">hello Azure AD Connector for FIM/MIM has **not** been announced as deprecated.</span></span> <span data-ttu-id="23d6d-149">它目前在 **功能凍結**狀態；不會新增任何功能，而且不會收到任何錯誤修正。</span><span class="sxs-lookup"><span data-stu-id="23d6d-149">It is at **feature freeze**; no new functionality is added and it receives no bug fixes.</span></span> <span data-ttu-id="23d6d-150">Microsoft 建議客戶使用它從其 tooplan toomove tooAzure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="23d6d-150">Microsoft recommends customers using it tooplan toomove from it tooAzure AD Connect.</span></span> <span data-ttu-id="23d6d-151">強烈建議 toonot 啟動任何新的部署使用它。</span><span class="sxs-lookup"><span data-stu-id="23d6d-151">It is strongly recommended toonot start any new deployments using it.</span></span> <span data-ttu-id="23d6d-152">將取代在未來的 hello 公告此連接器。</span><span class="sxs-lookup"><span data-stu-id="23d6d-152">This Connector will be announced deprecated in hello future.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="23d6d-153">其他資源</span><span class="sxs-lookup"><span data-stu-id="23d6d-153">Additional Resources</span></span>
* [<span data-ttu-id="23d6d-154">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="23d6d-154">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
