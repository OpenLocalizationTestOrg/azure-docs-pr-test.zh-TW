---
title: "設定工作負載 tooAzure aaaUse Azure 備份伺服器 tooback |Microsoft 文件"
description: "使用 Azure 備份伺服器 tooprotect 或備份工作負載 toohello Azure 入口網站。"
services: backup
documentationcenter: 
author: PVRK
manager: shivamg
editor: 
keywords: "Azure 備份伺服器; 保護工作負載; 備份工作負載"
ms.assetid: e7fb1907-9dc1-4ca1-8c61-50423d86540c
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.openlocfilehash: a99b2919ffd44c6133960e3a935038a2bb1281c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-using-azure-backup-server"></a>準備使用 Azure 備份伺服器的工作負載備份 tooback
> [!div class="op_single_selector"]
> * [Azure 備份伺服器](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
>
>

這篇文章說明如何 tooprepare 使用 Azure 備份伺服器的工作負載備份您的環境 tooback。 透過 Azure 備份伺服器，您將可從單一主控台保護 Hyper-V VM、Microsoft SQL Server、SharePoint Server、Microsoft Exchange 和 Windows 用戶端等應用程式工作負載。

> [!NOTE]
> Azure 備份伺服器現在可以保護 VMware VM，並提供改善的安全性功能。 下列; 的 hello 章節所述安裝 hello 產品套用 Update 1 和 hello 最新的 Azure 備份代理程式。 toolearn 深入了解備份 VMware 伺服器使用 Azure 備份伺服器，請參閱 hello 文章[VMware 伺服器使用 Azure 備份伺服器 tooback](backup-azure-backup-server-vmware.md)。 toolearn 有關安全性功能，請參閱太[Azure 備份的安全性功能的文件](backup-azure-security-feature.md)。
>
>

您也可以保護基礎結構即服務 (IaaS) 工作負載，例如 Azure 中的 VM。

> [!NOTE]
> Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。 本文章提供 hello 資訊和程序來還原使用 hello 資源管理員的模型部署的 Vm。
>
>

Azure 備份伺服器會繼承許多 hello 工作負載備份功能從 Data Protection Manager (DPM)。 這篇文章會連結 tooDPM 文件 tooexplain 某些 hello 共用功能。 雖然 Azure 備份伺服器共用許多 hello 與 DPM 相同的功能。 Azure 備份伺服器並不會備份 tootape，也不可以與 System Center 整合。

## <a name="1-choose-an-installation-platform"></a>1.選擇安裝平台
hello 向 Azure 備份伺服器 hello 快速安裝和執行的第一個步驟是 tooset Windows 伺服器。 伺服器可以位於 Azure 或內部部署中。

### <a name="using-a-server-in-azure"></a>使用 Azure 中的伺服器
在選擇用來執行 Azure 備份伺服器的伺服器時，建議您從 Windows Server 2012 R2 Datacenter 的資源庫映像來開始。 hello 文章[hello Azure 入口網站中建立第一個 Windows 虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)，提供的教學課程，開始使用 hello 建議虛擬機器，在 Azure 中，即使您從未使用過 Azure 之前。 hello 建議的最低需求 hello server 虛擬機器 (VM) 應該是： A2 標準與兩個核心，3.5 GB RAM。

使用 Azure 備份伺服器保護工作負載有許多細節需要注意。 hello 文章[安裝 DPM 作為 Azure 虛擬機器](https://technet.microsoft.com/library/jj852163.aspx)，可協助說明這些細節。 在部署之前 hello 機器，請完整閱讀這篇文章。

### <a name="using-an-on-premises-server"></a>使用內部部署伺服器
如果您不想在 Azure 中的 toorun hello 基底伺服器，您可以在 HYPER-V 虛擬機器、 VMware VM 或實體主機上執行 hello 伺服器。 hello 建議 hello 伺服器硬體的最低需求是兩個核心和 4 GB RAM。 hello 下表列出支援的 hello 作業系統：

| 作業系統 | 平台 | SKU |
|:--- | --- |:--- |
| Windows Server 2012 R2 和最新的 SP |64 位元 |Standard、Datacenter、Foundation |
| Windows Server 2012 和最新的 SP |64 位元 |Datacenter、Foundation、Standard |
| Windows Storage Server 2012 R2 和最新的 SP |64 位元 |Standard、Workgroup |
| Windows Storage Server 2012 和最新的 SP |64 位元 |Standard、Workgroup |

您可以使用 hello DPM 存放裝置使用 Windows Server 重複資料刪除重複資料刪除。 深入了解在 Hyper-V VM 中部署時， [DPM 和重複資料刪除](https://technet.microsoft.com/library/dn891438.aspx) 如何搭配運作。

> [!NOTE]
> Azure 備份伺服器是設計的 toorun 專用、 單一用途伺服器上。 您無法在下列位置安裝 Azure 備份伺服器︰
> - 執行為網域控制站的電腦
> - 哪些 hello 應用程式伺服器安裝角色的電腦
> - 本身是 System Center Operations Manager 管理群組的電腦
> - Exchange Server 執行所在的電腦
> - 本身是叢集節點的電腦

一律加入 Azure 備份伺服器 tooa 網域。 如果您計劃 toomove hello 伺服器 tooa 不同網域時，建議您在安裝 Azure 備份伺服器之前加入 hello 伺服器 toohello 新網域。 部署之後移動現有的 Azure 備份伺服器機器 tooa 新網域*不支援*。

## <a name="2-recovery-services-vault"></a>2.復原服務保存庫
當您傳送 tooAzure 備份資料，或將它保留在本機，需要連接 toobe tooAzure hello 軟體。 toobe 更明確，必須向復原服務保存庫的 toobe hello Azure 備份伺服器的機器。

toocreate 復原服務保存庫：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 在 hello 中樞功能表中，按一下 **瀏覽**hello 清單中的資源，在輸入**復原服務**。 當您開始輸入 hello 清單會篩選根據您的輸入。 按一下 [復原服務保存庫] 。

    ![建立復原服務保存庫的步驟 1](./media/backup-azure-microsoft-azure-backup/open-recovery-services-vault.png) <br/>

    復原服務保存庫的 hello 清單隨即顯示。
3. 在 hello**復原服務保存庫**功能表上，按一下 **新增**。

    ![建立復原服務保存庫的步驟 2](./media/backup-azure-microsoft-azure-backup/rs-vault-menu.png)

    hello 復原服務保存庫刀鋒視窗隨即開啟，提示您 tooprovide**名稱**，**訂用帳戶**，**資源群組**，和**位置**。

    ![建立復原服務保存庫的步驟 5](./media/backup-azure-microsoft-azure-backup/rs-vault-attributes.png)
4. 如**名稱**，輸入好記名稱 tooidentify hello 保存庫。 hello 名稱必須 toobe 唯一 hello Azure 訂用帳戶。 輸入包含 2 到 50 個字元的名稱。 該名稱必須以字母開頭，而且只可以包含字母、數字和連字號。
5. 按一下**訂用帳戶**toosee hello 可用訂閱清單。 如果您不確定哪一個訂用帳戶 toouse，使用預設的 hello （或建議） 訂用帳戶。 只有在您的組織帳戶與多個 Azure 訂用帳戶相關聯時，才會有多個選擇。
6. 按一下**資源群組**toosee hello 可用的資源群組的清單，或按一下**新增**toocreate 新的資源群組。 如需資源群組的完整資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)
7. 按一下**位置**hello 保存庫的 tooselect hello 地理區域。
8. 按一下 [建立] 。 它可能需要一段復原服務保存庫建立 toobe hello。 監視 hello 上方右側的區域在 hello 入口網站中的 hello 狀態通知。
   一旦建立您的保存庫，它會在 hello 入口網站中開啟。

### <a name="set-storage-replication"></a>設定儲存體複寫
hello 儲存體複寫選項可讓您 toochoose 地理備援儲存體和本機備援儲存體之間。 根據預設，保存庫具有異地備援儲存體。 如果此保存庫是您主要的保存庫，將 hello 儲存體選項集 toogeo 備援儲存體。 如果您想要更便宜但不持久的選項，請選擇本地備援儲存體。 深入了解[異地備援](../storage/common/storage-redundancy.md#geo-redundant-storage)和[本機備援](../storage/common/storage-redundancy.md#locally-redundant-storage)儲存選項的 hello [Azure 儲存體複寫概觀](../storage/common/storage-redundancy.md)。

tooedit hello 儲存體複寫設定：

1. 選取保存庫 tooopen hello 保存庫儀表板與 hello 設定 刀鋒視窗。 如果 hello**設定**刀鋒視窗未開啟，請按一下**所有設定**hello 保存庫儀表板中。
2. 在 hello**設定**刀鋒視窗中，按一下 **備份基礎結構** > **備份設定**tooopen hello**備份設定**刀鋒視窗。 在 hello**備份設定**刀鋒視窗中，選擇您的保存庫的 hello 存放裝置複寫選項。

    ![備份保存庫的清單](./media/backup-azure-vms-first-look-arm/choose-storage-configuration-rs-vault.png)

    選擇您的保存庫的 hello 儲存體選項之後，您就準備好 tooassociate hello VM 與 hello 保存庫。 toobegin hello 關聯，您應該探索及註冊 hello Azure 虛擬機器。

## <a name="3-software-package"></a>3.軟體封裝
### <a name="downloading-hello-software-package"></a>下載 hello 軟體套件
1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 如果您已經開啟的復原服務保存庫，繼續 toostep 3。 如果您不需要復原服務保存庫開啟之後，但在 hello hello 中樞功能表中，在 Azure 入口網站中按一下**瀏覽**。

   * 在 [hello] 清單中的資源，輸入**復原服務**。
   * 當您開始輸入 hello 清單會篩選器根據您的輸入。 當您看到 [復原服務保存庫] 時，請按一下它。

     ![建立復原服務保存庫的步驟 1](./media/backup-azure-microsoft-azure-backup/open-recovery-services-vault.png)

     復原服務保存庫 hello 清單隨即出現。
   * 從 hello 清單的 復原服務保存庫中，選取保存庫。

     hello 選取保存庫儀表板隨即開啟。

     ![開啟 [保存庫] 刀鋒視窗](./media/backup-azure-microsoft-azure-backup/vault-dashboard.png)
3. hello**設定**刀鋒視窗，預設會開啟。 如果它已關閉，按一下 [上**設定**tooopen hello 設定] 刀鋒視窗。

    ![開啟 [保存庫] 刀鋒視窗](./media/backup-azure-microsoft-azure-backup/vault-setting.png)
4. 按一下**備份**tooopen hello 入門精靈 」。

    ![備份開始使用](./media/backup-azure-microsoft-azure-backup/getting-started-backup.png)

    在 hello**開始使用備份**刀鋒視窗中開啟，**備份目標**將會自動選取。

    ![Backup-goals-default-opened](./media/backup-azure-microsoft-azure-backup/getting-started.png)

5. 在 hello**備份目標**刀鋒視窗中的，從 hello**您的工作負載執行**功能表上，選取**內部**。

    ![內部部署和做為目標的工作負載](./media/backup-azure-microsoft-azure-backup/backup-goals-azure-backup-server.png)

    從 hello**怎麼辦想 toobackup？**下拉式功能表、 選取 hello 工作負載 tooprotect 使用 Azure 備份伺服器，然後再按一下**確定**。

    hello**開始使用備份**精靈參數 hello**準備基礎結構**選項 tooback 向上 tooAzure 工作負載。

   > [!NOTE]
   > 如果您只想 tooback 檔案及資料夾，我們建議使用 hello Azure 備份代理程式，並遵循 hello 文章中的 hello 指引[第一印象： 備份檔案和資料夾](backup-try-azure-backup-in-10-mins.md)。 如果您正在 tooprotect 多個檔案和資料夾，或您計劃 tooexpand hello 保護需要 hello 未來，選取這些工作負載。
   >
   >

    ![開始使用精靈變更](./media/backup-azure-microsoft-azure-backup/getting-started-prep-infra.png)

6. 在 hello**準備基礎結構**刀鋒視窗隨即開啟，按一下 hello**下載**的連結安裝 Azure 備份伺服器，以及下載保存庫認證。 您的 Azure 備份伺服器 toohello 復原服務保存庫註冊期間使用 hello 保存庫認證。 hello 連結會帶領您 toohello 下載中心其中 hello 軟體可以下載套件。

    ![準備用於 Azure 備份伺服器的基礎結構](./media/backup-azure-microsoft-azure-backup/azure-backup-server-prep-infra.png)

7. 選取所有 hello 檔案，然後按一下**下一步**。 下載所有 hello hello Microsoft Azure 備份下載頁面上，從傳入的檔案和所有 hello 中的檔案的位置 hello 相同的資料夾。

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
2. 在 [hello 歡迎使用] 畫面上按一下 [hello**下一步**] 按鈕。 這會帶您 toohello *Prerequisite Checks* > 一節。 在這個畫面上，按一下 **檢查**toodetermine 如果已符合 hello 的 Azure 備份伺服器的硬體和軟體必要條件。 如果符合所有先決條件都已成功，您會看到訊息指出該 hello 機器符合 hello 需求。 按一下 hello**下一步** 按鈕。

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

    hello 下一個步驟為 tooconfigure hello Microsoft Azure Recovery Services Agent。 Hello 組態的一部分，您必須 tooprovide 您保存庫認證 tooregister hello 機器 toohello 復原服務保存庫。 您也會提供 Azure 與您內部部署之間傳送的複雜密碼 tooencrypt/解密 hello 資料。 您可以自動產生複雜密碼，或提供您自己的複雜密碼，最少 16 個字元。 必須已設定 hello 代理程式才能繼續 hello 精靈。

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
