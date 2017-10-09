---
title: "aaaAzure CLI 指令碼範例-重新啟動 Vm |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 依標記和識別碼重新啟動 VM"
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
ms.date: 03/01/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: a1ae07bd1d2be906553bef817385a4a333a10eca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restart-vms"></a>重新啟動 VM

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

這個範例示範幾個方式 tooget 一些 Vm，然後重新啟動它們。

hello 第一次重新啟動 hello 資源群組中的所有 hello Vm。

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

hello 第二個取得 hello 標記 Vm 使用`az resouce list`和篩選 toohello 資源的 Vm，並重新啟動這些 Vm。

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

這個範例適用於 Bash 殼層。 在 Windows 用戶端上執行 Azure CLI 指令碼選項，請參閱[Windows 中執行 hello Azure CLI](../windows/cli-options.md)。


## <a name="sample-script"></a>範例指令碼

hello 範例具備三個指令碼。
hello 第一個佈建 hello 虛擬機器。
因此 hello 命令會傳回而不會等到上佈建每個 VM toobe，它會使用 hello 否等候選項。
hello 第二個等候 hello Vm toobe 完整佈建。
hello 第三個指令碼會重新啟動所有的 hello Vm 已佈建，然後只 hello 標記 Vm。

### <a name="provision-hello-vms"></a>佈建 Vm hello

此指令碼會建立資源群組，然後再建立三個 Vm toorestart。
其中兩部已加上標記。

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision hello VMs")]

### <a name="wait"></a>等候

此指令碼會檢查在 hello 每 20 秒，直到所有的三個 Vm 會佈建，或其中一個失敗 tooprovision 佈建狀態。

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for hello VMs toobe provisioned")]

### <a name="restart-hello-vms"></a>重新啟動 Vm hello

此指令碼以 hello 資源群組，重新啟動所有 hello Vm，然後重新都啟動只 hello 標記 Vm。

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a>清除部署 

Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組，Vm 和所有相關的資源。

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器、 可用性設定組中，負載平衡器和所有相關的資源的 hello。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 建立用來存放所有資源的資源群組。 |
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | 建立 hello 虛擬機器。  |
| [az vm list](https://docs.microsoft.com/cli/azure/vm#list) | 搭配`--query`tooensure hello Vm 佈建後再重新啟動，並再 tooget hello 識別碼 hello Vm toorestart 它們。 |
| [az resource list](https://docs.microsoft.com/cli/azure/vm#list) | 搭配`--query`tooget hello hello Vm 使用 hello 標記的識別碼。 |
| [az vm restart](https://docs.microsoft.com/cli/azure/vm#list) | Hello Vm 會重新啟動。 |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | 刪除資源群組，包括所有的巢狀資源。 |

## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
