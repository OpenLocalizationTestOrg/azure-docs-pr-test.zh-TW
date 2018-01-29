---
title: "如何在 Windows Phone Silverlight 上使用 Engagement API"
description: "如何在 Windows Phone Silverlight 上使用 Engagement API"
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
ms.openlocfilehash: ec8b6c13ea052c8063dfde4321cdd286ab6cb817
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-use-the-engagement-api-on-windows-phone-silverlight"></a>如何在 Windows Phone Silverlight 上使用 Engagement API
此文件是 [如何在 Windows Phone Silverlight 應用程式中整合 Mobile Engagement](mobile-engagement-windows-phone-integrate-engagement.md)文件的附加說明。 它會提供關於如何使用 Engagement API 來回報您應用程式的統計資料之詳細資訊。

如果您只想要 Engagement 報告應用程式的工作階段、活動、當機和技術資訊，最簡單的方式就是讓您所有的 `PhoneApplicationPage` 子類別繼承自 `EngagementPage` 類別。

如果您想要執行更多工作 (例如，若您需要報告應用程式的特定事件、錯誤和作業，或者您需要以不同於 `EngagementPage` 類別中的方式來報告應用程式的活動)，則您需要使用 Engagement API。

Engagement API 是由 `EngagementAgent` 類別提供。 您可以透過 `EngagementAgent.Instance`取得這些方法。

檔代理程式模組尚未初始化時，每個對 API 的呼叫會被延後，並且將於代理程式可使用時再次執行。

## <a name="engagement-concepts"></a>Engagement 概念
以下部分簡要說明適用於 Windows Phone 平台的 Mobile Engagement 概念。

### <a name="session-and-activity"></a>`Session`和`Activity`
「活動」通常與應用程式的某個頁面關聯，也就是說，「活動」會在頁面顯示時啟動，當頁面關閉時就停止：使用 `EngagementPage` 類別來整合 Engagement SDK 的情況便是如此。

但您也可以透過 Engagement API 手動控制「活動」  。 這樣可允許將指定的頁面分割成多個部分，以獲得有關該頁面使用方式的詳細資訊 (例如，對話方塊在此頁面的使用平率和使用時間)。

## <a name="reporting-activities"></a>報告活動
### <a name="user-starts-a-new-activity"></a>使用者啟動新的活動
#### <a name="reference"></a>參考
            void StartActivity(string name, Dictionary<object, object> extras = null)

每當使用者活動變更，您就需要呼叫 `StartActivity()` 。 第一次呼叫此函式會啟動新的使用者工作階段。

> [!IMPORTANT]
> 當應用程式關閉時，SDK 會自動呼叫 EndActivity 方法。 因此，「強烈」建議每當使用者的活動變更時便叫呼叫 StartActivity 方法，並且「絕對不要」呼叫 EndActivity 方法，因為呼叫此方法會強制結束目前的工作階段。
> 
> 

#### <a name="example"></a>範例
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a>使用者結束其目前的活動
#### <a name="reference"></a>參考
            void EndActivity()

使用者完成最後一個活動時，您至少需要呼叫 `EndActivity()` 一次。 這會通知 Engagement SDK，說明使用者目前處於閒置狀態，且工作階段逾時到期時就得關閉使用者工作階段 (如果您在工作階段逾時到期前就呼叫 `StartActivity()` ，工作階段只會繼續)。

#### <a name="example"></a>範例
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a>報告作業
### <a name="start-a-job"></a>啟動作業
#### <a name="reference"></a>參考
            void StartJob(string name, Dictionary<object, object> extras = null)

您可以使用作業在一段時間內追蹤某些工作。

#### <a name="example"></a>範例
            // An upload begins...

            // Set the extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a>結束作業
#### <a name="reference"></a>參考
            void EndJob(string name)

一旦作業追蹤的工作被終止，您就應該針對該作業呼叫 EndJob 方法 (透過提供該作業名稱)。

#### <a name="example"></a>範例
            // In the previous section, we started an upload tracking with a job
            // Then, the upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a>報告事件
事件有三種類型：

* 獨立事件
* 工作階段事件
* 作業事件

### <a name="standalone-events"></a>獨立事件
#### <a name="reference"></a>參考
            void SendEvent(string name, Dictionary<object, object> extras = null)

獨立事件可以出現在工作階段的內容之外。

#### <a name="example"></a>範例
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a>工作階段事件
#### <a name="reference"></a>參考
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

工作階段事件通常用來報告在其工作階段期間由使用者所執行的動作。

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

作業事件通常用來報告在作業期間由使用者所執行的動作。

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

不同於工作階段錯誤，獨立錯誤可以出現在工作階段的內容之外。

#### <a name="example"></a>範例
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a>工作階段錯誤
#### <a name="reference"></a>參考
            void SendSessionError(string name, Dictionary<object, object> extras = null)

工作階段錯誤通常用來報告在其工作階段期間影響使用者的錯誤。

#### <a name="example"></a>範例
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a>作業錯誤
#### <a name="reference"></a>參考
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

錯誤可能與正在執行的工作關聯，而不是與目前的使用者工作階段關聯。

#### <a name="example"></a>範例
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a>報告當機
代理程式提供兩種處理當機的方法。

### <a name="send-an-exception"></a>傳送例外狀況
#### <a name="reference"></a>參考
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a>範例
透過呼叫下列函式您可以隨時傳送例外狀況：

            EngagementAgent.Instance.SendCrash(aCatchedException);

您也可以使用選擇性的參數來同時結束參與工作階段並傳送當機。 若要這樣做，請呼叫：

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

如果您這樣做，工作階段和作業將於傳送當機後立即關閉。

### <a name="send-an-unhandled-exception"></a>傳送未處理的例外狀況
#### <a name="reference"></a>參考
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

Engagement 也提供將傳送未處理的例外狀況之方法。 在 Silverlight 的 UnhandledException 事件處理常式內此方法特別有用。

此方法「一律」  會在被呼叫之後終止 Engagement 工作階段和作業。

#### <a name="example"></a>範例
您可以使用它來實作您自己的 UnhandledException 處理常式 (尤其是如果您已停用 Engagement 的自動損毀報告功能)。 例如在 `App.xaml.cs` 檔案的 `Application_UnhandledException` 方法中：

            // In your App.xaml.cs file

            // Code to execute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a>OnActivated
### <a name="reference"></a>參考
            void OnActivated(ActivatedEventArgs e)

當使用者繼續瀏覽並離開應用程式的時候，作業系統會在 Deactivated 事件引發之後嘗試讓應用程式進入休眠狀態。 然後該應用程式會被加上刪除標記。 此程序中的映欲程式會被終止，但會保留某些和應用程式狀態與個別頁面有關的資料。

您必須將 `EngagementAgent.Instance.OnActivated(e)` 插入來自 App.xaml.cs 檔案的 `Application_Activated` 方法中，以在應用程式被加上刪除標記時重設 Engagement 代理程式。

### <a name="example"></a>範例
            // Inside your App.xaml.cs file

            // Code to execute when the application is activated (brought to foreground)
            // This code will not execute when the application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a>裝置識別碼
            String GetDeviceId()

您可以藉由呼叫這個方法來取得 Egagement 的裝置識別碼。

## <a name="extras-parameters"></a>額外的參數
可以附加任意資料到事件、錯誤、活動或作業。 可以使用字典來結構化這些資料。 索引鍵和值可以是任何型別。

額外的資料已經序列化，因此如果您想要在額外資料中插入您自己的型別，您必須針對此型別新增資料合約。

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

然後將 `Person` 執行個體新增至額外資料。

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> 如果您新增其他類型的物件，請確定已實作它們的 ToString() 方法，以傳回使用者可閱讀的字串。
> 
> 

### <a name="limits"></a>限制
#### <a name="keys"></a>之間的信任
物件中的每個索引鍵都必須符合下列規則運算式：

`^[a-zA-Z][a-zA-Z_0-9]*$`

這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。

#### <a name="size"></a>大小
每次呼叫的額外資料限制為 **1024** 個字元。

## <a name="reporting-application-information"></a>報告應用程式資訊
### <a name="reference"></a>參考
            void SendAppInfo(Dictionary<object, object> appInfos)

您可以使用 SendAppInfo() 函式來報告追蹤資訊 (或任何其他應用程式相關的資訊)。

請注意，這些資訊可以累加地傳送：只有指定的索引鍵的最新值會保留給指定的裝置。 和事件額外資料一樣，請使用 Dictionary\<object, object\> 來附加資訊。

### <a name="example"></a>範例
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a>限制
#### <a name="keys"></a>之間的信任
物件中的每個索引鍵都必須符合下列規則運算式：

`^[a-zA-Z][a-zA-Z_0-9]*$`

這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。

#### <a name="size"></a>大小
每次呼叫的應用程式資訊限制為 **1024** 個字元。

在上述範例中，傳送到伺服器的 JSON 會是 44 個字元：

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a>記錄
### <a name="enable-logging"></a>啟用記錄
SDK 可以設定為在 IDE 主控台中產生測試記錄檔。
預設不會啟用這些記錄檔。 若要自訂這種情況，請將屬性 `EngagementAgent.Instance.TestLogEnabled` 更新為 `EngagementTestLogLevel` 列舉的其中一個可用值，例如︰

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
