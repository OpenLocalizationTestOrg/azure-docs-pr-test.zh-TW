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
# <a name="trace-hello-flow-of-a-cloud-services-application-with-azure-diagnostics"></a><span data-ttu-id="77e35-103">追蹤雲端服務應用程式使用 Azure 診斷的 hello 流程</span><span class="sxs-lookup"><span data-stu-id="77e35-103">Trace hello flow of a Cloud Services application with Azure Diagnostics</span></span>
<span data-ttu-id="77e35-104">執行時，追蹤會是您 toomonitor hello 應用程式執行的方式。</span><span class="sxs-lookup"><span data-stu-id="77e35-104">Tracing is a way for you toomonitor hello execution of your application while it is running.</span></span> <span data-ttu-id="77e35-105">您可以使用 hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx)， [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx)，和[System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx)類別 toorecord 錯誤的相關資訊，在記錄檔、 文字檔案或其他裝置，以便稍後進行分析的應用程式執行。</span><span class="sxs-lookup"><span data-stu-id="77e35-105">You can use hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), and [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classes toorecord information about errors and application execution in logs, text files, or other devices for later analysis.</span></span> <span data-ttu-id="77e35-106">如需追蹤的詳細資訊，請參閱 [追蹤和檢測應用程式](https://msdn.microsoft.com/library/zs6s4h68.aspx)。</span><span class="sxs-lookup"><span data-stu-id="77e35-106">For more information about tracing, see [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span></span>

## <a name="use-trace-statements-and-trace-switches"></a><span data-ttu-id="77e35-107">使用追蹤陳述式和追蹤參數</span><span class="sxs-lookup"><span data-stu-id="77e35-107">Use trace statements and trace switches</span></span>
<span data-ttu-id="77e35-108">藉由新增 hello 在雲端服務應用程式中的實作追蹤[DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello 應用程式組態，並呼叫 tooSystem.Diagnostics.Trace 或 System.Diagnostics.Debug 中的您應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="77e35-108">Implement tracing in your Cloud Services application by adding hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello application configuration and making calls tooSystem.Diagnostics.Trace or System.Diagnostics.Debug in your application code.</span></span> <span data-ttu-id="77e35-109">使用 hello 設定檔*app.config*背景工作角色和 hello *web.config* web 角色。</span><span class="sxs-lookup"><span data-stu-id="77e35-109">Use hello configuration file *app.config* for worker roles and hello *web.config* for web roles.</span></span> <span data-ttu-id="77e35-110">當您建立新的託管的服務使用 Visual Studio 範本時，Azure 診斷會自動加入 toohello 專案，然後 hello DiagnosticMonitorTraceListener 加入 toohello 適當的組態檔，針對您加入 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="77e35-110">When you create a new hosted service using a Visual Studio template, Azure Diagnostics is automatically added toohello project and hello DiagnosticMonitorTraceListener is added toohello appropriate configuration file for hello roles that you add.</span></span>

<span data-ttu-id="77e35-111">如需有關放置追蹤陳述式資訊，請參閱[How to： 將追蹤陳述式 tooApplication 程式碼](https://msdn.microsoft.com/library/zd83saa2.aspx)。</span><span class="sxs-lookup"><span data-stu-id="77e35-111">For information on placing trace statements, see [How to: Add Trace Statements tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>

<span data-ttu-id="77e35-112">藉由在程式碼中放置 [Trace 參數](https://msdn.microsoft.com/library/3at424ac.aspx) ，您可以控制是否發生追蹤以及廣泛程度。</span><span class="sxs-lookup"><span data-stu-id="77e35-112">By placing [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in your code, you can control whether tracing occurs and how extensive it is.</span></span> <span data-ttu-id="77e35-113">這可讓您監視應用程式在生產環境中的 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="77e35-113">This lets you monitor hello status of your application in a production environment.</span></span> <span data-ttu-id="77e35-114">對於在多部電腦上執行多個元件的商務應用程式來說，這特別重要。</span><span class="sxs-lookup"><span data-stu-id="77e35-114">This is especially important in a business application that uses multiple components running on multiple computers.</span></span> <span data-ttu-id="77e35-115">如需詳細資訊，請參閱 [做法：設定追蹤參數](https://msdn.microsoft.com/library/t06xyy08.aspx)。</span><span class="sxs-lookup"><span data-stu-id="77e35-115">For more information, see [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx).</span></span>

## <a name="configure-hello-trace-listener-in-an-azure-application"></a><span data-ttu-id="77e35-116">設定 Azure 應用程式中的 hello 追蹤接聽項</span><span class="sxs-lookup"><span data-stu-id="77e35-116">Configure hello trace listener in an Azure application</span></span>
<span data-ttu-id="77e35-117">追蹤，Debug 和 TraceSource 時，會要求您設定 「 接聽程式 」 toocollect 和傳送之記錄的 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="77e35-117">Trace, Debug and TraceSource, require you set up "listeners" toocollect and record hello messages that are sent.</span></span> <span data-ttu-id="77e35-118">接聽程式會收集、儲存和路由傳送追蹤訊息。</span><span class="sxs-lookup"><span data-stu-id="77e35-118">Listeners collect, store, and route tracing messages.</span></span> <span data-ttu-id="77e35-119">它們會直接 hello 追蹤輸出 tooan 適當的目標，例如記錄檔、 視窗或文字檔。</span><span class="sxs-lookup"><span data-stu-id="77e35-119">They direct hello tracing output tooan appropriate target, such as a log, window, or text file.</span></span> <span data-ttu-id="77e35-120">Azure 診斷使用 hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx)類別。</span><span class="sxs-lookup"><span data-stu-id="77e35-120">Azure Diagnostics uses hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) class.</span></span>

<span data-ttu-id="77e35-121">在您完成下列程序的 hello 之前，您必須初始化 hello Azure 診斷監視器。</span><span class="sxs-lookup"><span data-stu-id="77e35-121">Before you complete hello following procedure, you must initialize hello Azure diagnostic monitor.</span></span> <span data-ttu-id="77e35-122">toodo，請參閱[在 Microsoft Azure 中啟用診斷](cloud-services-dotnet-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="77e35-122">toodo this, see [Enabling Diagnostics in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="77e35-123">請注意，是否您使用 Visual studio 所提供的 hello 範本，hello hello 接聽程式組態會自動為您加入。</span><span class="sxs-lookup"><span data-stu-id="77e35-123">Note that if you use hello templates that are provided by Visual Studio, hello configuration of hello listener is added automatically for you.</span></span>

### <a name="add-a-trace-listener"></a><span data-ttu-id="77e35-124">加入追蹤接聽程式</span><span class="sxs-lookup"><span data-stu-id="77e35-124">Add a trace listener</span></span>
1. <span data-ttu-id="77e35-125">開啟您的角色的 hello web.config 或 app.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="77e35-125">Open hello web.config or app.config file for your role.</span></span>
2. <span data-ttu-id="77e35-126">新增下列程式碼 toohello 檔 hello。</span><span class="sxs-lookup"><span data-stu-id="77e35-126">Add hello following code toohello file.</span></span> <span data-ttu-id="77e35-127">變更 hello 版本屬性 toouse hello hello 組件版本號碼所參考。</span><span class="sxs-lookup"><span data-stu-id="77e35-127">Change hello Version attribute toouse hello version number of hello assembly you are referencing.</span></span> <span data-ttu-id="77e35-128">除非有更新 tooit hello 組件版本不一定變更每個 Azure SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="77e35-128">hello assembly version does not necessarily change with each Azure SDK release unless there are updates tooit.</span></span>
   
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
   > <span data-ttu-id="77e35-129">請確定您有專案參考 toohello Microsoft.WindowsAzure.Diagnostics 組件。</span><span class="sxs-lookup"><span data-stu-id="77e35-129">Make sure you have a project reference toohello Microsoft.WindowsAzure.Diagnostics assembly.</span></span> <span data-ttu-id="77e35-130">更新 hello 版本號碼高於 toomatch hello 版的 hello hello xml 參考 Microsoft.WindowsAzure.Diagnostics 組件。</span><span class="sxs-lookup"><span data-stu-id="77e35-130">Update hello version number in hello xml above toomatch hello version of hello referenced Microsoft.WindowsAzure.Diagnostics assembly.</span></span>
   > 
   > 
3. <span data-ttu-id="77e35-131">儲存 hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="77e35-131">Save hello config file.</span></span>

<span data-ttu-id="77e35-132">如需接聽程式的詳細資訊，請參閱 [追蹤接聽程式](https://msdn.microsoft.com/library/4y5y10s7.aspx)。</span><span class="sxs-lookup"><span data-stu-id="77e35-132">For more information about listeners, see [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span></span>

<span data-ttu-id="77e35-133">完成 hello 步驟 tooadd hello 接聽程式之後，您可以加入追蹤陳述式 tooyour 程式碼。</span><span class="sxs-lookup"><span data-stu-id="77e35-133">After you complete hello steps tooadd hello listener, you can add trace statements tooyour code.</span></span>

### <a name="tooadd-trace-statement-tooyour-code"></a><span data-ttu-id="77e35-134">tooadd 追蹤陳述式 tooyour 程式碼</span><span class="sxs-lookup"><span data-stu-id="77e35-134">tooadd trace statement tooyour code</span></span>
1. <span data-ttu-id="77e35-135">開啟您的應用程式的原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="77e35-135">Open a source file for your application.</span></span> <span data-ttu-id="77e35-136">例如，hello <RoleName>hello 背景工作角色或 web 角色的.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="77e35-136">For example, hello <RoleName>.cs file for hello worker role or web role.</span></span>
2. <span data-ttu-id="77e35-137">新增 hello 下列 using 陳述式，如果它有尚未加入：</span><span class="sxs-lookup"><span data-stu-id="77e35-137">Add hello following using statement if it has not already been added:</span></span>
    ```
        using System.Diagnostics;
    ```
3. <span data-ttu-id="77e35-138">加入您想 toocapture 資訊 hello 狀態，您的應用程式的相關追蹤陳述式。</span><span class="sxs-lookup"><span data-stu-id="77e35-138">Add Trace statements where you want toocapture information about hello state of your application.</span></span> <span data-ttu-id="77e35-139">您可以使用各種不同的方法 tooformat hello 輸出的 hello 追蹤陳述式。</span><span class="sxs-lookup"><span data-stu-id="77e35-139">You can use a variety of methods tooformat hello output of hello Trace statement.</span></span> <span data-ttu-id="77e35-140">如需詳細資訊，請參閱[How to： 將追蹤陳述式 tooApplication 程式碼](https://msdn.microsoft.com/library/zd83saa2.aspx)。</span><span class="sxs-lookup"><span data-stu-id="77e35-140">For more information, see [How to: Add Trace Statements tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>
4. <span data-ttu-id="77e35-141">儲存 hello 來源檔案。</span><span class="sxs-lookup"><span data-stu-id="77e35-141">Save hello source file.</span></span>

