---
title: "建立 Azure 自動化執行身分帳戶 | Microsoft Docs"
description: "本文說明如何更新您的自動化帳戶，並使用 PowerShell 或從入口網站建立執行身分帳戶。"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: eaf6eb49bbfe4572827fcc101d1f552b48ab91e6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a><span data-ttu-id="3c4ce-103">使用執行身分帳戶更新您的自動化帳戶驗證</span><span class="sxs-lookup"><span data-stu-id="3c4ce-103">Update your Automation account authentication with Run As accounts</span></span> 
<span data-ttu-id="3c4ce-104">您可以從入口網站或使用 PowerShell 來更新現有的自動化帳戶，前提是：</span><span class="sxs-lookup"><span data-stu-id="3c4ce-104">You can update your existing Automation account from the portal or use PowerShell if:</span></span>

* <span data-ttu-id="3c4ce-105">您已建立一個自動化帳戶，但拒絕建立執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-105">You create an Automation account but decline to create the Run As account.</span></span>
* <span data-ttu-id="3c4ce-106">您已使用自動化帳戶來管理 Resource Manager 資源，而且您想要更新此帳戶以包含可供 Runbook 驗證的執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-106">You already use an Automation account to manage Resource Manager resources and you want to update the account to include the Run As account for runbook authentication.</span></span>
* <span data-ttu-id="3c4ce-107">您已使用自動化帳戶來管理傳統資源，而且您想要更新此帳戶以使用傳統執行身分，而不是建立新的帳戶並將 Runbook 和資產移轉至該帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-107">You already use an Automation account to manage classic resources and you want to update it to use the Classic Run As account instead of creating a new account and migrating your runbooks and assets to it.</span></span>   
* <span data-ttu-id="3c4ce-108">您想要使用企業憑證授權單位 (CA) 所核發的憑證，來建立執行身分和傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-108">You want to create a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c4ce-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="3c4ce-109">Prerequisites</span></span>

* <span data-ttu-id="3c4ce-110">此指令碼只能在具有 Azure Resource Manager 模組 3.0.0 和更新版本的 Windows 10 與 Windows Server 2016 上執行。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-110">The script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 3.0.0 and later.</span></span> <span data-ttu-id="3c4ce-111">不支援在舊版 Windows 上執行。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="3c4ce-112">Azure PowerShell 1.0 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="3c4ce-113">如需有關 PowerShell 1.0 版本的資訊，請參閱[如何安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-113">For information about the PowerShell 1.0 release, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="3c4ce-114">自動化帳戶，系統會將其參照做為下列 PowerShell 指令碼中 –AutomationAccountName 和 -ApplicationDisplayName 參數的值。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-114">An Automation account, which is referenced as the value for the *–AutomationAccountName* and *-ApplicationDisplayName* parameters in the following PowerShell script.</span></span>

<span data-ttu-id="3c4ce-115">若要取得指令碼所需參數 SubscriptionID、ResourceGroup 和 AutomationAccountName 的值，請執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="3c4ce-115">To get the values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for the script, do the following:</span></span>

1. <span data-ttu-id="3c4ce-116">在 Azure 入口網站中，於 [自動化帳戶] 刀鋒視窗上選取您的自動化帳戶，然後選取 [所有設定]。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-116">In the Azure portal, select your Automation account on the **Automation account** blade, and then select **All settings**.</span></span>  
2. <span data-ttu-id="3c4ce-117">在 [所有設定] 刀鋒視窗上，選取 [帳戶設定] 之下的 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-117">On the **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="3c4ce-118">請記下 [屬性] 刀鋒視窗上的值。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-118">Note the values on the **Properties** blade.</span></span><br><br> <span data-ttu-id="3c4ce-119">![自動化帳戶的 [屬性] 刀鋒視窗](media/automation-create-runas-account/automation-account-properties.png)</span><span class="sxs-lookup"><span data-stu-id="3c4ce-119">![The Automation account "Properties" blade](media/automation-create-runas-account/automation-account-properties.png)</span></span>  

### <a name="required-permissions-to-update-your-automation-account"></a><span data-ttu-id="3c4ce-120">更新自動化帳戶所需的權限</span><span class="sxs-lookup"><span data-stu-id="3c4ce-120">Required permissions to update your Automation account</span></span>
<span data-ttu-id="3c4ce-121">若要更新自動化帳戶，您必須具有下列特定權限，才能完成本主題。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-121">To update an Automation account, you must have the following specific privileges and permissions required to complete this topic.</span></span>   
 
* <span data-ttu-id="3c4ce-122">您的 AD 使用者帳戶必須新增至具備與 Microsoft.Automation 資源的參與者角色同等權限的角色 (如[Azure 自動化中的角色型存取控制](automation-role-based-access-control.md#contributor-role-permissions)一文所述)。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-122">Your AD user account needs to be added to a role with permissions equivalent to the Contributor role for Microsoft.Automation resources as outlined in article [Role-based access control in Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).</span></span>  
* <span data-ttu-id="3c4ce-123">如果應用程式註冊設定為 [是]，Azure AD 租用戶中的非系統管理使用者可以[註冊 AD 應用程式](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions)。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-123">Non-admin users in your Azure AD tenant can [register AD applications](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) if the App registrations setting is set to **Yes**.</span></span>  <span data-ttu-id="3c4ce-124">如果應用程式註冊設定為 [否]，則執行此動作的使用者必須是 Azure AD 中的全域管理員。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-124">If the app registrations setting is set to **No**, the user performing this action must be a global administrator in Azure AD.</span></span> 

<span data-ttu-id="3c4ce-125">若您在新增至訂用帳戶的全域管理員/共同管理員角色之前，並非訂用帳戶 Active Directory 執行個體的成員，系統會將您以來賓身分新增至 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-125">If you are not a member of the subscription’s Active Directory instance before you are added to the global administrator/co-administrator role of the subscription, you are added to Active Directory as a guest.</span></span> <span data-ttu-id="3c4ce-126">在此情況下，您會在 [新增自動化帳戶] 刀鋒視窗中看到</span><span class="sxs-lookup"><span data-stu-id="3c4ce-126">In this situation, you receive a “You do not have permissions to create…”</span></span> <span data-ttu-id="3c4ce-127">「您沒有權限建立...」的警告。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-127">warning on the **Add Automation Account** blade.</span></span> <span data-ttu-id="3c4ce-128">新增至全域管理員/共同管理員角色的使用者可以先從訂用帳戶的 Active Directory 執行個體中移除並重新新增，使其成為 Active Directory 中的完整使用者。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-128">Users who were added to the global administrator/co-administrator role first can be removed from the subscription's Active Directory instance and re-added to make them a full User in Active Directory.</span></span> <span data-ttu-id="3c4ce-129">若要確認這種情況，請從 Azure 入口網站的 [Azure Active Directory] 窗格，選取 [使用者和群組]、選取 [所有使用者]，然後在選取特定使用者之後，選取 [設定檔]。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-129">To verify this situation, from the **Azure Active Directory** pane in the Azure portal, select **Users and groups**, select **All users** and, after you select the specific user, select **Profile**.</span></span> <span data-ttu-id="3c4ce-130">使用者設定檔之下 [使用者類型] 屬性的值不得等於 [來賓]。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-130">The value of the **User type** attribute under the users profile should not equal **Guest**.</span></span>

## <a name="create-run-as-account-from-the-portal"></a><span data-ttu-id="3c4ce-131">從 Azure 入口網站建立執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="3c4ce-131">Create Run As account from the portal</span></span>
<span data-ttu-id="3c4ce-132">在本節中，執行下列步驟以從 Azure 入口網站更新 Azure 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-132">In this section, perform the following steps to update your Azure Automation account from  the Azure portal.</span></span>  <span data-ttu-id="3c4ce-133">您會個別建立執行身分和傳統執行身分帳戶，如果您不需要在 Azure 傳統入口網站中管理資源，您就可以建立 Azure 執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-133">You create the Run As and Classic Run As accounts individually, and if you don't need to manage resources in the classic Azure portal, you can just create the Azure Run As account.</span></span>  

<span data-ttu-id="3c4ce-134">此程序會在自動化帳戶中建立下列項目。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-134">The process creates the following items in your Automation account.</span></span>

<span data-ttu-id="3c4ce-135">**若為執行身分帳戶︰**</span><span class="sxs-lookup"><span data-stu-id="3c4ce-135">**For Run As accounts:**</span></span>

* <span data-ttu-id="3c4ce-136">建立可使用自我簽署憑證或企業憑證的公開金鑰進行匯出的 Azure AD 應用程式、建立此應用程式在 Azure AD 中的服務主體帳戶，並在目前的訂用帳戶中為此帳戶指派參與者角色。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-136">Creates an Azure AD application with a self-signed certificate, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="3c4ce-137">您可以將此設定變更為擁有者或任何其他角色。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-137">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="3c4ce-138">如需詳細資訊，請參閱 [Azure 自動化中的角色型存取控制](automation-role-based-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-138">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="3c4ce-139">在指定的自動化帳戶中，建立名為 AzureRunAsCertificate 的自動化憑證資產。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-139">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="3c4ce-140">憑證資產會保存 Azure AD 應用程式所使用的憑證私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-140">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="3c4ce-141">在指定的自動化帳戶中，建立名為 AzureRunAsConnection 的自動化連線資產。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-141">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="3c4ce-142">連線資產會保存 applicationId、tenantId、subscriptionId 和憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-142">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="3c4ce-143">**若為傳統執行身分帳戶：**</span><span class="sxs-lookup"><span data-stu-id="3c4ce-143">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="3c4ce-144">在指定的自動化帳戶中，建立名為 AzureClassicRunAsCertificate 的自動化憑證資產。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-144">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="3c4ce-145">憑證資產會保存管理憑證所使用的憑證私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-145">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="3c4ce-146">在指定的自動化帳戶中，建立名為 AzureClassicRunAsConnection 的自動化連線資產。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-146">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="3c4ce-147">連線資產會保存訂用帳戶名稱、subscriptionId 和憑證資產名稱。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-147">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

1. <span data-ttu-id="3c4ce-148">以訂用帳戶管理員角色成員和訂用帳戶共同管理員的帳戶登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-148">Sign in to the Azure portal with an account that is a member of the Subscription Admins role and co-administrator of the subscription.</span></span>
2. <span data-ttu-id="3c4ce-149">從 [自動化帳戶] 刀鋒視窗，選取 [帳戶設定] 區段下的 [執行身分帳戶]。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-149">From the Automation account blade, select **Run As Accounts** under the section **Account Settings**.</span></span>  
3. <span data-ttu-id="3c4ce-150">根據您所需的帳戶，選取 [Azure 執行身分帳戶] 或 [Azure 傳統執行身分帳戶]。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-150">Depending on which account you require, select either **Azure Run As Account** or **Azure Classic Run As Account**.</span></span>  <span data-ttu-id="3c4ce-151">選取 [新增 Azure 執行身分] 之後或 [新增 Azure 傳統執行身分帳戶] 刀鋒視窗出現之後，並檢閱概觀資訊之後，請按一下 [建立] 繼續建立執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-151">After selecting either the **Add Azure Run As** or **Add Azure Classic Run As Account** blade appears and after reviewing the overview information, click **Create** to proceed with Run As account creation.</span></span>  
4. <span data-ttu-id="3c4ce-152">在 Azure 建立執行身分帳戶時，您可以在功能表的 [通知] 底下追蹤進度，系統會顯示一個橫幅，表示正在建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-152">While Azure creates the Run As account, you can track the progress under **Notifications** from the menu and a banner is displayed stating the account is being created.</span></span>  <span data-ttu-id="3c4ce-153">此程序需要數分鐘的時間完成。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-153">This process can take a few minutes to complete.</span></span>  

## <a name="create-run-as-account-using-powershell-script"></a><span data-ttu-id="3c4ce-154">使用 PowerShell 指令碼建立執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="3c4ce-154">Create Run As account using PowerShell script</span></span>
<span data-ttu-id="3c4ce-155">這個 PowerShell 指令碼包含下列組態的支援︰</span><span class="sxs-lookup"><span data-stu-id="3c4ce-155">This PowerShell script includes support for the following configurations:</span></span>

* <span data-ttu-id="3c4ce-156">使用自我簽署憑證建立執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-156">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="3c4ce-157">使用自我簽署憑證建立執行身分帳戶和傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-157">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="3c4ce-158">使用企業憑證建立執行身分帳戶和傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-158">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="3c4ce-159">在 Azure Government 雲端中，使用自我簽署憑證建立執行身分帳戶和傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-159">Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud.</span></span>

<span data-ttu-id="3c4ce-160">視您選取的組態選項，指令碼會建立下列項目。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-160">Depending on the configuration option you select, the script creates the following items.</span></span>

<span data-ttu-id="3c4ce-161">**若為執行身分帳戶︰**</span><span class="sxs-lookup"><span data-stu-id="3c4ce-161">**For Run As accounts:**</span></span>

* <span data-ttu-id="3c4ce-162">建立可使用自我簽署憑證或企業憑證的公開金鑰進行匯出的 Azure AD 應用程式、建立此應用程式在 Azure AD 中的服務主體帳戶，並在目前的訂用帳戶中為此帳戶指派參與者角色。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-162">Creates an Azure AD application to be exported with either the self-signed or enterprise certificate public key, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="3c4ce-163">您可以將此設定變更為擁有者或任何其他角色。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-163">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="3c4ce-164">如需詳細資訊，請參閱 [Azure 自動化中的角色型存取控制](automation-role-based-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-164">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="3c4ce-165">在指定的自動化帳戶中，建立名為 AzureRunAsCertificate 的自動化憑證資產。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-165">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="3c4ce-166">憑證資產會保存 Azure AD 應用程式所使用的憑證私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-166">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="3c4ce-167">在指定的自動化帳戶中，建立名為 AzureRunAsConnection 的自動化連線資產。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-167">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="3c4ce-168">連線資產會保存 applicationId、tenantId、subscriptionId 和憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-168">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="3c4ce-169">**若為傳統執行身分帳戶：**</span><span class="sxs-lookup"><span data-stu-id="3c4ce-169">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="3c4ce-170">在指定的自動化帳戶中，建立名為 AzureClassicRunAsCertificate 的自動化憑證資產。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-170">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="3c4ce-171">憑證資產會保存管理憑證所使用的憑證私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-171">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="3c4ce-172">在指定的自動化帳戶中，建立名為 AzureClassicRunAsConnection 的自動化連線資產。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-172">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="3c4ce-173">連線資產會保存訂用帳戶名稱、subscriptionId 和憑證資產名稱。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-173">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="3c4ce-174">如果您選取任一選項來建立傳統執行方式帳戶，在指令碼執行之後，請將公開憑證 (.cer 副檔名) 上傳至自動化帳戶建立所在之訂用帳戶的管理存放區中。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-174">If you select either option for creating a Classic Run As account, after the script is executed, upload the public certificate (.cer file name extension) to the management store for the subscription that the Automation account was created in.</span></span>
> 

1. <span data-ttu-id="3c4ce-175">將下列指令碼儲存到電腦。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-175">Save the following script on your computer.</span></span> <span data-ttu-id="3c4ce-176">在此範例中，請以檔案名稱 *New-RunAsAccount.ps1*進行儲存。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-176">In this example, save it with the filename *New-RunAsAccount.ps1*.</span></span>

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
        $KeyCredential.EndDate = Get-Date $PfxCert.GetExpirationDateString()
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
        if (!(($AzureRMProfileVersion.Major -ge 3 -and $AzureRMProfileVersion.Minor -ge 0) -or ($AzureRMProfileVersion.Major -gt 3)))
        {
            Write-Error -Message "Please install the latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
            return
        }

        Login-AzureRmAccount -Environment $EnvironmentName 
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
        $SubscriptionName = $subscription.Subscription.Name
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="3c4ce-177">在電腦上以提高的使用者權限從 [開始] 畫面啟動 **Windows PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-177">On your computer, start **Windows PowerShell** from the **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="3c4ce-178">從提高權限的命令列殼層，移至包含您在步驟 1 中建立的指令碼的資料夾。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-178">From the elevated command-line shell, go to the folder that contains the script you created in step 1.</span></span>  
4. <span data-ttu-id="3c4ce-179">使用所需設定的參數值來執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-179">Execute the script by using the parameter values for the configuration you require.</span></span>

    <span data-ttu-id="3c4ce-180">**使用自我簽署憑證建立執行身分帳戶**</span><span class="sxs-lookup"><span data-stu-id="3c4ce-180">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="3c4ce-181">**使用自我簽署憑證建立執行身分帳戶和傳統執行身分帳戶**</span><span class="sxs-lookup"><span data-stu-id="3c4ce-181">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="3c4ce-182">**使用企業憑證建立執行身分帳戶和傳統執行身分帳戶**</span><span class="sxs-lookup"><span data-stu-id="3c4ce-182">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="3c4ce-183">**在 Azure Government 雲端中，使用自我簽署憑證建立執行身分帳戶和傳統執行身分帳戶**</span><span class="sxs-lookup"><span data-stu-id="3c4ce-183">**Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="3c4ce-184">指令碼執行之後，您會收到向 Azure 進行驗證的提示。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-184">After the script has executed, you will be prompted to authenticate with Azure.</span></span> <span data-ttu-id="3c4ce-185">請以訂用帳戶管理員角色成員和訂用帳戶共同管理員的帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-185">Sign in with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>
    >
    >

<span data-ttu-id="3c4ce-186">指令碼執行成功之後，請注意下列事項︰</span><span class="sxs-lookup"><span data-stu-id="3c4ce-186">After the script has executed successfully, note the following:</span></span>
* <span data-ttu-id="3c4ce-187">如果您使用自我簽署的公開憑證 (.cer 檔案) 建立了傳統執行身分帳戶，指令碼會建立該帳戶並將其儲存在電腦上的暫存檔案資料夾中，用來執行 PowerShell 工作階段的使用者設定檔 %USERPROFILE%\AppData\Local\Temp 底下。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-187">If you created a Classic Run As account with a self-signed public certificate (.cer file), the script creates and saves it to the temporary files folder on your computer under the user profile *%USERPROFILE%\AppData\Local\Temp*, which you used to execute the PowerShell session.</span></span>
* <span data-ttu-id="3c4ce-188">如果您使用企業公開憑證 (.cer 檔案) 建立了傳統執行身分帳戶，請使用此憑證。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-188">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="3c4ce-189">請遵循[將管理 API 憑證上傳至 Azure 傳統入口網站](../azure-api-management-certs.md)的指示，然後使用[用來向服務 Azure 傳統部署資源進行驗證的範例程式碼](automation-verify-runas-authentication.md#classic-run-as-authentication)來驗證傳統部署資源的認證組態。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-189">Follow the instructions for [uploading a management API certificate to the Azure classic portal](../azure-api-management-certs.md), and then validate the credential configuration with classic deployment resources by using the [sample code to authenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="3c4ce-190">如果您「並未」建立傳統執行身分帳戶，請使用[用來向服務管理資源進行驗證的程式碼範例](automation-verify-runas-authentication.md#automation-run-as-authentication)向 Resource Manager 資源進行驗證並驗證認證組態。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-190">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate the credential configuration by using the [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c4ce-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3c4ce-191">Next steps</span></span>
* <span data-ttu-id="3c4ce-192">如需服務主體的詳細資訊，請參閱 [應用程式物件和服務主體物件](../active-directory/active-directory-application-objects.md)。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-192">For more information about Service Principals, refer to [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="3c4ce-193">如需有關憑證和 Azure 服務的詳細資訊，請參考 [Azure 雲端服務的憑證概觀](../cloud-services/cloud-services-certs-create.md)。</span><span class="sxs-lookup"><span data-stu-id="3c4ce-193">For more information about certificates and Azure services, refer to [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>