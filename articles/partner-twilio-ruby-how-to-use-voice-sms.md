---
title: "aaaHow tooUse Twilio 語音和 SMS (Ruby) |Microsoft 文件"
description: "了解如何 toomake 電話及傳送 SMS 訊息 hello Twilio API 服務在 Azure 上。 程式碼範例以 Ruby 撰寫。"
services: 
documentationcenter: ruby
author: devinrader
manager: twilio
editor: 
ms.assetid: 60e512f6-fa47-47c0-aedc-f19bb72a1158
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 11/25/2014
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: aca5ccb4663ff03c9c1f39c848469415f06dfb45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-ruby"></a><span data-ttu-id="f1a48-104">如何為語音和簡訊功能中 Ruby Twilio tooUse</span><span class="sxs-lookup"><span data-stu-id="f1a48-104">How tooUse Twilio for Voice and SMS Capabilities in Ruby</span></span>
<span data-ttu-id="f1a48-105">本指南示範如何 tooperform 常見的程式設計工作以 hello Twilio API 服務在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="f1a48-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="f1a48-106">涵蓋的 hello 案例包括撥電話及傳送短訊息服務 (SMS) 訊息。</span><span class="sxs-lookup"><span data-stu-id="f1a48-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="f1a48-107">如需有關 Twilio 和您的應用程式中使用語音和 SMS 的詳細資訊，請參閱 hello[接下來的步驟](#NextSteps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="f1a48-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="f1a48-108"><a id="WhatIs"></a>什麼是 Twilio？</span><span class="sxs-lookup"><span data-stu-id="f1a48-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="f1a48-109">Twilio 是電話語音 web 服務 API，可讓您使用現有的 web 語言和技術 toobuild 語音和 SMS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1a48-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills toobuild voice and SMS applications.</span></span> <span data-ttu-id="f1a48-110">Twilio 算是協力廠商服務 (並非 Azure 功能，也並非 Microsoft 產品)。</span><span class="sxs-lookup"><span data-stu-id="f1a48-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="f1a48-111">**Twilio 語音**可讓您的應用程式 toomake 撥打與接聽電話。</span><span class="sxs-lookup"><span data-stu-id="f1a48-111">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="f1a48-112">**Twilio SMS**可讓您的應用程式 toomake 和接收 SMS 訊息。</span><span class="sxs-lookup"><span data-stu-id="f1a48-112">**Twilio SMS** allows your applications toomake and receive SMS messages.</span></span> <span data-ttu-id="f1a48-113">**Twilio 用戶端**tooenable 語音通訊使用現有的網際網路連線，包括行動裝置的連線，可讓您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1a48-113">**Twilio Client** allows your applications tooenable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="f1a48-114"><a id="Pricing"></a>Twilio 定價和特別優惠</span><span class="sxs-lookup"><span data-stu-id="f1a48-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="f1a48-115">[Twilio 定價][twilio_pricing] (英文) 提供 Twilio 的定價資訊。</span><span class="sxs-lookup"><span data-stu-id="f1a48-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="f1a48-116">Azure 客戶可獲得[特殊優惠][special_offer]：免費 1000 則文字簡訊或接聽 1000 分鐘電話。</span><span class="sxs-lookup"><span data-stu-id="f1a48-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="f1a48-117">註冊這 toosign 提供或取得詳細資訊，請瀏覽[http://ahoy.twilio.com/azure][special_offer]。</span><span class="sxs-lookup"><span data-stu-id="f1a48-117">toosign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>  

## <span data-ttu-id="f1a48-118"><a id="Concepts"></a>概念</span><span class="sxs-lookup"><span data-stu-id="f1a48-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="f1a48-119">hello Twilio API 是 rest 式 API，應用程式提供語音和 SMS 功能。</span><span class="sxs-lookup"><span data-stu-id="f1a48-119">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="f1a48-120">用戶端程式庫有多種語言版本，相關清單請參閱 [Twilio API 程式庫][twilio_libraries]。</span><span class="sxs-lookup"><span data-stu-id="f1a48-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

### <span data-ttu-id="f1a48-121"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="f1a48-121"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="f1a48-122">TwiML 是一組以 XML 為基礎的指示，就會通知方式的 Twilio tooprocess 通話或 SMS。</span><span class="sxs-lookup"><span data-stu-id="f1a48-122">TwiML is a set of XML-based instructions that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="f1a48-123">例如，下列 TwiML hello 將轉換的 hello 文字**Hello World** toospeech。</span><span class="sxs-lookup"><span data-stu-id="f1a48-123">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="f1a48-124">所有 TwiML 文件皆會以 `<Response>` 作為其根元素。</span><span class="sxs-lookup"><span data-stu-id="f1a48-124">All TwiML documents have `<Response>` as their root element.</span></span> <span data-ttu-id="f1a48-125">從該處，您可以使用 Twilio 動詞 toodefine hello 應用程式的行為。</span><span class="sxs-lookup"><span data-stu-id="f1a48-125">From there, you use Twilio Verbs toodefine hello behavior of your application.</span></span>

### <span data-ttu-id="f1a48-126"><a id="Verbs"></a>TwiML 動詞</span><span class="sxs-lookup"><span data-stu-id="f1a48-126"><a id="Verbs"></a>TwiML Verbs</span></span>
<span data-ttu-id="f1a48-127">Twilio 動詞命令是向 Twilio 說明過的 XML 標記**不要**。</span><span class="sxs-lookup"><span data-stu-id="f1a48-127">Twilio Verbs are XML tags that tell Twilio what too**do**.</span></span> <span data-ttu-id="f1a48-128">例如，hello **&lt;說&gt;**動詞命令會指示 Twilio tooaudibly 傳遞的訊息上呼叫。</span><span class="sxs-lookup"><span data-stu-id="f1a48-128">For example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span> 

<span data-ttu-id="f1a48-129">hello 如下的 Twilio 指令動詞的清單。</span><span class="sxs-lookup"><span data-stu-id="f1a48-129">hello following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="f1a48-130">**&lt;撥號&gt;**： 連接 hello 呼叫端 tooanother 電話。</span><span class="sxs-lookup"><span data-stu-id="f1a48-130">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="f1a48-131">**&lt;收集&gt;**： 會收集輸入 hello 電話字鍵台上的數字。</span><span class="sxs-lookup"><span data-stu-id="f1a48-131">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="f1a48-132">**&lt;掛斷&gt;**：結束通話。</span><span class="sxs-lookup"><span data-stu-id="f1a48-132">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="f1a48-133">**&lt;播放&gt;**：播放音訊檔案。</span><span class="sxs-lookup"><span data-stu-id="f1a48-133">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="f1a48-134">**&lt;暫停&gt;**：靜候一段指定的秒數。</span><span class="sxs-lookup"><span data-stu-id="f1a48-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="f1a48-135">**&lt;記錄&gt;**： 記錄 hello 呼叫者的語音，並傳回包含 hello 記錄檔的 URL。</span><span class="sxs-lookup"><span data-stu-id="f1a48-135">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="f1a48-136">**&lt;重新導向&gt;**： 控制權的通話或 SMS toohello TwiML 於不同的 URL。</span><span class="sxs-lookup"><span data-stu-id="f1a48-136">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="f1a48-137">**&lt;拒絕&gt;**： 拒絕傳入的呼叫未使用計費您 tooyour Twilio 數目</span><span class="sxs-lookup"><span data-stu-id="f1a48-137">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="f1a48-138">**&lt;說出&gt;**： 將文字 toospeech 所做的呼叫上。</span><span class="sxs-lookup"><span data-stu-id="f1a48-138">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="f1a48-139">**&lt;Sms&gt;**：傳送簡訊。</span><span class="sxs-lookup"><span data-stu-id="f1a48-139">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

<span data-ttu-id="f1a48-140">如需 Twilio 動詞、屬性和 TwiML 的詳細資訊，請參閱 [TwiML][twiml]。</span><span class="sxs-lookup"><span data-stu-id="f1a48-140">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="f1a48-141">如需 hello Twilio API 的詳細資訊，請參閱[Twilio API][twilio_api]。</span><span class="sxs-lookup"><span data-stu-id="f1a48-141">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="f1a48-142"><a id="CreateAccount"></a>建立 Twilio 帳戶</span><span class="sxs-lookup"><span data-stu-id="f1a48-142"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="f1a48-143">當你準備好 tooget Twilio 帳戶時，請在註冊[再試一次 Twilio][try_twilio]。</span><span class="sxs-lookup"><span data-stu-id="f1a48-143">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="f1a48-144">您可以先使用免費帳戶，稍後再升級帳戶。</span><span class="sxs-lookup"><span data-stu-id="f1a48-144">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="f1a48-145">註冊 Twilio 帳戶時，您會獲得可供應用程式使用的免費電話號碼。</span><span class="sxs-lookup"><span data-stu-id="f1a48-145">When you sign up for a Twilio account, you'll get a free phone number for your application.</span></span> <span data-ttu-id="f1a48-146">您也會獲得帳戶 SID 和驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="f1a48-146">You'll also receive an account SID and an auth token.</span></span> <span data-ttu-id="f1a48-147">同時會為所需的 toomake Twilio API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="f1a48-147">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="f1a48-148">tooprevent 未經授權存取 tooyour 帳戶，讓驗證權杖的安全。</span><span class="sxs-lookup"><span data-stu-id="f1a48-148">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="f1a48-149">您的帳戶 SID 和授權權杖皆可檢視在 hello [Twilio 帳戶 頁面上][twilio_account]，請在 hello 欄位標示為**帳戶 SID**和**驗證語彙基元**分別。</span><span class="sxs-lookup"><span data-stu-id="f1a48-149">Your account SID and auth token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

### <span data-ttu-id="f1a48-150"><a id="VerifyPhoneNumbers"></a>驗證電話號碼</span><span class="sxs-lookup"><span data-stu-id="f1a48-150"><a id="VerifyPhoneNumbers"></a>Verify Phone Numbers</span></span>
<span data-ttu-id="f1a48-151">您也可以在您可以透過 Twilio 加法 toohello 數目、 確認用於控制 （也就是您的行動電話或家裡的電話號碼），在應用程式中的數字。</span><span class="sxs-lookup"><span data-stu-id="f1a48-151">In addition toohello number you are given by Twilio, you can also verify numbers that you control (i.e. your cell phone or home phone number) for use in your applications.</span></span> 

<span data-ttu-id="f1a48-152">如需詳細資訊 tooverify 電話號碼，請參閱[管理數字][verify_phone]。</span><span class="sxs-lookup"><span data-stu-id="f1a48-152">For information on how tooverify a phone number, see [Manage Numbers][verify_phone].</span></span>

## <span data-ttu-id="f1a48-153"><a id="create_app"></a>建立 Ruby 應用程式</span><span class="sxs-lookup"><span data-stu-id="f1a48-153"><a id="create_app"></a>Create a Ruby Application</span></span>
<span data-ttu-id="f1a48-154">使用 hello Twilio 服務和 Azure 中執行的 Ruby 應用程式是與任何其他拼音使用服務應用程式 hello Twilio 沒什麼不同了。</span><span class="sxs-lookup"><span data-stu-id="f1a48-154">A Ruby application that uses hello Twilio service and is running in Azure is no different than any other Ruby application that uses hello Twilio service.</span></span> <span data-ttu-id="f1a48-155">雖然 Twilio 服務是 RESTful，且可從 Ruby 呼叫數種方式，本文將著重在 toouse Twilio 的服務使用[Twilio Ruby 的協助程式程式庫][twilio_ruby]。</span><span class="sxs-lookup"><span data-stu-id="f1a48-155">While Twilio services are RESTful and can be called from Ruby in several ways, this article will focus on how toouse Twilio services with [Twilio helper library for Ruby][twilio_ruby].</span></span>

<span data-ttu-id="f1a48-156">首先，[安裝新的 Azure Linux VM] [ azure_vm_setup] tooact 做為新拼音 web 應用程式的主機。</span><span class="sxs-lookup"><span data-stu-id="f1a48-156">First, [set-up a new Azure Linux VM][azure_vm_setup] tooact as a host for your new Ruby web application.</span></span> <span data-ttu-id="f1a48-157">忽略涉及 hello 滑軌應用程式，只要安裝 hello VM 建立 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="f1a48-157">Ignore hello steps involving hello creation of a Rails app, just set-up hello VM.</span></span> <span data-ttu-id="f1a48-158">請確實建立具有外部連接埠 80 和內部連接埠 5000 的端點。</span><span class="sxs-lookup"><span data-stu-id="f1a48-158">Make sure you create an Endpoint with an external port of 80 and an internal port of 5000.</span></span>

<span data-ttu-id="f1a48-159">在 hello 下列範例中，我們將使用[Sinatra][sinatra]，Ruby 的非常簡單的 web 架構。</span><span class="sxs-lookup"><span data-stu-id="f1a48-159">In hello examples below, we will be using [Sinatra][sinatra], a very simple web framework for Ruby.</span></span> <span data-ttu-id="f1a48-160">但是，您一定可以使用為 Ruby hello Twilio 協助程式程式庫，與任何其他 web 架構，包括在滑軌上的 Ruby。</span><span class="sxs-lookup"><span data-stu-id="f1a48-160">But you can certainly use hello Twilio helper library for Ruby with any other web framework, including Ruby on Rails.</span></span>

<span data-ttu-id="f1a48-161">在您新的 VM 中加入 SSH，並為新的應用程式建立目錄。</span><span class="sxs-lookup"><span data-stu-id="f1a48-161">SSH into your new VM and create a directory for your new app.</span></span> <span data-ttu-id="f1a48-162">在該目錄中，建立檔案，稱為 Gemfile 並複製下列程式碼中的 hello:</span><span class="sxs-lookup"><span data-stu-id="f1a48-162">Inside that directory, create a file called Gemfile and copy hello following code into it:</span></span>

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

<span data-ttu-id="f1a48-163">Hello 命令列執行`bundle install`。</span><span class="sxs-lookup"><span data-stu-id="f1a48-163">On hello command line run `bundle install`.</span></span> <span data-ttu-id="f1a48-164">這會安裝上述 hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="f1a48-164">This will install hello dependencies above.</span></span> <span data-ttu-id="f1a48-165">接著，建立名為 `web.rb`的檔案。</span><span class="sxs-lookup"><span data-stu-id="f1a48-165">Next create a file called `web.rb`.</span></span> <span data-ttu-id="f1a48-166">這會是所在 hello web 應用程式的程式碼。</span><span class="sxs-lookup"><span data-stu-id="f1a48-166">This will be where hello code for your web app lives.</span></span> <span data-ttu-id="f1a48-167">貼上下列程式碼中的 hello:</span><span class="sxs-lookup"><span data-stu-id="f1a48-167">Paste hello following code into it:</span></span>

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

<span data-ttu-id="f1a48-168">此時您應該能夠執行的 hello hello 命令`ruby web.rb -p 5000`。</span><span class="sxs-lookup"><span data-stu-id="f1a48-168">At this point you should be able hello run hello command `ruby web.rb -p 5000`.</span></span> <span data-ttu-id="f1a48-169">這會在連接埠 5000 上啟動小型 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f1a48-169">This will spin-up a small web server on port 5000.</span></span> <span data-ttu-id="f1a48-170">您應該能夠 toobrowse toothis 應用程式在您的瀏覽器中造訪 hello URL 時所安裝的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="f1a48-170">You should be able toobrowse toothis app in your browser by visiting hello URL you set-up for your Azure VM.</span></span> <span data-ttu-id="f1a48-171">一旦可以達到 hello 瀏覽器中的 web 應用程式，您已準備好 toostart 建置 Twilio 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1a48-171">Once you can reach your web app in hello browser, you're ready toostart building a Twilio app.</span></span>

## <span data-ttu-id="f1a48-172"><a id="configure_app"></a>設定您的應用程式 tooUse Twilio</span><span class="sxs-lookup"><span data-stu-id="f1a48-172"><a id="configure_app"></a>Configure Your Application tooUse Twilio</span></span>
<span data-ttu-id="f1a48-173">您可以設定您 web 應用程式 toouse hello Twilio 程式庫，藉由更新您`Gemfile`tooinclude 這一行：</span><span class="sxs-lookup"><span data-stu-id="f1a48-173">You can configure your web app toouse hello Twilio library by updating your `Gemfile` tooinclude this line:</span></span>

    gem 'twilio-ruby'

<span data-ttu-id="f1a48-174">在 hello 命令列上執行`bundle install`。</span><span class="sxs-lookup"><span data-stu-id="f1a48-174">On hello command line, run `bundle install`.</span></span> <span data-ttu-id="f1a48-175">現在開啟`web.rb`，包括在 hello 頂端這一行：</span><span class="sxs-lookup"><span data-stu-id="f1a48-175">Now open `web.rb` and including this line at hello top:</span></span>

    require 'twilio-ruby'

<span data-ttu-id="f1a48-176">您現在需要設定所有 toouse hello Twilio 協助程式程式庫 Ruby web 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="f1a48-176">You're now all set toouse hello Twilio helper library for Ruby in your web app.</span></span>

## <span data-ttu-id="f1a48-177"><a id="howto_make_call"></a>作法：撥出電話</span><span class="sxs-lookup"><span data-stu-id="f1a48-177"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="f1a48-178">下列的 hello 會示範如何呼叫 toomake 傳出。</span><span class="sxs-lookup"><span data-stu-id="f1a48-178">hello following shows how toomake an outgoing call.</span></span> <span data-ttu-id="f1a48-179">重要概念包括使用 REST API 呼叫的拼音 toomake hello Twilio 協助程式程式庫和轉譯 TwiML。</span><span class="sxs-lookup"><span data-stu-id="f1a48-179">Key concepts include using hello Twilio helper library for Ruby toomake REST API calls and rendering TwiML.</span></span> <span data-ttu-id="f1a48-180">替換為您的值為 hello**從**和**至**電話號碼，並確保您確認 hello**從**電話號碼您 Twilio 帳戶先前 toorunning hello 撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="f1a48-180">Substitute your values for hello **From** and **To** phone numbers, and ensure that you verify hello **From** phone number for your Twilio account prior toorunning hello code.</span></span>

<span data-ttu-id="f1a48-181">新增此函式太`web.md`:</span><span class="sxs-lookup"><span data-stu-id="f1a48-181">Add this function too`web.md`:</span></span>

    # Set your account ID and authentication token.
    sid = "your_twilio_account_sid";
    token = "your_twilio_authentication_token";

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from = "NNNNNNNNNNN";

    # hello number of hello phone receiving call.
    too= "NNNNNNNNNNN";

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://yourdomain.cloudapp.net/voice_url";

    get '/make_call' do
      # Create hello call client.
      client = Twilio::REST::Client.new(sid, token);

      # Make hello call
      client.account.calls.create(to: to, from: from, url: url)
    end

    post '/voice_url' do
      "<Response>
         <Say>Hello Monkey!</Say>
       </Response>"
    end

<span data-ttu-id="f1a48-182">如果您開啟總`http://yourdomain.cloudapp.net/make_call`瀏覽器，就會觸發 hello 呼叫 toohello Twilio API toomake hello 電話通話。</span><span class="sxs-lookup"><span data-stu-id="f1a48-182">If you open-up `http://yourdomain.cloudapp.net/make_call` in a browser, that will trigger hello call toohello Twilio API toomake hello phone call.</span></span> <span data-ttu-id="f1a48-183">hello 中的前兩個參數`client.account.calls.create`會均相當容易理解： hello 數字的 hello 呼叫`from`和數字 hello 呼叫 hello `to`。</span><span class="sxs-lookup"><span data-stu-id="f1a48-183">hello first two parameters in `client.account.calls.create` are fairly self-explanatory: hello number hello call is `from` and hello number hello call is `to`.</span></span> 

<span data-ttu-id="f1a48-184">hello 第三個參數 (`url`) 是 hello Twilio 要求 tooget 指示哪些 toodo，一旦 hello 呼叫已連線的 URL。</span><span class="sxs-lookup"><span data-stu-id="f1a48-184">hello third parameter (`url`) is hello URL that Twilio requests tooget instructions on what toodo once hello call is connected.</span></span> <span data-ttu-id="f1a48-185">在此情況下我們設定的 URL (`http://yourdomain.cloudapp.net`)，傳回簡單的 TwiML 文件，並使用 hello`<Say>`動詞 toodo 一些文字轉換語音和假設接收"Hello 猴子"toohello 人 hello 呼叫。</span><span class="sxs-lookup"><span data-stu-id="f1a48-185">In this case we set-up a URL (`http://yourdomain.cloudapp.net`) that returns a simple TwiML document and uses hello `<Say>` verb toodo some text-to-speech and say "Hello Monkey" toohello person recieving hello call.</span></span>

## <span data-ttu-id="f1a48-186"><a id="howto_recieve_sms"></a>如何：接收 SMS 簡訊</span><span class="sxs-lookup"><span data-stu-id="f1a48-186"><a id="howto_recieve_sms"></a>How to: Recieve an SMS message</span></span>
<span data-ttu-id="f1a48-187">Hello 前一個範例中我們起始**傳出**通話。</span><span class="sxs-lookup"><span data-stu-id="f1a48-187">In hello previous example we initiated an **outgoing** phone call.</span></span> <span data-ttu-id="f1a48-188">這個時間，我們將使用的 Twilio 給予我們期間註冊 tooprocess hello 電話號碼**傳入**SMS 訊息。</span><span class="sxs-lookup"><span data-stu-id="f1a48-188">This time, let's use hello phone number that Twilio gave us during sign-up tooprocess an **incoming** SMS message.</span></span>

<span data-ttu-id="f1a48-189">首先，登入 tooyour [Twilio 儀表板][twilio_account]。</span><span class="sxs-lookup"><span data-stu-id="f1a48-189">First, log-in tooyour [Twilio dashboard][twilio_account].</span></span> <span data-ttu-id="f1a48-190">按一下 「 號碼 」 中 hello 上層瀏覽，，然後按一下 hello Twilio 所提供的數字。</span><span class="sxs-lookup"><span data-stu-id="f1a48-190">Click on "Numbers" in hello top nav and then click on hello Twilio number you were provided.</span></span> <span data-ttu-id="f1a48-191">您會看見兩個可以設定的 URL。</span><span class="sxs-lookup"><span data-stu-id="f1a48-191">You'll see two URLs that you can configure.</span></span> <span data-ttu-id="f1a48-192">語音要求 URL 和簡訊要求 URL。</span><span class="sxs-lookup"><span data-stu-id="f1a48-192">A Voice Request URL and an SMS Request URL.</span></span> <span data-ttu-id="f1a48-193">這些是 hello Url 的 Twilio 電話時已呼叫或 SMS 傳送 tooyour 數目。</span><span class="sxs-lookup"><span data-stu-id="f1a48-193">These are hello URLs that Twilio calls whenever a phone call is made or an SMS is sent tooyour number.</span></span> <span data-ttu-id="f1a48-194">hello Url 也可稱為 「 web 勾點 」。</span><span class="sxs-lookup"><span data-stu-id="f1a48-194">hello URLs are also known as "web hooks".</span></span>

<span data-ttu-id="f1a48-195">我們希望 tooprocess 傳入的 SMS 訊息，因此讓我們先更新 hello URL 太`http://yourdomain.cloudapp.net/sms_url`。</span><span class="sxs-lookup"><span data-stu-id="f1a48-195">We would like tooprocess incoming SMS messages, so let's update hello URL too`http://yourdomain.cloudapp.net/sms_url`.</span></span> <span data-ttu-id="f1a48-196">請繼續並按一下 在 hello hello 頁面底部的 儲存變更。</span><span class="sxs-lookup"><span data-stu-id="f1a48-196">Go ahead and click Save Changes at hello bottom of hello page.</span></span> <span data-ttu-id="f1a48-197">現在，回到`web.rb`我們這程式我們的應用程式 toohandle:</span><span class="sxs-lookup"><span data-stu-id="f1a48-197">Now, back in `web.rb` let's program our application toohandle this:</span></span>

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for hello ping! Twilio and Azure rock!</Message>
       </Response>"
    end

<span data-ttu-id="f1a48-198">Hello 變更後，請確定 toore 開始您的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1a48-198">After making hello change, make sure toore-start your web app.</span></span> <span data-ttu-id="f1a48-199">現在，取出您的電話，並傳送 SMS tooyour Twilio 數目。</span><span class="sxs-lookup"><span data-stu-id="f1a48-199">Now, take out your phone and send an SMS tooyour Twilio number.</span></span> <span data-ttu-id="f1a48-200">您應該立即取得 SMS 回應，指出 「 < Hey，hello ping 感謝您 ！</span><span class="sxs-lookup"><span data-stu-id="f1a48-200">You should promptly get an SMS response that says "Hey, thanks for hello ping!</span></span> <span data-ttu-id="f1a48-201">Twilio and Azure rock!"。</span><span class="sxs-lookup"><span data-stu-id="f1a48-201">Twilio and Azure rock!".</span></span>

## <span data-ttu-id="f1a48-202"><a id="additional_services"></a>如何：使用其他 Twilio 服務</span><span class="sxs-lookup"><span data-stu-id="f1a48-202"><a id="additional_services"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="f1a48-203">此外 toohello 範例所示，Twilio 提供網頁型應用程式開發介面，您可以使用其他 Twilio 功能 tooleverage 從 Azure 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1a48-203">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="f1a48-204">完整的詳細資訊，請參閱 hello [Twilio API 文件][twilio_api_documentation]。</span><span class="sxs-lookup"><span data-stu-id="f1a48-204">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

### <span data-ttu-id="f1a48-205"><a id="NextSteps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="f1a48-205"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="f1a48-206">既然您已經學會 hello hello Twilio 服務基本概念，請依照下列多個這些連結 toolearn:</span><span class="sxs-lookup"><span data-stu-id="f1a48-206">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="f1a48-207">[Twilio 安全性方針][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="f1a48-207">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="f1a48-208">[Twilio 作法與範例程式碼][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="f1a48-208">[Twilio HowTos and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="f1a48-209">[Twilio 快速入門教學課程][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="f1a48-209">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="f1a48-210">[GitHub 上的 Twilio][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="f1a48-210">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="f1a48-211">[Talk tooTwilio 支援][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="f1a48-211">[Talk tooTwilio Support][twilio_support]</span></span>

[twilio_ruby]: https://www.twilio.com/docs/ruby/install





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
[sinatra]: http://www.sinatrarb.com/
[azure_vm_setup]: http://www.windowsazure.com/develop/ruby/tutorials/web-app-with-linux-vm/
