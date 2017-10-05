---
title: "如何為您的應用程式服務應用程式設定 Azure Active Directory 驗證"
description: "了解如何為您的應用程式服務應用程式設定 Azure Active Directory 驗證。"
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: 6ec6a46c-bce4-47aa-b8a3-e133baef22eb
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: fe007fa8640d5641f29dc88f8f3a8ca52a1ca8ae
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-azure-active-directory-login"></a><span data-ttu-id="2d692-103">如何設定 App Service 應用程式使用 Azure Active Directory 登入</span><span class="sxs-lookup"><span data-stu-id="2d692-103">How to configure your App Service application to use Azure Active Directory login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="2d692-104">本主題說明如何設定 Azure 應用程式服務，以使用 Azure Active Directory 做為驗證提供者。</span><span class="sxs-lookup"><span data-stu-id="2d692-104">This topic shows you how to configure Azure App Services to use Azure Active Directory as an authentication provider.</span></span>

## <span data-ttu-id="2d692-105"><a name="express"> </a>使用快速設定設定 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d692-105"><a name="express"> </a>Configure Azure Active Directory using express settings</span></span>
1. <span data-ttu-id="2d692-106">在 [Azure 入口網站]中，瀏覽到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d692-106">In the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="2d692-107">依序按一下 [設定] 及 [驗證/授權]。</span><span class="sxs-lookup"><span data-stu-id="2d692-107">Click **Settings**, and then **Authentication/Authorization**.</span></span>
2. <span data-ttu-id="2d692-108">如果 [驗證/授權] 功能未啟用，請切換到 [開] 。</span><span class="sxs-lookup"><span data-stu-id="2d692-108">If the Authentication / Authorization feature is not enabled, turn the switch to **On**.</span></span>
3. <span data-ttu-id="2d692-109">按一下 [Azure Active Directory]，然後按一下 [管理模式] 下方的 [快速]。</span><span class="sxs-lookup"><span data-stu-id="2d692-109">Click **Azure Active Directory**, and then click **Express** under **Management Mode**.</span></span>
4. <span data-ttu-id="2d692-110">按一下 [確定]  以在 Azure Active Directory 中註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d692-110">Click **OK** to register the application in Azure Active Directory.</span></span> <span data-ttu-id="2d692-111">這樣會建立新的註冊。</span><span class="sxs-lookup"><span data-stu-id="2d692-111">This will create a new registration.</span></span> <span data-ttu-id="2d692-112">如果您想改為選擇現有的註冊，請按一下 [選取現有的應用程式]  ，然後在您的租用戶內搜尋先前建立之註冊的名稱。</span><span class="sxs-lookup"><span data-stu-id="2d692-112">If you want to choose an existing registration instead, click **Select an existing app** and then search for the name of a previously created registration within your tenant.</span></span>
   <span data-ttu-id="2d692-113">按一下註冊以選取它，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="2d692-113">Click the registration to select it and click **OK**.</span></span> <span data-ttu-id="2d692-114">然後在 Azure Active Directory 設定刀鋒視窗上按一下 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="2d692-114">Then click **OK** on the Azure Active Directory settings blade.</span></span>
   
   ![][0]
   
   <span data-ttu-id="2d692-115">App Service 預設會提供驗證，但不會限制對您網站內容和 API 的已授權存取。</span><span class="sxs-lookup"><span data-stu-id="2d692-115">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="2d692-116">您必須在應用程式程式碼中授權使用者。</span><span class="sxs-lookup"><span data-stu-id="2d692-116">You must authorize users in your app code.</span></span>
5. <span data-ttu-id="2d692-117">(選擇性) 若要限制只有透過 Azure Active Directory 授權的使用者可以存取您的網站，請將 [要求未經驗證時所採取的動作] 設為 [使用 Azure Active Directory 登入]。</span><span class="sxs-lookup"><span data-stu-id="2d692-117">(Optional) To restrict access to your site to only users authenticated by Azure Active Directory, set **Action to take when request is not authenticated** to **Log in with Azure Active Directory**.</span></span> <span data-ttu-id="2d692-118">這會要求所有要求都需經過驗證，且所有未經驗證的要求都會重新導向至 Azure Active Directory 以進行驗證。</span><span class="sxs-lookup"><span data-stu-id="2d692-118">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Azure Active Directory for authentication.</span></span>
6. <span data-ttu-id="2d692-119">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2d692-119">Click **Save**.</span></span>

<span data-ttu-id="2d692-120">現在，您已可在應用程式中使用 Azure Active Directory 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="2d692-120">You are now ready to use Azure Active Directory for authentication in your app.</span></span>

## <span data-ttu-id="2d692-121"><a name="advanced"> </a>(替代方法) 使用進階設定手動設定 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d692-121"><a name="advanced"> </a>(Alternative method) Manually configure Azure Active Directory with advanced settings</span></span>
<span data-ttu-id="2d692-122">您也可以選擇手動提供組態設定。</span><span class="sxs-lookup"><span data-stu-id="2d692-122">You can also choose to provide configuration settings manually.</span></span> <span data-ttu-id="2d692-123">如果您想使用的 AAD 租用戶不同於您登入 Azure 所用的租用戶，這會是較佳的解決方案。</span><span class="sxs-lookup"><span data-stu-id="2d692-123">This is the preferred solution if the AAD tenant you wish to use is different from the tenant with which you sign into Azure.</span></span> <span data-ttu-id="2d692-124">若要完成組態，您必須先在 Azure Active Directory 中建立註冊，接著必須提供一些註冊詳細資料給 App Service。</span><span class="sxs-lookup"><span data-stu-id="2d692-124">To complete the configuration, you must first create a registration in Azure Active Directory, and then you must provide some of the registration details to App Service.</span></span>

### <span data-ttu-id="2d692-125"><a name="register"> </a>向 Azure Active Directory 註冊您的應用程式</span><span class="sxs-lookup"><span data-stu-id="2d692-125"><a name="register"> </a>Register your application with Azure Active Directory</span></span>
1. <span data-ttu-id="2d692-126">登入 [Azure 入口網站]，並瀏覽到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d692-126">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="2d692-127">複製您的 **URL**。</span><span class="sxs-lookup"><span data-stu-id="2d692-127">Copy your **URL**.</span></span> <span data-ttu-id="2d692-128">您將使用此資訊設定 Azure Active Directory 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d692-128">You will use this to configure your Azure Active Directory app.</span></span>
2. <span data-ttu-id="2d692-129">登入 [Active Directory] ，並瀏覽到 **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="2d692-129">Sign in to the [Azure classic portal] and navigate to **Active Directory**.</span></span>
   
    ![][2]
3. <span data-ttu-id="2d692-130">選取您的目錄，然後選取頂端的 [ **應用程式** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2d692-130">Select your directory, and then select the **Applications** tab at the top.</span></span> <span data-ttu-id="2d692-131">按一下底部的 [ **新增** ]，以建立新的應用程式註冊。</span><span class="sxs-lookup"><span data-stu-id="2d692-131">Click **ADD** at the bottom to create a new app registration.</span></span>
4. <span data-ttu-id="2d692-132">按一下 [Add an application my organization is developing] 。</span><span class="sxs-lookup"><span data-stu-id="2d692-132">Click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="2d692-133">在 [新增應用程式精靈] 中，輸入應用程式的 [名稱]，然後按一下 [Web 應用程式和/或 Web API] 類型。</span><span class="sxs-lookup"><span data-stu-id="2d692-133">In the Add Application Wizard, enter a **Name** for your application and click the  **Web Application And/Or Web API** type.</span></span> <span data-ttu-id="2d692-134">接著，按一下以繼續。</span><span class="sxs-lookup"><span data-stu-id="2d692-134">Then click to continue.</span></span>
6. <span data-ttu-id="2d692-135">在 [登入 URL]  方塊中，貼上您之前複製的應用程式 URL。</span><span class="sxs-lookup"><span data-stu-id="2d692-135">In the **SIGN-ON URL** box, paste the application URL you copied earlier.</span></span> <span data-ttu-id="2d692-136">在 [應用程式識別碼 URI]  方塊中輸入相同的 URL。</span><span class="sxs-lookup"><span data-stu-id="2d692-136">Enter that same URL in the **App ID URI** box.</span></span> <span data-ttu-id="2d692-137">接著，按一下以繼續。</span><span class="sxs-lookup"><span data-stu-id="2d692-137">Then click to continue.</span></span>
7. <span data-ttu-id="2d692-138">新增應用程式之後，按一下 [設定]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2d692-138">Once the application has been added, click the **Configure** tab.</span></span> <span data-ttu-id="2d692-139">將 [單一登入] 下的 [回覆 URL] 編輯成您應用程式的 URL，並加上 /.auth/login/aad/callback 路徑。</span><span class="sxs-lookup"><span data-stu-id="2d692-139">Edit the **Reply URL** under **Single Sign-on** to be the URL of your application appended with the path, */.auth/login/aad/callback*.</span></span> <span data-ttu-id="2d692-140">例如， `https://contoso.azurewebsites.net/.auth/login/aad/callback`。</span><span class="sxs-lookup"><span data-stu-id="2d692-140">For example, `https://contoso.azurewebsites.net/.auth/login/aad/callback`.</span></span> <span data-ttu-id="2d692-141">請確實使用 HTTPS 配置。</span><span class="sxs-lookup"><span data-stu-id="2d692-141">Make sure that you are using the HTTPS scheme.</span></span>
   
    ![][3]
8. <span data-ttu-id="2d692-142">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2d692-142">Click **Save**.</span></span> <span data-ttu-id="2d692-143">然後，複製應用程式的 [用戶端識別碼]。</span><span class="sxs-lookup"><span data-stu-id="2d692-143">Then copy the **Client ID** for the app.</span></span> <span data-ttu-id="2d692-144">稍後您會設定您的應用程式使用此資訊。</span><span class="sxs-lookup"><span data-stu-id="2d692-144">You will configure your application to use this later.</span></span>
9. <span data-ttu-id="2d692-145">在底部命令列中，按一下 [檢視端點]，然後複製 [同盟中繼資料文件] URL 並下載該文件，或在瀏覽器中瀏覽至該文件。</span><span class="sxs-lookup"><span data-stu-id="2d692-145">In the bottom command bar, click **View Endpoints**, and then copy the **Federation Metadata Document** URL and download that document or navigate to it in a browser.</span></span>
10. <span data-ttu-id="2d692-146">在根 **EntityDescriptor** 元素中，應該會有 `https://sts.windows.net/` 格式的 **entityID** 屬性，後面是您的租用戶專屬的 GUID (稱為「租用戶識別碼」)。</span><span class="sxs-lookup"><span data-stu-id="2d692-146">Within the root **EntityDescriptor** element, there should be an **entityID** attribute of the form `https://sts.windows.net/` followed by a GUID specific to your tenant (called a "tenant ID").</span></span> <span data-ttu-id="2d692-147">複製這個值，此值將做為您的「簽發者 URL」 。</span><span class="sxs-lookup"><span data-stu-id="2d692-147">Copy this value - it will serve as your **Issuer URL**.</span></span> <span data-ttu-id="2d692-148">稍後您會設定您的應用程式使用此資訊。</span><span class="sxs-lookup"><span data-stu-id="2d692-148">You will configure your application to use this later.</span></span>

### <span data-ttu-id="2d692-149"><a name="secrets"> </a>將 Azure Active Directory 資訊新增至應用程式</span><span class="sxs-lookup"><span data-stu-id="2d692-149"><a name="secrets"> </a>Add Azure Active Directory information to your application</span></span>
1. <span data-ttu-id="2d692-150">回到 [Azure 入口網站]，並瀏覽到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d692-150">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="2d692-151">依序按一下 [設定] 及 [驗證/授權]。</span><span class="sxs-lookup"><span data-stu-id="2d692-151">Click **Settings**, and then **Authentication/Authorization**.</span></span>
2. <span data-ttu-id="2d692-152">如果 [驗證/授權] 功能未啟用，請切換到 [ **開啟**]。</span><span class="sxs-lookup"><span data-stu-id="2d692-152">If the Authentication/Authorization feature is not enabled, turn the switch to **On**.</span></span>
3. <span data-ttu-id="2d692-153">按一下 [Azure Active Directory]，然後按一下 [管理模式] 下方的 [進階]。</span><span class="sxs-lookup"><span data-stu-id="2d692-153">Click **Azure Active Directory**, and then click **Advanced** under **Management Mode**.</span></span> <span data-ttu-id="2d692-154">貼入您先前取得的用戶端識別碼和簽發者 URL 值。</span><span class="sxs-lookup"><span data-stu-id="2d692-154">Paste in the Client ID and Issuer URL value which you obtained previously.</span></span> <span data-ttu-id="2d692-155">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="2d692-155">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="2d692-156">App Service 預設會提供驗證，但不會限制對您網站內容和 API 的已授權存取。</span><span class="sxs-lookup"><span data-stu-id="2d692-156">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="2d692-157">您必須在應用程式程式碼中授權使用者。</span><span class="sxs-lookup"><span data-stu-id="2d692-157">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="2d692-158">(選擇性) 若要限制只有透過 Azure Active Directory 授權的使用者可以存取您的網站，請將 [要求未經驗證時所採取的動作] 設為 [使用 Azure Active Directory 登入]。</span><span class="sxs-lookup"><span data-stu-id="2d692-158">(Optional) To restrict access to your site to only users authenticated by Azure Active Directory, set **Action to take when request is not authenticated** to **Log in with Azure Active Directory**.</span></span> <span data-ttu-id="2d692-159">這會要求所有要求都需經過驗證，且所有未經驗證的要求都會重新導向至 Azure Active Directory 以進行驗證。</span><span class="sxs-lookup"><span data-stu-id="2d692-159">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Azure Active Directory for authentication.</span></span>
5. <span data-ttu-id="2d692-160">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2d692-160">Click **Save**.</span></span>

<span data-ttu-id="2d692-161">現在，您已可在應用程式中使用 Azure Active Directory 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="2d692-161">You are now ready to use Azure Active Directory for authentication in your app.</span></span>

## <a name="optional-configure-a-native-client-application"></a><span data-ttu-id="2d692-162">(選擇性步驟) 設定原生用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="2d692-162">(Optional) Configure a native client application</span></span>
<span data-ttu-id="2d692-163">Azure Active Directory 也可讓您註冊更能控制權限對應的原生用戶端。</span><span class="sxs-lookup"><span data-stu-id="2d692-163">Azure Active Directory also allows you to register native clients, which provides greater control over permissions mapping.</span></span> <span data-ttu-id="2d692-164">若您想要使用 **Active Directory Authentication Library**等程式庫執行登入，您會需要該功能。</span><span class="sxs-lookup"><span data-stu-id="2d692-164">You need this if you wish to perform logins using a library such as the **Active Directory Authentication Library**.</span></span>

1. <span data-ttu-id="2d692-165">請瀏覽到 **Azure 傳統入口網站** 中的 [Active Directory]</span><span class="sxs-lookup"><span data-stu-id="2d692-165">Navigate to **Active Directory** in the [Azure classic portal].</span></span>
2. <span data-ttu-id="2d692-166">選取您的目錄，然後選取頂端的 [ **應用程式** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2d692-166">Select your directory, and then select the **Applications** tab at the top.</span></span> <span data-ttu-id="2d692-167">按一下底部的 [ **新增** ]，以建立新的應用程式註冊。</span><span class="sxs-lookup"><span data-stu-id="2d692-167">Click **ADD** at the bottom to create a new app registration.</span></span>
3. <span data-ttu-id="2d692-168">按一下 [Add an application my organization is developing] 。</span><span class="sxs-lookup"><span data-stu-id="2d692-168">Click **Add an application my organization is developing**.</span></span>
4. <span data-ttu-id="2d692-169">在 [新增應用程式精靈] 中，輸入應用程式的 [名稱]，然後按一下 [原生用戶端應用程式] 類型。</span><span class="sxs-lookup"><span data-stu-id="2d692-169">In the Add Application Wizard, enter a **Name** for your application and click the  **Native Client Application** type.</span></span> <span data-ttu-id="2d692-170">接著，按一下以繼續。</span><span class="sxs-lookup"><span data-stu-id="2d692-170">Then click to continue.</span></span>
5. <span data-ttu-id="2d692-171">在 [重新導向 URI] 方塊中，使用 HTTPS 配置輸入您網站的 /.auth/login/done 端點。</span><span class="sxs-lookup"><span data-stu-id="2d692-171">In the **Redirect URI** box, enter your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="2d692-172">此值應與 *https://contoso.azurewebsites.net/.auth/login/done* 類似。</span><span class="sxs-lookup"><span data-stu-id="2d692-172">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span> <span data-ttu-id="2d692-173">如果是建立 Windows 應用程式，請改用 [封裝 SID](app-service-mobile-dotnet-how-to-use-client-library.md#package-sid) 作為 URI。</span><span class="sxs-lookup"><span data-stu-id="2d692-173">If creating a Windows application, instead use the [package SID](app-service-mobile-dotnet-how-to-use-client-library.md#package-sid) as the URI.</span></span>
6. <span data-ttu-id="2d692-174">新增原生應用程式之後，按一下 [ **設定** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2d692-174">Once the native application has been added, click the **Configure** tab.</span></span> <span data-ttu-id="2d692-175">請找到 **用戶端識別碼** 並記下該值。</span><span class="sxs-lookup"><span data-stu-id="2d692-175">Find the **Client ID** and make a note of this value.</span></span>
7. <span data-ttu-id="2d692-176">將頁面向下捲動至 [其他應用程式的權限] 區段，然後按一下 [新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="2d692-176">Scroll the page down to the **Permissions to other applications** section and click **Add application**.</span></span>
8. <span data-ttu-id="2d692-177">搜尋先前註冊的 Web 應用程式，再按一下加號圖示。</span><span class="sxs-lookup"><span data-stu-id="2d692-177">Search for the web application that you registered earlier and click the plus icon.</span></span> <span data-ttu-id="2d692-178">然後按一下核取標記以關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="2d692-178">Then click the check to close the dialog.</span></span> <span data-ttu-id="2d692-179">如果找不到 Web 應用程式，瀏覽至其註冊並加入新的回覆 URL (例如，您目前 URL 的 HTTP 版本)，按一下 [儲存]，然後重複這些步驟 - 應用程式應該會顯示在清單中。</span><span class="sxs-lookup"><span data-stu-id="2d692-179">If the web application cannot be found, navigate to its registration and add a new reply URL (e.g., the HTTP version of your current URL), click save, and then repeat these steps - the application should show up in the list.</span></span>
9. <span data-ttu-id="2d692-180">在您剛才新增的新項目上，開啟 [委派的權限] 下拉式清單，然後選取 [存取 (appName)]。</span><span class="sxs-lookup"><span data-stu-id="2d692-180">On the new entry you just added, open the **Delegated Permissions** dropdown and select **Access (appName)**.</span></span> <span data-ttu-id="2d692-181">然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2d692-181">Then click **Save**.</span></span>

<span data-ttu-id="2d692-182">您現在已設定了可以存取您 App Service 應用程式的原生用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d692-182">You have now configured a native client application which can access your App Service application.</span></span>

## <span data-ttu-id="2d692-183"><a name="related-content"> </a>相關內容</span><span class="sxs-lookup"><span data-stu-id="2d692-183"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/mobile-app-aad-express-settings.png
[1]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/mobile-app-aad-advanced-settings.png
[2]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/app-service-navigate-aad.png
[3]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/app-service-aad-app-configure.png

<!-- URLs. -->

<span data-ttu-id="2d692-184">[Azure 入口網站]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="2d692-184">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="2d692-185">[Active Directory]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="2d692-185">[Azure classic portal]: https://manage.windowsazure.com/</span></span>
[alternative method]:#advanced
