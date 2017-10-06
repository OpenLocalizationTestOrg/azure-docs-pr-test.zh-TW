---
title: "aaaHow toouse java 的通知中樞"
description: "深入了解如何從 Java 後端 toouse Azure 通知中樞。"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 4c3f966d-0158-4a48-b949-9fa3666cb7e4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: java
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: afcf305b1acd9ee28ee4889040ece59d9399d29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-java"></a>如何從 Java 的通知中樞 toouse
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

本主題描述 hello 的主要功能，完全支援 hello 新官方 Azure 通知中樞 Java SDK。 這是開放原始碼專案，您可以檢視 hello 整個 SDK 程式碼中的[Java SDK]。 

一般情況下，您可以從 Java/PHP/Python/Ruby 後端存取所有通知中樞功能 hello MSDN 主題中所述，使用 hello 通知中樞 REST 介面[通知中心 REST Api](http://msdn.microsoft.com/library/dn223264.aspx)。 此 Java SDK 透過 Java 中的這些 REST 介面提供了精簡型包裝函式。 

hello SDK 支援目前：

* 通知中樞的 CRUD 
* 註冊的 CRUD
* 安裝管理
* 匯入/匯出註冊
* 定期傳送
* 排程的傳送
* 透過 Java NIO 的非同步作業
* 受支援的平台：APNS (iOS)、GCM (Android)、WNS (Windows 市集應用程式)、MPNS (Windows Phone)、ADM (Amazon Kindle Fire)、Baidu (沒有 Google 服務的 Android) 

## <a name="sdk-usage"></a>SDK 的使用方式
### <a name="compile-and-build"></a>編譯和建置
使用 [Maven]

toobuild:

    mvn package

## <a name="code"></a>代碼
### <a name="notification-hub-cruds"></a>通知中樞 CRUD
**建立 NamespaceManager：**

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

**建立通知中樞：**

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 或

    hub = new NotificationHub("connection string", "hubname");

**取得通知中樞：**

    hub = namespaceManager.getNotificationHub("hubname");

**更新通知中樞：**

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

**刪除通知中樞：**

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a>註冊 CRUD
**建立通知中樞用戶端：**

    hub = new NotificationHub("connection string", "hubname");

**建立 Windows 註冊：**

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

**建立 iOS 註冊：**

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

同樣地，您可以建立 Android (GCM)、Windows Phone (MPNS) 和 Kindle Fire (ADM) 的註冊。

**建立範本註冊：**

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

**使用建立 registrationid + upsert 模式來建立註冊**

如果 hello 裝置上儲存註冊識別碼，請移除重複項目，因為遺失 tooany 回應：

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

**更新註冊：**

    hub.updateRegistration(reg);

**刪除註冊：**

    hub.deleteRegistration(regid);

**查詢註冊：**

* **取得單一註冊：**
  
    hub.getRegistration(regid);
* **取得中樞的所有註冊：**
  
    hub.getRegistrations();
* **取得具有標籤的註冊：**
  
    hub.getRegistrationsByTag("myTag");
* **依通道取得註冊：**
  
    hub.getRegistrationsByChannel("devicetoken");

所有集合查詢都支援 $top 和接續權杖。

### <a name="installation-api-usage"></a>安裝 API 的使用方式
安裝 API 是註冊管理的替代機制。 而不是維護多個註冊並非易事，且可能在錯誤或無效率地輕鬆完成，它現在是可能 toouse 單一安裝物件。 安裝包含所需的一切：推播通道 (裝置權杖)、標籤、範本、次要磚 (適用於 WNS 和 APNS)。 您不再需要 toocall hello 服務 tooget 識別碼-只產生 GUID 或任何其他識別項、 將它保留在裝置上並傳送推播通道 （裝置權杖） 以及 tooyour 後的端。 在 hello 後端，您應該只執行單一呼叫： CreateOrUpdateInstallation，它完全是等冪，所以您可以免費 tooretry 視。

以 Amazon Kindle Fire 為例，將如下所示：

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

如果您想 tooupdate 它： 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

在進階案例中，我們有部分更新功能可讓 toomodify hello 安裝物件的只有特定的屬性。 基本上，部分更新是您可以對安裝物件執行的 JSON Patch 作業子集。

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

刪除安裝：

    hub.deleteInstallation(installation.getInstallationId());

CreateOrUpdate、Patch 和 Delete 最終都會與 Get 一致。 要求的作業只會 hello 呼叫期間會 toohello 系統佇列，而且會在背景中執行。 請注意，取得不是主要的執行階段案例，但只針對偵錯和疑難排解的用途，hello 服務緊密節流。

安裝的傳送流程註冊 hello 與相同。 我們只導入選項 tootarget 通知 toohello 特定安裝-請使用標記"InstallationId: {預期-識別碼}"。 就上述案例而言，將如下所示：

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

數個範本之一：

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a>排程通知 (適用於 STANDARD 層)
為定期傳送，但具有一個額外的參數-scheduledTime 指出傳遞通知的時機，請 hello 相同。 服務可接受目前 + 5 分鐘與目前 + 7 天之間的任何時間點。

**排程 Windows 原生通知：**

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a>匯入/匯出 (適用於 STANDARD 層)
有時會對登錄的必要的 tooperform 大量作業。 通常它是與另一個系統或只修正 massive toosay 更新 hello 標記的整合。 如果我們說數千個註冊強烈不建議 toouse Get/更新流程。 匯入/匯出功能是設計的 toocover hello 案例。 基本上您提供存取 toosome blob 容器儲存體帳戶做為來源的連入的資料和輸出的位置。

**提交匯出工作：**

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


**提交匯入工作：**

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

**等到工作完成：**

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

**取得所有工作：**

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

**與 SAS 簽章 URI:**這是 hello 的部分 blob 檔案或 blob 容器的 URL，加上的權限和到期時間參數的集合再加上所有使用帳戶的 SAS 金鑰進行這些作業的簽章。 Azure Storage Java SDK 具有豐富的功能，包括建立此類的 URI。 簡單的替代方法，您可查看 ImportExportE2E 測試類別 （來自 hello github 位置） 具有的簽章演算法非常基本和壓縮實作的。

### <a name="send-notifications"></a>傳送通知
hello 通知物件只是標頭與本文，某些公用程式方法來協助建立 hello 原生和範本通知的物件。

* **Windows 市集和 Windows Phone 8.1 (非 Silverlight)**
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* **iOS**
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* **Android**
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* **Windows Phone 8.0 和 8.1 Silverlight**
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* **Kindle Fire**
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* **傳送 tooTags**
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* **傳送 tootag 運算式**       
  
        hub.sendNotification(n, "foo && ! bar");
* **傳送範本通知**
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

執行 Java 程式碼現在應會產生一則顯示於目標裝置的通知。

## <a name="next-steps"></a>後續步驟
本主題中我們也示範了如何 toocreate 簡單 Java 將通知中樞的用戶端。 您可以在這裡執行下列動作：

* 下載完整的 hello [Java SDK]，其中包含 hello 整個 SDK 程式碼。 
* 也使用 hello 範例：
  * [開始使用通知中心]
  * [傳送即時新聞]
  * [傳送當地語系化的即時新聞]
  * [傳送通知給 tooauthenticated 使用者]
  * [傳送跨平台通知 tooauthenticated 使用者]

[Java SDK]: https://github.com/Azure/azure-notificationhubs-java-backend
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[開始使用通知中心]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/
[傳送即時新聞]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/
[傳送當地語系化的即時新聞]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/
[傳送通知給 tooauthenticated 使用者]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/
[傳送跨平台通知 tooauthenticated 使用者]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/
[Maven]: http://maven.apache.org/

