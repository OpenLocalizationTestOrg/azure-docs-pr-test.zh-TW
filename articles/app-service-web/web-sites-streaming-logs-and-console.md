---
title: "aaaStreaming 記錄檔和主控台"
description: "串流記錄和主控台概觀"
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: 3e50a287-781b-4c6a-8c53-eec261889d7a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/12/2016
ms.author: byvinyal
ms.openlocfilehash: bb4b8ce5358da12041e164dfff8f43790dd67924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-logs-and-hello-console"></a><span data-ttu-id="39b1e-103">資料流處理的記錄檔和 hello 主控台</span><span class="sxs-lookup"><span data-stu-id="39b1e-103">Streaming Logs and hello Console</span></span>
## <a name="streaming-logs"></a><span data-ttu-id="39b1e-104">串流記錄</span><span class="sxs-lookup"><span data-stu-id="39b1e-104">Streaming Logs</span></span>
<span data-ttu-id="39b1e-105">hello **Azure 入口網站**提供了整合式資料流記錄檔檢視器，可讓您檢視追蹤事件，從您**App Service**即時應用程式。</span><span class="sxs-lookup"><span data-stu-id="39b1e-105">hello **Azure portal** provides an integrated streaming log viewer that lets you view tracing events from your **App Service** apps in real time.</span></span>  

<span data-ttu-id="39b1e-106">設定此功能只需要一些簡單的步驟：</span><span class="sxs-lookup"><span data-stu-id="39b1e-106">Setting up this feature requires a few simple steps:</span></span>

* <span data-ttu-id="39b1e-107">在程式碼中撰寫追蹤</span><span class="sxs-lookup"><span data-stu-id="39b1e-107">Write traces in your code</span></span>
* <span data-ttu-id="39b1e-108">啟用您應用程式的應用程式**診斷記錄**</span><span class="sxs-lookup"><span data-stu-id="39b1e-108">Enable Application **Diagnostic Logs** for your app</span></span>
* <span data-ttu-id="39b1e-109">檢視 hello hello 內建資料流**串流記錄**UI 中 hello **Azure 入口網站**。</span><span class="sxs-lookup"><span data-stu-id="39b1e-109">View hello stream from hello built-in **Streaming Logs** UI in hello **Azure portal**.</span></span>

### <a name="how-toowrite-traces-in-your-code"></a><span data-ttu-id="39b1e-110">Toowrite 如何追蹤程式碼中</span><span class="sxs-lookup"><span data-stu-id="39b1e-110">How toowrite traces in your code</span></span>
<span data-ttu-id="39b1e-111">在程式碼中撰寫追蹤很簡單。</span><span class="sxs-lookup"><span data-stu-id="39b1e-111">Writing traces in your code is easy.</span></span>  <span data-ttu-id="39b1e-112">在 C# 中是，只要撰寫下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="39b1e-112">In C# it's as easy as writing hello following code:</span></span>

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

<span data-ttu-id="39b1e-113">hello Trace 類別存在於 hello System.Diagnostics 命名空間。</span><span class="sxs-lookup"><span data-stu-id="39b1e-113">hello Trace class lives in hello System.Diagnostics namespace.</span></span>

<span data-ttu-id="39b1e-114">在 node.js 應用程式中，您可以撰寫此程式碼 tooachieve hello 相同的結果：</span><span class="sxs-lookup"><span data-stu-id="39b1e-114">In a node.js app you can write this code tooachieve hello same result:</span></span>

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-tooenable-and-view-hello-streaming-logs"></a><span data-ttu-id="39b1e-115">Tooenable 和檢視 hello 串流記錄</span><span class="sxs-lookup"><span data-stu-id="39b1e-115">How tooenable and view hello streaming logs</span></span>
<span data-ttu-id="39b1e-116">![][BrowseSitesScreenshot] 診斷會根據應用程式啟用。</span><span class="sxs-lookup"><span data-stu-id="39b1e-116">![][BrowseSitesScreenshot] Diagnostics are enabled on a per app basis.</span></span> <span data-ttu-id="39b1e-117">從開始瀏覽 toohello 網站希望 tooenable 這項功能。</span><span class="sxs-lookup"><span data-stu-id="39b1e-117">Start by browsing toohello site you would like tooenable this feature on.</span></span>  

<span data-ttu-id="39b1e-118">![][DiagnosticsLogs]從 [設定] 功能表，然後向下捲動 toohello**監視**區段，然後按一下**(1) 的診斷記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="39b1e-118">![][DiagnosticsLogs] From settings menu, scroll down toohello **Monitoring** section and click on **(1) Diagnostic Logs**.</span></span> <span data-ttu-id="39b1e-119">然後**(2) 啟用****的應用程式記錄 （檔案系統）**或**的應用程式記錄 (blob)** hello**層級**選項可讓您變更 hello追蹤 toocapture 嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="39b1e-119">Then **(2) enable** **Application Logging (Filesystem)** or **Application Logging (blob)** hello **Level** option lets you change hello severity level of traces toocapture.</span></span> <span data-ttu-id="39b1e-120">如果您只想要 tooget 熟悉 hello 功能，設定 hello 層級太**Verbose** tooensure 所有追蹤陳述式，都會收集。</span><span class="sxs-lookup"><span data-stu-id="39b1e-120">If you're just trying tooget familiar with hello feature, set hello level too**Verbose** tooensure all of your trace statements are collected.</span></span>

<span data-ttu-id="39b1e-121">按一下**儲存**頂端 hello hello 刀鋒視窗，而且您正在準備 tooview 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="39b1e-121">Click **SAVE** at hello top of hello blade and you're ready tooview logs.</span></span>

> [!NOTE]
> <span data-ttu-id="39b1e-122">hello 高 hello**嚴重性層級**hello 所需的資源取用的 toolog 和 hello 產生詳細的追蹤。</span><span class="sxs-lookup"><span data-stu-id="39b1e-122">hello higher hello **severity level** hello more resources are consumed toolog and hello more traces are produced.</span></span> <span data-ttu-id="39b1e-123">請確定**嚴重性層級**是生產或高流量網站設定的 toohello 正確的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="39b1e-123">Make sure **severity level** is configured toohello correct verbosity for a production or high traffic site.</span></span> 
> 
> 

<span data-ttu-id="39b1e-124">![][StreamingLogsScreenshot]tooview hello**資料流記錄**hello Azure 入口網站中按一下 [ **(1) 的記錄檔資料流**也在 hello**監視**hello 設定] 功能表上一節。</span><span class="sxs-lookup"><span data-stu-id="39b1e-124">![][StreamingLogsScreenshot] tooview hello **streaming logs** from within hello Azure portal, click on **(1) Log Stream** also in hello **Monitoring** section of hello settings menu.</span></span> <span data-ttu-id="39b1e-125">如果您的應用程式正在主動寫入追蹤陳述式，則您應該會看到 hello **(2) 資料流記錄 UI**幾近即時。</span><span class="sxs-lookup"><span data-stu-id="39b1e-125">If your app is actively writing trace statements, then you should see them in hello **(2) streaming logs UI** in near real time.</span></span>

## <a name="console"></a><span data-ttu-id="39b1e-126">主控台</span><span class="sxs-lookup"><span data-stu-id="39b1e-126">Console</span></span>
<span data-ttu-id="39b1e-127">hello **Azure 入口網站**提供主控台存取 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="39b1e-127">hello **Azure portal** provides console access tooyour app.</span></span> <span data-ttu-id="39b1e-128">您可以探索應用程式的檔案系統並執行 powershell/cmd 指令碼。</span><span class="sxs-lookup"><span data-stu-id="39b1e-128">You can explore your app's file system and run powershell/cmd scripts.</span></span> <span data-ttu-id="39b1e-129">由 hello 相同的權限設定為執行的應用程式程式碼執行主控台命令時，您會繫結。</span><span class="sxs-lookup"><span data-stu-id="39b1e-129">You are bound by hello same permissions set as your running app code when executing console commands.</span></span> <span data-ttu-id="39b1e-130">封鎖存取 tooprotected 目錄或執行需要提高權限的指令碼。</span><span class="sxs-lookup"><span data-stu-id="39b1e-130">Access tooprotected directories or running scripts that require elevated permissions is blocked.</span></span>  

<span data-ttu-id="39b1e-131">![][ConsoleScreenshot]從 [設定] 功能表，然後向下捲動太**開發工具**區段，然後按一下**（1） 主控台**和 hello **（2） 主控台**UI 開啟 toohello 權限。</span><span class="sxs-lookup"><span data-stu-id="39b1e-131">![][ConsoleScreenshot] From settings menu, scroll down too**Development Tools** section and click on **(1) Console** and hello **(2) console** UI opens toohello right.</span></span>

<span data-ttu-id="39b1e-132">熟悉 hello tooget**主控台**，再次嘗試基本命令，例如：</span><span class="sxs-lookup"><span data-stu-id="39b1e-132">tooget familiar with hello **console**, try basic commands like:</span></span>

`````````````````````````
dir
`````````````````````````

`````````````````````````
cd
`````````````````````````

<!-- Images. -->
[DiagnosticsLogs]: ./media/web-sites-streaming-logs-and-console/diagnostic-logs.png
[BrowseSitesScreenshot]: ./media/web-sites-streaming-logs-and-console/browse-sites.png
[StreamingLogsScreenshot]: ./media/web-sites-streaming-logs-and-console/streaming-logs.png
[ConsoleScreenshot]: ./media/web-sites-streaming-logs-and-console/console.png
