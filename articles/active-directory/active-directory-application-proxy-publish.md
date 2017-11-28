---
title: "aaaPublish 應用程式與 Azure AD Application Proxy |Microsoft 文件"
description: "將內部部署應用程式 toohello 雲端與 Azure AD Application Proxy 發行 hello 傳統入口網站中。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7926998314c65521ae48aebcceb33cb0c67e0b87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="c52d6-103">使用 Azure AD 應用程式 Proxy 發佈應用程式</span><span class="sxs-lookup"><span data-stu-id="c52d6-103">Publish applications using Azure AD Application Proxy</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c52d6-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c52d6-104">Azure portal</span></span>](application-proxy-publish-azure-portal.md)
> * [<span data-ttu-id="c52d6-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="c52d6-105">Azure classic portal</span></span>](active-directory-application-proxy-publish.md)

<span data-ttu-id="c52d6-106">Azure AD Application Proxy 可協助您支援遠端工作者所發佈在內部部署應用程式 toobe hello 透過存取網際網路。</span><span class="sxs-lookup"><span data-stu-id="c52d6-106">Azure AD Application Proxy helps you support remote workers by publishing on-premises applications toobe accessed over hello internet.</span></span> <span data-ttu-id="c52d6-107">此時，您應該已經有[hello Azure 傳統入口網站中啟用應用程式 Proxy](active-directory-application-proxy-enable.md)。</span><span class="sxs-lookup"><span data-stu-id="c52d6-107">By this point, you should already have [enabled Application Proxy in hello Azure classic portal](active-directory-application-proxy-enable.md).</span></span> <span data-ttu-id="c52d6-108">這篇文章會引導您完成 hello 步驟 toopublish 執行的應用程式在您的區域網路上，並提供安全的遠端存取從網路外部。</span><span class="sxs-lookup"><span data-stu-id="c52d6-108">This article walks you through hello steps toopublish applications that are running on your local network and provide secure remote access from outside your network.</span></span> <span data-ttu-id="c52d6-109">完成本文之後，您會準備 tooconfigure hello 應用程式與個人化的資訊或安全性需求。</span><span class="sxs-lookup"><span data-stu-id="c52d6-109">After you complete this article, you'll be ready tooconfigure hello application with personalized information or security requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="c52d6-110">應用程式 Proxy 是升級 toohello Premium 或 Azure Active Directory Basic 版時，才可使用的功能。</span><span class="sxs-lookup"><span data-stu-id="c52d6-110">Application Proxy is a feature that is available only if you upgraded toohello Premium or Basic edition of Azure Active Directory.</span></span> <span data-ttu-id="c52d6-111">如需詳細資訊，請參閱 [Azure Active Directory 版本](active-directory-editions.md)。</span><span class="sxs-lookup"><span data-stu-id="c52d6-111">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span> <span data-ttu-id="c52d6-112">如果您想 toouse 應用程式 Proxy，您可以[hello Azure 入口網站中發佈應用程式](application-proxy-publish-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="c52d6-112">If you want toouse Application Proxy, you can [Publish applications in hello Azure portal](application-proxy-publish-azure-portal.md).</span></span>

## <a name="publish-an-app-using-hello-wizard"></a><span data-ttu-id="c52d6-113">發行應用程式使用 hello 精靈</span><span class="sxs-lookup"><span data-stu-id="c52d6-113">Publish an app using hello wizard</span></span>
1. <span data-ttu-id="c52d6-114">Hello 中的系統管理員身分登入[Azure 傳統入口網站](https://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="c52d6-114">Sign in as an administrator in hello [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="c52d6-115">請 tooActive 目錄並選取 hello 目錄啟用應用程式 Proxy 的位置。</span><span class="sxs-lookup"><span data-stu-id="c52d6-115">Go tooActive Directory and select hello directory where you enabled Application Proxy.</span></span>
   
    ![Active Directory - 圖示](./media/active-directory-application-proxy-publish/ad_icon.png)
3. <span data-ttu-id="c52d6-117">按一下 hello**應用程式**索引標籤，然後再按一下 hello**新增**在 hello 囉 」 畫面底部的按鈕</span><span class="sxs-lookup"><span data-stu-id="c52d6-117">Click hello **Applications** tab, and then click hello **Add** button at hello bottom of hello screen</span></span>
   
    ![新增應用程式](./media/active-directory-application-proxy-publish/aad_appproxy_selectdirectory.png)
4. <span data-ttu-id="c52d6-119">選取 [發佈將可從您的網路外部存取的應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="c52d6-119">Select **Publish an application that will be accessible from outside your network**.</span></span>
   
    ![發佈將可從您的網路外部存取的應用程式](./media/active-directory-application-proxy-publish/aad_appproxy_addapp.png)
5. <span data-ttu-id="c52d6-121">提供下列應用程式的相關資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="c52d6-121">Provide hello following information about your application:</span></span>
   
   * <span data-ttu-id="c52d6-122">**名稱**: hello 應用程式的使用者易記名稱。</span><span class="sxs-lookup"><span data-stu-id="c52d6-122">**Name**: hello user-friendly name for your application.</span></span> <span data-ttu-id="c52d6-123">該名稱在您的目錄中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="c52d6-123">It must be unique within your directory.</span></span>
   * <span data-ttu-id="c52d6-124">**內部 URL**: hello 應用程式 Proxy 連接器的 hello 位址使用 tooaccess hello 應用程式從您的私人網路內。</span><span class="sxs-lookup"><span data-stu-id="c52d6-124">**Internal URL**: hello address that hello Application Proxy Connector uses tooaccess hello application from inside your private network.</span></span> <span data-ttu-id="c52d6-125">未發行的 hello 伺服器 hello rest 時，您可以在 hello 後端伺服器 toopublish，提供特定路徑。</span><span class="sxs-lookup"><span data-stu-id="c52d6-125">You can provide a specific path on hello backend server toopublish, while hello rest of hello server is unpublished.</span></span> <span data-ttu-id="c52d6-126">如此一來，您可以將不同站台發佈在 hello 同一部伺服器，並提供每一個其名稱和存取規則。</span><span class="sxs-lookup"><span data-stu-id="c52d6-126">In this way, you can publish different sites on hello same server, and give each one its own name and access rules.</span></span>
     
     > [!TIP]
     > <span data-ttu-id="c52d6-127">如果您發行路徑，請確定它包含所有的 hello 所需的映像、 指令碼和您的應用程式的樣式表。</span><span class="sxs-lookup"><span data-stu-id="c52d6-127">If you publish a path, make sure that it includes all hello necessary images, scripts, and style sheets for your application.</span></span> <span data-ttu-id="c52d6-128">例如，如果您的應用程式位於 https://yourapp/app，並且使用位於 https://yourapp/media 映像，然後您應該發佈 https://yourapp/ hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="c52d6-128">For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as hello path.</span></span>
     > 
     > 
   * <span data-ttu-id="c52d6-129">**預先驗證方法**： 應用程式 Proxy 如何授與存取 tooyour 應用程式之前驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="c52d6-129">**Preauthentication Method**: How Application Proxy verifies users before giving them access tooyour application.</span></span> <span data-ttu-id="c52d6-130">從 hello 下拉功能表中選擇其中一個 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="c52d6-130">Choose one of hello options from hello drop-down menu.</span></span>
     
     * <span data-ttu-id="c52d6-131">Azure Active Directory： 應用程式 Proxy 會重新導向使用者 toosign 入 Azure AD，驗證其 hello 目錄和應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="c52d6-131">Azure Active Directory: Application Proxy redirects users toosign in with Azure AD, which authenticates their permissions for hello directory and application.</span></span>
     * <span data-ttu-id="c52d6-132">通過： 使用者不能 tooauthenticate tooaccess hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c52d6-132">Passthrough: Users don't have tooauthenticate tooaccess hello application.</span></span>
     
     ![應用程式屬性](./media/active-directory-application-proxy-publish/aad_appproxy_appproperties.png)  
6. <span data-ttu-id="c52d6-134">toofinish hello 精靈 中，按一下 hello 在 hello 囉 」 畫面底部的核取記號。</span><span class="sxs-lookup"><span data-stu-id="c52d6-134">toofinish hello wizard, click hello check mark at hello bottom of hello screen.</span></span> <span data-ttu-id="c52d6-135">hello 應用程式現在是 Azure AD 中定義。</span><span class="sxs-lookup"><span data-stu-id="c52d6-135">hello application is now defined in Azure AD.</span></span>

## <a name="assign-users-and-groups-toohello-application"></a><span data-ttu-id="c52d6-136">指派使用者和群組 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="c52d6-136">Assign users and groups toohello application</span></span>
<span data-ttu-id="c52d6-137">在順序為您的使用者 tooaccess 發佈的應用程式，您需要 tooassign 它們個別或群組。</span><span class="sxs-lookup"><span data-stu-id="c52d6-137">In order for your users tooaccess your published application, you need tooassign them either individually or in groups.</span></span> <span data-ttu-id="c52d6-138">(請記住 tooassign 自行存取，太。)您指派的每位使用者需要 Azure Basic 或更新版本的授權。</span><span class="sxs-lookup"><span data-stu-id="c52d6-138">(Remember tooassign yourself access, too.) Each user you assign needs a license for Azure Basic or higher.</span></span> <span data-ttu-id="c52d6-139">您可以將授權指派個別或 toogroups。</span><span class="sxs-lookup"><span data-stu-id="c52d6-139">You can assign licenses individually or toogroups.</span></span> <span data-ttu-id="c52d6-140">如需詳細資訊，請參閱[tooan 應用程式指派給使用者](active-directory-applications-guiding-developers-assigning-users.md)。</span><span class="sxs-lookup"><span data-stu-id="c52d6-140">For more information, see [Assigning users tooan application](active-directory-applications-guiding-developers-assigning-users.md).</span></span> 

<span data-ttu-id="c52d6-141">針對需要預先驗證的應用程式，將使用者指派會授與權限 toouse hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c52d6-141">For apps that require preauthentication, assigning a user grants permission toouse hello application.</span></span> <span data-ttu-id="c52d6-142">不需要的應用程式的預先驗證時，將使用者指派表示該 hello 使用者可以存取 hello 應用程式透過 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="c52d6-142">For apps that don't require preauthentication, assigning a user means that hello user can access hello application through hello access panel.</span></span>

1. <span data-ttu-id="c52d6-143">分頁裝訂的 hello 新增應用程式精靈 之後，您會看到 hello 快速入門應用程式頁面。</span><span class="sxs-lookup"><span data-stu-id="c52d6-143">After finishing hello Add App wizard, you see hello Quick Start page for your application.</span></span> <span data-ttu-id="c52d6-144">toomanage 擁有存取 toohello 應用程式中，選取**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="c52d6-144">toomanage who has access toohello app, select **Users and groups**.</span></span>
   
    ![應用程式 Proxy 快速啟動指派使用者 - 螢幕擷取畫面](./media/active-directory-application-proxy-publish/aad_appproxy_usersgroups.png)
2. <span data-ttu-id="c52d6-146">在您的目錄中搜尋特定群組，或顯示所有的使用者。</span><span class="sxs-lookup"><span data-stu-id="c52d6-146">Search for specific groups in your directory, or show all your users.</span></span> <span data-ttu-id="c52d6-147">toodisplay hello 搜尋結果中，按一下 hello 核取記號。</span><span class="sxs-lookup"><span data-stu-id="c52d6-147">toodisplay hello search results, click hello check mark.</span></span>
   
      ![搜尋群組或使用者 - 螢幕擷取畫面](./media/active-directory-application-proxy-publish/aad_appproxy_search.png)
3. <span data-ttu-id="c52d6-149">選取每個使用者或群組，您想要 tooassign toothis 應用程式，然後按一下 **指派**。</span><span class="sxs-lookup"><span data-stu-id="c52d6-149">Select each user or group you want tooassign toothis app and click **Assign**.</span></span> <span data-ttu-id="c52d6-150">您要求 tooconfirm 此動作。</span><span class="sxs-lookup"><span data-stu-id="c52d6-150">You are asked tooconfirm this action.</span></span>

> [!NOTE]
> <span data-ttu-id="c52d6-151">若是整合式 Windows 驗證應用程式，您可以僅指派從內部部署 Active Directory 同步的使用者及群組。</span><span class="sxs-lookup"><span data-stu-id="c52d6-151">For Integrated Windows Authentication apps, you can assign only users and groups that are synced from your on-premises Active Directory.</span></span> <span data-ttu-id="c52d6-152">您無法為使用 Azure Active Directory 應用程式 Proxy 發佈的應用程式，指派使用 Microsoft 帳戶和來賓登入的使用者。</span><span class="sxs-lookup"><span data-stu-id="c52d6-152">Users who sign in with a Microsoft account and guests cannot be assigned for apps published with Azure Active Directory Application Proxy.</span></span> <span data-ttu-id="c52d6-153">請確定您使用屬於 hello 的認證登入的使用者與您要發行的 hello 應用程式相同的網域。</span><span class="sxs-lookup"><span data-stu-id="c52d6-153">Make sure your users sign in with credentials that are part of hello same domain as hello app you are publishing.</span></span>
> 
> 

## <a name="test-your-published-application"></a><span data-ttu-id="c52d6-154">測試已發佈的應用程式</span><span class="sxs-lookup"><span data-stu-id="c52d6-154">Test your published application</span></span>
<span data-ttu-id="c52d6-155">一旦您已經發行您的應用程式，您可以藉由瀏覽您發行的 toohello URL 測試它。</span><span class="sxs-lookup"><span data-stu-id="c52d6-155">Once you have published your application, you can test it out by navigating toohello URL that you published.</span></span> <span data-ttu-id="c52d6-156">確定您可以存取，且應用程式會正確地呈現，以及所有一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="c52d6-156">Make sure that you can access it, that it renders correctly, and that everything works as expected.</span></span> <span data-ttu-id="c52d6-157">如果您有問題或出現錯誤訊息，再試一次 hello[疑難排解指南](active-directory-application-proxy-troubleshoot.md)。</span><span class="sxs-lookup"><span data-stu-id="c52d6-157">If you have trouble or get an error message, try hello [troubleshooting guide](active-directory-application-proxy-troubleshoot.md).</span></span>

## <a name="configure-your-application"></a><span data-ttu-id="c52d6-158">設定您的應用程式</span><span class="sxs-lookup"><span data-stu-id="c52d6-158">Configure your application</span></span>
<span data-ttu-id="c52d6-159">您可以修改已發行的應用程式，或設定 hello 設定 頁面上的進階選項。</span><span class="sxs-lookup"><span data-stu-id="c52d6-159">You can modify published apps or set up advanced options on hello Configure page.</span></span> <span data-ttu-id="c52d6-160">這個頁面上，您可以變更 hello 名稱或上傳標誌，以自訂您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c52d6-160">On this page, you can customize your app by changing hello name or uploading a logo.</span></span> <span data-ttu-id="c52d6-161">您也可以管理存取規則一樣 hello 預先驗證方法或多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="c52d6-161">You can also manage access rules like hello preauthentication method or multi-factor authentication.</span></span>

![進階組態](./media/active-directory-application-proxy-publish/aad_appproxy_configure.png)

<span data-ttu-id="c52d6-163">發行應用程式之後使用 Azure Active Directory 應用程式 Proxy，它們會出現在 Azure AD 中在 hello 應用程式清單，並那里管理。</span><span class="sxs-lookup"><span data-stu-id="c52d6-163">After you publish applications using Azure Active Directory Application Proxy, they appear in hello Applications list in Azure AD, and you can manage them there.</span></span>

<span data-ttu-id="c52d6-164">如果您停用應用程式 Proxy 服務已發行應用程式之後，，就不再可從私人網路外部存取 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c52d6-164">If you disable Application Proxy services after you have published applications, hello applications are no longer accessible from outside your private network.</span></span> <span data-ttu-id="c52d6-165">您的使用者仍然可以存取 hello 應用程式內部像往常一樣。</span><span class="sxs-lookup"><span data-stu-id="c52d6-165">Your users can still access hello applications on-premises as usual.</span></span>

<span data-ttu-id="c52d6-166">tooview 應用程式，並確定它可以存取，按兩下 hello hello 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="c52d6-166">tooview an application and make sure that it is accessible, double-click hello name of hello application.</span></span> <span data-ttu-id="c52d6-167">如果 hello 應用程式 Proxy 服務已停用 hello 應用程式不提供，在 hello 囉 」 畫面最上方會出現警告訊息。</span><span class="sxs-lookup"><span data-stu-id="c52d6-167">If hello Application Proxy service is disabled and hello application is not available, a warning message appears at hello top of hello screen.</span></span>

<span data-ttu-id="c52d6-168">toodelete 應用程式，hello 清單中選取的應用程式，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="c52d6-168">toodelete an application, select an application in hello list and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c52d6-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c52d6-169">Next steps</span></span>
* [<span data-ttu-id="c52d6-170">使用您自己的網域名稱發行應用程式</span><span class="sxs-lookup"><span data-stu-id="c52d6-170">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="c52d6-171">啟用單一登入</span><span class="sxs-lookup"><span data-stu-id="c52d6-171">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="c52d6-172">啟用條件式存取</span><span class="sxs-lookup"><span data-stu-id="c52d6-172">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
* [<span data-ttu-id="c52d6-173">使用宣告感知應用程式</span><span class="sxs-lookup"><span data-stu-id="c52d6-173">Working with claims aware applications</span></span>](active-directory-application-proxy-claims-aware-apps.md)

<span data-ttu-id="c52d6-174">如 hello 最新消息和更新，請參閱 hello[應用程式 Proxy 部落格](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="c52d6-174">For hello latest news and updates, check out hello [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>

