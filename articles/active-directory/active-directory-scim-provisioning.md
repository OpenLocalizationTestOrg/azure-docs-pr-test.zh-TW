---
title: "aaaUsing 跨網域的識別管理的系統自動佈建使用者和群組從 Azure Active Directory tooapplications |Microsoft 文件"
description: "Azure Active Directory 會自動佈建使用者及群組 tooany 應用程式或身分識別存放區由 web 服務 fronted hello hello SCIM 通訊協定規格中定義的介面"
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
ms.openlocfilehash: 43045c97e68d0d22db598dcb5ec23481c4e97718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-system-for-cross-domain-identity-management-tooautomatically-provision-users-and-groups-from-azure-active-directory-tooapplications"></a><span data-ttu-id="a24f3-103">使用來自 Azure Active Directory tooapplications 跨網域身分識別管理 tooautomatically 佈建使用者和群組的系統</span><span class="sxs-lookup"><span data-stu-id="a24f3-103">Using System for Cross-Domain Identity Management tooautomatically provision users and groups from Azure Active Directory tooapplications</span></span>

## <a name="overview"></a><span data-ttu-id="a24f3-104">概觀</span><span class="sxs-lookup"><span data-stu-id="a24f3-104">Overview</span></span>
<span data-ttu-id="a24f3-105">Azure Active Directory (Azure AD) 可自動佈建使用者及群組 tooany 應用程式或身分識別存放區由 web 服務 fronted hello 介面定義中 hello[系統跨網域身分識別管理 (SCIM) 2.0通訊協定規格](https://tools.ietf.org/html/draft-ietf-scim-api-19)。</span><span class="sxs-lookup"><span data-stu-id="a24f3-105">Azure Active Directory (Azure AD) can automatically provision users and groups tooany application or identity store that is fronted by a web service with hello interface defined in hello [System for Cross-Domain Identity Management (SCIM) 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span></span> <span data-ttu-id="a24f3-106">Azure Active Directory 可以傳送要求 toocreate、 修改或刪除指定的使用者和群組 toohello web 服務。</span><span class="sxs-lookup"><span data-stu-id="a24f3-106">Azure Active Directory can send requests toocreate, modify, or delete assigned users and groups toohello web service.</span></span> <span data-ttu-id="a24f3-107">hello web 服務可以再將這些要求轉譯成 hello 目標身分識別存放區上的作業。</span><span class="sxs-lookup"><span data-stu-id="a24f3-107">hello web service can then translate those requests into operations on hello target identity store.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="a24f3-108">Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="a24f3-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 



<span data-ttu-id="a24f3-109">![][0]
*圖 1： 佈建 Azure Active Directory web 服務透過 tooan 身分識別存放區從*</span><span class="sxs-lookup"><span data-stu-id="a24f3-109">![][0]
*Figure 1: Provisioning from Azure Active Directory tooan identity store via a web service*</span></span>

<span data-ttu-id="a24f3-110">這項功能可搭配 Azure AD tooenable 單一登入和自動使用者佈建來提供或為 fronted SCIM web 服務應用程式中的 hello 「 攜帶您自己的應用程式 」 功能。</span><span class="sxs-lookup"><span data-stu-id="a24f3-110">This capability can be used in conjunction with hello “bring your own app” capability in Azure AD tooenable single sign-on and automatic user provisioning for applications that provide or are fronted by a SCIM web service.</span></span>

<span data-ttu-id="a24f3-111">在 Azure Active Directory 中使用 SCIM 有兩個使用案例：</span><span class="sxs-lookup"><span data-stu-id="a24f3-111">There are two use cases for using SCIM in Azure Active Directory:</span></span>

* <span data-ttu-id="a24f3-112">**佈建使用者及群組 tooapplications 支援 SCIM**支援 SCIM 2.0 和使用的驗證可搭配不需設定 Azure AD 的 OAuth 承載語彙基元的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a24f3-112">**Provisioning users and groups tooapplications that support SCIM** Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication works with Azure AD without configuration.</span></span>
* <span data-ttu-id="a24f3-113">**建置您自己的佈建解決方案針對支援其他應用程式開發介面為基礎的佈建應用程式**非 SCIM 應用程式，您可以建立 SCIM 端點 tootranslate hello Azure AD SCIM 端點之間任何 API hello 應用程式支援進行使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="a24f3-113">**Build your own provisioning solution for applications that support other API-based provisioning** For non-SCIM applications, you can create a SCIM endpoint tootranslate between hello Azure AD SCIM endpoint and any API hello application supports for user provisioning.</span></span> <span data-ttu-id="a24f3-114">toohelp 開發 SCIM 端點，我們提供通用語言基礎結構 (CLI) 文件庫，以及程式碼範例會示範如何 toodo 提供 SCIM 端點，以及將 SCIM 訊息轉譯。</span><span class="sxs-lookup"><span data-stu-id="a24f3-114">toohelp you develop a SCIM endpoint, we provide Common Language Infrastructure (CLI) libraries along with code samples that show you how toodo provide a SCIM endpoint and translate SCIM messages.</span></span>  

## <a name="provisioning-users-and-groups-tooapplications-that-support-scim"></a><span data-ttu-id="a24f3-115">佈建使用者及群組 tooapplications 支援 SCIM</span><span class="sxs-lookup"><span data-stu-id="a24f3-115">Provisioning users and groups tooapplications that support SCIM</span></span>
<span data-ttu-id="a24f3-116">Azure AD 可設定的 tooautomatically 指派的佈建使用者及群組 tooapplications 可實作[跨網域 2 (SCIM) 的身分識別管理系統](https://tools.ietf.org/html/draft-ietf-scim-api-19)web 服務，並接受驗證的 OAuth 承載語彙基元.</span><span class="sxs-lookup"><span data-stu-id="a24f3-116">Azure AD can be configured tooautomatically provision assigned users and groups tooapplications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web service and accept OAuth bearer tokens for authentication.</span></span> <span data-ttu-id="a24f3-117">Hello SCIM 2.0 規格中的應用程式必須符合下列需求：</span><span class="sxs-lookup"><span data-stu-id="a24f3-117">Within hello SCIM 2.0 specification, applications must meet these requirements:</span></span>

* <span data-ttu-id="a24f3-118">建立使用者和/或群組，根據 3.3 節 hello SCIM 通訊協定的支援。</span><span class="sxs-lookup"><span data-stu-id="a24f3-118">Supports creating users and/or groups, as per section 3.3 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="a24f3-119">修改使用者和/或群組與修補程式要求依照區段 3.5.2 hello SCIM 通訊協定的支援。</span><span class="sxs-lookup"><span data-stu-id="a24f3-119">Supports modifying users and/or groups with patch requests as per section 3.5.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="a24f3-120">擷取已知的資源，根據區段 3.4.1 hello SCIM 通訊協定的支援。</span><span class="sxs-lookup"><span data-stu-id="a24f3-120">Supports retrieving a known resource as per section 3.4.1 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="a24f3-121">查詢使用者和/或群組，依據區段 3.4.2 hello SCIM 通訊協定的支援。</span><span class="sxs-lookup"><span data-stu-id="a24f3-121">Supports querying users and/or groups, as per section 3.4.2 of hello SCIM protocol.</span></span>  <span data-ttu-id="a24f3-122">依預設會依 externalId 來查詢使用者，並依 displayName 查詢群組。</span><span class="sxs-lookup"><span data-stu-id="a24f3-122">By default, users are queried by externalId and groups are queried by displayName.</span></span>  
* <span data-ttu-id="a24f3-123">查詢使用者 ID 和由管理員根據區段 3.4.2 hello SCIM 通訊協定的支援。</span><span class="sxs-lookup"><span data-stu-id="a24f3-123">Supports querying user by ID and by manager as per section 3.4.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="a24f3-124">查詢群組 ID 和成員根據區段 3.4.2 hello SCIM 通訊協定的支援。</span><span class="sxs-lookup"><span data-stu-id="a24f3-124">Supports querying groups by ID and by member as per section 3.4.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="a24f3-125">接受授權 > 一節 2.1 根據 hello SCIM 通訊協定的 OAuth 承載語彙基元。</span><span class="sxs-lookup"><span data-stu-id="a24f3-125">Accepts OAuth bearer tokens for authorization as per section 2.1 of hello SCIM protocol.</span></span>

<span data-ttu-id="a24f3-126">洽詢應用程式提供者，或參閱應用程式提供者文件中的相關陳述，以了解是否符合這些需求。</span><span class="sxs-lookup"><span data-stu-id="a24f3-126">Check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span></span>

### <a name="getting-started"></a><span data-ttu-id="a24f3-127">開始使用</span><span class="sxs-lookup"><span data-stu-id="a24f3-127">Getting started</span></span>
<span data-ttu-id="a24f3-128">支援在本文中所述的 hello SCIM 設定檔的應用程式可連接的 tooAzure Active Directory 使用 hello Azure AD 應用程式庫中的 hello 「 非組件庫應用程式 」 功能。</span><span class="sxs-lookup"><span data-stu-id="a24f3-128">Applications that support hello SCIM profile described in this article can be connected tooAzure Active Directory using hello "non-gallery application" feature in hello Azure AD application gallery.</span></span> <span data-ttu-id="a24f3-129">一旦連線、 Azure AD 執行同步處理程序會用來查詢應用程式 hello SCIM 端點每隔 20 分鐘指派使用者和群組，並建立或修改它們根據 toohello 指派詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a24f3-129">Once connected, Azure AD runs a synchronization process every 20 minutes where it queries hello application's SCIM endpoint for assigned users and groups, and creates or modifies them according toohello assignment details.</span></span>

<span data-ttu-id="a24f3-130">**tooconnect 支援 SCIM 的應用程式：**</span><span class="sxs-lookup"><span data-stu-id="a24f3-130">**tooconnect an application that supports SCIM:**</span></span>

1. <span data-ttu-id="a24f3-131">登入太[hello Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a24f3-131">Sign in too[hello Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="a24f3-132">瀏覽過 * * Azure Active Directory > 企業應用程式，然後選取**新的應用程式 > 所有 > 非組件庫的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a24f3-132">Browse too**Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="a24f3-133">輸入您的應用程式的名稱，然後按一下**新增**圖示 toocreate 應用程式物件。</span><span class="sxs-lookup"><span data-stu-id="a24f3-133">Enter a name for your application, and click **Add** icon toocreate an app object.</span></span>
    
  <span data-ttu-id="a24f3-134">![][1]
  圖 2：使用 Azure AD 應用程式庫</span><span class="sxs-lookup"><span data-stu-id="a24f3-134">![][1]
*Figure 2: Azure AD application gallery*</span></span>
    
4. <span data-ttu-id="a24f3-135">在 hello 結果 畫面上，選取 hello**佈建**hello 左側資料行中的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a24f3-135">In hello resulting screen, select hello **Provisioning** tab in hello left column.</span></span>
5. <span data-ttu-id="a24f3-136">在 hello**佈建模式**功能表上，選取**自動**。</span><span class="sxs-lookup"><span data-stu-id="a24f3-136">In hello **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="a24f3-137">![][2]
  *圖 3： 設定 hello Azure 入口網站中佈建*</span><span class="sxs-lookup"><span data-stu-id="a24f3-137">![][2]
*Figure 3: Configuring provisioning in hello Azure portal*</span></span>
    
6. <span data-ttu-id="a24f3-138">在 hello**租用戶 URL**欄位中，輸入 hello hello 應用程式的 SCIM 端點 URL。</span><span class="sxs-lookup"><span data-stu-id="a24f3-138">In hello **Tenant URL** field, enter hello URL of hello application's SCIM endpoint.</span></span> <span data-ttu-id="a24f3-139">範例：https://api.contoso.com/scim/v2/</span><span class="sxs-lookup"><span data-stu-id="a24f3-139">Example: https://api.contoso.com/scim/v2/</span></span>
7. <span data-ttu-id="a24f3-140">如果 hello SCIM 端點需要簽發者以外的 Azure AD 中，從 OAuth 承載權杖，則複製 hello required OAuth 承載權杖到 hello 選擇性**密碼語彙基元**欄位。</span><span class="sxs-lookup"><span data-stu-id="a24f3-140">If hello SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy hello required OAuth bearer token into hello optional **Secret Token** field.</span></span> <span data-ttu-id="a24f3-141">如果此欄位保留空白，則 Azure AD 會在每個要求包含從 Azure AD 簽發的 OAuth 持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="a24f3-141">If this field is left blank, then Azure AD included an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="a24f3-142">使用 Azure AD 作為識別提供者的應用程式，可以驗證此 Azure AD 簽發的權杖。</span><span class="sxs-lookup"><span data-stu-id="a24f3-142">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="a24f3-143">按一下 hello**測試連接**按鈕 toohave Azure Active Directory 嘗試 tooconnect toohello SCIM 端點。</span><span class="sxs-lookup"><span data-stu-id="a24f3-143">Click hello **Test Connection** button toohave Azure Active Directory attempt tooconnect toohello SCIM endpoint.</span></span> <span data-ttu-id="a24f3-144">如果 hello 嘗試都失敗，則會顯示資訊時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="a24f3-144">If hello attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="a24f3-145">如果成功 hello 嘗試 tooconnect toohello 應用程式，然後按一下**儲存**toosave hello 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="a24f3-145">If hello attempts tooconnect toohello application succeed, then click **Save** toosave hello admin credentials.</span></span>
10. <span data-ttu-id="a24f3-146">在 hello**對應**區段中，有兩組可選取的屬性對應： 一個給使用者物件，一個群組物件。</span><span class="sxs-lookup"><span data-stu-id="a24f3-146">In hello **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="a24f3-147">選取同步處理每一個 tooreview hello 屬性從 Azure Active Directory tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a24f3-147">Select each one tooreview hello attributes that are synchronized from Azure Active Directory tooyour app.</span></span> <span data-ttu-id="a24f3-148">hello 做為所選取的屬性**比對**屬性是您的應用程式進行更新作業中使用的 toomatch hello 使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="a24f3-148">hello attributes selected as **Matching** properties are used toomatch hello users and groups in your app for update operations.</span></span> <span data-ttu-id="a24f3-149">選取 hello 儲存按鈕 toocommit 任何變更。</span><span class="sxs-lookup"><span data-stu-id="a24f3-149">Select hello Save button toocommit any changes.</span></span>

    >[!NOTE]
    ><span data-ttu-id="a24f3-150">您可以選擇性地停用正在同步處理群組物件的停用 hello 「 群組 」 對應。</span><span class="sxs-lookup"><span data-stu-id="a24f3-150">You can optionally disable syncing of group objects by disabling hello "groups" mapping.</span></span> 

11. <span data-ttu-id="a24f3-151">在下**設定**，hello**範圍**欄位會定義哪些使用者或工作群組同步處理。</span><span class="sxs-lookup"><span data-stu-id="a24f3-151">Under **Settings**, hello **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="a24f3-152">選取 「 同步處理只指派使用者和群組 （建議選項） 只會同步使用者和群組指派在 hello**使用者和群組** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a24f3-152">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in hello **Users and groups** tab.</span></span>
12. <span data-ttu-id="a24f3-153">您的設定完成之後，請變更 hello**佈建狀態**太**上**。</span><span class="sxs-lookup"><span data-stu-id="a24f3-153">Once your configuration is complete, change hello **Provisioning Status** too**On**.</span></span>
13. <span data-ttu-id="a24f3-154">按一下**儲存**toostart hello Azure AD 佈建服務。</span><span class="sxs-lookup"><span data-stu-id="a24f3-154">Click **Save** toostart hello Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="a24f3-155">如果同步處理只會指派使用者和群組 （建議選項），是確定 tooselect hello**使用者和群組**索引標籤上，並指派 hello 使用者和/或您想 toosync 的群組。</span><span class="sxs-lookup"><span data-stu-id="a24f3-155">If syncing only assigned users and groups (recommended), be sure tooselect hello **Users and groups** tab and assign hello users and/or groups you wish toosync.</span></span>

<span data-ttu-id="a24f3-156">一旦啟動 hello 初始同步處理後，您可以使用 hello**稽核記錄檔**toomonitor 進度會顯示 hello 佈建應用程式上的服務所執行的所有動作索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="a24f3-156">Once hello initial synchronization has started, you can use hello **Audit logs** tab toomonitor progress, which shows all actions performed by hello provisioning service on your app.</span></span> <span data-ttu-id="a24f3-157">如需有關 tooread hello Azure AD 佈建的記錄方式的詳細資訊，請參閱[報告使用者自動帳戶佈建](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)。</span><span class="sxs-lookup"><span data-stu-id="a24f3-157">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

>[!NOTE]
><span data-ttu-id="a24f3-158">hello 初始同步處理會較長的 tooperform 比發生大約每隔 20 分鐘，只要 hello 服務正在執行的後續同步處理。</span><span class="sxs-lookup"><span data-stu-id="a24f3-158">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> 


## <a name="building-your-own-provisioning-solution-for-any-application"></a><span data-ttu-id="a24f3-159">為任何應用程式建置您自己的佈建解決方案</span><span class="sxs-lookup"><span data-stu-id="a24f3-159">Building your own provisioning solution for any application</span></span>
<span data-ttu-id="a24f3-160">建立可與 Azure Active Directory 互動的 SCIM Web 服務後，您即可為提供 REST 或 SOAP 使用者佈建 API 的絕大多數應用程式啟用單一登入和自動使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="a24f3-160">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span></span>

<span data-ttu-id="a24f3-161">其運作方式如下：</span><span class="sxs-lookup"><span data-stu-id="a24f3-161">Here’s how it works:</span></span>

1. <span data-ttu-id="a24f3-162">Azure AD 提供名為 [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/)的通用語言基礎結構程式庫。</span><span class="sxs-lookup"><span data-stu-id="a24f3-162">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span></span> <span data-ttu-id="a24f3-163">系統整合人員和開發人員可以使用此程式庫 toocreate 並部署 SCIM 為基礎的 web 服務端點連接的 Azure AD tooany 應用程式的身分識別存放區功能。</span><span class="sxs-lookup"><span data-stu-id="a24f3-163">System integrators and developers can use this library toocreate and deploy a SCIM-based web service endpoint capable of connecting Azure AD tooany application’s identity store.</span></span>
2. <span data-ttu-id="a24f3-164">對應會實作 hello web 服務 toomap hello 標準的使用者結構描述 toohello 使用者結構描述和 hello 應用程式所需的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="a24f3-164">Mappings are implemented in hello web service toomap hello standardized user schema toohello user schema and protocol required by hello application.</span></span>
3. <span data-ttu-id="a24f3-165">hello 應用程式庫中的自訂應用程式一部分的 Azure AD 中註冊 hello 端點 URL。</span><span class="sxs-lookup"><span data-stu-id="a24f3-165">hello endpoint URL is registered in Azure AD as part of a custom application in hello application gallery.</span></span>
4. <span data-ttu-id="a24f3-166">使用者和群組指派 toothis 應用程式在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="a24f3-166">Users and groups are assigned toothis application in Azure AD.</span></span> <span data-ttu-id="a24f3-167">指派，時，它們被放入佇列進行同步處理的 toobe toohello 目標應用程式。</span><span class="sxs-lookup"><span data-stu-id="a24f3-167">Upon assignment, they are put into a queue toobe synchronized toohello target application.</span></span> <span data-ttu-id="a24f3-168">處理 hello 佇列 hello 同步處理程序執行每隔 20 分鐘。</span><span class="sxs-lookup"><span data-stu-id="a24f3-168">hello synchronization process handling hello queue runs every 20 minutes.</span></span>

### <a name="code-samples"></a><span data-ttu-id="a24f3-169">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="a24f3-169">Code Samples</span></span>
<span data-ttu-id="a24f3-170">toomake 此程序會更容易，一組[程式碼範例](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)會提供可建立 SCIM web 服務端點，並示範自動佈建。</span><span class="sxs-lookup"><span data-stu-id="a24f3-170">toomake this process easier, a set of [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span></span> <span data-ttu-id="a24f3-171">其中一個範例是維護代表使用者和群組、具有逗號分隔值資料列檔案的提供者。</span><span class="sxs-lookup"><span data-stu-id="a24f3-171">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span></span>  <span data-ttu-id="a24f3-172">其他 hello 是 hello Amazon Web Services 識別和存取管理服務上運作的提供者。</span><span class="sxs-lookup"><span data-stu-id="a24f3-172">hello other is of a provider that operates on hello Amazon Web Services Identity and Access Management service.</span></span>  

<span data-ttu-id="a24f3-173">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="a24f3-173">**Prerequisites**</span></span>

* <span data-ttu-id="a24f3-174">Visual Studio 2013 或更新版本</span><span class="sxs-lookup"><span data-stu-id="a24f3-174">Visual Studio 2013 or later</span></span>
* [<span data-ttu-id="a24f3-175">Azure SDK for .NET</span><span class="sxs-lookup"><span data-stu-id="a24f3-175">Azure SDK for .NET</span></span>](https://azure.microsoft.com/downloads/)
* <span data-ttu-id="a24f3-176">Hello SCIM 端點作為支援 hello ASP.NET framework 4.5 toobe 的 Windows 電腦。</span><span class="sxs-lookup"><span data-stu-id="a24f3-176">Windows machine that supports hello ASP.NET framework 4.5 toobe used as hello SCIM endpoint.</span></span> <span data-ttu-id="a24f3-177">此電腦必須能夠從 hello 雲端存取</span><span class="sxs-lookup"><span data-stu-id="a24f3-177">This machine must be accessible from hello cloud</span></span>
* [<span data-ttu-id="a24f3-178">具有 Azure AD Premium 試用版或授權版的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a24f3-178">An Azure subscription with a trial or licensed version of Azure AD Premium</span></span>](https://azure.microsoft.com/services/active-directory/)
* <span data-ttu-id="a24f3-179">hello Amazon AWS 範例需要程式庫 hello [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html)。</span><span class="sxs-lookup"><span data-stu-id="a24f3-179">hello Amazon AWS sample requires libraries from hello [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span></span> <span data-ttu-id="a24f3-180">如需詳細資訊，請參閱 hello 讀我檔案包含 hello 範例檔。</span><span class="sxs-lookup"><span data-stu-id="a24f3-180">For more information, see hello README file included with hello sample.</span></span>

### <a name="getting-started"></a><span data-ttu-id="a24f3-181">開始使用</span><span class="sxs-lookup"><span data-stu-id="a24f3-181">Getting Started</span></span>
<span data-ttu-id="a24f3-182">hello 可接受佈建 SCIM 端點會從 Azure AD 要求最簡單方式 tooimplement toobuild 並部署 hello 輸出 hello 佈建的使用者 tooa 逗點分隔值 (CSV) 檔案的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="a24f3-182">hello easiest way tooimplement a SCIM endpoint that can accept provisioning requests from Azure AD is toobuild and deploy hello code sample that outputs hello provisioned users tooa comma-separated value (CSV) file.</span></span>

<span data-ttu-id="a24f3-183">**toocreate 範例 SCIM 端點：**</span><span class="sxs-lookup"><span data-stu-id="a24f3-183">**toocreate a sample SCIM endpoint:**</span></span>

1. <span data-ttu-id="a24f3-184">下載 hello 程式碼範例套件[https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span><span class="sxs-lookup"><span data-stu-id="a24f3-184">Download hello code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span></span>
2. <span data-ttu-id="a24f3-185">解壓縮 hello 封裝，並將它放在您的 Windows 電腦，例如 C:\AzureAD-BYOA-Provisioning-Samples\ 位置上。</span><span class="sxs-lookup"><span data-stu-id="a24f3-185">Unzip hello package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span></span>
3. <span data-ttu-id="a24f3-186">在這個資料夾中，啟動 Visual Studio 中的 hello FileProvisioningAgent 方案。</span><span class="sxs-lookup"><span data-stu-id="a24f3-186">In this folder, launch hello FileProvisioningAgent solution in Visual Studio.</span></span>
4. <span data-ttu-id="a24f3-187">選取**工具 > 程式庫套件管理員 > Package Manager Console**，並執行下列命令 hello FileProvisioningAgent 專案 tooresolve hello 解決方案參考的 hello:</span><span class="sxs-lookup"><span data-stu-id="a24f3-187">Select **Tools > Library Package Manager > Package Manager Console**, and execute hello following commands for hello FileProvisioningAgent project tooresolve hello solution references:</span></span>
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. <span data-ttu-id="a24f3-188">建置 hello FileProvisioningAgent 專案。</span><span class="sxs-lookup"><span data-stu-id="a24f3-188">Build hello FileProvisioningAgent project.</span></span>
6. <span data-ttu-id="a24f3-189">Hello 命令提示字元中啟動應用程式視窗 （以系統管理員身分），並使用 hello **cd**命令 toochange hello 目錄 tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug**資料夾。</span><span class="sxs-lookup"><span data-stu-id="a24f3-189">Launch hello Command Prompt application in Windows (as an Administrator), and use hello **cd** command toochange hello directory tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folder.</span></span>
7. <span data-ttu-id="a24f3-190">執行下列命令，以 hello prb: hello Windows 電腦的發生 IP 位址或網域名稱取代 < 位址 > hello:</span><span class="sxs-lookup"><span data-stu-id="a24f3-190">Run hello following command, replacing <ip-address> with hello IP address or domain name of hello Windows machine:</span></span>
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. <span data-ttu-id="a24f3-191">在 Windows 下**Windows 設定 > 網路和網際網路設定**，選取 hello **Windows 防火牆 > 進階設定**，並建立**輸入規則**，允許對內的存取 tooport 9000。</span><span class="sxs-lookup"><span data-stu-id="a24f3-191">In Windows under **Windows Settings > Network & Internet Settings**, select hello **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access tooport 9000.</span></span>
9. <span data-ttu-id="a24f3-192">如果 hello Windows 電腦之路由器的後面，hello 路由器需求設定 toobe tooperform 網路存取轉譯其連接埠 9000 之間所公開的 toohello 網際網路及連接埠 9000 hello Windows 電腦上的。</span><span class="sxs-lookup"><span data-stu-id="a24f3-192">If hello Windows machine is behind a router, hello router needs toobe configured tooperform Network Access Translation between its port 9000 that is exposed toohello internet, and port 9000 on hello Windows machine.</span></span> <span data-ttu-id="a24f3-193">這是必要的 Azure AD toobe 無法 tooaccess hello 雲端中的這個端點。</span><span class="sxs-lookup"><span data-stu-id="a24f3-193">This is required for Azure AD toobe able tooaccess this endpoint in hello cloud.</span></span>

<span data-ttu-id="a24f3-194">**tooregister hello 範例 SCIM 端點在 Azure AD 中：**</span><span class="sxs-lookup"><span data-stu-id="a24f3-194">**tooregister hello sample SCIM endpoint in Azure AD:**</span></span>

1. <span data-ttu-id="a24f3-195">登入太[hello Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a24f3-195">Sign in too[hello Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="a24f3-196">瀏覽過 * * Azure Active Directory > 企業應用程式，然後選取**新的應用程式 > 所有 > 非組件庫的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a24f3-196">Browse too**Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="a24f3-197">輸入您的應用程式的名稱，然後按一下**新增**圖示 toocreate 應用程式物件。</span><span class="sxs-lookup"><span data-stu-id="a24f3-197">Enter a name for your application, and click **Add** icon toocreate an app object.</span></span> <span data-ttu-id="a24f3-198">建立 hello 應用程式物件是預定的 toorepresent hello 目標應用程式會提供 tooand 實作單一登入，並不只是 hello SCIM 端點。</span><span class="sxs-lookup"><span data-stu-id="a24f3-198">hello application object created is intended toorepresent hello target app you would be provisioning tooand implementing single sign-on for, and not just hello SCIM endpoint.</span></span>
4. <span data-ttu-id="a24f3-199">在 hello 結果 畫面上，選取 hello**佈建**hello 左側資料行中的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a24f3-199">In hello resulting screen, select hello **Provisioning** tab in hello left column.</span></span>
5. <span data-ttu-id="a24f3-200">在 hello**佈建模式**功能表上，選取**自動**。</span><span class="sxs-lookup"><span data-stu-id="a24f3-200">In hello **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="a24f3-201">![][2]
  *圖 4： 設定 hello Azure 入口網站中佈建*</span><span class="sxs-lookup"><span data-stu-id="a24f3-201">![][2]
*Figure 4: Configuring provisioning in hello Azure portal*</span></span>
    
6. <span data-ttu-id="a24f3-202">在 hello**租用戶 URL**欄位中，輸入 hello 網際網路公開的 URL 和連接埠 SCIM 端點。</span><span class="sxs-lookup"><span data-stu-id="a24f3-202">In hello **Tenant URL** field, enter hello internet-exposed URL and port of your SCIM endpoint.</span></span> <span data-ttu-id="a24f3-203">這看起來應該像 http://testmachine.contoso.com:9000 或 http://<ip-address>:9000/，其中 < 位址 > 是 hello 網際網路公開 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a24f3-203">This would be something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is hello internet exposed IP address.</span></span>  
7. <span data-ttu-id="a24f3-204">如果 hello SCIM 端點需要簽發者以外的 Azure AD 中，從 OAuth 承載權杖，則複製 hello required OAuth 承載權杖到 hello 選擇性**密碼語彙基元**欄位。</span><span class="sxs-lookup"><span data-stu-id="a24f3-204">If hello SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy hello required OAuth bearer token into hello optional **Secret Token** field.</span></span> <span data-ttu-id="a24f3-205">如果此欄位保留空白，則 Azure AD 將在每個要求包含從 Azure AD 簽發的 OAuth 持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="a24f3-205">If this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="a24f3-206">使用 Azure AD 作為識別提供者的應用程式，可以驗證此 Azure AD 簽發的權杖。</span><span class="sxs-lookup"><span data-stu-id="a24f3-206">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="a24f3-207">按一下 hello**測試連接**按鈕 toohave Azure Active Directory 嘗試 tooconnect toohello SCIM 端點。</span><span class="sxs-lookup"><span data-stu-id="a24f3-207">Click hello **Test Connection** button toohave Azure Active Directory attempt tooconnect toohello SCIM endpoint.</span></span> <span data-ttu-id="a24f3-208">如果 hello 嘗試都失敗，則會顯示資訊時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="a24f3-208">If hello attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="a24f3-209">如果成功 hello 嘗試 tooconnect toohello 應用程式，然後按一下**儲存**toosave hello 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="a24f3-209">If hello attempts tooconnect toohello application succeed, then click **Save** toosave hello admin credentials.</span></span>
10. <span data-ttu-id="a24f3-210">在 hello**對應**區段中，有兩組可選取的屬性對應： 一個給使用者物件，一個群組物件。</span><span class="sxs-lookup"><span data-stu-id="a24f3-210">In hello **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="a24f3-211">選取同步處理每一個 tooreview hello 屬性從 Azure Active Directory tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a24f3-211">Select each one tooreview hello attributes that are synchronized from Azure Active Directory tooyour app.</span></span> <span data-ttu-id="a24f3-212">hello 做為所選取的屬性**比對**屬性是您的應用程式進行更新作業中使用的 toomatch hello 使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="a24f3-212">hello attributes selected as **Matching** properties are used toomatch hello users and groups in your app for update operations.</span></span> <span data-ttu-id="a24f3-213">選取 hello 儲存按鈕 toocommit 任何變更。</span><span class="sxs-lookup"><span data-stu-id="a24f3-213">Select hello Save button toocommit any changes.</span></span>
11. <span data-ttu-id="a24f3-214">在下**設定**，hello**範圍**欄位會定義哪些使用者或工作群組同步處理。</span><span class="sxs-lookup"><span data-stu-id="a24f3-214">Under **Settings**, hello **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="a24f3-215">選取 「 同步處理只指派使用者和群組 （建議選項） 只會同步使用者和群組指派在 hello**使用者和群組** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a24f3-215">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in hello **Users and groups** tab.</span></span>
12. <span data-ttu-id="a24f3-216">您的設定完成之後，請變更 hello**佈建狀態**太**上**。</span><span class="sxs-lookup"><span data-stu-id="a24f3-216">Once your configuration is complete, change hello **Provisioning Status** too**On**.</span></span>
13. <span data-ttu-id="a24f3-217">按一下**儲存**toostart hello Azure AD 佈建服務。</span><span class="sxs-lookup"><span data-stu-id="a24f3-217">Click **Save** toostart hello Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="a24f3-218">如果同步處理只會指派使用者和群組 （建議選項），是確定 tooselect hello**使用者和群組**索引標籤上，並指派 hello 使用者和/或您想 toosync 的群組。</span><span class="sxs-lookup"><span data-stu-id="a24f3-218">If syncing only assigned users and groups (recommended), be sure tooselect hello **Users and groups** tab and assign hello users and/or groups you wish toosync.</span></span>

<span data-ttu-id="a24f3-219">一旦啟動 hello 初始同步處理後，您可以使用 hello**稽核記錄檔**toomonitor 進度會顯示 hello 佈建應用程式上的服務所執行的所有動作索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="a24f3-219">Once hello initial synchronization has started, you can use hello **Audit logs** tab toomonitor progress, which shows all actions performed by hello provisioning service on your app.</span></span> <span data-ttu-id="a24f3-220">如需有關 tooread hello Azure AD 佈建的記錄方式的詳細資訊，請參閱[報告使用者自動帳戶佈建](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)。</span><span class="sxs-lookup"><span data-stu-id="a24f3-220">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

<span data-ttu-id="a24f3-221">hello 驗證 hello 範例的最後一個步驟是 tooopen hello Windows 電腦上的 TargetFile.csv 檔 hello \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="a24f3-221">hello final step in verifying hello sample is tooopen hello TargetFile.csv file in hello \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span></span> <span data-ttu-id="a24f3-222">一旦執行 hello 佈建程序時，此檔案會顯示 hello 詳細資料，所有的指派，並佈建使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="a24f3-222">Once hello provisioning process is run, this file shows hello details of all assigned and provisioned users and groups.</span></span>

### <a name="development-libraries"></a><span data-ttu-id="a24f3-223">開發程式庫</span><span class="sxs-lookup"><span data-stu-id="a24f3-223">Development libraries</span></span>
<span data-ttu-id="a24f3-224">toodevelop 您自己的 web 服務，並符合 toohello SCIM 規格，先熟悉下列程式庫，提供由 Microsoft toohelp 加速 hello 開發程序的 hello:</span><span class="sxs-lookup"><span data-stu-id="a24f3-224">toodevelop your own web service that conforms toohello SCIM specification, first familiarize yourself with hello following libraries provided by Microsoft toohelp accelerate hello development process:</span></span> 

1. <span data-ttu-id="a24f3-225">提供通用語言基礎結構 (CLI) 程式庫，可與以該基礎結構為基礎的語言 (例如 C#) 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="a24f3-225">Common Language Infrastructure (CLI) libraries are offered for use with languages based on that infrastructure, such as C#.</span></span> <span data-ttu-id="a24f3-226">這些程式庫，其中[Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/)，宣告的介面，Microsoft.SystemForCrossDomainIdentityManagement.IProvider，hello 下列圖例所示： A使用 hello 程式庫的開發人員會實作該介面，也就是，一般提供者的類別。</span><span class="sxs-lookup"><span data-stu-id="a24f3-226">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in hello following illustration:  A developer using hello libraries would implement that interface with a class that may be referred to, generically, as a provider.</span></span> <span data-ttu-id="a24f3-227">hello 程式庫可讓 hello 開發人員 toodeploy 符合 toohello SCIM 規格的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="a24f3-227">hello libraries enable hello developer toodeploy a web service that conforms toohello SCIM specification.</span></span> <span data-ttu-id="a24f3-228">hello web 服務可以被裝載在 Internet Information Services 或任何可執行的通用語言基礎結構組件。</span><span class="sxs-lookup"><span data-stu-id="a24f3-228">hello web service can be either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span></span> <span data-ttu-id="a24f3-229">要求會轉譯成呼叫 toohello 提供者的方法，會由 hello 某些身分識別存放區上的開發人員 toooperate 編寫程式。</span><span class="sxs-lookup"><span data-stu-id="a24f3-229">Request is translated into calls toohello provider’s methods, which would be programmed by hello developer toooperate on some identity store.</span></span>
  
  ![][3]
  
2. <span data-ttu-id="a24f3-230">[Express 路由處理常式](http://expressjs.com/guide/routing.html)供剖析 node.js 要求物件，代表所呼叫 （它是由定義 hello SCIM 規格），的進行 tooa node.js web 服務。</span><span class="sxs-lookup"><span data-stu-id="a24f3-230">[Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by hello SCIM specification), made tooa node.js web service.</span></span>   

### <a name="building-a-custom-scim-endpoint"></a><span data-ttu-id="a24f3-231">建置自訂 SCIM 端點</span><span class="sxs-lookup"><span data-stu-id="a24f3-231">Building a Custom SCIM Endpoint</span></span>
<span data-ttu-id="a24f3-232">使用 hello CLI 程式庫，使用這些程式庫的開發人員可以裝載任何可執行檔的通用語言基礎結構組件，或 Internet Information Services 中其服務。</span><span class="sxs-lookup"><span data-stu-id="a24f3-232">Using hello CLI libraries, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span></span> <span data-ttu-id="a24f3-233">以下是裝載在 hello 位址 http://localhost:9000 可執行組件內的服務範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="a24f3-233">Here is sample code for hosting a service within an executable assembly, at hello address http://localhost:9000:</span></span> 

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

<span data-ttu-id="a24f3-234">此服務必須要有 HTTP 位址和伺服器驗證憑證的 hello 的根憑證授權單位是 hello 下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="a24f3-234">This service must have an HTTP address and server authentication certificate of which hello root certification authority is one of hello following:</span></span> 

* <span data-ttu-id="a24f3-235">CNNIC</span><span class="sxs-lookup"><span data-stu-id="a24f3-235">CNNIC</span></span>
* <span data-ttu-id="a24f3-236">Comodo</span><span class="sxs-lookup"><span data-stu-id="a24f3-236">Comodo</span></span>
* <span data-ttu-id="a24f3-237">CyberTrust</span><span class="sxs-lookup"><span data-stu-id="a24f3-237">CyberTrust</span></span>
* <span data-ttu-id="a24f3-238">DigiCert</span><span class="sxs-lookup"><span data-stu-id="a24f3-238">DigiCert</span></span>
* <span data-ttu-id="a24f3-239">GeoTrust</span><span class="sxs-lookup"><span data-stu-id="a24f3-239">GeoTrust</span></span>
* <span data-ttu-id="a24f3-240">GlobalSign</span><span class="sxs-lookup"><span data-stu-id="a24f3-240">GlobalSign</span></span>
* <span data-ttu-id="a24f3-241">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="a24f3-241">Go Daddy</span></span>
* <span data-ttu-id="a24f3-242">Verisign</span><span class="sxs-lookup"><span data-stu-id="a24f3-242">Verisign</span></span>
* <span data-ttu-id="a24f3-243">WoSign</span><span class="sxs-lookup"><span data-stu-id="a24f3-243">WoSign</span></span>

<span data-ttu-id="a24f3-244">伺服器驗證憑證可以是使用 hello 網路殼層公用程式的 Windows 主機上的繫結的 tooa 連接埠：</span><span class="sxs-lookup"><span data-stu-id="a24f3-244">A server authentication certificate can be bound tooa port on a Windows host using hello network shell utility:</span></span> 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

<span data-ttu-id="a24f3-245">此處 hello 值提供給 hello certhash 引數都是 hello 憑證的指紋 hello，而 hello 值提供給 hello appid 引數是任意的全域唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="a24f3-245">Here, hello value provided for hello certhash argument is hello thumbprint of hello certificate, while hello value provided for hello appid argument is an arbitrary globally unique identifier.</span></span>  

<span data-ttu-id="a24f3-246">toohost hello Internet Information Services 中的服務，開發人員會使用類別 hello hello 組件的預設命名空間中的啟動建置 CLA 程式碼程式庫組件。</span><span class="sxs-lookup"><span data-stu-id="a24f3-246">toohost hello service within Internet Information Services, a developer would build a CLA code library assembly with a class named Startup in hello default namespace of hello assembly.</span></span>  <span data-ttu-id="a24f3-247">以下是這種類別的範例：</span><span class="sxs-lookup"><span data-stu-id="a24f3-247">Here is a sample of such a class:</span></span> 

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

### <a name="handling-endpoint-authentication"></a><span data-ttu-id="a24f3-248">處理端點驗證</span><span class="sxs-lookup"><span data-stu-id="a24f3-248">Handling endpoint authentication</span></span>
<span data-ttu-id="a24f3-249">來自 Azure Active Directory 的要求包括 OAuth 2.0 持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="a24f3-249">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span></span>   <span data-ttu-id="a24f3-250">任何服務接收 hello 要求應該驗證為 Azure Active Directory 代表 hello 必須是 Azure Active Directory 租用戶，如存取 toohello Azure Active Directory Graph web 服務的 hello 簽發者。</span><span class="sxs-lookup"><span data-stu-id="a24f3-250">Any service receiving hello request should authenticate hello issuer as being Azure Active Directory on behalf of hello expected Azure Active Directory tenant, for access toohello Azure Active Directory Graph web service.</span></span>  <span data-ttu-id="a24f3-251">Hello 語彙基元，在 hello 簽發者由 iss 宣告，像是 「 iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/"。</span><span class="sxs-lookup"><span data-stu-id="a24f3-251">In hello token, hello issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span></span>  <span data-ttu-id="a24f3-252">在此範例中，基底位址 hello 宣告值 hello https://sts.windows.net，會識別 Azure Active Directory，為 hello 簽發者、 時 hello cbb1a5ac-f33b-45fa-9bf5-f37db0fed422，相對位址區段的唯一識別碼 hello Azure Active代表的 hello 發行權杖的目錄租用戶。</span><span class="sxs-lookup"><span data-stu-id="a24f3-252">In this example, hello base address of hello claim value, https://sts.windows.net, identifies Azure Active Directory as hello issuer, while hello relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of hello Azure Active Directory tenant on behalf of which hello token was issued.</span></span>  <span data-ttu-id="a24f3-253">如果發行的存取 hello Azure Active Directory Graph web 服務，該服務，然後 hello 識別碼 hello 權杖 00000002-0000-0000-c000-000000000000，應該是 hello 語彙基元則 hello 值中宣告。</span><span class="sxs-lookup"><span data-stu-id="a24f3-253">If hello token was issued for accessing hello Azure Active Directory Graph web service, then hello identifier of that service, 00000002-0000-0000-c000-000000000000, should be in hello value of hello token’s aud claim.</span></span>  

<span data-ttu-id="a24f3-254">使用由 Microsoft 提供的建置 SCIM 服務的 hello CLA 程式庫的開發人員可以驗證要求，從 Azure Active Directory 使用 hello Microsoft.Owin.Security.ActiveDirectory 套件，依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a24f3-254">Developers using hello CLA libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using hello Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span></span> 

1. <span data-ttu-id="a24f3-255">提供者，讓它傳回 hello 服務啟動時呼叫方法 toobe 實作 hello Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior 屬性：</span><span class="sxs-lookup"><span data-stu-id="a24f3-255">In a provider, implement hello Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method toobe called whenever hello service is started:</span></span> 

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

2. <span data-ttu-id="a24f3-256">加入下列程式碼 toothat 方法 toohave hello hello 服務端點為 bearing 代表指定的租用戶，存取 toohello Azure AD Graph web 服務的 Azure Active Directory 所發出的權杖進行驗證的任何要求 tooany:</span><span class="sxs-lookup"><span data-stu-id="a24f3-256">Add hello following code toothat method toohave any request tooany of hello service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access toohello Azure AD Graph web service:</span></span> 

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
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute hello appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a><span data-ttu-id="a24f3-257">使用者和群組結構描述</span><span class="sxs-lookup"><span data-stu-id="a24f3-257">User and group schema</span></span>
<span data-ttu-id="a24f3-258">Azure Active Directory 可以佈建兩種類型的資源 tooSCIM web 服務。</span><span class="sxs-lookup"><span data-stu-id="a24f3-258">Azure Active Directory can provision two types of resources tooSCIM web services.</span></span>  <span data-ttu-id="a24f3-259">這些類型的資源是使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="a24f3-259">Those types of resources are users and groups.</span></span>  

<span data-ttu-id="a24f3-260">使用者資源由識別碼所識別 hello 結構描述，urn: ietf:params:scim:schemas:extension:enterprise:2.0:User，隨附於此通訊協定規格： http://tools.ietf.org/html/draft-ietf-scim-core-schema。</span><span class="sxs-lookup"><span data-stu-id="a24f3-260">User resources are identified by hello schema identifier, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span></span>  <span data-ttu-id="a24f3-261">資料表 1，底下提供 hello 預設對應的 hello 屬性的 urn: ietf:params:scim:schemas:extension:enterprise:2.0:User 資源的 Azure Active Directory toohello 屬性中的使用者。</span><span class="sxs-lookup"><span data-stu-id="a24f3-261">hello default mapping of hello attributes of users in Azure Active Directory toohello attributes of urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resources is provided in table 1, below.</span></span>  

<span data-ttu-id="a24f3-262">群組資源會 hello 結構描述識別碼識別，http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group。</span><span class="sxs-lookup"><span data-stu-id="a24f3-262">Group resources are identified by hello schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  <span data-ttu-id="a24f3-263">資料表 2 的下方顯示 hello 預設對應的 Azure Active Directory toohello 屬性在資源群組的 http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group 的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="a24f3-263">Table 2, below, shows hello default mapping of hello attributes of groups in Azure Active Directory toohello attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span></span>  

### <a name="table-1-default-user-attribute-mapping"></a><span data-ttu-id="a24f3-264">表 1：預設使用者屬性對應</span><span class="sxs-lookup"><span data-stu-id="a24f3-264">Table 1: Default user attribute mapping</span></span>
| <span data-ttu-id="a24f3-265">Azure Active Directory 使用者</span><span class="sxs-lookup"><span data-stu-id="a24f3-265">Azure Active Directory user</span></span> | <span data-ttu-id="a24f3-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span><span class="sxs-lookup"><span data-stu-id="a24f3-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span></span> |
| --- | --- |
| <span data-ttu-id="a24f3-267">IsSoftDeleted</span><span class="sxs-lookup"><span data-stu-id="a24f3-267">IsSoftDeleted</span></span> |<span data-ttu-id="a24f3-268">作用中</span><span class="sxs-lookup"><span data-stu-id="a24f3-268">active</span></span> |
| <span data-ttu-id="a24f3-269">displayName</span><span class="sxs-lookup"><span data-stu-id="a24f3-269">displayName</span></span> |<span data-ttu-id="a24f3-270">displayName</span><span class="sxs-lookup"><span data-stu-id="a24f3-270">displayName</span></span> |
| <span data-ttu-id="a24f3-271">Facsimile-TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="a24f3-271">Facsimile-TelephoneNumber</span></span> |<span data-ttu-id="a24f3-272">phoneNumbers[type eq "fax"].value</span><span class="sxs-lookup"><span data-stu-id="a24f3-272">phoneNumbers[type eq "fax"].value</span></span> |
| <span data-ttu-id="a24f3-273">givenName</span><span class="sxs-lookup"><span data-stu-id="a24f3-273">givenName</span></span> |<span data-ttu-id="a24f3-274">name.givenName</span><span class="sxs-lookup"><span data-stu-id="a24f3-274">name.givenName</span></span> |
| <span data-ttu-id="a24f3-275">jobTitle</span><span class="sxs-lookup"><span data-stu-id="a24f3-275">jobTitle</span></span> |<span data-ttu-id="a24f3-276">title</span><span class="sxs-lookup"><span data-stu-id="a24f3-276">title</span></span> |
| <span data-ttu-id="a24f3-277">mail</span><span class="sxs-lookup"><span data-stu-id="a24f3-277">mail</span></span> |<span data-ttu-id="a24f3-278">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="a24f3-278">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="a24f3-279">mailNickname</span><span class="sxs-lookup"><span data-stu-id="a24f3-279">mailNickname</span></span> |<span data-ttu-id="a24f3-280">externalId</span><span class="sxs-lookup"><span data-stu-id="a24f3-280">externalId</span></span> |
| <span data-ttu-id="a24f3-281">manager</span><span class="sxs-lookup"><span data-stu-id="a24f3-281">manager</span></span> |<span data-ttu-id="a24f3-282">manager</span><span class="sxs-lookup"><span data-stu-id="a24f3-282">manager</span></span> |
| <span data-ttu-id="a24f3-283">mobile</span><span class="sxs-lookup"><span data-stu-id="a24f3-283">mobile</span></span> |<span data-ttu-id="a24f3-284">phoneNumbers[type eq "mobile"].value</span><span class="sxs-lookup"><span data-stu-id="a24f3-284">phoneNumbers[type eq "mobile"].value</span></span> |
| <span data-ttu-id="a24f3-285">objectId</span><span class="sxs-lookup"><span data-stu-id="a24f3-285">objectId</span></span> |<span data-ttu-id="a24f3-286">id</span><span class="sxs-lookup"><span data-stu-id="a24f3-286">id</span></span> |
| <span data-ttu-id="a24f3-287">postalCode</span><span class="sxs-lookup"><span data-stu-id="a24f3-287">postalCode</span></span> |<span data-ttu-id="a24f3-288">addresses[type eq "work"].postalCode</span><span class="sxs-lookup"><span data-stu-id="a24f3-288">addresses[type eq "work"].postalCode</span></span> |
| <span data-ttu-id="a24f3-289">proxy-Addresses</span><span class="sxs-lookup"><span data-stu-id="a24f3-289">proxy-Addresses</span></span> |<span data-ttu-id="a24f3-290">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="a24f3-290">emails[type eq "other"].Value</span></span> |
| <span data-ttu-id="a24f3-291">physical-Delivery-OfficeName</span><span class="sxs-lookup"><span data-stu-id="a24f3-291">physical-Delivery-OfficeName</span></span> |<span data-ttu-id="a24f3-292">addresses[type eq "other"].Formatted</span><span class="sxs-lookup"><span data-stu-id="a24f3-292">addresses[type eq "other"].Formatted</span></span> |
| <span data-ttu-id="a24f3-293">streetAddress</span><span class="sxs-lookup"><span data-stu-id="a24f3-293">streetAddress</span></span> |<span data-ttu-id="a24f3-294">addresses[type eq "work"].streetAddress</span><span class="sxs-lookup"><span data-stu-id="a24f3-294">addresses[type eq "work"].streetAddress</span></span> |
| <span data-ttu-id="a24f3-295">surname</span><span class="sxs-lookup"><span data-stu-id="a24f3-295">surname</span></span> |<span data-ttu-id="a24f3-296">name.familyName</span><span class="sxs-lookup"><span data-stu-id="a24f3-296">name.familyName</span></span> |
| <span data-ttu-id="a24f3-297">telephone-Number</span><span class="sxs-lookup"><span data-stu-id="a24f3-297">telephone-Number</span></span> |<span data-ttu-id="a24f3-298">phoneNumbers[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="a24f3-298">phoneNumbers[type eq "work"].value</span></span> |
| <span data-ttu-id="a24f3-299">user-PrincipalName</span><span class="sxs-lookup"><span data-stu-id="a24f3-299">user-PrincipalName</span></span> |<span data-ttu-id="a24f3-300">userName</span><span class="sxs-lookup"><span data-stu-id="a24f3-300">userName</span></span> |

### <a name="table-2-default-group-attribute-mapping"></a><span data-ttu-id="a24f3-301">表 2：預設群組屬性對應</span><span class="sxs-lookup"><span data-stu-id="a24f3-301">Table 2: Default group attribute mapping</span></span>
| <span data-ttu-id="a24f3-302">Azure Active Directory 群組</span><span class="sxs-lookup"><span data-stu-id="a24f3-302">Azure Active Directory group</span></span> | <span data-ttu-id="a24f3-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span><span class="sxs-lookup"><span data-stu-id="a24f3-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span></span> |
| --- | --- |
| <span data-ttu-id="a24f3-304">displayName</span><span class="sxs-lookup"><span data-stu-id="a24f3-304">displayName</span></span> |<span data-ttu-id="a24f3-305">externalId</span><span class="sxs-lookup"><span data-stu-id="a24f3-305">externalId</span></span> |
| <span data-ttu-id="a24f3-306">mail</span><span class="sxs-lookup"><span data-stu-id="a24f3-306">mail</span></span> |<span data-ttu-id="a24f3-307">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="a24f3-307">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="a24f3-308">mailNickname</span><span class="sxs-lookup"><span data-stu-id="a24f3-308">mailNickname</span></span> |<span data-ttu-id="a24f3-309">displayName</span><span class="sxs-lookup"><span data-stu-id="a24f3-309">displayName</span></span> |
| <span data-ttu-id="a24f3-310">members</span><span class="sxs-lookup"><span data-stu-id="a24f3-310">members</span></span> |<span data-ttu-id="a24f3-311">members</span><span class="sxs-lookup"><span data-stu-id="a24f3-311">members</span></span> |
| <span data-ttu-id="a24f3-312">objectId</span><span class="sxs-lookup"><span data-stu-id="a24f3-312">objectId</span></span> |<span data-ttu-id="a24f3-313">id</span><span class="sxs-lookup"><span data-stu-id="a24f3-313">id</span></span> |
| <span data-ttu-id="a24f3-314">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="a24f3-314">proxyAddresses</span></span> |<span data-ttu-id="a24f3-315">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="a24f3-315">emails[type eq "other"].Value</span></span> |

## <a name="user-provisioning-and-de-provisioning"></a><span data-ttu-id="a24f3-316">使用者佈建和取消佈建</span><span class="sxs-lookup"><span data-stu-id="a24f3-316">User provisioning and de-provisioning</span></span>
<span data-ttu-id="a24f3-317">下列圖例顯示 hello 訊息，而 Azure Active Directory 會將 tooa SCIM 服務 toomanage hello 生命週期的使用者傳送另一個身分識別存放區中的 hello。</span><span class="sxs-lookup"><span data-stu-id="a24f3-317">hello following illustration shows hello messages that Azure Active Directory sends tooa SCIM service toomanage hello lifecycle of a user in another identity store.</span></span> <span data-ttu-id="a24f3-318">hello 圖表也會示範如何實作使用 hello CLI 程式庫的 SCIM 服務由 Microsoft 提供建置這類服務會將這些要求轉譯成提供者的呼叫 toohello 方法。</span><span class="sxs-lookup"><span data-stu-id="a24f3-318">hello diagram also shows how a SCIM service implemented using hello CLI libraries provided by Microsoft for building such services translate those requests into calls toohello methods of a provider.</span></span>  

<span data-ttu-id="a24f3-319">![][4]
圖 5：使用者佈建和取消佈建順序</span><span class="sxs-lookup"><span data-stu-id="a24f3-319">![][4]
*Figure 5: User provisioning and de-provisioning sequence*</span></span>

1. <span data-ttu-id="a24f3-320">Azure Active Directory 查詢 hello 使用者的服務與 Azure AD 中的比對使用者的 hello mailNickname 屬性的值為 externalId 屬性值。</span><span class="sxs-lookup"><span data-stu-id="a24f3-320">Azure Active Directory queries hello service for a user with an externalId attribute value matching hello mailNickname attribute value of a user in Azure AD.</span></span> <span data-ttu-id="a24f3-321">hello 查詢會以超文字傳輸通訊協定 (HTTP) 的要求，例如此範例中，其中 jyoung 是 Azure Active Directory 中使用者的郵件別名的範例：</span><span class="sxs-lookup"><span data-stu-id="a24f3-321">hello query is expressed as a Hypertext Transfer Protocol (HTTP) request such as this example, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span></span> 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="a24f3-322">如果使用實作 SCIM 服務由 Microsoft 提供的 hello 通用語言基礎結構程式庫來建置 hello 服務時，則 hello 要求時轉譯為呼叫 toohello hello 服務提供者的查詢方法。</span><span class="sxs-lookup"><span data-stu-id="a24f3-322">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Query method of hello service’s provider.</span></span>  <span data-ttu-id="a24f3-323">以下是 hello 該方法的簽章：</span><span class="sxs-lookup"><span data-stu-id="a24f3-323">Here is hello signature of that method:</span></span> 
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
  <span data-ttu-id="a24f3-324">以下是 hello hello Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters 介面定義：</span><span class="sxs-lookup"><span data-stu-id="a24f3-324">Here is hello definition of hello Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span></span> 
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
  <span data-ttu-id="a24f3-325">在下列範例，具有給定值為 hello externalId 屬性查詢使用者的 hello，hello 傳遞 toohello 查詢方法的引數的值為：</span><span class="sxs-lookup"><span data-stu-id="a24f3-325">In hello following sample of a query for a user with a given value for hello externalId attribute, values of hello arguments passed toohello Query method are:</span></span> 
  * <span data-ttu-id="a24f3-326">parameters.AlternateFilters.Count: 1</span><span class="sxs-lookup"><span data-stu-id="a24f3-326">parameters.AlternateFilters.Count: 1</span></span>
  * <span data-ttu-id="a24f3-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span><span class="sxs-lookup"><span data-stu-id="a24f3-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span></span>
  * <span data-ttu-id="a24f3-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="a24f3-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="a24f3-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span><span class="sxs-lookup"><span data-stu-id="a24f3-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span></span>
  * <span data-ttu-id="a24f3-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span><span class="sxs-lookup"><span data-stu-id="a24f3-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span></span> 

2. <span data-ttu-id="a24f3-331">如果 hello 回應 tooa 查詢 toohello web 服務的使用者具有 externalId 屬性值符合使用者的 hello mailNickname 屬性的值不會傳回任何使用者，Azure Active Directory 要求該 hello 服務佈建使用者對應 toohello 其中一個 Azure Active Directory 中。</span><span class="sxs-lookup"><span data-stu-id="a24f3-331">If hello response tooa query toohello web service for a user with an externalId attribute value that matches hello mailNickname attribute value of a user does not return any users, then Azure Active Directory requests that hello service provision a user corresponding toohello one in Azure Active Directory.</span></span>  <span data-ttu-id="a24f3-332">以下是這類要求的範例：</span><span class="sxs-lookup"><span data-stu-id="a24f3-332">Here is an example of such a request:</span></span> 
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
  <span data-ttu-id="a24f3-333">hello 實作 SCIM 服務由 Microsoft 提供的通用語言基礎結構程式庫會將該要求轉譯成呼叫 toohello hello 服務提供者的建立方法。</span><span class="sxs-lookup"><span data-stu-id="a24f3-333">hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call toohello Create method of hello service’s provider.</span></span>  <span data-ttu-id="a24f3-334">Create 方法 hello 具有此簽章：</span><span class="sxs-lookup"><span data-stu-id="a24f3-334">hello Create method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="a24f3-335">要求 tooprovision 使用者，在 hello hello 資源引數是 hello Microsoft.SystemForCrossDomainIdentityManagement 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="a24f3-335">In a request tooprovision a user, hello value of hello resource argument is an instance of hello Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="a24f3-336">Hello Microsoft.SystemForCrossDomainIdentityManagement.Schemas 文件庫中定義的 Core2EnterpriseUser 類別。</span><span class="sxs-lookup"><span data-stu-id="a24f3-336">Core2EnterpriseUser class, defined in hello Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span></span>  <span data-ttu-id="a24f3-337">如果 hello 要求 tooprovision hello 使用者成功，則 hello hello 方法的實作是預期的 tooreturn hello Microsoft.SystemForCrossDomainIdentityManagement 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="a24f3-337">If hello request tooprovision hello user succeeds, then hello implementation of hello method is expected tooreturn an instance of hello Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="a24f3-338">Core2EnterpriseUser 類別，具有 hello 屬性值的 hello 識別碼設定 toohello hello 新佈建使用者的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="a24f3-338">Core2EnterpriseUser class, with hello value of hello Identifier property set toohello unique identifier of hello newly provisioned user.</span></span>  

3. <span data-ttu-id="a24f3-339">tooupdate 已知 tooexist fronted 由 SCIM，Azure Active Directory 會繼續進行這類要求 hello 服務要求 hello 目前狀態，該使用者的身分識別存放區中的使用者：</span><span class="sxs-lookup"><span data-stu-id="a24f3-339">tooupdate a user known tooexist in an identity store fronted by an SCIM, Azure Active Directory proceeds by requesting hello current state of that user from hello service with a request such as:</span></span> 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="a24f3-340">在服務中使用 hello 實作 SCIM 服務由 Microsoft 提供的通用語言基礎結構程式庫所建置，hello 要求會轉譯成呼叫 toohello hello 服務提供者的擷取方法。</span><span class="sxs-lookup"><span data-stu-id="a24f3-340">In a service built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, hello request is translated into a call toohello Retrieve method of hello service’s provider.</span></span>  <span data-ttu-id="a24f3-341">以下是 hello hello 擷取方法簽章：</span><span class="sxs-lookup"><span data-stu-id="a24f3-341">Here is hello signature of hello Retrieve method:</span></span> 
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
  <span data-ttu-id="a24f3-342">在 hello 範例中的使用者要求 tooretrieve hello 目前狀態，hello hello hello 物件提供給 hello hello 參數引數的值屬性的值如下：</span><span class="sxs-lookup"><span data-stu-id="a24f3-342">In hello example of a request tooretrieve hello current state of a user, hello values of hello properties of hello object provided as hello value of hello parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="a24f3-343">識別碼："54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="a24f3-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="a24f3-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="a24f3-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

4. <span data-ttu-id="a24f3-345">如果不論 hello hello 身分識別存放區中的 hello 參考屬性的目前值 fronted 所參考屬性 toobe 更新，然後 Azure Active Directory 查詢 hello 服務 toodetermine hello 服務就會與 hello 該屬性的值在 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="a24f3-345">If a reference attribute is toobe updated, then Azure Active Directory queries hello service toodetermine whether or not hello current value of hello reference attribute in hello identity store fronted by hello service already matches hello value of that attribute in Azure Active Directory.</span></span> <span data-ttu-id="a24f3-346">對於使用者而言 hello 的目前值會以這種方式查詢的唯一屬性是 hello 的 hello 經理屬性。</span><span class="sxs-lookup"><span data-stu-id="a24f3-346">For users, hello only attribute of which hello current value is queried in this way is hello manager attribute.</span></span> <span data-ttu-id="a24f3-347">以下是要求 toodetermine 的範例，特定的使用者物件的 hello 經理屬性目前已為某個值是否：</span><span class="sxs-lookup"><span data-stu-id="a24f3-347">Here is an example of a request toodetermine whether hello manager attribute of a particular user object currently has a certain value:</span></span> 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="a24f3-348">hello 值 hello 屬性查詢參數的識別碼，表示如果使用者物件存在，可滿足 hello 運算式提供給 hello 值 hello 篩選查詢參數，則 hello 服務是預期的 urn: ietf:params:scim:schemas toorespond:核心： 2.0:User 或 urn: ietf:params:scim:schemas:extension:enterprise:2.0:User 資源，包括只有 hello 該資源的 id 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="a24f3-348">hello value of hello attributes query parameter, id, signifies that if a user object exists that satisfies hello expression provided as hello value of hello filter query parameter, then hello service is expected toorespond with a urn:ietf:params:scim:schemas:core:2.0:User or urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resource, including only hello value of that resource’s id attribute.</span></span>  <span data-ttu-id="a24f3-349">hello 值 hello**識別碼**已知 toohello 要求者的屬性。</span><span class="sxs-lookup"><span data-stu-id="a24f3-349">hello value of hello **id** attribute is known toohello requestor.</span></span> <span data-ttu-id="a24f3-350">它包含在 hello 值 hello 篩選查詢參數。hello 目的要求它是實際 toorequest 滿足 hello 篩選運算式，以表示有這類物件存在資源的最小表示法。</span><span class="sxs-lookup"><span data-stu-id="a24f3-350">It is included in hello value of hello filter query parameter; hello purpose of asking for it is actually toorequest a minimal representation of a resource that satisfying hello filter expression as an indication of whether or not any such object exists.</span></span>   

  <span data-ttu-id="a24f3-351">如果使用實作 SCIM 服務由 Microsoft 提供的 hello 通用語言基礎結構程式庫來建置 hello 服務時，則 hello 要求時轉譯為呼叫 toohello hello 服務提供者的查詢方法。</span><span class="sxs-lookup"><span data-stu-id="a24f3-351">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Query method of hello service’s provider.</span></span> <span data-ttu-id="a24f3-352">hello hello hello 物件提供給 hello hello 參數引數的值屬性的值如下所示：</span><span class="sxs-lookup"><span data-stu-id="a24f3-352">hello value of hello properties of hello object provided as hello value of hello parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="a24f3-353">parameters.AlternateFilters.Count: 2</span><span class="sxs-lookup"><span data-stu-id="a24f3-353">parameters.AlternateFilters.Count: 2</span></span>
  * <span data-ttu-id="a24f3-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span><span class="sxs-lookup"><span data-stu-id="a24f3-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span></span>
  * <span data-ttu-id="a24f3-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="a24f3-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="a24f3-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="a24f3-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="a24f3-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="a24f3-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span></span>
  * <span data-ttu-id="a24f3-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="a24f3-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="a24f3-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span><span class="sxs-lookup"><span data-stu-id="a24f3-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span></span>
  * <span data-ttu-id="a24f3-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span><span class="sxs-lookup"><span data-stu-id="a24f3-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span></span>
  * <span data-ttu-id="a24f3-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="a24f3-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

  <span data-ttu-id="a24f3-362">在這裡，hello hello 索引 x 值可能是 0 和 hello hello 索引的 y 值可能是 1，或 hello x 值的值可能是 1 和 hello y 的值可能是 0，hello hello filter 查詢參數運算式中的 hello 順序而定。</span><span class="sxs-lookup"><span data-stu-id="a24f3-362">Here, hello value of hello index x may be 0 and hello value of hello index y may be 1, or hello value of x may be 1 and hello value of y may be 0, depending on hello order of hello expressions of hello filter query parameter.</span></span>   

5. <span data-ttu-id="a24f3-363">從 Azure Active Directory tooan SCIM 服務 tooupdate 使用者要求的範例如下：</span><span class="sxs-lookup"><span data-stu-id="a24f3-363">Here is an example of a request from Azure Active Directory tooan SCIM service tooupdate a user:</span></span> 
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
  <span data-ttu-id="a24f3-364">hello Microsoft 通用語言基礎結構程式庫實作 SCIM 服務會將 hello 要求轉譯成呼叫 toohello hello 服務提供者的更新方法。</span><span class="sxs-lookup"><span data-stu-id="a24f3-364">hello Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate hello request into a call toohello Update method of hello service’s provider.</span></span> <span data-ttu-id="a24f3-365">以下是 hello hello Update 方法簽章：</span><span class="sxs-lookup"><span data-stu-id="a24f3-365">Here is hello signature of hello Update method:</span></span> 
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
    <span data-ttu-id="a24f3-366">在 hello 範例中的要求 tooupdate 使用者，提供給 hello 修補程式引數的 hello 值 hello 物件會具有這些屬性值：</span><span class="sxs-lookup"><span data-stu-id="a24f3-366">In hello example of a request tooupdate a user, hello object provided as hello value of hello patch argument has these property values:</span></span> 
  
  * <span data-ttu-id="a24f3-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="a24f3-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="a24f3-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="a24f3-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>
  * <span data-ttu-id="a24f3-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span><span class="sxs-lookup"><span data-stu-id="a24f3-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span></span>
  * <span data-ttu-id="a24f3-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span><span class="sxs-lookup"><span data-stu-id="a24f3-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span></span>
  * <span data-ttu-id="a24f3-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="a24f3-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span></span>
  * <span data-ttu-id="a24f3-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span><span class="sxs-lookup"><span data-stu-id="a24f3-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span></span>
  * <span data-ttu-id="a24f3-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="a24f3-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span></span>
  * <span data-ttu-id="a24f3-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="a24f3-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span></span>

6. <span data-ttu-id="a24f3-375">toode 佈建的使用者身分識別存放區 fronted SCIM 服務，例如 Azure AD 傳送的要求：</span><span class="sxs-lookup"><span data-stu-id="a24f3-375">toode-provision a user from an identity store fronted by an SCIM service, Azure AD sends a request such as:</span></span> 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="a24f3-376">如果使用實作 SCIM 服務由 Microsoft 提供的 hello 通用語言基礎結構程式庫來建置 hello 服務時，則 hello 要求時轉譯為呼叫 toohello hello 服務提供者的 Delete 方法。</span><span class="sxs-lookup"><span data-stu-id="a24f3-376">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Delete method of hello service’s provider.</span></span>   <span data-ttu-id="a24f3-377">該方法具有此簽章：</span><span class="sxs-lookup"><span data-stu-id="a24f3-377">That method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="a24f3-378">hello 物件提供給 hello hello resourceIdentifier 引數的值具有這些屬性值在 hello 範例中的要求 toode 佈建使用者：</span><span class="sxs-lookup"><span data-stu-id="a24f3-378">hello object provided as hello value of hello resourceIdentifier argument has these property values in hello example of a request toode-provision a user:</span></span> 
  
  * <span data-ttu-id="a24f3-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="a24f3-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="a24f3-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="a24f3-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

## <a name="group-provisioning-and-de-provisioning"></a><span data-ttu-id="a24f3-381">群組佈建和取消佈建</span><span class="sxs-lookup"><span data-stu-id="a24f3-381">Group provisioning and de-provisioning</span></span>
<span data-ttu-id="a24f3-382">下列圖例顯示 hello 訊息，而 Azure AcD 傳送 tooa SCIM 服務 toomanage hello 生命週期的群組，另一個身分識別存放區中的 hello。</span><span class="sxs-lookup"><span data-stu-id="a24f3-382">hello following illustration shows hello messages that Azure AcD sends tooa SCIM service toomanage hello lifecycle of a group in another identity store.</span></span>  <span data-ttu-id="a24f3-383">這些郵件差異 hello 訊息相關 toousers 三種方式：</span><span class="sxs-lookup"><span data-stu-id="a24f3-383">Those messages differ from hello messages pertaining toousers in three ways:</span></span> 

* <span data-ttu-id="a24f3-384">hello 結構描述的群組資源會被視為 http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group。</span><span class="sxs-lookup"><span data-stu-id="a24f3-384">hello schema of a group resource is identified as http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  
* <span data-ttu-id="a24f3-385">Tooretrieve 群組中保證該 hello 成員屬性的要求是 toobe 排除回應 toohello 要求中提供的任何資源。</span><span class="sxs-lookup"><span data-stu-id="a24f3-385">Requests tooretrieve groups stipulate that hello members attribute is toobe excluded from any resource provided in response toohello request.</span></span>  
* <span data-ttu-id="a24f3-386">要求 toodetermine 參考屬性是否具有特定值，會要求有關 hello 成員屬性。</span><span class="sxs-lookup"><span data-stu-id="a24f3-386">Requests toodetermine whether a reference attribute has a certain value are requests about hello members attribute.</span></span>  

<span data-ttu-id="a24f3-387">![][5]
圖 6：群組佈建和取消佈建順序</span><span class="sxs-lookup"><span data-stu-id="a24f3-387">![][5]
*Figure 6: Group provisioning and de-provisioning sequence*</span></span>

## <a name="related-articles"></a><span data-ttu-id="a24f3-388">相關文章</span><span class="sxs-lookup"><span data-stu-id="a24f3-388">Related articles</span></span>
* [<span data-ttu-id="a24f3-389">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="a24f3-389">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="a24f3-390">自動化使用者佈建/取消佈建 tooSaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="a24f3-390">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="a24f3-391">自訂使用者佈建的屬性對應</span><span class="sxs-lookup"><span data-stu-id="a24f3-391">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="a24f3-392">撰寫屬性對應的運算式</span><span class="sxs-lookup"><span data-stu-id="a24f3-392">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="a24f3-393">適用於使用者佈建的範圍篩選器</span><span class="sxs-lookup"><span data-stu-id="a24f3-393">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="a24f3-394">帳戶佈建通知</span><span class="sxs-lookup"><span data-stu-id="a24f3-394">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="a24f3-395">如何教學課程清單 tooIntegrate SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="a24f3-395">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
