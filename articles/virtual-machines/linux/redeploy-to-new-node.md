---
title: "在 Azure 中 Linux 虛擬機器 aaaRedeploy |Microsoft 文件"
description: "如何 tooredeploy Linux 虛擬機器中 Azure toomitigate SSH 連線問題。"
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
ms.openlocfilehash: 9adfd1b11f262d362133366b2bba5e69c70c9b82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-linux-virtual-machine-toonew-azure-node"></a><span data-ttu-id="03d27-103">重新部署 Linux 虛擬機器 toonew Azure 節點</span><span class="sxs-lookup"><span data-stu-id="03d27-103">Redeploy Linux virtual machine toonew Azure node</span></span>
<span data-ttu-id="03d27-104">如果您遇到困難疑難排解 SSH 或應用程式在 Azure 中存取 tooa Linux 虛擬機器 (VM)，重新部署 hello VM 可能幫助。</span><span class="sxs-lookup"><span data-stu-id="03d27-104">If you face difficulties troubleshooting SSH or application access tooa Linux virtual machine (VM) in Azure, redeploying hello VM may help.</span></span> <span data-ttu-id="03d27-105">當您重新部署 VM 時，它會移 hello Azure 基礎結構中的 hello VM tooa 新節點，並再開啟它回到上的電源。</span><span class="sxs-lookup"><span data-stu-id="03d27-105">When you redeploy a VM, it moves hello VM tooa new node within hello Azure infrastructure and then powers it back on.</span></span> <span data-ttu-id="03d27-106">您所有組態選項和相關聯的資源都會加以保留。</span><span class="sxs-lookup"><span data-stu-id="03d27-106">All your configuration options and associated resources are retained.</span></span> <span data-ttu-id="03d27-107">本文章將示範如何使用 Azure CLI 或 hello Azure 入口網站的 VM 的 tooredeploy。</span><span class="sxs-lookup"><span data-stu-id="03d27-107">This article shows you how tooredeploy a VM using Azure CLI or hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="03d27-108">您重新部署 VM 之後，hello 暫存磁碟遺失，且會更新虛擬網路介面相關聯的動態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="03d27-108">After you redeploy a VM, hello temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 

<span data-ttu-id="03d27-109">您可以重新部署 VM，使用其中一種 hello 下列選項。</span><span class="sxs-lookup"><span data-stu-id="03d27-109">You can redeploy a VM using one of hello following options.</span></span> <span data-ttu-id="03d27-110">您只需要一個選項 tooredeploy toochoose VM:</span><span class="sxs-lookup"><span data-stu-id="03d27-110">You only need toochoose one option tooredeploy your VM:</span></span>

- [<span data-ttu-id="03d27-111">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="03d27-111">Azure CLI 2.0</span></span>](#azure-cli-20)
- [<span data-ttu-id="03d27-112">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="03d27-112">Azure CLI 1.0</span></span>](#azure-cli-10)
- [<span data-ttu-id="03d27-113">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="03d27-113">Azure portal</span></span>](#using-azure-portal)

## <a name="use-hello-azure-cli-20"></a><span data-ttu-id="03d27-114">使用 Azure CLI 2.0 hello</span><span class="sxs-lookup"><span data-stu-id="03d27-114">Use hello Azure CLI 2.0</span></span>
<span data-ttu-id="03d27-115">最新安裝 hello [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 帳戶使用登入和[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="03d27-115">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="03d27-116">使用 [az vm redeploy](/cli/azure/vm#redeploy) 來重新部署 VM。</span><span class="sxs-lookup"><span data-stu-id="03d27-116">Redeploy your VM with [az vm redeploy](/cli/azure/vm#redeploy).</span></span> <span data-ttu-id="03d27-117">下列範例重新部署的 hello hello 名為 VM *myVM* hello 資源群組中名為*myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="03d27-117">hello following example redeploys hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-hello-azure-cli-10"></a><span data-ttu-id="03d27-118">使用 Azure CLI 1.0 hello</span><span class="sxs-lookup"><span data-stu-id="03d27-118">Use hello Azure CLI 1.0</span></span>
<span data-ttu-id="03d27-119">安裝 hello[最新的 Azure CLI 1.0](../../cli-install-nodejs.md)，登入 tooan Azure 帳戶，並確定您是在 Resource Manager 模式 (`azure config mode arm`)。</span><span class="sxs-lookup"><span data-stu-id="03d27-119">Install hello [latest Azure CLI 1.0](../../cli-install-nodejs.md), log in tooan Azure account, and make sure that you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="03d27-120">下列範例重新部署的 hello hello 名為 VM *myVM* hello 資源群組中名為*myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="03d27-120">hello following example redeploys hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="03d27-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="03d27-121">Next steps</span></span>
<span data-ttu-id="03d27-122">如果您有連接 tooyour VM 的問題，您可以在找到特定說明[SSH 連接的疑難排解](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)或[詳細的疑難排解步驟的 SSH](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="03d27-122">If you are having issues connecting tooyour VM, you can find specific help on [troubleshooting SSH connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [detailed SSH troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="03d27-123">如果無法存取在您 VM 上執行的應用程式，您也可以參閱[應用程式疑難排解問題](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="03d27-123">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

