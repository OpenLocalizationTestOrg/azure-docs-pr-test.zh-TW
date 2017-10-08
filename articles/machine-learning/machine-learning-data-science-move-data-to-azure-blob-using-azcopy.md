---
title: "從 Azure Blob 儲存體，使用 AzCopy aaaMove 資料 tooand |Microsoft 文件"
description: "從 Azure Blob 儲存體，使用 AzCopy 移動資料 tooand"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c309ceb2-0e83-4a07-b16d-c997dcd62d5c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: b381ba004ac16879b6c633950d03d13ad82d5b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azcopy"></a>從 Azure Blob 儲存體，使用 AzCopy 移動資料 tooand
AzCopy 是上傳、 下載和複製資料 tooand 從 Microsoft Azure blob、 檔案和資料表儲存體設計的命令列公用程式。

如需使用以 hello Azure 平台上安裝 AzCopy 和其他資訊的指示，請參閱[開始使用 AzCopy 命令列公用程式的 hello](../storage/common/storage-use-azcopy.md)。

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> 如果您要使用所提供的 hello 指令碼與設定的 VM [Azure 中的資料科學虛擬機器](machine-learning-data-science-virtual-machines.md)，然後 AzCopy hello VM 上已安裝。
> 
> [!NOTE]
> 完成簡介 tooAzure blob 儲存體，請參閱太[Azure Blob 的基本概念](../storage/blobs/storage-dotnet-how-to-use-blobs.md)和太[Azure Blob 服務](https://msdn.microsoft.com/library/azure/dd179376.aspx)。
> 
> 

## <a name="prerequisites"></a>必要條件
本文件假設您有 Azure 訂閱，儲存體帳戶和 hello 對應的儲存體金鑰，該帳戶。 上傳/下載資料之前，您必須知道 Azure 儲存體帳戶名稱和帳戶金鑰。

* tooset 註冊 Azure 訂用帳戶，請參閱[免費試用一個月](https://azure.microsoft.com/pricing/free-trial/)。
* 如需建立儲存體帳戶的指示，以及取得帳戶和金鑰的資訊，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。

## <a name="run-azcopy-commands"></a>執行 AzCopy 命令
toorun 的 AzCopy 命令開啟命令視窗，並瀏覽您 hello AzCopy.exe 可執行檔所在的電腦上的 toohello AzCopy 安裝目錄。 

hello 的 AzCopy 命令的基本語法如下：

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> 您可以加入 hello AzCopy 安裝位置 tooyour 系統路徑，並從任何目錄執行 hello 命令。 根據預設，AzCopy 會太安裝*%programfiles (x86) %\Microsoft SDKs\Azure\AzCopy*或*%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*。
> 
> 

## <a name="upload-files-tooan-azure-blob"></a>上傳檔案 tooan Azure blob
tooupload 檔案，使用下列命令的 hello:

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a>從 Azure Blob 下載檔案
toodownload 檔案，以從 Azure blob，下列命令使用 hello:

    # Downloading blobs toolocal file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a>在 Azure 容器之間傳輸 Blob
Azure 的容器之間的 tootransfer blob 使用 hello 下列命令：

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: hello sub directory in hello container
    <your_local_directory>: directory of local file system where files toobe uploaded from or hello directory of local file system files toobe downloaded to
    <file_pattern>: pattern of file names toobe transferred. hello standard wildcards are supported


## <a name="tips-for-using-azcopy"></a>使用 AzCopy 的秘訣
> [!TIP]
> 1. **上傳**檔案時，*/S* 將以遞迴方式上傳檔案。 如果沒有這個參數，則不會上傳子目錄中的檔案。  
> 2. 當**下載**檔案， */S*搜尋才 hello 指定的目錄和其子目錄中的所有檔案 hello 容器以遞迴方式或相符的所有檔案都 hello 都 hello 指定中指定的模式目錄和其子目錄中，會下載。  
> 3. 您無法指定**特定 blob 檔案**toodownload 使用 hello */來源*參數。 toodownload 特定檔案，指定使用 hello hello blob 檔案名稱 toodownload */模式*參數。 **/S**參數可以是檔案名稱模式以遞迴方式使用的 toohave AzCopy 尋找。 如果沒有 hello 模式參數，AzCopy 會下載該目錄中的所有檔案。
> 
> 

