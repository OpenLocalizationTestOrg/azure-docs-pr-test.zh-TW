---
title: "CLI 指令碼範例-aaaAzure 部署 hello Load-Balanced 虛擬 Machin 規模集中的 LAMP 堆疊 |Microsoft 文件"
description: "使用自訂指令碼延伸 toodeploy hello LAMP 堆疊中的負載平衡的虛擬機器擴展集在 Azure 上的 =。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/05/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: d5278db809faaa0997a08b00a53387d754fce3d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a>部署負載平衡的虛擬機器規模集中的 hello LAMP 堆疊

這個範例會建立虛擬機器規模集，並套用 hello 規模集中的每部虛擬機器執行自訂指令碼 toodeploy hello LAMP 堆疊的擴充功能。

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>範例指令碼

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a>連線

使用此程式碼 toosee，tooconnect tooyour Vm 和您的小數位數的設定。

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access hello virtual machine scale set")]

## <a name="clean-up-deployment"></a>清除部署 

執行下列命令 tooremove hello 資源群組、 hello 擴展集 Vm，以及所有相關的資源的 hello。

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器、 可用性設定組中，負載平衡器和所有相關的資源的 hello。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 建立用來存放所有資源的資源群組。 |
| [az vmss create](https://docs.microsoft.com/cli/azure/vmss#create) | 建立虛擬機器擴展集 |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | 新增負載平衡端點 |
| [az vmss extension set](https://docs.microsoft.com/cli/azure/vmss/extension#set) | 建立 hello 自訂指令碼執行的 VM 部署的 hello 擴充功能 |
| [az vmss update-instances](https://docs.microsoft.com/cli/azure/vmss#update-instances) | 套用 hello 延伸模組之前，已部署的 hello VM 執行個體上執行自訂指令碼 hello toohello 規模集。 |
| [az vmss scale](https://docs.microsoft.com/cli/azure/vmss#scale) | 向上擴充 hello 標尺加入多個 VM 執行個體來設定。 這些執行 hello 自訂指令碼，在部署時。 |
| [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) | 取得 hello 的 hello hello 範例所建立的 Vm 的 IP 位址。 |
| [az network lb show](https://docs.microsoft.com/cli/azure/network/lb#show) | 取得 hello 前端及後端 hello 負載平衡器使用的通訊埠。 |

## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
