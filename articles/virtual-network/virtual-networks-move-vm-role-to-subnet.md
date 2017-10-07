---
title: "aaaMove （傳統） 的 VM 或雲端服務角色執行個體 tooa 不同子網路-Azure PowerShell |Microsoft 文件"
description: "深入了解如何 toomove Vm （傳統），以及雲端服務角色執行個體使用 PowerShell tooa 不同子網路。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: de4135c7-dc5b-4ffa-84cc-1b8364b7b427
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8d2de56f42a91be4a665414ea9641ffd46588fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-vm-classic-or-cloud-services-role-instance-tooa-different-subnet-using-powershell"></a>移動 VM （傳統） 或雲端服務角色執行個體 tooa 不同的子網路使用 PowerShell
您可以使用 PowerShell toomove Vm （傳統） 從一個子網路 tooanother hello 中相同的虛擬網路 (VNet)。 可以編輯 hello CSCFG 檔案，而不是使用 PowerShell 來移動角色執行個體。

> [!NOTE]
> 本文說明如何透過 hello 傳統部署模型只能部署 toomove Vm。
> 
> 

為什麼要移動 Vm tooanother 子網路？ 子網路移轉時，hello 較舊的子網路太小，而且不能展開到期 tooexisting 執行 Vm 子網路中。 在此情況下，您可以建立新的、 較大的子網路，然後移轉 hello Vm toohello 新的子網路，然後完成移轉之後，您可以刪除 hello 舊的空白子網路。

## <a name="how-toomove-a-vm-tooanother-subnet"></a>如何 toomove VM tooanother 子網路
toomove VM 執行 hello Set-azuresubnet PowerShell 指令程式，使用下面 hello 範例做為範本。 在 hello 下列範例中，我們要移動 TestVM 從其目前的子網路，tooSubnet-2。 為確定 tooedit hello 範例 tooreflect 您的環境。 請注意，每次您在程序執行 hello Update-azurevm cmdlet，它會重新啟動您的 VM hello 更新程序的一部分。

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

如果您為 VM 指定靜態內部私用 ip 位址，您就必須 tooclear 該設定之前您可以移動 hello VM tooa 新子網路。 在此情況下，使用下列 hello:

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="toomove-a-role-instance-tooanother-subnet"></a>toomove 角色執行個體 tooanother 子網路
toomove 角色執行個體中，編輯 hello CSCFG 檔案。 在 hello 下列範例中，我們要移動"Role0"虛擬網路中*VNETName*從其目前的子網路太*子網路 2*。 由於 hello 角色執行個體已部署，您將變更 hello 子網路名稱為 subnet-2。 為確定 tooedit hello 範例 tooreflect 您的環境。

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
