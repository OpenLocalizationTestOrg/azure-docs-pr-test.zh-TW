---
title: "PowerShell 指令碼範例-aaaAzure 加密 Windows VM |Microsoft 文件"
description: "Azure PowerShell 指令碼範例 - 加密 Windows VM"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 80c52a0b734a52a051ed30026b294840fd521143
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-windows-virtual-machine-with-azure-powershell"></a>使用 Azure PowerShell 加密 Windows 虛擬機器

此指令碼會建立一個安全的 Azure Key Vault、加密金鑰、Azure Active Directory 服務主體，以及 Window 虛擬機器 (VM)。 然後使用 hello 從金鑰保存庫和服務主體認證的加密金鑰來加密 hello VM。

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "Encrypt VM disks")]

## <a name="clean-up-deployment"></a>清除部署 

執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate hello 部署的 hello。 Hello 資料表中的每個項目連結 toocommand 特定文件。

| 命令 | 注意事項 |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | 建立用來存放所有資源的資源群組。 |
| [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) | 建立 Azure 金鑰保存庫 toostore 安全資料例如加密金鑰。 |
| [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) | 在 Key Vault 中建立加密金鑰。 |
| [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | 建立 Azure Active Directory 服務主體 toosecurely 驗證與控制存取 tooencryption 金鑰。 |
| [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) | 設定權限在 hello 金鑰保存庫 toogrant hello 服務主體存取 tooencryption 索引鍵。 |
| [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | 建立子網路組態。 此設定可搭配 hello 虛擬網路建立程序。 |
| [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | 建立虛擬網路。 |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | 建立公用 IP 位址。 |
| [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | 建立網路安全性群組規則組態。 此設定時，使用的 toocreate NSG 規則建立 hello NSG。 |
| [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | 建立網路安全性群組。 |
| [Get-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | 取得子網路資訊。 建立網路介面時會使用此資訊。 |
| [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | 建立網路介面。 |
| [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) | 建立 VM 組態。 此組態包括 VM 名稱、作業系統和系統管理認證等資訊。 在建立 VM 時，會使用 hello 組態。 |
| [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | 建立虛擬機器。 |
| [Get-AzureRmKeyVault](/powershell/module/azurerm.keyvault/get-azurermkeyvault) | 取得所需的 hello 金鑰保存庫的詳細資訊 |
| [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) | 可讓 VM 使用 hello 服務主體認證和加密金鑰加密。 |
| [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) | 顯示 hello hello VM 加密程序狀態。 |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | 移除資源群組及其內含的所有資源。 |

## <a name="next-steps"></a>後續步驟

如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。

其他虛擬機器的 PowerShell 指令碼範例可以在 hello [Azure Windows VM 文件](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
