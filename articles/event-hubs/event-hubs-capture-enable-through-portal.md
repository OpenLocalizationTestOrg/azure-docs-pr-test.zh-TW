---
title: "事件中心擷取 aaaAzure 啟用透過入口網站 |Microsoft 文件"
description: "啟用使用 hello Azure 入口網站的 hello 事件中心擷取功能。"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: 27c7528552c497a4d98873a22bd56a991c66247c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-event-hubs-capture-using-hello-azure-portal"></a>啟用事件中心擷取使用 hello Azure 入口網站

您可以在 hello 事件中心建立期間使用 hello 設定擷取[Azure 入口網站](https://portal.azure.com)。 您可以任一擷取 hello 資料 tooan Azure [Blob 儲存體](https://azure.microsoft.com/services/storage/blobs/)容器或 tooan [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/)帳戶。

## <a name="capture-data-tooan-azure-storage-account"></a>擷取資料 tooan Azure 儲存體帳戶  

當您建立事件中樞時，您可以按一下 hello 啟用擷取**上**按鈕在 hello**建立事件中樞**入口網站的刀鋒視窗。 然後依序按一下中指定的儲存體帳戶和容器**Azure 儲存體**在 hello**擷取提供者**方塊。 事件中心擷取使用儲存體服務對服務驗證，因為您不需要 toospecify 儲存體連接字串。 hello 資源選擇器會自動選取儲存體帳戶的 hello 資源 URI。 如果您使用 Azure Resource Manager，您必須以字串形式明確提供此 URI。

hello 預設時間間隔為 5 分鐘。 hello 最小值為 1，最多 15 hello。 hello**大小**視窗有 10-500 MB 的範圍。

![][1]

## <a name="capture-data-tooan-azure-data-lake-store-account"></a>擷取資料 tooan Azure Data Lake Store 帳戶

toocapture 資料 tooAzure 資料湖存放區，您建立的 Data Lake Store 帳戶，以及事件中心：

### <a name="create-an-azure-data-lake-store-account-and-folders"></a>建立 Azure Data Lake Store 帳戶和資料夾

1. 建立 Data Lake Store 帳戶中的 hello 指示[開始使用 Azure 資料湖存放區使用 hello Azure 入口網站](../data-lake-store/data-lake-store-get-started-portal.md)。 
2. 此帳戶時，遵照 hello 中的 hello 底下建立資料夾[Azure Data Lake Store 帳戶中建立資料夾](../data-lake-store/data-lake-store-get-started-portal.md#createfolder)> 一節。
3. 在 hello Data Lake Store 帳戶刀鋒視窗中，按一下 **資料總管**。
4. 按一下 [存取]。
5. 按一下 [新增] 。
6. 在 hello**依名稱或電子郵件搜尋**方塊中，輸入**Microsoft.EventHubs** ，然後選取此選項。 
7. hello**權限**索引標籤會出現。 設定 hello 權限，hello 遵循圖所示：

    ![][6]

8. 按一下 [確定] 。
9. 現在，建立資料夾 hello 根資料夾中，瀏覽 toohello 目標資料夾，然後按一下 hello 資料夾名稱。
10. 按一下 [存取]。
11. 按一下 [新增] 。
12. 在 hello**依名稱或電子郵件搜尋**方塊中，輸入**Microsoft.EventHubs** ，然後選取此選項。
13. hello**權限**索引標籤會出現一次。 設定 hello 權限，hello 遵循圖所示：

    ![][5]

### <a name="create-an-event-hub"></a>建立事件中心

1. 請注意該 hello 事件中心必須位於 hello 相同 Azure 訂用帳戶 hello 您剛才建立的 Azure 資料湖存放區。 建立 hello 事件中心按一下 hello**上**按鈕底下**擷取**在 hello**建立事件中樞**入口網站的刀鋒視窗。 
2. 在 hello**建立事件中樞**入口刀鋒視窗中，選取**Azure Data Lake Store**從 hello**擷取提供者**方塊。
3. 在**選取 Data Lake Store**，指定 hello Data Lake Store 帳戶的密碼之前，而且 hello**資料湖路徑**欄位中，輸入您所建立的 hello 路徑 toohello 資料資料夾。

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a>在現有的事件中樞上新增或設定擷取功能

您可以在位於事件中樞命名空間的現有事件中樞上設定擷取功能。 tooenable 擷取現有的事件中心或 toochange 上擷取設定，請按一下 hello 命名空間 tooload hello **Essentials**刀鋒視窗中，然後按一下您想 tooenable 或變更 hello 擷取設定 hello 事件中心。 最後，按一下 hello**屬性**hello 區段開啟刀鋒視窗並再編輯 hello 擷取設定，hello 下列圖表所示：

### <a name="azure-blob-storage"></a>Azure Blob 儲存體

![][2]

### <a name="azure-data-lake-store"></a>Azure Data Lake Store

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a>後續步驟

您也可以透過 Azure Resource Manager 範本來設定事件中樞擷取。 如需詳細資訊，請參閱[使用 Azure Resource Manager 範本啟用擷取功能](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)。
