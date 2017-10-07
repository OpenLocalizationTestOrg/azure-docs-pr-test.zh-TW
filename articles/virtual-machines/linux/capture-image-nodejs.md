---
title: "為範本 Azure Linux VM toouse aaaCapture |Microsoft 文件"
description: "深入了解如何 toocapture 和 Linux 型 Azure 虛擬機器 (VM) 與 hello Azure Resource Manager 部署模型所建立的映像一般化。"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 877eee5c842bebe80e755c2240cdaaef4ade6ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a><span data-ttu-id="a35a6-103">擷取在 Azure 上執行的 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a35a6-103">Capture a Linux virtual machine running on Azure</span></span>
<span data-ttu-id="a35a6-104">請遵循本文章 toogeneralize 中的 hello 步驟，並擷取 Azure Linux 虛擬機器 (VM) 中 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="a35a6-104">Follow hello steps in this article toogeneralize and capture your Azure Linux virtual machine (VM) in hello Resource Manager deployment model.</span></span> <span data-ttu-id="a35a6-105">當一般化 hello VM 時，您會移除個人帳戶資訊，並準備 hello VM toobe 做為映像。</span><span class="sxs-lookup"><span data-stu-id="a35a6-105">When you generalize hello VM, you remove personal account information and prepare hello VM toobe used as an image.</span></span> <span data-ttu-id="a35a6-106">您接著擷取的 hello 的作業系統上，連接的資料磁碟的 Vhd 映像一般化虛擬硬碟 (VHD) 和[Resource Manager 範本](../../azure-resource-manager/resource-group-overview.md)針對新的 VM 部署。</span><span class="sxs-lookup"><span data-stu-id="a35a6-106">You then capture a generalized virtual hard disk (VHD) image for hello OS, VHDs for attached data disks, and a [Resource Manager template](../../azure-resource-manager/resource-group-overview.md) for new VM deployments.</span></span> <span data-ttu-id="a35a6-107">這篇文章說明如何 toocapture VM 的映像以 hello Azure CLI 1.0 使用未受管理的磁碟的 VM。</span><span class="sxs-lookup"><span data-stu-id="a35a6-107">This article details how toocapture a VM image with hello Azure CLI 1.0 for a VM using unmanaged disks.</span></span> <span data-ttu-id="a35a6-108">您也可以[擷取 VM，使用 Azure 受管理磁碟的 hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a35a6-108">You can also [capture a VM using Azure Managed Disks with hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="a35a6-109">受管理的磁碟都由 hello Azure 平台，而且不需要任何準備或位置 toostore 它們。</span><span class="sxs-lookup"><span data-stu-id="a35a6-109">Managed disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="a35a6-110">如需詳細資訊，請參閱 [Azure 受控磁碟概觀](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a35a6-110">For more information, see [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="a35a6-111">toocreate Vm 使用 hello 映像，為每個新的 VM，並將它從 hello 擷取 VHD 映像使用 hello 範本 （JavaScript 物件標記法或 JSON，檔案） toodeploy 設定網路資源。</span><span class="sxs-lookup"><span data-stu-id="a35a6-111">toocreate VMs using hello image, set up network resources for each new VM, and use hello template (a JavaScript Object Notation, or JSON, file) toodeploy it from hello captured VHD images.</span></span> <span data-ttu-id="a35a6-112">如此一來，您可以複寫其目前軟體的組態，toohello 類似您在 hello Azure Marketplace 中使用映像的 VM。</span><span class="sxs-lookup"><span data-stu-id="a35a6-112">In this way, you can replicate a VM with its current software configuration, similar toohello way you use images in hello Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="a35a6-113">如果您想 toocreate 一份您現有的 Linux VM 以其特定狀態的備份] 或 [偵錯時，請參閱[建立在 Azure 上執行的 Linux 虛擬機器的複本](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a35a6-113">If you want toocreate a copy of your existing Linux VM with its specialized state for backup or debugging, see [Create a copy of a Linux virtual machine running on Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="a35a6-114">如果您想 tooupload Linux VHD 從內部部署 VM，請參閱和[上傳並從自訂的磁碟映像建立 Linux VM](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a35a6-114">And if you want tooupload a Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="a35a6-115">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="a35a6-115">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="a35a6-116">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="a35a6-116">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="a35a6-117">[Azure CLI 1.0](#before-you-begin) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）</span><span class="sxs-lookup"><span data-stu-id="a35a6-117">[Azure CLI 1.0](#before-you-begin) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="a35a6-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -hello 資源管理部署模型我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="a35a6-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a35a6-119">開始之前</span><span class="sxs-lookup"><span data-stu-id="a35a6-119">Before you begin</span></span>
<span data-ttu-id="a35a6-120">請確定您符合下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="a35a6-120">Ensure that you meet hello following prerequisites:</span></span>

* <span data-ttu-id="a35a6-121">**Hello Resource Manager 部署模型中建立的 azure VM** -如果您尚未建立 Linux VM，您可以使用 hello[入口網站](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，hello [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，或[資源管理員範本](create-ssh-secured-vm-from-template.md)。</span><span class="sxs-lookup"><span data-stu-id="a35a6-121">**Azure VM created in hello Resource Manager deployment model** - If you haven't created a Linux VM, you can use hello [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> 
  
    <span data-ttu-id="a35a6-122">設定 VM，視 hello。</span><span class="sxs-lookup"><span data-stu-id="a35a6-122">Configure hello VM as needed.</span></span> <span data-ttu-id="a35a6-123">例如，[新增資料磁碟](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)、套用更新，並安裝應用程式。</span><span class="sxs-lookup"><span data-stu-id="a35a6-123">For example, [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), apply updates, and install applications.</span></span> 
* <span data-ttu-id="a35a6-124">**Azure CLI** -安裝 hello [Azure CLI](../../cli-install-nodejs.md)本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="a35a6-124">**Azure CLI** - Install hello [Azure CLI](../../cli-install-nodejs.md) on a local computer.</span></span>

## <a name="step-1-remove-hello-azure-linux-agent"></a><span data-ttu-id="a35a6-125">步驟 1： 移除 hello Azure Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="a35a6-125">Step 1: Remove hello Azure Linux agent</span></span>
<span data-ttu-id="a35a6-126">首先，執行 hello **waagent**命令與 hello**解除佈建**hello Linux VM 上的參數。</span><span class="sxs-lookup"><span data-stu-id="a35a6-126">First, run hello **waagent** command with hello **deprovision** parameter on hello Linux VM.</span></span> <span data-ttu-id="a35a6-127">此命令會刪除檔案和資料 toomake hello 準備好將一般化 VM。</span><span class="sxs-lookup"><span data-stu-id="a35a6-127">This command deletes files and data toomake hello VM ready for generalizing.</span></span> <span data-ttu-id="a35a6-128">如需詳細資訊，請參閱 hello [Azure Linux 代理程式使用者指南](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a35a6-128">For details, see hello [Azure Linux Agent user guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

1. <span data-ttu-id="a35a6-129">連接 tooyour 使用 SSH 用戶端的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="a35a6-129">Connect tooyour Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="a35a6-130">在 hello SSH 視窗中，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a35a6-130">In hello SSH window, type hello following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > <span data-ttu-id="a35a6-131">只有執行此命令在 VM 上的您想 toocapture 做為映像。</span><span class="sxs-lookup"><span data-stu-id="a35a6-131">Only run this command on a VM that you intend toocapture as an image.</span></span> <span data-ttu-id="a35a6-132">它並不保證清除所有的機密資訊的 hello 映像，或適用於轉散發。</span><span class="sxs-lookup"><span data-stu-id="a35a6-132">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution.</span></span>
 
3. <span data-ttu-id="a35a6-133">型別**y** toocontinue。</span><span class="sxs-lookup"><span data-stu-id="a35a6-133">Type **y** toocontinue.</span></span> <span data-ttu-id="a35a6-134">您可以新增 hello **-強制**參數 tooavoid 此確認步驟。</span><span class="sxs-lookup"><span data-stu-id="a35a6-134">You can add hello **-force** parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="a35a6-135">Hello 命令完成之後，請輸入**結束**。</span><span class="sxs-lookup"><span data-stu-id="a35a6-135">After hello command completes, type **exit**.</span></span> <span data-ttu-id="a35a6-136">此步驟會關閉 hello SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="a35a6-136">This step closes hello SSH client.</span></span>

## <a name="step-2-capture-hello-vm"></a><span data-ttu-id="a35a6-137">步驟 2： 擷取 hello VM</span><span class="sxs-lookup"><span data-stu-id="a35a6-137">Step 2: Capture hello VM</span></span>
<span data-ttu-id="a35a6-138">使用 hello Azure CLI toogeneralize，並擷取 hello VM。</span><span class="sxs-lookup"><span data-stu-id="a35a6-138">Use hello Azure CLI toogeneralize and capture hello VM.</span></span> <span data-ttu-id="a35a6-139">在 hello 下列範例中，會取代您自己的值的範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="a35a6-139">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="a35a6-140">範例參數名稱包含 **myResourceGroup**、**myVnet** 和 **myVM**。</span><span class="sxs-lookup"><span data-stu-id="a35a6-140">Example parameter names include **myResourceGroup**, **myVnet**, and **myVM**.</span></span>

1. <span data-ttu-id="a35a6-141">從本機電腦，開啟 hello Azure CLI 和[Azure 訂用帳戶的登入 tooyour](../../xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="a35a6-141">From your local computer, open hello Azure CLI and [login tooyour Azure subscription](../../xplat-cli-connect.md).</span></span> 
2. <span data-ttu-id="a35a6-142">確定您處於 Resource Manager 模式。</span><span class="sxs-lookup"><span data-stu-id="a35a6-142">Make sure you are in Resource Manager mode.</span></span>
   
    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="a35a6-143">關閉 VM，您已經解除佈建使用下列命令的 hello hello:</span><span class="sxs-lookup"><span data-stu-id="a35a6-143">Shut down hello VM that you already deprovisioned by using hello following command:</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. <span data-ttu-id="a35a6-144">一般化 hello VM 以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="a35a6-144">Generalize hello VM with hello following command:</span></span>
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. <span data-ttu-id="a35a6-145">現在執行 hello **azure vm 擷取**命令中，哪些擷取 hello VM。</span><span class="sxs-lookup"><span data-stu-id="a35a6-145">Now run hello **azure vm capture** command, which captures hello VM.</span></span> <span data-ttu-id="a35a6-146">在下列範例的 hello，hello 以擷取 Vhd 的映像名稱開頭**MyVHDNamePrefix**，和 hello **-t**選項指定路徑 toohello 範本**MyTemplate.json**.</span><span class="sxs-lookup"><span data-stu-id="a35a6-146">In hello following example, hello image VHDs are captured with names beginning with **MyVHDNamePrefix**, and hello **-t** option specifies a path toohello template **MyTemplate.json**.</span></span> 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > <span data-ttu-id="a35a6-147">根據預設，在使用 hello 原始 VM 的相同儲存體帳戶的 hello 建立 hello 映像的 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="a35a6-147">hello image VHD files get created by default in hello same storage account that hello original VM used.</span></span> <span data-ttu-id="a35a6-148">使用 hello*相同儲存體帳戶*toostore hello 任何新的 Vm，您建立從 hello 映像的 Vhd。</span><span class="sxs-lookup"><span data-stu-id="a35a6-148">Use hello *same storage account* toostore hello VHDs for any new VMs you create from hello image.</span></span> 

6. <span data-ttu-id="a35a6-149">擷取的映像，在文字編輯器中開啟 hello JSON 範本 toofind hello 位置。</span><span class="sxs-lookup"><span data-stu-id="a35a6-149">toofind hello location of a captured image, open hello JSON template in a text editor.</span></span> <span data-ttu-id="a35a6-150">在 hello **storageProfile**，尋找 hello **uri**的 hello**映像**位於 hello**系統**容器。</span><span class="sxs-lookup"><span data-stu-id="a35a6-150">In hello **storageProfile**, find hello **uri** of hello **image** located in hello **system** container.</span></span> <span data-ttu-id="a35a6-151">例如，hello hello OS 磁碟映像的 URI 太類似`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="a35a6-151">For example, hello URI of hello OS disk image is similar too`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>

## <a name="step-3-create-a-vm-from-hello-captured-image"></a><span data-ttu-id="a35a6-152">步驟 3： 從 hello 擷取映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="a35a6-152">Step 3: Create a VM from hello captured image</span></span>
<span data-ttu-id="a35a6-153">現在使用 hello 映像與範本 toocreate Linux VM。</span><span class="sxs-lookup"><span data-stu-id="a35a6-153">Now use hello image with a template toocreate a Linux VM.</span></span> <span data-ttu-id="a35a6-154">下列步驟顯示如何 toouse hello Azure CLI 和 hello 擷取 toocreate hello VM 在新的虛擬網路中的 JSON 檔案範本。</span><span class="sxs-lookup"><span data-stu-id="a35a6-154">These steps show you how toouse hello Azure CLI and hello JSON file template you captured toocreate hello VM in a new virtual network.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="a35a6-155">建立網路資源</span><span class="sxs-lookup"><span data-stu-id="a35a6-155">Create network resources</span></span>
<span data-ttu-id="a35a6-156">toouse hello 範本，您必須先設定虛擬網路和 NIC tooset 新的 vm。</span><span class="sxs-lookup"><span data-stu-id="a35a6-156">toouse hello template, you first need tooset up a virtual network and NIC for your new VM.</span></span> <span data-ttu-id="a35a6-157">我們建議您對這些資源的資源群組中建立 hello 儲存您的 VM 映像的位置。</span><span class="sxs-lookup"><span data-stu-id="a35a6-157">We recommend you create a resource group for these resources in hello location where your VM image is stored.</span></span> <span data-ttu-id="a35a6-158">執行命令之後，以取代您的資源和適當的 Azure 位置 (在這些命令中為"centralus") 的名稱類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="a35a6-158">Run commands similar toohello following, substituting names for your resources and an appropriate Azure location ("centralus" in these commands):</span></span>

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-hello-id-of-hello-nic"></a><span data-ttu-id="a35a6-159">取得 hello hello NIC 的識別碼</span><span class="sxs-lookup"><span data-stu-id="a35a6-159">Get hello Id of hello NIC</span></span>
<span data-ttu-id="a35a6-160">toodeploy 從使用儲存在擷取期間的 JSON hello hello 映像的 VM，您需要 hello 識別碼 hello nic。</span><span class="sxs-lookup"><span data-stu-id="a35a6-160">toodeploy a VM from hello image by using hello JSON you saved during capture, you need hello Id of hello NIC.</span></span> <span data-ttu-id="a35a6-161">取得此執行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="a35a6-161">Obtain it by running hello following command:</span></span>

```azurecli
azure network nic show myResourceGroup1 myNIC
```

<span data-ttu-id="a35a6-162">hello**識別碼**在 hello 的輸出是類似太`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span><span class="sxs-lookup"><span data-stu-id="a35a6-162">hello **Id** in hello output is similar too`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="a35a6-163">建立 VM</span><span class="sxs-lookup"><span data-stu-id="a35a6-163">Create a VM</span></span>
<span data-ttu-id="a35a6-164">現在執行的 hello 下列命令 toocreate hello 從 VM 會擷取 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="a35a6-164">Now run hello following command toocreate your VM from hello captured VM image.</span></span> <span data-ttu-id="a35a6-165">使用 hello **-f**參數 toospecify hello 路徑 toohello 範本 JSON 檔案儲存。</span><span class="sxs-lookup"><span data-stu-id="a35a6-165">Use hello **-f** parameter toospecify hello path toohello template JSON file you saved.</span></span>

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

<span data-ttu-id="a35a6-166">在 hello 命令輸出中，您提示的 toosupply 新的 VM 名稱、 hello 系統管理員使用者名稱和密碼，而且 hello hello NIC 您先前建立的識別碼。</span><span class="sxs-lookup"><span data-stu-id="a35a6-166">In hello command output, you are prompted toosupply a new VM name, hello admin user name and password, and hello Id of hello NIC you created previously.</span></span>

```bash
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

<span data-ttu-id="a35a6-167">hello 下列範例會顯示您成功部署請參閱：</span><span class="sxs-lookup"><span data-stu-id="a35a6-167">hello following sample shows what you see for a successful deployment:</span></span>

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment toocomplete
data:    DeploymentName     : MyDeployment
data:    ResourceGroupName  : MyResourceGroup1
data:    ProvisioningState  : Succeeded
data:    Timestamp          : xxxxxxx
data:    Mode               : Incremental
data:    Name                Type          Value

data:    ------------------  ------------  -------------------------------------

data:    vmName              String        myNewVM

data:    vmSize              String        Standard_D1

data:    adminUserName       String        myAdminuser

data:    adminPassword       SecureString  undefined

data:    networkInterfaceId  String        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
info:    group deployment create command OK
```

### <a name="verify-hello-deployment"></a><span data-ttu-id="a35a6-168">確認 hello 部署</span><span class="sxs-lookup"><span data-stu-id="a35a6-168">Verify hello deployment</span></span>
<span data-ttu-id="a35a6-169">現在 SSH toohello 建立虛擬機器您 tooverify hello 部署並開始使用 hello 新的 VM。</span><span class="sxs-lookup"><span data-stu-id="a35a6-169">Now SSH toohello virtual machine you created tooverify hello deployment and start using hello new VM.</span></span> <span data-ttu-id="a35a6-170">透過 SSH，tooconnect 尋找 hello 的 hello 您藉由執行下列命令的 hello 建立的 VM 的 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="a35a6-170">tooconnect via SSH, find hello IP address of hello VM you created by running hello following command:</span></span>

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

<span data-ttu-id="a35a6-171">hello 公用 IP 位址會列在 hello 命令輸出。</span><span class="sxs-lookup"><span data-stu-id="a35a6-171">hello public IP address is listed in hello command output.</span></span> <span data-ttu-id="a35a6-172">依預設，您會連接 toohello Linux VM 的 SSH 連接埠 22。</span><span class="sxs-lookup"><span data-stu-id="a35a6-172">By default you connect toohello Linux VM by SSH on port 22.</span></span>

## <a name="create-additional-vms"></a><span data-ttu-id="a35a6-173">建立額外的 VM</span><span class="sxs-lookup"><span data-stu-id="a35a6-173">Create additional VMs</span></span>
<span data-ttu-id="a35a6-174">使用 hello 擷取映像和範本 toodeploy 使用 hello 步驟 hello 前面一節中的其他 Vm。</span><span class="sxs-lookup"><span data-stu-id="a35a6-174">Use hello captured image and template toodeploy additional VMs using hello steps in hello preceding section.</span></span> <span data-ttu-id="a35a6-175">其他選項 toocreate Vm 從 hello 映像包括使用快速入門範本，或執行 hello **azure vm 建立**命令。</span><span class="sxs-lookup"><span data-stu-id="a35a6-175">Other options toocreate VMs from hello image include using a quickstart template or running hello **azure vm create** command.</span></span>

### <a name="use-hello-captured-template"></a><span data-ttu-id="a35a6-176">使用 hello 擷取的範本</span><span class="sxs-lookup"><span data-stu-id="a35a6-176">Use hello captured template</span></span>
<span data-ttu-id="a35a6-177">toouse hello 擷取映像和範本，請遵循下列步驟 （hello 前面一節中詳細說明）：</span><span class="sxs-lookup"><span data-stu-id="a35a6-177">toouse hello captured image and template, follow these steps (detailed in hello preceding section):</span></span>

* <span data-ttu-id="a35a6-178">請確認您的 VM 映像處於 hello 裝載 VM 的 VHD 的相同儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a35a6-178">Ensure that your VM image is in hello same storage account that hosts your VM's VHD.</span></span>
* <span data-ttu-id="a35a6-179">複製 hello 範本 JSON 檔案，並指定 hello hello 新 VM 的 VHD （或 Vhd） 的作業系統磁碟的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="a35a6-179">Copy hello template JSON file and specify a unique name for hello OS disk of hello new VM's VHD (or VHDs).</span></span> <span data-ttu-id="a35a6-180">例如，在 hello **storageProfile**下**vhd**，請在**uri**，指定唯一的名稱，如 hello **osDisk** VHD，類似太`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="a35a6-180">For example, in hello **storageProfile**, under **vhd**, in **uri**, specify a unique name for hello **osDisk** VHD, similar too`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>
* <span data-ttu-id="a35a6-181">相同或不同的虛擬網路，請在任一個 hello 中建立的 NIC。</span><span class="sxs-lookup"><span data-stu-id="a35a6-181">Create a NIC in either hello same or a different virtual network.</span></span>
* <span data-ttu-id="a35a6-182">使用修改的 hello 範本 JSON 檔案，在您設定虛擬網路的 hello hello 資源群組中建立的部署。</span><span class="sxs-lookup"><span data-stu-id="a35a6-182">Using hello modified template JSON file, create a deployment in hello resource group in which you set up hello virtual network.</span></span>

### <a name="use-a-quickstart-template"></a><span data-ttu-id="a35a6-183">使用快速入門範本</span><span class="sxs-lookup"><span data-stu-id="a35a6-183">Use a quickstart template</span></span>
<span data-ttu-id="a35a6-184">如果您想 hello 網路設定當您從自動建立 VM hello 映像，您可以在範本中指定這些資源。</span><span class="sxs-lookup"><span data-stu-id="a35a6-184">If you want hello network set up automatically when you create a VM from hello image, you can specify those resources in a template.</span></span> <span data-ttu-id="a35a6-185">例如，請參閱 hello [101 vm 從-使用者-映像範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image)從 GitHub。</span><span class="sxs-lookup"><span data-stu-id="a35a6-185">For example, see hello [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) from GitHub.</span></span> <span data-ttu-id="a35a6-186">此範本建立的 VM，您自訂映像和 hello 必要的虛擬網路、 公用 IP 位址，及 NIC 的資源。</span><span class="sxs-lookup"><span data-stu-id="a35a6-186">This template creates a VM from your custom image and hello necessary virtual network, public IP address, and NIC resources.</span></span> <span data-ttu-id="a35a6-187">在 hello Azure 入口網站中使用 hello 範本的逐步解說，請參閱[如何 toocreate 使用資源管理員範本的自訂映像中的虛擬機器](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/)。</span><span class="sxs-lookup"><span data-stu-id="a35a6-187">For a walkthrough of using hello template in hello Azure portal, see [How toocreate a virtual machine from a custom image using a Resource Manager template](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span></span>

### <a name="use-hello-azure-vm-create-command"></a><span data-ttu-id="a35a6-188">使用 hello azure vm 建立命令</span><span class="sxs-lookup"><span data-stu-id="a35a6-188">Use hello azure vm create command</span></span>
<span data-ttu-id="a35a6-189">通常它是最簡單的 toouse 資源管理員範本 toocreate 從 hello 映像的 VM。</span><span class="sxs-lookup"><span data-stu-id="a35a6-189">Usually it's easiest toouse a Resource Manager template toocreate a VM from hello image.</span></span> <span data-ttu-id="a35a6-190">不過，您可以在其中建立 hello VM*以命令方式*使用 hello **azure vm 建立**命令與 hello **-Q** (**-映像 urn**) 參數.</span><span class="sxs-lookup"><span data-stu-id="a35a6-190">However, you can create hello VM *imperatively* by using hello **azure vm create** command with hello **-Q** (**--image-urn**) parameter.</span></span> <span data-ttu-id="a35a6-191">如果您使用此方法時，您也可以傳遞 hello **-d** (**-os-磁碟 vhd**) hello OS.vhd 檔案的參數 toospecify hello 位置 hello 新的 VM。</span><span class="sxs-lookup"><span data-stu-id="a35a6-191">If you use this method, you also pass hello **-d** (**--os-disk-vhd**) parameter toospecify hello location of hello OS .vhd file for hello new VM.</span></span> <span data-ttu-id="a35a6-192">這個檔案必須在 hello hello hello 映像的 VHD 檔案所在的儲存體帳戶的 vhd 容器中。</span><span class="sxs-lookup"><span data-stu-id="a35a6-192">This file must be in hello vhds container of hello storage account where hello image VHD file is stored.</span></span> <span data-ttu-id="a35a6-193">hello 命令複製 VHD hello hello 新的 VM 會自動 toohello **vhd**容器。</span><span class="sxs-lookup"><span data-stu-id="a35a6-193">hello command copies hello VHD for hello new VM automatically toohello **vhds** container.</span></span>

<span data-ttu-id="a35a6-194">執行前**azure vm 建立**hello 映像，以完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a35a6-194">Before running **azure vm create** with hello image, complete hello following steps:</span></span>

1. <span data-ttu-id="a35a6-195">建立資源群組，或識別 hello 部署現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a35a6-195">Create a resource group, or identify an existing resource group for hello deployment.</span></span>
2. <span data-ttu-id="a35a6-196">建立公用 IP 位址資源和 NIC 資源 hello 新的 VM。</span><span class="sxs-lookup"><span data-stu-id="a35a6-196">Create a public IP address resource and a NIC resource for hello new VM.</span></span> <span data-ttu-id="a35a6-197">如步驟 toocreate 的虛擬網路、 公用 IP 位址和 NIC 使用 hello CLI，請參閱稍早在本文中。</span><span class="sxs-lookup"><span data-stu-id="a35a6-197">For steps toocreate a virtual network, public IP address, and NIC by using hello CLI, see earlier in this article.</span></span> <span data-ttu-id="a35a6-198">(**azure vm 建立**也可以建立 NIC，但您需要為虛擬網路和子網路的 toopass 其他參數。)</span><span class="sxs-lookup"><span data-stu-id="a35a6-198">(**azure vm create** can also create a NIC, but you need toopass additional parameters for a virtual network and subnet.)</span></span>

<span data-ttu-id="a35a6-199">然後執行可將 Uri 傳遞 tooboth hello 新作業系統的 VHD 檔案，並 hello 現有映像的命令。</span><span class="sxs-lookup"><span data-stu-id="a35a6-199">Then run a command that passes URIs tooboth hello new OS VHD file and hello existing image.</span></span> <span data-ttu-id="a35a6-200">在此範例中，大小 Standard_A1 VM 建立 hello 美東地區。</span><span class="sxs-lookup"><span data-stu-id="a35a6-200">In this example, a size Standard_A1 VM is created in hello East US region.</span></span>

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

<span data-ttu-id="a35a6-201">如需其他命令選項，請執行 `azure help vm create`。</span><span class="sxs-lookup"><span data-stu-id="a35a6-201">For additional command options, run `azure help vm create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a35a6-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a35a6-202">Next steps</span></span>
<span data-ttu-id="a35a6-203">toomanage Vm 以 hello CLI，請參閱中的 hello 工作[部署和管理虛擬機器使用的 Azure Resource Manager 範本和 hello Azure CLI](create-ssh-secured-vm-from-template.md)。</span><span class="sxs-lookup"><span data-stu-id="a35a6-203">toomanage your VMs with hello CLI, see hello tasks in [Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI](create-ssh-secured-vm-from-template.md).</span></span>

