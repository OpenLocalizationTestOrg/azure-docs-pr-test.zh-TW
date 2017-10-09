---
title: "Azure Redis 快取的 aaaHow tooconfigure 地理複寫 |Microsoft 文件"
description: "了解如何 tooreplicate Azure Redis 快取執行個體跨地理區域。"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 375643dc-dbac-4bab-8004-d9ae9570440d
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: sdanie
ms.openlocfilehash: edcd6f202b51055d1a4e47ecaf11f9977d50aa81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-geo-replication-for-azure-redis-cache"></a>如何針對 Azure Redis 快取 tooconfigure 地理複寫

異地複寫提供一個機制，可供連結兩個高階層 Azure Redis 快取執行個體。 一個快取指定為 hello 主要的連線快取，而 hello hello 次要連結快取為其他。 hello 次要連結快取會變成唯讀的並寫入的 toohello 主要快取的資料複寫 toohello 次要連結快取。 這項功能可以跨 Azure 區域是使用的 tooreplicate 快取。 本文章提供您高階層 Azure Redis 快取執行個體的指南 tooconfiguring 地理複寫。

## <a name="geo-replication-prerequisites"></a>異地複寫的必要條件

必須符合 tooconfigure 地理複寫之間兩個快取，hello 下列必要條件：

- 這兩個快取必須是[高階層](cache-premium-tier-intro.md)快取。
- 這兩個快取必須在 hello 相同的 Azure 訂用帳戶。
- hello 次要連結快取必須是可以 hello 相同定價層或更大的定價層，比 hello 主要連結快取。
- Hello 次要連結快取 hello 主要連結快取已啟用叢集，如果以 hello 啟用叢集必須有相同數目的分區，做為 hello 主要連結快取。
- 必須建立兩個快取並同時處於執行中狀態。
- 任何一個快取上皆不能啟用持續性。
- Hello 支援相同的 VNET 中的快取之間的地理複寫。 也支援在不同的 Vnet 中的快取之間的地理複寫，只要 hello 兩個 Vnet 設定的方式 hello Vnet 中的資源都可以 tooreach 彼此透過 TCP 連線。

設定異地複寫後，hello 下列限制適用於 tooyour 連結的快取組：

- hello 次要連結快取是唯讀的。您可以讀取它，但您無法寫入任何資料 tooit。 
- 會移除任何加入 hello 連結之前已在 hello 次要連結快取中的資料。 Hello 地理複寫之後移除不過，如果 hello 複寫 hello 次要連結快取中的資料仍會保留。
- 無法起始[調整大小作業](cache-how-to-scale.md)任一個快取或[變更 hello 分區數目](cache-how-to-premium-clustering.md)如果 hello 快取已啟用叢集。
- 您無法啟用任一個快取的持續性。
- 您可以使用[匯出](cache-how-to-import-export-data.md#export)任一個快取，但是您可以只[匯入](cache-how-to-import-export-data.md#import)到主要 hello 連結快取。
- 您無法刪除連結的快取或包含它們，直到您移除 hello 異地複寫連結的 hello 資源群組。 如需詳細資訊，請參閱[未 hello 作業失敗的原因當我嘗試 toodelete 我連結的快取？](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)
- 如果 hello 兩個快取是在不同的區域中，網路輸出費用將會套用跨區域 toohello 次要連結快取複寫 toohello 資料。 如需詳細資訊，請參閱[多少作用成本 tooreplicate 我的資料跨 Azure 區域？](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)
- 沒有自動容錯移轉 toohello 次要連結快取如果 hello 主要快取 （和其複本） 當機。 順序 toofailover 用戶端應用程式，您會需要 toomanually 移除 hello 異地複寫連結，點 hello 用戶端應用程式 toohello 快取，先前作為 hello 次要連結快取。 如需詳細資訊，請參閱[容錯 toohello 次要連結快取移轉如何運作？](#how-does-failing-over-to-the-secondary-linked-cache-work)

## <a name="add-a-geo-replication-link"></a>新增異地複寫連結

1. toolink 兩個 premium 一起快取的地理複寫中，按一下**地理複寫**hello 主要連結所做的 hello 快取的 hello 資源功能表上，快取，然後再按一下**新增快取複寫連結**從 hello**地理複寫**刀鋒視窗。

    ![新增連結](./media/cache-how-to-geo-replication/cache-geo-location-menu.png)

2. 按一下所需的 hello 次要快取從 hello hello 名稱**相容的快取**清單。 如果您想要的快取未顯示 hello 清單中，確認該 hello[地理複寫必要條件](#geo-replication-prerequisites)的 hello 需要符合次要快取。 toofilter hello 快取，以區域、 按一下 hello 所需的區域中只會快取中 hello hello 對應 toodisplay**相容的快取**清單。

    ![異地複寫相容的快取](./media/cache-how-to-geo-replication/cache-geo-location-select-link.png)
    
    您也可以初始化 hello 使用 hello 操作功能表中連結 hello 次要快取相關的處理程序或檢視詳細資料。

    ![異地複寫操作功能表](./media/cache-how-to-geo-replication/cache-geo-location-select-link-context-menu.png)

3. 按一下**連結**toolink 一起 hello 兩個快取，並開始 hello 複寫程序。

    ![連結快取](./media/cache-how-to-geo-replication/cache-geo-location-confirm-link.png)

4. 您可以檢視 hello 進度 hello 複寫程序上 hello**地理複寫**刀鋒視窗。

    ![連結狀態](./media/cache-how-to-geo-replication/cache-geo-location-linking.png)

    您也可以檢視連結狀態 hello hello**概觀**這兩個 hello 主要和次要快取刀鋒視窗。

    ![快取狀態](./media/cache-how-to-geo-replication/cache-geo-location-link-status.png)

    Hello 複寫程序完成之後，hello**連結狀態**變更太**Succeeded**。

    ![快取狀態](./media/cache-how-to-geo-replication/cache-geo-location-link-successful.png)

    期間 hello 連結程序，hello 主要連結快取仍然可供使用，但 hello 連結程序完成之前，沒有可用 hello 次要連結快取。

## <a name="remove-a-geo-replication-link"></a>移除異地複寫連結

1. 按一下 停止地理複寫中，兩個快取之間 tooremove hello 連結**取消連結的快取**hello 從**地理複寫**刀鋒視窗。
    
    ![取消連結快取](./media/cache-how-to-geo-replication/cache-geo-location-unlink.png)

    Hello 取消連結的程序完成時，hello 次要快取會使用同時讀取和寫入。

>[!NOTE]
>Hello 異地複寫連結中移除時，hello 會從 hello 連結之主要快取仍會留在 hello 次要快取複寫資料。
>
>

## <a name="geo-replication-faq"></a>異地複寫常見問題集

- [可以使用異地複寫搭配標準或基本層快取嗎？](#can-i-use-geo-replication-with-a-standard-or-basic-tier-cache)
- [是可供 hello 連結或取消連結的程序期間使用我的快取？](#is-my-cache-available-for-use-during-the-linking-or-unlinking-process)
- [可以同時連結兩個以上的快取嗎？](#can-i-link-more-than-two-caches-together)
- [可以將不同 Azure 訂用帳戶中的兩個快取加以連結嗎？](#can-i-link-two-caches-from-different-azure-subscriptions)
- [可以將兩個不同大小的快取加以連結嗎？](#can-i-link-two-caches-with-different-sizes)
- [啟用叢集時可以使用異地複寫嗎？](#can-i-use-geo-replication-with-clustering-enabled)
- [可以使用異地複寫搭配 VNET 中的快取嗎？](#can-i-use-geo-replication-with-my-caches-in-a-vnet)
- [可以使用 PowerShell 或 Azure CLI toomanage 地理複寫嗎？](#can-i-use-powershell-or-azure-cli-to-manage-geo-replication)
- [多少成本 tooreplicate 我的資料跨 Azure 區域？](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)
- [為什麼沒有 hello 作業失敗時我已嘗試過 toodelete 我連結的快取？](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)
- [要將次要連結快取用於哪個區域？](#what-region-should-i-use-for-my-secondary-linked-cache)
- [容錯移轉 toohello 次要連結快取的運作方式為何？](#how-does-failing-over-to-the-secondary-linked-cache-work)

### <a name="can-i-use-geo-replication-with-a-standard-or-basic-tier-cache"></a>可以使用異地複寫搭配標準或基本層快取嗎？

否，異地複寫僅適用於高階層快取。

### <a name="is-my-cache-available-for-use-during-hello-linking-or-unlinking-process"></a>是可供 hello 連結或取消連結的程序期間使用我的快取？

- 當連結在一起異地備援的兩個快取，hello 主要連結快取仍然可供使用，但 hello 連結程序完成之前，沒有可用 hello 次要連結快取。
- 當移除兩個快取之間的 hello 異地複寫連結，這兩個快取保持可供使用。

### <a name="can-i-link-more-than-two-caches-together"></a>可以同時連結兩個以上的快取嗎？

否，使用異地複寫時，您只能將兩個快取連結在一起。

### <a name="can-i-link-two-caches-from-different-azure-subscriptions"></a>可以將不同 Azure 訂用帳戶中的兩個快取加以連結嗎？

不行，兩個快取必須在 hello 相同的 Azure 訂用帳戶。

### <a name="can-i-link-two-caches-with-different-sizes"></a>可以將兩個不同大小的快取加以連結嗎？

是，只要 hello 次要連結快取大於 hello 主要連結快取。

### <a name="can-i-use-geo-replication-with-clustering-enabled"></a>啟用叢集時可以使用異地複寫嗎？

是的這兩個快取有 hello 是相同的分區數目。

### <a name="can-i-use-geo-replication-with-my-caches-in-a-vnet"></a>可以使用異地複寫搭配 VNET 中的快取嗎？

是，支援 VNET 中快取的異地複寫。 

- Hello 支援相同的 VNET 中的快取之間的地理複寫。
- 也支援在不同的 Vnet 中的快取之間的地理複寫，只要 hello 兩個 Vnet 設定的方式 hello Vnet 中的資源都可以 tooreach 彼此透過 TCP 連線。

### <a name="can-i-use-powershell-or-azure-cli-toomanage-geo-replication"></a>可以使用 PowerShell 或 Azure CLI toomanage 地理複寫嗎？

此時，您只能管理地理複寫使用 hello Azure 入口網站。

### <a name="how-much-does-it-cost-tooreplicate-my-data-across-azure-regions"></a>多少成本 tooreplicate 我的資料跨 Azure 區域？

使用地理複寫，從 hello 主要連結快取的資料時，複寫的 toohello 次要連結快取。 快取與 hello 如果 hello 兩個連結位於相同的 Azure 區域 hello 資料傳輸不需付費。 如果 hello 兩個連結的快取中不同的 Azure 地區，hello 地理複寫資料傳送費用是 hello 複寫該資料 toohello 其他 Azure 區域的 [頻寬] 費用。 如需詳細資訊，請參閱[頻寬定價詳細資料](https://azure.microsoft.com/pricing/details/bandwidth/)。

### <a name="why-did-hello-operation-fail-when-i-tried-toodelete-my-linked-cache"></a>為什麼沒有 hello 作業失敗時我已嘗試過 toodelete 我連結的快取？

兩個快取連結在一起，您無法刪除快取或 hello 包含這些，直到您移除 hello 異地複寫連結的資源群組。 如果您嘗試 toodelete hello 資源群組，其中包含一或兩個 hello 連結快取、 hello hello 資源群組中的其他資源會被刪除，但 hello 資源群組會停留在 hello`deleting`狀態和任何連結 hello 資源群組中的快取保留在 hello`running`狀態。 中所述，toocomplete hello 刪除 hello 資源群組和 hello 連結內中斷 hello 異地複寫連結，它的快取[移除異地複寫連結](#remove-a-geo-replication-link)。

### <a name="what-region-should-i-use-for-my-secondary-linked-cache"></a>要將次要連結快取用於哪個區域？

一般情況下，建議您在 hello 的快取 tooexist 相同與 hello 存取它的應用程式的 Azure 區域。 如果您的應用程式有主要和後援區域，您的主要和次要快取就應該位於這些相同的區域。 如需配對區域的詳細資訊，請參閱[最佳做法 – Azure 配對的區域](../best-practices-availability-paired-regions.md)。

### <a name="how-does-failing-over-toohello-secondary-linked-cache-work"></a>容錯移轉 toohello 次要連結快取的運作方式為何？

在 hello 初始版本中的地理複寫，Azure Redis 快取不支援自動容錯移轉跨 Azure 區域。 異地複寫主要用於災害復原情節。 在 distater 復原案例中，客戶就可使備份區域中的 hello 整個應用程式堆疊中協調的方式，而不是讓個別的應用程式元件決定何時自行 tooswitch tootheir 備份。 這是 tooRedis 特別有關。 Hello 的主要優點之一是 redis 的它會非常低度延遲存放區。 如果所使用的 Redis 應用程式容錯移轉 tooa 不同 Azure 區域，但是 hello 計算層則否，hello round trip 時間加上效能會有明顯的影響。 基於這個理由，我們希望 tooavoid Redis 失敗透過自動到期，tootransient 可用性問題。

Tooinitiate hello 容錯移轉，目前，當您需要 tooremove hello 地理複寫連結 hello Azure 入口網站中，並從 hello 連結之主要快取 （先前稱為連結） 的 toohello 次要將 hello Redis 用戶端中的 hello 連接端點快取。 當兩個快取會分離，hello hello 複本變成一般再次讀取-寫入快取並接受直接來自 Redis 用戶端要求。


## <a name="next-steps"></a>後續步驟

深入了解 hello [Azure Redis 快取進階層](cache-premium-tier-intro.md)。

