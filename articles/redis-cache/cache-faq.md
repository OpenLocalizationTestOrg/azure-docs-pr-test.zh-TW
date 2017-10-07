---
title: "aaaAzure Redis 快取常見問題集 |Microsoft 文件"
description: "了解 Azure Redis 快取 hello 回答 toocommon 問題、 模式和最佳作法"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c2c52b7d-b2d1-433a-b635-c20180e5cab2
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 2c6ed2f65f755bd08f04857b7af31f520cf4f158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-redis-cache-faq"></a>Azure Redis 快取常見問題集
了解 hello 回答 toocommon 問題、 模式和最佳作法 Azure Redis 快取。

## <a name="what-if-my-question-isnt-answered-here"></a>如果這裡沒有解答我的問題該怎麼辦？
如果這裡未列出您的問題，請告訴我們，我們將協助您找到答案。

* 您可以將問題張貼在常見問題集中的 hello 結尾 hello 註解中，且要與 hello Azure 快取小組和其他關於本文的社群成員交流。
* tooreach 更多觀眾，您可以張貼問題上 hello [Azure 快取 MSDN 論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=azurecache)和要與 hello Azure 快取小組和其他 hello 社群成員交流。
* 如果您想 toomake 功能要求時，您可以送出您的要求和意見太[Azure Redis 快取使用者語音](https://feedback.azure.com/forums/169382-cache)。
* 您也可以傳送電子郵件在 toous [Azure 快取外部意見反應](mailto:azurecache@microsoft.com)。

## <a name="azure-redis-cache-basics"></a>Azure Redis 快取基本知識
本節中的常見問題集 hello 涵蓋一些 hello Azure Redis 快取的基本概念。

* [何謂 Azure Redis 快取？](#what-is-azure-redis-cache)
* [我該如何開始使用 Azure Redis 快取？](#how-can-i-get-started-with-azure-redis-cache)

下列常見問題集涵蓋基本概念和 Azure Redis 快取有關的問題，而且其中一種會有所解答的 hello hello 常見問題集的其他章節。

* [應該使用哪個 Redis 快取供應項目和大小？](#what-redis-cache-offering-and-size-should-i-use)
* [我可以使用哪些 Redis 快取用戶端？](#what-redis-cache-clients-can-i-use)
* [Azure Redis 快取有本機模擬器嗎？](#is-there-a-local-emulator-for-azure-redis-cache)
* [如何監視 hello 健全狀況和我的快取的效能？](#how-do-i-monitor-the-health-and-performance-of-my-cache)

## <a name="planning-faqs"></a>規劃常見問題集
* [應該使用哪個 Redis 快取供應項目和大小？](#what-redis-cache-offering-and-size-should-i-use)
* [Azure Redis 快取效能](#azure-redis-cache-performance)
* [我應該在哪個區域找到快取？](#in-what-region-should-i-locate-my-cache)
* [Azure Redis 快取如何收費？](#how-am-i-billed-for-azure-redis-cache)
* [是否可以搭配 Azure Government 雲端、Azure 中國雲端或 Microsoft Azure (德國) 使用 Azure Redis 快取？](#can-i-use-azure-redis-cache-with-azure-government-cloud-azure-china-cloud-or-microsoft-azure-germany)

## <a name="development-faqs"></a>開發常見問題集
* [Hello StackExchange.Redis 設定選項代表該怎麼辦？](#what-do-the-stackexchangeredis-configuration-options-do)
* [我可以使用哪些 Redis 快取用戶端？](#what-redis-cache-clients-can-i-use)
* [Azure Redis 快取有本機模擬器嗎？](#is-there-a-local-emulator-for-azure-redis-cache)
* [如何執行 Redis 命令？](#how-can-i-run-redis-commands)
* [Azure Redis 快取為什麼沒有 MSDN 類別庫參考的某些像 hello 其他 Azure 服務？](#why-doesnt-azure-redis-cache-have-an-msdn-class-library-reference-like-some-of-the-other-azure-services)
* [是否可以使用 Azure Redis 快取做為 PHP 工作階段快取？](#can-i-use-azure-redis-cache-as-a-php-session-cache)
* [什麼是 Redis 資料庫？](#what-are-redis-databases)

## <a name="security-faqs"></a>安全性常見問題集
* [何時啟用連接 tooRedis hello 非 SSL 連接埠？](#when-should-i-enable-the-non-ssl-port-for-connecting-to-redis)

## <a name="production-faqs"></a>生產環境常見問題集
* [生產環境的最佳作法有哪些？](#what-are-some-production-best-practices)
* [什麼是一些 hello 考量使用常見的 Redis 命令時？](#what-are-some-of-the-considerations-when-using-common-redis-commands)
* [如何建立基準和測試 hello 我快取的效能？](#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* [執行緒集區成長的重要詳細資料](#important-details-about-threadpool-growth)
* [使用 StackExchange.Redis 時啟用 tooget 伺服器 GC hello 用戶端上更多的輸送量](#enable-server-gc-to-get-more-throughput-on-the-client-when-using-stackexchangeredis)
* [連線相關的效能考量](#performance-considerations-around-connections)

## <a name="monitoring-and-troubleshooting-faqs"></a>監視與疑難排解常見問題集
在此節涵蓋常見監視和疑難排解問題中的 hello 常見問題集。 如需監視和疑難排解您的 Azure Redis 快取執行個體的詳細資訊，請參閱[如何 toomonitor Azure Redis 快取](cache-how-to-monitor.md)和[如何 tootroubleshoot Azure Redis 快取](cache-how-to-troubleshoot.md)。

* [如何監視 hello 健全狀況和我的快取的效能？](#how-do-i-monitor-the-health-and-performance-of-my-cache)
* [為什麼看到逾時？](#why-am-i-seeing-timeouts)
* [為什麼我的用戶端的連線中斷 hello 快取？](#why-was-my-client-disconnected-from-the-cache)

## <a name="prior-cache-offering-faqs"></a>先前的快取服務常見問題集
* [我適合使用哪個 Azure 快取服務？](#which-azure-cache-offering-is-right-for-me)

### <a name="what-is-azure-redis-cache"></a>何謂 Azure Redis 快取？
Azure Redis 快取根據 hello 熱門開放原始碼[Redis 快取](http://redis.io)。 它可讓您從任何應用程式在 Azure 中存取 tooa 安全且專用 Redis 快取中，由 Microsoft 管理且可存取。 如需更詳細的概觀，請參閱 hello [Azure Redis 快取](https://azure.microsoft.com/services/cache/)Azure.com 上的產品頁面。

### <a name="how-can-i-get-started-with-azure-redis-cache"></a>我該如何開始使用 Azure Redis 快取？
有數種方式可讓您開始使用 Azure Redis 快取。

* 您可以查看我們針對 [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)、[ASP.NET](cache-web-app-howto.md)、[Java](cache-java-get-started.md)、[Node.js](cache-nodejs-get-started.md) 和 [Python](cache-python-get-started.md) 提供的其中一套教學課程。
* 您可以觀看[如何 tooBuild 高效能應用程式使用 Microsoft Azure Redis 快取](https://azure.microsoft.com/documentation/videos/how-to-build-high-performance-apps-using-microsoft-azure-cache/)。
* 您可以簽出 hello 符合您的專案 toosee toouse 如何 Redis hello 開發語言的 hello 用戶端的用戶端文件集。 有許多的 Redis 用戶端可和 Azure Redis 快取搭配使用。 如需 Redis 用戶端的清單，請參閱 [http://redis.io/clients](http://redis.io/clients)。

如果您還沒有 Azure 帳戶，您可以：

* [免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero)。 就可以使用的 tootry 出支付 Azure 服務的信用額度。 即使 hello 信用額度用完之後，您可以讓 hello 帳戶，並使用免費的 Azure 服務和功能。
* [啟用 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero)。 您的 MSDN 訂用帳戶每月會提供您額度，您可以用在 Azure 付費服務。

<a name="cache-size"></a>

### <a name="what-redis-cache-offering-and-size-should-i-use"></a>應該使用哪個 Redis 快取供應項目和大小？
每個 Azure Redis 快取供應項目提供不同層級的**大小**、**頻寬**、**高可用性**和 **SLA** 選項。

hello 以下是選擇快取服務的考量。

* **記憶體**: hello 基本和標準層級提供 250 MB – 53 GB。 hello Premium 層提供向上 too530 GB。 如需詳細資訊，請參閱 [Azure Redis 快取價格](https://azure.microsoft.com/pricing/details/cache/)。
* **網路效能**： 如果您需要高輸送量工作負載，hello Premium 層提供更多頻寬比較 tooStandard 或 Basic。 在各層中，內較大的大小快取還有更多的頻寬因為 hello 基礎裝載 hello 快取的 VM。 請參閱 hello[下列資料表](#cache-performance)如需詳細資訊。
* **輸送量**: hello Premium 層提供 hello 可用輸送量最大值。 如果 hello 快取伺服器或用戶端達到 hello 頻寬限制，您可能會收到 hello 用戶端的逾時。 如需詳細資訊，請參閱下表中的 hello。
* **高的可用性 SLA**: Azure Redis 快取可以確保標準/優質快取將會使用至少 99.9%的 hello 時間。 toolearn 深入了解我們的 SLA，請參閱[Azure Redis 快取定價](https://azure.microsoft.com/support/legal/sla/cache/v1_0/)。 hello SLA 只涵蓋連線 toohello 快取端點。 hello SLA 並未涵蓋防止資料遺失。 我們建議使用 hello Premium 層 tooincrease 復原會遺失資料中的 hello Redis 資料持續性功能。
* **Redis 資料持續性**: hello Premium 層可讓您 toopersist hello 快取資料的 Azure 儲存體帳戶中。 基本/標準快取中，所有的 hello 資料會儲存只會在記憶體中。 如果基礎結構發生問題，資料可能會遺失。 我們建議使用 hello Premium 層 tooincrease 復原會遺失資料中的 hello Redis 資料持續性功能。 Azure Redis 快取在 Redis 永續性中提供 RDB 和 AOF (即將推出) 選項。 如需詳細資訊，請參閱[如何 tooconfigure Premium Azure Redis 快取的持續性](cache-how-to-premium-persistence.md)。
* **Redis 叢集**: toocreate 會快取大於 53 GB 或 tooshard 資料在多個 Redis 節點，您可以使用 Redis 叢集，此功能在 hello Premium 層。 每個節點均包含一個主要/複本快取組以提供高可用性。 如需詳細資訊，請參閱[如何 tooconfigure Premium Azure Redis 快取叢集](cache-how-to-premium-clustering.md)。
* **增強式安全性及網路隔離**: Azure 虛擬網路 (VNET) 部署提供增強式的安全性和隔離您的 Azure Redis 快取，以及子網路，存取控制原則，和其他功能 toofurther 限制存取。 如需詳細資訊，請參閱[如何 tooconfigure 虛擬網路支援 Premium Azure Redis 快取](cache-how-to-premium-vnet.md)。
* **設定 Redis**： 在 hello Standard 和 Premium 層中，您可以設定 Redis Keyspace 通知。
* **用戶端連線的最大數目**: hello Premium 層提供 hello 可以連接 tooRedis，以較高的數字的較大大小的快取連接的用戶端數目上限。 如需詳細資訊，請參閱 [Azure Redis 快取定價](https://azure.microsoft.com/pricing/details/cache/)。
* **Redis 伺服器的專用核心**： 在 hello 優質層次中，所有快取大小的專用的核心 Redis。 Hello 基本/標準層次中，在 hello C1 大小和以上版本有專用的 Redis 伺服器核心。
* **Redis 為單一執行緒** ，因此兩個以上核心所提供的優點與只有兩個核心相同，但較大的 VM 大小通常會比較小的有更多頻寬。 如果 hello 快取伺服器或用戶端達到 hello 頻寬限制，您會收到 hello 用戶端的逾時。
* **效能改進**: hello Premium 層中的快取已部署在具有更快的處理器的硬體上提供更好的效能比較的 toohello 基本或標準層次。 高階層快取的輸送量較高，延遲性較低。

<a name="cache-performance"></a>

### <a name="azure-redis-cache-performance"></a>Azure Redis 快取效能
hello 下表顯示測試各種大小的標準時觀察到的 hello 頻寬上限值和 Premium 快取使用`redis-benchmark.exe`從針對 hello Azure Redis 快取端點 Iaas VM。 

>[!NOTE] 
>這些值並非保證值，也沒有關於這些數字的 SLA，只代表一般情況。 您應該在載入測試您的應用程式的自訂應用程式 toodetermine hello 正確快取大小。
>
>

從這個資料表中，我們可以繪製 hello 下列結論：

* Hello 快取的 hello 相同的大小較高的輸送量為比較的 toohello 標準層 hello Premium 層。 比方說，6 GB 快取，P1 的輸送量為 180000 RPS 比較 too49，如 C3 000。
* Redis 叢集，輸送量會增加以線性方式隨著您增加 hello hello 叢集中的分區 （節點） 數目。 例如，如果您建立的 10 個分區 P4 叢集，然後 hello 可用輸送量是 400000 * 10 = 4 百萬 RPS。
* 較大的金鑰大小的輸送量較高者為 hello Premium 層中做為比較 toohello Standard 價格區間。

| 定價層  | 大小 | CPU 核心 | 可用的頻寬 | 1 KB 值大小 |
| --- | --- | --- | --- | --- |
| **標準快取大小** | | |**每秒 Mb (Mb/s) / 每秒 MB (MB/s)** |**每秒要求數目 (RPS)** |
| C0 |250 MB |共用 |5 / 0.625 |600 |
| C1 |1 GB |1 |100 / 12.5 |12,200 |
| C2 |2.5 GB |2 |200 / 25 |24,000 |
| C3 |6 GB |4 |400 / 50 |49,000 |
| C4 |13 GB |2 |500 / 62.5 |61,000 |
| C5 |26 GB |4 |1,000 / 125 |115,000 |
| C6 |53 GB |8 |2,000 / 250 |150,000 |
| **高階快取大小** | |**每一分區的 CPU 核心數目** | **每秒 Mb (Mb/s) / 每秒 MB (MB/s)** |**每一分區的每秒要求數目 (RPS)** |
| P1 |6 GB |2 |1,500 / 187.5 |180,000 |
| P2 |13 GB |4 |3,000 / 375 |360,000 |
| P3 |26 GB |4 |3,000 / 375 |360,000 |
| P4 |53 GB |8 |6,000 / 750 |400,000 |

指示下載 hello 例如 Redis 工具`redis-benchmark.exe`，請參閱 hello[如何執行 Redis 命令？](#cache-commands) > 一節。

<a name="cache-region"></a>

### <a name="in-what-region-should-i-locate-my-cache"></a>我應該在哪個區域找到快取？
為了最佳效能和最低延遲，找出您 Azure Redis 快取在 hello 與快取的用戶端應用程式相同的區域。

<a name="cache-billing"></a>

### <a name="how-am-i-billed-for-azure-redis-cache"></a>Azure Redis 快取如何收費？
[此處](https://azure.microsoft.com/pricing/details/cache/)提供 Azure Redis 快取價格。 hello 定價頁面列出定價與每小時的頻率。 快取會從已刪除的快取的 hello 階段之前建立 hello 快取的 hello 時間每分鐘根據計費。 沒有任何停止或暫停 hello 計費的快取的選項。

### <a name="can-i-use-azure-redis-cache-with-azure-government-cloud-azure-china-cloud-or-microsoft-azure-germany"></a>是否可以搭配 Azure Government 雲端、Azure 中國雲端或 Microsoft Azure (德國) 使用 Azure Redis 快取？
是，Azure Government 雲端、Azure 中國雲端與 Microsoft Azure (德國) 提供 Azure Redis 快取。 這些相較於 Azure 公用雲端的雲端中，用於存取和管理 Azure Redis 快取的 hello Url 會不同。 

| 雲端   | Redis 的 DNS 尾碼            |
|---------|---------------------------------|
| 公開  | *.redis.cache.windows.net       |
| US Gov  | *.redis.cache.usgovcloudapi.net |
| 德國 | *.redis.cache.cloudapi.de       |
| 中國   | *.redis.cache.chinacloudapi.cn  |

如需有關使用 Azure Redis 快取與其他雲端時的考量的詳細資訊，請參閱下列連結查看 hello。

- [Azure Government 資料庫 - Azure Redis 快取](../azure-government/documentation-government-services-database.md#azure-redis-cache)
- [Azure 中國雲端 - Azure Redis 快取](https://www.azure.cn/documentation/services/redis-cache/)
- [Microsoft Azure (德國)](https://azure.microsoft.com/overview/clouds/germany/)

如需使用 PowerShell 在 Azure 政府雲端、 Azure 中國雲端及 Microsoft Azure 德國使用 Azure Redis 快取的資訊，請參閱[如何 tooconnect tooother 雲端 Azure Redis 快取 PowerShell](cache-howto-manage-redis-cache-powershell.md#how-to-connect-to-other-clouds)。

<a name="cache-configuration"></a>

### <a name="what-do-hello-stackexchangeredis-configuration-options-do"></a>Hello StackExchange.Redis 設定選項代表該怎麼辦？
StackExchange.Redis 有許多選項。 本節討論一些 hello 一般設定。 如需 StackExchange.Redis 選項的詳細資訊，請參閱 [StackExchange.Redis 設定](https://stackexchange.github.io/StackExchange.Redis/Configuration)。

| ConfigurationOptions | 說明 | 建議 |
| --- | --- | --- |
| AbortOnConnectFail |當設定 tootrue，hello 連接會在網路失敗後不重新連線。 |設定 toofalse，並讓 StackExchange.Redis 自動重新連線。 |
| ConnectRetry |hello 數次 toorepeat 連線嘗試期間初始連接。 |請參閱下列指導方針的附註的 hello。 |
| ConnectTimeout |連線作業的逾時 (毫秒)。 |請參閱下列指導方針的附註的 hello。 |

通常 hello hello 用戶端的預設值已足夠。 您可以微調您的工作負載為基礎的 hello 選項。

* **重試**
  * ConnectRetry 和 ConnectTimeout，hello 一般指引 toofail 快速並再試一次。 本指南根據您的工作負載和多少時間平均它會為您的用戶端 tooissue Redis 命令和接收回應。
  * 讓 StackExchange.Redis 自動重新連線，而不檢查連線狀態，並自行重新連線。 **請避免使用 hello ConnectionMultiplexer.IsConnected 屬性**。
  * Snowballing-有時可能會遇到的問題，正在重試以及 「 hello 重試 snowball 及永遠不會復原。 如果 snowballing 發生時，您應該考慮使用指數型輪詢重試演算法，如下所示[重試的一般指引](../best-practices-retry-general.md)hello Microsoft Patterns & Practices 群組所發行。
* **逾時值**
  * 請考慮您的工作負載，並據此設定 hello 值。 如果您要將儲存較大的值，設定 hello 逾時 tooa 較高的值。
  * 設定`AbortOnConnectFail`toofalse，並讓 StackExchange.Redis 為您重新連線。
  * Hello 應用程式使用單一 ConnectionMultiplexer 執行個體。 中所示，您可以使用 LazyConnection toocreate、 連接屬性所傳回的單一執行個體[連接 toohello 快取使用 hello ConnectionMultiplexer 類別](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache)。
  * 設定 hello `ConnectionMultiplexer.ClientName` tooan 應用程式執行個體唯一的屬性名稱供診斷之用。
  * 針對自訂工作負載，使用多個 `ConnectionMultiplexer` 執行個體。
      * 如果您的應用程式中有不同的負載，則可以遵循此模型。 例如：
      * 您可以有一個多工器來處理大型索引鍵。
      * 您可以有一個多工器來處理小型索引鍵。
      * 您可以設定連線逾時的不同值，以及每個所使用 ConnectionMultiplexer 的重試邏輯。
      * 設定 hello`ClientName`上每個診斷的多工器 toohelp 屬性。
      * 本指南可能會導致每個已簡化 toomore 延遲`ConnectionMultiplexer`。

### <a name="what-redis-cache-clients-can-i-use"></a>我可以使用哪些 Redis 快取用戶端？
其中一個 hello 優點 Redis 是有許多用戶端支援許多不同的開發語言。 如需最新的用戶端清單，請參閱 [Redis 用戶端](http://redis.io/clients)。 如需教學課程涵蓋數個不同的語言和用戶端，請參閱[如何 toouse Azure Redis 快取](cache-dotnet-how-to-use-azure-redis-cache.md)按一下 hello 預期的語言，從頂端 hello 發行項的 hello hello 語言切換器。

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<a name="cache-emulator"></a>

### <a name="is-there-a-local-emulator-for-azure-redis-cache"></a>Azure Redis 快取有本機模擬器嗎？
沒有任何本機模擬器，可為 Azure Redis 快取，但您可以從 hello 執行 redis server.exe hello MSOpenTech 版本[Redis 命令列工具](https://github.com/MSOpenTech/redis/releases/)您的本機電腦，並連接 tooit tooget 類似的經驗 tooa 本機快取模擬器，hello 下列範例所示：

    private static Lazy<ConnectionMultiplexer>
          lazyConnection = new Lazy<ConnectionMultiplexer>
        (() =>
        {
            // Connect tooa locally running instance of Redis toosimulate a local cache emulator experience.
            return ConnectionMultiplexer.Connect("127.0.0.1:6379");
        });

        public static ConnectionMultiplexer Connection
        {
            get
            {
                return lazyConnection.Value;
            }
        }


您可以選擇性地設定[redis.conf](http://redis.io/topics/config)檔案 toomore 緊密符合 hello[預設快取設定](cache-configure.md#default-redis-server-configuration)規劃線上 Azure Redis 快取視。

<a name="cache-commands"></a>

### <a name="how-can-i-run-redis-commands"></a>如何執行 Redis 命令？
您可以使用任何 hello 命令列於[Redis 命令](http://redis.io/commands#)除了 hello 命令列於[Redis 命令不支援在 Azure Redis 快取](cache-configure.md#redis-commands-not-supported-in-azure-redis-cache)。 您有數個選項 toorun Redis 命令。

* 如果您有標準或進階版快取，您可以執行使用 hello Redis 命令[Redis 主控台](cache-configure.md#redis-console)。 hello Redis 主控台提供安全的方式 toorun hello Azure 入口網站中的 Redis 命令。
* 您也可以使用 hello Redis 命令列工具。 toouse 它們，執行下列步驟 hello:
* 下載 hello [Redis 命令列工具](https://github.com/MSOpenTech/redis/releases/)。
* 連接 toohello 快取使用`redis-cli.exe`。 傳入 hello 快取端點使用 hello-h 參數和 hello 使用機碼-hello 下列範例所示：
* `redis-cli -h <your cache="" name="">
  .redis.cache.windows.net -a <key>
  `

> [!NOTE]
> hello Redis 命令列工具不適用於 hello SSL 連接埠，但您可以使用公用程式，例如`stunnel`toosecurely hello 工具 toohello SSL 通訊埠連線遵循 hello hello 指示[宣佈適用於 ASP.NET 工作階段狀態提供者Redis 預覽版本](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx)部落格文章。
>
>

<a name="cache-reference"></a>

### <a name="why-doesnt-azure-redis-cache-have-an-msdn-class-library-reference-like-some-of-hello-other-azure-services"></a>Azure Redis 快取為什麼沒有 MSDN 類別庫參考的某些像 hello 其他 Azure 服務？
Microsoft Azure Redis 快取根據 hello 熱門開放原始碼 Redis 快取和可由各種不同的存取[Redis 用戶端](http://redis.io/clients)用於許多程式設計語言。 每個用戶端有其本身會呼叫 toohello Redis 快取執行個體使用的 API [Redis 命令](http://redis.io/commands)。

因為每個用戶端都不同，所以 MSDN 上沒有一個集中式類別參考，每個用戶端都會維護其專屬的參考文件。 此外 toohello 參考文件，有幾個教學課程顯示如何 tooget 開始使用 Azure Redis 快取使用不同的語言和快取用戶端。 tooaccess 這些教學課程，請參閱[如何 toouse Azure Redis 快取](cache-dotnet-how-to-use-azure-redis-cache.md)按一下 hello 預期的語言，從頂端 hello 發行項的 hello hello 語言切換器。

### <a name="can-i-use-azure-redis-cache-as-a-php-session-cache"></a>是否可以使用 Azure Redis 快取做為 PHP 工作階段快取？
Toouse 為 PHP 工作階段快取的 Azure Redis 快取指定 hello 連接字串 tooyour Azure Redis 快取執行個體中的 [是]， `session.save_path`。

> [!IMPORTANT]
> 當使用 Azure Redis 快取做為 PHP 工作階段快取，您必須 URL 編碼 hello 安全性金鑰使用的 tooconnect toohello 快取，hello 下列範例所示：
>
> `session.save_path = "tcp://mycache.redis.cache.windows.net:6379?auth=<url encoded primary or secondary key here>";`
>
> 如果 hello 索引鍵不是 URL 編碼，可能會收到訊息，以類似的例外狀況：`Failed tooparse session.save_path`
>
>

如需為 PHP 工作階段快取與 hello PhpRedis 用戶端使用 Redis 快取的詳細資訊，請參閱[PHP 工作階段處理常式](https://github.com/phpredis/phpredis#php-session-handler)。

### <a name="what-are-redis-databases"></a>什麼是 Redis 資料庫？

Redis 資料庫都只邏輯隔離的 hello 內的資料相同的 Redis 執行個體。 所有 hello 資料庫之間會共用 hello 快取記憶體，並指定資料庫的實際記憶體耗用量相依於 hello 索引鍵/值儲存在該資料庫。 假設 C6 快取有 53 GB 的記憶體。 您可以選擇 tooput 所有 53 GB 到一個資料庫或分割的多個資料庫之間。 

> [!NOTE]
> 使用進階 Azure Redis 快取且啟用叢集時，只有資料庫 0 可用。 這項限制是內建的 Redis 限制而非特定 tooAzure Redis 快取。 如需詳細資訊，請參閱[需要 toomake 叢集任何變更 toomy 用戶端應用程式 toouse 嗎？](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
> 
> 


<a name="cache-ssl"></a>

### <a name="when-should-i-enable-hello-non-ssl-port-for-connecting-tooredis"></a>何時啟用連接 tooRedis hello 非 SSL 連接埠？
Redis 伺服器原本就不支援 SSL，但 Azure Redis 快取則支援。 如果您要連接 tooAzure Redis 快取，而且您的用戶端支援 SSL，例如 StackExchange.Redis，您應該使用 SSL。

>[!NOTE]
>新的 Azure Redis 快取執行個體預設會停用 hello 非 SSL 連接埠。 如果您的用戶端不支援 SSL，則您必須依照下列指示 hello hello 啟用 hello 非 SSL 連接埠[存取連接埠](cache-configure.md#access-ports)區段 hello [Azure Redis 快取中設定快取](cache-configure.md)發行項。
>
>

例如 redis 工具`redis-cli`無法搭配 hello SSL 連接埠，但您可以使用公用程式，例如`stunnel`toosecurely hello 工具 toohello SSL 通訊埠連線遵循 hello hello 指示[發表的 ASP.NET 工作階段狀態提供者Redis 預覽版本](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx)部落格文章。

如需下載 hello 指示 Redis 工具，請參閱 < hello[如何執行 Redis 命令？](#cache-commands) > 一節。

### <a name="what-are-some-production-best-practices"></a>生產環境的最佳作法有哪些？
* [StackExchange.Redis 最佳作法](#stackexchangeredis-best-practices)
* [組態和概念](#configuration-and-concepts)
* [效能測試](#performance-testing)

#### <a name="stackexchangeredis-best-practices"></a>StackExchange.Redis 最佳作法
* 設定`AbortConnect`toofalse，然後讓的 hello ConnectionMultiplexer 自動重新連線。 [參閱此處了解詳細資訊](https://gist.github.com/JonCole/36ba6f60c274e89014dd#file-se-redis-setabortconnecttofalse-md)。
* 重複使用 hello ConnectionMultiplexer-不會建立一個新的每個要求。 hello`Lazy<ConnectionMultiplexer>`模式[如下所示](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache)建議。
* Redis 在值越小時運作得最好，因此請考慮將較大的資料切分成多個金鑰。 在[此 Redis 討論](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ)中，100kb 就算很大。 閱讀 [這篇文章](https://gist.github.com/JonCole/db0e90bedeb3fc4823c2#large-requestresponse-size) 以了解較大值所造成的範例問題。
* 設定您[執行緒集區設定](#important-details-about-threadpool-growth)tooavoid 逾時。
* 使用至少 hello 預設 connectTimeout 5 秒。 在此時間間隔也會提供足夠時間 toore StackExchange.Redis-建立 hello 連線，發生網路 blip。
* 留意 hello 與您正在執行的不同作業相關聯的效能成本。 比方說，hello`KEYS`命令是一種 o （n） 運算，且應予以避免。 hello [redis.io 網站](http://redis.io/commands/)周圍 hello 階段複雜，它支援每個作業以取得詳細資料。 按一下每個作業的每個命令 toosee hello 複雜性。

#### <a name="configuration-and-concepts"></a>組態和概念
* 為生產環境系統使用標準或進階層。 hello 基本層是單一節點系統沒有 SLA 與任何資料複寫。 此外，請至少使用 C1 快取。 C0 快取通常用於簡單的開發/測試案例。
* 請記住，Redis 是一種 **記憶體內部** 資料存放區。 閱讀 [這篇文章](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md) ，您就能知道資料可能遺失的案例。
* 開發您的系統，使它可以處理連線音效[toopatching 和容錯移轉由於](https://gist.github.com/JonCole/317fe03805d5802e31cfa37e646e419d#file-azureredis-patchingexplained-md)。

#### <a name="performance-testing"></a>效能測試
* 使用啟動`redis-benchmark.exe`tooget 寫入您自己的效能測試之前可能輸送量的感覺。 因為`redis-benchmark`不支援 SSL，您必須[啟用 hello 非 SSL 連接埠，透過 Azure 入口網站 hello](cache-configure.md#access-ports) hello 測試執行之前。 如需範例，請參閱[如何可以基準測試和測試 hello 我快取的效能？](#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* hello 用戶端用於測試的 VM 必須處於 hello Redis 快取執行個體與相同的區域。
* 建議用戶端使用 Dv2 VM 系列，因為它們有更佳的硬體，而且應該提供 hello 獲得最佳結果。
* 請確定您選擇的 VM 具有至少多計算和頻寬功能做為您要測試的 hello 快取的用戶端。
* 如果您在 Windows 上，請在 hello 用戶端電腦上啟用 VRSS。 [參閱此處了解詳細資訊](https://technet.microsoft.com/library/dn383582.aspx)。
* 進階層 Redis 執行個體會有比較好的網路延遲和輸送量，因為是在比較好的硬體 (CPU 和網路) 上執行。

<a name="cache-redis-commands"></a>

### <a name="what-are-some-of-hello-considerations-when-using-common-redis-commands"></a>什麼是一些 hello 考量使用常見的 Redis 命令時？
* 您不應執行某些 Redis 命令需要很長的時間 toocomplete，如果不了解這些命令的 hello 影響。
  * 例如，不會執行 hello[金鑰](http://redis.io/commands/keys)命令在生產環境中，如可能會需要很長的時間 tooreturn 根據索引鍵的 hello 數目而定。 Redis 是單一執行緒伺服器，並且一次處理一個命令。 如果您有金鑰之後發出其他命令，它們將不會處理直到 Redis 處理 hello 金鑰命令。 hello [redis.io 網站](http://redis.io/commands/)周圍 hello 階段複雜，它支援每個作業以取得詳細資料。 按一下每個作業的每個命令 toosee hello 複雜性。
* 索引鍵大小 - 應該使用較小的索引鍵/值還是較大的索引鍵/值？ 一般情況下，這取決於 hello 案例。 如果您的案例需要較大的金鑰，您可以調整 hello ConnectionTimeout 和重試值，然後調整重試邏輯。 Redis 伺服器的觀點而言，較小的值被觀察 toohave 更佳的效能。
* 這些考量不表示您無法將較大的值儲存於 Redis;您必須留意的 hello 下列考量。 延遲會比較高。 如果您有一組更大的資料，另一個則是較小，您可以使用多個 ConnectionMultiplexer 執行個體，每一個設定一組不同的逾時和重試值 hello 先前所述[什麼執行 helloStackExchange.Redis 設定選項進行](#cache-configuration)> 一節。

<a name="cache-benchmarking"></a>

### <a name="how-can-i-benchmark-and-test-hello-performance-of-my-cache"></a>如何建立基準和測試 hello 我快取的效能？
* [啟用快取診斷](cache-how-to-monitor.md#enable-cache-diagnostics)這樣您就可以[監視器](cache-how-to-monitor.md)hello 快取的健全狀況。 您可以檢視度量 hello Azure 入口網站，而且也可以的 hello[下載並檢閱](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring)它們使用您選擇的 hello 工具。
* 您可以使用 redis benchmark.exe tooload 測試 Redis 伺服器。
* 請確定 hello 負載測試用戶端與 hello Redis 快取中 hello 相同的區域。
* 使用 redis cli.exe 和監視使用 hello INFO 命令 hello 快取。
* 如果您的負載造成高記憶體分散的情形，您應該相應 tooa 較大的快取大小增加。
* 如需下載 hello 指示 Redis 工具，請參閱 < hello[如何執行 Redis 命令？](#cache-commands) > 一節。

hello 下列命令會提供使用 redis benchmark.exe 的範例。 精確的結果，請執行下列命令從 hello 中的 VM 與您的快取相同的區域。

* 使用 1k 承載測試進行管線處理的 SET 要求

  `redis-benchmark.exe -h **yourcache**.redis.cache.windows.net -a **yourAccesskey** -t SET -n 1000000 -d 1024 -P 50`
* 使用 1k 承載測試進行管線處理的 GET 要求。
  附註： 執行上述第一個 toopopulate 快取的 hello 組測試

  `redis-benchmark.exe -h **yourcache**.redis.cache.windows.net -a **yourAccesskey** -t GET -n 1000000 -d 1024 -P 50`

<a name="threadpool"></a>

### <a name="important-details-about-threadpool-growth"></a>執行緒集區成長的重要詳細資料
hello CLR 執行緒集區有兩種執行緒-「 背景工作 」 和 「 I/O 完成通訊埠 」 (也稱為 IOCP) 執行緒。

* 背景工作執行緒是用於處理 `Task.Run(…)` 或 `ThreadPool.QueueUserWorkItem(…)` 方法之類的作業。 當工作需要在背景執行緒上的 toohappen hello CLR 中各種元件也會使用這些執行緒。
* IOCP 執行緒可用時非同步 IO （例如讀取 hello 網路）。

hello 執行緒集區提供新的背景工作執行緒或 I/O 完成執行緒，直到它 （而不需要任何節流） 視達到執行緒的每個類型的 hello 「 最低 」 設定。 根據預設，hello 的執行緒數目下限是在系統上設定 toohello 處理器數目。

一次 hello 現有 （忙碌） 執行緒叫用 hello 「 最低 」 數目的執行緒數目，hello 執行緒集區會進行節流處理 hello 速率，它會插入新執行緒 tooone 每個執行緒，500 毫秒。 通常，如果您的系統需要 IOCP 執行緒的工作暴增，系統將可快速處理該工作。 不過，如果 hello 批突發之工作超過 hello 設定 「 最低 」 設定，會有一些延遲為 hello ThreadPool 等候其中一個兩件事 toohappen 處理某些 hello 工作。

1. 現有的執行緒會變成可用 tooprocess hello 工作。
2. 有 500 毫秒沒有現有的執行緒變得可用，因此會建立一個新的執行緒。

基本上，這表示，hello 的忙碌執行緒數目大於最小執行緒時，您可能支付 500 毫秒延遲才能 hello 應用程式處理網路流量。 此外，它是重要 toonote，當現有的執行緒會持續閒置的時間超過 15 秒 （根據我的記得）、 將會清除，而且可以重複這個循環的成長和壓縮，甚至。

如果我們查看來自 StackExchange.Redis (建置 1.0.450 或更新版本) 的範例錯誤訊息，您會看到它現在會列印執行緒集區統計資料 (請參閱以下的 IOCP 和背景工作詳細資料)。

    System.TimeoutException: Timeout performing GET MyKey, inst: 2, mgr: Inactive,
    queue: 6, qu: 0, qs: 6, qc: 0, wr: 0, wq: 0, in: 0, ar: 0,
    IOCP: (Busy=6,Free=994,Min=4,Max=1000),
    WORKER: (Busy=3,Free=997,Min=4,Max=1000)

在 hello 上述範例中，您可以看到 IOCP 執行緒中，有 6 的忙碌執行緒，而且 hello 系統是設定的 tooallow 4 最小執行緒。 在此情況下，hello 用戶端應該會有可能看到兩個 500 毫秒延遲因為 6 > 4。

請注意，如果 IOCP 或背景工作執行緒的成長發生節流，StackExchange.Redis 可能達到逾時。

### <a name="recommendation"></a>建議
指定這項資訊，我們強烈建議客戶將 IOCP 和背景工作執行緒 toosomething hello 最小的組態值大於 hello 預設值。 我們無法讓一體適用這個值應該是什麼由於 hello 右值，一個應用程式可能會太高/低另一個應用程式的指引。 這項設定可能也會影響 hello 效能的其他部分的複雜應用程式，讓每一客戶必須 toofine 微調此特定的設定 tootheir 需要。 200 或 300 是好的起點，那麼請測試並視需要調整。

如何 tooconfigure 這項設定：

* 在 ASP.NET 中，使用 hello ["minIoThreads 」 組態設定][ "minIoThreads" configuration setting]下 hello `<processModel>` web.config 中的組態項目。如果您在 Azure 網站內執行，此設定不會公開透過 hello 組態選項。 不過，您仍應該要能夠 tooconfigure 此以程式設計方式設定 （請參閱下方） 中 global.asax.cs Application_Start 方法的。

  > [!NOTE] 
  > hello 這個組態項目中指定的值是*每個核心*設定。 例如，如果您有 4 核心電腦，並想要在執行階段您 minIOThreads 設定 toobe 200，您會使用`<processModel minIoThreads="50"/>`。
  >

* 在 ASP.NET 之外，使用 hello [ThreadPool.SetMinThreads(...)](https://msdn.microsoft.com/library/system.threading.threadpool.setminthreads.aspx)應用程式開發介面。

<a name="server-gc"></a>

### <a name="enable-server-gc-tooget-more-throughput-on-hello-client-when-using-stackexchangeredis"></a>使用 StackExchange.Redis 時啟用 tooget 伺服器 GC hello 用戶端上更多的輸送量
啟用伺服器 GC 可以最佳化 hello 用戶端，並且使用 StackExchange.Redis 時提供更好的效能和輸送量。 如需有關伺服器 GC 以及 tooenable，請參閱下列文章 hello:

* [tooenable 伺服器 GC](https://msdn.microsoft.com/library/ms229357.aspx)
* [Fundamentals of Garbage Collection (記憶體回收的基本概念)](https://msdn.microsoft.com/library/ee787088.aspx)
* [Garbage Collection and Performance (記憶體回收與效能)](https://msdn.microsoft.com/library/ee851764.aspx)


### <a name="performance-considerations-around-connections"></a>連線相關的效能考量

每個定價層都有不同的用戶端連線、記憶體和頻寬的限制。 每個快取的大小可讓*最多*特定數目的連線，每個連線 tooRedis 具有額外負荷與其相關聯。 因 TLS/SSL 加密而產生的 CPU 與記憶體使用量即是這類額外負荷的其中一例。 指定快取大小的 hello 最大連線限制假設輕度載入的快取。 如果從連接的額外負荷載入*加上*從用戶端作業的負載超過容量的 hello 系統、 hello 快取可以體驗容量問題，即使您未超過 hello 目前快取大小的 hello 連線限制。

如需每一層的 hello 不同的連線限制的詳細資訊，請參閱[Azure Redis 快取定價](https://azure.microsoft.com/pricing/details/cache/)。 如需有關連線及其他預設組態的詳細資訊，請參閱[預設 Redis 伺服器組態](cache-configure.md#default-redis-server-configuration)。

<a name="cache-monitor"></a>

### <a name="how-do-i-monitor-hello-health-and-performance-of-my-cache"></a>如何監視 hello 健全狀況和我的快取的效能？
可監視 Microsoft Azure Redis 快取執行個體，在 hello [Azure 入口網站](https://portal.azure.com)。 您可以檢視度量、 釘選度量圖表 toohello 開始面板、 自訂 hello 日期和時間範圍的監控圖表、 加入和從 hello 圖表移除度量和設定警示，當符合特定條件。 如需詳細資訊，請參閱 [監視 Azure Redis 快取](cache-how-to-monitor.md)。

hello Redis 快取**資源功能表**也包含數個工具來監視和疑難排解您的快取。

* **疑難排解和解決問題**提供常見問題的相關資訊，以及解決問題的策略。
* **資源健康狀態** 會監看您的資源，並告知您資源是否正如預期般執行。 如需 hello Azure 資源健全狀況服務的詳細資訊，請參閱[Azure 資源健全狀況概觀](../resource-health/resource-health-overview.md)。
* **新的支援要求**提供您的快取選項 tooopen 支援要求。

這些工具讓您 toomonitor hello 健全狀況的 Azure Redis 快取執行個體，以及協助您管理應用程式快取。 如需詳細資訊，請參閱 hello 」 支援和疑難排解設定 」 一節[如何 tooconfigure Azure Redis 快取](cache-configure.md)。

<a name="cache-timeouts"></a>

### <a name="why-am-i-seeing-timeouts"></a>為什麼看到逾時？
逾時，就可能發生在 hello 用戶端，您會使用 tootalk tooRedis。 當將命令傳送 toohello Redis 伺服器時，hello 命令佇列時，Redis 伺服器最終會拾取 hello 命令，並加以執行。 不過 hello 用戶端可以在此程序的逾時以及如果它會發生例外狀況對呼叫端的 hello 引發。 如需對逾時問題進行疑難排解的詳細資訊，請參閱[用戶端疑難排解](cache-how-to-troubleshoot.md#client-side-troubleshooting)和 [StackExchange.Redis 逾時例外狀況](cache-how-to-troubleshoot.md#stackexchangeredis-timeout-exceptions)。

<a name="cache-disconnect"></a>

### <a name="why-was-my-client-disconnected-from-hello-cache"></a>為什麼我的用戶端的連線中斷 hello 快取？
hello 下面是一些常見的快取中斷連線的原因。

* 用戶端原因
  * hello 用戶端應用程式已重新部署。
  * hello 用戶端應用程式執行縮放的作業。
    * 在雲端服務或 Web 應用程式的 hello 情況下，這可能是因為 tooauto 縮放比例。
  * hello hello 變更的用戶端上的網路層。
  * 在用戶端中 hello 或 hello hello 用戶端和伺服器 hello 之間的網路節點中，就會發生暫時性錯誤。
  * 已達到 hello 頻寬的閾值限制。
  * 受限於 CPU 的作業花費太長 toocomplete。
* 伺服器端原因
  * 在 hello 標準版快取提供項目，hello Azure Redis 快取服務會起始 hello 主要節點 toohello 次要節點從容錯移轉。
  * Azure 已修補 hello hello 快取部署所在的執行個體
    * 這可能適用於 Redis 伺服器更新或一般 VM 維護。

### <a name="which-azure-cache-offering-is-right-for-me"></a>我適合使用哪個 Azure 快取服務？
> [!IMPORTANT]
> 根據去年的[公告](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)，Azure 受管理的快取服務和 Azure In-Role Cache 服務已在 2016 年 11 月 30 日**淘汰**。 我們建議 toouse [Azure Redis 快取](https://azure.microsoft.com/services/cache/)。 如需移轉資訊，請參閱[從受管理快取服務 tooAzure Redis 快取移轉](cache-migrate-to-redis.md)。
>
>

### <a name="azure-redis-cache"></a>Azure Redis 快取
Azure Redis 快取通常用於向上 too53 GB 的大小，並有 99.9%的 SLA 的可用性。 新的 hello [premium 層](cache-premium-tier-intro.md)提供 too530 GB 和支援的叢集，VNET，與持續性，以 99.9 %sla 的大小。

Azure Redis 快取可讓客戶 hello 能力 toouse 安全且專用的 Redis 快取中，由 Microsoft 管理。 透過這項優惠，您可以取得 tooleverage hello 豐富的功能集和生態系統提供的 Redis，以及可靠主控和監視 microsoft。

不同於僅處理金鑰-值組的傳統快取，Redis 受到歡迎是因為其高效能資料類型。 Redis 也支援執行不可部分完成作業，請在這些型別，如附加 tooa 字串;遞增雜湊; 中的 hello 值推送 tooa 清單;計算集合交集、 聯集和差異。或取得已排序資料集中的最高排名的 hello 成員。 其他功能包括支援交易、 pub/sub、 Lua 指令碼、 金鑰具有有限的存留時間，以及組態設定 toomake Redis 的行為更像傳統快取。

另一個重要層面 tooRedis 成功是建置 hello 健全、 有活力的開放原始碼生態系統。 這會反映在 hello 多樣的 Redis 用戶端可以使用多種語言。 這個生態系統和各種不同的用戶端可讓 Azure Redis 快取 toobe 幾乎您會在 Azure 內建置任何工作負載所使用。

如需有關如何開始使用 Azure Redis 快取的詳細資訊，請參閱[如何 tooUse Azure Redis 快取](cache-dotnet-how-to-use-azure-redis-cache.md)和[Azure Redis 快取文件](index.md)。

### <a name="managed-cache-service"></a>受管理的快取服務
[受管理的快取服務已在 2016 年 11 月 30 日淘汰 (英文)。](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)

tooview 封存文件，請參閱[封存受管理快取服務文件](https://msdn.microsoft.com/library/azure/dn386094.aspx)。

### <a name="in-role-cache"></a>角色中快取
[In-Role Cache 已在 2016 年 11 月 30 日淘汰 (英文)。](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)

tooview 封存文件，請參閱[封存的角色中快取文件](https://msdn.microsoft.com/library/azure/dn386103.aspx)。

["minIoThreads" configuration setting]: https://msdn.microsoft.com/library/vstudio/7w2sway1(v=vs.100).aspx
