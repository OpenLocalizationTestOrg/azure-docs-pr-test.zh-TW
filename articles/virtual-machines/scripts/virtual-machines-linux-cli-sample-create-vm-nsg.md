---
title: "aaaAzure CLI 指令碼範例-建立兩個 Vm 的內部和外部 NSG |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 建立兩個分別具有內部和外部 NSG 的 VM"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ba6a70200ca2923369e37b13531bd7ca65b05a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a>保護虛擬機器之間的網路流量

此指令碼會建立兩個虛擬機器及保護在連入流量 tooboth。 其中一個虛擬機器可以存取 hello 網際網路以及網路安全性群組 (NSG) 設定 tooallow 流量通訊埠 22 和連接埠 80 上。 hello 第二個虛擬機器不能存取在 hello 網際網路，並已設定的 NSG tooonly 允許從 hello 第一部虛擬機器的流量。 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a>清除部署 

執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器的 hello 和所有相關聯的資源。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 建立用來存放所有資源的資源群組。 |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) | 建立 Azure 虛擬網路和子網路。 |
| [az network vnet subnet create](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | 建立子網路。 |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | 建立 hello 虛擬機器，並將它連接 toohello 網路卡、 虛擬網路、 子網路和 NSG。 此命令也會指定使用，hello 虛擬機器映像 toobe 和系統管理認證。  |
| [az network nsg rule list](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | 傳回網路安全性群組規則的相關資訊。 在此範例中，hello 規則名稱會儲存在變數中以便稍後在 hello 指令碼中使用。 |
| [az network nsg rule update](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | 更新 NSG 規則。 在此範例中，hello 後端規則是更新的 toopass 只能從 hello 前端子網路的流量通過。 |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | 刪除資源群組，包括所有的巢狀資源。 |

## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
