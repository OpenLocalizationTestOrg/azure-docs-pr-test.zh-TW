---
title: "使用 CLI 2.0 在 Azure 中擷取 Linux VM 的映像 | Microsoft Docs"
description: "使用 Azure CLI 2.0 擷取要用於大型部署的 Azure VM 映像。"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: 19b573f77f2ee84600955d00d30bdb16c84e3623
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-create-an-image-of-a-virtual-machine-or-vhd"></a><span data-ttu-id="659b3-103">如何建立虛擬機器或 VHD 的映像</span><span class="sxs-lookup"><span data-stu-id="659b3-103">How to create an image of a virtual machine or VHD</span></span>

<!-- generalize, image - extended version of the tutorial-->

<span data-ttu-id="659b3-104">若要建立虛擬機器 (VM) 的多個複本以在 Azure 中使用，請擷取 VM 或 OS VHD 的映像。</span><span class="sxs-lookup"><span data-stu-id="659b3-104">To create multiple copies of a virtual machine (VM) to use in Azure, capture an image of the VM or the OS VHD.</span></span> <span data-ttu-id="659b3-105">若要建立映像，您必須將個人的帳戶資訊移除，使多次部署更安全。</span><span class="sxs-lookup"><span data-stu-id="659b3-105">To create an image, you need remove personal account information which makes it safer to deploy multiple times.</span></span> <span data-ttu-id="659b3-106">在下列步驟中，您將取消佈建現有的 VM、解除配置，然後建立映像。</span><span class="sxs-lookup"><span data-stu-id="659b3-106">In the following steps you deprovision an existing VM, deallocate and create an image.</span></span> <span data-ttu-id="659b3-107">您可以使用此映像，在您訂用帳戶的任何資源群組中建立 VM。</span><span class="sxs-lookup"><span data-stu-id="659b3-107">You can use this image to create VMs across any resource group within your subscription.</span></span>

<span data-ttu-id="659b3-108">如果您想要建立一份現有 Linux VM 的副本以進行備份或偵錯，或是從內部部署 VM 上傳特定的 Linux VHD，請參閱[從自訂的磁碟映像上傳及建立 Linux VM](upload-vhd.md)。</span><span class="sxs-lookup"><span data-stu-id="659b3-108">If you want to create a copy of your existing Linux VM for backup or debugging, or upload a specialized Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md).</span></span>  

<span data-ttu-id="659b3-109">您也可以使用 **Packer** 建立您的自訂設定。</span><span class="sxs-lookup"><span data-stu-id="659b3-109">You can also use **Packer** to create your custom configuration.</span></span> <span data-ttu-id="659b3-110">如需有關使用 Packer 的詳細資訊，請參閱[如何在 Azure 中使用 Packer 來建立 Linux 虛擬機器映像](build-image-with-packer.md)。</span><span class="sxs-lookup"><span data-stu-id="659b3-110">For more information on using Packer, see [How to use Packer to create Linux virtual machine images in Azure](build-image-with-packer.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="659b3-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="659b3-111">Before you begin</span></span>
<span data-ttu-id="659b3-112">請確保符合下列必要條件︰</span><span class="sxs-lookup"><span data-stu-id="659b3-112">Ensure that you meet the following prerequisites:</span></span>

* <span data-ttu-id="659b3-113">您需要在 Resource Manager 部署模型中使用受管理磁碟建立的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="659b3-113">You need an Azure VM created in the Resource Manager deployment model using managed disks.</span></span> <span data-ttu-id="659b3-114">如果您尚未建立 Linux VM，可以使用[入口網站](quick-create-portal.md)、[Azure CLI](quick-create-cli.md) 或 [Resource Manager 範本](create-ssh-secured-vm-from-template.md)。</span><span class="sxs-lookup"><span data-stu-id="659b3-114">If you haven't created a Linux VM, you can use the [portal](quick-create-portal.md), the [Azure CLI](quick-create-cli.md), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> <span data-ttu-id="659b3-115">視需要設定 VM。</span><span class="sxs-lookup"><span data-stu-id="659b3-115">Configure the VM as needed.</span></span> <span data-ttu-id="659b3-116">例如，[新增資料磁碟](add-disk.md)、套用更新，並安裝應用程式。</span><span class="sxs-lookup"><span data-stu-id="659b3-116">For example, [add data disks](add-disk.md), apply updates, and install applications.</span></span> 

* <span data-ttu-id="659b3-117">您還需要安裝最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2)，並使用 [az login](/cli/azure/#login) 來登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="659b3-117">You also need to have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and be logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="659b3-118">快速命令</span><span class="sxs-lookup"><span data-stu-id="659b3-118">Quick commands</span></span>

<span data-ttu-id="659b3-119">如需本主題的簡化版本，以進行測試、評估或深入了解 Azure 中的 VM，請參閱[使用 CLI 建立 Azure VM 的自訂映像](tutorial-custom-images.md)。</span><span class="sxs-lookup"><span data-stu-id="659b3-119">For a simplified version of this topic, for testing, evaluating or learning about VMs in Azure, see [Create a custom image of an Azure VM using the CLI](tutorial-custom-images.md).</span></span>


## <a name="step-1-deprovision-the-vm"></a><span data-ttu-id="659b3-120">步驟 1：取消佈建 VM</span><span class="sxs-lookup"><span data-stu-id="659b3-120">Step 1: Deprovision the VM</span></span>
<span data-ttu-id="659b3-121">使用 Azure VM 代理程式來取消佈建 VM，以將電腦特定的檔案和資料刪除。</span><span class="sxs-lookup"><span data-stu-id="659b3-121">You deprovision the VM, using the Azure VM agent, to delete machine specific files and data.</span></span> <span data-ttu-id="659b3-122">在來源 Linux VM 上使用 `waagent` 命令搭配 -deprovision+user 參數。</span><span class="sxs-lookup"><span data-stu-id="659b3-122">Use the `waagent` command with the *-deprovision+user* parameter on your source Linux VM.</span></span> <span data-ttu-id="659b3-123">如需詳細資訊，請參閱 [Azure Linux 代理程式使用者指南](../windows/agent-user-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="659b3-123">For more information, see the [Azure Linux Agent user guide](../windows/agent-user-guide.md).</span></span>

1. <span data-ttu-id="659b3-124">使用 SSH 用戶端連線到 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="659b3-124">Connect to your Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="659b3-125">在 SSH 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="659b3-125">In the SSH window, type the following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > <span data-ttu-id="659b3-126">只在您想要擷取作為映像的 VM 上執行這個命令。</span><span class="sxs-lookup"><span data-stu-id="659b3-126">Only run this command on a VM that you intend to capture as an image.</span></span> <span data-ttu-id="659b3-127">這不能保證映像檔中的所有機密資訊都會清除完畢或適合轉散發。</span><span class="sxs-lookup"><span data-stu-id="659b3-127">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution.</span></span> <span data-ttu-id="659b3-128">+user 參數也會移除最後一個佈建的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="659b3-128">The *+user* parameter also removes the last provisioned user account.</span></span> <span data-ttu-id="659b3-129">如果您想要保留 VM 中的帳戶認證，只要使用 -deprovision 就地保留使用者帳戶即可。</span><span class="sxs-lookup"><span data-stu-id="659b3-129">If you want to keep account credentials in the VM, just use *-deprovision* to leave the user account in place.</span></span>
 
3. <span data-ttu-id="659b3-130">輸入 **y** 繼續。</span><span class="sxs-lookup"><span data-stu-id="659b3-130">Type **y** to continue.</span></span> <span data-ttu-id="659b3-131">您可以加入 **-force** 參數，便不用進行此確認步驟。</span><span class="sxs-lookup"><span data-stu-id="659b3-131">You can add the **-force** parameter to avoid this confirmation step.</span></span>
4. <span data-ttu-id="659b3-132">在命令完成之後，請輸入 **exit**。</span><span class="sxs-lookup"><span data-stu-id="659b3-132">After the command completes, type **exit**.</span></span> <span data-ttu-id="659b3-133">此步驟會關閉 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="659b3-133">This step closes the SSH client.</span></span>

## <a name="step-2-create-vm-image"></a><span data-ttu-id="659b3-134">步驟 2：建立 VM 映像</span><span class="sxs-lookup"><span data-stu-id="659b3-134">Step 2: Create VM image</span></span>
<span data-ttu-id="659b3-135">使用 Azure CLI 2.0 將 VM 標記為一般化，並擷取映像。</span><span class="sxs-lookup"><span data-stu-id="659b3-135">Use the Azure CLI 2.0 to mark the VM as generalized and capture the image.</span></span> <span data-ttu-id="659b3-136">在下列範例中，請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="659b3-136">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="659b3-137">範例參數名稱包含 *myResourceGroup*、*myVnet* 和 *myVM*。</span><span class="sxs-lookup"><span data-stu-id="659b3-137">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

1. <span data-ttu-id="659b3-138">使用 [az vm deallocate](/cli//azure/vm#deallocate) 解除配置已取消佈建的 VM。</span><span class="sxs-lookup"><span data-stu-id="659b3-138">Deallocate the VM that you deprovisioned with [az vm deallocate](/cli//azure/vm#deallocate).</span></span> <span data-ttu-id="659b3-139">下列範例會解除配置名為 myResourceGroup 資源群組中名為 myVM 的 VM：</span><span class="sxs-lookup"><span data-stu-id="659b3-139">The following example deallocates the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. <span data-ttu-id="659b3-140">使用 [az vm generalize](/cli//azure/vm#generalize)，將 VM 標記為一般化。</span><span class="sxs-lookup"><span data-stu-id="659b3-140">Mark the VM as generalized with [az vm generalize](/cli//azure/vm#generalize).</span></span> <span data-ttu-id="659b3-141">下列範例會將名為 myResourceGroup 的資源群組中名為 myVM 的 VM 標記為一般化：</span><span class="sxs-lookup"><span data-stu-id="659b3-141">The following example marks the the VM named *myVM* in the resource group named *myResourceGroup* as generalized:</span></span>
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. <span data-ttu-id="659b3-142">使用 [az image create](/cli//azure/image#create) 建立 VM 資源的映像。</span><span class="sxs-lookup"><span data-stu-id="659b3-142">Now create an image of the VM resource with [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="659b3-143">下列範例會使用名為 myVM 的 VM 資源，在 myResourceGroup 資源群組中建立名為 myImage 的映像：</span><span class="sxs-lookup"><span data-stu-id="659b3-143">The following example creates an image named *myImage* in the resource group named *myResourceGroup* using the VM resource named *myVM*:</span></span>
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > <span data-ttu-id="659b3-144">此映像與來源 VM 建立於相同的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="659b3-144">The image is created in the same resource group as your source VM.</span></span> <span data-ttu-id="659b3-145">您可以從此映像，在您訂用帳戶的任何資源群組中建立 VM。</span><span class="sxs-lookup"><span data-stu-id="659b3-145">You can create VMs in any resource group within your subscription from this image.</span></span> <span data-ttu-id="659b3-146">從管理觀點來看，您可能想為您的 VM 資源和映像建立特定的資源群組。</span><span class="sxs-lookup"><span data-stu-id="659b3-146">From a management perspective, you may wish to create a specific resource group for your VM resources and images.</span></span>

## <a name="step-3-create-a-vm-from-the-captured-image"></a><span data-ttu-id="659b3-147">步驟 3：從擷取的映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="659b3-147">Step 3: Create a VM from the captured image</span></span>
<span data-ttu-id="659b3-148">使用您以 [az vm create](/cli/azure/vm#create) 建立的映像來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="659b3-148">Create a VM using the image you created with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="659b3-149">下列範例會從名為 myImage 的映像建立名為 myVMDeployed 的 VM：</span><span class="sxs-lookup"><span data-stu-id="659b3-149">The following example creates a VM named *myVMDeployed* from the image named *myImage*:</span></span>

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-the-vm-in-another-resource-group"></a><span data-ttu-id="659b3-150">在另一個資源群組中建立 VM</span><span class="sxs-lookup"><span data-stu-id="659b3-150">Creating the VM in another resource group</span></span> 

<span data-ttu-id="659b3-151">您可以從某個映像，在您訂用帳戶的任何資源群組中建立 VM。</span><span class="sxs-lookup"><span data-stu-id="659b3-151">You can create VMs from an image in any resource group within your subscription.</span></span> <span data-ttu-id="659b3-152">若要在與映像不同的資源群組中建立 VM，請指定您映像的完整資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="659b3-152">To create a VM in a different resource group than the image, specify the full resource ID to your image.</span></span> <span data-ttu-id="659b3-153">使用 [az image list](/cli/azure/image#list) 來檢視映像清單。</span><span class="sxs-lookup"><span data-stu-id="659b3-153">Use [az image list](/cli/azure/image#list) to view a list of images.</span></span> <span data-ttu-id="659b3-154">輸出類似於下列範例：</span><span class="sxs-lookup"><span data-stu-id="659b3-154">The output is similar to the following example:</span></span>

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

<span data-ttu-id="659b3-155">下列範例藉由指定映像資源識別碼，進而使用 [az vm create](/cli/azure/vm#create) 在與來源映像不同的資源群組中建立 VM︰</span><span class="sxs-lookup"><span data-stu-id="659b3-155">The following example uses [az vm create](/cli/azure/vm#create) to create a VM in a different resource group than the source image by specifying the image resource ID:</span></span>

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-the-deployment"></a><span data-ttu-id="659b3-156">步驟 4：驗證部署</span><span class="sxs-lookup"><span data-stu-id="659b3-156">Step 4: Verify the deployment</span></span>

<span data-ttu-id="659b3-157">現在使用您建立的虛擬機器的 SSH 來驗證部署並開始使用新的 VM。</span><span class="sxs-lookup"><span data-stu-id="659b3-157">Now SSH to the virtual machine you created to verify the deployment and start using the new VM.</span></span> <span data-ttu-id="659b3-158">若要透過 SSH 連接，請利用 [az vm show](/cli/azure/vm#show) 尋找您 VM 的 IP 位址或 FQDN：</span><span class="sxs-lookup"><span data-stu-id="659b3-158">To connect via SSH, find the IP address or FQDN of your VM with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a><span data-ttu-id="659b3-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="659b3-159">Next steps</span></span>
<span data-ttu-id="659b3-160">您可以從來源 VM 映像建立多個 VM。</span><span class="sxs-lookup"><span data-stu-id="659b3-160">You can create multiple VMs from your source VM image.</span></span> <span data-ttu-id="659b3-161">如果您需要變更您的映像︰</span><span class="sxs-lookup"><span data-stu-id="659b3-161">If you need to make changes to your image:</span></span> 

- <span data-ttu-id="659b3-162">從映像建立 VM。</span><span class="sxs-lookup"><span data-stu-id="659b3-162">Create a VM from your image.</span></span>
- <span data-ttu-id="659b3-163">進行任何更新或組態變更。</span><span class="sxs-lookup"><span data-stu-id="659b3-163">Make any updates or configuration changes.</span></span>
- <span data-ttu-id="659b3-164">再次遵循相關步驟，以取消佈建、解除配置、一般化及建立映像。</span><span class="sxs-lookup"><span data-stu-id="659b3-164">Follow the steps again to deprovision, deallocate, generalize, and create an image.</span></span>
- <span data-ttu-id="659b3-165">在日後的部署中使用這個新映像。</span><span class="sxs-lookup"><span data-stu-id="659b3-165">Use this new image for future deployments.</span></span> <span data-ttu-id="659b3-166">如有需要，刪除原始的映像。</span><span class="sxs-lookup"><span data-stu-id="659b3-166">If desired, delete the original image.</span></span>

<span data-ttu-id="659b3-167">如需有關使用 CLI 管理 VM 的詳細資訊，請參閱[Azure CLI 2.0](/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="659b3-167">For more information on managing your VMs with the CLI, see [Azure CLI 2.0](/cli/azure/overview).</span></span>
