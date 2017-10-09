---
title: "aaaIntroduction toohello Azure Redis 快取進階層 |Microsoft 文件"
description: "深入了解如何 toocreate 和管理 Redis 的持續性、 Redis 叢集，以及 Premium 層 Azure Redis 快取執行個體的 VNET 支援"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 30f46f9f-e6ec-4c38-a8cc-f9d4444856e5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 5b58a03647fbf1198509ac6f1acd04f1b682ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-redis-cache-premium-tier"></a>簡介 toohello Azure Redis 快取進階層
Azure Redis 快取是可協助您藉由提供的超快存取 tooyour 資料建立高度擴充且回應迅速的應用程式的分散式且受管理快取。 

hello 新 Premium 層是企業 」 準備好層，其中包含所有 hello 標準層功能和詳細資訊，例如更佳的效能、 更大的工作負載、 災害復原、 匯入/匯出，並增強式安全性。 繼續閱讀 toolearn 更多關於 hello 的 hello Premium 快取層額外的功能。

## <a name="better-performance-compared-toostandard-or-basic-tier"></a>較佳的效能比較 tooStandard 或基本層
**效能優於標準或基本層。** Hello Premium 層中的快取會有更快的處理器，並提供更好的效能比較 toohello 基本或標準層的硬體上部署。 高階層快取的輸送量較高，延遲性較低。 

**輸送量 hello 相同大小的快取較高者為 Premium 中做為比較的 tooStandard 層。** 例如，hello 輸送量 53 GB P4 (Premium) 快取是 250k 每秒要求數做為 C6 比較 too150K （標準）。

如需高階快取的大小、輸送量和頻寬的詳細資訊，請參閱 [Azure Redis 快取常見問題集](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)

## <a name="redis-data-persistence"></a>Redis 資料永續性
hello Premium 層可讓您 toopersist hello 快取資料的 Azure 儲存體帳戶中。 基本/標準快取中所有的 hello 資料會儲存只會在記憶體中。 如果基礎結構發生問題，資料可能會遺失。 我們建議使用 hello Premium 層 tooincrease 復原會遺失資料中的 hello Redis 資料持續性功能。 Azure Redis Cache 在 [Redis 永續性](http://redis.io/topics/persistence)中提供 RDB 和 AOF (即將推出) 選項。 

如需設定持續性的指示，請參閱[如何 tooconfigure Premium Azure Redis 快取的持續性](cache-how-to-premium-persistence.md)。

## <a name="redis-cluster"></a>Redis 叢集
如果您想 toocreate 快取大於 53 GB，或想要跨多個 Redis 節點的 tooshard 資料，您可以使用 Redis 叢集 hello Premium 層中所提供。 每個節點均包含一個 Azure 所管理的主要/複本快取組，可提供高可用性。 

**Redis 叢集可提供最大的擴充能力和輸送量。** 隨著您增加 hello hello 叢集中的分區 （節點） 數目，會以線性方式增加輸送量。 例如 如果您建立的 10 個分區，P4 叢集則 hello 可用輸送量 250k 之間 * 10 = 2.5 百萬個每秒要求數。 請參閱 hello [Azure Redis 快取常見問題集](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)如需詳細資訊大小、 輸送量和進階版快取使用的頻寬。

tooget 入門叢集，請參閱[如何 tooconfigure Premium Azure Redis 快取叢集](cache-how-to-premium-clustering.md)。

## <a name="enhanced-security-and-isolation"></a>增強的安全性和隔離
在 hello 基本或標準層中建立的快取都可供存取 hello 公用網際網路。 存取的 toohello 快取已限制根據 hello 存取金鑰。 與 hello Premium 層，您可以進一步確保只有指定的網路內的用戶端可以存取 hello 快取。 您可以在 [Azure 虛擬網路 (VNet)](https://azure.microsoft.com/services/virtual-network/)中部署 Redis Cache。 您可以使用 VNet 的所有 hello 的功能，例如子網路、 存取控制原則和其他功能 toofurther 限制存取 tooRedis。

如需詳細資訊，請參閱[如何 tooconfigure 虛擬網路支援 Premium Azure Redis 快取](cache-how-to-premium-vnet.md)。

## <a name="importexport"></a>匯入/匯出
匯入/匯出是 Azure Redis 快取資料管理作業可讓您 tooimport 資料至 Azure Redis 快取或匯出資料，從 Azure Redis 快取所匯入和匯出從 premium 快取 tooa 中的分頁 blob 的 Azure Redis 快取資料庫 (RDB) 快照集儲存體帳戶。 這可讓您 toomigrate 不同的 Azure Redis 快取執行個體之間或填入 hello 快取，以使用之前的資料。

匯入可為使用的 toobring Redis 相容 RDB 檔案從任何執行中的任何雲端或環境，包括 Linux、 Windows 或任何雲端提供者，例如 Amazon Web Services 等項目上執行的 Redis 的 Redis 伺服器。 匯入資料是簡單的方式 toocreate 預先填入資料的快取。 在 hello 匯入過程中，Azure Redis 快取 Azure 儲存體中的 hello RDB 檔案載入記憶體，然後插入 hello 快取中的 hello 索引鍵。

匯出可讓您 tooexport hello 資料儲存在 Azure Redis 快取 tooRedis 相容 RDB 檔案中。 您可以使用此功能 toomove 資料從一個 Azure Redis 快取執行個體 tooanother 或 tooanother Redis 伺服器。 在 hello 匯出程序，hello VM 的主機 hello Azure Redis 快取伺服器執行個體，而且 hello 檔案上傳的 toohello 指定儲存體帳戶上建立暫存檔。 Hello 匯出作業完成時為其中一個狀態為成功或失敗，則會刪除 hello 暫存檔案。

如需詳細資訊，請參閱[如何 tooimport 資料並將資料從 Azure Redis 快取匯出](cache-how-to-import-export-data.md)。

## <a name="reboot"></a>重新啟動
hello premium 層可讓您 tooreboot 您快取指定的一或多個節點。 這可讓您 tootest hello 事件中的恢復功能的應用程式的失敗。 您可以重新啟動下列節點的 hello。

* 快取的主要節點
* 快取的從屬節點
* 快取的主要和從屬節點
* 當使用進階版快取叢集，您可以重新啟動 hello master、 從屬版本或在兩個節點 hello 快取中的個別分區

如需詳細資訊，請參閱[重新啟動](cache-administration.md#reboot)和[重新啟動常見問題集](cache-administration.md#reboot-faq)。

>[!NOTE]
>重新啟動功能現在已對所有的 Azure Redis 快取層啟用。
>
>

## <a name="schedule-updates"></a>更新排程
hello 已排程的更新功能可讓您 toodesignate 用於您的快取的維護期間。 當指定 hello 維護視窗時，Redis 伺服器的任何更新都會在此期間。 toodesignate 維護視窗中，選取所需的 hello 天，並指定 hello 維護視窗開始時間的每一天。 請注意，hello 維護視窗時間-utc 時區。 

如需詳細資訊，請參閱[排程更新](cache-administration.md#schedule-updates)和[排程更新常見問題集](cache-administration.md#schedule-updates-faq)。

> [!NOTE]
> 只有 Redis 的伺服器 hello 排程的維護期間進行更新。 hello 維護視窗不會套用 tooAzure 更新，或更新 toohello VM 的作業系統。
> 
> 

## <a name="geo-replication"></a>異地複寫

**異地複寫**提供一個機制，可供連結兩個進階層 Azure Redis 快取執行個體。 一個快取指定為 hello 主要的連線快取，而 hello hello 次要連結快取為其他。 hello 次要連結快取會變成唯讀的並寫入的 toohello 主要快取的資料複寫 toohello 次要連結快取。 這項功能可以跨 Azure 區域是使用的 tooreplicate 快取。

如需詳細資訊，請參閱[如何 Azure Redis 快取的地理複寫 tooconfigure](cache-how-to-geo-replication.md)。


## <a name="tooscale-toohello-premium-tier"></a>tooscale toohello premium 層
tooscale toohello premium 層，只選擇其中一個 hello premium 層 hello**變更定價層**刀鋒視窗。 您也可以調整快取 toohello 高檔使用 PowerShell 和 CLI。 如需逐步指示，請參閱[如何 tooScale Azure Redis 快取](cache-how-to-scale.md)和[如何 tooautomate 縮放作業](cache-how-to-scale.md#how-to-automate-a-scaling-operation)。

## <a name="next-steps"></a>後續步驟
建立快取，並瀏覽 hello 新 premium 層功能。

* [如何 tooconfigure Premium Azure Redis 快取的持續性](cache-how-to-premium-persistence.md)
* [如何 tooconfigure 虛擬網路支援 Premium Azure Redis 快取](cache-how-to-premium-vnet.md)
* [如何 tooconfigure Premium Azure Redis 快取叢集](cache-how-to-premium-clustering.md)
* [如何將 tooimport 資料以及匯出資料從 Azure Redis 快取](cache-how-to-import-export-data.md)
* [如何 tooadminister Azure Redis 快取](cache-administration.md)

