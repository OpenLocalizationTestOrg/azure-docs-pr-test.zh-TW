---
title: "aaaConfigure 災害復原的 Azure SQL Database 安全性 |Microsoft 文件"
description: "本主題說明設定和管理安全性資料庫還原或容錯移轉 tooa 中的次要伺服器 hello 事件的資料中心中斷或其他災害後的安全性考量"
services: sql-database
documentationcenter: na
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: c7c898c9-69d4-4e16-8b7e-720bbb3353dd
ms.service: sql-database
ms.custom: business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 10/13/2016
ms.author: sashan
ms.openlocfilehash: c3172568e1b8ad2a53958200aa6cf19b4a9434ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a>建立和管理 Azure SQL Database 安全性以供異地還原或容錯移轉使用 

> [!NOTE]
> [作用中異地複寫](sql-database-geo-replication-overview.md)現在可供所有服務層中的所有資料庫使用。
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a>災害復原的驗證需求概觀
本主題說明 hello 驗證需求 tooconfigure 和控制[作用中地理複寫](sql-database-geo-replication-overview.md)及 hello 的步驟需要的 tooset 使用者存取 toohello 次要資料庫。 它也會說明如何啟用 access toohello 復原的資料庫之後使用[異地還原](sql-database-recovery-using-backups.md#geo-restore)。 如需復原選項的詳細資訊，請參閱 [商務持續性概觀](sql-database-business-continuity.md)。

## <a name="disaster-recovery-with-contained-users"></a>災害復原與自主使用者
不同於傳統的使用者必須是對應 toologins hello master 資料庫中的，包含的使用者完全由 hello 資料庫本身所管理。 這樣有兩個優點。 在 hello 災害復原案例中，hello 使用者可以繼續 tooconnect toohello 新主要資料庫或 hello 復原的資料庫使用地理還原而不需要任何額外的設定，因為 hello 資料庫管理 hello 使用者。 從登入的觀點來看，這個組態也有潛在的延展性和效能優勢。 如需詳細資訊，請參閱 [自主資料庫使用者 - 讓資料庫具有可攜性](https://msdn.microsoft.com/library/ff929188.aspx)。 

hello 主要取捨是管理 hello 大規模災害復原程序是更具挑戰性。 當您有多個資料庫維護 hello 認證使用的相同登入包含該使用 hello 多個資料庫中的使用者可能會否定 hello 優點包含的使用者。 例如，hello 密碼輪動原則需要進行變更以一致的方式在多個資料庫，而非 hello 登入的變更 hello 密碼一次 hello master 資料庫中。 基於這個理由，如果您有多個資料庫的使用 hello 相同的使用者名稱和密碼，不建議使用包含的使用者。 

## <a name="how-tooconfigure-logins-and-users"></a>如何 tooconfigure 登入和使用者
如果您使用的登入和使用者 （而不是包含的使用者），您必須採取額外的步驟 tooinsure 存在相同的登入該 hello hello master 資料庫中。 hello 下列各節簡述 hello 步驟涉及和其他考量。

### <a name="set-up-user-access-tooa-secondary-or-recovered-database"></a>設定使用者存取 tooa 次要或復原資料庫
為了讓 hello 次要資料庫 toobe 可用為唯讀的次要資料庫和 tooensure 適當的存取權 toohello 新的主要資料庫或 hello 資料庫使用地理還原復原 hello 主要 hello 目標伺服器的資料庫必須具有 hello在 hello 復原之前就定位適當的安全性設定。

在本主題稍後描述 hello 針對每個步驟的特定權限。

準備使用者存取 tooa 應該做為設定地理複寫的一部分執行地理複寫的次要資料庫。 準備 toohello 異地還原的資料庫使用者的存取權應該執行隨時 hello 原始伺服器在線上時 （例如為 hello DR 向下切入的一部分）。

> [!NOTE]
> 如果您無法移轉或異地還原 tooa 伺服器沒有正確設定的登入存取 tooit 會限制的 toohello 伺服器系統管理員帳戶。
> 
> 

設定登入 hello 目標伺服器上包含下列 3 個步驟：

#### <a name="1-determine-logins-with-access-toohello-primary-database"></a>1.判斷具有存取 toohello 主要資料庫的登入：
hello hello 程序的第一個步驟是的 toodetermine hello 目標伺服器複製哪些登入。 這是具有一對 SELECT 陳述式，一個在 hello 邏輯 master 資料庫中 hello 來源伺服器上，一個在 hello 主要資料庫本身。

只有 hello 伺服器管理員或成員的 hello **LoginManager**伺服器角色可以決定 hello 來源伺服器上的 hello 登入以 hello 下列 SELECT 陳述式。 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

只有 hello db_owner 資料庫角色、 hello dbo 使用者或伺服器管理員的成員可以決定所有 hello 主要資料庫中的 hello 資料庫使用者主體。

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-hello-sid-for-hello-logins-identified-in-step-1"></a>2.找出在步驟 1 所識別的 hello 登入 hello SID:
藉由比較 hello 查詢從 hello 上一節和比對 hello Sid 的 hello 輸出，您可以對應 hello 伺服器登入 toodatabase 使用者。 具有相符 SID 與資料庫使用者的登入具有使用者存取 toothat 資料庫主體資料庫使用者的身分。 

hello 下列查詢可使用的 toosee 所有 hello 使用者主體及其 Sid 在資料庫中的。 只有 hello db_owner 資料庫角色或伺服器管理員的成員才能執行此查詢。

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> hello **INFORMATION_SCHEMA**和**sys**使用者擁有*NULL* Sid 和 hello**客體**SID 是**0x00**。 hello **dbo** SID 可能開頭*0x01060000000001648000000000048454 開頭*，如果 hello 資料庫建立者即 hello 伺服器管理員，而不是屬於**DbManager**。
> 
> 

#### <a name="3-create-hello-logins-on-hello-target-server"></a>3.Hello 目標伺服器上建立 hello 登入：
hello 最後一個步驟是 toogo toohello 目標伺服器或伺服器，並產生以 hello hello 登入適當的 Sid。 hello 基本語法如下所示。

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> 如果您想要 toogrant 使用者存取 toohello 次要資料庫，而不是 toohello 主要，您可以會使用下列語法的 hello 改變 hello hello 主要伺服器上的使用者登入。
> 
> ALTER LOGIN <login name> DISABLE
> 
> 停用不會變更 hello 密碼，因此總是可以啟用它，如有需要。
> 
> 

## <a name="next-steps"></a>後續步驟
* 如需管理資料庫存取和登入的詳細資訊，請參閱 [SQL Database 安全性︰管理資料庫存取與登入安全性](sql-database-manage-logins.md)。
* 如需自主資料庫使用者的詳細資訊，請參閱 [自主資料庫使用者 - 使資料庫可攜](https://msdn.microsoft.com/library/ff929188.aspx)。
* 如需使用和設定主動式異地複寫的相關資訊，請參閱[主動式異地複寫](sql-database-geo-replication-overview.md)
* 如需使用異地還原的相關資訊，請參閱[異地還原](sql-database-recovery-using-backups.md#geo-restore)

