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
# <a name="move-a-linux-vm-tooanother-subscription-or-resource-group"></a>將 Linux VM tooanother 訂用帳戶或資源群組移動
本文將逐步引導您 toomove Linux VM 之間的資源群組或訂用帳戶。 訂用帳戶之間移動 VM 可以很方便，如果您個人的訂用帳戶中建立的 VM，而現在想 toomove 它 tooyour 公司的訂用帳戶。

> [!IMPORTANT]
>此時，您無法移動受控磁碟。 
>
>Hello 移動的一部分，會建立新的資源識別碼。 一旦 hello 已移動 VM，您需要 tooupdate 您工具和指令碼 toouse hello 新的資源 Id。 
> 
> 

## <a name="use-hello-azure-cli-toomove-a-vm"></a>使用 hello Azure CLI toomove VM
toosuccessfully 移動 VM，您需要 toomove hello VM 和其支援的所有資源。 使用 hello **azure 群組顯示**命令 toolist 所有 hello 與資源的資源群組及其 Id。 它可幫助 toopipe hello 輸出此命令 tooa 檔案，讓您可以複製並貼入更新版本的命令識別碼 hello。

    azure group show <resourceGroupName>

toomove VM 和其資源 tooanother 資源群組，使用 hello **azure 資源移動**CLI 命令。 hello 下列範例顯示如何 toomove VM 和 hello 最常見的資源需要。 我們使用 hello **-i**參數並以逗號分隔的清單 （不含空格） 的識別碼 hello 資源 toomove 傳入。

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

如果您想 toomove hello VM 和其資源 tooa 不同訂用帳戶、 新增 hello **-目的地 subscriptionId &#60; destinationSubscriptionID &#62;**參數 toospecify hello 目的地訂用帳戶。

如果您正在從 Windows 電腦上的 hello 命令提示字元中，您需要 tooadd  **$**  hello 變數名稱時將其宣告的前面。 在 Linux 中不需要這麼做。

系統會詢問您想 toomove hello tooconfirm 指定的資源。 型別**Y** tooconfirm 想 toomove hello 資源。

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a>後續步驟
您可以在資源群組和訂用帳戶之間移動許多不同類型的資源。 如需詳細資訊，請參閱[移動資源 toonew 資源群組或訂用帳戶](../../resource-group-move-resources.md)。    

