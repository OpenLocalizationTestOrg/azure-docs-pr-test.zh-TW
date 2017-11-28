---
title: "新增非組件庫的應用程式的 aaaProblem |Microsoft 文件"
description: "加入自訂非組件庫的應用程式時，了解 hello 一般問題的人臉"
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
ms.openlocfilehash: cfe9b657ae18cbacaddbd85658471a2c57c9cf95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problem-adding-a-non-gallery-application"></a><span data-ttu-id="80d71-103">新增不在資源庫內的應用程式時遇到問題</span><span class="sxs-lookup"><span data-stu-id="80d71-103">Problem adding a non-gallery application</span></span>

<span data-ttu-id="80d71-104">本文協助您 toounderstand hello 一般問題的人臉加入時**非組件庫的自訂應用程式**而且您可以執行 tooresolve 它們。</span><span class="sxs-lookup"><span data-stu-id="80d71-104">This article help you toounderstand hello common problems people face when adding **custom non-gallery applications** and what you can do tooresolve them.</span></span> 

## <a name="i-clicked-hello-add-button-and-my-application-took-a-long-time-tooappear"></a><span data-ttu-id="80d71-105">再按一下 [新增] 按鈕和我的應用程式花費很長的時間 tooappear hello</span><span class="sxs-lookup"><span data-stu-id="80d71-105">I clicked hello “add” button and my application took a long time tooappear</span></span>

<span data-ttu-id="80d71-106">在某些情況下，可能需要 1-2 分鐘 （或有時較長） 的應用程式 tooappear 之後將它加入 tooyour 目錄。</span><span class="sxs-lookup"><span data-stu-id="80d71-106">Under some circumstances, it can take 1-2 minutes (and sometimes longer) for an application tooappear after adding it tooyour directory.</span></span> <span data-ttu-id="80d71-107">雖然這不是 hello 正常預期的效能，您可以看到 hello 應用程式加入正在進行中，按一下 hello**通知**圖示 （hello 鈴聲） 在 hello 右上角 hello [Azure 入口網站](https://portal.azure.com/)，並尋找**進行中**或**已完成**通知標示為**建立應用程式**。</span><span class="sxs-lookup"><span data-stu-id="80d71-107">While this is not hello normal expected performance, you can see hello application addition is in progress by clicking on hello **Notifications** icon (hello bell) in hello upper right of hello [Azure Portal](https://portal.azure.com/) and looking for an **In Progress** or **Completed** notification labeled **Create application**.</span></span>

<span data-ttu-id="80d71-108">如果永遠不會加入您的應用程式，或按一下 [hello] 時，遇到錯誤**新增**按鈕，您會看到**通知**中**錯誤**狀態。</span><span class="sxs-lookup"><span data-stu-id="80d71-108">If your application is never added, or you encounter an error when clicking hello **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="80d71-109">如果您想 hello 錯誤 toolearn 詳細 tooor 分享支援 engingeer 需詳細資訊，您可以看到 hello 錯誤的詳細資訊 hello 中的 hello 步驟[如何 toosee hello 詳細資料的入口網站的通知](#how-to-see-the-details-of-a-portal-notification)> 一節。</span><span class="sxs-lookup"><span data-stu-id="80d71-109">If you want more details about hello error toolearn more tooor share with a support engingeer, you can see more information about hello error by following hello steps in hello [How toosee hello details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-clicked-hello-add-button-and-my-application-didnt-appear"></a><span data-ttu-id="80d71-110">按一下 [hello [新增] 按鈕和我的應用程式並未出現</span><span class="sxs-lookup"><span data-stu-id="80d71-110">I clicked hello “add” button and my application didn’t appear</span></span>

<span data-ttu-id="80d71-111">有時候，tootransient 問題，因為網路問題或 bug，請加入應用程式失敗。</span><span class="sxs-lookup"><span data-stu-id="80d71-111">Sometimes, due tootransient issues, networking problems, or a bug, adding an application fail.</span></span> <span data-ttu-id="80d71-112">當您按一下 hello 這樣，您可以告訴**通知**hello Azure 入口網站，並且 hello 右上角的圖示 （hello 鈴聲） 看到紅色 （！） 圖示下一步 tooyour**建立應用程式**通知。</span><span class="sxs-lookup"><span data-stu-id="80d71-112">You can tell this happens when you click hello **Notifications** icon (hello bell) in hello upper right of hello Azure Portal and you see a red (!) icon next tooyour **Create application** notification.</span></span> <span data-ttu-id="80d71-113">這表示有錯誤發生時建立 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="80d71-113">This indicates there was an error when creating hello application.</span></span>

<span data-ttu-id="80d71-114">如果您遇到錯誤時按一下 hello**新增**按鈕，您會看到**通知**中**錯誤**狀態。</span><span class="sxs-lookup"><span data-stu-id="80d71-114">If you encounter an error when clicking hello **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="80d71-115">如果您想 hello 錯誤 toolearn 詳細 tooor 分享支援 engingeer 需詳細資訊，您可以看到 hello 錯誤的詳細資訊 hello 中的 hello 步驟[如何 toosee hello 詳細資料的入口網站的通知](#how-to-see-the-details-of-a-portal-notification)> 一節。</span><span class="sxs-lookup"><span data-stu-id="80d71-115">If you want more details about hello error toolearn more tooor share with a support engingeer, you can see more information about hello error by following hello steps in hello [How toosee hello details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-dont-know-how-tooset-up-my-application-once-ive-added-it"></a><span data-ttu-id="80d71-116">我不知道如何註冊我的應用程式一次 tooset 我加入它</span><span class="sxs-lookup"><span data-stu-id="80d71-116">I don’t know how tooset up my application once I’ve added it</span></span>

<span data-ttu-id="80d71-117">若要深入了解自訂應用程式的說明，hello [Azure AD 應用程式文件庫](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index)協助您深入了解單一登入 Azure AD 與 toolearn 和它的運作方式。</span><span class="sxs-lookup"><span data-stu-id="80d71-117">If you need help learning about custom applications, hello [Azure AD Applications Document Library](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) help you toolearn more about single sign-on with Azure AD and how it works.</span></span>

## <a name="how-toosee-hello-details-of-a-portal-notification"></a><span data-ttu-id="80d71-118">如何 toosee hello 詳細資料的入口網站的通知</span><span class="sxs-lookup"><span data-stu-id="80d71-118">How toosee hello details of a portal notification</span></span>

<span data-ttu-id="80d71-119">您可以依照以下 hello 步驟看到 hello 詳細資料的任何入口網站的通知：</span><span class="sxs-lookup"><span data-stu-id="80d71-119">You can see hello details of any portal notification by following hello steps below:</span></span>

1.  <span data-ttu-id="80d71-120">按一下 hello**通知**hello Azure 入口網站的 hello 右上角的圖示 （hello 鈴聲）</span><span class="sxs-lookup"><span data-stu-id="80d71-120">click hello **Notifications** icon (hello bell) in hello upper right of hello Azure Portal</span></span>

2.  <span data-ttu-id="80d71-121">選取中的任何通知**錯誤**狀態 （紅色 （！） 的 [下一步 toothem 與那些）。</span><span class="sxs-lookup"><span data-stu-id="80d71-121">Select any notification in an **Error** state (those with a red (!) next toothem).</span></span>

   >[!NOTE]
   ><span data-ttu-id="80d71-122">您無法按一下**成功**或**進行中**狀態的通知。</span><span class="sxs-lookup"><span data-stu-id="80d71-122">You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
   >
   >

3.  <span data-ttu-id="80d71-123">這個開啟 hello**通知的詳細資料**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="80d71-123">This open hello **Notification Details** blade.</span></span>

4.  <span data-ttu-id="80d71-124">使用此資訊自行 toounderstand 更多有關 hello 問題詳細資料。</span><span class="sxs-lookup"><span data-stu-id="80d71-124">Use this information yourself toounderstand more details about hello problem.</span></span>

5.  <span data-ttu-id="80d71-125">如果您仍需要協助，您也可以與您的問題共用與支援工程師或 hello 產品群組 tooget 說明這項資訊。</span><span class="sxs-lookup"><span data-stu-id="80d71-125">If you still need help, you can also share this information with a support engineer or hello product group tooget help with your problem.</span></span>

6.  <span data-ttu-id="80d71-126">按一下 hello**複製圖示**方 hello toohello**複製錯誤**所有文字方塊 toocopy 都 hello 通知詳細資料 tooshare 與支援或產品的群組工程師。</span><span class="sxs-lookup"><span data-stu-id="80d71-126">Click hello **copy icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer.</span></span>

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a><span data-ttu-id="80d71-127">藉由傳送通知的詳細資料 tooa 支援工程師 tooget 的說明</span><span class="sxs-lookup"><span data-stu-id="80d71-127">How tooget help by sending notification details tooa support engineer</span></span>

<span data-ttu-id="80d71-128">它是非常重要，共用**所有 hello 下面所列的詳細資料**支援工程師，如果您需要協助，以便它們可以協助您快速。</span><span class="sxs-lookup"><span data-stu-id="80d71-128">It is very important that you share **all hello details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="80d71-129">您可以輕鬆**擷取螢幕畫面，**或按一下 hello**複製錯誤圖示**，找到 toohello 右邊 hello**複製錯誤**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="80d71-129">You can do this easily by **taking a screenshot,** or by clicking hello **Copy error icon**, found toohello right of hello **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="80d71-130">說明通知詳細資料</span><span class="sxs-lookup"><span data-stu-id="80d71-130">Notification Details Explained</span></span>

<span data-ttu-id="80d71-131">hello 以下說明更每一項 hello 通知項目表示，以及每個提供範例。</span><span class="sxs-lookup"><span data-stu-id="80d71-131">hello below explains more what each of hello notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="80d71-132">必要通知項目</span><span class="sxs-lookup"><span data-stu-id="80d71-132">Essential Notification Items</span></span>

-   <span data-ttu-id="80d71-133">**標題**– hello hello 通知的描述性標題</span><span class="sxs-lookup"><span data-stu-id="80d71-133">**Title** – hello descriptive title of hello notification</span></span>
   *  <span data-ttu-id="80d71-134">範例 - **應用程式 Proxy 設定**</span><span class="sxs-lookup"><span data-stu-id="80d71-134">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="80d71-135">**描述**– hello 所發生的 hello 運算結果的描述</span><span class="sxs-lookup"><span data-stu-id="80d71-135">**Description** – hello description of what occurred as a result of hello operation</span></span>

   *  <span data-ttu-id="80d71-136">範例 - **輸入的內部 URL 正由另一個應用程式使用中**</span><span class="sxs-lookup"><span data-stu-id="80d71-136">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="80d71-137">**通知識別碼**– hello 的 hello 通知的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="80d71-137">**Notification Id** – hello unique id of hello notification</span></span>

   *  <span data-ttu-id="80d71-138">範例 - **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="80d71-138">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="80d71-139">**用戶端要求 Id** – 您的瀏覽器所做的 hello 特定要求識別碼</span><span class="sxs-lookup"><span data-stu-id="80d71-139">**Client Request Id** – hello specific request id made by your browser</span></span>

   *  <span data-ttu-id="80d71-140">範例 - **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="80d71-140">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="80d71-141">**時間戳記 UTC** – hello 期間 hello 通知發生，以 UTC 時間戳記</span><span class="sxs-lookup"><span data-stu-id="80d71-141">**Time Stamp UTC** – hello timestamp during which hello notification occurred, in UTC</span></span>

   *  <span data-ttu-id="80d71-142">範例 - **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="80d71-142">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="80d71-143">**內部交易識別碼**– hello 我們可能佔用 toolook hello 錯誤，我們系統中的內部識別碼</span><span class="sxs-lookup"><span data-stu-id="80d71-143">**Internal Transaction Id** – hello internal ID we can use toolook hello error up in our systems</span></span>

   *  <span data-ttu-id="80d71-144">範例 - **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="80d71-144">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="80d71-145">**UPN** – 執行 hello 作業的 hello 使用者</span><span class="sxs-lookup"><span data-stu-id="80d71-145">**UPN** – hello user who performed hello operation</span></span>

   *  <span data-ttu-id="80d71-146">範例 - **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="80d71-146">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="80d71-147">**租用戶識別碼**– hello 唯一 hello 租用戶識別碼 hello 使用者執行 hello 作業人員是的成員</span><span class="sxs-lookup"><span data-stu-id="80d71-147">**Tenant Id** – hello unique ID of hello tenant that hello user who performed hello operation was a member of</span></span>

   *  <span data-ttu-id="80d71-148">範例 - **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="80d71-148">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="80d71-149">**使用者物件識別碼**– hello 執行 hello 作業的 hello 使用者的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="80d71-149">**User object Id** – hello unique ID of hello user who performed hello operation</span></span>

 *  <span data-ttu-id="80d71-150">範例 - **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="80d71-150">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="80d71-151">詳細通知項目</span><span class="sxs-lookup"><span data-stu-id="80d71-151">Detailed Notification Items</span></span>

-   <span data-ttu-id="80d71-152">**顯示名稱**– **（可以是空的）** hello 錯誤的更詳細的顯示名稱</span><span class="sxs-lookup"><span data-stu-id="80d71-152">**Display Name** – **(can be empty)** a more detailed display name for hello error</span></span>

  *  <span data-ttu-id="80d71-153">範例 - **應用程式 Proxy 設定**</span><span class="sxs-lookup"><span data-stu-id="80d71-153">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="80d71-154">**狀態**– hello hello 通知的特定狀態</span><span class="sxs-lookup"><span data-stu-id="80d71-154">**Status** – hello specific status of hello notification</span></span>

   *  <span data-ttu-id="80d71-155">範例 – **失敗**</span><span class="sxs-lookup"><span data-stu-id="80d71-155">Example – **Failed**</span></span>

-   <span data-ttu-id="80d71-156">**物件識別碼**– **（可以是空的）** hello 的 hello 針對已執行作業的物件識別碼</span><span class="sxs-lookup"><span data-stu-id="80d71-156">**Object Id** – **(can be empty)** hello object ID against which hello operation was performed</span></span>

   *  <span data-ttu-id="80d71-157">範例 - **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="80d71-157">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="80d71-158">**詳細資料**– hello 的詳細描述所發生的 hello 運算結果</span><span class="sxs-lookup"><span data-stu-id="80d71-158">**Details** – hello detailed description of what occurred as a result of hello operation</span></span>

   *  <span data-ttu-id="80d71-159">範例 - **內部 url 'http://bing.com/' 無效，因為已在使用中**</span><span class="sxs-lookup"><span data-stu-id="80d71-159">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="80d71-160">**複製錯誤**– 按一下 hello**複製圖示**方 hello toohello**複製錯誤**所有文字方塊 toocopy 都 hello 與支援或產品的群組工程師通知詳細資料 tooshare</span><span class="sxs-lookup"><span data-stu-id="80d71-160">**Copy error** – Click hello **copy icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer</span></span>

   *  <span data-ttu-id="80d71-161">範例 ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="80d71-161">Example ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="80d71-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="80d71-162">Next steps</span></span>
[<span data-ttu-id="80d71-163">使用 Azure Active Directory 管理應用程式</span><span class="sxs-lookup"><span data-stu-id="80d71-163">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)



