---
title: "aaaHow tooUse hello Engagement API 在 Windows Phone Silverlight 上"
description: "如何 tooUse hello Engagement API 在 Windows Phone Silverlight 上"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ae2ba2e8-f75b-4dee-a164-a7dd65d35a23
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1e84be95cc910be7f1227b4ae60eb483a1939284
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-phone-silverlight"></a>如何 tooUse hello Engagement API 在 Windows Phone Silverlight 上
這份文件是附加元件 toohello 文件[如何在 Windows Phone Silverlight 應用程式中的 toointegrate Mobile Engagement](mobile-engagement-windows-phone-integrate-engagement.md)。 它提供有關如何 toouse 會 hello Engagement API tooreport 您的應用程式統計資料的深入詳細資訊。

如果您的應用程式工作階段、 活動、 當機以及技術資訊，請只想 Engagement tooreport 則 hello 最簡單的方式是 toomake 所有您`PhoneApplicationPage`子類別是繼承自 hello`EngagementPage`類別。

如果您想 toodo 更多，例如，如果您需要 tooreport 應用程式特定事件、 錯誤與工作，或如果您在非 hello hello 中實作的其中一個 tooreport 應用程式的活動有不同的方式`EngagementPage`類別，則您需要 toouse helloEngagement 應用程式開發介面。

hello Engagement 應用程式開發介面由提供 hello`EngagementAgent`類別。 您可以存取透過 toothose 方法`EngagementAgent.Instance`。

即使尚未初始化 hello 代理程式的模組，每個呼叫 toohello API 會延後和 hello 代理程式可用時再重新執行。

## <a name="engagement-concepts"></a>Engagement 概念
下列組件的 hello 精簡 hello Mobile Engagement 概念 hello Windows Phone 平台。

### <a name="session-and-activity"></a>`Session`和`Activity`
*活動*通常都與一頁的 hello 應用程式，為 toosay hello*活動*hello 頁面隨即出現，而 hello 頁已關閉時停止時啟動： 這是 hello 的情況下如果 helloEngagement SDK 整合使用 hello`EngagementPage`類別。

但是*活動*可以也使用來控制手動 hello Engagement 應用程式開發介面。 這可以讓 toosplit 指定的頁面數個子組件 tooget 詳細 hello 使用量 （例如 tooknown 頻率和時間的對話方塊內使用，則此頁面） 此頁面。

## <a name="reporting-activities"></a>報告活動
### <a name="user-starts-a-new-activity"></a>使用者啟動新的活動
#### <a name="reference"></a>參考
            void StartActivity(string name, Dictionary<object, object> extras = null)

您需要 toocall`StartActivity()`變更每個階段 hello 使用者活動。 hello 第一個呼叫 toothis 函式會啟動新的使用者工作階段。

> [!IMPORTANT]
> hello SDK hello 應用程式關閉時，會自動呼叫 hello EndActivity 方法。 因此，強烈建議 toocall hello StartActivity 方法時的 hello 使用者變更與 hello EndActivity 方法，因為呼叫這個方法會強制 hello 目前工作階段 toobe tooNEVER 呼叫 hello 活動已結束。
> 
> 

#### <a name="example"></a>範例
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a>使用者結束其目前的活動
#### <a name="reference"></a>參考
            void EndActivity()

您需要 toocall`EndActivity()`至少一次當 hello 使用者完成其最後一個活動。 這會通知的 hello 逾期 Engagement SDK hello 使用者目前閒置，並 hello 使用者工作階段需要 toobe 關閉一次 hello 工作階段逾時 (如果您呼叫`StartActivity()`hello 工作階段逾時到期前，只需繼續 hello 工作階段的)。

#### <a name="example"></a>範例
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a>報告作業
### <a name="start-a-job"></a>啟動作業
#### <a name="reference"></a>參考
            void StartJob(string name, Dictionary<object, object> extras = null)

經過一段時間，您可以使用 hello tootrack certains 的工作。

#### <a name="example"></a>範例
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a>結束作業
#### <a name="reference"></a>參考
            void EndJob(string name)

只要已終止工作所追蹤的工作，您應該呼叫此作業，hello EndJob 方法藉由提供 hello 作業名稱。

#### <a name="example"></a>範例
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a>報告事件
事件有三種類型：

* 獨立事件
* 工作階段事件
* 作業事件

### <a name="standalone-events"></a>獨立事件
#### <a name="reference"></a>參考
            void SendEvent(string name, Dictionary<object, object> extras = null)

工作階段的 hello 環境之外發生獨立事件。

#### <a name="example"></a>範例
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a>工作階段事件
#### <a name="reference"></a>參考
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

工作階段事件是他的工作階段期間執行使用者通常使用的 tooreport hello 動作。

#### <a name="example"></a>範例
**沒有資料：**

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

**有資料：**

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a>作業事件
#### <a name="reference"></a>參考
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

作業事件是在作業期間執行使用者通常使用的 tooreport hello 動作。

#### <a name="example"></a>範例
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a>報告錯誤
錯誤有三種類型：

* 獨立錯誤
* 工作階段錯誤
* 作業錯誤

### <a name="standalone-errors"></a>獨立錯誤
#### <a name="reference"></a>參考
            void SendError(string name, Dictionary<object, object> extras = null)

反對 toosession，獨立錯誤可能會發生錯誤的工作階段的 hello 內容之外。

#### <a name="example"></a>範例
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a>工作階段錯誤
#### <a name="reference"></a>參考
            void SendSessionError(string name, Dictionary<object, object> extras = null)

工作階段錯誤是在他的工作階段期間影響 hello 使用者通常使用的 tooreport hello 錯誤。

#### <a name="example"></a>範例
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a>作業錯誤
#### <a name="reference"></a>參考
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

錯誤可能是正在執行而不是工作的相關的 tooa 相關 toohello 目前使用者工作階段。

#### <a name="example"></a>範例
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a>報告當機
hello 代理程式會將兩個方法 toodeal 提供當機。

### <a name="send-an-exception"></a>傳送例外狀況
#### <a name="reference"></a>參考
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a>範例
透過呼叫下列函式您可以隨時傳送例外狀況：

            EngagementAgent.Instance.SendCrash(aCatchedException);

您也可以使用選擇性參數 tooterminate hello 參與工作階段在 hello 相同的時間比傳送嗨損毀。 因此，呼叫 toodo:

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

如果您這樣做，請只在傳送嗨損毀之後將關閉 hello 工作階段和工作。

### <a name="send-an-unhandled-exception"></a>傳送未處理的例外狀況
#### <a name="reference"></a>參考
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

Engagement 也會提供方法 toosend 未處理的例外狀況。 這是 hello silverlight UnhandledException 事件處理常式內使用時特別有用。

這個方法將**永遠**呼叫後終止 hello 參與工作階段和工作。

#### <a name="example"></a>範例
您可以使用它 tooimplement 自己 UnhandledException 處理常式 （特別是如果您已停用報告功能的 Engagement hello 自動損毀）。 例如，在 hello`Application_UnhandledException`方法 hello`App.xaml.cs`檔案：

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a>OnActivated
### <a name="reference"></a>參考
            void OnActivated(ActivatedEventArgs e)

Hello 使用者向前巡覽，遠離應用程式之後就會引發 hello 停用事件，, hello 作業系統會進入休眠狀態的 tooput hello 應用程式。 接著，hello 應用程式是正在標記要刪除。 應用程式已終止這個處理序中，但會保留一些 hello 應用程式和 hello hello 應用程式內的個別頁面 hello 狀態相關的資料。

您有 tooinsert`EngagementAgent.Instance.OnActivated(e)`在 hello `Application_Activated` hello App.xaml.cs 檔案 tooreset hello Engagement 代理程式時 hello 應用程式是否已 Tombstoned 方法。

### <a name="example"></a>範例
            // Inside your App.xaml.cs file

            // Code tooexecute when hello application is activated (brought tooforeground)
            // This code will not execute when hello application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a>裝置識別碼
            String GetDeviceId()

您可以藉由呼叫這個方法來取得 hello engagement 裝置識別碼。

## <a name="extras-parameters"></a>額外的參數
附加的 tooan 事件、 錯誤、 活動或工作，可以是任意的資料。 可以使用字典來結構化這些資料。 索引鍵和值可以是任何型別。

額外項目資料會序列化，因此如果您想 tooinsert 自己的額外項目中的型別必須 tooadd 這種類型的資料合約。

### <a name="example"></a>範例
我們建立一個新的類別叫 "Person"。

            using System.Runtime.Serialization;

            namespace Engagement.Agent
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

然後，我們會加入`Person`額外的執行個體 tooan。

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> 如果您將其他類型的物件，請確定其 tostring （） 方法是實作的 tooreturn 人類可讀取的字串。
> 
> 

### <a name="limits"></a>限制
#### <a name="keys"></a>之間的信任
Hello 物件中的每個索引鍵必須符合下列規則運算式的 hello:

`^[a-zA-Z][a-zA-Z_0-9]*$`

這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。

#### <a name="size"></a>大小
額外項目會受到限制太**1024年**呼叫每個字元。

## <a name="reporting-application-information"></a>報告應用程式資訊
### <a name="reference"></a>參考
            void SendAppInfo(Dictionary<object, object> appInfos)

您可以手動報告追蹤資訊 （或任何其他應用程式特定資訊） 使用 hello SendAppInfo() 函式。

請注意，這些資訊可傳送以累加方式： 只 hello 最新的值指定索引鍵將會保留指定的裝置。 事件的額外功能，例如使用字典\<物件，物件\>tooattach 資訊。

### <a name="example"></a>範例
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a>限制
#### <a name="keys"></a>之間的信任
Hello 物件中的每個索引鍵必須符合下列規則運算式的 hello:

`^[a-zA-Z][a-zA-Z_0-9]*$`

這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。

#### <a name="size"></a>大小
應用程式資訊受到太**1024年**呼叫每個字元。

在 hello 上述範例中，JSON 傳送 toohello 伺服器 hello 是 44 個字元：

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a>記錄
### <a name="enable-logging"></a>啟用記錄
hello SDK 可設定的 tooproduce hello IDE 主控台中的測試記錄。
預設不會啟用這些記錄檔。 toocustomize，更新 hello 屬性`EngagementAgent.Instance.TestLogEnabled`hello 值可從 hello 的 tooone`EngagementTestLogLevel`列舉型別，例如：

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
