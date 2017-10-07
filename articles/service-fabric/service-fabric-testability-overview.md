---
title: "aaaFault Analysis Service 概觀 |Microsoft 文件"
description: "這篇文章描述 hello 錯誤分析服務，Service Fabric 中由引發錯誤，而針對您的服務執行測試案例。"
services: service-fabric
documentationcenter: .net
author: anmolah
manager: timlt
editor: vturecek
ms.assetid: 1f064276-293a-4989-a513-e0d0b9fdf703
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: anmola
ms.openlocfilehash: deac16ec830aa10d4e488e60691faa9ef2b6cd33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-fault-analysis-service"></a>簡介 toohello 錯誤 Analysis Service
hello 錯誤分析服務被設計用於測試 Microsoft Azure Service Fabric 建立的服務。 以 hello 錯誤分析服務，您可以產生有意義的錯誤，並對您的應用程式執行完成的測試案例。 這些錯誤和情況下執行，並驗證 hello 許多狀態和轉換，服務會在其存留期，發生在受控制、 安全且一致的方式。

動作是 hello 個別錯誤目標服務，以用於進行測試。 服務開發人員可以使用這些建置組塊 toowrite 複雜的案例。 例如：

* 重新啟動節點 toosimulate 任意數目的其中一部電腦或 VM 重新開機的情況。
* 移動您可設定狀態服務 toosimulate 負載平衡、 容錯移轉或應用程式升級的複本。
* 叫用上可設定狀態服務 toocreate 其中寫入作業無法繼續進行，因為沒有足夠的 「 備份 」 或"secondary"複本 tooaccept 新資料的情況下遺失仲裁。
* 叫用可設定狀態服務 toocreate 完全時抹除所有記憶體中狀態的情況下遺失資料。

案例都是一個或多個動作組成的複雜作業。 hello 錯誤分析服務提供兩個內建的完整案例：

* 混亂案例
* 容錯移轉案例

## <a name="testing-as-a-service"></a>測試即服務
hello 錯誤 Analysis Service 是以 Service Fabric 叢集時，會自動啟動服務網狀架構系統服務。 此服務做為錯誤資料隱碼、 測試案例執行時，和健全狀況分析的 hello 主機。 

![錯誤分析服務][0]

起始錯誤動作或測試案例時，將命令傳送 toohello 錯誤 Analysis Service toorun hello 錯誤動作或測試案例。 hello 錯誤分析服務是可設定狀態，使其能夠可靠地執行錯誤和狀況和驗證結果。 例如，您可以可靠地由 hello 錯誤 Analysis Service 執行長時間執行的測試案例。 而且因為 hello 叢集內正在執行測試，hello 服務可以檢查 hello hello 叢集狀態，且服務 tooprovide 有關失敗的更多深入資訊。

## <a name="testing-distributed-systems"></a>測試分散式系統
服務網狀架構可讓撰寫和管理分散式可擴充的應用程式大幅簡化的 hello 作業。 hello 錯誤分析服務可讓測試更容易同樣的分散式應用程式。 有三個主要問題需要 toobe 解決測試時：

1. 模擬/產生真實世界案例中可能發生的失敗： hello 的 Service Fabric 的重要層面的其中一個是它可讓分散式應用程式 toorecover 從各種失敗情況。 不過，hello 應用程式的 tootest 無法從這些失敗 toorecover，我們需要機制 toosimulate/產生這些受控制的測試環境中的真實世界失敗。
2. hello 能力 toogenerate 相互關聯失敗： hello 的系統，例如網路故障而機器失敗的基本失敗是個別地輕鬆 tooproduce。 產生大量可能是因為這些個別的失敗情況 hello 互動 hello 真實世界中的案例是重要的。
3. 跨各種開發和部署層級的統一經驗：許多錯誤插入系統都能讓您執行各種類型的失敗。 不過，hello 體驗中所有的這些不佳，從一個方塊開發人員的案例，toorunning hello 相同 toousing 大的測試環境中測試的測試生產環境中時。

雖然還有許多機制 toosolve 這些問題，並使用所需的保證-所有從一個方塊開發人員環境的 hello 方式 hello 相同的系統在實際執行叢集-tootest 遺失。 hello 錯誤分析服務可協助 hello 應用程式開發人員專注於測試其商務邏輯。 hello 錯誤 Analysis Service 提供所有 hello 功能所都需 tootest hello 與互動的 hello 服務 hello 基礎分散式系統。

### <a name="simulatinggenerating-real-world-failure-scenarios"></a>模擬/產生真實失敗案例
tootest hello 強固性的分散式系統故障，我們需要機制 toogenerate 失敗。 在理論上，產生失敗下, 一個節點看起來很簡單，同時也會叫用 hello 像相同集一致性問題的 Service Fabric 正嘗試 toosolve。 例如，如果我們想要關閉一個節點，tooshut hello 所需工作流程是 hello 下列：

1. 從用戶端 hello 發出關機節點要求。
2. 傳送嗨要求 toohello 正確節點。
   
    a. 如果找不到 hello 節點，它應該會失敗。
   
    b. 如果找到 hello 節點，則會傳回只当 hello 節點已關閉。

從測試檢視方塊 tooverify hello 失敗，hello 測試需要 tooknow 引發此錯誤，當 hello 失敗實際發生的。 Service Fabric 提供的 hello 保證是任一個 hello 節點會當機，或已關閉時 hello 命令已達到 hello 節點。 中任一案例 hello 測試應該是可以 toocorrectly hello 狀態相關的原因和 succeed 或 fail 正確其驗證。 實作 Service Fabric toodo hello 相同設定的失敗可能有許多網路叫用、 硬體和軟體的問題，而這可避免無法提供 hello 上述保證外部系統。 中的 hello 問題之前，Service Fabric 會重新設定 hello 叢集狀態 toowork 周圍 hello 問題，並因此 hello 錯誤 Analysis Service 所述的 hello 存在仍然會被可以 toogive hello 正確設定的保證。

### <a name="generating-required-events-and-scenarios"></a>產生必要的事件和案例
一致地模擬真實世界失敗是很難使用 toostart，是即使堅固 hello 能力 toogenerate 相互關聯失敗。 比方說，不會遺失資料的可設定狀態的持續性服務在 hello 遵循事情發生時：

1. 複寫僅寫入複本的仲裁 hello 會趕上狀態。 所有的 hello 次要複本落後於主要 hello。
2. 因為停機 （因為 tooa 程式碼封裝或往下的節點） 的 hello 複本關閉 hello 寫入仲裁。
3. hello 寫入仲裁無法恢復因為 hello 複本 hello 資料已遺失 （因為 toodisk 損毀或電腦重新安裝映像）。

這些相互關聯的失敗發生 hello 真實世界中，但是經常為個別的失敗。 這些案例之前仍發生在生產環境中的 hello 能力 tootest 相當重要。 更重要的是 hello 能力 toosimulate 生產工作負載在受控制的情況下使用這些案例 （在 hello 中間的投影片上的所有工程師 hello 天）。 這是比較好，比起其 hello 發生在上午 2:00 的生產環境中的第一次

### <a name="unified-experience-across-different-environments"></a>跨不同環境的統一經驗
hello 練習一直都 toocreate 三組不同的體驗，一個用於 hello 開發環境，另一個用於測試，，一個是正式用途。 hello 模型為：

1. 在 hello 開發環境中，會產生允許個別方法的單元測試的狀態轉換。
2. 在 hello 測試環境中，會產生失敗 tooallow 端對端測試，以執行各種失敗狀況。
3. 任何非自然失敗和 tooensure 是非常快速的人力回應 toofailure 保留 hello 實際執行環境原有 tooprevent。

Service Fabric 中透過 hello 錯誤分析服務，我們正在提議 tooturn 這周圍，並使用 hello 相同從開發人員環境 tooproduction 方法。 有兩種方式 tooachieve 這樣：

1. tooinduce 控制失敗，使用從一個方塊環境的 hello 錯誤分析服務 Api 所有 hello 方式 tooproduction 叢集。
2. toogive hello 叢集會自動失敗造成的失敗，使用 hello 錯誤 Analysis Service toogenerate 自動歸納相思。 透過組態失敗的控制 hello 速率可讓相同的服務 toobe 測試以不同的方式在不同環境的 hello。

Service Fabric 與 hello 標尺的失敗是不同的 hello 不同環境中，雖然 hello 實際機制就會相同。 這可讓多速度較快的程式碼來部署管線和 hello 能力 tootest hello 服務在真實世界負載。

## <a name="using-hello-fault-analysis-service"></a>使用 hello 錯誤 Analysis Service
**C#**

錯誤 Analysis Service 功能可在 hello Microsoft.ServiceFabric NuGet 封裝中的 hello System.Fabric 命名空間中。 toouse hello 錯誤 Analysis Service 功能，包括做為參考您的專案中的 hello nuget 封裝。

**PowerShell**

toouse PowerShell，您必須安裝 hello Service Fabric SDK。 安裝 SDK，hello hello ServiceFabric PowerShell 模組之後自動為您 toouse 載入。

## <a name="next-steps"></a>後續步驟
toocreate 真正雲端規模服務很重要的 tooensure 同時部署之前和之後，服務可以承受真實世界失敗。 在服務好今天，快速 hello 能力 tooinnovate，快速移動程式碼 tooproduction 是非常重要。 hello 錯誤分析服務有助於服務開發人員 toodo 精確。

開始測試您的應用程式和服務使用 hello 內建[測試案例](service-fabric-testability-scenarios.md)，或撰寫您自己的測試案例使用 hello[錯誤動作](service-fabric-testability-actions.md)hello 錯誤分析服務所提供。

<!--Image references-->
[0]: ./media/service-fabric-testability-overview/faultanalysisservice.png
