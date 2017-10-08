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
# <a name="using-webjobs-in-azure-app-service"></a>在 Azure App Service 中使用 WebJobs
這篇文章會連結 toodocumentation 資源有關 toouse Azure WebJobs 和 hello Azure WebJobs SDK。 Azure WebJobs 提供簡單的方式 toorun 指令碼或程式為在背景處理序[App Service Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)。 您可以上傳並執行可執行檔，例如 cmd、bat、exe (.NET)、ps1、sh、php、py、js 和 jar。 這些程式會依照排程 (cron) 或持續當作 WebJobs 執行。

hello WebJobs SDK 可讓您更輕鬆 toouse Azure 儲存體。 hello WebJobs SDK 已繫結和觸發程序可搭配 Microsoft Azure 儲存體 Blob、 佇列和資料表與服務匯流排佇列的系統。

使用 Visual Studio 中的整合工具可完美地建立、部署和管理 WebJobs。 您可以從範本建立 WebJobs、發佈及管理 (執行/停止/監視/偵錯) 它們。

hello Azure 入口網站中的 hello WebJobs 儀表板會提供功能強大的管理功能，可讓您完全掌控 hello 執行 WebJobs，包括 hello 能力 tooinvoke 個別函式內 WebJobs。 函式執行階段和記錄輸出，也會顯示 hello 儀表板。

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

