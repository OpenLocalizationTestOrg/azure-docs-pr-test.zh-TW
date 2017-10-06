---
title: "aaaPersist 結果或從記錄檔已完成的工作與工作 tooa 資料存放區-Azure 批次 |Microsoft 文件"
description: "深入了解從 Batch 工作和作業保存輸出資料的不同選項。 您可以保存資料 tooAzure 存放裝置或 tooanother 資料存放區。"
services: batch
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0b11e387f1694e1ce3e9573db7f6013f0154cad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-output"></a>持續作業及工作輸出

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

工作輸出的一些常見範例包括：

- Hello 工作會處理輸入資料時，建立的檔案。
- 與工作執行相關聯的記錄檔。 

本文說明保存工作輸出和 hello 案例每個選項是最合適的各種選項。   

## <a name="about-hello-batch-file-conventions-standard"></a>關於 hello 批次檔慣例標準

Batch 會定義一組選擇性的慣例，可在 Azure 儲存體中命名工作輸出檔案。 hello[批次檔慣例標準](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)描述這些慣例。 hello 檔案慣例標準決定 hello hello 容器和 blob 的目的地路徑 Azure 儲存體中的 hello 作業和工作的 hello 名稱為基礎的給定的輸出檔案名稱。

是由 tooyou 您是否決定 toouse hello 檔案慣例命名輸出資料檔案的標準。 不過，您希望，您可以也命名 hello 目的地容器和 blob。 如果您使用 hello 標準檔案慣例來命名輸出檔案，則輸出檔可供檢視之 hello [Azure 入口網站][portal]。

有幾個不同的方式，您可以使用 hello 檔案慣例標準：

- 如果您使用 hello 批次服務 API toopersist 輸出檔案，您可以選擇 tooname 目的地容器和 blob 根據 toohello 標準檔案慣例。 hello 批次服務 API 可讓您 toopersist 輸出檔，用戶端程式碼，而不需修改應用程式工作。
- 如果您正在開發的.NET，您可以使用 hello[適用於.NET 的 Azure 批次檔慣例程式庫][nuget_package]。 使用此程式庫的優點是它支援查詢您根據 tootheir 識別碼或用途的輸出檔案。 hello 內建查詢功能可讓您輕鬆 tooaccess 輸出檔案從用戶端應用程式或其他工作。 不過，您的工作應用程式必須修改的 toocall 檔案慣例程式庫。 如需詳細資訊，請參閱 hello hello 參考[檔案慣例.NET 程式庫](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.aspx)。
- 如果您正在開發以.NET 以外的語言，您可以實作 hello 標準應用程式中的檔案慣例。

## <a name="design-considerations-for-persisting-output"></a>保存輸出的設計考量 

設計您的批次解決方案時，請考慮 hello 下列因素相關的 toojob 以及工作輸出。

* **計算節點存留期**：計算節點通常是過渡性的，尤其是在啟用自動調整的集區中。 只有當 hello 節點存在，而且只有在 hello 檔案保留期限內您已經設定 hello 工作時使用的節點執行的工作輸出。 如果工作會產生 hello 工作完成之後可能需要的輸出，hello 工作必須上傳其輸出檔案 tooa 長期存放區例如 Azure 儲存體。

* **輸出儲存體**：建議使用 Azure 儲存體作為工作輸出的資料存放區，但是您可以使用任何持久的儲存體。 寫入工作輸出 tooAzure 儲存體已整合到 hello 批次服務 API。 如果您使用另一種持久儲存體，您將自己需要 toowrite hello 應用程式邏輯 toopersist 工作輸出。   

* **輸出擷取**： 您可以在擷取工作輸出直接從 hello 計算節點的 程式集區，或是從 Azure 儲存體或其他資料存放區已保存工作輸出。 tooretrieve 工作的輸出直接從運算節點，您需要 hello 檔案名稱和其 hello 節點上的輸出位置。 如果您將保存工作輸出 tooAzure 儲存體，您需要 Azure 儲存體 toodownload hello 以 hello Azure 儲存體 SDK 的輸出檔中的 hello 完整路徑 toohello 檔案。

* **檢視輸出**： 當您瀏覽 tooa 批次工作，在 Azure 入口網站，並選取 hello**節點上的檔案**，您會看到與 hello 工作相關聯的所有檔案，不只是 hello 您感興趣的輸出檔。 同樣地，在計算節點上的檔案，則使用只有 hello 節點存在，而且只有在 hello 檔案保留的時間內您已設定 hello 工作。 tooview 工作輸出，您已保存 tooAzure 儲存體，您可以使用 hello Azure 入口網站或 Azure 儲存體用戶端應用程式，例如 hello [Azure 儲存體總管][storage_explorer]。 tooview 輸出 Azure 儲存體中的資料與 hello 入口網站或其他工具，您必須知道 hello 檔案的位置，並直接瀏覽 tooit。

## <a name="options-for-persisting-output"></a>保存輸出的選項

根據您的案例中，有幾個不同的方法，您可以採取 toopersist 工作輸出：

- 使用 hello 批次服務 API。  
- 使用適用於.NET 的 hello 批次檔慣例程式庫。  
- 實作 hello 標準應用程式中的批次檔慣例。
- 實作自訂檔案移動解決方案。

hello 下列各節描述每一種方法中更多詳細資料。

### <a name="use-hello-batch-service-api"></a>使用 hello 批次服務 API

2017-05-01 版中，與 hello 批次服務將 Azure 儲存體中的輸出檔指定的工作資料的支援時您[加入工作 tooa 作業](https://docs.microsoft.com/rest/api/batchservice/add-a-task-to-a-job)或[新增的工作 tooa 工作集合](https://docs.microsoft.com/rest/api/batchservice/add-a-collection-of-tasks-to-a-job)。

hello 批次服務應用程式開發介面支援保存的工作資料 tooan 與 hello 虛擬機器組態建立集區的 Azure 儲存體帳戶。 以 hello 批次服務 API，您可以保存工作資料，而不需要修改您的工作執行的 hello 應用程式。 您可以選擇性地遵循 toohello[批次檔慣例標準](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)hello 檔案命名您保存 tooAzure 儲存體。 

使用 hello 批次服務 API toopersist 工作何時輸出：

- 您想要從批次工作及建立 hello 虛擬機器組態與集區中的作業管理員工作的 toopersist 資料。
- 您想使用任意名稱 toopersist 資料 tooan Azure 儲存體容器。
- 您想要 toopersist 資料 tooan Azure 儲存體容器名稱相應 toohello[批次檔慣例標準](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)。 

> [!NOTE]
> hello 批次服務應用程式開發介面不支援從與 hello 雲端服務組態建立集區中執行工作的保存資料。 如需保存的工作輸出從集區執行 hello 雲端服務的組態資訊，請參閱[保存作業和工作資料 tooAzure 儲存體與 hello.NET toopersist 的批次檔慣例文件庫](batch-task-output-file-conventions.md)
> 
> 

如需保存的工作輸出，以 hello 批次服務 API 的詳細資訊，請參閱[保存以 hello 批次服務應用程式開發介面的工作資料 tooAzure 儲存體](batch-task-output-files.md)。 另請參閱 hello [PersistOutputs] [github_persistoutputs] 的範例示範如何 toouse hello 批次用戶端程式庫.NET toopersist 工作輸出 toodurable 儲存體的 GitHub 上的專案。

### <a name="use-hello-batch-file-conventions-library-for-net"></a>使用適用於.NET 的 hello 批次檔慣例程式庫

建置批次解決方案使用 C# 和.NET 開發人員可以使用 hello[檔案慣例.NET 程式庫][ nuget_package] toopersist 工作資料 tooan Azure 儲存體帳戶，根據 toohello[批次檔標準的慣例](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)。 hello 檔案慣例程式庫會處理已知的方式移動的輸出檔案 tooAzure 儲存體和命名目的地容器和 blob。

hello 檔案慣例的程式庫支援查詢依識別碼或用途的輸出檔，它們不需要 hello 讓您輕鬆 toolocate 完成檔案的 Uri。 

使用.NET toopersist 工作 hello 批次檔慣例程式庫輸出時：

- Hello 工作仍在執行時，您會想 toostream 資料 tooAzure 儲存體。
- 您想要從以 hello 雲端服務組態或 hello 虛擬機器組態建立的集區的 toopersist 資料。
- 用戶端應用程式或其他工作在 hello 作業需求 toolocate 和下載工作輸出檔依識別碼或依用途。 
- 您想要初始結果 tooperform 檢查指標或早期上的傳。
- 您想 tooview hello Azure 入口網站中的工作輸出。

For.NET 上保存的工作輸出與 hello 檔案慣例媒體櫃資訊，請參閱[保存作業和工作資料 tooAzure 儲存體與 hello.NET toopersist 的批次檔慣例文件庫](batch-task-output-file-conventions.md)。 另請參閱 hello [PersistOutputs] [github_persistoutputs] 的範例示範如何 toouse hello 檔案慣例文件庫.NET toopersist 工作輸出 toodurable 儲存體的 GitHub 上的專案。

hello GitHub 上的 [PersistOutputs] [github_persistoutputs] 範例專案會示範如何 toouse hello 批次用戶端程式庫.NET toopersist 工作輸出 toodurable 儲存體。

### <a name="implement-hello-batch-file-conventions-standard"></a>實作 hello 標準的批次檔慣例

如果您使用.NET 以外的語言，您可以實作 hello[批次檔慣例標準](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)自己的應用程式中。 

您可能想 tooimplement hello 檔案慣例命名標準自己想經過證實的命名配置，或者您想 tooview hello Azure 入口網站中的工作輸出時。

### <a name="implement-a-custom-file-movement-solution"></a>實作自訂檔案移動解決方案

您也可以實作自己的完整檔案移動解決方案。 使用這個方法的時機：

- 您想 toopersist 工作資料 tooa 資料存放區以外 Azure 儲存體。 tooupload 檔案 tooa 資料存放區 SQL Azure 或 Azure DataLake 等，您可以建立自訂指令碼或可執行檔 tooupload toothat 位置。 您可以接著呼叫 hello 命令列上執行您的主要可執行檔之後。 例如，在 Windows 節點上，您可能會呼叫這兩個命令：`doMyWork.exe && uploadMyFilesToSql.exe`
- 您想要初始結果 tooperform 檢查指標或早期上的傳。
- 您想 toomaintain 更精確地控制錯誤處理。 比方說，您可能想的 tooimplement 自己的解決方案，如果您想 toouse 工作相依性動作 tootake 特定上載根據特定工作的結束代碼的動作。 如需有關工作相依性動作的詳細資訊，請參閱[toorun 工作相依於其他工作建立工作的相依性](batch-task-dependencies.md)。 

## <a name="next-steps"></a>後續步驟

- 探索使用中的 hello 批次服務 API toopersist 工作資料中的 hello 新功能[保存以 hello 批次服務應用程式開發介面的工作資料 tooAzure 儲存體](batch-task-output-files.md)。
- 了解如何使用 hello 批次檔慣例文件庫中的.net[保存作業和工作資料 tooAzure 儲存體與 hello.NET toopersist 的批次檔慣例文件庫](batch-task-output-file-conventions.md)。
- 請參閱 hello [PersistOutputs] [github_persistoutputs] GitHub，示範如何 toouse 兩者 hello 批次.NET 的用戶端程式庫和.NET toopersist 工作 hello 檔案慣例程式庫上範例專案輸出 toodurable 儲存體。

[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/
