---
title: "aaaMonitor Azure App Service 中的應用程式 |Microsoft 文件"
description: "了解如何使用 Azure App Service 中的 toomonitor 應用程式 hello Azure 入口網站。"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: d273da4e-07de-48e0-b99d-4020d84a425e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: byvinyal
ms.openlocfilehash: 80d5a466102a894a49d04ae35aa54cc1d05a58df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a>作法：監視 Azure App Service 中的應用程式
[應用程式服務](http://go.microsoft.com/fwlink/?LinkId=529714)會提供內建的監視功能，在 hello [Azure 入口網站](https://portal.azure.com)。
這包括 hello 能力 tooreview**配額**和**度量**應用程式，以及設定的 App Service 方案 hello**警示**，甚至**調整**自動根據這些度量。

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a>了解配額和計量
### <a name="quotas"></a>配額
App Service 中裝載的應用程式是主體 toocertain*限制*上可以使用的資源。 hello 限制由定義 hello **App Service 方案**hello 應用程式相關聯。

如果 hello 應用程式裝載在**免費**或**共用**計劃，則會由 hello hello hello 應用程式可以使用的資源限制**配額**。

如果 hello 應用程式裝載在**基本**，**標準**或**Premium**計劃，然後由 hello 設定 hello 他們可以使用的資源上的 hello 限制**大小**（小型、 中型的大） 和**執行個體計數**（1、 2、 3 …） 的 hello **App Service 方案**。

**免費**或**共用**應用程式的**配額**如下︰

* **CPU (短期)**
  * 此應用程式在 5 分鐘間隔內允許的 CPU 數量。 此配額會每 5 分鐘重設一次。
* **CPU (天)**
  * 此應用程式在 1 天內允許的 CPU 總量。 此配額會每隔 24 小時在午夜 (UTC) 重設一次。
* **記憶體**
  * 此應用程式允許的記憶體總量。
* **頻寬**
  * 此應用程式在 1 天內允許的連出頻寬總量。
    此配額會每隔 24 小時在午夜 (UTC) 重設一次。
* **Filesystem**
  * 允許的儲存體總量。

hello 只配額適用 tooapps 裝載於**基本**，**標準**和**Premium**計劃是**Filesystem**。

Hello 特定配額、 限制和 hello 不同的應用程式服務 Sku 的可用功能的詳細資訊可以在這裡找到： [Azure 訂用帳戶服務限制](../azure-subscription-service-limits.md#app-service-limits)

#### <a name="quota-enforcement"></a>強制配額
如果其使用方式中的應用程式超過 hello **CPU （短整數）**， **CPU （天）**，或**頻寬**配額則 hello 應用程式將會停止，直到 hello 配額重新設定。 在此期間，所有連入要求都會導致 **HTTP 403**。
![][http403]

如果應用程式的 hello**記憶體**超過配額時，則 hello 應用程式會重新啟動。

如果 hello **Filesystem**超過配額時，則任何寫入作業將會失敗，這包括寫入 toologs。

升級您的 App Service 方案，即可在應用程式中增加或移除配額。

### <a name="metrics"></a>度量
**度量**提供 hello 應用程式或應用程式服務方案行為的相關資訊。

如**應用程式**，hello 可用度量：

* **平均回應時間**
  * hello 毫秒 hello 應用程式 tooserve 要求所花費的平均時間。
* **平均記憶體工作集**
  * hello 平均量中 Mib hello 應用程式所使用的記憶體。
* **CPU 時間**
  * hello CPU 數量 hello 應用程式所耗用的秒數。 如需此計量的詳細資訊，請參閱︰[CPU 時間與 CPU 百分比](#cpu-time-vs-cpu-percentage)
* **資料輸入**
  * hello hello Mib 中的應用程式所使用的連入頻寬量。
* **資料輸出**
  * hello hello Mib 中的應用程式所使用的連出頻寬量。
* **Http 2xx**
  * 導致 http 狀態碼 >= 200 但 < 300 的要求計數。
* **Http 3xx**
  * 導致 http 狀態碼 >= 300 但 < 400 的要求計數。
* **Http 401**
  * 導致 HTTP 401 狀態碼的要求計數。
* **Http 403**
  * 導致 HTTP 403 狀態碼的要求計數。
* **Http 404**
  * 導致 HTTP 404 狀態碼的要求計數。
* **Http 406**
  * 導致 HTTP 406 狀態碼的要求計數。
* **Http 4xx**
  * 導致 http 狀態碼 >= 400 但 < 500 的要求計數。
* **Http 伺服器錯誤**
  * 導致 http 狀態碼 >= 500 但 < 600 的要求計數。
* **記憶體工作集**
  * 目前的 Mib 中的 hello 應用程式所使用的記憶體數量。
* **要求**
  * 要求總數 (不論其導致的 HTTP 狀態碼為何)。

如**App Service 方案**，hello 可用度量：

> [!NOTE]
> App Service 方案計量只適用於**基本**、**標準**和**進階** SKU 中的方案。
> 
> 

* **CPU 百分比**
  * hello 平均 CPU 使用 hello 計劃的所有執行個體。
* **記憶體百分比**
  * hello hello 計劃的所有執行個體之間使用的平均的記憶體。
* **資料輸入**
  * hello 平均跨 hello 計劃的所有執行個體使用的連入頻寬。
* **資料輸出**
  * hello 平均傳出 hello 計劃的所有執行個體所使用的頻寬。
* **磁碟佇列長度**
  * hello 平均數的讀取和寫入要求排入佇列的儲存體上。 高磁碟佇列長度是可能會變慢，因為 tooexcessive 磁碟 I/O 的應用程式的指示。
* **Http 佇列長度**
  * hello 的以前 toosit hello 佇列執行的 HTTP 要求的平均數目。 HTTP 佇列長度很大或不斷增加是方案負載過重的徵兆。

### <a name="cpu-time-vs-cpu-percentage"></a>CPU 時間與 CPU 百分比
<!-- toodo: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

有 2 個計量可反映 CPU 使用量。 **CPU 時間**與 **CPU 百分比**

**CPU 時間**很有用的應用程式裝載於**免費**或**共用**計劃，因為其配額的其中一個定義在 hello 應用程式所使用的 CPU 分鐘。

**CPU 百分比**上 hello 另一方面是有用的應用程式裝載於**基本**，**標準**和**premium**計劃，因為它們可以向外延展和此標準就代表 hello 的所有執行個體的整體使用狀況。

## <a name="metrics-granularity-and-retention-policy"></a>計量資料粒度和保留原則
記錄和彙總以 hello hello 服務應用程式和應用程式服務方案的度量資料粒度和保留原則：

* **分鐘**資料粒度度量會保留 **48 小時**
* **小時**資料粒度度量會保留 **30 天**
* **天**資料粒度度量會保留 **90 天**

## <a name="monitoring-quotas-and-metrics-in-hello-azure-portal"></a>Hello Azure 入口網站中的監視配額和計量。
您可以檢閱 hello hello 不同狀態**配額**和**度量**影響的應用程式在 hello [Azure 入口網站](https://portal.azure.com)。

在 [設定] > **配額** 之下可以找到 ![][quotas]
**配額**。 hello UX 可讓您檢閱: （1) hello 配額名稱、 （2） 重設的間隔、 （3） 其目前的限制和 （4） 目前的值。

![][metrics]
**度量**可以直接從 hello 資源刀鋒視窗存取。 您也可以自訂的 hello 圖表: （1)**按一下**它，然後選取 (2)**編輯圖表**。
從這裡您可以變更 hello (3)**時間範圍**、 (4)**圖表類型**，和 (5)**度量**toodisplay。  

您可以在此進一步了解計量︰[監視服務計量](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)。

## <a name="alerts-and-autoscale"></a>警示和自動調整
度量的應用程式或應用程式服務計劃可以接到 tooalerts，toolearn 程式的詳細資訊，請參閱[接收警示通知](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

基本、標準或進階 App Service 方案中裝載的 App Service 應用程式支援 **自動調整**。 這可讓您監視 App Service 方案計量，可以增加或減少 hello 視需要提供其他資源的執行個體計數的 tooconfigure 規則或儲存 money hello 應用程式時過度佈建。 您可以進一步了解自動調整規模：[如何 tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md)和這裡[Azure 監視的自動調整的最佳做法](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
