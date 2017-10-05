---
title: "如何使用 Twilio for Voice and SMS (Ruby) | Microsoft Docs"
description: "了解如何在 Azure 上使用 Twilio API 服務撥打電話及傳送簡訊。 程式碼範例以 Ruby 撰寫。"
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
ms.openlocfilehash: 69e50e7fe0e1f302e96c309878b8dea6869dff4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-ruby"></a><span data-ttu-id="88d14-104">如何在 Ruby 中透過 Twilio 使用語音和簡訊功能</span><span class="sxs-lookup"><span data-stu-id="88d14-104">How to Use Twilio for Voice and SMS Capabilities in Ruby</span></span>
<span data-ttu-id="88d14-105">本指南示範如何在 Azure 上透過 Twilio API 服務執行常見的程式設計工作。</span><span class="sxs-lookup"><span data-stu-id="88d14-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="88d14-106">涵蓋的案例包括打電話和傳送簡訊 (SMS)。</span><span class="sxs-lookup"><span data-stu-id="88d14-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="88d14-107">如需有關如何在應用程式中使用 Twilio 語音和 SMS 的詳細資訊，請參閱 [後續步驟](#NextSteps) 一節。</span><span class="sxs-lookup"><span data-stu-id="88d14-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="88d14-108"><a id="WhatIs"></a>什麼是 Twilio？</span><span class="sxs-lookup"><span data-stu-id="88d14-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="88d14-109">Twilio 是一種電話語音 Web 服務 API，能夠讓您使用現有的 Web 語言和技術建立語音和 SMS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="88d14-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills to build voice and SMS applications.</span></span> <span data-ttu-id="88d14-110">Twilio 算是協力廠商服務 (並非 Azure 功能，也並非 Microsoft 產品)。</span><span class="sxs-lookup"><span data-stu-id="88d14-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="88d14-111">**Twilio 語音** 可讓應用程式撥打和接聽電話。</span><span class="sxs-lookup"><span data-stu-id="88d14-111">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="88d14-112">**Twilio SMS** 可以讓您的應用程式撰寫和接收 SMS 訊息。</span><span class="sxs-lookup"><span data-stu-id="88d14-112">**Twilio SMS** allows your applications to make and receive SMS messages.</span></span> <span data-ttu-id="88d14-113">**Twilio Client** 可以讓您的應用程式在現有網際網路連線 (包括行動連線) 中啟用語音通訊。</span><span class="sxs-lookup"><span data-stu-id="88d14-113">**Twilio Client** allows your applications to enable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="88d14-114"><a id="Pricing"></a>Twilio 定價和特別優惠</span><span class="sxs-lookup"><span data-stu-id="88d14-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="88d14-115">[Twilio 定價][twilio_pricing] (英文) 提供 Twilio 的定價資訊。</span><span class="sxs-lookup"><span data-stu-id="88d14-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="88d14-116">Azure 客戶可獲得[特殊優惠][special_offer]：免費 1000 則文字簡訊或接聽 1000 分鐘電話。</span><span class="sxs-lookup"><span data-stu-id="88d14-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="88d14-117">若要註冊獲得這項優惠或取得詳細資訊，請造訪 [http://ahoy.twilio.com/azure][special_offer] (英文)。</span><span class="sxs-lookup"><span data-stu-id="88d14-117">To sign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>  

## <span data-ttu-id="88d14-118"><a id="Concepts"></a>概念</span><span class="sxs-lookup"><span data-stu-id="88d14-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="88d14-119">Twilio API 是一套為應用程式提供語音和簡訊功能的 RESTful API。</span><span class="sxs-lookup"><span data-stu-id="88d14-119">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="88d14-120">用戶端程式庫有多種語言版本，相關清單請參閱 [Twilio API 程式庫][twilio_libraries]。</span><span class="sxs-lookup"><span data-stu-id="88d14-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

### <span data-ttu-id="88d14-121"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="88d14-121"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="88d14-122">TwiML 是一組以 XML 為基礎的指令，可指示 Twilio 如何處理來電或簡訊。</span><span class="sxs-lookup"><span data-stu-id="88d14-122">TwiML is a set of XML-based instructions that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="88d14-123">例如，下列 TwiML 會將 **Hello World** 文字轉換成語音。</span><span class="sxs-lookup"><span data-stu-id="88d14-123">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="88d14-124">所有 TwiML 文件皆會以 `<Response>` 作為其根元素。</span><span class="sxs-lookup"><span data-stu-id="88d14-124">All TwiML documents have `<Response>` as their root element.</span></span> <span data-ttu-id="88d14-125">您可以由此處使用 Twilio 動詞定義應用程式的行為。</span><span class="sxs-lookup"><span data-stu-id="88d14-125">From there, you use Twilio Verbs to define the behavior of your application.</span></span>

### <span data-ttu-id="88d14-126"><a id="Verbs"></a>TwiML 動詞</span><span class="sxs-lookup"><span data-stu-id="88d14-126"><a id="Verbs"></a>TwiML Verbs</span></span>
<span data-ttu-id="88d14-127">Twilio 動詞是指示 Twilio 應執行哪些 **動作**的 XML 標籤。</span><span class="sxs-lookup"><span data-stu-id="88d14-127">Twilio Verbs are XML tags that tell Twilio what to **do**.</span></span> <span data-ttu-id="88d14-128">例如，**&lt;Say&gt;** 動詞會指示 Twilio 在通話中用語音傳遞訊息。</span><span class="sxs-lookup"><span data-stu-id="88d14-128">For example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span> 

<span data-ttu-id="88d14-129">以下是 Twilio 動詞清單。</span><span class="sxs-lookup"><span data-stu-id="88d14-129">The following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="88d14-130">**&lt;撥號&gt;**：使撥號者接通另一支電話。</span><span class="sxs-lookup"><span data-stu-id="88d14-130">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="88d14-131">**&lt;收集&gt;**：收集電話按鍵上輸入的號碼。</span><span class="sxs-lookup"><span data-stu-id="88d14-131">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="88d14-132">**&lt;掛斷&gt;**：結束通話。</span><span class="sxs-lookup"><span data-stu-id="88d14-132">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="88d14-133">**&lt;播放&gt;**：播放音訊檔案。</span><span class="sxs-lookup"><span data-stu-id="88d14-133">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="88d14-134">**&lt;暫停&gt;**：靜候一段指定的秒數。</span><span class="sxs-lookup"><span data-stu-id="88d14-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="88d14-135">**&lt;記錄&gt;**：錄製來電者的語音並傳回含有錄音的檔案 URL。</span><span class="sxs-lookup"><span data-stu-id="88d14-135">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="88d14-136">**&lt;重新導向&gt;**：將通話或簡訊的控制權移轉至不同 URL 的 TwiML。</span><span class="sxs-lookup"><span data-stu-id="88d14-136">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="88d14-137">**&lt;拒絕&gt;**：拒絕 Twilio 號碼的來電而不計費</span><span class="sxs-lookup"><span data-stu-id="88d14-137">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="88d14-138">**&lt;說出&gt;**：將來電的文字轉換成語音。</span><span class="sxs-lookup"><span data-stu-id="88d14-138">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="88d14-139">**&lt;Sms&gt;**：傳送簡訊。</span><span class="sxs-lookup"><span data-stu-id="88d14-139">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

<span data-ttu-id="88d14-140">如需 Twilio 動詞、屬性和 TwiML 的詳細資訊，請參閱 [TwiML][twiml]。</span><span class="sxs-lookup"><span data-stu-id="88d14-140">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="88d14-141">如需 Twilio API 的詳細資訊，請參閱 [Twilio API][twilio_api]。</span><span class="sxs-lookup"><span data-stu-id="88d14-141">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="88d14-142"><a id="CreateAccount"></a>建立 Twilio 帳戶</span><span class="sxs-lookup"><span data-stu-id="88d14-142"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="88d14-143">準備取得 Twilio 帳戶時，請至[試用 Twilio][try_twilio] 註冊。</span><span class="sxs-lookup"><span data-stu-id="88d14-143">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="88d14-144">您可以先使用免費帳戶，稍後再升級帳戶。</span><span class="sxs-lookup"><span data-stu-id="88d14-144">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="88d14-145">註冊 Twilio 帳戶時，您會獲得可供應用程式使用的免費電話號碼。</span><span class="sxs-lookup"><span data-stu-id="88d14-145">When you sign up for a Twilio account, you'll get a free phone number for your application.</span></span> <span data-ttu-id="88d14-146">您也會獲得帳戶 SID 和驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="88d14-146">You'll also receive an account SID and an auth token.</span></span> <span data-ttu-id="88d14-147">兩者皆為呼叫 Twilio API 所需。</span><span class="sxs-lookup"><span data-stu-id="88d14-147">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="88d14-148">為了防止未經授權存取您的帳戶，您妥善保管驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="88d14-148">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="88d14-149">在 [Twilio 帳戶頁面][twilio_account] 的 **ACCOUNT SID** 和 **AUTH TOKEN** 欄位中，分別可檢視您的帳戶 SID 和驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="88d14-149">Your account SID and auth token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

### <span data-ttu-id="88d14-150"><a id="VerifyPhoneNumbers"></a>驗證電話號碼</span><span class="sxs-lookup"><span data-stu-id="88d14-150"><a id="VerifyPhoneNumbers"></a>Verify Phone Numbers</span></span>
<span data-ttu-id="88d14-151">除了 Twilio 提供給您的號碼以外，您也可以驗證您在應用程式中控管使用性的號碼 (也就是您的行動電話或家用電話號碼)。</span><span class="sxs-lookup"><span data-stu-id="88d14-151">In addition to the number you are given by Twilio, you can also verify numbers that you control (i.e. your cell phone or home phone number) for use in your applications.</span></span> 

<span data-ttu-id="88d14-152">如需有關如何驗證電話號碼的詳細資訊，請參閱[管理電話號碼][verify_phone]。</span><span class="sxs-lookup"><span data-stu-id="88d14-152">For information on how to verify a phone number, see [Manage Numbers][verify_phone].</span></span>

## <span data-ttu-id="88d14-153"><a id="create_app"></a>建立 Ruby 應用程式</span><span class="sxs-lookup"><span data-stu-id="88d14-153"><a id="create_app"></a>Create a Ruby Application</span></span>
<span data-ttu-id="88d14-154">使用 Twilio 服務且執行於 Azure 的 Ruby 應用程式，與其他使用 Twilio 服務的 Ruby 應用程式並無不同。</span><span class="sxs-lookup"><span data-stu-id="88d14-154">A Ruby application that uses the Twilio service and is running in Azure is no different than any other Ruby application that uses the Twilio service.</span></span> <span data-ttu-id="88d14-155">雖然 Twilio 服務是以 REST 為基礎，並且可透過數種方式從 Ruby 撥打，但本文的重點是要說明如何搭配使用 Twilio 服務與[適用於 Ruby 的 Twilio 協助程式程式庫][twilio_ruby]。</span><span class="sxs-lookup"><span data-stu-id="88d14-155">While Twilio services are RESTful and can be called from Ruby in several ways, this article will focus on how to use Twilio services with [Twilio helper library for Ruby][twilio_ruby].</span></span>

<span data-ttu-id="88d14-156">首先，請[設定新的 Azure Linux VM][azure_vm_setup]，以作為新的 Ruby Web 應用程式主機。</span><span class="sxs-lookup"><span data-stu-id="88d14-156">First, [set-up a new Azure Linux VM][azure_vm_setup] to act as a host for your new Ruby web application.</span></span> <span data-ttu-id="88d14-157">請忽略建立 Rails 應用程式的相關步驟，直接設定 VM。</span><span class="sxs-lookup"><span data-stu-id="88d14-157">Ignore the steps involving the creation of a Rails app, just set-up the VM.</span></span> <span data-ttu-id="88d14-158">請確實建立具有外部連接埠 80 和內部連接埠 5000 的端點。</span><span class="sxs-lookup"><span data-stu-id="88d14-158">Make sure you create an Endpoint with an external port of 80 and an internal port of 5000.</span></span>

<span data-ttu-id="88d14-159">我們在下列範例中將使用 [Sinatra][sinatra]，這對 Ruby 而言是非常簡單的 Web 架構。</span><span class="sxs-lookup"><span data-stu-id="88d14-159">In the examples below, we will be using [Sinatra][sinatra], a very simple web framework for Ruby.</span></span> <span data-ttu-id="88d14-160">但適用於 Ruby 的 Twilio 協助程式程式庫是可以與任何其他 Web 架構搭配運作的，包括 Rails 上的 Ruby。</span><span class="sxs-lookup"><span data-stu-id="88d14-160">But you can certainly use the Twilio helper library for Ruby with any other web framework, including Ruby on Rails.</span></span>

<span data-ttu-id="88d14-161">在您新的 VM 中加入 SSH，並為新的應用程式建立目錄。</span><span class="sxs-lookup"><span data-stu-id="88d14-161">SSH into your new VM and create a directory for your new app.</span></span> <span data-ttu-id="88d14-162">請在該目錄中建立名為 Gemfile 的檔案，並將下列程式碼複製到檔案中：</span><span class="sxs-lookup"><span data-stu-id="88d14-162">Inside that directory, create a file called Gemfile and copy the following code into it:</span></span>

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

<span data-ttu-id="88d14-163">在命令列上執行 `bundle install`。</span><span class="sxs-lookup"><span data-stu-id="88d14-163">On the command line run `bundle install`.</span></span> <span data-ttu-id="88d14-164">這會安裝前述的相依性。</span><span class="sxs-lookup"><span data-stu-id="88d14-164">This will install the dependencies above.</span></span> <span data-ttu-id="88d14-165">接著，建立名為 `web.rb`的檔案。</span><span class="sxs-lookup"><span data-stu-id="88d14-165">Next create a file called `web.rb`.</span></span> <span data-ttu-id="88d14-166">Web 應用程式的程式碼會存留於該處。</span><span class="sxs-lookup"><span data-stu-id="88d14-166">This will be where the code for your web app lives.</span></span> <span data-ttu-id="88d14-167">請將下列程式碼貼到檔案中：</span><span class="sxs-lookup"><span data-stu-id="88d14-167">Paste the following code into it:</span></span>

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

<span data-ttu-id="88d14-168">此時，您應可執行 `ruby web.rb -p 5000`命令。</span><span class="sxs-lookup"><span data-stu-id="88d14-168">At this point you should be able the run the command `ruby web.rb -p 5000`.</span></span> <span data-ttu-id="88d14-169">這會在連接埠 5000 上啟動小型 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="88d14-169">This will spin-up a small web server on port 5000.</span></span> <span data-ttu-id="88d14-170">您應可在瀏覽器中造訪您為 Azure VM 設定的 URL，而瀏覽至此應用程式。</span><span class="sxs-lookup"><span data-stu-id="88d14-170">You should be able to browse to this app in your browser by visiting the URL you set-up for your Azure VM.</span></span> <span data-ttu-id="88d14-171">只要您可在瀏覽器中存取您的 Web 應用程式，您即可開始建置 Twilio 應用程式。</span><span class="sxs-lookup"><span data-stu-id="88d14-171">Once you can reach your web app in the browser, you're ready to start building a Twilio app.</span></span>

## <span data-ttu-id="88d14-172"><a id="configure_app"></a>設定應用程式以使用 Twilio</span><span class="sxs-lookup"><span data-stu-id="88d14-172"><a id="configure_app"></a>Configure Your Application to Use Twilio</span></span>
<span data-ttu-id="88d14-173">您可以更新 `Gemfile` 以加入下一行程式碼，將 Web 應用程式設為使用 Twilio 程式庫：</span><span class="sxs-lookup"><span data-stu-id="88d14-173">You can configure your web app to use the Twilio library by updating your `Gemfile` to include this line:</span></span>

    gem 'twilio-ruby'

<span data-ttu-id="88d14-174">在命令列上執行 `bundle install`。</span><span class="sxs-lookup"><span data-stu-id="88d14-174">On the command line, run `bundle install`.</span></span> <span data-ttu-id="88d14-175">接著，開啟 `web.rb` ，並將此行加入至頂端：</span><span class="sxs-lookup"><span data-stu-id="88d14-175">Now open `web.rb` and including this line at the top:</span></span>

    require 'twilio-ruby'

<span data-ttu-id="88d14-176">至此一切皆已就緒，您可以在 Web 應用程式中使用適用於 Ruby 的 Twilio 協助程式程式庫。</span><span class="sxs-lookup"><span data-stu-id="88d14-176">You're now all set to use the Twilio helper library for Ruby in your web app.</span></span>

## <span data-ttu-id="88d14-177"><a id="howto_make_call"></a>作法：撥出電話</span><span class="sxs-lookup"><span data-stu-id="88d14-177"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="88d14-178">下列程式碼將說明如何向外撥打電話。</span><span class="sxs-lookup"><span data-stu-id="88d14-178">The following shows how to make an outgoing call.</span></span> <span data-ttu-id="88d14-179">主要的概念包括使用適用於 Ruby 的 Twilio 協助程式程式庫，來撥打 REST API 電話以及轉譯 TwiML。</span><span class="sxs-lookup"><span data-stu-id="88d14-179">Key concepts include using the Twilio helper library for Ruby to make REST API calls and rendering TwiML.</span></span> <span data-ttu-id="88d14-180">請將 **From** 和 **To** 電話號碼換成您的值，在執行程式碼之前，請記得先驗證 Twilio 帳戶的 **From** 電話號碼。</span><span class="sxs-lookup"><span data-stu-id="88d14-180">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span></span>

<span data-ttu-id="88d14-181">將此函數新增至 `web.md`：</span><span class="sxs-lookup"><span data-stu-id="88d14-181">Add this function to `web.md`:</span></span>

    # Set your account ID and authentication token.
    sid = "your_twilio_account_sid";
    token = "your_twilio_authentication_token";

    # The number of the phone initiating the the call.
    # This should either be a Twilio number or a number that you've verified
    from = "NNNNNNNNNNN";

    # The number of the phone receiving call.
    to = "NNNNNNNNNNN";

    # Use the Twilio-provided site for the TwiML response.
    url = "http://yourdomain.cloudapp.net/voice_url";

    get '/make_call' do
      # Create the call client.
      client = Twilio::REST::Client.new(sid, token);

      # Make the call
      client.account.calls.create(to: to, from: from, url: url)
    end

    post '/voice_url' do
      "<Response>
         <Say>Hello Monkey!</Say>
       </Response>"
    end

<span data-ttu-id="88d14-182">您在瀏覽器中開啟 `http://yourdomain.cloudapp.net/make_call` 時，將觸發對 Twilio API 的呼叫來撥打電話。</span><span class="sxs-lookup"><span data-stu-id="88d14-182">If you open-up `http://yourdomain.cloudapp.net/make_call` in a browser, that will trigger the call to the Twilio API to make the phone call.</span></span> <span data-ttu-id="88d14-183">`client.account.calls.create` 中的前兩個參數很容易理解：來電 (`from`) 號碼和去電 (`to`) 號碼。</span><span class="sxs-lookup"><span data-stu-id="88d14-183">The first two parameters in `client.account.calls.create` are fairly self-explanatory: the number the call is `from` and the number the call is `to`.</span></span> 

<span data-ttu-id="88d14-184">第三個參數 (`url`) 是 Twilio 要求取得相關指示以得知在電話接通時應執行何種動作的 URL。</span><span class="sxs-lookup"><span data-stu-id="88d14-184">The third parameter (`url`) is the URL that Twilio requests to get instructions on what to do once the call is connected.</span></span> <span data-ttu-id="88d14-185">在此案例中，我們設定的 URL (`http://yourdomain.cloudapp.net`) 會傳回簡易的 TwiML 文件，並使用 `<Say>` 動詞來執行文字轉換成語音的動作，對接聽電話的人說出 "Hello Monkey"。</span><span class="sxs-lookup"><span data-stu-id="88d14-185">In this case we set-up a URL (`http://yourdomain.cloudapp.net`) that returns a simple TwiML document and uses the `<Say>` verb to do some text-to-speech and say "Hello Monkey" to the person recieving the call.</span></span>

## <span data-ttu-id="88d14-186"><a id="howto_recieve_sms"></a>如何：接收 SMS 簡訊</span><span class="sxs-lookup"><span data-stu-id="88d14-186"><a id="howto_recieve_sms"></a>How to: Recieve an SMS message</span></span>
<span data-ttu-id="88d14-187">在前述範例中，我們撥打了 **外撥** 電話。</span><span class="sxs-lookup"><span data-stu-id="88d14-187">In the previous example we initiated an **outgoing** phone call.</span></span> <span data-ttu-id="88d14-188">現在，我們要使用 Twilio 在註冊期間提供給我們的電話號碼來處理 **傳入的** 簡訊。</span><span class="sxs-lookup"><span data-stu-id="88d14-188">This time, let's use the phone number that Twilio gave us during sign-up to process an **incoming** SMS message.</span></span>

<span data-ttu-id="88d14-189">首先，請登入您的 [Twilio 儀表板][twilio_account]。</span><span class="sxs-lookup"><span data-stu-id="88d14-189">First, log-in to your [Twilio dashboard][twilio_account].</span></span> <span data-ttu-id="88d14-190">在頂端的導覽區中按一下「號碼」，然後按一下 Twilio 提供給您的號碼。</span><span class="sxs-lookup"><span data-stu-id="88d14-190">Click on "Numbers" in the top nav and then click on the Twilio number you were provided.</span></span> <span data-ttu-id="88d14-191">您會看見兩個可以設定的 URL。</span><span class="sxs-lookup"><span data-stu-id="88d14-191">You'll see two URLs that you can configure.</span></span> <span data-ttu-id="88d14-192">語音要求 URL 和簡訊要求 URL。</span><span class="sxs-lookup"><span data-stu-id="88d14-192">A Voice Request URL and an SMS Request URL.</span></span> <span data-ttu-id="88d14-193">這是在撥打電話或傳送簡訊至您的號碼時，Twilio 所將呼叫的 URL。</span><span class="sxs-lookup"><span data-stu-id="88d14-193">These are the URLs that Twilio calls whenever a phone call is made or an SMS is sent to your number.</span></span> <span data-ttu-id="88d14-194">這些 URL 也稱為 "Web hook"。</span><span class="sxs-lookup"><span data-stu-id="88d14-194">The URLs are also known as "web hooks".</span></span>

<span data-ttu-id="88d14-195">我們想要處理傳入的 SMS 簡訊，因此，要將 URL 更新為 `http://yourdomain.cloudapp.net/sms_url`。</span><span class="sxs-lookup"><span data-stu-id="88d14-195">We would like to process incoming SMS messages, so let's update the URL to `http://yourdomain.cloudapp.net/sms_url`.</span></span> <span data-ttu-id="88d14-196">接著，按一下頁面底部的 [儲存變更]。</span><span class="sxs-lookup"><span data-stu-id="88d14-196">Go ahead and click Save Changes at the bottom of the page.</span></span> <span data-ttu-id="88d14-197">現在，要在 `web.rb` 中將應用程式程式化，以進行相關處理：</span><span class="sxs-lookup"><span data-stu-id="88d14-197">Now, back in `web.rb` let's program our application to handle this:</span></span>

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for the ping! Twilio and Azure rock!</Message>
       </Response>"
    end

<span data-ttu-id="88d14-198">進行變更後，請確實重新啟動 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="88d14-198">After making the change, make sure to re-start your web app.</span></span> <span data-ttu-id="88d14-199">現在，請拿起電話，傳送簡訊至您的 Twilio 號碼。</span><span class="sxs-lookup"><span data-stu-id="88d14-199">Now, take out your phone and send an SMS to your Twilio number.</span></span> <span data-ttu-id="88d14-200">您應會立即收到簡訊回應，顯示 "Hey, thanks for the ping!</span><span class="sxs-lookup"><span data-stu-id="88d14-200">You should promptly get an SMS response that says "Hey, thanks for the ping!</span></span> <span data-ttu-id="88d14-201">Twilio and Azure rock!"。</span><span class="sxs-lookup"><span data-stu-id="88d14-201">Twilio and Azure rock!".</span></span>

## <span data-ttu-id="88d14-202"><a id="additional_services"></a>如何：使用其他 Twilio 服務</span><span class="sxs-lookup"><span data-stu-id="88d14-202"><a id="additional_services"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="88d14-203">除了此處所示的範例以外，Twilio 還提供網頁式 API，方便您從 Azure 應用程式中充份利用其他 Twilio 功能。</span><span class="sxs-lookup"><span data-stu-id="88d14-203">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="88d14-204">如需完整詳細資料，請參閱 [Twilio API 文件][twilio_api_documentation]。</span><span class="sxs-lookup"><span data-stu-id="88d14-204">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

### <span data-ttu-id="88d14-205"><a id="NextSteps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="88d14-205"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="88d14-206">了解基本的 Twilio 服務之後，請參考下列連結以取得更多資訊：</span><span class="sxs-lookup"><span data-stu-id="88d14-206">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="88d14-207">[Twilio 安全性方針][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="88d14-207">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="88d14-208">[Twilio 作法與範例程式碼][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="88d14-208">[Twilio HowTos and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="88d14-209">[Twilio 快速入門教學課程][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="88d14-209">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="88d14-210">[GitHub 上的 Twilio][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="88d14-210">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="88d14-211">[洽詢 Twilio 支援][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="88d14-211">[Talk to Twilio Support][twilio_support]</span></span>

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
