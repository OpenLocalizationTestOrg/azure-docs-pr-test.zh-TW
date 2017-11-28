---
title: "Azure Active Directory B2C：應用程式註冊 | Microsoft Docs"
description: "如何 tooregister 您應用程式與 Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: PatAltimore
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f69
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: parakhj
ms.openlocfilehash: bd58e123751db387d6c8f16bd010291ba698b1a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a><span data-ttu-id="de77d-103">Azure Active Directory B2C：註冊您的應用程式</span><span class="sxs-lookup"><span data-stu-id="de77d-103">Azure Active Directory B2C: Register your application</span></span>

<span data-ttu-id="de77d-104">本快速入門協助您在幾分鐘內於 Microsoft Azure Active Directory (Azure AD) B2C 租用戶中註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="de77d-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="de77d-105">當您完成時，使用 hello Azure B2C 租用戶中註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="de77d-105">When you're finished, your application is registered for use in hello Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de77d-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="de77d-106">Prerequisites</span></span>

<span data-ttu-id="de77d-107">toobuild 接受取用者註冊和登入的應用程式，您必須先 tooregister hello 應用程式與 Azure Active Directory B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="de77d-107">toobuild an application that accepts consumer sign-up and sign-in, you first need tooregister hello application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="de77d-108">使用 hello 中所述的步驟，以取得自己的租用戶[建立 Azure AD B2C 租用戶](active-directory-b2c-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="de77d-108">Get your own tenant by using hello steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="de77d-109">從 Azure AD B2C hello 刀鋒視窗 hello Azure 入口網站中建立的應用程式必須從 hello 管理相同的位置。</span><span class="sxs-lookup"><span data-stu-id="de77d-109">Applications created from hello Azure AD B2C blade in hello Azure portal must be managed from hello same location.</span></span> <span data-ttu-id="de77d-110">如果您編輯使用 PowerShell 或另一個入口網站的 hello B2C 應用程式，它們會變成不受支援，無法搭配 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="de77d-110">If you edit hello B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="de77d-111">查看詳細資料中 hello[發生錯誤的應用程式](#faulted-apps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="de77d-111">See details in hello [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-toob2c-settings"></a><span data-ttu-id="de77d-112">瀏覽 tooB2C 設定</span><span class="sxs-lookup"><span data-stu-id="de77d-112">Navigate tooB2C settings</span></span>

<span data-ttu-id="de77d-113">登入 toohello [Azure 入口網站](https://portal.azure.com/)為 hello hello B2C 租用戶的全域管理員。</span><span class="sxs-lookup"><span data-stu-id="de77d-113">Log in toohello [Azure portal](https://portal.azure.com/) as hello Global Administrator of hello B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="de77d-114">選擇 [下一步] 步驟會依據您所註冊的 hello 應用程式類型：</span><span class="sxs-lookup"><span data-stu-id="de77d-114">Choose next steps based on hello application type you are registering:</span></span>

* [<span data-ttu-id="de77d-115">註冊 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="de77d-115">Register a web application</span></span>](#register-a-web-app)
* [<span data-ttu-id="de77d-116">註冊 Web API</span><span class="sxs-lookup"><span data-stu-id="de77d-116">Register a web API</span></span>](#register-a-web-api)
* [<span data-ttu-id="de77d-117">註冊行動或原生應用程式</span><span class="sxs-lookup"><span data-stu-id="de77d-117">Register a mobile or native application</span></span>](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a><span data-ttu-id="de77d-118">註冊 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="de77d-118">Register a web app</span></span>

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

<span data-ttu-id="de77d-119">如果您的 Web 應用程式呼叫 Azure AD B2C 所保護的 Web API，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="de77d-119">If your web application calls a web API secured by Azure AD B2C, perform these steps:</span></span>
   1. <span data-ttu-id="de77d-120">建立應用程式密碼將 toohello**金鑰**刀鋒視窗，然後按一下 hello**產生金鑰** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="de77d-120">Create an application secret by going toohello **Keys** blade and clicking hello **Generate Key** button.</span></span> <span data-ttu-id="de77d-121">請記下 hello**應用程式金鑰**值。</span><span class="sxs-lookup"><span data-stu-id="de77d-121">Make note of hello **App key** value.</span></span> <span data-ttu-id="de77d-122">您可以使用 hello 值做為您的應用程式程式碼中的 hello 應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="de77d-122">You use hello value as hello application secret in your application's code.</span></span>
   2. <span data-ttu-id="de77d-123">按一下 [API 存取][新增] 並選取您的 Web API 和範圍 (權限)。</span><span class="sxs-lookup"><span data-stu-id="de77d-123">Click **API Access**, click **Add**, and select your web API and scopes (permissions).</span></span>

> [!NOTE]
> <span data-ttu-id="de77d-124">**應用程式密鑰** 是重要的安全性認證，應該適當地加以保護。</span><span class="sxs-lookup"><span data-stu-id="de77d-124">An **Application Secret** is an important security credential, and should be secured appropriately.</span></span>
> 

[<span data-ttu-id="de77d-125">跳過**後續步驟**</span><span class="sxs-lookup"><span data-stu-id="de77d-125">Jump too**next steps**</span></span>](#next-steps)

## <a name="register-a-web-api"></a><span data-ttu-id="de77d-126">註冊 Web API</span><span class="sxs-lookup"><span data-stu-id="de77d-126">Register a web API</span></span>

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

<span data-ttu-id="de77d-127">按一下**發行領域**tooadd 更範圍為必要。</span><span class="sxs-lookup"><span data-stu-id="de77d-127">Click **Published scopes** tooadd more scopes as necessary.</span></span> <span data-ttu-id="de77d-128">依預設，會定義 hello"user_impersonation"範圍。</span><span class="sxs-lookup"><span data-stu-id="de77d-128">By default, hello "user_impersonation" scope is defined.</span></span> <span data-ttu-id="de77d-129">hello user_impersonation 範圍可讓其他應用程式 hello 能力 tooaccess 此應用程式開發介面代表 hello 登入的使用者。</span><span class="sxs-lookup"><span data-stu-id="de77d-129">hello user_impersonation scope gives other applications hello ability tooaccess this api on behalf of hello signed-in user.</span></span> <span data-ttu-id="de77d-130">如果您希望，可以移除 hello user_impersonation 範圍。</span><span class="sxs-lookup"><span data-stu-id="de77d-130">If you wish, hello user_impersonation scope can be removed.</span></span>

[<span data-ttu-id="de77d-131">跳過**後續步驟**</span><span class="sxs-lookup"><span data-stu-id="de77d-131">Jump too**next steps**</span></span>](#next-steps)

## <a name="register-a-mobile-or-native-app"></a><span data-ttu-id="de77d-132">註冊行動或原生應用程式</span><span class="sxs-lookup"><span data-stu-id="de77d-132">Register a mobile or native app</span></span>

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[<span data-ttu-id="de77d-133">跳過**後續步驟**</span><span class="sxs-lookup"><span data-stu-id="de77d-133">Jump too**next steps**</span></span>](#next-steps)

## <a name="limitations"></a><span data-ttu-id="de77d-134">限制</span><span class="sxs-lookup"><span data-stu-id="de77d-134">Limitations</span></span>

### <a name="choosing-a-web-app-or-api-reply-url"></a><span data-ttu-id="de77d-135">選擇 Web 應用程式或 API 回覆 URL</span><span class="sxs-lookup"><span data-stu-id="de77d-135">Choosing a web app or api reply URL</span></span>

<span data-ttu-id="de77d-136">目前，會向 Azure AD B2C 的應用程式是有限的限制的 tooa 組回覆 URL 值。</span><span class="sxs-lookup"><span data-stu-id="de77d-136">Currently, apps that are registered with Azure AD B2C are restricted tooa limited set of reply URL values.</span></span> <span data-ttu-id="de77d-137">hello 的回覆的 web 應用程式和服務的 URL 必須以 hello 配置開頭`https`，及所有回覆 URL 值都必須共用單一的 DNS 網域。</span><span class="sxs-lookup"><span data-stu-id="de77d-137">hello reply URL for web apps and services must begin with hello scheme `https`, and all reply URL values must share a single DNS domain.</span></span> <span data-ttu-id="de77d-138">例如，您不能註冊具有下列其中一個回覆 URL 的 Web 應用程式︰</span><span class="sxs-lookup"><span data-stu-id="de77d-138">For example, you cannot register a web app that has one of these reply URLs:</span></span>

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="de77d-139">hello 註冊系統比較 hello 現有回覆 URL toohello DNS 名稱的 hello 回覆 URL，您要加入的 hello 整個 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="de77d-139">hello registration system compares hello whole DNS name of hello existing reply URL toohello DNS name of hello reply URL that you are adding.</span></span> <span data-ttu-id="de77d-140">如果其中一個 hello 下列條件成立，就會失敗 hello 要求 tooadd hello DNS 名稱：</span><span class="sxs-lookup"><span data-stu-id="de77d-140">hello request tooadd hello DNS name fails if either of hello following conditions is true:</span></span>

* <span data-ttu-id="de77d-141">hello 整個 DNS 名稱的新回覆 URL hello 與 hello 現有的回覆 URL hello DNS 名稱不相符。</span><span class="sxs-lookup"><span data-stu-id="de77d-141">hello whole DNS name of hello new reply URL does not match hello DNS name of hello existing reply URL.</span></span>
* <span data-ttu-id="de77d-142">新回覆 URL hello hello 整個 DNS 名稱不是 hello 現有的回覆 URL 的子網域。</span><span class="sxs-lookup"><span data-stu-id="de77d-142">hello whole DNS name of hello new reply URL is not a subdomain of hello existing reply URL.</span></span>

<span data-ttu-id="de77d-143">例如，如果 hello 應用程式會出現此回覆 URL:</span><span class="sxs-lookup"><span data-stu-id="de77d-143">For example, if hello app has this reply URL:</span></span>

`https://login.contoso.com`

<span data-ttu-id="de77d-144">您可以加入 tooit，像這樣：</span><span class="sxs-lookup"><span data-stu-id="de77d-144">You can add tooit, like this:</span></span>

`https://login.contoso.com/new`

<span data-ttu-id="de77d-145">在此情況下，hello DNS 名稱與完全相符。</span><span class="sxs-lookup"><span data-stu-id="de77d-145">In this case, hello DNS name matches exactly.</span></span> <span data-ttu-id="de77d-146">或者，您可以這樣做：</span><span class="sxs-lookup"><span data-stu-id="de77d-146">Or, you can do this:</span></span>

`https://new.login.contoso.com`

<span data-ttu-id="de77d-147">在此情況下，您參照 login.contoso.com tooa DNS 子的網域。如果您想 toohave 已登入： east.contoso.com 與登入-west.contoso.com，如回覆 Url 的應用程式，您必須加入這些回覆 Url 順序如下：</span><span class="sxs-lookup"><span data-stu-id="de77d-147">In this case, you're referring tooa DNS subdomain of login.contoso.com. If you want toohave an app that has login-east.contoso.com and login-west.contoso.com as reply URLs, you must add those reply URLs in this order:</span></span>

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="de77d-148">您可以新增 hello 後面兩個，因為它們是子網域的第一個回覆 URL hello，contoso.com。</span><span class="sxs-lookup"><span data-stu-id="de77d-148">You can add hello latter two because they are subdomains of hello first reply URL, contoso.com.</span></span>

### <a name="choosing-a-native-app-redirect-uri"></a><span data-ttu-id="de77d-149">選擇原生應用程式重新導向 URI</span><span class="sxs-lookup"><span data-stu-id="de77d-149">Choosing a native app redirect URI</span></span>

<span data-ttu-id="de77d-150">選擇行動/原生應用程式的重新導向 URI 時，有兩個重要的考量︰</span><span class="sxs-lookup"><span data-stu-id="de77d-150">There are two important considerations when choosing a redirect URI for mobile/native applications:</span></span>

* <span data-ttu-id="de77d-151">**唯一**: hello 配置 hello 重新導向 URI 應該是唯一的每個應用程式。</span><span class="sxs-lookup"><span data-stu-id="de77d-151">**Unique**: hello scheme of hello redirect URI should be unique for every application.</span></span> <span data-ttu-id="de77d-152">在我們的範例 (com.onmicrosoft.contoso.appname://redirect/path)，我們會使用 com.onmicrosoft.contoso.appname 為 hello 配置。</span><span class="sxs-lookup"><span data-stu-id="de77d-152">In our example (com.onmicrosoft.contoso.appname://redirect/path), we use com.onmicrosoft.contoso.appname as hello scheme.</span></span> <span data-ttu-id="de77d-153">我們建議您遵循此模式。</span><span class="sxs-lookup"><span data-stu-id="de77d-153">We recommend following this pattern.</span></span> <span data-ttu-id="de77d-154">如果兩個應用程式共用 hello 相同配置、 hello 使用者會看到 「 選擇應用程式 」 的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="de77d-154">If two applications share hello same scheme, hello user sees a "choose app" dialog.</span></span> <span data-ttu-id="de77d-155">如果 hello 使用者選擇不正確，hello 登入將會失敗。</span><span class="sxs-lookup"><span data-stu-id="de77d-155">If hello user makes an incorrect choice, hello login fails.</span></span>
* <span data-ttu-id="de77d-156">**完成**︰重新導向 URI 必須有配置和路徑。</span><span class="sxs-lookup"><span data-stu-id="de77d-156">**Complete**: Redirect URI must have a scheme and a path.</span></span> <span data-ttu-id="de77d-157">hello 路徑必須包含至少一個斜線之後 hello 網域 （例如，//contoso/ 運作和 //contoso 失敗）。</span><span class="sxs-lookup"><span data-stu-id="de77d-157">hello path must contain at least one forward slash after hello domain (for example, //contoso/ works and //contoso fails).</span></span>

<span data-ttu-id="de77d-158">請確定沒有任何特殊字元像 hello 中的底線重新導向 uri。</span><span class="sxs-lookup"><span data-stu-id="de77d-158">Ensure there are no special characters like underscores in hello redirect uri.</span></span>

### <a name="faulted-apps"></a><span data-ttu-id="de77d-159">發生錯誤的應用程式</span><span class="sxs-lookup"><span data-stu-id="de77d-159">Faulted apps</span></span>

<span data-ttu-id="de77d-160">下列情況不得編輯 B2C 應用程式：</span><span class="sxs-lookup"><span data-stu-id="de77d-160">B2C applications should NOT be edited:</span></span>

* <span data-ttu-id="de77d-161">在其他應用程式管理入口網站上，例如[Azure 傳統入口網站](https://manage.windowsazure.com/)和[應用程式註冊入口網站](https://apps.dev.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="de77d-161">On other application management portals such as the [Azure classic portal](https://manage.windowsazure.com/) & the [Application Registration Portal](https://apps.dev.microsoft.com/).</span></span>
* <span data-ttu-id="de77d-162">使用圖形 API 或 PowerShell</span><span class="sxs-lookup"><span data-stu-id="de77d-162">Using Graph API or PowerShell</span></span>

<span data-ttu-id="de77d-163">如果您編輯 hello B2C 應用程式，如上面所述，然後再次嘗試 tooedit 再次在 hello Azure AD B2C 功能刀鋒視窗上 hello Azure 入口網站、 它會變成錯誤的應用程式，和您的應用程式就不能再使用 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="de77d-163">If you edit hello B2C application as described above and try tooedit it again in hello Azure AD B2C features blade on hello Azure portal, it becomes a faulted app, and your application is no longer usable with Azure AD B2C.</span></span> <span data-ttu-id="de77d-164">您擁有 toodelete hello 應用程式，並且建立一次。</span><span class="sxs-lookup"><span data-stu-id="de77d-164">You have toodelete hello application and create it again.</span></span>

<span data-ttu-id="de77d-165">toodelete hello 應用程式，請移 toohello[應用程式註冊入口網站](https://apps.dev.microsoft.com/)並刪除那里 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="de77d-165">toodelete hello app, go toohello [Application Registration Portal](https://apps.dev.microsoft.com/) and delete hello application there.</span></span> <span data-ttu-id="de77d-166">為了讓 hello 應用程式 toobe 可見，您需要 toobe hello 的擁有者 hello 應用程式 （和不只是 hello 租用戶的系統管理員）。</span><span class="sxs-lookup"><span data-stu-id="de77d-166">In order for hello application toobe visible, you need toobe hello owner of hello application (and not just an admin of hello tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="de77d-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="de77d-167">Next steps</span></span>

<span data-ttu-id="de77d-168">現在，您已經向 Azure AD B2C 應用程式，您可以完成其中一種[我們的快速入門教學課程](active-directory-b2c-overview.md#get-started)tooget 啟動並執行。</span><span class="sxs-lookup"><span data-stu-id="de77d-168">Now that you have an application registered with Azure AD B2C, you can complete one of [our quick-start tutorials](active-directory-b2c-overview.md#get-started) tooget up and running.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="de77d-169">透過註冊、登入和密碼重設來建立 ASP.NET Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="de77d-169">Create an ASP.NET web app with sign-up, sign-in, and password reset</span></span>](active-directory-b2c-devquickstarts-web-dotnet-susi.md)