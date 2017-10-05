---
title: "Azure PowerShell 指令碼範例 - 加密 Windows VM | Microsoft Docs"
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
ms.openlocfilehash: 9279fea482fcd8716bcd996985e10f500a4775ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="e3ab3-103">使用 Azure PowerShell 加密 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="e3ab3-103">Encrypt a Windows virtual machine with Azure PowerShell</span></span>

<span data-ttu-id="e3ab3-104">此指令碼會建立一個安全的 Azure Key Vault、加密金鑰、Azure Active Directory 服務主體，以及 Window 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="e3ab3-105">然後會使用 Key Vault 中的加密金鑰和服務主體認證將 VM 加密。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-105">The VM is then encrypted using the encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e3ab3-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="e3ab3-106">Sample script</span></span>

<span data-ttu-id="e3ab3-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "加密 VM 磁碟")]</span><span class="sxs-lookup"><span data-stu-id="e3ab3-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "Encrypt VM disks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="e3ab3-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="e3ab3-108">Clean up deployment</span></span> 

<span data-ttu-id="e3ab3-109">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="e3ab3-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="e3ab3-110">Script explanation</span></span>

<span data-ttu-id="e3ab3-111">此指令碼會使用下列命令來建立部署。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="e3ab3-112">下表中的每個項目都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e3ab3-113">命令</span><span class="sxs-lookup"><span data-stu-id="e3ab3-113">Command</span></span> | <span data-ttu-id="e3ab3-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="e3ab3-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e3ab3-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e3ab3-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="e3ab3-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e3ab3-117">New-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="e3ab3-117">New-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/new-azurermkeyvault) | <span data-ttu-id="e3ab3-118">建立 Azure Key Vault 來儲存安全資料，例如加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-118">Creates an Azure Key Vault to store secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="e3ab3-119">Add-AzureKeyVaultKey</span><span class="sxs-lookup"><span data-stu-id="e3ab3-119">Add-AzureKeyVaultKey</span></span>](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) | <span data-ttu-id="e3ab3-120">在 Key Vault 中建立加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-120">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="e3ab3-121">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="e3ab3-121">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="e3ab3-122">建立 Azure Active Directory 服務主體，以安全地進行驗證及控制對加密金鑰的存取。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-122">Creates an Azure Active Directory service principal to securely authenticate and control access to encryption keys.</span></span> |
| [<span data-ttu-id="e3ab3-123">Set-AzureRmKeyVaultAccessPolicy</span><span class="sxs-lookup"><span data-stu-id="e3ab3-123">Set-AzureRmKeyVaultAccessPolicy</span></span>](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) | <span data-ttu-id="e3ab3-124">在 Key Vault 上設定權限，以授與服務主體對加密金鑰的存取權。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-124">Sets permissions on the Key Vault to grant the service principal access to encryption keys.</span></span> |
| [<span data-ttu-id="e3ab3-125">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="e3ab3-125">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="e3ab3-126">建立子網路組態。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-126">Creates a subnet configuration.</span></span> <span data-ttu-id="e3ab3-127">此組態可使用於虛擬網路建立程序。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-127">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="e3ab3-128">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="e3ab3-128">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="e3ab3-129">建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-129">Creates a virtual network.</span></span> |
| [<span data-ttu-id="e3ab3-130">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="e3ab3-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="e3ab3-131">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-131">Creates a public IP address.</span></span> |
| [<span data-ttu-id="e3ab3-132">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="e3ab3-132">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="e3ab3-133">建立網路安全性群組規則組態。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-133">Creates a network security group rule configuration.</span></span> <span data-ttu-id="e3ab3-134">建立 NSG 時，此組態用來建立 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-134">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="e3ab3-135">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="e3ab3-135">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="e3ab3-136">建立網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-136">Creates a network security group.</span></span> |
| [<span data-ttu-id="e3ab3-137">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="e3ab3-137">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="e3ab3-138">取得子網路資訊。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-138">Gets subnet information.</span></span> <span data-ttu-id="e3ab3-139">建立網路介面時會使用此資訊。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-139">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="e3ab3-140">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="e3ab3-140">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="e3ab3-141">建立網路介面。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-141">Creates a network interface.</span></span> |
| [<span data-ttu-id="e3ab3-142">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="e3ab3-142">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="e3ab3-143">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-143">Creates a VM configuration.</span></span> <span data-ttu-id="e3ab3-144">此組態包括 VM 名稱、作業系統和系統管理認證等資訊。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-144">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="e3ab3-145">建立 VM 時會使用此組態。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-145">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="e3ab3-146">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="e3ab3-146">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="e3ab3-147">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-147">Create a virtual machine.</span></span> |
| [<span data-ttu-id="e3ab3-148">Get-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="e3ab3-148">Get-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/get-azurermkeyvault) | <span data-ttu-id="e3ab3-149">取得 Key Vault 的必要資訊</span><span class="sxs-lookup"><span data-stu-id="e3ab3-149">Gets required information on the Key Vault</span></span> |
| [<span data-ttu-id="e3ab3-150">Set-AzureRmVMDiskEncryptionExtension</span><span class="sxs-lookup"><span data-stu-id="e3ab3-150">Set-AzureRmVMDiskEncryptionExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) | <span data-ttu-id="e3ab3-151">使用服務主體認證和加密金鑰在 VM 上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-151">Enables encryption on a VM using the service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="e3ab3-152">Get-AzureRmVmDiskEncryptionStatus</span><span class="sxs-lookup"><span data-stu-id="e3ab3-152">Get-AzureRmVmDiskEncryptionStatus</span></span>](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) | <span data-ttu-id="e3ab3-153">顯示 VM 加密程序的狀態。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-153">Shows the status of the VM encryption process.</span></span> |
| [<span data-ttu-id="e3ab3-154">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e3ab3-154">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="e3ab3-155">移除資源群組及其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-155">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e3ab3-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e3ab3-156">Next steps</span></span>

<span data-ttu-id="e3ab3-157">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-157">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e3ab3-158">您可以在 [Azure Windows VM 文件](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中找到其他的虛擬機器 PowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="e3ab3-158">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
