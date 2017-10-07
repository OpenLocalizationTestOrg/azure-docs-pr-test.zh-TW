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
# <a name="encrypt-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="bf9bb-103">使用 Azure PowerShell 加密 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="bf9bb-103">Encrypt a Windows virtual machine with Azure PowerShell</span></span>

<span data-ttu-id="bf9bb-104">此指令碼會建立一個安全的 Azure Key Vault、加密金鑰、Azure Active Directory 服務主體，以及 Window 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="bf9bb-105">然後使用 hello 從金鑰保存庫和服務主體認證的加密金鑰來加密 hello VM。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-105">hello VM is then encrypted using hello encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="bf9bb-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="bf9bb-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "Encrypt VM disks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="bf9bb-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="bf9bb-107">Clean up deployment</span></span> 

<span data-ttu-id="bf9bb-108">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="bf9bb-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="bf9bb-109">Script explanation</span></span>

<span data-ttu-id="bf9bb-110">此指令碼會使用下列命令 toocreate hello 部署的 hello。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="bf9bb-111">Hello 資料表中的每個項目連結 toocommand 特定文件。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="bf9bb-112">命令</span><span class="sxs-lookup"><span data-stu-id="bf9bb-112">Command</span></span> | <span data-ttu-id="bf9bb-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="bf9bb-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bf9bb-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="bf9bb-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="bf9bb-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bf9bb-116">New-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="bf9bb-116">New-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/new-azurermkeyvault) | <span data-ttu-id="bf9bb-117">建立 Azure 金鑰保存庫 toostore 安全資料例如加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-117">Creates an Azure Key Vault toostore secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="bf9bb-118">Add-AzureKeyVaultKey</span><span class="sxs-lookup"><span data-stu-id="bf9bb-118">Add-AzureKeyVaultKey</span></span>](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) | <span data-ttu-id="bf9bb-119">在 Key Vault 中建立加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-119">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="bf9bb-120">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="bf9bb-120">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="bf9bb-121">建立 Azure Active Directory 服務主體 toosecurely 驗證與控制存取 tooencryption 金鑰。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-121">Creates an Azure Active Directory service principal toosecurely authenticate and control access tooencryption keys.</span></span> |
| [<span data-ttu-id="bf9bb-122">Set-AzureRmKeyVaultAccessPolicy</span><span class="sxs-lookup"><span data-stu-id="bf9bb-122">Set-AzureRmKeyVaultAccessPolicy</span></span>](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) | <span data-ttu-id="bf9bb-123">設定權限在 hello 金鑰保存庫 toogrant hello 服務主體存取 tooencryption 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-123">Sets permissions on hello Key Vault toogrant hello service principal access tooencryption keys.</span></span> |
| [<span data-ttu-id="bf9bb-124">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="bf9bb-124">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="bf9bb-125">建立子網路組態。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-125">Creates a subnet configuration.</span></span> <span data-ttu-id="bf9bb-126">此設定可搭配 hello 虛擬網路建立程序。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-126">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="bf9bb-127">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="bf9bb-127">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="bf9bb-128">建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-128">Creates a virtual network.</span></span> |
| [<span data-ttu-id="bf9bb-129">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="bf9bb-129">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="bf9bb-130">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-130">Creates a public IP address.</span></span> |
| [<span data-ttu-id="bf9bb-131">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="bf9bb-131">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="bf9bb-132">建立網路安全性群組規則組態。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-132">Creates a network security group rule configuration.</span></span> <span data-ttu-id="bf9bb-133">此設定時，使用的 toocreate NSG 規則建立 hello NSG。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-133">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="bf9bb-134">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="bf9bb-134">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="bf9bb-135">建立網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-135">Creates a network security group.</span></span> |
| [<span data-ttu-id="bf9bb-136">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="bf9bb-136">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="bf9bb-137">取得子網路資訊。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-137">Gets subnet information.</span></span> <span data-ttu-id="bf9bb-138">建立網路介面時會使用此資訊。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-138">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="bf9bb-139">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="bf9bb-139">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="bf9bb-140">建立網路介面。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-140">Creates a network interface.</span></span> |
| [<span data-ttu-id="bf9bb-141">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="bf9bb-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="bf9bb-142">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-142">Creates a VM configuration.</span></span> <span data-ttu-id="bf9bb-143">此組態包括 VM 名稱、作業系統和系統管理認證等資訊。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="bf9bb-144">在建立 VM 時，會使用 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-144">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="bf9bb-145">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="bf9bb-145">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="bf9bb-146">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-146">Create a virtual machine.</span></span> |
| [<span data-ttu-id="bf9bb-147">Get-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="bf9bb-147">Get-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/get-azurermkeyvault) | <span data-ttu-id="bf9bb-148">取得所需的 hello 金鑰保存庫的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="bf9bb-148">Gets required information on hello Key Vault</span></span> |
| [<span data-ttu-id="bf9bb-149">Set-AzureRmVMDiskEncryptionExtension</span><span class="sxs-lookup"><span data-stu-id="bf9bb-149">Set-AzureRmVMDiskEncryptionExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) | <span data-ttu-id="bf9bb-150">可讓 VM 使用 hello 服務主體認證和加密金鑰加密。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-150">Enables encryption on a VM using hello service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="bf9bb-151">Get-AzureRmVmDiskEncryptionStatus</span><span class="sxs-lookup"><span data-stu-id="bf9bb-151">Get-AzureRmVmDiskEncryptionStatus</span></span>](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) | <span data-ttu-id="bf9bb-152">顯示 hello hello VM 加密程序狀態。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-152">Shows hello status of hello VM encryption process.</span></span> |
| [<span data-ttu-id="bf9bb-153">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="bf9bb-153">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="bf9bb-154">移除資源群組及其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-154">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bf9bb-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bf9bb-155">Next steps</span></span>

<span data-ttu-id="bf9bb-156">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-156">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="bf9bb-157">其他虛擬機器的 PowerShell 指令碼範例可以在 hello [Azure Windows VM 文件](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="bf9bb-157">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
