---
title: "aaaCapture Linux VM 的映像 |Microsoft 文件"
description: "了解如何 toocapture Linux 型 Azure 虛擬機器 (VM) 的映像建立 hello 傳統部署模型。"
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
ms.openlocfilehash: 33c4059d5bb919a86bdc3492abca540750f365ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocapture-a-classic-linux-virtual-machine-as-an-image"></a><span data-ttu-id="ddb01-103">如何 toocapture 傳統 Linux 虛擬機器做為映像</span><span class="sxs-lookup"><span data-stu-id="ddb01-103">How toocapture a classic Linux virtual machine as an image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ddb01-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="ddb01-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ddb01-105">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="ddb01-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="ddb01-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="ddb01-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="ddb01-107">了解如何太[使用 hello 資源管理員的模型執行這些步驟](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="ddb01-107">Learn how too[perform these steps using hello Resource Manager model](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="ddb01-108">本文章將示範如何 toocapture 傳統 Azure 虛擬機器 (VM) 執行 Linux 映像 toocreate 為其他虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ddb01-108">This article shows you how toocapture a classic Azure virtual machine (VM) running Linux as an image toocreate other virtual machines.</span></span> <span data-ttu-id="ddb01-109">此映像包含 hello OS 磁碟和資料磁碟附加 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="ddb01-109">This image includes hello OS disk and data disks attached toohello VM.</span></span> <span data-ttu-id="ddb01-110">它不包含網路設定，因此您需要 tooconfigure，當您建立 hello 其他 VM 從 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="ddb01-110">It doesn't include networking configuration, so you need tooconfigure that when you create hello other VM from hello image.</span></span>

<span data-ttu-id="ddb01-111">Azure 的存放區 hello 下方影像**映像**，以及任何您已上傳的映像。</span><span class="sxs-lookup"><span data-stu-id="ddb01-111">Azure stores hello image under **Images**, along with any images you've uploaded.</span></span> <span data-ttu-id="ddb01-112">如需映像的詳細資訊，請參閱[關於 Azure 中的虛擬機器映像][About Virtual Machine Images in Azure]。</span><span class="sxs-lookup"><span data-stu-id="ddb01-112">For more information about images, see [About Virtual Machine Images in Azure][About Virtual Machine Images in Azure].</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ddb01-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="ddb01-113">Before you begin</span></span>
<span data-ttu-id="ddb01-114">這些步驟假設，您已經建立 Azure VM 使用 hello 傳統部署模型和設定的 hello 作業系統，包括附加的任何資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="ddb01-114">These steps assume that you've already created an Azure VM using hello Classic deployment model and configured hello operating system, including attaching any data disks.</span></span> <span data-ttu-id="ddb01-115">如果您需要 toocreate VM，請閱讀[如何 tooCreate Linux 虛擬機器][How tooCreate a Linux Virtual Machine]。</span><span class="sxs-lookup"><span data-stu-id="ddb01-115">If you need toocreate a VM, read [How tooCreate a Linux Virtual Machine][How tooCreate a Linux Virtual Machine].</span></span>

## <a name="capture-hello-virtual-machine"></a><span data-ttu-id="ddb01-116">擷取 hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ddb01-116">Capture hello virtual machine</span></span>
1. <span data-ttu-id="ddb01-117">[連接 toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)使用您選擇的 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="ddb01-117">[Connect toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) using an SSH client of your choice.</span></span>
2. <span data-ttu-id="ddb01-118">在 hello SSH 視窗中，輸入下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="ddb01-118">In hello SSH window, type hello following command.</span></span> <span data-ttu-id="ddb01-119">從輸出 hello`waagent`根據 hello 版本，此公用程式可能會稍微不同：</span><span class="sxs-lookup"><span data-stu-id="ddb01-119">hello output from `waagent` may vary slightly depending on hello version of this utility:</span></span>

    ```bash
    sudo waagent -deprovision+user
    ```

    <span data-ttu-id="ddb01-120">hello 前述的命令嘗試 tooclean hello 系統，也適合用來重新佈建。</span><span class="sxs-lookup"><span data-stu-id="ddb01-120">hello preceding command attempts tooclean hello system and make it suitable for reprovisioning.</span></span> <span data-ttu-id="ddb01-121">這項作業會執行下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="ddb01-121">This operation performs hello following tasks:</span></span>

   * <span data-ttu-id="ddb01-122">移除 SSH 主機金鑰 （如果 Provisioning.RegenerateSshHostKeyPair 'y' hello 組態檔中）</span><span class="sxs-lookup"><span data-stu-id="ddb01-122">Removes SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in hello configuration file)</span></span>
   * <span data-ttu-id="ddb01-123">清除 /etc/resolv.conf 中的名稱伺服器設定</span><span class="sxs-lookup"><span data-stu-id="ddb01-123">Clears nameserver configuration in /etc/resolv.conf</span></span>
   * <span data-ttu-id="ddb01-124">移除 hello`root`使用者密碼從 /etc/hosts 陰影 （如果 Provisioning.DeleteRootPassword 'y' hello 組態檔中）</span><span class="sxs-lookup"><span data-stu-id="ddb01-124">Removes hello `root` user password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in hello configuration file)</span></span>
   * <span data-ttu-id="ddb01-125">移除快取的 DHCP 用戶端租用</span><span class="sxs-lookup"><span data-stu-id="ddb01-125">Removes cached DHCP client leases</span></span>
   * <span data-ttu-id="ddb01-126">重設主機名稱 toolocalhost.localdomain</span><span class="sxs-lookup"><span data-stu-id="ddb01-126">Resets host name toolocalhost.localdomain</span></span>
   * <span data-ttu-id="ddb01-127">刪除 hello （取自 /var/lib/waagent） 最後一個佈建的使用者帳戶**和相關聯資料**。</span><span class="sxs-lookup"><span data-stu-id="ddb01-127">Deletes hello last provisioned user account (obtained from /var/lib/waagent) **and associated data**.</span></span>

     > [!NOTE]
     > <span data-ttu-id="ddb01-128">取消佈建會刪除檔案和資料太""hello 映像一般化。</span><span class="sxs-lookup"><span data-stu-id="ddb01-128">Deprovisioning deletes files and data too"generalize" hello image.</span></span> <span data-ttu-id="ddb01-129">只執行您想要為新的映像範本 toocapture 此命令在 VM 上。</span><span class="sxs-lookup"><span data-stu-id="ddb01-129">Only run this command on a VM that you intend toocapture as a new image template.</span></span> <span data-ttu-id="ddb01-130">它並不保證該 hello 映像會清除所有的機密資訊或適用於轉散發 toothird 合作對象。</span><span class="sxs-lookup"><span data-stu-id="ddb01-130">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution toothird parties.</span></span>

3. <span data-ttu-id="ddb01-131">型別**y** toocontinue。</span><span class="sxs-lookup"><span data-stu-id="ddb01-131">Type **y** toocontinue.</span></span> <span data-ttu-id="ddb01-132">您可以新增 hello`-force`參數 tooavoid 此確認步驟。</span><span class="sxs-lookup"><span data-stu-id="ddb01-132">You can add hello `-force` parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="ddb01-133">型別**結束**tooclose hello SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="ddb01-133">Type **Exit** tooclose hello SSH client.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ddb01-134">hello 其餘步驟假設您已經有[安裝 hello Azure CLI](../../../cli-install-nodejs.md)用戶端電腦上。</span><span class="sxs-lookup"><span data-stu-id="ddb01-134">hello remaining steps assume you have already [installed hello Azure CLI](../../../cli-install-nodejs.md) on your client computer.</span></span> <span data-ttu-id="ddb01-135">所有步驟的 hello 還可以在 hello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="ddb01-135">All hello following steps can also be done in hello [Azure portal](http://portal.azure.com).</span></span>

5. <span data-ttu-id="ddb01-136">從用戶端電腦，開啟 Azure CLI 和登入 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ddb01-136">From your client computer, open Azure CLI and login tooyour Azure subscription.</span></span> <span data-ttu-id="ddb01-137">如需詳細資訊，請參閱[tooan Azure 訂用帳戶連線從 hello Azure CLI](../../../xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="ddb01-137">For details, read [Connect tooan Azure subscription from hello Azure CLI](../../../xplat-cli-connect.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="ddb01-138">在 hello Azure 入口網站，登入 toohello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="ddb01-138">In hello Azure portal, log in toohello portal.</span></span>

6. <span data-ttu-id="ddb01-139">請確定您是處於服務管理模式中：</span><span class="sxs-lookup"><span data-stu-id="ddb01-139">Make sure you are in Service Management mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

7. <span data-ttu-id="ddb01-140">關閉 hello 已解除佈建的 VM。</span><span class="sxs-lookup"><span data-stu-id="ddb01-140">Shut down hello VM that is already deprovisioned.</span></span> <span data-ttu-id="ddb01-141">hello 下例關閉 hello 名為 VM `myVM`:</span><span class="sxs-lookup"><span data-stu-id="ddb01-141">hello following example shuts down hello VM named `myVM`:</span></span>

    ```azurecli
    azure vm shutdown myVM
    ```
   <span data-ttu-id="ddb01-142">如有需要您可以檢視所有 hello Vm 都建立您的訂用帳戶中使用的清單`azure vm list`</span><span class="sxs-lookup"><span data-stu-id="ddb01-142">If needed, you can view a list all hello VMs created in your subscription by using `azure vm list`</span></span>

   > [!NOTE]
   > <span data-ttu-id="ddb01-143">如果您使用 hello Azure 入口網站，選取 hello VM，然後按一下**停止**關閉 hello VM。</span><span class="sxs-lookup"><span data-stu-id="ddb01-143">If you're using hello Azure portal, select hello VM and click **Stop** to shut down hello VM.</span></span>

8. <span data-ttu-id="ddb01-144">Hello VM 停止時，擷取 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="ddb01-144">When hello VM is stopped, capture hello image.</span></span> <span data-ttu-id="ddb01-145">下列範例會擷取 hello hello 名為 VM`myVM`並建立名為一般化映像`myNewVM`:</span><span class="sxs-lookup"><span data-stu-id="ddb01-145">hello following example captures hello VM named `myVM` and creates a generalized image named `myNewVM`:</span></span>

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    <span data-ttu-id="ddb01-146">hello`-t`刪除 hello 原始虛擬機器的子命令。</span><span class="sxs-lookup"><span data-stu-id="ddb01-146">hello `-t` subcommand deletes hello original virtual machine.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ddb01-147">在 hello Azure 入口網站，您可以藉由選取擷取映像**映像**從 hello 中樞功能表中。</span><span class="sxs-lookup"><span data-stu-id="ddb01-147">In hello Azure portal, you can capture an image by selecting **Image** from hello hub menu.</span></span> <span data-ttu-id="ddb01-148">您需要下列資訊 hello 映像的 toosupply hello： 名稱、 資源群組、 位置、 作業系統類型和儲存體 blob 的路徑。</span><span class="sxs-lookup"><span data-stu-id="ddb01-148">You need toosupply hello following information for hello image: name, resource group, location, operating system type, and storage blob path.</span></span>

9. <span data-ttu-id="ddb01-149">現在在 hello 清單中的映像可能是使用 tooconfigure 任何新的 VM，就會是 hello 新映像。</span><span class="sxs-lookup"><span data-stu-id="ddb01-149">hello new image is now available in hello list of images that can be used tooconfigure any new VM.</span></span> <span data-ttu-id="ddb01-150">您可以檢視它與 hello 命令：</span><span class="sxs-lookup"><span data-stu-id="ddb01-150">You can view it with hello command:</span></span>

   ```azurecli
   azure vm image list
   ```

   <span data-ttu-id="ddb01-151">在 hello [Azure 入口網站](http://portal.azure.com)，hello 新映像會出現在 hello **VM 映像 （傳統）**的所屬 toohello**計算**服務。</span><span class="sxs-lookup"><span data-stu-id="ddb01-151">On hello [Azure portal](http://portal.azure.com), hello new image appears in hello **VM images (classic)** that belongs toohello **Compute** services.</span></span> <span data-ttu-id="ddb01-152">您可以存取**VM 映像 （傳統）**按一下_更多服務_底部 hello hello Azure 服務 清單中，並再查看 hello**計算**服務。</span><span class="sxs-lookup"><span data-stu-id="ddb01-152">You can access **VM images (classic)** by clicking _More services_ at hello bottom of hello Azure service list, and then looking in hello **Compute** services.</span></span>   

   ![成功擷取映像](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="ddb01-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ddb01-154">Next steps</span></span>
<span data-ttu-id="ddb01-155">hello 映像已準備好用的 toobe toocreate Vm。</span><span class="sxs-lookup"><span data-stu-id="ddb01-155">hello image is ready toobe used toocreate VMs.</span></span> <span data-ttu-id="ddb01-156">您可以使用 hello Azure CLI 命令`azure vm create`和您所建立的供應 hello 映像名稱。</span><span class="sxs-lookup"><span data-stu-id="ddb01-156">You can use hello Azure CLI command `azure vm create` and supply hello image name you created.</span></span> <span data-ttu-id="ddb01-157">如需詳細資訊，請參閱[與傳統部署模型使用 hello Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="ddb01-157">For more information, see [Using hello Azure CLI with Classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

<span data-ttu-id="ddb01-158">或者，使用 hello [Azure 入口網站](http://portal.azure.com)toocreate 自訂 VM 使用 hello**映像**方法，然後選取 hello 映像所建立。</span><span class="sxs-lookup"><span data-stu-id="ddb01-158">Alternatively, use hello [Azure portal](http://portal.azure.com) toocreate a custom VM by using hello **Image** method and selecting hello image you created.</span></span> <span data-ttu-id="ddb01-159">如需詳細資訊，請參閱[如何 tooCreate 自訂 VM][How tooCreate a Custom Virtual Machine]。</span><span class="sxs-lookup"><span data-stu-id="ddb01-159">For more information, see [How tooCreate a Custom VM][How tooCreate a Custom Virtual Machine].</span></span>

<span data-ttu-id="ddb01-160">**另請參閱：** [Azure Linux 代理程式使用者指南](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="ddb01-160">**See also:** [Azure Linux Agent User Guide](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How tooCreate a Custom Virtual Machine]:create-custom.md
[How tooAttach a Data Disk tooa Virtual Machine]:attach-disk.md
[How tooCreate a Linux Virtual Machine]:create-custom.md
