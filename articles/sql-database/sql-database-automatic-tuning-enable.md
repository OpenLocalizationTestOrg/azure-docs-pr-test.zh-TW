---
title: "自動調整的 Azure SQL Database aaaEnable |Microsoft 文件"
description: "您可以輕鬆在 Azure SQL Database 上啟用自動調整。"
services: sql-database
documentationcenter: 
author: vvasic
manager: drasumic
editor: vvasic
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 06/05/2016
ms.author: vvasic
ms.openlocfilehash: af9da161eabc0f8c4cb100c050288f234efb8093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-automatic-tuning"></a><span data-ttu-id="40f68-103">啟用自動微調</span><span class="sxs-lookup"><span data-stu-id="40f68-103">Enable automatic tuning</span></span>

<span data-ttu-id="40f68-104">Azure SQL Database 是一種自動受管理的資料服務，不斷地監視您的查詢並找出您可以執行工作負載效能 tooimprove hello 動作。</span><span class="sxs-lookup"><span data-stu-id="40f68-104">Azure SQL Database is an automatically managed data service that constantly monitors your queries and identifies hello action that you can perform tooimprove performance of your workload.</span></span> <span data-ttu-id="40f68-105">您可以檢閱建議並加以手動套用，或讓 Azure SQL Database 自動套用矯正措施 - 這稱為**模式**。</span><span class="sxs-lookup"><span data-stu-id="40f68-105">You can review recommendations and manually apply them, or let Azure SQL Database automatically apply corrective actions - this is known as **automatic tuning mode**.</span></span> <span data-ttu-id="40f68-106">自動調整，可以在 hello 伺服器或 hello 資料庫層級啟用。</span><span class="sxs-lookup"><span data-stu-id="40f68-106">Automatic tuning can be enabled at hello server or hello database level.</span></span>

## <a name="enable-automatic-tuning-on-server"></a><span data-ttu-id="40f68-107">在伺服器上啟用自動調整</span><span class="sxs-lookup"><span data-stu-id="40f68-107">Enable automatic tuning on server</span></span>

<span data-ttu-id="40f68-108">tooenable 自動調整 Azure SQL Database 伺服器上瀏覽 Azure 入口網站，然後選取 toohello server**自動微調**hello 功能表中。</span><span class="sxs-lookup"><span data-stu-id="40f68-108">tooenable automatic tuning on Azure SQL Database server, navigate toohello server in Azure portal and then select **Automatic tuning** in hello menu.</span></span> <span data-ttu-id="40f68-109">選取 hello tooenable 再選取的自動調整選項**套用**:</span><span class="sxs-lookup"><span data-stu-id="40f68-109">Select hello automatic tuning options you want tooenable and select **Apply**:</span></span>

![伺服器](./media/sql-database-automatic-tuning-enable/server.png)

<span data-ttu-id="40f68-111">自動微調伺服器上的選項會套用的 tooall hello 伺服器上的資料庫。</span><span class="sxs-lookup"><span data-stu-id="40f68-111">Automatic tuning options on server are applied tooall databases on hello server.</span></span> <span data-ttu-id="40f68-112">根據預設，所有資料庫會都繼承其父伺服器中的 hello 設定，但是這可以覆寫並個別指定每個資料庫。</span><span class="sxs-lookup"><span data-stu-id="40f68-112">By default, all databases inherit hello configuration from their parent server, but this can be overridden and specified for each database individually.</span></span>

## <a name="configure-automatic-tuning-on-database"></a><span data-ttu-id="40f68-113">在資料庫上設定自動調整</span><span class="sxs-lookup"><span data-stu-id="40f68-113">Configure automatic tuning on database</span></span>

<span data-ttu-id="40f68-114">hello Azure 入口網站可讓您 tooindividually 每個資料庫上指定 hello 自動調整設定。</span><span class="sxs-lookup"><span data-stu-id="40f68-114">hello Azure portal enables you tooindividually specify hello automatic tuning configuration on each database.</span></span>

> [!NOTE]
> <span data-ttu-id="40f68-115">hello 一般建議是 toomanage hello 自動調整設定伺服器層級是相同的組態設定可以在每個資料庫自動套用的 hello。</span><span class="sxs-lookup"><span data-stu-id="40f68-115">hello general recommendation is toomanage hello automatic tuning configuration at server level so hello same configuration settings can be applied on every database automatically.</span></span> <span data-ttu-id="40f68-116">設定自動調整個別的資料庫上如果 hello 資料庫位於不同的其他人 hello 相同的伺服器。</span><span class="sxs-lookup"><span data-stu-id="40f68-116">Configure automatic tuning on an individual database if hello database is different that others on hello same server.</span></span>
>

<span data-ttu-id="40f68-117">tooenable 自動調整的單一資料庫上，瀏覽 toohello hello Azure 入口網站中的資料庫然後再選取**自動微調**。</span><span class="sxs-lookup"><span data-stu-id="40f68-117">tooenable automatic tuning on a single database, navigate toohello database in hello Azure portal and then and select **Automatic tuning**.</span></span> <span data-ttu-id="40f68-118">您可以設定單一資料庫 tooinherit hello 從 hello 資料庫選取 hello 核取方塊，或您可以個別指定資料庫的 「 hello 」 組態設定。</span><span class="sxs-lookup"><span data-stu-id="40f68-118">You can configure a single database tooinherit hello settings from hello database by selecting hello checkbox or you can specify hello configuration for a database individually.</span></span>

![資料庫](./media/sql-database-automatic-tuning-enable/database.png)

<span data-ttu-id="40f68-120">一旦您選取適當的設定後，按一下 [套用]。</span><span class="sxs-lookup"><span data-stu-id="40f68-120">Once you have selected appropriate configuration, click **Apply**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40f68-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="40f68-121">Next steps</span></span>
* <span data-ttu-id="40f68-122">讀取 hello[自動調整的發行項](sql-database-automatic-tuning.md)toolearn 深入了解自動調整，以及它如何協助您改善您的效能。</span><span class="sxs-lookup"><span data-stu-id="40f68-122">Read hello [Automatic tuning article](sql-database-automatic-tuning.md) toolearn more about automatic tuning and how it can help you improve your performance.</span></span>
* <span data-ttu-id="40f68-123">如需 Azure SQL Database 效能建議的概觀，請參閱[效能建議](sql-database-advisor.md)。</span><span class="sxs-lookup"><span data-stu-id="40f68-123">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="40f68-124">請參閱[查詢效能深入資訊](sql-database-query-performance.md)toolearn 有關檢視 hello 您排名最前面的查詢效能影響。</span><span class="sxs-lookup"><span data-stu-id="40f68-124">See [Query Performance Insights](sql-database-query-performance.md) toolearn about viewing hello performance impact of your top queries.</span></span>
