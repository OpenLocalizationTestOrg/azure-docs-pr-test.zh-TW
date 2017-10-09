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
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="f8059-103">在 Azure Linux 虛擬機器上備份及復原 Oracle Database 12c 資料庫</span><span class="sxs-lookup"><span data-stu-id="f8059-103">Back up and recover an Oracle Database 12c database on an Azure Linux virtual machine</span></span>

<span data-ttu-id="f8059-104">您可以使用 Azure CLI toocreate 和管理 Azure 資源，在命令提示字元，或使用指令碼。</span><span class="sxs-lookup"><span data-stu-id="f8059-104">You can use Azure CLI toocreate and manage Azure resources at a command prompt, or use scripts.</span></span> <span data-ttu-id="f8059-105">在本文中，我們會使用 Azure CLI 指令碼 toodeploy 從 Azure Marketplace 圖庫映像的 Oracle Database 12c 資料庫。</span><span class="sxs-lookup"><span data-stu-id="f8059-105">In this article, we use Azure CLI scripts toodeploy an Oracle Database 12c database from an Azure Marketplace gallery image.</span></span>

<span data-ttu-id="f8059-106">在開始之前，請確定您已安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="f8059-106">Before you begin, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="f8059-107">如需詳細資訊，請參閱 hello [Azure CLI 安裝指南](https://docs.microsoft.com/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="f8059-107">For more information, see hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="f8059-108">準備 hello 環境</span><span class="sxs-lookup"><span data-stu-id="f8059-108">Prepare hello environment</span></span>

### <a name="step-1-prerequisites"></a><span data-ttu-id="f8059-109">步驟 1：必要條件</span><span class="sxs-lookup"><span data-stu-id="f8059-109">Step 1: Prerequisites</span></span>

*   <span data-ttu-id="f8059-110">tooperform hello 備份和復原程序，您必須先建立 Linux VM 時，Oracle Database 12c 已安裝執行個體。</span><span class="sxs-lookup"><span data-stu-id="f8059-110">tooperform hello backup and recovery process, you must first create a Linux VM that has an installed instance of Oracle Database 12c.</span></span> <span data-ttu-id="f8059-111">hello Marketplace 映像使用名為 VM toocreate hello *Oracle: Oracle-資料庫-Ee:12.1.0.2:latest*。</span><span class="sxs-lookup"><span data-stu-id="f8059-111">hello Marketplace image you use toocreate hello VM is named *Oracle:Oracle-Database-Ee:12.1.0.2:latest*.</span></span>

    <span data-ttu-id="f8059-112">toolearn 如何 toocreate Oracle 資料庫，請參閱 hello [Oracle 建立資料庫快速入門](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create)。</span><span class="sxs-lookup"><span data-stu-id="f8059-112">toolearn how toocreate an Oracle database, see hello [Oracle create database quickstart](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span></span>


### <a name="step-2-connect-toohello-vm"></a><span data-ttu-id="f8059-113">步驟 2： 連接 toohello VM</span><span class="sxs-lookup"><span data-stu-id="f8059-113">Step 2: Connect toohello VM</span></span>

*   <span data-ttu-id="f8059-114">toocreate 安全殼層 (SSH) 的工作階段以 hello VM，使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="f8059-114">toocreate a Secure Shell (SSH) session with hello VM, use hello following command.</span></span> <span data-ttu-id="f8059-115">Hello IP 位址和 hello 主機名稱的組合取代 hello `publicIpAddress` VM 的值。</span><span class="sxs-lookup"><span data-stu-id="f8059-115">Replace hello IP address and hello host name combination with hello `publicIpAddress` value for your VM.</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-hello-database"></a><span data-ttu-id="f8059-116">步驟 3： 準備 hello 資料庫</span><span class="sxs-lookup"><span data-stu-id="f8059-116">Step 3: Prepare hello database</span></span>

1.  <span data-ttu-id="f8059-117">這個步驟假設您具有在 VM 上執行的 Oracle 執行個體 (cdb1)，稱為 myVM。</span><span class="sxs-lookup"><span data-stu-id="f8059-117">This step assumes that you have an Oracle instance (cdb1) that is running on a VM named *myVM*.</span></span>

    <span data-ttu-id="f8059-118">執行 hello *oracle* superuser 根目錄，然後再初始化 hello 接聽程式：</span><span class="sxs-lookup"><span data-stu-id="f8059-118">Run hello *oracle* superuser root, and then initialize hello listener:</span></span>

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

2.  <span data-ttu-id="f8059-119">（選擇性）請確定 hello 資料庫處於封存記錄模式：</span><span class="sxs-lookup"><span data-stu-id="f8059-119">(Optional) Make sure hello database is in archive log mode:</span></span>

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
3.  <span data-ttu-id="f8059-120">（選擇性）建立資料表 tootest hello 認可：</span><span class="sxs-lookup"><span data-stu-id="f8059-120">(Optional) Create a table tootest hello commit:</span></span>

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
4.  <span data-ttu-id="f8059-121">確認或變更 hello 備份檔案位置和大小：</span><span class="sxs-lookup"><span data-stu-id="f8059-121">Verify or change hello backup file location and size:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. <span data-ttu-id="f8059-122">使用 Oracle 復原管理員 」 (RMAN) tooback hello 資料庫備份：</span><span class="sxs-lookup"><span data-stu-id="f8059-122">Use Oracle Recovery Manager (RMAN) tooback up hello database:</span></span>

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a><span data-ttu-id="f8059-123">步驟 4：Linux VM 的應用程式一致備份</span><span class="sxs-lookup"><span data-stu-id="f8059-123">Step 4: Application-consistent backup for Linux VMs</span></span>

<span data-ttu-id="f8059-124">應用程式一致備份是 Azure 備份中的新功能。</span><span class="sxs-lookup"><span data-stu-id="f8059-124">Application-consistent backups is a new feature in Azure Backup.</span></span> <span data-ttu-id="f8059-125">您可以建立及選取指令碼 tooexecute 之前和之後 hello VM 快照集 （前快照集與後快照集）。</span><span class="sxs-lookup"><span data-stu-id="f8059-125">You can create and select scripts tooexecute before and after hello VM snapshot (pre-snapshot and post-snapshot).</span></span>

1. <span data-ttu-id="f8059-126">下載 hello JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="f8059-126">Download hello JSON file.</span></span>

    <span data-ttu-id="f8059-127">請從 https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig 下載 VMSnapshotScriptPluginConfig.json。</span><span class="sxs-lookup"><span data-stu-id="f8059-127">Download VMSnapshotScriptPluginConfig.json from https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig.</span></span> <span data-ttu-id="f8059-128">hello 檔案內容看起來類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="f8059-128">hello file contents look similar toohello following:</span></span>

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

2. <span data-ttu-id="f8059-129">在 hello VM 上建立 hello /etc/azure 資料夾：</span><span class="sxs-lookup"><span data-stu-id="f8059-129">Create hello /etc/azure folder on hello VM:</span></span>

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. <span data-ttu-id="f8059-130">複製 hello JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="f8059-130">Copy hello JSON file.</span></span>

    <span data-ttu-id="f8059-131">複製 VMSnapshotScriptPluginConfig.json toohello /etc/azure 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f8059-131">Copy VMSnapshotScriptPluginConfig.json toohello /etc/azure folder.</span></span>

4. <span data-ttu-id="f8059-132">編輯 hello JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="f8059-132">Edit hello JSON file.</span></span>

    <span data-ttu-id="f8059-133">編輯 hello VMSnapshotScriptPluginConfig.json 檔案 tooinclude hello`PreScriptLocation`和`PostScriptlocation`參數。</span><span class="sxs-lookup"><span data-stu-id="f8059-133">Edit hello VMSnapshotScriptPluginConfig.json file tooinclude hello `PreScriptLocation` and `PostScriptlocation` parameters.</span></span> <span data-ttu-id="f8059-134">例如：</span><span class="sxs-lookup"><span data-stu-id="f8059-134">For example:</span></span>

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

5. <span data-ttu-id="f8059-135">建立 hello 前快照集與後快照集指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="f8059-135">Create hello pre-snapshot and post-snapshot script files.</span></span>

    <span data-ttu-id="f8059-136">以下是「冷備份」(具有關閉和重新啟動的離線備份) 的前快照集和後快照集指令碼範例：</span><span class="sxs-lookup"><span data-stu-id="f8059-136">Here's an example of pre-snapshot and post-snapshot scripts for a "cold backup" (an offline backup, with shutdown and restart):</span></span>

    <span data-ttu-id="f8059-137">針對 /etc/azure/pre_script.sh：</span><span class="sxs-lookup"><span data-stu-id="f8059-137">For /etc/azure/pre_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="f8059-138">針對 /etc/azure/post_script.sh：</span><span class="sxs-lookup"><span data-stu-id="f8059-138">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" > /etc/azure/post_script_$v_date.log
    ```

    <span data-ttu-id="f8059-139">以下是「熱備份」(線上備份) 的前快照集和後快照集指令碼範例：</span><span class="sxs-lookup"><span data-stu-id="f8059-139">Here's an example of pre-snapshot and post-snapshot scripts for a "hot backup" (an online backup):</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/pre_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="f8059-140">針對 /etc/azure/post_script.sh：</span><span class="sxs-lookup"><span data-stu-id="f8059-140">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/post_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="f8059-141">/Etc/azure/pre_script.sql，修改您根據需求 hello 檔案 hello 內容：</span><span class="sxs-lookup"><span data-stu-id="f8059-141">For /etc/azure/pre_script.sql, modify hello contents of hello file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    <span data-ttu-id="f8059-142">/Etc/azure/post_script.sql，修改您根據需求 hello 檔案 hello 內容：</span><span class="sxs-lookup"><span data-stu-id="f8059-142">For /etc/azure/post_script.sql, modify hello contents of hello file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM end backup;
    ...
    ...
    alter system archive log start;
    ```

6. <span data-ttu-id="f8059-143">變更檔案權限：</span><span class="sxs-lookup"><span data-stu-id="f8059-143">Change file permissions:</span></span>

    ```bash
    # chmod 600 /etc/azure/VMSnapshotScriptPluginConfig.json
    # chmod 700 /etc/azure/pre_script.sh
    # chmod 700 /etc/azure/post_script.sh
    ```

7. <span data-ttu-id="f8059-144">測試 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f8059-144">Test hello scripts.</span></span>

    <span data-ttu-id="f8059-145">tootest hello 指令碼，首先，登入為根。</span><span class="sxs-lookup"><span data-stu-id="f8059-145">tootest hello scripts, first, sign in as root.</span></span> <span data-ttu-id="f8059-146">然後，確定沒有任何錯誤：</span><span class="sxs-lookup"><span data-stu-id="f8059-146">Then, ensure that there are no errors:</span></span>

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

<span data-ttu-id="f8059-147">如需詳細資訊，請參閱[適用於 Linux VM 的應用程式一致備份](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/)。</span><span class="sxs-lookup"><span data-stu-id="f8059-147">For more information, see [Application-consistent backup for Linux VMs](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).</span></span>


### <a name="step-5-use-azure-recovery-services-vaults-tooback-up-hello-vm"></a><span data-ttu-id="f8059-148">步驟 5： 使用 Azure 復原服務保存庫 tooback 向上 hello VM</span><span class="sxs-lookup"><span data-stu-id="f8059-148">Step 5: Use Azure Recovery Services vaults tooback up hello VM</span></span>

1.  <span data-ttu-id="f8059-149">在 hello Azure 入口網站中搜尋**復原服務保存庫**。</span><span class="sxs-lookup"><span data-stu-id="f8059-149">In hello Azure portal, search for **Recovery Services vaults**.</span></span>

    ![復原服務保存庫頁面](./media/oracle-backup-recovery/recovery_service_01.png)

2.  <span data-ttu-id="f8059-151">在 hello**復原服務保存庫**刀鋒視窗中，tooadd 新的保存庫中，按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="f8059-151">On hello **Recovery Services vaults** blade, tooadd a new vault, click **Add**.</span></span>

    ![復原服務保存庫新增頁面](./media/oracle-backup-recovery/recovery_service_02.png)

3.  <span data-ttu-id="f8059-153">toocontinue，按一下  **myVault**。</span><span class="sxs-lookup"><span data-stu-id="f8059-153">toocontinue, click **myVault**.</span></span>

    ![復原服務保存庫詳細資料頁面](./media/oracle-backup-recovery/recovery_service_03.png)

4.  <span data-ttu-id="f8059-155">在 hello **myVault**刀鋒視窗中，按一下 **備份**。</span><span class="sxs-lookup"><span data-stu-id="f8059-155">On hello **myVault** blade, click **Backup**.</span></span>

    ![復原服務保存庫備份頁面](./media/oracle-backup-recovery/recovery_service_04.png)

5.  <span data-ttu-id="f8059-157">在 hello**備份目標**刀鋒視窗中，使用 hello 預設值**Azure**和**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="f8059-157">On hello **Backup Goal** blade, use hello default values of **Azure** and **Virtual machine**.</span></span> <span data-ttu-id="f8059-158">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f8059-158">Click **OK**.</span></span>

    ![復原服務保存庫詳細資料頁面](./media/oracle-backup-recovery/recovery_service_05.png)

6.  <span data-ttu-id="f8059-160">在 [備份原則] 中，使用 **DefaultPolicy**，或選取 [建立新原則]。</span><span class="sxs-lookup"><span data-stu-id="f8059-160">For **Backup policy**, use **DefaultPolicy**, or select **Create New policy**.</span></span> <span data-ttu-id="f8059-161">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f8059-161">Click **OK**.</span></span>

    ![復原服務保存庫備份原則詳細資料頁面](./media/oracle-backup-recovery/recovery_service_06.png)

7.  <span data-ttu-id="f8059-163">在 hello**選取虛擬機器**刀鋒視窗中，選取 hello **myVM1**核取方塊，然後**確定**。</span><span class="sxs-lookup"><span data-stu-id="f8059-163">On hello **Select virtual machines** blade, select hello **myVM1** check box, and then click **OK**.</span></span> <span data-ttu-id="f8059-164">按一下 hello**啟用備份** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f8059-164">Click hello **Enable backup** button.</span></span>

    ![復原服務保存庫項目 toohello 備份的詳細資料頁面](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > <span data-ttu-id="f8059-166">按一下 之後**啟用備份**，hello 備份程序無法啟動，直到 hello 排定的時間過期為止。</span><span class="sxs-lookup"><span data-stu-id="f8059-166">After you click **Enable backup**, hello backup process doesn't start until hello scheduled time expires.</span></span> <span data-ttu-id="f8059-167">立即備份，完成 tooset hello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="f8059-167">tooset up an immediate backup, complete hello next step.</span></span>

8.  <span data-ttu-id="f8059-168">在 hello **myVault-備份項目**刀鋒視窗底下**備份的項目計數**，選取 hello 備份項目計數。</span><span class="sxs-lookup"><span data-stu-id="f8059-168">On hello **myVault - Backup items** blade, under **BACKUP ITEM COUNT**, select hello backup item count.</span></span>

    ![復原服務保存庫 myVault 詳細資料頁面](./media/oracle-backup-recovery/recovery_service_08.png)

9.  <span data-ttu-id="f8059-170">在 [hello**備份項目 （Azure 虛擬機器）**刀鋒視窗中的，右邊 hello hello] 頁面上，按一下 hello 省略符號 (**...**) 按鈕，然後再按一下**備份現在**。</span><span class="sxs-lookup"><span data-stu-id="f8059-170">On hello **Backup Items (Azure Virtual Machine)** blade, on hello right side of hello page, click hello ellipsis (**...**) button, and then click **Backup now**.</span></span>

    ![復原服務保存庫立即備份命令](./media/oracle-backup-recovery/recovery_service_09.png)

10. <span data-ttu-id="f8059-172">按一下 hello**備份** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f8059-172">Click hello **Backup** button.</span></span> <span data-ttu-id="f8059-173">等候 hello 備份程序 toofinish。</span><span class="sxs-lookup"><span data-stu-id="f8059-173">Wait for hello backup process toofinish.</span></span> <span data-ttu-id="f8059-174">然後，跳過[步驟 6： 移除 hello 的資料庫檔案](#step-6-remove-the-database-files)。</span><span class="sxs-lookup"><span data-stu-id="f8059-174">Then, go too[Step 6: Remove hello database files](#step-6-remove-the-database-files).</span></span>

    <span data-ttu-id="f8059-175">tooview hello 狀態 hello 備份作業中，按一下**作業**。</span><span class="sxs-lookup"><span data-stu-id="f8059-175">tooview hello status of hello backup job, click **Jobs**.</span></span>

    ![復原服務保存庫工作頁面](./media/oracle-backup-recovery/recovery_service_10.png)

    <span data-ttu-id="f8059-177">hello hello 備份工作狀態會出現在下列映像的 hello:</span><span class="sxs-lookup"><span data-stu-id="f8059-177">hello status of hello backup job appears in hello following image:</span></span>

    ![包含狀態的復原服務保存庫作業頁面](./media/oracle-backup-recovery/recovery_service_11.png)

11. <span data-ttu-id="f8059-179">應用程式一致的備份，解決任何錯誤 hello 記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="f8059-179">For an application-consistent backup, address any errors in hello log file.</span></span> <span data-ttu-id="f8059-180">hello 記錄檔位於 /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0。</span><span class="sxs-lookup"><span data-stu-id="f8059-180">hello log file is located at /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.</span></span>

### <a name="step-6-remove-hello-database-files"></a><span data-ttu-id="f8059-181">步驟 6： 移除 hello 的資料庫檔案</span><span class="sxs-lookup"><span data-stu-id="f8059-181">Step 6: Remove hello database files</span></span> 
<span data-ttu-id="f8059-182">在本文中，稍後您將學習如何 tootest hello 復原程序。</span><span class="sxs-lookup"><span data-stu-id="f8059-182">Later in this article, you'll learn how tootest hello recovery process.</span></span> <span data-ttu-id="f8059-183">您可以測試 hello 復原程序之前，您會有 tooremove hello 資料庫檔案。</span><span class="sxs-lookup"><span data-stu-id="f8059-183">Before you can test hello recovery process, you have tooremove hello database files.</span></span>

1.  <span data-ttu-id="f8059-184">移除 hello 資料表空間和備份檔案：</span><span class="sxs-lookup"><span data-stu-id="f8059-184">Remove hello tablespace and backup files:</span></span>

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  <span data-ttu-id="f8059-185">（選擇性）關閉 hello Oracle 執行個體：</span><span class="sxs-lookup"><span data-stu-id="f8059-185">(Optional) Shut down hello Oracle instance:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-hello-deleted-files-from-hello-recovery-services-vaults"></a><span data-ttu-id="f8059-186">從 復原服務保存庫的 hello 還原 hello 刪除檔案</span><span class="sxs-lookup"><span data-stu-id="f8059-186">Restore hello deleted files from hello Recovery Services vaults</span></span>
<span data-ttu-id="f8059-187">toorestore hello 刪除的檔案，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="f8059-187">toorestore hello deleted files, complete hello following steps:</span></span>

1. <span data-ttu-id="f8059-188">在 hello Azure 入口網站中，搜尋 hello *myVault*復原服務保存庫項目。</span><span class="sxs-lookup"><span data-stu-id="f8059-188">In hello Azure portal, search for hello *myVault* Recovery Services vaults item.</span></span> <span data-ttu-id="f8059-189">在 hello**概觀**刀鋒視窗底下**備份項目**，選取 hello 項目數目。</span><span class="sxs-lookup"><span data-stu-id="f8059-189">On hello **Overview** blade, under **Backup items**, select hello number of items.</span></span>

    ![復原服務保存庫 myVault 備份項目](./media/oracle-backup-recovery/recovery_service_12.png)

2. <span data-ttu-id="f8059-191">在下**備份項目計數**，選取 hello 項目數目。</span><span class="sxs-lookup"><span data-stu-id="f8059-191">Under **BACKUP ITEM COUNT**, select hello number of items.</span></span>

    ![復原服務保存庫 Azure 虛擬機器備份項目計數](./media/oracle-backup-recovery/recovery_service_13.png)

3. <span data-ttu-id="f8059-193">在 hello **myvm1**刀鋒視窗中，按一下 **檔案復原 （預覽）**。</span><span class="sxs-lookup"><span data-stu-id="f8059-193">On hello **myvm1** blade, click **File Recovery (Preview)**.</span></span>

    ![螢幕擷取畫面的 hello 復原服務保存庫的檔案復原 頁面](./media/oracle-backup-recovery/recovery_service_14.png)

4. <span data-ttu-id="f8059-195">在 hello**檔案復原 （預覽）**  窗格中，按一下 **下載指令碼**。</span><span class="sxs-lookup"><span data-stu-id="f8059-195">On hello **File Recovery (Preview)** pane, click **Download Script**.</span></span> <span data-ttu-id="f8059-196">然後，儲存 hello 下載 (.sh) 檔案 tooa 資料夾 hello 用戶端電腦上。</span><span class="sxs-lookup"><span data-stu-id="f8059-196">Then, save hello download (.sh) file tooa folder on hello client computer.</span></span>

    ![下載指令碼檔案會儲存選項](./media/oracle-backup-recovery/recovery_service_15.png)

5. <span data-ttu-id="f8059-198">將複製 hello.sh 檔案 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="f8059-198">Copy hello .sh file toohello VM.</span></span>

    <span data-ttu-id="f8059-199">hello 下列範例顯示如何 toouse 安全複製 (scp) 命令 toomove hello 檔案 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="f8059-199">hello following example shows how you toouse a secure copy (scp) command toomove hello file toohello VM.</span></span> <span data-ttu-id="f8059-200">您也可以複製 hello 內容 toohello 剪貼簿，然後按一下 貼上 hello 內容中的 hello VM 設定的新檔案。</span><span class="sxs-lookup"><span data-stu-id="f8059-200">You also can copy hello contents toohello clipboard, and then paste hello contents in a new file that is set up on hello VM.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f8059-201">在下列範例的 hello，請務必更新 hello IP 位址和資料夾值。</span><span class="sxs-lookup"><span data-stu-id="f8059-201">In hello following example, ensure that you update hello IP address and folder values.</span></span> <span data-ttu-id="f8059-202">hello 值必須對應 toohello hello 檔案的儲存位置的資料夾。</span><span class="sxs-lookup"><span data-stu-id="f8059-202">hello values must map toohello folder where hello file is saved.</span></span>

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. <span data-ttu-id="f8059-203">變更 hello 檔案，使它擁有 hello 根。</span><span class="sxs-lookup"><span data-stu-id="f8059-203">Change hello file, so that it's owned by hello root.</span></span>

    <span data-ttu-id="f8059-204">在下列範例的 hello，變更 hello 檔案，讓它擁有 hello 根。</span><span class="sxs-lookup"><span data-stu-id="f8059-204">In hello following example, change hello file so that it's owned by hello root.</span></span> <span data-ttu-id="f8059-205">然後，變更權限。</span><span class="sxs-lookup"><span data-stu-id="f8059-205">Then, change permissions.</span></span>

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    <span data-ttu-id="f8059-206">hello 下列範例顯示您執行上述指令碼的 hello 之後應該看到的內容。</span><span class="sxs-lookup"><span data-stu-id="f8059-206">hello following example shows what you should see after you run hello preceding script.</span></span> <span data-ttu-id="f8059-207">當系統提示您輸入 toocontinue，輸入**Y**。</span><span class="sxs-lookup"><span data-stu-id="f8059-207">When you're prompted toocontinue, enter **Y**.</span></span>

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

7. <span data-ttu-id="f8059-208">確認存取 toohello 掛接磁碟區。</span><span class="sxs-lookup"><span data-stu-id="f8059-208">Access toohello mounted volumes is confirmed.</span></span>

    <span data-ttu-id="f8059-209">tooexit，輸入**q**，然後搜尋 hello 掛接磁碟區。</span><span class="sxs-lookup"><span data-stu-id="f8059-209">tooexit, enter **q**, and then search for hello mounted volumes.</span></span> <span data-ttu-id="f8059-210">一份 hello 加入磁碟區，在命令提示字元中，輸入的 toocreate **df k**。</span><span class="sxs-lookup"><span data-stu-id="f8059-210">toocreate a list of hello added volumes, at a command prompt, enter **df -k**.</span></span>

    ![hello df-k 命令](./media/oracle-backup-recovery/recovery_service_16.png)

8. <span data-ttu-id="f8059-212">使用下列指令碼 toocopy hello 遺漏的 hello 檔案後 toohello 資料夾：</span><span class="sxs-lookup"><span data-stu-id="f8059-212">Use hello following script toocopy hello missing files back toohello folders:</span></span>

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
9. <span data-ttu-id="f8059-213">在下列指令碼的 hello，使用 RMAN toorecover hello 資料庫：</span><span class="sxs-lookup"><span data-stu-id="f8059-213">In hello following script, use RMAN toorecover hello database:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. <span data-ttu-id="f8059-214">取消掛接 hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="f8059-214">Unmount hello disk.</span></span>

    <span data-ttu-id="f8059-215">在 Azure 入口網站上 hello hello**檔案復原 （預覽）**刀鋒視窗中，按一下 **取消掛接磁碟**。</span><span class="sxs-lookup"><span data-stu-id="f8059-215">In hello Azure portal, on hello **File Recovery (Preview)** blade, click **Unmount Disks**.</span></span>

    ![取消掛接磁碟命令](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-hello-entire-vm"></a><span data-ttu-id="f8059-217">還原 hello 整個 VM</span><span class="sxs-lookup"><span data-stu-id="f8059-217">Restore hello entire VM</span></span>

<span data-ttu-id="f8059-218">而不是從 hello 復原服務保存庫還原 hello 刪除檔案，您可以還原 hello 整個 VM。</span><span class="sxs-lookup"><span data-stu-id="f8059-218">Instead of restoring hello deleted files from hello Recovery Services vaults, you can restore hello entire VM.</span></span>

### <a name="step-1-delete-myvm"></a><span data-ttu-id="f8059-219">步驟 1：刪除 myVM</span><span class="sxs-lookup"><span data-stu-id="f8059-219">Step 1: Delete myVM</span></span>

*   <span data-ttu-id="f8059-220">在 hello Azure 入口網站，移 toohello **myVM1**保存庫，然後再選取**刪除**。</span><span class="sxs-lookup"><span data-stu-id="f8059-220">In hello Azure portal, go toohello **myVM1** vault, and then select **Delete**.</span></span>

    ![保存庫刪除命令](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-hello-vm"></a><span data-ttu-id="f8059-222">步驟 2： 復原 hello VM</span><span class="sxs-lookup"><span data-stu-id="f8059-222">Step 2: Recover hello VM</span></span>

1.  <span data-ttu-id="f8059-223">跳過**復原服務保存庫**，然後選取**myVault**。</span><span class="sxs-lookup"><span data-stu-id="f8059-223">Go too**Recovery Services vaults**, and then select **myVault**.</span></span>

    ![myVault 項目](./media/oracle-backup-recovery/recover_vm_02.png)

2.  <span data-ttu-id="f8059-225">在 hello**概觀**刀鋒視窗底下**備份項目**，選取 hello 項目數目。</span><span class="sxs-lookup"><span data-stu-id="f8059-225">On hello **Overview** blade, under **Backup items**, select hello number of items.</span></span>

    ![myVault 備份項目](./media/oracle-backup-recovery/recover_vm_03.png)

3.  <span data-ttu-id="f8059-227">在 hello**備份項目 （Azure 虛擬機器）**刀鋒視窗中，選取**myvm1**。</span><span class="sxs-lookup"><span data-stu-id="f8059-227">On hello **Backup Items (Azure Virtual Machine)** blade, select **myvm1**.</span></span>

    ![復原 VM 頁面](./media/oracle-backup-recovery/recover_vm_04.png)

4.  <span data-ttu-id="f8059-229">在 hello **myvm1**刀鋒視窗中，按一下 hello 省略符號 (**...**) 按鈕，然後再按一下**還原 VM**。</span><span class="sxs-lookup"><span data-stu-id="f8059-229">On hello **myvm1** blade, click hello ellipsis (**...**) button,  and then click **Restore VM**.</span></span>

    ![還原 VM 命令](./media/oracle-backup-recovery/recover_vm_05.png)

5.  <span data-ttu-id="f8059-231">在 hello**選取還原點**刀鋒視窗中，選取 hello 項目您想 toorestore，，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="f8059-231">On hello **Select restore point** blade, select hello item that you want toorestore, and then click **OK**.</span></span>

    ![選取 hello 還原點](./media/oracle-backup-recovery/recover_vm_06.png)

    <span data-ttu-id="f8059-233">如果您已啟用應用程式一致備份，則會顯示藍色垂直線。</span><span class="sxs-lookup"><span data-stu-id="f8059-233">If you have enabled application-consistent backup, a vertical blue bar appears.</span></span>

6.  <span data-ttu-id="f8059-234">在 hello**還原組態**刀鋒視窗中，選取 hello 虛擬機器名稱，選取 hello 資源群組、，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="f8059-234">On hello **Restore configuration** blade, select hello virtual machine name, select hello resource group, and then click **OK**.</span></span>

    ![還原設定值](./media/oracle-backup-recovery/recover_vm_07.png)

7.  <span data-ttu-id="f8059-236">toorestore hello VM 中，按一下 hello**還原** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f8059-236">toorestore hello VM, click hello **Restore** button.</span></span>

8.  <span data-ttu-id="f8059-237">tooview hello 狀態 hello 還原程序中，按一下**作業**，然後按一下 **Backup 工作**。</span><span class="sxs-lookup"><span data-stu-id="f8059-237">tooview hello status of hello restore process, click **Jobs**, and then click **Backup Jobs**.</span></span>

    ![備份工作狀態命令](./media/oracle-backup-recovery/recover_vm_08.png)

    <span data-ttu-id="f8059-239">hello 下圖顯示 hello hello 還原程序的狀態：</span><span class="sxs-lookup"><span data-stu-id="f8059-239">hello following figure shows hello status of hello restore process:</span></span>

    ![Hello 還原程序的狀態](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-hello-public-ip-address"></a><span data-ttu-id="f8059-241">步驟 3： 設定 hello 公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="f8059-241">Step 3: Set hello public IP address</span></span>
<span data-ttu-id="f8059-242">Hello 還原 VM 時，設定之後 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f8059-242">After hello VM is restored, set up hello public IP address.</span></span>

1.  <span data-ttu-id="f8059-243">在 [hello] 搜尋方塊中，輸入**公用 IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="f8059-243">In hello search box, enter **public IP address**.</span></span>

    ![公用 IP 位址的清單](./media/oracle-backup-recovery/create_ip_00.png)

2.  <span data-ttu-id="f8059-245">在 hello**公用 IP 位址**刀鋒視窗中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="f8059-245">On hello **Public IP addresses** blade, click **Add**.</span></span> <span data-ttu-id="f8059-246">在 hello**建立公用 IP 位址**刀鋒視窗中，針對**名稱**，選取 hello 公用 IP 名稱。</span><span class="sxs-lookup"><span data-stu-id="f8059-246">On hello **Create public IP address** blade, for **Name**, select hello public IP name.</span></span> <span data-ttu-id="f8059-247">針對 [資源群組]，選取 [使用現有的]。</span><span class="sxs-lookup"><span data-stu-id="f8059-247">For **Resource group**, select **Use existing**.</span></span> <span data-ttu-id="f8059-248">然後按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="f8059-248">Then, click **Create**.</span></span>

    ![建立 IP 位址](./media/oracle-backup-recovery/create_ip_01.png)

3.  <span data-ttu-id="f8059-250">tooassociate hello 公用 IP 位址與 hello hello VM 的網路介面搜尋和選取**myVMip**。</span><span class="sxs-lookup"><span data-stu-id="f8059-250">tooassociate hello public IP address with hello network interface for hello VM, search for and select **myVMip**.</span></span> <span data-ttu-id="f8059-251">然後，按一下 [關聯]。</span><span class="sxs-lookup"><span data-stu-id="f8059-251">Then, click **Associate**.</span></span>

    ![將 IP 位址產生關聯](./media/oracle-backup-recovery/create_ip_02.png)

4.  <span data-ttu-id="f8059-253">在 [資源類型] 中，選取 [網路介面]。</span><span class="sxs-lookup"><span data-stu-id="f8059-253">For **Resource type**, select **Network interface**.</span></span> <span data-ttu-id="f8059-254">選取 hello hello myVM 執行個體，使用的網路介面，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="f8059-254">Select hello network interface that is used by hello myVM instance, and then click **OK**.</span></span>

    ![選取資源類型和 NIC 值](./media/oracle-backup-recovery/create_ip_03.png)

5.  <span data-ttu-id="f8059-256">搜尋並開啟 hello myVM 移植從 hello 入口網站的執行個體。</span><span class="sxs-lookup"><span data-stu-id="f8059-256">Search for and open hello instance of myVM that is ported from hello portal.</span></span> <span data-ttu-id="f8059-257">hello 與 hello VM 相關聯的 IP 位址會出現在 hello myVM**概觀**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f8059-257">hello IP address that is associated with hello VM appears on hello myVM **Overview** blade.</span></span>

    ![IP 位址值](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-toohello-vm"></a><span data-ttu-id="f8059-259">步驟 4： 連接 toohello VM</span><span class="sxs-lookup"><span data-stu-id="f8059-259">Step 4: Connect toohello VM</span></span>

*   <span data-ttu-id="f8059-260">tooconnect toohello VM，請使用下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="f8059-260">tooconnect toohello VM, use hello following script:</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-hello-database-is-accessible"></a><span data-ttu-id="f8059-261">步驟 5： 測試是否 hello 資料庫可存取</span><span class="sxs-lookup"><span data-stu-id="f8059-261">Step 5: Test whether hello database is accessible</span></span>
*   <span data-ttu-id="f8059-262">使用下列指令碼的 hello 的 tootest 協助工具：</span><span class="sxs-lookup"><span data-stu-id="f8059-262">tootest accessibility, use hello following script:</span></span>

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="f8059-263">如果 hello 資料庫**啟動**命令會產生錯誤，toorecover hello 資料庫，請參閱[步驟 6： 使用 RMAN toorecover hello 資料庫](#step-6-optional-use-rman-to-recover-the-database)。</span><span class="sxs-lookup"><span data-stu-id="f8059-263">If hello database **startup** command generates an error, toorecover hello database, see [Step 6: Use RMAN toorecover hello database](#step-6-optional-use-rman-to-recover-the-database).</span></span>

### <a name="step-6-optional-use-rman-toorecover-hello-database"></a><span data-ttu-id="f8059-264">步驟 6: （選擇性） 使用 RMAN toorecover hello 資料庫</span><span class="sxs-lookup"><span data-stu-id="f8059-264">Step 6: (Optional) Use RMAN toorecover hello database</span></span>
*   <span data-ttu-id="f8059-265">使用下列指令碼的 hello toorecover hello 資料庫：</span><span class="sxs-lookup"><span data-stu-id="f8059-265">toorecover hello database, use hello following script:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

<span data-ttu-id="f8059-266">hello 備份及修復 Azure Linux VM 上的 hello Oracle Database 12c 資料庫現在已完成。</span><span class="sxs-lookup"><span data-stu-id="f8059-266">hello backup and recovery of hello Oracle Database 12c database on an Azure Linux VM is now finished.</span></span>

## <a name="delete-hello-vm"></a><span data-ttu-id="f8059-267">刪除 VM hello</span><span class="sxs-lookup"><span data-stu-id="f8059-267">Delete hello VM</span></span>

<span data-ttu-id="f8059-268">當您不再需要 hello VM 時，您可以使用下列命令 tooremove hello 資源群組、 hello VM 和所有相關的資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="f8059-268">When you no longer need hello VM, you can use hello following command tooremove hello resource group, hello VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f8059-269">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f8059-269">Next steps</span></span>

[<span data-ttu-id="f8059-270">教學課程︰建立高可用性 VM</span><span class="sxs-lookup"><span data-stu-id="f8059-270">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="f8059-271">瀏覽 VM 部署 Azure CLI 範例</span><span class="sxs-lookup"><span data-stu-id="f8059-271">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)



