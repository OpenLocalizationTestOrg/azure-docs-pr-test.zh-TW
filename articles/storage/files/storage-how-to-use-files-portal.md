---
title: "aaaHow toomanage 從 hello Azure 入口網站的 Azure 檔案儲存體 |Microsoft 文件"
description: "了解 toouse hello Azure 入口網站 toomanage Azure 檔案儲存體。"
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
ms.openlocfilehash: 6ad2fbbf9ee2f86748b1b175d0f63274144dc5eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-file-storage-from-hello-azure-portal"></a>如何從 toouse Azure 檔案儲存體 hello Azure 入口網站
hello [Azure 入口網站](https://portal.azure.com)管理 Azure 檔案儲存體提供使用者介面。 您可以執行下列動作，從您網頁瀏覽器的 hello:

* 建立檔案共用
* 上傳和下載檔案 tooand 從檔案共用。
* 監視 hello 實際使用量的每個檔案共用。
* 調整 hello 檔案共用大小配額。
* 複製 Windows 或 Linux 的用戶端 hello 掛接命令 toouse toomount 您的檔案共用。

## <a name="create-file-share"></a>建立檔案共用
1. 登入 toohello Azure 入口網站。
2. Hello 導覽功能表上，按一下**儲存體帳戶**或**儲存體帳戶 （傳統）**。
    
    ![示範如何 toocreate 檔案共用 hello 入口網站中的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. 選擇儲存體帳戶

    ![示範如何 toocreate 檔案共用 hello 入口網站中的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. 選擇「檔案」服務。

    ![示範如何 toocreate 檔案共用 hello 入口網站中的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. 按一下 [檔案共用]，並遵循 hello 連結 toocreate 第一個檔案共用。

    ![示範如何 toocreate 檔案共用 hello 入口網站中的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. 填入您的第一個檔案共用 hello 檔案共用名稱與 hello 檔案共用 （向上 too5120 GB) toocreate hello 大小。 一旦建立 hello 檔案共用之後，您可以從任何支援 SMB 2.1 或 SMB 3.0 的檔案系統掛接它。 您可以按一下**配額**hello 檔案共用 toochange hello 大小 hello 向上 too5120 GB 的檔案。 請參閱太[Azure 定價計算機](https://azure.microsoft.com/pricing/calculator/)使用 Azure 檔案儲存體的 tooestimate hello 儲存體成本。

    ![示範如何 toocreate 檔案共用 hello 入口網站中的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a>上傳及下載檔案
1. 選擇一個您已建立的檔案共用。

    ![示範如何從 tooupload 和下載檔案 hello 入口網站的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. 按一下**上傳**開啟檔案上傳的 hello 使用者介面。

    ![示範如何 tooupload 檔案從 hello 入口網站的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-toofile-share"></a>連接 toofile 共用
-  按一下**連接**取得掛接 hello 檔案共用中的 hello 命令列，從 Windows 和 Linux。 針對 Linux 使用者，您也可以使用參照太[如何 toouse Linux 的 Azure 檔案儲存體](../storage-how-to-use-files-linux.md)針對其他 Linux 散發套件的其他掛接指示。

    ![示範如何 toomount hello 檔案共用的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-connect.png)
-  您可以複製的 hello 掛接檔案的命令在 Windows 或 Linux 上共用，並且執行您的 Azure VM 中或在內部部署機器。

    ![適用於 Windows 和 Linux 顯示 hello 掛接命令的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

**秘訣：**  
按一下 toofind hello 儲存體帳戶存取金鑰裝載、**檢視存取這個儲存體帳戶金鑰**底部 hello hello 連接頁面。

## <a name="see-also"></a>另請參閱
請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。

* [常見問題集](../storage-files-faq.md)
* [在 Windows 上進行疑難排解](storage-troubleshoot-windows-file-connection-problems.md)      
* [在 Linux 上進行疑難排解](storage-troubleshoot-linux-file-connection-problems.md)    