---
title: "aaaLoad 資料分析的 Azure 儲存體環境 |Microsoft 文件"
description: "從 Azure Blob 儲存體移動資料 tooand"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b8fbef77-3e80-4911-8e84-23dbf42c9bee
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 0fea2290991f9fa63d9e46c3a657000e27d95289
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a><span data-ttu-id="78c2c-103">將資料載入至儲存體環境以便進行分析</span><span class="sxs-lookup"><span data-stu-id="78c2c-103">Load data into storage environments for analytics</span></span>
<span data-ttu-id="78c2c-104">hello 小組資料科學程序需要該資料是內嵌或載入至各種不同的儲存體環境 toobe 處理或 hello 程序的每個階段中分析以 hello 最適當的方式。</span><span class="sxs-lookup"><span data-stu-id="78c2c-104">hello Team Data Science Process requires that data be ingested or loaded into a variety of different storage environments toobe processed or analyzed in hello most appropriate way in each stage of hello process.</span></span> <span data-ttu-id="78c2c-105">通常用於處理的資料目的地包括 Azure Blob 儲存體、SQL Azure 資料庫、Azure VM 上的 SQL Server、HDInsight (Hadoop) 和 Azure Machine Learning。</span><span class="sxs-lookup"><span data-stu-id="78c2c-105">Data destinations commonly used for processing include Azure Blob Storage, SQL Azure databases, SQL Server on Azure VM, HDInsight (Hadoop), and Azure Machine Learning.</span></span> 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="78c2c-106">這**功能表**連結 tootopics 描述 tooingest 資料插入這些目標的環境 hello 資料的位置儲存及處理的方式。</span><span class="sxs-lookup"><span data-stu-id="78c2c-106">This **menu** links tootopics that describe how tooingest data into these target environments where hello data is stored and processed.</span></span>

<span data-ttu-id="78c2c-107">技術和商務需求，以及 hello 初始位置，格式化，並將資料的大小會決定 hello 目標環境的 hello 到資料需要 toobe 內嵌的 tooachieve hello 目標分析。</span><span class="sxs-lookup"><span data-stu-id="78c2c-107">Technical and business needs, as well as hello initial location, format and size of your data will determine hello target environments into which hello data needs toobe ingested tooachieve hello goals of your analysis.</span></span> <span data-ttu-id="78c2c-108">是很常見的數個環境 tooachieve hello 各種不同的工作需要 tooconstruct 預測模型之間移動案例 toorequire 資料 toobe 的位置。</span><span class="sxs-lookup"><span data-stu-id="78c2c-108">It is not uncommon for a scenario toorequire data toobe moved between several environments tooachieve hello variety of tasks required tooconstruct a predictive model.</span></span> <span data-ttu-id="78c2c-109">比方說，這一系列工作可以包含資料瀏覽、前置處理、清除、向下取樣和模型定型。</span><span class="sxs-lookup"><span data-stu-id="78c2c-109">This sequence of tasks can include, for example, data exploration, pre-processing, cleaning, down-sampling, and model training.</span></span>

