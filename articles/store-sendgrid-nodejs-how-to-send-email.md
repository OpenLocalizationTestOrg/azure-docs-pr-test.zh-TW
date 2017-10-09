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
# <a name="how-toosend-email-using-sendgrid-from-nodejs"></a><span data-ttu-id="cf649-104">如何 tooSend 電子郵件使用 SendGrid 從 Node.js</span><span class="sxs-lookup"><span data-stu-id="cf649-104">How tooSend Email Using SendGrid from Node.js</span></span>
<span data-ttu-id="cf649-105">本指南示範如何 tooperform 常見的程式設計工作使用 SendGrid 傳送電子郵件在 Azure 上的服務。</span><span class="sxs-lookup"><span data-stu-id="cf649-105">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="cf649-106">使用 hello Node.js 應用程式開發介面撰寫 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="cf649-106">hello samples are written using hello Node.js API.</span></span> <span data-ttu-id="cf649-107">hello 涵蓋案例包括**建構電子郵件**，**傳送電子郵件**，**加入附件**，**使用篩選器**，和**更新屬性**。</span><span class="sxs-lookup"><span data-stu-id="cf649-107">hello scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="cf649-108">如需有關 SendGrid 和傳送電子郵件的詳細資訊，請參閱 hello[接下來的步驟](#next-steps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="cf649-108">For more information on SendGrid and sending email, see hello [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="cf649-109">什麼是 hello SendGrid 電子郵件服務？</span><span class="sxs-lookup"><span data-stu-id="cf649-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="cf649-110">SendGrid 是 [雲端架構電子郵件服務]，能提供可靠的 [交易式電子郵件傳遞]、擴充性和即時分析，以及有彈性的 API 來輕鬆進行自訂整合。</span><span class="sxs-lookup"><span data-stu-id="cf649-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="cf649-111">常見的 SendGrid 使用案例包括：</span><span class="sxs-lookup"><span data-stu-id="cf649-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="cf649-112">自動將資料傳送回條 toocustomers</span><span class="sxs-lookup"><span data-stu-id="cf649-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="cf649-113">管理通訊群組清單，以便將每月電子傳單和特別優惠傳送給客戶</span><span class="sxs-lookup"><span data-stu-id="cf649-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="cf649-114">收集封鎖的電子郵件、客戶的回應情形等項目的即時度量</span><span class="sxs-lookup"><span data-stu-id="cf649-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="cf649-115">產生 toohelp 識別趨勢的報表</span><span class="sxs-lookup"><span data-stu-id="cf649-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="cf649-116">轉寄客戶查詢</span><span class="sxs-lookup"><span data-stu-id="cf649-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="cf649-117">透過電子郵件從您的應用程式傳送通知</span><span class="sxs-lookup"><span data-stu-id="cf649-117">Email notifications from your application</span></span>

<span data-ttu-id="cf649-118">如需詳細資訊，請參閱 [https://sendgrid.com](https://sendgrid.com)。</span><span class="sxs-lookup"><span data-stu-id="cf649-118">For more information, see [https://sendgrid.com](https://sendgrid.com).</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="cf649-119">建立 SendGrid 帳戶</span><span class="sxs-lookup"><span data-stu-id="cf649-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-nodejs-module"></a><span data-ttu-id="cf649-120">參考 hello SendGrid Node.js 模組</span><span class="sxs-lookup"><span data-stu-id="cf649-120">Reference hello SendGrid Node.js Module</span></span>
<span data-ttu-id="cf649-121">可以使用下列命令的 hello，透過 hello node 封裝管理員 (npm) 安裝 Node.js 的 hello SendGrid 模組：</span><span class="sxs-lookup"><span data-stu-id="cf649-121">hello SendGrid module for Node.js can be installed through hello node package manager (npm) by using hello following command:</span></span>

    npm install sendgrid

<span data-ttu-id="cf649-122">安裝之後，您可以使用下列程式碼的 hello hello 模組要求應用程式中：</span><span class="sxs-lookup"><span data-stu-id="cf649-122">After installation, you can require hello module in your application by using hello following code:</span></span>

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

<span data-ttu-id="cf649-123">hello SendGrid 模組匯出的 hello **SendGrid**和**電子郵件**函式。</span><span class="sxs-lookup"><span data-stu-id="cf649-123">hello SendGrid module exports hello **SendGrid** and **Email** functions.</span></span>
<span data-ttu-id="cf649-124">**SendGrid** 負責透過 Web API 傳送電子郵件，而 **Email** 則負責封裝電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="cf649-124">**SendGrid** is responsible for sending email through Web API, while **Email** encapsulates an email message.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="cf649-125">如何：建立電子郵件</span><span class="sxs-lookup"><span data-stu-id="cf649-125">How to: Create an Email</span></span>
<span data-ttu-id="cf649-126">建立電子郵件訊息使用 hello SendGrid 模組包括第一次建立 hello 電子郵件，使用函式，然後將它使用 hello SendGrid 函式傳送的電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="cf649-126">Creating an email message using hello SendGrid module involves first creating an email message using hello Email function, and then sending it using hello SendGrid function.</span></span> <span data-ttu-id="cf649-127">hello 以下是建立新的訊息使用 hello 電子郵件函式的範例：</span><span class="sxs-lookup"><span data-stu-id="cf649-127">hello following is an example of creating a new message using hello Email function:</span></span>

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

<span data-ttu-id="cf649-128">您也可以指定 HTML 訊息之用戶端的支援設定 hello html 屬性。</span><span class="sxs-lookup"><span data-stu-id="cf649-128">You can also specify an HTML message for clients that support it by setting hello html property.</span></span> <span data-ttu-id="cf649-129">例如：</span><span class="sxs-lookup"><span data-stu-id="cf649-129">For example:</span></span>

    html: This is a sample <b>HTML<b> email message.

<span data-ttu-id="cf649-130">設定這兩個的 hello 文字和 html 屬性不支援 HTML 郵件用戶端提供依正常程序到文字內容的後援。</span><span class="sxs-lookup"><span data-stu-id="cf649-130">Setting both hello text and html properties provides graceful fallback to text content for clients that cannot support HTML messages.</span></span>

<span data-ttu-id="cf649-131">如需有關 hello 電子郵件函式所支援的所有屬性的詳細資訊，請參閱[sendgrid nodejs][sendgrid-nodejs]。</span><span class="sxs-lookup"><span data-stu-id="cf649-131">For more information on all properties supported by hello Email function, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="cf649-132">如何：傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="cf649-132">How to: Send an Email</span></span>
<span data-ttu-id="cf649-133">在建立之後使用 hello 電子郵件函式的電子郵件訊息，您可以傳送 hello SendGrid 所提供的 Web API 的使用。</span><span class="sxs-lookup"><span data-stu-id="cf649-133">After creating an email message using hello Email function, you can send it using hello Web API provided by SendGrid.</span></span> 

### <a name="web-api"></a><span data-ttu-id="cf649-134">Web API</span><span class="sxs-lookup"><span data-stu-id="cf649-134">Web API</span></span>
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> <span data-ttu-id="cf649-135">雖然 hello 上述範例會顯示在電子郵件物件和回呼函式傳遞，您可以也會直接叫用 hello 傳送函式直接指定電子郵件內容。</span><span class="sxs-lookup"><span data-stu-id="cf649-135">While hello above examples show passing in an email object and callback function, you can also directly invoke hello send function by directly specifying email properties.</span></span> <span data-ttu-id="cf649-136">例如：</span><span class="sxs-lookup"><span data-stu-id="cf649-136">For example:</span></span>  
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

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="cf649-137">如何：新增附件</span><span class="sxs-lookup"><span data-stu-id="cf649-137">How to: Add an Attachment</span></span>
<span data-ttu-id="cf649-138">附件可以指定 hello 檔案名稱和路徑在 hello 新增 tooa 訊息**檔案**屬性。</span><span class="sxs-lookup"><span data-stu-id="cf649-138">Attachments can be added tooa message by specifying hello file name(s) and path(s) in hello **files** property.</span></span> <span data-ttu-id="cf649-139">下列範例中的 hello 示範傳送附件：</span><span class="sxs-lookup"><span data-stu-id="cf649-139">hello following example demonstrates sending an attachment:</span></span>

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
> <span data-ttu-id="cf649-140">當使用 hello**檔案**屬性，hello 檔案必須可透過存取[fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile)。</span><span class="sxs-lookup"><span data-stu-id="cf649-140">When using hello **files** property, hello file must be accessible through [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span></span> <span data-ttu-id="cf649-141">如果您想 tooattach hello 檔案裝載在 Azure 儲存體，例如 Blob 容器，您必須先將 hello 檔案 toolocal 儲存體或 Azure 磁碟機 tooan 使用 hello 附件形式傳送之前**檔案**屬性。</span><span class="sxs-lookup"><span data-stu-id="cf649-141">If hello file you wish tooattach is hosted in Azure Storage, such as in a Blob container, you must first copy hello file toolocal storage or tooan Azure drive before it can be sent as an attachment using hello **files** property.</span></span>
> 
> 

## <a name="how-to-use-filters-tooenable-footers-and-tracking"></a><span data-ttu-id="cf649-142">如何： 使用篩選器 tooEnable 頁尾和追蹤</span><span class="sxs-lookup"><span data-stu-id="cf649-142">How to: Use Filters tooEnable Footers and Tracking</span></span>
<span data-ttu-id="cf649-143">SendGrid 提供其他電子郵件功能，透過 hello 使用篩選條件。</span><span class="sxs-lookup"><span data-stu-id="cf649-143">SendGrid provides additional email functionality through hello use of filters.</span></span> <span data-ttu-id="cf649-144">這些是可以加入 tooan 電子郵件訊息，若要啟用特定的功能，例如啟用點選追蹤、 Google analytics、 追蹤、 訂用帳戶的設定，依此類推。</span><span class="sxs-lookup"><span data-stu-id="cf649-144">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="cf649-145">如需完整的篩選器清單，請參閱[篩選器設定][Filter Settings]。</span><span class="sxs-lookup"><span data-stu-id="cf649-145">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

<span data-ttu-id="cf649-146">篩選可套用的 tooa 訊息使用 hello**篩選**屬性。</span><span class="sxs-lookup"><span data-stu-id="cf649-146">Filters can be applied tooa message by using hello **filters** property.</span></span>
<span data-ttu-id="cf649-147">每個篩選器都是由包含篩選器特定設定的雜湊來指定。</span><span class="sxs-lookup"><span data-stu-id="cf649-147">Each filter is specified by a hash containing filter-specific settings.</span></span>
<span data-ttu-id="cf649-148">hello 下列範例示範 hello 頁尾，並按一下 追蹤篩選器：</span><span class="sxs-lookup"><span data-stu-id="cf649-148">hello following examples demonstrate hello footer and click tracking filters:</span></span>

### <a name="footer"></a><span data-ttu-id="cf649-149">頁尾</span><span class="sxs-lookup"><span data-stu-id="cf649-149">Footer</span></span>
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

### <a name="click-tracking"></a><span data-ttu-id="cf649-150">點選追蹤</span><span class="sxs-lookup"><span data-stu-id="cf649-150">Click Tracking</span></span>
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

## <a name="how-to-update-email-properties"></a><span data-ttu-id="cf649-151">如何：更新電子郵件屬性</span><span class="sxs-lookup"><span data-stu-id="cf649-151">How to: Update Email Properties</span></span>
<span data-ttu-id="cf649-152">某些電子郵件內容會被覆寫使用**設定*屬性** * 或附加**新增*屬性** *。</span><span class="sxs-lookup"><span data-stu-id="cf649-152">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span> <span data-ttu-id="cf649-153">例如，您可以使用下列方式新增其他收件者：</span><span class="sxs-lookup"><span data-stu-id="cf649-153">For example, you can add additional recipients by using</span></span>

    email.addTo('jeff@contoso.com');

<span data-ttu-id="cf649-154">或使用下列方式設定篩選器：</span><span class="sxs-lookup"><span data-stu-id="cf649-154">or set a filter by using</span></span>

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

<span data-ttu-id="cf649-155">如需詳細資訊，請參閱[sendgrid nodejs][sendgrid-nodejs]。</span><span class="sxs-lookup"><span data-stu-id="cf649-155">For more information, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="cf649-156">如何：使用其他 SendGrid 服務</span><span class="sxs-lookup"><span data-stu-id="cf649-156">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="cf649-157">SendGrid 提供網頁型應用程式開發介面，您可以從 Azure 應用程式使用 tooleverage 其他 SendGrid 功能。</span><span class="sxs-lookup"><span data-stu-id="cf649-157">SendGrid offers web-based APIs that you can use tooleverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="cf649-158">完整的詳細資訊，請參閱 hello [SendGrid API 文件][SendGrid API documentation]。</span><span class="sxs-lookup"><span data-stu-id="cf649-158">For full details, see hello [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf649-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cf649-159">Next Steps</span></span>
<span data-ttu-id="cf649-160">既然您已經學會 hello 的 hello SendGrid 電子郵件服務的基本概念，請遵循這些連結 toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="cf649-160">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="cf649-161">SendGrid Node.js 模組存放庫： [sendgrid nodejs][sendgrid-nodejs]</span><span class="sxs-lookup"><span data-stu-id="cf649-161">SendGrid Node.js module repository: [sendgrid-nodejs][sendgrid-nodejs]</span></span>
* <span data-ttu-id="cf649-162">SendGrid API 文件︰<https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="cf649-162">SendGrid API documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="cf649-163">Azure 客戶的 SendGrid 特別優惠：[http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span><span class="sxs-lookup"><span data-stu-id="cf649-163">SendGrid special offer for Azure customers: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span></span>

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
[雲端架構電子郵件服務]: https://sendgrid.com/email-solutions
[交易式電子郵件傳遞]: https://sendgrid.com/transactional-email
