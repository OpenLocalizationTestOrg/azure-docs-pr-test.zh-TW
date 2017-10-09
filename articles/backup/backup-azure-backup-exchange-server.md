---
title: "使用 System Center 2012 R2 DPM 備份的 Exchange server tooAzure 向上 aaaBack |Microsoft 文件"
description: "深入了解如何設定 Exchange server tooAzure tooback 備份使用 System Center 2012 R2 DPM"
services: backup
documentationcenter: 
author: MaanasSaran
manager: NKolli1
editor: 
ms.assetid: 13f32256-888e-416e-a78b-40c2a26a5939
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: masaran;jimpark;delhan;trinadhk;markgal
ms.openlocfilehash: fa99296d095c180333474b6d419ebc5ec727547a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-system-center-2012-r2-dpm"></a>備份 Exchange server tooAzure 使用 System Center 2012 R2 DPM 備份
本文章說明如何設定 Microsoft Exchange server 的 System Center 2012 R2 Data Protection Manager (DPM) 伺服器 tooback tooconfigure 太 Azure 備份。  

## <a name="updates"></a>更新
toosuccessfully 暫存器 hello DPM 伺服器使用 Azure Backup，您必須安裝 hello 最新更新彙總套件 hello Azure Backup Agent 的 System Center 2012 R2 DPM 和 hello 最新版本。 收到 hello hello 最新的更新彙總[Microsoft 目錄](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager)。

> [!NOTE]
> 這篇文章中的 hello 範例，版本 2.0.8719.0 hello Azure Backup Agent 已安裝，且 System Center 2012 R2 DPM 上安裝更新彙總套件 6。
>
>

## <a name="prerequisites"></a>必要條件
在繼續之前，請確定所有 hello[必要條件](backup-azure-dpm-introduction.md#prerequisites)tooprotect 工作負載已符合使用 Microsoft Azure 備份。 這些必要條件 hello 如下：

* 已建立 hello Azure 站台上的備份保存庫。
* 已下載的 toohello DPM 伺服器代理程式和保存庫認證。
* hello DPM 伺服器上安裝 hello 代理程式。
* hello 保存庫認證是使用的 tooregister hello DPM 伺服器。
* 如果您要保護 Exchange 2016，請升級 tooDPM 2012 R2 UR9 或更新版本

## <a name="dpm-protection-agent"></a>DPM 保護代理程式
tooinstall hello DPM 保護代理程式在 hello Exchange 伺服器上，請遵循下列步驟：

1. 請確定已正確設定 hello 防火牆。 請參閱[設定 hello 代理程式的防火牆例外](https://technet.microsoft.com/library/Hh758204.aspx)。
2. Hello Exchange 伺服器上安裝 hello 代理程式，依序按一下**管理 > 代理程式 > 安裝**DPM 系統管理員主控台。 請參閱[hello DPM 保護代理程式安裝](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396)如需詳細步驟。

## <a name="create-a-protection-group-for-hello-exchange-server"></a>建立 hello Exchange 伺服器的保護群組
1. 在 hello DPM 系統管理員主控台中，按一下 **保護**，然後按一下**新增**上 hello 工具功能區 tooopen hello**建立新保護群組**精靈。
2. 在 hello ** 褖畫惎**hello 精靈按一下畫面**下一步**。
3. 在 hello**選取保護群組類型**畫面上，選取**伺服器**按一下**下一步**。
4. 您想 tooprotect 並按一下選取的 hello Exchange 伺服器資料庫**下一步**。

   > [!NOTE]
   > 如果您要保護 Exchange 2013，請檢查 hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx)。
   >
   >

    在下列範例的 hello，會選取 hello Exchange 2010 資料庫。

    ![選擇群組成員](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. 選取 hello 資料保護方式。

    名稱 hello 保護群組，然後再選取這兩個 hello 下列選項：

   * 我想要使用磁碟進行短期保護。
   * 我想要線上保護。
6. 按一下 [下一步] 。
7. 選取 hello**執行 Eseutil toocheck 資料完整性**如果您想 toocheck hello 完整性 hello Exchange Server 資料庫的選項。

    選取此選項之後，備份一致性檢查會執行上的 hello DPM 伺服器 tooavoid hello I/O 流量所產生的執行 hello **eseutil** hello Exchange 伺服器上的命令。

   > [!NOTE]
   > toouse 選取此選項，您必須複製 hello Ese.dll 和 Eseutil.exe 檔案 toohello hello DPM 伺服器上的 C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin 目錄。 否則，會觸發 hello 下列錯誤：  
   > ![eseutil 錯誤](./media/backup-azure-backup-exchange-server/eseutil-error.png)
   >
   >
8. 按一下 [下一步] 。
9. 選取 hello 資料庫**複製備份**，然後按一下**下一步**。

   > [!NOTE]
   > 如果您未對資料庫的至少一個 DAG 複本選取「完整備份」，則不會截斷記錄檔。
   >
   >
10. 設定目標 hello**短期備份**，然後按一下**下一步**。
11. 檢閱 hello 可用磁碟空間，然後按一下**下一步**。
12. 選取 hello 時間在哪一個 hello DPM 伺服器將會建立 hello 初始複寫，並按一下 **下一步**。
13. 選取 hello 一致性檢查選項，然後再按一下**下一步**。
14. 選擇您想要向上 tooAzure，tooback，然後按一下 hello 資料庫**下一步**。 例如：

    ![指定線上保護資料](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. 定義 hello 排程**Azure Backup**，然後按一下**下一步**。 例如：

    ![指定線上備份排程](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > 請注意，線上復原點是以快速完整復原點為基礎。 因此，您必須排程 hello 線上復原點之後所指定的 hello 的 hello 時間表達完整的復原點。
    >
    >
16. 設定保留原則 hello **Azure Backup**，然後按一下**下一步**。
17. 選擇線上複寫選項並按 [下一步] 。

    如果您有大型的資料庫時，可能需要很長的時間 hello 初始備份 toobe hello 網路上建立。 tooavoid 此問題，您可以建立離線備份。  

    ![指定線上保留期原則](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. 確認 hello 設定，然後按一下**建立群組**。
19. 按一下 [關閉] 。

## <a name="recover-hello-exchange-database"></a>Hello Exchange 資料庫復原
1. toorecover Exchange 資料庫，按一下**復原**hello DPM 系統管理員主控台中。
2. 找出您想 toorecover hello Exchange 資料庫。
3. 選取 線上復原點從 hello*復原時間*下拉式清單。
4. 按一下**復原**toostart hello**復原精靈**。

線上復原點有五種復原類型：

* **復原 toooriginal Exchange Server 位置：** hello 資料將會復原的 toohello 原始 Exchange server。
* **復原 Exchange Server 上的 tooanother 資料庫：** hello 資料將會復原的 tooanother 另一部 Exchange 伺服器上的資料庫。
* **復原 tooa 復原資料庫：** hello 資料將會復原的 tooan Exchange 復原資料庫 (RDB)。
* **複製 tooa 網路資料夾：** hello 資料將會復原的 tooa 網路資料夾。
* **複製 tootape:**如果您有任何磁帶媒體櫃或獨立磁帶機，將會附加，且設定在 hello DPM 伺服器，hello 復原點複製 tooa 可用磁帶。

    ![選擇線上複寫](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a>後續步驟
* [Azure 備份常見問題集](backup-azure-backup-faq.md)
