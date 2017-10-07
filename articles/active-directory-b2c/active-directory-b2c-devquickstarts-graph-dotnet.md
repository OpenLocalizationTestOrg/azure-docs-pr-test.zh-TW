---
title: "Azure Active Directory B2C： 使用 hello Graph API |Microsoft 文件"
description: "如何 toocall hello Graph API B2C 租用戶使用應用程式識別 tooautomate hello 程序。"
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
ms.openlocfilehash: a17cdc4adf57dbf22592d99ef8ecde41652763fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-use-hello-graph-api"></a><span data-ttu-id="92f13-103">Azure AD B2C： 使用 hello Graph API</span><span class="sxs-lookup"><span data-stu-id="92f13-103">Azure AD B2C: Use hello Graph API</span></span>
<span data-ttu-id="92f13-104">Azure Active Directory (Azure AD) B2C 租用戶通常 toobe 的非常大。</span><span class="sxs-lookup"><span data-stu-id="92f13-104">Azure Active Directory (Azure AD) B2C tenants tend toobe very large.</span></span> <span data-ttu-id="92f13-105">這表示許多常見的租用戶管理工作需要 toobe 以程式設計方式執行。</span><span class="sxs-lookup"><span data-stu-id="92f13-105">This means that many common tenant management tasks need toobe performed programmatically.</span></span> <span data-ttu-id="92f13-106">使用者管理是主要範例。</span><span class="sxs-lookup"><span data-stu-id="92f13-106">A primary example is user management.</span></span> <span data-ttu-id="92f13-107">您可能需要 toomigrate 現有使用者存放區 tooa B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="92f13-107">You might need toomigrate an existing user store tooa B2C tenant.</span></span> <span data-ttu-id="92f13-108">您可能想 toohost 使用者註冊您自己的頁面上，並在您的 Azure AD B2C 目錄 hello 幕後建立使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="92f13-108">You may want toohost user registration on your own page and create user accounts in your Azure AD B2C directory behind hello scenes.</span></span> <span data-ttu-id="92f13-109">這類工作需要 hello 能力 toocreate、 讀取、 更新及刪除使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="92f13-109">These types of tasks require hello ability toocreate, read, update, and delete user accounts.</span></span> <span data-ttu-id="92f13-110">您可以利用 hello Azure AD Graph API 來完成這些工作。</span><span class="sxs-lookup"><span data-stu-id="92f13-110">You can do these tasks by using hello Azure AD Graph API.</span></span>

<span data-ttu-id="92f13-111">B2C 租用戶，有兩個主要模式與 hello Graph API 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="92f13-111">For B2C tenants, there are two primary modes of communicating with hello Graph API.</span></span>

* <span data-ttu-id="92f13-112">互動、 執行一次的工作，您應該執行 hello 工作時做為在 hello B2C 租用戶系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="92f13-112">For interactive, run-once tasks, you should act as an administrator account in hello B2C tenant when you perform hello tasks.</span></span> <span data-ttu-id="92f13-113">這個模式需要使用認證管理員 toosign 系統管理員才能執行任何呼叫 toohello Graph API。</span><span class="sxs-lookup"><span data-stu-id="92f13-113">This mode requires an administrator toosign in with credentials before that admin can perform any calls toohello Graph API.</span></span>
* <span data-ttu-id="92f13-114">自動化、 連續工作，您應該使用某種類型的服務帳戶，您提供 hello 必要的權限 tooperform 管理工作。</span><span class="sxs-lookup"><span data-stu-id="92f13-114">For automated, continuous tasks, you should use some type of service account that you provide with hello necessary privileges tooperform management tasks.</span></span> <span data-ttu-id="92f13-115">在 Azure AD 中，您可以透過登錄應用程式和驗證 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="92f13-115">In Azure AD, you can do this by registering an application and authenticating tooAzure AD.</span></span> <span data-ttu-id="92f13-116">這是使用**應用程式識別碼**使用 hello [OAuth 2.0 用戶端認證授與](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api)。</span><span class="sxs-lookup"><span data-stu-id="92f13-116">This is done by using an **Application ID** that uses hello [OAuth 2.0 client credentials grant](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span></span> <span data-ttu-id="92f13-117">在此情況下，hello 應用程式做為本身，不做為使用者，toocall hello Graph API。</span><span class="sxs-lookup"><span data-stu-id="92f13-117">In this case, hello application acts as itself, not as a user, toocall hello Graph API.</span></span>

<span data-ttu-id="92f13-118">在本文中，我們將討論如何 tooperform hello 自動化使用案例。</span><span class="sxs-lookup"><span data-stu-id="92f13-118">In this article, we'll discuss how tooperform hello automated-use case.</span></span> <span data-ttu-id="92f13-119">toodemonstrate，我們會建置.NET 4.5`B2CGraphClient`它不會執行使用者建立、 讀取、 更新和刪除 (CRUD) 作業。</span><span class="sxs-lookup"><span data-stu-id="92f13-119">toodemonstrate, we'll build a .NET 4.5 `B2CGraphClient` that performs user create, read, update, and delete (CRUD) operations.</span></span> <span data-ttu-id="92f13-120">hello 用戶端將會有 Windows 命令列介面 (CLI)，可讓您 tooinvoke 各種方法。</span><span class="sxs-lookup"><span data-stu-id="92f13-120">hello client will have a Windows command-line interface (CLI) that allows you tooinvoke various methods.</span></span> <span data-ttu-id="92f13-121">不過，hello 程式碼會以非互動式、 自動化的方式寫入 toobehave。</span><span class="sxs-lookup"><span data-stu-id="92f13-121">However, hello code is written toobehave in a noninteractive, automated fashion.</span></span>

## <a name="get-an-azure-ad-b2c-tenant"></a><span data-ttu-id="92f13-122">取得 Azure AD B2C 租用戶</span><span class="sxs-lookup"><span data-stu-id="92f13-122">Get an Azure AD B2C tenant</span></span>
<span data-ttu-id="92f13-123">您可以建立應用程式或使用者，或完全與 Azure AD 互動之前，您將需要 Azure AD B2C 租用戶和 hello 租用戶中的全域管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="92f13-123">Before you can create applications or users, or interact with Azure AD at all, you will need an Azure AD B2C tenant and a global administrator account in hello tenant.</span></span> <span data-ttu-id="92f13-124">如果您還沒有租用戶，請參閱 [開始使用 Azure AD B2C](active-directory-b2c-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="92f13-124">If you don't have a tenant already, [get started with Azure AD B2C](active-directory-b2c-get-started.md).</span></span>

## <a name="register-your-application-in-your-tenant"></a><span data-ttu-id="92f13-125">在您的租用戶中註冊您的應用程式</span><span class="sxs-lookup"><span data-stu-id="92f13-125">Register your application in your tenant</span></span>
<span data-ttu-id="92f13-126">B2C 租用戶之後，您需要 tooregister 應用程式透過 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="92f13-126">After you have a B2C tenant, you need tooregister your application via hello [Azure Portal](https://portal.azure.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="92f13-127">toouse hello 與 B2C 租用戶的 Graph API，您將需要 tooregister 專用的應用程式使用 hello 泛型*應用程式註冊*hello Azure 入口網站中，在刀鋒視窗**不**Azure AD B2C 的*應用程式*刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="92f13-127">toouse hello Graph API with your B2C tenant, you will need tooregister a dedicated application by using hello generic *App Registrations* blade in hello Azure Portal, **NOT** Azure AD B2C's *Applications* blade.</span></span> <span data-ttu-id="92f13-128">您無法重複使用 hello 現有 B2C 的應用程式註冊，讓您在 Azure AD B2C 的 hello*應用程式*刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="92f13-128">You can't reuse hello already-existing B2C applications that you registered in hello Azure AD B2C's *Applications* blade.</span></span>

1. <span data-ttu-id="92f13-129">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="92f13-129">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="92f13-130">選擇您的 Azure AD B2C 租用戶 hello 右上角的 hello 頁面中選取您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="92f13-130">Choose your Azure AD B2C tenant by selecting your account in hello top right corner of hello page.</span></span>
3. <span data-ttu-id="92f13-131">在 hello 左側導覽窗格中，選擇 **更服務**，按一下**應用程式註冊**，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="92f13-131">In hello left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="92f13-132">依照 hello 提示，並建立新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="92f13-132">Follow hello prompts and create a new application.</span></span> 
    1. <span data-ttu-id="92f13-133">選取**Web 應用程式 / 應用程式開發介面**為 hello 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="92f13-133">Select **Web App / API** as hello Application Type.</span></span>    
    2. <span data-ttu-id="92f13-134">提供**任何重新導向 URI** (例如 https://B2CGraphAPI)，因為它在此範例中不重要。</span><span class="sxs-lookup"><span data-stu-id="92f13-134">Provide **any redirect URI** (e.g. https://B2CGraphAPI) as it's not relevant for this example.</span></span>  
5. <span data-ttu-id="92f13-135">hello 應用程式會立即顯示在 hello 應用程式清單，按一下它 tooobtain hello**應用程式識別碼**（也稱為用戶端識別碼）。</span><span class="sxs-lookup"><span data-stu-id="92f13-135">hello application will now show up in hello list of applications, click on it tooobtain hello **Application ID** (also known as Client ID).</span></span> <span data-ttu-id="92f13-136">將它複製下來，稍後一節需要用到。</span><span class="sxs-lookup"><span data-stu-id="92f13-136">Copy it as you'll need it in a later section.</span></span>
6. <span data-ttu-id="92f13-137">在 hello 設定刀鋒視窗中，按一下**金鑰**並加入新的金鑰 （也稱為用戶端密碼）。</span><span class="sxs-lookup"><span data-stu-id="92f13-137">In hello Settings blade, click on **Keys** and add a new key (also known as client secret).</span></span> <span data-ttu-id="92f13-138">也將它複製下來，稍後一節會用到。</span><span class="sxs-lookup"><span data-stu-id="92f13-138">Also copy it for use in a later section.</span></span>

## <a name="configure-create-read-and-update-permissions-for-your-application"></a><span data-ttu-id="92f13-139">設定應用程式的建立、讀取和更新權限</span><span class="sxs-lookup"><span data-stu-id="92f13-139">Configure create, read and update permissions for your application</span></span>
<span data-ttu-id="92f13-140">現在您需要 tooconfigure 所有 hello 您應用程式 tooget 所需的權限 toocreate、 讀取、 更新和刪除使用者。</span><span class="sxs-lookup"><span data-stu-id="92f13-140">Now you need tooconfigure your application tooget all hello required permissions toocreate, read, update and delete users.</span></span>

1. <span data-ttu-id="92f13-141">繼續在 hello Azure 入口網站應用程式註冊 刀鋒視窗中，選取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="92f13-141">Continuing in hello Azure portal's App Registrations blade, select your application.</span></span>
2. <span data-ttu-id="92f13-142">在 hello 設定刀鋒視窗中，按一下**必要的權限**。</span><span class="sxs-lookup"><span data-stu-id="92f13-142">In hello Settings blade, click on **Required permissions**.</span></span>
3. <span data-ttu-id="92f13-143">在 hello 必要的權限刀鋒視窗中，按一下**Windows Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="92f13-143">In hello Required permissions blade, click on **Windows Azure Active Directory**.</span></span>
4. <span data-ttu-id="92f13-144">在 hello 啟用存取刀鋒視窗中，選取 hello**讀取和寫入目錄資料**權限從**應用程式權限**按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="92f13-144">In hello Enable Access  blade, select hello **Read and write directory data** permission from **Application Permissions** and click **Save**.</span></span>
5. <span data-ttu-id="92f13-145">最後，在 [hello 必要的權限刀鋒視窗中，按一下 hello**授與權限**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="92f13-145">Finally, back in hello Required permissions blade, click on hello **Grant Permissions** button.</span></span>

<span data-ttu-id="92f13-146">現在您已經有具有從 B2C 租用戶的權限 toocreate、 讀取和更新使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="92f13-146">You now have an application that has permission toocreate, read and update users from your B2C tenant.</span></span>

## <a name="configure-delete-permissions-for-your-application"></a><span data-ttu-id="92f13-147">設定應用程式的刪除權限</span><span class="sxs-lookup"><span data-stu-id="92f13-147">Configure delete permissions for your application</span></span>
<span data-ttu-id="92f13-148">目前，hello*讀取和寫入目錄資料*權限未**不**包含 hello 能力 toodo 任何刪除動作，例如刪除使用者。</span><span class="sxs-lookup"><span data-stu-id="92f13-148">Currently, hello *Read and write directory data* permission does **NOT** include hello ability toodo any deletions such as deleting users.</span></span> <span data-ttu-id="92f13-149">如果您想 toogive 您 hello 能力 toodelete 應用程式的使用者，，您還需要 toodo 這些額外的步驟牽涉到 PowerShell 否則您可以略過 toohello 下一節。</span><span class="sxs-lookup"><span data-stu-id="92f13-149">If you want toogive your application hello ability toodelete users, you'll need toodo these extra steps that involve PowerShell, otherwise, you can skip toohello next section.</span></span>

<span data-ttu-id="92f13-150">首先，下載並安裝 hello [Microsoft Online Services 登入小幫手](http://go.microsoft.com/fwlink/?LinkID=286152)。</span><span class="sxs-lookup"><span data-stu-id="92f13-150">First, download and install hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span> <span data-ttu-id="92f13-151">請下載並安裝 hello [64 位元 Windows PowerShell 的 Azure Active Directory 模組](http://go.microsoft.com/fwlink/p/?linkid=236297)。</span><span class="sxs-lookup"><span data-stu-id="92f13-151">Then download and install hello [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>

<span data-ttu-id="92f13-152">安裝 hello PowerShell 模組之後，請開啟 PowerShell，並連接 tooyour B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="92f13-152">After you install hello PowerShell module, open PowerShell and connect tooyour B2C tenant.</span></span> <span data-ttu-id="92f13-153">當您執行`Get-Credential`，系統將提示您的使用者名稱和密碼、 輸入 hello 使用者名稱和 B2C 租用戶系統管理員帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="92f13-153">After you run `Get-Credential`, you will be prompted for a user name and password, Enter hello user name and password of your B2C tenant administrator account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="92f13-154">您必須是 toouse B2C 租用戶系統管理員帳戶**本機**toohello B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="92f13-154">You need toouse a B2C tenant administrator account that is **local** toohello B2C tenant.</span></span> <span data-ttu-id="92f13-155">這些帳戶看起來像這樣︰myusername@myb2ctenant.onmicrosoft.com。</span><span class="sxs-lookup"><span data-stu-id="92f13-155">These accounts look like this: myusername@myb2ctenant.onmicrosoft.com.</span></span>

```powershell
Connect-MsolService
```

<span data-ttu-id="92f13-156">現在我們將使用 hello**應用程式識別碼**hello tooassign hello 應用程式 hello 使用者帳戶系統管理員角色，讓它 toodelete 使用者指令碼中。</span><span class="sxs-lookup"><span data-stu-id="92f13-156">Now we'll use hello **Application ID** in hello script below tooassign hello application hello user account administrator role which will allow it toodelete users.</span></span> <span data-ttu-id="92f13-157">這些角色具有已知的識別項，因此您只需要 toodo 輸入您**應用程式識別碼**hello 以下的指令碼中。</span><span class="sxs-lookup"><span data-stu-id="92f13-157">These roles have well-known identifiers, so all you need toodo is input your **Application ID** in hello script below.</span></span>

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

<span data-ttu-id="92f13-158">您的應用程式現在也有 toodelete 使用者權限從 B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="92f13-158">Your application now also has permissions toodelete users from your B2C tenant.</span></span>

## <a name="download-configure-and-build-hello-sample-code"></a><span data-ttu-id="92f13-159">下載、 設定和建置 hello 範例程式碼</span><span class="sxs-lookup"><span data-stu-id="92f13-159">Download, configure, and build hello sample code</span></span>
<span data-ttu-id="92f13-160">首先，下載 hello 範例程式碼，並加以執行。</span><span class="sxs-lookup"><span data-stu-id="92f13-160">First, download hello sample code and get it running.</span></span> <span data-ttu-id="92f13-161">然後我們會仔細查看。</span><span class="sxs-lookup"><span data-stu-id="92f13-161">Then we will take a closer look at it.</span></span>  <span data-ttu-id="92f13-162">您可以[下載 hello 範例程式碼的.zip 檔](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip)。</span><span class="sxs-lookup"><span data-stu-id="92f13-162">You can [download hello sample code as a .zip file](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span></span> <span data-ttu-id="92f13-163">您可以將此檔案複製到您選擇的目錄中：</span><span class="sxs-lookup"><span data-stu-id="92f13-163">You can also clone it into a directory of your choice:</span></span>

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

<span data-ttu-id="92f13-164">開啟 hello `B2CGraphClient\B2CGraphClient.sln` Visual Studio 中的 Visual Studio 方案。</span><span class="sxs-lookup"><span data-stu-id="92f13-164">Open hello `B2CGraphClient\B2CGraphClient.sln` Visual Studio solution in Visual Studio.</span></span> <span data-ttu-id="92f13-165">在 hello`B2CGraphClient`專案、 開啟 hello 檔案`App.config`。</span><span class="sxs-lookup"><span data-stu-id="92f13-165">In hello `B2CGraphClient` project, open hello file `App.config`.</span></span> <span data-ttu-id="92f13-166">取代您自己的值為 hello 三個應用程式設定：</span><span class="sxs-lookup"><span data-stu-id="92f13-166">Replace hello three app settings with your own values:</span></span>

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{hello ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{hello Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="92f13-167">接下來，以滑鼠右鍵按一下 hello`B2CGraphClient`方案並重建 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="92f13-167">Next, right-click on hello `B2CGraphClient` solution and rebuild hello sample.</span></span> <span data-ttu-id="92f13-168">如果成功，您現在應該有一個 `B2C.exe` 可執行檔位於 `B2CGraphClient\bin\Debug`。</span><span class="sxs-lookup"><span data-stu-id="92f13-168">If you are successful, you should now have a `B2C.exe` executable file located in `B2CGraphClient\bin\Debug`.</span></span>

## <a name="build-user-crud-operations-by-using-hello-graph-api"></a><span data-ttu-id="92f13-169">利用 hello Graph API 來建立使用者 CRUD 作業</span><span class="sxs-lookup"><span data-stu-id="92f13-169">Build user CRUD operations by using hello Graph API</span></span>
<span data-ttu-id="92f13-170">toouse hello B2CGraphClient，開啟`cmd`Windows 命令提示字元並變更目錄 toohello`Debug`目錄。</span><span class="sxs-lookup"><span data-stu-id="92f13-170">toouse hello B2CGraphClient, open a `cmd` Windows command prompt and change your directory toohello `Debug` directory.</span></span> <span data-ttu-id="92f13-171">然後執行 hello`B2C Help`命令。</span><span class="sxs-lookup"><span data-stu-id="92f13-171">Then run hello `B2C Help` command.</span></span>

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

<span data-ttu-id="92f13-172">這會顯示每個命令的簡短描述。</span><span class="sxs-lookup"><span data-stu-id="92f13-172">This will display a brief description of each command.</span></span> <span data-ttu-id="92f13-173">您可以叫用其中一個命令，每次`B2CGraphClient`讓要求 toohello Azure AD Graph API。</span><span class="sxs-lookup"><span data-stu-id="92f13-173">Each time you invoke one of these commands, `B2CGraphClient` makes a request toohello Azure AD Graph API.</span></span>

### <a name="get-an-access-token"></a><span data-ttu-id="92f13-174">取得存取權杖</span><span class="sxs-lookup"><span data-stu-id="92f13-174">Get an access token</span></span>
<span data-ttu-id="92f13-175">任何要求 toohello Graph API 要求存取權杖進行驗證。</span><span class="sxs-lookup"><span data-stu-id="92f13-175">Any request toohello Graph API requires an access token for authentication.</span></span> <span data-ttu-id="92f13-176">`B2CGraphClient`使用 hello 開放原始碼 Active Directory 驗證程式庫 (ADAL) toohelp 取得存取權杖。</span><span class="sxs-lookup"><span data-stu-id="92f13-176">`B2CGraphClient` uses hello open-source Active Directory Authentication Library (ADAL) toohelp acquire access tokens.</span></span> <span data-ttu-id="92f13-177">ADAL 提供簡單的 API 並處理一些重要的細節，例如快取存取權杖，可讓您輕鬆取得權杖。</span><span class="sxs-lookup"><span data-stu-id="92f13-177">ADAL makes token acquisition easier by providing a simple API and taking care of some important details, such as caching access tokens.</span></span> <span data-ttu-id="92f13-178">雖然您不需要 toouse ADAL tooget 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="92f13-178">You don't have toouse ADAL tooget tokens, though.</span></span> <span data-ttu-id="92f13-179">您也可以藉由製作 HTTP 要求來取得權杖。</span><span class="sxs-lookup"><span data-stu-id="92f13-179">You can also get tokens by crafting HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="92f13-180">此程式碼範例會使用 ADAL v2 順序 toocommunicate 以 hello Graph API 中。</span><span class="sxs-lookup"><span data-stu-id="92f13-180">This code sample uses ADAL v2 in order toocommunicate with hello Graph API.</span></span>  <span data-ttu-id="92f13-181">您必須使用 ADAL v2 或 v3，就可以使用 Azure AD Graph API hello 順序 tooget 存取權杖中。</span><span class="sxs-lookup"><span data-stu-id="92f13-181">You must use ADAL v2 or v3 in order tooget access tokens which can be used with hello Azure AD Graph API.</span></span>
> 
> 

<span data-ttu-id="92f13-182">當`B2CGraphClient`執行時，它會建立執行個體的 hello`B2CGraphClient`類別。</span><span class="sxs-lookup"><span data-stu-id="92f13-182">When `B2CGraphClient` runs, it creates an instance of hello `B2CGraphClient` class.</span></span> <span data-ttu-id="92f13-183">這個類別的 hello 建構函式上設定 ADAL 驗證 scaffolding:</span><span class="sxs-lookup"><span data-stu-id="92f13-183">hello constructor for this class sets up an ADAL authentication scaffolding:</span></span>

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // hello client_id, client_secret, and tenant are provided in Program.cs, which pulls hello values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // hello AuthenticationContext is ADAL's primary class, in which you indicate hello tenant toouse.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // hello ClientCredential is where you pass in your client_id and client_secret, which are
    // provided tooAzure AD in order tooreceive an access_token by using hello app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

<span data-ttu-id="92f13-184">我們將使用 hello`B2C Get-User`命令做為範例。</span><span class="sxs-lookup"><span data-stu-id="92f13-184">We'll use hello `B2C Get-User` command as an example.</span></span> <span data-ttu-id="92f13-185">當`B2C Get-User`叫用不含任何其他輸入 hello CLI 呼叫 hello`B2CGraphClient.GetAllUsers(...)`方法。</span><span class="sxs-lookup"><span data-stu-id="92f13-185">When `B2C Get-User` is invoked without any additional inputs, hello CLI calls hello `B2CGraphClient.GetAllUsers(...)` method.</span></span> <span data-ttu-id="92f13-186">這個方法會呼叫`B2CGraphClient.SendGraphGetRequest(...)`，其中送出 HTTP GET 要求 toohello Graph API。</span><span class="sxs-lookup"><span data-stu-id="92f13-186">This method calls `B2CGraphClient.SendGraphGetRequest(...)`, which submits an HTTP GET request toohello Graph API.</span></span> <span data-ttu-id="92f13-187">之前`B2CGraphClient.SendGraphGetRequest(...)`傳送 hello GET 要求，它會先取得存取權杖使用 ADAL:</span><span class="sxs-lookup"><span data-stu-id="92f13-187">Before `B2CGraphClient.SendGraphGetRequest(...)` sends hello GET request, it first gets an access token by using ADAL:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL tooacquire a token by using hello app's identity (hello credential)
    // hello first parameter is hello resource we want an access_token for; in this case, hello Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

<span data-ttu-id="92f13-188">您可以取得存取權杖的 hello Graph API 的呼叫 hello ADAL`AuthenticationContext.AcquireToken(...)`方法。</span><span class="sxs-lookup"><span data-stu-id="92f13-188">You can get an access token for hello Graph API by calling hello ADAL `AuthenticationContext.AcquireToken(...)` method.</span></span> <span data-ttu-id="92f13-189">然後傳回 ADAL`access_token`表示 hello 應用程式的身分識別。</span><span class="sxs-lookup"><span data-stu-id="92f13-189">ADAL then returns an `access_token` that represents hello application's identity.</span></span>

### <a name="read-users"></a><span data-ttu-id="92f13-190">讀取使用者</span><span class="sxs-lookup"><span data-stu-id="92f13-190">Read users</span></span>
<span data-ttu-id="92f13-191">當您想 tooget 的使用者清單，或從 hello Graph API 取得特定的使用者時，您可以傳送 HTTP`GET`要求 toohello`/users`端點。</span><span class="sxs-lookup"><span data-stu-id="92f13-191">When you want tooget a list of users or get a particular user from hello Graph API, you can send an HTTP `GET` request toohello `/users` endpoint.</span></span> <span data-ttu-id="92f13-192">所有租用戶中的 hello 使用者的要求看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="92f13-192">A request for all of hello users in a tenant looks like this:</span></span>

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="92f13-193">toosee 這項要求，執行：</span><span class="sxs-lookup"><span data-stu-id="92f13-193">toosee this request, run:</span></span>

 ```
 > B2C Get-User
 ```

<span data-ttu-id="92f13-194">有兩個重要事項 toonote:</span><span class="sxs-lookup"><span data-stu-id="92f13-194">There are two important things toonote:</span></span>

* <span data-ttu-id="92f13-195">hello 透過 ADAL 取得存取權杖加入 toohello`Authorization`標頭使用 hello`Bearer`配置。</span><span class="sxs-lookup"><span data-stu-id="92f13-195">hello access token acquired via ADAL is added toohello `Authorization` header by using hello `Bearer` scheme.</span></span>
* <span data-ttu-id="92f13-196">B2C 租用戶，您必須使用 hello 查詢參數`api-version=1.6`。</span><span class="sxs-lookup"><span data-stu-id="92f13-196">For B2C tenants, you must use hello query parameter `api-version=1.6`.</span></span>

<span data-ttu-id="92f13-197">這兩個這些詳細資料會在 hello 處理`B2CGraphClient.SendGraphGetRequest(...)`方法：</span><span class="sxs-lookup"><span data-stu-id="92f13-197">Both of these details are handled in hello `B2CGraphClient.SendGraphGetRequest(...)` method:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure toouse hello 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append hello access token for hello Graph API toohello Authorization header of hello request by using hello Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a><span data-ttu-id="92f13-198">建立取用者的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="92f13-198">Create consumer user accounts</span></span>
<span data-ttu-id="92f13-199">當您 B2C 租用戶中建立使用者帳戶時，您可以傳送 HTTP`POST`要求 toohello`/users`端點：</span><span class="sxs-lookup"><span data-stu-id="92f13-199">When you create user accounts in your B2C tenant, you can send an HTTP `POST` request toohello `/users` endpoint:</span></span>

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required toocreate consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier hello user uses toosign in toohello account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set too'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying toohello end user
    "mailNickname": "joec",                        // an email alias for hello user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set toofalse
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

<span data-ttu-id="92f13-200">這個要求中的這些屬性大部分都是必要的 toocreate 取用者的使用者。</span><span class="sxs-lookup"><span data-stu-id="92f13-200">Most of these properties in this request are required toocreate consumer users.</span></span> <span data-ttu-id="92f13-201">詳細資訊，按一下 toolearn[這裡](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser)。</span><span class="sxs-lookup"><span data-stu-id="92f13-201">toolearn more, click [here](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span></span> <span data-ttu-id="92f13-202">請注意該 hello`//`註解已包含如圖例。</span><span class="sxs-lookup"><span data-stu-id="92f13-202">Note that hello `//` comments have been included for illustration.</span></span> <span data-ttu-id="92f13-203">請不要放入實際的要求中。</span><span class="sxs-lookup"><span data-stu-id="92f13-203">Do not include them in an actual request.</span></span>

<span data-ttu-id="92f13-204">toosee hello 要求，執行下列命令的 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="92f13-204">toosee hello request, run one of hello following commands:</span></span>

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

<span data-ttu-id="92f13-205">hello`Create-User`命令會使用做為輸入參數的.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="92f13-205">hello `Create-User` command takes a .json file as an input parameter.</span></span> <span data-ttu-id="92f13-206">這包含使用者物件的 JSON 表示法。</span><span class="sxs-lookup"><span data-stu-id="92f13-206">This contains a JSON representation of a user object.</span></span> <span data-ttu-id="92f13-207">Hello 範例程式碼中有兩個範例.json 檔案：`usertemplate-email.json`和`usertemplate-username.json`。</span><span class="sxs-lookup"><span data-stu-id="92f13-207">There are two sample .json files in hello sample code: `usertemplate-email.json` and `usertemplate-username.json`.</span></span> <span data-ttu-id="92f13-208">您可以修改這些檔案 toosuit 您的需求。</span><span class="sxs-lookup"><span data-stu-id="92f13-208">You can modify these files toosuit your needs.</span></span> <span data-ttu-id="92f13-209">此外 toohello 需要上述欄位，這些檔案中包含數個您可以使用的選擇性欄位。</span><span class="sxs-lookup"><span data-stu-id="92f13-209">In addition toohello required fields above, several optional fields that you can use are included in these files.</span></span> <span data-ttu-id="92f13-210">Hello 選擇性欄位的詳細資訊，請參閱 hello [Azure AD Graph API 實體參考](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity)。</span><span class="sxs-lookup"><span data-stu-id="92f13-210">Details on hello optional fields can be found in hello [Azure AD Graph API entity reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span></span>

<span data-ttu-id="92f13-211">您可以看到 hello POST 要求中的建構方式`B2CGraphClient.SendGraphPostRequest(...)`。</span><span class="sxs-lookup"><span data-stu-id="92f13-211">You can see how hello POST request is constructed in `B2CGraphClient.SendGraphPostRequest(...)`.</span></span>

* <span data-ttu-id="92f13-212">它會將附加存取語彙基元 toohello `Authorization` hello 要求標頭。</span><span class="sxs-lookup"><span data-stu-id="92f13-212">It attaches an access token toohello `Authorization` header of hello request.</span></span>
* <span data-ttu-id="92f13-213">它會設定 `api-version=1.6`。</span><span class="sxs-lookup"><span data-stu-id="92f13-213">It sets `api-version=1.6`.</span></span>
* <span data-ttu-id="92f13-214">在 hello hello 要求主體包含 hello JSON 使用者物件。</span><span class="sxs-lookup"><span data-stu-id="92f13-214">It includes hello JSON user object in hello body of hello request.</span></span>

> [!NOTE]
> <span data-ttu-id="92f13-215">Hello 帳戶如果您想從現有的使用者存放區 toomigrate 具有比 hello 的密碼強度較低[由 Azure AD B2C 強制執行強式密碼強度](https://msdn.microsoft.com/library/azure/jj943764.aspx)，您可以停用使用 hello hello強式密碼需求`DisableStrongPassword`中 hello 值`passwordPolicies`屬性。</span><span class="sxs-lookup"><span data-stu-id="92f13-215">If hello accounts that you want toomigrate from an existing user store has lower password strength than hello [strong password strength enforced by Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), you can disable hello strong password requirement using hello `DisableStrongPassword` value in hello `passwordPolicies` property.</span></span> <span data-ttu-id="92f13-216">比方說，您可以修改 hello 建立，如下所示以上所提供的使用者要求： `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`。</span><span class="sxs-lookup"><span data-stu-id="92f13-216">For instance, you can modify hello create user request provided above as follows: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span></span>
> 
> 

### <a name="update-consumer-user-accounts"></a><span data-ttu-id="92f13-217">更新取用者的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="92f13-217">Update consumer user accounts</span></span>
<span data-ttu-id="92f13-218">當您更新使用者物件時，hello 程序是類似 toohello 使用 toocreate 使用者物件。</span><span class="sxs-lookup"><span data-stu-id="92f13-218">When you update user objects, hello process is similar toohello one you use toocreate user objects.</span></span> <span data-ttu-id="92f13-219">但此程序使用 hello HTTP`PATCH`方法：</span><span class="sxs-lookup"><span data-stu-id="92f13-219">But this process uses hello HTTP `PATCH` method:</span></span>

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only hello user's displayName
}
```

<span data-ttu-id="92f13-220">嘗試 tooupdate 使用者藉由更新您的 JSON 檔案使用新的資料。</span><span class="sxs-lookup"><span data-stu-id="92f13-220">Try tooupdate a user by updating your JSON files with new data.</span></span> <span data-ttu-id="92f13-221">然後您可以使用`B2CGraphClient`toorun 其中一個命令：</span><span class="sxs-lookup"><span data-stu-id="92f13-221">You can then use `B2CGraphClient` toorun one of these commands:</span></span>

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

<span data-ttu-id="92f13-222">檢查 hello`B2CGraphClient.SendGraphPatchRequest(...)`方法的詳細資料 toosend 此要求。</span><span class="sxs-lookup"><span data-stu-id="92f13-222">Inspect hello `B2CGraphClient.SendGraphPatchRequest(...)` method for details on how toosend this request.</span></span>

### <a name="search-users"></a><span data-ttu-id="92f13-223">搜尋使用者</span><span class="sxs-lookup"><span data-stu-id="92f13-223">Search users</span></span>
<span data-ttu-id="92f13-224">您可以透過數種方式在 B2C 租用戶中搜尋使用者。</span><span class="sxs-lookup"><span data-stu-id="92f13-224">You can search for users in your B2C tenant in a couple of ways.</span></span> <span data-ttu-id="92f13-225">一個使用 hello 使用者的物件識別碼或兩個，使用登入識別碼 hello 使用者 (亦即，hello`signInNames`屬性)。</span><span class="sxs-lookup"><span data-stu-id="92f13-225">One, using hello user's object ID or two, using hello user's sign-in identifer (i.e., hello `signInNames` property).</span></span>

<span data-ttu-id="92f13-226">執行下列命令 toosearch 特定使用者的 hello 任一個：</span><span class="sxs-lookup"><span data-stu-id="92f13-226">Run one of hello following commands toosearch for a specific user:</span></span>

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

<span data-ttu-id="92f13-227">以下是一些範例︰</span><span class="sxs-lookup"><span data-stu-id="92f13-227">Here are a couple of examples:</span></span>

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a><span data-ttu-id="92f13-228">刪除使用者</span><span class="sxs-lookup"><span data-stu-id="92f13-228">Delete users</span></span>
<span data-ttu-id="92f13-229">刪除使用者 hello 程序很簡單。</span><span class="sxs-lookup"><span data-stu-id="92f13-229">hello process for deleting a user is straightforward.</span></span> <span data-ttu-id="92f13-230">使用 hello HTTP`DELETE`方法和建構 hello URL 以 hello 更正物件識別碼：</span><span class="sxs-lookup"><span data-stu-id="92f13-230">Use hello HTTP `DELETE` method and construct hello URL with hello correct object ID:</span></span>

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="92f13-231">toosee 範例中，輸入這個命令並檢視 hello 刪除要求所列印的 toohello 主控台：</span><span class="sxs-lookup"><span data-stu-id="92f13-231">toosee an example, enter this command and view hello delete request that is printed toohello console:</span></span>

```
> B2C Delete-User <object-id-of-user>
```

<span data-ttu-id="92f13-232">檢查 hello`B2CGraphClient.SendGraphDeleteRequest(...)`方法的詳細資料 toosend 此要求。</span><span class="sxs-lookup"><span data-stu-id="92f13-232">Inspect hello `B2CGraphClient.SendGraphDeleteRequest(...)` method for details on how toosend this request.</span></span>

<span data-ttu-id="92f13-233">您可以執行許多其他動作以 hello Azure AD Graph API 在加法 toouser 管理。</span><span class="sxs-lookup"><span data-stu-id="92f13-233">You can perform many other actions with hello Azure AD Graph API in addition toouser management.</span></span> <span data-ttu-id="92f13-234">[Azure AD 圖形 API 參考](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) 會提供每個動作的詳細資訊以及範例要求。</span><span class="sxs-lookup"><span data-stu-id="92f13-234">The [Azure AD Graph API reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) provides details on each action, along with sample requests.</span></span>

## <a name="use-custom-attributes"></a><span data-ttu-id="92f13-235">使用自訂屬性</span><span class="sxs-lookup"><span data-stu-id="92f13-235">Use custom attributes</span></span>
<span data-ttu-id="92f13-236">大部分的取用者應用程式需要 toostore 某種類型的自訂使用者設定檔資訊。</span><span class="sxs-lookup"><span data-stu-id="92f13-236">Most consumer applications need toostore some type of custom user profile information.</span></span> <span data-ttu-id="92f13-237">執行這項操作的一個方式是 toodefine B2C 租用戶中的自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="92f13-237">One way you can do this is toodefine a custom attribute in your B2C tenant.</span></span> <span data-ttu-id="92f13-238">然後，您可以將該屬性 hello 相同的方式，您將使用者物件上的任何其他內容。</span><span class="sxs-lookup"><span data-stu-id="92f13-238">You can then treat that attribute hello same way you treat any other property on a user object.</span></span> <span data-ttu-id="92f13-239">您可以更新 hello 屬性刪除 hello 屬性查詢 hello 屬性，在登入語彙基元和多個宣告的形式傳送 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="92f13-239">You can update hello attribute, delete hello attribute, query by hello attribute, send hello attribute as a claim in sign-in tokens, and more.</span></span>

<span data-ttu-id="92f13-240">toodefine B2C 租用戶中的自訂屬性，請參閱 「 hello [B2C 自訂屬性參考](active-directory-b2c-reference-custom-attr.md)。</span><span class="sxs-lookup"><span data-stu-id="92f13-240">toodefine a custom attribute in your B2C tenant, see hello [B2C custom attribute reference](active-directory-b2c-reference-custom-attr.md).</span></span>

<span data-ttu-id="92f13-241">您可以檢視 hello 使用 B2C 租用戶中定義的自訂屬性`B2CGraphClient`:</span><span class="sxs-lookup"><span data-stu-id="92f13-241">You can view hello custom attributes defined in your B2C tenant by using `B2CGraphClient`:</span></span>

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

<span data-ttu-id="92f13-242">這些函式的 hello 輸出會顯示 hello 詳細資料的每個自訂屬性，例如：</span><span class="sxs-lookup"><span data-stu-id="92f13-242">hello output of these functions reveals hello details of each custom attribute, such as:</span></span>

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

<span data-ttu-id="92f13-243">您可以使用完整名稱，例如 hello `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`，為您的使用者物件的屬性。</span><span class="sxs-lookup"><span data-stu-id="92f13-243">You can use hello full name, such as `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, as a property on your user objects.</span></span>  <span data-ttu-id="92f13-244">更新您的.json 檔案 hello 新屬性和 hello 屬性的值，然後執行：</span><span class="sxs-lookup"><span data-stu-id="92f13-244">Update your .json file with hello new property and a value for hello property, and then run:</span></span>

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

<span data-ttu-id="92f13-245">使用 `B2CGraphClient`，您會有一個服務應用程式可利用程式設計方式來管理 B2C 租用戶使用者。</span><span class="sxs-lookup"><span data-stu-id="92f13-245">By using `B2CGraphClient`, you have a service application that can manage your B2C tenant users programmatically.</span></span> <span data-ttu-id="92f13-246">`B2CGraphClient`會使用它自己的應用程式識別 tooauthenticate toohello Azure AD Graph API。</span><span class="sxs-lookup"><span data-stu-id="92f13-246">`B2CGraphClient` uses its own application identity tooauthenticate toohello Azure AD Graph API.</span></span> <span data-ttu-id="92f13-247">它也會使用用戶端密碼來取得權杖。</span><span class="sxs-lookup"><span data-stu-id="92f13-247">It also acquires tokens by using a client secret.</span></span> <span data-ttu-id="92f13-248">將這項功能納入您的應用程式時，請記住 B2C 應用程式的幾個重點：</span><span class="sxs-lookup"><span data-stu-id="92f13-248">As you incorporate this functionality into your application, remember a few key points for B2C apps:</span></span>

* <span data-ttu-id="92f13-249">您需要 toogrant hello 應用程式 hello 適當的權限 hello 租用戶中。</span><span class="sxs-lookup"><span data-stu-id="92f13-249">You need toogrant hello application hello proper permissions in hello tenant.</span></span>
* <span data-ttu-id="92f13-250">現在，您需要將 toouse ADAL (不 MSAL) tooget 存取語彙基元。</span><span class="sxs-lookup"><span data-stu-id="92f13-250">For now, you need toouse ADAL (not MSAL) tooget access tokens.</span></span> <span data-ttu-id="92f13-251">(也可以直接傳送通訊協定訊息，而不使用程式庫)。</span><span class="sxs-lookup"><span data-stu-id="92f13-251">(You can also send protocol messages directly, without using a library.)</span></span>
* <span data-ttu-id="92f13-252">當您呼叫 hello Graph API 時，使用`api-version=1.6`。</span><span class="sxs-lookup"><span data-stu-id="92f13-252">When you call hello Graph API, use `api-version=1.6`.</span></span>
* <span data-ttu-id="92f13-253">當建立和更新取用者使用者，有幾個必要的屬性，如上所述。</span><span class="sxs-lookup"><span data-stu-id="92f13-253">When you create and update consumer users, a few properties are required, as described above.</span></span>

<span data-ttu-id="92f13-254">如果您有任何問題或您想要 tooperform hello Graph API，透過動作的要求您 B2C 租用戶上這篇文章留下註解或 hello GitHub 的程式碼範例儲存機制中提出問題。</span><span class="sxs-lookup"><span data-stu-id="92f13-254">If you have any questions or requests for actions you would like tooperform by using hello Graph API on your B2C tenant, leave a comment on this article or file an issue in hello GitHub code sample repository.</span></span>

