---
title: "aaaMount Azure 檔案共用及存取 hello 共用 windows |Microsoft 文件"
description: "裝載 Azure 檔案共用及存取在 Windows 中的 hello 共用。"
services: storage
documentationcenter: na
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
ms.openlocfilehash: eb6d58ad391adb6c06703ad694150534ccf44ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="mount-an-azure-file-share-and-access-hello-share-in-windows"></a>裝載 Azure 檔案共用及存取在 Windows 中的 hello 共用
[Azure 檔案儲存體](../storage-dotnet-how-to-use-files.md)是 Microsoft 的簡單 toouse 雲端的檔案系統。 Azure 檔案共用可在 Windows 和 Windows Server 中掛接。 本文將說明三種不同的方式 toomount Azure 檔案共用在 Windows 上： 以 hello 檔案總管 UI，透過 PowerShell，並透過 hello 命令提示字元。 

Azure 檔案共用之外 hello Azure 區域中，例如內部或在不同的 Azure 區域中裝載的順序 toomount，hello 作業系統必須支援 SMB 3.0。 

Azure 檔案共用可以掛接在 Windows 電腦上 (視 OS 版本而定，不是內部部署環境就是 Azure VM)。 下表說明 hello 

| Windows 版本        | SMB 版本 |可在 Azure VM 上掛接|可在內部部署環境掛接|
|------------------------|-------------|---------------------|---------------------|
| Windows 7              | SMB 2.1     | 是                 | 否                  |
| Windows Server 2008 R2 | SMB 2.1     | 是                 | 否                  |
| Windows 8              | SMB 3.0     | 是                 | 是                 |
| Windows Server 2012    | SMB 3.0     | 是                 | 是                 |
| Windows Server 2012 R2 | SMB 3.0     | 是                 | 是                 |
| Windows 10             | SMB 3.0     | 是                 | 是                 |

> [!Note]  
> 我們仍建議製作 hello 最新版本 Windows 的 KB。

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a></a>使用 Windows 掛接 Azure 檔案共用的必要條件 
* **儲存體帳戶名稱**: toomount Azure 檔案共用，您將需要 hello hello 儲存體帳戶名稱。

* **儲存體帳戶金鑰**: toomount Azure 檔案共用，您將需要 hello 主要 （或次要） 的儲存體金鑰。 掛接目前不支援 SAS 金鑰。

* **請確定已開啟連接埠 445**：Azure 檔案儲存體使用 SMB 通訊協定。 SMB 通訊透過 TCP 通訊埠 445-檢查 toosee，如果您的防火牆不會封鎖從用戶端電腦的 TCP 通訊埠 445。

## <a name="mount-hello-azure-file-share-with-file-explorer"></a>掛接檔案總管 中的 hello Azure 檔案的共用
> [!Note]  
> 請注意，hello 指示會顯示在 Windows 10 上，而且上較舊版本中可能稍有不同。 

1. **開啟檔案總管**： 作法是從 [開始] 功能表中的 hello 開頭或按 Win + E 捷徑。

2. **瀏覽 toohello"此 PC"hello 左手邊內的項目 hello 視窗。這會變更提供 hello 功能區中的 hello 功能表。在 hello 電腦] 功能表上選取 [對應網路磁碟機"**。
    
    ![Hello 「 對應網路磁碟機 」 的螢幕擷取畫面下拉式功能表](./media/storage-how-to-use-files-windows/1_MountOnWindows10.png)

3. **從 hello hello Azure 入口網站中的 [連線] 窗格複製 hello UNC 路徑**： 的詳細的說明如何 toofind 這項資訊可以找到[這裡](storage-how-to-use-files-portal.md#connect-to-file-share)。

    ![從 hello Azure 檔案儲存體連線 窗格中的 hello UNC 路徑](./media/storage-how-to-use-files-windows/portal_netuse_connect.png)

4. **選取 hello 磁碟機代號，然後輸入 hello UNC 路徑。** 
    
    ![Hello 」 對應網路磁碟機 對話方塊的螢幕擷取畫面](./media/storage-how-to-use-files-windows/2_MountOnWindows10.png)

5. **使用 hello 儲存體帳戶名稱前面加上`Azure\`hello 使用者名稱以及與 hello 密碼的儲存體帳戶金鑰。**
    
    ![Hello 網路認證 對話方塊的螢幕擷取畫面](./media/storage-how-to-use-files-windows/3_MountOnWindows10.png)

6. **視需要使用 Azure 檔案共用**。
    
    ![現在已掛接 Azure 檔案共用](./media/storage-how-to-use-files-windows/4_MountOnWindows10.png)

7. **當您準備好 toodismount （或中斷連線） hello Azure 檔案共用時，您可以 hello 下 hello 」 網路位置"檔案總管 中的 hello 共用的項目上按一下滑鼠右鍵，然後選取 「 中斷連線 」**。

## <a name="mount-hello-azure-file-share-with-powershell"></a>掛接 hello Azure 檔案共用使用 PowerShell
1. **使用 hello 下列命令 toomount hello Azure 檔案共用**： 記住 tooreplace `<storage-account-name>`， `<share-name>`， `<storage-account-key>`， `<desired-drive-letter>` hello 適當資訊。

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. **使用 hello Azure 檔案共用做為所需**。

3. **當您完成時，卸載 hello Azure 檔案共用使用下列命令的 hello**。

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> 您可以使用 hello`-Persist`參數`New-PSDrive`toomake hello 的 hello OS 裝載時的 Azure 檔案共用可見 toohello 其餘部分。

## <a name="mount-hello-azure-file-share-with-command-prompt"></a>掛接 hello Azure 檔案共用，透過命令提示字元
1. **使用 hello 下列命令 toomount hello Azure 檔案共用**： 記住 tooreplace `<storage-account-name>`， `<share-name>`， `<storage-account-key>`， `<desired-drive-letter>` hello 適當資訊。

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. **使用 hello Azure 檔案共用做為所需**。

3. **當您完成時，卸載 hello Azure 檔案共用使用下列命令的 hello**。

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> 您可以保存在 Windows 中的 hello 認證在重新開機設定 hello Azure 檔案共用 tooautomatically 重新連線。 hello，下列命令將會保存 hello 認證：
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a>後續步驟
請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。

* [常見問題集](../storage-files-faq.md)
* [在 Windows 上進行疑難排解](storage-troubleshoot-windows-file-connection-problems.md)      

### <a name="conceptual-articles-and-videos"></a>概念性文章和影片
* [Azure 檔案儲存體：適用於 Windows 和 Linux 的無摩擦雲端 SMB 檔案系統](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [如何 toouse Linux 的 Azure 檔案儲存體](../storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a>Azure 檔案儲存體的工具支援
* [如何 toouse AzCopy 與 Microsoft Azure 儲存體](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [使用 Azure CLI hello 與 Azure 儲存體](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [針對 Azure 檔案儲存體問題進行疑難排解 - Windows](storage-troubleshoot-windows-file-connection-problems.md)
* [針對 Azure 檔案儲存體問題進行疑難排解 - Linux](storage-troubleshoot-linux-file-connection-problems.md)

### <a name="blog-posts"></a>部落格文章
* [Azure 檔案儲存體現已公開推出](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Azure 檔案儲存體內部](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Microsoft Azure 檔案服務簡介](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [移轉資料 tooAzure 檔案](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>參考
* [Storage Client Library for .NET 參考資料](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [檔案服務 REST API 參考](http://msdn.microsoft.com/library/azure/dn167006.aspx)
