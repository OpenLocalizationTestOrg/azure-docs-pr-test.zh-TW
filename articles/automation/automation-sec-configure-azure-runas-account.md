---
title: "aaaConfigure Azure 執行身分帳戶 |Microsoft 文件"
description: "本教學課程會引導您 hello 建立、 測試和範例使用在 Azure 自動化中的安全性主體驗證。"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
keywords: "服務主體名稱, setspn, azure 驗證"
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/06/2017
ms.author: magoedte
ROBOTS: NOINDEX
redirect_url: /azure/automation/
redirect_document_id: True
ms.openlocfilehash: 06675d2f6b9d8e7260ffaead4f2b2f61c2b98d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a><span data-ttu-id="88f85-104">使用 Azure 執行身分帳戶驗證 Runbook</span><span class="sxs-lookup"><span data-stu-id="88f85-104">Authenticate runbooks with an Azure Run As account</span></span>
<span data-ttu-id="88f85-105">本文章將示範如何 tooconfigure Azure 自動化帳戶 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="88f85-105">This article shows you how tooconfigure an Azure Automation account in hello Azure portal.</span></span> <span data-ttu-id="88f85-106">toodo 因此，您可以使用 hello 執行身分帳戶功能 tooauthenticate runbook 管理在 Azure 資源管理員] 或 [Azure 服務管理的資源。</span><span class="sxs-lookup"><span data-stu-id="88f85-106">toodo so, you use hello Run As account feature tooauthenticate runbooks managing resources in either Azure Resource Manager or Azure Service Management.</span></span>

<span data-ttu-id="88f85-107">當您在 hello Azure 入口網站中建立自動化帳戶時，您會自動建立兩個帳戶：</span><span class="sxs-lookup"><span data-stu-id="88f85-107">When you create an Automation account in hello Azure portal, you automatically create two accounts:</span></span>

* <span data-ttu-id="88f85-108">執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-108">A Run As account.</span></span> <span data-ttu-id="88f85-109">此帳戶會在 Azure Active Directory (Azure AD) 中建立服務主體，並建立一個憑證。</span><span class="sxs-lookup"><span data-stu-id="88f85-109">This account creates a service principal in Azure Active Directory (Azure AD) and a certificate.</span></span> <span data-ttu-id="88f85-110">它也會指派 hello 參與者角色型存取控制 (RBAC)，可使用 runbook 來管理資源管理員資源。</span><span class="sxs-lookup"><span data-stu-id="88f85-110">It also assigns hello Contributor role-based access control (RBAC), which manages Resource Manager resources by using runbooks.</span></span>
* <span data-ttu-id="88f85-111">傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-111">A Classic Run As account.</span></span> <span data-ttu-id="88f85-112">此帳戶上傳管理憑證，也就是使用服務管理 toomanage 或傳統資源使用 runbook。</span><span class="sxs-lookup"><span data-stu-id="88f85-112">This account uploads a management certificate, which is used toomanage Service Management or classic resources by using runbooks.</span></span>

<span data-ttu-id="88f85-113">必須建立您的自動化帳戶的您，並可協助您快速開始建置及部署 runbook toosupport 簡化 hello 程序自動化。</span><span class="sxs-lookup"><span data-stu-id="88f85-113">Creating an Automation account simplifies hello process for you and helps you quickly start building and deploying runbooks toosupport your automation needs.</span></span>

<span data-ttu-id="88f85-114">使用執行身分和傳統執行身分帳戶，您可以︰</span><span class="sxs-lookup"><span data-stu-id="88f85-114">With Run As and Classic Run As accounts, you can:</span></span>

* <span data-ttu-id="88f85-115">當資源管理員或服務管理資源管理 hello Azure 入口網站中的 runbook 從 Azure 提供標準化的方式 tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="88f85-115">Provide a standardized way tooauthenticate with Azure when you manage Resource Manager or Service Management resources from runbooks in hello Azure portal.</span></span>
* <span data-ttu-id="88f85-116">自動化 hello 使用通用的 runbook，您可以設定 Azure 的警示。</span><span class="sxs-lookup"><span data-stu-id="88f85-116">Automate hello use of global runbooks, which you can configure in Azure Alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="88f85-117">hello [Azure 警示的整合功能](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)與自動化全域 runbook 需要使用已設定執行身分帳戶與傳統執行身分帳戶的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-117">hello [Azure Alert integration feature](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) with Automation global runbooks requires an Automation account that's configured with a Run As account and a Classic Run As account.</span></span> <span data-ttu-id="88f85-118">您可以選取自動化帳戶已有定義執行身分和傳統執行身分帳戶，或您可以選擇 toocreate 新的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-118">You can select an Automation account that already has defined Run As and Classic Run As accounts, or you can choose toocreate a new Automation account.</span></span>
>  

<span data-ttu-id="88f85-119">本文示範 toocreate 自動化帳戶從 hello Azure 入口網站如何使用 Azure PowerShell 更新自動化帳戶、 管理 hello 帳戶設定，以及驗證您的 runbook。</span><span class="sxs-lookup"><span data-stu-id="88f85-119">This article shows how toocreate an Automation account from hello Azure portal, update an Automation account by using Azure PowerShell, manage hello account configuration, and authenticate in your runbooks.</span></span>

<span data-ttu-id="88f85-120">您開始建立自動化帳戶之前，它會是個不錯的主意 toounderstand，並考慮下列 hello:</span><span class="sxs-lookup"><span data-stu-id="88f85-120">Before you begin creating an Automation account, it's a good idea toounderstand and consider hello following:</span></span>

* <span data-ttu-id="88f85-121">建立自動化帳戶，不會影響您可能已經在傳統的 hello 或資源管理員部署模型中建立的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-121">Creating an Automation account does not affect Automation accounts you might have already created in either hello classic or Resource Manager deployment model.</span></span>
* <span data-ttu-id="88f85-122">hello 程序只適用於您在 hello Azure 入口網站中建立的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-122">hello process works only for Automation accounts that you create in hello Azure portal.</span></span> <span data-ttu-id="88f85-123">嘗試 toocreate hello Azure 傳統入口網站的帳戶不會複寫 hello 執行身分帳戶設定。</span><span class="sxs-lookup"><span data-stu-id="88f85-123">Attempting toocreate an account from hello Azure classic portal does not replicate hello Run As account configuration.</span></span>
* <span data-ttu-id="88f85-124">如果您已經有 runbook 與資產 （例如排程或變數） 中發生 toomanage 傳統資源，而且您想 runbook tooauthenticate 與 hello 新傳統執行身分帳戶，執行 hello 下列任一動作：</span><span class="sxs-lookup"><span data-stu-id="88f85-124">If you already have runbooks and assets (such as schedules or variables) in place toomanage classic resources, and you want runbooks tooauthenticate with hello new Classic Run As account, do either of hello following:</span></span>

  * <span data-ttu-id="88f85-125">toocreate 傳統執行身分帳戶，請遵循 hello < 管理您的執行身分帳戶 > 一節中的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="88f85-125">toocreate a Classic Run As account, follow hello instructions in hello "Managing your Run As account" section.</span></span> 
  * <span data-ttu-id="88f85-126">tooupdate hello 「 使用 PowerShell 來更新您的自動化帳戶 」 一節中的現有帳戶，使用 hello PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="88f85-126">tooupdate your existing account, use hello PowerShell script in hello "Update your Automation account by using PowerShell" section.</span></span>
* <span data-ttu-id="88f85-127">tooauthenticate 使用 hello 新執行身分帳戶和傳統執行與自動化帳戶，需要您現有的 runbook 與 hello hello > 一節中提供的範例程式碼的 toomodify[驗證程式碼範例](#authentication-code-examples)。</span><span class="sxs-lookup"><span data-stu-id="88f85-127">tooauthenticate by using hello new Run As account and Classic Run As Automation account, you  need toomodify your existing runbooks with hello example code provided in hello section [Authentication code examples](#authentication-code-examples).</span></span>

    >[!NOTE]
    ><span data-ttu-id="88f85-128">hello 執行身分帳戶是針對使用 hello 憑證為基礎的服務主體的資源管理員資源進行驗證。</span><span class="sxs-lookup"><span data-stu-id="88f85-128">hello Run As account is for authentication against Resource Manager resources using hello certificate-based service principal.</span></span> <span data-ttu-id="88f85-129">hello 傳統執行身分帳戶是對服務管理資源的管理憑證進行驗證。</span><span class="sxs-lookup"><span data-stu-id="88f85-129">hello Classic Run As account is for authenticating against Service Management resources with a management certificate.</span></span>

## <a name="create-an-automation-account-from-hello-azure-portal"></a><span data-ttu-id="88f85-130">從 hello Azure 入口網站中建立自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="88f85-130">Create an Automation account from hello Azure portal</span></span>
<span data-ttu-id="88f85-131">在本節中，您可以建立 Azure 自動化帳戶從 hello 接著會建立執行身分帳戶和傳統執行身分帳戶的 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="88f85-131">In this section, you create an Azure Automation account from hello Azure portal, which in turn creates both a Run As account and a Classic Run As account.</span></span>

>[!NOTE]
><span data-ttu-id="88f85-132">toocreate 自動化帳戶，您必須是 hello 服務系統管理員角色的成員或 hello 訂用帳戶會授與存取 toohello 訂用帳戶的共同管理員。</span><span class="sxs-lookup"><span data-stu-id="88f85-132">toocreate an Automation account, you must be a member of hello Service Admins role or co-administrator of hello subscription that is granting access toohello subscription.</span></span> <span data-ttu-id="88f85-133">您也必須新增為使用者 toothat 訂用帳戶的預設 Active Directory 執行個體。</span><span class="sxs-lookup"><span data-stu-id="88f85-133">You must also be added as a user toothat subscription's default Active Directory instance.</span></span> <span data-ttu-id="88f85-134">hello 帳戶不需要 toobe 的特殊權限的角色指派。</span><span class="sxs-lookup"><span data-stu-id="88f85-134">hello account does not need toobe assigned a privileged role.</span></span>
>
><span data-ttu-id="88f85-135">如果您不是成員的 hello 訂用帳戶的 Active Directory 執行個體加入 toohello hello 訂用帳戶的共同管理員角色之前，您將會做為來賓新增 tooActive 目錄。</span><span class="sxs-lookup"><span data-stu-id="88f85-135">If you are not a member of hello subscription’s Active Directory instance before you are added toohello co-administrator role of hello subscription, you will be added tooActive Directory as a guest.</span></span> <span data-ttu-id="88f85-136">在此例中，您會收到 「 您沒有權限 toocreate...」</span><span class="sxs-lookup"><span data-stu-id="88f85-136">In this instance, you will receive a “You do not have permissions toocreate…”</span></span> <span data-ttu-id="88f85-137">在 hello 警告**加入自動化帳戶**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="88f85-137">warning on hello **Add Automation Account** blade.</span></span>
>
><span data-ttu-id="88f85-138">Toohello 共同系統管理員角色首先會從 hello 訂用帳戶的 Active Directory 執行個體，並重新加入 toomake 加入的使用者其完整的使用者在 Active Directory 中。</span><span class="sxs-lookup"><span data-stu-id="88f85-138">Users who were added toohello co-administrator role first can be removed from hello subscription's Active Directory instance and re-added toomake them a full User in Active Directory.</span></span> <span data-ttu-id="88f85-139">tooverify 這種情況的 hello **Azure Active Directory** hello 選取 Azure 入口網站中的窗格**使用者和群組**、 選取**所有使用者**後，您選取hello 特定使用者，選取**設定檔**。</span><span class="sxs-lookup"><span data-stu-id="88f85-139">tooverify this situation from hello **Azure Active Directory** pane in hello Azure portal by selecting **Users and groups**, selecting **All users** and, after you select hello specific user, selecting **Profile**.</span></span> <span data-ttu-id="88f85-140">hello 值 hello**使用者類型**hello 使用者設定檔 下的屬性不可等於**客體**。</span><span class="sxs-lookup"><span data-stu-id="88f85-140">hello value of hello **User type** attribute under hello users profile should not equal **Guest**.</span></span>
>

1. <span data-ttu-id="88f85-141">登入 toohello hello 訂用帳戶系統管理員角色的成員且 hello 訂用帳戶的共同管理員帳戶的 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="88f85-141">Sign in toohello Azure portal with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>

2. <span data-ttu-id="88f85-142">選取 [自動化帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="88f85-142">Select **Automation Accounts**.</span></span>

3. <span data-ttu-id="88f85-143">在 hello**自動化帳戶**刀鋒視窗中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="88f85-143">On hello **Automation Accounts** blade, click **Add**.</span></span>
<span data-ttu-id="88f85-144">hello**加入自動化帳戶**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="88f85-144">hello **Add Automation Account** blade opens.</span></span>

 ![hello [加入自動化帳戶] 刀鋒視窗](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > <span data-ttu-id="88f85-146">如果您的帳戶不是 hello 訂用帳戶系統管理員角色的成員和 hello 訂用帳戶的共同管理員，hello 上會顯示下列警告 hello**加入自動化帳戶**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="88f85-146">If your account is not a member of hello subscription administrators role and co-administrator of hello subscription, hello following warning is displayed on hello **Add Automation Account** blade:</span></span>
   >
   >![加入自動化帳戶警告](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. <span data-ttu-id="88f85-148">在 hello**加入自動化帳戶**刀鋒視窗中的，在 hello**名稱**方塊中，輸入新的自動化帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="88f85-148">On hello **Add Automation Account** blade, in hello **Name** box, type a name for your new Automation account.</span></span>

5. <span data-ttu-id="88f85-149">如果您有多個訂用帳戶時，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="88f85-149">If you have more than one subscription, do hello following:</span></span>

    <span data-ttu-id="88f85-150">a.</span><span class="sxs-lookup"><span data-stu-id="88f85-150">a.</span></span> <span data-ttu-id="88f85-151">在下**訂用帳戶**，指定一個 hello 新帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-151">Under **Subscription**, specify one for hello new account.</span></span>

    <span data-ttu-id="88f85-152">b.</span><span class="sxs-lookup"><span data-stu-id="88f85-152">b.</span></span> <span data-ttu-id="88f85-153">在 [資源群組] 底下，按一下 [建立新的] 或 [使用現有的]。</span><span class="sxs-lookup"><span data-stu-id="88f85-153">Under **Resource Group**, click **Create new** or **Use existing**.</span></span>

    <span data-ttu-id="88f85-154">c.</span><span class="sxs-lookup"><span data-stu-id="88f85-154">c.</span></span> <span data-ttu-id="88f85-155">在 [位置] 底下，指定 Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="88f85-155">Under **Location**, specify an Azure datacenter.</span></span>

6. <span data-ttu-id="88f85-156">在 建立 Azure 執行身分帳戶 底下選取 是，然後按一下建立。</span><span class="sxs-lookup"><span data-stu-id="88f85-156">Under **Create Azure Run As account**, select **Yes**, and then click **Create**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="88f85-157">如果您選擇不 toocreate hello 執行身分帳戶選取**否**，會顯示警告訊息 hello**加入自動化帳戶**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="88f85-157">If you choose not toocreate hello Run As account by selecting **No**, a warning message is displayed hello **Add Automation Account** blade.</span></span> <span data-ttu-id="88f85-158">雖然 hello 帳戶建立 hello Azure 入口網站中，它並沒有對應的驗證識別身分，在您的傳統或資源管理員的訂用帳戶目錄服務中。</span><span class="sxs-lookup"><span data-stu-id="88f85-158">Although hello account is created in hello Azure portal, it does not have a corresponding authentication identity within your classic or Resource Manager subscription directory service.</span></span> <span data-ttu-id="88f85-159">因此，hello 帳戶已無存取 tooresources 您訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="88f85-159">Consequently, hello account has no access tooresources in your subscription.</span></span> <span data-ttu-id="88f85-160">此情況會導致參考此帳戶的任何 Runbook 無法進行驗證，也無法對這些部署模型中的資源執行工作。</span><span class="sxs-lookup"><span data-stu-id="88f85-160">This scenario prevents any runbooks that reference this account from authenticating and performing tasks against resources in those deployment models.</span></span>
   >
   > ![Hello [加入自動化帳戶] 刀鋒視窗上的警告訊息](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > <span data-ttu-id="88f85-162">此外，因為不建立 hello 服務主體、 hello 參與者角色未指派。</span><span class="sxs-lookup"><span data-stu-id="88f85-162">Additionally, because hello service principal is not created, hello Contributor role is not assigned.</span></span>
   >

7. <span data-ttu-id="88f85-163">而 Azure 會建立 hello 自動化帳戶，您可以追蹤在 hello 進度**通知**hello 功能表。</span><span class="sxs-lookup"><span data-stu-id="88f85-163">While Azure creates hello Automation account, you can track hello progress under **Notifications** from hello menu.</span></span>

### <a name="resources"></a><span data-ttu-id="88f85-164">資源</span><span class="sxs-lookup"><span data-stu-id="88f85-164">Resources</span></span>
<span data-ttu-id="88f85-165">已成功建立 hello 自動化帳戶時，會自動為您建立數個資源。</span><span class="sxs-lookup"><span data-stu-id="88f85-165">When hello Automation account is successfully created, several resources are automatically created for you.</span></span> <span data-ttu-id="88f85-166">下列兩個資料表的 hello 摘要 hello 資源：</span><span class="sxs-lookup"><span data-stu-id="88f85-166">hello resources are summarized in hello following two tables:</span></span>

#### <a name="run-as-account-resources"></a><span data-ttu-id="88f85-167">執行身分帳戶資源</span><span class="sxs-lookup"><span data-stu-id="88f85-167">Run As account resources</span></span>

| <span data-ttu-id="88f85-168">資源</span><span class="sxs-lookup"><span data-stu-id="88f85-168">Resource</span></span> | <span data-ttu-id="88f85-169">說明</span><span class="sxs-lookup"><span data-stu-id="88f85-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="88f85-170">AzureAutomationTutorial Runbook</span><span class="sxs-lookup"><span data-stu-id="88f85-170">AzureAutomationTutorial Runbook</span></span> | <span data-ttu-id="88f85-171">範例圖形化 runbook，示範如何使用 tooauthenticate hello 執行身分帳戶，並取得 hello 資源管理員的所有資源。</span><span class="sxs-lookup"><span data-stu-id="88f85-171">An example graphical runbook that demonstrates how tooauthenticate by using hello Run As account and gets all hello Resource Manager resources.</span></span> |
| <span data-ttu-id="88f85-172">AzureAutomationTutorialScript Runbook</span><span class="sxs-lookup"><span data-stu-id="88f85-172">AzureAutomationTutorialScript Runbook</span></span> | <span data-ttu-id="88f85-173">此範例 PowerShell runbook 會示範如何使用 tooauthenticate hello 執行身分帳戶，並取得 hello 資源管理員的所有資源。</span><span class="sxs-lookup"><span data-stu-id="88f85-173">An example PowerShell runbook that demonstrates how tooauthenticate by using hello Run As account and gets all hello Resource Manager resources.</span></span> |
| <span data-ttu-id="88f85-174">AzureRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="88f85-174">AzureRunAsCertificate</span></span> | <span data-ttu-id="88f85-175">hello 憑證資產會自動建立，當您建立自動化帳戶，或使用現有的帳戶的 PowerShell 指令碼後面的 hello。</span><span class="sxs-lookup"><span data-stu-id="88f85-175">hello certificate asset that's automatically created when you create an Automation account or use hello following PowerShell script for an existing account.</span></span> <span data-ttu-id="88f85-176">hello 憑證可讓您使用 Azure tooauthenticate，讓您可以從 runbook 來管理 Azure 資源管理員資源。</span><span class="sxs-lookup"><span data-stu-id="88f85-176">hello certificate allows you tooauthenticate with Azure so that you can manage Azure Resource Manager resources from runbooks.</span></span> <span data-ttu-id="88f85-177">hello 憑證都有一年的使用期限。</span><span class="sxs-lookup"><span data-stu-id="88f85-177">hello certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="88f85-178">AzureRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="88f85-178">AzureRunAsConnection</span></span> | <span data-ttu-id="88f85-179">hello 連線資產會自動建立，當您建立自動化帳戶，或使用現有帳戶的 hello PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="88f85-179">hello connection asset that's automatically created when you create an Automation account or use hello PowerShell script for an existing account.</span></span> |

#### <a name="classic-run-as-account-resources"></a><span data-ttu-id="88f85-180">傳統執行身分帳戶資源</span><span class="sxs-lookup"><span data-stu-id="88f85-180">Classic Run As account resources</span></span>

| <span data-ttu-id="88f85-181">資源</span><span class="sxs-lookup"><span data-stu-id="88f85-181">Resource</span></span> | <span data-ttu-id="88f85-182">說明</span><span class="sxs-lookup"><span data-stu-id="88f85-182">Description</span></span> |
| --- | --- |
| <span data-ttu-id="88f85-183">AzureClassicAutomationTutorial Runbook</span><span class="sxs-lookup"><span data-stu-id="88f85-183">AzureClassicAutomationTutorial Runbook</span></span> | <span data-ttu-id="88f85-184">取得所有訂用帳戶中的 hello 傳統部署模型，使用 hello 傳統執行身分帳戶 （憑證），來建立和再將 hello VM 名稱和狀態 hello Vm 範例圖形化 runbook。</span><span class="sxs-lookup"><span data-stu-id="88f85-184">An example graphical runbook that gets all hello VMs that are created using hello classic deployment model in a subscription by using hello Classic Run As account (certificate), and then writes hello VM name and status.</span></span> |
| <span data-ttu-id="88f85-185">AzureClassicAutomationTutorial 指令碼 Runbook</span><span class="sxs-lookup"><span data-stu-id="88f85-185">AzureClassicAutomationTutorial Script Runbook</span></span> | <span data-ttu-id="88f85-186">取得所有的範例 PowerShell runbook hello 傳統訂用帳戶中的 Vm 使用 hello 傳統執行身分帳戶 （憑證），並寫入然後 hello VM 名稱和狀態。</span><span class="sxs-lookup"><span data-stu-id="88f85-186">An example PowerShell runbook that gets all hello classic VMs in a subscription by using hello Classic Run As account (certificate), and then writes hello VM name and status.</span></span> |
| <span data-ttu-id="88f85-187">AzureClassicRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="88f85-187">AzureClassicRunAsCertificate</span></span> | <span data-ttu-id="88f85-188">您搭配 Azure 使用 tooauthenticate，使您可以管理 Azure 傳統資源從 runbook 自動建立 hello 憑證資產。</span><span class="sxs-lookup"><span data-stu-id="88f85-188">hello automatically created certificate asset that you use tooauthenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> <span data-ttu-id="88f85-189">hello 憑證都有一年的使用期限。</span><span class="sxs-lookup"><span data-stu-id="88f85-189">hello certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="88f85-190">AzureClassicRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="88f85-190">AzureClassicRunAsConnection</span></span> | <span data-ttu-id="88f85-191">您搭配 Azure 使用 tooauthenticate，以便您可以從 runbook 來管理 Azure 傳統資源 hello 自動建立的連線資產。</span><span class="sxs-lookup"><span data-stu-id="88f85-191">hello automatically created connection asset that you use tooauthenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> |

## <a name="verify-run-as-authentication"></a><span data-ttu-id="88f85-192">確認執行身分驗證</span><span class="sxs-lookup"><span data-stu-id="88f85-192">Verify Run As authentication</span></span>
<span data-ttu-id="88f85-193">執行使用 hello 新執行身分帳戶可以成功進行驗證的小型測試 tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="88f85-193">Perform a small test tooconfirm that you can successfully authenticate by using hello new Run As account.</span></span>

1. <span data-ttu-id="88f85-194">在 hello Azure 入口網站，開啟您稍早建立的 hello 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-194">In hello Azure portal, open hello Automation account that you created earlier.</span></span>

2. <span data-ttu-id="88f85-195">按一下 hello **Runbook**磚 tooopen hello runbook 的清單。</span><span class="sxs-lookup"><span data-stu-id="88f85-195">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>

3. <span data-ttu-id="88f85-196">選取 hello **AzureAutomationTutorialScript** runbook，然後按一下**啟動**toostart hello runbook。</span><span class="sxs-lookup"><span data-stu-id="88f85-196">Select hello **AzureAutomationTutorialScript** runbook, and then click **Start** toostart hello runbook.</span></span> <span data-ttu-id="88f85-197">發生下列事件的 hello:</span><span class="sxs-lookup"><span data-stu-id="88f85-197">hello following events occur:</span></span>
 * <span data-ttu-id="88f85-198">A [runbook 工作](automation-runbook-execution.md)建立時，hello**作業**刀鋒視窗會顯示，而 hello 工作狀態會顯示在 hello**工作摘要**磚。</span><span class="sxs-lookup"><span data-stu-id="88f85-198">A [runbook job](automation-runbook-execution.md) is created, hello **Job** blade is displayed, and hello job status is displayed in hello **Job Summary** tile.</span></span>
 * <span data-ttu-id="88f85-199">hello 作業狀態的開頭為**排入佇列**，表示它正在等待在 hello 雲端 toobecome 可用的 runbook worker。</span><span class="sxs-lookup"><span data-stu-id="88f85-199">hello job status begins as **Queued**, indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span>
 * <span data-ttu-id="88f85-200">hello 狀態會變成**起始**當背景工作宣告 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="88f85-200">hello status becomes **Starting** when a worker claims hello job.</span></span>
 * <span data-ttu-id="88f85-201">hello 狀態會變成**執行**hello runbook 開始執行時。</span><span class="sxs-lookup"><span data-stu-id="88f85-201">hello status becomes **Running** when hello runbook starts running.</span></span>
 * <span data-ttu-id="88f85-202">Hello runbook 工作完成時執行，您應該會看到狀態為**已完成**。</span><span class="sxs-lookup"><span data-stu-id="88f85-202">When hello runbook job has finished running, you should see a status of **Completed**.</span></span>

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. <span data-ttu-id="88f85-203">toosee hello hello runbook 的詳細的結果，請按一下 hello**輸出**磚。</span><span class="sxs-lookup"><span data-stu-id="88f85-203">toosee hello detailed results of hello runbook, click hello **Output** tile.</span></span>  
<span data-ttu-id="88f85-204">hello**輸出**刀鋒視窗會顯示，其中該 hello runbook 順利通過驗證，並傳回一份 hello 資源群組中所提供的所有資源。</span><span class="sxs-lookup"><span data-stu-id="88f85-204">hello **Output** blade is displayed, showing that hello runbook has successfully authenticated and returned a list of all resources available in hello resource group.</span></span>

5. <span data-ttu-id="88f85-205">關閉 hello**輸出**刀鋒視窗 tooreturn toohello**工作摘要**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="88f85-205">Close hello **Output** blade tooreturn toohello **Job Summary** blade.</span></span>

6. <span data-ttu-id="88f85-206">關閉 hello**工作摘要**刀鋒視窗，然後 hello 對應**AzureAutomationTutorialScript** runbook 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="88f85-206">Close hello **Job Summary** blade and hello corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="verify-classic-run-as-authentication"></a><span data-ttu-id="88f85-207">確認傳統執行身分驗證</span><span class="sxs-lookup"><span data-stu-id="88f85-207">Verify Classic Run As authentication</span></span>
<span data-ttu-id="88f85-208">執行類似的小型測試 tooconfirm 使用 hello 新傳統執行身分帳戶可以成功進行驗證。</span><span class="sxs-lookup"><span data-stu-id="88f85-208">Perform a similar small test tooconfirm that you can successfully authenticate by using hello new Classic Run As account.</span></span>

1. <span data-ttu-id="88f85-209">在 hello Azure 入口網站，開啟您稍早建立的 hello 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-209">In hello Azure portal, open hello Automation account that you created earlier.</span></span>

2. <span data-ttu-id="88f85-210">按一下 hello **Runbook**磚 tooopen hello runbook 的清單。</span><span class="sxs-lookup"><span data-stu-id="88f85-210">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>

3. <span data-ttu-id="88f85-211">選取 hello **AzureClassicAutomationTutorialScript** runbook，然後按一下**啟動**太啟動 hello runbook。</span><span class="sxs-lookup"><span data-stu-id="88f85-211">Select hello **AzureClassicAutomationTutorialScript** runbook, and then click **Start** too start hello runbook.</span></span> <span data-ttu-id="88f85-212">發生下列事件的 hello:</span><span class="sxs-lookup"><span data-stu-id="88f85-212">hello following events occur:</span></span>

 * <span data-ttu-id="88f85-213">A [runbook 工作](automation-runbook-execution.md)建立時，hello**作業**刀鋒視窗會顯示，而 hello 工作狀態會顯示在 hello**工作摘要**磚。</span><span class="sxs-lookup"><span data-stu-id="88f85-213">A [runbook job](automation-runbook-execution.md) is created, hello **Job** blade is displayed, and hello job status is displayed in hello **Job Summary** tile.</span></span>
 * <span data-ttu-id="88f85-214">hello 作業狀態的開頭為**排入佇列**，表示它正在等待在 hello 雲端 toobecome 可用的 runbook worker。</span><span class="sxs-lookup"><span data-stu-id="88f85-214">hello job status begins as **Queued**, indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span>
 * <span data-ttu-id="88f85-215">hello 狀態會變成**起始**當背景工作宣告 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="88f85-215">hello status becomes **Starting** when a worker claims hello job.</span></span>
 * <span data-ttu-id="88f85-216">hello 狀態會變成**執行**hello runbook 開始執行時。</span><span class="sxs-lookup"><span data-stu-id="88f85-216">hello status becomes **Running** when hello runbook starts running.</span></span>
 * <span data-ttu-id="88f85-217">Hello runbook 工作完成時執行，您應該會看到狀態為**已完成**。</span><span class="sxs-lookup"><span data-stu-id="88f85-217">When hello runbook job has finished running, you should see a status of **Completed**.</span></span>

    ![安全性主體 Runbook 測試](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. <span data-ttu-id="88f85-219">toosee hello hello runbook 的詳細的結果，請按一下 hello**輸出**磚。</span><span class="sxs-lookup"><span data-stu-id="88f85-219">toosee hello detailed results of hello runbook, click hello **Output** tile.</span></span>  
<span data-ttu-id="88f85-220">hello**輸出**刀鋒視窗會顯示，其中該 hello runbook 成功通過驗證，並傳回的清單中的所有傳統 Vm hello 訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="88f85-220">hello **Output** blade is displayed, showing that hello runbook has successfully authenticated and returned a list of all classic VMs in hello subscription.</span></span>

5. <span data-ttu-id="88f85-221">關閉 hello**輸出**刀鋒視窗 tooreturn toohello**工作摘要**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="88f85-221">Close hello **Output** blade tooreturn toohello **Job Summary** blade.</span></span>

6. <span data-ttu-id="88f85-222">關閉 hello**工作摘要**刀鋒視窗，然後 hello 對應**AzureAutomationTutorialScript** runbook 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="88f85-222">Close hello **Job Summary** blade and hello corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="managing-your-run-as-account"></a><span data-ttu-id="88f85-223">管理執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="88f85-223">Managing your Run As account</span></span>
<span data-ttu-id="88f85-224">在某個時間點您的自動化帳戶到期前，您將需要 toorenew hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="88f85-224">At some point before your Automation account expires, you will need toorenew hello certificate.</span></span> <span data-ttu-id="88f85-225">如果您認為該 hello 執行身分帳戶已遭洩漏，您可以刪除並重新建立它。</span><span class="sxs-lookup"><span data-stu-id="88f85-225">If you believe that hello Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="88f85-226">本章節將討論如何 tooperform 這些作業。</span><span class="sxs-lookup"><span data-stu-id="88f85-226">This section discusses how tooperform these operations.</span></span>

### <a name="self-signed-certificate-renewal"></a><span data-ttu-id="88f85-227">自我簽署憑證更新</span><span class="sxs-lookup"><span data-stu-id="88f85-227">Self-signed certificate renewal</span></span>
<span data-ttu-id="88f85-228">hello hello 執行身分帳戶建立的自我簽署的憑證到期從建立 hello 日期起一年。</span><span class="sxs-lookup"><span data-stu-id="88f85-228">hello self-signed certificate that you created for hello Run As account expires one year from hello date of creation.</span></span> <span data-ttu-id="88f85-229">您可以在該憑證到期前隨時更新憑證。</span><span class="sxs-lookup"><span data-stu-id="88f85-229">You can renew it at any time before it expires.</span></span> <span data-ttu-id="88f85-230">當您更新它時，hello 目前有效的憑證會保留的 tooensure 任何 runbook 的執行中或正在執行，會進入佇列，並可向 hello 執行身分帳戶，不會產生負面影響。</span><span class="sxs-lookup"><span data-stu-id="88f85-230">When you renew it, hello current valid certificate is retained tooensure that any runbooks that are queued up or actively running, and that authenticate with hello Run As account, are not negatively affected.</span></span> <span data-ttu-id="88f85-231">hello 憑證到期日前就持續有效。</span><span class="sxs-lookup"><span data-stu-id="88f85-231">hello certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="88f85-232">如果您已設定您自動化執行身分帳戶 toouse 您企業憑證授權單位所核發的憑證，且您使用此選項，將會自我簽署憑證所取代 hello 企業憑證。</span><span class="sxs-lookup"><span data-stu-id="88f85-232">If you have configured your Automation Run As account toouse a certificate issued by your enterprise certificate authority and you use this option, hello enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="88f85-233">toorenew hello 憑證，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="88f85-233">toorenew hello certificate, do hello following:</span></span>

1. <span data-ttu-id="88f85-234">在 hello Azure 入口網站，開啟 hello 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-234">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="88f85-235">在 hello**自動化帳戶**刀鋒視窗中的，在 hello**帳戶屬性**窗格下**帳戶設定**，選取**執行身分帳戶**。</span><span class="sxs-lookup"><span data-stu-id="88f85-235">On hello **Automation Account** blade, in hello **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![自動化帳戶的屬性窗格](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. <span data-ttu-id="88f85-237">在 hello**執行身分帳戶**屬性刀鋒視窗中，選取任一 hello 執行身分帳戶或 hello 傳統執行身分帳戶，您想要 toorenew hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="88f85-237">On hello **Run As Accounts** properties blade, select either hello Run As account or hello Classic Run As account that you want toorenew hello certificate for.</span></span>

4. <span data-ttu-id="88f85-238">在 hello**屬性**hello 刀鋒視窗中選取帳戶，請按一下**更新憑證**。</span><span class="sxs-lookup"><span data-stu-id="88f85-238">On hello **Properties** blade for hello selected account, click **Renew certificate**.</span></span>

    ![更新執行身分帳戶的憑證](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="88f85-240">當更新 hello 憑證後時，您可以追蹤下的 hello 進度**通知**hello 功能表。</span><span class="sxs-lookup"><span data-stu-id="88f85-240">While hello certificate is being renewed, you can track hello progress under **Notifications** from hello menu.</span></span>

### <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="88f85-241">刪除執行身分或傳統執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="88f85-241">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="88f85-242">本章節描述如何 toodelete 並重新建立執行身分或傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-242">This section describes how toodelete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="88f85-243">當您執行此動作時，會保留 hello 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-243">When you perform this action, hello Automation account is retained.</span></span> <span data-ttu-id="88f85-244">刪除執行身分或傳統執行身分帳戶後，您可以在 hello Azure 入口網站中重新建立它。</span><span class="sxs-lookup"><span data-stu-id="88f85-244">After you delete a Run As or Classic Run As account, you can re-create it in hello Azure portal.</span></span>

1. <span data-ttu-id="88f85-245">在 hello Azure 入口網站，開啟 hello 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-245">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="88f85-246">在 [hello**自動化帳戶**刀鋒視窗中的，hello 帳戶屬性] 窗格中，選取**執行身分帳戶**。</span><span class="sxs-lookup"><span data-stu-id="88f85-246">On hello **Automation account** blade, in hello account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="88f85-247">在 hello**執行身分帳戶**想 toodelete 屬性刀鋒視窗中，選取任一 hello 執行身分帳戶 」 或 「 傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-247">On hello **Run As Accounts** properties blade, select either hello Run As account or Classic Run As account that you want toodelete.</span></span> <span data-ttu-id="88f85-248">然後，在 hello**屬性**hello 刀鋒視窗中選取帳戶，請按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="88f85-248">Then, on hello **Properties** blade for hello selected account, click **Delete**.</span></span>

 ![刪除執行身分帳戶](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. <span data-ttu-id="88f85-250">正在刪除 hello 帳戶，而您可以追蹤下的 hello 進度**通知**hello 功能表。</span><span class="sxs-lookup"><span data-stu-id="88f85-250">While hello account is being deleted, you can track hello progress under **Notifications** from hello menu.</span></span>

5. <span data-ttu-id="88f85-251">Hello 帳戶已被刪除後，您可以重新建立它在 hello**執行身分帳戶**屬性刀鋒視窗中的選取 hello 建立選項**Azure 執行身分帳戶**。</span><span class="sxs-lookup"><span data-stu-id="88f85-251">After hello account has been deleted, you can re-create it on hello **Run As Accounts** properties blade by selecting hello create option **Azure Run As Account**.</span></span>

 ![重新建立 hello 自動化執行身分帳戶](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a><span data-ttu-id="88f85-253">設定錯誤</span><span class="sxs-lookup"><span data-stu-id="88f85-253">Misconfiguration</span></span>
<span data-ttu-id="88f85-254">某些組態項目所需的 hello 執行身分或傳統執行身分帳戶 toofunction 正確可能已刪除或在初始安裝期間，建立方式不正確。</span><span class="sxs-lookup"><span data-stu-id="88f85-254">Some configuration items necessary for hello Run As or Classic Run As account toofunction properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="88f85-255">hello 項目包括：</span><span class="sxs-lookup"><span data-stu-id="88f85-255">hello items include:</span></span>

* <span data-ttu-id="88f85-256">憑證資產</span><span class="sxs-lookup"><span data-stu-id="88f85-256">Certificate asset</span></span>
* <span data-ttu-id="88f85-257">連線資產</span><span class="sxs-lookup"><span data-stu-id="88f85-257">Connection asset</span></span>
* <span data-ttu-id="88f85-258">已從 hello 參與者角色移除執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="88f85-258">Run As account has been removed from hello contributor role</span></span>
* <span data-ttu-id="88f85-259">Azure AD 中的服務主體或應用程式</span><span class="sxs-lookup"><span data-stu-id="88f85-259">Service principal or application in Azure AD</span></span>

<span data-ttu-id="88f85-260">在上述的 hello 和設定錯誤的其他執行個體，hello 自動化帳戶會偵測 hello 變更，並顯示狀態為*完整*上 hello**執行身分帳戶**hello 的屬性刀鋒視窗帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-260">In hello preceding and other instances of misconfiguration, hello Automation account detects hello changes and displays a status of *Incomplete* on hello **Run As Accounts** properties blade for hello account.</span></span>

![不完整的執行身分帳戶設定狀態](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="88f85-262">當您選取執行身分帳戶 hello 時，hello 帳戶**屬性** 窗格會顯示下列錯誤訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="88f85-262">When you select hello Run As account, hello account **Properties** pane displays hello following error message:</span></span>

![不完整的執行身分設定警告訊息](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="88f85-264">.</span><span class="sxs-lookup"><span data-stu-id="88f85-264">.</span></span>

<span data-ttu-id="88f85-265">您可以快速解決這些執行身分帳戶的問題，藉由刪除並重新建立 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-265">You can quickly resolve these Run As account issues by deleting and re-creating hello account.</span></span>

## <a name="update-your-automation-account-by-using-powershell"></a><span data-ttu-id="88f85-266">使用 PowerShell 更新自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="88f85-266">Update your Automation account by using PowerShell</span></span>
<span data-ttu-id="88f85-267">如果您可以使用指定 PowerShell tooupdate 您現有的自動化帳戶：</span><span class="sxs-lookup"><span data-stu-id="88f85-267">You can use PowerShell tooupdate your existing Automation account if:</span></span>

* <span data-ttu-id="88f85-268">建立自動化帳戶，但拒絕 toocreate hello 執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-268">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="88f85-269">您已經使用自動化帳戶 toomanage 資源管理員資源，並想 runbook 驗證 tooupdate hello tooinclude hello 執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-269">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="88f85-270">您已經使用自動化帳戶 toomanage 傳統資源，而且您想 tooupdate 它 toouse hello 傳統執行身分帳戶，而不要建立新的帳戶和移轉您的 runbook 與資產 tooit。</span><span class="sxs-lookup"><span data-stu-id="88f85-270">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="88f85-271">您想要 toocreate 執行身分和傳統執行身分帳戶使用企業憑證授權單位 (CA) 所核發的憑證。</span><span class="sxs-lookup"><span data-stu-id="88f85-271">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

<span data-ttu-id="88f85-272">hello 指令碼有 hello 下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="88f85-272">hello script has hello following prerequisites:</span></span>

* <span data-ttu-id="88f85-273">hello 指令碼可以與 2.01 和更新版本的 Azure 資源管理員模組只能在 Windows 10 和 Windows Server 2016 上執行。</span><span class="sxs-lookup"><span data-stu-id="88f85-273">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="88f85-274">不支援在舊版 Windows 上執行。</span><span class="sxs-lookup"><span data-stu-id="88f85-274">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="88f85-275">Azure PowerShell 1.0 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="88f85-275">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="88f85-276">如需 hello PowerShell 1.0 版的資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="88f85-276">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="88f85-277">自動化帳戶被稱為 hello hello 值*– AutomationAccountName*和*-ApplicationDisplayName* hello 下列 PowerShell 指令碼中的參數。</span><span class="sxs-lookup"><span data-stu-id="88f85-277">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="88f85-278">tooget hello 值*SubscriptionID*， *ResourceGroup*，和*AutomationAccountName*、 哪些是 hello 指令碼的必要的參數、 執行 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="88f85-278">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello scripts, do hello following:</span></span>
1. <span data-ttu-id="88f85-279">在 hello Azure 入口網站中選取您的自動化帳戶上 hello**自動化帳戶**刀鋒視窗中，然後再選取**所有設定**。</span><span class="sxs-lookup"><span data-stu-id="88f85-279">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="88f85-280">在 hello**所有設定**刀鋒視窗底下**帳戶設定**，選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="88f85-280">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="88f85-281">請注意在 hello hello 值**屬性**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="88f85-281">Note hello values on hello **Properties** blade.</span></span>

![hello 自動化帳戶 [屬性] 刀鋒視窗](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a><span data-ttu-id="88f85-283">建立執行身分帳戶 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="88f85-283">Create a Run As account PowerShell script</span></span>
<span data-ttu-id="88f85-284">這個 PowerShell 指令碼包含支援的設定 hello:</span><span class="sxs-lookup"><span data-stu-id="88f85-284">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="88f85-285">使用自我簽署憑證建立執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-285">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="88f85-286">使用自我簽署憑證建立執行身分帳戶和傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-286">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="88f85-287">使用企業憑證建立執行身分帳戶和傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-287">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="88f85-288">建立執行身分帳戶和傳統執行身分帳戶 hello Azure 政府雲端中使用自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="88f85-288">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="88f85-289">視您選取的 hello 組態選項，hello 指令碼會建立 hello 下列項目。</span><span class="sxs-lookup"><span data-stu-id="88f85-289">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="88f85-290">**若為執行身分帳戶︰**</span><span class="sxs-lookup"><span data-stu-id="88f85-290">**For Run As accounts:**</span></span>

* <span data-ttu-id="88f85-291">建立 Azure AD 應用程式 toobe 匯出以自我簽署的任一個 hello 或企業憑證的公開金鑰，在 Azure AD 中建立 hello 應用程式的服務主體帳戶，並指派 hello hello 帳戶在您目前的參與者角色訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-291">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="88f85-292">您可以變更此設定 tooOwner 或任何其他角色。</span><span class="sxs-lookup"><span data-stu-id="88f85-292">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="88f85-293">如需詳細資訊，請參閱 [Azure 自動化中的角色型存取控制](automation-role-based-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="88f85-293">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="88f85-294">建立名為自動化憑證資產*AzureRunAsCertificate* hello 中指定的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-294">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="88f85-295">hello 憑證資產會保存 hello 憑證私密金鑰，可由 hello Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="88f85-295">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="88f85-296">建立名為自動化連線資產*AzureRunAsConnection* hello 中指定的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-296">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="88f85-297">hello 連線資產會保存 hello applicationId、 tenantId、 subscriptionId、 和憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="88f85-297">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="88f85-298">**若為傳統執行身分帳戶：**</span><span class="sxs-lookup"><span data-stu-id="88f85-298">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="88f85-299">建立名為自動化憑證資產*AzureClassicRunAsCertificate* hello 中指定的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-299">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="88f85-300">hello 憑證資產會保存 hello 憑證私密金鑰由 hello 管理憑證。</span><span class="sxs-lookup"><span data-stu-id="88f85-300">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="88f85-301">建立名為自動化連線資產*AzureClassicRunAsConnection* hello 中指定的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="88f85-301">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="88f85-302">hello 連線資產包含 hello 訂用帳戶名稱、 訂用帳戶 Id，與憑證資產名稱。</span><span class="sxs-lookup"><span data-stu-id="88f85-302">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="88f85-303">如果您選取其中一個選項，建立傳統執行身分帳戶，hello 指令碼執行之後上, 傳 hello 公用憑證 （.cer 檔案名稱副檔名） toohello 管理的存放區 hello 訂用帳戶的 hello 自動化帳戶中建立。</span><span class="sxs-lookup"><span data-stu-id="88f85-303">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

<span data-ttu-id="88f85-304">tooexecute hello 指令碼和 hello 憑證上傳，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="88f85-304">tooexecute hello script and upload hello certificate, do hello following:</span></span>

1. <span data-ttu-id="88f85-305">儲存您的電腦上下列指令碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="88f85-305">Save hello following script on your computer.</span></span> <span data-ttu-id="88f85-306">在此範例中，以儲存 hello filename*新增 RunAsAccount.ps1*。</span><span class="sxs-lookup"><span data-stu-id="88f85-306">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

        #Requires -RunAsAdministrator
         Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                      [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
           -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
           -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
           Sleep -s 10
           New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
           $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
           $Retries++;
        }
           return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
          $CertificateName = $AutomationAccountName+$CertifcateAssetName
          $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
          $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
          $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
          CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                    "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload hello .cer format of #CERT#"

             if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
             $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
             $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
             $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
             $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
             $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
             $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
             $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
             $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
             CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="88f85-307">在電腦上按一下 [啟動]，然後以提高的使用者權限啟動 **Windows PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="88f85-307">On your computer, click **Start**, and then start **Windows PowerShell** with elevated user rights.</span></span>

3. <span data-ttu-id="88f85-308">從 hello 提高 PowerShell 命令列殼層移 toohello 資料夾包含您在步驟 1 中建立的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="88f85-308">From hello elevated PowerShell command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>

4. <span data-ttu-id="88f85-309">您需要的 hello 組態使用 hello 參數值執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="88f85-309">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="88f85-310">**使用自我簽署憑證建立執行身分帳戶**</span><span class="sxs-lookup"><span data-stu-id="88f85-310">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="88f85-311">**使用自我簽署憑證建立執行身分帳戶和傳統執行身分帳戶**</span><span class="sxs-lookup"><span data-stu-id="88f85-311">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="88f85-312">**使用企業憑證建立執行身分帳戶和傳統執行身分帳戶**</span><span class="sxs-lookup"><span data-stu-id="88f85-312">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="88f85-313">**使用自我簽署的憑證 hello Azure 政府雲端中建立執行身分帳戶和傳統執行身分帳戶**</span><span class="sxs-lookup"><span data-stu-id="88f85-313">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="88f85-314">Hello 指令碼執行之後，您將會提示的 tooauthenticate 與 Azure。</span><span class="sxs-lookup"><span data-stu-id="88f85-314">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="88f85-315">使用屬於 hello 訂用帳戶系統管理員角色的成員和 hello 訂用帳戶的共同管理員帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="88f85-315">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="88f85-316">Hello 指令碼順利執行之後，請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="88f85-316">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="88f85-317">如果您使用自我簽署的公開憑證 （.cer 檔案） 建立傳統執行身分帳戶，hello 指令碼建立，並將它 hello 使用者設定檔在電腦上儲存 toohello 暫存檔案資料夾*%USERPROFILE%\AppData\Local\Temp*，使用 tooexecute hello PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="88f85-317">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="88f85-318">如果您使用企業公開憑證 (.cer 檔案) 建立了傳統執行身分帳戶，請使用此憑證。</span><span class="sxs-lookup"><span data-stu-id="88f85-318">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="88f85-319">請依照指示 hello[上傳 Azure 傳統入口網站管理 API 憑證 toohello](../azure-api-management-certs.md)，並驗證服務管理資源的 hello 認證組態使用 hello[範例程式碼服務管理資源 tooauthenticate](#sample-code-to-authenticate-with-service-management-resources)。</span><span class="sxs-lookup"><span data-stu-id="88f85-319">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with Service Management resources by using hello [sample code tooauthenticate with Service Management Resources](#sample-code-to-authenticate-with-service-management-resources).</span></span> 
* <span data-ttu-id="88f85-320">如果您未*不*建立傳統執行身分帳戶、 向資源管理員資源及驗證 hello 認證組態使用 hello[範例程式碼來驗證服務管理資源](#sample-code-to-authenticate-with-resource-manager-resources)。</span><span class="sxs-lookup"><span data-stu-id="88f85-320">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](#sample-code-to-authenticate-with-resource-manager-resources).</span></span>

## <a name="sample-code-tooauthenticate-with-resource-manager-resources"></a><span data-ttu-id="88f85-321">使用資源管理員資源的範例程式碼 tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="88f85-321">Sample code tooauthenticate with Resource Manager resources</span></span>
<span data-ttu-id="88f85-322">您可以使用更新的 hello 下列範例程式碼取自 hello *AzureAutomationTutorialScript*範例 runbook、 tooauthenticate 透過 hello 執行身分帳戶 toomanage 資源管理員資源與您的 runbook。</span><span class="sxs-lookup"><span data-stu-id="88f85-322">You can use hello following updated sample code, taken from hello *AzureAutomationTutorialScript* example runbook, tooauthenticate by using hello Run As account toomanage Resource Manager resources with your runbooks.</span></span>

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get hello connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in tooAzure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context tooa specific subscription"     
       Set-AzureRmContext -SubscriptionId $SubId              
    }
    catch {
        if (!$servicePrincipalConnection)
        {
           $ErrorMessage = "Connection $connectionName not found."
           throw $ErrorMessage
         } else{
            Write-Error -Message $_.Exception
            throw $_.Exception
         }
    }

<span data-ttu-id="88f85-323">您 tooeasily 處理多個訂用帳戶之間的 toohelp，hello 指令碼包含兩個額外的程式碼行支援參考在訂用帳戶的內容。</span><span class="sxs-lookup"><span data-stu-id="88f85-323">toohelp you tooeasily work between multiple subscriptions, hello script includes two additional lines of code that support referencing a subscription context.</span></span> <span data-ttu-id="88f85-324">名為變數資產*SubscriptionId*包含 hello hello 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="88f85-324">A variable asset named *SubscriptionId* contains hello ID of hello subscription.</span></span> <span data-ttu-id="88f85-325">之後 hello `Add-AzureRmAccount` cmdlet 陳述式，hello [ `Set-AzureRmContext` ](/powershell/module/azurerm.profile/set-azurermcontext)指令程式會與 hello 參數集陳述*-SubscriptionId*。</span><span class="sxs-lookup"><span data-stu-id="88f85-325">After hello `Add-AzureRmAccount` cmdlet statement, hello [`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet is stated with hello parameter set *-SubscriptionId*.</span></span> <span data-ttu-id="88f85-326">如果太泛型 hello 變數名稱，您可以修改它 tooinclude 前置詞，或使用另一個命名慣例 toomake 它更容易 tooidentify。</span><span class="sxs-lookup"><span data-stu-id="88f85-326">If hello variable name is too generic, you can revise it tooinclude a prefix or use another naming convention toomake it easier tooidentify.</span></span> <span data-ttu-id="88f85-327">或者，您可以使用 hello 參數集*-訂用帳戶名稱*而不是*-SubscriptionId*與對應的變數資產。</span><span class="sxs-lookup"><span data-stu-id="88f85-327">Alternatively, you can use hello parameter set *-SubscriptionName* instead of *-SubscriptionId* with a corresponding variable asset.</span></span>

<span data-ttu-id="88f85-328">hello 您用來驗證 hello runbook 中的 cmdlet `Add-AzureRmAccount`，使用 hello *ServicePrincipalCertificate*參數集。</span><span class="sxs-lookup"><span data-stu-id="88f85-328">hello cmdlet that you use for authenticating in hello runbook, `Add-AzureRmAccount`, uses hello *ServicePrincipalCertificate* parameter set.</span></span> <span data-ttu-id="88f85-329">它會使用 hello 服務主體認證，hello 使用者認證來驗證。</span><span class="sxs-lookup"><span data-stu-id="88f85-329">It authenticates by using hello service principal certificate, not hello user credentials.</span></span>

## <a name="sample-code-tooauthenticate-with-service-management-resources"></a><span data-ttu-id="88f85-330">範例程式碼 tooauthenticate 與服務管理資源</span><span class="sxs-lookup"><span data-stu-id="88f85-330">Sample code tooauthenticate with Service Management resources</span></span>
<span data-ttu-id="88f85-331">您可以使用下列更新的範例程式碼，取自 hello hello *AzureClassicAutomationTutorialScript*範例 runbook，使用傳統執行身分帳戶 toomanage，傳統資源與 hello tooauthenticate 您runbook。</span><span class="sxs-lookup"><span data-stu-id="88f85-331">You can use hello following updated sample code, which is taken from hello *AzureClassicAutomationTutorialScript* example runbook, tooauthenticate by using hello Classic Run As account toomanage classic resources with your runbooks.</span></span>

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a><span data-ttu-id="88f85-332">後續步驟</span><span class="sxs-lookup"><span data-stu-id="88f85-332">Next steps</span></span>
* [<span data-ttu-id="88f85-333">Azure AD 中的應用程式和服務主體物件</span><span class="sxs-lookup"><span data-stu-id="88f85-333">Application and service principal objects in Azure AD</span></span>](../active-directory/active-directory-application-objects.md)
* [<span data-ttu-id="88f85-334">Azure 自動化中的角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="88f85-334">Role-based access control in Azure Automation</span></span>](automation-role-based-access-control.md)
* [<span data-ttu-id="88f85-335">Azure 雲端服務的憑證概觀</span><span class="sxs-lookup"><span data-stu-id="88f85-335">Certificates overview for Azure Cloud Services</span></span>](../cloud-services/cloud-services-certs-create.md)
