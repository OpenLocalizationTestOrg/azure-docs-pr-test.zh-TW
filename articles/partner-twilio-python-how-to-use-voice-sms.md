---
title: "aaaHow tooUse Twilio 語音和 SMS (Python) |Microsoft 文件"
description: "了解如何 toomake 電話及傳送 SMS 訊息 hello Twilio API 服務在 Azure 上。 程式碼範例以 Python 撰寫。"
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
ms.openlocfilehash: 1f16a107d95c94589b8d61a0971c5b62d639c571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-python"></a><span data-ttu-id="dfa2d-104">如何為語音和簡訊功能以 Python Twilio tooUse</span><span class="sxs-lookup"><span data-stu-id="dfa2d-104">How tooUse Twilio for Voice and SMS Capabilities in Python</span></span>
<span data-ttu-id="dfa2d-105">本指南示範如何 tooperform 常見的程式設計工作以 hello Twilio API 服務在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="dfa2d-106">涵蓋的 hello 案例包括撥電話及傳送短訊息服務 (SMS) 訊息。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="dfa2d-107">如需有關 Twilio 和您的應用程式中使用語音和 SMS 的詳細資訊，請參閱 hello[接下來的步驟](#NextSteps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="dfa2d-108"><a id="WhatIs"></a>什麼是 Twilio？</span><span class="sxs-lookup"><span data-stu-id="dfa2d-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="dfa2d-109">Twilio 是及支援的業務通訊的 hello 未來、 啟用開發人員 tooembed 語音 VoIP 及訊息加入應用程式。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="dfa2d-110">這些虛擬化在雲端為基礎、 全域環境中，公開透過 hello Twilio 通訊 API 平台所需的所有基礎結構。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="dfa2d-111">應用程式是簡單 toobuild 及擴充。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="dfa2d-112">享受隨收隨付定價的彈性和雲端可靠性的好處。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="dfa2d-113">**Twilio 語音**可讓您的應用程式 toomake 撥打與接聽電話。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span>
<span data-ttu-id="dfa2d-114">**Twilio SMS**可讓您的應用程式 toosend 及接收文字訊息。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-114">**Twilio SMS** enables your application toosend and receive text messages.</span></span>
<span data-ttu-id="dfa2d-115">**Twilio 用戶端**可讓您從任何電話、 平板電腦或瀏覽器 toomake VoIP 呼叫，並支援 WebRTC。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="dfa2d-116"><a id="Pricing"></a>Twilio 定價和特別優惠</span><span class="sxs-lookup"><span data-stu-id="dfa2d-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="dfa2d-117">Azure 客戶可在升級 Twilio 帳戶時獲得價值 10 元美金的 Twilio 點數[特殊優惠][special_offer]。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-117">Azure customers receive a [special offer][special_offer] $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="dfa2d-118">此 Twilio 信用額度可以套用的 tooany Twilio 使用量 ($10 信用相等 toosending 多達 1000 SMS 訊息或接收向上 too1000 輸入語音分鐘，視您的電話號碼和訊息或呼叫目的地的 hello 位置而定)。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="dfa2d-119">請兌換此 [Twilio 點數][special_offer]，並開始使用。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-119">Redeem this [Twilio credit][special_offer] and get started.</span></span>

<span data-ttu-id="dfa2d-120">Twilio 是隨收隨付的服務。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="dfa2d-121">不需要設定費，隨時都可結清帳戶。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="dfa2d-122">如需詳細資訊，請參閱 [Twilio 價格][twilio_pricing]。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="dfa2d-123"><a id="Concepts"></a>概念</span><span class="sxs-lookup"><span data-stu-id="dfa2d-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="dfa2d-124">hello Twilio API 是 rest 式 API，應用程式提供語音和 SMS 功能。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="dfa2d-125">用戶端程式庫有多種語言版本，相關清單請參閱 [Twilio API 程式庫][twilio_libraries]。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="dfa2d-126">Hello Twilio API 的重要層面是 Twilio 動詞和 Twilio 標記語言 (TwiML)。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="dfa2d-127"><a id="Verbs"></a>Twilio 動詞</span><span class="sxs-lookup"><span data-stu-id="dfa2d-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="dfa2d-128">hello API 會使用 Twilio 動詞命令。例如，hello **&lt;說&gt;**動詞命令會指示 Twilio tooaudibly 傳遞的訊息上呼叫。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="dfa2d-129">hello 如下的 Twilio 指令動詞的清單。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-129">hello following is a list of Twilio verbs.</span></span> <span data-ttu-id="dfa2d-130">深入了解 hello 其他動詞命令和功能，透過[Twilio 標記語言的文件][twiml]。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation][twiml].</span></span>

* <span data-ttu-id="dfa2d-131">**&lt;撥號&gt;**： 連接 hello 呼叫端 tooanother 電話。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="dfa2d-132">**&lt;收集&gt;**： 會收集輸入 hello 電話字鍵台上的數字。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="dfa2d-133">**&lt;掛斷&gt;**：結束通話。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="dfa2d-134">**&lt;暫停&gt;**：靜候一段指定的秒數。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="dfa2d-135">**&lt;播放&gt;**：播放音訊檔案。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-135">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="dfa2d-136">**&lt;佇列&gt;**： 新增 hello tooa 佇列的呼叫端。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-136">**&lt;Queue&gt;**: Add hello tooa queue of callers.</span></span>
* <span data-ttu-id="dfa2d-137">**&lt;記錄&gt;**： 記錄 hello 呼叫端的 hello 語音，並傳回包含 hello 記錄檔的 URL。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-137">**&lt;Record&gt;**: Records hello voice of hello caller and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="dfa2d-138">**&lt;重新導向&gt;**： 控制權的通話或 SMS toohello TwiML 於不同的 URL。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-138">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="dfa2d-139">**&lt;拒絕&gt;**： 拒絕傳入的呼叫未使用計費您 tooyour Twilio 數目。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-139">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you.</span></span>
* <span data-ttu-id="dfa2d-140">**&lt;說出&gt;**： 將文字 toospeech 所做的呼叫上。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-140">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="dfa2d-141">**&lt;Sms&gt;**：傳送簡訊。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-141">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="dfa2d-142"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="dfa2d-142"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="dfa2d-143">TwiML 是以 XML 為基礎的指示，就會通知方式的 Twilio hello Twilio 動詞命令為基礎的一組 tooprocess 通話或 SMS。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-143">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="dfa2d-144">例如，下列 TwiML hello 將轉換的 hello 文字**Hello World** toospeech。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-144">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="dfa2d-145">當您的應用程式呼叫 hello Twilio 應用程式開發介面時，其中 hello API 參數會是傳回 hello TwiML 回應 hello URL。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-145">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="dfa2d-146">供開發應用程式，您可以使用您的應用程式所使用的 Twilio 提供 Url tooprovide hello TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-146">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="dfa2d-147">您也可以裝載自己 Url tooproduce hello TwiML 回應，和另一個選項是 toouse hello`TwiMLResponse`物件。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-147">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello `TwiMLResponse` object.</span></span>

<span data-ttu-id="dfa2d-148">如需 Twilio 動詞、屬性和 TwiML 的詳細資訊，請參閱 [TwiML][twiml]。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-148">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="dfa2d-149">如需 hello Twilio API 的詳細資訊，請參閱[Twilio API][twilio_api]。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-149">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="dfa2d-150"><a id="CreateAccount"></a>建立 Twilio 帳戶</span><span class="sxs-lookup"><span data-stu-id="dfa2d-150"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="dfa2d-151">當您準備好 tooget Twilio 帳戶，請在註冊[再試一次 Twilio][try_twilio]。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-151">When you are ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="dfa2d-152">您可以先使用免費帳戶，稍後再升級帳戶。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-152">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="dfa2d-153">註冊 Twilio 帳戶時，您會收到帳戶 SID 和驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-153">When you sign up for a Twilio account, you receive an account SID and an authentication token.</span></span> <span data-ttu-id="dfa2d-154">同時會為所需的 toomake Twilio API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-154">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="dfa2d-155">tooprevent 未經授權存取 tooyour 帳戶，讓驗證權杖的安全。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-155">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="dfa2d-156">您的帳戶 SID 與驗證權杖是否可在 hello [Twilio 主控台][twilio_console]，請在 hello 欄位標示為**帳戶 SID**和**驗證語彙基元**分別。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-156">Your account SID and authentication token are viewable in hello [Twilio Console][twilio_console], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="dfa2d-157"><a id="create_app"></a>建立 Python 應用程式</span><span class="sxs-lookup"><span data-stu-id="dfa2d-157"><a id="create_app"></a>Create a Python Application</span></span>
<span data-ttu-id="dfa2d-158">Python 應用程式使用 hello Twilio 服務，且在 Azure 中執行並無不同 hello Twilio 服務會使用任何其他 Python 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-158">A Python application that uses hello Twilio service and is running in Azure is no different than any other Python application that uses hello Twilio service.</span></span> <span data-ttu-id="dfa2d-159">雖然 Twilio 服務是以 REST 為基礎，並可以數種方式呼叫來自 Python，本文將著重在 toouse Twilio 的服務使用[Twilio 程式庫，從 GitHub python][twilio_python]。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-159">While Twilio services are REST-based and can be called from Python in several ways, this article will focus on how toouse Twilio services with [Twilio library for Python from GitHub][twilio_python].</span></span> <span data-ttu-id="dfa2d-160">如需使用 Python hello Twilio 程式庫的詳細資訊，請參閱[http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs]。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-160">For more information about using hello Twilio library for Python, see [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="dfa2d-161">首先，[安裝新的 Azure Linux VM] [azure_vm_setup] tooact 做為新的 Python web 應用程式的主機。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-161">First, [set-up a new Azure Linux VM][azure_vm_setup] tooact as a host for your new Python web application.</span></span> <span data-ttu-id="dfa2d-162">Hello 虛擬機器開始執行之後，您需要 tooexpose 公用連接埠上的應用程式，如下所述。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-162">Once hello Virtual Machine is running, you will need tooexpose your application on a public port as described below.</span></span>

### <a name="add-an-incoming-rule"></a><span data-ttu-id="dfa2d-163">新增傳入規則</span><span class="sxs-lookup"><span data-stu-id="dfa2d-163">Add An Incoming Rule</span></span>
  1. <span data-ttu-id="dfa2d-164">移 toohello [網路安全性群組] [azure_nsg] 頁面。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-164">Go toohello [Network Security Group][azure_nsg] page.</span></span>
  2. <span data-ttu-id="dfa2d-165">選取 hello 網路安全性群組對應與虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-165">Select hello Network Security Group that corresponds with your Virtual Machine.</span></span>
  3. <span data-ttu-id="dfa2d-166">新增**連接埠 80** 的**傳出規則**。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-166">Add and **Outgoing Rule** for **port 80**.</span></span> <span data-ttu-id="dfa2d-167">為確定 tooallow 連入來自任何位址。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-167">Be sure tooallow incoming from any address.</span></span>

### <a name="set-hello-dns-name-label"></a><span data-ttu-id="dfa2d-168">設定 hello DNS 名稱標籤</span><span class="sxs-lookup"><span data-stu-id="dfa2d-168">Set hello DNS Name Label</span></span>
  1. <span data-ttu-id="dfa2d-169">移 toohello [hello 公用 IP 地址] [azure_ips] 頁面。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-169">Go toohello [hello Public IP Adresses][azure_ips] page.</span></span>
  2. <span data-ttu-id="dfa2d-170">選取具有您的虛擬機器的公用 IP 該 correspends hello。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-170">Select hello Public IP that correspends with your Virtual Machine.</span></span>
  3. <span data-ttu-id="dfa2d-171">設定 hello **DNS 名稱標籤**在 hello**組態**> 一節。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-171">Set hello **DNS Name Label** in hello **Configuration** section.</span></span> <span data-ttu-id="dfa2d-172">在此範例中的 hello 情況下它看起來類似下面的*您網域標籤*。 centralus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="dfa2d-172">In hello case of this example it will look something like this *your-domain-label*.centralus.cloudapp.azure.com</span></span>

<span data-ttu-id="dfa2d-173">之後，就可以透過 SSH toohello 虛擬機器，您可以安裝 tooconnect hello 您選擇的 Web 架構 (hello 兩個最知名的 Python[酒瓶](http://flask.pocoo.org/)和[Django](https://www.djangoproject.com))。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-173">Once you are able tooconnect through SSH toohello Virtual Machine you can install hello Web Framework of your choice (hello two most well known in Python being [Flask](http://flask.pocoo.org/) and [Django](https://www.djangoproject.com)).</span></span> <span data-ttu-id="dfa2d-174">您可以只要執行 hello 安裝其中任一`pip install`命令。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-174">You can install either of them just by running hello `pip install` command.</span></span>

<span data-ttu-id="dfa2d-175">請注意，我們只在連接埠 80 上設定 hello 虛擬機器 tooallow 流量。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-175">Keep in mind that we configured hello Virtual Machine tooallow traffic only on port 80.</span></span> <span data-ttu-id="dfa2d-176">因此請確定 tooconfigure hello 應用程式 toouse 此連接埠。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-176">So make sure tooconfigure hello application toouse this port.</span></span>

## <span data-ttu-id="dfa2d-177"><a id="configure_app"></a>設定您的應用程式 tooUse Twilio 文件庫</span><span class="sxs-lookup"><span data-stu-id="dfa2d-177"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="dfa2d-178">您可以設定您應用程式 toouse hello Twilio 程式庫的 Python，有兩種：</span><span class="sxs-lookup"><span data-stu-id="dfa2d-178">You can configure your application toouse hello Twilio library for Python in two ways:</span></span>

* <span data-ttu-id="dfa2d-179">安裝 Python Pip 套件 hello Twilio 程式庫。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-179">Install hello Twilio library for Python as a Pip package.</span></span> <span data-ttu-id="dfa2d-180">它可以安裝以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="dfa2d-180">It can be installed with hello following commands:</span></span>
   
        $ pip install twilio

    <span data-ttu-id="dfa2d-181">-或-</span><span class="sxs-lookup"><span data-stu-id="dfa2d-181">-OR-</span></span>

* <span data-ttu-id="dfa2d-182">從 GitHub 的 python 下載 hello Twilio 程式庫 ([https://github.com/twilio/twilio-python][twilio_python]) 並將它安裝像這樣：</span><span class="sxs-lookup"><span data-stu-id="dfa2d-182">Download hello Twilio library for Python from GitHub ([https://github.com/twilio/twilio-python][twilio_python]) and install it like this:</span></span>

        $ python setup.py install

<span data-ttu-id="dfa2d-183">一旦您的 Python 安裝 hello Twilio 程式庫，您可以再`import`Python 檔案中：</span><span class="sxs-lookup"><span data-stu-id="dfa2d-183">Once you have installed hello Twilio library for Python, you can then `import` it in your Python files:</span></span>

        import twilio

<span data-ttu-id="dfa2d-184">如需詳細資訊，請參閱 [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme]。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-184">For more information, see [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="dfa2d-185"><a id="howto_make_call"></a>作法：撥出電話</span><span class="sxs-lookup"><span data-stu-id="dfa2d-185"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="dfa2d-186">下列的 hello 會示範如何呼叫 toomake 傳出。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-186">hello following shows how toomake an outgoing call.</span></span> <span data-ttu-id="dfa2d-187">此程式碼也會使用 Twilio 提供站台 tooreturn hello Twilio 標記語言 (TwiML) 回應。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-187">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="dfa2d-188">替換為您的值為 hello **from_number**和**to_number**電話號碼，並確定您已驗證過 hello **from_number**電話號碼為您的 Twilio 帳戶之前執行的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-188">Substitute your values for hello **from_number** and **to_number** phone numbers, and ensure that you've verified hello **from_number** phone number for your Twilio account before running hello code.</span></span>

    from urllib.parse import urlencode

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from_number = "NNNNNNNNNNN"

    # hello number of hello phone receiving call.
    to_number = "NNNNNNNNNNN"

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://twimlets.com/message?"

    # hello phone message text.
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url + urlencode({'Message': message}))
    print(call.sid)

<span data-ttu-id="dfa2d-189">如前所述，此程式碼會使用 Twilio 提供站台 tooreturn hello TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-189">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="dfa2d-190">您可以改為使用您自己的站台 tooprovide hello TwiML 回應。如需詳細資訊，請參閱[如何 tooProvide TwiML 回應從您自己網站](#howto_provide_twiml_responses)。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-190">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="dfa2d-191"><a id="howto_send_sms"></a>作法：傳送簡訊</span><span class="sxs-lookup"><span data-stu-id="dfa2d-191"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="dfa2d-192">hello 下列範例示範如何 toosend SMS 訊息使用 hello`TwilioRestClient`類別。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-192">hello following shows how toosend an SMS message using hello `TwilioRestClient` class.</span></span> <span data-ttu-id="dfa2d-193">hello **from_number**數目由 Twilio 為試用版帳戶 toosend SMS 訊息。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-193">hello **from_number** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="dfa2d-194">hello **to_number**數目必須在您的 Twilio 帳戶之前驗證執行 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-194">hello **to_number** number must be verified for your Twilio account before running hello code.</span></span>

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    from_number = "NNNNNNNNNNN"  # With trial account, texts can only be sent from your Twilio number.
    to_number = "NNNNNNNNNNN"
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Send hello SMS message.
    message = client.messages.create(to=to_number,
                                     from_=from_number,
                                     body=message)

## <span data-ttu-id="dfa2d-195"><a id="howto_provide_twiml_responses"></a>作法：從您自己的網站提供 TwiML 回應</span><span class="sxs-lookup"><span data-stu-id="dfa2d-195"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="dfa2d-196">當您的應用程式啟動呼叫 toohello Twilio 應用程式開發介面時，會傳送 Twilio，是您要求 tooa URL 必須是 tooreturn TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-196">When your application initiates a call toohello Twilio API, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="dfa2d-197">上述的 hello 範例會使用 hello Twilio 提供 URL [http://twimlets.com/message][twimlet_message_url]。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-197">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="dfa2d-198">(雖然 TwiML 是設計給 Twilio 使用的，但您也可以在瀏覽器中檢視 TwiML。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-198">(While TwiML is designed for use by Twilio, you can view it in your browser.</span></span> <span data-ttu-id="dfa2d-199">例如，按一下[http://twimlets.com/message] [ twimlet_message_url] toosee 空`<Response>`項目，另一個範例中，按一下 [ [http://twimlets.com/message?訊息 %5B0 %5 D = Hello %20world] [ twimlet_message_url_hello_world] toosee`<Response>`包含項目`<Say>`項目。)</span><span class="sxs-lookup"><span data-stu-id="dfa2d-199">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] toosee a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="dfa2d-200">而不是依賴 hello Twilio 提供 URL，您可以建立您自己會傳回 HTTP 回應的網站。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-200">Instead of relying on hello Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="dfa2d-201">您可以建立 hello 網站中的任何語言，傳回 XML 回應。本主題假設您將使用 Python toocreate hello TwiML。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-201">You can create hello site in any language that returns XML responses; this topic assumes you will be using Python toocreate hello TwiML.</span></span>

<span data-ttu-id="dfa2d-202">hello 下列範例會輸出 TwiML 回應指出**Hello World** hello 呼叫。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-202">hello following examples will output a TwiML response that says **Hello World** on hello call.</span></span>

<span data-ttu-id="dfa2d-203">使用 Flask：</span><span class="sxs-lookup"><span data-stu-id="dfa2d-203">With Flask:</span></span>

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

<span data-ttu-id="dfa2d-204">使用 Django：</span><span class="sxs-lookup"><span data-stu-id="dfa2d-204">With Django:</span></span>

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

<span data-ttu-id="dfa2d-205">您可以看到從 hello 上述範例中，hello TwiML 回應是只是 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-205">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="dfa2d-206">hello Python 的 Twilio 文件庫包含類別，會為您產生 TwiML。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-206">hello Twilio library for Python contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="dfa2d-207">hello 下面範例會產生 hello 相等回應，如上所示，但使用 hello `twiml` hello Python 的 Twilio 文件庫中的模組：</span><span class="sxs-lookup"><span data-stu-id="dfa2d-207">hello example below produces hello equivalent response as shown above, but uses hello `twiml` module in hello Twilio library for Python:</span></span>

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

<span data-ttu-id="dfa2d-208">如需 TwiML 的詳細資訊，請參閱 [https://www.twilio.com/docs/api/twiml][twiml_reference]。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-208">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span>

<span data-ttu-id="dfa2d-209">一旦您設定 tooprovide TwiML 回應的 Python 應用程式，做為 hello hello 應用程式 URL hello URL 傳入 hello`client.calls.create`方法。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-209">Once you have your Python application set up tooprovide TwiML responses, use hello URL of hello application as hello URL passed into hello `client.calls.create`  method.</span></span> <span data-ttu-id="dfa2d-210">例如，如果您有 Web 應用程式名為**MyTwiML**部署的 tooan Azure 託管服務，您可以使用它的 url 為 webhook，hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="dfa2d-210">For example, if you have a Web application named **MyTwiML** deployed tooan Azure hosted service, you can use its url as webhook as shown in hello following example:</span></span>

    from twilio.rest import TwilioRestClient

    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"
    from_number = "NNNNNNNNNNN"
    to_number = "NNNNNNNNNNN"
    url = "http://your-domain-label.centralus.cloudapp.azure.com/MyTwiML/"

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url)
    print(call.sid)

## <span data-ttu-id="dfa2d-211"><a id="AdditionalServices"></a>如何：使用其他 Twilio 服務</span><span class="sxs-lookup"><span data-stu-id="dfa2d-211"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="dfa2d-212">此外 toohello 範例所示，Twilio 提供網頁型應用程式開發介面，您可以使用其他 Twilio 功能 tooleverage 從 Azure 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-212">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="dfa2d-213">完整的詳細資訊，請參閱 hello [Twilio API 文件][twilio_api]。</span><span class="sxs-lookup"><span data-stu-id="dfa2d-213">For full details, see hello [Twilio API documentation][twilio_api].</span></span>

## <span data-ttu-id="dfa2d-214"><a id="NextSteps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="dfa2d-214"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="dfa2d-215">既然您已經學會 hello hello Twilio 服務基本概念，請依照下列多個這些連結 toolearn:</span><span class="sxs-lookup"><span data-stu-id="dfa2d-215">Now that you have learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="dfa2d-216">[Twilio 安全性方針][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="dfa2d-216">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="dfa2d-217">[Twilio 作法指南與範例程式碼][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="dfa2d-217">[Twilio HowTo Guides and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="dfa2d-218">[Twilio 快速入門教學課程][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="dfa2d-218">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="dfa2d-219">[GitHub 上的 Twilio][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="dfa2d-219">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="dfa2d-220">[Talk tooTwilio 支援][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="dfa2d-220">[Talk tooTwilio Support][twilio_support]</span></span>

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
