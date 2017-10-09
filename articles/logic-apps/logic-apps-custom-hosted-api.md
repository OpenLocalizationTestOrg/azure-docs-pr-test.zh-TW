---
title: "aaaDeploy，呼叫，並驗證 web 應用程式開發介面 （& s） REST Api 針對 Azure 邏輯應用程式 |Microsoft 文件"
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
ms.openlocfilehash: ca1e4f28196b21f43b7c9ab94029684121e36f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a><span data-ttu-id="9763f-104">部署、呼叫並驗證自訂 API 作為 Logic Apps 的連接器</span><span class="sxs-lookup"><span data-stu-id="9763f-104">Deploy, call, and authenticate custom APIs as connectors for logic apps</span></span>

<span data-ttu-id="9763f-105">之後您[建立自訂 Api](./logic-apps-create-api-app.md) ，提供邏輯在動作或觸發程序 toouse 應用程式工作流程，可以呼叫之前，您必須部署您的應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="9763f-105">After you [create custom APIs](./logic-apps-create-api-app.md) that provide actions or triggers toouse in logic apps workflows, you must deploy your APIs before you can call them.</span></span> <span data-ttu-id="9763f-106">雖然 hello 達到最佳體驗效果，您可以從邏輯應用程式呼叫任何 API，新增和[Swagger 中繼資料](http://swagger.io/specification/)描述您的 API 作業和參數。</span><span class="sxs-lookup"><span data-stu-id="9763f-106">And although you can call any API from a logic app, for hello best experience, add [Swagger metadata](http://swagger.io/specification/) that describes your API's operations and parameters.</span></span> <span data-ttu-id="9763f-107">Swagger 檔案可協助您改善 API 工作，並更輕鬆地整合 Logic Apps。</span><span class="sxs-lookup"><span data-stu-id="9763f-107">This Swagger file helps your API work better and integrate more easily with logic apps.</span></span>

<span data-ttu-id="9763f-108">您可以部署與您 Api [web 應用程式](../app-service-web/app-service-web-overview.md)，但請考慮部署與您 Api [API apps](../app-service-api/app-service-api-apps-why-best-platform.md)，這可讓您的工作更容易當您建置、 裝載，並使用 Api hello 雲端與內部部署。</span><span class="sxs-lookup"><span data-stu-id="9763f-108">You can deploy your APIs as [web apps](../app-service-web/app-service-web-overview.md), but consider deploying your APIs as [API apps](../app-service-api/app-service-api-apps-why-best-platform.md), which can make your job easier when you build, host, and consume APIs in hello cloud and on premises.</span></span> <span data-ttu-id="9763f-109">您不需要 toochange 任何程式碼在您的應用程式開發介面中--只部署 tooan API 應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="9763f-109">You don't have toochange any code in your APIs -- just deploy your code tooan API app.</span></span> <span data-ttu-id="9763f-110">您可以在裝載您 Api [Azure App Service](../app-service/app-service-value-prop-what-is.md)、 平台做為服務 (PaaS) 供應項目，提供一種 hello 最佳、 簡單的方法，和擴充性最高裝載應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="9763f-110">You can host your APIs on [Azure App Service](../app-service/app-service-value-prop-what-is.md), a platform-as-a-service (PaaS) offering that provides one of hello best, easiest, and most scalable ways for API hosting.</span></span>

<span data-ttu-id="9763f-111">tooauthenticate 從邏輯應用程式 tooyour Api 的呼叫，您可以設定 Azure Active Directory 中 hello Azure 入口網站，您無需 tooupdate 您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9763f-111">tooauthenticate calls from logic apps tooyour APIs, you can set up Azure Active Directory in hello Azure portal so you don't have tooupdate your code.</span></span> <span data-ttu-id="9763f-112">或者，您可以透過您的 API 程式碼要求並強制執行驗證。</span><span class="sxs-lookup"><span data-stu-id="9763f-112">Or, you can require and enforce authentication through your API's code.</span></span>

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a><span data-ttu-id="9763f-113">將您的 API 部署為 web 應用程式或 API 應用程式</span><span class="sxs-lookup"><span data-stu-id="9763f-113">Deploy your API as a web app or API app</span></span>

<span data-ttu-id="9763f-114">您可以從邏輯應用程式呼叫自訂 API 之前，請將做為 web 應用程式或應用程式開發介面應用程式 tooAzure App Service API 部署。</span><span class="sxs-lookup"><span data-stu-id="9763f-114">Before you can call your custom API from a logic app, deploy your API as a web app or API app tooAzure App Service.</span></span> <span data-ttu-id="9763f-115">此外，toomake hello 邏輯應用程式的設計工具，供讀取文件 Swagger 設定 hello API 定義屬性並開啟[跨原始資源共用 (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig)的 web 應用程式或應用程式開發介面應用程式。</span><span class="sxs-lookup"><span data-stu-id="9763f-115">Also, toomake your Swagger document readable by hello Logic App Designer, set hello API definition properties and turn on [cross-origin resource sharing (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) for your web app or API app.</span></span>

1. <span data-ttu-id="9763f-116">在 hello Azure 入口網站，選取您的 web 應用程式或應用程式開發介面應用程式。</span><span class="sxs-lookup"><span data-stu-id="9763f-116">In hello Azure portal, select your web app or API app.</span></span>

2. <span data-ttu-id="9763f-117">在 hello 刀鋒視窗中開啟，底下**API**，選擇**API 定義**。</span><span class="sxs-lookup"><span data-stu-id="9763f-117">In hello blade that opens, under **API**, choose **API definition**.</span></span> <span data-ttu-id="9763f-118">設定 hello **API 定義位置**toohello swagger.json 檔案的 URL。</span><span class="sxs-lookup"><span data-stu-id="9763f-118">Set hello **API definition location** toohello URL for your swagger.json file.</span></span>

   <span data-ttu-id="9763f-119">通常，hello URL 會出現在這種格式：`https://{name}.azurewebsites.net/swagger/docs/v1)`</span><span class="sxs-lookup"><span data-stu-id="9763f-119">Usually, hello URL appears in this format: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span></span>

   ![自訂 api 的連結 tooSwagger 檔案](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. <span data-ttu-id="9763f-121">在 [API] 下，選擇 [CORS]。</span><span class="sxs-lookup"><span data-stu-id="9763f-121">Under **API**, choose **CORS**.</span></span> <span data-ttu-id="9763f-122">設定的 CORS 原則 hello**允許出處**太**'*'** （全部允許）。</span><span class="sxs-lookup"><span data-stu-id="9763f-122">Set hello CORS policy for **Allowed origins** too**'*'** (allow all).</span></span>

   <span data-ttu-id="9763f-123">此設定允許來自 Logic App Designer 的要求。</span><span class="sxs-lookup"><span data-stu-id="9763f-123">This setting permits requests from Logic App Designer.</span></span>

   ![允許從邏輯應用程式的設計工具 tooyour 自訂 API 要求](media/logic-apps-custom-hosted-api/custom-api-cors.png)

<span data-ttu-id="9763f-125">如需詳細資訊，請參閱這些文章：</span><span class="sxs-lookup"><span data-stu-id="9763f-125">For more information, see these articles:</span></span>

* [<span data-ttu-id="9763f-126">新增 ASP.NET web API 的 Swagger 中繼資料</span><span class="sxs-lookup"><span data-stu-id="9763f-126">Add Swagger metadata for ASP.NET web APIs</span></span>](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [<span data-ttu-id="9763f-127">部署 ASP.NET web Api tooAzure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="9763f-127">Deploy ASP.NET web APIs tooAzure App Service</span></span>](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a><span data-ttu-id="9763f-128">從邏輯應用程式工作流程呼叫自訂 API</span><span class="sxs-lookup"><span data-stu-id="9763f-128">Call your custom API from logic app workflows</span></span>

<span data-ttu-id="9763f-129">Hello API 定義屬性和 CORS 設定之後，您的自訂 API 的觸發程序和動作應該可用於 tooinclude 邏輯應用程式工作流程中。</span><span class="sxs-lookup"><span data-stu-id="9763f-129">After you set up hello API definition properties and CORS, your custom API's triggers and actions should become available for you tooinclude in your logic app workflow.</span></span> 

*  <span data-ttu-id="9763f-130">tooview hello 具有 Swagger Url 的網站，您可以瀏覽您的訂用帳戶網站在 hello 邏輯應用程式的設計工具中。</span><span class="sxs-lookup"><span data-stu-id="9763f-130">tooview hello websites that have Swagger URLs, you can browse your subscription websites in hello Logic Apps Designer.</span></span>

*  <span data-ttu-id="9763f-131">tooview 可用的動作，並指向 Swagger 文件中，輸入使用 hello [HTTP + Swagger 動作](../connectors/connectors-native-http-swagger.md)。</span><span class="sxs-lookup"><span data-stu-id="9763f-131">tooview available actions and inputs by pointing at a Swagger document, use hello [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).</span></span>

*  <span data-ttu-id="9763f-132">toocall 任何應用程式開發介面，包括應用程式開發介面不具有或公開 Swagger 文件中，您一律可以建立要求以 hello [HTTP 動作](../connectors/connectors-native-http.md)。</span><span class="sxs-lookup"><span data-stu-id="9763f-132">toocall any API, including APIs that don't have or expose a Swagger document, you can always create a request with hello [HTTP action](../connectors/connectors-native-http.md).</span></span>

## <a name="authenticate-calls-tooyour-custom-api"></a><span data-ttu-id="9763f-133">驗證呼叫 tooyour 自訂 API</span><span class="sxs-lookup"><span data-stu-id="9763f-133">Authenticate calls tooyour custom API</span></span>

<span data-ttu-id="9763f-134">您可以保護以下列方式呼叫 tooyour 自訂 API:</span><span class="sxs-lookup"><span data-stu-id="9763f-134">You can secure calls tooyour custom API in these ways:</span></span>

* <span data-ttu-id="9763f-135">[變更任何程式碼](#no-code)： 保護您的 API 與[Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md)透過 hello Azure 入口網站，因此您尚未 tooupdate 您的程式碼，或重新部署您的 API。</span><span class="sxs-lookup"><span data-stu-id="9763f-135">[No code changes](#no-code): Protect your API with [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) through hello Azure portal, so you don't have tooupdate your code or redeploy your API.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9763f-136">根據預設，開啟 hello Azure 入口網站中的 hello Azure AD 驗證不會提供更細緻的授權。</span><span class="sxs-lookup"><span data-stu-id="9763f-136">By default, hello Azure AD authentication that you turn on in hello Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="9763f-137">比方說，這項驗證會鎖定 API toojust 特定租用戶、 不 tooa 特定使用者或應用程式。</span><span class="sxs-lookup"><span data-stu-id="9763f-137">For example, this authentication locks your API toojust a specific tenant, not tooa specific user or app.</span></span> 

* <span data-ttu-id="9763f-138">[更新您的 API 程式碼](#update-code)：保護您的 API，方法是透過程式碼強制執行[憑證驗證](#certificate)、[基本驗證](#basic)，或 [Azure AD 驗證](#azure-ad-code)。</span><span class="sxs-lookup"><span data-stu-id="9763f-138">[Update your API's code](#update-code): Protect your API by enforcing [certificate authentication](#certificate), [basic authentication](#basic), or [Azure AD authentication](#azure-ad-code) through code.</span></span>

<a name="no-code"></a>

### <a name="authenticate-calls-tooyour-api-without-changing-code"></a><span data-ttu-id="9763f-139">驗證呼叫 tooyour 應用程式開發介面，而不需要變更程式碼</span><span class="sxs-lookup"><span data-stu-id="9763f-139">Authenticate calls tooyour API without changing code</span></span>

<span data-ttu-id="9763f-140">以下是 hello，此方法的一般步驟：</span><span class="sxs-lookup"><span data-stu-id="9763f-140">Here's hello general steps for this method:</span></span>

1. <span data-ttu-id="9763f-141">將建立兩個 [Azure Active Directory (Azure AD) 應用程式識別](../app-service-api/app-service-api-dotnet-service-principal-auth.md)：一個用於邏輯應用程式，一個用於 Web 應用程式 (或 API 應用程式)。</span><span class="sxs-lookup"><span data-stu-id="9763f-141">Create two [Azure Active Directory (Azure AD) application identities](../app-service-api/app-service-api-dotnet-service-principal-auth.md): one for your logic app and one for your web app (or API app).</span></span>

2. <span data-ttu-id="9763f-142">tooauthenticate 呼叫 tooyour 應用程式開發介面，用於 hello hello 認證 （用戶端識別碼和密碼）[服務主體](../app-service-api/app-service-api-dotnet-service-principal-auth.md)，具有相關聯的 hello 邏輯應用程式的 Azure AD 應用程式識別。</span><span class="sxs-lookup"><span data-stu-id="9763f-142">tooauthenticate calls tooyour API, use hello credentials (client ID and secret) for hello [service principal](../app-service-api/app-service-api-dotnet-service-principal-auth.md) that's associated with hello Azure AD application identity for your logic app.</span></span>

3. <span data-ttu-id="9763f-143">包含在邏輯應用程式定義中的 hello 應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="9763f-143">Include hello application IDs in your logic app definition.</span></span>

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a><span data-ttu-id="9763f-144">第 1 部分：建立 Azure AD 邏輯應用程式的應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="9763f-144">Part 1: Create an Azure AD application identity for your logic app</span></span>

<span data-ttu-id="9763f-145">邏輯應用程式會使用 Azure AD 中針對這個 Azure AD 應用程式識別 tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="9763f-145">Your logic app uses this Azure AD application identity tooauthenticate against Azure AD.</span></span> <span data-ttu-id="9763f-146">您只需要註冊這個身分識別 tooset 一次為您的目錄。</span><span class="sxs-lookup"><span data-stu-id="9763f-146">You only have tooset up this identity one time for your directory.</span></span> <span data-ttu-id="9763f-147">例如，您可以選擇 toouse hello 針對您的邏輯應用程式，相同的識別，即使您可以建立的每個邏輯應用程式的唯一身分識別。</span><span class="sxs-lookup"><span data-stu-id="9763f-147">For example, you can choose toouse hello same identity for all your logic apps, even though you can create unique identities for each logic app.</span></span> <span data-ttu-id="9763f-148">您可以設定在 hello Azure 入口網站，這些身分識別[Azure 傳統入口網站](#app-identity-logic-classic)，或使用[PowerShell](#powershell)。</span><span class="sxs-lookup"><span data-stu-id="9763f-148">You can set up these identities in hello Azure portal, [Azure classic portal](#app-identity-logic-classic), or use [PowerShell](#powershell).</span></span>

<span data-ttu-id="9763f-149">**在 hello Azure 入口網站中建立 hello 邏輯應用程式的應用程式識別**</span><span class="sxs-lookup"><span data-stu-id="9763f-149">**Create hello application identity for your logic app in hello Azure portal**</span></span>

1. <span data-ttu-id="9763f-150">在 hello [Azure 入口網站](https://portal.azure.com "https://portal.azure.com")，選擇**Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="9763f-150">In hello [Azure portal](https://portal.azure.com "https://portal.azure.com"), choose **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="9763f-151">確認您在 hello 與 web 應用程式或應用程式開發介面應用程式相同的目錄。</span><span class="sxs-lookup"><span data-stu-id="9763f-151">Confirm that you're in hello same directory as your web app or API app.</span></span>

   > [!TIP]
   > <span data-ttu-id="9763f-152">tooswitch 目錄中，按一下您的設定檔，然後選取另一個目錄。</span><span class="sxs-lookup"><span data-stu-id="9763f-152">tooswitch directories, click your profile and select another directory.</span></span> <span data-ttu-id="9763f-153">或者，選擇 [概觀] > [切換目錄]。</span><span class="sxs-lookup"><span data-stu-id="9763f-153">Or, choose **Overview** > **Switch directory**.</span></span>

3. <span data-ttu-id="9763f-154">Hello 目錄在功能表上，在**管理**，選擇**應用程式註冊** > **新應用程式註冊**。</span><span class="sxs-lookup"><span data-stu-id="9763f-154">On hello directory menu, under **Manage**, choose **App registrations** > **New application registration**.</span></span>

   > [!TIP]
   > <span data-ttu-id="9763f-155">根據預設，hello 應用程式註冊清單會顯示所有應用程式註冊您的目錄中。</span><span class="sxs-lookup"><span data-stu-id="9763f-155">By default, hello app registrations list shows all app registrations in your directory.</span></span> <span data-ttu-id="9763f-156">只有您的應用程式註冊下, 一步 toohello 搜尋方塊中，選取 tooview**我的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9763f-156">tooview only your app registrations, next toohello search box, select **My apps**.</span></span> 

   ![建立新的應用程式註冊](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. <span data-ttu-id="9763f-158">指定您的應用程式身分識別名稱，並保留**應用程式類型**設定得**Web 應用程式 / 應用程式開發介面**，提供唯一字串格式的網域為**登入 URL**，選擇**建立**。</span><span class="sxs-lookup"><span data-stu-id="9763f-158">Give your application identity a name, leave **Application type** set too**Web app / API**, provide a unique string formatted as a domain for **Sign-on URL**, and choose **Create**.</span></span>

   ![提供應用程式識別碼的名稱和登入 URL](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   <span data-ttu-id="9763f-160">您現在建立應用程式邏輯的 hello 應用程式識別碼會出現在 hello 應用程式註冊清單。</span><span class="sxs-lookup"><span data-stu-id="9763f-160">hello application identity that you created for your logic app now appears in hello app registrations list.</span></span>

   ![邏輯應用程式的應用程式識別碼](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. <span data-ttu-id="9763f-162">在 hello 應用程式註冊清單中，選取新的應用程式識別。</span><span class="sxs-lookup"><span data-stu-id="9763f-162">In hello app registrations list, select your new application identity.</span></span> <span data-ttu-id="9763f-163">複製並儲存 hello**應用程式識別碼**toouse 為 hello 「 用戶端識別碼 」，在第 3 篇應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="9763f-163">Copy and save hello **Application ID** toouse as hello "client ID" for your logic app in Part 3.</span></span>

   ![複製並儲存邏輯應用程式的應用程式識別碼](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. <span data-ttu-id="9763f-165">如果看不到您的應用程式識別碼設定，請選擇 [設定] 或 [所有設定]。</span><span class="sxs-lookup"><span data-stu-id="9763f-165">If your application identity settings aren't visible, choose **Settings** or **All settings**.</span></span>

7. <span data-ttu-id="9763f-166">在 [API 存取] 下，選擇 [金鑰]。</span><span class="sxs-lookup"><span data-stu-id="9763f-166">Under **API Access**, choose **Keys**.</span></span> <span data-ttu-id="9763f-167">在 [描述] 下，提供您金鑰的名稱。</span><span class="sxs-lookup"><span data-stu-id="9763f-167">Under **Description**, provide a name for your key.</span></span> <span data-ttu-id="9763f-168">在 [到期時間] 下，選取您金鑰的持續時間。</span><span class="sxs-lookup"><span data-stu-id="9763f-168">Under **Expires**, select a duration for your key.</span></span>

   <span data-ttu-id="9763f-169">您要建立 hello 金鑰做為 hello 應用程式識別的 「 密碼 」 或邏輯應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="9763f-169">hello key that you're creating acts as hello application identity's "secret" or password for your logic app.</span></span>

   ![建立邏輯應用程式身分識別的金鑰](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. <span data-ttu-id="9763f-171">在 hello 工具列上選擇 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="9763f-171">On hello toolbar, choose **Save**.</span></span> <span data-ttu-id="9763f-172">在 [值] 下，現在會顯示您的金鑰。</span><span class="sxs-lookup"><span data-stu-id="9763f-172">Under **Value**, your key now appears.</span></span> 
<span data-ttu-id="9763f-173">**請確定 toocopy 和儲存您的金鑰**供稍後使用隱藏 hello 索引鍵，因此當您離開 hello 金鑰刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9763f-173">**Make sure toocopy and save your key** for later use because hello key is hidden when you leave hello key blade.</span></span>

   <span data-ttu-id="9763f-174">當您在第 3 篇設定應用程式邏輯時，您指定這個機碼，如 hello 「 密碼 」 或密碼。</span><span class="sxs-lookup"><span data-stu-id="9763f-174">When you configure your logic app in Part 3, you specify this key as hello "secret" or password.</span></span>

   ![複製並儲存金鑰供稍後使用](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

<span data-ttu-id="9763f-176">**在 hello Azure 傳統入口網站中建立 hello 邏輯應用程式的應用程式識別**</span><span class="sxs-lookup"><span data-stu-id="9763f-176">**Create hello application identity for your logic app in hello Azure classic portal**</span></span>

1. <span data-ttu-id="9763f-177">在 hello Azure 傳統入口網站中選擇[ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory)。</span><span class="sxs-lookup"><span data-stu-id="9763f-177">In hello Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2. <span data-ttu-id="9763f-178">選取 hello 您用於 web 應用程式或應用程式開發介面應用程式的相同目錄。</span><span class="sxs-lookup"><span data-stu-id="9763f-178">Select hello same directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="9763f-179">在 hello**應用程式**索引標籤上，選擇**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="9763f-179">On hello **Applications** tab, choose **Add** at hello bottom of hello page.</span></span>

4. <span data-ttu-id="9763f-180">為您的應用程式識別碼提供名稱，然後選擇 **[下一步]** \(向右箭號)。</span><span class="sxs-lookup"><span data-stu-id="9763f-180">Give your application identity a name, and choose **Next** (right arrow).</span></span>

5. <span data-ttu-id="9763f-181">在 [應用程式屬性] 下，提供格式化為**登入 URL** 和**應用程式識別碼 URI** 之網域的唯一字串，然後選擇 [完成] \(勾選記號)。</span><span class="sxs-lookup"><span data-stu-id="9763f-181">Under **App properties**, provide a unique string formatted as a domain for **Sign-on URL** and **App ID URI**, and choose **Complete** (checkmark).</span></span>

6. <span data-ttu-id="9763f-182">在 hello**設定**索引標籤上，複製並儲存 hello**用戶端識別碼**如您在第 3 篇的邏輯應用程式 toouse。</span><span class="sxs-lookup"><span data-stu-id="9763f-182">On hello **Configure** tab, copy and save hello **Client ID** for your logic app toouse in Part 3.</span></span>

7. <span data-ttu-id="9763f-183">在下**金鑰**，開啟 hello**選取持續時間**清單。</span><span class="sxs-lookup"><span data-stu-id="9763f-183">Under **Keys**, open hello **Select duration** list.</span></span> <span data-ttu-id="9763f-184">選取您金鑰的持續時間。</span><span class="sxs-lookup"><span data-stu-id="9763f-184">Select a duration for your key.</span></span>

   <span data-ttu-id="9763f-185">您要建立 hello 金鑰做為 hello 應用程式識別的 「 密碼 」 或邏輯應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="9763f-185">hello key that you're creating acts as hello application identity's "secret" or password for your logic app.</span></span>

8. <span data-ttu-id="9763f-186">在 hello hello 頁面底部，選擇**儲存**。</span><span class="sxs-lookup"><span data-stu-id="9763f-186">At hello bottom of hello page, choose **Save**.</span></span> <span data-ttu-id="9763f-187">您可能必須 toowait 幾秒鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="9763f-187">You might have toowait a few seconds.</span></span>

9. <span data-ttu-id="9763f-188">在下**金鑰**，請確定 toocopy 儲存 hello 金鑰現在會出現。</span><span class="sxs-lookup"><span data-stu-id="9763f-188">Under **Keys**, make sure toocopy and save hello key that now appears.</span></span> 

   <span data-ttu-id="9763f-189">當您在第 3 篇設定應用程式邏輯時，您指定這個機碼，如 hello 「 密碼 」 或密碼。</span><span class="sxs-lookup"><span data-stu-id="9763f-189">When you configure your logic app in Part 3, you specify this key as hello "secret" or password.</span></span>

<span data-ttu-id="9763f-190">如需詳細資訊，了解如何太[設定您應用程式服務應用程式 toouse 的 Azure Active Directory 登入](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="9763f-190">For more information, learn how too [configure your App Service application toouse Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>

<a name="powershell"></a>

<span data-ttu-id="9763f-191">**在 PowerShell 中建立應用程式邏輯的 hello 應用程式識別**</span><span class="sxs-lookup"><span data-stu-id="9763f-191">**Create hello application identity for your logic app in PowerShell**</span></span>

<span data-ttu-id="9763f-192">您可以使用 PowerShell，透過 Azure Resource Manager 來執行這項工作中。</span><span class="sxs-lookup"><span data-stu-id="9763f-192">You can perform this task through Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="9763f-193">在 PowerShell 中，執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="9763f-193">In PowerShell, run these commands:</span></span>

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. <span data-ttu-id="9763f-194">請確定 toocopy hello**租用戶識別碼**(Azure AD 租用戶的 GUID)，hello**應用程式識別碼**，和您所使用的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="9763f-194">Make sure toocopy hello **Tenant ID** (GUID for your Azure AD tenant), hello **Application ID**, and hello password that you used.</span></span>

<span data-ttu-id="9763f-195">如需詳細資訊，了解如何太[PowerShell tooaccess 資源以建立服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md)。</span><span class="sxs-lookup"><span data-stu-id="9763f-195">For more information, learn how too [create a service principal with PowerShell tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a><span data-ttu-id="9763f-196">第 2 部分：建立 Web 應用程式或 API 應用程式的 Azure AD 應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="9763f-196">Part 2: Create an Azure AD application identity for your web app or API app</span></span>

<span data-ttu-id="9763f-197">如果已部署 web 應用程式或應用程式開發介面應用程式，則可以啟用驗證，並在 hello Azure 入口網站中建立 hello 應用程式識別。</span><span class="sxs-lookup"><span data-stu-id="9763f-197">If your web app or API app is already deployed, you can turn on authentication and create hello application identity in hello Azure portal.</span></span> <span data-ttu-id="9763f-198">否則，您可以[在您使用 Azure Resource Manager 範本進行部署時開啟驗證](#authen-deploy)。</span><span class="sxs-lookup"><span data-stu-id="9763f-198">Otherwise, you can [turn on authentication when you deploy with an Azure Resource Manager template](#authen-deploy).</span></span> 

<span data-ttu-id="9763f-199">**建立 hello 應用程式識別，然後開啟 hello 部署的應用程式的 Azure 入口網站中的驗證**</span><span class="sxs-lookup"><span data-stu-id="9763f-199">**Create hello application identity and turn on authentication in hello Azure portal for deployed apps**</span></span>

1. <span data-ttu-id="9763f-200">在 hello [Azure 入口網站](https://portal.azure.com "https://portal.azure.com")、 尋找並選取您的 web 應用程式或應用程式開發介面應用程式。</span><span class="sxs-lookup"><span data-stu-id="9763f-200">In hello [Azure portal](https://portal.azure.com "https://portal.azure.com"), find and select your web app or API app.</span></span> 

2. <span data-ttu-id="9763f-201">在 [設定] 下，選擇 [驗證/授權]。</span><span class="sxs-lookup"><span data-stu-id="9763f-201">Under **Settings**, choose **Authentication/Authorization**.</span></span> <span data-ttu-id="9763f-202">在 [App Service 驗證] 下，將驗證 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="9763f-202">Under **App Service Authentication**, turn authentication **On**.</span></span> <span data-ttu-id="9763f-203">在 [驗證提供者] 下，選擇 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="9763f-203">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span>

   ![開啟驗證](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. <span data-ttu-id="9763f-205">現在建立 Web 應用程式或 API 應用程式的應用程式識別碼，如下所示。</span><span class="sxs-lookup"><span data-stu-id="9763f-205">Now create an application identity for your web app or API app as shown here.</span></span> <span data-ttu-id="9763f-206">在 hello **Azure Active Directory 設定**刀鋒視窗中，設定**管理模式**太**Express**。</span><span class="sxs-lookup"><span data-stu-id="9763f-206">On hello **Azure Active Directory Settings** blade, set **Management mode** too**Express**.</span></span> <span data-ttu-id="9763f-207">選擇 [建立新的 AD 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9763f-207">Choose **Create New AD App**.</span></span> <span data-ttu-id="9763f-208">為您的應用程式識別碼提供名稱，然後選擇 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="9763f-208">Give your application identity a name, and choose **OK**.</span></span> 

   ![建立 Web 應用程式或 API 應用程式的應用程式識別碼](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. <span data-ttu-id="9763f-210">在 hello**驗證 / 授權刀鋒視窗**，選擇**儲存**。</span><span class="sxs-lookup"><span data-stu-id="9763f-210">On hello **Authentication / Authorization blade**, choose **Save**.</span></span>

<span data-ttu-id="9763f-211">現在您必須尋找 hello 用戶端識別碼和租用戶識別碼 hello 與 web 應用程式或應用程式開發介面應用程式相關聯的應用程式識別。</span><span class="sxs-lookup"><span data-stu-id="9763f-211">Now you must find hello client ID and tenant ID for hello application identity that's associated with your web app or API app.</span></span> <span data-ttu-id="9763f-212">您可以在第 3 部分中使用這些識別碼。</span><span class="sxs-lookup"><span data-stu-id="9763f-212">You use these IDs in Part 3.</span></span> <span data-ttu-id="9763f-213">因此繼續執行下列步驟 hello Azure 入口網站或[Azure 傳統入口網站](#find-id-classic)。</span><span class="sxs-lookup"><span data-stu-id="9763f-213">So continue with these steps for hello Azure portal or [Azure classic portal](#find-id-classic).</span></span>

<span data-ttu-id="9763f-214">**尋找應用程式識別用戶端識別碼和您的 web 應用程式或 hello Azure 入口網站中的應用程式開發介面應用程式的租用戶識別碼**</span><span class="sxs-lookup"><span data-stu-id="9763f-214">**Find application identity's client ID and tenant ID for your web app or API app in hello Azure portal**</span></span>

1. <span data-ttu-id="9763f-215">在 [驗證提供者] 下，選擇 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="9763f-215">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span> 

   ![選擇 [Azure Active Directory]](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. <span data-ttu-id="9763f-217">在 hello **Azure Active Directory 設定**刀鋒視窗中，設定**管理模式**太**進階**。</span><span class="sxs-lookup"><span data-stu-id="9763f-217">On hello **Azure Active Directory Settings** blade, set **Management mode** too**Advanced**.</span></span>

3. <span data-ttu-id="9763f-218">複製 hello**用戶端識別碼**，並將 GUID 用於儲存在第 3 篇。</span><span class="sxs-lookup"><span data-stu-id="9763f-218">Copy hello **Client ID**, and save that GUID for use in Part 3.</span></span>

   > [!TIP] 
   > <span data-ttu-id="9763f-219">如果**用戶端識別碼**和**簽發者 Url**不會出現，請嘗試重新整理 hello Azure 入口網站，重複步驟 1。</span><span class="sxs-lookup"><span data-stu-id="9763f-219">If **Client ID** and **Issuer Url** don't appear, try refreshing hello Azure portal, and repeat Step 1.</span></span>

4. <span data-ttu-id="9763f-220">在下**簽發者 Url**、 複製和儲存 just hello GUID 部分 3。</span><span class="sxs-lookup"><span data-stu-id="9763f-220">Under **Issuer Url**, copy and save just hello GUID for Part 3.</span></span> <span data-ttu-id="9763f-221">您也可以視需要在您的 web 應用程式或 API 應用程式的部署範本中使用此 GUID。</span><span class="sxs-lookup"><span data-stu-id="9763f-221">You can also use this GUID in your web app or API app's deployment template, if necessary.</span></span>

   <span data-ttu-id="9763f-222">此 GUID 是您特定租用戶的 GUID (「租用戶 ID」)，且應該會出現在此 URL：`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="9763f-222">This GUID is your specific tenant's GUID ("tenant ID") and should appear in this URL: `https://sts.windows.net/{GUID}`</span></span>

5. <span data-ttu-id="9763f-223">不儲存變更，關閉 hello **Azure Active Directory 設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9763f-223">Without saving your changes, close hello **Azure Active Directory Settings** blade.</span></span>

<a name="find-id-classic"></a>

<span data-ttu-id="9763f-224">**尋找應用程式識別用戶端識別碼和您的 web 應用程式或 hello Azure 傳統入口網站中的應用程式開發介面應用程式的租用戶識別碼**</span><span class="sxs-lookup"><span data-stu-id="9763f-224">**Find application identity's client ID and tenant ID for your web app or API app in hello Azure classic portal**</span></span>

1. <span data-ttu-id="9763f-225">在 hello Azure 傳統入口網站中選擇[ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory)。</span><span class="sxs-lookup"><span data-stu-id="9763f-225">In hello Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2.  <span data-ttu-id="9763f-226">選取您要用於 web 應用程式或應用程式開發介面應用程式的 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="9763f-226">Select hello directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="9763f-227">在 hello**搜尋**，尋找並選取 web 應用程式或應用程式開發介面應用程式的 hello 應用程式識別。</span><span class="sxs-lookup"><span data-stu-id="9763f-227">In hello **Search** box, find and select hello application identity for your web app or API app.</span></span>

4. <span data-ttu-id="9763f-228">在 hello**設定**索引標籤上，複製 hello**用戶端識別碼**，並儲存在第 3 篇使用 GUID。</span><span class="sxs-lookup"><span data-stu-id="9763f-228">On hello **Configure** tab, copy hello **Client ID**, and save that GUID for use in Part 3.</span></span>

5. <span data-ttu-id="9763f-229">取得 hello 用戶端識別碼，在 hello 底部 hello 之後**設定**索引標籤上，選擇**檢視端點**。</span><span class="sxs-lookup"><span data-stu-id="9763f-229">After you get hello client ID, at hello bottom of hello **Configure** tab, choose **View endpoints**.</span></span>

6. <span data-ttu-id="9763f-230">複製 hello URL**同盟中繼資料文件**，並瀏覽 toothat URL。</span><span class="sxs-lookup"><span data-stu-id="9763f-230">Copy hello URL for **Federation Metadata Document**, and browse toothat URL.</span></span>

7. <span data-ttu-id="9763f-231">在開啟 hello 中繼資料文件中尋找 hello 根**EntityDescriptor 識別碼**項目，其具有**entityID**這種形式的屬性：`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="9763f-231">In hello metadata document that opens, find hello root **EntityDescriptor ID** element, which has an **entityID** attribute in this form: `https://sts.windows.net/{GUID}`</span></span> 

      <span data-ttu-id="9763f-232">這個屬性中的 hello GUID 是特定租用戶的 GUID (租用戶 ID)。</span><span class="sxs-lookup"><span data-stu-id="9763f-232">hello GUID in this attribute is your specific tenant's GUID (tenant ID).</span></span>

8. <span data-ttu-id="9763f-233">複製 hello 租用戶識別碼，並視需要儲存在第 3 部分和 toouse 在您 web 應用程式或應用程式開發介面應用程式的部署範本，使用該識別碼。</span><span class="sxs-lookup"><span data-stu-id="9763f-233">Copy hello tenant ID and save that ID for use in Part 3, and also toouse in your web app or API app's deployment template, if necessary.</span></span>

<span data-ttu-id="9763f-234">如需詳細資訊，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="9763f-234">For more information, see these topics:</span></span>

* [<span data-ttu-id="9763f-235">Azure App Service 中 API 應用程式的使用者驗證</span><span class="sxs-lookup"><span data-stu-id="9763f-235">User authentication for API apps in Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [<span data-ttu-id="9763f-236">Azure App Service 中的驗證與授權</span><span class="sxs-lookup"><span data-stu-id="9763f-236">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

<span data-ttu-id="9763f-237">**在您使用 Azure Resource Manager 範本進行部署時開啟驗證**</span><span class="sxs-lookup"><span data-stu-id="9763f-237">**Turn on authentication when you deploy with an Azure Resource Manager template**</span></span>

<span data-ttu-id="9763f-238">您仍然必須從 hello 應用程式識別建立 web 應用程式或不同的應用程式開發介面應用程式的 Azure AD 應用程式身分識別，邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="9763f-238">You must still create an Azure AD application identity for your web app or API app that differs from hello app identity for your logic app.</span></span> <span data-ttu-id="9763f-239">toocreate hello 應用程式識別，後續 hello 先前步驟中第 2 部分 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="9763f-239">toocreate hello application identity, follow hello previous steps in Part 2 for hello Azure portal.</span></span> <span data-ttu-id="9763f-240">您也可以在第 1 部分中的 hello 步驟，但請確定 toouse web 應用程式或應用程式開發介面應用程式的實際`https://{URL}`如**登入 URL**和**應用程式識別碼 URI**。</span><span class="sxs-lookup"><span data-stu-id="9763f-240">You can also follow hello steps in Part 1, but make sure toouse your web app or API app's actual `https://{URL}` for **Sign-on URL** and **App ID URI**.</span></span> <span data-ttu-id="9763f-241">這些步驟中，您有 toosave 這兩個 hello 用戶端識別碼和您的應用程式部署範本中使用，也部分 3 的租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="9763f-241">From these steps, you have toosave both hello client ID and tenant ID for use in your app's deployment template and also for Part 3.</span></span>

> [!NOTE]
> <span data-ttu-id="9763f-242">當您建立 web 應用程式或應用程式開發介面應用程式的 hello Azure AD 應用程式識別時，您必須使用 hello Azure 入口網站或 Azure 傳統入口網站，而不是 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="9763f-242">When you create hello Azure AD application identity for your web app or API app, you must use hello Azure portal or Azure classic portal, rather than PowerShell.</span></span> <span data-ttu-id="9763f-243">hello PowerShell 指令程式不會設定所需的 hello 權限 toosign 使用者在網站。</span><span class="sxs-lookup"><span data-stu-id="9763f-243">hello PowerShell commandlet doesn't set up hello required permissions toosign users into a website.</span></span>

<span data-ttu-id="9763f-244">取得 hello 用戶端識別碼和租用戶識別碼之後，將這些識別碼納入 subresource web 應用程式或部署範本中的應用程式開發介面應用程式：</span><span class="sxs-lookup"><span data-stu-id="9763f-244">After you get hello client ID and tenant ID, include these IDs as a subresource of your web app or API app in your deployment template:</span></span>

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

<span data-ttu-id="9763f-245">tooautomatically 部署空白 web 應用程式和邏輯應用程式與 Azure Active Directory 驗證[檢視 hello 完成範本這裡](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json)，或按一下**部署 tooAzure**這裡：</span><span class="sxs-lookup"><span data-stu-id="9763f-245">tooautomatically deploy a blank web app and a logic app together with Azure Active Directory authentication, [view hello complete template here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), or click **Deploy tooAzure** here:</span></span>

<span data-ttu-id="9763f-246">[![部署 tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="9763f-246">[![Deploy tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span></span>

#### <a name="part-3-populate-hello-authorization-section-in-your-logic-app"></a><span data-ttu-id="9763f-247">第 3 部分： 填入邏輯應用程式中的 hello 授權 > 一節</span><span class="sxs-lookup"><span data-stu-id="9763f-247">Part 3: Populate hello Authorization section in your logic app</span></span>

<span data-ttu-id="9763f-248">hello 先前的範本已設定好之後，此授權 > 一節，但如果您直接撰寫 hello 邏輯應用程式，您必須包含 hello 完整授權 > 一節。</span><span class="sxs-lookup"><span data-stu-id="9763f-248">hello previous template already has this authorization section set up, but if you are directly authoring hello logic app, you must include hello full authorization section.</span></span>

<span data-ttu-id="9763f-249">開啟您的邏輯應用程式定義在程式碼檢視中，移 toohello **HTTP**動作 區段中，尋找 hello**授權**區段，並加入這一行：</span><span class="sxs-lookup"><span data-stu-id="9763f-249">Open your logic app definition in code view, go toohello **HTTP** action section, find hello **Authorization** section, and include this line:</span></span>

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| <span data-ttu-id="9763f-250">元素</span><span class="sxs-lookup"><span data-stu-id="9763f-250">Element</span></span> | <span data-ttu-id="9763f-251">說明</span><span class="sxs-lookup"><span data-stu-id="9763f-251">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="9763f-252">tenant</span><span class="sxs-lookup"><span data-stu-id="9763f-252">tenant</span></span> |<span data-ttu-id="9763f-253">hello GUID hello Azure AD 租用戶</span><span class="sxs-lookup"><span data-stu-id="9763f-253">hello GUID for hello Azure AD tenant</span></span> |
| <span data-ttu-id="9763f-254">audience</span><span class="sxs-lookup"><span data-stu-id="9763f-254">audience</span></span> |<span data-ttu-id="9763f-255">必要。</span><span class="sxs-lookup"><span data-stu-id="9763f-255">Required.</span></span> <span data-ttu-id="9763f-256">您想 tooaccess-hello hello web 應用程式或應用程式開發介面應用程式的應用程式識別用戶端識別碼 hello 目標資源的 hello GUID</span><span class="sxs-lookup"><span data-stu-id="9763f-256">hello GUID for hello target resource that you want tooaccess - hello client ID from hello application identity for your web app or API app</span></span> |
| <span data-ttu-id="9763f-257">clientId</span><span class="sxs-lookup"><span data-stu-id="9763f-257">clientId</span></span> |<span data-ttu-id="9763f-258">hello GUID hello 用戶端要求存取-hello hello 邏輯應用程式的應用程式識別用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="9763f-258">hello GUID for hello client requesting access - hello client ID from hello application identity for your logic app</span></span> |
| <span data-ttu-id="9763f-259">secret</span><span class="sxs-lookup"><span data-stu-id="9763f-259">secret</span></span> |<span data-ttu-id="9763f-260">必要。</span><span class="sxs-lookup"><span data-stu-id="9763f-260">Required.</span></span> <span data-ttu-id="9763f-261">hello 金鑰或密碼，從 hello hello hello 存取權杖要求的用戶端應用程式識別</span><span class="sxs-lookup"><span data-stu-id="9763f-261">hello key or password from hello application identity for hello client that's requesting hello access token</span></span> |
| <span data-ttu-id="9763f-262">類型</span><span class="sxs-lookup"><span data-stu-id="9763f-262">type</span></span> |<span data-ttu-id="9763f-263">hello 驗證類型。</span><span class="sxs-lookup"><span data-stu-id="9763f-263">hello authentication type.</span></span> <span data-ttu-id="9763f-264">ActiveDirectoryOAuth 驗證的 hello 值是`ActiveDirectoryOAuth`。</span><span class="sxs-lookup"><span data-stu-id="9763f-264">For ActiveDirectoryOAuth authentication, hello value is `ActiveDirectoryOAuth`.</span></span> |

<span data-ttu-id="9763f-265">例如：</span><span class="sxs-lookup"><span data-stu-id="9763f-265">For example:</span></span>

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

### <a name="secure-api-calls-through-code"></a><span data-ttu-id="9763f-266">透過程式碼保護 API 呼叫</span><span class="sxs-lookup"><span data-stu-id="9763f-266">Secure API calls through code</span></span>

<a name="certificate"></a>

#### <a name="certificate-authentication"></a><span data-ttu-id="9763f-267">憑證驗證</span><span class="sxs-lookup"><span data-stu-id="9763f-267">Certificate authentication</span></span>

<span data-ttu-id="9763f-268">toovalidate hello 源自的連入邏輯應用程式 tooyour web 應用程式或應用程式開發介面應用程式，您可以使用用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="9763f-268">toovalidate hello incoming requests from your logic app tooyour web app or API app, you can use client certificates.</span></span> <span data-ttu-id="9763f-269">深入了解程式碼，tooset[如何 tooconfigure TLS 相互驗證](../app-service-web/app-service-web-configure-tls-mutual-auth.md)。</span><span class="sxs-lookup"><span data-stu-id="9763f-269">tooset up your code, learn [how tooconfigure TLS mutual authentication](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span>

<span data-ttu-id="9763f-270">在 hello**授權**區段中，加入這一行：</span><span class="sxs-lookup"><span data-stu-id="9763f-270">In hello **Authorization** section, include this line:</span></span> 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| <span data-ttu-id="9763f-271">元素</span><span class="sxs-lookup"><span data-stu-id="9763f-271">Element</span></span> | <span data-ttu-id="9763f-272">說明</span><span class="sxs-lookup"><span data-stu-id="9763f-272">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="9763f-273">類型</span><span class="sxs-lookup"><span data-stu-id="9763f-273">type</span></span> |<span data-ttu-id="9763f-274">必要。</span><span class="sxs-lookup"><span data-stu-id="9763f-274">Required.</span></span> <span data-ttu-id="9763f-275">hello 驗證類型。</span><span class="sxs-lookup"><span data-stu-id="9763f-275">hello authentication type.</span></span> <span data-ttu-id="9763f-276">SSL 用戶端憑證，hello 值必須是`ClientCertificate`。</span><span class="sxs-lookup"><span data-stu-id="9763f-276">For SSL client certificates, hello value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="9763f-277">password</span><span class="sxs-lookup"><span data-stu-id="9763f-277">password</span></span> |<span data-ttu-id="9763f-278">必要。</span><span class="sxs-lookup"><span data-stu-id="9763f-278">Required.</span></span> <span data-ttu-id="9763f-279">hello 密碼存取 hello 用戶端憑證 （PFX 檔案）</span><span class="sxs-lookup"><span data-stu-id="9763f-279">hello password for accessing hello client certificate (PFX file)</span></span> |
| <span data-ttu-id="9763f-280">pfx</span><span class="sxs-lookup"><span data-stu-id="9763f-280">pfx</span></span> |<span data-ttu-id="9763f-281">必要。</span><span class="sxs-lookup"><span data-stu-id="9763f-281">Required.</span></span> <span data-ttu-id="9763f-282">Base64 編碼內容的 hello 用戶端憑證 （PFX 檔案）</span><span class="sxs-lookup"><span data-stu-id="9763f-282">Base64-encoded contents of hello client certificate (PFX file)</span></span> |

<a name="basic"></a>

#### <a name="basic-authentication"></a><span data-ttu-id="9763f-283">基本驗證</span><span class="sxs-lookup"><span data-stu-id="9763f-283">Basic authentication</span></span>

<span data-ttu-id="9763f-284">toovalidate 源自的連入邏輯應用程式 tooyour web 應用程式或應用程式開發介面應用程式，您可以使用基本驗證，例如使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="9763f-284">toovalidate incoming requests from your logic app tooyour web app or API app, you can use basic authentication, such as a username and password.</span></span> <span data-ttu-id="9763f-285">基本驗證是常見的模式，和 web 應用程式或應用程式開發介面應用程式，您可以使用任何語言使用 toobuild 在此驗證。</span><span class="sxs-lookup"><span data-stu-id="9763f-285">Basic authentication is a common pattern, and you can use this authentication in any language used toobuild your web app or API app.</span></span>

<span data-ttu-id="9763f-286">在 hello**授權**區段中，加入這一行：</span><span class="sxs-lookup"><span data-stu-id="9763f-286">In hello **Authorization** section, include this line:</span></span>

<span data-ttu-id="9763f-287">`{"type": "basic", "username": "username", "password": "password"}`。</span><span class="sxs-lookup"><span data-stu-id="9763f-287">`{"type": "basic", "username": "username", "password": "password"}`.</span></span>

| <span data-ttu-id="9763f-288">元素</span><span class="sxs-lookup"><span data-stu-id="9763f-288">Element</span></span> | <span data-ttu-id="9763f-289">說明</span><span class="sxs-lookup"><span data-stu-id="9763f-289">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9763f-290">類型</span><span class="sxs-lookup"><span data-stu-id="9763f-290">type</span></span> |<span data-ttu-id="9763f-291">必要。</span><span class="sxs-lookup"><span data-stu-id="9763f-291">Required.</span></span> <span data-ttu-id="9763f-292">hello 驗證類型。</span><span class="sxs-lookup"><span data-stu-id="9763f-292">hello authentication type.</span></span> <span data-ttu-id="9763f-293">Hello 值必須是基本驗證， `Basic`。</span><span class="sxs-lookup"><span data-stu-id="9763f-293">For basic authentication, hello value must be `Basic`.</span></span> |
| <span data-ttu-id="9763f-294">username</span><span class="sxs-lookup"><span data-stu-id="9763f-294">username</span></span> |<span data-ttu-id="9763f-295">必要。</span><span class="sxs-lookup"><span data-stu-id="9763f-295">Required.</span></span> <span data-ttu-id="9763f-296">hello 進行驗證的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="9763f-296">hello username for authentication</span></span> |
| <span data-ttu-id="9763f-297">password</span><span class="sxs-lookup"><span data-stu-id="9763f-297">password</span></span> |<span data-ttu-id="9763f-298">必要。</span><span class="sxs-lookup"><span data-stu-id="9763f-298">Required.</span></span> <span data-ttu-id="9763f-299">hello 密碼進行驗證</span><span class="sxs-lookup"><span data-stu-id="9763f-299">hello password for authentication</span></span> |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a><span data-ttu-id="9763f-300">透過程式碼驗證 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9763f-300">Azure Active Directory authentication through code</span></span>

<span data-ttu-id="9763f-301">根據預設，開啟 hello Azure 入口網站中的 hello Azure AD 驗證不會提供更細緻的授權。</span><span class="sxs-lookup"><span data-stu-id="9763f-301">By default, hello Azure AD authentication that you turn on in hello Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="9763f-302">比方說，這項驗證會鎖定 API toojust 特定租用戶、 不 tooa 特定使用者或應用程式。</span><span class="sxs-lookup"><span data-stu-id="9763f-302">For example, this authentication locks your API toojust a specific tenant, not tooa specific user or app.</span></span> 

<span data-ttu-id="9763f-303">toorestrict API 存取 tooyour 邏輯應用程式透過程式碼，擷取已 hello JSON web 權杖 (JWT) 的 hello 標頭。</span><span class="sxs-lookup"><span data-stu-id="9763f-303">toorestrict API access tooyour logic app through code, extract hello header that has hello JSON web token (JWT).</span></span> <span data-ttu-id="9763f-304">檢查 hello 呼叫者的身分識別，並拒絕不符合要求。</span><span class="sxs-lookup"><span data-stu-id="9763f-304">Check hello caller's identity, and reject requests that don't match.</span></span>

<span data-ttu-id="9763f-305">繼續進行，tooimplement 此驗證您自己的程式碼以及不使用 hello Azure 入口網站中的完全了解如何太[以在 Azure 應用程式中的內部部署 Active Directory 驗證](../app-service-web/web-sites-authentication-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="9763f-305">Going further, tooimplement this authentication entirely in your own code, and not use hello Azure portal, learn how too [authenticate with on-premises Active Directory in your Azure app](../app-service-web/web-sites-authentication-authorization.md).</span></span>

<span data-ttu-id="9763f-306">toocreate 邏輯應用程式的應用程式識別和使用該身分識別 toocall 您的 API，您必須依照 hello 先前的步驟。</span><span class="sxs-lookup"><span data-stu-id="9763f-306">toocreate an application identity for your logic app and use that identity toocall your API, you must follow hello previous steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9763f-307">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9763f-307">Next steps</span></span>

* [<span data-ttu-id="9763f-308">使用診斷記錄及警示檢查邏輯應用程式效能</span><span class="sxs-lookup"><span data-stu-id="9763f-308">Check logic app performance with diagnostic logs and alerts</span></span>](logic-apps-monitor-your-logic-apps.md)