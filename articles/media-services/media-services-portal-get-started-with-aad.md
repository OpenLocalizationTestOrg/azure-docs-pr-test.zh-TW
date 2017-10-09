---
title: "aaaGet 使用 hello Azure 入口網站來啟動 Azure AD 驗證與 |Microsoft 文件"
description: "了解如何 toouse hello Azure 入口網站 tooaccess Azure Active Directory (Azure AD) 驗證 tooconsume hello Azure 媒體服務 API。"
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
ms.openlocfilehash: 497ad1806b3fd1262802adefb6e12b65ee9f2d61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-hello-azure-portal"></a><span data-ttu-id="94a1d-103">開始使用 Azure AD 驗證使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="94a1d-103">Get started with Azure AD authentication by using hello Azure portal</span></span>

<span data-ttu-id="94a1d-104">了解如何 toouse hello Azure 入口網站 tooaccess Azure Active Directory (Azure AD) 驗證 tooaccess hello Azure 媒體服務 API。</span><span class="sxs-lookup"><span data-stu-id="94a1d-104">Learn how toouse hello Azure portal tooaccess Azure Active Directory (Azure AD) authentication tooaccess hello Azure Media Services API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94a1d-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="94a1d-105">Prerequisites</span></span>

- <span data-ttu-id="94a1d-106">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="94a1d-106">An Azure account.</span></span> <span data-ttu-id="94a1d-107">如果您沒有帳戶，請先從 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。</span><span class="sxs-lookup"><span data-stu-id="94a1d-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="94a1d-108">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="94a1d-108">A Media Services account.</span></span> <span data-ttu-id="94a1d-109">如需詳細資訊，請參閱[使用 hello Azure 入口網站建立 Azure Media Services 帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="94a1d-109">For more information, see [Create an Azure Media Services account by using hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="94a1d-110">請確定您檢閱 hello[存取 Azure 媒體服務應用程式開發介面與 Azure AD 驗證概觀](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="94a1d-110">Make sure you review hello [Accessing Azure Media Services API with Azure AD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="94a1d-111">當您使用 Azure AD 驗證搭配 Azure 媒體服務 時，會有兩個驗證選項：</span><span class="sxs-lookup"><span data-stu-id="94a1d-111">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span></span>

- <span data-ttu-id="94a1d-112">**使用者驗證**。</span><span class="sxs-lookup"><span data-stu-id="94a1d-112">**User authentication**.</span></span> <span data-ttu-id="94a1d-113">驗證使用 hello 應用程式 toointeract 和媒體服務資源的人員。</span><span class="sxs-lookup"><span data-stu-id="94a1d-113">Authenticate a person who is using hello app toointeract with Media Services resources.</span></span> <span data-ttu-id="94a1d-114">hello 互動式應用程式應該會先提示 hello 使用者提供認證。</span><span class="sxs-lookup"><span data-stu-id="94a1d-114">hello interactive application should first prompt hello user for credentials.</span></span> <span data-ttu-id="94a1d-115">範例是由授權的使用者 toomonitor 編碼工作的主控台應用程式管理或即時資料流。</span><span class="sxs-lookup"><span data-stu-id="94a1d-115">An example is a management console app used by authorized users toomonitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="94a1d-116">**服務主體驗證**。</span><span class="sxs-lookup"><span data-stu-id="94a1d-116">**Service principal authentication**.</span></span> <span data-ttu-id="94a1d-117">驗證服務。</span><span class="sxs-lookup"><span data-stu-id="94a1d-117">Authenticate a service.</span></span> <span data-ttu-id="94a1d-118">通常使用這種驗證方法的應用程式有執行精靈服務、中介層服務或排程的工作的應用程式：Web 應用程式、函數應用程式、邏輯應用程式、API 或微服務。</span><span class="sxs-lookup"><span data-stu-id="94a1d-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs: web apps, function apps, logic apps, APIs, or a microservice.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94a1d-119">目前，Media Services 支援 hello Azure 存取控制服務驗證模型。</span><span class="sxs-lookup"><span data-stu-id="94a1d-119">Currently, Media Services supports hello Azure Access Control service authentication model.</span></span> <span data-ttu-id="94a1d-120">不過，存取控制授權將在 2018 年 6 月 1 日被取代。</span><span class="sxs-lookup"><span data-stu-id="94a1d-120">However, Access Control authorization will be deprecated on June 1, 2018.</span></span> <span data-ttu-id="94a1d-121">我們建議您儘速移轉 toohello Azure AD 驗證模型。</span><span class="sxs-lookup"><span data-stu-id="94a1d-121">We recommend that you migrate toohello Azure AD authentication model as soon as possible.</span></span>

## <a name="select-hello-authentication-method"></a><span data-ttu-id="94a1d-122">選取 hello 驗證方法</span><span class="sxs-lookup"><span data-stu-id="94a1d-122">Select hello authentication method</span></span>

1. <span data-ttu-id="94a1d-123">在 hello [Azure 入口網站](https://portal.azure.com/)，選取您的 Media Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="94a1d-123">In hello [Azure portal](https://portal.azure.com/), select your Media Services account.</span></span>
2. <span data-ttu-id="94a1d-124">選取如何 tooconnect toohello 媒體服務 API。</span><span class="sxs-lookup"><span data-stu-id="94a1d-124">Select how tooconnect toohello Media Services API.</span></span>

    ![選取連線方式的頁面](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a><span data-ttu-id="94a1d-126">使用者驗證</span><span class="sxs-lookup"><span data-stu-id="94a1d-126">User authentication</span></span>

<span data-ttu-id="94a1d-127">tooconnect toohello Media Services API 使用 hello 使用者驗證選項，hello 用戶端應用程式需要 toorequest 具有 hello 下列參數的 Azure AD 權杖：</span><span class="sxs-lookup"><span data-stu-id="94a1d-127">tooconnect toohello Media Services API by using hello user authentication option, hello client app needs toorequest an Azure AD token that has hello following parameters:</span></span>  

* <span data-ttu-id="94a1d-128">Azure AD 租用戶端點</span><span class="sxs-lookup"><span data-stu-id="94a1d-128">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="94a1d-129">媒體服務資源 URI</span><span class="sxs-lookup"><span data-stu-id="94a1d-129">Media Services resource URI</span></span>
* <span data-ttu-id="94a1d-130">媒體服務 (原生) 應用程式用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="94a1d-130">Media Services (native) application client ID</span></span> 
* <span data-ttu-id="94a1d-131">媒體服務 (原生) 應用程式重新導向 URI</span><span class="sxs-lookup"><span data-stu-id="94a1d-131">Media Services (native) application redirect URI</span></span> 
* <span data-ttu-id="94a1d-132">REST 媒體服務的資源 URI</span><span class="sxs-lookup"><span data-stu-id="94a1d-132">Resource URI for REST Media Services</span></span>

<span data-ttu-id="94a1d-133">您可以取得這些參數在 hello hello 值**Media Services API 的使用者驗證**頁面。</span><span class="sxs-lookup"><span data-stu-id="94a1d-133">You can get hello values for these parameters on hello **Media Services API with user authentication** page.</span></span> 

![使用使用者驗證頁面連線](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

<span data-ttu-id="94a1d-135">如果您使用 Media Services 的 Microsoft.NET SDK hello 連接 toohello Media Services API，hello 必要的值可用 tooyou hello SDK 的一部分。</span><span class="sxs-lookup"><span data-stu-id="94a1d-135">If you connect toohello Media Services API by using hello Media Services Microsoft .NET SDK, hello required values are available tooyou as part of hello SDK.</span></span> <span data-ttu-id="94a1d-136">如需詳細資訊，請參閱[使用 Azure AD 驗證 tooaccess hello 與.NET 的 Azure 媒體服務 API](media-services-dotnet-get-started-with-aad.md)。</span><span class="sxs-lookup"><span data-stu-id="94a1d-136">For more information, see [Use Azure AD authentication tooaccess hello Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="94a1d-137">如果您未使用 Media Services.NET 用戶端 hello SDK，所以您必須使用先前所討論的 hello 參數，手動建立的 Azure AD 的權杖要求。</span><span class="sxs-lookup"><span data-stu-id="94a1d-137">If you're not using hello Media Services .NET client SDK, you must manually create an Azure AD token request by using hello parameters discussed earlier.</span></span> <span data-ttu-id="94a1d-138">如需詳細資訊，請參閱[toouse hello Azure AD 驗證程式庫 tooget 如何 hello Azure AD 權杖](../active-directory/develop/active-directory-authentication-libraries.md)。</span><span class="sxs-lookup"><span data-stu-id="94a1d-138">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

## <a name="service-principal-authentication"></a><span data-ttu-id="94a1d-139">服務主體驗證</span><span class="sxs-lookup"><span data-stu-id="94a1d-139">Service principal authentication</span></span>

<span data-ttu-id="94a1d-140">tooconnect toohello Media Services API 使用 hello 服務主體的選項中, 介層應用程式 （web API 或 web 應用程式） 需要 toorequest 具有 hello 下列參數的 Azure AD 權杖：</span><span class="sxs-lookup"><span data-stu-id="94a1d-140">tooconnect toohello Media Services API by using hello service principal option, your middle-tier app (web API or web application) needs toorequest an Azure AD token that has hello following parameters:</span></span>  

* <span data-ttu-id="94a1d-141">Azure AD 租用戶端點</span><span class="sxs-lookup"><span data-stu-id="94a1d-141">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="94a1d-142">媒體服務資源 URI</span><span class="sxs-lookup"><span data-stu-id="94a1d-142">Media Services resource URI</span></span> 
* <span data-ttu-id="94a1d-143">REST 媒體服務的資源 URI</span><span class="sxs-lookup"><span data-stu-id="94a1d-143">Resource URI for REST Media Services</span></span>
* <span data-ttu-id="94a1d-144">Azure AD 應用程式的值： hello**用戶端識別碼**和**用戶端密碼**</span><span class="sxs-lookup"><span data-stu-id="94a1d-144">Azure AD application values: hello **client ID** and **client secret**</span></span>

<span data-ttu-id="94a1d-145">您可以取得這些參數在 hello hello 值**連接 tooMedia 服務應用程式開發介面與服務主體**頁面。</span><span class="sxs-lookup"><span data-stu-id="94a1d-145">You can get hello values for these parameters on hello **Connect tooMedia Services API with service principal** page.</span></span> <span data-ttu-id="94a1d-146">使用此頁面 toocreate 新的 Azure AD 應用程式或 tooselect 現有。</span><span class="sxs-lookup"><span data-stu-id="94a1d-146">Use this page toocreate a new Azure AD application or tooselect an existing one.</span></span> <span data-ttu-id="94a1d-147">選取 hello Azure AD 應用程式之後，您可以取得 hello 用戶端識別碼 （應用程式識別碼），並產生 hello 用戶端密碼 （金鑰） 值。</span><span class="sxs-lookup"><span data-stu-id="94a1d-147">After you select hello Azure AD app, you can get hello client ID (Application ID) and generate hello client secret (key) values.</span></span> 

![使用服務主體連線的頁面](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

<span data-ttu-id="94a1d-149">當 hello**服務主體**刀鋒視窗中開啟時，會選取 hello 第一個 Azure AD 應用程式符合下列準則的 hello:</span><span class="sxs-lookup"><span data-stu-id="94a1d-149">When hello **Service Principal** blade opens, hello first Azure AD application that meets hello following criteria is selected:</span></span>

- <span data-ttu-id="94a1d-150">它是已註冊的 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="94a1d-150">It is a registered Azure AD application.</span></span>
- <span data-ttu-id="94a1d-151">它對 hello 帳戶參與者或 Owner Role-Based 存取控制的權限。</span><span class="sxs-lookup"><span data-stu-id="94a1d-151">It has Contributor or Owner Role-Based Access Control permissions on hello account.</span></span>

<span data-ttu-id="94a1d-152">您建立或選取 Azure AD 應用程式之後，您可以建立和複製用戶端密碼 （金鑰） 和 hello 用戶端識別碼 （應用程式識別碼）。</span><span class="sxs-lookup"><span data-stu-id="94a1d-152">After you create or select an Azure AD app, you can create and copy a client secret (key) and hello client ID (Application ID).</span></span> <span data-ttu-id="94a1d-153">hello 用戶端密碼和用戶端識別碼是在此案例中需要的 tooget hello 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="94a1d-153">hello client secret and client ID are required tooget hello access token in this scenario.</span></span>

<span data-ttu-id="94a1d-154">如果您沒有權限 toocreate Azure AD 應用程式網域中，不會顯示 hello Azure AD 應用程式控制項的 hello 刀鋒視窗，並會顯示警告訊息。</span><span class="sxs-lookup"><span data-stu-id="94a1d-154">If you don't have permissions toocreate Azure AD apps in your domain, hello Azure AD app controls of hello blade are not shown, and a warning message is displayed.</span></span>

<span data-ttu-id="94a1d-155">如果您使用 Media Services.NET SDK hello 連接 toohello Media Services API，請參閱[使用 Azure AD 驗證 tooaccess hello 與.NET 的 Azure 媒體服務 API](media-services-dotnet-get-started-with-aad.md)。</span><span class="sxs-lookup"><span data-stu-id="94a1d-155">If you connect toohello Media Services API by using hello Media Services .NET SDK, see [Use Azure AD authentication tooaccess hello Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="94a1d-156">如果您未使用 Media Services.NET 用戶端 hello SDK，您必須手動建立使用先前所討論的 hello 參數的 Azure AD 權杖要求。</span><span class="sxs-lookup"><span data-stu-id="94a1d-156">If you are not using hello Media Services .NET client SDK, you must manually create an Azure AD token request using hello parameters discussed earlier.</span></span> <span data-ttu-id="94a1d-157">如需詳細資訊，請參閱[toouse hello Azure AD 驗證程式庫 tooget 如何 hello Azure AD 權杖](../active-directory/develop/active-directory-authentication-libraries.md)。</span><span class="sxs-lookup"><span data-stu-id="94a1d-157">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

### <a name="get-hello-client-id-and-client-secret"></a><span data-ttu-id="94a1d-158">取得 hello 用戶端識別碼和用戶端密碼</span><span class="sxs-lookup"><span data-stu-id="94a1d-158">Get hello client ID and client secret</span></span>

<span data-ttu-id="94a1d-159">您選取現有的 Azure AD 應用程式或選取 hello 選項 toocreate 新之後，會顯示 hello 下列按鈕：</span><span class="sxs-lookup"><span data-stu-id="94a1d-159">After you select an existing Azure AD app or select hello option toocreate a new one, hello following buttons appear:</span></span>

![[Manage permissions] \(管理權限\) 和 [Manage application] \(管理應用程式\) 按鈕](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

<span data-ttu-id="94a1d-161">tooopen hello Azure AD 應用程式 刀鋒視窗中，按一下**管理應用程式**。</span><span class="sxs-lookup"><span data-stu-id="94a1d-161">tooopen hello Azure AD application blade, click **Manage application**.</span></span> <span data-ttu-id="94a1d-162">在 hello**管理應用程式**刀鋒視窗中，您可以取得 hello 應用程式的用戶端識別碼 （應用程式識別碼）。</span><span class="sxs-lookup"><span data-stu-id="94a1d-162">On hello **Manage application** blade, you can get hello app's client ID (Application ID).</span></span> <span data-ttu-id="94a1d-163">用戶端密碼 （金鑰），選取 toogenerate**金鑰**。</span><span class="sxs-lookup"><span data-stu-id="94a1d-163">toogenerate a client secret (key), select **Keys**.</span></span>

![管理應用程式刀鋒視窗的 [Keys] \(金鑰\) 選項](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-hello-application"></a><span data-ttu-id="94a1d-165">管理權限和 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="94a1d-165">Manage permissions and hello application</span></span>

<span data-ttu-id="94a1d-166">選取 hello Azure AD 應用程式之後，您可以管理 hello 應用程式和權限。</span><span class="sxs-lookup"><span data-stu-id="94a1d-166">After you select hello Azure AD application, you can manage hello application and permissions.</span></span> <span data-ttu-id="94a1d-167">tooset 其他應用程式中，按一下 註冊您的 Azure AD 應用程式 tooaccess**管理權限**。</span><span class="sxs-lookup"><span data-stu-id="94a1d-167">tooset up your Azure AD application tooaccess other applications, click **Manage permissions**.</span></span> <span data-ttu-id="94a1d-168">管理工作，例如變更索引鍵和回覆 Url 或 tooedit hello 應用程式的資訊清單中，按一下**管理應用程式**。</span><span class="sxs-lookup"><span data-stu-id="94a1d-168">For management tasks, such as changing keys and reply URLs, or tooedit hello application’s manifest, click **Manage application**.</span></span>

### <a name="edit-hello-apps-settings-or-manifest"></a><span data-ttu-id="94a1d-169">編輯 hello 應用程式設定或資訊清單</span><span class="sxs-lookup"><span data-stu-id="94a1d-169">Edit hello app's settings or manifest</span></span>

<span data-ttu-id="94a1d-170">tooedit hello 應用程式的設定或資訊清單中，按一下**管理應用程式**。</span><span class="sxs-lookup"><span data-stu-id="94a1d-170">tooedit hello app's settings or manifest, click **Manage application**.</span></span>

![管理應用程式頁面](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a><span data-ttu-id="94a1d-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="94a1d-172">Next steps</span></span>

<span data-ttu-id="94a1d-173">開始使用[上傳檔案 tooyour 帳戶](media-services-portal-upload-files.md)。</span><span class="sxs-lookup"><span data-stu-id="94a1d-173">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
