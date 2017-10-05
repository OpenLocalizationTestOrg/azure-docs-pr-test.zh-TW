---
title: "如何使用 Twilio 來進行語音交談和傳送簡訊 (.NET) | Microsoft Docs"
description: "了解如何在 Azure 上使用 Twilio API 服務撥打電話及傳送簡訊。 程式碼範例以 .NET 撰寫。"
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
ms.openlocfilehash: 1442e3af26ae87e645cf207228ed1197b2afdd4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-from-azure"></a><span data-ttu-id="3afd8-104">如何透過 Twilio 來使用 Azure 的語音和簡訊功能</span><span class="sxs-lookup"><span data-stu-id="3afd8-104">How to use Twilio for voice and SMS capabilities from Azure</span></span>
<span data-ttu-id="3afd8-105">本指南示範如何在 Azure 上透過 Twilio API 服務執行常見的程式設計工作。</span><span class="sxs-lookup"><span data-stu-id="3afd8-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="3afd8-106">涵蓋的案例包括打電話和傳送簡訊 (SMS)。</span><span class="sxs-lookup"><span data-stu-id="3afd8-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="3afd8-107">如需有關如何在應用程式中使用 Twilio 語音和 SMS 的詳細資訊，請參閱[後續步驟](#NextSteps)一節。</span><span class="sxs-lookup"><span data-stu-id="3afd8-107">For more information on Twilio and using voice and SMS in your applications, see the [Next steps](#NextSteps) section.</span></span>

## <span data-ttu-id="3afd8-108"><a id="WhatIs"></a>什麼是 Twilio？</span><span class="sxs-lookup"><span data-stu-id="3afd8-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="3afd8-109">Twilio 正在形塑商業環境的未來，可讓開發人員將語音、VoIP 和訊息傳送內嵌到應用程式中。</span><span class="sxs-lookup"><span data-stu-id="3afd8-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="3afd8-110">它們將雲端、全球化環境中所需的整個基礎結構虛擬化，透過 Twilio 通訊 API 平台來揭露基礎結構。</span><span class="sxs-lookup"><span data-stu-id="3afd8-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span></span> <span data-ttu-id="3afd8-111">輕鬆就可建立和擴充應用程式。</span><span class="sxs-lookup"><span data-stu-id="3afd8-111">Applications are simple to build and scalable.</span></span> <span data-ttu-id="3afd8-112">享受隨收隨付定價的彈性和雲端可靠性的好處。</span><span class="sxs-lookup"><span data-stu-id="3afd8-112">Enjoy flexibility with pay-as-you-go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="3afd8-113">**Twilio 語音** 可讓應用程式撥打和接聽電話。</span><span class="sxs-lookup"><span data-stu-id="3afd8-113">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="3afd8-114">**Twilio 簡訊**可讓應用程式收發簡訊。</span><span class="sxs-lookup"><span data-stu-id="3afd8-114">**Twilio SMS** enables your applications to send and receive SMS messages.</span></span> <span data-ttu-id="3afd8-115">**Twilio 用戶端**可讓您從任何電話、平板電腦或瀏覽器撥打 VoIP 電話，且支援 WebRTC。</span><span class="sxs-lookup"><span data-stu-id="3afd8-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="3afd8-116"><a id="Pricing"></a>Twilio 定價和特別優惠</span><span class="sxs-lookup"><span data-stu-id="3afd8-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="3afd8-117">升級 Twilio 帳戶的 Azure 客戶，可[特別獲贈](http://www.twilio.com/azure)價值 $10 的 Twilio 點數。</span><span class="sxs-lookup"><span data-stu-id="3afd8-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="3afd8-118">此 Twilio 點數可用來折抵任何 Twilio 使用量 ($10 點數相當於最多傳送 1,000 則簡訊，或最多接收 1000 分鐘的撥入語音，視電話號碼所在地點或通話目的地而定)。</span><span class="sxs-lookup"><span data-stu-id="3afd8-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span></span> <span data-ttu-id="3afd8-119">請至 [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure) 兌換 Twilio 點數來開始使用。</span><span class="sxs-lookup"><span data-stu-id="3afd8-119">Redeem this Twilio credit and get started at [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="3afd8-120">Twilio 是隨收隨付的服務。</span><span class="sxs-lookup"><span data-stu-id="3afd8-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="3afd8-121">不需要設定費，隨時都可結清帳戶。</span><span class="sxs-lookup"><span data-stu-id="3afd8-121">There are no set-up fees, and you can close your account at any time.</span></span> <span data-ttu-id="3afd8-122">如需詳細資訊，請參閱 [Twilio 價格](http://www.twilio.com/voice/pricing)。</span><span class="sxs-lookup"><span data-stu-id="3afd8-122">You can find more details at [Twilio Pricing](http://www.twilio.com/voice/pricing).</span></span>

## <span data-ttu-id="3afd8-123"><a id="Concepts"></a>概念</span><span class="sxs-lookup"><span data-stu-id="3afd8-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="3afd8-124">Twilio API 是一套為應用程式提供語音和簡訊功能的 RESTful API。</span><span class="sxs-lookup"><span data-stu-id="3afd8-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="3afd8-125">用戶端程式庫有多種語言版本，相關清單請參閱 [Twilio API 程式庫][twilio_libraries]。</span><span class="sxs-lookup"><span data-stu-id="3afd8-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="3afd8-126">Twilio API 的兩大重點是 Twilio 動詞和 Twilio 標記語言 (TwiML)。</span><span class="sxs-lookup"><span data-stu-id="3afd8-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="3afd8-127"><a id="Verbs"></a>Twilio 動詞</span><span class="sxs-lookup"><span data-stu-id="3afd8-127"><a id="Verbs"></a>Twilio verbs</span></span>
<span data-ttu-id="3afd8-128">API 採用 Twilio 動詞。例如，**&lt;Say&gt;** 動詞指示 Twilio 在通話中用語音傳遞訊息。</span><span class="sxs-lookup"><span data-stu-id="3afd8-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="3afd8-129">以下是 Twilio 動詞清單。</span><span class="sxs-lookup"><span data-stu-id="3afd8-129">The following is a list of Twilio verbs.</span></span>  <span data-ttu-id="3afd8-130">如需了解其他動詞和功能，請參閱 [Twilio 標記語言文件](http://www.twilio.com/docs/api/twiml)。</span><span class="sxs-lookup"><span data-stu-id="3afd8-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="3afd8-131">**&lt;撥號&gt;**：使撥號者接通另一支電話。</span><span class="sxs-lookup"><span data-stu-id="3afd8-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="3afd8-132">**&lt;收集&gt;**：收集電話按鍵上輸入的號碼。</span><span class="sxs-lookup"><span data-stu-id="3afd8-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="3afd8-133">**&lt;掛斷&gt;**：結束通話。</span><span class="sxs-lookup"><span data-stu-id="3afd8-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="3afd8-134">**&lt;播放&gt;**：播放音訊檔案。</span><span class="sxs-lookup"><span data-stu-id="3afd8-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="3afd8-135">**&lt;暫停&gt;**：靜候一段指定的秒數。</span><span class="sxs-lookup"><span data-stu-id="3afd8-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="3afd8-136">**&lt;記錄&gt;**：錄製來電者的語音並傳回含有錄音的檔案 URL。</span><span class="sxs-lookup"><span data-stu-id="3afd8-136">**&lt;Record&gt;**: Records the caller's voice and returns an URL of a file that contains the recording.</span></span>
* <span data-ttu-id="3afd8-137">**&lt;重新導向&gt;**：將通話或簡訊的控制權移轉至不同 URL 的 TwiML。</span><span class="sxs-lookup"><span data-stu-id="3afd8-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="3afd8-138">**&lt;拒絕&gt;**：拒絕 Twilio 號碼的來電而不計費</span><span class="sxs-lookup"><span data-stu-id="3afd8-138">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="3afd8-139">**&lt;說出&gt;**：將來電的文字轉換成語音。</span><span class="sxs-lookup"><span data-stu-id="3afd8-139">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="3afd8-140">**&lt;Sms&gt;**：傳送簡訊。</span><span class="sxs-lookup"><span data-stu-id="3afd8-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="3afd8-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="3afd8-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="3afd8-142">TwiML 是以 Twilio 動詞為基礎的一組 XML 指令，可指示 Twilio 如何處理來電或簡訊。</span><span class="sxs-lookup"><span data-stu-id="3afd8-142">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="3afd8-143">例如，下列 TwiML 會將 **Hello World** 文字轉換成語音。</span><span class="sxs-lookup"><span data-stu-id="3afd8-143">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="3afd8-144">當應用程式呼叫 Twilio API 時，其中一個 API 參數是傳回 TwiML 回應的 URL。</span><span class="sxs-lookup"><span data-stu-id="3afd8-144">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="3afd8-145">在開發用途上，您可以使用 Twilio 提供的 URL 來提供應用程式所使用的 TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="3afd8-145">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="3afd8-146">您也可以裝載您自己的 URL 來產生 TwiML 回應，另一種選擇是使用 **TwiMLResponse** 物件。</span><span class="sxs-lookup"><span data-stu-id="3afd8-146">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="3afd8-147">如需 Twilio 動詞、屬性和 TwiML 的詳細資訊，請參閱 [TwiML][twiml]。</span><span class="sxs-lookup"><span data-stu-id="3afd8-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="3afd8-148">如需 Twilio API 的詳細資訊，請參閱 [Twilio API][twilio_api]。</span><span class="sxs-lookup"><span data-stu-id="3afd8-148">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="3afd8-149"><a id="CreateAccount"></a>建立 Twilio 帳戶</span><span class="sxs-lookup"><span data-stu-id="3afd8-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="3afd8-150">準備取得 Twilio 帳戶時，請至[試用 Twilio][try_twilio] 註冊。</span><span class="sxs-lookup"><span data-stu-id="3afd8-150">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="3afd8-151">您可以先使用免費帳戶，稍後再升級帳戶。</span><span class="sxs-lookup"><span data-stu-id="3afd8-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="3afd8-152">註冊 Twilio 帳戶時，您會收到帳戶識別碼和驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="3afd8-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="3afd8-153">兩者皆為呼叫 Twilio API 所需。</span><span class="sxs-lookup"><span data-stu-id="3afd8-153">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="3afd8-154">為了防止未經授權存取您的帳戶，您妥善保管驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="3afd8-154">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="3afd8-155">在 [Twilio 帳戶頁面][twilio_account] 的 **ACCOUNT SID** 和 **AUTH TOKEN** 欄位中，分別可檢視您的帳戶識別碼和驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="3afd8-155">Your account ID and authentication token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="3afd8-156"><a id="create_app"></a>建立 Azure 應用程式</span><span class="sxs-lookup"><span data-stu-id="3afd8-156"><a id="create_app"></a>Create an Azure Application</span></span>
<span data-ttu-id="3afd8-157">裝載已啟用 Twilio 功能之應用程式的 Azure 應用程式，與其他任何 Azure 應用程式並無不同。</span><span class="sxs-lookup"><span data-stu-id="3afd8-157">An Azure application that hosts a Twilio enabled application is no different from any other Azure application.</span></span> <span data-ttu-id="3afd8-158">您可以新增 Twilio .NET 程式庫並設定角色使用 Twilio .NET 程式庫。</span><span class="sxs-lookup"><span data-stu-id="3afd8-158">You add the Twilio .NET library and configure the role to use the Twilio .NET libraries.</span></span>
<span data-ttu-id="3afd8-159">如需有關建立初始 Azure 專案的詳細資訊，請參閱[使用 Visual Studio 建立 Azure 專案][vs_project]。</span><span class="sxs-lookup"><span data-stu-id="3afd8-159">For information on creating an initial Azure project, see [Creating an Azure project with Visual Studio][vs_project].</span></span>

## <span data-ttu-id="3afd8-160"><a id="configure_app"></a>設定應用程式使用 Twilio 程式庫</span><span class="sxs-lookup"><span data-stu-id="3afd8-160"><a id="configure_app"></a>Configure Your Application to use Twilio Libraries</span></span>
<span data-ttu-id="3afd8-161">Twilio 提供一套 .NET 協助程式庫，內已封裝 Twilio 的各種組件，讓您簡單又輕鬆地與 Twilio REST API 和 Twilio 用戶端互動，以產生 TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="3afd8-161">Twilio provides a set of .NET helper libraries that wrap various aspects of Twilio to provide simple and easy ways to interact with the Twilio REST API and Twilio Client to generate TwiML responses.</span></span>

<span data-ttu-id="3afd8-162">Twilio 為 .NET 開發人員提供五套程式庫：</span><span class="sxs-lookup"><span data-stu-id="3afd8-162">Twilio provides five libraries for .NET developers:</span></span>
<span data-ttu-id="3afd8-163">程式庫</span><span class="sxs-lookup"><span data-stu-id="3afd8-163">Library</span></span>|<span data-ttu-id="3afd8-164">說明</span><span class="sxs-lookup"><span data-stu-id="3afd8-164">Description</span></span>
---|---
<span data-ttu-id="3afd8-165">Twilio.API</span><span class="sxs-lookup"><span data-stu-id="3afd8-165">Twilio.API</span></span>|<span data-ttu-id="3afd8-166">核心 Twilio 程式庫將 Twilio REST API 包裝在一個好用的 .NET 程式庫中。</span><span class="sxs-lookup"><span data-stu-id="3afd8-166">The core Twilio library that wraps the Twilio REST API in a friendly .NET library.</span></span> <span data-ttu-id="3afd8-167">此程式庫適用於 .NET、Silverlight 和 Windows Phone 7。</span><span class="sxs-lookup"><span data-stu-id="3afd8-167">This library is available for .NET, Silverlight, and Windows Phone 7.</span></span>
<span data-ttu-id="3afd8-168">Twilio.TwiML</span><span class="sxs-lookup"><span data-stu-id="3afd8-168">Twilio.TwiML</span></span>|<span data-ttu-id="3afd8-169">輕鬆利用 .NET 來產生 TwiML 標記。</span><span class="sxs-lookup"><span data-stu-id="3afd8-169">Provides a .NET friendly way to generate TwiML markup.</span></span>
<span data-ttu-id="3afd8-170">Twilio.MVC</span><span class="sxs-lookup"><span data-stu-id="3afd8-170">Twilio.MVC</span></span>|<span data-ttu-id="3afd8-171">對於使用 ASP.NET MVC 的開發人員，此程式庫包含 TwilioController、TwiML ActionResult 和要求驗證屬性。</span><span class="sxs-lookup"><span data-stu-id="3afd8-171">For developers using ASP.NET MVC, this library includes a TwilioController, TwiML ActionResult, and request validation attribute.</span></span>
<span data-ttu-id="3afd8-172">Twilio.WebMatrix</span><span class="sxs-lookup"><span data-stu-id="3afd8-172">Twilio.WebMatrix</span></span>|<span data-ttu-id="3afd8-173">對於使用 Microsoft 免費 WebMatrix 開發工具的開發人員，此程式庫包含各種 Twilio 動作的 Razor 語法協助程式。</span><span class="sxs-lookup"><span data-stu-id="3afd8-173">For developers using Microsoft's free WebMatrix development tool, this library contains Razor syntax helpers for various Twilio actions.</span></span>
<span data-ttu-id="3afd8-174">Twilio.Client.Capability</span><span class="sxs-lookup"><span data-stu-id="3afd8-174">Twilio.Client.Capability</span></span>|<span data-ttu-id="3afd8-175">包含適用於 Twilio 用戶端 JavaScript SDK 的功能權杖產生器。</span><span class="sxs-lookup"><span data-stu-id="3afd8-175">Contains the Capability token generator for use with the Twilio Client JavaScript SDK.</span></span>

<span data-ttu-id="3afd8-176">請注意，所有程式庫都需要有 .NET 3.5、Silverlight 4 或 Windows Phone 7 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="3afd8-176">Note that all libraries require .NET 3.5, Silverlight 4, or Windows Phone 7 or later.</span></span>

<span data-ttu-id="3afd8-177">本指南提供的範例使用 Twilio.API 程式庫。</span><span class="sxs-lookup"><span data-stu-id="3afd8-177">The samples provided in this guide use the Twilio.API library.</span></span>

<span data-ttu-id="3afd8-178">程式庫可以[使用 NuGet 套件管理員延伸模組安裝](http://www.twilio.com/docs/csharp/install) (適用於 Visual Studio 2010 到 2015)。</span><span class="sxs-lookup"><span data-stu-id="3afd8-178">The libraries can be [installed using the NuGet package manager extension](http://www.twilio.com/docs/csharp/install) available for Visual Studio 2010 up to 2015.</span></span>  <span data-ttu-id="3afd8-179">原始程式碼可裝載於 [GitHub][twilio_github_repo]，它包含一個 Wiki，提供完整的程式庫使用說明文件。</span><span class="sxs-lookup"><span data-stu-id="3afd8-179">The source code is hosted on [GitHub][twilio_github_repo], which includes a Wiki that contains complete documentation for using the libraries.</span></span>

<span data-ttu-id="3afd8-180">依預設，Microsoft Visual Studio 2010 會安裝 NuGet 1.2 版。</span><span class="sxs-lookup"><span data-stu-id="3afd8-180">By default, Microsoft Visual Studio 2010 installs version 1.2 of NuGet.</span></span> <span data-ttu-id="3afd8-181">安裝 Twilio 程式庫需要有 NuGet 1.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="3afd8-181">Installing the Twilio libraries requires version 1.6 of NuGet or higher.</span></span> <span data-ttu-id="3afd8-182">如需有關安裝或更新 NuGet 的詳細資訊，請參閱 [http://nuget.org/][nuget]。</span><span class="sxs-lookup"><span data-stu-id="3afd8-182">For information on installing or updating NuGet, see [http://nuget.org/][nuget].</span></span>

> [!NOTE]
> <span data-ttu-id="3afd8-183">若要安裝最新版的 NuGet，您必須先使用 Visual Studio 擴充功能管理員來解除安裝已載入的版本。</span><span class="sxs-lookup"><span data-stu-id="3afd8-183">To install the latest version of NuGet, you must first uninstall the loaded version using the Visual Studio Extension Manager.</span></span> <span data-ttu-id="3afd8-184">若要這麼做，您必須以系統管理員身分執行 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="3afd8-184">To do so, you must run Visual Studio as administrator.</span></span> <span data-ttu-id="3afd8-185">否則，[解除安裝] 按鈕會停用。</span><span class="sxs-lookup"><span data-stu-id="3afd8-185">Otherwise, the Uninstall button is disabled.</span></span>
>
>

### <span data-ttu-id="3afd8-186"><a id="use_nuget"></a>將 Twilio 程式庫新增至 Visual Studio 專案：</span><span class="sxs-lookup"><span data-stu-id="3afd8-186"><a id="use_nuget"></a>To add the Twilio libraries to your Visual Studio project:</span></span>
1. <span data-ttu-id="3afd8-187">在 Visual Studio 中開啟方案。</span><span class="sxs-lookup"><span data-stu-id="3afd8-187">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="3afd8-188">以滑鼠右鍵按一下 [參考]。</span><span class="sxs-lookup"><span data-stu-id="3afd8-188">Right-click **References**.</span></span>
3. <span data-ttu-id="3afd8-189">按一下 [管理 NuGet 套件...]</span><span class="sxs-lookup"><span data-stu-id="3afd8-189">Click **Manage NuGet Packages...**</span></span>
4. <span data-ttu-id="3afd8-190">按一下 [線上]。</span><span class="sxs-lookup"><span data-stu-id="3afd8-190">Click **Online**.</span></span>
5. <span data-ttu-id="3afd8-191">在搜尋線上方塊中，輸入 twilio。</span><span class="sxs-lookup"><span data-stu-id="3afd8-191">In the search online box, type *twilio*.</span></span>
6. <span data-ttu-id="3afd8-192">在 Twilio 套件上按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="3afd8-192">Click **Install** on the Twilio package.</span></span>

## <span data-ttu-id="3afd8-193"><a id="howto_make_call"></a>作法：撥出電話</span><span class="sxs-lookup"><span data-stu-id="3afd8-193"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="3afd8-194">以下顯示如何使用 **CallResource** 類別撥出電話。</span><span class="sxs-lookup"><span data-stu-id="3afd8-194">The following shows how to make an outgoing call using the **CallResource** class.</span></span> <span data-ttu-id="3afd8-195">此程式碼也使用 Twilio 提供的網站來傳回 Twilio 標記語言 (TwiML) 回應。</span><span class="sxs-lookup"><span data-stu-id="3afd8-195">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="3afd8-196">請將 **to** 和 **from** 電話號碼換成您的值，在執行程式碼之前，請記得先驗證 Twilio 帳戶的 **from** 電話號碼。</span><span class="sxs-lookup"><span data-stu-id="3afd8-196">Substitute your values for the **to** and **from** phone numbers, and ensure that you verify the **from** phone number for your Twilio account before running the code.</span></span>

    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize the TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    // Use the Twilio-provided site for the TwiML response.
    var url = "http://twimlets.com/message";
    url = $"{url}?Message%5B0%5D=Hello%20World";

    // Set the call From, To, and URL values to use for the call.
    // This sample uses the sandbox number provided by
    // Twilio to make the call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri(url));
        }

<span data-ttu-id="3afd8-197">如需 **CallResource.Create** 方法中傳遞之參數的詳細資訊，請參閱 [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls]。</span><span class="sxs-lookup"><span data-stu-id="3afd8-197">For more information about the parameters passed in to the **CallResource.Create** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="3afd8-198">如前所述，此程式碼使用 Twilio 提供的網站來傳回 TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="3afd8-198">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="3afd8-199">您可以改用您自己的網站來提供 TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="3afd8-199">You could instead use your own site to provide the TwiML response.</span></span> <span data-ttu-id="3afd8-200">如需詳細資訊，請參閱[如何：從您自己的網站提供 TwiML 回應](#howto_provide_twiml_responses)。</span><span class="sxs-lookup"><span data-stu-id="3afd8-200">For more information, see [How to: Provide TwiML responses from your own website](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="3afd8-201"><a id="howto_send_sms"></a>作法：傳送簡訊</span><span class="sxs-lookup"><span data-stu-id="3afd8-201"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="3afd8-202">下列螢幕擷取畫面顯示如何使用 **MessageResource** 類別來傳送簡訊。</span><span class="sxs-lookup"><span data-stu-id="3afd8-202">The following screenshot shows how to send an SMS message using the **MessageResource**  class.</span></span> <span data-ttu-id="3afd8-203">**from** 號碼由 Twilio 提供給試用帳戶來傳送簡訊。</span><span class="sxs-lookup"><span data-stu-id="3afd8-203">The **from** number is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="3afd8-204">執行程式碼之前，必須驗證 Twilio 帳戶的 **to** 號碼。</span><span class="sxs-lookup"><span data-stu-id="3afd8-204">The **to** number must be verified for your Twilio account before you run the code.</span></span>

    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize the TwilioClient.
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
        // An exception occurred making the REST call
        Console.WriteLine(ex.Message);
    }

## <span data-ttu-id="3afd8-205"><a id="howto_provide_twiml_responses"></a>作法：從您自己的網站提供 TwiML 回應</span><span class="sxs-lookup"><span data-stu-id="3afd8-205"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own website</span></span>
<span data-ttu-id="3afd8-206">當您的應用程式呼叫 Twilio API 時 (例如透過 **CallResource.Create** 方法)，Twilio 會將您的要求傳送到應該傳送 TwiML 回應的 URL。</span><span class="sxs-lookup"><span data-stu-id="3afd8-206">When your application initiates a call to the Twilio API - for example, via the **CallResource.Create** method - Twilio sends your request to an URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="3afd8-207">[作法：撥出電話](#howto_make_call)中的範例使用 Twilio 提供的 URL [http://twimlets.com/message][twimlet_message_url] 傳回回應。</span><span class="sxs-lookup"><span data-stu-id="3afd8-207">The example in [How to: Make an outgoing call](#howto_make_call) uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url] to return the response.</span></span>

> [!NOTE]
> <span data-ttu-id="3afd8-208">雖然 TwiML 是專供 Web 服務使用，但您也可以在瀏覽器中檢視 TwiML。</span><span class="sxs-lookup"><span data-stu-id="3afd8-208">While TwiML is designed for use by web services, you can view the TwiML in your browser.</span></span> <span data-ttu-id="3afd8-209">例如，按一下 [http://twimlets.com/message][twimlet_message_url] 可查看空白 &lt;Response&gt; 元素，又例如，按一下 [http://twimlets.com/message?Message%5B0%5D=Hello%20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) 可查看包含 &lt;Say&gt; 元素的 &lt;Response&gt; 元素。</span><span class="sxs-lookup"><span data-stu-id="3afd8-209">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty &lt;Response&gt; element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) to see a &lt;Response&gt; element that contains a &lt;Say&gt; element.</span></span>
>
>

<span data-ttu-id="3afd8-210">除了依賴 Twilio 提供的 URL，您也可以建立自己的 URL 網站來傳回 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="3afd8-210">Instead of relying on the Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="3afd8-211">您可以使用任何可傳回 HTTP 回應的語言來建立網站。</span><span class="sxs-lookup"><span data-stu-id="3afd8-211">You can create the site in any language that returns HTTP responses.</span></span> <span data-ttu-id="3afd8-212">本主題假設您從 ASP.NET 通用處理常式來裝載 URL。</span><span class="sxs-lookup"><span data-stu-id="3afd8-212">This topic assumes you'll be hosting the URL from an ASP.NET generic handler.</span></span>

<span data-ttu-id="3afd8-213">下列 ASP.NET 處理常式建構一個 TwiML 回應，在來電中顯示 **Hello World** 。</span><span class="sxs-lookup"><span data-stu-id="3afd8-213">The following ASP.NET Handler crafts a TwiML response that says **Hello World** on the call.</span></span>

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
    
<span data-ttu-id="3afd8-214">從以上範例中可知，TwiML 回應只是一份 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="3afd8-214">As you can see from the example above, the TwiML response is simply an XML document.</span></span> <span data-ttu-id="3afd8-215">Twilio.TwiML 程式庫包含可為您產生 TwiML 的類別。</span><span class="sxs-lookup"><span data-stu-id="3afd8-215">The Twilio.TwiML library contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="3afd8-216">下列範例會產生同上的回應，但是使用 **VoiceResponse** 類別。</span><span class="sxs-lookup"><span data-stu-id="3afd8-216">The example below produces the equivalent response as shown above, but uses the **VoiceResponse** class.</span></span>

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

<span data-ttu-id="3afd8-217">如需 TwiML 的詳細資訊，請參閱 [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml)。</span><span class="sxs-lookup"><span data-stu-id="3afd8-217">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span></span>

<span data-ttu-id="3afd8-218">設定好如何提供 TwiML 回應之後，就可以將 URL 傳入 **CallResource.Create** 方法。</span><span class="sxs-lookup"><span data-stu-id="3afd8-218">Once you have set up a way to provide TwiML responses, you can pass that URL to the **CallResource.Create** method.</span></span> <span data-ttu-id="3afd8-219">例如，如果您將名為 MyTwiML 的 Web 應用程式部署至 Azure 雲端服務，且您的 ASP.NET 處理常式名稱為 mytwiml.ashx，則可以如下列程式碼範例所示，將 URL 傳遞至 **CallResource.Create**：</span><span class="sxs-lookup"><span data-stu-id="3afd8-219">For example, if you have a web application named MyTwiML deployed to an Azure cloud service, and the name of your ASP.NET Handler is mytwiml.ashx, the URL can be passed to **CallResource.Create** as shown in the following code sample:</span></span>

    // This sample uses the sandbox number provided by Twilio to make the call.
    // Place the call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

<span data-ttu-id="3afd8-220">如需有關在 Azure with ASP.NET 上使用 Twilio 的詳細資訊，請參閱[如何在 Azure 的 Web 角色中使用 Twilio 來撥打電話][howto_phonecall_dotnet]。</span><span class="sxs-lookup"><span data-stu-id="3afd8-220">For additional information about using Twilio on Azure with ASP.NET, see [How to make a phone call using Twilio in a web role on Azure][howto_phonecall_dotnet].</span></span>

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
