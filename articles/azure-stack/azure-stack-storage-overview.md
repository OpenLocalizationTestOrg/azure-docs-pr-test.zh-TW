---
title: "aaaIntroduction tooAzure 堆疊儲存體"
description: "了解 Azure Stack 儲存體"
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 092aba28-04bc-44c0-90e1-e79d82f4ff42
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/19/2017
ms.author: xiaofmao
ms.openlocfilehash: 8e156584dafb8b084bfc69b9dbe7cbaa78717135
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-stack-storage"></a>簡介 tooAzure 堆疊儲存體

## <a name="overview"></a>概觀
Azure Stack 儲存體是一組雲端儲存體服務，包括與 Azure 儲存體服務一致的 Blob、資料表和佇列。

## <a name="azure-stack-storage-services"></a>Azure Stack 儲存體服務
Azure 堆疊儲存體提供下列三項服務的 hello:

* **Blob 儲存體** 

    Blob 儲存體可儲存非結構化物件資料。 Blob 可以是任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。
* **資料表儲存體** 

    資料表儲存體可儲存結構化的資料集。 資料表儲存體是 NoSQL 索引鍵屬性的資料存放區，可快速開發和快速存取 toolarge 數量的資料。
* **佇列儲存體** 

    佇列儲存體針對工作流程處理及雲端服務元件間的通訊，提供可靠的訊息服務。

堆疊 Azure 儲存體帳戶是安全的帳戶，可讓您存取 tooservices Azure 堆疊儲存體中。 儲存體帳戶提供儲存體資源 hello 唯一命名空間。 hello 下列圖表顯示 hello 之間關聯性 hello 堆疊 Azure 儲存體資源中的儲存體帳戶：

![Azure Stack 儲存體概觀](media/azure-stack-storage-overview/AzureStackStorageOverview.png)


### <a name="blob-storage"></a>Blob 儲存體

Blob 儲存體具有大量非結構化的物件資料 toostore hello 雲端中的使用者，提供有效率且可調整的解決方案。 您可以使用 Blob 儲存體 toostore 內容，例如：

* 文件
* 社交資料 (例如照片、視訊、音樂和部落格)
* 檔案、電腦、資料庫和裝置的備份
* Web 應用程式的影像和文字
* 雲端應用程式的組態資料
* 巨量資料 (例如記錄和其他大型資料集)

每個 Blob 會組織成一個容器。 容器也會提供實用的方式 tooassign 安全性原則 toogroups 的物件。 儲存體帳戶可以包含任何數目的容器，以及容器可以包含任何數目的 blob，向上 toohello 限制的儲存體帳戶。

Blob 儲存體提供三種類型的 Blob： 
* **區塊 Blob** 

    區塊 Blob 已針對串流和儲存雲端物件進行最佳化，是儲存文件、媒體檔案、備份等的不錯選擇。
* **附加 Blob** 

    附加 blob 類似 tooblock blob，但適合用於附加作業。 附加 blob 可以只是藉由加入新的區塊 toohello 結尾更新。 附加 blob 是不錯的選擇，例如記錄、 需要新的資料寫入只 toohello 結尾 hello blob toobe 案例。
* **分頁 Blob** 

    分頁 blob 適用於代表 IaaS 磁碟，並支援隨機寫入這是總 too1 TB 的大小。 Azure Stack 虛擬機器連結的 IaaS 磁碟是以分頁 Blob 方式儲存的 VHD。


### <a name="table-storage"></a>表格儲存體
新式應用程式通常會要求以超越前幾代軟體需求的延伸性和彈性儲存資料。 資料表儲存體提供高可用性、 可大幅擴充的儲存體，讓您的應用程式可以自動調整 toomeet 使用者需求。 表格儲存體屬於 Microsoft 的 NoSQL 索引鍵屬性儲存，它的無結構描述設計讓它有別於傳統的關聯式資料庫。 Schemaless 資料存放區中，很容易 tooadapt 資料做為 hello 需要的應用程式 evolve。 資料表儲存體是簡單 toouse，因此開發人員可以快速建立應用程式。

表格儲存體屬於索引鍵屬性儲存，代表資料表中的每個值會與具型別的屬性名稱一起儲存。 hello 屬性名稱可以用於篩選和指定選取準則。 一組屬性及其值就構成一個實體。 由於 schemaless 資料表儲存體，在兩個實體 hello 相同資料表可以包含不同集合的屬性，而這些屬性可以屬於不同的類型。

您可以使用資料表儲存體 toostore 彈性的資料集，例如 web 應用程式、 通訊錄，裝置資訊和任何其他類型的中繼資料服務所需的使用者資料。 現今的以網際網路為基礎的應用程式對於類似資料表儲存體的 NoSQL 資料庫會提供常用的替代 tootraditional 關聯式資料庫。

儲存體帳戶可以包含任何數量的資料表，以及資料表可以包含任意數目的實體，向上 toohello hello 儲存體帳戶的容量限制。

### <a name="queue-storage"></a>佇列儲存體
設計擴充性的應用程式時，會經常分離應用程式元件，以便進行個別擴充。 佇列儲存體提供可靠的傳訊解決方案的應用程式元件之間的非同步通訊，不論它們是在 hello 雲端中，hello 桌面、 內部部署伺服器，或行動裝置。 佇列儲存體也支援管理非同步工作並建置處理工作流程。

儲存體帳戶可以包含任何數目的佇列，並佇列可以包含任意數目的訊息，向上 toohello hello 儲存體帳戶的容量限制。 個別訊息可能是 up too64 KB 的大小。

## <a name="next-steps"></a>後續步驟
* [與 Azure 一致的儲存體：差異與注意事項](azure-stack-acs-differences.md)

* toolearn 進一步了解 Azure 儲存體，請參閱[簡介 tooMicrosoft Azure 儲存體](../storage/common/storage-introduction.md)

