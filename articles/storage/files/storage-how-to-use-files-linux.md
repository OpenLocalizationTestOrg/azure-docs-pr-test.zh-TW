---
title: "aaaUse Linux 的 Azure 檔案儲存體 |Microsoft 文件"
description: "了解 toomount Azure 檔案如何透過在 Linux 上的 SMB 共用。"
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
ms.openlocfilehash: eeaa24b7f9e646724c5d86ae1e80dfdadaff34fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-storage-with-linux"></a><span data-ttu-id="22a5f-103">搭配 Linux 使用 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="22a5f-103">Use Azure File storage with Linux</span></span>
<span data-ttu-id="22a5f-104">[Azure 檔案儲存體](../storage-dotnet-how-to-use-files.md)是 Microsoft 的簡單 toouse 雲端的檔案系統。</span><span class="sxs-lookup"><span data-stu-id="22a5f-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's easy toouse cloud file system.</span></span> <span data-ttu-id="22a5f-105">Azure 檔案共用使用 hello 之 Linux 發行套件中只能裝載[cifs utils 封裝](https://wiki.samba.org/index.php/LinuxCIFS_utils)從 hello [Samba 專案](https://www.samba.org/)。</span><span class="sxs-lookup"><span data-stu-id="22a5f-105">Azure File shares can be mounted in Linux distributions using hello [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) from hello [Samba project](https://www.samba.org/).</span></span> <span data-ttu-id="22a5f-106">本文將說明兩種方式 toomount Azure 檔案共用： 依需求以 hello`mount`命令，並在開機藉由建立中的項目`/etc/fstab`。</span><span class="sxs-lookup"><span data-stu-id="22a5f-106">This article shows two ways toomount an Azure File share: on-demand with hello `mount` command and on-boot by creating an entry in `/etc/fstab`.</span></span>

> [!NOTE]  
> <span data-ttu-id="22a5f-107">順序 toomount Azure 檔案共用之外 hello Azure 地區，例如在內部部署或在不同 Azure 區域中，hello OS 裝載於，必須支援 SMB 3.0 的 hello 加密的功能。</span><span class="sxs-lookup"><span data-stu-id="22a5f-107">In order toomount an Azure File share outside of hello Azure region it is hosted in, such as on-premises or in a different Azure region, hello OS must support hello encryption functionality of SMB 3.0.</span></span> <span data-ttu-id="22a5f-108">4.11 核心推出 Linux 的 SMB 3.0 適用的加密功能。</span><span class="sxs-lookup"><span data-stu-id="22a5f-108">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="22a5f-109">此功能讓您可從內部部署或不同 Azure 區域的 Azure 檔案共用進行掛接。</span><span class="sxs-lookup"><span data-stu-id="22a5f-109">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="22a5f-110">在發行的 hello 階段，這項功能已被 backported tooUbuntu 從 16.04 及更新版本。</span><span class="sxs-lookup"><span data-stu-id="22a5f-110">At hello time of publishing, this functionality has been backported tooUbuntu from 16.04 and above.</span></span>


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-hello-cifs-utils-package"></a><span data-ttu-id="22a5f-111">裝載 Azure 檔案共用與 Linux 和 hello cifs 公用程式封裝的必要條件</span><span class="sxs-lookup"><span data-stu-id="22a5f-111">Prerequisities for mounting an Azure File share with Linux and hello cifs-utils package</span></span>
* <span data-ttu-id="22a5f-112">**挑選 Linux 散發套件可以已安裝的 hello cifs utils 封裝**: Microsoft 建議下列 Linux 散發套件 hello Azure 映像庫中的 hello:</span><span class="sxs-lookup"><span data-stu-id="22a5f-112">**Pick a Linux distribution that can have hello cifs-utils package installed**: Microsoft recommends hello following Linux distributions in hello Azure image gallery:</span></span>

    * <span data-ttu-id="22a5f-113">Ubuntu Server 14.04+</span><span class="sxs-lookup"><span data-stu-id="22a5f-113">Ubuntu Server 14.04+</span></span>
    * <span data-ttu-id="22a5f-114">RHEL 7+</span><span class="sxs-lookup"><span data-stu-id="22a5f-114">RHEL 7+</span></span>
    * <span data-ttu-id="22a5f-115">CentOS 7+</span><span class="sxs-lookup"><span data-stu-id="22a5f-115">CentOS 7+</span></span>
    * <span data-ttu-id="22a5f-116">Debian 8</span><span class="sxs-lookup"><span data-stu-id="22a5f-116">Debian 8</span></span>
    * <span data-ttu-id="22a5f-117">openSUSE 13.2+</span><span class="sxs-lookup"><span data-stu-id="22a5f-117">openSUSE 13.2+</span></span>
    * <span data-ttu-id="22a5f-118">SUSE Linux Enterprise Server 12</span><span class="sxs-lookup"><span data-stu-id="22a5f-118">SUSE Linux Enterprise Server 12</span></span>

* <span data-ttu-id="22a5f-119"><a id="install-cifs-utils"></a>**hello cifs 公用程式安裝封裝**: hello cifs 公用程式可以在您選擇的 hello Linux 發佈使用 hello 封裝管理員來安裝。</span><span class="sxs-lookup"><span data-stu-id="22a5f-119"><a id="install-cifs-utils"></a>**hello cifs-utils package is installed**: hello cifs-utils can be installed using hello package manager on hello Linux distribution of your choice.</span></span> 

    <span data-ttu-id="22a5f-120">在**Ubuntu**和**Debian 基礎**分佈，使用 hello`apt-get`封裝管理員：</span><span class="sxs-lookup"><span data-stu-id="22a5f-120">On **Ubuntu** and **Debian-based** distributions, use hello `apt-get` package manager:</span></span>

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    <span data-ttu-id="22a5f-121">在**RHEL**和**CentOS**，使用 hello`yum`封裝管理員：</span><span class="sxs-lookup"><span data-stu-id="22a5f-121">On **RHEL** and **CentOS**, use hello `yum` package manager:</span></span>

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    <span data-ttu-id="22a5f-122">在**openSUSE**，使用 hello`zypper`封裝管理員：</span><span class="sxs-lookup"><span data-stu-id="22a5f-122">On **openSUSE**, use hello `zypper` package manager:</span></span>

    ```
    sudo zypper install samba*
    ```

    <span data-ttu-id="22a5f-123">其他的發佈，使用 hello 適當的封裝管理員或[從來源編譯](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download)。</span><span class="sxs-lookup"><span data-stu-id="22a5f-123">On other distributions, use hello appropriate package manager or [compile from source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span></span>

* <span data-ttu-id="22a5f-124">**Hello hello 掛接共用目錄/檔案權限決定**: hello 下列範例中，我們使用 0777，toogive 讀取、 寫入及執行 tooall 使用者權限。</span><span class="sxs-lookup"><span data-stu-id="22a5f-124">**Decide on hello directory/file permissions of hello mounted share**: In hello examples below, we use 0777, toogive read, write, and execute permissions tooall users.</span></span> <span data-ttu-id="22a5f-125">您可以視需要將它取代為其他 [chmod 權限](https://en.wikipedia.org/wiki/Chmod)。</span><span class="sxs-lookup"><span data-stu-id="22a5f-125">You can replace it with other [chmod permissions](https://en.wikipedia.org/wiki/Chmod) as desired.</span></span> 

* <span data-ttu-id="22a5f-126">**儲存體帳戶名稱**: toomount Azure 檔案共用，您將需要 hello hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="22a5f-126">**Storage Account Name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="22a5f-127">**儲存體帳戶金鑰**: toomount Azure 檔案共用，您將需要 hello 主要 （或次要） 的儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="22a5f-127">**Storage Account Key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="22a5f-128">掛接目前不支援 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="22a5f-128">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="22a5f-129">**請確定已開啟連接埠 445**: SMB 通訊透過 TCP 通訊埠 445-檢查 toosee，如果您的防火牆不會封鎖 TCP 連接埠 445，從用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="22a5f-129">**Ensure port 445 is open**: SMB communicates over TCP port 445 - check toosee if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-hello-azure-file-share-on-demand-with-mount"></a><span data-ttu-id="22a5f-130">裝載 Azure 檔案共用上指定與 hello`mount`</span><span class="sxs-lookup"><span data-stu-id="22a5f-130">Mount hello Azure File share on-demand with `mount`</span></span>
1. <span data-ttu-id="22a5f-131">**[安裝 Linux 發佈的 hello cifs utils 套件](#install-cifs-utils)**。</span><span class="sxs-lookup"><span data-stu-id="22a5f-131">**[Install hello cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="22a5f-132">**建立 hello 掛接點資料夾**： 這可以完成 hello 檔案系統中的任何位置。</span><span class="sxs-lookup"><span data-stu-id="22a5f-132">**Create a folder for hello mount point**: This can be done anywhere on hello file system.</span></span>

    ```
    mkdir mymountpoint
    ```

3. <span data-ttu-id="22a5f-133">**使用 hello 掛接命令 toomount hello Azure 檔案共用**： 記住 tooreplace `<storage-account-name>`， `<share-name>`，和`<storage-account-key>`hello 適當資訊。</span><span class="sxs-lookup"><span data-stu-id="22a5f-133">**Use hello mount command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with hello proper information.</span></span>

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> <span data-ttu-id="22a5f-134">當您完成使用 hello Azure 檔案共用，您可以使用`sudo umount ./mymountpoint`toounmount hello 共用。</span><span class="sxs-lookup"><span data-stu-id="22a5f-134">When you are done using hello Azure File share, you may use `sudo umount ./mymountpoint` toounmount hello share.</span></span>

## <a name="create-a-persistent-mount-point-for-hello-azure-file-share-with-etcfstab"></a><span data-ttu-id="22a5f-135">建立 hello Azure 檔案共用對象的持續掛接點`/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="22a5f-135">Create a persistent mount point for hello Azure File share with `/etc/fstab`</span></span>
1. <span data-ttu-id="22a5f-136">**[安裝 Linux 發佈的 hello cifs utils 套件](#install-cifs-utils)**。</span><span class="sxs-lookup"><span data-stu-id="22a5f-136">**[Install hello cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="22a5f-137">**建立 hello 掛接點資料夾**： 這可以完成 hello 檔案系統中的任何位置，但您需要的 hello 資料夾 toonote hello 絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="22a5f-137">**Create a folder for hello mount point**: This can be done anywhere on hello file system, but you need toonote hello absolute path of hello folder.</span></span> <span data-ttu-id="22a5f-138">hello 下列範例會建立在根目錄下的資料夾。</span><span class="sxs-lookup"><span data-stu-id="22a5f-138">hello following example creates a folder under root.</span></span>

    ```
    sudo mkdir /mymountpoint
    ```

3. <span data-ttu-id="22a5f-139">**使用 hello 下列命令行下太 tooappend hello`/etc/fstab`**： 記住 tooreplace `<storage-account-name>`， `<share-name>`，和`<storage-account-key>`hello 適當資訊。</span><span class="sxs-lookup"><span data-stu-id="22a5f-139">**Use hello following command tooappend hello following line too`/etc/fstab`**: Remember tooreplace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with hello proper information.</span></span>

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> <span data-ttu-id="22a5f-140">您可以使用`sudo mount -a`toomount hello Azure 檔案共用，在編輯之後`/etc/fstab`而不需要重新開機。</span><span class="sxs-lookup"><span data-stu-id="22a5f-140">You can use `sudo mount -a` toomount hello Azure File share after editing `/etc/fstab` instead of rebooting.</span></span>

## <a name="feedback"></a><span data-ttu-id="22a5f-141">意見反應</span><span class="sxs-lookup"><span data-stu-id="22a5f-141">Feedback</span></span>
<span data-ttu-id="22a5f-142">Linux 使用者，我們想要從您的 toohear ！</span><span class="sxs-lookup"><span data-stu-id="22a5f-142">Linux users, we want toohear from you!</span></span>

<span data-ttu-id="22a5f-143">hello Linux users' 群組的 Azure 檔案儲存體論壇為您提供 tooshare 意見反應您評估及採用在 Linux 上的檔案存放裝置。</span><span class="sxs-lookup"><span data-stu-id="22a5f-143">hello Azure File storage for Linux users' group provides a forum for you tooshare feedback as you evaluate and adopt File storage on Linux.</span></span> <span data-ttu-id="22a5f-144">電子郵件[Azure 檔案儲存體 Linux 使用者](mailto:azurefileslinuxusers@microsoft.com)toojoin hello users' 群組。</span><span class="sxs-lookup"><span data-stu-id="22a5f-144">Email [Azure File storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) toojoin hello users' group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22a5f-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="22a5f-145">Next steps</span></span>
<span data-ttu-id="22a5f-146">請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="22a5f-146">See these links for more information about Azure File storage.</span></span>
* [<span data-ttu-id="22a5f-147">檔案服務 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="22a5f-147">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [<span data-ttu-id="22a5f-148">如何使用 Microsoft Azure 儲存體 toouse AzCopy</span><span class="sxs-lookup"><span data-stu-id="22a5f-148">How toouse AzCopy with Microsoft Azure storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="22a5f-149">使用 Azure CLI hello 與 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="22a5f-149">Using hello Azure CLI with Azure storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [<span data-ttu-id="22a5f-150">常見問題集</span><span class="sxs-lookup"><span data-stu-id="22a5f-150">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="22a5f-151">疑難排解</span><span class="sxs-lookup"><span data-stu-id="22a5f-151">Troubleshooting</span></span>](storage-troubleshoot-linux-file-connection-problems.md)
