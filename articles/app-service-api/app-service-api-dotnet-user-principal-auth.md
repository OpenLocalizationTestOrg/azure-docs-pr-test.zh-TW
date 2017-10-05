---
title: "Azure App Service 中 API Apps 的使用者驗證 | Microsoft Docs"
description: "了解如何藉由僅允許經過驗證的使用者存取，保護 Azure App Service 中的 API 應用程式。"
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
ms.openlocfilehash: a5b713f3a60b3886d813438496d704f464d914e6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="user-authentication-for-api-apps-in-azure-app-service"></a><span data-ttu-id="f5404-103">Azure App Service 中 API Apps 的使用者驗證</span><span class="sxs-lookup"><span data-stu-id="f5404-103">User authentication for API Apps in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="f5404-104">概觀</span><span class="sxs-lookup"><span data-stu-id="f5404-104">Overview</span></span>
<span data-ttu-id="f5404-105">本文說明如何保護 Azure API 應用程式，以便只有已驗證的使用者可以呼叫它。</span><span class="sxs-lookup"><span data-stu-id="f5404-105">This article shows how to protect an Azure API app so that only authenticated users can call it.</span></span> <span data-ttu-id="f5404-106">本文假設您已閱讀 [Azure App Service 驗證概觀](../app-service/app-service-authentication-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f5404-106">The article assumes that you have read the [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span>

<span data-ttu-id="f5404-107">您將了解：</span><span class="sxs-lookup"><span data-stu-id="f5404-107">You'll learn:</span></span>

* <span data-ttu-id="f5404-108">如何使用 Azure Active Directory (Azure AD) 的詳細資料設定驗證提供者。</span><span class="sxs-lookup"><span data-stu-id="f5404-108">How to configure an authentication provider, with details for Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="f5404-109">如何使用 [JavaScript 適用的 Active Directory 驗證程式庫 (ADAL)](https://github.com/AzureAD/azure-activedirectory-library-for-js)取用受保護的 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-109">How to consume a protected API app by using the [Active Directory Authentication Library (ADAL) for JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js).</span></span>

<span data-ttu-id="f5404-110">本文包含兩個部分：</span><span class="sxs-lookup"><span data-stu-id="f5404-110">The article contains two sections:</span></span>

* <span data-ttu-id="f5404-111">[如何在 Azure App Service 中設定使用者驗證](#authconfig) 一節大致說明如何為 API 應用程式設定使用者驗證，且一體適用於 App Service 支援的所有架構，包括 .NET、Node.js 和 Java。</span><span class="sxs-lookup"><span data-stu-id="f5404-111">The [How to configure user authentication in Azure App Service](#authconfig) section explains in general how to configure user authentication for any API app and applies equally to all frameworks supported by App Service, including .NET, Node.js, and Java.</span></span>
* <span data-ttu-id="f5404-112">從 [繼續進行 .NET API Apps 教學課程](#tutorialstart) 一節開始，本文會引導您使用 .NET 後端和 AngularJS 前端設定範例應用程式，使其使用 Azure Active Directory 進行使用者驗證。</span><span class="sxs-lookup"><span data-stu-id="f5404-112">Starting with the [Continuing the .NET API Apps tutorials](#tutorialstart) section, the article guides you through configuring a sample application with a .NET back end and an AngularJS front end so that it uses Azure Active Directory for user authentication.</span></span> 

## <span data-ttu-id="f5404-113"><a id="authconfig"></a> 如何在 Azure App Service 中設定使用者驗證</span><span class="sxs-lookup"><span data-stu-id="f5404-113"><a id="authconfig"></a> How to configure user authentication in Azure App Service</span></span>
<span data-ttu-id="f5404-114">本節提供適用於任何 API 應用程式的一般指示。</span><span class="sxs-lookup"><span data-stu-id="f5404-114">This section provides general instructions that apply to any API app.</span></span> <span data-ttu-id="f5404-115">如需「待辦事項清單」.NET 範例應用程式的專用步驟，請移至 [繼續進行 .NET 入門教學課程](#tutorialstart)。</span><span class="sxs-lookup"><span data-stu-id="f5404-115">For steps specific to the To Do List .NET sample application, go to [Continuing the .NET getting-started tutorials](#tutorialstart).</span></span>

1. <span data-ttu-id="f5404-116">在 [Azure 入口網站](https://portal.azure.com/)中，瀏覽至您想要保護的 API 應用程式的 [設定] 刀鋒視窗，尋找 [功能] 區段，再按一下 [驗證/授權]。</span><span class="sxs-lookup"><span data-stu-id="f5404-116">In the [Azure portal](https://portal.azure.com/), navigate to the **Settings** blade of the API app that you want to protect, find the **Features** section, and then click **Authentication/ Authorization**.</span></span>
   
    ![Azure 入口網站驗證/授權](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. <span data-ttu-id="f5404-118">在 [驗證/授權] 刀鋒視窗中，按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="f5404-118">In the **Authentication / Authorization** blade, click **On**.</span></span>
3. <span data-ttu-id="f5404-119">在 [要求未經驗證時所採取的動作]  下拉式清單中，選取其中一個選項。</span><span class="sxs-lookup"><span data-stu-id="f5404-119">Select one of the options from the **Action to take when request is not authenticated** drop-down list.</span></span>
   
   * <span data-ttu-id="f5404-120">如果您只想讓經過驗證的呼叫觸達 API 應用程式，請選擇其中一個 [登入方式]  選項。</span><span class="sxs-lookup"><span data-stu-id="f5404-120">If you want only authenticated calls to reach your API app, choose one of the **Log in with ...** options.</span></span> <span data-ttu-id="f5404-121">此選項可讓您保護 API 應用程式，卻不需要撰寫任何在其中執行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="f5404-121">This option enables you to protect the API app without writing any code that runs in it.</span></span>
   * <span data-ttu-id="f5404-122">如果您想讓所有呼叫觸達 API 應用程式，請選擇 [允許要求 (無動作)] 。</span><span class="sxs-lookup"><span data-stu-id="f5404-122">If you want all calls to reach your API app, choose **Allow request (no action)**.</span></span> <span data-ttu-id="f5404-123">您可以使用此選項將未經驗證的呼叫端導向您選擇的驗證提供者。</span><span class="sxs-lookup"><span data-stu-id="f5404-123">You can use this option to direct unauthenticated callers to a choice of authentication providers.</span></span> <span data-ttu-id="f5404-124">若要使用此選項，您必須撰寫程式碼來處理授權。</span><span class="sxs-lookup"><span data-stu-id="f5404-124">With this option you have to write code to handle authorization.</span></span>
     
     <span data-ttu-id="f5404-125">如需詳細資訊，請參閱 [Azure App Service 中的 API Apps 驗證與授權](app-service-api-authentication.md#multiple-protection-options)。</span><span class="sxs-lookup"><span data-stu-id="f5404-125">For more information, see [Authentication and authorization for API Apps in Azure App Service](app-service-api-authentication.md#multiple-protection-options).</span></span>
4. <span data-ttu-id="f5404-126">選取一或多個 [驗證提供者] 。</span><span class="sxs-lookup"><span data-stu-id="f5404-126">Select one or more of the **Authentication Providers**.</span></span>
   
    <span data-ttu-id="f5404-127">下圖顯示要求所有呼叫端要由 Azure AD 進行驗證的選項。</span><span class="sxs-lookup"><span data-stu-id="f5404-127">The image shows    choices that require all callers to be authenticated by Azure AD.</span></span>
   
    ![Azure 入口網站驗證/授權刀鋒視窗](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
   
    <span data-ttu-id="f5404-129">當您選擇驗證提供者後，入口網站會顯示該提供者的設定刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f5404-129">When you choose an authentication provider, the portal displays a configuration blade for that provider.</span></span> 
   
    <span data-ttu-id="f5404-130">如需說明如何設定驗證提供者設定刀鋒視窗的詳細指示，請參閱[如何設定 App Service 應用程式使用 Azure Active Directory 登入](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="f5404-130">For detailed instructions that explain how to configure the authentication provider configuration blades, see [How to configure your App Service application to use Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span> <span data-ttu-id="f5404-131">(此連結會移至有關 Azure AD 的文章，但該文章本身含有連往其他驗證提供者之文章的索引標籤)。</span><span class="sxs-lookup"><span data-stu-id="f5404-131">(The link goes to an article about Azure AD, but the article itself contains tabs that link to articles for the other authentication providers.)</span></span>
5. <span data-ttu-id="f5404-132">[驗證提供者設定] 刀鋒視窗使用完畢時，按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f5404-132">When you're done with the authentication provider configuration blade, click **OK**.</span></span>
6. <span data-ttu-id="f5404-133">在 [驗證/授權] 刀鋒視窗中，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="f5404-133">In the **Authentication / Authorization** blade, click **Save**.</span></span>

<span data-ttu-id="f5404-134">完成此作業後，App Service 就會先驗證 API 呼叫再讓其觸達 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-134">When this is done, App Service authenticates all API calls before they reach the API app.</span></span> <span data-ttu-id="f5404-135">凡是 App Service 所支援的語言 (包括 .NET、Node.js 和 Java)，驗證服務的運作方式都相同。</span><span class="sxs-lookup"><span data-stu-id="f5404-135">The authentication services work the same for all languages that App service supports, including .NET, Node.js, and Java.</span></span> 

<span data-ttu-id="f5404-136">為了讓 API 呼叫受到驗證，呼叫端會在 HTTP 要求的 Authorization 標頭中包含驗證提供者的 OAuth 2.0 持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="f5404-136">To make authenticated API calls, the caller includes the authentication provider's OAuth 2.0 bearer token in the Authorization header of HTTP requests.</span></span> <span data-ttu-id="f5404-137">若要取得權杖，請使用驗證提供者的 SDK。</span><span class="sxs-lookup"><span data-stu-id="f5404-137">The token can be acquired by using the authentication provider's SDK.</span></span>

## <span data-ttu-id="f5404-138"><a id="tutorialstart"></a> 繼續進行 .NET API Apps 教學課程</span><span class="sxs-lookup"><span data-stu-id="f5404-138"><a id="tutorialstart"></a> Continuing the .NET API Apps tutorials</span></span>
<span data-ttu-id="f5404-139">如果您要遵循適用於 API 應用程式的 Node.js 或 Java 教學課程，請跳至下一節 [API Apps 的服務主體驗證](app-service-api-dotnet-service-principal-auth.md)。</span><span class="sxs-lookup"><span data-stu-id="f5404-139">If you are following the Node.js or Java tutorials for API apps, skip to the next article, [service principal authentication for API apps](app-service-api-dotnet-service-principal-auth.md).</span></span> 

<span data-ttu-id="f5404-140">如果您要遵循適用於 API 應用程式的 .NET 教學課程系列，並已依照[第一個](app-service-api-dotnet-get-started.md)和[第二個](app-service-api-cors-consume-javascript.md)教學課程中的指示部署範例應用程式，請跳至在 [App Service 和 Azure AD 中設定驗證](#azureauth)一節。</span><span class="sxs-lookup"><span data-stu-id="f5404-140">If you are following the .NET tutorial series for API apps and have already deployed the sample application as directed in the [first](app-service-api-dotnet-get-started.md) and [second](app-service-api-cors-consume-javascript.md) tutorials, skip to the [Set up authentication in App Service and Azure AD](#azureauth) section.</span></span>

<span data-ttu-id="f5404-141">如果您想要遵循此教學課程，但又不想進行第一個和第二個教學課程，請進行下列步驟，其將會說明如何開始使用自動化程序來部署範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-141">If you want to follow this tutorial without going through the first and second tutorials, do the following steps which explain how to get started by using an automated process to deploy the sample application.</span></span>

> [!NOTE]
> <span data-ttu-id="f5404-142">下列步驟會讓您的起始點就彷彿已完成前兩個教學課程一樣，只有一點例外︰Visual Studio 不會知道每個專案部署至哪些 Web 應用程式或 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-142">The following steps get you to the same starting point as if you did the first two tutorials, with one exception: Visual Studio won't already know which web app or API app that each project gets deployed to.</span></span> <span data-ttu-id="f5404-143">這表示此教學課程中不會有說明如何部署至正確目標的確切指示。</span><span class="sxs-lookup"><span data-stu-id="f5404-143">That means you won't have exact instructions in this tutorial that explain how to deploy to the right targets.</span></span> <span data-ttu-id="f5404-144">如果您不熟悉該如何找出自行進行部署步驟的方式，您最好遵循 [第一個教學課程](app-service-api-dotnet-get-started.md) 中的教學課程系列，而非從這個自動化部署程序來開始。</span><span class="sxs-lookup"><span data-stu-id="f5404-144">If you're not comfortable with figuring out how to do the deployment steps on your own, it's better to follow the tutorial series from the [first tutorial](app-service-api-dotnet-get-started.md) than to start with this automated deployment process.</span></span>
> 
> 

1. <span data-ttu-id="f5404-145">請確定您有 [第一個教學課程](app-service-api-dotnet-get-started.md)中所列的所有必要條件。</span><span class="sxs-lookup"><span data-stu-id="f5404-145">Make sure that you have all of the prerequisites listed in the [first tutorial](app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="f5404-146">除了所列的必要條件之外，這些驗證教學課程還假設您已在 Visual Studio 和 Azure 入口網站中使用 App Service Web 應用程式和 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-146">In addition to the prerequisites listed, these authentication tutorials assume that you have worked with App Service web apps and API apps in Visual Studio and the Azure portal.</span></span>
2. <span data-ttu-id="f5404-147">按一下 [To Do List 範例儲存機制的讀我檔案](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md)中的 [部署至 Azure] 按鈕，部署 API 應用程式和 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-147">Click the **Deploy to Azure** button in the [To Do List sample repository readme file](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md) to deploy the API apps and the web app.</span></span> <span data-ttu-id="f5404-148">記下所建立的 Azure 資源群組，因為您稍後可以使用它來查閱 Web 應用程式和 API 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="f5404-148">Make a note of the Azure resource group that gets created, as you can use this later to look up web app and API app names.</span></span>
3. <span data-ttu-id="f5404-149">下載或複製 [To Do List 範例儲存機制](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) ，以取得您將在 Visual Studio 中本機使用的程式碼。</span><span class="sxs-lookup"><span data-stu-id="f5404-149">Download or clone the [To Do List sample repository](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) to get the code that you'll work with locally in Visual Studio.</span></span>

## <span data-ttu-id="f5404-150"><a id="azureauth"></a> 在 App Service 和 Azure AD 中設定驗證</span><span class="sxs-lookup"><span data-stu-id="f5404-150"><a id="azureauth"></a> Set up authentication in App Service and Azure AD</span></span>
<span data-ttu-id="f5404-151">您現在已擁有在 Azure App Service 中執行、且不需要使用者接受驗證的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-151">You now have the application running in Azure App Service without requiring that users be authenticated.</span></span> <span data-ttu-id="f5404-152">在本節中，您將執行下列工作來新增驗證機制：</span><span class="sxs-lookup"><span data-stu-id="f5404-152">In this section you add authentication by doing the following tasks:</span></span>

* <span data-ttu-id="f5404-153">設定 App Service 以要求在呼叫中介層 API 應用程式時需要進行 Azure Active Directory (Azure AD) 驗證。</span><span class="sxs-lookup"><span data-stu-id="f5404-153">Configure App Service to require Azure Active Directory (Azure AD) authentication for calling the middle tier API app.</span></span>
* <span data-ttu-id="f5404-154">建立 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-154">Create an Azure AD application.</span></span>
* <span data-ttu-id="f5404-155">設定 Azure AD 應用程式，使其在登入後將持有人權杖傳送到 AngularJS 前端。</span><span class="sxs-lookup"><span data-stu-id="f5404-155">Configure the Azure AD application to send the bearer token after logon to the AngularJS front end.</span></span> 

<span data-ttu-id="f5404-156">如果您遵循教學課程指示進行時遇到問題，請參閱教學課程尾端的 [疑難排解](#troubleshooting) 一節。</span><span class="sxs-lookup"><span data-stu-id="f5404-156">If you run into problems while following the tutorial directions, see the [Troubleshooting](#troubleshooting) section at the end of the tutorial.</span></span> 

### <a name="configure-authentication-for-the-middle-tier-api-app"></a><span data-ttu-id="f5404-157">為中介層 API 應用程式設定驗證</span><span class="sxs-lookup"><span data-stu-id="f5404-157">Configure authentication for the middle tier API app</span></span>
1. <span data-ttu-id="f5404-158">在 [Azure 入口網站](https://portal.azure.com/)中，瀏覽至您想要為 ToDoListAPI 專案建立的 API 應用程式的 [設定] 刀鋒視窗，尋找 [功能] 區段，再按一下 [驗證/授權]。</span><span class="sxs-lookup"><span data-stu-id="f5404-158">In the [Azure portal](https://portal.azure.com/), navigate to the **Settings** blade of the API app that you created for the ToDoListAPI project, find the **Features** section, and then click **Authentication / Authorization**.</span></span>
   
    ![Azure 入口網站驗證/授權](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. <span data-ttu-id="f5404-160">在 [驗證/授權] 刀鋒視窗中，按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="f5404-160">In the **Authentication / Authorization** blade, click **On**.</span></span>
3. <span data-ttu-id="f5404-161">在 [要求未經驗證時所採取的動作] 下拉式清單中，選取 [登入 Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="f5404-161">In the **Action to take when request is not authenticated** drop-down list, select **Log in with Azure Active Directory**.</span></span>
   
    <span data-ttu-id="f5404-162">此選項可確保未經驗證的要求均無法觸達 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-162">This option ensures that no unauathenticated requests will reach the API app.</span></span> 
4. <span data-ttu-id="f5404-163">在 [驗證提供者] 底下，按一下 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="f5404-163">Under **Authentication Providers**, click **Azure Active Directory**.</span></span>
   
    ![Azure 入口網站驗證/授權刀鋒視窗](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. <span data-ttu-id="f5404-165">在 [Azure Active Directory 設定] 刀鋒視窗中，按一下 [快速]</span><span class="sxs-lookup"><span data-stu-id="f5404-165">In the **Azure Active Directory Settings** blade, click **Express**</span></span>
   
    ![Azure 入口網站驗證/授權表達選項](./media/app-service-api-dotnet-user-principal-auth/aadsettings.png)
   
    <span data-ttu-id="f5404-167">在使用 [快速] 選項時，App Service 可以自動在 Azure AD [租用戶](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant)中建立 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-167">With the **Express** option, App Service can automatically create an Azure AD application in your Azure AD [tenant](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant).</span></span> 
   
    <span data-ttu-id="f5404-168">您不必建立租用戶，因為每個 Azure 帳戶都會自動擁有一個。</span><span class="sxs-lookup"><span data-stu-id="f5404-168">You don't have to create a tenant, because every Azure account automatically has one.</span></span>
6. <span data-ttu-id="f5404-169">在 [管理模式] 下，按一下 **建立新的 AD 應用程式** \(如果尚未選取)，並記下 [建立應用程式] 文字方塊中的值；您稍後將在 Azure 傳統入口網站中查閱此 AAD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-169">Under **Management mode**, click **Create New AD App** if it isn't already selected, and notice the value that is in the **Create App** text box; you'll look up this AAD application in the Azure classic portal later.</span></span>
   
    ![Azure 入口網站 Azure AD 設定](./media/app-service-api-dotnet-user-principal-auth/aadsettings2.png)
   
    <span data-ttu-id="f5404-171">Azure 會自動在 Azure AD 租用戶中建立包含指示值的 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-171">Azure will automatically create an Azure AD application with the indicated name in your Azure AD tenant.</span></span> <span data-ttu-id="f5404-172">根據預設，Azure AD 應用程式的名稱會與 API 應用程式相同。</span><span class="sxs-lookup"><span data-stu-id="f5404-172">By default, the Azure AD application is named the same as the API app.</span></span> <span data-ttu-id="f5404-173">如有需要，也可以輸入不同名稱。</span><span class="sxs-lookup"><span data-stu-id="f5404-173">If you prefer, you can enter a different name.</span></span>
7. <span data-ttu-id="f5404-174">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f5404-174">Click **OK**.</span></span>
8. <span data-ttu-id="f5404-175">在 [驗證/授權] 刀鋒視窗中，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="f5404-175">In the **Authentication / Authorization** blade, click **Save**.</span></span>
   
    ![按一下 [Save] (儲存)。](./media/app-service-api-dotnet-user-principal-auth/authsave.png)

<span data-ttu-id="f5404-177">現在，只有 Azure AD 租用戶中的使用者可以呼叫 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-177">Now only users in your Azure AD tenant can call the API app.</span></span>

### <a name="optional-test-the-api-app"></a><span data-ttu-id="f5404-178">選擇性：測試 API 應用程式</span><span class="sxs-lookup"><span data-stu-id="f5404-178">Optional: Test the API app</span></span>
1. <span data-ttu-id="f5404-179">在瀏覽器中，移至 API 應用程式的 URL：在 Azure 入口網站的 [API 應用程式] 刀鋒視窗中，按一下 [URL] 下方的連結。</span><span class="sxs-lookup"><span data-stu-id="f5404-179">In a browser go to the URL of the API app: in the **API app** blade in the Azure portal, click the link under **URL**.</span></span>  
   
    <span data-ttu-id="f5404-180">由於未經驗證的要求不得觸達 API 應用程式，因此系統會將您重新導向至登入畫面。</span><span class="sxs-lookup"><span data-stu-id="f5404-180">You are redirected to a login screen because unauthenticated requests are not allowed to reach the API app.</span></span>
   
    <span data-ttu-id="f5404-181">如果瀏覽器移至 [已成功建立] 頁面，則表示瀏覽器可能已登入，若是如此，請開啟 InPrivate 或 Incognito 視窗並移至 API 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="f5404-181">If your browser goes to the "successfully created" page, the browser might already be logged on -- in that case, open an InPrivate or Incognito window and go to the API app's URL.</span></span>
2. <span data-ttu-id="f5404-182">在 Azure AD 租用戶中以使用者的認證進行登入。</span><span class="sxs-lookup"><span data-stu-id="f5404-182">Log on using credentials for a user in your Azure AD tenant.</span></span>
   
    <span data-ttu-id="f5404-183">登入後，[已成功建立] 頁面隨即出現在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="f5404-183">When you're logged on, the "successfully created" page appears in the browser.</span></span>
3. <span data-ttu-id="f5404-184">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="f5404-184">Close the browser.</span></span>

### <a name="configure-the-azure-ad-application"></a><span data-ttu-id="f5404-185">設定 Azure AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="f5404-185">Configure the Azure AD application</span></span>
<span data-ttu-id="f5404-186">當您設定了 Azure AD 驗證，App Service 就會為您建立 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-186">When you configured Azure AD authentication, App Service created an Azure AD application for you.</span></span> <span data-ttu-id="f5404-187">根據預設，新的 Azure AD 應用程式已設定為會將持有人權杖提供給 API 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="f5404-187">By default the new Azure AD application was configured to provide the bearer token to the API app's URL.</span></span> <span data-ttu-id="f5404-188">在本節中，您將會設定 Azure AD 應用程式，以將持有人權杖提供給 AngularJS 前端，而非直接提供給中介層 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-188">In this section you configure the Azure AD application to provide the bearer token to the AngularJS front end instead of directly to the middle tier API app.</span></span> <span data-ttu-id="f5404-189">AngularJS 前端會在呼叫 API 應用程式時，將權杖傳送到 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-189">The AngularJS front end will send the token to the API app when it calls the API app.</span></span>

> [!NOTE]
> <span data-ttu-id="f5404-190">為了盡可能簡化程序，本教學課程為前端和中介層 API 應用程式使用單一 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-190">To keep the process as simple as possible, this tutorial uses a single Azure AD application for both the front end and the middle tier API app.</span></span> <span data-ttu-id="f5404-191">另一個選項是使用兩個 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-191">Another option is to use two Azure AD applications.</span></span> <span data-ttu-id="f5404-192">在此情況下，您必須授與前端的 Azure AD 應用程式權限才能呼叫中介層的 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-192">In that case you would have to give the front end's Azure AD application permission to call the middle tier's Azure AD application.</span></span> <span data-ttu-id="f5404-193">此多重應用程式方法可讓您更精細地控制每一個層級的權限。</span><span class="sxs-lookup"><span data-stu-id="f5404-193">This multi-application approach would give you more granular control over permissions to each tier.</span></span>
> 
> 

1. <span data-ttu-id="f5404-194">在 [Azure 傳統入口網站](https://manage.windowsazure.com/)中，移至 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="f5404-194">In the [Azure classic portal](https://manage.windowsazure.com/), go to **Azure Active Directory**.</span></span>
   
   <span data-ttu-id="f5404-195">您必須使用傳統入口網站，因為現行的 Azure 入口網站尚未提供您需要存取的特定 Azure Active Directory 設定。</span><span class="sxs-lookup"><span data-stu-id="f5404-195">You have to use the classic portal because certain Azure Active Directory settings that you need access to are not yet available in the current Azure portal.</span></span>
2. <span data-ttu-id="f5404-196">在 [目錄]  索引標籤中，選取您的 AAD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="f5404-196">On the **Directory** tab, click your AAD tenant.</span></span>
   
   ![傳統入口網站的 Azure AD](./media/app-service-api-dotnet-user-principal-auth/selecttenant.png)
3. <span data-ttu-id="f5404-198">按一下 [應用程式] > [我的公司擁有的應用程式]，然後按一下核取記號。</span><span class="sxs-lookup"><span data-stu-id="f5404-198">Click **Applications > Applications my company owns**, and then click the check mark.</span></span>
   
   <span data-ttu-id="f5404-199">您可能還必須重新整理頁面，才能看見新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-199">You might also have to refresh the page to see the new application.</span></span>
4. <span data-ttu-id="f5404-200">在應用程式清單中，按一下當您針對 API 應用程式啟用驗證時 Azure 為您建立的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="f5404-200">In the list of applications, click the name of the one that Azure created for you when you enabled authentication for your API app.</span></span>
   
   ![Azure AD [應用程式] 索引標籤](./media/app-service-api-dotnet-user-principal-auth/appstab.png)
5. <span data-ttu-id="f5404-202">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="f5404-202">Click **Configure**.</span></span>
   
   ![Azure AD [設定] 索引標籤](./media/app-service-api-dotnet-user-principal-auth/configure.png)
6. <span data-ttu-id="f5404-204">將 [登入 URL]  設定為 AngularJS Web 應用程式的 URL，且結尾不要有斜線。</span><span class="sxs-lookup"><span data-stu-id="f5404-204">Set **Sign-on URL** to the URL for your AngularJS web app, no trailing slash.</span></span>
   
   <span data-ttu-id="f5404-205">例如：https://todolistangular.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="f5404-205">For example: https://todolistangular.azurewebsites.net</span></span>
   
   ![登入 URL](./media/app-service-api-dotnet-user-principal-auth/signonurlazure.png)
7. <span data-ttu-id="f5404-207">將 [回覆 URL]  設定為 Web 應用程式的 URL，且結尾不要有斜線。</span><span class="sxs-lookup"><span data-stu-id="f5404-207">Set **Reply URL** to the URL for your web app, no trailing slash.</span></span>
   
   <span data-ttu-id="f5404-208">例如：https://todolistsangular.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="f5404-208">For example: https://todolistsangular.azurewebsites.net</span></span>
8. <span data-ttu-id="f5404-209">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="f5404-209">Click **Save**.</span></span>
   
   ![回覆 URL](./media/app-service-api-dotnet-user-principal-auth/replyurlazure.png)
9. <span data-ttu-id="f5404-211">在頁面底部，按一下 [管理資訊清單] > [下載資訊清單]。</span><span class="sxs-lookup"><span data-stu-id="f5404-211">At the bottom of the page, click **Manage manifest > Download manifest**.</span></span>
   
   ![下載資訊清單](./media/app-service-api-dotnet-user-principal-auth/downloadmanifest.png)
10. <span data-ttu-id="f5404-213">將檔案下載至可在其中編輯它的位置。</span><span class="sxs-lookup"><span data-stu-id="f5404-213">Download the file to a location where you can edit it.</span></span>
11. <span data-ttu-id="f5404-214">在下載的資訊清單檔案中，搜尋 `oauth2AllowImplicitFlow` 屬性。</span><span class="sxs-lookup"><span data-stu-id="f5404-214">In the downloaded manifest file, search for the  `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="f5404-215">將這個屬性的值從 `false` 變更為 `true`，然後儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="f5404-215">Change the value of this property from `false` to `true`, and then save the file.</span></span>
    
    <span data-ttu-id="f5404-216">必須要有這項設定才能從 JavaScript 單一頁面應用程式進行存取。</span><span class="sxs-lookup"><span data-stu-id="f5404-216">This setting is required for access from a JavaScript single-page application.</span></span> <span data-ttu-id="f5404-217">它可讓 Oauth 2.0 持有人權杖傳回 URL 片段中。</span><span class="sxs-lookup"><span data-stu-id="f5404-217">It enables the Oauth 2.0 bearer token to be returned in the URL fragment.</span></span>
12. <span data-ttu-id="f5404-218">按一下 [管理資訊清單] > [上傳資訊清單]，然後上傳您在上述步驟中更新的檔案。</span><span class="sxs-lookup"><span data-stu-id="f5404-218">Click **Manage manifest > Upload manifest**, and upload the file that you updated in the preceding step.</span></span>
    
    ![上傳資訊清單](./media/app-service-api-dotnet-user-principal-auth/uploadmanifest.png)
13. <span data-ttu-id="f5404-220">複製 [用戶端識別碼]  值，並將其儲存至可在稍後取得此值的位置。</span><span class="sxs-lookup"><span data-stu-id="f5404-220">Copy the **Client ID** value and save it somewhere you can get it from later.</span></span>

## <a name="configure-the-todolistangular-project-to-use-authentication"></a><span data-ttu-id="f5404-221">設定 ToDoListAngular 專案以使用驗證</span><span class="sxs-lookup"><span data-stu-id="f5404-221">Configure the ToDoListAngular project to use authentication</span></span>
<span data-ttu-id="f5404-222">在本節中，您將會變更 AngularJS 前端，使其使用 JS 適用的 Active Directory 驗證程式庫 (ADAL)，從 Azure AD 取得登入使用者的持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="f5404-222">In this section you change the AngularJS front end so that it uses Active Directory Authentication Library (ADAL) for JS to acquire a bearer token for the logged-on user from Azure AD.</span></span> <span data-ttu-id="f5404-223">程式碼會將權杖包含在傳送至中介層的 HTTP 要求中，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="f5404-223">The code will include the token in HTTP requests sent to the middle tier, as shown in the following diagram.</span></span> 

![使用者驗證圖表](./media/app-service-api-dotnet-user-principal-auth/appdiagram.png)

<span data-ttu-id="f5404-225">對 ToDoListAngular 專案中的檔案進行下列變更。</span><span class="sxs-lookup"><span data-stu-id="f5404-225">Make the following changes to files in the ToDoListAngular project.</span></span>

1. <span data-ttu-id="f5404-226">開啟 *index.cshtml* 檔。</span><span class="sxs-lookup"><span data-stu-id="f5404-226">Open the *index.cshtml* file.</span></span>
2. <span data-ttu-id="f5404-227">將參考 JS 適用的 Active Directory 驗證程式庫 (ADAL) 指令碼的程式行取消註解。</span><span class="sxs-lookup"><span data-stu-id="f5404-227">Uncomment the lines that reference the Active Directory Authentication Library (ADAL) for JS scripts.</span></span>
   
        <script src="app/scripts/adal.js"></script>
        <script src="app/scripts/adal-angular.js"></script>
3. <span data-ttu-id="f5404-228">開啟 *app/scripts/app.js* 檔案。</span><span class="sxs-lookup"><span data-stu-id="f5404-228">Open the *app/scripts/app.js* file.</span></span>
4. <span data-ttu-id="f5404-229">將標記為「不需要驗證」的程式碼區塊註解化，並將標記為「需要驗證」的程式碼區塊取消註解。</span><span class="sxs-lookup"><span data-stu-id="f5404-229">Comment out the block of code marked for "without authentication" and uncomment the block of code marked for "with authentication".</span></span>
   
    <span data-ttu-id="f5404-230">這項變更會參考 ADAL JS 驗證提供者，並為其提供設定值。</span><span class="sxs-lookup"><span data-stu-id="f5404-230">This change references the ADAL JS authentication provider and provides configuration values to it.</span></span> <span data-ttu-id="f5404-231">在下列步驟中，您會設定 API 應用程式和 Azure AD 應用程式的設定值。</span><span class="sxs-lookup"><span data-stu-id="f5404-231">In the following steps you set the configuration values for your API app and Azure AD application.</span></span>
5. <span data-ttu-id="f5404-232">在設定 `endpoints` 變數的程式碼中，將 API URL 設定為您為 ToDoListAPI 專案建立之 API 應用程式的 URL，並將 Azure AD 應用程式識別碼設定為您從 Azure 傳統入口網站複製而來的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="f5404-232">In the code that sets the `endpoints` variable, set the API URL to the URL of the API app that you created for the ToDoListAPI project, and set the Azure AD application ID to the client ID that you copied from the Azure classic portal.</span></span>
   
    <span data-ttu-id="f5404-233">程式碼現在類似下列範例。</span><span class="sxs-lookup"><span data-stu-id="f5404-233">The code is now similar to the following example.</span></span>
   
        var endpoints = {
            "https://todolistapi0121.azurewebsites.net/": "1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3"
        };
6. <span data-ttu-id="f5404-234">在 `adalProvider.init` 的呼叫中，將 `tenant` 設定為租用戶名稱，並將 `clientId` 設定為您在上一個步驟中使用的相同值。</span><span class="sxs-lookup"><span data-stu-id="f5404-234">In the call to `adalProvider.init`, set `tenant` to your tenant name and `clientId` to same value you used in the previous step.</span></span>
   
    <span data-ttu-id="f5404-235">程式碼現在類似下列範例。</span><span class="sxs-lookup"><span data-stu-id="f5404-235">The code is now similar to the following example.</span></span>
   
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
   
    <span data-ttu-id="f5404-236">這些 `app.js` 變更會指定讓呼叫端程式碼和接受呼叫的 API 位於相同的 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-236">These changes to `app.js` specify that the calling code and the called API are in the same Azure AD application.</span></span>
7. <span data-ttu-id="f5404-237">開啟 *app/scripts/homeCtrl.js* 檔案。</span><span class="sxs-lookup"><span data-stu-id="f5404-237">Open the *app/scripts/homeCtrl.js* file.</span></span>
8. <span data-ttu-id="f5404-238">將標記為「不需要驗證」的程式碼區塊註解化，並將標記為「需要驗證」的程式碼區塊取消註解。</span><span class="sxs-lookup"><span data-stu-id="f5404-238">Comment out the block of code marked for "without authentication" and uncomment the block of code marked for "with authentication".</span></span>
9. <span data-ttu-id="f5404-239">開啟 *app/scripts/indexCtrl.js* 檔案。</span><span class="sxs-lookup"><span data-stu-id="f5404-239">Open the *app/scripts/indexCtrl.js* file.</span></span>
10. <span data-ttu-id="f5404-240">將標記為「不需要驗證」的程式碼區塊註解化，並將標記為「需要驗證」的程式碼區塊取消註解。</span><span class="sxs-lookup"><span data-stu-id="f5404-240">Comment out the block of code marked for "without authentication" and uncomment the block of code marked for "with authentication".</span></span>

### <a name="deploy-the-todolistangular-project-to-azure"></a><span data-ttu-id="f5404-241">將 ToDoListAngular 專案部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="f5404-241">Deploy the ToDoListAngular project to Azure</span></span>
1. <span data-ttu-id="f5404-242">在 [方案總管] 中，以滑鼠右鍵按一下 ToDoListAngular 專案，然後按一下 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="f5404-242">In **Solution Explorer**, right-click the ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="f5404-243">按一下 [發行] 。</span><span class="sxs-lookup"><span data-stu-id="f5404-243">Click **Publish**.</span></span>
   
    <span data-ttu-id="f5404-244">Visual Studio 會部署專案並將瀏覽器開啟至 Web 應用程式的基底 URL。</span><span class="sxs-lookup"><span data-stu-id="f5404-244">Visual Studio deploys the project and opens a browser to the web app's base URL.</span></span> <span data-ttu-id="f5404-245">這會顯示 403 錯誤頁面，這是嘗試從瀏覽器移至 Web API 基底 URL 時的正常現象。</span><span class="sxs-lookup"><span data-stu-id="f5404-245">This will show a 403 error page, which is normal for an attempt to go to a Web API base URL from a browser.</span></span>
   
    <span data-ttu-id="f5404-246">您還需要變更中介層 API 應用程式，才能測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-246">You still have to make a change to the middle tier API app before you can test the application.</span></span>
3. <span data-ttu-id="f5404-247">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="f5404-247">Close the browser.</span></span>

## <a name="configure-the-todolistapi-project-to-use-authentication"></a><span data-ttu-id="f5404-248">設定 ToDoListAPI 專案以使用驗證</span><span class="sxs-lookup"><span data-stu-id="f5404-248">Configure the ToDoListAPI project to use authentication</span></span>
<span data-ttu-id="f5404-249">ToDoListAPI 專案目前會將 "*" 作為 `owner` 值傳送到 ToDoListDataAPI。</span><span class="sxs-lookup"><span data-stu-id="f5404-249">Currently the ToDoListAPI project sends "*" as the `owner` value to ToDoListDataAPI.</span></span> <span data-ttu-id="f5404-250">在本節中，您將會變更用來傳送登入使用者識別碼的程式碼。</span><span class="sxs-lookup"><span data-stu-id="f5404-250">In this section you change the code to send the ID of the logged-on user.</span></span>

<span data-ttu-id="f5404-251">對 ToDoListAPI 專案進行下列變更。</span><span class="sxs-lookup"><span data-stu-id="f5404-251">Make the following changes in the ToDoListAPI project.</span></span>

1. <span data-ttu-id="f5404-252">開啟 Controllers/ToDoListController.cs 檔案，並將每個動作方法中會把 `owner` 設定為 Azure AD `NameIdentifier` 宣告值的程式行取消註解。</span><span class="sxs-lookup"><span data-stu-id="f5404-252">Open the *Controllers/ToDoListController.cs* file, and uncomment the line in each action method that sets `owner` to the Azure AD `NameIdentifier` claim value.</span></span> <span data-ttu-id="f5404-253">例如：</span><span class="sxs-lookup"><span data-stu-id="f5404-253">For example:</span></span>
   
        owner = ((ClaimsIdentity)User.Identity).FindFirst(ClaimTypes.NameIdentifier).Value;
   
    <span data-ttu-id="f5404-254">**重要**︰不要取消註解 `ToDoListDataAPI` 方法中的程式碼；您稍後將在服務主體驗證教學課程中執行它。</span><span class="sxs-lookup"><span data-stu-id="f5404-254">**Important**: Don't uncomment code in the `ToDoListDataAPI` method; you'll do that later for the service principal authentication tutorial.</span></span>

### <a name="deploy-the-todolistapi-project-to-azure"></a><span data-ttu-id="f5404-255">將 ToDoListAPI 專案部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="f5404-255">Deploy the ToDoListAPI project to Azure</span></span>
1. <span data-ttu-id="f5404-256">在 [方案總管]中，以滑鼠右鍵按一下 ToDoListAPI 專案，然後按一下 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="f5404-256">In **Solution Explorer**, right-click the ToDoListAPI project, and then click **Publish**.</span></span>
2. <span data-ttu-id="f5404-257">按一下 [發行] 。</span><span class="sxs-lookup"><span data-stu-id="f5404-257">Click **Publish**.</span></span>
   
    <span data-ttu-id="f5404-258">Visual Studio 會部署專案並將瀏覽器開啟至 API 應用程式的基底 URL。</span><span class="sxs-lookup"><span data-stu-id="f5404-258">Visual Studio deploys the project and opens a browser to the API app's base URL.</span></span>
3. <span data-ttu-id="f5404-259">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="f5404-259">Close the browser.</span></span>

### <a name="test-the-application"></a><span data-ttu-id="f5404-260">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="f5404-260">Test the application</span></span>
1. <span data-ttu-id="f5404-261">使用 HTTPS 而非 HTTP 移至 Web 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="f5404-261">Go to the URL of the web app, **using HTTPS, not HTTP**.</span></span>
2. <span data-ttu-id="f5404-262">按一下 [待辦事項清單]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f5404-262">Click the **To Do List** tab.</span></span>
   
    <span data-ttu-id="f5404-263">系統會提示您登入。</span><span class="sxs-lookup"><span data-stu-id="f5404-263">You are prompted to log in.</span></span>
3. <span data-ttu-id="f5404-264">使用 AAD 租用戶中使用者的認證進行登入。</span><span class="sxs-lookup"><span data-stu-id="f5404-264">Log in with the credentials of a user in your AAD tenant.</span></span>
4. <span data-ttu-id="f5404-265">[待辦事項清單]  頁面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="f5404-265">The **To Do List** page appears.</span></span>
   
   ![待辦事項清單頁面](./media/app-service-api-dotnet-user-principal-auth/webappindex.png)
   
   <span data-ttu-id="f5404-267">目前並不會顯示任何待辦事項項目，因為這些項目到目前為止全都適用於擁有者 "*"。</span><span class="sxs-lookup"><span data-stu-id="f5404-267">No to-do items are displayed because until now they have all been for owner "*".</span></span> <span data-ttu-id="f5404-268">現在中介層正在要求登入使用者的項目，但目前尚未建立任何項目。</span><span class="sxs-lookup"><span data-stu-id="f5404-268">Now the middle tier is requesting items for the logged-on user, and none have been created yet.</span></span>
5. <span data-ttu-id="f5404-269">新增待辦事項項目，以確認應用程式可以運作。</span><span class="sxs-lookup"><span data-stu-id="f5404-269">Add new to-do items to verify that the application is working.</span></span>
6. <span data-ttu-id="f5404-270">在另一個瀏覽器視窗中，移至 ToDoListDataAPI API 應用程式的 Swagger UI URL，並按一下 [ToDoList] > [取得]。</span><span class="sxs-lookup"><span data-stu-id="f5404-270">In another browser window, go to the Swagger UI URL for the ToDoListDataAPI API app and click **ToDoList > Get**.</span></span> <span data-ttu-id="f5404-271">輸入星號來代表 `owner` 參數，然後按一下 [立即試用]。</span><span class="sxs-lookup"><span data-stu-id="f5404-271">Enter an asterisk for the `owner` parameter, and then click **Try it out**.</span></span>
   
   <span data-ttu-id="f5404-272">回應顯示新的待辦事項項目在 Owner 屬性中擁有實際的 Azure AD 使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="f5404-272">The response shows that the new to-do items have the actual Azure AD user ID in the Owner property.</span></span>
   
   ![JSON 回應中的擁有者識別碼](./media/app-service-api-dotnet-user-principal-auth/todolistapiauth.png)

## <a name="building-the-projects-from-scratch"></a><span data-ttu-id="f5404-274">從頭建置專案</span><span class="sxs-lookup"><span data-stu-id="f5404-274">Building the projects from scratch</span></span>
<span data-ttu-id="f5404-275">兩個 Web API 專案是透過使用 Azure API 應用程式  專案範本並以 ToDoList 控制器取代預設值控制器所建立。</span><span class="sxs-lookup"><span data-stu-id="f5404-275">The two Web API projects were created by using the **Azure API App** project template and replacing the default Values controller with a ToDoList controller.</span></span> 

<span data-ttu-id="f5404-276">如需如何使用 Web API 2 後端建立 AngularJS 單一頁面應用程式的相關資訊，請參閱[實習實驗室：使用 ASP.NET Web API 和 Angular.js 建置單一頁面應用程式 (SPA)](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs)。</span><span class="sxs-lookup"><span data-stu-id="f5404-276">For information about how to  create an AngularJS single-page application with a Web API 2 back end, see  [Hands On Lab: Build a Single Page Application (SPA) with ASP.NET Web API and Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs).</span></span> <span data-ttu-id="f5404-277">如需如何新增 Azure AD 驗證程式碼的相關資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="f5404-277">For information about how to add Azure AD authentication code, see the following resources:</span></span>

* <span data-ttu-id="f5404-278">[使用 Azure AD 保護 AngularJS 單一頁面應用程式](../active-directory/active-directory-devquickstarts-angular.md)。</span><span class="sxs-lookup"><span data-stu-id="f5404-278">[Securing AngularJS Single Page Apps with Azure AD](../active-directory/active-directory-devquickstarts-angular.md).</span></span>
* [<span data-ttu-id="f5404-279">簡介 ADAL JS v1</span><span class="sxs-lookup"><span data-stu-id="f5404-279">Introducing ADAL JS v1</span></span>](http://www.cloudidentity.com/blog/2015/02/19/introducing-adal-js-v1/)

## <a name="troubleshooting"></a><span data-ttu-id="f5404-280">疑難排解</span><span class="sxs-lookup"><span data-stu-id="f5404-280">Troubleshooting</span></span>
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* <span data-ttu-id="f5404-281">請確定不要混淆 ToDoListAPI (中介層) 和 ToDoListDataAPI (資料層)。</span><span class="sxs-lookup"><span data-stu-id="f5404-281">Make sure that you don't confuse ToDoListAPI (middle tier) and ToDoListDataAPI (data tier).</span></span> <span data-ttu-id="f5404-282">例如，請確認將驗證新增至中介層 API 應用程式而非資料層。</span><span class="sxs-lookup"><span data-stu-id="f5404-282">For example, verify that you added authentication to the middle tier API app, not the data tier.</span></span> 
* <span data-ttu-id="f5404-283">請確定 AngularJS 原始碼其參考中介層 API 應用程式 URL (ToDoListAPI 而非 ToDoListDataAPI) 和正確的 Azure AD 用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="f5404-283">Make sure that the AngularJS source code references the middle tier API app URL (ToDoListAPI, not ToDoListDataAPI)and the correct Azure AD client ID.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f5404-284">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f5404-284">Next steps</span></span>
<span data-ttu-id="f5404-285">在本教學課程中，您已了解如何使用 API 應用程式的 App Service 驗證，以及如何利用 ADAL JS 程式庫呼叫 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5404-285">In this tutorial you learned how to use App Service authentication for an API app and how to call the API app by using the ADAL JS library.</span></span> <span data-ttu-id="f5404-286">在下一個教學課程中，您將學習如何 [對於服務對服務的案例保護您的 API 應用程式存取](app-service-api-dotnet-service-principal-auth.md)。</span><span class="sxs-lookup"><span data-stu-id="f5404-286">In the next tutorial you'll learn how to [secure access to your API app for service-to-service scenarios](app-service-api-dotnet-service-principal-auth.md).</span></span>

