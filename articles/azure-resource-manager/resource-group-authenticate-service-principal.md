---
title: "使用 PowerShell 的 Azure 應用程式的 aaaCreate 識別 |Microsoft 文件"
description: "描述如何 toouse Azure PowerShell toocreate Azure Active Directory 應用程式和服務主體授與它存取 tooresources 透過以角色為基礎的存取控制。 它會顯示如何使用密碼或憑證 tooauthenticate 應用程式。"
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
ms.openlocfilehash: c534360799b590054a051e4426e5e27dccb559b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toocreate-a-service-principal-tooaccess-resources"></a><span data-ttu-id="939f9-104">使用 Azure PowerShell toocreate 服務主體 tooaccess 資源</span><span class="sxs-lookup"><span data-stu-id="939f9-104">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>

<span data-ttu-id="939f9-105">當您擁有的應用程式或需要 tooaccess 資源的指令碼時，您可以設定 hello 應用程式的身分識別，並驗證它自己的認證與 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="939f9-105">When you have an app or script that needs tooaccess resources, you can set up an identity for hello app and authenticate hello app with its own credentials.</span></span> <span data-ttu-id="939f9-106">此身分識別就是所謂的服務主體。</span><span class="sxs-lookup"><span data-stu-id="939f9-106">This identity is known as a service principal.</span></span> <span data-ttu-id="939f9-107">這種方法可讓您︰</span><span class="sxs-lookup"><span data-stu-id="939f9-107">This approach enables you to:</span></span>

* <span data-ttu-id="939f9-108">指派權限 toohello 不同於您自己的權限的應用程式識別。</span><span class="sxs-lookup"><span data-stu-id="939f9-108">Assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="939f9-109">一般而言，這些權限會限制的 tooexactly 哪些 hello 應用程式需要 toodo。</span><span class="sxs-lookup"><span data-stu-id="939f9-109">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="939f9-110">使用憑證在執行無人看管的指令碼時進行驗證。</span><span class="sxs-lookup"><span data-stu-id="939f9-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="939f9-111">本主題說明如何 toouse [Azure PowerShell](/powershell/azure/overview) tooset 好您的應用程式 toorun 在它自己的認證和身分識別的所需的一切。</span><span class="sxs-lookup"><span data-stu-id="939f9-111">This topic shows you how toouse [Azure PowerShell](/powershell/azure/overview) tooset up everything you need for an application toorun under its own credentials and identity.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="939f9-112">所需的權限</span><span class="sxs-lookup"><span data-stu-id="939f9-112">Required permissions</span></span>
<span data-ttu-id="939f9-113">toocomplete 本主題中，您必須在您的 Azure Active Directory 和 Azure 訂用帳戶擁有足夠的權限。</span><span class="sxs-lookup"><span data-stu-id="939f9-113">toocomplete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="939f9-114">具體來說，您必須是能夠 toocreate hello Azure Active Directory 中的應用程式，並且將 hello 服務主體 tooa 角色指派。</span><span class="sxs-lookup"><span data-stu-id="939f9-114">Specifically, you must be able toocreate an app in hello Azure Active Directory, and assign hello service principal tooa role.</span></span> 

<span data-ttu-id="939f9-115">hello 最簡單方式 toocheck 您的帳戶是否有足夠的權限是透過 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="939f9-115">hello easiest way toocheck whether your account has adequate permissions is through hello portal.</span></span> <span data-ttu-id="939f9-116">請參閱[檢查必要的權限](resource-group-create-service-principal-portal.md#required-permissions)。</span><span class="sxs-lookup"><span data-stu-id="939f9-116">See [Check required permission](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="939f9-117">現在，請繼續進行 tooa > 一節，以驗證：</span><span class="sxs-lookup"><span data-stu-id="939f9-117">Now, proceed tooa section for authenticating with:</span></span>

* [<span data-ttu-id="939f9-118">password</span><span class="sxs-lookup"><span data-stu-id="939f9-118">password</span></span>](#create-service-principal-with-password)
* [<span data-ttu-id="939f9-119">自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="939f9-119">self-signed certificate</span></span>](#create-service-principal-with-self-signed-certificate)
* [<span data-ttu-id="939f9-120">來自憑證授權單位的憑證</span><span class="sxs-lookup"><span data-stu-id="939f9-120">certificate from Certificate Authority</span></span>](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a><span data-ttu-id="939f9-121">PowerShell 命令</span><span class="sxs-lookup"><span data-stu-id="939f9-121">PowerShell commands</span></span>

<span data-ttu-id="939f9-122">tooset 註冊服務主體，您使用：</span><span class="sxs-lookup"><span data-stu-id="939f9-122">tooset up a service principal, you use:</span></span>

| <span data-ttu-id="939f9-123">命令</span><span class="sxs-lookup"><span data-stu-id="939f9-123">Command</span></span> | <span data-ttu-id="939f9-124">說明</span><span class="sxs-lookup"><span data-stu-id="939f9-124">Description</span></span> |
| ------- | ----------- | 
| [<span data-ttu-id="939f9-125">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="939f9-125">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="939f9-126">建立 Azure Active Directory 服務主體</span><span class="sxs-lookup"><span data-stu-id="939f9-126">Creates an Azure Active Directory service principal</span></span> |
| [<span data-ttu-id="939f9-127">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="939f9-127">New-AzureRmRoleAssignment</span></span>](/powershell/module/azurerm.resources/new-azurermroleassignment) | <span data-ttu-id="939f9-128">指派 hello 指定 RBAC 角色 toohello 指定的主體，在 hello 指定的範圍。</span><span class="sxs-lookup"><span data-stu-id="939f9-128">Assigns hello specified RBAC role toohello specified principal, at hello specified scope.</span></span> |


## <a name="create-service-principal-with-password"></a><span data-ttu-id="939f9-129">使用密碼建立服務主體</span><span class="sxs-lookup"><span data-stu-id="939f9-129">Create service principal with password</span></span>

<span data-ttu-id="939f9-130">toocreate 服務主體與 hello 參與者角色，您的訂用帳戶，使用：</span><span class="sxs-lookup"><span data-stu-id="939f9-130">toocreate a service principal with hello Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="939f9-131">hello 範例進入睡眠狀態 20 秒 tooallow hello 新服務主體 toopropagate 整個 Azure Active Directory 一些時間。</span><span class="sxs-lookup"><span data-stu-id="939f9-131">hello example sleeps for 20 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="939f9-132">如果您的指令碼不會等待足夠的時間，您看到錯誤指出: 「 PrincipalNotFound: hello 目錄中沒有主體 {id}。 」</span><span class="sxs-lookup"><span data-stu-id="939f9-132">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>

<span data-ttu-id="939f9-133">hello 下列指令碼可讓您 toospecify hello 預設訂用帳戶以外的範圍和重試 hello 角色指派，如果發生錯誤：</span><span class="sxs-lookup"><span data-stu-id="939f9-133">hello following script enables you toospecify a scope other than hello default subscription, and retries hello role assignment if an error occurs:</span></span>

```powershell
Param (

 # Use tooset scope tooresource group. If no value is provided, scope is set toosubscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use tooset subscription. If no value is provided, default subscription is used. 
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

 
 # Create Service Principal for hello AD app
 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

<span data-ttu-id="939f9-134">Hello 指令碼相關的幾個項目 toonote:</span><span class="sxs-lookup"><span data-stu-id="939f9-134">A few items toonote about hello script:</span></span>

* <span data-ttu-id="939f9-135">toogrant hello 身分識別存取 toohello 預設訂用帳戶，您不需要 tooprovide ResourceGroup 或 SubscriptionId 參數。</span><span class="sxs-lookup"><span data-stu-id="939f9-135">toogrant hello identity access toohello default subscription, you do not need tooprovide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="939f9-136">只有當您希望 toolimit hello 範圍 hello 角色指派 tooa 資源群組時，請指定 hello ResourceGroup 參數。</span><span class="sxs-lookup"><span data-stu-id="939f9-136">Specify hello ResourceGroup parameter only when you want toolimit hello scope of hello role assignment tooa resource group.</span></span>
*  <span data-ttu-id="939f9-137">在此範例中，您可以將 hello 服務主體 toohello 參與者角色。</span><span class="sxs-lookup"><span data-stu-id="939f9-137">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="939f9-138">若為其他角色，請參閱 [RBAC︰內建角色](../active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="939f9-138">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="939f9-139">hello 指令碼睡眠 15 秒 tooallow hello 新服務主體 toopropagate 整個 Azure Active Directory 一些時間。</span><span class="sxs-lookup"><span data-stu-id="939f9-139">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="939f9-140">如果您的指令碼不會等待足夠的時間，您看到錯誤指出: 「 PrincipalNotFound: hello 目錄中沒有主體 {id}。 」</span><span class="sxs-lookup"><span data-stu-id="939f9-140">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="939f9-141">如果您需要 toogrant hello 服務主體存取 toomore 訂閱或資源群組，執行 hello`New-AzureRMRoleAssignment`指令程式搭配不同範圍的一次。</span><span class="sxs-lookup"><span data-stu-id="939f9-141">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>


### <a name="provide-credentials-through-powershell"></a><span data-ttu-id="939f9-142">透過 PowerShell 提供認證</span><span class="sxs-lookup"><span data-stu-id="939f9-142">Provide credentials through PowerShell</span></span>
<span data-ttu-id="939f9-143">現在，您必須在 toolog 為 hello tooperform 應用程式的作業。</span><span class="sxs-lookup"><span data-stu-id="939f9-143">Now, you need toolog in as hello application tooperform operations.</span></span> <span data-ttu-id="939f9-144">Hello 使用者名稱，使用 hello `ApplicationId` hello 應用程式所建立。</span><span class="sxs-lookup"><span data-stu-id="939f9-144">For hello user name, use hello `ApplicationId` that you created for hello application.</span></span> <span data-ttu-id="939f9-145">Hello 密碼使用 hello 建立 hello 帳戶時，您指定的其中一個。</span><span class="sxs-lookup"><span data-stu-id="939f9-145">For hello password, use hello one you specified when creating hello account.</span></span> 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

<span data-ttu-id="939f9-146">hello 租用戶識別碼不區分大小寫，因此您可以將它內嵌直接在您的指令碼中。</span><span class="sxs-lookup"><span data-stu-id="939f9-146">hello tenant ID is not sensitive, so you can embed it directly in your script.</span></span> <span data-ttu-id="939f9-147">如果您需要 tooretrieve hello 租用戶識別碼，請使用：</span><span class="sxs-lookup"><span data-stu-id="939f9-147">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a><span data-ttu-id="939f9-148">使用自我簽署憑證建立服務主體</span><span class="sxs-lookup"><span data-stu-id="939f9-148">Create service principal with self-signed certificate</span></span>

<span data-ttu-id="939f9-149">toocreate 使用自我簽署的憑證和訂用帳戶，hello 參與者角色的服務主體：</span><span class="sxs-lookup"><span data-stu-id="939f9-149">toocreate a service principal with a self-signed certificate and hello Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="939f9-150">hello 範例進入睡眠狀態 20 秒 tooallow hello 新服務主體 toopropagate 整個 Azure Active Directory 一些時間。</span><span class="sxs-lookup"><span data-stu-id="939f9-150">hello example sleeps for 20 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="939f9-151">如果您的指令碼不會等待足夠的時間，您看到錯誤指出: 「 PrincipalNotFound: hello 目錄中沒有主體 {id}。 」</span><span class="sxs-lookup"><span data-stu-id="939f9-151">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>

<span data-ttu-id="939f9-152">hello 下列指令碼可讓您 toospecify hello 預設訂用帳戶以外的範圍和重試 hello 角色指派，如果發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="939f9-152">hello following script enables you toospecify a scope other than hello default subscription, and retries hello role assignment if an error occurs.</span></span> <span data-ttu-id="939f9-153">您必須擁有 Windows 10 或 Windows Server 2016 的 Azure PowerShell 2.0。</span><span class="sxs-lookup"><span data-stu-id="939f9-153">You must have Azure PowerShell 2.0 on Windows 10 or Windows Server 2016.</span></span>

```powershell
Param (

 # Use tooset scope tooresource group. If no value is provided, scope is set toosubscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use tooset subscription. If no value is provided, default subscription is used. 
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
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

<span data-ttu-id="939f9-154">Hello 指令碼相關的幾個項目 toonote:</span><span class="sxs-lookup"><span data-stu-id="939f9-154">A few items toonote about hello script:</span></span>

* <span data-ttu-id="939f9-155">toogrant hello 身分識別存取 toohello 預設訂用帳戶，您不需要 tooprovide ResourceGroup 或 SubscriptionId 參數。</span><span class="sxs-lookup"><span data-stu-id="939f9-155">toogrant hello identity access toohello default subscription, you do not need tooprovide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="939f9-156">只有當您希望 toolimit hello 範圍 hello 角色指派 tooa 資源群組時，請指定 hello ResourceGroup 參數。</span><span class="sxs-lookup"><span data-stu-id="939f9-156">Specify hello ResourceGroup parameter only when you want toolimit hello scope of hello role assignment tooa resource group.</span></span>
* <span data-ttu-id="939f9-157">在此範例中，您可以將 hello 服務主體 toohello 參與者角色。</span><span class="sxs-lookup"><span data-stu-id="939f9-157">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="939f9-158">若為其他角色，請參閱 [RBAC︰內建角色](../active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="939f9-158">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="939f9-159">hello 指令碼睡眠 15 秒 tooallow hello 新服務主體 toopropagate 整個 Azure Active Directory 一些時間。</span><span class="sxs-lookup"><span data-stu-id="939f9-159">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="939f9-160">如果您的指令碼不會等待足夠的時間，您看到錯誤指出: 「 PrincipalNotFound: hello 目錄中沒有主體 {id}。 」</span><span class="sxs-lookup"><span data-stu-id="939f9-160">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="939f9-161">如果您需要 toogrant hello 服務主體存取 toomore 訂閱或資源群組，執行 hello`New-AzureRMRoleAssignment`指令程式搭配不同範圍的一次。</span><span class="sxs-lookup"><span data-stu-id="939f9-161">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

<span data-ttu-id="939f9-162">如果您**不具有 Windows 10 或 Windows Server 2016 Technical Preview**，您需要 toodownload hello[自我簽署的憑證的產生器](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/)從 Microsoft 指令碼中心。</span><span class="sxs-lookup"><span data-stu-id="939f9-162">If you **do not have Windows 10 or Windows Server 2016 Technical Preview**, you need toodownload hello [Self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from Microsoft Script Center.</span></span> <span data-ttu-id="939f9-163">將其內容解壓縮，並匯入您所需要的 hello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="939f9-163">Extract its contents and import hello cmdlet you need.</span></span>

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
<span data-ttu-id="939f9-164">在 hello 指令碼，取代下列兩行 toogenerate hello 憑證 hello。</span><span class="sxs-lookup"><span data-stu-id="939f9-164">In hello script, substitute hello following two lines toogenerate hello certificate.</span></span>
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="939f9-165">透過自動化的 PowerShell 指令碼提供憑證</span><span class="sxs-lookup"><span data-stu-id="939f9-165">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="939f9-166">每當您登入做為服務主體時，您需要 tooprovide hello 租用戶識別碼 hello 目錄的 AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="939f9-166">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="939f9-167">租用戶是 Azure Active Directory 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="939f9-167">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="939f9-168">如果您只有一個訂用帳戶，您可以使用：</span><span class="sxs-lookup"><span data-stu-id="939f9-168">If you only have one subscription, you can use:</span></span>

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

<span data-ttu-id="939f9-169">hello 應用程式識別碼和租用戶識別碼不區分大小寫，因此您可以將其內嵌直接在您的指令碼中。</span><span class="sxs-lookup"><span data-stu-id="939f9-169">hello application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="939f9-170">如果您需要 tooretrieve hello 租用戶識別碼，請使用：</span><span class="sxs-lookup"><span data-stu-id="939f9-170">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="939f9-171">如果您需要 tooretrieve hello 應用程式識別碼，請使用：</span><span class="sxs-lookup"><span data-stu-id="939f9-171">If you need tooretrieve hello application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a><span data-ttu-id="939f9-172">使用憑證授權中心的憑證來建立服務主體</span><span class="sxs-lookup"><span data-stu-id="939f9-172">Create service principal with certificate from Certificate Authority</span></span>
<span data-ttu-id="939f9-173">toouse 為憑證授權單位 toocreate 服務主體時，使用下列指令碼的 hello 所發出的憑證：</span><span class="sxs-lookup"><span data-stu-id="939f9-173">toouse a certificate issued from a Certificate Authority toocreate service principal, use hello following script:</span></span>

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
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
 
 $NewRole
```

<span data-ttu-id="939f9-174">Hello 指令碼相關的幾個項目 toonote:</span><span class="sxs-lookup"><span data-stu-id="939f9-174">A few items toonote about hello script:</span></span>

* <span data-ttu-id="939f9-175">已設定領域的 toohello 訂用帳戶存取。</span><span class="sxs-lookup"><span data-stu-id="939f9-175">Access is scoped toohello subscription.</span></span>
* <span data-ttu-id="939f9-176">在此範例中，您可以將 hello 服務主體 toohello 參與者角色。</span><span class="sxs-lookup"><span data-stu-id="939f9-176">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="939f9-177">若為其他角色，請參閱 [RBAC︰內建角色](../active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="939f9-177">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="939f9-178">hello 指令碼睡眠 15 秒 tooallow hello 新服務主體 toopropagate 整個 Azure Active Directory 一些時間。</span><span class="sxs-lookup"><span data-stu-id="939f9-178">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="939f9-179">如果您的指令碼不會等待足夠的時間，您看到錯誤指出: 「 PrincipalNotFound: hello 目錄中沒有主體 {id}。 」</span><span class="sxs-lookup"><span data-stu-id="939f9-179">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="939f9-180">如果您需要 toogrant hello 服務主體存取 toomore 訂閱或資源群組，執行 hello`New-AzureRMRoleAssignment`指令程式搭配不同範圍的一次。</span><span class="sxs-lookup"><span data-stu-id="939f9-180">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="939f9-181">透過自動化的 PowerShell 指令碼提供憑證</span><span class="sxs-lookup"><span data-stu-id="939f9-181">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="939f9-182">每當您登入做為服務主體時，您需要 tooprovide hello 租用戶識別碼 hello 目錄的 AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="939f9-182">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="939f9-183">租用戶是 Azure Active Directory 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="939f9-183">A tenant is an instance of Azure Active Directory.</span></span>

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

<span data-ttu-id="939f9-184">hello 應用程式識別碼和租用戶識別碼不區分大小寫，因此您可以將其內嵌直接在您的指令碼中。</span><span class="sxs-lookup"><span data-stu-id="939f9-184">hello application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="939f9-185">如果您需要 tooretrieve hello 租用戶識別碼，請使用：</span><span class="sxs-lookup"><span data-stu-id="939f9-185">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="939f9-186">如果您需要 tooretrieve hello 應用程式識別碼，請使用：</span><span class="sxs-lookup"><span data-stu-id="939f9-186">If you need tooretrieve hello application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a><span data-ttu-id="939f9-187">管理認證</span><span class="sxs-lookup"><span data-stu-id="939f9-187">Change credentials</span></span>

<span data-ttu-id="939f9-188">AD 應用程式，因為安全性洩露或認證過期的 toochange hello 認證使用 hello[移除 AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential)和[新增 AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="939f9-188">toochange hello credentials for an AD app, either because of a security compromise or a credential expiration, use hello [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) and [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.</span></span>

<span data-ttu-id="939f9-189">tooremove 所有 hello 認證的應用程式，都使用：</span><span class="sxs-lookup"><span data-stu-id="939f9-189">tooremove all hello credentials for an application, use:</span></span>

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

<span data-ttu-id="939f9-190">tooadd 密碼，請使用：</span><span class="sxs-lookup"><span data-stu-id="939f9-190">tooadd a password, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

<span data-ttu-id="939f9-191">本主題中所示，tooadd 憑證的值，會建立自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="939f9-191">tooadd a certificate value, create a self-signed certificate as shown in this topic.</span></span> <span data-ttu-id="939f9-192">然後，使用︰</span><span class="sxs-lookup"><span data-stu-id="939f9-192">Then, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-toosimplify-log-in"></a><span data-ttu-id="939f9-193">儲存的存取權杖 toosimplify 登入</span><span class="sxs-lookup"><span data-stu-id="939f9-193">Save access token toosimplify log in</span></span>
<span data-ttu-id="939f9-194">tooavoid 提供 hello 服務主體認證每次需要 toolog 中的，您可以儲存 hello 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="939f9-194">tooavoid providing hello service principal credentials every time it needs toolog in, you can save hello access token.</span></span>

<span data-ttu-id="939f9-195">toouse hello 目前的存取權杖的更新版本的工作階段中儲存 hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="939f9-195">toouse hello current access token in a later session, save hello profile.</span></span>
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
<span data-ttu-id="939f9-196">開啟 hello 設定檔，並檢查其內容。</span><span class="sxs-lookup"><span data-stu-id="939f9-196">Open hello profile and examine its contents.</span></span> <span data-ttu-id="939f9-197">請注意其中包含存取權杖。</span><span class="sxs-lookup"><span data-stu-id="939f9-197">Notice that it contains an access token.</span></span> <span data-ttu-id="939f9-198">而不是以手動方式重新登入，只載入 hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="939f9-198">Instead of manually logging in again, simply load hello profile.</span></span>
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> <span data-ttu-id="939f9-199">hello 存取權杖到期，所以使用儲存的設定檔只適用於只要 hello 權杖是有效的。</span><span class="sxs-lookup"><span data-stu-id="939f9-199">hello access token expires, so using a saved profile only works for as long as hello token is valid.</span></span>
>  

<span data-ttu-id="939f9-200">或者，您可以叫用 REST 作業，從 PowerShell toolog 中。</span><span class="sxs-lookup"><span data-stu-id="939f9-200">Alternatively, you can invoke REST operations from PowerShell toolog in.</span></span> <span data-ttu-id="939f9-201">從 hello 驗證回應，您可以擷取 hello 存取權杖用於其他作業。</span><span class="sxs-lookup"><span data-stu-id="939f9-201">From hello authentication response, you can retrieve hello access token for use with other operations.</span></span> <span data-ttu-id="939f9-202">藉由叫用 REST 作業擷取 hello 存取權杖的範例，請參閱[產生存取權杖](resource-manager-rest-api.md#generating-an-access-token)。</span><span class="sxs-lookup"><span data-stu-id="939f9-202">For an example of retrieving hello access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="debug"></a><span data-ttu-id="939f9-203">偵錯</span><span class="sxs-lookup"><span data-stu-id="939f9-203">Debug</span></span>

<span data-ttu-id="939f9-204">您可能會遇到下列錯誤，建立服務主體時的 hello:</span><span class="sxs-lookup"><span data-stu-id="939f9-204">You may encounter hello following errors when creating a service principal:</span></span>

* <span data-ttu-id="939f9-205">**「 Authentication_Unauthorized"**或**」 沒有訂用帳戶中找到 hello 內容。 」**</span><span class="sxs-lookup"><span data-stu-id="939f9-205">**"Authentication_Unauthorized"** or **"No subscription found in hello context."**</span></span> <span data-ttu-id="939f9-206">-您會看到這個錯誤，當您的帳戶未具備 hello[必要的權限](#required-permissions)hello Azure Active Directory tooregister 應用程式上。</span><span class="sxs-lookup"><span data-stu-id="939f9-206">- You see this error when your account does not have hello [required permissions](#required-permissions) on hello Azure Active Directory tooregister an app.</span></span> <span data-ttu-id="939f9-207">通常，只有 Azure Active Directory 中的管理使用者可以註冊應用程式，且您的帳戶不是系統管理員時，就會看到此錯誤。請要求系統管理員 tooeither 指派您 tooan 系統管理員角色或 tooenable 使用者 tooregister 應用程式。</span><span class="sxs-lookup"><span data-stu-id="939f9-207">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin. Ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

* <span data-ttu-id="939f9-208">您的帳戶**」 沒有授權 tooperform 動作 'Microsoft.Authorization/roleAssignments/write' 對範圍 ' / 訂用帳戶 / {guid}'。 」** -當您的帳戶未具備足夠的權限 tooassign 角色 tooan 身分識別，您會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="939f9-208">Your account **"does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions tooassign a role tooan identity.</span></span> <span data-ttu-id="939f9-209">詢問您的訂用帳戶管理員 tooadd 您 tooUser 存取 」 系統管理員角色。</span><span class="sxs-lookup"><span data-stu-id="939f9-209">Ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="939f9-210">範例應用程式</span><span class="sxs-lookup"><span data-stu-id="939f9-210">Sample applications</span></span>
<span data-ttu-id="939f9-211">如需透過不同平台的 hello 應用程式以登入資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="939f9-211">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="939f9-212">.NET</span><span class="sxs-lookup"><span data-stu-id="939f9-212">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="939f9-213">Java</span><span class="sxs-lookup"><span data-stu-id="939f9-213">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="939f9-214">Node.js</span><span class="sxs-lookup"><span data-stu-id="939f9-214">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="939f9-215">Python</span><span class="sxs-lookup"><span data-stu-id="939f9-215">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="939f9-216">Ruby</span><span class="sxs-lookup"><span data-stu-id="939f9-216">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="939f9-217">後續步驟</span><span class="sxs-lookup"><span data-stu-id="939f9-217">Next steps</span></span>
* <span data-ttu-id="939f9-218">如需整合到 Azure 的應用程式管理資源的詳細步驟，請參閱[以 hello Azure 資源管理員 API 的開發人員指南 tooauthorization](resource-manager-api-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="939f9-218">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="939f9-219">如需應用程式和服務主體的詳細說明，請參閱[應用程式物件和服務主體物件](../active-directory/active-directory-application-objects.md)。</span><span class="sxs-lookup"><span data-stu-id="939f9-219">For a more detailed explanation of applications and service principals, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span> 
* <span data-ttu-id="939f9-220">如需 Azure Active Directory 驗證的詳細資訊，請參閱 [Azure AD 的驗證案例](../active-directory/active-directory-authentication-scenarios.md)。</span><span class="sxs-lookup"><span data-stu-id="939f9-220">For more information about Azure Active Directory authentication, see [Authentication Scenarios for Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span></span>
* <span data-ttu-id="939f9-221">如需可授與或拒絕 toousers 可用動作的清單，請參閱[Azure 資源管理員資源提供者作業](../active-directory/role-based-access-control-resource-provider-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="939f9-221">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>

