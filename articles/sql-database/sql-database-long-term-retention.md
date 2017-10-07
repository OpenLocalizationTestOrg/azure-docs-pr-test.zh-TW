---
title: "總 too10 年的 aaaStore Azure SQL Database 備份 |Microsoft 文件"
description: "了解 Azure SQL Database 支援儲存備份的 too10 年的方式。"
keywords: 
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 66fdb8b8-5903-4d3a-802e-af08d204566e
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/22/2016
ms.author: sashan
ms.openlocfilehash: 5825ebd4e3bd66b59b13aea603d377ef814a1df3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="store-azure-sql-database-backups-for-up-too10-years"></a>儲存註冊 too10 年的 Azure SQL Database 備份
許多應用程式有法規，相容性或其他商務用途，需要 tooretain 資料庫備份，超出 hello Azure SQL Database 所提供的 7-35 天[自動備份](sql-database-automated-backups.md)。 使用 hello 長期備份保留功能，您可以向上 too10 年的 Azure 復原服務保存庫中儲存您的 SQL 資料庫備份。 您可以儲存長達 too1，000 資料庫每個保存庫。 然後，您可以選取任何備份在 hello 保存庫 toorestore 它做為新的資料庫。

> [!IMPORTANT]
> 長期備份的保留為目前處於預覽狀態，並提供下列區域的 hello： 澳洲東部、 澳洲東南部、 巴西南部、 美國中部、 東亞、 美國東部、 美國東部 2、 印度中部、 印度南部、 日本東部、 日本西部、 美國中北部、 North歐洲、 中南部、 東南亞、 西歐、 和美國西部。
>

> [!NOTE]
> 您可以在 24 小時期間內啟用 too200 資料庫，每個保存庫。 我們建議您針對這項限制每個伺服器 toominimize hello 影響使用不同的保存庫。 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a>SQL Database 長期備份保留的運作方式

使用長期備份保留可以建立 SQL Database 伺服器與 Azure 復原服務保存庫的關聯。 

* 您必須建立 hello 保存庫在 hello 相同 Azure 訂用帳戶建立 hello SQL server，並在 hello 相同地理區域和資源群組。 
* 接著，您可以針對任何資料庫設定保留原則。 hello 原則原因 hello 每週完整資料庫備份 toobe 複製 toohello 復原服務保存庫，並保留 hello 指定的保留週期 （向上 too10 年）。 
* 然後，您就可以從這些備份 tooa 新的資料庫中任何伺服器 hello 訂用帳戶中的任何還原 hello 資料庫。 Azure 儲存體從現有的備份，建立複本並 hello 複製 hello 現有資料庫上具有任何效能影響。

> [!TIP]
> Tooguide 如何，請參閱[設定與還原自 Azure SQL Database 的長期備份保留](sql-database-long-term-backup-retention-configure.md)。

## <a name="enable-long-term-backup-retention"></a>啟用長期備份保留

tooconfigure 長期的備份保留的資料庫：

1. 建立 Azure 復原服務保存庫在 hello 與 SQL 資料庫伺服器相同的地區、 訂用帳戶和資源群組。 
2. 註冊 hello 伺服器 toohello 保存庫。
3. 建立 Azure 復原服務保護原則。
4. 適用於 hello 保護原則 toohello 資料庫需要長期備份的保留。

tooconfigure，管理，並還原 Azure 復原服務保存庫中的自動備份的長期備份保留的資料庫，執行 hello 下列其中一項：

* 使用 hello Azure 入口網站： 按一下**長期備份的保留**，選取 [資料庫]，然後按一下**設定**。 

   ![選取進行長期備份保留的資料庫](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* 使用 PowerShell： 跳過[設定與還原自 Azure SQL Database 的長期備份保留](sql-database-long-term-backup-retention-configure.md)。

## <a name="restore-a-database-thats-stored-with-hello-long-term-backup-retention-feature"></a>還原資料庫儲存的 hello 長期備份保留的功能

從長期的備份保留備份 toorecover:

1. Hello 備份儲存位置清單 hello 保存庫。
2. 是對應的 tooyour 邏輯伺服器的清單 hello 容器。
3. 清單 hello hello 保存庫所對應的 tooyour 資料庫內的資料來源。
4. 會使用 toorestore 清單 hello 復原點。
5. Hello 從還原資料庫 hello 復原點 toohello 您訂用帳戶內的目標伺服器。

tooconfigure，管理，並還原 Azure 復原服務保存庫中的自動備份的長期備份保留的資料庫，執行 hello 下列其中一項：

* 使用 hello Azure 入口網站： 跳過[長期備份保留使用管理 hello Azure 入口網站](sql-database-long-term-backup-retention-configure.md)。 

* 使用 PowerShell： 跳過[管理使用 PowerShell 的長期備份保留](sql-database-long-term-backup-retention-configure.md)。

## <a name="get-pricing-for-long-term-backup-retention"></a>取得長期備份保留的價格

SQL database 的長期備份保留負責根據 toohello[定價率的 Azure 備份服務](https://azure.microsoft.com/pricing/details/backup/)。

Hello SQL 資料庫伺服器已註冊的 toohello 保存庫之後，您必須支付 hello hello 每週備份儲存在 hello 保存庫使用的總儲存。

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a>檢視以長期備份保留儲存的可用備份

tooconfigure，會管理，並使用 hello Azure 入口網站的 Azure 復原服務保存庫中的自動備份的長期備份保留還原的資料庫，執行 hello 下列其中一項：

* 使用 hello Azure 入口網站： 跳過[長期備份保留使用管理 hello Azure 入口網站](sql-database-long-term-backup-retention-configure.md)。 

* 使用 PowerShell： 跳過[管理使用 PowerShell 的長期備份保留](sql-database-long-term-backup-retention-configure.md)。

## <a name="disable-long-term-retention"></a>停用長期保留

hello 復原服務會自動處理 hello 清除的 hello 提供保留原則為基礎的備份。 

toostop 傳送嗨備份特定資料庫 toohello 保存庫中，移除該資料庫的 hello 保留原則。
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> 已經在 hello 保存庫中的 hello 備份不受影響。 會自動刪除由 hello 復原服務的保留期限到期時。

## <a name="long-term-backup-retention-faq"></a>長期備份保留常見問題集

**我可以手動刪除 hello 保存庫中的特定備份嗎？**

目前不支援。 hello 保存庫會 hello 保留期限已過期時，會自動清除備份。

**可以註冊一個保存庫與 my server toostore 備份 toomore 嗎？**

否，您可以一次目前儲存備份 tooonly 一個保存庫。

**我可以在不同的訂用帳戶中有保存庫與伺服器嗎？**

否，目前 hello 保存庫和伺服器必須位在 hello 相同的訂用帳戶和資源群組。

**我可以使用在不同於伺服器區域的區域中建立的保存庫嗎？**

否，hello 保存庫和伺服器必須在 hello 相同區域 toominimize 複製時間並避免流量費用。

**我可以在一個保存庫中儲存幾個資料庫？**

目前，我們支援 too1，000 資料庫每個保存庫註冊。 

**每個訂用帳戶可以建立幾個保存庫？**

您可以建立每個訂閱 too25 保存庫註冊。

**每個保存庫每天可以設定幾個資料庫？**

每個保存庫每天最多可以設定 200 個資料庫。

**長期備份保留是否可與彈性集區搭配運作？**

是。 Hello 集區中的任何資料庫可以具有 hello 保留原則設定。

**可以選擇 hello 備份建立 hello 時間嗎？**

否，SQL Database 控制 hello 備份排程 toominimize hello 對效能影響您的資料庫。

**我的資料庫啟用了透明資料加密。我可以使用它與 hello 保存庫？** 

是，支援透明資料加密。 即使 hello 原始資料庫不存在，您可以從 hello 保存庫還原 hello 資料庫。

**發生什麼情況與 hello 保存庫中的 hello 備份我的訂用帳戶已暫止？** 

如果您的訂用帳戶已暫止，我們會保留 hello 現有的資料庫和備份。 新的備份不會複製的 toohello 保存庫。 您重新啟動 hello 訂用帳戶之後，hello 服務會繼續複製備份 toohello 保存庫。 您的保存庫會使用 hello 訂用帳戶暫止之前那里複製的 hello 備份變成可存取 toohello 還原作業。 

**可以取得存取 toohello SQL 資料庫的備份檔案，我可以下載，或將它們還原 toohello SQL 伺服器？**

否，目前無法。

**它是可能 toohave SQL 保留原則內多個排程每日、 每週、 每月 （每年）。**

否，目前僅虛擬機器備份提供多個排程。

**如果我們在使用中的異地複寫次要資料庫上設定長期備份保留，會發生什麼情況？**

因為複本不留備份，所以目前沒有在次要資料庫上進行長期備份保留的選項。 不過，最好向上作用中地理複寫的次要資料庫上的長期備份保留使用者 tooset 基於這些理由：
* 當發生容錯移轉時 hello 資料庫會變成主要資料庫，我們進行完整備份，也就是上傳的 toovault。
* 沒有不需額外成本 toohello 客戶設定次要資料庫上的長期備份保留。

## <a name="next-steps"></a>後續步驟
因為資料庫備份可保護資料免於意外損毀或刪除，是商務持續性和災害復原策略中不可或缺的一環。 toolearn hello 其他 SQL Database 業務持續性解決方案，請參閱[商務持續性概觀](sql-database-business-continuity.md)。
