---
title: "使用 Azure AD Connect Health 搭配 AD DS | Microsoft Docs"
description: "這是 Azure AD Connect Health 頁面，其中討論如何監視 AD DS。"
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
ms.openlocfilehash: 9e5b45d71b978c383932409f0037a4f6f32d0cb3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="using-azure-ad-connect-health-with-ad-ds"></a><span data-ttu-id="92613-103">在 AD DS 使用 Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="92613-103">Using Azure AD Connect Health with AD DS</span></span>
<span data-ttu-id="92613-104">下列文件適用於使用 Azure AD Connect Health 來監視 Active Directory 網域服務。</span><span class="sxs-lookup"><span data-stu-id="92613-104">The following documentation is specific to monitoring Active Directory Domain Services with Azure AD Connect Health.</span></span> <span data-ttu-id="92613-105">AD DS 支援的版本：Windows Server 2008 R2、Windows Server 2012、Windows Server 2012 R2 及 Windows Server 2016。</span><span class="sxs-lookup"><span data-stu-id="92613-105">The supported versions of AD DS are: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span></span>

<span data-ttu-id="92613-106">如需使用 Azure AD Connect Health 來監視 AD FS 的詳細資訊，請參閱[在 AD FS 使用 Azure AD Connect Health](active-directory-aadconnect-health-adfs.md)。</span><span class="sxs-lookup"><span data-stu-id="92613-106">For more information on monitoring AD FS with Azure AD Connect Health, see [Using Azure AD Connect Health with AD FS](active-directory-aadconnect-health-adfs.md).</span></span> <span data-ttu-id="92613-107">此外，如需使用 Azure AD Connect Health 來監視 Azure AD Connect (同步處理) 的詳細資訊，請參閱 [使用適用於同步處理的 Azure AD Connect Health](active-directory-aadconnect-health-sync.md)。</span><span class="sxs-lookup"><span data-stu-id="92613-107">Additionally, for information on monitoring Azure AD Connect (Sync) with Azure AD Connect Health see [Using Azure AD Connect Health for Sync](active-directory-aadconnect-health-sync.md).</span></span>

![適用於 AD DS 的 Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-entry.png)

## <a name="alerts-for-azure-ad-connect-health-for-ad-ds"></a><span data-ttu-id="92613-109">適用於 AD DS 的 Azure AD Connect Health 警示</span><span class="sxs-lookup"><span data-stu-id="92613-109">Alerts for Azure AD Connect Health for AD DS</span></span>
<span data-ttu-id="92613-110">適用於 AD DS 的 Azure AD Connect Health 中 [警示] 區段提供的作用中和已解決警示清單，與您的網域控制站相關。</span><span class="sxs-lookup"><span data-stu-id="92613-110">The Alerts section within Azure AD Connect Health for AD DS, provides you a list of active and resolved alerts, related to your domain controllers.</span></span> <span data-ttu-id="92613-111">選取作用中或已解決的警示會開啟新的刀鋒視窗，內含其他資訊和解決步驟以及支援文件的連結。</span><span class="sxs-lookup"><span data-stu-id="92613-111">Selecting an active or resolved alert opens a new blade with additional information, along with resolution steps, and links to supporting documentation.</span></span> <span data-ttu-id="92613-112">每個警示類型可以有一或多個執行個體，會對應到受該特定警示影響的各個網域控制站。</span><span class="sxs-lookup"><span data-stu-id="92613-112">Each alert type can have one or more instances, which correspond to each of the domain controllers affected by that particular alert.</span></span> <span data-ttu-id="92613-113">在靠近警示刀鋒視窗的底部，您可以連按兩下受影響的網域控制站來開啟額外的刀鋒視窗，內含有關該警示執行個體的其他詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="92613-113">Near the bottom of the alert blade, you can double-click an affected domain controller to open an additional blade with more details about that alert instance.</span></span>

<span data-ttu-id="92613-114">在此刀鋒視窗內，您可以啟用警示的電子郵件通知，以及變更檢視中的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="92613-114">Within this blade, you can enable email notifications for alerts and change the time range in view.</span></span> <span data-ttu-id="92613-115">展開時間範圍可讓您查看先前已解決的警示。</span><span class="sxs-lookup"><span data-stu-id="92613-115">Expanding the time range allows you to see prior resolved alerts.</span></span>

![Azure AD Connect 同步處理錯誤](./media/active-directory-aadconnect-health/aadconnect-health-adds-alerts.png)

## <a name="domain-controllers-dashboard"></a><span data-ttu-id="92613-117">網域控制站儀表板</span><span class="sxs-lookup"><span data-stu-id="92613-117">Domain Controllers Dashboard</span></span>
<span data-ttu-id="92613-118">此儀表板提供環境的拓撲檢視，以及關鍵作業計量和每個受監視網域控制站的健康狀態。</span><span class="sxs-lookup"><span data-stu-id="92613-118">This dashboard provides a topological view of your environment, along with key operational metrics and health status of each of your monitored domain controllers.</span></span> <span data-ttu-id="92613-119">顯示的計量有助於快速識別任何可能需要進一步調查的網域控制站。</span><span class="sxs-lookup"><span data-stu-id="92613-119">The presented metrics help to quickly identify, any domain controllers that might require further investigation.</span></span> <span data-ttu-id="92613-120">根據預設，只會顯示部份的資料行。</span><span class="sxs-lookup"><span data-stu-id="92613-120">By default, only a subset of the columns is displayed.</span></span> <span data-ttu-id="92613-121">不過，連按兩下資料行命令，即可找到整組可用的資料行。</span><span class="sxs-lookup"><span data-stu-id="92613-121">However, you can find the entire set of available columns, by double-clicking the columns command.</span></span> <span data-ttu-id="92613-122">選取您最想關注的資料行，即可在儀表板中單一且輕鬆地檢視 AD DS 環境的健康狀態。</span><span class="sxs-lookup"><span data-stu-id="92613-122">Selecting the columns that you most care about, turns this dashboard into a single and easy place to view the health of your AD DS environment.</span></span>

![網域控制站](./media/active-directory-aadconnect-health/aadconnect-health-adds-domainsandsites-dashboard.png)

<span data-ttu-id="92613-124">網域控制站可依其各別的網域或網站分組，有助您瞭解環境拓撲。</span><span class="sxs-lookup"><span data-stu-id="92613-124">Domain controllers can be grouped by their respective domain or site, which is helpful for understanding the environment topology.</span></span> <span data-ttu-id="92613-125">最後，如果連按兩下刀鋒視窗標頭，儀表板便會最大化以利用可用的螢幕畫面。</span><span class="sxs-lookup"><span data-stu-id="92613-125">Lastly, if you double-click the blade header, the dashboard maximizes to utilize the available screen real-estate.</span></span> <span data-ttu-id="92613-126">顯示多個資料行時，此較大的檢視很有幫助。</span><span class="sxs-lookup"><span data-stu-id="92613-126">This larger view is helpful when multiple columns are displayed.</span></span>

## <a name="replication-status-dashboard"></a><span data-ttu-id="92613-127">複寫狀態儀表板</span><span class="sxs-lookup"><span data-stu-id="92613-127">Replication Status Dashboard</span></span>
<span data-ttu-id="92613-128">此儀表板可檢視複寫狀態和受監視網域控制站的複寫拓撲。</span><span class="sxs-lookup"><span data-stu-id="92613-128">This dashboard provides a view of the replication status and replication topology of your monitored domain controllers.</span></span> <span data-ttu-id="92613-129">最新的複寫嘗試狀態會列出來，並附上針對所發現錯誤的有用文件。</span><span class="sxs-lookup"><span data-stu-id="92613-129">The status of the most recent replication attempt is listed, along with helpful documentation for any error that is found.</span></span> <span data-ttu-id="92613-130">您可以連按兩下包含錯誤的網域控制站，以開啟內含下列資訊的新刀鋒視窗：錯誤詳細資訊、建議的解決步驟，以及疑難排解文件的連結。</span><span class="sxs-lookup"><span data-stu-id="92613-130">You can double-click a domain controller with an error, to open a new blade with information such as: details about the error, recommended resolution steps, and links to troubleshooting documentation.</span></span>

![複寫狀態](./media/active-directory-aadconnect-health/aadconnect-health-adds-replication.png)

## <a name="monitoring"></a><span data-ttu-id="92613-132">監視</span><span class="sxs-lookup"><span data-stu-id="92613-132">Monitoring</span></span>
<span data-ttu-id="92613-133">這項功能提供不同效能計數器的圖形化趨勢，這是持續從每個受監視的網域控制站收集而來。</span><span class="sxs-lookup"><span data-stu-id="92613-133">This feature provides graphical trends of different performance counters, which are continuously collected from each of the monitored domain controllers.</span></span> <span data-ttu-id="92613-134">網域控制站的效能可以輕鬆地和樹系中所有其他受監視的網域控制站進行比較。</span><span class="sxs-lookup"><span data-stu-id="92613-134">Performance of a domain controller can easily be compared across all other monitored domain controllers in your forest.</span></span> <span data-ttu-id="92613-135">此外，您可以看到各種效能計數器並排，在環境中針對問題進行疑難排解時這很有用。</span><span class="sxs-lookup"><span data-stu-id="92613-135">Additionally, you can see various performance counters side by side, which is helpful when troubleshooting issues in your environment.</span></span>

![監視](./media/active-directory-aadconnect-health/aadconnect-health-adds-monitoring.png)

<span data-ttu-id="92613-137">根據預設，已預先選取四個效能計數器；不過，您可以按篩選命令並選取或取消選取任何想要的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="92613-137">By default, we have preselected four performance counters; however, you can include others by clicking the filter command and selecting or deselecting any desired performance counters.</span></span> <span data-ttu-id="92613-138">此外，您可以連按兩下效能計數器圖形以開啟新的刀鋒視窗，其中包含每個受監視網域控制站的資料點。</span><span class="sxs-lookup"><span data-stu-id="92613-138">Additionally, you can double-click a performance counter graph to open a new blade, which includes data points for each of the monitored domain controllers.</span></span>

## <a name="related-links"></a><span data-ttu-id="92613-139">相關連結</span><span class="sxs-lookup"><span data-stu-id="92613-139">Related links</span></span>
* [<span data-ttu-id="92613-140">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="92613-140">Azure AD Connect Health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="92613-141">Azure AD Connect Health 代理程式安裝</span><span class="sxs-lookup"><span data-stu-id="92613-141">Azure AD Connect Health Agent Installation</span></span>](active-directory-aadconnect-health-agent-install.md)
* [<span data-ttu-id="92613-142">Azure AD Connect Health 操作</span><span class="sxs-lookup"><span data-stu-id="92613-142">Azure AD Connect Health Operations</span></span>](active-directory-aadconnect-health-operations.md)
* [<span data-ttu-id="92613-143">在 AD FS 使用 Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="92613-143">Using Azure AD Connect Health with AD FS</span></span>](active-directory-aadconnect-health-adfs.md)
* [<span data-ttu-id="92613-144">使用 Azure AD Connect Health 進行同步處理</span><span class="sxs-lookup"><span data-stu-id="92613-144">Using Azure AD Connect Health for sync</span></span>](active-directory-aadconnect-health-sync.md)
* [<span data-ttu-id="92613-145">Azure AD Connect Health 常見問題集</span><span class="sxs-lookup"><span data-stu-id="92613-145">Azure AD Connect Health FAQ</span></span>](active-directory-aadconnect-health-faq.md)
* [<span data-ttu-id="92613-146">Azure AD Connect Health 版本歷程記錄</span><span class="sxs-lookup"><span data-stu-id="92613-146">Azure AD Connect Health Version History</span></span>](active-directory-aadconnect-health-version-history.md)

