---
title: "在 Azure 中的 aaaSample 資料 blob 容器，SQL Server 和 Hive 資料表 |Microsoft 文件"
description: "Tooexplore 資料如何儲存在各種 Azure enviromnents。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 80a9dfae-e3a6-4cfb-aecc-5701cfc7e39d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5a5295b59fa02f91da680fc7495a92ca135e26c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="d9b65-103"><a name="heading"></a>在 Azure Blob 容器、SQL Server 和 Hive 資料表中進行資料取樣</span><span class="sxs-lookup"><span data-stu-id="d9b65-103"><a name="heading"></a>Sample data in Azure blob containers, SQL Server, and Hive tables</span></span>
<span data-ttu-id="d9b65-104">這份文件連結，它涵蓋了 tootopics 如何 toosample 資料儲存在三個不同的 Azure 位置的其中一個：</span><span class="sxs-lookup"><span data-stu-id="d9b65-104">This document links tootopics that covers how toosample data that is stored in one of three different Azure locations:</span></span>

* <span data-ttu-id="d9b65-105">**Azure blob 儲存體資料** ，然後使用 Python 程式碼範例來進行取樣，這是對 Azure blob 儲存體資料進行取樣的方式。</span><span class="sxs-lookup"><span data-stu-id="d9b65-105">**Azure blob container data** is sampled by downloading it programmatically and then sampling it with sample Python code.</span></span>
* <span data-ttu-id="d9b65-106">**SQL Server 資料**取樣使用 SQL 和 hello Python 程式設計語言。</span><span class="sxs-lookup"><span data-stu-id="d9b65-106">**SQL Server data** is sampled using both SQL and hello Python Programming Language.</span></span> 
* <span data-ttu-id="d9b65-107">**Hive 資料表** 進行取樣。</span><span class="sxs-lookup"><span data-stu-id="d9b65-107">**Hive table data** is sampled using Hive queries.</span></span>

<span data-ttu-id="d9b65-108">hello 下列**功能表**連結 toohello 主題描述如何從每個 Azure 儲存體環境 toosample 資料。</span><span class="sxs-lookup"><span data-stu-id="d9b65-108">hello following **menu** links toohello topics that describe how toosample data from each of these Azure storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="d9b65-109">此取樣工作是在 hello 步驟[小組資料科學程序 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)。</span><span class="sxs-lookup"><span data-stu-id="d9b65-109">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

<span data-ttu-id="d9b65-110">**為何要對資料進行取樣？**</span><span class="sxs-lookup"><span data-stu-id="d9b65-110">**Why sample data?**</span></span>

<span data-ttu-id="d9b65-111">如果您計劃 tooanalyze hello 資料集很大，它通常是個不錯的主意 toodown 範例 hello 資料 tooreduce 它 tooa 小型但具代表性且更容易管理的大小。</span><span class="sxs-lookup"><span data-stu-id="d9b65-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="d9b65-112">這有助於資料了解、探索和功能工程。</span><span class="sxs-lookup"><span data-stu-id="d9b65-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="d9b65-113">Hello Cortana 分析程序在其角色將是 tooenable 快速原型化的 hello 資料處理函式和機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="d9b65-113">Its role in hello Cortana Analytics Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

