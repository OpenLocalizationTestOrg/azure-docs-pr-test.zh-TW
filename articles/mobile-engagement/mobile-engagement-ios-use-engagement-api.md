---
title: "如何在 iOS 上使用 Engagement API"
description: "最新的 iOS SDK - 如何在 iOS 上使用 Engagement API"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1fb4509e-3804-46c1-949f-1cf727f91f9f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a31424da98205e97bdf57010cccfd044360f03dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-ios"></a><span data-ttu-id="982d7-103">如何在 iOS 上使用 Engagement API</span><span class="sxs-lookup"><span data-stu-id="982d7-103">How to Use the Engagement API on iOS</span></span>
<span data-ttu-id="982d7-104">本文件是＜如何在 iOS 上整合 Engagement＞文件的附加說明：有關如何使用 Engagement API 來報告您應用程式的統計資料，本文件提供了深入的詳細說明。</span><span class="sxs-lookup"><span data-stu-id="982d7-104">This document is an add-on to the document How to Integrate Engagement on iOS: it provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="982d7-105">請記住，如果您只想要 Engagement 向您報告應用程式的工作階段、活動、當機和技術資訊，那麼最簡單的方法是讓所有自訂 `UIViewController` 物件繼承自對應的 `EngagementViewController` 類別。</span><span class="sxs-lookup"><span data-stu-id="982d7-105">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your custom `UIViewController` objects inherit from the corresponding `EngagementViewController` class.</span></span>

<span data-ttu-id="982d7-106">如果您想要執行更多工作 (例如，若您需要報告應用程式的特定事件、錯誤和作業，或者您需要以不同於 `EngagementViewController` 類別中的方式來報告應用程式的活動)，則您需要使用 Engagement API。</span><span class="sxs-lookup"><span data-stu-id="982d7-106">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementViewController` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="982d7-107">Engagement API 是由 `EngagementAgent` 類別提供。</span><span class="sxs-lookup"><span data-stu-id="982d7-107">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="982d7-108">此類別的執行個體，可以藉由呼叫 `[EngagementAgent shared]` 靜態方法 (請注意，傳回的 `EngagementAgent` 物件為單一值) 來擷取。</span><span class="sxs-lookup"><span data-stu-id="982d7-108">An instance of this class can be retrieved by calling the `[EngagementAgent shared]` static method (note that the `EngagementAgent` object returned is a singleton).</span></span>

<span data-ttu-id="982d7-109">在執行任何 API 呼叫之前，必須先初始化 `EngagementAgent` 物件 (藉由呼叫 `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];` 方法)</span><span class="sxs-lookup"><span data-stu-id="982d7-109">Before any API calls, the `EngagementAgent` object must be initialized by calling the method `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="982d7-110">Engagement 概念</span><span class="sxs-lookup"><span data-stu-id="982d7-110">Engagement concepts</span></span>
<span data-ttu-id="982d7-111">以下部分簡要說明適用於 iOS 平台的 [Mobile Engagement 概念](mobile-engagement-concepts.md) 。</span><span class="sxs-lookup"><span data-stu-id="982d7-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for the iOS platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="982d7-112">`Session`和`Activity`</span><span class="sxs-lookup"><span data-stu-id="982d7-112">`Session` and `Activity`</span></span>
<span data-ttu-id="982d7-113">活動通常會與應用程式的某個畫面相關聯，也就是說，活動會在畫面顯示時啟動，並在畫面關閉時停止：這是使用 `EngagementViewController` 類別整合 Engagement SDK 時的情況。</span><span class="sxs-lookup"><span data-stu-id="982d7-113">An *activity* is usually associated with one screen of the application, that is to say the *activity* starts when the screen is displayed and stops when the screen is closed: this is the case when the Engagement SDK is integrated by using the `EngagementViewController` classes.</span></span>

<span data-ttu-id="982d7-114">但您也可以透過 Engagement API 手動控制「活動」  。</span><span class="sxs-lookup"><span data-stu-id="982d7-114">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="982d7-115">這樣可以將指定的畫面分隔為數個子部分，以取得關於此畫面使用方式的詳細資料 (例如，可了解此畫面內對話方塊的使用頻率與使用時間長度)。</span><span class="sxs-lookup"><span data-stu-id="982d7-115">This allows to split a given screen in several sub parts to get more details about the usage of this screen (for example to known how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="982d7-116">報告活動</span><span class="sxs-lookup"><span data-stu-id="982d7-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="982d7-117">使用者啟動新的活動</span><span class="sxs-lookup"><span data-stu-id="982d7-117">User starts a new Activity</span></span>
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

<span data-ttu-id="982d7-118">每當使用者活動變更，您就需要呼叫 `startActivity()` 。</span><span class="sxs-lookup"><span data-stu-id="982d7-118">You need to call `startActivity()` each time the user activity changes.</span></span> <span data-ttu-id="982d7-119">第一次呼叫此函數會啟動新的使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="982d7-119">The first call to this function starts a new user session.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="982d7-120">使用者結束其目前的活動</span><span class="sxs-lookup"><span data-stu-id="982d7-120">User ends his current Activity</span></span>
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> <span data-ttu-id="982d7-121">您應該「永不」自行呼叫此函數，除非您希望將應用程式的一次使用分割為數個工作階段：呼叫此函數會立即結束目前的工作階段，因此後續的 `startActivity()` 呼叫會啟動新的工作階段。</span><span class="sxs-lookup"><span data-stu-id="982d7-121">You should **NEVER** call this function by yourself, except if you want to split one use of your application into several sessions: a call to this function would end the current session immediately, so, a subsequent call to `startActivity()` would start a new session.</span></span> <span data-ttu-id="982d7-122">當您的應用程式關閉時，SDK 會自動呼叫此函數。</span><span class="sxs-lookup"><span data-stu-id="982d7-122">This function is automatically called by the SDK when your application is closed.</span></span>
> 
> 

## <a name="reporting-events"></a><span data-ttu-id="982d7-123">報告事件</span><span class="sxs-lookup"><span data-stu-id="982d7-123">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="982d7-124">工作階段事件</span><span class="sxs-lookup"><span data-stu-id="982d7-124">Session events</span></span>
<span data-ttu-id="982d7-125">工作階段事件通常用來報告在其工作階段期間由使用者所執行的動作。</span><span class="sxs-lookup"><span data-stu-id="982d7-125">Session events are usually used to report the actions performed by a user during his session.</span></span>

<span data-ttu-id="982d7-126">**不含額外資料的範例：**</span><span class="sxs-lookup"><span data-stu-id="982d7-126">**Example without extra data:**</span></span>

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:nil];
            ...
       }
       [...]
    }

<span data-ttu-id="982d7-127">**含額外資料的範例：**</span><span class="sxs-lookup"><span data-stu-id="982d7-127">**Example with extra data:**</span></span>

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        NSMutableDictionary* extras = [NSMutableDictionary dictionary];
        [extras setObject:[NSNumber numberWithInt:toInterfaceOrientation] forKey:@"to_orientation_id"];
        [extras setObject:[NSNumber numberWithDouble:duration] forKey:@"duration"];
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:extras];
            ...
       }
       [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="982d7-128">獨立事件</span><span class="sxs-lookup"><span data-stu-id="982d7-128">Standalone events</span></span>
<span data-ttu-id="982d7-129">相對於工作階段事件，獨立事件可以在工作階段的內容之外使用。</span><span class="sxs-lookup"><span data-stu-id="982d7-129">Contrary to session events, standalone events can be used outside of the context of a session.</span></span>

<span data-ttu-id="982d7-130">**範例：**</span><span class="sxs-lookup"><span data-stu-id="982d7-130">**Example:**</span></span>

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a><span data-ttu-id="982d7-131">報告錯誤</span><span class="sxs-lookup"><span data-stu-id="982d7-131">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="982d7-132">工作階段錯誤</span><span class="sxs-lookup"><span data-stu-id="982d7-132">Session errors</span></span>
<span data-ttu-id="982d7-133">工作階段錯誤通常用來報告在其工作階段期間影響使用者的錯誤。</span><span class="sxs-lookup"><span data-stu-id="982d7-133">Session errors are usually used to report the errors impacting the user during his session.</span></span>

<span data-ttu-id="982d7-134">**範例：**</span><span class="sxs-lookup"><span data-stu-id="982d7-134">**Example:**</span></span>

    /** The user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* The user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="982d7-135">獨立錯誤</span><span class="sxs-lookup"><span data-stu-id="982d7-135">Standalone errors</span></span>
<span data-ttu-id="982d7-136">相對於工作階段錯誤，獨立錯誤可以在工作階段的內容之外使用。</span><span class="sxs-lookup"><span data-stu-id="982d7-136">Contrary to session errors, standalone errors can be used outside of the context of a session.</span></span>

<span data-ttu-id="982d7-137">**範例：**</span><span class="sxs-lookup"><span data-stu-id="982d7-137">**Example:**</span></span>

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a><span data-ttu-id="982d7-138">報告工作</span><span class="sxs-lookup"><span data-stu-id="982d7-138">Reporting Jobs</span></span>
<span data-ttu-id="982d7-139">**範例：**</span><span class="sxs-lookup"><span data-stu-id="982d7-139">**Example:**</span></span>

<span data-ttu-id="982d7-140">假設您想要報告登入程序的持續時間：</span><span class="sxs-lookup"><span data-stu-id="982d7-140">Suppose you want to report the duration of your login process:</span></span>

    [...]
    -(void)signIn
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      [... sign in ...]

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    }
    [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="982d7-141">報告工作期間的錯誤</span><span class="sxs-lookup"><span data-stu-id="982d7-141">Report Errors during a Job</span></span>
<span data-ttu-id="982d7-142">錯誤可能與正在執行的工作關聯，而不是與目前的使用者工作階段關聯。</span><span class="sxs-lookup"><span data-stu-id="982d7-142">Errors can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="982d7-143">**範例：**</span><span class="sxs-lookup"><span data-stu-id="982d7-143">**Example:**</span></span>

<span data-ttu-id="982d7-144">假設您想要報告您登入程序期間的錯誤：</span><span class="sxs-lookup"><span data-stu-id="982d7-144">Suppose you want to report an error during your login process:</span></span>

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try to sign in */
        NSError* error = nil;
        [self trySigin:&error];
        success = error == nil;

        /* If an error occured report it */
        if(!success)
        {
          [[EngagementAgent shared] sendJobError:@"sign_in_error"
                         jobName:@"sign_in"
                          extras:[NSDictionary dictionaryWithObject:[error localizedDescription] forKey:@"error"]];

          /* Retry after a moment */
          [NSThread sleepForTimeInterval:20];
        }
      }

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    };
    [...]

### <a name="events-during-a-job"></a><span data-ttu-id="982d7-145">工作期間的事件</span><span class="sxs-lookup"><span data-stu-id="982d7-145">Events during a job</span></span>
<span data-ttu-id="982d7-146">事件可能與執行的工作相關，而不是與目前的使用者工作階段相關。</span><span class="sxs-lookup"><span data-stu-id="982d7-146">Events can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="982d7-147">**範例：**</span><span class="sxs-lookup"><span data-stu-id="982d7-147">**Example:**</span></span>

<span data-ttu-id="982d7-148">假設我們有社交網路，且使用工作來報告使用者連接到伺服器這段期間的總時間。</span><span class="sxs-lookup"><span data-stu-id="982d7-148">Suppose we have a social network, and we use a job to report the total time during which the user is connected to the server.</span></span> <span data-ttu-id="982d7-149">使用者可以接收來自朋友的訊息，這就是工作事件。</span><span class="sxs-lookup"><span data-stu-id="982d7-149">The user can receive messages from his friends, this is a job event.</span></span>

    [...]
    - (void) signin
    {
      [...Sign in code...]
      [[EngagementAgent shared] startJob:@"connection" extras:nil];
    }
    [...]
    - (void) signout
    {
      [...Sign out code...]
      [[EngagementAgent shared] endJob:@"connection"];
    }
    [...]
    - (void) onMessageReceived
    {
      [...Notify user...]
      [[EngagementAgent shared] sendJobEvent:@"connection" jobName:@"message_received" extras:nil];
    }
    [...]

## <a name="extra-parameters"></a><span data-ttu-id="982d7-150">額外的參數</span><span class="sxs-lookup"><span data-stu-id="982d7-150">Extra parameters</span></span>
<span data-ttu-id="982d7-151">可以將任意資料附加到事件、錯誤、活動及工作。</span><span class="sxs-lookup"><span data-stu-id="982d7-151">Arbitrary data can be attached to events, errors, activities and jobs.</span></span>

<span data-ttu-id="982d7-152">此資料可以結構化，它會使用 iOS 的 NSDictionary 類別。</span><span class="sxs-lookup"><span data-stu-id="982d7-152">This data can be structured, it uses iOS's NSDictionary class.</span></span>

<span data-ttu-id="982d7-153">請注意，額外項目可以包含 `arrays(NSArray, NSMutableArray)`、`numbers(NSNumber class)`、`strings(NSString, NSMutableString)`、`urls(NSURL)`、`data(NSData, NSMutableData)` 或其他 `NSDictionary` 執行個體。</span><span class="sxs-lookup"><span data-stu-id="982d7-153">Note that extras can contain `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` or other `NSDictionary` instances.</span></span>

> [!NOTE]
> <span data-ttu-id="982d7-154">額外的參數會以 JSON 序列化。</span><span class="sxs-lookup"><span data-stu-id="982d7-154">The extra parameter is serialized in JSON.</span></span> <span data-ttu-id="982d7-155">如果您想要傳遞與上述不同的物件，必須在類別中實作以下方法：</span><span class="sxs-lookup"><span data-stu-id="982d7-155">If you want to pass different objects than the ones described above, you must implement the following method in your class:</span></span>
> 
> <span data-ttu-id="982d7-156">-(NSString*)JSONRepresentation;</span><span class="sxs-lookup"><span data-stu-id="982d7-156">-(NSString*)JSONRepresentation;</span></span>
> 
> <span data-ttu-id="982d7-157">方法應傳回您物件的 JSON 表示法。</span><span class="sxs-lookup"><span data-stu-id="982d7-157">The method should return a JSON representation of your object.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="982d7-158">範例</span><span class="sxs-lookup"><span data-stu-id="982d7-158">Example</span></span>
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a><span data-ttu-id="982d7-159">限制</span><span class="sxs-lookup"><span data-stu-id="982d7-159">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="982d7-160">之間的信任</span><span class="sxs-lookup"><span data-stu-id="982d7-160">Keys</span></span>
<span data-ttu-id="982d7-161">`NSDictionary` 中的每個索引鍵都必須符合下列規則運算式：</span><span class="sxs-lookup"><span data-stu-id="982d7-161">Each key in the `NSDictionary` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="982d7-162">這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。</span><span class="sxs-lookup"><span data-stu-id="982d7-162">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="982d7-163">大小</span><span class="sxs-lookup"><span data-stu-id="982d7-163">Size</span></span>
<span data-ttu-id="982d7-164">額外項目限制為一次呼叫 **1024** 個字元 (由 Engagement 代理程式以 JSON 編碼之後)。</span><span class="sxs-lookup"><span data-stu-id="982d7-164">Extras are limited to **1024** characters per call (once encoded in JSON by the Engagement agent).</span></span>

<span data-ttu-id="982d7-165">在上述範例中，傳送到伺服器的 JSON 會是 58 個字元：</span><span class="sxs-lookup"><span data-stu-id="982d7-165">In the previous example, the JSON sent to the server is 58 characters long:</span></span>

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="982d7-166">報告應用程式資訊</span><span class="sxs-lookup"><span data-stu-id="982d7-166">Reporting Application Information</span></span>
<span data-ttu-id="982d7-167">您可以使用 `sendAppInfo:` 函式手動報告追蹤資訊 (或是任何其他應用程式特定資訊)。</span><span class="sxs-lookup"><span data-stu-id="982d7-167">You can manually report tracking information (or any other application specific information) using the `sendAppInfo:` function.</span></span>

<span data-ttu-id="982d7-168">請注意，這些資訊可以累加地傳送：只有指定索引鍵的最新值會保留給指定的裝置。</span><span class="sxs-lookup"><span data-stu-id="982d7-168">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="982d7-169">如同事件額外項目一樣， `NSDictionary` 類別是用來摘錄應用程式資訊，並請注意，陣列或子字典將被視為一般字串 (使用 JSON 序列化)。</span><span class="sxs-lookup"><span data-stu-id="982d7-169">Like event extras, the `NSDictionary` class is used to abstract application information, note that arrays or sub-dictionaries will be treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="982d7-170">**範例：**</span><span class="sxs-lookup"><span data-stu-id="982d7-170">**Example:**</span></span>

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a><span data-ttu-id="982d7-171">限制</span><span class="sxs-lookup"><span data-stu-id="982d7-171">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="982d7-172">之間的信任</span><span class="sxs-lookup"><span data-stu-id="982d7-172">Keys</span></span>
<span data-ttu-id="982d7-173">`NSDictionary` 中的每個索引鍵都必須符合下列規則運算式：</span><span class="sxs-lookup"><span data-stu-id="982d7-173">Each key in the `NSDictionary` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="982d7-174">這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。</span><span class="sxs-lookup"><span data-stu-id="982d7-174">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="982d7-175">大小</span><span class="sxs-lookup"><span data-stu-id="982d7-175">Size</span></span>
<span data-ttu-id="982d7-176">應用程式資訊限制為一次呼叫 **1024** 個字元 (由 Engagement 代理程式以 JSON 編碼之後)。</span><span class="sxs-lookup"><span data-stu-id="982d7-176">Application information are limited to **1024** characters per call (once encoded in JSON by the Engagement agent).</span></span>

<span data-ttu-id="982d7-177">在上述範例中，傳送到伺服器的 JSON 會是 44 個字元：</span><span class="sxs-lookup"><span data-stu-id="982d7-177">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
