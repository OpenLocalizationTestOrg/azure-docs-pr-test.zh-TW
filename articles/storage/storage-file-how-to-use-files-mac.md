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
# <a name="mount-azure-file-share-over-smb-with-macos"></a>透過 macOS 的 SMB 掛接 Azure 檔案共用
[Azure 檔案儲存體](storage-dotnet-how-to-use-files.md)Microsoft 的服務，可讓您在 hello Azure toocreate 和使用網路檔案共用使用 hello 業界標準。 Azure 檔案共用可在 macOS Sierra (10.12) 和 El Capitan (10.11) 中掛接。 本文示範兩個不同的方式 toomount Azure 檔案共用上 macOS hello 搜尋工具 UI 和使用 hello 終端機。

> [!Note]  
> 在透過 SMB 掛接 Azure 檔案共用之前，建議您停用 SMB 封包簽章。 不這樣可能會產生效能不佳，從 macOS 存取 hello Azure 檔案共用時。 SMB 連接將會加密，因此這不會影響 hello 連線的安全性。 從終端機 hello hello 下列命令將會停用 SMB 封包簽章，如下所描述[Apple 技術支援文件上停用 SMB 封包簽章](https://support.apple.com/HT205926):  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a>在 macOS 上掛接 Azure 檔案共用的必要條件
* **儲存體帳戶名稱**: toomount Azure 檔案共用，您將需要 hello hello 儲存體帳戶名稱。

* **儲存體帳戶金鑰**: toomount Azure 檔案共用，您將需要 hello 主要 （或次要） 的儲存體金鑰。 掛接目前不支援 SAS 金鑰。

* **請確定已開啟連接埠 445**SMB 透過 TCP 通訊埠 445 進行通訊。 在用戶端電腦 (hello Mac)，檢查 toomake 確定防火牆不會封鎖 TCP 通訊埠 445。

## <a name="mount-an-azure-file-share-via-finder"></a>透過搜尋工具掛接 Azure 檔案共用
1. **Finder 開啟**： 搜尋已在 macOS 預設會開啟，但是您可以確保它是 hello 上目前選取的應用程式即可 hello"macOS 面臨的圖示"hello 停駐：  
    ![hello macOS 面臨圖示](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)

2. **選取 「 連接 tooServer"hello"Go"功能表從**： 使用 hello UNC 路徑從 hello[必要條件](#preq)，轉換 hello 開頭雙反斜線 (`\\`) 太`smb://`和所有其他反斜線 (`\`)tooforwards 斜線 (`/`)。 您的連結起來會像下列 hello: ![hello 「 連接 tooServer 」 對話方塊](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)

3. **使用 hello 共用名稱和儲存體帳戶金鑰時提示您輸入使用者名稱和密碼**： 當您在 hello 「 連接 tooServer 」 對話方塊中按一下 [連線] 時，系統會提示您 hello 使用者名稱和密碼 （這會是與您 macOS autopopulated使用者名稱）。 您可以將 hello 共用名稱/儲存體帳戶金鑰放入您 macOS Keychain hello 選擇。

4. **使用 hello Azure 檔案共用做為所需**： 在替換後 hello 共用名稱和儲存體帳戶金鑰 hello 使用者名稱和密碼，將掛接 hello 共用。 因為您通常會使用本機資料夾/檔案共用，包括拖放到 hello 檔案共用的檔案，您可以使用這個：

    ![已掛接之 Azure 檔案共用的快照集](./media/storage-file-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a>透過終端機掛接 Azure 檔案共用
1. 取代`<storage-account-name>`hello 的儲存體帳戶的名稱。 當系統提示時，請提供儲存體帳戶金鑰作為密碼。 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. **使用 hello Azure 檔案共用做為所需**: hello Azure 檔案共用將會掛接在 hello hello 前一個命令所指定的掛接點。  

    ![Hello 掛接 Azure 檔案共用的快照集](./media/storage-file-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a>後續步驟
請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。

* [Apple 技術支援文件-如何 tooconnect 以在 Mac 上的檔案共用](https://support.apple.com/HT204445)
* [常見問題集](storage-files-faq.md)
* [疑難排解](storage-troubleshoot-file-connection-problems.md)