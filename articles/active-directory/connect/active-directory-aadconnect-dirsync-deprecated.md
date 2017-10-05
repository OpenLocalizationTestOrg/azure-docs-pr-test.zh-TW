---
title: "從 DirSync 和 Azure AD Sync 升級 |Microsoft Docs"
description: "描述如何從 DirSync 和 Azure AD Sync 升級至 Azure AD Connect。"
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
ms.openlocfilehash: 3674670e10500d2992539ab60fbdb31b666fcf9a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="upgrade-windows-azure-active-directory-sync-and-azure-active-directory-sync"></a><span data-ttu-id="0f7d8-103">升級 Windows Azure Active Directory Sync 和 Azure Active Directory Sync</span><span class="sxs-lookup"><span data-stu-id="0f7d8-103">Upgrade Windows Azure Active Directory Sync and Azure Active Directory Sync</span></span>
<span data-ttu-id="0f7d8-104">Azure AD Connect 是連接內部部署目錄與 Azure AD 和 Office 365 的最佳方式。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-104">Azure AD Connect is the best way to connect your on-premises directory with Azure AD and Office 365.</span></span> <span data-ttu-id="0f7d8-105">這是將 Azure AD Connect 從 Windows Azure Active Directory Sync (DirSync) 或 Azure AD Sync 升級的最佳時機，因為這些工具現在已淘汰，而且會在 2017 年 4 月 13 日結束支援。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-105">This is a great time to upgrade to Azure AD Connect from Windows Azure Active Directory Sync (DirSync) or Azure AD Sync as these tools are now deprecated and will reach end of support on April 13, 2017.</span></span>

<span data-ttu-id="0f7d8-106">已淘汰的兩個身分識別同步處理工具會提供給單一樹系客戶 (DirSync)，以及多樹系和其他進階客戶 (Azure AD Sync)。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-106">The two identity synchronization tools that are deprecated were offered for single forest customers (DirSync) and for multi-forest and other advanced customers (Azure AD Sync).</span></span> <span data-ttu-id="0f7d8-107">這些較舊的工具已經取代為適用於所有案例的單一解決方案︰Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-107">These older tools have been replaced with a single solution that is available for all scenarios: Azure AD Connect.</span></span> <span data-ttu-id="0f7d8-108">它提供新的功能、增強功能和新案例的支援。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-108">It offers new functionality, feature enhancements, and support for new scenarios.</span></span> <span data-ttu-id="0f7d8-109">若要能夠繼續同步處理內部部署身分識別資料至 Azure AD 和 Office 365，強烈建議您升級至 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-109">To be able to continue to synchronize your on-premises identity data to Azure AD and Office 365, we strongly recommend that you upgrade to Azure AD Connect.</span></span>

<span data-ttu-id="0f7d8-110">最新版的 DirSync 發行於 2014 年 7 月，而最新版的 Azure AD Sync 發行於 2015 年 5 月。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-110">The last release of DirSync was released in July 2014 and the last release of Azure AD Sync was released in May 2015.</span></span>

## <a name="what-is-azure-ad-connect"></a><span data-ttu-id="0f7d8-111">何謂 Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="0f7d8-111">What is Azure AD Connect</span></span>
<span data-ttu-id="0f7d8-112">Azure AD Connect 是 DirSync 和 Azure AD Sync 的後續產品。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-112">Azure AD Connect is the successor to DirSync and Azure AD Sync.</span></span> <span data-ttu-id="0f7d8-113">它結合了兩者支援的所有案例。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-113">It combines all scenarios these two supported.</span></span> <span data-ttu-id="0f7d8-114">您可以在 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)中進一步了解。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-114">You can read more about it in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="deprecation-schedule"></a><span data-ttu-id="0f7d8-115">淘汰排程</span><span class="sxs-lookup"><span data-stu-id="0f7d8-115">Deprecation schedule</span></span>
| <span data-ttu-id="0f7d8-116">Date</span><span class="sxs-lookup"><span data-stu-id="0f7d8-116">Date</span></span> | <span data-ttu-id="0f7d8-117">註解</span><span class="sxs-lookup"><span data-stu-id="0f7d8-117">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="0f7d8-118">2016 年 4 月 13 日</span><span class="sxs-lookup"><span data-stu-id="0f7d8-118">April 13, 2016</span></span> |<span data-ttu-id="0f7d8-119">Windows Azure Active Directory Sync (“DirSync”) 和 Microsoft Azure Active Directory Sync (“Azure AD Sync”) 已宣布淘汰。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-119">Windows Azure Active Directory Sync (“DirSync”) and Microsoft Azure Active Directory Sync (“Azure AD Sync”) are announced as deprecated.</span></span> |
| <span data-ttu-id="0f7d8-120">2017 年 4 月 13 日</span><span class="sxs-lookup"><span data-stu-id="0f7d8-120">April 13, 2017</span></span> |<span data-ttu-id="0f7d8-121">支援結束。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-121">Support ends.</span></span> <span data-ttu-id="0f7d8-122">客戶必須先升級至 Azure AD Connect 才能開啟支援案例。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-122">Customers will no longer be able to open a support case without upgrading to Azure AD Connect first.</span></span> |
|<span data-ttu-id="0f7d8-123">2017 年 12 月 31 日</span><span class="sxs-lookup"><span data-stu-id="0f7d8-123">December 31, 2017</span></span>|<span data-ttu-id="0f7d8-124">Azure AD 已不再接受來自 Windows Azure Active Directory Sync (“DirSync”) 和 Microsoft Azure Active Directory Sync (“Azure AD Sync”) 的通訊。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-124">Azure AD will no longer accept communications from Windows Azure Active Directory Sync (“DirSync”) and Microsoft Azure Active Directory Sync (“Azure AD Sync”).</span></span>

## <a name="how-to-transition-to-azure-ad-connect"></a><span data-ttu-id="0f7d8-125">如何轉換為 Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="0f7d8-125">How to transition to Azure AD Connect</span></span>
<span data-ttu-id="0f7d8-126">如果您正在執行 DirSync，有兩種方式可以升級︰就地升級和平行部署。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-126">If you are running DirSync, there are two ways you can upgrade: In-place upgrade and parallel deployment.</span></span> <span data-ttu-id="0f7d8-127">對大多數的客戶，以及如果您擁有最新的作業系統和少於 50,000 個物件，建議採用就地升級。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-127">An in-place upgrade is recommended for most customers and if you have a recent operating system and less than 50,000 objects.</span></span> <span data-ttu-id="0f7d8-128">在其他情況下，建議執行平行部署，DirSync 組態會移至執行 Azure AD Connect 的新伺服器。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-128">In other cases, it is recommended to do a parallel deployment where your DirSync configuration is moved to a new server running Azure AD Connect.</span></span>

<span data-ttu-id="0f7d8-129">如果您使用 Azure AD Sync，則建議採用就地升級。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-129">If you use Azure AD Sync, then an in-place upgrade is recommended.</span></span> <span data-ttu-id="0f7d8-130">如果您想要，您也可以並行安裝新的 Azure AD Connect 伺服器，並且執行從 Azure AD 同步伺服器到 Azure AD Connect 的變換移轉。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-130">If you want to, it is possible to install a new Azure AD Connect server in parallel and do a swing migration from your Azure AD Sync server to Azure AD Connect.</span></span>

| <span data-ttu-id="0f7d8-131">方案</span><span class="sxs-lookup"><span data-stu-id="0f7d8-131">Solution</span></span> | <span data-ttu-id="0f7d8-132">案例</span><span class="sxs-lookup"><span data-stu-id="0f7d8-132">Scenario</span></span> |
| --- | --- |
| [<span data-ttu-id="0f7d8-133">從 DirSync 升級</span><span class="sxs-lookup"><span data-stu-id="0f7d8-133">Upgrade from DirSync</span></span>](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li><span data-ttu-id="0f7d8-134">如果您有已在執行中的現有 DirSync 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-134">If you have an existing DirSync server already running.</span></span></li> |
| [<span data-ttu-id="0f7d8-135">從 Azure AD Sync 升級</span><span class="sxs-lookup"><span data-stu-id="0f7d8-135">Upgrade from Azure AD Sync</span></span>](active-directory-aadconnect-upgrade-previous-version.md) |<li><span data-ttu-id="0f7d8-136">如果您要從 Azure AD Sync 移動。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-136">If you are moving from Azure AD Sync.</span></span></li> |

<span data-ttu-id="0f7d8-137">如果您想要了解如何執行就地升級以從 DirSync 升級到 Azure AD Connect，請觀看此第 9 頻道影片︰</span><span class="sxs-lookup"><span data-stu-id="0f7d8-137">If you want to see how to do an in-place upgrade from DirSync to Azure AD Connect, then see this Channel 9 video:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-in-place-upgrade-from-legacy-tools/player]
>
>

## <a name="faq"></a><span data-ttu-id="0f7d8-138">常見問題集</span><span class="sxs-lookup"><span data-stu-id="0f7d8-138">FAQ</span></span>
<span data-ttu-id="0f7d8-139">**問：我是使用 Connect，卻收到來自 Azure 團隊及/或來自 Office 365 郵件中心的訊息。**</span><span class="sxs-lookup"><span data-stu-id="0f7d8-139">**Q: I have received an email notification from the Azure Team and/or a message from the Office 365 message center, but I am using Connect.**</span></span>  
<span data-ttu-id="0f7d8-140">這項通知也會傳送給使用 Azure AD Connect 組建編號 1.0.\*.0 (使用 1.1 發行前版本) 的客戶。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-140">The notification was also sent to customers using Azure AD Connect with a build number 1.0.\*.0 (using a pre-1.1 release).</span></span> <span data-ttu-id="0f7d8-141">Microsoft 建議客戶使用最新的 Azure AD Connect 版本。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-141">Microsoft recommends customers to stay current with Azure AD Connect releases.</span></span> <span data-ttu-id="0f7d8-142">1.1 版引進的[自動升級](active-directory-aadconnect-feature-automatic-upgrade.md)功能可讓您持續輕鬆擁有最新的 Azure AD Connect 安裝版本。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-142">The [automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) feature introduced in 1.1 makes it easy to always have a recent version of Azure AD Connect installed.</span></span>

<span data-ttu-id="0f7d8-143">**問︰DirSync/Azure AD Sync 會在 2017 年 4 月 13 日停止運作嗎？**</span><span class="sxs-lookup"><span data-stu-id="0f7d8-143">**Q: Will DirSync/Azure AD Sync stop working on April 13, 2017?**</span></span>  
<span data-ttu-id="0f7d8-144">DirSync/Azure AD Sync 在 2017 年 4 月 13 日會繼續運作。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-144">DirSync/Azure AD Sync will continue to work on April 13th 2017.</span></span>  <span data-ttu-id="0f7d8-145">不過，Azure AD 在 2017 年 12 月 31 日將不再接受來自 DirSync/Azure AD Sync 的通訊。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-145">However, Azure AD will no longer accept communications from DirSync/Azure AD Sync on December 31st 2017.</span></span>

<span data-ttu-id="0f7d8-146">**問：哪些 DirSync 版本可以進行升級？**</span><span class="sxs-lookup"><span data-stu-id="0f7d8-146">**Q: Which DirSync versions can I upgrade from?**</span></span>  
<span data-ttu-id="0f7d8-147">目前使用的任何 DirSync 版本皆支援升級。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-147">It is supported to upgrade from any DirSync release currently being used.</span></span>

<span data-ttu-id="0f7d8-148">**問：什麼是 FIM/MIM 的 Azure AD 連接器？**</span><span class="sxs-lookup"><span data-stu-id="0f7d8-148">**Q: What about the Azure AD Connector for FIM/MIM?**</span></span>  
<span data-ttu-id="0f7d8-149">FIM/MIM 的 Azure AD 連接器**尚未**宣布淘汰。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-149">The Azure AD Connector for FIM/MIM has **not** been announced as deprecated.</span></span> <span data-ttu-id="0f7d8-150">它目前在 **功能凍結**狀態；不會新增任何功能，而且不會收到任何錯誤修正。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-150">It is at **feature freeze**; no new functionality is added and it receives no bug fixes.</span></span> <span data-ttu-id="0f7d8-151">Microsoft 建議使用它的客戶規劃從它移至 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-151">Microsoft recommends customers using it to plan to move from it to Azure AD Connect.</span></span> <span data-ttu-id="0f7d8-152">強烈建議不要使用它啟動任何新的部署。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-152">It is strongly recommended to not start any new deployments using it.</span></span> <span data-ttu-id="0f7d8-153">此連接器會在未來宣布淘汰。</span><span class="sxs-lookup"><span data-stu-id="0f7d8-153">This Connector will be announced deprecated in the future.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0f7d8-154">其他資源</span><span class="sxs-lookup"><span data-stu-id="0f7d8-154">Additional Resources</span></span>
* [<span data-ttu-id="0f7d8-155">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f7d8-155">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
