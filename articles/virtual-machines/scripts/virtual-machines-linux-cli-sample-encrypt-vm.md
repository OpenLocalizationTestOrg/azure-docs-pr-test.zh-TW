---
title: "Azure CLI 指令碼範例 - 將 Linux VM 加密 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 將 Linux VM 加密"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 9388bce04e37d049301521f808cd8494c327e335
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="38081-103">如何在 Azure 中將 Linux 虛擬機器加密</span><span class="sxs-lookup"><span data-stu-id="38081-103">Encrypt a Linux virtual machine in Azure</span></span>

<span data-ttu-id="38081-104">此指令碼會建立一個安全的 Azure Key Vault、加密金鑰、Azure Active Directory 服務主體，以及 Linux 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="38081-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Linux virtual machine (VM).</span></span> <span data-ttu-id="38081-105">然後會使用 Key Vault 中的加密金鑰和服務主體認證將 VM 加密。</span><span class="sxs-lookup"><span data-stu-id="38081-105">The VM is then encrypted using the encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="38081-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="38081-106">Sample script</span></span>

<span data-ttu-id="38081-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "加密 VM 磁碟")]</span><span class="sxs-lookup"><span data-stu-id="38081-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "Encrypt VM disks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="38081-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="38081-108">Clean up deployment</span></span> 

<span data-ttu-id="38081-109">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="38081-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="38081-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="38081-110">Script explanation</span></span>

<span data-ttu-id="38081-111">此指令碼會使用下列命令來建立資源群組、Azure Key Vault、服務主體、虛擬機器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="38081-111">This script uses the following commands to create a resource group, Azure Key Vault, service principal, virtual machine, and all related resources.</span></span> <span data-ttu-id="38081-112">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="38081-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="38081-113">命令</span><span class="sxs-lookup"><span data-stu-id="38081-113">Command</span></span> | <span data-ttu-id="38081-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="38081-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="38081-115">az group create</span><span class="sxs-lookup"><span data-stu-id="38081-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="38081-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="38081-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="38081-117">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="38081-117">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="38081-118">建立 Azure Key Vault 來儲存安全資料，例如加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="38081-118">Creates an Azure Key Vault to store secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="38081-119">az keyvault key create</span><span class="sxs-lookup"><span data-stu-id="38081-119">az keyvault key create</span></span>](https://docs.microsoft.com/cli/azure/keyvault/key#create) | <span data-ttu-id="38081-120">在 Key Vault 中建立加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="38081-120">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="38081-121">az ad sp create-for-rbac</span><span class="sxs-lookup"><span data-stu-id="38081-121">az ad sp create-for-rbac</span></span>](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | <span data-ttu-id="38081-122">建立 Azure Active Directory 服務主體，以安全地進行驗證及控制對加密金鑰的存取。</span><span class="sxs-lookup"><span data-stu-id="38081-122">Creates an Azure Active Directory service principal to securely authenticate and control access to encryption keys.</span></span> |
| [<span data-ttu-id="38081-123">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="38081-123">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="38081-124">在 Key Vault 上設定權限，以授與服務主體對加密金鑰的存取權。</span><span class="sxs-lookup"><span data-stu-id="38081-124">Sets permissions on the Key Vault to grant the service principal access to encryption keys.</span></span> |
| [<span data-ttu-id="38081-125">az vm create</span><span class="sxs-lookup"><span data-stu-id="38081-125">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="38081-126">建立虛擬機器，並將它連線到網路卡、虛擬網路、子網路及 NSG。</span><span class="sxs-lookup"><span data-stu-id="38081-126">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="38081-127">此命令也會指定要使用的虛擬機器映像和管理認證。</span><span class="sxs-lookup"><span data-stu-id="38081-127">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="38081-128">az vm encryption enable</span><span class="sxs-lookup"><span data-stu-id="38081-128">az vm encryption enable</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | <span data-ttu-id="38081-129">使用服務主體認證和加密金鑰在 VM 上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="38081-129">Enables encryption on a VM using the service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="38081-130">az vm encryption show</span><span class="sxs-lookup"><span data-stu-id="38081-130">az vm encryption show</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#show) | <span data-ttu-id="38081-131">顯示 VM 加密程序的狀態。</span><span class="sxs-lookup"><span data-stu-id="38081-131">Shows the status of the VM encryption process.</span></span> |
| [<span data-ttu-id="38081-132">az group delete</span><span class="sxs-lookup"><span data-stu-id="38081-132">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="38081-133">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="38081-133">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="38081-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="38081-134">Next steps</span></span>

<span data-ttu-id="38081-135">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="38081-135">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="38081-136">您可以在 [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中找到其他的虛擬機器 CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="38081-136">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
