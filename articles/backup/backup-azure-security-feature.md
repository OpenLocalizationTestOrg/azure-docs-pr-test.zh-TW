---
title: "保護使用 Azure 備份的混合式備份，aaaSecurity 功能 toohelp |Microsoft 文件"
description: "了解 toouse 安全性功能在 Azure Backup toomake 備份更安全的方式"
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 47bc8423-0a08-4191-826d-3f52de0b4cb8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: pajosh
ms.openlocfilehash: 17a0f5e877f84af53c15062ec4a8df480383125e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-features-toohelp-protect-hybrid-backups-that-use-azure-backup"></a>安全性功能 toohelp 保護使用 Azure 備份的混合式備份
現在越來越重視安全性問題，例如惡意程式碼、勒索軟體和入侵。 這些安全性問題在成本和資料方面付出的代價很高。 tooguard 抵禦這類攻擊中，Azure 備份現在提供的安全性功能 toohelp 保護儲存在混合式備份。 本文件涵蓋如何 tooenable 並使用這些功能，使用 Azure 復原服務代理程式和 Azure 備份伺服器。 這些功能包括：

- **預護**。 每當執行重要作業 (如變更複雜密碼) 時，就會多一道驗證。 這項驗證是這類作業可能是 tooensure 只能由擁有有效的 Azure 認證的使用者執行。
- **警示**。 電子郵件通知會傳送重要的作業，例如刪除備份資料時，toohello 訂用帳戶管理員會執行。 這封電子郵件可確保該 hello 使用者接收通知快速的這類動作。
- **復原**。 已刪除的備份資料會保留額外 14 天，從 hello hello 刪除日期。 在指定的時間間隔內中,，所以即使攻擊的情況不會遺失任何資料，這可確保 hello 資料的復原能力。 此外，最小復原點數目越大維護 tooguard 針對損毀的資料。

> [!NOTE]
> 如果您使用基礎結構即服務 (IaaS) VM 備份，則不應該啟用安全性功能。 這些功能尚無法用於 IaaS VM 備份，所以啟用它們不會有任何影響。 只有當您使用下列項目，才應該啟用安全性功能︰ <br/>
>  * **Azure 備份代理程式**。 至少為代理程式 2.0.9052 版。 啟用這些功能之後，您應先升級 toothis 代理程式版本 tooperform 重要作業。 <br/>
>  * **Azure 備份伺服器**。 至少為 Azure 備份代理程式 2.0.9052 版與 Azure 備份伺服器 Update 1。 <br/>
>  * **System Center Data Protection Manager**。 至少為 Azure 備份代理程式 2.0.9052 版與 Data Protection Manager 2012 R2 UR12 或 Data Protection Manager 2016 UR2。 <br/> 


> [!NOTE]
> 這些功能僅適用於復原服務保存庫。 所有新建立的復原服務保存庫的 hello 有預設啟用這些功能。 針對現有的復原服務保存庫，使用者會使用 hello hello 之後 > 一節中所述的步驟來啟用這些功能。 之後 hello 啟用功能，它們會套用 tooall hello 復原服務代理程式的電腦、 Azure 備份伺服器執行個體和與 hello 保存庫註冊的 Data Protection Manager 伺服器。 啟用此設定是一次性動作，啟用之後便無法停用這些功能。
>

## <a name="enable-security-features"></a>啟用安全性功能
如果您要建立的復原服務保存庫，您可以使用所有的 hello 安全性功能。 如果您在使用現有的保存庫，請依照下列這些步驟啟用安全性功能︰

1. Toohello Azure 入口網站使用的登入您的 Azure 認證。
2. 選取 [瀏覽]，然後輸入 [復原服務]。

    ![Azure 入口網站瀏覽選項的螢幕擷取畫面](./media/backup-azure-security-feature/browse-to-rs-vaults.png) <br/>

    復原服務保存庫 hello 清單隨即出現。 從此清單中選取保存庫。 hello 選取保存庫儀表板隨即開啟。
3. 從下方會出現在 hello 保存庫，之下的 hello 清單的項目**設定**，按一下 **屬性**。

    ![復原服務保存庫選項的螢幕擷取畫面](./media/backup-azure-security-feature/vault-list-properties.png)
4. 按一下 [安全性設定] 之下的 [更新]。

    ![復原服務保存庫屬性的螢幕擷取畫面](./media/backup-azure-security-feature/security-settings-update.png)

    hello 更新連結會開啟 hello**安全性設定**刀鋒視窗中，它可提供 hello 功能的摘要，並可讓您啟用它們。
5. Hello 下拉式清單從**已設定 Azure Multi-factor Authentication？**，如果您已啟用，請選取值 tooconfirm [Azure Multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)。 如果已啟用，會要求您從另一個裝置 （例如行動電話） tooauthenticate 時登入 toohello Azure 入口網站。

   當您執行重要作業在備份中時，您可以 tooenter 安全性 pin 碼，可在 hello Azure 入口網站上取得。 啟用 Multi-Factor Authentication 可多一道安全性。 只有獲得授權的使用者具有有效的 Azure 認證，而且驗證從第二台裝置，可以存取 hello Azure 入口網站。
6. toosave 安全性設定，請選取**啟用**按一下**儲存**。 您可以選取**啟用**只有您選取的值從 hello 之後**已設定 Azure Multi-factor Authentication？** hello 上一個步驟中的清單。

    ![安全性設定的螢幕擷取畫面](./media/backup-azure-security-feature/enable-security-settings-dpm-update.png)

## <a name="recover-deleted-backup-data"></a>復原已刪除的備份資料
備份會保留額外的 14 天，已刪除的備份資料，並不會刪除它立即如果 hello**停止與刪除備份資料的備份**執行作業。 toorestore hello 14 天的期限，在此資料會採取下列步驟，視您使用的 hello:

**Azure 復原服務代理程式**使用者：

1. 如果備份已發生所在的 hello 電腦仍然可以使用，請使用[復原資料 toohello 同一部電腦](backup-azure-restore-windows-server.md#use-instant-restore-to-recover-data-to-the-same-machine)Azure 復原服務，從所有 hello 舊的復原點 toorecover 中。
2. 如果無法使用這台電腦，使用[復原 tooan 替代機器](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine)toouse 另一個 Azure 復原服務的電腦 tooget 這項資料。

若為 **Azure 備份伺服器**使用者：

1. Hello 伺服器備份所發生的位置是否仍然可用，重新保護 hello 刪除資料來源，並使用 hello**復原資料**功能 toorecover 從所有 hello 舊的復原點。
2. 如果無法使用此伺服器，使用[從另一個 Azure 備份伺服器復原資料](backup-azure-alternate-dpm-server.md)toouse 另一個 Azure 備份伺服器執行個體 tooget 此資料。

**Data Protection Manager** 使用者：

1. Hello 伺服器備份所發生的位置是否仍然可用，重新保護 hello 刪除資料來源，並使用 hello**復原資料**功能 toorecover 從所有 hello 舊的復原點。
2. 如果無法使用此伺服器，使用[加入外部 DPM](backup-azure-alternate-dpm-server.md) toouse 另一個 Data Protection Manager 伺服器 tooget 這項資料。

## <a name="prevent-attacks"></a>防止攻擊
檢查已加入 toomake 確定只有有效的使用者可以執行各種作業。 其中包括新增額外一道驗證，並維護復原用途所需的最小保留範圍。

### <a name="authentication-tooperform-critical-operations"></a>驗證 tooperform 重要的作業
新增一層額外的驗證作業的一部分，您會提示的 tooenter 安全性 pin 碼執行時**停止保護，刪除資料與**和**變更複雜密碼**作業.

tooreceive 此 PIN:

1. 登入 toohello Azure 入口網站。
2. 瀏覽過**復原服務保存庫** > **設定** > **屬性**。
3. 在 [安全性 PIN 碼] 底下，按一下 [產生]。 這會開啟刀鋒視窗，其中包含 hello 的 PIN toobe hello Azure 復原服務代理程式使用者介面中輸入。
    此 PIN 碼的有效時間只有五分鐘，而且會在該期間後自動產生。

### <a name="maintain-a-minimum-retention-range"></a>維護最小的保留範圍
tooensure 有有效的數字的復原點可用，已新增下列檢查 hello:

- 若為每日保留，最少應該保留**七**天。
- 若為每週保留，最少應該保留**四**週。
- 若為每月保留，最少應該保留**三**個月。
- 若為每年保留，最少應該保留**一**年。

## <a name="notifications-for-critical-operations"></a>重要作業的通知
一般而言，執行重要的作業時，hello 訂用帳戶管理員會傳送電子郵件通知 hello 作業的相關詳細資料。 您可以使用 hello Azure 入口網站來設定這些通知其他電子郵件收件者。

本文提及的 hello 安全性功能提供對目標型攻擊的防禦機制。 更重要的是，如果攻擊發生時，這些功能可讓您 hello 能力 toorecover 您的資料。

## <a name="troubleshooting-errors"></a>錯誤疑難排解
| 作業 | 錯誤詳細資料 | 解決方案 |
| --- | --- | --- |
| 原則變更 |無法修改 hello 備份原則。 錯誤： hello 目前的作業失敗，因為 tooan 內部服務錯誤 [0x29834]。 請稍後重試 hello 作業。 如果 hello 問題持續發生，請連絡 Microsoft 支援服務。 |**原因：**<br/>當安全性設定已啟用，tooreduce 保留範圍下方 hello 上述指定的最小值再試一次，而您位於不受支援的版本會出現此錯誤 （指定第一個附註這篇文章中支援的版本）。 <br/>**建議的動作：**<br/> 在此情況下，您應該設定上述 hello 最小保留期限指定 （每日、 四週每週、 每月或一年安排每年的三週七天） 的保留期限 tooproceed 與原則相關的更新。 （選擇性） 慣用的方法是 tooupdate 備份代理程式，Azure 備份伺服器和/或 DPM UR tooleverage 所有 hello 安全性都更新。 |
| 變更複雜密碼 |輸入的安全性 PIN 碼不正確。 (識別碼： 100130)提供 hello 正確的安全性 pin 碼 toocomplete 這項作業。 |**原因：**<br/> 當您在執行重要作業 (例如變更複雜密碼) 時輸入無效或已到期的安全性 PIN 碼時，就會出現此錯誤。 <br/>**建議的動作：**<br/> toocomplete hello 作業，您必須輸入有效的安全性 pin 碼。 tooget hello 的 PIN，登入 tooAzure 入口網站並瀏覽 tooRecovery 服務保存庫 > 設定 > 內容 > 產生安全性 pin 碼。 使用這個 PIN toochange 複雜密碼。 |
| 變更複雜密碼 |作業失敗。 識別碼：120002 |**原因：**<br/>當安全性設定已啟用，toochange 複雜密碼再試一次，而您在位於不受支援的版本 （在本文的第一個附註中指定的有效版本），就會出現此錯誤。<br/>**建議的動作：**<br/> toochange 複雜密碼，您必須先更新備份代理程式 toominimum 版本最小 2.0.9052、 Azure 備份伺服器 toominimum 更新 1，及/或 DPM toominimum DPM 2012 R2 UR12 或 DPM 2016 UR2 （下載連結底下），然後輸入有效的安全性 pin 碼。 tooget hello 的 PIN，登入 tooAzure 入口網站並瀏覽 tooRecovery 服務保存庫 > 設定 > 內容 > 產生安全性 pin 碼。 使用這個 PIN toochange 複雜密碼。 |

## <a name="next-steps"></a>後續步驟
* [開始使用 Azure 復原服務保存庫](backup-azure-vms-first-look-arm.md)tooenable 這些功能。
* [下載最新 Azure 復原服務代理程式 hello](http://aka.ms/azurebackup_agent) toohelp 保護 Windows 電腦，並保護您的備份資料的攻擊。
* [下載 hello 最新的 Azure 備份伺服器](https://aka.ms/latest_azurebackupserver)toohelp 保護工作負載和備份資料不受攻擊的防護。
* [下載 System Center 2012 R2 Data Protection Manager 的 UR12](https://support.microsoft.com/help/3209592/update-rollup-12-for-system-center-2012-r2-data-protection-manager)或[下載 System Center 2016 Data Protection Manager 的 UR2](https://support.microsoft.com/help/3209593/update-rollup-2-for-system-center-2016-data-protection-manager) toohelp 保護工作負載和備份資料不受攻擊的防護。
