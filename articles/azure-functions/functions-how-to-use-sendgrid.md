---
title: "如何使用 Azure Functions 中的 SendGrid | Microsoft Docs"
description: "說明如何使用 Azure Functions 中的 SendGrid"
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
ms.openlocfilehash: 05c9f4e4a4351219da68af8b702c25f21d7d4d02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-sendgrid-in-azure-functions"></a><span data-ttu-id="7f2de-103">如何使用 Azure Functions 中的 SendGrid</span><span class="sxs-lookup"><span data-stu-id="7f2de-103">How to use SendGrid in Azure Functions</span></span>

## <a name="sendgrid-overview"></a><span data-ttu-id="7f2de-104">SendGrid 概觀</span><span class="sxs-lookup"><span data-stu-id="7f2de-104">SendGrid Overview</span></span>

<span data-ttu-id="7f2de-105">Azure Functions 支援 SendGrid 輸出繫結，可讓您的函式利用幾行程式碼和一個 SendGrid 帳戶，就能傳送電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="7f2de-105">Azure Functions supports SendGrid output bindings to enable your functions to send email messages with a few lines of code and a SendGrid account.</span></span>

<span data-ttu-id="7f2de-106">若要在 Azure 函式中使用 SendGrid API，您必須有 [SendGrid 帳戶](http://SendGrid.com)。</span><span class="sxs-lookup"><span data-stu-id="7f2de-106">To use the SendGrid API in an Azure Function, you must have a [SendGrid account](http://SendGrid.com).</span></span> <span data-ttu-id="7f2de-107">此外，您還必須有 SendGrid API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="7f2de-107">Additionally, you must have a SendGrid API Key.</span></span> <span data-ttu-id="7f2de-108">登入您的 SendGrid 帳戶，按一下 [設定]，然後按一下 [API 金鑰] 產生 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="7f2de-108">Log in to your SendGrid account and click **Settings** then **API Key** to generate an API key.</span></span> <span data-ttu-id="7f2de-109">請備妥此金鑰，在後續步驟中會用到。</span><span class="sxs-lookup"><span data-stu-id="7f2de-109">Keep this key available as you use it in an upcoming step.</span></span>

<span data-ttu-id="7f2de-110">您現在已經準備好建立 Azure 函數應用程式。</span><span class="sxs-lookup"><span data-stu-id="7f2de-110">You are now ready to create an Azure Function app.</span></span>

## <a name="create-an-azure-function-app"></a><span data-ttu-id="7f2de-111">建立 Azure 函數應用程式</span><span class="sxs-lookup"><span data-stu-id="7f2de-111">Create an Azure Function app</span></span> 

<span data-ttu-id="7f2de-112">Azure Functions 應用程式是一或多個 Azure 函式的容器。</span><span class="sxs-lookup"><span data-stu-id="7f2de-112">Azure Function Apps are containers for one or more Azure functions.</span></span> <span data-ttu-id="7f2de-113">Azure Functions 就只是函式。</span><span class="sxs-lookup"><span data-stu-id="7f2de-113">Azure functions are just that - a function.</span></span> <span data-ttu-id="7f2de-114">每個 Azure 函式會繫結至一個觸發程序，也就是會導致執行函式的事件。</span><span class="sxs-lookup"><span data-stu-id="7f2de-114">Each Azure function is tied to one trigger, which is an event that causes the function to run.</span></span>
<span data-ttu-id="7f2de-115">每個函式可以包含任意數目的輸入或輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="7f2de-115">Each function can contain any number of input or output bindings.</span></span> <span data-ttu-id="7f2de-116">繫結是您可以在函式中使用的服務。</span><span class="sxs-lookup"><span data-stu-id="7f2de-116">Bindings are services that you can use in a function.</span></span> <span data-ttu-id="7f2de-117">SendGrid 是可用來傳送電子郵件的輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="7f2de-117">SendGrid is an output binding you can use to send email.</span></span> 

1. <span data-ttu-id="7f2de-118">登入 Azure 入口網站，[建立 Azure 函數應用程式](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function)，或開啟現有的函數應用程式。</span><span class="sxs-lookup"><span data-stu-id="7f2de-118">Log in to the Azure portal and [create an Azure Function App](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) or open an existing Function app.</span></span> 
2. <span data-ttu-id="7f2de-119">建立 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="7f2de-119">Create an Azure function.</span></span> <span data-ttu-id="7f2de-120">為了簡單起見，請選擇手動觸發程序和 C#。</span><span class="sxs-lookup"><span data-stu-id="7f2de-120">To keep it simple, choose a manual trigger and C#.</span></span> 

 ![建立 Azure 函式](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a><span data-ttu-id="7f2de-122">設定 SendGrid 供 Azure 函數應用程式中使用</span><span class="sxs-lookup"><span data-stu-id="7f2de-122">Configure SendGrid for use in an Azure Function app</span></span>

<span data-ttu-id="7f2de-123">您必須將 SendGrid API 金鑰儲存為應用程式設定，才能在函式中使用。</span><span class="sxs-lookup"><span data-stu-id="7f2de-123">You must store your SendGrid API Key as an app setting to use it in a function.</span></span> <span data-ttu-id="7f2de-124">ApiKey 欄位不是實際的 SendGrid API 金鑰，而是您定義來代表實際 API 金鑰的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="7f2de-124">The ApiKey field is not your actual SendGrid API key, but an app setting you define that represents your actual API key.</span></span> <span data-ttu-id="7f2de-125">如此儲存金鑰是基於安全性，因為這樣會與任何可能簽入原始檔控制的程式碼或檔案分開。</span><span class="sxs-lookup"><span data-stu-id="7f2de-125">Storing your key this way is for security, since it is separate from any code or files that might be checked into source code control.</span></span>

- <span data-ttu-id="7f2de-126">在函式應用程式的 [應用程式設定] 中建立 **AppSettings**。</span><span class="sxs-lookup"><span data-stu-id="7f2de-126">Create an **AppSettings** key in your function app's **Application Settings**.</span></span>

 ![建立 Azure 函式](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a><span data-ttu-id="7f2de-128">設定 SendGrid 輸出繫結</span><span class="sxs-lookup"><span data-stu-id="7f2de-128">Configure SendGrid output bindings</span></span>

<span data-ttu-id="7f2de-129">SendGrid 可做為 Azure 函式輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="7f2de-129">SendGrid is available as an Azure function output binding.</span></span> <span data-ttu-id="7f2de-130">若要建立 SendGrid 輸出繫結：</span><span class="sxs-lookup"><span data-stu-id="7f2de-130">To create a SendGrid output binding:</span></span>

1. <span data-ttu-id="7f2de-131">在 Azure 入口網站中，移至函式的 [整合] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7f2de-131">Go to the **Integrate** tab of the function in the Azure portal.</span></span>
2. <span data-ttu-id="7f2de-132">按一下 [新增輸出]，建立 SendGrid 輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="7f2de-132">Click **New Output** to create a SendGrid output binding.</span></span>
3. <span data-ttu-id="7f2de-133">填寫 [API 金鑰] 和 [訊息參數名稱] 屬性。</span><span class="sxs-lookup"><span data-stu-id="7f2de-133">Fill in the **API Key** and **Message parameter name** properties.</span></span> <span data-ttu-id="7f2de-134">想要的話，您可以現在就輸入其他屬性，或改以在程式碼中撰寫。</span><span class="sxs-lookup"><span data-stu-id="7f2de-134">If you want, you can enter the other properties now, or code them instead.</span></span> <span data-ttu-id="7f2de-135">這些設定可用來當做預設值。</span><span class="sxs-lookup"><span data-stu-id="7f2de-135">These settings can be used as defaults.</span></span>

 ![設定 SendGrid 輸出繫結](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

<span data-ttu-id="7f2de-137">將繫結新增至函式時，函式的資料夾中會建立名為 **function.json** 的檔案。</span><span class="sxs-lookup"><span data-stu-id="7f2de-137">Adding a binding to a function creates a file called **function.json** in your function's folder.</span></span> <span data-ttu-id="7f2de-138">這個檔案包含的資訊與您在 Azure 函式的 [整合] 索引標籤中看到資訊完全相同，但為 Json 格式。</span><span class="sxs-lookup"><span data-stu-id="7f2de-138">This file contains all the same information that you see in the Azure function's **Integrate** tab, but in Json format.</span></span> <span data-ttu-id="7f2de-139">設定 [ApiKey]、[訊息] 和 [寄件者] 欄位後，將會在 **function.json** 檔案中建立下列項目︰</span><span class="sxs-lookup"><span data-stu-id="7f2de-139">Setting the **ApiKey**, **message**, and **from** fields create the following entries in the **function.json** file:</span></span> 

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

<span data-ttu-id="7f2de-140">想要的話，您可以自行直接修改這個檔案。</span><span class="sxs-lookup"><span data-stu-id="7f2de-140">If you prefer, you may modify this file yourself directly.</span></span>

<span data-ttu-id="7f2de-141">既然您已建立並設定函數應用程式和函式，接下來可以撰寫程式碼以傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="7f2de-141">Now that you have created and configured the Function App and function, you can write the code to send an email.</span></span>

## <a name="write-code-that-creates-and-sends-email"></a><span data-ttu-id="7f2de-142">撰寫程式碼來建立和傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="7f2de-142">Write code that creates and sends email</span></span>

<span data-ttu-id="7f2de-143">SendGrid API 包含建立和傳送電子郵件所需的全部命令。</span><span class="sxs-lookup"><span data-stu-id="7f2de-143">The SendGrid API contains all the commands you need to create and send an email.</span></span>  

- <span data-ttu-id="7f2de-144">使用下列程式碼取代函式中的程式碼：</span><span class="sxs-lookup"><span data-stu-id="7f2de-144">Replace the code in the function with the following code:</span></span>

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
    // change to email of recipient
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

<span data-ttu-id="7f2de-145">請注意，第一行包含 ```#r``` 指示詞來參考 SendGrid 組件。</span><span class="sxs-lookup"><span data-stu-id="7f2de-145">Notice the first line contains the ```#r``` directive that references the SendGrid assembly.</span></span> <span data-ttu-id="7f2de-146">之後，您可以使用 ```using``` 陳述式，更輕鬆地存取該命名空間中的物件。</span><span class="sxs-lookup"><span data-stu-id="7f2de-146">After that, you can use a ```using``` statement to more easily access the objects in that namespace.</span></span> <span data-ttu-id="7f2de-147">在程式碼中，從 SendGrid API 建立 ```Mail```、```Personalization``` 和 ```Content``` 物件 (構成電子郵件) 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="7f2de-147">In the code, create instances of ```Mail```, ```Personalization```, and ```Content``` objects from the SendGrid API that compose the email.</span></span> <span data-ttu-id="7f2de-148">當您傳回訊息時，SendGrid 會傳送它。</span><span class="sxs-lookup"><span data-stu-id="7f2de-148">When you return the message, SendGrid delivers it.</span></span> 

<span data-ttu-id="7f2de-149">函式的簽章也包含 ```Mail``` 類型的額外 out 參數，名為 ```message```。</span><span class="sxs-lookup"><span data-stu-id="7f2de-149">The function's signature also contains an extra out parameter of type ```Mail``` named ```message```.</span></span> <span data-ttu-id="7f2de-150">輸入和輸出繫結本身在程式碼中以函式參數表示。</span><span class="sxs-lookup"><span data-stu-id="7f2de-150">Both input and output bindings express themselves as function parameters in code.</span></span> 

2. <span data-ttu-id="7f2de-151">按一下 [測試]，在 [要求本文] 欄位中輸入訊息，然後按一下 [執行] 按鈕，以測試您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="7f2de-151">Test your code by clicking **Test** and entering a message into the **Request body** field, then clicking the **Run** button.</span></span>

 ![測試您的程式碼](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. <span data-ttu-id="7f2de-153">檢查電子郵件，確認 SendGrid 已傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="7f2de-153">Check email to verify that SendGrid sent the email.</span></span> <span data-ttu-id="7f2de-154">它應該會傳送至步驟 1 程式碼中的位址，且包含 [要求本文] 中的訊息。</span><span class="sxs-lookup"><span data-stu-id="7f2de-154">It should go to the address in the code from step 1, and contain the message from the **Request body**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f2de-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7f2de-155">Next steps</span></span>
<span data-ttu-id="7f2de-156">本文已示範如何使用 SendGrid 服務來建立和傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="7f2de-156">This article has demonstrated how to use the SendGrid service to create and send email.</span></span> <span data-ttu-id="7f2de-157">若要深入了解在您的應用程式中使用 Azure Functions，請參閱下列主題︰</span><span class="sxs-lookup"><span data-stu-id="7f2de-157">To learn more about using Azure Functions in your apps, see the following topics:</span></span> 

- <span data-ttu-id="7f2de-158">[Azure Functions 的最佳做法](functions-best-practices.md)列出建立 Azure 函式時可採用的一些最佳做法。</span><span class="sxs-lookup"><span data-stu-id="7f2de-158">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices to use when creating Azure Functions.</span></span>

- <span data-ttu-id="7f2de-159">[Azure Functions 開發人員參考](functions-reference.md) 可供程式設計人員撰寫函式及定義觸發程序和繫結時參考。</span><span class="sxs-lookup"><span data-stu-id="7f2de-159">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>

- <span data-ttu-id="7f2de-160">[測試 Azure Functions](functions-test-a-function.md) 說明可用於測試函式的各種工具和技巧。</span><span class="sxs-lookup"><span data-stu-id="7f2de-160">[Testing Azure Functions](functions-test-a-function.md) Describes various tools and techniques for testing your functions.</span></span>