---
title: "Azure App Service 中 aaaWebJobs"
description: "了解 toobuild WebJobs toorun 背景如何測試、 與服務，例如儲存體和 Service Bus 互動並建立排定的工作。"
services: app-service
documentationcenter: 
author: christopheranderson
manager: erikre
editor: mollybos
ms.assetid: 85975432-04c9-4b83-b937-b30c082d52a1
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/10/2015
ms.author: chrande
ms.openlocfilehash: 25c24bfe71a64036cd48e58f471995b4a06e3b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-webjobs-in-azure-app-service"></a><span data-ttu-id="0a840-103">在 Azure App Service 中使用 WebJobs</span><span class="sxs-lookup"><span data-stu-id="0a840-103">Using WebJobs in Azure App Service</span></span>
<span data-ttu-id="0a840-104">這篇文章會連結 toodocumentation 資源有關 toouse Azure WebJobs 和 hello Azure WebJobs SDK。</span><span class="sxs-lookup"><span data-stu-id="0a840-104">This article links toodocumentation resources about how toouse Azure WebJobs and hello Azure WebJobs SDK.</span></span> <span data-ttu-id="0a840-105">Azure WebJobs 提供簡單的方式 toorun 指令碼或程式為在背景處理序[App Service Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)。</span><span class="sxs-lookup"><span data-stu-id="0a840-105">Azure WebJobs provide an easy way toorun scripts or programs as background processes on [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="0a840-106">您可以上傳並執行可執行檔，例如 cmd、bat、exe (.NET)、ps1、sh、php、py、js 和 jar。</span><span class="sxs-lookup"><span data-stu-id="0a840-106">You can upload and run an executable file such as as cmd, bat, exe (.NET), ps1, sh, php, py, js and jar.</span></span> <span data-ttu-id="0a840-107">這些程式會依照排程 (cron) 或持續當作 WebJobs 執行。</span><span class="sxs-lookup"><span data-stu-id="0a840-107">These programs run as WebJobs on a schedule (cron) or continuously.</span></span>

<span data-ttu-id="0a840-108">hello WebJobs SDK 可讓您更輕鬆 toouse Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="0a840-108">hello WebJobs SDK makes it easier toouse Azure Storage.</span></span> <span data-ttu-id="0a840-109">hello WebJobs SDK 已繫結和觸發程序可搭配 Microsoft Azure 儲存體 Blob、 佇列和資料表與服務匯流排佇列的系統。</span><span class="sxs-lookup"><span data-stu-id="0a840-109">hello WebJobs SDK has a binding and trigger system which works with Microsoft Azure Storage Blobs, Queues and Tables as well as Service Bus Queues.</span></span>

<span data-ttu-id="0a840-110">使用 Visual Studio 中的整合工具可完美地建立、部署和管理 WebJobs。</span><span class="sxs-lookup"><span data-stu-id="0a840-110">Creating, deploying, and managing WebJobs is seamless with integrated tooling in Visual Studio.</span></span> <span data-ttu-id="0a840-111">您可以從範本建立 WebJobs、發佈及管理 (執行/停止/監視/偵錯) 它們。</span><span class="sxs-lookup"><span data-stu-id="0a840-111">You can create WebJobs from templates, publish, and manage (run/stop/monitor/debug) them.</span></span>

<span data-ttu-id="0a840-112">hello Azure 入口網站中的 hello WebJobs 儀表板會提供功能強大的管理功能，可讓您完全掌控 hello 執行 WebJobs，包括 hello 能力 tooinvoke 個別函式內 WebJobs。</span><span class="sxs-lookup"><span data-stu-id="0a840-112">hello WebJobs dashboard in hello Azure portal provides powerful management capabilities that give you full control over hello execution of WebJobs, including hello ability tooinvoke individual functions within WebJobs.</span></span> <span data-ttu-id="0a840-113">函式執行階段和記錄輸出，也會顯示 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="0a840-113">hello dashboard also displays function runtimes and logging output.</span></span>

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

