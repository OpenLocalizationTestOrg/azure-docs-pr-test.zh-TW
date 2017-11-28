---
title: "Active Directory B2C aaaAzure |Microsoft 文件"
description: "如何 toobuild Windows 桌面應用程式，包含登入、 註冊，以及使用 Azure Active Directory B2C 分析管理。"
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
ms.openlocfilehash: f22b0299ff74bfba2f3fea88f006da609859dda5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a><span data-ttu-id="d0103-103">Azure AD B2C：建置 Windows 桌面應用程式</span><span class="sxs-lookup"><span data-stu-id="d0103-103">Azure AD B2C: Build a Windows desktop app</span></span>
<span data-ttu-id="d0103-104">藉由使用 Azure Active Directory (Azure AD) B2C，您可以在幾個簡短步驟中加入功能強大的自助式身分識別管理功能 tooyour 傳統型應用程式。</span><span class="sxs-lookup"><span data-stu-id="d0103-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features tooyour desktop app in a few short steps.</span></span> <span data-ttu-id="d0103-105">這篇文章將示範如何 toocreate.NET Windows Presentation Foundation (WPF) 「 待辦事項清單 」 應用程式，其中包含註冊、 登入的使用者和管理設定檔。</span><span class="sxs-lookup"><span data-stu-id="d0103-105">This article will show you how toocreate a .NET Windows Presentation Foundation (WPF) "to-do list" app that includes user sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="d0103-106">hello 應用程式會使用使用者名稱或電子郵件包含支援註冊和登入。</span><span class="sxs-lookup"><span data-stu-id="d0103-106">hello app will include support for sign-up and sign-in by using a user name or email.</span></span> <span data-ttu-id="d0103-107">它也會支援以社交帳戶 (例如 Facebook 和 Google) 來註冊及登入。</span><span class="sxs-lookup"><span data-stu-id="d0103-107">It will also include support for sign-up and sign-in by using social accounts such as Facebook and Google.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="d0103-108">取得 Azure AD B2C 目錄</span><span class="sxs-lookup"><span data-stu-id="d0103-108">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="d0103-109">您必須先建立目錄或租用戶，才可使用 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="d0103-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="d0103-110">目錄是適用於所有使用者、app、群組等項目的容器。</span><span class="sxs-lookup"><span data-stu-id="d0103-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="d0103-111">如果您還沒有此資源，請先 [建立 B2C 目錄](active-directory-b2c-get-started.md) ，再繼續進行本指南。</span><span class="sxs-lookup"><span data-stu-id="d0103-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="d0103-112">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="d0103-112">Create an application</span></span>
<span data-ttu-id="d0103-113">接下來，您需要 toocreate 應用程式中 B2C 目錄。</span><span class="sxs-lookup"><span data-stu-id="d0103-113">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="d0103-114">提供 Azure AD，它需要 toosecurely 通訊與您的應用程式的資訊。</span><span class="sxs-lookup"><span data-stu-id="d0103-114">This gives Azure AD information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="d0103-115">toocreate 的應用程式，請遵循[這些指示](active-directory-b2c-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="d0103-115">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span>  <span data-ttu-id="d0103-116">請務必：</span><span class="sxs-lookup"><span data-stu-id="d0103-116">Be sure to:</span></span>

* <span data-ttu-id="d0103-117">包含**原生用戶端**hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="d0103-117">Include a **native client** in hello application.</span></span>
* <span data-ttu-id="d0103-118">複製 hello**重新導向 URI** `urn:ietf:wg:oauth:2.0:oob`。</span><span class="sxs-lookup"><span data-stu-id="d0103-118">Copy hello **Redirect URI** `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="d0103-119">它是 hello 預設 URL，此程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="d0103-119">It is hello default URL for this code sample.</span></span>
* <span data-ttu-id="d0103-120">複製 hello**應用程式識別碼**也就是指派的 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d0103-120">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="d0103-121">稍後您將會用到此資訊。</span><span class="sxs-lookup"><span data-stu-id="d0103-121">You will need it later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="d0103-122">建立您的原則</span><span class="sxs-lookup"><span data-stu-id="d0103-122">Create your policies</span></span>
<span data-ttu-id="d0103-123">在 Azure AD B2C 中，每個使用者經驗皆由 [原則](active-directory-b2c-reference-policies.md)所定義。</span><span class="sxs-lookup"><span data-stu-id="d0103-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="d0103-124">此程式碼範例包含三種身分識別體驗：註冊、登入和編輯設定檔。</span><span class="sxs-lookup"><span data-stu-id="d0103-124">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span></span> <span data-ttu-id="d0103-125">中所述，每個類型，需要 toocreate 原則[原則參考文件](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)。</span><span class="sxs-lookup"><span data-stu-id="d0103-125">You need toocreate a policy for each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="d0103-126">當您建立 hello 三個原則時，請務必：</span><span class="sxs-lookup"><span data-stu-id="d0103-126">When you create hello three policies, be sure to:</span></span>

* <span data-ttu-id="d0103-127">選擇 [**使用者識別碼註冊**或**電子郵件註冊**hello 身分識別提供者] 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="d0103-127">Choose either **User ID sign-up** or **Email sign-up** in hello identity providers blade.</span></span>
* <span data-ttu-id="d0103-128">在註冊原則中，選擇 [顯示名稱]  和其他註冊屬性。</span><span class="sxs-lookup"><span data-stu-id="d0103-128">Choose **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="d0103-129">針對每個原則選擇 [顯示名稱] 和 [物件識別碼] 宣告做為應用程式宣告。</span><span class="sxs-lookup"><span data-stu-id="d0103-129">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="d0103-130">您也可以選擇其他宣告。</span><span class="sxs-lookup"><span data-stu-id="d0103-130">You can choose other claims as well.</span></span>
* <span data-ttu-id="d0103-131">複製 hello**名稱**的每個原則建立之後。</span><span class="sxs-lookup"><span data-stu-id="d0103-131">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="d0103-132">就不應有 hello 前置詞`b2c_1_`。</span><span class="sxs-lookup"><span data-stu-id="d0103-132">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="d0103-133">稍後您將需要這些原則名稱。</span><span class="sxs-lookup"><span data-stu-id="d0103-133">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="d0103-134">您已成功建立 hello 三個原則之後，您便準備好 toobuild 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d0103-134">After you have successfully created hello three policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="d0103-135">下載 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="d0103-135">Download hello code</span></span>
<span data-ttu-id="d0103-136">hello 本教學課程中的程式碼[維護 GitHub 上](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet)。</span><span class="sxs-lookup"><span data-stu-id="d0103-136">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span></span> <span data-ttu-id="d0103-137">移 toobuild hello 範例時，您可以[下載為.zip 檔案的基本架構專案](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip)。</span><span class="sxs-lookup"><span data-stu-id="d0103-137">toobuild hello sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span></span> <span data-ttu-id="d0103-138">您也可以複製 hello 基本架構：</span><span class="sxs-lookup"><span data-stu-id="d0103-138">You can also clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

<span data-ttu-id="d0103-139">hello 完成應用程式也是[可以做為.zip 檔案](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip)或 hello `complete` hello 分支相同的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="d0103-139">hello completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) or on hello `complete` branch of hello same repository.</span></span>

<span data-ttu-id="d0103-140">下載 hello 範例程式碼之後，開啟 hello Visual Studio.sln 檔案 tooget 啟動。</span><span class="sxs-lookup"><span data-stu-id="d0103-140">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="d0103-141">hello`TaskClient`專案是 hello hello 使用者 WPF 桌面應用程式互動。</span><span class="sxs-lookup"><span data-stu-id="d0103-141">hello `TaskClient` project is hello WPF desktop application that hello user interacts with.</span></span> <span data-ttu-id="d0103-142">基於 hello 本教學課程中，它會呼叫後端工作 web API，裝載在 Azure 中，儲存每個使用者的待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="d0103-142">For hello purposes of this tutorial, it calls a back-end task web API, hosted in Azure, that stores each user's to-do list.</span></span>  <span data-ttu-id="d0103-143">您不需要 toobuild hello web API，我們已經為您執行它。</span><span class="sxs-lookup"><span data-stu-id="d0103-143">You do not need toobuild hello web API, we already have it running for you.</span></span>

<span data-ttu-id="d0103-144">toolearn 如何安全地使用 Azure AD B2C，來驗證要求的 web API 簽出[web API 使用者入門文件](active-directory-b2c-devquickstarts-api-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="d0103-144">toolearn how a web API securely authenticates requests by using Azure AD B2C, check out the [web API getting started article](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="execute-policies"></a><span data-ttu-id="d0103-145">執行原則</span><span class="sxs-lookup"><span data-stu-id="d0103-145">Execute policies</span></span>
<span data-ttu-id="d0103-146">您的應用程式可藉由傳送驗證訊息指定他們想 tooexecute hello HTTP 要求的一部分的 hello 原則會與 Azure AD B2C 通訊。</span><span class="sxs-lookup"><span data-stu-id="d0103-146">Your app communicates with Azure AD B2C by sending authentication messages that specify hello policy they want tooexecute as part of hello HTTP request.</span></span> <span data-ttu-id="d0103-147">對於.NET 桌面應用程式，您可以使用 hello 預覽 Microsoft 驗證程式庫 (MSAL) toosend OAuth 2.0 驗證訊息、 執行原則，以及該呼叫 web Api 取得的權杖。</span><span class="sxs-lookup"><span data-stu-id="d0103-147">For .NET desktop applications, you can use hello preview Microsoft Authentication Library (MSAL) toosend OAuth 2.0 authentication messages, execute policies, and get tokens that call web APIs.</span></span>

### <a name="install-msal"></a><span data-ttu-id="d0103-148">安裝 MSAL</span><span class="sxs-lookup"><span data-stu-id="d0103-148">Install MSAL</span></span>
<span data-ttu-id="d0103-149">新增 MSAL toohello `TaskClient` hello Visual Studio Package Manager Console 的專案。</span><span class="sxs-lookup"><span data-stu-id="d0103-149">Add MSAL toohello `TaskClient` project by using hello Visual Studio Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a><span data-ttu-id="d0103-150">輸入 B2C 詳細資料</span><span class="sxs-lookup"><span data-stu-id="d0103-150">Enter your B2C details</span></span>
<span data-ttu-id="d0103-151">開啟 hello 檔案`Globals.cs`並取代每個 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="d0103-151">Open hello file `Globals.cs` and replace each of hello property values with your own.</span></span> <span data-ttu-id="d0103-152">這個類別用在整個`TaskClient`tooreference 常用的值。</span><span class="sxs-lookup"><span data-stu-id="d0103-152">This class is used throughout `TaskClient` tooreference commonly used values.</span></span>

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

### <a name="create-hello-publicclientapplication"></a><span data-ttu-id="d0103-153">建立 hello PublicClientApplication</span><span class="sxs-lookup"><span data-stu-id="d0103-153">Create hello PublicClientApplication</span></span>
<span data-ttu-id="d0103-154">hello MSAL 主要類別是`PublicClientApplication`。</span><span class="sxs-lookup"><span data-stu-id="d0103-154">hello primary class of MSAL is `PublicClientApplication`.</span></span> <span data-ttu-id="d0103-155">此類別代表 hello Azure AD B2C 系統中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d0103-155">This class represents your application in hello Azure AD B2C system.</span></span> <span data-ttu-id="d0103-156">當 hello 應用程式初始化建立的執行個體`PublicClientApplication`中`MainWindow.xaml.cs`。</span><span class="sxs-lookup"><span data-stu-id="d0103-156">When hello app initalizes, create an instance of `PublicClientApplication` in `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="d0103-157">這可用於整個 hello 視窗。</span><span class="sxs-lookup"><span data-stu-id="d0103-157">This can be used throughout hello window.</span></span>

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens toopersist when hello user closes hello app,
        // we've extended hello MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a><span data-ttu-id="d0103-158">起始註冊流程</span><span class="sxs-lookup"><span data-stu-id="d0103-158">Initiate a sign-up flow</span></span>
<span data-ttu-id="d0103-159">當使用者選擇 toosigns 組成時，您會想 tooinitiate 會使用您所建立的 hello 註冊原則的註冊流程。</span><span class="sxs-lookup"><span data-stu-id="d0103-159">When a user opts toosigns up, you want tooinitiate a sign-up flow that uses hello sign-up policy you created.</span></span> <span data-ttu-id="d0103-160">藉由使用 MSAL，您只要呼叫 `pca.AcquireTokenAsync(...)`即可。</span><span class="sxs-lookup"><span data-stu-id="d0103-160">By using MSAL, you just call `pca.AcquireTokenAsync(...)`.</span></span> <span data-ttu-id="d0103-161">hello 您太傳遞的參數`AcquireTokenAsync(...)`判斷哪一個語彙基元收到，用於 hello 驗證要求，以及其他 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="d0103-161">hello parameters you pass too`AcquireTokenAsync(...)` determine which token you receive, hello policy used in hello authentication request, and more.</span></span>

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use hello app's clientId here as hello scope parameter, indicating that
        // you want a token toohello your app's backend web API (represented by
        // hello cloud hosted task API).  Use hello UiOptions.ForceLogin flag to
        // indicate tooMSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in hello app that hello user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When hello request completes successfully, you can get user
        // information from hello AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After hello sign up successfully completes, display hello user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of hello policy.
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

### <a name="initiate-a-sign-in-flow"></a><span data-ttu-id="d0103-162">起始登入流程</span><span class="sxs-lookup"><span data-stu-id="d0103-162">Initiate a sign-in flow</span></span>
<span data-ttu-id="d0103-163">您可以起始 hello 的登入流程起始註冊流程的方式相同。</span><span class="sxs-lookup"><span data-stu-id="d0103-163">You can initiate a sign-in flow in hello same way that you initiate a sign-up flow.</span></span> <span data-ttu-id="d0103-164">當使用者登入時，會進行相同的 hello 呼叫 tooMSAL，這次請使用您登入的原則：</span><span class="sxs-lookup"><span data-stu-id="d0103-164">When a user signs in, make hello same call tooMSAL, this time by using your sign-in policy:</span></span>

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

### <a name="initiate-an-edit-profile-flow"></a><span data-ttu-id="d0103-165">起始編輯設定檔流程</span><span class="sxs-lookup"><span data-stu-id="d0103-165">Initiate an edit-profile flow</span></span>
<span data-ttu-id="d0103-166">同樣地，您可以在 hello 中執行的編輯設定檔原則相同的方式：</span><span class="sxs-lookup"><span data-stu-id="d0103-166">Again, you can execute an edit-profile policy in hello same fashion:</span></span>

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

<span data-ttu-id="d0103-167">在所有這些案例中，MSAL 會傳回 `AuthenticationResult` 中的權杖，或是擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d0103-167">In all of these cases, MSAL either returns a token in `AuthenticationResult` or throws an exception.</span></span> <span data-ttu-id="d0103-168">每當您從 MSAL，取得權杖，您可以使用 hello `AuthenticationResult.User` hello 應用程式，例如 hello UI 中的 tooupdate hello 使用者資料的物件。</span><span class="sxs-lookup"><span data-stu-id="d0103-168">Each time you get a token from MSAL, you can use hello `AuthenticationResult.User` object tooupdate hello user data in hello app, such as hello UI.</span></span> <span data-ttu-id="d0103-169">ADAL 也快取 hello hello 應用程式的其他部分中使用的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="d0103-169">ADAL also caches hello token for use in other parts of hello application.</span></span>

### <a name="check-for-tokens-on-app-start"></a><span data-ttu-id="d0103-170">在應用程式啟動時檢查權杖</span><span class="sxs-lookup"><span data-stu-id="d0103-170">Check for tokens on app start</span></span>
<span data-ttu-id="d0103-171">您也可以使用 MSAL tookeep 追蹤 hello 使用者的登入狀態。</span><span class="sxs-lookup"><span data-stu-id="d0103-171">You can also use MSAL tookeep track of hello user's sign-in state.</span></span>  <span data-ttu-id="d0103-172">在此應用程式，我們會想 hello 使用者 tooremain 登入，即使他們關閉 hello 應用程式，並重新開啟它。</span><span class="sxs-lookup"><span data-stu-id="d0103-172">In this app, we want hello user tooremain signed in even after they close hello app & re-open it.</span></span>  <span data-ttu-id="d0103-173">傳回內 hello`OnInitialized`覆寫時，使用 MSAL 的`AcquireTokenSilent`方法 toocheck 快取權杖：</span><span class="sxs-lookup"><span data-stu-id="d0103-173">Back inside hello `OnInitialized` override, use MSAL's `AcquireTokenSilent` method toocheck for cached tokens:</span></span>

```C#
AuthenticationResult result = null;
try
{
    // If hello user has has a token cached with any policy, we'll display them as signed-in.
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
        // There are no tokens in hello cache.  Proceed without calling hello tooDo list service.
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

## <a name="call-hello-task-api"></a><span data-ttu-id="d0103-174">呼叫 hello 工作應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="d0103-174">Call hello task API</span></span>
<span data-ttu-id="d0103-175">您現在已經使用 MSAL tooexecute 原則，並取得語彙基元。</span><span class="sxs-lookup"><span data-stu-id="d0103-175">You have now used MSAL tooexecute policies and get tokens.</span></span>  <span data-ttu-id="d0103-176">當您想 toouse 其中一個這些語彙基元 toocall hello 工作應用程式開發介面時，您可以再次使用 MSAL 的`AcquireTokenSilent`方法 toocheck 快取權杖：</span><span class="sxs-lookup"><span data-stu-id="d0103-176">When you want toouse one these tokens toocall hello task API, you can again use MSAL's `AcquireTokenSilent` method toocheck for cached tokens:</span></span>

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want toocheck for a cached token, independent of whatever policy was used tooacquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent tooindicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch hello exception and show hello user a message.
    catch (MsalException ex)
    {
        // There is no access token in hello cache, so prompt hello user toosign-in.
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

<span data-ttu-id="d0103-177">當太 hello 呼叫`AcquireTokenSilentAsync(...)`成功語彙基元並在找到 hello 快取中，您可以加入 hello 語彙基元 toohello `Authorization` hello HTTP 要求標頭。</span><span class="sxs-lookup"><span data-stu-id="d0103-177">When hello call too`AcquireTokenSilentAsync(...)` succeeds and a token is found in hello cache, you can add hello token toohello `Authorization` header of hello HTTP request.</span></span> <span data-ttu-id="d0103-178">hello 工作 web API 將會使用此標頭 tooauthenticate hello 要求 tooread hello 使用者的待辦事項清單：</span><span class="sxs-lookup"><span data-stu-id="d0103-178">hello task web API will use this header tooauthenticate hello request tooread hello user's to-do list:</span></span>

```C#
    ...
    // Once hello token has been returned by MSAL, add it toohello http authorization header, before making hello call tooaccess hello tooDo list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call hello tooDo list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-hello-user-out"></a><span data-ttu-id="d0103-179">符號 hello 使用者登出</span><span class="sxs-lookup"><span data-stu-id="d0103-179">Sign hello user out</span></span>
<span data-ttu-id="d0103-180">最後，您可以使用 MSAL 與 hello 應用程式時 hello 使用者選取的使用者工作階段的 tooend**登出**。當使用 MSAL，這可以藉由清除所有來自 hello 權杖快取的 hello 權杖：</span><span class="sxs-lookup"><span data-stu-id="d0103-180">Finally, you can use MSAL tooend a user's session with hello app when hello user selects **Sign out**.  When using MSAL, this is accomplished by clearing all of hello tokens from hello token cache:</span></span>

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of hello user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in hello browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update hello UI tooshow hello user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-hello-sample-app"></a><span data-ttu-id="d0103-181">執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="d0103-181">Run hello sample app</span></span>
<span data-ttu-id="d0103-182">最後，建置並執行 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="d0103-182">Finally, build and run hello sample.</span></span>  <span data-ttu-id="d0103-183">註冊 hello 應用程式使用電子郵件地址或使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="d0103-183">Sign up for hello app by using an email address or user name.</span></span> <span data-ttu-id="d0103-184">先登出再重新登入為 hello 相同使用者。</span><span class="sxs-lookup"><span data-stu-id="d0103-184">Sign out and sign back in as hello same user.</span></span> <span data-ttu-id="d0103-185">編輯該使用者的設定檔。</span><span class="sxs-lookup"><span data-stu-id="d0103-185">Edit that user's profile.</span></span> <span data-ttu-id="d0103-186">請登出，然後以不同的使用者身分登入。</span><span class="sxs-lookup"><span data-stu-id="d0103-186">Sign out and sign up by using a different user.</span></span>

## <a name="add-social-idps"></a><span data-ttu-id="d0103-187">新增社交 IDP</span><span class="sxs-lookup"><span data-stu-id="d0103-187">Add social IDPs</span></span>
<span data-ttu-id="d0103-188">目前，hello 應用程式僅支援使用者註冊和登入使用**本機帳戶**。</span><span class="sxs-lookup"><span data-stu-id="d0103-188">Currently, hello app supports only user sign-up and sign-in that use **local accounts**.</span></span> <span data-ttu-id="d0103-189">這些是儲存在 B2C 目錄中使用使用者名稱和密碼的帳戶。</span><span class="sxs-lookup"><span data-stu-id="d0103-189">These are accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="d0103-190">藉由使用 Azure AD B2C，您可以新增對其他身分識別提供者 (IDP) 的支援，但不需變更任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="d0103-190">By using Azure AD B2C, you can add support for other identity providers (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="d0103-191">tooadd 社交 IDPs tooyour 應用程式中，遵循開始 hello 詳細這些文章中的指示。</span><span class="sxs-lookup"><span data-stu-id="d0103-191">tooadd social IDPs tooyour app, begin by following hello detailed instructions in these articles.</span></span> <span data-ttu-id="d0103-192">針對每個 IDP 想 toosupport，您必須在該系統 tooregister 應用程式，並取得用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="d0103-192">For each IDP you want toosupport, you need tooregister an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="d0103-193">將 Facebook 設定為 IDP</span><span class="sxs-lookup"><span data-stu-id="d0103-193">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="d0103-194">將 Google 設定為 IDP</span><span class="sxs-lookup"><span data-stu-id="d0103-194">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="d0103-195">將 Amazon 設定為 IDP</span><span class="sxs-lookup"><span data-stu-id="d0103-195">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="d0103-196">將 LinkedIn 設定為 IDP</span><span class="sxs-lookup"><span data-stu-id="d0103-196">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="d0103-197">新增 hello 身分識別提供者 tooyour B2C 目錄之後，您需要的每個 tooinclude hello 新 IDPs，做為您三個原則述 hello tooedit[原則參考文件](active-directory-b2c-reference-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="d0103-197">After you add hello identity providers tooyour B2C directory, you need tooedit each of your three policies tooinclude hello new IDPs, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="d0103-198">儲存您的原則之後，請再次執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d0103-198">After you save your policies, run hello app again.</span></span> <span data-ttu-id="d0103-199">您應該會看到新 IDPs 加入為登入並註冊選項，在每個身分識別體驗中的 hello。</span><span class="sxs-lookup"><span data-stu-id="d0103-199">You should see hello new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="d0103-200">您可以試驗您的原則，並觀察 hello 範例應用程式上的效果。</span><span class="sxs-lookup"><span data-stu-id="d0103-200">You can experiment with your policies and observe hello effects on your sample app.</span></span> <span data-ttu-id="d0103-201">新增或移除 IDP、管理應用程式宣告，或變更註冊屬性。</span><span class="sxs-lookup"><span data-stu-id="d0103-201">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="d0103-202">試驗到您能夠了解原則、驗證要求和 MSAL 如何結合在一起為止。</span><span class="sxs-lookup"><span data-stu-id="d0103-202">Experiment until you can see how policies, authentication requests, and MSAL tie together.</span></span>

<span data-ttu-id="d0103-203">如需參考，hello 完成範例[提供成.zip 檔案](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="d0103-203">For reference, hello completed sample [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="d0103-204">您也可以從 Github 複製它：</span><span class="sxs-lookup"><span data-stu-id="d0103-204">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
