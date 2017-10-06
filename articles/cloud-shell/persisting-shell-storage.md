---
title: "在 Azure 雲端介面 （預覽） 中的 aaaPersist 檔案 |Microsoft 文件"
description: "逐步解說 Azure Cloud Shell 如何保存檔案。"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: b230453d5551c545553d63559741950206e4f1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a>在 Azure Cloud Shell 中保存檔案
雲端殼層會利用 Azure 檔案儲存體 toopersist 檔案，在工作階段之間。

## <a name="set-up-a-clouddrive-file-share"></a>設定 `clouddrive` 檔案共用
初始一開始，雲端殼層會提示您 tooassociate 新的或現有的檔案共用 toopersist 檔案跨工作階段。

### <a name="create-new-storage"></a>建立新的儲存體

當您使用基本設定，並選取的訂用帳戶時，雲端殼層會代表您在最接近 tooyou hello 支援區域中建立三個資源：
* 資源群組：`cloud-shell-storage-<region>`
* 儲存體帳戶：`cs<uniqueGuid>`
* 檔案共用：`cs-<user>-<domain>-com-<uniqueGuid>`

![hello 訂用帳戶設定](media/basic-storage.png)

hello 檔案共用做為所掛接`clouddrive`中您`$Home`目錄。 hello 檔案共用也是使用的 toostore 會自動為您建立的 5 GB 映像更新並保存您`$Home`目錄。 這是單次的動作，並 hello 檔案共用會自動掛接在後續工作階段。

### <a name="use-existing-resources"></a>使用現有的資源

藉由使用 hello 進階選項，您可以結合現有的資源。 Hello 儲存安裝程式提示出現時，選取**顯示進階設定**tooview 其他選項。 現有的檔案共用接收 5 GB 使用者映像 toopersist 您`$Home`目錄。 hello 下拉式功能表經過篩選後，您的雲端殼層區域與本機備援和地理備援儲存體帳戶。

![hello 資源群組設定](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a>使用 Azure 資源原則限制資源建立
您在 Cloud Shell 中建立的儲存體帳戶都會標記 `ms-resource-usage:azure-cloud-shell`。 如果您希望 toodisallow 使用者無法在雲端介面中建立儲存體帳戶，建立[標記的 Azure 資源原則](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags)，都會觸發這個特定的標記。

## <a name="how-cloud-shell-works"></a>Cloud Shell 的運作方式
雲端殼層保存檔案透過這兩個 hello 下列方法：
* 建立磁碟映像的程式`$Home`hello 目錄內的所有目錄 toopersist 都內容。 hello 磁碟映像會儲存在您指定的檔案共用做為`acc_<User>.img`在`fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`，並自動進行同步的變更。

* 在您的 `$Home` 目錄中，將指定的檔案共用掛接為 `clouddrive`，以便直接與檔案共用互動。 `/Home/<User>/clouddrive`對應太`fileshare.storage.windows.net/fileshare`。
 
> [!NOTE]
> `$Home` 目錄中的所有檔案 (例如 SSH 金鑰) 會都保存於已掛接檔案共用中儲存的使用者磁碟映像中。 當您在 `$Home` 目錄和已掛接的檔案共用中保存資訊時，請套用最佳做法。

## <a name="use-hello-clouddrive-command"></a>使用 hello`clouddrive`命令
您可以使用雲端殼層執行命令，稱為`clouddrive`，它可讓您 toomanually 更新 hello 檔案共用的掛接的 tooCloud 殼層。
![執行 hello"clouddrive 」 命令](media/clouddrive-h.png)

## <a name="mount-a-new-clouddrive"></a>掛接新的 `clouddrive`

### <a name="prerequisites-for-manual-mounting"></a>手動掛接的先決條件
您可以更新 hello 與雲端殼層使用 hello 相關聯的檔案共用`clouddrive mount`命令。

如果您裝載現有的檔案共用，hello 儲存體帳戶必須是：
* 本機備援儲存體或地理備援儲存體 toosupport 檔案共用。
* 位於您的指派區域。 當您登入，hello 區域會指派給您 hello 資源群組名稱中所列的 toois `cloud-shell-storage-<region>`。

### <a name="supported-storage-regions"></a>支援的儲存體區域
hello Azure 檔案必須位在 hello 相同與您正在裝載它們的 hello 雲端殼層電腦的區域。 雲端殼層叢集目前存在於 hello 下列區域：
|領域|區域|
|---|---|
|美洲|美國東部、美國中南部、美國西部|
|歐洲|北歐、西歐|
|亞太地區|印度中部、東南亞|

### <a name="hello-clouddrive-mount-command"></a>hello`clouddrive mount`命令

> [!NOTE]
> 如果您要裝載新的檔案共用，為建立新的使用者映像您`$Home`目錄，因為您先前`$Home`映像就會保留在 hello 先前的檔案共用。

執行 hello`clouddrive mount`命令搭配下列參數的 hello:

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

tooview 詳細資訊，請執行`clouddrive mount -h`，如下所示：

![執行 hello ' clouddrive mount'command](media/mount-h.png)

## <a name="unmount-clouddrive"></a>卸載 `clouddrive`
您可以取消掛接的掛接的 tooCloud 殼層隨時將檔案共用。 一旦您的檔案共用正在卸載所造成，您將會提示的 toomount 新檔案共用之前 tooyour 下一個工作階段。

tooremove 檔案共用從雲端殼層：
1. 執行 `clouddrive unmount`。
2. 了解，並確認 hello 提示。

檔案共用將會繼續 tooexist，除非您手動將它刪除。 Cloud Shell 在後續的工作階段中將不再搜尋此檔案共用。

tooview 詳細資訊，請執行`clouddrive unmount -h`，如下所示：

![執行 hello ' clouddrive unmount'command](media/unmount-h.png)

> [!WARNING]
> 執行這個命令不會刪除任何資源。 手動刪除資源群組、 儲存體帳戶或檔案共用，則對應的 tooCloud 殼層會永久刪除您`$Home`目錄映像和檔案共用中的任何其他檔案。 此動作無法復原。

## <a name="list-clouddrive-file-shares"></a>列出 `clouddrive` 檔案共用
掛接的檔案共用為 toodiscover `clouddrive`，執行下列 hello`df`命令。 

hello 檔案路徑 tooclouddrive 顯示您的儲存體帳戶名稱和檔案共用 hello URL 中。 例如， `//storageaccountname.file.core.windows.net/filesharename`

```
justin@Azure:~$ df
Filesystem                                               1K-blocks     Used Available Use% Mounted on
overlay                                                   30428648 15585636  14826628  52% /
tmpfs                                                       986704        0    986704   0% /dev
tmpfs                                                       986704        0    986704   0% /sys/fs/cgroup
/dev/sda1                                                 30428648 15585636  14826628  52% /etc/hosts
shm                                                          65536        0     65536   0% /dev/shm
//mystoragename.file.core.windows.net/fileshareName        6291456  5242944   1048512  84% /usr/justin/clouddrive
/dev/loop0                                                 5160576   601652   4296780  13% /home/justin
```

## <a name="transfer-local-files-toocloud-shell"></a>傳輸的本機檔案 tooCloud 殼層
hello`clouddrive`與 hello Azure 入口網站的儲存體 刀鋒視窗的目錄同步。 使用此刀鋒視窗 tootransfer 本機檔案 tooor 」，從檔案共用。 更新雲端殼層中的檔案，當您重新整理 hello 刀鋒視窗是會反映 hello 檔案儲存體 GUI。

### <a name="download-files"></a>下載檔案

![本機檔案清單](media/download.png)
1. 在 hello Azure 入口網站，移 toohello 掛接的檔案共用。
2. 選取 hello 目標檔案。
3. 選取 hello**下載** 按鈕。

### <a name="upload-files"></a>上傳檔案

![本機檔案上傳的 toobe](media/upload.png)
1. 移 tooyour 掛接的檔案共用。
2. 選取 hello**上傳** 按鈕。
3. 選取 hello 檔案或您想 tooupload 檔案。
4. 確認 hello 上傳。

您現在應該會看到 hello 檔案的存取在您`clouddrive`目錄雲端 Shell 中。

## <a name="next-steps"></a>後續步驟
[Cloud Shell 快速入門](quickstart.md) <br>
[了解 Azure 檔案儲存體](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage) <br>
[了解儲存體標籤](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) <br>
