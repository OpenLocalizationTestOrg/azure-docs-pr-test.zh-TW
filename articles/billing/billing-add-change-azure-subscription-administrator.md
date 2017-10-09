---
title: "aaaAdd 或變更管理 Azure 訂用帳戶角色 |Microsoft 文件"
description: "描述如何 tooadd 或變更 Azure 共同管理員、 服務管理員及帳戶管理員"
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
ms.openlocfilehash: 14eaecf2dbfd7152775ac3552bf3a7ae3db596b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-change-azure-administrator-roles-that-manage-hello-subscription-or-services"></a><span data-ttu-id="457f2-103">新增或變更管理 hello 訂用帳戶或服務的 Azure 系統管理員角色</span><span class="sxs-lookup"><span data-stu-id="457f2-103">Add or change Azure administrator roles that manage hello subscription or services</span></span>
<span data-ttu-id="457f2-104">您可以變更 hello Azure 系統管理員管理您的 Azure 訂用帳戶或管理 hello Azure 訂用帳戶中使用的服務。</span><span class="sxs-lookup"><span data-stu-id="457f2-104">You can change hello Azure administrator that manages your Azure subscription or manages hello Azure services used in your subscription.</span></span> <span data-ttu-id="457f2-105">tooview Azure 帳單資訊和管理訂用帳戶，您必須登入 toohello[帳戶中心](https://account.windowsazure.com/Home/Index)為 hello 帳戶系統管理員。</span><span class="sxs-lookup"><span data-stu-id="457f2-105">tooview Azure billing information and manage subscriptions, you must sign in toohello [Account Center](https://account.windowsazure.com/Home/Index) as hello Account Administrator.</span></span> 

## <a name="add-an-admin-for-a-subscription"></a><span data-ttu-id="457f2-106">新增訂用帳戶的管理員</span><span class="sxs-lookup"><span data-stu-id="457f2-106">Add an admin for a subscription</span></span>
<span data-ttu-id="457f2-107">在 hello Azure 入口網站或 hello Azure 傳統入口網站中，您可以加入 Azure 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="457f2-107">You can add an Azure administrator in hello Azure portal or in hello Azure classic portal.</span></span>

<span data-ttu-id="457f2-108">**Azure 入口網站**</span><span class="sxs-lookup"><span data-stu-id="457f2-108">**Azure portal**</span></span>

<span data-ttu-id="457f2-109">tooadd 某人身為系統管理員的訂用帳戶 hello Azure 入口網站中，您可以讓 hello 擁有者角色。</span><span class="sxs-lookup"><span data-stu-id="457f2-109">tooadd someone as an admin for a subscription in hello Azure portal, you give them hello owner role.</span></span> <span data-ttu-id="457f2-110">hello 擁有者角色只能管理您所指派的 hello 訂用帳戶中的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="457f2-110">hello owner role can only manage hello resources in hello subscription that you assigned.</span></span> <span data-ttu-id="457f2-111">沒有存取權限 tooother 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="457f2-111">It doesn't have access privilege tooother subscriptions.</span></span> <span data-ttu-id="457f2-112">hello hello 透過您加入的擁有者[Azure 入口網站](https://portal.azure.com)無法管理資源在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="457f2-112">hello owners you add through hello [Azure portal](https://portal.azure.com) can't manage resource in hello [Azure classic portal](https://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="457f2-113">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="457f2-113">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="457f2-114">在 hello 中樞功能表中，選取 **訂用帳戶** > *hello 訂用帳戶的 hello admin tooaccess*。</span><span class="sxs-lookup"><span data-stu-id="457f2-114">On hello Hub menu, select **Subscription** > *hello subscription that you want hello admin tooaccess*.</span></span>

    ![顯示已選取訂用帳戶選項的螢幕擷取畫面](./media/billing-add-change-azure-subscription-administrator/newselectsub.png)

3. <span data-ttu-id="457f2-116">在 hello 訂用帳戶 刀鋒視窗中，選取 **存取控制 (IAM)**。</span><span class="sxs-lookup"><span data-stu-id="457f2-116">In hello subscription blade, select **Access control (IAM)**.</span></span>
4. <span data-ttu-id="457f2-117">選取 [新增] > [角色] > [擁有者]。</span><span class="sxs-lookup"><span data-stu-id="457f2-117">Select **Add** > **Role** > **Owner**.</span></span> <span data-ttu-id="457f2-118">輸入您想 tooadd 做為擁有者，選取 hello 使用者，然後選取 hello 使用者 hello 電子郵件地址**儲存**。</span><span class="sxs-lookup"><span data-stu-id="457f2-118">Type hello email address of hello user you want tooadd as owner, select hello user, and then select **Save**.</span></span>

    ![顯示選取的 hello 擁有者角色的螢幕擷取畫面](./media/billing-add-change-azure-subscription-administrator/add-role.png)

5. <span data-ttu-id="457f2-120">如果您想 tooadd hello 擁有者帳戶為共同管理員，在 hello**存取控制 (IAM)**頁面上，以滑鼠右鍵按一下 hello 使用者，然後選取**加入為共同管理員**。</span><span class="sxs-lookup"><span data-stu-id="457f2-120">If you want tooadd hello owner account as co-administrator, in hello  **Access control (IAM)** page, right-click hello user and then select **Add as co-administrator**.</span></span> <span data-ttu-id="457f2-121">[Azure 預覽入口網站](https://preview.portal.azure.com/)現提供此功能。</span><span class="sxs-lookup"><span data-stu-id="457f2-121">This feature is now available on [Azure preview portal](https://preview.portal.azure.com/).</span></span> 

     ![新增共同管理員的螢幕擷取畫面](./media/billing-add-change-azure-subscription-administrator/add-coadmin.png)

    >[!TIP]
    ><span data-ttu-id="457f2-123">如果，則需要 tooadd hello 「 擁有者 」 使用者共同系統管理員身分 hello 使用者需要 toomanage hello 的 Azure 服務[Azure 傳統入口網站](https://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="457f2-123">You will need tooadd hello "Owner" user as co-administrator if hello user needs toomanage hello Azure services in [Azure classic portal](https://manage.windowsazure.com/).</span></span>

    <span data-ttu-id="457f2-124">tooremove hello 共同系統管理員權限，以滑鼠右鍵按一下 hello 「 共同系統管理員 」 使用者，然後選取**移除共同管理員**。</span><span class="sxs-lookup"><span data-stu-id="457f2-124">tooremove hello co-administrator permission, right-click hello "co-administrator" user and then select **Remove co-administrator**.</span></span>

    ![移除共同管理員的螢幕擷取畫面](./media/billing-add-change-azure-subscription-administrator/remove-coadmin.png)


<span data-ttu-id="457f2-126">**Azure 傳統入口網站**</span><span class="sxs-lookup"><span data-stu-id="457f2-126">**Azure classic portal**</span></span>

1. <span data-ttu-id="457f2-127">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="457f2-127">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="457f2-128">在 hello 瀏覽窗格中，選取**設定**> **管理員**> **新增**。</span><span class="sxs-lookup"><span data-stu-id="457f2-128">In hello navigation pane, select **Settings**> **Administrators**> **Add**.</span></span> </br>

    ![顯示 tooget toohello 將按鈕加入的螢幕擷取畫面](./media/billing-add-change-azure-subscription-administrator/addcoadmin.png)
3. <span data-ttu-id="457f2-130">類型 hello 電子郵件地址 hello 人員想 tooadd 共同系統管理員身分，，然後選取您想 hello 共同管理員 tooaccess hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="457f2-130">Type hello email address of hello person you want tooadd as Co-administrator and then select hello subscription that you want hello Co-administrator tooaccess.</span></span></br>

    ![<span data-ttu-id="457f2-131">顯示已選取訂用帳戶選項的螢幕擷取畫面</span><span class="sxs-lookup"><span data-stu-id="457f2-131">Screenshot that shows a subscription selected</span></span> ](./media/billing-add-change-azure-subscription-administrator/addcoadmin2.png)</br>

<span data-ttu-id="457f2-132">遵循電子郵件地址的 hello 可新增為共同管理員：</span><span class="sxs-lookup"><span data-stu-id="457f2-132">hello following email address can be added as a Co-Administrator:</span></span>

* <span data-ttu-id="457f2-133">**Microsoft 帳戶** (先前的 Windows Live ID)</span><span class="sxs-lookup"><span data-stu-id="457f2-133">**Microsoft Account** (formerly Windows Live ID)</span></span> </br>
  <span data-ttu-id="457f2-134">您可以使用 Microsoft 帳戶 toosign tooall 消費者導向 Microsoft 產品和雲端服務，例如 Outlook (Hotmail)、 Skype (MSN)、 OneDrive、 Windows Phone 和 Xbox LIVE。</span><span class="sxs-lookup"><span data-stu-id="457f2-134">You can use a Microsoft Account toosign in tooall consumer-oriented Microsoft products and cloud services, such as Outlook (Hotmail), Skype (MSN), OneDrive, Windows Phone, and Xbox LIVE.</span></span>
* <span data-ttu-id="457f2-135">**Organizational account**</span><span class="sxs-lookup"><span data-stu-id="457f2-135">**Organizational account**</span></span></br>
  <span data-ttu-id="457f2-136">組織帳戶是建立在 Azure Active Directory 之下的帳戶。</span><span class="sxs-lookup"><span data-stu-id="457f2-136">An organizational account is an account that is created under Azure Active Directory.</span></span> <span data-ttu-id="457f2-137">hello 組織帳戶地址格式如下：</span><span class="sxs-lookup"><span data-stu-id="457f2-137">hello organizational account address has this format:</span></span>

    <span data-ttu-id="457f2-138">使用者@&lt;您的網域&gt;.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="457f2-138">user@&lt;your domain&gt;.onmicrosoft.com</span></span>

## <a name="change-service-administrator-for-a-subscription"></a><span data-ttu-id="457f2-139">變更訂用帳戶的服務管理員</span><span class="sxs-lookup"><span data-stu-id="457f2-139">Change Service Administrator for a subscription</span></span>
<span data-ttu-id="457f2-140">Hello 帳戶系統管理員可以變更 hello 服務系統管理員的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="457f2-140">Only hello Account Administrator can change hello Service Administrator for a subscription.</span></span>

1. <span data-ttu-id="457f2-141">登入太[Azure 帳戶中心](https://account.windowsazure.com/subscriptions)使用 hello 帳戶系統管理員。</span><span class="sxs-lookup"><span data-stu-id="457f2-141">Sign in too[Azure Account Center](https://account.windowsazure.com/subscriptions) by using hello Account Administrator.</span></span>
2. <span data-ttu-id="457f2-142">選取您想要 toochange hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="457f2-142">Select hello subscription you want toochange.</span></span>
3. <span data-ttu-id="457f2-143">在 hello 右邊，選取**編輯訂用帳戶**詳細資料。</span><span class="sxs-lookup"><span data-stu-id="457f2-143">On hello right side, select **Edit subscription** details.</span></span> </br>

    ![editsub](./media/billing-add-change-azure-subscription-administrator/editsub.png)
4. <span data-ttu-id="457f2-145">在 hello**服務系統管理員**方塊中，輸入 hello hello 電子郵件地址新增服務系統管理員。</span><span class="sxs-lookup"><span data-stu-id="457f2-145">In hello **SERVICE ADMINISTRATOR** box, enter hello email address of hello new Service Administrator.</span></span> </br>

    ![changeSA](./media/billing-add-change-azure-subscription-administrator/changeSA.png)

## <a name="change-hello-account-administrator"></a><span data-ttu-id="457f2-147">變更 hello 帳戶管理員</span><span class="sxs-lookup"><span data-stu-id="457f2-147">Change hello Account Administrator</span></span>
<span data-ttu-id="457f2-148">tootransfer 擁有權的 hello Azure 帳戶 tooanother 帳戶，請參閱[傳輸的 Azure 訂用帳戶的擁有權](billing-subscription-transfer.md)。</span><span class="sxs-lookup"><span data-stu-id="457f2-148">tootransfer ownership of hello Azure account tooanother account, see [Transferring Ownership of an Azure subscription](billing-subscription-transfer.md).</span></span>

<span data-ttu-id="457f2-149">我們強烈建議您不要刪除或重新命名 hello 帳戶系統管理員的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="457f2-149">We strongly recommend that you don't delete or rename hello Account Administrator's email address.</span></span> <span data-ttu-id="457f2-150">您可能會看到非預期且不想要的行為，以 hello Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="457f2-150">You may see unexpected and undesirable behavior with hello Azure account.</span></span> <span data-ttu-id="457f2-151">您不能與該帳戶的無法登入 tooAzure、 toohello 帳戶進行變更或管理該帳戶的資源。</span><span class="sxs-lookup"><span data-stu-id="457f2-151">You may not be able sign-in tooAzure with that account, make changes toohello account, or manage resources with that account.</span></span> 

## <a name="check-hello-account-administrator-of-hello-subscription"></a><span data-ttu-id="457f2-152">核取 hello hello 訂用帳戶的帳戶管理員</span><span class="sxs-lookup"><span data-stu-id="457f2-152">Check hello Account Administrator of hello subscription</span></span>
<span data-ttu-id="457f2-153">如果您不確定 hello 帳戶系統管理員是訂用帳戶，使用下列步驟 toofind 出 hello。</span><span class="sxs-lookup"><span data-stu-id="457f2-153">If you're not sure who hello account administrator is for your subscription, use hello following steps toofind out.</span></span>

  1. <span data-ttu-id="457f2-154">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="457f2-154">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
  2. <span data-ttu-id="457f2-155">在 hello 中樞功能表中，選取 **訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="457f2-155">On hello Hub menu, select **Subscription**.</span></span>
  3. <span data-ttu-id="457f2-156">選取您想 toocheck，，然後再查看底下的 hello 訂用帳戶**設定**。</span><span class="sxs-lookup"><span data-stu-id="457f2-156">Select hello subscription you want toocheck, and then look under **Settings**.</span></span>
  4. <span data-ttu-id="457f2-157">選取 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="457f2-157">Select **Properties**.</span></span> <span data-ttu-id="457f2-158">hello hello 訂用帳戶的帳戶管理員會顯示在 hello**帳戶管理員**方塊。</span><span class="sxs-lookup"><span data-stu-id="457f2-158">hello account administrator of hello subscription is displayed in hello **Account Admin** box.</span></span>  

## <a name="types-of-azure-admin-accounts"></a><span data-ttu-id="457f2-159">Azure 管理帳戶的類型</span><span class="sxs-lookup"><span data-stu-id="457f2-159">Types of Azure admin accounts</span></span>
 <span data-ttu-id="457f2-160">帳戶系統管理員、 服務管理員和共同管理員是 hello 三種類型的 Microsoft Azure 中的系統管理員角色。</span><span class="sxs-lookup"><span data-stu-id="457f2-160">Account Administrator, Service Administrator, and Co-administrator are hello three kinds of administrator roles in Microsoft Azure.</span></span> <span data-ttu-id="457f2-161">hello 下表描述這三個系統管理角色的 hello 差異。</span><span class="sxs-lookup"><span data-stu-id="457f2-161">hello following table describes hello difference between these three administrative roles.</span></span>

| <span data-ttu-id="457f2-162">管理角色</span><span class="sxs-lookup"><span data-stu-id="457f2-162">Administrative role</span></span> | <span data-ttu-id="457f2-163">限制</span><span class="sxs-lookup"><span data-stu-id="457f2-163">Limit</span></span> | <span data-ttu-id="457f2-164">說明</span><span class="sxs-lookup"><span data-stu-id="457f2-164">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="457f2-165">帳戶管理員 (AA)</span><span class="sxs-lookup"><span data-stu-id="457f2-165">Account Administrator (AA)</span></span> |<span data-ttu-id="457f2-166">每個 Azure 帳戶 1 名</span><span class="sxs-lookup"><span data-stu-id="457f2-166">1 per Azure account</span></span> |<span data-ttu-id="457f2-167">這是 hello 人員註冊或購買 Azure 訂用帳戶，並為授權的 tooaccess hello[帳戶中心](https://account.windowsazure.com/Home/Index)並執行各項管理工作。</span><span class="sxs-lookup"><span data-stu-id="457f2-167">This is hello person who signed up for or bought Azure subscriptions, and is authorized tooaccess hello [Account Center](https://account.windowsazure.com/Home/Index) and perform various management tasks.</span></span> <span data-ttu-id="457f2-168">這些包括能夠 toocreate 訂閱、 取消訂用帳戶、 變更 hello 計費訂用帳戶，及變更 hello 服務系統管理員。</span><span class="sxs-lookup"><span data-stu-id="457f2-168">These include being able toocreate subscriptions, cancel subscriptions, change hello billing for a subscription, and change hello Service Administrator.</span></span> |
| <span data-ttu-id="457f2-169">服務管理員 (SA)</span><span class="sxs-lookup"><span data-stu-id="457f2-169">Service Administrator (SA)</span></span> |<span data-ttu-id="457f2-170">每個 Azure 訂用帳戶 1 名</span><span class="sxs-lookup"><span data-stu-id="457f2-170">1 per Azure subscription</span></span> |<span data-ttu-id="457f2-171">這個角色是在 hello 授權的 toomanage 服務[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="457f2-171">This role is authorized toomanage services in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="457f2-172">根據預設，新的訂閱 hello 帳戶系統管理員也是 hello 服務系統管理員。</span><span class="sxs-lookup"><span data-stu-id="457f2-172">By default, for a new subscription, hello Account Administrator is also hello Service Administrator.</span></span> |
| <span data-ttu-id="457f2-173">共同管理員 (CA)，在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="457f2-173">Co-administrator (CA) in hello [Azure classic portal](https://manage.windowsazure.com)</span></span> |<span data-ttu-id="457f2-174">每個訂用帳戶 200 名</span><span class="sxs-lookup"><span data-stu-id="457f2-174">200 per subscription</span></span> |<span data-ttu-id="457f2-175">這個角色有 hello 相同 hello 服務系統管理員，以存取權限，但無法變更 hello 關聯的訂用帳戶 tooAzure 目錄。</span><span class="sxs-lookup"><span data-stu-id="457f2-175">This role has hello same access privileges as hello Service Administrator, but can’t change hello association of subscriptions tooAzure directories.</span></span> |

<span data-ttu-id="457f2-176">Azure Active Directory 角色型存取控制 (RBAC) 可讓使用者 toobe 加入 toomultiple 角色。</span><span class="sxs-lookup"><span data-stu-id="457f2-176">Azure Active Directory Role-based Access Control (RBAC) allows users toobe added toomultiple roles.</span></span> <span data-ttu-id="457f2-177">如需詳細資訊，請參閱 [Azure Active Directory 角色型存取控制](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="457f2-177">For more information, see [Azure Active Directory Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

## <a name="limitations-and-restrictions-for-admin-accounts"></a><span data-ttu-id="457f2-178">系統管理員帳戶的限制和約束</span><span class="sxs-lookup"><span data-stu-id="457f2-178">Limitations and restrictions for admin accounts</span></span>
* <span data-ttu-id="457f2-179">每個訂用帳戶相關聯的 Azure AD 目錄 (也稱為 hello 預設目錄)。</span><span class="sxs-lookup"><span data-stu-id="457f2-179">Each subscription is associated with an Azure AD directory (also known as hello Default Directory).</span></span> <span data-ttu-id="457f2-180">toofind hello 預設目錄 hello 訂用帳戶都與移 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)，選取**設定** > **訂閱**。</span><span class="sxs-lookup"><span data-stu-id="457f2-180">toofind hello Default Directory hello subscription is associated with, go toohello [Azure classic portal](https://manage.windowsazure.com/), select **Settings** > **Subscriptions**.</span></span> <span data-ttu-id="457f2-181">請檢查 hello 訂用帳戶 ID toofind hello 預設目錄。</span><span class="sxs-lookup"><span data-stu-id="457f2-181">Check hello subscription ID toofind hello Default Directory.</span></span>
* <span data-ttu-id="457f2-182">如果您登入 Microsoft 帳戶，您只可以共同系統管理員身分來加入其他的 Microsoft 帳戶或 hello 預設目錄中的使用者。</span><span class="sxs-lookup"><span data-stu-id="457f2-182">If you are signed in with a Microsoft Account, you can only add other Microsoft Accounts or users within hello Default Directory as Co-Administrator.</span></span>
* <span data-ttu-id="457f2-183">如果您以組織帳戶登入，就可以將組織中的其他組織帳戶新增為共同管理員。</span><span class="sxs-lookup"><span data-stu-id="457f2-183">If you are signed in with an organizational account, you can add other organizational accounts in your organization as Co-Administrator.</span></span> <span data-ttu-id="457f2-184">舉例來說，abby@contoso.com 可以將 bob@contoso.com 新增為服務管理員或共同管理員，但無法新增 john@notcontoso.com，除非 john@notcontoso.com 在預設目錄中。</span><span class="sxs-lookup"><span data-stu-id="457f2-184">For example, abby@contoso.com can add bob@contoso.com as Service Administrator or Co-Administrator, but can't add john@notcontoso.com unless john@notcontoso.com is in Default Directory.</span></span> <span data-ttu-id="457f2-185">登入組織帳戶的使用者可以繼續 tooadd Microsoft 帳戶使用者做為服務管理員或共同管理員。</span><span class="sxs-lookup"><span data-stu-id="457f2-185">Users signed in with organizational accounts can continue tooadd Microsoft Account users as Service Administrator or Co-Administrator.</span></span>
* <span data-ttu-id="457f2-186">現在，很可能在有組織帳戶 tooAzure toosign，以下是 hello 變更 tooService 系統管理員和共同管理員帳戶需求：</span><span class="sxs-lookup"><span data-stu-id="457f2-186">Now that it is possible toosign in tooAzure with an organizational account, here are hello changes tooService Administrator and Co-administrator account requirements:</span></span>

  | <span data-ttu-id="457f2-187">登入方法</span><span class="sxs-lookup"><span data-stu-id="457f2-187">Sign in Method</span></span> | <span data-ttu-id="457f2-188">將 Microsoft 帳戶或預設目錄中的使用者新增為 CA 或 SA？</span><span class="sxs-lookup"><span data-stu-id="457f2-188">Add Microsoft Account or users within Default Directory as CA or SA?</span></span> | <span data-ttu-id="457f2-189">在 hello 中新增組織帳戶做為 CA 或 SA 相同組織嗎？</span><span class="sxs-lookup"><span data-stu-id="457f2-189">Add organizational account in hello same organization as CA or SA?</span></span> | <span data-ttu-id="457f2-190">將不同組織中的組織帳戶新增為 CA 或 SA？</span><span class="sxs-lookup"><span data-stu-id="457f2-190">Add organizational account in different organization as CA or SA?</span></span> |
  | --- | --- | --- | --- |
  |  <span data-ttu-id="457f2-191">Microsoft 帳戶</span><span class="sxs-lookup"><span data-stu-id="457f2-191">Microsoft Account</span></span> |<span data-ttu-id="457f2-192">是</span><span class="sxs-lookup"><span data-stu-id="457f2-192">Yes</span></span> |<span data-ttu-id="457f2-193">否</span><span class="sxs-lookup"><span data-stu-id="457f2-193">No</span></span> |<span data-ttu-id="457f2-194">否</span><span class="sxs-lookup"><span data-stu-id="457f2-194">No</span></span> |
  |  <span data-ttu-id="457f2-195">組織帳戶</span><span class="sxs-lookup"><span data-stu-id="457f2-195">Organizational Account</span></span> |<span data-ttu-id="457f2-196">是</span><span class="sxs-lookup"><span data-stu-id="457f2-196">Yes</span></span> |<span data-ttu-id="457f2-197">是</span><span class="sxs-lookup"><span data-stu-id="457f2-197">Yes</span></span> |<span data-ttu-id="457f2-198">否</span><span class="sxs-lookup"><span data-stu-id="457f2-198">No</span></span> |

## <a name="learn-more-about-resource-access-control-and-active-directory"></a><span data-ttu-id="457f2-199">深入了解資源存取控制和 Active Directory</span><span class="sxs-lookup"><span data-stu-id="457f2-199">Learn more about resource access control and Active Directory</span></span>
* <span data-ttu-id="457f2-200">toolearn 深入了解如何控制資源存取 Microsoft Azure 中，請參閱[了解 Azure 中的資源存取](../active-directory/active-directory-understanding-resource-access.md)。</span><span class="sxs-lookup"><span data-stu-id="457f2-200">toolearn more about how resource access is controlled in Microsoft Azure, see [Understanding resource access in Azure](../active-directory/active-directory-understanding-resource-access.md).</span></span>
* <span data-ttu-id="457f2-201">如需有關 Azure Active Directory 的詳細資訊，請參閱 [Azure 訂用帳戶如何與 Azure Active Directory 產生關聯](../active-directory/active-directory-how-subscriptions-associated-directory.md)和[指派 Azure Active Directory 中的管理員角色](../active-directory/active-directory-assign-admin-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="457f2-201">For more information about Azure Active Directory, see [How Azure subscriptions are associated with Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md) and [Assigning administrator roles in Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="457f2-202">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="457f2-202">Need help?</span></span> <span data-ttu-id="457f2-203">請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="457f2-203">Contact support.</span></span>
<span data-ttu-id="457f2-204">如果您仍需要協助，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="457f2-204">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
