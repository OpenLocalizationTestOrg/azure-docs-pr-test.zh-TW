---
title: "aaaAzure 批次在 hello 雲端執行大規模的平行運算解決方案 |Microsoft 文件"
description: "了解如何使用 hello Azure 批次服務針對大規模的平行和 HPC 工作負載"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 93e37d44-7585-495e-8491-312ed584ab79
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: acc52e46330c465f81951441d9067371098cf63a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-intrinsically-parallel-workloads-with-batch"></a>使用 Batch 執行本質平行的工作負載

Azure 批次是 hello 雲端中有效率地執行大規模平行和高效能運算 (HPC) 應用程式的平台服務。 Azure 批次排程需要大量計算工作 toorun 上受管理的虛擬機器的集合，並可自動調整計算資源 toomeet hello 需求的工作。

透過 Azure 批次中，您可以輕鬆地定義 Azure 計算資源 tooexecute 應用程式以平行方式，而是在標尺。 沒有任何需要 toomanually 建立、 設定和管理 HPC 叢集、 個別的虛擬機器、 虛擬網路或複雜的工作和工作排程基礎結構。 Azure Batch 會為您自動執行或簡化這些工作。

## <a name="use-cases-for-batch"></a>Batch 的使用案例
Batch 是一項受管理的 Azure 服務，可用於批次處理或批次運算 -- 執行大量的類似工作以得到期望的結果。 定期處理、轉換和分析大量資料的組織最常使用批次運算。

Batch 很適合處理本質平行 (也稱為「超簡單平行」) 的應用程式和工作負載。 本質上平行的工作負載可輕易分割成多個工作，以在多部電腦上同時執行。

![平行工作][1]<br/>

常見使用這項技術處理的一些工作負載範例如下：

* 財務風險模型
* 氣候和水文資料分析
* 影像轉譯、分析和處理
* 媒體編碼及轉碼
* 基因序列分析
* 工程壓力分析
* 軟體測試

批次也可以執行平行計算 hello 結尾減少步驟，並執行更複雜的 HPC 工作負載，例如[訊息傳遞介面 (MPI)](batch-mpi.md)應用程式。

如需 Batch 與 Azure 中其他 HPC 解決方案選項的比較，請參閱 [Batch 和 HPC 解決方案](batch-hpc-solutions.md)。

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="scenario-scale-out-a-parallel-workload"></a>案例：相應放大平行工作負載
使用 hello 批次 Api toointeract 以 hello 批次服務的常見解決方案牽涉到向外延展本質平行工作-例如 hello 轉譯的 3D 場景-的運算節點的集區上的影像。 此集區的計算節點可以是您 「 轉譯伺服陣列 」，提供數十、 數百或甚至數千個核心 tooyour 轉譯工作，例如。

hello 下列圖表顯示常見的批次工作流程，用戶端應用程式或裝載的服務使用批次 toorun 平行的工作負載。

![Batch 解決方案工作流程][2]

在這個常見的案例中，應用程式或服務來處理 Azure 批次中的運算工作負載上執行下列步驟的 hello:

1. 上傳 hello**輸入檔**和 hello**應用程式**，將會處理這些檔案 tooyour Azure 儲存體帳戶。 hello 輸入的檔可以是會處理您的應用程式，例如財務模型化資料或視訊檔案 toobe 轉碼任何資料。 hello 應用程式檔案可以用於處理 hello 資料，例如 3D 呈現應用程式或媒體轉碼程式的任何應用程式。
2. 建立批次**集區**的運算節點，在您的 Batch 帳戶-這些節點 hello 的虛擬機器並將執行您的工作。 您指定屬性，例如 hello[節點大小](../cloud-services/cloud-services-sizes-specs.md)、 其作業系統和 Azure 儲存體中的 hello 應用程式 tooinstall hello 節點加入 hello 集區 （hello 應用程式，您在步驟 1 中上傳） 時的 hello 位置。 您也可以太設定 hello 集區[自動縮放表單](batch-automatic-scaling.md)回應 toohello 工作負載會產生您的工作中。 自動調整動態調整 hello hello 集區中的運算節點數目。
3. 建立批次**作業**toorun hello 工作負載的運算節點的 hello 集區上。 當您建立作業時，您需要將它與 Batch 集區建立關聯。
4. 新增**工作**toohello 作業。 當您新增工作 tooa 作業時，hello 批次服務會自動排程 hello hello 集區中的 hello 計算節點上執行的工作。 每項工作會使用您上傳 tooprocess hello 輸入的檔的 hello 應用程式。
   
   * 4a. 工作會執行之前，它可以下載它是指派給 tooprocess toohello 計算節點的 hello 資料 （hello 輸入檔案）。 如果 hello 應用程式未安裝 hello 節點上 （請參閱步驟 2），它可以在這裡下載改為。 Hello 下載完成時，會在其指派的節點上執行 hello 工作。
5. Hello 工作執行時，您可以查詢 hello 工作和其工作批次 toomonitor hello 進度。 用戶端應用程式或服務透過 HTTPS 通訊以 hello 批次服務。 因為您可能會監視數千個數千個計算節點上執行的工作，請務必太[有效率地查詢 hello 批次服務](batch-efficient-list-queries.md)。
6. 當 hello 工作完成時，他們可以上傳其結果資料 tooAzure 儲存體。 您也可以直接從 hello 計算節點上的檔案系統擷取檔案。
7. 當您的監視偵測到您的工作中的 hello 工作都完成後時，用戶端應用程式或服務可以下載 hello 做進一步處理或評估的輸出資料。

請記住，這是其中一個方法 toouse 批次，以及這個案例說明僅提供少數可用的功能。 例如，您可以執行[多項工作的平行](batch-parallel-node-tasks.md)上每個計算節點，而且您可以使用[作業準備與完成工作](batch-job-prep-release.md)tooprepare hello 節點為您的工作，然後清除之後。

## <a name="next-steps"></a>後續步驟
現在您擁有 hello 批次服務的高階概觀，它是時間 toodig 更深入 toolearn 您可以如何使用它 tooprocess 需要大量計算的平行工作負載。

* 讀取 hello[批次功能概觀，讓開發人員](batch-api-basics.md)，任何人準備 toouse 批次的重要資訊。 hello 發行項包含許多建置批次應用程式時，可以使用的 API 功能的批次服務資源集區、 節點、 工作和工作和 hello，如需詳細的資訊。
* 深入了解 hello[批次應用程式開發介面和工具](batch-apis-tools.md)可用來建置批次的解決方案。
* [開始使用 hello Azure Batch library for.NET](batch-dotnet-get-started.md) toolearn 如何 toouse C# 和 hello 批次.NET 程式庫 tooexecute 簡單的工作負載使用常見的批次工作流程。 這篇文章應為其中一個您同時學習如何 toouse hello 批次服務的第一個停止。 另外還有[Python 版本](batch-python-tutorial.md)hello 教學課程。
* 下載 hello[程式碼範例在 GitHub 上的][ github_samples] toosee C# 和 Python 與批次 tooschedule 和程序範例工作負載可以互動方式。
* 簽出 hello[批次學習路徑][ learning_path] tooget hello 資源可用 tooyou 您了解學習 toowork 與批次。


[github_samples]: https://github.com/Azure/azure-batch-samples
[learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/

[1]: ./media/batch-technical-overview/tech_overview_01.png
[2]: ./media/batch-technical-overview/tech_overview_02.png
