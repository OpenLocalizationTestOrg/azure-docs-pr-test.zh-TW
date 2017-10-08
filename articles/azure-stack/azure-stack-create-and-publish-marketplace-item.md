---
title: "aaaCreate 和發佈 Azure 堆疊中的 Marketplace 項目 |Microsoft 文件"
description: "在 Azure Stack 中建立和發佈 Marketplace 項目。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 77e5f60c-a86e-4d54-aa8d-288e9a889386
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: erikje
ms.openlocfilehash: 6f6a7af96f9d8de9098ac7eee4ba2ac9bc3d6a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-publish-a-marketplace-item"></a>建立及發行 Marketplace 項目
## <a name="create-a-marketplace-item"></a>建立 Marketplace 項目
1. [下載](http://www.aka.ms/azurestackmarketplaceitem)hello Azure 圖庫 Packager 工具和 hello 範例 Marketplace</堆疊項目。
2. 開啟 hello 範例 Marketplace 項目，並重新命名 hello **SimpleVMTemplate**資料夾。 (相同的名稱，為您的 Marketplace 項目-例如，使用 hello **Contoso.TodoList**。)此資料夾包含：
   
       /Contoso.TodoList/
       /Contoso.TodoList/Manifest.json
       /Contoso.TodoList/UIDefinition.json
       /Contoso.TodoList/Icons/
       /Contoso.TodoList/Strings/
       /Contoso.TodoList/DeploymentTemplates/
3. [建立 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)，或從 GitHub 選擇範本。 hello Marketplace 項目會使用此範本 toocreate 資源。
4. toomake 確定 hello 資源可以成功地部署、 測試與 Microsoft Azure 堆疊 Api hello hello 範本。
5. 如果您的範本依賴於虛擬機器映像，請依照 hello 指示太[新增虛擬機器映像 tooAzure 堆疊](azure-stack-add-vm-image.md)。
6. 將您的 Azure Resource Manager 範本儲存在 hello **/Contoso.TodoList/DeploymentTemplates/**資料夾。
7. 選擇 hello 圖示與您的 Marketplace 項目的文字。 新增圖示 toohello**圖示**資料夾，並加入文字 toohello**資源**檔案在 hello**字串**資料夾。 使用圖示 hello Small、 Medium、 Large 和通用命名慣例。 如需詳細的說明，請參閱 [Marketplace 項目 UI 參考](#reference-marketplace-item-ui)。
   
   > [!NOTE]
   > 所有四個圖示的大小 （小型、 中型的大，範圍） 所需的正確建立 hello Marketplace 項目。
   > 
   > 
8. 在 hello **manifest.json**檔案中，變更**名稱**toohello 您的 Marketplace 項目名稱。 也會變更**發行者**tooyour 名稱或公司。
9. 在下**成品**，變更**名稱**和**路徑**toohello hello Azure 資源管理員範本，包含正確的資訊。
   
         "artifacts": [
            {
                "name": "Type your template name",
                "type": "Template",
                "path": "DeploymentTemplates\\Type your path",
                "isDefault": true
            }
10. 取代**我的 Marketplace 項目**與 hello 分類您的 Marketplace 項目應該出現的位置清單。
    
             "categories":[
                 "My Marketplace Items"
              ],
11. 任何進一步編輯 toomanifest.json 參照太[參考： Marketplace 項目 manifest.json](#reference-marketplace-item-manifestjson)。
12. toopackage hello 資料夾到.azpkg 檔案中，開啟命令提示字元，然後執行下列命令的 hello:
    
        AzureGalleryPackager.exe package –m <path toomanifest.json> -o <output location for hello package>
    
    > [!NOTE]
    > hello 完整路徑 toohello 輸出封裝必須存在。 例如，如果 hello 輸出路徑 C:\MarketPlaceItem\yourpackage.azpkg，hello 資料夾 C:\MarketPlaceItem 必須存在。
    > 
    > 

## <a name="publish-a-marketplace-item"></a>發佈 Marketplace 項目
1. 使用 PowerShell 或 Azure 儲存體總管 tooupload 您的 Marketplace 項目 (.azpkg) tooAzure Blob 儲存體。 您可以上傳 toolocal 堆疊 Azure 儲存體，或上傳 tooAzure 儲存體。 （它是一個暫存位置的 hello 封裝）。請確定該 hello blob 是可公開存取。
2. 在 hello 用戶端 hello Microsoft Azure 堆疊環境中的虛擬機器，請確定您的 PowerShell 工作階段已設定使用您的服務系統管理員認證。 您可以找到有關如何 tooauthenticate Azure 堆疊中的 PowerShell 中[部署範本，以使用 PowerShell](azure-stack-deploy-template-powershell.md)。
3. 使用 hello**新增 AzureRMGalleryItem** PowerShell cmdlet toopublish hello Marketplace 項目 tooAzure 堆疊。 例如：
   
       Add-AzureRMGalleryItem -GalleryItemUri `
       https://sample.blob.core.windows.net/gallerypackages/Microsoft.SimpleTemplate.1.0.0.azpkg –Verbose
   
   | 參數 | 說明 |
   | --- | --- |
   | SubscriptionID |管理訂用帳戶 ID。 您可以使用 PowerShell 來擷取它。 如果您想使用 tooget 它在 hello 入口網站移 toohello 提供者的訂用帳戶，並複製 hello 訂用帳戶識別碼。 |
   | GalleryItemUri |已上傳的 toostorage 程式庫封裝的 blob URI。 |
   | Apiversion |設定為 **2015-04-01**。 |
4. 移 toohello 入口網站。 您現在可以看到在 hello 入口網站-身為系統管理員或租用戶身分 hello Marketplace 項目。
   
   > [!NOTE]
   > hello 封裝可能需要花費幾分鐘的時間 tooappear。
   > 
   > 
5. 您的 Marketplace 項目現在已儲存 toohello Marketplace</堆疊。 您可以選擇 toodelete 它從您的 Blob 儲存體位置。
6. 您可以移除 Marketplace 項目使用 hello**移除 AzureRMGalleryItem** cmdlet。 範例：
   
        Remove-AzureRMGalleryItem -Name Microsoft.SimpleTemplate.1.0.0  –Verbose
   
   > [!NOTE]
   > hello Marketplace UI 中移除項目之後，可能會顯示錯誤。 toofix hello 錯誤時，按一下 **設定**hello 入口網站中。 然後，在 [入口網站自訂] 之下，選取 [捨棄修改]。
   > 
   > 

## <a name="reference-marketplace-item-manifestjson"></a>參考：Marketplace 項目 manifest.json
### <a name="identity-information"></a>身分識別資訊
| 名稱 | 必要 | 類型 | 條件約束 | 說明 |
| --- | --- | --- | --- | --- |
| 名稱 |X |String |[A-a-za-z0-9] + | |
| 發行者 |X |String |[A-a-za-z0-9] + | |
| 版本 |X |String |[SemVer v2](http://semver.org/) | |

### <a name="metadata"></a>中繼資料
| 名稱 | 必要 | 類型 | 條件約束 | 說明 |
| --- | --- | --- | --- | --- |
| DisplayName |X |String |建議 80 個字元 |hello 入口網站可能無法顯示項目名稱依正常程序是否超過 80 個字元。 |
| PublisherDisplayName |X |String |建議 30 個字元 |hello 入口網站可能無法顯示您的發行者名稱依正常程序是否超過 30 個字元。 |
| PublisherLegalName |X |String |上限 256 個字元 | |
| 摘要 |X |String |60 too100 個字元 | |
| LongSummary |X |String |140 too256 個字元 |目前在 Azure Stack 中不適用。 |
| 說明 |X |[HTML](https://auxdocs.azurewebsites.net/en-us/documentation/articles/gallery-metadata#html-sanitization) |500 too5、 000 個字元 | |

### <a name="images"></a>映像
hello Marketplace 使用 hello 下列圖示：

| 名稱 | 寬度 | 高度 | 注意事項 |
| --- | --- | --- | --- |
| 寬 |255 像素 |115 像素 |一律需要 |
| 大型 |115 像素 |115 像素 |一律需要 |
| 中型 |90 像素 |90 像素 |一律需要 |
| 小型 |40 像素 |40 像素 |一律需要 |
| 螢幕擷取畫面 |533 像素 |32 像素 |選用 |

### <a name="categories"></a>類別
每個 Marketplace 項目應該標記的類別，可識別 hello 入口網站 UI hello 項目出現的位置。 您可以選擇其中一個 hello 現有類別目錄中 Azure 堆疊 (運算、 資料 + 儲存體，等) 或選擇新密碼。

### <a name="links"></a>連結
每個 Marketplace 項目可以包含各種連結 tooadditional 內容。 hello 連結已指定為一份名稱的 Uri。

| 名稱 | 必要 | 類型 | 條件約束 | 說明 |
| --- | --- | --- | --- | --- |
| DisplayName |X |String |上限 64 個字元 | |
| Uri |X |URI | | |

### <a name="additional-properties"></a>其他屬性
加法 toohello 前面中繼資料，在 Marketplace 作者可以提供自訂的索引鍵/值組資料，在下列形式的 hello:

| 名稱 | 必要 | 類型 | 條件約束 | 說明 |
| --- | --- | --- | --- | --- |
| DisplayName |X |String |上限 25 個字元 | |
| 值 |X |String |上限 30 個字元 | |

### <a name="html-sanitization"></a>HTML 病毒掃描
允許 HTML 的任何欄位，hello 下列項目和屬性可：

h1、h2、h3、h4、h5、p、ol、ul、li、a[target|href]、br、strong、em、b、i

## <a name="reference-marketplace-item-ui"></a>參考：Marketplace 項目 UI
圖示和文字 hello Azure 堆疊入口網站中所見的 Marketplace 項目為，如下所示。

### <a name="create-blade"></a>建立刀鋒視窗
![建立刀鋒視窗](media/azure-stack-marketplace-item-ui-reference/image1.png)

### <a name="marketplace-item-details-blade"></a>Marketplace 項目詳細資料刀鋒視窗
![Marketplace 項目詳細資料刀鋒視窗](media/azure-stack-marketplace-item-ui-reference/image3.png)

