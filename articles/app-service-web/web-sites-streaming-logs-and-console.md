---
title: "串流記錄和主控台"
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
ms.openlocfilehash: 120ce6b115820728b9f853e9ff349beb0ef29c9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="streaming-logs-and-the-console"></a><span data-ttu-id="66745-103">串流記錄和主控台</span><span class="sxs-lookup"><span data-stu-id="66745-103">Streaming Logs and the Console</span></span>
## <a name="streaming-logs"></a><span data-ttu-id="66745-104">串流記錄</span><span class="sxs-lookup"><span data-stu-id="66745-104">Streaming Logs</span></span>
<span data-ttu-id="66745-105">**Azure 入口網站**提供整合式串流記錄檢視器，可讓您從 **App Service** 應用程式即時檢視追蹤事件。</span><span class="sxs-lookup"><span data-stu-id="66745-105">The **Azure portal** provides an integrated streaming log viewer that lets you view tracing events from your **App Service** apps in real time.</span></span>  

<span data-ttu-id="66745-106">設定此功能只需要一些簡單的步驟：</span><span class="sxs-lookup"><span data-stu-id="66745-106">Setting up this feature requires a few simple steps:</span></span>

* <span data-ttu-id="66745-107">在程式碼中撰寫追蹤</span><span class="sxs-lookup"><span data-stu-id="66745-107">Write traces in your code</span></span>
* <span data-ttu-id="66745-108">啟用您應用程式的應用程式**診斷記錄**</span><span class="sxs-lookup"><span data-stu-id="66745-108">Enable Application **Diagnostic Logs** for your app</span></span>
* <span data-ttu-id="66745-109">在 **Azure 入口網站**中檢視來自內建**串流記錄** UI 的串流。</span><span class="sxs-lookup"><span data-stu-id="66745-109">View the stream from the built-in **Streaming Logs** UI in the **Azure portal**.</span></span>

### <a name="how-to-write-traces-in-your-code"></a><span data-ttu-id="66745-110">如何在程式碼中撰寫追蹤</span><span class="sxs-lookup"><span data-stu-id="66745-110">How to write traces in your code</span></span>
<span data-ttu-id="66745-111">在程式碼中撰寫追蹤很簡單。</span><span class="sxs-lookup"><span data-stu-id="66745-111">Writing traces in your code is easy.</span></span>  <span data-ttu-id="66745-112">在 C# 中可輕易撰寫下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="66745-112">In C# it's as easy as writing the following code:</span></span>

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

<span data-ttu-id="66745-113">Trace 類別位於 System.Diagnostics 命名空間。</span><span class="sxs-lookup"><span data-stu-id="66745-113">The Trace class lives in the System.Diagnostics namespace.</span></span>

<span data-ttu-id="66745-114">您可以在 node.js 應用程式中，撰寫此程式碼以取得相同的結果：</span><span class="sxs-lookup"><span data-stu-id="66745-114">In a node.js app you can write this code to achieve the same result:</span></span>

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-to-enable-and-view-the-streaming-logs"></a><span data-ttu-id="66745-115">如何啟用和檢視串流記錄</span><span class="sxs-lookup"><span data-stu-id="66745-115">How to enable and view the streaming logs</span></span>
<span data-ttu-id="66745-116">![][BrowseSitesScreenshot] 診斷會根據應用程式啟用。</span><span class="sxs-lookup"><span data-stu-id="66745-116">![][BrowseSitesScreenshot] Diagnostics are enabled on a per app basis.</span></span> <span data-ttu-id="66745-117">開始瀏覽至您想要啟用這項功能的網站。</span><span class="sxs-lookup"><span data-stu-id="66745-117">Start by browsing to the site you would like to enable this feature on.</span></span>  

<span data-ttu-id="66745-118">![][DiagnosticsLogs] 從 [設定] 功能表中，向下捲動至 [監視] 區段，然後按一下 [(1) 診斷記錄]。</span><span class="sxs-lookup"><span data-stu-id="66745-118">![][DiagnosticsLogs] From settings menu, scroll down to the **Monitoring** section and click on **(1) Diagnostic Logs**.</span></span> <span data-ttu-id="66745-119">然後 [(2) 啟用] **應用程式記錄 (檔案系統)** 或**應用程式記錄 (Blob)**。[層級] 選項可讓您變更要擷取之追蹤的嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="66745-119">Then **(2) enable** **Application Logging (Filesystem)** or **Application Logging (blob)** The **Level** option lets you change the severity level of traces to capture.</span></span> <span data-ttu-id="66745-120">如果您才剛嘗試熟悉此功能，將層級設定為 [詳細資訊]，以確保收集所有追蹤陳述式。</span><span class="sxs-lookup"><span data-stu-id="66745-120">If you're just trying to get familiar with the feature, set the level to **Verbose** to ensure all of your trace statements are collected.</span></span>

<span data-ttu-id="66745-121">按一下刀鋒頂端的 [儲存]  ，隨後可準備檢視記錄。</span><span class="sxs-lookup"><span data-stu-id="66745-121">Click **SAVE** at the top of the blade and you're ready to view logs.</span></span>

> [!NOTE]
> <span data-ttu-id="66745-122">**嚴重性層級**愈高，系統會耗用更多的資源進行記錄，且會產生更多追蹤。</span><span class="sxs-lookup"><span data-stu-id="66745-122">The higher the **severity level** the more resources are consumed to log and the more traces are produced.</span></span> <span data-ttu-id="66745-123">請確定**嚴重性層級**設定為正確的生產詳細資訊或高流量網站。</span><span class="sxs-lookup"><span data-stu-id="66745-123">Make sure **severity level** is configured to the correct verbosity for a production or high traffic site.</span></span> 
> 
> 

<span data-ttu-id="66745-124">![][StreamingLogsScreenshot] 若要檢視 Azure 入口網站內的**串流記錄**，按一下 [(1) 記錄串流] 以及 [設定] 功能表的 [監視] 區段。</span><span class="sxs-lookup"><span data-stu-id="66745-124">![][StreamingLogsScreenshot] To view the **streaming logs** from within the Azure portal, click on **(1) Log Stream** also in the **Monitoring** section of the settings menu.</span></span> <span data-ttu-id="66745-125">如果您的應用程式主動撰寫追蹤陳述式，則您應在 **(2) 資料流記錄 UI** 中近乎即時地看到這些追蹤陳述式。</span><span class="sxs-lookup"><span data-stu-id="66745-125">If your app is actively writing trace statements, then you should see them in the **(2) streaming logs UI** in near real time.</span></span>

## <a name="console"></a><span data-ttu-id="66745-126">主控台</span><span class="sxs-lookup"><span data-stu-id="66745-126">Console</span></span>
<span data-ttu-id="66745-127">**Azure 入口網站**提供能夠存取您 Web 應用程式環境的主控台。</span><span class="sxs-lookup"><span data-stu-id="66745-127">The **Azure portal** provides console access to your app.</span></span> <span data-ttu-id="66745-128">您可以探索應用程式的檔案系統並執行 powershell/cmd 指令碼。</span><span class="sxs-lookup"><span data-stu-id="66745-128">You can explore your app's file system and run powershell/cmd scripts.</span></span> <span data-ttu-id="66745-129">執行主控台命令時，您會受到與執行應用程式程式碼之相同權限集的限制。</span><span class="sxs-lookup"><span data-stu-id="66745-129">You are bound by the same permissions set as your running app code when executing console commands.</span></span> <span data-ttu-id="66745-130">已封鎖存取受保護的目錄或執行需要提高權限的指令碼。</span><span class="sxs-lookup"><span data-stu-id="66745-130">Access to protected directories or running scripts that require elevated permissions is blocked.</span></span>  

<span data-ttu-id="66745-131">![][ConsoleScreenshot] 從 [設定] 功能表中，向下捲動至 [開發工具] 區段，然後按一下 [(1) 主控台] 則 [(2) 主控台] UI 會在右方開啟。</span><span class="sxs-lookup"><span data-stu-id="66745-131">![][ConsoleScreenshot] From settings menu, scroll down to **Development Tools** section and click on **(1) Console** and the **(2) console** UI opens to the right.</span></span>

<span data-ttu-id="66745-132">若要熟悉**主控台**，請嘗試類似的基本命令：</span><span class="sxs-lookup"><span data-stu-id="66745-132">To get familiar with the **console**, try basic commands like:</span></span>

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
