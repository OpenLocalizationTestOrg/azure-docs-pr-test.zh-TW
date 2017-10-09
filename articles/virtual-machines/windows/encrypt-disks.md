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
# <a name="how-tooencrypt-virtual-disks-on-a-windows-vm"></a>如何在 Windows VM 上的 tooencrypt 虛擬磁碟
如需強化虛擬機器 (VM) 安全性與法規遵循，可以將 Azure 中的虛擬磁碟加密。 磁碟會使用 Azure 金鑰保存庫中受保護的密碼編譯金鑰進行加密。 您可控制這些密碼編譯金鑰，並可稽核其使用情況。 此發行項詳細資料時，如何使用 Azure PowerShell 的 Windows VM 上的 tooencrypt 虛擬磁碟。 您也可以[加密使用 Azure CLI 2.0 hello 的 Linux VM](../linux/encrypt-disks.md)。

## <a name="overview-of-disk-encryption"></a>磁碟加密概觀
加密 Windows VM 上的虛擬磁碟時，是在待用時使用 Bitlocker 進行加密。 將 Azure 中的虛擬磁碟加密完全免費。 密碼編譯金鑰會儲存在 Azure 金鑰保存庫使用軟體保護，或者您可以匯入或產生您的金鑰，在硬體安全性模組 (Hsm) 認證 tooFIPS 140-2 層級 2 標準。 這些密碼編譯金鑰會使用的 tooencrypt，並解密附加的 tooyour VM 虛擬磁碟。 您可保留這些密碼編譯金鑰的控制權，並可稽核其使用情況。 Azure Active Directory 服務主體會提供一個安全機制，以便在 VM 開機或關機時發出這些密碼編譯金鑰。

加密 VM hello 程序如下所示：

1. 在 Azure 金鑰保存庫中建立密碼編譯金鑰。
2. 設定 hello 密碼編譯金鑰 toobe 可用來加密磁碟。
3. tooread hello 密碼編譯金鑰從 hello Azure 金鑰保存庫，建立 Azure Active Directory 服務主體具有 hello 適當的權限。
4. 您的虛擬磁碟，指定 hello Azure Active Directory 服務主體 」 和 「 使用適當密碼編譯 toobe 發出 hello 命令 tooencrypt。
5. hello Azure Active Directory 服務主體要求 hello 必要的密碼編譯金鑰，從 Azure 金鑰保存庫。
6. hello 虛擬磁碟會使用提供的 hello 密碼編譯金鑰來加密。

## <a name="encryption-process"></a>加密程序
磁碟加密依賴 hello 下列額外的元件：

* **Azure 金鑰保存庫**-使用 toosafeguard 密碼編譯金鑰和 hello 磁碟加密/解密程序所使用的密碼。 
  * 如果有的話，您可以使用現有的 Azure 金鑰保存庫。 您沒有 toodedicate 金鑰保存庫 tooencrypting 磁碟。
  * 系統管理界限使用 tooseparate 和索引鍵的可見性，您可以建立專用的金鑰保存庫。
* **Azure Active Directory** -控點 hello 必要的密碼編譯金鑰的安全交換和驗證要求的動作。 
  * 您通常使用現有的 Azure Active Directory 執行個體來裝載您的應用程式。
  * 提供安全機制 toorequest hello 服務主體，並發出 hello 適當的密碼編譯金鑰。 您並未開發與 Azure Active Directory 整合的實際應用程式。

## <a name="requirements-and-limitations"></a>需求和限制
磁碟加密支援的案例和需求：

* 從 Azure Marketplace 映像或自訂 VHD 映像在新的 Windows VM 上啟用加密。
* 在 Azure 中現有的 Windows VM 上啟用加密。
* 在使用「儲存空間」來設定的 Windows VM 上啟用加密。
* 在 Windows VM 的 OS 和資料磁碟機上停用加密。
* 所有資源 （例如金鑰保存庫、 儲存體帳戶和 VM） 都必須在 hello 相同的 Azure 地區和訂用帳戶。
* 標準層 VM，例如 A、D、DS、G 及 GS 系列 VM。

磁碟加密目前不支援在下列案例的 hello:

* 基本層 VM。
* 使用 hello 傳統部署模型所建立的 Vm。
* 正在更新 hello 已加密的 VM 上的密碼編譯金鑰。
* 與內部部署「金鑰管理服務」整合。

## <a name="create-azure-key-vault-and-keys"></a>建立 Azure Key Vault 和金鑰
開始之前，請確定 hello Azure PowerShell 模組已安裝該 hello 最新版本。 如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。 整個 hello 命令範例，所有範例參數都取代您自己的名稱、 位置和索引鍵的值。 hello 下列範例會使用的慣例*myResourceGroup*， *myKeyVault*， *myVM*等等。

hello 第一個步驟是 toocreate Azure 金鑰保存庫 toostore 密碼編譯金鑰。 Azure 金鑰保存庫可以儲存金鑰，密碼，或密碼，可讓您 toosecurely 它們實作中，您的應用程式和服務。 虛擬磁碟加密，您可以建立金鑰保存庫 toostore 使用的 tooencrypt 的密碼編譯金鑰或解密您的虛擬磁碟。 

啟用 hello Azure 金鑰保存庫提供者與您 Azure 訂用帳戶內[暫存器 AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider)，然後建立的資源群組與[新增 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)。 hello 下列範例會建立資源群組名稱*myResourceGroup*在 hello*美國東部*位置：

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

hello Azure 金鑰保存庫包含 hello 密碼編譯金鑰與相關聯的計算資源，例如儲存體和 hello VM 本身必須位在 hello 相同的區域。 建立與 Azure 金鑰保存庫[新增 AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault)並啟用 hello 金鑰保存庫，磁碟加密搭配使用。 針對 *keyVaultName* 指定一個唯一的 Key Vault 名稱，如下所示︰

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

您可以使用軟體或硬體安全性模型 (HSM) 保護功能來儲存密碼編譯金鑰。 使用 HSM 時需要進階金鑰保存庫。 沒有額外的成本 toocreating 高階金鑰保存庫，而不是標準儲存軟體保護金鑰的金鑰保存庫。 toocreate hello 前面步驟中的高階金鑰保存庫，新增 hello *-Sku 「 高階 」*參數。 hello 下列範例會使用受軟體保護的金鑰因為我們建立標準的金鑰保存庫。 

這兩種保護模型中，hello Azure 平台必須 toobe hello VM 開機 toodecrypt hello 虛擬磁碟時，授與存取 toorequest hello 密碼編譯金鑰。 請使用 [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) 在您的 Key Vault 中建立密碼編譯金鑰。 hello 下列範例會建立名為*myKey*:

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-hello-azure-active-directory-service-principal"></a>建立 hello Azure Active Directory 服務主體
當虛擬磁碟加密或解密時，您可以指定帳戶 toohandle hello 驗證與金鑰保存庫中的密碼編譯金鑰交換。 此帳戶時，Azure Active Directory 服務主體可讓 hello Azure 平台 toorequest hello 適當的密碼編譯金鑰代表 hello VM。 雖然許多組織都有專用的 Azure Active Directory 目錄，但您的訂用帳戶中會有預設 Azure Active Directory 執行個體。

請使用 [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) 在 Azure Active Directory 中建立服務主體。 toospecify 安全的密碼，請遵循 hello[中 Azure Active Directory 密碼原則和限制](../../active-directory/active-directory-passwords-policy.md):

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

toosuccessfully 加密或解密虛擬磁碟，儲存在金鑰保存庫中的 hello 密碼編譯金鑰的權限必須是集 toopermit hello Azure Active Directory 服務主體 tooread hello 索引鍵。 請使用 [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) 來設定 Key Vault 的權限：

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a>Create virtual machine
tootest hello 加密程序，讓我們來建立 VM。 hello 下列範例會建立名為的 VM *myVM*使用*Windows Server 2016 Datacenter*映像：

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


## <a name="encrypt-virtual-machine"></a>將虛擬機器加密
tooencrypt hello 虛擬磁碟，您將一起所有 hello 舊版元件：

1. 指定 hello Azure Active Directory 服務主體和密碼。
2. 指定 hello 金鑰保存庫 toostore hello 中繼資料的加密磁碟。
3. 指定 hello hello 實際加密和解密的密碼編譯金鑰 toouse。
4. 指定是否要 tooencrypt hello OS 磁碟、 hello 資料磁碟，或全部。

加密您的 VM 與[組 AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension)使用 hello Azure 金鑰保存庫金鑰和 Azure Active Directory 服務主體認證。 hello 下列範例會擷取所有 hello 金鑰資訊然後加密 hello 名為 VM *myVM*:

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

接受 hello 提示 toocontinue hello VM 加密。 hello VM 重新啟動期間 hello 程序。 一旦 hello 加密程序完成且 hello VM 重新開機，檢閱與 hello 加密狀態[Get AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

hello 輸出是 toohello 類似下列範例程式碼：

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a>後續步驟
* 如需有關管理 Azure Key Vault 的詳細資訊，請參閱[為虛擬機器設定 Key Vault](key-vault-setup.md)。
* 如需有關磁碟加密，例如準備的加密自訂 VM tooupload tooAzure，請參閱[Azure 磁碟加密](../../security/azure-security-disk-encryption.md)。
