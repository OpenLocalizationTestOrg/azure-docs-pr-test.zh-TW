---
title: "Azure Linux 虛擬機器上的設定 Oracle ASM aaaSet |Microsoft 文件"
description: "快速在您的 Azure 環境中啟動並執行 Oracle ASM。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/19/2017
ms.author: rclaus
ms.openlocfilehash: d6a7046638e919876477d46943faabcb1872acac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="1c64e-103">在 Azure Linux 虛擬機器上設定 Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="1c64e-103">Set up Oracle ASM on an Azure Linux virtual machine</span></span>  

<span data-ttu-id="1c64e-104">Azure 虛擬機器提供完全可設定且彈性的計算環境。</span><span class="sxs-lookup"><span data-stu-id="1c64e-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="1c64e-105">本教學課程涵蓋結合 hello 安裝和設定的 Oracle 自動儲存體管理 (ASM) 的基本 Azure 虛擬機器部署。</span><span class="sxs-lookup"><span data-stu-id="1c64e-105">This tutorial covers basic Azure virtual machine deployment combined with hello installation and configuration of Oracle Automated Storage Management (ASM).</span></span>  <span data-ttu-id="1c64e-106">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="1c64e-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1c64e-107">建立和連線 tooan Oracle 資料庫的 VM</span><span class="sxs-lookup"><span data-stu-id="1c64e-107">Create and connect tooan Oracle Database VM</span></span>
> * <span data-ttu-id="1c64e-108">安裝和設定 Oracle 自動儲存體管理</span><span class="sxs-lookup"><span data-stu-id="1c64e-108">Install and configure Oracle Automated Storage Management</span></span>
> * <span data-ttu-id="1c64e-109">安裝和設定 Oracle Grid Infrastructure</span><span class="sxs-lookup"><span data-stu-id="1c64e-109">Install and configure Oracle Grid infrastructure</span></span>
> * <span data-ttu-id="1c64e-110">初始化 Oracle ASM 安裝</span><span class="sxs-lookup"><span data-stu-id="1c64e-110">Initialize an Oracle ASM installation</span></span>
> * <span data-ttu-id="1c64e-111">建立受 ASM 管理的 Oracle DB</span><span class="sxs-lookup"><span data-stu-id="1c64e-111">Create an Oracle DB managed by ASM</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1c64e-112">如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="1c64e-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="1c64e-113">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="1c64e-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1c64e-114">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="1c64e-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-hello-environment"></a><span data-ttu-id="1c64e-115">準備 hello 環境</span><span class="sxs-lookup"><span data-stu-id="1c64e-115">Prepare hello environment</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="1c64e-116">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="1c64e-116">Create a resource group</span></span>

<span data-ttu-id="1c64e-117">toocreate 資源群組、 使用 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="1c64e-117">toocreate a resource group, use hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="1c64e-118">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="1c64e-118">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> <span data-ttu-id="1c64e-119">在此範例中，資源群組命名為*myResourceGroup*在 hello *eastus*區域。</span><span class="sxs-lookup"><span data-stu-id="1c64e-119">In this example, a resource group named *myResourceGroup* in hello *eastus* region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a><span data-ttu-id="1c64e-120">建立 VM</span><span class="sxs-lookup"><span data-stu-id="1c64e-120">Create a VM</span></span>

<span data-ttu-id="1c64e-121">toocreate 虛擬機器根據 hello Oracle Database 映像和設定它 toouse Oracle ASM，請使用 hello [az vm 建立](/cli/azure/vm#create)命令。</span><span class="sxs-lookup"><span data-stu-id="1c64e-121">toocreate a virtual machine based on hello Oracle Database image and configure it toouse Oracle ASM, use hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="1c64e-122">hello 下列範例會建立名為 myVM Standard_DS2_v2 大小的 50 GB 的四個連接的資料磁碟的 VM。</span><span class="sxs-lookup"><span data-stu-id="1c64e-122">hello following example creates a VM named myVM that is a Standard_DS2_v2 size with four attached data disks of 50 GB each.</span></span> <span data-ttu-id="1c64e-123">如果它們尚不存在 hello 預設索引鍵位置中，它也會建立 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="1c64e-123">If they do not already exist in hello default key location, it also creates SSH keys.</span></span>  <span data-ttu-id="1c64e-124">toouse 一組特定的金鑰，請使用 hello`--ssh-key-value`選項。</span><span class="sxs-lookup"><span data-stu-id="1c64e-124">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

<span data-ttu-id="1c64e-125">建立 hello VM 之後，Azure CLI 顯示資訊的類似 toohello 下列範例。</span><span class="sxs-lookup"><span data-stu-id="1c64e-125">After you create hello VM, Azure CLI displays information similar toohello following example.</span></span> <span data-ttu-id="1c64e-126">請注意 hello 值`publicIpAddress`。</span><span class="sxs-lookup"><span data-stu-id="1c64e-126">Note hello value for `publicIpAddress`.</span></span> <span data-ttu-id="1c64e-127">您使用此位址 tooaccess hello VM。</span><span class="sxs-lookup"><span data-stu-id="1c64e-127">You use this address tooaccess hello VM.</span></span>

   ```azurecli
   {
     "fqdns": "",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
     "location": "eastus",
     "macAddress": "00-0D-3A-36-2F-56",
     "powerState": "VM running",
     "privateIpAddress": "10.0.0.4",
     "publicIpAddress": "13.64.104.241",
     "resourceGroup": "myResourceGroup"
   }
   ```

### <a name="connect-toohello-vm"></a><span data-ttu-id="1c64e-128">連接 toohello VM</span><span class="sxs-lookup"><span data-stu-id="1c64e-128">Connect toohello VM</span></span>

<span data-ttu-id="1c64e-129">SSH 工作階段與 toocreate hello VM 並設定其他設定，請使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="1c64e-129">toocreate an SSH session with hello VM and configure additional settings, use hello following command.</span></span> <span data-ttu-id="1c64e-130">Hello IP 位址取代成 hello `publicIpAddress` VM 的值。</span><span class="sxs-lookup"><span data-stu-id="1c64e-130">Replace hello IP address with hello `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a><span data-ttu-id="1c64e-131">安裝 Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="1c64e-131">Install Oracle ASM</span></span>

<span data-ttu-id="1c64e-132">tooinstall Oracle ASM，完成下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="1c64e-132">tooinstall Oracle ASM, complete hello following steps.</span></span> 

<span data-ttu-id="1c64e-133">如需關於安裝 Oracle ASM 的詳細資訊，請參閱 [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html)。</span><span class="sxs-lookup"><span data-stu-id="1c64e-133">For more information about installing Oracle ASM, see [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span></span>  

1. <span data-ttu-id="1c64e-134">您為根順序 toocontinue ASM 安裝中需要 toologin:</span><span class="sxs-lookup"><span data-stu-id="1c64e-134">You need toologin as root in order toocontinue with ASM installation:</span></span>

   ```bash
   sudo su -
   ```
   
2. <span data-ttu-id="1c64e-135">執行這些額外的命令 tooinstall Oracle ASM 元件：</span><span class="sxs-lookup"><span data-stu-id="1c64e-135">Run these additional commands tooinstall Oracle ASM components:</span></span>

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. <span data-ttu-id="1c64e-136">確認您已安裝 Oracle ASM：</span><span class="sxs-lookup"><span data-stu-id="1c64e-136">Verify that Oracle ASM is installed:</span></span>

   ```bash
   rpm -qa |grep oracleasm
   ```

    <span data-ttu-id="1c64e-137">hello 這個命令的輸出應該會列出 hello 下列元件：</span><span class="sxs-lookup"><span data-stu-id="1c64e-137">hello output of this command should list hello following components:</span></span>

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. <span data-ttu-id="1c64e-138">ASM 正確需要順序 toofunction 中特定的使用者與角色。</span><span class="sxs-lookup"><span data-stu-id="1c64e-138">ASM requires specific users and roles in order toofunction correctly.</span></span> <span data-ttu-id="1c64e-139">下列命令的 hello 建立 hello 先決條件的使用者帳戶和群組：</span><span class="sxs-lookup"><span data-stu-id="1c64e-139">hello following commands create hello pre-requisite user accounts and groups:</span></span> 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. <span data-ttu-id="1c64e-140">確認已正確建立使用者和群組：</span><span class="sxs-lookup"><span data-stu-id="1c64e-140">Verify users and groups were created correctly:</span></span>

   ```bash
   id grid
   ```

    <span data-ttu-id="1c64e-141">hello 這個命令的輸出應該會列出 hello 下列使用者和群組：</span><span class="sxs-lookup"><span data-stu-id="1c64e-141">hello output of this command should list hello following users and groups:</span></span>

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. <span data-ttu-id="1c64e-142">為使用者建立的資料夾*方格*和 hello 擁有者變更為：</span><span class="sxs-lookup"><span data-stu-id="1c64e-142">Create a folder for user *grid* and change hello owner:</span></span>

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a><span data-ttu-id="1c64e-143">設定 Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="1c64e-143">Set up Oracle ASM</span></span>

<span data-ttu-id="1c64e-144">此教學課程，hello 預設使用者是*方格*hello 預設群組，且*asmadmin*。</span><span class="sxs-lookup"><span data-stu-id="1c64e-144">For this tutorial, hello default user is *grid* and hello default group is *asmadmin*.</span></span> <span data-ttu-id="1c64e-145">請確定該 hello *oracle*使用者是 hello asmadmin 群組的一部分。</span><span class="sxs-lookup"><span data-stu-id="1c64e-145">Ensure that hello *oracle* user is part of hello asmadmin group.</span></span> <span data-ttu-id="1c64e-146">註冊您的 Oracle ASM 安裝，完成下列步驟的 hello tooset:</span><span class="sxs-lookup"><span data-stu-id="1c64e-146">tooset up your Oracle ASM installation, complete hello following steps:</span></span>

1. <span data-ttu-id="1c64e-147">設定 hello Oracle ASM 程式庫的驅動程式以及在開機設定 hello 磁碟機 toostart 包含定義 hello 預設使用者 （方格） 和預設群組 (asmadmin) （選擇 y） 和 tooscan 在開機磁碟 （選擇 y）。</span><span class="sxs-lookup"><span data-stu-id="1c64e-147">Setting up hello Oracle ASM library driver involves defining hello default user (grid) and default group (asmadmin) as well as configuring hello drive toostart on boot (choose y) and tooscan for disks on boot (choose y).</span></span> <span data-ttu-id="1c64e-148">您需要 tooanswer hello 提示 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="1c64e-148">You need tooanswer hello prompts from hello following command:</span></span>

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   <span data-ttu-id="1c64e-149">此命令的 hello 輸出應該看起來類似 toohello 遵循、 停止與提示 toobe 回答。</span><span class="sxs-lookup"><span data-stu-id="1c64e-149">hello output of this command should look similar toohello following, stopping with prompts toobe answered.</span></span>

    ```bash
   Configuring hello Oracle ASM library driver.

   This will configure hello on-boot properties of hello Oracle ASM library
   driver. hello following questions will determine whether hello driver is
   loaded on boot and what permissions it will have. hello current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user tooown hello driver interface []: grid
   Default group tooown hello driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. <span data-ttu-id="1c64e-150">檢視 hello 磁碟組態：</span><span class="sxs-lookup"><span data-stu-id="1c64e-150">View hello disk configuration:</span></span>
   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="1c64e-151">hello 這個命令的輸出應該看起來類似下列的可用磁碟清單的 toohello</span><span class="sxs-lookup"><span data-stu-id="1c64e-151">hello output of this command should look similar toohello following listing of available disks</span></span>

   ```bash
   8       16   14680064 sdb
   8       17   14678976 sdb1
   8        0   52428800 sda
   8        1     512000 sda1
   8        2   51915776 sda2
   8       48   52428800 sdd
   8       64   52428800 sde
   8       80   52428800 sdf
   8       32   52428800 sdc
   11       0       1152 sr0
   ```

3. <span data-ttu-id="1c64e-152">格式化磁片*/開發/sdc*執行 hello 下列命令，以及回答 hello 提示與：</span><span class="sxs-lookup"><span data-stu-id="1c64e-152">Format disk */dev/sdc* by running hello following command and answering hello prompts with:</span></span>
   - <span data-ttu-id="1c64e-153">n 為新磁碟分割</span><span class="sxs-lookup"><span data-stu-id="1c64e-153">*n* for new partition</span></span>
   - <span data-ttu-id="1c64e-154">*p* 為主要磁碟分割</span><span class="sxs-lookup"><span data-stu-id="1c64e-154">*p* for primary partition</span></span>
   - <span data-ttu-id="1c64e-155">*1* tooselect hello 第一個資料分割</span><span class="sxs-lookup"><span data-stu-id="1c64e-155">*1* tooselect hello first partition</span></span>
   - <span data-ttu-id="1c64e-156">按下`enter`hello 第一個磁柱的</span><span class="sxs-lookup"><span data-stu-id="1c64e-156">press `enter` for hello default first cylinder</span></span>
   - <span data-ttu-id="1c64e-157">按下`enter`hello 最後磁柱的</span><span class="sxs-lookup"><span data-stu-id="1c64e-157">press `enter` for hello default last cylinder</span></span>
   - <span data-ttu-id="1c64e-158">按下*w* toowrite hello 變更 toohello 磁碟分割表格</span><span class="sxs-lookup"><span data-stu-id="1c64e-158">press *w* toowrite hello changes toohello partition table</span></span>  

   ```bash
   fdisk /dev/sdc
   ```
   
   <span data-ttu-id="1c64e-159">使用以上所提供的 hello 答案，hello hello fdisk 命令的輸出應該看起來像 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="1c64e-159">Using hello answers provided above, hello output for hello fdisk command should look like hello following:</span></span>

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide toowrite them.
   After that, of course, hello previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   hello device presents a logical sector size that is smaller than
   hello physical sector size. Aligning tooa physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off hello mode (command 'c') and change display units to
           sectors (command 'u').

   Command (m for help): n
   Command action
     e   extended
     p   primary partition (1-4)
   p
   Partition number (1-4): 1
   First cylinder (1-6527, default 1):
   Using default value 1
   Last cylinder, +cylinders or +size{K,M,G} (1-6527, default 6527):
   Using default value 6527

   Command (m for help): w
   hello partition table has been altered!

   Calling ioctl() toore-read partition table.
   Syncing disks.
   ```

4. <span data-ttu-id="1c64e-160">重複前面 fdisk 命令的 hello `/dev/sdd`， `/dev/sde`，和`/dev/sdf`。</span><span class="sxs-lookup"><span data-stu-id="1c64e-160">Repeat hello preceding fdisk command for `/dev/sdd`, `/dev/sde`, and `/dev/sdf`.</span></span>

5. <span data-ttu-id="1c64e-161">請檢查 hello 磁碟組態：</span><span class="sxs-lookup"><span data-stu-id="1c64e-161">Check hello disk configuration:</span></span>

   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="1c64e-162">hello hello 命令輸出看起來應該類似下列 hello:</span><span class="sxs-lookup"><span data-stu-id="1c64e-162">hello output of hello command should look like hello following:</span></span>

   ```bash
   major minor  #blocks  name

     8       16   14680064 sdb
     8       17   14678976 sdb1
     8       32   52428800 sdc
     8       33   52428096 sdc1
     8       48   52428800 sdd
     8       49   52428096 sdd1
     8       64   52428800 sde
     8       65   52428096 sde1
     8       80   52428800 sdf
     8       81   52428096 sdf1
     8        0   52428800 sda
     8        1     512000 sda1
     8        2   51915776 sda2
     11       0    1048575 sr0
   ```

6. <span data-ttu-id="1c64e-163">檢查 hello Oracle ASM 服務狀態，並啟動 hello Oracle ASM 服務：</span><span class="sxs-lookup"><span data-stu-id="1c64e-163">Check hello Oracle ASM service status and start hello Oracle ASM service:</span></span>

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   <span data-ttu-id="1c64e-164">hello hello 命令輸出看起來應該類似下列 hello:</span><span class="sxs-lookup"><span data-stu-id="1c64e-164">hello output of hello command should look like hello following:</span></span>
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing hello Oracle ASMLib driver:                     [  OK  ]
   Scanning hello system for Oracle ASMLib disks:               [  OK  ]
   ```

7. <span data-ttu-id="1c64e-165">建立 Oracle ASM 磁碟︰</span><span class="sxs-lookup"><span data-stu-id="1c64e-165">Create Oracle ASM disks:</span></span>

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   <span data-ttu-id="1c64e-166">hello hello 命令輸出看起來應該類似下列 hello:</span><span class="sxs-lookup"><span data-stu-id="1c64e-166">hello output of hello command should look like hello following:</span></span>

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. <span data-ttu-id="1c64e-167">列出 Oracle ASM 磁碟︰</span><span class="sxs-lookup"><span data-stu-id="1c64e-167">List Oracle ASM disks:</span></span>

   ```bash
   service oracleasm listdisks
   ```   

   <span data-ttu-id="1c64e-168">hello hello 命令輸出應該會列出下列 Oracle ASM 磁碟 hello 關閉：</span><span class="sxs-lookup"><span data-stu-id="1c64e-168">hello output of hello command should list off hello following Oracle ASM disks:</span></span>

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. <span data-ttu-id="1c64e-169">變更 hello hello 根、 oracle 和方格使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="1c64e-169">Change hello passwords for hello root, oracle, and grid users.</span></span> <span data-ttu-id="1c64e-170">**請記下這些新的密碼**因為您稍後在 hello 安裝期間使用它們。</span><span class="sxs-lookup"><span data-stu-id="1c64e-170">**Make note of these new passwords** as you are using them later during hello installation.</span></span>

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. <span data-ttu-id="1c64e-171">變更 hello 資料夾權限：</span><span class="sxs-lookup"><span data-stu-id="1c64e-171">Change hello folder permission:</span></span>

   ```bash
   chmod -R 775 /opt 
   chown grid:oinstall /opt 
   chown oracle:oinstall /dev/sdc1 
   chown oracle:oinstall /dev/sdd1 
   chown oracle:oinstall /dev/sde1 
   chown oracle:oinstall /dev/sdf1 
   chmod 600 /dev/sdc1 
   chmod 600 /dev/sdd1 
   chmod 600 /dev/sde1 
   chmod 600 /dev/sdf1
   ```

## <a name="download-and-prepare-oracle-grid-infrastructure"></a><span data-ttu-id="1c64e-172">下載並準備 Oracle Grid Infrastructure</span><span class="sxs-lookup"><span data-stu-id="1c64e-172">Download and prepare Oracle Grid Infrastructure</span></span>

<span data-ttu-id="1c64e-173">toodownload 並準備 hello Oracle 方格基礎結構軟體，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c64e-173">toodownload and prepare hello Oracle Grid Infrastructure software, complete hello following steps:</span></span>

1. <span data-ttu-id="1c64e-174">下載 Oracle 方格基礎結構從 hello [Oracle ASM 下載頁面](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html)。</span><span class="sxs-lookup"><span data-stu-id="1c64e-174">Download Oracle Grid Infrastructure from hello [Oracle ASM download page](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span></span> 

   <span data-ttu-id="1c64e-175">下面的 hello 下載**Oracle Database 12c 版本 1 方格基礎結構 (12.1.0.2.0) 的 Linux x86-64**，下載 hello 兩個.zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="1c64e-175">Under hello download titled **Oracle Database 12c Release 1 Grid Infrastructure (12.1.0.2.0) for Linux x86-64**, download hello two .zip files.</span></span>

2. <span data-ttu-id="1c64e-176">下載 hello.zip 檔案 tooyour 用戶端電腦之後，您可以使用安全複製通訊協定 (SCP) toocopy hello 檔案 tooyour VM:</span><span class="sxs-lookup"><span data-stu-id="1c64e-176">After you download hello .zip files tooyour client computer, you can use Secure Copy Protocol (SCP) toocopy hello files tooyour VM:</span></span>

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. <span data-ttu-id="1c64e-177">SSH Oracle VM 在 Azure 中將 hello 順序 toomove hello.zip 檔案放回/選擇資料夾。</span><span class="sxs-lookup"><span data-stu-id="1c64e-177">SSH back into your Oracle VM in Azure in order toomove hello .zip files into hello /opt folder.</span></span> <span data-ttu-id="1c64e-178">然後，變更 hello hello 檔案擁有者：</span><span class="sxs-lookup"><span data-stu-id="1c64e-178">Then, change hello owner of hello files:</span></span>

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. <span data-ttu-id="1c64e-179">將 hello 檔解壓縮。</span><span class="sxs-lookup"><span data-stu-id="1c64e-179">Unzip hello files.</span></span> <span data-ttu-id="1c64e-180">（如果尚未安裝安裝 hello Linux 解壓縮工具）。</span><span class="sxs-lookup"><span data-stu-id="1c64e-180">(Install hello Linux unzip tool if it's not already installed.)</span></span>
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. <span data-ttu-id="1c64e-181">變更權限：</span><span class="sxs-lookup"><span data-stu-id="1c64e-181">Change permission:</span></span>
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. <span data-ttu-id="1c64e-182">更新設定的交換空間。</span><span class="sxs-lookup"><span data-stu-id="1c64e-182">Update configured swap space.</span></span> <span data-ttu-id="1c64e-183">Oracle 方格元件需要至少 6.8 GB 的交換空間 tooinstall 方格。</span><span class="sxs-lookup"><span data-stu-id="1c64e-183">Oracle Grid components need at least 6.8 GB of swap space tooinstall Grid.</span></span> <span data-ttu-id="1c64e-184">Oracle Linux 映像，在 Azure 中的 hello 預設交換檔案大小是只有 2048 MB。</span><span class="sxs-lookup"><span data-stu-id="1c64e-184">hello default swap file size for Oracle Linux images in Azure is only 2048MB.</span></span> <span data-ttu-id="1c64e-185">您需要 tooincrease`ResourceDisk.SwapSizeMB`在 hello`/etc/waagent.conf`檔案，並重新啟動 hello WALinuxAgent 服務，hello 更新設定 tootake 效果。</span><span class="sxs-lookup"><span data-stu-id="1c64e-185">You need tooincrease `ResourceDisk.SwapSizeMB` in hello `/etc/waagent.conf` file and restart hello WALinuxAgent service in order for hello updated settings tootake effect.</span></span> <span data-ttu-id="1c64e-186">因為它是唯讀的檔案，您會需要 toochange 檔案權限 tooenable 寫入權限。</span><span class="sxs-lookup"><span data-stu-id="1c64e-186">Because it is a read-only file, you need toochange file permissions tooenable write access.</span></span>

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   <span data-ttu-id="1c64e-187">搜尋`ResourceDisk.SwapSizeMB`太變更 hello 值**8192**。</span><span class="sxs-lookup"><span data-stu-id="1c64e-187">Search for `ResourceDisk.SwapSizeMB` and change hello value too**8192**.</span></span> <span data-ttu-id="1c64e-188">您將需要 toopress `insert` tooenter 插入模式中，型別中的 hello 值**8192** ，然後按`esc`tooreturn toocommand 模式。</span><span class="sxs-lookup"><span data-stu-id="1c64e-188">You will need toopress `insert` tooenter insert mode, type in hello value of **8192** and then press `esc` tooreturn toocommand mode.</span></span> <span data-ttu-id="1c64e-189">toowrite hello 變更和 quit 的 hello 檔案中，輸入`:wq`按`enter`。</span><span class="sxs-lookup"><span data-stu-id="1c64e-189">toowrite hello changes and quit hello file, type `:wq` and press `enter`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1c64e-190">我們強烈建議您一定要使用`WALinuxAgent`tooconfigure 交換空間，使它一定會建立 hello 暫時在本機磁碟上 （暫存磁碟） 為了達到最佳效能。</span><span class="sxs-lookup"><span data-stu-id="1c64e-190">We highly recommend that you always use `WALinuxAgent` tooconfigure swap space so that it's always created on hello local ephemeral disk (temporary disk) for best performance.</span></span> <span data-ttu-id="1c64e-191">如需詳細資訊，請參閱[tooadd 交換 Linux 的 Azure 虛擬機器中的檔案如何](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines)。</span><span class="sxs-lookup"><span data-stu-id="1c64e-191">For more information on, see [How tooadd a swap file in Linux Azure virtual machines](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span></span>

## <a name="prepare-your-local-client-and-vm-toorun-x11"></a><span data-ttu-id="1c64e-192">準備您的本機用戶端和 VM toorun x11</span><span class="sxs-lookup"><span data-stu-id="1c64e-192">Prepare your local client and VM toorun x11</span></span>
<span data-ttu-id="1c64e-193">設定 Oracle ASM 需要圖形化介面 toocomplete hello 安裝和組態。</span><span class="sxs-lookup"><span data-stu-id="1c64e-193">Configuring Oracle ASM requires a graphical interface toocomplete hello install and configuration.</span></span> <span data-ttu-id="1c64e-194">我們使用 hello x11 通訊協定 toofacilitate 此安裝。</span><span class="sxs-lookup"><span data-stu-id="1c64e-194">We are using hello x11 protocol toofacilitate this installation.</span></span> <span data-ttu-id="1c64e-195">如果您使用用戶端系統 （Mac 或 Linux） 已經有 X11 功能已啟用，而且已設定-您可以略過此設定並安裝獨佔 tooWindows 機器。</span><span class="sxs-lookup"><span data-stu-id="1c64e-195">If you are using a client system (Mac or Linux) that already has X11 capabilities enabled and configured - you can skip this configuration and setup exclusive tooWindows machines.</span></span> 

1. <span data-ttu-id="1c64e-196">[下載 PuTTY](http://www.putty.org/)和[下載 Xming](https://xming.en.softonic.com/) tooyour Windows 電腦。</span><span class="sxs-lookup"><span data-stu-id="1c64e-196">[Download PuTTY](http://www.putty.org/) and [download Xming](https://xming.en.softonic.com/) tooyour Windows computer.</span></span> <span data-ttu-id="1c64e-197">您需要 toocomplete hello 安裝兩個 hello 預設值，再繼續這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c64e-197">You will need toocomplete hello installation of both of these applications with hello default values before proceeding.</span></span>

2. <span data-ttu-id="1c64e-198">安裝 PuTTY 之後，開啟命令提示字元，變更為 hello PuTTY 資料夾 (例如，C:\Program Files\PuTTY) 並執行`puttygen.exe`中排序 toogenerate 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="1c64e-198">After you install PuTTY, open a command prompt, change into hello PuTTY folder (for example, C:\Program Files\PuTTY), and run `puttygen.exe` in order toogenerate a key.</span></span>

3. <span data-ttu-id="1c64e-199">在 PuTTY 金鑰產生器中︰</span><span class="sxs-lookup"><span data-stu-id="1c64e-199">In PuTTY Key Generator:</span></span>
   
   1. <span data-ttu-id="1c64e-200">產生金鑰選取 hello `Generate`  按鈕。</span><span class="sxs-lookup"><span data-stu-id="1c64e-200">Generate a key by selecting hello `Generate` button.</span></span>
   2. <span data-ttu-id="1c64e-201">複製 hello 的 hello 按鍵 (Ctrl + C) 的內容。</span><span class="sxs-lookup"><span data-stu-id="1c64e-201">Copy hello contents of hello key (Ctrl+C).</span></span>
   3. <span data-ttu-id="1c64e-202">選取 hello `Save private key`  按鈕。</span><span class="sxs-lookup"><span data-stu-id="1c64e-202">Select hello `Save private key` button.</span></span>
   4. <span data-ttu-id="1c64e-203">忽略有關保護 hello 金鑰的複雜密碼的 hello 警告，然後選取  `OK`。</span><span class="sxs-lookup"><span data-stu-id="1c64e-203">Ignore hello warning about securing hello key with a passphrase, and then select `OK`.</span></span>

   ![PuTTY 金鑰產生器的螢幕擷取畫面](./media/oracle-asm/puttykeygen.png)

4. <span data-ttu-id="1c64e-205">在您的 VM 中，執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="1c64e-205">In your VM, run these commands:</span></span>

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. <span data-ttu-id="1c64e-206">建立名為 `authorized_keys` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="1c64e-206">Create a file named `authorized_keys`.</span></span> <span data-ttu-id="1c64e-207">Hello hello 金鑰內容貼在檔案中，然後將檔案儲存 hello。</span><span class="sxs-lookup"><span data-stu-id="1c64e-207">Paste hello contents of hello key in this file, and then save hello file.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1c64e-208">hello 金鑰必須包含字串 hello `ssh-rsa`。</span><span class="sxs-lookup"><span data-stu-id="1c64e-208">hello key must contain hello string `ssh-rsa`.</span></span> <span data-ttu-id="1c64e-209">此外，hello hello 索引鍵內容必須是單行文字。</span><span class="sxs-lookup"><span data-stu-id="1c64e-209">Also, hello contents of hello key must be a single line of text.</span></span>
   >  

6. <span data-ttu-id="1c64e-210">在用戶端系統上，啟動 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="1c64e-210">On your client system, start PuTTY.</span></span> <span data-ttu-id="1c64e-211">在 hello**類別**] 窗格中，跳過**連接** > **SSH** > **Auth**。在 [hello**私密金鑰檔案驗證**方塊中，瀏覽您先前產生的 toohello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="1c64e-211">In hello **Category** pane, go too**Connection** > **SSH** > **Auth**. In hello **Private key file for authentication** box, browse toohello key that you generated earlier.</span></span>

   ![Hello SSH 驗證選項的螢幕擷取畫面](./media/oracle-asm/setprivatekey.png)

7. <span data-ttu-id="1c64e-213">在 [hello**類別**] 窗格中，跳過**連接** > **SSH** > **X11**。</span><span class="sxs-lookup"><span data-stu-id="1c64e-213">In hello **Category** pane, go too**Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="1c64e-214">選取 hello**啟用 X11 轉寄**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1c64e-214">Select hello **Enable X11 forwarding** check box.</span></span>

   ![螢幕擷取畫面的 hello SSH X11 轉寄選項](./media/oracle-asm/enablex11.png)

8. <span data-ttu-id="1c64e-216">在 [hello**類別**] 窗格中，跳過**工作階段**。</span><span class="sxs-lookup"><span data-stu-id="1c64e-216">In hello **Category** pane, go too**Session**.</span></span> <span data-ttu-id="1c64e-217">輸入您的 Oracle ASM VM`<publicIPaddress>`在 hello 主機名稱 對話方塊中，填入新`Saved Session`命名，然後按一下上`Save`。</span><span class="sxs-lookup"><span data-stu-id="1c64e-217">Enter your Oracle ASM VM `<publicIPaddress>` in hello host name dialog box, fill in a new `Saved Session` name and then click on `Save`.</span></span>  <span data-ttu-id="1c64e-218">儲存之後，按一下`open`tooconnect tooyour Oracle ASM 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1c64e-218">Once saved, click on `open` tooconnect tooyour Oracle ASM virtual machine.</span></span>  <span data-ttu-id="1c64e-219">hello 您連接您的第一次警告 hello 遠端系統不會快取中登錄。</span><span class="sxs-lookup"><span data-stu-id="1c64e-219">hello first time you connect you are warned  hello remote system is not cached in your registry.</span></span> <span data-ttu-id="1c64e-220">按一下`yes`tooadd 它並繼續。</span><span class="sxs-lookup"><span data-stu-id="1c64e-220">Click on `yes` tooadd it and continue.</span></span>

   ![Hello PuTTY 工作階段選項的螢幕擷取畫面](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a><span data-ttu-id="1c64e-222">安裝 Oracle Grid Infrastructure</span><span class="sxs-lookup"><span data-stu-id="1c64e-222">Install Oracle Grid Infrastructure</span></span>

<span data-ttu-id="1c64e-223">tooinstall Oracle 方格基礎結構，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c64e-223">tooinstall Oracle Grid Infrastructure, complete hello following steps:</span></span>

1. <span data-ttu-id="1c64e-224">以 **grid** 的身分登入。</span><span class="sxs-lookup"><span data-stu-id="1c64e-224">Sign in as **grid**.</span></span> <span data-ttu-id="1c64e-225">（您應該能夠 toosign 中的，而不會提示輸入密碼）。</span><span class="sxs-lookup"><span data-stu-id="1c64e-225">(You should be able toosign in without being prompted for a password.)</span></span> 

   > [!NOTE]
   > <span data-ttu-id="1c64e-226">如果您執行 Windows，請確定您已經啟動 Xming hello 安裝開始之前。</span><span class="sxs-lookup"><span data-stu-id="1c64e-226">If you are running Windows, make sure you have started Xming before you begin hello installation.</span></span>

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   <span data-ttu-id="1c64e-227">Oracle Grid Infrastructure 12c Release 1 安裝程式會隨即開啟 </span><span class="sxs-lookup"><span data-stu-id="1c64e-227">Oracle Grid Infrastructure 12c Release 1 Installer opens.</span></span> <span data-ttu-id="1c64e-228">（它可能需要幾分鐘，讓 hello installer toostart）。</span><span class="sxs-lookup"><span data-stu-id="1c64e-228">(It might take a few minutes for hello  installer toostart.)</span></span>

2. <span data-ttu-id="1c64e-229">在 hello**選取安裝選項**頁面上，選取**安裝和設定 Oracle 方格基礎結構適用於獨立伺服器**。</span><span class="sxs-lookup"><span data-stu-id="1c64e-229">On hello **Select Installation Option** page, select **Install and Configure Oracle Grid Infrastructure for a Standalone Server**.</span></span>

   ![Hello 安裝程式的 [選取安裝選項] 頁面的螢幕擷取畫面](./media/oracle-asm/install01.png)

3. <span data-ttu-id="1c64e-231">在 hello**選取產品語言**頁面上，確定**英文**或選取您想要的 hello 語言。</span><span class="sxs-lookup"><span data-stu-id="1c64e-231">On hello **Select Product Languages** page, ensure **English** or hello language that you want is selected.</span></span>  <span data-ttu-id="1c64e-232">按一下 `next`。</span><span class="sxs-lookup"><span data-stu-id="1c64e-232">Click `next`.</span></span>

4. <span data-ttu-id="1c64e-233">在 hello**建立 ASM 磁碟群組**頁面：</span><span class="sxs-lookup"><span data-stu-id="1c64e-233">On hello **Create ASM Disk Group** page:</span></span>
   - <span data-ttu-id="1c64e-234">輸入 hello 磁碟群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="1c64e-234">Enter a name for hello disk group.</span></span>
   - <span data-ttu-id="1c64e-235">在 [備援] 底下選取 [外部]。</span><span class="sxs-lookup"><span data-stu-id="1c64e-235">Under **Redundancy**, select **External**.</span></span>
   - <span data-ttu-id="1c64e-236">在 [配置單位大小] 底下選取 [4]。</span><span class="sxs-lookup"><span data-stu-id="1c64e-236">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="1c64e-237">在 [新增磁碟] 底下選取 [ORCLASMSP]。</span><span class="sxs-lookup"><span data-stu-id="1c64e-237">Under **Add Disks**, select **ORCLASMSP**.</span></span>
   - <span data-ttu-id="1c64e-238">按一下 `next`。</span><span class="sxs-lookup"><span data-stu-id="1c64e-238">Click `next`.</span></span>

5. <span data-ttu-id="1c64e-239">在 hello**指定 ASM 密碼**頁面上，選取 hello**使用這些帳戶的相同密碼**選項，然後輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="1c64e-239">On hello **Specify ASM Password** page, select hello **Use same passwords for these accounts** option, and enter a password.</span></span>

   ![安裝程式 hello 指定 ASM 密碼 頁面的螢幕擷取畫面](./media/oracle-asm/install04.png)

6. <span data-ttu-id="1c64e-241">在 [hello**指定管理選項**] 頁面上，您擁有 hello 選項 tooconfigure EM 雲端控制項。</span><span class="sxs-lookup"><span data-stu-id="1c64e-241">On hello **Specify Management Options** page, you have hello option tooconfigure EM Cloud Control.</span></span> <span data-ttu-id="1c64e-242">我們正略過此選項-按一下`next`toocontinue。</span><span class="sxs-lookup"><span data-stu-id="1c64e-242">We are skipping this option - click `next` toocontinue.</span></span> 

7. <span data-ttu-id="1c64e-243">在 hello**特殊權限的作業系統群組**頁面上，使用 hello 預設設定。</span><span class="sxs-lookup"><span data-stu-id="1c64e-243">On hello **Privileged Operating System Groups** page, use hello default settings.</span></span> <span data-ttu-id="1c64e-244">按一下`next`toocontinue。</span><span class="sxs-lookup"><span data-stu-id="1c64e-244">Click `next` toocontinue.</span></span>

8. <span data-ttu-id="1c64e-245">在 hello**指定安裝位置**頁面上，使用 hello 預設設定。</span><span class="sxs-lookup"><span data-stu-id="1c64e-245">On hello **Specify Installation Location** page, use hello default settings.</span></span> <span data-ttu-id="1c64e-246">按一下`next`toocontinue。</span><span class="sxs-lookup"><span data-stu-id="1c64e-246">Click `next` toocontinue.</span></span>

9. <span data-ttu-id="1c64e-247">在 hello**建立清查**頁面上，變更 hello 清查目錄太`/u01/app/grid/oraInventory`。</span><span class="sxs-lookup"><span data-stu-id="1c64e-247">On hello **Create Inventory** page, change hello Inventory Directory too`/u01/app/grid/oraInventory`.</span></span> <span data-ttu-id="1c64e-248">按一下`next`toocontinue。</span><span class="sxs-lookup"><span data-stu-id="1c64e-248">Click `next` toocontinue.</span></span>

   ![Hello 安裝程式建立詳細目錄 頁面的螢幕擷取畫面](./media/oracle-asm/install08.png)

10. <span data-ttu-id="1c64e-250">在 hello**根指令碼執行組態**頁面上，選取 hello**自動執行組態指令碼**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1c64e-250">On hello **Root script execution configuration** page, select hello **Automatically run configuration scripts** check box.</span></span> <span data-ttu-id="1c64e-251">然後，選取 hello**使用 「 根 」 的使用者認證**選項，然後輸入 hello 根使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="1c64e-251">Then, select hello **Use "root" user credential** option, and enter hello root user password.</span></span>

    ![Hello 安裝程式的根指令碼執行組態 頁面的螢幕擷取畫面](./media/oracle-asm/install09.png)

11. <span data-ttu-id="1c64e-253">在 [hello**執行必要條件檢查**] 頁面上，hello 目前的安裝程式將會失敗並出現錯誤。</span><span class="sxs-lookup"><span data-stu-id="1c64e-253">On hello **Perform Prerequisite Checks** page, hello current setup will fail with errors.</span></span> <span data-ttu-id="1c64e-254">這是預期中的行為。</span><span class="sxs-lookup"><span data-stu-id="1c64e-254">This is an expected behavior.</span></span> <span data-ttu-id="1c64e-255">選取 `Fix & Check Again`。</span><span class="sxs-lookup"><span data-stu-id="1c64e-255">Select `Fix & Check Again`.</span></span>

12. <span data-ttu-id="1c64e-256">在 hello**修復指令碼**對話方塊中，按一下  `OK`。</span><span class="sxs-lookup"><span data-stu-id="1c64e-256">In hello **Fixup Script** dialog box, click `OK`.</span></span>

13. <span data-ttu-id="1c64e-257">在 hello**摘要**頁面上，檢閱您選取的設定，然後按一下`Install`。</span><span class="sxs-lookup"><span data-stu-id="1c64e-257">On hello **Summary** page, review your selected settings, and then click `Install`.</span></span>

    ![Hello 安裝程式的 [摘要] 頁面的螢幕擷取畫面](./media/oracle-asm/install12.png)

14. <span data-ttu-id="1c64e-259">警告會出現對話方塊通知您設定指令碼需要特殊權限的使用者身分執行 toobe。</span><span class="sxs-lookup"><span data-stu-id="1c64e-259">A warning dialog box appears informing you configuration scripts need toobe run as a privileged user.</span></span> <span data-ttu-id="1c64e-260">按一下`Yes`toocontinue。</span><span class="sxs-lookup"><span data-stu-id="1c64e-260">Click `Yes` toocontinue.</span></span>

15. <span data-ttu-id="1c64e-261">在 hello**完成**頁面上，按一下`Close`toofinish hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="1c64e-261">On hello **Finish** page, click `Close` toofinish hello installation.</span></span>

## <a name="set-up-your-oracle-asm-installation"></a><span data-ttu-id="1c64e-262">設定 Oracle ASM 安裝</span><span class="sxs-lookup"><span data-stu-id="1c64e-262">Set up your Oracle ASM installation</span></span>

<span data-ttu-id="1c64e-263">註冊您的 Oracle ASM 安裝，完成下列步驟的 hello tooset:</span><span class="sxs-lookup"><span data-stu-id="1c64e-263">tooset up your Oracle ASM installation, complete hello following steps:</span></span>

1. <span data-ttu-id="1c64e-264">請確定您仍從 X11 工作階段以 **grid** 的身分登入。</span><span class="sxs-lookup"><span data-stu-id="1c64e-264">Ensure you are still signed in as **grid**, from your X11 session.</span></span> <span data-ttu-id="1c64e-265">您可能需要 toohit `enter` toorevive hello 終端機。</span><span class="sxs-lookup"><span data-stu-id="1c64e-265">You might need toohit `enter` toorevive hello terminal.</span></span> <span data-ttu-id="1c64e-266">然後啟動 Oracle 自動儲存體管理 Configuration Assistant hello:</span><span class="sxs-lookup"><span data-stu-id="1c64e-266">Then launch hello Oracle Automated Storage Management Configuration Assistant:</span></span>

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   <span data-ttu-id="1c64e-267">Oracle ASM Configuration Assistant 隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="1c64e-267">Oracle ASM Configuration Assistant opens.</span></span>

2. <span data-ttu-id="1c64e-268">在 hello**設定 ASM： 磁碟群組**對話方塊方塊中，按一下 hello`Create`按鈕，然後再按一下`Show Advanced Options`。</span><span class="sxs-lookup"><span data-stu-id="1c64e-268">In hello **Configure ASM: Disk Groups** dialog box, click hello `Create` button, and then click `Show Advanced Options`.</span></span>

3. <span data-ttu-id="1c64e-269">在 hello**建立磁碟群組**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="1c64e-269">In hello **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="1c64e-270">輸入 hello 磁碟群組名稱**資料**。</span><span class="sxs-lookup"><span data-stu-id="1c64e-270">Enter hello disk group name **DATA**.</span></span>
   - <span data-ttu-id="1c64e-271">在 [選取成員磁碟] 底下選取 [ORCL_DATA] 和 [ORCL_DATA1]。</span><span class="sxs-lookup"><span data-stu-id="1c64e-271">Under **Select Member Disks**, select **ORCL_DATA** and **ORCL_DATA1**.</span></span>
   - <span data-ttu-id="1c64e-272">在 [配置單位大小] 底下選取 [4]。</span><span class="sxs-lookup"><span data-stu-id="1c64e-272">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="1c64e-273">按一下`ok`toocreate hello 磁碟群組。</span><span class="sxs-lookup"><span data-stu-id="1c64e-273">Click `ok` toocreate hello disk group.</span></span>
   - <span data-ttu-id="1c64e-274">按一下`ok`tooclose hello 確認視窗。</span><span class="sxs-lookup"><span data-stu-id="1c64e-274">Click `ok` tooclose hello confirmation window.</span></span>

   ![Hello 建立磁碟群組 對話方塊的螢幕擷取畫面](./media/oracle-asm/asm02.png)

4. <span data-ttu-id="1c64e-276">在 hello**設定 ASM： 磁碟群組**對話方塊方塊中，按一下 hello`Create`按鈕，然後再按一下`Show Advanced Options`。</span><span class="sxs-lookup"><span data-stu-id="1c64e-276">In hello **Configure ASM: Disk Groups** dialog box, click hello `Create` button, and then click `Show Advanced Options`.</span></span>

5. <span data-ttu-id="1c64e-277">在 hello**建立磁碟群組**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="1c64e-277">In hello **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="1c64e-278">輸入 hello 磁碟群組名稱**FRA**。</span><span class="sxs-lookup"><span data-stu-id="1c64e-278">Enter hello disk group name **FRA**.</span></span>
   - <span data-ttu-id="1c64e-279">在 [備援] 底下選取 [外部 (無)]。</span><span class="sxs-lookup"><span data-stu-id="1c64e-279">Under **Redundancy**, select **External (none)**.</span></span>
   - <span data-ttu-id="1c64e-280">在 [選取成員磁碟] 底下選取 [ORCL_FRA]。</span><span class="sxs-lookup"><span data-stu-id="1c64e-280">Under **Select Member Disks**, select **ORCL_FRA**.</span></span>
   - <span data-ttu-id="1c64e-281">在 [配置單位大小] 底下選取 [4]。</span><span class="sxs-lookup"><span data-stu-id="1c64e-281">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="1c64e-282">按一下`ok`toocreate hello 磁碟群組。</span><span class="sxs-lookup"><span data-stu-id="1c64e-282">Click `ok` toocreate hello disk group.</span></span>
   - <span data-ttu-id="1c64e-283">按一下`ok`tooclose hello 確認視窗。</span><span class="sxs-lookup"><span data-stu-id="1c64e-283">Click `ok` tooclose hello confirmation window.</span></span>

   ![Hello 建立磁碟群組 對話方塊的螢幕擷取畫面](./media/oracle-asm/asm04.png)

6. <span data-ttu-id="1c64e-285">選取**結束**tooclose ASM Configuration Assistant。</span><span class="sxs-lookup"><span data-stu-id="1c64e-285">Select **Exit** tooclose ASM Configuration Assistant.</span></span>

   ![螢幕擷取畫面的 hello 設定 ASM： 磁碟群組 對話方塊的 結束 按鈕](./media/oracle-asm/asm05.png)

## <a name="create-hello-database"></a><span data-ttu-id="1c64e-287">建立 hello 資料庫</span><span class="sxs-lookup"><span data-stu-id="1c64e-287">Create hello database</span></span>

<span data-ttu-id="1c64e-288">hello Oracle 資料庫軟體已經安裝 hello Azure Marketplace 映像上。</span><span class="sxs-lookup"><span data-stu-id="1c64e-288">hello Oracle database software is already installed on hello Azure Marketplace image.</span></span> <span data-ttu-id="1c64e-289">toocreate 資料庫中，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c64e-289">toocreate a database, complete hello following steps:</span></span>

1. <span data-ttu-id="1c64e-290">切換使用者 toohello Oracle 超級使用者，然後初始化 記錄的 hello 接聽程式：</span><span class="sxs-lookup"><span data-stu-id="1c64e-290">Switch users toohello Oracle superuser, and then initialize hello listener for logging:</span></span>

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   <span data-ttu-id="1c64e-291">Database Configuration Assistant 隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="1c64e-291">Database Configuration Assistant opens.</span></span>

2. <span data-ttu-id="1c64e-292">在 hello**資料庫作業**頁面上，按一下`Create Database`。</span><span class="sxs-lookup"><span data-stu-id="1c64e-292">On hello **Database Operation** page, click `Create Database`.</span></span>

3. <span data-ttu-id="1c64e-293">在 hello**建立模式**頁面：</span><span class="sxs-lookup"><span data-stu-id="1c64e-293">On hello **Creation Mode** page:</span></span>

   - <span data-ttu-id="1c64e-294">輸入 hello 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="1c64e-294">Enter a name for hello database.</span></span>
   - <span data-ttu-id="1c64e-295">在 [儲存體類型] 中，請確定已選取 [自動儲存體管理 (ASM)]。</span><span class="sxs-lookup"><span data-stu-id="1c64e-295">For **Storage Type**, ensure **Automatic Storage Management (ASM)** is selected.</span></span>
   - <span data-ttu-id="1c64e-296">如**資料庫檔案位置**，使用預設的 hello ASM 建議位置。</span><span class="sxs-lookup"><span data-stu-id="1c64e-296">For **Database Files Location**, use hello default ASM suggested location.</span></span>
   - <span data-ttu-id="1c64e-297">如**快速復原區域**，使用預設的 hello ASM 建議位置。</span><span class="sxs-lookup"><span data-stu-id="1c64e-297">For **Fast Recovery Area**, use hello default ASM suggested location.</span></span>
   - <span data-ttu-id="1c64e-298">輸入 [管理密碼] 和 [確認密碼]。</span><span class="sxs-lookup"><span data-stu-id="1c64e-298">type in an **Administrative Password** and **confirm password**.</span></span>
   - <span data-ttu-id="1c64e-299">確定已選取 `create as container database`。</span><span class="sxs-lookup"><span data-stu-id="1c64e-299">ensure `create as container database` is selected.</span></span>
   - <span data-ttu-id="1c64e-300">輸入 `pluggable database name` 值。</span><span class="sxs-lookup"><span data-stu-id="1c64e-300">type in a `pluggable database name` value.</span></span>

4. <span data-ttu-id="1c64e-301">在 hello**摘要**頁面上，檢閱您選取的設定，然後按一下`Finish`toocreate hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1c64e-301">On hello **Summary** page, review your selected settings, and then click `Finish` toocreate hello database.</span></span>

   ![Hello 摘要 頁面的螢幕擷取畫面](./media/oracle-asm/createdb03.png)

5. <span data-ttu-id="1c64e-303">已建立 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1c64e-303">hello Database has been created.</span></span> <span data-ttu-id="1c64e-304">在 hello**完成**頁面上，您可以 hello 選項 toounlock 其他帳戶 toouse 這個資料庫，然後變更 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="1c64e-304">On hello **Finish** page, you have hello option toounlock additional accounts toouse this database and change hello passwords.</span></span> <span data-ttu-id="1c64e-305">如果想 toodo 操作，請選取**密碼管理**-否則按一下`close`。</span><span class="sxs-lookup"><span data-stu-id="1c64e-305">If you wish toodo so, select **Password Management** - otherwise click on `close`.</span></span>

## <a name="delete-hello-vm"></a><span data-ttu-id="1c64e-306">刪除 VM hello</span><span class="sxs-lookup"><span data-stu-id="1c64e-306">Delete hello VM</span></span>

<span data-ttu-id="1c64e-307">您已成功從 hello Azure Marketplace 的 hello Oracle DB 映像上設定 Oracle 自動儲存體管理。</span><span class="sxs-lookup"><span data-stu-id="1c64e-307">You have successfully configured Oracle Automated Storage Management on hello Oracle DB image from hello Azure Marketplace.</span></span>  <span data-ttu-id="1c64e-308">當您不再需要此 VM 時，您可以使用下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c64e-308">When you no longer need this VM, you can use hello following command tooremove hello resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="1c64e-309">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1c64e-309">Next steps</span></span>

[<span data-ttu-id="1c64e-310">教學課程：設定 Oracle DataGuard</span><span class="sxs-lookup"><span data-stu-id="1c64e-310">Tutorial: Configure Oracle DataGuard</span></span>](configure-oracle-dataguard.md)

[<span data-ttu-id="1c64e-311">教學課程：設定 Oracle GoldenGate</span><span class="sxs-lookup"><span data-stu-id="1c64e-311">Tutorial: Configure Oracle GoldenGate</span></span>](Configure-oracle-golden-gate.md)

<span data-ttu-id="1c64e-312">請檢閱[建置 Oracle DB](oracle-design.md)</span><span class="sxs-lookup"><span data-stu-id="1c64e-312">Review [Architect an Oracle DB](oracle-design.md)</span></span>
