---
title: "aaaMobile Engagement 匯出 API 概觀"
description: "了解 hello 基本概念匯出未經處理資料所產生使用者的裝置 tooleverage 它在您自己的工具"
services: mobile-engagement
documentationcenter: mobile
author: kpiteira
manager: erikre
editor: 
ms.assetid: 9380d47b-d7fa-4d4c-888f-97e6482196bb
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 04/26/2016
ms.author: kapiteir
ms.openlocfilehash: f55be29a29878e74f6a33419f08a5574a07a7478
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="mobile-engagement-export-api-overview"></a>Mobile Engagement 匯出 API 概觀
## <a name="introduction"></a>簡介
在本文件中，您將學習 hello 基本概念匯出未經處理資料所產生使用者的裝置 tooleverage 它在您自己的工具。

## <a name="pre-requisites"></a>必要條件
Mobile Engagement 的 hello 原始資料匯出需要：

* API 驗證安裝程式 toobe 無法 toouse hello Api (請參閱[驗證手動安裝](mobile-engagement-api-authentication-manual.md))，
* 使用 REST Api hello [.net SDK](mobile-engagement-dotnet-sdk-service-api.md)，
* Azure 儲存體帳戶。

> [!NOTE]
> 我們也建議在 hello 絕佳[Microsoft Azure 儲存體總管](http://storageexplorer.com/)，至少 hello 開發階段，因為它可提供簡單的 toouse UI 互動與 Azure 儲存體。
> 
> 

## <a name="what-can-be-exported"></a>您可以匯出什麼？
Mobile Engagement 可讓其使用者 toocollect 許多類型的資料和匯出的數種因此具有適合 toothese 不同的資料類型。
有 2 種基本類型的匯出︰

* 快照集： 通常用於 tooexport 資料所代表的狀態和 Mobile Engagement 沒有歷程記錄。 比方說，這包括標籤 (應用程式資訊)、權杖或推播宣傳活動的意見反應。 因此這些型別匯出的不相關 tooa 日期。
* 歷程記錄︰此匯出類型用於會隨一段時間累積的資料，例如事件或活動。

hello 下表描述徹底所有 hello 可能匯出：

| 匯出類型 | 資料類型 | 說明 |
| --- | --- | --- |
| 快照 |推播 |針對每個裝置識別碼/使用者識別碼，產生推播宣傳活動意見反應的匯出 |
| 快照 |Tag |產生 hello 關聯的標記 （應用程式資訊） tooeach 裝置的匯出 |
| 快照 |裝置 |產生大多數的 hello hello technicals （模型、 地區設定、 時區、）、 hello 標記、 第一個看到的時間，例如裝置相關的資料的匯出... |
| 快照 |權杖 |會產生所有 hello 有效權杖的匯出 |
| 歷程記錄 |活動 |會產生在指定的時段內的每個裝置的所有 hello 活動匯出 |
| 歷程記錄 |Event |會產生在指定的時段內的每個裝置的所有 hello 活動匯出 |
| 歷程記錄 |作業 |會產生在指定的時段內的每個裝置的所有 hello 工作匯出 |
| 歷程記錄 |錯誤 |會產生在指定的時段內的每個裝置的所有 hello 錯誤匯出 |

## <a name="how-does-it-work"></a>運作方式
匯出是長時間執行的工作，可能會產生大型資料檔案。 因此，它們不能是叫用的 tooreturn 立即檔案 toodownload。
在 Mobile Engagement 的訂單 tooexport 資料，您可以 toocreate**匯出作業**應用程式開發介面，讓您指定通常透過：

* （快照式或歷程記錄），匯出的 hello 型別
* hello 資料型別，
* hello **Azure 儲存體容器**（包括具有寫入存取權的有效 SAS） 的 hello 匯出的 hello 結果寫入的位置。
* 例如︰範例容器 URL 參數會是 https://[StorageAccountName].blob.core.windows.net/[ContainerName]?[SASWritePermissionsToken]  

以下是真實範例。 https://testazmeexport.blob.core.windows.net/test1234azme?sv=2015-12-11&ss=b&srt=sco&sp=rwdlac&se=2016-12-17T04:59:26Z&st=2016-12-16T20:59:26Z&spr=https&sig=KRF3aVWjp2NEJDzjlmoplmu0M9HHlLdkBWRPAFmw90Q%3D

請注意，可能需要幾分鐘，讓您的工作 toobe 啟動，則表示它可能會執行從幾秒，讓應用程式的使用者或活動大量的小型應用程式 tooseveral 小時。

一旦建立 hello 作業時，就可能 toocheck 其狀態 toosee 是否依然執行或已完成。

Hello 作業是成功，hello 產生的資料檔案位於 hello 提供儲存體容器。

