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
# <a name="use-azure-powershell-toocreate-a-service-principal-tooaccess-resources"></a>使用 Azure PowerShell toocreate 服務主體 tooaccess 資源

當您擁有的應用程式或需要 tooaccess 資源的指令碼時，您可以設定 hello 應用程式的身分識別，並驗證它自己的認證與 hello 應用程式。 此身分識別就是所謂的服務主體。 這種方法可讓您︰

* 指派權限 toohello 不同於您自己的權限的應用程式識別。 一般而言，這些權限會限制的 tooexactly 哪些 hello 應用程式需要 toodo。
* 使用憑證在執行無人看管的指令碼時進行驗證。

本主題說明如何 toouse [Azure PowerShell](/powershell/azure/overview) tooset 好您的應用程式 toorun 在它自己的認證和身分識別的所需的一切。

## <a name="required-permissions"></a>所需的權限
toocomplete 本主題中，您必須在您的 Azure Active Directory 和 Azure 訂用帳戶擁有足夠的權限。 具體來說，您必須是能夠 toocreate hello Azure Active Directory 中的應用程式，並且將 hello 服務主體 tooa 角色指派。 

hello 最簡單方式 toocheck 您的帳戶是否有足夠的權限是透過 hello 入口網站。 請參閱[檢查必要的權限](resource-group-create-service-principal-portal.md#required-permissions)。

現在，請繼續進行 tooa > 一節，以驗證：

* [password](#create-service-principal-with-password)
* [自我簽署憑證](#create-service-principal-with-self-signed-certificate)
* [來自憑證授權單位的憑證](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a>PowerShell 命令

tooset 註冊服務主體，您使用：

| 命令 | 說明 |
| ------- | ----------- | 
| [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | 建立 Azure Active Directory 服務主體 |
| [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment) | 指派 hello 指定 RBAC 角色 toohello 指定的主體，在 hello 指定的範圍。 |


## <a name="create-service-principal-with-password"></a>使用密碼建立服務主體

toocreate 服務主體與 hello 參與者角色，您的訂用帳戶，使用： 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

hello 範例進入睡眠狀態 20 秒 tooallow hello 新服務主體 toopropagate 整個 Azure Active Directory 一些時間。 如果您的指令碼不會等待足夠的時間，您看到錯誤指出: 「 PrincipalNotFound: hello 目錄中沒有主體 {id}。 」

hello 下列指令碼可讓您 toospecify hello 預設訂用帳戶以外的範圍和重試 hello 角色指派，如果發生錯誤：

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

Hello 指令碼相關的幾個項目 toonote:

* toogrant hello 身分識別存取 toohello 預設訂用帳戶，您不需要 tooprovide ResourceGroup 或 SubscriptionId 參數。
* 只有當您希望 toolimit hello 範圍 hello 角色指派 tooa 資源群組時，請指定 hello ResourceGroup 參數。
*  在此範例中，您可以將 hello 服務主體 toohello 參與者角色。 若為其他角色，請參閱 [RBAC︰內建角色](../active-directory/role-based-access-built-in-roles.md)。
* hello 指令碼睡眠 15 秒 tooallow hello 新服務主體 toopropagate 整個 Azure Active Directory 一些時間。 如果您的指令碼不會等待足夠的時間，您看到錯誤指出: 「 PrincipalNotFound: hello 目錄中沒有主體 {id}。 」
* 如果您需要 toogrant hello 服務主體存取 toomore 訂閱或資源群組，執行 hello`New-AzureRMRoleAssignment`指令程式搭配不同範圍的一次。


### <a name="provide-credentials-through-powershell"></a>透過 PowerShell 提供認證
現在，您必須在 toolog 為 hello tooperform 應用程式的作業。 Hello 使用者名稱，使用 hello `ApplicationId` hello 應用程式所建立。 Hello 密碼使用 hello 建立 hello 帳戶時，您指定的其中一個。 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

hello 租用戶識別碼不區分大小寫，因此您可以將它內嵌直接在您的指令碼中。 如果您需要 tooretrieve hello 租用戶識別碼，請使用：

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a>使用自我簽署憑證建立服務主體

toocreate 使用自我簽署的憑證和訂用帳戶，hello 參與者角色的服務主體： 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

hello 範例進入睡眠狀態 20 秒 tooallow hello 新服務主體 toopropagate 整個 Azure Active Directory 一些時間。 如果您的指令碼不會等待足夠的時間，您看到錯誤指出: 「 PrincipalNotFound: hello 目錄中沒有主體 {id}。 」

hello 下列指令碼可讓您 toospecify hello 預設訂用帳戶以外的範圍和重試 hello 角色指派，如果發生錯誤。 您必須擁有 Windows 10 或 Windows Server 2016 的 Azure PowerShell 2.0。

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

Hello 指令碼相關的幾個項目 toonote:

* toogrant hello 身分識別存取 toohello 預設訂用帳戶，您不需要 tooprovide ResourceGroup 或 SubscriptionId 參數。
* 只有當您希望 toolimit hello 範圍 hello 角色指派 tooa 資源群組時，請指定 hello ResourceGroup 參數。
* 在此範例中，您可以將 hello 服務主體 toohello 參與者角色。 若為其他角色，請參閱 [RBAC︰內建角色](../active-directory/role-based-access-built-in-roles.md)。
* hello 指令碼睡眠 15 秒 tooallow hello 新服務主體 toopropagate 整個 Azure Active Directory 一些時間。 如果您的指令碼不會等待足夠的時間，您看到錯誤指出: 「 PrincipalNotFound: hello 目錄中沒有主體 {id}。 」
* 如果您需要 toogrant hello 服務主體存取 toomore 訂閱或資源群組，執行 hello`New-AzureRMRoleAssignment`指令程式搭配不同範圍的一次。

如果您**不具有 Windows 10 或 Windows Server 2016 Technical Preview**，您需要 toodownload hello[自我簽署的憑證的產生器](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/)從 Microsoft 指令碼中心。 將其內容解壓縮，並匯入您所需要的 hello cmdlet。

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
在 hello 指令碼，取代下列兩行 toogenerate hello 憑證 hello。
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a>透過自動化的 PowerShell 指令碼提供憑證
每當您登入做為服務主體時，您需要 tooprovide hello 租用戶識別碼 hello 目錄的 AD 應用程式。 租用戶是 Azure Active Directory 的執行個體。 如果您只有一個訂用帳戶，您可以使用：

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

hello 應用程式識別碼和租用戶識別碼不區分大小寫，因此您可以將其內嵌直接在您的指令碼中。 如果您需要 tooretrieve hello 租用戶識別碼，請使用：

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

如果您需要 tooretrieve hello 應用程式識別碼，請使用：

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a>使用憑證授權中心的憑證來建立服務主體
toouse 為憑證授權單位 toocreate 服務主體時，使用下列指令碼的 hello 所發出的憑證：

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

Hello 指令碼相關的幾個項目 toonote:

* 已設定領域的 toohello 訂用帳戶存取。
* 在此範例中，您可以將 hello 服務主體 toohello 參與者角色。 若為其他角色，請參閱 [RBAC︰內建角色](../active-directory/role-based-access-built-in-roles.md)。
* hello 指令碼睡眠 15 秒 tooallow hello 新服務主體 toopropagate 整個 Azure Active Directory 一些時間。 如果您的指令碼不會等待足夠的時間，您看到錯誤指出: 「 PrincipalNotFound: hello 目錄中沒有主體 {id}。 」
* 如果您需要 toogrant hello 服務主體存取 toomore 訂閱或資源群組，執行 hello`New-AzureRMRoleAssignment`指令程式搭配不同範圍的一次。

### <a name="provide-certificate-through-automated-powershell-script"></a>透過自動化的 PowerShell 指令碼提供憑證
每當您登入做為服務主體時，您需要 tooprovide hello 租用戶識別碼 hello 目錄的 AD 應用程式。 租用戶是 Azure Active Directory 的執行個體。

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

hello 應用程式識別碼和租用戶識別碼不區分大小寫，因此您可以將其內嵌直接在您的指令碼中。 如果您需要 tooretrieve hello 租用戶識別碼，請使用：

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

如果您需要 tooretrieve hello 應用程式識別碼，請使用：

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a>管理認證

AD 應用程式，因為安全性洩露或認證過期的 toochange hello 認證使用 hello[移除 AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential)和[新增 AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlet。

tooremove 所有 hello 認證的應用程式，都使用：

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

tooadd 密碼，請使用：

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

本主題中所示，tooadd 憑證的值，會建立自我簽署的憑證。 然後，使用︰

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-toosimplify-log-in"></a>儲存的存取權杖 toosimplify 登入
tooavoid 提供 hello 服務主體認證每次需要 toolog 中的，您可以儲存 hello 存取權杖。

toouse hello 目前的存取權杖的更新版本的工作階段中儲存 hello 設定檔。
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
開啟 hello 設定檔，並檢查其內容。 請注意其中包含存取權杖。 而不是以手動方式重新登入，只載入 hello 設定檔。
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> hello 存取權杖到期，所以使用儲存的設定檔只適用於只要 hello 權杖是有效的。
>  

或者，您可以叫用 REST 作業，從 PowerShell toolog 中。 從 hello 驗證回應，您可以擷取 hello 存取權杖用於其他作業。 藉由叫用 REST 作業擷取 hello 存取權杖的範例，請參閱[產生存取權杖](resource-manager-rest-api.md#generating-an-access-token)。

## <a name="debug"></a>偵錯

您可能會遇到下列錯誤，建立服務主體時的 hello:

* **「 Authentication_Unauthorized"**或**」 沒有訂用帳戶中找到 hello 內容。 」** -您會看到這個錯誤，當您的帳戶未具備 hello[必要的權限](#required-permissions)hello Azure Active Directory tooregister 應用程式上。 通常，只有 Azure Active Directory 中的管理使用者可以註冊應用程式，且您的帳戶不是系統管理員時，就會看到此錯誤。請要求系統管理員 tooeither 指派您 tooan 系統管理員角色或 tooenable 使用者 tooregister 應用程式。

* 您的帳戶**」 沒有授權 tooperform 動作 'Microsoft.Authorization/roleAssignments/write' 對範圍 ' / 訂用帳戶 / {guid}'。 」** -當您的帳戶未具備足夠的權限 tooassign 角色 tooan 身分識別，您會看到此錯誤。 詢問您的訂用帳戶管理員 tooadd 您 tooUser 存取 」 系統管理員角色。

## <a name="sample-applications"></a>範例應用程式
如需透過不同平台的 hello 應用程式以登入資訊，請參閱：

* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a>後續步驟
* 如需整合到 Azure 的應用程式管理資源的詳細步驟，請參閱[以 hello Azure 資源管理員 API 的開發人員指南 tooauthorization](resource-manager-api-authentication.md)。
* 如需應用程式和服務主體的詳細說明，請參閱[應用程式物件和服務主體物件](../active-directory/active-directory-application-objects.md)。 
* 如需 Azure Active Directory 驗證的詳細資訊，請參閱 [Azure AD 的驗證案例](../active-directory/active-directory-authentication-scenarios.md)。
* 如需可授與或拒絕 toousers 可用動作的清單，請參閱[Azure 資源管理員資源提供者作業](../active-directory/role-based-access-control-resource-provider-operations.md)。

