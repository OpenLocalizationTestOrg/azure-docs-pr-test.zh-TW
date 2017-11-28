---
title: "aaaPublish 應用程式與 Azure AD Application Proxy |Microsoft 文件"
description: "發行與 Azure AD Application Proxy 的內部部署應用程式 toohello 雲端中的 hello Azure 入口網站。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ed5458467fb7d4376f65a222f1ba5f23cfdfc57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="74818-103">使用 Azure AD 應用程式 Proxy 發佈應用程式</span><span class="sxs-lookup"><span data-stu-id="74818-103">Publish applications using Azure AD Application Proxy</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="74818-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="74818-104">Azure portal</span></span>](application-proxy-publish-azure-portal.md)
> * [<span data-ttu-id="74818-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="74818-105">Azure classic portal</span></span>](active-directory-application-proxy-publish.md)

<span data-ttu-id="74818-106">Azure Active Directory (AD) 應用程式 Proxy 可協助您支援遠端工作者所發佈在內部部署應用程式 toobe hello 透過存取網際網路。</span><span class="sxs-lookup"><span data-stu-id="74818-106">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications toobe accessed over hello internet.</span></span> <span data-ttu-id="74818-107">您可以發行這些應用程式透過 hello Azure 入口網站 tooprovide 安全遠端存取從網路外部。</span><span class="sxs-lookup"><span data-stu-id="74818-107">You can publish these applications through hello Azure portal tooprovide secure remote access from outside your network.</span></span>

<span data-ttu-id="74818-108">這篇文章會引導您 hello 步驟 toopublish 在內部部署應用程式，但應用程式 Proxy。</span><span class="sxs-lookup"><span data-stu-id="74818-108">This article walks you through hello steps toopublish an on-premises app with Application Proxy.</span></span> <span data-ttu-id="74818-109">完成本文之後，您的使用者將會是能 tooaccess 您的應用程式從遠端。</span><span class="sxs-lookup"><span data-stu-id="74818-109">After you complete this article, your users will be able tooaccess your app remotely.</span></span> <span data-ttu-id="74818-110">是您已準備就緒 tooconfigure hello 應用程式，例如額外的功能和單一登入、 個人化的資訊和安全性需求。</span><span class="sxs-lookup"><span data-stu-id="74818-110">And you'll be ready tooconfigure extra features for hello application like single sign-on, personalized information, and security requirements.</span></span>

<span data-ttu-id="74818-111">如果您是新 tooApplication Proxy，深入了解這項功能與 hello 文章[如何 tooprovide 安全的遠端存取 tooon 內部部署應用程式](active-directory-application-proxy-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="74818-111">If you're new tooApplication Proxy, learn more about this feature with hello article [How tooprovide secure remote access tooon-premises applications](active-directory-application-proxy-get-started.md).</span></span>


## <a name="publish-an-on-premises-app-for-remote-access"></a><span data-ttu-id="74818-112">發佈可遠端存取的內部部署應用程式</span><span class="sxs-lookup"><span data-stu-id="74818-112">Publish an on-premises app for remote access</span></span>

<span data-ttu-id="74818-113">請遵循這些步驟 toopublish 您的應用程式與應用程式 Proxy。</span><span class="sxs-lookup"><span data-stu-id="74818-113">Follow these steps toopublish your apps with Application Proxy.</span></span> <span data-ttu-id="74818-114">如果您沒有已下載，並為您的組織設定連接器，請移至太[應用程式 Proxy 快速入門及安裝 hello 連接器](active-directory-application-proxy-enable.md)第一次，然後發行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="74818-114">If you haven't already downloaded and configured a connector for your organization, go too[Get started with Application Proxy and install hello connector](active-directory-application-proxy-enable.md) first, and then publish your app.</span></span>

> [!TIP]
> <span data-ttu-id="74818-115">如果您要測試應用程式 Proxy 出 hello 第一次，請選擇 設定密碼型驗證的應用程式。</span><span class="sxs-lookup"><span data-stu-id="74818-115">If you're testing out Application Proxy for hello first time, choose an application that's set up for password-based authentication.</span></span> <span data-ttu-id="74818-116">應用程式 Proxy 支援其他類型的驗證，但密碼為基礎的應用程式總 hello 最簡單 tooget 快速及執行。</span><span class="sxs-lookup"><span data-stu-id="74818-116">Application Proxy supports other types of authentication, but password-based apps are hello easiest tooget up and running quickly.</span></span> 

1. <span data-ttu-id="74818-117">Hello 中的系統管理員身分登入[Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="74818-117">Sign in as an administrator in hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="74818-118">選取 [Azure Active Directory]  >  [企業應用程式]  >  [新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="74818-118">Select **Azure Active Directory** > **Enterprise applications** > **New application**.</span></span>

  ![新增企業應用程式](./media/application-proxy-publish-azure-portal/add-app.png)

3. <span data-ttu-id="74818-120">依序選取 [所有]、[內部部署應用程式]。</span><span class="sxs-lookup"><span data-stu-id="74818-120">Select **All**, then select **On-premises application**.</span></span>  

  ![新增您自己的應用程式](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. <span data-ttu-id="74818-122">提供下列應用程式的相關資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="74818-122">Provide hello following information about your application:</span></span>

   - <span data-ttu-id="74818-123">**名稱**: hello 名稱會出現在 hello 存取面板和 hello Azure 入口網站中的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="74818-123">**Name**: hello name of hello application that will appear on hello access panel and in hello Azure portal.</span></span> 

   - <span data-ttu-id="74818-124">**內部 URL**: hello 您 tooaccess hello 從使用應用程式在私人網路內部的 URL。</span><span class="sxs-lookup"><span data-stu-id="74818-124">**Internal URL**: hello URL that you use tooaccess hello application from inside your private network.</span></span> <span data-ttu-id="74818-125">未發行的 hello 伺服器 hello rest 時，您可以在 hello 後端伺服器 toopublish，提供特定路徑。</span><span class="sxs-lookup"><span data-stu-id="74818-125">You can provide a specific path on hello backend server toopublish, while hello rest of hello server is unpublished.</span></span> <span data-ttu-id="74818-126">如此一來，您可以將不同站台發佈在 hello 與不同的應用程式相同的伺服器，並提供每一個其名稱和存取規則。</span><span class="sxs-lookup"><span data-stu-id="74818-126">In this way, you can publish different sites on hello same server as different apps, and give each one its own name and access rules.</span></span>

     > [!TIP]
     > <span data-ttu-id="74818-127">如果您發行路徑，請確定它包含所有的 hello 所需的映像、 指令碼和您的應用程式的樣式表。</span><span class="sxs-lookup"><span data-stu-id="74818-127">If you publish a path, make sure that it includes all hello necessary images, scripts, and style sheets for your application.</span></span> <span data-ttu-id="74818-128">例如，如果您的應用程式位於 https://yourapp/app，並且使用位於 https://yourapp/media 映像，然後您應該發佈 https://yourapp/ hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="74818-128">For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as hello path.</span></span> <span data-ttu-id="74818-129">此內部 URL 沒有 toobe hello 登陸頁面，請參閱您的使用者。</span><span class="sxs-lookup"><span data-stu-id="74818-129">This internal URL doesn't have toobe hello landing page your users see.</span></span> <span data-ttu-id="74818-130">如需詳細資訊，請參閱[針對發佈應用程式設定自訂的首頁](application-proxy-office365-app-launcher.md)。</span><span class="sxs-lookup"><span data-stu-id="74818-130">For more information, see [Set a custom home page for published apps](application-proxy-office365-app-launcher.md).</span></span>

   - <span data-ttu-id="74818-131">**外部 URL**: hello 您的使用者將會移 tooin 順序 tooaccess hello 應用程式從外部網路的位址。</span><span class="sxs-lookup"><span data-stu-id="74818-131">**External URL**: hello address your users will go tooin order tooaccess hello app from outside your network.</span></span> <span data-ttu-id="74818-132">如果您不想 toouse hello 預設應用程式 Proxy 的網域，閱讀[Azure AD Application Proxy 中的自訂網域](active-directory-application-proxy-custom-domains.md)。</span><span class="sxs-lookup"><span data-stu-id="74818-132">If you don't want toouse hello default Application Proxy domain, read about [custom domains in Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md).</span></span>
   - <span data-ttu-id="74818-133">**預先驗證**： 應用程式 Proxy 如何授與存取 tooyour 應用程式之前驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="74818-133">**Pre Authentication**: How Application Proxy verifies users before giving them access tooyour application.</span></span> 

     - <span data-ttu-id="74818-134">Azure Active Directory： 應用程式 Proxy 會重新導向使用者 toosign 入 Azure AD，驗證其 hello 目錄和應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="74818-134">Azure Active Directory: Application Proxy redirects users toosign in with Azure AD, which authenticates their permissions for hello directory and application.</span></span> <span data-ttu-id="74818-135">我們建議您保持為 hello 預設值，這個選項，讓您可以利用 Azure AD 安全性功能，例如條件式存取以及多因素驗證。</span><span class="sxs-lookup"><span data-stu-id="74818-135">We recommend keeping this option as hello default, so that you can take advantage of Azure AD security features like conditional access and Multi-Factor Authentication.</span></span>
     - <span data-ttu-id="74818-136">通過： 使用者不能 tooauthenticate 針對 Azure Active Directory tooaccess hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="74818-136">Passthrough: Users don't have tooauthenticate against Azure Active Directory tooaccess hello application.</span></span> <span data-ttu-id="74818-137">您仍然可以設定 hello 後端上的驗證需求。</span><span class="sxs-lookup"><span data-stu-id="74818-137">You can still set up authentication requirements on hello backend.</span></span>
   - <span data-ttu-id="74818-138">**連接器群組**： 連接器程序 hello 遠端存取 tooyour 應用程式，以及協助您組織連接器和應用程式區域、 網路或目的連接器群組。</span><span class="sxs-lookup"><span data-stu-id="74818-138">**Connector Group**: Connectors process hello remote access tooyour application, and connector groups help you organize connectors and apps by region, network, or purpose.</span></span> <span data-ttu-id="74818-139">如果您還沒有尚未建立任何連接器群組，您的應用程式會指派太**預設**。</span><span class="sxs-lookup"><span data-stu-id="74818-139">If you don't have any connector groups created yet, your app is assigned too**Default**.</span></span>

   ![設定您的應用程式](./media/application-proxy-publish-azure-portal/configure-app.png)
5. <span data-ttu-id="74818-141">如有必要，請設定其他設定。</span><span class="sxs-lookup"><span data-stu-id="74818-141">If necessary, configure additional settings.</span></span> <span data-ttu-id="74818-142">對於大部分的應用程式，您應該在其預設狀態中保留這些設定。</span><span class="sxs-lookup"><span data-stu-id="74818-142">For most applications, you should keep these settings in their default states.</span></span> 
   - <span data-ttu-id="74818-143">**後端應用程式逾時**： 將此值設定為太**長**只有在您的應用程式為緩慢 tooauthenticate 和連接。</span><span class="sxs-lookup"><span data-stu-id="74818-143">**Backend Application Timeout**: Set this value too**Long** only if your application is slow tooauthenticate and connect.</span></span> 
   - <span data-ttu-id="74818-144">**轉譯標頭中的 Url**： 保留此值做為**是**除非您的應用程式所需的 hello 原始主機標頭在 hello 驗證要求。</span><span class="sxs-lookup"><span data-stu-id="74818-144">**Translate URLs in Headers**: Keep this value as **Yes** unless your application required hello original host header in hello authentication request.</span></span>
   - <span data-ttu-id="74818-145">**將轉譯 Url 中的應用程式主體**： 保留此值做為**否**除非您有硬式編碼的 HTML 連結 tooother 在內部部署應用程式，而未使用自訂網域。</span><span class="sxs-lookup"><span data-stu-id="74818-145">**Translate URLs in Application Body**: Keep this value as **No** unless you have hardcoded HTML links tooother on-premises applications, and don't use custom domains.</span></span> <span data-ttu-id="74818-146">如需詳細資訊，請參閱[使用應用程式 Proxy 連結轉譯](application-proxy-link-translation.md)。</span><span class="sxs-lookup"><span data-stu-id="74818-146">For more information, see [Link translation with Application Proxy](application-proxy-link-translation.md).</span></span>
   
   ![設定您的應用程式](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. <span data-ttu-id="74818-148">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="74818-148">Select **Add**.</span></span>


## <a name="add-a-test-user"></a><span data-ttu-id="74818-149">新增測試使用者</span><span class="sxs-lookup"><span data-stu-id="74818-149">Add a test user</span></span> 

<span data-ttu-id="74818-150">tootest 發行應用程式已正確地加入測試使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="74818-150">tootest that your app was published correctly, add a test user account.</span></span> <span data-ttu-id="74818-151">請確認此帳戶已經有權限 tooaccess hello 應用程式從 hello 公司網路內。</span><span class="sxs-lookup"><span data-stu-id="74818-151">Verify that this account already has permissions tooaccess hello app from inside hello corporate network.</span></span>

1. <span data-ttu-id="74818-152">在 hello 快速入門刀鋒視窗中，選取 **指派給使用者的測試**。</span><span class="sxs-lookup"><span data-stu-id="74818-152">Back on hello Quick start blade, select **Assign a user for testing**.</span></span>

  ![指派測試使用者](./media/application-proxy-publish-azure-portal/assign-user.png)

2. <span data-ttu-id="74818-154">在 hello 使用者和群組 刀鋒視窗中，選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="74818-154">On hello Users and groups blade, select **Add**.</span></span>

  ![新增使用者或群組](./media/application-proxy-publish-azure-portal/add-user.png)

3. <span data-ttu-id="74818-156">在 hello 新增指派刀鋒視窗中，選取 **使用者和群組**然後選擇您想要讓 tooadd 的 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="74818-156">On hello Add assignment blade, select **Users and groups** then choose hello account you want tooadd.</span></span> 
4. <span data-ttu-id="74818-157">選取 [指派]。</span><span class="sxs-lookup"><span data-stu-id="74818-157">Select **Assign**.</span></span>

## <a name="test-your-published-app"></a><span data-ttu-id="74818-158">測試已發佈的應用程式</span><span class="sxs-lookup"><span data-stu-id="74818-158">Test your published app</span></span>

<span data-ttu-id="74818-159">在瀏覽器中，瀏覽 toohello hello 在您已設定的外部 URL 發行步驟。</span><span class="sxs-lookup"><span data-stu-id="74818-159">In your browser, navigate toohello external URL that you configured during hello publish step.</span></span> <span data-ttu-id="74818-160">您應該會看到 hello [開始] 畫面，且無法 toosign 以 hello 測試帳戶您設定。</span><span class="sxs-lookup"><span data-stu-id="74818-160">You should see hello start screen, and be able toosign in with hello test account you set up.</span></span>

![測試已發佈的應用程式](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a><span data-ttu-id="74818-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="74818-162">Next steps</span></span>
- <span data-ttu-id="74818-163">[下載連接器](active-directory-application-proxy-enable.md)和[建立連接器群組](active-directory-application-proxy-connectors-azure-portal.md)toopublish 應用程式在不同的網路和位置。</span><span class="sxs-lookup"><span data-stu-id="74818-163">[Download connectors](active-directory-application-proxy-enable.md) and [create connector groups](active-directory-application-proxy-connectors-azure-portal.md) toopublish applications on separate networks and locations.</span></span>

- <span data-ttu-id="74818-164">為您新發佈的應用程式[設定單一登入](application-proxy-sso-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="74818-164">[Set up single sign-on](application-proxy-sso-azure-portal.md) for your newly published app</span></span>
