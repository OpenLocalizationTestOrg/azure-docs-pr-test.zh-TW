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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-ruby"></a>如何為語音和簡訊功能中 Ruby Twilio tooUse
本指南示範如何 tooperform 常見的程式設計工作以 hello Twilio API 服務在 Azure 上。 涵蓋的 hello 案例包括撥電話及傳送短訊息服務 (SMS) 訊息。 如需有關 Twilio 和您的應用程式中使用語音和 SMS 的詳細資訊，請參閱 hello[接下來的步驟](#NextSteps)> 一節。

## <a id="WhatIs"></a>什麼是 Twilio？
Twilio 是電話語音 web 服務 API，可讓您使用現有的 web 語言和技術 toobuild 語音和 SMS 應用程式。 Twilio 算是協力廠商服務 (並非 Azure 功能，也並非 Microsoft 產品)。

**Twilio 語音**可讓您的應用程式 toomake 撥打與接聽電話。 **Twilio SMS**可讓您的應用程式 toomake 和接收 SMS 訊息。 **Twilio 用戶端**tooenable 語音通訊使用現有的網際網路連線，包括行動裝置的連線，可讓您的應用程式。

## <a id="Pricing"></a>Twilio 定價和特別優惠
[Twilio 定價][twilio_pricing] (英文) 提供 Twilio 的定價資訊。 Azure 客戶可獲得[特殊優惠][special_offer]：免費 1000 則文字簡訊或接聽 1000 分鐘電話。 註冊這 toosign 提供或取得詳細資訊，請瀏覽[http://ahoy.twilio.com/azure][special_offer]。  

## <a id="Concepts"></a>概念
hello Twilio API 是 rest 式 API，應用程式提供語音和 SMS 功能。 用戶端程式庫有多種語言版本，相關清單請參閱 [Twilio API 程式庫][twilio_libraries]。

### <a id="TwiML"></a>TwiML
TwiML 是一組以 XML 為基礎的指示，就會通知方式的 Twilio tooprocess 通話或 SMS。

例如，下列 TwiML hello 將轉換的 hello 文字**Hello World** toospeech。

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

所有 TwiML 文件皆會以 `<Response>` 作為其根元素。 從該處，您可以使用 Twilio 動詞 toodefine hello 應用程式的行為。

### <a id="Verbs"></a>TwiML 動詞
Twilio 動詞命令是向 Twilio 說明過的 XML 標記**不要**。 例如，hello **&lt;說&gt;**動詞命令會指示 Twilio tooaudibly 傳遞的訊息上呼叫。 

hello 如下的 Twilio 指令動詞的清單。

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

如需 Twilio 動詞、屬性和 TwiML 的詳細資訊，請參閱 [TwiML][twiml]。 如需 hello Twilio API 的詳細資訊，請參閱[Twilio API][twilio_api]。

## <a id="CreateAccount"></a>建立 Twilio 帳戶
當你準備好 tooget Twilio 帳戶時，請在註冊[再試一次 Twilio][try_twilio]。 您可以先使用免費帳戶，稍後再升級帳戶。

註冊 Twilio 帳戶時，您會獲得可供應用程式使用的免費電話號碼。 您也會獲得帳戶 SID 和驗證權杖。 同時會為所需的 toomake Twilio API 呼叫。 tooprevent 未經授權存取 tooyour 帳戶，讓驗證權杖的安全。 您的帳戶 SID 和授權權杖皆可檢視在 hello [Twilio 帳戶 頁面上][twilio_account]，請在 hello 欄位標示為**帳戶 SID**和**驗證語彙基元**分別。

### <a id="VerifyPhoneNumbers"></a>驗證電話號碼
您也可以在您可以透過 Twilio 加法 toohello 數目、 確認用於控制 （也就是您的行動電話或家裡的電話號碼），在應用程式中的數字。 

如需詳細資訊 tooverify 電話號碼，請參閱[管理數字][verify_phone]。

## <a id="create_app"></a>建立 Ruby 應用程式
使用 hello Twilio 服務和 Azure 中執行的 Ruby 應用程式是與任何其他拼音使用服務應用程式 hello Twilio 沒什麼不同了。 雖然 Twilio 服務是 RESTful，且可從 Ruby 呼叫數種方式，本文將著重在 toouse Twilio 的服務使用[Twilio Ruby 的協助程式程式庫][twilio_ruby]。

首先，[安裝新的 Azure Linux VM] [ azure_vm_setup] tooact 做為新拼音 web 應用程式的主機。 忽略涉及 hello 滑軌應用程式，只要安裝 hello VM 建立 hello 步驟。 請確實建立具有外部連接埠 80 和內部連接埠 5000 的端點。

在 hello 下列範例中，我們將使用[Sinatra][sinatra]，Ruby 的非常簡單的 web 架構。 但是，您一定可以使用為 Ruby hello Twilio 協助程式程式庫，與任何其他 web 架構，包括在滑軌上的 Ruby。

在您新的 VM 中加入 SSH，並為新的應用程式建立目錄。 在該目錄中，建立檔案，稱為 Gemfile 並複製下列程式碼中的 hello:

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

Hello 命令列執行`bundle install`。 這會安裝上述 hello 相依性。 接著，建立名為 `web.rb`的檔案。 這會是所在 hello web 應用程式的程式碼。 貼上下列程式碼中的 hello:

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

此時您應該能夠執行的 hello hello 命令`ruby web.rb -p 5000`。 這會在連接埠 5000 上啟動小型 Web 伺服器。 您應該能夠 toobrowse toothis 應用程式在您的瀏覽器中造訪 hello URL 時所安裝的 Azure VM。 一旦可以達到 hello 瀏覽器中的 web 應用程式，您已準備好 toostart 建置 Twilio 應用程式。

## <a id="configure_app"></a>設定您的應用程式 tooUse Twilio
您可以設定您 web 應用程式 toouse hello Twilio 程式庫，藉由更新您`Gemfile`tooinclude 這一行：

    gem 'twilio-ruby'

在 hello 命令列上執行`bundle install`。 現在開啟`web.rb`，包括在 hello 頂端這一行：

    require 'twilio-ruby'

您現在需要設定所有 toouse hello Twilio 協助程式程式庫 Ruby web 應用程式中。

## <a id="howto_make_call"></a>作法：撥出電話
下列的 hello 會示範如何呼叫 toomake 傳出。 重要概念包括使用 REST API 呼叫的拼音 toomake hello Twilio 協助程式程式庫和轉譯 TwiML。 替換為您的值為 hello**從**和**至**電話號碼，並確保您確認 hello**從**電話號碼您 Twilio 帳戶先前 toorunning hello 撰寫程式碼。

新增此函式太`web.md`:

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

如果您開啟總`http://yourdomain.cloudapp.net/make_call`瀏覽器，就會觸發 hello 呼叫 toohello Twilio API toomake hello 電話通話。 hello 中的前兩個參數`client.account.calls.create`會均相當容易理解： hello 數字的 hello 呼叫`from`和數字 hello 呼叫 hello `to`。 

hello 第三個參數 (`url`) 是 hello Twilio 要求 tooget 指示哪些 toodo，一旦 hello 呼叫已連線的 URL。 在此情況下我們設定的 URL (`http://yourdomain.cloudapp.net`)，傳回簡單的 TwiML 文件，並使用 hello`<Say>`動詞 toodo 一些文字轉換語音和假設接收"Hello 猴子"toohello 人 hello 呼叫。

## <a id="howto_recieve_sms"></a>如何：接收 SMS 簡訊
Hello 前一個範例中我們起始**傳出**通話。 這個時間，我們將使用的 Twilio 給予我們期間註冊 tooprocess hello 電話號碼**傳入**SMS 訊息。

首先，登入 tooyour [Twilio 儀表板][twilio_account]。 按一下 「 號碼 」 中 hello 上層瀏覽，，然後按一下 hello Twilio 所提供的數字。 您會看見兩個可以設定的 URL。 語音要求 URL 和簡訊要求 URL。 這些是 hello Url 的 Twilio 電話時已呼叫或 SMS 傳送 tooyour 數目。 hello Url 也可稱為 「 web 勾點 」。

我們希望 tooprocess 傳入的 SMS 訊息，因此讓我們先更新 hello URL 太`http://yourdomain.cloudapp.net/sms_url`。 請繼續並按一下 在 hello hello 頁面底部的 儲存變更。 現在，回到`web.rb`我們這程式我們的應用程式 toohandle:

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for hello ping! Twilio and Azure rock!</Message>
       </Response>"
    end

Hello 變更後，請確定 toore 開始您的 web 應用程式。 現在，取出您的電話，並傳送 SMS tooyour Twilio 數目。 您應該立即取得 SMS 回應，指出 「 < Hey，hello ping 感謝您 ！ Twilio and Azure rock!"。

## <a id="additional_services"></a>如何：使用其他 Twilio 服務
此外 toohello 範例所示，Twilio 提供網頁型應用程式開發介面，您可以使用其他 Twilio 功能 tooleverage 從 Azure 應用程式。 完整的詳細資訊，請參閱 hello [Twilio API 文件][twilio_api_documentation]。

### <a id="NextSteps"></a>後續步驟
既然您已經學會 hello hello Twilio 服務基本概念，請依照下列多個這些連結 toolearn:

* [Twilio 安全性方針][twilio_security_guidelines]
* [Twilio 作法與範例程式碼][twilio_howtos]
* [Twilio 快速入門教學課程][twilio_quickstarts] 
* [GitHub 上的 Twilio][twilio_on_github]
* [Talk tooTwilio 支援][twilio_support]

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
