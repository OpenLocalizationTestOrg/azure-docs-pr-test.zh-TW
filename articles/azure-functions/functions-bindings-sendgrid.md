---
title: "aaaAzure SendGrid 函式繫結 |Microsoft 文件"
description: "Azure Functions SendGrid 繫結參考"
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/16/2017
ms.author: rachelap
ms.openlocfilehash: 10a3837875eb6ae18e6c789bcf64cc401cf5f26a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-sendgrid-bindings"></a>Azure Functions SendGrid 繫結

這篇文章說明如何 tooconfigure 地使用 SendGrid Azure 函式中的繫結。 SendGrid，您可以使用 Azure 函式 toosend 自訂電子郵件以程式設計的方式。

此文章是適用於 Azure Functions 開發人員的參考資訊。 如果您是新 tooAzure 函式時，啟動以 hello 下列資源：

[建立您的第一個 Azure 函式](functions-create-first-azure-function.md)。 
[C#](functions-reference-csharp.md)、[F#](functions-reference-fsharp.md) 或 [Node](functions-reference-node.md) 開發人員參考。

## <a name="functionjson-for-sendgrid-bindings"></a>適用於 SendGrid 繫結的 function.json

Azure Functions 提供適用於 SendGrid 的輸出繫結。 hello SendGrid 輸出繫結可讓您 toocreate 及傳送電子郵件以程式設計的方式。 

hello SendGrid 繫結支援下列屬性的 hello:

- `name`： 需要-hello hello 要求或要求主體函式程式碼中使用的變數名稱。 當只有一個傳回值時，此值為 ```$return```。 
- `type`： 需要-必須設定太"sendGrid。 」
- `direction`： 需要-必須設定太"out"。
- `apiKey`： 需要-必須是組 toohello hello 函式應用程式的應用程式設定中儲存您的 API 金鑰名稱。
- `to`: hello 收件者的電子郵件地址。
- `from`: hello 寄件者的電子郵件地址。
- `subject`: hello hello 電子郵件主旨。
- `text`: hello 電子郵件內容。

**function.json** 範例：

```json 
{
    "bindings": [
        {
            "name": "$return",
            "type": "sendGrid",
            "direction": "out",
            "apiKey" : "MySendGridKey",
            "to": "{ToEmail}",
            "from": "{FromEmail}",
            "subject": "SendGrid output bindings"
        }
    ]
}
```

> [!NOTE]
> Azure Functions 將會您的連接資訊和 API 金鑰儲存為應用程式設定，使得不會將讓它們簽入至您的原始檔控制儲存機制。 這個動作會保護您的機密資訊。
>
>

## <a name="c-example-of-hello-sendgrid-output-binding"></a>C# 範例 hello SendGrid 的輸出繫結

```csharp
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static Mail Run(TraceWriter log, string input, out Mail message)
{
     message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    personalization.AddTo(new Email("recipient@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

## <a name="node-example-of-hello-sendgrid-output-binding"></a>節點範例中的 hello SendGrid 輸出繫結

```javascript
module.exports = function (context, input) {    
    var message = {
         "personalizations": [ { "to": [ { "email": "sample@sample.com" } ] } ],
        from: "sender@contoso.com",        
        subject: "Azure news",
        content: [{
            type: 'text/plain',
            value: input
        }]
    };

    context.done(null, message);
};

```

## <a name="next-steps"></a>後續步驟
如需 Azure Functions 其他繫結與觸發程序的相關資訊，請參閱 
- [Azure Functions 觸發程序和繫結開發人員參考](functions-triggers-bindings.md)

- [Azure 函式的最佳作法](functions-best-practices.md)列出一些最佳作法 toouse 時建立 Azure 函式。

- [Azure Functions 開發人員參考](functions-reference.md) 可供程式設計人員撰寫函式及定義觸發程序和繫結時參考。
