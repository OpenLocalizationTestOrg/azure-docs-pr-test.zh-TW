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
# <a name="how-toouse-notification-hubs-from-php"></a>如何 toouse 來自 PHP 的通知中樞
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

您可以從 Java/PHP/Ruby 後端存取所有通知中樞功能 hello MSDN 主題中所述，使用 hello 通知中樞 REST 介面[通知中心 REST Api](http://msdn.microsoft.com/library/dn223264.aspx)。

在本主題中，我們將說明如何：

* 在 PHP 中建置通知中心功能的 REST 用戶端；
* 請遵循 hello [Get 入門教學課程](notification-hubs-ios-apple-push-notification-apns-get-started.md)您選擇的方式，在 PHP 中實作 hello 後端部分為行動裝置平台。

## <a name="client-interface"></a>用戶端介面
hello 主要用戶端介面可以提供相同的方法用於 hello hello [.NET 通知中樞 SDK](http://msdn.microsoft.com/library/jj933431.aspx)，這可讓您 toodirectly 翻譯的所有 hello 教學課程和此站台上目前可用的範例，在 hello hello 社群所貢獻網際網路。

您可以找到所有 hello 程式碼用於 hello [PHP REST 包裝函式範例]。

例如，toocreate 用戶端：

    $hub = new NotificationHub("connection string", "hubname");    

toosend iOS 原生通知：

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a>實作
如果您還未這樣做，請依照我們[Get 入門教學課程]向上 toohello 您尚未 tooimplement hello 後端的最後一節。
此外，如果您想要您可以使用 hello 程式碼從 hello [PHP REST 包裝函式範例]並直接移 toohello[完成 hello 教學課程](#complete-tutorial)> 一節。

所有 hello 可找到完整的 REST 包裝函式的詳細資料 tooimplement [MSDN](http://msdn.microsoft.com/library/dn530746.aspx)。 在本節中，我們將說明 hello PHP 實作 hello 主要步驟需要 tooaccess 通知中心 REST 端點：

1. 剖析 hello 連接字串
2. 產生 hello 授權權杖
3. 執行 hello HTTP 呼叫

### <a name="parse-hello-connection-string"></a>剖析 hello 連接字串
以下是 hello 主要類別實作 hello 用戶端，會剖析 hello 連接字串的建構函式：

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


### <a name="create-security-token"></a>建立安全性權杖
語彙基元建立 hello 安全性的 hello 詳細資料可用[這裡](http://msdn.microsoft.com/library/dn495627.aspx)。
hello 下列方法已加入 toobe toohello **NotificationHub**類別 toocreate hello token 基礎 hello hello 目前要求和 hello 認證從 hello 連接字串中擷取的 URI。

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

### <a name="send-a-notification"></a>傳送通知
首先，讓我們先定義代表通知的類別。

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

此類別是原生通知主體的容器，或是一組範本通知案例的屬性，及一組包含格式 (原生平台或範本) 的標頭，以及平台特定屬性 (如 Apple 到期屬性和 WNS 標頭)。

請參閱 toohello[通知中心 REST Api 文件](http://msdn.microsoft.com/library/dn495827.aspx)和 hello 特定通知平台的格式，針對所有 hello 可用的選項。

與這個類別為利器，現在我們可以撰寫 hello 傳送嗨內的通知方法**NotificationHub**類別。

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

hello 上述方法傳送通知中樞，hello 正確本文和標頭 toosend hello 通知使用 HTTP POST 要求 toohello /messages 的端點。

## <a name="complete-tutorial"></a>完整的 hello 教學課程
現在您可以透過傳送嗨通知 PHP 後端完成 hello 快速入門教學課程。

初始化您通知中樞的用戶端 (hello 中的指示，以取代 hello 連接字串和中樞名稱[Get 入門教學課程]):

    $hub = new NotificationHub("connection string", "hubname");    

然後加入 hello 傳送程式碼取決於目標行動平台。

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a>Windows 市集和 Windows Phone 8.1 (非 Silverlight)
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a>iOS
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a>Android
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a>Windows Phone 8.0 和 8.1 Silverlight
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


### <a name="kindle-fire"></a>Kindle Fire
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

執行 PHP 程式碼現在應會產生一則顯示於目標裝置的通知。

## <a name="next-steps"></a>後續步驟
本主題中我們也示範了如何 toocreate 簡單 Java 將通知中樞的用戶端。 您可以在這裡執行下列動作：

* 下載完整的 hello [PHP REST 包裝函式範例]，其中包含所有上述的 hello 程式碼。
* 繼續了解標記 hello [即時新聞教學課程] 功能的通知中樞
* 深入了解推送通知 tooindividual 使用者在 [通知使用者教學課程]

如需詳細資訊，請參閱 hello [PHP 開發人員中心](/develop/php/)。

[PHP REST 包裝函式範例]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php
[Get 入門教學課程]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/

