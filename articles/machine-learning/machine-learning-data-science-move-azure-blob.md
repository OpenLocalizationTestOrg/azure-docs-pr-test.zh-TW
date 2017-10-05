---
title: "從 Azure Blob 儲存體來回移動資料 | Microsoft Docs"
description: "從 Azure Blob 儲存體來回移動資料"
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
ms.openlocfilehash: d9a626cccd3cdfcdc85f000bd3192aef2881e9a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-and-from-azure-blob-storage"></a><span data-ttu-id="e7018-103">從 Azure Blob 儲存體來回移動資料</span><span class="sxs-lookup"><span data-stu-id="e7018-103">Move data to and from Azure Blob Storage</span></span>
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this to separate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

<span data-ttu-id="e7018-104">哪一種方法最適合會取決於您的案例。</span><span class="sxs-lookup"><span data-stu-id="e7018-104">Which method is best for you depends on your scenario.</span></span> <span data-ttu-id="e7018-105">[在 Azure 機器學習中的進階分析案例](machine-learning-data-science-plan-sample-scenarios.md) 文章可協助您判斷進階分析程序中各種資料科學工作流程所需的資源。</span><span class="sxs-lookup"><span data-stu-id="e7018-105">The [Scenarios for advanced analytics in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) article helps you determine the resources you need for a variety of data science workflows used in the advanced analytics process.</span></span>

> [!NOTE]
> <span data-ttu-id="e7018-106">如需 Azure Blob 儲存體的完整介紹，請參閱 [Azure Blob 基本概念](../storage/blobs/storage-dotnet-how-to-use-blobs.md)和 [Azure Blob 服務](https://msdn.microsoft.com/library/azure/dd179376.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e7018-106">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

<span data-ttu-id="e7018-107">或者，您可以使用 [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) 來︰</span><span class="sxs-lookup"><span data-stu-id="e7018-107">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to:</span></span> 

* <span data-ttu-id="e7018-108">建立和排程管線，以從 Azure Blob 儲存體下載資料，</span><span class="sxs-lookup"><span data-stu-id="e7018-108">create and schedule a pipeline that downloads data from Azure blob storage,</span></span> 
* <span data-ttu-id="e7018-109">將其傳遞至已發佈的 Azure Machine Learning Web 服務，</span><span class="sxs-lookup"><span data-stu-id="e7018-109">pass it to a published Azure Machine Learning web service,</span></span> 
* <span data-ttu-id="e7018-110">接收預測性分析結果，並</span><span class="sxs-lookup"><span data-stu-id="e7018-110">receive the predictive analytics results, and</span></span> 
* <span data-ttu-id="e7018-111">將結果上傳至儲存體。</span><span class="sxs-lookup"><span data-stu-id="e7018-111">upload the results to storage.</span></span> 

<span data-ttu-id="e7018-112">如需詳細資訊，請參閱 [使用 Azure Data Factory 和 Azure Machine Learning 來建立預測管線](../data-factory/data-factory-azure-ml-batch-execution-activity.md)。</span><span class="sxs-lookup"><span data-stu-id="e7018-112">For more information, see [Create predictive pipelines using Azure Data Factory and Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7018-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="e7018-113">Prerequisites</span></span>
<span data-ttu-id="e7018-114">本文件假設您擁有 Azure 訂用帳戶、儲存體帳戶和該帳戶的對應儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="e7018-114">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span></span> <span data-ttu-id="e7018-115">上傳/下載資料之前，您必須知道 Azure 儲存體帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="e7018-115">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="e7018-116">若要設定 Azure 訂用帳戶，請參閱 [免費試用一個月](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="e7018-116">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e7018-117">如需建立儲存體帳戶的指示，以及取得帳戶和金鑰的資訊，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="e7018-117">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

