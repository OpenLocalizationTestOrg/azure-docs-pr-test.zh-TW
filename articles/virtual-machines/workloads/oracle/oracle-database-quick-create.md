---
title: "在 Azure VM 中的 Oracle 資料庫 aaaCreate |Microsoft 文件"
description: "在您的 Azure 環境中快速啟動並執行 Oracle Database 12c 資料庫。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/17/2017
ms.author: rclaus
ms.openlocfilehash: 83205154c3275d5f57b46c8acfb0cb4e5c68a412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-oracle-database-in-an-azure-vm"></a>在 Azure VM 中建立 Oracle 資料庫

本指南詳細說明使用 hello Azure CLI toodeploy Azure 虛擬機器從 hello [Oracle marketplace 資源庫映像](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview)中排序 toocreate Oracle 12c 資料庫。 Hello 伺服器部署之後，您會透過 SSH 連線順序 tooconfigure hello Oracle 資料庫中。 

如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本快速入門會要求執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。

## <a name="create-a-resource-group"></a>建立資源群組

建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。 Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。 

hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置。

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a>Create virtual machine

toocreate 虛擬機器 (VM)，使用 hello [az vm 建立](/cli/azure/vm#create)命令。 

hello 下列範例會建立名為的 VM `myVM`。 如果預設的金鑰位置還沒有 SSH 金鑰的話，此範例也會建立這些金鑰。 toouse 一組特定的金鑰，請使用 hello`--ssh-key-value`選項。  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

建立 hello VM 之後，Azure CLI 顯示資訊的類似 toohello 下列範例。 請注意 hello 值`publicIpAddress`。 您使用此位址 tooaccess hello VM。

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/{snip}/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="connect-toohello-vm"></a>連接 toohello VM

toocreate SSH 工作階段以 hello VM，使用下列命令的 hello。 Hello IP 位址取代成 hello `publicIpAddress` VM 的值。

```bash 
ssh <publicIpAddress>
```

## <a name="create-hello-database"></a>建立 hello 資料庫

hello Marketplace 映像上已安裝 Oracle 軟體 hello。 建立範例資料庫，如下所示。 

1.  切換 toohello *oracle*超級使用者，然後初始化 hello 接聽程式的記錄：

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    hello 輸出是類似 toohello 下列：

    ```bash
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

2.  建立 hello 資料庫：

    ```bash
    dbca -silent \
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

    花幾分鐘的時間 toocreate hello 資料庫。

3. 設定 Oracle 變數

在連接之前，您需要 tooset 兩個環境變數： *ORACLE_HOME*和*ORACLE_SID*。

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
您也可以加入 ORACLE_HOME 和 ORACLE_SID 變數 toohello.bashrc 檔。 這會將儲存未來的登入的 hello 環境的變數。確認 hello 下列陳述式已加入 toohello`~/.bashrc`檔案使用您選擇的編輯器。

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a>Oracle EM Express 連線能力

您可以使用的 GUI 管理工具為 tooexplore hello 資料庫，會設定 Oracle EM Express。 tooconnect tooOracle EM Express，您必須先設定在 Oracle 中的 hello 連接埠。 

1. 連線使用 sqlplus tooyour 資料庫：

    ```bash
    sqlplus / as sysdba
    ```

2. 一旦連接之後，設定 hello 連接埠 5502 EM express

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. 開啟 hello 容器 PDB1 如果不是已開啟，但首先檢查 hello 狀態：

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    hello 輸出是類似 toohello 下列：

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. 如果 hello 的 OPEN_MODE`PDB1`不會讀取寫入，然後執行 hello 下列項目命令 tooopen PDB1:

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

您需要 tootype `quit` tooend hello sqlplus 工作階段和型別`exit`toologout 的 hello oracle 使用者。

## <a name="automate-database-startup-and-shutdown"></a>自動進行資料庫啟動和關機

當您重新啟動 hello VM，hello Oracle 資料庫，依預設不會自動啟動。 向上 hello Oracle 資料庫 toostart tooset 自動，第一次登入為根。 接著，建立並更新一些系統檔案。

1. 以 root 的身分登入
    ```bash
    sudo su -
    ```

2.  使用您最愛的編輯器，編輯 hello 檔案`/etc/oratab`並變更 hello 預設`N`太`Y`:

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  建立名為`/etc/init.d/dbora`和 hello 貼上下列內容：

    ```
    #!/bin/sh
    # chkconfig: 345 99 10
    # Description: Oracle auto start-stop script.
    #
    # Set ORA_HOME toobe equivalent too$ORACLE_HOME.
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle

    case "$1" in
    'start')
        # Start hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        # Remove "&" if you don't want startup as a background process.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" &
        touch /var/lock/subsys/dbora
        ;;

    'stop')
        # Stop hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" &
        rm -f /var/lock/subsys/dbora
        ;;
    esac
    ```

4.  使用 chmod 變更檔案的權限，如下所示：

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  建立用於啟動和關閉的符號連結，如下所示：

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  tootest 您的變更，重新啟動 hello VM:

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a>開始連接埠進行連線

hello 最後一項工作是 tooconfigure 某些外部端點。 向上 tooset hello 保護 hello VM 的 Azure 網路安全性小組，先結束您 hello （應該已經被踢出 SSH 當上一個步驟中重新開機） 的 VM 中的 SSH 工作階段。 

1.  遠端電腦上，使用 tooaccess hello Oracle 資料庫 tooopen hello 端點建立的網路安全性群組規則[az 網路 nsg 規則建立](/cli/azure/network/nsg/rule#create)，如下所示： 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  遠端電腦上，使用 Oracle EM Express tooaccess tooopen hello 端點建立的網路安全性群組規則[az 網路 nsg 規則建立](/cli/azure/network/nsg/rule#create)，如下所示：

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. 如有需要取得您的 VM 使用再次 hello 公用 IP 位址[az 網路公用 ip 顯示](/cli/azure/network/public-ip#show)，如下所示：

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  從您的瀏覽器連接 EM Express。 確定您的瀏覽器與 EM Express 相容 (需要安裝 Flash)： 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

您可以使用登入 hello **SYS**帳戶，並檢查 hello**以 sysdba**核取方塊。 使用 hello 密碼**OraPasswd1**您在安裝期間設定。 

![Hello Oracle OEM Express 登入頁面的螢幕擷取畫面](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a>清除資源

當您完成在 Azure 上瀏覽您的第一個 Oracle 資料庫，而且 hello VM 已不再需要時您可以使用 hello [az 群組刪除](/cli/azure/group#delete)命令 tooremove hello 資源群組、 VM 和所有相關的資源。

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>後續步驟

深入了解 [Azure 上的其他 Oracle 解決方案](oracle-considerations.md)。 

再試一次 hello[安裝和設定 Oracle 自動儲存體管理](configure-oracle-asm.md)教學課程。
