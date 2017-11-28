---
title: "Active Directory B2C aaaAzure |Microsoft 文件"
description: "如何 toobuild sign-up/登入、 具有 web 應用程式設定檔編輯及使用 Azure Active Directory B2C 重設密碼。"
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: barbaraselden
ms.assetid: 30261336-d7a5-4a6d-8c1a-7943ad76ed25
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 187f99a8dd50d212de4f0517f552cdbbe5a8edf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a><span data-ttu-id="c05bc-103">建立支援 Azure Active Directory B2C 註冊、登入、設定檔編輯及密碼重設的 ASP.NET Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c05bc-103">Create an ASP.NET web app with Azure Active Directory B2C sign-up, sign-in, profile edit, and password reset</span></span>

<span data-ttu-id="c05bc-104">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="c05bc-104">This tutorial shows you how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c05bc-105">新增 Azure AD B2C 身分識別功能 tooyour web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c05bc-105">Add Azure AD B2C identity features tooyour web app</span></span>
> * <span data-ttu-id="c05bc-106">在您的 Azure AD B2C 目錄中註冊 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c05bc-106">Register your web app in your Azure AD B2C directory</span></span>
> * <span data-ttu-id="c05bc-107">為您的 Web 應用程式建立使用者註冊/登入、編輯設定檔和密碼重設原則</span><span class="sxs-lookup"><span data-stu-id="c05bc-107">Create a user sign-up/sign-in, profile edit, and password reset policy for your web app</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c05bc-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="c05bc-108">Prerequisites</span></span>

- <span data-ttu-id="c05bc-109">您必須連接您 B2C 租用戶 tooan Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c05bc-109">You must connect your B2C Tenant tooan Azure account.</span></span> <span data-ttu-id="c05bc-110">您可以在[這裡](https://azure.microsoft.com/en-us/)建立免費的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c05bc-110">You can create a free Azure account [here](https://azure.microsoft.com/en-us/).</span></span>
- <span data-ttu-id="c05bc-111">您需要[Microsoft Visual Studio](https://www.visualstudio.com/)或類似的程式 tooview 和修改 hello 範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="c05bc-111">You need [Microsoft Visual Studio](https://www.visualstudio.com/) or a similar program tooview and modify hello sample code.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="c05bc-112">建立 Azure AD B2C 目錄</span><span class="sxs-lookup"><span data-stu-id="c05bc-112">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="c05bc-113">您必須先建立目錄或租用戶，才可使用 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="c05bc-113">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="c05bc-114">目錄就是您所有使用者、應用程式、群組等項目的容器。</span><span class="sxs-lookup"><span data-stu-id="c05bc-114">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="c05bc-115">如果您還沒有此資源，請先建立 B2C 目錄，再繼續進行本指南。</span><span class="sxs-lookup"><span data-stu-id="c05bc-115">If you don't have one already, create a B2C directory before you continue in this guide.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> <span data-ttu-id="c05bc-116">您需要 tooconnect hello B2C 租用戶 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c05bc-116">You need tooconnect hello B2C Tenant tooyour Azure subscription.</span></span> <span data-ttu-id="c05bc-117">選取之後**建立**，選取 hello**連結現有的 Azure AD B2C 租用戶 toomy Azure 訂用帳戶**選項，然後在 hello **Azure AD B2C 租用戶**下拉式清單中，選取您想要 tooassociate hello 租用戶。</span><span class="sxs-lookup"><span data-stu-id="c05bc-117">After selecting **Create**, select hello **Link an existing Azure AD B2C Tenant toomy Azure subscription** option, and then in hello **Azure AD B2C Tenant** drop down, select hello tenant you want tooassociate.</span></span>

## <a name="create-and-register-an-application"></a><span data-ttu-id="c05bc-118">建立並註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="c05bc-118">Create and register an application</span></span>

<span data-ttu-id="c05bc-119">接下來，您需要 toocreate 和 B2C 目錄中註冊 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c05bc-119">Next, you need toocreate and register hello app in your B2C directory.</span></span> <span data-ttu-id="c05bc-120">這會提供 Azure AD B2C 需要 toosecurely 資訊與您的應用程式通訊。</span><span class="sxs-lookup"><span data-stu-id="c05bc-120">This provides information that Azure AD B2C needs toosecurely communicate with your app.</span></span> 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

<span data-ttu-id="c05bc-121">完成後，您的應用程式設定中會有 API 與原生應用程式。</span><span class="sxs-lookup"><span data-stu-id="c05bc-121">When you are done, you will have both an API and a native application in your application settings.</span></span>

## <a name="create-policies-on-your-b2c-tenant"></a><span data-ttu-id="c05bc-122">在 B2C 租用戶上建立原則</span><span class="sxs-lookup"><span data-stu-id="c05bc-122">Create policies on your B2C tenant</span></span>

<span data-ttu-id="c05bc-123">在 Azure AD B2C 中，每個使用者體驗皆是由某個 [原則](active-directory-b2c-reference-policies.md)所定義。</span><span class="sxs-lookup"><span data-stu-id="c05bc-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="c05bc-124">此程式碼範例包含三種身分識別體驗：**註冊和登入**、**設定檔編輯**和**密碼重設**。</span><span class="sxs-lookup"><span data-stu-id="c05bc-124">This code sample contains three identity experiences: **sign-up & sign-in**, **profile edit**, and **password reset**.</span></span>  <span data-ttu-id="c05bc-125">Hello 中所述，您會需要 toocreate 一個原則的每個類型，[原則參考文件](active-directory-b2c-reference-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="c05bc-125">You need toocreate one policy of each type, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="c05bc-126">每個原則，是原則的確定 tooselect hello 顯示名稱屬性或宣告，以及 toocopy 下 hello 中的名稱以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="c05bc-126">For each policy, be sure tooselect hello Display name attribute or claim, and toocopy down hello name of your policy for later use.</span></span>

### <a name="add-your-identity-providers"></a><span data-ttu-id="c05bc-127">新增識別提供者</span><span class="sxs-lookup"><span data-stu-id="c05bc-127">Add your identity providers</span></span>

<span data-ttu-id="c05bc-128">從您的設定中，選取 [識別提供者]，然後選擇 [使用者名稱註冊] 或 [電子郵件註冊]。</span><span class="sxs-lookup"><span data-stu-id="c05bc-128">From your settings, select **Identity Providers** and choose Username signup or Email signup.</span></span>

### <a name="create-a-sign-up-and-sign-in-policy"></a><span data-ttu-id="c05bc-129">建立註冊與登入原則</span><span class="sxs-lookup"><span data-stu-id="c05bc-129">Create a sign-up and sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a><span data-ttu-id="c05bc-130">建立設定檔編輯原則</span><span class="sxs-lookup"><span data-stu-id="c05bc-130">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a><span data-ttu-id="c05bc-131">建立密碼重設原則</span><span class="sxs-lookup"><span data-stu-id="c05bc-131">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

<span data-ttu-id="c05bc-132">建立您的原則之後，您便準備好 toobuild 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c05bc-132">After you create your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="c05bc-133">下載 hello 範例程式碼</span><span class="sxs-lookup"><span data-stu-id="c05bc-133">Download hello sample code</span></span>

<span data-ttu-id="c05bc-134">本教學課程中的 hello 程式碼維護在[GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi)。</span><span class="sxs-lookup"><span data-stu-id="c05bc-134">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="c05bc-135">您可以藉由執行複製 hello 範例：</span><span class="sxs-lookup"><span data-stu-id="c05bc-135">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="c05bc-136">下載 hello 範例程式碼之後，開啟 hello Visual Studio.sln 檔案 tooget 啟動。</span><span class="sxs-lookup"><span data-stu-id="c05bc-136">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="c05bc-137">hello 方案檔包含兩個專案：`TaskWebApp`和`TaskService`。</span><span class="sxs-lookup"><span data-stu-id="c05bc-137">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="c05bc-138">`TaskWebApp`是 hello hello 使用者的 MVC web 應用程式互動。</span><span class="sxs-lookup"><span data-stu-id="c05bc-138">`TaskWebApp` is hello MVC web application that hello user interacts with.</span></span> <span data-ttu-id="c05bc-139">`TaskService`是 hello 應用程式後端 web API，儲存每個使用者的待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="c05bc-139">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="c05bc-140">本文將只會討論 hello`TaskWebApp`應用程式。</span><span class="sxs-lookup"><span data-stu-id="c05bc-140">This article will only discuss hello `TaskWebApp` application.</span></span> <span data-ttu-id="c05bc-141">toolearn 如何 toobuild`TaskService`使用 Azure AD B2C，請參閱[我們.NET web api 教學課程](active-directory-b2c-devquickstarts-api-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="c05bc-141">toolearn how toobuild `TaskService` using Azure AD B2C, see [our .NET web api tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="update-code-toouse-your-tenant-and-policies"></a><span data-ttu-id="c05bc-142">更新程式碼 toouse 租用戶和原則</span><span class="sxs-lookup"><span data-stu-id="c05bc-142">Update code toouse your tenant and policies</span></span>

<span data-ttu-id="c05bc-143">我們的範例是設定的 toouse hello 原則和用戶端識別碼我們示範租用戶。</span><span class="sxs-lookup"><span data-stu-id="c05bc-143">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="c05bc-144">tooconnect 它 tooyour 自己的租用戶，您需要 tooopen`web.config`在 hello`TaskWebApp`專案，並取代 hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="c05bc-144">tooconnect it tooyour own tenant, you need tooopen `web.config` in hello `TaskWebApp` project and replace hello following values:</span></span>

* <span data-ttu-id="c05bc-145">`ida:Tenant`：使用您的租用戶名稱</span><span class="sxs-lookup"><span data-stu-id="c05bc-145">`ida:Tenant` with your tenant name</span></span>
* <span data-ttu-id="c05bc-146">`ida:ClientId`：使用您的 Web 應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="c05bc-146">`ida:ClientId` with your web app application ID</span></span>
* <span data-ttu-id="c05bc-147">`ida:ClientSecret`：使用您的 Web 應用程式祕密金鑰</span><span class="sxs-lookup"><span data-stu-id="c05bc-147">`ida:ClientSecret` with your web app secret key</span></span>
* <span data-ttu-id="c05bc-148">`ida:SignUpSignInPolicyId`：使用您的「註冊或登入」原則名稱</span><span class="sxs-lookup"><span data-stu-id="c05bc-148">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
* <span data-ttu-id="c05bc-149">`ida:EditProfilePolicyId`：使用您的「編輯設定檔」原則名稱</span><span class="sxs-lookup"><span data-stu-id="c05bc-149">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
* <span data-ttu-id="c05bc-150">`ida:ResetPasswordPolicyId`：使用您的「重設密碼」原則名稱</span><span class="sxs-lookup"><span data-stu-id="c05bc-150">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>

## <a name="launch-hello-app"></a><span data-ttu-id="c05bc-151">啟動 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="c05bc-151">Launch hello app</span></span>
<span data-ttu-id="c05bc-152">從 Visual Studio 內啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c05bc-152">From within Visual Studio, launch hello app.</span></span> <span data-ttu-id="c05bc-153">瀏覽 toohello 待辦事項清單] 索引標籤，然後注意 hello URl 是： https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*& client_id =*YourclientID*...</span><span class="sxs-lookup"><span data-stu-id="c05bc-153">Navigate toohello To-Do List tab, and note hello URl is: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*&client_id=*YourclientID*.....</span></span>

<span data-ttu-id="c05bc-154">註冊 hello 應用程式使用您的電子郵件地址或使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="c05bc-154">Sign up for hello app by using your email address or user name.</span></span> <span data-ttu-id="c05bc-155">登出，然後再次登入並編輯 hello 設定檔或 hello 密碼重設。</span><span class="sxs-lookup"><span data-stu-id="c05bc-155">Sign out, then sign in again and edit hello profile or reset hello password.</span></span> <span data-ttu-id="c05bc-156">請登出應用程式，再以不同的使用者身分登入，</span><span class="sxs-lookup"><span data-stu-id="c05bc-156">Sign out and sign in as a different user.</span></span> 

## <a name="add-social-idps"></a><span data-ttu-id="c05bc-157">新增社交 IDP</span><span class="sxs-lookup"><span data-stu-id="c05bc-157">Add social IDPs</span></span>

<span data-ttu-id="c05bc-158">目前，hello 應用程式支援使用只有使用者註冊和登入**本機帳戶**; B2C 目錄中儲存的帳戶，使用使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="c05bc-158">Currently, hello app supports only user sign-up and sign-in by using **local accounts**; accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="c05bc-159">藉由使用 Azure AD B2C，您可以新增對其他 **身分識別提供者** (IDP) 的支援，但不需變更任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="c05bc-159">By using Azure AD B2C, you can add support for other **identity providers** (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="c05bc-160">tooadd 社交 IDPs tooyour 應用程式中，遵循開始 hello 詳細這些文章中的指示。</span><span class="sxs-lookup"><span data-stu-id="c05bc-160">tooadd social IDPs tooyour app, begin by following hello detailed instructions in these articles.</span></span> <span data-ttu-id="c05bc-161">針對每個 IDP 想 toosupport，您必須在該系統 tooregister 應用程式，並取得用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="c05bc-161">For each IDP you want toosupport, you need tooregister an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="c05bc-162">將 Facebook 設定為 IDP</span><span class="sxs-lookup"><span data-stu-id="c05bc-162">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="c05bc-163">將 Google 設定為 IDP</span><span class="sxs-lookup"><span data-stu-id="c05bc-163">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="c05bc-164">將 Amazon 設定為 IDP</span><span class="sxs-lookup"><span data-stu-id="c05bc-164">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="c05bc-165">將 LinkedIn 設定為 IDP</span><span class="sxs-lookup"><span data-stu-id="c05bc-165">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="c05bc-166">您將加入之後 hello 身分識別提供者 tooyour B2C 目錄中，編輯每個有三個原則 tooinclude hello 新 IDPs，hello 中所述[原則參考文件](active-directory-b2c-reference-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="c05bc-166">After you add hello identity providers tooyour B2C directory, edit each of your three policies tooinclude hello new IDPs, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="c05bc-167">儲存您的原則之後，請再次執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c05bc-167">After you save your policies, run hello app again.</span></span>  <span data-ttu-id="c05bc-168">您應該會看到新 IDPs 加入為登入並註冊選項，在每個身分識別體驗中的 hello。</span><span class="sxs-lookup"><span data-stu-id="c05bc-168">You should see hello new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="c05bc-169">您可以試驗您的原則，並觀察 hello 範例應用程式上的效果。</span><span class="sxs-lookup"><span data-stu-id="c05bc-169">You can experiment with your policies and observe hello effect on your sample app.</span></span> <span data-ttu-id="c05bc-170">新增或移除 IDP、管理應用程式宣告，或變更註冊屬性。</span><span class="sxs-lookup"><span data-stu-id="c05bc-170">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="c05bc-171">試驗到您能夠了解原則、驗證要求和 OWIN 如何結合在一起為止。</span><span class="sxs-lookup"><span data-stu-id="c05bc-171">Experiment until you can see how policies, authentication requests, and OWIN tie together.</span></span>

## <a name="sample-code-walkthrough"></a><span data-ttu-id="c05bc-172">範例程式碼逐步解說</span><span class="sxs-lookup"><span data-stu-id="c05bc-172">Sample code walkthrough</span></span>
<span data-ttu-id="c05bc-173">下列各節的 hello 顯示 hello 範例應用程式程式碼的設定方式。</span><span class="sxs-lookup"><span data-stu-id="c05bc-173">hello following sections show you how hello sample application code is configured.</span></span> <span data-ttu-id="c05bc-174">您日後開發應用程式時，可以將此程式碼當作指引。</span><span class="sxs-lookup"><span data-stu-id="c05bc-174">You may use this as a guide in your future app development.</span></span>

### <a name="add-authentication-support"></a><span data-ttu-id="c05bc-175">新增驗證支援</span><span class="sxs-lookup"><span data-stu-id="c05bc-175">Add authentication support</span></span>

<span data-ttu-id="c05bc-176">您現在可以設定您的應用程式 toouse Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="c05bc-176">You can now configure your app toouse Azure AD B2C.</span></span> <span data-ttu-id="c05bc-177">您的應用程式會藉由傳送 OpenID Connect 驗證要求，來與 Azure AD B2C 通訊。</span><span class="sxs-lookup"><span data-stu-id="c05bc-177">Your app communicates with Azure AD B2C by sending OpenID Connect authentication requests.</span></span> <span data-ttu-id="c05bc-178">hello 要求聽寫 hello 使用者體驗您的應用程式想 tooexecute 藉由指定 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="c05bc-178">hello requests dictate hello user experience your app wants tooexecute by specifying hello policy.</span></span> <span data-ttu-id="c05bc-179">您可以使用 Microsoft 的 OWIN 程式庫 toosend 這些要求，執行原則、 管理使用者工作階段，等等。</span><span class="sxs-lookup"><span data-stu-id="c05bc-179">You can use Microsoft's OWIN library toosend these requests, execute policies, manage user sessions, and more.</span></span>

#### <a name="install-owin"></a><span data-ttu-id="c05bc-180">安裝 OWIN</span><span class="sxs-lookup"><span data-stu-id="c05bc-180">Install OWIN</span></span>

<span data-ttu-id="c05bc-181">toobegin，使用 Visual Studio Package Manager Console hello 新增 hello OWIN 中介軟體 NuGet 封裝 toohello 專案。</span><span class="sxs-lookup"><span data-stu-id="c05bc-181">toobegin, add hello OWIN middleware NuGet packages toohello project by using hello Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a><span data-ttu-id="c05bc-182">新增 OWIN 啟動類別</span><span class="sxs-lookup"><span data-stu-id="c05bc-182">Add an OWIN startup class</span></span>

<span data-ttu-id="c05bc-183">新增 OWIN 啟動類別 toohello API 呼叫`Startup.cs`。</span><span class="sxs-lookup"><span data-stu-id="c05bc-183">Add an OWIN startup class toohello API called `Startup.cs`.</span></span>  <span data-ttu-id="c05bc-184">以滑鼠右鍵按一下 hello 專案、 選取**新增**和**新項目**，然後搜尋 OWIN。</span><span class="sxs-lookup"><span data-stu-id="c05bc-184">Right-click on hello project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="c05bc-185">hello OWIN 中介軟體將會叫用 hello`Configuration(…)`方法，當您啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="c05bc-185">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="c05bc-186">在我們的範例中，我們變更 hello 類別宣告太`public partial class Startup`和實作 hello hello 類別中的其他部分`App_Start\Startup.Auth.cs`。</span><span class="sxs-lookup"><span data-stu-id="c05bc-186">In our sample, we changed hello class declaration too`public partial class Startup` and implemented hello other part of hello class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="c05bc-187">內部 hello`Configuration`方法中，我們加入呼叫太`ConfigureAuth`，定義在`Startup.Auth.cs`。</span><span class="sxs-lookup"><span data-stu-id="c05bc-187">Inside hello `Configuration` method, we added a call too`ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="c05bc-188">Hello 修改之後`Startup.cs`看起來像 hello 面：</span><span class="sxs-lookup"><span data-stu-id="c05bc-188">After hello modifications, `Startup.cs` looks like hello following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-hello-authentication-middleware"></a><span data-ttu-id="c05bc-189">設定 hello 驗證中介軟體</span><span class="sxs-lookup"><span data-stu-id="c05bc-189">Configure hello authentication middleware</span></span>

<span data-ttu-id="c05bc-190">開啟 hello 檔案`App_Start\Startup.Auth.cs`並實作 hello`ConfigureAuth(...)`方法。</span><span class="sxs-lookup"><span data-stu-id="c05bc-190">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="c05bc-191">hello 的參數中提供`OpenIdConnectAuthenticationOptions`做為您的應用程式 toocommunicate 與 Azure AD B2C 的座標。</span><span class="sxs-lookup"><span data-stu-id="c05bc-191">hello parameters you provide in `OpenIdConnectAuthenticationOptions` serve as coordinates for your app toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="c05bc-192">如果您未指定特定參數，它會使用 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="c05bc-192">If you do not specify certain parameters, it will use hello default value.</span></span> <span data-ttu-id="c05bc-193">例如，我們不指定 hello`ResponseType`在 hello 範例中，因此 hello 預設值`code id_token`將用於每個外寄要求 tooAzure AD B2C 中。</span><span class="sxs-lookup"><span data-stu-id="c05bc-193">For example, we do not specify hello `ResponseType` in hello sample, so hello default value `code id_token` will be used in each outgoing request tooAzure AD B2C.</span></span>

<span data-ttu-id="c05bc-194">您也需要設定的 cookie 驗證 tooset。</span><span class="sxs-lookup"><span data-stu-id="c05bc-194">You also need tooset up cookie authentication.</span></span> <span data-ttu-id="c05bc-195">hello OpenID Connect 中介軟體會使用 cookie toomaintain 使用者工作階段，以及其他項目。</span><span class="sxs-lookup"><span data-stu-id="c05bc-195">hello OpenID Connect middleware uses cookies toomaintain user sessions, among other things.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure hello OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate hello metadata address using hello tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify hello callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify hello claims toovalidate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement hello "Notification" methods...
}
```

<span data-ttu-id="c05bc-196">在`OpenIdConnectAuthenticationOptions`以上版本，我們會定義一組特定 hello OpenID Connect 中介軟體所收到的通知的回呼函式。</span><span class="sxs-lookup"><span data-stu-id="c05bc-196">In `OpenIdConnectAuthenticationOptions` above, we define a set of callback functions for specific notifications that are received by hello OpenID Connect middleware.</span></span> <span data-ttu-id="c05bc-197">這些行為透過定義`OpenIdConnectAuthenticationNotifications`物件，並儲存到 hello`Notifications`變數。</span><span class="sxs-lookup"><span data-stu-id="c05bc-197">These behaviors are defined using a `OpenIdConnectAuthenticationNotifications` object and stored into hello `Notifications` variable.</span></span> <span data-ttu-id="c05bc-198">在我們的範例中，我們會定義三個不同的回呼，視 hello 事件而定。</span><span class="sxs-lookup"><span data-stu-id="c05bc-198">In our sample, we define three different callbacks depending on hello event.</span></span>

### <a name="using-different-policies"></a><span data-ttu-id="c05bc-199">使用不同的原則</span><span class="sxs-lookup"><span data-stu-id="c05bc-199">Using different policies</span></span>

<span data-ttu-id="c05bc-200">hello`RedirectToIdentityProvider`通知時會觸發 tooAzure AD B2C 提出要求。</span><span class="sxs-lookup"><span data-stu-id="c05bc-200">hello `RedirectToIdentityProvider` notification is triggered whenever a request is made tooAzure AD B2C.</span></span> <span data-ttu-id="c05bc-201">在 [hello 回呼函式`OnRedirectToIdentityProvider`，我們會檢查在傳出呼叫，如果我們想要 toouse hello 不同的原則。</span><span class="sxs-lookup"><span data-stu-id="c05bc-201">In hello callback function `OnRedirectToIdentityProvider`, we check in hello outgoing call if we want toouse a different policy.</span></span> <span data-ttu-id="c05bc-202">在密碼重設或編輯設定檔的順序 toodo，您需要 toouse hello 對應原則，例如 hello 密碼重設原則，而不是 hello 預設 「 註冊或登入 」 原則。</span><span class="sxs-lookup"><span data-stu-id="c05bc-202">In order toodo a password reset or edit a profile, you need toouse hello corresponding policy such as hello password reset policy instead of hello default "Sign-up or Sign-in" policy.</span></span>

<span data-ttu-id="c05bc-203">在我們的範例中，當使用者想 tooreset hello 密碼，或編輯 hello 設定檔，我們會加入 hello 原則我們偏好 toouse 到 hello OWIN 內容。</span><span class="sxs-lookup"><span data-stu-id="c05bc-203">In our sample, when a user wants tooreset hello password or edit hello profile, we add hello policy we prefer toouse into hello OWIN context.</span></span> <span data-ttu-id="c05bc-204">您可以藉由 hello 下列來完成：</span><span class="sxs-lookup"><span data-stu-id="c05bc-204">That can be done by doing hello following:</span></span>

```CSharp
    // Let hello middleware know you are trying toouse hello edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

<span data-ttu-id="c05bc-205">您可以實作 hello 回呼函式和`OnRedirectToIdentityProvider`執行 hello 下列動作：</span><span class="sxs-lookup"><span data-stu-id="c05bc-205">And you can implement hello callback function `OnRedirectToIdentityProvider` by doing hello following:</span></span>

```CSharp
/*
*  On each call tooAzure AD B2C, check if a policy (e.g. hello profile edit or password reset policy) has been specified in hello OWIN context.
*  If so, use that policy when making hello call. Also, don't request a code (since it won't be needed).
*/
private Task OnRedirectToIdentityProvider(RedirectToIdentityProviderNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    var policy = notification.OwinContext.Get<string>("Policy");

    if (!string.IsNullOrEmpty(policy) && !policy.Equals(DefaultPolicy))
    {
        notification.ProtocolMessage.Scope = OpenIdConnectScopes.OpenId;
        notification.ProtocolMessage.ResponseType = OpenIdConnectResponseTypes.IdToken;
        notification.ProtocolMessage.IssuerAddress = notification.ProtocolMessage.IssuerAddress.Replace(DefaultPolicy, policy);
    }

    return Task.FromResult(0);
}
```

### <a name="handling-authorization-codes"></a><span data-ttu-id="c05bc-206">處理授權碼</span><span class="sxs-lookup"><span data-stu-id="c05bc-206">Handling authorization codes</span></span>

<span data-ttu-id="c05bc-207">hello`AuthorizationCodeReceived`通知收到授權碼時觸發。</span><span class="sxs-lookup"><span data-stu-id="c05bc-207">hello `AuthorizationCodeReceived` notification is triggered when an authorization code is received.</span></span> <span data-ttu-id="c05bc-208">hello OpenID Connect 中介軟體不支援交換代碼的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="c05bc-208">hello OpenID Connect middleware does not support exchanging codes for access tokens.</span></span> <span data-ttu-id="c05bc-209">您可以手動交換 hello hello 語彙基元中的回呼函式的程式碼。</span><span class="sxs-lookup"><span data-stu-id="c05bc-209">You can manually exchange hello code for hello token in a callback function.</span></span> <span data-ttu-id="c05bc-210">如需詳細資訊，請查看 hello[文件](active-directory-b2c-devquickstarts-web-api-dotnet.md)，說明如何。</span><span class="sxs-lookup"><span data-stu-id="c05bc-210">For more information, please look at hello [documentation](active-directory-b2c-devquickstarts-web-api-dotnet.md) that explains how.</span></span>

### <a name="handling-errors"></a><span data-ttu-id="c05bc-211">處理錯誤</span><span class="sxs-lookup"><span data-stu-id="c05bc-211">Handling errors</span></span>

<span data-ttu-id="c05bc-212">hello`AuthenticationFailed`驗證失敗時，會觸發通知。</span><span class="sxs-lookup"><span data-stu-id="c05bc-212">hello `AuthenticationFailed` notification is triggered when authentication fails.</span></span> <span data-ttu-id="c05bc-213">回呼方法時，您可以處理 hello 錯誤，在您希望的位置。</span><span class="sxs-lookup"><span data-stu-id="c05bc-213">In its callback method, you can handle hello errors as you wish.</span></span> <span data-ttu-id="c05bc-214">不過，您應該加入 hello 錯誤碼檢查`AADB2C90118`。</span><span class="sxs-lookup"><span data-stu-id="c05bc-214">You should however add a check for hello error code `AADB2C90118`.</span></span> <span data-ttu-id="c05bc-215">Hello hello 「 註冊或登入 」 的原則執行期間 hello 使用者擁有 hello 機會 tooselect**忘記密碼？**連結。</span><span class="sxs-lookup"><span data-stu-id="c05bc-215">During hello execution of hello "Sign-up or Sign-in" policy, hello user has hello opportunity tooselect a **Forgot your password?** link.</span></span> <span data-ttu-id="c05bc-216">在此情況下，Azure AD B2C 傳送您的應用程式的錯誤代碼，表示您的應用程式應該要改用 hello 密碼重設原則的要求。</span><span class="sxs-lookup"><span data-stu-id="c05bc-216">In this event, Azure AD B2C sends your app that error code indicating that your app should make a request using hello password reset policy instead.</span></span>

```CSharp
/*
* Catch any failures received by hello authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle hello error code that Azure AD B2C throws when trying tooreset a password from hello login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If hello user clicked hello reset password link, redirect toohello reset password route
        notification.Response.Redirect("/Account/ResetPassword");
    }
    else if (notification.Exception.Message == "access_denied")
    {
        notification.Response.Redirect("/");
    }
    else
    {
        notification.Response.Redirect("/Home/Error?message=" + notification.Exception.Message);
    }

    return Task.FromResult(0);
}
```

### <a name="send-authentication-requests-tooazure-ad"></a><span data-ttu-id="c05bc-217">傳送驗證要求 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="c05bc-217">Send authentication requests tooAzure AD</span></span>

<span data-ttu-id="c05bc-218">您的應用程式是現在已正確設定與 Azure AD B2C toocommunicate 使用 hello OpenID Connect 的驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="c05bc-218">Your app is now properly configured toocommunicate with Azure AD B2C by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="c05bc-219">OWIN 管理 hello 製作驗證訊息，驗證來自 Azure AD B2C，語彙基元和維護使用者工作階段的詳細的資料。</span><span class="sxs-lookup"><span data-stu-id="c05bc-219">OWIN manages hello details of crafting authentication messages, validating tokens from Azure AD B2C, and maintaining user session.</span></span> <span data-ttu-id="c05bc-220">所有仍然是 tooinitiate 每位使用者的流量。</span><span class="sxs-lookup"><span data-stu-id="c05bc-220">All that remains is tooinitiate each user's flow.</span></span>

<span data-ttu-id="c05bc-221">當使用者選取**登向上/登入**，**編輯設定檔**，或**重設密碼**hello web 應用程式，在相關聯的 hello 叫用動作中`Controllers\AccountController.cs`:</span><span class="sxs-lookup"><span data-stu-id="c05bc-221">When a user selects **Sign up/Sign in**, **Edit profile**, or **Reset password** in hello web app, hello associated action is invoked in `Controllers\AccountController.cs`:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign up or sign in
*/
public void SignUpSignIn()
{
    // Use hello default policy tooprocess hello sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting tooedit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let hello middleware know you are trying toouse hello edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set hello page tooredirect tooafter editing hello profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting tooreset a password
*/
public void ResetPassword()
{
    // Let hello middleware know you are trying toouse hello reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set hello page tooredirect tooafter changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

<span data-ttu-id="c05bc-222">您也可以使用 OWIN toosign 出 hello 從 hello 應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="c05bc-222">You can also use OWIN toosign out hello user from hello app.</span></span> <span data-ttu-id="c05bc-223">在 `Controllers\AccountController.cs` 中，我們有︰</span><span class="sxs-lookup"><span data-stu-id="c05bc-223">In `Controllers\AccountController.cs` we have:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign out
*/
public void SignOut()
{
    // toosign out hello user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

<span data-ttu-id="c05bc-224">在加法 tooexplicitly 叫用原則，您可以使用`[Authorize]`標記中的控制站執行原則，如果 hello 使用者未登入。</span><span class="sxs-lookup"><span data-stu-id="c05bc-224">In addition tooexplicitly invoking a policy, you can use a `[Authorize]` tag in your controllers that executes a policy if hello user is not signed in.</span></span> <span data-ttu-id="c05bc-225">開啟`Controllers\HomeController.cs`和新增 hello`[Authorize]`標記 toohello 宣告控制站。</span><span class="sxs-lookup"><span data-stu-id="c05bc-225">Open `Controllers\HomeController.cs` and add hello `[Authorize]` tag toohello claims controller.</span></span>  <span data-ttu-id="c05bc-226">OWIN 選取 hello 上次原則設定時 hello`[Authorize]`叫用標記。</span><span class="sxs-lookup"><span data-stu-id="c05bc-226">OWIN selects hello last policy configured when hello `[Authorize]` tag is hit.</span></span>

```CSharp
// Controllers\HomeController.cs

// You can use hello Authorize decorator tooexecute a certain policy if hello user is not already signed into hello app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a><span data-ttu-id="c05bc-227">顯示使用者資訊</span><span class="sxs-lookup"><span data-stu-id="c05bc-227">Display user information</span></span>

<span data-ttu-id="c05bc-228">當您使用 OpenID Connect 來驗證使用者時，Azure AD B2C 傳回識別碼權杖 toohello 應用程式，其中包含**宣告**。</span><span class="sxs-lookup"><span data-stu-id="c05bc-228">When you authenticate users by using OpenID Connect, Azure AD B2C returns an ID token toohello app that contains **claims**.</span></span> <span data-ttu-id="c05bc-229">這些是 hello 使用者判斷提示。</span><span class="sxs-lookup"><span data-stu-id="c05bc-229">These are assertions about hello user.</span></span> <span data-ttu-id="c05bc-230">您可以使用宣告 toopersonalize 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c05bc-230">You can use claims toopersonalize your app.</span></span>

<span data-ttu-id="c05bc-231">開啟 hello`Controllers\HomeController.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="c05bc-231">Open hello `Controllers\HomeController.cs` file.</span></span> <span data-ttu-id="c05bc-232">您可以在 hello 透過您控制站存取使用者宣告`ClaimsPrincipal.Current`安全性主體物件。</span><span class="sxs-lookup"><span data-stu-id="c05bc-232">You can access user claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

```CSharp
// Controllers\HomeController.cs

[Authorize]
public ActionResult Claims()
{
    Claim displayName = ClaimsPrincipal.Current.FindFirst(ClaimsPrincipal.Current.Identities.First().NameClaimType);
    ViewBag.DisplayName = displayName != null ? displayName.Value : string.Empty;
    return View();
}
```

<span data-ttu-id="c05bc-233">您可以存取任何宣告，您的應用程式收到 hello 中相同的方式。</span><span class="sxs-lookup"><span data-stu-id="c05bc-233">You can access any claim that your application receives in hello same way.</span></span>  <span data-ttu-id="c05bc-234">收到 hello 應用程式的所有 hello 宣告的清單是可供您在 hello**宣告**頁面。</span><span class="sxs-lookup"><span data-stu-id="c05bc-234">A list of all hello claims hello app receives is available for you on hello **Claims** page.</span></span>
