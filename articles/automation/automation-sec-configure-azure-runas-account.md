---
title: "設定 Azure 執行身分帳戶 | Microsoft Docs"
description: "本教學課程會逐步引導您在 Azure 自動化中建立、測試和舉例使用安全性主體驗證。"
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
redirect_document_id: TRUE
ms.openlocfilehash: f88c775eba19bb227d0e206d6420c08b57305b92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a><span data-ttu-id="ceacc-104">使用 Azure 執行身分帳戶驗證 Runbook</span><span class="sxs-lookup"><span data-stu-id="ceacc-104">Authenticate runbooks with an Azure Run As account</span></span>
<span data-ttu-id="ceacc-105">本文說明如何在 Azure 入口網站中設定 Azure 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-105">This article shows you how to configure an Azure Automation account in the Azure portal.</span></span> <span data-ttu-id="ceacc-106">若要進行此作業，請使用執行身分帳戶功能來驗證在 Azure Resource Manager 或 Azure 服務管理中管理資源的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="ceacc-106">To do so, you use the Run As account feature to authenticate runbooks managing resources in either Azure Resource Manager or Azure Service Management.</span></span>

<span data-ttu-id="ceacc-107">當您在 Azure 入口網站中建立自動化帳戶時，您會自動建立兩個帳戶：</span><span class="sxs-lookup"><span data-stu-id="ceacc-107">When you create an Automation account in the Azure portal, you automatically create two accounts:</span></span>

* <span data-ttu-id="ceacc-108">執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-108">A Run As account.</span></span> <span data-ttu-id="ceacc-109">此帳戶會在 Azure Active Directory (Azure AD) 中建立服務主體，並建立一個憑證。</span><span class="sxs-lookup"><span data-stu-id="ceacc-109">This account creates a service principal in Azure Active Directory (Azure AD) and a certificate.</span></span> <span data-ttu-id="ceacc-110">此外，也會指定參與者角色型存取控制 (RBAC)，此控制可使用 Runbook 來管理 Resource Manager 資源。</span><span class="sxs-lookup"><span data-stu-id="ceacc-110">It also assigns the Contributor role-based access control (RBAC), which manages Resource Manager resources by using runbooks.</span></span>
* <span data-ttu-id="ceacc-111">傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-111">A Classic Run As account.</span></span> <span data-ttu-id="ceacc-112">此帳戶會上傳管理憑證，利用此憑證就能使用 Runbook 來管理服務管理或傳統資源。</span><span class="sxs-lookup"><span data-stu-id="ceacc-112">This account uploads a management certificate, which is used to manage Service Management or classic resources by using runbooks.</span></span>

<span data-ttu-id="ceacc-113">建立自動化帳戶可為您簡化程序，協助您快速開始建置和部署 Runbook 以支援您的自動化需求。</span><span class="sxs-lookup"><span data-stu-id="ceacc-113">Creating an Automation account simplifies the process for you and helps you quickly start building and deploying runbooks to support your automation needs.</span></span>

<span data-ttu-id="ceacc-114">使用執行身分和傳統執行身分帳戶，您可以︰</span><span class="sxs-lookup"><span data-stu-id="ceacc-114">With Run As and Classic Run As accounts, you can:</span></span>

* <span data-ttu-id="ceacc-115">當您在 Azure 入口網站中透過 Runbook 管理 Resource Manager 或服務管理資源時，提供標準化的 Azure 驗證方式。</span><span class="sxs-lookup"><span data-stu-id="ceacc-115">Provide a standardized way to authenticate with Azure when you manage Resource Manager or Service Management resources from runbooks in the Azure portal.</span></span>
* <span data-ttu-id="ceacc-116">自動使用可在 Azure 警示中設定的全域 Runbook。</span><span class="sxs-lookup"><span data-stu-id="ceacc-116">Automate the use of global runbooks, which you can configure in Azure Alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="ceacc-117">若要搭配自動化全域 Runbook 使用 [Azure 警示整合功能](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)，您需要具備使用執行身分帳戶和傳統執行身分帳戶所設定的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-117">The [Azure Alert integration feature](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) with Automation global runbooks requires an Automation account that's configured with a Run As account and a Classic Run As account.</span></span> <span data-ttu-id="ceacc-118">您可以選取已定義執行身分和傳統執行身分帳戶的自動化帳戶，或是選擇建立新的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-118">You can select an Automation account that already has defined Run As and Classic Run As accounts, or you can choose to create a new Automation account.</span></span>
>  

<span data-ttu-id="ceacc-119">本文示範如何從 Azure 入口網站建立自動化帳戶、如何使用 Azure PowerShell 更新自動化帳戶、如何管理帳戶組態，以及如何在 Runbook 中進行驗證。</span><span class="sxs-lookup"><span data-stu-id="ceacc-119">This article shows how to create an Automation account from the Azure portal, update an Automation account by using Azure PowerShell, manage the account configuration, and authenticate in your runbooks.</span></span>

<span data-ttu-id="ceacc-120">在開始建立自動化帳戶之前，您最好先了解並考慮下列事項︰</span><span class="sxs-lookup"><span data-stu-id="ceacc-120">Before you begin creating an Automation account, it's a good idea to understand and consider the following:</span></span>

* <span data-ttu-id="ceacc-121">建立自動化帳戶並不會影響您可能已在傳統或 Resource Manager 部署模型中建立的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-121">Creating an Automation account does not affect Automation accounts you might have already created in either the classic or Resource Manager deployment model.</span></span>
* <span data-ttu-id="ceacc-122">此程序只適用於在 Azure 入口網站中建立的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-122">The process works only for Automation accounts that you create in the Azure portal.</span></span> <span data-ttu-id="ceacc-123">嘗試從 Azure 傳統入口網站建立帳戶，並不會複寫執行身分帳戶組態。</span><span class="sxs-lookup"><span data-stu-id="ceacc-123">Attempting to create an account from the Azure classic portal does not replicate the Run As account configuration.</span></span>
* <span data-ttu-id="ceacc-124">如果您已備有 Runbook 與資產 (例如排程或變數) 來管理傳統資源，且想要讓 Runbook 使用新的傳統執行身分帳戶進行驗證，請執行下列任一操作︰</span><span class="sxs-lookup"><span data-stu-id="ceacc-124">If you already have runbooks and assets (such as schedules or variables) in place to manage classic resources, and you want runbooks to authenticate with the new Classic Run As account, do either of the following:</span></span>

  * <span data-ttu-id="ceacc-125">若要建立傳統執行身分帳戶，請遵循＜管理執行身分帳戶＞一節中的指示。</span><span class="sxs-lookup"><span data-stu-id="ceacc-125">To create a Classic Run As account, follow the instructions in the "Managing your Run As account" section.</span></span> 
  * <span data-ttu-id="ceacc-126">若要更新現有帳戶，請使用＜使用 PowerShell 更新自動化帳戶＞一節中的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="ceacc-126">To update your existing account, use the PowerShell script in the "Update your Automation account by using PowerShell" section.</span></span>
* <span data-ttu-id="ceacc-127">若要使用新的執行身分帳戶和傳統執行身分自動化帳戶進行驗證，您必須以[自動化程式碼範例](#authentication-code-examples)一節中提供的範例程式碼修改現有的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="ceacc-127">To authenticate by using the new Run As account and Classic Run As Automation account, you  need to modify your existing runbooks with the example code provided in the section [Authentication code examples](#authentication-code-examples).</span></span>

    >[!NOTE]
    ><span data-ttu-id="ceacc-128">執行身分帳戶適用於使用以憑證為基礎的服務主體對 Resource Manager 資源進行驗證。</span><span class="sxs-lookup"><span data-stu-id="ceacc-128">The Run As account is for authentication against Resource Manager resources using the certificate-based service principal.</span></span> <span data-ttu-id="ceacc-129">傳統執行身分帳戶適用於使用管理憑證對服務管理資源進行驗證。</span><span class="sxs-lookup"><span data-stu-id="ceacc-129">The Classic Run As account is for authenticating against Service Management resources with a management certificate.</span></span>

## <a name="create-an-automation-account-from-the-azure-portal"></a><span data-ttu-id="ceacc-130">從 Azure 入口網站建立自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="ceacc-130">Create an Automation account from the Azure portal</span></span>
<span data-ttu-id="ceacc-131">在這一節中，您會從 Azure 入口網站建立 Azure 自動化帳戶，接著再建立執行身分帳戶和傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-131">In this section, you create an Azure Automation account from the Azure portal, which in turn creates both a Run As account and a Classic Run As account.</span></span>

>[!NOTE]
><span data-ttu-id="ceacc-132">若要建立自動化帳戶，您必須是服務管理員角色的成員，或是獲得訂用帳戶存取權的訂用帳戶共同管理員。</span><span class="sxs-lookup"><span data-stu-id="ceacc-132">To create an Automation account, you must be a member of the Service Admins role or co-administrator of the subscription that is granting access to the subscription.</span></span> <span data-ttu-id="ceacc-133">您必須已新增成為該訂用帳戶之預設 Active Directory 執行個體的使用者。</span><span class="sxs-lookup"><span data-stu-id="ceacc-133">You must also be added as a user to that subscription's default Active Directory instance.</span></span> <span data-ttu-id="ceacc-134">此帳戶不需要獲派特殊權限角色。</span><span class="sxs-lookup"><span data-stu-id="ceacc-134">The account does not need to be assigned a privileged role.</span></span>
>
><span data-ttu-id="ceacc-135">若您在新增至訂用帳戶的共同管理員角色之前，並非訂用帳戶之 Active Directory 執行個體的成員，您在新增至 Active Directory 時會成為來賓身分。</span><span class="sxs-lookup"><span data-stu-id="ceacc-135">If you are not a member of the subscription’s Active Directory instance before you are added to the co-administrator role of the subscription, you will be added to Active Directory as a guest.</span></span> <span data-ttu-id="ceacc-136">在此情況下，您會在 [新增自動化帳戶] 刀鋒視窗上看到</span><span class="sxs-lookup"><span data-stu-id="ceacc-136">In this instance, you will receive a “You do not have permissions to create…”</span></span> <span data-ttu-id="ceacc-137">「您沒有權限建立...」的警告。</span><span class="sxs-lookup"><span data-stu-id="ceacc-137">warning on the **Add Automation Account** blade.</span></span>
>
><span data-ttu-id="ceacc-138">新增至共同管理員角色的使用者可以先從訂用帳戶的 Active Directory 執行個體中移除並重新新增，使其成為 Active Directory 中的完整使用者。</span><span class="sxs-lookup"><span data-stu-id="ceacc-138">Users who were added to the co-administrator role first can be removed from the subscription's Active Directory instance and re-added to make them a full User in Active Directory.</span></span> <span data-ttu-id="ceacc-139">若要確認這種情況，請從 Azure 入口網站的 [Azure Active Directory] 窗格，選取 [使用者和群組]、選取 [所有使用者]，然後在選取特定使用者之後選取 [設定檔]。</span><span class="sxs-lookup"><span data-stu-id="ceacc-139">To verify this situation from the **Azure Active Directory** pane in the Azure portal by selecting **Users and groups**, selecting **All users** and, after you select the specific user, selecting **Profile**.</span></span> <span data-ttu-id="ceacc-140">使用者設定檔之下 [使用者類型] 屬性的值不得等於 [來賓]。</span><span class="sxs-lookup"><span data-stu-id="ceacc-140">The value of the **User type** attribute under the users profile should not equal **Guest**.</span></span>
>

1. <span data-ttu-id="ceacc-141">以訂用帳戶管理員角色成員和訂用帳戶共同管理員的帳戶登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="ceacc-141">Sign in to the Azure portal with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>

2. <span data-ttu-id="ceacc-142">選取 [自動化帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="ceacc-142">Select **Automation Accounts**.</span></span>

3. <span data-ttu-id="ceacc-143">在 [自動化帳戶] 刀鋒視窗上，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ceacc-143">On the **Automation Accounts** blade, click **Add**.</span></span>
<span data-ttu-id="ceacc-144">[新增自動化帳戶] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="ceacc-144">The **Add Automation Account** blade opens.</span></span>

 ![[新增自動化帳戶] 刀鋒視窗](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > <span data-ttu-id="ceacc-146">如果您的帳戶不是訂用帳戶管理員角色的成員和訂用帳戶的共同管理員，則 [新增自動化帳戶] 刀鋒視窗上會顯示下列警告：</span><span class="sxs-lookup"><span data-stu-id="ceacc-146">If your account is not a member of the subscription administrators role and co-administrator of the subscription, the following warning is displayed on the **Add Automation Account** blade:</span></span>
   >
   >![加入自動化帳戶警告](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. <span data-ttu-id="ceacc-148">在 [新增自動化帳戶] 刀鋒視窗的 [名稱] 方塊中，輸入新的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="ceacc-148">On the **Add Automation Account** blade, in the **Name** box, type a name for your new Automation account.</span></span>

5. <span data-ttu-id="ceacc-149">如果您有多個訂用帳戶，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="ceacc-149">If you have more than one subscription, do the following:</span></span>

    <span data-ttu-id="ceacc-150">a.</span><span class="sxs-lookup"><span data-stu-id="ceacc-150">a.</span></span> <span data-ttu-id="ceacc-151">在 [訂用帳戶] 底下，為新帳戶指定一個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-151">Under **Subscription**, specify one for the new account.</span></span>

    <span data-ttu-id="ceacc-152">b.</span><span class="sxs-lookup"><span data-stu-id="ceacc-152">b.</span></span> <span data-ttu-id="ceacc-153">在 [資源群組] 底下，按一下 [建立新的] 或 [使用現有的]。</span><span class="sxs-lookup"><span data-stu-id="ceacc-153">Under **Resource Group**, click **Create new** or **Use existing**.</span></span>

    <span data-ttu-id="ceacc-154">c.</span><span class="sxs-lookup"><span data-stu-id="ceacc-154">c.</span></span> <span data-ttu-id="ceacc-155">在 [位置] 底下，指定 Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="ceacc-155">Under **Location**, specify an Azure datacenter.</span></span>

6. <span data-ttu-id="ceacc-156">在 [建立 Azure 執行身分帳戶] 底下選取 [是]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="ceacc-156">Under **Create Azure Run As account**, select **Yes**, and then click **Create**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ceacc-157">如果您選取 [否] 以選擇不要建立執行身分帳戶，則 [新增自動化帳戶] 刀鋒視窗中會顯示一則警告訊息。</span><span class="sxs-lookup"><span data-stu-id="ceacc-157">If you choose not to create the Run As account by selecting **No**, a warning message is displayed the **Add Automation Account** blade.</span></span> <span data-ttu-id="ceacc-158">雖然此帳戶已在 Azure 入口網站中建立，但在傳統或 Resource Manager 訂用帳戶目錄服務內並沒有對應的驗證身分識別。</span><span class="sxs-lookup"><span data-stu-id="ceacc-158">Although the account is created in the Azure portal, it does not have a corresponding authentication identity within your classic or Resource Manager subscription directory service.</span></span> <span data-ttu-id="ceacc-159">因此，這個帳戶無法存取訂用帳戶中的資源。</span><span class="sxs-lookup"><span data-stu-id="ceacc-159">Consequently, the account has no access to resources in your subscription.</span></span> <span data-ttu-id="ceacc-160">此情況會導致參考此帳戶的任何 Runbook 無法進行驗證，也無法對這些部署模型中的資源執行工作。</span><span class="sxs-lookup"><span data-stu-id="ceacc-160">This scenario prevents any runbooks that reference this account from authenticating and performing tasks against resources in those deployment models.</span></span>
   >
   > ![[新增自動化帳戶] 刀鋒視窗上的警告訊息](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > <span data-ttu-id="ceacc-162">此外，因為服務主體並未建立，因此系統不會指派參與者角色。</span><span class="sxs-lookup"><span data-stu-id="ceacc-162">Additionally, because the service principal is not created, the Contributor role is not assigned.</span></span>
   >

7. <span data-ttu-id="ceacc-163">在 Azure 建立自動化帳戶時，您可以在功能表的 [通知]  底下追蹤進度。</span><span class="sxs-lookup"><span data-stu-id="ceacc-163">While Azure creates the Automation account, you can track the progress under **Notifications** from the menu.</span></span>

### <a name="resources"></a><span data-ttu-id="ceacc-164">資源</span><span class="sxs-lookup"><span data-stu-id="ceacc-164">Resources</span></span>
<span data-ttu-id="ceacc-165">順利建立自動化帳戶時，系統會自動為您建立幾項資源。</span><span class="sxs-lookup"><span data-stu-id="ceacc-165">When the Automation account is successfully created, several resources are automatically created for you.</span></span> <span data-ttu-id="ceacc-166">下面兩個資料表會摘要說明這些資源：</span><span class="sxs-lookup"><span data-stu-id="ceacc-166">The resources are summarized in the following two tables:</span></span>

#### <a name="run-as-account-resources"></a><span data-ttu-id="ceacc-167">執行身分帳戶資源</span><span class="sxs-lookup"><span data-stu-id="ceacc-167">Run As account resources</span></span>

| <span data-ttu-id="ceacc-168">資源</span><span class="sxs-lookup"><span data-stu-id="ceacc-168">Resource</span></span> | <span data-ttu-id="ceacc-169">說明</span><span class="sxs-lookup"><span data-stu-id="ceacc-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ceacc-170">AzureAutomationTutorial Runbook</span><span class="sxs-lookup"><span data-stu-id="ceacc-170">AzureAutomationTutorial Runbook</span></span> | <span data-ttu-id="ceacc-171">此為圖形化 Runbook 範例，示範如何使用執行身分帳戶進行驗證以及取得所有 Resource Manager 資源。</span><span class="sxs-lookup"><span data-stu-id="ceacc-171">An example graphical runbook that demonstrates how to authenticate by using the Run As account and gets all the Resource Manager resources.</span></span> |
| <span data-ttu-id="ceacc-172">AzureAutomationTutorialScript Runbook</span><span class="sxs-lookup"><span data-stu-id="ceacc-172">AzureAutomationTutorialScript Runbook</span></span> | <span data-ttu-id="ceacc-173">此為 PowerShell Runbook 範例，示範如何使用執行身分帳戶進行驗證以及取得 Resource Manager 資源。</span><span class="sxs-lookup"><span data-stu-id="ceacc-173">An example PowerShell runbook that demonstrates how to authenticate by using the Run As account and gets all the Resource Manager resources.</span></span> |
| <span data-ttu-id="ceacc-174">AzureRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="ceacc-174">AzureRunAsCertificate</span></span> | <span data-ttu-id="ceacc-175">在建立自動化帳戶時自動建立，或使用下列適用於現有帳戶的 PowerShell 指令碼建立的憑證資產。</span><span class="sxs-lookup"><span data-stu-id="ceacc-175">The certificate asset that's automatically created when you create an Automation account or use the following PowerShell script for an existing account.</span></span> <span data-ttu-id="ceacc-176">此憑證可讓您向 Azure 進行驗證，以便從 Runbook 管理 Azure Resource Manager 資源。</span><span class="sxs-lookup"><span data-stu-id="ceacc-176">The certificate allows you to authenticate with Azure so that you can manage Azure Resource Manager resources from runbooks.</span></span> <span data-ttu-id="ceacc-177">此憑證有一年的有效期。</span><span class="sxs-lookup"><span data-stu-id="ceacc-177">The certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="ceacc-178">AzureRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="ceacc-178">AzureRunAsConnection</span></span> | <span data-ttu-id="ceacc-179">在建立自動化帳戶時自動建立，或使用適用於現有帳戶的 PowerShell 指令碼建立的連線資產。</span><span class="sxs-lookup"><span data-stu-id="ceacc-179">The connection asset that's automatically created when you create an Automation account or use the PowerShell script for an existing account.</span></span> |

#### <a name="classic-run-as-account-resources"></a><span data-ttu-id="ceacc-180">傳統執行身分帳戶資源</span><span class="sxs-lookup"><span data-stu-id="ceacc-180">Classic Run As account resources</span></span>

| <span data-ttu-id="ceacc-181">資源</span><span class="sxs-lookup"><span data-stu-id="ceacc-181">Resource</span></span> | <span data-ttu-id="ceacc-182">說明</span><span class="sxs-lookup"><span data-stu-id="ceacc-182">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ceacc-183">AzureClassicAutomationTutorial Runbook</span><span class="sxs-lookup"><span data-stu-id="ceacc-183">AzureClassicAutomationTutorial Runbook</span></span> | <span data-ttu-id="ceacc-184">此為圖形化 Runbook 範例，可使用傳統執行身分帳戶 (憑證) 來取得訂用帳戶中使用傳統部署模型所建立的所有 VM，然後寫入 VM 名稱和狀態。</span><span class="sxs-lookup"><span data-stu-id="ceacc-184">An example graphical runbook that gets all the VMs that are created using the classic deployment model in a subscription by using the Classic Run As account (certificate), and then writes the VM name and status.</span></span> |
| <span data-ttu-id="ceacc-185">AzureClassicAutomationTutorial 指令碼 Runbook</span><span class="sxs-lookup"><span data-stu-id="ceacc-185">AzureClassicAutomationTutorial Script Runbook</span></span> | <span data-ttu-id="ceacc-186">此為 PowerShell Runbook 範例，可使用傳統執行身分帳戶 (憑證) 來取得訂用帳戶中的所有傳統 VM，然後寫入 VM 名稱和狀態。</span><span class="sxs-lookup"><span data-stu-id="ceacc-186">An example PowerShell runbook that gets all the classic VMs in a subscription by using the Classic Run As account (certificate), and then writes the VM name and status.</span></span> |
| <span data-ttu-id="ceacc-187">AzureClassicRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="ceacc-187">AzureClassicRunAsCertificate</span></span> | <span data-ttu-id="ceacc-188">自動建立的憑證資產，可供您向 Azure 進行驗證，以便從 Runbook 管理 Azure 傳統資源。</span><span class="sxs-lookup"><span data-stu-id="ceacc-188">The automatically created certificate asset that you use to authenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> <span data-ttu-id="ceacc-189">此憑證有一年的有效期。</span><span class="sxs-lookup"><span data-stu-id="ceacc-189">The certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="ceacc-190">AzureClassicRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="ceacc-190">AzureClassicRunAsConnection</span></span> | <span data-ttu-id="ceacc-191">自動建立的連線資產，可供您向 Azure 進行驗證，以便從 Runbook 管理 Azure 傳統資源。</span><span class="sxs-lookup"><span data-stu-id="ceacc-191">The automatically created connection asset that you use to authenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> |

## <a name="verify-run-as-authentication"></a><span data-ttu-id="ceacc-192">確認執行身分驗證</span><span class="sxs-lookup"><span data-stu-id="ceacc-192">Verify Run As authentication</span></span>
<span data-ttu-id="ceacc-193">執行一項小測試，以確認您可以使用新的執行身分帳戶成功進行驗證。</span><span class="sxs-lookup"><span data-stu-id="ceacc-193">Perform a small test to confirm that you can successfully authenticate by using the new Run As account.</span></span>

1. <span data-ttu-id="ceacc-194">在 Azure 入口網站中，開啟先前建立的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-194">In the Azure portal, open the Automation account that you created earlier.</span></span>

2. <span data-ttu-id="ceacc-195">按一下 [Runbook]  磚以開啟 Runbook 的清單。</span><span class="sxs-lookup"><span data-stu-id="ceacc-195">Click the **Runbooks** tile to open the list of runbooks.</span></span>

3. <span data-ttu-id="ceacc-196">選取 **AzureAutomationTutorialScript** Runbook，然後按一下 [啟動] 來啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="ceacc-196">Select the **AzureAutomationTutorialScript** runbook, and then click **Start** to start the runbook.</span></span> <span data-ttu-id="ceacc-197">隨即會發生下列事件︰</span><span class="sxs-lookup"><span data-stu-id="ceacc-197">The following events occur:</span></span>
 * <span data-ttu-id="ceacc-198">建立 [Runbook 作業](automation-runbook-execution.md)、顯示 [作業] 刀鋒視窗，而作業狀態會顯示在 [作業摘要] 圖格中。</span><span class="sxs-lookup"><span data-stu-id="ceacc-198">A [runbook job](automation-runbook-execution.md) is created, the **Job** blade is displayed, and the job status is displayed in the **Job Summary** tile.</span></span>
 * <span data-ttu-id="ceacc-199">作業狀態一開始會顯示為 [已排入佇列] ，表示其正在等候雲端中的 Runbook 背景工作變為可用狀態。</span><span class="sxs-lookup"><span data-stu-id="ceacc-199">The job status begins as **Queued**, indicating that it is waiting for a runbook worker in the cloud to become available.</span></span>
 * <span data-ttu-id="ceacc-200">當背景工作宣告該作業時，狀態會變成 [開始]。</span><span class="sxs-lookup"><span data-stu-id="ceacc-200">The status becomes **Starting** when a worker claims the job.</span></span>
 * <span data-ttu-id="ceacc-201">當 Runbook 開始執行時，狀態會變成 [執行中]。</span><span class="sxs-lookup"><span data-stu-id="ceacc-201">The status becomes **Running** when the runbook starts running.</span></span>
 * <span data-ttu-id="ceacc-202">當 Runbook 作業執行完成時，您應該會看到 [完成] 狀態。</span><span class="sxs-lookup"><span data-stu-id="ceacc-202">When the runbook job has finished running, you should see a status of **Completed**.</span></span>

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. <span data-ttu-id="ceacc-203">若要查看 Runbook 的詳細結果，請按一下 [輸出] 圖格。</span><span class="sxs-lookup"><span data-stu-id="ceacc-203">To see the detailed results of the runbook, click the **Output** tile.</span></span>  
<span data-ttu-id="ceacc-204">隨即會顯示 [輸出] 刀鋒視窗，其中顯示 Runbook 已驗證成功並傳回資源群組中的所有可用資源清單。</span><span class="sxs-lookup"><span data-stu-id="ceacc-204">The **Output** blade is displayed, showing that the runbook has successfully authenticated and returned a list of all resources available in the resource group.</span></span>

5. <span data-ttu-id="ceacc-205">關閉 [輸出] 刀鋒視窗以返回 [作業摘要] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ceacc-205">Close the **Output** blade to return to the **Job Summary** blade.</span></span>

6. <span data-ttu-id="ceacc-206">關閉 [作業摘要] 刀鋒視窗和對應的 **AzureAutomationTutorialScript** Runbook 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ceacc-206">Close the **Job Summary** blade and the corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="verify-classic-run-as-authentication"></a><span data-ttu-id="ceacc-207">確認傳統執行身分驗證</span><span class="sxs-lookup"><span data-stu-id="ceacc-207">Verify Classic Run As authentication</span></span>
<span data-ttu-id="ceacc-208">執行一項類似的小測試，以確認您可以使用新的傳統執行身分帳戶成功進行驗證。</span><span class="sxs-lookup"><span data-stu-id="ceacc-208">Perform a similar small test to confirm that you can successfully authenticate by using the new Classic Run As account.</span></span>

1. <span data-ttu-id="ceacc-209">在 Azure 入口網站中，開啟先前建立的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-209">In the Azure portal, open the Automation account that you created earlier.</span></span>

2. <span data-ttu-id="ceacc-210">按一下 [Runbook]  磚以開啟 Runbook 的清單。</span><span class="sxs-lookup"><span data-stu-id="ceacc-210">Click the **Runbooks** tile to open the list of runbooks.</span></span>

3. <span data-ttu-id="ceacc-211">選取 **AzureClassicAutomationTutorialScript** Runbook，然後按一下 [啟動] 來啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="ceacc-211">Select the **AzureClassicAutomationTutorialScript** runbook, and then click **Start** to  start the runbook.</span></span> <span data-ttu-id="ceacc-212">隨即會發生下列事件︰</span><span class="sxs-lookup"><span data-stu-id="ceacc-212">The following events occur:</span></span>

 * <span data-ttu-id="ceacc-213">建立 [Runbook 作業](automation-runbook-execution.md)、顯示 [作業] 刀鋒視窗，而作業狀態會顯示在 [作業摘要] 圖格中。</span><span class="sxs-lookup"><span data-stu-id="ceacc-213">A [runbook job](automation-runbook-execution.md) is created, the **Job** blade is displayed, and the job status is displayed in the **Job Summary** tile.</span></span>
 * <span data-ttu-id="ceacc-214">作業狀態一開始會顯示為 [已排入佇列] ，表示其正在等候雲端中的 Runbook 背景工作變為可用狀態。</span><span class="sxs-lookup"><span data-stu-id="ceacc-214">The job status begins as **Queued**, indicating that it is waiting for a runbook worker in the cloud to become available.</span></span>
 * <span data-ttu-id="ceacc-215">當背景工作宣告該作業時，狀態會變成 [開始]。</span><span class="sxs-lookup"><span data-stu-id="ceacc-215">The status becomes **Starting** when a worker claims the job.</span></span>
 * <span data-ttu-id="ceacc-216">當 Runbook 開始執行時，狀態會變成 [執行中]。</span><span class="sxs-lookup"><span data-stu-id="ceacc-216">The status becomes **Running** when the runbook starts running.</span></span>
 * <span data-ttu-id="ceacc-217">當 Runbook 作業執行完成時，您應該會看到 [完成] 狀態。</span><span class="sxs-lookup"><span data-stu-id="ceacc-217">When the runbook job has finished running, you should see a status of **Completed**.</span></span>

    ![安全性主體 Runbook 測試](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. <span data-ttu-id="ceacc-219">若要查看 Runbook 的詳細結果，請按一下 [輸出] 圖格。</span><span class="sxs-lookup"><span data-stu-id="ceacc-219">To see the detailed results of the runbook, click the **Output** tile.</span></span>  
<span data-ttu-id="ceacc-220">隨即會顯示 [輸出] 刀鋒視窗，其中顯示 Runbook 已驗證成功並傳回訂用帳戶中的所有傳統 VM 清單。</span><span class="sxs-lookup"><span data-stu-id="ceacc-220">The **Output** blade is displayed, showing that the runbook has successfully authenticated and returned a list of all classic VMs in the subscription.</span></span>

5. <span data-ttu-id="ceacc-221">關閉 [輸出] 刀鋒視窗以返回 [作業摘要] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ceacc-221">Close the **Output** blade to return to the **Job Summary** blade.</span></span>

6. <span data-ttu-id="ceacc-222">關閉 [作業摘要] 刀鋒視窗和對應的 **AzureAutomationTutorialScript** Runbook 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ceacc-222">Close the **Job Summary** blade and the corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="managing-your-run-as-account"></a><span data-ttu-id="ceacc-223">管理執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="ceacc-223">Managing your Run As account</span></span>
<span data-ttu-id="ceacc-224">有時您必須在自動化帳戶到期前更新憑證。</span><span class="sxs-lookup"><span data-stu-id="ceacc-224">At some point before your Automation account expires, you will need to renew the certificate.</span></span> <span data-ttu-id="ceacc-225">如果您認為執行身分帳戶遭到盜用，您可加以刪除並重新建立。</span><span class="sxs-lookup"><span data-stu-id="ceacc-225">If you believe that the Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="ceacc-226">本節會討論如何執行這些作業。</span><span class="sxs-lookup"><span data-stu-id="ceacc-226">This section discusses how to perform these operations.</span></span>

### <a name="self-signed-certificate-renewal"></a><span data-ttu-id="ceacc-227">自我簽署憑證更新</span><span class="sxs-lookup"><span data-stu-id="ceacc-227">Self-signed certificate renewal</span></span>
<span data-ttu-id="ceacc-228">您為執行身分帳戶建立的自我簽署憑證，會在建立日起算一年後到期。</span><span class="sxs-lookup"><span data-stu-id="ceacc-228">The self-signed certificate that you created for the Run As account expires one year from the date of creation.</span></span> <span data-ttu-id="ceacc-229">您可以在該憑證到期前隨時更新憑證。</span><span class="sxs-lookup"><span data-stu-id="ceacc-229">You can renew it at any time before it expires.</span></span> <span data-ttu-id="ceacc-230">當您更新憑證時，目前的有效憑證會予以保留，以確保已排入佇列或正在執行以及使用該執行身分帳戶進行驗證的任何 Runbook 不會受到負面影響。</span><span class="sxs-lookup"><span data-stu-id="ceacc-230">When you renew it, the current valid certificate is retained to ensure that any runbooks that are queued up or actively running, and that authenticate with the Run As account, are not negatively affected.</span></span> <span data-ttu-id="ceacc-231">憑證在到期日之前會保持有效。</span><span class="sxs-lookup"><span data-stu-id="ceacc-231">The certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="ceacc-232">如果您已設定您的自動化執行身分帳戶以使用您的企業憑證授權單位所核發的憑證，而且您使用此選項，該企業憑證將會由自我簽署憑證所取代。</span><span class="sxs-lookup"><span data-stu-id="ceacc-232">If you have configured your Automation Run As account to use a certificate issued by your enterprise certificate authority and you use this option, the enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="ceacc-233">若要更新憑證，請執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="ceacc-233">To renew the certificate, do the following:</span></span>

1. <span data-ttu-id="ceacc-234">在 Azure 入口網站中，開啟自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-234">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="ceacc-235">在 [自動化帳戶] 刀鋒視窗的 [帳戶屬性] 窗格中，於 [帳戶設定] 底下選取 [執行身分帳戶]。</span><span class="sxs-lookup"><span data-stu-id="ceacc-235">On the **Automation Account** blade, in the **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![自動化帳戶的屬性窗格](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. <span data-ttu-id="ceacc-237">在 [執行身分帳戶] 的屬性刀鋒視窗中，選取您想要更新憑證的執行身分帳戶或傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-237">On the **Run As Accounts** properties blade, select either the Run As account or the Classic Run As account that you want to renew the certificate for.</span></span>

4. <span data-ttu-id="ceacc-238">在所選帳戶的 [屬性] 刀鋒視窗上，按一下 [更新憑證]。</span><span class="sxs-lookup"><span data-stu-id="ceacc-238">On the **Properties** blade for the selected account, click **Renew certificate**.</span></span>

    ![更新執行身分帳戶的憑證](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="ceacc-240">更新憑證時，您可以在功能表的 [通知] 底下追蹤進度。</span><span class="sxs-lookup"><span data-stu-id="ceacc-240">While the certificate is being renewed, you can track the progress under **Notifications** from the menu.</span></span>

### <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="ceacc-241">刪除執行身分或傳統執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="ceacc-241">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="ceacc-242">本節說明如何刪除並重新建立執行身分或傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-242">This section describes how to delete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="ceacc-243">當您執行此動作時，系統不會保留自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-243">When you perform this action, the Automation account is retained.</span></span> <span data-ttu-id="ceacc-244">刪除執行身分或傳統執行身分帳戶之後，您可以在 Azure 入口網站中重新建立它。</span><span class="sxs-lookup"><span data-stu-id="ceacc-244">After you delete a Run As or Classic Run As account, you can re-create it in the Azure portal.</span></span>

1. <span data-ttu-id="ceacc-245">在 Azure 入口網站中，開啟自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-245">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="ceacc-246">在 [自動化帳戶] 刀鋒視窗的 [帳戶屬性] 窗格中，選取 [執行身分帳戶]。</span><span class="sxs-lookup"><span data-stu-id="ceacc-246">On the **Automation account** blade, in the account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="ceacc-247">在 [執行身分帳戶] 的屬性刀鋒視窗中，選取您想要刪除的執行身分帳戶或傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-247">On the **Run As Accounts** properties blade, select either the Run As account or Classic Run As account that you want to delete.</span></span> <span data-ttu-id="ceacc-248">然後，在所選帳戶的 [屬性] 刀鋒視窗上，按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="ceacc-248">Then, on the **Properties** blade for the selected account, click **Delete**.</span></span>

 ![刪除執行身分帳戶](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. <span data-ttu-id="ceacc-250">刪除帳戶時，您可以在功能表的 [通知] 底下追蹤進度。</span><span class="sxs-lookup"><span data-stu-id="ceacc-250">While the account is being deleted, you can track the progress under **Notifications** from the menu.</span></span>

5. <span data-ttu-id="ceacc-251">帳戶刪除之後，您可以在 [執行身分帳戶] 的屬性刀鋒視窗中，選取建立選項 [Azure 執行身分帳戶]來重新建立它。</span><span class="sxs-lookup"><span data-stu-id="ceacc-251">After the account has been deleted, you can re-create it on the **Run As Accounts** properties blade by selecting the create option **Azure Run As Account**.</span></span>

 ![重新建立自動化執行身分帳戶](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a><span data-ttu-id="ceacc-253">設定錯誤</span><span class="sxs-lookup"><span data-stu-id="ceacc-253">Misconfiguration</span></span>
<span data-ttu-id="ceacc-254">在初始設定期間，您可能會以不正確的方式刪除或建立要讓執行身分或傳統執行身分帳戶正常運作所需的某些設定項目。</span><span class="sxs-lookup"><span data-stu-id="ceacc-254">Some configuration items necessary for the Run As or Classic Run As account to function properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="ceacc-255">這些項目包括︰</span><span class="sxs-lookup"><span data-stu-id="ceacc-255">The items include:</span></span>

* <span data-ttu-id="ceacc-256">憑證資產</span><span class="sxs-lookup"><span data-stu-id="ceacc-256">Certificate asset</span></span>
* <span data-ttu-id="ceacc-257">連線資產</span><span class="sxs-lookup"><span data-stu-id="ceacc-257">Connection asset</span></span>
* <span data-ttu-id="ceacc-258">已從參與者角色移除了執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="ceacc-258">Run As account has been removed from the contributor role</span></span>
* <span data-ttu-id="ceacc-259">Azure AD 中的服務主體或應用程式</span><span class="sxs-lookup"><span data-stu-id="ceacc-259">Service principal or application in Azure AD</span></span>

<span data-ttu-id="ceacc-260">在上述設定錯誤和其他這類情況中，自動化帳戶會偵測到變更，並在帳戶的 [執行身分帳戶] 屬性刀鋒視窗上顯示 [不完整] 狀態。</span><span class="sxs-lookup"><span data-stu-id="ceacc-260">In the preceding and other instances of misconfiguration, the Automation account detects the changes and displays a status of *Incomplete* on the **Run As Accounts** properties blade for the account.</span></span>

![不完整的執行身分帳戶設定狀態](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="ceacc-262">當您選取執行身分帳戶時，帳戶的 [屬性] 窗格會顯示下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="ceacc-262">When you select the Run As account, the account **Properties** pane displays the following error message:</span></span>

![不完整的執行身分設定警告訊息](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="ceacc-264">。</span><span class="sxs-lookup"><span data-stu-id="ceacc-264">.</span></span>

<span data-ttu-id="ceacc-265">您可以藉由刪除並重新建立這些執行身分帳戶，來快速解決帳戶的問題。</span><span class="sxs-lookup"><span data-stu-id="ceacc-265">You can quickly resolve these Run As account issues by deleting and re-creating the account.</span></span>

## <a name="update-your-automation-account-by-using-powershell"></a><span data-ttu-id="ceacc-266">使用 PowerShell 更新自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="ceacc-266">Update your Automation account by using PowerShell</span></span>
<span data-ttu-id="ceacc-267">您可以使用 PowerShell 來更新現有的自動化帳戶，但前提是︰</span><span class="sxs-lookup"><span data-stu-id="ceacc-267">You can use PowerShell to update your existing Automation account if:</span></span>

* <span data-ttu-id="ceacc-268">您已建立一個自動化帳戶，但拒絕建立執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-268">You create an Automation account but decline to create the Run As account.</span></span>
* <span data-ttu-id="ceacc-269">您已使用自動化帳戶來管理 Resource Manager 資源，而且您想要更新此帳戶以包含可供 Runbook 驗證的執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-269">You already use an Automation account to manage Resource Manager resources and you want to update the account to include the Run As account for runbook authentication.</span></span>
* <span data-ttu-id="ceacc-270">您已使用自動化帳戶來管理傳統資源，而且您想要更新此帳戶以使用傳統執行身分，而不是建立新的帳戶並將 Runbook 和資產移轉至該帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-270">You already use an Automation account to manage classic resources and you want to update it to use the Classic Run As account instead of creating a new account and migrating your runbooks and assets to it.</span></span>   
* <span data-ttu-id="ceacc-271">您想要使用企業憑證授權單位 (CA) 所核發的憑證，來建立執行身分和傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-271">You want to create a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

<span data-ttu-id="ceacc-272">此指令碼有下列先決條件：</span><span class="sxs-lookup"><span data-stu-id="ceacc-272">The script has the following prerequisites:</span></span>

* <span data-ttu-id="ceacc-273">此指令碼只能在具有 Azure Resource Manager 模組 2.01 和更新版本的 Windows 10 與 Windows Server 2016 上執行。</span><span class="sxs-lookup"><span data-stu-id="ceacc-273">The script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="ceacc-274">不支援在舊版 Windows 上執行。</span><span class="sxs-lookup"><span data-stu-id="ceacc-274">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="ceacc-275">Azure PowerShell 1.0 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="ceacc-275">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="ceacc-276">如需有關 PowerShell 1.0 版本的資訊，請參閱[如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="ceacc-276">For information about the PowerShell 1.0 release, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="ceacc-277">自動化帳戶，系統會將其參照作為下列 PowerShell 指令碼中 –AutomationAccountName 和 -ApplicationDisplayName 參數的值。</span><span class="sxs-lookup"><span data-stu-id="ceacc-277">An Automation account, which is referenced as the value for the *–AutomationAccountName* and *-ApplicationDisplayName* parameters in the following PowerShell script.</span></span>

<span data-ttu-id="ceacc-278">若要取得指令碼所需參數 SubscriptionID、ResourceGroup 和 AutomationAccountName 的值，請執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="ceacc-278">To get the values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for the scripts, do the following:</span></span>
1. <span data-ttu-id="ceacc-279">在 Azure 入口網站中，於 [自動化帳戶] 刀鋒視窗上選取您的自動化帳戶，然後選取 [所有設定]。</span><span class="sxs-lookup"><span data-stu-id="ceacc-279">In the Azure portal, select your Automation account on the **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="ceacc-280">在 [所有設定] 刀鋒視窗上，選取 [帳戶設定] 之下的 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="ceacc-280">On the **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="ceacc-281">請記下 [屬性] 刀鋒視窗上的值。</span><span class="sxs-lookup"><span data-stu-id="ceacc-281">Note the values on the **Properties** blade.</span></span>

![自動化帳戶的 [屬性] 刀鋒視窗](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a><span data-ttu-id="ceacc-283">建立執行身分帳戶 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="ceacc-283">Create a Run As account PowerShell script</span></span>
<span data-ttu-id="ceacc-284">這個 PowerShell 指令碼包含下列組態的支援︰</span><span class="sxs-lookup"><span data-stu-id="ceacc-284">This PowerShell script includes support for the following configurations:</span></span>

* <span data-ttu-id="ceacc-285">使用自我簽署憑證建立執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-285">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="ceacc-286">使用自我簽署憑證建立執行身分帳戶和傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-286">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="ceacc-287">使用企業憑證建立執行身分帳戶和傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-287">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="ceacc-288">在 Azure Government 雲端中，使用自我簽署憑證建立執行身分帳戶和傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceacc-288">Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud.</span></span>

<span data-ttu-id="ceacc-289">視您選取的組態選項，指令碼會建立下列項目。</span><span class="sxs-lookup"><span data-stu-id="ceacc-289">Depending on the configuration option you select, the script creates the following items.</span></span>

<span data-ttu-id="ceacc-290">**若為執行身分帳戶︰**</span><span class="sxs-lookup"><span data-stu-id="ceacc-290">**For Run As accounts:**</span></span>

* <span data-ttu-id="ceacc-291">建立可使用自我簽署憑證或企業憑證的公開金鑰進行匯出的 Azure AD 應用程式、建立此應用程式在 Azure AD 中的服務主體帳戶，並在目前的訂用帳戶中為此帳戶指派參與者角色。</span><span class="sxs-lookup"><span data-stu-id="ceacc-291">Creates an Azure AD application to be exported with either the self-signed or enterprise certificate public key, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="ceacc-292">您可以將此設定變更為擁有者或任何其他角色。</span><span class="sxs-lookup"><span data-stu-id="ceacc-292">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="ceacc-293">如需詳細資訊，請參閱 [Azure 自動化中的角色型存取控制](automation-role-based-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="ceacc-293">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="ceacc-294">在指定的自動化帳戶中，建立名為 AzureRunAsCertificate 的自動化憑證資產。</span><span class="sxs-lookup"><span data-stu-id="ceacc-294">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="ceacc-295">憑證資產會保存 Azure AD 應用程式所使用的憑證私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="ceacc-295">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="ceacc-296">在指定的自動化帳戶中，建立名為 AzureRunAsConnection 的自動化連線資產。</span><span class="sxs-lookup"><span data-stu-id="ceacc-296">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="ceacc-297">連線資產會保存 applicationId、tenantId、subscriptionId 和憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="ceacc-297">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="ceacc-298">**若為傳統執行身分帳戶：**</span><span class="sxs-lookup"><span data-stu-id="ceacc-298">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="ceacc-299">在指定的自動化帳戶中，建立名為 AzureClassicRunAsCertificate 的自動化憑證資產。</span><span class="sxs-lookup"><span data-stu-id="ceacc-299">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="ceacc-300">憑證資產會保存管理憑證所使用的憑證私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="ceacc-300">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="ceacc-301">在指定的自動化帳戶中，建立名為 AzureClassicRunAsConnection 的自動化連線資產。</span><span class="sxs-lookup"><span data-stu-id="ceacc-301">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="ceacc-302">連線資產會保存訂用帳戶名稱、subscriptionId 和憑證資產名稱。</span><span class="sxs-lookup"><span data-stu-id="ceacc-302">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="ceacc-303">如果您選取任一選項來建立傳統執行方式帳戶，在指令碼執行之後，請將公開憑證 (.cer 副檔名) 上傳至自動化帳戶建立所在之訂用帳戶的管理存放區中。</span><span class="sxs-lookup"><span data-stu-id="ceacc-303">If you select either option for creating a Classic Run As account, after the script is executed, upload the public certificate (.cer file name extension) to the management store for the subscription that the Automation account was created in.</span></span>
> 

<span data-ttu-id="ceacc-304">若要執行指令碼並上傳憑證，請執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="ceacc-304">To execute the script and upload the certificate, do the following:</span></span>

1. <span data-ttu-id="ceacc-305">將下列指令碼儲存到電腦。</span><span class="sxs-lookup"><span data-stu-id="ceacc-305">Save the following script on your computer.</span></span> <span data-ttu-id="ceacc-306">在此範例中，請以檔案名稱 *New-RunAsAccount.ps1*進行儲存。</span><span class="sxs-lookup"><span data-stu-id="ceacc-306">In this example, save it with the filename *New-RunAsAccount.ps1*.</span></span>

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

        # Sleep here for a few seconds to allow the service principal application to become active (ordinarily takes a few seconds)
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
           Write-Error -Message "Please install the latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate the ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload the .cer format of #CERT# to the Management store by following the steps below." + [Environment]::NewLine +
                    "Log in to the Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload the .cer format of #CERT#"

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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate the ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="ceacc-307">在電腦上按一下 [啟動]，然後以提高的使用者權限啟動 **Windows PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="ceacc-307">On your computer, click **Start**, and then start **Windows PowerShell** with elevated user rights.</span></span>

3. <span data-ttu-id="ceacc-308">從提高權限的 PowerShell 命令列殼層，移至包含您在步驟 1 中建立的指令碼的資料夾。</span><span class="sxs-lookup"><span data-stu-id="ceacc-308">From the elevated PowerShell command-line shell, go to the folder that contains the script you created in step 1.</span></span>

4. <span data-ttu-id="ceacc-309">使用所需設定的參數值來執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="ceacc-309">Execute the script by using the parameter values for the configuration you require.</span></span>

    <span data-ttu-id="ceacc-310">**使用自我簽署憑證建立執行身分帳戶**</span><span class="sxs-lookup"><span data-stu-id="ceacc-310">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="ceacc-311">**使用自我簽署憑證建立執行身分帳戶和傳統執行身分帳戶**</span><span class="sxs-lookup"><span data-stu-id="ceacc-311">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="ceacc-312">**使用企業憑證建立執行身分帳戶和傳統執行身分帳戶**</span><span class="sxs-lookup"><span data-stu-id="ceacc-312">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="ceacc-313">**在 Azure Government 雲端中，使用自我簽署憑證建立執行身分帳戶和傳統執行身分帳戶**</span><span class="sxs-lookup"><span data-stu-id="ceacc-313">**Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="ceacc-314">指令碼執行之後，您會收到向 Azure 進行驗證的提示。</span><span class="sxs-lookup"><span data-stu-id="ceacc-314">After the script has executed, you will be prompted to authenticate with Azure.</span></span> <span data-ttu-id="ceacc-315">請以訂用帳戶管理員角色成員和訂用帳戶共同管理員的帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="ceacc-315">Sign in with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>
    >
    >

<span data-ttu-id="ceacc-316">指令碼執行成功之後，請注意下列事項︰</span><span class="sxs-lookup"><span data-stu-id="ceacc-316">After the script has executed successfully, note the following:</span></span>
* <span data-ttu-id="ceacc-317">如果您使用自我簽署的公開憑證 (.cer 檔案) 建立了傳統執行身分帳戶，指令碼會建立該帳戶並將其儲存在電腦上的暫存檔案資料夾中，用來執行 PowerShell 工作階段的使用者設定檔 %USERPROFILE%\AppData\Local\Temp 底下。</span><span class="sxs-lookup"><span data-stu-id="ceacc-317">If you created a Classic Run As account with a self-signed public certificate (.cer file), the script creates and saves it to the temporary files folder on your computer under the user profile *%USERPROFILE%\AppData\Local\Temp*, which you used to execute the PowerShell session.</span></span>
* <span data-ttu-id="ceacc-318">如果您使用企業公開憑證 (.cer 檔案) 建立了傳統執行身分帳戶，請使用此憑證。</span><span class="sxs-lookup"><span data-stu-id="ceacc-318">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="ceacc-319">請遵循[將管理 API 憑證上傳至 Azure 傳統入口網站](../azure-api-management-certs.md)的指示，然後使用[用來向服務管理資源進行驗證的程式碼範例](#sample-code-to-authenticate-with-service-management-resources)來驗證服務管理資源的認證組態。</span><span class="sxs-lookup"><span data-stu-id="ceacc-319">Follow the instructions for [uploading a management API certificate to the Azure classic portal](../azure-api-management-certs.md), and then validate the credential configuration with Service Management resources by using the [sample code to authenticate with Service Management Resources](#sample-code-to-authenticate-with-service-management-resources).</span></span> 
* <span data-ttu-id="ceacc-320">如果您「並未」建立傳統執行身分帳戶，請使用[用來向服務管理資源進行驗證的程式碼範例](#sample-code-to-authenticate-with-resource-manager-resources)向 Resource Manager 資源進行驗證並驗證認證組態。</span><span class="sxs-lookup"><span data-stu-id="ceacc-320">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate the credential configuration by using the [sample code for authenticating with Service Management resources](#sample-code-to-authenticate-with-resource-manager-resources).</span></span>

## <a name="sample-code-to-authenticate-with-resource-manager-resources"></a><span data-ttu-id="ceacc-321">用來向 Resource Manager 資源進行驗證的範例程式碼</span><span class="sxs-lookup"><span data-stu-id="ceacc-321">Sample code to authenticate with Resource Manager resources</span></span>
<span data-ttu-id="ceacc-322">您可以使用下列已更新的範例程式碼 (取自 AzureAutomationTutorialScript 範例 Runbook)，以執行身分帳戶進行驗證來使用 Runbook 管理 Resource Manager 資源。</span><span class="sxs-lookup"><span data-stu-id="ceacc-322">You can use the following updated sample code, taken from the *AzureAutomationTutorialScript* example runbook, to authenticate by using the Run As account to manage Resource Manager resources with your runbooks.</span></span>

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get the connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in to Azure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context to a specific subscription"     
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

<span data-ttu-id="ceacc-323">為了協助您輕鬆地在多個訂用帳戶之間進行工作，指令碼另外包含兩行程式碼來支援訂用帳戶內容的參考。</span><span class="sxs-lookup"><span data-stu-id="ceacc-323">To help you to easily work between multiple subscriptions, the script includes two additional lines of code that support referencing a subscription context.</span></span> <span data-ttu-id="ceacc-324">名為 SubscriptionId 的變數資產包含訂用帳戶的識別碼。</span><span class="sxs-lookup"><span data-stu-id="ceacc-324">A variable asset named *SubscriptionId* contains the ID of the subscription.</span></span> <span data-ttu-id="ceacc-325">在 `Add-AzureRmAccount` Cmdlet 陳述式後面，[`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) Cmdlet 會以參數集 -SubscriptionId 來指定。</span><span class="sxs-lookup"><span data-stu-id="ceacc-325">After the `Add-AzureRmAccount` cmdlet statement, the [`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet is stated with the parameter set *-SubscriptionId*.</span></span> <span data-ttu-id="ceacc-326">如果變數名稱太過一般，您可加以修改使其包含前置詞，或使用其他命名慣例讓名稱能夠更容易地識別。</span><span class="sxs-lookup"><span data-stu-id="ceacc-326">If the variable name is too generic, you can revise it to include a prefix or use another naming convention to make it easier to identify.</span></span> <span data-ttu-id="ceacc-327">或者，您可以使用參數集 -SubscriptionName (而非 -SubscriptionId) 與對應的變數資產。</span><span class="sxs-lookup"><span data-stu-id="ceacc-327">Alternatively, you can use the parameter set *-SubscriptionName* instead of *-SubscriptionId* with a corresponding variable asset.</span></span>

<span data-ttu-id="ceacc-328">Runbook 中用來驗證的 Cmdlet (`Add-AzureRmAccount`) 會使用 ServicePrincipalCertificate 參數集。</span><span class="sxs-lookup"><span data-stu-id="ceacc-328">The cmdlet that you use for authenticating in the runbook, `Add-AzureRmAccount`, uses the *ServicePrincipalCertificate* parameter set.</span></span> <span data-ttu-id="ceacc-329">它藉由使用服務主體憑證 (而非使用者認證) 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="ceacc-329">It authenticates by using the service principal certificate, not the user credentials.</span></span>

## <a name="sample-code-to-authenticate-with-service-management-resources"></a><span data-ttu-id="ceacc-330">用來向服務管理資源進行驗證的範例程式碼</span><span class="sxs-lookup"><span data-stu-id="ceacc-330">Sample code to authenticate with Service Management resources</span></span>
<span data-ttu-id="ceacc-331">您可以使用下列已更新的範例程式碼 (取自 AzureClassicAutomationTutorialScript Runbook 範例)，使用傳統執行身分帳戶進行驗證以使用 Runbook 管理傳統資源。</span><span class="sxs-lookup"><span data-stu-id="ceacc-331">You can use the following updated sample code, which is taken from the *AzureClassicAutomationTutorialScript* example runbook, to authenticate by using the Classic Run As account to manage classic resources with your runbooks.</span></span>

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get the connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate to Azure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in the Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting the certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in the Automation account."
    }

    Write-Verbose "Authenticating to Azure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a><span data-ttu-id="ceacc-332">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ceacc-332">Next steps</span></span>
* [<span data-ttu-id="ceacc-333">Azure AD 中的應用程式和服務主體物件</span><span class="sxs-lookup"><span data-stu-id="ceacc-333">Application and service principal objects in Azure AD</span></span>](../active-directory/active-directory-application-objects.md)
* [<span data-ttu-id="ceacc-334">Azure 自動化中的角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="ceacc-334">Role-based access control in Azure Automation</span></span>](automation-role-based-access-control.md)
* [<span data-ttu-id="ceacc-335">Azure 雲端服務的憑證概觀</span><span class="sxs-lookup"><span data-stu-id="ceacc-335">Certificates overview for Azure Cloud Services</span></span>](../cloud-services/cloud-services-certs-create.md)
