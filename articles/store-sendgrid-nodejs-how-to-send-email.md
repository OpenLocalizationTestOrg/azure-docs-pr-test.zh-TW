---
title: "aaaHow toouse hello SendGrid 電子郵件服務 (Node.js) |Microsoft 文件"
description: "深入了解如何在 Azure 上傳送電子郵件以 hello SendGrid 電子郵件服務。 程式碼使用 hello Node.js 應用程式開發介面撰寫的範例。"
services: 
documentationcenter: nodejs
author: erikre
manager: wpickett
editor: 
ms.assetid: cac444b4-26b0-45ea-9c3d-eca28d57dacb
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 01/05/2016
ms.author: erikre
ms.openlocfilehash: fd617b6aaa656e7b5dd51c51ebb0db1e848450f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-nodejs"></a>如何 tooSend 電子郵件使用 SendGrid 從 Node.js
本指南示範如何 tooperform 常見的程式設計工作使用 SendGrid 傳送電子郵件在 Azure 上的服務。 使用 hello Node.js 應用程式開發介面撰寫 hello 範例。 hello 涵蓋案例包括**建構電子郵件**，**傳送電子郵件**，**加入附件**，**使用篩選器**，和**更新屬性**。 如需有關 SendGrid 和傳送電子郵件的詳細資訊，請參閱 hello[接下來的步驟](#next-steps)> 一節。

## <a name="what-is-hello-sendgrid-email-service"></a>什麼是 hello SendGrid 電子郵件服務？
SendGrid 是 [雲端架構電子郵件服務]，能提供可靠的 [交易式電子郵件傳遞]、擴充性和即時分析，以及有彈性的 API 來輕鬆進行自訂整合。 常見的 SendGrid 使用案例包括：

* 自動將資料傳送回條 toocustomers
* 管理通訊群組清單，以便將每月電子傳單和特別優惠傳送給客戶
* 收集封鎖的電子郵件、客戶的回應情形等項目的即時度量
* 產生 toohelp 識別趨勢的報表
* 轉寄客戶查詢
* 透過電子郵件從您的應用程式傳送通知

如需詳細資訊，請參閱 [https://sendgrid.com](https://sendgrid.com)。

## <a name="create-a-sendgrid-account"></a>建立 SendGrid 帳戶
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-nodejs-module"></a>參考 hello SendGrid Node.js 模組
可以使用下列命令的 hello，透過 hello node 封裝管理員 (npm) 安裝 Node.js 的 hello SendGrid 模組：

    npm install sendgrid

安裝之後，您可以使用下列程式碼的 hello hello 模組要求應用程式中：

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

hello SendGrid 模組匯出的 hello **SendGrid**和**電子郵件**函式。
**SendGrid** 負責透過 Web API 傳送電子郵件，而 **Email** 則負責封裝電子郵件訊息。

## <a name="how-to-create-an-email"></a>如何：建立電子郵件
建立電子郵件訊息使用 hello SendGrid 模組包括第一次建立 hello 電子郵件，使用函式，然後將它使用 hello SendGrid 函式傳送的電子郵件訊息。 hello 以下是建立新的訊息使用 hello 電子郵件函式的範例：

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

您也可以指定 HTML 訊息之用戶端的支援設定 hello html 屬性。 例如：

    html: This is a sample <b>HTML<b> email message.

設定這兩個的 hello 文字和 html 屬性不支援 HTML 郵件用戶端提供依正常程序到文字內容的後援。

如需有關 hello 電子郵件函式所支援的所有屬性的詳細資訊，請參閱[sendgrid nodejs][sendgrid-nodejs]。

## <a name="how-to-send-an-email"></a>如何：傳送電子郵件
在建立之後使用 hello 電子郵件函式的電子郵件訊息，您可以傳送 hello SendGrid 所提供的 Web API 的使用。 

### <a name="web-api"></a>Web API
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> 雖然 hello 上述範例會顯示在電子郵件物件和回呼函式傳遞，您可以也會直接叫用 hello 傳送函式直接指定電子郵件內容。 例如：  
> 
> `````
> sendgrid.send({
> to: 'john@contoso.com',
> from: 'anna@contoso.com',
> subject: 'test mail',
> text: 'This is a sample email message.'
> });
> `````
> 
> 

## <a name="how-to-add-an-attachment"></a>如何：新增附件
附件可以指定 hello 檔案名稱和路徑在 hello 新增 tooa 訊息**檔案**屬性。 下列範例中的 hello 示範傳送附件：

    sendgrid.send({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.',
        files: [
            {
                filename:     '',           // required only if file.content is used.
                contentType:  '',           // optional
                cid:          '',           // optional, used toospecify cid for inline content
                path:         '',           //
                url:          '',           // == One of these three options is required
                content:      ('' | Buffer) //
            }
        ],
    });

> [!NOTE]
> 當使用 hello**檔案**屬性，hello 檔案必須可透過存取[fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile)。 如果您想 tooattach hello 檔案裝載在 Azure 儲存體，例如 Blob 容器，您必須先將 hello 檔案 toolocal 儲存體或 Azure 磁碟機 tooan 使用 hello 附件形式傳送之前**檔案**屬性。
> 
> 

## <a name="how-to-use-filters-tooenable-footers-and-tracking"></a>如何： 使用篩選器 tooEnable 頁尾和追蹤
SendGrid 提供其他電子郵件功能，透過 hello 使用篩選條件。 這些是可以加入 tooan 電子郵件訊息，若要啟用特定的功能，例如啟用點選追蹤、 Google analytics、 追蹤、 訂用帳戶的設定，依此類推。 如需完整的篩選器清單，請參閱[篩選器設定][Filter Settings]。

篩選可套用的 tooa 訊息使用 hello**篩選**屬性。
每個篩選器都是由包含篩選器特定設定的雜湊來指定。
hello 下列範例示範 hello 頁尾，並按一下 追蹤篩選器：

### <a name="footer"></a>頁尾
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'footer': {
            'settings': {
                'enable': 1,
                'text/plain': 'This is a text footer.'
            }
        }
    });

    sendgrid.send(email);

### <a name="click-tracking"></a>點選追蹤
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'clicktrack': {
            'settings': {
                'enable': 1
            }
        }
    });

    sendgrid.send(email);

## <a name="how-to-update-email-properties"></a>如何：更新電子郵件屬性
某些電子郵件內容會被覆寫使用**設定*屬性** * 或附加**新增*屬性** *。 例如，您可以使用下列方式新增其他收件者：

    email.addTo('jeff@contoso.com');

或使用下列方式設定篩選器：

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

如需詳細資訊，請參閱[sendgrid nodejs][sendgrid-nodejs]。

## <a name="how-to-use-additional-sendgrid-services"></a>如何：使用其他 SendGrid 服務
SendGrid 提供網頁型應用程式開發介面，您可以從 Azure 應用程式使用 tooleverage 其他 SendGrid 功能。 完整的詳細資訊，請參閱 hello [SendGrid API 文件][SendGrid API documentation]。

## <a name="next-steps"></a>後續步驟
既然您已經學會 hello 的 hello SendGrid 電子郵件服務的基本概念，請遵循這些連結 toolearn 更多。

* SendGrid Node.js 模組存放庫： [sendgrid nodejs][sendgrid-nodejs]
* SendGrid API 文件︰<https://sendgrid.com/docs>
* Azure 客戶的 SendGrid 特別優惠：[http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
[雲端架構電子郵件服務]: https://sendgrid.com/email-solutions
[交易式電子郵件傳遞]: https://sendgrid.com/transactional-email
