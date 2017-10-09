---
title: "aaaRegistration 管理"
description: "本主題說明如何 tooregister 裝置中順序 tooreceive 通知中樞推播通知。"
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: fd0ee230-132c-4143-b4f9-65cef7f463a1
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 76471a45c7a0da1614ceed82b73cdb3319979ff7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="registration-management"></a><span data-ttu-id="db201-103">註冊管理</span><span class="sxs-lookup"><span data-stu-id="db201-103">Registration management</span></span>
## <a name="overview"></a><span data-ttu-id="db201-104">概觀</span><span class="sxs-lookup"><span data-stu-id="db201-104">Overview</span></span>
<span data-ttu-id="db201-105">本主題說明如何 tooregister 裝置中順序 tooreceive 通知中樞推播通知。</span><span class="sxs-lookup"><span data-stu-id="db201-105">This topic explains how tooregister devices with notification hubs in order tooreceive push notifications.</span></span> <span data-ttu-id="db201-106">hello 主題描述註冊在高層級，然後介紹 hello 兩個主要模式註冊裝置： 註冊 hello 裝置從直接 toohello 通知中樞，並透過應用程式後端註冊。</span><span class="sxs-lookup"><span data-stu-id="db201-106">hello topic describes registrations at a high level, then introduces hello two main patterns for registering devices: registering from hello device directly toohello notification hub, and registering through an application backend.</span></span> 

## <a name="what-is-device-registration"></a><span data-ttu-id="db201-107">什麼是裝置註冊</span><span class="sxs-lookup"><span data-stu-id="db201-107">What is device registration</span></span>
<span data-ttu-id="db201-108">向「通知中樞」註冊裝置是藉由使用 [註冊] 或 [安裝] 來完成。</span><span class="sxs-lookup"><span data-stu-id="db201-108">Device registration with a Notification Hub is accomplished using a **Registration** or **Installation**.</span></span>

#### <a name="registrations"></a><span data-ttu-id="db201-109">註冊</span><span class="sxs-lookup"><span data-stu-id="db201-109">Registrations</span></span>
<span data-ttu-id="db201-110">註冊將的 hello 處理標記和可能的範本與裝置的平台通知服務 (PNS)。</span><span class="sxs-lookup"><span data-stu-id="db201-110">A registration associates hello Platform Notification Service (PNS) handle for a device with tags and possibly a template.</span></span> <span data-ttu-id="db201-111">hello PNS 控制代碼可能是 ChannelURI、 裝置權杖或 GCM 註冊識別碼。標記是使用的 tooroute 通知 toohello 一組正確的裝置控制代碼。</span><span class="sxs-lookup"><span data-stu-id="db201-111">hello PNS handle could be a ChannelURI, device token, or GCM registration id. Tags are used tooroute notifications toohello correct set of device handles.</span></span> <span data-ttu-id="db201-112">如需詳細資訊，請參閱 [路由與標記運算式](notification-hubs-tags-segment-push-message.md)。</span><span class="sxs-lookup"><span data-stu-id="db201-112">For more information, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span> <span data-ttu-id="db201-113">範本是使用的 tooimplement 註冊每個轉換。</span><span class="sxs-lookup"><span data-stu-id="db201-113">Templates are used tooimplement per-registration transformation.</span></span> <span data-ttu-id="db201-114">如需詳細資訊，請參閱 [範本](notification-hubs-templates-cross-platform-push-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="db201-114">For more information, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>

#### <a name="installations"></a><span data-ttu-id="db201-115">安裝</span><span class="sxs-lookup"><span data-stu-id="db201-115">Installations</span></span>
<span data-ttu-id="db201-116">安裝是增強型的註冊，包含一組推播相關的屬性。</span><span class="sxs-lookup"><span data-stu-id="db201-116">An Installation is an enhanced registration that includes a bag of push related properties.</span></span> <span data-ttu-id="db201-117">它是您的裝置 hello tooregistering 最新且最佳的方法。</span><span class="sxs-lookup"><span data-stu-id="db201-117">It is hello latest and best approach tooregistering your devices.</span></span> <span data-ttu-id="db201-118">不過，目前用戶端 .NET SDK([適用於後端作業的通知中樞 SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) 不支援此種安裝。</span><span class="sxs-lookup"><span data-stu-id="db201-118">However, it is not supported by client side .NET SDK ([Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) as of yet.</span></span>  <span data-ttu-id="db201-119">這表示如果您註冊從 hello 用戶端裝置本身，您就必須 toouse hello[通知中心 REST API](https://msdn.microsoft.com/library/mt621153.aspx)接近 toosupport 安裝。</span><span class="sxs-lookup"><span data-stu-id="db201-119">This means if you are registering from hello client device itself, you would have toouse hello [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx) approach toosupport installations.</span></span> <span data-ttu-id="db201-120">如果您使用後端服務，您應該能夠 toouse[後端作業的通知中樞 SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)。</span><span class="sxs-lookup"><span data-stu-id="db201-120">If you are using a backend service, you should be able toouse [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="db201-121">hello 下面是一些主要優點 toousing 安裝：</span><span class="sxs-lookup"><span data-stu-id="db201-121">hello following are some key advantages toousing installations:</span></span>

* <span data-ttu-id="db201-122">建立或更新安裝是完全等冪的。</span><span class="sxs-lookup"><span data-stu-id="db201-122">Creating or updating an installation is fully idempotent.</span></span> <span data-ttu-id="db201-123">因此您可以重試它，而不需顧慮重複註冊的情況。</span><span class="sxs-lookup"><span data-stu-id="db201-123">So you can retry it without any concerns about duplicate registrations.</span></span>
* <span data-ttu-id="db201-124">hello 安裝模型可輕鬆 toodo 個別推播通知的目標特定的裝置。</span><span class="sxs-lookup"><span data-stu-id="db201-124">hello installation model makes it easy toodo individual pushes - targeting specific device.</span></span> <span data-ttu-id="db201-125">在每個安裝型註冊，都會自動新增一個系統標記 **"$InstallationId:[installationId]"** 。</span><span class="sxs-lookup"><span data-stu-id="db201-125">A system tag **"$InstallationId:[installationId]"** is automatically added with each installation based registration.</span></span> <span data-ttu-id="db201-126">因此您可以呼叫傳送 toothis 標記 tootarget 特定裝置而不需要任何額外的程式碼 toodo。</span><span class="sxs-lookup"><span data-stu-id="db201-126">So you can call a send toothis tag tootarget a specific device without having toodo any additional coding.</span></span>
* <span data-ttu-id="db201-127">使用安裝時，也可讓您 toodo 部分登錄更新。</span><span class="sxs-lookup"><span data-stu-id="db201-127">Using installations also enables you toodo partial registration updates.</span></span> <span data-ttu-id="db201-128">hello 安裝部分更新要求使用修補程式的方法使用 hello [JSON 修補程式標準](https://tools.ietf.org/html/rfc6902)。</span><span class="sxs-lookup"><span data-stu-id="db201-128">hello partial update of an installation is requested with a PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902).</span></span> <span data-ttu-id="db201-129">當您想在 hello 註冊 tooupdate 標記時，這是特別有用。</span><span class="sxs-lookup"><span data-stu-id="db201-129">This is particularly useful when you want tooupdate tags on hello registration.</span></span> <span data-ttu-id="db201-130">沒有 toopull 向 hello 整個登錄，然後再一次重新傳送所有 hello 先前標記。</span><span class="sxs-lookup"><span data-stu-id="db201-130">You don't have toopull down hello entire registration and then resend all hello previous tags again.</span></span>

<span data-ttu-id="db201-131">安裝可以包含下列屬性的 hello hello。</span><span class="sxs-lookup"><span data-stu-id="db201-131">An installation can contain hello hello following properties.</span></span> <span data-ttu-id="db201-132">如需完整清單的 hello 安裝屬性，請參閱[建立或覆寫安裝使用 REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx)或[安裝內容](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx)hello。</span><span class="sxs-lookup"><span data-stu-id="db201-132">For a complete listing of hello installation properties see, [Create or Overwrite an Installation with REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) or [Installation Properties](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) for hello .</span></span>

    // Example installation format tooshow some supported properties
    {
        installationId: "",
        expirationTime: "",
        tags: [],
        platform: "",
        pushChannel: "",
        ………
        templates: {
            "templateName1" : {
                body: "",
                tags: [] },
            "templateName2" : {
                body: "",
                // Headers are for Windows Store only
                headers: {
                    "X-WNS-Type": "wns/tile" }
                tags: [] }
        },
        secondaryTiles: {
            "tileId1": {
                pushChannel: "",
                tags: [],
                templates: {
                    "otherTemplate": {
                        bodyTemplate: "",
                        headers: {
                            ... }
                        tags: [] }
                }
            }
        }
    }



<span data-ttu-id="db201-133">註冊和安裝依預設不會再過期的重要 toonote 它。</span><span class="sxs-lookup"><span data-stu-id="db201-133">It is important toonote that registrations and installations by default no longer expire.</span></span>

<span data-ttu-id="db201-134">註冊與安裝必須包含每個裝置/通道的有效 PNS 控制代碼。</span><span class="sxs-lookup"><span data-stu-id="db201-134">Registrations and installations must contain a valid PNS handle for each device/channel.</span></span> <span data-ttu-id="db201-135">因為只能在 hello 裝置上的用戶端應用程式中取得其 PNS 控制代碼，其中一個模式是 tooregister hello 用戶端應用程式與該裝置上直接。</span><span class="sxs-lookup"><span data-stu-id="db201-135">Because PNS handles can only be obtained in a client app on hello device, one pattern is tooregister directly on that device with hello client app.</span></span> <span data-ttu-id="db201-136">在 hello 其他手動、 安全性考量和商務邏輯相關 tootags 可能會要求您 toomanage hello 應用程式後端中的裝置註冊。</span><span class="sxs-lookup"><span data-stu-id="db201-136">On hello other hand, security considerations and business logic related tootags might require you toomanage device registration in hello app back-end.</span></span> 

#### <a name="templates"></a><span data-ttu-id="db201-137">範本</span><span class="sxs-lookup"><span data-stu-id="db201-137">Templates</span></span>
<span data-ttu-id="db201-138">如果您想 toouse[範本](notification-hubs-templates-cross-platform-push-messages.md)，hello 裝置安裝也會保存在 JSON 中該裝置與相關聯的所有範本格式 （請參閱上述範例）。</span><span class="sxs-lookup"><span data-stu-id="db201-138">If you want toouse [Templates](notification-hubs-templates-cross-platform-push-messages.md), hello device installation also hold all templates associated with that device in a JSON format (see sample above).</span></span> <span data-ttu-id="db201-139">hello 範本名稱說明目標 hello 的不同樣板相同的裝置。</span><span class="sxs-lookup"><span data-stu-id="db201-139">hello template names help target different templates for hello same device.</span></span>

<span data-ttu-id="db201-140">請注意，每個範本名稱會對應 tooa 範本主體和一組選擇性的標記。</span><span class="sxs-lookup"><span data-stu-id="db201-140">Note that each template name maps tooa template body and an optional set of tags.</span></span> <span data-ttu-id="db201-141">此外，每個平台可以有額外的範本屬性。</span><span class="sxs-lookup"><span data-stu-id="db201-141">Moreover, each platform can have additional template properties.</span></span> <span data-ttu-id="db201-142">（使用 WNS） 的 Windows 市集和 Windows Phone 8 （使用 MPNS），一組額外的標頭可以 hello 範本的一部分。</span><span class="sxs-lookup"><span data-stu-id="db201-142">For Windows Store (using WNS) and Windows Phone 8 (using MPNS), an additional set of headers can be part of hello template.</span></span> <span data-ttu-id="db201-143">在 APNs 的 hello 案例中，您可以設定到期屬性 tooeither 常數或 tooa 範本運算式。</span><span class="sxs-lookup"><span data-stu-id="db201-143">In hello case of APNs, you can set an expiry property tooeither a constant or tooa template expression.</span></span> <span data-ttu-id="db201-144">如需完整清單的 hello 安裝屬性，請參閱[建立或覆寫與其餘的安裝](https://msdn.microsoft.com/library/azure/mt621153.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="db201-144">For a complete listing of hello installation properties see, [Create or Overwrite an Installation with REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) topic.</span></span>

#### <a name="secondary-tiles-for-windows-store-apps"></a><span data-ttu-id="db201-145">Windows 市集應用程式的次要磚</span><span class="sxs-lookup"><span data-stu-id="db201-145">Secondary Tiles for Windows Store Apps</span></span>
<span data-ttu-id="db201-146">對於 Windows 市集用戶端應用程式，傳送通知 toosecondary 圖格是 hello 相同做為傳送 toohello 主要。</span><span class="sxs-lookup"><span data-stu-id="db201-146">For Windows Store client applications, sending notifications toosecondary tiles is hello same as sending them toohello primary one.</span></span> <span data-ttu-id="db201-147">在安裝中也支援此行為。</span><span class="sxs-lookup"><span data-stu-id="db201-147">This is also supported in installations.</span></span> <span data-ttu-id="db201-148">請注意，次要磚不同 ChannelUri、 哪些 hello SDK 用戶端應用程式上的會以透明的方式處理。</span><span class="sxs-lookup"><span data-stu-id="db201-148">Note that secondary tiles have a different ChannelUri, which hello SDK on your client app handles transparently.</span></span>

<span data-ttu-id="db201-149">hello SecondaryTiles 字典會使用 hello 是 Windows 市集應用程式中的使用的 toocreate hello SecondaryTiles 物件的相同 TileId。</span><span class="sxs-lookup"><span data-stu-id="db201-149">hello SecondaryTiles dictionary uses hello same TileId that is used toocreate hello SecondaryTiles object in your Windows Store app.</span></span>
<span data-ttu-id="db201-150">如同 hello ChannelUri 主要、 次要磚的 Channeluri 可以變更在任何時刻。</span><span class="sxs-lookup"><span data-stu-id="db201-150">As with hello primary ChannelUri, ChannelUris of secondary tiles can change at any moment.</span></span> <span data-ttu-id="db201-151">順序 tookeep hello hello 通知中樞更新的安裝，在 hello 裝置必須加以重新整理以 hello 目前 Channeluri hello 次要磚。</span><span class="sxs-lookup"><span data-stu-id="db201-151">In order tookeep hello installations in hello notification hub updated, hello device must refresh them with hello current ChannelUris of hello secondary tiles.</span></span>

## <a name="registration-management-from-hello-device"></a><span data-ttu-id="db201-152">從 hello 裝置的註冊管理</span><span class="sxs-lookup"><span data-stu-id="db201-152">Registration management from hello device</span></span>
<span data-ttu-id="db201-153">從用戶端應用程式中管理裝置註冊，hello 後端時只負責傳送通知。</span><span class="sxs-lookup"><span data-stu-id="db201-153">When managing device registration from client apps, hello backend is only responsible for sending notifications.</span></span> <span data-ttu-id="db201-154">用戶端應用程式保留 toodate、 註冊其 PNS 控制代碼，並註冊標記。</span><span class="sxs-lookup"><span data-stu-id="db201-154">Client apps keep PNS handles up toodate, and register tags.</span></span> <span data-ttu-id="db201-155">下列圖片的 hello 說明這個模式。</span><span class="sxs-lookup"><span data-stu-id="db201-155">hello following picture illustrates this pattern.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

<span data-ttu-id="db201-156">hello 裝置第一次從 hello PNS，擷取的 hello PNS 處理，然後直接使用 hello 通知中樞註冊。</span><span class="sxs-lookup"><span data-stu-id="db201-156">hello device first retrieves hello PNS handle from hello PNS, then registers with hello notification hub directly.</span></span> <span data-ttu-id="db201-157">Hello 註冊成功之後，hello 應用程式後端可以傳送通知目標註冊。</span><span class="sxs-lookup"><span data-stu-id="db201-157">After hello registration is successful, hello app backend can send a notification targeting that registration.</span></span> <span data-ttu-id="db201-158">如需有關如何 toosend 通知，請參閱[路由和標記運算式](notification-hubs-tags-segment-push-message.md)。</span><span class="sxs-lookup"><span data-stu-id="db201-158">For more information about how toosend notifications, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>
<span data-ttu-id="db201-159">請注意，在此情況下，您將使用只接聽權限 tooaccess 從 hello 裝置通知中樞。</span><span class="sxs-lookup"><span data-stu-id="db201-159">Note that in this case, you will use only Listen rights tooaccess your notification hubs from hello device.</span></span> <span data-ttu-id="db201-160">如需詳細資訊，請參閱[安全性](notification-hubs-push-notification-security.md)。</span><span class="sxs-lookup"><span data-stu-id="db201-160">For more information, see [Security](notification-hubs-push-notification-security.md).</span></span>

<span data-ttu-id="db201-161">從 hello 裝置註冊是 hello 最簡單的方法，但有一些缺點。</span><span class="sxs-lookup"><span data-stu-id="db201-161">Registering from hello device is hello simplest method, but it has some drawbacks.</span></span>
<span data-ttu-id="db201-162">hello 第一個缺點是用戶端應用程式可以只更新其標籤 hello 應用程式使用中時。</span><span class="sxs-lookup"><span data-stu-id="db201-162">hello first drawback is that a client app can only update its tags when hello app is active.</span></span> <span data-ttu-id="db201-163">比方說，如果使用者有註冊標記相關的 toosport 小組，當 hello 第一個裝置註冊其他標記 （例如，海鷹） 的兩個裝置，hello 第二部裝置不會收到 hello 通知有關 hello 海鷹直到 hello hello 上的應用程式第二個裝置會執行第二次。</span><span class="sxs-lookup"><span data-stu-id="db201-163">For example, if a user has two devices that register tags related toosport teams, when hello first device registers for an additional tag (for example, Seahawks), hello second device will not receive hello notifications about hello Seahawks until hello app on hello second device is executed a second time.</span></span> <span data-ttu-id="db201-164">較常見地，標記會受到多個裝置，從 hello 後端管理標記時，理想的選項。</span><span class="sxs-lookup"><span data-stu-id="db201-164">More generally, when tags are affected by multiple devices, managing tags from hello backend is a desirable option.</span></span>
<span data-ttu-id="db201-165">hello 註冊管理 hello 用戶端應用程式從第二個缺點是，由於應用程式可能會遭竊取，保護 hello 註冊 toospecific 標記時，必須特別小心，hello > 一節 「 標記層級安全性 」 中所述</span><span class="sxs-lookup"><span data-stu-id="db201-165">hello second drawback of registration management from hello client app is that, since apps can be hacked, securing hello registration toospecific tags requires extra care, as explained in hello section “Tag-level security.”</span></span>

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-an-installation"></a><span data-ttu-id="db201-166">範例程式碼 tooregister 與通知中樞，從利用安裝裝置</span><span class="sxs-lookup"><span data-stu-id="db201-166">Example code tooregister with a notification hub from a device using an installation</span></span>
<span data-ttu-id="db201-167">在這個階段中，這僅適用於使用 hello[通知中心 REST API](https://msdn.microsoft.com/library/mt621153.aspx)。</span><span class="sxs-lookup"><span data-stu-id="db201-167">At this time, this is only supported using hello [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx).</span></span>

<span data-ttu-id="db201-168">您也可以使用 hello PATCH 方法使用 hello [JSON 修補程式標準](https://tools.ietf.org/html/rfc6902)hello 安裝更新。</span><span class="sxs-lookup"><span data-stu-id="db201-168">You can also use hello PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating hello installation.</span></span>

    class DeviceInstallation
    {
        public string installationId { get; set; }
        public string platform { get; set; }
        public string pushChannel { get; set; }
        public string[] tags { get; set; }
    }

    private async Task<HttpStatusCode> CreateOrUpdateInstallationAsync(DeviceInstallation deviceInstallation,
         string hubName, string listenConnectionString)
    {
        if (deviceInstallation.installationId == null)
            return HttpStatusCode.BadRequest;

        // Parse connection string (https://msdn.microsoft.com/library/azure/dn495627.aspx)
        ConnectionStringUtility connectionSaSUtil = new ConnectionStringUtility(listenConnectionString);
        string hubResource = "installations/" + deviceInstallation.installationId + "?";
        string apiVersion = "api-version=2015-04";

        // Determine hello targetUri that we will sign
        string uri = connectionSaSUtil.Endpoint + hubName + "/" + hubResource + apiVersion;

        //=== Generate SaS Security Token for Authorization header ===
        // See, https://msdn.microsoft.com/library/azure/dn495627.aspx
        string SasToken = connectionSaSUtil.getSaSToken(uri, 60);

        using (var httpClient = new HttpClient())
        {
            string json = JsonConvert.SerializeObject(deviceInstallation);

            httpClient.DefaultRequestHeaders.Add("Authorization", SasToken);

            var response = await httpClient.PutAsync(uri, new StringContent(json, System.Text.Encoding.UTF8, "application/json"));
            return response.StatusCode;
        }
    }

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    string installationId = null;
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a installation id in application data, create and store as application data.
    if (!settings.ContainsKey("__NHInstallationId"))
    {
        installationId = Guid.NewGuid().ToString();
        settings.Add("__NHInstallationId", installationId);
    }

    installationId = (string)settings["__NHInstallationId"];

    var deviceInstallation = new DeviceInstallation
    {
        installationId = installationId,
        platform = "wns",
        pushChannel = channel.Uri,
        //tags = tags.ToArray<string>()
    };

    var statusCode = await CreateOrUpdateInstallationAsync(deviceInstallation, 
                        "<HUBNAME>", "<SHARED LISTEN CONNECTION STRING>");

    if (statusCode != HttpStatusCode.Accepted)
    {
        var dialog = new MessageDialog(statusCode.ToString(), "Registration failed. Installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
    else
    {
        var dialog = new MessageDialog("Registration successful using installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }



#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration"></a><span data-ttu-id="db201-169">範例程式碼 tooregister 與裝置的註冊通知中樞</span><span class="sxs-lookup"><span data-stu-id="db201-169">Example code tooregister with a notification hub from a device using a registration</span></span>
<span data-ttu-id="db201-170">這些方法會建立或更新 hello 呼叫所在的裝置註冊。</span><span class="sxs-lookup"><span data-stu-id="db201-170">These methods create or update a registration for hello device on which they are called.</span></span> <span data-ttu-id="db201-171">這表示在順序 tooupdate hello 控制代碼或 hello 標籤中，您必須覆寫 hello 整個登錄。</span><span class="sxs-lookup"><span data-stu-id="db201-171">This means that in order tooupdate hello handle or hello tags, you must overwrite hello entire registration.</span></span> <span data-ttu-id="db201-172">請記住，註冊會暫時性的因此您應該永遠具有具有特定裝置需要的 hello 目前標記的可靠存放區。</span><span class="sxs-lookup"><span data-stu-id="db201-172">Remember that registrations are transient, so you should always have a reliable store with hello current tags that a specific device needs.</span></span>

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // hello Device id from hello PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from hello client itself, then store this registration id in device
    // storage. Then when hello app starts, you can check if a registration id already exists or not before
    // creating.
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a registration id in application data, store in application data.
    if (!settings.ContainsKey("__NHRegistrationId"))
    {
        // make sure there are no existing registrations for this push handle (used for iOS and Android)    
        string newRegistrationId = null;
        var registrations = await hub.GetRegistrationsByChannelAsync(pushChannel.Uri, 100);
        foreach (RegistrationDescription registration in registrations)
        {
            if (newRegistrationId == null)
            {
                newRegistrationId = registration.RegistrationId;
            }
            else
            {
                await hub.DeleteRegistrationAsync(registration);
            }
        }

        newRegistrationId = await hub.CreateRegistrationIdAsync();

        settings.Add("__NHRegistrationId", newRegistrationId);
    }

    string regId = (string)settings["__NHRegistrationId"];

    RegistrationDescription registration = new WindowsRegistrationDescription(pushChannel.Uri);
    registration.RegistrationId = regId;
    registration.Tags = new HashSet<string>(YourTags);

    try
    {
        await hub.CreateOrUpdateRegistrationAsync(registration);
    }
    catch (Microsoft.WindowsAzure.Messaging.RegistrationGoneException e)
    {
        settings.Remove("__NHRegistrationId");
    }


## <a name="registration-management-from-a-backend"></a><span data-ttu-id="db201-173">從後端管理註冊</span><span class="sxs-lookup"><span data-stu-id="db201-173">Registration management from a backend</span></span>
<span data-ttu-id="db201-174">管理從 hello 後端註冊，需要撰寫額外的程式碼。</span><span class="sxs-lookup"><span data-stu-id="db201-174">Managing registrations from hello backend requires writing additional code.</span></span> <span data-ttu-id="db201-175">從 hello 裝置 hello 應用程式必須提供 hello 更新的 PNS 控制代碼 toohello 後端，每次 hello 應用程式開始 （以及標籤和範本），而 hello 後端就必須更新此控制代碼上 hello 通知中樞。</span><span class="sxs-lookup"><span data-stu-id="db201-175">hello app from hello device must provide hello updated PNS handle toohello backend every time hello app starts (along with tags and templates), and hello backend must update this handle on hello notification hub.</span></span> <span data-ttu-id="db201-176">下列圖片的 hello 說明這種設計。</span><span class="sxs-lookup"><span data-stu-id="db201-176">hello following picture illustrates this design.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

<span data-ttu-id="db201-177">hello 的優點 hello 後端管理註冊包括 hello 能力 toomodify 標記 tooregistrations hello hello 裝置上的對應應用程式為非使用中時，即使而且 tooauthenticate hello 用戶端應用程式然後再加入標記 tooits 註冊。</span><span class="sxs-lookup"><span data-stu-id="db201-177">hello advantages of managing registrations from hello backend include hello ability toomodify tags tooregistrations even when hello corresponding app on hello device is inactive, and tooauthenticate hello client app before adding a tag tooits registration.</span></span>

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-backend-using-an-installation"></a><span data-ttu-id="db201-178">範例程式碼 tooregister 與通知中樞從後端使用的安裝</span><span class="sxs-lookup"><span data-stu-id="db201-178">Example code tooregister with a notification hub from a backend using an installation</span></span>
<span data-ttu-id="db201-179">hello 用戶端裝置仍然取得其 PNS 處理及相關的安裝內容如往常一般，並可以執行 hello 登錄和授權 hello 後端自訂 API 標記等 hello 後端的呼叫可以利用 hello[通知中樞 SDK後端作業](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)。</span><span class="sxs-lookup"><span data-stu-id="db201-179">hello client device still gets its PNS handle and relevant installation properties as before and calls a custom API on hello backend that can perform hello registration and authorize tags etc. hello backend can leverage hello [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="db201-180">您也可以使用 hello PATCH 方法使用 hello [JSON 修補程式標準](https://tools.ietf.org/html/rfc6902)hello 安裝更新。</span><span class="sxs-lookup"><span data-stu-id="db201-180">You can also use hello PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating hello installation.</span></span>

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on hello backend
    public async Task<HttpResponseMessage> Put(DeviceInstallation deviceUpdate)
    {

        Installation installation = new Installation();
        installation.InstallationId = deviceUpdate.InstallationId;
        installation.PushChannel = deviceUpdate.Handle;
        installation.Tags = deviceUpdate.Tags;

        switch (deviceUpdate.Platform)
        {
            case "mpns":
                installation.Platform = NotificationPlatform.Mpns;
                break;
            case "wns":
                installation.Platform = NotificationPlatform.Wns;
                break;
            case "apns":
                installation.Platform = NotificationPlatform.Apns;
                break;
            case "gcm":
                installation.Platform = NotificationPlatform.Gcm;
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }


        // In hello backend we can control if a user is allowed tooadd tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration-id"></a><span data-ttu-id="db201-181">範例程式碼 tooregister 與裝置的註冊識別碼的通知中樞</span><span class="sxs-lookup"><span data-stu-id="db201-181">Example code tooregister with a notification hub from a device using a registration id</span></span>
<span data-ttu-id="db201-182">您可以從 app 後端，對註冊執行基本 CRUD 作業。</span><span class="sxs-lookup"><span data-stu-id="db201-182">From your app backend, you can perform basic CRUDS operations on registrations.</span></span> <span data-ttu-id="db201-183">例如：</span><span class="sxs-lookup"><span data-stu-id="db201-183">For example:</span></span>

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of hello correct type, e.g.
    var reg = new WindowsRegistrationDescription(channelUri, tags);

    // Create
    await hub.CreateRegistrationAsync(reg);

    // Get by id
    var r = await hub.GetRegistrationAsync<RegistrationDescription>("id");

    // update
    r.Tags.Add("myTag");

    // update on hub
    await hub.UpdateRegistrationAsync(r);

    // delete
    await hub.DeleteRegistrationAsync(r);


<span data-ttu-id="db201-184">hello 後端必須處理註冊更新之間的並行存取。</span><span class="sxs-lookup"><span data-stu-id="db201-184">hello backend must handle concurrency between registration updates.</span></span> <span data-ttu-id="db201-185">「服務匯流排」可提供開放式並行存取控制來管理註冊。</span><span class="sxs-lookup"><span data-stu-id="db201-185">Service Bus offers optimistic concurrency control for registration management.</span></span> <span data-ttu-id="db201-186">在 hello HTTP 層級，這被實作使用 hello ETag 註冊管理作業。</span><span class="sxs-lookup"><span data-stu-id="db201-186">At hello HTTP level, this is implemented with hello use of ETag on registration management operations.</span></span> <span data-ttu-id="db201-187">Microsoft SDK 會在背景使用這項功能，如果因並行存取而導致更新被拒，將會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="db201-187">This feature is transparently used by Microsoft SDKs, which throw an exception if an update is rejected for concurrency reasons.</span></span> <span data-ttu-id="db201-188">hello 應用程式後端負責處理這些例外狀況，並視需要重試 hello 更新。</span><span class="sxs-lookup"><span data-stu-id="db201-188">hello app backend is responsible for handling these exceptions and retrying hello update if required.</span></span>

