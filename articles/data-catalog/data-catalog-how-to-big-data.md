---
title: "與 「 偉大資料 」 資料來源的 aaaHow toowork |Microsoft 文件"
description: "如何 tooarticle 反白顯示的 「 偉大資料 」 的資料來源，包括 Azure Blob 儲存體、 Azure 資料湖，Hadoop HDFS 搭配使用 Azure 資料目錄的模式。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 626d1568-0780-4726-bad1-9c5000c6b31a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: e478f71f26744975a7d7e1784b74bf50b424cf65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowork-with-big-data-sources-in-azure-data-catalog"></a>在 Azure 資料目錄中 toowork 大型資料來源的方式
## <a name="introduction"></a>簡介
**Microsoft Azure 資料目錄** 是全面管理的雲端服務，可作為企業資料來源的註冊系統和探索系統。 它就是要協助大眾探索、 了解，以及使用資料來源，以及幫助組織 tooget 多個值，從其現有的資料來源，包括巨量資料。

**Azure 資料目錄**支援 hello 註冊的 Azure Blob 儲存體 blob 和目錄，以及 Hadoop HDFS 檔案及目錄。 hello 半結構化的本質，這些資料來源的提供很大的彈性。 不過，tooget hello 大部分的值從註冊它們與**Azure 資料目錄**，使用者必須考慮如何組織 hello 資料來源。

## <a name="directories-as-logical-data-sets"></a>將目錄視為邏輯資料集
組織大型資料來源的常見模式為邏輯的資料集是 tootreat 目錄。 最上層目錄會使用的 toodefine 資料集，而子資料夾定義資料分割，及它們所包含的 hello 檔案儲存 hello 資料本身。

此模式的可能範例如下：

    \vehicle_maintenance_events
        \2013
        \2014
        \2015
            \01
                \2015-01-trailer01.csv
                \2015-01-trailer92.csv
                \2015-01-canister9635.csv
                ...
    \location_tracking_events
        \2013
        ...

在此範例中，vehicle_maintenance_events 和 location_tracking_events 代表邏輯資料集。 上述每個資料夾包含資料檔案，依據年份和月份組織成子資料夾。 上述每個資料夾可能包含數百或數千個檔案。

在此模式中，向 **Azure 資料目錄** 註冊個別的檔案毫無意義。 相反地，註冊代表 hello 是有意義的 toohello 使用者使用 hello 資料的資料集的 hello 目錄。

## <a name="reference-data-files"></a>參考資料檔案
互補的模式是 toostore 參考資料集，以個別檔案。 這些資料集可能會視為 hello '小' 端的巨量資料，而且通常會類似 toodimensions 分析資料模型中。 參考資料檔案包含的記錄，使用的 tooprovide hello 大量 hello 資料檔案儲存在 hello 巨量資料存放區中的其他位置的內容。

此模式的可能範例如下：

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

當分析師或資料科學家便可使用 hello 較大的目錄結構中所含的 hello 資料時，這些參考檔案中的 hello 資料可以是使用的 tooprovide 的詳細資訊的實體的參考 tooonly 依名稱或識別碼 hello 較大的資料設定。

在這種模式是合理 tooregister hello 個別參考的資料檔案與**Azure 資料目錄**。 每個檔案都代表資料集，且每個都可以加上附註和個別地探索。

## <a name="alternate-patterns"></a>替代模式
hello hello 前面一節中所述的模式只有兩個可能的方式，可能會組織巨量資料存放區，但是每個實作不同。 不論您的資料來源的結構方式，註冊使用大型資料來源時**Azure 資料目錄**，專注於註冊 hello 檔案和目錄的代表 hello 資料集內的值 tooothers 的程式組織。 註冊的所有檔案和目錄可以干擾 hello 類別目錄，難度的使用者 toofind 他們的需要。

## <a name="summary"></a>摘要
註冊具有的資料來源**Azure 資料目錄**使其更容易 toodiscover 並了解。 登錄及註解 hello 巨量資料檔案和目錄的代表邏輯資料集，您可以協助使用者尋找並使用所需的 hello 巨量資料來源。
