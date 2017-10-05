---
title: "移動 Azure 中的 Linux VM | Microsoft Docs"
description: "在 Resource Manager 部署模型中將 Linux VM 移至另一個 Azure 訂用帳戶或資源群組。"
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
ms.openlocfilehash: 4695a9c934f97f2b2d448c4990e7ad5533e38e9f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="move-a-linux-vm-to-another-subscription-or-resource-group"></a><span data-ttu-id="8f9a3-103">將 Linux VM 移至另一個訂用帳戶或資源群組</span><span class="sxs-lookup"><span data-stu-id="8f9a3-103">Move a Linux VM to another subscription or resource group</span></span>
<span data-ttu-id="8f9a3-104">本文將逐步引導您了解如何在資源群組或訂用帳戶之間移動 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="8f9a3-104">This article walks you through how to move a Linux VM between resource groups or subscriptions.</span></span> <span data-ttu-id="8f9a3-105">如果您在個人訂用帳戶中建立了 VM，而現在想要將它移至您的公司訂用帳戶以繼續工作，在訂用帳戶之間移動 VM 會很方便。</span><span class="sxs-lookup"><span data-stu-id="8f9a3-105">Moving a VM between subscriptions can be handy if you created a VM in a personal subscription and now want to move it to your company's subscription.</span></span>

> [!IMPORTANT]
><span data-ttu-id="8f9a3-106">此時，您無法移動受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="8f9a3-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="8f9a3-107">移動過程中會建立新的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="8f9a3-107">New resource IDs are created as part of the move.</span></span> <span data-ttu-id="8f9a3-108">移動 VM 之後，您必須更新工具和指令碼以使用新的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="8f9a3-108">Once the VM has been moved, you need to update your tools and scripts to use the new resource IDs.</span></span> 
> 
> 

## <a name="use-the-azure-cli-to-move-a-vm"></a><span data-ttu-id="8f9a3-109">使用 Azure CLI 移動 VM</span><span class="sxs-lookup"><span data-stu-id="8f9a3-109">Use the Azure CLI to move a VM</span></span>
<span data-ttu-id="8f9a3-110">若要成功移動 VM，您需要移動 VM 及其所有支援的資源。</span><span class="sxs-lookup"><span data-stu-id="8f9a3-110">To successfully move a VM, you need to move the VM and all its supporting resources.</span></span> <span data-ttu-id="8f9a3-111">使用 **azure group show** 命令來列出資源群組中的所有資源及其識別碼。</span><span class="sxs-lookup"><span data-stu-id="8f9a3-111">Use the **azure group show** command to list all the resources in a resource group and their IDs.</span></span> <span data-ttu-id="8f9a3-112">它有助於將此命令的輸出透過管線送至檔案，以便您將識別碼複製並貼到稍後的命令中。</span><span class="sxs-lookup"><span data-stu-id="8f9a3-112">It helps to pipe the output of this command to a file so you can copy and paste the IDs into later commands.</span></span>

    azure group show <resourceGroupName>

<span data-ttu-id="8f9a3-113">若要將 VM 與其資源移到另一個資源群組，請使用 **azure resource move** CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="8f9a3-113">To move a VM and its resources to another resource group, use the **azure resource move** CLI command.</span></span> <span data-ttu-id="8f9a3-114">下列範例說明如何移動 VM 與其所需的大多數常見資源。</span><span class="sxs-lookup"><span data-stu-id="8f9a3-114">The following example shows how to move a VM and the most common resources it requires.</span></span> <span data-ttu-id="8f9a3-115">我們使用 **-i** 參數，並針對要移動的資源傳入以逗號分隔的識別碼清單 (不含空格)。</span><span class="sxs-lookup"><span data-stu-id="8f9a3-115">We use the **-i** parameter and pass in a comma-separated list (without spaces) of IDs for the resources to move.</span></span>

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

<span data-ttu-id="8f9a3-116">如果您想要將 VM 及其資源移至不同的訂用帳戶，請加入 **--destination-subscriptionId &#60;destinationSubscriptionID&#62;** 參數以指定目的地訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8f9a3-116">If you want to move the VM and its resources to a different subscription, add the **--destination-subscriptionId &#60;destinationSubscriptionID&#62;** parameter to specify the destination subscription.</span></span>

<span data-ttu-id="8f9a3-117">如果您從 Windows 電腦的命令提示字元作業，您必須於宣告變數名稱時在其前面加上 **$** 。</span><span class="sxs-lookup"><span data-stu-id="8f9a3-117">If you are working from the Command Prompt on a Windows computer, you need to add a **$** in front of the variable names when you declare them.</span></span> <span data-ttu-id="8f9a3-118">在 Linux 中不需要這麼做。</span><span class="sxs-lookup"><span data-stu-id="8f9a3-118">This isn't needed in Linux.</span></span>

<span data-ttu-id="8f9a3-119">系統會要求您確認您想要移動指定的資源。</span><span class="sxs-lookup"><span data-stu-id="8f9a3-119">You are asked to confirm that you want to move the specified resource.</span></span> <span data-ttu-id="8f9a3-120">輸入 **Y** 確認您要移除資源。</span><span class="sxs-lookup"><span data-stu-id="8f9a3-120">Type **Y** to confirm that you want to move the resources.</span></span>

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="8f9a3-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8f9a3-121">Next steps</span></span>
<span data-ttu-id="8f9a3-122">您可以在資源群組和訂用帳戶之間移動許多不同類型的資源。</span><span class="sxs-lookup"><span data-stu-id="8f9a3-122">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="8f9a3-123">如需詳細資訊，請參閱 [將資源移動到新的資源群組或訂用帳戶](../../resource-group-move-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="8f9a3-123">For more information, see [Move resources to new resource group or subscription](../../resource-group-move-resources.md).</span></span>    

