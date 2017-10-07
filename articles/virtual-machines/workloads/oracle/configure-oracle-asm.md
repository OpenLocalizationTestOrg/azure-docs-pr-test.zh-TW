---
title: "Azure Linux 虛擬機器上的設定 Oracle ASM aaaSet |Microsoft 文件"
description: "快速在您的 Azure 環境中啟動並執行 Oracle ASM。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/19/2017
ms.author: rclaus
ms.openlocfilehash: d6a7046638e919876477d46943faabcb1872acac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a>在 Azure Linux 虛擬機器上設定 Oracle ASM  

Azure 虛擬機器提供完全可設定且彈性的計算環境。 本教學課程涵蓋結合 hello 安裝和設定的 Oracle 自動儲存體管理 (ASM) 的基本 Azure 虛擬機器部署。  您會了解如何：

> [!div class="checklist"]
> * 建立和連線 tooan Oracle 資料庫的 VM
> * 安裝和設定 Oracle 自動儲存體管理
> * 安裝和設定 Oracle Grid Infrastructure
> * 初始化 Oracle ASM 安裝
> * 建立受 ASM 管理的 Oracle DB


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="prepare-hello-environment"></a>準備 hello 環境

### <a name="create-a-resource-group"></a>建立資源群組

toocreate 資源群組、 使用 hello [az 群組建立](/cli/azure/group#create)命令。 Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。 在此範例中，資源群組命名為*myResourceGroup*在 hello *eastus*區域。

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a>建立 VM

toocreate 虛擬機器根據 hello Oracle Database 映像和設定它 toouse Oracle ASM，請使用 hello [az vm 建立](/cli/azure/vm#create)命令。 

hello 下列範例會建立名為 myVM Standard_DS2_v2 大小的 50 GB 的四個連接的資料磁碟的 VM。 如果它們尚不存在 hello 預設索引鍵位置中，它也會建立 SSH 金鑰。  toouse 一組特定的金鑰，請使用 hello`--ssh-key-value`選項。  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

建立 hello VM 之後，Azure CLI 顯示資訊的類似 toohello 下列範例。 請注意 hello 值`publicIpAddress`。 您使用此位址 tooaccess hello VM。

   ```azurecli
   {
     "fqdns": "",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
     "location": "eastus",
     "macAddress": "00-0D-3A-36-2F-56",
     "powerState": "VM running",
     "privateIpAddress": "10.0.0.4",
     "publicIpAddress": "13.64.104.241",
     "resourceGroup": "myResourceGroup"
   }
   ```

### <a name="connect-toohello-vm"></a>連接 toohello VM

SSH 工作階段與 toocreate hello VM 並設定其他設定，請使用下列命令的 hello。 Hello IP 位址取代成 hello `publicIpAddress` VM 的值。

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a>安裝 Oracle ASM

tooinstall Oracle ASM，完成下列步驟的 hello。 

如需關於安裝 Oracle ASM 的詳細資訊，請參閱 [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html)。  

1. 您為根順序 toocontinue ASM 安裝中需要 toologin:

   ```bash
   sudo su -
   ```
   
2. 執行這些額外的命令 tooinstall Oracle ASM 元件：

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. 確認您已安裝 Oracle ASM：

   ```bash
   rpm -qa |grep oracleasm
   ```

    hello 這個命令的輸出應該會列出 hello 下列元件：

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. ASM 正確需要順序 toofunction 中特定的使用者與角色。 下列命令的 hello 建立 hello 先決條件的使用者帳戶和群組： 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. 確認已正確建立使用者和群組：

   ```bash
   id grid
   ```

    hello 這個命令的輸出應該會列出 hello 下列使用者和群組：

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. 為使用者建立的資料夾*方格*和 hello 擁有者變更為：

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a>設定 Oracle ASM

此教學課程，hello 預設使用者是*方格*hello 預設群組，且*asmadmin*。 請確定該 hello *oracle*使用者是 hello asmadmin 群組的一部分。 註冊您的 Oracle ASM 安裝，完成下列步驟的 hello tooset:

1. 設定 hello Oracle ASM 程式庫的驅動程式以及在開機設定 hello 磁碟機 toostart 包含定義 hello 預設使用者 （方格） 和預設群組 (asmadmin) （選擇 y） 和 tooscan 在開機磁碟 （選擇 y）。 您需要 tooanswer hello 提示 hello 下列命令：

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   此命令的 hello 輸出應該看起來類似 toohello 遵循、 停止與提示 toobe 回答。

    ```bash
   Configuring hello Oracle ASM library driver.

   This will configure hello on-boot properties of hello Oracle ASM library
   driver. hello following questions will determine whether hello driver is
   loaded on boot and what permissions it will have. hello current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user tooown hello driver interface []: grid
   Default group tooown hello driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. 檢視 hello 磁碟組態：
   ```bash
   cat /proc/partitions
   ```

   hello 這個命令的輸出應該看起來類似下列的可用磁碟清單的 toohello

   ```bash
   8       16   14680064 sdb
   8       17   14678976 sdb1
   8        0   52428800 sda
   8        1     512000 sda1
   8        2   51915776 sda2
   8       48   52428800 sdd
   8       64   52428800 sde
   8       80   52428800 sdf
   8       32   52428800 sdc
   11       0       1152 sr0
   ```

3. 格式化磁片*/開發/sdc*執行 hello 下列命令，以及回答 hello 提示與：
   - n 為新磁碟分割
   - *p* 為主要磁碟分割
   - *1* tooselect hello 第一個資料分割
   - 按下`enter`hello 第一個磁柱的
   - 按下`enter`hello 最後磁柱的
   - 按下*w* toowrite hello 變更 toohello 磁碟分割表格  

   ```bash
   fdisk /dev/sdc
   ```
   
   使用以上所提供的 hello 答案，hello hello fdisk 命令的輸出應該看起來像 hello 下列：

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide toowrite them.
   After that, of course, hello previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   hello device presents a logical sector size that is smaller than
   hello physical sector size. Aligning tooa physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off hello mode (command 'c') and change display units to
           sectors (command 'u').

   Command (m for help): n
   Command action
     e   extended
     p   primary partition (1-4)
   p
   Partition number (1-4): 1
   First cylinder (1-6527, default 1):
   Using default value 1
   Last cylinder, +cylinders or +size{K,M,G} (1-6527, default 6527):
   Using default value 6527

   Command (m for help): w
   hello partition table has been altered!

   Calling ioctl() toore-read partition table.
   Syncing disks.
   ```

4. 重複前面 fdisk 命令的 hello `/dev/sdd`， `/dev/sde`，和`/dev/sdf`。

5. 請檢查 hello 磁碟組態：

   ```bash
   cat /proc/partitions
   ```

   hello hello 命令輸出看起來應該類似下列 hello:

   ```bash
   major minor  #blocks  name

     8       16   14680064 sdb
     8       17   14678976 sdb1
     8       32   52428800 sdc
     8       33   52428096 sdc1
     8       48   52428800 sdd
     8       49   52428096 sdd1
     8       64   52428800 sde
     8       65   52428096 sde1
     8       80   52428800 sdf
     8       81   52428096 sdf1
     8        0   52428800 sda
     8        1     512000 sda1
     8        2   51915776 sda2
     11       0    1048575 sr0
   ```

6. 檢查 hello Oracle ASM 服務狀態，並啟動 hello Oracle ASM 服務：

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   hello hello 命令輸出看起來應該類似下列 hello:
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing hello Oracle ASMLib driver:                     [  OK  ]
   Scanning hello system for Oracle ASMLib disks:               [  OK  ]
   ```

7. 建立 Oracle ASM 磁碟︰

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   hello hello 命令輸出看起來應該類似下列 hello:

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. 列出 Oracle ASM 磁碟︰

   ```bash
   service oracleasm listdisks
   ```   

   hello hello 命令輸出應該會列出下列 Oracle ASM 磁碟 hello 關閉：

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. 變更 hello hello 根、 oracle 和方格使用者的密碼。 **請記下這些新的密碼**因為您稍後在 hello 安裝期間使用它們。

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. 變更 hello 資料夾權限：

   ```bash
   chmod -R 775 /opt 
   chown grid:oinstall /opt 
   chown oracle:oinstall /dev/sdc1 
   chown oracle:oinstall /dev/sdd1 
   chown oracle:oinstall /dev/sde1 
   chown oracle:oinstall /dev/sdf1 
   chmod 600 /dev/sdc1 
   chmod 600 /dev/sdd1 
   chmod 600 /dev/sde1 
   chmod 600 /dev/sdf1
   ```

## <a name="download-and-prepare-oracle-grid-infrastructure"></a>下載並準備 Oracle Grid Infrastructure

toodownload 並準備 hello Oracle 方格基礎結構軟體，完成下列步驟的 hello:

1. 下載 Oracle 方格基礎結構從 hello [Oracle ASM 下載頁面](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html)。 

   下面的 hello 下載**Oracle Database 12c 版本 1 方格基礎結構 (12.1.0.2.0) 的 Linux x86-64**，下載 hello 兩個.zip 檔案。

2. 下載 hello.zip 檔案 tooyour 用戶端電腦之後，您可以使用安全複製通訊協定 (SCP) toocopy hello 檔案 tooyour VM:

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. SSH Oracle VM 在 Azure 中將 hello 順序 toomove hello.zip 檔案放回/選擇資料夾。 然後，變更 hello hello 檔案擁有者：

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. 將 hello 檔解壓縮。 （如果尚未安裝安裝 hello Linux 解壓縮工具）。
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. 變更權限：
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. 更新設定的交換空間。 Oracle 方格元件需要至少 6.8 GB 的交換空間 tooinstall 方格。 Oracle Linux 映像，在 Azure 中的 hello 預設交換檔案大小是只有 2048 MB。 您需要 tooincrease`ResourceDisk.SwapSizeMB`在 hello`/etc/waagent.conf`檔案，並重新啟動 hello WALinuxAgent 服務，hello 更新設定 tootake 效果。 因為它是唯讀的檔案，您會需要 toochange 檔案權限 tooenable 寫入權限。

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   搜尋`ResourceDisk.SwapSizeMB`太變更 hello 值**8192**。 您將需要 toopress `insert` tooenter 插入模式中，型別中的 hello 值**8192** ，然後按`esc`tooreturn toocommand 模式。 toowrite hello 變更和 quit 的 hello 檔案中，輸入`:wq`按`enter`。
   
   > [!NOTE]
   > 我們強烈建議您一定要使用`WALinuxAgent`tooconfigure 交換空間，使它一定會建立 hello 暫時在本機磁碟上 （暫存磁碟） 為了達到最佳效能。 如需詳細資訊，請參閱[tooadd 交換 Linux 的 Azure 虛擬機器中的檔案如何](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines)。

## <a name="prepare-your-local-client-and-vm-toorun-x11"></a>準備您的本機用戶端和 VM toorun x11
設定 Oracle ASM 需要圖形化介面 toocomplete hello 安裝和組態。 我們使用 hello x11 通訊協定 toofacilitate 此安裝。 如果您使用用戶端系統 （Mac 或 Linux） 已經有 X11 功能已啟用，而且已設定-您可以略過此設定並安裝獨佔 tooWindows 機器。 

1. [下載 PuTTY](http://www.putty.org/)和[下載 Xming](https://xming.en.softonic.com/) tooyour Windows 電腦。 您需要 toocomplete hello 安裝兩個 hello 預設值，再繼續這些應用程式。

2. 安裝 PuTTY 之後，開啟命令提示字元，變更為 hello PuTTY 資料夾 (例如，C:\Program Files\PuTTY) 並執行`puttygen.exe`中排序 toogenerate 索引鍵。

3. 在 PuTTY 金鑰產生器中︰
   
   1. 產生金鑰選取 hello `Generate`  按鈕。
   2. 複製 hello 的 hello 按鍵 (Ctrl + C) 的內容。
   3. 選取 hello `Save private key`  按鈕。
   4. 忽略有關保護 hello 金鑰的複雜密碼的 hello 警告，然後選取  `OK`。

   ![PuTTY 金鑰產生器的螢幕擷取畫面](./media/oracle-asm/puttykeygen.png)

4. 在您的 VM 中，執行下列命令︰

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. 建立名為 `authorized_keys` 的檔案。 Hello hello 金鑰內容貼在檔案中，然後將檔案儲存 hello。

   > [!NOTE]
   > hello 金鑰必須包含字串 hello `ssh-rsa`。 此外，hello hello 索引鍵內容必須是單行文字。
   >  

6. 在用戶端系統上，啟動 PuTTY。 在 hello**類別**] 窗格中，跳過**連接** > **SSH** > **Auth**。在 [hello**私密金鑰檔案驗證**方塊中，瀏覽您先前產生的 toohello 索引鍵。

   ![Hello SSH 驗證選項的螢幕擷取畫面](./media/oracle-asm/setprivatekey.png)

7. 在 [hello**類別**] 窗格中，跳過**連接** > **SSH** > **X11**。 選取 hello**啟用 X11 轉寄**核取方塊。

   ![螢幕擷取畫面的 hello SSH X11 轉寄選項](./media/oracle-asm/enablex11.png)

8. 在 [hello**類別**] 窗格中，跳過**工作階段**。 輸入您的 Oracle ASM VM`<publicIPaddress>`在 hello 主機名稱 對話方塊中，填入新`Saved Session`命名，然後按一下上`Save`。  儲存之後，按一下`open`tooconnect tooyour Oracle ASM 虛擬機器。  hello 您連接您的第一次警告 hello 遠端系統不會快取中登錄。 按一下`yes`tooadd 它並繼續。

   ![Hello PuTTY 工作階段選項的螢幕擷取畫面](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a>安裝 Oracle Grid Infrastructure

tooinstall Oracle 方格基礎結構，完成下列步驟的 hello:

1. 以 **grid** 的身分登入。 （您應該能夠 toosign 中的，而不會提示輸入密碼）。 

   > [!NOTE]
   > 如果您執行 Windows，請確定您已經啟動 Xming hello 安裝開始之前。

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   Oracle Grid Infrastructure 12c Release 1 安裝程式會隨即開啟  （它可能需要幾分鐘，讓 hello installer toostart）。

2. 在 hello**選取安裝選項**頁面上，選取**安裝和設定 Oracle 方格基礎結構適用於獨立伺服器**。

   ![Hello 安裝程式的 [選取安裝選項] 頁面的螢幕擷取畫面](./media/oracle-asm/install01.png)

3. 在 hello**選取產品語言**頁面上，確定**英文**或選取您想要的 hello 語言。  按一下 `next`。

4. 在 hello**建立 ASM 磁碟群組**頁面：
   - 輸入 hello 磁碟群組的名稱。
   - 在 [備援] 底下選取 [外部]。
   - 在 [配置單位大小] 底下選取 [4]。
   - 在 [新增磁碟] 底下選取 [ORCLASMSP]。
   - 按一下 `next`。

5. 在 hello**指定 ASM 密碼**頁面上，選取 hello**使用這些帳戶的相同密碼**選項，然後輸入密碼。

   ![安裝程式 hello 指定 ASM 密碼 頁面的螢幕擷取畫面](./media/oracle-asm/install04.png)

6. 在 [hello**指定管理選項**] 頁面上，您擁有 hello 選項 tooconfigure EM 雲端控制項。 我們正略過此選項-按一下`next`toocontinue。 

7. 在 hello**特殊權限的作業系統群組**頁面上，使用 hello 預設設定。 按一下`next`toocontinue。

8. 在 hello**指定安裝位置**頁面上，使用 hello 預設設定。 按一下`next`toocontinue。

9. 在 hello**建立清查**頁面上，變更 hello 清查目錄太`/u01/app/grid/oraInventory`。 按一下`next`toocontinue。

   ![Hello 安裝程式建立詳細目錄 頁面的螢幕擷取畫面](./media/oracle-asm/install08.png)

10. 在 hello**根指令碼執行組態**頁面上，選取 hello**自動執行組態指令碼**核取方塊。 然後，選取 hello**使用 「 根 」 的使用者認證**選項，然後輸入 hello 根使用者的密碼。

    ![Hello 安裝程式的根指令碼執行組態 頁面的螢幕擷取畫面](./media/oracle-asm/install09.png)

11. 在 [hello**執行必要條件檢查**] 頁面上，hello 目前的安裝程式將會失敗並出現錯誤。 這是預期中的行為。 選取 `Fix & Check Again`。

12. 在 hello**修復指令碼**對話方塊中，按一下  `OK`。

13. 在 hello**摘要**頁面上，檢閱您選取的設定，然後按一下`Install`。

    ![Hello 安裝程式的 [摘要] 頁面的螢幕擷取畫面](./media/oracle-asm/install12.png)

14. 警告會出現對話方塊通知您設定指令碼需要特殊權限的使用者身分執行 toobe。 按一下`Yes`toocontinue。

15. 在 hello**完成**頁面上，按一下`Close`toofinish hello 安裝。

## <a name="set-up-your-oracle-asm-installation"></a>設定 Oracle ASM 安裝

註冊您的 Oracle ASM 安裝，完成下列步驟的 hello tooset:

1. 請確定您仍從 X11 工作階段以 **grid** 的身分登入。 您可能需要 toohit `enter` toorevive hello 終端機。 然後啟動 Oracle 自動儲存體管理 Configuration Assistant hello:

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   Oracle ASM Configuration Assistant 隨即開啟。

2. 在 hello**設定 ASM： 磁碟群組**對話方塊方塊中，按一下 hello`Create`按鈕，然後再按一下`Show Advanced Options`。

3. 在 hello**建立磁碟群組**對話方塊：

   - 輸入 hello 磁碟群組名稱**資料**。
   - 在 [選取成員磁碟] 底下選取 [ORCL_DATA] 和 [ORCL_DATA1]。
   - 在 [配置單位大小] 底下選取 [4]。
   - 按一下`ok`toocreate hello 磁碟群組。
   - 按一下`ok`tooclose hello 確認視窗。

   ![Hello 建立磁碟群組 對話方塊的螢幕擷取畫面](./media/oracle-asm/asm02.png)

4. 在 hello**設定 ASM： 磁碟群組**對話方塊方塊中，按一下 hello`Create`按鈕，然後再按一下`Show Advanced Options`。

5. 在 hello**建立磁碟群組**對話方塊：

   - 輸入 hello 磁碟群組名稱**FRA**。
   - 在 [備援] 底下選取 [外部 (無)]。
   - 在 [選取成員磁碟] 底下選取 [ORCL_FRA]。
   - 在 [配置單位大小] 底下選取 [4]。
   - 按一下`ok`toocreate hello 磁碟群組。
   - 按一下`ok`tooclose hello 確認視窗。

   ![Hello 建立磁碟群組 對話方塊的螢幕擷取畫面](./media/oracle-asm/asm04.png)

6. 選取**結束**tooclose ASM Configuration Assistant。

   ![螢幕擷取畫面的 hello 設定 ASM： 磁碟群組 對話方塊的 結束 按鈕](./media/oracle-asm/asm05.png)

## <a name="create-hello-database"></a>建立 hello 資料庫

hello Oracle 資料庫軟體已經安裝 hello Azure Marketplace 映像上。 toocreate 資料庫中，完成下列步驟的 hello:

1. 切換使用者 toohello Oracle 超級使用者，然後初始化 記錄的 hello 接聽程式：

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   Database Configuration Assistant 隨即開啟。

2. 在 hello**資料庫作業**頁面上，按一下`Create Database`。

3. 在 hello**建立模式**頁面：

   - 輸入 hello 資料庫的名稱。
   - 在 [儲存體類型] 中，請確定已選取 [自動儲存體管理 (ASM)]。
   - 如**資料庫檔案位置**，使用預設的 hello ASM 建議位置。
   - 如**快速復原區域**，使用預設的 hello ASM 建議位置。
   - 輸入 [管理密碼] 和 [確認密碼]。
   - 確定已選取 `create as container database`。
   - 輸入 `pluggable database name` 值。

4. 在 hello**摘要**頁面上，檢閱您選取的設定，然後按一下`Finish`toocreate hello 資料庫。

   ![Hello 摘要 頁面的螢幕擷取畫面](./media/oracle-asm/createdb03.png)

5. 已建立 hello 資料庫。 在 hello**完成**頁面上，您可以 hello 選項 toounlock 其他帳戶 toouse 這個資料庫，然後變更 hello 密碼。 如果想 toodo 操作，請選取**密碼管理**-否則按一下`close`。

## <a name="delete-hello-vm"></a>刪除 VM hello

您已成功從 hello Azure Marketplace 的 hello Oracle DB 映像上設定 Oracle 自動儲存體管理。  當您不再需要此 VM 時，您可以使用下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello:

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>後續步驟

[教學課程：設定 Oracle DataGuard](configure-oracle-dataguard.md)

[教學課程：設定 Oracle GoldenGate](Configure-oracle-golden-gate.md)

請檢閱[建置 Oracle DB](oracle-design.md)
