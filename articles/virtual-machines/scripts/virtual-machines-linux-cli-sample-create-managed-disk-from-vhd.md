---
title: "aaaAzure CLI 指令碼範例-從 hello 的儲存體帳戶的 VHD 檔案建立受管理的磁碟相同的訂用帳戶 |Microsoft 文件"
description: "Azure CLI 指令碼範例： 建立受管理的磁碟儲存體帳戶中 hello 的 VHD 檔案從相同訂用帳戶"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: 6cfb3c54a7692b0f3999c585861340c1a6b4d348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-hello-same-subscription-with-cli"></a><span data-ttu-id="7e460-103">從 VHD 檔案 hello 的儲存體帳戶中建立受管理的磁碟使用 CLI 的相同訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7e460-103">Create a managed disk from a VHD file in a storage account in hello same subscription with CLI</span></span>

<span data-ttu-id="7e460-104">此指令碼會建立受管理的磁碟儲存體帳戶中 hello 的 VHD 檔案從相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7e460-104">This script creates a managed disk from a VHD file in a storage account in hello same subscription.</span></span> <span data-ttu-id="7e460-105">使用此指令碼 tooimport 特製化 (無法一般化/執行過 sysprep) VHD toomanaged OS 磁碟 toocreate 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7e460-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD toomanaged OS disk toocreate a virtual machine.</span></span> <span data-ttu-id="7e460-106">或者，您也可以使用它 tooimport 資料 VHD toomanaged 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="7e460-106">Or, use it tooimport a data VHD toomanaged data disk.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="7e460-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="7e460-107">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="7e460-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="7e460-108">Script explanation</span></span>

<span data-ttu-id="7e460-109">此指令碼會使用下列命令 toocreate VHD 從受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="7e460-109">This script uses following commands toocreate a managed disk from a VHD.</span></span> <span data-ttu-id="7e460-110">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="7e460-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7e460-111">命令</span><span class="sxs-lookup"><span data-stu-id="7e460-111">Command</span></span> | <span data-ttu-id="7e460-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="7e460-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7e460-113">az disk create</span><span class="sxs-lookup"><span data-stu-id="7e460-113">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="7e460-114">建立受管理的磁碟在 hello 的儲存體帳戶中使用的 VHD URI 相同訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7e460-114">Creates a managed disk using URI of a VHD in a storage account in hello same subscription</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7e460-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7e460-115">Next steps</span></span>

[<span data-ttu-id="7e460-116">將受控磁碟連結為 OS 磁碟以建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="7e460-116">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="7e460-117">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="7e460-117">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7e460-118">其他虛擬機器和受管理的磁碟 CLI 指令碼範例可以在 hello [Azure Linux VM 文件](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="7e460-118">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
