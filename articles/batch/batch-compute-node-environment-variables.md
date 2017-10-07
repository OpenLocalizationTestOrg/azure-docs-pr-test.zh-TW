---
title: "aaa\"Azure Batch 計算節點環境變數 |Microsoft 文件 」"
description: "Azure Batch 分析的計算節點環境變數參考。"
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/05/2017
ms.author: tamram
ms.openlocfilehash: 860f34b530579a81fbd5cf8ffa31df79d917c080
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-compute-node-environment-variables"></a>Azure Batch 計算節點環境變數
hello [Azure 批次服務](https://azure.microsoft.com/services/batch/)設定 hello 計算節點上下列環境變數。 您可以參考這些環境變數，工作的命令列或 hello 程式和指令碼 hello 命令列方式執行。

如需有關將環境變數搭配 Batch 使用的詳細資訊，請參閱[工作的環境設定](https://docs.microsoft.com/azure/batch/batch-api-basics#environment-settings-for-tasks)。

## <a name="environment-variable-visibility"></a>環境變數可見性

這些環境變數是可見的只在 hello 內容中的 hello**工作使用者**，hello hello 執行工作時的節點上的使用者帳戶。 您將*不*看到這些，如果您[遠端連線](https://azure.microsoft.com/documentation/articles/batch-api-basics/#connecting-to-compute-nodes)tooa 計算節點，可透過遠端桌面通訊協定 (RDP) 或安全殼層 (SSH) 和清單 hello 環境變數。 這是因為 hello 遠端連線所使用的使用者帳戶不是 hello 與 hello hello 工作會使用的帳戶相同。

## <a name="command-line-expansion-of-environment-variables"></a>環境變數的命令列擴充功能

hello 命令列上工作來執行計算節點才會執行下一個殼層。 因此，這些命令列無法原生利用殼層功能，例如環境變數擴充 (這包括 hello `PATH`)。 tootake 利用這類功能，您必須**叫用 hello 殼層**hello 命令列中。 例如，在 Windows 計算節點上啟動 `cmd.exe`，或在 Linux 節點上啟動 `/bin/sh`：

`cmd /c MyTaskApplication.exe %MY_ENV_VAR%`

`/bin/sh -c MyTaskApplication $MY_ENV_VAR`

## <a name="environment-variables"></a>環境變數

| 變數名稱                     | 說明                                                              | Availability | 範例 |
|-----------------------------------|--------------------------------------------------------------------------|--------------|---------|
| AZ_BATCH_ACCOUNT_NAME           | 所屬 hello hello hello 工作的批次帳戶名稱。                  | 所有工作。   | mybatchaccount |
| AZ_BATCH_CERTIFICATES_DIR       | Hello 內的目錄[工作的工作目錄][ files_dirs]中的憑證會儲存適用於 Linux 的計算節點。 請注意這個環境變數不會套用 tooWindows 計算節點。                                                  | 所有工作。   |  /mnt/batch/tasks/workitems/batchjob001/job-1/task001/certs |
| AZ_BATCH_JOB_ID                 | 所屬的 hello hello 工作的 hello 作業識別碼。 | 啟動工作之外的所有工作。 | batchjob001 |
| AZ_BATCH_JOB_PREP_DIR           | hello 的完整路徑的 hello 作業準備[工作目錄][ files_dirs] hello 節點上。 | 啟動工作與作業準備工作之外的所有工作。 只有 hello 工作設定與作業準備工作。 | C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation |
| AZ_BATCH_JOB_PREP_WORKING_DIR   | hello 的完整路徑的 hello 作業準備[工作的工作目錄][ files_dirs] hello 節點上。 | 啟動工作與作業準備工作之外的所有工作。 只有 hello 工作設定與作業準備工作。 | C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation\wd |
| AZ_BATCH_NODE_ID                | hello hello 節點的 hello 工作識別碼被指派給。 | 所有工作。 | tvm-1219235766_3-20160919t172711z |
| AZ_BATCH_NODE_ROOT_DIR          | hello 的完整路徑的所有 hello 根[批次目錄][ files_dirs] hello 節點上。 | 所有工作。 | C:\user\tasks |
| AZ_BATCH_NODE_SHARED_DIR        | hello 的完整路徑的 hello[共用的目錄][ files_dirs] hello 節點上。 所有節點執行的工作都有讀取/寫入存取 toothis 目錄。 在其他節點執行的工作不需要遠端存取 toothis 目錄 （它不是 「 共用 」 的網路目錄）。 | 所有工作。 | C:\user\tasks\shared |
| AZ_BATCH_NODE_STARTUP_DIR       | hello 的完整路徑的 hello[啟動工作目錄][ files_dirs] hello 節點上。 | 所有工作。 | C:\user\tasks\startup |
| AZ_BATCH_POOL_ID                | hello 識別碼 hello hello 工作的集區上執行。 | 所有工作。 | batchpool001 |
| AZ_BATCH_TASK_DIR               | hello 的完整路徑的 hello[工作目錄][ files_dirs] hello 節點上。 此目錄包含 hello`stdout.txt`和`stderr.txt`hello 工作和 hello AZ_BATCH_TASK_WORKING_DIR。 | 所有工作。 | C:\user\tasks\workitems\batchjob001\job-1\task001 |
| AZ_BATCH_TASK_ID                | hello 識別碼 hello 目前的工作。 | 啟動工作之外的所有工作。 | task001 |
| AZ_BATCH_TASK_WORKING_DIR       | hello 的完整路徑的 hello[工作的工作目錄][ files_dirs] hello 節點上。 目前正在執行工作的 hello 都有讀/寫存取 toothis 目錄。 | 所有工作。 | C:\user\tasks\workitems\batchjob001\job-1\task001\wd |
| CCP_NODES                       | hello 清單的節點和每個節點配置 tooa 的核心數目[多重執行個體工作][multi_instance]。 節點與核心會列在 hello 格式`numNodes<space>node1IP<space>node1Cores<space>`<br/>`node2IP<space>node2Cores<space> ...`其中 hello 節點數目後面接著一個或多個節點的 IP 位址以及 hello 核心數目每個。 |  多重執行個體的主要工作和子工作。 |`2 10.0.0.4 1 10.0.0.5 1` |
| AZ_BATCH_NODE_LIST              | 節點配置 tooa hello 清單[多重執行個體工作][ multi_instance] hello 格式`nodeIP;nodeIP`。 | 多重執行個體的主要工作和子工作。 | `10.0.0.4;10.0.0.5` |
| AZ_BATCH_HOST_LIST              | 節點配置 tooa hello 清單[多重執行個體工作][ multi_instance] hello 格式`nodeIP,nodeIP`。 | 多重執行個體的主要工作和子工作。 | `10.0.0.4,10.0.0.5` |
| AZ_BATCH_MASTER_NODE            | hello IP 位址和連接埠 hello 計算節點上的 hello 主要工作就是[多重執行個體工作][ multi_instance]執行。 | 多重執行個體的主要工作和子工作。 | `10.0.0.4:6000`|
| AZ_BATCH_TASK_SHARED_DIR | Hello 主要工作和每個項目子任務的完全相同的目錄路徑[多重執行個體工作][multi_instance]。 hello 路徑存在哪些 hello 多重執行個體工作執行時，在每個節點上且可讀取/寫入存取 toohello 該節點上執行的工作命令 (這兩個 hello[協調命令][ coord_cmd]和 hello [應用程式命令][app_cmd])。 子工作或在其他節點執行的主要工作不需要遠端存取 toothis 目錄 （它不是 「 共用 」 的網路目錄）。 | 多重執行個體的主要工作和子工作。 | C:\user\tasks\workitems\multiinstancesamplejob\job-1\multiinstancesampletask |
| AZ_BATCH_IS_CURRENT_NODE_MASTER | 指定 hello 目前節點是否為 hello 主要節點[多重執行個體工作][multi_instance]。 可能的值為 `true` 與 `false`。| 多重執行個體的主要工作和子工作。 | `true` |
| AZ_BATCH_NODE_IS_DEDICATED | 如果`true`，hello 目前節點是一個專用的節點。 若為 `false`，它就是[低優先順序節點](batch-low-pri-vms.md)。 | 所有工作。 | `true` |

[files_dirs]: https://azure.microsoft.com/documentation/articles/batch-api-basics/#files-and-directories
[multi_instance]: https://azure.microsoft.com/documentation/articles/batch-mpi/
[coord_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#coordination-command
[app_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#application-command
