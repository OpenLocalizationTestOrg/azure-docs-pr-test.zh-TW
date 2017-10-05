---
title: "了解 Azure Active Directory 應用程式資訊清單 | Microsoft Docs"
description: "詳細說明 Azure Active Directory 應用程式資訊清單；此資訊清單代表應用程式在 Azure AD 租用戶中的身分識別組態，可用來協助進行 OAuth 授權、同意體驗等等。"
services: active-directory
documentationcenter: 
author: sureshja
manager: mbaldwin
editor: 
ms.assetid: 4804f3d4-0ff1-4280-b663-f8f10d54d184
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: sureshja
ms.custom: aaddev
ms.reviewer: elisol
ms.openlocfilehash: d5e18f41d6eb69ccb7eafaa4de2646c4c38df5e2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="understanding-the-azure-active-directory-application-manifest"></a><span data-ttu-id="4e9dd-103">了解 Azure Active Directory 應用程式資訊清單</span><span class="sxs-lookup"><span data-stu-id="4e9dd-103">Understanding the Azure Active Directory application manifest</span></span>
<span data-ttu-id="4e9dd-104">與 Azure Active Directory (AD) 整合的應用程式必須向 Azure AD 租用戶註冊，提供應用程式的持續性身分識別組態。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-104">Applications that integrate with Azure Active Directory (AD) must be registered with an Azure AD tenant, providing a persistent identity configuration for the application.</span></span> <span data-ttu-id="4e9dd-105">在執行階段參考此組態，啟用允許應用程式透過 Azure AD 外部和代理驗證/授權的案例。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-105">This configuration is consulted at runtime, enabling scenarios that allow an application to outsource and broker authentication/authorization through Azure AD.</span></span> <span data-ttu-id="4e9dd-106">如需 Azure AD 應用程式模型的詳細資訊，請參閱[新增、更新及移除應用程式][ADD-UPD-RMV-APP]一文。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-106">For more information about the Azure AD application model, see the [Adding, Updating, and Removing an Application][ADD-UPD-RMV-APP] article.</span></span>

## <a name="updating-an-applications-identity-configuration"></a><span data-ttu-id="4e9dd-107">更新應用程式的身分識別組態</span><span class="sxs-lookup"><span data-stu-id="4e9dd-107">Updating an application's identity configuration</span></span>
<span data-ttu-id="4e9dd-108">實際上有多個可用的選項可更新應用程式的身分識別組態屬性，隨著功能與困難度而有所不同，包括下列選項：</span><span class="sxs-lookup"><span data-stu-id="4e9dd-108">There are actually multiple options available for updating the properties on an application's identity configuration, which vary in capabilities and degrees of difficulty, including the following:</span></span>

* <span data-ttu-id="4e9dd-109">**[Azure 入口網站][AZURE-PORTAL] 的 Web 使用者介面** 可讓您更新應用程式的最常見屬性。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-109">The **[Azure portal's][AZURE-PORTAL] Web user interface** allows you to update the most common properties of an application.</span></span> <span data-ttu-id="4e9dd-110">這是更新應用程式屬性最快速且最不容易有錯誤的方法，但無法提供您所有屬性的完整存取權，如同下面兩個方法。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-110">This is the quickest and least error prone way of updating your application's properties, but does not give you full access to all properties, like the next two methods.</span></span>
* <span data-ttu-id="4e9dd-111">對於更進階的案例 (您在其中必須更新 Azure 傳統入口網站中未公開的屬性)，您可以修改 **應用程式資訊清單**。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-111">For more advanced scenarios where you need to update properties that are not exposed in the Azure classic portal, you can modify the **application manifest**.</span></span> <span data-ttu-id="4e9dd-112">這是本文的重點，並且會在下一節中開始詳細討論。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-112">This is the focus of this article and is discussed in more detail starting in the next section.</span></span>
* <span data-ttu-id="4e9dd-113">它也可**撰寫使用[圖形 API][GRAPH-API] 的應用程式**來更新您的應用程式，這樣是最費力的。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-113">It's also possible to **write an application that uses the [Graph API][GRAPH-API]** to update your application, which requires the most effort.</span></span> <span data-ttu-id="4e9dd-114">如果您要撰寫管理軟體或需要自動定期更新應用程式屬性，這可能是個不錯的選擇。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-114">This may be an attractive option though, if you are writing management software, or need to update application properties on a regular basis in an automated fashion.</span></span>

## <a name="using-the-application-manifest-to-update-an-applications-identity-configuration"></a><span data-ttu-id="4e9dd-115">使用應用程式資訊清單來更新應用程式的身分識別組態</span><span class="sxs-lookup"><span data-stu-id="4e9dd-115">Using the application manifest to update an application's identity configuration</span></span>
<span data-ttu-id="4e9dd-116">透過 [Azure 入口網站][AZURE-PORTAL]，您可以使用內嵌資訊清單編輯器更新應用程式資訊清單，藉此管理應用程式的身分識別組態。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-116">Through the [Azure portal][AZURE-PORTAL], you can manage your application's identity configuration by updating the application manifest using the inline manifest editor.</span></span> <span data-ttu-id="4e9dd-117">您也可以下載和上傳 JSON 檔案形式的應用程式資訊清單。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-117">You can also download and upload the application manifest as a JSON file.</span></span> <span data-ttu-id="4e9dd-118">沒有任何實際檔案會儲存在目錄中。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-118">No actual file is stored in the directory.</span></span> <span data-ttu-id="4e9dd-119">應用程式資訊清單只是「Azure AD Graph API 應用程式」實體上的 HTTP GET 作業，而上傳則是「應用程式」實體上的 HTTP PATCH 作業。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-119">The application manifest is merely an HTTP GET operation on the Azure AD Graph API Application entity, and the upload is an HTTP PATCH operation on the Application entity.</span></span>

<span data-ttu-id="4e9dd-120">因此，若要了解應用程式資訊清單的格式和屬性，您必須參考圖形 API [應用程式實體][APPLICATION-ENTITY]文件。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-120">As a result, in order to understand the format and properties of the application manifest, you will need to reference the Graph API [Application entity][APPLICATION-ENTITY] documentation.</span></span> <span data-ttu-id="4e9dd-121">可透過應用程式資訊清單上傳執行的更新範例包括：</span><span class="sxs-lookup"><span data-stu-id="4e9dd-121">Examples of updates that can be performed though application manifest upload include:</span></span>

* <span data-ttu-id="4e9dd-122">**宣告您的 Web API 所公開的權限範圍 (oauth2Permissions)** 。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-122">**Declare permission scopes (oauth2Permissions)** exposed by your web API.</span></span> <span data-ttu-id="4e9dd-123">如需有關使用 oauth2Permissions 委派權限範圍來實作使用者模擬的資訊，請參閱[整合應用程式與 Azure Active Directory][INTEGRATING-APPLICATIONS-AAD]中的＜向其他應用程式公開 Web API＞主題。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-123">See the "Exposing Web APIs to Other Applications" topic in [Integrating Applications with Azure Active Directory][INTEGRATING-APPLICATIONS-AAD] for information on implementing user impersonation using the oauth2Permissions delegated permission scope.</span></span> <span data-ttu-id="4e9dd-124">如先前所述，應用程式實體屬性都記錄在圖形 API [實體和複雜類型][APPLICATION-ENTITY]參考文章中，包括屬於 [OAuth2Permission][APPLICATION-ENTITY-OAUTH2-PERMISSION] 類型之集合的 oauth2Permissions 屬性。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-124">As mentioned previously, Application entity properties are documented in the Graph API [Entity and Complex Type][APPLICATION-ENTITY] reference article, including the oauth2Permissions property which is a collection of type [OAuth2Permission][APPLICATION-ENTITY-OAUTH2-PERMISSION].</span></span>
* <span data-ttu-id="4e9dd-125">**宣告您的應用程式所公開的應用程式角色 (appRoles)**。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-125">**Declare application roles (appRoles) exposed by your app**.</span></span> <span data-ttu-id="4e9dd-126">應用程式實體的 appRole 屬性是 [AppRole][APPLICATION-ENTITY-APP-ROLE] 類型的集合。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-126">The Application entity's appRoles property is a collection of type [AppRole][APPLICATION-ENTITY-APP-ROLE].</span></span> <span data-ttu-id="4e9dd-127">請參閱[雲端應用程式中使用 Azure AD 的角色型存取控制][RBAC-CLOUD-APPS-AZUREAD]一文以取得實作範例。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-127">See the [Role based access control in cloud applications using Azure AD][RBAC-CLOUD-APPS-AZUREAD] article for an implementation example.</span></span>
* <span data-ttu-id="4e9dd-128">**宣告已知的用戶端應用程式 (knownClientApplications)**，可讓您以邏輯方式將指定用戶端應用程式的同意繫結至資源/Web API。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-128">**Declare known client applications (knownClientApplications)**, which allow you to logically tie the consent of the specified client application(s) to the resource/web API.</span></span>
* <span data-ttu-id="4e9dd-129">**要求 Azure AD 對登入使用者發出群組成員資格宣告 (groupMembershipClaims)** 。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-129">**Request Azure AD to issue group memberships claim** for the signed in user (groupMembershipClaims).</span></span>  <span data-ttu-id="4e9dd-130">這也可以設定為發出有關使用者目錄角色成員資格的宣告。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-130">This can also be configured to issue claims about the user's directory roles memberships.</span></span> <span data-ttu-id="4e9dd-131">請參閱[雲端應用程式中使用 AD 群組的授權][AAD-GROUPS-FOR-AUTHORIZATION]一文以取得實作範例。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-131">See the [Authorization in Cloud Applications using AD Groups][AAD-GROUPS-FOR-AUTHORIZATION] article for an implementation example.</span></span>
* <span data-ttu-id="4e9dd-132">**可讓您的應用程式支援 OAuth 2.0 隱含授權** 流程 (oauth2AllowImplicitFlow)。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-132">**Allow your application to support OAuth 2.0 Implicit grant** flows (oauth2AllowImplicitFlow).</span></span> <span data-ttu-id="4e9dd-133">此類型的授權流程可用於內嵌的 JavaScript 網頁或單一頁面應用程式 (SPA)。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-133">This type of grant flow is used with embedded JavaScript web pages or Single Page Applications (SPA).</span></span> <span data-ttu-id="4e9dd-134">如需有關隱含授權授與的詳細資訊，請參閱[了解 Azure Active Directory 中的 OAuth2 隱含授與流程][IMPLICIT-GRANT]。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-134">For more information on the implicit authorization grant, see [Understanding the OAuth2 implicit grant flow in Azure Active Directory][IMPLICIT-GRANT].</span></span>
* <span data-ttu-id="4e9dd-135">**啟用 X509 憑證做為秘密金鑰** (keyCredentials)。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-135">**Enable use of X509 certificates as the secret key** (keyCredentials).</span></span> <span data-ttu-id="4e9dd-136">如需實作範例，請參閱[在 Office 365 中建置服務與精靈應用程式][O365-SERVICE-DAEMON-APPS]和[利用 Azure Resource Manager API 進行驗證開發人員指南][DEV-GUIDE-TO-AUTH-WITH-ARM]等文章。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-136">See the [Build service and daemon apps in Office 365][O365-SERVICE-DAEMON-APPS] and [Developer’s guide to auth with Azure Resource Manager API][DEV-GUIDE-TO-AUTH-WITH-ARM] articles for implementation examples.</span></span>
* <span data-ttu-id="4e9dd-137">為應用程式**新增應用程式識別碼 URI** (identifierURIs[])。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-137">**Add a new App ID URI** for your application (identifierURIs[]).</span></span> <span data-ttu-id="4e9dd-138">「應用程式識別碼 URI」可用來在應用程式的 Azure AD 租用戶內 (或針對透過已驗證的自訂網域來限定資格的多租用戶案例，則可跨多個 Azure AD 租用戶)，唯一識別該應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-138">App ID URIs are used to uniquely identify an application within its Azure AD tenant (or across multiple Azure AD tenants, for multi-tenant scenarios when qualified via verified custom domain).</span></span> <span data-ttu-id="4e9dd-139">在要求資源應用程式的權限或取得資源應用程式的存取權杖時，就會使用這些 URI。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-139">They are used when requesting permissions to a resource application, or acquiring an access token for a resource application.</span></span> <span data-ttu-id="4e9dd-140">當您更新此元素時，相同的更新也會套用到對應之服務主體的 servicePrincipalNames[] 集合 (位於應用程式的主要租用戶中)。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-140">When you update this element, the same update is made to the corresponding service principal's servicePrincipalNames[] collection, which lives in the application's home tenant.</span></span>

<span data-ttu-id="4e9dd-141">應用程式資訊清單也會提供追蹤應用程式註冊狀態的好方法。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-141">The application manifest also provides a good way to track the state of your application registration.</span></span> <span data-ttu-id="4e9dd-142">因為它可供 JSON 格式使用，所以檔案表示法可以簽入您的原始檔控制，以及應用程式的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-142">Because it's available in JSON format, the file representation can be checked into your source control, along with your application's source code.</span></span>

## <a name="step-by-step-example"></a><span data-ttu-id="4e9dd-143">逐步執行範例</span><span class="sxs-lookup"><span data-stu-id="4e9dd-143">Step by step example</span></span>
<span data-ttu-id="4e9dd-144">現在可逐步了解透過應用程式資訊清單更新您的應用程式身分識別組態所需的步驟：</span><span class="sxs-lookup"><span data-stu-id="4e9dd-144">Now lets walk through the steps required to update your application's identity configuration through the application manifest.</span></span> <span data-ttu-id="4e9dd-145">我們會加強說明上述其中一個範例，示範如何在資源應用程式上宣告一個新的權限範圍：</span><span class="sxs-lookup"><span data-stu-id="4e9dd-145">We will highlight one of the preceding examples, showing how to declare a new permission scope on a resource application:</span></span>

1. <span data-ttu-id="4e9dd-146">登入 [Azure 入口網站][AZURE-PORTAL]。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-146">Sign in to the [Azure portal][AZURE-PORTAL].</span></span>
2. <span data-ttu-id="4e9dd-147">驗證後，在頁面右上角選取您的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-147">After you've authenticated, choose your Azure AD tenant by selecting it from the top right corner of the page.</span></span>
3. <span data-ttu-id="4e9dd-148">選取左邊的導覽面板中的 [Azure Active Directory] 擴充，按一下 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-148">Select **Azure Active Directory** extension from the left navigation panel and click on **App Registrations**.</span></span>
4. <span data-ttu-id="4e9dd-149">找到您要在清單中更新的應用程式並按一下它。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-149">Find the application you want to update in the list and click on it.</span></span>
5. <span data-ttu-id="4e9dd-150">按一下應用程式頁面中的 [資訊清單]，以開啟內嵌資訊清單編輯器。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-150">From the application page, click **Manifest** to open the inline manifest editor.</span></span> 
6. <span data-ttu-id="4e9dd-151">您可以使用此編輯器直接編輯資訊清單。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-151">You can directly edit the manifest using this editor.</span></span> <span data-ttu-id="4e9dd-152">請注意，資訊清單遵循我們先前提到的[應用程式實體][APPLICATION-ENTITY]結構描述：例如，假設我們想要在資源應用程式 (API) 上實作/公開名為 "Employees.Read.All" 的新權限，您只需將新的/第二個元素新增至 oauth2Permissions 集合即可，即：</span><span class="sxs-lookup"><span data-stu-id="4e9dd-152">Note that the manifest follows the schema for the [Application entity][APPLICATION-ENTITY] as we mentioned earlier: For example, assuming we want to implement/expose a new permission called "Employees.Read.All" on our resource application (API), you would simply add a new/second element to the oauth2Permissions collection, ie:</span></span>
   
        "oauth2Permissions": [
        {
        "adminConsentDescription": "Allow the application to access MyWebApplication on behalf of the signed-in user.",
        "adminConsentDisplayName": "Access MyWebApplication",
        "id": "aade5b35-ea3e-481c-b38d-cba4c78682a0",
        "isEnabled": true,
        "type": "User",
        "userConsentDescription": "Allow the application to access MyWebApplication on your behalf.",
        "userConsentDisplayName": "Access MyWebApplication",
        "value": "user_impersonation"
        },
        {
        "adminConsentDescription": "Allow the application to have read-only access to all Employee data.",
        "adminConsentDisplayName": "Read-only access to Employee records",
        "id": "2b351394-d7a7-4a84-841e-08a6a17e4cb8",
        "isEnabled": true,
        "type": "User",
        "userConsentDescription": "Allow the application to have read-only access to your Employee data.",
        "userConsentDisplayName": "Read-only access to your Employee records",
        "value": "Employees.Read.All"
        }
        ],
   
    <span data-ttu-id="4e9dd-153">項目必須是唯一的，因此您必須為 `"id"` 屬性產生新的全域唯一識別碼 (GUID)。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-153">The entry must be unique, and you must therefore generate a new Globally Unique ID (GUID) for the `"id"` property.</span></span> <span data-ttu-id="4e9dd-154">在此情況下，由於我們已指定 `"type": "User"`，因此任何已由資源/API 應用程式註冊所在的 Azure AD 租用戶驗證的帳戶都可以對此權限表示同意。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-154">In this case, because we specified `"type": "User"`, this permission can be consented to by any account authenticated by the Azure AD tenant in which the resource/API application is registered.</span></span> <span data-ttu-id="4e9dd-155">這會授與用戶端應用程式代表帳戶存取它的權限。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-155">This grants the client application permission to access it on the account's behalf.</span></span> <span data-ttu-id="4e9dd-156">在同意期間會使用說明和顯示名稱字串，並且顯示在 Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-156">The description and display name strings are used during consent and for display in the Azure portal.</span></span>
6. <span data-ttu-id="4e9dd-157">當您完成資訊清單更新時，按一下 [儲存] 儲存資訊清單。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-157">When you're finished updating the manifest, click **Save** to save the manifest.</span></span>  
   
<span data-ttu-id="4e9dd-158">既然已儲存資訊清單，您便可以授權已註冊的用戶端應用程式存取我們在上面新增的權限。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-158">Now that the manifest is saved, you can give a registered client application access to the new permission we added above.</span></span> <span data-ttu-id="4e9dd-159">此時，您可以使用 Azure 入口網站的 Web UI，而不是編輯用戶端應用程式的資訊清單：</span><span class="sxs-lookup"><span data-stu-id="4e9dd-159">This time you can use the Azure portal's Web UI instead of editing the client application's manifest:</span></span>  

1. <span data-ttu-id="4e9dd-160">首先，移至要新增新 API 之存取權的用戶端應用程式的 [設定] 刀鋒視窗，按一下 [必要的權限]，然後選擇 [選取 API]。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-160">First go to the **Settings** blade of the client application to which you wish to add access to the new API, click **Required Permissions** and choose **Select an API**.</span></span>
2. <span data-ttu-id="4e9dd-161">畫面中會顯示租用戶中已註冊的資源應用程式 (API) 的清單。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-161">Then you will be presented with the list of registered resource applications (APIs) in the tenant.</span></span> <span data-ttu-id="4e9dd-162">按一下資源應用程式以選取它，或在搜尋方塊中輸入應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-162">Click the resource application to select it, or type the name of the application the search box.</span></span> <span data-ttu-id="4e9dd-163">當您找到該應用程式時，按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-163">When you've found the application, click **Select**.</span></span>  
3. <span data-ttu-id="4e9dd-164">這會將您帶到 [選取權限] 頁面，其中顯示該資源應用程式可使用的 [應用程式權限] 和 [委派權限] 的清單。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-164">This will take you to the **Select Permissions** page, which will show the list of Application Permissions and Delegated Permissions available for the resource application.</span></span> <span data-ttu-id="4e9dd-165">選取新的權限，以將其新增至用戶端要求的權限清單。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-165">Select the new permission in order to add it to the client's requested list of permissions.</span></span> <span data-ttu-id="4e9dd-166">這個新的權限會儲存在用戶端應用程式身分識別組態的 "requiredResourceAccess" 集合屬性中。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-166">This new permission will be stored in the client application's identity configuration, in the "requiredResourceAccess" collection property.</span></span>


<span data-ttu-id="4e9dd-167">就這麼簡單。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-167">That's it.</span></span> <span data-ttu-id="4e9dd-168">現在，您的應用程式將會使用其新的身分識別組態來執行。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-168">Now your applications will run using their new identity configuration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e9dd-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4e9dd-169">Next steps</span></span>
* <span data-ttu-id="4e9dd-170">如需有關應用程式之「應用程式」和「服務主體」物件之間關係的詳細資訊，請參閱 [Azure AD 中的應用程式和服務主體物件][AAD-APP-OBJECTS]。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-170">For more details on the relationship between an application's Application and Service Principal object(s), see [Application and service principal objects in Azure AD][AAD-APP-OBJECTS].</span></span>
* <span data-ttu-id="4e9dd-171">如需核心 Azure Active Directory (AD) 開發人員概念的一些定義，請參閱 [Azure AD 開發人員詞彙][AAD-DEVELOPER-GLOSSARY]。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-171">See the [Azure AD developer glossary][AAD-DEVELOPER-GLOSSARY] for definitions of some of the core Azure Active Directory (AD) developer concepts.</span></span>

<span data-ttu-id="4e9dd-172">請使用下方的註解區段來提供意見反應，並協助我們改善及設計我們的內容。</span><span class="sxs-lookup"><span data-stu-id="4e9dd-172">Please use the comments section below to provide feedback and help us refine and shape our content.</span></span>

<!--article references -->
[AAD-APP-OBJECTS]: active-directory-application-objects.md
[AAD-DEVELOPER-GLOSSARY]: active-directory-dev-glossary.md
[AAD-GROUPS-FOR-AUTHORIZATION]: http://www.dushyantgill.com/blog/2014/12/10/authorization-cloud-applications-using-ad-groups/
[ADD-UPD-RMV-APP]: active-directory-integrating-applications.md
[APPLICATION-ENTITY]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[APPLICATION-ENTITY-APP-ROLE]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#approle-type
[APPLICATION-ENTITY-OAUTH2-PERMISSION]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permission-type
[AZURE-PORTAL]: https://portal.azure.com
[DEV-GUIDE-TO-AUTH-WITH-ARM]: http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/
[GRAPH-API]: active-directory-graph-api.md
[IMPLICIT-GRANT]: active-directory-dev-understanding-oauth2-implicit-grant.md
[INTEGRATING-APPLICATIONS-AAD]: https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
[O365-PERM-DETAILS]: https://msdn.microsoft.com/office/office365/HowTo/application-manifest
[O365-SERVICE-DAEMON-APPS]: https://msdn.microsoft.com/office/office365/howto/building-service-apps-in-office-365
[RBAC-CLOUD-APPS-AZUREAD]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/

