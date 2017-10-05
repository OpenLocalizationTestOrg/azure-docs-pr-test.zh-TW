---
title: "將 Azure 中 Windows VM 上的磁碟加密 | Microsoft Docs"
description: "如何使用 Azure PowerShell 將 Windows VM 上的虛擬磁碟加密以增強安全性"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/10/2017
ms.author: iainfou
ms.openlocfilehash: 98b42b252a601af090579e3939f3c7ab91c3803b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-encrypt-virtual-disks-on-a-windows-vm"></a><span data-ttu-id="c8a61-103">如何將 Windows VM 上的虛擬磁碟加密</span><span class="sxs-lookup"><span data-stu-id="c8a61-103">How to encrypt virtual disks on a Windows VM</span></span>
<span data-ttu-id="c8a61-104">如需強化虛擬機器 (VM) 安全性與法規遵循，可以將 Azure 中的虛擬磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="c8a61-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="c8a61-105">磁碟會使用 Azure 金鑰保存庫中受保護的密碼編譯金鑰進行加密。</span><span class="sxs-lookup"><span data-stu-id="c8a61-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="c8a61-106">您可控制這些密碼編譯金鑰，並可稽核其使用情況。</span><span class="sxs-lookup"><span data-stu-id="c8a61-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="c8a61-107">本文詳細說明如何使用 Azure PowerShell 將 Windows VM 上的虛擬磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="c8a61-107">This article details how to encrypt virtual disks on a Windows VM using Azure PowerShell.</span></span> <span data-ttu-id="c8a61-108">您也可以[使用 Azure CLI 2.0 將 Linux VM 加密](../linux/encrypt-disks.md)。</span><span class="sxs-lookup"><span data-stu-id="c8a61-108">You can also [encrypt a Linux VM using the Azure CLI 2.0](../linux/encrypt-disks.md).</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="c8a61-109">磁碟加密概觀</span><span class="sxs-lookup"><span data-stu-id="c8a61-109">Overview of disk encryption</span></span>
<span data-ttu-id="c8a61-110">加密 Windows VM 上的虛擬磁碟時，是在待用時使用 Bitlocker 進行加密。</span><span class="sxs-lookup"><span data-stu-id="c8a61-110">Virtual disks on Windows VMs are encrypted at rest using Bitlocker.</span></span> <span data-ttu-id="c8a61-111">將 Azure 中的虛擬磁碟加密完全免費。</span><span class="sxs-lookup"><span data-stu-id="c8a61-111">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="c8a61-112">密碼編譯金鑰會使用軟體保護功能儲存在 Azure 金鑰保存庫中，或者您可以在 FIPS 140-2 第 2 級標準認證的硬體安全性模組 (HSM) 中匯入或產生金鑰。</span><span class="sxs-lookup"><span data-stu-id="c8a61-112">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="c8a61-113">這些密碼編譯金鑰用來加密及解密連接到 VM 的虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="c8a61-113">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span></span> <span data-ttu-id="c8a61-114">您可保留這些密碼編譯金鑰的控制權，並可稽核其使用情況。</span><span class="sxs-lookup"><span data-stu-id="c8a61-114">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="c8a61-115">Azure Active Directory 服務主體會提供一個安全機制，以便在 VM 開機或關機時發出這些密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="c8a61-115">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="c8a61-116">將 VM 加密的程序如下所示：</span><span class="sxs-lookup"><span data-stu-id="c8a61-116">The process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="c8a61-117">在 Azure 金鑰保存庫中建立密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="c8a61-117">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="c8a61-118">將密碼編譯金鑰設定為可用於磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="c8a61-118">Configure the cryptographic key to be usable for encrypting disks.</span></span>
3. <span data-ttu-id="c8a61-119">若要讀取 Azure Key Vault 中的密碼編譯金鑰，請使用適當的權限建立 Azure Active Directory 服務主體。</span><span class="sxs-lookup"><span data-stu-id="c8a61-119">To read the cryptographic key from the Azure Key Vault, create an Azure Active Directory service principal with the appropriate permissions.</span></span>
4. <span data-ttu-id="c8a61-120">發出命令以將您的虛擬磁碟加密，並指定要使用的 Azure Active Directory 服務主體和適當密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="c8a61-120">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory service principal and appropriate cryptographic key to be used.</span></span>
5. <span data-ttu-id="c8a61-121">Azure Active Directory 服務主體會向 Azure Key Vault 要求所需的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="c8a61-121">The Azure Active Directory service principal requests the required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="c8a61-122">虛擬磁碟會使用所提供的密碼編譯金鑰進行加密。</span><span class="sxs-lookup"><span data-stu-id="c8a61-122">The virtual disks are encrypted using the provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="c8a61-123">加密程序</span><span class="sxs-lookup"><span data-stu-id="c8a61-123">Encryption process</span></span>
<span data-ttu-id="c8a61-124">磁碟加密依賴下列其他元件︰</span><span class="sxs-lookup"><span data-stu-id="c8a61-124">Disk encryption relies on the following additional components:</span></span>

* <span data-ttu-id="c8a61-125">**Azure 金鑰保存庫** - 用來保護磁碟加密/解密程序所使用的密碼編譯金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="c8a61-125">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span></span> 
  * <span data-ttu-id="c8a61-126">如果有的話，您可以使用現有的 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="c8a61-126">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="c8a61-127">您沒有專門用來加密磁碟的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="c8a61-127">You do not have to dedicate a Key Vault to encrypting disks.</span></span>
  * <span data-ttu-id="c8a61-128">若要區分系統管理界限和金鑰可視性，您可以建立專用的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="c8a61-128">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="c8a61-129">**Azure Active Directory** - 處理必要密碼編譯金鑰的安全交換以及所要求動作的驗證。</span><span class="sxs-lookup"><span data-stu-id="c8a61-129">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span></span> 
  * <span data-ttu-id="c8a61-130">您通常使用現有的 Azure Active Directory 執行個體來裝載您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c8a61-130">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="c8a61-131">服務主體會提供一個安全機制來要求並取得適當的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="c8a61-131">The service principal provides a secure mechanism to request and be issued the appropriate cryptographic keys.</span></span> <span data-ttu-id="c8a61-132">您並未開發與 Azure Active Directory 整合的實際應用程式。</span><span class="sxs-lookup"><span data-stu-id="c8a61-132">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="c8a61-133">需求和限制</span><span class="sxs-lookup"><span data-stu-id="c8a61-133">Requirements and limitations</span></span>
<span data-ttu-id="c8a61-134">磁碟加密支援的案例和需求：</span><span class="sxs-lookup"><span data-stu-id="c8a61-134">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="c8a61-135">從 Azure Marketplace 映像或自訂 VHD 映像在新的 Windows VM 上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="c8a61-135">Enabling encryption on new Windows VMs from Azure Marketplace images or custom VHD image.</span></span>
* <span data-ttu-id="c8a61-136">在 Azure 中現有的 Windows VM 上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="c8a61-136">Enabling encryption on existing Windows VMs in Azure.</span></span>
* <span data-ttu-id="c8a61-137">在使用「儲存空間」來設定的 Windows VM 上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="c8a61-137">Enabling encryption on Windows VMs that are configured using Storage Spaces.</span></span>
* <span data-ttu-id="c8a61-138">在 Windows VM 的 OS 和資料磁碟機上停用加密。</span><span class="sxs-lookup"><span data-stu-id="c8a61-138">Disabling encryption on OS and data drives for Windows VMs.</span></span>
* <span data-ttu-id="c8a61-139">所有資源 (例如金鑰保存庫、儲存體帳戶、VM) 必須位於相同的 Azure 區域和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c8a61-139">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span></span>
* <span data-ttu-id="c8a61-140">標準層 VM，例如 A、D、DS、G 及 GS 系列 VM。</span><span class="sxs-lookup"><span data-stu-id="c8a61-140">Standard tier VMs, such as A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="c8a61-141">下列案例目前不支援磁碟加密︰</span><span class="sxs-lookup"><span data-stu-id="c8a61-141">Disk encryption is not currently supported in the following scenarios:</span></span>

* <span data-ttu-id="c8a61-142">基本層 VM。</span><span class="sxs-lookup"><span data-stu-id="c8a61-142">Basic tier VMs.</span></span>
* <span data-ttu-id="c8a61-143">使用傳統部署模型建立的 VM。</span><span class="sxs-lookup"><span data-stu-id="c8a61-143">VMs created using the Classic deployment model.</span></span>
* <span data-ttu-id="c8a61-144">在已經加密的 VM 上更新密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="c8a61-144">Updating the cryptographic keys on an already encrypted VM.</span></span>
* <span data-ttu-id="c8a61-145">與內部部署「金鑰管理服務」整合。</span><span class="sxs-lookup"><span data-stu-id="c8a61-145">Integration with on-prem Key Management Service.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="c8a61-146">建立 Azure Key Vault 和金鑰</span><span class="sxs-lookup"><span data-stu-id="c8a61-146">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="c8a61-147">開始之前，請確定已安裝最新版的 Azure PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="c8a61-147">Before you start, make sure that the latest version of the Azure PowerShell module has been installed.</span></span> <span data-ttu-id="c8a61-148">如需詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="c8a61-148">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="c8a61-149">在整個命令範例中，以您自己的名稱、位置和金鑰值取代所有的範例參數。</span><span class="sxs-lookup"><span data-stu-id="c8a61-149">Throughout the command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="c8a61-150">下列範例使用 *myResourceGroup*、*myKeyVault*、*myVM* 等慣例。</span><span class="sxs-lookup"><span data-stu-id="c8a61-150">The following examples use a convention of *myResourceGroup*, *myKeyVault*, *myVM*, etc.</span></span>

<span data-ttu-id="c8a61-151">建立 Azure 金鑰保存庫的第一個步驟是儲存您的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="c8a61-151">The first step is to create an Azure Key Vault to store your cryptographic keys.</span></span> <span data-ttu-id="c8a61-152">Azure 金鑰保存庫儲存可讓您安全地在應用程式和服務中實作的金鑰和密碼 (Secret 或 Password)。</span><span class="sxs-lookup"><span data-stu-id="c8a61-152">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span></span> <span data-ttu-id="c8a61-153">針對虛擬磁碟加密，您需建立 Key Vault 來儲存用來加密或解密虛擬磁碟的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="c8a61-153">For virtual disk encryption, you create a Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span></span> 

<span data-ttu-id="c8a61-154">請使用 [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider) 來啟用您 Azure 訂用帳戶內的 Azure Key Vault 提供者，然後使用 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="c8a61-154">Enable the Azure Key Vault provider within your Azure subscription with [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), then create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="c8a61-155">下列範例會在 *East US* 位置建立名為 *myResourceGroup* 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="c8a61-155">The following example creates a resource group name *myResourceGroup* in the *East US* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

<span data-ttu-id="c8a61-156">包含密碼編譯金鑰和相關聯計算資源 (例如儲存體和 VM) 的 Azure 金鑰保存庫本身必須位於相同的區域中。</span><span class="sxs-lookup"><span data-stu-id="c8a61-156">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span></span> <span data-ttu-id="c8a61-157">請使用 [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) 來建立 Azure Key Vault，然後啟用 Key Vault 以搭配磁碟加密使用。</span><span class="sxs-lookup"><span data-stu-id="c8a61-157">Create an Azure Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) and enable the Key Vault for use with disk encryption.</span></span> <span data-ttu-id="c8a61-158">針對 *keyVaultName* 指定一個唯一的 Key Vault 名稱，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="c8a61-158">Specify a unique Key Vault name for *keyVaultName* as follows:</span></span>

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

<span data-ttu-id="c8a61-159">您可以使用軟體或硬體安全性模型 (HSM) 保護功能來儲存密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="c8a61-159">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="c8a61-160">使用 HSM 時需要進階金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="c8a61-160">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="c8a61-161">建立進階金鑰保存庫 (而非用來儲存軟體保護金鑰的標準金鑰保存庫) 會有額外的成本。</span><span class="sxs-lookup"><span data-stu-id="c8a61-161">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="c8a61-162">若要建立進階 Key Vault，請在上一個步驟中新增 *-Sku "Premium"* 參數。</span><span class="sxs-lookup"><span data-stu-id="c8a61-162">To create a premium Key Vault, in the preceding step add the *-Sku "Premium"* parameters.</span></span> <span data-ttu-id="c8a61-163">下列範例會使用軟體保護的金鑰，因為我們建立了標準金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="c8a61-163">The following example uses software-protected keys since we created a standard Key Vault.</span></span> 

<span data-ttu-id="c8a61-164">在兩種保護模型中，Azure 平台都必須獲得存取權，才能在 VM 開機時要求密碼編譯金鑰來將虛擬磁碟解密。</span><span class="sxs-lookup"><span data-stu-id="c8a61-164">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span></span> <span data-ttu-id="c8a61-165">請使用 [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) 在您的 Key Vault 中建立密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="c8a61-165">Create a cryptographic key in your Key Vault with [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span></span> <span data-ttu-id="c8a61-166">下列範例會建立一個名為 *myKey* 的金鑰：</span><span class="sxs-lookup"><span data-stu-id="c8a61-166">The following example creates a key named *myKey*:</span></span>

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-the-azure-active-directory-service-principal"></a><span data-ttu-id="c8a61-167">建立 Azure Active Directory 服務主體</span><span class="sxs-lookup"><span data-stu-id="c8a61-167">Create the Azure Active Directory service principal</span></span>
<span data-ttu-id="c8a61-168">將虛擬磁碟加密或解密時，您可以指定帳戶以處理 Key Vault 中密碼編譯金鑰的驗證和交換。</span><span class="sxs-lookup"><span data-stu-id="c8a61-168">When virtual disks are encrypted or decrypted, you specify an account to handle the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="c8a61-169">此帳戶 (Azure Active Directory 服務主體) 可讓 Azure 平台代表 VM 要求適當的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="c8a61-169">This account, an Azure Active Directory service principal, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span></span> <span data-ttu-id="c8a61-170">雖然許多組織都有專用的 Azure Active Directory 目錄，但您的訂用帳戶中會有預設 Azure Active Directory 執行個體。</span><span class="sxs-lookup"><span data-stu-id="c8a61-170">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="c8a61-171">請使用 [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) 在 Azure Active Directory 中建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="c8a61-171">Create a service principal in Azure Active Directory with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span></span> <span data-ttu-id="c8a61-172">若要指定安全的密碼，請依照 [Azure Active Directory 中的密碼原則和限制](../../active-directory/active-directory-passwords-policy.md)所述進行操作：</span><span class="sxs-lookup"><span data-stu-id="c8a61-172">To specify a secure password, follow the [Password policies and restrictions in Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span></span>

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

<span data-ttu-id="c8a61-173">若要成功加密或解密虛擬磁碟，Key Vault 中儲存之密碼編譯金鑰的權限必須設定為允許 Azure Active Directory 服務主體讀取金鑰。</span><span class="sxs-lookup"><span data-stu-id="c8a61-173">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory service principal to read the keys.</span></span> <span data-ttu-id="c8a61-174">請使用 [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) 來設定 Key Vault 的權限：</span><span class="sxs-lookup"><span data-stu-id="c8a61-174">Set permissions on your Key Vault with [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a><span data-ttu-id="c8a61-175">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="c8a61-175">Create virtual machine</span></span>
<span data-ttu-id="c8a61-176">為了測試加密程序，讓我們建立一個 VM。</span><span class="sxs-lookup"><span data-stu-id="c8a61-176">To test the encryption process, let's create a VM.</span></span> <span data-ttu-id="c8a61-177">下列範例會使用 *Windows Server 2016 Datacenter* 映像來建立一個名為 *myVM* 的 VM︰</span><span class="sxs-lookup"><span data-stu-id="c8a61-177">The following example creates a VM named *myVM* using a *Windows Server 2016 Datacenter* image:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "mypublicdns$(Get-Random)"

$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$cred = Get-Credential

$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="c8a61-178">將虛擬機器加密</span><span class="sxs-lookup"><span data-stu-id="c8a61-178">Encrypt virtual machine</span></span>
<span data-ttu-id="c8a61-179">若要將虛擬磁碟加密，您可結合所有先前的元件︰</span><span class="sxs-lookup"><span data-stu-id="c8a61-179">To encrypt the virtual disks, you bring together all the previous components:</span></span>

1. <span data-ttu-id="c8a61-180">指定 Azure Active Directory 服務主體和密碼。</span><span class="sxs-lookup"><span data-stu-id="c8a61-180">Specify the Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="c8a61-181">指定金鑰保存庫以儲存已加密磁碟的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="c8a61-181">Specify the Key Vault to store the metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="c8a61-182">指定要用於實際加密和解密的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="c8a61-182">Specify the cryptographic keys to use for the actual encryption and decryption.</span></span>
4. <span data-ttu-id="c8a61-183">指定是否要將作業系統磁碟、資料磁碟或所有磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="c8a61-183">Specify whether you want to encrypt the OS disk, the data disks, or all.</span></span>

<span data-ttu-id="c8a61-184">請使用 [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) 搭配 Azure Key Vault 金鑰和 Azure Active Directory 服務主體認證，來加密您的 VM。</span><span class="sxs-lookup"><span data-stu-id="c8a61-184">Encrypt your VM with [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) using the Azure Key Vault key and Azure Active Directory service principal credentials.</span></span> <span data-ttu-id="c8a61-185">下列範例會擷取所有金鑰資訊，然後加密名為 *myVM* 的 VM：</span><span class="sxs-lookup"><span data-stu-id="c8a61-185">The following example retrieves all the key information then encrypts the VM named *myVM*:</span></span>

```powershell
$keyVault = Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $rgName;
$diskEncryptionKeyVaultUrl = $keyVault.VaultUri;
$keyVaultResourceId = $keyVault.ResourceId;
$keyEncryptionKeyUrl = (Get-AzureKeyVaultKey -VaultName $keyVaultName -Name myKey).Key.kid;

Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $rgName `
    -VMName $vmName `
    -AadClientID $app.ApplicationId `
    -AadClientSecret $securePassword `
    -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl `
    -DiskEncryptionKeyVaultId $keyVaultResourceId `
    -KeyEncryptionKeyUrl $keyEncryptionKeyUrl `
    -KeyEncryptionKeyVaultId $keyVaultResourceId
```

<span data-ttu-id="c8a61-186">接受提示以繼續進行 VM 加密。</span><span class="sxs-lookup"><span data-stu-id="c8a61-186">Accept the prompt to continue with the VM encryption.</span></span> <span data-ttu-id="c8a61-187">VM 會在此程序中重新啟動。</span><span class="sxs-lookup"><span data-stu-id="c8a61-187">The VM restarts during the process.</span></span> <span data-ttu-id="c8a61-188">加密程序完成且 VM 重新啟動之後，請使用 [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) 來檢閱加密狀態：</span><span class="sxs-lookup"><span data-stu-id="c8a61-188">Once the encryption process completes and the VM has rebooted, review the encryption status with [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span></span>

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

<span data-ttu-id="c8a61-189">輸出類似於下列範例：</span><span class="sxs-lookup"><span data-stu-id="c8a61-189">The output is similar to the following example:</span></span>

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a><span data-ttu-id="c8a61-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c8a61-190">Next steps</span></span>
* <span data-ttu-id="c8a61-191">如需有關管理 Azure Key Vault 的詳細資訊，請參閱[為虛擬機器設定 Key Vault](key-vault-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="c8a61-191">For more information about managing Azure Key Vault, see [Set up Key Vault for virtual machines](key-vault-setup.md).</span></span>
* <span data-ttu-id="c8a61-192">如需有關磁碟加密 (例如準備加密的自訂 VM 以上傳至 Azure) 的詳細資訊，請參閱 [Azure 磁碟加密](../../security/azure-security-disk-encryption.md)。</span><span class="sxs-lookup"><span data-stu-id="c8a61-192">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
