---
title: "aaaAzure 訂用帳戶限制和配額 |Microsoft 文件"
description: "提供通用的 Azure 訂用帳戶和服務限制、配額和條件約束的清單。 這包括 tooincrease 如何限制以及最大值的詳細資訊。"
services: 
documentationcenter: 
author: rothja
manager: jeffreyg
editor: 
tags: billing
ms.assetid: 60d848f9-ff26-496e-a5ec-ccf92ad7d125
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: byvinyal
ms.openlocfilehash: a754d56124520791254ab8f1729808f0750ff222
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-service-limits-quotas-and-constraints"></a>Azure 訂用帳戶和服務限制、配額與限制
本文列出一些 hello 最常見 Microsoft Azure 的限制，有時也稱為配額。 本文件目前未涵蓋所有 Azure 服務。 經過一段時間，hello 清單將會展開，並更新 hello 平台的更多的 toocover。

請瀏覽[Azure 定價一覽](https://azure.microsoft.com/pricing/)toolearn 深入了解 Azure 定價。 您可以估計成本使用 hello[定價計算機](https://azure.microsoft.com/pricing/calculator/)或透過瀏覽 hello 定價詳細資料頁面的服務 (例如， [Windows Vm](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows))。 提示 toohelp 用於管理您的成本，請參閱[避免非預期的成本，以及 Azure 帳單和成本管理](billing/billing-getting-started.md)。

> [!NOTE]
> 如果您想 tooraise hello 限制或配額上方 hello**預設限制**，[開啟免費線上客戶支援要求](azure-supportability/resource-manager-core-quotas-request.md)。 hello 限制無法引發上方 hello**上限**hello 下表所示的值。 如果沒有任何**上限**資料行，然後 hello 資源不會有可調整的限制。 
> 
> 免費試用訂用帳戶無法增加限制或配額。 如果您有免費的試用版，您可以升級 tooa[隨用隨付](https://azure.microsoft.com/offers/ms-azr-0003p/)訂用帳戶。 如需詳細資訊，請參閱[升級 Azure 免費試用 tooPay-為-您-Go](billing/billing-upgrade-azure-subscription.md)。
> 

## <a name="limits-and-hello-azure-resource-manager"></a>限制和 hello Azure 資源管理員
現在很可能 toocombine tooa 中的多個 Azure 資源的單一 Azure 資源群組。 當使用資源群組，一次是屬於全域的限制會變成管理在 hello Azure 資源管理員使用的地區層級。 如需 Azure 資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](azure-resource-manager/resource-group-overview.md)。

在新的資料表下方的 hello 限制已加入的 tooreflect 限制的任何差異使用 hello Azure 資源管理員時。 例如，有**訂用帳戶限制**資料表和**訂用帳戶限制 - Azure Resource Manager** 資料表。 當限制會套用 tooboth 案例時，它只會顯示 hello 第一個資料表中。 除非另有說明，限制在所有區域中全域適用。

> [!NOTE]
> 它會是重要 tooemphasize 的 Azure 資源群組中的資源配額是每個區域可以存取您的訂閱，並不是每個訂閱，是與 hello 服務管理配額一樣。 讓我們以核心配額為例。 如果您需要的 toorequest 核心支援增加配額，您如何需要 toodecide 許多核心您想要在哪一個區域，toouse，然後讓 Azure 資源群組中的特定要求核心配額為 hello 金額和您想要的區域。 因此，如果您需要 toouse 30 核心西歐 toorun 在您的應用程式那里;您應該特別要求在西歐 30 個核心。 但您不需要任何其他區域中增加核心配額--只西歐將會有 hello 30 核心配額。
> <!-- -->
> 如此一來，您可能會發現決定哪些 Azure 資源群組配額需要 toobe 金額考慮部署到其中的每個區域中任何一個區域，和要求的工作負載的有用 tooconsider。 請參閱 [移難排解部署問題](resource-manager-common-deployment-errors.md) ，以取得探索您特定區域目前的配額的其他說明。
> 
> 

## <a name="service-specific-limits"></a>特定服務的限制
* [Active Directory](#active-directory-limits)
* [API 管理](#api-management-limits)
* [App Service](#app-service-limits)
* [應用程式閘道](#application-gateway-limits)
* [Application Insights](#application-insights-limits)
* [自動化](#automation-limits)
* [Azure Cosmos DB](#azure-cosmos-db-limits)
* [事件格線](#azure-event-grid-limits)
* [Azure Redis 快取](#azure-redis-cache-limits)
* [Azure RemoteApp](#azure-remoteapp-limits)
* [備份](#backup-limits)
* [批次](#batch-limits)
* [BizTalk 服務](#biztalk-services-limits)
* [CDN](#cdn-limits)
* [雲端服務](#cloud-services-limits)
* [Container Instances](#container-instances-limits)
* [Data Factory](#data-factory-limits)
* [Data Lake Analytics](#data-lake-analytics-limits)
* [Data Lake Store](#data-lake-store-limits)
* [DNS](#dns-limits)
* [事件中樞](#event-hubs-limits)
* [IoT 中心](#iot-hub-limits)
* [金鑰保存庫](#key-vault-limits)
* [Log Analytics / Operational Insights](#log-analytics-limits)
* [媒體服務](#media-services-limits)
* [Mobile Engagement](#mobile-engagement-limits)
* [行動服務](#mobile-services-limits)
* [監視](#monitor-limits)
* [Multi-Factor Authentication](#multi-factor-authentication)
* [網路功能](#networking-limits)
* [網路監看員](#network-watcher-limits)
* [通知中樞服務](#notification-hub-service-limits)
* [資源群組](#resource-group-limits)
* [排程器](#scheduler-limits)
* [Search](#search-limits)
* [服務匯流排](#service-bus-limits)
* [站台復原](#site-recovery-limits)
* [SQL Database](#sql-database-limits)
* [儲存體](#storage-limits)
* [StorSimple 系統](#storsimple-system-limits)
* [串流分析](#stream-analytics-limits)
* [訂用帳戶](#subscription-limits)
* [流量管理員](#traffic-manager-limits)
* [虛擬機器](#virtual-machines-limits)
* [虛擬機器擴展集](#virtual-machine-scale-sets-limits)

### <a name="subscription-limits"></a>訂用帳戶限制
#### <a name="subscription-limits"></a>訂用帳戶限制
[!INCLUDE [azure-subscription-limits](../includes/azure-subscription-limits.md)]

#### <a name="subscription-limits---azure-resource-manager"></a>訂用帳戶限制 - Azure Resource Manager
使用 hello Azure 資源管理員和 Azure 資源群組時，就會適用下列限制的 hello。 下面未列出以 hello Azure 資源管理員中未變更的限制。 請這些限制，參閱 toohello 上表。

如需處理限制 Resource Manager 要求的資訊，請參閱[節流 Resource Manager 要求](resource-manager-request-limits.md)。

[!INCLUDE [azure-subscription-limits-azure-resource-manager](../includes/azure-subscription-limits-azure-resource-manager.md)]

### <a name="resource-group-limits"></a>資源群組限制
[!INCLUDE [azure-resource-groups-limits](../includes/azure-resource-groups-limits.md)]

### <a name="virtual-machines-limits"></a>虛擬機器限制
#### <a name="virtual-machine-limits"></a>虛擬機器限制
[!INCLUDE [azure-virtual-machines-limits](../includes/azure-virtual-machines-limits.md)]

#### <a name="virtual-machines-limits---azure-resource-manager"></a>虛擬機器限制 - Azure 資源管理員
使用 hello Azure 資源管理員和 Azure 資源群組時，就會適用下列限制的 hello。 下面未列出以 hello Azure 資源管理員中未變更的限制。 請這些限制，參閱 toohello 上表。

[!INCLUDE [azure-virtual-machines-limits-azure-resource-manager](../includes/azure-virtual-machines-limits-azure-resource-manager.md)]

### <a name="virtual-machine-scale-sets-limits"></a>虛擬機器擴展集限制
[!INCLUDE [virtual-machine-scale-sets-limits](../includes/azure-virtual-machine-scale-sets-limits.md)]

### <a name="container-instances-limits"></a>容器執行個體限制
[!INCLUDE [container-instances-limits](../includes/container-instances-limits.md)]

### <a name="networking-limits"></a>網路限制
[!INCLUDE [expressroute-limits](../includes/expressroute-limits.md)]

#### <a name="networking-limits"></a>網路限制
[!INCLUDE [azure-virtual-network-limits](../includes/azure-virtual-network-limits.md)]

#### <a name="application-gateway-limits"></a>應用程式閘道限制
[!INCLUDE [application-gateway-limits](../includes/application-gateway-limits.md)]

#### <a name="network-watcher-limits"></a>網路監看員限制
[!INCLUDE [network-watcher-limits](../includes/network-watcher-limits.md)]

#### <a name="traffic-manager-limits"></a>流量管理員限制
[!INCLUDE [traffic-manager-limits](../includes/traffic-manager-limits.md)]

#### <a name="dns-limits"></a>DNS 限制
[!INCLUDE [dns-limits](../includes/dns-limits.md)]

### <a name="storage-limits"></a>儲存體限制
如需儲存體帳戶限制的其他詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](storage/common/storage-scalability-targets.md)。
<!--like # storage accts --> 
#### <a name="storage-service-limits"></a>儲存體服務限制
[!INCLUDE [azure-storage-limits](../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
#### <a name="virtual-machine-disk-limits"></a>虛擬機器磁碟限制 
[!INCLUDE [azure-storage-limits-vm-disks](../includes/azure-storage-limits-vm-disks.md)]

如需其他詳細資訊，請參閱 [虛擬機器大小](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 。

#### <a name="managed-virtual-machine-disks"></a>受管理的虛擬機器磁碟

[!INCLUDE [azure-storage-limits-vm-disks-managed](../includes/azure-storage-limits-vm-disks-managed.md)]

#### <a name="unmanaged-virtual-machine-disks"></a>未受管理的虛擬機器磁碟

[!INCLUDE [azure-storage-limits-vm-disks-standard](../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../includes/azure-storage-limits-vm-disks-premium.md)]

#### <a name="storage-resource-provider-limits"></a>儲存體資源提供者限制
[!INCLUDE [azure-storage-limits-azure-resource-manager](../includes/azure-storage-limits-azure-resource-manager.md)]

### <a name="cloud-services-limits"></a>雲端服務限制
[!INCLUDE [azure-cloud-services-limits](../includes/azure-cloud-services-limits.md)]

### <a name="app-service-limits"></a>應用程式服務限制
hello 下列 App Service 的限制包括 Web 應用程式、 行動應用程式、 應用程式開發介面應用程式和邏輯應用程式的限制。

[!INCLUDE [azure-websites-limits](../includes/azure-websites-limits.md)]

### <a name="scheduler-limits"></a>排程器限制
[!INCLUDE [scheduler-limits-table](../includes/scheduler-limits-table.md)]

### <a name="batch-limits"></a>Batch 限制
[!INCLUDE [azure-batch-limits](../includes/azure-batch-limits.md)]

### <a name="biztalk-services-limits"></a>BizTalk 服務限制
hello 下表顯示 hello 限制 Azure Biztalk 服務。

[!INCLUDE [biztalk-services-service-limits](../includes/biztalk-services-service-limits.md)]

### <a name="azure-cosmos-db-limits"></a>Azure Cosmos DB 限制
Azure Cosmos DB 是輸送量與儲存體可以縮放的 toohandle 應用程式所需的任何全域延展資料庫。 如果您有任何疑問 hello Azure Cosmos DB 所提供的小數位數，請傳送電子郵件tooaskcosmosdb@microsoft.com。

### <a name="mobile-engagement-limits"></a>Mobile Engagement 限制
[!INCLUDE [azure-mobile-engagement-limits](../includes/azure-mobile-engagement-limits.md)]

### <a name="search-limits"></a>搜尋限制
定價層會決定 hello 容量限制您的搜尋服務。 層級包括：

*  多租用戶服務，與其他 Azure 訂戶共用，適用於評估及小型開發專案。
* *基本*提供專用的運算資源在規模較小的生產工作負載的高可用性的查詢工作負載的 toothree 複本。
*  適用於較大型生產工作負載。 多個層級存在於 hello 標準層，以便您可以選擇最符合您的工作負載設定檔的資源設定。

**每一訂用帳戶的限制**

[!INCLUDE [azure-search-limits-per-subscription](../includes/azure-search-limits-per-subscription.md)]

**每個搜尋服務的限制**

[!INCLUDE [azure-search-limits-per-service](../includes/azure-search-limits-per-service.md)]

toolearn 進一步了解限制更細微的層級，例如文件大小、 查詢每秒、 金鑰、 要求和回應，請參閱[服務在 Azure 搜尋中的限制](search/search-limits-quotas-capacity.md)。

### <a name="media-services-limits"></a>媒體服務限制
[!INCLUDE [azure-mediaservices-limits](../includes/azure-mediaservices-limits.md)]

### <a name="cdn-limits"></a>CDN 限制
[!INCLUDE [cdn-limits](../includes/cdn-limits.md)]

### <a name="mobile-services-limits"></a>行動服務限制
[!INCLUDE [mobile-services-limits](../includes/mobile-services-limits.md)]

### <a name="monitor-limits"></a>監視限制
[!INCLUDE [monitoring-limits](../includes/monitoring-limits.md)]

### <a name="notification-hub-service-limits"></a>通知中樞服務限制
[!INCLUDE [notification-hub-limits](../includes/notification-hub-limits.md)]

### <a name="event-hubs-limits"></a>事件中樞限制
[!INCLUDE [azure-servicebus-limits](../includes/event-hubs-limits.md)]

### <a name="service-bus-limits"></a>服務匯流排限制
[!INCLUDE [azure-servicebus-limits](../includes/service-bus-quotas-table.md)]

### <a name="iot-hub-limits"></a>IoT 中樞限制
[!INCLUDE [azure-iothub-limits](../includes/iot-hub-limits.md)]

### <a name="data-factory-limits"></a>Data Factory 限制
[!INCLUDE [azure-data-factory-limits](../includes/azure-data-factory-limits.md)]

### <a name="data-lake-analytics-limits"></a>Data Lake Analytics 限制
[!INCLUDE [azure-data-lake-analytics-limits](../includes/azure-data-lake-analytics-limits.md)]

### <a name="data-lake-store-limits"></a>Data Lake Store 限制
[!INCLUDE [azure-data-lake-store-limits](../includes/azure-data-lake-store-limits.md)]

### <a name="stream-analytics-limits"></a>串流分析限制
[!INCLUDE [stream-analytics-limits-table](../includes/stream-analytics-limits-table.md)]

### <a name="active-directory-limits"></a>Active Directory 限制
[!INCLUDE [AAD-service-limits](../includes/active-directory-service-limits-include.md)]

### <a name="azure-event-grid-limits"></a>Azure Event Grid 限制
[!INCLUDE [event-grid-limits](../includes/event-grid-limits.md)]

### <a name="azure-remoteapp-limits"></a>Azure RemoteApp 限制
[!INCLUDE [azure-remoteapp-limits](../includes/azure-remoteapp-limits.md)]

### <a name="storsimple-system-limits"></a>StorSimple 系統限制
[!INCLUDE [storsimple-limits-table](../includes/storsimple-limits-table.md)]

### <a name="log-analytics-limits"></a>Log Analytics 限制
[!INCLUDE [operational-insights-limits](../includes/operational-insights-limits.md)]

### <a name="backup-limits"></a>備份限制
[!INCLUDE [azure-backup-limits](../includes/azure-backup-limits.md)]

### <a name="site-recovery-limits"></a>Site Recovery 限制
[!INCLUDE [site-recovery-limits](../includes/site-recovery-limits.md)]

### <a name="application-insights-limits"></a>Application Insights 限制
[!INCLUDE [application-insights-limits](../includes/application-insights-limits.md)]

### <a name="api-management-limits"></a>API 管理限制
[!INCLUDE [api-management-service-limits](../includes/api-management-service-limits.md)]

### <a name="azure-redis-cache-limits"></a>Azure Redis 快取限制
[!INCLUDE [redis-cache-service-limits](../includes/redis-cache-service-limits.md)]

### <a name="key-vault-limits"></a>金鑰保存庫限制
[!INCLUDE [key-vault-limits](../includes/key-vault-limits.md)]

### <a name="multi-factor-authentication"></a>Multi-Factor Authentication
[!INCLUDE [azure-mfa-service-limits](../includes/azure-mfa-service-limits.md)]

### <a name="automation-limits"></a>自動化限制
[!INCLUDE [automation-limits](../includes/azure-automation-service-limits.md)]

### <a name="sql-database-limits"></a>SQL Database 限制
如需 SQL Database 的限制，請參閱 [SQL Database 資源限制](sql-database/sql-database-resource-limits.md)。

## <a name="see-also"></a>另請參閱
[了解 Azure 限制和增加](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)

[Azure 的虛擬機器和雲端服務大小](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[雲端服務的大小](cloud-services/cloud-services-sizes-specs.md)

