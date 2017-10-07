---
title: "aaaMonitoring Azure 函式 |Microsoft 文件"
description: "深入了解如何 toomonitor Azure 函式。"
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函式, 事件處理, webhook, 動態計算, 無伺服器架構"
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: 254348d1cefce925654bd9532715b6def571e0ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-functions"></a>監視 Azure Functions

## <a name="overview"></a>概觀 


hello**監視器**索引標籤上，每個函式可讓您 tooreview 函式的每個執行。

![Azure Functions 監視索引標籤](./media/functions-monitoring/monitor-tab.png) 

按一下 執行可讓您 tooreview hello 持續期間、 輸入的資料、 錯誤和關聯的記錄檔。 這對於函式的偵錯和效能調整很實用。


> [!IMPORTANT]
> 當使用 hello[裝載計劃的耗用量](functions-overview.md#pricing)對於 Azure 函式，hello**監視**hello 函式應用程式概觀刀鋒視窗中的磚將不會顯示任何資料。 這是因為 hello 平台動態調整，以及讓這些計量並沒有意義耗用量計劃，為您管理運算執行個體。 toomonitor hello 函式應用程式，您應該改為使用 hello 指引本文中。
> 
> 下列螢幕擷取畫面的 hello 顯示範例：
> 
> ![Hello 主要資源刀鋒視窗上的監視](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a>即時監視

按一下如下所示的 [即時事件串流]，即可進行即時監視。 

![即時事件資料流 hello 監視 索引標籤選項](./media/functions-monitoring/monitor-tab-live-event-stream.png)

將新的瀏覽器索引標籤以繪製 hello 即時事件資料流，如下所示。 

![即時事件串流範例](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> 沒有已知的問題，可能會造成填入您資料 toofail toobe。 如果您遇到的情況，您可能需要 tooclose hello 瀏覽器索引標籤包含 hello 即時事件資料流，然後按一下**即時事件資料流**再次 tooallow 它 tooproperly 填入事件資料流資料。 

hello 即時事件資料流將圖形 hello 遵循您的函式的統計資料：

* 每秒啟動的執行數
* 每秒完成的執行數
* 每秒失敗的執行數
* 平均執行時間 (以毫秒為單位)。

這些統計資料是即時但是 hello 實際 hello 執行資料的圖形可能會有約 10 秒的延遲。






## <a name="monitoring-log-files-from-a-command-line"></a>從命令列監視記錄檔


您可以使用 hello Azure 命令列介面 (CLI) 或 PowerShell 在本機工作站串流記錄檔案 tooa 命令列工作階段。

### <a name="monitoring-function-app-log-files-with-hello-azure-cli"></a>監視以 hello Azure CLI 函式應用程式記錄檔

啟動，tooget[安裝 hello Azure CLI](../cli-install-nodejs.md)

登入您的 Azure 帳戶使用 hello 下列命令，或任何 hello 涵蓋，其他選項[登入從 hello Azure CLI tooAzure](../xplat-cli-connect.md)。

    azure login

使用 hello 下列命令 tooenable Azure CLI 服務管理 (ASM) 模式:。

    azure config mode asm

如果您有多個訂閱，使用下列命令 toolist hello，您的訂用帳戶和設定 hello 目前訂用帳戶 toohello 訂用帳戶，其中包含應用程式函式。

    azure account list
    azure account set <subscriptionNameOrId>

hello 下列命令會串流 hello 記錄檔的函式應用程式 toohello 命令列：

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a>使用 PowerShell 監視函式應用程式記錄檔

啟動，tooget[安裝和設定 Azure PowerShell](/powershell/azure/overview)。

加入您的 Azure 帳戶執行下列命令的 hello:

    PS C:\> Add-AzureAccount

如果您有多個訂閱，您可以列出名稱以下列命令 toosee，如果正確的訂用帳戶為目前選取的 hello hello 為基礎的 hello`IsCurrent`屬性：

    PS C:\> Get-AzureSubscription

如果您需要 tooset hello 作用中訂用帳戶 toohello 一個包含您的函式應用程式，請使用下列命令的 hello:

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

資料流 hello 記錄 tooyour PowerShell 工作階段以 hello 下列命令：

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

如需詳細資訊，請參閱太[How to： 在 web 應用程式記錄檔資料流](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs)。 

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱下列資源的 hello:

* [測試函數](functions-test-a-function.md)
* [調整函數](functions-scale.md)

