---
title: "服務主體的 Azure 堆疊 aaaCreate |Microsoft 文件"
description: "描述如何 toocreate 新的服務主體，可以搭配 Azure Resource Manager toomanage 存取 tooresources hello 以角色為基礎的存取控制。"
services: azure-resource-manager
documentationcenter: na
author: heathl17
manager: byronr
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: helaw
ms.openlocfilehash: f090ceed941abe9255bc35ec966bc43df3bb2955
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="provide-applications-access-tooazure-stack"></a><span data-ttu-id="73db9-103">提供應用程式存取 tooAzure 堆疊</span><span class="sxs-lookup"><span data-stu-id="73db9-103">Provide applications access tooAzure Stack</span></span>
<span data-ttu-id="73db9-104">當應用程式需要存取 toodeploy 或 Azure 堆疊中設定資源透過 Azure 資源管理員時，您會建立服務主體，也就是您的應用程式的認證。</span><span class="sxs-lookup"><span data-stu-id="73db9-104">When an application needs access toodeploy or configure resources through Azure Resource Manager in Azure Stack, you create a service principal, which is a credential for your application.</span></span>  <span data-ttu-id="73db9-105">然後，您可以委派只能 hello 必要的權限 toothat 服務主體。</span><span class="sxs-lookup"><span data-stu-id="73db9-105">You can then delegate only hello necessary permissions toothat service principal.</span></span>  

<span data-ttu-id="73db9-106">例如，您可能會使用 Azure 資源管理員 tooinventory 組態管理工具的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="73db9-106">As an example, you may have a configuration management tool that uses Azure Resource Manager tooinventory Azure resources.</span></span>  <span data-ttu-id="73db9-107">在此案例中，您可以建立服務主體，和授與 hello 讀取器角色 toothat 服務主體，限制 hello 組態管理工具僅 tooread 的存取權。</span><span class="sxs-lookup"><span data-stu-id="73db9-107">In this scenario, you can create a service principal, grant hello reader role toothat service principal, and limit hello configuration management tool tooread-only access.</span></span> 

<span data-ttu-id="73db9-108">因為服務主體會是偏好的 toorunning hello 應用程式，以您自己的認證：</span><span class="sxs-lookup"><span data-stu-id="73db9-108">Service principals are preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="73db9-109">您可以指派不同於您自己的帳戶權限的權限 toohello 服務主體。</span><span class="sxs-lookup"><span data-stu-id="73db9-109">You can assign permissions toohello service principal that are different than your own account permissions.</span></span> <span data-ttu-id="73db9-110">一般而言，這些權限會限制的 tooexactly 哪些 hello 應用程式需要 toodo。</span><span class="sxs-lookup"><span data-stu-id="73db9-110">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="73db9-111">如果您的責任的變更，您並沒有 toochange hello 應用程式的認證。</span><span class="sxs-lookup"><span data-stu-id="73db9-111">You do not have toochange hello app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="73db9-112">執行無人看管的指令碼時，您可以使用憑證 tooautomate 驗證。</span><span class="sxs-lookup"><span data-stu-id="73db9-112">You can use a certificate tooautomate authentication when executing an unattended script.</span></span>  

## <a name="getting-started"></a><span data-ttu-id="73db9-113">開始使用</span><span class="sxs-lookup"><span data-stu-id="73db9-113">Getting started</span></span>

<span data-ttu-id="73db9-114">根據您部署 Azure Stack 的方式，您會從建立服務主體開始。</span><span class="sxs-lookup"><span data-stu-id="73db9-114">Depending on how you have deployed Azure Stack, you start by creating a service principal.</span></span>  <span data-ttu-id="73db9-115">此文件會引導您進行為 [Azure Active Directory (Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad) 和 [Active Directory Federation Services (AD FS)](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs) 建立服務主體的程序。</span><span class="sxs-lookup"><span data-stu-id="73db9-115">This document guides you through creating a service principal for both [Azure Active Directory (Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad) and [Active Directory Federation Services(AD FS)](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs).</span></span>  <span data-ttu-id="73db9-116">一旦您已建立服務主體 hello，整組步驟常見 tooboth AD FS 與 Azure Active Directory 可用太[委派權限](azure-stack-create-service-principals.md#assign-role-to-service-principal)toohello 角色。</span><span class="sxs-lookup"><span data-stu-id="73db9-116">Once you've created hello service principal, a set of steps common tooboth AD FS and Azure Active Directory are used too[delegate permissions](azure-stack-create-service-principals.md#assign-role-to-service-principal) toohello role.</span></span>     

## <a name="create-service-principal-for-azure-ad"></a><span data-ttu-id="73db9-117">為 Azure AD 建立服務主體</span><span class="sxs-lookup"><span data-stu-id="73db9-117">Create service principal for Azure AD</span></span>

<span data-ttu-id="73db9-118">如果您部署了 Azure 堆疊 hello 身分識別存放區以使用 Azure AD，您可以建立服務主體就像您的 Azure 執行。</span><span class="sxs-lookup"><span data-stu-id="73db9-118">If you've deployed Azure Stack using Azure AD as hello identity store, you can create service principals just like you do for Azure.</span></span>  <span data-ttu-id="73db9-119">本節說明如何 tooperform hello 逐步 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="73db9-119">This section shows you how tooperform hello steps through hello portal.</span></span>  <span data-ttu-id="73db9-120">請確認您已 hello[必要的 Azure AD 權限](../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions)開頭之前。</span><span class="sxs-lookup"><span data-stu-id="73db9-120">Check that you have hello [required Azure AD permissions](../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions) before beginning.</span></span>

### <a name="create-service-principal"></a><span data-ttu-id="73db9-121">建立服務主體</span><span class="sxs-lookup"><span data-stu-id="73db9-121">Create service principal</span></span>
<span data-ttu-id="73db9-122">在本節中，您會在 Azure AD 中建立將代表您的應用程式的應用程式 (服務主體)。</span><span class="sxs-lookup"><span data-stu-id="73db9-122">In this section, you create an application (service principal) in Azure AD that will represent your application.</span></span>

1. <span data-ttu-id="73db9-123">登入 tooyour Azure 帳戶透過 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="73db9-123">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="73db9-124">選取 [Azure Active Directory] > [應用程式註冊] > [新增]</span><span class="sxs-lookup"><span data-stu-id="73db9-124">Select **Azure Active Directory** > **App registrations** > **Add**</span></span>   
3. <span data-ttu-id="73db9-125">Hello 應用程式提供名稱和 URL。</span><span class="sxs-lookup"><span data-stu-id="73db9-125">Provide a name and URL for hello application.</span></span> <span data-ttu-id="73db9-126">選取  **Web 應用程式 / 應用程式開發介面**或**原生**想 toocreate hello 種應用程式。</span><span class="sxs-lookup"><span data-stu-id="73db9-126">Select either **Web app / API** or **Native** for hello type of application you want toocreate.</span></span> <span data-ttu-id="73db9-127">設定後 hello 值，請選取**建立**。</span><span class="sxs-lookup"><span data-stu-id="73db9-127">After setting hello values, select **Create**.</span></span>

<span data-ttu-id="73db9-128">您已建立應用程式的服務主體。</span><span class="sxs-lookup"><span data-stu-id="73db9-128">You have created a service principal for your application.</span></span>

### <a name="get-credentials"></a><span data-ttu-id="73db9-129">取得認證</span><span class="sxs-lookup"><span data-stu-id="73db9-129">Get credentials</span></span>
<span data-ttu-id="73db9-130">以程式設計方式登入時，您可以使用識別碼 hello 您的應用程式和驗證金鑰。</span><span class="sxs-lookup"><span data-stu-id="73db9-130">When programmatically logging in, you use hello ID for your application and an authentication key.</span></span> <span data-ttu-id="73db9-131">tooget 那些值，使用 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="73db9-131">tooget those values, use hello following steps:</span></span>

1. <span data-ttu-id="73db9-132">在 Active Directory 中，從 [應用程式註冊]選取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="73db9-132">From **App registrations** in Active Directory, select your application.</span></span>

2. <span data-ttu-id="73db9-133">複製 hello**應用程式識別碼**並將它儲存在應用程式程式碼中。</span><span class="sxs-lookup"><span data-stu-id="73db9-133">Copy hello **Application ID** and store it in your application code.</span></span> <span data-ttu-id="73db9-134">hello hello 中的應用程式[範例應用程式](#sample-applications)區段，請參閱 toothis hello 用戶端識別碼值。</span><span class="sxs-lookup"><span data-stu-id="73db9-134">hello applications in hello [sample applications](#sample-applications) section refer toothis value as hello client id.</span></span>

     ![用戶端識別碼](./media/azure-stack-create-service-principal/image12.png)
3. <span data-ttu-id="73db9-136">toogenerate 需有驗證金鑰，選取**金鑰**。</span><span class="sxs-lookup"><span data-stu-id="73db9-136">toogenerate an authentication key, select **Keys**.</span></span>

4. <span data-ttu-id="73db9-137">提供 hello 金鑰和 hello 金鑰的持續時間的描述。</span><span class="sxs-lookup"><span data-stu-id="73db9-137">Provide a description of hello key, and a duration for hello key.</span></span> <span data-ttu-id="73db9-138">完成時，選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="73db9-138">When done, select **Save**.</span></span>

<span data-ttu-id="73db9-139">在儲存之後 hello 索引鍵，會顯示 hello hello 機碼值。</span><span class="sxs-lookup"><span data-stu-id="73db9-139">After saving hello key, hello value of hello key is displayed.</span></span> <span data-ttu-id="73db9-140">因為您不能 tooretrieve hello 金鑰之後，請複製此值。</span><span class="sxs-lookup"><span data-stu-id="73db9-140">Copy this value because you are not able tooretrieve hello key later.</span></span> <span data-ttu-id="73db9-141">您提供 hello 索引鍵值 hello 應用程式識別碼 toosign hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="73db9-141">You provide hello key value with hello application ID toosign as hello application.</span></span> <span data-ttu-id="73db9-142">儲存您的應用程式可以擷取 hello 機碼值。</span><span class="sxs-lookup"><span data-stu-id="73db9-142">Store hello key value where your application can retrieve it.</span></span>

![儲存的金鑰](./media/azure-stack-create-service-principal/image15.png)


<span data-ttu-id="73db9-144">完成後，繼續太[將您的應用程式角色的指派](azure-stack-create-service-principals.md#assign-role-to-service-principal)。</span><span class="sxs-lookup"><span data-stu-id="73db9-144">Once complete, proceed too[assigning your application a role](azure-stack-create-service-principals.md#assign-role-to-service-principal).</span></span>

## <a name="create-service-principal-for-ad-fs"></a><span data-ttu-id="73db9-145">為 AD FS 建立服務主體</span><span class="sxs-lookup"><span data-stu-id="73db9-145">Create service principal for AD FS</span></span>
<span data-ttu-id="73db9-146">如果您已部署 AD FS 與 Azure 堆疊，可以使用 PowerShell toocreate 服務主體、 指派的角色存取權，以及 PowerShell 中使用該識別從登入。</span><span class="sxs-lookup"><span data-stu-id="73db9-146">If you have deployed Azure Stack with AD FS, you can use PowerShell toocreate a service principal, assign a role for access, and sign in from PowerShell using that identity.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="73db9-147">開始之前</span><span class="sxs-lookup"><span data-stu-id="73db9-147">Before you begin</span></span>

[<span data-ttu-id="73db9-148">下載 hello 工具需要的 toowork 與 Azure 堆疊 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="73db9-148">Download hello tools required toowork with Azure Stack tooyour local computer.</span></span>](azure-stack-powershell-download.md)

### <a name="import-hello-identity-powershell-module"></a><span data-ttu-id="73db9-149">匯入 hello 識別 PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="73db9-149">Import hello Identity PowerShell module</span></span>
<span data-ttu-id="73db9-150">下載 hello 工具之後，瀏覽 toohello 下載資料夾，並使用下列命令的 hello 匯入 hello 識別 PowerShell 模組：</span><span class="sxs-lookup"><span data-stu-id="73db9-150">After you download hello tools, navigate toohello downloaded folder and import hello Identity PowerShell module by using hello following command:</span></span>

```PowerShell
Import-Module .\Identity\AzureStack.Identity.psm1
```

<span data-ttu-id="73db9-151">當您匯入 hello 模組時，您可能會收到錯誤指出 「 AzureStack.Connect.psm1 未經數位簽署。</span><span class="sxs-lookup"><span data-stu-id="73db9-151">When you import hello module, you may receive an error that says “AzureStack.Connect.psm1 is not digitally signed.</span></span> <span data-ttu-id="73db9-152">hello 指令碼不會執行 hello 系統上 」。</span><span class="sxs-lookup"><span data-stu-id="73db9-152">hello script will not execute on hello system”.</span></span> <span data-ttu-id="73db9-153">tooresolve 此問題，您可以設定執行原則 tooallow hello 指令碼執行下列命令，在提升權限的 PowerShell 工作階段中的 hello:</span><span class="sxs-lookup"><span data-stu-id="73db9-153">tooresolve this issue, you can set execution policy tooallow running hello script with hello following command in an elevated PowerShell session:</span></span>

```PowerShell
Set-ExecutionPolicy Unrestricted
```

### <a name="create-hello-service-principal"></a><span data-ttu-id="73db9-154">建立服務主體的 hello</span><span class="sxs-lookup"><span data-stu-id="73db9-154">Create hello service principal</span></span>
<span data-ttu-id="73db9-155">您可以建立服務主體執行 hello 下列命令，讓確定 tooupdate hello *DisplayName*參數：</span><span class="sxs-lookup"><span data-stu-id="73db9-155">You can create a Service Principal by executing hello following command, making sure tooupdate hello *DisplayName* parameter:</span></span>
```powershell
$servicePrincipal = New-AzSADGraphServicePrincipal `
 -DisplayName "<YourServicePrincipalName>" `
 -AdminCredential $(Get-Credential) `
 -AdfsMachineName "AZS-ADFS01" `
 -Verbose
```
### <a name="assign-a-role"></a><span data-ttu-id="73db9-156">指派角色</span><span class="sxs-lookup"><span data-stu-id="73db9-156">Assign a role</span></span>
<span data-ttu-id="73db9-157">您必須在建立服務主體的 hello，一次[tooa 角色指派給它](azure-stack-create-service-principals.md#assign-role-to-service-principal)</span><span class="sxs-lookup"><span data-stu-id="73db9-157">Once hello Service Principal is created, you must [assign it tooa role](azure-stack-create-service-principals.md#assign-role-to-service-principal)</span></span>

### <a name="sign-in-through-powershell"></a><span data-ttu-id="73db9-158">透過 PowerShell 登入</span><span class="sxs-lookup"><span data-stu-id="73db9-158">Sign in through PowerShell</span></span>
<span data-ttu-id="73db9-159">一旦您已指派一個角色，您可以登入 tooAzure 堆疊 hello 服務主體使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="73db9-159">Once you've assigned a role, you can sign in tooAzure Stack using hello service principal with hello following command:</span></span>

```powershell
Add-AzureRmAccount -EnvironmentName "<AzureStackEnvironmentName>" `
 -ServicePrincipal `
 -CertificateThumbprint $servicePrincipal.Thumbprint `
 -ApplicationId $servicePrincipal.ApplicationId ` 
 -TenantId $directoryTenantId
```

## <a name="assign-role-tooservice-principal"></a><span data-ttu-id="73db9-160">指派角色 tooservice 主體</span><span class="sxs-lookup"><span data-stu-id="73db9-160">Assign role tooservice principal</span></span>
<span data-ttu-id="73db9-161">您的訂用帳戶中的 tooaccess 資源，您必須指派 hello 應用程式 tooa 角色。</span><span class="sxs-lookup"><span data-stu-id="73db9-161">tooaccess resources in your subscription, you must assign hello application tooa role.</span></span> <span data-ttu-id="73db9-162">決定哪些角色代表 hello hello 應用程式的正確權限。</span><span class="sxs-lookup"><span data-stu-id="73db9-162">Decide which role represents hello right permissions for hello application.</span></span> <span data-ttu-id="73db9-163">toolearn 有關 hello 可用的角色，請參閱[RBAC： 內建的角色](../active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="73db9-163">toolearn about hello available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="73db9-164">您可以設定 hello 範圍層級 hello hello 訂用帳戶、 資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="73db9-164">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="73db9-165">權限是繼承的 toolower 範圍層級。</span><span class="sxs-lookup"><span data-stu-id="73db9-165">Permissions are inherited toolower levels of scope.</span></span> <span data-ttu-id="73db9-166">例如，新增資源群組的應用程式 toohello 讀取器角色表示它可以讀取 hello 資源群組和它所包含的任何資源。</span><span class="sxs-lookup"><span data-stu-id="73db9-166">For example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains.</span></span>

1. <span data-ttu-id="73db9-167">在 hello Azure 堆疊入口網站中，瀏覽 toohello 想 tooassign hello 應用程式的範圍層級。</span><span class="sxs-lookup"><span data-stu-id="73db9-167">In hello Azure Stack portal, navigate toohello level of scope you wish tooassign hello application to.</span></span> <span data-ttu-id="73db9-168">例如，tooassign hello 訂用帳戶範圍，角色選取**訂閱**。</span><span class="sxs-lookup"><span data-stu-id="73db9-168">For example, tooassign a role at hello subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="73db9-169">您可以改為選取資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="73db9-169">You could instead select a resource group or resource.</span></span>

2. <span data-ttu-id="73db9-170">選取 hello 特定訂用帳戶 （資源群組或資源） tooassign hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="73db9-170">Select hello particular subscription (resource group or resource) tooassign hello application to.</span></span>

     ![選取要指派的訂用帳戶](./media/azure-stack-create-service-principal/image16.png)

3. <span data-ttu-id="73db9-172">選取 [存取控制 (IAM)]。</span><span class="sxs-lookup"><span data-stu-id="73db9-172">Select **Access Control (IAM)**.</span></span>

     ![選取存取](./media/azure-stack-create-service-principal/image17.png)

4. <span data-ttu-id="73db9-174">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="73db9-174">Select **Add**.</span></span>

5. <span data-ttu-id="73db9-175">選取您想 tooassign toohello 應用程式的 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="73db9-175">Select hello role you wish tooassign toohello application.</span></span>

6. <span data-ttu-id="73db9-176">搜尋並選取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="73db9-176">Search for your application, and select it.</span></span>

7. <span data-ttu-id="73db9-177">選取**確定**toofinish 指派 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="73db9-177">Select **OK** toofinish assigning hello role.</span></span> <span data-ttu-id="73db9-178">您會看到您 hello 清單中指派該範圍的 tooa 角色之使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="73db9-178">You see your application in hello list of users assigned tooa role for that scope.</span></span>

<span data-ttu-id="73db9-179">既然您已建立服務主體，並指派角色，您可以開始使用這在您的應用程式 tooaccess Azure 堆疊資源。</span><span class="sxs-lookup"><span data-stu-id="73db9-179">Now that you've created a service principal and assigned a role, you can begin using this within your application tooaccess Azure Stack resources.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="73db9-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="73db9-180">Next steps</span></span>

<span data-ttu-id="73db9-181">[為 ADFS 新增使用者](azure-stack-add-users-adfs.md)
[管理使用者權限](azure-stack-manage-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="73db9-181">[Add users for ADFS](azure-stack-add-users-adfs.md)
[Manage user permissions](azure-stack-manage-permissions.md)</span></span>