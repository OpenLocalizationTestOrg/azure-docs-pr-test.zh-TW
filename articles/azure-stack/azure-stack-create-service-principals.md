---
title: "為 Azure Stack 建立服務主體 | Microsoft Docs"
description: "描述如何建立可以與 Azure Resource Manager 中的角色型存取控制搭配使用來管理資源存取權的新服務主體。"
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
ms.openlocfilehash: b3992b296d5a999601eb69b071559f9d37dacf8f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="provide-applications-access-to-azure-stack"></a><span data-ttu-id="81d59-103">為 Azure Stack 提供應用程式存取</span><span class="sxs-lookup"><span data-stu-id="81d59-103">Provide applications access to Azure Stack</span></span>
<span data-ttu-id="81d59-104">當應用程式需要存取權透過 Azure Resource Manager 在 Azure Stack 中部署或設定資源時，您會建立服務主體，這是您的應用程式的認證。</span><span class="sxs-lookup"><span data-stu-id="81d59-104">When an application needs access to deploy or configure resources through Azure Resource Manager in Azure Stack, you create a service principal, which is a credential for your application.</span></span>  <span data-ttu-id="81d59-105">然後，您可以只對該服務主體委派必要權限。</span><span class="sxs-lookup"><span data-stu-id="81d59-105">You can then delegate only the necessary permissions to that service principal.</span></span>  

<span data-ttu-id="81d59-106">舉例來說，您可能有使用 Azure Resource Manager 來清查 Azure 資源的組態管理工具。</span><span class="sxs-lookup"><span data-stu-id="81d59-106">As an example, you may have a configuration management tool that uses Azure Resource Manager to inventory Azure resources.</span></span>  <span data-ttu-id="81d59-107">在此案例中，您可以建立服務主體、為該服務主體授與讀取者角色，以及將組態管理工具限制在唯讀存取權。</span><span class="sxs-lookup"><span data-stu-id="81d59-107">In this scenario, you can create a service principal, grant the reader role to that service principal, and limit the configuration management tool to read-only access.</span></span> 

<span data-ttu-id="81d59-108">以您自己的認證執行應用程式最好是使用服務主體，因為：</span><span class="sxs-lookup"><span data-stu-id="81d59-108">Service principals are preferable to running the app under your own credentials because:</span></span>

* <span data-ttu-id="81d59-109">您可以對服務主體指派不同於您自己帳戶權限的權限。</span><span class="sxs-lookup"><span data-stu-id="81d59-109">You can assign permissions to the service principal that are different than your own account permissions.</span></span> <span data-ttu-id="81d59-110">一般而言，這些權限只會限制為 App 必須執行的確切權限。</span><span class="sxs-lookup"><span data-stu-id="81d59-110">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="81d59-111">如果您的職責變更，就不需要變更 App 的認證。</span><span class="sxs-lookup"><span data-stu-id="81d59-111">You do not have to change the app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="81d59-112">您可以使用憑證在執行自動指令碼時自動進行驗證。</span><span class="sxs-lookup"><span data-stu-id="81d59-112">You can use a certificate to automate authentication when executing an unattended script.</span></span>  

## <a name="getting-started"></a><span data-ttu-id="81d59-113">開始使用</span><span class="sxs-lookup"><span data-stu-id="81d59-113">Getting started</span></span>

<span data-ttu-id="81d59-114">根據您部署 Azure Stack 的方式，您會從建立服務主體開始。</span><span class="sxs-lookup"><span data-stu-id="81d59-114">Depending on how you have deployed Azure Stack, you start by creating a service principal.</span></span>  <span data-ttu-id="81d59-115">此文件會引導您進行為 [Azure Active Directory (Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad) 和 [Active Directory Federation Services (AD FS)](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs) 建立服務主體的程序。</span><span class="sxs-lookup"><span data-stu-id="81d59-115">This document guides you through creating a service principal for both [Azure Active Directory (Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad) and [Active Directory Federation Services(AD FS)](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs).</span></span>  <span data-ttu-id="81d59-116">一旦您已建立服務主體，會使用 AD FS 與 Azure Active Directory 的一組共通步驟來對角色[委派權限](azure-stack-create-service-principals.md#assign-role-to-service-principal)。</span><span class="sxs-lookup"><span data-stu-id="81d59-116">Once you've created the service principal, a set of steps common to both AD FS and Azure Active Directory are used to [delegate permissions](azure-stack-create-service-principals.md#assign-role-to-service-principal) to the role.</span></span>     

## <a name="create-service-principal-for-azure-ad"></a><span data-ttu-id="81d59-117">為 Azure AD 建立服務主體</span><span class="sxs-lookup"><span data-stu-id="81d59-117">Create service principal for Azure AD</span></span>

<span data-ttu-id="81d59-118">如果您使用 Azure AD 做為身分識別存放區部署了 Azure Stack，則可以如同對 Azure 般建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="81d59-118">If you've deployed Azure Stack using Azure AD as the identity store, you can create service principals just like you do for Azure.</span></span>  <span data-ttu-id="81d59-119">本節說明如何透過入口網站執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="81d59-119">This section shows you how to perform the steps through the portal.</span></span>  <span data-ttu-id="81d59-120">開始之前，請確認您有[必要的 Azure AD 權限](../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions)。</span><span class="sxs-lookup"><span data-stu-id="81d59-120">Check that you have the [required Azure AD permissions](../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions) before beginning.</span></span>

### <a name="create-service-principal"></a><span data-ttu-id="81d59-121">建立服務主體</span><span class="sxs-lookup"><span data-stu-id="81d59-121">Create service principal</span></span>
<span data-ttu-id="81d59-122">在本節中，您會在 Azure AD 中建立將代表您的應用程式的應用程式 (服務主體)。</span><span class="sxs-lookup"><span data-stu-id="81d59-122">In this section, you create an application (service principal) in Azure AD that will represent your application.</span></span>

1. <span data-ttu-id="81d59-123">透過 [Azure 入口網站](https://portal.azure.com)登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="81d59-123">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="81d59-124">選取 [Azure Active Directory] > [應用程式註冊] > [新增]</span><span class="sxs-lookup"><span data-stu-id="81d59-124">Select **Azure Active Directory** > **App registrations** > **Add**</span></span>   
3. <span data-ttu-id="81d59-125">提供應用程式的名稱和 URL。</span><span class="sxs-lookup"><span data-stu-id="81d59-125">Provide a name and URL for the application.</span></span> <span data-ttu-id="81d59-126">針對您想要建立的應用程式類型，選取 [Web 應用程式/API] 或 [原生]。</span><span class="sxs-lookup"><span data-stu-id="81d59-126">Select either **Web app / API** or **Native** for the type of application you want to create.</span></span> <span data-ttu-id="81d59-127">設定值之後，選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="81d59-127">After setting the values, select **Create**.</span></span>

<span data-ttu-id="81d59-128">您已建立應用程式的服務主體。</span><span class="sxs-lookup"><span data-stu-id="81d59-128">You have created a service principal for your application.</span></span>

### <a name="get-credentials"></a><span data-ttu-id="81d59-129">取得認證</span><span class="sxs-lookup"><span data-stu-id="81d59-129">Get credentials</span></span>
<span data-ttu-id="81d59-130">以程式設計方式登入時，您會使用應用程式的識別碼和驗證金鑰。</span><span class="sxs-lookup"><span data-stu-id="81d59-130">When programmatically logging in, you use the ID for your application and an authentication key.</span></span> <span data-ttu-id="81d59-131">若要取得這些值，請使用下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="81d59-131">To get those values, use the following steps:</span></span>

1. <span data-ttu-id="81d59-132">在 Active Directory 中，從 [應用程式註冊]選取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="81d59-132">From **App registrations** in Active Directory, select your application.</span></span>

2. <span data-ttu-id="81d59-133">複製 [應用程式識別碼] 並儲存在您的應用程式碼中。</span><span class="sxs-lookup"><span data-stu-id="81d59-133">Copy the **Application ID** and store it in your application code.</span></span> <span data-ttu-id="81d59-134">[範例應用程式](#sample-applications) 區段中的應用程式會參考此值作為用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="81d59-134">The applications in the [sample applications](#sample-applications) section refer to this value as the client id.</span></span>

     ![用戶端識別碼](./media/azure-stack-create-service-principal/image12.png)
3. <span data-ttu-id="81d59-136">若要產生驗證金鑰，請選取 [金鑰]。</span><span class="sxs-lookup"><span data-stu-id="81d59-136">To generate an authentication key, select **Keys**.</span></span>

4. <span data-ttu-id="81d59-137">提供金鑰的描述和金鑰的持續時間。</span><span class="sxs-lookup"><span data-stu-id="81d59-137">Provide a description of the key, and a duration for the key.</span></span> <span data-ttu-id="81d59-138">完成時，選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="81d59-138">When done, select **Save**.</span></span>

<span data-ttu-id="81d59-139">儲存金鑰之後會顯示金鑰的值。</span><span class="sxs-lookup"><span data-stu-id="81d59-139">After saving the key, the value of the key is displayed.</span></span> <span data-ttu-id="81d59-140">請複製此值，因為您之後就無法擷取金鑰。</span><span class="sxs-lookup"><span data-stu-id="81d59-140">Copy this value because you are not able to retrieve the key later.</span></span> <span data-ttu-id="81d59-141">您提供金鑰值和應用程式識別碼，以應用程式身分簽署。</span><span class="sxs-lookup"><span data-stu-id="81d59-141">You provide the key value with the application ID to sign as the application.</span></span> <span data-ttu-id="81d59-142">將金鑰值儲存在應用程式可擷取的地方。</span><span class="sxs-lookup"><span data-stu-id="81d59-142">Store the key value where your application can retrieve it.</span></span>

![儲存的金鑰](./media/azure-stack-create-service-principal/image15.png)


<span data-ttu-id="81d59-144">完成後，繼續進行[將您的應用程式指派至角色](azure-stack-create-service-principals.md#assign-role-to-service-principal)。</span><span class="sxs-lookup"><span data-stu-id="81d59-144">Once complete, proceed to [assigning your application a role](azure-stack-create-service-principals.md#assign-role-to-service-principal).</span></span>

## <a name="create-service-principal-for-ad-fs"></a><span data-ttu-id="81d59-145">為 AD FS 建立服務主體</span><span class="sxs-lookup"><span data-stu-id="81d59-145">Create service principal for AD FS</span></span>
<span data-ttu-id="81d59-146">如果您是使用 Azure Stack 部署 AD FS，則可以使用 PowerShell 來建立服務主體、指派用於存取的角色，以及從 PowerShell 使用該身分識別登入。</span><span class="sxs-lookup"><span data-stu-id="81d59-146">If you have deployed Azure Stack with AD FS, you can use PowerShell to create a service principal, assign a role for access, and sign in from PowerShell using that identity.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="81d59-147">開始之前</span><span class="sxs-lookup"><span data-stu-id="81d59-147">Before you begin</span></span>

[<span data-ttu-id="81d59-148">下載與 Azure Stack 搭配運作所需的工具到您的本機電腦。</span><span class="sxs-lookup"><span data-stu-id="81d59-148">Download the tools required to work with Azure Stack to your local computer.</span></span>](azure-stack-powershell-download.md)

### <a name="import-the-identity-powershell-module"></a><span data-ttu-id="81d59-149">匯入身分識別 PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="81d59-149">Import the Identity PowerShell module</span></span>
<span data-ttu-id="81d59-150">下載工具之後，瀏覽至 [下載] 資料夾，並使用下列命令來匯入身分識別 PowerShell 模組：</span><span class="sxs-lookup"><span data-stu-id="81d59-150">After you download the tools, navigate to the downloaded folder and import the Identity PowerShell module by using the following command:</span></span>

```PowerShell
Import-Module .\Identity\AzureStack.Identity.psm1
```

<span data-ttu-id="81d59-151">匯入模組時，您可能會收到錯誤指出「AzureStack.Connect.psm1 未經過數位簽署。</span><span class="sxs-lookup"><span data-stu-id="81d59-151">When you import the module, you may receive an error that says “AzureStack.Connect.psm1 is not digitally signed.</span></span> <span data-ttu-id="81d59-152">這個指令碼將不會在系統上執行」。</span><span class="sxs-lookup"><span data-stu-id="81d59-152">The script will not execute on the system”.</span></span> <span data-ttu-id="81d59-153">若要解決此問題，您可以在提升權限的 PowerShell 工作階段中使用下列命令來設定執行原則，以允許執行指令碼：</span><span class="sxs-lookup"><span data-stu-id="81d59-153">To resolve this issue, you can set execution policy to allow running the script with the following command in an elevated PowerShell session:</span></span>

```PowerShell
Set-ExecutionPolicy Unrestricted
```

### <a name="create-the-service-principal"></a><span data-ttu-id="81d59-154">建立服務主體</span><span class="sxs-lookup"><span data-stu-id="81d59-154">Create the service principal</span></span>
<span data-ttu-id="81d59-155">您可以藉由執行下列命令來建立服務主體，請務必更新 *DisplayName* 參數：</span><span class="sxs-lookup"><span data-stu-id="81d59-155">You can create a Service Principal by executing the following command, making sure to update the *DisplayName* parameter:</span></span>
```powershell
$servicePrincipal = New-AzSADGraphServicePrincipal `
 -DisplayName "<YourServicePrincipalName>" `
 -AdminCredential $(Get-Credential) `
 -AdfsMachineName "AZS-ADFS01" `
 -Verbose
```
### <a name="assign-a-role"></a><span data-ttu-id="81d59-156">指派角色</span><span class="sxs-lookup"><span data-stu-id="81d59-156">Assign a role</span></span>
<span data-ttu-id="81d59-157">一旦建立服務主體，您必須[將它指派至角色](azure-stack-create-service-principals.md#assign-role-to-service-principal)</span><span class="sxs-lookup"><span data-stu-id="81d59-157">Once the Service Principal is created, you must [assign it to a role](azure-stack-create-service-principals.md#assign-role-to-service-principal)</span></span>

### <a name="sign-in-through-powershell"></a><span data-ttu-id="81d59-158">透過 PowerShell 登入</span><span class="sxs-lookup"><span data-stu-id="81d59-158">Sign in through PowerShell</span></span>
<span data-ttu-id="81d59-159">一旦已指派角色，您可以使用服務主體搭配下列命令登入 Azure Stack：</span><span class="sxs-lookup"><span data-stu-id="81d59-159">Once you've assigned a role, you can sign in to Azure Stack using the service principal with the following command:</span></span>

```powershell
Add-AzureRmAccount -EnvironmentName "<AzureStackEnvironmentName>" `
 -ServicePrincipal `
 -CertificateThumbprint $servicePrincipal.Thumbprint `
 -ApplicationId $servicePrincipal.ApplicationId ` 
 -TenantId $directoryTenantId
```

## <a name="assign-role-to-service-principal"></a><span data-ttu-id="81d59-160">指派角色給服務主體</span><span class="sxs-lookup"><span data-stu-id="81d59-160">Assign role to service principal</span></span>
<span data-ttu-id="81d59-161">若要存取您的訂用帳戶中的資源，您必須將應用程式指派給角色。</span><span class="sxs-lookup"><span data-stu-id="81d59-161">To access resources in your subscription, you must assign the application to a role.</span></span> <span data-ttu-id="81d59-162">決定哪個角色代表應用程式的正確權限。</span><span class="sxs-lookup"><span data-stu-id="81d59-162">Decide which role represents the right permissions for the application.</span></span> <span data-ttu-id="81d59-163">若要深入了解可用的角色，請參閱 [RBAC：內建角色](../active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="81d59-163">To learn about the available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="81d59-164">您可以針對訂用帳戶、資源群組或資源的層級設定範圍。</span><span class="sxs-lookup"><span data-stu-id="81d59-164">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="81d59-165">較低的範圍層級會繼承較高層級的權限。</span><span class="sxs-lookup"><span data-stu-id="81d59-165">Permissions are inherited to lower levels of scope.</span></span> <span data-ttu-id="81d59-166">例如，為資源群組的讀取者角色新增應用程式，代表該角色可以讀取資源群組及其所包含的任何資源。</span><span class="sxs-lookup"><span data-stu-id="81d59-166">For example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains.</span></span>

1. <span data-ttu-id="81d59-167">在 Azure Stack 入口網站中，瀏覽至您想要指派應用程式的範圍層級。</span><span class="sxs-lookup"><span data-stu-id="81d59-167">In the Azure Stack portal, navigate to the level of scope you wish to assign the application to.</span></span> <span data-ttu-id="81d59-168">例如，若要在訂用帳戶範圍指派角色，請選取 [訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="81d59-168">For example, to assign a role at the subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="81d59-169">您可以改為選取資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="81d59-169">You could instead select a resource group or resource.</span></span>

2. <span data-ttu-id="81d59-170">選取特定訂用帳戶作為指派應用程式的對象 (資源群組或資源)。</span><span class="sxs-lookup"><span data-stu-id="81d59-170">Select the particular subscription (resource group or resource) to assign the application to.</span></span>

     ![選取要指派的訂用帳戶](./media/azure-stack-create-service-principal/image16.png)

3. <span data-ttu-id="81d59-172">選取 [存取控制 (IAM)]。</span><span class="sxs-lookup"><span data-stu-id="81d59-172">Select **Access Control (IAM)**.</span></span>

     ![選取存取](./media/azure-stack-create-service-principal/image17.png)

4. <span data-ttu-id="81d59-174">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="81d59-174">Select **Add**.</span></span>

5. <span data-ttu-id="81d59-175">選取您想要將應用程式指派給哪個角色。</span><span class="sxs-lookup"><span data-stu-id="81d59-175">Select the role you wish to assign to the application.</span></span>

6. <span data-ttu-id="81d59-176">搜尋並選取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="81d59-176">Search for your application, and select it.</span></span>

7. <span data-ttu-id="81d59-177">選取 [確定] 以完成角色指派。</span><span class="sxs-lookup"><span data-stu-id="81d59-177">Select **OK** to finish assigning the role.</span></span> <span data-ttu-id="81d59-178">您在使用者清單中看到應用程式已指派給該範圍的角色。</span><span class="sxs-lookup"><span data-stu-id="81d59-178">You see your application in the list of users assigned to a role for that scope.</span></span>

<span data-ttu-id="81d59-179">既然您已建立服務主體並指派角色，您可以開始在應用程式內使用它來存取 Azure Stack 資源。</span><span class="sxs-lookup"><span data-stu-id="81d59-179">Now that you've created a service principal and assigned a role, you can begin using this within your application to access Azure Stack resources.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="81d59-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="81d59-180">Next steps</span></span>

<span data-ttu-id="81d59-181">[為 ADFS 新增使用者](azure-stack-add-users-adfs.md)
[管理使用者權限](azure-stack-manage-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="81d59-181">[Add users for ADFS](azure-stack-add-users-adfs.md)
[Manage user permissions](azure-stack-manage-permissions.md)</span></span>