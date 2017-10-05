---
title: "在 Azure Blob 容器、SQL Server 和 Hive 資料表中進行資料取樣 | Microsoft Docs"
description: "如何探索儲存在各種 Azure 環境中的資料。"
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
ms.openlocfilehash: 0683be564a88ef54882e8d882d196851ecac243d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="ec9b5-103"><a name="heading"></a>在 Azure Blob 容器、SQL Server 和 Hive 資料表中進行資料取樣</span><span class="sxs-lookup"><span data-stu-id="ec9b5-103"><a name="heading"></a>Sample data in Azure blob containers, SQL Server, and Hive tables</span></span>
<span data-ttu-id="ec9b5-104">本文件所連結的主題會說明如何對三個不同 Azure 位置中任一個位置所儲存的資料進行取樣：</span><span class="sxs-lookup"><span data-stu-id="ec9b5-104">This document links to topics that covers how to sample data that is stored in one of three different Azure locations:</span></span>

* <span data-ttu-id="ec9b5-105">**Azure blob 儲存體資料** ，然後使用 Python 程式碼範例來進行取樣，這是對 Azure blob 儲存體資料進行取樣的方式。</span><span class="sxs-lookup"><span data-stu-id="ec9b5-105">**Azure blob container data** is sampled by downloading it programmatically and then sampling it with sample Python code.</span></span>
* <span data-ttu-id="ec9b5-106">**SQL Server 資料** 進行取樣。</span><span class="sxs-lookup"><span data-stu-id="ec9b5-106">**SQL Server data** is sampled using both SQL and the Python Programming Language.</span></span> 
* <span data-ttu-id="ec9b5-107">**Hive 資料表** 進行取樣。</span><span class="sxs-lookup"><span data-stu-id="ec9b5-107">**Hive table data** is sampled using Hive queries.</span></span>

<span data-ttu-id="ec9b5-108">以下**功能表**所連結的主題會說明如何從這其中的每一個 Azure 儲存體環境進行資料取樣。</span><span class="sxs-lookup"><span data-stu-id="ec9b5-108">The following **menu** links to the topics that describe how to sample data from each of these Azure storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="ec9b5-109">這個取樣工作是 [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)中的一個步驟。</span><span class="sxs-lookup"><span data-stu-id="ec9b5-109">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

<span data-ttu-id="ec9b5-110">**為何要對資料進行取樣？**</span><span class="sxs-lookup"><span data-stu-id="ec9b5-110">**Why sample data?**</span></span>

<span data-ttu-id="ec9b5-111">如果您規劃分析的資料集很龐大，通常最好是對資料進行向下取樣，將資料縮減為更小但具代表性且更容易管理的大小。</span><span class="sxs-lookup"><span data-stu-id="ec9b5-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="ec9b5-112">這有助於資料了解、探索和功能工程。</span><span class="sxs-lookup"><span data-stu-id="ec9b5-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="ec9b5-113">它在 Cortana 分析程序中扮演的角色是能夠快速建立資料處理函式與機器學習服務模型的原型。</span><span class="sxs-lookup"><span data-stu-id="ec9b5-113">Its role in the Cortana Analytics Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

