---
title: "新增或變更 Azure 系統管理員訂用帳戶角色| Microsoft Docs"
description: "說明如何新增或變更 Azure 共同管理員、服務管理員和帳戶管理員"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: 13a72d76-e043-4212-bcac-a35f4a27ee26
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: genli
ms.openlocfilehash: da5995535d42ed52772cb09e0f4da51bbf878748
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="add-or-change-azure-administrator-roles-that-manage-the-subscription-or-services"></a><span data-ttu-id="4b456-103">新增或變更管理訂用帳戶或服務的 Azure 系統管理員角色</span><span class="sxs-lookup"><span data-stu-id="4b456-103">Add or change Azure administrator roles that manage the subscription or services</span></span>
<span data-ttu-id="4b456-104">您可以變更管理您的 Azure 訂用帳戶或訂用帳戶中所使用 Azure 服務的 Azure 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="4b456-104">You can change the Azure administrator that manages your Azure subscription or manages the Azure services used in your subscription.</span></span> <span data-ttu-id="4b456-105">若要檢視 Azure 帳單資訊及管理訂用帳戶，您必須以帳戶管理員的身分登入[帳戶中心](https://account.windowsazure.com/Home/Index)。</span><span class="sxs-lookup"><span data-stu-id="4b456-105">To view Azure billing information and manage subscriptions, you must sign in to the [Account Center](https://account.windowsazure.com/Home/Index) as the Account Administrator.</span></span> 

## <a name="add-an-admin-for-a-subscription"></a><span data-ttu-id="4b456-106">新增訂用帳戶的管理員</span><span class="sxs-lookup"><span data-stu-id="4b456-106">Add an admin for a subscription</span></span>
<span data-ttu-id="4b456-107">您可以在 Azure 入口網站或 Azure 傳統入口網站新增 Azure 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="4b456-107">You can add an Azure administrator in the Azure portal or in the Azure classic portal.</span></span>

<span data-ttu-id="4b456-108">**Azure 入口網站**</span><span class="sxs-lookup"><span data-stu-id="4b456-108">**Azure portal**</span></span>

<span data-ttu-id="4b456-109">若要在 Azure 入口網站中將某人新增為訂用帳戶的系統管理員，請賦予他擁有者角色。</span><span class="sxs-lookup"><span data-stu-id="4b456-109">To add someone as an admin for a subscription in the Azure portal, you give them the owner role.</span></span> <span data-ttu-id="4b456-110">擁有者角色只能管理您指派之訂用帳戶中的資源。</span><span class="sxs-lookup"><span data-stu-id="4b456-110">The owner role can only manage the resources in the subscription that you assigned.</span></span> <span data-ttu-id="4b456-111">此系統管理員沒有其他訂用帳戶的存取權限。</span><span class="sxs-lookup"><span data-stu-id="4b456-111">It doesn't have access privilege to other subscriptions.</span></span> <span data-ttu-id="4b456-112">您透過 [Azure 入口網站](https://portal.azure.com)新增的擁有者無法管理 [Azure 傳統入口網站](https://manage.windowsazure.com)中的資源。</span><span class="sxs-lookup"><span data-stu-id="4b456-112">The owners you add through the [Azure portal](https://portal.azure.com) can't manage resource in the [Azure classic portal](https://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="4b456-113">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="4b456-113">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4b456-114">在 [中樞] 功能表中，選取 [訂用帳戶] > *您想要讓管理員存取的訂用帳戶*。</span><span class="sxs-lookup"><span data-stu-id="4b456-114">On the Hub menu, select **Subscription** > *the subscription that you want the admin to access*.</span></span>

    ![顯示已選取訂用帳戶選項的螢幕擷取畫面](./media/billing-add-change-azure-subscription-administrator/newselectsub.png)

3. <span data-ttu-id="4b456-116">在 [訂用帳戶] 刀鋒視窗中，選取 [存取控制 (IAM)]。</span><span class="sxs-lookup"><span data-stu-id="4b456-116">In the subscription blade, select **Access control (IAM)**.</span></span>
4. <span data-ttu-id="4b456-117">選取 [新增] > [角色] > [擁有者]。</span><span class="sxs-lookup"><span data-stu-id="4b456-117">Select **Add** > **Role** > **Owner**.</span></span> <span data-ttu-id="4b456-118">輸入您想要新增為擁有者的使用者的電子郵件地址，選取使用者，再選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="4b456-118">Type the email address of the user you want to add as owner, select the user, and then select **Save**.</span></span>

    ![顯示已選取 [擁有者] 角色的螢幕擷取畫面](./media/billing-add-change-azure-subscription-administrator/add-role.png)

5. <span data-ttu-id="4b456-120">如果想要新增擁有者帳戶作為共同管理員，請在 [存取控制 (IAM)] 頁面上，以滑鼠右鍵按一下使用者，然後選取 [新增為共同管理員]。</span><span class="sxs-lookup"><span data-stu-id="4b456-120">If you want to add the owner account as co-administrator, in the  **Access control (IAM)** page, right-click the user and then select **Add as co-administrator**.</span></span> <span data-ttu-id="4b456-121">[Azure 預覽入口網站](https://preview.portal.azure.com/)現提供此功能。</span><span class="sxs-lookup"><span data-stu-id="4b456-121">This feature is now available on [Azure preview portal](https://preview.portal.azure.com/).</span></span> 

     ![新增共同管理員的螢幕擷取畫面](./media/billing-add-change-azure-subscription-administrator/add-coadmin.png)

    >[!TIP]
    ><span data-ttu-id="4b456-123">如果使用者需要在 [Azure 傳統入口網站](https://manage.windowsazure.com/)上管理 Azure 服務，您需要將「擁有者」使用者新增為共同管理員。</span><span class="sxs-lookup"><span data-stu-id="4b456-123">You will need to add the "Owner" user as co-administrator if the user needs to manage the Azure services in [Azure classic portal](https://manage.windowsazure.com/).</span></span>

    <span data-ttu-id="4b456-124">若要移除共同管理員權限，請以滑鼠右鍵按一下「共同管理員」使用者，然後選取 [移除共同管理員]。</span><span class="sxs-lookup"><span data-stu-id="4b456-124">To remove the co-administrator permission, right-click the "co-administrator" user and then select **Remove co-administrator**.</span></span>

    ![移除共同管理員的螢幕擷取畫面](./media/billing-add-change-azure-subscription-administrator/remove-coadmin.png)


<span data-ttu-id="4b456-126">**Azure 傳統入口網站**</span><span class="sxs-lookup"><span data-stu-id="4b456-126">**Azure classic portal**</span></span>

1. <span data-ttu-id="4b456-127">登入 [Azure 傳統入口網站](https://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="4b456-127">Sign in to the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="4b456-128">在導覽窗格中，選取 [設定]> [管理員]> [新增]。</span><span class="sxs-lookup"><span data-stu-id="4b456-128">In the navigation pane, select **Settings**> **Administrators**> **Add**.</span></span> </br>

    ![顯示如何存取 [新增] 按鈕的螢幕擷取畫面](./media/billing-add-change-azure-subscription-administrator/addcoadmin.png)
3. <span data-ttu-id="4b456-130">輸入您想新增為共同管理員之人員的電子郵件地址，然後選取您想讓共同管理員存取的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4b456-130">Type the email address of the person you want to add as Co-administrator and then select the subscription that you want the Co-administrator to access.</span></span></br>

    ![<span data-ttu-id="4b456-131">顯示已選取訂用帳戶選項的螢幕擷取畫面</span><span class="sxs-lookup"><span data-stu-id="4b456-131">Screenshot that shows a subscription selected</span></span> ](./media/billing-add-change-azure-subscription-administrator/addcoadmin2.png)</br>

<span data-ttu-id="4b456-132">下列電子郵件地址可以新增為共同管理員：</span><span class="sxs-lookup"><span data-stu-id="4b456-132">The following email address can be added as a Co-Administrator:</span></span>

* <span data-ttu-id="4b456-133">**Microsoft 帳戶** (先前的 Windows Live ID)</span><span class="sxs-lookup"><span data-stu-id="4b456-133">**Microsoft Account** (formerly Windows Live ID)</span></span> </br>
  <span data-ttu-id="4b456-134">您可以使用 Microsoft 帳戶登入所有消費者導向的 Microsoft 產品和雲端服務，例如 Outlook (Hotmail)、Skype (MSN)、OneDrive、Windows Phone 和 Xbox LIVE。</span><span class="sxs-lookup"><span data-stu-id="4b456-134">You can use a Microsoft Account to sign in to all consumer-oriented Microsoft products and cloud services, such as Outlook (Hotmail), Skype (MSN), OneDrive, Windows Phone, and Xbox LIVE.</span></span>
* <span data-ttu-id="4b456-135">**Organizational account**</span><span class="sxs-lookup"><span data-stu-id="4b456-135">**Organizational account**</span></span></br>
  <span data-ttu-id="4b456-136">組織帳戶是建立在 Azure Active Directory 之下的帳戶。</span><span class="sxs-lookup"><span data-stu-id="4b456-136">An organizational account is an account that is created under Azure Active Directory.</span></span> <span data-ttu-id="4b456-137">組織帳戶地址的格式如下︰</span><span class="sxs-lookup"><span data-stu-id="4b456-137">The organizational account address has this format:</span></span>

    <span data-ttu-id="4b456-138">使用者@&lt;您的網域&gt;.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="4b456-138">user@&lt;your domain&gt;.onmicrosoft.com</span></span>

## <a name="change-service-administrator-for-a-subscription"></a><span data-ttu-id="4b456-139">變更訂用帳戶的服務管理員</span><span class="sxs-lookup"><span data-stu-id="4b456-139">Change Service Administrator for a subscription</span></span>
<span data-ttu-id="4b456-140">只有帳戶管理員可以變更訂用帳戶的服務管理員。</span><span class="sxs-lookup"><span data-stu-id="4b456-140">Only the Account Administrator can change the Service Administrator for a subscription.</span></span>

1. <span data-ttu-id="4b456-141">使用帳戶管理員登入 [Azure 帳戶中心](https://account.windowsazure.com/subscriptions)。</span><span class="sxs-lookup"><span data-stu-id="4b456-141">Sign in to [Azure Account Center](https://account.windowsazure.com/subscriptions) by using the Account Administrator.</span></span>
2. <span data-ttu-id="4b456-142">選取您想變更的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4b456-142">Select the subscription you want to change.</span></span>
3. <span data-ttu-id="4b456-143">選取右側的 [編輯訂用帳戶詳細資料]。</span><span class="sxs-lookup"><span data-stu-id="4b456-143">On the right side, select **Edit subscription** details.</span></span> </br>

    ![editsub](./media/billing-add-change-azure-subscription-administrator/editsub.png)
4. <span data-ttu-id="4b456-145">在 [服務管理員  ] 方塊中，輸入新的服務管理員的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="4b456-145">In the **SERVICE ADMINISTRATOR** box, enter the email address of the new Service Administrator.</span></span> </br>

    ![changeSA](./media/billing-add-change-azure-subscription-administrator/changeSA.png)

## <a name="change-the-account-administrator"></a><span data-ttu-id="4b456-147">如何變更帳戶管理員</span><span class="sxs-lookup"><span data-stu-id="4b456-147">Change the Account Administrator</span></span>
<span data-ttu-id="4b456-148">若要將 Azure 帳戶的擁有權轉移到另一個帳戶，請參閱 [轉移 Azure 訂用帳戶的擁有權](billing-subscription-transfer.md)。</span><span class="sxs-lookup"><span data-stu-id="4b456-148">To transfer ownership of the Azure account to another account, see [Transferring Ownership of an Azure subscription](billing-subscription-transfer.md).</span></span>

<span data-ttu-id="4b456-149">強烈建議您不要將帳戶管理員的電子郵件地址重新命名或刪除。</span><span class="sxs-lookup"><span data-stu-id="4b456-149">We strongly recommend that you don't delete or rename the Account Administrator's email address.</span></span> <span data-ttu-id="4b456-150">否則 Azure 帳戶可能會有未預期的行為或出現問題。</span><span class="sxs-lookup"><span data-stu-id="4b456-150">You may see unexpected and undesirable behavior with the Azure account.</span></span> <span data-ttu-id="4b456-151">您可能會無法使用該帳戶登入 Azure、變更帳戶，或使用該帳戶來管理資源。</span><span class="sxs-lookup"><span data-stu-id="4b456-151">You may not be able sign-in to Azure with that account, make changes to the account, or manage resources with that account.</span></span> 

## <a name="check-the-account-administrator-of-the-subscription"></a><span data-ttu-id="4b456-152">檢查訂用帳戶的帳戶管理員</span><span class="sxs-lookup"><span data-stu-id="4b456-152">Check the Account Administrator of the subscription</span></span>
<span data-ttu-id="4b456-153">如果您不確定誰是訂用帳戶的帳戶管理員，請使用下列步驟來找出帳戶管理員。</span><span class="sxs-lookup"><span data-stu-id="4b456-153">If you're not sure who the account administrator is for your subscription, use the following steps to find out.</span></span>

  1. <span data-ttu-id="4b456-154">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="4b456-154">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
  2. <span data-ttu-id="4b456-155">在 [中樞] 功能表中，選取 [訂用帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="4b456-155">On the Hub menu, select **Subscription**.</span></span>
  3. <span data-ttu-id="4b456-156">選取您想要檢查的訂用帳戶，然後查看 [設定]。</span><span class="sxs-lookup"><span data-stu-id="4b456-156">Select the subscription you want to check, and then look under **Settings**.</span></span>
  4. <span data-ttu-id="4b456-157">選取 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="4b456-157">Select **Properties**.</span></span> <span data-ttu-id="4b456-158">該訂用帳戶的帳戶管理員會顯示在 [帳戶管理員]  方塊中。</span><span class="sxs-lookup"><span data-stu-id="4b456-158">The account administrator of the subscription is displayed in the **Account Admin** box.</span></span>  

## <a name="types-of-azure-admin-accounts"></a><span data-ttu-id="4b456-159">Azure 管理帳戶的類型</span><span class="sxs-lookup"><span data-stu-id="4b456-159">Types of Azure admin accounts</span></span>
 <span data-ttu-id="4b456-160">帳戶管理員、服務管理員和共同管理員是 Microsoft Azure 中的三種系統管理員角色。</span><span class="sxs-lookup"><span data-stu-id="4b456-160">Account Administrator, Service Administrator, and Co-administrator are the three kinds of administrator roles in Microsoft Azure.</span></span> <span data-ttu-id="4b456-161">下表說明這三個系統管理角色之間的差異。</span><span class="sxs-lookup"><span data-stu-id="4b456-161">The following table describes the difference between these three administrative roles.</span></span>

| <span data-ttu-id="4b456-162">管理角色</span><span class="sxs-lookup"><span data-stu-id="4b456-162">Administrative role</span></span> | <span data-ttu-id="4b456-163">限制</span><span class="sxs-lookup"><span data-stu-id="4b456-163">Limit</span></span> | <span data-ttu-id="4b456-164">說明</span><span class="sxs-lookup"><span data-stu-id="4b456-164">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4b456-165">帳戶管理員 (AA)</span><span class="sxs-lookup"><span data-stu-id="4b456-165">Account Administrator (AA)</span></span> |<span data-ttu-id="4b456-166">每個 Azure 帳戶 1 名</span><span class="sxs-lookup"><span data-stu-id="4b456-166">1 per Azure account</span></span> |<span data-ttu-id="4b456-167">這就是註冊或購買 Azure 訂用帳戶，且經過授權可存取 [帳戶中心](https://account.windowsazure.com/Home/Index) 及執行各種管理工作的那個人。</span><span class="sxs-lookup"><span data-stu-id="4b456-167">This is the person who signed up for or bought Azure subscriptions, and is authorized to access the [Account Center](https://account.windowsazure.com/Home/Index) and perform various management tasks.</span></span> <span data-ttu-id="4b456-168">包括能夠建立訂用帳戶、取消訂用帳戶、變更訂用帳戶的計費方式以及變更服務管理員。</span><span class="sxs-lookup"><span data-stu-id="4b456-168">These include being able to create subscriptions, cancel subscriptions, change the billing for a subscription, and change the Service Administrator.</span></span> |
| <span data-ttu-id="4b456-169">服務管理員 (SA)</span><span class="sxs-lookup"><span data-stu-id="4b456-169">Service Administrator (SA)</span></span> |<span data-ttu-id="4b456-170">每個 Azure 訂用帳戶 1 名</span><span class="sxs-lookup"><span data-stu-id="4b456-170">1 per Azure subscription</span></span> |<span data-ttu-id="4b456-171">此角色經過授權，可管理 [Azure 入口網站](https://portal.azure.com)上的服務。</span><span class="sxs-lookup"><span data-stu-id="4b456-171">This role is authorized to manage services in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4b456-172">根據預設，新訂用帳戶的帳戶管理員也是服務管理員。</span><span class="sxs-lookup"><span data-stu-id="4b456-172">By default, for a new subscription, the Account Administrator is also the Service Administrator.</span></span> |
| <span data-ttu-id="4b456-173">[Azure 傳統入口網站](https://manage.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="4b456-173">Co-administrator (CA) in the [Azure classic portal](https://manage.windowsazure.com)</span></span> |<span data-ttu-id="4b456-174">每個訂用帳戶 200 名</span><span class="sxs-lookup"><span data-stu-id="4b456-174">200 per subscription</span></span> |<span data-ttu-id="4b456-175">此角色的存取權限與服務管理員相同，但無法變更訂用帳戶與 Azure 目錄的關聯。</span><span class="sxs-lookup"><span data-stu-id="4b456-175">This role has the same access privileges as the Service Administrator, but can’t change the association of subscriptions to Azure directories.</span></span> |

<span data-ttu-id="4b456-176">Azure Active Directory 角色型存取控制 (RBAC) 能讓使用者擁有多個角色。</span><span class="sxs-lookup"><span data-stu-id="4b456-176">Azure Active Directory Role-based Access Control (RBAC) allows users to be added to multiple roles.</span></span> <span data-ttu-id="4b456-177">如需詳細資訊，請參閱 [Azure Active Directory 角色型存取控制](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="4b456-177">For more information, see [Azure Active Directory Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

## <a name="limitations-and-restrictions-for-admin-accounts"></a><span data-ttu-id="4b456-178">系統管理員帳戶的限制和約束</span><span class="sxs-lookup"><span data-stu-id="4b456-178">Limitations and restrictions for admin accounts</span></span>
* <span data-ttu-id="4b456-179">每個訂用帳戶都與一個 Azure AD 目錄 (也就是預設目錄) 相關聯。</span><span class="sxs-lookup"><span data-stu-id="4b456-179">Each subscription is associated with an Azure AD directory (also known as the Default Directory).</span></span> <span data-ttu-id="4b456-180">若要尋找與訂用帳戶相關聯的預設目錄，請前往 [Azure 傳統入口網站](https://manage.windowsazure.com/)，然後選取 [設定] > [訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="4b456-180">To find the Default Directory the subscription is associated with, go to the [Azure classic portal](https://manage.windowsazure.com/), select **Settings** > **Subscriptions**.</span></span> <span data-ttu-id="4b456-181">請查看訂用帳戶識別碼來尋找預設目錄。</span><span class="sxs-lookup"><span data-stu-id="4b456-181">Check the subscription ID to find the Default Directory.</span></span>
* <span data-ttu-id="4b456-182">如果您以 Microsoft 帳戶登入，就只能將其他 Microsoft 帳戶或預設目錄中的使用者新增為共同管理員。</span><span class="sxs-lookup"><span data-stu-id="4b456-182">If you are signed in with a Microsoft Account, you can only add other Microsoft Accounts or users within the Default Directory as Co-Administrator.</span></span>
* <span data-ttu-id="4b456-183">如果您以組織帳戶登入，就可以將組織中的其他組織帳戶新增為共同管理員。</span><span class="sxs-lookup"><span data-stu-id="4b456-183">If you are signed in with an organizational account, you can add other organizational accounts in your organization as Co-Administrator.</span></span> <span data-ttu-id="4b456-184">舉例來說，abby@contoso.com 可以將 bob@contoso.com 新增為服務管理員或共同管理員，但無法新增 john@notcontoso.com，除非 john@notcontoso.com 在預設目錄中。</span><span class="sxs-lookup"><span data-stu-id="4b456-184">For example, abby@contoso.com can add bob@contoso.com as Service Administrator or Co-Administrator, but can't add john@notcontoso.com unless john@notcontoso.com is in Default Directory.</span></span> <span data-ttu-id="4b456-185">以組織帳戶登入的使用者，可以繼續將 Microsoft 帳戶使用者新增為服務管理員或共同管理員。</span><span class="sxs-lookup"><span data-stu-id="4b456-185">Users signed in with organizational accounts can continue to add Microsoft Account users as Service Administrator or Co-Administrator.</span></span>
* <span data-ttu-id="4b456-186">現在可以使用組織帳戶登入至 Azure，以下是服務管理員和共同管理員帳戶需求的變更：</span><span class="sxs-lookup"><span data-stu-id="4b456-186">Now that it is possible to sign in to Azure with an organizational account, here are the changes to Service Administrator and Co-administrator account requirements:</span></span>

  | <span data-ttu-id="4b456-187">登入方法</span><span class="sxs-lookup"><span data-stu-id="4b456-187">Sign in Method</span></span> | <span data-ttu-id="4b456-188">將 Microsoft 帳戶或預設目錄中的使用者新增為 CA 或 SA？</span><span class="sxs-lookup"><span data-stu-id="4b456-188">Add Microsoft Account or users within Default Directory as CA or SA?</span></span> | <span data-ttu-id="4b456-189">將相同組織中的組織帳戶新增為 CA 或 SA？</span><span class="sxs-lookup"><span data-stu-id="4b456-189">Add organizational account in the same organization as CA or SA?</span></span> | <span data-ttu-id="4b456-190">將不同組織中的組織帳戶新增為 CA 或 SA？</span><span class="sxs-lookup"><span data-stu-id="4b456-190">Add organizational account in different organization as CA or SA?</span></span> |
  | --- | --- | --- | --- |
  |  <span data-ttu-id="4b456-191">Microsoft 帳戶</span><span class="sxs-lookup"><span data-stu-id="4b456-191">Microsoft Account</span></span> |<span data-ttu-id="4b456-192">是</span><span class="sxs-lookup"><span data-stu-id="4b456-192">Yes</span></span> |<span data-ttu-id="4b456-193">否</span><span class="sxs-lookup"><span data-stu-id="4b456-193">No</span></span> |<span data-ttu-id="4b456-194">否</span><span class="sxs-lookup"><span data-stu-id="4b456-194">No</span></span> |
  |  <span data-ttu-id="4b456-195">組織帳戶</span><span class="sxs-lookup"><span data-stu-id="4b456-195">Organizational Account</span></span> |<span data-ttu-id="4b456-196">是</span><span class="sxs-lookup"><span data-stu-id="4b456-196">Yes</span></span> |<span data-ttu-id="4b456-197">是</span><span class="sxs-lookup"><span data-stu-id="4b456-197">Yes</span></span> |<span data-ttu-id="4b456-198">否</span><span class="sxs-lookup"><span data-stu-id="4b456-198">No</span></span> |

## <a name="learn-more-about-resource-access-control-and-active-directory"></a><span data-ttu-id="4b456-199">深入了解資源存取控制和 Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b456-199">Learn more about resource access control and Active Directory</span></span>
* <span data-ttu-id="4b456-200">若要深入了解如何在 Microsoft Azure 中控制資源存取，請參閱[了解 Azure 中的資源存取](../active-directory/active-directory-understanding-resource-access.md)。</span><span class="sxs-lookup"><span data-stu-id="4b456-200">To learn more about how resource access is controlled in Microsoft Azure, see [Understanding resource access in Azure](../active-directory/active-directory-understanding-resource-access.md).</span></span>
* <span data-ttu-id="4b456-201">如需有關 Azure Active Directory 的詳細資訊，請參閱 [Azure 訂用帳戶如何與 Azure Active Directory 產生關聯](../active-directory/active-directory-how-subscriptions-associated-directory.md)和[指派 Azure Active Directory 中的管理員角色](../active-directory/active-directory-assign-admin-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="4b456-201">For more information about Azure Active Directory, see [How Azure subscriptions are associated with Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md) and [Assigning administrator roles in Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="4b456-202">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="4b456-202">Need help?</span></span> <span data-ttu-id="4b456-203">請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="4b456-203">Contact support.</span></span>
<span data-ttu-id="4b456-204">如果仍需要協助，請[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)以快速解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="4b456-204">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
