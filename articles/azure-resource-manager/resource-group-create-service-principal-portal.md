---
title: "在入口網站中建立 Azure App 的身分識別 | Microsoft Docs"
description: "描述如何建立可以與 Azure 資源管理員中的角色型存取控制搭配使用來管理資源存取權的新 Active Directory 應用程式和服務主體。描述如何建立可以與 Azure 資源管理員中的角色型存取控制搭配使用來管理資源存取權的新 Active Directory 應用程式和服務主體。"
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
ms.openlocfilehash: 5d24fb99e1095d53e5ea547e53b80178d9cb77c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-portal-to-create-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a><span data-ttu-id="72751-103">使用入口網站來建立可存取資源的 Active Directory 應用程式和服務主體</span><span class="sxs-lookup"><span data-stu-id="72751-103">Use portal to create an Azure Active Directory application and service principal that can access resources</span></span>

<span data-ttu-id="72751-104">如果您擁有需要存取或修改資源的應用程式，您就必須設定一個 Active Directory (AD) 應用程式並為其指派必要的權限。</span><span class="sxs-lookup"><span data-stu-id="72751-104">When you have an application that needs to access or modify resources, you must set up an Azure Active Directory (AD) application and assign the required permissions to it.</span></span> <span data-ttu-id="72751-105">以您自己的認證執行 App 是比較好的作法，因為︰</span><span class="sxs-lookup"><span data-stu-id="72751-105">This approach is preferable to running the app under your own credentials because:</span></span>

* <span data-ttu-id="72751-106">您可以對 App 身分識別指派不同於您自己權限的權限。</span><span class="sxs-lookup"><span data-stu-id="72751-106">You can assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="72751-107">一般而言，這些權限只會限制為 App 必須執行的確切權限。</span><span class="sxs-lookup"><span data-stu-id="72751-107">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="72751-108">如果您的職責變更，就不需要變更 App 的認證。</span><span class="sxs-lookup"><span data-stu-id="72751-108">You do not have to change the app's credentials if your responsibilities change.</span></span> 
* <span data-ttu-id="72751-109">您可以使用憑證在執行自動指令碼時自動進行驗證。</span><span class="sxs-lookup"><span data-stu-id="72751-109">You can use a certificate to automate authentication when executing an unattended script.</span></span>

<span data-ttu-id="72751-110">本主題說明如何透過入口網站執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="72751-110">This topic shows you how to perform those steps through the portal.</span></span> <span data-ttu-id="72751-111">其中著重在說明單一租用戶應用程式，此應用程式的目的是只在一個組織內執行。</span><span class="sxs-lookup"><span data-stu-id="72751-111">It focuses on a single-tenant application where the application is intended to run within only one organization.</span></span> <span data-ttu-id="72751-112">您通常會將單一租用戶應用程式用在組織內執行的企業營運系統應用程式。</span><span class="sxs-lookup"><span data-stu-id="72751-112">You typically use single-tenant applications for line-of-business applications that run within your organization.</span></span>
 
## <a name="required-permissions"></a><span data-ttu-id="72751-113">所需的權限</span><span class="sxs-lookup"><span data-stu-id="72751-113">Required permissions</span></span>
<span data-ttu-id="72751-114">若要完成本主題，您必須有足夠權限向 Azure AD 租用戶註冊應用程式，並將應用程式指派給 Azure 訂用帳戶中的角色。</span><span class="sxs-lookup"><span data-stu-id="72751-114">To complete this topic, you must have sufficient permissions to register an application with your Azure AD tenant, and assign the application to a role in your Azure subscription.</span></span> <span data-ttu-id="72751-115">讓我們來確定您具有適當的權限可執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="72751-115">Let's make sure you have the right permissions to perform those steps.</span></span>

### <a name="check-azure-active-directory-permissions"></a><span data-ttu-id="72751-116">檢查 Azure Active Directory 權限</span><span class="sxs-lookup"><span data-stu-id="72751-116">Check Azure Active Directory permissions</span></span>
1. <span data-ttu-id="72751-117">透過 [Azure 入口網站](https://portal.azure.com)登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="72751-117">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="72751-118">選取 **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="72751-118">Select **Azure Active Directory**.</span></span>

     ![選取 Azure Active Directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. <span data-ttu-id="72751-120">在 Azure Active Directory 中，選取 [使用者設定]。</span><span class="sxs-lookup"><span data-stu-id="72751-120">In Azure Active Directory, select **User settings**.</span></span>

     ![選取使用者設定](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. <span data-ttu-id="72751-122">檢查 [應用程式註冊] 設定。</span><span class="sxs-lookup"><span data-stu-id="72751-122">Check the **App registrations** setting.</span></span> <span data-ttu-id="72751-123">如果設定為 [是]，非系統管理使用者可以註冊 AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="72751-123">If set to **Yes**, non-admin users can register AD apps.</span></span> <span data-ttu-id="72751-124">這個設定表示 Azure AD 租用戶中的任何使用者都可以註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="72751-124">This setting means any user in the Azure AD tenant can register an app.</span></span> <span data-ttu-id="72751-125">您可以繼續到[檢查 Azure 訂用帳戶權限](#check-azure-subscription-permissions)。</span><span class="sxs-lookup"><span data-stu-id="72751-125">You can proceed to [Check Azure subscription permissions](#check-azure-subscription-permissions).</span></span>

     ![檢視應用程式註冊](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. <span data-ttu-id="72751-127">如果應用程式註冊設定為 [否]，則只有系統管理員使用者才能註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="72751-127">If the app registrations setting is set to **No**, only admin users can register apps.</span></span> <span data-ttu-id="72751-128">您需要檢查帳戶是否為 Azure AD 租用戶的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="72751-128">You need to check whether your account is an admin for the Azure AD tenant.</span></span> <span data-ttu-id="72751-129">從 [快速工作] 中，選取 [概觀] 和 [尋找使用者]。</span><span class="sxs-lookup"><span data-stu-id="72751-129">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![尋找使用者](./media/resource-group-create-service-principal-portal/find-user.png)
6. <span data-ttu-id="72751-131">搜尋您的帳戶，找到時選取它。</span><span class="sxs-lookup"><span data-stu-id="72751-131">Search for your account, and select it when you find it.</span></span>

     ![搜尋使用者](./media/resource-group-create-service-principal-portal/show-user.png)
7. <span data-ttu-id="72751-133">對於您的帳戶，選取 [目錄角色]。</span><span class="sxs-lookup"><span data-stu-id="72751-133">For your account, select **Directory role**.</span></span> 

     ![目錄角色](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. <span data-ttu-id="72751-135">在 Azure AD 中檢視您指派的目錄角色。</span><span class="sxs-lookup"><span data-stu-id="72751-135">View your assigned directory role in Azure AD.</span></span> <span data-ttu-id="72751-136">如果您的帳戶指派給「使用者」角色，但應用程式註冊設定 (從先前步驟中)僅限於系統管理員使用者，請洽詢系統管理員將您指派至系統管理員角色，或讓使用者可以註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="72751-136">If your account is assigned to the User role, but the app registration setting (from the preceding steps) is limited to admin users, ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

     ![檢視角色](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a><span data-ttu-id="72751-138">檢查 Azure 訂用帳戶權限</span><span class="sxs-lookup"><span data-stu-id="72751-138">Check Azure subscription permissions</span></span>
<span data-ttu-id="72751-139">在您的 Azure 訂用帳戶中，您的帳戶必須具有 `Microsoft.Authorization/*/Write` 存取權，才能將 AD 應用程式指派給角色。</span><span class="sxs-lookup"><span data-stu-id="72751-139">In your Azure subscription, your account must have `Microsoft.Authorization/*/Write` access to assign an AD app to a role.</span></span> <span data-ttu-id="72751-140">此動作是[擁有者](../active-directory/role-based-access-built-in-roles.md#owner)角色或[使用者存取系統管理員](../active-directory/role-based-access-built-in-roles.md#user-access-administrator)角色來授與。</span><span class="sxs-lookup"><span data-stu-id="72751-140">This action is granted through the [Owner](../active-directory/role-based-access-built-in-roles.md#owner) role or [User Access Administrator](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) role.</span></span> <span data-ttu-id="72751-141">如果您的帳戶已指派給**參與者**角色，則您沒有足夠的權限。</span><span class="sxs-lookup"><span data-stu-id="72751-141">If your account is assigned to the **Contributor** role, you do not have adequate permission.</span></span> <span data-ttu-id="72751-142">當您嘗試將服務主體指派給角色時，您會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="72751-142">You will receive an error when attempting to assign the service principal to a role.</span></span> 

<span data-ttu-id="72751-143">若要檢查訂用帳戶權限：</span><span class="sxs-lookup"><span data-stu-id="72751-143">To check your subscription permissions:</span></span>

1. <span data-ttu-id="72751-144">如果您在先前的步驟中還沒有查看您的 Azure AD 帳戶，請從左窗格選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="72751-144">If you are not already looking at your Azure AD account from the preceding steps, select **Azure Active Directory** from the left pane.</span></span>

2. <span data-ttu-id="72751-145">找到您的 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="72751-145">Find your Azure AD account.</span></span> <span data-ttu-id="72751-146">從 [快速工作] 中，選取 [概觀] 和 [尋找使用者]。</span><span class="sxs-lookup"><span data-stu-id="72751-146">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![尋找使用者](./media/resource-group-create-service-principal-portal/find-user.png)
2. <span data-ttu-id="72751-148">搜尋您的帳戶，找到時選取它。</span><span class="sxs-lookup"><span data-stu-id="72751-148">Search for your account, and select it when you find it.</span></span>

     ![搜尋使用者](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. <span data-ttu-id="72751-150">選取 [Azure 資源]。</span><span class="sxs-lookup"><span data-stu-id="72751-150">Select **Azure resources**.</span></span>

     ![選取資源](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. <span data-ttu-id="72751-152">檢視指派的角色，並判斷是否有足夠的權限可將 AD 應用程式指派給角色。</span><span class="sxs-lookup"><span data-stu-id="72751-152">View your assigned roles, and determine if you have adequate permissions to assign an AD app to a role.</span></span> <span data-ttu-id="72751-153">如果沒有，請洽詢訂用帳戶管理員，將您新增至「使用者存取系統管理員」角色。</span><span class="sxs-lookup"><span data-stu-id="72751-153">If not, ask your subscription administrator to add you to User Access Administrator role.</span></span> <span data-ttu-id="72751-154">在下圖中，使用者已指派給兩個訂用帳戶的「擁有者」角色，這表示該使用者具有足夠的權限。</span><span class="sxs-lookup"><span data-stu-id="72751-154">In the following image, the user is assigned to the Owner role for two subscriptions, which means that user has adequate permissions.</span></span> 

     ![顯示權限](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a><span data-ttu-id="72751-156">建立 Azure Active Directory 應用程式</span><span class="sxs-lookup"><span data-stu-id="72751-156">Create an Azure Active Directory application</span></span>
1. <span data-ttu-id="72751-157">透過 [Azure 入口網站](https://portal.azure.com)登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="72751-157">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="72751-158">選取 **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="72751-158">Select **Azure Active Directory**.</span></span>

     ![選取 Azure Active Directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. <span data-ttu-id="72751-160">選取 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="72751-160">Select **App registrations**.</span></span>   

     ![select app registrations](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. <span data-ttu-id="72751-162">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="72751-162">Select **Add**.</span></span>

     ![新增應用程式](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. <span data-ttu-id="72751-164">提供應用程式的名稱和 URL。</span><span class="sxs-lookup"><span data-stu-id="72751-164">Provide a name and URL for the application.</span></span> <span data-ttu-id="72751-165">針對您想要建立的應用程式類型，選取 [Web 應用程式/API] 或 [原生]。</span><span class="sxs-lookup"><span data-stu-id="72751-165">Select either **Web app / API** or **Native** for the type of application you want to create.</span></span> <span data-ttu-id="72751-166">設定值之後，選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="72751-166">After setting the values, select **Create**.</span></span>

     ![名稱應用程式](./media/resource-group-create-service-principal-portal/create-app.png)

<span data-ttu-id="72751-168">您已建立好應用程式。</span><span class="sxs-lookup"><span data-stu-id="72751-168">You have created your application.</span></span>

## <a name="get-application-id-and-authentication-key"></a><span data-ttu-id="72751-169">取得應用程式識別碼和驗證金鑰</span><span class="sxs-lookup"><span data-stu-id="72751-169">Get application ID and authentication key</span></span>
<span data-ttu-id="72751-170">以程式設計方式登入時，您需要應用程式識別碼和驗證金鑰。</span><span class="sxs-lookup"><span data-stu-id="72751-170">When programmatically logging in, you need the ID for your application and an authentication key.</span></span> <span data-ttu-id="72751-171">若要取得這些值，請使用下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="72751-171">To get those values, use the following steps:</span></span>

1. <span data-ttu-id="72751-172">在 Azure Active Directory 中，從 [應用程式註冊]選取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="72751-172">From **App registrations** in Azure Active Directory, select your application.</span></span>

     ![選取應用程式](./media/resource-group-create-service-principal-portal/select-app.png)
2. <span data-ttu-id="72751-174">複製 [應用程式識別碼] 並儲存在您的應用程式碼中。</span><span class="sxs-lookup"><span data-stu-id="72751-174">Copy the **Application ID** and store it in your application code.</span></span> <span data-ttu-id="72751-175">[範例應用程式](#sample-applications) 區段中的應用程式會參考此值作為用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="72751-175">The applications in the [sample applications](#sample-applications) section refer to this value as the client id.</span></span>

     ![用戶端識別碼](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. <span data-ttu-id="72751-177">若要產生驗證金鑰，請選取 [金鑰]。</span><span class="sxs-lookup"><span data-stu-id="72751-177">To generate an authentication key, select **Keys**.</span></span>

     ![選取金鑰](./media/resource-group-create-service-principal-portal/select-keys.png)
4. <span data-ttu-id="72751-179">提供金鑰的描述和金鑰的持續時間。</span><span class="sxs-lookup"><span data-stu-id="72751-179">Provide a description of the key, and a duration for the key.</span></span> <span data-ttu-id="72751-180">完成時，選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="72751-180">When done, select **Save**.</span></span>

     ![儲存金鑰](./media/resource-group-create-service-principal-portal/save-key.png)

     <span data-ttu-id="72751-182">儲存金鑰之後會顯示金鑰的值。</span><span class="sxs-lookup"><span data-stu-id="72751-182">After saving the key, the value of the key is displayed.</span></span> <span data-ttu-id="72751-183">請複製此值，因為您之後就無法擷取金鑰。</span><span class="sxs-lookup"><span data-stu-id="72751-183">Copy this value because you are not able to retrieve the key later.</span></span> <span data-ttu-id="72751-184">您提供金鑰值和應用程式識別碼，能夠以應用程式方式登入。</span><span class="sxs-lookup"><span data-stu-id="72751-184">You provide the key value with the application ID to log in as the application.</span></span> <span data-ttu-id="72751-185">將金鑰值儲存在應用程式可擷取的地方。</span><span class="sxs-lookup"><span data-stu-id="72751-185">Store the key value where your application can retrieve it.</span></span>

     ![儲存的金鑰](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a><span data-ttu-id="72751-187">取得租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="72751-187">Get tenant ID</span></span>
<span data-ttu-id="72751-188">以程式設計方式登入時，您需要將租用戶識別碼與您的驗證要求一起傳送。</span><span class="sxs-lookup"><span data-stu-id="72751-188">When programmatically logging in, you need to pass the tenant ID with your authentication request.</span></span> 

1. <span data-ttu-id="72751-189">若要取得租用戶識別碼，請選取 Azure AD 租用戶的 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="72751-189">To get the tenant ID, select **Properties** for your Azure AD tenant.</span></span> 

     ![選取 Azure AD 屬性](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. <span data-ttu-id="72751-191">複製 [目錄識別碼]。</span><span class="sxs-lookup"><span data-stu-id="72751-191">Copy the **Directory ID**.</span></span> <span data-ttu-id="72751-192">這個值是您的租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="72751-192">This value is your tenant ID.</span></span>

     ![租用戶識別碼](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-to-role"></a><span data-ttu-id="72751-194">將應用程式指派給角色</span><span class="sxs-lookup"><span data-stu-id="72751-194">Assign application to role</span></span>
<span data-ttu-id="72751-195">若要存取您的訂用帳戶中的資源，您必須將應用程式指派給角色。</span><span class="sxs-lookup"><span data-stu-id="72751-195">To access resources in your subscription, you must assign the application to a role.</span></span> <span data-ttu-id="72751-196">決定哪個角色代表應用程式的正確權限。</span><span class="sxs-lookup"><span data-stu-id="72751-196">Decide which role represents the right permissions for the application.</span></span> <span data-ttu-id="72751-197">若要深入了解可用的角色，請參閱 [RBAC：內建角色](../active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="72751-197">To learn about the available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="72751-198">您可以針對訂用帳戶、資源群組或資源的層級設定範圍。</span><span class="sxs-lookup"><span data-stu-id="72751-198">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="72751-199">較低的範圍層級會繼承較高層級的權限。</span><span class="sxs-lookup"><span data-stu-id="72751-199">Permissions are inherited to lower levels of scope.</span></span> <span data-ttu-id="72751-200">例如，為資源群組的讀取者角色新增應用程式，代表該角色可以讀取資源群組及其所包含的任何資源。</span><span class="sxs-lookup"><span data-stu-id="72751-200">For example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains.</span></span>

1. <span data-ttu-id="72751-201">瀏覽至您想要讓應用程式指派至的範圍層級。</span><span class="sxs-lookup"><span data-stu-id="72751-201">Navigate to the level of scope you wish to assign the application to.</span></span> <span data-ttu-id="72751-202">例如，若要在訂用帳戶範圍指派角色，請選取 [訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="72751-202">For example, to assign a role at the subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="72751-203">您可以改為選取資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="72751-203">You could instead select a resource group or resource.</span></span>

     ![select subscription](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. <span data-ttu-id="72751-205">選取特定訂用帳戶作為指派應用程式的對象 (資源群組或資源)。</span><span class="sxs-lookup"><span data-stu-id="72751-205">Select the particular subscription (resource group or resource) to assign the application to.</span></span>

     ![選取要指派的訂用帳戶](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. <span data-ttu-id="72751-207">選取 [存取控制 (IAM)]。</span><span class="sxs-lookup"><span data-stu-id="72751-207">Select **Access Control (IAM)**.</span></span>

     ![選取存取](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. <span data-ttu-id="72751-209">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="72751-209">Select **Add**.</span></span>

     ![選取 [新增]](./media/resource-group-create-service-principal-portal/select-add.png)
6. <span data-ttu-id="72751-211">選取您想要將應用程式指派給哪個角色。</span><span class="sxs-lookup"><span data-stu-id="72751-211">Select the role you wish to assign to the application.</span></span> <span data-ttu-id="72751-212">下圖顯示**讀者**角色：</span><span class="sxs-lookup"><span data-stu-id="72751-212">The following image shows the **Reader** role.</span></span>

     ![選取角色](./media/resource-group-create-service-principal-portal/select-role.png)

8. <span data-ttu-id="72751-214">搜尋並選取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="72751-214">Search for your application, and select it.</span></span>

     ![搜尋應用程式](./media/resource-group-create-service-principal-portal/search-app.png)
9. <span data-ttu-id="72751-216">選取 [確定] 以完成角色指派。</span><span class="sxs-lookup"><span data-stu-id="72751-216">Select **OK** to finish assigning the role.</span></span> <span data-ttu-id="72751-217">您在使用者清單中看到應用程式已指派給該範圍的角色。</span><span class="sxs-lookup"><span data-stu-id="72751-217">You see your application in the list of users assigned to a role for that scope.</span></span>

## <a name="log-in-as-the-application"></a><span data-ttu-id="72751-218">以應用程式身分登入</span><span class="sxs-lookup"><span data-stu-id="72751-218">Log in as the application</span></span>

<span data-ttu-id="72751-219">您的應用程式現在已設定在 Azure Active Directory 中。</span><span class="sxs-lookup"><span data-stu-id="72751-219">Your application is now set up in Azure Active Directory.</span></span> <span data-ttu-id="72751-220">您有識別碼和金鑰可用應用程式方式登入。</span><span class="sxs-lookup"><span data-stu-id="72751-220">You have an ID and key to use for signing in as the application.</span></span> <span data-ttu-id="72751-221">系統會對應用程式指派角色，允許它執行特定動作。</span><span class="sxs-lookup"><span data-stu-id="72751-221">The application is assigned to a role that gives it certain actions it can perform.</span></span> <span data-ttu-id="72751-222">如需透過不同平台以應用程式身分登入的資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="72751-222">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="72751-223">PowerShell</span><span class="sxs-lookup"><span data-stu-id="72751-223">PowerShell</span></span>](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [<span data-ttu-id="72751-224">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="72751-224">Azure CLI</span></span>](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [<span data-ttu-id="72751-225">REST</span><span class="sxs-lookup"><span data-stu-id="72751-225">REST</span></span>](/rest/api/#create-the-request)
* [<span data-ttu-id="72751-226">.NET</span><span class="sxs-lookup"><span data-stu-id="72751-226">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="72751-227">Java</span><span class="sxs-lookup"><span data-stu-id="72751-227">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="72751-228">Node.js</span><span class="sxs-lookup"><span data-stu-id="72751-228">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="72751-229">Python</span><span class="sxs-lookup"><span data-stu-id="72751-229">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="72751-230">Ruby</span><span class="sxs-lookup"><span data-stu-id="72751-230">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a><span data-ttu-id="72751-231">後續步驟</span><span class="sxs-lookup"><span data-stu-id="72751-231">Next steps</span></span>
* <span data-ttu-id="72751-232">若要設定多租用戶應用程式，請參閱 [利用 Azure Resource Manager API 進行授權的開發人員指南](resource-manager-api-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="72751-232">To set up a multi-tenant application, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="72751-233">若要了解如何指定安全性原則，請參閱 [Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="72751-233">To learn about specifying security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>  
* <span data-ttu-id="72751-234">如需可授與或拒絕使用者的可用動作清單，請參閱 [Azure Resource Manager 資源提供者作業](../active-directory/role-based-access-control-resource-provider-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="72751-234">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
