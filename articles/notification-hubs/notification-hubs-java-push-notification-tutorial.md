---
title: "如何搭配使用通知中樞與 Java"
description: "了解如何從 Java 後端使用 Azure 通知中樞。"
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
ms.openlocfilehash: 41f978750ddef9f7e878c65b0017e909720154aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-notification-hubs-from-java"></a><span data-ttu-id="4de4d-103">如何從 Java 使用通知中樞</span><span class="sxs-lookup"><span data-stu-id="4de4d-103">How to use Notification Hubs from Java</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="4de4d-104">本主題說明最新完整支援的官方 Azure 通知中樞 Java SDK 有哪些主要功能。</span><span class="sxs-lookup"><span data-stu-id="4de4d-104">This topic describes the key features of the new fully supported official Azure Notification Hub Java SDK.</span></span> <span data-ttu-id="4de4d-105">這是開放原始碼專案，您可以在 [Java SDK]中檢視完整的 SDK 程式碼。</span><span class="sxs-lookup"><span data-stu-id="4de4d-105">This is an open source project and you can view the entire SDK code at [Java SDK].</span></span> 

<span data-ttu-id="4de4d-106">一般而言，您可以使用通知中樞 REST 介面，來存取 Java/PHP/Python/Ruby 後端的所有通知中樞功能，如 MSDN 主題 [通知中樞 REST API](http://msdn.microsoft.com/library/dn223264.aspx)中所述。</span><span class="sxs-lookup"><span data-stu-id="4de4d-106">In general, you can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span> <span data-ttu-id="4de4d-107">此 Java SDK 透過 Java 中的這些 REST 介面提供了精簡型包裝函式。</span><span class="sxs-lookup"><span data-stu-id="4de4d-107">This Java SDK provides a thin wrapper over these REST interfaces in Java.</span></span> 

<span data-ttu-id="4de4d-108">SDK 目前支援：</span><span class="sxs-lookup"><span data-stu-id="4de4d-108">The SDK supports currently:</span></span>

* <span data-ttu-id="4de4d-109">通知中樞的 CRUD</span><span class="sxs-lookup"><span data-stu-id="4de4d-109">CRUD on Notification Hubs</span></span> 
* <span data-ttu-id="4de4d-110">註冊的 CRUD</span><span class="sxs-lookup"><span data-stu-id="4de4d-110">CRUD on Registrations</span></span>
* <span data-ttu-id="4de4d-111">安裝管理</span><span class="sxs-lookup"><span data-stu-id="4de4d-111">Installation Management</span></span>
* <span data-ttu-id="4de4d-112">匯入/匯出註冊</span><span class="sxs-lookup"><span data-stu-id="4de4d-112">Import/Export Registrations</span></span>
* <span data-ttu-id="4de4d-113">定期傳送</span><span class="sxs-lookup"><span data-stu-id="4de4d-113">Regular Sends</span></span>
* <span data-ttu-id="4de4d-114">排程的傳送</span><span class="sxs-lookup"><span data-stu-id="4de4d-114">Scheduled Sends</span></span>
* <span data-ttu-id="4de4d-115">透過 Java NIO 的非同步作業</span><span class="sxs-lookup"><span data-stu-id="4de4d-115">Async operations via Java NIO</span></span>
* <span data-ttu-id="4de4d-116">受支援的平台：APNS (iOS)、GCM (Android)、WNS (Windows 市集應用程式)、MPNS (Windows Phone)、ADM (Amazon Kindle Fire)、Baidu (沒有 Google 服務的 Android)</span><span class="sxs-lookup"><span data-stu-id="4de4d-116">Supported platforms: APNS (iOS), GCM (Android), WNS (Windows Store apps), MPNS(Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android without Google services)</span></span> 

## <a name="sdk-usage"></a><span data-ttu-id="4de4d-117">SDK 的使用方式</span><span class="sxs-lookup"><span data-stu-id="4de4d-117">SDK Usage</span></span>
### <a name="compile-and-build"></a><span data-ttu-id="4de4d-118">編譯和建置</span><span class="sxs-lookup"><span data-stu-id="4de4d-118">Compile and build</span></span>
<span data-ttu-id="4de4d-119">使用 [Maven]</span><span class="sxs-lookup"><span data-stu-id="4de4d-119">Use [Maven]</span></span>

<span data-ttu-id="4de4d-120">若要建置：</span><span class="sxs-lookup"><span data-stu-id="4de4d-120">To build:</span></span>

    mvn package

## <a name="code"></a><span data-ttu-id="4de4d-121">代碼</span><span class="sxs-lookup"><span data-stu-id="4de4d-121">Code</span></span>
### <a name="notification-hub-cruds"></a><span data-ttu-id="4de4d-122">通知中樞 CRUD</span><span class="sxs-lookup"><span data-stu-id="4de4d-122">Notification Hub CRUDs</span></span>
<span data-ttu-id="4de4d-123">**建立 NamespaceManager：**</span><span class="sxs-lookup"><span data-stu-id="4de4d-123">**Create a NamespaceManager:**</span></span>

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

<span data-ttu-id="4de4d-124">**建立通知中樞：**</span><span class="sxs-lookup"><span data-stu-id="4de4d-124">**Create Notification Hub:**</span></span>

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 <span data-ttu-id="4de4d-125">或</span><span class="sxs-lookup"><span data-stu-id="4de4d-125">OR</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="4de4d-126">**取得通知中樞：**</span><span class="sxs-lookup"><span data-stu-id="4de4d-126">**Get Notification Hub:**</span></span>

    hub = namespaceManager.getNotificationHub("hubname");

<span data-ttu-id="4de4d-127">**更新通知中樞：**</span><span class="sxs-lookup"><span data-stu-id="4de4d-127">**Update Notification Hub:**</span></span>

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

<span data-ttu-id="4de4d-128">**刪除通知中樞：**</span><span class="sxs-lookup"><span data-stu-id="4de4d-128">**Delete Notification Hub:**</span></span>

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a><span data-ttu-id="4de4d-129">註冊 CRUD</span><span class="sxs-lookup"><span data-stu-id="4de4d-129">Registration CRUDs</span></span>
<span data-ttu-id="4de4d-130">**建立通知中樞用戶端：**</span><span class="sxs-lookup"><span data-stu-id="4de4d-130">**Create a Notification Hub client:**</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="4de4d-131">**建立 Windows 註冊：**</span><span class="sxs-lookup"><span data-stu-id="4de4d-131">**Create Windows registration:**</span></span>

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

<span data-ttu-id="4de4d-132">**建立 iOS 註冊：**</span><span class="sxs-lookup"><span data-stu-id="4de4d-132">**Create iOS registration:**</span></span>

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

<span data-ttu-id="4de4d-133">同樣地，您可以建立 Android (GCM)、Windows Phone (MPNS) 和 Kindle Fire (ADM) 的註冊。</span><span class="sxs-lookup"><span data-stu-id="4de4d-133">Similarly you can create registrations for Android (GCM), Windows Phone (MPNS), and Kindle Fire (ADM).</span></span>

<span data-ttu-id="4de4d-134">**建立範本註冊：**</span><span class="sxs-lookup"><span data-stu-id="4de4d-134">**Create template registrations:**</span></span>

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

<span data-ttu-id="4de4d-135">**使用建立 registrationid + upsert 模式來建立註冊**</span><span class="sxs-lookup"><span data-stu-id="4de4d-135">**Create registrations using create registrationid + upsert pattern**</span></span>

<span data-ttu-id="4de4d-136">如果將註冊識別碼儲存在裝置上，請在發生任何遺失回應時移除複本：</span><span class="sxs-lookup"><span data-stu-id="4de4d-136">Removes duplicates due to any lost responses if storing registration ids on the device:</span></span>

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

<span data-ttu-id="4de4d-137">**更新註冊：**</span><span class="sxs-lookup"><span data-stu-id="4de4d-137">**Update registrations:**</span></span>

    hub.updateRegistration(reg);

<span data-ttu-id="4de4d-138">**刪除註冊：**</span><span class="sxs-lookup"><span data-stu-id="4de4d-138">**Delete registrations:**</span></span>

    hub.deleteRegistration(regid);

<span data-ttu-id="4de4d-139">**查詢註冊：**</span><span class="sxs-lookup"><span data-stu-id="4de4d-139">**Query registrations:**</span></span>

* <span data-ttu-id="4de4d-140">**取得單一註冊：**</span><span class="sxs-lookup"><span data-stu-id="4de4d-140">**Get single registration:**</span></span>
  
    <span data-ttu-id="4de4d-141">hub.getRegistration(regid);</span><span class="sxs-lookup"><span data-stu-id="4de4d-141">hub.getRegistration(regid);</span></span>
* <span data-ttu-id="4de4d-142">**取得中樞的所有註冊：**</span><span class="sxs-lookup"><span data-stu-id="4de4d-142">**Get all registrations in hub:**</span></span>
  
    <span data-ttu-id="4de4d-143">hub.getRegistrations();</span><span class="sxs-lookup"><span data-stu-id="4de4d-143">hub.getRegistrations();</span></span>
* <span data-ttu-id="4de4d-144">**取得具有標籤的註冊：**</span><span class="sxs-lookup"><span data-stu-id="4de4d-144">**Get registrations with tag:**</span></span>
  
    <span data-ttu-id="4de4d-145">hub.getRegistrationsByTag("myTag");</span><span class="sxs-lookup"><span data-stu-id="4de4d-145">hub.getRegistrationsByTag("myTag");</span></span>
* <span data-ttu-id="4de4d-146">**依通道取得註冊：**</span><span class="sxs-lookup"><span data-stu-id="4de4d-146">**Get registrations by channel:**</span></span>
  
    <span data-ttu-id="4de4d-147">hub.getRegistrationsByChannel("devicetoken");</span><span class="sxs-lookup"><span data-stu-id="4de4d-147">hub.getRegistrationsByChannel("devicetoken");</span></span>

<span data-ttu-id="4de4d-148">所有集合查詢都支援 $top 和接續權杖。</span><span class="sxs-lookup"><span data-stu-id="4de4d-148">All collection queries support $top and continuation tokens.</span></span>

### <a name="installation-api-usage"></a><span data-ttu-id="4de4d-149">安裝 API 的使用方式</span><span class="sxs-lookup"><span data-stu-id="4de4d-149">Installation API usage</span></span>
<span data-ttu-id="4de4d-150">安裝 API 是註冊管理的替代機制。</span><span class="sxs-lookup"><span data-stu-id="4de4d-150">Installation API is an alternative mechanism for registration management.</span></span> <span data-ttu-id="4de4d-151">要維護多個註冊並非易事，並且可能容易出錯或效率低落，但現在您已可以使用單一安裝物件。</span><span class="sxs-lookup"><span data-stu-id="4de4d-151">Instead of maintaining multiple registrations which is not trivial and may be easily done wrongly or inefficiently, it is now possible to use a SINGLE Installation object.</span></span> <span data-ttu-id="4de4d-152">安裝包含所需的一切：推播通道 (裝置權杖)、標籤、範本、次要磚 (適用於 WNS 和 APNS)。</span><span class="sxs-lookup"><span data-stu-id="4de4d-152">Installation contains everything you need: push channel (device token), tags, templates, secondary tiles (for WNS and APNS).</span></span> <span data-ttu-id="4de4d-153">現在您無須呼叫服務即可取得識別碼 - 只要產生 GUID 或任何其他識別碼、將它保存在裝置上，並透過推播通道傳送至您的後端 (裝置權杖) 即可。</span><span class="sxs-lookup"><span data-stu-id="4de4d-153">You don't need to call the service to get Id anymore - just generate GUID or any other identifier, keep it on device and send to your backend together with push channel (device token).</span></span> <span data-ttu-id="4de4d-154">您只能在後端執行單一呼叫：CreateOrUpdateInstallation，它是完全等冪的，因此您可以儘管在必要時重試。</span><span class="sxs-lookup"><span data-stu-id="4de4d-154">On the backend you should only do a single call: CreateOrUpdateInstallation, it is fully idempotent, so feel free to retry if needed.</span></span>

<span data-ttu-id="4de4d-155">以 Amazon Kindle Fire 為例，將如下所示：</span><span class="sxs-lookup"><span data-stu-id="4de4d-155">As example for Amazon Kindle Fire it looks like this:</span></span>

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="4de4d-156">如果您想要加以更新：</span><span class="sxs-lookup"><span data-stu-id="4de4d-156">If you want to update it:</span></span> 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="4de4d-157">在進階案例中，我們提供了部分更新功能，僅允許使用者對安裝物件的特定屬性進行修改。</span><span class="sxs-lookup"><span data-stu-id="4de4d-157">For advanced scenarios we have partial update capability which allows to modify only particular properties of the installation object.</span></span> <span data-ttu-id="4de4d-158">基本上，部分更新是您可以對安裝物件執行的 JSON Patch 作業子集。</span><span class="sxs-lookup"><span data-stu-id="4de4d-158">Basically partial update is subset of JSON Patch operations you can run against Installation object.</span></span>

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

<span data-ttu-id="4de4d-159">刪除安裝：</span><span class="sxs-lookup"><span data-stu-id="4de4d-159">Delete Installation:</span></span>

    hub.deleteInstallation(installation.getInstallationId());

<span data-ttu-id="4de4d-160">CreateOrUpdate、Patch 和 Delete 最終都會與 Get 一致。</span><span class="sxs-lookup"><span data-stu-id="4de4d-160">CreateOrUpdate, Patch and Delete are eventually consistent with Get.</span></span> <span data-ttu-id="4de4d-161">您要求的作業只會在呼叫期間進入系統佇列，並會在背景中執行。</span><span class="sxs-lookup"><span data-stu-id="4de4d-161">Your requested operation just goes to the system queue during the call and will be executed in background.</span></span> <span data-ttu-id="4de4d-162">請注意，Get 不是針對主要執行階段案例而設計的，而是專門用於偵錯和疑難排解的目的，因此受到服務嚴格的節流。</span><span class="sxs-lookup"><span data-stu-id="4de4d-162">Note that Get is not designed for main runtime scenario but just for debug and troubleshooting purposes, it is tightly throttled by the service.</span></span>

<span data-ttu-id="4de4d-163">安裝的傳送流量與註冊相同。</span><span class="sxs-lookup"><span data-stu-id="4de4d-163">Send flow for Installations is the same as for Registrations.</span></span> <span data-ttu-id="4de4d-164">我們僅介紹以特定安裝的通知為目標的選項 - 僅使用標籤 "InstallationId:{desired-id}"。</span><span class="sxs-lookup"><span data-stu-id="4de4d-164">We've just introduced an option to target notification to the particular Installation - just use tag "InstallationId:{desired-id}".</span></span> <span data-ttu-id="4de4d-165">就上述案例而言，將如下所示：</span><span class="sxs-lookup"><span data-stu-id="4de4d-165">For case above it would look like this:</span></span>

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

<span data-ttu-id="4de4d-166">數個範本之一：</span><span class="sxs-lookup"><span data-stu-id="4de4d-166">For one of several templates:</span></span>

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a><span data-ttu-id="4de4d-167">排程通知 (適用於 STANDARD 層)</span><span class="sxs-lookup"><span data-stu-id="4de4d-167">Schedule Notifications (available for STANDARD Tier)</span></span>
<span data-ttu-id="4de4d-168">與定期傳送相同，但使用了一個額外參數 scheduledTime，指出何時應傳遞通知。</span><span class="sxs-lookup"><span data-stu-id="4de4d-168">The same as regular send but with one additional parameter - scheduledTime which says when notification should be delivered.</span></span> <span data-ttu-id="4de4d-169">服務可接受目前 + 5 分鐘與目前 + 7 天之間的任何時間點。</span><span class="sxs-lookup"><span data-stu-id="4de4d-169">Service accepts any point of time between now + 5 minutes and now + 7 days.</span></span>

<span data-ttu-id="4de4d-170">**排程 Windows 原生通知：**</span><span class="sxs-lookup"><span data-stu-id="4de4d-170">**Schedule a Windows native notification:**</span></span>

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a><span data-ttu-id="4de4d-171">匯入/匯出 (適用於 STANDARD 層)</span><span class="sxs-lookup"><span data-stu-id="4de4d-171">Import/Export (available for STANDARD Tier)</span></span>
<span data-ttu-id="4de4d-172">有時候您需要對註冊執行大量作業。</span><span class="sxs-lookup"><span data-stu-id="4de4d-172">Sometimes it is required to perform bulk operation against registrations.</span></span> <span data-ttu-id="4de4d-173">通常這是為了與另一個系統整合，或是要進行大規模修正，例如更新標籤。</span><span class="sxs-lookup"><span data-stu-id="4de4d-173">Usually it is for integration with another system or just a massive fix to say update the tags.</span></span> <span data-ttu-id="4de4d-174">如果註冊數高達數千個，強烈建議您不要使用 Get/Update 流程。</span><span class="sxs-lookup"><span data-stu-id="4de4d-174">It is strongly not recommended to use Get/Update flow if we are talking about thousands of registrations.</span></span> <span data-ttu-id="4de4d-175">匯入/匯出功能可因應此案例。</span><span class="sxs-lookup"><span data-stu-id="4de4d-175">Import/Export capability is designed to cover the scenario.</span></span> <span data-ttu-id="4de4d-176">基本上，您會在儲存體帳戶提供對某個 Blob 容器的的存取權，做為內送資料的來源和輸出的位置。</span><span class="sxs-lookup"><span data-stu-id="4de4d-176">Basically you provide an access to some blob container under your storage account as a source of incoming data and location for output.</span></span>

<span data-ttu-id="4de4d-177">**提交匯出工作：**</span><span class="sxs-lookup"><span data-stu-id="4de4d-177">**Submit export job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


<span data-ttu-id="4de4d-178">**提交匯入工作：**</span><span class="sxs-lookup"><span data-stu-id="4de4d-178">**Submit import job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

<span data-ttu-id="4de4d-179">**等到工作完成：**</span><span class="sxs-lookup"><span data-stu-id="4de4d-179">**Wait until job is done:**</span></span>

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

<span data-ttu-id="4de4d-180">**取得所有工作：**</span><span class="sxs-lookup"><span data-stu-id="4de4d-180">**Get all jobs:**</span></span>

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

<span data-ttu-id="4de4d-181">**具備 SAS 簽章的 URI：** 這是某個 Blob 檔案或 Blob 容器的 URL，加上參數集 (例如權限和到期時間)，再加上所有使用帳戶 SAS 金鑰之項目的簽章。</span><span class="sxs-lookup"><span data-stu-id="4de4d-181">**URI with SAS signature:** This is the URL of some blob file or blob container plus set of parameters like permissions and expiration time plus signature of all these things made using account's SAS key.</span></span> <span data-ttu-id="4de4d-182">Azure Storage Java SDK 具有豐富的功能，包括建立此類的 URI。</span><span class="sxs-lookup"><span data-stu-id="4de4d-182">Azure Storage Java SDK has rich capabilities including creation of such kind of URIs.</span></span> <span data-ttu-id="4de4d-183">此外您可以參考 ImportExportE2E 測試類別 (從 github 位置) 的簡單替代方法，它可實作非常基本而精簡的簽署演算法。</span><span class="sxs-lookup"><span data-stu-id="4de4d-183">As simple alternative you can take a look at ImportExportE2E test class (from the github location) which has very basic and compact implementation of signing algorithm.</span></span>

### <a name="send-notifications"></a><span data-ttu-id="4de4d-184">傳送通知</span><span class="sxs-lookup"><span data-stu-id="4de4d-184">Send Notifications</span></span>
<span data-ttu-id="4de4d-185">通知物件是附有標頭的本文，某些公用程式方法有助於建立原生和範本通知物件。</span><span class="sxs-lookup"><span data-stu-id="4de4d-185">The Notification object is simply a body with headers, some utility methods help in building the native and template notifications objects.</span></span>

* <span data-ttu-id="4de4d-186">**Windows 市集和 Windows Phone 8.1 (非 Silverlight)**</span><span class="sxs-lookup"><span data-stu-id="4de4d-186">**Windows Store and Windows Phone 8.1 (non-Silverlight)**</span></span>
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="4de4d-187">**iOS**</span><span class="sxs-lookup"><span data-stu-id="4de4d-187">**iOS**</span></span>
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* <span data-ttu-id="4de4d-188">**Android**</span><span class="sxs-lookup"><span data-stu-id="4de4d-188">**Android**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="4de4d-189">**Windows Phone 8.0 和 8.1 Silverlight**</span><span class="sxs-lookup"><span data-stu-id="4de4d-189">**Windows Phone 8.0 and 8.1 Silverlight**</span></span>
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="4de4d-190">**Kindle Fire**</span><span class="sxs-lookup"><span data-stu-id="4de4d-190">**Kindle Fire**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="4de4d-191">**傳送至標籤**</span><span class="sxs-lookup"><span data-stu-id="4de4d-191">**Send to Tags**</span></span>
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* <span data-ttu-id="4de4d-192">**傳送至標籤運算式**</span><span class="sxs-lookup"><span data-stu-id="4de4d-192">**Send to tag expression**</span></span>       
  
        hub.sendNotification(n, "foo && ! bar");
* <span data-ttu-id="4de4d-193">**傳送範本通知**</span><span class="sxs-lookup"><span data-stu-id="4de4d-193">**Send template notification**</span></span>
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

<span data-ttu-id="4de4d-194">執行 Java 程式碼現在應會產生一則顯示於目標裝置的通知。</span><span class="sxs-lookup"><span data-stu-id="4de4d-194">Running your Java code should now produce a notification appearing on your target device.</span></span>

## <span data-ttu-id="4de4d-195"><a name="next-steps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="4de4d-195"><a name="next-steps"></a>Next Steps</span></span>
<span data-ttu-id="4de4d-196">在本主題中，我們會說明如何為通知中心建立簡單的 Java REST 用戶端。</span><span class="sxs-lookup"><span data-stu-id="4de4d-196">In this topic we showed how to create a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="4de4d-197">您可以在這裡執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="4de4d-197">From here you can:</span></span>

* <span data-ttu-id="4de4d-198">下載完整的 [Java SDK]，其中包含完整的 SDK 程式碼。</span><span class="sxs-lookup"><span data-stu-id="4de4d-198">Download the full [Java SDK], which contains the entire SDK code.</span></span> 
* <span data-ttu-id="4de4d-199">試用範例：</span><span class="sxs-lookup"><span data-stu-id="4de4d-199">Play with the samples:</span></span>
  * <span data-ttu-id="4de4d-200">[開始使用通知中樞]</span><span class="sxs-lookup"><span data-stu-id="4de4d-200">[Get Started with Notification Hubs]</span></span>
  * <span data-ttu-id="4de4d-201">[傳送即時新聞]</span><span class="sxs-lookup"><span data-stu-id="4de4d-201">[Send breaking news]</span></span>
  * <span data-ttu-id="4de4d-202">[傳送當地語系化的即時新聞]</span><span class="sxs-lookup"><span data-stu-id="4de4d-202">[Send localized breaking news]</span></span>
  * <span data-ttu-id="4de4d-203">[傳送通知給已驗證的使用者]</span><span class="sxs-lookup"><span data-stu-id="4de4d-203">[Send notifications to authenticated users]</span></span>
  * <span data-ttu-id="4de4d-204">[傳送跨平台通知給已驗證的使用者]</span><span class="sxs-lookup"><span data-stu-id="4de4d-204">[Send cross-platform notifications to authenticated users]</span></span>

<span data-ttu-id="4de4d-205">[Java SDK]: https://github.com/Azure/azure-notificationhubs-java-backend</span><span class="sxs-lookup"><span data-stu-id="4de4d-205">[Java SDK]: https://github.com/Azure/azure-notificationhubs-java-backend</span></span>
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
<span data-ttu-id="4de4d-206">[開始使用通知中樞]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/</span><span class="sxs-lookup"><span data-stu-id="4de4d-206">[Get Started with Notification Hubs]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/</span></span>
<span data-ttu-id="4de4d-207">[傳送即時新聞]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/</span><span class="sxs-lookup"><span data-stu-id="4de4d-207">[Send breaking news]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/</span></span>
<span data-ttu-id="4de4d-208">[傳送當地語系化的即時新聞]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/</span><span class="sxs-lookup"><span data-stu-id="4de4d-208">[Send localized breaking news]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/</span></span>
<span data-ttu-id="4de4d-209">[傳送通知給已驗證的使用者]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/</span><span class="sxs-lookup"><span data-stu-id="4de4d-209">[Send notifications to authenticated users]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/</span></span>
<span data-ttu-id="4de4d-210">[傳送跨平台通知給已驗證的使用者]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/</span><span class="sxs-lookup"><span data-stu-id="4de4d-210">[Send cross-platform notifications to authenticated users]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/</span></span>
<span data-ttu-id="4de4d-211">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="4de4d-211">[Maven]: http://maven.apache.org/</span></span>

