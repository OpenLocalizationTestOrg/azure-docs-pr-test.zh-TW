---
title: "使用 Azure Active Directory 驗證 Batch Management 解決方案 | Microsoft Docs"
description: "使用 Azure Resource Manager 和 Batch 資源提供者建置的應用程式會使用 Azure AD 進行驗證。"
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
ms.openlocfilehash: 26d4adf4f74f9aacc4cf8cf24be293ebdb4d63c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a><span data-ttu-id="d3532-103">使用 Active Directory 驗證 Batch Management 解決方案</span><span class="sxs-lookup"><span data-stu-id="d3532-103">Authenticate Batch Management solutions with Active Directory</span></span>

<span data-ttu-id="d3532-104">呼叫 Azure Batch Management 服務的應用程式會使用 [Azure Active Directory][aad_about] (Azure AD) 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="d3532-104">Applications that call the Azure Batch Management service authenticate with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="d3532-105">Azure AD 是 Microsoft 的多租用戶雲端型目錄和身分識別管理服務。</span><span class="sxs-lookup"><span data-stu-id="d3532-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="d3532-106">Azure 本身會使用 Azure AD 來驗證其客戶、服務管理員和組織的使用者。</span><span class="sxs-lookup"><span data-stu-id="d3532-106">Azure itself uses Azure AD for the authentication of its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="d3532-107">Batch 管理 .NET 程式庫會公開使用 Batch 帳戶、帳戶金鑰、應用程式和應用程式封裝的類型。</span><span class="sxs-lookup"><span data-stu-id="d3532-107">The Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span></span> <span data-ttu-id="d3532-108">Batch Management .NET 程式庫是 Azure 資源提供者用戶端，並與 [Azure Resource Manager][resman_overview] 搭配使用，以程式設計方式管理這些資源。</span><span class="sxs-lookup"><span data-stu-id="d3532-108">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage these resources programmatically.</span></span> <span data-ttu-id="d3532-109">驗證透過任何 Azure 資源提供者用戶端 (包括 Batch Management .NET 程式庫)，以及透過 [Azure Resource Manager][resman_overview] 所提出的要求時，都需要 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="d3532-109">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span>

<span data-ttu-id="d3532-110">在本文中，我們將探討從使用 Batch Management .NET 程式庫的應用程式，使用 Azure AD 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="d3532-110">In this article, we explore using Azure AD to authenticate from applications that use the Batch Management .NET library.</span></span> <span data-ttu-id="d3532-111">我們會示範如何利用整合式驗證，使用 Azure AD 來驗證訂用帳戶管理員或共同管理員。</span><span class="sxs-lookup"><span data-stu-id="d3532-111">We show how to use Azure AD to authenticate a subscription administrator or co-administrator, using integrated authentication.</span></span> <span data-ttu-id="d3532-112">我們會使用 GitHub 上提供的 [AccountManagment][acct_mgmt_sample] 範例專案，來逐步解說如何搭配使用 Azure AD 與 Batch Management .NET 程式庫。</span><span class="sxs-lookup"><span data-stu-id="d3532-112">We use the [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, to walk through using Azure AD with the Batch Management .NET library.</span></span>

<span data-ttu-id="d3532-113">若要深入了解使用 Batch 管理 .NET 程式庫和 AccountManagement 範例，請參閱[使用適用於 .NET 的 Batch 管理用戶端程式庫來管理 Batch 帳戶和配額](batch-management-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="d3532-113">To learn more about using the Batch Management .NET library and the AccountManagement sample, see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

## <a name="register-your-application-with-azure-ad"></a><span data-ttu-id="d3532-114">向 Azure AD 註冊您的應用程式</span><span class="sxs-lookup"><span data-stu-id="d3532-114">Register your application with Azure AD</span></span>

<span data-ttu-id="d3532-115">Azure [Active Directory Authentication Library][aad_adal] (ADAL) 為 Azure AD 提供程式設計介面以供您的應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="d3532-115">The Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface to Azure AD for use within your applications.</span></span> <span data-ttu-id="d3532-116">若要從您的應用程式呼叫 ADAL，您必須在 Azure AD 租用戶中註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d3532-116">To call ADAL from your application, you must register your application in an Azure AD tenant.</span></span> <span data-ttu-id="d3532-117">當您註冊應用程式時，要提供 Azure AD 有關您應用程式的資訊，包括 Azure AD 租用戶內的名稱。</span><span class="sxs-lookup"><span data-stu-id="d3532-117">When you register your application, you supply Azure AD with information about your application, including a name for it within the Azure AD tenant.</span></span> <span data-ttu-id="d3532-118">Azure AD 接著會提供您在執行階段用來將應用程式與 Azure AD 產生關聯的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="d3532-118">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span></span> <span data-ttu-id="d3532-119">若要深入了解應用程式識別碼，請參閱[Azure Active Directory 中的應用程式物件和服務主體物件之間的關聯性討論](../active-directory/develop/active-directory-application-objects.md)。</span><span class="sxs-lookup"><span data-stu-id="d3532-119">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="d3532-120">若要註冊 AccountManagement 範例應用程式，遵循[整合應用程式與 Azure Active Directory][aad_integrate] 之[新增應用程式](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application)一節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="d3532-120">To register the AccountManagement sample application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="d3532-121">指定 [原生用戶端應用程式] 作為應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="d3532-121">Specify **Native Client Application** for the type of application.</span></span> <span data-ttu-id="d3532-122">適用於**重新導向 URI** 的業界標準 OAuth 2.0 URI 是 `urn:ietf:wg:oauth:2.0:oob`。</span><span class="sxs-lookup"><span data-stu-id="d3532-122">The industry standard OAuth 2.0 URI for the **Redirect URI** is `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="d3532-123">不過，您可以針對**重新導向 URI** 指定任何有效的 URI (例如 `http://myaccountmanagementsample`)，因為它不需要是實際的端點：</span><span class="sxs-lookup"><span data-stu-id="d3532-123">However, you can specify any valid URI (such as `http://myaccountmanagementsample`) for the **Redirect URI**, as it does not need to be a real endpoint:</span></span>

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

<span data-ttu-id="d3532-124">完成註冊程序後，您會看到應用程式識別碼以及針對應用程式列出的物件 (服務主體) 識別碼。</span><span class="sxs-lookup"><span data-stu-id="d3532-124">Once you complete the registration process, you'll see the application ID and the object (service principal) ID listed for your application.</span></span>  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-the-azure-resource-manager-api-access-to-your-application"></a><span data-ttu-id="d3532-125">授與 Azure Resource Manager API 存取給您的應用程式</span><span class="sxs-lookup"><span data-stu-id="d3532-125">Grant the Azure Resource Manager API access to your application</span></span>

<span data-ttu-id="d3532-126">接下來，您必須將應用程式的存取委派給 Azure Resource Manager API。</span><span class="sxs-lookup"><span data-stu-id="d3532-126">Next, you'll need to delegate access to your application to the Azure Resource Manager API.</span></span> <span data-ttu-id="d3532-127">Resource Manager API 的 Azure AD 識別項是 **Windows Azure 服務管理 API**。</span><span class="sxs-lookup"><span data-stu-id="d3532-127">The Azure AD identifier for the Resource Manager API is **Windows Azure Service Management API**.</span></span>

<span data-ttu-id="d3532-128">在 Azure 入口網站中遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d3532-128">Follow these steps in the Azure portal:</span></span>

1. <span data-ttu-id="d3532-129">在 Azure 入口網站的左側導覽窗格中，選擇 [更多服務]，按一下 [應用程式註冊]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d3532-129">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
2. <span data-ttu-id="d3532-130">在應用程式註冊清單中搜尋您應用程式的名稱︰</span><span class="sxs-lookup"><span data-stu-id="d3532-130">Search for the name of your application in the list of app registrations:</span></span>

    ![搜尋您的應用程式名稱](./media/batch-aad-auth-management/search-app-registration.png)

3. <span data-ttu-id="d3532-132">顯示 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d3532-132">Display the **Settings** blade.</span></span> <span data-ttu-id="d3532-133">在 [API 存取] 區段中，選取 [必要權限]。</span><span class="sxs-lookup"><span data-stu-id="d3532-133">In the **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="d3532-134">按一下 [新增] 以新增必要權限。</span><span class="sxs-lookup"><span data-stu-id="d3532-134">Click **Add** to add a new required permission.</span></span> 
5. <span data-ttu-id="d3532-135">在步驟 1 中，輸入 **Windows Azure 服務管理 API**，從結果清單選取該 API，然後按一下 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d3532-135">In step 1, enter **Windows Azure Service Management API**, select that API from the list of results, and click the **Select** button.</span></span>
6. <span data-ttu-id="d3532-136">在步驟 2 中，選取**存取 Azure 傳統部署模型做為組織使用者**旁的核取方塊，然後按一下 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d3532-136">In step 2, select the check box next to **Access Azure classic deployment model as organization users**, and click the **Select** button.</span></span>
7. <span data-ttu-id="d3532-137">按一下 [完成] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d3532-137">Click the **Done** button.</span></span>

<span data-ttu-id="d3532-138">[必要權限] 刀鋒視窗現在會顯示已向 ADAL 和 Resource Manager API 授與您應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="d3532-138">The **Required Permissions** blade now shows that permissions to your application are granted to both the ADAL and Resource Manager APIs.</span></span> <span data-ttu-id="d3532-139">當您第一次向 Azure AD 註冊您的應用程式時，權限依預設會授與給 ADAL。</span><span class="sxs-lookup"><span data-stu-id="d3532-139">Permissions are granted to ADAL by default when you first register your app with Azure AD.</span></span>

![委派權限給 Azure Resource Manager API](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a><span data-ttu-id="d3532-141">Azure AD 端點</span><span class="sxs-lookup"><span data-stu-id="d3532-141">Azure AD endpoints</span></span>

<span data-ttu-id="d3532-142">若要使用 Azure AD 驗證您的 Batch Management 解決方案，需要兩個已知的端點。</span><span class="sxs-lookup"><span data-stu-id="d3532-142">To authenticate your Batch Management solutions with Azure AD, you'll need two well-known endpoints.</span></span>

- <span data-ttu-id="d3532-143">若未提供特定的租用戶，**Azure AD 通用端點**會提供一般認證蒐集介面，如同整合式驗證的情況：</span><span class="sxs-lookup"><span data-stu-id="d3532-143">The **Azure AD common endpoint** provides a generic credential gathering interface when a specific tenant is not provided, as in the case of integrated authentication:</span></span>

    `https://login.microsoftonline.com/common`

- <span data-ttu-id="d3532-144">**Azure Resource Manager 端點**可用來取得權杖，以驗證對 Batch Management 服務的要求：</span><span class="sxs-lookup"><span data-stu-id="d3532-144">The **Azure Resource Manager endpoint** is used to acquire a token for authenticating requests to the Batch management service:</span></span>

    `https://management.core.windows.net/`

<span data-ttu-id="d3532-145">AccountManagement 範例應用程式會定義這些端點的常數。</span><span class="sxs-lookup"><span data-stu-id="d3532-145">The AccountManagement sample application defines constants for these endpoints.</span></span> <span data-ttu-id="d3532-146">將這些常數保留不變︰</span><span class="sxs-lookup"><span data-stu-id="d3532-146">Leave these constants unchanged:</span></span>

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a><span data-ttu-id="d3532-147">參考您的應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="d3532-147">Reference your application ID</span></span> 

<span data-ttu-id="d3532-148">用戶端應用程式使用應用程式識別碼 (也稱為用戶端識別碼) 在執行階段存取 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="d3532-148">Your client application uses the application ID (also referred to as the client ID) to access Azure AD at runtime.</span></span> <span data-ttu-id="d3532-149">在 Azure 入口網站中註冊您的應用程式後，更新程式碼以使用 Azure AD 針對已註冊應用程式所提供的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="d3532-149">Once you've registered your application in the Azure portal, update your code to use the application ID provided by Azure AD for your registered application.</span></span> <span data-ttu-id="d3532-150">在 AccountManagement 範例應用程式中，從 Azure 入口網站將應用程式識別碼複製到適當的常數︰</span><span class="sxs-lookup"><span data-stu-id="d3532-150">In the AccountManagement sample application, copy your application ID from the Azure portal to the appropriate constant:</span></span>

```csharp
// Specify the unique identifier (the "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access the Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
<span data-ttu-id="d3532-151">同時，複製您在註冊程序期間指定的重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="d3532-151">Also copy the redirect URI that you specified during the registration process.</span></span> <span data-ttu-id="d3532-152">您程式碼中指定的重新導向 URI 必須符合您註冊應用程式時所提供的重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="d3532-152">The redirect URI specified in your code must match the redirect URI that you provided when you registered the application.</span></span>

```csharp
// The URI to which Azure AD will redirect in response to an OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need to be a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a><span data-ttu-id="d3532-153">取得 Azure AD 驗證權杖</span><span class="sxs-lookup"><span data-stu-id="d3532-153">Acquire an Azure AD authentication token</span></span>

<span data-ttu-id="d3532-154">在 Azure AD 租用戶中註冊 AccountManagement 範例，並使用您的值更新範例原始程式碼之後，範例就準備好使用 Azure AD 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="d3532-154">After you register the AccountManagement sample in the Azure AD tenant and update the sample source code with your values, the sample is ready to authenticate using Azure AD.</span></span> <span data-ttu-id="d3532-155">當您執行範例時，ADAL 會嘗試取得驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="d3532-155">When you run the sample, the ADAL attempts to acquire an authentication token.</span></span> <span data-ttu-id="d3532-156">在此步驟中，它會提示您輸入您的 Microsoft 認證︰</span><span class="sxs-lookup"><span data-stu-id="d3532-156">At this step, it prompts you for your Microsoft credentials:</span></span> 

```csharp
// Obtain an access token using the "common" AAD resource. This allows the application
// to query AAD for information that lies outside the application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

<span data-ttu-id="d3532-157">您提供認證之後，範例應用程式可以繼續發出已驗證要求給 Batch 管理服務。</span><span class="sxs-lookup"><span data-stu-id="d3532-157">After you provide your credentials, the sample application can proceed to issue authenticated requests to the Batch management service.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d3532-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d3532-158">Next steps</span></span>

<span data-ttu-id="d3532-159">如需執行 [AccountManagement 範例應用程式][acct_mgmt_sample]的相關資訊，請參閱[使用適用於 .NET 的 Batch 管理用戶端程式庫來管理 Batch 帳戶和配額](batch-management-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="d3532-159">For more information on running the [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

<span data-ttu-id="d3532-160">若要深入了解 Azure AD，請參閱 [Azure Active Directory 文件](https://docs.microsoft.com/azure/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="d3532-160">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="d3532-161">[Azure 程式碼範例](https://azure.microsoft.com/resources/samples/?service=active-directory)程式庫中有深入的範例示範如何使用 ADAL。</span><span class="sxs-lookup"><span data-stu-id="d3532-161">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="d3532-162">若要使用 Azure AD 驗證 Batch 服務應用程式，請參閱[使用 Active Directory 驗證 Batch 服務解決方案](batch-aad-auth.md)。</span><span class="sxs-lookup"><span data-stu-id="d3532-162">To authenticate Batch service applications using Azure AD, see [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span></span> 


<span data-ttu-id="d3532-163">[aad_about]: ../active-directory/active-directory-whatis.md "什麼是 Azure Active Directory？"</span><span class="sxs-lookup"><span data-stu-id="d3532-163">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="d3532-164">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD 的驗證案例"</span><span class="sxs-lookup"><span data-stu-id="d3532-164">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="d3532-165">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "整合應用程式與 Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="d3532-165">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
