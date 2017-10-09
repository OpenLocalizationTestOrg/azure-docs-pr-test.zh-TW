---
title: "aaaCreate 自訂 VM 映像以 hello Azure CLI |Microsoft 文件"
description: "教學課程-建立自訂的 VM 映像，使用 Azure CLI hello。"
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
ms.openlocfilehash: 217a993c0c1d48939b74108ac6c5f7a1a619416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-hello-cli"></a><span data-ttu-id="cab70-103">建立 Azure VM 使用 hello CLI 的自訂映像</span><span class="sxs-lookup"><span data-stu-id="cab70-103">Create a custom image of an Azure VM using hello CLI</span></span>

<span data-ttu-id="cab70-104">自訂映像類似 Marketplace 映像，但您要自行建立它們。</span><span class="sxs-lookup"><span data-stu-id="cab70-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="cab70-105">自訂映像可以使用的 toobootstrap 組態，例如預先載入應用程式、 應用程式設定和其他作業系統設定。</span><span class="sxs-lookup"><span data-stu-id="cab70-105">Custom images can be used toobootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="cab70-106">在本教學課程中，您將建立自己的 Azure 虛擬機器自訂映像。</span><span class="sxs-lookup"><span data-stu-id="cab70-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="cab70-107">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="cab70-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cab70-108">取消佈建及一般化 VM</span><span class="sxs-lookup"><span data-stu-id="cab70-108">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="cab70-109">建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="cab70-109">Create a custom image</span></span>
> * <span data-ttu-id="cab70-110">從自訂映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="cab70-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="cab70-111">列出您的訂用帳戶中的所有 hello 映像</span><span class="sxs-lookup"><span data-stu-id="cab70-111">List all hello images in your subscription</span></span>
> * <span data-ttu-id="cab70-112">删除映像</span><span class="sxs-lookup"><span data-stu-id="cab70-112">Delete an image</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="cab70-113">如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="cab70-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="cab70-114">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="cab70-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="cab70-115">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="cab70-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="cab70-116">開始之前</span><span class="sxs-lookup"><span data-stu-id="cab70-116">Before you begin</span></span>

<span data-ttu-id="cab70-117">下列的 hello 步驟詳細說明 tootake 現有的 VM 並開啟它的可重複使用的自訂映像，您可以使用 toocreate 新 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="cab70-117">hello steps below detail how tootake an existing VM and turn it into a re-usable custom image that you can use toocreate new VM instances.</span></span>

<span data-ttu-id="cab70-118">在本教學課程 toocomplete hello 範例中的，您必須擁有現有的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="cab70-118">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="cab70-119">如有需要，這個[指令碼範例](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md)可以為您建立一部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="cab70-119">If needed, this [script sample](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) can create one for you.</span></span> <span data-ttu-id="cab70-120">當工作透過 hello 教學課程中，取代 hello 資源群組和 VM 名稱在需要時。</span><span class="sxs-lookup"><span data-stu-id="cab70-120">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

## <a name="create-a-custom-image"></a><span data-ttu-id="cab70-121">建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="cab70-121">Create a custom image</span></span>

<span data-ttu-id="cab70-122">toocreate 虛擬機器的映像，您需要 tooprepare hello VM 和解除佈建、 解除配置，然後將標示 hello 來源為一般化 VM。</span><span class="sxs-lookup"><span data-stu-id="cab70-122">toocreate an image of a virtual machine, you need tooprepare hello VM by deprovisioning, deallocating, and then marking hello source VM as generalized.</span></span> <span data-ttu-id="cab70-123">一次 hello 已經準備好 VM，您可以建立映像。</span><span class="sxs-lookup"><span data-stu-id="cab70-123">Once hello VM has been prepared, you can create an image.</span></span>

### <a name="deprovision-hello-vm"></a><span data-ttu-id="cab70-124">取消佈建 VM hello</span><span class="sxs-lookup"><span data-stu-id="cab70-124">Deprovision hello VM</span></span> 

<span data-ttu-id="cab70-125">藉由移除電腦特定的資訊來解除佈建一般化 hello VM。</span><span class="sxs-lookup"><span data-stu-id="cab70-125">Deprovisioning generalizes hello VM by removing machine-specific information.</span></span> <span data-ttu-id="cab70-126">這項通則可讓可能 toodeploy 許多 Vm 從單一映像。</span><span class="sxs-lookup"><span data-stu-id="cab70-126">This generalization makes it possible toodeploy many VMs from a single image.</span></span> <span data-ttu-id="cab70-127">在解除佈建，hello 主機名稱就會重設太*localhost.localdomain*。</span><span class="sxs-lookup"><span data-stu-id="cab70-127">During deprovisioning, hello host name is reset too*localhost.localdomain*.</span></span> <span data-ttu-id="cab70-128">SSH 主機金鑰、名稱伺服器設定、根密碼及快取的 DHCP 租用也會一併刪除。</span><span class="sxs-lookup"><span data-stu-id="cab70-128">SSH host keys, nameserver configurations, root password, and cached DHCP leases are also deleted.</span></span>

<span data-ttu-id="cab70-129">toodeprovision hello VM，使用 hello Azure VM 代理程式 (waagent)。</span><span class="sxs-lookup"><span data-stu-id="cab70-129">toodeprovision hello VM, use hello Azure VM agent (waagent).</span></span> <span data-ttu-id="cab70-130">hello Azure VM 代理程式安裝在 hello VM 上，及管理佈建和互動 hello Azure 網狀架構控制器。</span><span class="sxs-lookup"><span data-stu-id="cab70-130">hello Azure VM agent is installed on hello VM and manages provisioning and interacting with hello Azure Fabric Controller.</span></span> <span data-ttu-id="cab70-131">如需詳細資訊，請參閱 hello [Azure Linux 代理程式使用者指南](agent-user-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="cab70-131">For more information, see hello [Azure Linux Agent user guide](agent-user-guide.md).</span></span>

<span data-ttu-id="cab70-132">連接 tooyour VM 使用 SSH 和執行的 hello 命令 toodeprovision hello VM。</span><span class="sxs-lookup"><span data-stu-id="cab70-132">Connect tooyour VM using SSH and run hello command toodeprovision hello VM.</span></span> <span data-ttu-id="cab70-133">以 hello`+user`引數、 hello 最後一個佈建的使用者帳戶和任何相關聯的資料也會一併刪除。</span><span class="sxs-lookup"><span data-stu-id="cab70-133">With hello `+user` argument, hello last provisioned user account and any associated data are also deleted.</span></span> <span data-ttu-id="cab70-134">Hello 範例 IP 位址取代成您的 VM hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="cab70-134">Replace hello example IP address with hello public IP address of your VM.</span></span>

<span data-ttu-id="cab70-135">SSH toohello VM。</span><span class="sxs-lookup"><span data-stu-id="cab70-135">SSH toohello VM.</span></span>
```bash
ssh azureuser@52.174.34.95
```
<span data-ttu-id="cab70-136">取消佈建 hello VM。</span><span class="sxs-lookup"><span data-stu-id="cab70-136">Deprovision hello VM.</span></span>

```bash
sudo waagent -deprovision+user -force
```
<span data-ttu-id="cab70-137">關閉 hello SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="cab70-137">Close hello SSH session.</span></span>

```bash
exit
```

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a><span data-ttu-id="cab70-138">解除配置，並將標示為一般化 VM hello</span><span class="sxs-lookup"><span data-stu-id="cab70-138">Deallocate and mark hello VM as generalized</span></span>

<span data-ttu-id="cab70-139">toocreate 映像，hello VM 需要 toobe 取消配置。</span><span class="sxs-lookup"><span data-stu-id="cab70-139">toocreate an image, hello VM needs toobe deallocated.</span></span> <span data-ttu-id="cab70-140">解除配置 hello VM 使用[az vm 解除配置](/cli//azure/vm#deallocate)。</span><span class="sxs-lookup"><span data-stu-id="cab70-140">Deallocate hello VM using [az vm deallocate](/cli//azure/vm#deallocate).</span></span> 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="cab70-141">最後，將 hello hello VM 狀態設定為與一般化[az vm 一般化](/cli//azure/vm#generalize)如此 hello Azure 平台才會知道的 hello VM 已一般化。</span><span class="sxs-lookup"><span data-stu-id="cab70-141">Finally, set hello state of hello VM as generalized with [az vm generalize](/cli//azure/vm#generalize) so hello Azure platform knows hello VM has been generalized.</span></span> <span data-ttu-id="cab70-142">您只能從一般化的 VM 建立映像。</span><span class="sxs-lookup"><span data-stu-id="cab70-142">You can only create an image from a generalized VM.</span></span>
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-hello-image"></a><span data-ttu-id="cab70-143">建立 hello 映像</span><span class="sxs-lookup"><span data-stu-id="cab70-143">Create hello image</span></span>

<span data-ttu-id="cab70-144">現在您可以使用，以建立 hello VM 的映像[az 映像建立](/cli//azure/image#create)。</span><span class="sxs-lookup"><span data-stu-id="cab70-144">Now you can create an image of hello VM by using [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="cab70-145">hello 下列範例會建立名為映像*myImage*從名為 VM *myVM*。</span><span class="sxs-lookup"><span data-stu-id="cab70-145">hello following example creates an image named *myImage* from a VM named *myVM*.</span></span>
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-hello-image"></a><span data-ttu-id="cab70-146">從 hello 映像建立 Vm</span><span class="sxs-lookup"><span data-stu-id="cab70-146">Create VMs from hello image</span></span>

<span data-ttu-id="cab70-147">既然您具有映像，您可以建立一或多個新的 Vm 從 hello 映像使用[az vm 建立](/cli/azure/vm#create)。</span><span class="sxs-lookup"><span data-stu-id="cab70-147">Now that you have an image, you can create one or more new VMs from hello image using [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="cab70-148">hello 下列範例會建立名為的 VM *myVMfromImage*從名為 「 hello 」 映像*myImage*。</span><span class="sxs-lookup"><span data-stu-id="cab70-148">hello following example creates a VM named *myVMfromImage* from hello image named *myImage*.</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a><span data-ttu-id="cab70-149">映像管理</span><span class="sxs-lookup"><span data-stu-id="cab70-149">Image management</span></span> 

<span data-ttu-id="cab70-150">以下是一些範例的映像的一般管理工作以及 toocomplete 它們使用 Azure CLI hello。</span><span class="sxs-lookup"><span data-stu-id="cab70-150">Here are some examples of common image management tasks and how toocomplete them using hello Azure CLI.</span></span>

<span data-ttu-id="cab70-151">以資料表格式依名稱列出所有映像。</span><span class="sxs-lookup"><span data-stu-id="cab70-151">List all images by name in a table format.</span></span>

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

<span data-ttu-id="cab70-152">删除映像。</span><span class="sxs-lookup"><span data-stu-id="cab70-152">Delete an image.</span></span> <span data-ttu-id="cab70-153">此範例中刪除 hello 名為映像*myOldImage*從 hello *myResourceGroup*。</span><span class="sxs-lookup"><span data-stu-id="cab70-153">This example deletes hello image named *myOldImage* from hello *myResourceGroup*.</span></span>

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="cab70-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cab70-154">Next steps</span></span>

<span data-ttu-id="cab70-155">您在本教學課程中建立了自訂 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="cab70-155">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="cab70-156">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="cab70-156">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cab70-157">取消佈建及一般化 VM</span><span class="sxs-lookup"><span data-stu-id="cab70-157">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="cab70-158">建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="cab70-158">Create a custom image</span></span>
> * <span data-ttu-id="cab70-159">從自訂映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="cab70-159">Create a VM from a custom image</span></span>
> * <span data-ttu-id="cab70-160">列出您的訂用帳戶中的所有 hello 映像</span><span class="sxs-lookup"><span data-stu-id="cab70-160">List all hello images in your subscription</span></span>
> * <span data-ttu-id="cab70-161">删除映像</span><span class="sxs-lookup"><span data-stu-id="cab70-161">Delete an image</span></span>

<span data-ttu-id="cab70-162">前進 toohello 下一個教學課程的 toolearn 有關高可用性虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="cab70-162">Advance toohello next tutorial toolearn about highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="cab70-163">[建立高可用性 VM](tutorial-availability-sets.md)。</span><span class="sxs-lookup"><span data-stu-id="cab70-163">[Create highly available VMs](tutorial-availability-sets.md).</span></span>

