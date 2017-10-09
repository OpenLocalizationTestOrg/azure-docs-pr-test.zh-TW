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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-from-azure"></a>如何為語音和簡訊功能，從 Azure toouse Twilio
本指南示範如何 tooperform 常見的程式設計工作以 hello Twilio API 服務在 Azure 上。 涵蓋的 hello 案例包括撥電話及傳送短訊息服務 (SMS) 訊息。 如需有關 Twilio 和您的應用程式中使用語音和 SMS 的詳細資訊，請參閱 hello[後續步驟](#NextSteps)> 一節。

## <a id="WhatIs"></a>什麼是 Twilio？
Twilio 是及支援的業務通訊的 hello 未來、 啟用開發人員 tooembed 語音 VoIP 及訊息加入應用程式。 這些虛擬化在雲端為基礎、 全域環境中，公開透過 hello Twilio 通訊 API 平台所需的所有基礎結構。 應用程式是簡單 toobuild 及擴充。 享受隨收隨付定價的彈性和雲端可靠性的好處。

**Twilio 語音**可讓您的應用程式 toomake 撥打與接聽電話。 **Twilio SMS**可讓您的應用程式 toosend 和接收 SMS 訊息。 **Twilio 用戶端**可讓您從任何電話、 平板電腦或瀏覽器 toomake VoIP 呼叫，並支援 WebRTC。

## <a id="Pricing"></a>Twilio 定價和特別優惠
升級 Twilio 帳戶的 Azure 客戶，可[特別獲贈](http://www.twilio.com/azure)價值 $10 的 Twilio 點數。 此 Twilio 信用額度可以套用的 tooany Twilio 使用量 ($10 信用相等 toosending 多達 1000 SMS 訊息或接收向上 too1000 輸入語音分鐘，視您的電話號碼和訊息或呼叫目的地的 hello 位置而定)。 請至 [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure) 兌換 Twilio 點數來開始使用。

Twilio 是隨收隨付的服務。 不需要設定費，隨時都可結清帳戶。 如需詳細資訊，請參閱 [Twilio 價格](http://www.twilio.com/voice/pricing)。

## <a id="Concepts"></a>概念
hello Twilio API 是 rest 式 API，應用程式提供語音和 SMS 功能。 用戶端程式庫有多種語言版本，相關清單請參閱 [Twilio API 程式庫][twilio_libraries]。

Hello Twilio API 的重要層面是 Twilio 動詞和 Twilio 標記語言 (TwiML)。

### <a id="Verbs"></a>Twilio 動詞
hello API 會使用 Twilio 動詞命令。例如，hello **&lt;說&gt;**動詞命令會指示 Twilio tooaudibly 傳遞的訊息上呼叫。

hello 如下的 Twilio 指令動詞的清單。  深入了解 hello 其他動詞命令和功能，透過[Twilio 標記語言的文件](http://www.twilio.com/docs/api/twiml)。

* **&lt;撥號&gt;**： 連接 hello 呼叫端 tooanother 電話。
* **&lt;收集&gt;**： 會收集輸入 hello 電話字鍵台上的數字。
* **&lt;掛斷&gt;**：結束通話。
* **&lt;播放&gt;**：播放音訊檔案。
* **&lt;暫停&gt;**：靜候一段指定的秒數。
* **&lt;記錄&gt;**： 記錄 hello 呼叫者的語音，並傳回包含 hello 記錄檔的 URL。
* **&lt;重新導向&gt;**： 控制權的通話或 SMS toohello TwiML 於不同的 URL。
* **&lt;拒絕&gt;**： 拒絕傳入的呼叫未使用計費您 tooyour Twilio 數目
* **&lt;說出&gt;**： 將文字 toospeech 所做的呼叫上。
* **&lt;Sms&gt;**：傳送簡訊。

### <a id="TwiML"></a>TwiML
TwiML 是以 XML 為基礎的指示，就會通知方式的 Twilio hello Twilio 動詞命令為基礎的一組 tooprocess 通話或 SMS。

例如，下列 TwiML hello 將轉換的 hello 文字**Hello World** toospeech。

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

當您的應用程式呼叫 hello Twilio 應用程式開發介面時，其中 hello API 參數會是傳回 hello TwiML 回應 hello URL。 供開發應用程式，您可以使用您的應用程式所使用的 Twilio 提供 Url tooprovide hello TwiML 回應。 您也可以裝載自己 Url tooproduce hello TwiML 回應，和另一個選項是 toouse hello **TwiMLResponse**物件。

如需 Twilio 動詞、屬性和 TwiML 的詳細資訊，請參閱 [TwiML][twiml]。 如需 hello Twilio API 的詳細資訊，請參閱[Twilio API][twilio_api]。

## <a id="CreateAccount"></a>建立 Twilio 帳戶
當你準備好 tooget Twilio 帳戶時，請在註冊[再試一次 Twilio][try_twilio]。 您可以先使用免費帳戶，稍後再升級帳戶。

註冊 Twilio 帳戶時，您會收到帳戶識別碼和驗證權杖。 同時會為所需的 toomake Twilio API 呼叫。 tooprevent 未經授權存取 tooyour 帳戶，讓驗證權杖的安全。 您的帳戶識別碼和驗證權杖皆可檢視在 hello [Twilio 帳戶 頁面上][twilio_account]，請在 hello 欄位標示為**帳戶 SID**和**驗證語彙基元**分別。

## <a id="create_app"></a>建立 Azure 應用程式
裝載已啟用 Twilio 功能之應用程式的 Azure 應用程式，與其他任何 Azure 應用程式並無不同。 您加入 hello Twilio.NET 程式庫，並設定 hello 角色 toouse hello Twilio.NET 程式庫。
如需有關建立初始 Azure 專案的詳細資訊，請參閱[使用 Visual Studio 建立 Azure 專案][vs_project]。

## <a id="configure_app"></a>設定您的應用程式 toouse Twilio 文件庫
Twilio 提供一組.NET 協助程式程式庫包裝 Twilio tooprovide 簡單且簡單的方式 toointeract hello Twilio REST API 與 Twilio 用戶端的各種層面的 toogenerate TwiML 回應。

Twilio 為 .NET 開發人員提供五套程式庫：
程式庫|說明
---|---
Twilio.API|hello 核心 Twilio 程式庫包裝易記的.NET 程式庫中的 hello Twilio REST API。 此程式庫適用於 .NET、Silverlight 和 Windows Phone 7。
Twilio.TwiML|提供.NET 易懂的方式 toogenerate TwiML 標記。
Twilio.MVC|對於使用 ASP.NET MVC 的開發人員，此程式庫包含 TwilioController、TwiML ActionResult 和要求驗證屬性。
Twilio.WebMatrix|對於使用 Microsoft 免費 WebMatrix 開發工具的開發人員，此程式庫包含各種 Twilio 動作的 Razor 語法協助程式。
Twilio.Client.Capability|包含與 hello Twilio 用戶端 JavaScript SDK 搭配使用的 hello 功能權杖產生器。

請注意，所有程式庫都需要有 .NET 3.5、Silverlight 4 或 Windows Phone 7 或更新版本。

本指南中提供的 hello 範例使用 hello Twilio.API 程式庫。

hello 媒體櫃可以是[使用 hello NuGet 套件管理員擴充功能安裝](http://www.twilio.com/docs/csharp/install)向上 too2015 適用於 Visual Studio 2010。  hello 原始程式碼位於[GitHub][twilio_github_repo]，其中包括 Wiki，其中包含完整的文件以 hello 文件庫。

依預設，Microsoft Visual Studio 2010 會安裝 NuGet 1.2 版。 安裝 hello Twilio 程式庫需要 1.6 版或更高版本的 NuGet。 如需有關安裝或更新 NuGet 的詳細資訊，請參閱 [http://nuget.org/][nuget]。

> [!NOTE]
> tooinstall hello 最新的 NuGet 版本，您必須先解除安裝使用 Visual Studio 擴充功能管理員 hello hello 載入的版本。 toodo 因此，您必須以系統管理員身分執行 Visual Studio。 否則，會停用 hello 解除安裝 按鈕。
>
>

### <a id="use_nuget"></a>tooadd hello Twilio 文件庫 tooyour Visual Studio 專案：
1. 在 Visual Studio 中開啟方案。
2. 以滑鼠右鍵按一下 [參考]。
3. 按一下 [管理 NuGet 套件...]
4. 按一下 [線上] 。
5. 在 hello 搜尋線上方塊中，輸入*twilio*。
6. 按一下**安裝**hello Twilio 封裝上。

## <a id="howto_make_call"></a>作法：撥出電話
hello 下列範例示範如何 toomake 傳出呼叫使用 hello **CallResource**類別。 此程式碼也會使用 Twilio 提供站台 tooreturn hello Twilio 標記語言 (TwiML) 回應。 替換為您的值為 hello**至**和**從**電話號碼，並確保您確認 hello**從**執行 hello 程式碼前電話 Twilio 帳戶的號碼。

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

如需有關 hello 參數傳入 toohello **CallResource.Create**方法，請參閱[http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls]。

如前所述，此程式碼會使用 Twilio 提供站台 tooreturn hello TwiML 回應。 您可以改為使用您自己的站台 tooprovide hello TwiML 回應。 如需詳細資訊，請參閱[如何：從您自己的網站提供 TwiML 回應](#howto_provide_twiml_responses)。

## <a id="howto_send_sms"></a>作法：傳送簡訊
hello 下列螢幕擷取畫面顯示如何 toosend SMS 訊息使用 hello **MessageResource**類別。 hello**從**數目由 Twilio 為試用版帳戶 toosend SMS 訊息。 hello**至**數目必須驗證您 Twilio 帳戶的執行 hello 程式碼。

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

## <a id="howto_provide_twiml_responses"></a>作法：從您自己的網站提供 TwiML 回應
當您的應用程式起始呼叫 toohello Twilio API-例如，透過 hello **CallResource.Create**方法-Twilio 傳送您的要求 tooan URL 所預期的 tooreturn TwiML 回應。 中的 hello 範例[如何： 進行傳出呼叫](#howto_make_call)使用 hello Twilio 提供 URL [http://twimlets.com/message] [ twimlet_message_url] tooreturn hello 回應。

> [!NOTE]
> 雖然 TwiML 設計為使用 web 服務，您可以檢視 hello TwiML 瀏覽器中。 例如，按一下[http://twimlets.com/message] [ twimlet_message_url] toosee 空&lt;回應&gt;項目，另一個範例中，按一下 [ [http://twimlets.com/message?訊息 %5B0 %5 D = Hello %20world](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee&lt;回應&gt;包含項目&lt;說&gt;項目。
>
>

而不是依賴 hello Twilio 提供 URL，您可以建立您自己會傳回 HTTP 回應的 URL 站台。 您可以建立 hello 站台會傳回 HTTP 回應的任何語言。 本主題假設您要主控 hello 從 ASP.NET 泛型處理常式的 URL。

下列 ASP.NET 處理常式的 hello 花瓶 TwiML 回應指出**Hello World** hello 呼叫。

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
    
您可以看到從 hello 上述範例中，hello TwiML 回應是只是 XML 文件。 hello Twilio.TwiML 程式庫包含類別，會為您產生 TwiML。 hello 下面範例會產生 hello 相等回應，如上所示，但使用 hello **VoiceResponse**類別。

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

如需 TwiML 的詳細資訊，請參閱 [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml)。

一旦您已設定的方式 tooprovide TwiML 回應，您可以傳遞該 URL toohello **CallResource.Create**方法。 例如，如果您為部署 MyTwiML tooan Azure 雲端服務的 web 應用程式，而且 hello ASP.NET 處理常式名稱是 mytwiml.ashx，hello URL 可以傳遞太**CallResource.Create** hello 下列程式碼所示範例：

    // This sample uses hello sandbox number provided by Twilio toomake hello call.
    // Place hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

如需有關使用 ASP.NET 在 Azure 上使用 Twilio 的詳細資訊，請參閱[如何 toomake 電話呼叫在 Azure 上的 web 角色中使用 Twilio][howto_phonecall_dotnet]。

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
