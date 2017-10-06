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
# <a name="how-toouse-notification-hubs-from-java"></a><span data-ttu-id="1c1aa-103">如何從 Java 的通知中樞 toouse</span><span class="sxs-lookup"><span data-stu-id="1c1aa-103">How toouse Notification Hubs from Java</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="1c1aa-104">本主題描述 hello 的主要功能，完全支援 hello 新官方 Azure 通知中樞 Java SDK。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-104">This topic describes hello key features of hello new fully supported official Azure Notification Hub Java SDK.</span></span> <span data-ttu-id="1c1aa-105">這是開放原始碼專案，您可以檢視 hello 整個 SDK 程式碼中的[Java SDK]。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-105">This is an open source project and you can view hello entire SDK code at [Java SDK].</span></span> 

<span data-ttu-id="1c1aa-106">一般情況下，您可以從 Java/PHP/Python/Ruby 後端存取所有通知中樞功能 hello MSDN 主題中所述，使用 hello 通知中樞 REST 介面[通知中心 REST Api](http://msdn.microsoft.com/library/dn223264.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-106">In general, you can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span> <span data-ttu-id="1c1aa-107">此 Java SDK 透過 Java 中的這些 REST 介面提供了精簡型包裝函式。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-107">This Java SDK provides a thin wrapper over these REST interfaces in Java.</span></span> 

<span data-ttu-id="1c1aa-108">hello SDK 支援目前：</span><span class="sxs-lookup"><span data-stu-id="1c1aa-108">hello SDK supports currently:</span></span>

* <span data-ttu-id="1c1aa-109">通知中樞的 CRUD</span><span class="sxs-lookup"><span data-stu-id="1c1aa-109">CRUD on Notification Hubs</span></span> 
* <span data-ttu-id="1c1aa-110">註冊的 CRUD</span><span class="sxs-lookup"><span data-stu-id="1c1aa-110">CRUD on Registrations</span></span>
* <span data-ttu-id="1c1aa-111">安裝管理</span><span class="sxs-lookup"><span data-stu-id="1c1aa-111">Installation Management</span></span>
* <span data-ttu-id="1c1aa-112">匯入/匯出註冊</span><span class="sxs-lookup"><span data-stu-id="1c1aa-112">Import/Export Registrations</span></span>
* <span data-ttu-id="1c1aa-113">定期傳送</span><span class="sxs-lookup"><span data-stu-id="1c1aa-113">Regular Sends</span></span>
* <span data-ttu-id="1c1aa-114">排程的傳送</span><span class="sxs-lookup"><span data-stu-id="1c1aa-114">Scheduled Sends</span></span>
* <span data-ttu-id="1c1aa-115">透過 Java NIO 的非同步作業</span><span class="sxs-lookup"><span data-stu-id="1c1aa-115">Async operations via Java NIO</span></span>
* <span data-ttu-id="1c1aa-116">受支援的平台：APNS (iOS)、GCM (Android)、WNS (Windows 市集應用程式)、MPNS (Windows Phone)、ADM (Amazon Kindle Fire)、Baidu (沒有 Google 服務的 Android)</span><span class="sxs-lookup"><span data-stu-id="1c1aa-116">Supported platforms: APNS (iOS), GCM (Android), WNS (Windows Store apps), MPNS(Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android without Google services)</span></span> 

## <a name="sdk-usage"></a><span data-ttu-id="1c1aa-117">SDK 的使用方式</span><span class="sxs-lookup"><span data-stu-id="1c1aa-117">SDK Usage</span></span>
### <a name="compile-and-build"></a><span data-ttu-id="1c1aa-118">編譯和建置</span><span class="sxs-lookup"><span data-stu-id="1c1aa-118">Compile and build</span></span>
<span data-ttu-id="1c1aa-119">使用 [Maven]</span><span class="sxs-lookup"><span data-stu-id="1c1aa-119">Use [Maven]</span></span>

<span data-ttu-id="1c1aa-120">toobuild:</span><span class="sxs-lookup"><span data-stu-id="1c1aa-120">toobuild:</span></span>

    mvn package

## <a name="code"></a><span data-ttu-id="1c1aa-121">代碼</span><span class="sxs-lookup"><span data-stu-id="1c1aa-121">Code</span></span>
### <a name="notification-hub-cruds"></a><span data-ttu-id="1c1aa-122">通知中樞 CRUD</span><span class="sxs-lookup"><span data-stu-id="1c1aa-122">Notification Hub CRUDs</span></span>
<span data-ttu-id="1c1aa-123">**建立 NamespaceManager：**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-123">**Create a NamespaceManager:**</span></span>

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

<span data-ttu-id="1c1aa-124">**建立通知中樞：**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-124">**Create Notification Hub:**</span></span>

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 <span data-ttu-id="1c1aa-125">或</span><span class="sxs-lookup"><span data-stu-id="1c1aa-125">OR</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="1c1aa-126">**取得通知中樞：**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-126">**Get Notification Hub:**</span></span>

    hub = namespaceManager.getNotificationHub("hubname");

<span data-ttu-id="1c1aa-127">**更新通知中樞：**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-127">**Update Notification Hub:**</span></span>

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

<span data-ttu-id="1c1aa-128">**刪除通知中樞：**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-128">**Delete Notification Hub:**</span></span>

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a><span data-ttu-id="1c1aa-129">註冊 CRUD</span><span class="sxs-lookup"><span data-stu-id="1c1aa-129">Registration CRUDs</span></span>
<span data-ttu-id="1c1aa-130">**建立通知中樞用戶端：**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-130">**Create a Notification Hub client:**</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="1c1aa-131">**建立 Windows 註冊：**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-131">**Create Windows registration:**</span></span>

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

<span data-ttu-id="1c1aa-132">**建立 iOS 註冊：**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-132">**Create iOS registration:**</span></span>

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

<span data-ttu-id="1c1aa-133">同樣地，您可以建立 Android (GCM)、Windows Phone (MPNS) 和 Kindle Fire (ADM) 的註冊。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-133">Similarly you can create registrations for Android (GCM), Windows Phone (MPNS), and Kindle Fire (ADM).</span></span>

<span data-ttu-id="1c1aa-134">**建立範本註冊：**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-134">**Create template registrations:**</span></span>

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

<span data-ttu-id="1c1aa-135">**使用建立 registrationid + upsert 模式來建立註冊**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-135">**Create registrations using create registrationid + upsert pattern**</span></span>

<span data-ttu-id="1c1aa-136">如果 hello 裝置上儲存註冊識別碼，請移除重複項目，因為遺失 tooany 回應：</span><span class="sxs-lookup"><span data-stu-id="1c1aa-136">Removes duplicates due tooany lost responses if storing registration ids on hello device:</span></span>

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

<span data-ttu-id="1c1aa-137">**更新註冊：**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-137">**Update registrations:**</span></span>

    hub.updateRegistration(reg);

<span data-ttu-id="1c1aa-138">**刪除註冊：**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-138">**Delete registrations:**</span></span>

    hub.deleteRegistration(regid);

<span data-ttu-id="1c1aa-139">**查詢註冊：**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-139">**Query registrations:**</span></span>

* <span data-ttu-id="1c1aa-140">**取得單一註冊：**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-140">**Get single registration:**</span></span>
  
    <span data-ttu-id="1c1aa-141">hub.getRegistration(regid);</span><span class="sxs-lookup"><span data-stu-id="1c1aa-141">hub.getRegistration(regid);</span></span>
* <span data-ttu-id="1c1aa-142">**取得中樞的所有註冊：**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-142">**Get all registrations in hub:**</span></span>
  
    <span data-ttu-id="1c1aa-143">hub.getRegistrations();</span><span class="sxs-lookup"><span data-stu-id="1c1aa-143">hub.getRegistrations();</span></span>
* <span data-ttu-id="1c1aa-144">**取得具有標籤的註冊：**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-144">**Get registrations with tag:**</span></span>
  
    <span data-ttu-id="1c1aa-145">hub.getRegistrationsByTag("myTag");</span><span class="sxs-lookup"><span data-stu-id="1c1aa-145">hub.getRegistrationsByTag("myTag");</span></span>
* <span data-ttu-id="1c1aa-146">**依通道取得註冊：**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-146">**Get registrations by channel:**</span></span>
  
    <span data-ttu-id="1c1aa-147">hub.getRegistrationsByChannel("devicetoken");</span><span class="sxs-lookup"><span data-stu-id="1c1aa-147">hub.getRegistrationsByChannel("devicetoken");</span></span>

<span data-ttu-id="1c1aa-148">所有集合查詢都支援 $top 和接續權杖。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-148">All collection queries support $top and continuation tokens.</span></span>

### <a name="installation-api-usage"></a><span data-ttu-id="1c1aa-149">安裝 API 的使用方式</span><span class="sxs-lookup"><span data-stu-id="1c1aa-149">Installation API usage</span></span>
<span data-ttu-id="1c1aa-150">安裝 API 是註冊管理的替代機制。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-150">Installation API is an alternative mechanism for registration management.</span></span> <span data-ttu-id="1c1aa-151">而不是維護多個註冊並非易事，且可能在錯誤或無效率地輕鬆完成，它現在是可能 toouse 單一安裝物件。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-151">Instead of maintaining multiple registrations which is not trivial and may be easily done wrongly or inefficiently, it is now possible toouse a SINGLE Installation object.</span></span> <span data-ttu-id="1c1aa-152">安裝包含所需的一切：推播通道 (裝置權杖)、標籤、範本、次要磚 (適用於 WNS 和 APNS)。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-152">Installation contains everything you need: push channel (device token), tags, templates, secondary tiles (for WNS and APNS).</span></span> <span data-ttu-id="1c1aa-153">您不再需要 toocall hello 服務 tooget 識別碼-只產生 GUID 或任何其他識別項、 將它保留在裝置上並傳送推播通道 （裝置權杖） 以及 tooyour 後的端。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-153">You don't need toocall hello service tooget Id anymore - just generate GUID or any other identifier, keep it on device and send tooyour backend together with push channel (device token).</span></span> <span data-ttu-id="1c1aa-154">在 hello 後端，您應該只執行單一呼叫： CreateOrUpdateInstallation，它完全是等冪，所以您可以免費 tooretry 視。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-154">On hello backend you should only do a single call: CreateOrUpdateInstallation, it is fully idempotent, so feel free tooretry if needed.</span></span>

<span data-ttu-id="1c1aa-155">以 Amazon Kindle Fire 為例，將如下所示：</span><span class="sxs-lookup"><span data-stu-id="1c1aa-155">As example for Amazon Kindle Fire it looks like this:</span></span>

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="1c1aa-156">如果您想 tooupdate 它：</span><span class="sxs-lookup"><span data-stu-id="1c1aa-156">If you want tooupdate it:</span></span> 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="1c1aa-157">在進階案例中，我們有部分更新功能可讓 toomodify hello 安裝物件的只有特定的屬性。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-157">For advanced scenarios we have partial update capability which allows toomodify only particular properties of hello installation object.</span></span> <span data-ttu-id="1c1aa-158">基本上，部分更新是您可以對安裝物件執行的 JSON Patch 作業子集。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-158">Basically partial update is subset of JSON Patch operations you can run against Installation object.</span></span>

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

<span data-ttu-id="1c1aa-159">刪除安裝：</span><span class="sxs-lookup"><span data-stu-id="1c1aa-159">Delete Installation:</span></span>

    hub.deleteInstallation(installation.getInstallationId());

<span data-ttu-id="1c1aa-160">CreateOrUpdate、Patch 和 Delete 最終都會與 Get 一致。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-160">CreateOrUpdate, Patch and Delete are eventually consistent with Get.</span></span> <span data-ttu-id="1c1aa-161">要求的作業只會 hello 呼叫期間會 toohello 系統佇列，而且會在背景中執行。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-161">Your requested operation just goes toohello system queue during hello call and will be executed in background.</span></span> <span data-ttu-id="1c1aa-162">請注意，取得不是主要的執行階段案例，但只針對偵錯和疑難排解的用途，hello 服務緊密節流。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-162">Note that Get is not designed for main runtime scenario but just for debug and troubleshooting purposes, it is tightly throttled by hello service.</span></span>

<span data-ttu-id="1c1aa-163">安裝的傳送流程註冊 hello 與相同。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-163">Send flow for Installations is hello same as for Registrations.</span></span> <span data-ttu-id="1c1aa-164">我們只導入選項 tootarget 通知 toohello 特定安裝-請使用標記"InstallationId: {預期-識別碼}"。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-164">We've just introduced an option tootarget notification toohello particular Installation - just use tag "InstallationId:{desired-id}".</span></span> <span data-ttu-id="1c1aa-165">就上述案例而言，將如下所示：</span><span class="sxs-lookup"><span data-stu-id="1c1aa-165">For case above it would look like this:</span></span>

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

<span data-ttu-id="1c1aa-166">數個範本之一：</span><span class="sxs-lookup"><span data-stu-id="1c1aa-166">For one of several templates:</span></span>

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a><span data-ttu-id="1c1aa-167">排程通知 (適用於 STANDARD 層)</span><span class="sxs-lookup"><span data-stu-id="1c1aa-167">Schedule Notifications (available for STANDARD Tier)</span></span>
<span data-ttu-id="1c1aa-168">為定期傳送，但具有一個額外的參數-scheduledTime 指出傳遞通知的時機，請 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-168">hello same as regular send but with one additional parameter - scheduledTime which says when notification should be delivered.</span></span> <span data-ttu-id="1c1aa-169">服務可接受目前 + 5 分鐘與目前 + 7 天之間的任何時間點。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-169">Service accepts any point of time between now + 5 minutes and now + 7 days.</span></span>

<span data-ttu-id="1c1aa-170">**排程 Windows 原生通知：**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-170">**Schedule a Windows native notification:**</span></span>

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a><span data-ttu-id="1c1aa-171">匯入/匯出 (適用於 STANDARD 層)</span><span class="sxs-lookup"><span data-stu-id="1c1aa-171">Import/Export (available for STANDARD Tier)</span></span>
<span data-ttu-id="1c1aa-172">有時會對登錄的必要的 tooperform 大量作業。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-172">Sometimes it is required tooperform bulk operation against registrations.</span></span> <span data-ttu-id="1c1aa-173">通常它是與另一個系統或只修正 massive toosay 更新 hello 標記的整合。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-173">Usually it is for integration with another system or just a massive fix toosay update hello tags.</span></span> <span data-ttu-id="1c1aa-174">如果我們說數千個註冊強烈不建議 toouse Get/更新流程。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-174">It is strongly not recommended toouse Get/Update flow if we are talking about thousands of registrations.</span></span> <span data-ttu-id="1c1aa-175">匯入/匯出功能是設計的 toocover hello 案例。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-175">Import/Export capability is designed toocover hello scenario.</span></span> <span data-ttu-id="1c1aa-176">基本上您提供存取 toosome blob 容器儲存體帳戶做為來源的連入的資料和輸出的位置。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-176">Basically you provide an access toosome blob container under your storage account as a source of incoming data and location for output.</span></span>

<span data-ttu-id="1c1aa-177">**提交匯出工作：**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-177">**Submit export job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


<span data-ttu-id="1c1aa-178">**提交匯入工作：**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-178">**Submit import job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

<span data-ttu-id="1c1aa-179">**等到工作完成：**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-179">**Wait until job is done:**</span></span>

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

<span data-ttu-id="1c1aa-180">**取得所有工作：**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-180">**Get all jobs:**</span></span>

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

<span data-ttu-id="1c1aa-181">**與 SAS 簽章 URI:**這是 hello 的部分 blob 檔案或 blob 容器的 URL，加上的權限和到期時間參數的集合再加上所有使用帳戶的 SAS 金鑰進行這些作業的簽章。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-181">**URI with SAS signature:** This is hello URL of some blob file or blob container plus set of parameters like permissions and expiration time plus signature of all these things made using account's SAS key.</span></span> <span data-ttu-id="1c1aa-182">Azure Storage Java SDK 具有豐富的功能，包括建立此類的 URI。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-182">Azure Storage Java SDK has rich capabilities including creation of such kind of URIs.</span></span> <span data-ttu-id="1c1aa-183">簡單的替代方法，您可查看 ImportExportE2E 測試類別 （來自 hello github 位置） 具有的簽章演算法非常基本和壓縮實作的。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-183">As simple alternative you can take a look at ImportExportE2E test class (from hello github location) which has very basic and compact implementation of signing algorithm.</span></span>

### <a name="send-notifications"></a><span data-ttu-id="1c1aa-184">傳送通知</span><span class="sxs-lookup"><span data-stu-id="1c1aa-184">Send Notifications</span></span>
<span data-ttu-id="1c1aa-185">hello 通知物件只是標頭與本文，某些公用程式方法來協助建立 hello 原生和範本通知的物件。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-185">hello Notification object is simply a body with headers, some utility methods help in building hello native and template notifications objects.</span></span>

* <span data-ttu-id="1c1aa-186">**Windows 市集和 Windows Phone 8.1 (非 Silverlight)**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-186">**Windows Store and Windows Phone 8.1 (non-Silverlight)**</span></span>
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="1c1aa-187">**iOS**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-187">**iOS**</span></span>
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* <span data-ttu-id="1c1aa-188">**Android**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-188">**Android**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="1c1aa-189">**Windows Phone 8.0 和 8.1 Silverlight**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-189">**Windows Phone 8.0 and 8.1 Silverlight**</span></span>
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="1c1aa-190">**Kindle Fire**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-190">**Kindle Fire**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="1c1aa-191">**傳送 tooTags**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-191">**Send tooTags**</span></span>
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* <span data-ttu-id="1c1aa-192">**傳送 tootag 運算式**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-192">**Send tootag expression**</span></span>       
  
        hub.sendNotification(n, "foo && ! bar");
* <span data-ttu-id="1c1aa-193">**傳送範本通知**</span><span class="sxs-lookup"><span data-stu-id="1c1aa-193">**Send template notification**</span></span>
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

<span data-ttu-id="1c1aa-194">執行 Java 程式碼現在應會產生一則顯示於目標裝置的通知。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-194">Running your Java code should now produce a notification appearing on your target device.</span></span>

## <span data-ttu-id="1c1aa-195"><a name="next-steps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="1c1aa-195"><a name="next-steps"></a>Next Steps</span></span>
<span data-ttu-id="1c1aa-196">本主題中我們也示範了如何 toocreate 簡單 Java 將通知中樞的用戶端。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-196">In this topic we showed how toocreate a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="1c1aa-197">您可以在這裡執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="1c1aa-197">From here you can:</span></span>

* <span data-ttu-id="1c1aa-198">下載完整的 hello [Java SDK]，其中包含 hello 整個 SDK 程式碼。</span><span class="sxs-lookup"><span data-stu-id="1c1aa-198">Download hello full [Java SDK], which contains hello entire SDK code.</span></span> 
* <span data-ttu-id="1c1aa-199">也使用 hello 範例：</span><span class="sxs-lookup"><span data-stu-id="1c1aa-199">Play with hello samples:</span></span>
  * <span data-ttu-id="1c1aa-200">[開始使用通知中心]</span><span class="sxs-lookup"><span data-stu-id="1c1aa-200">[Get Started with Notification Hubs]</span></span>
  * <span data-ttu-id="1c1aa-201">[傳送即時新聞]</span><span class="sxs-lookup"><span data-stu-id="1c1aa-201">[Send breaking news]</span></span>
  * <span data-ttu-id="1c1aa-202">[傳送當地語系化的即時新聞]</span><span class="sxs-lookup"><span data-stu-id="1c1aa-202">[Send localized breaking news]</span></span>
  * <span data-ttu-id="1c1aa-203">[傳送通知給 tooauthenticated 使用者]</span><span class="sxs-lookup"><span data-stu-id="1c1aa-203">[Send notifications tooauthenticated users]</span></span>
  * <span data-ttu-id="1c1aa-204">[傳送跨平台通知 tooauthenticated 使用者]</span><span class="sxs-lookup"><span data-stu-id="1c1aa-204">[Send cross-platform notifications tooauthenticated users]</span></span>

[Java SDK]: https://github.com/Azure/azure-notificationhubs-java-backend
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[開始使用通知中心]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/
[傳送即時新聞]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/
[傳送當地語系化的即時新聞]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/
[傳送通知給 tooauthenticated 使用者]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/
[傳送跨平台通知 tooauthenticated 使用者]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/
[Maven]: http://maven.apache.org/

