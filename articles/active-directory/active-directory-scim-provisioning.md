---
title: "使用 System for Cross-Domain Identity Management 自動將使用者和群組從 Azure Active Directory 佈建到應用程式 | Microsoft Docs"
description: "Azure Active Directory 會利用 SCIM 通訊協定規格中定義的介面，自動佈建使用者和群組到 Web 服務前端的任何應用程式或身分識別存放區"
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 4d86f3dc-e2d3-4bde-81a3-4a0e092551c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.custom: aaddev;it-pro;oldportal
ms.openlocfilehash: 91978cee88d55c99bcb63c63cdaf01581ae84668
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="using-system-for-cross-domain-identity-management-to-automatically-provision-users-and-groups-from-azure-active-directory-to-applications"></a><span data-ttu-id="162c5-103">使用 System for Cross-Domain Identity Management 自動將使用者和群組從 Azure Active Directory 佈建到應用程式</span><span class="sxs-lookup"><span data-stu-id="162c5-103">Using System for Cross-Domain Identity Management to automatically provision users and groups from Azure Active Directory to applications</span></span>

## <a name="overview"></a><span data-ttu-id="162c5-104">概觀</span><span class="sxs-lookup"><span data-stu-id="162c5-104">Overview</span></span>
<span data-ttu-id="162c5-105">Azure Active Directory (Azure AD) 會利用 [System for Cross-Domain Identity Management (SCIM) 2.0 通訊協定規格](https://tools.ietf.org/html/draft-ietf-scim-api-19)中定義的介面，自動佈建使用者和群組到 Web 服務前端的任何應用程式或身分識別存放區。</span><span class="sxs-lookup"><span data-stu-id="162c5-105">Azure Active Directory (Azure AD) can automatically provision users and groups to any application or identity store that is fronted by a web service with the interface defined in the [System for Cross-Domain Identity Management (SCIM) 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span></span> <span data-ttu-id="162c5-106">Azure Active Directory 可以傳送要求以建立、修改或刪除指派給 Web 服務的使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="162c5-106">Azure Active Directory can send requests to create, modify, or delete assigned users and groups to the web service.</span></span> <span data-ttu-id="162c5-107">然後 Web 服務可以將這些要求轉譯成目標身分識別存放區上的作業。</span><span class="sxs-lookup"><span data-stu-id="162c5-107">The web service can then translate those requests into operations on the target identity store.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="162c5-108">Microsoft 建議您使用 Azure 入口網站中的 [Azure AD 系統管理中心](https://aad.portal.azure.com)來管理 Azure AD，而不要使用本文所提及的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="162c5-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 



<span data-ttu-id="162c5-109">![][0]
圖 1：透過 Web 服務從 Azure Active Directory 佈建到身分識別存放區</span><span class="sxs-lookup"><span data-stu-id="162c5-109">![][0]
*Figure 1: Provisioning from Azure Active Directory to an identity store via a web service*</span></span>

<span data-ttu-id="162c5-110">這項功能可搭配 Azure AD 中的「自備應用程式」功能，以為提供 SCIM Web 服務或位於該服務後端的應用程式啟用單一登入和自動使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="162c5-110">This capability can be used in conjunction with the “bring your own app” capability in Azure AD to enable single sign-on and automatic user provisioning for applications that provide or are fronted by a SCIM web service.</span></span>

<span data-ttu-id="162c5-111">在 Azure Active Directory 中使用 SCIM 有兩個使用案例：</span><span class="sxs-lookup"><span data-stu-id="162c5-111">There are two use cases for using SCIM in Azure Active Directory:</span></span>

* <span data-ttu-id="162c5-112">**將使用者與群組佈建至支援 SCIM 的應用程式** - 應用程式若支援 SCIM 2.0，而且使用 OAuth 持有人權杖進行驗證，將可直接與 Azure AD 搭配運作，不需其他設定。</span><span class="sxs-lookup"><span data-stu-id="162c5-112">**Provisioning users and groups to applications that support SCIM** Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication works with Azure AD without configuration.</span></span>
* <span data-ttu-id="162c5-113">**為支援其他 API 型佈建的應用程式建置您自己的佈建解決方案** - 對於非 SCIM 應用程式，您可以建立能夠在 Azure AD SCIM 端點與應用程式為使用者佈建支援的任何 API 之間進行轉譯的 SCIM 端點。</span><span class="sxs-lookup"><span data-stu-id="162c5-113">**Build your own provisioning solution for applications that support other API-based provisioning** For non-SCIM applications, you can create a SCIM endpoint to translate between the Azure AD SCIM endpoint and any API the application supports for user provisioning.</span></span> <span data-ttu-id="162c5-114">為了協助您開發 SCIM 端點，我們連同程式碼範例提供了通用語言基礎結構 (CLI) 程式庫，為您說明如何提供 SCIM 端點及轉譯 SCIM 訊息。</span><span class="sxs-lookup"><span data-stu-id="162c5-114">To help you develop a SCIM endpoint, we provide Common Language Infrastructure (CLI) libraries along with code samples that show you how to do provide a SCIM endpoint and translate SCIM messages.</span></span>  

## <a name="provisioning-users-and-groups-to-applications-that-support-scim"></a><span data-ttu-id="162c5-115">將使用者與群組佈建至支援 SCIM 的應用程式</span><span class="sxs-lookup"><span data-stu-id="162c5-115">Provisioning users and groups to applications that support SCIM</span></span>
<span data-ttu-id="162c5-116">Azure AD 可以設定為將已指派的使用者和群組佈建至實作 [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) Web 服務、並接受以 OAuth 持有人權杖進行驗證的應用程式。</span><span class="sxs-lookup"><span data-stu-id="162c5-116">Azure AD can be configured to automatically provision assigned users and groups to applications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web service and accept OAuth bearer tokens for authentication.</span></span> <span data-ttu-id="162c5-117">在 SCIM 2.0 規格中，應用程式必須符合下列需求：</span><span class="sxs-lookup"><span data-stu-id="162c5-117">Within the SCIM 2.0 specification, applications must meet these requirements:</span></span>

* <span data-ttu-id="162c5-118">支援根據 SCIM 通訊協定 3.3 小節建立使用者和 (或) 群組的作業。</span><span class="sxs-lookup"><span data-stu-id="162c5-118">Supports creating users and/or groups, as per section 3.3 of the SCIM protocol.</span></span>  
* <span data-ttu-id="162c5-119">支援根據 SCIM 通訊協定 3.5.2 小節修改具有修補要求的使用者和 (或) 群組的作業。</span><span class="sxs-lookup"><span data-stu-id="162c5-119">Supports modifying users and/or groups with patch requests as per section 3.5.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="162c5-120">支援根據 SCIM 通訊協定 3.4.1 小節擷取已知資源的作業。</span><span class="sxs-lookup"><span data-stu-id="162c5-120">Supports retrieving a known resource as per section 3.4.1 of the SCIM protocol.</span></span>  
* <span data-ttu-id="162c5-121">支援根據 SCIM 通訊協定 3.4.2 小節查詢使用者和 (或) 群組的作業。</span><span class="sxs-lookup"><span data-stu-id="162c5-121">Supports querying users and/or groups, as per section 3.4.2 of the SCIM protocol.</span></span>  <span data-ttu-id="162c5-122">依預設會依 externalId 來查詢使用者，並依 displayName 查詢群組。</span><span class="sxs-lookup"><span data-stu-id="162c5-122">By default, users are queried by externalId and groups are queried by displayName.</span></span>  
* <span data-ttu-id="162c5-123">支援根據 SCIM 通訊協定 3.4.2 小節，依 ID 和管理員查詢使用者的作業。</span><span class="sxs-lookup"><span data-stu-id="162c5-123">Supports querying user by ID and by manager as per section 3.4.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="162c5-124">支援根據 SCIM 通訊協定 3.4.2 小節，依 ID 和成員查詢群組的作業。</span><span class="sxs-lookup"><span data-stu-id="162c5-124">Supports querying groups by ID and by member as per section 3.4.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="162c5-125">接受根據 SCIM 通訊協定 2.1 小節以 OAuth 持有人權杖進行授權的作法。</span><span class="sxs-lookup"><span data-stu-id="162c5-125">Accepts OAuth bearer tokens for authorization as per section 2.1 of the SCIM protocol.</span></span>

<span data-ttu-id="162c5-126">洽詢應用程式提供者，或參閱應用程式提供者文件中的相關陳述，以了解是否符合這些需求。</span><span class="sxs-lookup"><span data-stu-id="162c5-126">Check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span></span>

### <a name="getting-started"></a><span data-ttu-id="162c5-127">開始使用</span><span class="sxs-lookup"><span data-stu-id="162c5-127">Getting started</span></span>
<span data-ttu-id="162c5-128">支援本文所述 SCIM 設定檔的應用程式，可使用 Azure AD 應用程式庫中的「不在資源庫內的應用程式」功能連線到 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="162c5-128">Applications that support the SCIM profile described in this article can be connected to Azure Active Directory using the "non-gallery application" feature in the Azure AD application gallery.</span></span> <span data-ttu-id="162c5-129">連線之後，Azure AD 會每隔 20 分鐘執行一次同步處理程序，此程序會為指派的使用者和群組查詢應用程式的 SCIM 端點，並根據指派詳細資料加以建立或修改。</span><span class="sxs-lookup"><span data-stu-id="162c5-129">Once connected, Azure AD runs a synchronization process every 20 minutes where it queries the application's SCIM endpoint for assigned users and groups, and creates or modifies them according to the assignment details.</span></span>

<span data-ttu-id="162c5-130">**若要連接支援 SCIM 的應用程式：**</span><span class="sxs-lookup"><span data-stu-id="162c5-130">**To connect an application that supports SCIM:**</span></span>

1. <span data-ttu-id="162c5-131">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="162c5-131">Sign in to [the Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="162c5-132">瀏覽至 **Azure Active Directory > 企業應用程式，然後選取 [	新增應用程式] > [全部] > [不在資源庫內的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="162c5-132">Browse to **Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="162c5-133">輸入您的應用程式名稱，然後按一下 [新增] 圖示，以建立應用程式物件。</span><span class="sxs-lookup"><span data-stu-id="162c5-133">Enter a name for your application, and click **Add** icon to create an app object.</span></span>
    
  <span data-ttu-id="162c5-134">![][1]
  圖 2：使用 Azure AD 應用程式庫</span><span class="sxs-lookup"><span data-stu-id="162c5-134">![][1]
*Figure 2: Azure AD application gallery*</span></span>
    
4. <span data-ttu-id="162c5-135">在結果畫面中，選取左側資料行中的 [佈建] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="162c5-135">In the resulting screen, select the **Provisioning** tab in the left column.</span></span>
5. <span data-ttu-id="162c5-136">在 [佈建模式] 功能表上，選取 [自動]。</span><span class="sxs-lookup"><span data-stu-id="162c5-136">In the **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="162c5-137">![][2]
  圖 3：在 Azure 入口網站中設定佈建</span><span class="sxs-lookup"><span data-stu-id="162c5-137">![][2]
*Figure 3: Configuring provisioning in the Azure portal*</span></span>
    
6. <span data-ttu-id="162c5-138">在 [租用戶 URL] 欄位中，輸入應用程式 SCIM 端點的 URL。</span><span class="sxs-lookup"><span data-stu-id="162c5-138">In the **Tenant URL** field, enter the URL of the application's SCIM endpoint.</span></span> <span data-ttu-id="162c5-139">範例：https://api.contoso.com/scim/v2/</span><span class="sxs-lookup"><span data-stu-id="162c5-139">Example: https://api.contoso.com/scim/v2/</span></span>
7. <span data-ttu-id="162c5-140">如果 SCIM 端點需要來自非 Azure AD 簽發者的 OAuth 持有人權杖，那麼便將所需的 OAuth 持有人權杖複製到選擇性 [祕密權杖] 欄位。</span><span class="sxs-lookup"><span data-stu-id="162c5-140">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the optional **Secret Token** field.</span></span> <span data-ttu-id="162c5-141">如果此欄位保留空白，則 Azure AD 會在每個要求包含從 Azure AD 簽發的 OAuth 持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="162c5-141">If this field is left blank, then Azure AD included an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="162c5-142">使用 Azure AD 作為識別提供者的應用程式，可以驗證此 Azure AD 簽發的權杖。</span><span class="sxs-lookup"><span data-stu-id="162c5-142">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="162c5-143">按一下 [測試連線] 按鈕，讓 Azure Active Directory 嘗試連線到 SCIM 端點。</span><span class="sxs-lookup"><span data-stu-id="162c5-143">Click the **Test Connection** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span></span> <span data-ttu-id="162c5-144">如果嘗試失敗，則會顯示錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="162c5-144">If the attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="162c5-145">如果嘗試連線到應用程式成功，則按一下 [儲存] 以儲存管理員認證。</span><span class="sxs-lookup"><span data-stu-id="162c5-145">If the attempts to connect to the application succeed, then click **Save** to save the admin credentials.</span></span>
10. <span data-ttu-id="162c5-146">在 [對應] 區段中，有兩組可選取的屬性對應：一個用於使用者物件，一個用於群組物件。</span><span class="sxs-lookup"><span data-stu-id="162c5-146">In the **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="162c5-147">選取其中一個以檢閱從 Azure Active Directory 同步處理至應用程式的屬性。</span><span class="sxs-lookup"><span data-stu-id="162c5-147">Select each one to review the attributes that are synchronized from Azure Active Directory to your app.</span></span> <span data-ttu-id="162c5-148">選取為 [比對] 屬性的屬性會用來比對應用程式中的使用者和群組以進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="162c5-148">The attributes selected as **Matching** properties are used to match the users and groups in your app for update operations.</span></span> <span data-ttu-id="162c5-149">選取 [儲存] 按鈕以認可任何變更。</span><span class="sxs-lookup"><span data-stu-id="162c5-149">Select the Save button to commit any changes.</span></span>

    >[!NOTE]
    ><span data-ttu-id="162c5-150">您可以選擇性地藉由停用「群組」對應以停用同步處理群組物件。</span><span class="sxs-lookup"><span data-stu-id="162c5-150">You can optionally disable syncing of group objects by disabling the "groups" mapping.</span></span> 

11. <span data-ttu-id="162c5-151">在 [設定] 底下的 [範圍] 欄位定義哪些使用者或群組會進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="162c5-151">Under **Settings**, the **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="162c5-152">選取 [僅同步處理指派的使用者和群組]\(建議選項) 只會同步處理 [使用者和群組] 索引標籤中指派的使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="162c5-152">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in the **Users and groups** tab.</span></span>
12. <span data-ttu-id="162c5-153">一旦您的設定完成，請將 [佈建狀態] 變更為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="162c5-153">Once your configuration is complete, change the **Provisioning Status** to **On**.</span></span>
13. <span data-ttu-id="162c5-154">按一下 [儲存] 以啟動 Azure AD 佈建服務。</span><span class="sxs-lookup"><span data-stu-id="162c5-154">Click **Save** to start the Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="162c5-155">如果僅同步處理指派的使用者和群組 (建議選項)，請務必選取 [使用者和群組] 索引標籤，並且指派您想要同步處理的使用者和/或群組。</span><span class="sxs-lookup"><span data-stu-id="162c5-155">If syncing only assigned users and groups (recommended), be sure to select the **Users and groups** tab and assign the users and/or groups you wish to sync.</span></span>

<span data-ttu-id="162c5-156">一旦啟動初始同步處理，您可以使用 [稽核記錄] 索引標籤以監視進度，進步會顯示佈建服務在您的應用程式上執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="162c5-156">Once the initial synchronization has started, you can use the **Audit logs** tab to monitor progress, which shows all actions performed by the provisioning service on your app.</span></span> <span data-ttu-id="162c5-157">如需如何讀取 Azure AD 佈建記錄的詳細資訊，請參閱[關於使用者帳戶自動佈建的報告](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)。</span><span class="sxs-lookup"><span data-stu-id="162c5-157">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

>[!NOTE]
><span data-ttu-id="162c5-158">初始同步處理會比後續的同步處理花費較多時間執行，只要服務正在執行，大約每 20 分鐘便會發生一次。</span><span class="sxs-lookup"><span data-stu-id="162c5-158">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> 


## <a name="building-your-own-provisioning-solution-for-any-application"></a><span data-ttu-id="162c5-159">為任何應用程式建置您自己的佈建解決方案</span><span class="sxs-lookup"><span data-stu-id="162c5-159">Building your own provisioning solution for any application</span></span>
<span data-ttu-id="162c5-160">建立可與 Azure Active Directory 互動的 SCIM Web 服務後，您即可為提供 REST 或 SOAP 使用者佈建 API 的絕大多數應用程式啟用單一登入和自動使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="162c5-160">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span></span>

<span data-ttu-id="162c5-161">其運作方式如下：</span><span class="sxs-lookup"><span data-stu-id="162c5-161">Here’s how it works:</span></span>

1. <span data-ttu-id="162c5-162">Azure AD 提供名為 [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/)的通用語言基礎結構程式庫。</span><span class="sxs-lookup"><span data-stu-id="162c5-162">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span></span> <span data-ttu-id="162c5-163">系統整合業者和開發人員可以使用此程式庫來建立及部署能夠將 Azure AD 連線到任何應用程式的身分識別存放區的 SCIM 式 Web 服務端點。</span><span class="sxs-lookup"><span data-stu-id="162c5-163">System integrators and developers can use this library to create and deploy a SCIM-based web service endpoint capable of connecting Azure AD to any application’s identity store.</span></span>
2. <span data-ttu-id="162c5-164">對應會在 Web 服務中實作，以將標準的使用者結構描述對應到使用者結構描述和應用程式所需的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="162c5-164">Mappings are implemented in the web service to map the standardized user schema to the user schema and protocol required by the application.</span></span>
3. <span data-ttu-id="162c5-165">端點 URL 會在 Azure AD 中註冊，作為應用程式資源庫中自訂應用程式的一部分。</span><span class="sxs-lookup"><span data-stu-id="162c5-165">The endpoint URL is registered in Azure AD as part of a custom application in the application gallery.</span></span>
4. <span data-ttu-id="162c5-166">使用者和群組會在 Azure AD 中指派給此應用程式。</span><span class="sxs-lookup"><span data-stu-id="162c5-166">Users and groups are assigned to this application in Azure AD.</span></span> <span data-ttu-id="162c5-167">指派時，它們會被放入佇列，以同步處理至目標應用程式。</span><span class="sxs-lookup"><span data-stu-id="162c5-167">Upon assignment, they are put into a queue to be synchronized to the target application.</span></span> <span data-ttu-id="162c5-168">同步處理程序會每隔 20 分鐘處理佇列的執行。</span><span class="sxs-lookup"><span data-stu-id="162c5-168">The synchronization process handling the queue runs every 20 minutes.</span></span>

### <a name="code-samples"></a><span data-ttu-id="162c5-169">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="162c5-169">Code Samples</span></span>
<span data-ttu-id="162c5-170">為了讓這個程序更簡單，我們提供了一組 [程式碼範例](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) ，該範例會建立 SCIM Web 服務端點並示範自動佈建。</span><span class="sxs-lookup"><span data-stu-id="162c5-170">To make this process easier, a set of [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span></span> <span data-ttu-id="162c5-171">其中一個範例是維護代表使用者和群組、具有逗號分隔值資料列檔案的提供者。</span><span class="sxs-lookup"><span data-stu-id="162c5-171">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span></span>  <span data-ttu-id="162c5-172">另一個是在 Amazon Web 服務身分識別與存取管理服務上運作的提供者。</span><span class="sxs-lookup"><span data-stu-id="162c5-172">The other is of a provider that operates on the Amazon Web Services Identity and Access Management service.</span></span>  

<span data-ttu-id="162c5-173">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="162c5-173">**Prerequisites**</span></span>

* <span data-ttu-id="162c5-174">Visual Studio 2013 或更新版本</span><span class="sxs-lookup"><span data-stu-id="162c5-174">Visual Studio 2013 or later</span></span>
* [<span data-ttu-id="162c5-175">Azure SDK for .NET</span><span class="sxs-lookup"><span data-stu-id="162c5-175">Azure SDK for .NET</span></span>](https://azure.microsoft.com/downloads/)
* <span data-ttu-id="162c5-176">支援將 ASP.NET Framework 4.5 用作 SCIM 端點的 Windows 電腦。</span><span class="sxs-lookup"><span data-stu-id="162c5-176">Windows machine that supports the ASP.NET framework 4.5 to be used as the SCIM endpoint.</span></span> <span data-ttu-id="162c5-177">必須能夠自雲端存取這台電腦</span><span class="sxs-lookup"><span data-stu-id="162c5-177">This machine must be accessible from the cloud</span></span>
* [<span data-ttu-id="162c5-178">具有 Azure AD Premium 試用版或授權版的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="162c5-178">An Azure subscription with a trial or licensed version of Azure AD Premium</span></span>](https://azure.microsoft.com/services/active-directory/)
* <span data-ttu-id="162c5-179">Amazon AWS 範例需要來自 [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html)的程式庫。</span><span class="sxs-lookup"><span data-stu-id="162c5-179">The Amazon AWS sample requires libraries from the [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span></span> <span data-ttu-id="162c5-180">如需詳細資訊，請參閱範例隨附的讀我檔案。</span><span class="sxs-lookup"><span data-stu-id="162c5-180">For more information, see the README file included with the sample.</span></span>

### <a name="getting-started"></a><span data-ttu-id="162c5-181">開始使用</span><span class="sxs-lookup"><span data-stu-id="162c5-181">Getting Started</span></span>
<span data-ttu-id="162c5-182">實作可以接受來自 Azure AD 的佈建要求的 SCIM 端點的最簡單的方式是建置和部署會將佈建的使用者輸出至以逗號分隔值 (CSV) 檔案的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="162c5-182">The easiest way to implement a SCIM endpoint that can accept provisioning requests from Azure AD is to build and deploy the code sample that outputs the provisioned users to a comma-separated value (CSV) file.</span></span>

<span data-ttu-id="162c5-183">**若要建立範例 SCIM 端點：**</span><span class="sxs-lookup"><span data-stu-id="162c5-183">**To create a sample SCIM endpoint:**</span></span>

1. <span data-ttu-id="162c5-184">在 [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span><span class="sxs-lookup"><span data-stu-id="162c5-184">Download the code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span></span>
2. <span data-ttu-id="162c5-185">將套件解壓縮並將放在 Windows 電腦上的位置，例如 C:\AzureAD-BYOA-Provisioning-Samples\。</span><span class="sxs-lookup"><span data-stu-id="162c5-185">Unzip the package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span></span>
3. <span data-ttu-id="162c5-186">在此資料夾中，於 Visual Studio 中啟動 FileProvisioningAgent 方案。</span><span class="sxs-lookup"><span data-stu-id="162c5-186">In this folder, launch the FileProvisioningAgent solution in Visual Studio.</span></span>
4. <span data-ttu-id="162c5-187">選取 [工具] > [程式庫套件管理員] > [套件管理員主控台]，然後執行以下命令，讓 FileProvisioningAgent 專案解析方案參考：</span><span class="sxs-lookup"><span data-stu-id="162c5-187">Select **Tools > Library Package Manager > Package Manager Console**, and execute the following commands for the FileProvisioningAgent project to resolve the solution references:</span></span>
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. <span data-ttu-id="162c5-188">建置 FileProvisioningAgent 專案。</span><span class="sxs-lookup"><span data-stu-id="162c5-188">Build the FileProvisioningAgent project.</span></span>
6. <span data-ttu-id="162c5-189">在 Windows 中啟動「命令提示字元」應用程式 (以系統管理員身分)，然後使用 **cd** 命令將目錄變更為您的 **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="162c5-189">Launch the Command Prompt application in Windows (as an Administrator), and use the **cd** command to change the directory to your **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folder.</span></span>
7. <span data-ttu-id="162c5-190">執行以下命令，以 Windows 電腦的 IP 位址或網域名稱取代 <ip-address>：</span><span class="sxs-lookup"><span data-stu-id="162c5-190">Run the following command, replacing <ip-address> with the IP address or domain name of the Windows machine:</span></span>
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. <span data-ttu-id="162c5-191">在 Windows 中，於 [Windows 設定] > [網路和網際網路設定] 底下，選取 [Windows 防火牆] > [進階設定]，然後建立允許對連接埠 9000 進行輸入存取的「輸入規則」。</span><span class="sxs-lookup"><span data-stu-id="162c5-191">In Windows under **Windows Settings > Network & Internet Settings**, select the **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access to port 9000.</span></span>
9. <span data-ttu-id="162c5-192">如果 Windows 電腦位於路由器背後，必須將路由器設定為在公開到網際網路的連接埠 9000 和 Windows 電腦上的連接埠 9000 之間執行網路存取轉譯。</span><span class="sxs-lookup"><span data-stu-id="162c5-192">If the Windows machine is behind a router, the router needs to be configured to perform Network Access Translation between its port 9000 that is exposed to the internet, and port 9000 on the Windows machine.</span></span> <span data-ttu-id="162c5-193">為了讓 Azure AD 能夠在雲端中存取這個端點，這是必要的。</span><span class="sxs-lookup"><span data-stu-id="162c5-193">This is required for Azure AD to be able to access this endpoint in the cloud.</span></span>

<span data-ttu-id="162c5-194">**若要在 Azure AD 中註冊範例 SCIM 端點：**</span><span class="sxs-lookup"><span data-stu-id="162c5-194">**To register the sample SCIM endpoint in Azure AD:**</span></span>

1. <span data-ttu-id="162c5-195">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="162c5-195">Sign in to [the Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="162c5-196">瀏覽至 **Azure Active Directory > 企業應用程式，然後選取 [	新增應用程式] > [全部] > [不在資源庫內的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="162c5-196">Browse to **Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="162c5-197">輸入您的應用程式名稱，然後按一下 [新增] 圖示，以建立應用程式物件。</span><span class="sxs-lookup"><span data-stu-id="162c5-197">Enter a name for your application, and click **Add** icon to create an app object.</span></span> <span data-ttu-id="162c5-198">建立的應用程式物件要代表您要佈建和實作登一登入的目標應用程式，而不只是 SCIM 端點。</span><span class="sxs-lookup"><span data-stu-id="162c5-198">The application object created is intended to represent the target app you would be provisioning to and implementing single sign-on for, and not just the SCIM endpoint.</span></span>
4. <span data-ttu-id="162c5-199">在結果畫面中，選取左側資料行中的 [佈建] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="162c5-199">In the resulting screen, select the **Provisioning** tab in the left column.</span></span>
5. <span data-ttu-id="162c5-200">在 [佈建模式] 功能表上，選取 [自動]。</span><span class="sxs-lookup"><span data-stu-id="162c5-200">In the **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="162c5-201">![][2]
  圖 4：在 Azure 入口網站中設定佈建</span><span class="sxs-lookup"><span data-stu-id="162c5-201">![][2]
*Figure 4: Configuring provisioning in the Azure portal*</span></span>
    
6. <span data-ttu-id="162c5-202">在 [租用戶 URL] 欄位中，輸入網際網路公開的 URL 和 SCIM 端點的連接埠。</span><span class="sxs-lookup"><span data-stu-id="162c5-202">In the **Tenant URL** field, enter the internet-exposed URL and port of your SCIM endpoint.</span></span> <span data-ttu-id="162c5-203">這看起來會像 http://testmachine.contoso.com:9000 或 http://<ip-address>:9000/，其中 <ip-address> 是網際網路公開 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="162c5-203">This would be something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is the internet exposed IP address.</span></span>  
7. <span data-ttu-id="162c5-204">如果 SCIM 端點需要來自非 Azure AD 簽發者的 OAuth 持有人權杖，那麼便將所需的 OAuth 持有人權杖複製到選擇性 [祕密權杖] 欄位。</span><span class="sxs-lookup"><span data-stu-id="162c5-204">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the optional **Secret Token** field.</span></span> <span data-ttu-id="162c5-205">如果此欄位保留空白，則 Azure AD 將在每個要求包含從 Azure AD 簽發的 OAuth 持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="162c5-205">If this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="162c5-206">使用 Azure AD 作為識別提供者的應用程式，可以驗證此 Azure AD 簽發的權杖。</span><span class="sxs-lookup"><span data-stu-id="162c5-206">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="162c5-207">按一下 [測試連線] 按鈕，讓 Azure Active Directory 嘗試連線到 SCIM 端點。</span><span class="sxs-lookup"><span data-stu-id="162c5-207">Click the **Test Connection** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span></span> <span data-ttu-id="162c5-208">如果嘗試失敗，則會顯示錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="162c5-208">If the attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="162c5-209">如果嘗試連線到應用程式成功，則按一下 [儲存] 以儲存管理員認證。</span><span class="sxs-lookup"><span data-stu-id="162c5-209">If the attempts to connect to the application succeed, then click **Save** to save the admin credentials.</span></span>
10. <span data-ttu-id="162c5-210">在 [對應] 區段中，有兩組可選取的屬性對應：一個用於使用者物件，一個用於群組物件。</span><span class="sxs-lookup"><span data-stu-id="162c5-210">In the **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="162c5-211">選取其中一個以檢閱從 Azure Active Directory 同步處理至應用程式的屬性。</span><span class="sxs-lookup"><span data-stu-id="162c5-211">Select each one to review the attributes that are synchronized from Azure Active Directory to your app.</span></span> <span data-ttu-id="162c5-212">選取為 [比對] 屬性的屬性會用來比對應用程式中的使用者和群組以進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="162c5-212">The attributes selected as **Matching** properties are used to match the users and groups in your app for update operations.</span></span> <span data-ttu-id="162c5-213">選取 [儲存] 按鈕以認可任何變更。</span><span class="sxs-lookup"><span data-stu-id="162c5-213">Select the Save button to commit any changes.</span></span>
11. <span data-ttu-id="162c5-214">在 [設定] 底下的 [範圍] 欄位定義哪些使用者或群組會進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="162c5-214">Under **Settings**, the **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="162c5-215">選取 [僅同步處理指派的使用者和群組]\(建議選項) 只會同步處理 [使用者和群組] 索引標籤中指派的使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="162c5-215">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in the **Users and groups** tab.</span></span>
12. <span data-ttu-id="162c5-216">一旦您的設定完成，請將 [佈建狀態] 變更為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="162c5-216">Once your configuration is complete, change the **Provisioning Status** to **On**.</span></span>
13. <span data-ttu-id="162c5-217">按一下 [儲存] 以啟動 Azure AD 佈建服務。</span><span class="sxs-lookup"><span data-stu-id="162c5-217">Click **Save** to start the Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="162c5-218">如果僅同步處理指派的使用者和群組 (建議選項)，請務必選取 [使用者和群組] 索引標籤，並且指派您想要同步處理的使用者和/或群組。</span><span class="sxs-lookup"><span data-stu-id="162c5-218">If syncing only assigned users and groups (recommended), be sure to select the **Users and groups** tab and assign the users and/or groups you wish to sync.</span></span>

<span data-ttu-id="162c5-219">一旦啟動初始同步處理，您可以使用 [稽核記錄] 索引標籤以監視進度，進步會顯示佈建服務在您的應用程式上執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="162c5-219">Once the initial synchronization has started, you can use the **Audit logs** tab to monitor progress, which shows all actions performed by the provisioning service on your app.</span></span> <span data-ttu-id="162c5-220">如需如何讀取 Azure AD 佈建記錄的詳細資訊，請參閱[關於使用者帳戶自動佈建的報告](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)。</span><span class="sxs-lookup"><span data-stu-id="162c5-220">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

<span data-ttu-id="162c5-221">確認此範例的最後一個步驟是開啟 Windows 電腦上 \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug 資料夾中的 TargetFile.csv 檔案。</span><span class="sxs-lookup"><span data-stu-id="162c5-221">The final step in verifying the sample is to open the TargetFile.csv file in the \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span></span> <span data-ttu-id="162c5-222">一旦執行佈建程序，此檔案會顯示所有指派和佈建的使用者和群組的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="162c5-222">Once the provisioning process is run, this file shows the details of all assigned and provisioned users and groups.</span></span>

### <a name="development-libraries"></a><span data-ttu-id="162c5-223">開發程式庫</span><span class="sxs-lookup"><span data-stu-id="162c5-223">Development libraries</span></span>
<span data-ttu-id="162c5-224">若要開發自己符合 SCIM 規格的 Web 服務，請先熟悉下列 Microsoft 所提供、有助於加速開發程序的程式庫：</span><span class="sxs-lookup"><span data-stu-id="162c5-224">To develop your own web service that conforms to the SCIM specification, first familiarize yourself with the following libraries provided by Microsoft to help accelerate the development process:</span></span> 

1. <span data-ttu-id="162c5-225">提供通用語言基礎結構 (CLI) 程式庫，可與以該基礎結構為基礎的語言 (例如 C#) 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="162c5-225">Common Language Infrastructure (CLI) libraries are offered for use with languages based on that infrastructure, such as C#.</span></span> <span data-ttu-id="162c5-226">其中一個程式庫，[Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/)，會宣告介面 (Microsoft.SystemForCrossDomainIdentityManagement.IProvider)，如下圖所示：使用程式庫的開發人員會以參考 (通常是作為提供者) 的類別來實作該介面。</span><span class="sxs-lookup"><span data-stu-id="162c5-226">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in the following illustration:  A developer using the libraries would implement that interface with a class that may be referred to, generically, as a provider.</span></span> <span data-ttu-id="162c5-227">程式庫可讓開發人員部署符合 SCIM 規格的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="162c5-227">The libraries enable the developer to deploy a web service that conforms to the SCIM specification.</span></span> <span data-ttu-id="162c5-228">Web 服務可以裝載在 Internet Information Services 或任何可執行的通用語言基礎結構組件。</span><span class="sxs-lookup"><span data-stu-id="162c5-228">The web service can be either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span></span> <span data-ttu-id="162c5-229">要求會轉譯成對提供者的方法呼叫，該呼叫會由開發人員以程式方式設計，以對某些身分識別存放區進行操作。</span><span class="sxs-lookup"><span data-stu-id="162c5-229">Request is translated into calls to the provider’s methods, which would be programmed by the developer to operate on some identity store.</span></span>
  
  ![][3]
  
2. <span data-ttu-id="162c5-230">[ExpressRoute 處理常式](http://expressjs.com/guide/routing.html)可剖析代表對 node.js Web 服務發出之呼叫 (如 SCIM 規格所定義) 的 node.js 要求物件。</span><span class="sxs-lookup"><span data-stu-id="162c5-230">[Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by the SCIM specification), made to a node.js web service.</span></span>   

### <a name="building-a-custom-scim-endpoint"></a><span data-ttu-id="162c5-231">建置自訂 SCIM 端點</span><span class="sxs-lookup"><span data-stu-id="162c5-231">Building a Custom SCIM Endpoint</span></span>
<span data-ttu-id="162c5-232">使用 CLI 程式庫，使用這些程式庫的開發人員可以將其服務託管在任何可執行的通用語言基礎結構組件內，或在網際網路資訊服務內。</span><span class="sxs-lookup"><span data-stu-id="162c5-232">Using the CLI libraries, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span></span> <span data-ttu-id="162c5-233">以下是範例程式碼，此程式碼可將服務裝載於位於位址 http://localhost:9000 的可執行組件內：</span><span class="sxs-lookup"><span data-stu-id="162c5-233">Here is sample code for hosting a service within an executable assembly, at the address http://localhost:9000:</span></span> 

    private static void Main(string[] arguments)
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IProvider and 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
      new DevelopersMonitor();
    Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
      new DevelopersProvider(arguments[1]);
    Microsoft.SystemForCrossDomainIdentityManagement.Service webService = null;
    try
    {
        webService = new WebService(monitor, provider);
        webService.Start("http://localhost:9000");

        Console.ReadKey(true);
    }
    finally
    {
        if (webService != null)
        {
            webService.Dispose();
            webService = null;
        }
    }
    }

    public class WebService : Microsoft.SystemForCrossDomainIdentityManagement.Service
    {
    private Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor;
    private Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider;

    public WebService(
      Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitoringBehavior, 
      Microsoft.SystemForCrossDomainIdentityManagement.IProvider providerBehavior)
    {
        this.monitor = monitoringBehavior;
        this.provider = providerBehavior;
    }

    public override IMonitor MonitoringBehavior
    {
        get
        {
            return this.monitor;
        }

        set
        {
            this.monitor = value;
        }
    }

    public override IProvider ProviderBehavior
    {
        get
        {
            return this.provider;
        }

        set
        {
            this.provider = value;
        }
    }
    }

<span data-ttu-id="162c5-234">這項服務必須具有 HTTP 位址，而其伺服器驗證憑證的根憑證授權單位是下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="162c5-234">This service must have an HTTP address and server authentication certificate of which the root certification authority is one of the following:</span></span> 

* <span data-ttu-id="162c5-235">CNNIC</span><span class="sxs-lookup"><span data-stu-id="162c5-235">CNNIC</span></span>
* <span data-ttu-id="162c5-236">Comodo</span><span class="sxs-lookup"><span data-stu-id="162c5-236">Comodo</span></span>
* <span data-ttu-id="162c5-237">CyberTrust</span><span class="sxs-lookup"><span data-stu-id="162c5-237">CyberTrust</span></span>
* <span data-ttu-id="162c5-238">DigiCert</span><span class="sxs-lookup"><span data-stu-id="162c5-238">DigiCert</span></span>
* <span data-ttu-id="162c5-239">GeoTrust</span><span class="sxs-lookup"><span data-stu-id="162c5-239">GeoTrust</span></span>
* <span data-ttu-id="162c5-240">GlobalSign</span><span class="sxs-lookup"><span data-stu-id="162c5-240">GlobalSign</span></span>
* <span data-ttu-id="162c5-241">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="162c5-241">Go Daddy</span></span>
* <span data-ttu-id="162c5-242">Verisign</span><span class="sxs-lookup"><span data-stu-id="162c5-242">Verisign</span></span>
* <span data-ttu-id="162c5-243">WoSign</span><span class="sxs-lookup"><span data-stu-id="162c5-243">WoSign</span></span>

<span data-ttu-id="162c5-244">伺服器驗證憑證可以使用網路殼層公用程式繫結到 Windows 主機上的連接埠：</span><span class="sxs-lookup"><span data-stu-id="162c5-244">A server authentication certificate can be bound to a port on a Windows host using the network shell utility:</span></span> 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

<span data-ttu-id="162c5-245">此處，對 certhash 引數提供的值為憑證指紋，而對 appid 引數提供的值為任意的全域唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="162c5-245">Here, the value provided for the certhash argument is the thumbprint of the certificate, while the value provided for the appid argument is an arbitrary globally unique identifier.</span></span>  

<span data-ttu-id="162c5-246">若要將服務託管在網際網路資訊服務內，開發人員會建置 CLA 程式碼程式庫組件，並在組件的預設命名空間中使用名為 Startup 的類別。</span><span class="sxs-lookup"><span data-stu-id="162c5-246">To host the service within Internet Information Services, a developer would build a CLA code library assembly with a class named Startup in the default namespace of the assembly.</span></span>  <span data-ttu-id="162c5-247">以下是這種類別的範例：</span><span class="sxs-lookup"><span data-stu-id="162c5-247">Here is a sample of such a class:</span></span> 

    public class Startup
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor and  
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter starter;

    public Startup()
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
          new DevelopersMonitor();
        Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
          new DevelopersProvider();
        this.starter = 
          new Microsoft.SystemForCrossDomainIdentityManagement.WebApplicationStarter(
            provider, 
            monitor);
    }

    public void Configuration(
      Owin.IAppBuilder builder) // Defined in in Owin.dll.  
    {
        this.starter.ConfigureApplication(builder);
    }
    }

### <a name="handling-endpoint-authentication"></a><span data-ttu-id="162c5-248">處理端點驗證</span><span class="sxs-lookup"><span data-stu-id="162c5-248">Handling endpoint authentication</span></span>
<span data-ttu-id="162c5-249">來自 Azure Active Directory 的要求包括 OAuth 2.0 持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="162c5-249">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span></span>   <span data-ttu-id="162c5-250">接收要求的任何服務應該代表預期的 Azure Active Directory 租用戶，將簽發者驗證為 Azure Active Directory，以存取 Azure Active Directory 圖形 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="162c5-250">Any service receiving the request should authenticate the issuer as being Azure Active Directory on behalf of the expected Azure Active Directory tenant, for access to the Azure Active Directory Graph web service.</span></span>  <span data-ttu-id="162c5-251">在 Token 中，簽發者是由 iss 宣告，例如："iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/"。</span><span class="sxs-lookup"><span data-stu-id="162c5-251">In the token, the issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span></span>  <span data-ttu-id="162c5-252">在此範例中，宣告值的基礎位址 https://sts.windows.net 會將 Azure Active Directory 識別為簽發者，而相對位址區段 cbb1a5ac-f33b-45fa-9bf5-f37db0fed422 則是簽發權杖時所代表之 Azure Active Directory 租用戶的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="162c5-252">In this example, the base address of the claim value, https://sts.windows.net, identifies Azure Active Directory as the issuer, while the relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of the Azure Active Directory tenant on behalf of which the token was issued.</span></span>  <span data-ttu-id="162c5-253">如果發出的權杖要用於存取 Azure Active Directory 圖形 Web 服務，則該服務的識別項 00000002-0000-0000-c000-000000000000，應該位於權杖的 aud 宣告中的值。</span><span class="sxs-lookup"><span data-stu-id="162c5-253">If the token was issued for accessing the Azure Active Directory Graph web service, then the identifier of that service, 00000002-0000-0000-c000-000000000000, should be in the value of the token’s aud claim.</span></span>  

<span data-ttu-id="162c5-254">開發人員若使用 Microsoft 所提供的 CLA 程式庫來建置 SCIM 服務，可以依照下列步驟使用 Microsoft.Owin.Security.ActiveDirectory 套件以驗證來自 Azure Active Directory 的要求：</span><span class="sxs-lookup"><span data-stu-id="162c5-254">Developers using the CLA libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using the Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span></span> 

1. <span data-ttu-id="162c5-255">在提供者中，透過讓 Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior 屬性在每次服務啟動時傳回要呼叫的方法，來實作此屬性：</span><span class="sxs-lookup"><span data-stu-id="162c5-255">In a provider, implement the Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method to be called whenever the service is started:</span></span> 

  ````
    public override Action\<Owin.IAppBuilder, System.Web.Http.HttpConfiguration.HttpConfiguration\> StartupBehavior
    {
      get
      {
        return this.OnServiceStartup;
      }
    }

    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder,  // Defined in Owin.dll.  
      System.Web.Http.HttpConfiguration configuration)  // Defined in System.Web.Http.dll.  
    {
    }
  ````

2. <span data-ttu-id="162c5-256">將下列程式碼新增到該方法中，以將對任何服務端點發出的任何要求，都驗證為持有 Azure Active Directory 代表指定租用戶簽發的權杖，以存取 Azure AD 圖形 Web 服務：</span><span class="sxs-lookup"><span data-stu-id="162c5-256">Add the following code to that method to have any request to any of the service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access to the Azure AD Graph web service:</span></span> 

  ````
    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder IAppBuilder applicationBuilder, 
      System.Web.Http.HttpConfiguration HttpConfiguration configuration)
    {
      // IFilter is defined in System.Web.Http.dll.  
      System.Web.Http.Filters.IFilter authorizationFilter = 
        new System.Web.Http.AuthorizeAttribute(); // Defined in System.Web.Http.dll.configuration.Filters.Add(authorizationFilter);

      // SystemIdentityModel.Tokens.TokenValidationParameters is defined in    
      // System.IdentityModel.Token.Jwt.dll.
      SystemIdentityModel.Tokens.TokenValidationParameters tokenValidationParameters =     
        new TokenValidationParameters()
        {
          ValidAudience = "00000002-0000-0000-c000-000000000000"
        };

      // WindowsAzureActiveDirectoryBearerAuthenticationOptions is defined in 
      // Microsoft.Owin.Security.ActiveDirectory.dll
      Microsoft.Owin.Security.ActiveDirectory.
      WindowsAzureActiveDirectoryBearerAuthenticationOptions authenticationOptions =
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions()    {
        TokenValidationParameters = tokenValidationParameters,
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute the appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a><span data-ttu-id="162c5-257">使用者和群組結構描述</span><span class="sxs-lookup"><span data-stu-id="162c5-257">User and group schema</span></span>
<span data-ttu-id="162c5-258">Azure Active Directory 可以佈建兩種類型的資源至 SCIM Web 服務。</span><span class="sxs-lookup"><span data-stu-id="162c5-258">Azure Active Directory can provision two types of resources to SCIM web services.</span></span>  <span data-ttu-id="162c5-259">這些類型的資源是使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="162c5-259">Those types of resources are users and groups.</span></span>  

<span data-ttu-id="162c5-260">使用者資源是由結構描述識別碼 urn:ietf:params:scim:schemas:extension:enterprise:2.0:User 識別，此識別碼包含在下列通訊協定規格中：http://tools.ietf.org/html/draft-ietf-scim-core-schema。</span><span class="sxs-lookup"><span data-stu-id="162c5-260">User resources are identified by the schema identifier, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span></span>  <span data-ttu-id="162c5-261">以下的表 1 提供相對於urn:ietf:params:scim:schemas:extension:enterprise:2.0:User 資源的屬性，Azure Active Directory 中使用者屬性的預設對應。</span><span class="sxs-lookup"><span data-stu-id="162c5-261">The default mapping of the attributes of users in Azure Active Directory to the attributes of urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resources is provided in table 1, below.</span></span>  

<span data-ttu-id="162c5-262">群組資源是由結構描述識別碼 http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group 識別。</span><span class="sxs-lookup"><span data-stu-id="162c5-262">Group resources are identified by the schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  <span data-ttu-id="162c5-263">下面的表 2 顯示 Azure Active Directory 中的群組屬性與 http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group 資源之屬性的預設對應。</span><span class="sxs-lookup"><span data-stu-id="162c5-263">Table 2, below, shows the default mapping of the attributes of groups in Azure Active Directory to the attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span></span>  

### <a name="table-1-default-user-attribute-mapping"></a><span data-ttu-id="162c5-264">表 1：預設使用者屬性對應</span><span class="sxs-lookup"><span data-stu-id="162c5-264">Table 1: Default user attribute mapping</span></span>
| <span data-ttu-id="162c5-265">Azure Active Directory 使用者</span><span class="sxs-lookup"><span data-stu-id="162c5-265">Azure Active Directory user</span></span> | <span data-ttu-id="162c5-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span><span class="sxs-lookup"><span data-stu-id="162c5-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span></span> |
| --- | --- |
| <span data-ttu-id="162c5-267">IsSoftDeleted</span><span class="sxs-lookup"><span data-stu-id="162c5-267">IsSoftDeleted</span></span> |<span data-ttu-id="162c5-268">作用中</span><span class="sxs-lookup"><span data-stu-id="162c5-268">active</span></span> |
| <span data-ttu-id="162c5-269">displayName</span><span class="sxs-lookup"><span data-stu-id="162c5-269">displayName</span></span> |<span data-ttu-id="162c5-270">displayName</span><span class="sxs-lookup"><span data-stu-id="162c5-270">displayName</span></span> |
| <span data-ttu-id="162c5-271">Facsimile-TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="162c5-271">Facsimile-TelephoneNumber</span></span> |<span data-ttu-id="162c5-272">phoneNumbers[type eq "fax"].value</span><span class="sxs-lookup"><span data-stu-id="162c5-272">phoneNumbers[type eq "fax"].value</span></span> |
| <span data-ttu-id="162c5-273">givenName</span><span class="sxs-lookup"><span data-stu-id="162c5-273">givenName</span></span> |<span data-ttu-id="162c5-274">name.givenName</span><span class="sxs-lookup"><span data-stu-id="162c5-274">name.givenName</span></span> |
| <span data-ttu-id="162c5-275">jobTitle</span><span class="sxs-lookup"><span data-stu-id="162c5-275">jobTitle</span></span> |<span data-ttu-id="162c5-276">title</span><span class="sxs-lookup"><span data-stu-id="162c5-276">title</span></span> |
| <span data-ttu-id="162c5-277">mail</span><span class="sxs-lookup"><span data-stu-id="162c5-277">mail</span></span> |<span data-ttu-id="162c5-278">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="162c5-278">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="162c5-279">mailNickname</span><span class="sxs-lookup"><span data-stu-id="162c5-279">mailNickname</span></span> |<span data-ttu-id="162c5-280">externalId</span><span class="sxs-lookup"><span data-stu-id="162c5-280">externalId</span></span> |
| <span data-ttu-id="162c5-281">manager</span><span class="sxs-lookup"><span data-stu-id="162c5-281">manager</span></span> |<span data-ttu-id="162c5-282">manager</span><span class="sxs-lookup"><span data-stu-id="162c5-282">manager</span></span> |
| <span data-ttu-id="162c5-283">mobile</span><span class="sxs-lookup"><span data-stu-id="162c5-283">mobile</span></span> |<span data-ttu-id="162c5-284">phoneNumbers[type eq "mobile"].value</span><span class="sxs-lookup"><span data-stu-id="162c5-284">phoneNumbers[type eq "mobile"].value</span></span> |
| <span data-ttu-id="162c5-285">objectId</span><span class="sxs-lookup"><span data-stu-id="162c5-285">objectId</span></span> |<span data-ttu-id="162c5-286">id</span><span class="sxs-lookup"><span data-stu-id="162c5-286">id</span></span> |
| <span data-ttu-id="162c5-287">postalCode</span><span class="sxs-lookup"><span data-stu-id="162c5-287">postalCode</span></span> |<span data-ttu-id="162c5-288">addresses[type eq "work"].postalCode</span><span class="sxs-lookup"><span data-stu-id="162c5-288">addresses[type eq "work"].postalCode</span></span> |
| <span data-ttu-id="162c5-289">proxy-Addresses</span><span class="sxs-lookup"><span data-stu-id="162c5-289">proxy-Addresses</span></span> |<span data-ttu-id="162c5-290">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="162c5-290">emails[type eq "other"].Value</span></span> |
| <span data-ttu-id="162c5-291">physical-Delivery-OfficeName</span><span class="sxs-lookup"><span data-stu-id="162c5-291">physical-Delivery-OfficeName</span></span> |<span data-ttu-id="162c5-292">addresses[type eq "other"].Formatted</span><span class="sxs-lookup"><span data-stu-id="162c5-292">addresses[type eq "other"].Formatted</span></span> |
| <span data-ttu-id="162c5-293">streetAddress</span><span class="sxs-lookup"><span data-stu-id="162c5-293">streetAddress</span></span> |<span data-ttu-id="162c5-294">addresses[type eq "work"].streetAddress</span><span class="sxs-lookup"><span data-stu-id="162c5-294">addresses[type eq "work"].streetAddress</span></span> |
| <span data-ttu-id="162c5-295">surname</span><span class="sxs-lookup"><span data-stu-id="162c5-295">surname</span></span> |<span data-ttu-id="162c5-296">name.familyName</span><span class="sxs-lookup"><span data-stu-id="162c5-296">name.familyName</span></span> |
| <span data-ttu-id="162c5-297">telephone-Number</span><span class="sxs-lookup"><span data-stu-id="162c5-297">telephone-Number</span></span> |<span data-ttu-id="162c5-298">phoneNumbers[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="162c5-298">phoneNumbers[type eq "work"].value</span></span> |
| <span data-ttu-id="162c5-299">user-PrincipalName</span><span class="sxs-lookup"><span data-stu-id="162c5-299">user-PrincipalName</span></span> |<span data-ttu-id="162c5-300">userName</span><span class="sxs-lookup"><span data-stu-id="162c5-300">userName</span></span> |

### <a name="table-2-default-group-attribute-mapping"></a><span data-ttu-id="162c5-301">表 2：預設群組屬性對應</span><span class="sxs-lookup"><span data-stu-id="162c5-301">Table 2: Default group attribute mapping</span></span>
| <span data-ttu-id="162c5-302">Azure Active Directory 群組</span><span class="sxs-lookup"><span data-stu-id="162c5-302">Azure Active Directory group</span></span> | <span data-ttu-id="162c5-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span><span class="sxs-lookup"><span data-stu-id="162c5-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span></span> |
| --- | --- |
| <span data-ttu-id="162c5-304">displayName</span><span class="sxs-lookup"><span data-stu-id="162c5-304">displayName</span></span> |<span data-ttu-id="162c5-305">externalId</span><span class="sxs-lookup"><span data-stu-id="162c5-305">externalId</span></span> |
| <span data-ttu-id="162c5-306">mail</span><span class="sxs-lookup"><span data-stu-id="162c5-306">mail</span></span> |<span data-ttu-id="162c5-307">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="162c5-307">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="162c5-308">mailNickname</span><span class="sxs-lookup"><span data-stu-id="162c5-308">mailNickname</span></span> |<span data-ttu-id="162c5-309">displayName</span><span class="sxs-lookup"><span data-stu-id="162c5-309">displayName</span></span> |
| <span data-ttu-id="162c5-310">members</span><span class="sxs-lookup"><span data-stu-id="162c5-310">members</span></span> |<span data-ttu-id="162c5-311">members</span><span class="sxs-lookup"><span data-stu-id="162c5-311">members</span></span> |
| <span data-ttu-id="162c5-312">objectId</span><span class="sxs-lookup"><span data-stu-id="162c5-312">objectId</span></span> |<span data-ttu-id="162c5-313">id</span><span class="sxs-lookup"><span data-stu-id="162c5-313">id</span></span> |
| <span data-ttu-id="162c5-314">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="162c5-314">proxyAddresses</span></span> |<span data-ttu-id="162c5-315">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="162c5-315">emails[type eq "other"].Value</span></span> |

## <a name="user-provisioning-and-de-provisioning"></a><span data-ttu-id="162c5-316">使用者佈建和取消佈建</span><span class="sxs-lookup"><span data-stu-id="162c5-316">User provisioning and de-provisioning</span></span>
<span data-ttu-id="162c5-317">下圖顯示 Azure Active Directory 會傳送至 SCIM 服務的訊息，以管理使用者在其他身分識別存放區中的生命週期。</span><span class="sxs-lookup"><span data-stu-id="162c5-317">The following illustration shows the messages that Azure Active Directory sends to a SCIM service to manage the lifecycle of a user in another identity store.</span></span> <span data-ttu-id="162c5-318">圖表也會示範使用 Microsoft 提供、用於建置此類服務的 CLI 程式庫所實作之 SCIM 服務如何將這些要求轉譯為對提供者的方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="162c5-318">The diagram also shows how a SCIM service implemented using the CLI libraries provided by Microsoft for building such services translate those requests into calls to the methods of a provider.</span></span>  

<span data-ttu-id="162c5-319">![][4]
圖 5：使用者佈建和取消佈建順序</span><span class="sxs-lookup"><span data-stu-id="162c5-319">![][4]
*Figure 5: User provisioning and de-provisioning sequence*</span></span>

1. <span data-ttu-id="162c5-320">Azure Active Directory 會查詢服務是否有 externalId 屬性值與 Azure AD 中使用者的 mailNickname 屬性值相符的使用者。</span><span class="sxs-lookup"><span data-stu-id="162c5-320">Azure Active Directory queries the service for a user with an externalId attribute value matching the mailNickname attribute value of a user in Azure AD.</span></span> <span data-ttu-id="162c5-321">查詢會以類似於此範例的超文字傳輸通訊協定 (HTTP) 要求表示，其中，jyoung 是 Azure Active Directory 中使用者的 mailNickname 範例：</span><span class="sxs-lookup"><span data-stu-id="162c5-321">The query is expressed as a Hypertext Transfer Protocol (HTTP) request such as this example, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span></span> 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="162c5-322">如果是使用 Microsoft 所提供、用於實作 SCIM 服務的通用語言基礎結構程式庫建置服務，會將要求轉譯為對服務提供者的 Query 方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="162c5-322">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Query method of the service’s provider.</span></span>  <span data-ttu-id="162c5-323">以下是該方法的簽章：</span><span class="sxs-lookup"><span data-stu-id="162c5-323">Here is the signature of that method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Protocol.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource[]> Query(
      Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters parameters, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="162c5-324">以下是 Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters 介面的定義：</span><span class="sxs-lookup"><span data-stu-id="162c5-324">Here is the definition of the Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span></span> 
  ````
    public interface IQueryParameters: 
      Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
        System.Collections.Generic.IReadOnlyCollection <Microsoft.SystemForCrossDomainIdentityManagement.IFilter> AlternateFilters 
        { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
      system.Collections.Generic.IReadOnlyCollection<string> ExcludedAttributePaths 
      { get; }
      System.Collections.Generic.IReadOnlyCollection<string> RequestedAttributePaths 
      { get; }
      string SchemaIdentifier 
      { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IFilter
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IFilter AdditionalFilter 
          { get; set; }
        string AttributePath 
          { get; } 
        Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator FilterOperator 
          { get; }
        string ComparisonValue 
          { get; }
    }

    public enum Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator
    {
        Equals
    }
  ````
  <span data-ttu-id="162c5-325">在查詢具有給定值 externalId 屬性的使用者的下列範例中，傳遞至 Query 方法的引數值為：</span><span class="sxs-lookup"><span data-stu-id="162c5-325">In the following sample of a query for a user with a given value for the externalId attribute, values of the arguments passed to the Query method are:</span></span> 
  * <span data-ttu-id="162c5-326">parameters.AlternateFilters.Count: 1</span><span class="sxs-lookup"><span data-stu-id="162c5-326">parameters.AlternateFilters.Count: 1</span></span>
  * <span data-ttu-id="162c5-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span><span class="sxs-lookup"><span data-stu-id="162c5-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span></span>
  * <span data-ttu-id="162c5-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="162c5-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="162c5-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span><span class="sxs-lookup"><span data-stu-id="162c5-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span></span>
  * <span data-ttu-id="162c5-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span><span class="sxs-lookup"><span data-stu-id="162c5-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span></span> 

2. <span data-ttu-id="162c5-331">如果向 Web 服務查詢是否有 externalId 屬性值與使用者的 mailNickname 值相符的使用者時，回應未傳回任何使用者，Azure Active Directory 就會要求服務佈建與 Azure Active Directory 中的使用者對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="162c5-331">If the response to a query to the web service for a user with an externalId attribute value that matches the mailNickname attribute value of a user does not return any users, then Azure Active Directory requests that the service provision a user corresponding to the one in Azure Active Directory.</span></span>  <span data-ttu-id="162c5-332">以下是這類要求的範例：</span><span class="sxs-lookup"><span data-stu-id="162c5-332">Here is an example of such a request:</span></span> 
  ````
    POST https://.../scim/Users HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas":
      [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0User"],
      "externalId":"jyoung",
      "userName":"jyoung",
      "active":true,
      "addresses":null,
      "displayName":"Joy Young",
      "emails": [
        {
          "type":"work",
          "value":"jyoung@Contoso.com",
          "primary":true}],
      "meta": {
        "resourceType":"User"},
       "name":{
        "familyName":"Young",
        "givenName":"Joy"},
      "phoneNumbers":null,
      "preferredLanguage":null,
      "title":null,
      "department":null,
      "manager":null}
  ````
  <span data-ttu-id="162c5-333">Microsoft 所提供、用於實作 SCIM 服務的通用語言基礎結構程式庫，會將要求轉譯為對服務提供者的 Create 方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="162c5-333">The Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call to the Create method of the service’s provider.</span></span>  <span data-ttu-id="162c5-334">Create 方法具有此簽章：</span><span class="sxs-lookup"><span data-stu-id="162c5-334">The Create method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="162c5-335">在佈建使用者的要求中，資源引數的值會是 Microsoft.SystemForCrossDomainIdentityManagement 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="162c5-335">In a request to provision a user, the value of the resource argument is an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="162c5-336">Microsoft.SystemForCrossDomainIdentityManagement.Schemas 程式庫中定義的 Core2EnterpriseUser 類別。</span><span class="sxs-lookup"><span data-stu-id="162c5-336">Core2EnterpriseUser class, defined in the Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span></span>  <span data-ttu-id="162c5-337">如果佈建使用者的要求成功，則方法的實作應該會傳回 Microsoft.SystemForCrossDomainIdentityManagement 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="162c5-337">If the request to provision the user succeeds, then the implementation of the method is expected to return an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="162c5-338">Core2EnterpriseUser 類別，且其識別碼屬性值設定為新佈建使用者的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="162c5-338">Core2EnterpriseUser class, with the value of the Identifier property set to the unique identifier of the newly provisioned user.</span></span>  

3. <span data-ttu-id="162c5-339">為了更新已知存在於前端為 SCIM 之身分識別存放區中的使用者，Azure Active Directory 會以類似下方的要求向服務要求該使用者的目前狀態，來繼續執行：</span><span class="sxs-lookup"><span data-stu-id="162c5-339">To update a user known to exist in an identity store fronted by an SCIM, Azure Active Directory proceeds by requesting the current state of that user from the service with a request such as:</span></span> 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="162c5-340">如果是使用 Microsoft 所提供、用於實作 SCIM 服務的通用語言基礎結構程式庫建置服務，會將要求轉譯為對服務提供者的 Retrieve 方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="162c5-340">In a service built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, the request is translated into a call to the Retrieve method of the service’s provider.</span></span>  <span data-ttu-id="162c5-341">以下是 Retrieve 方法的簽章：</span><span class="sxs-lookup"><span data-stu-id="162c5-341">Here is the signature of the Retrieve method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource and 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
    // are defined in Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> 
       Retrieve(
         Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
           parameters, 
           string correlationIdentifier);

    public interface 
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters:   
        IRetrievalParameters
        {
          Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
            ResourceIdentifier 
              { get; }
    }
    public interface Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier
    {
        string Identifier 
          { get; set; }
        string Microsoft.SystemForCrossDomainIdentityManagement.SchemaIdentifier 
          { get; set; }
    }
  ````
  <span data-ttu-id="162c5-342">在擷取使用者目前狀態之要求的範例中，提供作為參數引數值的物件具有的屬性值如下所示：</span><span class="sxs-lookup"><span data-stu-id="162c5-342">In the example of a request to retrieve the current state of a user, the values of the properties of the object provided as the value of the parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="162c5-343">識別碼："54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="162c5-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="162c5-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="162c5-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

4. <span data-ttu-id="162c5-345">如果要更新某個參考屬性，Azure Active Directory 就會查詢服務，以判斷以該服務作為前端之身分識別存放區中參考屬性目前的值，是否已經與 Azure Active Directory 中該屬性的值相符。</span><span class="sxs-lookup"><span data-stu-id="162c5-345">If a reference attribute is to be updated, then Azure Active Directory queries the service to determine whether or not the current value of the reference attribute in the identity store fronted by the service already matches the value of that attribute in Azure Active Directory.</span></span> <span data-ttu-id="162c5-346">對於使用者，以這種方式可查詢目前值的唯一屬性會是管理員屬性。</span><span class="sxs-lookup"><span data-stu-id="162c5-346">For users, the only attribute of which the current value is queried in this way is the manager attribute.</span></span> <span data-ttu-id="162c5-347">要判斷特定使用者物件的管理員屬性目前是否具有某個值之要求的範例如下：</span><span class="sxs-lookup"><span data-stu-id="162c5-347">Here is an example of a request to determine whether the manager attribute of a particular user object currently has a certain value:</span></span> 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="162c5-348">屬性查詢參數 id 的值，表示如果滿足提供做為篩選查詢參數值的運算式的使用者物件存在，則服務應該以 urn:ietf:params:scim:schemas:core:2.0:User 或 urn:ietf:params:scim:schemas:extension:enterprise:2.0:User 資源回應，包僅括該資源 id 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="162c5-348">The value of the attributes query parameter, id, signifies that if a user object exists that satisfies the expression provided as the value of the filter query parameter, then the service is expected to respond with a urn:ietf:params:scim:schemas:core:2.0:User or urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resource, including only the value of that resource’s id attribute.</span></span>  <span data-ttu-id="162c5-349">要求者知道**識別碼**屬性的值。</span><span class="sxs-lookup"><span data-stu-id="162c5-349">The value of the **id** attribute is known to the requestor.</span></span> <span data-ttu-id="162c5-350">它包含在篩選查詢參數的值中；要求它的目的只是實際要求滿足篩選運算式作為任何這類物件是否存在指示之資源的最小表示。</span><span class="sxs-lookup"><span data-stu-id="162c5-350">It is included in the value of the filter query parameter; the purpose of asking for it is actually to request a minimal representation of a resource that satisfying the filter expression as an indication of whether or not any such object exists.</span></span>   

  <span data-ttu-id="162c5-351">如果是使用 Microsoft 所提供、用於實作 SCIM 服務的通用語言基礎結構程式庫建置服務，會將要求轉譯為對服務提供者的 Query 方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="162c5-351">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Query method of the service’s provider.</span></span> <span data-ttu-id="162c5-352">提供物件的屬性值作為參數引數的值，如下所示：</span><span class="sxs-lookup"><span data-stu-id="162c5-352">The value of the properties of the object provided as the value of the parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="162c5-353">parameters.AlternateFilters.Count: 2</span><span class="sxs-lookup"><span data-stu-id="162c5-353">parameters.AlternateFilters.Count: 2</span></span>
  * <span data-ttu-id="162c5-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span><span class="sxs-lookup"><span data-stu-id="162c5-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span></span>
  * <span data-ttu-id="162c5-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="162c5-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="162c5-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="162c5-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="162c5-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="162c5-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span></span>
  * <span data-ttu-id="162c5-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="162c5-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="162c5-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span><span class="sxs-lookup"><span data-stu-id="162c5-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span></span>
  * <span data-ttu-id="162c5-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span><span class="sxs-lookup"><span data-stu-id="162c5-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span></span>
  * <span data-ttu-id="162c5-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="162c5-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

  <span data-ttu-id="162c5-362">在此處，索引 x 的值可能會是 0，而索引 y 的值可能是 1，或 x 值可能是 1 而 y 的值可能是 0，視篩選查詢參數運算式的順序而定。</span><span class="sxs-lookup"><span data-stu-id="162c5-362">Here, the value of the index x may be 0 and the value of the index y may be 1, or the value of x may be 1 and the value of y may be 0, depending on the order of the expressions of the filter query parameter.</span></span>   

5. <span data-ttu-id="162c5-363">以下是由 Azure Active Directory 對 SCIM 服務發出要求來更新使用者的範例：</span><span class="sxs-lookup"><span data-stu-id="162c5-363">Here is an example of a request from Azure Active Directory to an SCIM service to update a user:</span></span> 
  ````
    PATCH ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas": 
      [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"],
      "Operations":
      [
        {
          "op":"Add",
          "path":"manager",
          "value":
            [
              {
                "$ref":"http://.../scim/Users/2819c223-7f76-453a-919d-413861904646",
                "value":"2819c223-7f76-453a-919d-413861904646"}]}]}
  ````
  <span data-ttu-id="162c5-364">用於實作 SCIM 服務的 Microsoft 通用語言基礎結構程式庫，會將要求轉譯為對服務提供者的 Update 方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="162c5-364">The Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate the request into a call to the Update method of the service’s provider.</span></span> <span data-ttu-id="162c5-365">以下是更新方法的簽章：</span><span class="sxs-lookup"><span data-stu-id="162c5-365">Here is the signature of the Update method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks and 
    // System.Collections.Generic.IReadOnlyCollection<T>
    // are defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IPatch, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation, 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationName, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IPath and 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationValue 
    // are all defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 

    System.Threading.Tasks.Task Update(
      Microsoft.SystemForCrossDomainIdentityManagement.IPatch patch, 
      string correlationIdentifier);

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IPatch
    {
    Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase 
      PatchRequest 
        { get; set; }
    Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
      ResourceIdentifier 
        { get; set; }        
    }

    public class PatchRequest2: 
      Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase
    {
    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation> 
        Operations
        { get;}

    public void AddOperation(
      Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation operation);
    }

    public class PatchOperation
    {
    public Microsoft.SystemForCrossDomainIdentityManagement.OperationName 
      Name
      { get; set; }

    public Microsoft.SystemForCrossDomainIdentityManagement.IPath 
      Path
      { get; set; }

    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.OperationValue> Value
      { get; }

    public void AddValue(
      Microsoft.SystemForCrossDomainIdentityManagement.OperationValue value);
    }

    public enum OperationName
    {
      Add,
      Remove,
      Replace
    }

    public interface IPath
    {
      string AttributePath { get; }
      System.Collections.Generic.IReadOnlyCollection<IFilter> SubAttributes { get; }
      Microsoft.SystemForCrossDomainIdentityManagement.IPath ValuePath { get; }
    }

    public class OperationValue
    {
      public string Reference
      { get; set; }

      public string Value
      { get; set; }
    }
  ````
    <span data-ttu-id="162c5-366">在更新使用者之要求的範例中，提供作為修補程式引數值的物件具有這些屬性值：</span><span class="sxs-lookup"><span data-stu-id="162c5-366">In the example of a request to update a user, the object provided as the value of the patch argument has these property values:</span></span> 
  
  * <span data-ttu-id="162c5-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="162c5-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="162c5-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="162c5-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>
  * <span data-ttu-id="162c5-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span><span class="sxs-lookup"><span data-stu-id="162c5-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span></span>
  * <span data-ttu-id="162c5-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span><span class="sxs-lookup"><span data-stu-id="162c5-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span></span>
  * <span data-ttu-id="162c5-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="162c5-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span></span>
  * <span data-ttu-id="162c5-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span><span class="sxs-lookup"><span data-stu-id="162c5-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span></span>
  * <span data-ttu-id="162c5-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="162c5-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span></span>
  * <span data-ttu-id="162c5-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="162c5-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span></span>

6. <span data-ttu-id="162c5-375">若要將使用者從前端為 SCIM 服務的身分識別存放區中取消佈建，Azure AD 會傳送像以下的要求：</span><span class="sxs-lookup"><span data-stu-id="162c5-375">To de-provision a user from an identity store fronted by an SCIM service, Azure AD sends a request such as:</span></span> 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="162c5-376">如果是使用 Microsoft 所提供、用於實作 SCIM 服務的通用語言基礎結構程式庫建置服務，會將要求轉譯為對服務提供者的 Delete 方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="162c5-376">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Delete method of the service’s provider.</span></span>   <span data-ttu-id="162c5-377">該方法具有此簽章：</span><span class="sxs-lookup"><span data-stu-id="162c5-377">That method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="162c5-378">提供作為 resourceIdentifier 引數值的物件，在要取消佈建使用者之要求的範例中，會具有這些屬性值：</span><span class="sxs-lookup"><span data-stu-id="162c5-378">The object provided as the value of the resourceIdentifier argument has these property values in the example of a request to de-provision a user:</span></span> 
  
  * <span data-ttu-id="162c5-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="162c5-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="162c5-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="162c5-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

## <a name="group-provisioning-and-de-provisioning"></a><span data-ttu-id="162c5-381">群組佈建和取消佈建</span><span class="sxs-lookup"><span data-stu-id="162c5-381">Group provisioning and de-provisioning</span></span>
<span data-ttu-id="162c5-382">下圖顯示 Azure AD 會傳送至 SCIM 服務的訊息，以管理群組在其他身分識別存放區中的生命週期。</span><span class="sxs-lookup"><span data-stu-id="162c5-382">The following illustration shows the messages that Azure AcD sends to a SCIM service to manage the lifecycle of a group in another identity store.</span></span>  <span data-ttu-id="162c5-383">這些訊息與使用者的訊息不同，有下列三個方面：</span><span class="sxs-lookup"><span data-stu-id="162c5-383">Those messages differ from the messages pertaining to users in three ways:</span></span> 

* <span data-ttu-id="162c5-384">群組資源的結構描述會識別為 http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group。</span><span class="sxs-lookup"><span data-stu-id="162c5-384">The schema of a group resource is identified as http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  
* <span data-ttu-id="162c5-385">擷取群組的要求會規定將成員屬性從回應要求中提供的任何資源中排除。</span><span class="sxs-lookup"><span data-stu-id="162c5-385">Requests to retrieve groups stipulate that the members attribute is to be excluded from any resource provided in response to the request.</span></span>  
* <span data-ttu-id="162c5-386">要求判斷參考屬性是否具有特定值，會是有關成員屬性的要求。</span><span class="sxs-lookup"><span data-stu-id="162c5-386">Requests to determine whether a reference attribute has a certain value are requests about the members attribute.</span></span>  

<span data-ttu-id="162c5-387">![][5]
圖 6：群組佈建和取消佈建順序</span><span class="sxs-lookup"><span data-stu-id="162c5-387">![][5]
*Figure 6: Group provisioning and de-provisioning sequence*</span></span>

## <a name="related-articles"></a><span data-ttu-id="162c5-388">相關文章</span><span class="sxs-lookup"><span data-stu-id="162c5-388">Related articles</span></span>
* [<span data-ttu-id="162c5-389">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="162c5-389">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="162c5-390">自動化 SaaS 應用程式使用者佈建/解除佈建</span><span class="sxs-lookup"><span data-stu-id="162c5-390">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="162c5-391">自訂使用者佈建的屬性對應</span><span class="sxs-lookup"><span data-stu-id="162c5-391">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="162c5-392">撰寫屬性對應的運算式</span><span class="sxs-lookup"><span data-stu-id="162c5-392">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="162c5-393">適用於使用者佈建的範圍篩選器</span><span class="sxs-lookup"><span data-stu-id="162c5-393">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="162c5-394">帳戶佈建通知</span><span class="sxs-lookup"><span data-stu-id="162c5-394">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="162c5-395">如何整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="162c5-395">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
