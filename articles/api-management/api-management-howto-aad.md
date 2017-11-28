---
title: "使用 Azure Active Directory Azure API 管理 aaaAuthorize 開發人員帳戶 |Microsoft 文件"
description: "深入了解如何使用 API 管理中的 Azure Active Directory tooauthorize 使用者。"
services: api-management
documentationcenter: API Management
author: steved0x
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ebf5447a509a47df35e4262138bfcf423cb1dd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a><span data-ttu-id="c2314-103">如何 tooauthorize 開發人員帳戶使用 Azure Active Directory 在 Azure API 管理</span><span class="sxs-lookup"><span data-stu-id="c2314-103">How tooauthorize developer accounts using Azure Active Directory in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="c2314-104">概觀</span><span class="sxs-lookup"><span data-stu-id="c2314-104">Overview</span></span>
<span data-ttu-id="c2314-105">本指南也說明如何 tooenable 存取 toohello 開發人員入口網站，讓使用者從 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="c2314-105">This guide shows you how tooenable access toohello developer portal for users from Azure Active Directory.</span></span> <span data-ttu-id="c2314-106">本指南也會顯示如何加入外部群組包含 Azure Active Directory 使用者 toomanage 群組 hello Azure Active Directory 使用者。</span><span class="sxs-lookup"><span data-stu-id="c2314-106">This guide also shows you how toomanage groups of Azure Active Directory users by adding external groups that contain hello users of an Azure Active Directory.</span></span>

> <span data-ttu-id="c2314-107">本指南中步驟 toocomplete hello 必須先有 Azure Active Directory 中哪些 toocreate 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2314-107">toocomplete hello steps in this guide you must first have an Azure Active Directory in which toocreate an application.</span></span>
> 
> 

## <a name="how-tooauthorize-developer-accounts-using-azure-active-directory"></a><span data-ttu-id="c2314-108">如何 tooauthorize 開發人員帳戶使用 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2314-108">How tooauthorize developer accounts using Azure Active Directory</span></span>
<span data-ttu-id="c2314-109">tooget 啟動，按一下**發行者入口網站**hello API 管理服務的 Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="c2314-109">tooget started, click **Publisher portal** in hello Azure portal for your API Management service.</span></span> <span data-ttu-id="c2314-110">這會帶您 toohello API 管理發行者入口網站。</span><span class="sxs-lookup"><span data-stu-id="c2314-110">This takes you toohello API Management publisher portal.</span></span>

![發行者入口網站][api-management-management-console]

> <span data-ttu-id="c2314-112">如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[開始使用 Azure API 管理][Get started with Azure API Management]教學課程。</span><span class="sxs-lookup"><span data-stu-id="c2314-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="c2314-113">按一下**安全性**從 hello **API 管理**hello 左側，按一下功能表**外部識別**。</span><span class="sxs-lookup"><span data-stu-id="c2314-113">Click **Security** from hello **API Management** menu on hello left and click **External Identities**.</span></span>

![外部身分識別][api-management-security-external-identities]

<span data-ttu-id="c2314-115">按一下 [ **Azure Active Directory**]。</span><span class="sxs-lookup"><span data-stu-id="c2314-115">Click **Azure Active Directory**.</span></span> <span data-ttu-id="c2314-116">請記下 hello**重新導向 URL**和切換 tooyour Azure Active Directory hello Azure 傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="c2314-116">Make a note of hello **Redirect URL** and switch over tooyour Azure Active Directory in hello Azure Classic Portal.</span></span>

![外部身分識別][api-management-security-aad-new]

<span data-ttu-id="c2314-118">按一下 hello**新增**按鈕 toocreate 新的 Azure Active Directory 應用程式，然後選擇**加入我組織正在開發的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c2314-118">Click hello **Add** button toocreate a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![加入新的 Azure Active Directory 應用程式][api-management-new-aad-application-menu]

<span data-ttu-id="c2314-120">輸入的名稱 hello 應用程式中，選取**Web 應用程式和/或 Web API**，然後按一下 下一步按鈕的 hello。</span><span class="sxs-lookup"><span data-stu-id="c2314-120">Enter a name for hello application, select **Web application and/or Web API**, and click hello next button.</span></span>

![新 Azure Active Directory 應用程式][api-management-new-aad-application-1]

<span data-ttu-id="c2314-122">如**登入 URL**，輸入 hello 登入您的開發人員入口網站的 URL。</span><span class="sxs-lookup"><span data-stu-id="c2314-122">For **Sign-on URL**, enter hello sign-on URL of your developer portal.</span></span> <span data-ttu-id="c2314-123">在此範例中，hello**登入 URL**是`https://aad03.portal.current.int-azure-api.net/signin`。</span><span class="sxs-lookup"><span data-stu-id="c2314-123">In this example, hello **Sign-on URL** is `https://aad03.portal.current.int-azure-api.net/signin`.</span></span> 

<span data-ttu-id="c2314-124">Hello**應用程式識別碼 URL**、 hello Azure Active Directory 中，輸入 hello 預設定義域或自訂網域，然後附加唯一字串 tooit。</span><span class="sxs-lookup"><span data-stu-id="c2314-124">For hello **App ID URL**, enter either hello default domain or a custom domain for hello Azure Active Directory, and append a unique string tooit.</span></span> <span data-ttu-id="c2314-125">在此範例中，hello 的預設網域**https://contoso5api.onmicrosoft.com**搭配 hello 尾碼**/api**指定。</span><span class="sxs-lookup"><span data-stu-id="c2314-125">In this example, hello default domain of **https://contoso5api.onmicrosoft.com** is used with hello suffix of **/api** specified.</span></span>

![新 Azure Active Directory 應用程式屬性][api-management-new-aad-application-2]

<span data-ttu-id="c2314-127">按一下 hello 核取按鈕 toosave 和建立 hello 應用程式，並切換 toohello**設定**tooconfigure hello 新應用程式索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="c2314-127">Click hello check button toosave and create hello application, and switch toohello **Configure** tab tooconfigure hello new application.</span></span>

![新 Azure Active Directory 應用程式已建立][api-management-new-aad-app-created]

<span data-ttu-id="c2314-129">如果多個 Azure Active Directory 將 toobe 此應用程式使用，請按一下**是**如**應用程式是多租用戶**。</span><span class="sxs-lookup"><span data-stu-id="c2314-129">If multiple Azure Active Directories are going toobe used for this application, click **Yes** for **Application is multi-tenant**.</span></span> <span data-ttu-id="c2314-130">hello 預設值是**否**。</span><span class="sxs-lookup"><span data-stu-id="c2314-130">hello default is **No**.</span></span>

![是][api-management-aad-app-multi-tenant]

<span data-ttu-id="c2314-132">複製 hello**重新導向 URL**從 hello **Azure Active Directory**區段 hello**外部識別**hello 發行者入口網站中索引標籤，並將它貼到 hello **回覆 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="c2314-132">Copy hello **Redirect URL** from hello **Azure Active Directory** section of hello **External Identities** tab in hello publisher portal and paste it into hello **Reply URL** text box.</span></span> 

![回覆 URL][api-management-aad-reply-url]

<span data-ttu-id="c2314-134">捲軸 toohello 底部 hello 設定索引標籤上，選取 hello**應用程式權限**下拉式清單中，並檢查**讀取目錄資料**。</span><span class="sxs-lookup"><span data-stu-id="c2314-134">Scroll toohello bottom of hello configure tab, select hello **Application Permissions** drop-down, and check **Read directory data**.</span></span>

![應用程式權限][api-management-aad-app-permissions]

<span data-ttu-id="c2314-136">選取 hello**委派權限**下拉式清單中，並檢查**啟用登入並讀取使用者的設定檔**。</span><span class="sxs-lookup"><span data-stu-id="c2314-136">Select hello **Delegate Permissions** drop-down, and check **Enable sign-on and read users' profiles**.</span></span>

![委派的權限][api-management-aad-delegated-permissions]

> <span data-ttu-id="c2314-138">如需應用程式和委派的權限的詳細資訊，請參閱[存取 hello Graph API][Accessing hello Graph API]。</span><span class="sxs-lookup"><span data-stu-id="c2314-138">For more information about application and delegated permissions, see [Accessing hello Graph API][Accessing hello Graph API].</span></span>
> 
> 

<span data-ttu-id="c2314-139">複製 hello**用戶端識別碼**toohello 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="c2314-139">Copy hello **Client Id** toohello clipboard.</span></span>

![用戶端識別碼][api-management-aad-app-client-id]

<span data-ttu-id="c2314-141">切換後 toohello 發行者入口網站，並貼上在 hello**用戶端識別碼**複製 hello Azure Active Directory 應用程式組態中。</span><span class="sxs-lookup"><span data-stu-id="c2314-141">Switch back toohello publisher portal and paste in hello **Client Id** copied from hello Azure Active Directory application configuration.</span></span>

![用戶端識別碼][api-management-client-id]

<span data-ttu-id="c2314-143">切換後 toohello Azure Active Directory 設定，然後按一下 hello**選取持續時間**下拉式清單中 hello**金鑰**區段，並指定間隔。</span><span class="sxs-lookup"><span data-stu-id="c2314-143">Switch back toohello Azure Active Directory configuration, and click hello **Select duration** drop-down in hello **Keys** section and specify an interval.</span></span> <span data-ttu-id="c2314-144">在此範例中使用 **1 年** 。</span><span class="sxs-lookup"><span data-stu-id="c2314-144">In this example, **1 year** is used.</span></span>

![Key][api-management-aad-key-before-save]

<span data-ttu-id="c2314-146">按一下**儲存**toosave hello 組態和顯示 hello 金鑰。</span><span class="sxs-lookup"><span data-stu-id="c2314-146">Click **Save** toosave hello configuration and display hello key.</span></span> <span data-ttu-id="c2314-147">將複製 hello 金鑰 toohello 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="c2314-147">Copy hello key toohello clipboard.</span></span>

> <span data-ttu-id="c2314-148">記下此金鑰。</span><span class="sxs-lookup"><span data-stu-id="c2314-148">Make a note of this key.</span></span> <span data-ttu-id="c2314-149">一旦您關閉 hello Azure Active Directory 設定 視窗中，無法再次顯示 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="c2314-149">Once you close hello Azure Active Directory configuration window, hello key cannot be displayed again.</span></span>
> 
> 

![Key][api-management-aad-key-after-save]

<span data-ttu-id="c2314-151">交換器後 toohello 發行者入口網站和貼上 hello 金鑰貼入 hello**用戶端密碼**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="c2314-151">Switch back toohello publisher portal and paste hello key into hello **Client Secret** text box.</span></span>

![用戶端密碼][api-management-client-secret]

<span data-ttu-id="c2314-153">**允許租用戶**指定的目錄有存取 toohello hello API 管理服務執行個體的應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="c2314-153">**Allowed Tenants** specifies which directories have access toohello APIs of hello API Management service instance.</span></span> <span data-ttu-id="c2314-154">指定您想要 toogrant 存取 Azure Active Directory 執行個體 toowhich hello 的 hello 網域。</span><span class="sxs-lookup"><span data-stu-id="c2314-154">Specify hello domains of hello Azure Active Directory instances toowhich you want toogrant access.</span></span> <span data-ttu-id="c2314-155">您可以使用換行符號、空格或逗號來分隔多個網域。</span><span class="sxs-lookup"><span data-stu-id="c2314-155">You can separate multiple domains with newlines, spaces, or commas.</span></span>

![允許的租用戶][api-management-client-allowed-tenants]


<span data-ttu-id="c2314-157">一旦 hello 想要指定組態，請按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="c2314-157">Once hello desired configuration is specified, click **Save**.</span></span>

![儲存][api-management-client-allowed-tenants-save]

<span data-ttu-id="c2314-159">一旦儲存 hello 變更了，指定 Azure Active Directory 可以登入 toohello 開發人員入口網站中的 hello 步驟在 hello hello 使用者[登入 toohello 開發人員入口網站使用的 Azure Active Directory 帳戶][Log in toohello Developer portal using an Azure Active Directory account].</span><span class="sxs-lookup"><span data-stu-id="c2314-159">Once hello changes are saved, hello users in hello specified Azure Active Directory can sign in toohello Developer portal by following hello steps in [Log in toohello Developer portal using an Azure Active Directory account][Log in toohello Developer portal using an Azure Active Directory account].</span></span>

<span data-ttu-id="c2314-160">可以指定多個網域在 hello**允許租用戶**> 一節。</span><span class="sxs-lookup"><span data-stu-id="c2314-160">Multiple domains can be specified in hello **Allowed Tenants** section.</span></span> <span data-ttu-id="c2314-161">任何使用者可以從不同 hello hello 應用程式註冊所在的原始網域的網域登入前，hello 不同網域的全域管理員必須授與權限 hello 應用程式 tooaccess 目錄資料。</span><span class="sxs-lookup"><span data-stu-id="c2314-161">Before any user can log in from a different domain than hello original domain where hello application was registered, a global administrator of hello different domain must grant permission for hello application tooaccess directory data.</span></span> <span data-ttu-id="c2314-162">toogrant 權限，hello 全域系統管理員應太`https://<URL of your developer portal>/aadadminconsent`(例如，https://contoso.portal.azure-api.net/aadadminconsent)，按一下 [提交] hello 網域名稱中的 hello 他們想 toogive 存取 tooand 的 Active Directory 租用戶的型別。</span><span class="sxs-lookup"><span data-stu-id="c2314-162">toogrant permission, hello global administrator should go too`https://<URL of your developer portal>/aadadminconsent` (for example, https://contoso.portal.azure-api.net/aadadminconsent), type in hello domain name of hello Active Directory tenant they want toogive access tooand click Submit.</span></span> <span data-ttu-id="c2314-163">在 hello 下列範例中，全域系統管理員身分從`miaoaad.onmicrosoft.com`正嘗試 toogive 權限 toothis 特定開發人員入口網站。</span><span class="sxs-lookup"><span data-stu-id="c2314-163">In hello following example, a global administrator from `miaoaad.onmicrosoft.com` is trying toogive permission toothis particular developer portal.</span></span> 

![權限][api-management-aad-consent]

<span data-ttu-id="c2314-165">Hello 下一個畫面中，在 hello 全域系統管理員可提示的 tooconfirm 賦予 hello 的權限。</span><span class="sxs-lookup"><span data-stu-id="c2314-165">In hello next screen, hello global administrator will be prompted tooconfirm giving hello permission.</span></span> 

![權限][api-management-permissions-form]

> <span data-ttu-id="c2314-167">如果非全域系統管理員嘗試 toolog 中之前的權限會授與全域系統管理員、 hello 登入嘗試失敗和錯誤畫面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="c2314-167">If a non-global administrator tries toolog in before permissions are granted by a global administrator, hello login attempt fails and an error screen is displayed.</span></span>
> 
> 

## <a name="how-tooadd-an-external-azure-active-directory-group"></a><span data-ttu-id="c2314-168">如何 tooadd 外部的 Azure Active Directory 群組</span><span class="sxs-lookup"><span data-stu-id="c2314-168">How tooadd an external Azure Active Directory Group</span></span>
<span data-ttu-id="c2314-169">啟用 Azure Active Directory 中使用者的存取權之後，您可以新增至 API 管理 toomore 的 Azure Active Directory 群組輕鬆地管理 hello 與之間的關聯 hello 群組中的 hello 開發人員想要的 hello 產品。</span><span class="sxs-lookup"><span data-stu-id="c2314-169">After enabling access for users in an Azure Active Directory, you can add Azure Active Directory groups into API Management toomore easily manage hello association of hello developers in hello group with hello desired products.</span></span>

> <span data-ttu-id="c2314-170">tooconfigure 外部的 Azure Active Directory 群組，hello Azure Active Directory 必須先設定 hello 身分識別 索引標籤中遵循 hello hello 前一節中的程序。</span><span class="sxs-lookup"><span data-stu-id="c2314-170">tooconfigure an external Azure Active Directory group, hello Azure Active Directory must first be configured in hello Identities tab by following hello procedure in hello previous section.</span></span> 
> 
> 

<span data-ttu-id="c2314-171">從 hello 加入外部 Azure Active Directory 群組**可視性**hello 產品想 toogrant 存取 toohello 群組 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c2314-171">External Azure Active Directory groups are added from hello **Visibility** tab of hello product for which you wish toogrant access toohello group.</span></span> <span data-ttu-id="c2314-172">按一下**產品**，然後按一下hello hello 所需的產品名稱。</span><span class="sxs-lookup"><span data-stu-id="c2314-172">Click **Products**, and then click hello name of hello desired product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="c2314-174">切換 toohello**可視性**索引標籤，然後按一下**新增的群組，從 Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="c2314-174">Switch toohello **Visibility** tab, and click **Add Groups from Azure Active Directory**.</span></span>

![加入群組][api-management-add-groups]

<span data-ttu-id="c2314-176">選取 hello **Azure Active Directory 租用戶**hello 下拉式清單中，與在 hello hello 所需群組然後類型 hello 名稱**群組**toobe 加入文字方塊。</span><span class="sxs-lookup"><span data-stu-id="c2314-176">Select hello **Azure Active Directory Tenant** from hello drop-down list, and then type hello name of hello desired group in hello **Groups** toobe added text box.</span></span>

![選取群組][api-management-select-group]

<span data-ttu-id="c2314-178">此群組名稱可以在 hello**群組**hello 下列範例所示，您的 Azure Active directory，清單。</span><span class="sxs-lookup"><span data-stu-id="c2314-178">This group name can be found in hello **Groups** list for your Azure Active Directory, as shown in hello following example.</span></span>

![Azure Active Directory 群組清單][api-management-aad-groups-list]

<span data-ttu-id="c2314-180">按一下**新增**toovalidate hello 群組名稱，並加入 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="c2314-180">Click **Add** toovalidate hello group name and add hello group.</span></span> <span data-ttu-id="c2314-181">在此範例中，hello **Contoso 5 開發人員**就會加入外部群組。</span><span class="sxs-lookup"><span data-stu-id="c2314-181">In this example, hello **Contoso 5 Developers** external group is added.</span></span> 

![Group added][api-management-aad-group-added]

<span data-ttu-id="c2314-183">按一下**儲存**toosave hello 新群組選取項目。</span><span class="sxs-lookup"><span data-stu-id="c2314-183">Click **Save** toosave hello new group selection.</span></span>

<span data-ttu-id="c2314-184">一旦已設定 Azure Active Directory 群組從一個產品，就是檢查 hello 可用 toobe**可視性** 索引標籤的 hello hello API 管理服務執行個體中的其他產品。</span><span class="sxs-lookup"><span data-stu-id="c2314-184">Once an Azure Active Directory group has been configured from one product, it is available toobe checked on hello **Visibility** tab for hello other products in hello API Management service instance.</span></span>

<span data-ttu-id="c2314-185">tooreview 並設定 hello 屬性外部一旦已加入的群組按一下 hello hello hello 群組名稱**群組** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c2314-185">tooreview and configure hello properties for external groups once they have been added, click hello name of hello group from hello **Groups** tab.</span></span>

![管理群組][api-management-groups]

<span data-ttu-id="c2314-187">您可以從這裡編輯 hello**名稱**和 hello**描述**的 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="c2314-187">From here you can edit hello **Name** and hello **Description** of hello group.</span></span>

![編輯群組][api-management-edit-group]

<span data-ttu-id="c2314-189">Hello 的使用者設定的 Azure Active Directory 登入 toohello 開發人員入口網站並檢視和訂閱他們擁有之可見性 hello 之後 > 一節中的 hello 指示 tooany 群組。</span><span class="sxs-lookup"><span data-stu-id="c2314-189">Users from hello configured Azure Active Directory can sign in toohello Developer portal and view and subscribe tooany groups for which they have visibility by following hello instructions in hello following section.</span></span>

## <a name="how-toolog-in-toohello-developer-portal-using-an-azure-active-directory-account"></a><span data-ttu-id="c2314-190">如何使用 Azure Active Directory 帳戶 toohello 開發人員入口網站中的 toolog</span><span class="sxs-lookup"><span data-stu-id="c2314-190">How toolog in toohello Developer portal using an Azure Active Directory account</span></span>
<span data-ttu-id="c2314-191">toolog hello 開發人員入口網站，使用 Azure Active Directory 帳戶設定在 hello 先前章節中，開啟新的瀏覽器視窗，使用 hello**登入 URL**從 hello Active Directory 應用程式組態，然後按一下**Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="c2314-191">toolog into hello Developer portal using an Azure Active Directory account configured in hello previous sections, open a new browser window using hello **Sign-on URL** from hello Active Directory application configuration, and click **Azure Active Directory**.</span></span>

![開發人員入口網站][api-management-dev-portal-signin]

<span data-ttu-id="c2314-193">輸入您 Azure Active Directory 中的 hello 的其中一個 hello 使用者的認證，然後按一下**登入**。</span><span class="sxs-lookup"><span data-stu-id="c2314-193">Enter hello credentials of one of hello users in your Azure Active Directory, and click **Sign in**.</span></span>

![Sign in][api-management-aad-signin]

<span data-ttu-id="c2314-195">如果需要其他資訊，可能會出現註冊表單的提示。</span><span class="sxs-lookup"><span data-stu-id="c2314-195">You may be prompted with a registration form if any additional information is required.</span></span> <span data-ttu-id="c2314-196">完成 hello 註冊表單，然後按一下**註冊**。</span><span class="sxs-lookup"><span data-stu-id="c2314-196">Complete hello registration form and click **Sign up**.</span></span>

![註冊][api-management-complete-registration]

<span data-ttu-id="c2314-198">您的使用者現在已登入您 API 管理服務執行個體的 hello 開發人員入口網站中。</span><span class="sxs-lookup"><span data-stu-id="c2314-198">Your user is now logged into hello developer portal for your API Management service instance.</span></span>

![註冊完成][api-management-registration-complete]

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-security-external-identities.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-aad-consent]: ./media/api-management-howto-aad/api-management-aad-consent.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

