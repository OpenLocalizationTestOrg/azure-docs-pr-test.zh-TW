---
title: "您在 Azure 中的 Office 365 訂閱的 aaaManage hello 目錄 |Microsoft 文件"
description: "管理 Azure Active Directory 和 hello Azure 傳統入口網站使用 Office 365 訂用帳戶目錄"
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
ms.openlocfilehash: 4faf9936d7e94b85356a18adfcf3d2a48e5b025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-directory-for-your-office-365-subscription-in-azure"></a><span data-ttu-id="240bc-103">管理 Office 365 訂用帳戶在 Azure 中的 hello 目錄</span><span class="sxs-lookup"><span data-stu-id="240bc-103">Manage hello directory for your Office 365 subscription in Azure</span></span>
<span data-ttu-id="240bc-104">本文說明如何 toomanage Office 365 訂用帳戶，使用 hello Azure 傳統入口網站建立的目錄。</span><span class="sxs-lookup"><span data-stu-id="240bc-104">This article describes how toomanage a directory that was created for an Office 365 subscription, using hello Azure classic portal.</span></span> <span data-ttu-id="240bc-105">您必須是 hello 服務系統管理員或共同管理員的 Azure 訂用帳戶 toosign toohello Azure 傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="240bc-105">You must be either hello Service Administrator or a co-administrator of an Azure subscription toosign in toohello Azure classic portal.</span></span> <span data-ttu-id="240bc-106">如果您尚未擁有 Azure 訂用帳戶，您可以立即註冊 [免費 30 天試用版](https://azure.microsoft.com/trial/get-started-active-directory/) ，並使用此連結在 5 分鐘內部署第一個雲端解決方案。</span><span class="sxs-lookup"><span data-stu-id="240bc-106">If you don’t yet have an Azure subscription, you can sign up for a [free 30-day trial](https://azure.microsoft.com/trial/get-started-active-directory/) today and deploy your first cloud solution in under 5 minutes, using this link.</span></span> <span data-ttu-id="240bc-107">確定 toouse hello 工作或學校帳戶，您使用 toosign tooOffice 365。</span><span class="sxs-lookup"><span data-stu-id="240bc-107">Be sure toouse hello work or school account that you use toosign in tooOffice 365.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="240bc-108">Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="240bc-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="240bc-109">完成 hello Azure 訂用帳戶之後，您可以登入 toohello Azure 傳統入口網站，並存取 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="240bc-109">After you complete hello Azure subscription, you can sign in toohello Azure classic portal and access Azure services.</span></span> <span data-ttu-id="240bc-110">按一下 hello Active Directory 延伸模組 toomanage hello 驗證 Office 365 使用者的相同目錄。</span><span class="sxs-lookup"><span data-stu-id="240bc-110">Click hello Active Directory extension toomanage hello same directory that authenticates your Office 365 users.</span></span>

<span data-ttu-id="240bc-111">如果您已經有 Azure 訂用帳戶，就也簡單 hello 程序 toomanage 的其他目錄。</span><span class="sxs-lookup"><span data-stu-id="240bc-111">If you do already have an Azure subscription, hello process toomanage an additional directory is also straightforward.</span></span> <span data-ttu-id="240bc-112">在此範例中，Michael Smith 可能擁有適用於 Contoso.com 的 Office 365 訂用帳戶。他也擁有使用其 Microsoft 帳戶 msmith@hotmail.com 所註冊的 Azure 訂用帳戶。在此情況下，他要管理兩個目錄。</span><span class="sxs-lookup"><span data-stu-id="240bc-112">For example, Michael Smith might have an Office 365 subscription for Contoso.com. He also has an Azure subscription that he signed up for by using his Microsoft account, msmith@hotmail.com. In this case, he manages two directories.</span></span>

| <span data-ttu-id="240bc-113">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="240bc-113">Subscription</span></span> | <span data-ttu-id="240bc-114">Office 365</span><span class="sxs-lookup"><span data-stu-id="240bc-114">Office 365</span></span> | <span data-ttu-id="240bc-115">Azure</span><span class="sxs-lookup"><span data-stu-id="240bc-115">Azure</span></span> |
| --- | --- | --- |
|   <span data-ttu-id="240bc-116">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="240bc-116">Display name</span></span> |<span data-ttu-id="240bc-117">Contoso</span><span class="sxs-lookup"><span data-stu-id="240bc-117">Contoso</span></span> |<span data-ttu-id="240bc-118">預設 Azure Active Directory (Azure AD) 目錄</span><span class="sxs-lookup"><span data-stu-id="240bc-118">Default Azure Active Directory (Azure AD) directory</span></span> |
|   <span data-ttu-id="240bc-119">網域名稱</span><span class="sxs-lookup"><span data-stu-id="240bc-119">Domain name</span></span> |<span data-ttu-id="240bc-120">contoso.com</span><span class="sxs-lookup"><span data-stu-id="240bc-120">contoso.com</span></span> |<span data-ttu-id="240bc-121">msmithhotmail.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="240bc-121">msmithhotmail.onmicrosoft.com</span></span> |

<span data-ttu-id="240bc-122">他會登入 tooAzure 使用 Microsoft 帳戶，以便他可以啟用 Azure AD 功能，例如多重要素驗證時，他想 toomanage hello 使用者身分在 hello Contoso 目錄中。</span><span class="sxs-lookup"><span data-stu-id="240bc-122">He wants toomanage hello user identities in hello Contoso directory while he is signed in tooAzure using his Microsoft account, so that he can enable Azure AD features such as multifactor authentication.</span></span> <span data-ttu-id="240bc-123">下列圖表中的 hello 有助於 tooillustrate hello 程序。</span><span class="sxs-lookup"><span data-stu-id="240bc-123">hello following diagram may help tooillustrate hello process.</span></span>

![圖表 toomanage 兩個獨立的目錄](./media/active-directory-manage-o365-subscription/AAD_O365_03.png)

<span data-ttu-id="240bc-125">在此情況下，hello 兩個目錄彼此各自獨立的。</span><span class="sxs-lookup"><span data-stu-id="240bc-125">In this case, hello two directories are independent of each other.</span></span>

## <a name="toomanage-two-independent-directories"></a><span data-ttu-id="240bc-126">toomanage 兩個獨立的目錄</span><span class="sxs-lookup"><span data-stu-id="240bc-126">toomanage two independent directories</span></span>
<span data-ttu-id="240bc-127">若要針對 Michael Smith toomanage 兩個目錄時登入為 tooAzure msmith@hotmail.com，他必須完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="240bc-127">In order for Michael Smith toomanage both directories while he is signed in tooAzure as msmith@hotmail.com, he must complete hello following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="240bc-128">只有當使用者使用 Microsoft 帳戶登入時，才能完成下列步驟。</span><span class="sxs-lookup"><span data-stu-id="240bc-128">These steps can be completed only when a user is signed in with a Microsoft account.</span></span> <span data-ttu-id="240bc-129">如果 hello 使用者登入工作或學校帳戶，hello 選項太**使用現有目錄**無法使用。</span><span class="sxs-lookup"><span data-stu-id="240bc-129">If hello user is signed in with a work or school account, hello option too**Use existing directory** isn't available.</span></span> <span data-ttu-id="240bc-130">工作或學校帳戶可以只由其主目錄 （也就是 hello 目錄 hello 工作或學校帳戶的儲存位置，而該 hello 公司或學校擁有） 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="240bc-130">A work or school account can be authenticated only by its home directory (that is, hello directory where hello work or school account is stored, and that hello business or school owns).</span></span>
>
>

1. <span data-ttu-id="240bc-131">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)為msmith@hotmail.com。</span><span class="sxs-lookup"><span data-stu-id="240bc-131">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as msmith@hotmail.com.</span></span>
2. <span data-ttu-id="240bc-132">按一下 [新增]  >  [應用程式服務]  >  [Active Directory]  >  [目錄]  >  [自訂建立]。</span><span class="sxs-lookup"><span data-stu-id="240bc-132">Click **New** > **App services** > **Active Directory** > **Directory** > **Custom Create**.</span></span>
3. <span data-ttu-id="240bc-133">按一下 使用現有的目錄中，而且選取 hello**我已準備好立即登出的 toobe**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="240bc-133">Click Use existing directory and select hello **I am ready toobe signed out now** checkbox.</span></span>
4. <span data-ttu-id="240bc-134">登入 toohello Azure 傳統入口網站以 Contoso.onmicrosoft.com 的全域管理員身分 (例如， msmith@contoso.com)。</span><span class="sxs-lookup"><span data-stu-id="240bc-134">Sign in toohello Azure classic portal as global admin of Contoso.onmicrosoft.com (for example, msmith@contoso.com).</span></span>
5. <span data-ttu-id="240bc-135">當系統提示您太**搭配 Azure 使用 hello Contoso 目錄？**，按一下 **繼續**。</span><span class="sxs-lookup"><span data-stu-id="240bc-135">When prompted too**Use hello Contoso directory with Azure?**, click **Continue**.</span></span>
6. <span data-ttu-id="240bc-136">按一下 [ **立即登出**]。</span><span class="sxs-lookup"><span data-stu-id="240bc-136">Click **Sign out now**.</span></span>
7. <span data-ttu-id="240bc-137">登入 toohello Azure 傳統入口網站，做為msmith@hotmail.com。 hello Contoso 目錄和 hello 預設目錄會出現在 hello Active Directory 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="240bc-137">Sign in toohello Azure classic portal as msmith@hotmail.com. hello Contoso directory and hello Default directory appear in hello Active Directory extension.</span></span>

<span data-ttu-id="240bc-138">完成這些步驟之後, msmith@hotmail.com hello Contoso 目錄中的全域系統管理員。</span><span class="sxs-lookup"><span data-stu-id="240bc-138">After completing these steps, msmith@hotmail.com is a global administrator in hello Contoso directory.</span></span>

## <a name="tooadminister-resources-as-hello-global-admin"></a><span data-ttu-id="240bc-139">hello 全域管理員 tooadminister 資源</span><span class="sxs-lookup"><span data-stu-id="240bc-139">tooadminister resources as hello global admin</span></span>
<span data-ttu-id="240bc-140">現在讓我們假設 Jane Doe 需要管理的網站，和相關聯的資料庫資源 hello Azure 訂用帳戶msmith@hotmail.com。她可以這麼做，Michael Smith 必須 toocomplete 下列額外步驟：</span><span class="sxs-lookup"><span data-stu-id="240bc-140">Now let’s suppose that Jane Doe needs administer websites and database resources that are associated with hello Azure subscription for msmith@hotmail.com. Before she can do that, Michael Smith needs toocomplete these additional steps:</span></span>

1. <span data-ttu-id="240bc-141">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)hello Azure 訂用帳戶使用 hello 服務系統管理員帳戶 (在此範例中， msmith@hotmail.com)。</span><span class="sxs-lookup"><span data-stu-id="240bc-141">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) using hello Service Administrator account for hello Azure subscription (in this example, msmith@hotmail.com).</span></span>
2. <span data-ttu-id="240bc-142">傳送嗨訂用帳戶 toohello Contoso 目錄： 按一下**設定** > **訂閱**> 選取 hello 訂用帳戶 >**編輯目錄**> 選取**Contoso (Contoso.com)**。</span><span class="sxs-lookup"><span data-stu-id="240bc-142">Transfer hello subscription toohello Contoso directory: click **Settings** > **Subscriptions** > select hello subscription > **Edit Directory** > select **Contoso (Contoso.com)**.</span></span> <span data-ttu-id="240bc-143">Hello 傳輸、 工作或學校的一部分移除共同管理員的 hello 訂用帳戶的帳戶。</span><span class="sxs-lookup"><span data-stu-id="240bc-143">As part of hello transfer, any work or school accounts that are co-administrators of hello subscription are removed.</span></span>
3. <span data-ttu-id="240bc-144">Jane Doe 加入為 hello 訂用帳戶的共同管理員： 按一下**設定** > **管理員**> 選取 hello 訂用帳戶 >**新增**> 類型**JohnDoe@Contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="240bc-144">Add Jane Doe as co-administrator of hello subscription: click **Settings** > **Administrators** > select hello subscription > **Add** > type **JohnDoe@Contoso.com**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="240bc-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="240bc-145">Next steps</span></span>
<span data-ttu-id="240bc-146">如需 hello 訂用帳戶與目錄之間的關聯性的詳細資訊，請參閱[訂用帳戶的目錄相關聯的方式](active-directory-how-subscriptions-associated-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="240bc-146">For more information about hello relationship between subscriptions and directories, see [How a subscription is associated with a directory](active-directory-how-subscriptions-associated-directory.md).</span></span>
