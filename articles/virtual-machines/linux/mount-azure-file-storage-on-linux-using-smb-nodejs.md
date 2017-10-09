---
title: "aaaMount Linux Vm 上使用 SMB 與 Azure CLI 1.0 的 Azure 檔案儲存體 |Microsoft 文件"
description: "如何 toomount Linux Vm 上使用 SMB 的 Azure 檔案儲存體"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/07/2016
ms.author: v-livech
ms.openlocfilehash: 14a4224228cadb0ae2f05e8e5c8022ee84f138a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a><span data-ttu-id="597bf-103">透過 Azure CLI 1.0 使用 SMB 在 Linux VM 上掛接 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="597bf-103">Mount Azure File storage on Linux VMs by using SMB with Azure CLI 1.0</span></span>

<span data-ttu-id="597bf-104">本文示範如何使用 Linux VM 上的 Azure 檔案儲存體 toomount hello 伺服器訊息區塊 (SMB) 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="597bf-104">This article shows how toomount Azure File storage on a Linux VM by using hello Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="597bf-105">檔案存放裝置提供透過 hello 標準 SMB 通訊協定的 hello 雲端中的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="597bf-105">File storage offers file shares in hello cloud via hello standard SMB protocol.</span></span> <span data-ttu-id="597bf-106">hello 需求如下：</span><span class="sxs-lookup"><span data-stu-id="597bf-106">hello requirements are:</span></span>

* <span data-ttu-id="597bf-107">[Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="597bf-107">An [Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* [<span data-ttu-id="597bf-108">安全殼層 (SSH) 公開金鑰和私密金鑰檔案</span><span class="sxs-lookup"><span data-stu-id="597bf-108">Secure Shell (SSH) public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="cli-versions-toouse"></a><span data-ttu-id="597bf-109">CLI 版本 toouse</span><span class="sxs-lookup"><span data-stu-id="597bf-109">CLI versions toouse</span></span>
<span data-ttu-id="597bf-110">您可以使用下列命令列介面 (CLI) 版本的 hello 其中完成 hello 工作：</span><span class="sxs-lookup"><span data-stu-id="597bf-110">You can complete hello task by using one of hello following command-line interface (CLI) versions:</span></span>

- <span data-ttu-id="597bf-111">[Azure CLI 1.0](#quick-commands) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）</span><span class="sxs-lookup"><span data-stu-id="597bf-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="597bf-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)-hello 資源管理部署模型我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="597bf-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)- our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="597bf-113">快速命令</span><span class="sxs-lookup"><span data-stu-id="597bf-113">Quick commands</span></span>
<span data-ttu-id="597bf-114">tooaccomplish hello 工作快速，請遵循本節中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="597bf-114">tooaccomplish hello task quickly, follow hello steps in this section.</span></span> <span data-ttu-id="597bf-115">如需詳細資訊和內容，開始 hello [< 詳細逐步解說 >](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) > 一節。</span><span class="sxs-lookup"><span data-stu-id="597bf-115">For more detailed information and context, begin at hello ["Detailed walkthrough"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) section.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="597bf-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="597bf-116">Prerequisites</span></span>
* <span data-ttu-id="597bf-117">資源群組</span><span class="sxs-lookup"><span data-stu-id="597bf-117">A resource group</span></span>
* <span data-ttu-id="597bf-118">Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="597bf-118">An Azure virtual network</span></span>
* <span data-ttu-id="597bf-119">具有 SSH 輸入的網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="597bf-119">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="597bf-120">子網路</span><span class="sxs-lookup"><span data-stu-id="597bf-120">A subnet</span></span>
* <span data-ttu-id="597bf-121">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="597bf-121">An Azure storage account</span></span>
* <span data-ttu-id="597bf-122">Azure 儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="597bf-122">Azure storage account keys</span></span>
* <span data-ttu-id="597bf-123">Azure 檔案儲存體共用</span><span class="sxs-lookup"><span data-stu-id="597bf-123">An Azure File storage share</span></span>
* <span data-ttu-id="597bf-124">Linux VM</span><span class="sxs-lookup"><span data-stu-id="597bf-124">A Linux VM</span></span>

<span data-ttu-id="597bf-125">將任何範例換成您自己的設定。</span><span class="sxs-lookup"><span data-stu-id="597bf-125">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-hello-local-mount"></a><span data-ttu-id="597bf-126">建立 hello 本機掛接的目錄</span><span class="sxs-lookup"><span data-stu-id="597bf-126">Create a directory for hello local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a><span data-ttu-id="597bf-127">掛接 hello 檔案儲存體 SMB 共用 toohello 掛接點</span><span class="sxs-lookup"><span data-stu-id="597bf-127">Mount hello File storage SMB share toohello mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a><span data-ttu-id="597bf-128">在重新開機後持續 hello 掛接</span><span class="sxs-lookup"><span data-stu-id="597bf-128">Persist hello mount after a reboot</span></span>
<span data-ttu-id="597bf-129">新增以下太 hello`/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="597bf-129">Add hello following line too`/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="597bf-130">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="597bf-130">Detailed walkthrough</span></span>

<span data-ttu-id="597bf-131">檔案存放裝置提供 hello 雲端中的檔案共用使用 hello 標準 SMB 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="597bf-131">File storage offers file shares in hello cloud that use hello standard SMB protocol.</span></span> <span data-ttu-id="597bf-132">Hello 最新版本的檔案儲存體中，您也可以從任何作業系統，支援 SMB 3.0 裝載檔案共用。</span><span class="sxs-lookup"><span data-stu-id="597bf-132">With hello latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="597bf-133">當您使用 SMB 裝載在 Linux 上時，您取得簡單備份 tooa 穩固、 永久封存儲存體位置的 SLA 支援。</span><span class="sxs-lookup"><span data-stu-id="597bf-133">When you use an SMB mount on Linux, you get easy backups tooa robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="597bf-134">檔案存放裝置上，從裝載 VM tooan SMB 掛接移動檔案是很好的方法 toodebug 記錄。</span><span class="sxs-lookup"><span data-stu-id="597bf-134">Moving files from a VM tooan SMB mount that's hosted on File storage is a great way toodebug logs.</span></span> <span data-ttu-id="597bf-135">這是因為可以在本機裝載相同的 SMB 共用的 hello tooyour Mac、 Linux 或 Windows 的工作站。</span><span class="sxs-lookup"><span data-stu-id="597bf-135">That's because hello same SMB share can be mounted locally tooyour Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="597bf-136">SMB 不 hello Linux 資料流處理的最佳解決方案，或因為 hello SMB 通訊協定不是應用程式記錄檔即時建置 toohandle 這類大量記錄的責任。</span><span class="sxs-lookup"><span data-stu-id="597bf-136">SMB isn't hello best solution for streaming Linux or application logs in real time, because hello SMB protocol is not built toohandle such heavy logging duties.</span></span> <span data-ttu-id="597bf-137">專用的整合記錄層級工具，像是 Fluentd，是比透過 SMB 收集 Linux 和應用程式記錄輸出更好的選擇。</span><span class="sxs-lookup"><span data-stu-id="597bf-137">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="597bf-138">此詳細逐步解說中，我們會建立 hello 必要條件需要 toofirst 建立 hello 檔案存放裝置共用，然後再將它裝載透過 SMB，Linux VM 上。</span><span class="sxs-lookup"><span data-stu-id="597bf-138">For this detailed walkthrough, we create hello prerequisites needed toofirst create hello File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="597bf-139">使用下列程式碼的 hello 建立 Azure 儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="597bf-139">Create an Azure storage account by using hello following code:</span></span>

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. <span data-ttu-id="597bf-140">顯示 hello 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="597bf-140">Show hello storage account keys.</span></span>

    <span data-ttu-id="597bf-141">當您建立儲存體帳戶時，會建立 hello 帳戶金鑰組中，讓它們可以旋轉沒有任何服務中斷。</span><span class="sxs-lookup"><span data-stu-id="597bf-141">When you create a storage account, hello account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="597bf-142">當您切換 toohello 第二個金鑰 hello 配對中時，您會建立新的金鑰組。</span><span class="sxs-lookup"><span data-stu-id="597bf-142">When you switch toohello second key in hello pair, you create a new key pair.</span></span> <span data-ttu-id="597bf-143">新的儲存體帳戶金鑰一律會在配對，確保永遠有至少一個未使用的儲存體金鑰準備 tooswitch 來建立。</span><span class="sxs-lookup"><span data-stu-id="597bf-143">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage key ready tooswitch to.</span></span> <span data-ttu-id="597bf-144">tooshow hello 儲存體帳戶金鑰，請使用下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="597bf-144">tooshow hello storage account keys, use hello following code:</span></span>

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. <span data-ttu-id="597bf-145">建立 hello 檔案存放裝置共用。</span><span class="sxs-lookup"><span data-stu-id="597bf-145">Create hello File storage share.</span></span>

    <span data-ttu-id="597bf-146">hello 檔案存放裝置共用包含 hello SMB 共用。</span><span class="sxs-lookup"><span data-stu-id="597bf-146">hello File storage share contains hello SMB share.</span></span> <span data-ttu-id="597bf-147">hello 配額一律會以表示 (gb)。</span><span class="sxs-lookup"><span data-stu-id="597bf-147">hello quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="597bf-148">toocreate hello 的儲存體檔案共用，請使用下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="597bf-148">toocreate hello File storage share, use hello following code:</span></span>

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. <span data-ttu-id="597bf-149">建立 hello 掛接點目錄。</span><span class="sxs-lookup"><span data-stu-id="597bf-149">Create hello mount-point directory.</span></span>

    <span data-ttu-id="597bf-150">您必須在 hello Linux 檔案系統 toomount hello SMB 共用中建立本機目錄。</span><span class="sxs-lookup"><span data-stu-id="597bf-150">You must create a local directory in hello Linux file system toomount hello SMB share to.</span></span> <span data-ttu-id="597bf-151">任何寫入或讀取 hello 本機掛接目錄轉送的 toohello SMB 共用上裝載的檔案存放裝置。</span><span class="sxs-lookup"><span data-stu-id="597bf-151">Anything written or read from hello local mount directory is forwarded toohello SMB share that's hosted on File storage.</span></span> <span data-ttu-id="597bf-152">下列程式碼使用 hello toocreate hello 目錄：</span><span class="sxs-lookup"><span data-stu-id="597bf-152">toocreate hello directory, use hello following code:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. <span data-ttu-id="597bf-153">掛接的 hello SMB 共用上使用下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="597bf-153">Mount hello SMB share by using hello following code:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. <span data-ttu-id="597bf-154">保存的 hello SMB 裝載重新開機。</span><span class="sxs-lookup"><span data-stu-id="597bf-154">Persist hello SMB mount through reboots.</span></span>

    <span data-ttu-id="597bf-155">當您重新啟動 hello Linux VM 時，hello 掛接的 SMB 共用正在卸載所造成關機期間。</span><span class="sxs-lookup"><span data-stu-id="597bf-155">When you reboot hello Linux VM, hello mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="597bf-156">tooremount hello SMB 共用上開機，您必須新增列 toohello Linux /etc/fstab。</span><span class="sxs-lookup"><span data-stu-id="597bf-156">tooremount hello SMB share on boot, you must add a line toohello Linux /etc/fstab.</span></span> <span data-ttu-id="597bf-157">Linux 使用 hello fstab 檔案 toolist hello 檔案系統，它需要 toomount hello 開機程序期間。</span><span class="sxs-lookup"><span data-stu-id="597bf-157">Linux uses hello fstab file toolist hello file systems that it needs toomount during hello boot process.</span></span> <span data-ttu-id="597bf-158">新增 hello SMB 共用可確保該 hello 檔案存放裝置共用是 hello Linux VM 的永久掛接的檔案系統。</span><span class="sxs-lookup"><span data-stu-id="597bf-158">Adding hello SMB share ensures that hello File storage share is a permanently mounted file system for hello Linux VM.</span></span> <span data-ttu-id="597bf-159">加入 hello 檔案存放裝置的 SMB 共用 tooa 新的 VM 時，可能您使用雲端 init。</span><span class="sxs-lookup"><span data-stu-id="597bf-159">Adding hello File storage SMB share tooa new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="597bf-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="597bf-160">Next steps</span></span>

- [<span data-ttu-id="597bf-161">在建立期間使用雲端 init toocustomize Linux VM</span><span class="sxs-lookup"><span data-stu-id="597bf-161">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="597bf-162">新增磁碟 tooa Linux VM</span><span class="sxs-lookup"><span data-stu-id="597bf-162">Add a disk tooa Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="597bf-163">使用 Azure CLI hello 加密 Linux VM 上的磁碟</span><span class="sxs-lookup"><span data-stu-id="597bf-163">Encrypt disks on a Linux VM by using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
