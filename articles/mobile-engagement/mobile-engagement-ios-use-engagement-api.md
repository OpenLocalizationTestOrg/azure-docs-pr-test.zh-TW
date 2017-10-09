---
title: "在 iOS 上 aaaHow tooUse hello Engagement 應用程式開發介面"
description: "最新的 iOS SDK-tooUse hello Engagement API 在 iOS 上的方式"
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
ms.openlocfilehash: 7fb9b95ad319cf3b1e2de81b5d6aee5b30266069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-ios"></a><span data-ttu-id="26a4a-103">TooUse hello Engagement API 在 iOS 上的方式</span><span class="sxs-lookup"><span data-stu-id="26a4a-103">How tooUse hello Engagement API on iOS</span></span>
<span data-ttu-id="26a4a-104">這份文件是附加元件 toohello 文件如何在 iOS 上的 tooIntegrate Engagement： 它會提供有關如何 toouse 會 hello Engagement API tooreport 您的應用程式統計資料的深入詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="26a4a-104">This document is an add-on toohello document How tooIntegrate Engagement on iOS: it provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="26a4a-105">請記住，如果您的應用程式工作階段、 活動、 當機以及技術資訊，請只想 Engagement tooreport 然後 hello 最簡單方式是您的自訂 toomake`UIViewController`物件繼承自 hello 對應`EngagementViewController`類別.</span><span class="sxs-lookup"><span data-stu-id="26a4a-105">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your custom `UIViewController` objects inherit from hello corresponding `EngagementViewController` class.</span></span>

<span data-ttu-id="26a4a-106">如果您想 toodo 更多，例如，如果您需要 tooreport 應用程式特定事件、 錯誤與工作，或如果您在非 hello hello 中實作的其中一個 tooreport 應用程式的活動有不同的方式`EngagementViewController`類別，則您需要 toouse helloEngagement 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="26a4a-106">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementViewController` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="26a4a-107">hello Engagement 應用程式開發介面由提供 hello`EngagementAgent`類別。</span><span class="sxs-lookup"><span data-stu-id="26a4a-107">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="26a4a-108">這個類別的執行個體可以擷取由呼叫 hello`[EngagementAgent shared]`靜態方法 (請注意該 hello`EngagementAgent`傳回的物件是單一值)。</span><span class="sxs-lookup"><span data-stu-id="26a4a-108">An instance of this class can be retrieved by calling hello `[EngagementAgent shared]` static method (note that hello `EngagementAgent` object returned is a singleton).</span></span>

<span data-ttu-id="26a4a-109">任何應用程式開發介面呼叫，hello`EngagementAgent`必須藉由呼叫 hello 方法初始化物件`[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span><span class="sxs-lookup"><span data-stu-id="26a4a-109">Before any API calls, hello `EngagementAgent` object must be initialized by calling hello method `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="26a4a-110">Engagement 概念</span><span class="sxs-lookup"><span data-stu-id="26a4a-110">Engagement concepts</span></span>
<span data-ttu-id="26a4a-111">hello 下列部分精簡 hello 常見[Mobile Engagement 概念](mobile-engagement-concepts.md)hello iOS 平台。</span><span class="sxs-lookup"><span data-stu-id="26a4a-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for hello iOS platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="26a4a-112">`Session`和`Activity`</span><span class="sxs-lookup"><span data-stu-id="26a4a-112">`Session` and `Activity`</span></span>
<span data-ttu-id="26a4a-113">*活動*通常都與一個螢幕的 hello 應用程式，為 toosay hello*活動*時囉 」 畫面隨即出現，並停止囉 」 畫面關閉時啟動： 這是 hello 情況hello Engagement SDK 整合使用 hello`EngagementViewController`類別。</span><span class="sxs-lookup"><span data-stu-id="26a4a-113">An *activity* is usually associated with one screen of hello application, that is toosay hello *activity* starts when hello screen is displayed and stops when hello screen is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementViewController` classes.</span></span>

<span data-ttu-id="26a4a-114">但是*活動*可以也使用來控制手動 hello Engagement 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="26a4a-114">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="26a4a-115">這可以讓 toosplit 指定的螢幕詳細 hello 這個畫面 （例如 tooknown 頻率和時間長度對話方塊內使用，則此畫面） 的使用方式的數個子組件 tooget。</span><span class="sxs-lookup"><span data-stu-id="26a4a-115">This allows toosplit a given screen in several sub parts tooget more details about hello usage of this screen (for example tooknown how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="26a4a-116">報告活動</span><span class="sxs-lookup"><span data-stu-id="26a4a-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="26a4a-117">使用者啟動新的活動</span><span class="sxs-lookup"><span data-stu-id="26a4a-117">User starts a new Activity</span></span>
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

<span data-ttu-id="26a4a-118">您需要 toocall`startActivity()`變更每個階段 hello 使用者活動。</span><span class="sxs-lookup"><span data-stu-id="26a4a-118">You need toocall `startActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="26a4a-119">hello 第一個呼叫 toothis 函式會啟動新的使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="26a4a-119">hello first call toothis function starts a new user session.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="26a4a-120">使用者結束其目前的活動</span><span class="sxs-lookup"><span data-stu-id="26a4a-120">User ends his current Activity</span></span>
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> <span data-ttu-id="26a4a-121">您應該**永不**呼叫此函式自己，，但如果您想 toosplit 的應用程式分成數個工作階段的另一個用途： 最後 toothis 函式會的呼叫 hello 立即，目前工作階段的後續呼叫，因此太`startActivity()`會啟動新的工作階段。</span><span class="sxs-lookup"><span data-stu-id="26a4a-121">You should **NEVER** call this function by yourself, except if you want toosplit one use of your application into several sessions: a call toothis function would end hello current session immediately, so, a subsequent call too`startActivity()` would start a new session.</span></span> <span data-ttu-id="26a4a-122">此函式會自動呼叫 hello SDK 關閉您的應用程式時。</span><span class="sxs-lookup"><span data-stu-id="26a4a-122">This function is automatically called by hello SDK when your application is closed.</span></span>
> 
> 

## <a name="reporting-events"></a><span data-ttu-id="26a4a-123">報告事件</span><span class="sxs-lookup"><span data-stu-id="26a4a-123">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="26a4a-124">工作階段事件</span><span class="sxs-lookup"><span data-stu-id="26a4a-124">Session events</span></span>
<span data-ttu-id="26a4a-125">工作階段事件是他的工作階段期間執行使用者通常使用的 tooreport hello 動作。</span><span class="sxs-lookup"><span data-stu-id="26a4a-125">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

<span data-ttu-id="26a4a-126">**不含額外資料的範例：**</span><span class="sxs-lookup"><span data-stu-id="26a4a-126">**Example without extra data:**</span></span>

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

<span data-ttu-id="26a4a-127">**含額外資料的範例：**</span><span class="sxs-lookup"><span data-stu-id="26a4a-127">**Example with extra data:**</span></span>

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

### <a name="standalone-events"></a><span data-ttu-id="26a4a-128">獨立事件</span><span class="sxs-lookup"><span data-stu-id="26a4a-128">Standalone events</span></span>
<span data-ttu-id="26a4a-129">反對 toosession 事件，獨立事件可用於外部 hello 的工作階段的內容。</span><span class="sxs-lookup"><span data-stu-id="26a4a-129">Contrary toosession events, standalone events can be used outside of hello context of a session.</span></span>

<span data-ttu-id="26a4a-130">**範例：**</span><span class="sxs-lookup"><span data-stu-id="26a4a-130">**Example:**</span></span>

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a><span data-ttu-id="26a4a-131">報告錯誤</span><span class="sxs-lookup"><span data-stu-id="26a4a-131">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="26a4a-132">工作階段錯誤</span><span class="sxs-lookup"><span data-stu-id="26a4a-132">Session errors</span></span>
<span data-ttu-id="26a4a-133">工作階段錯誤是在他的工作階段期間影響 hello 使用者通常使用的 tooreport hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="26a4a-133">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

<span data-ttu-id="26a4a-134">**範例：**</span><span class="sxs-lookup"><span data-stu-id="26a4a-134">**Example:**</span></span>

    /** hello user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* hello user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="26a4a-135">獨立錯誤</span><span class="sxs-lookup"><span data-stu-id="26a4a-135">Standalone errors</span></span>
<span data-ttu-id="26a4a-136">反對 toosession 錯誤，獨立錯誤可用的工作階段的 hello 內容之外。</span><span class="sxs-lookup"><span data-stu-id="26a4a-136">Contrary toosession errors, standalone errors can be used outside of hello context of a session.</span></span>

<span data-ttu-id="26a4a-137">**範例：**</span><span class="sxs-lookup"><span data-stu-id="26a4a-137">**Example:**</span></span>

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a><span data-ttu-id="26a4a-138">報告工作</span><span class="sxs-lookup"><span data-stu-id="26a4a-138">Reporting Jobs</span></span>
<span data-ttu-id="26a4a-139">**範例：**</span><span class="sxs-lookup"><span data-stu-id="26a4a-139">**Example:**</span></span>

<span data-ttu-id="26a4a-140">假設您要登入程序的 tooreport hello 持續時間：</span><span class="sxs-lookup"><span data-stu-id="26a4a-140">Suppose you want tooreport hello duration of your login process:</span></span>

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

### <a name="report-errors-during-a-job"></a><span data-ttu-id="26a4a-141">報告工作期間的錯誤</span><span class="sxs-lookup"><span data-stu-id="26a4a-141">Report Errors during a Job</span></span>
<span data-ttu-id="26a4a-142">錯誤可能是正在執行而不是工作的相關的 tooa 相關 toohello 目前使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="26a4a-142">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="26a4a-143">**範例：**</span><span class="sxs-lookup"><span data-stu-id="26a4a-143">**Example:**</span></span>

<span data-ttu-id="26a4a-144">假設您要在您登入程序期間的 tooreport 錯誤：</span><span class="sxs-lookup"><span data-stu-id="26a4a-144">Suppose you want tooreport an error during your login process:</span></span>

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try toosign in */
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

### <a name="events-during-a-job"></a><span data-ttu-id="26a4a-145">工作期間的事件</span><span class="sxs-lookup"><span data-stu-id="26a4a-145">Events during a job</span></span>
<span data-ttu-id="26a4a-146">事件可能會執行作業，而不是相關的 tooa 相關 toohello 目前使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="26a4a-146">Events can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="26a4a-147">**範例：**</span><span class="sxs-lookup"><span data-stu-id="26a4a-147">**Example:**</span></span>

<span data-ttu-id="26a4a-148">假設我們有社交網路，而且我們使用工作 tooreport hello 總時間期間的 hello 使用者是連接的 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="26a4a-148">Suppose we have a social network, and we use a job tooreport hello total time during which hello user is connected toohello server.</span></span> <span data-ttu-id="26a4a-149">hello 使用者可以從他的朋友接收訊息，這是作業的事件。</span><span class="sxs-lookup"><span data-stu-id="26a4a-149">hello user can receive messages from his friends, this is a job event.</span></span>

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

## <a name="extra-parameters"></a><span data-ttu-id="26a4a-150">額外的參數</span><span class="sxs-lookup"><span data-stu-id="26a4a-150">Extra parameters</span></span>
<span data-ttu-id="26a4a-151">附加的 tooevents、 錯誤、 活動與工作，可以是任意的資料。</span><span class="sxs-lookup"><span data-stu-id="26a4a-151">Arbitrary data can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="26a4a-152">此資料可以結構化，它會使用 iOS 的 NSDictionary 類別。</span><span class="sxs-lookup"><span data-stu-id="26a4a-152">This data can be structured, it uses iOS's NSDictionary class.</span></span>

<span data-ttu-id="26a4a-153">請注意，額外項目可以包含 `arrays(NSArray, NSMutableArray)`、`numbers(NSNumber class)`、`strings(NSString, NSMutableString)`、`urls(NSURL)`、`data(NSData, NSMutableData)` 或其他 `NSDictionary` 執行個體。</span><span class="sxs-lookup"><span data-stu-id="26a4a-153">Note that extras can contain `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` or other `NSDictionary` instances.</span></span>

> [!NOTE]
> <span data-ttu-id="26a4a-154">hello 額外的參數會以序列化 JSON。</span><span class="sxs-lookup"><span data-stu-id="26a4a-154">hello extra parameter is serialized in JSON.</span></span> <span data-ttu-id="26a4a-155">如果您想 toopass 比 hello 上述不同的物件，您必須實作下列方法在類別中的 hello:</span><span class="sxs-lookup"><span data-stu-id="26a4a-155">If you want toopass different objects than hello ones described above, you must implement hello following method in your class:</span></span>
> 
> <span data-ttu-id="26a4a-156">-(NSString*)JSONRepresentation;</span><span class="sxs-lookup"><span data-stu-id="26a4a-156">-(NSString*)JSONRepresentation;</span></span>
> 
> <span data-ttu-id="26a4a-157">hello 方法應該傳回物件的 JSON 表示法。</span><span class="sxs-lookup"><span data-stu-id="26a4a-157">hello method should return a JSON representation of your object.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="26a4a-158">範例</span><span class="sxs-lookup"><span data-stu-id="26a4a-158">Example</span></span>
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a><span data-ttu-id="26a4a-159">限制</span><span class="sxs-lookup"><span data-stu-id="26a4a-159">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="26a4a-160">之間的信任</span><span class="sxs-lookup"><span data-stu-id="26a4a-160">Keys</span></span>
<span data-ttu-id="26a4a-161">每個索引鍵中 hello`NSDictionary`必須符合下列規則運算式的 hello:</span><span class="sxs-lookup"><span data-stu-id="26a4a-161">Each key in hello `NSDictionary` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="26a4a-162">這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。</span><span class="sxs-lookup"><span data-stu-id="26a4a-162">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="26a4a-163">大小</span><span class="sxs-lookup"><span data-stu-id="26a4a-163">Size</span></span>
<span data-ttu-id="26a4a-164">額外項目會受到限制太**1024年**每個呼叫 （一次編碼 JSON 中的 hello Engagement 代理程式） 的字元。</span><span class="sxs-lookup"><span data-stu-id="26a4a-164">Extras are limited too**1024** characters per call (once encoded in JSON by hello Engagement agent).</span></span>

<span data-ttu-id="26a4a-165">在 hello 上述範例中，JSON 傳送 toohello 伺服器 hello 會是 58 字元：</span><span class="sxs-lookup"><span data-stu-id="26a4a-165">In hello previous example, hello JSON sent toohello server is 58 characters long:</span></span>

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="26a4a-166">報告應用程式資訊</span><span class="sxs-lookup"><span data-stu-id="26a4a-166">Reporting Application Information</span></span>
<span data-ttu-id="26a4a-167">您可以手動報告追蹤資訊 （或任何其他應用程式特定資訊） 使用 hello`sendAppInfo:`函式。</span><span class="sxs-lookup"><span data-stu-id="26a4a-167">You can manually report tracking information (or any other application specific information) using hello `sendAppInfo:` function.</span></span>

<span data-ttu-id="26a4a-168">請注意，這些資訊可傳送以累加方式： 只 hello 最新的值指定索引鍵將會保留指定的裝置。</span><span class="sxs-lookup"><span data-stu-id="26a4a-168">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="26a4a-169">類似事件 extras hello`NSDictionary`類別是使用的 tooabstract 應用程式資訊，請注意，陣列或子字典將會被視為一般字串 （使用 JSON 序列化）。</span><span class="sxs-lookup"><span data-stu-id="26a4a-169">Like event extras, hello `NSDictionary` class is used tooabstract application information, note that arrays or sub-dictionaries will be treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="26a4a-170">**範例：**</span><span class="sxs-lookup"><span data-stu-id="26a4a-170">**Example:**</span></span>

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a><span data-ttu-id="26a4a-171">限制</span><span class="sxs-lookup"><span data-stu-id="26a4a-171">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="26a4a-172">之間的信任</span><span class="sxs-lookup"><span data-stu-id="26a4a-172">Keys</span></span>
<span data-ttu-id="26a4a-173">每個索引鍵中 hello`NSDictionary`必須符合下列規則運算式的 hello:</span><span class="sxs-lookup"><span data-stu-id="26a4a-173">Each key in hello `NSDictionary` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="26a4a-174">這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。</span><span class="sxs-lookup"><span data-stu-id="26a4a-174">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="26a4a-175">大小</span><span class="sxs-lookup"><span data-stu-id="26a4a-175">Size</span></span>
<span data-ttu-id="26a4a-176">應用程式資訊受到太**1024年**每個呼叫 （一次編碼 JSON 中的 hello Engagement 代理程式） 的字元。</span><span class="sxs-lookup"><span data-stu-id="26a4a-176">Application information are limited too**1024** characters per call (once encoded in JSON by hello Engagement agent).</span></span>

<span data-ttu-id="26a4a-177">在 hello 上述範例中，JSON 傳送 toohello 伺服器 hello 是 44 個字元：</span><span class="sxs-lookup"><span data-stu-id="26a4a-177">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
