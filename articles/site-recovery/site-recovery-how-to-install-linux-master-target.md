---
title: "aaaHow tooinstall 從 Azure tooon 內部部署容錯移轉的 Linux 主要目標伺服器 |Microsoft 文件"
description: "在重新保護 Linux 虛擬機器之前，您必須先有 Linux 主要目標伺服器。 深入了解如何 tooinstall 其中一個。"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: d7c55d115712b9862414979f89efb1f177c5f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-linux-master-target-server"></a>安裝 Linux 主要目標伺服器
您虛擬機器容錯移轉之後，您可以容錯回復 hello 虛擬機器 toohello 在內部部署站台。 toofail 上一步，您需要從 Azure toohello 在內部部署站台 tooreprotect hello 虛擬機器。 此程序，您需要在內部部署主要目標伺服器 tooreceive hello 流量。 

如果受保護的虛擬機器是 Windows 虛擬機器，您需要 Windows 主要目標。 若是 Linux 虛擬機器，您需要 Linux 主要目標。 讀取 hello 下列步驟 toolearn toocreate 並安裝 Linux 主要目標。

> [!IMPORTANT]
> 從 hello 9.10.0 主要目標伺服器的版本開始，hello 最新的主要目標伺服器可以只安裝 Ubuntu 16.04 伺服器上。 CentOS6.6 伺服器上不允許安裝新的主要目標。 不過，您可以繼續 tooupgrade 舊的主要目標伺服器使用 hello 9.10.0 版本。

## <a name="overview"></a>概觀
本文說明如何 tooinstall Linux 主要目標。

將註解或問題張貼結尾 hello 這份文件或在 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="prerequisites"></a>必要條件

* toochoose hello 主機上的 toodeploy hello 的主要目標，判斷 toobe tooan 現有內部部署虛擬機器或 tooa 新的虛擬機器時，是否要將 hello 容錯回復。 
    * 現有的虛擬機器 hello 主要目標的 hello 主機應該具有存取 toohello 資料存放區的 hello 虛擬機器。
    * 如果 hello 在內部部署虛擬機器不存在，hello 相同裝載為 hello 主要目標上建立 hello 容錯回復虛擬機器。 您可以選擇任何 ESXi 主機 tooinstall hello 主要目標。
* hello 主要目標應該是可以與 hello 處理序伺服器和 hello 組態伺服器通訊的網路上。
* hello 版本 hello 主要目標必須等於 tooor 早於 hello hello 處理序伺服器和伺服器 hello 組態版本。 例如，9.4 hello 組態伺服器的 hello 版本時，hello hello 主要的目標版本可以 9.4 或 9.3 不 9.5。
* hello 主要目標只能是 VMware 虛擬機器而不是實體的伺服器。

## <a name="create-hello-master-target-according-toohello-sizing-guidelines"></a>建立 hello 主要的目標，根據 toohello 調整大小的指導方針

建立根據調整大小的指導方針的 hello hello 主要目標：
- **RAM**：6 GB 或更多
- **作業系統磁碟大小**: 100 GB 或更多的 (tooinstall CentOS6.6)
- **用於保留磁碟機的額外磁碟大小**：1 TB
- **CPU 核心**：4 核心或更多

hello 下列支援的 Ubuntu 支援核心。


|核心系列  |支援註冊太 |
|---------|---------|
|4.4      |4.4.0-81-generic         |
|4.8      |4.8.0-56-generic         |
|4.10     |4.10.0-24-generic        |


## <a name="deploy-hello-master-target-server"></a>部署 hello 主要目標伺服器

### <a name="install-ubuntu-16042-minimal"></a>安裝 Ubuntu 16.04.2 極簡版

需要 hello 遵循 hello 步驟 tooinstall hello Ubuntu 16.04.2 64 位元作業系統。

**步驟 1:**移 toohello[下載連結](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64)選擇 hello 最接近鏡像從其下載 Ubuntu 16.04.2 最小 64 位元 ISO。

保留最小 64 位元 ISO Ubuntu 16.04.2 hello DVD 光碟機中並啟動 hello 系統。

**步驟2：**選取 [English]\(英文\) 作為慣用語言，然後按 **Enter**。

![選取語言](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

**步驟 3：**選取 [Install Ubuntu Server]\(安裝 Ubuntu 伺服器\)，然後按 **Enter**。

![選取安裝 Ubuntu Server](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

**步驟 4：**選取 [English]\(英文\) 作為慣用語言，然後按 **Enter**。

![選取 English 作為慣用語言](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

**步驟 5:**選取 hello 適當的選項，從 hello**時區**選項清單，然後選取**Enter**。

![選取 hello 正確設定的時區](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

**步驟 6:**選取**否**(hello 預設選項)，然後選取**Enter**。


![Hello 鍵盤設定](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

**步驟 7:**選取**英文 （美國）**為 hello 國家的 hello 鍵盤的來源，然後選取**Enter**。

![選取 hello 國家/地區為美國](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

**步驟 8:**選取**英文 （美國）**作為 hello 鍵盤配置，然後選取**Enter**。

![做為 hello 鍵盤配置中選取 英文 （美國）](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

**步驟 9:**輸入您的伺服器 hello hello 主機名稱**Hostname**方塊，並選取**繼續**。

![輸入您的伺服器 hello 主機名稱](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

**步驟 10:** toocreate 使用者帳戶，輸入 hello 使用者名稱，然後選取**繼續**。

![建立使用者帳戶](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

**步驟 11:** hello 新的使用者帳戶，請輸入 hello 密碼，然後選取**繼續**。

![輸入 hello 密碼](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

**步驟 12:**確認 hello hello 新使用者的密碼，然後選取 **繼續**。

![確認 hello 密碼](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

**步驟 13:**選取**否**(hello 預設選項)，然後選取**Enter**。

![設定使用者和密碼](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

**步驟 14:**顯示 hello 時區是正確的如果選取**是**(hello 預設選項)，然後選取**Enter**。

tooreconfigure 您的時區，選取**否**。

![設定 hello 時鐘](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

**步驟 15:** hello 分割方式選項，從選取**指引-使用完整磁碟**，然後選取**Enter**。

![選取資料分割方法選項 hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

**步驟 16:**選取 hello 適當的磁碟與 hello**選取磁碟 toopartition**選項，然後選取**Enter**。


![選取 hello 磁碟](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

**步驟 17:**選取**是**toowrite hello 變更 toodisk，然後選取  **Enter**。

![寫入 hello 變更 toodisk](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

**步驟 18:**選取 hello 預設選項，請選取**繼續**，然後選取**Enter**。

![選取 hello 預設選項](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

**步驟 19:**選取 hello 適當的選項，來管理您的系統上的升級，然後選取**Enter**。

![選取 toomanage 如何升級](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> Hello Azure Site Recovery 的主要目標伺服器需要非常特定的 hello Ubuntu 版本，因此您需要 tooensure 升級已停用該 hello 核心 hello 虛擬機器。 如果有啟用，任何規則的升級會造成 hello 主要目標伺服器 toomalfunction。 請確定您選取 hello**沒有自動更新**選項。


**步驟 20：**選取預設選項。 如果您想 openSSH，SSH 連線，請選取 hello **OpenSSH 伺服器**選項，然後再選取**繼續**。

![選取軟體](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

**步驟 21：**選取 [Yes](是\)，然後按 **Enter**。

![安裝 hello 幼蟲開機載入器](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

**步驟 22:**選取 hello hello 開機載入器安裝適當的裝置 (最好是**/開發/sda**)，然後選取**Enter**。

![選取裝置以安裝開機載入器](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

**步驟 23:**選取**繼續**，然後選取**Enter** toofinish hello 安裝。

![完成 hello 安裝](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

Hello 安裝完成之後，登入 toohello VM 與 hello 新的使用者認證。 (請參閱太**步驟 10**如需詳細資訊。)

採取 hello 步驟所述的下列螢幕擷取畫面 tooset hello 根 hello 使用者密碼。 然後以根使用者的身分登入。

![設定 hello 根使用者密碼](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-hello-machine-for-configuration-as-a-master-target-server"></a>做為主要目標伺服器準備 hello 機器組態
接下來，做為主要目標伺服器準備 hello 機器組態。

在 Linux 虛擬機器中，每個 SCSI 磁碟 tooget hello 識別碼啟用 hello**磁碟。EnableUUID = TRUE**參數。

tooenable 這個參數，採用 hello 下列步驟：

1. 關閉虛擬機器。

2. Hello hello hello 左窗格中的虛擬機器的項目上按一下滑鼠右鍵，然後選取**編輯設定**。

3. 選取 hello**選項** 索引標籤。

4. Hello 左窗格中，選取**進階** > **一般**，然後選取 hello**組態參數**hello 右下方的組件的囉 」 畫面上的按鈕。

    ![[選項] 索引標籤](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    hello**組態參數**hello 機器執行時，並非可使用選項。 toomake 作用中，此索引標籤的 hello 虛擬機器關機。

5. 查看含有 [disk.EnableUUID] 的資料列是否已經存在。

    - 如果 hello 值存在而且設定得**False**，也變更 hello 值**True**。 （hello 值是不區分大小寫）。

    - 如果 hello 值存在而且設定得**True**，選取**取消**。

    - 如果 hello 值不存在，請選取**加入資料列**。

    - 在 hello 名稱 欄位加入**磁碟。EnableUUID**，然後將 hello 值設定太**TRUE**。

    ![檢查 disk.EnableUUID 是否已存在](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a>停用核心升級

Azure Site Recovery 的主要目標伺服器需要非常特定的 hello Ubuntu 版本，請確定 hello 核心升級已停用 hello 虛擬機器。

如果已啟用核心升級，任何規則的升級會造成 hello 主要目標伺服器 toomalfunction。

#### <a name="download-and-install-additional-packages"></a>下載並安裝其他套件

> [!NOTE]
> 請確定您有網際網路連線 toodownload，並安裝其他的封裝。 如果您沒有網際網路連線，您需要 toomanually 尋找這些 RPM 套件並安裝它們。

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-hello-installer-for-setup"></a>取得安裝程式中的 hello 安裝程式

如果您的主要目標有網際網路連線，您可以使用下列步驟 toodownload hello installer hello。 或者，您可以複製 hello installer 從 hello 處理序伺服器，然後再安裝它。

#### <a name="download-hello-master-target-installation-packages"></a>下載 hello 主要目標安裝封裝

[下載 hello 最新 Linux 主要目標安裝 bits](https://aka.ms/latestlinuxmobsvc)。

toodownload 它使用 Linux，類型：

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

請確定您下載並解壓縮您的主目錄中的 hello 安裝程式。 如果您將解壓縮太**/usr/本機**，則 hello 安裝會失敗。


#### <a name="access-hello-installer-from-hello-process-server"></a>從 hello 處理序伺服器存取 hello 安裝程式

1. Hello 程序在伺服器上，前往 太**C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**。

2. 將 hello 必要的安裝程式檔案複製從 hello 處理序伺服器，並將它儲存成**latestlinuxmobsvc.tar.gz**主目錄中。


### <a name="apply-custom-configuration-changes"></a>套用自訂組態變更

下列步驟使用 hello tooapply 自訂組態變更：


1. 執行下列命令 toountar hello 二進位 hello。
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Hello 命令 toorun 的螢幕擷取畫面](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. 執行下列命令 toogive 權限的 hello。
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. 執行下列命令 toorun hello 指令碼的 hello。
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> Hello 伺服器上執行一次 hello 指令碼。 關閉 hello 伺服器。 然後重新啟動伺服器 hello 之後新增磁碟，hello 下一節中所述。

### <a name="add-a-retention-disk-toohello-linux-master-target-virtual-machine"></a>加入保留磁碟 toohello Linux 主要目標虛擬機器

使用下列步驟 toocreate 保留磁碟的 hello:

1. 附加新 1 TB 磁碟 toohello Linux 主要目標虛擬機器，然後再啟動 hello 機器。

2. 使用 hello**多重路徑 ll**命令 toolearn hello 多重路徑磁碟的識別碼 hello 保留。

    ```
    multipath -ll
    ```
    ![hello hello 保留磁碟多重路徑識別碼](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. 格式化 hello 磁碟機，並再建立 hello 新磁碟機上的 檔案系統。

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Hello 磁碟機上建立檔案系統](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. 建立 hello 檔案系統之後，掛接 hello 保留磁碟。
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![掛接 hello 保留磁碟](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. 建立 hello **fstab**項目 toomount hello 保留磁碟機每次 hello 系統啟動時啟動。
    ```
    vi /etc/fstab
    ```
    選取**插入**toobegin 編輯 hello 檔案。 建立新的一行，然後再 hello 文字之後。 編輯 hello 磁碟多重路徑識別碼根據 hello 反白顯示 hello 前一個命令從多重路徑的識別碼。

    **/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**

    選取**Esc**，然後輸入**: wq** （寫入及結束） tooclose hello 編輯器 視窗。

### <a name="install-hello-master-target"></a>安裝主要目標的 hello

> [!IMPORTANT]
> hello hello 主要目標伺服器版本必須等於 tooor 早於 hello 版本 hello 處理序伺服器和伺服器 hello 組態。 如果不符合此條件，重新保護會成功，但複寫會失敗。


> [!NOTE]
> 安裝 hello 主要目標伺服器之前，請檢查該 hello **/etc/hosts 主機**hello 虛擬機器上的檔案包含對應 hello 本機主機名稱 toohello IP 位址與所有網路介面卡相關聯的項目。

1. 複製 hello 複雜密碼**C:\ProgramData\Microsoft Azure 站台 Recovery\private\connection.passphrase** hello 組態伺服器上。 然後將它儲存成**passphrase.txt** hello 中執行相同的本機目錄 hello 下列命令：

    ```
    echo <passphrase> >passphrase.txt
    ```
    範例： 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. 請注意 hello 組態伺服器的 IP 位址。 您需要在 hello 下一個步驟。

3. 執行下列命令 tooinstall hello 主要目標伺服器 hello 和伺服器 hello hello 組態伺服器註冊。

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    範例： 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    等候 hello 指令碼完成。 如果主要目標的 hello 註冊成功，hello 主要目標列在 hello **Site Recovery 基礎結構**hello 入口網站頁面。


#### <a name="install-hello-master-target-by-using-interactive-installation"></a>使用互動式安裝來安裝 hello 主要目標

1. 執行下列命令 tooinstall hello 主要目標的 hello。 對於 hello 代理程式角色，請選擇**主要目標**。

    ```
    ./install
    ```

2. 選擇 hello 預設安裝位置，然後選取**Enter** toocontinue。

    ![選擇主要目標的預設安裝位置](./media/site-recovery-how-to-install-linux-master-target/image17.png)

Hello 安裝完成之後，請使用 hello 命令列註冊 hello 組態伺服器。

1. 請注意 hello hello 組態伺服器 IP 位址。 您需要在 hello 下一個步驟。

2. 執行下列命令 tooinstall hello 主要目標伺服器 hello 和伺服器 hello hello 組態伺服器註冊。

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    範例： 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   等候 hello 指令碼完成。 如果 hello 主要目標是已登錄的成功，hello 主要目標列在 hello **Site Recovery 基礎結構**hello 入口網站頁面。


### <a name="upgrade-hello-master-target"></a>升級 hello 主要目標

執行 hello 安裝程式。 它會自動偵測 hello 主要目標上安裝該 hello 代理程式。 選取 tooupgrade **Y**。Hello 安裝完成之後，請檢查 hello 版本 hello 使用 hello 下列命令來安裝的主要目標。

    ```
    cat /usr/local/.vx_version
    ```

您可以看到該 hello**版本**欄位提供的 hello 主要目標的 hello 版本號碼。

### <a name="install-vmware-tools-on-hello-master-target-server"></a>Hello 主要目標伺服器上安裝 VMware 工具

您需要 tooinstall hello 主要目標上的 VMware 工具，讓它可以找出 hello 資料存放區。 如果未安裝 hello 工具，重新保護囉 」 畫面未列在 hello 資料存放區。 安裝之後 hello VMware 工具，您需要 toorestart。

## <a name="next-steps"></a>後續步驟
Hello 安裝和註冊 hello 主要目標有 finsihed 之後，您可以查看 hello 主要目標出現在 hello**主要目標**一節中**Site Recovery 基礎結構**，底下 hello設定伺服器的概觀。

您現在可以繼續[重新保護](site-recovery-how-to-reprotect.md)，接著進行容錯回復。

## <a name="common-issues"></a>常見問題

* 請確定您未在任何管理元件 (例如主要目標) 上啟動 Storage vMotion。 如果 hello 主要目標移動成功的重新保護之後，就無法卸離 hello 虛擬機器磁碟 (Vmdk)。 在此情況下，容錯回復會失敗。

* hello 主要目標不應該有 hello 虛擬機器上的任何快照集。 如果有快照集，容錯回復會失敗。

* 由於 toosome 自訂 NIC 上設定某些客戶，hello 網路介面已停用在啟動期間，與 hello 主要目標代理程式無法初始化。 請確定已正確設定下列屬性的 hello。 請檢查這些屬性在 hello 乙太網路介面卡檔案的 /etc/sysconfig/network-scripts/ifcfg-eth *。
    * BOOTPROTO=dhcp
    * ONBOOT=yes
