---
title: "Azure 入口網站︰SQL Database 異地複寫 | Microsoft Docs"
description: "針對 Azure SQL Database 設定地理複寫 hello Azure 入口網站和起始容錯移轉"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d0b29822-714f-4633-a5ab-fb1a09d43ced
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/06/2016
ms.author: carlrab
ms.openlocfilehash: 09cbbdb040f36c42593e3be87ce6db2238f36656
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-hello-azure-portal-and-initiate-failover"></a>在 hello Azure 入口網站和起始容錯移轉中，設定 Azure SQL database 的作用中地理複寫

本文章將示範如何 tooconfigure 作用中地理複寫 SQL database 中 hello [Azure 入口網站](http://portal.azure.com)和 tooinitiate 容錯移轉。

tooinitiate 容錯移轉以 hello Azure 入口網站，請參閱[for Azure SQL Database 起始計劃性或非計劃性容錯移轉以 hello Azure 入口網站](sql-database-geo-replication-portal.md)。

tooconfigure 作用中地理複寫使用 hello Azure 入口網站，您需要下列資源的 hello:

* Azure SQL database: hello 的 tooreplicate tooa 不同的地理區域的主要資料庫。

> [!Note]
作用中地理複寫必須是資料庫在 hello 之間相同訂用帳戶。

## <a name="add-a-secondary-database"></a>新增次要資料庫
hello 下列步驟會建立新的次要資料庫以進行異地複寫合作關係。  

tooadd 次要資料庫，您必須是 hello 訂用帳戶擁有者或共同擁有者。

hello 次要資料庫名稱為 hello 主要資料庫相同的 hello 且具有，根據預設，hello 相同服務層級。 hello 次要資料庫可以是單一資料庫或彈性集區中的資料庫。 如需詳細資訊，請參閱 [服務層](sql-database-service-tiers.md)。
建立並植入次要 hello 後，資料就會開始從 hello 主要資料庫 toohello 新的次要資料庫複寫。

> [!NOTE]
> 如果 hello 夥伴資料庫已經存在 （例如，由於結束先前的地理複寫關聯性） hello 命令將會失敗。
> 

1. 在 hello [Azure 入口網站](http://portal.azure.com)，瀏覽您要進行地理複寫 tooset toohello 資料庫。
2. 在 hello SQL 資料庫 頁面上，選取 **地理複寫**，然後選取 hello 區域 toocreate hello 次要資料庫。 您可以選取任何區域以外 hello 區域裝載 hello 主要資料庫，但我們建議 hello[配對的區域](../best-practices-availability-paired-regions.md)。
   
    ![設定異地複寫](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. 選取或設定伺服器 hello 和 hello 次要資料庫的定價層。
   
    ![設定次要資料庫](./media/sql-database-geo-replication-portal/create-secondary.png)
4. （選擇性） 您可以新增次要資料庫的 tooan 彈性集區。 toocreate hello 次要資料庫在資料庫中，按一下**彈性集區**選取 hello 目標伺服器上的集區。 集區必須已經存在 hello 目標伺服器上。 此工作流程不會建立集區。
5. 按一下**建立**tooadd hello 次要。
6. hello 次要資料庫會建立而且 hello 植入處理程序開始。
   
    ![設定次要資料庫](./media/sql-database-geo-replication-portal/seeding0.png)
7. Hello 植入處理程序完成時，hello 次要資料庫就會顯示其狀態。
   
    ![植入完成](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a>起始容錯移轉

hello 次要資料庫可以是主要的交換的 toobecome hello。  

1. 在 hello [Azure 入口網站](http://portal.azure.com)，瀏覽 toohello hello 地理複寫合作關係中的主要資料庫。
2. 在 hello SQL 資料庫刀鋒視窗中，選取 **所有設定** > **地理複寫**。
3. 在 hello**次要**清單時，要產生 toobecome 選取 hello 資料庫 hello 新主要複本，然後按一下**容錯移轉**。
   
    ![容錯移轉](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. 按一下**是**toobegin hello 容錯移轉。

hello 命令立即會切換成主要角色的 hello hello 次要資料庫。 

沒有在短期間這兩個資料庫是無法使用 （在 0 too25 秒 hello 順序） 而 hello 角色切換。 如果 hello 主要資料庫中有多個次要資料庫、 hello 命令自動檔重新設定 hello 其他次要 tooconnect toohello 新主要複本。 hello 整個作業花費時間小於一分鐘 toocomplete 在一般情況下。 

> [!NOTE]
> 此命令可供快速地復原 hello 資料庫發生中斷。 它會觸發容錯移轉但不進行資料同步 (強制性容錯移轉)。  如果主要 hello 在線上而且 hello 命令發出部分資料遺失時認可交易可能會發生。 
> 
> 

## <a name="remove-secondary-database"></a>移除次要資料庫
這項作業永久終止 hello 複寫 toohello 次要資料庫，並變更 hello hello 次要 tooa 規則讀寫資料庫的角色。 如果 hello 連線 toohello 次要資料庫已損毀，hello 命令成功，但連線恢復後 hello 次要並不會變成讀寫之前。  

1. 在 hello [Azure 入口網站](http://portal.azure.com)，瀏覽 toohello hello 地理複寫合作關係中的主要資料庫。
2. 在 hello SQL 資料庫 頁面上，選取 **地理複寫**。
3. 在 hello**次要**清單中，您想要從 hello 地理複寫合作關係 tooremove 選取 hello 資料庫。
4. 按一下 [ **停止複寫**]。
   
    ![移除次要](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. 隨即開啟確認視窗。 按一下**是**tooremove hello 資料庫從 hello 地理複寫合作關係。 （設定它 tooa 讀寫資料庫不屬於任何複寫的一部分）。

## <a name="next-steps"></a>後續步驟
* toolearn 進一步了解作用中的地理複寫，請參閱[作用中地理複寫](sql-database-geo-replication-overview.md)。
* 如需商務持續性概觀和案例，請參閱 [商務持續性概觀](sql-database-business-continuity.md)。

