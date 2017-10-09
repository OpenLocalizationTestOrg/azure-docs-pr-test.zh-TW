---
title: "使用 CLI 2.0 在 Azure 中 Linux VM 的映像 aaaCapture |Microsoft 文件"
description: "擷取映像，如需使用 Azure CLI 2.0 hello 的大型部署 Azure VM toouse。"
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
ms.openlocfilehash: 9558332a86186b282775097428df462709373012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-image-of-a-virtual-machine-or-vhd"></a><span data-ttu-id="181d6-103">如何 toocreate 的虛擬機器或 VHD 映像</span><span class="sxs-lookup"><span data-stu-id="181d6-103">How toocreate an image of a virtual machine or VHD</span></span>

<!-- generalize, image - extended version of hello tutorial-->

<span data-ttu-id="181d6-104">toocreate 多個副本在 Azure 中，虛擬機器 (VM) toouse 擷取 hello VM 映像或 hello OS VHD。</span><span class="sxs-lookup"><span data-stu-id="181d6-104">toocreate multiple copies of a virtual machine (VM) toouse in Azure, capture an image of hello VM or hello OS VHD.</span></span> <span data-ttu-id="181d6-105">toocreate 映像，您需要移除個人的帳戶資訊，使其更安全的 toodeploy 多次。</span><span class="sxs-lookup"><span data-stu-id="181d6-105">toocreate an image, you need remove personal account information which makes it safer toodeploy multiple times.</span></span> <span data-ttu-id="181d6-106">在您解除佈建現有 VM 的步驟 hello，取消配置並建立映像。</span><span class="sxs-lookup"><span data-stu-id="181d6-106">In hello following steps you deprovision an existing VM, deallocate and create an image.</span></span> <span data-ttu-id="181d6-107">您可以使用此映像 toocreate Vm 之間的任何資源群組，您的訂用帳戶內。</span><span class="sxs-lookup"><span data-stu-id="181d6-107">You can use this image toocreate VMs across any resource group within your subscription.</span></span>

<span data-ttu-id="181d6-108">如果您想要備份或偵錯，toocreate 現有的 Linux VM 的複本或特定的 Linux VHD 從內部部署 VM 上傳，請參閱[上傳並從自訂的磁碟映像建立 Linux VM](upload-vhd.md)。</span><span class="sxs-lookup"><span data-stu-id="181d6-108">If you want toocreate a copy of your existing Linux VM for backup or debugging, or upload a specialized Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md).</span></span>  

<span data-ttu-id="181d6-109">您也可以使用**Packer** toocreate 您的自訂設定。</span><span class="sxs-lookup"><span data-stu-id="181d6-109">You can also use **Packer** toocreate your custom configuration.</span></span> <span data-ttu-id="181d6-110">如需有關使用 Packer 的詳細資訊，請參閱[toouse Packer toocreate Linux 虛擬機器在 Azure 中的映像](build-image-with-packer.md)。</span><span class="sxs-lookup"><span data-stu-id="181d6-110">For more information on using Packer, see [How toouse Packer toocreate Linux virtual machine images in Azure](build-image-with-packer.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="181d6-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="181d6-111">Before you begin</span></span>
<span data-ttu-id="181d6-112">請確定您符合下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="181d6-112">Ensure that you meet hello following prerequisites:</span></span>

* <span data-ttu-id="181d6-113">您必須使用受管理的磁碟 hello Resource Manager 部署模型中建立 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="181d6-113">You need an Azure VM created in hello Resource Manager deployment model using managed disks.</span></span> <span data-ttu-id="181d6-114">如果您尚未建立 Linux VM，您可以使用 hello[入口網站](quick-create-portal.md)，hello [Azure CLI](quick-create-cli.md)，或[資源管理員範本](create-ssh-secured-vm-from-template.md)。</span><span class="sxs-lookup"><span data-stu-id="181d6-114">If you haven't created a Linux VM, you can use hello [portal](quick-create-portal.md), hello [Azure CLI](quick-create-cli.md), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> <span data-ttu-id="181d6-115">設定 VM，視 hello。</span><span class="sxs-lookup"><span data-stu-id="181d6-115">Configure hello VM as needed.</span></span> <span data-ttu-id="181d6-116">例如，[新增資料磁碟](add-disk.md)、套用更新，並安裝應用程式。</span><span class="sxs-lookup"><span data-stu-id="181d6-116">For example, [add data disks](add-disk.md), apply updates, and install applications.</span></span> 

* <span data-ttu-id="181d6-117">您也需要 toohave hello 最新[Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="181d6-117">You also need toohave hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and be logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="181d6-118">快速命令</span><span class="sxs-lookup"><span data-stu-id="181d6-118">Quick commands</span></span>

<span data-ttu-id="181d6-119">本主題，適用於測試的簡化版本的評估，或深入了解 Azure 中的 Vm，請參閱[建立自訂映像的 Azure VM 使用 hello CLI](tutorial-custom-images.md)。</span><span class="sxs-lookup"><span data-stu-id="181d6-119">For a simplified version of this topic, for testing, evaluating or learning about VMs in Azure, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md).</span></span>


## <a name="step-1-deprovision-hello-vm"></a><span data-ttu-id="181d6-120">步驟 1： 解除佈建 VM hello</span><span class="sxs-lookup"><span data-stu-id="181d6-120">Step 1: Deprovision hello VM</span></span>
<span data-ttu-id="181d6-121">您解除佈建 hello hello Azure VM 代理程式、 toodelete 機器特定檔案和資料所使用的 VM。</span><span class="sxs-lookup"><span data-stu-id="181d6-121">You deprovision hello VM, using hello Azure VM agent, toodelete machine specific files and data.</span></span> <span data-ttu-id="181d6-122">使用 hello`waagent`命令與 hello *-取消佈建 + 使用者*您來源 Linux VM 上的參數。</span><span class="sxs-lookup"><span data-stu-id="181d6-122">Use hello `waagent` command with hello *-deprovision+user* parameter on your source Linux VM.</span></span> <span data-ttu-id="181d6-123">如需詳細資訊，請參閱 hello [Azure Linux 代理程式使用者指南](../windows/agent-user-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="181d6-123">For more information, see hello [Azure Linux Agent user guide](../windows/agent-user-guide.md).</span></span>

1. <span data-ttu-id="181d6-124">連接 tooyour 使用 SSH 用戶端的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="181d6-124">Connect tooyour Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="181d6-125">在 hello SSH 視窗中，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="181d6-125">In hello SSH window, type hello following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > <span data-ttu-id="181d6-126">只有執行此命令在 VM 上的您想 toocapture 做為映像。</span><span class="sxs-lookup"><span data-stu-id="181d6-126">Only run this command on a VM that you intend toocapture as an image.</span></span> <span data-ttu-id="181d6-127">它並不保證清除所有的機密資訊的 hello 映像，或適用於轉散發。</span><span class="sxs-lookup"><span data-stu-id="181d6-127">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution.</span></span> <span data-ttu-id="181d6-128">hello *+ 使用者*參數也會移除 hello 最後一個佈建的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="181d6-128">hello *+user* parameter also removes hello last provisioned user account.</span></span> <span data-ttu-id="181d6-129">如果您想 tookeep hello VM 中的帳戶認證，只要使用*-取消佈建*就地 tooleave hello 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="181d6-129">If you want tookeep account credentials in hello VM, just use *-deprovision* tooleave hello user account in place.</span></span>
 
3. <span data-ttu-id="181d6-130">型別**y** toocontinue。</span><span class="sxs-lookup"><span data-stu-id="181d6-130">Type **y** toocontinue.</span></span> <span data-ttu-id="181d6-131">您可以新增 hello **-強制**參數 tooavoid 此確認步驟。</span><span class="sxs-lookup"><span data-stu-id="181d6-131">You can add hello **-force** parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="181d6-132">Hello 命令完成之後，請輸入**結束**。</span><span class="sxs-lookup"><span data-stu-id="181d6-132">After hello command completes, type **exit**.</span></span> <span data-ttu-id="181d6-133">此步驟會關閉 hello SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="181d6-133">This step closes hello SSH client.</span></span>

## <a name="step-2-create-vm-image"></a><span data-ttu-id="181d6-134">步驟 2：建立 VM 映像</span><span class="sxs-lookup"><span data-stu-id="181d6-134">Step 2: Create VM image</span></span>
<span data-ttu-id="181d6-135">使用 Azure CLI 2.0 hello toomark hello VM 一般化，擷取 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="181d6-135">Use hello Azure CLI 2.0 toomark hello VM as generalized and capture hello image.</span></span> <span data-ttu-id="181d6-136">在 hello 下列範例中，會取代您自己的值的範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="181d6-136">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="181d6-137">範例參數名稱包含 *myResourceGroup*、*myVnet* 和 *myVM*。</span><span class="sxs-lookup"><span data-stu-id="181d6-137">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

1. <span data-ttu-id="181d6-138">解除配置 hello 解除與佈建的 VM [az vm 解除配置](/cli//azure/vm#deallocate)。</span><span class="sxs-lookup"><span data-stu-id="181d6-138">Deallocate hello VM that you deprovisioned with [az vm deallocate](/cli//azure/vm#deallocate).</span></span> <span data-ttu-id="181d6-139">hello 下列範例會取消配置 hello 名為 VM *myVM* hello 資源群組中名為*myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="181d6-139">hello following example deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. <span data-ttu-id="181d6-140">標記 hello 工作者角色是與一般化[az vm 一般化](/cli//azure/vm#generalize)。</span><span class="sxs-lookup"><span data-stu-id="181d6-140">Mark hello VM as generalized with [az vm generalize](/cli//azure/vm#generalize).</span></span> <span data-ttu-id="181d6-141">下列範例標記 hello hello VM 名為 hello *myVM* hello 資源群組中名為*myResourceGroup*為一般化：</span><span class="sxs-lookup"><span data-stu-id="181d6-141">hello following example marks hello hello VM named *myVM* in hello resource group named *myResourceGroup* as generalized:</span></span>
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. <span data-ttu-id="181d6-142">現在建立 hello VM 資源的映像[az 映像建立](/cli//azure/image#create)。</span><span class="sxs-lookup"><span data-stu-id="181d6-142">Now create an image of hello VM resource with [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="181d6-143">hello 下列範例會建立名為映像*myImage* hello 資源群組中名為*myResourceGroup*使用名為 hello VM 資源*myVM*:</span><span class="sxs-lookup"><span data-stu-id="181d6-143">hello following example creates an image named *myImage* in hello resource group named *myResourceGroup* using hello VM resource named *myVM*:</span></span>
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > <span data-ttu-id="181d6-144">hello 映像中建立 hello 相同資源群組，做為來源 VM。</span><span class="sxs-lookup"><span data-stu-id="181d6-144">hello image is created in hello same resource group as your source VM.</span></span> <span data-ttu-id="181d6-145">您可以從此映像，在您訂用帳戶的任何資源群組中建立 VM。</span><span class="sxs-lookup"><span data-stu-id="181d6-145">You can create VMs in any resource group within your subscription from this image.</span></span> <span data-ttu-id="181d6-146">管理的觀點而言，您可能希望 toocreate 您 VM 資源和影像的特定資源群組。</span><span class="sxs-lookup"><span data-stu-id="181d6-146">From a management perspective, you may wish toocreate a specific resource group for your VM resources and images.</span></span>

## <a name="step-3-create-a-vm-from-hello-captured-image"></a><span data-ttu-id="181d6-147">步驟 3： 從 hello 擷取映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="181d6-147">Step 3: Create a VM from hello captured image</span></span>
<span data-ttu-id="181d6-148">使用您建立與 hello 映像建立 VM [az vm 建立](/cli/azure/vm#create)。</span><span class="sxs-lookup"><span data-stu-id="181d6-148">Create a VM using hello image you created with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="181d6-149">hello 下列範例會建立名為的 VM *myVMDeployed*從名為 「 hello 」 映像*myImage*:</span><span class="sxs-lookup"><span data-stu-id="181d6-149">hello following example creates a VM named *myVMDeployed* from hello image named *myImage*:</span></span>

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-hello-vm-in-another-resource-group"></a><span data-ttu-id="181d6-150">建立另一個資源群組中的 hello VM</span><span class="sxs-lookup"><span data-stu-id="181d6-150">Creating hello VM in another resource group</span></span> 

<span data-ttu-id="181d6-151">您可以從某個映像，在您訂用帳戶的任何資源群組中建立 VM。</span><span class="sxs-lookup"><span data-stu-id="181d6-151">You can create VMs from an image in any resource group within your subscription.</span></span> <span data-ttu-id="181d6-152">toocreate 比 hello 影像的不同資源群組中的 VM 指定 hello 完整資源識別碼 tooyour 映像。</span><span class="sxs-lookup"><span data-stu-id="181d6-152">toocreate a VM in a different resource group than hello image, specify hello full resource ID tooyour image.</span></span> <span data-ttu-id="181d6-153">使用[az 影像清單](/cli/azure/image#list)tooview 映像清單。</span><span class="sxs-lookup"><span data-stu-id="181d6-153">Use [az image list](/cli/azure/image#list) tooview a list of images.</span></span> <span data-ttu-id="181d6-154">hello 輸出是 toohello 類似下列範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="181d6-154">hello output is similar toohello following example:</span></span>

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

<span data-ttu-id="181d6-155">hello 下列範例會使用[az vm 建立](/cli/azure/vm#create)toocreate 比藉由指定 hello 的影像資源識別碼 hello 來源影像的不同資源群組中的 VM:</span><span class="sxs-lookup"><span data-stu-id="181d6-155">hello following example uses [az vm create](/cli/azure/vm#create) toocreate a VM in a different resource group than hello source image by specifying hello image resource ID:</span></span>

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-hello-deployment"></a><span data-ttu-id="181d6-156">步驟 4： 驗證 hello 部署</span><span class="sxs-lookup"><span data-stu-id="181d6-156">Step 4: Verify hello deployment</span></span>

<span data-ttu-id="181d6-157">現在 SSH toohello 建立虛擬機器您 tooverify hello 部署並開始使用 hello 新的 VM。</span><span class="sxs-lookup"><span data-stu-id="181d6-157">Now SSH toohello virtual machine you created tooverify hello deployment and start using hello new VM.</span></span> <span data-ttu-id="181d6-158">透過 SSH，tooconnect 尋找具有您 VM 的 hello IP 位址或者 FQDN [az vm 顯示](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="181d6-158">tooconnect via SSH, find hello IP address or FQDN of your VM with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a><span data-ttu-id="181d6-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="181d6-159">Next steps</span></span>
<span data-ttu-id="181d6-160">您可以從來源 VM 映像建立多個 VM。</span><span class="sxs-lookup"><span data-stu-id="181d6-160">You can create multiple VMs from your source VM image.</span></span> <span data-ttu-id="181d6-161">如果您需要 toomake 變更 tooyour 映像：</span><span class="sxs-lookup"><span data-stu-id="181d6-161">If you need toomake changes tooyour image:</span></span> 

- <span data-ttu-id="181d6-162">從映像建立 VM。</span><span class="sxs-lookup"><span data-stu-id="181d6-162">Create a VM from your image.</span></span>
- <span data-ttu-id="181d6-163">進行任何更新或組態變更。</span><span class="sxs-lookup"><span data-stu-id="181d6-163">Make any updates or configuration changes.</span></span>
- <span data-ttu-id="181d6-164">請遵循 hello 步驟再次 toodeprovision、 取消、 一般化，和建立映像。</span><span class="sxs-lookup"><span data-stu-id="181d6-164">Follow hello steps again toodeprovision, deallocate, generalize, and create an image.</span></span>
- <span data-ttu-id="181d6-165">在日後的部署中使用這個新映像。</span><span class="sxs-lookup"><span data-stu-id="181d6-165">Use this new image for future deployments.</span></span> <span data-ttu-id="181d6-166">如有需要，刪除 hello 原始映像。</span><span class="sxs-lookup"><span data-stu-id="181d6-166">If desired, delete hello original image.</span></span>

<span data-ttu-id="181d6-167">如需有關如何管理您的 Vm 以 hello CLI 的詳細資訊，請參閱[Azure CLI 2.0](/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="181d6-167">For more information on managing your VMs with hello CLI, see [Azure CLI 2.0](/cli/azure/overview).</span></span>
