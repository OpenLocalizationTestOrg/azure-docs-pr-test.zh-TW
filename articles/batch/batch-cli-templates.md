---
title: "aaaRun Azure 批次的端對端工作而不需要撰寫程式碼 （預覽） |Microsoft 文件"
description: "建立 hello Azure CLI toocreate 批次集區、 工作和工作的範本檔案。"
services: batch
author: mscurrell
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: na
ms.topic: article
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: markscu
ms.openlocfilehash: c0434d09766451f6ba516efbad949834711ee819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a>使用 Azure Batch CLI 範本和檔案傳輸 (預覽)

使用 Azure CLI hello 很可能 toorun 批次作業，而不需要撰寫程式碼。

可建立及使用以 hello Azure CLI，讓批次集區、 工作和工作 toobe 建立範本檔案。 作業輸入的檔可以輕鬆地上載 hello 與 hello 批次帳戶與工作輸出檔下載相關聯的儲存體帳戶。

## <a name="overview"></a>概觀

延伸模組 toohello Azure CLI 啟用批次 toobe 使用端對端的使用者不是開發人員。 可以建立的集區、 輸入的資料上傳，工作與相關聯的工作建立，以及 hello 產生輸出資料下載 – 沒有必要的程式碼 hello CLI 直接使用或已整合到指令碼。

批次範本建置 hello [hello Azure CLI 中現有的批次支援](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation)toospecify 屬性值的 hello 建立集區、 工作、 工作和其他項目允許 JSON 檔案。 與批次範本 hello 下列功能會加入透過極限 hello JSON 檔案：

-   可以定義參數。 使用 hello 範本時，只有 hello 參數值會指定的 toocreate hello 的項目，hello 的範本主體中指定其他項目屬性值。 了解批次和應用程式 toobe 執行批次的使用者可以建立範本，指定集區、 工作和工作屬性值。 較不熟悉批次和 （或） 應用程式的使用者只需要定義 hello 參數 toospecify hello 值。

-   作業工作 factory 建立一個或多個作業，避免 hello 與相關聯的工作需要許多建立的工作定義 toobe 和大幅簡化提交作業。


輸入的資料檔案需 toobe 提供給工作，通常會產生輸出資料檔案。 儲存體帳戶相關聯，根據預設，每一批次帳戶和檔案可以輕鬆地轉移的 tooand 從撰寫任何程式碼使用 CLI，此儲存體帳戶並所需的任何儲存體認證。

例如，[ffmpeg](http://ffmpeg.org/) 是常用的應用程式，可處理音訊和視訊檔案。 hello Azure 批次 CLI 可以是使用的 tooinvoke ffmpeg tootranscode 來源視訊檔案 toodifferent 解析度。

-   會建立集區範本。 建立 hello 範本的 hello 使用者知道如何 toocall hello ffmpeg 應用程式和其的需求。它們指定 hello 適當的作業系統，VM 容量，ffmpeg 方式是安裝 （從應用程式封裝或使用封裝管理員，例如），和其他集區的屬性值。 因此只有 hello 集區識別碼和 Vm 數目使用 hello 範本時，需要 toobe 指定，會建立參數。

-   會建立作業範本。 hello 使用者建立 hello 範本知道如何 ffmpeg 需求 toobe 叫用 tootranscode 來源視訊 tooa 不同的解決方案，並指定 hello 工作命令列。它們也會知道已 hello 來源視訊檔案，包含與工作，每個輸入檔所需的資料夾。

-   使用者所擁有的視訊檔案 tootranscode 一組會先建立集區使用 hello 集區範本，請指定唯一的 hello 集區識別碼和所需的 Vm 數目。 然後，他們可以上傳 hello 來源檔案 tootranscode。 工作可以再使用提交 hello 工作範本，指定只有 hello 集區識別碼和上傳的 hello 來源檔案的位置。 建立 hello 批次作業，請使用每個輸入檔案所產生的一項工作。 最後，hello 轉碼輸出檔可能會下載。

## <a name="installation"></a>安裝

hello 範本和檔案傳輸的功能需要安裝擴充功能 toobe。

如需有關如何查看 tooinstall hello Azure CLI 指示[安裝 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)。

一次 hello Azure CLI 安裝之後，可以安裝擴充功能，使用下列的 CLI 命令的批次 hello:

```azurecli
az component update --add batch-extensions --allow-third-party
```

如需 hello 批次的擴充功能的詳細資訊，請參閱[Microsoft Azure 批次 CLI 擴充功能的 Windows、 Mac 和 Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux)。

## <a name="templates"></a>範本

Azure 批次 CLI hello 可讓項目，例如集區、 工作和工作 toobe 藉由指定包含屬性名稱和值的 JSON 檔案建立。 例如：

```azurecli
az batch pool create –-json-file AppPool.json
```

Azure 批次是類似 tooAzure 資源管理員範本，在功能和語法。 這些屬性的 JSON 檔案所含的項目屬性名稱和值，但新增下列主要概念的 hello:

-   **參數**

    -   允許屬性值 toobe 區段中指定主體，以只需要 toobe 時使用 hello 範本所提供的參數值。 例如，hello 完整定義集區可以架設在 hello 本文和集區識別碼; 針對定義只有一個參數只包含集區的識別碼字串因此需要提供 toobe toocreate 集區。
        
    -   hello 的範本主體可以用來撰寫的其他人了解的批次及 hello 應用程式 toobe 執行批次。當 hello 範本時，必須提供只有 hello 作者定義參數的值。 不含使用者 hello 深入的批次和/或應用程式知識因此可以使用的範本。

-   **變數**

    -   允許簡單或複雜的參數值 toobe 在一個位置指定與 hello 範本主體中的一個或多個地方使用。 變數可以簡化和縮小 hello hello 範本，以及讓它更容易維護保留其中一個位置 toochange 屬性可能會變更其值。

-   **較高層級的建構**

    -   尚無法使用 hello 批次 Api 中的 hello 範本中使用較高層級的某些建構。 例如，工作 factory 可以建立 hello 作業使用的通用的工作定義的多個工作的工作範本定義。 這些建構函式會避免 hello 需要 toocode 來動態建立多個 JSON 檔案，例如每個工作中，一個檔案，以及建立指令碼檔案 tooinstall 應用程式透過封裝管理員 中，例如。

    -   在某些點，適用這些建構函式可能會加入 toothe 批次服務和中可用的 hello 批次 Api、 Ui 等等。

### <a name="pool-templates"></a>集區範本

此外 hello 集區範本所支援的參數和變數，遵循較高層級建構的 hello toohello 標準範本功能：

-   **套件參考**

    -   （選擇性） 可讓軟體 toobe 複製 toopool 節點使用封裝管理員。 指定 hello 封裝管理員 」 和 「 套件識別碼。 所能 toodeclare 一或多個封裝可避免 hello 需要 toocreate 取得所需的 hello 封裝的指令碼、 安裝 hello 指令碼，並在集區中的每個節點上執行 hello 指令碼。

hello 下面是範例的安裝，且僅會建立 Linux Vm 的集區與 ffmpeg 範本需要集區識別碼字串和 hello 數量的 Vm 提供 toobe toouse:

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "hello number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello pool id "
            }
        }
    },
    "pool": {
        "type": "Microsoft.Batch/batchAccounts/pools",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('poolId')]",
            "virtualMachineConfiguration": {
                "imageReference": {
                    "publisher": "Canonical",
                    "offer": "UbuntuServer",
                    "sku": "16.04.0-LTS",
                    "version": "latest"
                },
                "nodeAgentSKUId": "batch.node.ubuntu 16.04"
            },
            "vmSize": "STANDARD_D3_V2",
            "targetDedicatedNodes": "[parameters('nodeCount')]",
            "enableAutoScale": false,
            "maxTasksPerNode": 1,
            "packageReferences": [
                {
                    "type": "aptPackage",
                    "id": "ffmpeg"
                }
            ]
        }
    }
}
```

如果 hello 範本檔案命名為_集區 ffmpeg.json_，然後 hello 範本會叫用，如下所示：

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a>作業範本

此外 hello 工作範本所支援的參數和變數，遵循較高層級建構的 hello toohello 標準範本功能：

-   **工作 Factory**

    -   會從一個工作定義中建立作業的多個工作。 支援三種工作 Factory – 參數整理、每個檔案的工作和工作集合。

hello 以下是範例會建立工作以 ffmpeg 轉碼 MP4 視訊檔案 tooone 的兩個較低的解析度，以使用每個來源視訊檔案建立一個工作的範本：

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch pool which runs hello job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch job"
            }
        },
        "resolution": {
            "type": "string",
            "defaultValue": "428x240",
            "allowedValues": [
                "428x240",
                "854x480"
            ],
            "metadata": {
                "description": "Target video resolution"
            }
        }
    },
    "job": {
        "type": "Microsoft.Batch/batchAccounts/jobs",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('jobId')]",
            "constraints": {
                "maxWallClockTime": "PT5H",
                "maxTaskRetryCount": 1
            },
            "poolInfo": {
                "poolId": "[parameters('poolId')]"
            },
            "taskFactory": {
                "type": "taskPerFile",
                "source": { 
                    "fileGroup": "ffmpeg-input"
                },
                "repeatTask": {
                    "commandLine": "ffmpeg -i {fileName} -y -s [parameters('resolution')] -strict -2 {fileNameWithoutExtension}_[parameters('resolution')].mp4",
                    "resourceFiles": [
                        {
                            "blobSource": "{url}",
                            "filePath": "{fileName}"
                        }
                    ],
                    "outputFiles": [
                        {
                            "filePattern": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                            "destination": {
                                "autoStorage": {
                                    "path": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                                    "fileGroup": "ffmpeg-output"
                                }
                            },
                            "uploadOptions": {
                                "uploadCondition": "TaskSuccess"
                            }
                        }
                    ]
                }
            },
            "onAllTasksComplete": "terminatejob"
        }
    }
}
```

如果 hello 範本檔案命名為_作業 ffmpeg.json_，然後 hello 範本會叫用，如下所示：

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a>檔案群組和檔案傳輸

大部分的作業與工作都需要輸入檔，並且會產生輸出檔。 這兩個輸入檔和輸出檔通常需要 toobe 傳輸，從 hello 用戶端 toohello 節點，或從 hello 節點 toohello 用戶端。 hello Azure 批次 CLI 延伸抽象化抽離的檔案傳輸，而且會運用 hello 儲存體帳戶所建立的每個批次帳戶的預設值。

檔案群組等同 tooa hello Azure 儲存體帳戶中建立的容器。 hello 檔案群組可能會有子資料夾。

hello 批次 CLI 延伸模組會提供來自用戶端 tooa 指定的檔案群組的檔案上傳和下載檔案，從指定的檔案群組 tooa 用戶端 hello 命令。

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

集區和工作的範本可讓儲存在檔案群組 toobe 為複製到集區的節點上指定的檔案或集區關閉節點恢復 tooa 檔案群組。 比方說，在先前指定的工作範本，hello 檔案群組 「 ffmpeg-輸入 」，被指定 hello 工作 factory 為 hello 的 hello 來源視訊檔案複製到的轉碼; hello 節點上的位置hello 檔案群組"ffmpeg-output"作為 hello 位置 hello 轉碼輸出檔案的位置複製 toofrom hello 節點執行每項工作。

## <a name="summary"></a>摘要

範本和檔案傳輸支援目前已加入 toohello Azure CLI。 hello 目標是可讓使用者不需要使用 hello 批次應用程式開發介面，例如研究人員、 IT 使用者等 toodevelop 程式碼的批次 toousers tooexpand hello 對象。 沒有程式碼撰寫，非常了解 Azure 批次及 hello 應用程式 toobe 批次所執行的使用者可以建立集區和工作建立的範本。 範本參數，與未批次和 hello 的應用程式的詳細知識，使用者可以使用 hello 範本。

嘗試 hello hello Azure CLI 的批次延伸模組，並提供任何意見反應或改善建議，可能是在 hello 註解，如這篇文章，或透過 hello [Azure Batch 論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch)。

## <a name="next-steps"></a>後續步驟

- 請參閱 hello 批次範本部落格文章：[執行 Azure 批次作業使用 hello Azure CLI – 沒有所需的程式碼](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/)。
- 詳細的安裝與使用文件、 範例和原始程式碼位於 hello [Azure GitHub 儲存機制](https://github.com/Azure/azure-batch-cli-extensions)。
