---
title: "工作負載 tooAzure 入口網站註冊 aaaUse DPM tooback |Microsoft 文件"
description: "DPM 伺服器使用 hello Azure 備份服務簡介 toobacking"
services: backup
documentationcenter: 
author: adigan
manager: nkolli
editor: 
keywords: "System Center Data Protection Manager, Data Protection Manager, DPM 備份"
ms.assetid: c8c322cf-f5eb-422c-a34c-04a4801bfec7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: adigan;giridham;jimpark;markgal;trinadhk
ms.openlocfilehash: 1dd988ae55012ac7dc485d2416458542c60b6ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-tooazure-with-dpm"></a>準備註冊與 DPM 工作負載 tooAzure tooback
> [!div class="op_single_selector"]
> * [Azure 備份伺服器](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Azure 備份伺服器 (傳統)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (傳統)](backup-azure-dpm-introduction-classic.md)
>
>

本文章提供簡介 toousing Microsoft Azure 備份 tooprotect System Center Data Protection Manager (DPM) 伺服器和工作負載。 在閱讀本文後，您將了解：

* Azure DPM 伺服器備份的運作方式
* hello 必要條件 tooachieve smooth 備份體驗
* hello 發生一般錯誤以及如何與它們 toodeal
* 支援的案例

> [!NOTE]
> Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。 本文章提供 hello 資訊和程序來還原使用 hello 資源管理員的模型部署的 Vm。
>
>

System Center DPM 會備份檔案和應用程式資料。 可以儲存在磁帶上，在磁碟上，或備份至 Microsoft Azure 備份 tooAzure tooDPM 所備份的資料。 DPM 與 Azure 備份的互動方式如下：

* **DPM 部署為實體伺服器或內部部署虛擬機器**— 如果 DPM 部署為實體伺服器或內部部署 HYPER-V 虛擬機器，您可以備份資料 tooa 復原服務保存庫此外 toodisk 與磁帶備份。
* **DPM 部署為 Azure 虛擬機器** — 從 System Center 2012 R2 Update 3 開始，DPM 可以部署為 Azure 虛擬機器。 如果 DPM 部署為 Azure 虛擬機器您可以備份資料 tooAzure 連接磁碟 toohello DPM Azure 虛擬機器，或您可以將 hello 資料儲存區卸載備份 tooa 復原服務保存庫。

## <a name="why-backup-from-dpm-tooazure"></a>為什麼還要備份從 DPM tooAzure 嗎？
使用 Azure 備份來備份 DPM 伺服器 hello 商業優勢包括：

* 在內部部署 DPM 部署，您可以使用 Azure 做為替代 toolong 詞彙部署 tootape。
* 若是在 Azure 中的 DPM 部署，Azure Backup 可讓您 toooffload 存放裝置與 hello Azure 磁碟，您 tooscale 向上藉由將較舊的資料儲存在復原服務保存庫，在磁碟上的新資料。

## <a name="prerequisites"></a>必要條件
準備 Azure Backup tooback DPM 資料備份，如下所示：

1. **建立復原服務保存庫** — 在 Azure 入口網站中建立保存庫。
2. **下載保存庫認證**— 下載 hello 認證使用 tooregister hello DPM 伺服器 tooRecovery 服務保存庫。
3. **安裝 Azure Backup Agent hello** — 從 Azure Backup，在每一部 DPM 伺服器上安裝 hello 代理程式。
4. **註冊伺服器 hello** — 暫存器 hello DPM 伺服器 tooRecovery 服務保存庫。

### <a name="1-create-a-recovery-services-vault"></a>1.建立復原服務保存庫
toocreate 復原服務保存庫：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 在 hello 中樞功能表中，按一下 **瀏覽**hello 清單中的資源，在輸入**復原服務**。 當您開始輸入 hello 清單會篩選器根據您的輸入。 按一下 [復原服務保存庫] 。

    ![建立復原服務保存庫的步驟 1](./media/backup-azure-dpm-introduction/open-recovery-services-vault.png)

    復原服務保存庫的 hello 清單隨即顯示。
3. 在 hello**復原服務保存庫**功能表上，按一下 **新增**。

    ![建立復原服務保存庫的步驟 2](./media/backup-azure-dpm-introduction/rs-vault-menu.png)

    hello 復原服務保存庫刀鋒視窗隨即開啟，提示您 tooprovide**名稱**，**訂用帳戶**，**資源群組**，和**位置**。

    ![建立復原服務保存庫的步驟 5](./media/backup-azure-dpm-introduction/rs-vault-attributes.png)
4. 如**名稱**，輸入好記名稱 tooidentify hello 保存庫。 hello 名稱必須 toobe 唯一 hello Azure 訂用帳戶。 輸入包含 2 到 50 個字元的名稱。 該名稱必須以字母開頭，而且只可以包含字母、數字和連字號。
5. 按一下**訂用帳戶**toosee hello 可用訂閱清單。 如果您不確定哪一個訂用帳戶 toouse，使用預設的 hello （或建議） 訂用帳戶。 只有在您的組織帳戶與多個 Azure 訂用帳戶相關聯時，才會有多個選擇。
6. 按一下**資源群組**toosee hello 可用的資源群組的清單，或按一下**新增**toocreate 新的資源群組。 如需資源群組的完整資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)
7. 按一下**位置**hello 保存庫的 tooselect hello 地理區域。
8. 按一下 [建立] 。 它可能需要一段復原服務保存庫建立 toobe hello。 監視 hello 上方右側的區域在 hello 入口網站中的 hello 狀態通知。
   一旦建立您的保存庫，它會在 hello 入口網站中開啟。

### <a name="set-storage-replication"></a>設定儲存體複寫
hello 儲存體複寫選項可讓您 toochoose 地理備援儲存體和本機備援儲存體之間。 根據預設，保存庫具有異地備援儲存體。 如果這是您主要的備份，請保留 hello 選項集 toogeo 備援儲存體。 如果您想要更便宜但不持久的選項，請選擇本地備援儲存體。 深入了解[異地備援](../storage/common/storage-redundancy.md#geo-redundant-storage)和[本機備援](../storage/common/storage-redundancy.md#locally-redundant-storage)儲存選項的 hello [Azure 儲存體複寫概觀](../storage/common/storage-redundancy.md)。

tooedit hello 儲存體複寫設定：

1. 選取保存庫 tooopen hello 保存庫儀表板與 hello 設定 刀鋒視窗。 如果 hello**設定**刀鋒視窗未開啟，請按一下**所有設定**hello 保存庫儀表板中。
2. 在 hello**設定**刀鋒視窗中，按一下 **備份基礎結構** > **備份設定**tooopen hello**備份設定**刀鋒視窗。 在 hello**備份設定**刀鋒視窗中，選擇您的保存庫的 hello 存放裝置複寫選項。

    ![備份保存庫的清單](./media/backup-azure-vms-first-look-arm/choose-storage-configuration-rs-vault.png)

    選擇您的保存庫的 hello 儲存體選項之後，您就準備好 tooassociate hello VM 與 hello 保存庫。 toobegin hello 關聯，您應該探索及註冊 hello Azure 虛擬機器。

### <a name="2-download-vault-credentials"></a>2.下載保存庫認證
hello 保存庫認證檔案是由每個備份保存庫的 hello 入口網站所產生的憑證。 hello 入口網站再上傳 hello 公用金鑰 toohello 存取控制服務 (ACS)。 hello hello 憑證私密金鑰進行可用 toohello 使用者指定做為輸入 hello 機器註冊工作流程中的 hello 工作流程的一部分。 這會驗證 hello 機器 toosend 備份資料 tooan 識別保存庫中 hello Azure 備份服務。

只有在 hello 註冊工作流程期間使用 hello 保存庫認證。 Hello 保存庫認證檔案不會洩露的 hello 使用者的責任 tooensure 它。 它會落在任何惡意使用者的 hello 未授權者手中，如果 hello 保存庫認證檔案可以使用的 tooregister 針對其他機器 hello 相同保存庫。 不過，因為 hello 備份資料已加密的複雜密碼所屬 toohello 客戶，現有的備份資料不會遭到洩漏。 toomitigate 考慮此保存庫認證中所設定 tooexpire 48hrs。 您可以下載 hello 復原服務保存庫認證任意數目的時間 – 但是只有 hello 最新的保存庫認證檔案都適用 hello 註冊工作流程期間。

透過從 hello Azure 入口網站的安全通道會下載 hello 保存庫認證檔案。 hello Azure 備份服務不會知道 hello hello 憑證私密金鑰和 hello 私密金鑰不會保存在 hello 入口網站或 hello 服務中。 使用下列步驟 toodownload hello 保存庫認證檔案 tooa 本機電腦的 hello。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 開啟復原服務保存庫 toowhich toowhich 想 tooregister DPM 電腦。
3. 根據預設，[設定] 刀鋒視窗隨即會開啟。 如果它已關閉，按一下 [上**設定**保存庫儀表板 tooopen hello 設定] 刀鋒視窗上。 在 [設定] 刀鋒視窗中，按一下 [屬性] 。

    ![開啟 [保存庫] 刀鋒視窗](./media/backup-azure-dpm-introduction/vault-settings-dpm.png)
4. Hello 屬性頁面上，按一下 **下載**下**備份認證**。 hello 入口網站會產生 hello 保存庫認證檔案，會成為可供下載。

    ![下載](./media/backup-azure-dpm-introduction/vault-credentials.png)

hello 入口網站將會產生保存庫認證使用組合的 hello 保存庫名稱和 hello 目前的日期。 按一下**儲存**toodownload hello 保存庫認證 toohello 本機帳戶的下載資料夾中，或從 hello 另存新檔選取儲存功能表 toospecify hello 保存庫認證的位置。 就會在產生的 hello 檔案 toobe tooa 分鐘。

### <a name="note"></a>注意
* 請確定該 hello 保存庫認證檔案會儲存在可從您的電腦存取的位置。 如果它儲存在檔案共用 SMB，檢查 hello 存取權限。
* 只有在 hello 註冊工作流程會使用 hello 保存庫認證檔案。
* hello 保存庫認證檔案 48hrs 後會到期，而您可以從 hello 入口網站下載。

### <a name="3-install-backup-agent"></a>3.安裝備份代理程式
應該在每個資料和應用程式的備份可讓您 Windows 電腦 （Windows Server、 Windows 用戶端、 System Center Data Protection Manager 伺服器或 Azure 備份伺服器的電腦） 上安裝代理程式建立 hello Azure 備份保存庫之後tooAzure。

1. 開啟復原服務保存庫 toowhich toowhich 想 tooregister DPM 電腦。
2. 根據預設，[設定] 刀鋒視窗隨即會開啟。 如果它已關閉，按一下 [上**設定**tooopen hello 設定] 刀鋒視窗。 在 [設定] 刀鋒視窗中，按一下 [屬性] 。

    ![開啟 [保存庫] 刀鋒視窗](./media/backup-azure-dpm-introduction/vault-settings-dpm.png)
3. 在 hello 設定頁面上，按一下 **下載**下**Azure Backup Agent**。

    ![下載](./media/backup-azure-dpm-introduction/azure-backup-agent.png)

   一旦下載 hello 代理程式之後，按兩下 MARSAgentInstaller.exe toolaunch hello 安裝 hello Azure Backup agent。 選擇 hello 安裝資料夾和 hello 代理程式所需的臨時資料夾。 指定的 hello 快取位置必須有可用空間可供至少 5%的 hello 備份資料。
4. 如果您使用 proxy 伺服器 tooconnect toohello 網際網路 hello **Proxy 組態**畫面上，輸入 hello proxy 伺服器的詳細資料。 如果您使用驗證的 proxy，請在此畫面輸入 hello 使用者名稱與密碼詳細資料。
5. hello Azure 備份代理程式會安裝 Windows PowerShell 和.NET Framework 4.5 （如果它尚未提供） toocomplete hello 安裝。
6. Hello 代理程式安裝之後，**關閉**hello 視窗。

   ![關閉](../../includes/media/backup-install-agent/dpm_FinishInstallation.png)
7. 太**暫存器 hello DPM 伺服器**toohello 保存庫，在 hello**管理** 索引標籤，按一下**線上**。 接著，選取 [註冊] 。 它會開啟 hello 註冊安裝精靈。
8. 如果您使用 proxy 伺服器 tooconnect toohello 網際網路 hello **Proxy 組態**畫面上，輸入 hello proxy 伺服器的詳細資料。 如果您使用驗證的 proxy，請在此畫面輸入 hello 使用者名稱與密碼詳細資料。

    ![Proxy 組態](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Proxy.png)
9. 在 [hello 保存庫認證] 畫面上，瀏覽 tooand 選取 hello 保存庫認證檔案先前已下載。

    ![保存庫認證](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Credentials.jpg)

    hello 保存庫認證檔案無效，只 48 小時 （下載後，從 hello 入口網站）。 如果您遇到任何錯誤，在這個畫面 （例如，「 保存庫的認證檔案，提供已過期 」），登入 toohello Azure 入口網站並下載 hello 保存庫認證檔案一次。

    確定該 hello 保存庫認證檔案可用在 hello 安裝應用程式可以存取的位置。 如果您遇到存取相關的錯誤，請複製 hello 保存庫認證檔案在這部機器 tooa 暫存位置，然後重試 hello 作業。

    如果您遇到無效的保存庫認證錯誤 （例如，「 無效的保存庫認證提供 「） hello 檔案可能已損毀或沒有不 hello 與 hello 復原服務相關聯的最新認證。 Hello 作業之後從 hello 入口網站下載新的保存庫認證檔案重試一次。 如果 hello 使用者在 hello，通常會發生這個錯誤**下載保存庫認證**hello 中快速且連續的 Azure 入口網站中的選項。 在此情況下，只有 hello 第二個保存庫認證檔案無效。
10. toocontrol hello （work) 和非工作時間，在 hello 期間的網路頻寬使用量**節流設定** 畫面上，您可以設定的 hello 頻寬使用量限制定義 hello 工作和非工作小時。

    ![節流設定](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Throttling.png)
11. 在 hello**復原資料夾設定**畫面上，瀏覽的 hello 下載的檔案從 Azure 的 hello 資料夾將會暫時分段。

    ![復原資料夾設定](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_RecoveryFolder.png)
12. 在 [hello**加密設定**] 畫面上，您可以產生複雜密碼，或提供複雜密碼 （最少 16 個字元）。 請記住 toosave hello 複雜密碼，在安全的位置。

    ![加密](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Encryption.png)

    > [!WARNING]
    > 如果 hello 已遺失或忘記複雜密碼。Microsoft 無法協助您復原 hello 備份資料。 hello 終端使用者擁有 hello 加密複雜密碼，且 Microsoft 不會顯示出來 hello hello 終端使用者所使用的複雜密碼。 請視需要執行復原作業時，請在安全的位置儲存 hello 檔案。
    >
    >
13. 一旦您按一下 hello**註冊**按鈕，hello 電腦註冊成功 toohello 保存庫，您現在已準備好 toostart tooMicrosoft Azure 備份。
14. 當使用 Data Protection Manager，您可以修改 hello，即可指定在 hello 註冊工作流程期間的 hello 設定**設定**選項選取**線上**下 hello **管理** 索引標籤。

## <a name="requirements-and-limitations"></a>需求 (和限制)
* DPM 可以做為實體伺服器或 System Center 2012 SP1 或 System Center 2012 R2 上安裝的 HYPER-V 虛擬機器來執行。 它也可以做為 System Center 2012 R2 (至少含 DPM 2012 R2 更新彙總套件 3) 上執行的 Azure 虛擬機器，或 System Center 2012 R2 (至少含更新彙總套件 5) 上執行之 VMWare 中的 Windows 虛擬機器來執行。
* 如果您使用 System Center 2012 SP1 來執行 DPM，則應該安裝 System Center Data Protection Manager SP1 的更新彙總套件 2。 這是必要的才能安裝 hello Azure Backup Agent。
* hello DPM 伺服器應該使用 Windows PowerShell 和.Net Framework 4.5 安裝。
* DPM 可以備份大部分的工作負載 tooAzure 備份。 如需完整清單，支援功能的請參閱 hello Azure Backup 支援以下項目。
* Azure 備份中儲存的資料無法復原使用 hello 「 複製 tootape 」 選項。
* 您需要 Azure 帳戶啟用 hello Azure Backup 功能。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 請閱讀 [Azure 備份定價](https://azure.microsoft.com/pricing/details/backup/)。
* 使用 Azure Backup 必須安裝在您想 tooback hello 伺服器 hello Azure Backup Agent toobe。 每個伺服器都必須有至少 5%的 hello 正在備份，可做為本機可用儲存體的 hello 資料大小。 例如，備份 100 GB 資料的最少需要 5 gb 的可用空間 hello 臨時位置。
* 資料會儲存在 hello Azure 保存庫儲存體中。 您可以備份 tooan Azure 備份保存庫的資料沒有限制 toohello 數量但 hello 大小的資料來源 （例如虛擬機器或資料庫） 不應該超過 54400 GB。

這些檔案類型支援 tooAzure 備份：

* 加密 (僅限完整備份)
* 壓縮 (支援增量備份)
* 疏鬆 (支援增量備份)
* 壓縮和疏鬆 (視為疏鬆來處理)

下列為不支援的類型：

* 不支援區分大小寫的檔案系統上的伺服器。
* 硬式連結 (略過)
* 重新分析點 (略過)
* 加密和壓縮 (略過)
* 加密和疏鬆 (略過)
* 壓縮資料流
* 疏鬆資料流

> [!NOTE]
> 從 System Center 2012 DPM sp1 及更新版本中您可以備份使用 Microsoft Azure 備份的 DPM tooAzure 所保護的工作負載。
>
>
