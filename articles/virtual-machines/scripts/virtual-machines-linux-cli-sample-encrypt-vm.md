---
title: "CLI 指令碼範例-aaaAzure 加密 Linux VM |Microsoft 文件"
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
ms.openlocfilehash: 1e455da4a8ea6d75b6d0d74b338d2e4d84973413
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="b5755-103">如何在 Azure 中將 Linux 虛擬機器加密</span><span class="sxs-lookup"><span data-stu-id="b5755-103">Encrypt a Linux virtual machine in Azure</span></span>

<span data-ttu-id="b5755-104">此指令碼會建立一個安全的 Azure Key Vault、加密金鑰、Azure Active Directory 服務主體，以及 Linux 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="b5755-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Linux virtual machine (VM).</span></span> <span data-ttu-id="b5755-105">然後使用 hello 從金鑰保存庫和服務主體認證的加密金鑰來加密 hello VM。</span><span class="sxs-lookup"><span data-stu-id="b5755-105">hello VM is then encrypted using hello encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b5755-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="b5755-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "Encrypt VM disks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b5755-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="b5755-107">Clean up deployment</span></span> 

<span data-ttu-id="b5755-108">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="b5755-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b5755-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="b5755-109">Script explanation</span></span>

<span data-ttu-id="b5755-110">此指令碼會使用下列命令 toocreate hello 資源群組中，Azure 金鑰保存庫、 服務主體，虛擬機器，以及所有相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="b5755-110">This script uses hello following commands toocreate a resource group, Azure Key Vault, service principal, virtual machine, and all related resources.</span></span> <span data-ttu-id="b5755-111">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="b5755-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b5755-112">命令</span><span class="sxs-lookup"><span data-stu-id="b5755-112">Command</span></span> | <span data-ttu-id="b5755-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="b5755-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b5755-114">az group create</span><span class="sxs-lookup"><span data-stu-id="b5755-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b5755-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="b5755-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b5755-116">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="b5755-116">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="b5755-117">建立 Azure 金鑰保存庫 toostore 安全資料例如加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="b5755-117">Creates an Azure Key Vault toostore secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="b5755-118">az keyvault key create</span><span class="sxs-lookup"><span data-stu-id="b5755-118">az keyvault key create</span></span>](https://docs.microsoft.com/cli/azure/keyvault/key#create) | <span data-ttu-id="b5755-119">在 Key Vault 中建立加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="b5755-119">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="b5755-120">az ad sp create-for-rbac</span><span class="sxs-lookup"><span data-stu-id="b5755-120">az ad sp create-for-rbac</span></span>](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | <span data-ttu-id="b5755-121">建立 Azure Active Directory 服務主體 toosecurely 驗證與控制存取 tooencryption 金鑰。</span><span class="sxs-lookup"><span data-stu-id="b5755-121">Creates an Azure Active Directory service principal toosecurely authenticate and control access tooencryption keys.</span></span> |
| [<span data-ttu-id="b5755-122">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="b5755-122">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="b5755-123">設定權限在 hello 金鑰保存庫 toogrant hello 服務主體存取 tooencryption 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b5755-123">Sets permissions on hello Key Vault toogrant hello service principal access tooencryption keys.</span></span> |
| [<span data-ttu-id="b5755-124">az vm create</span><span class="sxs-lookup"><span data-stu-id="b5755-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="b5755-125">建立 hello 虛擬機器，並將它連接 toohello 網路卡、 虛擬網路、 子網路和 NSG。</span><span class="sxs-lookup"><span data-stu-id="b5755-125">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="b5755-126">此命令也會指定使用，hello 虛擬機器映像 toobe 和系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="b5755-126">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="b5755-127">az vm encryption enable</span><span class="sxs-lookup"><span data-stu-id="b5755-127">az vm encryption enable</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | <span data-ttu-id="b5755-128">可讓 VM 使用 hello 服務主體認證和加密金鑰加密。</span><span class="sxs-lookup"><span data-stu-id="b5755-128">Enables encryption on a VM using hello service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="b5755-129">az vm encryption show</span><span class="sxs-lookup"><span data-stu-id="b5755-129">az vm encryption show</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#show) | <span data-ttu-id="b5755-130">顯示 hello hello VM 加密程序狀態。</span><span class="sxs-lookup"><span data-stu-id="b5755-130">Shows hello status of hello VM encryption process.</span></span> |
| [<span data-ttu-id="b5755-131">az group delete</span><span class="sxs-lookup"><span data-stu-id="b5755-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="b5755-132">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="b5755-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b5755-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b5755-133">Next steps</span></span>

<span data-ttu-id="b5755-134">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="b5755-134">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b5755-135">您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b5755-135">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
