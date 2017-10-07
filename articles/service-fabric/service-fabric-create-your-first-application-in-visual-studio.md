---
title: "aaaCreate Azure Service Fabric 可靠的服務使用 C#"
description: "使用 Visual Studio，建立、部署和偵錯以 Azure Service Fabric 為建置基礎的 Reliable Service 應用程式。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 740c866da6e639219b529fe92ed63cbeaa702a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a>建立第一個 C# Service Fabric 具狀態 Reliable Services 應用程式

深入了解如何 toodeploy 第一個 Service Fabric 應用程式在 Windows 上的.net 在短短幾分鐘內。 當您完成時，將會有以可靠服務應用程式執行的本機叢集。

## <a name="prerequisites"></a>必要條件

開始之前，請確定您已 [設定開發環境](service-fabric-get-started.md)。 這包括安裝 hello Service Fabric SDK 及 Visual Studio 2017 或 2015年。

## <a name="create-hello-application"></a>建立 hello 應用程式

以**系統管理員**身分啟動 Visual Studio。

使用 `CTRL`+`SHIFT`+`N` 建立專案

在 [hello**新專案**] 對話方塊中，選擇**雲端 > Service Fabric 應用程式**。

Hello 應用程式命名**MyApplication**按**確定**。

   
![Visual Studio 中的新增專案對話方塊][1]

您可以從 hello 下一步 對話方塊建立 Service Fabric 應用程式的任何型別。 在本快速入門中，選擇 [具狀態服務]。

Hello 服務名稱**MyStatefulService**按**確定**。

![Visual Studio 中的新增服務對話方塊][2]


Visual Studio 會建立 hello 應用程式專案和 hello 可設定狀態的服務專案，並顯示在 [方案總管] 中。

![使用具狀態服務建立應用程式後的方案總管][3]

hello 應用程式專案 (**MyApplication**) 直接不包含任何程式碼。 它反而會參考一組服務專案。 此外，它包含三種其他類型的內容：

* **發佈設定檔**  
部署 toodifferent 環境的設定檔。

* **指令碼**  
包含用來部署/升級應用程式的 PowerShell 指令碼。

* **應用程式定義**  
包含下的 hello ApplicationManifest.xml 檔案*ApplicationPackageRoot*用來描述應用程式的組合。 相關聯的應用程式參數檔案受到*ApplicationParameters*，它可以是使用的 toospecify 環境特有的參數。 Hello 中指定的應用程式參數檔案相關聯的 visual Studio 選取 tooa 特定環境時，部署期間發行設定檔。
    
如需 hello hello 服務專案內容的概觀，請參閱[可靠的服務入門](service-fabric-reliable-services-quick-start.md)。

## <a name="deploy-and-debug-hello-application"></a>部署和偵錯 hello 應用程式

請執行您現有的應用程式。

在 Visual Studio 中，按`F5`toodeploy hello 應用程式進行偵錯。

>[!NOTE]
>hello 第一次執行，並部署 hello 應用程式在本機，Visual Studio 會建立偵錯的本機叢集。 這可能需要一些時間。 hello Visual Studio 輸出 視窗中會顯示 hello 叢集建立狀態。

Hello 叢集就緒時，您會收到通知，從 hello 本機叢集系統匣管理員應用程式隨附 hello SDK。
   
![本機叢集系統匣通知][4]

一次 hello 應用程式啟動時，Visual Studio 會自動顯示 hello**診斷事件檢視器**，您可以在其中看到與您的服務追蹤輸出。
   
![診斷事件檢視器][5]

hello 我們使用的可設定狀態的服務範本只會顯示計數器值遞增中 hello`RunAsync`方法**MyStatefulService.cs**。

展開其中一個 hello 事件 toosee 更多詳細資料，包括 hello hello 程式碼執行所在的節點。 在此情況下是 \_Node\_2，但在您的電腦上可能會是其他節點。
   
![診斷事件檢視器詳細資訊][6]

hello 本機叢集包含五個節點裝載在同一部電腦。 在生產環境中，每個節點會裝載於不同的實體或虛擬機器上。 toosimulate hello 遺失機器時執行 hello Visual Studio 的偵錯工具在 hello 相同時間，讓我們來看下一個 hello hello 本機叢集上的節點。

在 [hello**方案總管] 中**視窗中，開啟**MyStatefulService.cs**。 

尋找 hello`RunAsync`方法並將 hello hello 方法第一行上的中斷點。

![具狀態服務 RunAsync 方法的中斷點][7]

啟動 hello **Service Fabric 總管**工具，以滑鼠右鍵按一下 hello**本機叢集管理員**系統匣應用程式，然後選擇 **管理本機叢集**。

![從 hello 本機叢集管理員啟動 Service Fabric 總管][systray-launch-sfx]

[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) 會提供叢集的視覺表示法。 它包含部署的應用程式 tooit hello 組和它構成實體節點的 hello 組。

Hello 左窗格中，展開 **叢集 > 節點**和尋找 hello 節點正在您的程式碼。

按一下**動作 > 停用 （重新啟動）** toosimulate 機器重新啟動。

![在 Service Fabric Explorer 中停止節點][sfx-stop-node]

您應該會立即看到中斷點為 hello 計算您順暢地執行其中一個節點容錯移轉 tooanother Visual Studio 中叫用。


接下來，傳回 toohello 診斷事件檢視器，並觀察 hello 訊息。 hello 計數器一直在遞增，即使 hello 事件實際上來自不同的節點。

![容錯移轉之後的診斷事件檢視器][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-hello-local-cluster-optional"></a>清除 hello 本機叢集 （選擇性）

請記住，此本機叢集是真實的叢集。 停止 hello 偵錯工具會移除您的應用程式執行個體，並取消註冊 hello 應用程式類型。 不過，hello 叢集會繼續 toorun hello 背景執行。 當您準備好 toostop hello 本機叢集時，有幾個選項。

### <a name="keep-application-and-trace-data"></a>保留應用程式和追蹤資料

關閉 hello 叢集，以滑鼠右鍵按一下 hello**本機叢集管理員**系統匣應用程式，然後選擇 **停止本機叢集**。

### <a name="delete-hello-cluster-and-all-data"></a>資料刪除 hello 叢集

以滑鼠右鍵按一下 hello 移除 hello 叢集**本機叢集管理員**系統匣應用程式，然後選擇 **移除本機叢集**。 

如果您選擇此選項時，Visual Studio 重新部署 hello 叢集 hello 下次您執行 hello 應用程式。 如果您不想 toouse hello 本機叢集段時間，或如果您需要 tooreclaim 資源，請選擇此選項。

## <a name="next-steps"></a>後續步驟
深入了解 [Reliable Services](service-fabric-reliable-services-introduction.md)。
<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
