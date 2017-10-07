---
title: "aaaAzure Insights 遙測資料模型的應用程式的遙測內容 |Microsoft 文件"
description: "Application Insights 遙測內容資料模型"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/15/2017
ms.author: sergkanz
ms.openlocfilehash: 6cdd6240d1c448f883d104a871ee9d5f6b5af2ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-context-application-insights-data-model"></a>遙測內容：Application Insights 資料模型

每個遙測項目都可能具有強型別的內容欄位。 每個欄位都具有特定的監視案例。 使用 hello 自訂屬性集合 toostore 自訂或特定應用程式的內容資訊。


##<a name="application-version"></a>應用程式版本

Hello 應用程式內容欄位中的資訊永遠是有關傳送嗨遙測的 hello 應用程式。 應用程式版本是使用的 tooanalyze 趨勢變更 hello 應用程式行為以及其相互關聯 toohello 部署。

最大長度：1024


##<a name="client-ip-address"></a>用戶端 IP 位址

hello hello 用戶端裝置的 IP 位址。 支援 IPv4 和 IPv6。 從服務傳送遙測，hello 位置內容時，關於 hello 使用者起始 hello 服務中的 hello 作業。 Application Insights 從 hello 用戶端 IP 擷取 hello 地理位置資訊，並予以截斷。 因此用戶端 IP 本身無法作為終端使用者識別資訊。 

最大長度：46


##<a name="device-type"></a>裝置類型

這個欄位用最初 tooindicate hello 類型 hello 裝置 hello hello 應用程式的終端使用者使用。 今天主要 toodistinguish JavaScript 遙測 hello 裝置類型使用 '瀏覽器' 從伺服器端遙測 hello 'PC' 的裝置類型。

最大長度：64


##<a name="operation-id"></a>作業 id

Hello 根作業的唯一識別碼。 這個識別碼可跨多個元件，讓 toogroup 遙測。 如需詳細資訊，請參閱[遙測相互關聯](application-insights-correlation.md)。 hello 作業 id 會建立 要求 或 頁面檢視。 所有其他遙測設定 hello 包含要求或頁面檢視此欄位 toohello 值。 

最大長度：128


##<a name="parent-operation-id"></a>父作業識別碼

hello hello 遙測項目的直屬父系的唯一識別碼。 如需詳細資訊，請參閱[遙測相互關聯](application-insights-correlation.md)。

最大長度：128


##<a name="operation-name"></a>作業名稱

hello 作業的 hello 名稱 （群組）。 hello 作業名稱會建立 要求 或 頁面檢視。 所有其他遙測項目欄位 toohello 將此值設定 hello 包含要求或頁面的檢視。 作業名稱會尋找所有 hello 遙測項目群組的作業 (例如 ' GET Home/Index ')。 這個內容屬性是使用的 tooanswer 類似 「 什麼是 hello 擲回此頁面上的一般例外狀況 」。

最大長度：1024


##<a name="synthetic-source-of-hello-operation"></a>綜合作業來源的 hello

綜合來源的名稱。 某些 hello 應用程式的遙測可能代表綜合流量。 它可能 web crawler 建立索引 hello web 站台、 站台可用性測試或從診斷程式庫，例如 Application Insights SDK 本身的追蹤。

最大長度：1024


##<a name="session-id"></a>工作階段識別碼

工作階段識別碼 hello hello 使用者互動 hello 應用程式執行個體。 Hello 工作階段內容欄位中的資訊永遠是關於 hello 終端使用者。 從服務傳送遙測，hello 工作階段內容時，關於 hello 使用者起始 hello 服務中的 hello 作業。

最大長度：64


##<a name="anonymous-user-id"></a>匿名使用者識別碼

匿名使用者識別碼。代表 hello hello 應用程式的使用者。 從服務傳送遙測，hello 使用者內容時，關於 hello 使用者起始 hello 服務中的 hello 作業。

[取樣](app-insights-sampling.md)是其中一個 hello 技術 toominimize hello 數量所收集的遙測。 取樣演算法嘗試 tooeither in 或 out 所有 hello 的範例相互關聯的遙測。 匿名使用者識別碼可用於產生取樣分數。 因此匿名使用者識別碼應該為足夠隨機的值。 

使用匿名使用者識別碼 toostore 使用者名稱是 hello 欄位誤用。 使用已驗證的使用者識別碼。

最大長度：128


##<a name="authenticated-user-id"></a>已驗證的使用者識別碼

已驗證的使用者識別碼。相反的 hello 匿名使用者 id，這個欄位代表 hello 使用者易記名稱。 由於其 PII 資訊，根據預設，大部分的 SDK 都不會收集該資訊。

最大長度：1024


##<a name="account-id"></a>帳戶識別碼

在多租用戶應用程式中，這是 hello 帳戶識別碼或名稱，與 hello 使用者做。 範例包括 Azure 入口網站的訂用帳戶識別碼或部落格平台的部落格名稱。

最大長度：1024


##<a name="cloud-role"></a>雲端角色

Hello 角色 hello 應用程式的名稱是的一部分。 直接對應 toohello 在 azure 中的角色名稱。 也可以使用的 toodistinguish 屬於單一應用程式中的微服務。

最大長度：256


##<a name="cloud-role-instance"></a>雲端角色執行個體

Hello hello 應用程式執行所在的執行個體名稱。 內部部署的電腦名稱、Azure 的執行個體名稱。

最大長度：256


##<a name="internal-sdk-version"></a>內部：SDK 版本

SDK 版本。 如需相關資訊，請參閱 https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification。

最大長度：64


##<a name="internal-node-name"></a>內部：節點名稱

此欄位會顯示用來進行計費的 hello 節點名稱。 使用 toooverride hello 標準偵測的節點。

最大長度：256


## <a name="next-steps"></a>後續步驟

- 了解如何太[擴充和篩選遙測](app-insights-api-filtering-sampling.md)。
- 如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。
- 請查看標準內容屬性集合[組態](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet)。
