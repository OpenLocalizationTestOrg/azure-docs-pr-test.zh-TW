---
title: "如何透過 Python 使用通知中樞"
description: "了解如何透過 Python 後端使用 Azure 通知中樞。"
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
ms.openlocfilehash: 9ceedb9940759427fc8cec74a1307e42472563a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-notification-hubs-from-python"></a><span data-ttu-id="4244e-103">如何透過 Python 使用通知中樞</span><span class="sxs-lookup"><span data-stu-id="4244e-103">How to use Notification Hubs from Python</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="4244e-104">您可以使用通知中樞 REST 介面，透過 Java/PHP/Python/Ruby 後端來存取所有通知中樞功能，如 MSDN 主題 [通知中樞 REST API](http://msdn.microsoft.com/library/dn223264.aspx)所述。</span><span class="sxs-lookup"><span data-stu-id="4244e-104">You can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="4244e-105">這是在 Python 實作通知傳送的範例參考實作，並非正式支援的通知中樞 Python SDK。</span><span class="sxs-lookup"><span data-stu-id="4244e-105">This is a sample reference implementation for implementing the notification sends in Python and is not the officially supported Notifications Hub Python SDK.</span></span>
> 
> <span data-ttu-id="4244e-106">這個範例是使用 Python 3.4 撰寫的。</span><span class="sxs-lookup"><span data-stu-id="4244e-106">This sample is written using Python 3.4.</span></span>
> 
> 

<span data-ttu-id="4244e-107">在本主題中，我們將說明如何：</span><span class="sxs-lookup"><span data-stu-id="4244e-107">In this topic we show how to:</span></span>

* <span data-ttu-id="4244e-108">在 Python 中建置通知中樞功能的 REST 用戶端。</span><span class="sxs-lookup"><span data-stu-id="4244e-108">Build a REST client for Notification Hubs features in Python.</span></span>
* <span data-ttu-id="4244e-109">使用 Python 介面傳送通知到通知中樞 REST API。</span><span class="sxs-lookup"><span data-stu-id="4244e-109">Send notifications using the Python interface to the Notification Hub REST APIs.</span></span> 
* <span data-ttu-id="4244e-110">取得 HTTP REST 要求/回應的傾印以用於偵錯/教學用途。</span><span class="sxs-lookup"><span data-stu-id="4244e-110">Get a dump of the HTTP REST request/response for debugging/educational purpose.</span></span> 

<span data-ttu-id="4244e-111">您可以遵循選定行動平台的 [開始使用教學課程](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) 來實作 Python 的後端部分。</span><span class="sxs-lookup"><span data-stu-id="4244e-111">You can follow the [Get started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) for your mobile platform of choice, implementing the back-end portion in Python.</span></span>

> [!NOTE]
> <span data-ttu-id="4244e-112">此範例的範圍僅限於傳送通知，不會執行任何註冊管理。</span><span class="sxs-lookup"><span data-stu-id="4244e-112">The scope of the sample is only limited to send notifications and it doesn't do any registration management.</span></span>
> 
> 

## <a name="client-interface"></a><span data-ttu-id="4244e-113">用戶端介面</span><span class="sxs-lookup"><span data-stu-id="4244e-113">Client interface</span></span>
<span data-ttu-id="4244e-114">主要用戶端介面提供的方法與 [.NET 通知中樞 SDK](http://msdn.microsoft.com/library/jj933431.aspx)中的方法相同。</span><span class="sxs-lookup"><span data-stu-id="4244e-114">The main client interface can provide the same methods that are available in the [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx).</span></span> <span data-ttu-id="4244e-115">這可讓您直接轉換目前此網站上和網際網路社群所貢獻的所有教學課程和範例。</span><span class="sxs-lookup"><span data-stu-id="4244e-115">This will allow you to directly translate all the tutorials and samples currently available on this site, and contributed by the community on the internet.</span></span>

<span data-ttu-id="4244e-116">您可在 [Python REST 包裝函式範例]中找到所有可用的程式碼。</span><span class="sxs-lookup"><span data-stu-id="4244e-116">You can find all the code available in the [Python REST wrapper sample].</span></span>

<span data-ttu-id="4244e-117">例如，若要建立用戶端：</span><span class="sxs-lookup"><span data-stu-id="4244e-117">For example, to create a client:</span></span>

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="4244e-118">傳送 Windows 快顯通知：</span><span class="sxs-lookup"><span data-stu-id="4244e-118">To send a Windows toast notification:</span></span>

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a><span data-ttu-id="4244e-119">實作</span><span class="sxs-lookup"><span data-stu-id="4244e-119">Implementation</span></span>
<span data-ttu-id="4244e-120">如果您尚未執行此作業，請遵循 [開始使用教學課程] 的指示，進行到您必須實作後端的最後一節。</span><span class="sxs-lookup"><span data-stu-id="4244e-120">If you did not already, please follow our [Get started tutorial] up to the last section where you have to implement the back-end.</span></span>

<span data-ttu-id="4244e-121">您可以在 [MSDN](http://msdn.microsoft.com/library/dn530746.aspx)上找到所有實作完整 REST 包裝函式的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4244e-121">All the details to implement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="4244e-122">在本節中，我們將針對存取通知中樞 REST 端點和傳送通知所需之主要步驟的 Python 實作進行說明：</span><span class="sxs-lookup"><span data-stu-id="4244e-122">In this section we will describe the Python implementation of the main steps required to access Notification Hubs REST endpoints and send notifications</span></span>

1. <span data-ttu-id="4244e-123">解析連接字串</span><span class="sxs-lookup"><span data-stu-id="4244e-123">Parse the connection string</span></span>
2. <span data-ttu-id="4244e-124">產生授權權杖</span><span class="sxs-lookup"><span data-stu-id="4244e-124">Generate the authorization token</span></span>
3. <span data-ttu-id="4244e-125">使用 HTTP REST API 傳送通知</span><span class="sxs-lookup"><span data-stu-id="4244e-125">Send a notification using HTTP REST API</span></span>

### <a name="parse-the-connection-string"></a><span data-ttu-id="4244e-126">解析連接字串</span><span class="sxs-lookup"><span data-stu-id="4244e-126">Parse the connection string</span></span>
<span data-ttu-id="4244e-127">以下是實作其建構函式可解析連接字串之用戶端的主要類別：</span><span class="sxs-lookup"><span data-stu-id="4244e-127">Here is the main class implementing the client, whose constructor parses the connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="4244e-128">建立安全性權杖</span><span class="sxs-lookup"><span data-stu-id="4244e-128">Create security token</span></span>
<span data-ttu-id="4244e-129">您可以在 [此處](http://msdn.microsoft.com/library/dn495627.aspx)找到建立安全性權杖的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4244e-129">The details of the security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="4244e-130">必須將下列方法新增至 **NotificationHub** 類別，才能依據目前要求的 URI 和從連接字串擷取的認證建立權杖。</span><span class="sxs-lookup"><span data-stu-id="4244e-130">The following methods have to be added to the **NotificationHub** class to create the token based on the URI of the current request and the credentials extracted from the connection string.</span></span>

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

### <a name="send-a-notification-using-http-rest-api"></a><span data-ttu-id="4244e-131">使用 HTTP REST API 傳送通知</span><span class="sxs-lookup"><span data-stu-id="4244e-131">Send a notification using HTTP REST API</span></span>
<span data-ttu-id="4244e-132">首先，讓我們先定義呈現通知的類別。</span><span class="sxs-lookup"><span data-stu-id="4244e-132">First, let use define a class representing a notification.</span></span>

    class Notification:
        def __init__(self, notification_format=None, payload=None, debug=0):
            valid_formats = ['template', 'apple', 'gcm', 'windows', 'windowsphone', "adm", "baidu"]
            if not any(x in notification_format for x in valid_formats):
                raise Exception(
                    "Invalid Notification format. " +
                    "Must be one of the following - 'template', 'apple', 'gcm', 'windows', 'windowsphone', 'adm', 'baidu'")

            self.format = notification_format
            self.payload = payload

            # array with keynames for headers
            # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
            # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry
            # in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
            self.headers = None

<span data-ttu-id="4244e-133">此類別是原生通知主體的容器，或是一組範本通知案例的屬性，及一組包含格式 (原生平台或範本) 的標頭，以及平台特定屬性 (如 Apple 到期屬性和 WNS 標頭)。</span><span class="sxs-lookup"><span data-stu-id="4244e-133">This class is a container for a native notification body or a set of properties in case of a template notification, a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="4244e-134">請參閱 [通知中心 REST API 文件](http://msdn.microsoft.com/library/dn495827.aspx) 及特定通知平台的格式，以取得所有可用選項。</span><span class="sxs-lookup"><span data-stu-id="4244e-134">Please refer to the [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and the specific notification platforms' formats for all the options available.</span></span>

<span data-ttu-id="4244e-135">有了此類別之後，我們現在可以在 **NotificationHub** 類別內寫入傳送通知方法。</span><span class="sxs-lookup"><span data-stu-id="4244e-135">Now with this class, we can write the send notification methods inside of the **NotificationHub** class.</span></span>

    def make_http_request(self, url, payload, headers):
        parsed_url = urllib.parse.urlparse(url)
        connection = http.client.HTTPSConnection(parsed_url.hostname, parsed_url.port)

        if self.Debug > 0:
            connection.set_debuglevel(self.Debug)
            # adding this querystring parameter gets detailed information about the PNS send notification outcome
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

        # add the tags/tag expressions to the headers collection
        if tag_list != "":
            headers.update({'ServiceBusNotification-Tags': tag_list})

        # add any custom headers to the headers collection that the user may have added
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

<span data-ttu-id="4244e-136">上述方法會傳送 HTTP POST 要求至通知中心的 /messages 端點，並使用正確的主體和標頭傳送通知。</span><span class="sxs-lookup"><span data-stu-id="4244e-136">The above methods send an HTTP POST request to the /messages endpoint of your notification hub, with the correct body and headers to send the notification.</span></span>

### <a name="using-debug-property-to-enable-detailed-logging"></a><span data-ttu-id="4244e-137">使用偵錯屬性啟用詳細的記錄</span><span class="sxs-lookup"><span data-stu-id="4244e-137">Using debug property to enable detailed logging</span></span>
<span data-ttu-id="4244e-138">在初始化通知中樞時啟用偵錯屬性會寫出關於 HTTP 要求和回應傾印的詳細記錄資訊，以及詳細的通知訊息傳送結果。</span><span class="sxs-lookup"><span data-stu-id="4244e-138">Enabling debug property while initializing the Notification Hub will write out detailed logging information about the HTTP request and response dump as well as detailed Notification message send outcome.</span></span> <span data-ttu-id="4244e-139">我們近期新增了稱為 [通知中樞 TestSend 屬性](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) 的屬性，該屬性會傳回關於通知傳送結果的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="4244e-139">We recently added this property called [Notification Hubs TestSend property](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) which returns detailed information about the notification send outcome.</span></span> <span data-ttu-id="4244e-140">若要使用它 - 請使用下列命令初始化：</span><span class="sxs-lookup"><span data-stu-id="4244e-140">To use it - initialize using the following:</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="4244e-141">通知中樞傳送要求 HTTP URL 會附加 "test" 查詢字串做為結果。</span><span class="sxs-lookup"><span data-stu-id="4244e-141">The Notification Hub Send request HTTP URL gets appended with a "test" querystring as a result.</span></span> 

## <span data-ttu-id="4244e-142"><a name="complete-tutorial"></a>完成教學課程</span><span class="sxs-lookup"><span data-stu-id="4244e-142"><a name="complete-tutorial"></a>Complete the tutorial</span></span>
<span data-ttu-id="4244e-143">現在您可以透過從 Python 後端傳送通知，來完成開始使用教學課程。</span><span class="sxs-lookup"><span data-stu-id="4244e-143">Now you can complete the Get Started tutorial by sending the notification from a Python back-end.</span></span>

<span data-ttu-id="4244e-144">初始化您的通知中樞用戶端 (請依 [開始使用教學課程]中的指示替換連接字串和中心名稱)：</span><span class="sxs-lookup"><span data-stu-id="4244e-144">Initialize your Notification Hubs client (substitute the connection string and hub name as instructed in the [Get started tutorial]):</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

<span data-ttu-id="4244e-145">然後根據您的目標行動平台新增傳送程式碼。</span><span class="sxs-lookup"><span data-stu-id="4244e-145">Then add the send code depending on your target mobile platform.</span></span> <span data-ttu-id="4244e-146">此範例也會新增更高層級的方法以依據平台傳送通知，例如，Windows 為 send_windows_notification；Apple 為 send_apple_notification 等等。</span><span class="sxs-lookup"><span data-stu-id="4244e-146">This sample also adds higher level methods to enable sending notifications based on the platform e.g. send_windows_notification for windows; send_apple_notification (for apple) etc.</span></span> 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="4244e-147">Windows 市集和 Windows Phone 8.1 (非 Silverlight)</span><span class="sxs-lookup"><span data-stu-id="4244e-147">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="4244e-148">Windows Phone 8.0 和 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="4244e-148">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    hub.send_mpns_notification(toast)

### <a name="ios"></a><span data-ttu-id="4244e-149">iOS</span><span class="sxs-lookup"><span data-stu-id="4244e-149">iOS</span></span>
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a><span data-ttu-id="4244e-150">Android</span><span class="sxs-lookup"><span data-stu-id="4244e-150">Android</span></span>
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a><span data-ttu-id="4244e-151">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="4244e-151">Kindle Fire</span></span>
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a><span data-ttu-id="4244e-152">Baidu</span><span class="sxs-lookup"><span data-stu-id="4244e-152">Baidu</span></span>
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

<span data-ttu-id="4244e-153">執行 Python 程式碼應會產生一則顯示於目標裝置的通知。</span><span class="sxs-lookup"><span data-stu-id="4244e-153">Running your Python code should produce a notification appearing on your target device.</span></span>

## <a name="examples"></a><span data-ttu-id="4244e-154">範例：</span><span class="sxs-lookup"><span data-stu-id="4244e-154">Examples:</span></span>
### <a name="enabling-debug-property"></a><span data-ttu-id="4244e-155">啟用偵錯屬性</span><span class="sxs-lookup"><span data-stu-id="4244e-155">Enabling debug property</span></span>
<span data-ttu-id="4244e-156">若在初始化 NotificationHub 時啟用偵錯旗標，您會看到詳細的 HTTP 要求和回應傾印，還有類似以下的 NotificationOutcome，您可從中了解在要求中傳送的 HTTP 標頭，以及從通知中樞收到的 HTTP 回應：![][1]</span><span class="sxs-lookup"><span data-stu-id="4244e-156">When you enable debug flag while initializing the NotificationHub then you will see detailed HTTP request and response dump as well as NotificationOutcome like the following where you can understand what HTTP headers are passed in the request and what HTTP response was received from the Notification Hub: ![][1]</span></span>

<span data-ttu-id="4244e-157">您會看到詳細的通知中樞結果，例如</span><span class="sxs-lookup"><span data-stu-id="4244e-157">You will see detailed Notification Hub result e.g.</span></span> 

* <span data-ttu-id="4244e-158">訊息成功傳送至推播通知服務的時間。</span><span class="sxs-lookup"><span data-stu-id="4244e-158">when the message is successfully sent to the Push Notification Service.</span></span> 
  
        <Outcome>The Notification was successfully sent to the Push Notification System</Outcome>
* <span data-ttu-id="4244e-159">如果找不到任何推播通知的目標，您可能會在回應中看到下列內容 (表示找不到可傳遞通知的註冊，可能是因為註冊有一些不相符的標記)</span><span class="sxs-lookup"><span data-stu-id="4244e-159">If there were no targets found for any push notification then you are likely going to see the following in the response (which indicates that there were no registrations found to deliver the notification probably because the registrations had some mismatched tags)</span></span>
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-to-windows"></a><span data-ttu-id="4244e-160">廣播快顯通知給 Windows</span><span class="sxs-lookup"><span data-stu-id="4244e-160">Broadcast toast notification to Windows</span></span>
<span data-ttu-id="4244e-161">請注意當您傳送廣播快顯通知給 Windows 用戶端時所送出的標頭。</span><span class="sxs-lookup"><span data-stu-id="4244e-161">Notice the headers that get sent out when you are sending a broadcast toast notification to Windows client.</span></span> 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a><span data-ttu-id="4244e-162">傳送指定標記 (或標記運算式) 的通知</span><span class="sxs-lookup"><span data-stu-id="4244e-162">Send notification specifying a tag (or tag expression)</span></span>
<span data-ttu-id="4244e-163">請注意新增至 HTTP 要求的 Tags HTTP 標頭 (在下列範例中，我們只將通知傳送給含有 'sports' 承載的註冊)</span><span class="sxs-lookup"><span data-stu-id="4244e-163">Notice the Tags HTTP header which gets added to the HTTP request (in the example below, we are sending the notification only to registrations with 'sports' payload)</span></span>

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a><span data-ttu-id="4244e-164">傳送指定多個標記的通知</span><span class="sxs-lookup"><span data-stu-id="4244e-164">Send notification specifying multiple tags</span></span>
<span data-ttu-id="4244e-165">請注意傳送多個標記時的 Tags HTTP 標頭如何變更</span><span class="sxs-lookup"><span data-stu-id="4244e-165">Notice how the Tags HTTP header changes when multiple tags are sent.</span></span> 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a><span data-ttu-id="4244e-166">樣板化通知</span><span class="sxs-lookup"><span data-stu-id="4244e-166">Templated notification</span></span>
<span data-ttu-id="4244e-167">請注意，Format HTTP 標頭會變更，承載主體則會傳送為 HTTP 要求主體的一部分：</span><span class="sxs-lookup"><span data-stu-id="4244e-167">Notice that the Format HTTP header changes and the payload body is sent as part of the HTTP request body:</span></span>

<span data-ttu-id="4244e-168">**用戶端 - 註冊的範本**</span><span class="sxs-lookup"><span data-stu-id="4244e-168">**Client side - registered template**</span></span>

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

<span data-ttu-id="4244e-169">**伺服器端 - 傳送承載**</span><span class="sxs-lookup"><span data-stu-id="4244e-169">**Server side - sending the payload**</span></span>

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a><span data-ttu-id="4244e-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4244e-170">Next Steps</span></span>
<span data-ttu-id="4244e-171">在本主題中，我們會說明如何為通知中樞建立簡單的 Python REST 用戶端。</span><span class="sxs-lookup"><span data-stu-id="4244e-171">In this topic we showed how to create a simple Python REST client for Notification Hubs.</span></span> <span data-ttu-id="4244e-172">您可以在這裡執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="4244e-172">From here you can:</span></span>

* <span data-ttu-id="4244e-173">下載完整的 [Python REST 包裝函式範例]，其中包含上述所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="4244e-173">Download the full [Python REST wrapper sample], which contains all the code above.</span></span>
* <span data-ttu-id="4244e-174">繼續了解 [即時新聞教學課程]</span><span class="sxs-lookup"><span data-stu-id="4244e-174">Continue learning about Notification Hubs tagging feature in the [Breaking News tutorial]</span></span>
* <span data-ttu-id="4244e-175">繼續了解 [當地語系化新聞教學課程]</span><span class="sxs-lookup"><span data-stu-id="4244e-175">Continue learning about Notification Hubs Templates feature in the [Localizing News tutorial]</span></span>

<!-- URLs -->
<span data-ttu-id="4244e-176">[Python REST 包裝函式範例]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python</span><span class="sxs-lookup"><span data-stu-id="4244e-176">[Python REST wrapper sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python</span></span>
<span data-ttu-id="4244e-177">[開始使用教學課程]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span><span class="sxs-lookup"><span data-stu-id="4244e-177">[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span></span>
<span data-ttu-id="4244e-178">[即時新聞教學課程]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/</span><span class="sxs-lookup"><span data-stu-id="4244e-178">[Breaking News tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/</span></span>
<span data-ttu-id="4244e-179">[當地語系化新聞教學課程]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/</span><span class="sxs-lookup"><span data-stu-id="4244e-179">[Localizing News tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-python-backend-how-to/DetailedLoggingInfo.png
[2]: ./media/notification-hubs-python-backend-how-to/BroadcastScenario.png
[3]: ./media/notification-hubs-python-backend-how-to/SendWithOneTag.png
[4]: ./media/notification-hubs-python-backend-how-to/SendWithMultipleTags.png
[5]: ./media/notification-hubs-python-backend-how-to/TemplatedNotification.png

