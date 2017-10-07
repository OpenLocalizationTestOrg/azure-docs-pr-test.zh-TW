---
title: "aaaAzure SQL Database 的自動，異地備援備份 |Microsoft 文件"
description: "SQL Database 每隔幾鐘會自動建立一個本機資料庫備份，並使用 Azure 讀取權限異地備援儲存體來進行異地備援。"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 3ee3d49d-16fa-47cf-a3ab-7b22aa491a8d
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 8aff5356e8142707dd7cd2533a4aa5ea8fec866d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-automatic-sql-database-backups"></a>了解自動 SQL Database 備份

SQL Database 會自動建立資料庫備份，並使用 Azure 讀取存取異地備援儲存體 (RA-GRS) tooprovide 異地備援。 這些備份是自動建立的，且不需額外付費。 您不需要 toodo 任何項目 toomake 它們就會發生的情況。 資料庫備份可保護資料免於意外損毀或刪除，是商務持續性和災害復原策略中不可或缺的一部分。 如果您想 tookeep 備份您的儲存體容器中，您可以設定長期的備份保留原則。 如需詳細資訊，請參閱[長期保存](sql-database-long-term-retention.md)。

## <a name="what-is-a-sql-database-backup"></a>什麼是 SQL Database 備份？

SQL Database 會使用 SQL Server 技術 toocreate[完整](https://msdn.microsoft.com/library/ms186289.aspx)，[差異](https://msdn.microsoft.com/library/ms175526.aspx)，和[交易記錄檔](https://msdn.microsoft.com/library/ms191429.aspx)備份。 hello 交易記錄備份通常會每隔 5-10 分鐘，以根據 hello 效能層級和資料庫活動量的 hello 頻率發生問題。 交易記錄備份，使用完整和差異備份，可讓您 toorestore 資料庫 tooa 特定時間點 toohello 裝載 hello 資料庫的同一部伺服器。 當您還原資料庫時，hello 服務的完整、 差異及交易記錄備份需要還原 toobe 的數字。


您可以使用這些備份︰

* 還原資料庫 tooa 在時間點 hello 保留期限內。 這項作業會建立新的資料庫在 hello 與 hello 原始資料庫相同的伺服器。
* 還原已刪除的資料庫 toohello 時間或 hello 保留期限內的任何時間。 hello 刪除資料庫只能還原在 hello hello 原始資料庫建立所在的同一部伺服器。
* 還原資料庫 tooanother 地理區域。 這可讓您從地理災害 toorecover 時您無法存取您的伺服器和資料庫。 Hello 世界各地的任何現有伺服器建立新的資料庫。 
* 從 Azure 復原服務保存庫中儲存的特定備份中還原資料庫。 這可讓您 toorestore 較舊版本的 hello 資料庫 toosatisfy 規範要求或 toorun hello 應用程式的舊版本。 請參閱[長期保留](sql-database-long-term-retention.md)。
* tooperform 還原，請參閱[從備份還原資料庫](sql-database-recovery-using-backups.md)。

> [!NOTE]
> 在 Azure 儲存體，hello 詞彙*複寫*參考從一個位置 tooanother toocopying 檔案。 SQL 的*資料庫複寫*參考 tookeeping toomultiple 次要資料庫與主要資料庫同步處理。 
> 

## <a name="how-much-backup-storage-is-included-at-no-cost"></a>在免費情況下包含多少備份儲存體？
SQL Database 提供最大佈建的資料庫儲存體 too200%做為備份儲存體不需要額外成本。 例如，如果您擁有可佈建 DB 大小為 250 GB 的標準 DB 執行個體，您就能免費獲得 500 GB 的備份儲存體。 如果您的資料庫超過 hello 提供備份儲存體，您可以透過連絡 Azure 支援人員選擇 tooreduce hello 保留期限。 另一個選項是 toopay 計費費率 hello 標準讀取權限地理備援儲存體 (RA-GRS) 的額外備份存放區。 

## <a name="how-often-do-backups-happen"></a>備份頻率是？
每週進行一次完整備份，通常每幾個小時進行一次差異資料庫備份，以及通常每隔 5 - 10 分鐘進行一次交易記錄備份。 建立資料庫之後，立即排定 hello 的第一個完整備份。 30 分鐘內，通常完成，但極大的 hello 資料庫時可能需要較長。 比方說，hello 初始備份可能需要較長，已還原的資料庫或資料庫複本上。 Hello 第一個完整備份之後，所有進一步的備份均已排程自動並 hello 背景中以無訊息方式管理。 hello 確切的時間，所有的資料庫備份的由 hello SQL Database 服務，因為它平衡 hello 整體系統工作負載。 

hello 備份儲存體地理複寫是根據 hello Azure 儲存體複寫排程。

## <a name="how-long-do-you-keep-my-backups"></a>您會保留我的備份多久？
每個 SQL Database 備份具有保留期間，取決於 hello[服務層](sql-database-service-tiers.md)的 hello 資料庫。 資料庫中的 hello 保留期限:


* 基本服務層為 7 天。
* 標準服務層為 35 天。
* 進階服務層為 35 天。

如果您降級 hello Standard 或 Premium 服務層 tooBasic 資料庫之後，hello 備份會儲存七天。 所有超過 7 天的現有備份都無法再使用。 

如果您是從 hello 基本服務層 tooStandard 或 Premium 升級您的資料庫，SQL Database 會保留現有的備份前 35 天。 它也會將新的備份自其建立日期算起保存 35 天。

如果您刪除資料庫時，SQL Database 會保留 hello 的 hello 備份一樣線上資料庫的方式相同。 例如，假設您刪除保存期限為 7 天的「基本」資料庫。 已保存 4 天的備份會再保存 3 天。

> [!IMPORTANT]
> 如果您刪除 hello Azure SQL server 裝載 SQL 資料庫，也會一併刪除屬於 toohello 伺服器的所有資料庫，且無法復原。 您無法還原已刪除的伺服器。
> 

## <a name="how-tooextend-hello-backup-retention-period"></a>如何 tooextend hello 備份保留期限嗎？
如果您的應用程式需要較長一段時間的 hello 備份可供使用您可以藉由設定個別資料庫 （LTR 原則） 的 hello 長期備份保留原則擴充 hello 內建的保留期限。 這可讓您從 35 天 tooup too10 年的 tooextend hello 建置 it 保留期限。 如需詳細資訊，請參閱[長期保存](sql-database-long-term-retention.md)。

一旦您加入 hello LTR 原則 tooa 資料庫使用 Azure 入口網站或應用程式開發介面，hello 每週的完整資料庫備份將不會自動複製的 tooyour 擁有 Azure 備份服務保存庫。 如果您的資料庫已加密與 TDE hello 備份會自動加密在靜止。  hello 服務保存庫會自動刪除您已過期的備份，根據其時間戳記和 hello LTR 原則。  因此您不需要 toomanage hello 備份排程或擔心 hello 清除 hello 舊的檔案。 儲存在 hello 的備份保存庫，只要 hello 保存庫中的 hello 還原應用程式開發介面支援 hello 與您的 SQL 資料庫的相同訂用帳戶。 您可以使用 hello Azure 入口網站或 PowerShell tooaccess 這些備份。

> [!TIP]
> Tooguide 如何，請參閱[設定與還原自 Azure SQL Database 的長期備份保留](sql-database-long-term-backup-retention-configure.md)
>

## <a name="are-backups-encrypted"></a>備份經過加密？

Azure SQL 資料庫啟用 TDE 時，也會加密備份。 所有新的 Azure SQL Database 預設都會設定為啟用 TDE。 如需 TDE 的詳細資訊，請參閱 [Azure SQL Database 的透明資料加密](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)。

## <a name="next-steps"></a>後續步驟

- 資料庫備份可保護資料免於意外損毀或刪除，是商務持續性和災害復原策略中不可或缺的一部分。 toolearn hello 其他 Azure SQL Database 業務持續性解決方案，請參閱[商務持續性概觀](sql-database-business-continuity.md)。
- toorestore tooa 的時間點使用 hello Azure 入口網站，請參閱[時間使用 hello Azure 入口網站中還原資料庫 tooa 點](sql-database-recovery-using-backups.md)。
- toorestore tooa 的時間點使用 PowerShell，請參閱[還原時間使用 PowerShell 資料庫 tooa 點](scripts/sql-database-restore-database-powershell.md)。
- tooconfigure，管理和還原的使用 hello Azure 復原服務保存庫中的自動備份的長期保存從 Azure 入口網站，請參閱[長期備份保留使用管理 hello Azure 入口網站](sql-database-long-term-backup-retention-configure.md)。
- tooconfigure，管理，並從長期保存使用 PowerShell 的 Azure 復原服務保存庫中的自動備份的還原，請參閱[管理使用 PowerShell 的長期備份保留](sql-database-long-term-backup-retention-configure.md)。
