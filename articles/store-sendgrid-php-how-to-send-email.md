---
title: "aaaHow toouse hello SendGrid 電子郵件服務 (PHP) |Microsoft 文件"
description: "深入了解如何在 Azure 上傳送電子郵件以 hello SendGrid 電子郵件服務。 程式碼範例以 PHP 撰寫。"
documentationcenter: php
services: 
manager: sendgrid
editor: mollybos
author: thinkingserious
ms.assetid: 51a9928a-4c9e-4b0a-aca8-9a408aeb6f47
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork; matt.bernier@sendgrid.com
ms.openlocfilehash: 0076e56dc185cb8f52e629395e7d2c143cb5cfa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-sendgrid-email-service-from-php"></a>如何 tooUse hello SendGrid 來自 PHP 的電子郵件服務
本指南示範如何 tooperform 常見的程式設計工作以 hello SendGrid 傳送電子郵件在 Azure 上的服務。 hello 範例是以 PHP 撰寫。
hello 涵蓋案例包括**建構電子郵件**，**傳送電子郵件**，和**加入附件**。 如需有關 SendGrid 和傳送電子郵件的詳細資訊，請參閱 hello[接下來的步驟](#next-steps)> 一節。

## <a name="what-is-hello-sendgrid-email-service"></a>什麼是 hello SendGrid 電子郵件服務？
SendGrid 是 [雲端架構電子郵件服務]，能提供可靠的 [交易式電子郵件傳遞]、擴充性和即時分析，以及有彈性的 API 來輕鬆進行自訂整合。 常見的 SendGrid 使用案例包括：

* 自動將資料傳送回條 toocustomers
* 管理通訊群組清單，以便將每月電子傳單和特別優惠傳送給客戶
* 收集封鎖的電子郵件、客戶的回應情形等項目的即時度量
* 產生 toohelp 識別趨勢的報表
* 轉寄客戶查詢
* 透過電子郵件從您的應用程式傳送通知

如需詳細資訊，請參閱 [https://sendgrid.com][https://sendgrid.com]。

## <a name="create-a-sendgrid-account"></a>建立 SendGrid 帳戶
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="using-sendgrid-from-your-php-application"></a>透過 PHP 應用程式使用 SendGrid
在 Azure PHP 應用程式中使用 SendGrid 並不需要特殊的組態或程式碼。 SendGrid 是一項服務，因為它可以存取完全 hello 中相同的方式，從雲端應用程式，因為它可以從內部部署應用程式。

## <a name="how-to-send-an-email"></a>如何：傳送電子郵件
您可以傳送電子郵件使用 SMTP 或 hello SendGrid 所提供的 Web API。

### <a name="smtp-api"></a>SMTP API
使用 SendGrid SMTP API，使用 hello toosend 電子郵件*Swift 寄件者*，從 PHP 應用程式傳送電子郵件的元件為基礎的程式庫。 您可以下載 hello *Swift 寄件者*從程式庫[http://swiftmailer.org/download] [ http://swiftmailer.org/download] v5.3.0 (使用[編輯器]tooinstallSwift 寄件者）。 傳送電子郵件與 hello 程式庫包含建立的執行個體<span class="auto-style2">Swift\_SmtpTransport</span>， <span class="auto-style2">Swift\_寄件者</span>，和<span class="auto-style2">Swift\_訊息</span>類別，設定適當的屬性，以及呼叫<span class="auto-style2">Swift\_Mailer::send</span>方法。

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create hello body of hello message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of hello email
      * If hello receiver is able tooview html emails then only hello html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
     $html = "<html>
           <head></head>
           <body>
               <p>Hi!<br>
                   How are you?<br>
               </p>
           </body>
           </html>";
     // This is your From email address
     $from = array('someone@example.com' => 'Name tooAppear');
     // Email recipients
     $too= array(
           'john@contoso.com'=>'Destination 1 Name',
           'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach hello body of hello email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
         // This will let us know how many users received this message
         echo 'Message sent out too'.$recipients.' users';
     }
     // something went wrong =(
     else
     {
         echo "Something went wrong - ";
         print_r($failures);
     }

### <a name="web-api"></a>Web API
使用 PHP 的[curl 函式][ curl function] toosend 電子郵件使用 hello SendGrid Web API。

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $params = array(
          'api_user' => $user,
          'api_key' => $pass,
          'to' => 'john@contoso.com',
          'subject' => 'testing from curl',
          'html' => 'testing body',
          'text' => 'testing body',
          'from' => 'anna@contoso.com',
       );

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl toouse HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is hello body of hello POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not tooreturn headers, but do return hello response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

SendGrid 的 Web API 是非常類似 tooa REST API，但它不是真正 rest 式 API，因為在大部分的呼叫中，同時取得的可以交換使用 POST 動詞命令。

## <a name="how-to-add-an-attachment"></a>如何：新增附件
### <a name="smtp-api"></a>SMTP API
傳送使用 hello SMTP API 的附加檔案包含一個額外的一行程式碼 toohello 範例指令碼來傳送含有 Swift 寄件者的電子郵件。

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create hello body of hello message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of hello email
      * If hello reciever is able tooview html emails then only hello html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
      $html = "<html>
          <head></head>
          <body>
             <p>Hi!<br>
                How are you?<br>
             </p>
          </body>
          </html>";

     // This is your From email address
     $from = array('someone@example.com' => 'Name tooAppear');

     // Email recipients
     $too= array(
          'john@contoso.com'=>'Destination 1 Name',
          'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach hello body of hello email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');
     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName("file_name"));

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
          // This will let us know how many users received this message
          echo 'Message sent out too'.$recipients.' users';
     }
     // something went wrong =(
     else
     {
          echo "Something went wrong - ";
          print_r($failures);
     }

hello 額外的一行程式碼如下所示：

     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName('file_name'));

這一行程式碼呼叫 hello 附加方法上<span class="auto-style2">Swift\_訊息</span>物件並使用靜態方法<span class="auto-style2">fromPath</span>上<span class="auto-style2">Swift\_附件</span>類別 tooget 和附加檔案 tooa 訊息。

### <a name="web-api"></a>Web API
傳送附件使用 hello Web API 的 toosending 的非常類似電子郵件使用 hello Web API。 不過，請注意，在 hello 接下來的範例，hello 參數陣列必須包含這個項目：

    'files['.$fileName.']' => '@'.$filePath.'/'.$fileName

範例：

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $fileName = 'myfile';
     $filePath = dirname(__FILE__);

     $params = array(
         'api_user' => $user,
         'api_key' => $pass,
         'to' =>'john@contoso.com',
         'subject' => 'test of file sends',
         'html' => '<p> hello HTML </p>',
         'text' => 'hello plain text',
         'from' => 'anna@contoso.com',
         'files['.$fileName.']' => '@'.$filePath.'/'.$fileName
     );

     print_r($params);

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl toouse HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is hello body of hello POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not tooreturn headers, but do return hello response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a>如何： 使用篩選器 tooEnable 頁尾、 追蹤和分析
SendGrid 提供透過 '篩選' hello 使用其他電子郵件功能。 這些是可以加入 tooan 電子郵件訊息，若要啟用特定的功能，例如啟用點選追蹤、 Google analytics、 追蹤、 訂用帳戶的設定，依此類推。

篩選可套用的 tooa 訊息使用 hello 篩選屬性。 每個篩選器都是由包含篩選器特定設定的雜湊來指定。 下列範例會啟用 hello 頁尾篩選器，並指定文字訊息，將會附加 toohello 底部 hello 電子郵件訊息。
在此範例中，我們將使用 [sendgrid-php 程式庫]。
使用[編輯器]tooinstall 程式庫：

    php composer.phar require sendgrid/sendgrid 2.1.1

範例：    

    <?php
     /*
      * This example is used for sendgrid-php V2.1.1 (https://github.com/sendgrid/sendgrid-php/tree/v2.1.1)
      */
     include "vendor/autoload.php";

     $email = new SendGrid\Email();
     // hello list of addresses this message will be sent to
     // [This list is used for sending multiple emails using just ONE request tooSendGrid]
     $toList = array('john@contoso.com', 'anna@contoso.com');

     // Specify hello names of hello recipients
     $nameList = array('Name 1', 'Name 2');

     // Used as an example of variable substitution
     $timeList = array('4 PM', '5 PM');

     // Set all of hello above variables
     $email->setTos($toList);
     $email->addSubstitution('-name-', $nameList);
     $email->addSubstitution('-time-', $timeList);

     // Specify that this is an initial contact message
     $email->addCategory("initial");

     // You can optionally setup individual filters here, in this example, we have
     // enabled hello footer filter
     $email->addFilter('footer', 'enable', 1);
     $email->addFilter('footer', "text/plain", "Thank you for your business");
     $email->addFilter('footer', "text/html", "Thank you for your business");

     // hello subject of your email
     $subject = 'Example SendGrid Email';

     // Where is this message coming from. For example, this message can be from
     // support@yourcompany.com, info@yourcompany.com
     $from = 'someone@example.com';

     // If you do not specify a sender list above, you can specifiy hello user here. If
     // a sender list IS specified above, this email address becomes irrelevant.
     $too= 'john@contoso.com';

     # Create hello body of hello message (a plain-text and an HTML version).
     # text is your plain-text email
     # html is your html version of hello email
     # if hello receiver is able tooview html emails then only hello html
     # email will be displayed

     /*
      * Note hello variable substitution here =)
      */
     $text = "
     Hello -name-,
     Thank you for your interest in our products. We have set up an appointment toocall you at -time- EST toodiscuss your needs in more detail.
     Regards,
     Fred";

     $html = "
     <html>
     <head></head>
     <body>
     <p>Hello -name-,<br>
     Thank you for your interest in our products. We have set up an appointment
     toocall you at -time- EST toodiscuss your needs in more detail.

     Regards,

     Fred<br>
     </p>
     </body>
     </html>";

     // set subject
     $email->setSubject($subject);

     // attach hello body of hello email
     $email->setFrom($from);
     $email->setHtml($html);
     $email->addTo($to);
     $email->setText($text);

     // Your SendGrid account credentials
     $username = 'sendgridusername@yourdomain.com';
     $password = 'example';

     // Create SendGrid object
     $sendgrid = new SendGrid($username, $password);

     // send message
     $response = $sendgrid->send($email);

     print_r($response);

## <a name="next-steps"></a>後續步驟
既然您已經學會 hello 的 hello SendGrid 電子郵件服務的基本概念，請遵循這些連結 toolearn 更多。

* SendGrid 文件︰<https://sendgrid.com/docs>
* SendGrid PHP 程式庫︰<https://github.com/sendgrid/sendgrid-php>
* Azure 客戶的 SendGrid 特別優惠：<https://sendgrid.com/windowsazure.html>

如需詳細資訊，請參閱 hello [PHP 開發人員中心](/develop/php/)。

[https://sendgrid.com]: https://sendgrid.com
[https://sendgrid.com/transactional-email/pricing]: https://sendgrid.com/transactional-email/pricing
[special offer]: https://www.sendgrid.com/windowsazure.html
[Packaging and Deploying PHP Applications for Azure]: http://msdn.microsoft.com/library/windowsazure/hh674499(v=VS.103).aspx
[http://swiftmailer.org/download]: http://swiftmailer.org/download
[curl function]: http://php.net/curl
[雲端架構電子郵件服務]: https://sendgrid.com/email-solutions
[交易式電子郵件傳遞]: https://sendgrid.com/transactional-email
[sendgrid-php 程式庫]: https://github.com/sendgrid/sendgrid-php/tree/v2.1.1
[編輯器]: https://getcomposer.org/download/
