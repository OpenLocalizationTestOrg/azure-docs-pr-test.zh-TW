---
title: "擷取 Azure Linux VM 作為範本使用 | Microsoft Docs"
description: "了解如何擷取以 Azure Resource Manager 部署模型建立的以 Linux 為基礎之 Azure 虛擬機器 (VM) 的映像，並將它一般化。"
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
ms.openlocfilehash: b1164fbd816eea5189786850f096438e32f8f802
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a><span data-ttu-id="72b2b-103">擷取在 Azure 上執行的 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="72b2b-103">Capture a Linux virtual machine running on Azure</span></span>
<span data-ttu-id="72b2b-104">請遵循本文中的步驟，在 Resource Manager 部署模型中一般化和擷取 Azure Linux 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="72b2b-104">Follow the steps in this article to generalize and capture your Azure Linux virtual machine (VM) in the Resource Manager deployment model.</span></span> <span data-ttu-id="72b2b-105">當您一般化 VM 時，需移除個人帳戶資訊，並準備要做為映像的 VM。</span><span class="sxs-lookup"><span data-stu-id="72b2b-105">When you generalize the VM, you remove personal account information and prepare the VM to be used as an image.</span></span> <span data-ttu-id="72b2b-106">您接著擷取作業系統的一般化虛擬硬碟 (VHD) 映像、連接資料磁碟的 VHD 以及新 VM 部署的 [Resource Manager 範本](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="72b2b-106">You then capture a generalized virtual hard disk (VHD) image for the OS, VHDs for attached data disks, and a [Resource Manager template](../../azure-resource-manager/resource-group-overview.md) for new VM deployments.</span></span> <span data-ttu-id="72b2b-107">本文詳細說明如何針對使用非受控磁碟的 VM，透過 Azure CLI 1.0 擷取 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="72b2b-107">This article details how to capture a VM image with the Azure CLI 1.0 for a VM using unmanaged disks.</span></span> <span data-ttu-id="72b2b-108">您也可以[透過 Azure CLI 2.0 使用 Azure 受控磁碟擷取 VM](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="72b2b-108">You can also [capture a VM using Azure Managed Disks with the Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="72b2b-109">受控磁碟是由 Azure 平台處理，不需要任何準備或位置來儲存它們。</span><span class="sxs-lookup"><span data-stu-id="72b2b-109">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="72b2b-110">如需詳細資訊，請參閱 [Azure 受控磁碟概觀](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="72b2b-110">For more information, see [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="72b2b-111">若要使用映像建立 VM、針對每個新的 VM 設定網路資源，並使用範本 (JavaScript 物件標記法 (亦稱為 JSON) 檔案) 從擷取的 VHD 映像部署它。</span><span class="sxs-lookup"><span data-stu-id="72b2b-111">To create VMs using the image, set up network resources for each new VM, and use the template (a JavaScript Object Notation, or JSON, file) to deploy it from the captured VHD images.</span></span> <span data-ttu-id="72b2b-112">如此一來，您可以使用 VM 目前軟體的組態來複寫 VM，與您在 Azure Marketplace 中使用映像的方式類似。</span><span class="sxs-lookup"><span data-stu-id="72b2b-112">In this way, you can replicate a VM with its current software configuration, similar to the way you use images in the Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="72b2b-113">如果您想要建立一份您現有 Linux VM 的複本，當中包含其特殊的備份或偵錯狀態，請參閱[建立在 Azure 上執行的 Linux 虛擬機器複本](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="72b2b-113">If you want to create a copy of your existing Linux VM with its specialized state for backup or debugging, see [Create a copy of a Linux virtual machine running on Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="72b2b-114">如果您想要從內部部署 VM 上傳 Linux VHD，請參閱[上傳自訂磁碟映像並從這個映像建立 Linux VM](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="72b2b-114">And if you want to upload a Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="72b2b-115">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="72b2b-115">CLI versions to complete the task</span></span>
<span data-ttu-id="72b2b-116">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="72b2b-116">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="72b2b-117">[Azure CLI 1.0](#before-you-begin) – 適用於傳統和資源管理部署模型的 CLI (本文章)</span><span class="sxs-lookup"><span data-stu-id="72b2b-117">[Azure CLI 1.0](#before-you-begin) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="72b2b-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - 適用於資源管理部署模型的新一代 CLI</span><span class="sxs-lookup"><span data-stu-id="72b2b-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="72b2b-119">開始之前</span><span class="sxs-lookup"><span data-stu-id="72b2b-119">Before you begin</span></span>
<span data-ttu-id="72b2b-120">請確保符合下列必要條件︰</span><span class="sxs-lookup"><span data-stu-id="72b2b-120">Ensure that you meet the following prerequisites:</span></span>

* <span data-ttu-id="72b2b-121">**在 Resource Manager 部署模型中建立的 Azure VM** - 如果您尚未建立 Linux VM，可以使用[入口網站](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)、[Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 或 [Resource Manager 範本](create-ssh-secured-vm-from-template.md)。</span><span class="sxs-lookup"><span data-stu-id="72b2b-121">**Azure VM created in the Resource Manager deployment model** - If you haven't created a Linux VM, you can use the [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), the [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> 
  
    <span data-ttu-id="72b2b-122">視需要設定 VM。</span><span class="sxs-lookup"><span data-stu-id="72b2b-122">Configure the VM as needed.</span></span> <span data-ttu-id="72b2b-123">例如，[新增資料磁碟](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)、套用更新，並安裝應用程式。</span><span class="sxs-lookup"><span data-stu-id="72b2b-123">For example, [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), apply updates, and install applications.</span></span> 
* <span data-ttu-id="72b2b-124">**Azure CLI** - 在本機電腦上安裝 [Azure CLI](../../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="72b2b-124">**Azure CLI** - Install the [Azure CLI](../../cli-install-nodejs.md) on a local computer.</span></span>

## <a name="step-1-remove-the-azure-linux-agent"></a><span data-ttu-id="72b2b-125">步驟 1：移除 Azure Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="72b2b-125">Step 1: Remove the Azure Linux agent</span></span>
<span data-ttu-id="72b2b-126">首先，在 Linux VM 上執行 **waagent** 命令並搭配 **deprovision**參數。</span><span class="sxs-lookup"><span data-stu-id="72b2b-126">First, run the **waagent** command with the **deprovision** parameter on the Linux VM.</span></span> <span data-ttu-id="72b2b-127">此命令會刪除檔案與資料，使 VM 準備好進行一般化。</span><span class="sxs-lookup"><span data-stu-id="72b2b-127">This command deletes files and data to make the VM ready for generalizing.</span></span> <span data-ttu-id="72b2b-128">如需詳細資訊，請參閱 [Azure Linux 代理程式使用者指南](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="72b2b-128">For details, see the [Azure Linux Agent user guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

1. <span data-ttu-id="72b2b-129">使用 SSH 用戶端連線到 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="72b2b-129">Connect to your Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="72b2b-130">在 SSH 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="72b2b-130">In the SSH window, type the following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > <span data-ttu-id="72b2b-131">只在您想要擷取作為映像的 VM 上執行這個命令。</span><span class="sxs-lookup"><span data-stu-id="72b2b-131">Only run this command on a VM that you intend to capture as an image.</span></span> <span data-ttu-id="72b2b-132">這不能保證映像檔中的所有機密資訊都會清除完畢或適合轉散發。</span><span class="sxs-lookup"><span data-stu-id="72b2b-132">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution.</span></span>
 
3. <span data-ttu-id="72b2b-133">輸入 **y** 繼續。</span><span class="sxs-lookup"><span data-stu-id="72b2b-133">Type **y** to continue.</span></span> <span data-ttu-id="72b2b-134">您可以加入 **-force** 參數，便不用進行此確認步驟。</span><span class="sxs-lookup"><span data-stu-id="72b2b-134">You can add the **-force** parameter to avoid this confirmation step.</span></span>
4. <span data-ttu-id="72b2b-135">在命令完成之後，請輸入 **exit**。</span><span class="sxs-lookup"><span data-stu-id="72b2b-135">After the command completes, type **exit**.</span></span> <span data-ttu-id="72b2b-136">此步驟會關閉 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="72b2b-136">This step closes the SSH client.</span></span>

## <a name="step-2-capture-the-vm"></a><span data-ttu-id="72b2b-137">步驟 2：擷取 VM</span><span class="sxs-lookup"><span data-stu-id="72b2b-137">Step 2: Capture the VM</span></span>
<span data-ttu-id="72b2b-138">使用 Azure CLI 來一般化和擷取 VM。</span><span class="sxs-lookup"><span data-stu-id="72b2b-138">Use the Azure CLI to generalize and capture the VM.</span></span> <span data-ttu-id="72b2b-139">在下列範例中，請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="72b2b-139">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="72b2b-140">範例參數名稱包含 **myResourceGroup**、**myVnet** 和 **myVM**。</span><span class="sxs-lookup"><span data-stu-id="72b2b-140">Example parameter names include **myResourceGroup**, **myVnet**, and **myVM**.</span></span>

1. <span data-ttu-id="72b2b-141">從本機電腦，開啟 Azure CLI 並[登入您的 Azure 訂用帳戶](../../xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="72b2b-141">From your local computer, open the Azure CLI and [login to your Azure subscription](../../xplat-cli-connect.md).</span></span> 
2. <span data-ttu-id="72b2b-142">確定您處於 Resource Manager 模式。</span><span class="sxs-lookup"><span data-stu-id="72b2b-142">Make sure you are in Resource Manager mode.</span></span>
   
    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="72b2b-143">使用下列命令，關閉您已經解除佈建的 VM：</span><span class="sxs-lookup"><span data-stu-id="72b2b-143">Shut down the VM that you already deprovisioned by using the following command:</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. <span data-ttu-id="72b2b-144">使用下列命令將 VM 一般化：</span><span class="sxs-lookup"><span data-stu-id="72b2b-144">Generalize the VM with the following command:</span></span>
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. <span data-ttu-id="72b2b-145">現在執行 **azure vm capture** 命令，它會擷取 VM。</span><span class="sxs-lookup"><span data-stu-id="72b2b-145">Now run the **azure vm capture** command, which captures the VM.</span></span> <span data-ttu-id="72b2b-146">在下列範例中，會使用開頭為 **MyVHDNamePrefix** 的名稱來擷取映像 VHD，而 **-t** 選項會指定範本 **MyTemplate.json** 的路徑。</span><span class="sxs-lookup"><span data-stu-id="72b2b-146">In the following example, the image VHDs are captured with names beginning with **MyVHDNamePrefix**, and the **-t** option specifies a path to the template **MyTemplate.json**.</span></span> 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > <span data-ttu-id="72b2b-147">在原始 VM 使用的相同儲存體帳戶中預設會建立映像 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="72b2b-147">The image VHD files get created by default in the same storage account that the original VM used.</span></span> <span data-ttu-id="72b2b-148">使用相同儲存體帳戶來儲存從映像建立之所有新 VM 的 VHD。</span><span class="sxs-lookup"><span data-stu-id="72b2b-148">Use the *same storage account* to store the VHDs for any new VMs you create from the image.</span></span> 

6. <span data-ttu-id="72b2b-149">若要尋找擷取之映像的位置，請在文字編輯器中開啟 JSON 範本。</span><span class="sxs-lookup"><span data-stu-id="72b2b-149">To find the location of a captured image, open the JSON template in a text editor.</span></span> <span data-ttu-id="72b2b-150">在 **storageProfile** 中，尋找位於 **system** 容器的**映像**的 **uri**。</span><span class="sxs-lookup"><span data-stu-id="72b2b-150">In the **storageProfile**, find the **uri** of the **image** located in the **system** container.</span></span> <span data-ttu-id="72b2b-151">例如，OS 磁碟映像的 URI 類似於 `https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="72b2b-151">For example, the URI of the OS disk image is similar to `https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>

## <a name="step-3-create-a-vm-from-the-captured-image"></a><span data-ttu-id="72b2b-152">步驟 3：從擷取的映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="72b2b-152">Step 3: Create a VM from the captured image</span></span>
<span data-ttu-id="72b2b-153">現在使用具有範本的映像來建立 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="72b2b-153">Now use the image with a template to create a Linux VM.</span></span> <span data-ttu-id="72b2b-154">下列步驟示範如何使用您擷取的 Azure CLI 和 JSON 檔案範本，在新的虛擬網路中建立 VM。</span><span class="sxs-lookup"><span data-stu-id="72b2b-154">These steps show you how to use the Azure CLI and the JSON file template you captured to create the VM in a new virtual network.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="72b2b-155">建立網路資源</span><span class="sxs-lookup"><span data-stu-id="72b2b-155">Create network resources</span></span>
<span data-ttu-id="72b2b-156">若要使用範本，您必須先為新的 VM 設定虛擬網路和 NIC。</span><span class="sxs-lookup"><span data-stu-id="72b2b-156">To use the template, you first need to set up a virtual network and NIC for your new VM.</span></span> <span data-ttu-id="72b2b-157">建議您在儲存 VM 映像的位置中，為這些資源建立一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="72b2b-157">We recommend you create a resource group for these resources in the location where your VM image is stored.</span></span> <span data-ttu-id="72b2b-158">執行類似下列的命令，替換您的資源名稱和適當的 Azure 位置 (在這些命令列中為 "centralus")：</span><span class="sxs-lookup"><span data-stu-id="72b2b-158">Run commands similar to the following, substituting names for your resources and an appropriate Azure location ("centralus" in these commands):</span></span>

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-the-id-of-the-nic"></a><span data-ttu-id="72b2b-159">取得 NIC 的識別碼</span><span class="sxs-lookup"><span data-stu-id="72b2b-159">Get the Id of the NIC</span></span>
<span data-ttu-id="72b2b-160">若要使用您在擷取期間所儲存的 JSON，從映像部署 VM，您需要 NIC 的識別碼。</span><span class="sxs-lookup"><span data-stu-id="72b2b-160">To deploy a VM from the image by using the JSON you saved during capture, you need the Id of the NIC.</span></span> <span data-ttu-id="72b2b-161">執行下列命令來取得識別碼：</span><span class="sxs-lookup"><span data-stu-id="72b2b-161">Obtain it by running the following command:</span></span>

```azurecli
azure network nic show myResourceGroup1 myNIC
```

<span data-ttu-id="72b2b-162">輸出中的**識別碼**類似於 `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span><span class="sxs-lookup"><span data-stu-id="72b2b-162">The **Id** in the output is similar to `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="72b2b-163">建立 VM</span><span class="sxs-lookup"><span data-stu-id="72b2b-163">Create a VM</span></span>
<span data-ttu-id="72b2b-164">現在執行下列命令，從擷取的 VM 映像建立 VM。</span><span class="sxs-lookup"><span data-stu-id="72b2b-164">Now run the following command to create your VM from the captured VM image.</span></span> <span data-ttu-id="72b2b-165">使用 **-f** 參數來指定您所儲存之範本 JSON 檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="72b2b-165">Use the **-f** parameter to specify the path to the template JSON file you saved.</span></span>

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

<span data-ttu-id="72b2b-166">在命令輸出中，系統會提示您提供新的 VM 名稱、系統管理員使用者名稱和密碼，以及您先前建立的 NIC 識別碼。</span><span class="sxs-lookup"><span data-stu-id="72b2b-166">In the command output, you are prompted to supply a new VM name, the admin user name and password, and the Id of the NIC you created previously.</span></span>

```bash
info:    Executing command group deployment create
info:    Supply values for the following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

<span data-ttu-id="72b2b-167">下列範例會顯示您成功部署後所看到的內容︰</span><span class="sxs-lookup"><span data-stu-id="72b2b-167">The following sample shows what you see for a successful deployment:</span></span>

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment to complete
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

### <a name="verify-the-deployment"></a><span data-ttu-id="72b2b-168">驗證部署</span><span class="sxs-lookup"><span data-stu-id="72b2b-168">Verify the deployment</span></span>
<span data-ttu-id="72b2b-169">現在使用您建立的虛擬機器的 SSH 來驗證部署並開始使用新的 VM。</span><span class="sxs-lookup"><span data-stu-id="72b2b-169">Now SSH to the virtual machine you created to verify the deployment and start using the new VM.</span></span> <span data-ttu-id="72b2b-170">若要透過 SSH 連接，請尋找您藉由執行下列命令所建立的 VM 的 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="72b2b-170">To connect via SSH, find the IP address of the VM you created by running the following command:</span></span>

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

<span data-ttu-id="72b2b-171">公用 IP 位址會列在命令輸出中。</span><span class="sxs-lookup"><span data-stu-id="72b2b-171">The public IP address is listed in the command output.</span></span> <span data-ttu-id="72b2b-172">根據預設，您會經由連接埠 22 上的 SSH 連接到 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="72b2b-172">By default you connect to the Linux VM by SSH on port 22.</span></span>

## <a name="create-additional-vms"></a><span data-ttu-id="72b2b-173">建立額外的 VM</span><span class="sxs-lookup"><span data-stu-id="72b2b-173">Create additional VMs</span></span>
<span data-ttu-id="72b2b-174">依照前一節中的步驟，使用擷取的映像和範本來部署其他 VM。</span><span class="sxs-lookup"><span data-stu-id="72b2b-174">Use the captured image and template to deploy additional VMs using the steps in the preceding section.</span></span> <span data-ttu-id="72b2b-175">從映像建立 VM 的其他選項包括使用快速入門範本，或執行 **azure vm create** 命令。</span><span class="sxs-lookup"><span data-stu-id="72b2b-175">Other options to create VMs from the image include using a quickstart template or running the **azure vm create** command.</span></span>

### <a name="use-the-captured-template"></a><span data-ttu-id="72b2b-176">使用擷取的範本</span><span class="sxs-lookup"><span data-stu-id="72b2b-176">Use the captured template</span></span>
<span data-ttu-id="72b2b-177">若要使用擷取的映像和範本，請遵循下列步驟 (上一節中詳細說明)︰</span><span class="sxs-lookup"><span data-stu-id="72b2b-177">To use the captured image and template, follow these steps (detailed in the preceding section):</span></span>

* <span data-ttu-id="72b2b-178">確保您的 VM 映像位於裝載 VM 之 VHD 的相同儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="72b2b-178">Ensure that your VM image is in the same storage account that hosts your VM's VHD.</span></span>
* <span data-ttu-id="72b2b-179">複製範本 JSON 檔案，並指定新 VM 的 VHD (或 VHDs) 作業系統磁碟的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="72b2b-179">Copy the template JSON file and specify a unique name for the OS disk of the new VM's VHD (or VHDs).</span></span> <span data-ttu-id="72b2b-180">例如，在 **storageProfile** 的 **vhd** 下，於 **uri** 中，指定 **osDisk** VHD 的唯一名稱，類似於 `https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="72b2b-180">For example, in the **storageProfile**, under **vhd**, in **uri**, specify a unique name for the **osDisk** VHD, similar to `https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>
* <span data-ttu-id="72b2b-181">在相同或不同的虛擬網路中建立 NIC。</span><span class="sxs-lookup"><span data-stu-id="72b2b-181">Create a NIC in either the same or a different virtual network.</span></span>
* <span data-ttu-id="72b2b-182">使用修改過的範本 JSON 檔案，在您設定虛擬網路的資源群組中建立部署。</span><span class="sxs-lookup"><span data-stu-id="72b2b-182">Using the modified template JSON file, create a deployment in the resource group in which you set up the virtual network.</span></span>

### <a name="use-a-quickstart-template"></a><span data-ttu-id="72b2b-183">使用快速入門範本</span><span class="sxs-lookup"><span data-stu-id="72b2b-183">Use a quickstart template</span></span>
<span data-ttu-id="72b2b-184">如果您要在從映像建立 VM 時自動設定網路，可以在範本中指定這些資源。</span><span class="sxs-lookup"><span data-stu-id="72b2b-184">If you want the network set up automatically when you create a VM from the image, you can specify those resources in a template.</span></span> <span data-ttu-id="72b2b-185">例如，請從 GitHub 參閱 [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image)。</span><span class="sxs-lookup"><span data-stu-id="72b2b-185">For example, see the [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) from GitHub.</span></span> <span data-ttu-id="72b2b-186">此範本會從自訂映像和必要的虛擬網路、公用 IP 位址和 NIC 資源建立 VM。</span><span class="sxs-lookup"><span data-stu-id="72b2b-186">This template creates a VM from your custom image and the necessary virtual network, public IP address, and NIC resources.</span></span> <span data-ttu-id="72b2b-187">如需在 Azure 入口網站中使用範本的逐步解說，請參閱 [如何從使用 Resource Manager 範本的自訂映像建立虛擬機器](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/)。</span><span class="sxs-lookup"><span data-stu-id="72b2b-187">For a walkthrough of using the template in the Azure portal, see [How to create a virtual machine from a custom image using a Resource Manager template](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span></span>

### <a name="use-the-azure-vm-create-command"></a><span data-ttu-id="72b2b-188">使用 azure vm create 命令</span><span class="sxs-lookup"><span data-stu-id="72b2b-188">Use the azure vm create command</span></span>
<span data-ttu-id="72b2b-189">通常最簡單的方式是使用 Resource Manager 範本從映像建立 VM。</span><span class="sxs-lookup"><span data-stu-id="72b2b-189">Usually it's easiest to use a Resource Manager template to create a VM from the image.</span></span> <span data-ttu-id="72b2b-190">不過，您可以使用 **azure vm create** 命令搭配 **-Q** (**--image-urn**) 參數，以*「命令方式」*建立 VM。</span><span class="sxs-lookup"><span data-stu-id="72b2b-190">However, you can create the VM *imperatively* by using the **azure vm create** command with the **-Q** (**--image-urn**) parameter.</span></span> <span data-ttu-id="72b2b-191">如果您使用此方法，您也要傳遞 **-d** (**--os-disk-vhd**) 參數來指定新 VM 的 OS .vhd 檔案位置。</span><span class="sxs-lookup"><span data-stu-id="72b2b-191">If you use this method, you also pass the **-d** (**--os-disk-vhd**) parameter to specify the location of the OS .vhd file for the new VM.</span></span> <span data-ttu-id="72b2b-192">此檔案必須位於儲存映像 VHD 檔案之儲存體帳戶的 vhds 容器中。</span><span class="sxs-lookup"><span data-stu-id="72b2b-192">This file must be in the vhds container of the storage account where the image VHD file is stored.</span></span> <span data-ttu-id="72b2b-193">此命令會自動將新 VM 的 VHD 複製到 **vhds** 容器。</span><span class="sxs-lookup"><span data-stu-id="72b2b-193">The command copies the VHD for the new VM automatically to the **vhds** container.</span></span>

<span data-ttu-id="72b2b-194">對映像執行 **azure vm create** 之前，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="72b2b-194">Before running **azure vm create** with the image, complete the following steps:</span></span>

1. <span data-ttu-id="72b2b-195">建立資源群組，或識別現有的資源群組以供部署。</span><span class="sxs-lookup"><span data-stu-id="72b2b-195">Create a resource group, or identify an existing resource group for the deployment.</span></span>
2. <span data-ttu-id="72b2b-196">為新的 VM 建立公用 IP 位址資源和 NIC 資源。</span><span class="sxs-lookup"><span data-stu-id="72b2b-196">Create a public IP address resource and a NIC resource for the new VM.</span></span> <span data-ttu-id="72b2b-197">如需使用 CLI 建立虛擬網路、公用 IP 位址及 NIC 的步驟，請參閱在本文中先前的說明。</span><span class="sxs-lookup"><span data-stu-id="72b2b-197">For steps to create a virtual network, public IP address, and NIC by using the CLI, see earlier in this article.</span></span> <span data-ttu-id="72b2b-198">(**azure vm create** 也可以建立 NIC，但您需要傳遞其他參數以取得虛擬網路和子網路。)</span><span class="sxs-lookup"><span data-stu-id="72b2b-198">(**azure vm create** can also create a NIC, but you need to pass additional parameters for a virtual network and subnet.)</span></span>

<span data-ttu-id="72b2b-199">然後，執行將 URI 傳遞給新 OS VHD 檔案和現有映像的命令。</span><span class="sxs-lookup"><span data-stu-id="72b2b-199">Then run a command that passes URIs to both the new OS VHD file and the existing image.</span></span> <span data-ttu-id="72b2b-200">在此範例中，會在美國東部地區建立 Standard_A1 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="72b2b-200">In this example, a size Standard_A1 VM is created in the East US region.</span></span>

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

<span data-ttu-id="72b2b-201">如需其他命令選項，請執行 `azure help vm create`。</span><span class="sxs-lookup"><span data-stu-id="72b2b-201">For additional command options, run `azure help vm create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72b2b-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="72b2b-202">Next steps</span></span>
<span data-ttu-id="72b2b-203">若要使用 CIL 管理 VM，請參閱 [使用 Azure 資源管理員範本和 Azure CLI 部署和管理虛擬機器](create-ssh-secured-vm-from-template.md)中的工作。</span><span class="sxs-lookup"><span data-stu-id="72b2b-203">To manage your VMs with the CLI, see the tasks in [Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI](create-ssh-secured-vm-from-template.md).</span></span>

