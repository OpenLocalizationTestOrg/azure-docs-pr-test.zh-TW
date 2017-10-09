---
title: "在 Azure 中的 Windows VM 上 aaaEncrypt 磁碟 |Microsoft 文件"
description: "如何針對 Windows VM 上的 tooencrypt 虛擬磁碟增強式安全性使用 Azure PowerShell"
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
ms.openlocfilehash: 77c42a67cb57a9dc5fe3159fce0be75e3a965be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-windows-vm"></a><span data-ttu-id="fcc53-103">如何在 Windows VM 上的 tooencrypt 虛擬磁碟</span><span class="sxs-lookup"><span data-stu-id="fcc53-103">How tooencrypt virtual disks on a Windows VM</span></span>
<span data-ttu-id="fcc53-104">如需強化虛擬機器 (VM) 安全性與法規遵循，可以將 Azure 中的虛擬磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="fcc53-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="fcc53-105">磁碟會使用 Azure 金鑰保存庫中受保護的密碼編譯金鑰進行加密。</span><span class="sxs-lookup"><span data-stu-id="fcc53-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="fcc53-106">您可控制這些密碼編譯金鑰，並可稽核其使用情況。</span><span class="sxs-lookup"><span data-stu-id="fcc53-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="fcc53-107">此發行項詳細資料時，如何使用 Azure PowerShell 的 Windows VM 上的 tooencrypt 虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="fcc53-107">This article details how tooencrypt virtual disks on a Windows VM using Azure PowerShell.</span></span> <span data-ttu-id="fcc53-108">您也可以[加密使用 Azure CLI 2.0 hello 的 Linux VM](../linux/encrypt-disks.md)。</span><span class="sxs-lookup"><span data-stu-id="fcc53-108">You can also [encrypt a Linux VM using hello Azure CLI 2.0](../linux/encrypt-disks.md).</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="fcc53-109">磁碟加密概觀</span><span class="sxs-lookup"><span data-stu-id="fcc53-109">Overview of disk encryption</span></span>
<span data-ttu-id="fcc53-110">加密 Windows VM 上的虛擬磁碟時，是在待用時使用 Bitlocker 進行加密。</span><span class="sxs-lookup"><span data-stu-id="fcc53-110">Virtual disks on Windows VMs are encrypted at rest using Bitlocker.</span></span> <span data-ttu-id="fcc53-111">將 Azure 中的虛擬磁碟加密完全免費。</span><span class="sxs-lookup"><span data-stu-id="fcc53-111">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="fcc53-112">密碼編譯金鑰會儲存在 Azure 金鑰保存庫使用軟體保護，或者您可以匯入或產生您的金鑰，在硬體安全性模組 (Hsm) 認證 tooFIPS 140-2 層級 2 標準。</span><span class="sxs-lookup"><span data-stu-id="fcc53-112">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="fcc53-113">這些密碼編譯金鑰會使用的 tooencrypt，並解密附加的 tooyour VM 虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="fcc53-113">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="fcc53-114">您可保留這些密碼編譯金鑰的控制權，並可稽核其使用情況。</span><span class="sxs-lookup"><span data-stu-id="fcc53-114">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="fcc53-115">Azure Active Directory 服務主體會提供一個安全機制，以便在 VM 開機或關機時發出這些密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="fcc53-115">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="fcc53-116">加密 VM hello 程序如下所示：</span><span class="sxs-lookup"><span data-stu-id="fcc53-116">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="fcc53-117">在 Azure 金鑰保存庫中建立密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="fcc53-117">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="fcc53-118">設定 hello 密碼編譯金鑰 toobe 可用來加密磁碟。</span><span class="sxs-lookup"><span data-stu-id="fcc53-118">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="fcc53-119">tooread hello 密碼編譯金鑰從 hello Azure 金鑰保存庫，建立 Azure Active Directory 服務主體具有 hello 適當的權限。</span><span class="sxs-lookup"><span data-stu-id="fcc53-119">tooread hello cryptographic key from hello Azure Key Vault, create an Azure Active Directory service principal with hello appropriate permissions.</span></span>
4. <span data-ttu-id="fcc53-120">您的虛擬磁碟，指定 hello Azure Active Directory 服務主體 」 和 「 使用適當密碼編譯 toobe 發出 hello 命令 tooencrypt。</span><span class="sxs-lookup"><span data-stu-id="fcc53-120">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory service principal and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="fcc53-121">hello Azure Active Directory 服務主體要求 hello 必要的密碼編譯金鑰，從 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="fcc53-121">hello Azure Active Directory service principal requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="fcc53-122">hello 虛擬磁碟會使用提供的 hello 密碼編譯金鑰來加密。</span><span class="sxs-lookup"><span data-stu-id="fcc53-122">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="fcc53-123">加密程序</span><span class="sxs-lookup"><span data-stu-id="fcc53-123">Encryption process</span></span>
<span data-ttu-id="fcc53-124">磁碟加密依賴 hello 下列額外的元件：</span><span class="sxs-lookup"><span data-stu-id="fcc53-124">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="fcc53-125">**Azure 金鑰保存庫**-使用 toosafeguard 密碼編譯金鑰和 hello 磁碟加密/解密程序所使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="fcc53-125">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span> 
  * <span data-ttu-id="fcc53-126">如果有的話，您可以使用現有的 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="fcc53-126">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="fcc53-127">您沒有 toodedicate 金鑰保存庫 tooencrypting 磁碟。</span><span class="sxs-lookup"><span data-stu-id="fcc53-127">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="fcc53-128">系統管理界限使用 tooseparate 和索引鍵的可見性，您可以建立專用的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="fcc53-128">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="fcc53-129">**Azure Active Directory** -控點 hello 必要的密碼編譯金鑰的安全交換和驗證要求的動作。</span><span class="sxs-lookup"><span data-stu-id="fcc53-129">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span> 
  * <span data-ttu-id="fcc53-130">您通常使用現有的 Azure Active Directory 執行個體來裝載您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fcc53-130">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="fcc53-131">提供安全機制 toorequest hello 服務主體，並發出 hello 適當的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="fcc53-131">hello service principal provides a secure mechanism toorequest and be issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="fcc53-132">您並未開發與 Azure Active Directory 整合的實際應用程式。</span><span class="sxs-lookup"><span data-stu-id="fcc53-132">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="fcc53-133">需求和限制</span><span class="sxs-lookup"><span data-stu-id="fcc53-133">Requirements and limitations</span></span>
<span data-ttu-id="fcc53-134">磁碟加密支援的案例和需求：</span><span class="sxs-lookup"><span data-stu-id="fcc53-134">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="fcc53-135">從 Azure Marketplace 映像或自訂 VHD 映像在新的 Windows VM 上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="fcc53-135">Enabling encryption on new Windows VMs from Azure Marketplace images or custom VHD image.</span></span>
* <span data-ttu-id="fcc53-136">在 Azure 中現有的 Windows VM 上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="fcc53-136">Enabling encryption on existing Windows VMs in Azure.</span></span>
* <span data-ttu-id="fcc53-137">在使用「儲存空間」來設定的 Windows VM 上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="fcc53-137">Enabling encryption on Windows VMs that are configured using Storage Spaces.</span></span>
* <span data-ttu-id="fcc53-138">在 Windows VM 的 OS 和資料磁碟機上停用加密。</span><span class="sxs-lookup"><span data-stu-id="fcc53-138">Disabling encryption on OS and data drives for Windows VMs.</span></span>
* <span data-ttu-id="fcc53-139">所有資源 （例如金鑰保存庫、 儲存體帳戶和 VM） 都必須在 hello 相同的 Azure 地區和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fcc53-139">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="fcc53-140">標準層 VM，例如 A、D、DS、G 及 GS 系列 VM。</span><span class="sxs-lookup"><span data-stu-id="fcc53-140">Standard tier VMs, such as A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="fcc53-141">磁碟加密目前不支援在下列案例的 hello:</span><span class="sxs-lookup"><span data-stu-id="fcc53-141">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="fcc53-142">基本層 VM。</span><span class="sxs-lookup"><span data-stu-id="fcc53-142">Basic tier VMs.</span></span>
* <span data-ttu-id="fcc53-143">使用 hello 傳統部署模型所建立的 Vm。</span><span class="sxs-lookup"><span data-stu-id="fcc53-143">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="fcc53-144">正在更新 hello 已加密的 VM 上的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="fcc53-144">Updating hello cryptographic keys on an already encrypted VM.</span></span>
* <span data-ttu-id="fcc53-145">與內部部署「金鑰管理服務」整合。</span><span class="sxs-lookup"><span data-stu-id="fcc53-145">Integration with on-prem Key Management Service.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="fcc53-146">建立 Azure Key Vault 和金鑰</span><span class="sxs-lookup"><span data-stu-id="fcc53-146">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="fcc53-147">開始之前，請確定 hello Azure PowerShell 模組已安裝該 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="fcc53-147">Before you start, make sure that hello latest version of hello Azure PowerShell module has been installed.</span></span> <span data-ttu-id="fcc53-148">如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="fcc53-148">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="fcc53-149">整個 hello 命令範例，所有範例參數都取代您自己的名稱、 位置和索引鍵的值。</span><span class="sxs-lookup"><span data-stu-id="fcc53-149">Throughout hello command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="fcc53-150">hello 下列範例會使用的慣例*myResourceGroup*， *myKeyVault*， *myVM*等等。</span><span class="sxs-lookup"><span data-stu-id="fcc53-150">hello following examples use a convention of *myResourceGroup*, *myKeyVault*, *myVM*, etc.</span></span>

<span data-ttu-id="fcc53-151">hello 第一個步驟是 toocreate Azure 金鑰保存庫 toostore 密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="fcc53-151">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="fcc53-152">Azure 金鑰保存庫可以儲存金鑰，密碼，或密碼，可讓您 toosecurely 它們實作中，您的應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="fcc53-152">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="fcc53-153">虛擬磁碟加密，您可以建立金鑰保存庫 toostore 使用的 tooencrypt 的密碼編譯金鑰或解密您的虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="fcc53-153">For virtual disk encryption, you create a Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span> 

<span data-ttu-id="fcc53-154">啟用 hello Azure 金鑰保存庫提供者與您 Azure 訂用帳戶內[暫存器 AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider)，然後建立的資源群組與[新增 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)。</span><span class="sxs-lookup"><span data-stu-id="fcc53-154">Enable hello Azure Key Vault provider within your Azure subscription with [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), then create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="fcc53-155">hello 下列範例會建立資源群組名稱*myResourceGroup*在 hello*美國東部*位置：</span><span class="sxs-lookup"><span data-stu-id="fcc53-155">hello following example creates a resource group name *myResourceGroup* in hello *East US* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

<span data-ttu-id="fcc53-156">hello Azure 金鑰保存庫包含 hello 密碼編譯金鑰與相關聯的計算資源，例如儲存體和 hello VM 本身必須位在 hello 相同的區域。</span><span class="sxs-lookup"><span data-stu-id="fcc53-156">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="fcc53-157">建立與 Azure 金鑰保存庫[新增 AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault)並啟用 hello 金鑰保存庫，磁碟加密搭配使用。</span><span class="sxs-lookup"><span data-stu-id="fcc53-157">Create an Azure Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="fcc53-158">針對 *keyVaultName* 指定一個唯一的 Key Vault 名稱，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="fcc53-158">Specify a unique Key Vault name for *keyVaultName* as follows:</span></span>

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

<span data-ttu-id="fcc53-159">您可以使用軟體或硬體安全性模型 (HSM) 保護功能來儲存密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="fcc53-159">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="fcc53-160">使用 HSM 時需要進階金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="fcc53-160">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="fcc53-161">沒有額外的成本 toocreating 高階金鑰保存庫，而不是標準儲存軟體保護金鑰的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="fcc53-161">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="fcc53-162">toocreate hello 前面步驟中的高階金鑰保存庫，新增 hello *-Sku 「 高階 」*參數。</span><span class="sxs-lookup"><span data-stu-id="fcc53-162">toocreate a premium Key Vault, in hello preceding step add hello *-Sku "Premium"* parameters.</span></span> <span data-ttu-id="fcc53-163">hello 下列範例會使用受軟體保護的金鑰因為我們建立標準的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="fcc53-163">hello following example uses software-protected keys since we created a standard Key Vault.</span></span> 

<span data-ttu-id="fcc53-164">這兩種保護模型中，hello Azure 平台必須 toobe hello VM 開機 toodecrypt hello 虛擬磁碟時，授與存取 toorequest hello 密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="fcc53-164">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="fcc53-165">請使用 [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) 在您的 Key Vault 中建立密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="fcc53-165">Create a cryptographic key in your Key Vault with [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span></span> <span data-ttu-id="fcc53-166">hello 下列範例會建立名為*myKey*:</span><span class="sxs-lookup"><span data-stu-id="fcc53-166">hello following example creates a key named *myKey*:</span></span>

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-hello-azure-active-directory-service-principal"></a><span data-ttu-id="fcc53-167">建立 hello Azure Active Directory 服務主體</span><span class="sxs-lookup"><span data-stu-id="fcc53-167">Create hello Azure Active Directory service principal</span></span>
<span data-ttu-id="fcc53-168">當虛擬磁碟加密或解密時，您可以指定帳戶 toohandle hello 驗證與金鑰保存庫中的密碼編譯金鑰交換。</span><span class="sxs-lookup"><span data-stu-id="fcc53-168">When virtual disks are encrypted or decrypted, you specify an account toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="fcc53-169">此帳戶時，Azure Active Directory 服務主體可讓 hello Azure 平台 toorequest hello 適當的密碼編譯金鑰代表 hello VM。</span><span class="sxs-lookup"><span data-stu-id="fcc53-169">This account, an Azure Active Directory service principal, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="fcc53-170">雖然許多組織都有專用的 Azure Active Directory 目錄，但您的訂用帳戶中會有預設 Azure Active Directory 執行個體。</span><span class="sxs-lookup"><span data-stu-id="fcc53-170">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="fcc53-171">請使用 [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) 在 Azure Active Directory 中建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="fcc53-171">Create a service principal in Azure Active Directory with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span></span> <span data-ttu-id="fcc53-172">toospecify 安全的密碼，請遵循 hello[中 Azure Active Directory 密碼原則和限制](../../active-directory/active-directory-passwords-policy.md):</span><span class="sxs-lookup"><span data-stu-id="fcc53-172">toospecify a secure password, follow hello [Password policies and restrictions in Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span></span>

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

<span data-ttu-id="fcc53-173">toosuccessfully 加密或解密虛擬磁碟，儲存在金鑰保存庫中的 hello 密碼編譯金鑰的權限必須是集 toopermit hello Azure Active Directory 服務主體 tooread hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="fcc53-173">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory service principal tooread hello keys.</span></span> <span data-ttu-id="fcc53-174">請使用 [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) 來設定 Key Vault 的權限：</span><span class="sxs-lookup"><span data-stu-id="fcc53-174">Set permissions on your Key Vault with [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a><span data-ttu-id="fcc53-175">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="fcc53-175">Create virtual machine</span></span>
<span data-ttu-id="fcc53-176">tootest hello 加密程序，讓我們來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="fcc53-176">tootest hello encryption process, let's create a VM.</span></span> <span data-ttu-id="fcc53-177">hello 下列範例會建立名為的 VM *myVM*使用*Windows Server 2016 Datacenter*映像：</span><span class="sxs-lookup"><span data-stu-id="fcc53-177">hello following example creates a VM named *myVM* using a *Windows Server 2016 Datacenter* image:</span></span>

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


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="fcc53-178">將虛擬機器加密</span><span class="sxs-lookup"><span data-stu-id="fcc53-178">Encrypt virtual machine</span></span>
<span data-ttu-id="fcc53-179">tooencrypt hello 虛擬磁碟，您將一起所有 hello 舊版元件：</span><span class="sxs-lookup"><span data-stu-id="fcc53-179">tooencrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="fcc53-180">指定 hello Azure Active Directory 服務主體和密碼。</span><span class="sxs-lookup"><span data-stu-id="fcc53-180">Specify hello Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="fcc53-181">指定 hello 金鑰保存庫 toostore hello 中繼資料的加密磁碟。</span><span class="sxs-lookup"><span data-stu-id="fcc53-181">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="fcc53-182">指定 hello hello 實際加密和解密的密碼編譯金鑰 toouse。</span><span class="sxs-lookup"><span data-stu-id="fcc53-182">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="fcc53-183">指定是否要 tooencrypt hello OS 磁碟、 hello 資料磁碟，或全部。</span><span class="sxs-lookup"><span data-stu-id="fcc53-183">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="fcc53-184">加密您的 VM 與[組 AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension)使用 hello Azure 金鑰保存庫金鑰和 Azure Active Directory 服務主體認證。</span><span class="sxs-lookup"><span data-stu-id="fcc53-184">Encrypt your VM with [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) using hello Azure Key Vault key and Azure Active Directory service principal credentials.</span></span> <span data-ttu-id="fcc53-185">hello 下列範例會擷取所有 hello 金鑰資訊然後加密 hello 名為 VM *myVM*:</span><span class="sxs-lookup"><span data-stu-id="fcc53-185">hello following example retrieves all hello key information then encrypts hello VM named *myVM*:</span></span>

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

<span data-ttu-id="fcc53-186">接受 hello 提示 toocontinue hello VM 加密。</span><span class="sxs-lookup"><span data-stu-id="fcc53-186">Accept hello prompt toocontinue with hello VM encryption.</span></span> <span data-ttu-id="fcc53-187">hello VM 重新啟動期間 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="fcc53-187">hello VM restarts during hello process.</span></span> <span data-ttu-id="fcc53-188">一旦 hello 加密程序完成且 hello VM 重新開機，檢閱與 hello 加密狀態[Get AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span><span class="sxs-lookup"><span data-stu-id="fcc53-188">Once hello encryption process completes and hello VM has rebooted, review hello encryption status with [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span></span>

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

<span data-ttu-id="fcc53-189">hello 輸出是 toohello 類似下列範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="fcc53-189">hello output is similar toohello following example:</span></span>

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a><span data-ttu-id="fcc53-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fcc53-190">Next steps</span></span>
* <span data-ttu-id="fcc53-191">如需有關管理 Azure Key Vault 的詳細資訊，請參閱[為虛擬機器設定 Key Vault](key-vault-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="fcc53-191">For more information about managing Azure Key Vault, see [Set up Key Vault for virtual machines](key-vault-setup.md).</span></span>
* <span data-ttu-id="fcc53-192">如需有關磁碟加密，例如準備的加密自訂 VM tooupload tooAzure，請參閱[Azure 磁碟加密](../../security/azure-security-disk-encryption.md)。</span><span class="sxs-lookup"><span data-stu-id="fcc53-192">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
