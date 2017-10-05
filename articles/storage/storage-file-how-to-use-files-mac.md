---
title: "透過 macOS 的 SMB 掛接 Azure 檔案共用 | Microsoft Docs"
description: "了解如何透過 macOS 的 SMB 掛接 Azure 檔案共用。"
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 428086910273d10a68cb8193df377a4db267d6a3
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a><span data-ttu-id="5b3c5-103">透過 macOS 的 SMB 掛接 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="5b3c5-103">Mount Azure File share over SMB with macOS</span></span>
<span data-ttu-id="5b3c5-104">[Azure 檔案儲存體](storage-dotnet-how-to-use-files.md)是 Microsoft 的服務，可讓您在 Azure 中使用業界標準建立和使用網路檔案共用。</span><span class="sxs-lookup"><span data-stu-id="5b3c5-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's service that enables you to create and use network file shares in the Azure using the industry standard.</span></span> <span data-ttu-id="5b3c5-105">Azure 檔案共用可在 macOS Sierra (10.12) 和 El Capitan (10.11) 中掛接。</span><span class="sxs-lookup"><span data-stu-id="5b3c5-105">Azure File shares can be mounted in macOS Sierra (10.12) and El Capitan (10.11).</span></span> <span data-ttu-id="5b3c5-106">本文將說明兩種不同的方式，在 macOS 上使用搜尋工具 UI 和使用終端機來掛接 Azure 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="5b3c5-106">This article shows two different ways to mount an Azure File share on macOS with the Finder UI and using the Terminal.</span></span>

> [!Note]  
> <span data-ttu-id="5b3c5-107">在透過 SMB 掛接 Azure 檔案共用之前，建議您停用 SMB 封包簽章。</span><span class="sxs-lookup"><span data-stu-id="5b3c5-107">Before mounting an Azure File share over SMB, we recommend disabling SMB packet signing.</span></span> <span data-ttu-id="5b3c5-108">不這樣做可能會導致從 macOS 存取 Azure 檔案共用時效能不佳。</span><span class="sxs-lookup"><span data-stu-id="5b3c5-108">Not doing so may yield poor performance when accessing the Azure File share from macOS.</span></span> <span data-ttu-id="5b3c5-109">SMB 連線將會加密，因此這不會影響您連線的安全性。</span><span class="sxs-lookup"><span data-stu-id="5b3c5-109">Your SMB connection will be encrypted, so this does not affect the security of your connection.</span></span> <span data-ttu-id="5b3c5-110">從終端機中，下列命令會停用 SMB 封包簽章，如同[停用 SMB 封包簽章的 Apple 支援文章](https://support.apple.com/HT205926)所描述：</span><span class="sxs-lookup"><span data-stu-id="5b3c5-110">From the terminal, the following commands will disable SMB packet signing, as described by this [Apple support article on disabling SMB packet signing](https://support.apple.com/HT205926):</span></span>  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a><span data-ttu-id="5b3c5-111">在 macOS 上掛接 Azure 檔案共用的必要條件</span><span class="sxs-lookup"><span data-stu-id="5b3c5-111">Prerequisites for mounting an Azure File share on macOS</span></span>
* <span data-ttu-id="5b3c5-112">**儲存體帳戶名稱**：若要掛接 Azure 檔案共用，您需要儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="5b3c5-112">**Storage account name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="5b3c5-113">**儲存體帳戶金鑰**：若要掛接 Azure 檔案共用，您需要主要 (或次要) 金鑰。</span><span class="sxs-lookup"><span data-stu-id="5b3c5-113">**Storage account key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="5b3c5-114">掛接目前不支援 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="5b3c5-114">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="5b3c5-115">**請確定已開啟連接埠 445**SMB 透過 TCP 通訊埠 445 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="5b3c5-115">**Ensure port 445 is open**: SMB communicates over TCP port 445.</span></span> <span data-ttu-id="5b3c5-116">在用戶端電腦 (Mac) 中，請檢查並確定您的防火牆不會封鎖 TCP 通訊埠 445。</span><span class="sxs-lookup"><span data-stu-id="5b3c5-116">On your client machine (the Mac), check to make sure your firewall is not blocking TCP port 445.</span></span>

## <a name="mount-an-azure-file-share-via-finder"></a><span data-ttu-id="5b3c5-117">透過搜尋工具掛接 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="5b3c5-117">Mount an Azure File share via Finder</span></span>
1. <span data-ttu-id="5b3c5-118">**開啟搜尋工具**：搜尋工具在 macOS 中為預設開啟，但是您可以按一下 Dock 上的 [macOS 臉部圖示] 確保它是目前選取的應用程式：</span><span class="sxs-lookup"><span data-stu-id="5b3c5-118">**Open Finder**: Finder is open on macOS by default, but you can ensure it is the currently selected application by clicking the "macOS face icon" on the dock:</span></span>  
    <span data-ttu-id="5b3c5-119">![macOS 臉部圖示](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span><span class="sxs-lookup"><span data-stu-id="5b3c5-119">![The macOS face icon](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span></span>

2. <span data-ttu-id="5b3c5-120">**從 [前往] 功能表選取 [連線至伺服器]**：使用[必要條件](#preq)的 UNC 路徑，將開頭的雙反斜線 (`\\`) 轉換至 `smb://`，並將所有其他的反斜線 (`\`) 轉換至正斜線 (`/`)。</span><span class="sxs-lookup"><span data-stu-id="5b3c5-120">**Select "Connect to Server" from the "Go" Menu**: Using the UNC path from the [prerequisites](#preq), convert the beginning double backslash (`\\`) to `smb://` and all other backslashes (`\`) to forwards slashes (`/`).</span></span> <span data-ttu-id="5b3c5-121">您的連結應看起來如下所示：![[連線至伺服器] 對話方塊](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span><span class="sxs-lookup"><span data-stu-id="5b3c5-121">Your link should look like the following: ![The "Connect to Server" dialog](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span></span>

3. <span data-ttu-id="5b3c5-122">**提示您輸入使用者名稱和密碼時，使用共用名稱和儲存體帳戶金鑰**：當您在 [連線至伺服器] 對話方塊中按一下 [連線] 時，系統會提示您的使用者名稱和密碼 (這會使用您的 macOS 使用者名稱自動填入)。</span><span class="sxs-lookup"><span data-stu-id="5b3c5-122">**Use the share name and storage account key when prompted for a username and password**: When you click "Connect" on the "Connect to Server" dialog, you will be prompted for the username and password (This will be autopopulated with your macOS username).</span></span> <span data-ttu-id="5b3c5-123">您可以選擇將共用名稱/儲存體帳戶金鑰置於您的 macOS 金鑰鏈。</span><span class="sxs-lookup"><span data-stu-id="5b3c5-123">You have the option of placing the share name/storage account key in your macOS Keychain.</span></span>

4. <span data-ttu-id="5b3c5-124">**視需要使用 Azure 檔案共用**：在使用共用名稱和儲存體帳戶金鑰替換使用者名稱和密碼之後，系統將掛接共用。</span><span class="sxs-lookup"><span data-stu-id="5b3c5-124">**Use the Azure File share as desired**: After substituting the share name and storage account key in for the username and password, the share will be mounted.</span></span> <span data-ttu-id="5b3c5-125">您可以依照平常使用本機資料夾/檔案共用的方式使用，包括將檔案拖放到檔案共用中：</span><span class="sxs-lookup"><span data-stu-id="5b3c5-125">You may use this as you would normally use a local folder/file share, including dragging and dropping files into the file share:</span></span>

    ![已掛接之 Azure 檔案共用的快照集](./media/storage-file-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a><span data-ttu-id="5b3c5-127">透過終端機掛接 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="5b3c5-127">Mount an Azure File share via Terminal</span></span>
1. <span data-ttu-id="5b3c5-128">使用您的儲存體帳戶名稱取代 `<storage-account-name>`。</span><span class="sxs-lookup"><span data-stu-id="5b3c5-128">Replace `<storage-account-name>` with the name of your storage account.</span></span> <span data-ttu-id="5b3c5-129">當系統提示時，請提供儲存體帳戶金鑰作為密碼。</span><span class="sxs-lookup"><span data-stu-id="5b3c5-129">Provide Storage Account Key as password when prompted.</span></span> 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. <span data-ttu-id="5b3c5-130">**視需要使用 Azure 檔案共用**Azure 檔案共用將會掛接先前命令所指定的掛接點。</span><span class="sxs-lookup"><span data-stu-id="5b3c5-130">**Use the Azure File share as desired**: The Azure File share will be mounted at the mount point specified by the previous command.</span></span>  

    ![已掛接之 Azure 檔案共用的快照集](./media/storage-file-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a><span data-ttu-id="5b3c5-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5b3c5-132">Next steps</span></span>
<span data-ttu-id="5b3c5-133">請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5b3c5-133">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="5b3c5-134">Apple 支援文章 - 如何在 Mac 上連線檔案共用</span><span class="sxs-lookup"><span data-stu-id="5b3c5-134">Apple Support Article - How to connect with File Sharing on your Mac</span></span>](https://support.apple.com/HT204445)
* [<span data-ttu-id="5b3c5-135">常見問題集</span><span class="sxs-lookup"><span data-stu-id="5b3c5-135">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="5b3c5-136">疑難排解</span><span class="sxs-lookup"><span data-stu-id="5b3c5-136">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)