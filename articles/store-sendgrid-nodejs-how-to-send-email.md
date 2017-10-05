---
title: "如何使用 SendGrid 電子郵件服務 (Node.js) | Microsoft Docs"
description: "了解如何在 Azure 使用 SendGrid 電子郵件服務傳送電子郵件。 程式碼範例以 Node.js API 撰寫。"
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
ms.openlocfilehash: 327cea3a24cc47a9cc463b37cc2346ebc475ef7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-email-using-sendgrid-from-nodejs"></a><span data-ttu-id="a7a05-104">如何使用 SendGrid 透過 Node.js 傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="a7a05-104">How to Send Email Using SendGrid from Node.js</span></span>
<span data-ttu-id="a7a05-105">本指南示範如何在 Azure 上透過 SendGrid 電子郵件服務執行常見程式設計工作。</span><span class="sxs-lookup"><span data-stu-id="a7a05-105">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="a7a05-106">這些範例使用 Node.js API 撰寫。</span><span class="sxs-lookup"><span data-stu-id="a7a05-106">The samples are written using the Node.js API.</span></span> <span data-ttu-id="a7a05-107">涵蓋的案例包括**建構電子郵件**、**傳送電子郵件**、**新增附件**、**使用篩選器**及**更新屬性**。</span><span class="sxs-lookup"><span data-stu-id="a7a05-107">The scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="a7a05-108">如需有關 SendGrid 及傳送電子郵件的詳細資訊，請參閱 [後續步驟](#next-steps) 一節。</span><span class="sxs-lookup"><span data-stu-id="a7a05-108">For more information on SendGrid and sending email, see the [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="a7a05-109">什麼是 SendGrid 電子郵件服務？</span><span class="sxs-lookup"><span data-stu-id="a7a05-109">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="a7a05-110">SendGrid 是 [雲端架構電子郵件服務]，能提供可靠的 [交易式電子郵件傳遞]、擴充性和即時分析，以及有彈性的 API 來輕鬆進行自訂整合。</span><span class="sxs-lookup"><span data-stu-id="a7a05-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="a7a05-111">常見的 SendGrid 使用案例包括：</span><span class="sxs-lookup"><span data-stu-id="a7a05-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="a7a05-112">自動傳送回條給客戶</span><span class="sxs-lookup"><span data-stu-id="a7a05-112">Automatically sending receipts to customers</span></span>
* <span data-ttu-id="a7a05-113">管理通訊群組清單，以便將每月電子傳單和特別優惠傳送給客戶</span><span class="sxs-lookup"><span data-stu-id="a7a05-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="a7a05-114">收集封鎖的電子郵件、客戶的回應情形等項目的即時度量</span><span class="sxs-lookup"><span data-stu-id="a7a05-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="a7a05-115">產生報表，協助找出趨勢</span><span class="sxs-lookup"><span data-stu-id="a7a05-115">Generating reports to help identify trends</span></span>
* <span data-ttu-id="a7a05-116">轉寄客戶查詢</span><span class="sxs-lookup"><span data-stu-id="a7a05-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="a7a05-117">透過電子郵件從您的應用程式傳送通知</span><span class="sxs-lookup"><span data-stu-id="a7a05-117">Email notifications from your application</span></span>

<span data-ttu-id="a7a05-118">如需詳細資訊，請參閱 [https://sendgrid.com](https://sendgrid.com)。</span><span class="sxs-lookup"><span data-stu-id="a7a05-118">For more information, see [https://sendgrid.com](https://sendgrid.com).</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="a7a05-119">建立 SendGrid 帳戶</span><span class="sxs-lookup"><span data-stu-id="a7a05-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-the-sendgrid-nodejs-module"></a><span data-ttu-id="a7a05-120">參考 SendGrid Node.js 模組</span><span class="sxs-lookup"><span data-stu-id="a7a05-120">Reference the SendGrid Node.js Module</span></span>
<span data-ttu-id="a7a05-121">您可以使用下列命令，透過節點封裝管理員 (npm) 安裝適用於 Node.js 的 SendGrid 模組：</span><span class="sxs-lookup"><span data-stu-id="a7a05-121">The SendGrid module for Node.js can be installed through the node package manager (npm) by using the following command:</span></span>

    npm install sendgrid

<span data-ttu-id="a7a05-122">安裝之後，您可以使用下列程式碼要求您應用程式中的模組：</span><span class="sxs-lookup"><span data-stu-id="a7a05-122">After installation, you can require the module in your application by using the following code:</span></span>

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

<span data-ttu-id="a7a05-123">SendGrid 模組會匯出 **SendGrid** 和 **Email** 函數。</span><span class="sxs-lookup"><span data-stu-id="a7a05-123">The SendGrid module exports the **SendGrid** and **Email** functions.</span></span>
<span data-ttu-id="a7a05-124">**SendGrid** 負責透過 Web API 傳送電子郵件，而 **Email** 則負責封裝電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="a7a05-124">**SendGrid** is responsible for sending email through Web API, while **Email** encapsulates an email message.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="a7a05-125">如何：建立電子郵件</span><span class="sxs-lookup"><span data-stu-id="a7a05-125">How to: Create an Email</span></span>
<span data-ttu-id="a7a05-126">使用 SendGrid 模組建立電子郵件訊息涉及先使用 Email 函數建立電子郵件訊息，再使用 SendGrid 函數傳送該電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="a7a05-126">Creating an email message using the SendGrid module involves first creating an email message using the Email function, and then sending it using the SendGrid function.</span></span> <span data-ttu-id="a7a05-127">以下是使用 Email 函數建立新訊息的範例：</span><span class="sxs-lookup"><span data-stu-id="a7a05-127">The following is an example of creating a new message using the Email function:</span></span>

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

<span data-ttu-id="a7a05-128">您也可以設定 html 屬性，為支援 HTML 訊息的用戶端指定一個 HTML 訊息。</span><span class="sxs-lookup"><span data-stu-id="a7a05-128">You can also specify an HTML message for clients that support it by setting the html property.</span></span> <span data-ttu-id="a7a05-129">例如：</span><span class="sxs-lookup"><span data-stu-id="a7a05-129">For example:</span></span>

    html: This is a sample <b>HTML<b> email message.

<span data-ttu-id="a7a05-130">同時設定 text 和 html 屬性可以為無法支援 HTML 訊息的用戶端提供正常的文字內容遞補。</span><span class="sxs-lookup"><span data-stu-id="a7a05-130">Setting both the text and html properties provides graceful fallback to text content for clients that cannot support HTML messages.</span></span>

<span data-ttu-id="a7a05-131">如需有關電子郵件函式所支援的所有屬性的詳細資訊，請參閱[sendgrid nodejs][sendgrid-nodejs]。</span><span class="sxs-lookup"><span data-stu-id="a7a05-131">For more information on all properties supported by the Email function, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="a7a05-132">如何：傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="a7a05-132">How to: Send an Email</span></span>
<span data-ttu-id="a7a05-133">使用 Email 函數建立電子郵件訊息之後，您可以使用 SendGrid 所提供的 Web API 進行傳送。</span><span class="sxs-lookup"><span data-stu-id="a7a05-133">After creating an email message using the Email function, you can send it using the Web API provided by SendGrid.</span></span> 

### <a name="web-api"></a><span data-ttu-id="a7a05-134">Web API</span><span class="sxs-lookup"><span data-stu-id="a7a05-134">Web API</span></span>
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> <span data-ttu-id="a7a05-135">上述範例示範的是傳入一個電子郵件物件和回呼函數，您也可以直接指定電子郵件屬性來直接叫用 send 函數。</span><span class="sxs-lookup"><span data-stu-id="a7a05-135">While the above examples show passing in an email object and callback function, you can also directly invoke the send function by directly specifying email properties.</span></span> <span data-ttu-id="a7a05-136">例如：</span><span class="sxs-lookup"><span data-stu-id="a7a05-136">For example:</span></span>  
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

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="a7a05-137">如何：新增附件</span><span class="sxs-lookup"><span data-stu-id="a7a05-137">How to: Add an Attachment</span></span>
<span data-ttu-id="a7a05-138">您可以透過在 **files** 屬性中指定檔案名稱和路徑，將附件新增至訊息中。</span><span class="sxs-lookup"><span data-stu-id="a7a05-138">Attachments can be added to a message by specifying the file name(s) and path(s) in the **files** property.</span></span> <span data-ttu-id="a7a05-139">下列範例示範如何傳送附件：</span><span class="sxs-lookup"><span data-stu-id="a7a05-139">The following example demonstrates sending an attachment:</span></span>

    sendgrid.send({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.',
        files: [
            {
                filename:     '',           // required only if file.content is used.
                contentType:  '',           // optional
                cid:          '',           // optional, used to specify cid for inline content
                path:         '',           //
                url:          '',           // == One of these three options is required
                content:      ('' | Buffer) //
            }
        ],
    });

> [!NOTE]
> <span data-ttu-id="a7a05-140">使用 **files** 屬性時，必須要能夠透過 [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile) 存取檔案。</span><span class="sxs-lookup"><span data-stu-id="a7a05-140">When using the **files** property, the file must be accessible through [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span></span> <span data-ttu-id="a7a05-141">如果您想要附加的檔案裝載於 Azure 儲存體中 (例如 Blob 容器中)，您就必須先將該檔案複製到本機儲存體或 Azure 磁碟機，才能使用 **files** 屬性以附件形式傳送它。</span><span class="sxs-lookup"><span data-stu-id="a7a05-141">If the file you wish to attach is hosted in Azure Storage, such as in a Blob container, you must first copy the file to local storage or to an Azure drive before it can be sent as an attachment using the **files** property.</span></span>
> 
> 

## <a name="how-to-use-filters-to-enable-footers-and-tracking"></a><span data-ttu-id="a7a05-142">如何：使用篩選器來啟用頁尾和追蹤</span><span class="sxs-lookup"><span data-stu-id="a7a05-142">How to: Use Filters to Enable Footers and Tracking</span></span>
<span data-ttu-id="a7a05-143">SendGrid 提供了運用篩選器的其他電子郵件功能。</span><span class="sxs-lookup"><span data-stu-id="a7a05-143">SendGrid provides additional email functionality through the use of filters.</span></span> <span data-ttu-id="a7a05-144">這些設定可新增到電子郵件以啟用特定功能，例如啟用點擊追蹤、Google 分析、訂閱追蹤等。</span><span class="sxs-lookup"><span data-stu-id="a7a05-144">These are settings that can be added to an email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="a7a05-145">如需完整的篩選器清單，請參閱[篩選器設定][Filter Settings]。</span><span class="sxs-lookup"><span data-stu-id="a7a05-145">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

<span data-ttu-id="a7a05-146">您可以使用 **filters** 屬性在訊息套用篩選器。</span><span class="sxs-lookup"><span data-stu-id="a7a05-146">Filters can be applied to a message by using the **filters** property.</span></span>
<span data-ttu-id="a7a05-147">每個篩選器都是由包含篩選器特定設定的雜湊來指定。</span><span class="sxs-lookup"><span data-stu-id="a7a05-147">Each filter is specified by a hash containing filter-specific settings.</span></span>
<span data-ttu-id="a7a05-148">下列範例示範頁尾和點選追蹤篩選器：</span><span class="sxs-lookup"><span data-stu-id="a7a05-148">The following examples demonstrate the footer and click tracking filters:</span></span>

### <a name="footer"></a><span data-ttu-id="a7a05-149">頁尾</span><span class="sxs-lookup"><span data-stu-id="a7a05-149">Footer</span></span>
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

### <a name="click-tracking"></a><span data-ttu-id="a7a05-150">點選追蹤</span><span class="sxs-lookup"><span data-stu-id="a7a05-150">Click Tracking</span></span>
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

## <a name="how-to-update-email-properties"></a><span data-ttu-id="a7a05-151">如何：更新電子郵件屬性</span><span class="sxs-lookup"><span data-stu-id="a7a05-151">How to: Update Email Properties</span></span>
<span data-ttu-id="a7a05-152">某些電子郵件內容會被覆寫使用**設定*屬性** * 或附加**新增*屬性** *。</span><span class="sxs-lookup"><span data-stu-id="a7a05-152">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span> <span data-ttu-id="a7a05-153">例如，您可以使用下列方式新增其他收件者：</span><span class="sxs-lookup"><span data-stu-id="a7a05-153">For example, you can add additional recipients by using</span></span>

    email.addTo('jeff@contoso.com');

<span data-ttu-id="a7a05-154">或使用下列方式設定篩選器：</span><span class="sxs-lookup"><span data-stu-id="a7a05-154">or set a filter by using</span></span>

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

<span data-ttu-id="a7a05-155">如需詳細資訊，請參閱[sendgrid nodejs][sendgrid-nodejs]。</span><span class="sxs-lookup"><span data-stu-id="a7a05-155">For more information, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="a7a05-156">如何：使用其他 SendGrid 服務</span><span class="sxs-lookup"><span data-stu-id="a7a05-156">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="a7a05-157">SendGrid 提供的網頁式 API 可供從 Azure 應用程式運用其他 SendGrid 功能。</span><span class="sxs-lookup"><span data-stu-id="a7a05-157">SendGrid offers web-based APIs that you can use to leverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="a7a05-158">如需完整詳細資料，請參閱 [SendGrid API 文件][SendGrid API documentation]。</span><span class="sxs-lookup"><span data-stu-id="a7a05-158">For full details, see the [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7a05-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a7a05-159">Next Steps</span></span>
<span data-ttu-id="a7a05-160">了解 SendGrid 電子郵件服務的基本概念後，請參考下列連結以取得更多資訊。</span><span class="sxs-lookup"><span data-stu-id="a7a05-160">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="a7a05-161">SendGrid Node.js 模組存放庫： [sendgrid nodejs][sendgrid-nodejs]</span><span class="sxs-lookup"><span data-stu-id="a7a05-161">SendGrid Node.js module repository: [sendgrid-nodejs][sendgrid-nodejs]</span></span>
* <span data-ttu-id="a7a05-162">SendGrid API 文件︰<https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="a7a05-162">SendGrid API documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="a7a05-163">Azure 客戶的 SendGrid 特別優惠：[http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span><span class="sxs-lookup"><span data-stu-id="a7a05-163">SendGrid special offer for Azure customers: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span></span>

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
<span data-ttu-id="a7a05-164">[雲端架構電子郵件服務]: https://sendgrid.com/email-solutions</span><span class="sxs-lookup"><span data-stu-id="a7a05-164">[cloud-based email service]: https://sendgrid.com/email-solutions</span></span>
<span data-ttu-id="a7a05-165">[交易式電子郵件傳遞]: https://sendgrid.com/transactional-email</span><span class="sxs-lookup"><span data-stu-id="a7a05-165">[transactional email delivery]: https://sendgrid.com/transactional-email</span></span>
