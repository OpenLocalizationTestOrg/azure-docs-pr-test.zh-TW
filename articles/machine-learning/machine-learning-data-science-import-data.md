---
title: "Machine Learning Studio aaaImport 資料 |Microsoft 文件"
description: "如何 tooimport 您 Azure Machine Learning Studio 從各種資料來源的資料。 了解支援的資料類型和資料格式。"
keywords: "匯入資料,資料格式,資料類型,資料來源,定型資料"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: garye;bradsev
ms.openlocfilehash: 830dcdde9d43809900c520a41d6d94a65731ca3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a>從各種資料來源將訓練資料匯入 Azure Machine Learning Studio
toouse 自己在 Machine Learning Studio toodevelop 和定型預測性分析方案中的資料，您可以： 

* 從資料上傳**本機檔案**提前時間從硬碟機 toocreate 工作區中的資料集模組
* 存取資料，從一種**線上資料來源**實驗執行時使用 hello[匯入資料][ import-data]模組 
* 使用其他 Azure Machine Learning **實驗**中儲存為資料集的資料
* 使用內部部署 **SQL Server 資料庫**中的資料

每個選項所述其中一個 hello 主題下方的 hello 功能表上。 這些主題顯示如何從各種資料 tooimport 資料來源 toouse Machine Learning Studio 中。 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> Machine Learning Studio 中有一些可用於訓練資料的範例資料集。 如需這些資訊，請參閱[使用 Azure Machine Learning Studio 中的 hello 範例資料集](machine-learning-use-sample-datasets.md))。
> 
> 

這個簡介主題也會討論 tooget 資料供 Machine Learning Studio 中的使用方式，並描述支援的資料格式和資料類型。 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a>備妥資料以在 Azure Machine Learning Studio 中使用
Machine Learning Studio 是設計的 toowork 矩形或表格式資料，例如結構化資料，從資料庫，不過，在某些情況下可能會使用非矩形的資料或分隔的文字資料。

如果您的資料相對乾淨是最佳狀況。 也就是說，您會想 tootake care of 問題，例如未加引號的字串之前，您將 hello 資料上傳到您的經驗。

但是，Machine Learning Studio 中有模組可讓您在實驗中進行一些資料操作。 根據您要使用的 hello 機器學習演算法，您可能會如何需要 toodecide 您將處理資料結構的問題，例如遺漏值和疏鬆的資料，且可以有幫助的模組。 查看 hello**資料轉換**hello 模組調色盤的模組，執行這些功能的一節。

在您實驗中的任何一點，您可以檢視或下載 hello 按一下 hello 輸出連接埠模組所產生的資料。 根據 hello 模組可能會有不同的下載選項可用，或者您可能無法 toovisualize hello 資料在 Machine Learning Studio 中 web 瀏覽器。

## <a name="data-formats-and-data-types-supported"></a>支援的資料格式和資料類型
您可以數種資料類型匯入您的經驗，根據哪些機制使用 tooimport 資料和此流量來自：

* 純文字 (.txt)
* 逗號分隔值 (CSV)，具有標頭 (.csv) 或不具標頭 (.nh.csv)
* 定位鍵分隔值 (TSV)，具有標頭 (.tsv) 或不具標頭 (.nh.tsv)
* Excel 檔案
* Azure 資料表
* Hive 資料表
* SQL 資料庫資料表
* OData 值
* SVMLight 資料 (.svmlight) (請參閱 hello [SVMLight 定義](http://svmlight.joachims.org/)格式資訊)
* 屬性關聯檔案格式 (ARFF) 資料 (.arff) (請參閱 hello [ARFF 定義](http://weka.wikispaces.com/ARFF)格式資訊)
* Zip 檔案 (.zip)
* R 物件或工作區檔案 (.RData)

如果您匯入資料例如 ARFF 包含中繼資料的格式，Machine Learning Studio 會使用此中繼資料 toodefine hello 標題和每個資料行的資料類型。

如果您匯入資料，例如不包含這個中繼資料的 TSV 或 CSV 格式，Machine Learning Studio 就會由取樣 hello 資料推斷 hello 每個資料行的資料類型。 如果 hello 資料也不會有資料行標題，Machine Learning Studio 提供預設名稱。

您可以明確指定或變更 hello 標題和資料類型資料行使用 hello[編輯中繼資料][edit-metadata]。

hello 下列**資料型別**Machine Learning Studio 可辨識：

* String
* Integer
* 兩倍
* Boolean
* DateTime
* 時間範圍

Machine Learning Studio 使用內部的資料類型呼叫***資料表***toopass 模組之間的資料。 您可以明確將資料轉換成資料表格式使用 hello[轉換 tooDataset] [ convert-to-dataset]模組。

任何模組可接受資料表以外的格式會以無訊息模式轉換 hello 資料 tooData 資料表，再將其傳遞 toohello 下一個模組。

您可以視需要使用其他轉換模組，將「資料表格」格式轉換回 CSV、TSV、ARFF 或 SVMLight 格式。
查看 hello**資料格式轉換**hello 模組調色盤的模組，執行這些功能的一節。

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
