---
title: "一份您的 Linux VM 以 hello Azure CLI 1.0 aaaCreate |Microsoft 文件"
description: "了解與您 Azure Linux 虛擬機器的複本 toocreate 如何 hello Azure CLI 1.0 hello Resource Manager 部署模型中"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 997a2c8109e7083ececd76fd1013e9ed4d3e6afd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-hello-azure-cli-10"></a><span data-ttu-id="04ded-103">建立 hello Azure CLI 1.0 使用在 Azure 上執行的 Linux 虛擬機器的複本</span><span class="sxs-lookup"><span data-stu-id="04ded-103">Create a copy of a Linux virtual machine running on Azure with hello Azure CLI 1.0</span></span>
<span data-ttu-id="04ded-104">本文章將示範如何 toocreate 程式 Azure 虛擬機器 (VM) 執行 Linux，請使用一份 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="04ded-104">This article shows you how toocreate a copy of your Azure virtual machine (VM) running Linux using hello Resource Manager deployment model.</span></span> <span data-ttu-id="04ded-105">第一次您已複製 hello 作業系統和資料磁碟 tooa 新的容器，然後設定 hello 網路資源並建立新虛擬機器 hello。</span><span class="sxs-lookup"><span data-stu-id="04ded-105">First you copy over hello operating system and data disks tooa new container, then set up hello network resources and create hello new virtual machine.</span></span>

<span data-ttu-id="04ded-106">您也可以[上傳自訂磁碟映像並從這個映像建立 VM](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="04ded-106">You can also [upload and create a VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="04ded-107">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="04ded-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="04ded-108">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="04ded-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="04ded-109">Azure CLI 1.0 – 我們 CLI hello 傳統和資源管理部署模型 （此文件）</span><span class="sxs-lookup"><span data-stu-id="04ded-109">Azure CLI 1.0 – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="04ded-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -hello 資源管理部署模型我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="04ded-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="04ded-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="04ded-111">Before you begin</span></span>
<span data-ttu-id="04ded-112">請確定您符合下列必要條件再啟動 hello 步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="04ded-112">Ensure that you meet hello following prerequisites before you start hello steps:</span></span>

* <span data-ttu-id="04ded-113">您已擁有 hello [Azure CLI](../../cli-install-nodejs.md)下載並安裝在您的電腦。</span><span class="sxs-lookup"><span data-stu-id="04ded-113">You have hello [Azure CLI](../../cli-install-nodejs.md) downloaded and installed on your machine.</span></span> 
* <span data-ttu-id="04ded-114">您也需要現有 Azure Linux VM 的一些相關資訊：</span><span class="sxs-lookup"><span data-stu-id="04ded-114">You also need some information about your existing Azure Linux VM:</span></span>

| <span data-ttu-id="04ded-115">來源 VM 資訊</span><span class="sxs-lookup"><span data-stu-id="04ded-115">Source VM information</span></span> | <span data-ttu-id="04ded-116">其中 tooget 它</span><span class="sxs-lookup"><span data-stu-id="04ded-116">Where tooget it</span></span> |
| --- | --- |
| <span data-ttu-id="04ded-117">VM 名稱</span><span class="sxs-lookup"><span data-stu-id="04ded-117">VM name</span></span> |`azure vm list` |
| <span data-ttu-id="04ded-118">資源群組名稱</span><span class="sxs-lookup"><span data-stu-id="04ded-118">Resource Group name</span></span> |`azure vm list` |
| <span data-ttu-id="04ded-119">位置</span><span class="sxs-lookup"><span data-stu-id="04ded-119">Location</span></span> |`azure vm list` |
| <span data-ttu-id="04ded-120">儲存體帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="04ded-120">Storage Account name</span></span> |`azure storage account list -g <resourceGroup>` |
| <span data-ttu-id="04ded-121">容器名稱</span><span class="sxs-lookup"><span data-stu-id="04ded-121">Container name</span></span> |`azure storage container list -a <sourcestorageaccountname>` |
| <span data-ttu-id="04ded-122">來源 VM VHD 檔案名稱</span><span class="sxs-lookup"><span data-stu-id="04ded-122">Source VM VHD file name</span></span> |`azure storage blob list --container <containerName>` |

* <span data-ttu-id="04ded-123">您將有關新的 VM 需要 toomake 一些選項：   </span><span class="sxs-lookup"><span data-stu-id="04ded-123">You will need toomake some choices about your new VM:    </span></span><br> <span data-ttu-id="04ded-124">-容器名稱    </span><span class="sxs-lookup"><span data-stu-id="04ded-124">-Container name    </span></span><br> <span data-ttu-id="04ded-125">-VM 名稱    </span><span class="sxs-lookup"><span data-stu-id="04ded-125">-VM name    </span></span><br> <span data-ttu-id="04ded-126">-VM 大小    </span><span class="sxs-lookup"><span data-stu-id="04ded-126">-VM size    </span></span><br> <span data-ttu-id="04ded-127">-vNet 名稱    </span><span class="sxs-lookup"><span data-stu-id="04ded-127">-vNet name    </span></span><br> <span data-ttu-id="04ded-128">-SubNet 名稱    </span><span class="sxs-lookup"><span data-stu-id="04ded-128">-SubNet name    </span></span><br> <span data-ttu-id="04ded-129">-IP 名稱    </span><span class="sxs-lookup"><span data-stu-id="04ded-129">-IP Name    </span></span><br> <span data-ttu-id="04ded-130">-NIC 名稱</span><span class="sxs-lookup"><span data-stu-id="04ded-130">-NIC name</span></span>

## <a name="login-and-set-your-subscription"></a><span data-ttu-id="04ded-131">登入及設定您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="04ded-131">Login and set your subscription</span></span>
1. <span data-ttu-id="04ded-132">登入 toohello CLI。</span><span class="sxs-lookup"><span data-stu-id="04ded-132">Login toohello CLI.</span></span>

    ```azurecli
    azure login
    ```
2. <span data-ttu-id="04ded-133">確定您處於 Resource Manager 模式。</span><span class="sxs-lookup"><span data-stu-id="04ded-133">Make sure you are in Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="04ded-134">設定 hello 正確的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="04ded-134">Set hello correct subscription.</span></span> <span data-ttu-id="04ded-135">您可以使用 '的 azure 帳戶 list' toosee 您所有的訂閱。</span><span class="sxs-lookup"><span data-stu-id="04ded-135">You can use 'azure account list' toosee all of your subscriptions.</span></span>

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-hello-vm"></a><span data-ttu-id="04ded-136">停止 hello VM</span><span class="sxs-lookup"><span data-stu-id="04ded-136">Stop hello VM</span></span>
<span data-ttu-id="04ded-137">停止並取消配置 hello 來源 VM。</span><span class="sxs-lookup"><span data-stu-id="04ded-137">Stop and deallocate hello source VM.</span></span> <span data-ttu-id="04ded-138">您可以使用 'azure vm list' tooget 所有 hello Vm 的清單中訂用帳戶及資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="04ded-138">You can use 'azure vm list' tooget a list of all of hello VMs in your subscription and their resource group names.</span></span>

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-hello-vhd"></a><span data-ttu-id="04ded-139">複製 hello VHD</span><span class="sxs-lookup"><span data-stu-id="04ded-139">Copy hello VHD</span></span>
<span data-ttu-id="04ded-140">您可以從 hello 來源儲存體 toohello 目的地使用 hello 複製 hello VHD `azure storage blob copy start`。</span><span class="sxs-lookup"><span data-stu-id="04ded-140">You can copy hello VHD from hello source storage toohello destination using hello `azure storage blob copy start`.</span></span> <span data-ttu-id="04ded-141">在此範例中，我們會 toocopy hello VHD toohello 相同的儲存體帳戶，但不同的容器。</span><span class="sxs-lookup"><span data-stu-id="04ded-141">In this example, we are going toocopy hello VHD toohello same storage account, but a different container.</span></span>

<span data-ttu-id="04ded-142">在 hello toocopy hello VHD tooanother 容器相同的儲存體帳戶中，輸入：</span><span class="sxs-lookup"><span data-stu-id="04ded-142">toocopy hello VHD tooanother container in hello same storage account, type:</span></span>

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-hello-virtual-network-for-your-new-vm"></a><span data-ttu-id="04ded-143">新的 vm 設定 hello 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="04ded-143">Set up hello virtual network for your new VM</span></span>
<span data-ttu-id="04ded-144">為新 VM 設定虛擬網路和 NIC。</span><span class="sxs-lookup"><span data-stu-id="04ded-144">Set up a virtual network and NIC for your new VM.</span></span> 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-hello-new-vm"></a><span data-ttu-id="04ded-145">建立 hello 新的 VM</span><span class="sxs-lookup"><span data-stu-id="04ded-145">Create hello new VM</span></span>
<span data-ttu-id="04ded-146">您現在可以從已上傳虛擬硬碟建立 VM[使用資源管理員範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd)或藉由指定 hello URI tooyour CLI hello 透過輸入複製磁碟：</span><span class="sxs-lookup"><span data-stu-id="04ded-146">You can now create a VM from your uploaded virtual disk [using a resource manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) or through hello CLI by specifying hello URI tooyour copied disk by typing:</span></span>

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a><span data-ttu-id="04ded-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="04ded-147">Next steps</span></span>
<span data-ttu-id="04ded-148">toolearn 如何 toouse Azure CLI toomanage 新的虛擬機器，請參閱[hello Azure 資源管理員的 Azure CLI 命令](../azure-cli-arm-commands.md)。</span><span class="sxs-lookup"><span data-stu-id="04ded-148">toolearn how toouse Azure CLI toomanage your new virtual machine, see [Azure CLI commands for hello Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>

