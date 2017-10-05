---
title: "使用角色來管理對 Azure 帳單的存取 | Microsoft Docs"
description: 
services: 
documentationcenter: 
author: vikramdesai01
manager: vikdesai
editor: 
tags: billing
ms.assetid: e4c4d136-2826-4938-868f-a7e67ff6b025
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: vikdesai
ms.openlocfilehash: c70904097f139bc2178feed83f1cf1274f3c738d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="manage-access-to-billing-information-for-azure-using-role-based-access-control"></a><span data-ttu-id="47a60-102">使用角色型存取控制來管理對 Azure 帳單資訊的存取</span><span class="sxs-lookup"><span data-stu-id="47a60-102">Manage access to billing information for Azure using role-based access control</span></span>

<span data-ttu-id="47a60-103">您可以透過將下列其中一個使用者角色指派給您的訂用帳戶，將 Azure 帳單資訊的存取權授與您的小組成員：帳戶管理員、服務管理員、共同管理員、擁有者、參與者，以及帳單讀者。</span><span class="sxs-lookup"><span data-stu-id="47a60-103">You can grant access for Azure billing information to members of your team by assigning one of the following user roles to your subscription: Account Administrator, Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader.</span></span> <span data-ttu-id="47a60-104">他們將可在 [Azure 入口網站](https://portal.azure.com/)中存取帳單資訊，並且可以使用[計費 API](billing-usage-rate-card-overview.md) 透過程式設計方式取得發票 (選擇加入後) 和使用量詳細資料。</span><span class="sxs-lookup"><span data-stu-id="47a60-104">They would have access to billing information in the [Azure portal](https://portal.azure.com/), and they can use the [Billing APIs](billing-usage-rate-card-overview.md) to programmatically get invoices (once opted-in) and usage details.</span></span> <span data-ttu-id="47a60-105">如需有關角色授權者及角色功能的詳細資訊，請參閱 [Azure RBAC 中的角色](../active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="47a60-105">For more information about who can grant roles, and which roles can do what, see [Roles in Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span></span>

## <span data-ttu-id="47a60-106"><a name="opt-in"></a> 允許額外的使用者存取發票</span><span class="sxs-lookup"><span data-stu-id="47a60-106"><a name="opt-in"></a> Allowing additional users to access invoices</span></span>

<span data-ttu-id="47a60-107">「帳戶管理員」必須使用 [Azure 入口網站](https://portal.azure.com/)來加入其他使用者，才能允許這些使用者及透過 API 存取發票。</span><span class="sxs-lookup"><span data-stu-id="47a60-107">The Account Administrator must opt in using the [Azure portal](https://portal.azure.com/) allow access to invoices for other users and via API.</span></span>

1. <span data-ttu-id="47a60-108">如果您是「帳戶管理員」，請從 Azure 入口網站中的 [[訂用帳戶] 刀鋒視窗](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="47a60-108">As the Account Administrator, select your subscription from the [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="47a60-109">選取 [發票]，然後選取 [存取發票]。</span><span class="sxs-lookup"><span data-stu-id="47a60-109">Select **Invoices** and then **Access to invoices**.</span></span>

    ![螢幕擷取畫面顯示如何委派存取發票](./media/billing-manage-access/AA-optin.png)

1. <span data-ttu-id="47a60-111">**開啟**存取權，然後儲存變更，以允許訂用帳戶限域角色中的使用者下載發票。</span><span class="sxs-lookup"><span data-stu-id="47a60-111">Turn **On** the access followed by saving the changes, to allow users in subscription scoped roles to download invoice.</span></span>

    ![螢幕擷取畫面顯示委派存取發票的開關](./media/billing-manage-access/AA-optinAllow.png)

<span data-ttu-id="47a60-113">加入即可讓訂用帳戶上的「服務管理員」、「共同管理員」、「擁有者」、「參與者」、「讀者」及「帳單讀者」在 Azure 入口網站中下載 PDF 發票。</span><span class="sxs-lookup"><span data-stu-id="47a60-113">Opting in allows Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader on the subscription to download PDF invoices in the Azure portal.</span></span> <span data-ttu-id="47a60-114">不過，2016 年 12 月以前的發票目前僅供「帳戶管理員」使用。</span><span class="sxs-lookup"><span data-stu-id="47a60-114">However, invoices older than December 2016 are available only to the Account Administrator for now.</span></span>

<span data-ttu-id="47a60-115">「帳戶管理員」也可以設定透過電子郵件傳送發票。</span><span class="sxs-lookup"><span data-stu-id="47a60-115">The Account Administrator can also configure to have invoices sent via email.</span></span> <span data-ttu-id="47a60-116">若要深入了解，請參閱[透過電子郵件取得發票](billing-download-azure-invoice-daily-usage-date.md)。</span><span class="sxs-lookup"><span data-stu-id="47a60-116">To learn more, see [Get your invoice in email](billing-download-azure-invoice-daily-usage-date.md).</span></span>

## <a name="adding-users-to-the-billing-reader-role"></a><span data-ttu-id="47a60-117">將使用者新增到帳單讀者角色</span><span class="sxs-lookup"><span data-stu-id="47a60-117">Adding users to the Billing Reader role</span></span>

<span data-ttu-id="47a60-118">「帳單讀者」角色可在 Azure 入口網站中以唯讀方式存取訂用帳戶帳單資訊，但無法存取 VM 和儲存體帳戶之類的服務。</span><span class="sxs-lookup"><span data-stu-id="47a60-118">The Billing Reader role has read-only access to subscription billing information in Azure portal, and no access to services such as VMs and storage accounts.</span></span> <span data-ttu-id="47a60-119">請將「帳單讀者」角色指派給需要存取訂用帳戶帳單資訊但不需要能夠管理 Azure 服務的使用者。</span><span class="sxs-lookup"><span data-stu-id="47a60-119">Assign the Billing Reader role to someone that needs access to the subscription billing information but not the ability to manage Azure services.</span></span> <span data-ttu-id="47a60-120">此角色適用於組織內只負責執行 Azure 訂用帳戶之財務和成本管理的使用者。</span><span class="sxs-lookup"><span data-stu-id="47a60-120">This role is appropriate for users in an organization who only perform financial and cost management for Azure subscriptions.</span></span>

1. <span data-ttu-id="47a60-121">從 Azure 入口網站中的 [[訂用帳戶] 刀鋒視窗](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="47a60-121">Select your subscription from the [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="47a60-122">選取 [存取控制 (IAM)]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="47a60-122">Select **Access control (IAM)** and then click **Add**.</span></span>

    ![顯示 [訂用帳戶] 刀鋒視窗中 IAM 的螢幕擷取畫面](./media/billing-manage-access/select-iam.PNG)

1. <span data-ttu-id="47a60-124">在 [選取角色] 頁面中，選取 [帳單讀者]。</span><span class="sxs-lookup"><span data-stu-id="47a60-124">Choose **Billing Reader** in the **Select a role** page.</span></span>

    ![顯示快顯檢視中 [帳單讀者] 的螢幕擷取畫面](./media/billing-manage-access/select-roles.PNG)

1. <span data-ttu-id="47a60-126">輸入您想要邀請之使用者的電子郵件，然後按一下 [確定] 以傳送邀請。</span><span class="sxs-lookup"><span data-stu-id="47a60-126">Type the email for the user you want to invite, then click **OK** to send the invitation.</span></span>

    ![顯示輸入電子郵件以邀請某位使用者的螢幕擷取畫面](./media/billing-manage-access/add-user.PNG)

1. <span data-ttu-id="47a60-128">依照邀請電子郵件中的指示，以「帳單讀者」身分登入。</span><span class="sxs-lookup"><span data-stu-id="47a60-128">Follow instructions in the invite email to log in as a Billing Reader.</span></span>

    ![顯示「帳單讀者」在 Azure 入口網站中可見內容的螢幕擷取畫面](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> <span data-ttu-id="47a60-130">「帳單讀者」功能目前為預覽版，尚未支援企業 (EA) 訂用帳戶或非全球雲端。</span><span class="sxs-lookup"><span data-stu-id="47a60-130">The Billing Reader feature is in preview, and does not yet support enterprise (EA) subscriptions or non-global clouds.</span></span>

## <a name="adding-users-to-other-roles"></a><span data-ttu-id="47a60-131">將使用者新增到其他角色</span><span class="sxs-lookup"><span data-stu-id="47a60-131">Adding users to other roles</span></span>

<span data-ttu-id="47a60-132">具備其他角色 (例如「擁有者」和「參與者」) 的使用者不僅可存取帳單資訊，還可存取 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="47a60-132">Users in other roles, such as Owner or Contributor, can access not just billing information, but Azure services as well.</span></span> <span data-ttu-id="47a60-133">若要管理這些角色，請參閱[新增或變更管理訂用帳戶或服務的 Azure 系統管理員角色](billing-add-change-azure-subscription-administrator.md)。</span><span class="sxs-lookup"><span data-stu-id="47a60-133">To manage these roles, see [Add or change Azure administrator roles that manage the subscription or services](billing-add-change-azure-subscription-administrator.md).</span></span>

## <a name="who-can-access-the-account-centerhttpsaccountwindowsazurecom"></a><span data-ttu-id="47a60-134">誰可以存取[帳戶中心](https://account.windowsazure.com)？</span><span class="sxs-lookup"><span data-stu-id="47a60-134">Who can access the [Account Center](https://account.windowsazure.com)?</span></span>

<span data-ttu-id="47a60-135">只有「帳戶管理員」可以登入「帳戶中心」。</span><span class="sxs-lookup"><span data-stu-id="47a60-135">Only the Account Administrator can log in to the Account center.</span></span> <span data-ttu-id="47a60-136">「帳戶管理員」是訂用帳戶的法定擁有者。</span><span class="sxs-lookup"><span data-stu-id="47a60-136">The Account Administrator is the legal owner of the subscription.</span></span> <span data-ttu-id="47a60-137">註冊或購買 Azure 訂用帳戶的人員預設即是「帳戶管理員」，除非[已將訂用帳戶擁有權轉移](billing-subscription-transfer.md)給其他人。</span><span class="sxs-lookup"><span data-stu-id="47a60-137">By default, the person who signed up for or bought the Azure subscription is the Account Administrator, unless the [subscription ownership was transferred](billing-subscription-transfer.md) to somebody else.</span></span> <span data-ttu-id="47a60-138">「帳戶管理員」可以建立訂用帳戶、取消訂用帳戶、變更訂用帳戶的帳單地址，以及管理訂用帳戶的存取原則。</span><span class="sxs-lookup"><span data-stu-id="47a60-138">The Account Administrator can create subscriptions, cancel subscriptions, change the billing address for a subscription, and manage access policies for the subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="47a60-139">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="47a60-139">Need help?</span></span> <span data-ttu-id="47a60-140">請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="47a60-140">Contact support.</span></span>

<span data-ttu-id="47a60-141">如果您仍有其他問題，請[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)以快速解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="47a60-141">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
