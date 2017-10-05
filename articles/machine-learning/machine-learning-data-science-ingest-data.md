---
title: "將資料載入至 Azure 儲存體環境以便進行分析 | Microsoft Docs"
description: "從 Azure Blob 儲存體來回移動資料"
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
ms.openlocfilehash: 7fbf3bfedca8fa57a5e9428c9399558992b4acbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a><span data-ttu-id="fc8ee-103">將資料載入至儲存體環境以便進行分析</span><span class="sxs-lookup"><span data-stu-id="fc8ee-103">Load data into storage environments for analytics</span></span>
<span data-ttu-id="fc8ee-104">Team Data Science Process 要求將資料內嵌或載入至各種不同的儲存體環境，以便在程序的每個階段中以最適當的方式處理或分析。</span><span class="sxs-lookup"><span data-stu-id="fc8ee-104">The Team Data Science Process requires that data be ingested or loaded into a variety of different storage environments to be processed or analyzed in the most appropriate way in each stage of the process.</span></span> <span data-ttu-id="fc8ee-105">通常用於處理的資料目的地包括 Azure Blob 儲存體、SQL Azure 資料庫、Azure VM 上的 SQL Server、HDInsight (Hadoop) 和 Azure Machine Learning。</span><span class="sxs-lookup"><span data-stu-id="fc8ee-105">Data destinations commonly used for processing include Azure Blob Storage, SQL Azure databases, SQL Server on Azure VM, HDInsight (Hadoop), and Azure Machine Learning.</span></span> 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="fc8ee-106">此 **功能表** 所連結的主題會說明如何將資料內嵌至可儲存和處理資料的目標環境。</span><span class="sxs-lookup"><span data-stu-id="fc8ee-106">This **menu** links to topics that describe how to ingest data into these target environments where the data is stored and processed.</span></span>

<span data-ttu-id="fc8ee-107">技術和商務需求以及資料的初始位置、格式和大小，會決定需要擷取資料到其中的目標環境以達成您的分析目標。</span><span class="sxs-lookup"><span data-stu-id="fc8ee-107">Technical and business needs, as well as the initial location, format and size of your data will determine the target environments into which the data needs to be ingested to achieve the goals of your analysis.</span></span> <span data-ttu-id="fc8ee-108">以下案例並不常見：要求在數個環境之間移動資料來達成建構預測模型所需的各種工作。</span><span class="sxs-lookup"><span data-stu-id="fc8ee-108">It is not uncommon for a scenario to require data to be moved between several environments to achieve the variety of tasks required to construct a predictive model.</span></span> <span data-ttu-id="fc8ee-109">比方說，這一系列工作可以包含資料瀏覽、前置處理、清除、向下取樣和模型定型。</span><span class="sxs-lookup"><span data-stu-id="fc8ee-109">This sequence of tasks can include, for example, data exploration, pre-processing, cleaning, down-sampling, and model training.</span></span>

