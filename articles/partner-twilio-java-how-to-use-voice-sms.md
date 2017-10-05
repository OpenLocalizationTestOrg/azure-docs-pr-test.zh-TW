---
title: "如何使用 Twilio for Voice and SMS (Java) | Microsoft Docs"
description: "了解如何在 Azure 上使用 Twilio API 服務撥打電話及傳送簡訊。 程式碼範例以 Java 撰寫。"
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
ms.openlocfilehash: 5a1b2ffa160a31b639605242b651dc8d14e7a01b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-java"></a><span data-ttu-id="9b793-104">如何在 Java 中透過 Twilio 使用語音和簡訊功能</span><span class="sxs-lookup"><span data-stu-id="9b793-104">How to Use Twilio for Voice and SMS Capabilities in Java</span></span>
<span data-ttu-id="9b793-105">本指南示範如何在 Azure 上透過 Twilio API 服務執行常見的程式設計工作。</span><span class="sxs-lookup"><span data-stu-id="9b793-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="9b793-106">涵蓋的案例包括打電話和傳送簡訊 (SMS)。</span><span class="sxs-lookup"><span data-stu-id="9b793-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="9b793-107">如需有關如何在應用程式中使用 Twilio 語音和 SMS 的詳細資訊，請參閱 [後續步驟](#NextSteps) 一節。</span><span class="sxs-lookup"><span data-stu-id="9b793-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="9b793-108"><a id="WhatIs"></a>什麼是 Twilio？</span><span class="sxs-lookup"><span data-stu-id="9b793-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="9b793-109">Twilio 是一種電話語音 Web 服務 API，能夠讓您使用現有的 Web 語言和技術建立語音和 SMS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b793-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills to build voice and SMS applications.</span></span> <span data-ttu-id="9b793-110">Twilio 算是協力廠商服務 (並非 Azure 功能，也並非 Microsoft 產品)。</span><span class="sxs-lookup"><span data-stu-id="9b793-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="9b793-111">**Twilio 語音** 可讓應用程式撥打和接聽電話。</span><span class="sxs-lookup"><span data-stu-id="9b793-111">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="9b793-112">**Twilio SMS** 可以讓您的應用程式撰寫和接收 SMS 訊息。</span><span class="sxs-lookup"><span data-stu-id="9b793-112">**Twilio SMS** allows your applications to make and receive SMS messages.</span></span> <span data-ttu-id="9b793-113">**Twilio Client** 可以讓您的應用程式在現有網際網路連線 (包括行動連線) 中啟用語音通訊。</span><span class="sxs-lookup"><span data-stu-id="9b793-113">**Twilio Client** allows your applications to enable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="9b793-114"><a id="Pricing"></a>Twilio 定價和特別優惠</span><span class="sxs-lookup"><span data-stu-id="9b793-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="9b793-115">[Twilio 定價][twilio_pricing] (英文) 提供 Twilio 的定價資訊。</span><span class="sxs-lookup"><span data-stu-id="9b793-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="9b793-116">Azure 客戶可獲得[特殊優惠][special_offer]：免費 1000 則文字簡訊或接聽 1000 分鐘電話。</span><span class="sxs-lookup"><span data-stu-id="9b793-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="9b793-117">若要註冊獲得這項優惠或取得詳細資訊，請造訪 [http://ahoy.twilio.com/azure][special_offer] (英文)。</span><span class="sxs-lookup"><span data-stu-id="9b793-117">To sign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>

## <span data-ttu-id="9b793-118"><a id="Concepts"></a>概念</span><span class="sxs-lookup"><span data-stu-id="9b793-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="9b793-119">Twilio API 是一套為應用程式提供語音和簡訊功能的 RESTful API。</span><span class="sxs-lookup"><span data-stu-id="9b793-119">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="9b793-120">用戶端程式庫有多種語言版本，相關清單請參閱 [Twilio API 程式庫][twilio_libraries]。</span><span class="sxs-lookup"><span data-stu-id="9b793-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="9b793-121">Twilio API 的兩大重點是 Twilio 動詞和 Twilio 標記語言 (TwiML)。</span><span class="sxs-lookup"><span data-stu-id="9b793-121">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="9b793-122"><a id="Verbs"></a>Twilio 動詞</span><span class="sxs-lookup"><span data-stu-id="9b793-122"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="9b793-123">API 採用 Twilio 動詞。例如，**&lt;Say&gt;** 動詞指示 Twilio 在通話中用語音傳遞訊息。</span><span class="sxs-lookup"><span data-stu-id="9b793-123">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="9b793-124">以下是 Twilio 動詞清單。</span><span class="sxs-lookup"><span data-stu-id="9b793-124">The following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="9b793-125">**&lt;撥號&gt;**：使撥號者接通另一支電話。</span><span class="sxs-lookup"><span data-stu-id="9b793-125">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="9b793-126">**&lt;收集&gt;**：收集電話按鍵上輸入的號碼。</span><span class="sxs-lookup"><span data-stu-id="9b793-126">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="9b793-127">**&lt;掛斷&gt;**：結束通話。</span><span class="sxs-lookup"><span data-stu-id="9b793-127">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="9b793-128">**&lt;播放&gt;**：播放音訊檔案。</span><span class="sxs-lookup"><span data-stu-id="9b793-128">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="9b793-129">**&lt;佇列&gt;**︰新增至呼叫端佇列。</span><span class="sxs-lookup"><span data-stu-id="9b793-129">**&lt;Queue&gt;**: Add the to a queue of callers.</span></span>
* <span data-ttu-id="9b793-130">**&lt;暫停&gt;**：靜候一段指定的秒數。</span><span class="sxs-lookup"><span data-stu-id="9b793-130">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="9b793-131">**&lt;記錄&gt;**：錄製來電者的語音並傳回含有錄音的檔案 URL。</span><span class="sxs-lookup"><span data-stu-id="9b793-131">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="9b793-132">**&lt;重新導向&gt;**：將通話或簡訊的控制權移轉至不同 URL 的 TwiML。</span><span class="sxs-lookup"><span data-stu-id="9b793-132">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="9b793-133">**&lt;拒絕&gt;**：拒絕 Twilio 號碼的來電而不計費。</span><span class="sxs-lookup"><span data-stu-id="9b793-133">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you.</span></span>
* <span data-ttu-id="9b793-134">**&lt;說出&gt;**：將來電的文字轉換成語音。</span><span class="sxs-lookup"><span data-stu-id="9b793-134">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="9b793-135">**&lt;Sms&gt;**：傳送簡訊。</span><span class="sxs-lookup"><span data-stu-id="9b793-135">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="9b793-136"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="9b793-136"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="9b793-137">TwiML 是以 Twilio 動詞為基礎的一組 XML 指令，可指示 Twilio 如何處理來電或簡訊。</span><span class="sxs-lookup"><span data-stu-id="9b793-137">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="9b793-138">例如，下列 TwiML 會將文字 **Hello World!** 轉換</span><span class="sxs-lookup"><span data-stu-id="9b793-138">As an example, the following TwiML would convert the text **Hello World!**</span></span> <span data-ttu-id="9b793-139">成語音。</span><span class="sxs-lookup"><span data-stu-id="9b793-139">to speech.</span></span>

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="9b793-140">當應用程式呼叫 Twilio API 時，其中一個 API 參數是傳回 TwiML 回應的 URL。</span><span class="sxs-lookup"><span data-stu-id="9b793-140">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="9b793-141">在開發用途上，您可以使用 Twilio 提供的 URL 來提供應用程式所使用的 TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="9b793-141">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="9b793-142">您也可以裝載您自己的 URL 來產生 TwiML 回應，另一種選擇是使用 **TwiMLResponse** 物件。</span><span class="sxs-lookup"><span data-stu-id="9b793-142">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="9b793-143">如需 Twilio 動詞、屬性和 TwiML 的詳細資訊，請參閱 [TwiML][twiml]。</span><span class="sxs-lookup"><span data-stu-id="9b793-143">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="9b793-144">如需 Twilio API 的詳細資訊，請參閱 [Twilio API][twilio_api]。</span><span class="sxs-lookup"><span data-stu-id="9b793-144">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="9b793-145"><a id="CreateAccount"></a>建立 Twilio 帳戶</span><span class="sxs-lookup"><span data-stu-id="9b793-145"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="9b793-146">準備取得 Twilio 帳戶時，請至[試用 Twilio][try_twilio] 註冊。</span><span class="sxs-lookup"><span data-stu-id="9b793-146">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="9b793-147">您可以先使用免費帳戶，稍後再升級帳戶。</span><span class="sxs-lookup"><span data-stu-id="9b793-147">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="9b793-148">註冊 Twilio 帳戶時，您會收到帳戶識別碼和驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="9b793-148">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="9b793-149">兩者皆為呼叫 Twilio API 所需。</span><span class="sxs-lookup"><span data-stu-id="9b793-149">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="9b793-150">為了防止未經授權存取您的帳戶，您妥善保管驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="9b793-150">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="9b793-151">在 [Twilio 主控台][twilio_console]的 **ACCOUNT SID** 和 **AUTH TOKEN** 欄位中，分別可檢視您的帳戶識別碼和驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="9b793-151">Your account ID and authentication token are viewable at the [Twilio Console][twilio_console], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="9b793-152"><a id="create_app"></a>建立 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="9b793-152"><a id="create_app"></a>Create a Java Application</span></span>
1. <span data-ttu-id="9b793-153">取得 Twilio JAR 並將它加到您的 Java 組建路徑和 WAR 部署組件。</span><span class="sxs-lookup"><span data-stu-id="9b793-153">Obtain the Twilio JAR and add it to your Java build path and your WAR deployment assembly.</span></span> <span data-ttu-id="9b793-154">在 [https://github.com/twilio/twilio-java][twilio_java] 上，您可以下載 GitHub 來源及建立自己的 JAR，或下載預先建置的 JAR (可能有相依性)。</span><span class="sxs-lookup"><span data-stu-id="9b793-154">At [https://github.com/twilio/twilio-java][twilio_java], you can download the GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
2. <span data-ttu-id="9b793-155">確定 JDK 的 **cacerts** 金鑰存放區包含 MD5 指紋為 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (序號為 35:DE:F4:CF 且 SHA1 指紋為 D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A) 的 Equifax 安全憑證授權單位憑證。</span><span class="sxs-lookup"><span data-stu-id="9b793-155">Ensure your JDK's **cacerts** keystore contains the Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (the serial number is 35:DE:F4:CF and the SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="9b793-156">這是 [https://api.twilio.com][twilio_api_service] 服務的憑證授權單位 (CA) 憑證，會在您使用 Twilio API 時受到呼叫。</span><span class="sxs-lookup"><span data-stu-id="9b793-156">This is the certificate authority (CA) certificate for the [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="9b793-157">如需關於確定 JDK 的 **cacerts** 金鑰存放區包含正確 CA 憑證的詳細資訊，請參閱[新增憑證至 Java CA 憑證存放區][add_ca_cert]。</span><span class="sxs-lookup"><span data-stu-id="9b793-157">For information about ensuring your JDK's **cacerts** keystore contains the correct CA certificate, see [Adding a Certificate to the Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="9b793-158">[如何從 Azure 中的 Java 應用程式使用 Twilio 撥打電話][howto_phonecall_java]中提供使用 Java 版 Twilio 用戶端程式庫的詳細指示。</span><span class="sxs-lookup"><span data-stu-id="9b793-158">Detailed instructions for using the Twilio client library for Java are available at [How to Make a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="9b793-159"><a id="configure_app"></a>設定應用程式以使用 Twilio 程式庫</span><span class="sxs-lookup"><span data-stu-id="9b793-159"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="9b793-160">在您的程式碼中，您可以針對於要在應用程式中使用的 Twilio 封裝或類別，在其原始程式檔的頂端加入 **import** 陳述式。</span><span class="sxs-lookup"><span data-stu-id="9b793-160">Within your code, you can add **import** statements at the top of your source files for the Twilio packages or classes you want to use in your application.</span></span>

<span data-ttu-id="9b793-161">對於 Java 原始程式檔：</span><span class="sxs-lookup"><span data-stu-id="9b793-161">For Java source files:</span></span>

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

<span data-ttu-id="9b793-162">對於 Java 伺服器頁面 (JSP) 原始程式檔：</span><span class="sxs-lookup"><span data-stu-id="9b793-162">For Java Server Page (JSP) source files:</span></span>

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
<span data-ttu-id="9b793-163">端視要使用的 Twilio 封裝或類別而定，您的 **import** 陳述式可能不同。</span><span class="sxs-lookup"><span data-stu-id="9b793-163">Depending on which Twilio packages or classes you want to use, your **import** statements may be different.</span></span>

## <span data-ttu-id="9b793-164"><a id="howto_make_call"></a>作法：撥出電話</span><span class="sxs-lookup"><span data-stu-id="9b793-164"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="9b793-165">以下顯示如何使用 **Call** 類別撥出電話。</span><span class="sxs-lookup"><span data-stu-id="9b793-165">The following shows how to make an outgoing call using the **Call** class.</span></span> <span data-ttu-id="9b793-166">此程式碼也使用 Twilio 提供的網站來傳回 Twilio 標記語言 (TwiML) 回應。</span><span class="sxs-lookup"><span data-stu-id="9b793-166">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="9b793-167">請將 **from** 和 **to** 電話號碼換成您的值，在執行程式碼之前，請記得先驗證 Twilio 帳戶的 **from** 電話號碼。</span><span class="sxs-lookup"><span data-stu-id="9b793-167">Substitute your values for the **from** and **to** phone numbers, and ensure that you verify the **from** phone number for your Twilio account prior to running the code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize the Twilio client.
    Twilio.init(accountSID, authToken);

    // Use the Twilio-provided site for the TwiML response.
    URI uri = new URI("http://twimlets.com/message" +
            "?Message%5B0%5D=Hello%20World%21");

    // Declare To and From numbers
    PhoneNumber to = new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");

    // Create a Call creator passing From, To and URL values
    // then make the call by executing the create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="9b793-168">如需 **Call.creator** 方法中傳遞之參數的詳細資訊，請參閱 [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls] (英文)。</span><span class="sxs-lookup"><span data-stu-id="9b793-168">For more information about the parameters passed in to the **Call.creator** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="9b793-169">如前所述，此程式碼使用 Twilio 提供的網站來傳回 TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="9b793-169">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="9b793-170">您可以改用自己的網站提供 TwiML 回應；如需詳細資訊，請參閱 [如何在 Azure 上的 Java 應用程式中提供 TwiML 回應](#howto_provide_twiml_responses)。</span><span class="sxs-lookup"><span data-stu-id="9b793-170">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses in a Java Application on Azure](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="9b793-171"><a id="howto_send_sms"></a>作法：傳送簡訊</span><span class="sxs-lookup"><span data-stu-id="9b793-171"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="9b793-172">以下顯示如何使用 **Message** 類別傳送 SMS 訊息。</span><span class="sxs-lookup"><span data-stu-id="9b793-172">The following shows how to send an SMS message using the **Message** class.</span></span> <span data-ttu-id="9b793-173">**from** 號碼 **4155992671** 是 Twilio 提供來傳送 SMS 訊息的試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9b793-173">The **from** number, **4155992671**, is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="9b793-174">執行程式碼之前，必須驗證您 Twilio 帳戶的 **to** 號碼。</span><span class="sxs-lookup"><span data-stu-id="9b793-174">The **to** number must be verified for your Twilio account prior to running the code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize the Twilio client.
    Twilio.init(accountSID, authToken);

    // Declare To and From numbers and the Body of the SMS message
    PhoneNumber to = new PhoneNumber("+14159352345"); // Replace with a valid phone number for your account.
    PhoneNumber from = new PhoneNumber("+14158141829"); // Replace with a valid phone number for your account.
    String body = "Where's Wallace?";

    // Create a Message creator passing From, To and Body values
    // then send the SMS message by calling the create() method
    Message sms = Message.creator(to, from, body).create();
```

<span data-ttu-id="9b793-175">如需 **Message.creator** 方法中傳遞之參數的詳細資訊，請參閱 [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms] (英文)。</span><span class="sxs-lookup"><span data-stu-id="9b793-175">For more information about the parameters passed in to the **Message.creator** method, see [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span></span>

## <span data-ttu-id="9b793-176"><a id="howto_provide_twiml_responses"></a>作法：從您自己的網站提供 TwiML 回應</span><span class="sxs-lookup"><span data-stu-id="9b793-176"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="9b793-177">當您的應用程式呼叫 Twilio API 時 (例如透過 **CallCreator.create** 方法)，Twilio 將傳送您的要求到應該傳送 TwiML 回應的 URL。</span><span class="sxs-lookup"><span data-stu-id="9b793-177">When your application initiates a call to the Twilio API, for example via the **CallCreator.create** method, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="9b793-178">前述範例使用 Twilio 提供的 URL [http://twimlets.com/message][twimlet_message_url]。</span><span class="sxs-lookup"><span data-stu-id="9b793-178">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="9b793-179">(雖然 TwiML 是針對供 Web 服務使用而設計，但您可以在瀏覽器中檢視 TwiML。</span><span class="sxs-lookup"><span data-stu-id="9b793-179">(While TwiML is designed for use by Web services, you can view the TwiML in your browser.</span></span> <span data-ttu-id="9b793-180">例如，按一下 [http://twimlets.com/message][twimlet_message_url] 可查看空白 **&lt;Response&gt;** 元素，又例如，按一下 [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] 可查看包含 **&lt;Say&gt;** 元素的 **&lt;Response&gt;** 元素。)</span><span class="sxs-lookup"><span data-stu-id="9b793-180">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty **&lt;Response&gt;** element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] to see a **&lt;Response&gt;** element that contains a **&lt;Say&gt;** element.)</span></span>

<span data-ttu-id="9b793-181">除了依賴 Twilio 提供的 URL，您也可以建立自己的 URL 網站來傳回 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="9b793-181">Instead of relying on the Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="9b793-182">您可以使用任何語言建立會傳回 HTTP 回應的網站；本主題假設您將該 URL 裝載在 JSP 頁面中。</span><span class="sxs-lookup"><span data-stu-id="9b793-182">You can create the site in any language that returns HTTP responses; this topic assumes you'll be hosting the URL in a JSP page.</span></span>

<span data-ttu-id="9b793-183">下列 JSP 頁面將引起 TwiML 說出 **Hello World** 作為回應</span><span class="sxs-lookup"><span data-stu-id="9b793-183">The following JSP page results in a TwiML response that says **Hello World!**</span></span> <span data-ttu-id="9b793-184">(在通話中)。</span><span class="sxs-lookup"><span data-stu-id="9b793-184">on the call.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="9b793-185">下列 JSP 頁面將引起 TwiML 有以下回應：說出一些文字、停頓數次，然後說出 Twilio API 版本和 Azure 角色名稱資訊。</span><span class="sxs-lookup"><span data-stu-id="9b793-185">The following JSP page results in a TwiML response that says some text, has several pauses, and says information about the Twilio API version and the Azure role name.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello from Azure!</Say>
        <Pause></Pause>
        <Say>The Twilio API version is <%= request.getParameter("ApiVersion") %>.</Say>
        <Say>The Azure role name is <%= System.getenv("RoleName") %>.</Say>
        <Pause></Pause>
        <Say>Good bye.</Say>
    </Response>
```

<span data-ttu-id="9b793-186">**ApiVersion** 參數會出現在 Twilio 語音要求 (而非 SMS 要求) 中。</span><span class="sxs-lookup"><span data-stu-id="9b793-186">The **ApiVersion** parameter is available in Twilio voice requests (not SMS requests).</span></span> <span data-ttu-id="9b793-187">若要查看 Twilio 語音和 SMS 要求的可用要求參數，請分別參閱 <https://www.twilio.com/docs/api/twiml/twilio_request> (英文) 及 <https://www.twilio.com/docs/api/twiml/sms/twilio_request> (英文)。</span><span class="sxs-lookup"><span data-stu-id="9b793-187">To see the available request parameters for Twilio voice and SMS requests, see <https://www.twilio.com/docs/api/twiml/twilio_request> and <https://www.twilio.com/docs/api/twiml/sms/twilio_request>, respectively.</span></span> <span data-ttu-id="9b793-188">**RoleName** 環境參數會隨附在 Azure 部署中。</span><span class="sxs-lookup"><span data-stu-id="9b793-188">The **RoleName** environment variable is available as part of an Azure deployment.</span></span> <span data-ttu-id="9b793-189">(如果您要新增自訂環境參數，以便可以從 **System.getenv** 選擇這些參數，請參閱[其他角色組態設定的環境變數][misc_role_config_settings]一節。)</span><span class="sxs-lookup"><span data-stu-id="9b793-189">(If you want to add custom environment variables so they could be picked up from **System.getenv**, see the environment variables section at [Miscellaneous Role Configuration Settings][misc_role_config_settings].)</span></span>

<span data-ttu-id="9b793-190">設定 JSP 頁面來提供 TwiML 回應之後，請使用 JSP 頁面的 URL 作為傳遞到 **Call.creator** 方法的 URL。</span><span class="sxs-lookup"><span data-stu-id="9b793-190">Once you have your JSP page set up to provide TwiML responses, use the URL of the JSP page as the URL passed into the **Call.creator** method.</span></span> <span data-ttu-id="9b793-191">例如，如果將名稱為 MyTwiML 的 Web 應用程式部署到 Azure 託管服務，而且 JSP 頁面的名稱是 mytwiml.jsp，則可以將 URL 傳遞到 **Call.creator**，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9b793-191">For example, if you have a Web application named MyTwiML deployed to an Azure hosted service, and the name of the JSP page is mytwiml.jsp, the URL can be passed to **Call.creator** as shown in the following:</span></span>

```java
    // Declare To and From numbers and the URL of your JSP page
    PhoneNumber to = new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, To and URL values
    // then make the call by executing the create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="9b793-192">另一個選項是透過 **com.twilio.twiml** 封裝中的 **VoiceResponse** 類別進行 TwiML 回應。</span><span class="sxs-lookup"><span data-stu-id="9b793-192">Another option for responding with TwiML is via the **VoiceResponse** class, which is available in the **com.twilio.twiml** package.</span></span>

<span data-ttu-id="9b793-193">如需關於透過 Java 在 Azure 中使用 Twilio 的詳細資訊，請參閱[如何從 Azure 中的 Java 應用程式使用 Twilio 撥打電話][howto_phonecall_java]。</span><span class="sxs-lookup"><span data-stu-id="9b793-193">For additional information about using Twilio in Azure with Java, see [How to Make a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="9b793-194"><a id="AdditionalServices"></a>如何：使用其他 Twilio 服務</span><span class="sxs-lookup"><span data-stu-id="9b793-194"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="9b793-195">除了此處所示的範例以外，Twilio 還提供網頁式 API，方便您從 Azure 應用程式中充份利用其他 Twilio 功能。</span><span class="sxs-lookup"><span data-stu-id="9b793-195">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="9b793-196">如需完整詳細資料，請參閱 [Twilio API 文件][twilio_api_documentation]。</span><span class="sxs-lookup"><span data-stu-id="9b793-196">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="9b793-197"><a id="NextSteps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="9b793-197"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="9b793-198">了解基本的 Twilio 服務之後，請參考下列連結以取得更多資訊：</span><span class="sxs-lookup"><span data-stu-id="9b793-198">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="9b793-199">[Twilio 安全性方針][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="9b793-199">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="9b793-200">[Twilio 作法與範例程式碼][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="9b793-200">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="9b793-201">[Twilio 快速入門教學課程][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="9b793-201">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="9b793-202">[GitHub 上的 Twilio][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="9b793-202">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="9b793-203">[洽詢 Twilio 支援][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="9b793-203">[Talk to Twilio Support][twilio_support]</span></span>

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
