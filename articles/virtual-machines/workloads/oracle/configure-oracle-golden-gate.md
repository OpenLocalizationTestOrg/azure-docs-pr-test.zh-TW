---
title: "Azure Linux VM 上的 Oracle 金閘道 aaaImplement |Microsoft 文件"
description: "快速在您的 Azure 環境中啟動並執行 Oracle Golden Gate。"
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
ms.date: 05/19/2017
ms.author: rclaus
ms.openlocfilehash: 320cafd5d23ee472f0af9f92577bc6f432f65778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a><span data-ttu-id="411d8-103">在 Azure Linux VM 上實作 Oracle Golden Gate</span><span class="sxs-lookup"><span data-stu-id="411d8-103">Implement Oracle Golden Gate on an Azure Linux VM</span></span> 

<span data-ttu-id="411d8-104">hello Azure CLI 會使用的 toocreate 和管理 Azure 資源，從 hello 命令列或指令碼中。</span><span class="sxs-lookup"><span data-stu-id="411d8-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="411d8-105">本指南詳述，toouse hello Azure CLI toodeploy 的 Oracle 12c hello Azure Marketplace 的資源庫映像從資料庫的方式。</span><span class="sxs-lookup"><span data-stu-id="411d8-105">This guide details how toouse hello Azure CLI toodeploy an Oracle 12c database from hello Azure Marketplace gallery image.</span></span> 

<span data-ttu-id="411d8-106">本文件將按部就班示範如何 toocreate，安裝及設定 Azure VM 上的 Oracle 金閘道。</span><span class="sxs-lookup"><span data-stu-id="411d8-106">This document shows you step-by-step how toocreate, install, and configure Oracle Golden Gate on an Azure VM.</span></span>

<span data-ttu-id="411d8-107">開始之前，請確定已安裝 Azure CLI 該 hello。</span><span class="sxs-lookup"><span data-stu-id="411d8-107">Before you start, make sure that hello Azure CLI has been installed.</span></span> <span data-ttu-id="411d8-108">如需詳細資訊，請參閱 [Azure CLI 安裝指南](https://docs.microsoft.com/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="411d8-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="411d8-109">準備 hello 環境</span><span class="sxs-lookup"><span data-stu-id="411d8-109">Prepare hello environment</span></span>

<span data-ttu-id="411d8-110">tooperform hello Oracle 金閘道安裝，您需要 toocreate 兩個 Azure Vm 上 hello 相同可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="411d8-110">tooperform hello Oracle Golden Gate installation, you need toocreate two Azure VMs on hello same availability set.</span></span> <span data-ttu-id="411d8-111">hello Marketplace 映像使用 toocreate hello Vm 是**Oracle: Oracle-資料庫-Ee:12.1.0.2:latest**。</span><span class="sxs-lookup"><span data-stu-id="411d8-111">hello Marketplace image you use toocreate hello VMs is **Oracle:Oracle-Database-Ee:12.1.0.2:latest**.</span></span>

<span data-ttu-id="411d8-112">您也必須熟悉 Unix 編輯器 vi toobe 並且 x11 (X Windows) 的基本知識。</span><span class="sxs-lookup"><span data-stu-id="411d8-112">You also need toobe familiar with Unix editor vi and have a basic understanding of x11 (X Windows).</span></span>

<span data-ttu-id="411d8-113">hello 下面是 hello 環境設定的摘要：</span><span class="sxs-lookup"><span data-stu-id="411d8-113">hello following is a summary of hello environment configuration:</span></span>
> 
> |  | <span data-ttu-id="411d8-114">**主要網站**</span><span class="sxs-lookup"><span data-stu-id="411d8-114">**Primary site**</span></span> | <span data-ttu-id="411d8-115">**複寫網站**</span><span class="sxs-lookup"><span data-stu-id="411d8-115">**Replicate site**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="411d8-116">**Oracle 版本**</span><span class="sxs-lookup"><span data-stu-id="411d8-116">**Oracle release**</span></span> |<span data-ttu-id="411d8-117">Oracle 12c 版本 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="411d8-117">Oracle 12c Release 2 – (12.1.0.2)</span></span> |<span data-ttu-id="411d8-118">Oracle 12c 版本 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="411d8-118">Oracle 12c Release 2 – (12.1.0.2)</span></span>|
> | <span data-ttu-id="411d8-119">**機器名稱**</span><span class="sxs-lookup"><span data-stu-id="411d8-119">**Machine name**</span></span> |<span data-ttu-id="411d8-120">myVM1</span><span class="sxs-lookup"><span data-stu-id="411d8-120">myVM1</span></span> |<span data-ttu-id="411d8-121">myVM2</span><span class="sxs-lookup"><span data-stu-id="411d8-121">myVM2</span></span> |
> | <span data-ttu-id="411d8-122">**作業系統**</span><span class="sxs-lookup"><span data-stu-id="411d8-122">**Operating system**</span></span> |<span data-ttu-id="411d8-123">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="411d8-123">Oracle Linux 6.x</span></span> |<span data-ttu-id="411d8-124">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="411d8-124">Oracle Linux 6.x</span></span> |
> | <span data-ttu-id="411d8-125">**Oracle SID**</span><span class="sxs-lookup"><span data-stu-id="411d8-125">**Oracle SID**</span></span> |<span data-ttu-id="411d8-126">CDB1</span><span class="sxs-lookup"><span data-stu-id="411d8-126">CDB1</span></span> |<span data-ttu-id="411d8-127">CDB1</span><span class="sxs-lookup"><span data-stu-id="411d8-127">CDB1</span></span> |
> | <span data-ttu-id="411d8-128">**複寫結構描述**</span><span class="sxs-lookup"><span data-stu-id="411d8-128">**Replication schema**</span></span> |<span data-ttu-id="411d8-129">TEST</span><span class="sxs-lookup"><span data-stu-id="411d8-129">TEST</span></span>|<span data-ttu-id="411d8-130">TEST</span><span class="sxs-lookup"><span data-stu-id="411d8-130">TEST</span></span> |
> | <span data-ttu-id="411d8-131">**Golden Gate 擁有者/複寫**</span><span class="sxs-lookup"><span data-stu-id="411d8-131">**Golden Gate owner/replicate**</span></span> |<span data-ttu-id="411d8-132">C##GGADMIN</span><span class="sxs-lookup"><span data-stu-id="411d8-132">C##GGADMIN</span></span> |<span data-ttu-id="411d8-133">REPUSER</span><span class="sxs-lookup"><span data-stu-id="411d8-133">REPUSER</span></span> |
> | <span data-ttu-id="411d8-134">**Golden Gate 流程**</span><span class="sxs-lookup"><span data-stu-id="411d8-134">**Golden Gate process**</span></span> |<span data-ttu-id="411d8-135">EXTORA</span><span class="sxs-lookup"><span data-stu-id="411d8-135">EXTORA</span></span> |<span data-ttu-id="411d8-136">REPORA</span><span class="sxs-lookup"><span data-stu-id="411d8-136">REPORA</span></span>|


### <a name="sign-in-tooazure"></a><span data-ttu-id="411d8-137">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="411d8-137">Sign in tooAzure</span></span> 

<span data-ttu-id="411d8-138">登入 Azure 訂用帳戶以 hello tooyour [az 登入](/cli/azure/#login)命令。</span><span class="sxs-lookup"><span data-stu-id="411d8-138">Sign in tooyour Azure subscription with hello [az login](/cli/azure/#login) command.</span></span> <span data-ttu-id="411d8-139">然後依照 hello 螢幕上指示。</span><span class="sxs-lookup"><span data-stu-id="411d8-139">Then follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="411d8-140">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="411d8-140">Create a resource group</span></span>

<span data-ttu-id="411d8-141">建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="411d8-141">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="411d8-142">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="411d8-142">An Azure resource group is a logical container into which Azure resources are deployed and from which they can be managed.</span></span> 

<span data-ttu-id="411d8-143">hello 下列範例會建立名為的資源群組`myResourceGroup`在 hello`westus`位置。</span><span class="sxs-lookup"><span data-stu-id="411d8-143">hello following example creates a resource group named `myResourceGroup` in hello `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="411d8-144">建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="411d8-144">Create an availability set</span></span>

<span data-ttu-id="411d8-145">hello 遵循步驟是選擇性但建議使用。</span><span class="sxs-lookup"><span data-stu-id="411d8-145">hello following step is optional but recommended.</span></span> <span data-ttu-id="411d8-146">如需詳細資訊，請參閱 [Azure 可用性設定組指南](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines)。</span><span class="sxs-lookup"><span data-stu-id="411d8-146">For more information, see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="411d8-147">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="411d8-147">Create a virtual machine</span></span>

<span data-ttu-id="411d8-148">建立 VM 以 hello [az vm 建立](/cli/azure/vm#create)命令。</span><span class="sxs-lookup"><span data-stu-id="411d8-148">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="411d8-149">hello 下列範例會建立名為兩個 Vm`myVM1`和`myVM2`。</span><span class="sxs-lookup"><span data-stu-id="411d8-149">hello following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="411d8-150">如果預設的金鑰位置還沒有 SSH 金鑰，請建立這些金鑰。</span><span class="sxs-lookup"><span data-stu-id="411d8-150">Create SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="411d8-151">toouse 一組特定的金鑰，請使用 hello`--ssh-key-value`選項。</span><span class="sxs-lookup"><span data-stu-id="411d8-151">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

#### <a name="create-myvm1-primary"></a><span data-ttu-id="411d8-152">建立 myVM1 (主要)：</span><span class="sxs-lookup"><span data-stu-id="411d8-152">Create myVM1 (primary):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="411d8-153">在建立 VM 的 hello 之後, hello Azure CLI 會顯示下列範例的資訊類似 toohello。</span><span class="sxs-lookup"><span data-stu-id="411d8-153">After hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="411d8-154">(請注意 hello `publicIpAddress`。</span><span class="sxs-lookup"><span data-stu-id="411d8-154">(Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="411d8-155">此位址是使用的 tooaccess hello VM）。</span><span class="sxs-lookup"><span data-stu-id="411d8-155">This address is used tooaccess hello VM.)</span></span>

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

#### <a name="create-myvm2-replicate"></a><span data-ttu-id="411d8-156">建立 myVM2 (複寫)：</span><span class="sxs-lookup"><span data-stu-id="411d8-156">Create myVM2 (replicate):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="411d8-157">記下 hello`publicIpAddress`一併建立它之後。</span><span class="sxs-lookup"><span data-stu-id="411d8-157">Take note of hello `publicIpAddress` as well after it has been created.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="411d8-158">開啟 hello 連線的 TCP 連接埠</span><span class="sxs-lookup"><span data-stu-id="411d8-158">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="411d8-159">hello 下一個步驟是 tooconfigure 外部端點，可讓您 tooaccess hello Oracle 資料庫遠端。</span><span class="sxs-lookup"><span data-stu-id="411d8-159">hello next step is tooconfigure external endpoints,  which enable you tooaccess hello Oracle database remotely.</span></span> <span data-ttu-id="411d8-160">tooconfigure hello 外部端點，請執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="411d8-160">tooconfigure hello external endpoints, run hello following commands.</span></span>

#### <a name="open-hello-port-for-myvm1"></a><span data-ttu-id="411d8-161">開啟 myVM1 hello 連接埠：</span><span class="sxs-lookup"><span data-stu-id="411d8-161">Open hello port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="411d8-162">hello 結果看起來類似 toohello 下列回應：</span><span class="sxs-lookup"><span data-stu-id="411d8-162">hello results should look similar toohello following response:</span></span>

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

#### <a name="open-hello-port-for-myvm2"></a><span data-ttu-id="411d8-163">開啟 myVM2 hello 連接埠：</span><span class="sxs-lookup"><span data-stu-id="411d8-163">Open hello port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="411d8-164">Toohello 虛擬機器連線</span><span class="sxs-lookup"><span data-stu-id="411d8-164">Connect toohello virtual machine</span></span>

<span data-ttu-id="411d8-165">使用 hello 下列命令 toocreate 與 hello 虛擬機器的 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="411d8-165">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="411d8-166">Hello IP 位址取代成 hello`publicIpAddress`的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="411d8-166">Replace hello IP address with hello `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh <publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a><span data-ttu-id="411d8-167">建立 myVM1 hello 資料庫 （主要）</span><span class="sxs-lookup"><span data-stu-id="411d8-167">Create hello database on myVM1 (primary)</span></span>

<span data-ttu-id="411d8-168">hello Oracle 軟體上已安裝 hello Marketplace 映像，因此 hello 下一個步驟是 tooinstall hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="411d8-168">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> 

<span data-ttu-id="411d8-169">執行 hello 'oracle' superuser hello 軟體：</span><span class="sxs-lookup"><span data-stu-id="411d8-169">Run hello software as hello 'oracle' superuser:</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="411d8-170">建立 hello 資料庫：</span><span class="sxs-lookup"><span data-stu-id="411d8-170">Create hello database:</span></span>

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
<span data-ttu-id="411d8-171">輸出應該看起來類似 toohello 下列回應：</span><span class="sxs-lookup"><span data-stu-id="411d8-171">Outputs should look similar toohello following response:</span></span>

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
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

<span data-ttu-id="411d8-172">設定 hello ORACLE_SID 和 ORACLE_HOME 變數。</span><span class="sxs-lookup"><span data-stu-id="411d8-172">Set hello ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="411d8-173">（選擇性） 您可以加入 ORACLE_HOME 和 ORACLE_SID toohello.bashrc 檔案，以便這些設定會儲存為未來的登入：</span><span class="sxs-lookup"><span data-stu-id="411d8-173">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future sign-ins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="411d8-174">啟動 Oracle 接聽程式</span><span class="sxs-lookup"><span data-stu-id="411d8-174">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-hello-database-on-myvm2-replicate"></a><span data-ttu-id="411d8-175">建立 hello 資料庫上 myVM2 （複寫）</span><span class="sxs-lookup"><span data-stu-id="411d8-175">Create hello database on myVM2 (replicate)</span></span>

```bash
sudo su - oracle
```
<span data-ttu-id="411d8-176">建立 hello 資料庫：</span><span class="sxs-lookup"><span data-stu-id="411d8-176">Create hello database:</span></span>

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
<span data-ttu-id="411d8-177">設定 hello ORACLE_SID 和 ORACLE_HOME 變數。</span><span class="sxs-lookup"><span data-stu-id="411d8-177">Set hello ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="411d8-178">（選擇性） 您可以加入的 ORACLE_HOME 和 ORACLE_SID toohello.bashrc 的檔案，以便這些設定會儲存為未來的登入。</span><span class="sxs-lookup"><span data-stu-id="411d8-178">Optionally, you can added ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future sign-ins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="411d8-179">啟動 Oracle 接聽程式</span><span class="sxs-lookup"><span data-stu-id="411d8-179">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a><span data-ttu-id="411d8-180">設定 Golden Gate</span><span class="sxs-lookup"><span data-stu-id="411d8-180">Configure Golden Gate</span></span> 
<span data-ttu-id="411d8-181">tooconfigure 金閘道採取本節中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="411d8-181">tooconfigure Golden Gate, take hello steps in this section.</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="411d8-182">在 myVM1 (主要) 上啟用封存記錄模式</span><span class="sxs-lookup"><span data-stu-id="411d8-182">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="411d8-183">啟用強制記錄功能，並確定至少有一個記錄檔存在。</span><span class="sxs-lookup"><span data-stu-id="411d8-183">Enable force logging, and make sure at least one log file is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a><span data-ttu-id="411d8-184">下載 Golden Gate 軟體</span><span class="sxs-lookup"><span data-stu-id="411d8-184">Download Golden Gate software</span></span>
<span data-ttu-id="411d8-185">toodownload 並準備 hello Oracle 金閘道軟體，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="411d8-185">toodownload and prepare hello Oracle Golden Gate software, complete hello following steps:</span></span>

1. <span data-ttu-id="411d8-186">下載 hello **fbo_ggs_Linux_x64_shiphome.zip**檔案從 hello [Oracle 金閘道下載頁面](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html)。</span><span class="sxs-lookup"><span data-stu-id="411d8-186">Download hello **fbo_ggs_Linux_x64_shiphome.zip** file from hello [Oracle Golden Gate download page](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span></span> <span data-ttu-id="411d8-187">在 hello 下載標題**Oracle Linux x86-64 的 Oracle GoldenGate 12.x.x.x**，應該有一組的.zip 檔案 toodownload。</span><span class="sxs-lookup"><span data-stu-id="411d8-187">Under hello download title **Oracle GoldenGate 12.x.x.x for Oracle Linux x86-64**, there should be a set of .zip files toodownload.</span></span>

2. <span data-ttu-id="411d8-188">下載 hello.zip 檔案 tooyour 用戶端電腦之後，使用安全複製通訊協定 (SCP) toocopy hello 檔案 tooyour VM:</span><span class="sxs-lookup"><span data-stu-id="411d8-188">After you download hello .zip files tooyour client computer, use Secure Copy Protocol (SCP) toocopy hello files tooyour VM:</span></span>

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. <span data-ttu-id="411d8-189">移動 hello.zip 檔案 toohello **/opt**資料夾。</span><span class="sxs-lookup"><span data-stu-id="411d8-189">Move hello .zip files toohello **/opt** folder.</span></span> <span data-ttu-id="411d8-190">然後變更 hello hello 檔案擁有者，如下所示：</span><span class="sxs-lookup"><span data-stu-id="411d8-190">Then change hello owner of hello files as follows:</span></span>

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. <span data-ttu-id="411d8-191">解壓縮 hello 檔案 （安裝 hello Linux 如果尚未安裝解壓縮公用程式）：</span><span class="sxs-lookup"><span data-stu-id="411d8-191">Unzip hello files (install hello Linux unzip utility if it's not already installed):</span></span>

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. <span data-ttu-id="411d8-192">變更權限：</span><span class="sxs-lookup"><span data-stu-id="411d8-192">Change permission:</span></span>

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-hello-client-and-vm-toorun-x11-for-windows-clients-only"></a><span data-ttu-id="411d8-193">準備 hello 用戶端和 VM toorun x11 （適用於 Windows 的用戶端只）</span><span class="sxs-lookup"><span data-stu-id="411d8-193">Prepare hello client and VM toorun x11 (for Windows clients only)</span></span>
<span data-ttu-id="411d8-194">這是選擇性步驟。</span><span class="sxs-lookup"><span data-stu-id="411d8-194">This is an optional step.</span></span> <span data-ttu-id="411d8-195">如果您使用 Linux 用戶端或是已設定 x11，可以跳過此步驟。</span><span class="sxs-lookup"><span data-stu-id="411d8-195">You can skip this step if you are using a Linux client or already have x11 setup.</span></span>

1. <span data-ttu-id="411d8-196">下載 PuTTY 和 Xming tooyour Windows 電腦：</span><span class="sxs-lookup"><span data-stu-id="411d8-196">Download PuTTY and Xming tooyour Windows computer:</span></span>

  * [<span data-ttu-id="411d8-197">下載 PuTTY</span><span class="sxs-lookup"><span data-stu-id="411d8-197">Download PuTTY</span></span>](http://www.putty.org/)
  * [<span data-ttu-id="411d8-198">下載 Xming</span><span class="sxs-lookup"><span data-stu-id="411d8-198">Download Xming</span></span>](https://xming.en.softonic.com/)

2.  <span data-ttu-id="411d8-199">安裝 PuTTY 之後，在 hello PuTTY 資料夾 (例如，C:\Program Files\PuTTY) 中執行 puttygen.exe （PuTTY 金鑰產生器）。</span><span class="sxs-lookup"><span data-stu-id="411d8-199">After you install PuTTY, in hello PuTTY folder (for example, C:\Program Files\PuTTY), run puttygen.exe (PuTTY Key Generator).</span></span>

3.  <span data-ttu-id="411d8-200">在 PuTTY 金鑰產生器中︰</span><span class="sxs-lookup"><span data-stu-id="411d8-200">In PuTTY Key Generator:</span></span>

  - <span data-ttu-id="411d8-201">索引鍵，選取 hello toogenerate**產生** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="411d8-201">toogenerate a key, select hello **Generate** button.</span></span>
  - <span data-ttu-id="411d8-202">複製 hello hello 索引鍵內容 (**Ctrl + C**)。</span><span class="sxs-lookup"><span data-stu-id="411d8-202">Copy hello contents of hello key (**Ctrl+C**).</span></span>
  - <span data-ttu-id="411d8-203">選取 hello**儲存私密金鑰** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="411d8-203">Select hello **Save private key** button.</span></span>
  - <span data-ttu-id="411d8-204">忽略 hello 警告，隨即出現，然後選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="411d8-204">Ignore hello warning that appears, and then select **OK**.</span></span>

    ![Hello PuTTY 金鑰產生器頁面的螢幕擷取畫面](./media/oracle-golden-gate/puttykeygen.png)

4.  <span data-ttu-id="411d8-206">在您的 VM 中，執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="411d8-206">In your VM, run these commands:</span></span>

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. <span data-ttu-id="411d8-207">建立名為 **authorized_keys** 的檔案。</span><span class="sxs-lookup"><span data-stu-id="411d8-207">Create a file named **authorized_keys**.</span></span> <span data-ttu-id="411d8-208">Hello hello 金鑰內容貼在檔案中，然後將檔案儲存 hello。</span><span class="sxs-lookup"><span data-stu-id="411d8-208">Paste hello contents of hello key in this file, and then save hello file.</span></span>

  > [!NOTE]
  > <span data-ttu-id="411d8-209">hello 金鑰必須包含字串 hello `ssh-rsa`。</span><span class="sxs-lookup"><span data-stu-id="411d8-209">hello key must contain hello string `ssh-rsa`.</span></span> <span data-ttu-id="411d8-210">此外，hello hello 索引鍵內容必須是單行文字。</span><span class="sxs-lookup"><span data-stu-id="411d8-210">Also, hello contents of hello key must be a single line of text.</span></span>
  >  

6. <span data-ttu-id="411d8-211">啟動 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="411d8-211">Start PuTTY.</span></span> <span data-ttu-id="411d8-212">在 hello**類別**窗格中，選取**連接** > **SSH** > **Auth**。在 hello**私密金鑰檔案驗證**方塊中，瀏覽您先前產生的 toohello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="411d8-212">In hello **Category** pane, select **Connection** > **SSH** > **Auth**. In hello **Private key file for authentication** box, browse toohello key that you generated earlier.</span></span>

  ![Hello 設定私密金鑰 頁面上的螢幕擷取畫面](./media/oracle-golden-gate/setprivatekey.png)

7. <span data-ttu-id="411d8-214">在 hello**類別**窗格中，選取**連接** > **SSH** > **X11**。</span><span class="sxs-lookup"><span data-stu-id="411d8-214">In hello **Category** pane, select **Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="411d8-215">然後選取 hello**啟用 X11 轉寄**方塊。</span><span class="sxs-lookup"><span data-stu-id="411d8-215">Then select hello **Enable X11 forwarding** box.</span></span>

  ![Hello 啟用 X11 頁面的螢幕擷取畫面](./media/oracle-golden-gate/enablex11.png)

8. <span data-ttu-id="411d8-217">在 [hello**類別**] 窗格中，跳過**工作階段**。</span><span class="sxs-lookup"><span data-stu-id="411d8-217">In hello **Category** pane, go too**Session**.</span></span> <span data-ttu-id="411d8-218">輸入 hello 主機資訊，然後選取**開啟**。</span><span class="sxs-lookup"><span data-stu-id="411d8-218">Enter hello host information, and then select **Open**.</span></span>

  ![Hello 工作階段頁面的螢幕擷取畫面](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a><span data-ttu-id="411d8-220">安裝 Golden Gate 軟體</span><span class="sxs-lookup"><span data-stu-id="411d8-220">Install Golden Gate software</span></span>

<span data-ttu-id="411d8-221">tooinstall Oracle 金閘道，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="411d8-221">tooinstall Oracle Golden Gate, complete hello following steps:</span></span>

1. <span data-ttu-id="411d8-222">以 oracle 的身分登入。</span><span class="sxs-lookup"><span data-stu-id="411d8-222">Sign in as oracle.</span></span> <span data-ttu-id="411d8-223">（您應該能夠 toosign 中的，而不會提示輸入密碼）。請確定 Xming 執行之前開始 hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="411d8-223">(You should be able toosign in without being prompted for a password.) Make sure that Xming is running before you begin hello installation.</span></span>
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. <span data-ttu-id="411d8-224">選取 'Oracle GoldenGate for Oracle Database 12c'。</span><span class="sxs-lookup"><span data-stu-id="411d8-224">Select 'Oracle GoldenGate for Oracle Database 12c'.</span></span> <span data-ttu-id="411d8-225">然後選取**下一步**toocontinue。</span><span class="sxs-lookup"><span data-stu-id="411d8-225">Then select **Next** toocontinue.</span></span>

  ![Hello 安裝程式選取 [安裝] 頁面的螢幕擷取畫面](./media/oracle-golden-gate/golden_gate_install_01.png)

3. <span data-ttu-id="411d8-227">變更 hello 軟體位置。</span><span class="sxs-lookup"><span data-stu-id="411d8-227">Change hello software location.</span></span> <span data-ttu-id="411d8-228">然後選取 hello**啟動管理員**方塊，然後輸入 hello 資料庫位置。</span><span class="sxs-lookup"><span data-stu-id="411d8-228">Then select  hello **Start Manager** box and enter hello database location.</span></span> <span data-ttu-id="411d8-229">選取**下一步**toocontinue。</span><span class="sxs-lookup"><span data-stu-id="411d8-229">Select **Next** toocontinue.</span></span>

  ![Hello 選取 [安裝] 頁面上的螢幕擷取畫面](./media/oracle-golden-gate/golden_gate_install_02.png)

4. <span data-ttu-id="411d8-231">變更 hello 清查目錄，然後選取 **下一步**toocontinue。</span><span class="sxs-lookup"><span data-stu-id="411d8-231">Change hello inventory directory, and then select **Next** toocontinue.</span></span>

  ![Hello 選取 [安裝] 頁面上的螢幕擷取畫面](./media/oracle-golden-gate/golden_gate_install_03.png)

5. <span data-ttu-id="411d8-233">在 hello**摘要**畫面上，選取**安裝**toocontinue。</span><span class="sxs-lookup"><span data-stu-id="411d8-233">On hello **Summary** screen, select **Install** toocontinue.</span></span>

  ![Hello 安裝程式選取 [安裝] 頁面的螢幕擷取畫面](./media/oracle-golden-gate/golden_gate_install_04.png)

6. <span data-ttu-id="411d8-235">您可能會提示的 toorun 指令碼 'root' 身分。</span><span class="sxs-lookup"><span data-stu-id="411d8-235">You might be prompted toorun a script as 'root'.</span></span> <span data-ttu-id="411d8-236">如果是，開啟個別的工作階段，ssh toohello sudo tooroot 的 VM，然後再執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="411d8-236">If so, open a separate session, ssh toohello VM, sudo tooroot, and then run hello script.</span></span> <span data-ttu-id="411d8-237">選取 [確定] 以繼續操作。</span><span class="sxs-lookup"><span data-stu-id="411d8-237">Select **OK** continue.</span></span>

  ![Hello 選取 [安裝] 頁面上的螢幕擷取畫面](./media/oracle-golden-gate/golden_gate_install_05.png)

7. <span data-ttu-id="411d8-239">Hello 安裝完成時，選取**關閉**toocomplete hello 程序。</span><span class="sxs-lookup"><span data-stu-id="411d8-239">When hello installation has finished, select **Close** toocomplete hello process.</span></span>

  ![Hello 選取 [安裝] 頁面上的螢幕擷取畫面](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="411d8-241">設定 myVM1 (主要) 上的服務</span><span class="sxs-lookup"><span data-stu-id="411d8-241">Set up service on myVM1 (primary)</span></span>

1. <span data-ttu-id="411d8-242">建立或更新 hello tnsnames.ora 檔案：</span><span class="sxs-lookup"><span data-stu-id="411d8-242">Create or update hello tnsnames.ora file:</span></span>

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. <span data-ttu-id="411d8-243">建立 hello 金閘道擁有者和使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="411d8-243">Create hello Golden Gate owner and user accounts.</span></span>

  > [!NOTE]
  > <span data-ttu-id="411d8-244">hello 擁有者的帳戶必須具有 C# # 前置詞。</span><span class="sxs-lookup"><span data-stu-id="411d8-244">hello owner account must have C## prefix.</span></span>
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA tooC##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. <span data-ttu-id="411d8-245">建立 hello 金閘道測試使用者帳戶：</span><span class="sxs-lookup"><span data-stu-id="411d8-245">Create hello Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. <span data-ttu-id="411d8-246">設定 hello 擷取參數檔案。</span><span class="sxs-lookup"><span data-stu-id="411d8-246">Configure hello extract parameter file.</span></span>

 <span data-ttu-id="411d8-247">啟動 hello 黃金閘道命令列介面 (ggsci):</span><span class="sxs-lookup"><span data-stu-id="411d8-247">Start hello Golden gate command-line interface (ggsci):</span></span>

  ```bash
  $ sudo su - oracle
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> DBLOGIN USERID test@pdb1, PASSWORD test
  Successfully logged into database  pdb1
  GGSCI>  ADD SCHEMATRANDATA pdb1.test
  2017-05-23 15:44:25  INFO    OGG-01788  SCHEMATRANDATA has been added on schema test.
  2017-05-23 15:44:25  INFO    OGG-01976  SCHEMATRANDATA for scheduling columns has been added on schema test.

  GGSCI> EDIT PARAMS EXTORA
  ```
5. <span data-ttu-id="411d8-248">新增 hello 遵循 toohello 擷取參數檔案 （透過使用 vi 命令）。</span><span class="sxs-lookup"><span data-stu-id="411d8-248">Add hello following toohello EXTRACT parameter file (by using vi commands).</span></span> <span data-ttu-id="411d8-249">按下 Esc 鍵，':wq!'</span><span class="sxs-lookup"><span data-stu-id="411d8-249">Press Esc key, ':wq!'</span></span> <span data-ttu-id="411d8-250">toosave 檔案。</span><span class="sxs-lookup"><span data-stu-id="411d8-250">toosave file.</span></span> 

  ```bash
  EXTRACT EXTORA
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTRAIL ./dirdat/rt  
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT 
  LOGALLSUPCOLS
  UPDATERECORDFORMAT COMPACT
  TABLE pdb1.test.TCUSTMER;
  TABLE pdb1.test.TCUSTORD;
  ```
6. <span data-ttu-id="411d8-251">註冊 extract--integrated 擷取：</span><span class="sxs-lookup"><span data-stu-id="411d8-251">Register extract--integrated extract:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. <span data-ttu-id="411d8-252">設定擷取檢查點，並啟動即時擷取：</span><span class="sxs-lookup"><span data-stu-id="411d8-252">Set up extract checkpoints and start real-time extract:</span></span>

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request tooMANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
<span data-ttu-id="411d8-253">在此步驟中，您會看到啟動 SCN，將更新版本中，使用不同的區段中的 hello:</span><span class="sxs-lookup"><span data-stu-id="411d8-253">In this step, you find hello starting SCN, which will be used later, in a different section:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> SELECT current_scn from v$database;
  CURRENT_SCN
  -----------
      1857887
  SQL> EXIT;
  ```

  ```bash
  $ ./ggsci
  GGSCI> EDIT PARAMS INITEXT
  ```

  ```bash
  EXTRACT INITEXT
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTASK REPLICAT, GROUP INITREP
  TABLE pdb1.test.*, SQLPREDICATE 'AS OF SCN 1857887'; 
  ```

  ```bash
  GGSCI> ADD EXTRACT INITEXT, SOURCEISTABLE
  ```

### <a name="set-up-service-on-myvm2-replicate"></a><span data-ttu-id="411d8-254">設定 myVM2 (複寫) 上的服務</span><span class="sxs-lookup"><span data-stu-id="411d8-254">Set up service on myVM2 (replicate)</span></span>


1. <span data-ttu-id="411d8-255">建立或更新 hello tnsnames.ora 檔案：</span><span class="sxs-lookup"><span data-stu-id="411d8-255">Create or update hello tnsnames.ora file:</span></span>

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. <span data-ttu-id="411d8-256">建立複寫帳戶：</span><span class="sxs-lookup"><span data-stu-id="411d8-256">Create a replicate account:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba toorepuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. <span data-ttu-id="411d8-257">建立 Golden Gate 測試使用者帳戶：</span><span class="sxs-lookup"><span data-stu-id="411d8-257">Create a Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. <span data-ttu-id="411d8-258">REPLICAT 參數檔案 tooreplicate 變更：</span><span class="sxs-lookup"><span data-stu-id="411d8-258">REPLICAT parameter file tooreplicate changes:</span></span> 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  <span data-ttu-id="411d8-259">REPORA 參數檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="411d8-259">Content of REPORA parameter file:</span></span>

  ```bash
  REPLICAT REPORA
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/repora.dsc, PURGE, MEGABYTES 100
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT
  DBOPTIONS INTEGRATEDPARAMS(parallelism 6)
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;
  ```

5. <span data-ttu-id="411d8-260">設定複寫檢查點：</span><span class="sxs-lookup"><span data-stu-id="411d8-260">Set up a replicat checkpoint:</span></span>

  ```bash
  GGSCI> ADD REPLICAT REPORA, INTEGRATED, EXTTRAIL ./dirdat/rt
  GGSCI> EDIT PARAMS INITREP

  ```

  ```bash
  REPLICAT INITREP
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/tcustmer.dsc, APPEND
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;   
  ```

  ```bash
  GGSCI> ADD REPLICAT INITREP, SPECIALRUN
  ```

### <a name="set-up-hello-replication-myvm1-and-myvm2"></a><span data-ttu-id="411d8-261">設定 hello 複寫 （myVM1 和 myVM2）</span><span class="sxs-lookup"><span data-stu-id="411d8-261">Set up hello replication (myVM1 and myVM2)</span></span>

#### <a name="1-set-up-hello-replication-on-myvm2-replicate"></a><span data-ttu-id="411d8-262">1.設定上 myVM2 hello 複寫 （複寫）</span><span class="sxs-lookup"><span data-stu-id="411d8-262">1. Set up hello replication on myVM2 (replicate)</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
<span data-ttu-id="411d8-263">更新 hello 下列 hello 檔案：</span><span class="sxs-lookup"><span data-stu-id="411d8-263">Update hello file with hello following:</span></span>

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
<span data-ttu-id="411d8-264">然後重新啟動 hello 管理員服務：</span><span class="sxs-lookup"><span data-stu-id="411d8-264">Then restart hello Manager service:</span></span>

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-hello-replication-on-myvm1-primary"></a><span data-ttu-id="411d8-265">2.設定上 myVM1 hello 複寫 （主要）</span><span class="sxs-lookup"><span data-stu-id="411d8-265">2. Set up hello replication on myVM1 (primary)</span></span>

<span data-ttu-id="411d8-266">啟動 hello 初始載入和檢查發生錯誤：</span><span class="sxs-lookup"><span data-stu-id="411d8-266">Start hello initial load and check for errors:</span></span>

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-hello-replication-on-myvm2-replicate"></a><span data-ttu-id="411d8-267">3.設定上 myVM2 hello 複寫 （複寫）</span><span class="sxs-lookup"><span data-stu-id="411d8-267">3. Set up hello replication on myVM2 (replicate)</span></span>

<span data-ttu-id="411d8-268">變更您之前取得的 hello SCN 編號與 hello 數目：</span><span class="sxs-lookup"><span data-stu-id="411d8-268">Change hello SCN number with hello number you obtained before:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
<span data-ttu-id="411d8-269">hello 複寫已經開始，而且您可以插入新記錄 tooTEST 資料表來測試。</span><span class="sxs-lookup"><span data-stu-id="411d8-269">hello replication has begun, and you can test it by inserting new records tooTEST tables.</span></span>


### <a name="view-job-status-and-troubleshooting"></a><span data-ttu-id="411d8-270">檢視作業狀態和疑難排解</span><span class="sxs-lookup"><span data-stu-id="411d8-270">View job status and troubleshooting</span></span>

#### <a name="view-reports"></a><span data-ttu-id="411d8-271">檢視報告</span><span class="sxs-lookup"><span data-stu-id="411d8-271">View reports</span></span>
<span data-ttu-id="411d8-272">tooview 報告 myVM1，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="411d8-272">tooview reports on myVM1, run hello following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
<span data-ttu-id="411d8-273">tooview 報告 myVM2，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="411d8-273">tooview reports on myVM2, run hello following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a><span data-ttu-id="411d8-274">檢視狀態和記錄</span><span class="sxs-lookup"><span data-stu-id="411d8-274">View status and history</span></span>
<span data-ttu-id="411d8-275">tooview 狀態和歷程記錄上 myVM1，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="411d8-275">tooview status and history on myVM1, run hello following commands:</span></span>

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

<span data-ttu-id="411d8-276">tooview 狀態和歷程記錄上 myVM2，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="411d8-276">tooview status and history on myVM2, run hello following commands:</span></span>

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
<span data-ttu-id="411d8-277">如此即完成 hello 安裝和 Oracle linux 上金閘道的設定。</span><span class="sxs-lookup"><span data-stu-id="411d8-277">This completes hello installation and configuration of Golden Gate on Oracle linux.</span></span>


## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="411d8-278">刪除 hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="411d8-278">Delete hello virtual machine</span></span>

<span data-ttu-id="411d8-279">當不再需要時，下列命令的 hello 可以使用的 tooremove hello 資源群組、 VM 和所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="411d8-279">When it's no longer needed, hello following command can be used tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="411d8-280">後續步驟</span><span class="sxs-lookup"><span data-stu-id="411d8-280">Next steps</span></span>

[<span data-ttu-id="411d8-281">建立高可用性的虛擬機器教學課程</span><span class="sxs-lookup"><span data-stu-id="411d8-281">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="411d8-282">瀏覽 VM 部署 CLI 範例</span><span class="sxs-lookup"><span data-stu-id="411d8-282">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
