---
title: "在雲端服務應用程式中使用 Azure 診斷 aaaTrace hello 流程 |Microsoft 文件"
description: "新增追蹤訊息 tooan Azure 應用程式 toohelp 偵錯、 測量效能、 監視、 流量分析以及其他等等。"
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 09934772-cc07-4fd2-ba88-b224ca192f8e
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/20/2016
ms.author: robb
ms.openlocfilehash: d2ed7b5997ae1d298115b4ce593bb5051a9a0c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="trace-hello-flow-of-a-cloud-services-application-with-azure-diagnostics"></a>追蹤雲端服務應用程式使用 Azure 診斷的 hello 流程
執行時，追蹤會是您 toomonitor hello 應用程式執行的方式。 您可以使用 hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx)， [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx)，和[System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx)類別 toorecord 錯誤的相關資訊，在記錄檔、 文字檔案或其他裝置，以便稍後進行分析的應用程式執行。 如需追蹤的詳細資訊，請參閱 [追蹤和檢測應用程式](https://msdn.microsoft.com/library/zs6s4h68.aspx)。

## <a name="use-trace-statements-and-trace-switches"></a>使用追蹤陳述式和追蹤參數
藉由新增 hello 在雲端服務應用程式中的實作追蹤[DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello 應用程式組態，並呼叫 tooSystem.Diagnostics.Trace 或 System.Diagnostics.Debug 中的您應用程式程式碼。 使用 hello 設定檔*app.config*背景工作角色和 hello *web.config* web 角色。 當您建立新的託管的服務使用 Visual Studio 範本時，Azure 診斷會自動加入 toohello 專案，然後 hello DiagnosticMonitorTraceListener 加入 toohello 適當的組態檔，針對您加入 hello 角色。

如需有關放置追蹤陳述式資訊，請參閱[How to： 將追蹤陳述式 tooApplication 程式碼](https://msdn.microsoft.com/library/zd83saa2.aspx)。

藉由在程式碼中放置 [Trace 參數](https://msdn.microsoft.com/library/3at424ac.aspx) ，您可以控制是否發生追蹤以及廣泛程度。 這可讓您監視應用程式在生產環境中的 hello 狀態。 對於在多部電腦上執行多個元件的商務應用程式來說，這特別重要。 如需詳細資訊，請參閱 [做法：設定追蹤參數](https://msdn.microsoft.com/library/t06xyy08.aspx)。

## <a name="configure-hello-trace-listener-in-an-azure-application"></a>設定 Azure 應用程式中的 hello 追蹤接聽項
追蹤，Debug 和 TraceSource 時，會要求您設定 「 接聽程式 」 toocollect 和傳送之記錄的 hello 訊息。 接聽程式會收集、儲存和路由傳送追蹤訊息。 它們會直接 hello 追蹤輸出 tooan 適當的目標，例如記錄檔、 視窗或文字檔。 Azure 診斷使用 hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx)類別。

在您完成下列程序的 hello 之前，您必須初始化 hello Azure 診斷監視器。 toodo，請參閱[在 Microsoft Azure 中啟用診斷](cloud-services-dotnet-diagnostics.md)。

請注意，是否您使用 Visual studio 所提供的 hello 範本，hello hello 接聽程式組態會自動為您加入。

### <a name="add-a-trace-listener"></a>加入追蹤接聽程式
1. 開啟您的角色的 hello web.config 或 app.config 檔案。
2. 新增下列程式碼 toohello 檔 hello。 變更 hello 版本屬性 toouse hello hello 組件版本號碼所參考。 除非有更新 tooit hello 組件版本不一定變更每個 Azure SDK 版本。
   
    ```
    <system.diagnostics>
        <trace>
            <listeners>
                <add type="Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener,
                  Microsoft.WindowsAzure.Diagnostics,
                  Version=2.8.0.0,
                  Culture=neutral,
                  PublicKeyToken=31bf3856ad364e35"
                  name="AzureDiagnostics">
                    <filter type="" />
                </add>
            </listeners>
        </trace>
    </system.diagnostics>
    ```
   > [!IMPORTANT]
   > 請確定您有專案參考 toohello Microsoft.WindowsAzure.Diagnostics 組件。 更新 hello 版本號碼高於 toomatch hello 版的 hello hello xml 參考 Microsoft.WindowsAzure.Diagnostics 組件。
   > 
   > 
3. 儲存 hello 設定檔。

如需接聽程式的詳細資訊，請參閱 [追蹤接聽程式](https://msdn.microsoft.com/library/4y5y10s7.aspx)。

完成 hello 步驟 tooadd hello 接聽程式之後，您可以加入追蹤陳述式 tooyour 程式碼。

### <a name="tooadd-trace-statement-tooyour-code"></a>tooadd 追蹤陳述式 tooyour 程式碼
1. 開啟您的應用程式的原始程式檔。 例如，hello <RoleName>hello 背景工作角色或 web 角色的.cs 檔案。
2. 新增 hello 下列 using 陳述式，如果它有尚未加入：
    ```
        using System.Diagnostics;
    ```
3. 加入您想 toocapture 資訊 hello 狀態，您的應用程式的相關追蹤陳述式。 您可以使用各種不同的方法 tooformat hello 輸出的 hello 追蹤陳述式。 如需詳細資訊，請參閱[How to： 將追蹤陳述式 tooApplication 程式碼](https://msdn.microsoft.com/library/zd83saa2.aspx)。
4. 儲存 hello 來源檔案。

