---
title: "aaaUpload VHD 檔案使用 Microsoft Azure 儲存體總管 tooAzure DevTest Labs |Microsoft 文件"
description: "上傳 VHD 檔案 toolab 的儲存體帳戶使用 Microsoft Azure 儲存體總管"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 686691e3676cea4b2d7cd8bf045bc43a792c667e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-microsoft-azure-storage-explorer"></a>上傳 VHD 檔案 toolab 的儲存體帳戶使用 Microsoft Azure 儲存體總管

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

在 Azure 的 DevTest Labs、 VHD 檔案可以是使用的 toocreate 自訂映像，也就是使用的 tooprovision 虛擬機器。 本文將說明如何 toouse [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)tooupload VHD 檔案 tooa 實驗室儲存體帳戶。 一旦您已上傳 VHD 檔案，hello[後續步驟 > 一節](#next-steps)列出說明如何 toocreate hello 從自訂映像上傳 VHD 檔案的某些文件。 如需有關 Azure 中磁碟和 VHD 的詳細資訊，請參閱[關於虛擬機器的磁碟和 VHD](../virtual-machines/linux/about-disks-and-vhds.md)

## <a name="step-by-step-instructions"></a>逐步指示

下列步驟查核行程您上傳 VHD 檔案使用 tooDevTest 實驗室 hello [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)。

1. [下載並安裝 hello 最新版 Microsoft Azure 儲存體總管 hello](http://www.storageexplorer.com)。

1. 收到 hello 使用 hello Azure 入口網站的 hello 實驗室儲存體帳戶名稱：

    1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。
    
    1. 選取**更多服務**，然後選取**DevTest Labs**從 hello 清單。
    
    1. 從 hello 清單的實驗室中，選取 hello 所需的實驗室。  
    
    1. 在 hello 實驗室刀鋒視窗中，選取 **組態**。 
    
    1. 在 hello 實驗室**組態**刀鋒視窗中，選取**自訂映像 (Vhd)**。
    
    1. 在 hello**自訂映像**刀鋒視窗中，選取**+ 加**。 
    
    1. 在 hello**自訂映像**刀鋒視窗中，選取**VHD**。
    
    1. 在 hello **VHD**刀鋒視窗中，選取**使用 PowerShell 將 VHD 上傳**。
    
        ![使用 PowerShell 上傳 VHD][0]
    
    1. hello**上傳映像使用 PowerShell**刀鋒視窗會顯示呼叫 toohello **Add-azurevhd** cmdlet。 hello 第一個參數 (*目的地*) 包含下列格式的 hello 中的 hello 實驗室 hello 儲存體帳戶名稱：
    
        https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/... 

    1. 請記 hello 儲存體帳戶名稱，因為它在稍後步驟中使用。
    
1. 連接 tooan 使用存放裝置總管的 Azure 訂用帳戶。

    > [!TIP] 
    > 
    > 儲存體總管支援數個連線選項。 本節說明您的 Azure 訂用帳戶相關聯的連接 tooa 儲存體帳戶。 toosee hello 儲存體總管支援其他連接選項，請參閱 toohello 文章[開始使用儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)。
 
    1. 開啟儲存體總管。
    
    1. 在儲存體總管中，選取 [Azure 帳戶設定]。 
    
        ![Azure 帳戶設定][1]
    
    1. hello 左的窗格會顯示您已登入的 hello Microsoft 帳戶。 tooconnect tooanother 帳戶，請選取**將帳戶加入**，並遵循 hello 對話方塊 toosign 使用至少一個有效的 Azure 訂閱相關聯的 Microsoft 帳戶。
    
        ![新增帳戶][2]
    
    1. 一旦您已成功登入 Microsoft 帳戶，hello 左的窗格中填入 hello 與該帳戶相關聯的 Azure 訂用帳戶。 選取 hello Azure 訂用帳戶與您想 toowork，，然後選取**套用**。 (選取**所有訂用帳戶**切換 hello 所有的選取範圍或列出任何 hello Azure 訂用帳戶。)
    
        ![選取 Azure 訂用帳戶][3]
    
    1. hello 左的窗格會顯示 hello 與 hello 選取 Azure 訂用帳戶相關聯的儲存體帳戶。
    
        ![已選取的 Azure 訂用帳戶][4]

1. 找出 hello 實驗室儲存體帳戶：

    1. Hello 存放裝置總管左窗格中，找出並展開 hello hello 擁有 hello 實驗室的 Azure 訂用帳戶節點。
    
    1. Hello 訂用帳戶的節點下，依序展開**儲存體帳戶**。

    1. 展開 hello 實驗室儲存體帳戶節點 tooreveal 節點**Blob 容器**，**檔案共用**，**佇列**，和**資料表**。
    
    1. 展開 hello **Blob 容器**節點。
    
    1. Hello 右窗格中選取 hello 上傳 blob 容器 toodisplay 其內容。
        
        ![上傳目錄][5]

1. 使用儲存體總管的 hello VHD 檔案上傳：

    1. Hello 存放裝置總管右窗格中，您應該會看到 hello 中的 hello blob 清單**上載**hello 實驗室儲存體帳戶的 blob 容器。 在 hello blob 編輯器工具列上，選取 **上傳** 
        
        ![上傳按鈕][6]
    
    1. 從 hello**上傳**下拉式選單中，選取**上傳檔案...**.
    
    1. 在 hello**將檔案上傳**對話方塊中，選取 hello 省略符號。
        
        ![選取檔案][8]  

    1. 在 hello**選取檔案 tooupload**  對話方塊中，瀏覽 toohello 預期 VHD 檔案，選取它，並選取**開啟**。
    
    1. 當傳回 toohello**將檔案上傳** 對話方塊中，變更**Blob 類型**太**分頁 Blob**。
    
    1. 選取 [上傳] 。

        ![選取檔案][9]  
    
    1. 儲存體總管 hello**活動記錄檔** 窗格會顯示 hello 下載狀態 （與連結 toocancel hello 上傳）。 上傳 VHD 檔案 hello 程序可能很費時視 hello hello VHD 檔案大小和您的連線速度而定。 

        ![上傳檔案狀態][10]  

## <a name="next-steps"></a>後續步驟

- [在 Azure DevTest Labs 從 VHD 檔案使用 hello Azure 入口網站中建立自訂映像](devtest-lab-create-template.md)
- [使用 PowerShell 在 Azure DevTest Labs 中從 VHD 檔案建立自訂映像](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

[0]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-image-using-psh.png
[1]: ./media/devtest-lab-upload-vhd-using-storage-explorer/settings-icon.png
[2]: ./media/devtest-lab-upload-vhd-using-storage-explorer/add-account-link.png
[3]: ./media/devtest-lab-upload-vhd-using-storage-explorer/subscriptions-list.png
[4]: ./media/devtest-lab-upload-vhd-using-storage-explorer/storage-accounts-list.png
[5]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-dir.png
[6]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-button.png
[7]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-files.png
[8]: ./media/devtest-lab-upload-vhd-using-storage-explorer/select-file.png
[9]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-file.png
[10]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-status.png
