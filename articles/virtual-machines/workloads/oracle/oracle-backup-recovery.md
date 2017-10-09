---
title: "Azure Linux 虛擬機器上資料庫的總 aaaBack 和 Oracle Database 12c 復原 |Microsoft 文件"
description: "了解如何註冊 tooback 和復原的 Oracle Database 12c 資料庫 Azure 環境中。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 5/17/2017
ms.author: rclaus
ms.openlocfilehash: 68846f4efce5eabdb71cd71772e003838154e93b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a>在 Azure Linux 虛擬機器上備份及復原 Oracle Database 12c 資料庫

您可以使用 Azure CLI toocreate 和管理 Azure 資源，在命令提示字元，或使用指令碼。 在本文中，我們會使用 Azure CLI 指令碼 toodeploy 從 Azure Marketplace 圖庫映像的 Oracle Database 12c 資料庫。

在開始之前，請確定您已安裝 Azure CLI。 如需詳細資訊，請參閱 hello [Azure CLI 安裝指南](https://docs.microsoft.com/cli/azure/install-azure-cli)。

## <a name="prepare-hello-environment"></a>準備 hello 環境

### <a name="step-1-prerequisites"></a>步驟 1：必要條件

*   tooperform hello 備份和復原程序，您必須先建立 Linux VM 時，Oracle Database 12c 已安裝執行個體。 hello Marketplace 映像使用名為 VM toocreate hello *Oracle: Oracle-資料庫-Ee:12.1.0.2:latest*。

    toolearn 如何 toocreate Oracle 資料庫，請參閱 hello [Oracle 建立資料庫快速入門](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create)。


### <a name="step-2-connect-toohello-vm"></a>步驟 2： 連接 toohello VM

*   toocreate 安全殼層 (SSH) 的工作階段以 hello VM，使用下列命令的 hello。 Hello IP 位址和 hello 主機名稱的組合取代 hello `publicIpAddress` VM 的值。

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-hello-database"></a>步驟 3： 準備 hello 資料庫

1.  這個步驟假設您具有在 VM 上執行的 Oracle 執行個體 (cdb1)，稱為 myVM。

    執行 hello *oracle* superuser 根目錄，然後再初始化 hello 接聽程式：

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

    TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Log messages written too/u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

    Connecting too(ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of hello LISTENER
    ------------------------
    Alias                     LISTENER
    Version                   TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Start Date                23-MAR-2017 15:32:08
    Uptime                    0 days 0 hr. 0 min. 0 sec
    Trace Level               off
    Security                  ON: Local OS Authentication
    SNMP                      OFF
    Listener Log File         /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening Endpoints Summary...
    (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))
    hello listener supports no services
    hello command completed successfully
    ```

2.  （選擇性）請確定 hello 資料庫處於封存記錄模式：

    ```bash
    $ sqlplus / as sysdba
    SQL> SELECT log_mode FROM v$database;

    LOG_MODE
    ------------
    NOARCHIVELOG

    SQL> SHUTDOWN IMMEDIATE;
    SQL> STARTUP MOUNT;
    SQL> ALTER DATABASE ARCHIVELOG;
    SQL> ALTER DATABASE OPEN;
    SQL> ALTER SYSTEM SWITCH LOGFILE;
    ```
3.  （選擇性）建立資料表 tootest hello 認可：

    ```bash
    SQL> alter session set "_ORACLE_SCRIPT"=true ;
    Session altered.
    SQL> create user scott identified by tiger;
    User created.
    SQL> grant create session tooscott;
    Grant succeeded.
    SQL> grant create table tooscott;
    Grant succeeded.
    SQL> alter user scott quota 100M on users;
    User altered.
    SQL> connect scott/tiger
    SQL> create table scott_table(col1 number, col2 varchar2(50));
    Table created.
    SQL> insert into scott_Table VALUES(1,'Line 1');
    1 row created.
    SQL> commit;
    Commit complete.
    ```
4.  確認或變更 hello 備份檔案位置和大小：

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. 使用 Oracle 復原管理員 」 (RMAN) tooback hello 資料庫備份：

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a>步驟 4：Linux VM 的應用程式一致備份

應用程式一致備份是 Azure 備份中的新功能。 您可以建立及選取指令碼 tooexecute 之前和之後 hello VM 快照集 （前快照集與後快照集）。

1. 下載 hello JSON 檔案。

    請從 https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig 下載 VMSnapshotScriptPluginConfig.json。 hello 檔案內容看起來類似 toohello 下列：

    ```azurecli
    {
        "pluginName" : "ScriptRunner",
        "preScriptLocation" : "",
        "postScriptLocation" : "",
        "preScriptParams" : ["", ""],
        "postScriptParams" : ["", ""],
        "preScriptNoOfRetries" : 0,
        "postScriptNoOfRetries" : 0,
        "timeoutInSeconds" : 30,
        "continueBackupOnFailure" : true,
        "fsFreezeEnabled" : true
    }
    ```

2. 在 hello VM 上建立 hello /etc/azure 資料夾：

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. 複製 hello JSON 檔案。

    複製 VMSnapshotScriptPluginConfig.json toohello /etc/azure 資料夾。

4. 編輯 hello JSON 檔案。

    編輯 hello VMSnapshotScriptPluginConfig.json 檔案 tooinclude hello`PreScriptLocation`和`PostScriptlocation`參數。 例如：

    ```azurecli
    {
        "pluginName" : "ScriptRunner",
        "preScriptLocation" : "/etc/azure/pre_script.sh",
        "postScriptLocation" : "/etc/azure/post_script.sh",
        "preScriptParams" : ["", ""],
        "postScriptParams" : ["", ""],
        "preScriptNoOfRetries" : 0,
        "postScriptNoOfRetries" : 0,
        "timeoutInSeconds" : 30,
        "continueBackupOnFailure" : true,
        "fsFreezeEnabled" : true
    }
    ```

5. 建立 hello 前快照集與後快照集指令碼檔案。

    以下是「冷備份」(具有關閉和重新啟動的離線備份) 的前快照集和後快照集指令碼範例：

    針對 /etc/azure/pre_script.sh：

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" > /etc/azure/pre_script_$v_date.log
    ```

    針對 /etc/azure/post_script.sh：

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" > /etc/azure/post_script_$v_date.log
    ```

    以下是「熱備份」(線上備份) 的前快照集和後快照集指令碼範例：

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/pre_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    針對 /etc/azure/post_script.sh：

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/post_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    /Etc/azure/pre_script.sql，修改您根據需求 hello 檔案 hello 內容：

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    /Etc/azure/post_script.sql，修改您根據需求 hello 檔案 hello 內容：

    ```bash
    alter tablespace SYSTEM end backup;
    ...
    ...
    alter system archive log start;
    ```

6. 變更檔案權限：

    ```bash
    # chmod 600 /etc/azure/VMSnapshotScriptPluginConfig.json
    # chmod 700 /etc/azure/pre_script.sh
    # chmod 700 /etc/azure/post_script.sh
    ```

7. 測試 hello 指令碼。

    tootest hello 指令碼，首先，登入為根。 然後，確定沒有任何錯誤：

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

如需詳細資訊，請參閱[適用於 Linux VM 的應用程式一致備份](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/)。


### <a name="step-5-use-azure-recovery-services-vaults-tooback-up-hello-vm"></a>步驟 5： 使用 Azure 復原服務保存庫 tooback 向上 hello VM

1.  在 hello Azure 入口網站中搜尋**復原服務保存庫**。

    ![復原服務保存庫頁面](./media/oracle-backup-recovery/recovery_service_01.png)

2.  在 hello**復原服務保存庫**刀鋒視窗中，tooadd 新的保存庫中，按一下**新增**。

    ![復原服務保存庫新增頁面](./media/oracle-backup-recovery/recovery_service_02.png)

3.  toocontinue，按一下  **myVault**。

    ![復原服務保存庫詳細資料頁面](./media/oracle-backup-recovery/recovery_service_03.png)

4.  在 hello **myVault**刀鋒視窗中，按一下 **備份**。

    ![復原服務保存庫備份頁面](./media/oracle-backup-recovery/recovery_service_04.png)

5.  在 hello**備份目標**刀鋒視窗中，使用 hello 預設值**Azure**和**虛擬機器**。 按一下 [確定] 。

    ![復原服務保存庫詳細資料頁面](./media/oracle-backup-recovery/recovery_service_05.png)

6.  在 [備份原則] 中，使用 **DefaultPolicy**，或選取 [建立新原則]。 按一下 [確定] 。

    ![復原服務保存庫備份原則詳細資料頁面](./media/oracle-backup-recovery/recovery_service_06.png)

7.  在 hello**選取虛擬機器**刀鋒視窗中，選取 hello **myVM1**核取方塊，然後**確定**。 按一下 hello**啟用備份** 按鈕。

    ![復原服務保存庫項目 toohello 備份的詳細資料頁面](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > 按一下 之後**啟用備份**，hello 備份程序無法啟動，直到 hello 排定的時間過期為止。 立即備份，完成 tooset hello 下一個步驟。

8.  在 hello **myVault-備份項目**刀鋒視窗底下**備份的項目計數**，選取 hello 備份項目計數。

    ![復原服務保存庫 myVault 詳細資料頁面](./media/oracle-backup-recovery/recovery_service_08.png)

9.  在 [hello**備份項目 （Azure 虛擬機器）**刀鋒視窗中的，右邊 hello hello] 頁面上，按一下 hello 省略符號 (**...**) 按鈕，然後再按一下**備份現在**。

    ![復原服務保存庫立即備份命令](./media/oracle-backup-recovery/recovery_service_09.png)

10. 按一下 hello**備份** 按鈕。 等候 hello 備份程序 toofinish。 然後，跳過[步驟 6： 移除 hello 的資料庫檔案](#step-6-remove-the-database-files)。

    tooview hello 狀態 hello 備份作業中，按一下**作業**。

    ![復原服務保存庫工作頁面](./media/oracle-backup-recovery/recovery_service_10.png)

    hello hello 備份工作狀態會出現在下列映像的 hello:

    ![包含狀態的復原服務保存庫作業頁面](./media/oracle-backup-recovery/recovery_service_11.png)

11. 應用程式一致的備份，解決任何錯誤 hello 記錄檔中。 hello 記錄檔位於 /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0。

### <a name="step-6-remove-hello-database-files"></a>步驟 6： 移除 hello 的資料庫檔案 
在本文中，稍後您將學習如何 tootest hello 復原程序。 您可以測試 hello 復原程序之前，您會有 tooremove hello 資料庫檔案。

1.  移除 hello 資料表空間和備份檔案：

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  （選擇性）關閉 hello Oracle 執行個體：

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-hello-deleted-files-from-hello-recovery-services-vaults"></a>從 復原服務保存庫的 hello 還原 hello 刪除檔案
toorestore hello 刪除的檔案，完成下列步驟的 hello:

1. 在 hello Azure 入口網站中，搜尋 hello *myVault*復原服務保存庫項目。 在 hello**概觀**刀鋒視窗底下**備份項目**，選取 hello 項目數目。

    ![復原服務保存庫 myVault 備份項目](./media/oracle-backup-recovery/recovery_service_12.png)

2. 在下**備份項目計數**，選取 hello 項目數目。

    ![復原服務保存庫 Azure 虛擬機器備份項目計數](./media/oracle-backup-recovery/recovery_service_13.png)

3. 在 hello **myvm1**刀鋒視窗中，按一下 **檔案復原 （預覽）**。

    ![螢幕擷取畫面的 hello 復原服務保存庫的檔案復原 頁面](./media/oracle-backup-recovery/recovery_service_14.png)

4. 在 hello**檔案復原 （預覽）**  窗格中，按一下 **下載指令碼**。 然後，儲存 hello 下載 (.sh) 檔案 tooa 資料夾 hello 用戶端電腦上。

    ![下載指令碼檔案會儲存選項](./media/oracle-backup-recovery/recovery_service_15.png)

5. 將複製 hello.sh 檔案 toohello VM。

    hello 下列範例顯示如何 toouse 安全複製 (scp) 命令 toomove hello 檔案 toohello VM。 您也可以複製 hello 內容 toohello 剪貼簿，然後按一下 貼上 hello 內容中的 hello VM 設定的新檔案。

    > [!IMPORTANT]
    > 在下列範例的 hello，請務必更新 hello IP 位址和資料夾值。 hello 值必須對應 toohello hello 檔案的儲存位置的資料夾。

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. 變更 hello 檔案，使它擁有 hello 根。

    在下列範例的 hello，變更 hello 檔案，讓它擁有 hello 根。 然後，變更權限。

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    hello 下列範例顯示您執行上述指令碼的 hello 之後應該看到的內容。 當系統提示您輸入 toocontinue，輸入**Y**。

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
    hello script requires 'open-iscsi' and 'lshw' toorun.
    Do you want us tooinstall 'open-iscsi' and 'lshw' on this machine?
    Please press 'Y' toocontinue with installation, 'N' tooabort hello operation. : Y
    Installing 'open-iscsi'....
    Installing 'lshw'....

    Connecting toorecovery point using ISCSI service...

    Connection succeeded!

    Please wait while we attach volumes of hello recovery point toothis machine...

    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath

    1)  | /dev/sde  |  /dev/sde1  |  /root/myVM-20170517093913/Volume1

    2)  | /dev/sde  |  /dev/sde2  |  /root/myVM-20170517093913/Volume2

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

7. 確認存取 toohello 掛接磁碟區。

    tooexit，輸入**q**，然後搜尋 hello 掛接磁碟區。 一份 hello 加入磁碟區，在命令提示字元中，輸入的 toocreate **df k**。

    ![hello df-k 命令](./media/oracle-backup-recovery/recovery_service_16.png)

8. 使用下列指令碼 toocopy hello 遺漏的 hello 檔案後 toohello 資料夾：

    ```bash
    # cd /root/myVM-2017XXXXXXX/Volume2/u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # cp *.bkp /u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # cd /u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # chown oracle:oinstall *.bkp
    # cd /root/myVM-2017XXXXXXX/Volume2/u01/app/oracle/oradata/cdb1
    # cp *.dbf /u01/app/oracle/oradata/cdb1
    # cd /u01/app/oracle/oradata/cdb1
    # chown oracle:oinstall *.dbf
    ```
9. 在下列指令碼的 hello，使用 RMAN toorecover hello 資料庫：

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. 取消掛接 hello 磁碟。

    在 Azure 入口網站上 hello hello**檔案復原 （預覽）**刀鋒視窗中，按一下 **取消掛接磁碟**。

    ![取消掛接磁碟命令](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-hello-entire-vm"></a>還原 hello 整個 VM

而不是從 hello 復原服務保存庫還原 hello 刪除檔案，您可以還原 hello 整個 VM。

### <a name="step-1-delete-myvm"></a>步驟 1：刪除 myVM

*   在 hello Azure 入口網站，移 toohello **myVM1**保存庫，然後再選取**刪除**。

    ![保存庫刪除命令](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-hello-vm"></a>步驟 2： 復原 hello VM

1.  跳過**復原服務保存庫**，然後選取**myVault**。

    ![myVault 項目](./media/oracle-backup-recovery/recover_vm_02.png)

2.  在 hello**概觀**刀鋒視窗底下**備份項目**，選取 hello 項目數目。

    ![myVault 備份項目](./media/oracle-backup-recovery/recover_vm_03.png)

3.  在 hello**備份項目 （Azure 虛擬機器）**刀鋒視窗中，選取**myvm1**。

    ![復原 VM 頁面](./media/oracle-backup-recovery/recover_vm_04.png)

4.  在 hello **myvm1**刀鋒視窗中，按一下 hello 省略符號 (**...**) 按鈕，然後再按一下**還原 VM**。

    ![還原 VM 命令](./media/oracle-backup-recovery/recover_vm_05.png)

5.  在 hello**選取還原點**刀鋒視窗中，選取 hello 項目您想 toorestore，，然後按一下**確定**。

    ![選取 hello 還原點](./media/oracle-backup-recovery/recover_vm_06.png)

    如果您已啟用應用程式一致備份，則會顯示藍色垂直線。

6.  在 hello**還原組態**刀鋒視窗中，選取 hello 虛擬機器名稱，選取 hello 資源群組、，然後按一下**確定**。

    ![還原設定值](./media/oracle-backup-recovery/recover_vm_07.png)

7.  toorestore hello VM 中，按一下 hello**還原** 按鈕。

8.  tooview hello 狀態 hello 還原程序中，按一下**作業**，然後按一下 **Backup 工作**。

    ![備份工作狀態命令](./media/oracle-backup-recovery/recover_vm_08.png)

    hello 下圖顯示 hello hello 還原程序的狀態：

    ![Hello 還原程序的狀態](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-hello-public-ip-address"></a>步驟 3： 設定 hello 公用 IP 位址
Hello 還原 VM 時，設定之後 hello 公用 IP 位址。

1.  在 [hello] 搜尋方塊中，輸入**公用 IP 位址**。

    ![公用 IP 位址的清單](./media/oracle-backup-recovery/create_ip_00.png)

2.  在 hello**公用 IP 位址**刀鋒視窗中，按一下 **新增**。 在 hello**建立公用 IP 位址**刀鋒視窗中，針對**名稱**，選取 hello 公用 IP 名稱。 針對 [資源群組]，選取 [使用現有的]。 然後按一下 [建立] 。

    ![建立 IP 位址](./media/oracle-backup-recovery/create_ip_01.png)

3.  tooassociate hello 公用 IP 位址與 hello hello VM 的網路介面搜尋和選取**myVMip**。 然後，按一下 [關聯]。

    ![將 IP 位址產生關聯](./media/oracle-backup-recovery/create_ip_02.png)

4.  在 [資源類型] 中，選取 [網路介面]。 選取 hello hello myVM 執行個體，使用的網路介面，然後按一下**確定**。

    ![選取資源類型和 NIC 值](./media/oracle-backup-recovery/create_ip_03.png)

5.  搜尋並開啟 hello myVM 移植從 hello 入口網站的執行個體。 hello 與 hello VM 相關聯的 IP 位址會出現在 hello myVM**概觀**刀鋒視窗。

    ![IP 位址值](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-toohello-vm"></a>步驟 4： 連接 toohello VM

*   tooconnect toohello VM，請使用下列指令碼的 hello:

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-hello-database-is-accessible"></a>步驟 5： 測試是否 hello 資料庫可存取
*   使用下列指令碼的 hello 的 tootest 協助工具：

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > 如果 hello 資料庫**啟動**命令會產生錯誤，toorecover hello 資料庫，請參閱[步驟 6： 使用 RMAN toorecover hello 資料庫](#step-6-optional-use-rman-to-recover-the-database)。

### <a name="step-6-optional-use-rman-toorecover-hello-database"></a>步驟 6: （選擇性） 使用 RMAN toorecover hello 資料庫
*   使用下列指令碼的 hello toorecover hello 資料庫：

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

hello 備份及修復 Azure Linux VM 上的 hello Oracle Database 12c 資料庫現在已完成。

## <a name="delete-hello-vm"></a>刪除 VM hello

當您不再需要 hello VM 時，您可以使用下列命令 tooremove hello 資源群組、 hello VM 和所有相關的資源的 hello:

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>後續步驟

[教學課程︰建立高可用性 VM](../../linux/create-cli-complete.md)

[瀏覽 VM 部署 Azure CLI 範例](../../linux/cli-samples.md)



