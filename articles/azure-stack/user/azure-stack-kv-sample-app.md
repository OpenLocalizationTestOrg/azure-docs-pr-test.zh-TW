---
title: "允許應用程式取出 Azure Stack Key Vault 密碼 | Microsoft Docs"
description: "使用範例應用程式來處理 Azure Stack Key Vault"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 3748b719-e269-4b48-8d7d-d75a84b0e1e5
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/26/2017
ms.author: sngun
ms.openlocfilehash: 7cfb78cc5219d4adab5ceddc9d7eb8d1fc71b678
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="sample-application-that-uses-keys-and-secrets-stored-in-a-key-vault"></a><span data-ttu-id="c848c-103">使用金鑰保存庫中所儲存金鑰和密碼的範例應用程式</span><span class="sxs-lookup"><span data-stu-id="c848c-103">Sample application that uses keys and secrets stored in a key vault</span></span>

<span data-ttu-id="c848c-104">在本文章中，我們將說明如何執行範例應用程式 (HelloKeyVault) 以取出 Azure Stack 中金鑰保存庫的金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="c848c-104">In this article, we show you how to run a sample application (HelloKeyVault) that retrieves keys and secrets from a key vault in Azure Stack.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c848c-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="c848c-105">Prerequisites</span></span> 

<span data-ttu-id="c848c-106">從[開發套件](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop)，或從 Windows 型外部用戶端 (如果您是[透過 VPN 連線](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn))，執行下列先決條件：</span><span class="sxs-lookup"><span data-stu-id="c848c-106">Run the following prerequisites either from the [Development Kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="c848c-107">安裝 [Azure Stack 相容的 Azure PowerShell 模組](azure-stack-powershell-install.md)。</span><span class="sxs-lookup"><span data-stu-id="c848c-107">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
* <span data-ttu-id="c848c-108">下載[處理 Azure Stack 所需的工具](azure-stack-powershell-download.md)。</span><span class="sxs-lookup"><span data-stu-id="c848c-108">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span> 

## <a name="create-and-get-the-key-vault-and-application-settings"></a><span data-ttu-id="c848c-109">建立並取得金鑰保存庫和應用程式設定</span><span class="sxs-lookup"><span data-stu-id="c848c-109">Create and get the key vault and application settings</span></span>

<span data-ttu-id="c848c-110">首先，您應該在 Azure Stack 中建立金鑰保存庫，並在 Azure Active Directory (Azure AD) 中註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="c848c-110">First, you should create a key vault in Azure Stack, and register an application in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="c848c-111">您可以使用 Azure 入口網站或 PowerShell 來建立及註冊金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="c848c-111">You can create and register the key vaults by using the Azure portal or PowerShell.</span></span> <span data-ttu-id="c848c-112">此文章說明以 PowerShell 的方式來執行該作業。</span><span class="sxs-lookup"><span data-stu-id="c848c-112">This article shows you the PowerShell way to do the tasks.</span></span> <span data-ttu-id="c848c-113">依預設，此 PowerShell 指令碼會在 Active Directory 中建立新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c848c-113">By default, this PowerShell script creates a new application in Active Directory.</span></span> <span data-ttu-id="c848c-114">不過，您也可以使用您的其中一個現有的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c848c-114">However, you can also use one of your existing applications.</span></span> <span data-ttu-id="c848c-115">請確定提供 `aadTenantName` 和 `applicationPassword` 變數的值。</span><span class="sxs-lookup"><span data-stu-id="c848c-115">Make sure to provide a value for the `aadTenantName` and `applicationPassword` variables.</span></span> <span data-ttu-id="c848c-116">如果您並未指定 `applicationPassword` 變數的值，則此指令碼將會產生隨機密碼。</span><span class="sxs-lookup"><span data-stu-id="c848c-116">If you don't specify a value for the `applicationPassword` variable, this script generates a random password.</span></span> 

```powershell
$vaultName           = 'myVault'
$resourceGroupName   = 'myResourceGroup'
$applicationName     = 'myApp'
$location            = 'local' 

# Password for the application. If not specified, this script will generate a random password during app creation.
$applicationPassword = '' 
                         
# Function to generate a random password for the application.
Function GenerateSymmetricKey()
{
    $key = New-Object byte[](32)
    $rng = [System.Security.Cryptography.RNGCryptoServiceProvider]::Create()
    $rng.GetBytes($key)
    return [System.Convert]::ToBase64String($key)
}

Write-Host 'Please log into your Azure Stack user environment' -foregroundcolor Green

$tenantARM = "https://management.local.azurestack.external"
$aadTenantName = "PLEASE FILL THIS IN WITH YOUR AAD TENANT NAME. FOR EXAMPLE: myazurestack.onmicrosoft.com"

# Configure the Azure Stack operator’s PowerShell environment.
Add-AzureRMEnvironment `
  -Name "AzureStackUser" `
  -ArmEndpoint $tenantARM

Set-AzureRmEnvironment `
  -Name "AzureStackAdmin" `
  -GraphAudience "https://graph.windows.net/"

$TenantID = Get-AzsDirectoryTenantId `
  -AADTenantName $aadTenantName `
  -EnvironmentName AzureStackUser

# Sign in to the user portal.
Login-AzureRmAccount `
  -EnvironmentName "AzureStackUser" `
  -TenantId $TenantID `
  
$now = [System.DateTime]::Now
$oneYearFromNow = $now.AddYears(1)

$applicationPassword = GenerateSymmetricKey
    
# Create a new Azure AD application.
$identifierUri = [string]::Format("http://localhost:8080/{0}",[Guid]::NewGuid().ToString("N"))
$homePage = "http://contoso.com"

Write-Host "Creating a new AAD Application"
$ADApp = New-AzureRmADApplication `
  -DisplayName $applicationName `
  -HomePage $homePage `
  -IdentifierUris $identifierUri `
  -StartDate $now `
  -EndDate $oneYearFromNow `
  -Password $applicationPassword

Write-Host "Creating a new AAD service principal"
$servicePrincipal = New-AzureRmADServicePrincipal `
  -ApplicationId $ADApp.ApplicationId

# Create a new resource group and a key vault within that resource group.
New-AzureRmResourceGroup `
  -Name $resourceGroupName `
  -Location $location   

Write-Host "Creating vault $vaultName"
$vault = New-AzureRmKeyVault -VaultName $vaultName `
  -ResourceGroupName $resourceGroupName `
  -Sku standard `
  -Location $location

# Specify full privileges to the vault for the application.
Write-Host "Setting access policy"
Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName `
  -ObjectId $servicePrincipal.Id `
  -PermissionsToKeys all `
  -PermissionsToSecrets all

Write-Host "Paste the following settings into the app.config file for the HelloKeyVault project:"
'<add key="VaultUrl" value="' + $vault.VaultUri + '"/>'
'<add key="AuthClientId" value="' + $servicePrincipal.ApplicationId + '"/>'
'<add key="AuthClientSecret" value="' + $applicationPassword + '"/>'
Write-Host

``` 

<span data-ttu-id="c848c-117">下列螢幕擷取畫面會顯示先前指令碼的輸出：</span><span class="sxs-lookup"><span data-stu-id="c848c-117">The following screenshot shows the output of the previous script:</span></span>

![應用程式組態](media/azure-stack-kv-sample-app/settingsoutput.png)

<span data-ttu-id="c848c-119">記下先前指令碼所傳回 **VaultUrl**、**AuthClientId** 和 **AuthClientSecret** 的值。</span><span class="sxs-lookup"><span data-stu-id="c848c-119">Make a note of the **VaultUrl**, **AuthClientId**, and **AuthClientSecret** values returned by the previous script.</span></span> <span data-ttu-id="c848c-120">您將使用這些值來執行 HelloKeyVault 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c848c-120">You use these values to run the HelloKeyVault application.</span></span>

## <a name="download-and-run-the-sample-application"></a><span data-ttu-id="c848c-121">下載並執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="c848c-121">Download and run the sample application</span></span>

<span data-ttu-id="c848c-122">下載 Azure [金鑰保存庫用戶端範例](https://www.microsoft.com/en-us/download/details.aspx?id=45343)頁面所提供的金鑰保存庫範例。</span><span class="sxs-lookup"><span data-stu-id="c848c-122">Download the key vault sample from the Azure [Key Vault client samples](https://www.microsoft.com/en-us/download/details.aspx?id=45343) page.</span></span> <span data-ttu-id="c848c-123">將.zip 檔的內容解壓縮至您的開發工作站上。</span><span class="sxs-lookup"><span data-stu-id="c848c-123">Extract the contents of the .zip file onto your development workstation.</span></span> <span data-ttu-id="c848c-124">範例資料夾中有兩個範例。</span><span class="sxs-lookup"><span data-stu-id="c848c-124">There are two samples within the samples folder.</span></span> <span data-ttu-id="c848c-125">我們在本主題中會使用 HellpKeyVault 範例。</span><span class="sxs-lookup"><span data-stu-id="c848c-125">We use the HellpKeyVault sample in this topic.</span></span> <span data-ttu-id="c848c-126">瀏覽至 **Microsoft.Azure.KeyVault.Samples** > **範例** > **HelloKeyVault** 資料夾，然後在 Visual Studio 中開啟 HelloKeyVault 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c848c-126">Browse to the **Microsoft.Azure.KeyVault.Samples** > **samples** > **HelloKeyVault** folder and open the HelloKeyVault application in Visual Studio.</span></span> 

<span data-ttu-id="c848c-127">開啟 HelloKeyVault\App.config 檔案並取代 <appSettings> 元素以及先前指令碼所傳回 **VaultUrl**、**AuthClientId** 和 **AuthClientSecret** 的值。</span><span class="sxs-lookup"><span data-stu-id="c848c-127">Open the HelloKeyVault\App.config file and replace the values of the <appSettings> element with the **VaultUrl**, **AuthClientId**, and **AuthClientSecret** values returned by the previous script.</span></span> <span data-ttu-id="c848c-128">請注意，依預設 App.config 會包含 *AuthCertThumbprint* 的預留位置，但您將會改用 *AuthClientSecret*。</span><span class="sxs-lookup"><span data-stu-id="c848c-128">Note that by default the App.config contains a placeholder for *AuthCertThumbprint*, but use *AuthClientSecret* instead.</span></span> <span data-ttu-id="c848c-129">取代設定之後，請重建解決方案並啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="c848c-129">After you replace the settings, rebuild the solution and start the application.</span></span>

![應用程式設定](media/azure-stack-kv-sample-app/appconfig.png)
 
<span data-ttu-id="c848c-131">應用程式會登入 Azure AD，然後使用該權杖來驗證 Azure Stack 中的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="c848c-131">The application signs in to Azure AD, and then uses that token to authenticate to the key vault in Azure Stack.</span></span> <span data-ttu-id="c848c-132">應用程式會對金鑰保存庫的金鑰和密碼執行如建立、加密、包裝和刪除等作業。</span><span class="sxs-lookup"><span data-stu-id="c848c-132">The application performs operations like create, encrypt, wrap, and delete on the keys and secrets of the key vault.</span></span> <span data-ttu-id="c848c-133">您也可以將特定參數如 *encrypt* 和 *decrypt* 等傳遞至應用程式，以確保應用程式僅對保存庫執行那些作業。</span><span class="sxs-lookup"><span data-stu-id="c848c-133">You can also pass specific parameters such as *encrypt* and *decrypt* to the application, which makes sure that the application executes only those operations against the vault.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="c848c-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c848c-134">Next steps</span></span>
[<span data-ttu-id="c848c-135">使用金鑰保存庫密碼部署 VM</span><span class="sxs-lookup"><span data-stu-id="c848c-135">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)

[<span data-ttu-id="c848c-136">使用 Key Vault 憑證部署 VM</span><span class="sxs-lookup"><span data-stu-id="c848c-136">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)



