---
title: "aaaAzure CDN 的即時警示 |Microsoft 文件"
description: "Microsoft Azure CDN 中的即時警示。 即時警示提供有關 hello 效能，您的 CDN 設定檔中的 hello 端點的通知。"
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
ms.openlocfilehash: 269c90437088bbc41bf899a8c02749e8e6f3006c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a><span data-ttu-id="73e17-104">Microsoft Azure CDN 中的即時警示</span><span class="sxs-lookup"><span data-stu-id="73e17-104">Real-time alerts in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="73e17-105">Overview</span><span class="sxs-lookup"><span data-stu-id="73e17-105">Overview</span></span>
<span data-ttu-id="73e17-106">本文件說明 Microsoft Azure CDN 中的即時警示。</span><span class="sxs-lookup"><span data-stu-id="73e17-106">This document explains real-time alerts in Microsoft Azure CDN.</span></span> <span data-ttu-id="73e17-107">這項功能提供您的 CDN 設定檔中的 hello 端點的 hello 效能的即時通知。</span><span class="sxs-lookup"><span data-stu-id="73e17-107">This functionality provides real-time notifications about hello performance of hello endpoints in your CDN profile.</span></span>  <span data-ttu-id="73e17-108">您可以根據以下狀況設定電子郵件或 HTTP 警示︰</span><span class="sxs-lookup"><span data-stu-id="73e17-108">You can set up email or HTTP alerts based on:</span></span>

* <span data-ttu-id="73e17-109">頻寬</span><span class="sxs-lookup"><span data-stu-id="73e17-109">Bandwidth</span></span>
* <span data-ttu-id="73e17-110">狀態碼</span><span class="sxs-lookup"><span data-stu-id="73e17-110">Status Codes</span></span>
* <span data-ttu-id="73e17-111">快取狀態</span><span class="sxs-lookup"><span data-stu-id="73e17-111">Cache Statuses</span></span>
* <span data-ttu-id="73e17-112">連線</span><span class="sxs-lookup"><span data-stu-id="73e17-112">Connections</span></span>

## <a name="creating-a-real-time-alert"></a><span data-ttu-id="73e17-113">建立即時警示</span><span class="sxs-lookup"><span data-stu-id="73e17-113">Creating a real-time alert</span></span>
1. <span data-ttu-id="73e17-114">在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 tooyour 的 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="73e17-114">In hello [Azure Portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>
   
    ![CDN 設定檔刀鋒視窗](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. <span data-ttu-id="73e17-116">從 hello CDN 設定檔刀鋒視窗中，按一下 [hello**管理**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="73e17-116">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    <span data-ttu-id="73e17-118">hello CDN 管理入口網站隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="73e17-118">hello CDN management portal opens.</span></span>
3. <span data-ttu-id="73e17-119">暫留在 hello**分析** 索引標籤，然後暫留在 hello**即時統計資料**彈出式視窗。</span><span class="sxs-lookup"><span data-stu-id="73e17-119">Hover over hello **Analytics** tab, then hover over hello **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="73e17-120">按一下 [即時警示] 。</span><span class="sxs-lookup"><span data-stu-id="73e17-120">Click on **Real-Time Alerts**.</span></span>
   
    ![CDN 管理入口網站](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    <span data-ttu-id="73e17-122">會顯示 hello 清單的現有警示的組態 （如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="73e17-122">hello list of existing alert configurations (if any) is displayed.</span></span>
4. <span data-ttu-id="73e17-123">按一下 hello**新增警示** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="73e17-123">Click hello **Add Alert** button.</span></span>
   
    ![新增警示按鈕](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    <span data-ttu-id="73e17-125">隨即會顯示可供建立新警示的表單。</span><span class="sxs-lookup"><span data-stu-id="73e17-125">A form for creating a new alert is displayed.</span></span>
   
    ![新增警示表單](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. <span data-ttu-id="73e17-127">如果您想要此警示 toobe active 當您按一下**儲存**，檢查 hello**啟用警示**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="73e17-127">If you want this alert toobe active when you click **Save**, check hello **Alert Enabled** checkbox.</span></span>
6. <span data-ttu-id="73e17-128">輸入您的警示的描述性名稱在 hello**名稱**欄位。</span><span class="sxs-lookup"><span data-stu-id="73e17-128">Enter a descriptive name for your alert in hello **Name** field.</span></span>
7. <span data-ttu-id="73e17-129">在 hello**媒體類型**下拉式清單中，選取**HTTP 大型物件**。</span><span class="sxs-lookup"><span data-stu-id="73e17-129">In hello **Media Type** dropdown, select **HTTP Large Object**.</span></span>
   
    ![選取了 HTTP 大型物件的媒體類型](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="73e17-131">您必須選取**HTTP 大型物件**為 hello**媒體類型**。</span><span class="sxs-lookup"><span data-stu-id="73e17-131">You must select **HTTP Large Object** as hello **Media Type**.</span></span>  <span data-ttu-id="73e17-132">hello 其他選項不會使用**Verizon 從 Azure CDN**。</span><span class="sxs-lookup"><span data-stu-id="73e17-132">hello other choices are not used by **Azure CDN from Verizon**.</span></span>  <span data-ttu-id="73e17-133">失敗 tooselect **HTTP 大型物件**會導致您的警示觸發 toonever。</span><span class="sxs-lookup"><span data-stu-id="73e17-133">Failure tooselect **HTTP Large Object** will cause your alert toonever be triggered.</span></span>
   > 
   > 
8. <span data-ttu-id="73e17-134">建立**運算式**選取 toomonitor**度量**，**運算子**，和**觸發值**。</span><span class="sxs-lookup"><span data-stu-id="73e17-134">Create an **Expression** toomonitor by selecting a **Metric**, **Operator**, and **Trigger value**.</span></span>
   
   * <span data-ttu-id="73e17-135">如**度量**，選取您想要監視的狀況 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="73e17-135">For **Metric**, select hello type of condition you want monitored.</span></span>  <span data-ttu-id="73e17-136">**頻寬 Mbps**是 hello mbps 的頻寬使用量的數量。</span><span class="sxs-lookup"><span data-stu-id="73e17-136">**Bandwidth Mbps** is hello amount of bandwidth usage in megabits per second.</span></span>  <span data-ttu-id="73e17-137">**總連線**是 hello 數字的並行 HTTP 連線 tooour 邊緣伺服器。</span><span class="sxs-lookup"><span data-stu-id="73e17-137">**Total Connections** is hello number of concurrent HTTP connections tooour edge servers.</span></span>  <span data-ttu-id="73e17-138">如需 hello 的定義各種快取狀態和狀態碼，請參閱[Azure CDN 快取狀態碼](https://msdn.microsoft.com/library/mt759237.aspx)和[Azure CDN HTTP 狀態碼](https://msdn.microsoft.com/library/mt759238.aspx)</span><span class="sxs-lookup"><span data-stu-id="73e17-138">For definitions of hello various cache statuses and status codes, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) and [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)</span></span>
   * <span data-ttu-id="73e17-139">**運算子**是 hello 數學運算子，以建立 hello hello 度量和 hello 觸發程序的值之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="73e17-139">**Operator** is hello mathematical operator that establishes hello relationship between hello metric and hello trigger value.</span></span>
   * <span data-ttu-id="73e17-140">**觸發值**通知將送出之前，必須符合的 hello 臨界值。</span><span class="sxs-lookup"><span data-stu-id="73e17-140">**Trigger Value** is hello threshold value that must be met before a notification will be sent out.</span></span>
     
     <span data-ttu-id="73e17-141">在下列範例中的 hello，我已經建立 hello 運算式會表示我希望 toobe hello 404 狀態碼的數目大於 25 時收到通知。</span><span class="sxs-lookup"><span data-stu-id="73e17-141">In hello below example, hello expression I have created indicates that I would like toobe notified when hello number of 404 status codes is greater than 25.</span></span>
     
     ![即時警示的範例運算式](./media/cdn-real-time-alerts/cdn-expression.png)
9. <span data-ttu-id="73e17-143">如**間隔**，輸入您想要評估的 hello 運算式的頻率。</span><span class="sxs-lookup"><span data-stu-id="73e17-143">For **Interval**, enter how frequently you would like hello expression evaluated.</span></span>
10. <span data-ttu-id="73e17-144">在 hello**通知**下拉式清單中，選取您想要 toobe 時收到通知 hello 運算式為 true 時。</span><span class="sxs-lookup"><span data-stu-id="73e17-144">In hello **Notify on** dropdown, select when you would like toobe notified when hello expression is true.</span></span>
    
    * <span data-ttu-id="73e17-145">**條件開始**指出 hello 指定首次偵測到條件時，將收到通知。</span><span class="sxs-lookup"><span data-stu-id="73e17-145">**Condition Start** indicates that a notification will be sent when hello specified condition is first detected.</span></span>
    * <span data-ttu-id="73e17-146">**條件結束**指出 hello 可讓您指定不會再偵測到條件時，將收到通知。</span><span class="sxs-lookup"><span data-stu-id="73e17-146">**Condition End** indicates that a notification will be sent when hello specified condition is no longer detected.</span></span> <span data-ttu-id="73e17-147">網路監視系統偵測到指定的 hello 之後，可以只觸發此通知條件發生。</span><span class="sxs-lookup"><span data-stu-id="73e17-147">This notification can only be triggered after our network monitoring system detected that hello specified condition occurred.</span></span>
    * <span data-ttu-id="73e17-148">**連續**表示通知會傳送 hello 網路監視系統每次偵測到指定的 hello 條件。</span><span class="sxs-lookup"><span data-stu-id="73e17-148">**Continuous** indicates that a notification will be sent each time that hello network monitoring system detects hello specified condition.</span></span> <span data-ttu-id="73e17-149">請記住 hello 網路監視系統將只檢查一次每個間隔 hello 指定條件。</span><span class="sxs-lookup"><span data-stu-id="73e17-149">Keep in mind that hello network monitoring system will only check once per interval for hello specified condition.</span></span>
    * <span data-ttu-id="73e17-150">**條件開始和結束**指出 hello 偵測到 hello 指定的條件的第一次，然後再次 hello 條件不會再偵測到時，將收到通知。</span><span class="sxs-lookup"><span data-stu-id="73e17-150">**Condition Start and End** indicates that a notification will be sent hello first time that hello specified condition is detected and once again when hello condition is no longer detected.</span></span>
11. <span data-ttu-id="73e17-151">如果您想要 tooreceive 通知電子郵件，請檢查 hello**透過電子郵件通知**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="73e17-151">If you want tooreceive notifications by email, check hello **Notify by Email** checkbox.</span></span>  
    
    ![透過電子郵件通知表單](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    <span data-ttu-id="73e17-153">在 hello**至**欄位中，輸入您想通知傳送嗨電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="73e17-153">In hello **To** field, enter hello email address you where you want notifications sent.</span></span> <span data-ttu-id="73e17-154">如**主旨**和**主體**、 您可能會讓 hello 預設值，或您可以自訂 hello 訊息使用 hello**可用關鍵字**清單 toodynamically 插入警示資料時傳送 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="73e17-154">For **Subject** and **Body**, you may leave hello default, or you may customize hello message using hello **Available keywords** list toodynamically insert alert data when hello message is sent.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="73e17-155">您可以測試 hello 電子郵件通知，依序按一下 hello**測試通知**按鈕，但僅限於儲存 hello 警示設定後。</span><span class="sxs-lookup"><span data-stu-id="73e17-155">You can test hello email notification by clicking hello **Test Notification** button, but only after hello alert configuration has been saved.</span></span>
    > 
    > 
12. <span data-ttu-id="73e17-156">如果您想通知 toobe 張貼 tooa web 伺服器，請檢查 hello**通知，透過 HTTP Post**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="73e17-156">If you want notifications toobe posted tooa web server, check hello **Notify by HTTP Post** checkbox.</span></span>
    
    ![透過 HTTP Post 通知表單](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    <span data-ttu-id="73e17-158">在 hello **Url**欄位中，輸入您想讓 hello HTTP 訊息公佈的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="73e17-158">In hello **Url** field, enter hello URL you where you want hello HTTP message posted.</span></span> <span data-ttu-id="73e17-159">在 hello**標頭**文字方塊中，輸入 hello HTTP 標頭 toobe hello 要求中傳送。</span><span class="sxs-lookup"><span data-stu-id="73e17-159">In hello **Headers** textbox, enter hello HTTP headers toobe sent in hello request.</span></span>  <span data-ttu-id="73e17-160">如**主體**您呇簏濻 hello 訊息使用 hello**可用關鍵字**清單 toodynamically 傳送 hello 訊息時，插入警示資料。</span><span class="sxs-lookup"><span data-stu-id="73e17-160">For **Body** you may customize hello message using hello **Available keywords** list toodynamically insert alert data when hello message is sent.</span></span>  <span data-ttu-id="73e17-161">**標頭**和**主體**預設下列範例中的 tooan XML 裝載類似 toohello。</span><span class="sxs-lookup"><span data-stu-id="73e17-161">**Headers** and **Body** default tooan XML payload similar toohello below example.</span></span>
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > <span data-ttu-id="73e17-162">您可以按一下 hello 測試 hello HTTP Post 通知**測試通知**按鈕，但僅限於儲存 hello 警示設定後。</span><span class="sxs-lookup"><span data-stu-id="73e17-162">You can test hello HTTP Post notification by clicking hello **Test Notification** button, but only after hello alert configuration has been saved.</span></span>
    > 
    > 
13. <span data-ttu-id="73e17-163">按一下 hello**儲存**按鈕 toosave 您警示設定。</span><span class="sxs-lookup"><span data-stu-id="73e17-163">Click hello **Save** button toosave your alert configuration.</span></span>  <span data-ttu-id="73e17-164">如果您在步驟 5 中核取了 [已啟用警示]  ，您的警示現在便已啟用。</span><span class="sxs-lookup"><span data-stu-id="73e17-164">If you checked **Alert Enabled** in step 5, your alert is now active.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73e17-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="73e17-165">Next Steps</span></span>
* <span data-ttu-id="73e17-166">分析 [Azure CDN 中的即時統計資料](cdn-real-time-stats.md)</span><span class="sxs-lookup"><span data-stu-id="73e17-166">Analyze [Real-time stats in Azure CDN](cdn-real-time-stats.md)</span></span>
* <span data-ttu-id="73e17-167">進一步了解 [進階 HTTP 報告](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="73e17-167">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="73e17-168">分析 [使用模式](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="73e17-168">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

