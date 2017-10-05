---
title: "Azure CDN 即時警示 | Microsoft Docs"
description: "Microsoft Azure CDN 中的即時警示。 即時警示可針對 CDN 設定檔中端點的效能提供通知。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 1e85b809-e1a9-4473-b835-69d1b4ed3393
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6e66eb076ac7220823a848b5047f147d4101cd55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a><span data-ttu-id="20ff7-104">Microsoft Azure CDN 中的即時警示</span><span class="sxs-lookup"><span data-stu-id="20ff7-104">Real-time alerts in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="20ff7-105">Overview</span><span class="sxs-lookup"><span data-stu-id="20ff7-105">Overview</span></span>
<span data-ttu-id="20ff7-106">本文件說明 Microsoft Azure CDN 中的即時警示。</span><span class="sxs-lookup"><span data-stu-id="20ff7-106">This document explains real-time alerts in Microsoft Azure CDN.</span></span> <span data-ttu-id="20ff7-107">這項功能可針對 CDN 設定檔中端點的效能提供即時通知。</span><span class="sxs-lookup"><span data-stu-id="20ff7-107">This functionality provides real-time notifications about the performance of the endpoints in your CDN profile.</span></span>  <span data-ttu-id="20ff7-108">您可以根據以下狀況設定電子郵件或 HTTP 警示︰</span><span class="sxs-lookup"><span data-stu-id="20ff7-108">You can set up email or HTTP alerts based on:</span></span>

* <span data-ttu-id="20ff7-109">頻寬</span><span class="sxs-lookup"><span data-stu-id="20ff7-109">Bandwidth</span></span>
* <span data-ttu-id="20ff7-110">狀態碼</span><span class="sxs-lookup"><span data-stu-id="20ff7-110">Status Codes</span></span>
* <span data-ttu-id="20ff7-111">快取狀態</span><span class="sxs-lookup"><span data-stu-id="20ff7-111">Cache Statuses</span></span>
* <span data-ttu-id="20ff7-112">連線</span><span class="sxs-lookup"><span data-stu-id="20ff7-112">Connections</span></span>

## <a name="creating-a-real-time-alert"></a><span data-ttu-id="20ff7-113">建立即時警示</span><span class="sxs-lookup"><span data-stu-id="20ff7-113">Creating a real-time alert</span></span>
1. <span data-ttu-id="20ff7-114">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽到您的 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="20ff7-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span></span>
   
    ![CDN 設定檔刀鋒視窗](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. <span data-ttu-id="20ff7-116">在 [CDN 設定檔] 刀鋒視窗中，按一下 [管理]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="20ff7-116">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    <span data-ttu-id="20ff7-118">隨即開啟 CDN 管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="20ff7-118">The CDN management portal opens.</span></span>
3. <span data-ttu-id="20ff7-119">將滑鼠移至 [分析] 索引標籤上，然後將滑鼠移至 [即時統計資料] 飛出視窗上。</span><span class="sxs-lookup"><span data-stu-id="20ff7-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="20ff7-120">按一下 [即時警示] 。</span><span class="sxs-lookup"><span data-stu-id="20ff7-120">Click on **Real-Time Alerts**.</span></span>
   
    ![CDN 管理入口網站](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    <span data-ttu-id="20ff7-122">隨即會顯示現有警示組態 (如果有的話) 的清單。</span><span class="sxs-lookup"><span data-stu-id="20ff7-122">The list of existing alert configurations (if any) is displayed.</span></span>
4. <span data-ttu-id="20ff7-123">按一下 [新增警示]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="20ff7-123">Click the **Add Alert** button.</span></span>
   
    ![新增警示按鈕](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    <span data-ttu-id="20ff7-125">隨即會顯示可供建立新警示的表單。</span><span class="sxs-lookup"><span data-stu-id="20ff7-125">A form for creating a new alert is displayed.</span></span>
   
    ![新增警示表單](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. <span data-ttu-id="20ff7-127">如果您想要在按一下 [儲存] 時讓此警示啟用，請核取 [已啟用警示] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="20ff7-127">If you want this alert to be active when you click **Save**, check the **Alert Enabled** checkbox.</span></span>
6. <span data-ttu-id="20ff7-128">在 [名稱]  欄位中輸入用來描述警示的名稱。</span><span class="sxs-lookup"><span data-stu-id="20ff7-128">Enter a descriptive name for your alert in the **Name** field.</span></span>
7. <span data-ttu-id="20ff7-129">在 [媒體類型] 下拉式清單中，選取 [HTTP 大型物件]。</span><span class="sxs-lookup"><span data-stu-id="20ff7-129">In the **Media Type** dropdown, select **HTTP Large Object**.</span></span>
   
    ![選取了 HTTP 大型物件的媒體類型](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="20ff7-131">您必須選取 [HTTP 大型物件] 做為 [媒體類型]。</span><span class="sxs-lookup"><span data-stu-id="20ff7-131">You must select **HTTP Large Object** as the **Media Type**.</span></span>  <span data-ttu-id="20ff7-132">**來自 Verizon 的 Azure CDN** 不會使用其他選項。</span><span class="sxs-lookup"><span data-stu-id="20ff7-132">The other choices are not used by **Azure CDN from Verizon**.</span></span>  <span data-ttu-id="20ff7-133">若未能選取 [HTTP 大型物件]，將導致警示永不觸發。</span><span class="sxs-lookup"><span data-stu-id="20ff7-133">Failure to select **HTTP Large Object** will cause your alert to never be triggered.</span></span>
   > 
   > 
8. <span data-ttu-id="20ff7-134">選取 [度量]、[運算子] 和 [觸發值]，來建立要監視的 [運算式]。</span><span class="sxs-lookup"><span data-stu-id="20ff7-134">Create an **Expression** to monitor by selecting a **Metric**, **Operator**, and **Trigger value**.</span></span>
   
   * <span data-ttu-id="20ff7-135">針對 [度量] ，請選取您要監視的狀況類型。</span><span class="sxs-lookup"><span data-stu-id="20ff7-135">For **Metric**, select the type of condition you want monitored.</span></span>  <span data-ttu-id="20ff7-136"> 是頻寬使用量，單位是每秒 Mb 數。</span><span class="sxs-lookup"><span data-stu-id="20ff7-136">**Bandwidth Mbps** is the amount of bandwidth usage in megabits per second.</span></span>  <span data-ttu-id="20ff7-137"> 是連往 Edge Server 的並行 HTTP 連線數目。</span><span class="sxs-lookup"><span data-stu-id="20ff7-137">**Total Connections** is the number of concurrent HTTP connections to our edge servers.</span></span>  <span data-ttu-id="20ff7-138">如需各種快取狀態和狀態碼的定義，請參閱 [Azure CDN 快取狀態碼](https://msdn.microsoft.com/library/mt759237.aspx)和 [Azure CDN HTTP 狀態碼](https://msdn.microsoft.com/library/mt759238.aspx)</span><span class="sxs-lookup"><span data-stu-id="20ff7-138">For definitions of the various cache statuses and status codes, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) and [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)</span></span>
   * <span data-ttu-id="20ff7-139"> 是可在度量和觸發值之間建立關聯性的數學運算子。</span><span class="sxs-lookup"><span data-stu-id="20ff7-139">**Operator** is the mathematical operator that establishes the relationship between the metric and the trigger value.</span></span>
   * <span data-ttu-id="20ff7-140">**Trigger Value** 是在傳送通知之前必須先符合的臨界值。</span><span class="sxs-lookup"><span data-stu-id="20ff7-140">**Trigger Value** is the threshold value that must be met before a notification will be sent out.</span></span>
     
     <span data-ttu-id="20ff7-141">在下面的範例中，我所建立的運算式表示我想要在 404 狀態碼數目大於 25 時收到通知。</span><span class="sxs-lookup"><span data-stu-id="20ff7-141">In the below example, the expression I have created indicates that I would like to be notified when the number of 404 status codes is greater than 25.</span></span>
     
     ![即時警示的範例運算式](./media/cdn-real-time-alerts/cdn-expression.png)
9. <span data-ttu-id="20ff7-143">在 [間隔] 中，輸入您想要評估運算式的頻率。</span><span class="sxs-lookup"><span data-stu-id="20ff7-143">For **Interval**, enter how frequently you would like the expression evaluated.</span></span>
10. <span data-ttu-id="20ff7-144">在 [通知時機]  下拉式清單中，選取當運算式評估為 true 時，您想要在何時收到通知。</span><span class="sxs-lookup"><span data-stu-id="20ff7-144">In the **Notify on** dropdown, select when you would like to be notified when the expression is true.</span></span>
    
    * <span data-ttu-id="20ff7-145"> 表示會在第一次偵測到指定狀況時傳送通知。</span><span class="sxs-lookup"><span data-stu-id="20ff7-145">**Condition Start** indicates that a notification will be sent when the specified condition is first detected.</span></span>
    * <span data-ttu-id="20ff7-146"> 表示會於未再偵測到指定狀況時傳送通知。</span><span class="sxs-lookup"><span data-stu-id="20ff7-146">**Condition End** indicates that a notification will be sent when the specified condition is no longer detected.</span></span> <span data-ttu-id="20ff7-147">只有在網路監視系統已偵測到發生指定狀況後，才會觸發此通知。</span><span class="sxs-lookup"><span data-stu-id="20ff7-147">This notification can only be triggered after our network monitoring system detected that the specified condition occurred.</span></span>
    * <span data-ttu-id="20ff7-148"> 表示會在網路監視系統每一次偵測到指定狀況時傳送通知。</span><span class="sxs-lookup"><span data-stu-id="20ff7-148">**Continuous** indicates that a notification will be sent each time that the network monitoring system detects the specified condition.</span></span> <span data-ttu-id="20ff7-149">請記住，在每一次的間隔中，網路監視系統只會檢查一次是否發生指定狀況。</span><span class="sxs-lookup"><span data-stu-id="20ff7-149">Keep in mind that the network monitoring system will only check once per interval for the specified condition.</span></span>
    * <span data-ttu-id="20ff7-150"> 表示會在第一次偵測到指定狀況時傳送通知，並於未再偵測到該狀況時再次傳送通知。</span><span class="sxs-lookup"><span data-stu-id="20ff7-150">**Condition Start and End** indicates that a notification will be sent the first time that the specified condition is detected and once again when the condition is no longer detected.</span></span>
11. <span data-ttu-id="20ff7-151">如果您想要透過電子郵件接收通知，請核取 [透過電子郵件通知]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="20ff7-151">If you want to receive notifications by email, check the **Notify by Email** checkbox.</span></span>  
    
    ![透過電子郵件通知表單](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    <span data-ttu-id="20ff7-153">在 [收件者]  欄位中，輸入您想要讓通知傳送到的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="20ff7-153">In the **To** field, enter the email address you where you want notifications sent.</span></span> <span data-ttu-id="20ff7-154">在 [主旨] 和 [內文] 中，您可以保留預設值，或者使用 [可用關鍵字] 清單來自訂訊息，以在傳送訊息時動態插入警示資料。</span><span class="sxs-lookup"><span data-stu-id="20ff7-154">For **Subject** and **Body**, you may leave the default, or you may customize the message using the **Available keywords** list to dynamically insert alert data when the message is sent.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="20ff7-155">您可以按一下 [測試通知] 按鈕來測試電子郵件通知，但僅限在儲存警示組態之後進行。</span><span class="sxs-lookup"><span data-stu-id="20ff7-155">You can test the email notification by clicking the **Test Notification** button, but only after the alert configuration has been saved.</span></span>
    > 
    > 
12. <span data-ttu-id="20ff7-156">如果您想要讓通知張貼到 Web 伺服器，請核取 [透過 HTTP Post 通知]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="20ff7-156">If you want notifications to be posted to a web server, check the **Notify by HTTP Post** checkbox.</span></span>
    
    ![透過 HTTP Post 通知表單](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    <span data-ttu-id="20ff7-158">在 [Url]  欄位中，輸入您想要用來張貼 HTTP 訊息的 URL。</span><span class="sxs-lookup"><span data-stu-id="20ff7-158">In the **Url** field, enter the URL you where you want the HTTP message posted.</span></span> <span data-ttu-id="20ff7-159">在 [標頭]  文字方塊中，輸入要在要求中傳送的 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="20ff7-159">In the **Headers** textbox, enter the HTTP headers to be sent in the request.</span></span>  <span data-ttu-id="20ff7-160">在 [內文] 中，您可以使用 [可用關鍵字] 清單來自訂訊息，以在傳送訊息時動態插入警示資料。</span><span class="sxs-lookup"><span data-stu-id="20ff7-160">For **Body** you may customize the message using the **Available keywords** list to dynamically insert alert data when the message is sent.</span></span>  <span data-ttu-id="20ff7-161">[標頭] 和 [內文] 會預設為 XML 承載，情形類似下面的範例。</span><span class="sxs-lookup"><span data-stu-id="20ff7-161">**Headers** and **Body** default to an XML payload similar to the below example.</span></span>
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > <span data-ttu-id="20ff7-162">您可以按一下 [測試通知] 按鈕來測試 HTTP Post 通知，但僅限在儲存警示組態之後進行。</span><span class="sxs-lookup"><span data-stu-id="20ff7-162">You can test the HTTP Post notification by clicking the **Test Notification** button, but only after the alert configuration has been saved.</span></span>
    > 
    > 
13. <span data-ttu-id="20ff7-163">按一下 [儲存]  按鈕以儲存您的警示組態。</span><span class="sxs-lookup"><span data-stu-id="20ff7-163">Click the **Save** button to save your alert configuration.</span></span>  <span data-ttu-id="20ff7-164">如果您在步驟 5 中核取了 [已啟用警示]  ，您的警示現在便已啟用。</span><span class="sxs-lookup"><span data-stu-id="20ff7-164">If you checked **Alert Enabled** in step 5, your alert is now active.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20ff7-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="20ff7-165">Next Steps</span></span>
* <span data-ttu-id="20ff7-166">分析 [Azure CDN 中的即時統計資料](cdn-real-time-stats.md)</span><span class="sxs-lookup"><span data-stu-id="20ff7-166">Analyze [Real-time stats in Azure CDN](cdn-real-time-stats.md)</span></span>
* <span data-ttu-id="20ff7-167">進一步了解 [進階 HTTP 報告](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="20ff7-167">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="20ff7-168">分析 [使用模式](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="20ff7-168">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

