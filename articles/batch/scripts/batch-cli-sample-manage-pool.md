---
title: "aaaAzure CLI 指令碼範例的批次中的 管理集區 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 管理 Batch 中的集區"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 6c9ca9515565aff42752231a080943be8e4c810b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a>使用 Azure CLI 管理 Azure Batch 集區

這些指令碼示範一些可用的 hello Azure CLI toocreate hello 工具和管理集區的 hello Azure 批次服務中的運算節點。

> [!NOTE]
> 在此範例中的 hello 命令會建立 Azure 虛擬機器。 執行中 Vm 會累算費用 tooyour 帳戶。 toominimize 費用，刪除 hello Vm 一旦您完成時執行的 hello 範例。 請參閱[清除集區](#clean-up-pools)。

有兩種方式可以設定 Batch 集區，即使用雲端服務組態 (僅限 Windows) 或虛擬機器組態 (Windows 和 Linux)。 下列的 hello 範例指令碼會顯示 toocreate 這兩種設定使用的集區。

## <a name="prerequisites"></a>必要條件

- 安裝 hello Azure CLI 使用 hello 中提供的 hello 指示[Azure CLI 安裝指南](https://docs.microsoft.com/cli/azure/install-azure-cli)，如果您有不這麼做。
- 建立 Batch 帳戶 (如果您還沒有帳戶的話)。 請參閱[建立 Batch 帳戶以 hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account)建立帳戶的範例指令碼。
- 如果您尚未尚未這麼做，請設定應用程式 toorun，從啟動工作。 請參閱[加入應用程式 tooAzure 批次使用 Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application)所建立的應用程式，並上傳應用程式封裝 tooAzure 的範例指令碼。

## <a name="pool-with-cloud-service-configuration-sample-script"></a>使用雲端服務組態範例指令碼的集區

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a>使用虛擬機器組態範例指令碼的集區

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a>清除集區

執行上述範例指令碼的 hello 之後，執行下列命令 toodelete hello 集區的 hello。
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate hello 和操作批次集區。
Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | 對 Batch 帳戶進行驗證。  |
| [az batch application summary list](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | 列出可用的應用程式 hello hello 批次帳戶中。  |
| [az batch pool create](https://docs.microsoft.com/cli/azure/batch/pool#create) | 建立 VM 集區。  |
| [az batch pool set](https://docs.microsoft.com/cli/azure/batch/pool#set) | 更新集區的屬性。  |
| [az batch pool node-agent-skus list](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | 列出可用的節點代理程式 SKU 和映像資訊。  |
| [az batch pool resize](https://docs.microsoft.com/cli/azure/batch/pool#resize) | 集區指定的執行中 hello Vm 的調整大小 hello 數目。  |
| [az batch pool show](https://docs.microsoft.com/cli/azure/batch/pool#show) | 顯示 hello 屬性集區。  |
| [az batch pool delete](https://docs.microsoft.com/cli/azure/batch/pool#delete) | 刪除指定的 hello 集區。  |
| [az batch pool autoscale enable](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | 在集區啟用自動調整規模並套用公式。  |
| [az batch pool autoscale disable](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | 在集區停用自動調整規模。  |
| [az batch node list](https://docs.microsoft.com/cli/azure/batch/node#list) | 列出所有在 hello hello 計算節點指定集區。  |
| [az batch node reboot](https://docs.microsoft.com/cli/azure/batch/node#reboot) | 重新啟動 hello 指定的運算節點。  |
| [az batch node delete](https://docs.microsoft.com/cli/azure/batch/node#delete) | 刪除列出的 hello 節點從 hello 指定集區。  |

## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

其他批次 CLI 指令碼範例可以在 hello [Azure 批次 CLI 文件](../batch-cli-samples.md)。

