---
title: "aaaCreate hello 入口網站中，在 Azure 搜尋服務 |Microsoft 文件"
description: "佈建 Azure 搜尋服務 hello 入口網站中。"
services: search
manager: jhubbard
author: HeidiSteen
documentationcenter: 
ms.assetid: c8c88922-69aa-4099-b817-60f7b54e62df
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: f1c7197a1467e32bd4b360b165c9059e6bb0e496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-service-in-hello-portal"></a>在 hello 入口網站中建立 Azure 搜尋服務

本文說明如何 toocreate 或佈建 Azure 搜尋服務 hello 入口網站中。 如需 PowerShell 的指示，請參閱[使用 PowerShell 管理 Azure 搜尋服務](search-manage-powershell.md)。

## <a name="subscribe-free-or-paid"></a>訂閱 (免費或付費)

[開啟免費的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)並使用免費信用額度 tootry 出支付 Azure 服務。 信用額度用完之後，保留 hello 帳戶，並繼續 toouse 免費的 Azure 服務，例如網站。 除非您明確地變更您的設定，並詢問 toobe 收費，永遠不會收取您的信用卡。

或者，請[啟用 MSDN 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。 MSDN 訂用帳戶每月會提供您信用額度，讓您可以用於 Azure 付費服務。 

## <a name="find-azure-search"></a>尋找 Azure 搜尋服務
1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 按一下 hello 加上正負號 （"+"） 中的 hello 左上角。
3. 選取 [Web + 行動] > [Azure 搜尋服務]。

![](./media/search-create-service-portal/find-search2.png)

## <a name="name-hello-service-and-url-endpoint"></a>服務名稱的 hello 和 URL 端點

服務名稱是依據 API 呼叫所發出的 hello URL 端點的一部分。 輸入您的服務名稱在 hello **URL**欄位。 

服務名稱需求：
   * 長度為 2 到 60 個字元
   * 小寫字母、數字或連字號 ("-")
   * 沒有破折號 ("-") 為 hello 前 2 個或最後一個單一字元
   * 不能是連續的破折號 ("-")

## <a name="select-a-subscription"></a>選取一個訂用帳戶
如果您有一個以上的訂用帳戶，請選擇一個同樣具有資料或檔案儲存體服務的訂用帳戶。 Azure 搜尋可以自動偵測 Azure 資料表和 Blob 儲存體、 SQL Database 和 Azure Cosmos DB 透過編製索引*索引子*，但只在 hello 服務相同的訂用帳戶。

## <a name="select-a-resource-group"></a>選取資源群組
資源群組是一起使用之 Azure 服務和資源的集合。 比方說，如果您使用 Azure 搜尋 tooindex SQL 資料庫，則這兩項服務應該 hello 屬於相同的資源群組。

> [!TIP]
> 刪除資源群組時，也會刪除 hello 服務。 利用多個服務，將它們全部放在 hello 原型專案相同的資源群組輕鬆清理之後 hello 專案是透過。 

## <a name="select-a-hosting-location"></a>選取裝載位置 
作為 Azure 服務，可以在 hello 世界各地的資料中心裝載 Azure 搜尋。 請注意，各地理位置的[價格可能不同](https://azure.microsoft.com/pricing/details/search/) 。

## <a name="select-a-pricing-tier-sku"></a>選取定價層 (SKU)
[Azure 搜尋服務目前提供多個定價層](https://azure.microsoft.com/pricing/details/search/)︰免費、基本或標準。 每一層都有自己的[容量和限制](search-limits-quotas-capacity.md)。 請參閱[選擇定價層或 SKU](search-sku-tier.md) 以取得指導方針。

在本逐步解說中，我們選擇 hello 標準層針對我們的服務。

## <a name="create-your-service"></a>建立您的服務

每當您登入記住 toopin 服務 toohello 儀表板，以方便存取。

![](./media/search-create-service-portal/new-service2.png)

## <a name="scale-your-service"></a>調整您的服務
它可能需要幾分鐘的時間 toocreate （15 分鐘或更多視 hello 層） 服務。 佈建您的服務之後，您可以調整它 toomeet 您的需求。 因為您的 Azure 搜尋服務選擇 hello 標準層，您可以在兩個維度來調整您的服務： 複本和資料分割。 您已選擇 hello 基本層，您只能新增複本。 如果您佈建 hello 免費服務，就無法使用小數位數。

***資料分割***讓服務 toostore 和搜尋多個文件。

***複本***允許服務 toohandle 的搜尋查詢更高的負載。

> [!Important]
> 服務必須具有 [2 個唯讀 SLA 的複本和 3 個讀/寫 SLA 的複本](https://azure.microsoft.com/support/legal/sla/search/v1_0/)。

1. 移 tooyour hello Azure 入口網站中的搜尋服務刀鋒視窗。
2. 在 hello 左瀏覽窗格中，選取 **設定** > **標尺**。
3. 使用 hello slidebar tooadd 複本或資料分割。

![](./media/search-create-service-portal/settings-scale.png)

> [!Note] 
> 每個層次都有不同[限制](search-limits-quotas-capacity.md)hello 總數允許在單一服務中的搜尋單位 (複本 * 分割 = 總的搜尋單位)。

## <a name="when-tooadd-a-second-service"></a>當 tooadd 第二個服務

大部分的客戶使用只有一個服務佈建於提供 hello 層[以滑鼠右鍵的資源平衡](search-sku-tier.md)。 一項服務可以裝載多個索引、 主旨 toohello [hello 層您選取的最大限制](search-capacity-planning.md)，與從另一個隔離每個索引。 在 Azure 搜尋中，要求只能是導向的 tooone 索引，從其他意外或故意情況下的資料傳送的 hello 機會降到最低索引 hello 相同服務。

雖然大部分的客戶使用只有一個服務，服務備援可能需要如果操作需求 hello 如下：

+ 災害復原 (資料中心中斷)。 Azure 搜尋不提供立即中斷的 hello 事件中的容錯移轉。 如需建議和指導方針，請參閱[服務管理](search-manage.md)。
+ 將調查多租用戶模型的程式判定額外的服務為 hello 最佳設計。 如需詳細資訊，請參閱[針對多租用戶設計](search-modeling-multitenant-saas-applications.md)。
+ 針對全域部署的應用程式，您可能需要 Azure 搜尋的執行個體的多個區域 toominimize 延遲的應用程式的國際流量。

> [!NOTE]
> 在 Azure 搜尋服務中，您無法區隔索引和查詢工作負載，因此您永遠不會針對區隔的工作負載建立多重服務。 索引一律上查詢 hello 服務處於已建立 （您無法在一個服務中建立索引並將它複製 tooanother）。
>

不需要第二個服務即可獲得高可用性。 使用 2 或多個複本中的 hello 相同的服務時，被達成高可用性的查詢。 複本更新是循序的，這表示當服務更新推出時，至少會有一個複本是可運作的。如需執行時間的詳細資訊，請參閱[服務等級協定](https://azure.microsoft.com/support/legal/sla/search/v1_0/)。

## <a name="next-steps"></a>後續步驟
之後佈建 Azure 搜尋服務，您就可以開始太[定義索引](search-what-is-an-index.md)讓您可以上傳，並搜尋您的資料。

從程式碼或指令碼，tooaccess hello 服務提供 hello URL (*服務名稱*。 search.windows.net) 和金鑰。 系統管理金鑰授與完整存取權；查詢金鑰則授與唯讀存取權。 請參閱[如何 toouse Azure 搜尋.net](search-howto-dotnet-sdk.md) tooget 啟動。

請參閱[建置及查詢您的第一個索引](search-get-started-portal.md)，來取得以入口網站為基礎的快速教學課程。

