---
title: "設定 Windows 伺服器或工作站 tooAzure （傳統模型） aaaBack |Microsoft 文件"
description: "備份 Windows 伺服器或用戶端 tooa 備份保存庫在 Azure 中。 通過基本概念，來保護檔案和資料夾 tooa 備份保存庫使用 hello Azure Backup agent。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "備份保存庫；備份 Windows Server；備份Windows；"
ms.assetid: 3b543bfd-8978-4f11-816a-0498fe14a8ba
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: c8f2a9bed1e5885f5c272c65b9282ededc05850a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-workstation-tooazure-using-hello-classic-portal"></a>備份使用 hello 傳統入口網站的 Windows 伺服器或工作站 tooAzure
> [!div class="op_single_selector"]
> * [傳統入口網站](backup-configure-vault-classic.md)
> * [Azure 入口網站](backup-configure-vault.md)
>
>

本文涵蓋 hello 程序，您需要 toofollow tooprepare 您的環境，並將 Windows 伺服器 （或工作站） tooAzure 備份。 它還涵蓋部署備份解決方案的考量。 如果您想要在第一次嘗試 hello Azure 備份，這篇文章快速引導您 hello 程序。

Azure 建立和處理資源的部署模型有二種：資源管理員和傳統。 本文說明如何使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

## <a name="before-you-start"></a>開始之前
伺服器或用戶端 tooAzure tooback，您需要 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立 [免費帳戶](https://azure.microsoft.com/free/) 。

## <a name="create-a-backup-vault"></a>建立備份保存庫
tooback 檔案及資料夾從伺服器或用戶端，您需要 toocreate hello toostore hello 資料所在的地理區域的備份保存庫。

> [!IMPORTANT]
> 從開始 2017 年 3 月，您無法再使用 hello 傳統入口網站 toocreate 備份保存庫。
>
> 您現在可以升級您備份保存庫 tooRecovery 服務保存庫。 如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。 Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。<br/> **2017 年 10 月 15，**，您將不再能夠 toouse PowerShell toocreate 備份保存庫。 <br/> **自 2017 年 11 月 1 日起**：
>- 任何其餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。
>- 您將無法 tooaccess hello 傳統入口網站中無法備份資料。 相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。
>


## <a name="download-hello-vault-credential-file"></a>下載 hello 保存庫認證檔案
必須先驗證用戶端向備份保存庫可以備份資料 tooAzure toobe hello 在內部部署的機器。 hello 驗證透過來達成*保存庫認證*。 透過從 hello 傳統入口網站的安全通道會下載 hello 保存庫認證檔案。 hello 憑證私密金鑰不會保存在 hello 入口網站或 hello 服務中。

### <a name="toodownload-hello-vault-credential-file-tooa-local-machine"></a>toodownload hello 保存庫認證檔案 tooa 本機電腦
1. 在 hello 左側瀏覽窗格中，按一下 **復原服務**，然後選取您所建立的 hello 備份保存庫。

    ![IR 已完成](./media/backup-configure-vault-classic/rs-left-nav.png)
2. 在 hello 快速入門 頁面上，按一下 **下載保存庫認證**。

   hello 傳統入口網站會使用組合的 hello 保存庫名稱和 hello 目前的日期，以產生保存庫認證。 hello 保存庫認證檔案 hello 註冊工作流程期間只會使用，且 48 小時後到期。

   hello 保存庫認證檔案可以從 hello 入口網站下載。
3. 按一下**儲存**toodownload hello 保存庫認證檔案 toohello 下載 資料夾的 hello 本機帳戶。 您也可以選取**存**從 hello**儲存**功能表 toospecify hello 保存庫認證檔案的位置。

   > [!NOTE]
   > 請確定 hello 保存庫認證檔案會儲存在可從您的電腦存取的位置。 如果它儲存在檔案共用或伺服器訊息區塊，確認您擁有 hello 權限 tooaccess 它。
   >
   >

## <a name="download-install-and-register-hello-backup-agent"></a>下載、 安裝及註冊 hello 備份代理程式
您建立備份保存庫 hello 和下載 hello 保存庫認證檔案之後，代理程式必須安裝在每一部 Windows 電腦上。

### <a name="toodownload-install-and-register-hello-agent"></a>toodownload，安裝及註冊 hello 代理程式
1. 按一下**復原服務**，然後選取您想要與伺服器 tooregister hello 備份保存庫。
2. 在 hello 快速入門] 頁面上，按一下 [hello 代理程式**代理程式適用於 Windows Server 或 System Center Data Protection Manager 或 Windows 用戶端**。 然後按一下 [儲存] 。

    ![儲存代理程式](./media/backup-configure-vault-classic/agent.png)
3. Hello MARSagentinstaller.exe 檔案下載之後，請按一下**執行**(或按兩下**MARSAgentInstaller.exe**從 hello 儲存位置)。
4. 選擇 hello 安裝資料夾，以及所需的 hello 代理程式，快取資料夾，然後按一下**下一步**。 您指定的 hello 快取位置必須有可用空間等於 tooat hello 備份資料的最少 5%。
5. 您可以繼續 tooconnect toohello 網際網路透過 hello 預設 proxy 設定。             如果您使用 proxy 伺服器 tooconnect toohello 網際網路，hello Proxy 組態 頁面上，選取 hello**使用自訂 proxy 設定**核取方塊，，，然後輸入 hello proxy 伺服器的詳細資料。 如果您使用驗證的 proxy 時，輸入 hello 使用者名稱和密碼的詳細資訊，，然後按一下**下一步**。
6. 按一下**安裝**toobegin hello 代理程式安裝。 hello 備份代理程式安裝.NET Framework 4.5 和 Windows PowerShell （如果尚未安裝） toocomplete hello 安裝。
7. Hello 代理程式安裝之後，請按一下**繼續 tooRegistration** toocontinue 與 hello 的工作流程。
8. 在 hello 保存庫識別 頁面上，瀏覽 tooand 選取 hello 保存庫認證檔案，您先前下載。

    hello 保存庫認證檔案無效只 48 個小時之後從 hello 入口網站下載。 如果您遇到錯誤，在此頁面 （例如 「 保存庫認證檔案，提供已過期 」），登入 toohello 入口網站，並再次下載 hello 保存庫認證檔案。

    確定該 hello 保存庫認證檔案可用在 hello 安裝應用程式可以存取的位置。 如果您遇到與存取相關的錯誤，將複製 hello 保存庫認證檔 tooa 暫存位置的相同電腦，然後重試 hello 作業 hello。

    如果您遇到的保存庫認證錯誤，例如 「 無效的保存庫認證提供 」，hello 檔案已損毀，或沒有不 hello 與 hello 復原服務相關聯的最新認證。 Hello 作業之後從 hello 入口網站下載新的保存庫認證檔案重試一次。 如果使用者按一下 hello，也會發生此錯誤**下載保存庫認證**中快速且連續數次的選項。 在此情況下，只有 hello 最後一個保存庫認證檔案無效。
9. 在 hello 加密設定 頁面上，您可以產生複雜密碼，或提供複雜密碼 （至最少 16 個字元）。 請記住 toosave hello 複雜密碼，在安全的位置。
10. 按一下 [完成] 。 hello 註冊伺服器精靈 」 會登錄 hello 伺服器備份。

    > [!WARNING]
    > 如果您遺失或忘記 hello 複雜密碼時，Microsoft 無法協助您復原 hello 備份資料。 您擁有 hello 加密複雜密碼，而 Microsoft 並沒有您所使用的 hello 複雜密碼的可視性。 因為它會在需要復原作業期間，請將 hello 檔案儲存在安全的位置。
    >
    >

11. 設定 hello 加密金鑰之後，保留 hello**啟動 Microsoft Azure Recovery Services Agent**核取方塊，然後**關閉**。

## <a name="complete-hello-initial-backup"></a>完整的 hello 初始備份
hello 初始備份包含兩個主要工作：

* 正在建立 hello 備份排程
* 備份檔案和資料夾進行 hello 第一次

Hello 備份原則完成 hello 初始備份之後，它會建立您需要 toorecover hello 資料時，您可使用的備份點。 hello 備份原則會根據您定義的 hello 排程。

### <a name="tooschedule-hello-backup"></a>tooschedule hello 備份
1. 開啟 hello Microsoft Azure 備份代理程式。 (它會開啟自動保留 hello**啟動 Microsoft Azure Recovery Services Agent**關閉 hello 註冊伺服器精靈時選取核取方塊。)您可以透過在您的電腦中搜尋 **Microsoft Azure 備份**來找出備份。

    ![啟動 hello Azure 備份代理程式](./media/backup-configure-vault-classic/snap-in-search.png)
2. 在 hello 備份代理程式，按一下 **排程備份**。

    ![Windows Server 備份排程](./media/backup-configure-vault-classic/schedule-backup-close.png)
3. 在 [hello 上開始使用 hello 排程備份精靈] 頁面中，按一下**下一步**。
4. 在 hello 選取項目 tooBackup 頁面上，按一下 **新增的項目**。
5. 選取 hello 檔案和資料夾，您想 tooback、，然後按一下**好**。
6. 按一下 [下一步] 。
7. 在 hello**指定備份排程**頁面上，指定 hello**備份排程**按一下**下一步**。

    您可以排程每日 (一天最多三次) 或每週備份。

    ![Windows Server 備份項目](./media/backup-configure-vault-classic/specify-backup-schedule-close.png)

   > [!NOTE]
   > 如需有關如何 toospecify hello 備份排程的詳細資訊，請參閱 hello 文章[使用 Azure Backup tooreplace 磁帶基礎結構](backup-azure-backup-cloud-as-tape.md)。
   >
   >

8. 在 hello**選取保留原則**頁面上，選取 hello**保留原則**為 hello 備份副本。

    hello 保留原則會指定儲存 hello 備份 hello 持續時間。 而不是只指定 「 一般原則 」 的所有備份的點，您可以指定不同的保留原則根據 hello 備份發生時。 您可以修改 hello 每日、 每週、 每月和每年保留原則 toomeet 您的需求。
9. 在 [hello 選擇初始備份類型] 頁面上，選擇 hello 初始備份類型。 保留 hello 選項**自動透過網路 hello**選取，然後再按一下**下一步**。

    您可以備份自動 hello 網路上或您可以離線備份。 hello 本文其餘部分說明 hello 程序會自動備份。 如果您偏好 toodo 離線備份，請檢閱 hello 文件[Azure Backup 中的離線備份工作流程](backup-azure-backup-import-export.md)如需詳細資訊。
10. 在 hello 確認頁面上，檢閱 hello 資訊，然後再按一下**完成**。
11. Hello 精靈可讓您完成建立 hello 備份排程後，按一下**關閉**。

### <a name="enable-network-throttling-optional"></a>啟用網路節流 (選擇性)
hello 備份代理程式會提供網路節流設定。 節流會控制資料傳輸期間的網路頻寬使用方式。 如果您需要 tooback 資料在工作時間，但不是想將備份程序 toointerfere hello 與其他的網際網路流量，此控制項可以是很有幫助。 節流設定會套用 tooback 和還原活動。

**tooenable 網路節流設定**

1. 在 hello 備份代理程式，按一下 **變更屬性**。

    ![變更屬性](./media/backup-configure-vault-classic/change-properties.png)
2. 在 hello**節流**索引標籤，選取 hello**啟用網際網路頻寬使用節流設定的備份操作**核取方塊。

    ![網路節流](./media/backup-configure-vault-classic/throttling-dialog.png)
3. 啟用節流設定後，指定允許的頻寬的備份資料傳輸期間的 hello**上班**和**非工作小時**。

    hello 頻寬值開始每秒 (Kbps) 為 512 kb，最高 too1，023 mb / 秒 (MBps)。 也可以指定 hello 開始和完成**上班**，和 hello 一週的哪幾天都視為的工作日。 指定之工作時間以外的時間則視為非工作時間。
4. 按一下 [確定] 。

### <a name="tooback-up-now"></a>現在向上 tooback
1. 在 hello 備份代理程式，按一下 **立即備份**toocomplete hello 初始植入 hello 網路上。

    ![Windows Server 立即備份](./media/backup-configure-vault-classic/backup-now.png)
2. 在 hello 確認頁面上，檢閱 hello 立即備份精靈的 hello 設定會使用 tooback hello 機器。 然後按一下 [備份] 。
3. 按一下**關閉**tooclose hello 精靈。 如果 hello 備份程序完成之前，您可以這樣做，hello 精靈會繼續 toorun hello 背景。

Hello 初始備份完成後，hello**作業已完成**hello Backup 主控台中顯示的狀態。

![IR 已完成](./media/backup-configure-vault-classic/ircomplete.png)

## <a name="next-steps"></a>後續步驟
* 註冊 [免費的 Azure 帳戶](https://azure.microsoft.com/free/)。

如需備份 VM 或其他工作負載的詳細資訊，請參閱︰

* [備份 IaaS VM](backup-azure-vms-prepare.md)
* [備份工作負載 tooAzure 與 Microsoft Azure 備份伺服器](backup-azure-microsoft-azure-backup.md)
* [備份與 DPM 工作負載 tooAzure](backup-azure-dpm-introduction.md)
