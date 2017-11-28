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
# <a name="how-toodeploy-an-azure-api-management-service-instance-toomultiple-azure-regions"></a><span data-ttu-id="4469e-103">如何 toodeploy Azure API 管理服務執行個體 toomultiple Azure 區域</span><span class="sxs-lookup"><span data-stu-id="4469e-103">How toodeploy an Azure API Management service instance toomultiple Azure regions</span></span>
<span data-ttu-id="4469e-104">API 管理支援多重地區部署可讓任何數目的所需的 Azure 區域之間的 API 發行者 toodistribute 單一的 API 管理服務。</span><span class="sxs-lookup"><span data-stu-id="4469e-104">API Management supports multi-region deployment which enables API publishers toodistribute a single API management service across any number of desired Azure regions.</span></span> <span data-ttu-id="4469e-105">這有助於降低地理上分散的 API 取用者感受到的要求延遲，並且可以改善某個區域離線時服務的可用性。</span><span class="sxs-lookup"><span data-stu-id="4469e-105">This helps reduce request latency perceived by geographically distributed API consumers and also improves service availability if one region goes offline.</span></span> 

<span data-ttu-id="4469e-106">一開始建立 API 管理服務時，它只包含[單元][ unit]和位於單一 Azure 區域，其指定為 hello 主要區域中。</span><span class="sxs-lookup"><span data-stu-id="4469e-106">When an API Management service is created initially, it contains only one [unit][unit] and resides in a single Azure region, which is designated as hello Primary Region.</span></span> <span data-ttu-id="4469e-107">透過 hello Azure 入口網站，可以輕鬆地加入其他地區。</span><span class="sxs-lookup"><span data-stu-id="4469e-107">Additional regions can be easily added through hello Azure Portal.</span></span> <span data-ttu-id="4469e-108">API 管理閘道伺服器是部署的 tooeach 區域，並呼叫流量將路由的 toohello 最接近的閘道。</span><span class="sxs-lookup"><span data-stu-id="4469e-108">An API Management gateway server is deployed tooeach region and call traffic will be routed toohello closest gateway.</span></span> <span data-ttu-id="4469e-109">如果離線的區域，已自動重新導向的 toohello 下一個最接近閘道 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="4469e-109">If a region goes offline, hello traffic is automatically re-directed toohello next closest gateway.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="4469e-110">多區域部署僅供以 hello  **[Premium] [ Premium]** 層。</span><span class="sxs-lookup"><span data-stu-id="4469e-110">Multi-region deployment is only available in hello **[Premium][Premium]** tier.</span></span>
> 
> 

## <span data-ttu-id="4469e-111"><a name="add-region"></a>部署 API 管理服務執行個體 tooa 新區域</span><span class="sxs-lookup"><span data-stu-id="4469e-111"><a name="add-region"> </a>Deploy an API Management service instance tooa new region</span></span>
> [!NOTE]
> <span data-ttu-id="4469e-112">如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[開始使用 Azure API 管理][Get started with Azure API Management]教學課程。</span><span class="sxs-lookup"><span data-stu-id="4469e-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="4469e-113">在 hello Azure 入口網站瀏覽 toohello**小數位數和定價**您 API 管理服務執行個體的頁面。</span><span class="sxs-lookup"><span data-stu-id="4469e-113">In hello Azure Portal navigate toohello **Scale and pricing** page for your API Management service instance.</span></span> 

![調整索引標籤][api-management-scale-service]

<span data-ttu-id="4469e-115">toodeploy tooa 新區域，請按一下  **+ 新增區域**從 hello 工具列。</span><span class="sxs-lookup"><span data-stu-id="4469e-115">toodeploy tooa new region, click on **+ Add region** from hello toolbar.</span></span>

![加入區域][api-management-add-region]

<span data-ttu-id="4469e-117">從 [hello] 下拉式清單選取 hello 位置並設定 hello 與 hello 滑桿的單位數目。</span><span class="sxs-lookup"><span data-stu-id="4469e-117">Select hello location from hello drop-down list and set hello number of units for with hello slider.</span></span>

![指定單位][api-management-select-location-units]

<span data-ttu-id="4469e-119">按一下**新增**tooplace hello 位置資料表中的選取範圍。</span><span class="sxs-lookup"><span data-stu-id="4469e-119">Click **Add** tooplace your selection in hello Locations table.</span></span> 

<span data-ttu-id="4469e-120">重複此程序，直到您設定的所有位置，然後按一下**儲存**從 hello 工具列 toostart hello 部署程序。</span><span class="sxs-lookup"><span data-stu-id="4469e-120">Repeat this process until you have all locations configured and click **Save** from hello toolbar toostart hello deployment process.</span></span>

## <span data-ttu-id="4469e-121"><a name="remove-region"> </a>從區域中刪除 API 管理服務執行個體</span><span class="sxs-lookup"><span data-stu-id="4469e-121"><a name="remove-region"> </a>Delete an API Management service instance from a location</span></span>
<span data-ttu-id="4469e-122">在 hello Azure 入口網站瀏覽 toohello**小數位數和定價**您 API 管理服務執行個體的頁面。</span><span class="sxs-lookup"><span data-stu-id="4469e-122">In hello Azure Portal navigate toohello **Scale and pricing** page for your API Management service instance.</span></span> 

![調整索引標籤][api-management-scale-service]

<span data-ttu-id="4469e-124">針對您想要的 hello 位置 tooremove 開啟 hello 內容功能表使用 hello **...** hello 右端的 hello 資料表 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4469e-124">For hello location you would like tooremove open hello context menu using hello **...** button at hello right end of hello table.</span></span> <span data-ttu-id="4469e-125">選取 hello**刪除**選項。</span><span class="sxs-lookup"><span data-stu-id="4469e-125">Select hello **Delete** option.</span></span>

![移除區域][api-management-remove-region]

<span data-ttu-id="4469e-127">確認 hello 刪除，然後按一下**儲存**tooapply hello 變更。</span><span class="sxs-lookup"><span data-stu-id="4469e-127">Confirm hello deletion and click **Save** tooapply hello changes.</span></span>

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

