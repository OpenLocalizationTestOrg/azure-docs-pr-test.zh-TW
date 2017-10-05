---
title: Azure Active Directory B2C | Microsoft Docs
description: "如何使用 Azure Active Directory B2C 建置支援註冊/登入、設定檔編輯及密碼重設的 Web 應用程式。"
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
ms.openlocfilehash: 3144ced01b524abb035dc1c6f0cdf764bec46804
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a><span data-ttu-id="2b87b-103">建立支援 Azure Active Directory B2C 註冊、登入、設定檔編輯及密碼重設的 ASP.NET Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="2b87b-103">Create an ASP.NET web app with Azure Active Directory B2C sign-up, sign-in, profile edit, and password reset</span></span>

<span data-ttu-id="2b87b-104">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="2b87b-104">This tutorial shows you how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2b87b-105">將 Azure AD B2C 身分識別功能新增至您的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="2b87b-105">Add Azure AD B2C identity features to your web app</span></span>
> * <span data-ttu-id="2b87b-106">在您的 Azure AD B2C 目錄中註冊 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="2b87b-106">Register your web app in your Azure AD B2C directory</span></span>
> * <span data-ttu-id="2b87b-107">為您的 Web 應用程式建立使用者註冊/登入、編輯設定檔和密碼重設原則</span><span class="sxs-lookup"><span data-stu-id="2b87b-107">Create a user sign-up/sign-in, profile edit, and password reset policy for your web app</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b87b-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="2b87b-108">Prerequisites</span></span>

- <span data-ttu-id="2b87b-109">您必須將 B2C 租用戶與 Azure 帳戶連接。</span><span class="sxs-lookup"><span data-stu-id="2b87b-109">You must connect your B2C Tenant to an Azure account.</span></span> <span data-ttu-id="2b87b-110">您可以在[這裡](https://azure.microsoft.com/en-us/)建立免費的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b87b-110">You can create a free Azure account [here](https://azure.microsoft.com/en-us/).</span></span>
- <span data-ttu-id="2b87b-111">您需要 [Microsoft Visual Studio](https://www.visualstudio.com/) 或類似的程式來檢視與修改範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="2b87b-111">You need [Microsoft Visual Studio](https://www.visualstudio.com/) or a similar program to view and modify the sample code.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="2b87b-112">建立 Azure AD B2C 目錄</span><span class="sxs-lookup"><span data-stu-id="2b87b-112">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="2b87b-113">您必須先建立目錄或租用戶，才可使用 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="2b87b-113">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="2b87b-114">目錄就是您所有使用者、應用程式、群組等項目的容器。</span><span class="sxs-lookup"><span data-stu-id="2b87b-114">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="2b87b-115">如果您還沒有此資源，請先建立 B2C 目錄，再繼續進行本指南。</span><span class="sxs-lookup"><span data-stu-id="2b87b-115">If you don't have one already, create a B2C directory before you continue in this guide.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> <span data-ttu-id="2b87b-116">您必須將 B2C 租用戶與您的 Azure 訂用帳戶連接。</span><span class="sxs-lookup"><span data-stu-id="2b87b-116">You need to connect the B2C Tenant to your Azure subscription.</span></span> <span data-ttu-id="2b87b-117">選取 [建立] 後，請選取 [連結現有 Azure AD B2C 租用戶至我的 Azure 訂用帳戶] 選項，然後在 [Azure AD B2C 租用戶] 下拉式清單中選取想要連接的租用戶。</span><span class="sxs-lookup"><span data-stu-id="2b87b-117">After selecting **Create**, select the **Link an existing Azure AD B2C Tenant to my Azure subscription** option, and then in the **Azure AD B2C Tenant** drop down, select the tenant you want to associate.</span></span>

## <a name="create-and-register-an-application"></a><span data-ttu-id="2b87b-118">建立並註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="2b87b-118">Create and register an application</span></span>

<span data-ttu-id="2b87b-119">接下來需在 B2C 目錄中建立並註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b87b-119">Next, you need to create and register the app in your B2C directory.</span></span> <span data-ttu-id="2b87b-120">這會提供必要資訊給 Azure AD B2C，讓它與應用程式安全地通訊。</span><span class="sxs-lookup"><span data-stu-id="2b87b-120">This provides information that Azure AD B2C needs to securely communicate with your app.</span></span> 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

<span data-ttu-id="2b87b-121">完成後，您的應用程式設定中會有 API 與原生應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b87b-121">When you are done, you will have both an API and a native application in your application settings.</span></span>

## <a name="create-policies-on-your-b2c-tenant"></a><span data-ttu-id="2b87b-122">在 B2C 租用戶上建立原則</span><span class="sxs-lookup"><span data-stu-id="2b87b-122">Create policies on your B2C tenant</span></span>

<span data-ttu-id="2b87b-123">在 Azure AD B2C 中，每個使用者體驗皆是由某個 [原則](active-directory-b2c-reference-policies.md)所定義。</span><span class="sxs-lookup"><span data-stu-id="2b87b-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="2b87b-124">此程式碼範例包含三種身分識別體驗：**註冊和登入**、**設定檔編輯**和**密碼重設**。</span><span class="sxs-lookup"><span data-stu-id="2b87b-124">This code sample contains three identity experiences: **sign-up & sign-in**, **profile edit**, and **password reset**.</span></span>  <span data-ttu-id="2b87b-125">您必須為每個類型建立一個原則，如 [原則參考文章](active-directory-b2c-reference-policies.md)所述。</span><span class="sxs-lookup"><span data-stu-id="2b87b-125">You need to create one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="2b87b-126">針對每個原則，請務必選取 [顯示名稱] 屬性或宣告，並複製原則名稱以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="2b87b-126">For each policy, be sure to select the Display name attribute or claim, and to copy down the name of your policy for later use.</span></span>

### <a name="add-your-identity-providers"></a><span data-ttu-id="2b87b-127">新增識別提供者</span><span class="sxs-lookup"><span data-stu-id="2b87b-127">Add your identity providers</span></span>

<span data-ttu-id="2b87b-128">從您的設定中，選取 [識別提供者]，然後選擇 [使用者名稱註冊] 或 [電子郵件註冊]。</span><span class="sxs-lookup"><span data-stu-id="2b87b-128">From your settings, select **Identity Providers** and choose Username signup or Email signup.</span></span>

### <a name="create-a-sign-up-and-sign-in-policy"></a><span data-ttu-id="2b87b-129">建立註冊與登入原則</span><span class="sxs-lookup"><span data-stu-id="2b87b-129">Create a sign-up and sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a><span data-ttu-id="2b87b-130">建立設定檔編輯原則</span><span class="sxs-lookup"><span data-stu-id="2b87b-130">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a><span data-ttu-id="2b87b-131">建立密碼重設原則</span><span class="sxs-lookup"><span data-stu-id="2b87b-131">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

<span data-ttu-id="2b87b-132">建立您的原則後，就可以開始建置您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b87b-132">After you create your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="2b87b-133">下載範例程式碼</span><span class="sxs-lookup"><span data-stu-id="2b87b-133">Download the sample code</span></span>

<span data-ttu-id="2b87b-134">本教學課程的程式碼保留在 [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi) 上。</span><span class="sxs-lookup"><span data-stu-id="2b87b-134">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="2b87b-135">您可以藉由執行下列作業來複製範例︰</span><span class="sxs-lookup"><span data-stu-id="2b87b-135">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="2b87b-136">下載範例程式碼後，請開啟 Visual Studio .sln 檔案開始進行。</span><span class="sxs-lookup"><span data-stu-id="2b87b-136">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="2b87b-137">您的方案現在包含兩個專案：`TaskWebApp``TaskService`。</span><span class="sxs-lookup"><span data-stu-id="2b87b-137">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="2b87b-138">`TaskWebApp` 是使用者所互動的 MVC Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b87b-138">`TaskWebApp` is the MVC web application that the user interacts with.</span></span> <span data-ttu-id="2b87b-139">`TaskService` 是應用程式的後端 Web API，其會儲存每位使用者的待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="2b87b-139">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="2b87b-140">本文只會討論 `TaskWebApp` 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b87b-140">This article will only discuss the `TaskWebApp` application.</span></span> <span data-ttu-id="2b87b-141">若要了解如何使用 Azure AD B2C 建置 `TaskService`，請參閱 [.NET Web API 教學課程](active-directory-b2c-devquickstarts-api-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="2b87b-141">To learn how to build `TaskService` using Azure AD B2C, see [our .NET web api tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="update-code-to-use-your-tenant-and-policies"></a><span data-ttu-id="2b87b-142">更新程式碼以使用您的租用戶與原則</span><span class="sxs-lookup"><span data-stu-id="2b87b-142">Update code to use your tenant and policies</span></span>

<span data-ttu-id="2b87b-143">我們的範例已設定成使用示範租用戶的原則和用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="2b87b-143">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="2b87b-144">若要將它與您自己的租用戶連接，您必須在 `TaskWebApp` 專案中開啟 `web.config`，然後取代以下的值：</span><span class="sxs-lookup"><span data-stu-id="2b87b-144">To connect it to your own tenant, you need to open `web.config` in the `TaskWebApp` project and replace the following values:</span></span>

* <span data-ttu-id="2b87b-145">`ida:Tenant`：使用您的租用戶名稱</span><span class="sxs-lookup"><span data-stu-id="2b87b-145">`ida:Tenant` with your tenant name</span></span>
* <span data-ttu-id="2b87b-146">`ida:ClientId`：使用您的 Web 應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="2b87b-146">`ida:ClientId` with your web app application ID</span></span>
* <span data-ttu-id="2b87b-147">`ida:ClientSecret`：使用您的 Web 應用程式祕密金鑰</span><span class="sxs-lookup"><span data-stu-id="2b87b-147">`ida:ClientSecret` with your web app secret key</span></span>
* <span data-ttu-id="2b87b-148">`ida:SignUpSignInPolicyId`：使用您的「註冊或登入」原則名稱</span><span class="sxs-lookup"><span data-stu-id="2b87b-148">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
* <span data-ttu-id="2b87b-149">`ida:EditProfilePolicyId`：使用您的「編輯設定檔」原則名稱</span><span class="sxs-lookup"><span data-stu-id="2b87b-149">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
* <span data-ttu-id="2b87b-150">`ida:ResetPasswordPolicyId`：使用您的「重設密碼」原則名稱</span><span class="sxs-lookup"><span data-stu-id="2b87b-150">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>

## <a name="launch-the-app"></a><span data-ttu-id="2b87b-151">啟動應用程式</span><span class="sxs-lookup"><span data-stu-id="2b87b-151">Launch the app</span></span>
<span data-ttu-id="2b87b-152">在 Visual Studio 內啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b87b-152">From within Visual Studio, launch the app.</span></span> <span data-ttu-id="2b87b-153">瀏覽至 [待辦事項清單] 索引標籤，並記下 URl 為：https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*&client_id=*YourclientID*.....</span><span class="sxs-lookup"><span data-stu-id="2b87b-153">Navigate to the To-Do List tab, and note the URl is: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*&client_id=*YourclientID*.....</span></span>

<span data-ttu-id="2b87b-154">使用電子郵件地址或使用者名稱來註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b87b-154">Sign up for the app by using your email address or user name.</span></span> <span data-ttu-id="2b87b-155">登出後再次登入，然後編輯設定檔或重設密碼。</span><span class="sxs-lookup"><span data-stu-id="2b87b-155">Sign out, then sign in again and edit the profile or reset the password.</span></span> <span data-ttu-id="2b87b-156">請登出應用程式，再以不同的使用者身分登入，</span><span class="sxs-lookup"><span data-stu-id="2b87b-156">Sign out and sign in as a different user.</span></span> 

## <a name="add-social-idps"></a><span data-ttu-id="2b87b-157">新增社交 IDP</span><span class="sxs-lookup"><span data-stu-id="2b87b-157">Add social IDPs</span></span>

<span data-ttu-id="2b87b-158">目前，應用程式僅支援使用**本機帳戶**的使用者註冊與登入；本機帳戶是指儲存在您 B2C 目錄中使用使用者名稱與密碼的帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b87b-158">Currently, the app supports only user sign-up and sign-in by using **local accounts**; accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="2b87b-159">藉由使用 Azure AD B2C，您可以新增對其他 **身分識別提供者** (IDP) 的支援，但不需變更任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="2b87b-159">By using Azure AD B2C, you can add support for other **identity providers** (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="2b87b-160">若要將社交 IDP 加入至應用程式，請依照下列文章中的詳細指示開始。</span><span class="sxs-lookup"><span data-stu-id="2b87b-160">To add social IDPs to your app, begin by following the detailed instructions in these articles.</span></span> <span data-ttu-id="2b87b-161">針對您想要支援的每個 IDP，您必須在該系統中註冊應用程式並取得用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="2b87b-161">For each IDP you want to support, you need to register an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="2b87b-162">將 Facebook 設定為 IDP</span><span class="sxs-lookup"><span data-stu-id="2b87b-162">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="2b87b-163">將 Google 設定為 IDP</span><span class="sxs-lookup"><span data-stu-id="2b87b-163">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="2b87b-164">將 Amazon 設定為 IDP</span><span class="sxs-lookup"><span data-stu-id="2b87b-164">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="2b87b-165">將 LinkedIn 設定為 IDP</span><span class="sxs-lookup"><span data-stu-id="2b87b-165">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="2b87b-166">當您將識別提供者新增到 B2C 目錄之後，請一一編輯您的三個原則以包含新的 IDP，如[原則參考文章](active-directory-b2c-reference-policies.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="2b87b-166">After you add the identity providers to your B2C directory, edit each of your three policies to include the new IDPs, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="2b87b-167">儲存您的原則之後，重新執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b87b-167">After you save your policies, run the app again.</span></span>  <span data-ttu-id="2b87b-168">在每一次的身分識別體驗中，您應該會看到新的 IDP 已加入成為登入和註冊選項。</span><span class="sxs-lookup"><span data-stu-id="2b87b-168">You should see the new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="2b87b-169">您可以在範例應用程式上試驗原則並觀察其效果。</span><span class="sxs-lookup"><span data-stu-id="2b87b-169">You can experiment with your policies and observe the effect on your sample app.</span></span> <span data-ttu-id="2b87b-170">新增或移除 IDP、管理應用程式宣告，或變更註冊屬性。</span><span class="sxs-lookup"><span data-stu-id="2b87b-170">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="2b87b-171">試驗到您能夠了解原則、驗證要求和 OWIN 如何結合在一起為止。</span><span class="sxs-lookup"><span data-stu-id="2b87b-171">Experiment until you can see how policies, authentication requests, and OWIN tie together.</span></span>

## <a name="sample-code-walkthrough"></a><span data-ttu-id="2b87b-172">範例程式碼逐步解說</span><span class="sxs-lookup"><span data-stu-id="2b87b-172">Sample code walkthrough</span></span>
<span data-ttu-id="2b87b-173">以下各節說明如何設定範例應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="2b87b-173">The following sections show you how the sample application code is configured.</span></span> <span data-ttu-id="2b87b-174">您日後開發應用程式時，可以將此程式碼當作指引。</span><span class="sxs-lookup"><span data-stu-id="2b87b-174">You may use this as a guide in your future app development.</span></span>

### <a name="add-authentication-support"></a><span data-ttu-id="2b87b-175">新增驗證支援</span><span class="sxs-lookup"><span data-stu-id="2b87b-175">Add authentication support</span></span>

<span data-ttu-id="2b87b-176">您現在可以設定您的應用程式以使用 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="2b87b-176">You can now configure your app to use Azure AD B2C.</span></span> <span data-ttu-id="2b87b-177">您的應用程式會藉由傳送 OpenID Connect 驗證要求，來與 Azure AD B2C 通訊。</span><span class="sxs-lookup"><span data-stu-id="2b87b-177">Your app communicates with Azure AD B2C by sending OpenID Connect authentication requests.</span></span> <span data-ttu-id="2b87b-178">要求會藉由指定原則來決定您的應用程式想要執行的使用者經驗。</span><span class="sxs-lookup"><span data-stu-id="2b87b-178">The requests dictate the user experience your app wants to execute by specifying the policy.</span></span> <span data-ttu-id="2b87b-179">您可以使用 Microsoft 的 OWIN 程式庫來傳送這些要求、執行原則、管理使用者工作階段等等。</span><span class="sxs-lookup"><span data-stu-id="2b87b-179">You can use Microsoft's OWIN library to send these requests, execute policies, manage user sessions, and more.</span></span>

#### <a name="install-owin"></a><span data-ttu-id="2b87b-180">安裝 OWIN</span><span class="sxs-lookup"><span data-stu-id="2b87b-180">Install OWIN</span></span>

<span data-ttu-id="2b87b-181">首先，請使用 Visual Studio Package Manager Console，將 OWIN 中介軟體 NuGet 封裝加入至專案。</span><span class="sxs-lookup"><span data-stu-id="2b87b-181">To begin, add the OWIN middleware NuGet packages to the project by using the Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a><span data-ttu-id="2b87b-182">新增 OWIN 啟動類別</span><span class="sxs-lookup"><span data-stu-id="2b87b-182">Add an OWIN startup class</span></span>

<span data-ttu-id="2b87b-183">將 OWIN 啟動類別新增至名為 `Startup.cs` 的 API。</span><span class="sxs-lookup"><span data-stu-id="2b87b-183">Add an OWIN startup class to the API called `Startup.cs`.</span></span>  <span data-ttu-id="2b87b-184">以滑鼠右鍵按一下專案，依序選取 [新增] 和 [新增項目]，然後搜尋 OWIN。</span><span class="sxs-lookup"><span data-stu-id="2b87b-184">Right-click on the project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="2b87b-185">OWIN 中介軟體將會在應用程式啟動時叫用 `Configuration(…)` 方法。</span><span class="sxs-lookup"><span data-stu-id="2b87b-185">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="2b87b-186">在我們的範例中，我們將類別宣告變更為 `public partial class Startup` 並且在 `App_Start\Startup.Auth.cs` 中實作類別的其他部分。</span><span class="sxs-lookup"><span data-stu-id="2b87b-186">In our sample, we changed the class declaration to `public partial class Startup` and implemented the other part of the class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="2b87b-187">在 `Configuration` 方法中，我們將呼叫新增至 `ConfigureAuth`(其定義於 `Startup.Auth.cs`)。</span><span class="sxs-lookup"><span data-stu-id="2b87b-187">Inside the `Configuration` method, we added a call to `ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="2b87b-188">修改之後，`Startup.cs` 如下所示︰</span><span class="sxs-lookup"><span data-stu-id="2b87b-188">After the modifications, `Startup.cs` looks like the following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // The OWIN middleware will invoke this method when the app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of the class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-the-authentication-middleware"></a><span data-ttu-id="2b87b-189">設定驗證中介軟體</span><span class="sxs-lookup"><span data-stu-id="2b87b-189">Configure the authentication middleware</span></span>

<span data-ttu-id="2b87b-190">開啟檔案 `App_Start\Startup.Auth.cs` 並實作 `ConfigureAuth(...)` 方法。</span><span class="sxs-lookup"><span data-stu-id="2b87b-190">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="2b87b-191">您在 `OpenIdConnectAuthenticationOptions` 中所提供的參數會做為座標，讓您的應用程式與 Azure AD B2C 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="2b87b-191">The parameters you provide in `OpenIdConnectAuthenticationOptions` serve as coordinates for your app to communicate with Azure AD B2C.</span></span> <span data-ttu-id="2b87b-192">如果未指定特定參數，它會使用預設值。</span><span class="sxs-lookup"><span data-stu-id="2b87b-192">If you do not specify certain parameters, it will use the default value.</span></span> <span data-ttu-id="2b87b-193">例如，我們不在範例中指定 `ResponseType`，因此預設值 `code id_token` 將用於每個對 Azure AD B2C 的外送要求。</span><span class="sxs-lookup"><span data-stu-id="2b87b-193">For example, we do not specify the `ResponseType` in the sample, so the default value `code id_token` will be used in each outgoing request to Azure AD B2C.</span></span>

<span data-ttu-id="2b87b-194">您還必須設定 Cookie 驗證。</span><span class="sxs-lookup"><span data-stu-id="2b87b-194">You also need to set up cookie authentication.</span></span> <span data-ttu-id="2b87b-195">OpenID Connect 中介軟體會使用 Cookie 維護使用者工作階段，此外還有其他用途。</span><span class="sxs-lookup"><span data-stu-id="2b87b-195">The OpenID Connect middleware uses cookies to maintain user sessions, among other things.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure the OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate the metadata address using the tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify the callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify the claims to validate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify the scope by appending all of the scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement the "Notification" methods...
}
```

<span data-ttu-id="2b87b-196">在上述的 `OpenIdConnectAuthenticationOptions` 中，我們會定義一組 OpenID Connect 中介軟體所收到的特定通知之回呼函式。</span><span class="sxs-lookup"><span data-stu-id="2b87b-196">In `OpenIdConnectAuthenticationOptions` above, we define a set of callback functions for specific notifications that are received by the OpenID Connect middleware.</span></span> <span data-ttu-id="2b87b-197">這些行為會使用 `OpenIdConnectAuthenticationNotifications` 物件來定義，並儲存至 `Notifications` 變數。</span><span class="sxs-lookup"><span data-stu-id="2b87b-197">These behaviors are defined using a `OpenIdConnectAuthenticationNotifications` object and stored into the `Notifications` variable.</span></span> <span data-ttu-id="2b87b-198">在我們的範例中，我們會根據事件定義三個不同的回呼。</span><span class="sxs-lookup"><span data-stu-id="2b87b-198">In our sample, we define three different callbacks depending on the event.</span></span>

### <a name="using-different-policies"></a><span data-ttu-id="2b87b-199">使用不同的原則</span><span class="sxs-lookup"><span data-stu-id="2b87b-199">Using different policies</span></span>

<span data-ttu-id="2b87b-200">`RedirectToIdentityProvider` 在對 Azure AD B2C 要求時就會觸發通知。</span><span class="sxs-lookup"><span data-stu-id="2b87b-200">The `RedirectToIdentityProvider` notification is triggered whenever a request is made to Azure AD B2C.</span></span> <span data-ttu-id="2b87b-201">在回呼函式 `OnRedirectToIdentityProvider` 中，如果我們想要使用不同的原則，我們會簽入撥出呼叫。</span><span class="sxs-lookup"><span data-stu-id="2b87b-201">In the callback function `OnRedirectToIdentityProvider`, we check in the outgoing call if we want to use a different policy.</span></span> <span data-ttu-id="2b87b-202">若要執行密碼重設或編輯設定檔，您必須使用對應的原則，例如密碼重設原則，而不是預設的「註冊或登入」原則。</span><span class="sxs-lookup"><span data-stu-id="2b87b-202">In order to do a password reset or edit a profile, you need to use the corresponding policy such as the password reset policy instead of the default "Sign-up or Sign-in" policy.</span></span>

<span data-ttu-id="2b87b-203">在我們的範例中，當使用者想要重設密碼或編輯設定檔時，我們會新增我們想要在 OWIN 內容中使用的原則。</span><span class="sxs-lookup"><span data-stu-id="2b87b-203">In our sample, when a user wants to reset the password or edit the profile, we add the policy we prefer to use into the OWIN context.</span></span> <span data-ttu-id="2b87b-204">可以透過下列方式完成︰</span><span class="sxs-lookup"><span data-stu-id="2b87b-204">That can be done by doing the following:</span></span>

```CSharp
    // Let the middleware know you are trying to use the edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

<span data-ttu-id="2b87b-205">且您可以藉由執行下列方法實作回呼函式 `OnRedirectToIdentityProvider`︰</span><span class="sxs-lookup"><span data-stu-id="2b87b-205">And you can implement the callback function `OnRedirectToIdentityProvider` by doing the following:</span></span>

```CSharp
/*
*  On each call to Azure AD B2C, check if a policy (e.g. the profile edit or password reset policy) has been specified in the OWIN context.
*  If so, use that policy when making the call. Also, don't request a code (since it won't be needed).
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

### <a name="handling-authorization-codes"></a><span data-ttu-id="2b87b-206">處理授權碼</span><span class="sxs-lookup"><span data-stu-id="2b87b-206">Handling authorization codes</span></span>

<span data-ttu-id="2b87b-207">收到授權碼時會觸發 `AuthorizationCodeReceived` 通知。</span><span class="sxs-lookup"><span data-stu-id="2b87b-207">The `AuthorizationCodeReceived` notification is triggered when an authorization code is received.</span></span> <span data-ttu-id="2b87b-208">OpenID Connect 中介軟體不支援存取權杖的交換程式碼。</span><span class="sxs-lookup"><span data-stu-id="2b87b-208">The OpenID Connect middleware does not support exchanging codes for access tokens.</span></span> <span data-ttu-id="2b87b-209">您可以手動交換回呼函式中的權杖程式碼。</span><span class="sxs-lookup"><span data-stu-id="2b87b-209">You can manually exchange the code for the token in a callback function.</span></span> <span data-ttu-id="2b87b-210">如需詳細資訊，請參閱說明做法的[文件](active-directory-b2c-devquickstarts-web-api-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="2b87b-210">For more information, please look at the [documentation](active-directory-b2c-devquickstarts-web-api-dotnet.md) that explains how.</span></span>

### <a name="handling-errors"></a><span data-ttu-id="2b87b-211">處理錯誤</span><span class="sxs-lookup"><span data-stu-id="2b87b-211">Handling errors</span></span>

<span data-ttu-id="2b87b-212">驗證失敗時，會觸發 `AuthenticationFailed` 通知。</span><span class="sxs-lookup"><span data-stu-id="2b87b-212">The `AuthenticationFailed` notification is triggered when authentication fails.</span></span> <span data-ttu-id="2b87b-213">在其回呼方法中，您可以如您所願處理錯誤。</span><span class="sxs-lookup"><span data-stu-id="2b87b-213">In its callback method, you can handle the errors as you wish.</span></span> <span data-ttu-id="2b87b-214">不過，您應該新增錯誤碼 `AADB2C90118` 的檢查。</span><span class="sxs-lookup"><span data-stu-id="2b87b-214">You should however add a check for the error code `AADB2C90118`.</span></span> <span data-ttu-id="2b87b-215">在執行「註冊或登入」原則期間，使用者有機會選取 [忘記密碼] 連結。</span><span class="sxs-lookup"><span data-stu-id="2b87b-215">During the execution of the "Sign-up or Sign-in" policy, the user has the opportunity to select a **Forgot your password?** link.</span></span> <span data-ttu-id="2b87b-216">在此情況下，Azure AD B2C 會將該錯誤代碼傳送給您的應用程式，其指出您的應用程式須改為使用密碼重設原則來進行要求。</span><span class="sxs-lookup"><span data-stu-id="2b87b-216">In this event, Azure AD B2C sends your app that error code indicating that your app should make a request using the password reset policy instead.</span></span>

```CSharp
/*
* Catch any failures received by the authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle the error code that Azure AD B2C throws when trying to reset a password from the login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If the user clicked the reset password link, redirect to the reset password route
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

### <a name="send-authentication-requests-to-azure-ad"></a><span data-ttu-id="2b87b-217">將驗證要求傳送至 Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b87b-217">Send authentication requests to Azure AD</span></span>

<span data-ttu-id="2b87b-218">您的應用程式現在已正確設定，將使用 OpenID Connect 驗證通訊協定與 Azure AD B2C 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="2b87b-218">Your app is now properly configured to communicate with Azure AD B2C by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="2b87b-219">OWIN 會管理有關製作驗證訊息、驗證 Azure AD B2C 的權杖，以及維護使用者工作階段的細節。</span><span class="sxs-lookup"><span data-stu-id="2b87b-219">OWIN manages the details of crafting authentication messages, validating tokens from Azure AD B2C, and maintaining user session.</span></span> <span data-ttu-id="2b87b-220">剩下的就是啟動每個使用者的流程。</span><span class="sxs-lookup"><span data-stu-id="2b87b-220">All that remains is to initiate each user's flow.</span></span>

<span data-ttu-id="2b87b-221">當使用者在 Web 應用程式中選取 [註冊/登入]、[編輯設定檔] 或 [重設密碼] 時，`Controllers\AccountController.cs`中會叫用相關聯的動作：</span><span class="sxs-lookup"><span data-stu-id="2b87b-221">When a user selects **Sign up/Sign in**, **Edit profile**, or **Reset password** in the web app, the associated action is invoked in `Controllers\AccountController.cs`:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting to sign up or sign in
*/
public void SignUpSignIn()
{
    // Use the default policy to process the sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting to edit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let the middleware know you are trying to use the edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set the page to redirect to after editing the profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting to reset a password
*/
public void ResetPassword()
{
    // Let the middleware know you are trying to use the reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set the page to redirect to after changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

<span data-ttu-id="2b87b-222">您也可以使用 OWIN 將使用者登出應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b87b-222">You can also use OWIN to sign out the user from the app.</span></span> <span data-ttu-id="2b87b-223">在 `Controllers\AccountController.cs` 中，我們有︰</span><span class="sxs-lookup"><span data-stu-id="2b87b-223">In `Controllers\AccountController.cs` we have:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting to sign out
*/
public void SignOut()
{
    // To sign out the user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

<span data-ttu-id="2b87b-224">除了明確叫用原則外，您也可以在控制器中使用會在使用者未登入時執行原則的 `[Authorize]` 標記。</span><span class="sxs-lookup"><span data-stu-id="2b87b-224">In addition to explicitly invoking a policy, you can use a `[Authorize]` tag in your controllers that executes a policy if the user is not signed in.</span></span> <span data-ttu-id="2b87b-225">開啟 `Controllers\HomeController.cs`，將 `[Authorize]` 標籤新增至宣告控制器。</span><span class="sxs-lookup"><span data-stu-id="2b87b-225">Open `Controllers\HomeController.cs` and add the `[Authorize]` tag to the claims controller.</span></span>  <span data-ttu-id="2b87b-226">在觸及 `[Authorize]` 標籤時，OWIN 會選取所設定的最後一個原則。</span><span class="sxs-lookup"><span data-stu-id="2b87b-226">OWIN selects the last policy configured when the `[Authorize]` tag is hit.</span></span>

```CSharp
// Controllers\HomeController.cs

// You can use the Authorize decorator to execute a certain policy if the user is not already signed into the app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a><span data-ttu-id="2b87b-227">顯示使用者資訊</span><span class="sxs-lookup"><span data-stu-id="2b87b-227">Display user information</span></span>

<span data-ttu-id="2b87b-228">當您使用 OpenID Connect 驗證使用者時，Azure AD B2C 會將包含 **宣告**的 ID 權杖傳回給應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b87b-228">When you authenticate users by using OpenID Connect, Azure AD B2C returns an ID token to the app that contains **claims**.</span></span> <span data-ttu-id="2b87b-229">這些是有關使用者的判斷提示。</span><span class="sxs-lookup"><span data-stu-id="2b87b-229">These are assertions about the user.</span></span> <span data-ttu-id="2b87b-230">您可以使用宣告來個人化應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b87b-230">You can use claims to personalize your app.</span></span>

<span data-ttu-id="2b87b-231">開啟 `Controllers\HomeController.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="2b87b-231">Open the `Controllers\HomeController.cs` file.</span></span> <span data-ttu-id="2b87b-232">您可以透過 `ClaimsPrincipal.Current` 安全性主體物件來存取控制器中的使用者宣告。</span><span class="sxs-lookup"><span data-stu-id="2b87b-232">You can access user claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

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

<span data-ttu-id="2b87b-233">您可以用相同方式存取您的應用程式所接收的任何宣告。</span><span class="sxs-lookup"><span data-stu-id="2b87b-233">You can access any claim that your application receives in the same way.</span></span>  <span data-ttu-id="2b87b-234">您可以在 [宣告]  頁面看到應用程式收到的所有宣告的清單。</span><span class="sxs-lookup"><span data-stu-id="2b87b-234">A list of all the claims the app receives is available for you on the **Claims** page.</span></span>
