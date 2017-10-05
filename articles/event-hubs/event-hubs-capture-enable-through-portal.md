---
title: "透過入口網站啟用 Azure 事件中樞擷取功能 | Microsoft Docs"
description: "使用 Azure 入口網站啟用事件中樞擷取功能。"
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
ms.openlocfilehash: 0cbf45dce922647f2996f929d2c7cf885a2f4db4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="enable-event-hubs-capture-using-the-azure-portal"></a>使用 Azure 入口網站啟用事件中樞擷取功能

您可以使用 [Azure 入口網站](https://portal.azure.com)，在建立事件中樞時設定擷取功能。 您可以將資料擷取至 Azure [Blob 儲存體](https://azure.microsoft.com/services/storage/blobs/)容器或 [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) 帳戶。

## <a name="capture-data-to-an-azure-storage-account"></a>將資料擷取至 Azure 儲存體帳戶  

當您建立事件中樞時，您可以按一下來啟用擷取**上**按鈕**建立事件中樞**入口網站的刀鋒視窗。 然後按一下 [擷取提供者] 方塊中的 [Azure 儲存體]，以指定儲存體帳戶和容器。 事件中樞擷取會對儲存體使用服務對服務驗證，因此您不需要指定儲存體連接字串。 資源選擇器會自動選取儲存體帳戶的資源 URI。 如果您使用 Azure Resource Manager，您必須以字串形式明確提供此 URI。

預設時間範圍為 5 分鐘。 最小值是 1，最大值是 15。 **大小** 範圍為 10-500 MB。

![][1]

## <a name="capture-data-to-an-azure-data-lake-store-account"></a>將資料擷取至 Azure Data Lake Store 帳戶

若要將資料擷取至 Azure Data Lake Store，請建立 Data Lake Store 帳戶及事件中樞：

### <a name="create-an-azure-data-lake-store-account-and-folders"></a>建立 Azure Data Lake Store 帳戶和資料夾

1. 遵循[使用 Azure 入口網站開始使用 Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md) 中的指示，建立 Data Lake Store 帳戶。 
2. 遵循[在 Azure Data Lake Store 帳戶中建立資料夾](../data-lake-store/data-lake-store-get-started-portal.md#createfolder)一節中的指示，在此帳戶下建立資料夾。
3. 在 [Data Lake Store 帳戶] 刀鋒視窗中，按一下**資料總管**。
4. 按一下 [存取]。
5. 按一下 [新增] 。
6. 在 [依姓名或電子郵件搜尋] 方塊中輸入 **Microsoft.EventHubs**，然後選取此選項。 
7. [權限] 索引標籤隨即出現。 設定權限，如下圖所示：

    ![][6]

8. 按一下 [確定] 。
9. 現在，瀏覽至目標資料夾，然後按一下資料夾名稱，以在根資料夾中建立資料夾。
10. 按一下 [存取]。
11. 按一下 [新增] 。
12. 在 [依姓名或電子郵件搜尋] 方塊中輸入 **Microsoft.EventHubs**，然後選取此選項。
13. [權限] 索引標籤再次出現。 設定權限，如下圖所示：

    ![][5]

### <a name="create-an-event-hub"></a>建立事件中心

1. 請注意，事件中樞必須位於與您剛建立之 Azure Data Lake Store 相同的 Azure 訂用帳戶中。 建立事件中樞中，按一下**上**按鈕底下**擷取**中**建立事件中樞**入口網站的刀鋒視窗。 
2. 在**建立事件中樞**入口刀鋒視窗中，選取**Azure Data Lake Store**從**擷取提供者**方塊。
3. 在 [選取 Data Lake Store] 中，指定您先前建立的 Data Lake Store 帳戶，以及在 [Data Lake 路徑] 欄位中，輸入您建立之資料資料夾的路徑。

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a>在現有的事件中樞上新增或設定擷取功能

您可以在位於事件中樞命名空間的現有事件中樞上設定擷取功能。 若要在現有事件中樞上啟用擷取功能，或變更您的擷取設定，請按一下命名空間以載入 [基本資訊] 刀鋒視窗，然後按一下您要啟用或變更擷取設定的事件中樞。 最後，按一下 **屬性**開啟刀鋒視窗的區段，然後編輯擷取設定下, 圖所示：

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
