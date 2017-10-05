---
title: "如何從 Twilio 撥打電話 (PHP) | Microsoft Docs"
description: "了解如何在 Azure 上使用 Twilio API 服務撥打電話及傳送簡訊。 範例適用於 PHP 應用程式。"
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
ms.openlocfilehash: f35450ace02727ddf392dbbe857b934a45ee022a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-make-a-phone-call-using-twilio-in-a-php-application-on-azure"></a><span data-ttu-id="b7d61-104">如何在 Azure 上的 PHP 應用程式中使用 Twilio 撥打電話</span><span class="sxs-lookup"><span data-stu-id="b7d61-104">How to Make a Phone Call Using Twilio in a PHP Application on Azure</span></span>
<span data-ttu-id="b7d61-105">下列範例將說明如何從 Azure 代管的 PHP 網頁上使用 Twilio 撥打電話。</span><span class="sxs-lookup"><span data-stu-id="b7d61-105">The following example shows you how you can use Twilio to make a call from a PHP web page hosted in Azure.</span></span> <span data-ttu-id="b7d61-106">產生的應用程式會提示使用者提供電話值，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="b7d61-106">The resulting application will prompt the user for phone call values, as shown in the following screen shot.</span></span>

![Azure Call Form Using Twilio and PHP][twilio_php]

<span data-ttu-id="b7d61-108">您必須執行下列動作才能使用本主題中的程式碼：</span><span class="sxs-lookup"><span data-stu-id="b7d61-108">You'll need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="b7d61-109">從您的 [Twilio 主控台][twilio_console]取得 Twilio 帳戶和驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="b7d61-109">Acquire a Twilio account and authentication token from your [Twilio Console][twilio_console].</span></span> <span data-ttu-id="b7d61-110">若要開始使用 Twilio，請在 [http://www.twilio.com/pricing][twilio_pricing] 上評估價格。</span><span class="sxs-lookup"><span data-stu-id="b7d61-110">To get started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="b7d61-111">您可以在 [https://www.twilio.com/try-twilio][try_twilio] 上註冊試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7d61-111">You can sign up for a trial account at [https://www.twilio.com/try-twilio][try_twilio].</span></span>
2. <span data-ttu-id="b7d61-112">取得 [適用於 PHP 的 Twilio 程式庫](https://github.com/twilio/twilio-php) ，或以 PEAR 封裝的形式進行安裝。</span><span class="sxs-lookup"><span data-stu-id="b7d61-112">Obtain the [Twilio library for PHP](https://github.com/twilio/twilio-php) or install it as a PEAR package.</span></span> <span data-ttu-id="b7d61-113">如需詳細資訊，請參閱 [讀我檔案](https://github.com/twilio/twilio-php/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="b7d61-113">For more information, see the [readme file](https://github.com/twilio/twilio-php/blob/master/README.md).</span></span>
3. <span data-ttu-id="b7d61-114">安裝 Azure SDK for PHP。</span><span class="sxs-lookup"><span data-stu-id="b7d61-114">Install the Azure SDK for PHP.</span></span> <span data-ttu-id="b7d61-115">如需 SDK 的概觀及其安裝指示，請參閱[設定 Azure SDK for PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span><span class="sxs-lookup"><span data-stu-id="b7d61-115">For an overview of the SDK and instructions on installing it, see [Set up the Azure SDK for PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="b7d61-116">建立用以撥打電話的 Web 表單</span><span class="sxs-lookup"><span data-stu-id="b7d61-116">Create a web form for making a call</span></span>
<span data-ttu-id="b7d61-117">下列 HTML 程式碼將說明如何建置網頁 (**callform.html**)，以擷取撥打電話所需的使用者資料：</span><span class="sxs-lookup"><span data-stu-id="b7d61-117">The following HTML code shows how to build a web page (**callform.html**) that retrieves user data for making a call:</span></span>

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
        <td><input name="callText" size="100" type="text" value="Hello. This is the call text. Good bye."></td>
      </tr>
      <tr>
        <td colspan="2"><input type="submit" value="Make this call"></td>
      </tr>
    </table>
  </form><br>
</body>
</html>
```

## <a name="create-the-code-to-make-the-call"></a><span data-ttu-id="b7d61-118">建立用以撥打電話的程式碼</span><span class="sxs-lookup"><span data-stu-id="b7d61-118">Create the code to make the call</span></span>
<span data-ttu-id="b7d61-119">下列程式碼將說明如何建置會在使用者提交 **callform.html** 所顯示的表單時受到呼叫的 **makecall.php**。</span><span class="sxs-lookup"><span data-stu-id="b7d61-119">The following code shows how to build **makecall.php**, which is called when the user submits the form displayed by **callform.html**.</span></span> <span data-ttu-id="b7d61-120">下方顯示的程式碼會建立通話訊息及產生通話。</span><span class="sxs-lookup"><span data-stu-id="b7d61-120">The code shown below creates the call message and generates the call.</span></span> <span data-ttu-id="b7d61-121">同時，請務必使用來自 [Twilio 主控台][twilio_console]的 Twilio 帳戶和驗證權杖，而不是下方程式碼中指派給 **$sid** 和 **$token** 的預留位置值。</span><span class="sxs-lookup"><span data-stu-id="b7d61-121">Also, be sure to use your Twilio account and authentication token from the [Twilio Console][twilio_console] instead of the placeholder values assigned to **$sid** and **$token** in the code below.</span></span>

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

<span data-ttu-id="b7d61-122">除了撥打電話以外，**makecall.php** 也會顯示某些通話中繼資料，如以下影像中所示。</span><span class="sxs-lookup"><span data-stu-id="b7d61-122">In addition to making the call, **makecall.php** displays some call metadata, as is shown in the image below.</span></span> <span data-ttu-id="b7d61-123">如需通話中繼資料的詳細資訊，請參閱 [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties]。</span><span class="sxs-lookup"><span data-stu-id="b7d61-123">For more information about call metadata, see [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span></span>

![Azure Call Response Using Twilio and PHP][twilio_php_response]

## <a name="run-the-application"></a><span data-ttu-id="b7d61-125">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="b7d61-125">Run the application</span></span>
<span data-ttu-id="b7d61-126">下一個步驟是將您的應用程式部署至 Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="b7d61-126">The next step is to deploy your application to Azure Websites.</span></span> <span data-ttu-id="b7d61-127">下列文章包含使用 Git、FTP 或 WebMatrix 來建立網站及部署程式碼的相關資訊 (並非每篇文章中的所有資訊都是相關的)：</span><span class="sxs-lookup"><span data-stu-id="b7d61-127">The following articles contain the information for creating a website and deploying your code with Git, FTP, or WebMatrix (though not all information in each article is relevant):</span></span>

* [<span data-ttu-id="b7d61-128">建立 PHP-MySQL Azure 網站並使用 Git 部署</span><span class="sxs-lookup"><span data-stu-id="b7d61-128">Create a PHP-MySQL Azure Web Site and deploy using Git</span></span>](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [<span data-ttu-id="b7d61-129">建立 PHP-MySQL Azure 網站並使用 FTP 部署</span><span class="sxs-lookup"><span data-stu-id="b7d61-129">Create a PHP-MySQL Azure Web Site and Deploy Using FTP</span></span>](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a><span data-ttu-id="b7d61-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b7d61-130">Next steps</span></span>
<span data-ttu-id="b7d61-131">此程式可說明在 Azure 上的 PHP 中使用 Twilio 的基本功能。</span><span class="sxs-lookup"><span data-stu-id="b7d61-131">This code was provided to show you basic functionality using Twilio in PHP on Azure.</span></span> <span data-ttu-id="b7d61-132">在部署至生產環境中的 Azure 之前，您可以新增更多錯誤處理或其他功能。</span><span class="sxs-lookup"><span data-stu-id="b7d61-132">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="b7d61-133">例如：</span><span class="sxs-lookup"><span data-stu-id="b7d61-133">For example:</span></span>

* <span data-ttu-id="b7d61-134">除了使用 Web 表單以外，您也可以使用 Azure 儲存體 Blob 或 SQL Database 來儲存電話號碼和通話文字。</span><span class="sxs-lookup"><span data-stu-id="b7d61-134">Instead of using a web form, you could use Azure storage blobs or SQL Database to store phone numbers and call text.</span></span> <span data-ttu-id="b7d61-135">如需在 PHP 中使用 Azure 儲存體 Blob 的相關資訊，請參閱[搭配使用 Azure 儲存體與 PHP 應用程式][howto_blob_storage_php]。</span><span class="sxs-lookup"><span data-stu-id="b7d61-135">For information about using Azure storage blobs in PHP, see [Using Azure Storage with PHP Applications][howto_blob_storage_php].</span></span> <span data-ttu-id="b7d61-136">如需在 PHP 中使用 SQL Database 的相關資訊，請參閱[搭配使用 SQL Database 與 PHP 應用程式][howto_sql_azure_php]。</span><span class="sxs-lookup"><span data-stu-id="b7d61-136">For information about using SQL Database in PHP, see [Using SQL Database with PHP Applications][howto_sql_azure_php].</span></span>
* <span data-ttu-id="b7d61-137">**makecall.php** 程式碼會使用 Twilio 提供的 URL ([http://twimlets.com/message][twimlet_message_url]) 來提供 Twilio 標記語言 (TwiML) 回應，以告知 Twilio 應如何執行通話。</span><span class="sxs-lookup"><span data-stu-id="b7d61-137">The **makecall.php** code uses Twilio-provided URL ([http://twimlets.com/message][twimlet_message_url]) to provide a Twilio Markup Language (TwiML) response that informs Twilio how to proceed with the call.</span></span> <span data-ttu-id="b7d61-138">例如，傳回的 TwiML 可能會包含 `<Say>` 動詞，而產生要傳達給受話方的文字。</span><span class="sxs-lookup"><span data-stu-id="b7d61-138">For example, the TwiML that is returned can contain a `<Say>` verb that results in text being spoken to the call recipient.</span></span> <span data-ttu-id="b7d61-139">除了使用 Twilio 提供的 URL 以外，您也可以建置自己的服務來回應 Twilio 的要求；如需詳細資訊，請參閱[如何在 PHP 中透過 Twilio 使用語音和簡訊功能][howto_twilio_voice_sms_php]。</span><span class="sxs-lookup"><span data-stu-id="b7d61-139">Instead of using the Twilio-provided URL, you could build your own service to respond to Twilio's request; for more information, see [How to Use Twilio for Voice and SMS Capabilities in PHP][howto_twilio_voice_sms_php].</span></span> <span data-ttu-id="b7d61-140">如需 TwiML 的詳細資訊，請參閱 [http://www.twilio.com/docs/api/twiml][twiml]；如需 `<Say>` 和其他 Twilio 動詞的詳細資訊，請參閱 [http://www.twilio.com/docs/api/twiml/say][twilio_say]。</span><span class="sxs-lookup"><span data-stu-id="b7d61-140">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about `<Say>` and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="b7d61-141">閱讀 [https://www.twilio.com/docs/security][twilio_docs_security] 上的 Twilio 安全性指引。</span><span class="sxs-lookup"><span data-stu-id="b7d61-141">Read the Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="b7d61-142">如需 Twilio 的其他資訊，請參閱 [https://www.twilio.com/docs][twilio_docs]。</span><span class="sxs-lookup"><span data-stu-id="b7d61-142">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="b7d61-143">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b7d61-143">See Also</span></span>
* [<span data-ttu-id="b7d61-144">如何在 PHP 中透過 Twilio 使用語音和簡訊功能</span><span class="sxs-lookup"><span data-stu-id="b7d61-144">How to Use Twilio for Voice and SMS Capabilities in PHP</span></span>](partner-twilio-php-how-to-use-voice-sms.md)

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
