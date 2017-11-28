---
title: "使用 PowerShell 建立 Azure App 的身分識別 | Microsoft Docs"
description: "描述如何使用 Azure PowerShell 建立 Azure Active Directory 應用程式和服務主體，並透過角色型存取控制將存取權授與資源。 它示範如何使用密碼或憑證來驗證應用程式。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: d2caf121-9fbe-4f00-bf9d-8f3d1f00a6ff
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 55e83b0742652abbb42100a11a468bc13a7a8aed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-azure-powershell-to-create-a-service-principal-to-access-resources"></a><span data-ttu-id="23256-104">使用 Azure PowerShell 建立用來存取資源的服務主體</span><span class="sxs-lookup"><span data-stu-id="23256-104">Use Azure PowerShell to create a service principal to access resources</span></span>

<span data-ttu-id="23256-105">當您有 App 或指令碼需要存取資源時，可以設定 App 的身分識別，並使用 App 自己的認證進行驗證。</span><span class="sxs-lookup"><span data-stu-id="23256-105">When you have an app or script that needs to access resources, you can set up an identity for the app and authenticate the app with its own credentials.</span></span> <span data-ttu-id="23256-106">此身分識別就是所謂的服務主體。</span><span class="sxs-lookup"><span data-stu-id="23256-106">This identity is known as a service principal.</span></span> <span data-ttu-id="23256-107">這種方法可讓您︰</span><span class="sxs-lookup"><span data-stu-id="23256-107">This approach enables you to:</span></span>

* <span data-ttu-id="23256-108">將權限指派給不同於您自己權限的 App 身分識別。</span><span class="sxs-lookup"><span data-stu-id="23256-108">Assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="23256-109">一般而言，這些權限只會限制為 App 必須執行的確切權限。</span><span class="sxs-lookup"><span data-stu-id="23256-109">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="23256-110">使用憑證在執行無人看管的指令碼時進行驗證。</span><span class="sxs-lookup"><span data-stu-id="23256-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="23256-111">本主題說明如何使用 [Azure PowerShell](/powershell/azure/overview) 來設定所需的一切項目，以便讓應用程式利用自己的認證和身分識別來執行。</span><span class="sxs-lookup"><span data-stu-id="23256-111">This topic shows you how to use [Azure PowerShell](/powershell/azure/overview) to set up everything you need for an application to run under its own credentials and identity.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="23256-112">所需的權限</span><span class="sxs-lookup"><span data-stu-id="23256-112">Required permissions</span></span>
<span data-ttu-id="23256-113">若要完成本主題，您必須在 Azure Active Directory 和您的 Azure 訂用帳戶中有足夠的權限。</span><span class="sxs-lookup"><span data-stu-id="23256-113">To complete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="23256-114">具體來說，您必須能夠在 Azure Active Directory 中建立應用程式，並將服務主體指派給角色。</span><span class="sxs-lookup"><span data-stu-id="23256-114">Specifically, you must be able to create an app in the Azure Active Directory, and assign the service principal to a role.</span></span> 

<span data-ttu-id="23256-115">檢查您的帳戶是否具有足夠的權限，最簡單的方式是透過入口網站。</span><span class="sxs-lookup"><span data-stu-id="23256-115">The easiest way to check whether your account has adequate permissions is through the portal.</span></span> <span data-ttu-id="23256-116">請參閱[檢查必要的權限](resource-group-create-service-principal-portal.md#required-permissions)。</span><span class="sxs-lookup"><span data-stu-id="23256-116">See [Check required permission](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="23256-117">現在，繼續使用下列方式進行驗證的區段：</span><span class="sxs-lookup"><span data-stu-id="23256-117">Now, proceed to a section for authenticating with:</span></span>

* [<span data-ttu-id="23256-118">password</span><span class="sxs-lookup"><span data-stu-id="23256-118">password</span></span>](#create-service-principal-with-password)
* [<span data-ttu-id="23256-119">自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="23256-119">self-signed certificate</span></span>](#create-service-principal-with-self-signed-certificate)
* [<span data-ttu-id="23256-120">來自憑證授權單位的憑證</span><span class="sxs-lookup"><span data-stu-id="23256-120">certificate from Certificate Authority</span></span>](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a><span data-ttu-id="23256-121">PowerShell 命令</span><span class="sxs-lookup"><span data-stu-id="23256-121">PowerShell commands</span></span>

<span data-ttu-id="23256-122">若要設定服務主體，您要使用︰</span><span class="sxs-lookup"><span data-stu-id="23256-122">To set up a service principal, you use:</span></span>

| <span data-ttu-id="23256-123">命令</span><span class="sxs-lookup"><span data-stu-id="23256-123">Command</span></span> | <span data-ttu-id="23256-124">說明</span><span class="sxs-lookup"><span data-stu-id="23256-124">Description</span></span> |
| ------- | ----------- | 
| [<span data-ttu-id="23256-125">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="23256-125">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="23256-126">建立 Azure Active Directory 服務主體</span><span class="sxs-lookup"><span data-stu-id="23256-126">Creates an Azure Active Directory service principal</span></span> |
| [<span data-ttu-id="23256-127">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="23256-127">New-AzureRmRoleAssignment</span></span>](/powershell/module/azurerm.resources/new-azurermroleassignment) | <span data-ttu-id="23256-128">在指定的範圍中，將指定的 RBAC 角色指派給指定的主體。</span><span class="sxs-lookup"><span data-stu-id="23256-128">Assigns the specified RBAC role to the specified principal, at the specified scope.</span></span> |


## <a name="create-service-principal-with-password"></a><span data-ttu-id="23256-129">使用密碼建立服務主體</span><span class="sxs-lookup"><span data-stu-id="23256-129">Create service principal with password</span></span>

<span data-ttu-id="23256-130">若要使用您訂用帳戶的參與者角色來建立服務主體，請使用︰</span><span class="sxs-lookup"><span data-stu-id="23256-130">To create a service principal with the Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="23256-131">範例會睡 20 秒，留一些時間讓新的服務主體在整個 Azure Active Directory 中傳播。</span><span class="sxs-lookup"><span data-stu-id="23256-131">The example sleeps for 20 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="23256-132">如果您的指令碼等得不夠久，您會看到錯誤指出：「PrincipalNotFound︰主體 {id} 不存在於目錄中」。</span><span class="sxs-lookup"><span data-stu-id="23256-132">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>

<span data-ttu-id="23256-133">下列指令碼可讓您指定預設訂用帳戶以外的範圍，然後如果發生錯誤，就重試角色指派︰</span><span class="sxs-lookup"><span data-stu-id="23256-133">The following script enables you to specify a scope other than the default subscription, and retries the role assignment if an error occurs:</span></span>

```powershell
Param (

 # Use to set scope to resource group. If no value is provided, scope is set to subscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use to set subscription. If no value is provided, default subscription is used. 
 [Parameter(Mandatory=$false)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName,

 [Parameter(Mandatory=$true)]
 [String] $Password
)

 Login-AzureRmAccount
 Import-Module AzureRM.Resources

 if ($SubscriptionId -eq "") 
 {
    $SubscriptionId = (Get-AzureRmContext).Subscription.Id
 }
 else
 {
    Set-AzureRmContext -SubscriptionId $SubscriptionId
 }

 if ($ResourceGroup -eq "")
 {
    $Scope = "/subscriptions/" + $SubscriptionId
 }
 else
 {
    $Scope = (Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop).ResourceId
 }

 
 # Create Service Principal for the AD app
 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

<span data-ttu-id="23256-134">有關指令碼的一些注意事項︰</span><span class="sxs-lookup"><span data-stu-id="23256-134">A few items to note about the script:</span></span>

* <span data-ttu-id="23256-135">若要授與身分識別存取預設訂用帳戶，您不需要提供 ResourceGroup 或 SubscriptionId 參數。</span><span class="sxs-lookup"><span data-stu-id="23256-135">To grant the identity access to the default subscription, you do not need to provide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="23256-136">只有當您想要將角色指派的範圍限制為資源群組時，才指定 ResourceGroup 參數。</span><span class="sxs-lookup"><span data-stu-id="23256-136">Specify the ResourceGroup parameter only when you want to limit the scope of the role assignment to a resource group.</span></span>
*  <span data-ttu-id="23256-137">在此範例中，您將服務主體新增至參與者角色。</span><span class="sxs-lookup"><span data-stu-id="23256-137">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="23256-138">若為其他角色，請參閱 [RBAC︰內建角色](../active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="23256-138">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="23256-139">指令碼會睡 15 秒，留一些時間讓新的服務主體在整個 Azure Active Directory 中傳播。</span><span class="sxs-lookup"><span data-stu-id="23256-139">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="23256-140">如果您的指令碼等得不夠久，您會看到錯誤指出：「PrincipalNotFound︰主體 {id} 不存在於目錄中」。</span><span class="sxs-lookup"><span data-stu-id="23256-140">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="23256-141">如果您要授與服務主體存取更多訂用帳戶或資源群組，請以不同範圍再次執行 `New-AzureRMRoleAssignment` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="23256-141">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>


### <a name="provide-credentials-through-powershell"></a><span data-ttu-id="23256-142">透過 PowerShell 提供認證</span><span class="sxs-lookup"><span data-stu-id="23256-142">Provide credentials through PowerShell</span></span>
<span data-ttu-id="23256-143">現在，您需要以應用程式的形式登入以執行作業。</span><span class="sxs-lookup"><span data-stu-id="23256-143">Now, you need to log in as the application to perform operations.</span></span> <span data-ttu-id="23256-144">針對使用者名稱，使用您針對應用程式建立的 `ApplicationId`。</span><span class="sxs-lookup"><span data-stu-id="23256-144">For the user name, use the `ApplicationId` that you created for the application.</span></span> <span data-ttu-id="23256-145">針對密碼，使用您在建立帳戶時所指定的密碼。</span><span class="sxs-lookup"><span data-stu-id="23256-145">For the password, use the one you specified when creating the account.</span></span> 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

<span data-ttu-id="23256-146">租用戶識別碼不區分大小寫，因此您可以直接將它內嵌在指令碼中。</span><span class="sxs-lookup"><span data-stu-id="23256-146">The tenant ID is not sensitive, so you can embed it directly in your script.</span></span> <span data-ttu-id="23256-147">如果您要擷取租用戶識別碼，請使用︰</span><span class="sxs-lookup"><span data-stu-id="23256-147">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a><span data-ttu-id="23256-148">使用自我簽署憑證建立服務主體</span><span class="sxs-lookup"><span data-stu-id="23256-148">Create service principal with self-signed certificate</span></span>

<span data-ttu-id="23256-149">若要使用自我簽署的憑證和訂用帳戶的參與者角色來建立服務主體，請使用︰</span><span class="sxs-lookup"><span data-stu-id="23256-149">To create a service principal with a self-signed certificate and the Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="23256-150">範例會睡 20 秒，留一些時間讓新的服務主體在整個 Azure Active Directory 中傳播。</span><span class="sxs-lookup"><span data-stu-id="23256-150">The example sleeps for 20 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="23256-151">如果您的指令碼等得不夠久，您會看到錯誤指出：「PrincipalNotFound︰主體 {id} 不存在於目錄中」。</span><span class="sxs-lookup"><span data-stu-id="23256-151">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>

<span data-ttu-id="23256-152">下列指令碼可讓您指定預設訂用帳戶以外的範圍，然後如果發生錯誤，就重試角色指派。</span><span class="sxs-lookup"><span data-stu-id="23256-152">The following script enables you to specify a scope other than the default subscription, and retries the role assignment if an error occurs.</span></span> <span data-ttu-id="23256-153">您必須擁有 Windows 10 或 Windows Server 2016 的 Azure PowerShell 2.0。</span><span class="sxs-lookup"><span data-stu-id="23256-153">You must have Azure PowerShell 2.0 on Windows 10 or Windows Server 2016.</span></span>

```powershell
Param (

 # Use to set scope to resource group. If no value is provided, scope is set to subscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use to set subscription. If no value is provided, default subscription is used. 
 [Parameter(Mandatory=$false)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources

 if ($SubscriptionId -eq "") 
 {
    $SubscriptionId = (Get-AzureRmContext).Subscription.Id
 }
 else
 {
    Set-AzureRmContext -SubscriptionId $SubscriptionId
 }

 if ($ResourceGroup -eq "")
 {
    $Scope = "/subscriptions/" + $SubscriptionId
 }
 else
 {
    $Scope = (Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop).ResourceId
 }

 $cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
 $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

<span data-ttu-id="23256-154">有關指令碼的一些注意事項︰</span><span class="sxs-lookup"><span data-stu-id="23256-154">A few items to note about the script:</span></span>

* <span data-ttu-id="23256-155">若要授與身分識別存取預設訂用帳戶，您不需要提供 ResourceGroup 或 SubscriptionId 參數。</span><span class="sxs-lookup"><span data-stu-id="23256-155">To grant the identity access to the default subscription, you do not need to provide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="23256-156">只有當您想要將角色指派的範圍限制為資源群組時，才指定 ResourceGroup 參數。</span><span class="sxs-lookup"><span data-stu-id="23256-156">Specify the ResourceGroup parameter only when you want to limit the scope of the role assignment to a resource group.</span></span>
* <span data-ttu-id="23256-157">在此範例中，您將服務主體新增至參與者角色。</span><span class="sxs-lookup"><span data-stu-id="23256-157">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="23256-158">若為其他角色，請參閱 [RBAC︰內建角色](../active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="23256-158">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="23256-159">指令碼會睡 15 秒，留一些時間讓新的服務主體在整個 Azure Active Directory 中傳播。</span><span class="sxs-lookup"><span data-stu-id="23256-159">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="23256-160">如果您的指令碼等得不夠久，您會看到錯誤指出：「PrincipalNotFound︰主體 {id} 不存在於目錄中」。</span><span class="sxs-lookup"><span data-stu-id="23256-160">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="23256-161">如果您要授與服務主體存取更多訂用帳戶或資源群組，請以不同範圍再次執行 `New-AzureRMRoleAssignment` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="23256-161">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

<span data-ttu-id="23256-162">如果您 **不是執行 Windows 10 或 Windows Server 2016 Technical Preview**，則必須從 Microsoft 指令碼中心下載 [自我簽署憑證產生器](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) 。</span><span class="sxs-lookup"><span data-stu-id="23256-162">If you **do not have Windows 10 or Windows Server 2016 Technical Preview**, you need to download the [Self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from Microsoft Script Center.</span></span> <span data-ttu-id="23256-163">將其內容解壓縮，並匯入您需要的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="23256-163">Extract its contents and import the cmdlet you need.</span></span>

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
<span data-ttu-id="23256-164">在指令碼中，取代下列兩行來產生憑證。</span><span class="sxs-lookup"><span data-stu-id="23256-164">In the script, substitute the following two lines to generate the certificate.</span></span>
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="23256-165">透過自動化的 PowerShell 指令碼提供憑證</span><span class="sxs-lookup"><span data-stu-id="23256-165">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="23256-166">每當您以服務主體的形式登入時，都需要提供 AD 應用程式目錄的租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="23256-166">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="23256-167">租用戶是 Azure Active Directory 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="23256-167">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="23256-168">如果您只有一個訂用帳戶，您可以使用：</span><span class="sxs-lookup"><span data-stu-id="23256-168">If you only have one subscription, you can use:</span></span>

```powershell
Param (
 
 [Parameter(Mandatory=$true)]
 [String] $CertSubject,
 
 [Parameter(Mandatory=$true)]
 [String] $ApplicationId,

 [Parameter(Mandatory=$true)]
 [String] $TenantId
 )

 $Thumbprint = (Get-ChildItem cert:\CurrentUser\My\ | Where-Object {$_.Subject -match $CertSubject }).Thumbprint
 Login-AzureRmAccount -ServicePrincipal -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId
```

<span data-ttu-id="23256-169">應用程式識別碼和租用戶識別碼不區分大小寫，因此您可以直接將它們內嵌在您的指令碼中。</span><span class="sxs-lookup"><span data-stu-id="23256-169">The application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="23256-170">如果您要擷取租用戶識別碼，請使用︰</span><span class="sxs-lookup"><span data-stu-id="23256-170">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="23256-171">如果您要擷取應用程式識別碼，請使用︰</span><span class="sxs-lookup"><span data-stu-id="23256-171">If you need to retrieve the application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a><span data-ttu-id="23256-172">使用憑證授權中心的憑證來建立服務主體</span><span class="sxs-lookup"><span data-stu-id="23256-172">Create service principal with certificate from Certificate Authority</span></span>
<span data-ttu-id="23256-173">若要使用憑證授權中心所發行的憑證來建立服務主體，請使用下列指令碼︰</span><span class="sxs-lookup"><span data-stu-id="23256-173">To use a certificate issued from a Certificate Authority to create service principal, use the following script:</span></span>

```powershell
Param (
 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName,

 [Parameter(Mandatory=$true)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $CertPath,

 [Parameter(Mandatory=$true)]
 [String] $CertPlainPassword
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources
 Set-AzureRmContext -SubscriptionId $SubscriptionId

 $KeyId = (New-Guid).Guid
 $CertPassword = ConvertTo-SecureString $CertPlainPassword -AsPlainText -Force

 $PFXCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($CertPath, $CertPassword)
 $KeyValue = [System.Convert]::ToBase64String($PFXCert.GetRawCertData())

 $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
 $KeyCredential.StartDate = $PFXCert.NotBefore
 $KeyCredential.EndDate= $PFXCert.NotAfter
 $KeyCredential.KeyId = $KeyId
 $KeyCredential.CertValue = $KeyValue

 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -KeyCredentials $keyCredential
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
 
 $NewRole
```

<span data-ttu-id="23256-174">有關指令碼的一些注意事項︰</span><span class="sxs-lookup"><span data-stu-id="23256-174">A few items to note about the script:</span></span>

* <span data-ttu-id="23256-175">存取限域為訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="23256-175">Access is scoped to the subscription.</span></span>
* <span data-ttu-id="23256-176">在此範例中，您將服務主體新增至參與者角色。</span><span class="sxs-lookup"><span data-stu-id="23256-176">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="23256-177">若為其他角色，請參閱 [RBAC︰內建角色](../active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="23256-177">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="23256-178">指令碼會睡 15 秒，留一些時間讓新的服務主體在整個 Azure Active Directory 中傳播。</span><span class="sxs-lookup"><span data-stu-id="23256-178">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="23256-179">如果您的指令碼等得不夠久，您會看到錯誤指出：「PrincipalNotFound︰主體 {id} 不存在於目錄中」。</span><span class="sxs-lookup"><span data-stu-id="23256-179">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="23256-180">如果您要授與服務主體存取更多訂用帳戶或資源群組，請以不同範圍再次執行 `New-AzureRMRoleAssignment` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="23256-180">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="23256-181">透過自動化的 PowerShell 指令碼提供憑證</span><span class="sxs-lookup"><span data-stu-id="23256-181">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="23256-182">每當您以服務主體的形式登入時，都需要提供 AD 應用程式目錄的租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="23256-182">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="23256-183">租用戶是 Azure Active Directory 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="23256-183">A tenant is an instance of Azure Active Directory.</span></span>

```powershell
Param (
 
 [Parameter(Mandatory=$true)]
 [String] $CertPath,

 [Parameter(Mandatory=$true)]
 [String] $CertPlainPassword,
 
 [Parameter(Mandatory=$true)]
 [String] $ApplicationId,

 [Parameter(Mandatory=$true)]
 [String] $TenantId
 )

 $CertPassword = ConvertTo-SecureString $CertPlainPassword -AsPlainText -Force
 $PFXCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($CertPath, $CertPassword)
 $Thumbprint = $PFXCert.Thumbprint

 Login-AzureRmAccount -ServicePrincipal -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId
```

<span data-ttu-id="23256-184">應用程式識別碼和租用戶識別碼不區分大小寫，因此您可以直接將它們內嵌在您的指令碼中。</span><span class="sxs-lookup"><span data-stu-id="23256-184">The application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="23256-185">如果您要擷取租用戶識別碼，請使用︰</span><span class="sxs-lookup"><span data-stu-id="23256-185">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="23256-186">如果您要擷取應用程式識別碼，請使用︰</span><span class="sxs-lookup"><span data-stu-id="23256-186">If you need to retrieve the application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a><span data-ttu-id="23256-187">管理認證</span><span class="sxs-lookup"><span data-stu-id="23256-187">Change credentials</span></span>

<span data-ttu-id="23256-188">若要變更 AD App 的認證，不管是因為安全性危害或認證過期，請使用 [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) 和 [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="23256-188">To change the credentials for an AD app, either because of a security compromise or a credential expiration, use the [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) and [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.</span></span>

<span data-ttu-id="23256-189">若要移除應用程式的所有認證，使用︰</span><span class="sxs-lookup"><span data-stu-id="23256-189">To remove all the credentials for an application, use:</span></span>

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

<span data-ttu-id="23256-190">若要新增密碼，使用：</span><span class="sxs-lookup"><span data-stu-id="23256-190">To add a password, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

<span data-ttu-id="23256-191">若要新增憑證值，請建立自我簽署的憑證，如本主題中所述。</span><span class="sxs-lookup"><span data-stu-id="23256-191">To add a certificate value, create a self-signed certificate as shown in this topic.</span></span> <span data-ttu-id="23256-192">然後，使用︰</span><span class="sxs-lookup"><span data-stu-id="23256-192">Then, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-to-simplify-log-in"></a><span data-ttu-id="23256-193">儲存存取權杖以簡化登入</span><span class="sxs-lookup"><span data-stu-id="23256-193">Save access token to simplify log in</span></span>
<span data-ttu-id="23256-194">若要避免每次需要登入時都要提供服務主體認證，您可以儲存存取權杖。</span><span class="sxs-lookup"><span data-stu-id="23256-194">To avoid providing the service principal credentials every time it needs to log in, you can save the access token.</span></span>

<span data-ttu-id="23256-195">若要在稍後的工作階段中使用目前的存取權杖，請儲存設定檔。</span><span class="sxs-lookup"><span data-stu-id="23256-195">To use the current access token in a later session, save the profile.</span></span>
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
<span data-ttu-id="23256-196">開啟設定檔，並檢查其內容。</span><span class="sxs-lookup"><span data-stu-id="23256-196">Open the profile and examine its contents.</span></span> <span data-ttu-id="23256-197">請注意其中包含存取權杖。</span><span class="sxs-lookup"><span data-stu-id="23256-197">Notice that it contains an access token.</span></span> <span data-ttu-id="23256-198">請不要以手動方式再次登入，只要載入設定檔即可。</span><span class="sxs-lookup"><span data-stu-id="23256-198">Instead of manually logging in again, simply load the profile.</span></span>
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> <span data-ttu-id="23256-199">存取權杖會過期，因此，只要權杖有效，就只使用可使用的已儲存設定檔。</span><span class="sxs-lookup"><span data-stu-id="23256-199">The access token expires, so using a saved profile only works for as long as the token is valid.</span></span>
>  

<span data-ttu-id="23256-200">或者，您可以從 PowerShell 叫用 REST 作業來登入。</span><span class="sxs-lookup"><span data-stu-id="23256-200">Alternatively, you can invoke REST operations from PowerShell to log in.</span></span> <span data-ttu-id="23256-201">從驗證回應，您可以擷取存取權杖以用於其他作業。</span><span class="sxs-lookup"><span data-stu-id="23256-201">From the authentication response, you can retrieve the access token for use with other operations.</span></span> <span data-ttu-id="23256-202">如需叫用 REST 作業擷取存取權杖的範例，請參閱[產生存取權杖](resource-manager-rest-api.md#generating-an-access-token)。</span><span class="sxs-lookup"><span data-stu-id="23256-202">For an example of retrieving the access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="debug"></a><span data-ttu-id="23256-203">偵錯</span><span class="sxs-lookup"><span data-stu-id="23256-203">Debug</span></span>

<span data-ttu-id="23256-204">建立服務主體時，您可能會遇到下列錯誤︰</span><span class="sxs-lookup"><span data-stu-id="23256-204">You may encounter the following errors when creating a service principal:</span></span>

* <span data-ttu-id="23256-205">**Authentication_Unauthorized」**或**「在內容中找不到訂用帳戶。」**</span><span class="sxs-lookup"><span data-stu-id="23256-205">**"Authentication_Unauthorized"** or **"No subscription found in the context."**</span></span> <span data-ttu-id="23256-206">- 當您的帳戶在 Azure Active Directory 上未具備註冊應用程式的[必要權限](#required-permissions)時，您就會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="23256-206">- You see this error when your account does not have the [required permissions](#required-permissions) on the Azure Active Directory to register an app.</span></span> <span data-ttu-id="23256-207">通常，只有 Azure Active Directory 中的管理使用者可以註冊應用程式，且您的帳戶不是系統管理員時，就會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="23256-207">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin.</span></span> <span data-ttu-id="23256-208">要求系統管理員將您指派給系統管理員角色，或是讓使用者註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="23256-208">Ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

* <span data-ttu-id="23256-209">您的帳戶**「沒有在範圍 '/subscriptions/{guid}' 中執行 'Microsoft.Authorization/roleAssignments/write' 動作的權限。」** - 當您的帳戶沒有足夠權限可將角色指派給身分識別時，您就會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="23256-209">Your account **"does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions to assign a role to an identity.</span></span> <span data-ttu-id="23256-210">要求訂用帳戶管理員將您新增至「使用者存取系統管理員」角色。</span><span class="sxs-lookup"><span data-stu-id="23256-210">Ask your subscription administrator to add you to User Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="23256-211">範例應用程式</span><span class="sxs-lookup"><span data-stu-id="23256-211">Sample applications</span></span>
<span data-ttu-id="23256-212">如需透過不同平台以應用程式身分登入的資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="23256-212">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="23256-213">.NET</span><span class="sxs-lookup"><span data-stu-id="23256-213">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="23256-214">Java</span><span class="sxs-lookup"><span data-stu-id="23256-214">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="23256-215">Node.js</span><span class="sxs-lookup"><span data-stu-id="23256-215">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="23256-216">Python</span><span class="sxs-lookup"><span data-stu-id="23256-216">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="23256-217">Ruby</span><span class="sxs-lookup"><span data-stu-id="23256-217">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="23256-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="23256-218">Next steps</span></span>
* <span data-ttu-id="23256-219">如需有關將應用程式整合至 Azure 來管理資源的詳細步驟，請參閱 [利用 Azure Resource Manager API 進行授權的開發人員指南](resource-manager-api-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="23256-219">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="23256-220">如需應用程式和服務主體的詳細說明，請參閱[應用程式物件和服務主體物件](../active-directory/active-directory-application-objects.md)。</span><span class="sxs-lookup"><span data-stu-id="23256-220">For a more detailed explanation of applications and service principals, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span> 
* <span data-ttu-id="23256-221">如需 Azure Active Directory 驗證的詳細資訊，請參閱 [Azure AD 的驗證案例](../active-directory/active-directory-authentication-scenarios.md)。</span><span class="sxs-lookup"><span data-stu-id="23256-221">For more information about Azure Active Directory authentication, see [Authentication Scenarios for Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span></span>
* <span data-ttu-id="23256-222">如需可授與或拒絕使用者的可用動作清單，請參閱 [Azure Resource Manager 資源提供者作業](../active-directory/role-based-access-control-resource-provider-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="23256-222">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>

