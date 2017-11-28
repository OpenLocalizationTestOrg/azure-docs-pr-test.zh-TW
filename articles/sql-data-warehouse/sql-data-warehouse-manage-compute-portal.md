---
title: "aaaManage 的計算能力，在 Azure SQL 資料倉儲 （Azure 入口網站） |Microsoft 文件"
description: "Azure 入口網站工作 toomanage 運算能力。 透過調整 DWU 以調整計算資源。 或者，您也可以暫停和繼續計算資源 toosave 成本。"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 233b0da5-4abd-4d1d-9586-4ccc5f50b071
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: b2e84b3763e97ce88c190eecfb64b2d06f727229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a><span data-ttu-id="f3e07-105">管理 Azure SQL 資料倉儲中的計算能力 (Azure 入口網站)</span><span class="sxs-lookup"><span data-stu-id="f3e07-105">Manage compute power in Azure SQL Data Warehouse (Azure portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f3e07-106">概觀</span><span class="sxs-lookup"><span data-stu-id="f3e07-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="f3e07-107">入口網站</span><span class="sxs-lookup"><span data-stu-id="f3e07-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="f3e07-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3e07-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="f3e07-109">REST</span><span class="sxs-lookup"><span data-stu-id="f3e07-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="f3e07-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="f3e07-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a><span data-ttu-id="f3e07-111">調整計算能力</span><span class="sxs-lookup"><span data-stu-id="f3e07-111">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="f3e07-112">toochange 計算資源：</span><span class="sxs-lookup"><span data-stu-id="f3e07-112">toochange compute resources:</span></span>

1. <span data-ttu-id="f3e07-113">開啟 hello [Azure 入口網站][Azure portal]，開啟您的資料庫，然後按一下**標尺**。</span><span class="sxs-lookup"><span data-stu-id="f3e07-113">Open hello [Azure portal][Azure portal], open your database, and click **Scale**.</span></span>

    ![按一下 [調整]][1]
2. <span data-ttu-id="f3e07-115">在 hello 小數位數 刀鋒視窗中，移動 hello 滑桿向左或向右 toochange hello DWU 設定。</span><span class="sxs-lookup"><span data-stu-id="f3e07-115">In hello Scale blade, move hello slider left or right toochange hello DWU setting.</span></span>

    ![移動滑桿][2]
3. <span data-ttu-id="f3e07-117">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="f3e07-117">Click **Save**.</span></span> <span data-ttu-id="f3e07-118">確認訊息隨即出現。</span><span class="sxs-lookup"><span data-stu-id="f3e07-118">A confirmation message appears.</span></span> <span data-ttu-id="f3e07-119">按一下**是**tooconfirm 或**沒有**toocancel。</span><span class="sxs-lookup"><span data-stu-id="f3e07-119">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![按一下 [Save] \(儲存)。][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="f3e07-121">暫停計算</span><span class="sxs-lookup"><span data-stu-id="f3e07-121">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="f3e07-122">toopause 資料庫：</span><span class="sxs-lookup"><span data-stu-id="f3e07-122">toopause a database:</span></span>

1. <span data-ttu-id="f3e07-123">開啟 hello [Azure 入口網站][ Azure portal]並開啟您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="f3e07-123">Open hello [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="f3e07-124">請注意該狀態的 hello**線上**。</span><span class="sxs-lookup"><span data-stu-id="f3e07-124">Notice that hello Status is **Online**.</span></span>

    ![線上狀態][6]
2. <span data-ttu-id="f3e07-126">按一下 toosuspend 運算和記憶體資源，**暫停**，和就會顯示確認訊息。</span><span class="sxs-lookup"><span data-stu-id="f3e07-126">toosuspend compute and memory resources, click **Pause**, and then a confirmation message appears.</span></span> <span data-ttu-id="f3e07-127">按一下**是**tooconfirm 或**沒有**toocancel。</span><span class="sxs-lookup"><span data-stu-id="f3e07-127">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![確認暫停][7]
3. <span data-ttu-id="f3e07-129">SQL 資料倉儲啟動 hello 資料庫時，hello 狀態即**暫停**。</span><span class="sxs-lookup"><span data-stu-id="f3e07-129">While SQL Data Warehouse is starting hello database, hello status is **Pausing**.</span></span>
4. <span data-ttu-id="f3e07-130">Hello 狀態時**暫停**hello 暫停作業完成，您無法再所負責的 Dwu。</span><span class="sxs-lookup"><span data-stu-id="f3e07-130">When hello status is **Paused**, hello pause operation is done and you are no longer being charged for DWUs.</span></span>

    ![暫停狀態][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="f3e07-132">繼續計算</span><span class="sxs-lookup"><span data-stu-id="f3e07-132">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="f3e07-133">tooresume 資料庫：</span><span class="sxs-lookup"><span data-stu-id="f3e07-133">tooresume a database:</span></span>

1. <span data-ttu-id="f3e07-134">開啟 hello [Azure 入口網站][ Azure portal]並開啟您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="f3e07-134">Open hello [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="f3e07-135">請注意該狀態的 hello**暫停**。</span><span class="sxs-lookup"><span data-stu-id="f3e07-135">Notice that hello Status is **Paused**.</span></span>

    ![暫停資料庫][4]
2. <span data-ttu-id="f3e07-137">tooresume hello 資料庫按一下**啟動**，並就會顯示確認訊息。</span><span class="sxs-lookup"><span data-stu-id="f3e07-137">tooresume hello database click **Start**, and then a confirmation message appears.</span></span> <span data-ttu-id="f3e07-138">按一下**是**tooconfirm 或**沒有**toocancel。</span><span class="sxs-lookup"><span data-stu-id="f3e07-138">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![確認繼續][5]
3. <span data-ttu-id="f3e07-140">SQL 資料倉儲啟動 hello 資料庫時，hello 狀態即 「 繼續 」。</span><span class="sxs-lookup"><span data-stu-id="f3e07-140">While SQL Data Warehouse is starting hello database, hello status is "Resuming".</span></span>
4. <span data-ttu-id="f3e07-141">Hello 狀態時**線上**，hello 資料庫就緒。</span><span class="sxs-lookup"><span data-stu-id="f3e07-141">When hello status is **online**, hello database is ready.</span></span>

    ![線上狀態][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="f3e07-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f3e07-143">Next steps</span></span>
<span data-ttu-id="f3e07-144">如需詳細資訊，請參閱[管理概觀][Management overview]。</span><span class="sxs-lookup"><span data-stu-id="f3e07-144">For more information, see [Management overview][Management overview].</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-manage-compute-portal/click-scale.png
[2]: ./media/sql-data-warehouse-manage-compute-portal/move-slider.png
[3]: ./media/sql-data-warehouse-manage-compute-portal/click-save.png
[4]: ./media/sql-data-warehouse-manage-compute-portal/resume-database.png
[5]: ./media/sql-data-warehouse-manage-compute-portal/resume-confirm.png
[6]: ./media/sql-data-warehouse-manage-compute-portal/pause-database.png
[7]: ./media/sql-data-warehouse-manage-compute-portal/pause-confirm.png

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
