---
title: "在 Azure Linux VM 上實作 Oracle Golden Gate | Microsoft Docs"
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
ms.openlocfilehash: a05711357d345267647c02e42336fd37c09e1bff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a><span data-ttu-id="956ed-103">在 Azure Linux VM 上實作 Oracle Golden Gate</span><span class="sxs-lookup"><span data-stu-id="956ed-103">Implement Oracle Golden Gate on an Azure Linux VM</span></span> 

<span data-ttu-id="956ed-104">Azure CLI 可用來從命令列或在指令碼中建立和管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="956ed-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="956ed-105">本指南詳述如何使用 Azure CLI 從 Azure Marketplace 資源庫映像部署 Oracle 12c 資料庫。</span><span class="sxs-lookup"><span data-stu-id="956ed-105">This guide details how to use the Azure CLI to deploy an Oracle 12c database from the Azure Marketplace gallery image.</span></span> 

<span data-ttu-id="956ed-106">這份文件逐步示範如何在 Azure VM 上建立、安裝及設定 Oracle Golden Gate。</span><span class="sxs-lookup"><span data-stu-id="956ed-106">This document shows you step-by-step how to create, install, and configure Oracle Golden Gate on an Azure VM.</span></span>

<span data-ttu-id="956ed-107">開始之前，請確定已安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="956ed-107">Before you start, make sure that the Azure CLI has been installed.</span></span> <span data-ttu-id="956ed-108">如需詳細資訊，請參閱 [Azure CLI 安裝指南](https://docs.microsoft.com/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="956ed-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="956ed-109">準備環境</span><span class="sxs-lookup"><span data-stu-id="956ed-109">Prepare the environment</span></span>

<span data-ttu-id="956ed-110">若要執行 Oracle Golden Gate 的安裝，您需要在相同的可用性設定組建立兩個 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="956ed-110">To perform the Oracle Golden Gate installation, you need to create two Azure VMs on the same availability set.</span></span> <span data-ttu-id="956ed-111">您用來建立 VM 的 Marketplace 映像是 **Oracle:Oracle-Database-Ee:12.1.0.2:latest**。</span><span class="sxs-lookup"><span data-stu-id="956ed-111">The Marketplace image you use to create the VMs is **Oracle:Oracle-Database-Ee:12.1.0.2:latest**.</span></span>

<span data-ttu-id="956ed-112">您也需要熟悉 Unix 編輯器 vi，並且對 x11 (X Windows) 有基本了解。</span><span class="sxs-lookup"><span data-stu-id="956ed-112">You also need to be familiar with Unix editor vi and have a basic understanding of x11 (X Windows).</span></span>

<span data-ttu-id="956ed-113">環境設定的摘要如下：</span><span class="sxs-lookup"><span data-stu-id="956ed-113">The following is a summary of the environment configuration:</span></span>
> 
> |  | <span data-ttu-id="956ed-114">**主要網站**</span><span class="sxs-lookup"><span data-stu-id="956ed-114">**Primary site**</span></span> | <span data-ttu-id="956ed-115">**複寫網站**</span><span class="sxs-lookup"><span data-stu-id="956ed-115">**Replicate site**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="956ed-116">**Oracle 版本**</span><span class="sxs-lookup"><span data-stu-id="956ed-116">**Oracle release**</span></span> |<span data-ttu-id="956ed-117">Oracle 12c 版本 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="956ed-117">Oracle 12c Release 2 – (12.1.0.2)</span></span> |<span data-ttu-id="956ed-118">Oracle 12c 版本 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="956ed-118">Oracle 12c Release 2 – (12.1.0.2)</span></span>|
> | <span data-ttu-id="956ed-119">**機器名稱**</span><span class="sxs-lookup"><span data-stu-id="956ed-119">**Machine name**</span></span> |<span data-ttu-id="956ed-120">myVM1</span><span class="sxs-lookup"><span data-stu-id="956ed-120">myVM1</span></span> |<span data-ttu-id="956ed-121">myVM2</span><span class="sxs-lookup"><span data-stu-id="956ed-121">myVM2</span></span> |
> | <span data-ttu-id="956ed-122">**作業系統**</span><span class="sxs-lookup"><span data-stu-id="956ed-122">**Operating system**</span></span> |<span data-ttu-id="956ed-123">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="956ed-123">Oracle Linux 6.x</span></span> |<span data-ttu-id="956ed-124">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="956ed-124">Oracle Linux 6.x</span></span> |
> | <span data-ttu-id="956ed-125">**Oracle SID**</span><span class="sxs-lookup"><span data-stu-id="956ed-125">**Oracle SID**</span></span> |<span data-ttu-id="956ed-126">CDB1</span><span class="sxs-lookup"><span data-stu-id="956ed-126">CDB1</span></span> |<span data-ttu-id="956ed-127">CDB1</span><span class="sxs-lookup"><span data-stu-id="956ed-127">CDB1</span></span> |
> | <span data-ttu-id="956ed-128">**複寫結構描述**</span><span class="sxs-lookup"><span data-stu-id="956ed-128">**Replication schema**</span></span> |<span data-ttu-id="956ed-129">TEST</span><span class="sxs-lookup"><span data-stu-id="956ed-129">TEST</span></span>|<span data-ttu-id="956ed-130">TEST</span><span class="sxs-lookup"><span data-stu-id="956ed-130">TEST</span></span> |
> | <span data-ttu-id="956ed-131">**Golden Gate 擁有者/複寫**</span><span class="sxs-lookup"><span data-stu-id="956ed-131">**Golden Gate owner/replicate**</span></span> |<span data-ttu-id="956ed-132">C##GGADMIN</span><span class="sxs-lookup"><span data-stu-id="956ed-132">C##GGADMIN</span></span> |<span data-ttu-id="956ed-133">REPUSER</span><span class="sxs-lookup"><span data-stu-id="956ed-133">REPUSER</span></span> |
> | <span data-ttu-id="956ed-134">**Golden Gate 流程**</span><span class="sxs-lookup"><span data-stu-id="956ed-134">**Golden Gate process**</span></span> |<span data-ttu-id="956ed-135">EXTORA</span><span class="sxs-lookup"><span data-stu-id="956ed-135">EXTORA</span></span> |<span data-ttu-id="956ed-136">REPORA</span><span class="sxs-lookup"><span data-stu-id="956ed-136">REPORA</span></span>|


### <a name="sign-in-to-azure"></a><span data-ttu-id="956ed-137">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="956ed-137">Sign in to Azure</span></span> 

<span data-ttu-id="956ed-138">使用 [az login](/cli/azure/#login) 命令登入您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="956ed-138">Sign in to your Azure subscription with the [az login](/cli/azure/#login) command.</span></span> <span data-ttu-id="956ed-139">然後，遵循螢幕上的指示來進行。</span><span class="sxs-lookup"><span data-stu-id="956ed-139">Then follow the on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="956ed-140">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="956ed-140">Create a resource group</span></span>

<span data-ttu-id="956ed-141">使用 [az group create](/cli/azure/group#create) 命令來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="956ed-141">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="956ed-142">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="956ed-142">An Azure resource group is a logical container into which Azure resources are deployed and from which they can be managed.</span></span> 

<span data-ttu-id="956ed-143">下列範例會在 `westus` 位置建立名為 `myResourceGroup` 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="956ed-143">The following example creates a resource group named `myResourceGroup` in the `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="956ed-144">建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="956ed-144">Create an availability set</span></span>

<span data-ttu-id="956ed-145">下列步驟為選用步驟，但建議執行。</span><span class="sxs-lookup"><span data-stu-id="956ed-145">The following step is optional but recommended.</span></span> <span data-ttu-id="956ed-146">如需詳細資訊，請參閱 [Azure 可用性設定組指南](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines)。</span><span class="sxs-lookup"><span data-stu-id="956ed-146">For more information, see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="956ed-147">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="956ed-147">Create a virtual machine</span></span>

<span data-ttu-id="956ed-148">使用 [az vm create](/cli/azure/vm#create) 命令來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="956ed-148">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="956ed-149">下列範例會建立兩個 VM，名為 `myVM1` 和 `myVM2`。</span><span class="sxs-lookup"><span data-stu-id="956ed-149">The following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="956ed-150">如果預設的金鑰位置還沒有 SSH 金鑰，請建立這些金鑰。</span><span class="sxs-lookup"><span data-stu-id="956ed-150">Create SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="956ed-151">若要使用一組特定金鑰，請使用 `--ssh-key-value` 選項。</span><span class="sxs-lookup"><span data-stu-id="956ed-151">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>

#### <a name="create-myvm1-primary"></a><span data-ttu-id="956ed-152">建立 myVM1 (主要)：</span><span class="sxs-lookup"><span data-stu-id="956ed-152">Create myVM1 (primary):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="956ed-153">建立 VM 後，Azure CLI 會顯示類似下列範例的資訊。</span><span class="sxs-lookup"><span data-stu-id="956ed-153">After the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="956ed-154">(記下 `publicIpAddress`。</span><span class="sxs-lookup"><span data-stu-id="956ed-154">(Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="956ed-155">此位址用來存取 VM。)</span><span class="sxs-lookup"><span data-stu-id="956ed-155">This address is used to access the VM.)</span></span>

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

#### <a name="create-myvm2-replicate"></a><span data-ttu-id="956ed-156">建立 myVM2 (複寫)：</span><span class="sxs-lookup"><span data-stu-id="956ed-156">Create myVM2 (replicate):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="956ed-157">在建立之後一樣記下 `publicIpAddress`。</span><span class="sxs-lookup"><span data-stu-id="956ed-157">Take note of the `publicIpAddress` as well after it has been created.</span></span>

### <a name="open-the-tcp-port-for-connectivity"></a><span data-ttu-id="956ed-158">開啟用於連線的 TCP 通訊埠</span><span class="sxs-lookup"><span data-stu-id="956ed-158">Open the TCP port for connectivity</span></span>

<span data-ttu-id="956ed-159">下一個步驟是設定外部端點，可讓您從遠端存取 Oracle 資料庫。</span><span class="sxs-lookup"><span data-stu-id="956ed-159">The next step is to configure external endpoints,  which enable you to access the Oracle database remotely.</span></span> <span data-ttu-id="956ed-160">若要設定外部端點，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="956ed-160">To configure the external endpoints, run the following commands.</span></span>

#### <a name="open-the-port-for-myvm1"></a><span data-ttu-id="956ed-161">開啟 myVM1 的連接埠：</span><span class="sxs-lookup"><span data-stu-id="956ed-161">Open the port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="956ed-162">結果看起來應該會像下面的回應這樣：</span><span class="sxs-lookup"><span data-stu-id="956ed-162">The results should look similar to the following response:</span></span>

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

#### <a name="open-the-port-for-myvm2"></a><span data-ttu-id="956ed-163">開啟 myVM2 的連接埠：</span><span class="sxs-lookup"><span data-stu-id="956ed-163">Open the port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="956ed-164">連接至虛擬機器</span><span class="sxs-lookup"><span data-stu-id="956ed-164">Connect to the virtual machine</span></span>

<span data-ttu-id="956ed-165">使用下列命令，建立與虛擬機器的 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="956ed-165">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="956ed-166">以虛擬機器的 `publicIpAddress` 取代 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="956ed-166">Replace the IP address with the `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh <publicIpAddress>
```

### <a name="create-the-database-on-myvm1-primary"></a><span data-ttu-id="956ed-167">在 myVM1 (主要) 上建立資料庫</span><span class="sxs-lookup"><span data-stu-id="956ed-167">Create the database on myVM1 (primary)</span></span>

<span data-ttu-id="956ed-168">Oracle 軟體已安裝於 Marketplace 映像上，因此下一個步驟是安裝資料庫。</span><span class="sxs-lookup"><span data-stu-id="956ed-168">The Oracle software is already installed on the Marketplace image, so the next step is to install the database.</span></span> 

<span data-ttu-id="956ed-169">以 'oracle' 超級使用者的身分執行軟體：</span><span class="sxs-lookup"><span data-stu-id="956ed-169">Run the software as the 'oracle' superuser:</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="956ed-170">建立資料庫︰</span><span class="sxs-lookup"><span data-stu-id="956ed-170">Create the database:</span></span>

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
<span data-ttu-id="956ed-171">輸出結果看起來應該會像下面的回應這樣：</span><span class="sxs-lookup"><span data-stu-id="956ed-171">Outputs should look similar to the following response:</span></span>

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
Look at the log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

<span data-ttu-id="956ed-172">設定 ORACLE_SID 和 ORACLE_HOME 變數。</span><span class="sxs-lookup"><span data-stu-id="956ed-172">Set the ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="956ed-173">您可以視需要將 ORACLE_HOME 和 ORACLE_SID 新增到 .bashrc 檔案中，如此可將這些設定儲存，以供日後登入使用：</span><span class="sxs-lookup"><span data-stu-id="956ed-173">Optionally, you can add ORACLE_HOME and ORACLE_SID to the .bashrc file, so that these settings are saved for future sign-ins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="956ed-174">啟動 Oracle 接聽程式</span><span class="sxs-lookup"><span data-stu-id="956ed-174">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-the-database-on-myvm2-replicate"></a><span data-ttu-id="956ed-175">在 myVM2 (複寫) 上建立資料庫</span><span class="sxs-lookup"><span data-stu-id="956ed-175">Create the database on myVM2 (replicate)</span></span>

```bash
sudo su - oracle
```
<span data-ttu-id="956ed-176">建立資料庫︰</span><span class="sxs-lookup"><span data-stu-id="956ed-176">Create the database:</span></span>

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
<span data-ttu-id="956ed-177">設定 ORACLE_SID 和 ORACLE_HOME 變數。</span><span class="sxs-lookup"><span data-stu-id="956ed-177">Set the ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="956ed-178">您可以視需要將 ORACLE_HOME 和 ORACLE_SID 新增到 .bashrc 檔案中，如此可將這些設定儲存，以供日後登入使用。</span><span class="sxs-lookup"><span data-stu-id="956ed-178">Optionally, you can added ORACLE_HOME and ORACLE_SID to the .bashrc file, so that these settings are saved for future sign-ins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="956ed-179">啟動 Oracle 接聽程式</span><span class="sxs-lookup"><span data-stu-id="956ed-179">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a><span data-ttu-id="956ed-180">設定 Golden Gate</span><span class="sxs-lookup"><span data-stu-id="956ed-180">Configure Golden Gate</span></span> 
<span data-ttu-id="956ed-181">若要設定 Golden Gate，請採取本節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="956ed-181">To configure Golden Gate, take the steps in this section.</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="956ed-182">在 myVM1 (主要) 上啟用封存記錄模式</span><span class="sxs-lookup"><span data-stu-id="956ed-182">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="956ed-183">啟用強制記錄功能，並確定至少有一個記錄檔存在。</span><span class="sxs-lookup"><span data-stu-id="956ed-183">Enable force logging, and make sure at least one log file is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a><span data-ttu-id="956ed-184">下載 Golden Gate 軟體</span><span class="sxs-lookup"><span data-stu-id="956ed-184">Download Golden Gate software</span></span>
<span data-ttu-id="956ed-185">若要下載並準備 Oracle Golden Gate 軟體，請完成下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="956ed-185">To download and prepare the Oracle Golden Gate software, complete the following steps:</span></span>

1. <span data-ttu-id="956ed-186">從 [Oracle Golden Gate 下載分頁](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html)下載 **fbo_ggs_Linux_x64_shiphome.zip** 檔案。</span><span class="sxs-lookup"><span data-stu-id="956ed-186">Download the **fbo_ggs_Linux_x64_shiphome.zip** file from the [Oracle Golden Gate download page](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span></span> <span data-ttu-id="956ed-187">在下載標題 **Oracle GoldenGate 12.x.x.x for Oracle Linux x86-64** 底下，應該有一組 .zip 檔可以下載。</span><span class="sxs-lookup"><span data-stu-id="956ed-187">Under the download title **Oracle GoldenGate 12.x.x.x for Oracle Linux x86-64**, there should be a set of .zip files to download.</span></span>

2. <span data-ttu-id="956ed-188">將 .zip 檔下載到用戶端電腦之後，請使用「安全複製通訊協定 (SCP)」將這些檔案複製到 VM：</span><span class="sxs-lookup"><span data-stu-id="956ed-188">After you download the .zip files to your client computer, use Secure Copy Protocol (SCP) to copy the files to your VM:</span></span>

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. <span data-ttu-id="956ed-189">將 .zip 檔移到 **/opt** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="956ed-189">Move the .zip files to the **/opt** folder.</span></span> <span data-ttu-id="956ed-190">接著，變更檔案的擁有者，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="956ed-190">Then change the owner of the files as follows:</span></span>

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. <span data-ttu-id="956ed-191">將檔案解壓縮 (如果您尚未安裝 Linux 解壓縮公用程式，請加以安裝)︰</span><span class="sxs-lookup"><span data-stu-id="956ed-191">Unzip the files (install the Linux unzip utility if it's not already installed):</span></span>

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. <span data-ttu-id="956ed-192">變更權限：</span><span class="sxs-lookup"><span data-stu-id="956ed-192">Change permission:</span></span>

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-the-client-and-vm-to-run-x11-for-windows-clients-only"></a><span data-ttu-id="956ed-193">讓用戶端和 VM 準備好執行 x11 (僅適用於 Windows 用戶端)</span><span class="sxs-lookup"><span data-stu-id="956ed-193">Prepare the client and VM to run x11 (for Windows clients only)</span></span>
<span data-ttu-id="956ed-194">這是選擇性步驟。</span><span class="sxs-lookup"><span data-stu-id="956ed-194">This is an optional step.</span></span> <span data-ttu-id="956ed-195">如果您使用 Linux 用戶端或是已設定 x11，可以跳過此步驟。</span><span class="sxs-lookup"><span data-stu-id="956ed-195">You can skip this step if you are using a Linux client or already have x11 setup.</span></span>

1. <span data-ttu-id="956ed-196">將 PuTTY 和 Xming 下載到 Windows 電腦︰</span><span class="sxs-lookup"><span data-stu-id="956ed-196">Download PuTTY and Xming to your Windows computer:</span></span>

  * [<span data-ttu-id="956ed-197">下載 PuTTY</span><span class="sxs-lookup"><span data-stu-id="956ed-197">Download PuTTY</span></span>](http://www.putty.org/)
  * [<span data-ttu-id="956ed-198">下載 Xming</span><span class="sxs-lookup"><span data-stu-id="956ed-198">Download Xming</span></span>](https://xming.en.softonic.com/)

2.  <span data-ttu-id="956ed-199">在 PuTTY 安裝好之後，請在 PuTTY 資料夾 (例如 C:\Program Files\PuTTY) 執行 puttygen.exe (PuTTY 金鑰產生器)。</span><span class="sxs-lookup"><span data-stu-id="956ed-199">After you install PuTTY, in the PuTTY folder (for example, C:\Program Files\PuTTY), run puttygen.exe (PuTTY Key Generator).</span></span>

3.  <span data-ttu-id="956ed-200">在 PuTTY 金鑰產生器中︰</span><span class="sxs-lookup"><span data-stu-id="956ed-200">In PuTTY Key Generator:</span></span>

  - <span data-ttu-id="956ed-201">若要產生金鑰，請選取 [產生] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="956ed-201">To generate a key, select the **Generate** button.</span></span>
  - <span data-ttu-id="956ed-202">複製金鑰的內容 (**Ctrl+C**)。</span><span class="sxs-lookup"><span data-stu-id="956ed-202">Copy the contents of the key (**Ctrl+C**).</span></span>
  - <span data-ttu-id="956ed-203">選取 [儲存私密金鑰] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="956ed-203">Select the **Save private key** button.</span></span>
  - <span data-ttu-id="956ed-204">略過隨之出現的警告，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="956ed-204">Ignore the warning that appears, and then select **OK**.</span></span>

    ![PuTTY 金鑰產生器頁面的螢幕擷取畫面](./media/oracle-golden-gate/puttykeygen.png)

4.  <span data-ttu-id="956ed-206">在您的 VM 中，執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="956ed-206">In your VM, run these commands:</span></span>

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. <span data-ttu-id="956ed-207">建立名為 **authorized_keys** 的檔案。</span><span class="sxs-lookup"><span data-stu-id="956ed-207">Create a file named **authorized_keys**.</span></span> <span data-ttu-id="956ed-208">在此檔案中貼上金鑰的內容，然後儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="956ed-208">Paste the contents of the key in this file, and then save the file.</span></span>

  > [!NOTE]
  > <span data-ttu-id="956ed-209">金鑰中必須包含字串 `ssh-rsa`。</span><span class="sxs-lookup"><span data-stu-id="956ed-209">The key must contain the string `ssh-rsa`.</span></span> <span data-ttu-id="956ed-210">此外，金鑰的內容必須是單行文字。</span><span class="sxs-lookup"><span data-stu-id="956ed-210">Also, the contents of the key must be a single line of text.</span></span>
  >  

6. <span data-ttu-id="956ed-211">啟動 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="956ed-211">Start PuTTY.</span></span> <span data-ttu-id="956ed-212">在 [類別] 窗格中，選取 [連線] > [SSH] > [驗證]。</span><span class="sxs-lookup"><span data-stu-id="956ed-212">In the **Category** pane, select **Connection** > **SSH** > **Auth**.</span></span> <span data-ttu-id="956ed-213">在 [用於驗證的私密金鑰檔] 方塊中，瀏覽至您稍早產生的金鑰。</span><span class="sxs-lookup"><span data-stu-id="956ed-213">In the **Private key file for authentication** box, browse to the key that you generated earlier.</span></span>

  ![[設定私密金鑰] 頁面上的螢幕擷取畫面](./media/oracle-golden-gate/setprivatekey.png)

7. <span data-ttu-id="956ed-215">在 [類別] 窗格中，選取 [連線] > [SSH] > [X11]。</span><span class="sxs-lookup"><span data-stu-id="956ed-215">In the **Category** pane, select **Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="956ed-216">然後選取 [啟用 X11 轉送] 方塊。</span><span class="sxs-lookup"><span data-stu-id="956ed-216">Then select the **Enable X11 forwarding** box.</span></span>

  ![[啟用 X11] 頁面的螢幕擷取畫面](./media/oracle-golden-gate/enablex11.png)

8. <span data-ttu-id="956ed-218">在 [類別] 窗格中，移至 [工作階段]。</span><span class="sxs-lookup"><span data-stu-id="956ed-218">In the **Category** pane, go to **Session**.</span></span> <span data-ttu-id="956ed-219">輸入主機資訊，然後選取 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="956ed-219">Enter the host information, and then select **Open**.</span></span>

  ![工作階段分頁的螢幕擷取畫面](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a><span data-ttu-id="956ed-221">安裝 Golden Gate 軟體</span><span class="sxs-lookup"><span data-stu-id="956ed-221">Install Golden Gate software</span></span>

<span data-ttu-id="956ed-222">若要安裝 Oracle Golden Gate，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="956ed-222">To install Oracle Golden Gate, complete the following steps:</span></span>

1. <span data-ttu-id="956ed-223">以 oracle 的身分登入。</span><span class="sxs-lookup"><span data-stu-id="956ed-223">Sign in as oracle.</span></span> <span data-ttu-id="956ed-224">(您應該能夠順利登入，而不會收到需要輸入密碼的提示)。請確定 Xming 已在執行，然後才開始安裝。</span><span class="sxs-lookup"><span data-stu-id="956ed-224">(You should be able to sign in without being prompted for a password.) Make sure that Xming is running before you begin the installation.</span></span>
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. <span data-ttu-id="956ed-225">選取 'Oracle GoldenGate for Oracle Database 12c'。</span><span class="sxs-lookup"><span data-stu-id="956ed-225">Select 'Oracle GoldenGate for Oracle Database 12c'.</span></span> <span data-ttu-id="956ed-226">然後選取 [下一步] 以繼續操作。</span><span class="sxs-lookup"><span data-stu-id="956ed-226">Then select **Next** to continue.</span></span>

  ![安裝程式之 [選取安裝] 分頁的螢幕擷取畫面](./media/oracle-golden-gate/golden_gate_install_01.png)

3. <span data-ttu-id="956ed-228">變更軟體位置。</span><span class="sxs-lookup"><span data-stu-id="956ed-228">Change the software location.</span></span> <span data-ttu-id="956ed-229">然後選取 [啟動管理員] 方塊並輸入資料庫位置。</span><span class="sxs-lookup"><span data-stu-id="956ed-229">Then select  the **Start Manager** box and enter the database location.</span></span> <span data-ttu-id="956ed-230">選取 [下一步] 以繼續操作。</span><span class="sxs-lookup"><span data-stu-id="956ed-230">Select **Next** to continue.</span></span>

  ![[選取安裝] 分頁的螢幕擷取畫面](./media/oracle-golden-gate/golden_gate_install_02.png)

4. <span data-ttu-id="956ed-232">變更清查目錄，然後選取 [下一步] 以繼續操作。</span><span class="sxs-lookup"><span data-stu-id="956ed-232">Change the inventory directory, and then select **Next** to continue.</span></span>

  ![[選取安裝] 分頁的螢幕擷取畫面](./media/oracle-golden-gate/golden_gate_install_03.png)

5. <span data-ttu-id="956ed-234">在 [摘要] 畫面上，選取 [安裝] 以繼續操作。</span><span class="sxs-lookup"><span data-stu-id="956ed-234">On the **Summary** screen, select **Install** to continue.</span></span>

  ![安裝程式之 [選取安裝] 分頁的螢幕擷取畫面](./media/oracle-golden-gate/golden_gate_install_04.png)

6. <span data-ttu-id="956ed-236">系統可能會提示您以 'root' 的身分執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="956ed-236">You might be prompted to run a script as 'root'.</span></span> <span data-ttu-id="956ed-237">如果是這樣，請開啟不同的工作階段，ssh 為 VM、sudo 為 root，然後執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="956ed-237">If so, open a separate session, ssh to the VM, sudo to root, and then run the script.</span></span> <span data-ttu-id="956ed-238">選取 [確定] 以繼續操作。</span><span class="sxs-lookup"><span data-stu-id="956ed-238">Select **OK** continue.</span></span>

  ![[選取安裝] 分頁的螢幕擷取畫面](./media/oracle-golden-gate/golden_gate_install_05.png)

7. <span data-ttu-id="956ed-240">當安裝完成時，選取 [關閉] 以完成流程。</span><span class="sxs-lookup"><span data-stu-id="956ed-240">When the installation has finished, select **Close** to complete the process.</span></span>

  ![[選取安裝] 分頁的螢幕擷取畫面](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="956ed-242">設定 myVM1 (主要) 上的服務</span><span class="sxs-lookup"><span data-stu-id="956ed-242">Set up service on myVM1 (primary)</span></span>

1. <span data-ttu-id="956ed-243">建立或更新 tnsnames.ora 檔案：</span><span class="sxs-lookup"><span data-stu-id="956ed-243">Create or update the tnsnames.ora file:</span></span>

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

2. <span data-ttu-id="956ed-244">建立 Golden Gate 擁有者和使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="956ed-244">Create the Golden Gate owner and user accounts.</span></span>

  > [!NOTE]
  > <span data-ttu-id="956ed-245">擁有者帳戶必須有 C## 前置詞。</span><span class="sxs-lookup"><span data-stu-id="956ed-245">The owner account must have C## prefix.</span></span>
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA to C##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. <span data-ttu-id="956ed-246">建立 Golden Gate 測試使用者帳戶：</span><span class="sxs-lookup"><span data-stu-id="956ed-246">Create the Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba TO test;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. <span data-ttu-id="956ed-247">設定擷取參數檔案。</span><span class="sxs-lookup"><span data-stu-id="956ed-247">Configure the extract parameter file.</span></span>

 <span data-ttu-id="956ed-248">啟動 Golden Gate 命令列介面 (ggsci)：</span><span class="sxs-lookup"><span data-stu-id="956ed-248">Start the Golden gate command-line interface (ggsci):</span></span>

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
5. <span data-ttu-id="956ed-249">將下列項目新增至 EXTRACT 參數檔案 (使用 vi 命令)。</span><span class="sxs-lookup"><span data-stu-id="956ed-249">Add the following to the EXTRACT parameter file (by using vi commands).</span></span> <span data-ttu-id="956ed-250">按下 Esc 鍵，':wq!'</span><span class="sxs-lookup"><span data-stu-id="956ed-250">Press Esc key, ':wq!'</span></span> <span data-ttu-id="956ed-251">以儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="956ed-251">to save file.</span></span> 

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
6. <span data-ttu-id="956ed-252">註冊 extract--integrated 擷取：</span><span class="sxs-lookup"><span data-stu-id="956ed-252">Register extract--integrated extract:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. <span data-ttu-id="956ed-253">設定擷取檢查點，並啟動即時擷取：</span><span class="sxs-lookup"><span data-stu-id="956ed-253">Set up extract checkpoints and start real-time extract:</span></span>

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request to MANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
<span data-ttu-id="956ed-254">在此步驟中，您會找到開始 SCN，將會在稍後於不同區段中使用：</span><span class="sxs-lookup"><span data-stu-id="956ed-254">In this step, you find the starting SCN, which will be used later, in a different section:</span></span>

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

### <a name="set-up-service-on-myvm2-replicate"></a><span data-ttu-id="956ed-255">設定 myVM2 (複寫) 上的服務</span><span class="sxs-lookup"><span data-stu-id="956ed-255">Set up service on myVM2 (replicate)</span></span>


1. <span data-ttu-id="956ed-256">建立或更新 tnsnames.ora 檔案：</span><span class="sxs-lookup"><span data-stu-id="956ed-256">Create or update the tnsnames.ora file:</span></span>

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

2. <span data-ttu-id="956ed-257">建立複寫帳戶：</span><span class="sxs-lookup"><span data-stu-id="956ed-257">Create a replicate account:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba to repuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. <span data-ttu-id="956ed-258">建立 Golden Gate 測試使用者帳戶：</span><span class="sxs-lookup"><span data-stu-id="956ed-258">Create a Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba TO test;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. <span data-ttu-id="956ed-259">REPLICAT 參數檔案以複寫變更：</span><span class="sxs-lookup"><span data-stu-id="956ed-259">REPLICAT parameter file to replicate changes:</span></span> 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  <span data-ttu-id="956ed-260">REPORA 參數檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="956ed-260">Content of REPORA parameter file:</span></span>

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

5. <span data-ttu-id="956ed-261">設定複寫檢查點：</span><span class="sxs-lookup"><span data-stu-id="956ed-261">Set up a replicat checkpoint:</span></span>

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

### <a name="set-up-the-replication-myvm1-and-myvm2"></a><span data-ttu-id="956ed-262">設定複寫 (myVM1 和 myVM2)</span><span class="sxs-lookup"><span data-stu-id="956ed-262">Set up the replication (myVM1 and myVM2)</span></span>

#### <a name="1-set-up-the-replication-on-myvm2-replicate"></a><span data-ttu-id="956ed-263">1.設定 myVM2 (複寫) 上的複寫</span><span class="sxs-lookup"><span data-stu-id="956ed-263">1. Set up the replication on myVM2 (replicate)</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
<span data-ttu-id="956ed-264">使用下列內容更新檔案：</span><span class="sxs-lookup"><span data-stu-id="956ed-264">Update the file with the following:</span></span>

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
<span data-ttu-id="956ed-265">然後重新啟動管理員服務：</span><span class="sxs-lookup"><span data-stu-id="956ed-265">Then restart the Manager service:</span></span>

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-the-replication-on-myvm1-primary"></a><span data-ttu-id="956ed-266">2.設定 myVM1 (主要) 上的複寫</span><span class="sxs-lookup"><span data-stu-id="956ed-266">2. Set up the replication on myVM1 (primary)</span></span>

<span data-ttu-id="956ed-267">啟動初始載入並且檢查錯誤：</span><span class="sxs-lookup"><span data-stu-id="956ed-267">Start the initial load and check for errors:</span></span>

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-the-replication-on-myvm2-replicate"></a><span data-ttu-id="956ed-268">3.設定 myVM2 (複寫) 上的複寫</span><span class="sxs-lookup"><span data-stu-id="956ed-268">3. Set up the replication on myVM2 (replicate)</span></span>

<span data-ttu-id="956ed-269">使用您之前取得的數字變更 SCN 編號：</span><span class="sxs-lookup"><span data-stu-id="956ed-269">Change the SCN number with the number you obtained before:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
<span data-ttu-id="956ed-270">複寫已開始進行，您可以將新記錄插入測試資料表，以進行測試。</span><span class="sxs-lookup"><span data-stu-id="956ed-270">The replication has begun, and you can test it by inserting new records to TEST tables.</span></span>


### <a name="view-job-status-and-troubleshooting"></a><span data-ttu-id="956ed-271">檢視作業狀態和疑難排解</span><span class="sxs-lookup"><span data-stu-id="956ed-271">View job status and troubleshooting</span></span>

#### <a name="view-reports"></a><span data-ttu-id="956ed-272">檢視報告</span><span class="sxs-lookup"><span data-stu-id="956ed-272">View reports</span></span>
<span data-ttu-id="956ed-273">若要檢視 myVM1 上的報告，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="956ed-273">To view reports on myVM1, run the following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
<span data-ttu-id="956ed-274">若要檢視 myVM2 上的報告，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="956ed-274">To view reports on myVM2, run the following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a><span data-ttu-id="956ed-275">檢視狀態和記錄</span><span class="sxs-lookup"><span data-stu-id="956ed-275">View status and history</span></span>
<span data-ttu-id="956ed-276">若要檢視 myVM1 上的狀態和記錄，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="956ed-276">To view status and history on myVM1, run the following commands:</span></span>

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

<span data-ttu-id="956ed-277">若要檢視 myVM2 上的狀態和記錄，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="956ed-277">To view status and history on myVM2, run the following commands:</span></span>

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
<span data-ttu-id="956ed-278">這樣便已完成 Oracle Linux 上的 Golden Gate 安裝和設定。</span><span class="sxs-lookup"><span data-stu-id="956ed-278">This completes the installation and configuration of Golden Gate on Oracle linux.</span></span>


## <a name="delete-the-virtual-machine"></a><span data-ttu-id="956ed-279">刪除虛擬機器</span><span class="sxs-lookup"><span data-stu-id="956ed-279">Delete the virtual machine</span></span>

<span data-ttu-id="956ed-280">若不再需要，您可以使用下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="956ed-280">When it's no longer needed, the following command can be used to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="956ed-281">後續步驟</span><span class="sxs-lookup"><span data-stu-id="956ed-281">Next steps</span></span>

[<span data-ttu-id="956ed-282">建立高可用性的虛擬機器教學課程</span><span class="sxs-lookup"><span data-stu-id="956ed-282">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="956ed-283">瀏覽 VM 部署 CLI 範例</span><span class="sxs-lookup"><span data-stu-id="956ed-283">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
