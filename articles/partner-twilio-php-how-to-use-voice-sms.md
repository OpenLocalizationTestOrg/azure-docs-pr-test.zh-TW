---
title: "如何使用 Twilio for Voice and SMS (PHP) | Microsoft Docs"
description: "了解如何在 Azure 上使用 Twilio API 服務撥打電話及傳送簡訊。 程式碼範例以 PHP 撰寫。"
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
ms.openlocfilehash: bd50eac7390e8639f77894689388e6926cdb619c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-php"></a><span data-ttu-id="53495-104">如何在 PHP 中透過 Twilio 使用語音和簡訊功能</span><span class="sxs-lookup"><span data-stu-id="53495-104">How to Use Twilio for Voice and SMS Capabilities in PHP</span></span>
<span data-ttu-id="53495-105">本指南示範如何在 Azure 上透過 Twilio API 服務執行常見的程式設計工作。</span><span class="sxs-lookup"><span data-stu-id="53495-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="53495-106">涵蓋的案例包括打電話和傳送簡訊 (SMS)。</span><span class="sxs-lookup"><span data-stu-id="53495-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="53495-107">如需有關如何在應用程式中使用 Twilio 語音和 SMS 的詳細資訊，請參閱 [後續步驟](#NextSteps) 一節。</span><span class="sxs-lookup"><span data-stu-id="53495-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="53495-108"><a id="WhatIs"></a>什麼是 Twilio？</span><span class="sxs-lookup"><span data-stu-id="53495-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="53495-109">Twilio 正在形塑商業環境的未來，可讓開發人員將語音、VoIP 和訊息傳送內嵌到應用程式中。</span><span class="sxs-lookup"><span data-stu-id="53495-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="53495-110">它們將雲端、全球化環境中所需的整個基礎結構虛擬化，透過 Twilio 通訊 API 平台來揭露基礎結構。</span><span class="sxs-lookup"><span data-stu-id="53495-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span></span> <span data-ttu-id="53495-111">輕鬆就可建立和擴充應用程式。</span><span class="sxs-lookup"><span data-stu-id="53495-111">Applications are simple to build and scalable.</span></span> <span data-ttu-id="53495-112">享受隨收隨付定價的彈性和雲端可靠性的好處。</span><span class="sxs-lookup"><span data-stu-id="53495-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="53495-113">**Twilio 語音** 可讓應用程式撥打和接聽電話。</span><span class="sxs-lookup"><span data-stu-id="53495-113">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="53495-114">**Twilio 簡訊** 可讓應用程式收發簡訊。</span><span class="sxs-lookup"><span data-stu-id="53495-114">**Twilio SMS** enables your application to send and receive text messages.</span></span> <span data-ttu-id="53495-115">**Twilio 用戶端** 可讓您從任何電話、平板電腦或瀏覽器撥打 VoIP 電話，且支援 WebRTC。</span><span class="sxs-lookup"><span data-stu-id="53495-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="53495-116"><a id="Pricing"></a>Twilio 定價和特別優惠</span><span class="sxs-lookup"><span data-stu-id="53495-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="53495-117">升級 Twilio 帳戶的 Azure 客戶，可[特別獲贈](http://www.twilio.com/azure)價值 $10 的 Twilio 點數。</span><span class="sxs-lookup"><span data-stu-id="53495-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="53495-118">此 Twilio 點數可用來折抵任何 Twilio 使用量 ($10 點數相當於最多傳送 1,000 則簡訊，或最多接收 1000 分鐘的撥入語音，視電話號碼所在地點或通話目的地而定)。</span><span class="sxs-lookup"><span data-stu-id="53495-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span></span> <span data-ttu-id="53495-119">請至 [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure)兌換 Twilio 點數來開始使用。</span><span class="sxs-lookup"><span data-stu-id="53495-119">Redeem this Twilio credit and get started at: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="53495-120">Twilio 是隨收隨付的服務。</span><span class="sxs-lookup"><span data-stu-id="53495-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="53495-121">不需要設定費，隨時都可結清帳戶。</span><span class="sxs-lookup"><span data-stu-id="53495-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="53495-122">如需詳細資訊，請參閱 [Twilio 價格][twilio_pricing]。</span><span class="sxs-lookup"><span data-stu-id="53495-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="53495-123"><a id="Concepts"></a>概念</span><span class="sxs-lookup"><span data-stu-id="53495-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="53495-124">Twilio API 是一套為應用程式提供語音和簡訊功能的 RESTful API。</span><span class="sxs-lookup"><span data-stu-id="53495-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="53495-125">用戶端程式庫有多種語言版本，相關清單請參閱 [Twilio API 程式庫][twilio_libraries]。</span><span class="sxs-lookup"><span data-stu-id="53495-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="53495-126">Twilio API 的兩大重點是 Twilio 動詞和 Twilio 標記語言 (TwiML)。</span><span class="sxs-lookup"><span data-stu-id="53495-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="53495-127"><a id="Verbs"></a>Twilio 動詞</span><span class="sxs-lookup"><span data-stu-id="53495-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="53495-128">API 採用 Twilio 動詞。例如，**&lt;Say&gt;** 動詞指示 Twilio 在通話中用語音傳遞訊息。</span><span class="sxs-lookup"><span data-stu-id="53495-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="53495-129">以下是 Twilio 動詞清單。</span><span class="sxs-lookup"><span data-stu-id="53495-129">The following is a list of Twilio verbs.</span></span> <span data-ttu-id="53495-130">如需了解其他動詞和功能，請參閱 [Twilio 標記語言文件](http://www.twilio.com/docs/api/twiml)。</span><span class="sxs-lookup"><span data-stu-id="53495-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="53495-131">**&lt;撥號&gt;**：使撥號者接通另一支電話。</span><span class="sxs-lookup"><span data-stu-id="53495-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="53495-132">**&lt;收集&gt;**：收集電話按鍵上輸入的號碼。</span><span class="sxs-lookup"><span data-stu-id="53495-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="53495-133">**&lt;掛斷&gt;**：結束通話。</span><span class="sxs-lookup"><span data-stu-id="53495-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="53495-134">**&lt;播放&gt;**：播放音訊檔案。</span><span class="sxs-lookup"><span data-stu-id="53495-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="53495-135">**&lt;暫停&gt;**：靜候一段指定的秒數。</span><span class="sxs-lookup"><span data-stu-id="53495-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="53495-136">**&lt;記錄&gt;**：錄製來電者的語音並傳回含有錄音的檔案 URL。</span><span class="sxs-lookup"><span data-stu-id="53495-136">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="53495-137">**&lt;重新導向&gt;**：將通話或簡訊的控制權移轉至不同 URL 的 TwiML。</span><span class="sxs-lookup"><span data-stu-id="53495-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="53495-138">**&lt;拒絕&gt;**：拒絕 Twilio 號碼的來電而不計費</span><span class="sxs-lookup"><span data-stu-id="53495-138">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="53495-139">**&lt;說出&gt;**：將來電的文字轉換成語音。</span><span class="sxs-lookup"><span data-stu-id="53495-139">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="53495-140">**&lt;Sms&gt;**：傳送簡訊。</span><span class="sxs-lookup"><span data-stu-id="53495-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="53495-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="53495-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="53495-142">TwiML 是以 Twilio 動詞為基礎的一組 XML 指令，可指示 Twilio 如何處理來電或簡訊。</span><span class="sxs-lookup"><span data-stu-id="53495-142">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="53495-143">例如，下列 TwiML 會將 **Hello World** 文字轉換成語音。</span><span class="sxs-lookup"><span data-stu-id="53495-143">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="53495-144">當應用程式呼叫 Twilio API 時，其中一個 API 參數是傳回 TwiML 回應的 URL。</span><span class="sxs-lookup"><span data-stu-id="53495-144">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="53495-145">在開發用途上，您可以使用 Twilio 提供的 URL 來提供應用程式所使用的 TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="53495-145">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="53495-146">您也可以裝載您自己的 URL 來產生 TwiML 回應，另一種選擇是使用 **TwiMLResponse** 物件。</span><span class="sxs-lookup"><span data-stu-id="53495-146">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="53495-147">如需 Twilio 動詞、屬性和 TwiML 的詳細資訊，請參閱 [TwiML][twiml]。</span><span class="sxs-lookup"><span data-stu-id="53495-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="53495-148">如需 Twilio API 的詳細資訊，請參閱 [Twilio API][twilio_api]。</span><span class="sxs-lookup"><span data-stu-id="53495-148">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="53495-149"><a id="CreateAccount"></a>建立 Twilio 帳戶</span><span class="sxs-lookup"><span data-stu-id="53495-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="53495-150">準備取得 Twilio 帳戶時，請至[試用 Twilio][try_twilio] 註冊。</span><span class="sxs-lookup"><span data-stu-id="53495-150">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="53495-151">您可以先使用免費帳戶，稍後再升級帳戶。</span><span class="sxs-lookup"><span data-stu-id="53495-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="53495-152">註冊 Twilio 帳戶時，您會收到帳戶識別碼和驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="53495-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="53495-153">兩者皆為呼叫 Twilio API 所需。</span><span class="sxs-lookup"><span data-stu-id="53495-153">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="53495-154">為了防止未經授權存取您的帳戶，您妥善保管驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="53495-154">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="53495-155">在 [Twilio 帳戶頁面][twilio_account] 的 **ACCOUNT SID** 和 **AUTH TOKEN** 欄位中，分別可檢視您的帳戶識別碼和驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="53495-155">Your account ID and authentication token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="53495-156"><a id="create_app"></a>建立 PHP 應用程式</span><span class="sxs-lookup"><span data-stu-id="53495-156"><a id="create_app"></a>Create a PHP Application</span></span>
<span data-ttu-id="53495-157">使用 Twilio 服務且執行於 Azure 的 PHP 應用程式，與其他使用 Twilio 服務的 PHP 應用程式並無不同。</span><span class="sxs-lookup"><span data-stu-id="53495-157">A PHP application that uses the Twilio service and is running in Azure is no different than any other PHP application that uses the Twilio service.</span></span> <span data-ttu-id="53495-158">雖然 Twilio 服務是以 REST 為基礎，並可從 PHP 呼叫數種方式，本文將著重在如何搭配使用 Twilio 服務與[Twilio 程式庫從 GitHub PHP][twilio_php]。</span><span class="sxs-lookup"><span data-stu-id="53495-158">While Twilio services are REST-based and can be called from PHP in several ways, this article will focus on how to use Twilio services with [Twilio library for PHP from GitHub][twilio_php].</span></span> <span data-ttu-id="53495-159">如需使用 PHP Twilio 程式庫的詳細資訊，請參閱[http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs]。</span><span class="sxs-lookup"><span data-stu-id="53495-159">For more information about using the Twilio library for PHP, see [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="53495-160">在可用來建置並部署至 Azure 的 Twilio/PHP 應用程式的詳細的指示[如何在 Azure 上的 PHP 應用程式中進行通話使用 Twilio][howto_phonecall_php]。</span><span class="sxs-lookup"><span data-stu-id="53495-160">Detailed instructions for building and deploying a Twilio/PHP application to Azure are available at [How to Make a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="53495-161"><a id="configure_app"></a>設定應用程式以使用 Twilio 程式庫</span><span class="sxs-lookup"><span data-stu-id="53495-161"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="53495-162">您可以透過兩種方式設定應用程式，以使用適用於 PHP 的 Twilio 程式庫：</span><span class="sxs-lookup"><span data-stu-id="53495-162">You can configure your application to use the Twilio library for PHP in two ways:</span></span>

1. <span data-ttu-id="53495-163">適用於 PHP 從 GitHub 下載 Twilio 程式庫 ([https://github.com/twilio/twilio-php][twilio_php]) 並加入**服務**您的應用程式目錄。</span><span class="sxs-lookup"><span data-stu-id="53495-163">Download the Twilio library for PHP from GitHub ([https://github.com/twilio/twilio-php][twilio_php]) and add the **Services** directory to your application.</span></span>
   
    <span data-ttu-id="53495-164">-或-</span><span class="sxs-lookup"><span data-stu-id="53495-164">-OR-</span></span>
2. <span data-ttu-id="53495-165">以 PEAR 封裝的形式，安裝適用於 PHP 的 Twilio 程式庫。</span><span class="sxs-lookup"><span data-stu-id="53495-165">Install the Twilio library for PHP as a PEAR package.</span></span> <span data-ttu-id="53495-166">您可以使用下列命令進行此安裝：</span><span class="sxs-lookup"><span data-stu-id="53495-166">It can be installed with the following commands:</span></span>
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

<span data-ttu-id="53495-167">在適用於 PHP 的 Twilio 程式庫安裝完成後，您可以在 PHP 檔案頂端新增 **require_once** 陳述式，以參考該程式庫：</span><span class="sxs-lookup"><span data-stu-id="53495-167">Once you have installed the Twilio library for PHP, you can then add a **require_once** statement at the top of your PHP files to reference the library:</span></span>

        require_once 'Services/Twilio.php';

<span data-ttu-id="53495-168">如需詳細資訊，請參閱[https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme]。</span><span class="sxs-lookup"><span data-stu-id="53495-168">For more information, see [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="53495-169"><a id="howto_make_call"></a>作法：撥出電話</span><span class="sxs-lookup"><span data-stu-id="53495-169"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="53495-170">以下說明如何使用 **Services_Twilio** 類別來撥出電話。</span><span class="sxs-lookup"><span data-stu-id="53495-170">The following shows how to make an outgoing call using the **Services_Twilio** class.</span></span> <span data-ttu-id="53495-171">此程式碼也使用 Twilio 提供的網站來傳回 Twilio 標記語言 (TwiML) 回應。</span><span class="sxs-lookup"><span data-stu-id="53495-171">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="53495-172">請將 **From** 和 **To** 電話號碼換成您的值，在執行程式碼之前，請記得先驗證 Twilio 帳戶的 **From** 電話號碼。</span><span class="sxs-lookup"><span data-stu-id="53495-172">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span></span>

    // Include the Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // The number of the phone initiating the the call.
    $from_number = "NNNNNNNNNNN";

    // The number of the phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use the Twilio-provided site for the TwiML response.
    $url = "http://twimlets.com/message";

    // The phone message text.
    $message = "Hello world.";

    // Create the call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make the call.
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

<span data-ttu-id="53495-173">如前所述，此程式碼使用 Twilio 提供的網站來傳回 TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="53495-173">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="53495-174">您可以改用自己的網站來提供 TwiML 回應；如需詳細資訊，請參閱 [如何從您自己的網站提供 TwiML 回應](#howto_provide_twiml_responses)。</span><span class="sxs-lookup"><span data-stu-id="53495-174">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

* <span data-ttu-id="53495-175">**請注意**： 若要疑難排解 SSL 憑證驗證錯誤，請參閱[http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span><span class="sxs-lookup"><span data-stu-id="53495-175">**Note**: To troubleshoot SSL certificate validation errors, see [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span></span> 

## <span data-ttu-id="53495-176"><a id="howto_send_sms"></a>作法：傳送簡訊</span><span class="sxs-lookup"><span data-stu-id="53495-176"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="53495-177">以下說明如何使用 **Services_Twilio** 類別來傳送簡訊。</span><span class="sxs-lookup"><span data-stu-id="53495-177">The following shows how to send an SMS message using the **Services_Twilio** class.</span></span> <span data-ttu-id="53495-178">**From** 號碼由 Twilio 提供給試用帳戶來傳送簡訊。</span><span class="sxs-lookup"><span data-stu-id="53495-178">The **From** number is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="53495-179">執行程式碼之前，必須驗證您 Twilio 帳戶的 **To** 號碼。</span><span class="sxs-lookup"><span data-stu-id="53495-179">The **To** number must be verified for your Twilio account prior to running the code.</span></span>

    // Include the Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create the call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send the SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <span data-ttu-id="53495-180"><a id="howto_provide_twiml_responses"></a>作法：從您自己的網站提供 TwiML 回應</span><span class="sxs-lookup"><span data-stu-id="53495-180"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="53495-181">當您的應用程式開始呼叫 Twilio API 時，Twilio 會將要求傳送至 URL，然後應該會傳回 TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="53495-181">When your application initiates a call to the Twilio API, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="53495-182">前述範例使用 Twilio 提供的 URL [http://twimlets.com/message][twimlet_message_url]。</span><span class="sxs-lookup"><span data-stu-id="53495-182">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="53495-183">(雖然 TwiML 是設計給 Twilio 使用的，但您也可以在瀏覽器中檢視 TwiML。</span><span class="sxs-lookup"><span data-stu-id="53495-183">(While TwiML is designed for use by Twilio, you can view the it in your browser.</span></span> <span data-ttu-id="53495-184">例如，按一下 [http://twimlets.com/message][twimlet_message_url] 可查看空白的 `<Response>` 元素，又例如，按一下 [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] 可查看包含 `<Say>` 元素的 `<Response>` 元素。)</span><span class="sxs-lookup"><span data-stu-id="53495-184">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] to see a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="53495-185">除了使用 Twilio 提供的 URL 以外，您也可以建立自己的網站來傳回 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="53495-185">Instead of relying on the Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="53495-186">您可以使用任何語言建立會傳回 XML 回應的網站；本主題假設您將使用 PHP 建立 TwiML。</span><span class="sxs-lookup"><span data-stu-id="53495-186">You can create the site in any language that returns XML responses; this topic assumes you'll be using PHP to create the TwiML.</span></span>

<span data-ttu-id="53495-187">下列 PHP 頁面會產生一個在來電中顯示 **Hello World** 的 TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="53495-187">The following PHP page results in a TwiML response that says **Hello World** on the call.</span></span>

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

<span data-ttu-id="53495-188">從以上範例中可知，TwiML 回應只是一份 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="53495-188">As you can see from the example above, the TwiML response is simply an XML document.</span></span> <span data-ttu-id="53495-189">適用於 PHP 的 Twilio 程式庫包含可為您產生 TwiML 的類別。</span><span class="sxs-lookup"><span data-stu-id="53495-189">The Twilio library for PHP contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="53495-190">下列範例會產生同上的回應，但改用適用於 PHP 的 Twilio 程式庫中的 **Services\_Twilio\_Twiml** 類別：</span><span class="sxs-lookup"><span data-stu-id="53495-190">The example below produces the equivalent response as shown above, but uses the **Services\_Twilio\_Twiml** class in the Twilio library for PHP:</span></span>

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

<span data-ttu-id="53495-191">如需 TwiML 的詳細資訊，請參閱 [https://www.twilio.com/docs/api/twiml][twiml_reference]。</span><span class="sxs-lookup"><span data-stu-id="53495-191">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span> 

<span data-ttu-id="53495-192">設定 PHP 頁面來提供 TwiML 回應之後，請使用 PHP 頁面的 URL 作為傳遞到 `Services_Twilio->account->calls->create` 方法的 URL。</span><span class="sxs-lookup"><span data-stu-id="53495-192">Once you have your PHP page set up to provide TwiML responses, use the URL of the PHP page as the URL passed into the  `Services_Twilio->account->calls->create`  method.</span></span> <span data-ttu-id="53495-193">例如，如果您已將名為 **MyTwiML** 的 Web 應用程式部署至 Azure 託管服務，而 PHP 頁面的名稱為 **mytwiml.php**，則可將其 URL 傳至 **Services_Twilio->account->calls->create**，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="53495-193">For example, if you have a Web application named **MyTwiML** deployed to an Azure hosted service, and the name of the PHP page is **mytwiml.php**, the URL can be passed to  **Services_Twilio->account->calls->create**  as shown in the following example:</span></span>

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // The phone message text.
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

<span data-ttu-id="53495-194">如需有關使用 PHP 的 Azure 中使用 Twilio 的詳細資訊，請參閱[如何在 Azure 上的 PHP 應用程式中進行通話使用 Twilio][howto_phonecall_php]。</span><span class="sxs-lookup"><span data-stu-id="53495-194">For additional information about using Twilio in Azure with PHP, see [How to Make a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="53495-195"><a id="AdditionalServices"></a>如何：使用其他 Twilio 服務</span><span class="sxs-lookup"><span data-stu-id="53495-195"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="53495-196">除了此處所示的範例以外，Twilio 還提供網頁式 API，方便您從 Azure 應用程式中充份利用其他 Twilio 功能。</span><span class="sxs-lookup"><span data-stu-id="53495-196">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="53495-197">如需完整詳細資料，請參閱 [Twilio API 文件][twilio_api_documentation]。</span><span class="sxs-lookup"><span data-stu-id="53495-197">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="53495-198"><a id="NextSteps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="53495-198"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="53495-199">了解基本的 Twilio 服務之後，請參考下列連結以取得更多資訊：</span><span class="sxs-lookup"><span data-stu-id="53495-199">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="53495-200">[Twilio 安全性方針][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="53495-200">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="53495-201">[Twilio 作法與範例程式碼][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="53495-201">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="53495-202">[Twilio 快速入門教學課程][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="53495-202">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="53495-203">[GitHub 上的 Twilio][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="53495-203">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="53495-204">[洽詢 Twilio 支援][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="53495-204">[Talk to Twilio Support][twilio_support]</span></span>

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
