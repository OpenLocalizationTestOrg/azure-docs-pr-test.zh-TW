---
title: "B2B 整合帳戶-Azure 邏輯應用程式的 aaaDisaster 復原 |Microsoft 文件"
description: "Logic Apps B2B 災害復原"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e86564a3c5a2607d22514936c606e2843cba0416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a><span data-ttu-id="686f5-103">Logic Apps B2B 跨區域災害復原</span><span class="sxs-lookup"><span data-stu-id="686f5-103">Logic Apps B2B cross-region disaster recovery</span></span>

<span data-ttu-id="686f5-104">B2B 工作負載涉及金錢交易，例如訂單和發票。</span><span class="sxs-lookup"><span data-stu-id="686f5-104">B2B workloads involve money transactions like orders and invoices.</span></span> <span data-ttu-id="686f5-105">在發生損壞事件，它是關鍵商業層級 Sla 達成了協議與交易夥伴商務 tooquickly 復原 toomeet hello 項目。</span><span class="sxs-lookup"><span data-stu-id="686f5-105">During a disaster event, it's critical for a business tooquickly recover toomeet hello business-level SLAs agreed upon with their partners.</span></span> <span data-ttu-id="686f5-106">本文示範如何 toobuild 業務持續性計劃 B2B 工作負載。</span><span class="sxs-lookup"><span data-stu-id="686f5-106">This article demonstrates how toobuild a business continuity plan for B2B workloads.</span></span> 

* <span data-ttu-id="686f5-107">災害復原整備</span><span class="sxs-lookup"><span data-stu-id="686f5-107">Disaster Recovery readiness</span></span> 
* <span data-ttu-id="686f5-108">在嚴重損壞事件期間容錯移轉 toosecondary 區域</span><span class="sxs-lookup"><span data-stu-id="686f5-108">Fail over toosecondary region during a disaster event</span></span> 
* <span data-ttu-id="686f5-109">切換回 tooprimary 區域之後發生損壞事件</span><span class="sxs-lookup"><span data-stu-id="686f5-109">Fall back tooprimary region after a disaster event</span></span>

## <a name="disaster-recovery-readiness"></a><span data-ttu-id="686f5-110">災害復原整備</span><span class="sxs-lookup"><span data-stu-id="686f5-110">Disaster Recovery readiness</span></span>  

1. <span data-ttu-id="686f5-111">指出次要區域並建立[整合帳戶](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md)hello 次要區域中。</span><span class="sxs-lookup"><span data-stu-id="686f5-111">Identify a secondary region and create an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) in hello secondary region.</span></span>

2. <span data-ttu-id="686f5-112">新增夥伴、 結構描述和合約的執行狀態的 hello 中需要複寫 toobe toosecondary 區域整合帳戶所需的 hello 訊息流程。</span><span class="sxs-lookup"><span data-stu-id="686f5-112">Add partners, schemas, and agreements for hello required message flows where hello run status needs toobe replicated toosecondary region integration account.</span></span>

   > [!TIP]
   > <span data-ttu-id="686f5-113">請確定沒有一致性 hello 整合帳戶成品的命名慣例在跨區域。</span><span class="sxs-lookup"><span data-stu-id="686f5-113">Make sure there's consistency in hello integration account artifact's naming convention across regions.</span></span> 

3. <span data-ttu-id="686f5-114">hello 主要區域中，從執行狀態的 toopull hello hello 次要區域中建立邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="686f5-114">toopull hello run status from hello primary region, create a logic app in hello secondary region.</span></span> 

   <span data-ttu-id="686f5-115">這個邏輯應用程式應該有觸發程序和動作。</span><span class="sxs-lookup"><span data-stu-id="686f5-115">This logic app should have a *trigger* and an *action*.</span></span> 
   <span data-ttu-id="686f5-116">hello 觸發程序應該連接 tooprimary 區域整合帳戶，並 hello 動作應該 toosecondary 區域整合帳戶連接。</span><span class="sxs-lookup"><span data-stu-id="686f5-116">hello trigger should connect tooprimary region integration account, and hello action should connect toosecondary region integration account.</span></span> 
   <span data-ttu-id="686f5-117">根據 hello 時間間隔，hello 觸發程序輪詢 hello 主要區域執行狀態資料表，並且會提取 hello 新的記錄，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="686f5-117">Based on hello time interval, hello trigger polls hello primary region run status table and pulls hello new records, if any.</span></span> <span data-ttu-id="686f5-118">hello 動作來更新這些 toosecondary 區域整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="686f5-118">hello action updates them toosecondary region integration account.</span></span> 
   <span data-ttu-id="686f5-119">這是從主要區域 toosecondary 區域有助於 tooget 累加式的執行階段狀態。</span><span class="sxs-lookup"><span data-stu-id="686f5-119">This helps tooget incremental runtime status from primary region toosecondary region.</span></span>

4. <span data-ttu-id="686f5-120">業務續航力 Logic Apps 整合帳戶被設計 toosupport B2B 通訊協定-X12、 AS2 和 EDIFACT 為基礎。</span><span class="sxs-lookup"><span data-stu-id="686f5-120">Business continuity in Logic Apps integration account is designed toosupport based on B2B protocols - X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="686f5-121">toofind 詳細步驟，選取 hello 各自的連結。</span><span class="sxs-lookup"><span data-stu-id="686f5-121">toofind detailed steps, select hello respective links.</span></span>

5. <span data-ttu-id="686f5-122">hello 建議太 toodeploy 次要區域中的所有主要區域資源。</span><span class="sxs-lookup"><span data-stu-id="686f5-122">hello recommendation is toodeploy all primary region resources in a secondary region too.</span></span> 

   <span data-ttu-id="686f5-123">主要區域的資源包括 Azure SQL Database 或 Azure Cosmos DB、 Azure 服務匯流排和 Azure 事件中心用於訊息、 Azure API 管理，以及 Azure App Service 中的 hello Azure 邏輯應用程式功能。</span><span class="sxs-lookup"><span data-stu-id="686f5-123">Primary region resources include Azure SQL Database or Azure Cosmos DB, Azure Service Bus and Azure Event Hubs used for messaging, Azure API Management, and hello Azure Logic Apps feature in Azure App Service.</span></span>   

6. <span data-ttu-id="686f5-124">從建立連線的主要區域 tooa 次要區域。</span><span class="sxs-lookup"><span data-stu-id="686f5-124">Establish a connection from a primary region tooa secondary region.</span></span> <span data-ttu-id="686f5-125">主要區域中，從執行狀態的 toopull hello 次要區域中建立邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="686f5-125">toopull hello run status from a primary region, create a logic app in a secondary region.</span></span> 

   <span data-ttu-id="686f5-126">hello 邏輯應用程式應該有觸發程序和動作。</span><span class="sxs-lookup"><span data-stu-id="686f5-126">hello logic app should have a trigger and an action.</span></span> 
   <span data-ttu-id="686f5-127">hello 觸發程序應該連接 tooa 主要區域整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="686f5-127">hello trigger should connect tooa primary region integration account.</span></span> 
   <span data-ttu-id="686f5-128">hello 動作應該連接 tooa 次要區域整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="686f5-128">hello action should connect tooa secondary region integration account.</span></span> 
   <span data-ttu-id="686f5-129">根據 hello 時間間隔，hello 觸發程序輪詢 hello 主要區域執行狀態資料表，並且會提取 hello 新的記錄，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="686f5-129">Based on hello time interval, hello trigger polls hello primary region run status table and pulls hello new records, if any.</span></span> 
   <span data-ttu-id="686f5-130">hello 動作來更新這些 tooa 次要區域整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="686f5-130">hello action updates them tooa secondary region integration account.</span></span> 
   <span data-ttu-id="686f5-131">此程序有助於 tooget 累加式的執行階段狀態從 hello 主要區域 toohello 次要區域。</span><span class="sxs-lookup"><span data-stu-id="686f5-131">This process helps tooget incremental runtime status from hello primary region toohello secondary region.</span></span>

<span data-ttu-id="686f5-132">業務續航力 Logic Apps 整合帳戶提供根據 hello B2B 通訊協定 X12、 AS2 和 EDIFACT 的支援。</span><span class="sxs-lookup"><span data-stu-id="686f5-132">Business continuity in a Logic Apps integration account provides support based on hello B2B protocols X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="686f5-133">如需使用 X12 和 AS2 的詳細步驟，請參閱本文中的 [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) 和 [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2)。</span><span class="sxs-lookup"><span data-stu-id="686f5-133">For detailed steps on using X12 and AS2, see [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) and [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) in this article.</span></span>

## <a name="fail-over-tooa-secondary-region-during-a-disaster-event"></a><span data-ttu-id="686f5-134">在嚴重損壞事件期間容錯移轉 tooa 次要區域</span><span class="sxs-lookup"><span data-stu-id="686f5-134">Fail over tooa secondary region during a disaster event</span></span>

<span data-ttu-id="686f5-135">Hello 主要地區未提供商務持續性資料流導向 toohello 次要區域在嚴重損壞事件。</span><span class="sxs-lookup"><span data-stu-id="686f5-135">During a disaster event, when hello primary region is not available for business continuity, direct traffic toohello secondary region.</span></span> <span data-ttu-id="686f5-136">次要區域可讓您商務 toorecover 函數快速 toomeet hello RPO/RTO 同意其夥伴。</span><span class="sxs-lookup"><span data-stu-id="686f5-136">A secondary region helps a business toorecover functions quickly toomeet hello RPO/RTO agreed upon by their partners.</span></span> <span data-ttu-id="686f5-137">它也會盡可能降低努力 toofail 透過從一個區域 tooanother 區域。</span><span class="sxs-lookup"><span data-stu-id="686f5-137">It also minimizes efforts toofail over from one region tooanother region.</span></span> 

<span data-ttu-id="686f5-138">同時複製的主要區域 tooa 次要區域中的控制編號沒有預期的延遲。</span><span class="sxs-lookup"><span data-stu-id="686f5-138">There is an expected latency while copying control numbers from a primary region tooa secondary region.</span></span> <span data-ttu-id="686f5-139">tooavoid 傳送產生的重複控制編號 toopartners 災害事件期間，hello 建議使用將 tooincrement hello 控制編號會在 hello 次要區域協議[PowerShell cmdlet](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery)。</span><span class="sxs-lookup"><span data-stu-id="686f5-139">tooavoid sending duplicate generated control numbers toopartners during a disaster event, hello recommendation is tooincrement hello control numbers in hello secondary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>

## <a name="fall-back-tooa-primary-region-post-disaster-event"></a><span data-ttu-id="686f5-140">切換回 tooa 主要區域後發生損壞事件</span><span class="sxs-lookup"><span data-stu-id="686f5-140">Fall back tooa primary region post-disaster event</span></span>

<span data-ttu-id="686f5-141">toofall 後 tooa 主要區域時，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="686f5-141">toofall back tooa primary region when it is available, follow these steps:</span></span>

1. <span data-ttu-id="686f5-142">停止接受來自夥伴 hello 次要區域中的訊息。</span><span class="sxs-lookup"><span data-stu-id="686f5-142">Stop accepting messages from partners in hello secondary region.</span></span>  

2. <span data-ttu-id="686f5-143">使用遞增 hello 主要區域的所有合約的 hello 產生控制編號[PowerShell cmdlet](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery)。</span><span class="sxs-lookup"><span data-stu-id="686f5-143">Increment hello generated control numbers for all hello primary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>  

3. <span data-ttu-id="686f5-144">直接從 hello 次要區域 toohello 主要區域的流量。</span><span class="sxs-lookup"><span data-stu-id="686f5-144">Direct traffic from hello secondary region toohello primary region.</span></span>

4. <span data-ttu-id="686f5-145">檢查建立 hello 提取從 hello 主要區域執行狀態的次要區域中的 hello 邏輯應用程式已啟用。</span><span class="sxs-lookup"><span data-stu-id="686f5-145">Check that hello logic app created in hello secondary region for pulling run status from hello primary region is enabled.</span></span>

## <a name="x12"></a><span data-ttu-id="686f5-146">X12</span><span class="sxs-lookup"><span data-stu-id="686f5-146">X12</span></span> 

<span data-ttu-id="686f5-147">EDI X12 文件的商務持續性是根據控制編號：</span><span class="sxs-lookup"><span data-stu-id="686f5-147">Business continuity for EDI X12 documents is based on control numbers:</span></span>

> [!TIP]
> <span data-ttu-id="686f5-148">您也可以使用 hello [X12 快速啟動範本](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/)toocreate 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="686f5-148">You can also use hello [X12 quick start template](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate logic apps.</span></span> <span data-ttu-id="686f5-149">建立主要和次要整合帳戶就是先決條件 toouse hello 範本。</span><span class="sxs-lookup"><span data-stu-id="686f5-149">Creating primary and secondary integration accounts are prerequisites toouse hello template.</span></span> <span data-ttu-id="686f5-150">hello 範本可協助 toocreate 兩個邏輯應用程式，一個用於接收的控制編號，另一個用於產生的控制編號。</span><span class="sxs-lookup"><span data-stu-id="686f5-150">hello template helps toocreate two logic apps, one for received control numbers and another for generated control numbers.</span></span> <span data-ttu-id="686f5-151">Hello logic apps 連接 hello 觸發程序 toohello 主要整合帳戶與 hello 動作 toohello 次要整合帳戶中建立個別的觸發程序和動作。</span><span class="sxs-lookup"><span data-stu-id="686f5-151">Respective triggers and actions are created in hello logic apps, connecting hello trigger toohello primary integration account and hello action toohello secondary integration account.</span></span>

<span data-ttu-id="686f5-152">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="686f5-152">**Prerequisites**</span></span>

<span data-ttu-id="686f5-153">對於輸入訊息，tooenable 嚴重損壞修復 hello X12 協議的接收設定中，選取 hello 重複檢查設定。</span><span class="sxs-lookup"><span data-stu-id="686f5-153">tooenable disaster recovery for inbound messages, select hello duplicate check settings in hello X12 agreement's Receive Settings.</span></span>

![選取重複檢查設定](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. <span data-ttu-id="686f5-155">在次要地區中建立[邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="686f5-155">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="686f5-156">搜尋 **X12**，並選取 [X12 - 當控制編號修改時]。</span><span class="sxs-lookup"><span data-stu-id="686f5-156">Search on **X12**, and select **X12 - When a control number is modified**.</span></span>   

   ![搜尋 x12](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   <span data-ttu-id="686f5-158">hello 觸發程序會提示您 tooestablish 連線 tooan 整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="686f5-158">hello trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="686f5-159">hello 觸發程序應該連接 tooa 主要區域整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="686f5-159">hello trigger should be connected tooa primary region integration account.</span></span>

3. <span data-ttu-id="686f5-160">輸入連線名稱，選取您*主要區域整合帳戶*從 hello 清單，並選擇**建立**。</span><span class="sxs-lookup"><span data-stu-id="686f5-160">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>   

   ![主要區域整合帳戶名稱](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. <span data-ttu-id="686f5-162">hello **DateTime toostart 控制編號同步**設定是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="686f5-162">hello **DateTime toostart control number sync** setting is optional.</span></span> <span data-ttu-id="686f5-163">hello**頻率**可以設定得**天**，**小時**，**分鐘**，或**第二個**間隔。</span><span class="sxs-lookup"><span data-stu-id="686f5-163">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![日期時間和頻率](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. <span data-ttu-id="686f5-165">選取 [新增步驟] > [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="686f5-165">Select **New step** > **Add an action**.</span></span>

   ![選取 [新增步驟]，然後選取 [新增動作]](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. <span data-ttu-id="686f5-167">搜尋 **X12**，並選取 [X12 - 新增或更新控制編號]。</span><span class="sxs-lookup"><span data-stu-id="686f5-167">Search on **X12**, and select **X12 - Add or update control numbers**.</span></span>   

   ![新增或更新控制編號](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. <span data-ttu-id="686f5-169">選取 tooconnect 動作 tooa 次要區域整合帳戶，**變更連接** > **加入新的連接**hello 取得整合帳戶的清單。</span><span class="sxs-lookup"><span data-stu-id="686f5-169">tooconnect an action tooa secondary region integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="686f5-170">輸入連線名稱，選取您*次要區域整合帳戶*從 hello 清單，並選擇**建立**。</span><span class="sxs-lookup"><span data-stu-id="686f5-170">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span> 

   ![次要地區整合帳戶名稱](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. <span data-ttu-id="686f5-172">切換 tooraw 輸入 hello 右上角的圖示即可。</span><span class="sxs-lookup"><span data-stu-id="686f5-172">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![切換 tooraw 輸入](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. <span data-ttu-id="686f5-174">從 hello 動態內容選擇器中，選取主體，並儲存 hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="686f5-174">Select Body from hello dynamic content picker, and save hello logic app.</span></span>

   ![動態內容欄位](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   <span data-ttu-id="686f5-176">根據 hello 時間間隔，hello 觸發程序會輪詢 hello 收到的主要區域控制編號的資料表，並會提取 hello 新記錄。</span><span class="sxs-lookup"><span data-stu-id="686f5-176">Based on hello time interval, hello trigger polls hello primary region received control number table and pulls hello new records.</span></span> 
   <span data-ttu-id="686f5-177">hello 動作來更新 hello 次要區域整合帳戶中的 hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="686f5-177">hello action updates hello records in hello secondary region integration account.</span></span> 
   <span data-ttu-id="686f5-178">如果有任何更新，hello 觸發程序狀態會顯示為**已略過**。</span><span class="sxs-lookup"><span data-stu-id="686f5-178">If there are no updates, hello trigger status appears as **Skipped**.</span></span>   

   ![控制編號資料表](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="686f5-180">根據 hello 時間間隔，hello 累加式的執行階段狀態將會從複寫的主要區域 tooa 次要區域。</span><span class="sxs-lookup"><span data-stu-id="686f5-180">Based on hello time interval, hello incremental runtime status replicates from a primary region tooa secondary region.</span></span> <span data-ttu-id="686f5-181">在 hello 主要區域無法時可用的直接流量 toohello 次要區域的業務持續性的嚴重損壞事件。</span><span class="sxs-lookup"><span data-stu-id="686f5-181">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="edifact"></a><span data-ttu-id="686f5-182">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="686f5-182">EDIFACT</span></span> 

<span data-ttu-id="686f5-183">EDI EDIFACT 文件的商務持續性是根據控制編號。</span><span class="sxs-lookup"><span data-stu-id="686f5-183">Business continuity for EDI EDIFACT documents is based on control numbers.</span></span>

<span data-ttu-id="686f5-184">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="686f5-184">**Prerequisites**</span></span>

<span data-ttu-id="686f5-185">tooenable 災害復原，對於輸入訊息，會選取 EDIFACT 協議的接收設定中的 hello 重複檢查設定。</span><span class="sxs-lookup"><span data-stu-id="686f5-185">tooenable disaster recovery for inbound messages, select hello duplicate check settings in your EDIFACT agreement's Receive Settings.</span></span>

![選取重複檢查設定](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. <span data-ttu-id="686f5-187">在次要地區中建立[邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="686f5-187">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="686f5-188">搜尋 **EDIFACT**，並選取 [EDIFACT - 當控制編號修改時]。</span><span class="sxs-lookup"><span data-stu-id="686f5-188">Search on **EDIFACT**, and select **EDIFACT - When a control number is modified**.</span></span>

   ![搜尋 EDIFACT](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   <span data-ttu-id="686f5-190">hello 觸發程序會提示您 tooestablish 連線 tooan 整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="686f5-190">hello trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="686f5-191">hello 觸發程序應該連接 tooa 主要區域整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="686f5-191">hello trigger should be connected tooa primary region integration account.</span></span> 

3. <span data-ttu-id="686f5-192">輸入連線名稱，選取您*主要區域整合帳戶*從 hello 清單，並選擇**建立**。</span><span class="sxs-lookup"><span data-stu-id="686f5-192">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>    

   ![主要區域整合帳戶名稱](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. <span data-ttu-id="686f5-194">hello **DateTime toostart 控制編號同步**設定是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="686f5-194">hello **DateTime toostart control number sync** setting is optional.</span></span> <span data-ttu-id="686f5-195">hello**頻率**可以設定得**天**，**小時**，**分鐘**，或**第二個**間隔。</span><span class="sxs-lookup"><span data-stu-id="686f5-195">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>    

   ![日期時間和頻率](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. <span data-ttu-id="686f5-197">選取 [新增步驟] > [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="686f5-197">Select **New step** > **Add an action**.</span></span>    

   ![選取 [新增步驟]，然後選取 [新增動作]](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. <span data-ttu-id="686f5-199">搜尋 **EDIFACT**，並選取 [EDIFACT - 新增或更新控制編號]。</span><span class="sxs-lookup"><span data-stu-id="686f5-199">Search on **EDIFACT**, and select **EDIFACT - Add or update control numbers**.</span></span>   

   ![新增或更新控制編號](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. <span data-ttu-id="686f5-201">選取 tooconnect 動作 tooa 次要區域整合帳戶，**變更連接** > **加入新的連接**hello 取得整合帳戶的清單。</span><span class="sxs-lookup"><span data-stu-id="686f5-201">tooconnect an action tooa secondary region integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="686f5-202">輸入連線名稱，選取您*次要區域整合帳戶*從 hello 清單，並選擇**建立**。</span><span class="sxs-lookup"><span data-stu-id="686f5-202">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span>

   ![次要地區整合帳戶名稱](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. <span data-ttu-id="686f5-204">切換 tooraw 輸入 hello 右上角的圖示即可。</span><span class="sxs-lookup"><span data-stu-id="686f5-204">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![切換 tooraw 輸入](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. <span data-ttu-id="686f5-206">從 hello 動態內容選擇器中，選取主體，並儲存 hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="686f5-206">Select Body from hello dynamic content picker, and save hello logic app.</span></span>   

   ![動態內容欄位](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   <span data-ttu-id="686f5-208">根據 hello 時間間隔，hello 觸發程序會輪詢 hello 收到的主要區域控制編號的資料表，並會提取 hello 新記錄。</span><span class="sxs-lookup"><span data-stu-id="686f5-208">Based on hello time interval, hello trigger polls hello primary region received control number table and pulls hello new records.</span></span>
   <span data-ttu-id="686f5-209">hello 動作來更新 hello 記錄 toohello 次要區域整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="686f5-209">hello action updates hello records toohello secondary region integration account.</span></span> 
   <span data-ttu-id="686f5-210">如果有任何更新，hello 觸發程序狀態會顯示為**已略過**。</span><span class="sxs-lookup"><span data-stu-id="686f5-210">If there are no updates, hello trigger status appears as **Skipped**.</span></span>

   ![控制編號資料表](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="686f5-212">根據 hello 時間間隔，hello 累加式的執行階段狀態將會從複寫的主要區域 tooa 次要區域。</span><span class="sxs-lookup"><span data-stu-id="686f5-212">Based on hello time interval, hello incremental runtime status replicates from a primary region tooa secondary region.</span></span> <span data-ttu-id="686f5-213">在 hello 主要區域無法時可用的直接流量 toohello 次要區域的業務持續性的嚴重損壞事件。</span><span class="sxs-lookup"><span data-stu-id="686f5-213">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="as2"></a><span data-ttu-id="686f5-214">AS2</span><span class="sxs-lookup"><span data-stu-id="686f5-214">AS2</span></span> 

<span data-ttu-id="686f5-215">業務持續性，使用 hello AS2 通訊協定的文件以 hello 訊息識別碼及 hello MIC 值。</span><span class="sxs-lookup"><span data-stu-id="686f5-215">Business continuity for documents that use hello AS2 protocol is based on hello message ID and hello MIC value.</span></span>

> [!TIP]
> <span data-ttu-id="686f5-216">您也可以使用 hello [AS2 快速入門範本](https://github.com/Azure/azure-quickstart-templates/pull/3302)toocreate 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="686f5-216">You can also use hello [AS2 quick start template](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate logic apps.</span></span> <span data-ttu-id="686f5-217">建立主要和次要整合帳戶就是先決條件 toouse hello 範本。</span><span class="sxs-lookup"><span data-stu-id="686f5-217">Creating primary and secondary integration accounts are prerequisites toouse hello template.</span></span> <span data-ttu-id="686f5-218">hello 範本可協助建立觸發程序和動作之邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="686f5-218">hello template helps create a logic app that has a trigger and an action.</span></span> <span data-ttu-id="686f5-219">hello 邏輯應用程式會從觸發程序 tooa 主要整合帳戶和動作 tooa 次要整合帳戶建立連接。</span><span class="sxs-lookup"><span data-stu-id="686f5-219">hello logic app creates a connection from a trigger tooa primary integration account and an action tooa secondary integration account.</span></span>

1. <span data-ttu-id="686f5-220">建立[邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)hello 次要區域中。</span><span class="sxs-lookup"><span data-stu-id="686f5-220">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in hello secondary region.</span></span>  

2. <span data-ttu-id="686f5-221">搜尋 **AS2**，並選取 [AS2 - 建立 MIC 值時]。</span><span class="sxs-lookup"><span data-stu-id="686f5-221">Search on **AS2**, and select **AS2 - When a MIC value is created**.</span></span>   

   ![搜尋 AS2](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   <span data-ttu-id="686f5-223">觸發程序會提示您 tooestablish 連線 tooan 整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="686f5-223">A trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="686f5-224">hello 觸發程序應該連接 tooa 主要區域整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="686f5-224">hello trigger should be connected tooa primary region integration account.</span></span> 
   
3. <span data-ttu-id="686f5-225">輸入連線名稱，選取您*主要區域整合帳戶*從 hello 清單，並選擇**建立**。</span><span class="sxs-lookup"><span data-stu-id="686f5-225">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>

   ![主要區域整合帳戶名稱](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. <span data-ttu-id="686f5-227">hello **DateTime toostart MIC 值同步**設定是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="686f5-227">hello **DateTime toostart MIC value sync** setting is optional.</span></span> <span data-ttu-id="686f5-228">hello**頻率**可以設定得**天**，**小時**，**分鐘**，或**第二個**間隔。</span><span class="sxs-lookup"><span data-stu-id="686f5-228">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![日期時間和頻率](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. <span data-ttu-id="686f5-230">選取 [新增步驟] > [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="686f5-230">Select **New step** > **Add an action**.</span></span>  

   ![選取 [新增步驟]，然後選取 [新增動作]](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. <span data-ttu-id="686f5-232">搜尋 **AS2**，並選取 [AS2 - 新增或更新 MIC 內容]。</span><span class="sxs-lookup"><span data-stu-id="686f5-232">Search on **AS2**, and select **AS2 - Add or update MIC contents**.</span></span>  

   ![MIC 新增或更新](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. <span data-ttu-id="686f5-234">tooconnect 動作 tooa 次要整合帳戶 中，選取**變更連接** > **加入新的連接**hello 取得整合帳戶的清單。</span><span class="sxs-lookup"><span data-stu-id="686f5-234">tooconnect an action tooa secondary integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="686f5-235">輸入連線名稱，選取您*次要區域整合帳戶*從 hello 清單，並選擇**建立**。</span><span class="sxs-lookup"><span data-stu-id="686f5-235">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span>

   ![次要地區整合帳戶名稱](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. <span data-ttu-id="686f5-237">切換 tooraw 輸入 hello 右上角的圖示即可。</span><span class="sxs-lookup"><span data-stu-id="686f5-237">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![切換 tooraw 輸入](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. <span data-ttu-id="686f5-239">從 hello 動態內容選擇器中，選取主體，並儲存 hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="686f5-239">Select Body from hello dynamic content picker, and save hello logic app.</span></span>   

   ![動態內容](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   <span data-ttu-id="686f5-241">根據 hello 時間間隔，hello 觸發程序會輪詢 hello 主要區域 」 資料表，並會提取 hello 新記錄。</span><span class="sxs-lookup"><span data-stu-id="686f5-241">Based on hello time interval, hello trigger polls hello primary region table and pulls hello new records.</span></span> <span data-ttu-id="686f5-242">hello 動作來更新這些 toohello 次要區域整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="686f5-242">hello action updates them toohello secondary region integration account.</span></span> 
   <span data-ttu-id="686f5-243">如果有任何更新，hello 觸發程序狀態會顯示為**已略過**。</span><span class="sxs-lookup"><span data-stu-id="686f5-243">If there are no updates, hello trigger status appears as **Skipped**.</span></span>  

   ![主要區域資料表](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

<span data-ttu-id="686f5-245">根據 hello 時間間隔，hello 累加式的執行階段狀態將會從複寫 hello 主要區域 toohello 次要區域。</span><span class="sxs-lookup"><span data-stu-id="686f5-245">Based on hello time interval, hello incremental runtime status replicates from hello primary region toohello secondary region.</span></span> <span data-ttu-id="686f5-246">在 hello 主要區域無法時可用的直接流量 toohello 次要區域的業務持續性的嚴重損壞事件。</span><span class="sxs-lookup"><span data-stu-id="686f5-246">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="686f5-247">後續步驟</span><span class="sxs-lookup"><span data-stu-id="686f5-247">Next steps</span></span>

[<span data-ttu-id="686f5-248">監視 B2B 訊息</span><span class="sxs-lookup"><span data-stu-id="686f5-248">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md)

