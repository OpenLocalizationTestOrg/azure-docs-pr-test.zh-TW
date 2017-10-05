---
title: "使用 Azure AD 應用程式 Proxy 發佈應用程式 | Microsoft Docs"
description: "在 Azure 入口網站中使用 Azure AD 應用程式 Proxy 將內部部署應用程式發佈至雲端。"
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
ms.openlocfilehash: e00a939f2b20ab8e0a2ddf0ff91e59db440213ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="be87d-103">使用 Azure AD 應用程式 Proxy 發佈應用程式</span><span class="sxs-lookup"><span data-stu-id="be87d-103">Publish applications using Azure AD Application Proxy</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="be87d-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="be87d-104">Azure portal</span></span>](application-proxy-publish-azure-portal.md)
> * [<span data-ttu-id="be87d-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="be87d-105">Azure classic portal</span></span>](active-directory-application-proxy-publish.md)

<span data-ttu-id="be87d-106">Azure Active Directory (AD) 應用程式 Proxy 可藉由發佈要透過網際網路存取的內部部署應用程式，協助您支援遠端背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="be87d-106">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications to be accessed over the internet.</span></span> <span data-ttu-id="be87d-107">您可以透過 Azure 入口網站來發佈這些應用程式，提供從您網路外部的安全遠端存取。</span><span class="sxs-lookup"><span data-stu-id="be87d-107">You can publish these applications through the Azure portal to provide secure remote access from outside your network.</span></span>

<span data-ttu-id="be87d-108">本文會逐步引導您完成使用應用程式 Proxy 發佈內部部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="be87d-108">This article walks you through the steps to publish an on-premises app with Application Proxy.</span></span> <span data-ttu-id="be87d-109">完成本文之後，您的使用者將能夠從遠端存取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="be87d-109">After you complete this article, your users will be able to access your app remotely.</span></span> <span data-ttu-id="be87d-110">且您可以設定應用程式的單一登入、個人化資訊或安全性需求等額外功能。</span><span class="sxs-lookup"><span data-stu-id="be87d-110">And you'll be ready to configure extra features for the application like single sign-on, personalized information, and security requirements.</span></span>

<span data-ttu-id="be87d-111">如果您是應用程式 Proxy 的新手，可至[如何為內部部署應用程式提供安全的遠端存取](active-directory-application-proxy-get-started.md)深入了解這個功能。</span><span class="sxs-lookup"><span data-stu-id="be87d-111">If you're new to Application Proxy, learn more about this feature with the article [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md).</span></span>


## <a name="publish-an-on-premises-app-for-remote-access"></a><span data-ttu-id="be87d-112">發佈可遠端存取的內部部署應用程式</span><span class="sxs-lookup"><span data-stu-id="be87d-112">Publish an on-premises app for remote access</span></span>

<span data-ttu-id="be87d-113">遵循這些步驟可發佈您的應用程式與應用程式 Proxy。</span><span class="sxs-lookup"><span data-stu-id="be87d-113">Follow these steps to publish your apps with Application Proxy.</span></span> <span data-ttu-id="be87d-114">如果您尚未下載並為您的組織設定連接器，請先移至[開始使用應用程式 Proxy 並安裝連接器](active-directory-application-proxy-enable.md)，然後發佈您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="be87d-114">If you haven't already downloaded and configured a connector for your organization, go to [Get started with Application Proxy and install the connector](active-directory-application-proxy-enable.md) first, and then publish your app.</span></span>

> [!TIP]
> <span data-ttu-id="be87d-115">如果您是第一次測試應用程式 Proxy，請選擇設定為密碼型驗證的應用程式。</span><span class="sxs-lookup"><span data-stu-id="be87d-115">If you're testing out Application Proxy for the first time, choose an application that's set up for password-based authentication.</span></span> <span data-ttu-id="be87d-116">應用程式 Proxy 支援其他類型的驗證，但密碼型應用程式是開始使用並快速執行最簡單的方式。</span><span class="sxs-lookup"><span data-stu-id="be87d-116">Application Proxy supports other types of authentication, but password-based apps are the easiest to get up and running quickly.</span></span> 

1. <span data-ttu-id="be87d-117">在 [Azure 入口網站](https://portal.azure.com/)中，以系統管理員身分登入。</span><span class="sxs-lookup"><span data-stu-id="be87d-117">Sign in as an administrator in the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="be87d-118">選取 [Azure Active Directory]  >  [企業應用程式]  >  [新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="be87d-118">Select **Azure Active Directory** > **Enterprise applications** > **New application**.</span></span>

  ![新增企業應用程式](./media/application-proxy-publish-azure-portal/add-app.png)

3. <span data-ttu-id="be87d-120">依序選取 [所有]、[內部部署應用程式]。</span><span class="sxs-lookup"><span data-stu-id="be87d-120">Select **All**, then select **On-premises application**.</span></span>  

  ![新增您自己的應用程式](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. <span data-ttu-id="be87d-122">提供您的應用程式的下列資訊：</span><span class="sxs-lookup"><span data-stu-id="be87d-122">Provide the following information about your application:</span></span>

   - <span data-ttu-id="be87d-123">**名稱**︰會出現在存取面板上和 Azure 入口網站的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="be87d-123">**Name**: The name of the application that will appear on the access panel and in the Azure portal.</span></span> 

   - <span data-ttu-id="be87d-124">**內部 URL**：要從您私人網路中存取應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="be87d-124">**Internal URL**: The URL that you use to access the application from inside your private network.</span></span> <span data-ttu-id="be87d-125">您可以提供後端伺服器上要發佈的特定路徑，而伺服器的其餘部分則不發佈。</span><span class="sxs-lookup"><span data-stu-id="be87d-125">You can provide a specific path on the backend server to publish, while the rest of the server is unpublished.</span></span> <span data-ttu-id="be87d-126">如此一來，您可以在相同的伺服器上將不同網站發佈為不同應用程式，並給予各自的名稱和存取規則。</span><span class="sxs-lookup"><span data-stu-id="be87d-126">In this way, you can publish different sites on the same server as different apps, and give each one its own name and access rules.</span></span>

     > [!TIP]
     > <span data-ttu-id="be87d-127">如果您發佈路徑，請確定其中包含您的應用程式的所有必要映像、指令碼和樣式表。</span><span class="sxs-lookup"><span data-stu-id="be87d-127">If you publish a path, make sure that it includes all the necessary images, scripts, and style sheets for your application.</span></span> <span data-ttu-id="be87d-128">例如，如果您的應用程式位於 https://yourapp/app 並使用位於 https://yourapp/media 的映像，您應該發佈 https://yourapp/ 做為路徑。</span><span class="sxs-lookup"><span data-stu-id="be87d-128">For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as the path.</span></span> <span data-ttu-id="be87d-129">此內部 URL 不一定是您使用者所看見的登陸頁面。</span><span class="sxs-lookup"><span data-stu-id="be87d-129">This internal URL doesn't have to be the landing page your users see.</span></span> <span data-ttu-id="be87d-130">如需詳細資訊，請參閱[針對發佈應用程式設定自訂的首頁](application-proxy-office365-app-launcher.md)。</span><span class="sxs-lookup"><span data-stu-id="be87d-130">For more information, see [Set a custom home page for published apps](application-proxy-office365-app-launcher.md).</span></span>

   - <span data-ttu-id="be87d-131">**外部 URL**：您的使用者要前往此位址才能在您的網路之外存取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="be87d-131">**External URL**: The address your users will go to in order to access the app from outside your network.</span></span> <span data-ttu-id="be87d-132">如果您不想使用預設的應用程式 Proxy 網域，請閱讀 [Azure AD Application Proxy 中的自訂網域](active-directory-application-proxy-custom-domains.md)。</span><span class="sxs-lookup"><span data-stu-id="be87d-132">If you don't want to use the default Application Proxy domain, read about [custom domains in Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md).</span></span>
   - <span data-ttu-id="be87d-133">**預先驗證**︰應用程式 Proxy 在給予您的應用程式存取權前，用來驗證使用者的方式。</span><span class="sxs-lookup"><span data-stu-id="be87d-133">**Pre Authentication**: How Application Proxy verifies users before giving them access to your application.</span></span> 

     - <span data-ttu-id="be87d-134">Azure Active Directory︰應用程式 Proxy 會重新導向使用者以使用 Azure AD 登入，進而驗證目錄和應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="be87d-134">Azure Active Directory: Application Proxy redirects users to sign in with Azure AD, which authenticates their permissions for the directory and application.</span></span> <span data-ttu-id="be87d-135">建議您將這個選項保持為預設值，讓您可以利用諸如條件式存取以及 Multi-Factor Authentication 等 Azure AD 安全性功能。</span><span class="sxs-lookup"><span data-stu-id="be87d-135">We recommend keeping this option as the default, so that you can take advantage of Azure AD security features like conditional access and Multi-Factor Authentication.</span></span>
     - <span data-ttu-id="be87d-136">即時通行︰使用者不必向 Azure Active Directory 進行驗證即可存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="be87d-136">Passthrough: Users don't have to authenticate against Azure Active Directory to access the application.</span></span> <span data-ttu-id="be87d-137">您還是可以在後端設定驗證需求。</span><span class="sxs-lookup"><span data-stu-id="be87d-137">You can still set up authentication requirements on the backend.</span></span>
   - <span data-ttu-id="be87d-138">**連接器群組**︰連接器會處理針對應用程式的遠端存取，連接器群組可協助您依區域、網路或用途組織連接器和應用程式。</span><span class="sxs-lookup"><span data-stu-id="be87d-138">**Connector Group**: Connectors process the remote access to your application, and connector groups help you organize connectors and apps by region, network, or purpose.</span></span> <span data-ttu-id="be87d-139">如果您尚未建立任何連接器群組，您的應用程式就會指派給 [預設]。</span><span class="sxs-lookup"><span data-stu-id="be87d-139">If you don't have any connector groups created yet, your app is assigned to **Default**.</span></span>

   ![設定您的應用程式](./media/application-proxy-publish-azure-portal/configure-app.png)
5. <span data-ttu-id="be87d-141">如有必要，請設定其他設定。</span><span class="sxs-lookup"><span data-stu-id="be87d-141">If necessary, configure additional settings.</span></span> <span data-ttu-id="be87d-142">對於大部分的應用程式，您應該在其預設狀態中保留這些設定。</span><span class="sxs-lookup"><span data-stu-id="be87d-142">For most applications, you should keep these settings in their default states.</span></span> 
   - <span data-ttu-id="be87d-143">**後端應用程式逾時**：只有當您的應用程式太慢而無法驗證和連線時，才將此值設定為 [長]。</span><span class="sxs-lookup"><span data-stu-id="be87d-143">**Backend Application Timeout**: Set this value to **Long** only if your application is slow to authenticate and connect.</span></span> 
   - <span data-ttu-id="be87d-144">**轉譯標頭中的 URL**：除非您的應用程式需要驗證要求中的原始主機標頭，否則請將此值保留為 [是]。</span><span class="sxs-lookup"><span data-stu-id="be87d-144">**Translate URLs in Headers**: Keep this value as **Yes** unless your application required the original host header in the authentication request.</span></span>
   - <span data-ttu-id="be87d-145">**轉譯應用程式主體中的 URL**：除非您有其他內部部署應用程式的硬式編碼 HTML 連結，且未使用自訂網域，否則請將此值保留為 [否]。</span><span class="sxs-lookup"><span data-stu-id="be87d-145">**Translate URLs in Application Body**: Keep this value as **No** unless you have hardcoded HTML links to other on-premises applications, and don't use custom domains.</span></span> <span data-ttu-id="be87d-146">如需詳細資訊，請參閱[使用應用程式 Proxy 連結轉譯](application-proxy-link-translation.md)。</span><span class="sxs-lookup"><span data-stu-id="be87d-146">For more information, see [Link translation with Application Proxy](application-proxy-link-translation.md).</span></span>
   
   ![設定您的應用程式](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. <span data-ttu-id="be87d-148">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="be87d-148">Select **Add**.</span></span>


## <a name="add-a-test-user"></a><span data-ttu-id="be87d-149">新增測試使用者</span><span class="sxs-lookup"><span data-stu-id="be87d-149">Add a test user</span></span> 

<span data-ttu-id="be87d-150">若要測試您的應用程式是否已正確發佈，可新增一個測試使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="be87d-150">To test that your app was published correctly, add a test user account.</span></span> <span data-ttu-id="be87d-151">請確認此帳戶已有權限，可存取來自公司網路內部的應用程式。</span><span class="sxs-lookup"><span data-stu-id="be87d-151">Verify that this account already has permissions to access the app from inside the corporate network.</span></span>

1. <span data-ttu-id="be87d-152">在 [快速啟動] 刀鋒視窗中，選取 [指派測試使用者]。</span><span class="sxs-lookup"><span data-stu-id="be87d-152">Back on the Quick start blade, select **Assign a user for testing**.</span></span>

  ![指派測試使用者](./media/application-proxy-publish-azure-portal/assign-user.png)

2. <span data-ttu-id="be87d-154">在 [使用者和群組] 刀鋒視窗上，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="be87d-154">On the Users and groups blade, select **Add**.</span></span>

  ![新增使用者或群組](./media/application-proxy-publish-azure-portal/add-user.png)

3. <span data-ttu-id="be87d-156">在 [新增] 指派刀鋒視窗上，選取 [使用者和群組]，然後選擇您要新增的帳戶。</span><span class="sxs-lookup"><span data-stu-id="be87d-156">On the Add assignment blade, select **Users and groups** then choose the account you want to add.</span></span> 
4. <span data-ttu-id="be87d-157">選取 [指派]。</span><span class="sxs-lookup"><span data-stu-id="be87d-157">Select **Assign**.</span></span>

## <a name="test-your-published-app"></a><span data-ttu-id="be87d-158">測試已發佈的應用程式</span><span class="sxs-lookup"><span data-stu-id="be87d-158">Test your published app</span></span>

<span data-ttu-id="be87d-159">在瀏覽器中瀏覽至您在發行步驟所設定的外部 URL。</span><span class="sxs-lookup"><span data-stu-id="be87d-159">In your browser, navigate to the external URL that you configured during the publish step.</span></span> <span data-ttu-id="be87d-160">您應該會看到開始畫面，且能夠使用您設定的測試帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="be87d-160">You should see the start screen, and be able to sign in with the test account you set up.</span></span>

![測試已發佈的應用程式](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a><span data-ttu-id="be87d-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="be87d-162">Next steps</span></span>
- <span data-ttu-id="be87d-163">[下載連接器](active-directory-application-proxy-enable.md)和[建立連接器群組](active-directory-application-proxy-connectors-azure-portal.md)，在不同的網路和位置上發佈應用程式。</span><span class="sxs-lookup"><span data-stu-id="be87d-163">[Download connectors](active-directory-application-proxy-enable.md) and [create connector groups](active-directory-application-proxy-connectors-azure-portal.md) to publish applications on separate networks and locations.</span></span>

- <span data-ttu-id="be87d-164">為您新發佈的應用程式[設定單一登入](application-proxy-sso-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="be87d-164">[Set up single sign-on](application-proxy-sso-azure-portal.md) for your newly published app</span></span>
