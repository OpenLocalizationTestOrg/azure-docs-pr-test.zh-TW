---
title: "Azure AD Connect：開始使用快速設定 | Microsoft Docs"
description: "了解如何 toodownload，安裝及執行 Azure AD Connect 的 hello 安裝精靈。"
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
ms.openlocfilehash: 79f796fa7738b85e9236e856bddb529379f60390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-ad-connect-using-express-settings"></a><span data-ttu-id="75532-103">使用快速設定開始使用 Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="75532-103">Getting started with Azure AD Connect using express settings</span></span>
<span data-ttu-id="75532-104">當您有單一樹系拓撲和用於驗證的**密碼同步處理**時，便可使用 Azure AD Connect [快速設定](active-directory-aadconnectsync-implement-password-synchronization.md)。</span><span class="sxs-lookup"><span data-stu-id="75532-104">Azure AD Connect **Express Settings** is used when you have a single-forest topology and [password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) for authentication.</span></span> <span data-ttu-id="75532-105">**快速設定**是 hello 預設選項，而且是最常部署的 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="75532-105">**Express Settings** is hello default option and is used for hello most commonly deployed scenario.</span></span> <span data-ttu-id="75532-106">您會在內部部署目錄 toohello 雲端只有幾個簡短按一下離開 tooextend。</span><span class="sxs-lookup"><span data-stu-id="75532-106">You are only a few short clicks away tooextend your on-premises directory toohello cloud.</span></span>

<span data-ttu-id="75532-107">您開始安裝 Azure AD Connect，請確定太[下載 Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)和中的步驟完成 hello 必要條件[Azure AD Connect： 硬體和必要條件](active-directory-aadconnect-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="75532-107">Before you start installing Azure AD Connect, make sure too[download Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) and complete hello pre-requisite steps in [Azure AD Connect: Hardware and prerequisites](active-directory-aadconnect-prerequisites.md).</span></span>

<span data-ttu-id="75532-108">如果快速設定不符合拓撲，請參閱 [相關文件](#related-documentation) 中的其他案例。</span><span class="sxs-lookup"><span data-stu-id="75532-108">If express settings does not match your topology, see [related documentation](#related-documentation) for other scenarios.</span></span>

## <a name="express-installation-of-azure-ad-connect"></a><span data-ttu-id="75532-109">快速安裝 Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="75532-109">Express installation of Azure AD Connect</span></span>
<span data-ttu-id="75532-110">您可以看到這些步驟在動作中 hello[視訊](#videos)> 一節。</span><span class="sxs-lookup"><span data-stu-id="75532-110">You can see these steps in action in hello [videos](#videos) section.</span></span>

1. <span data-ttu-id="75532-111">以您想 tooinstall Azure AD Connect 的本機系統管理員 toohello 伺服器登入。</span><span class="sxs-lookup"><span data-stu-id="75532-111">Sign in as a local administrator toohello server you wish tooinstall Azure AD Connect on.</span></span> <span data-ttu-id="75532-112">您應該這樣 hello 在伺服器上您想 toobe hello 同步伺服器。</span><span class="sxs-lookup"><span data-stu-id="75532-112">You should do this on hello server you wish toobe hello sync server.</span></span>
2. <span data-ttu-id="75532-113">瀏覽 tooand 按兩下**AzureADConnect.msi**。</span><span class="sxs-lookup"><span data-stu-id="75532-113">Navigate tooand double-click **AzureADConnect.msi**.</span></span>
3. <span data-ttu-id="75532-114">在 hello 歡迎畫面上，選取 hello 方塊即表示同意 toohello 授權條款，然後按一下**繼續**。</span><span class="sxs-lookup"><span data-stu-id="75532-114">On hello Welcome screen, select hello box agreeing toohello licensing terms and click **Continue**.</span></span>  
4. <span data-ttu-id="75532-115">在 hello Express 設定畫面中，按一下 **使用 express 設定**。</span><span class="sxs-lookup"><span data-stu-id="75532-115">On hello Express settings screen, click **Use express settings**.</span></span>  
   <span data-ttu-id="75532-116">![歡迎使用 tooAzure AD Connect](./media/active-directory-aadconnect-get-started-express/express.png)</span><span class="sxs-lookup"><span data-stu-id="75532-116">![Welcome tooAzure AD Connect](./media/active-directory-aadconnect-get-started-express/express.png)</span></span>
5. <span data-ttu-id="75532-117">Hello 連接 tooAzure AD 在畫面上，輸入您的 Azure AD hello 使用者名稱和密碼的全域管理員。</span><span class="sxs-lookup"><span data-stu-id="75532-117">On hello Connect tooAzure AD screen, enter hello username and password of a global administrator for your Azure AD.</span></span> <span data-ttu-id="75532-118">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="75532-118">Click **Next**.</span></span>  
   <span data-ttu-id="75532-119">![連接 tooAzure AD](./media/active-directory-aadconnect-get-started-express/connectaad.png)如果您收到錯誤，且有連線問題，然後查看[疑難排解連線問題](active-directory-aadconnect-troubleshoot-connectivity.md)。</span><span class="sxs-lookup"><span data-stu-id="75532-119">![Connect tooAzure AD](./media/active-directory-aadconnect-get-started-express/connectaad.png) If you receive an error and have problems with connectivity, then see [Troubleshoot connectivity problems](active-directory-aadconnect-troubleshoot-connectivity.md).</span></span>
6. <span data-ttu-id="75532-120">Hello 連接 tooAD DS 在畫面上，輸入企業系統管理員帳戶 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="75532-120">On hello Connect tooAD DS screen, enter hello username and password for an enterprise admin account.</span></span> <span data-ttu-id="75532-121">您可以輸入 NetBios 或 FQDN 格式，也就是 FABRIKAM\administrator 或 fabrikam.com\administrator hello 網域 」 部分。</span><span class="sxs-lookup"><span data-stu-id="75532-121">You can enter hello domain part in either NetBios or FQDN format, that is, FABRIKAM\administrator or fabrikam.com\administrator.</span></span> <span data-ttu-id="75532-122">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="75532-122">Click **Next**.</span></span>  
   <span data-ttu-id="75532-123">![連接 tooAD DS](./media/active-directory-aadconnect-get-started-express/connectad.png)</span><span class="sxs-lookup"><span data-stu-id="75532-123">![Connect tooAD DS](./media/active-directory-aadconnect-get-started-express/connectad.png)</span></span>
7. <span data-ttu-id="75532-124">hello [ **Azure AD 登入組態**](active-directory-aadconnect-user-signin.md#azure-ad-sign-in-configuration)頁面只會顯示是否您未完成[確認您的網域](../active-directory-add-domain.md)在 hello[必要條件](active-directory-aadconnect-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="75532-124">hello [**Azure AD sign-in configuration**](active-directory-aadconnect-user-signin.md#azure-ad-sign-in-configuration) page only shows if you did not complete [verify your domains](../active-directory-add-domain.md) in hello [prerequisites](active-directory-aadconnect-prerequisites.md).</span></span>
   <span data-ttu-id="75532-125">![未驗證的網域](./media/active-directory-aadconnect-get-started-express/unverifieddomain.png)</span><span class="sxs-lookup"><span data-stu-id="75532-125">![Unverified domains](./media/active-directory-aadconnect-get-started-express/unverifieddomain.png)</span></span>  
   <span data-ttu-id="75532-126">如果您看到此頁面，請檢閱每一個標示為**未新增**和**未驗證**的網域。</span><span class="sxs-lookup"><span data-stu-id="75532-126">If you see this page, then review every domain marked **Not Added** and **Not Verified**.</span></span> <span data-ttu-id="75532-127">確定您所使用的網域皆已在 Azure AD 中完成驗證。</span><span class="sxs-lookup"><span data-stu-id="75532-127">Make sure those domains you use have been verified in Azure AD.</span></span> <span data-ttu-id="75532-128">當您已確認您的網域，請按一下 hello 重新整理符號。</span><span class="sxs-lookup"><span data-stu-id="75532-128">Click hello Refresh symbol when you have verified your domains.</span></span>
8. <span data-ttu-id="75532-129">Hello 準備 tooconfigure 畫面上，按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="75532-129">On hello Ready tooconfigure screen, click **Install**.</span></span>
   * <span data-ttu-id="75532-130">（選擇性） 在 hello 準備 tooconfigure 頁面上，您可以取消選取 hello**啟動 hello 同步處理程序，設定完成之後儘速**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="75532-130">Optionally on hello Ready tooconfigure page, you can unselect hello **Start hello synchronization process as soon as configuration completes** checkbox.</span></span> <span data-ttu-id="75532-131">如果您想 toodo 額外的設定，例如，您應該取消選取此核取方塊[篩選](active-directory-aadconnectsync-configure-filtering.md)。</span><span class="sxs-lookup"><span data-stu-id="75532-131">You should unselect this checkbox if you want toodo additional configuration, such as [filtering](active-directory-aadconnectsync-configure-filtering.md).</span></span> <span data-ttu-id="75532-132">如果您取消選取此選項，hello 精靈設定同步處理，但會保留 hello 排程器已停用。</span><span class="sxs-lookup"><span data-stu-id="75532-132">If you unselect this option, hello wizard configures sync but leaves hello scheduler disabled.</span></span> <span data-ttu-id="75532-133">不會執行直到您手動藉由啟用[hello 安裝精靈重新執行](active-directory-aadconnectsync-installation-wizard.md)。</span><span class="sxs-lookup"><span data-stu-id="75532-133">It does not run until you enable it manually by [rerunning hello installation wizard](active-directory-aadconnectsync-installation-wizard.md).</span></span>
   * <span data-ttu-id="75532-134">如果您在您的內部部署 Active Directory、 Exchange，則您也可以選項 tooenable [ **Exchange 混合部署**](https://technet.microsoft.com/library/jj200581.aspx)。</span><span class="sxs-lookup"><span data-stu-id="75532-134">If you have Exchange in your on-premises Active Directory, then you also have an option tooenable [**Exchange Hybrid deployment**](https://technet.microsoft.com/library/jj200581.aspx).</span></span> <span data-ttu-id="75532-135">啟用此選項，如果您計劃 toohave Exchange 信箱這兩個 hello 雲端和內部 hello 在相同的時間。</span><span class="sxs-lookup"><span data-stu-id="75532-135">Enable this option if you plan toohave Exchange mailboxes both in hello cloud and on-premises at hello same time.</span></span>
     <span data-ttu-id="75532-136">![準備好 tooconfigure Azure AD Connect](./media/active-directory-aadconnect-get-started-express/readytoconfigure.png)</span><span class="sxs-lookup"><span data-stu-id="75532-136">![Ready tooconfigure Azure AD Connect](./media/active-directory-aadconnect-get-started-express/readytoconfigure.png)</span></span>
9. <span data-ttu-id="75532-137">Hello 安裝完成時，按一下**結束**。</span><span class="sxs-lookup"><span data-stu-id="75532-137">When hello installation completes, click **Exit**.</span></span>
10. <span data-ttu-id="75532-138">Hello 安裝完成後，登出並再次登入之前您使用同步處理服務管理員或同步處理規則編輯器。</span><span class="sxs-lookup"><span data-stu-id="75532-138">After hello installation has completed, sign off and sign in again before you use Synchronization Service Manager or Synchronization Rule Editor.</span></span>

## <a name="videos"></a><span data-ttu-id="75532-139">影片</span><span class="sxs-lookup"><span data-stu-id="75532-139">Videos</span></span>
<span data-ttu-id="75532-140">如需有關使用 hello 快速安裝的影片，請參閱：</span><span class="sxs-lookup"><span data-stu-id="75532-140">For a video on using hello express installation, see:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="75532-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="75532-141">Next steps</span></span>
<span data-ttu-id="75532-142">既然您已安裝的 Azure AD Connect 可以[確認 hello 安裝並指派授權](active-directory-aadconnect-whats-next.md)。</span><span class="sxs-lookup"><span data-stu-id="75532-142">Now that you have Azure AD Connect installed you can [verify hello installation and assign licenses](active-directory-aadconnect-whats-next.md).</span></span>

<span data-ttu-id="75532-143">深入了解這些功能，與 hello 安裝已啟用：[自動升級](active-directory-aadconnect-feature-automatic-upgrade.md)，[防止被意外刪除](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)，和[Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md)。</span><span class="sxs-lookup"><span data-stu-id="75532-143">Learn more about these features, which were enabled with hello installation: [Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md), [Prevent accidental deletes](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), and [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).</span></span>

<span data-ttu-id="75532-144">深入了解這些常見的主題：[排程器和 tootrigger 的同步處理](active-directory-aadconnectsync-feature-scheduler.md)。</span><span class="sxs-lookup"><span data-stu-id="75532-144">Learn more about these common topics: [scheduler and how tootrigger sync](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

<span data-ttu-id="75532-145">深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="75532-145">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="related-documentation"></a><span data-ttu-id="75532-146">相關文件</span><span class="sxs-lookup"><span data-stu-id="75532-146">Related documentation</span></span>
| <span data-ttu-id="75532-147">主題</span><span class="sxs-lookup"><span data-stu-id="75532-147">Topic</span></span> |
| --- | --- |
| <span data-ttu-id="75532-148">Azure AD Connect 概觀</span><span class="sxs-lookup"><span data-stu-id="75532-148">Azure AD Connect overview</span></span> |
| <span data-ttu-id="75532-149">使用自訂設定進行安裝</span><span class="sxs-lookup"><span data-stu-id="75532-149">Install using customized settings</span></span> |
| <span data-ttu-id="75532-150">從 DirSync 升級</span><span class="sxs-lookup"><span data-stu-id="75532-150">Upgrade from DirSync</span></span> |
| <span data-ttu-id="75532-151">用於安裝的帳戶</span><span class="sxs-lookup"><span data-stu-id="75532-151">Accounts used for installation</span></span> |

