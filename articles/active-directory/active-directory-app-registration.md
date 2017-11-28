---
title: "Active Directory 應用程式註冊 aaaAzure |Microsoft 文件"
description: "本文說明如何 toouse 會 hello Azure 入口網站 tooregister 與 Azure Active Directory 應用程式"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 7dc7b89f-653f-405a-b5f4-2c1288720c15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: priyamo
ms.reviewer: elisol
ms.openlocfilehash: 0134e299dcc53919a6f789a0878a1cf64a8e244d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="register-your-application-with-your-azure-active-directory-tenant"></a><span data-ttu-id="74879-103">向 Azure Active Directory 租用戶註冊您的應用程式</span><span class="sxs-lookup"><span data-stu-id="74879-103">Register your application with your Azure Active Directory tenant</span></span>

<span data-ttu-id="74879-104">您可以使用 Azure 入口網站 tooregister hello 您的應用程式，利用 Azure Active Directory (Azure AD) 租用戶。</span><span class="sxs-lookup"><span data-stu-id="74879-104">You can use hello Azure portal tooregister your application with your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="74879-105">這會建立 hello 應用程式，應用程式識別碼，並讓它 tooreceive 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="74879-105">This creates an Application ID for hello application, and enables it tooreceive tokens.</span></span>

1. <span data-ttu-id="74879-106">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="74879-106">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="74879-107">選擇您的 Azure AD 租用戶 hello 右上角的 hello 頁面中選取您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="74879-107">Choose your Azure AD tenant by selecting your account in hello top right corner of hello page.</span></span>
3. <span data-ttu-id="74879-108">在 hello 左側導覽窗格中，選擇 [**更服務**，按一下**應用程式註冊**，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="74879-108">In hello left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="74879-109">依照 hello 提示，並建立新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="74879-109">Follow hello prompts and create a new application.</span></span> <span data-ttu-id="74879-110">如果您想要 Web 應用程式或原生應用程式的特定範例，請查看我們的[快速入門](active-directory-developers-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="74879-110">If you'd like specific examples for web applications or native applications, check out our [quickstarts](active-directory-developers-guide.md).</span></span>
  * <span data-ttu-id="74879-111">Web 應用程式，提供 hello**登入 URL**，這是應用程式的 hello 基底 URL，使用者可以登入在例如`http://localhost:12345`。</span><span class="sxs-lookup"><span data-stu-id="74879-111">For Web Applications, provide hello **Sign-On URL**, which is hello base URL of your app, where users can sign in e.g `http://localhost:12345`.</span></span>
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * <span data-ttu-id="74879-112">原生應用程式，提供**重新導向 URI**，哪些 Azure AD 使用 tooreturn 權杖回應。</span><span class="sxs-lookup"><span data-stu-id="74879-112">For Native Applications, provide a **Redirect URI**, which Azure AD uses tooreturn token responses.</span></span> <span data-ttu-id="74879-113">輸入值特定 tooyour 應用程式。 例如`http://MyFirstAADApp`</span><span class="sxs-lookup"><span data-stu-id="74879-113">Enter a value specific tooyour application, .e.g `http://MyFirstAADApp`</span></span>
5. <span data-ttu-id="74879-114">當您完成註冊之後時，Azure AD 會指派給您的應用程式的唯一用戶端識別碼，hello 應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="74879-114">Once you've completed registration, Azure AD assigns your application a unique client identifier, hello Application ID.</span></span>

## <a name="update-application-settings-from-hello-azure-portal"></a><span data-ttu-id="74879-115">更新從 hello Azure 入口網站應用程式設定</span><span class="sxs-lookup"><span data-stu-id="74879-115">Update application settings from hello Azure portal</span></span>

<span data-ttu-id="74879-116">您可以輕鬆地修改現有的應用程式的設定，使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="74879-116">You can easily modify an existing application's settings using hello Azure portal.</span></span> <span data-ttu-id="74879-117">例如，您可能想 tooconfigure 回覆 URL，也就是，Azure AD 發出權杖的回應。</span><span class="sxs-lookup"><span data-stu-id="74879-117">For example, you may want tooconfigure a reply URL, which is where Azure AD issues token responses.</span></span> <span data-ttu-id="74879-118">您也可以 tooconfigure 權限 tooother 應用程式，您的應用程式 tooaccess 的執行個體 tooallow hello Microsoft Graph API。</span><span class="sxs-lookup"><span data-stu-id="74879-118">You may also want tooconfigure permissions tooother applications, for instance tooallow your application tooaccess hello Microsoft Graph API.</span></span> <span data-ttu-id="74879-119">您可以執行這所有工作透過 hello 應用程式設定] 頁面。</span><span class="sxs-lookup"><span data-stu-id="74879-119">You can do all this through hello application settings page.</span></span>

1. <span data-ttu-id="74879-120">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="74879-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="74879-121">選擇您的 Azure AD 租用戶 hello 右上角的 hello 頁面中選取您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="74879-121">Choose your Azure AD tenant by selecting your account in hello top right corner of hello page.</span></span>
3. <span data-ttu-id="74879-122">在 hello 左側導覽窗格中，選擇 [**更服務**，按一下**應用程式註冊**，並從 hello 清單中選擇您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="74879-122">In hello left-hand navigation pane, choose **More Services**, click **App Registrations**, and choose your application from hello list.</span></span>
4. <span data-ttu-id="74879-123">按一下**設定**tooopen hello 的 hello 應用程式設定] 頁面上。</span><span class="sxs-lookup"><span data-stu-id="74879-123">Click **Settings** tooopen up hello settings page for hello application.</span></span>
  * <span data-ttu-id="74879-124">hello**屬性**頁面可讓您修改 hello hello 應用程式的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="74879-124">hello **Properties** page lets you modify hello general information for hello application.</span></span> <span data-ttu-id="74879-125">這包括 hello 應用程式名稱、 登入 URL hello 和 hello 登出 URL。</span><span class="sxs-lookup"><span data-stu-id="74879-125">This includes hello application name, hello sign-on URL, and hello logout URL.</span></span>
  * <span data-ttu-id="74879-126">hello**回覆 Url**頁面可讓您 tooadd 回覆 URL，這可能會讓 Azure AD 會傳送權杖回應。</span><span class="sxs-lookup"><span data-stu-id="74879-126">hello **Reply URLs** page allows you tooadd a reply URL, which is where Azure AD sends token responses.</span></span>
  * <span data-ttu-id="74879-127">hello**擁有者**頁面可讓您 tooadd 應用程式擁有者。</span><span class="sxs-lookup"><span data-stu-id="74879-127">hello **Owners** page allows you tooadd application owners.</span></span>
  * <span data-ttu-id="74879-128">hello**權限**頁面可讓您 tooconfigure hello 應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="74879-128">hello **Permissions** page allows you tooconfigure permissions for hello app.</span></span> <span data-ttu-id="74879-129">比方說，tooaccess hello Microsoft Graph API 中，按一下 [**新增**選取**Microsoft Graph** hello API 選取器，然後選擇 hello 例如所需的權限**讀取目錄資料**.</span><span class="sxs-lookup"><span data-stu-id="74879-129">For example, tooaccess hello Microsoft Graph API, click **Add** and select **Microsoft Graph** in hello API selector, then choose hello permission required, for example **Read Directory Data**.</span></span>
  * <span data-ttu-id="74879-130">hello**金鑰**頁面可讓您 tooadd 應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="74879-130">hello **Keys** page allows you tooadd application secrets.</span></span> <span data-ttu-id="74879-131">hello 密碼只會顯示一次之後建立，因此請確定 toocopy 以便進一步使用於它。</span><span class="sxs-lookup"><span data-stu-id="74879-131">hello secret will only be displayed once immediately after creation, so make sure toocopy it for further use.</span></span>

## <a name="use-hello-inline-manifest-editor"></a><span data-ttu-id="74879-132">使用 hello 內嵌資訊清單編輯器</span><span class="sxs-lookup"><span data-stu-id="74879-132">Use hello inline manifest editor</span></span>

<span data-ttu-id="74879-133">您可以使用 hello 內嵌資訊清單編輯器 toomodify 特定應用程式內容不會直接在公開 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="74879-133">You can use hello inline manifest editor toomodify certain application properties that are not exposed directly in hello Azure portal.</span></span> <span data-ttu-id="74879-134">例如，您可以使用它 toomodify hello 應用程式的應用程式識別碼 URI 或 tooenable hello OAuth2.0 隱含流程，而不是 hello 預設授權授與程式碼流程。</span><span class="sxs-lookup"><span data-stu-id="74879-134">For example, you can use it toomodify hello application's App ID URI or tooenable hello OAuth2.0 implicit flow instead of hello default authorization grant code flow.</span></span>

1. <span data-ttu-id="74879-135">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="74879-135">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="74879-136">選擇您的 Azure AD 租用戶 hello 右上角的 hello 頁面中選取您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="74879-136">Choose your Azure AD tenant by selecting your account in hello top right corner of hello page.</span></span>
3. <span data-ttu-id="74879-137">在 hello 左側導覽窗格中，選擇 [**更服務**，按一下**應用程式註冊**，並從 hello 清單中選擇您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="74879-137">In hello left-hand navigation pane, choose **More Services**, click **App Registrations**, and choose your application from hello list.</span></span>
4. <span data-ttu-id="74879-138">按一下**資訊清單**從 hello 應用程式頁面 tooopen hello 內嵌資訊清單編輯器。</span><span class="sxs-lookup"><span data-stu-id="74879-138">Click **Manifest** from hello application page tooopen hello inline manifest editor.</span></span>
5. <span data-ttu-id="74879-139">您可以直接進行變更 toohello 資訊清單，並將它儲存，當您準備好。</span><span class="sxs-lookup"><span data-stu-id="74879-139">You can directly make changes toohello manifest and save it when you're ready.</span></span> <span data-ttu-id="74879-140">或者，您可以下載 hello 資訊清單 tooopen 它在您最愛的編輯器和上傳 hello 更新資訊清單。</span><span class="sxs-lookup"><span data-stu-id="74879-140">Alternatively, you can download hello manifest tooopen it in your favorite editor and upload hello updated manifest.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74879-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="74879-141">Next Steps</span></span>

1. <span data-ttu-id="74879-142">簽出 hello[快速入門](active-directory-developers-guide.md)如需使用 Azure AD 執行驗證的應用程式的詳細逐步解說。</span><span class="sxs-lookup"><span data-stu-id="74879-142">Check out hello [Quickstarts](active-directory-developers-guide.md) for detailed walkthroughs of applications performing authentication using Azure AD.</span></span>
2. <span data-ttu-id="74879-143">查看 [GitHub](https://github.com/azure-samples) 中完整的程式碼範例清單。</span><span class="sxs-lookup"><span data-stu-id="74879-143">Check out our full list of code samples in [GitHub](https://github.com/azure-samples).</span></span>
