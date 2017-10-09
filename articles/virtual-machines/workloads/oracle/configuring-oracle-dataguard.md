---
title: "Azure Linux VM 上的 Oracle 資料防護 aaaImplement |Microsoft 文件"
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
ms.openlocfilehash: 101196b2f50dfca64d3eb1b4be56ff0c108693e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-azure-linux-vm"></a><span data-ttu-id="2d6dd-103">在 Azure Linux VM 上實作 Oracle Data Guard</span><span class="sxs-lookup"><span data-stu-id="2d6dd-103">Implement Oracle Data Guard on Azure Linux VM</span></span> 

<span data-ttu-id="2d6dd-104">hello Azure CLI 會使用的 toocreate 和管理 Azure 資源，從 hello 命令列或指令碼中。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="2d6dd-105">本指南將詳細說明使用 hello Azure CLI toodeploy 的 Oracle 12c 資料庫從 hello Marketplace 圖庫映像。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-105">This guide details using hello Azure CLI toodeploy an Oracle 12c Database from hello Marketplace gallery image.</span></span> <span data-ttu-id="2d6dd-106">Hello Oracle 資料庫建立之後，本文件說明如何逐步 tooinstall 和 Azure VM 上設定資料保護。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-106">Once hello Oracle database is created, this document shows you step-by-step how tooinstall and configure Data Guard on Azure VM.</span></span>

<span data-ttu-id="2d6dd-107">開始之前，請確定已安裝 Azure CLI 該 hello。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-107">Before you start, make sure that hello Azure CLI has been installed.</span></span> <span data-ttu-id="2d6dd-108">如需詳細資訊，請參閱 [Azure CLI 安裝指南](https://docs.microsoft.com/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="2d6dd-109">準備 hello 環境</span><span class="sxs-lookup"><span data-stu-id="2d6dd-109">Prepare hello environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="2d6dd-110">假設</span><span class="sxs-lookup"><span data-stu-id="2d6dd-110">Assumptions</span></span>

<span data-ttu-id="2d6dd-111">Oracle 資料防護安裝 tooperform hello，您需要 toocreate 兩個 Azure Vm 上 hello 相同可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-111">tooperform hello Oracle Data Guard install, you need toocreate two Azure VMs on hello same availability set.</span></span> <span data-ttu-id="2d6dd-112">hello Marketplace 映像使用 toocreate hello Vm 為 「 Oracle: Oracle-資料庫-Ee:12.1.0.2:latest"。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-112">hello Marketplace image you use toocreate hello VMs is "Oracle:Oracle-Database-Ee:12.1.0.2:latest".</span></span>

<span data-ttu-id="2d6dd-113">hello 主要 VM (myVM1) 具有正在執行的 Oracle 執行個體。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-113">hello primary VM (myVM1) has a running Oracle instance.</span></span>

<span data-ttu-id="2d6dd-114">hello 待命 VM (myVM2) 具有只安裝 hello Oracle 軟體。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-114">hello standby VM (myVM2) has hello Oracle software installed only.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="2d6dd-115">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="2d6dd-115">Log in tooAzure</span></span> 

<span data-ttu-id="2d6dd-116">登入 Azure 訂用帳戶以 hello tooyour [az 登入](/cli/azure/#login)命令，並遵循螢幕上指示 hello。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-116">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="2d6dd-117">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="2d6dd-117">Create a resource group</span></span>

<span data-ttu-id="2d6dd-118">建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-118">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="2d6dd-119">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-119">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="2d6dd-120">hello 下列範例會建立名為的資源群組`myResourceGroup`在 hello`westus`位置。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-120">hello following example creates a resource group named `myResourceGroup` in hello `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-availability-set"></a><span data-ttu-id="2d6dd-121">建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="2d6dd-121">Create availability set</span></span>

<span data-ttu-id="2d6dd-122">此步驟為選用步驟，但建議執行。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-122">This step is optional, but is recommended.</span></span> <span data-ttu-id="2d6dd-123">如需詳細資訊，請參閱 [Azure 可用性設定組指南](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines)。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-123">see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) for more information.</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-virtual-machine"></a><span data-ttu-id="2d6dd-124">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="2d6dd-124">Create virtual machine</span></span>

<span data-ttu-id="2d6dd-125">建立 VM 以 hello [az vm 建立](/cli/azure/vm#create)命令。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-125">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="2d6dd-126">hello 下列範例會建立名為 2 個 Vm`myVM1`和`myVM2`。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-126">hello following example creates 2 VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="2d6dd-127">如果預設的金鑰位置還沒有 SSH 金鑰，請建立這些金鑰。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-127">Creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="2d6dd-128">toouse 一組特定的金鑰，請使用 hello`--ssh-key-value`選項。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-128">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

<span data-ttu-id="2d6dd-129">建立 myVM1 (主要)</span><span class="sxs-lookup"><span data-stu-id="2d6dd-129">Create myVM1 (primary)</span></span>
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

<span data-ttu-id="2d6dd-130">一次在建立 VM 的 hello，hello Azure CLI 顯示下列範例的資訊類似 toohello: hello Take 記下`publicIpAddress`。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-130">Once hello VM has been created, hello Azure CLI shows information similar toohello following example: Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="2d6dd-131">此位址為使用的 tooaccess hello VM。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-131">This address is used tooaccess hello VM.</span></span>

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

<span data-ttu-id="2d6dd-132">建立 myVM2 (待命)</span><span class="sxs-lookup"><span data-stu-id="2d6dd-132">Create myVM2 (standby)</span></span>
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

<span data-ttu-id="2d6dd-133">記下 hello`publicIpAddress`建立它以及一次。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-133">Take note of hello `publicIpAddress` as well once it created.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="2d6dd-134">開啟 hello 連線的 TCP 連接埠</span><span class="sxs-lookup"><span data-stu-id="2d6dd-134">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="2d6dd-135">hello 步驟是 tooconfigure 外部端點，這可以讓遠端存取 hello Oracle DB，請執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-135">hello step is tooconfigure external endpoints, which allows accessing hello Oracle DB remotely, you execute hello following command.</span></span>

<span data-ttu-id="2d6dd-136">開啟 myVM1 的連接埠</span><span class="sxs-lookup"><span data-stu-id="2d6dd-136">Open port for myVM1</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVmN1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="2d6dd-137">結果看起來類似 toohello 下列回應：</span><span class="sxs-lookup"><span data-stu-id="2d6dd-137">Result should look similar toohello following response:</span></span>

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

<span data-ttu-id="2d6dd-138">開啟 myVM2 的連接埠</span><span class="sxs-lookup"><span data-stu-id="2d6dd-138">Open port for myVM2</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2N1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toovirtual-machine"></a><span data-ttu-id="2d6dd-139">Toovirtual 機器連線</span><span class="sxs-lookup"><span data-stu-id="2d6dd-139">Connect toovirtual machine</span></span>

<span data-ttu-id="2d6dd-140">使用 hello 下列命令 toocreate 與 hello 虛擬機器的 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-140">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="2d6dd-141">Hello IP 位址取代成 hello`publicIpAddress`的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-141">Replace hello IP address with hello `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh azureuser@<publicIpAddress>
```

### <a name="create-database-on-myvm1-primary"></a><span data-ttu-id="2d6dd-142">在 myVM1 (主要) 上建立資料庫</span><span class="sxs-lookup"><span data-stu-id="2d6dd-142">Create Database on myVM1 (Primary)</span></span>

<span data-ttu-id="2d6dd-143">hello Oracle 軟體上已安裝 hello Marketplace 映像，因此 hello 下一個步驟是 tooinstall hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-143">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> <span data-ttu-id="2d6dd-144">hello 第一個步驟以 hello 'oracle' 超級使用者執行。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-144">hello first step is running as hello 'oracle' superuser.</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="2d6dd-145">建立 hello 資料庫：</span><span class="sxs-lookup"><span data-stu-id="2d6dd-145">create hello database:</span></span>

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
<span data-ttu-id="2d6dd-146">輸出應該看起來類似 toohello 下列回應：</span><span class="sxs-lookup"><span data-stu-id="2d6dd-146">Outputs should look similar toohello following response:</span></span>

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

<span data-ttu-id="2d6dd-147">設定 hello ORACLE_SID 和 ORACLE_HOME 變數</span><span class="sxs-lookup"><span data-stu-id="2d6dd-147">Set hello ORACLE_SID and ORACLE_HOME variables</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="2d6dd-148">（選擇性） 您可以加入的 ORACLE_HOME 和 ORACLE_SID toohello.bashrc 的檔案，以便這些設定會儲存為未來的登入。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-148">Optionally, You can added ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future logins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="data-guard-configurations"></a><span data-ttu-id="2d6dd-149">Data Guard 組態</span><span class="sxs-lookup"><span data-stu-id="2d6dd-149">Data Guard Configurations</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="2d6dd-150">在 myVM1 (主要) 上啟用封存記錄模式</span><span class="sxs-lookup"><span data-stu-id="2d6dd-150">Enable Archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="2d6dd-151">啟用強制記錄功能，並確定至少有一個記錄檔存在。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-151">Enable force logging, and make sure at least one logfile is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="2d6dd-152">建立待命重做記錄</span><span class="sxs-lookup"><span data-stu-id="2d6dd-152">Create standby redo logs</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="2d6dd-153">回溯 （其中許多之前建立 hello 復原） 開啟，並設定 STANDBY_FILE_MANAGEMENT tooauto</span><span class="sxs-lookup"><span data-stu-id="2d6dd-153">Turn on Flashback (which made hello recovery a lot earlier) and set STANDBY_FILE_MANAGEMENT tooauto</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
```

### <a name="service-setup-on-myvm1-primary"></a><span data-ttu-id="2d6dd-154">myVM1 (主要) 上的服務設定</span><span class="sxs-lookup"><span data-stu-id="2d6dd-154">Service setup on myVM1 (primary)</span></span>

<span data-ttu-id="2d6dd-155">編輯或建立 hello tnsnames.ora 檔案，位於 $ORACLE_HOME\network\admin 資料夾</span><span class="sxs-lookup"><span data-stu-id="2d6dd-155">Edit or create hello tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="2d6dd-156">新增下列項目 hello</span><span class="sxs-lookup"><span data-stu-id="2d6dd-156">Add hello following entries</span></span>

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

<span data-ttu-id="2d6dd-157">編輯或建立 hello listener.ora 檔案，位於 $ORACLE_HOME\network\admin 資料夾</span><span class="sxs-lookup"><span data-stu-id="2d6dd-157">Edit or create hello listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="2d6dd-158">新增下列項目 hello</span><span class="sxs-lookup"><span data-stu-id="2d6dd-158">Add hello following entries</span></span>

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

<span data-ttu-id="2d6dd-159">啟動 hello 接聽程式</span><span class="sxs-lookup"><span data-stu-id="2d6dd-159">Start hello listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="service-setup-on-myvm2-standby"></a><span data-ttu-id="2d6dd-160">myVM2 (待命) 上的服務設定</span><span class="sxs-lookup"><span data-stu-id="2d6dd-160">Service setup on myVM2 (Standby)</span></span>

<span data-ttu-id="2d6dd-161">編輯或建立 hello tnsnames.ora 檔案，位於 $ORACLE_HOME\network\admin 資料夾</span><span class="sxs-lookup"><span data-stu-id="2d6dd-161">Edit or create hello tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="2d6dd-162">新增下列項目 hello</span><span class="sxs-lookup"><span data-stu-id="2d6dd-162">Add hello following entries</span></span>

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

<span data-ttu-id="2d6dd-163">編輯或建立 hello listener.ora 檔案，位於 $ORACLE_HOME\network\admin 資料夾</span><span class="sxs-lookup"><span data-stu-id="2d6dd-163">Edit or create hello listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="2d6dd-164">新增下列項目 hello</span><span class="sxs-lookup"><span data-stu-id="2d6dd-164">Add hello following entries</span></span>

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

<span data-ttu-id="2d6dd-165">啟動 hello 接聽程式</span><span class="sxs-lookup"><span data-stu-id="2d6dd-165">Start hello listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

<span data-ttu-id="2d6dd-166">啟用 Data Guard Broker</span><span class="sxs-lookup"><span data-stu-id="2d6dd-166">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="restore-database-toomyvm2-standby"></a><span data-ttu-id="2d6dd-167">還原資料庫 toomyVM2 （貣暀）</span><span class="sxs-lookup"><span data-stu-id="2d6dd-167">Restore database toomyVM2 (Standby)</span></span>

<span data-ttu-id="2d6dd-168">建立參數檔案 ' / tmp/initcdb1_stby.ora' hello 下列項目內容</span><span class="sxs-lookup"><span data-stu-id="2d6dd-168">Create a parameter file '/tmp/initcdb1_stby.ora' with hello followings contents</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="2d6dd-169">建立資料夾</span><span class="sxs-lookup"><span data-stu-id="2d6dd-169">Create folders</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="2d6dd-170">建立密碼檔案</span><span class="sxs-lookup"><span data-stu-id="2d6dd-170">Create password file</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0.2/db_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="2d6dd-171">在 myVM2 上啟動資料庫</span><span class="sxs-lookup"><span data-stu-id="2d6dd-171">Start up database on myVM2</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="2d6dd-172">使用 RMAN 公用程式來還原資料庫</span><span class="sxs-lookup"><span data-stu-id="2d6dd-172">Restore database using RMAN utility</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="2d6dd-173">執行下列命令中 RMAN hello</span><span class="sxs-lookup"><span data-stu-id="2d6dd-173">Execute hello following commands in RMAN</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="2d6dd-174">啟用 Data Guard Broker</span><span class="sxs-lookup"><span data-stu-id="2d6dd-174">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="2d6dd-175">在 myVM1 (主要) 上設定 Data Guard Broker</span><span class="sxs-lookup"><span data-stu-id="2d6dd-175">Configure Data Guard broker on myVM1 (primary)</span></span>

<span data-ttu-id="2d6dd-176">啟動 hello 資料防護管理員和登入使用 SYS 和密碼 （都有不使用作業系統驗證）。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-176">Start hello Data Guard manager and login using SYS and password (do not using OS authentication).</span></span> <span data-ttu-id="2d6dd-177">執行 hello 下列項目</span><span class="sxs-lookup"><span data-stu-id="2d6dd-177">Perform hello followings</span></span>

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

<span data-ttu-id="2d6dd-178">檢閱 hello 設定</span><span class="sxs-lookup"><span data-stu-id="2d6dd-178">Review hello configuration</span></span>
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

<span data-ttu-id="2d6dd-179">完成此作業 hello Oracle 資料保護設定。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-179">This completed hello Oracle Data Guard setup.</span></span> <span data-ttu-id="2d6dd-180">hello 下一節說明您如何 tootest hello 連線並切換</span><span class="sxs-lookup"><span data-stu-id="2d6dd-180">hello next section shows you how tootest hello connectivity and switching over</span></span>

### <a name="connect-database-from-client-machine"></a><span data-ttu-id="2d6dd-181">從用戶端機器連線到資料庫</span><span class="sxs-lookup"><span data-stu-id="2d6dd-181">Connect database from client machine</span></span>

<span data-ttu-id="2d6dd-182">更新或建立 hello tnsnames.ora 檔案通常位於 $ORACLE_HOME\network\admin 用戶端電腦上。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-182">Update or create hello tnsnames.ora file on your client machine which usually is located at $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="2d6dd-183">取代具有 hello IP 您`publicIpAddress`myVM1 和 myVM2</span><span class="sxs-lookup"><span data-stu-id="2d6dd-183">Replace hello IP with your `publicIpAddress` for myVM1 and myVM2</span></span>

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

<span data-ttu-id="2d6dd-184">啟動 sqlplus</span><span class="sxs-lookup"><span data-stu-id="2d6dd-184">Start sqlplus</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-data-guard-configuration"></a><span data-ttu-id="2d6dd-185">測試 Data Guard 組態</span><span class="sxs-lookup"><span data-stu-id="2d6dd-185">Test Data Guard configuration</span></span>

### <a name="database-switchover-on-myvm1-primary"></a><span data-ttu-id="2d6dd-186">myVM1 (主要) 上的資料庫轉換</span><span class="sxs-lookup"><span data-stu-id="2d6dd-186">Database switchover on myVM1 (primary)</span></span>

<span data-ttu-id="2d6dd-187">從主要 toostandby (cdb1 toocdb1_stby) tooswitch</span><span class="sxs-lookup"><span data-stu-id="2d6dd-187">tooswitch from primary toostandby (cdb1 toocdb1_stby)</span></span>

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

<span data-ttu-id="2d6dd-188">您現在應該能夠 tooconnect toohello 待命資料庫</span><span class="sxs-lookup"><span data-stu-id="2d6dd-188">You should now be able tooconnect toohello standby database</span></span>

<span data-ttu-id="2d6dd-189">啟動 sqlplus</span><span class="sxs-lookup"><span data-stu-id="2d6dd-189">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="database-switch-back-on-myvm2-standby"></a><span data-ttu-id="2d6dd-190">myVM2 (待命) 上的資料庫反向切換</span><span class="sxs-lookup"><span data-stu-id="2d6dd-190">Database switch back on myVM2 (standby)</span></span>

<span data-ttu-id="2d6dd-191">上一步 tooswitch myVM2 上執行 hello 下列項目</span><span class="sxs-lookup"><span data-stu-id="2d6dd-191">tooswitch back, run hello followings on myVM2</span></span>
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

<span data-ttu-id="2d6dd-192">同樣地，您現在應該能夠 tooconnect toohello 主要資料庫</span><span class="sxs-lookup"><span data-stu-id="2d6dd-192">Once again, You should now be able tooconnect toohello primary database</span></span>

<span data-ttu-id="2d6dd-193">啟動 sqlplus</span><span class="sxs-lookup"><span data-stu-id="2d6dd-193">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="2d6dd-194">Hello 安裝和 Oracle linux 上的資料保護設定完成此作業。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-194">This completed hello installation and configuration of Data Guard on Oracle linux.</span></span>


## <a name="delete-virtual-machine"></a><span data-ttu-id="2d6dd-195">刪除虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2d6dd-195">Delete virtual machine</span></span>

<span data-ttu-id="2d6dd-196">不再需要時，下列命令的 hello 可以是使用的 tooremove hello 資源群組，VM，而且所有相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="2d6dd-196">When no longer needed, hello following command can be used tooremove hello Resource Group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="2d6dd-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2d6dd-197">Next steps</span></span>

[<span data-ttu-id="2d6dd-198">建立高可用性的虛擬機器教學課程</span><span class="sxs-lookup"><span data-stu-id="2d6dd-198">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="2d6dd-199">瀏覽 VM 部署 CLI 範例</span><span class="sxs-lookup"><span data-stu-id="2d6dd-199">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
