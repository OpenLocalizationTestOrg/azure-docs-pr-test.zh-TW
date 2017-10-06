---
title: "aaaHow toouse 通知中樞與 PHP"
description: "深入了解如何從 PHP 後端 toouse Azure 通知中樞。"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 0156f994-96d0-4878-b07b-49b7be4fd856
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: php
ms.devlang: php
ms.topic: article
ms.date: 06/07/2016
ms.author: yuaxu
ms.openlocfilehash: 6cd426286a684006a07867fcf44a8ff71be7efa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-php"></a><span data-ttu-id="4c396-103">如何 toouse 來自 PHP 的通知中樞</span><span class="sxs-lookup"><span data-stu-id="4c396-103">How toouse Notification Hubs from PHP</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="4c396-104">您可以從 Java/PHP/Ruby 後端存取所有通知中樞功能 hello MSDN 主題中所述，使用 hello 通知中樞 REST 介面[通知中心 REST Api](http://msdn.microsoft.com/library/dn223264.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4c396-104">You can access all Notification Hubs features from a Java/PHP/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

<span data-ttu-id="4c396-105">在本主題中，我們將說明如何：</span><span class="sxs-lookup"><span data-stu-id="4c396-105">In this topic we show how to:</span></span>

* <span data-ttu-id="4c396-106">在 PHP 中建置通知中心功能的 REST 用戶端；</span><span class="sxs-lookup"><span data-stu-id="4c396-106">Build a REST client for Notification Hubs features in PHP;</span></span>
* <span data-ttu-id="4c396-107">請遵循 hello [Get 入門教學課程](notification-hubs-ios-apple-push-notification-apns-get-started.md)您選擇的方式，在 PHP 中實作 hello 後端部分為行動裝置平台。</span><span class="sxs-lookup"><span data-stu-id="4c396-107">Follow hello [Get started tutorial](notification-hubs-ios-apple-push-notification-apns-get-started.md) for your mobile platform of choice, implementing hello back-end portion in PHP.</span></span>

## <a name="client-interface"></a><span data-ttu-id="4c396-108">用戶端介面</span><span class="sxs-lookup"><span data-stu-id="4c396-108">Client interface</span></span>
<span data-ttu-id="4c396-109">hello 主要用戶端介面可以提供相同的方法用於 hello hello [.NET 通知中樞 SDK](http://msdn.microsoft.com/library/jj933431.aspx)，這可讓您 toodirectly 翻譯的所有 hello 教學課程和此站台上目前可用的範例，在 hello hello 社群所貢獻網際網路。</span><span class="sxs-lookup"><span data-stu-id="4c396-109">hello main client interface can provide hello same methods that are available in hello [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx), this will allow you toodirectly translate all hello tutorials and samples currently available on this site, and contributed by hello community on hello internet.</span></span>

<span data-ttu-id="4c396-110">您可以找到所有 hello 程式碼用於 hello [PHP REST 包裝函式範例]。</span><span class="sxs-lookup"><span data-stu-id="4c396-110">You can find all hello code available in hello [PHP REST wrapper sample].</span></span>

<span data-ttu-id="4c396-111">例如，toocreate 用戶端：</span><span class="sxs-lookup"><span data-stu-id="4c396-111">For example, toocreate a client:</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="4c396-112">toosend iOS 原生通知：</span><span class="sxs-lookup"><span data-stu-id="4c396-112">toosend an iOS native notification:</span></span>

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a><span data-ttu-id="4c396-113">實作</span><span class="sxs-lookup"><span data-stu-id="4c396-113">Implementation</span></span>
<span data-ttu-id="4c396-114">如果您還未這樣做，請依照我們[Get 入門教學課程]向上 toohello 您尚未 tooimplement hello 後端的最後一節。</span><span class="sxs-lookup"><span data-stu-id="4c396-114">If you did not already, please follow our [Get started tutorial] up toohello last section where you have tooimplement hello back-end.</span></span>
<span data-ttu-id="4c396-115">此外，如果您想要您可以使用 hello 程式碼從 hello [PHP REST 包裝函式範例]並直接移 toohello[完成 hello 教學課程](#complete-tutorial)> 一節。</span><span class="sxs-lookup"><span data-stu-id="4c396-115">Also, if you want you can use hello code from hello [PHP REST wrapper sample] and go directly toohello [Complete hello tutorial](#complete-tutorial) section.</span></span>

<span data-ttu-id="4c396-116">所有 hello 可找到完整的 REST 包裝函式的詳細資料 tooimplement [MSDN](http://msdn.microsoft.com/library/dn530746.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4c396-116">All hello details tooimplement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="4c396-117">在本節中，我們將說明 hello PHP 實作 hello 主要步驟需要 tooaccess 通知中心 REST 端點：</span><span class="sxs-lookup"><span data-stu-id="4c396-117">In this section we will describe hello PHP implementation of hello main steps required tooaccess Notification Hubs REST endpoints:</span></span>

1. <span data-ttu-id="4c396-118">剖析 hello 連接字串</span><span class="sxs-lookup"><span data-stu-id="4c396-118">Parse hello connection string</span></span>
2. <span data-ttu-id="4c396-119">產生 hello 授權權杖</span><span class="sxs-lookup"><span data-stu-id="4c396-119">Generate hello authorization token</span></span>
3. <span data-ttu-id="4c396-120">執行 hello HTTP 呼叫</span><span class="sxs-lookup"><span data-stu-id="4c396-120">Perform hello HTTP call</span></span>

### <a name="parse-hello-connection-string"></a><span data-ttu-id="4c396-121">剖析 hello 連接字串</span><span class="sxs-lookup"><span data-stu-id="4c396-121">Parse hello connection string</span></span>
<span data-ttu-id="4c396-122">以下是 hello 主要類別實作 hello 用戶端，會剖析 hello 連接字串的建構函式：</span><span class="sxs-lookup"><span data-stu-id="4c396-122">Here is hello main class implementing hello client, whose constructor that parses hello connection string:</span></span>

    class NotificationHub {
        const API_VERSION = "?api-version=2013-10";

        private $endpoint;
        private $hubPath;
        private $sasKeyName;
        private $sasKeyValue;

        function __construct($connectionString, $hubPath) {
            $this->hubPath = $hubPath;

            $this->parseConnectionString($connectionString);
        }

        private function parseConnectionString($connectionString) {
            $parts = explode(";", $connectionString);
            if (sizeof($parts) != 3) {
                throw new Exception("Error parsing connection string: " . $connectionString);
            }

            foreach ($parts as $part) {
                if (strpos($part, "Endpoint") === 0) {
                    $this->endpoint = "https" . substr($part, 11);
                } else if (strpos($part, "SharedAccessKeyName") === 0) {
                    $this->sasKeyName = substr($part, 20);
                } else if (strpos($part, "SharedAccessKey") === 0) {
                    $this->sasKeyValue = substr($part, 16);
                }
            }
        }
    }


### <a name="create-security-token"></a><span data-ttu-id="4c396-123">建立安全性權杖</span><span class="sxs-lookup"><span data-stu-id="4c396-123">Create security token</span></span>
<span data-ttu-id="4c396-124">語彙基元建立 hello 安全性的 hello 詳細資料可用[這裡](http://msdn.microsoft.com/library/dn495627.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4c396-124">hello details of hello security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="4c396-125">hello 下列方法已加入 toobe toohello **NotificationHub**類別 toocreate hello token 基礎 hello hello 目前要求和 hello 認證從 hello 連接字串中擷取的 URI。</span><span class="sxs-lookup"><span data-stu-id="4c396-125">hello following method has toobe added toohello **NotificationHub** class toocreate hello token based on hello URI of hello current request and hello credentials extracted from hello connection string.</span></span>

    private function generateSasToken($uri) {
        $targetUri = strtolower(rawurlencode(strtolower($uri)));

        $expires = time();
        $expiresInMins = 60;
        $expires = $expires + $expiresInMins * 60;
        $toSign = $targetUri . "\n" . $expires;

        $signature = rawurlencode(base64_encode(hash_hmac('sha256', $toSign, $this->sasKeyValue, TRUE)));

        $token = "SharedAccessSignature sr=" . $targetUri . "&sig="
                    . $signature . "&se=" . $expires . "&skn=" . $this->sasKeyName;

        return $token;
    }

### <a name="send-a-notification"></a><span data-ttu-id="4c396-126">傳送通知</span><span class="sxs-lookup"><span data-stu-id="4c396-126">Send a notification</span></span>
<span data-ttu-id="4c396-127">首先，讓我們先定義代表通知的類別。</span><span class="sxs-lookup"><span data-stu-id="4c396-127">First, let us define a class representing a notification.</span></span>

    class Notification {
        public $format;
        public $payload;

        # array with keynames for headers
        # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
        # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
        public $headers;

        function __construct($format, $payload) {
            if (!in_array($format, ["template", "apple", "windows", "gcm", "windowsphone"])) {
                throw new Exception('Invalid format: ' . $format);
            }

            $this->format = $format;
            $this->payload = $payload;
        }
    }

<span data-ttu-id="4c396-128">此類別是原生通知主體的容器，或是一組範本通知案例的屬性，及一組包含格式 (原生平台或範本) 的標頭，以及平台特定屬性 (如 Apple 到期屬性和 WNS 標頭)。</span><span class="sxs-lookup"><span data-stu-id="4c396-128">This class is a container for a native notification body, or a set of properties on case of a template notification, and a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="4c396-129">請參閱 toohello[通知中心 REST Api 文件](http://msdn.microsoft.com/library/dn495827.aspx)和 hello 特定通知平台的格式，針對所有 hello 可用的選項。</span><span class="sxs-lookup"><span data-stu-id="4c396-129">Please refer toohello [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and hello specific notification platforms' formats for all hello options available.</span></span>

<span data-ttu-id="4c396-130">與這個類別為利器，現在我們可以撰寫 hello 傳送嗨內的通知方法**NotificationHub**類別。</span><span class="sxs-lookup"><span data-stu-id="4c396-130">Armed with this class, we can now write hello send notification methods inside of hello **NotificationHub** class.</span></span>

    public function sendNotification($notification, $tagsOrTagExpression="") {
        if (is_array($tagsOrTagExpression)) {
            $tagExpression = implode(" || ", $tagsOrTagExpression);
        } else {
            $tagExpression = $tagsOrTagExpression;
        }

        # build uri
        $uri = $this->endpoint . $this->hubPath . "/messages" . NotificationHub::API_VERSION;
        $ch = curl_init($uri);

        if (in_array($notification->format, ["template", "apple", "gcm"])) {
            $contentType = "application/json";
        } else {
            $contentType = "application/xml";
        }

        $token = $this->generateSasToken($uri);

        $headers = [
            'Authorization: '.$token,
            'Content-Type: '.$contentType,
            'ServiceBusNotification-Format: '.$notification->format
        ];

        if ("" !== $tagExpression) {
            $headers[] = 'ServiceBusNotification-Tags: '.$tagExpression;
        }

        # add headers for other platforms
        if (is_array($notification->headers)) {
            $headers = array_merge($headers, $notification->headers);
        }

        curl_setopt_array($ch, array(
            CURLOPT_POST => TRUE,
            CURLOPT_RETURNTRANSFER => TRUE,
            CURLOPT_SSL_VERIFYPEER => FALSE,
            CURLOPT_HTTPHEADER => $headers,
            CURLOPT_POSTFIELDS => $notification->payload
        ));

        // Send hello request
        $response = curl_exec($ch);

        // Check for errors
        if($response === FALSE){
            throw new Exception(curl_error($ch));
        }

        $info = curl_getinfo($ch);

        if ($info['http_code'] <> 201) {
            throw new Exception('Error sending notificaiton: '. $info['http_code'] . ' msg: ' . $response);
        }
    } 

<span data-ttu-id="4c396-131">hello 上述方法傳送通知中樞，hello 正確本文和標頭 toosend hello 通知使用 HTTP POST 要求 toohello /messages 的端點。</span><span class="sxs-lookup"><span data-stu-id="4c396-131">hello above methods send an HTTP POST request toohello /messages endpoint of your notification hub, with hello correct body and headers toosend hello notification.</span></span>

## <span data-ttu-id="4c396-132"><a name="complete-tutorial"></a>完整的 hello 教學課程</span><span class="sxs-lookup"><span data-stu-id="4c396-132"><a name="complete-tutorial"></a>Complete hello tutorial</span></span>
<span data-ttu-id="4c396-133">現在您可以透過傳送嗨通知 PHP 後端完成 hello 快速入門教學課程。</span><span class="sxs-lookup"><span data-stu-id="4c396-133">Now you can complete hello Get Started tutorial by sending hello notification from a PHP back-end.</span></span>

<span data-ttu-id="4c396-134">初始化您通知中樞的用戶端 (hello 中的指示，以取代 hello 連接字串和中樞名稱[Get 入門教學課程]):</span><span class="sxs-lookup"><span data-stu-id="4c396-134">Initialize your Notification Hubs client (substitute hello connection string and hub name as instructed in hello [Get started tutorial]):</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="4c396-135">然後加入 hello 傳送程式碼取決於目標行動平台。</span><span class="sxs-lookup"><span data-stu-id="4c396-135">Then add hello send code depending on your target mobile platform.</span></span>

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="4c396-136">Windows 市集和 Windows Phone 8.1 (非 Silverlight)</span><span class="sxs-lookup"><span data-stu-id="4c396-136">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a><span data-ttu-id="4c396-137">iOS</span><span class="sxs-lookup"><span data-stu-id="4c396-137">iOS</span></span>
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a><span data-ttu-id="4c396-138">Android</span><span class="sxs-lookup"><span data-stu-id="4c396-138">Android</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="4c396-139">Windows Phone 8.0 和 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="4c396-139">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    $toast = '<?xml version="1.0" encoding="utf-8"?>' .
                '<wp:Notification xmlns:wp="WPNotification">' .
                   '<wp:Toast>' .
                        '<wp:Text1>Hello from PHP!</wp:Text1>' .
                   '</wp:Toast> ' .
                '</wp:Notification>';
    $notification = new Notification("windowsphone", $toast);
    $notification->headers[] = 'X-WindowsPhone-Target : toast';
    $notification->headers[] = 'X-NotificationClass : 2';
    $hub->sendNotification($notification, null);


### <a name="kindle-fire"></a><span data-ttu-id="4c396-140">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="4c396-140">Kindle Fire</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

<span data-ttu-id="4c396-141">執行 PHP 程式碼現在應會產生一則顯示於目標裝置的通知。</span><span class="sxs-lookup"><span data-stu-id="4c396-141">Running your PHP code should produce now a notification appearing on your target device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c396-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4c396-142">Next Steps</span></span>
<span data-ttu-id="4c396-143">本主題中我們也示範了如何 toocreate 簡單 Java 將通知中樞的用戶端。</span><span class="sxs-lookup"><span data-stu-id="4c396-143">In this topic we showed how toocreate a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="4c396-144">您可以在這裡執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="4c396-144">From here you can:</span></span>

* <span data-ttu-id="4c396-145">下載完整的 hello [PHP REST 包裝函式範例]，其中包含所有上述的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="4c396-145">Download hello full [PHP REST wrapper sample], which contains all hello code above.</span></span>
* <span data-ttu-id="4c396-146">繼續了解標記 hello [即時新聞教學課程] 功能的通知中樞</span><span class="sxs-lookup"><span data-stu-id="4c396-146">Continue learning about Notification Hubs tagging feature in hello [Breaking News tutorial]</span></span>
* <span data-ttu-id="4c396-147">深入了解推送通知 tooindividual 使用者在 [通知使用者教學課程]</span><span class="sxs-lookup"><span data-stu-id="4c396-147">Learn about pushing notifications tooindividual users in [Notify Users tutorial]</span></span>

<span data-ttu-id="4c396-148">如需詳細資訊，請參閱 hello [PHP 開發人員中心](/develop/php/)。</span><span class="sxs-lookup"><span data-stu-id="4c396-148">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[PHP REST 包裝函式範例]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php
[Get 入門教學課程]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/

