---
title: "在 Azure VM 中建立 Oracle 資料庫 | Microsoft Docs"
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
ms.openlocfilehash: 8683b016c4db2c66fb1dd994405b70c3d137a7fc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-oracle-database-in-an-azure-vm"></a><span data-ttu-id="49ac9-103">在 Azure VM 中建立 Oracle 資料庫</span><span class="sxs-lookup"><span data-stu-id="49ac9-103">Create an Oracle Database in an Azure VM</span></span>

<span data-ttu-id="49ac9-104">本指南詳述如何使用 Azure CLI 從 [Oracle Marketplace 資源庫映像](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview)部署 Azure 虛擬機器，以便建立 Oracle 12c 資料庫。</span><span class="sxs-lookup"><span data-stu-id="49ac9-104">This guide details using the Azure CLI to deploy an Azure virtual machine from the [Oracle marketplace gallery image](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) in order to create an Oracle 12c database.</span></span> <span data-ttu-id="49ac9-105">部署伺服器之後，您會透過 SSH 連接，以設定 Oracle 資料庫。</span><span class="sxs-lookup"><span data-stu-id="49ac9-105">Once the server is deployed, you will connect via SSH in order to configure the Oracle database.</span></span> 

<span data-ttu-id="49ac9-106">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="49ac9-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="49ac9-107">如果您選擇在本機安裝和使用 CLI，本快速入門會要求您執行 Azure CLI 2.0.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="49ac9-107">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="49ac9-108">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="49ac9-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="49ac9-109">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="49ac9-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="49ac9-110">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="49ac9-110">Create a resource group</span></span>

<span data-ttu-id="49ac9-111">使用 [az group create](/cli/azure/group#create) 命令來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="49ac9-111">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="49ac9-112">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="49ac9-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="49ac9-113">下列範例會在 eastus 位置建立名為 myResourceGroup 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="49ac9-113">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a><span data-ttu-id="49ac9-114">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="49ac9-114">Create virtual machine</span></span>

<span data-ttu-id="49ac9-115">若要建立虛擬機器，請使用 [az vm create](/cli/azure/vm#create) 命令。</span><span class="sxs-lookup"><span data-stu-id="49ac9-115">To create a virtual machine (VM), use the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="49ac9-116">下列範例會建立名為 `myVM` 的 VM。</span><span class="sxs-lookup"><span data-stu-id="49ac9-116">The following example creates a VM named `myVM`.</span></span> <span data-ttu-id="49ac9-117">如果預設的金鑰位置還沒有 SSH 金鑰的話，此範例也會建立這些金鑰。</span><span class="sxs-lookup"><span data-stu-id="49ac9-117">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="49ac9-118">若要使用一組特定金鑰，請使用 `--ssh-key-value` 選項。</span><span class="sxs-lookup"><span data-stu-id="49ac9-118">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="49ac9-119">在您建立 VM 後，Azure CLI 會顯示類似下列範例的資訊。</span><span class="sxs-lookup"><span data-stu-id="49ac9-119">After you create the VM, Azure CLI displays information similar to the following example.</span></span> <span data-ttu-id="49ac9-120">請記下 `publicIpAddress` 的值。</span><span class="sxs-lookup"><span data-stu-id="49ac9-120">Note the value for `publicIpAddress`.</span></span> <span data-ttu-id="49ac9-121">您必須使用此位址來存取 VM。</span><span class="sxs-lookup"><span data-stu-id="49ac9-121">You use this address to access the VM.</span></span>

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

## <a name="connect-to-the-vm"></a><span data-ttu-id="49ac9-122">連接至 VM</span><span class="sxs-lookup"><span data-stu-id="49ac9-122">Connect to the VM</span></span>

<span data-ttu-id="49ac9-123">若要對 VM 建立 SSH 工作階段，請使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="49ac9-123">To create an SSH session with the VM, use the following command.</span></span> <span data-ttu-id="49ac9-124">以 VM 的 `publicIpAddress` 值取代 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="49ac9-124">Replace the IP address with the `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="create-the-database"></a><span data-ttu-id="49ac9-125">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="49ac9-125">Create the database</span></span>

<span data-ttu-id="49ac9-126">Marketplace 映像上已安裝 Oracle 軟體。</span><span class="sxs-lookup"><span data-stu-id="49ac9-126">The Oracle software is already installed on the Marketplace image.</span></span> <span data-ttu-id="49ac9-127">建立範例資料庫，如下所示。</span><span class="sxs-lookup"><span data-stu-id="49ac9-127">Create a sample database as follows.</span></span> 

1.  <span data-ttu-id="49ac9-128">切換至 oracle 超級使用者，然後將接聽程式初始化以啟用記錄功能：</span><span class="sxs-lookup"><span data-stu-id="49ac9-128">Switch to the *oracle* superuser, then initialize the listener for logging:</span></span>

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    <span data-ttu-id="49ac9-129">輸出大致如下：</span><span class="sxs-lookup"><span data-stu-id="49ac9-129">The output is similar to the following:</span></span>

    ```bash
    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

    TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Log messages written to /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

    Connecting to (ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of the LISTENER
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
    The listener supports no services
    The command completed successfully
    ```

2.  <span data-ttu-id="49ac9-130">建立資料庫︰</span><span class="sxs-lookup"><span data-stu-id="49ac9-130">Create the database:</span></span>

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

    <span data-ttu-id="49ac9-131">建立資料庫需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="49ac9-131">It takes a few minutes to create the database.</span></span>

3. <span data-ttu-id="49ac9-132">設定 Oracle 變數</span><span class="sxs-lookup"><span data-stu-id="49ac9-132">Set Oracle variables</span></span>

<span data-ttu-id="49ac9-133">在連線之前，您需要設定兩個環境變數︰ORACLE_HOME 和 ORACLE_SID。</span><span class="sxs-lookup"><span data-stu-id="49ac9-133">Before you connect, you need to set two environment variables: *ORACLE_HOME* and *ORACLE_SID*.</span></span>

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
<span data-ttu-id="49ac9-134">您也可以將 ORACLE_HOME 和 ORACLE_SID 變數新增至 .bashrc 檔案。</span><span class="sxs-lookup"><span data-stu-id="49ac9-134">You also can add ORACLE_HOME and ORACLE_SID variables to the .bashrc file.</span></span> <span data-ttu-id="49ac9-135">這會儲存環境變數以供未來登入。</span><span class="sxs-lookup"><span data-stu-id="49ac9-135">This would save the environment variables for future sign-ins.</span></span> <span data-ttu-id="49ac9-136">請確認已使用您選擇的編輯器，將下列陳述式新增至 `~/.bashrc` 檔案。</span><span class="sxs-lookup"><span data-stu-id="49ac9-136">Confirm the following statements have been added to the `~/.bashrc` file using editor of your choice.</span></span>

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a><span data-ttu-id="49ac9-137">Oracle EM Express 連線能力</span><span class="sxs-lookup"><span data-stu-id="49ac9-137">Oracle EM Express connectivity</span></span>

<span data-ttu-id="49ac9-138">對於您可用來瀏覽資料庫的 GUI 管理工具，請設定 Oracle EM Express。</span><span class="sxs-lookup"><span data-stu-id="49ac9-138">For a GUI management tool that you can use to explore the database, set up Oracle EM Express.</span></span> <span data-ttu-id="49ac9-139">若要連線到 Oracle EM Express，您必須先在 Oracle 中設定連接埠。</span><span class="sxs-lookup"><span data-stu-id="49ac9-139">To connect to Oracle EM Express, you must first set up the port in Oracle.</span></span> 

1. <span data-ttu-id="49ac9-140">使用 sqlplus 連線到您的資料庫：</span><span class="sxs-lookup"><span data-stu-id="49ac9-140">Connect to your database using sqlplus:</span></span>

    ```bash
    sqlplus / as sysdba
    ```

2. <span data-ttu-id="49ac9-141">連線後，請針對 EM Express 設定連接埠 5502</span><span class="sxs-lookup"><span data-stu-id="49ac9-141">Once connected, set the port 5502 for EM Express</span></span>

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. <span data-ttu-id="49ac9-142">如果容器 PDB1 尚未開啟，請加以開啟，但是先檢查狀態：</span><span class="sxs-lookup"><span data-stu-id="49ac9-142">Open the container PDB1 if not already opened, but first check the status:</span></span>

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    <span data-ttu-id="49ac9-143">輸出大致如下：</span><span class="sxs-lookup"><span data-stu-id="49ac9-143">The output is similar to the following:</span></span>

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. <span data-ttu-id="49ac9-144">如果 `PDB1` 的 OPEN_MODE 不是「讀寫」，則執行下列命令以開啟 PDB1：</span><span class="sxs-lookup"><span data-stu-id="49ac9-144">If the OPEN_MODE for `PDB1` is not READ WRITE, then run the followings commands to open PDB1:</span></span>

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

<span data-ttu-id="49ac9-145">您需要鍵入 `quit` 結束 sqlplus 工作階段，並鍵入 `exit` 登出 oracle 使用者。</span><span class="sxs-lookup"><span data-stu-id="49ac9-145">You need to type `quit` to end the sqlplus session and type `exit` to logout of the oracle user.</span></span>

## <a name="automate-database-startup-and-shutdown"></a><span data-ttu-id="49ac9-146">自動進行資料庫啟動和關機</span><span class="sxs-lookup"><span data-stu-id="49ac9-146">Automate database startup and shutdown</span></span>

<span data-ttu-id="49ac9-147">當您重新啟動 VM 時，Oracle 資料庫預設不會自動啟動。</span><span class="sxs-lookup"><span data-stu-id="49ac9-147">The Oracle database by default doesn't automatically start when you restart the VM.</span></span> <span data-ttu-id="49ac9-148">若要將 Oracle 資料庫設定為自動啟動，請先以 root 的身分登入。</span><span class="sxs-lookup"><span data-stu-id="49ac9-148">To set up the Oracle database to start automatically, first sign in as root.</span></span> <span data-ttu-id="49ac9-149">接著，建立並更新一些系統檔案。</span><span class="sxs-lookup"><span data-stu-id="49ac9-149">Then, create and update some system files.</span></span>

1. <span data-ttu-id="49ac9-150">以 root 的身分登入</span><span class="sxs-lookup"><span data-stu-id="49ac9-150">Sign on as root</span></span>
    ```bash
    sudo su -
    ```

2.  <span data-ttu-id="49ac9-151">使用您最愛的編輯器，編輯 `/etc/oratab` 檔案，並將預設的 `N` 變更為 `Y`：</span><span class="sxs-lookup"><span data-stu-id="49ac9-151">Using your favorite editor, edit the file `/etc/oratab` and change the default `N` to `Y`:</span></span>

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  <span data-ttu-id="49ac9-152">建立名為 `/etc/init.d/dbora` 的檔案，並貼上下列內容︰</span><span class="sxs-lookup"><span data-stu-id="49ac9-152">Create a file named `/etc/init.d/dbora` and paste the following contents:</span></span>

    ```
    #!/bin/sh
    # chkconfig: 345 99 10
    # Description: Oracle auto start-stop script.
    #
    # Set ORA_HOME to be equivalent to $ORACLE_HOME.
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle

    case "$1" in
    'start')
        # Start the Oracle databases:
        # The following command assumes that the Oracle sign-in
        # will not prompt the user for any values.
        # Remove "&" if you don't want startup as a background process.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" &
        touch /var/lock/subsys/dbora
        ;;

    'stop')
        # Stop the Oracle databases:
        # The following command assumes that the Oracle sign-in
        # will not prompt the user for any values.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" &
        rm -f /var/lock/subsys/dbora
        ;;
    esac
    ```

4.  <span data-ttu-id="49ac9-153">使用 chmod 變更檔案的權限，如下所示：</span><span class="sxs-lookup"><span data-stu-id="49ac9-153">Change permissions on files with *chmod* as follows:</span></span>

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  <span data-ttu-id="49ac9-154">建立用於啟動和關閉的符號連結，如下所示：</span><span class="sxs-lookup"><span data-stu-id="49ac9-154">Create symbolic links for startup and shutdown as follows:</span></span>

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  <span data-ttu-id="49ac9-155">若要測試您的變更，請重新啟動 VM：</span><span class="sxs-lookup"><span data-stu-id="49ac9-155">To test your changes, restart the VM:</span></span>

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a><span data-ttu-id="49ac9-156">開始連接埠進行連線</span><span class="sxs-lookup"><span data-stu-id="49ac9-156">Open ports for connectivity</span></span>

<span data-ttu-id="49ac9-157">最後一項工作是設定一些外部端點。</span><span class="sxs-lookup"><span data-stu-id="49ac9-157">The final task is to configure some external endpoints.</span></span> <span data-ttu-id="49ac9-158">若要設定可保護 VM 的 Azure 網路安全性群組，請先結束 VM 中您的 SSH 工作階段 (應已在前一個步驟中重新啟動時被移出 SSH)。</span><span class="sxs-lookup"><span data-stu-id="49ac9-158">To set up the Azure Network Security Group that protects the VM, first exit your SSH session in the VM (should have been kicked out of SSH when rebooting in previous step).</span></span> 

1.  <span data-ttu-id="49ac9-159">若要開啟您用來從遠端存取 Oracle 資料庫的端點，請使用 [az network nsg rule create](/cli/azure/network/nsg/rule#create) 建立網路安全性群組規則，如下所示：</span><span class="sxs-lookup"><span data-stu-id="49ac9-159">To open the endpoint that you use to access the Oracle database remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span> 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  <span data-ttu-id="49ac9-160">若要開啟您用來從遠端存取 Oracle EM Express 的端點，請使用 [az network nsg rule create](/cli/azure/network/nsg/rule#create) 建立網路安全性群組規則，如下所示：</span><span class="sxs-lookup"><span data-stu-id="49ac9-160">To open the endpoint that you use to access Oracle EM Express remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span>

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. <span data-ttu-id="49ac9-161">如有需要，請使用 [az network public-ip show](/cli/azure/network/public-ip#show) 再次取得 VM 的公用 IP 位址，如下所示：</span><span class="sxs-lookup"><span data-stu-id="49ac9-161">If needed, obtain the public IP address of your VM again with [az network public-ip show](/cli/azure/network/public-ip#show) as follows:</span></span>

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  <span data-ttu-id="49ac9-162">從您的瀏覽器連接 EM Express。</span><span class="sxs-lookup"><span data-stu-id="49ac9-162">Connect EM Express from your browser.</span></span> <span data-ttu-id="49ac9-163">確定您的瀏覽器與 EM Express 相容 (需要安裝 Flash)：</span><span class="sxs-lookup"><span data-stu-id="49ac9-163">Make sure your browser is compatible with EM Express (Flash install is required):</span></span> 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

<span data-ttu-id="49ac9-164">您可以使用 SYS 帳戶進行登入，然後勾選 as sysdba 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="49ac9-164">You can log in by using the **SYS** account, and check the **as sysdba** checkbox.</span></span> <span data-ttu-id="49ac9-165">使用您在安裝期間設定的密碼 OraPasswd1。</span><span class="sxs-lookup"><span data-stu-id="49ac9-165">Use the password **OraPasswd1** that you set during installation.</span></span> 

![Oracle OEM Express 登入頁面的螢幕擷取畫面](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a><span data-ttu-id="49ac9-167">清除資源</span><span class="sxs-lookup"><span data-stu-id="49ac9-167">Clean up resources</span></span>

<span data-ttu-id="49ac9-168">完成在 Azure 上探索第一個 Oracle 資料庫而且不再需要 VM 之後，就可以使用 [az group delete](/cli/azure/group#delete) 命令移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="49ac9-168">Once you have finished exploring your first Oracle database on Azure and the VM is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="49ac9-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="49ac9-169">Next steps</span></span>

<span data-ttu-id="49ac9-170">深入了解 [Azure 上的其他 Oracle 解決方案](oracle-considerations.md)。</span><span class="sxs-lookup"><span data-stu-id="49ac9-170">Learn about other [Oracle solutions on Azure](oracle-considerations.md).</span></span> 

<span data-ttu-id="49ac9-171">嘗試[安裝和設定 Oracle Automated Storage Management](configure-oracle-asm.md) 教學課程。</span><span class="sxs-lookup"><span data-stu-id="49ac9-171">Try the [Installing and Configuring Oracle Automated Storage Management](configure-oracle-asm.md) tutorial.</span></span>