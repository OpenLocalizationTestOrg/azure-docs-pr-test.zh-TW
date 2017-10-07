---
title: "aaaRecover 資料，從 Azure 備份伺服器 |Microsoft 文件"
description: "復原您所保護的 hello 資料 tooa 復原服務保存庫，從任何 Azure 備份伺服器已註冊的 toothat 保存庫。"
services: backup
documentationcenter: 
author: nkolli1
manager: shreeshd
editor: 
ms.assetid: a55f8c6b-3627-42e1-9d25-ed3e4ab17b1f
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: adigan;giridham;trinadhk;markgal
ms.openlocfilehash: 74847880e646c3c4f198afe318f1db30363d137a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="recover-data-from-azure-backup-server"></a>從 Azure 備份伺服器復原資料
您可以使用 Azure 備份伺服器 toorecover hello 資料，而您已備份的 tooa 復原服務保存庫。 hello 程序提供執行因此整合至 hello Azure 備份伺服器管理主控台中，並且其他 Azure 備份 」 元件類似 toohello 復原工作流程。

> [!NOTE]
> 這篇文章僅適用於 [System Center Data Protection Manager 2012 R2 UR7 或更新版本] (https://support.microsoft.com/en-us/kb/3065246)，結合 hello[最新的 Azure 備份代理程式](http://aka.ms/azurebackup_agent)。
>
>

toorecover 資料，從 Azure 備份伺服器：

1. 從 hello**復原**索引標籤上的 hello Azure 備份伺服器管理主控台中，按一下**加入外部 DPM'** (在 hello 囉 」 畫面的左上角)。   
    ![新增外部 DPM](./media/backup-azure-alternate-dpm-server/add-external-dpm.png)
2. 下載新**保存庫認證**hello hello 與相關聯的保存庫中**Azure 備份伺服器**其中要復原 hello 資料，從 Azure 備份伺服器 hello 清單中選擇 hello Azure 備份伺服器向 hello 復原服務保存庫，並提供 hello**加密複雜密碼**hello 伺服器要復原其資料相關聯。

    ![外部 DPM 認證](./media/backup-azure-alternate-dpm-server/external-dpm-credentials.png)

   > [!NOTE]
   > 僅 Azure 備份伺服器相關聯 hello 相同註冊保存庫可以復原彼此的資料。
   >
   >

    一旦 hello 外部的 Azure 備份伺服器成功加入，您可以瀏覽 hello 外部伺服器 hello 資料並 hello 本機的 Azure 備份伺服器，從 hello**復原** 索引標籤。
3. 瀏覽 hello 可用清單所保護的實際執行伺服器 hello 外部的 Azure 備份伺服器，並選取 hello 適當的資料來源。

    ![瀏覽外部 DPM 伺服器](./media/backup-azure-alternate-dpm-server/browse-external-dpm.png)
4. 選取**hello 的月份和年份**從 hello**復原點**下拉式清單選取所需的 hello**復原日期**的 hello 復原點時已建立，並選取 hello**復原時間**。

    檔案和資料夾清單隨即出現在 hello 底部窗格中，可以瀏覽並復原 tooany 位置。

    ![外部 DPM 伺服器復原點](./media/backup-azure-alternate-dpm-server/external-dpm-recoverypoint.png)
5. 以滑鼠右鍵按一下 hello 適當的項目，然後按一下**復原**。

    ![外部 DPM 復原](./media/backup-azure-alternate-dpm-server/recover.png)
6. 檢閱 hello**復原選取項目**。 請確認 hello 資料和 hello 要復原的備份複本的時間以及 hello 來源從中建立 hello 備份複本。 如果 hello 選取範圍不正確，請按一下**取消**toonavigate 後 toorecovery 索引標籤 tooselect 適當的復原點。 如果 hello 選擇正確時，請按一下**下一步**。

    ![外部 DPM 復原摘要](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-summary.png)
7. 選取**復原 tooan 替代位置**。 **瀏覽**toohello hello 復原正確的位置。

    ![外部 DPM 復原替代位置](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-alternate-location.png)
8. 選擇相關太 hello 選項**建立複本**，**略過**，或**覆寫**。

   * **建立複本**-建立 hello 檔案的副本，如果沒有名稱衝突。
   * **略過**-如果有名稱衝突，這會將 hello 原始檔案 hello 檔案時無法復原。
   * **覆寫**-名稱衝突，是否會覆寫 hello 現有 hello 檔案副本。

     選擇適當選項，hello 太**還原安全性**。 您可以套用 hello 的 hello hello 資料要復原的目的地電腦的安全性設定或 hello 所適用的 tooproduct 次 hello hello 的復原點建立的安全性設定。

     識別是否**通知**傳送，一旦 hello 復原已成功完成。

     ![外部 DPM 復原通知](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-notifications.png)
9. hello**摘要**畫面會列出目前選擇的 hello 選項。 一旦您按一下**「 復原 」**，hello 資料是復原的 toohello 適當的內部部署位置。

    ![外部 DPM 復原選項摘要](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-options-summary.png)

   > [!NOTE]
   > hello 復原工作可以監視在 hello**監視**hello Azure 備份伺服器 索引標籤。
   >
   >

    ![監視復原](./media/backup-azure-alternate-dpm-server/monitoring-recovery.png)
10. 您可以按一下**清除外部 DPM**上 hello**復原**hello hello 外部 DPM 伺服器的 DPM 伺服器 tooremove hello 檢視 索引標籤。

    ![清除外部 DPM](./media/backup-azure-alternate-dpm-server/clear-external-dpm.png)

## <a name="troubleshooting-error-messages"></a>疑難排解錯誤訊息
| 否。 | 錯誤訊息 | 疑難排解步驟 |
|:---:|:--- |:--- |
| 1. |此伺服器未註冊的 toohello hello 保存庫認證所指定的保存庫。 |**原因：**會出現這個錯誤時 hello 保存庫認證檔案選取不屬於的 toohello 復原服務保存庫相關聯 Azure 備份伺服器的 hello 嘗試修復。 <br> **解決方式：**下載 hello 保存庫認證檔案從 hello 復原服務保存庫 toowhich hello 註冊 Azure 備份伺服器。 |
| 2. |Hello 可復原的資料無法使用，或 hello 選取的伺服器不是 DPM 伺服器。 |**原因：**有沒有其他 Azure 備份伺服器已註冊的 toohello 復原服務保存庫，或伺服器 hello 您尚未尚未上傳 hello 中繼資料，或是 hello 選取的伺服器不是 Azure 備份伺服器 （也稱為 Windows Server 或 Windows 用戶端）。 <br> **解決方式：**如果有其他 Azure 備份伺服器已註冊的 toohello 復原服務保存庫，請確定該 hello 最新 Azure 備份代理程式安裝。 <br>如果有其他 Azure 備份伺服器已註冊的 toohello 復原服務保存庫，請等候一天後安裝 toostart hello 復原程序。 hello 夜間工作都會將上傳所有受保護的 hello 備份 toocloud hello 中繼資料。 hello 資料可供復原。 |
| 3. |沒有其他 DPM 伺服器是已註冊的 toothis 保存庫。 |**原因：**沒有其他 Azure 備份伺服器的已註冊的 toohello 保存庫中的 hello 嘗試修復。<br>**解決方式：**如果有其他 Azure 備份伺服器已註冊的 toohello 復原服務保存庫，請確定該 hello 最新 Azure 備份代理程式安裝。<br>如果有其他 Azure 備份伺服器已註冊的 toohello 復原服務保存庫，請等候一天後安裝 toostart hello 復原程序。 hello 夜間工作會上傳所有受保護的備份 toocloud hello 中繼資料。 hello 資料可供復原。 |
| 4. |提供的 hello 加密複雜密碼不符合以 hello 下列伺服器關聯的複雜密碼：**<server name>** |**原因：** hello hello 加密 hello hello Azure 備份伺服器的資料要復原資料的程序中使用的加密複雜密碼不符合提供的 hello 加密複雜密碼。 hello 代理程式是無法 toodecrypt hello 資料。 因此 hello 復原會失敗。<br>**解決方式：**請提供 hello 完全相同的加密複雜密碼與 hello 要復原其資料的 Azure 備份伺服器相關聯。 |

## <a name="frequently-asked-questions"></a>常見問題集

### <a name="why-cant-i-add-an-external-dpm-server-after-installing-ur7-and-latest-azure-backup-agent"></a>為什麼不能在安裝 UR7 和最新的 Azure 備份代理程式之後，從另一部 DPM 伺服器新增外部 DPM 伺服器？

Hello 屬於資料來源的 DPM 伺服器受保護的雲端 toohello （透過早於更新彙總套件 7 使用更新彙總套件），您必須等待至少一天後安裝 hello UR7 和最新的 Azure Backup agent，toostart**加入外部 DPM 伺服器**. hello 一天時間週期為 hello DPM 保護群組 tooAzure 需要的 tooupload hello 中繼資料。 保護群組的中繼資料上傳 hello 透過夜間工作的第一次。

### <a name="what-is-hello-minimum-version-of-hello-microsoft-azure-recovery-services-agent-needed"></a>Hello hello Microsoft Azure 復原服務代理程式所需的最小版本為何？

hello 最小版本 hello Microsoft Azure 復原服務代理程式或 Azure 備份代理程式，需要 tooenable 這項功能是 2.0.8719.0。  tooview hello 代理程式的版本： 開啟 控制台 **>** 所有控制台項目 **>** 程式和功能 **>** Microsoft Azure Recovery Services Agent。 如果是小於 2.0.8719.0 hello 版，下載並安裝 hello[最新的 Azure 備份代理程式](https://go.microsoft.com/fwLink/?LinkID=288905)。

![清除外部 DPM](./media/backup-azure-alternate-dpm-server/external-dpm-azurebackupagentversion.png)

## <a name="next-steps"></a>後續步驟：
•    [Azure 備份常見問題集](backup-azure-backup-faq.md)
