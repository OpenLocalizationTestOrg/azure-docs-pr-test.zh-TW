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
ms.openlocfilehash: ed6ba9b98f121d6629d858320ca3760384303ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-storage-with-linux"></a>搭配 Linux 使用 Azure 檔案儲存體
[Azure 檔案儲存體](storage-dotnet-how-to-use-files.md)是 Microsoft 的簡單 toouse 雲端的檔案系統。 Azure 檔案共用使用 hello 之 Linux 發行套件中只能裝載[cifs utils 封裝](https://wiki.samba.org/index.php/LinuxCIFS_utils)從 hello [Samba 專案](https://www.samba.org/)。 本文將說明兩種方式 toomount Azure 檔案共用： 依需求以 hello`mount`命令，並在開機藉由建立中的項目`/etc/fstab`。

> [!NOTE]  
> 順序 toomount Azure 檔案共用之外 hello Azure 地區，例如在內部部署或在不同 Azure 區域中，hello OS 裝載於，必須支援 SMB 3.0 的 hello 加密的功能。 4.11 核心推出 Linux 的 SMB 3.0 適用的加密功能。 此功能讓您可從內部部署或不同 Azure 區域的 Azure 檔案共用進行掛接。 在發行的 hello 階段，這項功能已被 backported tooUbuntu 從 16.04 及更新版本。


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-hello-cifs-utils-package"></a>裝載 Azure 檔案共用與 Linux 和 hello cifs 公用程式封裝的必要條件
* **挑選 Linux 散發套件可以已安裝的 hello cifs utils 封裝**: Microsoft 建議下列 Linux 散發套件 hello Azure 映像庫中的 hello:

    * Ubuntu Server 14.04+
    * RHEL 7+
    * CentOS 7+
    * Debian 8
    * openSUSE 13.2+
    * SUSE Linux Enterprise Server 12

* <a id="install-cifs-utils"></a>**hello cifs 公用程式安裝封裝**: hello cifs 公用程式可以在您選擇的 hello Linux 發佈使用 hello 封裝管理員來安裝。 

    在**Ubuntu**和**Debian 基礎**分佈，使用 hello`apt-get`封裝管理員：

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    在**RHEL**和**CentOS**，使用 hello`yum`封裝管理員：

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    在**openSUSE**，使用 hello`zypper`封裝管理員：

    ```
    sudo zypper install samba*
    ```

    其他的發佈，使用 hello 適當的封裝管理員或[從來源編譯](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download)。

* **Hello hello 掛接共用目錄/檔案權限決定**: hello 下列範例中，我們使用 0777，toogive 讀取、 寫入及執行 tooall 使用者權限。 您可以視需要將它取代為其他 [chmod 權限](https://en.wikipedia.org/wiki/Chmod)。 

* **儲存體帳戶名稱**: toomount Azure 檔案共用，您將需要 hello hello 儲存體帳戶名稱。

* **儲存體帳戶金鑰**: toomount Azure 檔案共用，您將需要 hello 主要 （或次要） 的儲存體金鑰。 掛接目前不支援 SAS 金鑰。

* **請確定已開啟連接埠 445**: SMB 通訊透過 TCP 通訊埠 445-檢查 toosee，如果您的防火牆不會封鎖 TCP 連接埠 445，從用戶端電腦。

## <a name="mount-hello-azure-file-share-on-demand-with-mount"></a>裝載 Azure 檔案共用上指定與 hello`mount`
1. **[安裝 Linux 發佈的 hello cifs utils 套件](#install-cifs-utils)**。

2. **建立 hello 掛接點資料夾**： 這可以完成 hello 檔案系統中的任何位置。

    ```
    mkdir mymountpoint
    ```

3. **使用 hello 掛接命令 toomount hello Azure 檔案共用**： 記住 tooreplace `<storage-account-name>`， `<share-name>`，和`<storage-account-key>`hello 適當資訊。

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> 當您完成使用 hello Azure 檔案共用，您可以使用`sudo umount ./mymountpoint`toounmount hello 共用。

## <a name="create-a-persistent-mount-point-for-hello-azure-file-share-with-etcfstab"></a>建立 hello Azure 檔案共用對象的持續掛接點`/etc/fstab`
1. **[安裝 Linux 發佈的 hello cifs utils 套件](#install-cifs-utils)**。

2. **建立 hello 掛接點資料夾**： 這可以完成 hello 檔案系統中的任何位置，但您需要的 hello 資料夾 toonote hello 絕對路徑。 hello 下列範例會建立在根目錄下的資料夾。

    ```
    sudo mkdir /mymountpoint
    ```

3. **使用 hello 下列命令行下太 tooappend hello`/etc/fstab`**： 記住 tooreplace `<storage-account-name>`， `<share-name>`，和`<storage-account-key>`hello 適當資訊。

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> 您可以使用`sudo mount -a`toomount hello Azure 檔案共用，在編輯之後`/etc/fstab`而不需要重新開機。

## <a name="feedback"></a>意見反應
Linux 使用者，我們想要從您的 toohear ！

hello Linux users' 群組的 Azure 檔案儲存體論壇為您提供 tooshare 意見反應您評估及採用在 Linux 上的檔案存放裝置。 電子郵件[Azure 檔案儲存體 Linux 使用者](mailto:azurefileslinuxusers@microsoft.com)toojoin hello users' 群組。

## <a name="next-steps"></a>後續步驟
請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。
* [檔案服務 REST API 參考](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [搭配使用 Azure PowerShell 與 Azure 儲存體](storage-powershell-guide-full.md)
* [如何使用 Microsoft Azure 儲存體 toouse AzCopy](storage-use-azcopy.md)
* [使用 Azure CLI hello 與 Azure 儲存體](storage-azure-cli.md#create-and-manage-file-shares)
* [常見問題集](storage-files-faq.md)
* [疑難排解](storage-troubleshoot-file-connection-problems.md)
