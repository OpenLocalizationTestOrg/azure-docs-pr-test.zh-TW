---
title: "從 Windows Azure VM 的 Azure 檔案儲存體 aaaMount |Microsoft 文件"
description: "將檔案儲存在 hello 雲端，使用 Azure 檔案儲存體，並從 Azure 虛擬機器 (VM) 掛接您雲端的檔案共用。"
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 965f1c1b3f0d07fec6d86f9312a05e02e8ce7fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a>搭配 Windows VM 使用 Azure 檔案共用 

您可以使用 Azure 檔案共用方式 toostore 及存取檔案，從您的 VM。 例如，您可以儲存指令碼或您想要您所有的 Vm tooshare 應用程式組態檔。 在本主題中，我們會示範如何 toocreate 及掛接 Azure 檔案共用，以及如何 tooupload 和下載檔案。

## <a name="connect-tooa-file-share-from-a-vm"></a>從 VM 連接 tooa 檔案共用

本節假設您已經有個檔案共用您想要 tooconnect。 如果您需要一個 toocreate，請參閱[建立檔案共用](#create-a-file-share)本主題稍後。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 左窗格中，按一下 **儲存體帳戶**。
3. 選擇儲存體帳戶
4. 在 hello**概觀**頁面的 **服務**，選取**檔案**。
5. 選取檔案共用。
6. 按一下**連接**tooopen 頁面，其中顯示 hello 命令列語法，從 Windows 或 Linux 掛接 hello 檔案共用。
7. 反白顯示 hello hello 命令語法，並將它貼到 [記事本] 或其他位置，您可以輕鬆地存取。 
8. 編輯 hello 語法 tooremove hello 前置 * * > * * 並取代*[磁碟機代號]* hello 磁碟機代號 (例如， **y:**) toomount hello 檔案共用的位置。
8. 連接 tooyour VM，然後開啟命令提示字元。
9. 貼上的 hello 編輯連接語法，叫用**Enter**。
10. Hello 連線建立後，您會收到 hello 訊息**hello 命令已順利完成。**
11. 請檢查輸入 hello 磁碟機代號 tooswitch toothat 磁碟機中的 hello 連線，然後輸入**dir** toosee hello hello 檔案共用內容。



## <a name="create-a-file-share"></a>建立檔案共用 
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 左窗格中，按一下 **儲存體帳戶**。
3. 選擇儲存體帳戶
4. 在 hello**概觀**頁面的 **服務**，選取**檔案**。
5. 在 hello 檔案服務 頁面上，按一下  **+ 檔案共用**toocreate 第一個檔案共用。 \
6. 填寫 hello 檔案共用名稱。 檔案共用名稱可以使用小寫字母、數字和單一連字號。 hello 名稱不能以連字號開頭，而且您無法使用多個連續連字號。 
7. 最長 too5120 GB，可能會填滿多少 hello 檔案上的限制。
8. 按一下**確定**toodeploy hello 檔案共用。
   
## <a name="upload-files"></a>上傳檔案
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 左窗格中，按一下 **儲存體帳戶**。
3. 選擇儲存體帳戶
4. 在 hello**概觀**頁面的 **服務**，選取**檔案**。
5. 選取檔案共用。
6. 按一下**上傳**tooopen hello**將檔案上傳**頁面。
7. 按一下 hello 資料夾圖示 toobrowse 本機檔案系統，對檔案 tooupload。   
8. 按一下**上傳**tooupload hello 檔案 toohello 檔案共用。

## <a name="download-files"></a>下載檔案
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 左窗格中，按一下 **儲存體帳戶**。
3. 選擇儲存體帳戶
4. 在 hello**概觀**頁面的 **服務**，選取**檔案**。
5. 選取檔案共用。
6. Hello 檔案上按一下滑鼠右鍵，然後選擇 **下載**toodownload 它 tooyour 本機電腦。
   

## <a name="next-steps"></a>後續步驟

您也可以使用 PowerShell 建立和管理檔案共用。 如需詳細資訊，請參閱[開始使用 Windows 上的 Azure 檔案儲存體](../../storage/files/storage-dotnet-how-to-use-files.md)。
