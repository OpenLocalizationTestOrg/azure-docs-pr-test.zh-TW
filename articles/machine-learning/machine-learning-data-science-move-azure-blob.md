---
title: "從 Azure Blob 儲存體 aaaMove 資料 tooand |Microsoft 文件"
description: "從 Azure Blob 儲存體移動資料 tooand"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d6681e30-ab45-45ea-a9fb-ac8acefe544d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;sachouks
ms.openlocfilehash: e12b8c157955195e826f8b108075afaf25ca7bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage"></a>從 Azure Blob 儲存體移動資料 tooand
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this tooseparate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

哪一種方法最適合會取決於您的案例。 hello [Azure Machine Learning 中的進階分析的案例](machine-learning-data-science-plan-sample-scenarios.md)篇文章可協助您判斷您需要的各種不同的 hello 進階分析程序中使用的資料科學工作流程的 hello 資源。

> [!NOTE]
> 完成簡介 tooAzure blob 儲存體，請參閱太[Azure Blob 的基本概念](../storage/blobs/storage-dotnet-how-to-use-blobs.md)和太[Azure Blob 服務](https://msdn.microsoft.com/library/azure/dd179376.aspx)。
> 
> 

或者，您可以使用 [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) 來︰ 

* 建立和排程管線，以從 Azure Blob 儲存體下載資料， 
* 將它傳遞 tooa 發佈 Azure Machine Learning web 服務， 
* 收到 hello 的預測分析的結果，並 
* 上傳 hello 結果 toostorage。 

如需詳細資訊，請參閱 [使用 Azure Data Factory 和 Azure Machine Learning 來建立預測管線](../data-factory/data-factory-azure-ml-batch-execution-activity.md)。

## <a name="prerequisites"></a>必要條件
本文件假設您有 Azure 訂用帳戶、 儲存體帳戶和該帳戶 hello 對應儲存體金鑰。 上傳/下載資料之前，您必須知道 Azure 儲存體帳戶名稱和帳戶金鑰。

* tooset 註冊 Azure 訂用帳戶，請參閱[免費試用一個月](https://azure.microsoft.com/pricing/free-trial/)。
* 如需建立儲存體帳戶的指示，以及取得帳戶和金鑰的資訊，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。

