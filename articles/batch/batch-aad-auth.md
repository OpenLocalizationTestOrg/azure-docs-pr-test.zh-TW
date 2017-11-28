---
title: "aaaUse Azure Active Directory tooauthenticate Azure Batch 服務解決方案 |Microsoft 文件"
description: "批次支援 Azure AD 的 hello 批次服務驗證。"
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
ms.openlocfilehash: 6c825c30f1c80bb059a797a2e78367e599acd109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a><span data-ttu-id="cefc5-103">使用 Active Directory 驗證 Batch 服務解決方案</span><span class="sxs-lookup"><span data-stu-id="cefc5-103">Authenticate Batch service solutions with Active Directory</span></span>

<span data-ttu-id="cefc5-104">Azure Batch 支援使用 [Azure Active Directory][aad_about] (Azure AD)進行驗證。</span><span class="sxs-lookup"><span data-stu-id="cefc5-104">Azure Batch supports authentication with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="cefc5-105">Azure AD 是 Microsoft 的多租用戶雲端型目錄和身分識別管理服務。</span><span class="sxs-lookup"><span data-stu-id="cefc5-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="cefc5-106">Azure 本身會使用 Azure AD tooauthenticate 其客戶、 服務管理員和組織使用者。</span><span class="sxs-lookup"><span data-stu-id="cefc5-106">Azure itself uses Azure AD tooauthenticate its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="cefc5-107">搭配 Azure Batch 使用 Azure AD 驗證時，您可以使用下列其中一種方式進行驗證：</span><span class="sxs-lookup"><span data-stu-id="cefc5-107">When using Azure AD authentication with Azure Batch, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="cefc5-108">使用**整合式的驗證**tooauthenticate hello 應用程式互動的使用者。</span><span class="sxs-lookup"><span data-stu-id="cefc5-108">By using **integrated authentication** tooauthenticate a user that is interacting with hello application.</span></span> <span data-ttu-id="cefc5-109">使用整合式的驗證的應用程式收集使用者的認證，並使用這些認證 tooauthenticate 存取 tooBatch 資源。</span><span class="sxs-lookup"><span data-stu-id="cefc5-109">An application using integrated authentication gathers a user's credentials and uses those credentials tooauthenticate access tooBatch resources.</span></span>
- <span data-ttu-id="cefc5-110">使用**服務主體**tooauthenticate 無人看管的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cefc5-110">By using a **service principal** tooauthenticate an unattended application.</span></span> <span data-ttu-id="cefc5-111">服務主體定義 hello 原則和應用程式的權限順序 toorepresent hello 應用程式中存取資源，在執行階段時。</span><span class="sxs-lookup"><span data-stu-id="cefc5-111">A service principal defines hello policy and permissions for an application in order toorepresent hello application when accessing resources at runtime.</span></span>

<span data-ttu-id="cefc5-112">toolearn 進一步了解 Azure AD，請參閱 hello [Azure Active Directory 文件](https://docs.microsoft.com/azure/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="cefc5-112">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span>

## <a name="authentication-and-pool-allocation-mode"></a><span data-ttu-id="cefc5-113">驗證和集區配置模式</span><span class="sxs-lookup"><span data-stu-id="cefc5-113">Authentication and pool allocation mode</span></span>

<span data-ttu-id="cefc5-114">當您建立 Batch 帳戶時，可以指定應配置為該帳戶所建立之集區的位置。</span><span class="sxs-lookup"><span data-stu-id="cefc5-114">When you create a Batch account, you can specify where pools created for that account should be allocated.</span></span> <span data-ttu-id="cefc5-115">在 hello 預設批次服務訂用帳戶或使用者訂用帳戶中，您可以選擇 tooallocate 集區。</span><span class="sxs-lookup"><span data-stu-id="cefc5-115">You can choose tooallocate pools either in hello default Batch service subscription or in a user subscription.</span></span> <span data-ttu-id="cefc5-116">您的選擇會影響您驗證該帳戶中的存取 tooresources 的方式。</span><span class="sxs-lookup"><span data-stu-id="cefc5-116">Your choice affects how you authenticate access tooresources in that account.</span></span>

- <span data-ttu-id="cefc5-117">**Batch 服務訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="cefc5-117">**Batch service subscription**.</span></span> <span data-ttu-id="cefc5-118">根據預設，Batch 集區會在 Batch 服務訂用帳戶中配置。</span><span class="sxs-lookup"><span data-stu-id="cefc5-118">By default, Batch pools are allocated in a Batch service subscription.</span></span> <span data-ttu-id="cefc5-119">如果您選擇此選項時，您可以驗證該帳戶中的存取 tooresources 不論是透過[共用金鑰](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service)或與 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="cefc5-119">If you choose this option, you can authenticate access tooresources in that account either with [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) or with Azure AD.</span></span>
- <span data-ttu-id="cefc5-120">**使用者訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="cefc5-120">**User subscription.**</span></span> <span data-ttu-id="cefc5-121">您可以選擇 tooallocate 批次集區，您指定的使用者訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="cefc5-121">You can choose tooallocate Batch pools in a user subscription that you specify.</span></span> <span data-ttu-id="cefc5-122">如果您選擇此選項，必須向 Azure AD 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="cefc5-122">If you choose this option, you must authenticate with Azure AD.</span></span>

## <a name="endpoints-for-authentication"></a><span data-ttu-id="cefc5-123">用於驗證的端點</span><span class="sxs-lookup"><span data-stu-id="cefc5-123">Endpoints for authentication</span></span>

<span data-ttu-id="cefc5-124">您需要 tooinclude tooauthenticate 批次應用程式與 Azure AD，您的程式碼在某些已知端點。</span><span class="sxs-lookup"><span data-stu-id="cefc5-124">tooauthenticate Batch applications with Azure AD, you need tooinclude some well-known endpoints in your code.</span></span>

### <a name="azure-ad-endpoint"></a><span data-ttu-id="cefc5-125">Azure AD 端點</span><span class="sxs-lookup"><span data-stu-id="cefc5-125">Azure AD endpoint</span></span>

<span data-ttu-id="cefc5-126">基底 hello Azure AD 授權端點：</span><span class="sxs-lookup"><span data-stu-id="cefc5-126">hello base Azure AD authority endpoint is:</span></span>

`https://login.microsoftonline.com/`

<span data-ttu-id="cefc5-127">tooauthenticate 與 Azure AD，您會使用這個端點以及 hello 租用戶識別碼 （目錄識別碼）。</span><span class="sxs-lookup"><span data-stu-id="cefc5-127">tooauthenticate with Azure AD, you use this endpoint together with hello tenant ID (directory ID).</span></span> <span data-ttu-id="cefc5-128">hello 租用戶識別碼會識別 hello Azure AD 租用戶 toouse 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="cefc5-128">hello tenant ID identifies hello Azure AD tenant toouse for authentication.</span></span> <span data-ttu-id="cefc5-129">tooretrieve hello 租用戶識別碼，請遵循所述的 hello 步驟[取得 Azure Active Directory 中的 hello 租用戶識別碼](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="cefc5-129">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> <span data-ttu-id="cefc5-130">當您使用服務主體進行驗證時需要 hello 租用戶專用端點。</span><span class="sxs-lookup"><span data-stu-id="cefc5-130">hello tenant-specific endpoint is required when you authenticate using a service principal.</span></span> 
> 
> <span data-ttu-id="cefc5-131">當您使用整合式的驗證進行驗證，但建議使用 hello 租用戶專用端點。</span><span class="sxs-lookup"><span data-stu-id="cefc5-131">hello tenant-specific endpoint is optional when you authenticate using integrated authentication, but recommended.</span></span> <span data-ttu-id="cefc5-132">不過，您也可以使用 hello Azure AD 通用端點。</span><span class="sxs-lookup"><span data-stu-id="cefc5-132">However, you can also use hello Azure AD common endpoint.</span></span> <span data-ttu-id="cefc5-133">hello 一般端點提供一般認證未提供特定租用戶時，收集介面。</span><span class="sxs-lookup"><span data-stu-id="cefc5-133">hello common endpoint provides a generic credential gathering interface when a specific tenant is not provided.</span></span> <span data-ttu-id="cefc5-134">hello 共同端點`https://login.microsoftonline.com/common`。</span><span class="sxs-lookup"><span data-stu-id="cefc5-134">hello common endpoint is `https://login.microsoftonline.com/common`.</span></span>
>
>

<span data-ttu-id="cefc5-135">如需 Azure AD 端點的詳細資訊，請參閱 [Azure AD 的驗證案例][aad_auth_scenarios]。</span><span class="sxs-lookup"><span data-stu-id="cefc5-135">For more information about Azure AD endpoints, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>

### <a name="batch-resource-endpoint"></a><span data-ttu-id="cefc5-136">Batch 資源端點</span><span class="sxs-lookup"><span data-stu-id="cefc5-136">Batch resource endpoint</span></span>

<span data-ttu-id="cefc5-137">使用 hello **Azure Batch 資源端點**tooacquire token 來驗證要求 toohello 批次服務：</span><span class="sxs-lookup"><span data-stu-id="cefc5-137">Use hello **Azure Batch resource endpoint** tooacquire a token for authenticating requests toohello Batch service:</span></span>

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a><span data-ttu-id="cefc5-138">向租用戶註冊您的應用程式</span><span class="sxs-lookup"><span data-stu-id="cefc5-138">Register your application with a tenant</span></span>

<span data-ttu-id="cefc5-139">hello 第一個步驟中使用 Azure AD tooauthenticate 在 Azure AD 租用戶註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cefc5-139">hello first step in using Azure AD tooauthenticate is registering your application in an Azure AD tenant.</span></span> <span data-ttu-id="cefc5-140">註冊您的應用程式可讓您 toocall hello Azure [Active Directory Authentication Library] [ aad_adal] (ADAL) 從程式碼。</span><span class="sxs-lookup"><span data-stu-id="cefc5-140">Registering your application enables you toocall hello Azure [Active Directory Authentication Library][aad_adal] (ADAL) from your code.</span></span> <span data-ttu-id="cefc5-141">hello ADAL 提供應用程式開發介面使用從您的應用程式的 Azure AD 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="cefc5-141">hello ADAL provides an API for authenticating with Azure AD from your application.</span></span> <span data-ttu-id="cefc5-142">不論您計劃 toouse 整合式的驗證或服務主體，註冊您的應用程式是必要。</span><span class="sxs-lookup"><span data-stu-id="cefc5-142">Registering your application is required whether you plan toouse integrated authentication or a service principal.</span></span>

<span data-ttu-id="cefc5-143">當您註冊您的應用程式時，您會提供有關您的應用程式 tooAzure AD 資訊。</span><span class="sxs-lookup"><span data-stu-id="cefc5-143">When you register your application, you supply information about your application tooAzure AD.</span></span> <span data-ttu-id="cefc5-144">然後 azure AD 提供應用程式識別碼，搭配 tooassociate 您的應用程式在執行階段的 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="cefc5-144">Azure AD then provides an application ID that you use tooassociate your application with Azure AD at runtime.</span></span> <span data-ttu-id="cefc5-145">toolearn 深入了解 hello 應用程式識別碼，請參閱[應用程式與 Azure Active Directory 中的服務主體物件](../active-directory/develop/active-directory-application-objects.md)。</span><span class="sxs-lookup"><span data-stu-id="cefc5-145">toolearn more about hello application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="cefc5-146">tooregister 批次應用程式中，遵循 hello 步驟在 hello[來新增應用程式](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application)一節中[整合應用程式與 Azure Active Directory][aad_integrate]。</span><span class="sxs-lookup"><span data-stu-id="cefc5-146">tooregister your Batch application, follow hello steps in hello [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="cefc5-147">如果您為原生應用程式註冊您的應用程式，您可以指定任何有效的 URI hello**重新導向 URI**。</span><span class="sxs-lookup"><span data-stu-id="cefc5-147">If you register your application as a Native Application, you can specify any valid URI for hello **Redirect URI**.</span></span> <span data-ttu-id="cefc5-148">不需要 toobe 實際的端點。</span><span class="sxs-lookup"><span data-stu-id="cefc5-148">It does not need toobe a real endpoint.</span></span>

<span data-ttu-id="cefc5-149">您已註冊您的應用程式之後，您會看到 hello 應用程式識別碼：</span><span class="sxs-lookup"><span data-stu-id="cefc5-149">After you've registered your application, you'll see hello application ID:</span></span>

![向 Azure AD 註冊您的 Batch 應用程式](./media/batch-aad-auth/app-registration-data-plane.png)

<span data-ttu-id="cefc5-151">如需向 Azure AD 註冊應用程式的詳細資訊，請參閱 [Azure AD 的驗證案例](../active-directory/develop/active-directory-authentication-scenarios.md)。</span><span class="sxs-lookup"><span data-stu-id="cefc5-151">For more information about registering an application with Azure AD, see [Authentication Scenarios for Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span></span>

## <a name="get-hello-tenant-id-for-your-active-directory"></a><span data-ttu-id="cefc5-152">取得您的 Active Directory 中的 hello 租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="cefc5-152">Get hello tenant ID for your Active Directory</span></span>

<span data-ttu-id="cefc5-153">hello 租用戶識別碼會識別 hello Azure AD 租用戶提供驗證服務 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cefc5-153">hello tenant ID identifies hello Azure AD tenant that provides authentication services tooyour application.</span></span> <span data-ttu-id="cefc5-154">tooget hello 租用戶識別碼，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cefc5-154">tooget hello tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="cefc5-155">在 hello Azure 入口網站，選取您的 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="cefc5-155">In hello Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="cefc5-156">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="cefc5-156">Click **Properties**.</span></span>
3. <span data-ttu-id="cefc5-157">複製 hello GUID 值提供給 hello 目錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="cefc5-157">Copy hello GUID value provided for hello directory ID.</span></span> <span data-ttu-id="cefc5-158">此值也稱為 hello 租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="cefc5-158">This value is also called hello tenant ID.</span></span>

![複製 hello 目錄識別碼](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a><span data-ttu-id="cefc5-160">使用整合式驗證</span><span class="sxs-lookup"><span data-stu-id="cefc5-160">Use integrated authentication</span></span>

<span data-ttu-id="cefc5-161">tooauthenticate 使用整合式驗證，您需要 toogrant 您應用程式的權限 tooconnect toohello 批次服務 API。</span><span class="sxs-lookup"><span data-stu-id="cefc5-161">tooauthenticate with integrated authentication, you need toogrant your application permissions tooconnect toohello Batch service API.</span></span> <span data-ttu-id="cefc5-162">這個步驟可讓您的應用程式 tooauthenticate 呼叫 toohello 批次服務 API 與 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="cefc5-162">This step enables your application tooauthenticate calls toohello Batch service API with Azure AD.</span></span>

<span data-ttu-id="cefc5-163">一旦您[註冊您的應用程式](#register-your-application-with-an-azure-ad-tenant)，請遵循下列步驟在 hello Azure 入口網站的 toogrant 它存取 toohello 批次服務：</span><span class="sxs-lookup"><span data-stu-id="cefc5-163">Once you've [registered your application](#register-your-application-with-an-azure-ad-tenant), follow these steps in hello Azure portal toogrant it access toohello Batch service:</span></span>

1. <span data-ttu-id="cefc5-164">在 hello 左側導覽窗格中的 hello Azure 入口網站，選擇 **更服務**，按一下**應用程式註冊**。</span><span class="sxs-lookup"><span data-stu-id="cefc5-164">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="cefc5-165">搜尋 hello hello 清單中的應用程式註冊您應用程式名稱：</span><span class="sxs-lookup"><span data-stu-id="cefc5-165">Search for hello name of your application in hello list of app registrations:</span></span>

    ![搜尋您的應用程式名稱](./media/batch-aad-auth/search-app-registration.png)

3. <span data-ttu-id="cefc5-167">開啟 hello**設定**刀鋒視窗，您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cefc5-167">Open hello **Settings** blade for your application.</span></span> <span data-ttu-id="cefc5-168">在 hello **API 存取**區段中，選取**必要的權限**。</span><span class="sxs-lookup"><span data-stu-id="cefc5-168">In hello **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="cefc5-169">在 [hello**必要的權限**刀鋒視窗中，按一下 hello**新增**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cefc5-169">In hello **Required permissions** blade, click hello **Add** button.</span></span>
5. <span data-ttu-id="cefc5-170">在步驟 1 中，搜尋 hello 批次 API。</span><span class="sxs-lookup"><span data-stu-id="cefc5-170">In step 1, search for hello Batch API.</span></span> <span data-ttu-id="cefc5-171">針對每個這些字串的搜尋，直到您找到 hello API:</span><span class="sxs-lookup"><span data-stu-id="cefc5-171">Search for each of these strings until you find hello API:</span></span>
    1. <span data-ttu-id="cefc5-172">**MicrosoftAzureBatch**。</span><span class="sxs-lookup"><span data-stu-id="cefc5-172">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="cefc5-173">**Microsoft Azure Batch**。</span><span class="sxs-lookup"><span data-stu-id="cefc5-173">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="cefc5-174">較新的 Azure AD 租用戶可以使用這個名稱。</span><span class="sxs-lookup"><span data-stu-id="cefc5-174">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="cefc5-175">**ddbf3205-c6bd-46ae-8127-60eb93363864**是 hello 識別碼 hello 批次 API。</span><span class="sxs-lookup"><span data-stu-id="cefc5-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** is hello ID for hello Batch API.</span></span> 
6. <span data-ttu-id="cefc5-176">一旦您找到 hello 批次 API，請選取它，然後按一下 hello**選取** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cefc5-176">Once you find hello Batch API, select it and click hello **Select** button.</span></span>
6. <span data-ttu-id="cefc5-177">在步驟 2 中，選取 hello 核取方塊旁太**存取 Azure 批次服務**按一下 hello**選取** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cefc5-177">In step 2, select hello check box next too**Access Azure Batch Service** and click hello **Select** button.</span></span>
7. <span data-ttu-id="cefc5-178">按一下 hello**完成** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cefc5-178">Click hello **Done** button.</span></span>

<span data-ttu-id="cefc5-179">hello**必要的使用權限**刀鋒視窗現在顯示您的 Azure AD 應用程式具有存取 tooboth ADAL 和 hello 批次服務 API。</span><span class="sxs-lookup"><span data-stu-id="cefc5-179">hello **Required Permissions** blade now shows that your Azure AD application has access tooboth ADAL and hello Batch service API.</span></span> <span data-ttu-id="cefc5-180">權限會自動授與 tooADAL 當您第一次使用 Azure AD 註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cefc5-180">Permissions are granted tooADAL automatically when you first register your app with Azure AD.</span></span>

![授與 API 權限](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a><span data-ttu-id="cefc5-182">使用服務主體</span><span class="sxs-lookup"><span data-stu-id="cefc5-182">Use a service principal</span></span> 

<span data-ttu-id="cefc5-183">tooauthenticate 執行自動安裝的應用程式，您可以使用服務主體。</span><span class="sxs-lookup"><span data-stu-id="cefc5-183">tooauthenticate an application that runs unattended, you use a service principal.</span></span> <span data-ttu-id="cefc5-184">您已註冊您的應用程式之後，請遵循下列步驟在 hello Azure 入口網站 tooconfigure 服務主體：</span><span class="sxs-lookup"><span data-stu-id="cefc5-184">After you've registered your application, follow these steps in hello Azure portal tooconfigure a service principal:</span></span>

1. <span data-ttu-id="cefc5-185">要求應用程式的祕密金鑰。</span><span class="sxs-lookup"><span data-stu-id="cefc5-185">Request a secret key for your application.</span></span>
2. <span data-ttu-id="cefc5-186">指派 RBAC 角色 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cefc5-186">Assign an RBAC role tooyour application.</span></span>

### <a name="request-a-secret-key-for-your-application"></a><span data-ttu-id="cefc5-187">要求應用程式的祕密金鑰</span><span class="sxs-lookup"><span data-stu-id="cefc5-187">Request a secret key for your application</span></span>

<span data-ttu-id="cefc5-188">當您的應用程式進行驗證與服務主體時，會傳送 hello 應用程式識別碼和祕密金鑰 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="cefc5-188">When your application authenticates with a service principal, it sends both hello application ID and a secret key tooAzure AD.</span></span> <span data-ttu-id="cefc5-189">您將需要 toocreate，並從您的程式碼複製 hello 秘密金鑰 toouse。</span><span class="sxs-lookup"><span data-stu-id="cefc5-189">You'll need toocreate and copy hello secret key toouse from your code.</span></span>

<span data-ttu-id="cefc5-190">請遵循這些步驟 hello Azure 入口網站中：</span><span class="sxs-lookup"><span data-stu-id="cefc5-190">Follow these steps in hello Azure portal:</span></span>

1. <span data-ttu-id="cefc5-191">在 hello 左側導覽窗格中的 hello Azure 入口網站，選擇 **更服務**，按一下**應用程式註冊**。</span><span class="sxs-lookup"><span data-stu-id="cefc5-191">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="cefc5-192">搜尋 hello hello 清單中的應用程式註冊您應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="cefc5-192">Search for hello name of your application in hello list of app registrations.</span></span>
3. <span data-ttu-id="cefc5-193">顯示 hello**設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="cefc5-193">Display hello **Settings** blade.</span></span> <span data-ttu-id="cefc5-194">在 hello **API 存取**區段中，選取**金鑰**。</span><span class="sxs-lookup"><span data-stu-id="cefc5-194">In hello **API Access** section, select **Keys**.</span></span>
4. <span data-ttu-id="cefc5-195">toocreate 金鑰，請輸入 hello 索引鍵的說明。</span><span class="sxs-lookup"><span data-stu-id="cefc5-195">toocreate a key, enter a description for hello key.</span></span> <span data-ttu-id="cefc5-196">然後，選取一或二年 hello 索引鍵的持續時間。</span><span class="sxs-lookup"><span data-stu-id="cefc5-196">Then select a duration for hello key of either one or two years.</span></span> 
5. <span data-ttu-id="cefc5-197">按一下 hello**儲存**按鈕 toocreate，並顯示 hello 鍵。</span><span class="sxs-lookup"><span data-stu-id="cefc5-197">Click hello **Save** button toocreate and display hello key.</span></span> <span data-ttu-id="cefc5-198">您必須能夠 tooaccess 複製 hello 索引鍵值 tooa 安全的地方，它一次之後保留 hello 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="cefc5-198">Copy hello key value tooa safe place, as you won't be able tooaccess it again after you leave hello blade.</span></span> 

    ![建立祕密金鑰](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-tooyour-application"></a><span data-ttu-id="cefc5-200">指派 RBAC 角色 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="cefc5-200">Assign an RBAC role tooyour application</span></span>

<span data-ttu-id="cefc5-201">與服務主體 tooauthenticate，您需要 tooassign RBAC 角色 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cefc5-201">tooauthenticate with a service principal, you need tooassign an RBAC role tooyour application.</span></span> <span data-ttu-id="cefc5-202">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cefc5-202">Follow these steps:</span></span>

1. <span data-ttu-id="cefc5-203">在 hello Azure 入口網站，瀏覽您的應用程式所使用的 toohello 批次帳戶。</span><span class="sxs-lookup"><span data-stu-id="cefc5-203">In hello Azure portal, navigate toohello Batch account used by your application.</span></span>
2. <span data-ttu-id="cefc5-204">在 hello**設定**刀鋒視窗中的 hello 批次帳戶，請選取**存取控制 (IAM)**。</span><span class="sxs-lookup"><span data-stu-id="cefc5-204">In hello **Settings** blade for hello Batch account, select **Access Control (IAM)**.</span></span>
3. <span data-ttu-id="cefc5-205">按一下 hello**新增** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cefc5-205">Click hello **Add** button.</span></span> 
4. <span data-ttu-id="cefc5-206">從 hello**角色**下拉式清單中，選擇其中一個 hello_參與者_或_讀取器_應用程式角色。</span><span class="sxs-lookup"><span data-stu-id="cefc5-206">From hello **Role** drop-down, choose either hello _Contributor_ or _Reader_ role for your application.</span></span> <span data-ttu-id="cefc5-207">如需有關這些角色的詳細資訊，請參閱[開始 hello Azure 入口網站中的 角色型存取控制使用](../active-directory/role-based-access-control-what-is.md)。</span><span class="sxs-lookup"><span data-stu-id="cefc5-207">For more information on these roles, see [Get started with Role-Based Access Control in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>  
5. <span data-ttu-id="cefc5-208">在 hello**選取**欄位中，輸入 hello 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="cefc5-208">In hello **Select** field, enter hello name of your application.</span></span> <span data-ttu-id="cefc5-209">從 [hello] 清單中，選取您的應用程式，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="cefc5-209">Select your application from hello list, and click **Save**.</span></span>

<span data-ttu-id="cefc5-210">您的應用程式現在應該會以您指派的 RBAC 角色，出現在您的存取控制設定中。</span><span class="sxs-lookup"><span data-stu-id="cefc5-210">Your application should now appear in your access control settings with an RBAC role assigned.</span></span> 

![指派 RBAC 角色 tooyour 應用程式](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-hello-tenant-id-for-your-azure-active-directory"></a><span data-ttu-id="cefc5-212">取得 Azure Active Directory 中的 hello 租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="cefc5-212">Get hello tenant ID for your Azure Active Directory</span></span>

<span data-ttu-id="cefc5-213">hello 租用戶識別碼會識別 hello Azure AD 租用戶提供驗證服務 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cefc5-213">hello tenant ID identifies hello Azure AD tenant that provides authentication services tooyour application.</span></span> <span data-ttu-id="cefc5-214">tooget hello 租用戶識別碼，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cefc5-214">tooget hello tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="cefc5-215">在 hello Azure 入口網站，選取您的 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="cefc5-215">In hello Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="cefc5-216">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="cefc5-216">Click **Properties**.</span></span>
3. <span data-ttu-id="cefc5-217">複製 hello GUID 值提供給 hello 目錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="cefc5-217">Copy hello GUID value provided for hello directory ID.</span></span> <span data-ttu-id="cefc5-218">此值也稱為 hello 租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="cefc5-218">This value is also called hello tenant ID.</span></span>

![複製 hello 目錄識別碼](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a><span data-ttu-id="cefc5-220">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="cefc5-220">Code examples</span></span>

<span data-ttu-id="cefc5-221">本節中的 hello 程式碼範例顯示如何使用 Azure AD tooauthenticate 整合式驗證，以及與服務主體。</span><span class="sxs-lookup"><span data-stu-id="cefc5-221">hello code examples in this section show how tooauthenticate with Azure AD using integrated authentication and with a service principal.</span></span> <span data-ttu-id="cefc5-222">這些程式碼範例會使用.NET 中，但 hello 概念類似於其他語言。</span><span class="sxs-lookup"><span data-stu-id="cefc5-222">These code examples use .NET, but hello concepts are similar for other languages.</span></span>

> [!NOTE]
> <span data-ttu-id="cefc5-223">Azure AD 驗證權杖會在一小時後過期。</span><span class="sxs-lookup"><span data-stu-id="cefc5-223">An Azure AD authentication token expires after one hour.</span></span> <span data-ttu-id="cefc5-224">使用長時間執行時**BatchClient**物件，我們建議您擷取權杖從 ADAL 上每個要求 tooensure 一定有效的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="cefc5-224">When using a long-lived **BatchClient** object, we recommend that you retrieve a token from ADAL on every request tooensure you always have a valid token.</span></span> 
>
>
> <span data-ttu-id="cefc5-225">tooachieve 這在.NET 中，撰寫方法擷取 hello 從 Azure AD 權杖，並傳遞該方法 tooa **BatchTokenCredentials**為委派的物件。</span><span class="sxs-lookup"><span data-stu-id="cefc5-225">tooachieve this in .NET, write a method that retrieves hello token from Azure AD and pass that method tooa **BatchTokenCredentials** object as a delegate.</span></span> <span data-ttu-id="cefc5-226">hello 委派方法會呼叫每個要求 toohello 批次服務 tooensure 提供有效的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="cefc5-226">hello delegate method is called on every request toohello Batch service tooensure that a valid token is provided.</span></span> <span data-ttu-id="cefc5-227">根據預設，ADAL 會快取權杖，因此只在必要時才會從 Azure AD 擷取新的權杖。</span><span class="sxs-lookup"><span data-stu-id="cefc5-227">By default ADAL caches tokens, so a new token is retrieved from Azure AD only when necessary.</span></span> <span data-ttu-id="cefc5-228">如需關於 Azure AD 中的權杖資訊，請參閱 [Azure AD 的驗證案例][aad_auth_scenarios]。</span><span class="sxs-lookup"><span data-stu-id="cefc5-228">For more information about tokens in Azure AD, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a><span data-ttu-id="cefc5-229">程式碼範例︰搭配 Batch .NET 使用 Azure AD 整合式驗證</span><span class="sxs-lookup"><span data-stu-id="cefc5-229">Code example: Using Azure AD integrated authentication with Batch .NET</span></span>

<span data-ttu-id="cefc5-230">使用整合式驗證從批次.NET 中，參考 hello tooauthenticate [Azure 批次.NET](https://www.nuget.org/packages/Azure.Batch/)封裝和 hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/)封裝。</span><span class="sxs-lookup"><span data-stu-id="cefc5-230">tooauthenticate with integrated authentication from Batch .NET, reference hello [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="cefc5-231">Hello 如下`using`程式碼中的陳述式：</span><span class="sxs-lookup"><span data-stu-id="cefc5-231">Include hello following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="cefc5-232">參考 hello Azure AD 端點，在您的程式碼，包括 hello 租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="cefc5-232">Reference hello Azure AD endpoint in your code, including hello tenant ID.</span></span> <span data-ttu-id="cefc5-233">tooretrieve hello 租用戶識別碼，請遵循所述的 hello 步驟[取得 Azure Active Directory 中的 hello 租用戶識別碼](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="cefc5-233">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="cefc5-234">參考 hello 批次服務資源端點：</span><span class="sxs-lookup"><span data-stu-id="cefc5-234">Reference hello Batch service resource endpoint:</span></span>

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="cefc5-235">參考您的 Batch 帳戶：</span><span class="sxs-lookup"><span data-stu-id="cefc5-235">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="cefc5-236">指定您的應用程式的 hello 應用程式識別碼 （用戶端識別碼）。</span><span class="sxs-lookup"><span data-stu-id="cefc5-236">Specify hello application ID (client ID) for your application.</span></span> <span data-ttu-id="cefc5-237">hello 應用程式識別碼是可從您的應用程式註冊在 hello Azure 入口網站中：</span><span class="sxs-lookup"><span data-stu-id="cefc5-237">hello application ID is available from your app registration in hello Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="cefc5-238">也請複製 hello 重新導向 hello 註冊程序期間所指定的 URI。</span><span class="sxs-lookup"><span data-stu-id="cefc5-238">Also copy hello redirect URI that you specified during hello registration process.</span></span> <span data-ttu-id="cefc5-239">hello 重新導向 URI 指定在您的程式碼必須符合 hello 重新導向時註冊 hello 應用程式所提供的 URI:</span><span class="sxs-lookup"><span data-stu-id="cefc5-239">hello redirect URI specified in your code must match hello redirect URI that you provided when you registered hello application:</span></span>

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

<span data-ttu-id="cefc5-240">從 Azure AD 中撰寫回呼方法 tooacquire hello 驗證語彙基元。</span><span class="sxs-lookup"><span data-stu-id="cefc5-240">Write a callback method tooacquire hello authentication token from Azure AD.</span></span> <span data-ttu-id="cefc5-241">hello **GetAuthenticationTokenAsync**如下所示的回呼方法會呼叫 ADAL tooauthenticate hello 應用程式互動的使用者。</span><span class="sxs-lookup"><span data-stu-id="cefc5-241">hello **GetAuthenticationTokenAsync** callback method shown here calls ADAL tooauthenticate a user who is interacting with hello application.</span></span> <span data-ttu-id="cefc5-242">hello **AcquireTokenAsync**方法提供 adal 提示 hello 使用者輸入其認證，然後 hello 應用程式一次進行 hello 使用者提供他們 （除非它已快取的認證）：</span><span class="sxs-lookup"><span data-stu-id="cefc5-242">hello **AcquireTokenAsync** method provided by ADAL prompts hello user for their credentials, and hello application proceeds once hello user provides them (unless it has already cached credentials):</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire hello authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

<span data-ttu-id="cefc5-243">建構**BatchTokenCredentials**採用 hello 委派做為參數的物件。</span><span class="sxs-lookup"><span data-stu-id="cefc5-243">Construct a **BatchTokenCredentials** object that takes hello delegate as a parameter.</span></span> <span data-ttu-id="cefc5-244">使用這些認證 tooopen **BatchClient**物件。</span><span class="sxs-lookup"><span data-stu-id="cefc5-244">Use those credentials tooopen a **BatchClient** object.</span></span> <span data-ttu-id="cefc5-245">您可以使用該**BatchClient** hello 批次服務針對後續作業的物件：</span><span class="sxs-lookup"><span data-stu-id="cefc5-245">You can use that **BatchClient** object for subsequent operations against hello Batch service:</span></span>

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

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a><span data-ttu-id="cefc5-246">程式碼範例︰搭配 Batch .NET 使用 Azure AD 服務主體</span><span class="sxs-lookup"><span data-stu-id="cefc5-246">Code example: Using an Azure AD service principal with Batch .NET</span></span>

<span data-ttu-id="cefc5-247">與服務主體從批次.NET 中，參考 hello tooauthenticate [Azure 批次.NET](https://www.nuget.org/packages/Azure.Batch/)封裝和 hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/)封裝。</span><span class="sxs-lookup"><span data-stu-id="cefc5-247">tooauthenticate with a service principal from Batch .NET, reference hello [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="cefc5-248">Hello 如下`using`程式碼中的陳述式：</span><span class="sxs-lookup"><span data-stu-id="cefc5-248">Include hello following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="cefc5-249">參考 hello Azure AD 端點，在您的程式碼，包括 hello 租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="cefc5-249">Reference hello Azure AD endpoint in your code, including hello tenant ID.</span></span> <span data-ttu-id="cefc5-250">使用服務主體時，您必須提供租用戶特定的端點。</span><span class="sxs-lookup"><span data-stu-id="cefc5-250">When using a service principal, you must provide a tenant-specific endpoint.</span></span> <span data-ttu-id="cefc5-251">tooretrieve hello 租用戶識別碼，請遵循所述的 hello 步驟[取得 Azure Active Directory 中的 hello 租用戶識別碼](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="cefc5-251">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="cefc5-252">參考 hello 批次服務資源端點：</span><span class="sxs-lookup"><span data-stu-id="cefc5-252">Reference hello Batch service resource endpoint:</span></span>  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="cefc5-253">參考您的 Batch 帳戶：</span><span class="sxs-lookup"><span data-stu-id="cefc5-253">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="cefc5-254">指定您的應用程式的 hello 應用程式識別碼 （用戶端識別碼）。</span><span class="sxs-lookup"><span data-stu-id="cefc5-254">Specify hello application ID (client ID) for your application.</span></span> <span data-ttu-id="cefc5-255">hello 應用程式識別碼是可從您的應用程式註冊在 hello Azure 入口網站中：</span><span class="sxs-lookup"><span data-stu-id="cefc5-255">hello application ID is available from your app registration in hello Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="cefc5-256">指定您所複製的 hello Azure 入口網站的 hello 祕密金鑰：</span><span class="sxs-lookup"><span data-stu-id="cefc5-256">Specify hello secret key that you copied from hello Azure portal:</span></span>

```csharp
private const string ClientKey = "<secret-key>";
```

<span data-ttu-id="cefc5-257">從 Azure AD 中撰寫回呼方法 tooacquire hello 驗證語彙基元。</span><span class="sxs-lookup"><span data-stu-id="cefc5-257">Write a callback method tooacquire hello authentication token from Azure AD.</span></span> <span data-ttu-id="cefc5-258">hello **GetAuthenticationTokenAsync**回呼方法，如下所示呼叫 ADAL 自動驗證：</span><span class="sxs-lookup"><span data-stu-id="cefc5-258">hello **GetAuthenticationTokenAsync** callback method shown here calls ADAL for unattended authentication:</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

<span data-ttu-id="cefc5-259">建構**BatchTokenCredentials**採用 hello 委派做為參數的物件。</span><span class="sxs-lookup"><span data-stu-id="cefc5-259">Construct a **BatchTokenCredentials** object that takes hello delegate as a parameter.</span></span> <span data-ttu-id="cefc5-260">使用這些認證 tooopen **BatchClient**物件。</span><span class="sxs-lookup"><span data-stu-id="cefc5-260">Use those credentials tooopen a **BatchClient** object.</span></span> <span data-ttu-id="cefc5-261">然後您可以使用， **BatchClient** hello 批次服務針對後續作業的物件：</span><span class="sxs-lookup"><span data-stu-id="cefc5-261">You can then use that **BatchClient** object for subsequent operations against hello Batch service:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="cefc5-262">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cefc5-262">Next steps</span></span>

<span data-ttu-id="cefc5-263">toolearn 進一步了解 Azure AD，請參閱 hello [Azure Active Directory 文件](https://docs.microsoft.com/azure/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="cefc5-263">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="cefc5-264">深入了解範例來示範如何 toouse ADAL 位於 hello [Azure 程式碼範例](https://azure.microsoft.com/resources/samples/?service=active-directory)程式庫。</span><span class="sxs-lookup"><span data-stu-id="cefc5-264">In-depth examples showing how toouse ADAL are available in hello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="cefc5-265">toolearn 進一步了解服務主體，請參閱[應用程式與 Azure Active Directory 中的服務主體物件](../active-directory/develop/active-directory-application-objects.md)。</span><span class="sxs-lookup"><span data-stu-id="cefc5-265">toolearn more about service principals, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span> <span data-ttu-id="cefc5-266">服務主體使用 toocreate hello Azure 入口網站，請參閱[使用入口網站 toocreate Active Directory 應用程式和服務主體可存取資源](../resource-group-create-service-principal-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="cefc5-266">toocreate a service principal using hello Azure portal, see [Use portal toocreate Active Directory application and service principal that can access resources](../resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="cefc5-267">您也可以使用 PowerShell 或 Azure CLI 來建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="cefc5-267">You can also create a service principal with PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="cefc5-268">tooauthenticate 批次管理應用程式使用 Azure AD，請參閱[與 Active Directory 驗證批次管理解決方案](batch-aad-auth-management.md)。</span><span class="sxs-lookup"><span data-stu-id="cefc5-268">tooauthenticate Batch Management applications using Azure AD, see [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span> 

[aad_about]: ../active-directory/active-directory-whatis.md "什麼是 Azure Active Directory？"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD 的驗證案例"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "整合應用程式與 Azure Active Directory"
[azure_portal]: http://portal.azure.com
