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
# <a name="heading"></a>在 Azure Blob 容器、SQL Server 和 Hive 資料表中進行資料取樣
這份文件連結，它涵蓋了 tootopics 如何 toosample 資料儲存在三個不同的 Azure 位置的其中一個：

* **Azure blob 儲存體資料** ，然後使用 Python 程式碼範例來進行取樣，這是對 Azure blob 儲存體資料進行取樣的方式。
* **SQL Server 資料**取樣使用 SQL 和 hello Python 程式設計語言。 
* **Hive 資料表** 進行取樣。

hello 下列**功能表**連結 toohello 主題描述如何從每個 Azure 儲存體環境 toosample 資料。 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

此取樣工作是在 hello 步驟[小組資料科學程序 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)。

**為何要對資料進行取樣？**

如果您計劃 tooanalyze hello 資料集很大，它通常是個不錯的主意 toodown 範例 hello 資料 tooreduce 它 tooa 小型但具代表性且更容易管理的大小。 這有助於資料了解、探索和功能工程。 Hello Cortana 分析程序在其角色將是 tooenable 快速原型化的 hello 資料處理函式和機器學習模型。

