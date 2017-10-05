---
title: "利用 Azure 入口網站開始使用 Azure AD 驗證 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站存取 Azure Active Directory (Azure AD) 驗證，以使用 Azure 媒體服務 API。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 829e0759f8aeb8758f6b8895b88b60b66ffb22ed
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-the-azure-portal"></a><span data-ttu-id="f8a97-103">利用 Azure 入口網站開始使用 Azure AD 驗證</span><span class="sxs-lookup"><span data-stu-id="f8a97-103">Get started with Azure AD authentication by using the Azure portal</span></span>

<span data-ttu-id="f8a97-104">了解如何使用 Azure 入口網站存取 Azure Active Directory (Azure AD) 驗證，以存取 Azure 媒體服務 API。</span><span class="sxs-lookup"><span data-stu-id="f8a97-104">Learn how to use the Azure portal to access Azure Active Directory (Azure AD) authentication to access the Azure Media Services API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8a97-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="f8a97-105">Prerequisites</span></span>

- <span data-ttu-id="f8a97-106">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f8a97-106">An Azure account.</span></span> <span data-ttu-id="f8a97-107">如果您沒有帳戶，請先從 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。</span><span class="sxs-lookup"><span data-stu-id="f8a97-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="f8a97-108">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="f8a97-108">A Media Services account.</span></span> <span data-ttu-id="f8a97-109">如需詳細資訊，請參閱[使用 Azure 入口網站建立 Azure 媒體服務帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="f8a97-109">For more information, see [Create an Azure Media Services account by using the Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="f8a97-110">請先複習[使用 Azure AD 驗證存取 Azure 媒體服務 API 概觀](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="f8a97-110">Make sure you review the [Accessing Azure Media Services API with Azure AD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="f8a97-111">當您使用 Azure AD 驗證搭配 Azure 媒體服務 時，會有兩個驗證選項：</span><span class="sxs-lookup"><span data-stu-id="f8a97-111">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span></span>

- <span data-ttu-id="f8a97-112">**使用者驗證**。</span><span class="sxs-lookup"><span data-stu-id="f8a97-112">**User authentication**.</span></span> <span data-ttu-id="f8a97-113">驗證使用應用程式與媒體服務資源互動的人員。</span><span class="sxs-lookup"><span data-stu-id="f8a97-113">Authenticate a person who is using the app to interact with Media Services resources.</span></span> <span data-ttu-id="f8a97-114">互動式應用程式應該會先提示使用者輸入認證。</span><span class="sxs-lookup"><span data-stu-id="f8a97-114">The interactive application should first prompt the user for credentials.</span></span> <span data-ttu-id="f8a97-115">例如，授權的使用者用來監控編碼工作或即時串流的管理主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f8a97-115">An example is a management console app used by authorized users to monitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="f8a97-116">**服務主體驗證**。</span><span class="sxs-lookup"><span data-stu-id="f8a97-116">**Service principal authentication**.</span></span> <span data-ttu-id="f8a97-117">驗證服務。</span><span class="sxs-lookup"><span data-stu-id="f8a97-117">Authenticate a service.</span></span> <span data-ttu-id="f8a97-118">通常使用這種驗證方法的應用程式有執行精靈服務、中介層服務或排程的工作的應用程式：Web 應用程式、函數應用程式、邏輯應用程式、API 或微服務。</span><span class="sxs-lookup"><span data-stu-id="f8a97-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs: web apps, function apps, logic apps, APIs, or a microservice.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8a97-119">目前，媒體服務支援 Azure 存取控制服務驗證模型。</span><span class="sxs-lookup"><span data-stu-id="f8a97-119">Currently, Media Services supports the Azure Access Control service authentication model.</span></span> <span data-ttu-id="f8a97-120">不過，存取控制授權將在 2018 年 6 月 1 日被取代。</span><span class="sxs-lookup"><span data-stu-id="f8a97-120">However, Access Control authorization will be deprecated on June 1, 2018.</span></span> <span data-ttu-id="f8a97-121">建議您儘速移轉至 Azure AD 驗證模型。</span><span class="sxs-lookup"><span data-stu-id="f8a97-121">We recommend that you migrate to the Azure AD authentication model as soon as possible.</span></span>

## <a name="select-the-authentication-method"></a><span data-ttu-id="f8a97-122">選取驗證方法</span><span class="sxs-lookup"><span data-stu-id="f8a97-122">Select the authentication method</span></span>

1. <span data-ttu-id="f8a97-123">在 [Azure 入口網站](https://portal.azure.com/)中，選取您的媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="f8a97-123">In the [Azure portal](https://portal.azure.com/), select your Media Services account.</span></span>
2. <span data-ttu-id="f8a97-124">選取如何連線到媒體服務 API。</span><span class="sxs-lookup"><span data-stu-id="f8a97-124">Select how to connect to the Media Services API.</span></span>

    ![選取連線方式的頁面](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a><span data-ttu-id="f8a97-126">使用者驗證</span><span class="sxs-lookup"><span data-stu-id="f8a97-126">User authentication</span></span>

<span data-ttu-id="f8a97-127">若要利用使用者驗證選項連線到媒體服務 API，用戶端應用程式必須要求具有下列參數的 Azure AD 權杖：</span><span class="sxs-lookup"><span data-stu-id="f8a97-127">To connect to the Media Services API by using the user authentication option, the client app needs to request an Azure AD token that has the following parameters:</span></span>  

* <span data-ttu-id="f8a97-128">Azure AD 租用戶端點</span><span class="sxs-lookup"><span data-stu-id="f8a97-128">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="f8a97-129">媒體服務資源 URI</span><span class="sxs-lookup"><span data-stu-id="f8a97-129">Media Services resource URI</span></span>
* <span data-ttu-id="f8a97-130">媒體服務 (原生) 應用程式用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="f8a97-130">Media Services (native) application client ID</span></span> 
* <span data-ttu-id="f8a97-131">媒體服務 (原生) 應用程式重新導向 URI</span><span class="sxs-lookup"><span data-stu-id="f8a97-131">Media Services (native) application redirect URI</span></span> 
* <span data-ttu-id="f8a97-132">REST 媒體服務的資源 URI</span><span class="sxs-lookup"><span data-stu-id="f8a97-132">Resource URI for REST Media Services</span></span>

<span data-ttu-id="f8a97-133">您可以在**使用使用者驗證的媒體服務 API**取得這些參數的值。</span><span class="sxs-lookup"><span data-stu-id="f8a97-133">You can get the values for these parameters on the **Media Services API with user authentication** page.</span></span> 

![使用使用者驗證頁面連線](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

<span data-ttu-id="f8a97-135">如果您使用媒體服務的 Microsoft .NET SDK 連線到媒體服務 API，此 SDK 會提供您所需的值。</span><span class="sxs-lookup"><span data-stu-id="f8a97-135">If you connect to the Media Services API by using the Media Services Microsoft .NET SDK, the required values are available to you as part of the SDK.</span></span> <span data-ttu-id="f8a97-136">如需詳細資訊，請參閱[使用 Azure AD 驗證搭配 .NET 存取 Azure 媒體服務 API](media-services-dotnet-get-started-with-aad.md)。</span><span class="sxs-lookup"><span data-stu-id="f8a97-136">For more information, see [Use Azure AD authentication to access the Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="f8a97-137">如果您不是使用媒體服務 .NET 用戶端 SDK，您必須使用先前討論的參數手動建立 Azure AD 權杖要求。</span><span class="sxs-lookup"><span data-stu-id="f8a97-137">If you're not using the Media Services .NET client SDK, you must manually create an Azure AD token request by using the parameters discussed earlier.</span></span> <span data-ttu-id="f8a97-138">如需詳細資訊，請參閱[如何使用 Azure AD 驗證程式庫取得 Azure AD 權杖](../active-directory/develop/active-directory-authentication-libraries.md)。</span><span class="sxs-lookup"><span data-stu-id="f8a97-138">For more information, see [How to use the Azure AD Authentication Library to get the Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

## <a name="service-principal-authentication"></a><span data-ttu-id="f8a97-139">服務主體驗證</span><span class="sxs-lookup"><span data-stu-id="f8a97-139">Service principal authentication</span></span>

<span data-ttu-id="f8a97-140">若要利用服務主體選項連線到媒體服務 API，您的中介層應用程式 (Web API 或 Web 應用程式) 必須要求具有下列參數的 Azure AD 權杖：</span><span class="sxs-lookup"><span data-stu-id="f8a97-140">To connect to the Media Services API by using the service principal option, your middle-tier app (web API or web application) needs to request an Azure AD token that has the following parameters:</span></span>  

* <span data-ttu-id="f8a97-141">Azure AD 租用戶端點</span><span class="sxs-lookup"><span data-stu-id="f8a97-141">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="f8a97-142">媒體服務資源 URI</span><span class="sxs-lookup"><span data-stu-id="f8a97-142">Media Services resource URI</span></span> 
* <span data-ttu-id="f8a97-143">REST 媒體服務的資源 URI</span><span class="sxs-lookup"><span data-stu-id="f8a97-143">Resource URI for REST Media Services</span></span>
* <span data-ttu-id="f8a97-144">Azure AD 應用程式的值：**用戶端識別碼**和**用戶端祕密**</span><span class="sxs-lookup"><span data-stu-id="f8a97-144">Azure AD application values: the **client ID** and **client secret**</span></span>

<span data-ttu-id="f8a97-145">您可以在**使用服務主體連線到媒體服務 API** 頁面取得這些參數的值。</span><span class="sxs-lookup"><span data-stu-id="f8a97-145">You can get the values for these parameters on the **Connect to Media Services API with service principal** page.</span></span> <span data-ttu-id="f8a97-146">使用此頁面可建立新的 Azure AD 應用程式或選取現有的 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f8a97-146">Use this page to create a new Azure AD application or to select an existing one.</span></span> <span data-ttu-id="f8a97-147">選取 Azure AD 應用程式之後，您可以取得用戶端識別碼 (應用程式識別碼)，並產生用戶端祕密 (金鑰) 值。</span><span class="sxs-lookup"><span data-stu-id="f8a97-147">After you select the Azure AD app, you can get the client ID (Application ID) and generate the client secret (key) values.</span></span> 

![使用服務主體連線的頁面](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

<span data-ttu-id="f8a97-149">當服務主體的刀鋒視窗開啟時，會選取符合下列準則的第一個 Azure AD 應用程式：</span><span class="sxs-lookup"><span data-stu-id="f8a97-149">When the **Service Principal** blade opens, the first Azure AD application that meets the following criteria is selected:</span></span>

- <span data-ttu-id="f8a97-150">它是已註冊的 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f8a97-150">It is a registered Azure AD application.</span></span>
- <span data-ttu-id="f8a97-151">它對帳戶具有參與者或擁有者角色型存取控制權限。</span><span class="sxs-lookup"><span data-stu-id="f8a97-151">It has Contributor or Owner Role-Based Access Control permissions on the account.</span></span>

<span data-ttu-id="f8a97-152">建立或選取 Azure AD 應用程式之後，您可以建立並複製用戶端祕密 (金鑰) 和用戶端識別碼 (應用程式識別碼)。</span><span class="sxs-lookup"><span data-stu-id="f8a97-152">After you create or select an Azure AD app, you can create and copy a client secret (key) and the client ID (Application ID).</span></span> <span data-ttu-id="f8a97-153">在此案例中，需要有用戶端祕密和用戶端識別碼才能取得存取權杖。</span><span class="sxs-lookup"><span data-stu-id="f8a97-153">The client secret and client ID are required to get the access token in this scenario.</span></span>

<span data-ttu-id="f8a97-154">如果您沒有在網域中建立 Azure AD 應用程式的權限，則不會顯示此刀鋒視窗的 Azure AD 應用程式控制項，並會顯示警告訊息。</span><span class="sxs-lookup"><span data-stu-id="f8a97-154">If you don't have permissions to create Azure AD apps in your domain, the Azure AD app controls of the blade are not shown, and a warning message is displayed.</span></span>

<span data-ttu-id="f8a97-155">如果您使用媒體服務 .NET SDK 連線到媒體服務 API，請參閱[使用 Azure AD 驗證搭配 .NET 存取 Azure 媒體服務 API](media-services-dotnet-get-started-with-aad.md)。</span><span class="sxs-lookup"><span data-stu-id="f8a97-155">If you connect to the Media Services API by using the Media Services .NET SDK, see [Use Azure AD authentication to access the Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="f8a97-156">如果您不是使用媒體服務 .NET 用戶端 SDK，您必須使用先前討論的參數手動建立 Azure AD 權杖要求。</span><span class="sxs-lookup"><span data-stu-id="f8a97-156">If you are not using the Media Services .NET client SDK, you must manually create an Azure AD token request using the parameters discussed earlier.</span></span> <span data-ttu-id="f8a97-157">如需詳細資訊，請參閱[如何使用 Azure AD 驗證程式庫取得 Azure AD 權杖](../active-directory/develop/active-directory-authentication-libraries.md)。</span><span class="sxs-lookup"><span data-stu-id="f8a97-157">For more information, see [How to use the Azure AD Authentication Library to get the Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

### <a name="get-the-client-id-and-client-secret"></a><span data-ttu-id="f8a97-158">取得用戶端識別碼和用戶端祕密</span><span class="sxs-lookup"><span data-stu-id="f8a97-158">Get the client ID and client secret</span></span>

<span data-ttu-id="f8a97-159">選取現有的 Azure AD 應用程式或選取建立新的 Azure AD 應用程式的選項後，會顯示下列按鈕：</span><span class="sxs-lookup"><span data-stu-id="f8a97-159">After you select an existing Azure AD app or select the option to create a new one, the following buttons appear:</span></span>

![[Manage permissions] \(管理權限\) 和 [Manage application] \(管理應用程式\) 按鈕](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

<span data-ttu-id="f8a97-161">若要開啟 Azure AD 應用程式刀鋒視窗，請按一下 [Manage application] \(管理應用程式\)。</span><span class="sxs-lookup"><span data-stu-id="f8a97-161">To open the Azure AD application blade, click **Manage application**.</span></span> <span data-ttu-id="f8a97-162">在 [Manage application] \(管理應用程式\) 刀鋒視窗中，您可以取得應用程式的用戶端識別碼 (應用程式識別碼)。</span><span class="sxs-lookup"><span data-stu-id="f8a97-162">On the **Manage application** blade, you can get the app's client ID (Application ID).</span></span> <span data-ttu-id="f8a97-163">若要產生用戶端祕密 (金鑰)，請選取 [金鑰]。</span><span class="sxs-lookup"><span data-stu-id="f8a97-163">To generate a client secret (key), select **Keys**.</span></span>

![管理應用程式刀鋒視窗的 [Keys] \(金鑰\) 選項](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-the-application"></a><span data-ttu-id="f8a97-165">管理權限和應用程式</span><span class="sxs-lookup"><span data-stu-id="f8a97-165">Manage permissions and the application</span></span>

<span data-ttu-id="f8a97-166">選取 Azure AD 應用程式之後，您可以管理應用程式和權限。</span><span class="sxs-lookup"><span data-stu-id="f8a97-166">After you select the Azure AD application, you can manage the application and permissions.</span></span> <span data-ttu-id="f8a97-167">若要設定您的 Azure AD 應用程式以存取其他應用程式，請按一下 [Manage permissions] \(管理權限\)。</span><span class="sxs-lookup"><span data-stu-id="f8a97-167">To set up your Azure AD application to access other applications, click **Manage permissions**.</span></span> <span data-ttu-id="f8a97-168">對於管理工作，例如變更金鑰和回覆 URL，或編輯應用程式的資訊清單，請按一下 [Manage application] \(管理應用程式\)。</span><span class="sxs-lookup"><span data-stu-id="f8a97-168">For management tasks, such as changing keys and reply URLs, or to edit the application’s manifest, click **Manage application**.</span></span>

### <a name="edit-the-apps-settings-or-manifest"></a><span data-ttu-id="f8a97-169">編輯應用程式的設定或資訊清單</span><span class="sxs-lookup"><span data-stu-id="f8a97-169">Edit the app's settings or manifest</span></span>

<span data-ttu-id="f8a97-170">若要編輯應用程式的設定或資訊清單，請按一下 [Manage application] \(管理應用程式\)。</span><span class="sxs-lookup"><span data-stu-id="f8a97-170">To edit the app's settings or manifest, click **Manage application**.</span></span>

![管理應用程式頁面](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a><span data-ttu-id="f8a97-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f8a97-172">Next steps</span></span>

<span data-ttu-id="f8a97-173">開始使用[上傳檔案至您的帳戶](media-services-portal-upload-files.md)。</span><span class="sxs-lookup"><span data-stu-id="f8a97-173">Get started with [uploading files to your account](media-services-portal-upload-files.md).</span></span>
