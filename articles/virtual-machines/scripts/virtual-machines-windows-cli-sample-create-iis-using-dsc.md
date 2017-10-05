---
title: "Azure CLI 指令碼範例 - 使用 DSC 建立具有 IIS 的 Windows Server 2016 VM | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 使用 DSC 建立具有 IIS 的 Windows Server 2016 VM"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.custom: mvc
ms.openlocfilehash: 1f605c0260fcaea29851d76c90ba0b287bec5ae7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-iis-using-dsc"></a><span data-ttu-id="c3037-103">使用 DSC 建立具有 IIS 的 VM</span><span class="sxs-lookup"><span data-stu-id="c3037-103">Create a VM with IIS using DSC</span></span>

<span data-ttu-id="c3037-104">此指令碼會建立虛擬機器，並使用 Azure 虛擬機器 DSC 自訂指令碼擴充功能來安裝及設定 IIS。</span><span class="sxs-lookup"><span data-stu-id="c3037-104">This script creates a virtual machine, and uses the Azure Virtual Machine DSC custom script extension to install and configure IIS.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c3037-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="c3037-105">Sample script</span></span>

<span data-ttu-id="c3037-106">[!code-azurecli-interactive[主要](../../../cli_scripts/virtual-machine/create-windows-iis-using-dsc/create-windows-iis-using-dsc.sh "快速建立 VM")]</span><span class="sxs-lookup"><span data-stu-id="c3037-106">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-windows-iis-using-dsc/create-windows-iis-using-dsc.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c3037-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="c3037-107">Clean up deployment</span></span> 

<span data-ttu-id="c3037-108">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="c3037-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="c3037-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="c3037-109">Script explanation</span></span>

<span data-ttu-id="c3037-110">此指令碼使用下列命令來建立資源群組、虛擬機器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="c3037-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="c3037-111">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="c3037-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c3037-112">命令</span><span class="sxs-lookup"><span data-stu-id="c3037-112">Command</span></span> | <span data-ttu-id="c3037-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="c3037-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c3037-114">az group create</span><span class="sxs-lookup"><span data-stu-id="c3037-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c3037-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c3037-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c3037-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="c3037-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="c3037-117">建立虛擬機器，並將它連線到網路卡、虛擬網路、子網路及 NSG。</span><span class="sxs-lookup"><span data-stu-id="c3037-117">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="c3037-118">此命令也會指定要使用的虛擬機器映像和管理認證。</span><span class="sxs-lookup"><span data-stu-id="c3037-118">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="c3037-119">az vm extension set</span><span class="sxs-lookup"><span data-stu-id="c3037-119">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="c3037-120">將自訂指令碼擴充功能新增至會叫用指令碼來安裝 IIS 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c3037-120">Add the Custom Script Extension to the virtual machine which invokes a script to install IIS.</span></span> |
| [<span data-ttu-id="c3037-121">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="c3037-121">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="c3037-122">建立網路安全性群組規則以允許輸入流量。</span><span class="sxs-lookup"><span data-stu-id="c3037-122">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="c3037-123">在此範例中，會開放連接埠 80 供 HTTP 流量使用。</span><span class="sxs-lookup"><span data-stu-id="c3037-123">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="c3037-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="c3037-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="c3037-125">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="c3037-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c3037-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c3037-126">Next steps</span></span>

<span data-ttu-id="c3037-127">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="c3037-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c3037-128">您可以在 [Azure Windows VM 文件](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中找到其他的虛擬機器 CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="c3037-128">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
