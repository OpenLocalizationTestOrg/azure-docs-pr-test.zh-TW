---
title: "在 Microsoft Azure 中的 aaaMonitoring |Microsoft 文件"
description: "當您想 toomonitor 任何項目在 Microsoft Azure 中的選項。 Azure 監視器, Application Insights Log Analytics"
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1b962c74-8d36-4778-b816-a893f738f92d
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: f5a4f32525c52613f01a913e09a9fe3fbcbaeb21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-monitoring-in-microsoft-azure"></a>Microsoft Azure 中的監視概觀
本文提供可用來監視 Microsoft Azure 的工具概觀。 適用於太
- 監視在 Microsoft Azure 中執行的應用程式 
- 在 Azure 外部執行且可監視 Azure 中物件的工具/服務。 

其中也會討論各種產品和服務的可用 hello 和它們如何共同運作。 它可協助您 toodetermine 哪一個工具是最適合您在哪些情況下。  

## <a name="why-use-monitoring-and-diagnostics"></a>為何要使用監視和診斷？

您雲端應用程式中的效能問題可能會對企業產生影響。 透過多個互連的元件和頻繁的發行，隨時都可能導致效能降低。 此外，如果您正在開發應用程式，您的使用者通常會探索到您在測試時未發現的問題。 您應該立即，這些問題的相關資訊，並已進行診斷與修正 hello 問題的工具。 Microsoft Azure 提供多種工具來識別這些問題。

## <a name="how-do-i-monitor-my-azure-cloud-apps"></a>如何監視我的 Azure 雲端應用程式？

有多種工具可用來監視 Azure 應用程式和服務。 其中有些功能會重疊。 這是部分原因歷程記錄和部分到期 toohello 模糊開發和作業的應用程式之間。 

以下是 hello 主要工具：

-   **Azure 監視器**是用以監視 Azure 上執行之服務的基本工具。 它會提供您相關的服務，且周圍環境的 hello hello 輸送量的基礎結構層級資料。 如果您要管理您的應用程式在 Azure 中，決定是否 tooscale 向上或向下的資源，然後 Azure 監視器可讓您使用什麼 toostart。

-   **Application Insights** 可用來開發，並作為監視生產環境的解決方案。 它的運作方式是將封裝安裝到您的應用程式，因此可讓您更深入檢視內部情形。 它的資料包括相依性的回應時間、例外狀況追蹤、偵錯快照集、執行設定檔。 它提供功能強大的智慧工具來分析所有此遙測這兩個 toohelp 您偵錯應用程式和 toohelp 您了解使用者與它的行為。 您可以分辨是否突然增加回應時間是因為 toosomething 中應用程式或某些外部 resourcing 問題。 如果您使用 Visual Studio hello 應用程式有問題，您可以採取右 toohello 問題行程式碼，您可以修正此問題。  

-   **記錄分析**適用於需要 tootune 在生產環境中執行的應用程式的效能和計畫維護。 它是 Azure 中的基本工具。 它會收集，並從多個來源、 彙總資料，但仍有延遲 10 too15 分鐘的時間。 它會針對 Azure、內部部署及協力廠商的雲端式基礎結構 (例如 Amazon Web 服務) 提供整體 IT 管理解決方案。 它提供更豐富的工具 tooanalyze 資料跨多個來源、 跨所有記錄檔，讓複雜的查詢和上指定的條件可以主動警示。  您甚至可以將自訂資料收集到其中央存放庫，如此便能查詢並將其視覺化。 

-   **System Center Operations Manager (SCOM)** 可用來管理及監視大型雲端安裝。 您可能已經熟悉它做為適用於內部部署 Windows Sever 和 Hyper-V 型雲端的管理工具，但它也可以與 Azure 應用程式整合並加以管理。 在其他方面，它可以在現有的即時應用程式上安裝 Application Insights。  如果應用程式當機，它會在短時間內通知您。 請注意，Log Analytics 不會取代 SCOM。 它也可與其搭配使用。  


## <a name="accessing-monitoring-in-hello-azure-portal"></a>存取 hello Azure 入口網站中的監視
所有的 Azure 監視服務現在都可在單一 UI 窗格中取得。 如需有關如何 tooaccess 這個區域中，請參閱[開始使用 Azure 監視器](monitoring-get-started.md)。 

您也可以存取特定資源的監視功能，方法是將那些資源反白顯示，然後向下切入至它們的監視選項。 

## <a name="examples-of-when-toouse-which-tool"></a>範例 toouse 的工具 

下列各節的 hello 示範一些基本的案例，以及應該一起使用的工具。 

### <a name="scenario-1--fix-errors-in-an-azure-application-under-development"></a>案例 1：在開發期間，修正 Azure 應用程式中的錯誤   

**hello 最佳選項 toouse Application Insights、 Azure 監視器和 Visual Studio 在一起會**

Azure 現在提供 hello hello hello 雲端中的 Visual Studio 偵錯工具的完整功能。 設定 Azure 監視器 toosend 遙測 tooApplication 深入資訊。 可讓您的應用程式中的 Visual Studio tooinclude hello Application Insights SDK。 一旦在 Application Insights，您可以視覺化方式使用 hello 應用程式對應 toodiscover 或未執行的應用程式的哪些部分的狀況不良。 針對那些狀況不良的部分，已經有錯誤和例外狀況可供探索。 您可以使用 hello 更深入的 Application Insights toogo 中各種分析。 如果您不確定有關 hello 錯誤，您可以使用 hello Visual Studio 偵錯工具 tootrace 成程式碼和 pin 指標進一步的問題。 

如需詳細資訊，請參閱[監視 Web 應用程式](../application-insights/app-insights-azure-web-apps.md)和各種類型的應用程式和語言的指示，請參閱 toohello hello 左側的目錄中的資料表。  

### <a name="scenario-2--debug-an-azure-net-web-application-for-errors-that-only-show-in-production"></a>案例 2：對 Azure.NET Web 應用程式進行偵錯，以取得只會在生產環境中顯示的錯誤 

> [!NOTE]
> 這些功能目前為預覽狀態。 

**hello 最佳選項 toouse Application Insights 而且盡可能 hello 的 Visual Studio 的完整的偵錯體驗。**

使用 hello 應用程式 Insights 快照偵錯工具 toodebug 您的應用程式。 Hello 系統與生產元件特定的錯誤臨界值時，自動擷取遙測中稱為 「 快照集。 」 的時間窗口 hello 擷取量是安全的生產雲端因為小足夠不 tooaffect 效能，但足以 tooallow 追蹤。  hello 系統可以擷取多個快照集。 您可以在 hello Azure 入口網站中的時間點看起來，或使用 Visual Studio 進行 hello 完整體驗。 使用 Visual Studio，開發人員就能逐步執行該快照集，如同他們正在進行即時偵錯。 本機變數、參數、記憶體及框架全都可供使用。 開發人員必須授與存取 toothis 實際執行資料透過 RBAC 角色。  

如需詳細資訊，請參閱[快照集偵錯](../application-insights/app-insights-snapshot-debugger.md)。 

### <a name="scenario-3--debug-an-azure-application-that-uses-containers-or-microservices"></a>案例 3：對使用容器或微服務的 Azure 應用程式進行偵錯 

**與案例 1 相同。一起使用 Application Insights、Azure 監視器和 Visual Studio** Application Insights 也支援從在容器內部執行的程序以及從微服務 (Kubernetes、Docker、Azure Service Fabric) 蒐集遙測。 如需詳細資訊，[請參閱這段對容器和微服務進行偵錯的相關影片](https://go.microsoft.com/fwlink/?linkid=848184)。 


### <a name="scenario-4--fix-performance-issues-in-your-azure-application"></a>案例 4：修正 Azure 應用程式中的效能問題

hello [Application Insights profiler](../application-insights/app-insights-profiler.md)是設計的 toohelp 疑難排解這類問題。 您可以針對在應用程式服務 (Web Apps、Logic Apps、Mobile Apps、API Apps) 中執行的應用程式及其他元件 (例如，虛擬機器、虛擬機器擴展集 (VMSS)、雲端服務及 Service Fabric)，識別效能問題並進行疑難排解。 

> [!NOTE]
> 虛擬機器，虛擬機器擴展集 (VMSS)，雲端服務和服務網狀架構的能力 tooprofile 處於預覽狀態。   

此外，會主動通知您透過電子郵件有關的錯誤，例如變慢的頁面載入時間，特定類型 hello 智慧偵測工具。  您不需要 toodo 這項工具上的任何設定。 如需詳細資訊，請參閱[智慧型偵測 - 效能異常](../application-insights/app-insights-proactive-performance-diagnostics.md)和[智慧型偵測 - 效能異常](https://azure.microsoft.com/blog/Enhancments-ApplicationInsights-SmartDetection/preview)。



## <a name="next-steps"></a>後續步驟
深入了解

* [Ignite 2016 上的 Azure 監視器影片](https://myignite.microsoft.com/videos/4977)
* [開始使用 Azure 監視器](monitoring-get-started.md)
* [Azure 診斷](../azure-diagnostics.md)如果您正嘗試 toodiagnose 問題，在您的雲端服務，虛擬機器，虛擬機器進行調整設定，或 Service Fabric 應用程式。
* [Application Insights](https://azure.microsoft.com/documentation/services/application-insights/)如果您在應用程式服務 Web 應用程式中嘗試 toodiagnostic 問題。
* [記錄分析](https://azure.microsoft.com/documentation/services/log-analytics/)和 hello [Operations Management Suite](https://www.microsoft.com/oms/)監控解決方案的生產環境