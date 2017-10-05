---
title: "Azure Functions SendGrid 繫結 | Microsoft Docs"
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
ms.openlocfilehash: 445a40a884e648cdb2a57f8ef43bed4f8a3efcf2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-sendgrid-bindings"></a><span data-ttu-id="04efb-103">Azure Functions SendGrid 繫結</span><span class="sxs-lookup"><span data-stu-id="04efb-103">Azure Functions SendGrid bindings</span></span>

<span data-ttu-id="04efb-104">此文章說明如何在 Azure Functions 中設定及使用 SendGrid 繫結。</span><span class="sxs-lookup"><span data-stu-id="04efb-104">This article explains how to configure and work with SendGrid bindings in Azure Functions.</span></span> <span data-ttu-id="04efb-105">透過 SendGrid，您可以使用 Azure Functions 以程式設計方式傳送自訂的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="04efb-105">With SendGrid, you can use Azure Functions to send customized email programmatically.</span></span>

<span data-ttu-id="04efb-106">此文章是適用於 Azure Functions 開發人員的參考資訊。</span><span class="sxs-lookup"><span data-stu-id="04efb-106">This article is reference information for Azure Functions developers.</span></span> <span data-ttu-id="04efb-107">如果您不熟悉 Azure Functions，請從下列資源開始︰</span><span class="sxs-lookup"><span data-stu-id="04efb-107">If you're new to Azure Functions, start with the following resources:</span></span>

<span data-ttu-id="04efb-108">[建立您的第一個 Azure 函式](functions-create-first-azure-function.md)。</span><span class="sxs-lookup"><span data-stu-id="04efb-108">[Create your first Azure Function](functions-create-first-azure-function.md).</span></span> 
<span data-ttu-id="04efb-109">[C#](functions-reference-csharp.md)、[F#](functions-reference-fsharp.md) 或 [Node](functions-reference-node.md) 開發人員參考。</span><span class="sxs-lookup"><span data-stu-id="04efb-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md), or [Node](functions-reference-node.md) developer references.</span></span>

## <a name="functionjson-for-sendgrid-bindings"></a><span data-ttu-id="04efb-110">適用於 SendGrid 繫結的 function.json</span><span class="sxs-lookup"><span data-stu-id="04efb-110">function.json for SendGrid bindings</span></span>

<span data-ttu-id="04efb-111">Azure Functions 提供適用於 SendGrid 的輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="04efb-111">Azure Functions provides an output binding for SendGrid.</span></span> <span data-ttu-id="04efb-112">SendGrid 輸出繫結可讓您以程式設計方式建立並傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="04efb-112">The SendGrid output binding enables you to create and send email programmatically.</span></span> 

<span data-ttu-id="04efb-113">SendGrid 繫結支援下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="04efb-113">The SendGrid binding supports the following properties:</span></span>

- <span data-ttu-id="04efb-114">`name`：必要項目 - 函式程式碼中用於要求或要求主體的變數名稱。</span><span class="sxs-lookup"><span data-stu-id="04efb-114">`name` : Required - the variable name used in function code for the request or request body.</span></span> <span data-ttu-id="04efb-115">當只有一個傳回值時，此值為 ```$return```。</span><span class="sxs-lookup"><span data-stu-id="04efb-115">This value is ```$return``` when there is only one return value.</span></span> 
- <span data-ttu-id="04efb-116">`type`：必要項目 - 必須設定為 "sendGrid"。</span><span class="sxs-lookup"><span data-stu-id="04efb-116">`type` : Required - must be set to "sendGrid."</span></span>
- <span data-ttu-id="04efb-117">`direction`：必要項目 - 必須設定為 "out"。</span><span class="sxs-lookup"><span data-stu-id="04efb-117">`direction` : Required - must be set to "out."</span></span>
- <span data-ttu-id="04efb-118">`apiKey`：必要項目 - 必須設定為函數應用程式的應用程式設定中儲存的 API 金鑰名稱。</span><span class="sxs-lookup"><span data-stu-id="04efb-118">`apiKey` : Required - must be set to the name of your API key stored in the Function App's app settings.</span></span>
- <span data-ttu-id="04efb-119">`to`：收件者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="04efb-119">`to` : the recipient's email address.</span></span>
- <span data-ttu-id="04efb-120">`from`：寄件者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="04efb-120">`from` : the sender's email address.</span></span>
- <span data-ttu-id="04efb-121">`subject`：電子郵件主旨。</span><span class="sxs-lookup"><span data-stu-id="04efb-121">`subject` : the subject of the email.</span></span>
- <span data-ttu-id="04efb-122">`text`：電子郵件內容。</span><span class="sxs-lookup"><span data-stu-id="04efb-122">`text` : the email content.</span></span>

<span data-ttu-id="04efb-123">**function.json** 範例：</span><span class="sxs-lookup"><span data-stu-id="04efb-123">Example of **function.json**:</span></span>

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
> <span data-ttu-id="04efb-124">Azure Functions 將會您的連接資訊和 API 金鑰儲存為應用程式設定，使得不會將讓它們簽入至您的原始檔控制儲存機制。</span><span class="sxs-lookup"><span data-stu-id="04efb-124">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="04efb-125">這個動作會保護您的機密資訊。</span><span class="sxs-lookup"><span data-stu-id="04efb-125">This action safeguards your sensitive information.</span></span>
>
>

## <a name="c-example-of-the-sendgrid-output-binding"></a><span data-ttu-id="04efb-126">SendGrid 輸出繫結的 C# 範例</span><span class="sxs-lookup"><span data-stu-id="04efb-126">C# example of the SendGrid output binding</span></span>

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

## <a name="node-example-of-the-sendgrid-output-binding"></a><span data-ttu-id="04efb-127">SendGrid 輸出繫結的 Node 範例</span><span class="sxs-lookup"><span data-stu-id="04efb-127">Node example of the SendGrid output binding</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="04efb-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="04efb-128">Next steps</span></span>
<span data-ttu-id="04efb-129">如需 Azure Functions 其他繫結與觸發程序的相關資訊，請參閱</span><span class="sxs-lookup"><span data-stu-id="04efb-129">For information about other bindings and triggers for Azure Functions, see</span></span> 
- [<span data-ttu-id="04efb-130">Azure Functions 觸發程序和繫結開發人員參考</span><span class="sxs-lookup"><span data-stu-id="04efb-130">Azure Functions triggers and bindings developer reference</span></span>](functions-triggers-bindings.md)

- <span data-ttu-id="04efb-131">[Azure Functions 的最佳做法](functions-best-practices.md)列出建立 Azure 函式時可採用的一些最佳做法。</span><span class="sxs-lookup"><span data-stu-id="04efb-131">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices to use when creating Azure Functions.</span></span>

- <span data-ttu-id="04efb-132">[Azure Functions 開發人員參考](functions-reference.md) 可供程式設計人員撰寫函式及定義觸發程序和繫結時參考。</span><span class="sxs-lookup"><span data-stu-id="04efb-132">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>
