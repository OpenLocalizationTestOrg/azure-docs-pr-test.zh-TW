---
title: "aaaDeploy Azure API 管理服務 toomultiple Azure 區域 |Microsoft 文件"
description: "了解如何 toodeploy Azure API 管理服務執行個體 toomultiple Azure 區域。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 47389ad6-f865-4706-833f-846115e22e4d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 04a3e762261237d73a769320a21363f99f1d20cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-an-azure-api-management-service-instance-toomultiple-azure-regions"></a>如何 toodeploy Azure API 管理服務執行個體 toomultiple Azure 區域
API 管理支援多重地區部署可讓任何數目的所需的 Azure 區域之間的 API 發行者 toodistribute 單一的 API 管理服務。 這有助於降低地理上分散的 API 取用者感受到的要求延遲，並且可以改善某個區域離線時服務的可用性。 

一開始建立 API 管理服務時，它只包含[單元][ unit]和位於單一 Azure 區域，其指定為 hello 主要區域中。 透過 hello Azure 入口網站，可以輕鬆地加入其他地區。 API 管理閘道伺服器是部署的 tooeach 區域，並呼叫流量將路由的 toohello 最接近的閘道。 如果離線的區域，已自動重新導向的 toohello 下一個最接近閘道 hello 流量。 

> [!IMPORTANT]
> 多區域部署僅供以 hello  **[Premium] [ Premium]** 層。
> 
> 

## <a name="add-region"></a>部署 API 管理服務執行個體 tooa 新區域
> [!NOTE]
> 如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[開始使用 Azure API 管理][Get started with Azure API Management]教學課程。
> 
> 

在 hello Azure 入口網站瀏覽 toohello**小數位數和定價**您 API 管理服務執行個體的頁面。 

![調整索引標籤][api-management-scale-service]

toodeploy tooa 新區域，請按一下  **+ 新增區域**從 hello 工具列。

![加入區域][api-management-add-region]

從 [hello] 下拉式清單選取 hello 位置並設定 hello 與 hello 滑桿的單位數目。

![指定單位][api-management-select-location-units]

按一下**新增**tooplace hello 位置資料表中的選取範圍。 

重複此程序，直到您設定的所有位置，然後按一下**儲存**從 hello 工具列 toostart hello 部署程序。

## <a name="remove-region"> </a>從區域中刪除 API 管理服務執行個體
在 hello Azure 入口網站瀏覽 toohello**小數位數和定價**您 API 管理服務執行個體的頁面。 

![調整索引標籤][api-management-scale-service]

針對您想要的 hello 位置 tooremove 開啟 hello 內容功能表使用 hello **...** hello 右端的 hello 資料表 按鈕。 選取 hello**刪除**選項。

![移除區域][api-management-remove-region]

確認 hello 刪除，然後按一下**儲存**tooapply hello 變更。

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance tooa new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

