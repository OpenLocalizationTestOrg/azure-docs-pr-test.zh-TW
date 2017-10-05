---
title: Azure Active Directory B2C | Microsoft Docs
description: "如何使用 Azure Active Directory B2C 來建置包含登入、註冊及設定檔管理功能的 Windows 桌面應用程式。"
services: active-directory-b2c
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9da14362-8216-4485-960e-af17cd5ba3bd
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: 8e2b5c704230ee2ba1395dc76a1551aaa8e7af7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a><span data-ttu-id="8b6c3-103">Azure AD B2C：建置 Windows 桌面應用程式</span><span class="sxs-lookup"><span data-stu-id="8b6c3-103">Azure AD B2C: Build a Windows desktop app</span></span>
<span data-ttu-id="8b6c3-104">如果您利用 Azure Active Directory (Azure AD) B2C，只要幾個簡短的步驟，就在您的桌面應用程式中新增功能強大的自助式身分識別管理功能。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features to your desktop app in a few short steps.</span></span> <span data-ttu-id="8b6c3-105">本文章說明如何建立 .NET Windows Presentation Foundation (WPF)「待辦事項清單」應用程式，其中包含使用者註冊、登入和設定檔管理的功能。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-105">This article will show you how to create a .NET Windows Presentation Foundation (WPF) "to-do list" app that includes user sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="8b6c3-106">該應用程式將支援以使用者名稱或電子郵件來註冊及登入的功能。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-106">The app will include support for sign-up and sign-in by using a user name or email.</span></span> <span data-ttu-id="8b6c3-107">它也會支援以社交帳戶 (例如 Facebook 和 Google) 來註冊及登入。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-107">It will also include support for sign-up and sign-in by using social accounts such as Facebook and Google.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="8b6c3-108">取得 Azure AD B2C 目錄</span><span class="sxs-lookup"><span data-stu-id="8b6c3-108">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="8b6c3-109">您必須先建立目錄或租用戶，才可使用 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="8b6c3-110">目錄是適用於所有使用者、app、群組等項目的容器。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="8b6c3-111">如果您還沒有此資源，請先 [建立 B2C 目錄](active-directory-b2c-get-started.md) ，再繼續進行本指南。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="8b6c3-112">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="8b6c3-112">Create an application</span></span>
<span data-ttu-id="8b6c3-113">接著，您必須在 B2C 目錄中建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-113">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="8b6c3-114">這會提供必要資訊給 Azure AD，讓它與應用程式安全地通訊。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-114">This gives Azure AD information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="8b6c3-115">若要建立應用程式，請遵循 [這些指示](active-directory-b2c-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-115">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span>  <span data-ttu-id="8b6c3-116">請務必：</span><span class="sxs-lookup"><span data-stu-id="8b6c3-116">Be sure to:</span></span>

* <span data-ttu-id="8b6c3-117">在應用程式中加入 **原生用戶端** 。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-117">Include a **native client** in the application.</span></span>
* <span data-ttu-id="8b6c3-118">複製**重新導向 URI** `urn:ietf:wg:oauth:2.0:oob`。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-118">Copy the **Redirect URI** `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="8b6c3-119">這是此程式碼範例的預設 URL。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-119">It is the default URL for this code sample.</span></span>
* <span data-ttu-id="8b6c3-120">複製指派給您的應用程式的 **應用程式識別碼** 。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-120">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="8b6c3-121">稍後您將會用到此資訊。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-121">You will need it later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="8b6c3-122">建立您的原則</span><span class="sxs-lookup"><span data-stu-id="8b6c3-122">Create your policies</span></span>
<span data-ttu-id="8b6c3-123">在 Azure AD B2C 中，每個使用者經驗皆由 [原則](active-directory-b2c-reference-policies.md)所定義。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="8b6c3-124">此程式碼範例包含三種身分識別體驗：註冊、登入和編輯設定檔。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-124">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span></span> <span data-ttu-id="8b6c3-125">您必須為每個類型建立一個原則，如 [原則參考文章](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)中所述。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-125">You need to create a policy for each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="8b6c3-126">建立這三個原則時，請務必：</span><span class="sxs-lookup"><span data-stu-id="8b6c3-126">When you create the three policies, be sure to:</span></span>

* <span data-ttu-id="8b6c3-127">在識別提供者刀鋒視窗中，選擇 [使用者識別碼註冊] 或 [電子郵件註冊]。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-127">Choose either **User ID sign-up** or **Email sign-up** in the identity providers blade.</span></span>
* <span data-ttu-id="8b6c3-128">在註冊原則中，選擇 [顯示名稱]  和其他註冊屬性。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-128">Choose **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="8b6c3-129">針對每個原則選擇 [顯示名稱] 和 [物件識別碼] 宣告做為應用程式宣告。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-129">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="8b6c3-130">您也可以選擇其他宣告。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-130">You can choose other claims as well.</span></span>
* <span data-ttu-id="8b6c3-131">在您建立每個原則之後，請複製原則的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-131">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="8b6c3-132">其前置詞應該為 `b2c_1_`。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-132">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="8b6c3-133">稍後您將需要這些原則名稱。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-133">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="8b6c3-134">當您成功建立這三個原則之後，就可以開始建置您的 app。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-134">After you have successfully created the three policies, you're ready to build your app.</span></span>

## <a name="download-the-code"></a><span data-ttu-id="8b6c3-135">下載程式碼</span><span class="sxs-lookup"><span data-stu-id="8b6c3-135">Download the code</span></span>
<span data-ttu-id="8b6c3-136">本教學課程的程式碼保留在 [GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet)。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-136">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span></span> <span data-ttu-id="8b6c3-137">如要依照指示建置範例，請 [下載 .zip 檔案格式的基本架構專案](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip)。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-137">To build the sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span></span> <span data-ttu-id="8b6c3-138">您也可以複製基本架構：</span><span class="sxs-lookup"><span data-stu-id="8b6c3-138">You can also clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

<span data-ttu-id="8b6c3-139">完整的 App 也[提供 .zip 檔案格式](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip)，或放在相同儲存機制的 `complete` 分支中。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-139">The completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) or on the `complete` branch of the same repository.</span></span>

<span data-ttu-id="8b6c3-140">下載範例程式碼後，請開啟 Visual Studio .sln 檔案開始進行。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-140">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="8b6c3-141">`TaskClient` 專案是使用者與之互動的 WPF 桌面應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-141">The `TaskClient` project is the WPF desktop application that the user interacts with.</span></span> <span data-ttu-id="8b6c3-142">基於本教學課程的目的，它會呼叫後端工作 Web API (裝載在 Azure 中) 以儲存每個使用者的待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-142">For the purposes of this tutorial, it calls a back-end task web API, hosted in Azure, that stores each user's to-do list.</span></span>  <span data-ttu-id="8b6c3-143">您不需要建置 Web API，我們已經為您執行它。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-143">You do not need to build the web API, we already have it running for you.</span></span>

<span data-ttu-id="8b6c3-144">如要了解 Web API 如何利用 Azure AD B2C 來安全地驗證要求，請查看 [Web API 開始使用文章](active-directory-b2c-devquickstarts-api-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-144">To learn how a web API securely authenticates requests by using Azure AD B2C, check out the [web API getting started article](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="execute-policies"></a><span data-ttu-id="8b6c3-145">執行原則</span><span class="sxs-lookup"><span data-stu-id="8b6c3-145">Execute policies</span></span>
<span data-ttu-id="8b6c3-146">您的應用程式與 Azure AD B2C 通訊時會傳送驗證訊息，其中指定它們想要在 HTTP 要求中執行的原則。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-146">Your app communicates with Azure AD B2C by sending authentication messages that specify the policy they want to execute as part of the HTTP request.</span></span> <span data-ttu-id="8b6c3-147">對於 .NET 桌面應用程式，您可以使用預覽 Microsoft Authentication Library (MSAL) 來傳送 OAuth 2.0 驗證訊息、執行原則，並取得會呼叫 Web API 的權杖。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-147">For .NET desktop applications, you can use the preview Microsoft Authentication Library (MSAL) to send OAuth 2.0 authentication messages, execute policies, and get tokens that call web APIs.</span></span>

### <a name="install-msal"></a><span data-ttu-id="8b6c3-148">安裝 MSAL</span><span class="sxs-lookup"><span data-stu-id="8b6c3-148">Install MSAL</span></span>
<span data-ttu-id="8b6c3-149">使用 Visual Studio Package Manager Console 來把 MSAL 新增到 `TaskClient` 專案中。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-149">Add MSAL to the `TaskClient` project by using the Visual Studio Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a><span data-ttu-id="8b6c3-150">輸入 B2C 詳細資料</span><span class="sxs-lookup"><span data-stu-id="8b6c3-150">Enter your B2C details</span></span>
<span data-ttu-id="8b6c3-151">開啟檔案 `Globals.cs` ，然後用您自己的值來取代每個屬性值。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-151">Open the file `Globals.cs` and replace each of the property values with your own.</span></span> <span data-ttu-id="8b6c3-152">整個 `TaskClient` 都會使用這個類別來參考常用的值。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-152">This class is used throughout `TaskClient` to reference commonly used values.</span></span>

```C#
public static class Globals
{
    ...

    // TODO: Replace these five default with your own configuration values
    public static string tenant = "fabrikamb2c.onmicrosoft.com";
    public static string clientId = "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6";
    public static string signInPolicy = "b2c_1_sign_in";
    public static string signUpPolicy = "b2c_1_sign_up";
    public static string editProfilePolicy = "b2c_1_edit_profile";

    ...
}
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="create-the-publicclientapplication"></a><span data-ttu-id="8b6c3-153">建立 PublicClientApplication</span><span class="sxs-lookup"><span data-stu-id="8b6c3-153">Create the PublicClientApplication</span></span>
<span data-ttu-id="8b6c3-154">MSAL 的主要類別是 `PublicClientApplication`。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-154">The primary class of MSAL is `PublicClientApplication`.</span></span> <span data-ttu-id="8b6c3-155">此類別代表您在 Azure AD B2C 系統中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-155">This class represents your application in the Azure AD B2C system.</span></span> <span data-ttu-id="8b6c3-156">當應用程式初始化時，請在 `MainWindow.xaml.cs` 中建立 `PublicClientApplication` 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-156">When the app initalizes, create an instance of `PublicClientApplication` in `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="8b6c3-157">這可用在整個視窗上。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-157">This can be used throughout the window.</span></span>

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens to persist when the user closes the app,
        // we've extended the MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a><span data-ttu-id="8b6c3-158">起始註冊流程</span><span class="sxs-lookup"><span data-stu-id="8b6c3-158">Initiate a sign-up flow</span></span>
<span data-ttu-id="8b6c3-159">當使用者選擇要註冊時，您會想要起始利用您所建立註冊原則的註冊流程。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-159">When a user opts to signs up, you want to initiate a sign-up flow that uses the sign-up policy you created.</span></span> <span data-ttu-id="8b6c3-160">藉由使用 MSAL，您只要呼叫 `pca.AcquireTokenAsync(...)`即可。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-160">By using MSAL, you just call `pca.AcquireTokenAsync(...)`.</span></span> <span data-ttu-id="8b6c3-161">您傳遞給 `AcquireTokenAsync(...)` 的參數決定您會收到哪個權杖、用於驗證要求中的原則等等。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-161">The parameters you pass to `AcquireTokenAsync(...)` determine which token you receive, the policy used in the authentication request, and more.</span></span>

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use the app's clientId here as the scope parameter, indicating that
        // you want a token to the your app's backend web API (represented by
        // the cloud hosted task API).  Use the UiOptions.ForceLogin flag to
        // indicate to MSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in the app that the user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When the request completes successfully, you can get user
        // information from the AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After the sign up successfully completes, display the user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of the policy.
    catch (MsalException ex)
    {
        if (ex.ErrorCode != "authentication_canceled")
        {
            // An unexpected error occurred.
            string message = ex.Message;
            if (ex.InnerException != null)
            {
                message += "Inner Exception : " + ex.InnerException.Message;
            }

            MessageBox.Show(message);
        }

        return;
    }
}
```

### <a name="initiate-a-sign-in-flow"></a><span data-ttu-id="8b6c3-162">起始登入流程</span><span class="sxs-lookup"><span data-stu-id="8b6c3-162">Initiate a sign-in flow</span></span>
<span data-ttu-id="8b6c3-163">您可以用您起始註冊流程的相同方式來起始登入流程。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-163">You can initiate a sign-in flow in the same way that you initiate a sign-up flow.</span></span> <span data-ttu-id="8b6c3-164">當使用者登入時，請用同樣的方式呼叫 MSAL，但這次是利用您的登入原則：</span><span class="sxs-lookup"><span data-stu-id="8b6c3-164">When a user signs in, make the same call to MSAL, this time by using your sign-in policy:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.signInPolicy);
        ...
```

### <a name="initiate-an-edit-profile-flow"></a><span data-ttu-id="8b6c3-165">起始編輯設定檔流程</span><span class="sxs-lookup"><span data-stu-id="8b6c3-165">Initiate an edit-profile flow</span></span>
<span data-ttu-id="8b6c3-166">同樣地，您可以用相同的方式執行編輯設定檔原則：</span><span class="sxs-lookup"><span data-stu-id="8b6c3-166">Again, you can execute an edit-profile policy in the same fashion:</span></span>

```C#
private async void EditProfile(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.editProfilePolicy);
```

<span data-ttu-id="8b6c3-167">在所有這些案例中，MSAL 會傳回 `AuthenticationResult` 中的權杖，或是擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-167">In all of these cases, MSAL either returns a token in `AuthenticationResult` or throws an exception.</span></span> <span data-ttu-id="8b6c3-168">每次從 MSAL 取得權杖時，您都可以使用 `AuthenticationResult.User` 物件來更新應用程式中的使用者資料，例如 UI。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-168">Each time you get a token from MSAL, you can use the `AuthenticationResult.User` object to update the user data in the app, such as the UI.</span></span> <span data-ttu-id="8b6c3-169">ADAL 也會快取權杖，以供應用程式的其他部分使用。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-169">ADAL also caches the token for use in other parts of the application.</span></span>

### <a name="check-for-tokens-on-app-start"></a><span data-ttu-id="8b6c3-170">在應用程式啟動時檢查權杖</span><span class="sxs-lookup"><span data-stu-id="8b6c3-170">Check for tokens on app start</span></span>
<span data-ttu-id="8b6c3-171">您也可以使用 MSAL 來追蹤使用者的登入狀態。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-171">You can also use MSAL to keep track of the user's sign-in state.</span></span>  <span data-ttu-id="8b6c3-172">在此應用程式中，我們想要讓使用者在關閉應用程式再予以重新開啟後仍保持登入狀態。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-172">In this app, we want the user to remain signed in even after they close the app & re-open it.</span></span>  <span data-ttu-id="8b6c3-173">回到 `OnInitialized` 覆寫，使用 MSAL 的 `AcquireTokenSilent` 方法來檢查已快取的權杖︰</span><span class="sxs-lookup"><span data-stu-id="8b6c3-173">Back inside the `OnInitialized` override, use MSAL's `AcquireTokenSilent` method to check for cached tokens:</span></span>

```C#
AuthenticationResult result = null;
try
{
    // If the user has has a token cached with any policy, we'll display them as signed-in.
    TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
    string existingPolicy = tci == null ? null : tci.Policy;
    result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    SignInButton.Visibility = Visibility.Collapsed;
    SignUpButton.Visibility = Visibility.Collapsed;
    EditProfileButton.Visibility = Visibility.Visible;
    SignOutButton.Visibility = Visibility.Visible;
    UsernameLabel.Content = result.User.Name;
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "failed_to_acquire_token_silently")
    {
        // There are no tokens in the cache.  Proceed without calling the To Do list service.
    }
    else
    {
        // An unexpected error occurred.
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
    return;
}
```

## <a name="call-the-task-api"></a><span data-ttu-id="8b6c3-174">呼叫工作 API</span><span class="sxs-lookup"><span data-stu-id="8b6c3-174">Call the task API</span></span>
<span data-ttu-id="8b6c3-175">您已經使用 MSAL 來執行原則並取得權杖。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-175">You have now used MSAL to execute policies and get tokens.</span></span>  <span data-ttu-id="8b6c3-176">當您想要使用這些權杖的其中一個來呼叫工作 API 時，您可以再次使用 MSAL 的 `AcquireTokenSilent` 方法來檢查已快取的權杖︰</span><span class="sxs-lookup"><span data-stu-id="8b6c3-176">When you want to use one these tokens to call the task API, you can again use MSAL's `AcquireTokenSilent` method to check for cached tokens:</span></span>

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want to check for a cached token, independent of whatever policy was used to acquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent to indicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch the exception and show the user a message.
    catch (MsalException ex)
    {
        // There is no access token in the cache, so prompt the user to sign-in.
        if (ex.ErrorCode == "failed_to_acquire_token_silently")
        {
            MessageBox.Show("Please sign up or sign in first");
            SignInButton.Visibility = Visibility.Visible;
            SignUpButton.Visibility = Visibility.Visible;
            EditProfileButton.Visibility = Visibility.Collapsed;
            SignOutButton.Visibility = Visibility.Collapsed;
            UsernameLabel.Content = string.Empty;
        }
        else
        {
            // An unexpected error occurred.
            string message = ex.Message;
            if (ex.InnerException != null)
            {
                message += "Inner Exception : " + ex.InnerException.Message;
            }
            MessageBox.Show(message);
        }

        return;
    }
    ...
```

<span data-ttu-id="8b6c3-177">當您成功呼叫 `AcquireTokenSilentAsync(...)`，且在快取中找到權杖之後，便可以將該權杖新增至 HTTP 要求的 `Authorization` 標頭中。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-177">When the call to `AcquireTokenSilentAsync(...)` succeeds and a token is found in the cache, you can add the token to the `Authorization` header of the HTTP request.</span></span> <span data-ttu-id="8b6c3-178">工作 Web API 會使用此標頭來驗證讀取使用者待辦事項清單的要求︰</span><span class="sxs-lookup"><span data-stu-id="8b6c3-178">The task web API will use this header to authenticate the request to read the user's to-do list:</span></span>

```C#
    ...
    // Once the token has been returned by MSAL, add it to the http authorization header, before making the call to access the To Do list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call the To Do list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-the-user-out"></a><span data-ttu-id="8b6c3-179">登出使用者</span><span class="sxs-lookup"><span data-stu-id="8b6c3-179">Sign the user out</span></span>
<span data-ttu-id="8b6c3-180">最後，您可以在使用者選取 [登出] 時，使用 MSAL 來結束使用者的應用程式工作階段。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-180">Finally, you can use MSAL to end a user's session with the app when the user selects **Sign out**.</span></span>  <span data-ttu-id="8b6c3-181">在使用 MSAL 時，您只要清除權杖快取中的所有權杖即可：</span><span class="sxs-lookup"><span data-stu-id="8b6c3-181">When using MSAL, this is accomplished by clearing all of the tokens from the token cache:</span></span>

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of the user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in the browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update the UI to show the user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-the-sample-app"></a><span data-ttu-id="8b6c3-182">執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="8b6c3-182">Run the sample app</span></span>
<span data-ttu-id="8b6c3-183">最後，建置並執行範例。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-183">Finally, build and run the sample.</span></span>  <span data-ttu-id="8b6c3-184">使用電子郵件地址或使用者名稱來註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-184">Sign up for the app by using an email address or user name.</span></span> <span data-ttu-id="8b6c3-185">登出，再以相同的使用者身分重新登入。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-185">Sign out and sign back in as the same user.</span></span> <span data-ttu-id="8b6c3-186">編輯該使用者的設定檔。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-186">Edit that user's profile.</span></span> <span data-ttu-id="8b6c3-187">請登出，然後以不同的使用者身分登入。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-187">Sign out and sign up by using a different user.</span></span>

## <a name="add-social-idps"></a><span data-ttu-id="8b6c3-188">新增社交 IDP</span><span class="sxs-lookup"><span data-stu-id="8b6c3-188">Add social IDPs</span></span>
<span data-ttu-id="8b6c3-189">目前，應用程式僅支援使用者以 **本機帳戶**來註冊及登入。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-189">Currently, the app supports only user sign-up and sign-in that use **local accounts**.</span></span> <span data-ttu-id="8b6c3-190">這些是儲存在 B2C 目錄中使用使用者名稱和密碼的帳戶。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-190">These are accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="8b6c3-191">藉由使用 Azure AD B2C，您可以新增對其他身分識別提供者 (IDP) 的支援，但不需變更任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-191">By using Azure AD B2C, you can add support for other identity providers (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="8b6c3-192">若要將社交 IDP 加入至應用程式，請依照下列文章中的詳細指示開始。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-192">To add social IDPs to your app, begin by following the detailed instructions in these articles.</span></span> <span data-ttu-id="8b6c3-193">針對您想要支援的每個 IDP，您必須在該系統中註冊應用程式並取得用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-193">For each IDP you want to support, you need to register an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="8b6c3-194">將 Facebook 設定為 IDP</span><span class="sxs-lookup"><span data-stu-id="8b6c3-194">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="8b6c3-195">將 Google 設定為 IDP</span><span class="sxs-lookup"><span data-stu-id="8b6c3-195">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="8b6c3-196">將 Amazon 設定為 IDP</span><span class="sxs-lookup"><span data-stu-id="8b6c3-196">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="8b6c3-197">將 LinkedIn 設定為 IDP</span><span class="sxs-lookup"><span data-stu-id="8b6c3-197">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="8b6c3-198">當您將身分識別提供者新增到 B2C 目錄之後，就必須分別編輯您的三個原則來包含新的 IDP，如 [原則參考文章](active-directory-b2c-reference-policies.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-198">After you add the identity providers to your B2C directory, you need to edit each of your three policies to include the new IDPs, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="8b6c3-199">儲存您的原則之後，重新執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-199">After you save your policies, run the app again.</span></span> <span data-ttu-id="8b6c3-200">在每一次的身分識別體驗中，您應該會看到新的 IDP 已加入成為登入和註冊選項。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-200">You should see the new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="8b6c3-201">您可以在範例應用程式上對原則進行試驗，並觀察試驗結果。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-201">You can experiment with your policies and observe the effects on your sample app.</span></span> <span data-ttu-id="8b6c3-202">新增或移除 IDP、管理應用程式宣告，或變更註冊屬性。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-202">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="8b6c3-203">試驗到您能夠了解原則、驗證要求和 MSAL 如何結合在一起為止。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-203">Experiment until you can see how policies, authentication requests, and MSAL tie together.</span></span>

<span data-ttu-id="8b6c3-204">為供您參考，我們提供 [.zip 檔案格式](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip)的完整範例。</span><span class="sxs-lookup"><span data-stu-id="8b6c3-204">For reference, the completed sample [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="8b6c3-205">您也可以從 Github 複製它：</span><span class="sxs-lookup"><span data-stu-id="8b6c3-205">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
