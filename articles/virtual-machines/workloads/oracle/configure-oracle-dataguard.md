---
title: "Azure Linux 虛擬機器上的 Oracle 資料防護 aaaImplement |Microsoft 文件"
description: "快速在您的 Azure 環境中啟動並執行 Oracle Data Guard。"
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
ms.date: 05/10/2017
ms.author: rclaus
ms.openlocfilehash: 6bb530098737e3ca7dd8bab3f4306ecbb620f3f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a>在 Azure Linux 虛擬機器上實作 Oracle Data Guard 

Azure CLI 會使用的 toocreate，及管理 Azure 資源，從 hello 命令列或指令碼中。 本文說明如何 toouse Azure CLI toodeploy Oracle Database 12c 資料庫從 hello Azure Marketplace 映像。 這篇文章然後為您示範，逐步解說，如何 tooinstall 和 Azure 的虛擬機器 (VM) 上設定資料保護。

在開始之前，請確定您已安裝 Azure CLI。 如需詳細資訊，請參閱 hello [Azure CLI 安裝指南](https://docs.microsoft.com/cli/azure/install-azure-cli)。

## <a name="prepare-hello-environment"></a>準備 hello 環境
### <a name="assumptions"></a>假設

tooinstall Oracle 資料保護，您需要 toocreate 兩個 Azure Vm 上 hello 相同可用性設定組：

- hello 主要 VM (myVM1) 具有正在執行的 Oracle 執行個體。
- hello 待命 VM (myVM2) 具有只安裝 hello Oracle 軟體。

hello Marketplace 映像，您會使用 toocreate hello Vm 是 Oracle: Oracle-資料庫-Ee:12.1.0.2:latest。

### <a name="sign-in-tooazure"></a>登入 tooAzure 

使用 hello 登入 Azure 訂用帳戶 tooyour [az 登入](/cli/azure/#login)命令，並遵循螢幕上指示 hello。

```azurecli
az login
```

### <a name="create-a-resource-group"></a>建立資源群組

建立資源群組使用 hello [az 群組建立](/cli/azure/group#create)命令。 Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。 

hello 下列範例會建立名為的資源群組`myResourceGroup`在 hello`westus`位置：

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a>建立可用性設定組

建立可用性設定組是選擇性的，但我們仍建議您這麼做。 如需詳細資訊，請參閱 [Azure 可用性設定組指導方針](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines)。

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a>建立虛擬機器

建立 VM 使用 hello [az vm 建立](/cli/azure/vm#create)命令。 

hello 下列範例會建立名為兩個 Vm`myVM1`和`myVM2`。 如果預設的金鑰位置還沒有 SSH 金鑰的話，此範例也會建立這些金鑰。 toouse 一組特定的金鑰，請使用 hello`--ssh-key-value`選項。

建立 myVM1 (主要)：
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

您建立 hello VM 之後，Azure CLI 就會顯示下列範例的資訊類似 toohello。 請注意 hello 值`publicIpAddress`。 您使用此位址 tooaccess hello VM。

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

建立 myVM2 (待命)：
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

請注意 hello 值`publicIpAddress`建立 myVM2 之後。

### <a name="open-hello-tcp-port-for-connectivity"></a>開啟 hello 連線的 TCP 連接埠

此步驟會設定允許遠端存取 toohello Oracle 資料庫中的外部端點。

開啟 myVM1 hello 連接埠：

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

hello 結果看起來類似 toohello 下列回應：

```bash
{
  "access": "Allow",
  "description": null,
  "destinationAddressPrefix": "*",
  "destinationPortRange": "1521",
  "direction": "Inbound",
  "etag": "W/\"bd77dcae-e5fd-4bd6-a632-26045b646414\"",
  "id": "/subscriptions/<subscription-id>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myVmNSG/securityRules/allow-oracle",
  "name": "allow-oracle",
  "priority": 999,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

開啟 myVM2 hello 連接埠：

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a>Toohello 虛擬機器連線

使用 hello 下列命令 toocreate 與 hello 虛擬機器的 SSH 工作階段。 Hello IP 位址取代成 hello`publicIpAddress`虛擬機器的值。

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a>建立 myVM1 hello 資料庫 （主要）

hello Oracle 軟體上已安裝 hello Marketplace 映像，因此 hello 下一個步驟是 tooinstall hello 資料庫。 

切換 toohello Oracle 超級使用者：

```bash
$ sudo su - oracle
```

建立 hello 資料庫：

```bash
$ dbca -silent \
   -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 \
   -sid cdb1 \
   -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs
```
輸出應該看起來類似 toohello 下列回應：

```bash
Copying database files
1% complete
2% complete
8% complete
13% complete
19% complete
27% complete
Creating and starting Oracle instance
29% complete
32% complete
33% complete
34% complete
38% complete
42% complete
43% complete
45% complete
Completing Database Creation
48% complete
51% complete
53% complete
62% complete
70% complete
72% complete
Creating Pluggable Databases
78% complete
100% complete
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

設定 hello ORACLE_SID 和 ORACLE_HOME 變數：

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

（選擇性） 您可以加入 ORACLE_HOME 和 ORACLE_SID toohello /home/oracle/.bashrc 檔案，以便這些設定會儲存為未來的登入：

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a>設定 Data Guard

### <a name="enable-archive-log-mode-on-myvm1-primary"></a>在 myVM1 (主要) 上啟用封存記錄模式

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
```
啟用強制記錄功能，並確定至少有一個記錄檔存在：

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

建立待命重做記錄：

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

回溯 （這樣會復原來得簡單許多） 開啟，並設定待命\_檔案\_管理 tooauto。 在此之後結束 SQL*Plus。

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a>設定 myVM1 (主要) 上的服務

編輯或建立 hello $ORACLE_HOME\network\admin 資料夾中的 hello tnsnames.ora 檔案。

加入下列項目 hello:

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

編輯或建立 hello $ORACLE_HOME\network\admin 資料夾中的 hello listener.ora 檔案。

加入下列項目 hello:

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

啟用 Data Guard Broker：
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
啟動 hello 接聽程式：

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a>設定 myVM2 (待命) 上的服務

SSH toomyVM2:

```bash 
$ ssh azureuser@<publicIpAddress>
```

以 Oracle 的身分登入：

```bash
$ sudo su - oracle
```

編輯或建立 hello $ORACLE_HOME\network\admin 資料夾中的 hello tnsnames.ora 檔案。

加入下列項目 hello:

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

編輯或建立 hello $ORACLE_HOME\network\admin 資料夾中的 hello listener.ora 檔案。

加入下列項目 hello:

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

啟動 hello 接聽程式：

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-hello-database-toomyvm2-standby"></a>還原 hello 資料庫 toomyVM2 （待命）

建立 hello 參數檔案 /tmp/initcdb1_stby.ora 以 hello 下列內容：
```bash
*.db_name='cdb1'
```

建立資料夾：

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

建立密碼檔案：

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
開始在 myVM2 hello 資料庫：

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

使用 hello RMAN 工具還原 hello 資料庫：

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

執行下列命令中 RMAN hello:
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

Hello 命令完成時，應該會看到類似 toohello 下列訊息。 結束 RMAN。
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

（選擇性） 您可以加入 ORACLE_HOME 和 ORACLE_SID toohello /home/oracle/.bashrc 檔案，以便這些設定會儲存為未來的登入：

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

啟用 Data Guard Broker：
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a>在 myVM1 (主要) 上設定 Data Guard Broker

啟動 Data Guard Manager，並使用 SYS 和密碼登入。 (請勿使用 OS 驗證。)執行下列 hello:

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> CREATE CONFIGURATION my_dg_config AS PRIMARY DATABASE IS cdb1 CONNECT IDENTIFIER IS cdb1;
Configuration "my_dg_config" created with primary database "cdb1"
DGMGRL> ADD DATABASE cdb1_stby AS CONNECT IDENTIFIER IS cdb1_stby MAINTAINED AS PHYSICAL;
Database "cdb1_stby" added
DGMGRL> ENABLE CONFIGURATION;
Enabled.
```

檢閱 hello 設定：
```bash
DGMGRL> SHOW CONFIGURATION;

Configuration - my_dg_config

  Protection Mode: MaxPerformance
  Members:
  cdb1      - Primary database
    cdb1_stby - Physical standby database

Fast-Start Failover: DISABLED

Configuration Status:
SUCCESS   (status updated 26 seconds ago)
```

您已經完成 hello Oracle 資料保護設定。 hello 下一節將說明如何 tootest hello 連線並切換。

### <a name="connect-hello-database-from-hello-client-machine"></a>從 hello 用戶端電腦連接 hello 資料庫

更新或建立您的用戶端電腦上的 hello tnsnames.ora 檔案。 這個檔案通常位於 $ORACLE_HOME\network\admin。

取代 hello IP 位址，與您`publicIpAddress`myVM1 和 myVM2 值：

```bash
cdb1=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM1 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1)
    )
  )

cdb1_stby=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM2 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1_stby)
    )
  )
```

啟動 SQL*Plus：

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-hello-data-guard-configuration"></a>測試 hello 資料保護設定

### <a name="switch-over-hello-database-on-myvm1-primary"></a>切換 hello myVM1 （主要） 上的資料庫

從主要 toostandby (cdb1 toocdb1_stby) tooswitch:

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1_stby;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1_stby"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1_stby" is opening...
Operation requires start up of instance "cdb1" on database "cdb1"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1_stby"
DGMGRL>
```

您現在可以連接 toohello 待命資料庫。

啟動 SQL*Plus：

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-hello-database-on-myvm2-standby"></a>切換 myVM2 hello 資料庫 （待命）

進入 tooswitch 執行 myVM2 hello 下列：
```bash
$ dgmgrl sys/OraPasswd1@cdb1_stby
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1" is opening...
Operation requires start up of instance "cdb1" on database "cdb1_stby"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1"
```

同樣地，您現在應該能夠 tooconnect toohello 主要資料庫。

啟動 SQL*Plus：

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

您已完成 hello 安裝和設定 Oracle Linux 上的資料保護。


## <a name="delete-hello-virtual-machine"></a>刪除 hello 虛擬機器

當您不再需要 hello VM 時，您可以使用下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello:

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>後續步驟

[教學課程：建立高可用性的虛擬機器](../../linux/create-cli-complete.md)

[瀏覽 VM 部署 Azure CLI 範例](../../linux/cli-samples.md)
