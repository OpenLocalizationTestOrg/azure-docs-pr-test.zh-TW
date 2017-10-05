---
title: "Azure Active Directory B2C：使用 Graph API | Microsoft Docs"
description: "如何使用應用程式身分識別對 B2C 租用戶呼叫圖形 API，以將程序自動化。"
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f9904516-d9f7-43b1-ae4f-e4d9eb1c67a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: parakhj
ms.openlocfilehash: c838fcad21875c4f813159ad78d4c87129a40a86
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-use-the-graph-api"></a><span data-ttu-id="45923-103">Azure AD B2C：使用圖形 API</span><span class="sxs-lookup"><span data-stu-id="45923-103">Azure AD B2C: Use the Graph API</span></span>
<span data-ttu-id="45923-104">Azure Active Directory (Azure AD) B2C 租用戶通常會很龐大。</span><span class="sxs-lookup"><span data-stu-id="45923-104">Azure Active Directory (Azure AD) B2C tenants tend to be very large.</span></span> <span data-ttu-id="45923-105">這表示許多常見的租用戶管理工作需要以程式設計方式執行。</span><span class="sxs-lookup"><span data-stu-id="45923-105">This means that many common tenant management tasks need to be performed programmatically.</span></span> <span data-ttu-id="45923-106">使用者管理是主要範例。</span><span class="sxs-lookup"><span data-stu-id="45923-106">A primary example is user management.</span></span> <span data-ttu-id="45923-107">您可能需要將現有的使用者存放區移轉到 B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="45923-107">You might need to migrate an existing user store to a B2C tenant.</span></span> <span data-ttu-id="45923-108">您希望在自己的頁面上裝載使用者註冊，並在幕後的 Azure AD B2C 目錄中建立使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="45923-108">You may want to host user registration on your own page and create user accounts in your Azure AD B2C directory behind the scenes.</span></span> <span data-ttu-id="45923-109">這類工作需要能夠建立、讀取、更新和刪除使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="45923-109">These types of tasks require the ability to create, read, update, and delete user accounts.</span></span> <span data-ttu-id="45923-110">這些工作都可以透過 Azure AD 圖形 API 達成</span><span class="sxs-lookup"><span data-stu-id="45923-110">You can do these tasks by using the Azure AD Graph API.</span></span>

<span data-ttu-id="45923-111">對於 B2C 租用戶，與圖形 API 通訊有兩種主要模式。</span><span class="sxs-lookup"><span data-stu-id="45923-111">For B2C tenants, there are two primary modes of communicating with the Graph API.</span></span>

* <span data-ttu-id="45923-112">對於互動式、執行一次的工作，您應以 B2C 租用戶中的系統管理員帳戶來執行管理工作。</span><span class="sxs-lookup"><span data-stu-id="45923-112">For interactive, run-once tasks, you should act as an administrator account in the B2C tenant when you perform the tasks.</span></span> <span data-ttu-id="45923-113">此模式需要系統管理員先使用認證登入，系統管理員才能對圖形 API進行任何呼叫。</span><span class="sxs-lookup"><span data-stu-id="45923-113">This mode requires an administrator to sign in with credentials before that admin can perform any calls to the Graph API.</span></span>
* <span data-ttu-id="45923-114">對於自動化、持續的工作，您應使用您提供必要權限的某種服務帳戶來執行管理工作。</span><span class="sxs-lookup"><span data-stu-id="45923-114">For automated, continuous tasks, you should use some type of service account that you provide with the necessary privileges to perform management tasks.</span></span> <span data-ttu-id="45923-115">在 Azure AD 中，作法上您可以註冊應用程式並向 Azure AD 驗證。</span><span class="sxs-lookup"><span data-stu-id="45923-115">In Azure AD, you can do this by registering an application and authenticating to Azure AD.</span></span> <span data-ttu-id="45923-116">使用採用 **OAuth 2.0 用戶端認證授與** 的 [應用程式識別碼](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api)即可完成。</span><span class="sxs-lookup"><span data-stu-id="45923-116">This is done by using an **Application ID** that uses the [OAuth 2.0 client credentials grant](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span></span> <span data-ttu-id="45923-117">在此情況下，應用程式會以本身 (而非使用者的身分) 呼叫圖形 API。</span><span class="sxs-lookup"><span data-stu-id="45923-117">In this case, the application acts as itself, not as a user, to call the Graph API.</span></span>

<span data-ttu-id="45923-118">在本文中，我們將討論如何執行自動化使用案例。</span><span class="sxs-lookup"><span data-stu-id="45923-118">In this article, we'll discuss how to perform the automated-use case.</span></span> <span data-ttu-id="45923-119">為了示範，我們會建置 .NET 4.5 `B2CGraphClient` 來執行使用者建立、讀取、更新和刪除 (CRUD) 作業。</span><span class="sxs-lookup"><span data-stu-id="45923-119">To demonstrate, we'll build a .NET 4.5 `B2CGraphClient` that performs user create, read, update, and delete (CRUD) operations.</span></span> <span data-ttu-id="45923-120">用戶端會有 Windows 命令列介面讓您叫用各種方法。</span><span class="sxs-lookup"><span data-stu-id="45923-120">The client will have a Windows command-line interface (CLI) that allows you to invoke various methods.</span></span> <span data-ttu-id="45923-121">不過，程式碼會撰寫成以非互動、自動化的方式運作。</span><span class="sxs-lookup"><span data-stu-id="45923-121">However, the code is written to behave in a noninteractive, automated fashion.</span></span>

## <a name="get-an-azure-ad-b2c-tenant"></a><span data-ttu-id="45923-122">取得 Azure AD B2C 租用戶</span><span class="sxs-lookup"><span data-stu-id="45923-122">Get an Azure AD B2C tenant</span></span>
<span data-ttu-id="45923-123">您需要一個 Azure AD B2C 租用戶和該租用戶中的全域系統管理員帳戶，才可建立應用程式或使用者，或與 Azure AD 進行互動。</span><span class="sxs-lookup"><span data-stu-id="45923-123">Before you can create applications or users, or interact with Azure AD at all, you will need an Azure AD B2C tenant and a global administrator account in the tenant.</span></span> <span data-ttu-id="45923-124">如果您還沒有租用戶，請參閱 [開始使用 Azure AD B2C](active-directory-b2c-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="45923-124">If you don't have a tenant already, [get started with Azure AD B2C](active-directory-b2c-get-started.md).</span></span>

## <a name="register-your-application-in-your-tenant"></a><span data-ttu-id="45923-125">在您的租用戶中註冊您的應用程式</span><span class="sxs-lookup"><span data-stu-id="45923-125">Register your application in your tenant</span></span>
<span data-ttu-id="45923-126">在您有 B2C 租用戶之後，您需要透過 [Azure 入口網站](https://portal.azure.com)註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="45923-126">After you have a B2C tenant, you need to register your application via the [Azure Portal](https://portal.azure.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="45923-127">若要搭配 B2C 租用戶使用圖形 API，您必須使用 Azure 入口網站中的通用 [應用程式註冊] 刀鋒視窗，註冊專用的應用程式 (**不是** Azure AD B2C 的 [應用程式] 刀鋒視窗)。</span><span class="sxs-lookup"><span data-stu-id="45923-127">To use the Graph API with your B2C tenant, you will need to register a dedicated application by using the generic *App Registrations* blade in the Azure Portal, **NOT** Azure AD B2C's *Applications* blade.</span></span> <span data-ttu-id="45923-128">您不能重複使用您已在 Azure AD B2C 的 [應用程式] 刀鋒視窗中註冊的現有 B2C 應用程式。</span><span class="sxs-lookup"><span data-stu-id="45923-128">You can't reuse the already-existing B2C applications that you registered in the Azure AD B2C's *Applications* blade.</span></span>

1. <span data-ttu-id="45923-129">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="45923-129">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="45923-130">在頁面右上角選取您的帳戶，以選擇您的 Azure AD B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="45923-130">Choose your Azure AD B2C tenant by selecting your account in the top right corner of the page.</span></span>
3. <span data-ttu-id="45923-131">在左側導覽窗格中，選擇 [更多服務]，按一下 [應用程式註冊]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="45923-131">In the left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="45923-132">遵照提示進行，並建立新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="45923-132">Follow the prompts and create a new application.</span></span> 
    1. <span data-ttu-id="45923-133">選取 [Web 應用程式/API] 作為 [應用程式類型]。</span><span class="sxs-lookup"><span data-stu-id="45923-133">Select **Web App / API** as the Application Type.</span></span>    
    2. <span data-ttu-id="45923-134">提供**任何重新導向 URI** (例如 https://B2CGraphAPI)，因為它在此範例中不重要。</span><span class="sxs-lookup"><span data-stu-id="45923-134">Provide **any redirect URI** (e.g. https://B2CGraphAPI) as it's not relevant for this example.</span></span>  
5. <span data-ttu-id="45923-135">應用程式會立即顯示在應用程式清單中，按一下它以取得 [應用程式識別碼] (也稱為用戶端識別碼)。</span><span class="sxs-lookup"><span data-stu-id="45923-135">The application will now show up in the list of applications, click on it to obtain the **Application ID** (also known as Client ID).</span></span> <span data-ttu-id="45923-136">將它複製下來，稍後一節需要用到。</span><span class="sxs-lookup"><span data-stu-id="45923-136">Copy it as you'll need it in a later section.</span></span>
6. <span data-ttu-id="45923-137">在 [設定] 刀鋒視窗中，按一下 [金鑰]新增金鑰 (也稱為用戶端祕密)。</span><span class="sxs-lookup"><span data-stu-id="45923-137">In the Settings blade, click on **Keys** and add a new key (also known as client secret).</span></span> <span data-ttu-id="45923-138">也將它複製下來，稍後一節會用到。</span><span class="sxs-lookup"><span data-stu-id="45923-138">Also copy it for use in a later section.</span></span>

## <a name="configure-create-read-and-update-permissions-for-your-application"></a><span data-ttu-id="45923-139">設定應用程式的建立、讀取和更新權限</span><span class="sxs-lookup"><span data-stu-id="45923-139">Configure create, read and update permissions for your application</span></span>
<span data-ttu-id="45923-140">現在，您需要設定應用程式，以取得建立、讀取、更新和刪除使用者的所有必要權限。</span><span class="sxs-lookup"><span data-stu-id="45923-140">Now you need to configure your application to get all the required permissions to create, read, update and delete users.</span></span>

1. <span data-ttu-id="45923-141">在 Azure 入口網站的 [應用程式註冊] 刀鋒視窗中繼續，選取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="45923-141">Continuing in the Azure portal's App Registrations blade, select your application.</span></span>
2. <span data-ttu-id="45923-142">在 [設定] 刀鋒視窗中，按一下 [必要權限]。</span><span class="sxs-lookup"><span data-stu-id="45923-142">In the Settings blade, click on **Required permissions**.</span></span>
3. <span data-ttu-id="45923-143">在 [必要權限] 刀鋒視窗中，按一下 [Windows Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="45923-143">In the Required permissions blade, click on **Windows Azure Active Directory**.</span></span>
4. <span data-ttu-id="45923-144">在 [啟用存取] 刀鋒視窗中，從 [應用程式權限]中選取 [讀取和寫入目錄資料] 權限，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="45923-144">In the Enable Access  blade, select the **Read and write directory data** permission from **Application Permissions** and click **Save**.</span></span>
5. <span data-ttu-id="45923-145">最後，回到 [必要權限] 刀鋒視窗，按一下 [授與權限] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="45923-145">Finally, back in the Required permissions blade, click on the **Grant Permissions** button.</span></span>

<span data-ttu-id="45923-146">現在，您的應用程式具有從 B2C 租用戶建立、讀取和更新使用者的權限。</span><span class="sxs-lookup"><span data-stu-id="45923-146">You now have an application that has permission to create, read and update users from your B2C tenant.</span></span>

## <a name="configure-delete-permissions-for-your-application"></a><span data-ttu-id="45923-147">設定應用程式的刪除權限</span><span class="sxs-lookup"><span data-stu-id="45923-147">Configure delete permissions for your application</span></span>
<span data-ttu-id="45923-148">目前，「讀取和寫入目錄資料」權限**不**包含執行任何刪除作業的能力，例如刪除使用者。</span><span class="sxs-lookup"><span data-stu-id="45923-148">Currently, the *Read and write directory data* permission does **NOT** include the ability to do any deletions such as deleting users.</span></span> <span data-ttu-id="45923-149">如果希望應用程式有能力刪除使用者，您必須執行下列額外步驟 (需要使用 PowerShell)，否則可以跳到下一節。</span><span class="sxs-lookup"><span data-stu-id="45923-149">If you want to give your application the ability to delete users, you'll need to do these extra steps that involve PowerShell, otherwise, you can skip to the next section.</span></span>

<span data-ttu-id="45923-150">首先，下載並安裝 [Microsoft Online Services 登入小幫手](http://go.microsoft.com/fwlink/?LinkID=286152)。</span><span class="sxs-lookup"><span data-stu-id="45923-150">First, download and install the [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span> <span data-ttu-id="45923-151">接著下載並安裝 [適用於 Windows PowerShell 的 64 位元 Azure Active Directory 模組](http://go.microsoft.com/fwlink/p/?linkid=236297)。</span><span class="sxs-lookup"><span data-stu-id="45923-151">Then download and install the [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>

<span data-ttu-id="45923-152">安裝 Powershell 模組之後，請開啟 Powershell 並連線到 B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="45923-152">After you install the PowerShell module, open PowerShell and connect to your B2C tenant.</span></span> <span data-ttu-id="45923-153">執行 `Get-Credential` 之後，系統將提示您輸入使用者名稱和密碼。請輸入 B2C 租用戶系統管理員帳戶的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="45923-153">After you run `Get-Credential`, you will be prompted for a user name and password, Enter the user name and password of your B2C tenant administrator account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="45923-154">您必須使用 B2C 租用戶**本機**的 B2C 租用戶系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="45923-154">You need to use a B2C tenant administrator account that is **local** to the B2C tenant.</span></span> <span data-ttu-id="45923-155">這些帳戶看起來像這樣︰myusername@myb2ctenant.onmicrosoft.com。</span><span class="sxs-lookup"><span data-stu-id="45923-155">These accounts look like this: myusername@myb2ctenant.onmicrosoft.com.</span></span>

```powershell
Connect-MsolService
```

<span data-ttu-id="45923-156">現在，我們將於下列指令碼中使用**應用程式識別碼**，將使用者帳戶管理員角色指派給應用程式，讓它能夠刪除使用者。</span><span class="sxs-lookup"><span data-stu-id="45923-156">Now we'll use the **Application ID** in the script below to assign the application the user account administrator role which will allow it to delete users.</span></span> <span data-ttu-id="45923-157">這些角色具有已知的識別項，您只需要在下列指令碼中輸入您的**應用程式識別碼**即可。</span><span class="sxs-lookup"><span data-stu-id="45923-157">These roles have well-known identifiers, so all you need to do is input your **Application ID** in the script below.</span></span>

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

<span data-ttu-id="45923-158">您的應用程式現在也具有從 B2C 租用戶刪除使用者的權限。</span><span class="sxs-lookup"><span data-stu-id="45923-158">Your application now also has permissions to delete users from your B2C tenant.</span></span>

## <a name="download-configure-and-build-the-sample-code"></a><span data-ttu-id="45923-159">下載、設定和建置範例程式碼</span><span class="sxs-lookup"><span data-stu-id="45923-159">Download, configure, and build the sample code</span></span>
<span data-ttu-id="45923-160">首先，下載範例程式碼並開始執行。</span><span class="sxs-lookup"><span data-stu-id="45923-160">First, download the sample code and get it running.</span></span> <span data-ttu-id="45923-161">然後我們會仔細查看。</span><span class="sxs-lookup"><span data-stu-id="45923-161">Then we will take a closer look at it.</span></span>  <span data-ttu-id="45923-162">您可以 [將範例程式碼下載為 .zip 檔案](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip)。</span><span class="sxs-lookup"><span data-stu-id="45923-162">You can [download the sample code as a .zip file](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span></span> <span data-ttu-id="45923-163">您可以將此檔案複製到您選擇的目錄中：</span><span class="sxs-lookup"><span data-stu-id="45923-163">You can also clone it into a directory of your choice:</span></span>

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

<span data-ttu-id="45923-164">在 Visual Studio 中開啟 `B2CGraphClient\B2CGraphClient.sln` Visual Studio 方案。</span><span class="sxs-lookup"><span data-stu-id="45923-164">Open the `B2CGraphClient\B2CGraphClient.sln` Visual Studio solution in Visual Studio.</span></span> <span data-ttu-id="45923-165">在 `B2CGraphClient` 專案中，開啟 `App.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="45923-165">In the `B2CGraphClient` project, open the file `App.config`.</span></span> <span data-ttu-id="45923-166">使用您自己的值取代三個應用程式設定：</span><span class="sxs-lookup"><span data-stu-id="45923-166">Replace the three app settings with your own values:</span></span>

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{The ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{The Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="45923-167">接下來，以滑鼠右鍵按一下 `B2CGraphClient` 方案並重建範例。</span><span class="sxs-lookup"><span data-stu-id="45923-167">Next, right-click on the `B2CGraphClient` solution and rebuild the sample.</span></span> <span data-ttu-id="45923-168">如果成功，您現在應該有一個 `B2C.exe` 可執行檔位於 `B2CGraphClient\bin\Debug`。</span><span class="sxs-lookup"><span data-stu-id="45923-168">If you are successful, you should now have a `B2C.exe` executable file located in `B2CGraphClient\bin\Debug`.</span></span>

## <a name="build-user-crud-operations-by-using-the-graph-api"></a><span data-ttu-id="45923-169">使用圖形 API 來建置使用者 CRUD 作業</span><span class="sxs-lookup"><span data-stu-id="45923-169">Build user CRUD operations by using the Graph API</span></span>
<span data-ttu-id="45923-170">若要使用 B2CGraphClient，請開啟 `cmd` Windows 命令提示字元，將您的目錄變更為 `Debug` 目錄。</span><span class="sxs-lookup"><span data-stu-id="45923-170">To use the B2CGraphClient, open a `cmd` Windows command prompt and change your directory to the `Debug` directory.</span></span> <span data-ttu-id="45923-171">然後執行 `B2C Help` 命令。</span><span class="sxs-lookup"><span data-stu-id="45923-171">Then run the `B2C Help` command.</span></span>

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

<span data-ttu-id="45923-172">這會顯示每個命令的簡短描述。</span><span class="sxs-lookup"><span data-stu-id="45923-172">This will display a brief description of each command.</span></span> <span data-ttu-id="45923-173">您每次叫用上述其中一個命令時， `B2CGraphClient` 會對 Azure AD 圖形 API 發出要求。</span><span class="sxs-lookup"><span data-stu-id="45923-173">Each time you invoke one of these commands, `B2CGraphClient` makes a request to the Azure AD Graph API.</span></span>

### <a name="get-an-access-token"></a><span data-ttu-id="45923-174">取得存取權杖</span><span class="sxs-lookup"><span data-stu-id="45923-174">Get an access token</span></span>
<span data-ttu-id="45923-175">對圖形 API 發出任何要求時，需要有存取權杖進行驗證。</span><span class="sxs-lookup"><span data-stu-id="45923-175">Any request to the Graph API requires an access token for authentication.</span></span> <span data-ttu-id="45923-176">`B2CGraphClient` 會使用開放原始碼 Active Directory 驗證程式庫 (ADAL) 來協助取得存取權杖。</span><span class="sxs-lookup"><span data-stu-id="45923-176">`B2CGraphClient` uses the open-source Active Directory Authentication Library (ADAL) to help acquire access tokens.</span></span> <span data-ttu-id="45923-177">ADAL 提供簡單的 API 並處理一些重要的細節，例如快取存取權杖，可讓您輕鬆取得權杖。</span><span class="sxs-lookup"><span data-stu-id="45923-177">ADAL makes token acquisition easier by providing a simple API and taking care of some important details, such as caching access tokens.</span></span> <span data-ttu-id="45923-178">不過，您不必使用 ADAL 來取得權杖。</span><span class="sxs-lookup"><span data-stu-id="45923-178">You don't have to use ADAL to get tokens, though.</span></span> <span data-ttu-id="45923-179">您也可以藉由製作 HTTP 要求來取得權杖。</span><span class="sxs-lookup"><span data-stu-id="45923-179">You can also get tokens by crafting HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="45923-180">此程式碼範例會使用 ADAL v2，以便與圖形 API 通訊。</span><span class="sxs-lookup"><span data-stu-id="45923-180">This code sample uses ADAL v2 in order to communicate with the Graph API.</span></span>  <span data-ttu-id="45923-181">您必須使用 ADAL v2 或 v3，才能取得可與 Azure AD 圖形 API 搭配使用的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="45923-181">You must use ADAL v2 or v3 in order to get access tokens which can be used with the Azure AD Graph API.</span></span>
> 
> 

<span data-ttu-id="45923-182">`B2CGraphClient` 執行時會建立 `B2CGraphClient` 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="45923-182">When `B2CGraphClient` runs, it creates an instance of the `B2CGraphClient` class.</span></span> <span data-ttu-id="45923-183">這個類別的建構函式會設定 ADAL 驗證架構：</span><span class="sxs-lookup"><span data-stu-id="45923-183">The constructor for this class sets up an ADAL authentication scaffolding:</span></span>

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // The client_id, client_secret, and tenant are provided in Program.cs, which pulls the values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // The AuthenticationContext is ADAL's primary class, in which you indicate the tenant to use.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // The ClientCredential is where you pass in your client_id and client_secret, which are
    // provided to Azure AD in order to receive an access_token by using the app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

<span data-ttu-id="45923-184">我們將以 `B2C Get-User` 命令為例。</span><span class="sxs-lookup"><span data-stu-id="45923-184">We'll use the `B2C Get-User` command as an example.</span></span> <span data-ttu-id="45923-185">叫用 `B2C Get-User` 而沒有任何其他輸入時，CLI 會呼叫 `B2CGraphClient.GetAllUsers(...)` 方法。</span><span class="sxs-lookup"><span data-stu-id="45923-185">When `B2C Get-User` is invoked without any additional inputs, the CLI calls the `B2CGraphClient.GetAllUsers(...)` method.</span></span> <span data-ttu-id="45923-186">這個方法會呼叫 `B2CGraphClient.SendGraphGetRequest(...)`，後者會送出 HTTP GET 要求給圖形 API。</span><span class="sxs-lookup"><span data-stu-id="45923-186">This method calls `B2CGraphClient.SendGraphGetRequest(...)`, which submits an HTTP GET request to the Graph API.</span></span> <span data-ttu-id="45923-187">在 `B2CGraphClient.SendGraphGetRequest(...)` 傳送 GET 要求之前，它會先使用 ADAL 取得存取權杖：</span><span class="sxs-lookup"><span data-stu-id="45923-187">Before `B2CGraphClient.SendGraphGetRequest(...)` sends the GET request, it first gets an access token by using ADAL:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL to acquire a token by using the app's identity (the credential)
    // The first parameter is the resource we want an access_token for; in this case, the Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

<span data-ttu-id="45923-188">您可以呼叫 ADAL `AuthenticationContext.AcquireToken(...)` 方法，以取得圖形 API 的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="45923-188">You can get an access token for the Graph API by calling the ADAL `AuthenticationContext.AcquireToken(...)` method.</span></span> <span data-ttu-id="45923-189">然後 ADAL 會傳回 `access_token` 表示應用程式的身分識別。</span><span class="sxs-lookup"><span data-stu-id="45923-189">ADAL then returns an `access_token` that represents the application's identity.</span></span>

### <a name="read-users"></a><span data-ttu-id="45923-190">讀取使用者</span><span class="sxs-lookup"><span data-stu-id="45923-190">Read users</span></span>
<span data-ttu-id="45923-191">當您想要從圖形 API 取得使用者清單或取得特定的使用者時，您可以傳送 HTTP `GET` 要求給 `/users` 端點。</span><span class="sxs-lookup"><span data-stu-id="45923-191">When you want to get a list of users or get a particular user from the Graph API, you can send an HTTP `GET` request to the `/users` endpoint.</span></span> <span data-ttu-id="45923-192">要求取得租用戶中所有使用者時，情況如下：</span><span class="sxs-lookup"><span data-stu-id="45923-192">A request for all of the users in a tenant looks like this:</span></span>

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="45923-193">若要查看此要求，請執行：</span><span class="sxs-lookup"><span data-stu-id="45923-193">To see this request, run:</span></span>

 ```
 > B2C Get-User
 ```

<span data-ttu-id="45923-194">有兩個重點值得注意：</span><span class="sxs-lookup"><span data-stu-id="45923-194">There are two important things to note:</span></span>

* <span data-ttu-id="45923-195">透過 ADAL 取得的存取權杖已利用 `Bearer` 配置加入至 `Authorization` 標頭。</span><span class="sxs-lookup"><span data-stu-id="45923-195">The access token acquired via ADAL is added to the `Authorization` header by using the `Bearer` scheme.</span></span>
* <span data-ttu-id="45923-196">對於 B2C 租用戶，您必須使用查詢參數 `api-version=1.6`。</span><span class="sxs-lookup"><span data-stu-id="45923-196">For B2C tenants, you must use the query parameter `api-version=1.6`.</span></span>

<span data-ttu-id="45923-197">這兩個細節都在 `B2CGraphClient.SendGraphGetRequest(...)` 方法中處理：</span><span class="sxs-lookup"><span data-stu-id="45923-197">Both of these details are handled in the `B2CGraphClient.SendGraphGetRequest(...)` method:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure to use the 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append the access token for the Graph API to the Authorization header of the request by using the Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a><span data-ttu-id="45923-198">建立取用者的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="45923-198">Create consumer user accounts</span></span>
<span data-ttu-id="45923-199">在 B2C 租用戶中建立使用者帳戶時，您可以傳送 HTTP `POST` 要求給 `/users` 端點：</span><span class="sxs-lookup"><span data-stu-id="45923-199">When you create user accounts in your B2C tenant, you can send an HTTP `POST` request to the `/users` endpoint:</span></span>

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required to create consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier the user uses to sign in to the account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set to 'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying to the end user
    "mailNickname": "joec",                        // an email alias for the user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set to false
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

<span data-ttu-id="45923-200">此要求中的這些屬性，在建立取用者使用者時，大部分都是必要的屬性。</span><span class="sxs-lookup"><span data-stu-id="45923-200">Most of these properties in this request are required to create consumer users.</span></span> <span data-ttu-id="45923-201">若要深入了解，請按一下[這裡](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser)。</span><span class="sxs-lookup"><span data-stu-id="45923-201">To learn more, click [here](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span></span> <span data-ttu-id="45923-202">請注意，加上 `//` 註解是為了講解，</span><span class="sxs-lookup"><span data-stu-id="45923-202">Note that the `//` comments have been included for illustration.</span></span> <span data-ttu-id="45923-203">請不要放入實際的要求中。</span><span class="sxs-lookup"><span data-stu-id="45923-203">Do not include them in an actual request.</span></span>

<span data-ttu-id="45923-204">若要查看此要求，請執行下列其中一個命令：</span><span class="sxs-lookup"><span data-stu-id="45923-204">To see the request, run one of the following commands:</span></span>

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

<span data-ttu-id="45923-205">`Create-User` 命令會以 .json 檔案做為輸入參數。</span><span class="sxs-lookup"><span data-stu-id="45923-205">The `Create-User` command takes a .json file as an input parameter.</span></span> <span data-ttu-id="45923-206">這包含使用者物件的 JSON 表示法。</span><span class="sxs-lookup"><span data-stu-id="45923-206">This contains a JSON representation of a user object.</span></span> <span data-ttu-id="45923-207">範例程式碼中有兩個範例 .json 檔案：`usertemplate-email.json` 和 `usertemplate-username.json`。</span><span class="sxs-lookup"><span data-stu-id="45923-207">There are two sample .json files in the sample code: `usertemplate-email.json` and `usertemplate-username.json`.</span></span> <span data-ttu-id="45923-208">您可以修改這些檔案以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="45923-208">You can modify these files to suit your needs.</span></span> <span data-ttu-id="45923-209">除了上述必要欄位以外，這些檔案包含一些您可以使用的選擇性欄位。</span><span class="sxs-lookup"><span data-stu-id="45923-209">In addition to the required fields above, several optional fields that you can use are included in these files.</span></span> <span data-ttu-id="45923-210">[Azure AD 圖形 API 實體參考](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity)提供選擇性欄位的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="45923-210">Details on the optional fields can be found in the [Azure AD Graph API entity reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span></span>

<span data-ttu-id="45923-211">您可以在 `B2CGraphClient.SendGraphPostRequest(...)`中看到如何建構 POST 要求。</span><span class="sxs-lookup"><span data-stu-id="45923-211">You can see how the POST request is constructed in `B2CGraphClient.SendGraphPostRequest(...)`.</span></span>

* <span data-ttu-id="45923-212">它會將存取權杖附加至要求的 `Authorization` 標頭。</span><span class="sxs-lookup"><span data-stu-id="45923-212">It attaches an access token to the `Authorization` header of the request.</span></span>
* <span data-ttu-id="45923-213">它會設定 `api-version=1.6`。</span><span class="sxs-lookup"><span data-stu-id="45923-213">It sets `api-version=1.6`.</span></span>
* <span data-ttu-id="45923-214">它會將 JSON 使用者物件加入要求主體中。</span><span class="sxs-lookup"><span data-stu-id="45923-214">It includes the JSON user object in the body of the request.</span></span>

> [!NOTE]
> <span data-ttu-id="45923-215">如果您想要從現有使用者存放區移轉的帳戶密碼強度比[由 Azure AD B2C 強制執行的強式密碼強度](https://msdn.microsoft.com/library/azure/jj943764.aspx)還低，您可以使用 `passwordPolicies` 屬性中的 `DisableStrongPassword` 值來停用強式密碼需求。</span><span class="sxs-lookup"><span data-stu-id="45923-215">If the accounts that you want to migrate from an existing user store has lower password strength than the [strong password strength enforced by Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), you can disable the strong password requirement using the `DisableStrongPassword` value in the `passwordPolicies` property.</span></span> <span data-ttu-id="45923-216">例如，您可以修改上述提供的建立使用者要求，如下所示︰ `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`。</span><span class="sxs-lookup"><span data-stu-id="45923-216">For instance, you can modify the create user request provided above as follows: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span></span>
> 
> 

### <a name="update-consumer-user-accounts"></a><span data-ttu-id="45923-217">更新取用者的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="45923-217">Update consumer user accounts</span></span>
<span data-ttu-id="45923-218">當您更新使用者物件時，此程序類似於您用來建立使用者物件的程序。</span><span class="sxs-lookup"><span data-stu-id="45923-218">When you update user objects, the process is similar to the one you use to create user objects.</span></span> <span data-ttu-id="45923-219">但此程序會使用 HTTP `PATCH` 方法：</span><span class="sxs-lookup"><span data-stu-id="45923-219">But this process uses the HTTP `PATCH` method:</span></span>

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only the user's displayName
}
```

<span data-ttu-id="45923-220">嘗試以新資料更新 JSON 檔案，進而更新使用者。</span><span class="sxs-lookup"><span data-stu-id="45923-220">Try to update a user by updating your JSON files with new data.</span></span> <span data-ttu-id="45923-221">然後您可以使用 `B2CGraphClient` 來執行下列其中一個命令：</span><span class="sxs-lookup"><span data-stu-id="45923-221">You can then use `B2CGraphClient` to run one of these commands:</span></span>

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

<span data-ttu-id="45923-222">如需有關如何傳送此要求的詳細資訊，請檢閱 `B2CGraphClient.SendGraphPatchRequest(...)` 方法。</span><span class="sxs-lookup"><span data-stu-id="45923-222">Inspect the `B2CGraphClient.SendGraphPatchRequest(...)` method for details on how to send this request.</span></span>

### <a name="search-users"></a><span data-ttu-id="45923-223">搜尋使用者</span><span class="sxs-lookup"><span data-stu-id="45923-223">Search users</span></span>
<span data-ttu-id="45923-224">您可以透過數種方式在 B2C 租用戶中搜尋使用者。</span><span class="sxs-lookup"><span data-stu-id="45923-224">You can search for users in your B2C tenant in a couple of ways.</span></span> <span data-ttu-id="45923-225">一個是利用使用者的物件識別碼，另一個則是使用者的登入識別碼 (亦即 `signInNames` 屬性)。</span><span class="sxs-lookup"><span data-stu-id="45923-225">One, using the user's object ID or two, using the user's sign-in identifer (i.e., the `signInNames` property).</span></span>

<span data-ttu-id="45923-226">執行下列其中一個命令來搜尋特定的使用者︰</span><span class="sxs-lookup"><span data-stu-id="45923-226">Run one of the following commands to search for a specific user:</span></span>

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

<span data-ttu-id="45923-227">以下是一些範例︰</span><span class="sxs-lookup"><span data-stu-id="45923-227">Here are a couple of examples:</span></span>

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a><span data-ttu-id="45923-228">刪除使用者</span><span class="sxs-lookup"><span data-stu-id="45923-228">Delete users</span></span>
<span data-ttu-id="45923-229">刪除使用者的程序很簡單。</span><span class="sxs-lookup"><span data-stu-id="45923-229">The process for deleting a user is straightforward.</span></span> <span data-ttu-id="45923-230">使用 HTTP `DELETE` 方法並以正確的物件識別碼建構 URL：</span><span class="sxs-lookup"><span data-stu-id="45923-230">Use the HTTP `DELETE` method and construct the URL with the correct object ID:</span></span>

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="45923-231">若要查看範例，請輸入此命令並檢視主控台印出的 Delete 要求：</span><span class="sxs-lookup"><span data-stu-id="45923-231">To see an example, enter this command and view the delete request that is printed to the console:</span></span>

```
> B2C Delete-User <object-id-of-user>
```

<span data-ttu-id="45923-232">如需有關如何傳送此要求的詳細資訊，請檢閱 `B2CGraphClient.SendGraphDeleteRequest(...)` 方法。</span><span class="sxs-lookup"><span data-stu-id="45923-232">Inspect the `B2CGraphClient.SendGraphDeleteRequest(...)` method for details on how to send this request.</span></span>

<span data-ttu-id="45923-233">除了使用者管理，您還可以使用 Azure AD 圖形 API 執行其他許多動作。</span><span class="sxs-lookup"><span data-stu-id="45923-233">You can perform many other actions with the Azure AD Graph API in addition to user management.</span></span> <span data-ttu-id="45923-234">[Azure AD 圖形 API 參考](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) 會提供每個動作的詳細資訊以及範例要求。</span><span class="sxs-lookup"><span data-stu-id="45923-234">The [Azure AD Graph API reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) provides details on each action, along with sample requests.</span></span>

## <a name="use-custom-attributes"></a><span data-ttu-id="45923-235">使用自訂屬性</span><span class="sxs-lookup"><span data-stu-id="45923-235">Use custom attributes</span></span>
<span data-ttu-id="45923-236">大部分消費者應用程式都需要儲存某種自訂使用者設定檔資訊。</span><span class="sxs-lookup"><span data-stu-id="45923-236">Most consumer applications need to store some type of custom user profile information.</span></span> <span data-ttu-id="45923-237">作法之一是在 B2C 租用戶中定義自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="45923-237">One way you can do this is to define a custom attribute in your B2C tenant.</span></span> <span data-ttu-id="45923-238">然後，您可將該屬性視同使用者物件的任何其他屬性一樣處理。</span><span class="sxs-lookup"><span data-stu-id="45923-238">You can then treat that attribute the same way you treat any other property on a user object.</span></span> <span data-ttu-id="45923-239">該屬性就像登入權杖中的宣告，您可以更新、刪除、查詢、傳送該屬性。</span><span class="sxs-lookup"><span data-stu-id="45923-239">You can update the attribute, delete the attribute, query by the attribute, send the attribute as a claim in sign-in tokens, and more.</span></span>

<span data-ttu-id="45923-240">若要在 B2C 租用戶中定義自訂屬性，請參閱 [B2C 自訂屬性參考](active-directory-b2c-reference-custom-attr.md)。</span><span class="sxs-lookup"><span data-stu-id="45923-240">To define a custom attribute in your B2C tenant, see the [B2C custom attribute reference](active-directory-b2c-reference-custom-attr.md).</span></span>

<span data-ttu-id="45923-241">您可以使用 `B2CGraphClient`來檢視 B2C 租用戶中定義的自訂屬性：</span><span class="sxs-lookup"><span data-stu-id="45923-241">You can view the custom attributes defined in your B2C tenant by using `B2CGraphClient`:</span></span>

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

<span data-ttu-id="45923-242">這些函式的輸出會顯示每個自訂屬性的詳細資料，例如：</span><span class="sxs-lookup"><span data-stu-id="45923-242">The output of these functions reveals the details of each custom attribute, such as:</span></span>

```JSON
{
      "odata.type": "Microsoft.DirectoryServices.ExtensionProperty",
      "objectType": "ExtensionProperty",
      "objectId": "cec6391b-204d-42fe-8f7c-89c2b1964fca",
      "deletionTimestamp": null,
      "appDisplayName": "",
      "name": "extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number",
      "dataType": "Integer",
      "isSyncedFromOnPremises": false,
      "targetObjects": [
        "User"
      ]
}
```

<span data-ttu-id="45923-243">您可以使用完整名稱做為使用者物件的屬性，例如 `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`。</span><span class="sxs-lookup"><span data-stu-id="45923-243">You can use the full name, such as `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, as a property on your user objects.</span></span>  <span data-ttu-id="45923-244">以新的屬性和該屬性的值更新 .json 檔案，然後執行：</span><span class="sxs-lookup"><span data-stu-id="45923-244">Update your .json file with the new property and a value for the property, and then run:</span></span>

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

<span data-ttu-id="45923-245">使用 `B2CGraphClient`，您會有一個服務應用程式可利用程式設計方式來管理 B2C 租用戶使用者。</span><span class="sxs-lookup"><span data-stu-id="45923-245">By using `B2CGraphClient`, you have a service application that can manage your B2C tenant users programmatically.</span></span> <span data-ttu-id="45923-246">`B2CGraphClient` 會使用自己的應用程式身分識別，向 Azure AD 圖形 API 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="45923-246">`B2CGraphClient` uses its own application identity to authenticate to the Azure AD Graph API.</span></span> <span data-ttu-id="45923-247">它也會使用用戶端密碼來取得權杖。</span><span class="sxs-lookup"><span data-stu-id="45923-247">It also acquires tokens by using a client secret.</span></span> <span data-ttu-id="45923-248">將這項功能納入您的應用程式時，請記住 B2C 應用程式的幾個重點：</span><span class="sxs-lookup"><span data-stu-id="45923-248">As you incorporate this functionality into your application, remember a few key points for B2C apps:</span></span>

* <span data-ttu-id="45923-249">您需要將租用戶中的適當權限授與應用程式。</span><span class="sxs-lookup"><span data-stu-id="45923-249">You need to grant the application the proper permissions in the tenant.</span></span>
* <span data-ttu-id="45923-250">現在，您需要使用 ADAL (不是 MSAL) 取得存取權杖。</span><span class="sxs-lookup"><span data-stu-id="45923-250">For now, you need to use ADAL (not MSAL) to get access tokens.</span></span> <span data-ttu-id="45923-251">(也可以直接傳送通訊協定訊息，而不使用程式庫)。</span><span class="sxs-lookup"><span data-stu-id="45923-251">(You can also send protocol messages directly, without using a library.)</span></span>
* <span data-ttu-id="45923-252">當您呼叫圖形 API 時，請使用 `api-version=1.6`。</span><span class="sxs-lookup"><span data-stu-id="45923-252">When you call the Graph API, use `api-version=1.6`.</span></span>
* <span data-ttu-id="45923-253">當建立和更新取用者使用者，有幾個必要的屬性，如上所述。</span><span class="sxs-lookup"><span data-stu-id="45923-253">When you create and update consumer users, a few properties are required, as described above.</span></span>

<span data-ttu-id="45923-254">對於您想要使用圖形 API 在 B2C 租用戶上執行的動作，如有任何問題或要求，請在本文上留言，或在 GitHub 程式碼範例儲存機制中提出問題。</span><span class="sxs-lookup"><span data-stu-id="45923-254">If you have any questions or requests for actions you would like to perform by using the Graph API on your B2C tenant, leave a comment on this article or file an issue in the GitHub code sample repository.</span></span>

