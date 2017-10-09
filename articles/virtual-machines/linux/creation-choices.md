---
title: "aaaDifferent 方式 toocreate Azure 中的 Linux VM |Microsoft Azure"
description: "了解 hello 不同的方式 toocreate Azure，包括連結 tootools 和教學課程，每個方法上的 Linux 虛擬機器。"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 250e92c063c87a8c1279097dc2264777d95478d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-linux-vm"></a><span data-ttu-id="13c30-103">不同的方式 toocreate Linux VM</span><span class="sxs-lookup"><span data-stu-id="13c30-103">Different ways toocreate a Linux VM</span></span>
<span data-ttu-id="13c30-104">您擁有 hello 彈性 Azure toocreate 中使用工具和工作流程的舒適 tooyou 在 Linux 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="13c30-104">You have hello flexibility in Azure toocreate a Linux virtual machine (VM) using tools and workflows comfortable tooyou.</span></span> <span data-ttu-id="13c30-105">本文摘要說明這些差異和建立 Linux Vm，包括 hello Azure CLI 2.0 的範例。</span><span class="sxs-lookup"><span data-stu-id="13c30-105">This article summarizes these differences and examples for creating your Linux VMs, including hello Azure CLI 2.0.</span></span> <span data-ttu-id="13c30-106">您也可以檢視建立選項包括 hello [Azure CLI 1.0](creation-choices-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="13c30-106">You can also view creation choices including hello [Azure CLI 1.0](creation-choices-nodejs.md).</span></span>

<span data-ttu-id="13c30-107">hello [Azure CLI 2.0](/cli/azure/install-az-cli2)可跨平台透過 npm 封裝、 distro 提供的封裝或 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="13c30-107">hello [Azure CLI 2.0](/cli/azure/install-az-cli2) is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="13c30-108">安裝您的環境的 hello 最適合組建並 tooan Azure 帳戶使用登入[az 登入](/cli/azure/#login)</span><span class="sxs-lookup"><span data-stu-id="13c30-108">Install hello most appropriate build for your environment and log in tooan Azure account using [az login](/cli/azure/#login)</span></span>

* [<span data-ttu-id="13c30-109">建立 Linux VM 以 hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="13c30-109">Create a Linux VM with hello Azure CLI 2.0</span></span>](quick-create-cli.md)
  
  * <span data-ttu-id="13c30-110">使用名為 myResourceGroup 的 [az group create](/cli/azure/group#create) 來建立資源群組：</span><span class="sxs-lookup"><span data-stu-id="13c30-110">Create a resource group with [az group create](/cli/azure/group#create) named *myResourceGroup*:</span></span> 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * <span data-ttu-id="13c30-111">建立與 VM [az vm 建立](/cli/azure/vm#create)名為*myVM*使用最新 hello *UbuntuLTS*映像，如果它們尚不存在中產生 SSH 金鑰*~/.ssh*:</span><span class="sxs-lookup"><span data-stu-id="13c30-111">Create a VM with [az vm create](/cli/azure/vm#create) named *myVM* using hello latest *UbuntuLTS* image and generate SSH keys if they do not already exist in *~/.ssh*:</span></span>

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [<span data-ttu-id="13c30-112">使用 Azure 範本建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="13c30-112">Create a Linux VM with an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="13c30-113">hello 下列範例會使用[az 群組部署建立](/cli/azure/group/deployment#create)toocreate 將 VM 從 GitHub 上存放的範本：</span><span class="sxs-lookup"><span data-stu-id="13c30-113">hello following example uses [az group deployment create](/cli/azure/group/deployment#create) toocreate a VM from a template stored on GitHub:</span></span>
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [<span data-ttu-id="13c30-114">建立 Linux VM，並使用 cloud-init 進行自訂</span><span class="sxs-lookup"><span data-stu-id="13c30-114">Create a Linux VM and customize with cloud-init</span></span>](tutorial-automate-vm-deployment.md)

* [<span data-ttu-id="13c30-115">在多個 Linux VM 上建立負載平衡和高可用性的應用程式</span><span class="sxs-lookup"><span data-stu-id="13c30-115">Create a load balanced and highly available application on multiple Linux VMs</span></span>](tutorial-load-balancer.md)


## <a name="azure-portal"></a><span data-ttu-id="13c30-116">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="13c30-116">Azure portal</span></span>
<span data-ttu-id="13c30-117">hello [Azure 入口網站](https://portal.azure.com)可讓您 tooquickly 建立 VM，因為沒有任何 tooinstall 您系統上的。</span><span class="sxs-lookup"><span data-stu-id="13c30-117">hello [Azure portal](https://portal.azure.com) allows you tooquickly create a VM since there is nothing tooinstall on your system.</span></span> <span data-ttu-id="13c30-118">使用 hello Azure 入口網站 toocreate hello VM:</span><span class="sxs-lookup"><span data-stu-id="13c30-118">Use hello Azure portal toocreate hello VM:</span></span>

* [<span data-ttu-id="13c30-119">建立 Linux VM 使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="13c30-119">Create a Linux VM using hello Azure portal</span></span>](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a><span data-ttu-id="13c30-120">作業系統和映像選項</span><span class="sxs-lookup"><span data-stu-id="13c30-120">Operating system and image choices</span></span>
<span data-ttu-id="13c30-121">在建立 VM 時，您可以選擇根據 hello 想 toorun 作業系統映像。</span><span class="sxs-lookup"><span data-stu-id="13c30-121">When creating a VM, you choose an image based on hello operating system you want toorun.</span></span> <span data-ttu-id="13c30-122">Azure 與其合作夥伴提供許多映像，其中有些包括已預先安裝的應用程式和工具。</span><span class="sxs-lookup"><span data-stu-id="13c30-122">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="13c30-123">或者，您也可以上傳自己的映像的其中一個 (請參閱[hello 下列區段](#use-your-own-image))。</span><span class="sxs-lookup"><span data-stu-id="13c30-123">Or, upload one of your own images (see [hello following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="13c30-124">Azure 映像</span><span class="sxs-lookup"><span data-stu-id="13c30-124">Azure images</span></span>
<span data-ttu-id="13c30-125">使用 hello [az vm 映像](/cli/azure/vm/image)命令 toosee 可用的發行者、 distro 版本和組建。</span><span class="sxs-lookup"><span data-stu-id="13c30-125">Use hello [az vm image](/cli/azure/vm/image) commands toosee what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="13c30-126">列出可用的發佈者：</span><span class="sxs-lookup"><span data-stu-id="13c30-126">List available publishers:</span></span>

```azurecli
az vm image list-publishers --location eastus
```

<span data-ttu-id="13c30-127">列出特定發佈者的可用產品 (提供項目)︰</span><span class="sxs-lookup"><span data-stu-id="13c30-127">List available products (offers) for a given publisher:</span></span>

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

<span data-ttu-id="13c30-128">清單特定提供項目的可用 SKU (散發版本)︰</span><span class="sxs-lookup"><span data-stu-id="13c30-128">List available SKUs (distro releases) of a given offer:</span></span>

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

<span data-ttu-id="13c30-129">列出特定版本的所有可用映像︰</span><span class="sxs-lookup"><span data-stu-id="13c30-129">List all available images for a given release:</span></span>

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

<span data-ttu-id="13c30-130">瀏覽和使用可用的映像的詳細範例，請參閱[瀏覽並選取 Azure 虛擬機器映像以 hello Azure CLI](cli-ps-findimage.md)。</span><span class="sxs-lookup"><span data-stu-id="13c30-130">For more examples on browsing and using available images, see [Navigate and select Azure virtual machine images with hello Azure CLI](cli-ps-findimage.md).</span></span>

<span data-ttu-id="13c30-131">hello [az vm 建立](/cli/azure/vm#create)命令有別名，您可以使用 tooquickly 存取 hello 較常見的散發版本，其最新版本。</span><span class="sxs-lookup"><span data-stu-id="13c30-131">hello [az vm create](/cli/azure/vm#create) command has aliases you can use tooquickly access hello more common distros and their latest releases.</span></span> <span data-ttu-id="13c30-132">使用別名，通常會快於每次當您建立的 VM 指定 hello 發行者、 方案、 SKU 和版本：</span><span class="sxs-lookup"><span data-stu-id="13c30-132">Using aliases is often quicker than specifying hello publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="13c30-133">Alias</span><span class="sxs-lookup"><span data-stu-id="13c30-133">Alias</span></span> | <span data-ttu-id="13c30-134">發佈者</span><span class="sxs-lookup"><span data-stu-id="13c30-134">Publisher</span></span> | <span data-ttu-id="13c30-135">提供項目</span><span class="sxs-lookup"><span data-stu-id="13c30-135">Offer</span></span> | <span data-ttu-id="13c30-136">SKU</span><span class="sxs-lookup"><span data-stu-id="13c30-136">SKU</span></span> | <span data-ttu-id="13c30-137">版本</span><span class="sxs-lookup"><span data-stu-id="13c30-137">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="13c30-138">CentOS</span><span class="sxs-lookup"><span data-stu-id="13c30-138">CentOS</span></span> |<span data-ttu-id="13c30-139">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="13c30-139">OpenLogic</span></span> |<span data-ttu-id="13c30-140">Centos</span><span class="sxs-lookup"><span data-stu-id="13c30-140">Centos</span></span> |<span data-ttu-id="13c30-141">7.2</span><span class="sxs-lookup"><span data-stu-id="13c30-141">7.2</span></span> |<span data-ttu-id="13c30-142">最新</span><span class="sxs-lookup"><span data-stu-id="13c30-142">latest</span></span> |
| <span data-ttu-id="13c30-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="13c30-143">CoreOS</span></span> |<span data-ttu-id="13c30-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="13c30-144">CoreOS</span></span> |<span data-ttu-id="13c30-145">CoreOS</span><span class="sxs-lookup"><span data-stu-id="13c30-145">CoreOS</span></span> |<span data-ttu-id="13c30-146">Stable</span><span class="sxs-lookup"><span data-stu-id="13c30-146">Stable</span></span> |<span data-ttu-id="13c30-147">最新</span><span class="sxs-lookup"><span data-stu-id="13c30-147">latest</span></span> |
| <span data-ttu-id="13c30-148">Debian</span><span class="sxs-lookup"><span data-stu-id="13c30-148">Debian</span></span> |<span data-ttu-id="13c30-149">credativ</span><span class="sxs-lookup"><span data-stu-id="13c30-149">credativ</span></span> |<span data-ttu-id="13c30-150">Debian</span><span class="sxs-lookup"><span data-stu-id="13c30-150">Debian</span></span> |<span data-ttu-id="13c30-151">8</span><span class="sxs-lookup"><span data-stu-id="13c30-151">8</span></span> |<span data-ttu-id="13c30-152">最新</span><span class="sxs-lookup"><span data-stu-id="13c30-152">latest</span></span> |
| <span data-ttu-id="13c30-153">openSUSE</span><span class="sxs-lookup"><span data-stu-id="13c30-153">openSUSE</span></span> |<span data-ttu-id="13c30-154">SUSE</span><span class="sxs-lookup"><span data-stu-id="13c30-154">SUSE</span></span> |<span data-ttu-id="13c30-155">openSUSE</span><span class="sxs-lookup"><span data-stu-id="13c30-155">openSUSE</span></span> |<span data-ttu-id="13c30-156">13.2</span><span class="sxs-lookup"><span data-stu-id="13c30-156">13.2</span></span> |<span data-ttu-id="13c30-157">最新</span><span class="sxs-lookup"><span data-stu-id="13c30-157">latest</span></span> |
| <span data-ttu-id="13c30-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="13c30-158">RHEL</span></span> |<span data-ttu-id="13c30-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="13c30-159">Redhat</span></span> |<span data-ttu-id="13c30-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="13c30-160">RHEL</span></span> |<span data-ttu-id="13c30-161">7.2</span><span class="sxs-lookup"><span data-stu-id="13c30-161">7.2</span></span> |<span data-ttu-id="13c30-162">最新</span><span class="sxs-lookup"><span data-stu-id="13c30-162">latest</span></span> |
| <span data-ttu-id="13c30-163">SLES</span><span class="sxs-lookup"><span data-stu-id="13c30-163">SLES</span></span> |<span data-ttu-id="13c30-164">SLES</span><span class="sxs-lookup"><span data-stu-id="13c30-164">SLES</span></span> |<span data-ttu-id="13c30-165">SLES</span><span class="sxs-lookup"><span data-stu-id="13c30-165">SLES</span></span> |<span data-ttu-id="13c30-166">12-SP1</span><span class="sxs-lookup"><span data-stu-id="13c30-166">12-SP1</span></span> |<span data-ttu-id="13c30-167">最新</span><span class="sxs-lookup"><span data-stu-id="13c30-167">latest</span></span> |
| <span data-ttu-id="13c30-168">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="13c30-168">UbuntuLTS</span></span> |<span data-ttu-id="13c30-169">Canonical</span><span class="sxs-lookup"><span data-stu-id="13c30-169">Canonical</span></span> |<span data-ttu-id="13c30-170">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="13c30-170">UbuntuServer</span></span> |<span data-ttu-id="13c30-171">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="13c30-171">14.04.4-LTS</span></span> |<span data-ttu-id="13c30-172">最新</span><span class="sxs-lookup"><span data-stu-id="13c30-172">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="13c30-173">使用您自己的映像</span><span class="sxs-lookup"><span data-stu-id="13c30-173">Use your own image</span></span>
<span data-ttu-id="13c30-174">如果您需要特定的自訂，可以擷取該 VM，根據現有的 Azure VM 使用映像。</span><span class="sxs-lookup"><span data-stu-id="13c30-174">If you require specific customizations, you can use an image based on an existing Azure VM by capturing that VM.</span></span> <span data-ttu-id="13c30-175">也可以上傳在內部部署建立的映像。</span><span class="sxs-lookup"><span data-stu-id="13c30-175">You can also upload an image created on-premises.</span></span> <span data-ttu-id="13c30-176">如需有關支援的散發版本以及如何 toouse 自己的映像，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="13c30-176">For more information on supported distros and how toouse your own images, see hello following articles:</span></span>

* [<span data-ttu-id="13c30-177">Azure 背書的散發套件</span><span class="sxs-lookup"><span data-stu-id="13c30-177">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="13c30-178">非背書散發套件的資訊</span><span class="sxs-lookup"><span data-stu-id="13c30-178">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* <span data-ttu-id="13c30-179">[如何從現有的 Azure VM 映像 toocreate](tutorial-custom-images.md)。</span><span class="sxs-lookup"><span data-stu-id="13c30-179">[How toocreate an image from an existing Azure VM](tutorial-custom-images.md).</span></span>
  
  * <span data-ttu-id="13c30-180">快速入門範例命令 toocreate 從現有的 Azure VM 映像：</span><span class="sxs-lookup"><span data-stu-id="13c30-180">Quick-start example commands toocreate an image from an existing Azure VM:</span></span>
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a><span data-ttu-id="13c30-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="13c30-181">Next steps</span></span>
* <span data-ttu-id="13c30-182">建立 Linux VM 以 hello [CLI](quick-create-cli.md)，從 hello[入口網站](quick-create-portal.md)，或使用[Azure Resource Manager 範本](../windows/cli-deploy-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="13c30-182">Create a Linux VM with hello [CLI](quick-create-cli.md), from hello [portal](quick-create-portal.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="13c30-183">建立 Linux VM 之後，[深入了解 Azure 磁碟與儲存體](tutorial-manage-disks.md)。</span><span class="sxs-lookup"><span data-stu-id="13c30-183">After creating a Linux VM, [learn about Azure disks and storage](tutorial-manage-disks.md).</span></span>
* <span data-ttu-id="13c30-184">快速步驟太[重設密碼或 SSH 金鑰，以及管理使用者](using-vmaccess-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="13c30-184">Quick steps too[reset a password or SSH keys and manage users](using-vmaccess-extension.md).</span></span>
