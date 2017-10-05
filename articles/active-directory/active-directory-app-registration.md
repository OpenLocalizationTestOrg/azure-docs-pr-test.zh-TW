---
title: "Azure Active Directory 應用程式註冊 | Microsoft Docs"
description: "本文說明如何使用 Azure 入口網站向 Azure Active Directory 註冊應用程式"
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
ms.openlocfilehash: 2f2817688beb2028fd0bba8522827d87a0097f21
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="register-your-application-with-your-azure-active-directory-tenant"></a><span data-ttu-id="16827-103">向 Azure Active Directory 租用戶註冊您的應用程式</span><span class="sxs-lookup"><span data-stu-id="16827-103">Register your application with your Azure Active Directory tenant</span></span>

<span data-ttu-id="16827-104">您可以使用 Azure 入口網站向 Azure Active Directory (Azure AD) 租用戶註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="16827-104">You can use the Azure portal to register your application with your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="16827-105">這會為應用程式建立應用程式識別碼，並加以啟用以接收權杖。</span><span class="sxs-lookup"><span data-stu-id="16827-105">This creates an Application ID for the application, and enables it to receive tokens.</span></span>

1. <span data-ttu-id="16827-106">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="16827-106">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="16827-107">在頁面右上角選取您的帳戶，以選擇您的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="16827-107">Choose your Azure AD tenant by selecting your account in the top right corner of the page.</span></span>
3. <span data-ttu-id="16827-108">在左側導覽窗格中，選擇 [更多服務]，按一下 [應用程式註冊]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="16827-108">In the left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="16827-109">遵照提示進行，並建立新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="16827-109">Follow the prompts and create a new application.</span></span> <span data-ttu-id="16827-110">如果您想要 Web 應用程式或原生應用程式的特定範例，請查看我們的[快速入門](active-directory-developers-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="16827-110">If you'd like specific examples for web applications or native applications, check out our [quickstarts](active-directory-developers-guide.md).</span></span>
  * <span data-ttu-id="16827-111">若為 Web 應用程式，請提供屬於應用程式基礎 URL 的**登入 URL**以供使用者登入，例如 `http://localhost:12345`。</span><span class="sxs-lookup"><span data-stu-id="16827-111">For Web Applications, provide the **Sign-On URL**, which is the base URL of your app, where users can sign in e.g `http://localhost:12345`.</span></span>
<!--TODO: add once App ID URI is configurable: The **App ID URI** is a unique identifier for your application. The convention is to use `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * <span data-ttu-id="16827-112">若為原生應用程式，請提供 [重新導向 URI]，以供 Azure AD 用來傳回權杖回應。</span><span class="sxs-lookup"><span data-stu-id="16827-112">For Native Applications, provide a **Redirect URI**, which Azure AD uses to return token responses.</span></span> <span data-ttu-id="16827-113">輸入應用程式特定的值，例如 `http://MyFirstAADApp`</span><span class="sxs-lookup"><span data-stu-id="16827-113">Enter a value specific to your application, .e.g `http://MyFirstAADApp`</span></span>
5. <span data-ttu-id="16827-114">完成註冊後，Azure AD 會為您的應用程式指派一個唯一用戶端識別碼 (應用程式識別碼)。</span><span class="sxs-lookup"><span data-stu-id="16827-114">Once you've completed registration, Azure AD assigns your application a unique client identifier, the Application ID.</span></span>

## <a name="update-application-settings-from-the-azure-portal"></a><span data-ttu-id="16827-115">從 Azure 入口網站更新應用程式設定</span><span class="sxs-lookup"><span data-stu-id="16827-115">Update application settings from the Azure portal</span></span>

<span data-ttu-id="16827-116">您可以使用 Azure 入口網站，輕鬆地修改現有應用程式的設定。</span><span class="sxs-lookup"><span data-stu-id="16827-116">You can easily modify an existing application's settings using the Azure portal.</span></span> <span data-ttu-id="16827-117">例如，您可以設定回覆 URL，也就是 Azure AD 發出權杖回應的位置。</span><span class="sxs-lookup"><span data-stu-id="16827-117">For example, you may want to configure a reply URL, which is where Azure AD issues token responses.</span></span> <span data-ttu-id="16827-118">您也可以設定其他應用程式的權限，例如允許您的應用程式存取 Microsoft 圖形 API。</span><span class="sxs-lookup"><span data-stu-id="16827-118">You may also want to configure permissions to other applications, for instance to allow your application to access the Microsoft Graph API.</span></span> <span data-ttu-id="16827-119">您可以透過應用程式設定頁面來執行這一切。</span><span class="sxs-lookup"><span data-stu-id="16827-119">You can do all this through the application settings page.</span></span>

1. <span data-ttu-id="16827-120">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="16827-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="16827-121">在頁面右上角選取您的帳戶，以選擇您的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="16827-121">Choose your Azure AD tenant by selecting your account in the top right corner of the page.</span></span>
3. <span data-ttu-id="16827-122">在左側導覽窗格中，選擇 [更多服務]，按一下 [應用程式註冊]，然後從清單中選取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="16827-122">In the left-hand navigation pane, choose **More Services**, click **App Registrations**, and choose your application from the list.</span></span>
4. <span data-ttu-id="16827-123">按一下 [設定] 以開啟應用程式的設定頁面。</span><span class="sxs-lookup"><span data-stu-id="16827-123">Click **Settings** to open up the settings page for the application.</span></span>
  * <span data-ttu-id="16827-124">[屬性] 頁面可讓您修改應用程式的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="16827-124">The **Properties** page lets you modify the general information for the application.</span></span> <span data-ttu-id="16827-125">這包括應用程式名稱、登入 URL 以及登出 URL。</span><span class="sxs-lookup"><span data-stu-id="16827-125">This includes the application name, the sign-on URL, and the logout URL.</span></span>
  * <span data-ttu-id="16827-126">[回覆 URL] 頁面可讓您新增回覆 URL，也就是 Azure AD 傳送權杖回應的位置。</span><span class="sxs-lookup"><span data-stu-id="16827-126">The **Reply URLs** page allows you to add a reply URL, which is where Azure AD sends token responses.</span></span>
  * <span data-ttu-id="16827-127">[擁有者] 頁面可讓您新增應用程式擁有者。</span><span class="sxs-lookup"><span data-stu-id="16827-127">The **Owners** page allows you to add application owners.</span></span>
  * <span data-ttu-id="16827-128">[權限] 頁面可讓您設定應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="16827-128">The **Permissions** page allows you to configure permissions for the app.</span></span> <span data-ttu-id="16827-129">例如，若要存取 Microsoft 圖形 API，請按一下 [新增] 並在 API 選取器中選取 [Microsoft Graph]，然後選擇所需的權限，例如 [讀取目錄資料]。</span><span class="sxs-lookup"><span data-stu-id="16827-129">For example, to access the Microsoft Graph API, click **Add** and select **Microsoft Graph** in the API selector, then choose the permission required, for example **Read Directory Data**.</span></span>
  * <span data-ttu-id="16827-130">[金鑰] 頁面可讓您新增應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="16827-130">The **Keys** page allows you to add application secrets.</span></span> <span data-ttu-id="16827-131">密碼只會在建立後立即顯示一次，請務必加以複製以便進一步使用。</span><span class="sxs-lookup"><span data-stu-id="16827-131">The secret will only be displayed once immediately after creation, so make sure to copy it for further use.</span></span>

## <a name="use-the-inline-manifest-editor"></a><span data-ttu-id="16827-132">使用內嵌資訊清單編輯器</span><span class="sxs-lookup"><span data-stu-id="16827-132">Use the inline manifest editor</span></span>

<span data-ttu-id="16827-133">您可以使用內嵌資訊清單編輯器，修改未在 Azure 入口網站中直接公開的某些應用程式屬性。</span><span class="sxs-lookup"><span data-stu-id="16827-133">You can use the inline manifest editor to modify certain application properties that are not exposed directly in the Azure portal.</span></span> <span data-ttu-id="16827-134">例如，您可以使用它來修改應用程式的應用程式識別碼 URI，或啟用 OAuth2.0 隱含流程，而不是預設授權授與代碼流程。</span><span class="sxs-lookup"><span data-stu-id="16827-134">For example, you can use it to modify the application's App ID URI or to enable the OAuth2.0 implicit flow instead of the default authorization grant code flow.</span></span>

1. <span data-ttu-id="16827-135">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="16827-135">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="16827-136">在頁面右上角選取您的帳戶，以選擇您的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="16827-136">Choose your Azure AD tenant by selecting your account in the top right corner of the page.</span></span>
3. <span data-ttu-id="16827-137">在左側導覽窗格中，選擇 [更多服務]，按一下 [應用程式註冊]，然後從清單中選取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="16827-137">In the left-hand navigation pane, choose **More Services**, click **App Registrations**, and choose your application from the list.</span></span>
4. <span data-ttu-id="16827-138">按一下應用程式頁面中的 [資訊清單]，以開啟內嵌資訊清單編輯器。</span><span class="sxs-lookup"><span data-stu-id="16827-138">Click **Manifest** from the application page to open the inline manifest editor.</span></span>
5. <span data-ttu-id="16827-139">您可以直接變更資訊清單並適時予以儲存。</span><span class="sxs-lookup"><span data-stu-id="16827-139">You can directly make changes to the manifest and save it when you're ready.</span></span> <span data-ttu-id="16827-140">或者，您也可以下載資訊清單以在您喜好的編輯器中開啟，並上傳更新後的資訊清單。</span><span class="sxs-lookup"><span data-stu-id="16827-140">Alternatively, you can download the manifest to open it in your favorite editor and upload the updated manifest.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16827-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="16827-141">Next Steps</span></span>

1. <span data-ttu-id="16827-142">查看[快速入門](active-directory-developers-guide.md)，以取得使用 Azure AD 執行應用程式驗證的詳細逐步解說。</span><span class="sxs-lookup"><span data-stu-id="16827-142">Check out the [Quickstarts](active-directory-developers-guide.md) for detailed walkthroughs of applications performing authentication using Azure AD.</span></span>
2. <span data-ttu-id="16827-143">查看 [GitHub](https://github.com/azure-samples) 中完整的程式碼範例清單。</span><span class="sxs-lookup"><span data-stu-id="16827-143">Check out our full list of code samples in [GitHub](https://github.com/azure-samples).</span></span>
