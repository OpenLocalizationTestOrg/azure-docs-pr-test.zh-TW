---
title: "aaaUse Azure 批次 Api 及工具 toodevelop 大規模的平行處理解決方案 |Microsoft 文件"
description: "深入了解 hello Api 及工具可用於開發與 hello Azure Batch 服務方案。"
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: tamram
ms.openlocfilehash: ca75a1a63b3e7e6b0805e79a63685bc49aaaca8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-batch-apis-and-tools"></a>Batch API 和工具的概觀

處理 Azure 批次的平行工作負載通常是以程式設計方式使用其中一種 hello[批次 Api](#batch-development-apis)。 用戶端應用程式或服務可以使用 hello 批次 Api toocommunicate hello 批次服務。 以 hello 批次 Api，您可以建立並管理計算節點的集區的虛擬機器或雲端服務。 然後，您可以排程工作與工作 toorun 那些節點上。 

可以有效率地處理大型工作負載，為您的組織，或提供服務的前端 tooyour 客戶，讓它們可以執行作業和工作，即依需求，或根據排程-在上一個、 數百或甚至數千個節點。 您也可以在 [Azure Data Factory](../data-factory/data-factory-data-processing-using-batch.md?toc=%2fazure%2fbatch%2ftoc.json)之類的工具所管理的大型工作流程中使用 Azure Batch。

> [!TIP]
> 當您準備好 toodig toohello 批次 API 中的 hello 的更深入了解功能，它提供、 簽出 hello[批次功能概觀，讓開發人員](batch-api-basics.md)。
> 
> 

## <a name="azure-accounts-for-batch-development"></a>用於 Batch 開發的 Azure 帳戶
當您開發批次的解決方案時，您將使用下列帳戶在 Microsoft Azure 中的 hello。

* **Azure 帳戶和訂用帳戶** - 如果您沒有 Azure 訂用帳戶，您可以啟用 [MSDN 訂戶權益][msdn_benefits]，或是註冊[免費 Azure 帳戶][free_account]。 當您建立帳戶時，會為您建立預設訂用帳戶。
* **Batch 帳戶** - Azure Batch 資源 (包括集區、計算節點、作業和工作) 都與 Azure Batch 帳戶相關聯。 當您的應用程式對 hello 批次服務提出之要求時，它會驗證 hello 要求使用 hello Azure Batch 帳戶名稱、 hello hello 帳戶 URL 和存取金鑰。 您可以[建立批次帳戶](batch-account-create-portal.md)hello Azure 入口網站中。
* **儲存體帳戶** - Batch 內建就支援處理 [Azure 儲存體][azure_storage]中的檔案。 幾乎每個批次的案例會使用 Azure Blob 儲存體臨時區域，您的工作執行的 hello 程式和 hello 資料所處理，以及 hello 儲存它們所產生的輸出資料。 toocreate 儲存體帳戶，請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。

## <a name="batch-service-apis"></a>Batch 服務 API

您的應用程式和服務可以發出 REST API 的直接呼叫或使用一或多個下列用戶端程式庫 toorun hello 和管理您的 Azure 批次工作負載。

| API | API 參考資料 | 下載 | 教學課程 | 程式碼範例 | 其他資訊 |
| --- | --- | --- | --- | --- | --- |
| **Batch REST** |[MSDN][batch_rest] |N/A |- |- | [支援的版本](https://docs.microsoft.com/rest/api/batchservice/batch-service-rest-api-versioning) |
| **Batch .NET** |[docs.microsoft.com][api_net] |[NuGet ][api_net_nuget] |[教學課程](batch-dotnet-get-started.md) |[GitHub][api_sample_net] | [版本資訊](http://aka.ms/batch-net-dataplane-changelog) |
| **Batch Python** |[readthedocs.io][api_python] |[PyPI][api_python_pypi] |[教學課程](batch-python-tutorial.md)|[GitHub][api_sample_python] | [讀我檔案](https://github.com/Azure/azure-sdk-for-python/blob/master/doc/batch.rst) |
| **Batch Node.js** |[github.io][api_nodejs] |[npm][api_nodejs_npm] |- |- | [讀我檔案](https://github.com/Azure/azure-sdk-for-node/tree/master/lib/services/batch) |
| **Batch Java** |[github.io][api_java] |[Maven][api_java_jar] |- |[讀我檔案][api_sample_java] | [讀我檔案](https://github.com/Azure/azure-batch-sdk-for-java)|

## <a name="batch-management-apis"></a>Batch 管理 API

hello 批次的 Azure 資源管理員 Api 提供以程式設計方式存取 tooBatch 帳戶。 使用這些 API，您可以透過程式設計方式管理 Batch 帳戶、配額和應用程式套件。  

| API | API 參考資料 | 下載 | 教學課程 | 程式碼範例 |
| --- | --- | --- | --- | --- |
| **Batch Resource Manager REST** |[docs.microsoft.com][api_rest_mgmt] |N/A |- |[GitHub](https://github.com/Azure-Samples/batch-dotnet-manage-batch-accounts) |
| **Batch Resource Manager .NET** |[docs.microsoft.com][api_net_mgmt] |[NuGet ][api_net_mgmt_nuget] | [教學課程](batch-management-dotnet.md) |[GitHub][api_sample_net] |

## <a name="batch-command-line-tools"></a>Batch 命令列工具

這些命令列工具提供 hello 相同的功能，如 hello 批次服務和批次管理 Api: 

* [PowerShell 指令程式的批次][batch_ps]: hello Azure 批次 cmdlet，在 hello [Azure PowerShell](/powershell/azure/overview)模組可讓您使用 PowerShell toomanage 批次資源。
* [Azure CLI](/cli/azure/overview): hello Azure 命令列介面 (Azure CLI) 是可提供殼層命令與許多 Azure 服務，包括 hello 批次服務和批次管理服務互動的跨平台工具組。 請參閱[管理批次資源，使用 Azure CLI](batch-cli-get-started.md)如需有關使用 Azure CLI hello 與批次。

## <a name="other-tools-for-application-development"></a>其他用於應用程式開發的工具

以下是其他一些可能有助於建置及偵錯 Batch 應用程式和服務的工具︰

* [Azure 入口網站][portal]： 您可以建立、 監視及刪除批次集區、 工作和工作中 hello Azure 入口網站的批次的刀鋒視窗。 您執行您的工作，以及甚至從 hello 計算節點下載檔案，在 程式集區時，您可以檢視這些和其他資源的 hello 狀態資訊。 例如，您可以在進行疑難排解時下載失敗的工作 `stderr.txt`。 您也可以下載可讓您 toolog toocompute 節點中的遠端桌面 (RDP) 檔案。
* [Azure 批次總管][batch_explorer]： 批次總管提供類似的批次資源管理功能，如 hello Azure 入口網站，但在獨立 Windows Presentation Foundation (WPF) 用戶端應用程式。 Hello 批次.NET 範例應用程式上可用的其中一個[GitHub][github_samples]，您可以使用 Visual Studio 2015 或更新版本，請建立該它 toobrowse 和使用開發過程中，在您的 Batch 帳戶管理 hello 資源和偵錯您批次的解決方案。 檢視工作、 集區和工作的詳細資訊，從運算節點下載檔案，然後從遠端連線 toonodes，批次檔案總管中使用遠端桌面 (RDP) 檔案，您可以下載。
* [Microsoft Azure 儲存體總管][storage_explorer]： 不完全的 Azure 批次工具，同時 hello 存放裝置總管時，另一個重要的工具 toohave 您開發與偵錯您批次的解決方案。

## <a name="additional-resources"></a>其他資源

- 請參閱 < 從批次應用程式記錄事件的相關 toolearn[診斷評估和監控的批次方案的事件記錄](batch-diagnostics.md)。 Hello 批次服務所引發的事件上的參考，請參閱[批次分析](batch-analytics.md)。
- 如需計算節點環境變數的詳細資訊，請參閱 [Azure Batch 計算節點環境變數](batch-compute-node-environment-variables.md)。

## <a name="next-steps"></a>後續步驟

* 讀取 hello[批次功能概觀，讓開發人員](batch-api-basics.md)，任何人準備 toouse 批次的重要資訊。 hello 發行項包含許多建置批次應用程式時，可以使用的 API 功能的批次服務資源集區、 節點、 工作和工作和 hello，如需詳細的資訊。
* [開始使用 hello Azure Batch library for.NET](batch-dotnet-get-started.md) toolearn 如何 toouse C# 和 hello 批次.NET 程式庫 tooexecute 簡單的工作負載使用常見的批次工作流程。 這篇文章應為其中一個您同時學習如何 toouse hello 批次服務的第一個停止。 另外還有[Python 版本](batch-python-tutorial.md)hello 教學課程。
* 下載 hello[程式碼範例在 GitHub 上的][ github_samples] toosee C# 和 Python 與批次 tooschedule 和程序範例工作負載可以互動方式。
* 簽出 hello[批次學習路徑][ learning_path] tooget hello 資源可用 tooyou 您了解學習 toowork 與批次。


[azure_storage]: https://azure.microsoft.com/services/storage/
[api_java]: http://azure.github.io/azure-sdk-for-java/
[api_java_jar]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-batch%22
[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_nuget]: https://www.nuget.org/packages/Azure.Batch/
[api_rest_mgmt]: https://docs.microsoft.com/\rest/api/batchmanagement/
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_net_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[api_nodejs]: http://azure.github.io/azure-sdk-for-node/azure-batch/latest/
[api_nodejs_npm]: https://www.npmjs.com/package/azure-batch
[api_python]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html
[api_python_pypi]: https://pypi.python.org/pypi/azure-batch
[api_sample_net]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp
[api_sample_python]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[api_sample_java]: https://github.com/Azure/azure-batch-samples/tree/master/Java/
[batch_ps]: /powershell/resourcemanager/azurerm.batch/v2.7.0/azurerm.batch
[batch_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx
[free_account]: https://azure.microsoft.com/free/
[github_samples]: https://github.com/Azure/azure-batch-samples
[learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[msdn_benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[storage_explorer]: http://storageexplorer.com/
[portal]: https://portal.azure.com
