---
title: "在 Azure 中 Linux VM aaaMove |Microsoft 文件"
description: "移動 hello Resource Manager 部署模型中的 Linux VM tooanother Azure 訂用帳戶或資源群組。"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d635f0a5-4458-4b95-a5f8-eed4f41eb4d4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 938d04234059111912f03e72d14dabd338bc0678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-linux-vm-tooanother-subscription-or-resource-group"></a><span data-ttu-id="15a3c-103">將 Linux VM tooanother 訂用帳戶或資源群組移動</span><span class="sxs-lookup"><span data-stu-id="15a3c-103">Move a Linux VM tooanother subscription or resource group</span></span>
<span data-ttu-id="15a3c-104">本文將逐步引導您 toomove Linux VM 之間的資源群組或訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="15a3c-104">This article walks you through how toomove a Linux VM between resource groups or subscriptions.</span></span> <span data-ttu-id="15a3c-105">訂用帳戶之間移動 VM 可以很方便，如果您個人的訂用帳戶中建立的 VM，而現在想 toomove 它 tooyour 公司的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="15a3c-105">Moving a VM between subscriptions can be handy if you created a VM in a personal subscription and now want toomove it tooyour company's subscription.</span></span>

> [!IMPORTANT]
><span data-ttu-id="15a3c-106">此時，您無法移動受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="15a3c-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="15a3c-107">Hello 移動的一部分，會建立新的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="15a3c-107">New resource IDs are created as part of hello move.</span></span> <span data-ttu-id="15a3c-108">一旦 hello 已移動 VM，您需要 tooupdate 您工具和指令碼 toouse hello 新的資源 Id。</span><span class="sxs-lookup"><span data-stu-id="15a3c-108">Once hello VM has been moved, you need tooupdate your tools and scripts toouse hello new resource IDs.</span></span> 
> 
> 

## <a name="use-hello-azure-cli-toomove-a-vm"></a><span data-ttu-id="15a3c-109">使用 hello Azure CLI toomove VM</span><span class="sxs-lookup"><span data-stu-id="15a3c-109">Use hello Azure CLI toomove a VM</span></span>
<span data-ttu-id="15a3c-110">toosuccessfully 移動 VM，您需要 toomove hello VM 和其支援的所有資源。</span><span class="sxs-lookup"><span data-stu-id="15a3c-110">toosuccessfully move a VM, you need toomove hello VM and all its supporting resources.</span></span> <span data-ttu-id="15a3c-111">使用 hello **azure 群組顯示**命令 toolist 所有 hello 與資源的資源群組及其 Id。</span><span class="sxs-lookup"><span data-stu-id="15a3c-111">Use hello **azure group show** command toolist all hello resources in a resource group and their IDs.</span></span> <span data-ttu-id="15a3c-112">它可幫助 toopipe hello 輸出此命令 tooa 檔案，讓您可以複製並貼入更新版本的命令識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="15a3c-112">It helps toopipe hello output of this command tooa file so you can copy and paste hello IDs into later commands.</span></span>

    azure group show <resourceGroupName>

<span data-ttu-id="15a3c-113">toomove VM 和其資源 tooanother 資源群組，使用 hello **azure 資源移動**CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="15a3c-113">toomove a VM and its resources tooanother resource group, use hello **azure resource move** CLI command.</span></span> <span data-ttu-id="15a3c-114">hello 下列範例顯示如何 toomove VM 和 hello 最常見的資源需要。</span><span class="sxs-lookup"><span data-stu-id="15a3c-114">hello following example shows how toomove a VM and hello most common resources it requires.</span></span> <span data-ttu-id="15a3c-115">我們使用 hello **-i**參數並以逗號分隔的清單 （不含空格） 的識別碼 hello 資源 toomove 傳入。</span><span class="sxs-lookup"><span data-stu-id="15a3c-115">We use hello **-i** parameter and pass in a comma-separated list (without spaces) of IDs for hello resources toomove.</span></span>

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

<span data-ttu-id="15a3c-116">如果您想 toomove hello VM 和其資源 tooa 不同訂用帳戶、 新增 hello **-目的地 subscriptionId &#60; destinationSubscriptionID &#62;**參數 toospecify hello 目的地訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="15a3c-116">If you want toomove hello VM and its resources tooa different subscription, add hello **--destination-subscriptionId &#60;destinationSubscriptionID&#62;** parameter toospecify hello destination subscription.</span></span>

<span data-ttu-id="15a3c-117">如果您正在從 Windows 電腦上的 hello 命令提示字元中，您需要 tooadd  **$**  hello 變數名稱時將其宣告的前面。</span><span class="sxs-lookup"><span data-stu-id="15a3c-117">If you are working from hello Command Prompt on a Windows computer, you need tooadd a **$** in front of hello variable names when you declare them.</span></span> <span data-ttu-id="15a3c-118">在 Linux 中不需要這麼做。</span><span class="sxs-lookup"><span data-stu-id="15a3c-118">This isn't needed in Linux.</span></span>

<span data-ttu-id="15a3c-119">系統會詢問您想 toomove hello tooconfirm 指定的資源。</span><span class="sxs-lookup"><span data-stu-id="15a3c-119">You are asked tooconfirm that you want toomove hello specified resource.</span></span> <span data-ttu-id="15a3c-120">型別**Y** tooconfirm 想 toomove hello 資源。</span><span class="sxs-lookup"><span data-stu-id="15a3c-120">Type **Y** tooconfirm that you want toomove hello resources.</span></span>

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="15a3c-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="15a3c-121">Next steps</span></span>
<span data-ttu-id="15a3c-122">您可以在資源群組和訂用帳戶之間移動許多不同類型的資源。</span><span class="sxs-lookup"><span data-stu-id="15a3c-122">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="15a3c-123">如需詳細資訊，請參閱[移動資源 toonew 資源群組或訂用帳戶](../../resource-group-move-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="15a3c-123">For more information, see [Move resources toonew resource group or subscription](../../resource-group-move-resources.md).</span></span>    

