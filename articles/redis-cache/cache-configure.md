---
title: "aaaHow tooconfigure Azure Redis 快取 |Microsoft 文件"
description: "了解 hello Azure Redis 快取的預設 Redis 組態，並了解如何 tooconfigure Azure Redis 快取執行個體"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: d0bf2e1f-6a26-4e62-85ba-d82b35fc5aa6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 08/22/2017
ms.author: sdanie
ms.openlocfilehash: 46bffb74cdf40e0e0a99c3a83dbe06d6fe1ea65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-azure-redis-cache"></a>如何 tooconfigure Azure Redis 快取
本主題描述如何 tooreview 和 update hello 設定您的 Azure Redis 快取執行個體，並涵蓋 hello 預設 Redis 伺服器設定 Azure Redis 快取執行個體。

> [!NOTE]
> 如需有關設定和使用 premium 快取功能的詳細資訊，請參閱[如何 tooconfigure 持續性](cache-how-to-premium-persistence.md)，[如何叢集 tooconfigure](cache-how-to-premium-clustering.md)，和[如何 tooconfigure 虛擬網路支援](cache-how-to-premium-vnet.md).
> 
> 

## <a name="configure-redis-cache-settings"></a>設定 Redis 快取設定
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

Azure Redis 快取設定會檢視和設定上 hello **Redis 快取**刀鋒視窗中使用 hello**資源功能表**。

![Redis 快取設定](./media/cache-configure/redis-cache-settings.png)

您可以檢視並設定下列設定使用 hello hello**資源功能表**。

* [概觀](#overview)
* [活動記錄檔](#activity-log)
* [存取控制 (IAM)](#access-control-iam)
* [標記](#tags)
* [診斷並解決問題](#diagnose-and-solve-problems)
* [設定](#settings)
    * [存取金鑰](#access-keys)
    * [進階設定](#advanced-settings)
    * [Redis 快取顧問](#redis-cache-advisor)
    * [調整](#scale)
    * [Redis 叢集大小](#cluster-size)
    * [Redis 資料永續性](#redis-data-persistence)
    * [排程更新](#schedule-updates)
    * [異地複寫](#geo-replication)
    * [虛擬網路](#virtual-network)
    * [防火牆](#firewall)
    * [屬性](#properties)
    * [鎖定](#locks)
    * [自動化指令碼](#automation-script)
* [系統管理](#administration)
    * [匯入資料](#importexport)
    * [匯出資料](#importexport)
    * [重新啟動](#reboot)
* [監視](#monitoring)
    * [Redis 度量](#redis-metrics)
    * [警示規則](#alert-rules)
    * [診斷](#diagnostics)
* [支援和疑難排解設定](#support-amp-troubleshooting-settings)
    * [資源健康情況](#resource-health)
    * [新的支援要求](#new-support-request)


## <a name="overview"></a>概觀

**概觀**提供您快取的基本資訊，例如名稱、連接埠、定價層，以及選取的快取度量。

### <a name="activity-log"></a>活動記錄檔

按一下**活動記錄檔**tooview 動作對您的快取。 您也可以使用篩選 tooexpand 此檢視 tooinclude 其他資源。 如需使用稽核記錄的詳細資訊，請參閱[使用 Resource Manager 來稽核作業](../azure-resource-manager/resource-group-audit.md)。 如需有關監視 Azure Redis 快取事件的詳細資訊，請參閱 [作業和警示](cache-how-to-monitor.md#operations-and-alerts)。

### <a name="access-control-iam"></a>存取控制 (IAM)

hello**存取控制 (IAM)** > 一節提供角色型存取控制 (RBAC) 的支援 hello Azure 入口網站 toohelp 組織符合其存取管理需求簡單和精確地。 如需詳細資訊，請參閱[hello Azure 入口網站中的角色型存取控制](../active-directory/role-based-access-control-configure.md)。

### <a name="tags"></a>標記

hello**標記**一節可協助您組織資源。 如需詳細資訊，請參閱[使用標記 tooorganize 您的 Azure 資源](../azure-resource-manager/resource-group-using-tags.md)。


### <a name="diagnose-and-solve-problems"></a>診斷並解決問題

按一下**診斷並解決問題**toobe 提供解決一般問題和策略。



## <a name="settings"></a>設定
hello**設定**區段可讓您 tooaccess，並設定下列設定您的快取的 hello。

* [存取金鑰](#access-keys)
* [進階設定](#advanced-settings)
* [Redis 快取顧問](#redis-cache-advisor)
* [調整](#scale)
* [Redis 叢集大小](#cluster-size)
* [Redis 資料永續性](#redis-data-persistence)
* [排程更新](#schedule-updates)
* [異地複寫](#geo-replication)
* [虛擬網路](#virtual-network)
* [防火牆](#firewall)
* [屬性](#properties)
* [鎖定](#locks)
* [自動化指令碼](#automation-script)



### <a name="access-keys"></a>存取金鑰
按一下**存取金鑰**tooview 或重新建立 hello 存取您的快取的索引鍵。 Hello 連接 tooyour 快取的用戶端會使用這些金鑰。

![Redis 快取存取金鑰](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a>進階設定
hello 下列設定會在 hello**進階設定**刀鋒視窗。

* [存取連接埠](#access-ports)
* [記憶體原則](#memory-policies)
* [Keyspace 通知 (進階設定)](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a>存取連接埠
根據預設，新的快取會停用非 SSL 存取。 tooenable hello 非 SSL 連接埠，按一下 **否**如**允許存取僅限透過 SSL**上 hello**進階設定**刀鋒視窗，然後按一下**儲存**。

![Redis 快取存取連接埠](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a>記憶體原則
hello **Maxmemory 原則**， **maxmemory 保留**，和**maxfragmentationmemory 保留**hello 上的設定**進階設定**刀鋒視窗中設定 hello 快取的 hello 記憶體原則。

![Redis 快取 Maxmemory 原則](./media/cache-configure/redis-cache-maxmemory-policy.png)

**Maxmemory 原則**設定 hello hello 快取的收回原則，並可讓您從下列收回原則 hello toochoose:

* `volatile-lru`-這是 hello 預設值。
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

如需 `maxmemory` 原則的詳細資訊，請參閱[收回原則](http://redis.io/topics/lru-cache#eviction-policies)。

hello **maxmemory 保留**設定會設定為非快取作業，例如複寫容錯移轉期間保留 （mb） 的 hello 的記憶體數量。 設定此值可讓您更一致的 Redis 伺服器經驗 toohave 時您的負載而改變。 對於頻繁寫入的工作負載，此值應該設定為更高的值。 當記憶體保留給這類作業時，無法用於儲存快取的資料。

hello **maxfragmentationmemory 保留**設定會設定 hello 的記憶體數量 （mb） 是保留的記憶體分散程度 tooaccommodate。 設定此值可讓您更一致的 Redis 伺服器經驗 toohave hello 快取已滿，或關閉 toofull 和 hello 片段比率很高時。 當記憶體保留給這類作業時，無法用於儲存快取的資料。

選擇新的記憶體保留項目值的一件事 tooconsider (**maxmemory 保留**或**maxfragmentationmemory 保留**) 是這項變更可能會如何影響已在執行與快取大量的資料。 比方說，如果您有 53 GB 快取與 49 GB 的資料，則變更 hello 保留項目值 too8 GB，這將會卸除 hello 最大的可用記憶體 hello 系統關閉 too45 GB。 如果您目前`used_memory`或`used_memory_rss`值高於 hello 新限制 45 gb，則 hello 系統將等到有 tooevict 資料`used_memory`和`used_memory_rss`低於 45 GB。 收回會增加伺服器負載並讓記憶體過於分散。 如需快取計量的詳細資訊，例如 `used_memory` 和 `used_memory_rss`，請參閱[可用計量和報告間隔](cache-how-to-monitor.md#available-metrics-and-reporting-intervals)。

> [!IMPORTANT]
> hello **maxmemory 保留**和**maxfragmentationmemory 保留**設定只適用於 Standard 和 Premium 快取。
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a>Keyspace 通知 (進階設定)
Redis 的 keyspace 通知設定 hello**進階設定**刀鋒視窗。 Keyspace 通知發生特定事件時，允許用戶端 tooreceive 通知。

![Redis 快取進階設定](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> Keyspace 通知和 hello**通知 keyspace 事件**設定只適用於標準和進階版快取。
> 
> 

如需詳細資訊，請參閱 [Redis Keyspace 通知](http://redis.io/topics/notifications)(英文)。 範例程式碼，請參閱 hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs)檔案在 hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld)範例。


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a>Redis 快取顧問
hello **Redis 快取 Advisor**刀鋒視窗會顯示您的快取的建議。 在一般作業期間，不會顯示任何建議。 

![建議](./media/cache-configure/redis-cache-no-recommendations.png)

如果您的快取，例如高記憶體使用量、 網路頻寬或伺服器負載 hello 作業過程中發生任何條件，警示會顯示在 hello **Redis 快取**刀鋒視窗。

![建議](./media/cache-configure/redis-cache-recommendations-alert.png)

可以在 hello 上找到的進一步資訊**建議**刀鋒視窗。

![建議](./media/cache-configure/redis-cache-recommendations.png)

您可以監視這些度量在 hello[監控圖表](cache-how-to-monitor.md#monitoring-charts)和[使用量圖表](cache-how-to-monitor.md#usage-charts)區段 hello **Redis 快取**刀鋒視窗。

每個定價層都有不同的用戶端連線、記憶體和頻寬的限制。 如果您的快取持續一段時間接近這些計量的最大容量，即會提供建議。 如需有關 hello 度量和限制的 hello 檢閱**建議**工具，請參閱下表中的 hello:

| Redis 快取計量 | 詳細資訊 |
| --- | --- |
| 網路頻寬使用量 |[快取效能 - 可用的頻寬](cache-faq.md#cache-performance) |
| 連線的用戶端 |[預設 Redis 伺服器組態 - maxclients](#maxclients) |
| 伺服器負載 |[使用量圖表 - Redis 伺服器負載](cache-how-to-monitor.md#usage-charts) |
| 記憶體使用量 |[快取效能 - 大小](cache-faq.md#cache-performance) |

tooupgrade 快取中，按一下 **立即升級**toochange hello 定價層和[標尺](#scale)您的快取。 如需選擇定價層的詳細資訊，請參閱 [應該使用哪個 Redis 快取供應項目和大小？](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)


### <a name="scale"></a>調整
按一下**標尺**tooview 或變更定價層快取的 hello。 如需有關調整的詳細資訊，請參閱[如何 tooScale Azure Redis 快取](cache-how-to-scale.md)。

![Redis 快取定價層](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a>Redis 叢集大小
按一下**（預覽） Redis 叢集大小**toochange hello 叢集大小執行進階版快取叢集啟用。

> [!NOTE]
> 請注意，雖然 hello Azure Redis 快取進階層已被釋放 tooGeneral 可用性 hello Redis 叢集大小功能目前為預覽狀態。
> 
> 

![Redis 叢集大小](./media/cache-configure/redis-cache-redis-cluster-size.png)

toochange hello 叢集大小，使用 hello 滑桿，或輸入介於 1 到 10 之間的數字 hello**分區計數**文字方塊中，然後按一下**確定**toosave。

> [!IMPORTANT]
> Redis 叢集只適用於進階快取。 如需詳細資訊，請參閱[如何 tooconfigure Premium Azure Redis 快取叢集](cache-how-to-premium-clustering.md)。
> 
> 


### <a name="redis-data-persistence"></a>Redis 資料永續性
按一下**Redis 資料持續性**tooenable，停用或設定您的進階版快取的資料持續性。 Azure Redis 快取使用 [RDB 持續性](cache-how-to-premium-persistence.md#configure-rdb-persistence)或 [AOF 持續性](cache-how-to-premium-persistence.md#configure-aof-persistence)來提供 Redis 持續性。

如需詳細資訊，請參閱[如何 tooconfigure Premium Azure Redis 快取的持續性](cache-how-to-premium-persistence.md)。


> [!IMPORTANT]
> Redis 資料持續性僅適用於進階快取。 
> 
> 

### <a name="schedule-updates"></a>更新排程
hello**更新排程**刀鋒視窗可讓您 toodesignate Redis 快取的伺服器更新的維護視窗。 

> [!IMPORTANT]
> hello 維護視窗適用於僅 tooRedis 伺服器更新，並不 tooany Azure 更新或更新 toohello 作業系統 hello vm 的主機 hello 快取。
> 
> 

![更新排程](./media/cache-configure/redis-schedule-updates.png)

toospecify 維護視窗中，檢查所需的 hello 天 hello 維護視窗開始時間的每一天，並指定按一下**確定**。 請注意，hello 維護視窗時間-utc 時區。 

> [!IMPORTANT]
> hello**更新排程**功能只適用於 Premium 層快取。 如需詳細資訊和指示，請參閱 [Azure Redis 快取管理 - 排程更新](cache-administration.md#schedule-updates)。
> 
> 

### <a name="geo-replication"></a>異地複寫

hello**地理複寫**刀鋒視窗中提供一個機制，連結兩個 Premium 層 Azure Redis 快取執行個體。 一個快取指定為 hello 主要的連線快取，而 hello hello 次要連結快取為其他。 hello 次要連結快取會變成唯讀的並寫入的 toohello 主要快取的資料複寫 toohello 次要連結快取。 這項功能可以跨 Azure 區域是使用的 tooreplicate 快取。

> [!IMPORTANT]
> **異地複寫**僅適用於進階層快取。 如需詳細資訊和指示，請參閱[如何 Azure Redis 快取的地理複寫 tooconfigure](cache-how-to-geo-replication.md)。
> 
> 

### <a name="virtual-network"></a>虛擬網路
hello**虛擬網路**區段可讓您快取 tooconfigure hello 虛擬網路設定。 如需有關使用 VNET 中建立進階版快取資訊支援，並更新其設定，請參閱[如何 tooconfigure 虛擬網路支援 Premium Azure Redis 快取](cache-how-to-premium-vnet.md)。

> [!IMPORTANT]
> 虛擬網路設定只適用於快取建立期間利用 VNET 支援設定的進階快取。 
> 
> 

### <a name="firewall"></a>防火牆

按一下**防火牆**tooview 和 Premium Azure Redis 快取設定防火牆規則。

![防火牆](./media/cache-configure/redis-firewall-rules.png)

您可以利用開始和結束 IP 位址範圍來指定防火牆規則。 防火牆規則設定時，只有 hello 來自用戶端連線會指定 IP 位址範圍可以連接 toohello 快取。 儲存防火牆規則時是短暫的延遲 hello 規則之前有效。 此延遲通常不超過一分鐘。

> [!IMPORTANT]
> 一律允許來自 Azure Redis 快取監視系統的連線，即使設定了防火牆規則也一樣。
> 
> 防火牆規則僅適用於進階層快取。
> 
> 

### <a name="properties"></a>屬性
按一下**屬性**tooview 快取，包括 hello 快取端點及連接埠相關的資訊。

![Redis 快取屬性](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a>鎖定
hello**鎖定**區段可讓您 toolock 訂用帳戶、 資源群組或資源 tooprevent 不小心刪除或修改重要的資源組織中其他使用者。 如需詳細資訊，請參閱[使用 Azure Resource Manager 來鎖定資源](../azure-resource-manager/resource-group-lock-resources.md)。

### <a name="automation-script"></a>自動化指令碼

按一下**自動化指令碼**toobuild 和匯出範本，未來的部署。 您已部署的資源。 如需使用範本的詳細資訊，請參閱 [使用 Azure Resource Manager 範本部署資源](../azure-resource-manager/resource-group-template-deploy.md)。

## <a name="administration-settings"></a>管理設定
hello hello 中的設定**管理**區段可讓您 tooperform hello 下列快取的系統管理工作。 

![系統管理](./media/cache-configure/redis-cache-administration.png)

* [匯入資料](#importexport)
* [匯出資料](#importexport)
* [重新啟動](#reboot)


### <a name="importexport"></a>匯入/匯出
匯入/匯出是可讓您所匯入和匯出 Redis 快取資料庫 (RDB) 快照集 premium 快取 tooa 分頁 blob 中的 Azure 儲存體帳戶中的 hello 快取中的 tooimport 和匯出資料的 Azure Redis 快取資料管理作業。 匯入/匯出可讓您 toomigrate 不同的 Azure Redis 快取執行個體之間，或填入 hello 快取，以使用之前的資料。

匯入可為使用的 toobring Redis 相容 RDB 檔案從任何執行中的任何雲端或環境，包括 Linux、 Windows 或任何雲端提供者，例如 Amazon Web Services 等項目上執行的 Redis 的 Redis 伺服器。 匯入資料是簡單的方式 toocreate 預先填入資料的快取。 在 hello 匯入過程中，Azure Redis 快取 Azure 儲存體中的 hello RDB 檔案載入記憶體，並再插入 hello 快取中的 hello 索引鍵。

匯出可讓您 tooexport hello 資料儲存在 Azure Redis 快取 tooRedis 相容 RDB 檔案。 您可以使用此功能 toomove 資料從一個 Azure Redis 快取執行個體 tooanother 或 tooanother Redis 伺服器。 在 hello 匯出程序，hello VM 的主機 hello Azure Redis 快取伺服器執行個體，而且 hello 檔案上傳的 toohello 指定儲存體帳戶上建立暫存檔。 Hello 匯出作業完成時為其中一個狀態為成功或失敗，則會刪除 hello 暫存檔案。

> [!IMPORTANT]
> 匯入/匯出僅供進階層快取使用。 如需詳細資訊和指示，請參閱 [在 Azure Redis 快取中匯入與匯出資料](cache-how-to-import-export-data.md)。
> 
> 

### <a name="reboot"></a>重新啟動
hello**重新開機**刀鋒視窗可讓您的快取 tooreboot hello 節點。 這個重新開機功能可讓您 tootest 提供恢復功能的應用程式的快取節點失敗時。

![重新啟動](./media/cache-configure/redis-cache-reboot.png)

如果您有進階版快取以啟用叢集時，您可以選取 hello 快取 tooreboot 哪一個的分區。

![重新啟動](./media/cache-configure/redis-cache-reboot-cluster.png)

tooreboot 一或多個節點的快取中，選取所需的 hello 節點，然後按一下 **重新開機**。 如果您有進階版快取之啟用叢集時，選取 hello 分區 tooreboot，然後按一下**重新開機**。 後幾分鐘的時間，hello 選取的節點重新開機，且上線幾分鐘後。

> [!IMPORTANT]
> 重新啟動現在適用於所有定價層。 如需詳細資訊和指示，請參閱 [Azure Redis Cache administration - Reboot (Azure Redis 快取管理 - 重新啟動)](cache-administration.md#reboot)。
> 
> 


## <a name="monitoring"></a>監視

hello**監視**區段可讓您 tooconfigure 診斷和監視 Redis 快取。 如需有關 Azure Redis 快取監視和診斷的詳細資訊，請參閱[如何 toomonitor Azure Redis 快取](cache-how-to-monitor.md)。

![診斷](./media/cache-configure/redis-cache-diagnostics.png)

* [Redis 度量](#redis-metrics)
* [警示規則](#alert-rules)
* [診斷](#diagnostics)

### <a name="redis-metrics"></a>Redis 度量
按一下**Redis 度量**太[檢視度量](cache-how-to-monitor.md#view-cache-metrics)快取。

### <a name="alert-rules"></a>警示規則

按一下**警示規則**tooconfigure 警示根據 Redis 快取度量。 如需詳細資訊，請參閱[警示](cache-how-to-monitor.md#alerts)。

### <a name="diagnostics"></a>診斷

根據預設，Azure 監視器中的快取計量會[儲存 30 天](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive)，而後刪除。 您的快取度量的時間超過 30 天內，按一下 toopersist**診斷**太[設定 hello 儲存體帳戶](cache-how-to-monitor.md#export-cache-metrics)用 toostore 快取診斷。

>[!NOTE]
>在加法 tooarchiving 您快取度量 toostorage，您也可以[它們進行串流處理 tooan 事件中心，或將它們傳送 tooLog 分析](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics)。
>
>

## <a name="support--troubleshooting-settings"></a>支援和疑難排解設定
hello hello 中的設定**支援 + 疑難排解**> 一節提供您選項來解決您的快取的問題。

![支援 + 疑難排解](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [資源健康情況](#resource-health)
* [新的支援要求](#new-support-request)

### <a name="resource-health"></a>資源健康情況
**資源健康狀態** 會監看您的資源，並告知您資源是否正如預期般執行。 如需 hello Azure 資源健全狀況服務的詳細資訊，請參閱[Azure 資源健全狀況概觀](../resource-health/resource-health-overview.md)。

> [!NOTE]
> 資源健全狀況是目前無法 tooreport hello 的虛擬網路中託管的 Azure Redis 快取執行個體的健全狀況。 如需詳細資訊，請參閱 [將快取裝載於 VNET 時，所有快取功能都可以正常運作嗎？](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)
> 
> 

### <a name="new-support-request"></a>新增支援要求
按一下**新增支援要求**tooopen 您的快取的支援要求。





## <a name="default-redis-server-configuration"></a>預設 Redis 伺服器組態
Hello 下列預設的 Redis 組態值來設定新的 Azure Redis 快取執行個體。

> [!NOTE]
> 本節中的 hello 設定無法使用 hello 變更`StackExchange.Redis.IServer.ConfigSet`方法。 如果一本章節中的 hello 命令呼叫此方法時，會擲回的例外狀況類似 toohello 下列：  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> 任何值，可加以設定，例如**最大記憶體原則**，可透過 hello Azure 入口網站或 Azure CLI 或 PowerShell 之類的命令列管理工具。
> 
> 

| 設定 | 預設值 | 說明 |
| --- | --- | --- |
| `databases` |16 |資料庫的 hello 預設數目為 16，但您可以設定定價層不同數字根據的 hello。<sup>1</sup> hello 預設資料庫為 DB 0，則可以選取每個連線使用不同的`connection.GetDatabase(dbid)`其中`dbid`是之間的數字`0`和`databases - 1`。 |
| `maxclients` |取決於定價層的 hello<sup>2</sup> |這是 hello 允許在 hello 相同連接的用戶端數目最大時間。 一旦達到 hello 限制 Redis 會關閉所有 hello 新的連接，傳回 '的用戶端達到的最大數目' 錯誤。 |
| `maxmemory-policy` |`volatile-lru` |Maxmemory 原則是 hello 設定 Redis 如何選取哪些 tooremove 時`maxmemory`為止 （hello 供應項目建立 hello 快取時選取的快取中的 hello 大小）。 Azure Redis 快取 hello 預設值是設定`volatile-lru`，以移除具有以 LRU 演算法設定到期日的 hello 索引鍵。 可以在 hello Azure 入口網站中設定此設定。 如需詳細資訊，請參閱[記憶體原則](#memory-policies)。 |
| `maxmemory-samples` |3 |toosave 記憶體、 LRU 和 minimal TTL 演算法是近似的演算法，而不是精確的演算法。 根據預設 Redis 檢查三個索引鍵和取用 hello 其中一個較不最近已使用。 |
| `lua-time-limit` |5,000 |Lua 指令碼的最大執行時間 (以毫秒為單位)。 如果已到達最大執行時間 hello，Redis 會記錄的指令碼仍在執行之後 hello 最大允許的時間，以及啟動 tooreply tooqueries 並產生錯誤。 |
| `lua-event-limit` |500 |指令碼事件佇列的大小上限。 |
| `client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub` |0 0 032mb 8mb 60 |hello 用戶端輸出緩衝區限制可使用 tooforce 中斷連線的用戶端完全不讀取資料從 hello 伺服器速度夠快，基於某些原因 （常見的原因是 Pub/Sub 用戶端無法以最快速度 hello 發行者產生它們取用訊息）。 如需詳細資訊，請參閱 [http://redis.io/topics/clients](http://redis.io/topics/clients)。 |

<a name="databases"></a>
<sup>1</sup>hello 限制`databases`每個 Azure Redis 快取定價層不同，且可以在建立快取設定。 如果沒有`databases`設定指定快取建立期間 hello 預設值為 16。

* 基本和標準的快取
  * C0 250 MB 的快取-too16 資料庫
  * C1 1 GB 快取-too16 資料庫
  * C2 2.5 GB 的快取-too16 資料庫
  * C3 6 GB 的快取-too16 資料庫
  * C4 13 GB 快取-too32 資料庫
  * C5 (26 GB) 的快取-too48 資料庫
  * C6 (53 GB) 的快取-too64 資料庫
* 進階快取
  * P1 (6 GB-60 GB)-too16 資料庫
  * P2 (13 GB-130 GB)-too32 資料庫
  * P3 (26 GB-260 GB)-too48 資料庫
  * P4 53 GB-530 GB-too64 資料庫
  * 啟用-Redis 叢集的所有進階版快取 Redis 都叢集的支援使用資料庫 0 因此 hello`databases`限制與 Redis 都叢集啟用任何進階版快取有效地為 1，而 hello[選取](http://redis.io/commands/select)不允許的命令。 如需詳細資訊，請參閱[需要 toomake 叢集任何變更 toomy 用戶端應用程式 toouse 嗎？](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)

如需資料庫的詳細資訊，請參閱[什麼是 Redis 資料庫？](cache-faq.md#what-are-redis-databases)

> [!NOTE]
> hello`databases`設定可設定只有在快取建立期間，而且只使用 PowerShell、 CLI 或其他管理用戶端。 如需在快取建立期間使用 PowerShell 設定 `databases` 的範例，請參閱 [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases)。
> 
> 

<a name="maxclients"></a>
<sup>2</sup>適用於每個 Azure Redis 快取定價層的 `maxclients` 皆不相同。

* 基本和標準的快取
  * C0 250 MB 的快取-too256 連線
  * C1 1 GB 快取-too1 向上、 000 連線
  * C2 2.5 GB 的快取-too2 向上、 000 連線
  * C3 6 GB 的快取-too5 向上、 000 連線
  * C4 13 GB 快取-too10 向上、 000 連線
  * C5 (26 GB) 的快取-too15 向上、 000 連線
  * C6 (53 GB) 的快取-too20 向上、 000 連線
* 進階快取
  * P1 (6 GB-60 GB)-向上 too7，500 的連線
  * P2 (13 GB-130 GB)-too15，000 連線設定
  * P3 (26 GB-260 GB)-too30，000 連線設定
  * P4 53 GB-530 GB-too40，000 連線設定

> [!NOTE]
> 每個快取的大小可讓*最多*特定數目的連線，每個連線 tooRedis 具有額外負荷與其相關聯。 因 TLS/SSL 加密而產生的 CPU 與記憶體使用量即是這類額外負荷的其中一例。 指定快取大小的 hello 最大連線限制假設輕度載入的快取。 如果從連接的額外負荷載入*加上*從用戶端作業的負載超過容量的 hello 系統、 hello 快取可以體驗容量問題，即使您未超過 hello 目前快取大小的 hello 連線限制。
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a>Azure Redis 快取中不支援的 Redis 命令
> [!IMPORTANT]
> 設定和管理 Azure Redis 快取執行個體由 Microsoft 管理的因為 hello 下列命令會停用。 如果您嘗試 tooinvoke 它們，您會收到類似的錯誤訊息太`"(error) ERR unknown command"`。
> 
> * BGREWRITEAOF
> * BGSAVE
> * CONFIG
> * DEBUG
> * MIGRATE
> * SAVE
> * SHUTDOWN
> * SLAVEOF
> * CLUSTER - 叢集寫入命令已停用，但允許唯讀的叢集命令。
> 
> 

如需 Redis 命令的詳細資訊，請參閱 [http://redis.io/commands](http://redis.io/commands)。

## <a name="redis-console"></a>Redis 主控台
您可以安全地發出命令使用 hello tooyour Azure Redis 快取執行個體**Redis 主控台**，此功能在 hello Azure 入口網站的所有快取層。

> [!IMPORTANT]
> - hello Redis 主控台不適用於[VNET](cache-how-to-premium-vnet.md)。 當您的快取是 VNET 的一部分時，hello VNET 中的用戶端可以存取 hello 快取。 Redis 主控台在超出範圍 hello VNET，您本機瀏覽器中執行，因為它無法連線 tooyour 快取。
> - Azure Redis 快取並未支援所有的 Redis 命令。 Azure Redis 快取已停用 Redis 命令的清單，請參閱先前的 hello [Redis 命令不支援在 Azure Redis 快取](#redis-commands-not-supported-in-azure-redis-cache)> 一節。 如需 Redis 命令的詳細資訊，請參閱 [http://redis.io/commands](http://redis.io/commands)。
> 
> 

tooaccess hello Redis 主控台中，按一下**主控台**從 hello **Redis 快取**刀鋒視窗。

![Redis 主控台](./media/cache-configure/redis-console-menu.png)

tooissue 命令，針對您的快取執行個體，只要類型 hello 所需的命令到 hello 主控台。

![Redis 主控台](./media/cache-configure/redis-console.png)


### <a name="using-hello-redis-console-with-a-premium-clustered-cache"></a>使用 hello Redis 主控台使用 premium 叢集快取

當使用高階 hello Redis 主控台叢集快取時，您可以發出命令 tooa 單一分區 hello 快取。 tooissue 命令 tooa 特定分區，第一次連接 toohello 所需的分區按一下 hello 分區選擇器上。

![Redis 主控台](./media/cache-configure/redis-console-premium-cluster.png)

如果您嘗試 tooaccess 比 hello 連接的分區會儲存在不同的分區化索引鍵，您會收到下列訊息錯誤的訊息類似 toohello。

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

在 hello 前一個範例中，分區 1 是 hello 選的分區，但是`myKey`hello 所示位於分區 0， `(shard 0)` hello 錯誤訊息的一部分。 在此範例中，tooaccess `myKey`，請選取分區 0 使用 hello 分區選擇器，然後按一下 問題所需的 hello 命令。


## <a name="move-your-cache-tooa-new-subscription"></a>移動您快取 tooa 新訂用帳戶
您可以按一下來移動快取 tooa 新的訂用**移動**。

![移動 Redis 快取](./media/cache-configure/redis-cache-move.png)

如需從一個資源群組 tooanother，以及從一個訂用帳戶 tooanother 移動資源資訊，請參閱[移動資源 toonew 資源群組或訂用帳戶](../azure-resource-manager/resource-group-move-resources.md)。

## <a name="next-steps"></a>後續步驟
* 如需使用 Redis 命令的詳細資訊，請參閱[如何執行 Redis 命令？](cache-faq.md#how-can-i-run-redis-commands)

