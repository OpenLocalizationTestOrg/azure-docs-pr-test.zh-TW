---
title: "使用 SMB 的 Linux Vm 上的 Azure 檔案儲存體 aaaMount |Microsoft 文件"
description: "使用 SMB 與 Linux Vm 上的 Azure 檔案儲存體 toomount hello Azure CLI 2.0 的方式"
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
ms.date: 02/13/2017
ms.author: v-livech
ms.openlocfilehash: 7b34c81e602748b78c924f44a54b876744c28f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a><span data-ttu-id="b6ead-103">使用 SMB 在 Linux VM 上掛接 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="b6ead-103">Mount Azure File storage on Linux VMs using SMB</span></span>

<span data-ttu-id="b6ead-104">本文章將示範如何 tooutilize hello Azure 檔案儲存體服務，使用 SMB 在 Linux VM 上裝載以 hello Azure CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="b6ead-104">This article shows you how tooutilize hello Azure File storage service on a Linux VM using an SMB mount with hello Azure CLI 2.0.</span></span> <span data-ttu-id="b6ead-105">Azure 檔案儲存體提供使用標準 SMB 通訊協定 hello hello 雲端中的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="b6ead-105">Azure File storage offers file shares in hello cloud using hello standard SMB protocol.</span></span> <span data-ttu-id="b6ead-106">您也可以執行下列步驟以 hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b6ead-106">You can also perform these steps with hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b6ead-107">hello 需求如下：</span><span class="sxs-lookup"><span data-stu-id="b6ead-107">hello requirements are:</span></span>

- [<span data-ttu-id="b6ead-108">一個 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="b6ead-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="b6ead-109">SSH 公開金鑰和私密金鑰檔案</span><span class="sxs-lookup"><span data-stu-id="b6ead-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="quick-commands"></a><span data-ttu-id="b6ead-110">快速命令</span><span class="sxs-lookup"><span data-stu-id="b6ead-110">Quick Commands</span></span>

* <span data-ttu-id="b6ead-111">資源群組</span><span class="sxs-lookup"><span data-stu-id="b6ead-111">A resource group</span></span>
* <span data-ttu-id="b6ead-112">Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="b6ead-112">An Azure virtual network</span></span>
* <span data-ttu-id="b6ead-113">具有 SSH 輸入的網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="b6ead-113">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="b6ead-114">子網路</span><span class="sxs-lookup"><span data-stu-id="b6ead-114">A subnet</span></span>
* <span data-ttu-id="b6ead-115">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="b6ead-115">An Azure storage account</span></span>
* <span data-ttu-id="b6ead-116">Azure 儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="b6ead-116">Azure storage account keys</span></span>
* <span data-ttu-id="b6ead-117">Azure 檔案儲存體共用</span><span class="sxs-lookup"><span data-stu-id="b6ead-117">An Azure File storage share</span></span>
* <span data-ttu-id="b6ead-118">Linux VM</span><span class="sxs-lookup"><span data-stu-id="b6ead-118">A Linux VM</span></span>

<span data-ttu-id="b6ead-119">將任何範例換成您自己的設定。</span><span class="sxs-lookup"><span data-stu-id="b6ead-119">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-hello-local-mount"></a><span data-ttu-id="b6ead-120">建立 hello 本機掛接的目錄</span><span class="sxs-lookup"><span data-stu-id="b6ead-120">Create a directory for hello local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a><span data-ttu-id="b6ead-121">掛接 hello 檔案儲存體 SMB 共用 toohello 掛接點</span><span class="sxs-lookup"><span data-stu-id="b6ead-121">Mount hello File storage SMB share toohello mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a><span data-ttu-id="b6ead-122">在重新開機後持續 hello 掛接</span><span class="sxs-lookup"><span data-stu-id="b6ead-122">Persist hello mount after a reboot</span></span>
<span data-ttu-id="b6ead-123">toodo，加入下列行 toohello hello `/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="b6ead-123">toodo so, add hello following line toohello `/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="b6ead-124">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="b6ead-124">Detailed walkthrough</span></span>

<span data-ttu-id="b6ead-125">檔案存放裝置提供 hello 雲端中的檔案共用使用 hello 標準 SMB 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="b6ead-125">File storage offers file shares in hello cloud that use hello standard SMB protocol.</span></span> <span data-ttu-id="b6ead-126">Hello 最新版本的檔案儲存體中，您也可以從任何作業系統，支援 SMB 3.0 裝載檔案共用。</span><span class="sxs-lookup"><span data-stu-id="b6ead-126">With hello latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="b6ead-127">當您使用 SMB 裝載在 Linux 上時，您取得簡單備份 tooa 穩固、 永久封存儲存體位置的 SLA 支援。</span><span class="sxs-lookup"><span data-stu-id="b6ead-127">When you use an SMB mount on Linux, you get easy backups tooa robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="b6ead-128">檔案存放裝置上，從裝載 VM tooan SMB 掛接移動檔案是很好的方法 toodebug 記錄。</span><span class="sxs-lookup"><span data-stu-id="b6ead-128">Moving files from a VM tooan SMB mount that's hosted on File storage is a great way toodebug logs.</span></span> <span data-ttu-id="b6ead-129">這是因為可以在本機裝載相同的 SMB 共用的 hello tooyour Mac、 Linux 或 Windows 的工作站。</span><span class="sxs-lookup"><span data-stu-id="b6ead-129">That's because hello same SMB share can be mounted locally tooyour Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="b6ead-130">SMB 不 hello Linux 資料流處理的最佳解決方案，或因為 hello SMB 通訊協定不是應用程式記錄檔即時建置 toohandle 這類大量記錄的責任。</span><span class="sxs-lookup"><span data-stu-id="b6ead-130">SMB isn't hello best solution for streaming Linux or application logs in real time, because hello SMB protocol is not built toohandle such heavy logging duties.</span></span> <span data-ttu-id="b6ead-131">專用的整合記錄層級工具，像是 Fluentd，是比透過 SMB 收集 Linux 和應用程式記錄輸出更好的選擇。</span><span class="sxs-lookup"><span data-stu-id="b6ead-131">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="b6ead-132">此詳細逐步解說中，我們會建立 hello 必要條件需要 toofirst 建立 hello 檔案存放裝置共用，然後再將它裝載透過 SMB，Linux VM 上。</span><span class="sxs-lookup"><span data-stu-id="b6ead-132">For this detailed walkthrough, we create hello prerequisites needed toofirst create hello File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="b6ead-133">建立資源群組與[az 群組建立](/cli/azure/group#create)toohold hello 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="b6ead-133">Create a resource group with [az group create](/cli/azure/group#create) toohold hello file share.</span></span>

    <span data-ttu-id="b6ead-134">資源群組命名為的 toocreate `myResourceGroup` hello 「 美國西部 」 位置，使用下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="b6ead-134">toocreate a resource group named `myResourceGroup` in hello "West US" location, use hello following example:</span></span>

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. <span data-ttu-id="b6ead-135">建立 Azure 儲存體帳戶與[az 儲存體帳戶建立](/cli/azure/storage/account#create)toostore hello 實際檔案。</span><span class="sxs-lookup"><span data-stu-id="b6ead-135">Create an Azure storage account with [az storage account create](/cli/azure/storage/account#create) toostore hello actual files.</span></span>

    <span data-ttu-id="b6ead-136">toocreate 儲存體帳戶命名 mystorageaccount 使用 hello Standard_LRS 儲存體 SKU，下列範例使用 hello:</span><span class="sxs-lookup"><span data-stu-id="b6ead-136">toocreate a storage account named mystorageaccount by using hello Standard_LRS storage SKU, use hello following example:</span></span>

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. <span data-ttu-id="b6ead-137">顯示 hello 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="b6ead-137">Show hello storage account keys.</span></span>

    <span data-ttu-id="b6ead-138">當您建立儲存體帳戶時，會建立 hello 帳戶金鑰組中，讓它們可以旋轉沒有任何服務中斷。</span><span class="sxs-lookup"><span data-stu-id="b6ead-138">When you create a storage account, hello account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="b6ead-139">當您切換 toohello 第二個金鑰 hello 配對中時，您會建立新的金鑰組。</span><span class="sxs-lookup"><span data-stu-id="b6ead-139">When you switch toohello second key in hello pair, you create a new key pair.</span></span> <span data-ttu-id="b6ead-140">新的儲存體帳戶金鑰一律會在配對，確保永遠有至少一個未使用的儲存體帳戶金鑰準備 tooswitch 來建立。</span><span class="sxs-lookup"><span data-stu-id="b6ead-140">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage account key ready tooswitch to.</span></span>

    <span data-ttu-id="b6ead-141">檢視 hello 儲存體帳戶金鑰，以 hello [az 儲存體帳戶金鑰清單](/cli/azure/storage/account/keys#list)。</span><span class="sxs-lookup"><span data-stu-id="b6ead-141">View hello storage account keys with hello [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="b6ead-142">hello hello 名為的儲存體帳戶金鑰`mystorageaccount`hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="b6ead-142">hello storage account keys for hello named `mystorageaccount` are listed in hello following example:</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    <span data-ttu-id="b6ead-143">tooextract 單一索引鍵，使用 hello`--query`旗標。</span><span class="sxs-lookup"><span data-stu-id="b6ead-143">tooextract a single key, use hello `--query` flag.</span></span> <span data-ttu-id="b6ead-144">hello 下列範例會擷取 hello 第一個索引鍵 (`[0]`):</span><span class="sxs-lookup"><span data-stu-id="b6ead-144">hello following example extracts hello first key (`[0]`):</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. <span data-ttu-id="b6ead-145">建立 hello 檔案存放裝置共用。</span><span class="sxs-lookup"><span data-stu-id="b6ead-145">Create hello File storage share.</span></span>

    <span data-ttu-id="b6ead-146">hello 檔案存放裝置共用包含的 hello 與 SMB 共用[az 存放裝置共用建立](/cli/azure/storage/share#create)。</span><span class="sxs-lookup"><span data-stu-id="b6ead-146">hello File storage share contains hello SMB share with [az storage share create](/cli/azure/storage/share#create).</span></span> <span data-ttu-id="b6ead-147">hello 配額一律會以表示 (gb)。</span><span class="sxs-lookup"><span data-stu-id="b6ead-147">hello quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="b6ead-148">從上述 hello 傳入 hello 金鑰的其中之一`az storage account keys list`命令。</span><span class="sxs-lookup"><span data-stu-id="b6ead-148">Pass in one of hello keys from hello preceding `az storage account keys list` command.</span></span> <span data-ttu-id="b6ead-149">建立共用，使用下列範例中的 hello 具名 mystorageshare 具有 10 GB 配額：</span><span class="sxs-lookup"><span data-stu-id="b6ead-149">Create a share named mystorageshare with a 10-GB quota by using hello following example:</span></span>

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. <span data-ttu-id="b6ead-150">建立掛接點目錄。</span><span class="sxs-lookup"><span data-stu-id="b6ead-150">Create a mount-point directory.</span></span>

    <span data-ttu-id="b6ead-151">在 hello Linux 檔案系統 toomount hello SMB 共用上建立本機目錄。</span><span class="sxs-lookup"><span data-stu-id="b6ead-151">Create a local directory in hello Linux file system toomount hello SMB share to.</span></span> <span data-ttu-id="b6ead-152">任何寫入或讀取 hello 本機掛接目錄轉送的 toohello SMB 共用上裝載的檔案存放裝置。</span><span class="sxs-lookup"><span data-stu-id="b6ead-152">Anything written or read from hello local mount directory is forwarded toohello SMB share that's hosted on File storage.</span></span> <span data-ttu-id="b6ead-153">toocreate /mnt/retention/ mymountdirectory，下列範例使用 hello 的本機目錄：</span><span class="sxs-lookup"><span data-stu-id="b6ead-153">toocreate a local directory at /mnt/mymountdirectory, use hello following example:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. <span data-ttu-id="b6ead-154">掛接 hello SMB 共用 toohello 本機目錄。</span><span class="sxs-lookup"><span data-stu-id="b6ead-154">Mount hello SMB share toohello local directory.</span></span>

    <span data-ttu-id="b6ead-155">請提供您自己的儲存體帳戶的使用者名稱和 hello 掛接認證的儲存體帳戶金鑰，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b6ead-155">Provide your own storage account username and storage account key for hello mount credentials as follows:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. <span data-ttu-id="b6ead-156">保存的 hello SMB 裝載重新開機。</span><span class="sxs-lookup"><span data-stu-id="b6ead-156">Persist hello SMB mount through reboots.</span></span>

    <span data-ttu-id="b6ead-157">當您重新啟動 hello Linux VM 時，hello 掛接的 SMB 共用正在卸載所造成關機期間。</span><span class="sxs-lookup"><span data-stu-id="b6ead-157">When you reboot hello Linux VM, hello mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="b6ead-158">SMB 共用的開機，tooremount hello 新增列 toohello Linux /etc/fstab。</span><span class="sxs-lookup"><span data-stu-id="b6ead-158">tooremount hello SMB share on boot, add a line toohello Linux /etc/fstab.</span></span> <span data-ttu-id="b6ead-159">Linux 使用 hello fstab 檔案 toolist hello 檔案系統，它需要 toomount hello 開機程序期間。</span><span class="sxs-lookup"><span data-stu-id="b6ead-159">Linux uses hello fstab file toolist hello file systems that it needs toomount during hello boot process.</span></span> <span data-ttu-id="b6ead-160">新增 hello SMB 共用可確保該 hello 檔案存放裝置共用是 hello Linux VM 的永久掛接的檔案系統。</span><span class="sxs-lookup"><span data-stu-id="b6ead-160">Adding hello SMB share ensures that hello File storage share is a permanently mounted file system for hello Linux VM.</span></span> <span data-ttu-id="b6ead-161">加入 hello 檔案存放裝置的 SMB 共用 tooa 新的 VM 時，可能您使用雲端 init。</span><span class="sxs-lookup"><span data-stu-id="b6ead-161">Adding hello File storage SMB share tooa new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="b6ead-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b6ead-162">Next steps</span></span>

- [<span data-ttu-id="b6ead-163">在建立期間使用雲端 init toocustomize Linux VM</span><span class="sxs-lookup"><span data-stu-id="b6ead-163">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="b6ead-164">新增磁碟 tooa Linux VM</span><span class="sxs-lookup"><span data-stu-id="b6ead-164">Add a disk tooa Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="b6ead-165">使用 Azure CLI hello 加密 Linux VM 上的磁碟</span><span class="sxs-lookup"><span data-stu-id="b6ead-165">Encrypt disks on a Linux VM by using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
