---
title: "使用 Azure CLI 建立自訂的 VM 映像 | Microsoft Docs"
description: "教學課程 - 使用 Azure CLI 建立自訂的 VM 映像。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/21/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: d32980f05ad17a76793021d0a5355d597974a4e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-the-cli"></a><span data-ttu-id="a92db-103">使用 CLI 建立 Azure VM 的自訂映像</span><span class="sxs-lookup"><span data-stu-id="a92db-103">Create a custom image of an Azure VM using the CLI</span></span>

<span data-ttu-id="a92db-104">自訂映像類似 Marketplace 映像，但您要自行建立它們。</span><span class="sxs-lookup"><span data-stu-id="a92db-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="a92db-105">自訂映像可用於啟動程序設定，例如，預先載入應用程式、應用程式設定和其他 OS 設定。</span><span class="sxs-lookup"><span data-stu-id="a92db-105">Custom images can be used to bootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="a92db-106">在本教學課程中，您將建立自己的 Azure 虛擬機器自訂映像。</span><span class="sxs-lookup"><span data-stu-id="a92db-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="a92db-107">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="a92db-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a92db-108">取消佈建及一般化 VM</span><span class="sxs-lookup"><span data-stu-id="a92db-108">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="a92db-109">建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="a92db-109">Create a custom image</span></span>
> * <span data-ttu-id="a92db-110">從自訂映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="a92db-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="a92db-111">列出訂用帳戶中的所有映像</span><span class="sxs-lookup"><span data-stu-id="a92db-111">List all the images in your subscription</span></span>
> * <span data-ttu-id="a92db-112">删除映像</span><span class="sxs-lookup"><span data-stu-id="a92db-112">Delete an image</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a92db-113">如果您選擇在本機安裝和使用 CLI，本教學課程會要求您執行 Azure CLI 2.0.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="a92db-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a92db-114">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="a92db-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="a92db-115">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="a92db-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="a92db-116">開始之前</span><span class="sxs-lookup"><span data-stu-id="a92db-116">Before you begin</span></span>

<span data-ttu-id="a92db-117">下列步驟將詳細說明如何將現有 VM 轉換成可重複使用的自訂映像，以便讓您用來建立新的 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a92db-117">The steps below detail how to take an existing VM and turn it into a re-usable custom image that you can use to create new VM instances.</span></span>

<span data-ttu-id="a92db-118">若要完成本教學課程中的範例，您目前必須具有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a92db-118">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="a92db-119">如有需要，這個[指令碼範例](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md)可以為您建立一部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a92db-119">If needed, this [script sample](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) can create one for you.</span></span> <span data-ttu-id="a92db-120">逐步完成教學課程之後，請視需要取代資源群組和 VM 名稱。</span><span class="sxs-lookup"><span data-stu-id="a92db-120">When working through the tutorial, replace the resource group and VM names where needed.</span></span>

## <a name="create-a-custom-image"></a><span data-ttu-id="a92db-121">建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="a92db-121">Create a custom image</span></span>

<span data-ttu-id="a92db-122">若要建立虛擬機器的映像，您需要藉由取消佈建、解除配置，然後將來源 VM 標示為一般化，來準備 VM。</span><span class="sxs-lookup"><span data-stu-id="a92db-122">To create an image of a virtual machine, you need to prepare the VM by deprovisioning, deallocating, and then marking the source VM as generalized.</span></span> <span data-ttu-id="a92db-123">一旦已備妥 VM，便可以建立映像。</span><span class="sxs-lookup"><span data-stu-id="a92db-123">Once the VM has been prepared, you can create an image.</span></span>

### <a name="deprovision-the-vm"></a><span data-ttu-id="a92db-124">取消佈建 VM</span><span class="sxs-lookup"><span data-stu-id="a92db-124">Deprovision the VM</span></span> 

<span data-ttu-id="a92db-125">取消佈建會藉由移除電腦特定的資訊來將 VM 一般化。</span><span class="sxs-lookup"><span data-stu-id="a92db-125">Deprovisioning generalizes the VM by removing machine-specific information.</span></span> <span data-ttu-id="a92db-126">這個一般化讓您能夠從單一映像部署多部 VM。</span><span class="sxs-lookup"><span data-stu-id="a92db-126">This generalization makes it possible to deploy many VMs from a single image.</span></span> <span data-ttu-id="a92db-127">解除佈建期間，將主機名稱重設為 localhost.localdomain。</span><span class="sxs-lookup"><span data-stu-id="a92db-127">During deprovisioning, the host name is reset to *localhost.localdomain*.</span></span> <span data-ttu-id="a92db-128">SSH 主機金鑰、名稱伺服器設定、根密碼及快取的 DHCP 租用也會一併刪除。</span><span class="sxs-lookup"><span data-stu-id="a92db-128">SSH host keys, nameserver configurations, root password, and cached DHCP leases are also deleted.</span></span>

<span data-ttu-id="a92db-129">若要取消佈建 VM，請使用 Azure VM 代理程式 (waagent)。</span><span class="sxs-lookup"><span data-stu-id="a92db-129">To deprovision the VM, use the Azure VM agent (waagent).</span></span> <span data-ttu-id="a92db-130">Azure VM 代理程式會安裝於 VM 上，並管理佈建以及與 Azure 網狀架構控制器進行互動。</span><span class="sxs-lookup"><span data-stu-id="a92db-130">The Azure VM agent is installed on the VM and manages provisioning and interacting with the Azure Fabric Controller.</span></span> <span data-ttu-id="a92db-131">如需詳細資訊，請參閱 [Azure Linux 代理程式使用者指南](agent-user-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="a92db-131">For more information, see the [Azure Linux Agent user guide](agent-user-guide.md).</span></span>

<span data-ttu-id="a92db-132">使用 SSH 連接到您的 VM，並執行命令以取消佈建 VM。</span><span class="sxs-lookup"><span data-stu-id="a92db-132">Connect to your VM using SSH and run the command to deprovision the VM.</span></span> <span data-ttu-id="a92db-133">利用 `+user` 引數，同時刪除最後佈建的使用者帳戶及所有相關聯的資料。</span><span class="sxs-lookup"><span data-stu-id="a92db-133">With the `+user` argument, the last provisioned user account and any associated data are also deleted.</span></span> <span data-ttu-id="a92db-134">以 VM 的公用 IP 位址取代範例 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a92db-134">Replace the example IP address with the public IP address of your VM.</span></span>

<span data-ttu-id="a92db-135">透過 SSH 連接到 VM。</span><span class="sxs-lookup"><span data-stu-id="a92db-135">SSH to the VM.</span></span>
```bash
ssh azureuser@52.174.34.95
```
<span data-ttu-id="a92db-136">取消佈建 VM。</span><span class="sxs-lookup"><span data-stu-id="a92db-136">Deprovision the VM.</span></span>

```bash
sudo waagent -deprovision+user -force
```
<span data-ttu-id="a92db-137">關閉 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="a92db-137">Close the SSH session.</span></span>

```bash
exit
```

### <a name="deallocate-and-mark-the-vm-as-generalized"></a><span data-ttu-id="a92db-138">解除配置並將 VM 標示為一般化</span><span class="sxs-lookup"><span data-stu-id="a92db-138">Deallocate and mark the VM as generalized</span></span>

<span data-ttu-id="a92db-139">若要建立映像，必須解除配置 VM。</span><span class="sxs-lookup"><span data-stu-id="a92db-139">To create an image, the VM needs to be deallocated.</span></span> <span data-ttu-id="a92db-140">使用 [az vm deallocate](/cli//azure/vm#deallocate) 解除配置 VM。</span><span class="sxs-lookup"><span data-stu-id="a92db-140">Deallocate the VM using [az vm deallocate](/cli//azure/vm#deallocate).</span></span> 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="a92db-141">最後，使用 [az vm generalize](/cli//azure/vm#generalize) 將 VM 的狀態設為一般化，如此一來，Azure 平台就會知道 VM 已一般化。</span><span class="sxs-lookup"><span data-stu-id="a92db-141">Finally, set the state of the VM as generalized with [az vm generalize](/cli//azure/vm#generalize) so the Azure platform knows the VM has been generalized.</span></span> <span data-ttu-id="a92db-142">您只能從一般化的 VM 建立映像。</span><span class="sxs-lookup"><span data-stu-id="a92db-142">You can only create an image from a generalized VM.</span></span>
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-the-image"></a><span data-ttu-id="a92db-143">建立映像</span><span class="sxs-lookup"><span data-stu-id="a92db-143">Create the image</span></span>

<span data-ttu-id="a92db-144">現在，您可以使用 [az image create](/cli//azure/image#create) 來建立 VM 的映像。</span><span class="sxs-lookup"><span data-stu-id="a92db-144">Now you can create an image of the VM by using [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="a92db-145">下列範例會從名為 myVM 的 VM 建立名為 myImage 的映像。</span><span class="sxs-lookup"><span data-stu-id="a92db-145">The following example creates an image named *myImage* from a VM named *myVM*.</span></span>
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-the-image"></a><span data-ttu-id="a92db-146">從映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="a92db-146">Create VMs from the image</span></span>

<span data-ttu-id="a92db-147">現在您已有映像，您可以使用 [az vm create](/cli/azure/vm#create) 從映像建立一個或多個新的 VM。</span><span class="sxs-lookup"><span data-stu-id="a92db-147">Now that you have an image, you can create one or more new VMs from the image using [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="a92db-148">下列範例會從名為 myImage 的映像建立名為 myVMfromImage 的 VM。</span><span class="sxs-lookup"><span data-stu-id="a92db-148">The following example creates a VM named *myVMfromImage* from the image named *myImage*.</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a><span data-ttu-id="a92db-149">映像管理</span><span class="sxs-lookup"><span data-stu-id="a92db-149">Image management</span></span> 

<span data-ttu-id="a92db-150">以下範例是一些常見的映像管理作業，以及如何使用 Azure CLI 完成這些作業。</span><span class="sxs-lookup"><span data-stu-id="a92db-150">Here are some examples of common image management tasks and how to complete them using the Azure CLI.</span></span>

<span data-ttu-id="a92db-151">以資料表格式依名稱列出所有映像。</span><span class="sxs-lookup"><span data-stu-id="a92db-151">List all images by name in a table format.</span></span>

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

<span data-ttu-id="a92db-152">删除映像。</span><span class="sxs-lookup"><span data-stu-id="a92db-152">Delete an image.</span></span> <span data-ttu-id="a92db-153">此範例會刪除 myResourceGroup 中名為 myOldImage 的映像。</span><span class="sxs-lookup"><span data-stu-id="a92db-153">This example deletes the image named *myOldImage* from the *myResourceGroup*.</span></span>

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="a92db-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a92db-154">Next steps</span></span>

<span data-ttu-id="a92db-155">您在本教學課程中建立了自訂 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="a92db-155">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="a92db-156">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="a92db-156">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a92db-157">取消佈建及一般化 VM</span><span class="sxs-lookup"><span data-stu-id="a92db-157">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="a92db-158">建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="a92db-158">Create a custom image</span></span>
> * <span data-ttu-id="a92db-159">從自訂映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="a92db-159">Create a VM from a custom image</span></span>
> * <span data-ttu-id="a92db-160">列出訂用帳戶中的所有映像</span><span class="sxs-lookup"><span data-stu-id="a92db-160">List all the images in your subscription</span></span>
> * <span data-ttu-id="a92db-161">删除映像</span><span class="sxs-lookup"><span data-stu-id="a92db-161">Delete an image</span></span>

<span data-ttu-id="a92db-162">請前進到下一個教學課程，了解高可用性的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a92db-162">Advance to the next tutorial to learn about highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="a92db-163">[建立高可用性 VM](tutorial-availability-sets.md)。</span><span class="sxs-lookup"><span data-stu-id="a92db-163">[Create highly available VMs](tutorial-availability-sets.md).</span></span>

