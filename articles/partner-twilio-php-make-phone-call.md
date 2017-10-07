---
title: "aaaHow toomake 通話從 Twilio (PHP) |Microsoft 文件"
description: "了解如何 toomake 電話及傳送 SMS 訊息 hello Twilio API 服務在 Azure 上。 範例適用於 PHP 應用程式。"
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 44e35adc-be06-4700-beee-8c9e2c20c540
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: e6fecc345bf9ae787d14d533bd8d96b175c2453b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-php-application-on-azure"></a>如何在 Azure 上的 PHP 應用程式的電話使用 Twilio tooMake
hello 下列範例示範您如何使用 Twilio toomake 從裝載於 Azure 的 PHP 網頁上的呼叫。 hello 產生應用程式會提示 hello 使用者通話值 hello 下列螢幕擷取畫面所示。

![Azure Call Form Using Twilio and PHP][twilio_php]

您將需要 toodo hello 下列 toouse 本主題中的 hello 程式碼：

1. 從您的 [Twilio 主控台][twilio_console]取得 Twilio 帳戶和驗證權杖。 開始使用 Twilio，tooget 評估在定價[http://www.twilio.com/pricing][twilio_pricing]。 您可以在 [https://www.twilio.com/try-twilio][try_twilio] 上註冊試用帳戶。
2. 取得 hello [Twilio for PHP 的程式庫](https://github.com/twilio/twilio-php)或將它安裝為西洋梨封裝。 如需詳細資訊，請參閱 hello[讀我檔案](https://github.com/twilio/twilio-php/blob/master/README.md)。
3. 安裝 hello Azure SDK for PHP。 如需 hello SDK 和安裝指示的概觀，請參閱[hello Azure SDK for PHP 設定](app-service-web/web-sites-php-mysql-deploy-use-git.md)

## <a name="create-a-web-form-for-making-a-call"></a>建立用以撥打電話的 Web 表單
hello 下列 HTML 程式碼示範如何 toobuild 網頁 (**callform.html**)，擷取使用者資料進行呼叫：

```html
<!DOCTYPE html>
<html>
<head>
  <title>Automated call form</title>
</head>
<body>
  <h1>Automated Call Form</h1>
  <p>Fill in all fields and click <b>Make this call</b>.</p>
  <form action="makecall.php" method="post">
    <table>
      <tr>
        <td>To:</td>
        <td><input name="callTo" size="50" type="text" value=""></td>
      </tr>
      <tr>
        <td>From:</td>
        <td><input name="callFrom" size="50" type="text" value=""></td>
      </tr>
      <tr>
        <td>Call message:</td>
        <td><input name="callText" size="100" type="text" value="Hello. This is hello call text. Good bye."></td>
      </tr>
      <tr>
        <td colspan="2"><input type="submit" value="Make this call"></td>
      </tr>
    </table>
  </form><br>
</body>
</html>
```

## <a name="create-hello-code-toomake-hello-call"></a>建立 hello 程式碼 toomake hello 呼叫
hello 下列程式碼會示範如何 toobuild **makecall.php**，稱為 hello 使用者送出 hello 表單顯示時**callform.html**。 hello 如下所示的程式碼會建立 hello 呼叫訊息，並產生 hello 呼叫。 此外，請確定您的 Twilio 帳戶和驗證語彙基元 hello 的 toouse [Twilio 主控台][ twilio_console]而不是太指派 hello 預留位置值**$sid**和**$token** hello 的下列程式碼。

```html
<html>
<head><title>Making call...</title></head>
<body>
<p>Your call is being made.</p>

<?php
require_once 'path/to/vendor/autoload.php';

$sid   = "your_account_sid";
$token = "your_authentication_token";

$from_number = $_POST['callFrom']; // Calls must be made from a registered Twilio number.
$to_number   = $_POST['callTo'];
$message     = $_POST['callText'];

$client = new Twilio\Rest\Client($sid, $token);

$call = $client->calls->create(
            $to_number,
            $from_number,
            array('url' => http://twimlets.com/message?Message=' . urlencode($message))
        );

echo "Call status: " . $call->status . "<br />";
echo "URI resource: " . $call->uri . "<br />";
?>
</body>
</html>
```

此外 toomaking hello 呼叫， **makecall.php**中所示為 hello 圖顯示一些呼叫中繼資料。 如需通話中繼資料的詳細資訊，請參閱 [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties]。

![Azure Call Response Using Twilio and PHP][twilio_php_response]

## <a name="run-hello-application"></a>執行 hello 應用程式
hello 下一個步驟是 toodeploy 您應用程式 tooAzure 網站。 hello 下列文件包含用於建立網站及部署您使用 Git、 FTP 或 WebMatrix 的程式碼 （但並非所有的資訊，在每個發行項無關） hello 資訊：

* [建立 PHP-MySQL Azure 網站並使用 Git 部署](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [建立 PHP-MySQL Azure 網站並使用 FTP 部署](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a>後續步驟
此程式碼提供 tooshow 您基本的功能使用 Twilio 在 Azure 上的 PHP。 在部署之前 tooAzure 在生產環境中的，您可能想要 tooadd 詳細的錯誤處理或其他功能。 例如：

* 而不是使用網頁表單，也可以使用 Azure 儲存體 blob 或 SQL Database toostore 電話號碼，並呼叫的文字。 如需在 PHP 中使用 Azure 儲存體 Blob 的相關資訊，請參閱[搭配使用 Azure 儲存體與 PHP 應用程式][howto_blob_storage_php]。 如需在 PHP 中使用 SQL Database 的相關資訊，請參閱[搭配使用 SQL Database 與 PHP 應用程式][howto_sql_azure_php]。
* hello **makecall.php**程式碼會使用 Twilio 提供的 URL ([http://twimlets.com/message][twimlet_message_url]) tooprovide Twilio 標記語言 (TwiML) 回應，如何通知 Twiliotooproceed hello 呼叫。 例如，可以包含 hello TwiML 傳回`<Say>`正在口語的 toohello 呼叫收件者的文字會產生的指令動詞。 而不是使用 hello Twilio 提供 URL，您可以建置自己服務 toorespond tooTwilio 要求。如需詳細資訊，請參閱[如何 tooUse 語音和簡訊功能的 PHP Twilio][howto_twilio_voice_sms_php]。 如需 TwiML 的詳細資訊，請參閱 [http://www.twilio.com/docs/api/twiml][twiml]；如需 `<Say>` 和其他 Twilio 動詞的詳細資訊，請參閱 [http://www.twilio.com/docs/api/twiml/say][twilio_say]。
* 讀取 hello Twilio 安全性指導方針，在[https://www.twilio.com/docs/security][twilio_docs_security]。

如需 Twilio 的其他資訊，請參閱 [https://www.twilio.com/docs][twilio_docs]。

## <a name="see-also"></a>另請參閱
* [如何 tooUse Twilio 語音和簡訊功能的 PHP](partner-twilio-php-how-to-use-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/docs/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[build_php_azure_app]: http://azurephp.interoperabilitybridges.com/articles/build-and-deploy-a-windows-azure-php-application
[howto_twilio_voice_sms_php]: partner-twilio-php-how-to-use-voice-sms.md
[howto_blob_storage_php]: http://azure.microsoft.com/documentation/articles/storage-php-how-to-use-blobs/
[howto_sql_azure_php]: http://azure.microsoft.com/documentation/articles/sql-database-php-how-to-use/
[twilio_call_properties]: https://www.twilio.com/docs/api/rest/call#instance-properties
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_php]: ./media/partner-twilio-php-make-phone-call/WA_TwilioPHPCallForm.jpg
[twilio_php_response]: ./media/partner-twilio-php-make-phone-call/WA_TwilioPHPMakeCall.jpg
[website-git]: ./web-sites/web-sites-php-mysql-deploy-use-git.md
[website-ftp]: ./web-sites/web-sites-php-mysql-deploy-use-ftp.md
[twilio_php_github]: https://github.com/twilio/twilio-php
