---
title: "aaaMount Azure 檔案共用，透過 SMB 的 macOS |Microsoft 文件"
description: "了解如何 toomount Azure 檔案共用透過 SMB macOS。"
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
ms.openlocfilehash: 7b4924cb42247470521c1ae8b9d03ab1756996e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a><span data-ttu-id="e064a-103">透過 macOS 的 SMB 掛接 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="e064a-103">Mount Azure File share over SMB with macOS</span></span>
<span data-ttu-id="e064a-104">[Azure 檔案儲存體](storage-dotnet-how-to-use-files.md)Microsoft 的服務，可讓您在 hello Azure toocreate 和使用網路檔案共用使用 hello 業界標準。</span><span class="sxs-lookup"><span data-stu-id="e064a-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's service that enables you toocreate and use network file shares in hello Azure using hello industry standard.</span></span> <span data-ttu-id="e064a-105">Azure 檔案共用可在 macOS Sierra (10.12) 和 El Capitan (10.11) 中掛接。</span><span class="sxs-lookup"><span data-stu-id="e064a-105">Azure File shares can be mounted in macOS Sierra (10.12) and El Capitan (10.11).</span></span> <span data-ttu-id="e064a-106">本文示範兩個不同的方式 toomount Azure 檔案共用上 macOS hello 搜尋工具 UI 和使用 hello 終端機。</span><span class="sxs-lookup"><span data-stu-id="e064a-106">This article shows two different ways toomount an Azure File share on macOS with hello Finder UI and using hello Terminal.</span></span>

> [!Note]  
> <span data-ttu-id="e064a-107">在透過 SMB 掛接 Azure 檔案共用之前，建議您停用 SMB 封包簽章。</span><span class="sxs-lookup"><span data-stu-id="e064a-107">Before mounting an Azure File share over SMB, we recommend disabling SMB packet signing.</span></span> <span data-ttu-id="e064a-108">不這樣可能會產生效能不佳，從 macOS 存取 hello Azure 檔案共用時。</span><span class="sxs-lookup"><span data-stu-id="e064a-108">Not doing so may yield poor performance when accessing hello Azure File share from macOS.</span></span> <span data-ttu-id="e064a-109">SMB 連接將會加密，因此這不會影響 hello 連線的安全性。</span><span class="sxs-lookup"><span data-stu-id="e064a-109">Your SMB connection will be encrypted, so this does not affect hello security of your connection.</span></span> <span data-ttu-id="e064a-110">從終端機 hello hello 下列命令將會停用 SMB 封包簽章，如下所描述[Apple 技術支援文件上停用 SMB 封包簽章](https://support.apple.com/HT205926):</span><span class="sxs-lookup"><span data-stu-id="e064a-110">From hello terminal, hello following commands will disable SMB packet signing, as described by this [Apple support article on disabling SMB packet signing](https://support.apple.com/HT205926):</span></span>  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a><span data-ttu-id="e064a-111">在 macOS 上掛接 Azure 檔案共用的必要條件</span><span class="sxs-lookup"><span data-stu-id="e064a-111">Prerequisites for mounting an Azure File share on macOS</span></span>
* <span data-ttu-id="e064a-112">**儲存體帳戶名稱**: toomount Azure 檔案共用，您將需要 hello hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="e064a-112">**Storage account name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="e064a-113">**儲存體帳戶金鑰**: toomount Azure 檔案共用，您將需要 hello 主要 （或次要） 的儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="e064a-113">**Storage account key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="e064a-114">掛接目前不支援 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="e064a-114">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="e064a-115">**請確定已開啟連接埠 445**SMB 透過 TCP 通訊埠 445 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="e064a-115">**Ensure port 445 is open**: SMB communicates over TCP port 445.</span></span> <span data-ttu-id="e064a-116">在用戶端電腦 (hello Mac)，檢查 toomake 確定防火牆不會封鎖 TCP 通訊埠 445。</span><span class="sxs-lookup"><span data-stu-id="e064a-116">On your client machine (hello Mac), check toomake sure your firewall is not blocking TCP port 445.</span></span>

## <a name="mount-an-azure-file-share-via-finder"></a><span data-ttu-id="e064a-117">透過搜尋工具掛接 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="e064a-117">Mount an Azure File share via Finder</span></span>
1. <span data-ttu-id="e064a-118">**Finder 開啟**： 搜尋已在 macOS 預設會開啟，但是您可以確保它是 hello 上目前選取的應用程式即可 hello"macOS 面臨的圖示"hello 停駐：</span><span class="sxs-lookup"><span data-stu-id="e064a-118">**Open Finder**: Finder is open on macOS by default, but you can ensure it is hello currently selected application by clicking hello "macOS face icon" on hello dock:</span></span>  
    <span data-ttu-id="e064a-119">![hello macOS 面臨圖示](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span><span class="sxs-lookup"><span data-stu-id="e064a-119">![hello macOS face icon](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span></span>

2. <span data-ttu-id="e064a-120">**選取 「 連接 tooServer"hello"Go"功能表從**： 使用 hello UNC 路徑從 hello[必要條件](#preq)，轉換 hello 開頭雙反斜線 (`\\`) 太`smb://`和所有其他反斜線 (`\`)tooforwards 斜線 (`/`)。</span><span class="sxs-lookup"><span data-stu-id="e064a-120">**Select "Connect tooServer" from hello "Go" Menu**: Using hello UNC path from hello [prerequisites](#preq), convert hello beginning double backslash (`\\`) too`smb://` and all other backslashes (`\`) tooforwards slashes (`/`).</span></span> <span data-ttu-id="e064a-121">您的連結起來會像下列 hello: ![hello 「 連接 tooServer 」 對話方塊](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span><span class="sxs-lookup"><span data-stu-id="e064a-121">Your link should look like hello following: ![hello "Connect tooServer" dialog](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span></span>

3. <span data-ttu-id="e064a-122">**使用 hello 共用名稱和儲存體帳戶金鑰時提示您輸入使用者名稱和密碼**： 當您在 hello 「 連接 tooServer 」 對話方塊中按一下 [連線] 時，系統會提示您 hello 使用者名稱和密碼 （這會是與您 macOS autopopulated使用者名稱）。</span><span class="sxs-lookup"><span data-stu-id="e064a-122">**Use hello share name and storage account key when prompted for a username and password**: When you click "Connect" on hello "Connect tooServer" dialog, you will be prompted for hello username and password (This will be autopopulated with your macOS username).</span></span> <span data-ttu-id="e064a-123">您可以將 hello 共用名稱/儲存體帳戶金鑰放入您 macOS Keychain hello 選擇。</span><span class="sxs-lookup"><span data-stu-id="e064a-123">You have hello option of placing hello share name/storage account key in your macOS Keychain.</span></span>

4. <span data-ttu-id="e064a-124">**使用 hello Azure 檔案共用做為所需**： 在替換後 hello 共用名稱和儲存體帳戶金鑰 hello 使用者名稱和密碼，將掛接 hello 共用。</span><span class="sxs-lookup"><span data-stu-id="e064a-124">**Use hello Azure File share as desired**: After substituting hello share name and storage account key in for hello username and password, hello share will be mounted.</span></span> <span data-ttu-id="e064a-125">因為您通常會使用本機資料夾/檔案共用，包括拖放到 hello 檔案共用的檔案，您可以使用這個：</span><span class="sxs-lookup"><span data-stu-id="e064a-125">You may use this as you would normally use a local folder/file share, including dragging and dropping files into hello file share:</span></span>

    ![已掛接之 Azure 檔案共用的快照集](./media/storage-file-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a><span data-ttu-id="e064a-127">透過終端機掛接 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="e064a-127">Mount an Azure File share via Terminal</span></span>
1. <span data-ttu-id="e064a-128">取代`<storage-account-name>`hello 的儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="e064a-128">Replace `<storage-account-name>` with hello name of your storage account.</span></span> <span data-ttu-id="e064a-129">當系統提示時，請提供儲存體帳戶金鑰作為密碼。</span><span class="sxs-lookup"><span data-stu-id="e064a-129">Provide Storage Account Key as password when prompted.</span></span> 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. <span data-ttu-id="e064a-130">**使用 hello Azure 檔案共用做為所需**: hello Azure 檔案共用將會掛接在 hello hello 前一個命令所指定的掛接點。</span><span class="sxs-lookup"><span data-stu-id="e064a-130">**Use hello Azure File share as desired**: hello Azure File share will be mounted at hello mount point specified by hello previous command.</span></span>  

    ![Hello 掛接 Azure 檔案共用的快照集](./media/storage-file-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a><span data-ttu-id="e064a-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e064a-132">Next steps</span></span>
<span data-ttu-id="e064a-133">請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e064a-133">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="e064a-134">Apple 技術支援文件-如何 tooconnect 以在 Mac 上的檔案共用</span><span class="sxs-lookup"><span data-stu-id="e064a-134">Apple Support Article - How tooconnect with File Sharing on your Mac</span></span>](https://support.apple.com/HT204445)
* [<span data-ttu-id="e064a-135">常見問題集</span><span class="sxs-lookup"><span data-stu-id="e064a-135">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="e064a-136">疑難排解</span><span class="sxs-lookup"><span data-stu-id="e064a-136">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)