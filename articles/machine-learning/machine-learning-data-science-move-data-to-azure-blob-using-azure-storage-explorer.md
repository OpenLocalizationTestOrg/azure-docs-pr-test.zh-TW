---
title: "從 Blob 儲存體與 Azure 儲存體總管 aaaMove 資料 tooand |Microsoft 文件"
description: "移動資料 tooand 從 Azure Blob 儲存體，使用 Azure 儲存體總管"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 10bd283f-0875-4c67-af63-6492270b7656
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 38d3bc009950c97d8474b0acceaf74814638dac0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azure-storage-explorer"></a>移動資料 tooand 從 Azure Blob 儲存體，使用 Azure 儲存體總管
Azure 儲存體總管是 microsoft Windows、 macOS 和 Linux 的 Azure 儲存體資料 toowork 可讓您的免費的工具。 本主題描述如何 toouse 它 tooupload 和下載資料從 Azure blob 儲存體。 hello 工具可以從下載[Microsoft Azure 儲存體總管](http://storageexplorer.com/)。

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> 如果您要使用所提供的 hello 指令碼與設定的 VM [Azure 中的資料科學虛擬機器](machine-learning-data-science-virtual-machines.md)，然後 hello VM 上已安裝 Azure 儲存體總管。
> 
> [!NOTE]
> 完成簡介 tooAzure blob 儲存體，請參閱太[Azure Blob 的基本概念](../storage/blobs/storage-dotnet-how-to-use-blobs.md)和[Azure Blob 服務](https://msdn.microsoft.com/library/azure/dd179376.aspx)。   
> 
> 

## <a name="prerequisites"></a>必要條件
本文件假設您有 Azure 訂用帳戶、 儲存體帳戶和該帳戶 hello 對應儲存體金鑰。 上傳/下載資料之前，您必須知道 Azure 儲存體帳戶名稱和帳戶金鑰。 

* tooset 註冊 Azure 訂用帳戶，請參閱[免費試用一個月](https://azure.microsoft.com/pricing/free-trial/)。
* 如需建立儲存體帳戶的指示，以及取得帳戶和金鑰的資訊，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。 請注意 hello 存取金鑰的儲存體帳戶，因為您需要此金鑰 tooconnect toohello 帳戶與 hello Azure 儲存體總管工具。
* hello Azure 儲存體總管工具可以從下載[Microsoft Azure 儲存體總管](http://storageexplorer.com/)。 接受 hello 期間的預設值安裝。

<a id="explorer"></a>

## <a name="use-azure-storage-explorer"></a>使用 Azure 儲存體總管
hello 遵循步驟文件如何使用 Azure 儲存體總管 tooupload/下載資料。 

1. 啟動 Microsoft Azure 儲存體總管。
2. 向上 hello toobring**登入 tooyour 帳戶...**精靈中，選取**Azure 帳戶設定**圖示，然後**將帳戶加入**並輸入您的認證。 ![新增 Azure 儲存體帳戶](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/add-an-azure-store-account.png)
3. 向上 hello toobring**連接儲存體 tooAzure**精靈、 選取 hello **tooAzure 存放裝置連線**圖示。 ![TooAzure 存放裝置連線](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-1.png)
4. 從您的 Azure 儲存體帳戶輸入 hello 存取金鑰，在 hello**連接儲存體 tooAzure**精靈，然後**下一步**。 ![TooAzure 存放裝置連線](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-2.png)
5. 輸入儲存體帳戶名稱在 hello**帳戶名稱**方塊，然後選取 **下一步**。 ![附加外部儲存體](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/attach-external-storage.png)
6. 現在應該會顯示 hello 新增儲存體帳戶。 toocreate blob 容器中的儲存體帳戶，以滑鼠右鍵按一下 hello **Blob 容器**中該帳戶，請選取節點**建立 Blob 容器**，然後輸入的名稱。
7. tooupload 資料 tooa 容器、 選取 hello 目標容器，按一下 hello**上傳** 按鈕。![儲存體帳戶](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/storage-accounts.png)
8. 按一下 hello **...**方 hello toohello**檔案**方塊選取一個或多個檔案 tooupload hello 檔案系統中，按一下**上傳**toobegin hello 檔案上載。![上傳檔案](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/upload-files-to-blob.png)
9. 選取 hello 的 toodownload 資料 hello 對應容器 toodownload 中的 blob，並按一下**下載**。 ![下載檔案](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/download-files-from-blob.png)

