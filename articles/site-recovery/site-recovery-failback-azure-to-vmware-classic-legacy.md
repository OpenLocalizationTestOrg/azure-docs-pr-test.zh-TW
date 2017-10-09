---
title: "aaaFail hello 傳統舊版入口網站中從 Azure 備份 VMware Vm |Microsoft 文件"
description: "本文說明 toofail 後將 VMware 虛擬機器已複寫 tooAzure 與 Azure Site Recovery 的方式。"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: a63524bf-990c-42ee-8554-e017e6e67e68
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 5ef66b366dcdc43f3bc171e0ed1532216cc2ab89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-from-azure-toovmware-with-azure-site-recovery-legacy"></a>失敗後的 VMware 虛擬機器和實體伺服器從 Azure tooVMware 與 Azure Site Recovery （舊版）
> [!div class="op_single_selector"]
> * [Azure 入口網站](site-recovery-failback-azure-to-vmware.md)
> * [Azure 傳統入口網站](site-recovery-failback-azure-to-vmware-classic.md)
> * [Azure 傳統入口網站 (舊版)](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

本文說明如何 toofail 後 VMware 虛擬機器和 Windows/Linux 實體伺服器，從 Azure tooyour 在內部部署站台之後，您已從您內部部署複寫站台使用 tooAzure [Azure Site Recovery？](site-recovery-overview.md)。

本文說明的是舊版設定，不應用於新的保存庫。

## <a name="architecture"></a>架構
此圖表顯示 hello 容錯移轉和容錯回復案例。 hello 藍色行會 hello 容錯移轉期間使用的連接。 hello 紅線是 hello 容錯回復期間使用的連接。 有箭頭的 hello 線經過 hello 網際網路。

![](./media/site-recovery-failback-azure-to-vmware/vconports.png)

## <a name="before-you-start"></a>開始之前
* 您應該已容錯移轉您的 VMware VM 或實體伺服器，且它們應該在 Azure 中執行。
* 您應該注意，您可以只失敗後的 VMware 虛擬機器和 Azure tooVMware hello 在內部部署主要站台中的虛擬機器從 Windows/Linux 實體伺服器。  如果您正在失敗實體機器，容錯移轉 tooAzure 會將它轉換 tooan Azure VM，並容錯回復 tooVMware 會將它轉換 tooa VMware VM。

設定容錯回復的方式如下︰

1. **設定容錯回復元件**： 您將需要 tooset vContinuum 伺服器內部部署，並使之指向 toohello 組態伺服器 VM 在 Azure 中。 您也會設定處理序伺服器，為 Azure VM toosend 資料回復 toohello 在內部部署主要目標伺服器。 透過處理 hello 容錯移轉的 hello 組態伺服器註冊 hello 處理序伺服器。 您安裝內部部署主要目標伺服器。 如果您需要 Windows 主要目標伺服器，它會在您安裝 vContinuum 時自動設定。 如果您需要 Linux 需要 tooset 它以手動方式在不同的伺服器上。
2. **啟用保護和容錯回復**： 當您設定 hello 元件之後，在 vContinuum 您將需要 tooenable 保護容錯移轉 Azure Vm。 將執行整備檢查 hello Vm 上的，並從 Azure tooyour 在內部部署站台執行容錯移轉。 容錯回復完成後您重新保護內部部署機器，讓他們可以啟動複寫 tooAzure。

## <a name="step-1-install-vcontinuum-on-premises"></a>步驟 1：安裝 vContinuum 內部部署
您將需要 tooinstall vContinuum 伺服器在內部部署，而且它指向 toohello 組態伺服器。

1. [下載 vContinuum](http://go.microsoft.com/fwlink/?linkid=526305)。
2. 然後下載 hello [vContinuum 更新](http://go.microsoft.com/fwlink/?LinkID=533813)版本。
3. 安裝 vContinuum hello 最新版本。 在 hello ** 褖畫惎**頁面上，按一下**下一步**。
    ![](./media/site-recovery-failback-azure-to-vmware/image2.png)
4. 在 hello hello 精靈第一頁指定 hello CX 伺服器 IP 位址和 hello CX 伺服器連接埠。 選取 [使用 HTTPS] 。

   ![](./media/site-recovery-failback-azure-to-vmware/image3.png)
5. 尋找 hello 組態伺服器 IP 位址上 hello**儀表板**hello 組態伺服器中 Azure VM 索引標籤。
   ![](./media/site-recovery-failback-azure-to-vmware/image4.png)
6. 尋找 hello 組態伺服器 HTTPS 公用連接埠上 hello**端點**hello 組態伺服器中 Azure VM 索引標籤。

   ![](./media/site-recovery-failback-azure-to-vmware/image5.png)
7. 在 hello **CS 複雜密碼詳細資料**頁面上，指定您記下下註冊 hello 組態伺服器時的 hello 複雜密碼。 如果您不記得它簽入**c:\\Program Files (x86)\\InMage 系統\\私人\\connection.passphrase** hello 組態伺服器 VM 上。

    ![](./media/site-recovery-failback-azure-to-vmware/image6.png)
8. 在 hello**選取目的地位置**頁面上，指定您希望 tooinstall hello vContinuum 伺服器並按一下**安裝**。

   ![](./media/site-recovery-failback-azure-to-vmware/image7.png)
9. 安裝完成後，您可以啟動 vContinuum。
    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)

## <a name="step-2-install-a-process-server-in-azure"></a>步驟 2：在 Azure 中安裝處理序伺服器
您需要 tooinstall 在 Azure 中的處理序伺服器，以便在 Azure 中的 hello Vm 可以傳送 hello 資料回復 tooan 在內部部署主要目標伺服器。

1. 在 hello**設定伺服器**頁面在 Azure 中，選取 tooadd 新的處理序伺服器。

   ![](./media/site-recovery-failback-azure-to-vmware/image9.png)
2. 指定處理序伺服器名稱，以及名稱和密碼 tooconnect toohello 虛擬機器系統管理員身分。 選取您想 tooregister hello 處理序伺服器 hello 組態伺服器 toowhich。 這應該是 hello 相同的伺服器，您使用 tooprotect，並將虛擬機器容錯移轉。
3. 指定 hello Azure 網路中的 hello 應該部署處理序伺服器。 它應該是相同的 hello hello 組態伺服器的網路。 指定唯一的 IP 位址選取的子網路並開始部署。

   ![](./media/site-recovery-failback-azure-to-vmware/image10.png)
4. 作業是觸發的 toodeploy hello 處理序伺服器。

   ![](./media/site-recovery-failback-azure-to-vmware/image11.png)
5. Hello 處理序伺服器部署在 Azure 中之後，您可以使用登入 hello server hello 您指定的認證。 註冊 hello 處理序伺服器在 hello 註冊 hello 的相同方式在內部處理序伺服器。

   ![](./media/site-recovery-failback-azure-to-vmware/image12.png)

> [!NOTE]
> hello 容錯回復期間已註冊的伺服器將不會顯示在 Site Recovery 中的 VM 屬性。 它們才會顯示在 [hello**伺服器**hello 組態伺服器 toowhich 進行登錄] 索引標籤。 可能需要大約 10-15 分鐘直到它們 hello 處理序伺服器已出現在 [hello] 索引標籤上。
>
>

## <a name="step-3-install-a-master-target-server-on-premises"></a>步驟 3：安裝主要目標伺服器內部部署
根據您來源虛擬機器的作業系統，您需要 tooinstall Linux 或 Windows 主要目標伺服器在內部。

### <a name="deploy-a-windows-master-target-server"></a>部署 Windows 主要目標伺服器
Windows 主要目標已經隨附於 vContinuum 安裝程式中。 當您安裝 hello vContinuum 時，主要伺服器也部署在 hello 上相同的電腦和已註冊的 toohello 組態伺服器。

1. toobegin 部署中，建立空白電腦在內部想 toorecover hello 從 Azure Vm 的 hello ESX 主機上。
2. 請確定有兩個以上的磁碟附加 toohello VM – hello 作業系統使用的其中一種，而且其他 hello 用於 hello 保留磁碟機。
3. Hello 作業系統安裝。
4. Hello 伺服器上安裝 hello vContinuum。 這也會完成 hello 主要目標伺服器的安裝。

### <a name="deploy-a-linux-master-target-server"></a>部署 Linux 主要目標伺服器
1. toobegin 部署中，建立空白電腦在內部想 toorecover hello 從 Azure Vm 的 hello ESX 主機上。
2. 請確定有兩個以上的磁碟附加 toohello VM – hello 作業系統使用的其中一種，而且其他 hello 用於 hello 保留磁碟機。
3. 安裝 hello Linux 作業系統。 hello Linux 主要目標系統不應該使用 LVM 根或保留儲存空間。 依預設，的 Linux 主要目標伺服器已設定 tooavoid LVM 分割區/磁碟探索。
4. 您可以建立的磁碟分割：

   ![](./media/site-recovery-failback-azure-to-vmware/image13.png)
5. 開始 hello 主要目標安裝之前執行下列後續安裝步驟 hello。

#### <a name="post-os-installation-steps"></a>作業系統的安裝前步驟
tooget hello SCSI 識別碼傳回的每個 SCSI 硬碟，在 Linux 虛擬機器，啟用 hello 參數 「 磁碟。EnableUUID = TRUE"，如下所示：

1. 關閉虛擬機器。
2. 以滑鼠右鍵按一下 hello 左側面板中的 hello VM 項目 >**編輯設定**。
3. 按一下 hello**選項** 索引標籤。選取 進階\> 一般項目  >  組態參數。 hello**組態參數**hello 機器關機時，才可用選項。

    ![](./media/site-recovery-failback-azure-to-vmware/image14.png)
4. 查看含有 **disk.EnableUUID** 的資料列是否已經存在？ 如果它設定得**False**然後將它設定太**True** （不區分大小寫）。 如果存在，而且是設定 tootrue，請按一下**取消**和開機設定之後，測試 hello hello 客體作業系統內的 SCSI 命令。 如果不存在，請按一下 [加入資料列] 。
5. 新增磁碟。在 hello EnableUUID**名稱**資料行。 將其值儲存為 TRUE。 請勿將加入 hello 高於以及雙引號的值。

    ![](./media/site-recovery-failback-azure-to-vmware/image15.png)

#### <a name="download-and-install-hello-additional-packages"></a>下載並安裝 hello 其他封裝
注意： 請確定 hello 系統具有網際網路連線才能下載和安裝 hello 其他封裝。

\# yum install -y xfsprogs perl lsscsi rsync wget kexec-tools

此命令會從 CentOS 6.6 儲存機制下載這 15 個封裝，並加以安裝：

bc-1.06.95-1.el6.x86\_64.rpm

busybox-1.15.1-20.el6.x86\_64.rpm

elfutils-libs-0.158-3.2.el6.x86\_64.rpm

kexec-tools-2.0.0-280.el6.x86\_64.rpm

lsscsi-0.23-2.el6.x86\_64.rpm

lzo-2.03-3.1.el6\_5.1.x86\_64.rpm

perl-5.10.1-136.el6\_6.1.x86\_64.rpm

perl-Module-Pluggable-3.90-136.el6\_6.1.x86\_64.rpm

perl-Pod-Escapes-1.04-136.el6\_6.1.x86\_64.rpm

perl-Pod-Simple-3.13-136.el6\_6.1.x86\_64.rpm

perl-libs-5.10.1-136.el6\_6.1.x86\_64.rpm

perl-version-0.77-136.el6\_6.1.x86\_64.rpm

rsync-3.0.6-12.el6.x86\_64.rpm

snappy-1.1.0-1.el6.x86\_64.rpm

wget-1.12-5.el6\_6.1.x86\_64.rpm

如果 hello 來源電腦會使用 Reiser 或 XFS filesystem hello 根或開機裝置，然後下列套件必須下載並安裝 tooprotection 先前的 Linux 主要目標上。

\# cd /usr/local

\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm>

\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm>

\# rpm -ivh kmod-reiserfs-0.0-1.el6.elrepo.x86\_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86\_64.rpm

\# wget <http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_64.rpm>

\# rpm -ivh xfsprogs-3.1.1-16.el6.x86\_64.rpm

#### <a name="apply-custom-configuration-changes"></a>套用自訂組態變更
套用這些變更之前請先確定您已完成 hello 上一節，則請遵循下列步驟：

1. 將複製 hello RHEL 6 64 整合代理程式二進位 toohello 新建立的作業系統。
2. 執行這個命令 toountar hello 二進位： **tar-zxvf\<檔案名稱\>**
3. 執行這個命令 toogive 權限： \# **chmod 755./ApplyCustomChanges.sh**
4. 執行 hello 指令碼：  **\# ./ApplyCustomChanges.sh**。Hello 伺服器上執行一次 hello 指令碼。 Hello 指令碼執行後，請重新啟動 hello 伺服器。

### <a name="install-hello-linux-server"></a>安裝 hello Linux 伺服器
1. [下載](http://go.microsoft.com/fwlink/?LinkID=529757)hello 安裝檔案。
2. 將複製 hello 檔案 toohello Linux 主要目標虛擬機器使用您選擇的 sftp 用戶端公用程式。 或者，您便可以登入 hello Linux 主要目標虛擬機器上，並使用 wget toodownload hello 安裝套件從提供的連結
3. 登入 hello Linux 主要目標伺服器的虛擬機器使用 ssh 您選擇的用戶端
4. 如果您已經連接 toohello Azure 網路的方法，您可以部署 Linux 主要目標伺服器透過 VPN 連線，然後 hello server 發現虛擬機器中使用的內部 IP 位址**儀表板** 索引標籤和連接埠22 tooconnect toohello Linux 主要目標伺服器使用 Secure Shell。
5. 如果您正在連接 toohello Linux 主要目標伺服器，透過公用網際網路連線使用 hello Linux 主要目標伺服器的公用虛擬 IP 位址 (hello 虛擬機器從**儀表板** 索引標籤) 和 hello 公用端點針對建立 ssh toologin toohello Linux servder。
6. 執行從 hello gzipped Linux 主要目標伺服器安裝程式的 tar 檔案解壓縮封存擷取 hello 檔案： *"tar – xvzf Microsoft ASR\_UA\_8.2.0.0\_RHEL6 64"* hello 目錄中，包含 hello 安裝程式檔案。

    ![](./media/site-recovery-failback-azure-to-vmware/image16.png)
7. 如果您擷取的 hello 安裝程式檔案 tooa 不同的目錄變更 toohello 目錄 toowhich hello hello tar 檔案解壓縮封存內容解壓縮。 從這個目錄路徑執行 “sudo ./install.sh”。

    ![](./media/site-recovery-failback-azure-to-vmware/image17.png)
8. 當提示的 toochoose 主要角色選取**2 （主要目標）**。 Hello 其他互動式安裝選項保留其預設值。
9. 等候安裝 toocontinue 和 hello 主機組態介面 tooappear。 hello hello Linux 主要目標伺服器的主機組態公用程式是命令列公用程式。 不要 hello ssh 用戶端公用程式調整視窗的大小。 使用 hello 箭號鍵 tooselect hello **Global**選項並按下鍵盤上的輸入。

    ![](./media/site-recovery-failback-azure-to-vmware/image18.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image19.png)
10. 在 hello 欄位中**IP**輸入 hello hello 組態伺服器的內部 IP 位址 (在 hello**儀表板**hello 組態伺服器 VM 索引標籤) 按下 ENTER。 在 [連接埠] 中，輸入 **22**，然後按 ENTER 鍵。
11. 保留 [使用 HTTPS] 為 [是]，然後按 ENTER 鍵。
12. 輸入 hello hello 組態伺服器所產生的複雜密碼。 如果您使用 PUTTY 的用戶端從 Windows 電腦 toossh toohello Linux 虛擬機器，您可以使用 Shift + Insert toopaste hello 內容 hello 剪貼簿。 複製 hello 複雜密碼 toohello 本機剪貼簿使用 Ctrl + C，並使用 Shift + Insert toopaste 它。 按 ENTER 鍵。
13. 使用 hello 向右箭號鍵 toonavigate tooquit，然後按 ENTER。 等候安裝 toocomplete。

    ![](./media/site-recovery-failback-azure-to-vmware/image20.png)

如果基於某些原因您無法 tooregister Linux 主要目標伺服器 toohello 組態伺服器您可以再次從 /usr/local/ASR/Vx/bin/hostconfigcli （您必須先 tooset 存取權限 toothis 執行主機組態公用程式目錄執行 chmod 做為進階使用者）。

#### <a name="validate-master-target-registration"></a>驗證主要目標註冊
您可以驗證該 hello 主要目標伺服器已成功註冊 Azure Site Recovery 保存庫中的 toohello 組態伺服器 >**組態伺服器** > **伺服器詳細資料**。

> [!NOTE]
> 如果您收到 hello 虛擬機器的組態錯誤註冊 hello 主要目標伺服器，可能已經刪除從 Azure 或端點設定不正確之後，這是因為雖然 hello 偵測到主要目標設定由 hello Azure dndpoints hello 主要目標是部署在 Azure 中，這不是在內部部署主要目標伺服器內部部署，則為 true。 這並不會影響容錯回復，您可以忽略這些錯誤。
>
>

## <a name="step-4-protect-hello-virtual-machines-toohello-on-premises-site"></a>步驟 4： 保護虛擬機器 toohello 在內部部署站台 hello
您的容錯回復之前，您會需要 tooprotect Vm toohello 在內部部署站台。

### <a name="before-you-begin"></a>開始之前
VM 容錯移轉 tooAzure，它會新增網頁檔案的額外暫存磁碟機。 這通常是您已容錯移轉的 VM 不需要的額外磁碟機，因為它可能已經有分頁檔專用的磁碟機。 在開始反向 hello 虛擬機器的保護之前，您需要請確定此磁碟機已離線，因此它並不會受到保護。 以下列方式來執行此動作：

1. 開啟 電腦管理，然後選取存放裝置管理，因此，它會列出 hello 磁碟線上和附加 toohello 機器。
2. 選取 hello 暫存磁碟附加的 toohello 機器，然後選擇 toobring 離線。

### <a name="protect-hello-vms"></a>保護 hello Vm
1. 在 hello Azure 入口網站，檢查 hello 它們正在容錯移轉的虛擬機器 tooensure hello 狀態。

    ![](./media/site-recovery-failback-azure-to-vmware/image21.png)
2. 啟動機器上的 vContinuum。

    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)
3. 按一下**新的保護**選取 hello 作業系統類型，
4. 在 hello 新視窗中開啟選取的 hello **OS 類型** > **取得詳細資料**想 hello Vm toofail 回。 在**主要伺服器的詳細資料**、 識別及選取 hello 您想 tooprotect 虛擬機器。 Vm 列在進行容錯移轉前的 hello vCenter 主機名稱。
5. 當您選取虛擬機器 tooprotect （它已經有容錯 tooAzure） 快顯視窗會提供兩個項目 hello 虛擬機器。 這是因為 hello 組態伺服器偵測到的 hello 註冊的虛擬機器 tooit 的兩個執行個體。 Hello 在內部部署 VM，讓您可以保護 hello 正確的 VM，您會需要 tooremove hello 項目。 tooidentify hello 正確 Azure VM 的項目這裡，您可以登入 hello Azure VM 和移 tooC:\Program 檔案 (x86) \Microsoft Azure Site Recovery\Application Data\etc。在 hello 檔案 drscout.conf，找出 hello 主機識別碼。 在 [hello vContinuum] 對話方塊保持 hello 項目，您必須找到 hello 主機識別碼 hello VM。 刪除所有其他項目。 tooselect hello 更正 VM，您可以使用參照 tooits IP 位址。 hello IP 位址範圍在內部將 hello 在內部部署 VM。

   ![](./media/site-recovery-failback-azure-to-vmware/image22.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image23.png)
6. Hello vCenter server 上停止 hello 虛擬機器。 您也可以刪除 hello Vm 內部部署。
7. 然後指定您想要 tooprotect hello Vm hello 內部 MT 伺服器 toowhich。 toodo，連接您想要回到 toofail toohello vCenter server toowhich。

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
8. 選取 hello 主要目標伺服器根據 hello 主機 toowhich 想 toorecover hello VM。

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
9. 提供每個 hello 虛擬機器的 hello replication 選項。 toodo 這您需要 tooselect hello 復原端資料存放區 toowhich hello Vm 將會復原。 hello 表格摘要說明您需要為每個 VM 的 tooprovide hello 不同的選項。

    ![](./media/site-recovery-failback-azure-to-vmware/image25.png)

   | **選項** | **選項建議值** |
   | --- | --- |
   |  處理序伺服器 IP 位址 |選取 Azure 中部署的 hello 處理序伺服器 |
   |  保留大小 (以 MB 為單位) | |
   |  保留值 |1 |
   |  天/小時 |星期幾 |
   |  一致性間隔 |1 |
   |  選取目標資料存放區 |hello 資料存放區可用 hello 復原站台上。 hello 資料存放區應該有足夠空間，並且想 toorestore hello 虛擬機器的可用 toohello ESX 主機。 |
10. 設定的 hello hello 虛擬機器的屬性會取得容錯移轉 tooon 內部部署站台之後。 hello 屬性都摘要在下表中的 hello。

    ![](./media/site-recovery-failback-azure-to-vmware/image26.png)

    | **屬性** | **詳細資料** |
    | --- | --- |
    | 網路組態 |偵測到每個網路介面卡，請選取它，然後按一下 **變更**tooconfigure hello 容錯回復 hello 虛擬機器的 IP 位址。 |
    | 硬體組態 |指定 hello CPU 和 hello 記憶體 hello VM。 設定可以套用的 tooall hello 想 tooprotect 的 Vm。 tooidentify hello hello CPU 和記憶體的正確值，您可以參考 toohello IAAS Vm 角色大小，請參閱 hello 的核心數及指派的記憶體。 |
    | 顯示名稱 |容錯回復 tooon 內部部署之後, 您可以重新命名 hello 虛擬機器會出現在 hello vCenter 清查。 hello 預設名稱是 hello 虛擬機器的電腦主機名稱。 tooidentify hello VM 名稱，您可以參考 toohello hello 保護群組中的 VM 清單。 |
    | NAT 組態 |以下將詳細討論 |

    ![](./media/site-recovery-failback-azure-to-vmware/image27.png)

#### <a name="configure-nat-settings"></a>設定 NAT 原則
1. tooenable hello 虛擬機器的保護，兩個通訊通道必須 toobe 建立。 hello 第一個通道是 hello 虛擬機器與 hello 處理序伺服器之間。 此通道會從 hello VM 收集 hello 資料，並將它傳送 toohello 哪些然後傳送 hello 資料 toohello 主要目標伺服器的處理序伺服器。 Hello 處理序伺服器和受保護的 hello 虛擬機器 toobe 是否 hello 位於相同 Azure 虛擬網路，則您不需要 toouse NAT 設定。 否則，請指定 NAT 設定。 在 Azure 中檢視 hello 處理序伺服器 hello 公用 IP 的位址。

    ![](./media/site-recovery-failback-azure-to-vmware/image28.png)
2. hello 第二個通道是 hello 處理序伺服器與 hello 主要目標伺服器之間。 hello 選項 toouse NAT，或者不會取決於您是使用基礎的 VPN 連線或透過 hello 通訊網際網路。 如果您使用 VPN，請不要選取 NAt，只有當您使用網際網路連線時才選取。

    ![](./media/site-recovery-failback-azure-to-vmware/image29.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image30.png)
3. 如果您沒有刪除 hello 在內部部署虛擬機器所指定，則需要 tooensure 容錯回復 toostill 如果 hello 資料存放區會包含 hello 舊 VMDK 的 hello 容錯回復 VM 取得中建立新的位置。 toodo 此選取 hello**進階**設定，並指定替代資料夾 toorestore tooin**資料夾名稱設定**。 將 hello 保留其預設設定其他選項。 適用於 hello 資料夾名稱設定 tooall hello 伺服器。

    ![](./media/site-recovery-failback-azure-to-vmware/image31.png)
4. 執行整備檢查 tooensure hello 的虛擬機器會準備 toobe 受到保護後 tooon 內部。

    ![](./media/site-recovery-failback-azure-to-vmware/image32.png)
5. 等候它 toocomplete。 如果已順利在所有 Vm 上，您可以指定 hello 保護計劃的名稱。 然後按一下 **保護**toobegin。

    ![](./media/site-recovery-failback-azure-to-vmware/image33.png)
6. 您可以在 vContinuum 中監視進度。

    ![](./media/site-recovery-failback-azure-to-vmware/image34.png)
7. Hello 步驟之後**啟用保護計劃**完成，您可以監視 hello Site Recovery 入口網站中的 VM 防護。

    ![](./media/site-recovery-failback-azure-to-vmware/image35.png)
8. 您可以看到 hello 精確狀態 hello VM 上按一下，然後監視其進度。

    ![](./media/site-recovery-failback-azure-to-vmware/image36.png)

## <a name="prepare-hello-failback-plan"></a>準備 hello 容錯回復計劃
您可以準備使用 vContinuum hello 應用程式可以在任何時間失敗後 toohello 在內部部署站台的容錯回復計劃。 這些復原計劃會在站台復原中的非常類似 toohello 復原計劃。

1. 啟動 vContinuum，然後選取 [管理方案]  >  [復原]。 您可以看到的所有 Vm 上已使用的 toofail hello 計劃清單。 您可以使用 hello 相同計劃 toorecover。

   ![](./media/site-recovery-failback-azure-to-vmware/image37.png)
2. 選取 hello 保護計劃和所有您想要在其中 toorecover Vm hello。 當您選取每個 VM，您可以查看更多詳細資料，包括 hello 目標 ESX 伺服器 hello 來源 VM 磁碟。 按一下**下一步**toobegin hello 復原精靈 」，然後選取您想要 toorecover hello Vm。

    ![](./media/site-recovery-failback-azure-to-vmware/image38.png)
3. 您可以復原根據多個選項，但我們建議您改用**最新標籤**並選取**套用之所有 Vm** tooensure hello hello 虛擬機器的最新資料，將會使用。
4. 執行 hello**整備檢查。** 這會檢查 hello 正確的參數是否已設定的 tooenable VM 復原。 按一下**下一步**如果所有的 hello 檢查成功。 如果未檢查 hello 記錄檔，並解決 hello 錯誤。

    ![](./media/site-recovery-failback-azure-to-vmware/image39.png)
5. 在**VM 組態**確定 hello 復原設定已正確設定。 如果您需要您可以變更 hello VM 設定。

   ![](./media/site-recovery-failback-azure-to-vmware/image40.png)
6. 檢閱虛擬機器，將會復原並指定復原順序 hello 清單。 請注意，Vm 會列出使用 hello 電腦主機名稱。 可能很難 toomap hello 電腦主機名稱 toohello 虛擬機器。
   toomap hello 名稱，請移 toohello 虛擬機器**儀表板**在 Azure 與核取 hello VM 主機名稱。

    ![](./media/site-recovery-failback-azure-to-vmware/image41.png)
7. 指定方案名稱，然後選取 [稍後復原] 。 我們建議 toorecover 稍後因為 hello 初始保護可能不完整。
8. 按一下**復原**toosave hello 計劃或觸發程序 hello 復原如果您已選取 toorecover 現在和不更新版本。 如果已儲存 hello 計劃，您可以檢查 hello 復原狀態 toosee。

   ![](./media/site-recovery-failback-azure-to-vmware/image42.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image43.png)

## <a name="recover-virtual-machines"></a>復原虛擬機器
建立 hello 計劃之後，您可以復原 hello 虛擬機器。 之前您，請檢查該 hello 虛擬機器已完成同步處理。 如果複寫狀態會顯示 [確定]，完成 hello 保護，並已符合 hello RPO 臨界值。 您可以確認 hello VM 屬性中的健全狀況。

![](./media/site-recovery-failback-azure-to-vmware/image44.png)

關閉 hello Azure 虛擬機器才能起始 hello 復原。 這可確保沒有任何拆分，而且使用者將只能存取一份 hello 應用程式。

1. 啟動 hello 儲存計劃。 在 vContinuum 選取**監視器**hello 計劃。 這樣就會列出所有已執行的 hello 計劃。

   ![](./media/site-recovery-failback-azure-to-vmware/image45.png)
2. 在選取的 hello 計劃**復原**按一下**啟動**。 您可以監視復原。 開啟 Vm 之後在您可以在此連接在 vCenter toothem。

   ![](./media/site-recovery-failback-azure-to-vmware/image46.png)

## <a name="protect-tooazure-again-after-failback"></a>容錯回復之後，再次保護 tooAzure
容錯回復完成後您可能會想 tooprotect hello 虛擬機器一次。 以下列方式來執行此動作：

1. 請檢查正在 hello 虛擬機器內部部署和應用程式都可以連線。
2. Hello Azure Site Recovery 入口網站中，選取 hello 的虛擬機器，然後予以刪除。 選取 toodisable hello 保護 hello 虛擬機器。 這可確保不會再保護 hello Vm。
3. 在 Azure 中刪除 hello 無法透過 Azure 虛擬機器
4. 刪除上 vSpehere hello 舊虛擬機器。 這些是您先前容錯 tooAzure 的 hello Vm。
5. 在 hello Site Recovery 入口網站中保護 hello 最近容錯移轉的 Vm。 它們受保護之後您可以將它們 tooa 復原計劃。

## <a name="next-steps"></a>後續步驟
* [閱讀有關](site-recovery-vmware-to-azure-classic.md)複寫 VMware 虛擬機器和實體伺服器 tooAzure 使用增強的 hello 部署。
