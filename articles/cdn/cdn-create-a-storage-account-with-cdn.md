---
title: "aaaIntegrate Azure CDN 的 Azure 儲存體帳戶 |Microsoft 文件"
description: "了解 toouse hello Azure 內容傳遞網路 (CDN) toodeliver 高頻寬內容快取從 Azure 儲存體的 blob。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: cbc2ff98-916d-4339-8959-622823c5b772
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e44716969d6a784265cc4b1da34f0d021a17b38d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a>整合 Azure 儲存體帳戶與 Azure CDN
CDN 可啟用的 toocache 來自您 Azure 儲存體的內容。 它提供開發人員一套傳遞高頻寬內容的快取 blob 和靜態計算執行個體上的 hello 美國、 歐洲、 亞洲、 澳大利亞及南美洲的實體節點內容的全球解決方案。

## <a name="step-1-create-a-storage-account"></a>步驟 1：建立儲存體帳戶
使用下列程序 toocreate Azure 訂用帳戶的新儲存體帳戶的 hello。 有了儲存體帳戶，才能存取 Azure 儲存體服務。 hello 儲存體帳戶代表 hello hello 存取 hello Azure 儲存體服務元件的每個命名空間的最高層級： Blob 服務、 佇列服務和表格服務。 如需詳細資訊，請參閱 toohello[簡介 tooMicrosoft Azure 儲存體](../storage/common/storage-introduction.md)。

toocreate 儲存體帳戶，您必須是 hello 服務系統管理員或共同管理員 hello 相關聯的訂用帳戶。

> [!NOTE]
> 有數種方法，您可以使用 toocreate 儲存體帳戶，包括 hello Azure 入口網站和 Powershell。  此教學課程中，我們將使用 hello Azure 入口網站。  
> 
> 

**toocreate Azure 訂用帳戶的儲存體帳戶**

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 左上角，選取 **新增**。 在 hello**新增**對話方塊中，選取**資料 + 儲存體**，然後按一下**儲存體帳戶**。
    
    hello**建立儲存體帳戶**刀鋒視窗隨即出現。   

    ![建立儲存體帳戶][create-new-storage-account]  

3. 在 hello**名稱**欄位中，輸入的子網域名稱。 此項目可以包含 3 至 24 個小寫字母與數字。
   
    這個值會成為 hello hello 用來定址 hello 訂用帳戶的 Blob、 佇列或表格資源的 URI 內的主機名稱。 若要解決 hello Blob 服務中的容器資源，您會將 URI 中 hello 遵循格式，其中 *&lt;StorageAccountLabel&gt;* 是指您在輸入 toohello 值**輸入的URL**:
   
    http://&lt;StorageAcountLabel&gt;.blob.core.windows.net/&lt;mycontainer&gt;
   
    **重要事項：** hello URL 標籤 form hello 子網域的 hello 儲存體帳戶 URI，而且必須是唯一在 Azure 中的所有託管服務。
   
    以程式設計方式存取此帳戶時，這個值也會用做為 hello hello 網站，或此儲存體帳戶名稱。
4. 保留 hello 的預設值**部署模型**，**帳戶類型**，**效能**，和**複寫**。 
5. 選取 hello**訂用帳戶**hello 儲存體帳戶，將會搭配使用。
6. 選取或建立 **資源群組**。  如需資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md#resource-groups)。
7. 選取儲存體帳戶的位置。
8. 按一下 [建立] 。 建立 hello 儲存體帳戶的 hello 程序可能需要幾分鐘的時間 toocomplete。

## <a name="step-2-enable-cdn-for-hello-storage-account"></a>步驟 2: Hello 儲存體帳戶啟用 CDN

與 hello 最新的整合，您現在可以啟用 CDN 的儲存體帳戶而不需離開您的儲存體入口網站擴充功能。 

1. 選取 hello 儲存體帳戶，向搜尋"CDN 」 或捲軸從 hello 左的導覽功能表，然後按一下 「 Azure CDN 」。
    
    hello **Azure CDN**刀鋒視窗隨即出現。

    ![CDN 啟用導覽][cdn-enable-navigation]
    
2. 輸入所需的 hello 資訊建立新的端點
    - **CDN 設定檔**：您可以建立新的設定檔，或使用現有設定檔。
    - **定價層**： 您只需要的 tooselect 定價層，如果您建立新的 CDN 設定檔。
    - **CDN 端點名稱**︰依照您的選擇輸入端點名稱。

    > [!TIP]
    > 依預設，hello 建立 CDN 端點會使用儲存體帳戶的 hello 主機的名稱作為來源。

    ![cdn new endpoint creation][cdn-new-endpoint-creation]

3. 在建立之後，hello 新端點會出現在上述的 hello 端點清單。

    ![CDN 儲存體新端點][cdn-storage-new-endpoint]

> [!NOTE]
> 您也可以移 tooAzure CDN 延伸 tooenable CDN。[教學課程](#Tutorial-cdn-create-profile)。
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a>步驟 3︰ 啟用其他 CDN 功能

從儲存體帳戶"Azure CDN 」 刀鋒視窗中，按一下 從 hello 清單 tooopen CDN 組態刀鋒視窗的 hello CDN 端點。 您可以為傳遞啟用其他的 CDN 功能，例如壓縮、查詢字串、地理篩選。 您也可以新增自訂網域對應 tooyour CDN 端點，並啟用 HTTPS 的自訂網域。
    
![CDN 儲存體 CDN 組態][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a>步驟 4：存取 CDN 內容
使用 hello CDN URL tooaccess 快取上 hello CDN 的內容，hello 入口網站中提供。 快取之 blob 的 hello 位址會是類似 toohello 下列：

http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\>

> [!NOTE]
> 一旦您啟用 CDN 存取 tooa 儲存體帳戶時，所有公開可用物件皆適用於 CDN 邊緣快取。 如果您修改目前在 hello CDN 中快取的物件，直到 hello CDN 快取的 hello 內容存留時間期限到期時重新整理內容，將無法使用透過 hello CDN hello 新內容。
> 
> 

## <a name="step-5-remove-content-from-hello-cdn"></a>步驟 5: Hello CDN 移除內容
如果您不再想 toocache 物件 hello Azure 內容傳遞網路 (CDN) 中，您可以採取下列步驟的 hello:

* 您可以進行 hello 容器私人而非公用。 請參閱[管理匿名讀取權限 toocontainers 和 blob](../storage/blobs/storage-manage-access-to-resources.md)如需詳細資訊。
* 您可以停用或刪除使用 hello 管理入口網站的 hello CDN 端點。
* 您可以修改您的託管的服務 toono 長回應 toorequests hello 物件。

已在 hello CDN 中快取的物件會維持快取，直到 hello hello 物件的存留時間期間過期，或直到 hello 端點都會被清除。 Hello 存留時間期間過期時，hello CDN 會檢查 toosee hello CDN 端點是否仍然有效，hello 物件仍可匿名存取。 如果不存在，然後 hello 物件將不再快取。

## <a name="additional-resources"></a>其他資源
* [如何 tooMap CDN 內容 tooa 自訂網域](cdn-map-content-to-custom-domain.md)
* [啟用自訂網域的 HTTPS](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
