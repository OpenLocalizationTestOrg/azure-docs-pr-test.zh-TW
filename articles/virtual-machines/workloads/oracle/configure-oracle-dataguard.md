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
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="101c2-103">在 Azure Linux 虛擬機器上實作 Oracle Data Guard</span><span class="sxs-lookup"><span data-stu-id="101c2-103">Implement Oracle Data Guard on an Azure Linux virtual machine</span></span> 

<span data-ttu-id="101c2-104">Azure CLI 會使用的 toocreate，及管理 Azure 資源，從 hello 命令列或指令碼中。</span><span class="sxs-lookup"><span data-stu-id="101c2-104">Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="101c2-105">本文說明如何 toouse Azure CLI toodeploy Oracle Database 12c 資料庫從 hello Azure Marketplace 映像。</span><span class="sxs-lookup"><span data-stu-id="101c2-105">This article describes how toouse Azure CLI toodeploy an Oracle Database 12c database from hello Azure Marketplace image.</span></span> <span data-ttu-id="101c2-106">這篇文章然後為您示範，逐步解說，如何 tooinstall 和 Azure 的虛擬機器 (VM) 上設定資料保護。</span><span class="sxs-lookup"><span data-stu-id="101c2-106">This article then shows you, step by step, how tooinstall and configure Data Guard on an Azure virtual machine (VM).</span></span>

<span data-ttu-id="101c2-107">在開始之前，請確定您已安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="101c2-107">Before you start, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="101c2-108">如需詳細資訊，請參閱 hello [Azure CLI 安裝指南](https://docs.microsoft.com/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="101c2-108">For more information, see hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="101c2-109">準備 hello 環境</span><span class="sxs-lookup"><span data-stu-id="101c2-109">Prepare hello environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="101c2-110">假設</span><span class="sxs-lookup"><span data-stu-id="101c2-110">Assumptions</span></span>

<span data-ttu-id="101c2-111">tooinstall Oracle 資料保護，您需要 toocreate 兩個 Azure Vm 上 hello 相同可用性設定組：</span><span class="sxs-lookup"><span data-stu-id="101c2-111">tooinstall Oracle Data Guard, you need toocreate two Azure VMs on hello same availability set:</span></span>

- <span data-ttu-id="101c2-112">hello 主要 VM (myVM1) 具有正在執行的 Oracle 執行個體。</span><span class="sxs-lookup"><span data-stu-id="101c2-112">hello primary VM (myVM1) has a running Oracle instance.</span></span>
- <span data-ttu-id="101c2-113">hello 待命 VM (myVM2) 具有只安裝 hello Oracle 軟體。</span><span class="sxs-lookup"><span data-stu-id="101c2-113">hello standby VM (myVM2) has hello Oracle software installed only.</span></span>

<span data-ttu-id="101c2-114">hello Marketplace 映像，您會使用 toocreate hello Vm 是 Oracle: Oracle-資料庫-Ee:12.1.0.2:latest。</span><span class="sxs-lookup"><span data-stu-id="101c2-114">hello Marketplace image that you use toocreate hello VMs is Oracle:Oracle-Database-Ee:12.1.0.2:latest.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="101c2-115">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="101c2-115">Sign in tooAzure</span></span> 

<span data-ttu-id="101c2-116">使用 hello 登入 Azure 訂用帳戶 tooyour [az 登入](/cli/azure/#login)命令，並遵循螢幕上指示 hello。</span><span class="sxs-lookup"><span data-stu-id="101c2-116">Sign in tooyour Azure subscription by using hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="101c2-117">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="101c2-117">Create a resource group</span></span>

<span data-ttu-id="101c2-118">建立資源群組使用 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="101c2-118">Create a resource group by using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="101c2-119">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="101c2-119">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="101c2-120">hello 下列範例會建立名為的資源群組`myResourceGroup`在 hello`westus`位置：</span><span class="sxs-lookup"><span data-stu-id="101c2-120">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="101c2-121">建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="101c2-121">Create an availability set</span></span>

<span data-ttu-id="101c2-122">建立可用性設定組是選擇性的，但我們仍建議您這麼做。</span><span class="sxs-lookup"><span data-stu-id="101c2-122">Creating an availability set is optional, but we recommend it.</span></span> <span data-ttu-id="101c2-123">如需詳細資訊，請參閱 [Azure 可用性設定組指導方針](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines)。</span><span class="sxs-lookup"><span data-stu-id="101c2-123">For more information, see [Azure availability sets guidelines](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="101c2-124">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="101c2-124">Create a virtual machine</span></span>

<span data-ttu-id="101c2-125">建立 VM 使用 hello [az vm 建立](/cli/azure/vm#create)命令。</span><span class="sxs-lookup"><span data-stu-id="101c2-125">Create a VM by using hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="101c2-126">hello 下列範例會建立名為兩個 Vm`myVM1`和`myVM2`。</span><span class="sxs-lookup"><span data-stu-id="101c2-126">hello following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="101c2-127">如果預設的金鑰位置還沒有 SSH 金鑰的話，此範例也會建立這些金鑰。</span><span class="sxs-lookup"><span data-stu-id="101c2-127">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="101c2-128">toouse 一組特定的金鑰，請使用 hello`--ssh-key-value`選項。</span><span class="sxs-lookup"><span data-stu-id="101c2-128">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

<span data-ttu-id="101c2-129">建立 myVM1 (主要)：</span><span class="sxs-lookup"><span data-stu-id="101c2-129">Create myVM1 (primary):</span></span>
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

<span data-ttu-id="101c2-130">您建立 hello VM 之後，Azure CLI 就會顯示下列範例的資訊類似 toohello。</span><span class="sxs-lookup"><span data-stu-id="101c2-130">After you create hello VM, Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="101c2-131">請注意 hello 值`publicIpAddress`。</span><span class="sxs-lookup"><span data-stu-id="101c2-131">Note hello value of `publicIpAddress`.</span></span> <span data-ttu-id="101c2-132">您使用此位址 tooaccess hello VM。</span><span class="sxs-lookup"><span data-stu-id="101c2-132">You use this address tooaccess hello VM.</span></span>

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

<span data-ttu-id="101c2-133">建立 myVM2 (待命)：</span><span class="sxs-lookup"><span data-stu-id="101c2-133">Create myVM2 (standby):</span></span>
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

<span data-ttu-id="101c2-134">請注意 hello 值`publicIpAddress`建立 myVM2 之後。</span><span class="sxs-lookup"><span data-stu-id="101c2-134">Note hello value of `publicIpAddress` after you create myVM2.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="101c2-135">開啟 hello 連線的 TCP 連接埠</span><span class="sxs-lookup"><span data-stu-id="101c2-135">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="101c2-136">此步驟會設定允許遠端存取 toohello Oracle 資料庫中的外部端點。</span><span class="sxs-lookup"><span data-stu-id="101c2-136">This step configures external endpoints, which allow remote access toohello Oracle database.</span></span>

<span data-ttu-id="101c2-137">開啟 myVM1 hello 連接埠：</span><span class="sxs-lookup"><span data-stu-id="101c2-137">Open hello port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="101c2-138">hello 結果看起來類似 toohello 下列回應：</span><span class="sxs-lookup"><span data-stu-id="101c2-138">hello result should look similar toohello following response:</span></span>

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

<span data-ttu-id="101c2-139">開啟 myVM2 hello 連接埠：</span><span class="sxs-lookup"><span data-stu-id="101c2-139">Open hello port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="101c2-140">Toohello 虛擬機器連線</span><span class="sxs-lookup"><span data-stu-id="101c2-140">Connect toohello virtual machine</span></span>

<span data-ttu-id="101c2-141">使用 hello 下列命令 toocreate 與 hello 虛擬機器的 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="101c2-141">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="101c2-142">Hello IP 位址取代成 hello`publicIpAddress`虛擬機器的值。</span><span class="sxs-lookup"><span data-stu-id="101c2-142">Replace hello IP address with hello `publicIpAddress` value for your virtual machine.</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a><span data-ttu-id="101c2-143">建立 myVM1 hello 資料庫 （主要）</span><span class="sxs-lookup"><span data-stu-id="101c2-143">Create hello database on myVM1 (primary)</span></span>

<span data-ttu-id="101c2-144">hello Oracle 軟體上已安裝 hello Marketplace 映像，因此 hello 下一個步驟是 tooinstall hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="101c2-144">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> 

<span data-ttu-id="101c2-145">切換 toohello Oracle 超級使用者：</span><span class="sxs-lookup"><span data-stu-id="101c2-145">Switch toohello Oracle superuser:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="101c2-146">建立 hello 資料庫：</span><span class="sxs-lookup"><span data-stu-id="101c2-146">Create hello database:</span></span>

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
<span data-ttu-id="101c2-147">輸出應該看起來類似 toohello 下列回應：</span><span class="sxs-lookup"><span data-stu-id="101c2-147">Outputs should look similar toohello following response:</span></span>

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

<span data-ttu-id="101c2-148">設定 hello ORACLE_SID 和 ORACLE_HOME 變數：</span><span class="sxs-lookup"><span data-stu-id="101c2-148">Set hello ORACLE_SID and ORACLE_HOME variables:</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="101c2-149">（選擇性） 您可以加入 ORACLE_HOME 和 ORACLE_SID toohello /home/oracle/.bashrc 檔案，以便這些設定會儲存為未來的登入：</span><span class="sxs-lookup"><span data-stu-id="101c2-149">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a><span data-ttu-id="101c2-150">設定 Data Guard</span><span class="sxs-lookup"><span data-stu-id="101c2-150">Configure Data Guard</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="101c2-151">在 myVM1 (主要) 上啟用封存記錄模式</span><span class="sxs-lookup"><span data-stu-id="101c2-151">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="101c2-152">啟用強制記錄功能，並確定至少有一個記錄檔存在：</span><span class="sxs-lookup"><span data-stu-id="101c2-152">Enable force logging, and make sure at least one log file is present:</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="101c2-153">建立待命重做記錄：</span><span class="sxs-lookup"><span data-stu-id="101c2-153">Create standby redo logs:</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="101c2-154">回溯 （這樣會復原來得簡單許多） 開啟，並設定待命\_檔案\_管理 tooauto。</span><span class="sxs-lookup"><span data-stu-id="101c2-154">Turn on Flashback (which makes recovery a lot easier) and set STANDBY\_FILE\_MANAGEMENT tooauto.</span></span> <span data-ttu-id="101c2-155">在此之後結束 SQL*Plus。</span><span class="sxs-lookup"><span data-stu-id="101c2-155">Exit SQL*Plus after that.</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="101c2-156">設定 myVM1 (主要) 上的服務</span><span class="sxs-lookup"><span data-stu-id="101c2-156">Set up service on myVM1 (primary)</span></span>

<span data-ttu-id="101c2-157">編輯或建立 hello $ORACLE_HOME\network\admin 資料夾中的 hello tnsnames.ora 檔案。</span><span class="sxs-lookup"><span data-stu-id="101c2-157">Edit or create hello tnsnames.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="101c2-158">加入下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="101c2-158">Add hello following entries:</span></span>

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

<span data-ttu-id="101c2-159">編輯或建立 hello $ORACLE_HOME\network\admin 資料夾中的 hello listener.ora 檔案。</span><span class="sxs-lookup"><span data-stu-id="101c2-159">Edit or create hello listener.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="101c2-160">加入下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="101c2-160">Add hello following entries:</span></span>

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

<span data-ttu-id="101c2-161">啟用 Data Guard Broker：</span><span class="sxs-lookup"><span data-stu-id="101c2-161">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
<span data-ttu-id="101c2-162">啟動 hello 接聽程式：</span><span class="sxs-lookup"><span data-stu-id="101c2-162">Start hello listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a><span data-ttu-id="101c2-163">設定 myVM2 (待命) 上的服務</span><span class="sxs-lookup"><span data-stu-id="101c2-163">Set up service on myVM2 (standby)</span></span>

<span data-ttu-id="101c2-164">SSH toomyVM2:</span><span class="sxs-lookup"><span data-stu-id="101c2-164">SSH toomyVM2:</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="101c2-165">以 Oracle 的身分登入：</span><span class="sxs-lookup"><span data-stu-id="101c2-165">Log in as Oracle:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="101c2-166">編輯或建立 hello $ORACLE_HOME\network\admin 資料夾中的 hello tnsnames.ora 檔案。</span><span class="sxs-lookup"><span data-stu-id="101c2-166">Edit or create hello tnsnames.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="101c2-167">加入下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="101c2-167">Add hello following entries:</span></span>

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

<span data-ttu-id="101c2-168">編輯或建立 hello $ORACLE_HOME\network\admin 資料夾中的 hello listener.ora 檔案。</span><span class="sxs-lookup"><span data-stu-id="101c2-168">Edit or create hello listener.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="101c2-169">加入下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="101c2-169">Add hello following entries:</span></span>

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

<span data-ttu-id="101c2-170">啟動 hello 接聽程式：</span><span class="sxs-lookup"><span data-stu-id="101c2-170">Start hello listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-hello-database-toomyvm2-standby"></a><span data-ttu-id="101c2-171">還原 hello 資料庫 toomyVM2 （待命）</span><span class="sxs-lookup"><span data-stu-id="101c2-171">Restore hello database toomyVM2 (standby)</span></span>

<span data-ttu-id="101c2-172">建立 hello 參數檔案 /tmp/initcdb1_stby.ora 以 hello 下列內容：</span><span class="sxs-lookup"><span data-stu-id="101c2-172">Create hello parameter file /tmp/initcdb1_stby.ora with hello following contents:</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="101c2-173">建立資料夾：</span><span class="sxs-lookup"><span data-stu-id="101c2-173">Create folders:</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="101c2-174">建立密碼檔案：</span><span class="sxs-lookup"><span data-stu-id="101c2-174">Create a password file:</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="101c2-175">開始在 myVM2 hello 資料庫：</span><span class="sxs-lookup"><span data-stu-id="101c2-175">Start hello database on myVM2:</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="101c2-176">使用 hello RMAN 工具還原 hello 資料庫：</span><span class="sxs-lookup"><span data-stu-id="101c2-176">Restore hello database by using hello RMAN tool:</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="101c2-177">執行下列命令中 RMAN hello:</span><span class="sxs-lookup"><span data-stu-id="101c2-177">Run hello following commands in RMAN:</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="101c2-178">Hello 命令完成時，應該會看到類似 toohello 下列訊息。</span><span class="sxs-lookup"><span data-stu-id="101c2-178">You should see messages similar toohello following when hello command is completed.</span></span> <span data-ttu-id="101c2-179">結束 RMAN。</span><span class="sxs-lookup"><span data-stu-id="101c2-179">Exit RMAN.</span></span>
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

<span data-ttu-id="101c2-180">（選擇性） 您可以加入 ORACLE_HOME 和 ORACLE_SID toohello /home/oracle/.bashrc 檔案，以便這些設定會儲存為未來的登入：</span><span class="sxs-lookup"><span data-stu-id="101c2-180">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

<span data-ttu-id="101c2-181">啟用 Data Guard Broker：</span><span class="sxs-lookup"><span data-stu-id="101c2-181">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="101c2-182">在 myVM1 (主要) 上設定 Data Guard Broker</span><span class="sxs-lookup"><span data-stu-id="101c2-182">Configure Data Guard Broker on myVM1 (primary)</span></span>

<span data-ttu-id="101c2-183">啟動 Data Guard Manager，並使用 SYS 和密碼登入。</span><span class="sxs-lookup"><span data-stu-id="101c2-183">Start Data Guard Manager and log in by using SYS and a password.</span></span> <span data-ttu-id="101c2-184">(請勿使用 OS 驗證。)執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="101c2-184">(Do not use OS authentication.) Perform hello following:</span></span>

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

<span data-ttu-id="101c2-185">檢閱 hello 設定：</span><span class="sxs-lookup"><span data-stu-id="101c2-185">Review hello configuration:</span></span>
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

<span data-ttu-id="101c2-186">您已經完成 hello Oracle 資料保護設定。</span><span class="sxs-lookup"><span data-stu-id="101c2-186">You've completed hello Oracle Data Guard setup.</span></span> <span data-ttu-id="101c2-187">hello 下一節將說明如何 tootest hello 連線並切換。</span><span class="sxs-lookup"><span data-stu-id="101c2-187">hello next section shows you how tootest hello connectivity and switch over.</span></span>

### <a name="connect-hello-database-from-hello-client-machine"></a><span data-ttu-id="101c2-188">從 hello 用戶端電腦連接 hello 資料庫</span><span class="sxs-lookup"><span data-stu-id="101c2-188">Connect hello database from hello client machine</span></span>

<span data-ttu-id="101c2-189">更新或建立您的用戶端電腦上的 hello tnsnames.ora 檔案。</span><span class="sxs-lookup"><span data-stu-id="101c2-189">Update or create hello tnsnames.ora file on your client machine.</span></span> <span data-ttu-id="101c2-190">這個檔案通常位於 $ORACLE_HOME\network\admin。</span><span class="sxs-lookup"><span data-stu-id="101c2-190">This file is usually in $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="101c2-191">取代 hello IP 位址，與您`publicIpAddress`myVM1 和 myVM2 值：</span><span class="sxs-lookup"><span data-stu-id="101c2-191">Replace hello IP addresses with your `publicIpAddress` values for myVM1 and myVM2:</span></span>

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

<span data-ttu-id="101c2-192">啟動 SQL*Plus：</span><span class="sxs-lookup"><span data-stu-id="101c2-192">Start SQL*Plus:</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-hello-data-guard-configuration"></a><span data-ttu-id="101c2-193">測試 hello 資料保護設定</span><span class="sxs-lookup"><span data-stu-id="101c2-193">Test hello Data Guard configuration</span></span>

### <a name="switch-over-hello-database-on-myvm1-primary"></a><span data-ttu-id="101c2-194">切換 hello myVM1 （主要） 上的資料庫</span><span class="sxs-lookup"><span data-stu-id="101c2-194">Switch over hello database on myVM1 (primary)</span></span>

<span data-ttu-id="101c2-195">從主要 toostandby (cdb1 toocdb1_stby) tooswitch:</span><span class="sxs-lookup"><span data-stu-id="101c2-195">tooswitch from primary toostandby (cdb1 toocdb1_stby):</span></span>

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

<span data-ttu-id="101c2-196">您現在可以連接 toohello 待命資料庫。</span><span class="sxs-lookup"><span data-stu-id="101c2-196">You can now connect toohello standby database.</span></span>

<span data-ttu-id="101c2-197">啟動 SQL*Plus：</span><span class="sxs-lookup"><span data-stu-id="101c2-197">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-hello-database-on-myvm2-standby"></a><span data-ttu-id="101c2-198">切換 myVM2 hello 資料庫 （待命）</span><span class="sxs-lookup"><span data-stu-id="101c2-198">Switch over hello database on myVM2 (standby)</span></span>

<span data-ttu-id="101c2-199">進入 tooswitch 執行 myVM2 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="101c2-199">tooswitch over, run hello following on myVM2:</span></span>
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

<span data-ttu-id="101c2-200">同樣地，您現在應該能夠 tooconnect toohello 主要資料庫。</span><span class="sxs-lookup"><span data-stu-id="101c2-200">Once again, you should now be able tooconnect toohello primary database.</span></span>

<span data-ttu-id="101c2-201">啟動 SQL*Plus：</span><span class="sxs-lookup"><span data-stu-id="101c2-201">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="101c2-202">您已完成 hello 安裝和設定 Oracle Linux 上的資料保護。</span><span class="sxs-lookup"><span data-stu-id="101c2-202">You've finished hello installation and configuration of Data Guard on Oracle Linux.</span></span>


## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="101c2-203">刪除 hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="101c2-203">Delete hello virtual machine</span></span>

<span data-ttu-id="101c2-204">當您不再需要 hello VM 時，您可以使用下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="101c2-204">When you no longer need hello VM, you can use hello following command tooremove hello resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="101c2-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="101c2-205">Next steps</span></span>

[<span data-ttu-id="101c2-206">教學課程：建立高可用性的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="101c2-206">Tutorial: Create highly available virtual machines</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="101c2-207">瀏覽 VM 部署 Azure CLI 範例</span><span class="sxs-lookup"><span data-stu-id="101c2-207">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
