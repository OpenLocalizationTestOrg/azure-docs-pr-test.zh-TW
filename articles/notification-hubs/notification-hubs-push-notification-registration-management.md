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
# <a name="registration-management"></a>註冊管理
## <a name="overview"></a>概觀
本主題說明如何 tooregister 裝置中順序 tooreceive 通知中樞推播通知。 hello 主題描述註冊在高層級，然後介紹 hello 兩個主要模式註冊裝置： 註冊 hello 裝置從直接 toohello 通知中樞，並透過應用程式後端註冊。 

## <a name="what-is-device-registration"></a>什麼是裝置註冊
向「通知中樞」註冊裝置是藉由使用 [註冊] 或 [安裝] 來完成。

#### <a name="registrations"></a>註冊
註冊將的 hello 處理標記和可能的範本與裝置的平台通知服務 (PNS)。 hello PNS 控制代碼可能是 ChannelURI、 裝置權杖或 GCM 註冊識別碼。標記是使用的 tooroute 通知 toohello 一組正確的裝置控制代碼。 如需詳細資訊，請參閱 [路由與標記運算式](notification-hubs-tags-segment-push-message.md)。 範本是使用的 tooimplement 註冊每個轉換。 如需詳細資訊，請參閱 [範本](notification-hubs-templates-cross-platform-push-messages.md)。

#### <a name="installations"></a>安裝
安裝是增強型的註冊，包含一組推播相關的屬性。 它是您的裝置 hello tooregistering 最新且最佳的方法。 不過，目前用戶端 .NET SDK([適用於後端作業的通知中樞 SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) 不支援此種安裝。  這表示如果您註冊從 hello 用戶端裝置本身，您就必須 toouse hello[通知中心 REST API](https://msdn.microsoft.com/library/mt621153.aspx)接近 toosupport 安裝。 如果您使用後端服務，您應該能夠 toouse[後端作業的通知中樞 SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)。

hello 下面是一些主要優點 toousing 安裝：

* 建立或更新安裝是完全等冪的。 因此您可以重試它，而不需顧慮重複註冊的情況。
* hello 安裝模型可輕鬆 toodo 個別推播通知的目標特定的裝置。 在每個安裝型註冊，都會自動新增一個系統標記 **"$InstallationId:[installationId]"** 。 因此您可以呼叫傳送 toothis 標記 tootarget 特定裝置而不需要任何額外的程式碼 toodo。
* 使用安裝時，也可讓您 toodo 部分登錄更新。 hello 安裝部分更新要求使用修補程式的方法使用 hello [JSON 修補程式標準](https://tools.ietf.org/html/rfc6902)。 當您想在 hello 註冊 tooupdate 標記時，這是特別有用。 沒有 toopull 向 hello 整個登錄，然後再一次重新傳送所有 hello 先前標記。

安裝可以包含下列屬性的 hello hello。 如需完整清單的 hello 安裝屬性，請參閱[建立或覆寫安裝使用 REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx)或[安裝內容](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx)hello。

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



註冊和安裝依預設不會再過期的重要 toonote 它。

註冊與安裝必須包含每個裝置/通道的有效 PNS 控制代碼。 因為只能在 hello 裝置上的用戶端應用程式中取得其 PNS 控制代碼，其中一個模式是 tooregister hello 用戶端應用程式與該裝置上直接。 在 hello 其他手動、 安全性考量和商務邏輯相關 tootags 可能會要求您 toomanage hello 應用程式後端中的裝置註冊。 

#### <a name="templates"></a>範本
如果您想 toouse[範本](notification-hubs-templates-cross-platform-push-messages.md)，hello 裝置安裝也會保存在 JSON 中該裝置與相關聯的所有範本格式 （請參閱上述範例）。 hello 範本名稱說明目標 hello 的不同樣板相同的裝置。

請注意，每個範本名稱會對應 tooa 範本主體和一組選擇性的標記。 此外，每個平台可以有額外的範本屬性。 （使用 WNS） 的 Windows 市集和 Windows Phone 8 （使用 MPNS），一組額外的標頭可以 hello 範本的一部分。 在 APNs 的 hello 案例中，您可以設定到期屬性 tooeither 常數或 tooa 範本運算式。 如需完整清單的 hello 安裝屬性，請參閱[建立或覆寫與其餘的安裝](https://msdn.microsoft.com/library/azure/mt621153.aspx)主題。

#### <a name="secondary-tiles-for-windows-store-apps"></a>Windows 市集應用程式的次要磚
對於 Windows 市集用戶端應用程式，傳送通知 toosecondary 圖格是 hello 相同做為傳送 toohello 主要。 在安裝中也支援此行為。 請注意，次要磚不同 ChannelUri、 哪些 hello SDK 用戶端應用程式上的會以透明的方式處理。

hello SecondaryTiles 字典會使用 hello 是 Windows 市集應用程式中的使用的 toocreate hello SecondaryTiles 物件的相同 TileId。
如同 hello ChannelUri 主要、 次要磚的 Channeluri 可以變更在任何時刻。 順序 tookeep hello hello 通知中樞更新的安裝，在 hello 裝置必須加以重新整理以 hello 目前 Channeluri hello 次要磚。

## <a name="registration-management-from-hello-device"></a>從 hello 裝置的註冊管理
從用戶端應用程式中管理裝置註冊，hello 後端時只負責傳送通知。 用戶端應用程式保留 toodate、 註冊其 PNS 控制代碼，並註冊標記。 下列圖片的 hello 說明這個模式。

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

hello 裝置第一次從 hello PNS，擷取的 hello PNS 處理，然後直接使用 hello 通知中樞註冊。 Hello 註冊成功之後，hello 應用程式後端可以傳送通知目標註冊。 如需有關如何 toosend 通知，請參閱[路由和標記運算式](notification-hubs-tags-segment-push-message.md)。
請注意，在此情況下，您將使用只接聽權限 tooaccess 從 hello 裝置通知中樞。 如需詳細資訊，請參閱[安全性](notification-hubs-push-notification-security.md)。

從 hello 裝置註冊是 hello 最簡單的方法，但有一些缺點。
hello 第一個缺點是用戶端應用程式可以只更新其標籤 hello 應用程式使用中時。 比方說，如果使用者有註冊標記相關的 toosport 小組，當 hello 第一個裝置註冊其他標記 （例如，海鷹） 的兩個裝置，hello 第二部裝置不會收到 hello 通知有關 hello 海鷹直到 hello hello 上的應用程式第二個裝置會執行第二次。 較常見地，標記會受到多個裝置，從 hello 後端管理標記時，理想的選項。
hello 註冊管理 hello 用戶端應用程式從第二個缺點是，由於應用程式可能會遭竊取，保護 hello 註冊 toospecific 標記時，必須特別小心，hello > 一節 「 標記層級安全性 」 中所述

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-an-installation"></a>範例程式碼 tooregister 與通知中樞，從利用安裝裝置
在這個階段中，這僅適用於使用 hello[通知中心 REST API](https://msdn.microsoft.com/library/mt621153.aspx)。

您也可以使用 hello PATCH 方法使用 hello [JSON 修補程式標準](https://tools.ietf.org/html/rfc6902)hello 安裝更新。

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



#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration"></a>範例程式碼 tooregister 與裝置的註冊通知中樞
這些方法會建立或更新 hello 呼叫所在的裝置註冊。 這表示在順序 tooupdate hello 控制代碼或 hello 標籤中，您必須覆寫 hello 整個登錄。 請記住，註冊會暫時性的因此您應該永遠具有具有特定裝置需要的 hello 目前標記的可靠存放區。

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


## <a name="registration-management-from-a-backend"></a>從後端管理註冊
管理從 hello 後端註冊，需要撰寫額外的程式碼。 從 hello 裝置 hello 應用程式必須提供 hello 更新的 PNS 控制代碼 toohello 後端，每次 hello 應用程式開始 （以及標籤和範本），而 hello 後端就必須更新此控制代碼上 hello 通知中樞。 下列圖片的 hello 說明這種設計。

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

hello 的優點 hello 後端管理註冊包括 hello 能力 toomodify 標記 tooregistrations hello hello 裝置上的對應應用程式為非使用中時，即使而且 tooauthenticate hello 用戶端應用程式然後再加入標記 tooits 註冊。

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-backend-using-an-installation"></a>範例程式碼 tooregister 與通知中樞從後端使用的安裝
hello 用戶端裝置仍然取得其 PNS 處理及相關的安裝內容如往常一般，並可以執行 hello 登錄和授權 hello 後端自訂 API 標記等 hello 後端的呼叫可以利用 hello[通知中樞 SDK後端作業](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)。

您也可以使用 hello PATCH 方法使用 hello [JSON 修補程式標準](https://tools.ietf.org/html/rfc6902)hello 安裝更新。

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


#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration-id"></a>範例程式碼 tooregister 與裝置的註冊識別碼的通知中樞
您可以從 app 後端，對註冊執行基本 CRUD 作業。 例如：

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


hello 後端必須處理註冊更新之間的並行存取。 「服務匯流排」可提供開放式並行存取控制來管理註冊。 在 hello HTTP 層級，這被實作使用 hello ETag 註冊管理作業。 Microsoft SDK 會在背景使用這項功能，如果因並行存取而導致更新被拒，將會擲回例外狀況。 hello 應用程式後端負責處理這些例外狀況，並視需要重試 hello 更新。

