---
title: "如何為 SQL 資料倉儲建立支援票證 | Microsoft Docs"
description: "如何在 Azure SQL 資料倉儲中建立支援票證。"
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: a91d1f53-03cb-464b-9d5b-4a9c1a194ed3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 058ff1229acee5d03db7c0305c5565ae95a85758
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-support-ticket-for-sql-data-warehouse"></a><span data-ttu-id="47f2d-103">如何為 SQL 資料倉儲建立支援票證</span><span class="sxs-lookup"><span data-stu-id="47f2d-103">How to create a support ticket for SQL Data Warehouse</span></span>
<span data-ttu-id="47f2d-104">如果您的 SQL 資料倉儲有任何問題，請建立支援票證，以便我們的工程小組協助您。</span><span class="sxs-lookup"><span data-stu-id="47f2d-104">If you are having any issues with your SQL Data Warehouse, please create a support ticket so that our engineering team can assist you.</span></span>

> [!NOTE] 
> <span data-ttu-id="47f2d-105">截至 2016 年 12 月 20 日時，Azure 入口網站中的資源健全狀況檢查並不正確。</span><span class="sxs-lookup"><span data-stu-id="47f2d-105">As of 12/20/2016, the resource health check in the Azure portal is not accurate.</span></span> <span data-ttu-id="47f2d-106">我們正著手解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="47f2d-106">We are actively working to fix this issue.</span></span> 


## <a name="create-a-support-ticket"></a><span data-ttu-id="47f2d-107">建立支援票證</span><span class="sxs-lookup"><span data-stu-id="47f2d-107">Create a support ticket</span></span>
1. <span data-ttu-id="47f2d-108">開啟 [Azure 入口網站][Azure portal]。</span><span class="sxs-lookup"><span data-stu-id="47f2d-108">Open the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="47f2d-109">在 [首頁] 畫面上，按一下 [說明 + 支援]  圖格。</span><span class="sxs-lookup"><span data-stu-id="47f2d-109">On the Home screen, click the **Help + support** tile.</span></span>
   
    ![說明 + 支援](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. <span data-ttu-id="47f2d-111">在 [說明 + 支援] 刀鋒視窗上，按一下 [建立支援要求] 。</span><span class="sxs-lookup"><span data-stu-id="47f2d-111">On the Help + Support blade, click **Create support request**.</span></span>
   
    ![新的支援要求](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. <span data-ttu-id="47f2d-113">選取 [要求類型] 。</span><span class="sxs-lookup"><span data-stu-id="47f2d-113">Select the **Request Type**.</span></span>
   
    ![要求類型](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > <span data-ttu-id="47f2d-115">根據預設，每個 SQL Server (例如 myserver.database.windows.net) 的 **DTU 配額** 為 45,000。</span><span class="sxs-lookup"><span data-stu-id="47f2d-115">By default, each SQL server (e.g. myserver.database.windows.net) has a **DTU Quota** of 45,000.</span></span> <span data-ttu-id="47f2d-116">此配額僅是安全限制。</span><span class="sxs-lookup"><span data-stu-id="47f2d-116">This quota is simply a safety limit.</span></span> <span data-ttu-id="47f2d-117">您可以藉由建立支援票證，並選取 [配額]  做為要求類型來增加配額。</span><span class="sxs-lookup"><span data-stu-id="47f2d-117">You can increase your quota by creating a support ticket and selecting *Quota* as the request type.</span></span> <span data-ttu-id="47f2d-118">若要計算 DTU 需求，將所需的總 [DWU][DWU] 乘以 7.5。</span><span class="sxs-lookup"><span data-stu-id="47f2d-118">To calculate your DTU needs, multiply the 7.5 by the total [DWU][DWU] needed.</span></span> <span data-ttu-id="47f2d-119">例如，如果您想要在一個 SQL Server 上裝載兩個 DW6000，則應該要求 90,000 的 DTU 配額。</span><span class="sxs-lookup"><span data-stu-id="47f2d-119">For example, you would like to host two DW6000s on one SQL server, then you should request a DTU quota of 90,000.</span></span>  <span data-ttu-id="47f2d-120">您可以在入口網站的 [SQL Server] 刀鋒視窗中檢視目前的 DTU 耗用量。</span><span class="sxs-lookup"><span data-stu-id="47f2d-120">You can view your current DTU consumption from the SQL server blade in the portal.</span></span> <span data-ttu-id="47f2d-121">已暫停和未暫停的資料庫都會計入 DTU 配額。</span><span class="sxs-lookup"><span data-stu-id="47f2d-121">Both paused and un-paused databases count toward the DTU quota.</span></span> 
   > 
   > 
5. <span data-ttu-id="47f2d-122">選取主控您回報發生問題之資料庫的 [訂用帳戶]  。</span><span class="sxs-lookup"><span data-stu-id="47f2d-122">Select the **Subscription** that hosts the database with the problem you are reporting.</span></span>
   
    ![訂閱](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. <span data-ttu-id="47f2d-124">選取 [SQL 資料倉儲]  做為資源。</span><span class="sxs-lookup"><span data-stu-id="47f2d-124">Select **SQL Data Warehouse** as the Resource.</span></span>
   
    ![資源](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. <span data-ttu-id="47f2d-126">選取 [Azure 支援計劃][Azure support plan]。</span><span class="sxs-lookup"><span data-stu-id="47f2d-126">Select your [Azure support plan][Azure support plan].</span></span>
   
   * <span data-ttu-id="47f2d-127">**帳單、配額及訂用帳戶管理** 支援。</span><span class="sxs-lookup"><span data-stu-id="47f2d-127">**Billing, quota and subscription management** support is available at all support levels.</span></span>
   * <span data-ttu-id="47f2d-128">**協助修正**支援則透過[開發人員][Developer]、[標準][Standard]、[專業直導][Professional Direct]支援或[頂級][Premier]支援來提供。</span><span class="sxs-lookup"><span data-stu-id="47f2d-128">**Break-fix** support is provided through [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] or [Premier][Premier] support.</span></span> <span data-ttu-id="47f2d-129">客戶在使用 Azure 期間如果遇到可合理認為是 Microsoft 所造成的問題，這類問題即屬於可協助修正的問題。</span><span class="sxs-lookup"><span data-stu-id="47f2d-129">Break-fix issues are problems experienced by customers while using Azure where there is a reasonable expectation that Microsoft caused the problem.</span></span>
   * <span data-ttu-id="47f2d-130">[專業指導][Professional Direct]和[頂級][Premier]支援層級可提供**開發顧問**和**諮詢服務**。</span><span class="sxs-lookup"><span data-stu-id="47f2d-130">**Developer mentoring** and **advisory services** are available at the [Professional Direct][Professional Direct] and [Premier][Premier] support levels.</span></span> 
     
     <span data-ttu-id="47f2d-131">如果您有頂級支援計劃，您也可以在 [Microsoft Premier 線上入口網站][Microsoft Premier online portal]回報 SQL 資料倉儲的相關問題。</span><span class="sxs-lookup"><span data-stu-id="47f2d-131">If you have a Premier support plan, you can also report SQL Data Warehouse related issues on the [Microsoft Premier online portal][Microsoft Premier online portal].</span></span>  <span data-ttu-id="47f2d-132">請參閱 [Azure 支援計畫][Azure support plan]，進一步了解包括範圍、回應時間、價格等各種 Azure 支援計畫。如需有關 Azure 支援的常見問題集，請參閱 [Azure 支援常見問題集][Azure support FAQs]。</span><span class="sxs-lookup"><span data-stu-id="47f2d-132">See [Azure support plans][Azure support plan] to learn more about the various support plans, including scope, response times, pricing, etc.  For frequently asked questions about Azure support, see [Azure support FAQs][Azure support FAQs].</span></span>  
     
     ![支援計劃](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. <span data-ttu-id="47f2d-134">選取**問題類型**和**類別**。</span><span class="sxs-lookup"><span data-stu-id="47f2d-134">Select the **Problem Type** and **Category**.</span></span> <span data-ttu-id="47f2d-135">在此範例中，我們選擇了 [工具] 做為問題類型，選擇 [用戶端工具] 做為類別。</span><span class="sxs-lookup"><span data-stu-id="47f2d-135">In this example, we have chosen "Tools" as the Problem type and "Client tools" as the category.</span></span> 
   
    ![問題類型類別](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. <span data-ttu-id="47f2d-137">描述問題並選擇商業影響層級。</span><span class="sxs-lookup"><span data-stu-id="47f2d-137">Describe the problem and choose the level of business impact.</span></span>
   
    ![問題說明](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. <span data-ttu-id="47f2d-139">將預先填入此支援票證的您的 **連絡資訊** 。</span><span class="sxs-lookup"><span data-stu-id="47f2d-139">Your **contact information** for this support ticket will be pre-filled.</span></span> <span data-ttu-id="47f2d-140">必要時更新此項目。</span><span class="sxs-lookup"><span data-stu-id="47f2d-140">Update this if necessary.</span></span>
    
    ![連絡資訊](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. <span data-ttu-id="47f2d-142">按一下 [建立]  提交支援要求。</span><span class="sxs-lookup"><span data-stu-id="47f2d-142">Click **Create** to submit the support request.</span></span>

## <a name="monitor-a-support-ticket"></a><span data-ttu-id="47f2d-143">監視支援票證</span><span class="sxs-lookup"><span data-stu-id="47f2d-143">Monitor a support ticket</span></span>
<span data-ttu-id="47f2d-144">在您提交支援要求之後，Azure 支援小組會與您連絡。</span><span class="sxs-lookup"><span data-stu-id="47f2d-144">After you have submitted the support request, the Azure support team will contact you.</span></span> <span data-ttu-id="47f2d-145">若要檢查您的要求狀態和詳細資料，請在儀表板上按一下 [管理支援要求]  。</span><span class="sxs-lookup"><span data-stu-id="47f2d-145">To check your request status and details, click **Manage support requests** on the dashboard.</span></span>

![檢查狀態](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a><span data-ttu-id="47f2d-147">其他資源</span><span class="sxs-lookup"><span data-stu-id="47f2d-147">Other Resources</span></span>
<span data-ttu-id="47f2d-148">此外，您可以在 [Stack Overflow][Stack Overflow] 或在 [Azure SQL 資料倉儲 MSDN 論壇][Azure SQL Data Warehouse MSDN forum]上與 SQL 資料倉儲社群聯繫。</span><span class="sxs-lookup"><span data-stu-id="47f2d-148">Additionally, you can connect with the SQL Data Warehouse community on [Stack Overflow][Stack Overflow] or on the [Azure SQL Data Warehouse MSDN forum][Azure SQL Data Warehouse MSDN forum].</span></span>

<!--Image references--> 

<!--Article references--> 
[DWU]: ./sql-data-warehouse-overview-what-is.md

<!--MSDN references--> 

<!--Other web references--> 
[Azure portal]: https://portal.azure.com/
[Azure support plan]: https://azure.microsoft.com/support/plans/?WT.mc_id=Support_Plan_510979/  
[Developer]: https://azure.microsoft.com/support/plans/developer/  
[Standard]: https://azure.microsoft.com/support/plans/standard/  
[Professional Direct]: https://azure.microsoft.com/support/plans/prodirect/  
[Premier]: https://azure.microsoft.com/support/plans/premier/  
[Azure support FAQs]: https://azure.microsoft.com/support/faq/
[Microsoft Premier online portal]: https://premier.microsoft.com/
[Stack Overflow]: https://stackoverflow.com/questions/tagged/azure-sqldw/
[Azure SQL Data Warehouse MSDN forum]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse/

