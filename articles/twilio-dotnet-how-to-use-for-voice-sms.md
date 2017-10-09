---
title: "aaaHow tooUse Twilio 語音和 SMS (.NET) |Microsoft 文件"
description: "了解如何 toomake 電話及傳送 SMS 訊息 hello Twilio API 服務在 Azure 上。 程式碼範例以 .NET 撰寫。"
services: 
documentationcenter: .net
author: devinrader
manager: twilio
editor: 
ms.assetid: 74d4f3c9-f1cb-4968-b744-36b32cd0e834
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/24/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: f568da87ef15e9f540fee9674de31e983d4acb6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-from-azure"></a><span data-ttu-id="6f845-104">如何為語音和簡訊功能，從 Azure toouse Twilio</span><span class="sxs-lookup"><span data-stu-id="6f845-104">How toouse Twilio for voice and SMS capabilities from Azure</span></span>
<span data-ttu-id="6f845-105">本指南示範如何 tooperform 常見的程式設計工作以 hello Twilio API 服務在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="6f845-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="6f845-106">涵蓋的 hello 案例包括撥電話及傳送短訊息服務 (SMS) 訊息。</span><span class="sxs-lookup"><span data-stu-id="6f845-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="6f845-107">如需有關 Twilio 和您的應用程式中使用語音和 SMS 的詳細資訊，請參閱 hello[後續步驟](#NextSteps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="6f845-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next steps](#NextSteps) section.</span></span>

## <span data-ttu-id="6f845-108"><a id="WhatIs"></a>什麼是 Twilio？</span><span class="sxs-lookup"><span data-stu-id="6f845-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="6f845-109">Twilio 是及支援的業務通訊的 hello 未來、 啟用開發人員 tooembed 語音 VoIP 及訊息加入應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f845-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="6f845-110">這些虛擬化在雲端為基礎、 全域環境中，公開透過 hello Twilio 通訊 API 平台所需的所有基礎結構。</span><span class="sxs-lookup"><span data-stu-id="6f845-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="6f845-111">應用程式是簡單 toobuild 及擴充。</span><span class="sxs-lookup"><span data-stu-id="6f845-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="6f845-112">享受隨收隨付定價的彈性和雲端可靠性的好處。</span><span class="sxs-lookup"><span data-stu-id="6f845-112">Enjoy flexibility with pay-as-you-go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="6f845-113">**Twilio 語音**可讓您的應用程式 toomake 撥打與接聽電話。</span><span class="sxs-lookup"><span data-stu-id="6f845-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="6f845-114">**Twilio SMS**可讓您的應用程式 toosend 和接收 SMS 訊息。</span><span class="sxs-lookup"><span data-stu-id="6f845-114">**Twilio SMS** enables your applications toosend and receive SMS messages.</span></span> <span data-ttu-id="6f845-115">**Twilio 用戶端**可讓您從任何電話、 平板電腦或瀏覽器 toomake VoIP 呼叫，並支援 WebRTC。</span><span class="sxs-lookup"><span data-stu-id="6f845-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="6f845-116"><a id="Pricing"></a>Twilio 定價和特別優惠</span><span class="sxs-lookup"><span data-stu-id="6f845-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="6f845-117">升級 Twilio 帳戶的 Azure 客戶，可[特別獲贈](http://www.twilio.com/azure)價值 $10 的 Twilio 點數。</span><span class="sxs-lookup"><span data-stu-id="6f845-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="6f845-118">此 Twilio 信用額度可以套用的 tooany Twilio 使用量 ($10 信用相等 toosending 多達 1000 SMS 訊息或接收向上 too1000 輸入語音分鐘，視您的電話號碼和訊息或呼叫目的地的 hello 位置而定)。</span><span class="sxs-lookup"><span data-stu-id="6f845-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="6f845-119">請至 [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure) 兌換 Twilio 點數來開始使用。</span><span class="sxs-lookup"><span data-stu-id="6f845-119">Redeem this Twilio credit and get started at [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="6f845-120">Twilio 是隨收隨付的服務。</span><span class="sxs-lookup"><span data-stu-id="6f845-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="6f845-121">不需要設定費，隨時都可結清帳戶。</span><span class="sxs-lookup"><span data-stu-id="6f845-121">There are no set-up fees, and you can close your account at any time.</span></span> <span data-ttu-id="6f845-122">如需詳細資訊，請參閱 [Twilio 價格](http://www.twilio.com/voice/pricing)。</span><span class="sxs-lookup"><span data-stu-id="6f845-122">You can find more details at [Twilio Pricing](http://www.twilio.com/voice/pricing).</span></span>

## <span data-ttu-id="6f845-123"><a id="Concepts"></a>概念</span><span class="sxs-lookup"><span data-stu-id="6f845-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="6f845-124">hello Twilio API 是 rest 式 API，應用程式提供語音和 SMS 功能。</span><span class="sxs-lookup"><span data-stu-id="6f845-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="6f845-125">用戶端程式庫有多種語言版本，相關清單請參閱 [Twilio API 程式庫][twilio_libraries]。</span><span class="sxs-lookup"><span data-stu-id="6f845-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="6f845-126">Hello Twilio API 的重要層面是 Twilio 動詞和 Twilio 標記語言 (TwiML)。</span><span class="sxs-lookup"><span data-stu-id="6f845-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="6f845-127"><a id="Verbs"></a>Twilio 動詞</span><span class="sxs-lookup"><span data-stu-id="6f845-127"><a id="Verbs"></a>Twilio verbs</span></span>
<span data-ttu-id="6f845-128">hello API 會使用 Twilio 動詞命令。例如，hello **&lt;說&gt;**動詞命令會指示 Twilio tooaudibly 傳遞的訊息上呼叫。</span><span class="sxs-lookup"><span data-stu-id="6f845-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="6f845-129">hello 如下的 Twilio 指令動詞的清單。</span><span class="sxs-lookup"><span data-stu-id="6f845-129">hello following is a list of Twilio verbs.</span></span>  <span data-ttu-id="6f845-130">深入了解 hello 其他動詞命令和功能，透過[Twilio 標記語言的文件](http://www.twilio.com/docs/api/twiml)。</span><span class="sxs-lookup"><span data-stu-id="6f845-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="6f845-131">**&lt;撥號&gt;**： 連接 hello 呼叫端 tooanother 電話。</span><span class="sxs-lookup"><span data-stu-id="6f845-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="6f845-132">**&lt;收集&gt;**： 會收集輸入 hello 電話字鍵台上的數字。</span><span class="sxs-lookup"><span data-stu-id="6f845-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="6f845-133">**&lt;掛斷&gt;**：結束通話。</span><span class="sxs-lookup"><span data-stu-id="6f845-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="6f845-134">**&lt;播放&gt;**：播放音訊檔案。</span><span class="sxs-lookup"><span data-stu-id="6f845-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="6f845-135">**&lt;暫停&gt;**：靜候一段指定的秒數。</span><span class="sxs-lookup"><span data-stu-id="6f845-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="6f845-136">**&lt;記錄&gt;**： 記錄 hello 呼叫者的語音，並傳回包含 hello 記錄檔的 URL。</span><span class="sxs-lookup"><span data-stu-id="6f845-136">**&lt;Record&gt;**: Records hello caller's voice and returns an URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="6f845-137">**&lt;重新導向&gt;**： 控制權的通話或 SMS toohello TwiML 於不同的 URL。</span><span class="sxs-lookup"><span data-stu-id="6f845-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="6f845-138">**&lt;拒絕&gt;**： 拒絕傳入的呼叫未使用計費您 tooyour Twilio 數目</span><span class="sxs-lookup"><span data-stu-id="6f845-138">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="6f845-139">**&lt;說出&gt;**： 將文字 toospeech 所做的呼叫上。</span><span class="sxs-lookup"><span data-stu-id="6f845-139">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="6f845-140">**&lt;Sms&gt;**：傳送簡訊。</span><span class="sxs-lookup"><span data-stu-id="6f845-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="6f845-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="6f845-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="6f845-142">TwiML 是以 XML 為基礎的指示，就會通知方式的 Twilio hello Twilio 動詞命令為基礎的一組 tooprocess 通話或 SMS。</span><span class="sxs-lookup"><span data-stu-id="6f845-142">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="6f845-143">例如，下列 TwiML hello 將轉換的 hello 文字**Hello World** toospeech。</span><span class="sxs-lookup"><span data-stu-id="6f845-143">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="6f845-144">當您的應用程式呼叫 hello Twilio 應用程式開發介面時，其中 hello API 參數會是傳回 hello TwiML 回應 hello URL。</span><span class="sxs-lookup"><span data-stu-id="6f845-144">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="6f845-145">供開發應用程式，您可以使用您的應用程式所使用的 Twilio 提供 Url tooprovide hello TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="6f845-145">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="6f845-146">您也可以裝載自己 Url tooproduce hello TwiML 回應，和另一個選項是 toouse hello **TwiMLResponse**物件。</span><span class="sxs-lookup"><span data-stu-id="6f845-146">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="6f845-147">如需 Twilio 動詞、屬性和 TwiML 的詳細資訊，請參閱 [TwiML][twiml]。</span><span class="sxs-lookup"><span data-stu-id="6f845-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="6f845-148">如需 hello Twilio API 的詳細資訊，請參閱[Twilio API][twilio_api]。</span><span class="sxs-lookup"><span data-stu-id="6f845-148">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="6f845-149"><a id="CreateAccount"></a>建立 Twilio 帳戶</span><span class="sxs-lookup"><span data-stu-id="6f845-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="6f845-150">當你準備好 tooget Twilio 帳戶時，請在註冊[再試一次 Twilio][try_twilio]。</span><span class="sxs-lookup"><span data-stu-id="6f845-150">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="6f845-151">您可以先使用免費帳戶，稍後再升級帳戶。</span><span class="sxs-lookup"><span data-stu-id="6f845-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="6f845-152">註冊 Twilio 帳戶時，您會收到帳戶識別碼和驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="6f845-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="6f845-153">同時會為所需的 toomake Twilio API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="6f845-153">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="6f845-154">tooprevent 未經授權存取 tooyour 帳戶，讓驗證權杖的安全。</span><span class="sxs-lookup"><span data-stu-id="6f845-154">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="6f845-155">您的帳戶識別碼和驗證權杖皆可檢視在 hello [Twilio 帳戶 頁面上][twilio_account]，請在 hello 欄位標示為**帳戶 SID**和**驗證語彙基元**分別。</span><span class="sxs-lookup"><span data-stu-id="6f845-155">Your account ID and authentication token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="6f845-156"><a id="create_app"></a>建立 Azure 應用程式</span><span class="sxs-lookup"><span data-stu-id="6f845-156"><a id="create_app"></a>Create an Azure Application</span></span>
<span data-ttu-id="6f845-157">裝載已啟用 Twilio 功能之應用程式的 Azure 應用程式，與其他任何 Azure 應用程式並無不同。</span><span class="sxs-lookup"><span data-stu-id="6f845-157">An Azure application that hosts a Twilio enabled application is no different from any other Azure application.</span></span> <span data-ttu-id="6f845-158">您加入 hello Twilio.NET 程式庫，並設定 hello 角色 toouse hello Twilio.NET 程式庫。</span><span class="sxs-lookup"><span data-stu-id="6f845-158">You add hello Twilio .NET library and configure hello role toouse hello Twilio .NET libraries.</span></span>
<span data-ttu-id="6f845-159">如需有關建立初始 Azure 專案的詳細資訊，請參閱[使用 Visual Studio 建立 Azure 專案][vs_project]。</span><span class="sxs-lookup"><span data-stu-id="6f845-159">For information on creating an initial Azure project, see [Creating an Azure project with Visual Studio][vs_project].</span></span>

## <span data-ttu-id="6f845-160"><a id="configure_app"></a>設定您的應用程式 toouse Twilio 文件庫</span><span class="sxs-lookup"><span data-stu-id="6f845-160"><a id="configure_app"></a>Configure Your Application toouse Twilio Libraries</span></span>
<span data-ttu-id="6f845-161">Twilio 提供一組.NET 協助程式程式庫包裝 Twilio tooprovide 簡單且簡單的方式 toointeract hello Twilio REST API 與 Twilio 用戶端的各種層面的 toogenerate TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="6f845-161">Twilio provides a set of .NET helper libraries that wrap various aspects of Twilio tooprovide simple and easy ways toointeract with hello Twilio REST API and Twilio Client toogenerate TwiML responses.</span></span>

<span data-ttu-id="6f845-162">Twilio 為 .NET 開發人員提供五套程式庫：</span><span class="sxs-lookup"><span data-stu-id="6f845-162">Twilio provides five libraries for .NET developers:</span></span>
<span data-ttu-id="6f845-163">程式庫</span><span class="sxs-lookup"><span data-stu-id="6f845-163">Library</span></span>|<span data-ttu-id="6f845-164">說明</span><span class="sxs-lookup"><span data-stu-id="6f845-164">Description</span></span>
---|---
<span data-ttu-id="6f845-165">Twilio.API</span><span class="sxs-lookup"><span data-stu-id="6f845-165">Twilio.API</span></span>|<span data-ttu-id="6f845-166">hello 核心 Twilio 程式庫包裝易記的.NET 程式庫中的 hello Twilio REST API。</span><span class="sxs-lookup"><span data-stu-id="6f845-166">hello core Twilio library that wraps hello Twilio REST API in a friendly .NET library.</span></span> <span data-ttu-id="6f845-167">此程式庫適用於 .NET、Silverlight 和 Windows Phone 7。</span><span class="sxs-lookup"><span data-stu-id="6f845-167">This library is available for .NET, Silverlight, and Windows Phone 7.</span></span>
<span data-ttu-id="6f845-168">Twilio.TwiML</span><span class="sxs-lookup"><span data-stu-id="6f845-168">Twilio.TwiML</span></span>|<span data-ttu-id="6f845-169">提供.NET 易懂的方式 toogenerate TwiML 標記。</span><span class="sxs-lookup"><span data-stu-id="6f845-169">Provides a .NET friendly way toogenerate TwiML markup.</span></span>
<span data-ttu-id="6f845-170">Twilio.MVC</span><span class="sxs-lookup"><span data-stu-id="6f845-170">Twilio.MVC</span></span>|<span data-ttu-id="6f845-171">對於使用 ASP.NET MVC 的開發人員，此程式庫包含 TwilioController、TwiML ActionResult 和要求驗證屬性。</span><span class="sxs-lookup"><span data-stu-id="6f845-171">For developers using ASP.NET MVC, this library includes a TwilioController, TwiML ActionResult, and request validation attribute.</span></span>
<span data-ttu-id="6f845-172">Twilio.WebMatrix</span><span class="sxs-lookup"><span data-stu-id="6f845-172">Twilio.WebMatrix</span></span>|<span data-ttu-id="6f845-173">對於使用 Microsoft 免費 WebMatrix 開發工具的開發人員，此程式庫包含各種 Twilio 動作的 Razor 語法協助程式。</span><span class="sxs-lookup"><span data-stu-id="6f845-173">For developers using Microsoft's free WebMatrix development tool, this library contains Razor syntax helpers for various Twilio actions.</span></span>
<span data-ttu-id="6f845-174">Twilio.Client.Capability</span><span class="sxs-lookup"><span data-stu-id="6f845-174">Twilio.Client.Capability</span></span>|<span data-ttu-id="6f845-175">包含與 hello Twilio 用戶端 JavaScript SDK 搭配使用的 hello 功能權杖產生器。</span><span class="sxs-lookup"><span data-stu-id="6f845-175">Contains hello Capability token generator for use with hello Twilio Client JavaScript SDK.</span></span>

<span data-ttu-id="6f845-176">請注意，所有程式庫都需要有 .NET 3.5、Silverlight 4 或 Windows Phone 7 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6f845-176">Note that all libraries require .NET 3.5, Silverlight 4, or Windows Phone 7 or later.</span></span>

<span data-ttu-id="6f845-177">本指南中提供的 hello 範例使用 hello Twilio.API 程式庫。</span><span class="sxs-lookup"><span data-stu-id="6f845-177">hello samples provided in this guide use hello Twilio.API library.</span></span>

<span data-ttu-id="6f845-178">hello 媒體櫃可以是[使用 hello NuGet 套件管理員擴充功能安裝](http://www.twilio.com/docs/csharp/install)向上 too2015 適用於 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="6f845-178">hello libraries can be [installed using hello NuGet package manager extension](http://www.twilio.com/docs/csharp/install) available for Visual Studio 2010 up too2015.</span></span>  <span data-ttu-id="6f845-179">hello 原始程式碼位於[GitHub][twilio_github_repo]，其中包括 Wiki，其中包含完整的文件以 hello 文件庫。</span><span class="sxs-lookup"><span data-stu-id="6f845-179">hello source code is hosted on [GitHub][twilio_github_repo], which includes a Wiki that contains complete documentation for using hello libraries.</span></span>

<span data-ttu-id="6f845-180">依預設，Microsoft Visual Studio 2010 會安裝 NuGet 1.2 版。</span><span class="sxs-lookup"><span data-stu-id="6f845-180">By default, Microsoft Visual Studio 2010 installs version 1.2 of NuGet.</span></span> <span data-ttu-id="6f845-181">安裝 hello Twilio 程式庫需要 1.6 版或更高版本的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="6f845-181">Installing hello Twilio libraries requires version 1.6 of NuGet or higher.</span></span> <span data-ttu-id="6f845-182">如需有關安裝或更新 NuGet 的詳細資訊，請參閱 [http://nuget.org/][nuget]。</span><span class="sxs-lookup"><span data-stu-id="6f845-182">For information on installing or updating NuGet, see [http://nuget.org/][nuget].</span></span>

> [!NOTE]
> <span data-ttu-id="6f845-183">tooinstall hello 最新的 NuGet 版本，您必須先解除安裝使用 Visual Studio 擴充功能管理員 hello hello 載入的版本。</span><span class="sxs-lookup"><span data-stu-id="6f845-183">tooinstall hello latest version of NuGet, you must first uninstall hello loaded version using hello Visual Studio Extension Manager.</span></span> <span data-ttu-id="6f845-184">toodo 因此，您必須以系統管理員身分執行 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="6f845-184">toodo so, you must run Visual Studio as administrator.</span></span> <span data-ttu-id="6f845-185">否則，會停用 hello 解除安裝 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6f845-185">Otherwise, hello Uninstall button is disabled.</span></span>
>
>

### <span data-ttu-id="6f845-186"><a id="use_nuget"></a>tooadd hello Twilio 文件庫 tooyour Visual Studio 專案：</span><span class="sxs-lookup"><span data-stu-id="6f845-186"><a id="use_nuget"></a>tooadd hello Twilio libraries tooyour Visual Studio project:</span></span>
1. <span data-ttu-id="6f845-187">在 Visual Studio 中開啟方案。</span><span class="sxs-lookup"><span data-stu-id="6f845-187">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="6f845-188">以滑鼠右鍵按一下 [參考]。</span><span class="sxs-lookup"><span data-stu-id="6f845-188">Right-click **References**.</span></span>
3. <span data-ttu-id="6f845-189">按一下 [管理 NuGet 套件...]</span><span class="sxs-lookup"><span data-stu-id="6f845-189">Click **Manage NuGet Packages...**</span></span>
4. <span data-ttu-id="6f845-190">按一下 [線上] 。</span><span class="sxs-lookup"><span data-stu-id="6f845-190">Click **Online**.</span></span>
5. <span data-ttu-id="6f845-191">在 hello 搜尋線上方塊中，輸入*twilio*。</span><span class="sxs-lookup"><span data-stu-id="6f845-191">In hello search online box, type *twilio*.</span></span>
6. <span data-ttu-id="6f845-192">按一下**安裝**hello Twilio 封裝上。</span><span class="sxs-lookup"><span data-stu-id="6f845-192">Click **Install** on hello Twilio package.</span></span>

## <span data-ttu-id="6f845-193"><a id="howto_make_call"></a>作法：撥出電話</span><span class="sxs-lookup"><span data-stu-id="6f845-193"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="6f845-194">hello 下列範例示範如何 toomake 傳出呼叫使用 hello **CallResource**類別。</span><span class="sxs-lookup"><span data-stu-id="6f845-194">hello following shows how toomake an outgoing call using hello **CallResource** class.</span></span> <span data-ttu-id="6f845-195">此程式碼也會使用 Twilio 提供站台 tooreturn hello Twilio 標記語言 (TwiML) 回應。</span><span class="sxs-lookup"><span data-stu-id="6f845-195">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="6f845-196">替換為您的值為 hello**至**和**從**電話號碼，並確保您確認 hello**從**執行 hello 程式碼前電話 Twilio 帳戶的號碼。</span><span class="sxs-lookup"><span data-stu-id="6f845-196">Substitute your values for hello **to** and **from** phone numbers, and ensure that you verify hello **from** phone number for your Twilio account before running hello code.</span></span>

    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize hello TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    var url = "http://twimlets.com/message";
    url = $"{url}?Message%5B0%5D=Hello%20World";

    // Set hello call From, To, and URL values toouse for hello call.
    // This sample uses hello sandbox number provided by
    // Twilio toomake hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri(url));
        }

<span data-ttu-id="6f845-197">如需有關 hello 參數傳入 toohello **CallResource.Create**方法，請參閱[http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls]。</span><span class="sxs-lookup"><span data-stu-id="6f845-197">For more information about hello parameters passed in toohello **CallResource.Create** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="6f845-198">如前所述，此程式碼會使用 Twilio 提供站台 tooreturn hello TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="6f845-198">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="6f845-199">您可以改為使用您自己的站台 tooprovide hello TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="6f845-199">You could instead use your own site tooprovide hello TwiML response.</span></span> <span data-ttu-id="6f845-200">如需詳細資訊，請參閱[如何：從您自己的網站提供 TwiML 回應](#howto_provide_twiml_responses)。</span><span class="sxs-lookup"><span data-stu-id="6f845-200">For more information, see [How to: Provide TwiML responses from your own website](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="6f845-201"><a id="howto_send_sms"></a>作法：傳送簡訊</span><span class="sxs-lookup"><span data-stu-id="6f845-201"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="6f845-202">hello 下列螢幕擷取畫面顯示如何 toosend SMS 訊息使用 hello **MessageResource**類別。</span><span class="sxs-lookup"><span data-stu-id="6f845-202">hello following screenshot shows how toosend an SMS message using hello **MessageResource**  class.</span></span> <span data-ttu-id="6f845-203">hello**從**數目由 Twilio 為試用版帳戶 toosend SMS 訊息。</span><span class="sxs-lookup"><span data-stu-id="6f845-203">hello **from** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="6f845-204">hello**至**數目必須驗證您 Twilio 帳戶的執行 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="6f845-204">hello **to** number must be verified for your Twilio account before you run hello code.</span></span>

    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize hello TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    try
    {
        // Send an SMS message.
        var message = MessageResource.Create(
            to: new PhoneNumber("+12069419717"),
            from: new PhoneNumber("+14155992671"),
            body: "This is my SMS message.");
    }
    catch (TwilioException ex)
    {
        // An exception occurred making hello REST call
        Console.WriteLine(ex.Message);
    }

## <span data-ttu-id="6f845-205"><a id="howto_provide_twiml_responses"></a>作法：從您自己的網站提供 TwiML 回應</span><span class="sxs-lookup"><span data-stu-id="6f845-205"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own website</span></span>
<span data-ttu-id="6f845-206">當您的應用程式起始呼叫 toohello Twilio API-例如，透過 hello **CallResource.Create**方法-Twilio 傳送您的要求 tooan URL 所預期的 tooreturn TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="6f845-206">When your application initiates a call toohello Twilio API - for example, via hello **CallResource.Create** method - Twilio sends your request tooan URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="6f845-207">中的 hello 範例[如何： 進行傳出呼叫](#howto_make_call)使用 hello Twilio 提供 URL [http://twimlets.com/message] [ twimlet_message_url] tooreturn hello 回應。</span><span class="sxs-lookup"><span data-stu-id="6f845-207">hello example in [How to: Make an outgoing call](#howto_make_call) uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url] tooreturn hello response.</span></span>

> [!NOTE]
> <span data-ttu-id="6f845-208">雖然 TwiML 設計為使用 web 服務，您可以檢視 hello TwiML 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="6f845-208">While TwiML is designed for use by web services, you can view hello TwiML in your browser.</span></span> <span data-ttu-id="6f845-209">例如，按一下[http://twimlets.com/message] [ twimlet_message_url] toosee 空&lt;回應&gt;項目，另一個範例中，按一下 [ [http://twimlets.com/message?訊息 %5B0 %5 D = Hello %20world](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee&lt;回應&gt;包含項目&lt;說&gt;項目。</span><span class="sxs-lookup"><span data-stu-id="6f845-209">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty &lt;Response&gt; element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee a &lt;Response&gt; element that contains a &lt;Say&gt; element.</span></span>
>
>

<span data-ttu-id="6f845-210">而不是依賴 hello Twilio 提供 URL，您可以建立您自己會傳回 HTTP 回應的 URL 站台。</span><span class="sxs-lookup"><span data-stu-id="6f845-210">Instead of relying on hello Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="6f845-211">您可以建立 hello 站台會傳回 HTTP 回應的任何語言。</span><span class="sxs-lookup"><span data-stu-id="6f845-211">You can create hello site in any language that returns HTTP responses.</span></span> <span data-ttu-id="6f845-212">本主題假設您要主控 hello 從 ASP.NET 泛型處理常式的 URL。</span><span class="sxs-lookup"><span data-stu-id="6f845-212">This topic assumes you'll be hosting hello URL from an ASP.NET generic handler.</span></span>

<span data-ttu-id="6f845-213">下列 ASP.NET 處理常式的 hello 花瓶 TwiML 回應指出**Hello World** hello 呼叫。</span><span class="sxs-lookup"><span data-stu-id="6f845-213">hello following ASP.NET Handler crafts a TwiML response that says **Hello World** on hello call.</span></span>

    using System.Text;
    using System.Web;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {
            public void ProcessRequest(HttpContext context)
            {
                const string twiMLResponse =
                    "<Response><Say>Hello World.</Say></Response>";
                
                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.ContentEncoding = Encoding.UTF8;
                context.Response.Write(twiMLResponse);
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }
    
<span data-ttu-id="6f845-214">您可以看到從 hello 上述範例中，hello TwiML 回應是只是 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="6f845-214">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="6f845-215">hello Twilio.TwiML 程式庫包含類別，會為您產生 TwiML。</span><span class="sxs-lookup"><span data-stu-id="6f845-215">hello Twilio.TwiML library contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="6f845-216">hello 下面範例會產生 hello 相等回應，如上所示，但使用 hello **VoiceResponse**類別。</span><span class="sxs-lookup"><span data-stu-id="6f845-216">hello example below produces hello equivalent response as shown above, but uses hello **VoiceResponse** class.</span></span>

    using System.Web;
    using Twilio.TwiML;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {

            public void ProcessRequest(HttpContext context)
            {
                var twiml = new VoiceResponse();
                twiml.Say("Hello World.");

                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.Write(twiml.ToString());
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }

<span data-ttu-id="6f845-217">如需 TwiML 的詳細資訊，請參閱 [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml)。</span><span class="sxs-lookup"><span data-stu-id="6f845-217">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span></span>

<span data-ttu-id="6f845-218">一旦您已設定的方式 tooprovide TwiML 回應，您可以傳遞該 URL toohello **CallResource.Create**方法。</span><span class="sxs-lookup"><span data-stu-id="6f845-218">Once you have set up a way tooprovide TwiML responses, you can pass that URL toohello **CallResource.Create** method.</span></span> <span data-ttu-id="6f845-219">例如，如果您為部署 MyTwiML tooan Azure 雲端服務的 web 應用程式，而且 hello ASP.NET 處理常式名稱是 mytwiml.ashx，hello URL 可以傳遞太**CallResource.Create** hello 下列程式碼所示範例：</span><span class="sxs-lookup"><span data-stu-id="6f845-219">For example, if you have a web application named MyTwiML deployed tooan Azure cloud service, and hello name of your ASP.NET Handler is mytwiml.ashx, hello URL can be passed too**CallResource.Create** as shown in hello following code sample:</span></span>

    // This sample uses hello sandbox number provided by Twilio toomake hello call.
    // Place hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

<span data-ttu-id="6f845-220">如需有關使用 ASP.NET 在 Azure 上使用 Twilio 的詳細資訊，請參閱[如何 toomake 電話呼叫在 Azure 上的 web 角色中使用 Twilio][howto_phonecall_dotnet]。</span><span class="sxs-lookup"><span data-stu-id="6f845-220">For additional information about using Twilio on Azure with ASP.NET, see [How toomake a phone call using Twilio in a web role on Azure][howto_phonecall_dotnet].</span></span>

[!INCLUDE [twilio-additional-services-and-next-steps](../includes/twilio-additional-services-and-next-steps.md)]

[howto_phonecall_dotnet]: partner-twilio-cloud-services-dotnet-phone-call-web-role.md

[twimlet_message_url]: http://twimlets.com/message

[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls

[vs_project]:http://msdn.microsoft.com/library/windowsazure/ee405487.aspx
[nuget]:http://nuget.org/
[twilio_github_repo]:https://github.com/twilio/twilio-csharp

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
