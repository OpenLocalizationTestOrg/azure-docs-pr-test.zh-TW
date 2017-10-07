---
title: "aaaUse Azure Active Directory tooauthenticate 批次管理解決方案 |Microsoft 文件"
description: "使用 Azure 資源管理員所建立的應用程式和 hello 批次資源提供者向 Azure AD。"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/27/2017
ms.author: tamram
ms.openlocfilehash: 192aa9f8d7cbfc0282a4a0c33ab1659f1f351525
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a><span data-ttu-id="d69c6-103">使用 Active Directory 驗證 Batch Management 解決方案</span><span class="sxs-lookup"><span data-stu-id="d69c6-103">Authenticate Batch Management solutions with Active Directory</span></span>

<span data-ttu-id="d69c6-104">呼叫 hello Azure 批次管理服務應用程式向[Azure Active Directory] [ aad_about] (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="d69c6-104">Applications that call hello Azure Batch Management service authenticate with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="d69c6-105">Azure AD 是 Microsoft 的多租用戶雲端型目錄和身分識別管理服務。</span><span class="sxs-lookup"><span data-stu-id="d69c6-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="d69c6-106">Azure 本身會使用 Azure AD hello 驗證其客戶、 服務管理員和組織使用者。</span><span class="sxs-lookup"><span data-stu-id="d69c6-106">Azure itself uses Azure AD for hello authentication of its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="d69c6-107">hello Batch Management.NET 程式庫會公開使用批次帳戶，帳戶金鑰、 應用程式和應用程式封裝的類型。</span><span class="sxs-lookup"><span data-stu-id="d69c6-107">hello Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span></span> <span data-ttu-id="d69c6-108">hello Batch Management.NET 程式庫是 Azure 資源提供者用戶端，並會搭配[Azure Resource Manager] [ resman_overview] toomanage 這些資源以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="d69c6-108">hello Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] toomanage these resources programmatically.</span></span> <span data-ttu-id="d69c6-109">Azure AD 會透過任何 Azure 資源提供者用戶端，包括 hello Batch Management.NET 程式庫，以及透過需要的 tooauthenticate 要求[Azure Resource Manager][resman_overview]。</span><span class="sxs-lookup"><span data-stu-id="d69c6-109">Azure AD is required tooauthenticate requests made through any Azure resource provider client, including hello Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span>

<span data-ttu-id="d69c6-110">在本文中，我們會探討使用 Azure AD tooauthenticate 從使用 hello Batch Management.NET 程式庫的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d69c6-110">In this article, we explore using Azure AD tooauthenticate from applications that use hello Batch Management .NET library.</span></span> <span data-ttu-id="d69c6-111">我們會示範如何在 Azure AD toouse tooauthenticate 訂用帳戶管理員或共同管理員，使用整合式驗證。</span><span class="sxs-lookup"><span data-stu-id="d69c6-111">We show how toouse Azure AD tooauthenticate a subscription administrator or co-administrator, using integrated authentication.</span></span> <span data-ttu-id="d69c6-112">我們使用 hello [AccountManagment] [ acct_mgmt_sample] GitHub，toowalk 透過使用 Azure AD 與 hello Batch Management.NET 程式庫提供的範例專案。</span><span class="sxs-lookup"><span data-stu-id="d69c6-112">We use hello [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, toowalk through using Azure AD with hello Batch Management .NET library.</span></span>

<span data-ttu-id="d69c6-113">toolearn 進一步了解使用 hello Batch Management.NET 程式庫和 hello AccountManagement 範例，請參閱[管理批次帳戶與配額與.NET 的 hello 批次管理用戶端程式庫](batch-management-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="d69c6-113">toolearn more about using hello Batch Management .NET library and hello AccountManagement sample, see [Manage Batch accounts and quotas with hello Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

## <a name="register-your-application-with-azure-ad"></a><span data-ttu-id="d69c6-114">向 Azure AD 註冊您的應用程式</span><span class="sxs-lookup"><span data-stu-id="d69c6-114">Register your application with Azure AD</span></span>

<span data-ttu-id="d69c6-115">hello Azure [Active Directory Authentication Library] [ aad_adal] (ADAL) 提供應用程式中的程式設計介面 tooAzure AD 供使用。</span><span class="sxs-lookup"><span data-stu-id="d69c6-115">hello Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface tooAzure AD for use within your applications.</span></span> <span data-ttu-id="d69c6-116">toocall ADAL 從您的應用程式，您必須在 Azure AD 租用戶中註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d69c6-116">toocall ADAL from your application, you must register your application in an Azure AD tenant.</span></span> <span data-ttu-id="d69c6-117">當您註冊您的應用程式時，您會提供有關您的應用程式，包括其名稱 hello Azure AD 租用戶內資訊與 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="d69c6-117">When you register your application, you supply Azure AD with information about your application, including a name for it within hello Azure AD tenant.</span></span> <span data-ttu-id="d69c6-118">然後 azure AD 提供應用程式識別碼，搭配 tooassociate 您的應用程式在執行階段的 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="d69c6-118">Azure AD then provides an application ID that you use tooassociate your application with Azure AD at runtime.</span></span> <span data-ttu-id="d69c6-119">toolearn 深入了解 hello 應用程式識別碼，請參閱[應用程式與 Azure Active Directory 中的服務主體物件](../active-directory/develop/active-directory-application-objects.md)。</span><span class="sxs-lookup"><span data-stu-id="d69c6-119">toolearn more about hello application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="d69c6-120">tooregister hello AccountManagement 範例應用程式，請遵循 hello 中的 hello 步驟[來新增應用程式](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application)一節中[整合應用程式與 Azure Active Directory] [ aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="d69c6-120">tooregister hello AccountManagement sample application, follow hello steps in hello [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="d69c6-121">指定**原生用戶端應用程式**hello 種應用程式。</span><span class="sxs-lookup"><span data-stu-id="d69c6-121">Specify **Native Client Application** for hello type of application.</span></span> <span data-ttu-id="d69c6-122">hello 業界標準 OAuth 2.0 URI hello**重新導向 URI**是`urn:ietf:wg:oauth:2.0:oob`。</span><span class="sxs-lookup"><span data-stu-id="d69c6-122">hello industry standard OAuth 2.0 URI for hello **Redirect URI** is `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="d69c6-123">不過，您可以指定任何有效的 URI (例如`http://myaccountmanagementsample`) hello**重新導向 URI**，因為它並不需要 toobe 實際的端點：</span><span class="sxs-lookup"><span data-stu-id="d69c6-123">However, you can specify any valid URI (such as `http://myaccountmanagementsample`) for hello **Redirect URI**, as it does not need toobe a real endpoint:</span></span>

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

<span data-ttu-id="d69c6-124">一旦您完成 hello 註冊程序，您將看到 hello 應用程式識別碼，並 hello 列出您的應用程式的物件 （服務主體） 識別碼。</span><span class="sxs-lookup"><span data-stu-id="d69c6-124">Once you complete hello registration process, you'll see hello application ID and hello object (service principal) ID listed for your application.</span></span>  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-hello-azure-resource-manager-api-access-tooyour-application"></a><span data-ttu-id="d69c6-125">授與 hello Azure 資源管理員 API 存取 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="d69c6-125">Grant hello Azure Resource Manager API access tooyour application</span></span>

<span data-ttu-id="d69c6-126">接下來，您將需要 toodelegate 存取 tooyour 應用程式 toohello Azure 資源管理員 API。</span><span class="sxs-lookup"><span data-stu-id="d69c6-126">Next, you'll need toodelegate access tooyour application toohello Azure Resource Manager API.</span></span> <span data-ttu-id="d69c6-127">hello 資源管理員 API 的 hello Azure AD 識別項是**Windows Azure 服務管理 API**。</span><span class="sxs-lookup"><span data-stu-id="d69c6-127">hello Azure AD identifier for hello Resource Manager API is **Windows Azure Service Management API**.</span></span>

<span data-ttu-id="d69c6-128">請遵循這些步驟 hello Azure 入口網站中：</span><span class="sxs-lookup"><span data-stu-id="d69c6-128">Follow these steps in hello Azure portal:</span></span>

1. <span data-ttu-id="d69c6-129">在 hello 左側導覽窗格中的 hello Azure 入口網站，選擇 **更服務**，按一下**應用程式註冊**，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="d69c6-129">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
2. <span data-ttu-id="d69c6-130">搜尋 hello hello 清單中的應用程式註冊您應用程式名稱：</span><span class="sxs-lookup"><span data-stu-id="d69c6-130">Search for hello name of your application in hello list of app registrations:</span></span>

    ![搜尋您的應用程式名稱](./media/batch-aad-auth-management/search-app-registration.png)

3. <span data-ttu-id="d69c6-132">顯示 hello**設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d69c6-132">Display hello **Settings** blade.</span></span> <span data-ttu-id="d69c6-133">在 hello **API 存取**區段中，選取**必要的權限**。</span><span class="sxs-lookup"><span data-stu-id="d69c6-133">In hello **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="d69c6-134">按一下**新增**tooadd 新增必要的權限。</span><span class="sxs-lookup"><span data-stu-id="d69c6-134">Click **Add** tooadd a new required permission.</span></span> 
5. <span data-ttu-id="d69c6-135">在步驟 1 中，輸入**Windows Azure 服務管理 API**、 從 hello 結果的清單中選取該應用程式開發介面，然後按一下 hello**選取** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d69c6-135">In step 1, enter **Windows Azure Service Management API**, select that API from hello list of results, and click hello **Select** button.</span></span>
6. <span data-ttu-id="d69c6-136">在步驟 2 中，選取 hello 核取方塊旁太**做為組織的使用者存取 Azure 傳統部署模型**，然後按一下 hello**選取**按鈕。</span><span class="sxs-lookup"><span data-stu-id="d69c6-136">In step 2, select hello check box next too**Access Azure classic deployment model as organization users**, and click hello **Select** button.</span></span>
7. <span data-ttu-id="d69c6-137">按一下 hello**完成** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d69c6-137">Click hello **Done** button.</span></span>

<span data-ttu-id="d69c6-138">hello**必要的使用權限**現在顯示 tooyour 應用程式的權限會授與 tooboth hello ADAL 和資源管理員 Api 的 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d69c6-138">hello **Required Permissions** blade now shows that permissions tooyour application are granted tooboth hello ADAL and Resource Manager APIs.</span></span> <span data-ttu-id="d69c6-139">權限預設會授與 tooADAL 當您第一次使用 Azure AD 註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d69c6-139">Permissions are granted tooADAL by default when you first register your app with Azure AD.</span></span>

![委派權限 toohello Azure 資源管理員 API](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a><span data-ttu-id="d69c6-141">Azure AD 端點</span><span class="sxs-lookup"><span data-stu-id="d69c6-141">Azure AD endpoints</span></span>

<span data-ttu-id="d69c6-142">tooauthenticate 批次管理解決方案與 Azure AD，您將需要兩個已知的端點。</span><span class="sxs-lookup"><span data-stu-id="d69c6-142">tooauthenticate your Batch Management solutions with Azure AD, you'll need two well-known endpoints.</span></span>

- <span data-ttu-id="d69c6-143">hello **Azure AD 的一般端點**提供一般認證未提供特定租用戶，如同 hello 案例中整合式驗證時，收集介面：</span><span class="sxs-lookup"><span data-stu-id="d69c6-143">hello **Azure AD common endpoint** provides a generic credential gathering interface when a specific tenant is not provided, as in hello case of integrated authentication:</span></span>

    `https://login.microsoftonline.com/common`

- <span data-ttu-id="d69c6-144">hello **Azure 資源管理員端點**是使用的 tooacquire token 來驗證要求 toohello 批次管理服務：</span><span class="sxs-lookup"><span data-stu-id="d69c6-144">hello **Azure Resource Manager endpoint** is used tooacquire a token for authenticating requests toohello Batch management service:</span></span>

    `https://management.core.windows.net/`

<span data-ttu-id="d69c6-145">hello AccountManagement 範例應用程式定義這些端點的常數。</span><span class="sxs-lookup"><span data-stu-id="d69c6-145">hello AccountManagement sample application defines constants for these endpoints.</span></span> <span data-ttu-id="d69c6-146">將這些常數保留不變︰</span><span class="sxs-lookup"><span data-stu-id="d69c6-146">Leave these constants unchanged:</span></span>

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a><span data-ttu-id="d69c6-147">參考您的應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="d69c6-147">Reference your application ID</span></span> 

<span data-ttu-id="d69c6-148">用戶端應用程式會在執行階段使用 hello 應用程式識別碼 （也參考的 tooas hello 用戶端識別碼） tooaccess Azure AD。</span><span class="sxs-lookup"><span data-stu-id="d69c6-148">Your client application uses hello application ID (also referred tooas hello client ID) tooaccess Azure AD at runtime.</span></span> <span data-ttu-id="d69c6-149">一旦您已 hello Azure 入口網站中註冊您的應用程式，更新 Azure AD 註冊應用程式所提供您的程式碼 toouse hello 應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="d69c6-149">Once you've registered your application in hello Azure portal, update your code toouse hello application ID provided by Azure AD for your registered application.</span></span> <span data-ttu-id="d69c6-150">Hello AccountManagement 範例應用程式，可以從 hello Azure 入口網站 toohello 適當常數複製應用程式識別碼：</span><span class="sxs-lookup"><span data-stu-id="d69c6-150">In hello AccountManagement sample application, copy your application ID from hello Azure portal toohello appropriate constant:</span></span>

```csharp
// Specify hello unique identifier (hello "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access hello Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
<span data-ttu-id="d69c6-151">也請複製 hello 重新導向 hello 註冊程序期間所指定的 URI。</span><span class="sxs-lookup"><span data-stu-id="d69c6-151">Also copy hello redirect URI that you specified during hello registration process.</span></span> <span data-ttu-id="d69c6-152">hello 重新導向 URI 指定在您的程式碼必須符合 hello 重新導向時註冊 hello 應用程式所提供的 URI。</span><span class="sxs-lookup"><span data-stu-id="d69c6-152">hello redirect URI specified in your code must match hello redirect URI that you provided when you registered hello application.</span></span>

```csharp
// hello URI toowhich Azure AD will redirect in response tooan OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need toobe a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a><span data-ttu-id="d69c6-153">取得 Azure AD 驗證權杖</span><span class="sxs-lookup"><span data-stu-id="d69c6-153">Acquire an Azure AD authentication token</span></span>

<span data-ttu-id="d69c6-154">在 hello Azure AD 租用戶中註冊 hello AccountManagement 範例後，當您更新 hello 範例原始程式碼以您的值，hello 範例是使用 Azure AD 準備 tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="d69c6-154">After you register hello AccountManagement sample in hello Azure AD tenant and update hello sample source code with your values, hello sample is ready tooauthenticate using Azure AD.</span></span> <span data-ttu-id="d69c6-155">當您執行 hello 範例時，hello ADAL 嘗試 tooacquire 驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="d69c6-155">When you run hello sample, hello ADAL attempts tooacquire an authentication token.</span></span> <span data-ttu-id="d69c6-156">在此步驟中，它會提示您輸入您的 Microsoft 認證︰</span><span class="sxs-lookup"><span data-stu-id="d69c6-156">At this step, it prompts you for your Microsoft credentials:</span></span> 

```csharp
// Obtain an access token using hello "common" AAD resource. This allows hello application
// tooquery AAD for information that lies outside hello application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

<span data-ttu-id="d69c6-157">您提供認證之後，hello 範例應用程式可以繼續 tooissue 驗證要求 toohello 批次管理服務。</span><span class="sxs-lookup"><span data-stu-id="d69c6-157">After you provide your credentials, hello sample application can proceed tooissue authenticated requests toohello Batch management service.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d69c6-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d69c6-158">Next steps</span></span>

<span data-ttu-id="d69c6-159">如需有關執行 hello [AccountManagement 範例應用程式][acct_mgmt_sample]，請參閱[管理批次帳戶與配額與 hello 批次管理用戶端程式庫適用於.NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="d69c6-159">For more information on running hello [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with hello Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

<span data-ttu-id="d69c6-160">toolearn 進一步了解 Azure AD，請參閱 hello [Azure Active Directory 文件](https://docs.microsoft.com/azure/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="d69c6-160">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="d69c6-161">深入了解範例來示範如何 toouse ADAL 位於 hello [Azure 程式碼範例](https://azure.microsoft.com/resources/samples/?service=active-directory)程式庫。</span><span class="sxs-lookup"><span data-stu-id="d69c6-161">In-depth examples showing how toouse ADAL are available in hello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="d69c6-162">tooauthenticate 批次服務應用程式使用 Azure AD，請參閱[與 Active Directory 驗證批次服務解決方案](batch-aad-auth.md)。</span><span class="sxs-lookup"><span data-stu-id="d69c6-162">tooauthenticate Batch service applications using Azure AD, see [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span></span> 


[aad_about]: ../active-directory/active-directory-whatis.md "什麼是 Azure Active Directory？"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD 的驗證案例"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "整合應用程式與 Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
