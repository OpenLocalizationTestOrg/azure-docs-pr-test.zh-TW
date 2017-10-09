---
title: "aaaCreating hello Azure Marketplace 的內部部署虛擬機器映像 |Microsoft 文件"
description: "了解並執行 hello 步驟 toocreate 在內部部署 VM 映像及部署 toohello Azure Marketplace 的其他人 toopurchase。"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 26dfbd5a-8685-4b19-987e-c20ca60540ec
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c7a265330f1e494db8d0e981a38ee00d85746bb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-hello-azure-marketplace"></a>開發 hello Azure Marketplace 的內部部署虛擬機器映像
我們強烈建議直接在 hello 雲端開發 Azure 的虛擬硬碟 (Vhd)，使用遠端桌面通訊協定。 不過，如果您必須是可能 toodownload 的 VHD，開發可以使用內部部署基礎結構。  

在內部部署開發，您必須下載 hello 作業系統 VHD 的 hello 建立 VM。 這些步驟會在前述的步驟 3.3 進行。  

## <a name="download-a-vhd-image"></a>下載 VHD 映像
### <a name="locate-a-blob-url"></a>找出 Blob URL
在訂單 toodownload hello VHD，您必須先找出 hello 作業系統磁碟的 hello blob URL。

找出 hello blob URL 從 hello 新[Microsoft Azure 入口網站](https://portal.azure.com):

1. 跳過**瀏覽** > **Vm**，，然後選取 hello 部署 VM。
2. 在下**設定**，選取 hello**磁碟**磚，以開啟 hello 磁碟刀鋒視窗。
   
   ![繪圖](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. 選取 hello **OS 磁碟**，如此即會開啟另一個的刀鋒視窗，其中會顯示磁碟內容，包括 hello VHD 的位置。
4. 複製此 Blob URL。
   
   ![繪圖](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. 現在，請刪除 hello 而不刪除 hello 備份磁碟部署 VM。 您也可以停止 hello VM 而不是刪除它。 Hello VM 正在執行時，請不要下載 hello 作業系統 VHD。
   
   ![繪圖](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a>下載 VHD
您知道 hello blob URL 之後，您可以使用 hello 下載 hello VHD [Azure 入口網站](http://manage.windowsazure.com/)或 PowerShell。  

> [!NOTE]
> 本指南建立 hello 時，hello 功能 toodownload VHD 尚未存在於 hello 新 Microsoft Azure 入口網站。  
> 
> 

**下載 hello 作業系統 VHD hello 目前透過[Azure 入口網站](http://manage.windowsazure.com/)**

1. 如果您有尚未完成，再登入 toohello Azure 入口網站。
2. 按一下 hello**儲存體** 索引標籤。
3. 選取哪些 hello 內儲存 VHD 的 hello 儲存體帳戶。
   
   ![繪圖](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. 這樣即會顯示儲存體帳戶屬性 選取 hello**容器** 索引標籤。
   
   ![繪圖](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. 選取儲存 VHD 中的 hello hello 容器。 根據預設，當從 hello 入口網站中，建立 hello VHD 儲存在 vhd 容器。
   
   ![繪圖](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. 藉由比較您儲存一個 hello URL toohello 選取 hello 正確的作業系統 VHD。
7. 按一下 [下載] 。
   
   ![繪圖](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a>使用 PowerShell 下載 VHD
此外 toousing hello Azure 入口網站，您可以使用 hello [Save-azurevhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet toodownload hello 作業系統 VHD。

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
例如，Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String>

> [!NOTE]
> **Save-azurevhd**還有**NumberOfThreads**選項可用於 hello 下載 tooincrease 平行處理原則 toomake hello 充分利用可用的頻寬。
> 
> 

## <a name="upload-vhds-tooan-azure-storage-account"></a>上傳 Vhd tooan Azure 儲存體帳戶
如果您準備的 Vhd 在內部，您會需要的 tooupload 到儲存體帳戶在 Azure 中。 這個步驟會在建立內部部署的 VHD 之後，但在取得 VM 映像認證之前進行。

### <a name="create-a-storage-account-and-container"></a>建立儲存體帳戶和容器
我們建議您到 hello 美國地區的儲存體帳戶上傳 Vhd。 單一 SKU 的所有 VHD 都應該放在單一儲存體帳戶內的單一容器中。

toocreate 儲存體帳戶，您可以使用 hello [Microsoft Azure 入口網站](https://portal.azure.com/)、 PowerShell 或 hello Linux 命令列工具。  

**從 hello Microsoft Azure 入口網站建立儲存體帳戶**

1. 按一下 [新增] 。
2. 選取 [儲存體] 。
3. 填寫 hello 儲存體帳戶名稱，然後選取 位置。
   
   ![繪圖](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. 按一下 [建立] 。
5. 建立儲存體帳戶的 hello 的 hello 刀鋒視窗應開啟。 如果沒有，請選取 [瀏覽] > [儲存體帳戶]。 在 hello 儲存體帳戶] 刀鋒視窗中，選取 [建立 hello 儲存體帳戶。
6. 選取 [容器] 。
   
   ![繪圖](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. 在 hello 容器刀鋒視窗中，選取 **新增**，然後輸入容器名稱和 hello 容器權限。 為容器權限選取 [私人]  。

> [!TIP]
> 我們建議您建立一個容器，每個您計劃 toopublish SKU。
> 
> 

  ![繪圖](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a>使用 PowerShell 建立儲存體帳戶
使用 PowerShell，建立儲存體帳戶使用 hello[新增 AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet。

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

然後您可以建立該儲存體帳戶內的容器使用 hello [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet。

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> 這些命令假設在 PowerShell 中的 hello 目前儲存體帳戶內容已設定。   請參閱太[設定 Azure PowerShell](marketplace-publishing-powershell-setup.md)如需有關 PowerShell 安裝程式。  
> 
> ### <a name="create-a-storage-account-by-using-hello-command-line-tool-for-mac-and-linux"></a>使用適用於 Mac 和 Linux hello 命令列工具來建立儲存體帳戶
> 從 [Linux 命令列工具](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)建立儲存體帳戶，如下所示。
> 
> 

        azure storage account create mystorageaccount --location "West US"

如下所示建立容器。

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a>上傳 VHD
Hello 儲存體帳戶和容器建立後，您可以上傳您準備的 Vhd。 您可以使用 PowerShell、 hello Linux 命令列工具或其他 Azure 儲存體管理工具。

### <a name="upload-a-vhd-via-powershell"></a>透過 PowerShell 上傳 VHD
使用 hello [Add-azurevhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet。

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-hello-command-line-tool-for-mac-and-linux"></a>使用適用於 Mac 和 Linux hello 命令列工具來上傳 VHD
以 hello [Linux 命令列工具](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)，使用下列 hello: azure vm 映像建立<image name>-位置<Location of hello data center>-OS Linux<LocationOfLocalVHD>

## <a name="see-also"></a>另請參閱
* [建立虛擬機器映像的 hello Marketplace](marketplace-publishing-vm-image-creation.md)
* [設定 Azure PowerShell](marketplace-publishing-powershell-setup.md)

