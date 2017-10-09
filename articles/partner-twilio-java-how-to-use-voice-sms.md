---
title: "aaaHow tooUse Twilio 語音和 SMS (Java) |Microsoft 文件"
description: "了解如何 toomake 電話及傳送 SMS 訊息 hello Twilio API 服務在 Azure 上。 程式碼範例以 Java 撰寫。"
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: f3508965-5527-4255-9d51-5d5f926f4d43
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: a186e2c8e73ced928bd0dec348971034f10ba82c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-java"></a><span data-ttu-id="41162-104">如何 tooUse Twilio 語音和簡訊功能，在 Java 中</span><span class="sxs-lookup"><span data-stu-id="41162-104">How tooUse Twilio for Voice and SMS Capabilities in Java</span></span>
<span data-ttu-id="41162-105">本指南示範如何 tooperform 常見的程式設計工作以 hello Twilio API 服務在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="41162-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="41162-106">涵蓋的 hello 案例包括撥電話及傳送短訊息服務 (SMS) 訊息。</span><span class="sxs-lookup"><span data-stu-id="41162-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="41162-107">如需有關 Twilio 和您的應用程式中使用語音和 SMS 的詳細資訊，請參閱 hello[接下來的步驟](#NextSteps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="41162-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="41162-108"><a id="WhatIs"></a>什麼是 Twilio？</span><span class="sxs-lookup"><span data-stu-id="41162-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="41162-109">Twilio 是電話語音 web 服務 API，可讓您使用現有的 web 語言和技術 toobuild 語音和 SMS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="41162-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills toobuild voice and SMS applications.</span></span> <span data-ttu-id="41162-110">Twilio 算是協力廠商服務 (並非 Azure 功能，也並非 Microsoft 產品)。</span><span class="sxs-lookup"><span data-stu-id="41162-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="41162-111">**Twilio 語音**可讓您的應用程式 toomake 撥打與接聽電話。</span><span class="sxs-lookup"><span data-stu-id="41162-111">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="41162-112">**Twilio SMS**可讓您的應用程式 toomake 和接收 SMS 訊息。</span><span class="sxs-lookup"><span data-stu-id="41162-112">**Twilio SMS** allows your applications toomake and receive SMS messages.</span></span> <span data-ttu-id="41162-113">**Twilio 用戶端**tooenable 語音通訊使用現有的網際網路連線，包括行動裝置的連線，可讓您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="41162-113">**Twilio Client** allows your applications tooenable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="41162-114"><a id="Pricing"></a>Twilio 定價和特別優惠</span><span class="sxs-lookup"><span data-stu-id="41162-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="41162-115">[Twilio 定價][twilio_pricing] (英文) 提供 Twilio 的定價資訊。</span><span class="sxs-lookup"><span data-stu-id="41162-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="41162-116">Azure 客戶可獲得[特殊優惠][special_offer]：免費 1000 則文字簡訊或接聽 1000 分鐘電話。</span><span class="sxs-lookup"><span data-stu-id="41162-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="41162-117">註冊這 toosign 提供或取得詳細資訊，請瀏覽[http://ahoy.twilio.com/azure][special_offer]。</span><span class="sxs-lookup"><span data-stu-id="41162-117">toosign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>

## <span data-ttu-id="41162-118"><a id="Concepts"></a>概念</span><span class="sxs-lookup"><span data-stu-id="41162-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="41162-119">hello Twilio API 是 rest 式 API，應用程式提供語音和 SMS 功能。</span><span class="sxs-lookup"><span data-stu-id="41162-119">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="41162-120">用戶端程式庫有多種語言版本，相關清單請參閱 [Twilio API 程式庫][twilio_libraries]。</span><span class="sxs-lookup"><span data-stu-id="41162-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="41162-121">Hello Twilio API 的重要層面是 Twilio 動詞和 Twilio 標記語言 (TwiML)。</span><span class="sxs-lookup"><span data-stu-id="41162-121">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="41162-122"><a id="Verbs"></a>Twilio 動詞</span><span class="sxs-lookup"><span data-stu-id="41162-122"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="41162-123">hello API 會使用 Twilio 動詞命令。例如，hello **&lt;說&gt;**動詞命令會指示 Twilio tooaudibly 傳遞的訊息上呼叫。</span><span class="sxs-lookup"><span data-stu-id="41162-123">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="41162-124">hello 如下的 Twilio 指令動詞的清單。</span><span class="sxs-lookup"><span data-stu-id="41162-124">hello following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="41162-125">**&lt;撥號&gt;**： 連接 hello 呼叫端 tooanother 電話。</span><span class="sxs-lookup"><span data-stu-id="41162-125">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="41162-126">**&lt;收集&gt;**： 會收集輸入 hello 電話字鍵台上的數字。</span><span class="sxs-lookup"><span data-stu-id="41162-126">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="41162-127">**&lt;掛斷&gt;**：結束通話。</span><span class="sxs-lookup"><span data-stu-id="41162-127">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="41162-128">**&lt;播放&gt;**：播放音訊檔案。</span><span class="sxs-lookup"><span data-stu-id="41162-128">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="41162-129">**&lt;佇列&gt;**： 新增 hello tooa 佇列的呼叫端。</span><span class="sxs-lookup"><span data-stu-id="41162-129">**&lt;Queue&gt;**: Add hello tooa queue of callers.</span></span>
* <span data-ttu-id="41162-130">**&lt;暫停&gt;**：靜候一段指定的秒數。</span><span class="sxs-lookup"><span data-stu-id="41162-130">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="41162-131">**&lt;記錄&gt;**： 記錄 hello 呼叫者的語音，並傳回包含 hello 記錄檔的 URL。</span><span class="sxs-lookup"><span data-stu-id="41162-131">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="41162-132">**&lt;重新導向&gt;**： 控制權的通話或 SMS toohello TwiML 於不同的 URL。</span><span class="sxs-lookup"><span data-stu-id="41162-132">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="41162-133">**&lt;拒絕&gt;**： 拒絕傳入的呼叫未使用計費您 tooyour Twilio 數目。</span><span class="sxs-lookup"><span data-stu-id="41162-133">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you.</span></span>
* <span data-ttu-id="41162-134">**&lt;說出&gt;**： 將文字 toospeech 所做的呼叫上。</span><span class="sxs-lookup"><span data-stu-id="41162-134">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="41162-135">**&lt;Sms&gt;**：傳送簡訊。</span><span class="sxs-lookup"><span data-stu-id="41162-135">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="41162-136"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="41162-136"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="41162-137">TwiML 是以 XML 為基礎的指示，就會通知方式的 Twilio hello Twilio 動詞命令為基礎的一組 tooprocess 通話或 SMS。</span><span class="sxs-lookup"><span data-stu-id="41162-137">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="41162-138">例如，下列 TwiML hello 將轉換的 hello 文字**Hello World ！**</span><span class="sxs-lookup"><span data-stu-id="41162-138">As an example, hello following TwiML would convert hello text **Hello World!**</span></span> <span data-ttu-id="41162-139">toospeech。</span><span class="sxs-lookup"><span data-stu-id="41162-139">toospeech.</span></span>

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="41162-140">當您的應用程式呼叫 hello Twilio 應用程式開發介面時，其中 hello API 參數會是傳回 hello TwiML 回應 hello URL。</span><span class="sxs-lookup"><span data-stu-id="41162-140">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="41162-141">供開發應用程式，您可以使用您的應用程式所使用的 Twilio 提供 Url tooprovide hello TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="41162-141">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="41162-142">您也可以裝載自己 Url tooproduce hello TwiML 回應，和另一個選項是 toouse hello **TwiMLResponse**物件。</span><span class="sxs-lookup"><span data-stu-id="41162-142">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="41162-143">如需 Twilio 動詞、屬性和 TwiML 的詳細資訊，請參閱 [TwiML][twiml]。</span><span class="sxs-lookup"><span data-stu-id="41162-143">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="41162-144">如需 hello Twilio API 的詳細資訊，請參閱[Twilio API][twilio_api]。</span><span class="sxs-lookup"><span data-stu-id="41162-144">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="41162-145"><a id="CreateAccount"></a>建立 Twilio 帳戶</span><span class="sxs-lookup"><span data-stu-id="41162-145"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="41162-146">當你準備好 tooget Twilio 帳戶時，請在註冊[再試一次 Twilio][try_twilio]。</span><span class="sxs-lookup"><span data-stu-id="41162-146">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="41162-147">您可以先使用免費帳戶，稍後再升級帳戶。</span><span class="sxs-lookup"><span data-stu-id="41162-147">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="41162-148">註冊 Twilio 帳戶時，您會收到帳戶識別碼和驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="41162-148">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="41162-149">同時會為所需的 toomake Twilio API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="41162-149">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="41162-150">tooprevent 未經授權存取 tooyour 帳戶，讓驗證權杖的安全。</span><span class="sxs-lookup"><span data-stu-id="41162-150">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="41162-151">您的帳戶識別碼和驗證權杖皆可檢視在 hello [Twilio 主控台][twilio_console]，請在 hello 欄位標示為**帳戶 SID**和**驗證語彙基元**分別。</span><span class="sxs-lookup"><span data-stu-id="41162-151">Your account ID and authentication token are viewable at hello [Twilio Console][twilio_console], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="41162-152"><a id="create_app"></a>建立 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="41162-152"><a id="create_app"></a>Create a Java Application</span></span>
1. <span data-ttu-id="41162-153">取得 hello Twilio JAR，並將它加入的 tooyour Java 建置路徑與 WAR 部署組件。</span><span class="sxs-lookup"><span data-stu-id="41162-153">Obtain hello Twilio JAR and add it tooyour Java build path and your WAR deployment assembly.</span></span> <span data-ttu-id="41162-154">在[https://github.com/twilio/twilio-java][twilio_java]，您可以下載 hello GitHub 來源並建立您自己的 JAR，或下載預先建立的 JAR （不論有無相依性）。</span><span class="sxs-lookup"><span data-stu-id="41162-154">At [https://github.com/twilio/twilio-java][twilio_java], you can download hello GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
2. <span data-ttu-id="41162-155">請確定您的 JDK **cacerts**金鑰存放區包含 hello Equifax 安全憑證授權單位憑證的 MD5 指紋 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 （hello 序號為 35:DE:F4:CF 和 hello SHA1指紋是 D2:32:09:AD:23:D3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A)。</span><span class="sxs-lookup"><span data-stu-id="41162-155">Ensure your JDK's **cacerts** keystore contains hello Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello serial number is 35:DE:F4:CF and hello SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="41162-156">這是 hello hello 憑證授權單位 (CA) 憑證[https://api.twilio.com] [ twilio_api_service]服務，當您使用 Twilio Api 時呼叫。</span><span class="sxs-lookup"><span data-stu-id="41162-156">This is hello certificate authority (CA) certificate for hello [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="41162-157">如需確保您的 JDK **cacerts**金鑰存放區包含 hello 正確的 CA 憑證，請參閱[新增憑證 toohello Java CA 憑證存放區][add_ca_cert]。</span><span class="sxs-lookup"><span data-stu-id="41162-157">For information about ensuring your JDK's **cacerts** keystore contains hello correct CA certificate, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="41162-158">使用 Java hello Twilio 用戶端程式庫的詳細的指示位於[如何 tooMake 在 Java 應用程式在 Azure 上的電話使用 Twilio][howto_phonecall_java]。</span><span class="sxs-lookup"><span data-stu-id="41162-158">Detailed instructions for using hello Twilio client library for Java are available at [How tooMake a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="41162-159"><a id="configure_app"></a>設定您的應用程式 tooUse Twilio 文件庫</span><span class="sxs-lookup"><span data-stu-id="41162-159"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="41162-160">在您的程式碼中，您可以加入**匯入**在 hello hello Twilio 封裝，或您類別的原始程式檔最上方的陳述式要 toouse 應用程式中的。</span><span class="sxs-lookup"><span data-stu-id="41162-160">Within your code, you can add **import** statements at hello top of your source files for hello Twilio packages or classes you want toouse in your application.</span></span>

<span data-ttu-id="41162-161">對於 Java 原始程式檔：</span><span class="sxs-lookup"><span data-stu-id="41162-161">For Java source files:</span></span>

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

<span data-ttu-id="41162-162">對於 Java 伺服器頁面 (JSP) 原始程式檔：</span><span class="sxs-lookup"><span data-stu-id="41162-162">For Java Server Page (JSP) source files:</span></span>

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
<span data-ttu-id="41162-163">根據哪些 Twilio 封裝或類別中，您想 toouse，您**匯入**陳述式可能會不同。</span><span class="sxs-lookup"><span data-stu-id="41162-163">Depending on which Twilio packages or classes you want toouse, your **import** statements may be different.</span></span>

## <span data-ttu-id="41162-164"><a id="howto_make_call"></a>作法：撥出電話</span><span class="sxs-lookup"><span data-stu-id="41162-164"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="41162-165">hello 下列範例示範如何 toomake 傳出呼叫使用 hello**呼叫**類別。</span><span class="sxs-lookup"><span data-stu-id="41162-165">hello following shows how toomake an outgoing call using hello **Call** class.</span></span> <span data-ttu-id="41162-166">此程式碼也會使用 Twilio 提供站台 tooreturn hello Twilio 標記語言 (TwiML) 回應。</span><span class="sxs-lookup"><span data-stu-id="41162-166">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="41162-167">替換為您的值為 hello**從**和**至**電話號碼，並確保您確認 hello**從**電話號碼您 Twilio 帳戶先前 toorunning hello 撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="41162-167">Substitute your values for hello **from** and **to** phone numbers, and ensure that you verify hello **from** phone number for your Twilio account prior toorunning hello code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    URI uri = new URI("http://twimlets.com/message" +
            "?Message%5B0%5D=Hello%20World%21");

    // Declare tooand From numbers
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="41162-168">如需有關 hello 參數傳入 toohello **Call.creator**方法，請參閱[http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls]。</span><span class="sxs-lookup"><span data-stu-id="41162-168">For more information about hello parameters passed in toohello **Call.creator** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="41162-169">如前所述，此程式碼會使用 Twilio 提供站台 tooreturn hello TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="41162-169">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="41162-170">您可以改為使用您自己的站台 tooprovide hello TwiML 回應。如需詳細資訊，請參閱[如何在 Java 應用程式在 Azure 上 TwiML 回應 tooProvide](#howto_provide_twiml_responses)。</span><span class="sxs-lookup"><span data-stu-id="41162-170">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses in a Java Application on Azure](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="41162-171"><a id="howto_send_sms"></a>作法：傳送簡訊</span><span class="sxs-lookup"><span data-stu-id="41162-171"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="41162-172">hello 下列範例示範如何 toosend SMS 訊息使用 hello**訊息**類別。</span><span class="sxs-lookup"><span data-stu-id="41162-172">hello following shows how toosend an SMS message using hello **Message** class.</span></span> <span data-ttu-id="41162-173">hello**從**號**4155992671**，為試用版帳戶 toosend SMS 訊息由 Twilio 中提供。</span><span class="sxs-lookup"><span data-stu-id="41162-173">hello **from** number, **4155992671**, is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="41162-174">hello**至**數目必須驗證您 Twilio 帳戶先前 toorunning hello 撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="41162-174">hello **to** number must be verified for your Twilio account prior toorunning hello code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Declare tooand From numbers and hello Body of hello SMS message
    PhoneNumber too= new PhoneNumber("+14159352345"); // Replace with a valid phone number for your account.
    PhoneNumber from = new PhoneNumber("+14158141829"); // Replace with a valid phone number for your account.
    String body = "Where's Wallace?";

    // Create a Message creator passing From, tooand Body values
    // then send hello SMS message by calling hello create() method
    Message sms = Message.creator(to, from, body).create();
```

<span data-ttu-id="41162-175">如需有關 hello 參數傳入 toohello **Message.creator**方法，請參閱[http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms]。</span><span class="sxs-lookup"><span data-stu-id="41162-175">For more information about hello parameters passed in toohello **Message.creator** method, see [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span></span>

## <span data-ttu-id="41162-176"><a id="howto_provide_twiml_responses"></a>作法：從您自己的網站提供 TwiML 回應</span><span class="sxs-lookup"><span data-stu-id="41162-176"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="41162-177">當您的應用程式會起始呼叫 toohello Twilio 應用程式開發介面，例如透過 hello **CallCreator.create**方法，Twilio 會傳送要求 tooa URL 所預期的 tooreturn TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="41162-177">When your application initiates a call toohello Twilio API, for example via hello **CallCreator.create** method, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="41162-178">上述的 hello 範例會使用 hello Twilio 提供 URL [http://twimlets.com/message][twimlet_message_url]。</span><span class="sxs-lookup"><span data-stu-id="41162-178">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="41162-179">（雖然 TwiML 設計為使用 Web 服務，您可以檢視 hello TwiML 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="41162-179">(While TwiML is designed for use by Web services, you can view hello TwiML in your browser.</span></span> <span data-ttu-id="41162-180">例如，按一下[http://twimlets.com/message] [ twimlet_message_url] toosee 空**&lt;回應&gt;**項目，做為另一個範例中，按一下 [ [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21] [ twimlet_message_url_hello_world] toosee **&lt;回應&gt;**包含項目**&lt;說&gt;** 項目。)</span><span class="sxs-lookup"><span data-stu-id="41162-180">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty **&lt;Response&gt;** element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] toosee a **&lt;Response&gt;** element that contains a **&lt;Say&gt;** element.)</span></span>

<span data-ttu-id="41162-181">而不是依賴 hello Twilio 提供 URL，您可以建立您自己會傳回 HTTP 回應的 URL 站台。</span><span class="sxs-lookup"><span data-stu-id="41162-181">Instead of relying on hello Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="41162-182">您可以建立 hello 網站中的任何語言，會傳回 HTTP 回應。本主題假設您要主控 JSP 頁面中的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="41162-182">You can create hello site in any language that returns HTTP responses; this topic assumes you'll be hosting hello URL in a JSP page.</span></span>

<span data-ttu-id="41162-183">hello 遵循 JSP 頁面結果以指出 TwiML 回應**Hello World ！**</span><span class="sxs-lookup"><span data-stu-id="41162-183">hello following JSP page results in a TwiML response that says **Hello World!**</span></span> <span data-ttu-id="41162-184">在 hello 呼叫。</span><span class="sxs-lookup"><span data-stu-id="41162-184">on hello call.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="41162-185">遵循 JSP 頁面結果，以顯示一些文字，TwiML 回應 hello 具有數個暫停，而且隻字 hello Twilio API 版本與 hello Azure 角色名稱的資訊。</span><span class="sxs-lookup"><span data-stu-id="41162-185">hello following JSP page results in a TwiML response that says some text, has several pauses, and says information about hello Twilio API version and hello Azure role name.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello from Azure!</Say>
        <Pause></Pause>
        <Say>hello Twilio API version is <%= request.getParameter("ApiVersion") %>.</Say>
        <Say>hello Azure role name is <%= System.getenv("RoleName") %>.</Say>
        <Pause></Pause>
        <Say>Good bye.</Say>
    </Response>
```

<span data-ttu-id="41162-186">hello **Microsoft.authorization**參數可用於 Twilio 提出要求 （不是 SMS 要求）。</span><span class="sxs-lookup"><span data-stu-id="41162-186">hello **ApiVersion** parameter is available in Twilio voice requests (not SMS requests).</span></span> <span data-ttu-id="41162-187">toosee hello 可用的要求參數 Twilio 語音和 SMS 要求，請參閱<https://www.twilio.com/docs/api/twiml/twilio_request>和<https://www.twilio.com/docs/api/twiml/sms/twilio_request>分別。</span><span class="sxs-lookup"><span data-stu-id="41162-187">toosee hello available request parameters for Twilio voice and SMS requests, see <https://www.twilio.com/docs/api/twiml/twilio_request> and <https://www.twilio.com/docs/api/twiml/sms/twilio_request>, respectively.</span></span> <span data-ttu-id="41162-188">hello **RoleName**環境變數可做為 Azure 部署的一部分。</span><span class="sxs-lookup"><span data-stu-id="41162-188">hello **RoleName** environment variable is available as part of an Azure deployment.</span></span> <span data-ttu-id="41162-189">(如果您想 tooadd 自訂的環境變數，它們無法從挑選**System.getenv**，請參閱 hello 環境變數[其他角色的組態設定][misc_role_config_settings].)</span><span class="sxs-lookup"><span data-stu-id="41162-189">(If you want tooadd custom environment variables so they could be picked up from **System.getenv**, see hello environment variables section at [Miscellaneous Role Configuration Settings][misc_role_config_settings].)</span></span>

<span data-ttu-id="41162-190">一旦您的 JSP 頁面設定 tooprovide TwiML 回應，做為 hello hello JSP 網頁 URL hello URL 傳入 hello **Call.creator**方法。</span><span class="sxs-lookup"><span data-stu-id="41162-190">Once you have your JSP page set up tooprovide TwiML responses, use hello URL of hello JSP page as hello URL passed into hello **Call.creator** method.</span></span> <span data-ttu-id="41162-191">比方說，如果您的 Web 應用程式名為 MyTwiML 部署 tooan Azure 託管服務，和 hello 頁面名稱的 hello JSP mytwiml.jsp，可以傳遞 hello URL 太**Call.creator** hello 下列所示：</span><span class="sxs-lookup"><span data-stu-id="41162-191">For example, if you have a Web application named MyTwiML deployed tooan Azure hosted service, and hello name of hello JSP page is mytwiml.jsp, hello URL can be passed too**Call.creator** as shown in hello following:</span></span>

```java
    // Declare tooand From numbers and hello URL of your JSP page
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="41162-192">以 TwiML 回應的另一個選項是透過 hello **VoiceResponse**類別，其可於 hello **com.twilio.twiml**封裝。</span><span class="sxs-lookup"><span data-stu-id="41162-192">Another option for responding with TwiML is via hello **VoiceResponse** class, which is available in hello **com.twilio.twiml** package.</span></span>

<span data-ttu-id="41162-193">如需有關在 Azure 的 Java 中使用 Twilio 的詳細資訊，請參閱[如何 tooMake 在 Java 應用程式在 Azure 上的電話使用 Twilio][howto_phonecall_java]。</span><span class="sxs-lookup"><span data-stu-id="41162-193">For additional information about using Twilio in Azure with Java, see [How tooMake a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="41162-194"><a id="AdditionalServices"></a>如何：使用其他 Twilio 服務</span><span class="sxs-lookup"><span data-stu-id="41162-194"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="41162-195">此外 toohello 範例所示，Twilio 提供網頁型應用程式開發介面，您可以使用其他 Twilio 功能 tooleverage 從 Azure 應用程式。</span><span class="sxs-lookup"><span data-stu-id="41162-195">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="41162-196">完整的詳細資訊，請參閱 hello [Twilio API 文件][twilio_api_documentation]。</span><span class="sxs-lookup"><span data-stu-id="41162-196">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="41162-197"><a id="NextSteps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="41162-197"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="41162-198">既然您已經學會 hello hello Twilio 服務基本概念，請依照下列多個這些連結 toolearn:</span><span class="sxs-lookup"><span data-stu-id="41162-198">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="41162-199">[Twilio 安全性方針][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="41162-199">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="41162-200">[Twilio 作法與範例程式碼][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="41162-200">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="41162-201">[Twilio 快速入門教學課程][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="41162-201">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="41162-202">[GitHub 上的 Twilio][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="41162-202">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="41162-203">[Talk tooTwilio 支援][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="41162-203">[Talk tooTwilio Support][twilio_support]</span></span>

[twilio_java]: https://github.com/twilio/twilio-java
[twilio_api_service]: https://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[howto_phonecall_java]: partner-twilio-java-phone-call-example.md
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World%21
[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls
[twilio_rest_sending_sms]: http://www.twilio.com/docs/api/rest/sending-sms
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/docs
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
