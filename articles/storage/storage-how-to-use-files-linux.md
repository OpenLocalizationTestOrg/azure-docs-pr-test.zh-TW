---
title: "搭配 Linux 使用 Azure 檔案儲存體 | Microsoft Docs"
description: "了解如何透過 Linux 上的 SMB 掛接 Azure 檔案共用。"
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6edc37ce-698f-4d50-8fc1-591ad456175d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/8/2017
ms.author: renash
ms.openlocfilehash: 27b393a899c60a3a0393619f338a396dff659498
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="use-azure-file-storage-with-linux"></a><span data-ttu-id="525f8-103">搭配 Linux 使用 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="525f8-103">Use Azure File storage with Linux</span></span>
<span data-ttu-id="525f8-104">[Azure 檔案儲存體](storage-dotnet-how-to-use-files.md)是 Microsoft 容易使用的雲端檔案系統。</span><span class="sxs-lookup"><span data-stu-id="525f8-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy to use cloud file system.</span></span> <span data-ttu-id="525f8-105">Azure 檔案共用可裝載於使用 [cifs-utils 封裝](https://wiki.samba.org/index.php/LinuxCIFS_utils) (來自 [Samba 專案](https://www.samba.org/)) 的 Linux 發行版本。</span><span class="sxs-lookup"><span data-stu-id="525f8-105">Azure File shares can be mounted in Linux distributions using the [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) from the [Samba project](https://www.samba.org/).</span></span> <span data-ttu-id="525f8-106">本文將說明掛接 Azure 檔案共用的兩種方式：使用 `mount` 命令的隨選掛接，以及建立項目 `/etc/fstab` 的開機掛接。</span><span class="sxs-lookup"><span data-stu-id="525f8-106">This article shows two ways to mount an Azure File share: on-demand with the `mount` command and on-boot by creating an entry in `/etc/fstab`.</span></span>

> [!NOTE]  
> <span data-ttu-id="525f8-107">若要在 Azure 區域之外掛接 Azure 檔案共用，例如內部部署或是在不同的 Azure 區域，作業系統必須支援 SMB 3.0 的加密功能。</span><span class="sxs-lookup"><span data-stu-id="525f8-107">In order to mount an Azure File share outside of the Azure region it is hosted in, such as on-premises or in a different Azure region, the OS must support the encryption functionality of SMB 3.0.</span></span> <span data-ttu-id="525f8-108">4.11 核心推出 Linux 的 SMB 3.0 適用的加密功能。</span><span class="sxs-lookup"><span data-stu-id="525f8-108">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="525f8-109">此功能讓您可從內部部署或不同 Azure 區域的 Azure 檔案共用進行掛接。</span><span class="sxs-lookup"><span data-stu-id="525f8-109">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="525f8-110">發佈時，這項功能已向前移植到 16.04 及以上版本的 Ubuntu。</span><span class="sxs-lookup"><span data-stu-id="525f8-110">At the time of publishing, this functionality has been backported to Ubuntu from 16.04 and above.</span></span>


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-the-cifs-utils-package"></a><span data-ttu-id="525f8-111">以 Linux 掛接 Azure 檔案共用和 cifs-utils 封裝的必要條件</span><span class="sxs-lookup"><span data-stu-id="525f8-111">Prerequisities for mounting an Azure File share with Linux and the cifs-utils package</span></span>
* <span data-ttu-id="525f8-112">**挑選可安裝 cifs-utils 封裝的 Linux 發行版本**：Microsoft 建議使用 Azure 映像庫中的下列 Linux 發行版本：</span><span class="sxs-lookup"><span data-stu-id="525f8-112">**Pick a Linux distribution that can have the cifs-utils package installed**: Microsoft recommends the following Linux distributions in the Azure image gallery:</span></span>

    * <span data-ttu-id="525f8-113">Ubuntu Server 14.04+</span><span class="sxs-lookup"><span data-stu-id="525f8-113">Ubuntu Server 14.04+</span></span>
    * <span data-ttu-id="525f8-114">RHEL 7+</span><span class="sxs-lookup"><span data-stu-id="525f8-114">RHEL 7+</span></span>
    * <span data-ttu-id="525f8-115">CentOS 7+</span><span class="sxs-lookup"><span data-stu-id="525f8-115">CentOS 7+</span></span>
    * <span data-ttu-id="525f8-116">Debian 8</span><span class="sxs-lookup"><span data-stu-id="525f8-116">Debian 8</span></span>
    * <span data-ttu-id="525f8-117">openSUSE 13.2+</span><span class="sxs-lookup"><span data-stu-id="525f8-117">openSUSE 13.2+</span></span>
    * <span data-ttu-id="525f8-118">SUSE Linux Enterprise Server 12</span><span class="sxs-lookup"><span data-stu-id="525f8-118">SUSE Linux Enterprise Server 12</span></span>

* <span data-ttu-id="525f8-119"><a id="install-cifs-utils"></a>**安裝 cifs-utils 封裝**：可使用封裝管理員將 cifs-utils 安裝在所選擇的 Linux 發行版本上。</span><span class="sxs-lookup"><span data-stu-id="525f8-119"><a id="install-cifs-utils"></a>**The cifs-utils package is installed**: The cifs-utils can be installed using the package manager on the Linux distribution of your choice.</span></span> 

    <span data-ttu-id="525f8-120">在 **Ubuntu** 和 **Debian 型**發行版本上，請使用 `apt-get` 封裝管理員：</span><span class="sxs-lookup"><span data-stu-id="525f8-120">On **Ubuntu** and **Debian-based** distributions, use the `apt-get` package manager:</span></span>

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    <span data-ttu-id="525f8-121">在 **RHEL** 和 **CentOS** 上，請使用 `yum` 封裝管理員：</span><span class="sxs-lookup"><span data-stu-id="525f8-121">On **RHEL** and **CentOS**, use the `yum` package manager:</span></span>

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    <span data-ttu-id="525f8-122">在 **openSUSE** 上，請使用 `zypper` 封裝管理員：</span><span class="sxs-lookup"><span data-stu-id="525f8-122">On **openSUSE**, use the `zypper` package manager:</span></span>

    ```
    sudo zypper install samba*
    ```

    <span data-ttu-id="525f8-123">在其他發行版本上，請使用適當的封裝管理員或[從來源編譯](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download)。</span><span class="sxs-lookup"><span data-stu-id="525f8-123">On other distributions, use the appropriate package manager or [compile from source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span></span>

* <span data-ttu-id="525f8-124">**對於掛接的共用決定目錄/檔案權限**：下列範例使用 0777 提供所有使用者的讀取、寫入和執行權限。</span><span class="sxs-lookup"><span data-stu-id="525f8-124">**Decide on the directory/file permissions of the mounted share**: In the examples below, we use 0777, to give read, write, and execute permissions to all users.</span></span> <span data-ttu-id="525f8-125">您可以視需要將它取代為其他 [chmod 權限](https://en.wikipedia.org/wiki/Chmod)。</span><span class="sxs-lookup"><span data-stu-id="525f8-125">You can replace it with other [chmod permissions](https://en.wikipedia.org/wiki/Chmod) as desired.</span></span> 

* <span data-ttu-id="525f8-126">**儲存體帳戶名稱**：若要掛接 Azure 檔案共用，您需要儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="525f8-126">**Storage Account Name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="525f8-127">**儲存體帳戶金鑰**：若要掛接 Azure 檔案共用，您需要主要 (或次要) 金鑰。</span><span class="sxs-lookup"><span data-stu-id="525f8-127">**Storage Account Key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="525f8-128">掛接目前不支援 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="525f8-128">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="525f8-129">**請確定已開啟連接埠 445**：SMB 透過 TCP 通訊埠 445 進行通訊 - 請檢查您的防火牆不會將 TCP 通訊埠 445 從用戶端電腦封鎖。</span><span class="sxs-lookup"><span data-stu-id="525f8-129">**Ensure port 445 is open**: SMB communicates over TCP port 445 - check to see if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-the-azure-file-share-on-demand-with-mount"></a><span data-ttu-id="525f8-130">使用 `mount` 隨需掛接 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="525f8-130">Mount the Azure File share on-demand with `mount`</span></span>
1. <span data-ttu-id="525f8-131">**[在您的 Linux 發行版本上安裝 cifs-utils 封裝](#install-cifs-utils)**。</span><span class="sxs-lookup"><span data-stu-id="525f8-131">**[Install the cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="525f8-132">**建立掛接點的資料夾**：在檔案系統的任何位置均可完成此作業。</span><span class="sxs-lookup"><span data-stu-id="525f8-132">**Create a folder for the mount point**: This can be done anywhere on the file system.</span></span>

    ```
    mkdir mymountpoint
    ```

3. <span data-ttu-id="525f8-133">**使用 mount 命令掛接 Azure 檔案共用**：請記得要使用正確的資訊來取代 `<storage-account-name>`、`<share-name>` 和 `<storage-account-key>`。</span><span class="sxs-lookup"><span data-stu-id="525f8-133">**Use the mount command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with the proper information.</span></span>

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> <span data-ttu-id="525f8-134">使用 Azure 檔案共用後，即可使用 `sudo umount ./mymountpoint` 取消掛接共用。</span><span class="sxs-lookup"><span data-stu-id="525f8-134">When you are done using the Azure File share, you may use `sudo umount ./mymountpoint` to unmount the share.</span></span>

## <a name="create-a-persistent-mount-point-for-the-azure-file-share-with-etcfstab"></a><span data-ttu-id="525f8-135">使用 `/etc/fstab` 建立 Azure 檔案共用的持續掛接點</span><span class="sxs-lookup"><span data-stu-id="525f8-135">Create a persistent mount point for the Azure File share with `/etc/fstab`</span></span>
1. <span data-ttu-id="525f8-136">**[在您的 Linux 發行版本上安裝 cifs-utils 封裝](#install-cifs-utils)**。</span><span class="sxs-lookup"><span data-stu-id="525f8-136">**[Install the cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="525f8-137">**建立掛接點的資料夾**：這可以在檔案系統中的任何位置完成，但是您必須記下資料夾的絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="525f8-137">**Create a folder for the mount point**: This can be done anywhere on the file system, but you need to note the absolute path of the folder.</span></span> <span data-ttu-id="525f8-138">下列範例會建立在根目錄下的資料夾。</span><span class="sxs-lookup"><span data-stu-id="525f8-138">The following example creates a folder under root.</span></span>

    ```
    sudo mkdir /mymountpoint
    ```

3. <span data-ttu-id="525f8-139">**使用下列命令將下列一行附加至 `/etc/fstab`**：請記得要使用正確的資訊來取代 `<storage-account-name>`、`<share-name>` 和 `<storage-account-key>`。</span><span class="sxs-lookup"><span data-stu-id="525f8-139">**Use the following command to append the following line to `/etc/fstab`**: Remember to replace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with the proper information.</span></span>

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> <span data-ttu-id="525f8-140">您可以使用 `sudo mount -a` 在編輯之後掛接 Azure 檔案共用`/etc/fstab`而不需要重新開機。</span><span class="sxs-lookup"><span data-stu-id="525f8-140">You can use `sudo mount -a` to mount the Azure File share after editing `/etc/fstab` instead of rebooting.</span></span>

## <a name="feedback"></a><span data-ttu-id="525f8-141">意見反應</span><span class="sxs-lookup"><span data-stu-id="525f8-141">Feedback</span></span>
<span data-ttu-id="525f8-142">Linux 使用者，歡迎您提供相關資訊！</span><span class="sxs-lookup"><span data-stu-id="525f8-142">Linux users, we want to hear from you!</span></span>

<span data-ttu-id="525f8-143">Linux 使用者群組的 Azure 檔案儲存體提供論壇，讓您在 Linux 上評估並採用檔案儲存體的同時分享意見。</span><span class="sxs-lookup"><span data-stu-id="525f8-143">The Azure File storage for Linux users' group provides a forum for you to share feedback as you evaluate and adopt File storage on Linux.</span></span> <span data-ttu-id="525f8-144">請寄電子郵件至 [Azure 檔案儲存體 Linux 使用者](mailto:azurefileslinuxusers@microsoft.com) 以加入使用者的群組。</span><span class="sxs-lookup"><span data-stu-id="525f8-144">Email [Azure File storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) to join the users' group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="525f8-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="525f8-145">Next steps</span></span>
<span data-ttu-id="525f8-146">請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="525f8-146">See these links for more information about Azure File storage.</span></span>
* [<span data-ttu-id="525f8-147">檔案服務 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="525f8-147">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [<span data-ttu-id="525f8-148">搭配使用 Azure PowerShell 與 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="525f8-148">Using Azure PowerShell with Azure storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="525f8-149">如何搭配使用 AzCopy 與 Microsoft Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="525f8-149">How to use AzCopy with Microsoft Azure storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="525f8-150">使用 Azure CLI 搭配 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="525f8-150">Using the Azure CLI with Azure storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="525f8-151">常見問題集</span><span class="sxs-lookup"><span data-stu-id="525f8-151">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="525f8-152">疑難排解</span><span class="sxs-lookup"><span data-stu-id="525f8-152">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)
