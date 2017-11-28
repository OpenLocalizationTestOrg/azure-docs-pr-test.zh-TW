---
title: "CLI 指令碼範例-aaaAzure 建立 VM 的 vhd |Microsoft 文件"
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
ms.openlocfilehash: ce39092697a51e4e8a8e59ba8eb919955f616458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a><span data-ttu-id="67ab4-103">使用虛擬硬碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="67ab4-103">Create a VM with a virtual hard disk</span></span>

<span data-ttu-id="67ab4-104">此範例會使用 VHD 建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="67ab4-104">This example creates a virtual machine using a VHD.</span></span>
<span data-ttu-id="67ab4-105">它會建立資源群組、 儲存體帳戶和容器，接著它會建立 VM 上傳 hello VHD toohello 容器。</span><span class="sxs-lookup"><span data-stu-id="67ab4-105">It creates a resource group, a storage account, and a container, then it creates a VM by uploading hello VHD toohello container.</span></span>
<span data-ttu-id="67ab4-106">它會取代 hello ssh 公開，所以您需要存取 toohello VM，您的公開金鑰與索引鍵。</span><span class="sxs-lookup"><span data-stu-id="67ab4-106">It replaces hello ssh public key with your public key so that you have access toohello VM.</span></span>

<span data-ttu-id="67ab4-107">您將需要可開機的 VHD。</span><span class="sxs-lookup"><span data-stu-id="67ab4-107">You'll need a bootable VHD.</span></span>
<span data-ttu-id="67ab4-108">您可以從 https://azclisamples.blob.core.windows.net/vhds/sample.vhd，下載 hello 我們使用的 VHD，或使用您自己的 VHD。</span><span class="sxs-lookup"><span data-stu-id="67ab4-108">You can download hello VHD that we used from https://azclisamples.blob.core.windows.net/vhds/sample.vhd, or use your own VHD.</span></span> <span data-ttu-id="67ab4-109">hello 指令碼會尋找`~/sample.vhd`。</span><span class="sxs-lookup"><span data-stu-id="67ab4-109">hello script looks for `~/sample.vhd`.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="67ab4-110">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="67ab4-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a><span data-ttu-id="67ab4-111">清除部署</span><span class="sxs-lookup"><span data-stu-id="67ab4-111">Clean up deployment</span></span> 

<span data-ttu-id="67ab4-112">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="67ab4-112">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a><span data-ttu-id="67ab4-113">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="67ab4-113">Script explanation</span></span>

<span data-ttu-id="67ab4-114">此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器、 可用性設定組中，負載平衡器和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="67ab4-114">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="67ab4-115">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="67ab4-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="67ab4-116">命令</span><span class="sxs-lookup"><span data-stu-id="67ab4-116">Command</span></span> | <span data-ttu-id="67ab4-117">注意事項</span><span class="sxs-lookup"><span data-stu-id="67ab4-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="67ab4-118">az group create</span><span class="sxs-lookup"><span data-stu-id="67ab4-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="67ab4-119">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="67ab4-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="67ab4-120">az storage account list</span><span class="sxs-lookup"><span data-stu-id="67ab4-120">az storage account list</span></span>](https://docs.microsoft.com/cli/azure/storage/account#list) | <span data-ttu-id="67ab4-121">列出儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="67ab4-121">Lists storage accounts</span></span> |
| [<span data-ttu-id="67ab4-122">az storage account check-name</span><span class="sxs-lookup"><span data-stu-id="67ab4-122">az storage account check-name</span></span>](https://docs.microsoft.com/cli/azure/storage/account#check-name) | <span data-ttu-id="67ab4-123">檢查儲存體帳戶名稱有效，而且該它尚不存在</span><span class="sxs-lookup"><span data-stu-id="67ab4-123">Checks that a storage account name is valid and that it doesn't already exist</span></span> |
| [<span data-ttu-id="67ab4-124">az storage account keys list</span><span class="sxs-lookup"><span data-stu-id="67ab4-124">az storage account keys list</span></span>](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | <span data-ttu-id="67ab4-125">列出 hello 儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="67ab4-125">Lists keys for hello storage accounts</span></span> |
| [<span data-ttu-id="67ab4-126">az storage blob exists</span><span class="sxs-lookup"><span data-stu-id="67ab4-126">az storage blob exists</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#exists) | <span data-ttu-id="67ab4-127">檢查 hello blob 是否存在</span><span class="sxs-lookup"><span data-stu-id="67ab4-127">Checks whether hello blob exists</span></span> |
| [<span data-ttu-id="67ab4-128">az storage container create</span><span class="sxs-lookup"><span data-stu-id="67ab4-128">az storage container create</span></span>](https://docs.microsoft.com/cli/azure/storage/container#create) | <span data-ttu-id="67ab4-129">在儲存體帳戶中建立容器。</span><span class="sxs-lookup"><span data-stu-id="67ab4-129">Creates a container in a storage account.</span></span> |
| [<span data-ttu-id="67ab4-130">az storage blob upload</span><span class="sxs-lookup"><span data-stu-id="67ab4-130">az storage blob upload</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#upload) | <span data-ttu-id="67ab4-131">正在上傳 hello VHD hello 容器中建立 blob。</span><span class="sxs-lookup"><span data-stu-id="67ab4-131">Creates a blob in hello container by uploading hello VHD.</span></span> |
| [<span data-ttu-id="67ab4-132">az vm list</span><span class="sxs-lookup"><span data-stu-id="67ab4-132">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="67ab4-133">搭配`--query`檢查 hello VM 名稱是否正在使用中。</span><span class="sxs-lookup"><span data-stu-id="67ab4-133">Used with `--query` check whether hello VM name is in use.</span></span> | 
| [<span data-ttu-id="67ab4-134">az vm create</span><span class="sxs-lookup"><span data-stu-id="67ab4-134">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="67ab4-135">建立 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="67ab4-135">Creates hello virtual machines.</span></span> |
| [<span data-ttu-id="67ab4-136">az vm access set-linux-user</span><span class="sxs-lookup"><span data-stu-id="67ab4-136">az vm access set-linux-user</span></span>](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | <span data-ttu-id="67ab4-137">重設 hello SSH 金鑰 toogive hello 目前使用者存取 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="67ab4-137">Resets hello SSH key toogive hello current user access toohello VM.</span></span> |
| [<span data-ttu-id="67ab4-138">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="67ab4-138">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="67ab4-139">取得 hello 的 hello 所建立的 VM 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="67ab4-139">Gets hello IP address of hello VM that was created.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="67ab4-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="67ab4-140">Next steps</span></span>

<span data-ttu-id="67ab4-141">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="67ab4-141">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="67ab4-142">您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="67ab4-142">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
