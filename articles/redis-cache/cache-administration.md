---
title: "aaaHow tooadminister Azure Redis 快取 |Microsoft 文件"
description: "了解 tooperform 系統管理工作這類的重新和排程 Azure Redis 快取更新"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 8c915ae6-5322-4046-9938-8f7832403000
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: eb24668a3f6264444e7d4daf1ac43b41b12dfe66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadminister-azure-redis-cache"></a>如何 tooadminister Azure Redis 快取
本主題描述如何 tooperform 系統管理工作如[重新開機](#reboot)和[排程更新](#schedule-updates)對您的 Azure Redis 快取執行個體。

## <a name="reboot"></a>重新啟動
hello**重新開機**刀鋒視窗可讓您 tooreboot 快取的一個或多個節點。 這個重新開機功能可讓您 tootest 提供恢復功能的應用程式的快取節點失敗時。

![重新啟動](./media/cache-administration/redis-cache-administration-reboot.png)

選取 hello 節點 tooreboot，然後按一下**重新開機**。

![重新啟動](./media/cache-administration/redis-cache-reboot.png)

如果您有進階版快取以啟用叢集時，您可以選取 hello 快取 tooreboot 哪一個的分區。

![重新啟動](./media/cache-administration/redis-cache-reboot-cluster.png)

tooreboot 一或多個節點的快取中，選取所需的 hello 節點，然後按一下 **重新開機**。 如果您有進階版快取之啟用叢集時，選取所需的 hello 分區 tooreboot，然後按一下**重新開機**。 後幾分鐘的時間，hello 選取的節點重新開機，且上線幾分鐘後。

hello 影響用戶端應用程式而異的哪些節點您重新開機。

* **主要**-hello 主要節點重新啟動，Azure Redis 快取失敗 toohello 複本節點上，並將它升級 toomaster 時。 在此容錯移轉，可能會較短的間隔中的連線可能會失敗 toohello 快取。
* **從屬**-時 hello 從屬節點重新開機時，通常是沒有影響 toocache 用戶端。
* **主要和備用**-當這兩個快取節點重新開機時，hello 主要節點恢復上線之前，將會遺失在 hello 快取和連線 toohello 快取失敗的所有資料。 如果您已設定[資料持續性](cache-how-to-premium-persistence.md)，hello 最新的備份還原時 hello 快取的重新上線，但 hello 最近備份之後發生的任何快取寫入都會遺失。
* **快取啟用叢集節點的高階**-當您重新啟動其中一個或更多進階版快取叢集的節點已啟用，hello 行為 hello 選取節點是 hello 相同做為當您重新啟動 hello 對應的節點或節點的非叢集快取。

> [!IMPORTANT]
> 重新啟動現在適用於所有定價層。
> 
> 

## <a name="reboot-faq"></a>重新啟動常見問題集
* [哪些節點應該我重新啟動 tootest 我的應用程式嗎？](#which-node-should-i-reboot-to-test-my-application)
* [可以重新啟動 hello 快取 tooclear 用戶端連線嗎？](#can-i-reboot-the-cache-to-clear-client-connections)
* [如果我重新啟動，將會遺失快取中的資料嗎？](#will-i-lose-data-from-my-cache-if-i-do-a-reboot)
* [我可以使用 PowerShell、CLI 或其他管理工具重新啟動我的快取嗎？](#can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools)
* [哪些定價層可以使用 hello 重新開機功能嗎？](#what-pricing-tiers-can-use-the-reboot-functionality)

### <a name="which-node-should-i-reboot-tootest-my-application"></a>哪些節點應該我重新啟動 tootest 我的應用程式嗎？
tootest hello 恢復功能的應用程式發生故障的 hello 主要節點的快取、 重新開機 hello **Master**節點。 tootest hello 恢復功能的應用程式發生故障的 hello 次要節點，重新開機 hello**從屬**節點。 tootest hello 復原應用程式的總發生故障的 hello 快取，重新啟動**兩者**節點。

### <a name="can-i-reboot-hello-cache-tooclear-client-connections"></a>可以重新啟動 hello 快取 tooclear 用戶端連線嗎？
是，如果您重新啟動 hello 快取會清除所有用戶端連線。 重新開機可以是其中所有用戶端連接都用完到期 tooa 邏輯錯誤或 hello 用戶端應用程式中的 bug hello 案例中很有用。 每個定價層而有不同[用戶端連線限制](cache-configure.md#default-redis-server-configuration)的 hello 各種大小，而且一旦達到這些限制，會接受用戶端連線。 重新開機 hello 快取提供方式 tooclear 所有用戶端連線。

> [!IMPORTANT]
> 如果您重新啟動您的快取 tooclear 用戶端連線，StackExchange.Redis 會自動重新連線之後 hello Redis 節點上線。 如果未解決根本問題的 hello，hello 用戶端連線可能會繼續 toobe 用完。
> 
> 

### <a name="will-i-lose-data-from-my-cache-if-i-do-a-reboot"></a>如果我重新啟動，將會遺失快取中的資料嗎？
如果您重新啟動這兩個 hello **Master**和**從屬**節點 hello 快取 （或如果您使用進階版快取叢集啟用該分區） 中的所有資料都都會遺失。 如果您已設定[資料持續性](cache-how-to-premium-persistence.md)，hello 快取的重新上線，但 hello 備份之後所發生的任何快取寫入都會遺失時，將會還原 hello 最新備份。

如果您重新啟動其中一個 hello 節點，資料不是通常遺失，但仍可能。 例如，如果 hello 主要節點重新開機，而且快取寫入正在進行中，從 hello 快取寫入 hello 資料就會遺失。 另一個資料遺失的狀況是如果您重新啟動一個節點，然後 hello 其他節點會 toogo 向下 hello tooa 失敗因為相同的時間。 如需資料遺失的可能原因的詳細資訊，請參閱[Redis 在何種情形的 toomy 資料嗎？](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md)

### <a name="can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools"></a>我可以使用 PowerShell、CLI 或其他管理工具重新啟動我的快取嗎？
是，適用於 PowerShell 指示看到[tooreboot Redis 快取](cache-howto-manage-redis-cache-powershell.md#to-reboot-a-redis-cache)。

### <a name="what-pricing-tiers-can-use-hello-reboot-functionality"></a>哪些定價層可以使用 hello 重新開機功能嗎？
重新啟動適用於所有定價層。

## <a name="schedule-updates"></a>更新排程
hello**更新排程**刀鋒視窗可讓您 toodesignate Premium 層快取的維護視窗。 當指定 hello 維護視窗時，Redis 伺服器的任何更新都會在此期間。 

> [!NOTE] 
> hello 維護視窗適用於僅 tooRedis 伺服器更新，並不 tooany Azure 更新或更新 toohello 作業系統 hello vm 的主機 hello 快取。
> 
> 

![更新排程](./media/cache-administration/redis-schedule-updates.png)

toospecify 維護視窗中，檢查所需的 hello 天 hello 維護視窗開始時間的每一天，並指定按一下**確定**。 請注意，hello 維護視窗時間-utc 時區。 

> [!NOTE]
> 更新 hello 預設維護視窗是 5 小時。 這個值不是可從 hello Azure 入口網站設定，但您可以設定它在 PowerShell 中使用 hello `MaintenanceWindow` hello 參數[新增 AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry) cmdlet。 如需詳細資訊，請參閱[我可以使用 PowerShell、CLI 或其他管理工具管理排程更新嗎？](#can-i-manage-scheduled-updates-using-powershell-cli-or-other-management-tools)
> 
> 

## <a name="schedule-updates-faq"></a>排程更新常見問題集
* [更新時如果我沒有將 hello 排程更新功能？](#when-do-updates-occur-if-i-dont-use-the-schedule-updates-feature)
* [Hello 期間所做的更新類型排程維護視窗嗎？](#what-type-of-updates-are-made-during-the-scheduled-maintenance-window)
* [我可以使用 PowerShell、CLI 或其他管理工具管理排程更新嗎？](#can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools)
* [哪些定價層可以使用 hello 排程更新的功能嗎？](#what-pricing-tiers-can-use-the-schedule-updates-functionality)

### <a name="when-do-updates-occur-if-i-dont-use-hello-schedule-updates-feature"></a>更新時如果我沒有將 hello 排程更新功能？
如果您未指定維護期間，隨時都可進行更新。

### <a name="what-type-of-updates-are-made-during-hello-scheduled-maintenance-window"></a>Hello 期間所做的更新類型排程維護視窗嗎？
只有 Redis 的伺服器 hello 排程的維護期間進行更新。 hello 維護視窗不會套用 tooAzure 更新，或更新 toohello VM 的作業系統。

### <a name="can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools"></a>我可以使用 PowerShell、CLI 或其他管理工具管理排程更新嗎？
是，您可以管理您使用下列 PowerShell 指令程式的 hello 的排程的更新：

* [Get-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/get-azurermrediscachepatchschedule)
* [New-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/new-azurermrediscachepatchschedule)
* [New-AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry)
* [Remove-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/remove-azurermrediscachepatchschedule)

### <a name="what-pricing-tiers-can-use-hello-schedule-updates-functionality"></a>哪些定價層可以使用 hello 排程更新的功能嗎？
hello**更新排程**功能僅供以 hello premium 定價層。

## <a name="next-steps"></a>後續步驟
* 瀏覽 [Azure Redis 快取進階層](cache-premium-tier-intro.md) 功能。

