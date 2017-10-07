---
title: "呼叫的自訂應用程式的 aaaConfigure 驗證和授權 hello Azure 時間數列 Insights API，|Microsoft 文件"
description: "本教學課程說明如何在呼叫的自訂應用程式的 tooconfigure 驗證和授權 hello Azure 時間數列 Insights API"
keywords: 
services: time-series-insights
documentationcenter: 
author: dmdenmsft
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/24/2017
ms.author: dmden
ms.openlocfilehash: 5043468bfc2af3c0d27e8602508d92ba2848409e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a><span data-ttu-id="4a9fd-103">Azure Time Series Insights API 的驗證和授權</span><span class="sxs-lookup"><span data-stu-id="4a9fd-103">Authentication and authorization for Azure Time Series Insights API</span></span>

<span data-ttu-id="4a9fd-104">本文說明如何自訂的應用程式呼叫 tooconfigure hello Azure 時間數列 Insights API。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-104">This article explains how tooconfigure a custom application that calls hello Azure Time Series Insights API.</span></span>

## <a name="service-principal"></a><span data-ttu-id="4a9fd-105">服務主體</span><span class="sxs-lookup"><span data-stu-id="4a9fd-105">Service principal</span></span>

<span data-ttu-id="4a9fd-106">本節說明如何 tooconfigure 應用程式 tooaccess hello 代表 hello 應用程式的時間序列 Insights API。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-106">This section explains how tooconfigure an application tooaccess hello Time Series Insights API on behalf of hello application.</span></span> <span data-ttu-id="4a9fd-107">hello 應用程式可以接著查詢資料或發行應用程式認證和 hello 使用者認證 hello 時間數列 Insights 環境中的參考資料。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-107">hello application can then query data or publish reference data in hello Time Series Insights environment with application credentials and not hello user credentials.</span></span>

<span data-ttu-id="4a9fd-108">當您需要 tooaccess 時間數列 Insights 的應用程式時，您必須在設定 Azure Active Directory 應用程式，並指派 hello 時間數列 Insights 環境中的 hello 資料存取原則。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-108">When you have an application that needs tooaccess Time Series Insights, you must set up an Azure Active Directory application and assign hello data access policies in hello Time Series Insights environment.</span></span> <span data-ttu-id="4a9fd-109">這個方法很理想 toorunning hello 應用程式，以您自己的認證，因為：</span><span class="sxs-lookup"><span data-stu-id="4a9fd-109">This approach is preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="4a9fd-110">您可以指派權限 toohello 應用程式識別碼不同於您自己的權限。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-110">You can assign permissions toohello app identity that are different from your own permissions.</span></span> <span data-ttu-id="4a9fd-111">一般而言，這些權限會限制的 tooexactly 哪些 hello 應用程式需要 toodo。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-111">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span> <span data-ttu-id="4a9fd-112">例如，您可以允許 hello 應用程式 tooonly 讀取特定的時間序列 Insights 環境中的資料。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-112">For example, you can allow hello app tooonly read data in a particular Time Series Insights environment.</span></span>
* <span data-ttu-id="4a9fd-113">如果您的責任的變更，您不需要 toochange hello 應用程式的認證。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-113">You don't have toochange hello app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="4a9fd-114">如果您執行自動執行的指令碼，您可以使用憑證或金鑰 tooautomate 驗證應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-114">You can use a certificate or an application key tooautomate authentication when you're running an unattended script.</span></span>

<span data-ttu-id="4a9fd-115">本文將說明這些逐步的 tooperform hello Azure 入口網站的方式。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-115">This article shows you how tooperform those steps through hello Azure portal.</span></span> <span data-ttu-id="4a9fd-116">它著重在 hello 應用程式所在預定的 toorun 只能有一個組織中的單一租用戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-116">It focuses on a single-tenant application where hello application is intended toorun in only one organization.</span></span> <span data-ttu-id="4a9fd-117">您通常會將單一租用戶應用程式用在組織內執行的企業營運系統應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-117">You typically use single-tenant applications for line-of-business applications that run in your organization.</span></span>

<span data-ttu-id="4a9fd-118">hello 的安裝程式流程是由三個高階步驟所組成：</span><span class="sxs-lookup"><span data-stu-id="4a9fd-118">hello setup flow consists of three high-level steps:</span></span>

1. <span data-ttu-id="4a9fd-119">在 Azure Active Directory 中建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-119">Create an application in Azure Active Directory.</span></span>
2. <span data-ttu-id="4a9fd-120">授權這個應用程式 tooaccess hello 時間數列 Insights 環境。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-120">Authorize this application tooaccess hello Time Series Insights environment.</span></span>
3. <span data-ttu-id="4a9fd-121">使用 hello 應用程式識別碼和金鑰 tooacquire 語彙基元 toohello`"https://api.timeseries.azure.com/"`對象或資源。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-121">Use hello application ID and key tooacquire a token toohello `"https://api.timeseries.azure.com/"` audience or resource.</span></span> <span data-ttu-id="4a9fd-122">hello 語彙基元接著可以使用的 toocall hello Insights API，時間序列。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-122">hello token can then be used toocall hello Time Series Insights API.</span></span>

<span data-ttu-id="4a9fd-123">以下是 hello 詳細的步驟：</span><span class="sxs-lookup"><span data-stu-id="4a9fd-123">Here are hello detailed steps:</span></span>

1. <span data-ttu-id="4a9fd-124">在 hello Azure 入口網站，選取  **Azure Active Directory** > **應用程式註冊** > **新應用程式註冊**。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-124">In hello Azure portal, select **Azure Active Directory** > **App registrations** > **New application registration**.</span></span>

   ![Azure Active Directory 中的新應用程式註冊](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. <span data-ttu-id="4a9fd-126">提供 hello 應用程式名稱、 選取 hello 類型 toobe **Web 應用程式 / 應用程式開發介面**，選取任何有效的 URI，如**登入 URL**，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-126">Give hello application a name, select hello type toobe **Web app / API**, select any valid URI for **Sign-on URL**, and click **Create**.</span></span>

   ![在 Azure Active Directory 中建立 hello 應用程式](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. <span data-ttu-id="4a9fd-128">選取您新建立的應用程式並複製其應用程式識別碼 tooyour 慣用的文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-128">Select your newly created application and copy its application ID tooyour favorite text editor.</span></span>

   ![複製 hello 應用程式識別碼](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. <span data-ttu-id="4a9fd-130">選取**金鑰**，輸入 hello 索引鍵名稱，選取 hello 到期，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-130">Select **Keys**, enter hello key name, select hello expiration, and click **Save**.</span></span>

   ![選取應用程式金鑰](media/authentication-and-authorization/active-directory-application-keys.png)

   ![輸入 hello 索引鍵名稱和到期日，然後按一下 [儲存]](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. <span data-ttu-id="4a9fd-133">複製 hello 金鑰 tooyour 慣用的文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-133">Copy hello key tooyour favorite text editor.</span></span>

   ![複製 hello 應用程式金鑰](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. <span data-ttu-id="4a9fd-135">Hello 時間數列 Insights 環境中，選取**資料存取原則**按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-135">For hello Time Series Insights environment, select **Data Access Policies** and click **Add**.</span></span>

   ![加入新資料的存取原則 toohello 時間數列 Insights 環境](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. <span data-ttu-id="4a9fd-137">在 [hello**選取使用者**] 對話方塊中，貼上 hello 應用程式名稱 （來自步驟 2） 或應用程式識別碼 （從步驟 3）。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-137">In hello **Select User** dialog box, paste hello application name (from step 2) or application ID (from step 3).</span></span>

   ![尋找應用程式在 hello [選取使用者] 對話方塊](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. <span data-ttu-id="4a9fd-139">選取 hello 角色 (**讀取器**來查詢資料，**參與者**查詢資料和變更參考資料)，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-139">Select hello role (**Reader** for querying data, **Contributor** for querying data and changing reference data) and click **Ok**.</span></span>

   ![在 hello 選取角色 對話方塊中挑選讀者或參與者](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. <span data-ttu-id="4a9fd-141">按一下以儲存 hello 原則**確定**。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-141">Save hello policy by clicking **Ok**.</span></span>

10. <span data-ttu-id="4a9fd-142">使用 hello 應用程式識別碼 （從步驟 3） 和應用程式 （從步驟 5） 索引鍵 tooacquire hello 語彙基元，代表 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-142">Use hello application ID (from step 3) and application key (from step 5) tooacquire hello token on behalf of hello application.</span></span> <span data-ttu-id="4a9fd-143">hello 語彙基元可以然後傳入 hello `Authorization` hello 應用程式會呼叫 hello 時間數列 Insights API 時，標頭。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-143">hello token can then be passed in hello `Authorization` header when hello application calls hello Time Series Insights API.</span></span>

    <span data-ttu-id="4a9fd-144">如果您使用 C#，您可以使用下列程式碼 tooacquire hello 語彙基元，代表 hello 應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-144">If you're using C#, you can use hello following code tooacquire hello token on behalf of hello application.</span></span> <span data-ttu-id="4a9fd-145">如需完整範例，請參閱[使用 C# 查詢資料](time-series-insights-query-data-csharp.md)。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-145">For a complete sample, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set hello resource URI toohello Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of hello application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a><span data-ttu-id="4a9fd-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4a9fd-146">Next steps</span></span>

<span data-ttu-id="4a9fd-147">應用程式中使用 hello 應用程式識別碼和金鑰。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-147">Use hello application ID and key in your application.</span></span> <span data-ttu-id="4a9fd-148">呼叫 hello 時間數列 Insights API 的範例程式碼，請參閱[查詢資料使用 C#](time-series-insights-query-data-csharp.md)。</span><span class="sxs-lookup"><span data-stu-id="4a9fd-148">For sample code that calls hello Time Series Insights API, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="4a9fd-149">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4a9fd-149">See also</span></span>

* <span data-ttu-id="4a9fd-150">[查詢 API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) hello 完整查詢 API 參考</span><span class="sxs-lookup"><span data-stu-id="4a9fd-150">[Query API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) for hello full Query API reference</span></span>
* [<span data-ttu-id="4a9fd-151">建立服務主體在 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4a9fd-151">Create a service principal in hello Azure portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
