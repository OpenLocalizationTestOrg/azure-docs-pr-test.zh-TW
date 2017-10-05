---
title: "使用 Azure 診斷追蹤雲端服務應用程式中的流程 | Microsoft Docs"
description: "將追蹤訊息加入至 Azure 應用程式來協助偵錯、測量效能、監視、流量分析等等。"
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
ms.openlocfilehash: 35b4a4270846c54a1ca760e803ef7adba60cf03b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="trace-the-flow-of-a-cloud-services-application-with-azure-diagnostics"></a><span data-ttu-id="cdb24-103">使用 Azure 診斷追蹤雲端服務應用程式的流程</span><span class="sxs-lookup"><span data-stu-id="cdb24-103">Trace the flow of a Cloud Services application with Azure Diagnostics</span></span>
<span data-ttu-id="cdb24-104">追蹤是一種方式，可讓您在應用程式執行時加以監視。</span><span class="sxs-lookup"><span data-stu-id="cdb24-104">Tracing is a way for you to monitor the execution of your application while it is running.</span></span> <span data-ttu-id="cdb24-105">您可以使用 [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx)、[System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx) 和 [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) 類別，在記錄檔、文字檔或其他裝置中記錄錯誤和應用程式執行的相關資訊，供稍後分析。</span><span class="sxs-lookup"><span data-stu-id="cdb24-105">You can use the [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), and [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classes to record information about errors and application execution in logs, text files, or other devices for later analysis.</span></span> <span data-ttu-id="cdb24-106">如需追蹤的詳細資訊，請參閱 [追蹤和檢測應用程式](https://msdn.microsoft.com/library/zs6s4h68.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cdb24-106">For more information about tracing, see [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span></span>

## <a name="use-trace-statements-and-trace-switches"></a><span data-ttu-id="cdb24-107">使用追蹤陳述式和追蹤參數</span><span class="sxs-lookup"><span data-stu-id="cdb24-107">Use trace statements and trace switches</span></span>
<span data-ttu-id="cdb24-108">藉由加入 [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) 至應用程式組態，並在您的應用程式程式碼中對 System.Diagnostics.Trace 或 System.Diagnostics.Debug 進行呼叫，藉此在雲端服務應用程式中實作追蹤。</span><span class="sxs-lookup"><span data-stu-id="cdb24-108">Implement tracing in your Cloud Services application by adding the [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) to the application configuration and making calls to System.Diagnostics.Trace or System.Diagnostics.Debug in your application code.</span></span> <span data-ttu-id="cdb24-109">將組態檔 app.config 用於背景工作角色，將 web.config 用於 Web 角色。</span><span class="sxs-lookup"><span data-stu-id="cdb24-109">Use the configuration file *app.config* for worker roles and the *web.config* for web roles.</span></span> <span data-ttu-id="cdb24-110">使用 Visual Studio 範本建立新的託管服務時，Azure 診斷會自動加入至專案，並且 DiagnosticMonitorTraceListener 會加入至您所加入角色的適當組態檔。</span><span class="sxs-lookup"><span data-stu-id="cdb24-110">When you create a new hosted service using a Visual Studio template, Azure Diagnostics is automatically added to the project and the DiagnosticMonitorTraceListener is added to the appropriate configuration file for the roles that you add.</span></span>

<span data-ttu-id="cdb24-111">如需有關放置追蹤陳述式資訊，請參閱 [作法：加入 Trace 陳述式至應用程式程式碼](https://msdn.microsoft.com/library/zd83saa2.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cdb24-111">For information on placing trace statements, see [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>

<span data-ttu-id="cdb24-112">藉由在程式碼中放置 [Trace 參數](https://msdn.microsoft.com/library/3at424ac.aspx) ，您可以控制是否發生追蹤以及廣泛程度。</span><span class="sxs-lookup"><span data-stu-id="cdb24-112">By placing [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in your code, you can control whether tracing occurs and how extensive it is.</span></span> <span data-ttu-id="cdb24-113">這可讓您監視您的應用程式在生產環境中的狀態。</span><span class="sxs-lookup"><span data-stu-id="cdb24-113">This lets you monitor the status of your application in a production environment.</span></span> <span data-ttu-id="cdb24-114">對於在多部電腦上執行多個元件的商務應用程式來說，這特別重要。</span><span class="sxs-lookup"><span data-stu-id="cdb24-114">This is especially important in a business application that uses multiple components running on multiple computers.</span></span> <span data-ttu-id="cdb24-115">如需詳細資訊，請參閱 [做法：設定追蹤參數](https://msdn.microsoft.com/library/t06xyy08.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cdb24-115">For more information, see [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx).</span></span>

## <a name="configure-the-trace-listener-in-an-azure-application"></a><span data-ttu-id="cdb24-116">在 Azure 應用程式中設定追蹤接聽程式</span><span class="sxs-lookup"><span data-stu-id="cdb24-116">Configure the trace listener in an Azure application</span></span>
<span data-ttu-id="cdb24-117">Trace、Debug 和 TraceSource，需要您設定「接聽程式」來收集和記錄傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="cdb24-117">Trace, Debug and TraceSource, require you set up "listeners" to collect and record the messages that are sent.</span></span> <span data-ttu-id="cdb24-118">接聽程式會收集、儲存和路由傳送追蹤訊息。</span><span class="sxs-lookup"><span data-stu-id="cdb24-118">Listeners collect, store, and route tracing messages.</span></span> <span data-ttu-id="cdb24-119">它們將追蹤輸出導向至適當的目標，例如記錄檔、視窗或文字檔。</span><span class="sxs-lookup"><span data-stu-id="cdb24-119">They direct the tracing output to an appropriate target, such as a log, window, or text file.</span></span> <span data-ttu-id="cdb24-120">Azure 診斷使用 [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) 類別。</span><span class="sxs-lookup"><span data-stu-id="cdb24-120">Azure Diagnostics uses the [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) class.</span></span>

<span data-ttu-id="cdb24-121">完成下列程序之前，您必須初始化 Azure 診斷監視器。</span><span class="sxs-lookup"><span data-stu-id="cdb24-121">Before you complete the following procedure, you must initialize the Azure diagnostic monitor.</span></span> <span data-ttu-id="cdb24-122">若要這樣做，請參閱 [在 Microsoft Azure 中啟用診斷](cloud-services-dotnet-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="cdb24-122">To do this, see [Enabling Diagnostics in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="cdb24-123">請注意，如果您使用 Visual Studio 所提供的範本，則會自動為您加入接聽程式的組態。</span><span class="sxs-lookup"><span data-stu-id="cdb24-123">Note that if you use the templates that are provided by Visual Studio, the configuration of the listener is added automatically for you.</span></span>

### <a name="add-a-trace-listener"></a><span data-ttu-id="cdb24-124">加入追蹤接聽程式</span><span class="sxs-lookup"><span data-stu-id="cdb24-124">Add a trace listener</span></span>
1. <span data-ttu-id="cdb24-125">開啟您的角色的 web.config 或 app.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="cdb24-125">Open the web.config or app.config file for your role.</span></span>
2. <span data-ttu-id="cdb24-126">將下列程式碼新增至檔案。</span><span class="sxs-lookup"><span data-stu-id="cdb24-126">Add the following code to the file.</span></span> <span data-ttu-id="cdb24-127">變更 Version 屬性以使用您所參考的組件版本號碼。</span><span class="sxs-lookup"><span data-stu-id="cdb24-127">Change the Version attribute to use the version number of the assembly you are referencing.</span></span> <span data-ttu-id="cdb24-128">除非有更新，否則組件版本不一定會隨著每個 Azure SDK 版本而變更。</span><span class="sxs-lookup"><span data-stu-id="cdb24-128">The assembly version does not necessarily change with each Azure SDK release unless there are updates to it.</span></span>
   
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
   > <span data-ttu-id="cdb24-129">請確定您有參照 Microsoft.WindowsAzure.Diagnostics 組件的專案參考。</span><span class="sxs-lookup"><span data-stu-id="cdb24-129">Make sure you have a project reference to the Microsoft.WindowsAzure.Diagnostics assembly.</span></span> <span data-ttu-id="cdb24-130">更新上述 xml 中的版本號碼，以和參考的 Microsoft.WindowsAzure.Diagnostics 組件版本相符。</span><span class="sxs-lookup"><span data-stu-id="cdb24-130">Update the version number in the xml above to match the version of the referenced Microsoft.WindowsAzure.Diagnostics assembly.</span></span>
   > 
   > 
3. <span data-ttu-id="cdb24-131">儲存組態檔。</span><span class="sxs-lookup"><span data-stu-id="cdb24-131">Save the config file.</span></span>

<span data-ttu-id="cdb24-132">如需接聽程式的詳細資訊，請參閱 [追蹤接聽程式](https://msdn.microsoft.com/library/4y5y10s7.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cdb24-132">For more information about listeners, see [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span></span>

<span data-ttu-id="cdb24-133">完成加入接聽程式的步驟之後，您可以加入您的追蹤陳述式到程式碼中。</span><span class="sxs-lookup"><span data-stu-id="cdb24-133">After you complete the steps to add the listener, you can add trace statements to your code.</span></span>

### <a name="to-add-trace-statement-to-your-code"></a><span data-ttu-id="cdb24-134">將追蹤陳述式加入至您的程式碼</span><span class="sxs-lookup"><span data-stu-id="cdb24-134">To add trace statement to your code</span></span>
1. <span data-ttu-id="cdb24-135">開啟您的應用程式的原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="cdb24-135">Open a source file for your application.</span></span> <span data-ttu-id="cdb24-136">例如，背景工作角色或 Web 角色的 <RoleName>.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="cdb24-136">For example, the <RoleName>.cs file for the worker role or web role.</span></span>
2. <span data-ttu-id="cdb24-137">加入下列 using 陳述式 (如果尚未加入)：</span><span class="sxs-lookup"><span data-stu-id="cdb24-137">Add the following using statement if it has not already been added:</span></span>
    ```
        using System.Diagnostics;
    ```
3. <span data-ttu-id="cdb24-138">在您想要用來擷取應用程式狀態資訊的位置加入 Trace 陳述式。</span><span class="sxs-lookup"><span data-stu-id="cdb24-138">Add Trace statements where you want to capture information about the state of your application.</span></span> <span data-ttu-id="cdb24-139">您可以使用各種方法來格式化 Trace 陳述式的輸出。</span><span class="sxs-lookup"><span data-stu-id="cdb24-139">You can use a variety of methods to format the output of the Trace statement.</span></span> <span data-ttu-id="cdb24-140">如需詳細資訊，請參閱 [做法：加入 Trace 陳述式至應用程式程式碼](https://msdn.microsoft.com/library/zd83saa2.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cdb24-140">For more information, see [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>
4. <span data-ttu-id="cdb24-141">儲存原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="cdb24-141">Save the source file.</span></span>

