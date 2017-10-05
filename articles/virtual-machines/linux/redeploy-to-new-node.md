---
title: "在 Azure 中重新部署 Linux 虛擬機器 | Microsoft Docs"
description: "如何在 Azure 中重新部署 Linux 虛擬機器，以減輕 SSH 連線問題。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: e9530dd6-f5b0-4160-b36b-d75151d99eb7
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 7a8653a82775e718c38f65f246d997ba61f99d58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="redeploy-linux-virtual-machine-to-new-azure-node"></a><span data-ttu-id="1c099-103">將 Linux 虛擬機器重新部署至新的 Azure 節點</span><span class="sxs-lookup"><span data-stu-id="1c099-103">Redeploy Linux virtual machine to new Azure node</span></span>
<span data-ttu-id="1c099-104">如果您在 Azure 中進行對 Linux 虛擬機器 (VM) 的 SSH 或應用程式存取疑難排解時遇到問題，重新部署 VM 也許可以解決。</span><span class="sxs-lookup"><span data-stu-id="1c099-104">If you face difficulties troubleshooting SSH or application access to a Linux virtual machine (VM) in Azure, redeploying the VM may help.</span></span> <span data-ttu-id="1c099-105">重新部署 VM 時會將 VM 移到 Azure 基礎結構內的新節點，然後重新開啟它的電源。</span><span class="sxs-lookup"><span data-stu-id="1c099-105">When you redeploy a VM, it moves the VM to a new node within the Azure infrastructure and then powers it back on.</span></span> <span data-ttu-id="1c099-106">您所有組態選項和相關聯的資源都會加以保留。</span><span class="sxs-lookup"><span data-stu-id="1c099-106">All your configuration options and associated resources are retained.</span></span> <span data-ttu-id="1c099-107">本文將說明如何使用 Azure CLI 或 Azure 入口網站來重新部署 VM。</span><span class="sxs-lookup"><span data-stu-id="1c099-107">This article shows you how to redeploy a VM using Azure CLI or the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="1c099-108">重新部署 VM 之後，暫存磁碟會遺失，而系統會更新與虛擬網路介面關聯的動態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1c099-108">After you redeploy a VM, the temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 

<span data-ttu-id="1c099-109">您可以使用下列其中一個選項來重新部署 VM。</span><span class="sxs-lookup"><span data-stu-id="1c099-109">You can redeploy a VM using one of the following options.</span></span> <span data-ttu-id="1c099-110">您只需要選擇一個選項來重新部署 VM：</span><span class="sxs-lookup"><span data-stu-id="1c099-110">You only need to choose one option to redeploy your VM:</span></span>

- [<span data-ttu-id="1c099-111">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1c099-111">Azure CLI 2.0</span></span>](#azure-cli-20)
- [<span data-ttu-id="1c099-112">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1c099-112">Azure CLI 1.0</span></span>](#azure-cli-10)
- [<span data-ttu-id="1c099-113">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="1c099-113">Azure portal</span></span>](#using-azure-portal)

## <a name="use-the-azure-cli-20"></a><span data-ttu-id="1c099-114">使用 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1c099-114">Use the Azure CLI 2.0</span></span>
<span data-ttu-id="1c099-115">請安裝最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2) 並使用 [az login](/cli/azure/#login) 來登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1c099-115">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="1c099-116">使用 [az vm redeploy](/cli/azure/vm#redeploy) 來重新部署 VM。</span><span class="sxs-lookup"><span data-stu-id="1c099-116">Redeploy your VM with [az vm redeploy](/cli/azure/vm#redeploy).</span></span> <span data-ttu-id="1c099-117">下列範例會將名為 *myResourceGroup* 資源群組中名為 *myVM* 的 VM 重新部署：</span><span class="sxs-lookup"><span data-stu-id="1c099-117">The following example redeploys the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-the-azure-cli-10"></a><span data-ttu-id="1c099-118">使用 Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1c099-118">Use the Azure CLI 1.0</span></span>
<span data-ttu-id="1c099-119">安裝[最新的 Azure CLI 1.0](../../cli-install-nodejs.md)登入 Azure 帳戶，然後確定您處於 Resource Manager 模式 (`azure config mode arm`)。</span><span class="sxs-lookup"><span data-stu-id="1c099-119">Install the [latest Azure CLI 1.0](../../cli-install-nodejs.md), log in to an Azure account, and make sure that you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="1c099-120">下列範例會將名為 *myResourceGroup* 資源群組中名為 *myVM* 的 VM 重新部署：</span><span class="sxs-lookup"><span data-stu-id="1c099-120">The following example redeploys the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="1c099-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1c099-121">Next steps</span></span>
<span data-ttu-id="1c099-122">如果您在連接至 VM 時發生問題，您可以在[針對 SSH 連線進行疑難排解](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)或[詳細的 SSH 疑難排解步驟](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中找到具體的說明。</span><span class="sxs-lookup"><span data-stu-id="1c099-122">If you are having issues connecting to your VM, you can find specific help on [troubleshooting SSH connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [detailed SSH troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="1c099-123">如果無法存取在您 VM 上執行的應用程式，您也可以參閱[應用程式疑難排解問題](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1c099-123">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

