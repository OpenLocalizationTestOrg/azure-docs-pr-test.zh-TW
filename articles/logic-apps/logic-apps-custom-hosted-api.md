---
title: "部署、呼叫並驗證 Azure Logic Apps 的 web API 與 REST API | Microsoft Docs"
description: "在工作流程中部署、驗證並呼叫 web API 與 REST API，以便與 Azure Logic Apps 進行系統整合"
keywords: "web API, REST API, 連接器, 工作流程, 系統整合, 驗證"
services: logic-apps
author: stepsic-microsoft-com
manager: anneta
editor: 
documentationcenter: 
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: 88c62d5ab046d8cf4bce5d23b776e517bb0e1d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a><span data-ttu-id="f14ca-104">部署、呼叫並驗證自訂 API 作為 Logic Apps 的連接器</span><span class="sxs-lookup"><span data-stu-id="f14ca-104">Deploy, call, and authenticate custom APIs as connectors for logic apps</span></span>

<span data-ttu-id="f14ca-105">在您[建立可提供 Logic Apps 工作流程中所使用之動作或觸發程序的自訂 API](./logic-apps-create-api-app.md) 之後，您在呼叫之前必須先部署您的 API。</span><span class="sxs-lookup"><span data-stu-id="f14ca-105">After you [create custom APIs](./logic-apps-create-api-app.md) that provide actions or triggers to use in logic apps workflows, you must deploy your APIs before you can call them.</span></span> <span data-ttu-id="f14ca-106">且雖然您可以從邏輯應用程式呼叫任何 API，但請新增描述您 API 之作業和參數的 [Swagger 中繼資料](http://swagger.io/specification/)以獲得最佳體驗。</span><span class="sxs-lookup"><span data-stu-id="f14ca-106">And although you can call any API from a logic app, for the best experience, add [Swagger metadata](http://swagger.io/specification/) that describes your API's operations and parameters.</span></span> <span data-ttu-id="f14ca-107">Swagger 檔案可協助您改善 API 工作，並更輕鬆地整合 Logic Apps。</span><span class="sxs-lookup"><span data-stu-id="f14ca-107">This Swagger file helps your API work better and integrate more easily with logic apps.</span></span>

<span data-ttu-id="f14ca-108">您可以將 API 部署為 [web 應用程式](../app-service-web/app-service-web-overview.md)，但請考慮將您的 API 部署為 [API 應用程式](../app-service-api/app-service-api-apps-why-best-platform.md)，如此一來，當您在雲端中及內部部署建置、裝載並自訂 API 時，可讓您的作業更容易。</span><span class="sxs-lookup"><span data-stu-id="f14ca-108">You can deploy your APIs as [web apps](../app-service-web/app-service-web-overview.md), but consider deploying your APIs as [API apps](../app-service-api/app-service-api-apps-why-best-platform.md), which can make your job easier when you build, host, and consume APIs in the cloud and on premises.</span></span> <span data-ttu-id="f14ca-109">您不需要在 API 中變更任何程式碼 -- 只需將您的程式碼部署至 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f14ca-109">You don't have to change any code in your APIs -- just deploy your code to an API app.</span></span> <span data-ttu-id="f14ca-110">您可以在 [Azure App Service](../app-service/app-service-value-prop-what-is.md) 上裝載您的 API，Azure App Service 是平台即服務 (PaaS) 供應項目，能為 API 裝載提供最佳、最簡單且擴充性最高的方法。</span><span class="sxs-lookup"><span data-stu-id="f14ca-110">You can host your APIs on [Azure App Service](../app-service/app-service-value-prop-what-is.md), a platform-as-a-service (PaaS) offering that provides one of the best, easiest, and most scalable ways for API hosting.</span></span>

<span data-ttu-id="f14ca-111">若要驗證從 Logic Apps 對您 API 的呼叫，您可以在 Azure 入口網站中設定 Azure Active Directory，讓您不需要更新您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="f14ca-111">To authenticate calls from logic apps to your APIs, you can set up Azure Active Directory in the Azure portal so you don't have to update your code.</span></span> <span data-ttu-id="f14ca-112">或者，您可以透過您的 API 程式碼要求並強制執行驗證。</span><span class="sxs-lookup"><span data-stu-id="f14ca-112">Or, you can require and enforce authentication through your API's code.</span></span>

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a><span data-ttu-id="f14ca-113">將您的 API 部署為 web 應用程式或 API 應用程式</span><span class="sxs-lookup"><span data-stu-id="f14ca-113">Deploy your API as a web app or API app</span></span>

<span data-ttu-id="f14ca-114">請先將您的 API 部署為 web 應用程式或 API 應用程式到 Azure App Service 後，才能從邏輯應用程式呼叫自訂 API。</span><span class="sxs-lookup"><span data-stu-id="f14ca-114">Before you can call your custom API from a logic app, deploy your API as a web app or API app to Azure App Service.</span></span> <span data-ttu-id="f14ca-115">此外，若要讓 Logic App Designer 可讀取您的 Swagger 文件，請設定 API 定義屬性，並開啟 web 應用程式或 API 應用程式的[跨原始資源共用 (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig)。</span><span class="sxs-lookup"><span data-stu-id="f14ca-115">Also, to make your Swagger document readable by the Logic App Designer, set the API definition properties and turn on [cross-origin resource sharing (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) for your web app or API app.</span></span>

1. <span data-ttu-id="f14ca-116">在 Azure 入口網站中，選取您的 Web 應用程式或 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f14ca-116">In the Azure portal, select your web app or API app.</span></span>

2. <span data-ttu-id="f14ca-117">在開啟的刀鋒視窗之 [API] 下方，選擇 [API 定義]。</span><span class="sxs-lookup"><span data-stu-id="f14ca-117">In the blade that opens, under **API**, choose **API definition**.</span></span> <span data-ttu-id="f14ca-118">將 [API 定義位置] 設定為 swagger.json 檔案的 URL。</span><span class="sxs-lookup"><span data-stu-id="f14ca-118">Set the **API definition location** to the URL for your swagger.json file.</span></span>

   <span data-ttu-id="f14ca-119">通常，URL 會以這種格式出現：`https://{name}.azurewebsites.net/swagger/docs/v1)`</span><span class="sxs-lookup"><span data-stu-id="f14ca-119">Usually, the URL appears in this format: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span></span>

   ![您自訂 API 的 Swagger 檔案連結](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. <span data-ttu-id="f14ca-121">在 [API] 下，選擇 [CORS]。</span><span class="sxs-lookup"><span data-stu-id="f14ca-121">Under **API**, choose **CORS**.</span></span> <span data-ttu-id="f14ca-122">將 [允許的來源] 的 CORS 原則 設定為 **'*'** (全部允許)。</span><span class="sxs-lookup"><span data-stu-id="f14ca-122">Set the CORS policy for **Allowed origins** to **'*'** (allow all).</span></span>

   <span data-ttu-id="f14ca-123">此設定允許來自 Logic App Designer 的要求。</span><span class="sxs-lookup"><span data-stu-id="f14ca-123">This setting permits requests from Logic App Designer.</span></span>

   ![允許來自 Logic App Designer 對您自訂 API 的要求](media/logic-apps-custom-hosted-api/custom-api-cors.png)

<span data-ttu-id="f14ca-125">如需詳細資訊，請參閱這些文章：</span><span class="sxs-lookup"><span data-stu-id="f14ca-125">For more information, see these articles:</span></span>

* [<span data-ttu-id="f14ca-126">新增 ASP.NET web API 的 Swagger 中繼資料</span><span class="sxs-lookup"><span data-stu-id="f14ca-126">Add Swagger metadata for ASP.NET web APIs</span></span>](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [<span data-ttu-id="f14ca-127">將 ASP.NET web API 部署至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f14ca-127">Deploy ASP.NET web APIs to Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a><span data-ttu-id="f14ca-128">從邏輯應用程式工作流程呼叫自訂 API</span><span class="sxs-lookup"><span data-stu-id="f14ca-128">Call your custom API from logic app workflows</span></span>

<span data-ttu-id="f14ca-129">在您設定 API 定義屬性和 CORS 之後，您自訂 API 的觸發程序和動作應該就可供您用來包含在邏輯應用程式工作流程中。</span><span class="sxs-lookup"><span data-stu-id="f14ca-129">After you set up the API definition properties and CORS, your custom API's triggers and actions should become available for you to include in your logic app workflow.</span></span> 

*  <span data-ttu-id="f14ca-130">若要檢視具有 Swagger URL 的網站，您可以在 Logic Apps Designer 中瀏覽訂用帳戶網站。</span><span class="sxs-lookup"><span data-stu-id="f14ca-130">To view the websites that have Swagger URLs, you can browse your subscription websites in the Logic Apps Designer.</span></span>

*  <span data-ttu-id="f14ca-131">若要藉由指向 Swagger 文件來檢視可用的動作和輸入，請使用 [HTTP + Swagger 動作](../connectors/connectors-native-http-swagger.md)。</span><span class="sxs-lookup"><span data-stu-id="f14ca-131">To view available actions and inputs by pointing at a Swagger document, use the [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).</span></span>

*  <span data-ttu-id="f14ca-132">若要呼叫任何 API，包含沒有或未公開 Swagger 文件的 API，您一律可以使用 [HTTP 動作](../connectors/connectors-native-http.md)建立要求。</span><span class="sxs-lookup"><span data-stu-id="f14ca-132">To call any API, including APIs that don't have or expose a Swagger document, you can always create a request with the [HTTP action](../connectors/connectors-native-http.md).</span></span>

## <a name="authenticate-calls-to-your-custom-api"></a><span data-ttu-id="f14ca-133">驗證您自訂 API 的呼叫</span><span class="sxs-lookup"><span data-stu-id="f14ca-133">Authenticate calls to your custom API</span></span>

<span data-ttu-id="f14ca-134">您可以以下列方式保護對自訂 API 的呼叫：</span><span class="sxs-lookup"><span data-stu-id="f14ca-134">You can secure calls to your custom API in these ways:</span></span>

* <span data-ttu-id="f14ca-135">[無程式碼變更](#no-code)：透過 Azure 入口網站使用 [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) 來保護您的 API，因此您不需要更新程式碼或重新部署您的 API。</span><span class="sxs-lookup"><span data-stu-id="f14ca-135">[No code changes](#no-code): Protect your API with [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) through the Azure portal, so you don't have to update your code or redeploy your API.</span></span>

  > [!NOTE]
  > <span data-ttu-id="f14ca-136">根據預設，您在 Azure 入口網站中開啟的 Azure AD 驗證不提供精細的授權。</span><span class="sxs-lookup"><span data-stu-id="f14ca-136">By default, the Azure AD authentication that you turn on in the Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="f14ca-137">例如，這項驗證會將您的 API 鎖定為僅限特定租用戶，而非特定使用者或應用程式。</span><span class="sxs-lookup"><span data-stu-id="f14ca-137">For example, this authentication locks your API to just a specific tenant, not to a specific user or app.</span></span> 

* <span data-ttu-id="f14ca-138">[更新您的 API 程式碼](#update-code)：保護您的 API，方法是透過程式碼強制執行[憑證驗證](#certificate)、[基本驗證](#basic)，或 [Azure AD 驗證](#azure-ad-code)。</span><span class="sxs-lookup"><span data-stu-id="f14ca-138">[Update your API's code](#update-code): Protect your API by enforcing [certificate authentication](#certificate), [basic authentication](#basic), or [Azure AD authentication](#azure-ad-code) through code.</span></span>

<a name="no-code"></a>

### <a name="authenticate-calls-to-your-api-without-changing-code"></a><span data-ttu-id="f14ca-139">驗證對 API 的呼叫，不需要變更程式碼</span><span class="sxs-lookup"><span data-stu-id="f14ca-139">Authenticate calls to your API without changing code</span></span>

<span data-ttu-id="f14ca-140">以下是這個方法的一般步驟：</span><span class="sxs-lookup"><span data-stu-id="f14ca-140">Here's the general steps for this method:</span></span>

1. <span data-ttu-id="f14ca-141">將建立兩個 [Azure Active Directory (Azure AD) 應用程式識別](../app-service-api/app-service-api-dotnet-service-principal-auth.md)：一個用於邏輯應用程式，一個用於 Web 應用程式 (或 API 應用程式)。</span><span class="sxs-lookup"><span data-stu-id="f14ca-141">Create two [Azure Active Directory (Azure AD) application identities](../app-service-api/app-service-api-dotnet-service-principal-auth.md): one for your logic app and one for your web app (or API app).</span></span>

2. <span data-ttu-id="f14ca-142">若要驗證對您 API 的呼叫，請使用與邏輯應用程式的 Azure AD 應用程式識別碼相關聯的[服務主體](../app-service-api/app-service-api-dotnet-service-principal-auth.md)認證 (用戶端識別碼和祕密)。</span><span class="sxs-lookup"><span data-stu-id="f14ca-142">To authenticate calls to your API, use the credentials (client ID and secret) for the [service principal](../app-service-api/app-service-api-dotnet-service-principal-auth.md) that's associated with the Azure AD application identity for your logic app.</span></span>

3. <span data-ttu-id="f14ca-143">將應用程式識別碼包含在邏輯應用程式定義中。</span><span class="sxs-lookup"><span data-stu-id="f14ca-143">Include the application IDs in your logic app definition.</span></span>

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a><span data-ttu-id="f14ca-144">第 1 部分：建立 Azure AD 邏輯應用程式的應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="f14ca-144">Part 1: Create an Azure AD application identity for your logic app</span></span>

<span data-ttu-id="f14ca-145">您的邏輯應用程式會使用這個 Azure AD 應用程式識別碼向 Azure AD 驗證。</span><span class="sxs-lookup"><span data-stu-id="f14ca-145">Your logic app uses this Azure AD application identity to authenticate against Azure AD.</span></span> <span data-ttu-id="f14ca-146">您只需要為您的目錄設定一次這個身分識別。</span><span class="sxs-lookup"><span data-stu-id="f14ca-146">You only have to set up this identity one time for your directory.</span></span> <span data-ttu-id="f14ca-147">例如，儘管您可以為每個邏輯應用程式建立唯一的身分識別，但可以選擇讓所有的 Logic Apps 使用相同的身分識別。</span><span class="sxs-lookup"><span data-stu-id="f14ca-147">For example, you can choose to use the same identity for all your logic apps, even though you can create unique identities for each logic app.</span></span> <span data-ttu-id="f14ca-148">您可以在 Azure 入口網站、[Azure 傳統入口網站](#app-identity-logic-classic)，或使用 [PowerShell](#powershell) 設定這些身分識別。</span><span class="sxs-lookup"><span data-stu-id="f14ca-148">You can set up these identities in the Azure portal, [Azure classic portal](#app-identity-logic-classic), or use [PowerShell](#powershell).</span></span>

<span data-ttu-id="f14ca-149">**在 Azure 入口網站中建立邏輯應用程式的應用程式識別碼**</span><span class="sxs-lookup"><span data-stu-id="f14ca-149">**Create the application identity for your logic app in the Azure portal**</span></span>

1. <span data-ttu-id="f14ca-150">在 [Azure 入口網站](https://portal.azure.com "https://portal.azure.com")中，選擇 **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="f14ca-150">In the [Azure portal](https://portal.azure.com "https://portal.azure.com"), choose **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="f14ca-151">請確認您與 web 應用程式或 API 應用程式位於相同的目錄中。</span><span class="sxs-lookup"><span data-stu-id="f14ca-151">Confirm that you're in the same directory as your web app or API app.</span></span>

   > [!TIP]
   > <span data-ttu-id="f14ca-152">若要切換目錄，請按一下您的設定檔並選取另一個目錄。</span><span class="sxs-lookup"><span data-stu-id="f14ca-152">To switch directories, click your profile and select another directory.</span></span> <span data-ttu-id="f14ca-153">或者，選擇 [概觀] > [切換目錄]。</span><span class="sxs-lookup"><span data-stu-id="f14ca-153">Or, choose **Overview** > **Switch directory**.</span></span>

3. <span data-ttu-id="f14ca-154">在 [目錄] 功能表的 [管理] 下，選擇 [應用程式註冊] > [新增應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="f14ca-154">On the directory menu, under **Manage**, choose **App registrations** > **New application registration**.</span></span>

   > [!TIP]
   > <span data-ttu-id="f14ca-155">根據預設，應用程式註冊清單會顯示您目錄中的所有應用程式註冊。</span><span class="sxs-lookup"><span data-stu-id="f14ca-155">By default, the app registrations list shows all app registrations in your directory.</span></span> <span data-ttu-id="f14ca-156">若只要檢視您的應用程式註冊，請在搜尋方塊旁選取 [我的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f14ca-156">To view only your app registrations, next to the search box, select **My apps**.</span></span> 

   ![建立新的應用程式註冊](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. <span data-ttu-id="f14ca-158">為您的應用程式識別碼指定名稱，並保留**應用程式類型**設為 **Web 應用程式 / API**，提供格式化為**登入 URL** 之網域的唯一字串，然後選擇 [建立]。</span><span class="sxs-lookup"><span data-stu-id="f14ca-158">Give your application identity a name, leave **Application type** set to **Web app / API**, provide a unique string formatted as a domain for **Sign-on URL**, and choose **Create**.</span></span>

   ![提供應用程式識別碼的名稱和登入 URL](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   <span data-ttu-id="f14ca-160">您針對邏輯應用程式建立的應用程式識別碼現在會出現在應用程式註冊清單中。</span><span class="sxs-lookup"><span data-stu-id="f14ca-160">The application identity that you created for your logic app now appears in the app registrations list.</span></span>

   ![邏輯應用程式的應用程式識別碼](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. <span data-ttu-id="f14ca-162">在應用程式註冊清單中，選取新的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="f14ca-162">In the app registrations list, select your new application identity.</span></span> <span data-ttu-id="f14ca-163">複製並儲存**應用程式識別碼**，用來作為第 3 部分中邏輯應用程式的「用戶端識別碼」。</span><span class="sxs-lookup"><span data-stu-id="f14ca-163">Copy and save the **Application ID** to use as the "client ID" for your logic app in Part 3.</span></span>

   ![複製並儲存邏輯應用程式的應用程式識別碼](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. <span data-ttu-id="f14ca-165">如果看不到您的應用程式識別碼設定，請選擇 [設定] 或 [所有設定]。</span><span class="sxs-lookup"><span data-stu-id="f14ca-165">If your application identity settings aren't visible, choose **Settings** or **All settings**.</span></span>

7. <span data-ttu-id="f14ca-166">在 [API 存取] 下，選擇 [金鑰]。</span><span class="sxs-lookup"><span data-stu-id="f14ca-166">Under **API Access**, choose **Keys**.</span></span> <span data-ttu-id="f14ca-167">在 [描述] 下，提供您金鑰的名稱。</span><span class="sxs-lookup"><span data-stu-id="f14ca-167">Under **Description**, provide a name for your key.</span></span> <span data-ttu-id="f14ca-168">在 [到期時間] 下，選取您金鑰的持續時間。</span><span class="sxs-lookup"><span data-stu-id="f14ca-168">Under **Expires**, select a duration for your key.</span></span>

   <span data-ttu-id="f14ca-169">您要建立的金鑰會作為應用程式識別碼的「祕密」或邏輯應用程式的密碼。</span><span class="sxs-lookup"><span data-stu-id="f14ca-169">The key that you're creating acts as the application identity's "secret" or password for your logic app.</span></span>

   ![建立邏輯應用程式身分識別的金鑰](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. <span data-ttu-id="f14ca-171">在工具列上，選擇 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="f14ca-171">On the toolbar, choose **Save**.</span></span> <span data-ttu-id="f14ca-172">在 [值] 下，現在會顯示您的金鑰。</span><span class="sxs-lookup"><span data-stu-id="f14ca-172">Under **Value**, your key now appears.</span></span> 
<span data-ttu-id="f14ca-173">**請務必複製並儲存您的金鑰**供稍後使用，因為當您離開 [金鑰] 刀鋒視窗時會將金鑰隱藏。</span><span class="sxs-lookup"><span data-stu-id="f14ca-173">**Make sure to copy and save your key** for later use because the key is hidden when you leave the key blade.</span></span>

   <span data-ttu-id="f14ca-174">當您在第 3 部分設定邏輯應用程式時，您要指定這個金鑰作為「祕密」或密碼。</span><span class="sxs-lookup"><span data-stu-id="f14ca-174">When you configure your logic app in Part 3, you specify this key as the "secret" or password.</span></span>

   ![複製並儲存金鑰供稍後使用](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

<span data-ttu-id="f14ca-176">**在 Azure 傳統入口網站中建立邏輯應用程式的應用程式識別碼**</span><span class="sxs-lookup"><span data-stu-id="f14ca-176">**Create the application identity for your logic app in the Azure classic portal**</span></span>

1. <span data-ttu-id="f14ca-177">在 Azure 傳統入口網站中，選擇 [**[Active Directory]**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory) 。</span><span class="sxs-lookup"><span data-stu-id="f14ca-177">In the Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2. <span data-ttu-id="f14ca-178">選取您用於 Web 應用程式或 API 應用程式的相同目錄。</span><span class="sxs-lookup"><span data-stu-id="f14ca-178">Select the same directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="f14ca-179">在 [應用程式] 索引標籤上，選擇頁面底部的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="f14ca-179">On the **Applications** tab, choose **Add** at the bottom of the page.</span></span>

4. <span data-ttu-id="f14ca-180">為您的應用程式識別碼提供名稱，然後選擇 **[下一步]** \(向右箭號)。</span><span class="sxs-lookup"><span data-stu-id="f14ca-180">Give your application identity a name, and choose **Next** (right arrow).</span></span>

5. <span data-ttu-id="f14ca-181">在 [應用程式屬性] 下，提供格式化為**登入 URL** 和**應用程式識別碼 URI** 之網域的唯一字串，然後選擇 [完成] \(勾選記號)。</span><span class="sxs-lookup"><span data-stu-id="f14ca-181">Under **App properties**, provide a unique string formatted as a domain for **Sign-on URL** and **App ID URI**, and choose **Complete** (checkmark).</span></span>

6. <span data-ttu-id="f14ca-182">在 [設定] 索引標籤上，複製並儲存用來作為第 3 部分中邏輯應用程式的「用戶端識別碼」。</span><span class="sxs-lookup"><span data-stu-id="f14ca-182">On the **Configure** tab, copy and save the **Client ID** for your logic app to use in Part 3.</span></span>

7. <span data-ttu-id="f14ca-183">在 [金鑰] 下，開啟 [選取持續時間] 清單。</span><span class="sxs-lookup"><span data-stu-id="f14ca-183">Under **Keys**, open the **Select duration** list.</span></span> <span data-ttu-id="f14ca-184">選取您金鑰的持續時間。</span><span class="sxs-lookup"><span data-stu-id="f14ca-184">Select a duration for your key.</span></span>

   <span data-ttu-id="f14ca-185">您要建立的金鑰會作為應用程式識別碼的「祕密」或邏輯應用程式的密碼。</span><span class="sxs-lookup"><span data-stu-id="f14ca-185">The key that you're creating acts as the application identity's "secret" or password for your logic app.</span></span>

8. <span data-ttu-id="f14ca-186">在頁面底部選擇 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="f14ca-186">At the bottom of the page, choose **Save**.</span></span> <span data-ttu-id="f14ca-187">您可能必須等候幾秒鐘。</span><span class="sxs-lookup"><span data-stu-id="f14ca-187">You might have to wait a few seconds.</span></span>

9. <span data-ttu-id="f14ca-188">在 [金鑰] 下，請務必複製並儲存現在顯示的金鑰。</span><span class="sxs-lookup"><span data-stu-id="f14ca-188">Under **Keys**, make sure to copy and save the key that now appears.</span></span> 

   <span data-ttu-id="f14ca-189">當您在第 3 部分設定邏輯應用程式時，您要指定這個金鑰作為「祕密」或密碼。</span><span class="sxs-lookup"><span data-stu-id="f14ca-189">When you configure your logic app in Part 3, you specify this key as the "secret" or password.</span></span>

<span data-ttu-id="f14ca-190">如需詳細資訊，請了解如何[設定 App Service 應用程式使用 Azure Active Directory 登入](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="f14ca-190">For more information, learn how to [configure your App Service application to use Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>

<a name="powershell"></a>

<span data-ttu-id="f14ca-191">**在 PowerShell 中建立邏輯應用程式的應用程式識別碼**</span><span class="sxs-lookup"><span data-stu-id="f14ca-191">**Create the application identity for your logic app in PowerShell**</span></span>

<span data-ttu-id="f14ca-192">您可以使用 PowerShell，透過 Azure Resource Manager 來執行這項工作中。</span><span class="sxs-lookup"><span data-stu-id="f14ca-192">You can perform this task through Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="f14ca-193">在 PowerShell 中，執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="f14ca-193">In PowerShell, run these commands:</span></span>

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. <span data-ttu-id="f14ca-194">請務必複製 [租用戶識別碼] (您 Azure AD 租用戶的 GUID)、[應用程式識別碼] 和您所使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="f14ca-194">Make sure to copy the **Tenant ID** (GUID for your Azure AD tenant), the **Application ID**, and the password that you used.</span></span>

<span data-ttu-id="f14ca-195">如需詳細資訊，請了解如何[使用 PowerShell 建立用來存取資源的服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md)。</span><span class="sxs-lookup"><span data-stu-id="f14ca-195">For more information, learn how to [create a service principal with PowerShell to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a><span data-ttu-id="f14ca-196">第 2 部分：建立 Web 應用程式或 API 應用程式的 Azure AD 應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="f14ca-196">Part 2: Create an Azure AD application identity for your web app or API app</span></span>

<span data-ttu-id="f14ca-197">如果已部署 web 應用程式或 API 應用程式，您就可以開啟驗證，並在 Azure 入口網站中建立應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="f14ca-197">If your web app or API app is already deployed, you can turn on authentication and create the application identity in the Azure portal.</span></span> <span data-ttu-id="f14ca-198">否則，您可以[在您使用 Azure Resource Manager 範本進行部署時開啟驗證](#authen-deploy)。</span><span class="sxs-lookup"><span data-stu-id="f14ca-198">Otherwise, you can [turn on authentication when you deploy with an Azure Resource Manager template](#authen-deploy).</span></span> 

<span data-ttu-id="f14ca-199">**建立應用程式識別碼，並在 Azure 入口網站中開啟已部署應用程式的驗證**</span><span class="sxs-lookup"><span data-stu-id="f14ca-199">**Create the application identity and turn on authentication in the Azure portal for deployed apps**</span></span>

1. <span data-ttu-id="f14ca-200">在 [Azure 入口網站](https://portal.azure.com "https://portal.azure.com")中，尋找並選取您的 web 應用程式或 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f14ca-200">In the [Azure portal](https://portal.azure.com "https://portal.azure.com"), find and select your web app or API app.</span></span> 

2. <span data-ttu-id="f14ca-201">在 [設定] 下，選擇 [驗證/授權]。</span><span class="sxs-lookup"><span data-stu-id="f14ca-201">Under **Settings**, choose **Authentication/Authorization**.</span></span> <span data-ttu-id="f14ca-202">在 [App Service 驗證] 下，將驗證 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="f14ca-202">Under **App Service Authentication**, turn authentication **On**.</span></span> <span data-ttu-id="f14ca-203">在 [驗證提供者] 下，選擇 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="f14ca-203">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span>

   ![開啟驗證](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. <span data-ttu-id="f14ca-205">現在建立 Web 應用程式或 API 應用程式的應用程式識別碼，如下所示。</span><span class="sxs-lookup"><span data-stu-id="f14ca-205">Now create an application identity for your web app or API app as shown here.</span></span> <span data-ttu-id="f14ca-206">在 [Azure Active Directory 設定] 刀鋒視窗上，將 [管理模式] 設定為 [快速]。</span><span class="sxs-lookup"><span data-stu-id="f14ca-206">On the **Azure Active Directory Settings** blade, set **Management mode** to **Express**.</span></span> <span data-ttu-id="f14ca-207">選擇 [建立新的 AD 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f14ca-207">Choose **Create New AD App**.</span></span> <span data-ttu-id="f14ca-208">為您的應用程式識別碼提供名稱，然後選擇 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="f14ca-208">Give your application identity a name, and choose **OK**.</span></span> 

   ![建立 Web 應用程式或 API 應用程式的應用程式識別碼](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. <span data-ttu-id="f14ca-210">在 [驗證/授權] 刀鋒視窗上，選擇 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="f14ca-210">On the **Authentication / Authorization blade**, choose **Save**.</span></span>

<span data-ttu-id="f14ca-211">現在您必須尋找的應用程式識別碼之用戶端識別碼和租用戶識別碼，是與您的 web 應用程式或 API 應用程式相關聯。</span><span class="sxs-lookup"><span data-stu-id="f14ca-211">Now you must find the client ID and tenant ID for the application identity that's associated with your web app or API app.</span></span> <span data-ttu-id="f14ca-212">您可以在第 3 部分中使用這些識別碼。</span><span class="sxs-lookup"><span data-stu-id="f14ca-212">You use these IDs in Part 3.</span></span> <span data-ttu-id="f14ca-213">因此，繼續執行 Azure 入口網站或 [Azure 傳統入口網站](#find-id-classic)的下列步驟。</span><span class="sxs-lookup"><span data-stu-id="f14ca-213">So continue with these steps for the Azure portal or [Azure classic portal](#find-id-classic).</span></span>

<span data-ttu-id="f14ca-214">**在 Azure 入口網站中尋找 web 應用程式或 API 應用程式的應用程式識別碼之用戶端識別碼和租用戶識別碼**</span><span class="sxs-lookup"><span data-stu-id="f14ca-214">**Find application identity's client ID and tenant ID for your web app or API app in the Azure portal**</span></span>

1. <span data-ttu-id="f14ca-215">在 [驗證提供者] 下，選擇 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="f14ca-215">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span> 

   ![選擇 [Azure Active Directory]](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. <span data-ttu-id="f14ca-217">在 [Azure Active Directory 設定] 刀鋒視窗上，將 [管理模式] 設定為 [進階]。</span><span class="sxs-lookup"><span data-stu-id="f14ca-217">On the **Azure Active Directory Settings** blade, set **Management mode** to **Advanced**.</span></span>

3. <span data-ttu-id="f14ca-218">複製 [用戶端識別碼]，並儲存用於第 3 部分的 GUID。</span><span class="sxs-lookup"><span data-stu-id="f14ca-218">Copy the **Client ID**, and save that GUID for use in Part 3.</span></span>

   > [!TIP] 
   > <span data-ttu-id="f14ca-219">如果未出現 [用戶端識別碼] 和 [簽發者 URL]，請嘗試重新整理 Azure 入口網站，然後重複步驟 1。</span><span class="sxs-lookup"><span data-stu-id="f14ca-219">If **Client ID** and **Issuer Url** don't appear, try refreshing the Azure portal, and repeat Step 1.</span></span>

4. <span data-ttu-id="f14ca-220">在 [簽發者 URL] 下，僅複製並儲存用於第 3 部分的 GUID。</span><span class="sxs-lookup"><span data-stu-id="f14ca-220">Under **Issuer Url**, copy and save just the GUID for Part 3.</span></span> <span data-ttu-id="f14ca-221">您也可以視需要在您的 web 應用程式或 API 應用程式的部署範本中使用此 GUID。</span><span class="sxs-lookup"><span data-stu-id="f14ca-221">You can also use this GUID in your web app or API app's deployment template, if necessary.</span></span>

   <span data-ttu-id="f14ca-222">此 GUID 是您特定租用戶的 GUID (「租用戶 ID」)，且應該會出現在此 URL：`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="f14ca-222">This GUID is your specific tenant's GUID ("tenant ID") and should appear in this URL: `https://sts.windows.net/{GUID}`</span></span>

5. <span data-ttu-id="f14ca-223">無須儲存變更，關閉 [Azure Active Directory 設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f14ca-223">Without saving your changes, close the **Azure Active Directory Settings** blade.</span></span>

<a name="find-id-classic"></a>

<span data-ttu-id="f14ca-224">**在 Azure 傳統入口網站中尋找 web 應用程式或 API 應用程式的應用程式識別碼之用戶端識別碼和租用戶識別碼**</span><span class="sxs-lookup"><span data-stu-id="f14ca-224">**Find application identity's client ID and tenant ID for your web app or API app in the Azure classic portal**</span></span>

1. <span data-ttu-id="f14ca-225">在 Azure 傳統入口網站中，選擇 [**[Active Directory]**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory) 。</span><span class="sxs-lookup"><span data-stu-id="f14ca-225">In the Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2.  <span data-ttu-id="f14ca-226">選取您用於 Web 應用程式或 API 應用程式的目錄。</span><span class="sxs-lookup"><span data-stu-id="f14ca-226">Select the directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="f14ca-227">在 [搜尋] 方塊中，尋找並選取 web 應用程式或 API 應用程式的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="f14ca-227">In the **Search** box, find and select the application identity for your web app or API app.</span></span>

4. <span data-ttu-id="f14ca-228">在 [設定] 索引標籤上，複製 [用戶端識別碼]，並儲存用於第 3 部分的 GUID。</span><span class="sxs-lookup"><span data-stu-id="f14ca-228">On the **Configure** tab, copy the **Client ID**, and save that GUID for use in Part 3.</span></span>

5. <span data-ttu-id="f14ca-229">取得用戶端識別碼之後，請在 [設定] 索引標籤上選擇 [檢視端點]。</span><span class="sxs-lookup"><span data-stu-id="f14ca-229">After you get the client ID, at the bottom of the **Configure** tab, choose **View endpoints**.</span></span>

6. <span data-ttu-id="f14ca-230">複製 [同盟中繼資料文件] 的 URL，並瀏覽至該 URL。</span><span class="sxs-lookup"><span data-stu-id="f14ca-230">Copy the URL for **Federation Metadata Document**, and browse to that URL.</span></span>

7. <span data-ttu-id="f14ca-231">在隨即開啟的中繼資料文件中，尋找根 **EntityDescriptor ID** 元素，其具有以下形式的 **entityID** 屬性：`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="f14ca-231">In the metadata document that opens, find the root **EntityDescriptor ID** element, which has an **entityID** attribute in this form: `https://sts.windows.net/{GUID}`</span></span> 

      <span data-ttu-id="f14ca-232">這個屬性中的 GUID 是特定租用戶的 GUID (租用戶 ID)。</span><span class="sxs-lookup"><span data-stu-id="f14ca-232">The GUID in this attribute is your specific tenant's GUID (tenant ID).</span></span>

8. <span data-ttu-id="f14ca-233">複製租用戶識別碼，並儲存該識別碼以在第 3 部分中使用，並視需要也在您 web 應用程式或 API 應用程式的部署範本中使用。</span><span class="sxs-lookup"><span data-stu-id="f14ca-233">Copy the tenant ID and save that ID for use in Part 3, and also to use in your web app or API app's deployment template, if necessary.</span></span>

<span data-ttu-id="f14ca-234">如需詳細資訊，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="f14ca-234">For more information, see these topics:</span></span>

* [<span data-ttu-id="f14ca-235">Azure App Service 中 API 應用程式的使用者驗證</span><span class="sxs-lookup"><span data-stu-id="f14ca-235">User authentication for API apps in Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [<span data-ttu-id="f14ca-236">Azure App Service 中的驗證與授權</span><span class="sxs-lookup"><span data-stu-id="f14ca-236">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

<span data-ttu-id="f14ca-237">**在您使用 Azure Resource Manager 範本進行部署時開啟驗證**</span><span class="sxs-lookup"><span data-stu-id="f14ca-237">**Turn on authentication when you deploy with an Azure Resource Manager template**</span></span>

<span data-ttu-id="f14ca-238">您還是必須建立 web 應用程式或 API 應用程式的 Azure AD 應用程式識別碼，其與邏輯應用程式的應用程式識別碼不同。</span><span class="sxs-lookup"><span data-stu-id="f14ca-238">You must still create an Azure AD application identity for your web app or API app that differs from the app identity for your logic app.</span></span> <span data-ttu-id="f14ca-239">若要建立應用程式識別碼，請遵循第 2 部分中 Azure 入口網站的先前步驟。</span><span class="sxs-lookup"><span data-stu-id="f14ca-239">To create the application identity, follow the previous steps in Part 2 for the Azure portal.</span></span> <span data-ttu-id="f14ca-240">您也可以遵循第 1 部分中的步驟，但請務必使用您的 web 應用程式或 API 應用程式適用於**登入 URL** 和**應用程式識別碼 URI** 的實際 `https://{URL}`。</span><span class="sxs-lookup"><span data-stu-id="f14ca-240">You can also follow the steps in Part 1, but make sure to use your web app or API app's actual `https://{URL}` for **Sign-on URL** and **App ID URI**.</span></span> <span data-ttu-id="f14ca-241">在這些步驟中，您必須儲存用戶端識別碼和租用戶識別碼，以在您應用程式的部署範本以及用於第 3 部分中使用。</span><span class="sxs-lookup"><span data-stu-id="f14ca-241">From these steps, you have to save both the client ID and tenant ID for use in your app's deployment template and also for Part 3.</span></span>

> [!NOTE]
> <span data-ttu-id="f14ca-242">當您建立 web 應用程式或 API 應用程式的 Azure AD 應用程式識別碼時，必須使用 Azure 入口網站或 Azure 傳統入口網站，而不是 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f14ca-242">When you create the Azure AD application identity for your web app or API app, you must use the Azure portal or Azure classic portal, rather than PowerShell.</span></span> <span data-ttu-id="f14ca-243">PowerShell commandlet 不會設定使用者登入網站的必要權限。</span><span class="sxs-lookup"><span data-stu-id="f14ca-243">The PowerShell commandlet doesn't set up the required permissions to sign users into a website.</span></span>

<span data-ttu-id="f14ca-244">取得用戶端識別碼和租用戶識別碼後，請在部署範本中納入這些識別碼，作為 Web 應用程式或 API 應用程式的子資源：</span><span class="sxs-lookup"><span data-stu-id="f14ca-244">After you get the client ID and tenant ID, include these IDs as a subresource of your web app or API app in your deployment template:</span></span>

   ```
   "resources": [
       {
           "apiVersion": "2015-08-01",
           "name": "web",
           "type": "config",
           "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
           "properties": {
               "siteAuthEnabled": true,
               "siteAuthSettings": {
                 "clientId": "{client-ID}",
                 "issuer": "https://sts.windows.net/{tenant-ID}/",
               }
           }
       }
   ]
   ```

<span data-ttu-id="f14ca-245">若要自動將空白 web 應用程式和邏輯應用程式與 Azure Active Directory 驗證共同部署，請[在這裡檢視完整範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json)，或在這裡按一下 [部署至 Azure]：</span><span class="sxs-lookup"><span data-stu-id="f14ca-245">To automatically deploy a blank web app and a logic app together with Azure Active Directory authentication, [view the complete template here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), or click **Deploy to Azure** here:</span></span>

<span data-ttu-id="f14ca-246">[![部署至 Azure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="f14ca-246">[![Deploy to Azure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span></span>

#### <a name="part-3-populate-the-authorization-section-in-your-logic-app"></a><span data-ttu-id="f14ca-247">第 3 部分：填入邏輯應用程式中的授權區段</span><span class="sxs-lookup"><span data-stu-id="f14ca-247">Part 3: Populate the Authorization section in your logic app</span></span>

<span data-ttu-id="f14ca-248">前一個範本已設定此授權區段，但如果您要直接撰寫邏輯應用程式，則必須包含完整的授權區段。</span><span class="sxs-lookup"><span data-stu-id="f14ca-248">The previous template already has this authorization section set up, but if you are directly authoring the logic app, you must include the full authorization section.</span></span>

<span data-ttu-id="f14ca-249">在程式碼檢視中開啟您的邏輯應用程式定義、移至 [HTTP] 動作區段、尋找 [授權] 區段，並納入這一行：</span><span class="sxs-lookup"><span data-stu-id="f14ca-249">Open your logic app definition in code view, go to the **HTTP** action section, find the **Authorization** section, and include this line:</span></span>

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| <span data-ttu-id="f14ca-250">元素</span><span class="sxs-lookup"><span data-stu-id="f14ca-250">Element</span></span> | <span data-ttu-id="f14ca-251">說明</span><span class="sxs-lookup"><span data-stu-id="f14ca-251">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="f14ca-252">tenant</span><span class="sxs-lookup"><span data-stu-id="f14ca-252">tenant</span></span> |<span data-ttu-id="f14ca-253">Azure AD 租用戶的 GUID</span><span class="sxs-lookup"><span data-stu-id="f14ca-253">The GUID for the Azure AD tenant</span></span> |
| <span data-ttu-id="f14ca-254">audience</span><span class="sxs-lookup"><span data-stu-id="f14ca-254">audience</span></span> |<span data-ttu-id="f14ca-255">必要。</span><span class="sxs-lookup"><span data-stu-id="f14ca-255">Required.</span></span> <span data-ttu-id="f14ca-256">您想要存取之目標資源的 GUID - 來自您 web 應用程式或 API 應用程式的應用程式識別碼之用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="f14ca-256">The GUID for the target resource that you want to access - the client ID from the application identity for your web app or API app</span></span> |
| <span data-ttu-id="f14ca-257">clientId</span><span class="sxs-lookup"><span data-stu-id="f14ca-257">clientId</span></span> |<span data-ttu-id="f14ca-258">要求存取之用戶端的 GUID - 來自您邏輯應用程式的應用程式識別碼之用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="f14ca-258">The GUID for the client requesting access - the client ID from the application identity for your logic app</span></span> |
| <span data-ttu-id="f14ca-259">secret</span><span class="sxs-lookup"><span data-stu-id="f14ca-259">secret</span></span> |<span data-ttu-id="f14ca-260">必要。</span><span class="sxs-lookup"><span data-stu-id="f14ca-260">Required.</span></span> <span data-ttu-id="f14ca-261">來自要求存取權杖的用戶端之應用程式識別碼的金鑰或密碼</span><span class="sxs-lookup"><span data-stu-id="f14ca-261">The key or password from the application identity for the client that's requesting the access token</span></span> |
| <span data-ttu-id="f14ca-262">類型</span><span class="sxs-lookup"><span data-stu-id="f14ca-262">type</span></span> |<span data-ttu-id="f14ca-263">驗證類型。</span><span class="sxs-lookup"><span data-stu-id="f14ca-263">The authentication type.</span></span> <span data-ttu-id="f14ca-264">若為 ActiveDirectoryOAuth 驗證，值為 `ActiveDirectoryOAuth`。</span><span class="sxs-lookup"><span data-stu-id="f14ca-264">For ActiveDirectoryOAuth authentication, the value is `ActiveDirectoryOAuth`.</span></span> |

<span data-ttu-id="f14ca-265">例如：</span><span class="sxs-lookup"><span data-stu-id="f14ca-265">For example:</span></span>

```
{
   ...
   "actions": {
      "some-action": {
         "conditions": [],
         "inputs": {
            "method": "post",
            "uri": "https://your-api-azurewebsites.net/api/your-method",
            "authentication": {
               "tenant": "tenant-ID",
               "audience": "client-ID-from-azure-ad-app-for-web-app-or-api-app",
               "clientId": "client-ID-from-azure-ad-app-for-logic-app",
               "secret": "key-from-azure-ad-app-for-logic-app",
               "type": "ActiveDirectoryOAuth"
            }
         },
      }
   }
}
```

<a name="update-code"></a>

### <a name="secure-api-calls-through-code"></a><span data-ttu-id="f14ca-266">透過程式碼保護 API 呼叫</span><span class="sxs-lookup"><span data-stu-id="f14ca-266">Secure API calls through code</span></span>

<a name="certificate"></a>

#### <a name="certificate-authentication"></a><span data-ttu-id="f14ca-267">憑證驗證</span><span class="sxs-lookup"><span data-stu-id="f14ca-267">Certificate authentication</span></span>

<span data-ttu-id="f14ca-268">若要驗證邏輯應用程式傳入 Web 應用程式或 API 應用程式中的要求，您可以使用用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="f14ca-268">To validate the incoming requests from your logic app to your web app or API app, you can use client certificates.</span></span> <span data-ttu-id="f14ca-269">如需設定程式碼，請了解[如何設定 TLS 相互驗證](../app-service-web/app-service-web-configure-tls-mutual-auth.md)。</span><span class="sxs-lookup"><span data-stu-id="f14ca-269">To set up your code, learn [how to configure TLS mutual authentication](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span>

<span data-ttu-id="f14ca-270">在 [授權] 區段中，納入這一行：</span><span class="sxs-lookup"><span data-stu-id="f14ca-270">In the **Authorization** section, include this line:</span></span> 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| <span data-ttu-id="f14ca-271">元素</span><span class="sxs-lookup"><span data-stu-id="f14ca-271">Element</span></span> | <span data-ttu-id="f14ca-272">說明</span><span class="sxs-lookup"><span data-stu-id="f14ca-272">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="f14ca-273">類型</span><span class="sxs-lookup"><span data-stu-id="f14ca-273">type</span></span> |<span data-ttu-id="f14ca-274">必要。</span><span class="sxs-lookup"><span data-stu-id="f14ca-274">Required.</span></span> <span data-ttu-id="f14ca-275">驗證類型。</span><span class="sxs-lookup"><span data-stu-id="f14ca-275">The authentication type.</span></span> <span data-ttu-id="f14ca-276">若為 SSL 用戶端憑證，值必須是 `ClientCertificate`。</span><span class="sxs-lookup"><span data-stu-id="f14ca-276">For SSL client certificates, the value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="f14ca-277">password</span><span class="sxs-lookup"><span data-stu-id="f14ca-277">password</span></span> |<span data-ttu-id="f14ca-278">必要。</span><span class="sxs-lookup"><span data-stu-id="f14ca-278">Required.</span></span> <span data-ttu-id="f14ca-279">用以存取用戶端憑證的密碼 (PFX 檔案)</span><span class="sxs-lookup"><span data-stu-id="f14ca-279">The password for accessing the client certificate (PFX file)</span></span> |
| <span data-ttu-id="f14ca-280">pfx</span><span class="sxs-lookup"><span data-stu-id="f14ca-280">pfx</span></span> |<span data-ttu-id="f14ca-281">必要。</span><span class="sxs-lookup"><span data-stu-id="f14ca-281">Required.</span></span> <span data-ttu-id="f14ca-282">用戶端憑證的 Base64 編碼內容 (PFX 檔案)</span><span class="sxs-lookup"><span data-stu-id="f14ca-282">Base64-encoded contents of the client certificate (PFX file)</span></span> |

<a name="basic"></a>

#### <a name="basic-authentication"></a><span data-ttu-id="f14ca-283">基本驗證</span><span class="sxs-lookup"><span data-stu-id="f14ca-283">Basic authentication</span></span>

<span data-ttu-id="f14ca-284">若要驗證邏輯應用程式傳入 Web 應用程式或 API 應用程式中的要求，您可以使用基本驗證，例如使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="f14ca-284">To validate incoming requests from your logic app to your web app or API app, you can use basic authentication, such as a username and password.</span></span> <span data-ttu-id="f14ca-285">基本驗證的常見模式，任何用來建置 Web 應用程式或 API 應用程式的語言都可以使用此驗證。</span><span class="sxs-lookup"><span data-stu-id="f14ca-285">Basic authentication is a common pattern, and you can use this authentication in any language used to build your web app or API app.</span></span>

<span data-ttu-id="f14ca-286">在 [授權] 區段中，納入這一行：</span><span class="sxs-lookup"><span data-stu-id="f14ca-286">In the **Authorization** section, include this line:</span></span>

<span data-ttu-id="f14ca-287">`{"type": "basic", "username": "username", "password": "password"}`。</span><span class="sxs-lookup"><span data-stu-id="f14ca-287">`{"type": "basic", "username": "username", "password": "password"}`.</span></span>

| <span data-ttu-id="f14ca-288">元素</span><span class="sxs-lookup"><span data-stu-id="f14ca-288">Element</span></span> | <span data-ttu-id="f14ca-289">說明</span><span class="sxs-lookup"><span data-stu-id="f14ca-289">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f14ca-290">類型</span><span class="sxs-lookup"><span data-stu-id="f14ca-290">type</span></span> |<span data-ttu-id="f14ca-291">必要。</span><span class="sxs-lookup"><span data-stu-id="f14ca-291">Required.</span></span> <span data-ttu-id="f14ca-292">驗證類型。</span><span class="sxs-lookup"><span data-stu-id="f14ca-292">The authentication type.</span></span> <span data-ttu-id="f14ca-293">若為基本驗證，值必須是 `Basic`。</span><span class="sxs-lookup"><span data-stu-id="f14ca-293">For basic authentication, the value must be `Basic`.</span></span> |
| <span data-ttu-id="f14ca-294">username</span><span class="sxs-lookup"><span data-stu-id="f14ca-294">username</span></span> |<span data-ttu-id="f14ca-295">必要。</span><span class="sxs-lookup"><span data-stu-id="f14ca-295">Required.</span></span> <span data-ttu-id="f14ca-296">驗證的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="f14ca-296">The username for authentication</span></span> |
| <span data-ttu-id="f14ca-297">password</span><span class="sxs-lookup"><span data-stu-id="f14ca-297">password</span></span> |<span data-ttu-id="f14ca-298">必要。</span><span class="sxs-lookup"><span data-stu-id="f14ca-298">Required.</span></span> <span data-ttu-id="f14ca-299">驗證的密碼</span><span class="sxs-lookup"><span data-stu-id="f14ca-299">The password for authentication</span></span> |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a><span data-ttu-id="f14ca-300">透過程式碼驗證 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f14ca-300">Azure Active Directory authentication through code</span></span>

<span data-ttu-id="f14ca-301">根據預設，您在 Azure 入口網站中開啟的 Azure AD 驗證不提供精細的授權。</span><span class="sxs-lookup"><span data-stu-id="f14ca-301">By default, the Azure AD authentication that you turn on in the Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="f14ca-302">例如，這項驗證會將您的 API 鎖定為僅限特定租用戶，而非特定使用者或應用程式。</span><span class="sxs-lookup"><span data-stu-id="f14ca-302">For example, this authentication locks your API to just a specific tenant, not to a specific user or app.</span></span> 

<span data-ttu-id="f14ca-303">若要限制 API 透過程式碼存取您的邏輯應用程式，請擷取具有 JSON Web 權杖 (JWT) 的標頭。</span><span class="sxs-lookup"><span data-stu-id="f14ca-303">To restrict API access to your logic app through code, extract the header that has the JSON web token (JWT).</span></span> <span data-ttu-id="f14ca-304">檢查呼叫者的身分識別，並拒絕不相符的要求。</span><span class="sxs-lookup"><span data-stu-id="f14ca-304">Check the caller's identity, and reject requests that don't match.</span></span>

<span data-ttu-id="f14ca-305">此外，若要完全在自己的程式碼中實作這項驗證，而不使用 Azure 入口網站，請了解如何[在 Azure 應用程式中使用內部部署 Active Directory 進行驗證](../app-service-web/web-sites-authentication-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="f14ca-305">Going further, to implement this authentication entirely in your own code, and not use the Azure portal, learn how to [authenticate with on-premises Active Directory in your Azure app](../app-service-web/web-sites-authentication-authorization.md).</span></span>

<span data-ttu-id="f14ca-306">若要建立邏輯應用程式的應用程式識別碼，並使用此身分識別來呼叫您的 API，您必須遵循前述步驟。</span><span class="sxs-lookup"><span data-stu-id="f14ca-306">To create an application identity for your logic app and use that identity to call your API, you must follow the previous steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f14ca-307">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f14ca-307">Next steps</span></span>

* [<span data-ttu-id="f14ca-308">使用診斷記錄及警示檢查邏輯應用程式效能</span><span class="sxs-lookup"><span data-stu-id="f14ca-308">Check logic app performance with diagnostic logs and alerts</span></span>](logic-apps-monitor-your-logic-apps.md)