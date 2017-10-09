---
title: "aaaHow toouse PowerShell toomanage Azure 檔案儲存體 |Microsoft 文件"
description: "了解 toouse PowerShell toomanage Azure 檔案儲存體。"
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
ms.openlocfilehash: 7bd84c9cfa31782aedf4a209cb15d4b8d92e2737
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-powershell-toomanage-azure-file-storage"></a>如何 toouse PowerShell toomanage Azure 檔案儲存體
您可以使用 Azure PowerShell toocreate 和管理檔案共用。

## <a name="install-hello-powershell-cmdlets-for-azure-storage"></a>安裝適用於 Azure 儲存體 hello PowerShell cmdlet
tooprepare toouse PowerShell 中，下載並安裝 hello Azure PowerShell cmdlet。 請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs) hello 安裝點和安裝指示。

> [!NOTE]
> 建議您下載並安裝或升級 toohello 最新的 Azure PowerShell 模組。
> 
> 

透過按一下 [啟動]，然後輸入 **Windows PowerShell** 來開啟 Azure PowerShell 視窗。 hello PowerShell 視窗會為您載入 hello Azure Powershell 模組。

## <a name="create-a-context-for-your-storage-account-and-key"></a>建立儲存體帳戶和金鑰的內容
建立 hello 儲存體帳戶的內容。 hello 內容封裝 hello 儲存體帳戶名稱和帳戶金鑰。 如需有關您的帳戶金鑰複製 hello 指示[Azure 入口網站](https://portal.azure.com)，請參閱[檢視與複製的儲存體存取金鑰](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys)。

取代`storage-account-name`和`storage-account-key`與您的儲存體帳戶名稱 hello 下列範例中的索引鍵。

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a>建立新的檔案共用
建立 hello 新的共用，名為`logs`。

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

現在，您的檔案儲存體中便有一個檔案共用。 接下來，我們將新增目錄和檔案。

> [!IMPORTANT]
> 檔案共用的 hello 名稱必須全部小寫。 如需有關為檔案共用與檔案命名的完整詳細資料，請參閱 [命名和參考共用、目錄、檔案及中繼資料](https://msdn.microsoft.com/library/azure/dn167011.aspx)。
> 
> 

## <a name="create-a-directory-in-hello-file-share"></a>在 hello 檔案共用建立目錄
Hello 共用中建立目錄。 在下列範例的 hello，名為 hello 目錄`CustomLogs`。

```powershell
# create a directory in hello share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-toohello-directory"></a>上傳本機檔案 toohello 目錄
現在您可以上傳本機檔案 toohello 目錄。 hello 例會將檔案上傳從`C:\temp\Log1.txt`。 編輯 hello 檔案路徑，使它所指 tooa 有效的檔案在本機電腦上。

```powershell
# upload a local file toohello new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-hello-files-in-hello-directory"></a>Hello 目錄中的清單 hello 檔案
toosee hello hello 目錄中的檔案，您可以列出所有 hello 目錄檔案。 此命令傳回 hello 檔案和子目錄 （如果有的話） hello CustomLogs 目錄中。

```powershell
# list files in hello new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

Get-AzureStorageFile 會傳回已傳入任何目錄物件的檔案和目錄清單。 「 Get AzureStorageFile-共用 $s"hello 根目錄中會傳回一份檔案和目錄。 tooget 子目錄中檔案的清單，您必須 toopass hello 子目錄 tooGet AzureStorageFile。 這是這個動作--hello 第一部分 hello toohello 管道命令傳回 hello 子目錄 CustomLogs 的目錄執行個體。 然後，已傳遞到 Get-AzureStorageFile，在 CustomLogs 傳回 hello 檔案和目錄。

## <a name="copy-files"></a>複製檔案
從 Azure PowerShell 0.9.7 版開始，您可以複製檔案 tooanother 檔案、 檔案 tooa blob 或 blob tooa 檔案。 下面我們將示範這些複製 tooperform 如何使用 PowerShell 指令程式的作業。

```powershell
# copy a file toohello new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob tooa file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a>後續步驟
請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。

* [常見問題集](../storage-files-faq.md)
* [在 Windows 上進行疑難排解](storage-troubleshoot-windows-file-connection-problems.md)      
* [在 Linux 上進行疑難排解](storage-troubleshoot-linux-file-connection-problems.md)    