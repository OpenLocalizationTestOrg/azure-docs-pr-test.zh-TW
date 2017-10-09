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
# <a name="how-toouse-hello-engagement-api-on-ios"></a>TooUse hello Engagement API 在 iOS 上的方式
這份文件是附加元件 toohello 文件如何在 iOS 上的 tooIntegrate Engagement： 它會提供有關如何 toouse 會 hello Engagement API tooreport 您的應用程式統計資料的深入詳細資訊。

請記住，如果您的應用程式工作階段、 活動、 當機以及技術資訊，請只想 Engagement tooreport 然後 hello 最簡單方式是您的自訂 toomake`UIViewController`物件繼承自 hello 對應`EngagementViewController`類別.

如果您想 toodo 更多，例如，如果您需要 tooreport 應用程式特定事件、 錯誤與工作，或如果您在非 hello hello 中實作的其中一個 tooreport 應用程式的活動有不同的方式`EngagementViewController`類別，則您需要 toouse helloEngagement 應用程式開發介面。

hello Engagement 應用程式開發介面由提供 hello`EngagementAgent`類別。 這個類別的執行個體可以擷取由呼叫 hello`[EngagementAgent shared]`靜態方法 (請注意該 hello`EngagementAgent`傳回的物件是單一值)。

任何應用程式開發介面呼叫，hello`EngagementAgent`必須藉由呼叫 hello 方法初始化物件`[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`

## <a name="engagement-concepts"></a>Engagement 概念
hello 下列部分精簡 hello 常見[Mobile Engagement 概念](mobile-engagement-concepts.md)hello iOS 平台。

### <a name="session-and-activity"></a>`Session`和`Activity`
*活動*通常都與一個螢幕的 hello 應用程式，為 toosay hello*活動*時囉 」 畫面隨即出現，並停止囉 」 畫面關閉時啟動： 這是 hello 情況hello Engagement SDK 整合使用 hello`EngagementViewController`類別。

但是*活動*可以也使用來控制手動 hello Engagement 應用程式開發介面。 這可以讓 toosplit 指定的螢幕詳細 hello 這個畫面 （例如 tooknown 頻率和時間長度對話方塊內使用，則此畫面） 的使用方式的數個子組件 tooget。

## <a name="reporting-activities"></a>報告活動
### <a name="user-starts-a-new-activity"></a>使用者啟動新的活動
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

您需要 toocall`startActivity()`變更每個階段 hello 使用者活動。 hello 第一個呼叫 toothis 函式會啟動新的使用者工作階段。

### <a name="user-ends-his-current-activity"></a>使用者結束其目前的活動
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> 您應該**永不**呼叫此函式自己，，但如果您想 toosplit 的應用程式分成數個工作階段的另一個用途： 最後 toothis 函式會的呼叫 hello 立即，目前工作階段的後續呼叫，因此太`startActivity()`會啟動新的工作階段。 此函式會自動呼叫 hello SDK 關閉您的應用程式時。
> 
> 

## <a name="reporting-events"></a>報告事件
### <a name="session-events"></a>工作階段事件
工作階段事件是他的工作階段期間執行使用者通常使用的 tooreport hello 動作。

**不含額外資料的範例：**

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

**含額外資料的範例：**

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

### <a name="standalone-events"></a>獨立事件
反對 toosession 事件，獨立事件可用於外部 hello 的工作階段的內容。

**範例：**

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a>報告錯誤
### <a name="session-errors"></a>工作階段錯誤
工作階段錯誤是在他的工作階段期間影響 hello 使用者通常使用的 tooreport hello 錯誤。

**範例：**

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

### <a name="standalone-errors"></a>獨立錯誤
反對 toosession 錯誤，獨立錯誤可用的工作階段的 hello 內容之外。

**範例：**

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a>報告工作
**範例：**

假設您要登入程序的 tooreport hello 持續時間：

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

### <a name="report-errors-during-a-job"></a>報告工作期間的錯誤
錯誤可能是正在執行而不是工作的相關的 tooa 相關 toohello 目前使用者工作階段。

**範例：**

假設您要在您登入程序期間的 tooreport 錯誤：

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

### <a name="events-during-a-job"></a>工作期間的事件
事件可能會執行作業，而不是相關的 tooa 相關 toohello 目前使用者工作階段。

**範例：**

假設我們有社交網路，而且我們使用工作 tooreport hello 總時間期間的 hello 使用者是連接的 toohello 伺服器。 hello 使用者可以從他的朋友接收訊息，這是作業的事件。

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

## <a name="extra-parameters"></a>額外的參數
附加的 tooevents、 錯誤、 活動與工作，可以是任意的資料。

此資料可以結構化，它會使用 iOS 的 NSDictionary 類別。

請注意，額外項目可以包含 `arrays(NSArray, NSMutableArray)`、`numbers(NSNumber class)`、`strings(NSString, NSMutableString)`、`urls(NSURL)`、`data(NSData, NSMutableData)` 或其他 `NSDictionary` 執行個體。

> [!NOTE]
> hello 額外的參數會以序列化 JSON。 如果您想 toopass 比 hello 上述不同的物件，您必須實作下列方法在類別中的 hello:
> 
> -(NSString*)JSONRepresentation;
> 
> hello 方法應該傳回物件的 JSON 表示法。
> 
> 

### <a name="example"></a>範例
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a>限制
#### <a name="keys"></a>之間的信任
每個索引鍵中 hello`NSDictionary`必須符合下列規則運算式的 hello:

`^[a-zA-Z][a-zA-Z_0-9]*`

這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。

#### <a name="size"></a>大小
額外項目會受到限制太**1024年**每個呼叫 （一次編碼 JSON 中的 hello Engagement 代理程式） 的字元。

在 hello 上述範例中，JSON 傳送 toohello 伺服器 hello 會是 58 字元：

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>報告應用程式資訊
您可以手動報告追蹤資訊 （或任何其他應用程式特定資訊） 使用 hello`sendAppInfo:`函式。

請注意，這些資訊可傳送以累加方式： 只 hello 最新的值指定索引鍵將會保留指定的裝置。

類似事件 extras hello`NSDictionary`類別是使用的 tooabstract 應用程式資訊，請注意，陣列或子字典將會被視為一般字串 （使用 JSON 序列化）。

**範例：**

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a>限制
#### <a name="keys"></a>之間的信任
每個索引鍵中 hello`NSDictionary`必須符合下列規則運算式的 hello:

`^[a-zA-Z][a-zA-Z_0-9]*`

這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。

#### <a name="size"></a>大小
應用程式資訊受到太**1024年**每個呼叫 （一次編碼 JSON 中的 hello Engagement 代理程式） 的字元。

在 hello 上述範例中，JSON 傳送 toohello 伺服器 hello 是 44 個字元：

    {"birthdate":"1983-12-07","gender":"female"}
