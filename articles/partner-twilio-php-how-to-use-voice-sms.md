---
title: "aaaHow tooUse Twilio 語音和 SMS (PHP) |Microsoft 文件"
description: "了解如何 toomake 電話及傳送 SMS 訊息 hello Twilio API 服務在 Azure 上。 程式碼範例以 PHP 撰寫。"
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 007f22e3-ac75-4868-8315-da000c2e0dd0
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 9354df8de694826a0ff7ea92620ec4d7e5c2fd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-php"></a>如何 tooUse Twilio 語音和簡訊功能的 PHP
本指南示範如何 tooperform 常見的程式設計工作以 hello Twilio API 服務在 Azure 上。 涵蓋的 hello 案例包括撥電話及傳送短訊息服務 (SMS) 訊息。 如需有關 Twilio 和您的應用程式中使用語音和 SMS 的詳細資訊，請參閱 hello[接下來的步驟](#NextSteps)> 一節。

## <a id="WhatIs"></a>什麼是 Twilio？
Twilio 是及支援的業務通訊的 hello 未來、 啟用開發人員 tooembed 語音 VoIP 及訊息加入應用程式。 這些虛擬化在雲端為基礎、 全域環境中，公開透過 hello Twilio 通訊 API 平台所需的所有基礎結構。 應用程式是簡單 toobuild 及擴充。 享受隨收隨付定價的彈性和雲端可靠性的好處。

**Twilio 語音**可讓您的應用程式 toomake 撥打與接聽電話。 **Twilio SMS**可讓您的應用程式 toosend 及接收文字訊息。 **Twilio 用戶端**可讓您從任何電話、 平板電腦或瀏覽器 toomake VoIP 呼叫，並支援 WebRTC。

## <a id="Pricing"></a>Twilio 定價和特別優惠
升級 Twilio 帳戶的 Azure 客戶，可[特別獲贈](http://www.twilio.com/azure)價值 $10 的 Twilio 點數。 此 Twilio 信用額度可以套用的 tooany Twilio 使用量 ($10 信用相等 toosending 多達 1000 SMS 訊息或接收向上 too1000 輸入語音分鐘，視您的電話號碼和訊息或呼叫目的地的 hello 位置而定)。 請至 [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure)兌換 Twilio 點數來開始使用。

Twilio 是隨收隨付的服務。 不需要設定費，隨時都可結清帳戶。 如需詳細資訊，請參閱 [Twilio 價格][twilio_pricing]。

## <a id="Concepts"></a>概念
hello Twilio API 是 rest 式 API，應用程式提供語音和 SMS 功能。 用戶端程式庫有多種語言版本，相關清單請參閱 [Twilio API 程式庫][twilio_libraries]。

Hello Twilio API 的重要層面是 Twilio 動詞和 Twilio 標記語言 (TwiML)。

### <a id="Verbs"></a>Twilio 動詞
hello API 會使用 Twilio 動詞命令。例如，hello **&lt;說&gt;**動詞命令會指示 Twilio tooaudibly 傳遞的訊息上呼叫。

hello 如下的 Twilio 指令動詞的清單。 深入了解 hello 其他動詞命令和功能，透過[Twilio 標記語言的文件](http://www.twilio.com/docs/api/twiml)。

* **&lt;撥號&gt;**： 連接 hello 呼叫端 tooanother 電話。
* **&lt;收集&gt;**： 會收集輸入 hello 電話字鍵台上的數字。
* **&lt;掛斷&gt;**：結束通話。
* **&lt;播放&gt;**：播放音訊檔案。
* **&lt;暫停&gt;**：靜候一段指定的秒數。
* **&lt;記錄&gt;**： 記錄 hello 呼叫者的語音，並傳回包含 hello 記錄檔的 URL。
* **&lt;重新導向&gt;**： 控制權的通話或 SMS toohello TwiML 於不同的 URL。
* **&lt;拒絕&gt;**： 拒絕傳入的呼叫未使用計費您 tooyour Twilio 數目
* **&lt;說出&gt;**： 將文字 toospeech 所做的呼叫上。
* **&lt;Sms&gt;**：傳送簡訊。

### <a id="TwiML"></a>TwiML
TwiML 是以 XML 為基礎的指示，就會通知方式的 Twilio hello Twilio 動詞命令為基礎的一組 tooprocess 通話或 SMS。

例如，下列 TwiML hello 將轉換的 hello 文字**Hello World** toospeech。

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

當您的應用程式呼叫 hello Twilio 應用程式開發介面時，其中 hello API 參數會是傳回 hello TwiML 回應 hello URL。 供開發應用程式，您可以使用您的應用程式所使用的 Twilio 提供 Url tooprovide hello TwiML 回應。 您也可以裝載自己 Url tooproduce hello TwiML 回應，和另一個選項是 toouse hello **TwiMLResponse**物件。

如需 Twilio 動詞、屬性和 TwiML 的詳細資訊，請參閱 [TwiML][twiml]。 如需 hello Twilio API 的詳細資訊，請參閱[Twilio API][twilio_api]。

## <a id="CreateAccount"></a>建立 Twilio 帳戶
當你準備好 tooget Twilio 帳戶時，請在註冊[再試一次 Twilio][try_twilio]。 您可以先使用免費帳戶，稍後再升級帳戶。

註冊 Twilio 帳戶時，您會收到帳戶識別碼和驗證權杖。 同時會為所需的 toomake Twilio API 呼叫。 tooprevent 未經授權存取 tooyour 帳戶，讓驗證權杖的安全。 您的帳戶識別碼和驗證權杖皆可檢視在 hello [Twilio 帳戶 頁面上][twilio_account]，請在 hello 欄位標示為**帳戶 SID**和**驗證語彙基元**分別。

## <a id="create_app"></a>建立 PHP 應用程式
PHP 應用程式使用 hello Twilio 服務，且在 Azure 中執行並無不同 hello Twilio 服務會使用任何其他 PHP 應用程式。 雖然 Twilio 服務是以 REST 為基礎，並可從 PHP 呼叫數種方式，本文將著重在如何 toouse Twilio 服務使用[Twilio 程式庫從 GitHub PHP][twilio_php]。 如需使用 PHP hello Twilio 程式庫的詳細資訊，請參閱[http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs]。

詳細的指示，用於建置及部署 Twilio/PHP 應用程式 tooAzure 位於[如何在 Azure 上的 PHP 應用程式的電話使用 Twilio tooMake][howto_phonecall_php]。

## <a id="configure_app"></a>設定您的應用程式 tooUse Twilio 文件庫
您可以設定 PHP 應用程式 toouse hello Twilio 庫有兩種：

1. 適用於 PHP 從 GitHub 下載 hello Twilio 程式庫 ([https://github.com/twilio/twilio-php][twilio_php]) 和新增 hello**服務**directory tooyour 應用程式。
   
    -或-
2. 安裝 PHP 的西洋梨套件 hello Twilio 程式庫。 它可以安裝以 hello 下列命令：
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

一旦您的 PHP 安裝 hello Twilio 程式庫，然後您可以加入**require_once**陳述式，在您的 PHP hello 頂端檔案 tooreference hello 程式庫：

        require_once 'Services/Twilio.php';

如需詳細資訊，請參閱[https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme]。

## <a id="howto_make_call"></a>作法：撥出電話
hello 下列範例示範如何 toomake 傳出呼叫使用 hello **Services_Twilio**類別。 此程式碼也會使用 Twilio 提供站台 tooreturn hello Twilio 標記語言 (TwiML) 回應。 替換為您的值為 hello**從**和**至**電話號碼，並確保您確認 hello**從**電話號碼您 Twilio 帳戶先前 toorunning hello 撰寫程式碼。

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // hello number of hello phone initiating hello hello call.
    $from_number = "NNNNNNNNNNN";

    // hello number of hello phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use hello Twilio-provided site for hello TwiML response.
    $url = "http://twimlets.com/message";

    // hello phone message text.
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make hello call.
    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

如前所述，此程式碼會使用 Twilio 提供站台 tooreturn hello TwiML 回應。 您可以改為使用您自己的站台 tooprovide hello TwiML 回應。如需詳細資訊，請參閱[如何 tooProvide TwiML 回應從您自己網站](#howto_provide_twiml_responses)。

* **請注意**: tootroubleshoot SSL 憑證驗證錯誤，請參閱[http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation] 

## <a id="howto_send_sms"></a>作法：傳送簡訊
hello 下列範例示範如何 toosend SMS 訊息使用 hello **Services_Twilio**類別。 hello**從**數目由 Twilio 為試用版帳戶 toosend SMS 訊息。 hello**至**數目必須驗證您 Twilio 帳戶先前 toorunning hello 撰寫程式碼。

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send hello SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <a id="howto_provide_twiml_responses"></a>作法：從您自己的網站提供 TwiML 回應
當您的應用程式啟動呼叫 toohello Twilio 應用程式開發介面時，會傳送 Twilio，是您要求 tooa URL 必須是 tooreturn TwiML 回應。 上述的 hello 範例會使用 hello Twilio 提供 URL [http://twimlets.com/message][twimlet_message_url]。 (雖然 TwiML 的 Twilio 設計使用，您可以檢視 hello 瀏覽器中。 例如，按一下[http://twimlets.com/message] [ twimlet_message_url] toosee 空`<Response>`項目，另一個範例中，按一下 [ [http://twimlets.com/message?訊息 %5B0 %5 D = Hello %20world] [ twimlet_message_url_hello_world] toosee`<Response>`包含項目`<Say>`項目。)

而不是依賴 hello Twilio 提供 URL，您可以建立您自己會傳回 HTTP 回應的網站。 您可以建立 hello 網站中的任何語言，傳回 XML 回應。本主題假設您將會使用 PHP toocreate hello TwiML。

hello 遵循 PHP 頁面結果以指出 TwiML 回應**Hello World** hello 呼叫。

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

您可以看到從 hello 上述範例中，hello TwiML 回應是只是 XML 文件。 適用於 PHP 的 hello Twilio 程式庫包含類別，會為您產生 TwiML。 hello 下面範例會產生 hello 相等回應，如上所示，但使用 hello**服務\_Twilio\_Twiml** hello PHP 的 Twilio 文件庫中的類別：

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

如需 TwiML 的詳細資訊，請參閱 [https://www.twilio.com/docs/api/twiml][twiml_reference]。 

一旦您的 PHP 頁面設定 tooprovide TwiML 回應，做為 hello hello PHP 網頁 URL hello URL 傳入 hello`Services_Twilio->account->calls->create`方法。 比方說，如果您有 Web 應用程式名為**MyTwiML**部署的 tooan Azure 託管服務，而且 hello 頁面名稱的 hello PHP **mytwiml.php**，URL 可以太傳送的嗨**Services_Twilio]-> [帳戶]-> [呼叫]-> [建立**hello 下列範例所示：

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // hello phone message text.
    $message = "Hello world.";

    $client = new Services_Twilio($sid, $token, "2010-04-01");

    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

使用 Twilio 與 PHP 的 Azure 中的其他資訊，請參閱[如何在 Azure 上的 PHP 應用程式的電話使用 Twilio tooMake][howto_phonecall_php]。

## <a id="AdditionalServices"></a>如何：使用其他 Twilio 服務
此外 toohello 範例所示，Twilio 提供網頁型應用程式開發介面，您可以使用其他 Twilio 功能 tooleverage 從 Azure 應用程式。 完整的詳細資訊，請參閱 hello [Twilio API 文件][twilio_api_documentation]。

## <a id="NextSteps"></a>後續步驟
既然您已經學會 hello hello Twilio 服務基本概念，請依照下列多個這些連結 toolearn:

* [Twilio 安全性方針][twilio_security_guidelines]
* [Twilio 作法與範例程式碼][twilio_howtos]
* [Twilio 快速入門教學課程][twilio_quickstarts] 
* [GitHub 上的 Twilio][twilio_on_github]
* [Talk tooTwilio 支援][twilio_support]

[twilio_php]: https://github.com/twilio/twilio-php
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-php/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-php/blob/master/README.md
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_api_service]: https://api.twilio.com
[howto_phonecall_php]: partner-twilio-php-make-phone-call.md
[twilio_voice_request]: https://www.twilio.com/docs/api/twiml/twilio_request
[twilio_sms_request]: https://www.twilio.com/docs/api/twiml/sms/twilio_request
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/user/account
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/api
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
