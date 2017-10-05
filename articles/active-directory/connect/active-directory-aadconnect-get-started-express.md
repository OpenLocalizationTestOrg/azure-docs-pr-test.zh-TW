---
title: "Azure AD Connect：開始使用快速設定 | Microsoft Docs"
description: "了解如何下載、安裝和執行 Azure AD Connect 的安裝精靈。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: curtand
ms.assetid: b6ce45fd-554d-4f4d-95d1-47996d561c9f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 8a08f6e441a856a06bf7870747ca20af45a0364e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="getting-started-with-azure-ad-connect-using-express-settings"></a><span data-ttu-id="833d8-103">使用快速設定開始使用 Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="833d8-103">Getting started with Azure AD Connect using express settings</span></span>
<span data-ttu-id="833d8-104">當您有單一樹系拓撲和用於驗證的**密碼同步處理**時，便可使用 Azure AD Connect [快速設定](active-directory-aadconnectsync-implement-password-synchronization.md)。</span><span class="sxs-lookup"><span data-stu-id="833d8-104">Azure AD Connect **Express Settings** is used when you have a single-forest topology and [password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) for authentication.</span></span> <span data-ttu-id="833d8-105">**快速設定** 是預設選項，並且會用在最常部署的案例。</span><span class="sxs-lookup"><span data-stu-id="833d8-105">**Express Settings** is the default option and is used for the most commonly deployed scenario.</span></span> <span data-ttu-id="833d8-106">只要簡短地按幾下即可將內部部署目錄擴充至雲端。</span><span class="sxs-lookup"><span data-stu-id="833d8-106">You are only a few short clicks away to extend your on-premises directory to the cloud.</span></span>

<span data-ttu-id="833d8-107">在開始安裝 Azure AD Connect 之前，請務必要[下載 Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) 並完成 [Azure AD Connect：硬體和必要條件](active-directory-aadconnect-prerequisites.md)中的必要條件步驟。</span><span class="sxs-lookup"><span data-stu-id="833d8-107">Before you start installing Azure AD Connect, make sure to [download Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) and complete the pre-requisite steps in [Azure AD Connect: Hardware and prerequisites](active-directory-aadconnect-prerequisites.md).</span></span>

<span data-ttu-id="833d8-108">如果快速設定不符合拓撲，請參閱 [相關文件](#related-documentation) 中的其他案例。</span><span class="sxs-lookup"><span data-stu-id="833d8-108">If express settings does not match your topology, see [related documentation](#related-documentation) for other scenarios.</span></span>

## <a name="express-installation-of-azure-ad-connect"></a><span data-ttu-id="833d8-109">快速安裝 Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="833d8-109">Express installation of Azure AD Connect</span></span>
<span data-ttu-id="833d8-110">您可以在 [影片](#videos) 一節看到這些步驟的執行示範。</span><span class="sxs-lookup"><span data-stu-id="833d8-110">You can see these steps in action in the [videos](#videos) section.</span></span>

1. <span data-ttu-id="833d8-111">以本機系統管理員身分登入您想要安裝 Azure AD Connect 的伺服器。</span><span class="sxs-lookup"><span data-stu-id="833d8-111">Sign in as a local administrator to the server you wish to install Azure AD Connect on.</span></span> <span data-ttu-id="833d8-112">請在您想要做為同步處理伺服器的伺服器上進行此步驟。</span><span class="sxs-lookup"><span data-stu-id="833d8-112">You should do this on the server you wish to be the sync server.</span></span>
2. <span data-ttu-id="833d8-113">瀏覽並按兩下 **AzureADConnect.msi**。</span><span class="sxs-lookup"><span data-stu-id="833d8-113">Navigate to and double-click **AzureADConnect.msi**.</span></span>
3. <span data-ttu-id="833d8-114">在 [歡迎] 畫面上，選取同意授權條款的方塊，然後按一下 [繼續] 。</span><span class="sxs-lookup"><span data-stu-id="833d8-114">On the Welcome screen, select the box agreeing to the licensing terms and click **Continue**.</span></span>  
4. <span data-ttu-id="833d8-115">在 [快速設定] 畫面上，按一下 [ **使用快速設定**]。</span><span class="sxs-lookup"><span data-stu-id="833d8-115">On the Express settings screen, click **Use express settings**.</span></span>  
   <span data-ttu-id="833d8-116">![歡迎使用 Azure AD Connect](./media/active-directory-aadconnect-get-started-express/express.png)</span><span class="sxs-lookup"><span data-stu-id="833d8-116">![Welcome to Azure AD Connect](./media/active-directory-aadconnect-get-started-express/express.png)</span></span>
5. <span data-ttu-id="833d8-117">在 [連接到 Azure AD] 畫面上，輸入您的 Azure AD 的全域系統管理員使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="833d8-117">On the Connect to Azure AD screen, enter the username and password of a global administrator for your Azure AD.</span></span> <span data-ttu-id="833d8-118">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="833d8-118">Click **Next**.</span></span>  
   <span data-ttu-id="833d8-119">![連接至 Azure AD](./media/active-directory-aadconnect-get-started-express/connectaad.png) 如果您收到錯誤訊息，而且有連線問題，請參閱[針對連線問題進行疑難排解](active-directory-aadconnect-troubleshoot-connectivity.md)中的必要條件步驟。</span><span class="sxs-lookup"><span data-stu-id="833d8-119">![Connect to Azure AD](./media/active-directory-aadconnect-get-started-express/connectaad.png) If you receive an error and have problems with connectivity, then see [Troubleshoot connectivity problems](active-directory-aadconnect-troubleshoot-connectivity.md).</span></span>
6. <span data-ttu-id="833d8-120">在 [連接到 AD DS] 畫面上輸入企業系統管理員帳戶的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="833d8-120">On the Connect to AD DS screen, enter the username and password for an enterprise admin account.</span></span> <span data-ttu-id="833d8-121">您可以用 NetBios 或 FQDN 格式輸入網域部分，也就是 FABRIKAM\administrator 或 fabrikam.com\administrator。</span><span class="sxs-lookup"><span data-stu-id="833d8-121">You can enter the domain part in either NetBios or FQDN format, that is, FABRIKAM\administrator or fabrikam.com\administrator.</span></span> <span data-ttu-id="833d8-122">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="833d8-122">Click **Next**.</span></span>  
   <span data-ttu-id="833d8-123">![連線到 AD DS](./media/active-directory-aadconnect-get-started-express/connectad.png)</span><span class="sxs-lookup"><span data-stu-id="833d8-123">![Connect to AD DS](./media/active-directory-aadconnect-get-started-express/connectad.png)</span></span>
7. <span data-ttu-id="833d8-124">只有在未完成[必要條件](active-directory-aadconnect-prerequisites.md)中的[驗證網域](../active-directory-add-domain.md)時，才會顯示 [[**Azure AD 登入組態**](active-directory-aadconnect-user-signin.md#azure-ad-sign-in-configuration)] 頁面。</span><span class="sxs-lookup"><span data-stu-id="833d8-124">The [**Azure AD sign-in configuration**](active-directory-aadconnect-user-signin.md#azure-ad-sign-in-configuration) page only shows if you did not complete [verify your domains](../active-directory-add-domain.md) in the [prerequisites](active-directory-aadconnect-prerequisites.md).</span></span>
   <span data-ttu-id="833d8-125">![未驗證的網域](./media/active-directory-aadconnect-get-started-express/unverifieddomain.png)</span><span class="sxs-lookup"><span data-stu-id="833d8-125">![Unverified domains](./media/active-directory-aadconnect-get-started-express/unverifieddomain.png)</span></span>  
   <span data-ttu-id="833d8-126">如果您看到此頁面，請檢閱每一個標示為**未新增**和**未驗證**的網域。</span><span class="sxs-lookup"><span data-stu-id="833d8-126">If you see this page, then review every domain marked **Not Added** and **Not Verified**.</span></span> <span data-ttu-id="833d8-127">確定您所使用的網域皆已在 Azure AD 中完成驗證。</span><span class="sxs-lookup"><span data-stu-id="833d8-127">Make sure those domains you use have been verified in Azure AD.</span></span> <span data-ttu-id="833d8-128">驗證好網域時，按一下 [重新整理] 符號。</span><span class="sxs-lookup"><span data-stu-id="833d8-128">Click the Refresh symbol when you have verified your domains.</span></span>
8. <span data-ttu-id="833d8-129">在 [準備好設定] 畫面中，按一下 [安裝] 。</span><span class="sxs-lookup"><span data-stu-id="833d8-129">On the Ready to configure screen, click **Install**.</span></span>
   * <span data-ttu-id="833d8-130">在 [準備設定] 頁面上，您可以取消選取 [設定一完成，即開始同步處理程序]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="833d8-130">Optionally on the Ready to configure page, you can unselect the **Start the synchronization process as soon as configuration completes** checkbox.</span></span> <span data-ttu-id="833d8-131">如果您想要進行其他設定 (例如[篩選](active-directory-aadconnectsync-configure-filtering.md))，應該取消選取此核取方塊。</span><span class="sxs-lookup"><span data-stu-id="833d8-131">You should unselect this checkbox if you want to do additional configuration, such as [filtering](active-directory-aadconnectsync-configure-filtering.md).</span></span> <span data-ttu-id="833d8-132">若您取消選取此選項，精靈會設定同步處理，但是會讓排程器保持停用。</span><span class="sxs-lookup"><span data-stu-id="833d8-132">If you unselect this option, the wizard configures sync but leaves the scheduler disabled.</span></span> <span data-ttu-id="833d8-133">直到您[重新執行安裝精靈](active-directory-aadconnectsync-installation-wizard.md)以手動方式加以啟用時，才會執行排程器。</span><span class="sxs-lookup"><span data-stu-id="833d8-133">It does not run until you enable it manually by [rerunning the installation wizard](active-directory-aadconnectsync-installation-wizard.md).</span></span>
   * <span data-ttu-id="833d8-134">如果您的內部部署 Active Directory 中有 Exchange，則您也可以選擇啟用 [**Exchange 混合式部署**](https://technet.microsoft.com/library/jj200581.aspx)。</span><span class="sxs-lookup"><span data-stu-id="833d8-134">If you have Exchange in your on-premises Active Directory, then you also have an option to enable [**Exchange Hybrid deployment**](https://technet.microsoft.com/library/jj200581.aspx).</span></span> <span data-ttu-id="833d8-135">如果您打算在雲端和內部部署均設置 Exchange 信箱，請啟用此選項。</span><span class="sxs-lookup"><span data-stu-id="833d8-135">Enable this option if you plan to have Exchange mailboxes both in the cloud and on-premises at the same time.</span></span>
     <span data-ttu-id="833d8-136">![準備設定 Azure AD Connect](./media/active-directory-aadconnect-get-started-express/readytoconfigure.png)</span><span class="sxs-lookup"><span data-stu-id="833d8-136">![Ready to configure Azure AD Connect](./media/active-directory-aadconnect-get-started-express/readytoconfigure.png)</span></span>
9. <span data-ttu-id="833d8-137">當安裝完成時，按一下 [結束] 。</span><span class="sxs-lookup"><span data-stu-id="833d8-137">When the installation completes, click **Exit**.</span></span>
10. <span data-ttu-id="833d8-138">安裝完成之後，請先登出再重新登入，才能使用 Synchronization Service Manager 或同步處理規則編輯器。</span><span class="sxs-lookup"><span data-stu-id="833d8-138">After the installation has completed, sign off and sign in again before you use Synchronization Service Manager or Synchronization Rule Editor.</span></span>

## <a name="videos"></a><span data-ttu-id="833d8-139">影片</span><span class="sxs-lookup"><span data-stu-id="833d8-139">Videos</span></span>
<span data-ttu-id="833d8-140">如需使用快速安裝的影片，請參閱：</span><span class="sxs-lookup"><span data-stu-id="833d8-140">For a video on using the express installation, see:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="833d8-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="833d8-141">Next steps</span></span>
<span data-ttu-id="833d8-142">安裝了 Azure AD Connect 之後，您可以 [驗證安裝和指派授權](active-directory-aadconnect-whats-next.md)。</span><span class="sxs-lookup"><span data-stu-id="833d8-142">Now that you have Azure AD Connect installed you can [verify the installation and assign licenses](active-directory-aadconnect-whats-next.md).</span></span>

<span data-ttu-id="833d8-143">深入了解這些在安裝時啟用的功能︰[自動升級](active-directory-aadconnect-feature-automatic-upgrade.md)、[防止意外刪除](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)和 [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md)。</span><span class="sxs-lookup"><span data-stu-id="833d8-143">Learn more about these features, which were enabled with the installation: [Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md), [Prevent accidental deletes](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), and [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).</span></span>

<span data-ttu-id="833d8-144">深入了解這些常見主題︰[排程器和如何觸發同步處理](active-directory-aadconnectsync-feature-scheduler.md)。</span><span class="sxs-lookup"><span data-stu-id="833d8-144">Learn more about these common topics: [scheduler and how to trigger sync](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

<span data-ttu-id="833d8-145">深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="833d8-145">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="related-documentation"></a><span data-ttu-id="833d8-146">相關文件</span><span class="sxs-lookup"><span data-stu-id="833d8-146">Related documentation</span></span>
| <span data-ttu-id="833d8-147">主題</span><span class="sxs-lookup"><span data-stu-id="833d8-147">Topic</span></span> |
| --- | --- |
| <span data-ttu-id="833d8-148">Azure AD Connect 概觀</span><span class="sxs-lookup"><span data-stu-id="833d8-148">Azure AD Connect overview</span></span> |
| <span data-ttu-id="833d8-149">使用自訂設定進行安裝</span><span class="sxs-lookup"><span data-stu-id="833d8-149">Install using customized settings</span></span> |
| <span data-ttu-id="833d8-150">從 DirSync 升級</span><span class="sxs-lookup"><span data-stu-id="833d8-150">Upgrade from DirSync</span></span> |
| <span data-ttu-id="833d8-151">用於安裝的帳戶</span><span class="sxs-lookup"><span data-stu-id="833d8-151">Accounts used for installation</span></span> |

