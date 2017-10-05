---
title: "擷取 Linux VM 的映像 | Microsoft Docs"
description: "了解如何對以傳統部署模型建立的 Linux Azure 虛擬機器 (VM) 擷取映像。"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: ecde5dd3211bfbb290e6910d7d55136d079c6cf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-capture-a-classic-linux-virtual-machine-as-an-image"></a><span data-ttu-id="b6033-103">如何將傳統 Linux 虛擬機器擷取成映像</span><span class="sxs-lookup"><span data-stu-id="b6033-103">How to capture a classic Linux virtual machine as an image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b6033-104">Azure 建立和處理資源的部署模型有二種： [Resource Manager 和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="b6033-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b6033-105">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="b6033-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="b6033-106">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="b6033-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="b6033-107">了解如何[使用 Resource Manager 模型執行這些步驟](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b6033-107">Learn how to [perform these steps using the Resource Manager model](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b6033-108">本文說明如何將執行 Linux 的傳統 Azure 虛擬機器 (VM) 擷取成映像，以建立其他虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b6033-108">This article shows you how to capture a classic Azure virtual machine (VM) running Linux as an image to create other virtual machines.</span></span> <span data-ttu-id="b6033-109">此映像包含作業系統磁碟和連結至虛擬機器的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="b6033-109">This image includes the OS disk and data disks attached to the VM.</span></span> <span data-ttu-id="b6033-110">它並不包含網路組態，因此當您從此映像建立其他 VM 時，將需要設定該組態。</span><span class="sxs-lookup"><span data-stu-id="b6033-110">It doesn't include networking configuration, so you need to configure that when you create the other VM from the image.</span></span>

<span data-ttu-id="b6033-111">Azure 會將映像儲存在 [映像] 底下，連同您已上傳的任何映像。</span><span class="sxs-lookup"><span data-stu-id="b6033-111">Azure stores the image under **Images**, along with any images you've uploaded.</span></span> <span data-ttu-id="b6033-112">如需映像的詳細資訊，請參閱[關於 Azure 中的虛擬機器映像][About Virtual Machine Images in Azure]。</span><span class="sxs-lookup"><span data-stu-id="b6033-112">For more information about images, see [About Virtual Machine Images in Azure][About Virtual Machine Images in Azure].</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b6033-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="b6033-113">Before you begin</span></span>
<span data-ttu-id="b6033-114">這些步驟假設您已使用傳統部署模型建立 Azure VM，並設定好作業系統，包括連接任何資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="b6033-114">These steps assume that you've already created an Azure VM using the Classic deployment model and configured the operating system, including attaching any data disks.</span></span> <span data-ttu-id="b6033-115">如果您需要建立 VM，請閱讀[如何建立 Linux 虛擬機器][How to Create a Linux Virtual Machine]。</span><span class="sxs-lookup"><span data-stu-id="b6033-115">If you need to create a VM, read [How to Create a Linux Virtual Machine][How to Create a Linux Virtual Machine].</span></span>

## <a name="capture-the-virtual-machine"></a><span data-ttu-id="b6033-116">擷取虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b6033-116">Capture the virtual machine</span></span>
1. <span data-ttu-id="b6033-117">使用您所選擇的 SSH 用戶端來[連接到 VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b6033-117">[Connect to the VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) using an SSH client of your choice.</span></span>
2. <span data-ttu-id="b6033-118">在 SSH 視窗中，輸入下列命令。</span><span class="sxs-lookup"><span data-stu-id="b6033-118">In the SSH window, type the following command.</span></span> <span data-ttu-id="b6033-119">來自 `waagent` 的輸出可能會依此公用程式的版本而稍有不同：</span><span class="sxs-lookup"><span data-stu-id="b6033-119">The output from `waagent` may vary slightly depending on the version of this utility:</span></span>

    ```bash
    sudo waagent -deprovision+user
    ```

    <span data-ttu-id="b6033-120">上述命令會嘗試清除系統，使之適合重新佈建。</span><span class="sxs-lookup"><span data-stu-id="b6033-120">The preceding command attempts to clean the system and make it suitable for reprovisioning.</span></span> <span data-ttu-id="b6033-121">這項作業會執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="b6033-121">This operation performs the following tasks:</span></span>

   * <span data-ttu-id="b6033-122">移除 SSH 主機金鑰 (如果組態檔中的 Provisioning.RegenerateSshHostKeyPair 是 'y')</span><span class="sxs-lookup"><span data-stu-id="b6033-122">Removes SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in the configuration file)</span></span>
   * <span data-ttu-id="b6033-123">清除 /etc/resolv.conf 中的名稱伺服器設定</span><span class="sxs-lookup"><span data-stu-id="b6033-123">Clears nameserver configuration in /etc/resolv.conf</span></span>
   * <span data-ttu-id="b6033-124">移除 /etc/shadow 中的 `root` 使用者密碼 (如果組態檔中的 Provisioning.DeleteRootPassword 是 'y')</span><span class="sxs-lookup"><span data-stu-id="b6033-124">Removes the `root` user password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in the configuration file)</span></span>
   * <span data-ttu-id="b6033-125">移除快取的 DHCP 用戶端租用</span><span class="sxs-lookup"><span data-stu-id="b6033-125">Removes cached DHCP client leases</span></span>
   * <span data-ttu-id="b6033-126">將主機名稱重設為 localhost.localdomain</span><span class="sxs-lookup"><span data-stu-id="b6033-126">Resets host name to localhost.localdomain</span></span>
   * <span data-ttu-id="b6033-127">刪除最後佈建的使用者帳戶 (取自於 /var/lib/waagent) **和相關聯的資料**。</span><span class="sxs-lookup"><span data-stu-id="b6033-127">Deletes the last provisioned user account (obtained from /var/lib/waagent) **and associated data**.</span></span>

     > [!NOTE]
     > <span data-ttu-id="b6033-128">解除佈建會將檔案和資料刪除以將映像「一般化」。</span><span class="sxs-lookup"><span data-stu-id="b6033-128">Deprovisioning deletes files and data to "generalize" the image.</span></span> <span data-ttu-id="b6033-129">請只在您想要擷取做為新映像範本的 VM 上執行這個命令。</span><span class="sxs-lookup"><span data-stu-id="b6033-129">Only run this command on a VM that you intend to capture as a new image template.</span></span> <span data-ttu-id="b6033-130">這不能保證映像檔中的所有機密資訊都會清除完畢或適合轉散發給第三方。</span><span class="sxs-lookup"><span data-stu-id="b6033-130">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution to third parties.</span></span>

3. <span data-ttu-id="b6033-131">輸入 **y** 繼續。</span><span class="sxs-lookup"><span data-stu-id="b6033-131">Type **y** to continue.</span></span> <span data-ttu-id="b6033-132">您可以新增 `-force` 參數，便不用進行此確認步驟。</span><span class="sxs-lookup"><span data-stu-id="b6033-132">You can add the `-force` parameter to avoid this confirmation step.</span></span>
4. <span data-ttu-id="b6033-133">輸入 **Exit** 關閉 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="b6033-133">Type **Exit** to close the SSH client.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b6033-134">其餘步驟會假設您已經在用戶端電腦上[安裝 Azure CLI](../../../cli-install-nodejs.md) 。</span><span class="sxs-lookup"><span data-stu-id="b6033-134">The remaining steps assume you have already [installed the Azure CLI](../../../cli-install-nodejs.md) on your client computer.</span></span> <span data-ttu-id="b6033-135">您也可以在 [Azure 入口網站](http://portal.azure.com)中完成接下來的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="b6033-135">All the following steps can also be done in the [Azure portal](http://portal.azure.com).</span></span>

5. <span data-ttu-id="b6033-136">從用戶端電腦，開啟 Azure CLI 並登入您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b6033-136">From your client computer, open Azure CLI and login to your Azure subscription.</span></span> <span data-ttu-id="b6033-137">如需詳細資料，請閱讀[從 Azure CLI 連接到 Azure 訂用帳戶](../../../xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="b6033-137">For details, read [Connect to an Azure subscription from the Azure CLI](../../../xplat-cli-connect.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="b6033-138">在 Azure 入口網站中，登入入口網站。</span><span class="sxs-lookup"><span data-stu-id="b6033-138">In the Azure portal, log in to the portal.</span></span>

6. <span data-ttu-id="b6033-139">請確定您是處於服務管理模式中：</span><span class="sxs-lookup"><span data-stu-id="b6033-139">Make sure you are in Service Management mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

7. <span data-ttu-id="b6033-140">關閉已取消佈建的 VM。</span><span class="sxs-lookup"><span data-stu-id="b6033-140">Shut down the VM that is already deprovisioned.</span></span> <span data-ttu-id="b6033-141">下列範例會關閉名為 `myVM` 的 VM：</span><span class="sxs-lookup"><span data-stu-id="b6033-141">The following example shuts down the VM named `myVM`:</span></span>

    ```azurecli
    azure vm shutdown myVM
    ```
   <span data-ttu-id="b6033-142">如有需要，您可以使用 `azure vm list`，檢視在您的訂用帳戶中建立的所有 VM</span><span class="sxs-lookup"><span data-stu-id="b6033-142">If needed, you can view a list all the VMs created in your subscription by using `azure vm list`</span></span>

   > [!NOTE]
   > <span data-ttu-id="b6033-143">如果您使用 Azure 入口網站，請選取 VM，然後按一下 [停止] 來關閉 VM。</span><span class="sxs-lookup"><span data-stu-id="b6033-143">If you're using the Azure portal, select the VM and click **Stop** to shut down the VM.</span></span>

8. <span data-ttu-id="b6033-144">當 VM 停止時，擷取映像。</span><span class="sxs-lookup"><span data-stu-id="b6033-144">When the VM is stopped, capture the image.</span></span> <span data-ttu-id="b6033-145">下列範例會擷取名為 `myVM` 的 VM，並建立名為 `myNewVM` 的一般化映像：</span><span class="sxs-lookup"><span data-stu-id="b6033-145">The following example captures the VM named `myVM` and creates a generalized image named `myNewVM`:</span></span>

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    <span data-ttu-id="b6033-146">`-t` 子命令會刪除原本的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b6033-146">The `-t` subcommand deletes the original virtual machine.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b6033-147">在 Azure 入口網站中，您可以從中樞功能表選取 [映像] 來擷取映像。</span><span class="sxs-lookup"><span data-stu-id="b6033-147">In the Azure portal, you can capture an image by selecting **Image** from the hub menu.</span></span> <span data-ttu-id="b6033-148">您需要提供映像的下列資訊：名稱、資源群組、位置、作業系統類型和儲存體 Blob 路徑。</span><span class="sxs-lookup"><span data-stu-id="b6033-148">You need to supply the following information for the image: name, resource group, location, operating system type, and storage blob path.</span></span>

9. <span data-ttu-id="b6033-149">新的映像現在可從映像清單中取得，且可用來設定任何新的 VM。</span><span class="sxs-lookup"><span data-stu-id="b6033-149">The new image is now available in the list of images that can be used to configure any new VM.</span></span> <span data-ttu-id="b6033-150">您可以使用下列命令進行檢視：</span><span class="sxs-lookup"><span data-stu-id="b6033-150">You can view it with the command:</span></span>

   ```azurecli
   azure vm image list
   ```

   <span data-ttu-id="b6033-151">在 [Azure 入口網站](http://portal.azure.com) 上，新的映像會出現在屬於 [計算] 服務的 [VM 映像 (傳統)] 中。</span><span class="sxs-lookup"><span data-stu-id="b6033-151">On the [Azure portal](http://portal.azure.com), the new image appears in the **VM images (classic)** that belongs to the **Compute** services.</span></span> <span data-ttu-id="b6033-152">您可以按一下 Azure 服務清單底部的 [更多服務]，接著查看 [計算] 服務，來存取 [VM 映像 (傳統)]。</span><span class="sxs-lookup"><span data-stu-id="b6033-152">You can access **VM images (classic)** by clicking _More services_ at the bottom of the Azure service list, and then looking in the **Compute** services.</span></span>   

   ![成功擷取映像](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="b6033-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b6033-154">Next steps</span></span>
<span data-ttu-id="b6033-155">映像已準備好用來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="b6033-155">The image is ready to be used to create VMs.</span></span> <span data-ttu-id="b6033-156">您可以使用 Azure CLI 命令 `azure vm create`，並提供您已建立的映像名稱。</span><span class="sxs-lookup"><span data-stu-id="b6033-156">You can use the Azure CLI command `azure vm create` and supply the image name you created.</span></span> <span data-ttu-id="b6033-157">如需詳細資訊，請參閱[搭配使用 Azure CLI 與傳統部署模型](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="b6033-157">For more information, see [Using the Azure CLI with Classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

<span data-ttu-id="b6033-158">或者，您也可以透過 [Azure 入口網站](http://portal.azure.com)，使用 [映像] 方法並選取您已建立的映像來建立自訂 VM。</span><span class="sxs-lookup"><span data-stu-id="b6033-158">Alternatively, use the [Azure portal](http://portal.azure.com) to create a custom VM by using the **Image** method and selecting the image you created.</span></span> <span data-ttu-id="b6033-159">如需詳細資訊，請參閱[如何建立自訂 VM][How to Create a Custom Virtual Machine]。</span><span class="sxs-lookup"><span data-stu-id="b6033-159">For more information, see [How to Create a Custom VM][How to Create a Custom Virtual Machine].</span></span>

<span data-ttu-id="b6033-160">**另請參閱：** [Azure Linux 代理程式使用者指南](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="b6033-160">**See also:** [Azure Linux Agent User Guide](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How to Create a Custom Virtual Machine]:create-custom.md
[How to Attach a Data Disk to a Virtual Machine]:attach-disk.md
[How to Create a Linux Virtual Machine]:create-custom.md
