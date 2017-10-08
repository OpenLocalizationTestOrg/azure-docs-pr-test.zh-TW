---
title: "Azure 入口網站中的應用程式的 aaaCreate 識別 |Microsoft 文件"
description: "描述如何 toocreate 新的 Azure Active Directory 應用程式和服務主體可以使用 Azure Resource Manager toomanage hello 角色型存取控制存取 tooresources。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 9624715ac612f42df6f9e9e67b8233bd4b914174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-portal-toocreate-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a><span data-ttu-id="5458a-103">使用入口網站 toocreate Azure Active Directory 應用程式和服務主體可存取資源</span><span class="sxs-lookup"><span data-stu-id="5458a-103">Use portal toocreate an Azure Active Directory application and service principal that can access resources</span></span>

<span data-ttu-id="5458a-104">當您需要 tooaccess 或修改資源的應用程式時，您必須在設定 Azure Active Directory (AD) 應用程式，並指派 hello 所需的權限 tooit。</span><span class="sxs-lookup"><span data-stu-id="5458a-104">When you have an application that needs tooaccess or modify resources, you must set up an Azure Active Directory (AD) application and assign hello required permissions tooit.</span></span> <span data-ttu-id="5458a-105">這個方法很理想 toorunning hello 應用程式，以您自己的認證，因為：</span><span class="sxs-lookup"><span data-stu-id="5458a-105">This approach is preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="5458a-106">您可以指派權限 toohello 不同於您自己的權限的應用程式識別。</span><span class="sxs-lookup"><span data-stu-id="5458a-106">You can assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="5458a-107">一般而言，這些權限會限制的 tooexactly 哪些 hello 應用程式需要 toodo。</span><span class="sxs-lookup"><span data-stu-id="5458a-107">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="5458a-108">如果您的責任的變更，您並沒有 toochange hello 應用程式的認證。</span><span class="sxs-lookup"><span data-stu-id="5458a-108">You do not have toochange hello app's credentials if your responsibilities change.</span></span> 
* <span data-ttu-id="5458a-109">執行無人看管的指令碼時，您可以使用憑證 tooautomate 驗證。</span><span class="sxs-lookup"><span data-stu-id="5458a-109">You can use a certificate tooautomate authentication when executing an unattended script.</span></span>

<span data-ttu-id="5458a-110">本主題說明您如何 tooperform 那些逐步 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="5458a-110">This topic shows you how tooperform those steps through hello portal.</span></span> <span data-ttu-id="5458a-111">它著重在 hello 應用程式所在預定的 toorun 只能有一個組織內的單一租用戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="5458a-111">It focuses on a single-tenant application where hello application is intended toorun within only one organization.</span></span> <span data-ttu-id="5458a-112">您通常會將單一租用戶應用程式用在組織內執行的企業營運系統應用程式。</span><span class="sxs-lookup"><span data-stu-id="5458a-112">You typically use single-tenant applications for line-of-business applications that run within your organization.</span></span>
 
## <a name="required-permissions"></a><span data-ttu-id="5458a-113">所需的權限</span><span class="sxs-lookup"><span data-stu-id="5458a-113">Required permissions</span></span>
<span data-ttu-id="5458a-114">toocomplete 本主題中，您必須有足夠的權限 tooregister 的應用程式與 Azure AD 租用戶，並在您 Azure 訂用帳戶中指派 hello 應用程式 tooa 角色。</span><span class="sxs-lookup"><span data-stu-id="5458a-114">toocomplete this topic, you must have sufficient permissions tooregister an application with your Azure AD tenant, and assign hello application tooa role in your Azure subscription.</span></span> <span data-ttu-id="5458a-115">讓我們確定您擁有 hello 正確的權限 tooperform 那些步驟。</span><span class="sxs-lookup"><span data-stu-id="5458a-115">Let's make sure you have hello right permissions tooperform those steps.</span></span>

### <a name="check-azure-active-directory-permissions"></a><span data-ttu-id="5458a-116">檢查 Azure Active Directory 權限</span><span class="sxs-lookup"><span data-stu-id="5458a-116">Check Azure Active Directory permissions</span></span>
1. <span data-ttu-id="5458a-117">登入 tooyour Azure 帳戶透過 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="5458a-117">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5458a-118">選取 **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="5458a-118">Select **Azure Active Directory**.</span></span>

     ![選取 Azure Active Directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. <span data-ttu-id="5458a-120">在 Azure Active Directory 中，選取 [使用者設定]。</span><span class="sxs-lookup"><span data-stu-id="5458a-120">In Azure Active Directory, select **User settings**.</span></span>

     ![選取使用者設定](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. <span data-ttu-id="5458a-122">檢查 hello**應用程式註冊**設定。</span><span class="sxs-lookup"><span data-stu-id="5458a-122">Check hello **App registrations** setting.</span></span> <span data-ttu-id="5458a-123">如果設定太**是**，非系統管理使用者可以註冊 AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5458a-123">If set too**Yes**, non-admin users can register AD apps.</span></span> <span data-ttu-id="5458a-124">這個設定表示 hello Azure AD 租用戶中的任何使用者可以註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="5458a-124">This setting means any user in hello Azure AD tenant can register an app.</span></span> <span data-ttu-id="5458a-125">您可以繼續在太[檢查 Azure 訂用帳戶的權限](#check-azure-subscription-permissions)。</span><span class="sxs-lookup"><span data-stu-id="5458a-125">You can proceed too[Check Azure subscription permissions](#check-azure-subscription-permissions).</span></span>

     ![檢視應用程式註冊](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. <span data-ttu-id="5458a-127">如果設定太 hello 應用程式登錄設定**否**，只有系統管理員使用者可以註冊的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5458a-127">If hello app registrations setting is set too**No**, only admin users can register apps.</span></span> <span data-ttu-id="5458a-128">您的帳戶是否 hello Azure AD 租用戶系統管理員，您會需要 toocheck。</span><span class="sxs-lookup"><span data-stu-id="5458a-128">You need toocheck whether your account is an admin for hello Azure AD tenant.</span></span> <span data-ttu-id="5458a-129">從 [快速工作] 中，選取 [概觀] 和 [尋找使用者]。</span><span class="sxs-lookup"><span data-stu-id="5458a-129">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![尋找使用者](./media/resource-group-create-service-principal-portal/find-user.png)
6. <span data-ttu-id="5458a-131">搜尋您的帳戶，找到時選取它。</span><span class="sxs-lookup"><span data-stu-id="5458a-131">Search for your account, and select it when you find it.</span></span>

     ![搜尋使用者](./media/resource-group-create-service-principal-portal/show-user.png)
7. <span data-ttu-id="5458a-133">對於您的帳戶，選取 [目錄角色]。</span><span class="sxs-lookup"><span data-stu-id="5458a-133">For your account, select **Directory role**.</span></span> 

     ![目錄角色](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. <span data-ttu-id="5458a-135">在 Azure AD 中檢視您指派的目錄角色。</span><span class="sxs-lookup"><span data-stu-id="5458a-135">View your assigned directory role in Azure AD.</span></span> <span data-ttu-id="5458a-136">如果您的帳戶指派 toohello 使用者角色，但 hello 應用程式登錄設定 （從先前步驟的 hello) 有限的 tooadmin 使用者，請要求系統管理員 tooeither 指派您 tooan 系統管理員角色或 tooenable 使用者 tooregister 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5458a-136">If your account is assigned toohello User role, but hello app registration setting (from hello preceding steps) is limited tooadmin users, ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

     ![檢視角色](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a><span data-ttu-id="5458a-138">檢查 Azure 訂用帳戶權限</span><span class="sxs-lookup"><span data-stu-id="5458a-138">Check Azure subscription permissions</span></span>
<span data-ttu-id="5458a-139">您 Azure 訂用帳戶，您的帳戶必須具有`Microsoft.Authorization/*/Write`存取 tooassign AD 應用程式 tooa 角色。</span><span class="sxs-lookup"><span data-stu-id="5458a-139">In your Azure subscription, your account must have `Microsoft.Authorization/*/Write` access tooassign an AD app tooa role.</span></span> <span data-ttu-id="5458a-140">這個動作透過 hello 授與[擁有者](../active-directory/role-based-access-built-in-roles.md#owner)角色或[使用者存取系統管理員](../active-directory/role-based-access-built-in-roles.md#user-access-administrator)角色。</span><span class="sxs-lookup"><span data-stu-id="5458a-140">This action is granted through hello [Owner](../active-directory/role-based-access-built-in-roles.md#owner) role or [User Access Administrator](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) role.</span></span> <span data-ttu-id="5458a-141">如果您的帳戶指派 toohello**參與者**角色，您沒有足夠的權限。</span><span class="sxs-lookup"><span data-stu-id="5458a-141">If your account is assigned toohello **Contributor** role, you do not have adequate permission.</span></span> <span data-ttu-id="5458a-142">嘗試 tooassign hello 服務主體 tooa 角色時，您會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="5458a-142">You will receive an error when attempting tooassign hello service principal tooa role.</span></span> 

<span data-ttu-id="5458a-143">toocheck 您訂用帳戶的權限：</span><span class="sxs-lookup"><span data-stu-id="5458a-143">toocheck your subscription permissions:</span></span>

1. <span data-ttu-id="5458a-144">如果您不已查看您的 Azure AD 帳戶 hello 先前步驟中，選取**Azure Active Directory** hello 左窗格中。</span><span class="sxs-lookup"><span data-stu-id="5458a-144">If you are not already looking at your Azure AD account from hello preceding steps, select **Azure Active Directory** from hello left pane.</span></span>

2. <span data-ttu-id="5458a-145">找到您的 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5458a-145">Find your Azure AD account.</span></span> <span data-ttu-id="5458a-146">從 [快速工作] 中，選取 [概觀] 和 [尋找使用者]。</span><span class="sxs-lookup"><span data-stu-id="5458a-146">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![尋找使用者](./media/resource-group-create-service-principal-portal/find-user.png)
2. <span data-ttu-id="5458a-148">搜尋您的帳戶，找到時選取它。</span><span class="sxs-lookup"><span data-stu-id="5458a-148">Search for your account, and select it when you find it.</span></span>

     ![搜尋使用者](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. <span data-ttu-id="5458a-150">選取 [Azure 資源]。</span><span class="sxs-lookup"><span data-stu-id="5458a-150">Select **Azure resources**.</span></span>

     ![選取資源](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. <span data-ttu-id="5458a-152">檢視指派的角色，並判斷是否有足夠的權限 tooassign AD 應用程式 tooa 角色。</span><span class="sxs-lookup"><span data-stu-id="5458a-152">View your assigned roles, and determine if you have adequate permissions tooassign an AD app tooa role.</span></span> <span data-ttu-id="5458a-153">如果沒有，請詢問您的訂用帳戶管理員 tooadd 您 tooUser 存取 」 系統管理員角色。</span><span class="sxs-lookup"><span data-stu-id="5458a-153">If not, ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span> <span data-ttu-id="5458a-154">在下列映像的 hello，hello 使用者是指派的 toohello 擁有者角色的兩個訂閱，這表示該使用者具有足夠的權限。</span><span class="sxs-lookup"><span data-stu-id="5458a-154">In hello following image, hello user is assigned toohello Owner role for two subscriptions, which means that user has adequate permissions.</span></span> 

     ![顯示權限](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a><span data-ttu-id="5458a-156">建立 Azure Active Directory 應用程式</span><span class="sxs-lookup"><span data-stu-id="5458a-156">Create an Azure Active Directory application</span></span>
1. <span data-ttu-id="5458a-157">登入 tooyour Azure 帳戶透過 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="5458a-157">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5458a-158">選取 **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="5458a-158">Select **Azure Active Directory**.</span></span>

     ![選取 Azure Active Directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. <span data-ttu-id="5458a-160">選取 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="5458a-160">Select **App registrations**.</span></span>   

     ![select app registrations](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. <span data-ttu-id="5458a-162">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="5458a-162">Select **Add**.</span></span>

     ![新增應用程式](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. <span data-ttu-id="5458a-164">Hello 應用程式提供名稱和 URL。</span><span class="sxs-lookup"><span data-stu-id="5458a-164">Provide a name and URL for hello application.</span></span> <span data-ttu-id="5458a-165">選取  **Web 應用程式 / 應用程式開發介面**或**原生**想 toocreate hello 種應用程式。</span><span class="sxs-lookup"><span data-stu-id="5458a-165">Select either **Web app / API** or **Native** for hello type of application you want toocreate.</span></span> <span data-ttu-id="5458a-166">設定後 hello 值，請選取**建立**。</span><span class="sxs-lookup"><span data-stu-id="5458a-166">After setting hello values, select **Create**.</span></span>

     ![名稱應用程式](./media/resource-group-create-service-principal-portal/create-app.png)

<span data-ttu-id="5458a-168">您已建立好應用程式。</span><span class="sxs-lookup"><span data-stu-id="5458a-168">You have created your application.</span></span>

## <a name="get-application-id-and-authentication-key"></a><span data-ttu-id="5458a-169">取得應用程式識別碼和驗證金鑰</span><span class="sxs-lookup"><span data-stu-id="5458a-169">Get application ID and authentication key</span></span>
<span data-ttu-id="5458a-170">以程式設計方式登入時，您會需要您的應用程式和驗證金鑰的 hello 識別碼。</span><span class="sxs-lookup"><span data-stu-id="5458a-170">When programmatically logging in, you need hello ID for your application and an authentication key.</span></span> <span data-ttu-id="5458a-171">tooget 那些值，使用 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5458a-171">tooget those values, use hello following steps:</span></span>

1. <span data-ttu-id="5458a-172">在 Azure Active Directory 中，從 [應用程式註冊]選取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5458a-172">From **App registrations** in Azure Active Directory, select your application.</span></span>

     ![選取應用程式](./media/resource-group-create-service-principal-portal/select-app.png)
2. <span data-ttu-id="5458a-174">複製 hello**應用程式識別碼**並將它儲存在應用程式程式碼中。</span><span class="sxs-lookup"><span data-stu-id="5458a-174">Copy hello **Application ID** and store it in your application code.</span></span> <span data-ttu-id="5458a-175">hello hello 中的應用程式[範例應用程式](#sample-applications)區段，請參閱 toothis hello 用戶端識別碼值。</span><span class="sxs-lookup"><span data-stu-id="5458a-175">hello applications in hello [sample applications](#sample-applications) section refer toothis value as hello client id.</span></span>

     ![用戶端識別碼](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. <span data-ttu-id="5458a-177">toogenerate 需有驗證金鑰，選取**金鑰**。</span><span class="sxs-lookup"><span data-stu-id="5458a-177">toogenerate an authentication key, select **Keys**.</span></span>

     ![選取金鑰](./media/resource-group-create-service-principal-portal/select-keys.png)
4. <span data-ttu-id="5458a-179">提供 hello 金鑰和 hello 金鑰的持續時間的描述。</span><span class="sxs-lookup"><span data-stu-id="5458a-179">Provide a description of hello key, and a duration for hello key.</span></span> <span data-ttu-id="5458a-180">完成時，選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="5458a-180">When done, select **Save**.</span></span>

     ![儲存金鑰](./media/resource-group-create-service-principal-portal/save-key.png)

     <span data-ttu-id="5458a-182">在儲存之後 hello 索引鍵，會顯示 hello hello 機碼值。</span><span class="sxs-lookup"><span data-stu-id="5458a-182">After saving hello key, hello value of hello key is displayed.</span></span> <span data-ttu-id="5458a-183">因為您不能 tooretrieve hello 金鑰之後，請複製此值。</span><span class="sxs-lookup"><span data-stu-id="5458a-183">Copy this value because you are not able tooretrieve hello key later.</span></span> <span data-ttu-id="5458a-184">您提供 hello 機碼值中的 hello 應用程式識別碼 toolog hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5458a-184">You provide hello key value with hello application ID toolog in as hello application.</span></span> <span data-ttu-id="5458a-185">儲存您的應用程式可以擷取 hello 機碼值。</span><span class="sxs-lookup"><span data-stu-id="5458a-185">Store hello key value where your application can retrieve it.</span></span>

     ![儲存的金鑰](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a><span data-ttu-id="5458a-187">取得租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="5458a-187">Get tenant ID</span></span>
<span data-ttu-id="5458a-188">以程式設計方式登入時，您需要 toopass hello 租用戶識別碼與驗證要求。</span><span class="sxs-lookup"><span data-stu-id="5458a-188">When programmatically logging in, you need toopass hello tenant ID with your authentication request.</span></span> 

1. <span data-ttu-id="5458a-189">tooget hello 租用戶識別碼，選取**屬性**Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="5458a-189">tooget hello tenant ID, select **Properties** for your Azure AD tenant.</span></span> 

     ![選取 Azure AD 屬性](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. <span data-ttu-id="5458a-191">複製 hello**目錄識別碼**。</span><span class="sxs-lookup"><span data-stu-id="5458a-191">Copy hello **Directory ID**.</span></span> <span data-ttu-id="5458a-192">這個值是您的租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="5458a-192">This value is your tenant ID.</span></span>

     ![租用戶識別碼](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-toorole"></a><span data-ttu-id="5458a-194">指派應用程式 toorole</span><span class="sxs-lookup"><span data-stu-id="5458a-194">Assign application toorole</span></span>
<span data-ttu-id="5458a-195">您的訂用帳戶中的 tooaccess 資源，您必須指派 hello 應用程式 tooa 角色。</span><span class="sxs-lookup"><span data-stu-id="5458a-195">tooaccess resources in your subscription, you must assign hello application tooa role.</span></span> <span data-ttu-id="5458a-196">決定哪些角色代表 hello hello 應用程式的正確權限。</span><span class="sxs-lookup"><span data-stu-id="5458a-196">Decide which role represents hello right permissions for hello application.</span></span> <span data-ttu-id="5458a-197">toolearn 有關 hello 可用的角色，請參閱[RBAC： 內建的角色](../active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="5458a-197">toolearn about hello available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="5458a-198">您可以設定 hello 範圍層級 hello hello 訂用帳戶、 資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="5458a-198">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="5458a-199">權限是繼承的 toolower 範圍層級。</span><span class="sxs-lookup"><span data-stu-id="5458a-199">Permissions are inherited toolower levels of scope.</span></span> <span data-ttu-id="5458a-200">例如，新增資源群組的應用程式 toohello 讀取器角色表示它可以讀取 hello 資源群組和它所包含的任何資源。</span><span class="sxs-lookup"><span data-stu-id="5458a-200">For example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains.</span></span>

1. <span data-ttu-id="5458a-201">瀏覽 toohello 想 tooassign hello 應用程式的範圍層級。</span><span class="sxs-lookup"><span data-stu-id="5458a-201">Navigate toohello level of scope you wish tooassign hello application to.</span></span> <span data-ttu-id="5458a-202">例如，tooassign hello 訂用帳戶範圍，角色選取**訂閱**。</span><span class="sxs-lookup"><span data-stu-id="5458a-202">For example, tooassign a role at hello subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="5458a-203">您可以改為選取資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="5458a-203">You could instead select a resource group or resource.</span></span>

     ![select subscription](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. <span data-ttu-id="5458a-205">選取 hello 特定訂用帳戶 （資源群組或資源） tooassign hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5458a-205">Select hello particular subscription (resource group or resource) tooassign hello application to.</span></span>

     ![選取要指派的訂用帳戶](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. <span data-ttu-id="5458a-207">選取 [存取控制 (IAM)]。</span><span class="sxs-lookup"><span data-stu-id="5458a-207">Select **Access Control (IAM)**.</span></span>

     ![選取存取](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. <span data-ttu-id="5458a-209">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="5458a-209">Select **Add**.</span></span>

     ![選取 [新增]](./media/resource-group-create-service-principal-portal/select-add.png)
6. <span data-ttu-id="5458a-211">選取您想 tooassign toohello 應用程式的 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="5458a-211">Select hello role you wish tooassign toohello application.</span></span> <span data-ttu-id="5458a-212">hello 下列影像顯示 hello**讀取器**角色。</span><span class="sxs-lookup"><span data-stu-id="5458a-212">hello following image shows hello **Reader** role.</span></span>

     ![選取角色](./media/resource-group-create-service-principal-portal/select-role.png)

8. <span data-ttu-id="5458a-214">搜尋並選取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5458a-214">Search for your application, and select it.</span></span>

     ![搜尋應用程式](./media/resource-group-create-service-principal-portal/search-app.png)
9. <span data-ttu-id="5458a-216">選取**確定**toofinish 指派 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="5458a-216">Select **OK** toofinish assigning hello role.</span></span> <span data-ttu-id="5458a-217">您會看到您 hello 清單中指派該範圍的 tooa 角色之使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5458a-217">You see your application in hello list of users assigned tooa role for that scope.</span></span>

## <a name="log-in-as-hello-application"></a><span data-ttu-id="5458a-218">Hello 應用程式身分登入</span><span class="sxs-lookup"><span data-stu-id="5458a-218">Log in as hello application</span></span>

<span data-ttu-id="5458a-219">您的應用程式現在已設定在 Azure Active Directory 中。</span><span class="sxs-lookup"><span data-stu-id="5458a-219">Your application is now set up in Azure Active Directory.</span></span> <span data-ttu-id="5458a-220">您必須有識別碼和金鑰 toouse hello 應用程式以登入。</span><span class="sxs-lookup"><span data-stu-id="5458a-220">You have an ID and key toouse for signing in as hello application.</span></span> <span data-ttu-id="5458a-221">hello 應用程式會指派 tooa 角色，讓它可以執行特定動作。</span><span class="sxs-lookup"><span data-stu-id="5458a-221">hello application is assigned tooa role that gives it certain actions it can perform.</span></span> <span data-ttu-id="5458a-222">如需透過不同平台的 hello 應用程式以登入資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="5458a-222">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="5458a-223">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5458a-223">PowerShell</span></span>](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [<span data-ttu-id="5458a-224">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5458a-224">Azure CLI</span></span>](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [<span data-ttu-id="5458a-225">REST</span><span class="sxs-lookup"><span data-stu-id="5458a-225">REST</span></span>](/rest/api/#create-the-request)
* [<span data-ttu-id="5458a-226">.NET</span><span class="sxs-lookup"><span data-stu-id="5458a-226">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="5458a-227">Java</span><span class="sxs-lookup"><span data-stu-id="5458a-227">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="5458a-228">Node.js</span><span class="sxs-lookup"><span data-stu-id="5458a-228">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="5458a-229">Python</span><span class="sxs-lookup"><span data-stu-id="5458a-229">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="5458a-230">Ruby</span><span class="sxs-lookup"><span data-stu-id="5458a-230">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a><span data-ttu-id="5458a-231">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5458a-231">Next steps</span></span>
* <span data-ttu-id="5458a-232">tooset 多租用戶應用程式，請參閱[以 hello Azure 資源管理員 API 的開發人員指南 tooauthorization](resource-manager-api-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="5458a-232">tooset up a multi-tenant application, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="5458a-233">toolearn 有關指定安全性原則，請參閱[Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="5458a-233">toolearn about specifying security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>  
* <span data-ttu-id="5458a-234">如需可授與或拒絕 toousers 可用動作的清單，請參閱[Azure 資源管理員資源提供者作業](../active-directory/role-based-access-control-resource-provider-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="5458a-234">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
