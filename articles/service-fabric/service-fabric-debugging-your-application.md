---
title: "aaaDebug Visual Studio 中的應用程式 |Microsoft 文件"
description: "開發和偵錯在 Visual Studio 在本機開發叢集改進 hello 可靠性和效能，您的服務。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: 8d08689e82195d09f57b462631ad04fd237bc4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a>使用 Visual Studio 偵錯 Service Fabric 應用程式
> [!div class="op_single_selector"]
> * [Visual Studio/CSharp](service-fabric-debugging-your-application.md) 
> * [Eclipse/Java](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a>偵錯本機 Service Fabric 應用程式
您可以在本機電腦開發叢集中開發和偵錯 Azure Service Fabric 應用程式來節省時間和金錢。 Visual Studio 2017 或 Visual Studio 2015 可以部署 hello 應用程式 toohello 本機叢集，並自動連接 hello 偵錯工具 tooall 應用程式執行個體。

1. 中的 hello 步驟來啟動本機開發叢集[設定 Service Fabric 開發環境](service-fabric-get-started.md)。
2. 按 **F5** 或按一下 [偵錯]  >  [開始偵錯]。
   
    ![開始偵錯應用程式][startdebugging]
3. 您的程式碼和逐步執行 hello 應用程式中設定中斷點，即可在 hello 命令**偵錯**功能表。
   
   > [!NOTE]
   > Visual Studio 會將附加 tooall 應用程式執行個體。 當您逐步執行程式碼時，系統可能會透過多個程序叫用中斷點而導致並行工作階段。 請嘗試停用 hello 中斷點之後就叫用，讓每個中斷點條件上 hello 執行緒 ID 或使用診斷事件。
   > 
   > 
4. hello**診斷事件**視窗會自動開啟，讓您即時檢視診斷事件。
   
    ![即時檢視診斷事件][diagnosticevents]
5. 您也可以開啟 hello**診斷事件**在 Cloud Explorer 中的視窗。  在 [Service Fabric] 之下，以滑鼠右鍵按一下任何節點，然後選擇 [檢視串流追蹤]。
   
    ![開啟 hello 診斷事件視窗][viewdiagnosticevents]
   
    如果您想 toofilter 追蹤 tooa 特定服務或應用程式，只要啟用該特定服務或應用程式上的資料流追蹤。
6. 自動產生的 hello 中可以看到 hello 診斷事件**ServiceEventSource.cs**檔案，並從應用程式程式碼呼叫。
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. hello**診斷事件**視窗支援篩選、 暫停與檢查即時事件。  hello 篩選器是簡單的字串搜尋 hello 事件訊息，包括其內容。
   
    ![篩選、暫停和繼續，或即時檢查事件][diagnosticeventsactions]
8. 偵錯服務如同偵錯任何其他應用程式。 您通常可以透過 Visual Studio 設定中斷點，以便進行偵錯。 即使可靠集合會在多個節點上複寫，它們仍會實作 IEnumerable。 這表示您可以使用 hello 結果檢視 Visual Studio 中偵錯 toosee 時已儲存在內部。 您可以在程式碼中的任何位置輕鬆設定中斷點。
   
    ![開始偵錯應用程式][breakpoint]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a>偵錯遠端 Service Fabric 應用程式
如果您的 Service Fabric 應用程式在 Azure 中的 Service Fabric 叢集上執行，也可以 tooremotely 偵錯這些項目，直接從 Visual Studio。

> [!NOTE]
> hello 功能需要[Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015)和[Azure SDK for.NET 2.9](https://azure.microsoft.com/downloads/)。    
> 
> 

<!-- -->
> [!WARNING]
> 遠端偵錯適用於開發/測試案例和 toobe 用在實際執行環境，因為 hello hello 執行應用程式的影響。
> 
> 

1. 瀏覽 tooyour 叢集中**Cloud Explorer**，以滑鼠右鍵按一下，然後選擇 **啟用偵錯**
   
    ![啟用遠端偵錯][enableremotedebugging]
   
    這會啟動啟用遠端偵錯您的叢集節點上的擴充功能的 hello 的 hello 程序，以及所需的網路組態。
2. 中的以滑鼠右鍵按一下 hello 叢集節點**Cloud Explorer**，然後選擇 **附加偵錯工具**
   
    ![連結偵錯工具][attachdebugger]
3. 在 [hello**附加 tooprocess** ] 對話方塊中，選擇 toodebug，然後按一下 「 hello 」 處理序**附加**
   
    ![選擇程序][chooseprocess]
   
    hello 名稱 hello 程序中，您想以 tooattach，等於 hello 程式的服務專案的組件名稱。
   
    hello 偵錯工具會附加 tooall 節點執行 hello 程序。
   
   * 在您將正在偵錯的無狀態服務的 hello 情況下，hello 服務的所有節點上的所有執行個體是 hello 偵錯工作階段的一部分。
   * 如果您正在偵錯的可設定狀態的服務，只有 hello 主要複本的任何資料分割將作用中和 hello 偵錯工具，因此已攔截。 如果 hello 主要複本移 hello 偵錯工作階段期間，該複本的 hello 處理仍會 hello 偵錯工作階段的一部分。
   * 在訂單 tooonly catch 相關的資料分割或特定服務的執行個體中，您可以使用條件式中斷點 tooonly 中斷特定分割區或執行個體。
     
     ![條件式中斷點][conditionalbreakpoint]
     
     > [!NOTE]
     > 目前我們不支援偵錯多個執行個體的 hello Service Fabric 叢集相同的服務可執行檔的名稱。
     > 
     > 
4. 一旦您完成偵錯您的應用程式，您可以停用 hello 遠端偵錯延伸模組中的 hello 叢集上按一下滑鼠右鍵**Cloud Explorer**選擇**停用偵錯**
   
    ![停用遠端偵錯][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a>從遠端叢集節點串流追蹤
您也會直接從遠端叢集節點 tooVisual Studio 能夠 toostream 追蹤。 這項功能可讓您 toostream ETW 追蹤事件，產生的 Service Fabric 叢集節點上。

> [!NOTE]
> 此功能需要 [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) 和 [Azure SDK for.NET 2.9](https://azure.microsoft.com/downloads/)。
> 這項功能僅支援在 Azure 中執行的叢集。
> 
> 

<!-- -->
> [!WARNING]
> 資料流追蹤適用於開發/測試案例和 toobe 用在實際執行環境，因為 hello hello 執行應用程式的影響。
> 在生產案例中，您應依賴使用 Azure 診斷轉送事件。
> 
> 

1. 瀏覽 tooyour 叢集中**Cloud Explorer**，以滑鼠右鍵按一下，然後選擇 **啟用資料流追蹤**
   
    ![啟用遠端串流追蹤][enablestreamingtraces]
   
    這會啟動啟用 hello 串流處理您的叢集節點上的追蹤延伸模組的 hello 程序，以及所需的網路組態。
2. 展開 hello**節點**中的項目**Cloud Explorer**，以滑鼠右鍵按一下您想要從 toostream 追蹤，並選擇 hello 節點**檢視資料流追蹤**
   
    ![檢視遠端串流追蹤][viewremotestreamingtraces]
   
    您想要從 toosee 追蹤的許多節點重複步驟 2。 每個節點串流會顯示在專用視窗中。
   
    現在您已經準備 Service Fabric 和您的服務所發出的能 toosee hello 追蹤。 如果您想 toofilter hello 事件 tooonly 顯示特定應用程式，只要輸入 hello hello 篩選中的 hello 應用程式名稱。
   
    ![檢視串流追蹤][viewingstreamingtraces]
3. 在您完成從叢集中的資料流處理的追蹤，您可以停用遠端資料流處理的追蹤，以滑鼠右鍵按一下中的 hello 叢集**Cloud Explorer**選擇**停用資料流追蹤**
   
    ![停用遠端串流追蹤][disablestreamingtraces]

## <a name="next-steps"></a>後續步驟
* [測試 Service Fabric 服務](service-fabric-testability-overview.md)。
* [在 Visual Studio 中管理 Service Fabric 應用程式](service-fabric-manage-application-in-visual-studio.md)。

<!--Image references-->
[startdebugging]: ./media/service-fabric-debugging-your-application/startdebugging.png
[diagnosticevents]: ./media/service-fabric-debugging-your-application/diagnosticevents.png
[viewdiagnosticevents]: ./media/service-fabric-debugging-your-application/viewdiagnosticevents.png
[diagnosticeventsactions]: ./media/service-fabric-debugging-your-application/diagnosticeventsactions.png
[breakpoint]: ./media/service-fabric-debugging-your-application/breakpoint.png
[enableremotedebugging]: ./media/service-fabric-debugging-your-application/enableremotedebugging.png
[attachdebugger]: ./media/service-fabric-debugging-your-application/attachdebugger.png
[chooseprocess]: ./media/service-fabric-debugging-your-application/chooseprocess.png
[conditionalbreakpoint]: ./media/service-fabric-debugging-your-application/conditionalbreakpoint.png
[disableremotedebugging]: ./media/service-fabric-debugging-your-application/disableremotedebugging.png
[enablestreamingtraces]: ./media/service-fabric-debugging-your-application/enablestreamingtraces.png
[viewingstreamingtraces]: ./media/service-fabric-debugging-your-application/viewingstreamingtraces.png
[viewremotestreamingtraces]: ./media/service-fabric-debugging-your-application/viewremotestreamingtraces.png
[disablestreamingtraces]: ./media/service-fabric-debugging-your-application/disablestreamingtraces.png
