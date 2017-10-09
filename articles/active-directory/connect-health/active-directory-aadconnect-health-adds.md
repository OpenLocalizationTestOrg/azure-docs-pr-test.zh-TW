---
title: "與 AD DS 的 Azure AD Connect Health aaaUsing |Microsoft 文件"
description: "這是 hello Azure AD Connect Health 頁面，將討論如何 toomonitor AD DS。"
services: active-directory
documentationcenter: 
author: arluca
manager: femila
editor: curtand
ms.assetid: 19e3cf15-f150-46a3-a10c-2990702cd700
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: e2fb6be65407d02c214dcab385b85d6cb54f48de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-ad-connect-health-with-ad-ds"></a><span data-ttu-id="e4364-103">在 AD DS 使用 Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="e4364-103">Using Azure AD Connect Health with AD DS</span></span>
<span data-ttu-id="e4364-104">下列文件的 hello 是特定 toomonitoring Active Directory 網域服務與 Azure AD Connect Health。</span><span class="sxs-lookup"><span data-stu-id="e4364-104">hello following documentation is specific toomonitoring Active Directory Domain Services with Azure AD Connect Health.</span></span> <span data-ttu-id="e4364-105">AD DS 的 hello 支援版本： Windows Server 2008 R2、 Windows Server 2012、 Windows Server 2012 R2 和 Windows Server 2016。</span><span class="sxs-lookup"><span data-stu-id="e4364-105">hello supported versions of AD DS are: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span></span>

<span data-ttu-id="e4364-106">如需使用 Azure AD Connect Health 來監視 AD FS 的詳細資訊，請參閱[在 AD FS 使用 Azure AD Connect Health](active-directory-aadconnect-health-adfs.md)。</span><span class="sxs-lookup"><span data-stu-id="e4364-106">For more information on monitoring AD FS with Azure AD Connect Health, see [Using Azure AD Connect Health with AD FS](active-directory-aadconnect-health-adfs.md).</span></span> <span data-ttu-id="e4364-107">此外，如需使用 Azure AD Connect Health 來監視 Azure AD Connect (同步處理) 的詳細資訊，請參閱 [使用適用於同步處理的 Azure AD Connect Health](active-directory-aadconnect-health-sync.md)。</span><span class="sxs-lookup"><span data-stu-id="e4364-107">Additionally, for information on monitoring Azure AD Connect (Sync) with Azure AD Connect Health see [Using Azure AD Connect Health for Sync](active-directory-aadconnect-health-sync.md).</span></span>

![適用於 AD DS 的 Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-entry.png)

## <a name="alerts-for-azure-ad-connect-health-for-ad-ds"></a><span data-ttu-id="e4364-109">適用於 AD DS 的 Azure AD Connect Health 警示</span><span class="sxs-lookup"><span data-stu-id="e4364-109">Alerts for Azure AD Connect Health for AD DS</span></span>
<span data-ttu-id="e4364-110">AD DS 的 hello Azure AD Connect Health 警示一節，提供您的使用中和未解決的警示，相關的 tooyour 網域控制站清單。</span><span class="sxs-lookup"><span data-stu-id="e4364-110">hello Alerts section within Azure AD Connect Health for AD DS, provides you a list of active and resolved alerts, related tooyour domain controllers.</span></span> <span data-ttu-id="e4364-111">選取 使用中或已解決的警示開啟新的刀鋒視窗的其他資訊，以及解決步驟，並連結 toosupporting 文件。</span><span class="sxs-lookup"><span data-stu-id="e4364-111">Selecting an active or resolved alert opens a new blade with additional information, along with resolution steps, and links toosupporting documentation.</span></span> <span data-ttu-id="e4364-112">每種警示類型可以有一或多個對應 tooeach hello 受該特定的警示影響的網域控制站的執行個體。</span><span class="sxs-lookup"><span data-stu-id="e4364-112">Each alert type can have one or more instances, which correspond tooeach of hello domain controllers affected by that particular alert.</span></span> <span data-ttu-id="e4364-113">Hello hello 警示刀鋒視窗底部，您可以按兩下受影響的網域控制站 tooopen 有關該警示的執行個體的更多詳細資料與其他刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e4364-113">Near hello bottom of hello alert blade, you can double-click an affected domain controller tooopen an additional blade with more details about that alert instance.</span></span>

<span data-ttu-id="e4364-114">在這個刀鋒視窗中，您可以啟用警示的電子郵件通知，並檢視中變更 hello 時間範圍。</span><span class="sxs-lookup"><span data-stu-id="e4364-114">Within this blade, you can enable email notifications for alerts and change hello time range in view.</span></span> <span data-ttu-id="e4364-115">展開 hello 時間範圍可讓您 toosee 先前已解決的警示。</span><span class="sxs-lookup"><span data-stu-id="e4364-115">Expanding hello time range allows you toosee prior resolved alerts.</span></span>

![Azure AD Connect 同步處理錯誤](./media/active-directory-aadconnect-health/aadconnect-health-adds-alerts.png)

## <a name="domain-controllers-dashboard"></a><span data-ttu-id="e4364-117">網域控制站儀表板</span><span class="sxs-lookup"><span data-stu-id="e4364-117">Domain Controllers Dashboard</span></span>
<span data-ttu-id="e4364-118">此儀表板提供環境的拓撲檢視，以及關鍵作業計量和每個受監視網域控制站的健康狀態。</span><span class="sxs-lookup"><span data-stu-id="e4364-118">This dashboard provides a topological view of your environment, along with key operational metrics and health status of each of your monitored domain controllers.</span></span> <span data-ttu-id="e4364-119">hello 呈現的衡量標準協助識別 tooquickly，任何網域控制站，可能需要進一步調查。</span><span class="sxs-lookup"><span data-stu-id="e4364-119">hello presented metrics help tooquickly identify, any domain controllers that might require further investigation.</span></span> <span data-ttu-id="e4364-120">根據預設，會顯示 hello 資料行的子集。</span><span class="sxs-lookup"><span data-stu-id="e4364-120">By default, only a subset of hello columns is displayed.</span></span> <span data-ttu-id="e4364-121">不過，您可以找到 hello 整組可用的資料行中，按兩下 hello 資料行命令。</span><span class="sxs-lookup"><span data-stu-id="e4364-121">However, you can find hello entire set of available columns, by double-clicking hello columns command.</span></span> <span data-ttu-id="e4364-122">選取您最關心，開啟此儀表板在單一、 輕鬆地將 tooview hello 健全狀況的 AD DS 環境的 hello 資料行。</span><span class="sxs-lookup"><span data-stu-id="e4364-122">Selecting hello columns that you most care about, turns this dashboard into a single and easy place tooview hello health of your AD DS environment.</span></span>

![網域控制站](./media/active-directory-aadconnect-health/aadconnect-health-adds-domainsandsites-dashboard.png)

<span data-ttu-id="e4364-124">網域控制站可以依其個別網域或站台，可協助您了解 hello 環境拓撲。</span><span class="sxs-lookup"><span data-stu-id="e4364-124">Domain controllers can be grouped by their respective domain or site, which is helpful for understanding hello environment topology.</span></span> <span data-ttu-id="e4364-125">最後，如果您按兩下 hello 刀鋒視窗中的標頭，hello 儀表板最大化 tooutilize hello 可用的螢幕大小。</span><span class="sxs-lookup"><span data-stu-id="e4364-125">Lastly, if you double-click hello blade header, hello dashboard maximizes tooutilize hello available screen real-estate.</span></span> <span data-ttu-id="e4364-126">顯示多個資料行時，此較大的檢視很有幫助。</span><span class="sxs-lookup"><span data-stu-id="e4364-126">This larger view is helpful when multiple columns are displayed.</span></span>

## <a name="replication-status-dashboard"></a><span data-ttu-id="e4364-127">複寫狀態儀表板</span><span class="sxs-lookup"><span data-stu-id="e4364-127">Replication Status Dashboard</span></span>
<span data-ttu-id="e4364-128">此儀表板提供 hello 複寫狀態以及複寫拓撲的受監視的網域控制站的檢視。</span><span class="sxs-lookup"><span data-stu-id="e4364-128">This dashboard provides a view of hello replication status and replication topology of your monitored domain controllers.</span></span> <span data-ttu-id="e4364-129">列出 hello 最近的複寫嘗試 hello 狀態，以及任何找到的錯誤很有幫助文件。</span><span class="sxs-lookup"><span data-stu-id="e4364-129">hello status of hello most recent replication attempt is listed, along with helpful documentation for any error that is found.</span></span> <span data-ttu-id="e4364-130">您可以按兩下網域控制站並顯示錯誤，tooopen 資訊的新刀鋒視窗，例如： hello 錯誤，並建議解決方法步驟的相關詳細資料，以及連結 tootroubleshooting 文件。</span><span class="sxs-lookup"><span data-stu-id="e4364-130">You can double-click a domain controller with an error, tooopen a new blade with information such as: details about hello error, recommended resolution steps, and links tootroubleshooting documentation.</span></span>

![複寫狀態](./media/active-directory-aadconnect-health/aadconnect-health-adds-replication.png)

## <a name="monitoring"></a><span data-ttu-id="e4364-132">監視</span><span class="sxs-lookup"><span data-stu-id="e4364-132">Monitoring</span></span>
<span data-ttu-id="e4364-133">這項功能提供不同的效能計數器，會持續收集從每個 hello 監視網域控制站的圖形化的趨勢。</span><span class="sxs-lookup"><span data-stu-id="e4364-133">This feature provides graphical trends of different performance counters, which are continuously collected from each of hello monitored domain controllers.</span></span> <span data-ttu-id="e4364-134">網域控制站的效能可以輕鬆地和樹系中所有其他受監視的網域控制站進行比較。</span><span class="sxs-lookup"><span data-stu-id="e4364-134">Performance of a domain controller can easily be compared across all other monitored domain controllers in your forest.</span></span> <span data-ttu-id="e4364-135">此外，您可以看到各種效能計數器並排，在環境中針對問題進行疑難排解時這很有用。</span><span class="sxs-lookup"><span data-stu-id="e4364-135">Additionally, you can see various performance counters side by side, which is helpful when troubleshooting issues in your environment.</span></span>

![監視](./media/active-directory-aadconnect-health/aadconnect-health-adds-monitoring.png)

<span data-ttu-id="e4364-137">根據預設，我們已預先選取四個效能計數器。不過，您可以藉由按一下 hello 篩選命令和選取或取消選取任何所需的效能計數器包含其他項目。</span><span class="sxs-lookup"><span data-stu-id="e4364-137">By default, we have preselected four performance counters; however, you can include others by clicking hello filter command and selecting or deselecting any desired performance counters.</span></span> <span data-ttu-id="e4364-138">此外，您可以按兩下效能計數器圖形 tooopen hello 監視網域控制站的每個包含資料點的新刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e4364-138">Additionally, you can double-click a performance counter graph tooopen a new blade, which includes data points for each of hello monitored domain controllers.</span></span>

## <a name="related-links"></a><span data-ttu-id="e4364-139">相關連結</span><span class="sxs-lookup"><span data-stu-id="e4364-139">Related links</span></span>
* [<span data-ttu-id="e4364-140">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="e4364-140">Azure AD Connect Health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="e4364-141">Azure AD Connect Health 代理程式安裝</span><span class="sxs-lookup"><span data-stu-id="e4364-141">Azure AD Connect Health Agent Installation</span></span>](active-directory-aadconnect-health-agent-install.md)
* [<span data-ttu-id="e4364-142">Azure AD Connect Health 操作</span><span class="sxs-lookup"><span data-stu-id="e4364-142">Azure AD Connect Health Operations</span></span>](active-directory-aadconnect-health-operations.md)
* [<span data-ttu-id="e4364-143">在 AD FS 使用 Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="e4364-143">Using Azure AD Connect Health with AD FS</span></span>](active-directory-aadconnect-health-adfs.md)
* [<span data-ttu-id="e4364-144">使用 Azure AD Connect Health 進行同步處理</span><span class="sxs-lookup"><span data-stu-id="e4364-144">Using Azure AD Connect Health for sync</span></span>](active-directory-aadconnect-health-sync.md)
* [<span data-ttu-id="e4364-145">Azure AD Connect Health 常見問題集</span><span class="sxs-lookup"><span data-stu-id="e4364-145">Azure AD Connect Health FAQ</span></span>](active-directory-aadconnect-health-faq.md)
* [<span data-ttu-id="e4364-146">Azure AD Connect Health 版本歷程記錄</span><span class="sxs-lookup"><span data-stu-id="e4364-146">Azure AD Connect Health Version History</span></span>](active-directory-aadconnect-health-version-history.md)

