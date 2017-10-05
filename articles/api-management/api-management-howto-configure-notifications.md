---
title: "在 Azure API 管理中設定通知和電子郵件範本 | Microsoft Docs"
description: "了解如何在 Azure API 管理中設定通知和電子郵件範本。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: ee25f26d-4752-433b-af9c-3817db38aed5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 3d8b74e32059cfc1a4c3a8fc7d3bd04676ee80c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-notifications-and-email-templates-in-azure-api-management"></a><span data-ttu-id="ac50a-103">如何在 Azure API 管理中設定通知和電子郵件範本</span><span class="sxs-lookup"><span data-stu-id="ac50a-103">How to configure notifications and email templates in Azure API Management</span></span>
<span data-ttu-id="ac50a-104">API 管理可讓您設定特定事件的通知，以及設定用來與 API 管理執行個體的管理員和開發人員通訊的電子郵件範本。</span><span class="sxs-lookup"><span data-stu-id="ac50a-104">API Management provides the ability to configure notifications for specific events, and to configure the email templates that are used to communicate with the administrators and developers of an API Management instance.</span></span> <span data-ttu-id="ac50a-105">本主題說明如何為可用的事件設定通知，並提供設定這些事件所使用之電子郵件範本的概觀。</span><span class="sxs-lookup"><span data-stu-id="ac50a-105">This topic shows how to configure notifications for the available events, and provides an overview of configuring the email templates used for these events.</span></span>

## <span data-ttu-id="ac50a-106"><a name="publisher-notifications"> </a>設定發行者通知</span><span class="sxs-lookup"><span data-stu-id="ac50a-106"><a name="publisher-notifications"> </a>Configure publisher notifications</span></span>
<span data-ttu-id="ac50a-107">若要設定通知，請在您「API 管理」服務的「Azure 入口網站」中按一下 [發行者入口網站]。</span><span class="sxs-lookup"><span data-stu-id="ac50a-107">To configure notifications, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="ac50a-108">這會帶您前往 API 管理發行者入口網站。</span><span class="sxs-lookup"><span data-stu-id="ac50a-108">This takes you to the API Management publisher portal.</span></span>

![發行者入口網站][api-management-management-console]

> [!NOTE] 
> <span data-ttu-id="ac50a-110">如果您尚未建立 API 管理服務執行個體，請參閱[開始使用 Azure API 管理][Get started with Azure API Management]教學課程中的[建立 API 管理服務執行個體][Create an API Management service instance]。</span><span class="sxs-lookup"><span data-stu-id="ac50a-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

<span data-ttu-id="ac50a-111">從左邊的 [API 管理] 功能表中按一下 [通知]，以檢視可用的通知。</span><span class="sxs-lookup"><span data-stu-id="ac50a-111">Click **Notifications** from the **API Management** menu on the left to view the available notifications.</span></span>

![Publisher notifications][api-management-publisher-notifications]

<span data-ttu-id="ac50a-113">下列事件清單可設定通知。</span><span class="sxs-lookup"><span data-stu-id="ac50a-113">The following list of events can be configured for notifications.</span></span>

* <span data-ttu-id="ac50a-114">**訂用帳戶要求 (需要核准)** - 關於需要核准的 API 產品訂用帳戶要求，指定的電子郵件收件者和使用者會收到電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="ac50a-114">**Subscription requests (requiring approval)** - The specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span></span>
* <span data-ttu-id="ac50a-115">**新的訂用帳戶** - 關於新的 API 產品訂用帳戶，指定的電子郵件收件者和使用者會收到電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="ac50a-115">**New subscriptions** - The specified email recipients and users will receive email notifications about new API product subscriptions.</span></span>
* <span data-ttu-id="ac50a-116">**應用程式庫要求** - 當新的應用程式提交至應用程式庫時，指定的電子郵件收件者和使用者會收到電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="ac50a-116">**Application gallery requests** - The specified email recipients and users will receive email notifications when new applications are submitted to the application gallery.</span></span>
* <span data-ttu-id="ac50a-117">**BCC** - 指定的電子郵件收件者和使用者會收到所有寄給開發人員的電子郵件的密件副本。</span><span class="sxs-lookup"><span data-stu-id="ac50a-117">**BCC** - The specified email recipients and users will receive email blind carbon copies of all emails sent to developers.</span></span>
* <span data-ttu-id="ac50a-118">**新的問題或意見** - 當開發人員入口網站上提出新的問題或意見時，指定的電子郵件收件者和使用者會收到電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="ac50a-118">**New issue or comment** - The specified email recipients and users will receive email notifications when a new issue or comment is submitted on the developer portal.</span></span>
* <span data-ttu-id="ac50a-119">**關閉帳戶訊息** - 有帳戶關閉時，指定的電子郵件收件者和使用者會收到電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="ac50a-119">**Close account message** - The specified email recipients and users will receive email notifications when an account is closed.</span></span>
* <span data-ttu-id="ac50a-120">**接近訂用帳戶配額限制** - 當訂用帳戶使用量接近使用量配額時，下列電子郵件收件者和使用者會收到電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="ac50a-120">**Approaching subscription quota limit** - The following email recipients and users will receive email notifications when subscription usage gets close to usage quota.</span></span>

<span data-ttu-id="ac50a-121">針對每一個事件，您可以使用電子郵件地址文字方塊來指定電子郵件地址，或從清單中選取使用者。</span><span class="sxs-lookup"><span data-stu-id="ac50a-121">For each event, you can specify email recipients using the email address text box or you can select users from a list.</span></span>

<span data-ttu-id="ac50a-122">若要指定要通知的電子郵件地址，請在電子郵件地址文字方塊中輸入。</span><span class="sxs-lookup"><span data-stu-id="ac50a-122">To specify the email addresses to be notified, enter them in the email address text box.</span></span> <span data-ttu-id="ac50a-123">如果您有多個電子郵件地址，請以逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="ac50a-123">If you have multiple email addresses, separate them using commas.</span></span>

![Notification recipients][api-management-email-addresses]

<span data-ttu-id="ac50a-125">若要指定要通知的使用者，請按一下 [新增收件者]，選取要通知之使用者旁邊的核取方塊，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ac50a-125">To specify the users to be notified, click **add recipient**, check the box beside the users to be notified, and click **OK**.</span></span>

> [!NOTE] 
> <span data-ttu-id="ac50a-126">清單中只會顯示系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ac50a-126">Only administrators are displayed in the list.</span></span>


<span data-ttu-id="ac50a-127">設定通知收件者之後，按一下 [儲存]  ，套用已更新的通知收件者。</span><span class="sxs-lookup"><span data-stu-id="ac50a-127">After configuring the notification recipients, click **Save** to apply the updated notification recipients.</span></span>

> [!NOTE] 
> <span data-ttu-id="ac50a-128">如果您離開 [發行者通知]  索引標籤，發行者入口網站會警告有未儲存的變更。</span><span class="sxs-lookup"><span data-stu-id="ac50a-128">If you navigate away from the **Publisher Notifications** tab the publisher portal alerts you if there are unsaved changes.</span></span>


## <span data-ttu-id="ac50a-129"><a name="email-templates"> </a>設定電子郵件範本</span><span class="sxs-lookup"><span data-stu-id="ac50a-129"><a name="email-templates"> </a>Configure email templates</span></span>
<span data-ttu-id="ac50a-130">對於管理和使用服務期間傳送的電子郵件訊息，API 管理提供電子郵件範本。</span><span class="sxs-lookup"><span data-stu-id="ac50a-130">API Management provides email templates for the email messages that are sent in the course of administering and using the service.</span></span> <span data-ttu-id="ac50a-131">提供的電子郵件範本如下。</span><span class="sxs-lookup"><span data-stu-id="ac50a-131">The following email templates are provided.</span></span>

* <span data-ttu-id="ac50a-132">已核准應用程式庫提交</span><span class="sxs-lookup"><span data-stu-id="ac50a-132">Application gallery submission approved</span></span>
* <span data-ttu-id="ac50a-133">開發人員離職信</span><span class="sxs-lookup"><span data-stu-id="ac50a-133">Developer farewell letter</span></span>
* <span data-ttu-id="ac50a-134">開發人員接近配額限制通知</span><span class="sxs-lookup"><span data-stu-id="ac50a-134">Developer quota limit approaching notification</span></span>
* <span data-ttu-id="ac50a-135">邀請使用者</span><span class="sxs-lookup"><span data-stu-id="ac50a-135">Invite user</span></span>
* <span data-ttu-id="ac50a-136">問題中加入新的意見</span><span class="sxs-lookup"><span data-stu-id="ac50a-136">New comment added to an issue</span></span>
* <span data-ttu-id="ac50a-137">收到新的問題</span><span class="sxs-lookup"><span data-stu-id="ac50a-137">New issue received</span></span>
* <span data-ttu-id="ac50a-138">已啟用新的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ac50a-138">New subscription activated</span></span>
* <span data-ttu-id="ac50a-139">確認訂用帳戶已更新</span><span class="sxs-lookup"><span data-stu-id="ac50a-139">Subscription renewed confirmation</span></span>
* <span data-ttu-id="ac50a-140">拒絕訂用帳戶要求</span><span class="sxs-lookup"><span data-stu-id="ac50a-140">Subscription request declines</span></span>
* <span data-ttu-id="ac50a-141">收到訂用帳戶要求</span><span class="sxs-lookup"><span data-stu-id="ac50a-141">Subscription request received</span></span>

<span data-ttu-id="ac50a-142">可依需要修改這些範本。</span><span class="sxs-lookup"><span data-stu-id="ac50a-142">These templates can be modified as desired.</span></span>

<span data-ttu-id="ac50a-143">若要檢視和設定 API 管理執行個體的電子郵件範本，請從左邊的 [API 管理] 功能表中按一下 [通知]，然後選取 [電子郵件範本] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ac50a-143">To view and configure the email templates for your API Management instance, click **Notifications** from the **API Management** menu on the left, and select the **Email Templates** tab.</span></span>

![Email templates][api-management-email-templates]

<span data-ttu-id="ac50a-145">若要檢視或修改特定的範本，請從 [範本]  下拉式清單中選取它。</span><span class="sxs-lookup"><span data-stu-id="ac50a-145">To view or modify a specific template, select it from the **Templates** drop-down list.</span></span>

![Email templates list][api-management-email-templates-list]

<span data-ttu-id="ac50a-147">每一個電子郵件範本都有純文字的主旨，以及 HTML 格式的本文定義。</span><span class="sxs-lookup"><span data-stu-id="ac50a-147">Each email template has a subject in plain text, and a body definition in HTML format.</span></span> <span data-ttu-id="ac50a-148">可依需要自訂每一個項目。</span><span class="sxs-lookup"><span data-stu-id="ac50a-148">Each item can be customized as desired.</span></span>

![Email template editor][api-management-email-template]

<span data-ttu-id="ac50a-150">[參數]  清單包含一份參數清單，當插入至主旨或本文時，則會在傳送電子郵件時取代為指定的值。</span><span class="sxs-lookup"><span data-stu-id="ac50a-150">The **Parameters** list contains a list of parameters, which when inserted into the subject or body, will be replaced the designated value when the email is sent.</span></span> <span data-ttu-id="ac50a-151">若要插入參數，請將游標移至您要放置參數的地方，然後按一下參數名稱左邊的箭頭。</span><span class="sxs-lookup"><span data-stu-id="ac50a-151">To insert a parameter, place the cursor where you wish the parameter to go, and click the arrow to the left of the parameter name.</span></span>

<span data-ttu-id="ac50a-152">按一下 [預覽] 或 [傳送測試]，以預覽電子郵件的內容或傳送測試電子郵件。</span><span class="sxs-lookup"><span data-stu-id="ac50a-152">Click **Preview** or **Send a test** to see how the email will look or send a test email.</span></span>

> [!NOTE] 
> <span data-ttu-id="ac50a-153">預覽或傳送測試時，不會以實際值來取代參數。</span><span class="sxs-lookup"><span data-stu-id="ac50a-153">The parameters are not replaced with actual values when previewing or sending a test.</span></span>

<span data-ttu-id="ac50a-154">若要儲存電子郵件範本的變更，請按一下 [儲存]，若要取消變更，請按一下 [取消]。</span><span class="sxs-lookup"><span data-stu-id="ac50a-154">To save the changes to the email template, click **Save**, or to cancel the changes click **Cancel**.</span></span>
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
