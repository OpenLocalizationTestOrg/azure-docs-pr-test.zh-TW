---
title: "aaaUpload VHD 檔案使用 AzCopy tooAzure DevTest Labs |Microsoft 文件"
description: "上傳 VHD 檔案 toolab 的儲存體帳戶，使用 AzCopy"
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
ms.openlocfilehash: 14f9e933b0bd27451f6bcb94841ecc381213e578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-azcopy"></a>上傳 VHD 檔案 toolab 的儲存體帳戶，使用 AzCopy

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

在 Azure 的 DevTest Labs、 VHD 檔案可以是使用的 toocreate 自訂映像，也就是使用的 tooprovision 虛擬機器。 hello 步驟引導您完成使用 hello AzCopy 命令列公用程式 tooupload 的 VHD 檔案 tooa 實驗室儲存體帳戶。 一旦您已上傳 VHD 檔案，hello[後續步驟 > 一節](#next-steps)列出說明如何 toocreate hello 從自訂映像上傳 VHD 檔案的某些文件。 如需有關 Azure 中磁碟和 VHD 的詳細資訊，請參閱[關於虛擬機器的磁碟和 VHD](../virtual-machines/linux/about-disks-and-vhds.md)

> [!NOTE] 
>  
> AzCopy 是一個僅適用於 Windows 的命令列公用程式。

## <a name="step-by-step-instructions"></a>逐步指示

下列步驟查核行程您上傳 VHD 檔案使用 tooAzure DevTest Labs hello [AzCopy](http://aka.ms/downloadazcopy)。 

1. 收到 hello 使用 hello Azure 入口網站的 hello 實驗室儲存體帳戶名稱：

1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。

1. 選取**更多服務**，然後選取**DevTest Labs**從 hello 清單。

1. 從 hello 清單的實驗室中，選取 hello 所需的實驗室。  

1. 在 hello 實驗室刀鋒視窗中，選取 **組態**。 

1. 在 hello 實驗室**組態**刀鋒視窗中，選取**自訂映像 (Vhd)**。

1. 在 hello**自訂映像**刀鋒視窗中，選取**+ 加**。 

1. 在 hello**自訂映像**刀鋒視窗中，選取**VHD**。

1. 在 hello **VHD**刀鋒視窗中，選取**使用 PowerShell 將 VHD 上傳**。

    ![使用 PowerShell 上傳 VHD](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. hello**上傳映像使用 PowerShell**刀鋒視窗會顯示呼叫 toohello **Add-azurevhd** cmdlet。 hello 第一個參數 (*目的地*) 包含 hello URI blob 容器 (*上載*) 在 hello 下列格式：

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. 請記下 hello 完整 URI，因為它用於接下來的步驟。

1. 使用 AzCopy 的 hello VHD 檔案上傳：
 
1. [下載並安裝新版 AzCopy hello](http://aka.ms/downloadazcopy)。

1. 開啟命令視窗，並瀏覽 toohello AzCopy 安裝目錄。 （選擇性） 您可以加入 hello AzCopy 安裝位置 tooyour 系統路徑。 根據預設，AzCopy 會是已安裝的 toohello 下列目錄：

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. 使用 hello 儲存體帳戶金鑰和 blob 容器的 URI，執行下列命令在 hello 命令提示字元的 hello。 hello *vhdFileName*值必須以引號括住 toobe。 上傳 VHD 檔案 hello 程序可能很費時視 hello hello VHD 檔案大小和您的連線速度而定。   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a>後續步驟

- [在 Azure DevTest Labs 從 VHD 檔案使用 hello Azure 入口網站中建立自訂映像](devtest-lab-create-template.md)
- [使用 PowerShell 在 Azure DevTest Labs 中從 VHD 檔案建立自訂映像](devtest-lab-create-custom-image-from-vhd-using-powershell.md)