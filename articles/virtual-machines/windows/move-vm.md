---
title: "在 Azure 中的 Windows VM 資源 aaaMove |Microsoft 文件"
description: "移動 hello Resource Manager 部署模型中的 Windows VM tooanother Azure 訂用帳戶或資源群組。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 859e78dce9acf1168780d4ee8e9f6dac0e3c11cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-tooanother-azure-subscription-or-resource-group"></a><span data-ttu-id="df09b-103">Windows VM tooanother Azure 訂用帳戶或資源群組移動</span><span class="sxs-lookup"><span data-stu-id="df09b-103">Move a Windows VM tooanother Azure subscription or resource group</span></span>
<span data-ttu-id="df09b-104">本文將逐步引導您 toomove Windows VM 之間的資源群組或訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="df09b-104">This article walks you through how toomove a Windows VM between resource groups or subscriptions.</span></span> <span data-ttu-id="df09b-105">訂用帳戶之間移動可以很方便，如果您最初個人的訂用帳戶中建立 VM，而現在想 toomove 它 tooyour 公司的訂用帳戶 toocontinue 您的工作。</span><span class="sxs-lookup"><span data-stu-id="df09b-105">Moving between subscriptions can be handy if you originally created a VM in a personal subscription and now want toomove it tooyour company's subscription toocontinue your work.</span></span>

> [!IMPORTANT]
><span data-ttu-id="df09b-106">此時，您無法移動受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="df09b-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="df09b-107">Hello 移動的一部分，會建立新的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="df09b-107">New resource IDs are created as part of hello move.</span></span> <span data-ttu-id="df09b-108">一旦 hello 已移動 VM，您需要 tooupdate 您工具和指令碼 toouse hello 新的資源 Id。</span><span class="sxs-lookup"><span data-stu-id="df09b-108">Once hello VM has been moved, you need tooupdate your tools and scripts toouse hello new resource IDs.</span></span> 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-toomove-a-vm"></a><span data-ttu-id="df09b-109">使用 Powershell toomove VM</span><span class="sxs-lookup"><span data-stu-id="df09b-109">Use Powershell toomove a VM</span></span>
<span data-ttu-id="df09b-110">toomove 虛擬機器 tooanother 資源群組，您需要 toomake 確定也移動所有 hello 相依資源。</span><span class="sxs-lookup"><span data-stu-id="df09b-110">toomove a virtual machine tooanother resource group, you need toomake sure that you also move all of hello dependent resources.</span></span> <span data-ttu-id="df09b-111">toouse hello Move-azurermresource cmdlet，您需要 hello 資源名稱和 hello 資源類型。</span><span class="sxs-lookup"><span data-stu-id="df09b-111">toouse hello Move-AzureRMResource cmdlet, you need hello resource name and hello type of resource.</span></span> <span data-ttu-id="df09b-112">您可以取得從 hello 尋找 AzureRMResource cmdlet。</span><span class="sxs-lookup"><span data-stu-id="df09b-112">You can get both from hello Find-AzureRMResource cmdlet.</span></span>

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


<span data-ttu-id="df09b-113">toomove toomove 我們需要多個資源的 VM。</span><span class="sxs-lookup"><span data-stu-id="df09b-113">toomove a VM we need toomove multiple resources.</span></span> <span data-ttu-id="df09b-114">我們可以為每個資源建立不同的變數，然後加以列出。</span><span class="sxs-lookup"><span data-stu-id="df09b-114">We can just create separate variables for each resource and then list them.</span></span> <span data-ttu-id="df09b-115">這個範例包含大部分的 hello 基本資源針對 VM，但您可以加入更多視需要。</span><span class="sxs-lookup"><span data-stu-id="df09b-115">This example includes most of hello basic resources for a VM, but you can add more as needed.</span></span>

    $sourceRG = "<sourceResourceGroupName>"
    $destinationRG = "<destinationResourceGroupName>"

    $vm = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Compute/virtualMachines" -ResourceName "<vmName>"
    $storageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<storageAccountName>"
    $diagStorageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<diagnosticStorageAccountName>"
    $vNet = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/virtualNetworks" -ResourceName "<vNetName>"
    $nic = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkInterfaces" -ResourceName "<nicName>"
    $ip = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/publicIPAddresses" -ResourceName "<ipName>"
    $nsg = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkSecurityGroups" -ResourceName "<nsgName>"

    Move-AzureRmResource -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId

<span data-ttu-id="df09b-116">toomove hello 資源 toodifferent 訂用帳戶，包括 hello **-DestinationSubscriptionId**參數。</span><span class="sxs-lookup"><span data-stu-id="df09b-116">toomove hello resources toodifferent subscription, include hello **-DestinationSubscriptionId** parameter.</span></span> 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



<span data-ttu-id="df09b-117">系統會詢問您想 toomove hello tooconfirm 指定資源。</span><span class="sxs-lookup"><span data-stu-id="df09b-117">You will be asked tooconfirm that you want toomove hello specified resources.</span></span> <span data-ttu-id="df09b-118">型別**Y** tooconfirm 想 toomove hello 資源。</span><span class="sxs-lookup"><span data-stu-id="df09b-118">Type **Y** tooconfirm that you want toomove hello resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df09b-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="df09b-119">Next steps</span></span>
<span data-ttu-id="df09b-120">您可以在資源群組和訂用帳戶之間移動許多不同類型的資源。</span><span class="sxs-lookup"><span data-stu-id="df09b-120">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="df09b-121">如需詳細資訊，請參閱[移動資源 toonew 資源群組或訂用帳戶](../../resource-group-move-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="df09b-121">For more information, see [Move resources toonew resource group or subscription](../../resource-group-move-resources.md).</span></span>    

