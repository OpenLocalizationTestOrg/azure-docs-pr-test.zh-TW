---
title: "aaaAzure 函式概觀 |Microsoft 文件"
description: "了解如何 toouse Azure 函式 toooptimize 非同步工作負載以分鐘為單位。"
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函式, 事件處理, webhook, 動態計算, 無伺服器架構"
ms.assetid: 01d6ca9f-ca3f-44fa-b0b9-7ffee115acd4
ms.service: functions
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 668f9055a007fee662a4c7ec774d3c0a1d847800
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-functions"></a>簡介 tooAzure 函式  
Azure 的函式會很輕鬆地執行少量的程式碼或 「 函數 」 方案 hello 雲端中。 您可以撰寫只 hello 程式碼，不必耽心整個應用程式或 hello 基礎結構 toorun 它需要手邊，hello 問題。 Functions 可讓開發更有生產力，而且您可以使用您選擇的開發語言，例如 C#、F#、Node.js、Python 或 PHP。 只支付您的程式碼執行的 hello 時間，視信任 Azure tooscale。 Azure Functions 可讓您在 Microsoft Azure 上開發無伺服器應用程式。

本主題提供 Azure Functions 的高階概觀。 如果您希望 toojump right，並開始使用 Azure 函式，以啟動[建立您的第一個 Azure 函式](functions-create-first-azure-function.md)。 如果您要尋找有關函數的更多技術資訊，請參閱 hello[開發人員參考](functions-reference.md)。

## <a name="features"></a>特性
以下是 Azure Functions 的一些主要功能︰

* **選擇的語言** - 使用 C#、F#、Node.js、Python、PHP、batch、bash 或任何可執行檔撰寫函式。
* **付款-每次使用定價模型**付費-只針對 hello 時間花在執行您的程式碼。 請參閱 hello 耗用量裝載計劃中 hello 選項[定價區段](#pricing)。  
* **自備相依性** - Functions 支援 NuGet 和 NPM，以便您使用您最愛的程式庫。  
* **整合式安全性** - 利用 OAuth 提供者 (如 Azure Active Directory、Facebook、Google、Twitter 和 Microsoft 帳戶) 保護 HTTP 觸發的函數。  
* **簡化整合** - 輕鬆地利用 Azure 服務和軟體即服務 (SaaS) 供應項目。 請參閱 hello[整合 > 一節](#integrations)的一些範例。  
* **彈性開發**-程式碼在 hello 入口網站中的將函式直接設定連續整合和部署您的程式碼到 GitHub、 Visual Studio Team Services 和其他[支援開發工具](../app-service-web/web-sites-deploy.md#deploy-using-an-ide)。  
* **開放原始碼**-hello 函式執行階段是開放原始碼和[github](https://github.com/azure/azure-webjobs-sdk-script)。  

## <a name="what-can-i-do-with-functions"></a>我可以用 Functions 來做什麼？
Azure 的函式很棒的解決方案來處理資料、 整合系統中，使用 hello 網際網路的物聯網 (IoT)，並建置簡單的應用程式開發介面和 microservices。 對於工作，例如影像或訂單處理、 檔案維護或您想 toorun 排程任何工作，請考慮函式。 

函式會提供您一開始安裝重要的案例，包括 hello 下列範本 tooget:

* **BlobTrigger** -加入時加以 toocontainers 程序的 Azure 儲存體的 blob。 您可以使用此函式調整映像大小。
* **EventHubTrigger** -回應 tooevents 傳遞 tooan Azure 事件中心。 特別適合用於應用程式檢測、使用者經驗或工作流程處理及物聯網 (IoT) 案例。
* **泛型 webhook** - 處理來自支援 webhook 的任何服務的 webhook HTTP 要求。
* **GitHub webhook** -回應 tooevents 您 GitHub 儲存機制中發生。 如需範例，請參閱 [建立 Webhook 或 API 函數](functions-create-a-web-hook-or-api-function.md)。
* **HTTPTrigger** -觸發 hello 執行程式碼使用的 HTTP 要求。
* **QueueTrigger** -回應 toomessages 達 Azure 儲存體佇列中。 如需範例，請參閱[建立 Azure 函式繫結 tooan Azure 服務](functions-create-an-azure-connected-function.md)。
* **ServiceBusQueueTrigger** -連接您的程式碼 tooother Azure 服務或內部部署服務所接聽的 toomessage 佇列。 
* **ServiceBusTopicTrigger** -連接您的程式碼 tooother Azure 服務或內部部署服務藉由訂閱 tootopics。 
* **TimerTrigger** - 在預先定義的排程執行清除或其他批次工作。 如需範例，請參閱 [建立事件處理函數](functions-create-an-event-processing-function.md)。

Azure 的函式支援*觸發程序*，此種 toostart 執行程式碼，和*繫結*，這在方式 toosimplify 撰寫程式碼的輸入和輸出資料。 Hello 觸發程序和 Azure 函式提供的繫結的詳細說明，請參閱[Azure 函式的觸發程序和繫結開發人員的參考](functions-triggers-bindings.md)。

## <a name="integrations"></a>整合
Azure Functions 可以與各種 Azure 和協力廠商服務整合。 這些服務可以觸發您的函式並開始執行，或做為您程式碼的輸入和輸出。 支援下列服務整合的 hello Azure 函式。 

* Azure Cosmos DB
* Azure 事件中心 
* Azure Mobile Apps (資料表)
* Azure 通知中心
* Azure 服務匯流排 (佇列和主題)
* Azure 儲存體 (Blob、佇列和資料表) 
* GitHub (webhook)
* 內部部署 (使用服務匯流排)
* Twilio (SMS 訊息)

## <a name="pricing"></a>Functions 的計費方式
Azure 的函式有兩種類型的定價方案時，最適合您需求的其中一個選擇 hello: 

* **耗用量計劃**-當您的函式會執行，Azure 會提供所有必要的計算資源 hello。 您不需要資源管理需 tooworry，您只需要針對您的程式碼執行的 hello 時間。 
* **App Service 方案** - 可讓您如同 Web、行動及 API 應用程式一樣執行函數。 當您已經為其他應用程式使用應用程式服務時，您可以執行您的函式上 hello 相同計劃不需要額外成本。 

完整的定價詳細資料位於 hello[函式定價頁面](https://azure.microsoft.com/pricing/details/functions/)。 如需調整您的函式的詳細資訊，請參閱[如何 tooscale Azure 函式](functions-scale.md)。

## <a name="next-steps"></a>後續步驟
* [建立您的第一個 Azure 函式](functions-create-first-azure-function.md)  
  您可以直接，並建立您使用 hello Azure 函式的快速入門的第一個函式。 
* [Azure Functions 開發人員參考](functions-reference.md)  
  提供程式碼撰寫函式，以及定義觸發程序和繫結的 hello Azure 函式執行階段和參考的其他技術資訊。
* [測試 Azure Functions](functions-test-a-function.md)  
  說明可用於測試函式的各種工具和技巧。
* [如何 tooscale Azure 函式](functions-scale.md)  
  討論適用於 Azure 函式，包括 hello 耗用量主控方案，以及如何 toochoose hello 右計劃的服務方案。 
* [深入了解 Azure App Service](../app-service/app-service-value-prop-what-is.md)  
  Azure 的函式會利用 hello Azure 應用程式服務的平台的核心功能，例如部署、 環境變數，以及診斷。 

