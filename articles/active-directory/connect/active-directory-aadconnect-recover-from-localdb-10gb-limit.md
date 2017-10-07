---
title: "Azure AD Connect： 如何限制來自 LocalDB 10GB toorecover 問題 |Microsoft 文件"
description: "本主題描述如何 toorecover Azure AD Connect 同步處理服務遇到 LocalDB 10 GB 時限制問題。"
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 41d081af-ed89-4e17-be34-14f7e80ae358
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 7b8ce6e19b68837639017bb0315eda4b924d525a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-how-toorecover-from-localdb-10-gb-limit"></a>Azure AD Connect： 如何 toorecover 從 LocalDB 10 GB 的限制
Azure AD Connect 需要 SQL Server 資料庫 toostore 識別資料。 您可以使用 SQL Server 2012 Express LocalDB 安裝 Azure AD Connect 與 hello 預設值，或使用完整的 SQL。 SQL Server Express 會實行 10 GB 的大小限制。 使用 LocalDB 且達到這個限制時，Azure AD Connect 同步處理服務無法再啟動或正確同步處理。 本文章提供 hello 復原步驟。

## <a name="symptoms"></a>徵兆
有兩個常見的徵兆︰

* Azure AD Connect 同步處理服務**執行**但無法與 toosynchronize *"停止-資料庫-磁碟-full"*錯誤。

* Azure AD Connect 同步處理服務**是無法 toostart**。 當您嘗試 toostart hello 服務時，它會因 6323 事件和錯誤訊息*"hello 伺服器發生錯誤，因為 SQL Server 已用完磁碟空間。 」*

## <a name="short-term-recovery-steps"></a>短期復原步驟
本節提供所需的 Azure AD Connect 同步處理服務 tooresume 作業 hello 步驟 tooreclaim DB 空間。 hello 步驟包括：
1. [判斷 hello 同步處理服務狀態](#determine-the-synchronization-service-status)
2. [壓縮 hello 資料庫](#shrink-the-database)
3. [刪除執行記錄資料](#delete-run-history-data)
4. [縮短執行歷程記錄資料的保留期間](#shorten-retention-period-for-run-history-data)

### <a name="determine-hello-synchronization-service-status"></a>判斷 hello 同步處理服務狀態
首先，判斷是否 hello 同步處理服務仍在執行或無法：

1. 登入 tooyour Azure AD Connect 的伺服器系統管理員身分。

2. 跳過**服務控制管理員**。

3. 檢查 hello 狀態**Microsoft Azure AD Sync**。


4. 如果它正在執行，不要停止或重新啟動 hello 服務。 略過[壓縮 hello 資料庫](#shrink-the-database)步驟並移過[刪除執行記錄資料](#delete-run-history-data)步驟。

5. 如果未執行，請嘗試 toostart hello 服務。 如果 hello 服務成功啟動，請略過[壓縮 hello 資料庫](#shrink-the-database)步驟並移過[刪除執行記錄資料](#delete-run-history-data)步驟。 否則，請繼續[壓縮 hello 資料庫](#shrink-the-database)步驟。

### <a name="shrink-hello-database"></a>壓縮 hello 資料庫
使用 hello 壓縮作業 toofree 向上足夠 DB 空間 toostart hello 同步處理服務。 它會釋放資料庫空間 hello 資料庫中移除空白字元。 這個步驟是最佳方式，因為不保證一律可以復原空間。 進一步了解壓縮作業 toolearn 閱讀此文章[壓縮資料庫](https://msdn.microsoft.com/library/ms189035.aspx)。

> [!IMPORTANT]
> 如果您可以取得 hello 同步處理服務 toorun，略過此步驟。 因為它會導致因為 tooincreased 片段 toopoor 效能不建議 tooshrink hello SQL DB。

建立 Azure AD Connect 的 hello 資料庫 hello 名稱**ADSync**。 tooperform 壓縮作業，您必須登入為 hello sysadmin 或 hello 資料庫的 DBO。 Azure AD Connect 在安裝期間，下列帳戶的 hello 被授與系統管理員權限：
* 本機系統管理員
* hello 使用者帳戶已使用的 toorun Azure AD Connect 的安裝。
* hello 做為 hello 運作的 Azure AD Connect 同步處理服務內容的同步處理服務帳戶。
* 本機群組已在安裝期間建立的 ADSyncAdmins hello。

1. 藉由複製 hello 資料庫**ADSync.mdf**和**ADSync_log.ldf**檔案位於`%ProgramFiles%\program files\Microsoft Azure AD Sync\Data`tooa 安全的位置。

2. 啟動新的 PowerShell 工作階段。

3. 瀏覽 toofolder `%ProgramFiles%\Program Files\Microsoft SQL Server\110\Tools\Binn`。

4. 啟動**sqlcmd**公用程式執行 hello 命令`./SQLCMD.EXE -S “(localdb)\.\ADSync” -U <Username> -P <Password>`、 使用 hello 認證的 sysadmin 或 hello 資料庫 DBO。

5. 在提示字元中 sqlcmd hello tooshrink hello 資料庫 (1 >)，輸入`DBCC Shrinkdatabase(ADSync,1);`，後面接著`GO`hello 下一行中。

6. 如果 hello 作業成功，請再試一次 toostart hello 同步處理服務。 如果您可以啟動 hello 同步處理服務，請移至太[刪除執行記錄資料](#delete-run-history-data)步驟。 否則請連絡支援人員。

### <a name="delete-run-history-data"></a>刪除執行記錄資料
根據預設，Azure AD Connect 會向上 tooseven 天份的執行歷程記錄資料保留。 在此步驟中，我們會刪除 hello 執行歷程記錄資料 tooreclaim DB 空間，讓 Azure AD Connect 同步處理服務可以啟動同步處理一次。

1.  啟動**同步處理服務管理員**移 tooSTART → 所同步處理服務。

2.  移 toohello**作業** 索引標籤。

3.  選取 [動作] 下方的 [清除執行]...

4.  您可以選擇 [清除所有執行] 或 [清除之前的執行...]**<date>** 選項。 建議您一開始先清除執行超過兩天的歷程記錄資料。 如果您繼續 toorun 進入資料庫大小問題，然後選擇 hello**清除所有執行**選項。

### <a name="shorten-retention-period-for-run-history-data"></a>縮短執行歷程記錄資料的保留期間
這個步驟是 tooreduce hello 可能性的多個同步處理循環之後執行 hello 10 GB 限制的問題。

1. 開啟新的 PowerShell 工作階段。

2. 執行`Get-ADSyncScheduler`並記下 hello PurgeRunHistoryInterval 屬性，指定 hello 目前保留期限。

3. 執行`Set-ADSyncScheduler -PurgeRunHistoryInterval 2.00:00:00`tooset hello 保留週期 tootwo 天數。 調整為適當的 hello 保留期限。

## <a name="long-term-solution--migrate-toofull-sql"></a>長期解決方案 – 移轉 toofull SQL
一般而言，稍有差異，10 GB 的資料庫大小不再足以讓 Azure AD Connect toosynchronize hello 問題是您在內部部署 Active Directory tooAzure AD。 建議您先切換 toousing hello 完整版的 SQL server。 您無法直接將 hello hello 完整版本的 SQL 資料庫 hello LocalDB 的現有 Azure AD Connect 部署取代。 相反地，您必須部署新的 Azure AD Connect 伺服器 hello 完整版本的 SQL。 建議您迴旋移轉 hello 新 Azure AD Connect 的伺服器 （搭配 SQL DB) 做為執行的伺服器，下一步 toohello 現有 Azure AD Connect 的伺服器 （含有 LocalDB) 中的部署。 
* 如需如何 tooconfigure 遠端的 SQL 搭配 Azure AD Connect，請參閱指示 tooarticle[的 Azure AD Connect 自訂安裝](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom)。
* 如需 Azure AD Connect 升級迴旋移轉的指示，請參閱 tooarticle [Azure AD Connect： 從先前版本 toohello 最新升級](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version#swing-migration)。

## <a name="next-steps"></a>後續步驟
深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。
