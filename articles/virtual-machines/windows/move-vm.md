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
# <a name="move-a-windows-vm-tooanother-azure-subscription-or-resource-group"></a>Windows VM tooanother Azure 訂用帳戶或資源群組移動
本文將逐步引導您 toomove Windows VM 之間的資源群組或訂用帳戶。 訂用帳戶之間移動可以很方便，如果您最初個人的訂用帳戶中建立 VM，而現在想 toomove 它 tooyour 公司的訂用帳戶 toocontinue 您的工作。

> [!IMPORTANT]
>此時，您無法移動受控磁碟。 
>
>Hello 移動的一部分，會建立新的資源識別碼。 一旦 hello 已移動 VM，您需要 tooupdate 您工具和指令碼 toouse hello 新的資源 Id。 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-toomove-a-vm"></a>使用 Powershell toomove VM
toomove 虛擬機器 tooanother 資源群組，您需要 toomake 確定也移動所有 hello 相依資源。 toouse hello Move-azurermresource cmdlet，您需要 hello 資源名稱和 hello 資源類型。 您可以取得從 hello 尋找 AzureRMResource cmdlet。

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


toomove toomove 我們需要多個資源的 VM。 我們可以為每個資源建立不同的變數，然後加以列出。 這個範例包含大部分的 hello 基本資源針對 VM，但您可以加入更多視需要。

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

toomove hello 資源 toodifferent 訂用帳戶，包括 hello **-DestinationSubscriptionId**參數。 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



系統會詢問您想 toomove hello tooconfirm 指定資源。 型別**Y** tooconfirm 想 toomove hello 資源。

## <a name="next-steps"></a>後續步驟
您可以在資源群組和訂用帳戶之間移動許多不同類型的資源。 如需詳細資訊，請參閱[移動資源 toonew 資源群組或訂用帳戶](../../resource-group-move-resources.md)。    

