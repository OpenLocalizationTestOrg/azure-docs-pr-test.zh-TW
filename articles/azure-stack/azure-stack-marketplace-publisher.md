---
title: "aaaUse hello Marketplace toolkit toocreate 和發行 marketplace 項目 |Microsoft 文件"
description: "了解 tooquickly 以 hello 發行工具組所建立的 marketplace 項目"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: ByronR
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/14/2017
ms.author: helaw
ms.openlocfilehash: c1cf9ad1da44787901297eec12faf2a3dea82a6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#  <a name="add-marketplace-items-using-publishing-tool"></a>使用發佈工具新增 Marketplace 項目
加入您的內容 toohello [Marketplace</堆疊](azure-stack-marketplace.md)可讓您的方案使用 tooyou 且您的租用戶部署。  hello Marketplace 工具組建立根據您的 IaaS Azure Resource Manager 範本或 VM 擴充功能的 Azure Marketplace 封裝 (.azpkg) 檔案。  您也可以使用 hello Marketplace Toolkit toopublish.azpkg 檔案時，請建立具有 hello 工具或使用[手動](azure-stack-create-and-publish-marketplace-item.md)步驟。  本主題會引導您完成下載 hello 工具、 建立 marketplace 項目，根據 VM 範本中，並再發佈該項目 toohello Marketplace</堆疊。     


## <a name="prerequisites"></a>必要條件
 - 您必須在 hello Azure 堆疊主機上執行 hello 工具組，或具有[VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)從您執行 hello 工具所在的 hello 機器連線。

 - 下載 hello [Azure 堆疊快速入門範本](https://github.com/Azure/AzureStack-QuickStart-Templates/archive/master.zip)和擷取。

 - 下載 hello [Azure 圖庫封裝工具](http://aka.ms/azurestackmarketplaceitem)(AzureGalleryPackage.exe)。 

 - 發行 toohello marketplace 需要圖示和縮圖的檔案。  您可以使用您自己，或是儲存 hello[範例](azure-stack-marketplace-publisher.md#support-files)檔案在本機，這個範例。

## <a name="download-hello-tool"></a>下載 hello 工具
hello Marketplace Toolkit 可以是[hello Azure 堆疊工具儲存機制從下載](azure-stack-powershell-download.md)。


##  <a name="create-marketplace-items"></a>建立 Marketplace 項目
在本節中，您可以使用 hello Marketplace Toolkit toocreate.azpkg 格式 marketplace 項目封裝。  

### <a name="provide-marketplace-information-with-wizard"></a>以精靈提供 Marketplace 資訊
1. 從 PowerShell 工作階段中執行 hello Marketplace 工具組：
```PowerShell
    .\MarketplaceToolkit.ps1
```

2. 按一下 hello**方案** 索引標籤。此畫面會接受您的 Marketplace 項目相關資訊。 輸入您要它 tooappear hello marketplace 中的程式項目的相關資訊。  您也可以指定[參數檔案](azure-stack-marketplace-publisher.md#use-a-parameters-file)tooprepopulate hello 表單。  
    
    ![Marketplace 工具組第一個畫面的螢幕擷取畫面](./media/azure-stack-marketplace-publisher/image7.png)
3. 按一下 [瀏覽] 以選取每個圖示和螢幕擷取畫面欄位的影像檔。  您可以使用您自己的圖示，或 hello hello 範例圖示[支援檔案](azure-stack-marketplace-publisher.md#support-files)> 一節。
4. 一旦所有欄位都已都填入，選取 「 預覽解決方案 」 hello 方案 hello Marketplace 中的預覽。  您可以修改並編輯 hello 文字、 影像和螢幕擷取畫面後，再按一下**下一步**。  

### <a name="import-template-and-create-package"></a>匯入範本並建立套件
本節中，您可以匯入 hello 範本，並為您的方案使用的輸入。

1.  按一下**瀏覽**和選取 hello *azuredeploy.json* hello 101 簡單的 Windows VM 資料夾中 hello 下載範本。

    ![Marketplace 工具組第二個畫面的螢幕擷取畫面](./media/azure-stack-marketplace-publisher/image8.png)
2.  hello 部署精靈會填入*基本*hello 範本中指定每個參數的步驟和輸入項目。  您可以新增其他步驟，並在步驟之間移動輸入項。  例如，您可能會想要為您的解決方案新增「前端設定」和「後端設定」步驟。
3.  指定 hello 路徑 tooAzureGalleryPackager.exe。  
4.  按一下**建立**並 hello Marketplace 工具組封裝您的方案到.azpkg 檔案。  完成後，hello 精靈會顯示 hello 路徑 tooyour 方案檔和授與 hello 選項 toocontinue 發行您的封裝 tooAzure 堆疊。


## <a name="publish-marketplace-items"></a>發佈 Marketplace 項目
在本節中，您可以發行 hello marketplace 項目 tooyour Marketplace</堆疊。

![Marketplace 工具組第一個畫面的螢幕擷取畫面](./media/azure-stack-marketplace-publisher/image9.png)

1.  hello 精靈需要資訊 toopublish 方案：
    
    |欄位|說明|
    |-----|-----|
    | 服務管理員名稱 | 服務管理員帳戶。  範例：ServiceAdmin@mydomain.onmicrosoft.com |
    | 密碼 | 服務管理員帳戶的密碼。 |
    | API 端點 | Azure Stack Azure Resource Manager 端點。  範例：management.local.azurestack.external |
2.  按一下**發行**，顯示 hello 發行記錄。
3.  您是現在可以 toodeploy hello Azure 堆疊入口網站透過您已發行的項目。


## <a name="use-a-parameters-file"></a>使用參數檔案
您也可以使用參數檔案 toocomplete hello marketplace 項目資訊。  

hello Marketplace Toolkit 包含*solution.parameters.ps1*使用 toocreate 參數檔案。


## <a name="support-files"></a>支援檔案
| 說明 | 範例 |
| ----- | ----- |
| 40 x 40.png 圖示 | ![](./media/azure-stack-marketplace-publisher/image1.png) |
| 90x90 .png 圖示 | ![](./media/azure-stack-marketplace-publisher/image2.png) |
| 115x115 .png 圖示 | ![](./media/azure-stack-marketplace-publisher/image3.png) |
| 255x115 .png 圖示 | ![](./media/azure-stack-marketplace-publisher/image4.png) |
| 533x324 .png 縮圖 | ![](./media/azure-stack-marketplace-publisher/image5.png) |


