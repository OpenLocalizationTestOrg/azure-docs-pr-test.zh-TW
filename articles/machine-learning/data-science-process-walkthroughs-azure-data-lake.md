---
title: "使用 U-SQL 的 Azure Data Lake 資料科學逐步解說 | Microsoft Docs"
description: "舉例逐步解說如何在 Azure Data Lake 上使用 U-SQL 來執行預測性分析。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: 118fd5167e67b8259cde8b6e672be325a41a842d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-data-lake-data-science-walkthroughs-using-u-sql"></a><span data-ttu-id="ce143-103">使用 U-SQL 的 Azure Data Lake 資料科學逐步解說</span><span class="sxs-lookup"><span data-stu-id="ce143-103">Azure Data Lake data science walkthroughs using U-SQL</span></span>

<span data-ttu-id="ce143-104">這些逐步解說會使用 U-SQL 搭配 Azure Data Lake 來執行預測性分析。</span><span class="sxs-lookup"><span data-stu-id="ce143-104">These walkthroughs use U-SQL with Azure Data Lake to do predictive analytics.</span></span> <span data-ttu-id="ce143-105">其遵循 Team Data Science Process 中所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="ce143-105">They follow the steps outlined in the Team Data Science Process.</span></span> <span data-ttu-id="ce143-106">如需 Team Data Science Process 的概觀，請參閱 [Data Science Process](data-science-process-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="ce143-106">For an overview of the Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> <span data-ttu-id="ce143-107">如需 Azure Data Lake 的簡介，請參閱 [Azure Data Lake Store 概觀](../data-lake-store/data-lake-store-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="ce143-107">For an introduction to Azure Data Lake, see [Overview of Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>

<span data-ttu-id="ce143-108">執行 Team Data Science Process 的其他資料科學逐步解說是依據它們使用的**平台**來歸納整理：</span><span class="sxs-lookup"><span data-stu-id="ce143-108">Additional data science walkthroughs that execute the Team Data Science Process are grouped by the **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-u-sql-with-azure-data-lake"></a><span data-ttu-id="ce143-109">使用 U-SQL 搭配 Azure Data Lake 來預測計程車小費</span><span class="sxs-lookup"><span data-stu-id="ce143-109">Predict taxi tips using U-SQL with Azure Data Lake</span></span>

<span data-ttu-id="ce143-110">[使用 Azure Data Lake 的資料科學](machine-learning-data-science-process-data-lake-walkthrough.md)逐步解說會示範如何使用 Azure Data Lake，在 NYC 計程車車程和車資資料集範例上執行資料探索和二元分類工作，以預測客戶是否給予小費。</span><span class="sxs-lookup"><span data-stu-id="ce143-110">The [Use Azure Data Lake for data science](machine-learning-data-science-process-data-lake-walkthrough.md) walkthrough shows how to use Azure Data Lake to do data exploration and binary classification tasks on a sample of the NYC taxi dataset to predict whether or not a tip is paid by a customer.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="ce143-111">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ce143-111">Next steps</span></span>

<span data-ttu-id="ce143-112">如需組成 Team Data Science Process 之主要元件的討論，請參閱 [Team Data Science Process 概觀](data-science-process-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="ce143-112">For a discussion of the key components that comprise the Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="ce143-113">如需您可以用來結構化資料科學專案之 Team Data Science Process 生命週期的討論，請參閱 [Team Data Science Process 生命週期](data-science-process-lifecycle.md)。</span><span class="sxs-lookup"><span data-stu-id="ce143-113">For a discussion of the Team Data Science Process lifecycle that you can use to structure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="ce143-114">生命週期會概述專案在執行時通常會遵循之從開始到完成的步驟。</span><span class="sxs-lookup"><span data-stu-id="ce143-114">The lifecycle outlines the steps, from start to finish, that projects usually follow when they are executed.</span></span> 