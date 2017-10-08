---
title: "工作負載 tooAzure 傳統入口網站註冊 aaaUse Azure 備份伺服器 tooback |Microsoft 文件"
description: "請確定您的環境已正確準備 tooback 工作負載使用 Azure 備份伺服器備份"
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
keywords: "Azure 備份伺服器；備份保存庫"
ms.assetid: d86450e8-da63-4283-8fd7-2ee629fa14ab
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.openlocfilehash: 7b574824c448096e0c0ba74a872ab8f2a434f6a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-using-azure-backup-server"></a>準備使用 Azure 備份伺服器的工作負載備份 tooback
> [!div class="op_single_selector"]
> * [Azure 備份伺服器](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Azure 備份伺服器 (傳統)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (傳統)](backup-azure-dpm-introduction-classic.md)
>
>

這篇文章是關於準備您的環境 tooback 工作負載使用 Azure 備份伺服器備份。 透過 Azure 備份伺服器，您將可從單一主控台保護 Hyper-V VM、Microsoft SQL Server、SharePoint Server、Microsoft Exchange 和 Windows 用戶端等應用程式工作負載。

> [!WARNING]
> Azure 備份伺服器會繼承 hello 功能的 Data Protection Manager (DPM) 工作負載備份。 您會發現指標 tooDPM 某些功能的文件。 不過，Azure 備份伺服器不會保護磁帶，也不會與 System Center 整合。
>
>

## <a name="1-windows-server-machine"></a>1.Windows Server 機器
![步驟 1](./media/backup-azure-microsoft-azure-backup/step1.png)

hello 向 Azure 備份伺服器 hello 快速安裝和執行的第一個步驟是 toohave Windows Server 電腦。

| 位置 | 最低需求 | 其他指示 |
| --- | --- | --- |
| Azure |Azure IaaS 虛擬機器 <br><br>A2 標準：雙核心、3.5GB 的 RAM |您可以先從 Windows Server 2012 R2 Datacenter 的簡單資源庫映像開始著手。 [使用 Azure 備份伺服器 (DPM) 保護 IaaS 工作負載](https://technet.microsoft.com/library/jj852163.aspx) 有許多細節需要注意。 請確認您已閱讀 hello 發行項完全部署 hello 機器之前。 |
| 內部部署 |Hyper-V VM、<br> VMWare VM、<br> 或實體主機<br><br>雙核心和 4GB 的 RAM |您可以使用 hello DPM 存放裝置使用 Windows Server 重複資料刪除重複資料刪除。 深入了解在 Hyper-V VM 中部署時， [DPM 和重複資料刪除](https://technet.microsoft.com/library/dn891438.aspx) 如何搭配運作。 |

> [!NOTE]
> 建議您在具有 Windows Server 2012 R2 Datacenter 的機器上安裝 Azure 備份伺服器。 Hello 必要條件大量自動涵蓋 hello hello Windows 作業系統的最新版本。
>
>

如果您計劃 toojoin Azure 備份伺服器 tooa 網域，建議您加入 hello 實體伺服器或虛擬機器 toohello 網域再安裝 hello Azure 備份伺服器軟體。 部署之後，移動 Azure 備份伺服器 tooa 新的網域，是*不支援*。

## <a name="2-backup-vault"></a>2.備份保存庫
![步驟 2](./media/backup-azure-microsoft-azure-backup/step2.png)

當您傳送 tooAzure 備份資料，或將它保留在本機，hello Azure 備份伺服器必須是已註冊的 tooa 保存庫。 如果您是新的 Azure 備份使用者，而且想 toouse Azure 備份伺服器，請參閱 hello Azure 入口網站的版本，這篇文章-[準備使用 Azure 備份伺服器的工作負載備份 tooback](backup-azure-microsoft-azure-backup.md)。

> [!IMPORTANT]
> 從開始 2017 年 3 月，您無法再使用 hello 傳統入口網站 toocreate 備份保存庫。
> 您現在可以升級您備份保存庫 tooRecovery 服務保存庫。 如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。 Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。<br/> 2017 年 10 月 15 之後，您無法使用 PowerShell toocreate 備份保存庫。 **在 2017 年 11 月 1 日以前**：
>- 所有剩餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。
>- 您將無法 tooaccess hello 傳統入口網站中無法備份資料。 相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。
>



## <a name="3-software-package"></a>3.軟體封裝
![步驟 3](./media/backup-azure-microsoft-azure-backup/step3.png)

### <a name="downloading-hello-software-package"></a>下載 hello 軟體套件
類似 toovault 認證，您可以下載 Microsoft Azure 備份應用程式工作負載從 hello**快速入門 頁面上**hello 備份保存庫。

1. 按一下**對於應用程式的工作負載 (磁碟 tooDisk tooCloud)**。 這會帶您 toohello 下載中心頁面下載 hello 軟體套件的程式。

    ![Microsoft Azure 備份歡迎使用畫面](./media/backup-azure-microsoft-azure-backup/dpm-venus1.png)
2. 按一下 [下載] 。

    ![下載中心 1](./media/backup-azure-microsoft-azure-backup/downloadcenter1.png)
3. 選取所有 hello 檔案，然後按一下**下一步**。 下載所有 hello hello Microsoft Azure 備份下載頁面上，從傳入的檔案和所有 hello 中的檔案的位置 hello 相同的資料夾。
   ![下載中心 1](./media/backup-azure-microsoft-azure-backup/downloadcenter.png)

    由於 hello hello 的所有檔案的下載大小一起 > 3g，10Mbps 下載連結，可能需要 too60 hello 分鐘會下載 toocomplete。

### <a name="extracting-hello-software-package"></a>正在擷取 hello 軟體套件
您已下載所有 hello 檔案之後，請按一下**MicrosoftAzureBackupInstaller.exe**。 這會啟動 hello **Microsoft Azure 備份安裝精靈**tooextract hello 安裝程式檔案 tooa 您所指定的位置。 繼續完成 hello 精靈，然後按一下 hello**擷取**按鈕 toobegin hello 擷取程序。

> [!WARNING]
> 至少 4 GB 的可用空間是必要的 tooextract hello 安裝程式檔案。
>
>

![Microsoft Azure 備份安裝精靈](./media/backup-azure-microsoft-azure-backup/extract/03.png)

一次 hello 擷取程序完成，核取 hello 方塊 toolaunch hello 全新擷取*setup.exe* toobegin 安裝 Microsoft Azure 備份伺服器，然後按一下 [hello**完成**] 按鈕。

### <a name="installing-hello-software-package"></a>安裝 hello 軟體套件
1. 按一下**Microsoft Azure 備份**toolaunch hello 安裝精靈。

    ![Microsoft Azure 備份安裝精靈](./media/backup-azure-microsoft-azure-backup/launch-screen2.png)
2. 在 [hello 歡迎使用] 畫面上按一下 [hello**下一步**] 按鈕。 這會帶您 toohello *Prerequisite Checks* > 一節。 在這個畫面上，按一下 hello**檢查**按鈕 toodetermine，如果已符合 hello 的 Azure 備份伺服器的硬體和軟體必要條件。 如果成功已符合所有先決條件都已 hello，您會看到訊息指出該 hello 機器符合 hello 需求。 按一下 hello**下一步** 按鈕。

    ![Azure 備份伺服器 - 歡迎使用和必要條件檢查](./media/backup-azure-microsoft-azure-backup/prereq/prereq-screen2.png)
3. Microsoft Azure 備份伺服器需要 SQL Server Standard，並需要 hello 適當 SQL Server 二進位檔隨附配套 hello Azure 備份伺服器的安裝套件。 當開始處理新的 Azure 備份伺服器安裝，您就應該挑選 hello 選項**此安裝程式以安裝新的 SQL Server 執行個體**按一下 hello**檢查並安裝** 按鈕。 已順利安裝 hello 先決條件、 後按一下**下一步**。

    ![Azure 備份伺服器 - SQL 檢查](./media/backup-azure-microsoft-azure-backup/sql/01.png)

    如果與建議 toorestart hello 機器發生失敗，執行這項操作，然後按一下**再檢查一次**。

   > [!NOTE]
   > Azure 備份伺服器不會使用遠端 SQL Server 執行個體。 hello 執行個體正在使用 Azure 備份伺服器需要 toobe 本機。
   >
   >

4. 提供 hello 安裝 Microsoft Azure 備份伺服器檔案位置，然後按一下 **下一步**。

    ![Microsoft Azure 備份必要條件 2](./media/backup-azure-microsoft-azure-backup/space-screen.png)

    hello 臨時位置是 tooAzure 備份的需求。 請確定 hello 臨時位置是在至少 5%的 hello 資料計劃 toobe toohello 雲端備份。 對於磁碟保護，不同的磁碟需要 toobe hello 安裝完成之後設定。 如需有關存放集區的詳細資訊，請參閱 [設定存放集區和磁碟儲存體](https://technet.microsoft.com/library/hh758075.aspx)。
5. 為受限的本機使用者帳戶提供強式密碼，按 [下一步] 。

    ![Microsoft Azure 備份必要條件 2](./media/backup-azure-microsoft-azure-backup/security-screen.png)
6. 選取您要讓 toouse *Microsoft Update*更新，然後按一下 toocheck**下一步**。

   > [!NOTE]
   > 我們建議您使用 Windows Update 重新導向 tooMicrosoft 更新，這適用於 Windows 和 Microsoft Azure 備份伺服器等其他產品提供安全性與重要更新。
   >
   >

    ![Microsoft Azure 備份必要條件 2](./media/backup-azure-microsoft-azure-backup/update-opt-screen2.png)
7. 檢閱 hello*設定摘要*按一下**安裝**。

    ![Microsoft Azure 備份必要條件 2](./media/backup-azure-microsoft-azure-backup/summary-screen.png)
8. 在階段中，發生 hello 安裝。 在第一個階段 hello hello 是 hello 伺服器上安裝 Microsoft Azure Recovery Services Agent。 hello 精靈也會檢查網際網路連線。 如果網際網路連線功能才能繼續安裝，如果沒有，您必須 tooprovide proxy 詳細資料 tooconnect toohello 網際網路。

    hello 下一個步驟為 tooconfigure hello Microsoft Azure Recovery Services Agent。 Hello 組態的一部分，您必須 tooprovide 您 hello 保存庫認證 tooregister hello 機器 toohello 備份保存庫。 您也會提供 Azure 與您內部部署之間傳送的複雜密碼 tooencrypt/解密 hello 資料。 您可以自動產生複雜密碼，或提供您自己的複雜密碼，最少 16 個字元。 必須已設定 hello 代理程式才能繼續 hello 精靈。

    ![Azure 備份伺服器必要條件 2](./media/backup-azure-microsoft-azure-backup/mars/04.png)
9. 一旦成功完成註冊 hello Microsoft Azure 備份伺服器，hello 整體安裝精靈會繼續 toohello 安裝及設定 SQL Server 和 hello Azure 備份伺服器元件。 Hello SQL Server 元件安裝完成之後，請安裝 hello Azure 備份伺服器元件。

    ![Azure 備份伺服器](./media/backup-azure-microsoft-azure-backup/final-install/venus-installation-screen.png)

Hello 安裝步驟完成時，hello 產品的桌面圖示將會建立以及。 只要連按兩下 hello 圖示 toolaunch hello 產品。

### <a name="add-backup-storage"></a>新增備份儲存體
hello 的第一個備份複本就會保留連接的存放裝置 toohello Azure 備份伺服器電腦上。 如需有關新增磁碟的詳細資訊，請參閱 [設定存放集區和磁碟儲存體](https://technet.microsoft.com/library/hh758075.aspx)。

> [!NOTE]
> 您需要 tooadd 備份儲存體，即使您打算 toosend 資料 tooAzure。 在 Azure 備份伺服器 hello 目前架構，hello Azure 備份保存庫保存 hello*第二個*hello 資料時 hello 本機儲存體保存 hello 第一個 （且強制） 備份副本。  
>
>

## <a name="4-network-connectivity"></a>4.網路連線
![步驟 4](./media/backup-azure-microsoft-azure-backup/step4.png)

Azure 備份伺服器已成功要求 hello 產品 toowork 連接 toohello Azure 備份的服務。 toovalidate hello 機器具有 hello 連線 tooAzure，是否使用 hello ```Get-DPMCloudConnection``` hello Azure 備份伺服器 PowerShell 主控台中的 cmdlet。 如果 hello hello cmdlet 的輸出則為 TRUE，則有連線存在，否則都沒有連線。

在 hello toobe 處於狀況良好的狀態需要相同的時間，hello Azure 訂用帳戶。 toofind 出 hello 狀態的訂用帳戶和 toomanage 它登入 toohello[訂用帳戶入口網站](https://account.windowsazure.com/Subscriptions)。

一旦您知道 hello hello Azure 的連線和 hello Azure 訂用帳戶的狀態，您可以使用下方 toofind 出 hello 影響的 hello 資料表上提供的 hello 備份/還原功能。

| 連線狀態 | Azure 訂閱 | 備份 tooAzure | 備份 toodisk | 從 Azure 還原 | 從磁碟還原 |
| --- | --- | --- | --- | --- | --- |
| 連線 |Active |允許 |允許 |允許 |允許 |
| 連線 |已過期 |已停止 |已停止 |允許 |允許 |
| 連線 |已取消佈建 |已停止 |已停止 |已停止且已刪除 Azure 復原點 |已停止 |
| 連線中斷 > 15 天 |Active |已停止 |已停止 |允許 |允許 |
| 連線中斷 > 15 天 |已過期 |已停止 |已停止 |允許 |允許 |
| 連線中斷 > 15 天 |已取消佈建 |已停止 |已停止 |已停止且已刪除 Azure 復原點 |已停止 |

### <a name="recovering-from-loss-of-connectivity"></a>從連線中斷的情況復原
如果您有防火牆或 proxy，導致無法存取 tooAzure，您需要遵循 hello 防火牆/proxy 設定檔中的網域位址 toowhitelist hello:

* www.msftncsi.com
* \*.Microsoft.com
* \*.WindowsAzure.com
* \*.microsoftonline.com
* \*.windows.net

一旦連線 tooAzure 已還原的 toohello Azure 備份伺服器的電腦，可以執行的 hello 作業取決於 hello Azure 訂用帳戶狀態。 上述的 hello 資料表有允許一旦 hello 機器 「 連線 」 的 hello 作業有關的詳細資料。

### <a name="handling-subscription-states"></a>處理訂用帳戶狀態
它是從 Azure 訂用帳戶可能 tootake*已過期*或*Deprovisioned*狀態 toohello *Active*狀態。 但是這有一些影響 hello 產品行為時 hello 狀態不是*Active*:

* A *Deprovisioned*訂用帳戶進行解除佈建的 hello 期間失去功能。 在開啟*Active*，hello 產品功能的備份/還原已恢復。 hello hello 本機磁碟上的備份資料也可以擷取如果它保留為夠大的保留期間。 不過，hello Azure 中的備份資料永久遺失一旦為 hello 訂閱就會進入 hello *Deprovisioned*狀態。
* 「已過期」的訂用帳戶只有在恢復「作用中」狀態之前會失去功能。 Hello 訂閱任何備份排定 hello 期間已*已過期*將不會執行。

## <a name="troubleshooting"></a>疑難排解
如果在 hello 安裝階段 （或備份或還原），Microsoft Azure 備份伺服器失敗但發生錯誤，請參閱 toothis[文件時發生錯誤代碼](https://support.microsoft.com/kb/3041338)如需詳細資訊。
您也可以使用參照太[Azure Backup 的相關常見問題集](backup-azure-backup-faq.md)

## <a name="next-steps"></a>後續步驟
您可以取得詳細的資訊， [DPM 的環境準備](https://technet.microsoft.com/library/hh758176.aspx)hello Microsoft TechNet 網站上。 其中也包含可據以部署和使用 Azure 備份伺服器之支援組態的相關資訊。

您可以使用這些文章 toogain 更深入瞭解使用 Microsoft Azure 備份伺服器工作負載保護。

* [SQL Server 備份](backup-azure-backup-sql.md)
* [SharePoint 伺服器備份](backup-azure-backup-sharepoint.md)
* [替代伺服器備份](backup-azure-alternate-dpm-server.md)
