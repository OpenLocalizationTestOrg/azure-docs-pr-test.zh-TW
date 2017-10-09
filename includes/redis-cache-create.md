toocreate 快取中，第一次登入 toohello [Azure 入口網站](https://portal.azure.com)，然後按一下**新增** > **資料庫** > **Redis 快取**.

> [!NOTE]
> 如果您沒有 Azure 帳戶，只需要幾分鐘的時間就可以 [免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) 。
> 
> 

![New cache](media/redis-cache-create/redis-cache-new-cache-menu.png)

> [!NOTE]
> 此外 toocreating hello Azure 入口網站中的快取，您也可以建立使用資源管理員範本、 PowerShell 或 Azure CLI。
> 
> * toocreate 的快取使用資源管理員範本，請參閱[建立 Redis 快取使用的範本](../articles/redis-cache/cache-redis-cache-arm-provision.md)。
> * toocreate 快取使用 Azure PowerShell，請參閱[管理 Azure Redis 快取使用 Azure PowerShell](../articles/redis-cache/cache-howto-manage-redis-cache-powershell.md)。
> * toocreate 快取使用 Azure CLI，請參閱[如何 toocreate 和管理 Azure Redis 快取使用 hello Azure 命令列介面 (Azure CLI)](../articles/redis-cache/cache-manage-cli.md)。
> 
> 

在 hello**新增 Redis 快取**刀鋒視窗中，指定 hello hello 快取所需的組態。

![Create cache](media/redis-cache-create/redis-cache-cache-create.png) 

* 在**Dns 名稱**，輸入唯一的快取名稱 toouse hello 快取端點。 hello 快取名稱必須是介於 1 到 63 個字元之間的字串，且包含數字、 字母及 hello`-`字元。 hello 快取名稱不能以開頭或結尾 hello`-`連續的字元，和`-`字元是無效的。
* 如**訂用帳戶**，選取 hello toouse 需 hello 快取的 Azure 訂用帳戶。 如果您的帳戶有只有一個訂用帳戶，它會自動選取和 hello**訂用帳戶**下拉式清單將不會顯示。
* 在 [資源群組] 中，選取或建立快取的資源群組。 如需詳細資訊，請參閱[使用資源群組 toomanage 您的 Azure 資源](../articles/azure-resource-manager/resource-group-overview.md)。 
* 使用**位置**toospecify hello 在其中裝載您快取的地理位置。 Hello 獲得最佳效能，Microsoft 強烈建議您建立 hello 快取可在 hello 與 hello 快取的用戶端應用程式相同的區域。
* 使用**定價層**tooselect hello 需要快取大小和功能。
* **Redis 叢集**可讓您 toocreate 快取大於 53 GB 和 tooshard 資料在多個 Redis 節點。 如需詳細資訊，請參閱[如何 tooconfigure Premium Azure Redis 快取叢集](../articles/redis-cache/cache-how-to-premium-clustering.md)。
* **Redis 持續性**提供 hello 能力 toopersist 您快取 tooan Azure 儲存體帳戶。 如需設定持續性的指示，請參閱[如何 tooconfigure Premium Azure Redis 快取的持續性](../articles/redis-cache/cache-how-to-premium-persistence.md)。
* **虛擬網路**提供增強式的安全性和隔離藉由限制存取 tooyour 快取 tooonly 這些用戶端內指定的 hello Azure 虛擬網路。 您可以使用 VNet 的所有 hello 的功能，例如子網路、 存取控制原則和其他功能 toofurther 限制存取 tooRedis。 如需詳細資訊，請參閱[如何 tooconfigure 虛擬網路支援 Premium Azure Redis 快取](../articles/redis-cache/cache-how-to-premium-vnet.md)。
* 根據預設，新的快取會停用非 SSL 存取。 tooenable hello 非 SSL 連接埠，核取**解除封鎖通訊埠 (非 SSL 加密) 6379**。

一旦設定 hello 新快取選項，按一下**建立**。 可能需要幾分鐘，讓建立 hello 快取 toobe。 toocheck hello 狀態，您可以監視 hello hello 開始面板上的進度。 建立 hello 快取之後，您新的快取都有**執行**狀態，而且已準備用於[預設設定](../articles/redis-cache/cache-configure.md#default-redis-server-configuration)。

![Cache created](media/redis-cache-create/redis-cache-cache-created.png)

