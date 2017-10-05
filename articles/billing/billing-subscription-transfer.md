---
title: "將 Azure 訂用帳戶擁有權轉移給另一個帳戶 |Microsoft 文件"
description: "描述如何將 Azure 訂用帳戶轉移給另一位使用者，以及一些關於此程序的常見問題集 (FAQ)"
keywords: "轉移 azure 訂用帳戶,azure 轉移訂用帳戶,將 azure 訂用帳戶移到另一個帳戶,azure 變更訂用帳戶擁有者,將 azure 訂用帳戶轉移給另一個帳戶"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing,top-support-issue
ms.assetid: c8ecdc1e-c9c5-468c-a024-94ae41e64702
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8a856c39eb11546f35cb4e8c21e6bdcce98857a8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="transfer-ownership-of-an-azure-subscription-to-another-account"></a><span data-ttu-id="b7b40-104">將 Azure 訂用帳戶的擁有權轉移給另一個帳戶</span><span class="sxs-lookup"><span data-stu-id="b7b40-104">Transfer ownership of an Azure subscription to another account</span></span>

<span data-ttu-id="b7b40-105">您可以在帳戶中心內，將您的訂用帳戶轉送給隨用隨付、Visual Studio、行動套件或 BizSpark 訂用帳戶的使用者。</span><span class="sxs-lookup"><span data-stu-id="b7b40-105">You can transfer your subscription to another user for Pay-As-You-Go, Visual Studio, Action Pack, or BizSpark subscriptions in the Account Center.</span></span> <span data-ttu-id="b7b40-106">我們也支援轉送這些訂用帳戶類型的 Azure 外部服務。</span><span class="sxs-lookup"><span data-stu-id="b7b40-106">We support the transfer of Azure external services for these subscription types as well.</span></span> 

<span data-ttu-id="b7b40-107">在下列情況下，您可能想要轉移 Azure 訂用帳戶的擁有權：</span><span class="sxs-lookup"><span data-stu-id="b7b40-107">You might want to transfer ownership of an Azure subscription if you:</span></span>

* <span data-ttu-id="b7b40-108">需要將 Azure 訂用帳戶的帳單擁有權交給其他人。</span><span class="sxs-lookup"><span data-stu-id="b7b40-108">Need to hand over billing ownership of your Azure subscription to someone else.</span></span>
* <span data-ttu-id="b7b40-109">想要變更用來註冊 Azure 的帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7b40-109">Want to change the account used to sign up for Azure.</span></span> <span data-ttu-id="b7b40-110">或許您是使用 Microsoft 帳戶，但原本是想要使用您的公司或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7b40-110">Perhaps you used your Microsoft Account but meant to use your work or school account instead.</span></span>
* <span data-ttu-id="b7b40-111">想要將您的 Azure 訂用帳戶移到另一個目錄。</span><span class="sxs-lookup"><span data-stu-id="b7b40-111">Want to move your Azure subscription from one directory to another.</span></span>
* <span data-ttu-id="b7b40-112">Azure 和 Office 365 在不同的租用戶中，並想要合併。</span><span class="sxs-lookup"><span data-stu-id="b7b40-112">Have Azure and Office 365 in different tenants and want to consolidate.</span></span>

<span data-ttu-id="b7b40-113">若要將您的訂用帳戶變更至不同的優惠，請參閱[切換至不同的 Azure 訂用帳戶優惠](billing-how-to-switch-azure-offer.md)。</span><span class="sxs-lookup"><span data-stu-id="b7b40-113">To change your subscription to a different offer, see [Switch your Azure subscription to another offer](billing-how-to-switch-azure-offer.md).</span></span> 

## <a name="transfer-ownership-of-an-azure-subscription"></a><span data-ttu-id="b7b40-114">轉移 Azure 訂用帳戶的擁有權</span><span class="sxs-lookup"><span data-stu-id="b7b40-114">Transfer ownership of an Azure subscription</span></span>
> [!VIDEO https://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/Transfer-an-Azure-subscription/player]
>
>

1. <span data-ttu-id="b7b40-115">登入 <https://account.windowsazure.com/Subscriptions>。</span><span class="sxs-lookup"><span data-stu-id="b7b40-115">Sign in at <https://account.windowsazure.com/Subscriptions>.</span></span> <span data-ttu-id="b7b40-116">您必須是帳戶管理員，才能執行擁有權轉送。</span><span class="sxs-lookup"><span data-stu-id="b7b40-116">You have to be the Account Administrator to perform an ownership transfer.</span></span> <span data-ttu-id="b7b40-117">若要找出誰是訂用帳戶的帳戶管理員，請參閱[常見問題集](#faq)。</span><span class="sxs-lookup"><span data-stu-id="b7b40-117">To find out who is the Account Administrator of the subscription, see the [Frequently asked questions](#faq).</span></span>

2. <span data-ttu-id="b7b40-118">選取要移轉的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7b40-118">Select the subscription to transfer.</span></span>

3. <span data-ttu-id="b7b40-119">按一下 [轉移訂用帳戶]  選項。</span><span class="sxs-lookup"><span data-stu-id="b7b40-119">Click the **Transfer Subscription** option.</span></span> <span data-ttu-id="b7b40-120">如果您未看到此按鈕，請參閱[常見問題集](#no-button)。</span><span class="sxs-lookup"><span data-stu-id="b7b40-120">See [FAQ](#no-button) if you do not see the button.</span></span>

   ![Azure 帳戶的訂用帳戶索引標籤](./media/billing-subscription-transfer/image1.png)
4. <span data-ttu-id="b7b40-122">指定接受者。</span><span class="sxs-lookup"><span data-stu-id="b7b40-122">Specify the recipient.</span></span>

   ![移轉訂用帳戶對話方塊](./media/billing-subscription-transfer/image2.PNG)
5. <span data-ttu-id="b7b40-124">接受者會自動收到含有接受連結的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="b7b40-124">The recipient automatically gets an email with an acceptance link.</span></span>

   ![給接受者的訂用帳戶移轉電子郵件](./media/billing-subscription-transfer/image3.png)
6. <span data-ttu-id="b7b40-126">接受者按一下連結並遵循指示進行，包括輸入他們的付款資訊。</span><span class="sxs-lookup"><span data-stu-id="b7b40-126">The recipient clicks the link and follows the instructions, including entering their payment information.</span></span>

   ![第一個訂用帳戶移轉網頁](./media/billing-subscription-transfer/image4.png)

   ![第二個訂用帳戶移轉網頁](./media/billing-subscription-transfer/image5.png)
7. <span data-ttu-id="b7b40-129">成功！</span><span class="sxs-lookup"><span data-stu-id="b7b40-129">Success!</span></span> <span data-ttu-id="b7b40-130">現在已移轉訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7b40-130">The subscription is now transferred.</span></span>

## <a name="transfer-subscription-ownership-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="b7b40-131">轉送 Enterprise 合約 (EA) 客戶的訂用帳戶擁有權</span><span class="sxs-lookup"><span data-stu-id="b7b40-131">Transfer subscription ownership for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="b7b40-132">企業系統管理員可以轉送註冊內之訂用帳戶的擁有權。</span><span class="sxs-lookup"><span data-stu-id="b7b40-132">The Enterprise Administrator can transfer ownership of subscriptions within an enrollment.</span></span> <span data-ttu-id="b7b40-133">若要開始使用，請參閱 EA 入口網站中的[轉送帳戶擁有權](https://ea.azure.com/helpdocs/changeAccountOwnerForASubscription)。</span><span class="sxs-lookup"><span data-stu-id="b7b40-133">To get started, see [Transfer Account Ownership](https://ea.azure.com/helpdocs/changeAccountOwnerForASubscription) in the EA portal.</span></span>

## <a name="next-steps-after-accepting-ownership-of-a-subscription"></a><span data-ttu-id="b7b40-134">接受訂用帳戶擁有權後的後續步驟</span><span class="sxs-lookup"><span data-stu-id="b7b40-134">Next steps after accepting ownership of a subscription</span></span>
1. <span data-ttu-id="b7b40-135">您現在是帳戶管理員。</span><span class="sxs-lookup"><span data-stu-id="b7b40-135">You are now the Account Administrator.</span></span> <span data-ttu-id="b7b40-136">請檢視並更新服務管理員和共同管理員。</span><span class="sxs-lookup"><span data-stu-id="b7b40-136">Review and update the Service Administrator and Co-Administrators.</span></span> <span data-ttu-id="b7b40-137">移至 [設定]，管理 [Azure 傳統入口網站](https://manage.windowsazure.com) 中的管理員。</span><span class="sxs-lookup"><span data-stu-id="b7b40-137">Manage admins in the [Azure classic portal](https://manage.windowsazure.com) by going to Settings.</span></span> <span data-ttu-id="b7b40-138">[深入了解管理員角色](billing-add-change-azure-subscription-administrator.md)。</span><span class="sxs-lookup"><span data-stu-id="b7b40-138">[Learn more about administrator roles](billing-add-change-azure-subscription-administrator.md).</span></span>

2. <span data-ttu-id="b7b40-139">您也可以針對訂用帳戶和服務使用角色型存取控制 (RBAC)。</span><span class="sxs-lookup"><span data-stu-id="b7b40-139">You can also use role-based access control (RBAC) for your subscription and services.</span></span> <span data-ttu-id="b7b40-140">瀏覽 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b7b40-140">Visit the [Azure portal](https://portal.azure.com).</span></span> [<span data-ttu-id="b7b40-141">深入了解 RBAC</span><span class="sxs-lookup"><span data-stu-id="b7b40-141">Learn more about RBAC</span></span>](../active-directory/role-based-access-control-configure.md)

3. <span data-ttu-id="b7b40-142">更新與此訂用帳戶服務相關聯的認證，包括：</span><span class="sxs-lookup"><span data-stu-id="b7b40-142">Update credentials associated with this subscription's services including:</span></span>
   
   * <span data-ttu-id="b7b40-143">可將使用者管理權限授與給訂用帳戶資源的管理憑證。</span><span class="sxs-lookup"><span data-stu-id="b7b40-143">Management certificates that grant the user admin rights to subscription resources.</span></span> <span data-ttu-id="b7b40-144">如需詳細資訊，請參閱 [Create and upload a management certificate for Azure](../cloud-services/cloud-services-certs-create.md)</span><span class="sxs-lookup"><span data-stu-id="b7b40-144">For more information, see [Create and upload a management certificate for Azure](../cloud-services/cloud-services-certs-create.md)</span></span>
   
   * <span data-ttu-id="b7b40-145">服務 (例如儲存體) 的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="b7b40-145">Access keys for services like Storage.</span></span> <span data-ttu-id="b7b40-146">如需詳細資訊，請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)</span><span class="sxs-lookup"><span data-stu-id="b7b40-146">For more information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md)</span></span>
   
   * <span data-ttu-id="b7b40-147">服務 (例如 Azure 虛擬機器) 的遠端存取認證。</span><span class="sxs-lookup"><span data-stu-id="b7b40-147">Remote Access credentials for services like Azure Virtual Machines.</span></span> 

4. <span data-ttu-id="b7b40-148">若要[更新此訂用帳戶的計費警示](https://account.windowsazure.com/Subscriptions)，請至 [Azure 帳戶中心](billing-set-up-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="b7b40-148">[Update billing alerts for this subscription](billing-set-up-alerts.md) at the [Azure Account Center](https://account.windowsazure.com/Subscriptions).</span></span> 

5. <span data-ttu-id="b7b40-149">如果您正與合作夥伴協力作業，請考慮更新此訂用帳戶的合作夥伴 ID。</span><span class="sxs-lookup"><span data-stu-id="b7b40-149">If you're working with a partner, consider updating the partner ID on this subscription.</span></span> <span data-ttu-id="b7b40-150">您可以在 [Azure 帳戶中心](https://account.windowsazure.com/Subscriptions)更新合作夥伴識別碼。</span><span class="sxs-lookup"><span data-stu-id="b7b40-150">You can update the partner ID in the [Azure Account Center](https://account.windowsazure.com/Subscriptions).</span></span>

<a id="faq"></a>

## <a name="frequently-asked-questions-faq"></a><span data-ttu-id="b7b40-151">常見問題集 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="b7b40-151">Frequently asked questions (FAQ)</span></span>
* <span data-ttu-id="b7b40-152"><a name="whoisaa"></a>**訂用帳戶的帳戶管理員是誰？**</span><span class="sxs-lookup"><span data-stu-id="b7b40-152"><a name="whoisaa"></a> **Who is the account administrator of the subscription?**</span></span>

  <span data-ttu-id="b7b40-153">帳戶管理員就是註冊或購買 Azure 訂用帳戶的人員。</span><span class="sxs-lookup"><span data-stu-id="b7b40-153">The account administrator is the person who signed up for or bought the Azure subscription.</span></span> <span data-ttu-id="b7b40-154">他們已獲得授權存取[帳戶中心](https://account.windowsazure.com/Home/Index)並可執行各種管理工作，像是建立訂用帳戶、取消訂用帳戶、變更訂用帳戶的計費方式，或變更服務管理員。</span><span class="sxs-lookup"><span data-stu-id="b7b40-154">They're authorized to access the [Account Center](https://account.windowsazure.com/Home/Index) and perform various management tasks like create subscriptions, cancel subscriptions, change the billing for a subscription, or change the Service Administrator.</span></span> <span data-ttu-id="b7b40-155">如果您不確定誰是訂用帳戶的帳戶管理員，請使用下列步驟來找出帳戶管理員。</span><span class="sxs-lookup"><span data-stu-id="b7b40-155">If you're not sure who the account administrator is for a subscription, use the following steps to find out.</span></span>

  1. <span data-ttu-id="b7b40-156">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b7b40-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
  2. <span data-ttu-id="b7b40-157">在 [中樞] 功能表中，選取 [訂用帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="b7b40-157">On the Hub menu, select **Subscription**.</span></span>
  3. <span data-ttu-id="b7b40-158">選取您想要檢查的訂用帳戶，然後查看 [設定]。</span><span class="sxs-lookup"><span data-stu-id="b7b40-158">Select the subscription you want to check, and then look under **Settings**.</span></span>
  4. <span data-ttu-id="b7b40-159">選取 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="b7b40-159">Select **Properties**.</span></span> <span data-ttu-id="b7b40-160">該訂用帳戶的帳戶管理員會顯示在 [帳戶管理員]  方塊中。</span><span class="sxs-lookup"><span data-stu-id="b7b40-160">The account administrator of the subscription is displayed in the **Account Admin** box.</span></span>  

* <span data-ttu-id="b7b40-161">**所有項目都會轉送嗎？包括資源群組、VM、磁碟和其他執行中的服務？**</span><span class="sxs-lookup"><span data-stu-id="b7b40-161">**Does everything transfer? Including resource groups, VMs, disks, and other running services?**</span></span>

  <span data-ttu-id="b7b40-162">是，VM、磁碟和網站等所有資源都會轉移給新的擁有者。</span><span class="sxs-lookup"><span data-stu-id="b7b40-162">Yes, all your resources like VMs, disks, and websites transfer to the new owner.</span></span> <span data-ttu-id="b7b40-163">不過，不會跨不同目錄轉送您所設定的任何[系統管理員角色](billing-add-change-azure-subscription-administrator.md)和[角色型存取控制 (RBAC)](../active-directory/role-based-access-control-configure.md) 原則。</span><span class="sxs-lookup"><span data-stu-id="b7b40-163">However, any [administrator roles](billing-add-change-azure-subscription-administrator.md) and [Role-based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) policies you've set up do not transfer across different directories.</span></span>

* <span data-ttu-id="b7b40-164"><a id="no-button"></a>為何沒看到 [轉送訂用帳戶] 按鈕？</span><span class="sxs-lookup"><span data-stu-id="b7b40-164"><a id="no-button"></a> **Why don't I see the Transfer Subscription button?**</span></span>

  <span data-ttu-id="b7b40-165">如果您沒看到 [轉送訂用帳戶] 按鈕，則表示您的優惠不支援訂用帳戶轉送。</span><span class="sxs-lookup"><span data-stu-id="b7b40-165">If you don't see the **Transfer Subscription** button, then we don't support subscription transfer for your offer.</span></span> <span data-ttu-id="b7b40-166">[連絡客戶支援](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。</span><span class="sxs-lookup"><span data-stu-id="b7b40-166">[Contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

* <span data-ttu-id="b7b40-167">**訂用帳戶移轉會造成服務中斷嗎？**</span><span class="sxs-lookup"><span data-stu-id="b7b40-167">**Does a subscription transfer result in any service downtime?**</span></span>

  <span data-ttu-id="b7b40-168">不會影響服務。</span><span class="sxs-lookup"><span data-stu-id="b7b40-168">There is no impact to the service.</span></span> <span data-ttu-id="b7b40-169">轉送訂用帳戶會在目前帳戶管理員之下取消訂用帳戶，並在接受者的帳戶之下建立訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7b40-169">Transferring the subscription cancels the subscription under the current Account Administrator and creates a subscription under the recipient's account.</span></span> <span data-ttu-id="b7b40-170">新的訂用帳戶與基礎 Azure 服務相關聯。</span><span class="sxs-lookup"><span data-stu-id="b7b40-170">The new subscription is associated to the underlying Azure services.</span></span> <span data-ttu-id="b7b40-171">訂用帳戶 ID 維持不變。</span><span class="sxs-lookup"><span data-stu-id="b7b40-171">The subscription ID remains the same.</span></span>

* <span data-ttu-id="b7b40-172">**如何使用此程序來變更訂用帳戶的目錄？**</span><span class="sxs-lookup"><span data-stu-id="b7b40-172">**How do I use this process to change the directory for subscription?**</span></span>

  <span data-ttu-id="b7b40-173">Azure 訂用帳戶建立在帳戶管理員所屬的目錄中。</span><span class="sxs-lookup"><span data-stu-id="b7b40-173">An Azure subscription is created in the directory that the Account Administrator belongs to.</span></span> <span data-ttu-id="b7b40-174">若要變更目錄，請將訂用帳戶轉移到目標目錄中的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7b40-174">To change the directory, transfer the subscription to a user account in the target directory.</span></span> <span data-ttu-id="b7b40-175">當使用者完成步驟接受轉移時，訂用帳戶就會自動移至目標目錄。</span><span class="sxs-lookup"><span data-stu-id="b7b40-175">When that user completes the steps to accept transfer, the subscription is automatically moved to the target directory.</span></span>

* <span data-ttu-id="b7b40-176">**如果我接管另一個組織的訂用帳戶帳單擁有權，他們可以繼續存取我的資源嗎？**</span><span class="sxs-lookup"><span data-stu-id="b7b40-176">**If I take over billing ownership of a subscription from another organization, do they continue to have access to my resources?**</span></span>

  <span data-ttu-id="b7b40-177">如果訂用帳戶轉移到另一個租用戶，與先前的租用戶相關聯的使用者會失去訂用帳戶的存取權。</span><span class="sxs-lookup"><span data-stu-id="b7b40-177">If the subscription is transferred to another tenant, the users associated with the previous tenant lose access to the subscription.</span></span> <span data-ttu-id="b7b40-178">即使使用者不再是服務管理員或共同管理員，他們仍可能透過其他安全性機制來存取訂用帳戶，包括：</span><span class="sxs-lookup"><span data-stu-id="b7b40-178">Even if a user is not a Service Admin or Co-admin anymore, they might still have access to the subscription through other security mechanisms, including:</span></span>

  * <span data-ttu-id="b7b40-179">可將使用者管理權限授與給訂用帳戶資源的管理憑證。</span><span class="sxs-lookup"><span data-stu-id="b7b40-179">Management certificates that grant the user admin rights to subscription resources.</span></span> <span data-ttu-id="b7b40-180">如需詳細資訊，請參閱[建立和上傳 Azure 的管理憑證](../cloud-services/cloud-services-certs-create.md)。</span><span class="sxs-lookup"><span data-stu-id="b7b40-180">For more information, see [Create and Upload a Management Certificate for Azure](../cloud-services/cloud-services-certs-create.md).</span></span>
  * <span data-ttu-id="b7b40-181">服務 (例如儲存體) 的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="b7b40-181">Access keys for services like Storage.</span></span> <span data-ttu-id="b7b40-182">如需詳細資訊，請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="b7b40-182">For more information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
  * <span data-ttu-id="b7b40-183">服務 (例如 Azure 虛擬機器) 的遠端存取認證。</span><span class="sxs-lookup"><span data-stu-id="b7b40-183">Remote Access credentials for services like Azure Virtual Machines.</span></span>

 <span data-ttu-id="b7b40-184">如果接受者需要限制對其資源的存取權，則應考慮更新所有與服務相關聯的密碼。</span><span class="sxs-lookup"><span data-stu-id="b7b40-184">If the recipient needs to restrict access to their resources, they should consider updating any secrets associated with the service.</span></span> <span data-ttu-id="b7b40-185">您可以使用下列步驟來更新大部分的資源：</span><span class="sxs-lookup"><span data-stu-id="b7b40-185">Most resources can be updated by using the following steps:</span></span>

    1. <span data-ttu-id="b7b40-186">移至 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b7b40-186">Go to the [Azure portal](https://portal.azure.com).</span></span>
    2. <span data-ttu-id="b7b40-187">在 [中樞] 功能表中，選取 [所有資源]。</span><span class="sxs-lookup"><span data-stu-id="b7b40-187">On the Hub menu, select **All resources**.</span></span>
    3. <span data-ttu-id="b7b40-188">選取資源。</span><span class="sxs-lookup"><span data-stu-id="b7b40-188">Select the resource.</span></span> 
    4. <span data-ttu-id="b7b40-189">在資源刀鋒視窗中，按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="b7b40-189">In the resource blade, click **Settings**.</span></span> <span data-ttu-id="b7b40-190">您可以在這裡檢視並更新現有的密碼。</span><span class="sxs-lookup"><span data-stu-id="b7b40-190">Here you can view and update existing secrets.</span></span>

* <span data-ttu-id="b7b40-191">**如果我在計費週期中途移轉訂用帳戶，接受者需要支付整個計費週期嗎？**</span><span class="sxs-lookup"><span data-stu-id="b7b40-191">**If I transfer the subscription in the middle of the billing cycle, does the recipient pay for the entire billing cycle?**</span></span>

  <span data-ttu-id="b7b40-192">傳送者負責支付移轉完成當時所報告的任何使用量。</span><span class="sxs-lookup"><span data-stu-id="b7b40-192">The sender is responsible for payment for any usage that was reported up to the point that the transfer is completed.</span></span> <span data-ttu-id="b7b40-193">接受者負責支付移傳以後所報告的使用量。</span><span class="sxs-lookup"><span data-stu-id="b7b40-193">The recipient is responsible for usage reported from the time of transfer onwards.</span></span> <span data-ttu-id="b7b40-194">可能有某些使用量是在移轉之前發生，但在之後才報告。</span><span class="sxs-lookup"><span data-stu-id="b7b40-194">There may be some usage that took place before transfer but was reported afterwards.</span></span> <span data-ttu-id="b7b40-195">使用量會包含在接受者的帳單中。</span><span class="sxs-lookup"><span data-stu-id="b7b40-195">The usage is included in the recipient's bill.</span></span>

* <span data-ttu-id="b7b40-196">**接受者可存取使用量及帳單記錄嗎？**</span><span class="sxs-lookup"><span data-stu-id="b7b40-196">**Does the recipient have access to usage and billing history?**</span></span>

  <span data-ttu-id="b7b40-197">接受者可用的資訊只有最新帳單的金額，而如果訂用帳戶是在產生第一份帳單之前移轉，則可使用目前餘額。</span><span class="sxs-lookup"><span data-stu-id="b7b40-197">The only information available to the recipient is the amount of the last bill or if the subscription was transferred before the first bill was generated, the current balance.</span></span> <span data-ttu-id="b7b40-198">其餘的使用量及帳單記錄不會隨著訂用帳戶一起移轉。</span><span class="sxs-lookup"><span data-stu-id="b7b40-198">The rest of the usage and billing history does not transfer with the subscription.</span></span>

* <span data-ttu-id="b7b40-199">**移轉期間可以變更優惠嗎？**</span><span class="sxs-lookup"><span data-stu-id="b7b40-199">**Can the offer be changed during a transfer?**</span></span>

  <span data-ttu-id="b7b40-200">優惠必須維持不變。</span><span class="sxs-lookup"><span data-stu-id="b7b40-200">The offer must remain the same.</span></span> <span data-ttu-id="b7b40-201">若要變更優惠，請參閱[切換至不同的 Azure 訂用帳戶優惠](billing-how-to-switch-azure-offer.md)。</span><span class="sxs-lookup"><span data-stu-id="b7b40-201">To change your offer, see [Switch your Azure subscription to another offer](billing-how-to-switch-azure-offer.md).</span></span>

* <span data-ttu-id="b7b40-202">**我可以將訂用帳戶轉移給另一個國家/地區的使用者帳戶嗎？**</span><span class="sxs-lookup"><span data-stu-id="b7b40-202">**Can I transfer a subscription to a user account in another country?**</span></span>

  <span data-ttu-id="b7b40-203">否，不支援將訂用帳戶轉移給另一個國家/地區的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7b40-203">No, transferring a subscription to a user account in another country is not supported.</span></span> <span data-ttu-id="b7b40-204">接受者的使用者帳戶必須在相同的國家/地區。</span><span class="sxs-lookup"><span data-stu-id="b7b40-204">The recipient's user account must be in the same country.</span></span>

* <span data-ttu-id="b7b40-205">**接受者可以使用不同的付款方法嗎？**</span><span class="sxs-lookup"><span data-stu-id="b7b40-205">**Can the recipient use a different payment method?**</span></span>

  <span data-ttu-id="b7b40-206">是。</span><span class="sxs-lookup"><span data-stu-id="b7b40-206">Yes.</span></span> <span data-ttu-id="b7b40-207">但訂用帳戶帳單記錄會拆成兩個帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7b40-207">But the subscription billing history is split across two accounts.</span></span>  

* <span data-ttu-id="b7b40-208">**Azure 訂用帳戶轉移後，付款方法會受到影響嗎？**</span><span class="sxs-lookup"><span data-stu-id="b7b40-208">**Is the payment method impacted after I transferred an Azure subscription?**</span></span>

  <span data-ttu-id="b7b40-209">若要接受訂用帳戶轉移，必須提供信用卡或類似的訂用帳戶付款方法。</span><span class="sxs-lookup"><span data-stu-id="b7b40-209">To accept a subscription transfer, a credit card, or similar payment method must be provided to pay for the subscription.</span></span> <span data-ttu-id="b7b40-210">例如，如果 Bob 將訂用帳戶轉移給 Jane，而 Jane 接受轉移，則 Jane 必須提供用來支付訂用帳戶的付款方法。</span><span class="sxs-lookup"><span data-stu-id="b7b40-210">For example, if Bob transfers a subscription to Jane and Jane accepts the transfer, Jane must provide a payment method to pay for the subscription.</span></span> <span data-ttu-id="b7b40-211">完成轉移之後，就會向 Jane 收取訂用帳戶的費用，而不是向 Bob 收取。</span><span class="sxs-lookup"><span data-stu-id="b7b40-211">After the transfer is complete, Jane is billed for the subscription not Bob.</span></span>

* <span data-ttu-id="b7b40-212">**如何將我的 Azure 訂用帳戶資料與服務移轉至新的訂用帳戶？**</span><span class="sxs-lookup"><span data-stu-id="b7b40-212">**How do I migrate data and services for my Azure subscription to new subscription?**</span></span>

  <span data-ttu-id="b7b40-213">如果您無法轉移訂用帳戶的擁有權，則可手動移轉您的資源。</span><span class="sxs-lookup"><span data-stu-id="b7b40-213">If you can't transfer subscription ownership, you can manually migrate your resources.</span></span> <span data-ttu-id="b7b40-214">請參閱[將資源移動到新的資源群組或訂用帳戶](../azure-resource-manager/resource-group-move-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="b7b40-214">See [Move resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>



## <a name="need-help-contact-support"></a><span data-ttu-id="b7b40-215">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="b7b40-215">Need help?</span></span> <span data-ttu-id="b7b40-216">請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="b7b40-216">Contact support.</span></span>
<span data-ttu-id="b7b40-217">如果仍需要協助，請[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)以快速解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="b7b40-217">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span> 


