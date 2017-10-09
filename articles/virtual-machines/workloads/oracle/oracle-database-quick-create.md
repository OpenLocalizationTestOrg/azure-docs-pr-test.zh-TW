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
# <a name="create-an-oracle-database-in-an-azure-vm"></a><span data-ttu-id="6aad3-103">在 Azure VM 中建立 Oracle 資料庫</span><span class="sxs-lookup"><span data-stu-id="6aad3-103">Create an Oracle Database in an Azure VM</span></span>

<span data-ttu-id="6aad3-104">本指南詳細說明使用 hello Azure CLI toodeploy Azure 虛擬機器從 hello [Oracle marketplace 資源庫映像](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview)中排序 toocreate Oracle 12c 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6aad3-104">This guide details using hello Azure CLI toodeploy an Azure virtual machine from hello [Oracle marketplace gallery image](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) in order toocreate an Oracle 12c database.</span></span> <span data-ttu-id="6aad3-105">Hello 伺服器部署之後，您會透過 SSH 連線順序 tooconfigure hello Oracle 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="6aad3-105">Once hello server is deployed, you will connect via SSH in order tooconfigure hello Oracle database.</span></span> 

<span data-ttu-id="6aad3-106">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="6aad3-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6aad3-107">如果您選擇 tooinstall，並在本機上使用 hello CLI，本快速入門會要求執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6aad3-107">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="6aad3-108">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="6aad3-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="6aad3-109">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="6aad3-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="6aad3-110">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="6aad3-110">Create a resource group</span></span>

<span data-ttu-id="6aad3-111">建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="6aad3-111">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="6aad3-112">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="6aad3-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="6aad3-113">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置。</span><span class="sxs-lookup"><span data-stu-id="6aad3-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a><span data-ttu-id="6aad3-114">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="6aad3-114">Create virtual machine</span></span>

<span data-ttu-id="6aad3-115">toocreate 虛擬機器 (VM)，使用 hello [az vm 建立](/cli/azure/vm#create)命令。</span><span class="sxs-lookup"><span data-stu-id="6aad3-115">toocreate a virtual machine (VM), use hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="6aad3-116">hello 下列範例會建立名為的 VM `myVM`。</span><span class="sxs-lookup"><span data-stu-id="6aad3-116">hello following example creates a VM named `myVM`.</span></span> <span data-ttu-id="6aad3-117">如果預設的金鑰位置還沒有 SSH 金鑰的話，此範例也會建立這些金鑰。</span><span class="sxs-lookup"><span data-stu-id="6aad3-117">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="6aad3-118">toouse 一組特定的金鑰，請使用 hello`--ssh-key-value`選項。</span><span class="sxs-lookup"><span data-stu-id="6aad3-118">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="6aad3-119">建立 hello VM 之後，Azure CLI 顯示資訊的類似 toohello 下列範例。</span><span class="sxs-lookup"><span data-stu-id="6aad3-119">After you create hello VM, Azure CLI displays information similar toohello following example.</span></span> <span data-ttu-id="6aad3-120">請注意 hello 值`publicIpAddress`。</span><span class="sxs-lookup"><span data-stu-id="6aad3-120">Note hello value for `publicIpAddress`.</span></span> <span data-ttu-id="6aad3-121">您使用此位址 tooaccess hello VM。</span><span class="sxs-lookup"><span data-stu-id="6aad3-121">You use this address tooaccess hello VM.</span></span>

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

## <a name="connect-toohello-vm"></a><span data-ttu-id="6aad3-122">連接 toohello VM</span><span class="sxs-lookup"><span data-stu-id="6aad3-122">Connect toohello VM</span></span>

<span data-ttu-id="6aad3-123">toocreate SSH 工作階段以 hello VM，使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="6aad3-123">toocreate an SSH session with hello VM, use hello following command.</span></span> <span data-ttu-id="6aad3-124">Hello IP 位址取代成 hello `publicIpAddress` VM 的值。</span><span class="sxs-lookup"><span data-stu-id="6aad3-124">Replace hello IP address with hello `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="create-hello-database"></a><span data-ttu-id="6aad3-125">建立 hello 資料庫</span><span class="sxs-lookup"><span data-stu-id="6aad3-125">Create hello database</span></span>

<span data-ttu-id="6aad3-126">hello Marketplace 映像上已安裝 Oracle 軟體 hello。</span><span class="sxs-lookup"><span data-stu-id="6aad3-126">hello Oracle software is already installed on hello Marketplace image.</span></span> <span data-ttu-id="6aad3-127">建立範例資料庫，如下所示。</span><span class="sxs-lookup"><span data-stu-id="6aad3-127">Create a sample database as follows.</span></span> 

1.  <span data-ttu-id="6aad3-128">切換 toohello *oracle*超級使用者，然後初始化 hello 接聽程式的記錄：</span><span class="sxs-lookup"><span data-stu-id="6aad3-128">Switch toohello *oracle* superuser, then initialize hello listener for logging:</span></span>

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    <span data-ttu-id="6aad3-129">hello 輸出是類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="6aad3-129">hello output is similar toohello following:</span></span>

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

2.  <span data-ttu-id="6aad3-130">建立 hello 資料庫：</span><span class="sxs-lookup"><span data-stu-id="6aad3-130">Create hello database:</span></span>

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

    <span data-ttu-id="6aad3-131">花幾分鐘的時間 toocreate hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6aad3-131">It takes a few minutes toocreate hello database.</span></span>

3. <span data-ttu-id="6aad3-132">設定 Oracle 變數</span><span class="sxs-lookup"><span data-stu-id="6aad3-132">Set Oracle variables</span></span>

<span data-ttu-id="6aad3-133">在連接之前，您需要 tooset 兩個環境變數： *ORACLE_HOME*和*ORACLE_SID*。</span><span class="sxs-lookup"><span data-stu-id="6aad3-133">Before you connect, you need tooset two environment variables: *ORACLE_HOME* and *ORACLE_SID*.</span></span>

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
<span data-ttu-id="6aad3-134">您也可以加入 ORACLE_HOME 和 ORACLE_SID 變數 toohello.bashrc 檔。</span><span class="sxs-lookup"><span data-stu-id="6aad3-134">You also can add ORACLE_HOME and ORACLE_SID variables toohello .bashrc file.</span></span> <span data-ttu-id="6aad3-135">這會將儲存未來的登入的 hello 環境的變數。確認 hello 下列陳述式已加入 toohello`~/.bashrc`檔案使用您選擇的編輯器。</span><span class="sxs-lookup"><span data-stu-id="6aad3-135">This would save hello environment variables for future sign-ins. Confirm hello following statements have been added toohello `~/.bashrc` file using editor of your choice.</span></span>

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a><span data-ttu-id="6aad3-136">Oracle EM Express 連線能力</span><span class="sxs-lookup"><span data-stu-id="6aad3-136">Oracle EM Express connectivity</span></span>

<span data-ttu-id="6aad3-137">您可以使用的 GUI 管理工具為 tooexplore hello 資料庫，會設定 Oracle EM Express。</span><span class="sxs-lookup"><span data-stu-id="6aad3-137">For a GUI management tool that you can use tooexplore hello database, set up Oracle EM Express.</span></span> <span data-ttu-id="6aad3-138">tooconnect tooOracle EM Express，您必須先設定在 Oracle 中的 hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="6aad3-138">tooconnect tooOracle EM Express, you must first set up hello port in Oracle.</span></span> 

1. <span data-ttu-id="6aad3-139">連線使用 sqlplus tooyour 資料庫：</span><span class="sxs-lookup"><span data-stu-id="6aad3-139">Connect tooyour database using sqlplus:</span></span>

    ```bash
    sqlplus / as sysdba
    ```

2. <span data-ttu-id="6aad3-140">一旦連接之後，設定 hello 連接埠 5502 EM express</span><span class="sxs-lookup"><span data-stu-id="6aad3-140">Once connected, set hello port 5502 for EM Express</span></span>

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. <span data-ttu-id="6aad3-141">開啟 hello 容器 PDB1 如果不是已開啟，但首先檢查 hello 狀態：</span><span class="sxs-lookup"><span data-stu-id="6aad3-141">Open hello container PDB1 if not already opened, but first check hello status:</span></span>

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    <span data-ttu-id="6aad3-142">hello 輸出是類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="6aad3-142">hello output is similar toohello following:</span></span>

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. <span data-ttu-id="6aad3-143">如果 hello 的 OPEN_MODE`PDB1`不會讀取寫入，然後執行 hello 下列項目命令 tooopen PDB1:</span><span class="sxs-lookup"><span data-stu-id="6aad3-143">If hello OPEN_MODE for `PDB1` is not READ WRITE, then run hello followings commands tooopen PDB1:</span></span>

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

<span data-ttu-id="6aad3-144">您需要 tootype `quit` tooend hello sqlplus 工作階段和型別`exit`toologout 的 hello oracle 使用者。</span><span class="sxs-lookup"><span data-stu-id="6aad3-144">You need tootype `quit` tooend hello sqlplus session and type `exit` toologout of hello oracle user.</span></span>

## <a name="automate-database-startup-and-shutdown"></a><span data-ttu-id="6aad3-145">自動進行資料庫啟動和關機</span><span class="sxs-lookup"><span data-stu-id="6aad3-145">Automate database startup and shutdown</span></span>

<span data-ttu-id="6aad3-146">當您重新啟動 hello VM，hello Oracle 資料庫，依預設不會自動啟動。</span><span class="sxs-lookup"><span data-stu-id="6aad3-146">hello Oracle database by default doesn't automatically start when you restart hello VM.</span></span> <span data-ttu-id="6aad3-147">向上 hello Oracle 資料庫 toostart tooset 自動，第一次登入為根。</span><span class="sxs-lookup"><span data-stu-id="6aad3-147">tooset up hello Oracle database toostart automatically, first sign in as root.</span></span> <span data-ttu-id="6aad3-148">接著，建立並更新一些系統檔案。</span><span class="sxs-lookup"><span data-stu-id="6aad3-148">Then, create and update some system files.</span></span>

1. <span data-ttu-id="6aad3-149">以 root 的身分登入</span><span class="sxs-lookup"><span data-stu-id="6aad3-149">Sign on as root</span></span>
    ```bash
    sudo su -
    ```

2.  <span data-ttu-id="6aad3-150">使用您最愛的編輯器，編輯 hello 檔案`/etc/oratab`並變更 hello 預設`N`太`Y`:</span><span class="sxs-lookup"><span data-stu-id="6aad3-150">Using your favorite editor, edit hello file `/etc/oratab` and change hello default `N` too`Y`:</span></span>

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  <span data-ttu-id="6aad3-151">建立名為`/etc/init.d/dbora`和 hello 貼上下列內容：</span><span class="sxs-lookup"><span data-stu-id="6aad3-151">Create a file named `/etc/init.d/dbora` and paste hello following contents:</span></span>

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

4.  <span data-ttu-id="6aad3-152">使用 chmod 變更檔案的權限，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6aad3-152">Change permissions on files with *chmod* as follows:</span></span>

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  <span data-ttu-id="6aad3-153">建立用於啟動和關閉的符號連結，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6aad3-153">Create symbolic links for startup and shutdown as follows:</span></span>

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  <span data-ttu-id="6aad3-154">tootest 您的變更，重新啟動 hello VM:</span><span class="sxs-lookup"><span data-stu-id="6aad3-154">tootest your changes, restart hello VM:</span></span>

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a><span data-ttu-id="6aad3-155">開始連接埠進行連線</span><span class="sxs-lookup"><span data-stu-id="6aad3-155">Open ports for connectivity</span></span>

<span data-ttu-id="6aad3-156">hello 最後一項工作是 tooconfigure 某些外部端點。</span><span class="sxs-lookup"><span data-stu-id="6aad3-156">hello final task is tooconfigure some external endpoints.</span></span> <span data-ttu-id="6aad3-157">向上 tooset hello 保護 hello VM 的 Azure 網路安全性小組，先結束您 hello （應該已經被踢出 SSH 當上一個步驟中重新開機） 的 VM 中的 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="6aad3-157">tooset up hello Azure Network Security Group that protects hello VM, first exit your SSH session in hello VM (should have been kicked out of SSH when rebooting in previous step).</span></span> 

1.  <span data-ttu-id="6aad3-158">遠端電腦上，使用 tooaccess hello Oracle 資料庫 tooopen hello 端點建立的網路安全性群組規則[az 網路 nsg 規則建立](/cli/azure/network/nsg/rule#create)，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6aad3-158">tooopen hello endpoint that you use tooaccess hello Oracle database remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span> 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  <span data-ttu-id="6aad3-159">遠端電腦上，使用 Oracle EM Express tooaccess tooopen hello 端點建立的網路安全性群組規則[az 網路 nsg 規則建立](/cli/azure/network/nsg/rule#create)，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6aad3-159">tooopen hello endpoint that you use tooaccess Oracle EM Express remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span>

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. <span data-ttu-id="6aad3-160">如有需要取得您的 VM 使用再次 hello 公用 IP 位址[az 網路公用 ip 顯示](/cli/azure/network/public-ip#show)，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6aad3-160">If needed, obtain hello public IP address of your VM again with [az network public-ip show](/cli/azure/network/public-ip#show) as follows:</span></span>

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  <span data-ttu-id="6aad3-161">從您的瀏覽器連接 EM Express。</span><span class="sxs-lookup"><span data-stu-id="6aad3-161">Connect EM Express from your browser.</span></span> <span data-ttu-id="6aad3-162">確定您的瀏覽器與 EM Express 相容 (需要安裝 Flash)：</span><span class="sxs-lookup"><span data-stu-id="6aad3-162">Make sure your browser is compatible with EM Express (Flash install is required):</span></span> 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

<span data-ttu-id="6aad3-163">您可以使用登入 hello **SYS**帳戶，並檢查 hello**以 sysdba**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="6aad3-163">You can log in by using hello **SYS** account, and check hello **as sysdba** checkbox.</span></span> <span data-ttu-id="6aad3-164">使用 hello 密碼**OraPasswd1**您在安裝期間設定。</span><span class="sxs-lookup"><span data-stu-id="6aad3-164">Use hello password **OraPasswd1** that you set during installation.</span></span> 

![Hello Oracle OEM Express 登入頁面的螢幕擷取畫面](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a><span data-ttu-id="6aad3-166">清除資源</span><span class="sxs-lookup"><span data-stu-id="6aad3-166">Clean up resources</span></span>

<span data-ttu-id="6aad3-167">當您完成在 Azure 上瀏覽您的第一個 Oracle 資料庫，而且 hello VM 已不再需要時您可以使用 hello [az 群組刪除](/cli/azure/group#delete)命令 tooremove hello 資源群組、 VM 和所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="6aad3-167">Once you have finished exploring your first Oracle database on Azure and hello VM is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="6aad3-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6aad3-168">Next steps</span></span>

<span data-ttu-id="6aad3-169">深入了解 [Azure 上的其他 Oracle 解決方案](oracle-considerations.md)。</span><span class="sxs-lookup"><span data-stu-id="6aad3-169">Learn about other [Oracle solutions on Azure](oracle-considerations.md).</span></span> 

<span data-ttu-id="6aad3-170">再試一次 hello[安裝和設定 Oracle 自動儲存體管理](configure-oracle-asm.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="6aad3-170">Try hello [Installing and Configuring Oracle Automated Storage Management](configure-oracle-asm.md) tutorial.</span></span>
