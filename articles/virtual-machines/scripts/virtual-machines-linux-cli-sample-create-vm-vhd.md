---
title: "Azure CLI 指令碼範例 - 使用 VHD 建立 VM | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 使用虛擬硬碟建立 VM。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/09/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: fab65296a552c1839522c5254a868a3dc96227f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a><span data-ttu-id="6945c-103">使用虛擬硬碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="6945c-103">Create a VM with a virtual hard disk</span></span>

<span data-ttu-id="6945c-104">此範例會使用 VHD 建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6945c-104">This example creates a virtual machine using a VHD.</span></span>
<span data-ttu-id="6945c-105">它會建立資源群組、儲存體帳戶和容器，然後透過將 VHD 上傳至容器來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="6945c-105">It creates a resource group, a storage account, and a container, then it creates a VM by uploading the VHD to the container.</span></span>
<span data-ttu-id="6945c-106">它會將 SSH 公用金鑰以公開金鑰取代，使得您可以存取 VM。</span><span class="sxs-lookup"><span data-stu-id="6945c-106">It replaces the ssh public key with your public key so that you have access to the VM.</span></span>

<span data-ttu-id="6945c-107">您將需要可開機的 VHD。</span><span class="sxs-lookup"><span data-stu-id="6945c-107">You'll need a bootable VHD.</span></span>
<span data-ttu-id="6945c-108">您可以從 https://azclisamples.blob.core.windows.net/vhds/sample.vhd 下載我們使用的 VHD，或使用您自己的 VHD。</span><span class="sxs-lookup"><span data-stu-id="6945c-108">You can download the VHD that we used from https://azclisamples.blob.core.windows.net/vhds/sample.vhd, or use your own VHD.</span></span> <span data-ttu-id="6945c-109">指令碼會尋找 `~/sample.vhd`。</span><span class="sxs-lookup"><span data-stu-id="6945c-109">The script looks for `~/sample.vhd`.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6945c-110">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="6945c-110">Sample script</span></span>

<span data-ttu-id="6945c-111">[!code-azurecli-interactive[主要](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "使用 VHD 建立 VM")]</span><span class="sxs-lookup"><span data-stu-id="6945c-111">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6945c-112">清除部署</span><span class="sxs-lookup"><span data-stu-id="6945c-112">Clean up deployment</span></span> 

<span data-ttu-id="6945c-113">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="6945c-113">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a><span data-ttu-id="6945c-114">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="6945c-114">Script explanation</span></span>

<span data-ttu-id="6945c-115">此指令碼使用下列命令來建立資源群組、虛擬機器、可用性設定組、負載平衡器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="6945c-115">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="6945c-116">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="6945c-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6945c-117">命令</span><span class="sxs-lookup"><span data-stu-id="6945c-117">Command</span></span> | <span data-ttu-id="6945c-118">注意事項</span><span class="sxs-lookup"><span data-stu-id="6945c-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6945c-119">az group create</span><span class="sxs-lookup"><span data-stu-id="6945c-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6945c-120">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6945c-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6945c-121">az storage account list</span><span class="sxs-lookup"><span data-stu-id="6945c-121">az storage account list</span></span>](https://docs.microsoft.com/cli/azure/storage/account#list) | <span data-ttu-id="6945c-122">列出儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="6945c-122">Lists storage accounts</span></span> |
| [<span data-ttu-id="6945c-123">az storage account check-name</span><span class="sxs-lookup"><span data-stu-id="6945c-123">az storage account check-name</span></span>](https://docs.microsoft.com/cli/azure/storage/account#check-name) | <span data-ttu-id="6945c-124">檢查儲存體帳戶名稱有效，而且該它尚不存在</span><span class="sxs-lookup"><span data-stu-id="6945c-124">Checks that a storage account name is valid and that it doesn't already exist</span></span> |
| [<span data-ttu-id="6945c-125">az storage account keys list</span><span class="sxs-lookup"><span data-stu-id="6945c-125">az storage account keys list</span></span>](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | <span data-ttu-id="6945c-126">列出儲存體帳戶的金鑰</span><span class="sxs-lookup"><span data-stu-id="6945c-126">Lists keys for the storage accounts</span></span> |
| [<span data-ttu-id="6945c-127">az storage blob exists</span><span class="sxs-lookup"><span data-stu-id="6945c-127">az storage blob exists</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#exists) | <span data-ttu-id="6945c-128">檢查 blob 是否存在</span><span class="sxs-lookup"><span data-stu-id="6945c-128">Checks whether the blob exists</span></span> |
| [<span data-ttu-id="6945c-129">az storage container create</span><span class="sxs-lookup"><span data-stu-id="6945c-129">az storage container create</span></span>](https://docs.microsoft.com/cli/azure/storage/container#create) | <span data-ttu-id="6945c-130">在儲存體帳戶中建立容器。</span><span class="sxs-lookup"><span data-stu-id="6945c-130">Creates a container in a storage account.</span></span> |
| [<span data-ttu-id="6945c-131">az storage blob upload</span><span class="sxs-lookup"><span data-stu-id="6945c-131">az storage blob upload</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#upload) | <span data-ttu-id="6945c-132">透過上傳 VHD 在容器中建立 blob。</span><span class="sxs-lookup"><span data-stu-id="6945c-132">Creates a blob in the container by uploading the VHD.</span></span> |
| [<span data-ttu-id="6945c-133">az vm list</span><span class="sxs-lookup"><span data-stu-id="6945c-133">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="6945c-134">搭配 `--query` 可檢查 VM 名稱是否正在使用中。</span><span class="sxs-lookup"><span data-stu-id="6945c-134">Used with `--query` check whether the VM name is in use.</span></span> | 
| [<span data-ttu-id="6945c-135">az vm create</span><span class="sxs-lookup"><span data-stu-id="6945c-135">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="6945c-136">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6945c-136">Creates the virtual machines.</span></span> |
| [<span data-ttu-id="6945c-137">az vm access set-linux-user</span><span class="sxs-lookup"><span data-stu-id="6945c-137">az vm access set-linux-user</span></span>](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | <span data-ttu-id="6945c-138">重設 SSH 金鑰以授與目前使用者對 VM 的存取。</span><span class="sxs-lookup"><span data-stu-id="6945c-138">Resets the SSH key to give the current user access to the VM.</span></span> |
| [<span data-ttu-id="6945c-139">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="6945c-139">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="6945c-140">取得所建立 VM 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6945c-140">Gets the IP address of the VM that was created.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6945c-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6945c-141">Next steps</span></span>

<span data-ttu-id="6945c-142">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="6945c-142">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6945c-143">您可以在 [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中找到其他的虛擬機器 CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="6945c-143">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
