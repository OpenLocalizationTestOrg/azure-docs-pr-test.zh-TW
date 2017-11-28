---
title: "Azure 自動化執行身分帳戶 aaaCreate |Microsoft 文件"
description: "本文說明如何 tooupdate 您的自動化帳戶，並使用 PowerShell，或從 hello 入口網站建立執行身分帳戶。"
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
ms.openlocfilehash: 94eb54fa0b518056a726d17146c63411e248273b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a><span data-ttu-id="5ef27-103">使用執行身分帳戶更新您的自動化帳戶驗證</span><span class="sxs-lookup"><span data-stu-id="5ef27-103">Update your Automation account authentication with Run As accounts</span></span> 
<span data-ttu-id="5ef27-104">您可以更新您現有的自動化帳戶從 hello 入口網站，或使用 PowerShell，如果：</span><span class="sxs-lookup"><span data-stu-id="5ef27-104">You can update your existing Automation account from hello portal or use PowerShell if:</span></span>

* <span data-ttu-id="5ef27-105">建立自動化帳戶，但拒絕 toocreate hello 執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ef27-105">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="5ef27-106">您已經使用自動化帳戶 toomanage 資源管理員資源，並想 runbook 驗證 tooupdate hello tooinclude hello 執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ef27-106">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="5ef27-107">您已經使用自動化帳戶 toomanage 傳統資源，而且您想 tooupdate 它 toouse hello 傳統執行身分帳戶，而不要建立新的帳戶和移轉您的 runbook 與資產 tooit。</span><span class="sxs-lookup"><span data-stu-id="5ef27-107">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="5ef27-108">您想要 toocreate 執行身分和傳統執行身分帳戶使用企業憑證授權單位 (CA) 所核發的憑證。</span><span class="sxs-lookup"><span data-stu-id="5ef27-108">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ef27-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="5ef27-109">Prerequisites</span></span>

* <span data-ttu-id="5ef27-110">hello 指令碼可以執行只在 Windows 10 及 Windows Server 2016 與 Azure 資源管理員模組 3.0.0 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="5ef27-110">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 3.0.0 and later.</span></span> <span data-ttu-id="5ef27-111">不支援在舊版 Windows 上執行。</span><span class="sxs-lookup"><span data-stu-id="5ef27-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="5ef27-112">Azure PowerShell 1.0 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="5ef27-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="5ef27-113">如需 hello PowerShell 1.0 版的資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)。</span><span class="sxs-lookup"><span data-stu-id="5ef27-113">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="5ef27-114">自動化帳戶被稱為 hello hello 值*– AutomationAccountName*和*-ApplicationDisplayName* hello 下列 PowerShell 指令碼中的參數。</span><span class="sxs-lookup"><span data-stu-id="5ef27-114">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="5ef27-115">tooget hello 值*SubscriptionID*， *ResourceGroup*，和*AutomationAccountName*、 哪些是 hello 指令碼的必要的參數、 執行 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="5ef27-115">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello script, do hello following:</span></span>

1. <span data-ttu-id="5ef27-116">在 hello Azure 入口網站中選取您的自動化帳戶上 hello**自動化帳戶**刀鋒視窗中，然後再選取**所有設定**。</span><span class="sxs-lookup"><span data-stu-id="5ef27-116">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span>  
2. <span data-ttu-id="5ef27-117">在 hello**所有設定**刀鋒視窗底下**帳戶設定**，選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="5ef27-117">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="5ef27-118">請注意在 hello hello 值**屬性**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5ef27-118">Note hello values on hello **Properties** blade.</span></span><br><br> <span data-ttu-id="5ef27-119">![hello 自動化帳戶 [屬性] 刀鋒視窗](media/automation-create-runas-account/automation-account-properties.png)</span><span class="sxs-lookup"><span data-stu-id="5ef27-119">![hello Automation account "Properties" blade](media/automation-create-runas-account/automation-account-properties.png)</span></span>  

### <a name="required-permissions-tooupdate-your-automation-account"></a><span data-ttu-id="5ef27-120">您的自動化帳戶所需的權限 tooupdate</span><span class="sxs-lookup"><span data-stu-id="5ef27-120">Required permissions tooupdate your Automation account</span></span>
<span data-ttu-id="5ef27-121">tooupdate 自動化帳戶，您必須擁有 hello 遵循特定的權限，而且所需權限 toocomplete 本主題。</span><span class="sxs-lookup"><span data-stu-id="5ef27-121">tooupdate an Automation account, you must have hello following specific privileges and permissions required toocomplete this topic.</span></span>   
 
* <span data-ttu-id="5ef27-122">您的 AD 使用者帳戶會需要 Microsoft.Automation 資源 toobe 加入的 tooa 角色與權限相等 toohello 參與者角色發行項中所述[Azure 自動化中的角色型存取控制](automation-role-based-access-control.md#contributor-role-permissions)。</span><span class="sxs-lookup"><span data-stu-id="5ef27-122">Your AD user account needs toobe added tooa role with permissions equivalent toohello Contributor role for Microsoft.Automation resources as outlined in article [Role-based access control in Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).</span></span>  
* <span data-ttu-id="5ef27-123">Azure AD 租用戶中的非系統管理使用者可以[註冊 AD 應用程式](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions)如果 hello 應用程式登錄設定已設定太**是**。</span><span class="sxs-lookup"><span data-stu-id="5ef27-123">Non-admin users in your Azure AD tenant can [register AD applications](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) if hello App registrations setting is set too**Yes**.</span></span>  <span data-ttu-id="5ef27-124">如果設定太 hello 應用程式登錄設定**否**，執行此動作的 hello 使用者必須是 Azure AD 中的全域管理員。</span><span class="sxs-lookup"><span data-stu-id="5ef27-124">If hello app registrations setting is set too**No**, hello user performing this action must be a global administrator in Azure AD.</span></span> 

<span data-ttu-id="5ef27-125">如果您不是成員的 hello 訂用帳戶的 Active Directory 執行個體加入 toohello 全域系統管理員/共同管理員的角色 hello 訂用帳戶之前，您會做為來賓新增 tooActive 目錄。</span><span class="sxs-lookup"><span data-stu-id="5ef27-125">If you are not a member of hello subscription’s Active Directory instance before you are added toohello global administrator/co-administrator role of hello subscription, you are added tooActive Directory as a guest.</span></span> <span data-ttu-id="5ef27-126">在此情況下，您會收到 「 您沒有權限 toocreate...」</span><span class="sxs-lookup"><span data-stu-id="5ef27-126">In this situation, you receive a “You do not have permissions toocreate…”</span></span> <span data-ttu-id="5ef27-127">在 hello 警告**加入自動化帳戶**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5ef27-127">warning on hello **Add Automation Account** blade.</span></span> <span data-ttu-id="5ef27-128">Toohello 全域系統管理員/共同管理員角色首先會從 hello 訂用帳戶的 Active Directory 執行個體，並重新加入 toomake 加入的使用者其完整的使用者在 Active Directory 中。</span><span class="sxs-lookup"><span data-stu-id="5ef27-128">Users who were added toohello global administrator/co-administrator role first can be removed from hello subscription's Active Directory instance and re-added toomake them a full User in Active Directory.</span></span> <span data-ttu-id="5ef27-129">tooverify，請在此情況下，從 hello **Azure Active Directory** hello Azure 入口網站，選取在窗格**使用者和群組**，選取**所有使用者**和選取 hello 之後特定使用者，則選取**設定檔**。</span><span class="sxs-lookup"><span data-stu-id="5ef27-129">tooverify this situation, from hello **Azure Active Directory** pane in hello Azure portal, select **Users and groups**, select **All users** and, after you select hello specific user, select **Profile**.</span></span> <span data-ttu-id="5ef27-130">hello 值 hello**使用者類型**hello 使用者設定檔 下的屬性不可等於**客體**。</span><span class="sxs-lookup"><span data-stu-id="5ef27-130">hello value of hello **User type** attribute under hello users profile should not equal **Guest**.</span></span>

## <a name="create-run-as-account-from-hello-portal"></a><span data-ttu-id="5ef27-131">從 hello 入口網站中建立執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="5ef27-131">Create Run As account from hello portal</span></span>
<span data-ttu-id="5ef27-132">在本節中，從 hello Azure 入口網站 Azure 自動化帳戶執行下列步驟 tooupdate hello。</span><span class="sxs-lookup"><span data-stu-id="5ef27-132">In this section, perform hello following steps tooupdate your Azure Automation account from  hello Azure portal.</span></span>  <span data-ttu-id="5ef27-133">您建立 hello 執行身分和傳統執行身分帳戶會個別，如果您不需要 toomanage hello 傳統 Azure 入口網站中的資源，您可以只建立 hello Azure 執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ef27-133">You create hello Run As and Classic Run As accounts individually, and if you don't need toomanage resources in hello classic Azure portal, you can just create hello Azure Run As account.</span></span>  

<span data-ttu-id="5ef27-134">hello 程序會建立下列項目，在您的自動化帳戶中的 hello。</span><span class="sxs-lookup"><span data-stu-id="5ef27-134">hello process creates hello following items in your Automation account.</span></span>

<span data-ttu-id="5ef27-135">**若為執行身分帳戶︰**</span><span class="sxs-lookup"><span data-stu-id="5ef27-135">**For Run As accounts:**</span></span>

* <span data-ttu-id="5ef27-136">會建立 Azure AD 應用程式使用自我簽署憑證，在 Azure AD 中建立 hello 應用程式的服務主體帳戶並指派 hello 參與者角色，您目前的訂用帳戶中的 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ef27-136">Creates an Azure AD application with a self-signed certificate, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="5ef27-137">您可以變更此設定 tooOwner 或任何其他角色。</span><span class="sxs-lookup"><span data-stu-id="5ef27-137">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="5ef27-138">如需詳細資訊，請參閱 [Azure 自動化中的角色型存取控制](automation-role-based-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="5ef27-138">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="5ef27-139">建立名為自動化憑證資產*AzureRunAsCertificate* hello 中指定的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ef27-139">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="5ef27-140">hello 憑證資產會保存 hello 憑證私密金鑰，可由 hello Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5ef27-140">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="5ef27-141">建立名為自動化連線資產*AzureRunAsConnection* hello 中指定的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ef27-141">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="5ef27-142">hello 連線資產會保存 hello applicationId、 tenantId、 subscriptionId、 和憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="5ef27-142">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="5ef27-143">**若為傳統執行身分帳戶：**</span><span class="sxs-lookup"><span data-stu-id="5ef27-143">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="5ef27-144">建立名為自動化憑證資產*AzureClassicRunAsCertificate* hello 中指定的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ef27-144">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="5ef27-145">hello 憑證資產會保存 hello 憑證私密金鑰由 hello 管理憑證。</span><span class="sxs-lookup"><span data-stu-id="5ef27-145">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="5ef27-146">建立名為自動化連線資產*AzureClassicRunAsConnection* hello 中指定的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ef27-146">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="5ef27-147">hello 連線資產包含 hello 訂用帳戶名稱、 訂用帳戶 Id，與憑證資產名稱。</span><span class="sxs-lookup"><span data-stu-id="5ef27-147">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

1. <span data-ttu-id="5ef27-148">登入 toohello hello 訂用帳戶系統管理員角色的成員且 hello 訂用帳戶的共同管理員帳戶的 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="5ef27-148">Sign in toohello Azure portal with an account that is a member of hello Subscription Admins role and co-administrator of hello subscription.</span></span>
2. <span data-ttu-id="5ef27-149">從 hello 自動化帳戶刀鋒視窗中，選取**執行身分帳戶**hello 區段下方**帳戶設定**。</span><span class="sxs-lookup"><span data-stu-id="5ef27-149">From hello Automation account blade, select **Run As Accounts** under hello section **Account Settings**.</span></span>  
3. <span data-ttu-id="5ef27-150">根據您所需的帳戶，選取 [Azure 執行身分帳戶] 或 [Azure 傳統執行身分帳戶]。</span><span class="sxs-lookup"><span data-stu-id="5ef27-150">Depending on which account you require, select either **Azure Run As Account** or **Azure Classic Run As Account**.</span></span>  <span data-ttu-id="5ef27-151">選取任一 hello 之後**新增 Azure 執行身分**或**新增 Azure 傳統執行身分帳戶**刀鋒視窗隨即出現，並檢閱 hello 概觀資訊之後，按一下 **建立**建立執行身分帳戶與 tooproceed。</span><span class="sxs-lookup"><span data-stu-id="5ef27-151">After selecting either hello **Add Azure Run As** or **Add Azure Classic Run As Account** blade appears and after reviewing hello overview information, click **Create** tooproceed with Run As account creation.</span></span>  
4. <span data-ttu-id="5ef27-152">而 Azure 會建立 hello 執行身分帳戶，您可以追蹤下的 hello 進度**通知**hello 從功能表和橫幅顯示，指出正在建立 hello 的帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ef27-152">While Azure creates hello Run As account, you can track hello progress under **Notifications** from hello menu and a banner is displayed stating hello account is being created.</span></span>  <span data-ttu-id="5ef27-153">此程序可能需要幾分鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="5ef27-153">This process can take a few minutes toocomplete.</span></span>  

## <a name="create-run-as-account-using-powershell-script"></a><span data-ttu-id="5ef27-154">使用 PowerShell 指令碼建立執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="5ef27-154">Create Run As account using PowerShell script</span></span>
<span data-ttu-id="5ef27-155">這個 PowerShell 指令碼包含支援的設定 hello:</span><span class="sxs-lookup"><span data-stu-id="5ef27-155">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="5ef27-156">使用自我簽署憑證建立執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ef27-156">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="5ef27-157">使用自我簽署憑證建立執行身分帳戶和傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ef27-157">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="5ef27-158">使用企業憑證建立執行身分帳戶和傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ef27-158">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="5ef27-159">建立執行身分帳戶和傳統執行身分帳戶 hello Azure 政府雲端中使用自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="5ef27-159">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="5ef27-160">視您選取的 hello 組態選項，hello 指令碼會建立 hello 下列項目。</span><span class="sxs-lookup"><span data-stu-id="5ef27-160">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="5ef27-161">**若為執行身分帳戶︰**</span><span class="sxs-lookup"><span data-stu-id="5ef27-161">**For Run As accounts:**</span></span>

* <span data-ttu-id="5ef27-162">建立 Azure AD 應用程式 toobe 匯出以自我簽署的任一個 hello 或企業憑證的公開金鑰，在 Azure AD 中建立 hello 應用程式的服務主體帳戶，並指派 hello hello 帳戶在您目前的參與者角色訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ef27-162">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="5ef27-163">您可以變更此設定 tooOwner 或任何其他角色。</span><span class="sxs-lookup"><span data-stu-id="5ef27-163">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="5ef27-164">如需詳細資訊，請參閱 [Azure 自動化中的角色型存取控制](automation-role-based-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="5ef27-164">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="5ef27-165">建立名為自動化憑證資產*AzureRunAsCertificate* hello 中指定的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ef27-165">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="5ef27-166">hello 憑證資產會保存 hello 憑證私密金鑰，可由 hello Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5ef27-166">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="5ef27-167">建立名為自動化連線資產*AzureRunAsConnection* hello 中指定的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ef27-167">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="5ef27-168">hello 連線資產會保存 hello applicationId、 tenantId、 subscriptionId、 和憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="5ef27-168">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="5ef27-169">**若為傳統執行身分帳戶：**</span><span class="sxs-lookup"><span data-stu-id="5ef27-169">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="5ef27-170">建立名為自動化憑證資產*AzureClassicRunAsCertificate* hello 中指定的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ef27-170">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="5ef27-171">hello 憑證資產會保存 hello 憑證私密金鑰由 hello 管理憑證。</span><span class="sxs-lookup"><span data-stu-id="5ef27-171">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="5ef27-172">建立名為自動化連線資產*AzureClassicRunAsConnection* hello 中指定的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ef27-172">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="5ef27-173">hello 連線資產包含 hello 訂用帳戶名稱、 訂用帳戶 Id，與憑證資產名稱。</span><span class="sxs-lookup"><span data-stu-id="5ef27-173">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="5ef27-174">如果您選取其中一個選項，建立傳統執行身分帳戶，hello 指令碼執行之後上, 傳 hello 公用憑證 （.cer 檔案名稱副檔名） toohello 管理的存放區 hello 訂用帳戶的 hello 自動化帳戶中建立。</span><span class="sxs-lookup"><span data-stu-id="5ef27-174">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

1. <span data-ttu-id="5ef27-175">儲存您的電腦上下列指令碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="5ef27-175">Save hello following script on your computer.</span></span> <span data-ttu-id="5ef27-176">在此範例中，以儲存 hello filename*新增 RunAsAccount.ps1*。</span><span class="sxs-lookup"><span data-stu-id="5ef27-176">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

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
        if (!(($AzureRMProfileVersion.Major -ge 3 -and $AzureRMProfileVersion.Minor -ge 0) -or ($AzureRMProfileVersion.Major -gt 3)))
        {
            Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
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
        $SubscriptionName = $subscription.Subscription.Name
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="5ef27-177">在您的電腦上啟動**Windows PowerShell**從 hello**啟動**螢幕，以提高的使用者權限。</span><span class="sxs-lookup"><span data-stu-id="5ef27-177">On your computer, start **Windows PowerShell** from hello **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="5ef27-178">Hello 從提高權限的命令列殼層，移 toohello 資料夾包含您在步驟 1 中建立的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5ef27-178">From hello elevated command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>  
4. <span data-ttu-id="5ef27-179">您需要的 hello 組態使用 hello 參數值執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5ef27-179">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="5ef27-180">**使用自我簽署憑證建立執行身分帳戶**</span><span class="sxs-lookup"><span data-stu-id="5ef27-180">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="5ef27-181">**使用自我簽署憑證建立執行身分帳戶和傳統執行身分帳戶**</span><span class="sxs-lookup"><span data-stu-id="5ef27-181">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="5ef27-182">**使用企業憑證建立執行身分帳戶和傳統執行身分帳戶**</span><span class="sxs-lookup"><span data-stu-id="5ef27-182">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="5ef27-183">**使用自我簽署的憑證 hello Azure 政府雲端中建立執行身分帳戶和傳統執行身分帳戶**</span><span class="sxs-lookup"><span data-stu-id="5ef27-183">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="5ef27-184">Hello 指令碼執行之後，您將會提示的 tooauthenticate 與 Azure。</span><span class="sxs-lookup"><span data-stu-id="5ef27-184">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="5ef27-185">使用屬於 hello 訂用帳戶系統管理員角色的成員和 hello 訂用帳戶的共同管理員帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="5ef27-185">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="5ef27-186">Hello 指令碼順利執行之後，請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="5ef27-186">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="5ef27-187">如果您使用自我簽署的公開憑證 （.cer 檔案） 建立傳統執行身分帳戶，hello 指令碼建立，並將它 hello 使用者設定檔在電腦上儲存 toohello 暫存檔案資料夾*%USERPROFILE%\AppData\Local\Temp*，使用 tooexecute hello PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="5ef27-187">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="5ef27-188">如果您使用企業公開憑證 (.cer 檔案) 建立了傳統執行身分帳戶，請使用此憑證。</span><span class="sxs-lookup"><span data-stu-id="5ef27-188">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="5ef27-189">請依照指示 hello[上傳 Azure 傳統入口網站管理 API 憑證 toohello](../azure-api-management-certs.md)，並使用 hello 驗證使用傳統部署資源的 hello 認證組態[範例程式碼使用 Azure 傳統部署資源 tooauthenticate](automation-verify-runas-authentication.md#classic-run-as-authentication)。</span><span class="sxs-lookup"><span data-stu-id="5ef27-189">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with classic deployment resources by using hello [sample code tooauthenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="5ef27-190">如果您未*不*建立傳統執行身分帳戶、 向資源管理員資源及驗證 hello 認證組態使用 hello[範例程式碼來驗證服務管理資源](automation-verify-runas-authentication.md#automation-run-as-authentication)。</span><span class="sxs-lookup"><span data-stu-id="5ef27-190">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ef27-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5ef27-191">Next steps</span></span>
* <span data-ttu-id="5ef27-192">如需有關服務主體的詳細資訊，請參閱太[應用程式與服務主體物件](../active-directory/active-directory-application-objects.md)。</span><span class="sxs-lookup"><span data-stu-id="5ef27-192">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="5ef27-193">如需有關憑證和 Azure 服務的詳細資訊，請參閱太[Azure 雲端服務憑證概觀](../cloud-services/cloud-services-certs-create.md)。</span><span class="sxs-lookup"><span data-stu-id="5ef27-193">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
