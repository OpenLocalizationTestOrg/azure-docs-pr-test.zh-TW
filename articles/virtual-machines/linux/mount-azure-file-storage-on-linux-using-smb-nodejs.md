---
title: "透過 Azure CLI 1.0 使用 SMB 在 Linux VM 上掛接 Azure 檔案儲存體 | Microsoft Docs"
description: "如何使用 SMB 在 Linux VM 上掛接 Azure 檔案儲存體"
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
ms.openlocfilehash: 4951860630f0aad107d0846d52ebe4423ee0b91c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a><span data-ttu-id="eb029-103">透過 Azure CLI 1.0 使用 SMB 在 Linux VM 上掛接 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="eb029-103">Mount Azure File storage on Linux VMs by using SMB with Azure CLI 1.0</span></span>

<span data-ttu-id="eb029-104">本文說明如何使用伺服器訊息區 (SMB) 通訊協定在 Linux VM 上掛接 Azure 檔案儲存體。</span><span class="sxs-lookup"><span data-stu-id="eb029-104">This article shows how to mount Azure File storage on a Linux VM by using the Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="eb029-105">檔案儲存體可透過標準的 SMB 通訊協定在雲端中提供檔案共用。</span><span class="sxs-lookup"><span data-stu-id="eb029-105">File storage offers file shares in the cloud via the standard SMB protocol.</span></span> <span data-ttu-id="eb029-106">這些需求包括：</span><span class="sxs-lookup"><span data-stu-id="eb029-106">The requirements are:</span></span>

* <span data-ttu-id="eb029-107">[Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="eb029-107">An [Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* [<span data-ttu-id="eb029-108">安全殼層 (SSH) 公開金鑰和私密金鑰檔案</span><span class="sxs-lookup"><span data-stu-id="eb029-108">Secure Shell (SSH) public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="cli-versions-to-use"></a><span data-ttu-id="eb029-109">要使用的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="eb029-109">CLI versions to use</span></span>
<span data-ttu-id="eb029-110">您可以使用下列其中一個命令列介面 (CLI) 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="eb029-110">You can complete the task by using one of the following command-line interface (CLI) versions:</span></span>

- <span data-ttu-id="eb029-111">[Azure CLI 1.0](#quick-commands) – 適用於傳統和資源管理部署模型的 CLI (本文章)</span><span class="sxs-lookup"><span data-stu-id="eb029-111">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="eb029-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - 適用於資源管理部署模型的新一代 CLI</span><span class="sxs-lookup"><span data-stu-id="eb029-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)- our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="eb029-113">快速命令</span><span class="sxs-lookup"><span data-stu-id="eb029-113">Quick commands</span></span>
<span data-ttu-id="eb029-114">若要快速完成工作，請遵循本節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="eb029-114">To accomplish the task quickly, follow the steps in this section.</span></span> <span data-ttu-id="eb029-115">如需詳細資訊和內容，請從＜[詳細的逐步解說](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough)＞一節來開始。</span><span class="sxs-lookup"><span data-stu-id="eb029-115">For more detailed information and context, begin at the ["Detailed walkthrough"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) section.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="eb029-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="eb029-116">Prerequisites</span></span>
* <span data-ttu-id="eb029-117">資源群組</span><span class="sxs-lookup"><span data-stu-id="eb029-117">A resource group</span></span>
* <span data-ttu-id="eb029-118">Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="eb029-118">An Azure virtual network</span></span>
* <span data-ttu-id="eb029-119">具有 SSH 輸入的網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="eb029-119">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="eb029-120">子網路</span><span class="sxs-lookup"><span data-stu-id="eb029-120">A subnet</span></span>
* <span data-ttu-id="eb029-121">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="eb029-121">An Azure storage account</span></span>
* <span data-ttu-id="eb029-122">Azure 儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="eb029-122">Azure storage account keys</span></span>
* <span data-ttu-id="eb029-123">Azure 檔案儲存體共用</span><span class="sxs-lookup"><span data-stu-id="eb029-123">An Azure File storage share</span></span>
* <span data-ttu-id="eb029-124">Linux VM</span><span class="sxs-lookup"><span data-stu-id="eb029-124">A Linux VM</span></span>

<span data-ttu-id="eb029-125">將任何範例換成您自己的設定。</span><span class="sxs-lookup"><span data-stu-id="eb029-125">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-the-local-mount"></a><span data-ttu-id="eb029-126">建立本機掛接的目錄</span><span class="sxs-lookup"><span data-stu-id="eb029-126">Create a directory for the local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-the-file-storage-smb-share-to-the-mount-point"></a><span data-ttu-id="eb029-127">掛接檔案儲存體 SMB 共用至掛接點</span><span class="sxs-lookup"><span data-stu-id="eb029-127">Mount the File storage SMB share to the mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-the-mount-after-a-reboot"></a><span data-ttu-id="eb029-128">在重新開機之後保留掛接</span><span class="sxs-lookup"><span data-stu-id="eb029-128">Persist the mount after a reboot</span></span>
<span data-ttu-id="eb029-129">將下面這行新增至 `/etc/fstab`：</span><span class="sxs-lookup"><span data-stu-id="eb029-129">Add the following line to `/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="eb029-130">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="eb029-130">Detailed walkthrough</span></span>

<span data-ttu-id="eb029-131">檔案儲存體可在使用標準 SMB 通訊協定的雲端中提供檔案共用。</span><span class="sxs-lookup"><span data-stu-id="eb029-131">File storage offers file shares in the cloud that use the standard SMB protocol.</span></span> <span data-ttu-id="eb029-132">有了最新版本的檔案儲存體，您也可以從支援 SMB 3.0 的任何作業系統掛接檔案共用。</span><span class="sxs-lookup"><span data-stu-id="eb029-132">With the latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="eb029-133">在 Linux 上使用 SMB 掛接時，您可以輕鬆地將備份放到有 SLA 支援的強大、永久封存儲存體位置。</span><span class="sxs-lookup"><span data-stu-id="eb029-133">When you use an SMB mount on Linux, you get easy backups to a robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="eb029-134">將檔案從 VM 移至裝載在檔案儲存體上的 SMB 掛接，可方便您對記錄進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="eb029-134">Moving files from a VM to an SMB mount that's hosted on File storage is a great way to debug logs.</span></span> <span data-ttu-id="eb029-135">這是因為相同的 SMB 共用也可掛接至 Mac、Linux 或 Windows 工作站的本機上。</span><span class="sxs-lookup"><span data-stu-id="eb029-135">That's because the same SMB share can be mounted locally to your Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="eb029-136">SMB 並非即時串流 Linux 或應用程式記錄的最佳解決方案，因為 SMB 通訊協定的建置目的不是要處理如此繁重的記錄職責。</span><span class="sxs-lookup"><span data-stu-id="eb029-136">SMB isn't the best solution for streaming Linux or application logs in real time, because the SMB protocol is not built to handle such heavy logging duties.</span></span> <span data-ttu-id="eb029-137">專用的整合記錄層級工具，像是 Fluentd，是比透過 SMB 收集 Linux 和應用程式記錄輸出更好的選擇。</span><span class="sxs-lookup"><span data-stu-id="eb029-137">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="eb029-138">對於此詳細逐步解說，我們會建立必要的先決條件，先建立檔案儲存體共用，然後透過 SMB 在 Linux VM 上掛接它。</span><span class="sxs-lookup"><span data-stu-id="eb029-138">For this detailed walkthrough, we create the prerequisites needed to first create the File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="eb029-139">使用下列程式碼來建立 Azure 儲存體帳戶︰</span><span class="sxs-lookup"><span data-stu-id="eb029-139">Create an Azure storage account by using the following code:</span></span>

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. <span data-ttu-id="eb029-140">顯示儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="eb029-140">Show the storage account keys.</span></span>

    <span data-ttu-id="eb029-141">在建立儲存體帳戶時，帳戶金鑰會成對建立，因此您可以輪替金鑰，而不會干擾到服務。</span><span class="sxs-lookup"><span data-stu-id="eb029-141">When you create a storage account, the account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="eb029-142">當您將金鑰切換為金鑰組中的第二個金鑰時，您會建立新的金鑰組。</span><span class="sxs-lookup"><span data-stu-id="eb029-142">When you switch to the second key in the pair, you create a new key pair.</span></span> <span data-ttu-id="eb029-143">新的儲存體帳戶金鑰一律會成對建立，確保您永遠有至少一個準備切換到的未使用儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="eb029-143">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage key ready to switch to.</span></span> <span data-ttu-id="eb029-144">若要顯示儲存體帳戶金鑰，請使用下列程式碼︰</span><span class="sxs-lookup"><span data-stu-id="eb029-144">To show the storage account keys, use the following code:</span></span>

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. <span data-ttu-id="eb029-145">建立檔案儲存體共用。</span><span class="sxs-lookup"><span data-stu-id="eb029-145">Create the File storage share.</span></span>

    <span data-ttu-id="eb029-146">檔案儲存體共用包含 SMB 共用。</span><span class="sxs-lookup"><span data-stu-id="eb029-146">The File storage share contains the SMB share.</span></span> <span data-ttu-id="eb029-147">配額永遠是以 GB 表示。</span><span class="sxs-lookup"><span data-stu-id="eb029-147">The quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="eb029-148">若要建立檔案儲存體共用，請使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="eb029-148">To create the File storage share, use the following code:</span></span>

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. <span data-ttu-id="eb029-149">建立掛接點目錄。</span><span class="sxs-lookup"><span data-stu-id="eb029-149">Create the mount-point directory.</span></span>

    <span data-ttu-id="eb029-150">您必須在 Linux 檔案系統上建立本機目錄，以供 SMB 共用來掛接。</span><span class="sxs-lookup"><span data-stu-id="eb029-150">You must create a local directory in the Linux file system to mount the SMB share to.</span></span> <span data-ttu-id="eb029-151">任何從本機掛接目錄寫入或讀取的項目會轉送給裝載於檔案儲存體上的 SMB 共用。</span><span class="sxs-lookup"><span data-stu-id="eb029-151">Anything written or read from the local mount directory is forwarded to the SMB share that's hosted on File storage.</span></span> <span data-ttu-id="eb029-152">若要建立目錄，請使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="eb029-152">To create the directory, use the following code:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. <span data-ttu-id="eb029-153">使用下列程式碼來掛接 SMB 共用︰</span><span class="sxs-lookup"><span data-stu-id="eb029-153">Mount the SMB share by using the following code:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. <span data-ttu-id="eb029-154">透過重新開機持續 SMB 掛接。</span><span class="sxs-lookup"><span data-stu-id="eb029-154">Persist the SMB mount through reboots.</span></span>

    <span data-ttu-id="eb029-155">當您重新開機 Linux VM 時，掛接的 SMB 共用會在關機期間取消掛接。</span><span class="sxs-lookup"><span data-stu-id="eb029-155">When you reboot the Linux VM, the mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="eb029-156">若要在開機時重新掛接 SMB 共用，您必須新增一行至 Linux /etc/fstab。</span><span class="sxs-lookup"><span data-stu-id="eb029-156">To remount the SMB share on boot, you must add a line to the Linux /etc/fstab.</span></span> <span data-ttu-id="eb029-157">Linux 會使用 fstab 檔案來列出它在開機程序期間所必須掛接的檔案系統。</span><span class="sxs-lookup"><span data-stu-id="eb029-157">Linux uses the fstab file to list the file systems that it needs to mount during the boot process.</span></span> <span data-ttu-id="eb029-158">新增 SMB 共用可確保檔案儲存體共用是 Linux VM 的永久掛接檔案系統。</span><span class="sxs-lookup"><span data-stu-id="eb029-158">Adding the SMB share ensures that the File storage share is a permanently mounted file system for the Linux VM.</span></span> <span data-ttu-id="eb029-159">當您使用 cloud-init 時，便可以將檔案儲存體 SMB 共用新增至新的 VM。</span><span class="sxs-lookup"><span data-stu-id="eb029-159">Adding the File storage SMB share to a new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="eb029-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eb029-160">Next steps</span></span>

- [<span data-ttu-id="eb029-161">在建立期間使用 cloud-init 自訂 Linux VM</span><span class="sxs-lookup"><span data-stu-id="eb029-161">Using cloud-init to customize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="eb029-162">在 Linux VM 中新增磁碟</span><span class="sxs-lookup"><span data-stu-id="eb029-162">Add a disk to a Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="eb029-163">使用 Azure CLI 將 Linux VM 上的磁碟加密</span><span class="sxs-lookup"><span data-stu-id="eb029-163">Encrypt disks on a Linux VM by using the Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
