---
title: "使用 Azure Active Directory 驗證 Azure Batch 服務解決方案 | Microsoft Docs"
description: "Batch 支援 Azure AD 從 Batch 服務進行驗證。"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/20/2017
ms.author: tamram
ms.openlocfilehash: 9c03bde919c46cd301229255c0b12ee69dda6f78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a><span data-ttu-id="824f1-103">使用 Active Directory 驗證 Batch 服務解決方案</span><span class="sxs-lookup"><span data-stu-id="824f1-103">Authenticate Batch service solutions with Active Directory</span></span>

<span data-ttu-id="824f1-104">Azure Batch 支援使用 [Azure Active Directory][aad_about] (Azure AD)進行驗證。</span><span class="sxs-lookup"><span data-stu-id="824f1-104">Azure Batch supports authentication with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="824f1-105">Azure AD 是 Microsoft 的多租用戶雲端型目錄和身分識別管理服務。</span><span class="sxs-lookup"><span data-stu-id="824f1-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="824f1-106">Azure 本身會使用 Azure AD 來驗證其客戶、服務管理員和組織的使用者。</span><span class="sxs-lookup"><span data-stu-id="824f1-106">Azure itself uses Azure AD to authenticate its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="824f1-107">搭配 Azure Batch 使用 Azure AD 驗證時，您可以使用下列其中一種方式進行驗證：</span><span class="sxs-lookup"><span data-stu-id="824f1-107">When using Azure AD authentication with Azure Batch, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="824f1-108">使用**整合式驗證**來驗證與應用程式互動的使用者。</span><span class="sxs-lookup"><span data-stu-id="824f1-108">By using **integrated authentication** to authenticate a user that is interacting with the application.</span></span> <span data-ttu-id="824f1-109">使用整合式驗證的應用程式會蒐集使用者的認證，並使用這些認證來驗證對 Batch 資源的存取。</span><span class="sxs-lookup"><span data-stu-id="824f1-109">An application using integrated authentication gathers a user's credentials and uses those credentials to authenticate access to Batch resources.</span></span>
- <span data-ttu-id="824f1-110">使用**服務主體**來驗證自動執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="824f1-110">By using a **service principal** to authenticate an unattended application.</span></span> <span data-ttu-id="824f1-111">服務主體會定義應用程式的原則和權限，以便在執行階段存取資源時代表應用程式。</span><span class="sxs-lookup"><span data-stu-id="824f1-111">A service principal defines the policy and permissions for an application in order to represent the application when accessing resources at runtime.</span></span>

<span data-ttu-id="824f1-112">若要深入了解 Azure AD，請參閱 [Azure Active Directory 文件](https://docs.microsoft.com/azure/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="824f1-112">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span>

## <a name="authentication-and-pool-allocation-mode"></a><span data-ttu-id="824f1-113">驗證和集區配置模式</span><span class="sxs-lookup"><span data-stu-id="824f1-113">Authentication and pool allocation mode</span></span>

<span data-ttu-id="824f1-114">當您建立 Batch 帳戶時，可以指定應配置為該帳戶所建立之集區的位置。</span><span class="sxs-lookup"><span data-stu-id="824f1-114">When you create a Batch account, you can specify where pools created for that account should be allocated.</span></span> <span data-ttu-id="824f1-115">您可以選擇在預設的 Batch 服務訂用帳戶或使用者訂用帳戶中配置集區。</span><span class="sxs-lookup"><span data-stu-id="824f1-115">You can choose to allocate pools either in the default Batch service subscription or in a user subscription.</span></span> <span data-ttu-id="824f1-116">您的選擇會影響如何在該帳戶中驗證對資源之存取的方式。</span><span class="sxs-lookup"><span data-stu-id="824f1-116">Your choice affects how you authenticate access to resources in that account.</span></span>

- <span data-ttu-id="824f1-117">**Batch 服務訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="824f1-117">**Batch service subscription**.</span></span> <span data-ttu-id="824f1-118">根據預設，Batch 集區會在 Batch 服務訂用帳戶中配置。</span><span class="sxs-lookup"><span data-stu-id="824f1-118">By default, Batch pools are allocated in a Batch service subscription.</span></span> <span data-ttu-id="824f1-119">如果您選擇此選項，就可以使用[共用金鑰](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service)或使用 Azure AD 來驗證該帳戶中對資源的存取。</span><span class="sxs-lookup"><span data-stu-id="824f1-119">If you choose this option, you can authenticate access to resources in that account either with [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) or with Azure AD.</span></span>
- <span data-ttu-id="824f1-120">**使用者訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="824f1-120">**User subscription.**</span></span> <span data-ttu-id="824f1-121">您可以選擇在指定的使用者訂用帳戶中配置 Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="824f1-121">You can choose to allocate Batch pools in a user subscription that you specify.</span></span> <span data-ttu-id="824f1-122">如果您選擇此選項，必須向 Azure AD 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="824f1-122">If you choose this option, you must authenticate with Azure AD.</span></span>

## <a name="endpoints-for-authentication"></a><span data-ttu-id="824f1-123">用於驗證的端點</span><span class="sxs-lookup"><span data-stu-id="824f1-123">Endpoints for authentication</span></span>

<span data-ttu-id="824f1-124">若要使用 Azure AD 驗證 Batch 應用程式，您需要在程式碼中包含一些已知的端點。</span><span class="sxs-lookup"><span data-stu-id="824f1-124">To authenticate Batch applications with Azure AD, you need to include some well-known endpoints in your code.</span></span>

### <a name="azure-ad-endpoint"></a><span data-ttu-id="824f1-125">Azure AD 端點</span><span class="sxs-lookup"><span data-stu-id="824f1-125">Azure AD endpoint</span></span>

<span data-ttu-id="824f1-126">基底 Azure AD 授權端點為：</span><span class="sxs-lookup"><span data-stu-id="824f1-126">The base Azure AD authority endpoint is:</span></span>

`https://login.microsoftonline.com/`

<span data-ttu-id="824f1-127">若要使用 Azure AD 進行驗證，您可以同時使用此端點及租用戶識別碼 (目錄識別碼)。</span><span class="sxs-lookup"><span data-stu-id="824f1-127">To authenticate with Azure AD, you use this endpoint together with the tenant ID (directory ID).</span></span> <span data-ttu-id="824f1-128">租用戶識別碼會識別要用來驗證的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="824f1-128">The tenant ID identifies the Azure AD tenant to use for authentication.</span></span> <span data-ttu-id="824f1-129">若要擷取租用戶識別碼，請依照[取得 Azure Active Directory 的租用戶識別碼](#get-the-tenant-id-for-your-active-directory)所述的步驟執行：</span><span class="sxs-lookup"><span data-stu-id="824f1-129">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> <span data-ttu-id="824f1-130">當您使用服務主體進行驗證時，租用戶特定的端點是必要的。</span><span class="sxs-lookup"><span data-stu-id="824f1-130">The tenant-specific endpoint is required when you authenticate using a service principal.</span></span> 
> 
> <span data-ttu-id="824f1-131">當您使用整合式驗證進行驗證時，租用戶特定的端點是選擇性的，但建議使用。</span><span class="sxs-lookup"><span data-stu-id="824f1-131">The tenant-specific endpoint is optional when you authenticate using integrated authentication, but recommended.</span></span> <span data-ttu-id="824f1-132">不過，您也可以使用 Azure AD 的通用端點。</span><span class="sxs-lookup"><span data-stu-id="824f1-132">However, you can also use the Azure AD common endpoint.</span></span> <span data-ttu-id="824f1-133">若未提供特定的租用戶，通用端點會提供一般認證蒐集介面。</span><span class="sxs-lookup"><span data-stu-id="824f1-133">The common endpoint provides a generic credential gathering interface when a specific tenant is not provided.</span></span> <span data-ttu-id="824f1-134">通用端點為 `https://login.microsoftonline.com/common`。</span><span class="sxs-lookup"><span data-stu-id="824f1-134">The common endpoint is `https://login.microsoftonline.com/common`.</span></span>
>
>

<span data-ttu-id="824f1-135">如需 Azure AD 端點的詳細資訊，請參閱 [Azure AD 的驗證案例][aad_auth_scenarios]。</span><span class="sxs-lookup"><span data-stu-id="824f1-135">For more information about Azure AD endpoints, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>

### <a name="batch-resource-endpoint"></a><span data-ttu-id="824f1-136">Batch 資源端點</span><span class="sxs-lookup"><span data-stu-id="824f1-136">Batch resource endpoint</span></span>

<span data-ttu-id="824f1-137">使用 **Azure Batch 資源端點**來取得權杖，以驗證對 Batch 服務的要求：</span><span class="sxs-lookup"><span data-stu-id="824f1-137">Use the **Azure Batch resource endpoint** to acquire a token for authenticating requests to the Batch service:</span></span>

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a><span data-ttu-id="824f1-138">向租用戶註冊您的應用程式</span><span class="sxs-lookup"><span data-stu-id="824f1-138">Register your application with a tenant</span></span>

<span data-ttu-id="824f1-139">使用 Azure AD 進行驗證的第一個步驟是在 Azure AD 租用戶中註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="824f1-139">The first step in using Azure AD to authenticate is registering your application in an Azure AD tenant.</span></span> <span data-ttu-id="824f1-140">註冊您的應用程式，可讓您從程式碼中呼叫 Azure [Active Directory Authentication Library] [aad_adal] (ADAL)。</span><span class="sxs-lookup"><span data-stu-id="824f1-140">Registering your application enables you to call the Azure [Active Directory Authentication Library][aad_adal] (ADAL) from your code.</span></span> <span data-ttu-id="824f1-141">ADAL 提供 API，從您的應用程式使用 Azure AD 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="824f1-141">The ADAL provides an API for authenticating with Azure AD from your application.</span></span> <span data-ttu-id="824f1-142">不論您是否計劃使用整合式驗證或服務主體，都需要註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="824f1-142">Registering your application is required whether you plan to use integrated authentication or a service principal.</span></span>

<span data-ttu-id="824f1-143">當您註冊應用程式時，會向 Azure AD 提供應用程式的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="824f1-143">When you register your application, you supply information about your application to Azure AD.</span></span> <span data-ttu-id="824f1-144">Azure AD 接著會提供您在執行階段用來將應用程式與 Azure AD 產生關聯的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="824f1-144">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span></span> <span data-ttu-id="824f1-145">若要深入了解應用程式識別碼，請參閱[Azure Active Directory 中的應用程式物件和服務主體物件之間的關聯性討論](../active-directory/develop/active-directory-application-objects.md)。</span><span class="sxs-lookup"><span data-stu-id="824f1-145">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="824f1-146">若要註冊 Batch 應用程式，遵循[整合應用程式與 Azure Active Directory][aad_integrate] 之[新增應用程式](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application)一節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="824f1-146">To register your Batch application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="824f1-147">如果您將應用程式註冊為原生應用程式，就能為**重新導向 URI** 指定任何有效的 URI。</span><span class="sxs-lookup"><span data-stu-id="824f1-147">If you register your application as a Native Application, you can specify any valid URI for the **Redirect URI**.</span></span> <span data-ttu-id="824f1-148">它不需要是實際的端點。</span><span class="sxs-lookup"><span data-stu-id="824f1-148">It does not need to be a real endpoint.</span></span>

<span data-ttu-id="824f1-149">註冊應用程式之後，您將會看到應用程式識別碼：</span><span class="sxs-lookup"><span data-stu-id="824f1-149">After you've registered your application, you'll see the application ID:</span></span>

![向 Azure AD 註冊您的 Batch 應用程式](./media/batch-aad-auth/app-registration-data-plane.png)

<span data-ttu-id="824f1-151">如需向 Azure AD 註冊應用程式的詳細資訊，請參閱 [Azure AD 的驗證案例](../active-directory/develop/active-directory-authentication-scenarios.md)。</span><span class="sxs-lookup"><span data-stu-id="824f1-151">For more information about registering an application with Azure AD, see [Authentication Scenarios for Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span></span>

## <a name="get-the-tenant-id-for-your-active-directory"></a><span data-ttu-id="824f1-152">取得 Active Directory 的租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="824f1-152">Get the tenant ID for your Active Directory</span></span>

<span data-ttu-id="824f1-153">租用戶識別碼會識別可為您的應用程式提供驗證服務的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="824f1-153">The tenant ID identifies the Azure AD tenant that provides authentication services to your application.</span></span> <span data-ttu-id="824f1-154">若要取得租用戶識別碼，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="824f1-154">To get the tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="824f1-155">在 Azure 入口網站中，選取您的 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="824f1-155">In the Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="824f1-156">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="824f1-156">Click **Properties**.</span></span>
3. <span data-ttu-id="824f1-157">複製針對目錄識別碼提供的 GUID 值。</span><span class="sxs-lookup"><span data-stu-id="824f1-157">Copy the GUID value provided for the directory ID.</span></span> <span data-ttu-id="824f1-158">此值也稱為租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="824f1-158">This value is also called the tenant ID.</span></span>

![複製目錄識別碼](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a><span data-ttu-id="824f1-160">使用整合式驗證</span><span class="sxs-lookup"><span data-stu-id="824f1-160">Use integrated authentication</span></span>

<span data-ttu-id="824f1-161">若要使用整合式驗證進行驗證，您需要為應用程式授與權限，以連接到 Batch 服務 API。</span><span class="sxs-lookup"><span data-stu-id="824f1-161">To authenticate with integrated authentication, you need to grant your application permissions to connect to the Batch service API.</span></span> <span data-ttu-id="824f1-162">此步驟可讓您的應用程式使用 Azure AD 來驗證與對 Batch 服務 API 的呼叫。</span><span class="sxs-lookup"><span data-stu-id="824f1-162">This step enables your application to authenticate calls to the Batch service API with Azure AD.</span></span>

<span data-ttu-id="824f1-163">一旦[註冊您的應用程式](#register-your-application-with-an-azure-ad-tenant)之後，請在 Azure 入口網站中遵循下列步驟，以授與它存取 Batch 服務的權限：</span><span class="sxs-lookup"><span data-stu-id="824f1-163">Once you've [registered your application](#register-your-application-with-an-azure-ad-tenant), follow these steps in the Azure portal to grant it access to the Batch service:</span></span>

1. <span data-ttu-id="824f1-164">在 Azure 入口網站的左側瀏覽窗格中，選擇 [更多服務]，按一下 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="824f1-164">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="824f1-165">在應用程式註冊清單中搜尋您應用程式的名稱︰</span><span class="sxs-lookup"><span data-stu-id="824f1-165">Search for the name of your application in the list of app registrations:</span></span>

    ![搜尋您的應用程式名稱](./media/batch-aad-auth/search-app-registration.png)

3. <span data-ttu-id="824f1-167">開啟應用程式的 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="824f1-167">Open the **Settings** blade for your application.</span></span> <span data-ttu-id="824f1-168">在 [API 存取] 區段中，選取 [必要權限]。</span><span class="sxs-lookup"><span data-stu-id="824f1-168">In the **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="824f1-169">在 [必要權限] 刀鋒視窗中，按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="824f1-169">In the **Required permissions** blade, click the **Add** button.</span></span>
5. <span data-ttu-id="824f1-170">在步驟 1 中，搜尋 Batch API。</span><span class="sxs-lookup"><span data-stu-id="824f1-170">In step 1, search for the Batch API.</span></span> <span data-ttu-id="824f1-171">搜尋這些字串，直到您找到 API 為止：</span><span class="sxs-lookup"><span data-stu-id="824f1-171">Search for each of these strings until you find the API:</span></span>
    1. <span data-ttu-id="824f1-172">**MicrosoftAzureBatch**。</span><span class="sxs-lookup"><span data-stu-id="824f1-172">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="824f1-173">**Microsoft Azure Batch**。</span><span class="sxs-lookup"><span data-stu-id="824f1-173">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="824f1-174">較新的 Azure AD 租用戶可以使用這個名稱。</span><span class="sxs-lookup"><span data-stu-id="824f1-174">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="824f1-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** 是 Batch API 的識別碼。</span><span class="sxs-lookup"><span data-stu-id="824f1-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** is the ID for the Batch API.</span></span> 
6. <span data-ttu-id="824f1-176">一旦您找到 Batch API，請選取它，然後按一下 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="824f1-176">Once you find the Batch API, select it and click the **Select** button.</span></span>
6. <span data-ttu-id="824f1-177">在步驟 2 中，選取 [存取 Azure Batch 服務] 旁的核取方塊，然後按一下 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="824f1-177">In step 2, select the check box next to **Access Azure Batch Service** and click the **Select** button.</span></span>
7. <span data-ttu-id="824f1-178">按一下 [完成] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="824f1-178">Click the **Done** button.</span></span>

<span data-ttu-id="824f1-179">[必要權限] 刀鋒視窗現在會顯示您的 Azure AD 應用程式具備 ADAL 與 Batch 服務 API 的存取權限。</span><span class="sxs-lookup"><span data-stu-id="824f1-179">The **Required Permissions** blade now shows that your Azure AD application has access to both ADAL and the Batch service API.</span></span> <span data-ttu-id="824f1-180">當您第一次向 Azure AD 註冊應用程式時，會自動將權限授與 ADAL。</span><span class="sxs-lookup"><span data-stu-id="824f1-180">Permissions are granted to ADAL automatically when you first register your app with Azure AD.</span></span>

![授與 API 權限](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a><span data-ttu-id="824f1-182">使用服務主體</span><span class="sxs-lookup"><span data-stu-id="824f1-182">Use a service principal</span></span> 

<span data-ttu-id="824f1-183">若要驗證自動執行的應用程式，您可以使用服務主體。</span><span class="sxs-lookup"><span data-stu-id="824f1-183">To authenticate an application that runs unattended, you use a service principal.</span></span> <span data-ttu-id="824f1-184">註冊您的應用程式之後，請在 Azure 入口網站中遵循下列步驟來設定服務主體：</span><span class="sxs-lookup"><span data-stu-id="824f1-184">After you've registered your application, follow these steps in the Azure portal to configure a service principal:</span></span>

1. <span data-ttu-id="824f1-185">要求應用程式的祕密金鑰。</span><span class="sxs-lookup"><span data-stu-id="824f1-185">Request a secret key for your application.</span></span>
2. <span data-ttu-id="824f1-186">將 RBAC 角色指派給應用程式。</span><span class="sxs-lookup"><span data-stu-id="824f1-186">Assign an RBAC role to your application.</span></span>

### <a name="request-a-secret-key-for-your-application"></a><span data-ttu-id="824f1-187">要求應用程式的祕密金鑰</span><span class="sxs-lookup"><span data-stu-id="824f1-187">Request a secret key for your application</span></span>

<span data-ttu-id="824f1-188">當您的應用程式使用服務主體進行驗證時，它會同時將應用程式識別碼和祕密金鑰傳送到 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="824f1-188">When your application authenticates with a service principal, it sends both the application ID and a secret key to Azure AD.</span></span> <span data-ttu-id="824f1-189">您必須建立並複製祕密金鑰，以便從程式碼中使用。</span><span class="sxs-lookup"><span data-stu-id="824f1-189">You'll need to create and copy the secret key to use from your code.</span></span>

<span data-ttu-id="824f1-190">在 Azure 入口網站中遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="824f1-190">Follow these steps in the Azure portal:</span></span>

1. <span data-ttu-id="824f1-191">在 Azure 入口網站的左側瀏覽窗格中，選擇 [更多服務]，按一下 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="824f1-191">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="824f1-192">在應用程式註冊清單中搜尋您應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="824f1-192">Search for the name of your application in the list of app registrations.</span></span>
3. <span data-ttu-id="824f1-193">顯示 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="824f1-193">Display the **Settings** blade.</span></span> <span data-ttu-id="824f1-194">在 [API 存取] 區段中，選取 [金鑰]。</span><span class="sxs-lookup"><span data-stu-id="824f1-194">In the **API Access** section, select **Keys**.</span></span>
4. <span data-ttu-id="824f1-195">若要建立金鑰，請輸入金鑰的描述。</span><span class="sxs-lookup"><span data-stu-id="824f1-195">To create a key, enter a description for the key.</span></span> <span data-ttu-id="824f1-196">接著選取一或兩年的金鑰持續期間。</span><span class="sxs-lookup"><span data-stu-id="824f1-196">Then select a duration for the key of either one or two years.</span></span> 
5. <span data-ttu-id="824f1-197">按一下 [儲存] 按鈕以建立並顯示金鑰。</span><span class="sxs-lookup"><span data-stu-id="824f1-197">Click the **Save** button to create and display the key.</span></span> <span data-ttu-id="824f1-198">將金鑰值複製到安全的地方，因為當您離開此刀鋒視窗之後，再也無法存取它。</span><span class="sxs-lookup"><span data-stu-id="824f1-198">Copy the key value to a safe place, as you won't be able to access it again after you leave the blade.</span></span> 

    ![建立祕密金鑰](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-to-your-application"></a><span data-ttu-id="824f1-200">將 RBAC 角色指派給應用程式</span><span class="sxs-lookup"><span data-stu-id="824f1-200">Assign an RBAC role to your application</span></span>

<span data-ttu-id="824f1-201">若要使用服務主體進行驗證，您需要將 RBAC 角色指派給應用程式。</span><span class="sxs-lookup"><span data-stu-id="824f1-201">To authenticate with a service principal, you need to assign an RBAC role to your application.</span></span> <span data-ttu-id="824f1-202">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="824f1-202">Follow these steps:</span></span>

1. <span data-ttu-id="824f1-203">在 Azure 入口網站中，瀏覽至應用程式所使用的 Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="824f1-203">In the Azure portal, navigate to the Batch account used by your application.</span></span>
2. <span data-ttu-id="824f1-204">在 Batch 帳戶的 [設定] 刀鋒視窗中，選取 [存取控制 (IAM)]。</span><span class="sxs-lookup"><span data-stu-id="824f1-204">In the **Settings** blade for the Batch account, select **Access Control (IAM)**.</span></span>
3. <span data-ttu-id="824f1-205">按一下 [新增]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="824f1-205">Click the **Add** button.</span></span> 
4. <span data-ttu-id="824f1-206">從 [角色] 下拉式清單中，選擇應用程式的 [參與者] 或 [讀者] 角色。</span><span class="sxs-lookup"><span data-stu-id="824f1-206">From the **Role** drop-down, choose either the _Contributor_ or _Reader_ role for your application.</span></span> <span data-ttu-id="824f1-207">如需這些角色的詳細資訊，請參閱[在 Azure 入口網站中開始使用角色型存取控制](../active-directory/role-based-access-control-what-is.md)。</span><span class="sxs-lookup"><span data-stu-id="824f1-207">For more information on these roles, see [Get started with Role-Based Access Control in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>  
5. <span data-ttu-id="824f1-208">在 [選取] 欄位中，輸入應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="824f1-208">In the **Select** field, enter the name of your application.</span></span> <span data-ttu-id="824f1-209">從清單中選取您的應用程式，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="824f1-209">Select your application from the list, and click **Save**.</span></span>

<span data-ttu-id="824f1-210">您的應用程式現在應該會以您指派的 RBAC 角色，出現在您的存取控制設定中。</span><span class="sxs-lookup"><span data-stu-id="824f1-210">Your application should now appear in your access control settings with an RBAC role assigned.</span></span> 

![將 RBAC 角色指派給應用程式](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-the-tenant-id-for-your-azure-active-directory"></a><span data-ttu-id="824f1-212">取得 Azure Active Directory 的租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="824f1-212">Get the tenant ID for your Azure Active Directory</span></span>

<span data-ttu-id="824f1-213">租用戶識別碼會識別可為您的應用程式提供驗證服務的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="824f1-213">The tenant ID identifies the Azure AD tenant that provides authentication services to your application.</span></span> <span data-ttu-id="824f1-214">若要取得租用戶識別碼，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="824f1-214">To get the tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="824f1-215">在 Azure 入口網站中，選取您的 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="824f1-215">In the Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="824f1-216">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="824f1-216">Click **Properties**.</span></span>
3. <span data-ttu-id="824f1-217">複製針對目錄識別碼提供的 GUID 值。</span><span class="sxs-lookup"><span data-stu-id="824f1-217">Copy the GUID value provided for the directory ID.</span></span> <span data-ttu-id="824f1-218">此值也稱為租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="824f1-218">This value is also called the tenant ID.</span></span>

![複製目錄識別碼](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a><span data-ttu-id="824f1-220">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="824f1-220">Code examples</span></span>

<span data-ttu-id="824f1-221">本節中的程式碼範例示範如何使用整合式驗證搭配 Azure AD 進行驗證，以及使用服務主體進行驗證。</span><span class="sxs-lookup"><span data-stu-id="824f1-221">The code examples in this section show how to authenticate with Azure AD using integrated authentication and with a service principal.</span></span> <span data-ttu-id="824f1-222">這些程式碼範例會使用 .NET，但概念類似其他語言。</span><span class="sxs-lookup"><span data-stu-id="824f1-222">These code examples use .NET, but the concepts are similar for other languages.</span></span>

> [!NOTE]
> <span data-ttu-id="824f1-223">Azure AD 驗證權杖會在一小時後過期。</span><span class="sxs-lookup"><span data-stu-id="824f1-223">An Azure AD authentication token expires after one hour.</span></span> <span data-ttu-id="824f1-224">使用長時間執行 **BatchClient** 物件時，我們建議您在每個要求從 ADAL 擷取權杖，以確保您一律擁有有效的權杖。</span><span class="sxs-lookup"><span data-stu-id="824f1-224">When using a long-lived **BatchClient** object, we recommend that you retrieve a token from ADAL on every request to ensure you always have a valid token.</span></span> 
>
>
> <span data-ttu-id="824f1-225">若要在 .NET 中達到此目的，撰寫可從 Azure AD 中擷取權杖的方法，並傳遞該方法至 **BatchTokenCredentials** 物件做為委派。</span><span class="sxs-lookup"><span data-stu-id="824f1-225">To achieve this in .NET, write a method that retrieves the token from Azure AD and pass that method to a **BatchTokenCredentials** object as a delegate.</span></span> <span data-ttu-id="824f1-226">每個要求都會對 Batch 服務呼叫委派方法，以確保已提供有效的權杖。</span><span class="sxs-lookup"><span data-stu-id="824f1-226">The delegate method is called on every request to the Batch service to ensure that a valid token is provided.</span></span> <span data-ttu-id="824f1-227">根據預設，ADAL 會快取權杖，因此只在必要時才會從 Azure AD 擷取新的權杖。</span><span class="sxs-lookup"><span data-stu-id="824f1-227">By default ADAL caches tokens, so a new token is retrieved from Azure AD only when necessary.</span></span> <span data-ttu-id="824f1-228">如需關於 Azure AD 中的權杖資訊，請參閱 [Azure AD 的驗證案例][aad_auth_scenarios]。</span><span class="sxs-lookup"><span data-stu-id="824f1-228">For more information about tokens in Azure AD, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a><span data-ttu-id="824f1-229">程式碼範例︰搭配 Batch .NET 使用 Azure AD 整合式驗證</span><span class="sxs-lookup"><span data-stu-id="824f1-229">Code example: Using Azure AD integrated authentication with Batch .NET</span></span>

<span data-ttu-id="824f1-230">若要從 Batch .NET 使用整合式驗證進行驗證，請參考 [Azure Batch .NET (英文)](https://www.nuget.org/packages/Azure.Batch/) 封裝和 [ADAL (英文)](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) 封裝。</span><span class="sxs-lookup"><span data-stu-id="824f1-230">To authenticate with integrated authentication from Batch .NET, reference the [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and the [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="824f1-231">在您的程式碼中，包括下列 `using` 陳述式︰</span><span class="sxs-lookup"><span data-stu-id="824f1-231">Include the following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="824f1-232">在您的程式碼中參考 Azure AD 端點，包括租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="824f1-232">Reference the Azure AD endpoint in your code, including the tenant ID.</span></span> <span data-ttu-id="824f1-233">若要擷取租用戶識別碼，請依照[取得 Azure Active Directory 的租用戶識別碼](#get-the-tenant-id-for-your-active-directory)所述的步驟執行：</span><span class="sxs-lookup"><span data-stu-id="824f1-233">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="824f1-234">參考 Batch 服務資源端點：</span><span class="sxs-lookup"><span data-stu-id="824f1-234">Reference the Batch service resource endpoint:</span></span>

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="824f1-235">參考您的 Batch 帳戶：</span><span class="sxs-lookup"><span data-stu-id="824f1-235">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="824f1-236">指定您應用程式的應用程式識別碼 (用戶端識別碼)。</span><span class="sxs-lookup"><span data-stu-id="824f1-236">Specify the application ID (client ID) for your application.</span></span> <span data-ttu-id="824f1-237">應用程式識別碼可在 Azure 入口網站中，從您的應用程式註冊取得：</span><span class="sxs-lookup"><span data-stu-id="824f1-237">The application ID is available from your app registration in the Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="824f1-238">同時，複製您在註冊程序期間指定的重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="824f1-238">Also copy the redirect URI that you specified during the registration process.</span></span> <span data-ttu-id="824f1-239">您程式碼中指定的重新導向 URI 必須符合您註冊應用程式時所提供的重新導向 URI：</span><span class="sxs-lookup"><span data-stu-id="824f1-239">The redirect URI specified in your code must match the redirect URI that you provided when you registered the application:</span></span>

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

<span data-ttu-id="824f1-240">撰寫回呼方法，以從 Azure AD 取得驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="824f1-240">Write a callback method to acquire the authentication token from Azure AD.</span></span> <span data-ttu-id="824f1-241">此處所示的 **GetAuthenticationTokenAsync** 回呼方法會呼叫 ADAL，來驗證與應用程式互動的使用者。</span><span class="sxs-lookup"><span data-stu-id="824f1-241">The **GetAuthenticationTokenAsync** callback method shown here calls ADAL to authenticate a user who is interacting with the application.</span></span> <span data-ttu-id="824f1-242">ADAL 所提供的 **AcquireTokenAsync** 方法會提示使用者輸入其認證，而應用程式會在使用者提供認證之後繼續進行 (除非它已經快取了認證)：</span><span class="sxs-lookup"><span data-stu-id="824f1-242">The **AcquireTokenAsync** method provided by ADAL prompts the user for their credentials, and the application proceeds once the user provides them (unless it has already cached credentials):</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire the authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

<span data-ttu-id="824f1-243">建構接受委派做為參數的 **BatchTokenCredentials** 物件。</span><span class="sxs-lookup"><span data-stu-id="824f1-243">Construct a **BatchTokenCredentials** object that takes the delegate as a parameter.</span></span> <span data-ttu-id="824f1-244">使用這些認證來開啟 **BatchClient** 物件。</span><span class="sxs-lookup"><span data-stu-id="824f1-244">Use those credentials to open a **BatchClient** object.</span></span> <span data-ttu-id="824f1-245">您可以針對 Batch 服務的後續作業使用該 **BatchClient** 物件：</span><span class="sxs-lookup"><span data-stu-id="824f1-245">You can use that **BatchClient** object for subsequent operations against the Batch service:</span></span>

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a><span data-ttu-id="824f1-246">程式碼範例︰搭配 Batch .NET 使用 Azure AD 服務主體</span><span class="sxs-lookup"><span data-stu-id="824f1-246">Code example: Using an Azure AD service principal with Batch .NET</span></span>

<span data-ttu-id="824f1-247">若要從 Batch .NET 使用服務主體進行驗證，請參考 [Azure Batch .NET (英文)](https://www.nuget.org/packages/Azure.Batch/) 封裝和 [ADAL (英文)](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) 封裝。</span><span class="sxs-lookup"><span data-stu-id="824f1-247">To authenticate with a service principal from Batch .NET, reference the [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and the [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="824f1-248">在您的程式碼中，包括下列 `using` 陳述式︰</span><span class="sxs-lookup"><span data-stu-id="824f1-248">Include the following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="824f1-249">在您的程式碼中參考 Azure AD 端點，包括租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="824f1-249">Reference the Azure AD endpoint in your code, including the tenant ID.</span></span> <span data-ttu-id="824f1-250">使用服務主體時，您必須提供租用戶特定的端點。</span><span class="sxs-lookup"><span data-stu-id="824f1-250">When using a service principal, you must provide a tenant-specific endpoint.</span></span> <span data-ttu-id="824f1-251">若要擷取租用戶識別碼，請依照[取得 Azure Active Directory 的租用戶識別碼](#get-the-tenant-id-for-your-active-directory)所述的步驟執行：</span><span class="sxs-lookup"><span data-stu-id="824f1-251">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="824f1-252">參考 Batch 服務資源端點：</span><span class="sxs-lookup"><span data-stu-id="824f1-252">Reference the Batch service resource endpoint:</span></span>  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="824f1-253">參考您的 Batch 帳戶：</span><span class="sxs-lookup"><span data-stu-id="824f1-253">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="824f1-254">指定您應用程式的應用程式識別碼 (用戶端識別碼)。</span><span class="sxs-lookup"><span data-stu-id="824f1-254">Specify the application ID (client ID) for your application.</span></span> <span data-ttu-id="824f1-255">應用程式識別碼可在 Azure 入口網站中，從您的應用程式註冊取得：</span><span class="sxs-lookup"><span data-stu-id="824f1-255">The application ID is available from your app registration in the Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="824f1-256">指定您從 Azure 入口網站中複製的祕密金鑰：</span><span class="sxs-lookup"><span data-stu-id="824f1-256">Specify the secret key that you copied from the Azure portal:</span></span>

```csharp
private const string ClientKey = "<secret-key>";
```

<span data-ttu-id="824f1-257">撰寫回呼方法，以從 Azure AD 取得驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="824f1-257">Write a callback method to acquire the authentication token from Azure AD.</span></span> <span data-ttu-id="824f1-258">此處所示的 **GetAuthenticationTokenAsync** 回呼方法會呼叫 ADAL 進行自動驗證：</span><span class="sxs-lookup"><span data-stu-id="824f1-258">The **GetAuthenticationTokenAsync** callback method shown here calls ADAL for unattended authentication:</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

<span data-ttu-id="824f1-259">建構接受委派做為參數的 **BatchTokenCredentials** 物件。</span><span class="sxs-lookup"><span data-stu-id="824f1-259">Construct a **BatchTokenCredentials** object that takes the delegate as a parameter.</span></span> <span data-ttu-id="824f1-260">使用這些認證來開啟 **BatchClient** 物件。</span><span class="sxs-lookup"><span data-stu-id="824f1-260">Use those credentials to open a **BatchClient** object.</span></span> <span data-ttu-id="824f1-261">接著，您可以針對 Batch 服務的後續作業使用該 **BatchClient** 物件：</span><span class="sxs-lookup"><span data-stu-id="824f1-261">You can then use that **BatchClient** object for subsequent operations against the Batch service:</span></span>

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="824f1-262">後續步驟</span><span class="sxs-lookup"><span data-stu-id="824f1-262">Next steps</span></span>

<span data-ttu-id="824f1-263">若要深入了解 Azure AD，請參閱 [Azure Active Directory 文件](https://docs.microsoft.com/azure/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="824f1-263">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="824f1-264">[Azure 程式碼範例](https://azure.microsoft.com/resources/samples/?service=active-directory)程式庫中有深入的範例示範如何使用 ADAL。</span><span class="sxs-lookup"><span data-stu-id="824f1-264">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="824f1-265">若要深入了解服務主體，請參閱 [Azure Active Directory 中的應用程式和服務主體物件](../active-directory/develop/active-directory-application-objects.md)。</span><span class="sxs-lookup"><span data-stu-id="824f1-265">To learn more about service principals, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span> <span data-ttu-id="824f1-266">若要使用 Azure 入口網站建立服務主體，請參閱[使用入口網站來建立可存取資源的 Active Directory 應用程式和服務主體](../resource-group-create-service-principal-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="824f1-266">To create a service principal using the Azure portal, see [Use portal to create Active Directory application and service principal that can access resources](../resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="824f1-267">您也可以使用 PowerShell 或 Azure CLI 來建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="824f1-267">You can also create a service principal with PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="824f1-268">若要使用 Azure AD 驗證 Batch Management 應用程式，請參閱[使用 Active Directory 驗證 Batch Management 解決方案](batch-aad-auth-management.md)。</span><span class="sxs-lookup"><span data-stu-id="824f1-268">To authenticate Batch Management applications using Azure AD, see [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span> 

<span data-ttu-id="824f1-269">[aad_about]: ../active-directory/active-directory-whatis.md "什麼是 Azure Active Directory？"</span><span class="sxs-lookup"><span data-stu-id="824f1-269">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="824f1-270">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD 的驗證案例"</span><span class="sxs-lookup"><span data-stu-id="824f1-270">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="824f1-271">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "整合應用程式與 Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="824f1-271">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
[azure_portal]: http://portal.azure.com
