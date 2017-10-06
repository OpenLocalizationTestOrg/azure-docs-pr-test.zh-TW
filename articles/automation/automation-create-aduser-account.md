---
title: "Azure AD 使用者帳戶 aaaCreate |Microsoft 文件"
description: "本文說明 toocreate Azure AD 使用者帳戶的 runbook 在 Azure 自動化 tooauthenticate Azure 和傳統 Azure 中的認證。"
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
keywords: "azure active directory 使用者, azure 服務管理, azure ad 使用者帳戶"
ms.assetid: fcfe266d-b22e-4dfb-8272-adcab09fc0cf
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 7c6ed4182dbab074d0bc5da7057f74ad321d8884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-azure-classic-deployment-and-resource-manager"></a><span data-ttu-id="c9a2d-104">使用 Azure 傳統部署和 Resource Manager 驗證 Runbook</span><span class="sxs-lookup"><span data-stu-id="c9a2d-104">Authenticate Runbooks with Azure classic deployment and Resource Manager</span></span>
<span data-ttu-id="c9a2d-105">本文將告訴您必須執行 tooconfigure Azure AD 使用者帳戶的 Azure 傳統部署模型或 Azure 資源管理員資源上執行的 Azure 自動化 runbook 的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-105">This article describes hello steps you must perform tooconfigure an Azure AD User account for Azure Automation runbooks running against Azure classic deployment model or Azure Resource Manager resources.</span></span>  <span data-ttu-id="c9a2d-106">Toobe 然後繼續進行時支援的驗證身分識別您 Azure 資源管理員的基礎 runbook、 hello 建議的方法使用 Azure 執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-106">While this continues toobe a supported authentication identity for your Azure Resource Manager based runbooks, hello recommended method is using an Azure Run As account.</span></span>       

## <a name="create-a-new-azure-active-directory-user"></a><span data-ttu-id="c9a2d-107">建立新的 Azure Active Directory 使用者</span><span class="sxs-lookup"><span data-stu-id="c9a2d-107">Create a new Azure Active Directory user</span></span>
1. <span data-ttu-id="c9a2d-108">Hello 想 toomanage 的 Azure 訂用帳戶的服務系統管理員身分登入 toohello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-108">Log in toohello Azure Classic portal as a service administrator for hello Azure subscription you want toomanage.</span></span>
2. <span data-ttu-id="c9a2d-109">選取**Active Directory**，然後選取您的組織目錄中的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-109">Select **Active Directory**, and then select hello name of your organization directory.</span></span>
3. <span data-ttu-id="c9a2d-110">選取 hello**使用者**索引標籤，然後在 hello 命令區域中，選取**新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-110">Select hello **Users** tab, and then, in hello command area, select **Add User**.</span></span>
4. <span data-ttu-id="c9a2d-111">在 hello**告訴我們這位使用者**頁面的 **使用者類型**，選取**您組織中的新使用者**。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-111">On hello **Tell us about this user** page, under **Type of user**, select **New user in your organization**.</span></span>
5. <span data-ttu-id="c9a2d-112">輸入使用者稱。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-112">Enter a user name.</span></span>  
6. <span data-ttu-id="c9a2d-113">選取您在 hello Active Directory 頁面上的 Azure 訂用帳戶相關聯的 hello 目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-113">Select hello directory name that is associated with your Azure subscription on hello Active Directory page.</span></span>
7. <span data-ttu-id="c9a2d-114">在 hello**使用者設定檔**頁面上，提供第一個和最後一個名稱、 使用者易記的名稱，與使用者從 hello**角色**清單。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-114">On hello **user profile** page, provide a first and last name, a user-friendly name, and User from hello **Roles** list.</span></span>  <span data-ttu-id="c9a2d-115">請勿 [啟用 Multi-Factor Authentication] 。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-115">Do not **Enable Multi-Factor Authentication**.</span></span>
8. <span data-ttu-id="c9a2d-116">請注意 hello 使用者的完整名稱和暫時密碼。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-116">Note hello user’s full name and temporary password.</span></span>
9. <span data-ttu-id="c9a2d-117">選取 [設定] > [系統管理員] > [新增]。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-117">Select **Settings > Administrators > Add**.</span></span>
10. <span data-ttu-id="c9a2d-118">輸入您所建立的 hello 使用者 hello 完整使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-118">Type hello full user name of hello user that you created.</span></span>
11. <span data-ttu-id="c9a2d-119">選取您想 hello 使用者 toomanage hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-119">Select hello subscription that you want hello user toomanage.</span></span>
12. <span data-ttu-id="c9a2d-120">登出 Azure，然後重新登入您剛建立的 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-120">Log out of Azure and then log back in with hello account you just created.</span></span> <span data-ttu-id="c9a2d-121">您將會提示的 toochange hello 使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-121">You will be prompted toochange hello user’s password.</span></span>

## <a name="create-an-automation-account-in-azure-classic-portal"></a><span data-ttu-id="c9a2d-122">在 Azure 傳統入口網站中建立自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="c9a2d-122">Create an Automation account in Azure Classic portal</span></span>
<span data-ttu-id="c9a2d-123">在本節中，您可以執行 hello 遵循步驟 toocreate hello 使用 Azure 入口網站中的 Azure 自動化帳戶與您管理在 Azure 傳統部署資源的 runbook。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-123">In this section, you perform hello following steps toocreate an Azure Automation account in hello Azure portal for use with your runbooks managing resources in Azure classic deployment.</span></span>  

> [!NOTE]
> <span data-ttu-id="c9a2d-124">以 hello Azure 傳統入口網站建立的自動化帳戶可以管理由 Azure 傳統 hello 和 Azure 入口網站和其中的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-124">Automation accounts created with hello Azure Classic portal can be managed by both hello Azure Classic and Azure portal and either set of cmdlets.</span></span> <span data-ttu-id="c9a2d-125">一旦建立 hello 帳戶，並沒有差別如何建立及管理 hello 帳戶內的資源。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-125">Once hello account is created, it makes no difference how you create and manage resources within hello account.</span></span> <span data-ttu-id="c9a2d-126">如果您打算 toocontinue toouse hello Azure 傳統入口網站，則您應該使用，而不是 hello Azure 入口網站 toocreate 任何自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-126">If you are planning toocontinue toouse hello Azure Classic portal, then you should use it instead of hello Azure portal toocreate any Automation accounts.</span></span>
> 
> 

1. <span data-ttu-id="c9a2d-127">Hello 想 toomanage 的 Azure 訂用帳戶的服務系統管理員身分登入 toohello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-127">Log in toohello Azure Classic portal as a service administrator for hello Azure subscription you want toomanage.</span></span>
2. <span data-ttu-id="c9a2d-128">選取 [自動化] 。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-128">Select **Automation**.</span></span>
3. <span data-ttu-id="c9a2d-129">在 hello**自動化**頁面上，選取**建立自動化帳戶**。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-129">On hello **Automation** page, select **Create an Automation Account**.</span></span>
4. <span data-ttu-id="c9a2d-130">在 hello**建立自動化帳戶**，輸入新的自動化帳戶的名稱，然後選取**區域**hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-130">In hello **Create an Automation Account** box, type in a name for your new Automation account and select a **Region** from hello drop-down list.</span></span>  
5. <span data-ttu-id="c9a2d-131">按一下**確定**tooaccept 您的設定，並建立 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-131">Click **OK** tooaccept your settings and create hello account.</span></span>
6. <span data-ttu-id="c9a2d-132">建立之後，它就會列在 hello**自動化**頁面。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-132">After it is created it will be listed on hello **Automation** page.</span></span>
7. <span data-ttu-id="c9a2d-133">按一下 hello 帳戶，它會使您 toohello 儀表板頁面。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-133">Click on hello account and it will bring you toohello Dashboard page.</span></span>  
8. <span data-ttu-id="c9a2d-134">在 hello 自動化儀表板 頁面上，選取 **資產**。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-134">On hello Automation Dashboard page, select **Assets**.</span></span>
9. <span data-ttu-id="c9a2d-135">在 hello**資產**頁面上，選取**加入設定**位於 hello hello 頁面的底部。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-135">On hello **Assets** page, select **Add Settings** located at hello bottom of hello page.</span></span>
10. <span data-ttu-id="c9a2d-136">在 hello**加入設定**頁面上，選取**Add Credential**。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-136">On hello **Add Settings** page, select **Add Credential**.</span></span>
11. <span data-ttu-id="c9a2d-137">在 hello**定義認證**頁面上，選取**Windows PowerShell 認證**從 hello**認證類型**下拉式清單，並提供 hello 認證的名稱。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-137">On hello **Define Credential** page, select **Windows PowerShell Credential** from hello **Credential Type** drop-down list and provide a name for hello credential.</span></span>
12. <span data-ttu-id="c9a2d-138">在 hello 下列**定義認證** 頁面中輸入的 hello 密碼 hello AD 使用者帳戶在 hello 稍早建立的**使用者名**hello 中的欄位和 hello 密碼**密碼**和**確認密碼**欄位。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-138">On hello following **Define Credential** page type in hello username of hello AD user account created earlier in hello **User Name** field and hello password in hello **Password** and **Confirm Password** fields.</span></span> <span data-ttu-id="c9a2d-139">按一下**確定**toosave 您的變更。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-139">Click **OK** toosave your changes.</span></span>

## <a name="create-an-automation-account-in-hello-azure-portal"></a><span data-ttu-id="c9a2d-140">在 hello Azure 入口網站中建立自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="c9a2d-140">Create an Automation account in hello Azure portal</span></span>
<span data-ttu-id="c9a2d-141">本節中，執行下列步驟 toocreate hello 使用 Azure 入口網站中的 Azure 自動化帳戶與您管理 Azure Resource Manager 模式中的資源的 runbook 的 hello。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-141">In this section, perform hello following steps toocreate an Azure Automation account in hello Azure portal for use with your runbooks managing resources in Azure Resource Manager mode.</span></span>  

1. <span data-ttu-id="c9a2d-142">以登入 toohello Azure 入口網站 hello 想 toomanage 的 Azure 訂用帳戶的服務系統管理員。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-142">Log in toohello Azure portal as a service administrator for hello Azure subscription you want toomanage.</span></span>
2. <span data-ttu-id="c9a2d-143">選取 [自動化帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-143">Select **Automation Accounts**.</span></span>
3. <span data-ttu-id="c9a2d-144">在 hello 自動化帳戶刀鋒視窗中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-144">In hello Automation Accounts blade, click **Add**.</span></span><br><br><span data-ttu-id="c9a2d-145">![加入自動化帳戶](media/automation-create-aduser-account/add-automation-acct-properties.png)</span><span class="sxs-lookup"><span data-stu-id="c9a2d-145">![Add Automation Account](media/automation-create-aduser-account/add-automation-acct-properties.png)</span></span>
4. <span data-ttu-id="c9a2d-146">在 hello**加入自動化帳戶**刀鋒視窗中的，在 hello**名稱**方塊中，輸入新的自動化帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-146">In hello **Add Automation Account** blade, in hello **Name** box type in a name for your new Automation account.</span></span>
5. <span data-ttu-id="c9a2d-147">如果您有多個訂閱，指定 hello 新帳戶，以及新的其中一個 hello 或現有的**資源群組**和 Azure 資料中心**位置**。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-147">If you have more than one subscription, specify hello one for hello new account, as well as a new or existing **Resource group** and an Azure datacenter **Location**.</span></span>
6. <span data-ttu-id="c9a2d-148">選取 hello 值**是**hello**建立 Azure 執行身分帳戶**選項，然後按一下 hello**建立** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-148">Select hello value **Yes** for hello **Create Azure Run As account** option, and click hello **Create** button.</span></span>  
   
    > [!NOTE]
    > <span data-ttu-id="c9a2d-149">如果您選擇 toonot hello 執行身分帳戶選取 hello 選項建立**否**，您會看到一則警告訊息中 hello 與**加入自動化帳戶**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-149">If you choose toonot create hello Run As account by selecting hello option **No**, you will be presented with a warning message in hello **Add Automation Account** blade.</span></span>  <span data-ttu-id="c9a2d-150">雖然 hello 帳戶建立並指派 toohello**參與者**角色在 hello 訂用帳戶，不會有對應的驗證識別身分，在您的訂用帳戶目錄服務，因此，沒有存取權您的訂用帳戶中的資源。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-150">While hello account is created and assigned toohello **Contributor** role in hello subscription, it will not have a corresponding authentication identity within your subscriptions directory service and therefore, no access resources in your subscription.</span></span>  <span data-ttu-id="c9a2d-151">這會防止任何從正在 tooauthenticate 可以參考此帳戶的 runbook，並執行對 Azure 資源管理員資源的工作。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-151">This will prevent any runbooks referencing this account from being able tooauthenticate and perform tasks against Azure Resource Manager resources.</span></span>
    > 
    >

    <br>![加入自動化帳戶警告](media/automation-create-aduser-account/add-automation-acct-properties-error.png)<br>  
7. <span data-ttu-id="c9a2d-153">而 Azure 會建立 hello 自動化帳戶，您可以追蹤在 hello 進度**通知**hello 功能表。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-153">While Azure creates hello Automation account, you can track hello progress under **Notifications** from hello menu.</span></span>

<span data-ttu-id="c9a2d-154">Hello hello 認證建立完成後，您會需要的 toocreate 稍早建立認證資產 tooassociate hello 自動化帳戶以 hello AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-154">When hello creation of hello credential is completed, you need toocreate a Credential Asset tooassociate hello Automation Account with hello AD User account created earlier.</span></span>  <span data-ttu-id="c9a2d-155">請記住，我們只建立 hello 自動化帳戶並不是與驗證身分識別相關聯。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-155">Remember, we only created hello Automation account and it is not associated with an authentication identity.</span></span>  <span data-ttu-id="c9a2d-156">Hello 中所述步驟 hello[認證 Azure 自動化文件中的資產](automation-credentials.md#creating-a-new-credential-asset)，然後輸入 hello 值**username** hello 格式**網域 \ 使用者**。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-156">Perform hello steps outlined in hello [Credential assets in Azure Automation article](automation-credentials.md#creating-a-new-credential-asset) and enter hello value for **username** in hello format **domain\user**.</span></span>

## <a name="use-hello-credential-in-a-runbook"></a><span data-ttu-id="c9a2d-157">在 runbook 中使用 hello 認證</span><span class="sxs-lookup"><span data-stu-id="c9a2d-157">Use hello credential in a runbook</span></span>
<span data-ttu-id="c9a2d-158">您可以擷取使用 hello runbook 中的 hello 認證[Get-automationpscredential](http://msdn.microsoft.com/library/dn940015.aspx)活動，然後使用它與[Add-azureaccount](http://msdn.microsoft.com/library/azure/dn722528.aspx) tooconnect tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-158">You can retrieve hello credential in a runbook using hello [Get-AutomationPSCredential](http://msdn.microsoft.com/library/dn940015.aspx) activity and then use it with [Add-AzureAccount](http://msdn.microsoft.com/library/azure/dn722528.aspx) tooconnect tooyour Azure subscription.</span></span> <span data-ttu-id="c9a2d-159">如果 hello 認證是系統管理員的多個 Azure 訂用帳戶，則您也應該使用[Select-azuresubscription](http://msdn.microsoft.com/library/dn495203.aspx) toospecify hello 正確。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-159">If hello credential is an administrator of multiple Azure subscriptions, then you should also use [Select-AzureSubscription](http://msdn.microsoft.com/library/dn495203.aspx) toospecify hello correct one.</span></span> <span data-ttu-id="c9a2d-160">這通常會出現在大多數 Azure 自動化 runbook 的 hello 頂端的 hello 範例下列 Windows PowerShell 中顯示。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-160">This is shown in hello sample Windows PowerShell below that will typically appear at hello top of most Azure Automation runbooks.</span></span>

    $cred = Get-AutomationPSCredential –Name "myuseraccount.onmicrosoft.com"
    Add-AzureAccount –Credential $cred
    Select-AzureSubscription –SubscriptionName "My Subscription"

<span data-ttu-id="c9a2d-161">您應該在您的 Runbook 中的任何 [檢查點](http://technet.microsoft.com/library/dn469257.aspx#bk_Checkpoints) 後重複這幾行。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-161">You should repeat these lines after any [checkpoints](http://technet.microsoft.com/library/dn469257.aspx#bk_Checkpoints) in your runbook.</span></span> <span data-ttu-id="c9a2d-162">如果 hello runbook 已暫停，然後繼續在另一個背景工作上，它將需要再次 tooperform hello 驗證。</span><span class="sxs-lookup"><span data-stu-id="c9a2d-162">If hello runbook is suspended and then resumes on another worker, then it will need tooperform hello authentication again.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9a2d-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c9a2d-163">Next Steps</span></span>
* <span data-ttu-id="c9a2d-164">檢閱 hello 不同的 runbook 類型和建立您自己的 runbook 從步驟 hello 下列文章[Azure 自動化 runbook 類型](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="c9a2d-164">Review hello different runbook types and steps for creating your own runbooks from hello following article [Azure Automation runbook types](automation-runbook-types.md)</span></span>

