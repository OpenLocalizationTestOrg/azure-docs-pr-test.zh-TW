---
title: "新增不在資源庫內的應用程式時遇到問題 | Microsoft Docs"
description: "了解新增不在資源庫內的自訂應用程式時的常見問題"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: bb3fc7877f4e7cafc3904fc67abd87b897874d8a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="problem-adding-a-non-gallery-application"></a><span data-ttu-id="49294-103">新增不在資源庫內的應用程式時遇到問題</span><span class="sxs-lookup"><span data-stu-id="49294-103">Problem adding a non-gallery application</span></span>

<span data-ttu-id="49294-104">本文協助您了解新增**不在資源庫內的自訂應用程式**時的常見問題及如何解決。</span><span class="sxs-lookup"><span data-stu-id="49294-104">This article help you to understand the common problems people face when adding **custom non-gallery applications** and what you can do to resolve them.</span></span> 

## <a name="i-clicked-the-add-button-and-my-application-took-a-long-time-to-appear"></a><span data-ttu-id="49294-105">按一下 [新增] 按鈕，但應用程式經過佷久才出現</span><span class="sxs-lookup"><span data-stu-id="49294-105">I clicked the “add” button and my application took a long time to appear</span></span>

<span data-ttu-id="49294-106">在某些情況下，將應用程式新增至目錄後，可能需要 1-2 分鐘 (有時更久)，應用程式才會出現。</span><span class="sxs-lookup"><span data-stu-id="49294-106">Under some circumstances, it can take 1-2 minutes (and sometimes longer) for an application to appear after adding it to your directory.</span></span> <span data-ttu-id="49294-107">雖然這不是正常預期的表現，您還是可以按一下 [Azure 入口網站](https://portal.azure.com/)右上角的 **通知** 圖示 (鐘)，尋找標示為 **[建立應用程式]** 的 **進行中** 或 **已完成**通知，看到正在新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="49294-107">While this is not the normal expected performance, you can see the application addition is in progress by clicking on the **Notifications** icon (the bell) in the upper right of the [Azure Portal](https://portal.azure.com/) and looking for an **In Progress** or **Completed** notification labeled **Create application**.</span></span>

<span data-ttu-id="49294-108">如果一直都沒有新增的應用程式，或您按一下 **[新增]** 按鈕時發生錯誤，您會看到**錯誤**狀態的**通知**。</span><span class="sxs-lookup"><span data-stu-id="49294-108">If your application is never added, or you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="49294-109">如果您想要取得此錯誤的詳細資訊以進一步了解，或分享給支援工程師，您可以依照[如何查看入口網站通知的詳細資訊](#how-to-see-the-details-of-a-portal-notification)一節的步驟，查看此錯誤的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="49294-109">If you want more details about the error to learn more to or share with a support engingeer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-clicked-the-add-button-and-my-application-didnt-appear"></a><span data-ttu-id="49294-110">我按一下 [新增] 按鈕，但應用程式沒有出現</span><span class="sxs-lookup"><span data-stu-id="49294-110">I clicked the “add” button and my application didn’t appear</span></span>

<span data-ttu-id="49294-111">有時由於暫時性問題、網路問題或錯誤，新增應用程式會失敗。</span><span class="sxs-lookup"><span data-stu-id="49294-111">Sometimes, due to transient issues, networking problems, or a bug, adding an application fail.</span></span> <span data-ttu-id="49294-112">當您按一下 Azure 入口網站右上方的 [通知] 圖示 (鐘)，然後在 [建立應用程式] 通知旁看到紅色 (!) 圖示時，就表示發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="49294-112">You can tell this happens when you click the **Notifications** icon (the bell) in the upper right of the Azure Portal and you see a red (!) icon next to your **Create application** notification.</span></span> <span data-ttu-id="49294-113">這表示建立應用程式時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="49294-113">This indicates there was an error when creating the application.</span></span>

<span data-ttu-id="49294-114">如果您按一下 [新增] 按鈕時發生錯誤，您會看到**錯誤**狀態的**通知**。</span><span class="sxs-lookup"><span data-stu-id="49294-114">If you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="49294-115">如果您想要取得此錯誤的詳細資訊以進一步了解，或分享給支援工程師，您可以依照[如何查看入口網站通知的詳細資訊](#how-to-see-the-details-of-a-portal-notification)一節的步驟，查看此錯誤的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="49294-115">If you want more details about the error to learn more to or share with a support engingeer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-dont-know-how-to-set-up-my-application-once-ive-added-it"></a><span data-ttu-id="49294-116">我在新增應用程式之後不知道如何設定</span><span class="sxs-lookup"><span data-stu-id="49294-116">I don’t know how to set up my application once I’ve added it</span></span>

<span data-ttu-id="49294-117">如果您需要了解自訂應用程式，[Azure AD 應用程式文件庫](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index)可幫助您進一步了解搭配 Azure AD 的單一登入和其運作方式。</span><span class="sxs-lookup"><span data-stu-id="49294-117">If you need help learning about custom applications, the [Azure AD Applications Document Library](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) help you to learn more about single sign-on with Azure AD and how it works.</span></span>

## <a name="how-to-see-the-details-of-a-portal-notification"></a><span data-ttu-id="49294-118">如何查看入口網站通知的詳細資料</span><span class="sxs-lookup"><span data-stu-id="49294-118">How to see the details of a portal notification</span></span>

<span data-ttu-id="49294-119">您可以依照下列步驟來查看任何入口網站通知的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="49294-119">You can see the details of any portal notification by following the steps below:</span></span>

1.  <span data-ttu-id="49294-120">按一下 Azure 入口網站右上方的 [通知] 圖示 (鐘)。</span><span class="sxs-lookup"><span data-stu-id="49294-120">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span></span>

2.  <span data-ttu-id="49294-121">選取**錯誤** 狀態的任何通知 (旁邊有紅色 (!))。</span><span class="sxs-lookup"><span data-stu-id="49294-121">Select any notification in an **Error** state (those with a red (!) next to them).</span></span>

   >[!NOTE]
   ><span data-ttu-id="49294-122">您無法按一下**成功**或**進行中**狀態的通知。</span><span class="sxs-lookup"><span data-stu-id="49294-122">You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
   >
   >

3.  <span data-ttu-id="49294-123">這會開啟 [通知詳細資料] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="49294-123">This open the **Notification Details** blade.</span></span>

4.  <span data-ttu-id="49294-124">請自行利用這項資訊來了解更多問題的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="49294-124">Use this information yourself to understand more details about the problem.</span></span>

5.  <span data-ttu-id="49294-125">如果您仍然需要協助，您也可以將這項資訊分享給支援工程師或產品群組，以取得協助來解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="49294-125">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span></span>

6.  <span data-ttu-id="49294-126">按一下 [複製錯誤] 文字方塊右邊的**複製圖示**，以複製所有通知詳細資料來分享給支援工程師或產品群組工程師。</span><span class="sxs-lookup"><span data-stu-id="49294-126">Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer.</span></span>

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a><span data-ttu-id="49294-127">如何將通知詳細資料傳送給支援工程師以取得協助</span><span class="sxs-lookup"><span data-stu-id="49294-127">How to get help by sending notification details to a support engineer</span></span>

<span data-ttu-id="49294-128">如果您需要協助，一定要與支援工程師分享**下列所有詳細資料**，好讓他們儘快幫助您。</span><span class="sxs-lookup"><span data-stu-id="49294-128">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="49294-129">只要**擷取螢幕畫面**，或按一下 [複製錯誤] 文字方塊右邊的**複製錯誤圖示**，輕鬆就能這樣做。</span><span class="sxs-lookup"><span data-stu-id="49294-129">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="49294-130">說明通知詳細資料</span><span class="sxs-lookup"><span data-stu-id="49294-130">Notification Details Explained</span></span>

<span data-ttu-id="49294-131">以下詳細說明每個通知項目的意義，並提供個別的範例。</span><span class="sxs-lookup"><span data-stu-id="49294-131">The below explains more what each of the notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="49294-132">必要通知項目</span><span class="sxs-lookup"><span data-stu-id="49294-132">Essential Notification Items</span></span>

-   <span data-ttu-id="49294-133">**標題** - 通知的描述性標題</span><span class="sxs-lookup"><span data-stu-id="49294-133">**Title** – the descriptive title of the notification</span></span>
   *  <span data-ttu-id="49294-134">範例 - **應用程式 Proxy 設定**</span><span class="sxs-lookup"><span data-stu-id="49294-134">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="49294-135">**描述** - 作業所產生之結果的描述</span><span class="sxs-lookup"><span data-stu-id="49294-135">**Description** – the description of what occurred as a result of the operation</span></span>

   *  <span data-ttu-id="49294-136">範例 - **輸入的內部 URL 正由另一個應用程式使用中**</span><span class="sxs-lookup"><span data-stu-id="49294-136">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="49294-137">**通知識別碼** - 通知的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="49294-137">**Notification Id** – the unique id of the notification</span></span>

   *  <span data-ttu-id="49294-138">範例 - **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="49294-138">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="49294-139">**用戶端要求識別碼** - 瀏覽器所產生的特定要求識別碼</span><span class="sxs-lookup"><span data-stu-id="49294-139">**Client Request Id** – the specific request id made by your browser</span></span>

   *  <span data-ttu-id="49294-140">範例 - **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="49294-140">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="49294-141">**時間戳記 UTC** - 發生通知期間的時間戳記 (UTC)</span><span class="sxs-lookup"><span data-stu-id="49294-141">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span></span>

   *  <span data-ttu-id="49294-142">範例 - **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="49294-142">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="49294-143">**內部交易識別碼** - 可用來在系統中查閱錯誤的內部識別碼</span><span class="sxs-lookup"><span data-stu-id="49294-143">**Internal Transaction Id** – the internal ID we can use to look the error up in our systems</span></span>

   *  <span data-ttu-id="49294-144">範例 - **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="49294-144">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="49294-145">**UPN** - 執行作業的使用者</span><span class="sxs-lookup"><span data-stu-id="49294-145">**UPN** – the user who performed the operation</span></span>

   *  <span data-ttu-id="49294-146">範例 - **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="49294-146">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="49294-147">**租用戶識別碼** - 作業執行使用者所屬之租用戶的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="49294-147">**Tenant Id** – the unique ID of the tenant that the user who performed the operation was a member of</span></span>

   *  <span data-ttu-id="49294-148">範例 - **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="49294-148">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="49294-149">**使用者物件識別碼** - 執行作業之使用者的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="49294-149">**User object Id** – the unique ID of the user who performed the operation</span></span>

 *  <span data-ttu-id="49294-150">範例 - **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="49294-150">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="49294-151">詳細通知項目</span><span class="sxs-lookup"><span data-stu-id="49294-151">Detailed Notification Items</span></span>

-   <span data-ttu-id="49294-152">**顯示名稱** – **(可以是空白)** 錯誤的詳細顯示名稱</span><span class="sxs-lookup"><span data-stu-id="49294-152">**Display Name** – **(can be empty)** a more detailed display name for the error</span></span>

  *  <span data-ttu-id="49294-153">範例 - **應用程式 Proxy 設定**</span><span class="sxs-lookup"><span data-stu-id="49294-153">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="49294-154">**狀態** – 通知的特定狀態</span><span class="sxs-lookup"><span data-stu-id="49294-154">**Status** – the specific status of the notification</span></span>

   *  <span data-ttu-id="49294-155">範例 – **失敗**</span><span class="sxs-lookup"><span data-stu-id="49294-155">Example – **Failed**</span></span>

-   <span data-ttu-id="49294-156">**物件識別碼** – **(可以是空白)** 執行作業所針對的物件識別碼</span><span class="sxs-lookup"><span data-stu-id="49294-156">**Object Id** – **(can be empty)** the object ID against which the operation was performed</span></span>

   *  <span data-ttu-id="49294-157">範例 - **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="49294-157">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="49294-158">**詳細資料** - 作業所產生之結果的詳細描述</span><span class="sxs-lookup"><span data-stu-id="49294-158">**Details** – the detailed description of what occurred as a result of the operation</span></span>

   *  <span data-ttu-id="49294-159">範例 - **內部 url 'http://bing.com/' 無效，因為已在使用中**</span><span class="sxs-lookup"><span data-stu-id="49294-159">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="49294-160">**複製錯誤** - 按一下 [複製錯誤] 文字方塊右邊的**複製圖示**，複製所有通知詳細資料來分享給支援工程師或產品群組工程師</span><span class="sxs-lookup"><span data-stu-id="49294-160">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

   *  <span data-ttu-id="49294-161">範例 ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="49294-161">Example ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="49294-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="49294-162">Next steps</span></span>
[<span data-ttu-id="49294-163">使用 Azure Active Directory 管理應用程式</span><span class="sxs-lookup"><span data-stu-id="49294-163">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)



