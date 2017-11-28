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
# <a name="azure-functions-sendgrid-bindings"></a><span data-ttu-id="e011e-103">Azure Functions SendGrid 繫結</span><span class="sxs-lookup"><span data-stu-id="e011e-103">Azure Functions SendGrid bindings</span></span>

<span data-ttu-id="e011e-104">這篇文章說明如何 tooconfigure 地使用 SendGrid Azure 函式中的繫結。</span><span class="sxs-lookup"><span data-stu-id="e011e-104">This article explains how tooconfigure and work with SendGrid bindings in Azure Functions.</span></span> <span data-ttu-id="e011e-105">SendGrid，您可以使用 Azure 函式 toosend 自訂電子郵件以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="e011e-105">With SendGrid, you can use Azure Functions toosend customized email programmatically.</span></span>

<span data-ttu-id="e011e-106">此文章是適用於 Azure Functions 開發人員的參考資訊。</span><span class="sxs-lookup"><span data-stu-id="e011e-106">This article is reference information for Azure Functions developers.</span></span> <span data-ttu-id="e011e-107">如果您是新 tooAzure 函式時，啟動以 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="e011e-107">If you're new tooAzure Functions, start with hello following resources:</span></span>

<span data-ttu-id="e011e-108">[建立您的第一個 Azure 函式](functions-create-first-azure-function.md)。</span><span class="sxs-lookup"><span data-stu-id="e011e-108">[Create your first Azure Function](functions-create-first-azure-function.md).</span></span> 
<span data-ttu-id="e011e-109">[C#](functions-reference-csharp.md)、[F#](functions-reference-fsharp.md) 或 [Node](functions-reference-node.md) 開發人員參考。</span><span class="sxs-lookup"><span data-stu-id="e011e-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md), or [Node](functions-reference-node.md) developer references.</span></span>

## <a name="functionjson-for-sendgrid-bindings"></a><span data-ttu-id="e011e-110">適用於 SendGrid 繫結的 function.json</span><span class="sxs-lookup"><span data-stu-id="e011e-110">function.json for SendGrid bindings</span></span>

<span data-ttu-id="e011e-111">Azure Functions 提供適用於 SendGrid 的輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="e011e-111">Azure Functions provides an output binding for SendGrid.</span></span> <span data-ttu-id="e011e-112">hello SendGrid 輸出繫結可讓您 toocreate 及傳送電子郵件以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="e011e-112">hello SendGrid output binding enables you toocreate and send email programmatically.</span></span> 

<span data-ttu-id="e011e-113">hello SendGrid 繫結支援下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="e011e-113">hello SendGrid binding supports hello following properties:</span></span>

- <span data-ttu-id="e011e-114">`name`： 需要-hello hello 要求或要求主體函式程式碼中使用的變數名稱。</span><span class="sxs-lookup"><span data-stu-id="e011e-114">`name` : Required - hello variable name used in function code for hello request or request body.</span></span> <span data-ttu-id="e011e-115">當只有一個傳回值時，此值為 ```$return```。</span><span class="sxs-lookup"><span data-stu-id="e011e-115">This value is ```$return``` when there is only one return value.</span></span> 
- <span data-ttu-id="e011e-116">`type`： 需要-必須設定太"sendGrid。 」</span><span class="sxs-lookup"><span data-stu-id="e011e-116">`type` : Required - must be set too"sendGrid."</span></span>
- <span data-ttu-id="e011e-117">`direction`： 需要-必須設定太"out"。</span><span class="sxs-lookup"><span data-stu-id="e011e-117">`direction` : Required - must be set too"out."</span></span>
- <span data-ttu-id="e011e-118">`apiKey`： 需要-必須是組 toohello hello 函式應用程式的應用程式設定中儲存您的 API 金鑰名稱。</span><span class="sxs-lookup"><span data-stu-id="e011e-118">`apiKey` : Required - must be set toohello name of your API key stored in hello Function App's app settings.</span></span>
- <span data-ttu-id="e011e-119">`to`: hello 收件者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="e011e-119">`to` : hello recipient's email address.</span></span>
- <span data-ttu-id="e011e-120">`from`: hello 寄件者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="e011e-120">`from` : hello sender's email address.</span></span>
- <span data-ttu-id="e011e-121">`subject`: hello hello 電子郵件主旨。</span><span class="sxs-lookup"><span data-stu-id="e011e-121">`subject` : hello subject of hello email.</span></span>
- <span data-ttu-id="e011e-122">`text`: hello 電子郵件內容。</span><span class="sxs-lookup"><span data-stu-id="e011e-122">`text` : hello email content.</span></span>

<span data-ttu-id="e011e-123">**function.json** 範例：</span><span class="sxs-lookup"><span data-stu-id="e011e-123">Example of **function.json**:</span></span>

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
> <span data-ttu-id="e011e-124">Azure Functions 將會您的連接資訊和 API 金鑰儲存為應用程式設定，使得不會將讓它們簽入至您的原始檔控制儲存機制。</span><span class="sxs-lookup"><span data-stu-id="e011e-124">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="e011e-125">這個動作會保護您的機密資訊。</span><span class="sxs-lookup"><span data-stu-id="e011e-125">This action safeguards your sensitive information.</span></span>
>
>

## <a name="c-example-of-hello-sendgrid-output-binding"></a><span data-ttu-id="e011e-126">C# 範例 hello SendGrid 的輸出繫結</span><span class="sxs-lookup"><span data-stu-id="e011e-126">C# example of hello SendGrid output binding</span></span>

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

## <a name="node-example-of-hello-sendgrid-output-binding"></a><span data-ttu-id="e011e-127">節點範例中的 hello SendGrid 輸出繫結</span><span class="sxs-lookup"><span data-stu-id="e011e-127">Node example of hello SendGrid output binding</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e011e-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e011e-128">Next steps</span></span>
<span data-ttu-id="e011e-129">如需 Azure Functions 其他繫結與觸發程序的相關資訊，請參閱</span><span class="sxs-lookup"><span data-stu-id="e011e-129">For information about other bindings and triggers for Azure Functions, see</span></span> 
- [<span data-ttu-id="e011e-130">Azure Functions 觸發程序和繫結開發人員參考</span><span class="sxs-lookup"><span data-stu-id="e011e-130">Azure Functions triggers and bindings developer reference</span></span>](functions-triggers-bindings.md)

- <span data-ttu-id="e011e-131">[Azure 函式的最佳作法](functions-best-practices.md)列出一些最佳作法 toouse 時建立 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="e011e-131">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices toouse when creating Azure Functions.</span></span>

- <span data-ttu-id="e011e-132">[Azure Functions 開發人員參考](functions-reference.md) 可供程式設計人員撰寫函式及定義觸發程序和繫結時參考。</span><span class="sxs-lookup"><span data-stu-id="e011e-132">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>
