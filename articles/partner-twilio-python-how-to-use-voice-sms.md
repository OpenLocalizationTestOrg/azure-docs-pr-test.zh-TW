---
title: "如何使用 Twilio for Voice and SMS (Python) | Microsoft Docs"
description: "了解如何在 Azure 上使用 Twilio API 服務撥打電話及傳送簡訊。 程式碼範例以 Python 撰寫。"
services: 
documentationcenter: python
author: devinrader
manager: twilio
editor: 
ms.assetid: 561bc75b-4ac4-40ba-bcba-48e901f27cc3
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: f4a02bb7a7c46e7a0e3c75b870c522eae8294339
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-python"></a><span data-ttu-id="e7d0e-104">如何在 Python 中透過 Twilio 使用語音和簡訊功能</span><span class="sxs-lookup"><span data-stu-id="e7d0e-104">How to Use Twilio for Voice and SMS Capabilities in Python</span></span>
<span data-ttu-id="e7d0e-105">本指南示範如何在 Azure 上透過 Twilio API 服務執行常見的程式設計工作。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="e7d0e-106">涵蓋的案例包括打電話和傳送簡訊 (SMS)。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="e7d0e-107">如需有關如何在應用程式中使用 Twilio 語音和 SMS 的詳細資訊，請參閱 [後續步驟](#NextSteps) 一節。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="e7d0e-108"><a id="WhatIs"></a>什麼是 Twilio？</span><span class="sxs-lookup"><span data-stu-id="e7d0e-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="e7d0e-109">Twilio 正在形塑商業環境的未來，可讓開發人員將語音、VoIP 和訊息傳送內嵌到應用程式中。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="e7d0e-110">它們將雲端、全球化環境中所需的整個基礎結構虛擬化，透過 Twilio 通訊 API 平台來揭露基礎結構。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span></span> <span data-ttu-id="e7d0e-111">輕鬆就可建立和擴充應用程式。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-111">Applications are simple to build and scalable.</span></span> <span data-ttu-id="e7d0e-112">享受隨收隨付定價的彈性和雲端可靠性的好處。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="e7d0e-113">**Twilio 語音** 可讓應用程式撥打和接聽電話。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-113">**Twilio Voice** allows your applications to make and receive phone calls.</span></span>
<span data-ttu-id="e7d0e-114">**Twilio 簡訊** 可讓應用程式收發簡訊。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-114">**Twilio SMS** enables your application to send and receive text messages.</span></span>
<span data-ttu-id="e7d0e-115">**Twilio 用戶端** 可讓您從任何電話、平板電腦或瀏覽器撥打 VoIP 電話，且支援 WebRTC。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="e7d0e-116"><a id="Pricing"></a>Twilio 定價和特別優惠</span><span class="sxs-lookup"><span data-stu-id="e7d0e-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="e7d0e-117">Azure 客戶可在升級 Twilio 帳戶時獲得價值 10 元美金的 Twilio 點數[特殊優惠][special_offer]。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-117">Azure customers receive a [special offer][special_offer] $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="e7d0e-118">此 Twilio 點數可用來折抵任何 Twilio 使用量 ($10 點數相當於最多傳送 1,000 則簡訊，或最多接收 1000 分鐘的撥入語音，視電話號碼所在地點或通話目的地而定)。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span></span> <span data-ttu-id="e7d0e-119">請兌換此 [Twilio 點數][special_offer]，並開始使用。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-119">Redeem this [Twilio credit][special_offer] and get started.</span></span>

<span data-ttu-id="e7d0e-120">Twilio 是隨收隨付的服務。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="e7d0e-121">不需要設定費，隨時都可結清帳戶。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="e7d0e-122">如需詳細資訊，請參閱 [Twilio 價格][twilio_pricing]。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="e7d0e-123"><a id="Concepts"></a>概念</span><span class="sxs-lookup"><span data-stu-id="e7d0e-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="e7d0e-124">Twilio API 是一套為應用程式提供語音和簡訊功能的 RESTful API。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="e7d0e-125">用戶端程式庫有多種語言版本，相關清單請參閱 [Twilio API 程式庫][twilio_libraries]。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="e7d0e-126">Twilio API 的兩大重點是 Twilio 動詞和 Twilio 標記語言 (TwiML)。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="e7d0e-127"><a id="Verbs"></a>Twilio 動詞</span><span class="sxs-lookup"><span data-stu-id="e7d0e-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="e7d0e-128">API 採用 Twilio 動詞。例如，**&lt;Say&gt;** 動詞指示 Twilio 在通話中用語音傳遞訊息。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="e7d0e-129">以下是 Twilio 動詞清單。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-129">The following is a list of Twilio verbs.</span></span> <span data-ttu-id="e7d0e-130">如需了解其他動詞和功能，請參閱 [Twilio 標記語言文件][twiml]。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation][twiml].</span></span>

* <span data-ttu-id="e7d0e-131">**&lt;撥號&gt;**：使撥號者接通另一支電話。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="e7d0e-132">**&lt;收集&gt;**：收集電話按鍵上輸入的號碼。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="e7d0e-133">**&lt;掛斷&gt;**：結束通話。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="e7d0e-134">**&lt;暫停&gt;**：靜候一段指定的秒數。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="e7d0e-135">**&lt;播放&gt;**：播放音訊檔案。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-135">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="e7d0e-136">**&lt;佇列&gt;**︰新增至呼叫端佇列。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-136">**&lt;Queue&gt;**: Add the to a queue of callers.</span></span>
* <span data-ttu-id="e7d0e-137">**&lt;錄音&gt;**：錄製來電者的語音並傳回含有錄音的檔案 URL。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-137">**&lt;Record&gt;**: Records the voice of the caller and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="e7d0e-138">**&lt;重新導向&gt;**：將通話或簡訊的控制權移轉至不同 URL 的 TwiML。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-138">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="e7d0e-139">**&lt;拒絕&gt;**：拒絕 Twilio 號碼的來電而不計費。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-139">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you.</span></span>
* <span data-ttu-id="e7d0e-140">**&lt;說出&gt;**：將來電的文字轉換成語音。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-140">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="e7d0e-141">**&lt;Sms&gt;**：傳送簡訊。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-141">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="e7d0e-142"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="e7d0e-142"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="e7d0e-143">TwiML 是以 Twilio 動詞為基礎的一組 XML 指令，可指示 Twilio 如何處理來電或簡訊。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-143">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="e7d0e-144">例如，下列 TwiML 會將 **Hello World** 文字轉換成語音。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-144">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="e7d0e-145">當應用程式呼叫 Twilio API 時，其中一個 API 參數是傳回 TwiML 回應的 URL。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-145">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="e7d0e-146">在開發用途上，您可以使用 Twilio 提供的 URL 來提供應用程式所使用的 TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-146">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="e7d0e-147">您也可以裝載您自己的 URL 來產生 TwiML 回應，另一種選擇是使用 `TwiMLResponse` 物件。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-147">You could also host your own URLs to produce the TwiML responses, and another option is to use the `TwiMLResponse` object.</span></span>

<span data-ttu-id="e7d0e-148">如需 Twilio 動詞、屬性和 TwiML 的詳細資訊，請參閱 [TwiML][twiml]。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-148">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="e7d0e-149">如需 Twilio API 的詳細資訊，請參閱 [Twilio API][twilio_api]。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-149">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="e7d0e-150"><a id="CreateAccount"></a>建立 Twilio 帳戶</span><span class="sxs-lookup"><span data-stu-id="e7d0e-150"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="e7d0e-151">準備取得 Twilio 帳戶時，請至[試用 Twilio 註冊][try_twilio]。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-151">When you are ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="e7d0e-152">您可以先使用免費帳戶，稍後再升級帳戶。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-152">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="e7d0e-153">註冊 Twilio 帳戶時，您會收到帳戶 SID 和驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-153">When you sign up for a Twilio account, you receive an account SID and an authentication token.</span></span> <span data-ttu-id="e7d0e-154">兩者皆為呼叫 Twilio API 所需。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-154">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="e7d0e-155">為了防止未經授權存取您的帳戶，您妥善保管驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-155">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="e7d0e-156">在 [Twilio 主控台][twilio_console]標示為 **ACCOUNT SID** 和 **AUTH TOKEN** 的欄位中，分別可檢視您的帳戶 SID 和驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-156">Your account SID and authentication token are viewable in the [Twilio Console][twilio_console], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="e7d0e-157"><a id="create_app"></a>建立 Python 應用程式</span><span class="sxs-lookup"><span data-stu-id="e7d0e-157"><a id="create_app"></a>Create a Python Application</span></span>
<span data-ttu-id="e7d0e-158">使用 Twilio 服務且執行於 Azure 的 Python 應用程式，與其他使用 Twilio 服務的 Python 應用程式並無不同。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-158">A Python application that uses the Twilio service and is running in Azure is no different than any other Python application that uses the Twilio service.</span></span> <span data-ttu-id="e7d0e-159">雖然 Twilio 服務是以 REST 為基礎，並且可透過數種方式從 Python 撥打，但本文的重點是要說明如何搭配使用 Twilio 服務與[適用於 Python 的 Twiliofor 程式庫 (由 GitHub 提供)][twilio_python]。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-159">While Twilio services are REST-based and can be called from Python in several ways, this article will focus on how to use Twilio services with [Twilio library for Python from GitHub][twilio_python].</span></span> <span data-ttu-id="e7d0e-160">若想進一步了解如何使用適用於 Python 的 Twilio 程式庫，請參閱 [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs]。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-160">For more information about using the Twilio library for Python, see [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="e7d0e-161">首先，[set-up a new Azure Linux VM][azure_vm_setup]，以作為新的 Python Web 應用程式主機。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-161">First, [set-up a new Azure Linux VM][azure_vm_setup] to act as a host for your new Python web application.</span></span> <span data-ttu-id="e7d0e-162">當虛擬機器執行時，您必須在公用連接埠上公開應用程式，如下所述。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-162">Once the Virtual Machine is running, you will need to expose your application on a public port as described below.</span></span>

### <a name="add-an-incoming-rule"></a><span data-ttu-id="e7d0e-163">新增傳入規則</span><span class="sxs-lookup"><span data-stu-id="e7d0e-163">Add An Incoming Rule</span></span>
  1. <span data-ttu-id="e7d0e-164">移至 [Network Security Group][azure_nsg] 頁面。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-164">Go to the [Network Security Group][azure_nsg] page.</span></span>
  2. <span data-ttu-id="e7d0e-165">選取與您的虛擬機器對應的網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-165">Select the Network Security Group that corresponds with your Virtual Machine.</span></span>
  3. <span data-ttu-id="e7d0e-166">新增**連接埠 80** 的**傳出規則**。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-166">Add and **Outgoing Rule** for **port 80**.</span></span> <span data-ttu-id="e7d0e-167">務必允許來自任何位址的傳入。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-167">Be sure to allow incoming from any address.</span></span>

### <a name="set-the-dns-name-label"></a><span data-ttu-id="e7d0e-168">設定 DNS 名稱標籤</span><span class="sxs-lookup"><span data-stu-id="e7d0e-168">Set the DNS Name Label</span></span>
  1. <span data-ttu-id="e7d0e-169">移至 [公用 IP 位址] [azure_ips] 頁面。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-169">Go to the [The Public IP Adresses][azure_ips] page.</span></span>
  2. <span data-ttu-id="e7d0e-170">選取與您的虛擬機器對應的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-170">Select the Public IP that correspends with your Virtual Machine.</span></span>
  3. <span data-ttu-id="e7d0e-171">在 [組態] 區段中設定 [DNS 名稱標籤]。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-171">Set the **DNS Name Label** in the **Configuration** section.</span></span> <span data-ttu-id="e7d0e-172">在此範例的情況下，它看起來類似 *your-domain-label*.centralus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="e7d0e-172">In the case of this example it will look something like this *your-domain-label*.centralus.cloudapp.azure.com</span></span>

<span data-ttu-id="e7d0e-173">可透過 SSH 連線到虛擬機器連線之後，就可以安裝您所選擇的 Web 架構 (Python 中最廣為人知的兩個為 [Flask](http://flask.pocoo.org/) 和 [Django](https://www.djangoproject.com))。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-173">Once you are able to connect through SSH to the Virtual Machine you can install the Web Framework of your choice (the two most well known in Python being [Flask](http://flask.pocoo.org/) and [Django](https://www.djangoproject.com)).</span></span> <span data-ttu-id="e7d0e-174">只要執行 `pip install` 命令即可安裝其中一項。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-174">You can install either of them just by running the `pip install` command.</span></span>

<span data-ttu-id="e7d0e-175">請記住，我們已將虛擬機器設定為僅允許連接埠 80 的流量。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-175">Keep in mind that we configured the Virtual Machine to allow traffic only on port 80.</span></span> <span data-ttu-id="e7d0e-176">因此請務必將應用程式設定為使用此連接埠。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-176">So make sure to configure the application to use this port.</span></span>

## <span data-ttu-id="e7d0e-177"><a id="configure_app"></a>設定應用程式以使用 Twilio 程式庫</span><span class="sxs-lookup"><span data-stu-id="e7d0e-177"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="e7d0e-178">您可以透過兩種方式設定應用程式，以使用適用於 Python 的 Twilio 程式庫：</span><span class="sxs-lookup"><span data-stu-id="e7d0e-178">You can configure your application to use the Twilio library for Python in two ways:</span></span>

* <span data-ttu-id="e7d0e-179">以 Pip 封裝的形式，安裝適用於 Python 的 Twilio 程式庫。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-179">Install the Twilio library for Python as a Pip package.</span></span> <span data-ttu-id="e7d0e-180">您可以使用下列命令進行此安裝：</span><span class="sxs-lookup"><span data-stu-id="e7d0e-180">It can be installed with the following commands:</span></span>
   
        $ pip install twilio

    <span data-ttu-id="e7d0e-181">-或-</span><span class="sxs-lookup"><span data-stu-id="e7d0e-181">-OR-</span></span>

* <span data-ttu-id="e7d0e-182">從 GitHub 下載適用於 Python 的 Twilio 程式庫 ([https://github.com/twilio/twilio-python][twilio_python])，並以與此類似的方式安裝它：</span><span class="sxs-lookup"><span data-stu-id="e7d0e-182">Download the Twilio library for Python from GitHub ([https://github.com/twilio/twilio-python][twilio_python]) and install it like this:</span></span>

        $ python setup.py install

<span data-ttu-id="e7d0e-183">安裝了適用於 Python 的 Twilio 程式庫之後，您可以在 Python 檔案中對它進行 `import`︰</span><span class="sxs-lookup"><span data-stu-id="e7d0e-183">Once you have installed the Twilio library for Python, you can then `import` it in your Python files:</span></span>

        import twilio

<span data-ttu-id="e7d0e-184">如需詳細資訊，請參閱 [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme]。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-184">For more information, see [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="e7d0e-185"><a id="howto_make_call"></a>作法：撥出電話</span><span class="sxs-lookup"><span data-stu-id="e7d0e-185"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="e7d0e-186">下列程式碼將說明如何向外撥打電話。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-186">The following shows how to make an outgoing call.</span></span> <span data-ttu-id="e7d0e-187">此程式碼也使用 Twilio 提供的網站來傳回 Twilio 標記語言 (TwiML) 回應。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-187">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="e7d0e-188">請將 **from_number** 和 **to_number** 電話號碼的值換成您的值，並在執行程式碼之前，已驗證 Twilio 帳戶的 **from_number** 電話號碼。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-188">Substitute your values for the **from_number** and **to_number** phone numbers, and ensure that you've verified the **from_number** phone number for your Twilio account before running the code.</span></span>

    from urllib.parse import urlencode

    # Import the Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    # The number of the phone initiating the the call.
    # This should either be a Twilio number or a number that you've verified
    from_number = "NNNNNNNNNNN"

    # The number of the phone receiving call.
    to_number = "NNNNNNNNNNN"

    # Use the Twilio-provided site for the TwiML response.
    url = "http://twimlets.com/message?"

    # The phone message text.
    message = "Hello world."

    # Initialize the Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make the call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url + urlencode({'Message': message}))
    print(call.sid)

<span data-ttu-id="e7d0e-189">如前所述，此程式碼使用 Twilio 提供的網站來傳回 TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-189">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="e7d0e-190">您可以改用自己的網站來提供 TwiML 回應；如需詳細資訊，請參閱 [如何從您自己的網站提供 TwiML 回應](#howto_provide_twiml_responses)。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-190">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="e7d0e-191"><a id="howto_send_sms"></a>作法：傳送簡訊</span><span class="sxs-lookup"><span data-stu-id="e7d0e-191"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="e7d0e-192">以下顯示如何使用 `TwilioRestClient` 類別傳送 SMS 訊息。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-192">The following shows how to send an SMS message using the `TwilioRestClient` class.</span></span> <span data-ttu-id="e7d0e-193">**from_number** 號碼由 Twilio 提供給試用帳戶來傳送簡訊。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-193">The **from_number** number is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="e7d0e-194">執行程式碼之前，必須驗證您 Twilio 帳戶的 **to_number** 號碼。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-194">The **to_number** number must be verified for your Twilio account before running the code.</span></span>

    # Import the Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    from_number = "NNNNNNNNNNN"  # With trial account, texts can only be sent from your Twilio number.
    to_number = "NNNNNNNNNNN"
    message = "Hello world."

    # Initialize the Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Send the SMS message.
    message = client.messages.create(to=to_number,
                                     from_=from_number,
                                     body=message)

## <span data-ttu-id="e7d0e-195"><a id="howto_provide_twiml_responses"></a>作法：從您自己的網站提供 TwiML 回應</span><span class="sxs-lookup"><span data-stu-id="e7d0e-195"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="e7d0e-196">當您的應用程式開始呼叫 Twilio API 時，Twilio 會將要求傳送至 URL，然後應該會傳回 TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-196">When your application initiates a call to the Twilio API, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="e7d0e-197">前述範例使用 Twilio 提供的 URL [http://twimlets.com/message][twimlet_message_url]。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-197">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="e7d0e-198">(雖然 TwiML 是設計給 Twilio 使用的，但您也可以在瀏覽器中檢視 TwiML。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-198">(While TwiML is designed for use by Twilio, you can view it in your browser.</span></span> <span data-ttu-id="e7d0e-199">例如，按一下 [http://twimlets.com/message][twimlet_message_url] 可查看空白的 `<Response>` 元素，又例如，按一下 [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] 可查看包含 `<Say>` 元素的 `<Response>` 元素。)</span><span class="sxs-lookup"><span data-stu-id="e7d0e-199">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] to see a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="e7d0e-200">除了使用 Twilio 提供的 URL 以外，您也可以建立自己的網站來傳回 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-200">Instead of relying on the Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="e7d0e-201">您可以使用任何語言建立會傳回 XML 回應的網站；本主題假設您將使用 Python 建立 TwiML。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-201">You can create the site in any language that returns XML responses; this topic assumes you will be using Python to create the TwiML.</span></span>

<span data-ttu-id="e7d0e-202">下列範例將輸出 TwiML 回應，其會在通話中說出 **Hello World**。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-202">The following examples will output a TwiML response that says **Hello World** on the call.</span></span>

<span data-ttu-id="e7d0e-203">使用 Flask：</span><span class="sxs-lookup"><span data-stu-id="e7d0e-203">With Flask:</span></span>

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

<span data-ttu-id="e7d0e-204">使用 Django：</span><span class="sxs-lookup"><span data-stu-id="e7d0e-204">With Django:</span></span>

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

<span data-ttu-id="e7d0e-205">從以上範例中可知，TwiML 回應只是一份 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-205">As you can see from the example above, the TwiML response is simply an XML document.</span></span> <span data-ttu-id="e7d0e-206">適用於 Python 的 Twilio 程式庫包含可為您產生 TwiML 的類別。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-206">The Twilio library for Python contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="e7d0e-207">下列範例會產生同上的回應，但改用適用於 Python 的 Twilio 程式庫中的 `twiml` 模組：</span><span class="sxs-lookup"><span data-stu-id="e7d0e-207">The example below produces the equivalent response as shown above, but uses the `twiml` module in the Twilio library for Python:</span></span>

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

<span data-ttu-id="e7d0e-208">如需 TwiML 的詳細資訊，請參閱 [https://www.twilio.com/docs/api/twiml][twiml_reference]。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-208">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span>

<span data-ttu-id="e7d0e-209">將 Python 應用程式設定來提供 TwiML 回應之後，請使用應用程式的 URL 作為傳遞到 `client.calls.create` 方法的 URL。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-209">Once you have your Python application set up to provide TwiML responses, use the URL of the application as the URL passed into the `client.calls.create`  method.</span></span> <span data-ttu-id="e7d0e-210">例如，如果您有部署到 Azure 託管服務、名為**MyTwiML** 的 Web 應用程式，您可以使用其 URL 作為 webhook，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="e7d0e-210">For example, if you have a Web application named **MyTwiML** deployed to an Azure hosted service, you can use its url as webhook as shown in the following example:</span></span>

    from twilio.rest import TwilioRestClient

    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"
    from_number = "NNNNNNNNNNN"
    to_number = "NNNNNNNNNNN"
    url = "http://your-domain-label.centralus.cloudapp.azure.com/MyTwiML/"

    # Initialize the Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make the call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url)
    print(call.sid)

## <span data-ttu-id="e7d0e-211"><a id="AdditionalServices"></a>如何：使用其他 Twilio 服務</span><span class="sxs-lookup"><span data-stu-id="e7d0e-211"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="e7d0e-212">除了此處所示的範例以外，Twilio 還提供網頁式 API，方便您從 Azure 應用程式中充份利用其他 Twilio 功能。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-212">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="e7d0e-213">如需完整詳細資料，請參閱 [Twilio API 文件][twilio_api]。</span><span class="sxs-lookup"><span data-stu-id="e7d0e-213">For full details, see the [Twilio API documentation][twilio_api].</span></span>

## <span data-ttu-id="e7d0e-214"><a id="NextSteps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="e7d0e-214"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="e7d0e-215">了解基本的 Twilio 服務之後，請參考下列連結以取得更多資訊：</span><span class="sxs-lookup"><span data-stu-id="e7d0e-215">Now that you have learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="e7d0e-216">[Twilio 安全性方針][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="e7d0e-216">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="e7d0e-217">[Twilio 作法指南與範例程式碼][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="e7d0e-217">[Twilio HowTo Guides and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="e7d0e-218">[Twilio 快速入門教學課程][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="e7d0e-218">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="e7d0e-219">[GitHub 上的 Twilio][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="e7d0e-219">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="e7d0e-220">[洽詢 Twilio 支援][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="e7d0e-220">[Talk to Twilio Support][twilio_support]</span></span>

[special_offer]: http://ahoy.twilio.com/azure
[twilio_python]: https://github.com/twilio/twilio-python
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-python/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-python/blob/master/README.md

[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
