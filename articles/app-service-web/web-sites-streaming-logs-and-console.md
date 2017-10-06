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
# <a name="streaming-logs-and-hello-console"></a>資料流處理的記錄檔和 hello 主控台
## <a name="streaming-logs"></a>串流記錄
hello **Azure 入口網站**提供了整合式資料流記錄檔檢視器，可讓您檢視追蹤事件，從您**App Service**即時應用程式。  

設定此功能只需要一些簡單的步驟：

* 在程式碼中撰寫追蹤
* 啟用您應用程式的應用程式**診斷記錄**
* 檢視 hello hello 內建資料流**串流記錄**UI 中 hello **Azure 入口網站**。

### <a name="how-toowrite-traces-in-your-code"></a>Toowrite 如何追蹤程式碼中
在程式碼中撰寫追蹤很簡單。  在 C# 中是，只要撰寫下列程式碼的 hello:

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

hello Trace 類別存在於 hello System.Diagnostics 命名空間。

在 node.js 應用程式中，您可以撰寫此程式碼 tooachieve hello 相同的結果：

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-tooenable-and-view-hello-streaming-logs"></a>Tooenable 和檢視 hello 串流記錄
![][BrowseSitesScreenshot] 診斷會根據應用程式啟用。 從開始瀏覽 toohello 網站希望 tooenable 這項功能。  

![][DiagnosticsLogs]從 [設定] 功能表，然後向下捲動 toohello**監視**區段，然後按一下**(1) 的診斷記錄檔**。 然後**(2) 啟用****的應用程式記錄 （檔案系統）**或**的應用程式記錄 (blob)** hello**層級**選項可讓您變更 hello追蹤 toocapture 嚴重性層級。 如果您只想要 tooget 熟悉 hello 功能，設定 hello 層級太**Verbose** tooensure 所有追蹤陳述式，都會收集。

按一下**儲存**頂端 hello hello 刀鋒視窗，而且您正在準備 tooview 記錄檔。

> [!NOTE]
> hello 高 hello**嚴重性層級**hello 所需的資源取用的 toolog 和 hello 產生詳細的追蹤。 請確定**嚴重性層級**是生產或高流量網站設定的 toohello 正確的詳細資訊。 
> 
> 

![][StreamingLogsScreenshot]tooview hello**資料流記錄**hello Azure 入口網站中按一下 [ **(1) 的記錄檔資料流**也在 hello**監視**hello 設定] 功能表上一節。 如果您的應用程式正在主動寫入追蹤陳述式，則您應該會看到 hello **(2) 資料流記錄 UI**幾近即時。

## <a name="console"></a>主控台
hello **Azure 入口網站**提供主控台存取 tooyour 應用程式。 您可以探索應用程式的檔案系統並執行 powershell/cmd 指令碼。 由 hello 相同的權限設定為執行的應用程式程式碼執行主控台命令時，您會繫結。 封鎖存取 tooprotected 目錄或執行需要提高權限的指令碼。  

![][ConsoleScreenshot]從 [設定] 功能表，然後向下捲動太**開發工具**區段，然後按一下**（1） 主控台**和 hello **（2） 主控台**UI 開啟 toohello 權限。

熟悉 hello tooget**主控台**，再次嘗試基本命令，例如：

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
