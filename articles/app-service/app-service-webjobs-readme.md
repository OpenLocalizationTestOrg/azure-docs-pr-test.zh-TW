---
title: "Azure App Service 中的 WebJobs"
description: "了解如何建置 WebJobs 以執行背景測試、與儲存體和服務匯流排之類的服務進行互動，以及建立排定的工作。"
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
ms.openlocfilehash: 1ca6d2eabe9781a8bb09fc5948ed306e3e8b013c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-webjobs-in-azure-app-service"></a><span data-ttu-id="c1052-103">在 Azure App Service 中使用 WebJobs</span><span class="sxs-lookup"><span data-stu-id="c1052-103">Using WebJobs in Azure App Service</span></span>
<span data-ttu-id="c1052-104">本文連結至有關如何使用 Azure WebJobs 和 Azure WebJobs SDK 的文件資源。</span><span class="sxs-lookup"><span data-stu-id="c1052-104">This article links to documentation resources about how to use Azure WebJobs and the Azure WebJobs SDK.</span></span> <span data-ttu-id="c1052-105">Azure WebJob 可讓您輕鬆地在 [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714)上以背景處理序的方式執行指令碼或程式。</span><span class="sxs-lookup"><span data-stu-id="c1052-105">Azure WebJobs provide an easy way to run scripts or programs as background processes on [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="c1052-106">您可以上傳並執行可執行檔，例如 cmd、bat、exe (.NET)、ps1、sh、php、py、js 和 jar。</span><span class="sxs-lookup"><span data-stu-id="c1052-106">You can upload and run an executable file such as as cmd, bat, exe (.NET), ps1, sh, php, py, js and jar.</span></span> <span data-ttu-id="c1052-107">這些程式會依照排程 (cron) 或持續當作 WebJobs 執行。</span><span class="sxs-lookup"><span data-stu-id="c1052-107">These programs run as WebJobs on a schedule (cron) or continuously.</span></span>

<span data-ttu-id="c1052-108">WebJobs SDK 可讓您更輕鬆地使用 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="c1052-108">The WebJobs SDK makes it easier to use Azure Storage.</span></span> <span data-ttu-id="c1052-109">WebJobs SDK 具有繫結和觸發系統，適用於 Microsoft Azure 儲存體 Blob、佇列和資料表以及服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="c1052-109">The WebJobs SDK has a binding and trigger system which works with Microsoft Azure Storage Blobs, Queues and Tables as well as Service Bus Queues.</span></span>

<span data-ttu-id="c1052-110">使用 Visual Studio 中的整合工具可完美地建立、部署和管理 WebJobs。</span><span class="sxs-lookup"><span data-stu-id="c1052-110">Creating, deploying, and managing WebJobs is seamless with integrated tooling in Visual Studio.</span></span> <span data-ttu-id="c1052-111">您可以從範本建立 WebJobs、發佈及管理 (執行/停止/監視/偵錯) 它們。</span><span class="sxs-lookup"><span data-stu-id="c1052-111">You can create WebJobs from templates, publish, and manage (run/stop/monitor/debug) them.</span></span>

<span data-ttu-id="c1052-112">Azure 入口網站中的 WebJob 儀表板提供強大的管理功能，讓您能夠完全掌控 WebJob 的執行，包括叫用 WebJob 內個別函數的功能。</span><span class="sxs-lookup"><span data-stu-id="c1052-112">The WebJobs dashboard in the Azure portal provides powerful management capabilities that give you full control over the execution of WebJobs, including the ability to invoke individual functions within WebJobs.</span></span> <span data-ttu-id="c1052-113">儀表板也會顯示函數執行階段和記錄輸出。</span><span class="sxs-lookup"><span data-stu-id="c1052-113">The dashboard also displays function runtimes and logging output.</span></span>

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

