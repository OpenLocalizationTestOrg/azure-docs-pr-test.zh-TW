---
title: "在 Windows Azure microservices aaaDebug |Microsoft 文件"
description: "深入了解如何 toomonitor 及診斷您使用本機開發電腦上的 Microsoft Azure Service Fabric 撰寫的服務。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: edcc0631-ed2d-45a3-851d-2c4fa0f4a326
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/24/2017
ms.author: dekapur
ms.openlocfilehash: 24868aa194b8a28fa3e6de95c1de5506d912a544
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a>監視和診斷本機開發設定中的服務
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
> 
> 

監視、 偵測、 診斷及疑難排解允許服務 toocontinue 盡量減少 toohello 使用者體驗。 雖然監視和診斷重大的實際部署的生產環境中，hello 效率將取決於服務 tooensure 運作時移動 tooa 真實世界的安裝程式的開發期間採用類似的模型。 Service Fabric 輕鬆可以順暢地適用於所有單一電腦的本機開發的設定和實際生產環境叢集安裝的服務開發人員 tooimplement 診斷。

## <a name="event-tracing-for-windows"></a>Windows 的事件追蹤
[為 Windows 事件追蹤](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx)(ETW) 為 hello 建議技術，用於 Service Fabric 中追蹤訊息。 使用 ETW 的部分優點為：

* **ETW 相當快速。** 其是以一種追蹤技術建置而成，並對您程式碼執行時間的影響降到最低。
* **ETW 會在本機開發環境以及實際叢集設定順暢地進行追蹤。** 這表示您不需要您追蹤程式碼，當您準備好 toodeploy toorewrite 您程式碼 tooa 真實的叢集。
* **Service Fabric 系統程式碼也會將 ETW 用於內部追蹤。** 這可讓您 tooview 交錯 Service Fabric 的系統追蹤的應用程式追蹤。 它也可協助您 toomore 輕鬆瞭解 hello 基礎系統中的 hello 順序與您的應用程式程式碼與事件之間的相互關係。
* **沒有服務網狀架構的 Visual Studio 工具 中的內建支援 tooview ETW 事件。** 一旦 Visual Studio 已正確設定以 Service Fabric hello Visual Studio 的診斷事件 檢視中會出現 ETW 事件。 

## <a name="view-service-fabric-system-events-in-visual-studio"></a>在 Visual Studio 中檢視 Service Fabric 系統事件
Service Fabric 會發出 toohelp 應用程式開發人員了解為什麼在 hello 平台的 ETW 事件。 如果您尚未這麼做，請繼續進行，並依照中的 hello 步驟[Visual Studio 中建立第一個應用程式](service-fabric-create-your-first-application-in-visual-studio.md)。 這項資訊可協助您取得應用程式啟動並執行以 hello 診斷事件檢視器顯示 hello 追蹤訊息。

1. 如果 hello 診斷事件視窗不會自動顯示，當 toohello**檢視**Visual Studio 中的索引標籤上，選擇 **其他視窗**然後**診斷事件檢視器**。
2. 每一個事件有會告訴您 hello 節點、 應用程式及服務 hello 事件來自的標準中繼資料資訊。 您也可以篩選事件 hello 清單使用 hello**篩選事件**hello hello 事件視窗上方的方塊。 例如，您可以依 [節點名稱] 或 [服務名稱] 進行篩選。 當您在查看事件詳細資料，您也可以暫停使用 hello 和**暫停**hello hello 事件視窗上方的按鈕，然後稍後再繼續而不會遺失任何事件。
   
   ![Visual Studio 診斷事件檢視器](./media/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally/DiagEventsExamples2.png)

## <a name="add-your-own-custom-traces-toohello-application-code"></a>新增您自己自訂的追蹤 toohello 應用程式程式碼
hello Service Fabric Visual Studio 專案範本包含範例程式碼。 hello 程式碼會示範如何 tooadd 自訂應用程式程式碼 ETW 追蹤向上 hello Visual Studio ETW 檢視器，以及從服務網狀架構的系統追蹤中會顯示。 hello 這個方法的優點是中繼資料會自動加入 tootraces，，和 hello Visual Studio 診斷事件檢視器已設定 toodisplay 它們。

針對專案所建立的 hello**服務範本**（無狀態或狀態） 只搜尋 hello`RunAsync`實作：

1. 太 hello 呼叫`ServiceEventSource.Current.ServiceMessage`在 hello`RunAsync`方法顯示 hello 應用程式程式碼從自訂的 ETW 追蹤的範例。
2. 在 hello **ServiceEventSource.cs**檔案中，您會看到多載的 hello`ServiceEventSource.ServiceMessage`應該用於 tooperformance 原因由於高頻率事件的方法。

針對專案所建立的 hello**動作項目範本**（無狀態或狀態）：

1. 開啟 hello **"ProjectName".cs**檔案*ProjectName* hello 您選擇的 Visual Studio 專案的名稱。  
2. 找出 hello 程式碼`ActorEventSource.Current.ActorMessage(this, "Doing Work");`在 hello *DoWorkAsync*方法。  這是來自應用程式程式碼撰寫的自訂 ETW 追蹤範例。  
3. 在檔案中**ActorEventSource.cs**，您會看到多載的 hello`ActorEventSource.ActorMessage`應該用於 tooperformance 原因由於高頻率事件的方法。

加入自訂的 ETW 追蹤 tooyour 服務程式碼之後, 您可以建置、 部署和執行 hello 應用程式再次 toosee 您 hello 診斷事件檢視器中的事件。 如果您偵錯 hello 應用程式與**F5**，hello 診斷事件檢視器會自動開啟。

## <a name="next-steps"></a>後續步驟
hello 相同的追蹤程式碼加入 tooyour 本機診斷上述應用程式將使用工具，您可以使用 tooview Azure 的叢集上執行您的應用程式時，這些事件。 簽出這些文章會討論 hello 的 hello 工具的不同選項，並且描述如何設定這些。

* [Toocollect 使用 Azure 診斷的記錄檔](service-fabric-diagnostics-how-to-setup-wad.md)
* [使用 EventFlow 的事件彙總與集合](service-fabric-diagnostics-event-aggregation-eventflow.md)

