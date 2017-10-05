---
title: "在 Azure 中管理 Office 365 訂用帳戶的目錄 | Microsoft Docs"
description: "使用 Azure Active Directory 和 Azure 傳統入口網站管理 Office 365 訂用帳戶目錄"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 746987b7-2dfd-4b35-819d-37c1b65c5c81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: b520a5e96417fb766a757fabc384a1fc4eb0f14e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="manage-the-directory-for-your-office-365-subscription-in-azure"></a><span data-ttu-id="98f29-103">在 Azure 中管理 Office 365 訂用帳戶的目錄</span><span class="sxs-lookup"><span data-stu-id="98f29-103">Manage the directory for your Office 365 subscription in Azure</span></span>
<span data-ttu-id="98f29-104">本文說明如何使用 Azure 傳統入口網站，管理針對 Office 365 訂用帳戶建立的目錄。</span><span class="sxs-lookup"><span data-stu-id="98f29-104">This article describes how to manage a directory that was created for an Office 365 subscription, using the Azure classic portal.</span></span> <span data-ttu-id="98f29-105">您必須是服務管理員或 Azure 訂用帳戶的共同管理員，才能登入 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="98f29-105">You must be either the Service Administrator or a co-administrator of an Azure subscription to sign in to the Azure classic portal.</span></span> <span data-ttu-id="98f29-106">如果您尚未擁有 Azure 訂用帳戶，您可以立即註冊 [免費 30 天試用版](https://azure.microsoft.com/trial/get-started-active-directory/) ，並使用此連結在 5 分鐘內部署第一個雲端解決方案。</span><span class="sxs-lookup"><span data-stu-id="98f29-106">If you don’t yet have an Azure subscription, you can sign up for a [free 30-day trial](https://azure.microsoft.com/trial/get-started-active-directory/) today and deploy your first cloud solution in under 5 minutes, using this link.</span></span> <span data-ttu-id="98f29-107">請確認使用您用來登入 Office 365 的工作或學校帳戶來註冊。</span><span class="sxs-lookup"><span data-stu-id="98f29-107">Be sure to use the work or school account that you use to sign in to Office 365.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98f29-108">Microsoft 建議您使用 Azure 入口網站中的 [Azure AD 系統管理中心](https://aad.portal.azure.com)來管理 Azure AD，而不要使用本文所提及的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="98f29-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="98f29-109">完成 Azure 訂用帳戶之後，您便可以登入 Azure 傳統入口網站並存取 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="98f29-109">After you complete the Azure subscription, you can sign in to the Azure classic portal and access Azure services.</span></span> <span data-ttu-id="98f29-110">按一下 Active Directory 擴充模組，以便管理用來驗證您 Office 365 使用者的相同目錄。</span><span class="sxs-lookup"><span data-stu-id="98f29-110">Click the Active Directory extension to manage the same directory that authenticates your Office 365 users.</span></span>

<span data-ttu-id="98f29-111">如果您已經擁有 Azure 訂用帳戶，則管理其他目錄的程序也很簡單。</span><span class="sxs-lookup"><span data-stu-id="98f29-111">If you do already have an Azure subscription, the process to manage an additional directory is also straightforward.</span></span> <span data-ttu-id="98f29-112">在此範例中，Michael Smith 可能擁有適用於 Contoso.com 的 Office 365 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="98f29-112">For example, Michael Smith might have an Office 365 subscription for Contoso.com.</span></span> <span data-ttu-id="98f29-113">他也擁有使用其 Microsoft 帳戶 msmith@hotmail.com 所註冊的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="98f29-113">He also has an Azure subscription that he signed up for by using his Microsoft account, msmith@hotmail.com.</span></span> <span data-ttu-id="98f29-114">在此情況下，他要管理兩個目錄。</span><span class="sxs-lookup"><span data-stu-id="98f29-114">In this case, he manages two directories.</span></span>

| <span data-ttu-id="98f29-115">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="98f29-115">Subscription</span></span> | <span data-ttu-id="98f29-116">Office 365</span><span class="sxs-lookup"><span data-stu-id="98f29-116">Office 365</span></span> | <span data-ttu-id="98f29-117">Azure</span><span class="sxs-lookup"><span data-stu-id="98f29-117">Azure</span></span> |
| --- | --- | --- |
|   <span data-ttu-id="98f29-118">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="98f29-118">Display name</span></span> |<span data-ttu-id="98f29-119">Contoso</span><span class="sxs-lookup"><span data-stu-id="98f29-119">Contoso</span></span> |<span data-ttu-id="98f29-120">預設 Azure Active Directory (Azure AD) 目錄</span><span class="sxs-lookup"><span data-stu-id="98f29-120">Default Azure Active Directory (Azure AD) directory</span></span> |
|   <span data-ttu-id="98f29-121">網域名稱</span><span class="sxs-lookup"><span data-stu-id="98f29-121">Domain name</span></span> |<span data-ttu-id="98f29-122">contoso.com</span><span class="sxs-lookup"><span data-stu-id="98f29-122">contoso.com</span></span> |<span data-ttu-id="98f29-123">msmithhotmail.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="98f29-123">msmithhotmail.onmicrosoft.com</span></span> |

<span data-ttu-id="98f29-124">他想要在使用 Microsoft 帳戶登入 Azure 時，管理 Contoso 目錄中的使用者身分識別，如此就能啟用 Azure AD 功能，例如多重要素驗證 。</span><span class="sxs-lookup"><span data-stu-id="98f29-124">He wants to manage the user identities in the Contoso directory while he is signed in to Azure using his Microsoft account, so that he can enable Azure AD features such as multifactor authentication.</span></span> <span data-ttu-id="98f29-125">下圖可能有助於說明此程序。</span><span class="sxs-lookup"><span data-stu-id="98f29-125">The following diagram may help to illustrate the process.</span></span>

![兩個獨立目錄的管理圖表](./media/active-directory-manage-o365-subscription/AAD_O365_03.png)

<span data-ttu-id="98f29-127">在此情況下，這兩個目錄是彼此獨立的。</span><span class="sxs-lookup"><span data-stu-id="98f29-127">In this case, the two directories are independent of each other.</span></span>

## <a name="to-manage-two-independent-directories"></a><span data-ttu-id="98f29-128">管理兩個獨立的目錄</span><span class="sxs-lookup"><span data-stu-id="98f29-128">To manage two independent directories</span></span>
<span data-ttu-id="98f29-129">為了讓 Michael Smith 能夠在使用 msmith@hotmail.com 登入 Azure 時管理這兩個目錄，他必須完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="98f29-129">In order for Michael Smith to manage both directories while he is signed in to Azure as msmith@hotmail.com, he must complete the following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="98f29-130">只有當使用者使用 Microsoft 帳戶登入時，才能完成下列步驟。</span><span class="sxs-lookup"><span data-stu-id="98f29-130">These steps can be completed only when a user is signed in with a Microsoft account.</span></span> <span data-ttu-id="98f29-131">如果使用者使用工作或學校帳戶登入，就無法使用 [使用現有的目錄]  選項。</span><span class="sxs-lookup"><span data-stu-id="98f29-131">If the user is signed in with a work or school account, the option to **Use existing directory** isn't available.</span></span> <span data-ttu-id="98f29-132">工作或學校帳戶只能透過其主目錄 (也就是儲存工作或學校帳戶，且由公司或學校所擁有的目錄) 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="98f29-132">A work or school account can be authenticated only by its home directory (that is, the directory where the work or school account is stored, and that the business or school owns).</span></span>
>
>

1. <span data-ttu-id="98f29-133">以 msmith@hotmail.com 身分登入 [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="98f29-133">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as msmith@hotmail.com.</span></span>
2. <span data-ttu-id="98f29-134">按一下 [新增]  >  [應用程式服務]  >  [Active Directory]  >  [目錄]  >  [自訂建立]。</span><span class="sxs-lookup"><span data-stu-id="98f29-134">Click **New** > **App services** > **Active Directory** > **Directory** > **Custom Create**.</span></span>
3. <span data-ttu-id="98f29-135">按一下 [使用現有的目錄]，然後選取 [我現在已經可以登出]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="98f29-135">Click Use existing directory and select the **I am ready to be signed out now** checkbox.</span></span>
4. <span data-ttu-id="98f29-136">以 Contoso.onmicrosoft.com 的全域管理員身分登入 Azure 傳統入口網站 (例如 msmith@contoso.com)。</span><span class="sxs-lookup"><span data-stu-id="98f29-136">Sign in to the Azure classic portal as global admin of Contoso.onmicrosoft.com (for example, msmith@contoso.com).</span></span>
5. <span data-ttu-id="98f29-137">當系統出現 [搭配使用 Contoso 目錄和 Azure？] 提示時，按一下 [繼續]。</span><span class="sxs-lookup"><span data-stu-id="98f29-137">When prompted to **Use the Contoso directory with Azure?**, click **Continue**.</span></span>
6. <span data-ttu-id="98f29-138">按一下 [ **立即登出**]。</span><span class="sxs-lookup"><span data-stu-id="98f29-138">Click **Sign out now**.</span></span>
7. <span data-ttu-id="98f29-139">以 msmith@hotmail.com 身分登入 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="98f29-139">Sign in to the Azure classic portal as msmith@hotmail.com.</span></span> <span data-ttu-id="98f29-140">Contoso 目錄和預設目錄會出現在 Active Directory 延伸模組中。</span><span class="sxs-lookup"><span data-stu-id="98f29-140">The Contoso directory and the Default directory appear in the Active Directory extension.</span></span>

<span data-ttu-id="98f29-141">完成這些步驟之後，msmith@hotmail.com 會成為 Contoso 目錄中的全域管理員。</span><span class="sxs-lookup"><span data-stu-id="98f29-141">After completing these steps, msmith@hotmail.com is a global administrator in the Contoso directory.</span></span>

## <a name="to-administer-resources-as-the-global-admin"></a><span data-ttu-id="98f29-142">以全域管理員身分管理資源</span><span class="sxs-lookup"><span data-stu-id="98f29-142">To administer resources as the global admin</span></span>
<span data-ttu-id="98f29-143">現在我們假設 Jane Doe 需要管理與 msmith@hotmail.com 的 Azure 訂用帳戶相關聯的網站和資料庫資源。</span><span class="sxs-lookup"><span data-stu-id="98f29-143">Now let’s suppose that Jane Doe needs administer websites and database resources that are associated with the Azure subscription for msmith@hotmail.com.</span></span> <span data-ttu-id="98f29-144">在這麼做之前，Michael Smith 必須先完成下列額外步驟：</span><span class="sxs-lookup"><span data-stu-id="98f29-144">Before she can do that, Michael Smith needs to complete these additional steps:</span></span>

1. <span data-ttu-id="98f29-145">使用 Azure 訂用帳戶的服務管理員帳戶登入 [Azure 傳統入口網站](https://manage.windowsazure.com) (在此範例中為 msmith@hotmail.com)。</span><span class="sxs-lookup"><span data-stu-id="98f29-145">Sign in to the [Azure classic portal](https://manage.windowsazure.com) using the Service Administrator account for the Azure subscription (in this example, msmith@hotmail.com).</span></span>
2. <span data-ttu-id="98f29-146">將訂用帳戶移轉至 Contoso 目錄：按一下 [設定]  >  [訂用帳戶] > 選取訂用帳戶 > [編輯目錄] > 選取 [Contoso (Contoso.com)]。</span><span class="sxs-lookup"><span data-stu-id="98f29-146">Transfer the subscription to the Contoso directory: click **Settings** > **Subscriptions** > select the subscription > **Edit Directory** > select **Contoso (Contoso.com)**.</span></span> <span data-ttu-id="98f29-147">在移轉過程中，如果有工作或學校帳戶是訂用帳戶的共同管理員，則會移除這類帳戶。</span><span class="sxs-lookup"><span data-stu-id="98f29-147">As part of the transfer, any work or school accounts that are co-administrators of the subscription are removed.</span></span>
3. <span data-ttu-id="98f29-148">新增 Jane Doe 做為訂用帳戶的共同管理員：按一下 [設定]  >  [系統管理員] > 選取訂用帳戶 > [新增] > 輸入 **JohnDoe@Contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="98f29-148">Add Jane Doe as co-administrator of the subscription: click **Settings** > **Administrators** > select the subscription > **Add** > type **JohnDoe@Contoso.com**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98f29-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="98f29-149">Next steps</span></span>
<span data-ttu-id="98f29-150">如需訂用帳戶與目錄間的關聯性詳細資訊，請參閱 [如何將訂用帳戶如何關聯至目錄](active-directory-how-subscriptions-associated-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="98f29-150">For more information about the relationship between subscriptions and directories, see [How a subscription is associated with a directory](active-directory-how-subscriptions-associated-directory.md).</span></span>
