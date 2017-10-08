---
title: "CLI 指令碼範例的批次執行作業 aaaAzure |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 使用 Batch 執行工作"
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
ms.openlocfilehash: f73a7cb341e550fd1c92f92201e20b27fa20d238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a>在 Azure Batch 上使用 Azure CLI 執行工作

此指令碼建立批次作業，並將一系列的工作 toohello 作業。 它也會示範如何 toomonitor 的作業，且其工作。 最後，它會顯示如何 tooquery hello 批次服務有效率地 hello 作業 」 工作的相關資訊。

## <a name="prerequisites"></a>必要條件

- 安裝 hello Azure CLI 使用 hello 中提供的 hello 指示[Azure CLI 安裝指南](https://docs.microsoft.com/cli/azure/install-azure-cli)，如果您有不這麼做。
- 建立 Batch 帳戶 (如果您還沒有帳戶的話)。 請參閱[建立 Batch 帳戶以 hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account)建立帳戶的範例指令碼。
- 如果您尚未尚未這麼做，請設定應用程式 toorun，從啟動工作。 請參閱[加入應用程式 tooAzure 批次使用 Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application)所建立的應用程式，並上傳應用程式封裝 tooAzure 的範例指令碼。
- 設定哪些 hello 將執行作業的集區。 如需指令碼範例以使用雲端服務組態或虛擬機器組態來建立集區，請參閱[使用 Azure CLI 管理 Azure Batch 集區](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool)。

## <a name="sample-script"></a>範例指令碼

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a>清除工作

執行 hello 上面的範例指令碼之後，執行下列命令 tooremove hello 的工作及所有的工作。 請注意，hello 集區必須另外刪除 toobe。 如需建立和刪除集區的詳細資訊，請參閱[使用 Azure CLI 管理 Azure Batch 集區](./batch-cli-sample-manage-pool.md)。

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate hello 批次工作和工作。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | 對 Batch 帳戶進行驗證。  |
| [az batch job create](https://docs.microsoft.com/cli/azure/batch/job#create) | 建立 Batch 工作。  |
| [az batch job set](https://docs.microsoft.com/cli/azure/batch/job#set) | 更新 Batch 工作的屬性。  |
| [az batch job show](https://docs.microsoft.com/cli/azure/batch/job#show) | 擷取指定的 Batch 工作的詳細資料。  |
| [az batch task create](https://docs.microsoft.com/cli/azure/batch/task#create) | 新增工作 toohello 指定批次作業。  |
| [az batch task show](https://docs.microsoft.com/cli/azure/batch/task#show) | 擷取 hello hello 工作詳細資料指定批次作業。  |
| [az batch task list](https://docs.microsoft.com/cli/azure/batch/task#list) | 列出 hello 與 hello 指定作業相關聯的工作。  |

## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

其他批次 CLI 指令碼範例可以在 hello [Azure 批次 CLI 文件](../batch-cli-samples.md)。
