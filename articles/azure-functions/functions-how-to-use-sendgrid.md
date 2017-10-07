---
title: "aaaHow toouse Azure 函式中的 SendGrid |Microsoft 文件"
description: "示範如何 toouse SendGrid Azure 函式中"
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/31/2017
ms.author: rachelap
ms.openlocfilehash: a0ffdae04e5924c773d2d26427626fc1f570f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-sendgrid-in-azure-functions"></a><span data-ttu-id="e821e-103">如何 toouse SendGrid Azure 函式中</span><span class="sxs-lookup"><span data-stu-id="e821e-103">How toouse SendGrid in Azure Functions</span></span>

## <a name="sendgrid-overview"></a><span data-ttu-id="e821e-104">SendGrid 概觀</span><span class="sxs-lookup"><span data-stu-id="e821e-104">SendGrid Overview</span></span>

<span data-ttu-id="e821e-105">Azure 函式支援 SendGrid 輸出繫結 tooenable 幾行程式碼和 SendGrid 帳戶與您函式 toosend 電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="e821e-105">Azure Functions supports SendGrid output bindings tooenable your functions toosend email messages with a few lines of code and a SendGrid account.</span></span>

<span data-ttu-id="e821e-106">在 Azure 函式 toouse hello SendGrid API，您必須擁有[SendGrid 帳戶](http://SendGrid.com)。</span><span class="sxs-lookup"><span data-stu-id="e821e-106">toouse hello SendGrid API in an Azure Function, you must have a [SendGrid account](http://SendGrid.com).</span></span> <span data-ttu-id="e821e-107">此外，您還必須有 SendGrid API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="e821e-107">Additionally, you must have a SendGrid API Key.</span></span> <span data-ttu-id="e821e-108">登入 tooyour SendGrid 帳戶，然後按一下 **設定**然後**API 金鑰**toogenerate API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="e821e-108">Log in tooyour SendGrid account and click **Settings** then **API Key** toogenerate an API key.</span></span> <span data-ttu-id="e821e-109">請備妥此金鑰，在後續步驟中會用到。</span><span class="sxs-lookup"><span data-stu-id="e821e-109">Keep this key available as you use it in an upcoming step.</span></span>

<span data-ttu-id="e821e-110">現在您已經準備就緒 toocreate Azure 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="e821e-110">You are now ready toocreate an Azure Function app.</span></span>

## <a name="create-an-azure-function-app"></a><span data-ttu-id="e821e-111">建立 Azure 函數應用程式</span><span class="sxs-lookup"><span data-stu-id="e821e-111">Create an Azure Function app</span></span> 

<span data-ttu-id="e821e-112">Azure Functions 應用程式是一或多個 Azure 函式的容器。</span><span class="sxs-lookup"><span data-stu-id="e821e-112">Azure Function Apps are containers for one or more Azure functions.</span></span> <span data-ttu-id="e821e-113">Azure Functions 就只是函式。</span><span class="sxs-lookup"><span data-stu-id="e821e-113">Azure functions are just that - a function.</span></span> <span data-ttu-id="e821e-114">每個 Azure 函式是繫結的 tooone 觸發程序，這可能會導致 hello 函式 toorun 事件。</span><span class="sxs-lookup"><span data-stu-id="e821e-114">Each Azure function is tied tooone trigger, which is an event that causes hello function toorun.</span></span>
<span data-ttu-id="e821e-115">每個函式可以包含任意數目的輸入或輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="e821e-115">Each function can contain any number of input or output bindings.</span></span> <span data-ttu-id="e821e-116">繫結是您可以在函式中使用的服務。</span><span class="sxs-lookup"><span data-stu-id="e821e-116">Bindings are services that you can use in a function.</span></span> <span data-ttu-id="e821e-117">SendGrid 是輸出繫結，您可以使用 toosend 電子郵件。</span><span class="sxs-lookup"><span data-stu-id="e821e-117">SendGrid is an output binding you can use toosend email.</span></span> 

1. <span data-ttu-id="e821e-118">登入 Azure 入口網站 toohello 和[建立 Azure 函式應用程式](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function)或開啟現有的函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="e821e-118">Log in toohello Azure portal and [create an Azure Function App](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) or open an existing Function app.</span></span> 
2. <span data-ttu-id="e821e-119">建立 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="e821e-119">Create an Azure function.</span></span> <span data-ttu-id="e821e-120">tookeep 簡單，它會選擇手動觸發程序和 C#。</span><span class="sxs-lookup"><span data-stu-id="e821e-120">tookeep it simple, choose a manual trigger and C#.</span></span> 

 ![建立 Azure 函式](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a><span data-ttu-id="e821e-122">設定 SendGrid 供 Azure 函數應用程式中使用</span><span class="sxs-lookup"><span data-stu-id="e821e-122">Configure SendGrid for use in an Azure Function app</span></span>

<span data-ttu-id="e821e-123">您必須將您的 SendGrid API 金鑰儲存為應用程式設定 toouse 它的函式中。</span><span class="sxs-lookup"><span data-stu-id="e821e-123">You must store your SendGrid API Key as an app setting toouse it in a function.</span></span> <span data-ttu-id="e821e-124">hello ApiKey 欄位不是您實際的 SendGrid API 金鑰，但設定您的應用程式定義代表實際的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="e821e-124">hello ApiKey field is not your actual SendGrid API key, but an app setting you define that represents your actual API key.</span></span> <span data-ttu-id="e821e-125">如此儲存金鑰是基於安全性，因為這樣會與任何可能簽入原始檔控制的程式碼或檔案分開。</span><span class="sxs-lookup"><span data-stu-id="e821e-125">Storing your key this way is for security, since it is separate from any code or files that might be checked into source code control.</span></span>

- <span data-ttu-id="e821e-126">在函式應用程式的 [應用程式設定] 中建立 **AppSettings**。</span><span class="sxs-lookup"><span data-stu-id="e821e-126">Create an **AppSettings** key in your function app's **Application Settings**.</span></span>

 ![建立 Azure 函式](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a><span data-ttu-id="e821e-128">設定 SendGrid 輸出繫結</span><span class="sxs-lookup"><span data-stu-id="e821e-128">Configure SendGrid output bindings</span></span>

<span data-ttu-id="e821e-129">SendGrid 可做為 Azure 函式輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="e821e-129">SendGrid is available as an Azure function output binding.</span></span> <span data-ttu-id="e821e-130">toocreate SendGrid 輸出繫結：</span><span class="sxs-lookup"><span data-stu-id="e821e-130">toocreate a SendGrid output binding:</span></span>

1. <span data-ttu-id="e821e-131">移 toohello**整合**hello Azure 入口網站中的 hello 函式的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e821e-131">Go toohello **Integrate** tab of hello function in hello Azure portal.</span></span>
2. <span data-ttu-id="e821e-132">按一下**新輸出**toocreate SendGrid 輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="e821e-132">Click **New Output** toocreate a SendGrid output binding.</span></span>
3. <span data-ttu-id="e821e-133">填寫 hello **API 金鑰**和**訊息參數名稱**屬性。</span><span class="sxs-lookup"><span data-stu-id="e821e-133">Fill in hello **API Key** and **Message parameter name** properties.</span></span> <span data-ttu-id="e821e-134">如果您想，您可以輸入 hello 其他屬性，或改為將這些程式碼。</span><span class="sxs-lookup"><span data-stu-id="e821e-134">If you want, you can enter hello other properties now, or code them instead.</span></span> <span data-ttu-id="e821e-135">這些設定可用來當做預設值。</span><span class="sxs-lookup"><span data-stu-id="e821e-135">These settings can be used as defaults.</span></span>

 ![設定 SendGrid 輸出繫結](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

<span data-ttu-id="e821e-137">加入繫結 tooa 函式會建立名為的檔案**function.json**函式的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="e821e-137">Adding a binding tooa function creates a file called **function.json** in your function's folder.</span></span> <span data-ttu-id="e821e-138">這個檔案包含所有 hello 相同的資訊，您在看到 hello Azure 函式的**整合**索引標籤上，但採用 Json 格式。</span><span class="sxs-lookup"><span data-stu-id="e821e-138">This file contains all hello same information that you see in hello Azure function's **Integrate** tab, but in Json format.</span></span> <span data-ttu-id="e821e-139">設定 hello **ApiKey**，**訊息**，和**從**欄位建立下列項目在 hello hello **function.json**檔案：</span><span class="sxs-lookup"><span data-stu-id="e821e-139">Setting hello **ApiKey**, **message**, and **from** fields create hello following entries in hello **function.json** file:</span></span> 

```json
{
  "bindings": [    
    {
      "type": "sendGrid",
      "name": "message",
      "apiKey": "SendGridKey",
      "direction": "out",
      "from": "azure@contoso.com"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="e821e-140">想要的話，您可以自行直接修改這個檔案。</span><span class="sxs-lookup"><span data-stu-id="e821e-140">If you prefer, you may modify this file yourself directly.</span></span>

<span data-ttu-id="e821e-141">既然您已建立和設定 hello 函式應用程式和函式，您可以撰寫 hello 程式碼 toosend 電子郵件。</span><span class="sxs-lookup"><span data-stu-id="e821e-141">Now that you have created and configured hello Function App and function, you can write hello code toosend an email.</span></span>

## <a name="write-code-that-creates-and-sends-email"></a><span data-ttu-id="e821e-142">撰寫程式碼來建立和傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="e821e-142">Write code that creates and sends email</span></span>

<span data-ttu-id="e821e-143">hello SendGrid API 包含所有 hello 命令，您需要 toocreate 並傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="e821e-143">hello SendGrid API contains all hello commands you need toocreate and send an email.</span></span>  

- <span data-ttu-id="e821e-144">取代下列程式碼的 hello hello hello 函式中的程式碼：</span><span class="sxs-lookup"><span data-stu-id="e821e-144">Replace hello code in hello function with hello following code:</span></span>

```cs
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static void Run(TraceWriter log, string input, out Mail message)
{
    message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    // change tooemail of recipient
    personalization.AddTo(new Email("MoreEmailPlease@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

<span data-ttu-id="e821e-145">請注意 hello 第一行包含 hello```#r```參考 hello SendGrid 組件的指示詞。</span><span class="sxs-lookup"><span data-stu-id="e821e-145">Notice hello first line contains hello ```#r``` directive that references hello SendGrid assembly.</span></span> <span data-ttu-id="e821e-146">在這之後，您可以使用```using```陳述式 toomore 輕鬆地存取該命名空間中的 hello 物件。</span><span class="sxs-lookup"><span data-stu-id="e821e-146">After that, you can use a ```using``` statement toomore easily access hello objects in that namespace.</span></span> <span data-ttu-id="e821e-147">在 hello 程式碼中建立的執行個體```Mail```， ```Personalization```，和```Content```從 hello SendGrid API 撰寫 hello 電子郵件的物件。</span><span class="sxs-lookup"><span data-stu-id="e821e-147">In hello code, create instances of ```Mail```, ```Personalization```, and ```Content``` objects from hello SendGrid API that compose hello email.</span></span> <span data-ttu-id="e821e-148">當您傳回 hello 訊息時，SendGrid 傳送該郵件。</span><span class="sxs-lookup"><span data-stu-id="e821e-148">When you return hello message, SendGrid delivers it.</span></span> 

<span data-ttu-id="e821e-149">hello 函式的簽章也包含額外的 out 參數的型別```Mail```名為```message```。</span><span class="sxs-lookup"><span data-stu-id="e821e-149">hello function's signature also contains an extra out parameter of type ```Mail``` named ```message```.</span></span> <span data-ttu-id="e821e-150">輸入和輸出繫結本身在程式碼中以函式參數表示。</span><span class="sxs-lookup"><span data-stu-id="e821e-150">Both input and output bindings express themselves as function parameters in code.</span></span> 

2. <span data-ttu-id="e821e-151">按一下以測試您的程式碼**測試**輸入 hello 訊息和**要求本文** 欄位中，然後按一下 hello**執行** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e821e-151">Test your code by clicking **Test** and entering a message into hello **Request body** field, then clicking hello **Run** button.</span></span>

 ![測試您的程式碼](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. <span data-ttu-id="e821e-153">請檢查電子郵件 tooverify SendGrid 傳送嗨電子郵件。</span><span class="sxs-lookup"><span data-stu-id="e821e-153">Check email tooverify that SendGrid sent hello email.</span></span> <span data-ttu-id="e821e-154">它應該從步驟 1 中，移至 toohello hello 程式碼中的位址，且包含從 hello hello 訊息**要求本文**。</span><span class="sxs-lookup"><span data-stu-id="e821e-154">It should go toohello address in hello code from step 1, and contain hello message from hello **Request body**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e821e-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e821e-155">Next steps</span></span>
<span data-ttu-id="e821e-156">本文示範如何 toouse hello SendGrid 服務 toocreate 及傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="e821e-156">This article has demonstrated how toouse hello SendGrid service toocreate and send email.</span></span> <span data-ttu-id="e821e-157">toolearn 進一步了解使用 Azure 函式在您的應用程式，請參閱下列主題中的 hello:</span><span class="sxs-lookup"><span data-stu-id="e821e-157">toolearn more about using Azure Functions in your apps, see hello following topics:</span></span> 

- <span data-ttu-id="e821e-158">[Azure 函式的最佳作法](functions-best-practices.md)列出一些最佳作法 toouse 時建立 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="e821e-158">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices toouse when creating Azure Functions.</span></span>

- <span data-ttu-id="e821e-159">[Azure Functions 開發人員參考](functions-reference.md) 可供程式設計人員撰寫函式及定義觸發程序和繫結時參考。</span><span class="sxs-lookup"><span data-stu-id="e821e-159">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>

- <span data-ttu-id="e821e-160">[測試 Azure Functions](functions-test-a-function.md) 說明可用於測試函式的各種工具和技巧。</span><span class="sxs-lookup"><span data-stu-id="e821e-160">[Testing Azure Functions](functions-test-a-function.md) Describes various tools and techniques for testing your functions.</span></span>