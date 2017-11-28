---
title: "在 Azure App Service API 應用程式的 aaaUser 驗證 |Microsoft 文件"
description: "了解 tooprotect 藉由使用 Azure App Service 中的應用程式開發介面應用程式的唯一 tooauthenticated 使用者的存取方式。"
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 3896760d-46ff-4b67-b98a-edd233f24758
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: 4702fc77fcfe736405e22b033c35d22ae3c5a300
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="user-authentication-for-api-apps-in-azure-app-service"></a><span data-ttu-id="0840a-103">Azure App Service 中 API Apps 的使用者驗證</span><span class="sxs-lookup"><span data-stu-id="0840a-103">User authentication for API Apps in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="0840a-104">概觀</span><span class="sxs-lookup"><span data-stu-id="0840a-104">Overview</span></span>
<span data-ttu-id="0840a-105">這篇文章會示範如何 tooprotect 的 Azure API 應用程式，因此只能驗證的使用者可以呼叫它。</span><span class="sxs-lookup"><span data-stu-id="0840a-105">This article shows how tooprotect an Azure API app so that only authenticated users can call it.</span></span> <span data-ttu-id="0840a-106">hello 文章假設您已閱讀 hello [Azure 應用程式服務驗證概觀](../app-service/app-service-authentication-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0840a-106">hello article assumes that you have read hello [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span>

<span data-ttu-id="0840a-107">您將了解：</span><span class="sxs-lookup"><span data-stu-id="0840a-107">You'll learn:</span></span>

* <span data-ttu-id="0840a-108">如何 tooconfigure 驗證提供者，具有 Azure Active Directory (Azure AD) 的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0840a-108">How tooconfigure an authentication provider, with details for Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="0840a-109">Tooconsume 受保護的應用程式開發介面應用程式使用方式 hello [Active Directory 驗證程式庫 (ADAL) for JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js)。</span><span class="sxs-lookup"><span data-stu-id="0840a-109">How tooconsume a protected API app by using hello [Active Directory Authentication Library (ADAL) for JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js).</span></span>

<span data-ttu-id="0840a-110">hello 文章包含兩個區段：</span><span class="sxs-lookup"><span data-stu-id="0840a-110">hello article contains two sections:</span></span>

* <span data-ttu-id="0840a-111">hello[如何 tooconfigure Azure App Service 中的使用者驗證](#authconfig)章節將說明一般方式 tooconfigure 任何 API 應用程式的使用者驗證和同樣適用於支援的應用程式服務，包括.NET、 tooall 架構Node.js 和 Java。</span><span class="sxs-lookup"><span data-stu-id="0840a-111">hello [How tooconfigure user authentication in Azure App Service](#authconfig) section explains in general how tooconfigure user authentication for any API app and applies equally tooall frameworks supported by App Service, including .NET, Node.js, and Java.</span></span>
* <span data-ttu-id="0840a-112">開頭為 hello[繼續 hello.NET API 的應用程式教學課程](#tutorialstart)區段中，hello 您完成設定的.NET 範例應用程式備份結束和 AngularJS 前端使其使用 Azure Active Directory 使用者的文件指南驗證。</span><span class="sxs-lookup"><span data-stu-id="0840a-112">Starting with hello [Continuing hello .NET API Apps tutorials](#tutorialstart) section, hello article guides you through configuring a sample application with a .NET back end and an AngularJS front end so that it uses Azure Active Directory for user authentication.</span></span> 

## <span data-ttu-id="0840a-113"><a id="authconfig"></a>如何在 Azure App Service 中的 tooconfigure 使用者驗證</span><span class="sxs-lookup"><span data-stu-id="0840a-113"><a id="authconfig"></a> How tooconfigure user authentication in Azure App Service</span></span>
<span data-ttu-id="0840a-114">本節提供適用於 tooany API 應用程式的一般指示。</span><span class="sxs-lookup"><span data-stu-id="0840a-114">This section provides general instructions that apply tooany API app.</span></span> <span data-ttu-id="0840a-115">步驟特定 toohello tooDo 清單.NET 範例應用程式，跳過[繼續 hello.NET 使用者入門教學課程](#tutorialstart)。</span><span class="sxs-lookup"><span data-stu-id="0840a-115">For steps specific toohello tooDo List .NET sample application, go too[Continuing hello .NET getting-started tutorials](#tutorialstart).</span></span>

1. <span data-ttu-id="0840a-116">在 hello [Azure 入口網站](https://portal.azure.com/)，瀏覽 toohello**設定**刀鋒視窗中的 hello API 應用程式的 tooprotect，尋找 hello**功能**區段，，然後按一下**驗證 / 授權**。</span><span class="sxs-lookup"><span data-stu-id="0840a-116">In hello [Azure portal](https://portal.azure.com/), navigate toohello **Settings** blade of hello API app that you want tooprotect, find hello **Features** section, and then click **Authentication/ Authorization**.</span></span>
   
    ![Azure 入口網站驗證/授權](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. <span data-ttu-id="0840a-118">在 hello**驗證 / 授權**刀鋒視窗中，按一下 **上**。</span><span class="sxs-lookup"><span data-stu-id="0840a-118">In hello **Authentication / Authorization** blade, click **On**.</span></span>
3. <span data-ttu-id="0840a-119">選取其中一個 hello 選項從 hello**當要求未經驗證的動作 tootake**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="0840a-119">Select one of hello options from hello **Action tootake when request is not authenticated** drop-down list.</span></span>
   
   * <span data-ttu-id="0840a-120">如果您想只驗證的呼叫 tooreach 您 API 應用程式，選擇其中一個 hello**登入...**選項。</span><span class="sxs-lookup"><span data-stu-id="0840a-120">If you want only authenticated calls tooreach your API app, choose one of hello **Log in with ...** options.</span></span> <span data-ttu-id="0840a-121">此選項可讓您 tooprotect hello API 應用程式而不需要撰寫任何程式碼中執行。</span><span class="sxs-lookup"><span data-stu-id="0840a-121">This option enables you tooprotect hello API app without writing any code that runs in it.</span></span>
   * <span data-ttu-id="0840a-122">如果您想要的所有電話 tooreach 您 API 應用程式，選擇**允許要求 （無動作）**。</span><span class="sxs-lookup"><span data-stu-id="0840a-122">If you want all calls tooreach your API app, choose **Allow request (no action)**.</span></span> <span data-ttu-id="0840a-123">您可以使用這個選項 toodirect 未經驗證的呼叫端 tooa 選擇的驗證提供者。</span><span class="sxs-lookup"><span data-stu-id="0840a-123">You can use this option toodirect unauthenticated callers tooa choice of authentication providers.</span></span> <span data-ttu-id="0840a-124">使用此選項時，您會有 toowrite 程式碼 toohandle 授權。</span><span class="sxs-lookup"><span data-stu-id="0840a-124">With this option you have toowrite code toohandle authorization.</span></span>
     
     <span data-ttu-id="0840a-125">如需詳細資訊，請參閱 [Azure App Service 中的 API Apps 驗證與授權](app-service-api-authentication.md#multiple-protection-options)。</span><span class="sxs-lookup"><span data-stu-id="0840a-125">For more information, see [Authentication and authorization for API Apps in Azure App Service](app-service-api-authentication.md#multiple-protection-options).</span></span>
4. <span data-ttu-id="0840a-126">選取一或多個 hello**驗證提供者**。</span><span class="sxs-lookup"><span data-stu-id="0840a-126">Select one or more of hello **Authentication Providers**.</span></span>
   
    <span data-ttu-id="0840a-127">hello 影像顯示的選項需要 Azure AD 驗證的所有呼叫端 toobe。</span><span class="sxs-lookup"><span data-stu-id="0840a-127">hello image shows    choices that require all callers toobe authenticated by Azure AD.</span></span>
   
    ![Azure 入口網站驗證/授權刀鋒視窗](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
   
    <span data-ttu-id="0840a-129">當您選擇的驗證提供者時，hello 入口網站組態刀鋒視窗中顯示該提供者。</span><span class="sxs-lookup"><span data-stu-id="0840a-129">When you choose an authentication provider, hello portal displays a configuration blade for that provider.</span></span> 
   
    <span data-ttu-id="0840a-130">如需詳細指示，說明如何 tooconfigure hello 驗證提供者組態刀鋒視窗，請參閱[如何 tooconfigure 您 App Service 應用程式 toouse 的 Azure Active Directory 登入](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="0840a-130">For detailed instructions that explain how tooconfigure hello authentication provider configuration blades, see [How tooconfigure your App Service application toouse Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span> <span data-ttu-id="0840a-131">（hello 連結是有關在 Azure AD，tooan 發行項，但是本身 hello 文章包含連結的 hello tooarticles 其他驗證提供者的索引標籤）。</span><span class="sxs-lookup"><span data-stu-id="0840a-131">(hello link goes tooan article about Azure AD, but hello article itself contains tabs that link tooarticles for hello other authentication providers.)</span></span>
5. <span data-ttu-id="0840a-132">當您完成 hello 驗證提供者組態刀鋒視窗中時，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="0840a-132">When you're done with hello authentication provider configuration blade, click **OK**.</span></span>
6. <span data-ttu-id="0840a-133">在 hello**驗證 / 授權**刀鋒視窗中，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="0840a-133">In hello **Authentication / Authorization** blade, click **Save**.</span></span>

<span data-ttu-id="0840a-134">完成此動作後，應用程式服務在到達 hello API 應用程式之前，就會驗證所有 API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="0840a-134">When this is done, App Service authenticates all API calls before they reach hello API app.</span></span> <span data-ttu-id="0840a-135">hello 驗證服務的運作 hello 相同的應用程式的服務支援，包括.NET、 Node.js 和 Java 的所有語言。</span><span class="sxs-lookup"><span data-stu-id="0840a-135">hello authentication services work hello same for all languages that App service supports, including .NET, Node.js, and Java.</span></span> 

<span data-ttu-id="0840a-136">toomake 驗證 API 呼叫、 hello 呼叫端 hello 授權標頭的 HTTP 要求中包含 hello 驗證提供者的 OAuth 2.0 承載權杖。</span><span class="sxs-lookup"><span data-stu-id="0840a-136">toomake authenticated API calls, hello caller includes hello authentication provider's OAuth 2.0 bearer token in hello Authorization header of HTTP requests.</span></span> <span data-ttu-id="0840a-137">hello 語彙基元可藉由使用 hello 驗證提供者的 SDK。</span><span class="sxs-lookup"><span data-stu-id="0840a-137">hello token can be acquired by using hello authentication provider's SDK.</span></span>

## <span data-ttu-id="0840a-138"><a id="tutorialstart"></a>繼續 hello.NET API 的應用程式教學課程</span><span class="sxs-lookup"><span data-stu-id="0840a-138"><a id="tutorialstart"></a> Continuing hello .NET API Apps tutorials</span></span>
<span data-ttu-id="0840a-139">如果您要遵照 API 應用程式的 hello Node.js 或 Java 教學課程，請略過 toohello 下一個文件： [API 應用程式的服務主體驗證](app-service-api-dotnet-service-principal-auth.md)。</span><span class="sxs-lookup"><span data-stu-id="0840a-139">If you are following hello Node.js or Java tutorials for API apps, skip toohello next article, [service principal authentication for API apps](app-service-api-dotnet-service-principal-auth.md).</span></span> 

<span data-ttu-id="0840a-140">如果您要遵照 hello.NET 教學課程系列的 API 應用程式，並已部署 hello 範例應用程式中的 hello[第一個](app-service-api-dotnet-get-started.md)和[第二個](app-service-api-cors-consume-javascript.md)教學課程，請略過 toohello[設定應用程式服務和 Azure AD 中的驗證](#azureauth)> 一節。</span><span class="sxs-lookup"><span data-stu-id="0840a-140">If you are following hello .NET tutorial series for API apps and have already deployed hello sample application as directed in hello [first](app-service-api-dotnet-get-started.md) and [second](app-service-api-cors-consume-javascript.md) tutorials, skip toohello [Set up authentication in App Service and Azure AD](#azureauth) section.</span></span>

<span data-ttu-id="0840a-141">如果您想 toofollow 本教學課程無須經過 hello 第一個和第二個教學課程，請勿 hello 下列步驟說明如何使用自動化程序 toodeploy hello 範例應用程式 tooget 啟動。</span><span class="sxs-lookup"><span data-stu-id="0840a-141">If you want toofollow this tutorial without going through hello first and second tutorials, do hello following steps which explain how tooget started by using an automated process toodeploy hello sample application.</span></span>

> [!NOTE]
> <span data-ttu-id="0840a-142">hello 下列步驟協助您取得的 toohello 相同起點時，如果您未 hello 前兩個教學課程中的，有一個例外狀況： Visual Studio 不會知道哪些 web 應用程式或每個專案部署至 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0840a-142">hello following steps get you toohello same starting point as if you did hello first two tutorials, with one exception: Visual Studio won't already know which web app or API app that each project gets deployed to.</span></span> <span data-ttu-id="0840a-143">這表示您不需要在此教學課程中說明的確切指示如何 toodeploy toohello 右目標。</span><span class="sxs-lookup"><span data-stu-id="0840a-143">That means you won't have exact instructions in this tutorial that explain how toodeploy toohello right targets.</span></span> <span data-ttu-id="0840a-144">如果您不想要找出 toodo hello 部署您自己的步驟，是較佳 toofollow hello 教學課程系列從 hello[第一個教學課程](app-service-api-dotnet-get-started.md)比 toostart 與此自動化部署程序。</span><span class="sxs-lookup"><span data-stu-id="0840a-144">If you're not comfortable with figuring out how toodo hello deployment steps on your own, it's better toofollow hello tutorial series from hello [first tutorial](app-service-api-dotnet-get-started.md) than toostart with this automated deployment process.</span></span>
> 
> 

1. <span data-ttu-id="0840a-145">請確定您有所有 hello 中所列的 hello 必要條件[第一個教學課程](app-service-api-dotnet-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="0840a-145">Make sure that you have all of hello prerequisites listed in hello [first tutorial](app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="0840a-146">中所列的加法 toohello 必要條件，這些驗證教學課程假設您已使用 App Service web 應用程式與 Visual Studio 中的應用程式開發介面應用程式和 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0840a-146">In addition toohello prerequisites listed, these authentication tutorials assume that you have worked with App Service web apps and API apps in Visual Studio and hello Azure portal.</span></span>
2. <span data-ttu-id="0840a-147">按一下 hello**部署 tooAzure**按鈕在 hello [tooDo 清單範例儲存機制讀我檔案](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md)toodeploy hello API 應用程式和 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0840a-147">Click hello **Deploy tooAzure** button in hello [tooDo List sample repository readme file](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md) toodeploy hello API apps and hello web app.</span></span> <span data-ttu-id="0840a-148">記下 hello Azure 資源群組的建立，因為您可以使用這個更新 toolook web 應用程式及 API 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="0840a-148">Make a note of hello Azure resource group that gets created, as you can use this later toolook up web app and API app names.</span></span>
3. <span data-ttu-id="0840a-149">下載或複製 hello [tooDo 清單範例儲存機制](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list)tooget hello 程式碼，您會與本機 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="0840a-149">Download or clone hello [tooDo List sample repository](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) tooget hello code that you'll work with locally in Visual Studio.</span></span>

## <span data-ttu-id="0840a-150"><a id="azureauth"></a> 在 App Service 和 Azure AD 中設定驗證</span><span class="sxs-lookup"><span data-stu-id="0840a-150"><a id="azureauth"></a> Set up authentication in App Service and Azure AD</span></span>
<span data-ttu-id="0840a-151">您現在可以 hello Azure App Service 中執行，而不需要使用者進行驗證的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0840a-151">You now have hello application running in Azure App Service without requiring that users be authenticated.</span></span> <span data-ttu-id="0840a-152">在本節中，您可以加入驗證執行下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="0840a-152">In this section you add authentication by doing hello following tasks:</span></span>

* <span data-ttu-id="0840a-153">設定應用程式服務 toorequire Azure Active Directory (Azure AD) 驗證，來呼叫 hello 中介層應用程式開發介面應用程式。</span><span class="sxs-lookup"><span data-stu-id="0840a-153">Configure App Service toorequire Azure Active Directory (Azure AD) authentication for calling hello middle tier API app.</span></span>
* <span data-ttu-id="0840a-154">建立 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0840a-154">Create an Azure AD application.</span></span>
* <span data-ttu-id="0840a-155">登入 toohello AngularJS 前端之後設定 hello Azure AD 應用程式 toosend hello 持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="0840a-155">Configure hello Azure AD application toosend hello bearer token after logon toohello AngularJS front end.</span></span> 

<span data-ttu-id="0840a-156">如果您執行下列 hello 教學課程指引時出現問題，請參閱 hello[疑難排解](#troubleshooting)hello 結尾 hello 教學課程 > 一節。</span><span class="sxs-lookup"><span data-stu-id="0840a-156">If you run into problems while following hello tutorial directions, see hello [Troubleshooting](#troubleshooting) section at hello end of hello tutorial.</span></span> 

### <a name="configure-authentication-for-hello-middle-tier-api-app"></a><span data-ttu-id="0840a-157">設定 hello 中介層應用程式開發介面應用程式的驗證</span><span class="sxs-lookup"><span data-stu-id="0840a-157">Configure authentication for hello middle tier API app</span></span>
1. <span data-ttu-id="0840a-158">在 hello [Azure 入口網站](https://portal.azure.com/)，瀏覽 toohello**設定**hello API 應用程式，您所建立的刀鋒視窗中的 hello ToDoListAPI 專案中，尋找 hello**功能** 區段中，然後按一下**驗證 / 授權**。</span><span class="sxs-lookup"><span data-stu-id="0840a-158">In hello [Azure portal](https://portal.azure.com/), navigate toohello **Settings** blade of hello API app that you created for hello ToDoListAPI project, find hello **Features** section, and then click **Authentication / Authorization**.</span></span>
   
    ![Azure 入口網站驗證/授權](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. <span data-ttu-id="0840a-160">在 hello**驗證 / 授權**刀鋒視窗中，按一下 **上**。</span><span class="sxs-lookup"><span data-stu-id="0840a-160">In hello **Authentication / Authorization** blade, click **On**.</span></span>
3. <span data-ttu-id="0840a-161">在 hello**當要求未經驗證的動作 tootake**下拉式清單中，選取**登入 Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="0840a-161">In hello **Action tootake when request is not authenticated** drop-down list, select **Log in with Azure Active Directory**.</span></span>
   
    <span data-ttu-id="0840a-162">此選項可確保任何 unauathenticated 要求會到達 hello API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0840a-162">This option ensures that no unauathenticated requests will reach hello API app.</span></span> 
4. <span data-ttu-id="0840a-163">在 [驗證提供者] 底下，按一下 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="0840a-163">Under **Authentication Providers**, click **Azure Active Directory**.</span></span>
   
    ![Azure 入口網站驗證/授權刀鋒視窗](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. <span data-ttu-id="0840a-165">在 hello **Azure Active Directory 設定**刀鋒視窗中，按一下  **Express**</span><span class="sxs-lookup"><span data-stu-id="0840a-165">In hello **Azure Active Directory Settings** blade, click **Express**</span></span>
   
    ![Azure 入口網站驗證/授權表達選項](./media/app-service-api-dotnet-user-principal-auth/aadsettings.png)
   
    <span data-ttu-id="0840a-167">以 hello **Express**選項時，應用程式服務可以自動建立 Azure AD 應用程式在您的 Azure AD 中[租用戶](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant)。</span><span class="sxs-lookup"><span data-stu-id="0840a-167">With hello **Express** option, App Service can automatically create an Azure AD application in your Azure AD [tenant](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant).</span></span> 
   
    <span data-ttu-id="0840a-168">您不需要 toocreate 租用戶，因為每個 Azure 帳戶會自動擁有一個。</span><span class="sxs-lookup"><span data-stu-id="0840a-168">You don't have toocreate a tenant, because every Azure account automatically has one.</span></span>
6. <span data-ttu-id="0840a-169">下**管理模式**，按一下**建立新的 AD 應用程式**如果尚未選取，並請注意在 hello hello 值**建立應用程式**文字方塊中，您將查閱此 AADhello Azure 傳統入口網站更新版本中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0840a-169">Under **Management mode**, click **Create New AD App** if it isn't already selected, and notice hello value that is in hello **Create App** text box; you'll look up this AAD application in hello Azure classic portal later.</span></span>
   
    ![Azure 入口網站 Azure AD 設定](./media/app-service-api-dotnet-user-principal-auth/aadsettings2.png)
   
    <span data-ttu-id="0840a-171">Azure 會自動建立 Azure AD 應用程式與 Azure AD 租用戶中的 hello 指定名稱。</span><span class="sxs-lookup"><span data-stu-id="0840a-171">Azure will automatically create an Azure AD application with hello indicated name in your Azure AD tenant.</span></span> <span data-ttu-id="0840a-172">根據預設，名為 hello Azure AD 應用程式相同 hello 與 hello API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0840a-172">By default, hello Azure AD application is named hello same as hello API app.</span></span> <span data-ttu-id="0840a-173">如有需要，也可以輸入不同名稱。</span><span class="sxs-lookup"><span data-stu-id="0840a-173">If you prefer, you can enter a different name.</span></span>
7. <span data-ttu-id="0840a-174">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="0840a-174">Click **OK**.</span></span>
8. <span data-ttu-id="0840a-175">在 hello**驗證 / 授權**刀鋒視窗中，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="0840a-175">In hello **Authentication / Authorization** blade, click **Save**.</span></span>
   
    ![按一下 [Save] \(儲存)。](./media/app-service-api-dotnet-user-principal-auth/authsave.png)

<span data-ttu-id="0840a-177">現在只有 Azure AD 租用戶的使用者，才可以呼叫 hello API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0840a-177">Now only users in your Azure AD tenant can call hello API app.</span></span>

### <a name="optional-test-hello-api-app"></a><span data-ttu-id="0840a-178">選擇性： 測試 hello API 的應用程式</span><span class="sxs-lookup"><span data-stu-id="0840a-178">Optional: Test hello API app</span></span>
1. <span data-ttu-id="0840a-179">在瀏覽器中前往 toohello hello API 應用程式 URL: hello 中**API 應用程式**刀鋒視窗中 hello Azure 入口網站中，按一下底下的 hello 連結**URL**。</span><span class="sxs-lookup"><span data-stu-id="0840a-179">In a browser go toohello URL of hello API app: in hello **API app** blade in hello Azure portal, click hello link under **URL**.</span></span>  
   
    <span data-ttu-id="0840a-180">您是重新導向的 tooa 登入畫面，因為 tooreach hello API 應用程式不允許未經驗證的要求。</span><span class="sxs-lookup"><span data-stu-id="0840a-180">You are redirected tooa login screen because unauthenticated requests are not allowed tooreach hello API app.</span></span>
   
    <span data-ttu-id="0840a-181">如果您的瀏覽器 toohello 「 成功建立 」 頁面，hello 瀏覽器可能已登入-在此情況下，開啟 InPrivate 或 Incognito 視窗，並移 toohello API 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="0840a-181">If your browser goes toohello "successfully created" page, hello browser might already be logged on -- in that case, open an InPrivate or Incognito window and go toohello API app's URL.</span></span>
2. <span data-ttu-id="0840a-182">在 Azure AD 租用戶中以使用者的認證進行登入。</span><span class="sxs-lookup"><span data-stu-id="0840a-182">Log on using credentials for a user in your Azure AD tenant.</span></span>
   
    <span data-ttu-id="0840a-183">當您登入時，hello"建立成功 」 的頁面會顯示 hello 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="0840a-183">When you're logged on, hello "successfully created" page appears in hello browser.</span></span>
3. <span data-ttu-id="0840a-184">關閉 hello 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="0840a-184">Close hello browser.</span></span>

### <a name="configure-hello-azure-ad-application"></a><span data-ttu-id="0840a-185">Hello Azure AD 應用程式設定</span><span class="sxs-lookup"><span data-stu-id="0840a-185">Configure hello Azure AD application</span></span>
<span data-ttu-id="0840a-186">當您設定了 Azure AD 驗證，App Service 就會為您建立 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0840a-186">When you configured Azure AD authentication, App Service created an Azure AD application for you.</span></span> <span data-ttu-id="0840a-187">根據預設 hello 新的 Azure AD 應用程式已設定的 tooprovide hello 持有人權杖 toohello API 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="0840a-187">By default hello new Azure AD application was configured tooprovide hello bearer token toohello API app's URL.</span></span> <span data-ttu-id="0840a-188">本節中，您會設定 hello Azure AD 應用程式 tooprovide hello 持有人權杖 toohello AngularJS 前端而不是直接 toohello 中介層應用程式開發介面應用程式。</span><span class="sxs-lookup"><span data-stu-id="0840a-188">In this section you configure hello Azure AD application tooprovide hello bearer token toohello AngularJS front end instead of directly toohello middle tier API app.</span></span> <span data-ttu-id="0840a-189">hello AngularJS 前端呼叫 hello API 應用程式時，會傳送 hello 語彙基元 toohello API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0840a-189">hello AngularJS front end will send hello token toohello API app when it calls hello API app.</span></span>

> [!NOTE]
> <span data-ttu-id="0840a-190">tookeep hello 程序越簡單越好，本教學課程會使用單一的 Azure AD 應用程式來進行 hello 前端和 hello 中介層應用程式開發介面應用程式。</span><span class="sxs-lookup"><span data-stu-id="0840a-190">tookeep hello process as simple as possible, this tutorial uses a single Azure AD application for both hello front end and hello middle tier API app.</span></span> <span data-ttu-id="0840a-191">另一個選項是 toouse 兩個 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0840a-191">Another option is toouse two Azure AD applications.</span></span> <span data-ttu-id="0840a-192">在此情況下，您必須 toogive hello 前端的 Azure AD 應用程式的權限 toocall hello 中介層的 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0840a-192">In that case you would have toogive hello front end's Azure AD application permission toocall hello middle tier's Azure AD application.</span></span> <span data-ttu-id="0840a-193">此多重應用程式的方法會提供更細微地控制的權限 tooeach 層。</span><span class="sxs-lookup"><span data-stu-id="0840a-193">This multi-application approach would give you more granular control over permissions tooeach tier.</span></span>
> 
> 

1. <span data-ttu-id="0840a-194">在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，跳過**Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="0840a-194">In hello [Azure classic portal](https://manage.windowsazure.com/), go too**Azure Active Directory**.</span></span>
   
   <span data-ttu-id="0840a-195">您必須 toouse hello 傳統入口網站，因為某些 Azure Active Directory 設定，您需要存取 tooare 尚無法使用 hello 目前的 Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="0840a-195">You have toouse hello classic portal because certain Azure Active Directory settings that you need access tooare not yet available in hello current Azure portal.</span></span>
2. <span data-ttu-id="0840a-196">在 hello**目錄**索引標籤上，按一下您的 AAD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="0840a-196">On hello **Directory** tab, click your AAD tenant.</span></span>
   
   ![傳統入口網站的 Azure AD](./media/app-service-api-dotnet-user-principal-auth/selecttenant.png)
3. <span data-ttu-id="0840a-198">按一下**應用程式 > 我公司所擁有的應用程式**，然後按一下hello 核取記號。</span><span class="sxs-lookup"><span data-stu-id="0840a-198">Click **Applications > Applications my company owns**, and then click hello check mark.</span></span>
   
   <span data-ttu-id="0840a-199">您可能還有 toorefresh hello 頁面 toosee hello 新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0840a-199">You might also have toorefresh hello page toosee hello new application.</span></span>
4. <span data-ttu-id="0840a-200">Hello 應用程式清單中按一下 hello hello 時您的應用程式開發介面應用程式啟用驗證為您建立 Azure 的其中一個名稱。</span><span class="sxs-lookup"><span data-stu-id="0840a-200">In hello list of applications, click hello name of hello one that Azure created for you when you enabled authentication for your API app.</span></span>
   
   ![Azure AD [應用程式] 索引標籤](./media/app-service-api-dotnet-user-principal-auth/appstab.png)
5. <span data-ttu-id="0840a-202">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="0840a-202">Click **Configure**.</span></span>
   
   ![Azure AD [設定] 索引標籤](./media/app-service-api-dotnet-user-principal-auth/configure.png)
6. <span data-ttu-id="0840a-204">設定**登入 URL** toohello URL AngularJS web 應用程式，沒有尾端斜線。</span><span class="sxs-lookup"><span data-stu-id="0840a-204">Set **Sign-on URL** toohello URL for your AngularJS web app, no trailing slash.</span></span>
   
   <span data-ttu-id="0840a-205">例如：https://todolistangular.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="0840a-205">For example: https://todolistangular.azurewebsites.net</span></span>
   
   ![登入 URL](./media/app-service-api-dotnet-user-principal-auth/signonurlazure.png)
7. <span data-ttu-id="0840a-207">設定**回覆 URL** toohello URL，web 應用程式，沒有尾端斜線。</span><span class="sxs-lookup"><span data-stu-id="0840a-207">Set **Reply URL** toohello URL for your web app, no trailing slash.</span></span>
   
   <span data-ttu-id="0840a-208">例如：https://todolistsangular.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="0840a-208">For example: https://todolistsangular.azurewebsites.net</span></span>
8. <span data-ttu-id="0840a-209">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="0840a-209">Click **Save**.</span></span>
   
   ![回覆 URL](./media/app-service-api-dotnet-user-principal-auth/replyurlazure.png)
9. <span data-ttu-id="0840a-211">在 hello hello 頁面底部，按一下**管理資訊清單 > 下載資訊清單**。</span><span class="sxs-lookup"><span data-stu-id="0840a-211">At hello bottom of hello page, click **Manage manifest > Download manifest**.</span></span>
   
   ![下載資訊清單](./media/app-service-api-dotnet-user-principal-auth/downloadmanifest.png)
10. <span data-ttu-id="0840a-213">下載 hello 檔案 tooa 位置可在其中編輯它。</span><span class="sxs-lookup"><span data-stu-id="0840a-213">Download hello file tooa location where you can edit it.</span></span>
11. <span data-ttu-id="0840a-214">在 hello 下載資訊清單檔案，搜尋 hello`oauth2AllowImplicitFlow`屬性。</span><span class="sxs-lookup"><span data-stu-id="0840a-214">In hello downloaded manifest file, search for hello  `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="0840a-215">變更這個屬性從 hello 值`false`太`true`，然後儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="0840a-215">Change hello value of this property from `false` too`true`, and then save hello file.</span></span>
    
    <span data-ttu-id="0840a-216">必須要有這項設定才能從 JavaScript 單一頁面應用程式進行存取。</span><span class="sxs-lookup"><span data-stu-id="0840a-216">This setting is required for access from a JavaScript single-page application.</span></span> <span data-ttu-id="0840a-217">它可讓 hello Oauth 2.0 承載權杖 toobe hello URL 片段中傳回。</span><span class="sxs-lookup"><span data-stu-id="0840a-217">It enables hello Oauth 2.0 bearer token toobe returned in hello URL fragment.</span></span>
12. <span data-ttu-id="0840a-218">按一下**管理資訊清單 > 上傳資訊清單**，和上傳 hello 檔案，您在 hello 前面步驟中更新。</span><span class="sxs-lookup"><span data-stu-id="0840a-218">Click **Manage manifest > Upload manifest**, and upload hello file that you updated in hello preceding step.</span></span>
    
    ![上傳資訊清單](./media/app-service-api-dotnet-user-principal-auth/uploadmanifest.png)
13. <span data-ttu-id="0840a-220">複製 hello**用戶端識別碼**值，並將其儲存的地方，就可以從更新版本。</span><span class="sxs-lookup"><span data-stu-id="0840a-220">Copy hello **Client ID** value and save it somewhere you can get it from later.</span></span>

## <a name="configure-hello-todolistangular-project-toouse-authentication"></a><span data-ttu-id="0840a-221">設定 hello ToDoListAngular 專案 toouse 驗證</span><span class="sxs-lookup"><span data-stu-id="0840a-221">Configure hello ToDoListAngular project toouse authentication</span></span>
<span data-ttu-id="0840a-222">本節中您會變更 hello AngularJS 前端，使其使用 Active Directory 驗證程式庫 (ADAL) for JS tooacquire hello 登入的使用者從 Azure AD 的承載權杖。</span><span class="sxs-lookup"><span data-stu-id="0840a-222">In this section you change hello AngularJS front end so that it uses Active Directory Authentication Library (ADAL) for JS tooacquire a bearer token for hello logged-on user from Azure AD.</span></span> <span data-ttu-id="0840a-223">hello 程式碼會將包含 hello 語彙基元傳送 toohello 中介層，HTTP 要求中 hello 下列圖表所示。</span><span class="sxs-lookup"><span data-stu-id="0840a-223">hello code will include hello token in HTTP requests sent toohello middle tier, as shown in hello following diagram.</span></span> 

![使用者驗證圖表](./media/app-service-api-dotnet-user-principal-auth/appdiagram.png)

<span data-ttu-id="0840a-225">請遵循變更 toofiles hello ToDoListAngular 專案中的 hello。</span><span class="sxs-lookup"><span data-stu-id="0840a-225">Make hello following changes toofiles in hello ToDoListAngular project.</span></span>

1. <span data-ttu-id="0840a-226">開啟 hello *index.cshtml*檔案。</span><span class="sxs-lookup"><span data-stu-id="0840a-226">Open hello *index.cshtml* file.</span></span>
2. <span data-ttu-id="0840a-227">參考 JS 指令碼的 hello Active Directory 驗證程式庫 (ADAL) 的 hello 行取消註解。</span><span class="sxs-lookup"><span data-stu-id="0840a-227">Uncomment hello lines that reference hello Active Directory Authentication Library (ADAL) for JS scripts.</span></span>
   
        <script src="app/scripts/adal.js"></script>
        <script src="app/scripts/adal-angular.js"></script>
3. <span data-ttu-id="0840a-228">開啟 hello *app/scripts/app.js*檔案。</span><span class="sxs-lookup"><span data-stu-id="0840a-228">Open hello *app/scripts/app.js* file.</span></span>
4. <span data-ttu-id="0840a-229">註解的程式碼的 hello 區塊標示為 「 未驗證 」，並取消註解的程式碼的 hello 區塊標示為 [使用驗證]。</span><span class="sxs-lookup"><span data-stu-id="0840a-229">Comment out hello block of code marked for "without authentication" and uncomment hello block of code marked for "with authentication".</span></span>
   
    <span data-ttu-id="0840a-230">這項變更參考 hello ADAL JS 驗證提供者，並提供組態值 tooit。</span><span class="sxs-lookup"><span data-stu-id="0840a-230">This change references hello ADAL JS authentication provider and provides configuration values tooit.</span></span> <span data-ttu-id="0840a-231">您可以在 hello 下列步驟設定 hello API 應用程式和 Azure AD 應用程式的組態值。</span><span class="sxs-lookup"><span data-stu-id="0840a-231">In hello following steps you set hello configuration values for your API app and Azure AD application.</span></span>
5. <span data-ttu-id="0840a-232">設定 hello hello 程式碼中`endpoints`hello API 應用程式，您建立 hello ToDoListAPI 專案，並將設定的變數，將 hello API URL toohello URL hello Azure AD 應用程式識別碼 toohello 用戶端識別碼，您所複製的 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="0840a-232">In hello code that sets hello `endpoints` variable, set hello API URL toohello URL of hello API app that you created for hello ToDoListAPI project, and set hello Azure AD application ID toohello client ID that you copied from hello Azure classic portal.</span></span>
   
    <span data-ttu-id="0840a-233">下列範例類似 toohello 的現在 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="0840a-233">hello code is now similar toohello following example.</span></span>
   
        var endpoints = {
            "https://todolistapi0121.azurewebsites.net/": "1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3"
        };
6. <span data-ttu-id="0840a-234">在 hello 呼叫太`adalProvider.init`，將`tenant`tooyour 租用戶名稱和`clientId`toosame hello 先前步驟中的值。</span><span class="sxs-lookup"><span data-stu-id="0840a-234">In hello call too`adalProvider.init`, set `tenant` tooyour tenant name and `clientId` toosame value you used in hello previous step.</span></span>
   
    <span data-ttu-id="0840a-235">下列範例類似 toohello 的現在 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="0840a-235">hello code is now similar toohello following example.</span></span>
   
        adalProvider.init(
            {
                instance: 'https://login.microsoftonline.com/', 
                tenant: 'contoso.onmicrosoft.com',
                clientId: '1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3',
                extraQueryParameter: 'nux=1',
                endpoints: endpoints
            },
            $httpProvider
            );
   
    <span data-ttu-id="0840a-236">這些變更太`app.js`指定 hello 呼叫程式碼和呼叫 API 的 hello 位於 hello 相同的 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0840a-236">These changes too`app.js` specify that hello calling code and hello called API are in hello same Azure AD application.</span></span>
7. <span data-ttu-id="0840a-237">開啟 hello *app/scripts/homeCtrl.js*檔案。</span><span class="sxs-lookup"><span data-stu-id="0840a-237">Open hello *app/scripts/homeCtrl.js* file.</span></span>
8. <span data-ttu-id="0840a-238">註解的程式碼的 hello 區塊標示為 「 未驗證 」，並取消註解的程式碼的 hello 區塊標示為 [使用驗證]。</span><span class="sxs-lookup"><span data-stu-id="0840a-238">Comment out hello block of code marked for "without authentication" and uncomment hello block of code marked for "with authentication".</span></span>
9. <span data-ttu-id="0840a-239">開啟 hello *app/scripts/indexCtrl.js*檔案。</span><span class="sxs-lookup"><span data-stu-id="0840a-239">Open hello *app/scripts/indexCtrl.js* file.</span></span>
10. <span data-ttu-id="0840a-240">註解的程式碼的 hello 區塊標示為 「 未驗證 」，並取消註解的程式碼的 hello 區塊標示為 [使用驗證]。</span><span class="sxs-lookup"><span data-stu-id="0840a-240">Comment out hello block of code marked for "without authentication" and uncomment hello block of code marked for "with authentication".</span></span>

### <a name="deploy-hello-todolistangular-project-tooazure"></a><span data-ttu-id="0840a-241">部署 hello ToDoListAngular 專案 tooAzure</span><span class="sxs-lookup"><span data-stu-id="0840a-241">Deploy hello ToDoListAngular project tooAzure</span></span>
1. <span data-ttu-id="0840a-242">在**方案總管 中**hello ToDoListAngular 專案中，以滑鼠右鍵按一下，然後按**發行**。</span><span class="sxs-lookup"><span data-stu-id="0840a-242">In **Solution Explorer**, right-click hello ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="0840a-243">按一下 [發行] 。</span><span class="sxs-lookup"><span data-stu-id="0840a-243">Click **Publish**.</span></span>
   
    <span data-ttu-id="0840a-244">Visual Studio 部署 hello 專案，並開啟瀏覽器 toohello web 應用程式的基底 URL。</span><span class="sxs-lookup"><span data-stu-id="0840a-244">Visual Studio deploys hello project and opens a browser toohello web app's base URL.</span></span> <span data-ttu-id="0840a-245">這會顯示 403 錯誤頁面上，也就是從瀏覽器嘗試 toogo tooa Web API 基底 URL 的一般。</span><span class="sxs-lookup"><span data-stu-id="0840a-245">This will show a 403 error page, which is normal for an attempt toogo tooa Web API base URL from a browser.</span></span>
   
    <span data-ttu-id="0840a-246">您仍然必須 toomake 變更 toohello 中介層應用程式開發介面應用程式之前，您可以測試 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0840a-246">You still have toomake a change toohello middle tier API app before you can test hello application.</span></span>
3. <span data-ttu-id="0840a-247">關閉 hello 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="0840a-247">Close hello browser.</span></span>

## <a name="configure-hello-todolistapi-project-toouse-authentication"></a><span data-ttu-id="0840a-248">設定 hello ToDoListAPI 專案 toouse 驗證</span><span class="sxs-lookup"><span data-stu-id="0840a-248">Configure hello ToDoListAPI project toouse authentication</span></span>
<span data-ttu-id="0840a-249">目前 hello ToDoListAPI 專案傳送"*"做為 hello`owner`值 tooToDoListDataAPI。</span><span class="sxs-lookup"><span data-stu-id="0840a-249">Currently hello ToDoListAPI project sends "*" as hello `owner` value tooToDoListDataAPI.</span></span> <span data-ttu-id="0840a-250">本節中您要變更 hello 程式碼 toosend hello hello 登入的使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="0840a-250">In this section you change hello code toosend hello ID of hello logged-on user.</span></span>

<span data-ttu-id="0840a-251">請 hello 遵循 hello ToDoListAPI 專案中的變更。</span><span class="sxs-lookup"><span data-stu-id="0840a-251">Make hello following changes in hello ToDoListAPI project.</span></span>

1. <span data-ttu-id="0840a-252">開啟 hello *Controllers/ToDoListController.cs*檔案，並設定每個動作方法中的 hello 行取消註解`owner`toohello Azure AD`NameIdentifier`宣告值。</span><span class="sxs-lookup"><span data-stu-id="0840a-252">Open hello *Controllers/ToDoListController.cs* file, and uncomment hello line in each action method that sets `owner` toohello Azure AD `NameIdentifier` claim value.</span></span> <span data-ttu-id="0840a-253">例如：</span><span class="sxs-lookup"><span data-stu-id="0840a-253">For example:</span></span>
   
        owner = ((ClaimsIdentity)User.Identity).FindFirst(ClaimTypes.NameIdentifier).Value;
   
    <span data-ttu-id="0840a-254">**重要**： 不要取消註解程式碼中 hello`ToDoListDataAPI`方法; 您將會執行，稍後 hello 服務主體的驗證教學課程。</span><span class="sxs-lookup"><span data-stu-id="0840a-254">**Important**: Don't uncomment code in hello `ToDoListDataAPI` method; you'll do that later for hello service principal authentication tutorial.</span></span>

### <a name="deploy-hello-todolistapi-project-tooazure"></a><span data-ttu-id="0840a-255">部署 hello ToDoListAPI 專案 tooAzure</span><span class="sxs-lookup"><span data-stu-id="0840a-255">Deploy hello ToDoListAPI project tooAzure</span></span>
1. <span data-ttu-id="0840a-256">在**方案總管 中**hello ToDoListAPI 專案中，以滑鼠右鍵按一下，然後按**發行**。</span><span class="sxs-lookup"><span data-stu-id="0840a-256">In **Solution Explorer**, right-click hello ToDoListAPI project, and then click **Publish**.</span></span>
2. <span data-ttu-id="0840a-257">按一下 [發行] 。</span><span class="sxs-lookup"><span data-stu-id="0840a-257">Click **Publish**.</span></span>
   
    <span data-ttu-id="0840a-258">Visual Studio 部署 hello 專案，並開啟瀏覽器 toohello API 應用程式的基底 URL。</span><span class="sxs-lookup"><span data-stu-id="0840a-258">Visual Studio deploys hello project and opens a browser toohello API app's base URL.</span></span>
3. <span data-ttu-id="0840a-259">關閉 hello 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="0840a-259">Close hello browser.</span></span>

### <a name="test-hello-application"></a><span data-ttu-id="0840a-260">測試 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="0840a-260">Test hello application</span></span>
1. <span data-ttu-id="0840a-261">移 toohello hello web 應用程式，URL**使用 HTTPS，而不是 HTTP**。</span><span class="sxs-lookup"><span data-stu-id="0840a-261">Go toohello URL of hello web app, **using HTTPS, not HTTP**.</span></span>
2. <span data-ttu-id="0840a-262">按一下 hello **tooDo 清單** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0840a-262">Click hello **tooDo List** tab.</span></span>
   
    <span data-ttu-id="0840a-263">您必須提示的 toolog 中。</span><span class="sxs-lookup"><span data-stu-id="0840a-263">You are prompted toolog in.</span></span>
3. <span data-ttu-id="0840a-264">Hello AAD 租用戶中的使用者的認證登入。</span><span class="sxs-lookup"><span data-stu-id="0840a-264">Log in with hello credentials of a user in your AAD tenant.</span></span>
4. <span data-ttu-id="0840a-265">hello **tooDo 清單**頁面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="0840a-265">hello **tooDo List** page appears.</span></span>
   
   ![tooDo 清單頁面](./media/app-service-api-dotnet-user-principal-auth/webappindex.png)
   
   <span data-ttu-id="0840a-267">目前並不會顯示任何待辦事項項目，因為這些項目到目前為止全都適用於擁有者 "*"。</span><span class="sxs-lookup"><span data-stu-id="0840a-267">No to-do items are displayed because until now they have all been for owner "*".</span></span> <span data-ttu-id="0840a-268">Hello 中介層現在要求 hello 登入之使用者的項目，並無尚未建立。</span><span class="sxs-lookup"><span data-stu-id="0840a-268">Now hello middle tier is requesting items for hello logged-on user, and none have been created yet.</span></span>
5. <span data-ttu-id="0840a-269">加入新的待辦項目 tooverify 正在 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0840a-269">Add new to-do items tooverify that hello application is working.</span></span>
6. <span data-ttu-id="0840a-270">在另一個瀏覽器視窗中，移 toohello 的 UI Swagger URL hello ToDoListDataAPI API 應用程式，然後按一下**ToDoList > 取得**。</span><span class="sxs-lookup"><span data-stu-id="0840a-270">In another browser window, go toohello Swagger UI URL for hello ToDoListDataAPI API app and click **ToDoList > Get**.</span></span> <span data-ttu-id="0840a-271">輸入星號 hello`owner`參數，然後再按一下**現在就試試看**。</span><span class="sxs-lookup"><span data-stu-id="0840a-271">Enter an asterisk for hello `owner` parameter, and then click **Try it out**.</span></span>
   
   <span data-ttu-id="0840a-272">hello 回應會顯示 hello 新待辦項目有 hello 實際的 Azure AD 使用者識別碼 hello 擁有者屬性中。</span><span class="sxs-lookup"><span data-stu-id="0840a-272">hello response shows that hello new to-do items have hello actual Azure AD user ID in hello Owner property.</span></span>
   
   ![JSON 回應中的擁有者識別碼](./media/app-service-api-dotnet-user-principal-auth/todolistapiauth.png)

## <a name="building-hello-projects-from-scratch"></a><span data-ttu-id="0840a-274">建置從頭 hello 專案</span><span class="sxs-lookup"><span data-stu-id="0840a-274">Building hello projects from scratch</span></span>
<span data-ttu-id="0840a-275">hello 兩個 Web API 專案所建立的 hello **Azure API 應用程式**專案範本和取代 hello 預設值的控制站與 ToDoList 控制站。</span><span class="sxs-lookup"><span data-stu-id="0840a-275">hello two Web API projects were created by using hello **Azure API App** project template and replacing hello default Values controller with a ToDoList controller.</span></span> 

<span data-ttu-id="0840a-276">如需有關資訊太建立 AngularJS 單一頁面應用程式 Web API 2 的後端，請參閱[手上實驗室： 建置單一頁面應用程式 (SPA)，使用 ASP.NET Web API 和 Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs)。</span><span class="sxs-lookup"><span data-stu-id="0840a-276">For information about how too create an AngularJS single-page application with a Web API 2 back end, see  [Hands On Lab: Build a Single Page Application (SPA) with ASP.NET Web API and Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs).</span></span> <span data-ttu-id="0840a-277">如需有關資訊 tooadd Azure AD 驗證程式碼，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="0840a-277">For information about how tooadd Azure AD authentication code, see hello following resources:</span></span>

* <span data-ttu-id="0840a-278">[使用 Azure AD 保護 AngularJS 單一頁面應用程式](../active-directory/active-directory-devquickstarts-angular.md)。</span><span class="sxs-lookup"><span data-stu-id="0840a-278">[Securing AngularJS Single Page Apps with Azure AD](../active-directory/active-directory-devquickstarts-angular.md).</span></span>
* [<span data-ttu-id="0840a-279">簡介 ADAL JS v1</span><span class="sxs-lookup"><span data-stu-id="0840a-279">Introducing ADAL JS v1</span></span>](http://www.cloudidentity.com/blog/2015/02/19/introducing-adal-js-v1/)

## <a name="troubleshooting"></a><span data-ttu-id="0840a-280">疑難排解</span><span class="sxs-lookup"><span data-stu-id="0840a-280">Troubleshooting</span></span>
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* <span data-ttu-id="0840a-281">請確定不要混淆 ToDoListAPI (中介層) 和 ToDoListDataAPI (資料層)。</span><span class="sxs-lookup"><span data-stu-id="0840a-281">Make sure that you don't confuse ToDoListAPI (middle tier) and ToDoListDataAPI (data tier).</span></span> <span data-ttu-id="0840a-282">例如，確認您新增 authentication toohello 中介層應用程式開發介面應用程式，hello 資料層。</span><span class="sxs-lookup"><span data-stu-id="0840a-282">For example, verify that you added authentication toohello middle tier API app, not hello data tier.</span></span> 
* <span data-ttu-id="0840a-283">請確定 hello AngularJS 來源的程式碼參考 hello 中介層應用程式開發介面應用程式 URL （ToDoListAPI、 不 ToDoListDataAPI） 和 hello 修正 Azure AD 用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="0840a-283">Make sure that hello AngularJS source code references hello middle tier API app URL (ToDoListAPI, not ToDoListDataAPI)and hello correct Azure AD client ID.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0840a-284">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0840a-284">Next steps</span></span>
<span data-ttu-id="0840a-285">在本教學課程中，您學會 toouse App Service API 應用程式的驗證和 toocall hello API 應用程式使用的方式 hello JS ADAL 程式庫。</span><span class="sxs-lookup"><span data-stu-id="0840a-285">In this tutorial you learned how toouse App Service authentication for an API app and how toocall hello API app by using hello ADAL JS library.</span></span> <span data-ttu-id="0840a-286">Hello 下一個教學課程中您將學習如何太[tooyour API 應用程式安全地存取服務對服務案例](app-service-api-dotnet-service-principal-auth.md)。</span><span class="sxs-lookup"><span data-stu-id="0840a-286">In hello next tutorial you'll learn how too[secure access tooyour API app for service-to-service scenarios](app-service-api-dotnet-service-principal-auth.md).</span></span>

