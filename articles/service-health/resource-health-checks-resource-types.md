---
title: "透過 Azure 資源健全狀況的資源類型 aaaSupported |Microsoft 文件"
description: "透過 Azure 資源健康狀態支援的資源類型"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 03/19/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: fc7bef214702f8ba6954b5aca62236b38023d27a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resource-types-and-health-checks-in-azure-resource-health"></a>Azure 資源健康狀態中的資源類型和健康情況檢查
以下是所有的 hello 檢查透過資源健全狀況執行的資源類型的完整清單。

## <a name="microsoftcacheredisredis"></a>Microsoft.CacheRedis/Redis
|執行的檢查|
|---|
|<ul><li>Hello 快取的所有節點都都已啟動並執行？</li><li>可以快取 hello 從聯繫 hello 資料中心內？</li><li>已快取達到 hello 的連線數目上限的 hello？</li><li> Hello 快取已達可用的記憶體？ </li><li>Hello 快取發生分頁錯誤數目？</li><li>是在負載過重 hello 快取嗎？</li></ul>|

## <a name="microsoftcdnprofile"></a>Microsoft.CDN/profile
|執行的檢查|
|---|
|<ul> <li>任何 hello 端點已停止，已移除，或設定錯誤？</li><li>是 hello 補充入口網站存取 CDN 組態作業？</li><li>有進行中傳遞問題以 hello CDN 端點嗎？</li><li>使用者可以變更其 CDN 資源的 hello 組態嗎？</li><li>組態變更會傳播 hello 預期速率嗎？</li><li>使用者可以管理使用 hello Azure 入口網站、 PowerShell 或 hello API hello CDN 組態嗎？</li> </ul>|

## <a name="microsoftclassiccomputevirtualmachines"></a>Microsoft.classiccompute/virtualmachines
|執行的檢查|
|---|
|<ul><li>Hello 主機伺服器已啟動並執行？</li><li>已完成 hello 主機 OS 開機嗎？</li><li>佈建並開啟電源 hello 虛擬機器容器？</li><li>有 hello 主機與 hello 儲存體帳戶之間的網路連線嗎？</li><li>已完成 hello 開機的 hello 客體作業系統？</li><li>是否有持續性的規劃維護？</li></ul>|

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.cognitiveservices/accounts
|執行的檢查|
|---|
|<ul><li>可以 hello 帳戶從聯繫 hello 資料中心內？</li><li>是 hello 認知服務資源提供者可用？</li><li>是 hello 認知可用的服務在 hello 適當區域？</li><li>可以讀取作業 hello 保存 hello 資源的中繼資料的儲存體帳戶上執行？</li><li>已達到 hello API 呼叫配額？</li><li>已達到 hello API 呼叫讀取限制？</li></ul>|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.compute/virtualmachines
|執行的檢查|
|---|
|<ul><li>Hello 伺服器上裝載此虛擬機器，且執行？</li><li>已完成 hello 主機 OS 開機嗎？</li><li>佈建並開啟電源 hello 虛擬機器容器？</li><li>有 hello 主機與 hello 儲存體帳戶之間的網路連線嗎？</li><li>已完成 hello 開機的 hello 客體作業系統？</li><li>是否有持續性的規劃維護？</li></ul>|

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.datalakeanalytics/accounts
|執行的檢查|
|---|
|<ul><li>使用者送出作業中的 tooData Lake Analytics 可以 hello 區域？</li><li>執行基本工作執行並完成成功地在 hello 區域？</li><li>使用者可以列出 hello 區域中的類別目錄項目嗎？</li>|


## <a name="microsoftdatalakestoreaccounts"></a>Microsoft.datalakestore/accounts
|執行的檢查|
|---|
|<ul><li>使用者可以上傳資料區內 hello tooData 湖存放區嗎？</li><li>使用者可以從 Data Lake Store hello 區域中下載資料嗎？</li></ul>|

## <a name="microsoftdocumentdbdatabaseaccounts"></a>Microsoft.documentdb/databaseAccounts
|執行的檢查|
|---|
|<ul><li>已有任何資料庫或集合的要求不因為 tooa DocumentDB 服務無法使用服務？</li><li>已有未處理因為 tooa DocumentDB 服務無法使用任何文件要求嗎？</li></ul>|

## <a name="microsoftnetworkconnections"></a>Microsoft.network/connections
|執行的檢查|
|---|
|<ul><li>Hello VPN 通道連線？</li><li>Hello 連線中是否有設定衝突？</li><li>Hello 預先共用的金鑰正確設定嗎？</li><li>是 hello VPN 在內部部署裝置的連線嗎？</li><li>Hello IPSec/IKE 安全性原則中是否有不相符？</li><li>是 hello S2S VPN 連線正確佈建或處於失敗狀態？</li><li>是 hello VNET 對 VNET 連線正確佈建或處於失敗狀態？</li></ul>|

## <a name="microsoftnetworkvirtualnetworkgateways"></a>Microsoft.network/virtualNetworkGateways
|執行的檢查|
|---|
|<ul><li>是從 hello VPN 閘道 hello 網際網路嗎？</li><li>會在待命模式 hello VPN 閘道嗎？</li><li>Hello VPN 服務是否執行 hello 閘道？</li></ul>|

## <a name="microsoftnotificationhubsnamespace"></a>Microsoft.NotificationHubs/namespace
|執行的檢查|
|---|
|<ul><li> 可以在 hello 命名空間上執行執行階段作業，例如註冊、 安裝或傳送？</li></ul>|

## <a name="microsoftpowerbiworkspacecollections"></a>Microsoft.PowerBI/workspaceCollections
|執行的檢查|
|---|
|<ul><li>Hello 主機 OS 已啟動並執行？</li><li>是從 hello 資料中心外部連到 hello workspaceCollection？</li><li>是 hello PowerBI 資源提供者可用？</li><li>是 hello PowerBI hello 適當區域中可用的服務嗎？</li></ul>|

## <a name="microsoftsearchsearchservices"></a>Microsoft.search/searchServices
|執行的檢查|
|---|
|<ul><li>可以在 hello 叢集上執行診斷操作嗎？</li></ul>|

## <a name="microsoftsqlserverdatabase"></a>Microsoft.SQL/Server/database
|執行的檢查|
|---|
|<ul><li> 已有登入 toohello 資料庫嗎？</li></ul>|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs
|執行的檢查|
|---|
|<ul><li>是所有的 hello 主機是執行向上而執行 hello 作業嗎？</li><li>已 hello 工作無法 toostart 嗎？</li><li>有進行中的執行階段升級嗎？</li><li>是預期的狀態 （例如執行或停止的客戶） 中的 hello 工作嗎？</li><li>Hello 作業發現外的記憶體例外狀況？</li><li>是否有進行中的排程計算更新？</li><li>是 hello 執行管理員 （控制計畫） 可用？</li></ul>|

## <a name="microsoftwebserverfarms"></a>Microsoft.web/serverFarms
|執行的檢查|
|---|
|<ul><li>Hello 主機伺服器已啟動並執行？</li><li>網際網路資訊服務是否執行中？</li><li>正在執行的 hello 負載平衡器</li><li>可以 hello Web 服務計劃從聯繫 hello 資料中心內？</li><li>是 hello 儲存體帳戶裝載 hello 站台內容的 hello serverFarm 可用??</li></ul>|

## <a name="microsoftwebsites"></a>Microsoft.web/sites
|執行的檢查|
|---|
|<ul><li>Hello 主機伺服器已啟動並執行？</li><li>網際網路資訊服務是否執行中？</li><li>正在執行的 hello 負載平衡器</li><li>可以 hello Web 應用程式從聯繫 hello 資料中心內？</li><li>Hello 儲存體帳戶裝載 hello 站台的內容嗎？</li></ul>|

# <a name="next-steps"></a>後續步驟
-  請參閱[簡介 tooAzure 服務健全狀況](service-health-overview.md)和[簡介 tooAzure 資源健全狀況](resource-health-overview.md)toounderstand 深入了解它們。 
-  [關於 Azure 資源健康狀態的常見問題集](resource-health-faq.md)
- 設定警示，如此就能收到健康狀態問題的通知。 如需詳細資訊，請參閱[設定適用於服務健康情況的警示](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md)。 