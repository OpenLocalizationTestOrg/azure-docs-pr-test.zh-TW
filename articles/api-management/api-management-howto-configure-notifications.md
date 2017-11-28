---
title: "aaaConfigure 通知和電子郵件範本，在 Azure API 管理 |Microsoft 文件"
description: "深入了解如何 tooconfigure 通知和電子郵件範本，在 Azure API 管理。"
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
ms.openlocfilehash: dc23289c25a1641992b73cb955099b3f207b6968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-notifications-and-email-templates-in-azure-api-management"></a><span data-ttu-id="73002-103">如何 tooconfigure 通知和電子郵件範本，在 Azure API 管理</span><span class="sxs-lookup"><span data-stu-id="73002-103">How tooconfigure notifications and email templates in Azure API Management</span></span>
<span data-ttu-id="73002-104">API 管理提供 hello 能力 tooconfigure 通知的特定事件及 tooconfigure hello 電子郵件範本，而且使用的 toocommunicate 與 hello 管理員和開發人員的 API 管理執行個體。</span><span class="sxs-lookup"><span data-stu-id="73002-104">API Management provides hello ability tooconfigure notifications for specific events, and tooconfigure hello email templates that are used toocommunicate with hello administrators and developers of an API Management instance.</span></span> <span data-ttu-id="73002-105">本主題說明如何 tooconfigure 通知 hello 可用的事件，並提供設定使用這些事件的 hello 電子郵件範本的概觀。</span><span class="sxs-lookup"><span data-stu-id="73002-105">This topic shows how tooconfigure notifications for hello available events, and provides an overview of configuring hello email templates used for these events.</span></span>

## <span data-ttu-id="73002-106"><a name="publisher-notifications"> </a>設定發行者通知</span><span class="sxs-lookup"><span data-stu-id="73002-106"><a name="publisher-notifications"> </a>Configure publisher notifications</span></span>
<span data-ttu-id="73002-107">按一下 tooconfigure 通知**發行者入口網站**API 管理服務的 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="73002-107">tooconfigure notifications, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="73002-108">這會帶您 toohello API 管理發行者入口網站。</span><span class="sxs-lookup"><span data-stu-id="73002-108">This takes you toohello API Management publisher portal.</span></span>

![發行者入口網站][api-management-management-console]

> [!NOTE] 
> <span data-ttu-id="73002-110">如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[開始使用 Azure API 管理][Get started with Azure API Management]教學課程。</span><span class="sxs-lookup"><span data-stu-id="73002-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

<span data-ttu-id="73002-111">按一下**通知**從 hello **API 管理**hello 功能表左 tooview hello 可用的通知。</span><span class="sxs-lookup"><span data-stu-id="73002-111">Click **Notifications** from hello **API Management** menu on hello left tooview hello available notifications.</span></span>

![Publisher notifications][api-management-publisher-notifications]

<span data-ttu-id="73002-113">hello 下列事件的清單可以設定通知。</span><span class="sxs-lookup"><span data-stu-id="73002-113">hello following list of events can be configured for notifications.</span></span>

* <span data-ttu-id="73002-114">**（需要核准） 的訂用帳戶要求**-hello 指定的電子郵件收件者和使用者會收到電子郵件通知訂閱要求的應用程式開發介面需要核准的產品。</span><span class="sxs-lookup"><span data-stu-id="73002-114">**Subscription requests (requiring approval)** - hello specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span></span>
* <span data-ttu-id="73002-115">**新的訂閱**-hello 指定的電子郵件收件者和使用者會收到有關新的應用程式開發介面產品訂閱電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="73002-115">**New subscriptions** - hello specified email recipients and users will receive email notifications about new API product subscriptions.</span></span>
* <span data-ttu-id="73002-116">**組件庫的應用程式要求**-hello 指定的電子郵件收件者，並提交的 toohello 應用程式庫，新的應用程式時，使用者會收到電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="73002-116">**Application gallery requests** - hello specified email recipients and users will receive email notifications when new applications are submitted toohello application gallery.</span></span>
* <span data-ttu-id="73002-117">**密件副本**-hello 指定的電子郵件收件者和使用者會收到電子郵件密件副本的所有傳送的電子郵件 toodevelopers。</span><span class="sxs-lookup"><span data-stu-id="73002-117">**BCC** - hello specified email recipients and users will receive email blind carbon copies of all emails sent toodevelopers.</span></span>
* <span data-ttu-id="73002-118">**新問題或評論**-hello 指定的電子郵件收件者和使用者會收到電子郵件通知時新問題或意見送出 hello 開發人員入口網站上。</span><span class="sxs-lookup"><span data-stu-id="73002-118">**New issue or comment** - hello specified email recipients and users will receive email notifications when a new issue or comment is submitted on hello developer portal.</span></span>
* <span data-ttu-id="73002-119">**關閉帳戶訊息**-hello 指定的電子郵件收件者，並關閉帳戶時，使用者會收到電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="73002-119">**Close account message** - hello specified email recipients and users will receive email notifications when an account is closed.</span></span>
* <span data-ttu-id="73002-120">**接近的訂用帳戶配額限制**-hello 遵循電子郵件收件者和使用者會收到電子郵件通知訂用帳戶使用量取得關閉 toousage 配額。</span><span class="sxs-lookup"><span data-stu-id="73002-120">**Approaching subscription quota limit** - hello following email recipients and users will receive email notifications when subscription usage gets close toousage quota.</span></span>

<span data-ttu-id="73002-121">針對每個事件，您可以指定電子郵件收件者使用 hello 電子郵件位址 文字方塊中，或從清單中選取使用者。</span><span class="sxs-lookup"><span data-stu-id="73002-121">For each event, you can specify email recipients using hello email address text box or you can select users from a list.</span></span>

<span data-ttu-id="73002-122">toospecify hello 電子郵件地址 toobe 收到通知，請在 [hello 電子郵件地址] 文字方塊中輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="73002-122">toospecify hello email addresses toobe notified, enter them in hello email address text box.</span></span> <span data-ttu-id="73002-123">如果您有多個電子郵件地址，請以逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="73002-123">If you have multiple email addresses, separate them using commas.</span></span>

![Notification recipients][api-management-email-addresses]

<span data-ttu-id="73002-125">toospecify hello 使用者 toobe 收到通知，請按一下**加入收件者**，核取 hello hello 使用者 toobe 通知時，旁邊的方塊，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="73002-125">toospecify hello users toobe notified, click **add recipient**, check hello box beside hello users toobe notified, and click **OK**.</span></span>

> [!NOTE] 
> <span data-ttu-id="73002-126">只有系統管理員會顯示在 [hello] 清單中。</span><span class="sxs-lookup"><span data-stu-id="73002-126">Only administrators are displayed in hello list.</span></span>


<span data-ttu-id="73002-127">設定後 hello 通知收件者，請按一下**儲存**tooapply hello 更新通知收件者。</span><span class="sxs-lookup"><span data-stu-id="73002-127">After configuring hello notification recipients, click **Save** tooapply hello updated notification recipients.</span></span>

> [!NOTE] 
> <span data-ttu-id="73002-128">如果您離開 hello**發行者通知** 索引標籤 hello 發行者入口網站會提醒您若那里未儲存的變更。</span><span class="sxs-lookup"><span data-stu-id="73002-128">If you navigate away from hello **Publisher Notifications** tab hello publisher portal alerts you if there are unsaved changes.</span></span>


## <span data-ttu-id="73002-129"><a name="email-templates"> </a>設定電子郵件範本</span><span class="sxs-lookup"><span data-stu-id="73002-129"><a name="email-templates"> </a>Configure email templates</span></span>
<span data-ttu-id="73002-130">API 管理提供電子郵件範本 hello 在 hello 課程中的管理和使用 hello 服務所傳送的電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="73002-130">API Management provides email templates for hello email messages that are sent in hello course of administering and using hello service.</span></span> <span data-ttu-id="73002-131">提供下列電子郵件範本的 hello。</span><span class="sxs-lookup"><span data-stu-id="73002-131">hello following email templates are provided.</span></span>

* <span data-ttu-id="73002-132">已核准應用程式庫提交</span><span class="sxs-lookup"><span data-stu-id="73002-132">Application gallery submission approved</span></span>
* <span data-ttu-id="73002-133">開發人員離職信</span><span class="sxs-lookup"><span data-stu-id="73002-133">Developer farewell letter</span></span>
* <span data-ttu-id="73002-134">開發人員接近配額限制通知</span><span class="sxs-lookup"><span data-stu-id="73002-134">Developer quota limit approaching notification</span></span>
* <span data-ttu-id="73002-135">邀請使用者</span><span class="sxs-lookup"><span data-stu-id="73002-135">Invite user</span></span>
* <span data-ttu-id="73002-136">將新的註解加入 tooan 問題</span><span class="sxs-lookup"><span data-stu-id="73002-136">New comment added tooan issue</span></span>
* <span data-ttu-id="73002-137">收到新的問題</span><span class="sxs-lookup"><span data-stu-id="73002-137">New issue received</span></span>
* <span data-ttu-id="73002-138">已啟用新的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="73002-138">New subscription activated</span></span>
* <span data-ttu-id="73002-139">確認訂用帳戶已更新</span><span class="sxs-lookup"><span data-stu-id="73002-139">Subscription renewed confirmation</span></span>
* <span data-ttu-id="73002-140">拒絕訂用帳戶要求</span><span class="sxs-lookup"><span data-stu-id="73002-140">Subscription request declines</span></span>
* <span data-ttu-id="73002-141">收到訂用帳戶要求</span><span class="sxs-lookup"><span data-stu-id="73002-141">Subscription request received</span></span>

<span data-ttu-id="73002-142">可依需要修改這些範本。</span><span class="sxs-lookup"><span data-stu-id="73002-142">These templates can be modified as desired.</span></span>

<span data-ttu-id="73002-143">tooview 並設定您的 API 管理執行個體的 hello 電子郵件範本，請按一下**通知**從 hello **API 管理**功能表靠左、 hello 和選取 hello**電子郵件範本**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="73002-143">tooview and configure hello email templates for your API Management instance, click **Notifications** from hello **API Management** menu on hello left, and select hello **Email Templates** tab.</span></span>

![Email templates][api-management-email-templates]

<span data-ttu-id="73002-145">tooview 或修改特定範本，請選取從 hello**範本**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="73002-145">tooview or modify a specific template, select it from hello **Templates** drop-down list.</span></span>

![Email templates list][api-management-email-templates-list]

<span data-ttu-id="73002-147">每一個電子郵件範本都有純文字的主旨，以及 HTML 格式的本文定義。</span><span class="sxs-lookup"><span data-stu-id="73002-147">Each email template has a subject in plain text, and a body definition in HTML format.</span></span> <span data-ttu-id="73002-148">可依需要自訂每一個項目。</span><span class="sxs-lookup"><span data-stu-id="73002-148">Each item can be customized as desired.</span></span>

![Email template editor][api-management-email-template]

<span data-ttu-id="73002-150">hello**參數**清單包含清單的參數，當插入 hello 主旨或內文，傳送嗨電子郵件時，將會取代的 hello 指定值。</span><span class="sxs-lookup"><span data-stu-id="73002-150">hello **Parameters** list contains a list of parameters, which when inserted into hello subject or body, will be replaced hello designated value when hello email is sent.</span></span> <span data-ttu-id="73002-151">tooinsert 參數，將您想 hello 參數 toogo，並按一下 hello 箭號 toohello hello 參數名稱左邊的 hello 游標。</span><span class="sxs-lookup"><span data-stu-id="73002-151">tooinsert a parameter, place hello cursor where you wish hello parameter toogo, and click hello arrow toohello left of hello parameter name.</span></span>

<span data-ttu-id="73002-152">按一下**預覽**或**傳送測試**toosee 如何 hello 電子郵件將會尋找或傳送測試電子郵件。</span><span class="sxs-lookup"><span data-stu-id="73002-152">Click **Preview** or **Send a test** toosee how hello email will look or send a test email.</span></span>

> [!NOTE] 
> <span data-ttu-id="73002-153">hello 參數未取代成實際的值，當在預覽或傳送的測試。</span><span class="sxs-lookup"><span data-stu-id="73002-153">hello parameters are not replaced with actual values when previewing or sending a test.</span></span>

<span data-ttu-id="73002-154">toosave hello 變更 toohello 電子郵件範本，按一下 **儲存**，或按一下 toocancel hello 變更**取消**。</span><span class="sxs-lookup"><span data-stu-id="73002-154">toosave hello changes toohello email template, click **Save**, or toocancel hello changes click **Cancel**.</span></span>
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
