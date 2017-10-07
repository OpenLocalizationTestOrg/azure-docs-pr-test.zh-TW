---
title: "aaaHow toouse 使用 Python 的通知中樞"
description: "深入了解如何從 Python 的後端 toouse Azure 通知中樞。"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 5640dd4a-a91e-4aa0-a833-93615bde49b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: python
ms.devlang: php
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 21d5aaf7fc24c9936fac8e0a8de640c66c51ab0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-python"></a>如何 toouse 來自 Python 的通知中樞
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

您可以從 Java/PHP/Python/Ruby 後端存取所有通知中樞功能 hello MSDN 主題中所述，使用 hello 通知中樞 REST 介面[通知中心 REST Api](http://msdn.microsoft.com/library/dn223264.aspx)。

> [!NOTE]
> 這是實作以 Python hello 通知傳送的範例參考實作，而且不是 hello 正式支援通知中樞 Python SDK。
> 
> 這個範例是使用 Python 3.4 撰寫的。
> 
> 

在本主題中，我們將說明如何：

* 在 Python 中建置通知中樞功能的 REST 用戶端。
* 傳送通知使用 hello Python 介面 toohello 通知中樞 REST Api。 
* 取得偵錯/教育目的 hello HTTP REST 要求/回應的傾印。 

您可以依照 hello [Get 入門教學課程](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)針對您的選擇，以 Python 實作 hello 後端部分的行動平台。

> [!NOTE]
> hello 範例 hello 範圍是只有有限的 toosend 通知並不會執行任何註冊管理。
> 
> 

## <a name="client-interface"></a>用戶端介面
hello 主要用戶端介面可以提供相同的方法用於 hello hello [.NET 通知中樞 SDK](http://msdn.microsoft.com/library/jj933431.aspx)。 這可讓您 toodirectly 轉譯所有 hello 教學課程和此站台上目前可用的範例，並在 hello hello 社群所貢獻網際網路。

您可以找到所有 hello 程式碼用於 hello [Python REST 包裝函式範例]。

例如，toocreate 用戶端：

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

toosend Windows 快顯通知：

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a>實作
如果您還未這樣做，請依照我們[Get 入門教學課程]向上 toohello 您尚未 tooimplement hello 後端的最後一節。

所有 hello 可找到完整的 REST 包裝函式的詳細資料 tooimplement [MSDN](http://msdn.microsoft.com/library/dn530746.aspx)。 本節中，我們將描述 hello Python 實作 hello 主要步驟需要 tooaccess 通知中心 REST 端點及傳送通知

1. 剖析 hello 連接字串
2. 產生 hello 授權權杖
3. 使用 HTTP REST API 傳送通知

### <a name="parse-hello-connection-string"></a>剖析 hello 連接字串
以下是實作 hello 用戶端，其建構函式會剖析 hello 連接字串 hello 主要類別：

    class NotificationHub:
        API_VERSION = "?api-version=2013-10"
        DEBUG_SEND = "&test"

        def __init__(self, connection_string=None, hub_name=None, debug=0):
            self.HubName = hub_name
            self.Debug = debug

            # Parse connection string
            parts = connection_string.split(';')
            if len(parts) != 3:
                raise Exception("Invalid ConnectionString.")

            for part in parts:
                if part.startswith('Endpoint'):
                    self.Endpoint = 'https' + part[11:]
                if part.startswith('SharedAccessKeyName'):
                    self.SasKeyName = part[20:]
                if part.startswith('SharedAccessKey'):
                    self.SasKeyValue = part[16:]


### <a name="create-security-token"></a>建立安全性權杖
語彙基元建立 hello 安全性的 hello 詳細資料可用[這裡](http://msdn.microsoft.com/library/dn495627.aspx)。
hello 下列方法將加入 toobe toohello **NotificationHub**類別 toocreate hello token 基礎 hello hello 目前要求和 hello 認證從 hello 連接字串中擷取的 URI。

    @staticmethod
    def get_expiry():
        # By default returns an expiration of 5 minutes (=300 seconds) from now
        return int(round(time.time() + 300))

    @staticmethod
    def encode_base64(data):
        return base64.b64encode(data)

    def sign_string(self, to_sign):
        key = self.SasKeyValue.encode('utf-8')
        to_sign = to_sign.encode('utf-8')
        signed_hmac_sha256 = hmac.HMAC(key, to_sign, hashlib.sha256)
        digest = signed_hmac_sha256.digest()
        encoded_digest = self.encode_base64(digest)
        return encoded_digest

    def generate_sas_token(self):
        target_uri = self.Endpoint + self.HubName
        my_uri = urllib.parse.quote(target_uri, '').lower()
        expiry = str(self.get_expiry())
        to_sign = my_uri + '\n' + expiry
        signature = urllib.parse.quote(self.sign_string(to_sign))
        auth_format = 'SharedAccessSignature sig={0}&se={1}&skn={2}&sr={3}'
        sas_token = auth_format.format(signature, expiry, self.SasKeyName, my_uri)
        return sas_token

### <a name="send-a-notification-using-http-rest-api"></a>使用 HTTP REST API 傳送通知
首先，讓我們先定義呈現通知的類別。

    class Notification:
        def __init__(self, notification_format=None, payload=None, debug=0):
            valid_formats = ['template', 'apple', 'gcm', 'windows', 'windowsphone', "adm", "baidu"]
            if not any(x in notification_format for x in valid_formats):
                raise Exception(
                    "Invalid Notification format. " +
                    "Must be one of hello following - 'template', 'apple', 'gcm', 'windows', 'windowsphone', 'adm', 'baidu'")

            self.format = notification_format
            self.payload = payload

            # array with keynames for headers
            # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
            # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry
            # in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
            self.headers = None

此類別是原生通知主體的容器，或是一組範本通知案例的屬性，及一組包含格式 (原生平台或範本) 的標頭，以及平台特定屬性 (如 Apple 到期屬性和 WNS 標頭)。

請參閱 toohello[通知中心 REST Api 文件](http://msdn.microsoft.com/library/dn495827.aspx)和 hello 特定通知平台的格式，針對所有 hello 可用的選項。

與這個類別中，我們可以撰寫 hello 傳送通知方法內 hello 現在**NotificationHub**類別。

    def make_http_request(self, url, payload, headers):
        parsed_url = urllib.parse.urlparse(url)
        connection = http.client.HTTPSConnection(parsed_url.hostname, parsed_url.port)

        if self.Debug > 0:
            connection.set_debuglevel(self.Debug)
            # adding this querystring parameter gets detailed information about hello PNS send notification outcome
            url += self.DEBUG_SEND
            print("--- REQUEST ---")
            print("URI: " + url)
            print("Headers: " + json.dumps(headers, sort_keys=True, indent=4, separators=(' ', ': ')))
            print("--- END REQUEST ---\n")

        connection.request('POST', url, payload, headers)
        response = connection.getresponse()

        if self.Debug > 0:
            # print out detailed response information for debugging purpose
            print("\n\n--- RESPONSE ---")
            print(str(response.status) + " " + response.reason)
            print(response.msg)
            print(response.read())
            print("--- END RESPONSE ---")

        elif response.status != 201:
            # Successful outcome of send message is HTTP 201 - Created
            raise Exception(
                "Error sending notification. Received HTTP code " + str(response.status) + " " + response.reason)

        connection.close()

    def send_notification(self, notification, tag_or_tag_expression=None):
        url = self.Endpoint + self.HubName + '/messages' + self.API_VERSION

        json_platforms = ['template', 'apple', 'gcm', 'adm', 'baidu']

        if any(x in notification.format for x in json_platforms):
            content_type = "application/json"
            payload_to_send = json.dumps(notification.payload)
        else:
            content_type = "application/xml"
            payload_to_send = notification.payload

        headers = {
            'Content-type': content_type,
            'Authorization': self.generate_sas_token(),
            'ServiceBusNotification-Format': notification.format
        }

        if isinstance(tag_or_tag_expression, set):
            tag_list = ' || '.join(tag_or_tag_expression)
        else:
            tag_list = tag_or_tag_expression

        # add hello tags/tag expressions toohello headers collection
        if tag_list != "":
            headers.update({'ServiceBusNotification-Tags': tag_list})

        # add any custom headers toohello headers collection that hello user may have added
        if notification.headers is not None:
            headers.update(notification.headers)

        self.make_http_request(url, payload_to_send, headers)

    def send_apple_notification(self, payload, tags=""):
        nh = Notification("apple", payload)
        self.send_notification(nh, tags)

    def send_gcm_notification(self, payload, tags=""):
        nh = Notification("gcm", payload)
        self.send_notification(nh, tags)

    def send_adm_notification(self, payload, tags=""):
        nh = Notification("adm", payload)
        self.send_notification(nh, tags)

    def send_baidu_notification(self, payload, tags=""):
        nh = Notification("baidu", payload)
        self.send_notification(nh, tags)

    def send_mpns_notification(self, payload, tags=""):
        nh = Notification("windowsphone", payload)

        if "<wp:Toast>" in payload:
            nh.headers = {'X-WindowsPhone-Target': 'toast', 'X-NotificationClass': '2'}
        elif "<wp:Tile>" in payload:
            nh.headers = {'X-WindowsPhone-Target': 'tile', 'X-NotificationClass': '1'}

        self.send_notification(nh, tags)

    def send_windows_notification(self, payload, tags=""):
        nh = Notification("windows", payload)

        if "<toast>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/toast'}
        elif "<tile>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/tile'}
        elif "<badge>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/badge'}

        self.send_notification(nh, tags)

    def send_template_notification(self, properties, tags=""):
        nh = Notification("template", properties)
        self.send_notification(nh, tags)

hello 上述方法傳送通知中樞，hello 正確本文和標頭 toosend hello 通知使用 HTTP POST 要求 toohello /messages 的端點。

### <a name="using-debug-property-tooenable-detailed-logging"></a>使用偵錯屬性 tooenable 詳細記錄
初始化 hello 通知中樞時啟用偵錯屬性會寫出記錄详细 hello HTTP 要求和回應的傾印，以及詳細的通知訊息傳送結果。 我們最近加入此屬性稱為[通知中樞 TestSend 屬性](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx)傳回 hello 通知傳送結果的相關詳細的資訊。 toouse 它-使用 hello 下列初始化：

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

取得結果與 「 測試 」 querystring 附加 hello 通知中樞傳送要求的 HTTP URL。 

## <a name="complete-tutorial"></a>完整的 hello 教學課程
現在您可以透過傳送嗨通知 Python 的後端完成 hello 快速入門教學課程。

初始化您通知中樞的用戶端 (hello 中的指示，以取代 hello 連接字串和中樞名稱[Get 入門教學課程]):

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

然後加入 hello 傳送程式碼取決於目標行動平台。 此範例也會將較高的層級方法 tooenable 傳送 hello 平台，例如 windows; send_windows_notification 為基礎的通知（適用於 apple) send_apple_notification 等等。 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a>Windows 市集和 Windows Phone 8.1 (非 Silverlight)
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a>Windows Phone 8.0 和 8.1 Silverlight
    hub.send_mpns_notification(toast)

### <a name="ios"></a>iOS
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a>Android
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a>Kindle Fire
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a>Baidu
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

執行 Python 程式碼應會產生一則顯示於目標裝置的通知。

## <a name="examples"></a>範例：
### <a name="enabling-debug-property"></a>啟用偵錯屬性
當您將會看到初始化 hello NotificationHub 時啟用偵錯旗標的詳細 HTTP 要求和回應的傾印，以及 NotificationOutcome 類似 hello 下列您可以瞭解哪些 HTTP 標頭會傳入 hello 要求，哪些 HTTP收到 hello 通知中樞的回應：![][1]

您會看到詳細的通知中樞結果，例如 

* 當傳送 hello 訊息成功 toohello 推播通知服務。 
  
        <Outcome>hello Notification was successfully sent toohello Push Notification System</Outcome>
* 如果沒有任何推播通知找不到任何目標，則您可能將 toosee （表示沒有任何註冊可能找到 toodeliver hello 通知，因為 hello 註冊具有一些 hello 回應 hello 下列不相符的標記）
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-toowindows"></a>廣播快顯通知 tooWindows
請注意，當您傳送廣播的快顯通知 tooWindows 用戶端取得送出 hello 標頭。 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a>傳送指定標記 (或標記運算式) 的通知
請注意 hello 標記 HTTP 標頭加入 toohello HTTP 要求 （在 hello 面範例中，我們會傳送 hello 通知只有 tooregistrations '運動' 裝載的）

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a>傳送指定多個標記的通知
請注意 hello 標記 HTTP 標頭如何變更時傳送多個標記。 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a>樣板化通知
請注意，hello 格式為 HTTP 標頭的變更和 hello 裝載主體所傳送 hello HTTP 要求主體的一部分：

**用戶端 - 註冊的範本**

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

**伺服器端的傳送嗨裝載**

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a>後續步驟
本主題中我們也示範了如何 toocreate 簡單 Python 將通知中樞的用戶端。 您可以在這裡執行下列動作：

* 下載完整的 hello [Python REST 包裝函式範例]，其中包含所有上述的 hello 程式碼。
* 繼續了解通知中心 hello 標記功能[即時新聞教學課程]
* 了解相關的通知中樞範本功能繼續在 hello[當地語系化新聞教學課程]

<!-- URLs -->
[Python REST 包裝函式範例]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python
[Get 入門教學課程]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/
[即時新聞教學課程]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/
[當地語系化新聞教學課程]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/

<!-- Images. -->
[1]: ./media/notification-hubs-python-backend-how-to/DetailedLoggingInfo.png
[2]: ./media/notification-hubs-python-backend-how-to/BroadcastScenario.png
[3]: ./media/notification-hubs-python-backend-how-to/SendWithOneTag.png
[4]: ./media/notification-hubs-python-backend-how-to/SendWithMultipleTags.png
[5]: ./media/notification-hubs-python-backend-how-to/TemplatedNotification.png
