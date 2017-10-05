---
title: "建立 Azure AD 使用者帳戶 | Microsoft Docs"
description: "本文說明如何在 Azure 自動化中為 Runbook 建立 Azure AD 使用者帳戶認證，以在 Azure 和傳統 Azure 中進行驗證。"
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
ms.openlocfilehash: 4eaa3e36ededddeb5268ec4f49b9daee2f824cee
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="authenticate-runbooks-with-azure-classic-deployment-and-resource-manager"></a><span data-ttu-id="cb23a-104">使用 Azure 傳統部署和 Resource Manager 驗證 Runbook</span><span class="sxs-lookup"><span data-stu-id="cb23a-104">Authenticate Runbooks with Azure classic deployment and Resource Manager</span></span>
<span data-ttu-id="cb23a-105">本文說明要為針對 Azure 傳統部署模型或 Azure Resource Manager 資源執行的 Azure 自動化 Runbook 設定 Azure AD 使用者帳戶，所必須執行的步驟。</span><span class="sxs-lookup"><span data-stu-id="cb23a-105">This article describes the steps you must perform to configure an Azure AD User account for Azure Automation runbooks running against Azure classic deployment model or Azure Resource Manager resources.</span></span>  <span data-ttu-id="cb23a-106">雖然這您的 Azure Resource Manager 型 Runbook 仍然持續支援驗證身分識別，但還是建議您使用 Azure 執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="cb23a-106">While this continues to be a supported authentication identity for your Azure Resource Manager based runbooks, the recommended method is using an Azure Run As account.</span></span>       

## <a name="create-a-new-azure-active-directory-user"></a><span data-ttu-id="cb23a-107">建立新的 Azure Active Directory 使用者</span><span class="sxs-lookup"><span data-stu-id="cb23a-107">Create a new Azure Active Directory user</span></span>
1. <span data-ttu-id="cb23a-108">以您想要管理的 Azure 訂用帳戶服務系統管理員身分登入 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="cb23a-108">Log in to the Azure Classic portal as a service administrator for the Azure subscription you want to manage.</span></span>
2. <span data-ttu-id="cb23a-109">選取 [Active Directory] ，然後選取貴組織目錄的名稱。</span><span class="sxs-lookup"><span data-stu-id="cb23a-109">Select **Active Directory**, and then select the name of your organization directory.</span></span>
3. <span data-ttu-id="cb23a-110">選取 [使用者] 索引標籤，然後在命令區域中選取 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="cb23a-110">Select the **Users** tab, and then, in the command area, select **Add User**.</span></span>
4. <span data-ttu-id="cb23a-111">在 [告訴我們這位使用者] 頁面上，於 [使用者類型] 底下選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="cb23a-111">On the **Tell us about this user** page, under **Type of user**, select **New user in your organization**.</span></span>
5. <span data-ttu-id="cb23a-112">輸入使用者稱。</span><span class="sxs-lookup"><span data-stu-id="cb23a-112">Enter a user name.</span></span>  
6. <span data-ttu-id="cb23a-113">在 [Active Directory] 頁面上選取與您的 Azure 訂用帳戶相關聯的目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="cb23a-113">Select the directory name that is associated with your Azure subscription on the Active Directory page.</span></span>
7. <span data-ttu-id="cb23a-114">在 [使用者設定檔] 頁面上，提供姓氏和名字、使用者易記名稱，並從 [角色] 清單中選擇使用者。</span><span class="sxs-lookup"><span data-stu-id="cb23a-114">On the **user profile** page, provide a first and last name, a user-friendly name, and User from the **Roles** list.</span></span>  <span data-ttu-id="cb23a-115">請勿 [啟用 Multi-Factor Authentication] 。</span><span class="sxs-lookup"><span data-stu-id="cb23a-115">Do not **Enable Multi-Factor Authentication**.</span></span>
8. <span data-ttu-id="cb23a-116">請記下使用者的完整名稱和暫時密碼。</span><span class="sxs-lookup"><span data-stu-id="cb23a-116">Note the user’s full name and temporary password.</span></span>
9. <span data-ttu-id="cb23a-117">選取 [設定] > [系統管理員] > [新增]。</span><span class="sxs-lookup"><span data-stu-id="cb23a-117">Select **Settings > Administrators > Add**.</span></span>
10. <span data-ttu-id="cb23a-118">輸入您所建立之使用者的完整使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="cb23a-118">Type the full user name of the user that you created.</span></span>
11. <span data-ttu-id="cb23a-119">選取您想讓使用者管理的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="cb23a-119">Select the subscription that you want the user to manage.</span></span>
12. <span data-ttu-id="cb23a-120">登出 Azure，然後使用您剛才建立的帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="cb23a-120">Log out of Azure and then log back in with the account you just created.</span></span> <span data-ttu-id="cb23a-121">將提示您變更使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="cb23a-121">You will be prompted to change the user’s password.</span></span>

## <a name="create-an-automation-account-in-azure-classic-portal"></a><span data-ttu-id="cb23a-122">在 Azure 傳統入口網站中建立自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="cb23a-122">Create an Automation account in Azure Classic portal</span></span>
<span data-ttu-id="cb23a-123">在本節中，您會執行下列步驟以在 Azure 入口網站中建立 Azure 自動化帳戶，以便與您用來在 Azure 傳統部署中管理資源的 Runbook 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="cb23a-123">In this section, you perform the following steps to create an Azure Automation account in the Azure portal for use with your runbooks managing resources in Azure classic deployment.</span></span>  

> [!NOTE]
> <span data-ttu-id="cb23a-124">您可以透過 Azure 傳統入口網站和 Azure 入口網站以及任一組 Cmdlet，來管理使用 Azure 傳統入口網站建立的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="cb23a-124">Automation accounts created with the Azure Classic portal can be managed by both the Azure Classic and Azure portal and either set of cmdlets.</span></span> <span data-ttu-id="cb23a-125">帳戶一旦建立，您在帳戶中建立和管理資源的方式就沒有差別。</span><span class="sxs-lookup"><span data-stu-id="cb23a-125">Once the account is created, it makes no difference how you create and manage resources within the account.</span></span> <span data-ttu-id="cb23a-126">如果您打算繼續使用 Azure 傳統入口網站，應該使用它代替 Azure 入口網站來建立任何的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="cb23a-126">If you are planning to continue to use the Azure Classic portal, then you should use it instead of the Azure portal to create any Automation accounts.</span></span>
> 
> 

1. <span data-ttu-id="cb23a-127">以您想要管理的 Azure 訂用帳戶服務系統管理員身分登入 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="cb23a-127">Log in to the Azure Classic portal as a service administrator for the Azure subscription you want to manage.</span></span>
2. <span data-ttu-id="cb23a-128">選取 [自動化] 。</span><span class="sxs-lookup"><span data-stu-id="cb23a-128">Select **Automation**.</span></span>
3. <span data-ttu-id="cb23a-129">在 [自動化] 頁面上，選取 [建立自動化帳戶]。</span><span class="sxs-lookup"><span data-stu-id="cb23a-129">On the **Automation** page, select **Create an Automation Account**.</span></span>
4. <span data-ttu-id="cb23a-130">在 [建立自動化帳戶] 方塊中輸入新的自動化帳戶的名稱，然後在下拉式清單中選取 [區域]。</span><span class="sxs-lookup"><span data-stu-id="cb23a-130">In the **Create an Automation Account** box, type in a name for your new Automation account and select a **Region** from the drop-down list.</span></span>  
5. <span data-ttu-id="cb23a-131">按一下 [確定]  接受您的設定並建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="cb23a-131">Click **OK** to accept your settings and create the account.</span></span>
6. <span data-ttu-id="cb23a-132">帳戶建立之後就會列在 [自動化]  頁面上。</span><span class="sxs-lookup"><span data-stu-id="cb23a-132">After it is created it will be listed on the **Automation** page.</span></span>
7. <span data-ttu-id="cb23a-133">按一下該帳戶，您便會前往 [儀表板] 頁面。</span><span class="sxs-lookup"><span data-stu-id="cb23a-133">Click on the account and it will bring you to the Dashboard page.</span></span>  
8. <span data-ttu-id="cb23a-134">在 [自動化儀表板] 頁面上，選取 [資產] 。</span><span class="sxs-lookup"><span data-stu-id="cb23a-134">On the Automation Dashboard page, select **Assets**.</span></span>
9. <span data-ttu-id="cb23a-135">在 [資產] 頁面上，選取位於頁面底部的 [新增設定]。</span><span class="sxs-lookup"><span data-stu-id="cb23a-135">On the **Assets** page, select **Add Settings** located at the bottom of the page.</span></span>
10. <span data-ttu-id="cb23a-136">在 [新增設定] 頁面上選取 [新增認證]。</span><span class="sxs-lookup"><span data-stu-id="cb23a-136">On the **Add Settings** page, select **Add Credential**.</span></span>
11. <span data-ttu-id="cb23a-137">在 [定義認證] 頁面的 [認證類型] 下拉式清單中選取 [Windows PowerShell 認證]，並提供認證名稱。</span><span class="sxs-lookup"><span data-stu-id="cb23a-137">On the **Define Credential** page, select **Windows PowerShell Credential** from the **Credential Type** drop-down list and provide a name for the credential.</span></span>
12. <span data-ttu-id="cb23a-138">在下列 [定義認證] 頁面中，於 [使用者名稱] 欄位中輸入稍早建立之 AD 使用者帳戶的使用者名稱，並於 [密碼] 和 [確認密碼] 欄位中輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="cb23a-138">On the following **Define Credential** page type in the username of the AD user account created earlier in the **User Name** field and the password in the **Password** and **Confirm Password** fields.</span></span> <span data-ttu-id="cb23a-139">按一下 [確定]  儲存變更。</span><span class="sxs-lookup"><span data-stu-id="cb23a-139">Click **OK** to save your changes.</span></span>

## <a name="create-an-automation-account-in-the-azure-portal"></a><span data-ttu-id="cb23a-140">在 Azure 入口網站中建立自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="cb23a-140">Create an Automation account in the Azure portal</span></span>
<span data-ttu-id="cb23a-141">在本節中，您會執行下列步驟以在 Azure 入口網站中建立 Azure 自動化帳戶，以便與您用來在 Azure Resource Manager 模式中管理資源的 Runbook 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="cb23a-141">In this section, perform the following steps to create an Azure Automation account in the Azure portal for use with your runbooks managing resources in Azure Resource Manager mode.</span></span>  

1. <span data-ttu-id="cb23a-142">以您想要管理的 Azure 訂用帳戶的服務系統管理員身分登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="cb23a-142">Log in to the Azure portal as a service administrator for the Azure subscription you want to manage.</span></span>
2. <span data-ttu-id="cb23a-143">選取 [自動化帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="cb23a-143">Select **Automation Accounts**.</span></span>
3. <span data-ttu-id="cb23a-144">在 [自動化帳戶] 刀鋒視窗中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cb23a-144">In the Automation Accounts blade, click **Add**.</span></span><br><br><span data-ttu-id="cb23a-145">![加入自動化帳戶](media/automation-create-aduser-account/add-automation-acct-properties.png)</span><span class="sxs-lookup"><span data-stu-id="cb23a-145">![Add Automation Account](media/automation-create-aduser-account/add-automation-acct-properties.png)</span></span>
4. <span data-ttu-id="cb23a-146">在 [新增自動化帳戶] 刀鋒視窗的 [名稱] 方塊中，輸入新的自動化帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="cb23a-146">In the **Add Automation Account** blade, in the **Name** box type in a name for your new Automation account.</span></span>
5. <span data-ttu-id="cb23a-147">如果您有多個訂用帳戶，請為新的自動化帳戶指定其中一個訂用帳戶，並指定新的或現有的 [資源群組] 和 Azure 資料中心的 [位置]。</span><span class="sxs-lookup"><span data-stu-id="cb23a-147">If you have more than one subscription, specify the one for the new account, as well as a new or existing **Resource group** and an Azure datacenter **Location**.</span></span>
6. <span data-ttu-id="cb23a-148">在 [建立 Azure 執行身分帳戶] 選項中選取 [是] 這個值，然後按一下 [建立] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cb23a-148">Select the value **Yes** for the **Create Azure Run As account** option, and click the **Create** button.</span></span>  
   
    > [!NOTE]
    > <span data-ttu-id="cb23a-149">如果您選取選項 [否] 以選擇不要建立執行身分帳戶，則會在 [新增自動化帳戶] 刀鋒視窗中看到一則警告訊息。</span><span class="sxs-lookup"><span data-stu-id="cb23a-149">If you choose to not create the Run As account by selecting the option **No**, you will be presented with a warning message in the **Add Automation Account** blade.</span></span>  <span data-ttu-id="cb23a-150">雖然會建立帳戶並將其指派給訂用帳戶中的 [參與者]  角色，但帳戶在訂用帳戶的目錄服務內不會有對應的驗證身分識別，因此在訂用帳戶中沒有存取資源。</span><span class="sxs-lookup"><span data-stu-id="cb23a-150">While the account is created and assigned to the **Contributor** role in the subscription, it will not have a corresponding authentication identity within your subscriptions directory service and therefore, no access resources in your subscription.</span></span>  <span data-ttu-id="cb23a-151">這將導致參考此帳戶的任何 Runbook 無法進行驗證並針對 Azure Resource Manager 資源執行工作。</span><span class="sxs-lookup"><span data-stu-id="cb23a-151">This will prevent any runbooks referencing this account from being able to authenticate and perform tasks against Azure Resource Manager resources.</span></span>
    > 
    >

    <br>![加入自動化帳戶警告](media/automation-create-aduser-account/add-automation-acct-properties-error.png)<br>  
7. <span data-ttu-id="cb23a-153">在 Azure 建立自動化帳戶時，您可以在功能表的 [通知]  底下追蹤進度。</span><span class="sxs-lookup"><span data-stu-id="cb23a-153">While Azure creates the Automation account, you can track the progress under **Notifications** from the menu.</span></span>

<span data-ttu-id="cb23a-154">認證建立完成後，您需要建立一個認證資產，讓自動化帳戶與稍早建立的 AD 使用者帳戶產生關聯。</span><span class="sxs-lookup"><span data-stu-id="cb23a-154">When the creation of the credential is completed, you need to create a Credential Asset to associate the Automation Account with the AD User account created earlier.</span></span>  <span data-ttu-id="cb23a-155">請記住，我們只建立了自動化帳戶，但它並未與驗證身分識別產生關聯。</span><span class="sxs-lookup"><span data-stu-id="cb23a-155">Remember, we only created the Automation account and it is not associated with an authentication identity.</span></span>  <span data-ttu-id="cb23a-156">執行 [Azure 自動化中的認證資產](automation-credentials.md#creating-a-new-credential-asset)一文所述的步驟，並以**網域\使用者**格式輸入 [使用者名稱] 值。</span><span class="sxs-lookup"><span data-stu-id="cb23a-156">Perform the steps outlined in the [Credential assets in Azure Automation article](automation-credentials.md#creating-a-new-credential-asset) and enter the value for **username** in the format **domain\user**.</span></span>

## <a name="use-the-credential-in-a-runbook"></a><span data-ttu-id="cb23a-157">在 Runbook 中使用認證</span><span class="sxs-lookup"><span data-stu-id="cb23a-157">Use the credential in a runbook</span></span>
<span data-ttu-id="cb23a-158">您可以在 Runbook 中使用 [Get-AutomationPSCredential](http://msdn.microsoft.com/library/dn940015.aspx) 活動來擷取認證，然後將它搭配 [Add-AzureAccount](http://msdn.microsoft.com/library/azure/dn722528.aspx) 來連接到您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="cb23a-158">You can retrieve the credential in a runbook using the [Get-AutomationPSCredential](http://msdn.microsoft.com/library/dn940015.aspx) activity and then use it with [Add-AzureAccount](http://msdn.microsoft.com/library/azure/dn722528.aspx) to connect to your Azure subscription.</span></span> <span data-ttu-id="cb23a-159">如果認證是多個 Azure 訂用帳戶的管理員，則您也應該使用 [Select-AzureSubscription](http://msdn.microsoft.com/library/dn495203.aspx) 來指定正確的一個。</span><span class="sxs-lookup"><span data-stu-id="cb23a-159">If the credential is an administrator of multiple Azure subscriptions, then you should also use [Select-AzureSubscription](http://msdn.microsoft.com/library/dn495203.aspx) to specify the correct one.</span></span> <span data-ttu-id="cb23a-160">這會在以下的 Windows PowerShell 範例中顯示，通常會出現在大部分 Azure 自動化 Runbook 的頂端。</span><span class="sxs-lookup"><span data-stu-id="cb23a-160">This is shown in the sample Windows PowerShell below that will typically appear at the top of most Azure Automation runbooks.</span></span>

    $cred = Get-AutomationPSCredential –Name "myuseraccount.onmicrosoft.com"
    Add-AzureAccount –Credential $cred
    Select-AzureSubscription –SubscriptionName "My Subscription"

<span data-ttu-id="cb23a-161">您應該在您的 Runbook 中的任何 [檢查點](http://technet.microsoft.com/library/dn469257.aspx#bk_Checkpoints) 後重複這幾行。</span><span class="sxs-lookup"><span data-stu-id="cb23a-161">You should repeat these lines after any [checkpoints](http://technet.microsoft.com/library/dn469257.aspx#bk_Checkpoints) in your runbook.</span></span> <span data-ttu-id="cb23a-162">如果 Runbook 暫止然後在另一個背景工作上繼續執行，則它必須重新執行驗證。</span><span class="sxs-lookup"><span data-stu-id="cb23a-162">If the runbook is suspended and then resumes on another worker, then it will need to perform the authentication again.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb23a-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cb23a-163">Next Steps</span></span>
* <span data-ttu-id="cb23a-164">在接下來的 [Azure 自動化 Runbook 類型](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="cb23a-164">Review the different runbook types and steps for creating your own runbooks from the following article [Azure Automation runbook types](automation-runbook-types.md)</span></span>

