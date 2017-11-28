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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-php"></a><span data-ttu-id="678fc-104">如何 tooUse Twilio 語音和簡訊功能的 PHP</span><span class="sxs-lookup"><span data-stu-id="678fc-104">How tooUse Twilio for Voice and SMS Capabilities in PHP</span></span>
<span data-ttu-id="678fc-105">本指南示範如何 tooperform 常見的程式設計工作以 hello Twilio API 服務在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="678fc-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="678fc-106">涵蓋的 hello 案例包括撥電話及傳送短訊息服務 (SMS) 訊息。</span><span class="sxs-lookup"><span data-stu-id="678fc-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="678fc-107">如需有關 Twilio 和您的應用程式中使用語音和 SMS 的詳細資訊，請參閱 hello[接下來的步驟](#NextSteps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="678fc-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="678fc-108"><a id="WhatIs"></a>什麼是 Twilio？</span><span class="sxs-lookup"><span data-stu-id="678fc-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="678fc-109">Twilio 是及支援的業務通訊的 hello 未來、 啟用開發人員 tooembed 語音 VoIP 及訊息加入應用程式。</span><span class="sxs-lookup"><span data-stu-id="678fc-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="678fc-110">這些虛擬化在雲端為基礎、 全域環境中，公開透過 hello Twilio 通訊 API 平台所需的所有基礎結構。</span><span class="sxs-lookup"><span data-stu-id="678fc-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="678fc-111">應用程式是簡單 toobuild 及擴充。</span><span class="sxs-lookup"><span data-stu-id="678fc-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="678fc-112">享受隨收隨付定價的彈性和雲端可靠性的好處。</span><span class="sxs-lookup"><span data-stu-id="678fc-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="678fc-113">**Twilio 語音**可讓您的應用程式 toomake 撥打與接聽電話。</span><span class="sxs-lookup"><span data-stu-id="678fc-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="678fc-114">**Twilio SMS**可讓您的應用程式 toosend 及接收文字訊息。</span><span class="sxs-lookup"><span data-stu-id="678fc-114">**Twilio SMS** enables your application toosend and receive text messages.</span></span> <span data-ttu-id="678fc-115">**Twilio 用戶端**可讓您從任何電話、 平板電腦或瀏覽器 toomake VoIP 呼叫，並支援 WebRTC。</span><span class="sxs-lookup"><span data-stu-id="678fc-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="678fc-116"><a id="Pricing"></a>Twilio 定價和特別優惠</span><span class="sxs-lookup"><span data-stu-id="678fc-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="678fc-117">升級 Twilio 帳戶的 Azure 客戶，可[特別獲贈](http://www.twilio.com/azure)價值 $10 的 Twilio 點數。</span><span class="sxs-lookup"><span data-stu-id="678fc-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="678fc-118">此 Twilio 信用額度可以套用的 tooany Twilio 使用量 ($10 信用相等 toosending 多達 1000 SMS 訊息或接收向上 too1000 輸入語音分鐘，視您的電話號碼和訊息或呼叫目的地的 hello 位置而定)。</span><span class="sxs-lookup"><span data-stu-id="678fc-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="678fc-119">請至 [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure)兌換 Twilio 點數來開始使用。</span><span class="sxs-lookup"><span data-stu-id="678fc-119">Redeem this Twilio credit and get started at: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="678fc-120">Twilio 是隨收隨付的服務。</span><span class="sxs-lookup"><span data-stu-id="678fc-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="678fc-121">不需要設定費，隨時都可結清帳戶。</span><span class="sxs-lookup"><span data-stu-id="678fc-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="678fc-122">如需詳細資訊，請參閱 [Twilio 價格][twilio_pricing]。</span><span class="sxs-lookup"><span data-stu-id="678fc-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="678fc-123"><a id="Concepts"></a>概念</span><span class="sxs-lookup"><span data-stu-id="678fc-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="678fc-124">hello Twilio API 是 rest 式 API，應用程式提供語音和 SMS 功能。</span><span class="sxs-lookup"><span data-stu-id="678fc-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="678fc-125">用戶端程式庫有多種語言版本，相關清單請參閱 [Twilio API 程式庫][twilio_libraries]。</span><span class="sxs-lookup"><span data-stu-id="678fc-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="678fc-126">Hello Twilio API 的重要層面是 Twilio 動詞和 Twilio 標記語言 (TwiML)。</span><span class="sxs-lookup"><span data-stu-id="678fc-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="678fc-127"><a id="Verbs"></a>Twilio 動詞</span><span class="sxs-lookup"><span data-stu-id="678fc-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="678fc-128">hello API 會使用 Twilio 動詞命令。例如，hello **&lt;說&gt;**動詞命令會指示 Twilio tooaudibly 傳遞的訊息上呼叫。</span><span class="sxs-lookup"><span data-stu-id="678fc-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="678fc-129">hello 如下的 Twilio 指令動詞的清單。</span><span class="sxs-lookup"><span data-stu-id="678fc-129">hello following is a list of Twilio verbs.</span></span> <span data-ttu-id="678fc-130">深入了解 hello 其他動詞命令和功能，透過[Twilio 標記語言的文件](http://www.twilio.com/docs/api/twiml)。</span><span class="sxs-lookup"><span data-stu-id="678fc-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="678fc-131">**&lt;撥號&gt;**： 連接 hello 呼叫端 tooanother 電話。</span><span class="sxs-lookup"><span data-stu-id="678fc-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="678fc-132">**&lt;收集&gt;**： 會收集輸入 hello 電話字鍵台上的數字。</span><span class="sxs-lookup"><span data-stu-id="678fc-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="678fc-133">**&lt;掛斷&gt;**：結束通話。</span><span class="sxs-lookup"><span data-stu-id="678fc-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="678fc-134">**&lt;播放&gt;**：播放音訊檔案。</span><span class="sxs-lookup"><span data-stu-id="678fc-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="678fc-135">**&lt;暫停&gt;**：靜候一段指定的秒數。</span><span class="sxs-lookup"><span data-stu-id="678fc-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="678fc-136">**&lt;記錄&gt;**： 記錄 hello 呼叫者的語音，並傳回包含 hello 記錄檔的 URL。</span><span class="sxs-lookup"><span data-stu-id="678fc-136">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="678fc-137">**&lt;重新導向&gt;**： 控制權的通話或 SMS toohello TwiML 於不同的 URL。</span><span class="sxs-lookup"><span data-stu-id="678fc-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="678fc-138">**&lt;拒絕&gt;**： 拒絕傳入的呼叫未使用計費您 tooyour Twilio 數目</span><span class="sxs-lookup"><span data-stu-id="678fc-138">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="678fc-139">**&lt;說出&gt;**： 將文字 toospeech 所做的呼叫上。</span><span class="sxs-lookup"><span data-stu-id="678fc-139">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="678fc-140">**&lt;Sms&gt;**：傳送簡訊。</span><span class="sxs-lookup"><span data-stu-id="678fc-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="678fc-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="678fc-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="678fc-142">TwiML 是以 XML 為基礎的指示，就會通知方式的 Twilio hello Twilio 動詞命令為基礎的一組 tooprocess 通話或 SMS。</span><span class="sxs-lookup"><span data-stu-id="678fc-142">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="678fc-143">例如，下列 TwiML hello 將轉換的 hello 文字**Hello World** toospeech。</span><span class="sxs-lookup"><span data-stu-id="678fc-143">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="678fc-144">當您的應用程式呼叫 hello Twilio 應用程式開發介面時，其中 hello API 參數會是傳回 hello TwiML 回應 hello URL。</span><span class="sxs-lookup"><span data-stu-id="678fc-144">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="678fc-145">供開發應用程式，您可以使用您的應用程式所使用的 Twilio 提供 Url tooprovide hello TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="678fc-145">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="678fc-146">您也可以裝載自己 Url tooproduce hello TwiML 回應，和另一個選項是 toouse hello **TwiMLResponse**物件。</span><span class="sxs-lookup"><span data-stu-id="678fc-146">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="678fc-147">如需 Twilio 動詞、屬性和 TwiML 的詳細資訊，請參閱 [TwiML][twiml]。</span><span class="sxs-lookup"><span data-stu-id="678fc-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="678fc-148">如需 hello Twilio API 的詳細資訊，請參閱[Twilio API][twilio_api]。</span><span class="sxs-lookup"><span data-stu-id="678fc-148">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="678fc-149"><a id="CreateAccount"></a>建立 Twilio 帳戶</span><span class="sxs-lookup"><span data-stu-id="678fc-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="678fc-150">當你準備好 tooget Twilio 帳戶時，請在註冊[再試一次 Twilio][try_twilio]。</span><span class="sxs-lookup"><span data-stu-id="678fc-150">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="678fc-151">您可以先使用免費帳戶，稍後再升級帳戶。</span><span class="sxs-lookup"><span data-stu-id="678fc-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="678fc-152">註冊 Twilio 帳戶時，您會收到帳戶識別碼和驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="678fc-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="678fc-153">同時會為所需的 toomake Twilio API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="678fc-153">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="678fc-154">tooprevent 未經授權存取 tooyour 帳戶，讓驗證權杖的安全。</span><span class="sxs-lookup"><span data-stu-id="678fc-154">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="678fc-155">您的帳戶識別碼和驗證權杖皆可檢視在 hello [Twilio 帳戶 頁面上][twilio_account]，請在 hello 欄位標示為**帳戶 SID**和**驗證語彙基元**分別。</span><span class="sxs-lookup"><span data-stu-id="678fc-155">Your account ID and authentication token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="678fc-156"><a id="create_app"></a>建立 PHP 應用程式</span><span class="sxs-lookup"><span data-stu-id="678fc-156"><a id="create_app"></a>Create a PHP Application</span></span>
<span data-ttu-id="678fc-157">PHP 應用程式使用 hello Twilio 服務，且在 Azure 中執行並無不同 hello Twilio 服務會使用任何其他 PHP 應用程式。</span><span class="sxs-lookup"><span data-stu-id="678fc-157">A PHP application that uses hello Twilio service and is running in Azure is no different than any other PHP application that uses hello Twilio service.</span></span> <span data-ttu-id="678fc-158">雖然 Twilio 服務是以 REST 為基礎，並可從 PHP 呼叫數種方式，本文將著重在如何 toouse Twilio 服務使用[Twilio 程式庫從 GitHub PHP][twilio_php]。</span><span class="sxs-lookup"><span data-stu-id="678fc-158">While Twilio services are REST-based and can be called from PHP in several ways, this article will focus on how toouse Twilio services with [Twilio library for PHP from GitHub][twilio_php].</span></span> <span data-ttu-id="678fc-159">如需使用 PHP hello Twilio 程式庫的詳細資訊，請參閱[http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs]。</span><span class="sxs-lookup"><span data-stu-id="678fc-159">For more information about using hello Twilio library for PHP, see [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="678fc-160">詳細的指示，用於建置及部署 Twilio/PHP 應用程式 tooAzure 位於[如何在 Azure 上的 PHP 應用程式的電話使用 Twilio tooMake][howto_phonecall_php]。</span><span class="sxs-lookup"><span data-stu-id="678fc-160">Detailed instructions for building and deploying a Twilio/PHP application tooAzure are available at [How tooMake a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="678fc-161"><a id="configure_app"></a>設定您的應用程式 tooUse Twilio 文件庫</span><span class="sxs-lookup"><span data-stu-id="678fc-161"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="678fc-162">您可以設定 PHP 應用程式 toouse hello Twilio 庫有兩種：</span><span class="sxs-lookup"><span data-stu-id="678fc-162">You can configure your application toouse hello Twilio library for PHP in two ways:</span></span>

1. <span data-ttu-id="678fc-163">適用於 PHP 從 GitHub 下載 hello Twilio 程式庫 ([https://github.com/twilio/twilio-php][twilio_php]) 和新增 hello**服務**directory tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="678fc-163">Download hello Twilio library for PHP from GitHub ([https://github.com/twilio/twilio-php][twilio_php]) and add hello **Services** directory tooyour application.</span></span>
   
    <span data-ttu-id="678fc-164">-或-</span><span class="sxs-lookup"><span data-stu-id="678fc-164">-OR-</span></span>
2. <span data-ttu-id="678fc-165">安裝 PHP 的西洋梨套件 hello Twilio 程式庫。</span><span class="sxs-lookup"><span data-stu-id="678fc-165">Install hello Twilio library for PHP as a PEAR package.</span></span> <span data-ttu-id="678fc-166">它可以安裝以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="678fc-166">It can be installed with hello following commands:</span></span>
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

<span data-ttu-id="678fc-167">一旦您的 PHP 安裝 hello Twilio 程式庫，然後您可以加入**require_once**陳述式，在您的 PHP hello 頂端檔案 tooreference hello 程式庫：</span><span class="sxs-lookup"><span data-stu-id="678fc-167">Once you have installed hello Twilio library for PHP, you can then add a **require_once** statement at hello top of your PHP files tooreference hello library:</span></span>

        require_once 'Services/Twilio.php';

<span data-ttu-id="678fc-168">如需詳細資訊，請參閱[https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme]。</span><span class="sxs-lookup"><span data-stu-id="678fc-168">For more information, see [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="678fc-169"><a id="howto_make_call"></a>作法：撥出電話</span><span class="sxs-lookup"><span data-stu-id="678fc-169"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="678fc-170">hello 下列範例示範如何 toomake 傳出呼叫使用 hello **Services_Twilio**類別。</span><span class="sxs-lookup"><span data-stu-id="678fc-170">hello following shows how toomake an outgoing call using hello **Services_Twilio** class.</span></span> <span data-ttu-id="678fc-171">此程式碼也會使用 Twilio 提供站台 tooreturn hello Twilio 標記語言 (TwiML) 回應。</span><span class="sxs-lookup"><span data-stu-id="678fc-171">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="678fc-172">替換為您的值為 hello**從**和**至**電話號碼，並確保您確認 hello**從**電話號碼您 Twilio 帳戶先前 toorunning hello 撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="678fc-172">Substitute your values for hello **From** and **To** phone numbers, and ensure that you verify hello **From** phone number for your Twilio account prior toorunning hello code.</span></span>

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

<span data-ttu-id="678fc-173">如前所述，此程式碼會使用 Twilio 提供站台 tooreturn hello TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="678fc-173">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="678fc-174">您可以改為使用您自己的站台 tooprovide hello TwiML 回應。如需詳細資訊，請參閱[如何 tooProvide TwiML 回應從您自己網站](#howto_provide_twiml_responses)。</span><span class="sxs-lookup"><span data-stu-id="678fc-174">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

* <span data-ttu-id="678fc-175">**請注意**: tootroubleshoot SSL 憑證驗證錯誤，請參閱[http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span><span class="sxs-lookup"><span data-stu-id="678fc-175">**Note**: tootroubleshoot SSL certificate validation errors, see [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span></span> 

## <span data-ttu-id="678fc-176"><a id="howto_send_sms"></a>作法：傳送簡訊</span><span class="sxs-lookup"><span data-stu-id="678fc-176"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="678fc-177">hello 下列範例示範如何 toosend SMS 訊息使用 hello **Services_Twilio**類別。</span><span class="sxs-lookup"><span data-stu-id="678fc-177">hello following shows how toosend an SMS message using hello **Services_Twilio** class.</span></span> <span data-ttu-id="678fc-178">hello**從**數目由 Twilio 為試用版帳戶 toosend SMS 訊息。</span><span class="sxs-lookup"><span data-stu-id="678fc-178">hello **From** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="678fc-179">hello**至**數目必須驗證您 Twilio 帳戶先前 toorunning hello 撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="678fc-179">hello **To** number must be verified for your Twilio account prior toorunning hello code.</span></span>

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

## <span data-ttu-id="678fc-180"><a id="howto_provide_twiml_responses"></a>作法：從您自己的網站提供 TwiML 回應</span><span class="sxs-lookup"><span data-stu-id="678fc-180"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="678fc-181">當您的應用程式啟動呼叫 toohello Twilio 應用程式開發介面時，會傳送 Twilio，是您要求 tooa URL 必須是 tooreturn TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="678fc-181">When your application initiates a call toohello Twilio API, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="678fc-182">上述的 hello 範例會使用 hello Twilio 提供 URL [http://twimlets.com/message][twimlet_message_url]。</span><span class="sxs-lookup"><span data-stu-id="678fc-182">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="678fc-183">(雖然 TwiML 的 Twilio 設計使用，您可以檢視 hello 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="678fc-183">(While TwiML is designed for use by Twilio, you can view hello it in your browser.</span></span> <span data-ttu-id="678fc-184">例如，按一下[http://twimlets.com/message] [ twimlet_message_url] toosee 空`<Response>`項目，另一個範例中，按一下 [ [http://twimlets.com/message?訊息 %5B0 %5 D = Hello %20world] [ twimlet_message_url_hello_world] toosee`<Response>`包含項目`<Say>`項目。)</span><span class="sxs-lookup"><span data-stu-id="678fc-184">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] toosee a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="678fc-185">而不是依賴 hello Twilio 提供 URL，您可以建立您自己會傳回 HTTP 回應的網站。</span><span class="sxs-lookup"><span data-stu-id="678fc-185">Instead of relying on hello Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="678fc-186">您可以建立 hello 網站中的任何語言，傳回 XML 回應。本主題假設您將會使用 PHP toocreate hello TwiML。</span><span class="sxs-lookup"><span data-stu-id="678fc-186">You can create hello site in any language that returns XML responses; this topic assumes you'll be using PHP toocreate hello TwiML.</span></span>

<span data-ttu-id="678fc-187">hello 遵循 PHP 頁面結果以指出 TwiML 回應**Hello World** hello 呼叫。</span><span class="sxs-lookup"><span data-stu-id="678fc-187">hello following PHP page results in a TwiML response that says **Hello World** on hello call.</span></span>

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

<span data-ttu-id="678fc-188">您可以看到從 hello 上述範例中，hello TwiML 回應是只是 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="678fc-188">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="678fc-189">適用於 PHP 的 hello Twilio 程式庫包含類別，會為您產生 TwiML。</span><span class="sxs-lookup"><span data-stu-id="678fc-189">hello Twilio library for PHP contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="678fc-190">hello 下面範例會產生 hello 相等回應，如上所示，但使用 hello**服務\_Twilio\_Twiml** hello PHP 的 Twilio 文件庫中的類別：</span><span class="sxs-lookup"><span data-stu-id="678fc-190">hello example below produces hello equivalent response as shown above, but uses hello **Services\_Twilio\_Twiml** class in hello Twilio library for PHP:</span></span>

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

<span data-ttu-id="678fc-191">如需 TwiML 的詳細資訊，請參閱 [https://www.twilio.com/docs/api/twiml][twiml_reference]。</span><span class="sxs-lookup"><span data-stu-id="678fc-191">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span> 

<span data-ttu-id="678fc-192">一旦您的 PHP 頁面設定 tooprovide TwiML 回應，做為 hello hello PHP 網頁 URL hello URL 傳入 hello`Services_Twilio->account->calls->create`方法。</span><span class="sxs-lookup"><span data-stu-id="678fc-192">Once you have your PHP page set up tooprovide TwiML responses, use hello URL of hello PHP page as hello URL passed into hello  `Services_Twilio->account->calls->create`  method.</span></span> <span data-ttu-id="678fc-193">比方說，如果您有 Web 應用程式名為**MyTwiML**部署的 tooan Azure 託管服務，而且 hello 頁面名稱的 hello PHP **mytwiml.php**，URL 可以太傳送的嗨**Services_Twilio]-> [帳戶]-> [呼叫]-> [建立**hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="678fc-193">For example, if you have a Web application named **MyTwiML** deployed tooan Azure hosted service, and hello name of hello PHP page is **mytwiml.php**, hello URL can be passed too **Services_Twilio->account->calls->create**  as shown in hello following example:</span></span>

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

<span data-ttu-id="678fc-194">使用 Twilio 與 PHP 的 Azure 中的其他資訊，請參閱[如何在 Azure 上的 PHP 應用程式的電話使用 Twilio tooMake][howto_phonecall_php]。</span><span class="sxs-lookup"><span data-stu-id="678fc-194">For additional information about using Twilio in Azure with PHP, see [How tooMake a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="678fc-195"><a id="AdditionalServices"></a>如何：使用其他 Twilio 服務</span><span class="sxs-lookup"><span data-stu-id="678fc-195"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="678fc-196">此外 toohello 範例所示，Twilio 提供網頁型應用程式開發介面，您可以使用其他 Twilio 功能 tooleverage 從 Azure 應用程式。</span><span class="sxs-lookup"><span data-stu-id="678fc-196">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="678fc-197">完整的詳細資訊，請參閱 hello [Twilio API 文件][twilio_api_documentation]。</span><span class="sxs-lookup"><span data-stu-id="678fc-197">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="678fc-198"><a id="NextSteps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="678fc-198"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="678fc-199">既然您已經學會 hello hello Twilio 服務基本概念，請依照下列多個這些連結 toolearn:</span><span class="sxs-lookup"><span data-stu-id="678fc-199">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="678fc-200">[Twilio 安全性方針][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="678fc-200">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="678fc-201">[Twilio 作法與範例程式碼][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="678fc-201">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="678fc-202">[Twilio 快速入門教學課程][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="678fc-202">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="678fc-203">[GitHub 上的 Twilio][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="678fc-203">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="678fc-204">[Talk tooTwilio 支援][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="678fc-204">[Talk tooTwilio Support][twilio_support]</span></span>

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
