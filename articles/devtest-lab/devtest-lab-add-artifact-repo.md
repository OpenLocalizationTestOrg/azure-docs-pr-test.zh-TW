---
title: "將 Git存放庫加入 Azure DevTest Labs 中的實驗室 | Microsoft Docs"
description: "將適用於自訂構件來源的 GitHub 或 Visual Studio Team Services Git 儲存機制加入 Azure DevTest Labs"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 01b459f7-eaf2-45a8-b4b5-2c0a821b33c8
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 053f92a65f9ae29154d471fd22ee842620b4f273
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="add-a-git-repository-to-store-custom-artifacts-and-azure-resource-manager-templates"></a><span data-ttu-id="196a2-103">新增可以存放自訂構件和 Azure Resource Manager 範本的 Git 存放庫</span><span class="sxs-lookup"><span data-stu-id="196a2-103">Add a Git repository to store custom artifacts and Azure Resource Manager templates</span></span>

<span data-ttu-id="196a2-104">如果您想要在實驗室中為 VM [建立自訂構件](devtest-lab-artifact-author.md)，或[使用 Azure Resource Manager 範本來建立自訂的測試環境](devtest-lab-create-environment-from-arm.md)，您必須新增 Git 存放庫，來容納您的團隊建立的構件或 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="196a2-104">If you want to [create custom artifacts](devtest-lab-artifact-author.md) for the VMs in your lab, or [use Azure Resource Manager templates to create a custom test environment](devtest-lab-create-environment-from-arm.md), you must also add a private Git repository to include the artifacts or Azure Resource Manager templates that your team creates.</span></span> <span data-ttu-id="196a2-105">儲存機制可以裝載在 [GitHub](https://github.com) 或 [Visual Studio Team Services (VSTS)](https://visualstudio.com) 上。</span><span class="sxs-lookup"><span data-stu-id="196a2-105">The repository can be hosted on [GitHub](https://github.com) or on [Visual Studio Team Services (VSTS)](https://visualstudio.com).</span></span>

<span data-ttu-id="196a2-106">我們提供[構件的 Github 存放庫](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts)，您可以為您的實驗室依原樣部署為自行自訂。</span><span class="sxs-lookup"><span data-stu-id="196a2-106">We have provided a [Github repository of artifacts](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts) that you can deploy as-is or customize for your labs.</span></span> <span data-ttu-id="196a2-107">自訂或建立構件時，您無法將構件儲存在公共存放庫中，您必須建立自己的私人存放庫。</span><span class="sxs-lookup"><span data-stu-id="196a2-107">When you customize or create an artifact, you cannot store them in the public repository – you must create your own private repo.</span></span> 

<span data-ttu-id="196a2-108">建立 VM 時，您可以儲存 Azure Resource Manager 範本，並依您的需求自訂，並在稍後使用範本來更輕易地建立更多 VM。</span><span class="sxs-lookup"><span data-stu-id="196a2-108">When you create a VM, you can save the Azure Resource Manager template, customize it if you want, and then use it later to easily create more VMs.</span></span> <span data-ttu-id="196a2-109">您必須建立您自己的私人存放庫，來儲存您自訂的 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="196a2-109">You must create your own private repository to store your custom Azure Resource Manager templates.</span></span>  

* <span data-ttu-id="196a2-110">若要了解如何建立 GitHub 儲存機制，請參閱 [GitHub Bootcamp](https://help.github.com/categories/bootcamp/)。</span><span class="sxs-lookup"><span data-stu-id="196a2-110">To learn how to create a GitHub repository, see [GitHub Bootcamp](https://help.github.com/categories/bootcamp/).</span></span>
* <span data-ttu-id="196a2-111">若要了解如何使用 Git 儲存機制建立 Team Services 專案，請參閱 [連接到 Visual Studio Team Services](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online)。</span><span class="sxs-lookup"><span data-stu-id="196a2-111">To learn how to create a Team Services project with a Git Repository, see [Connect to Visual Studio Team Services](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online).</span></span>

<span data-ttu-id="196a2-112">下列螢幕擷取畫面顯示包含構件的儲存機制在 GitHub 中的可能外觀範例：</span><span class="sxs-lookup"><span data-stu-id="196a2-112">The following screen shot shows an example of how a repository containing artifacts might look in GitHub:</span></span>  
![GitHub 構件儲存機制範例](./media/devtest-lab-add-repo/devtestlab-github-artifact-repo-home.png)

## <a name="get-the-repository-information-and-credentials"></a><span data-ttu-id="196a2-114">取得儲存機制資訊和認證</span><span class="sxs-lookup"><span data-stu-id="196a2-114">Get the repository information and credentials</span></span>
<span data-ttu-id="196a2-115">若要將存放庫加入您的實驗室，您必須先從存放庫取得特定資訊。</span><span class="sxs-lookup"><span data-stu-id="196a2-115">To add a repository to your lab, you must first get certain information from your repository.</span></span> <span data-ttu-id="196a2-116">下列各節會引導您取得 GitHub 與 Visual Studio Team Services 上裝載的儲存庫資訊。</span><span class="sxs-lookup"><span data-stu-id="196a2-116">The following sections guide you through getting this information for repositories hosted on GitHub and Visual Studio Team Services.</span></span>

### <a name="get-the-github-repository-clone-url-and-personal-access-token"></a><span data-ttu-id="196a2-117">取得 GitHub 儲存機制複製 URL 和個人存取權杖</span><span class="sxs-lookup"><span data-stu-id="196a2-117">Get the GitHub repository clone URL and personal access token</span></span>
<span data-ttu-id="196a2-118">若要取得 GitHub 儲存機制複製 URL 和個人存取權杖，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="196a2-118">To get the GitHub repository clone URL and personal access token, follow these steps:</span></span>

1. <span data-ttu-id="196a2-119">瀏覽至包含構件或 Azure Resource Manager 範本定義的 GitHub 儲存庫首頁。</span><span class="sxs-lookup"><span data-stu-id="196a2-119">Browse to the home page of the GitHub repository that contains the artifact or Azure Resource Manager template definitions.</span></span>
2. <span data-ttu-id="196a2-120">選取 [複製或下載] 。</span><span class="sxs-lookup"><span data-stu-id="196a2-120">Select **Clone or download**.</span></span>
3. <span data-ttu-id="196a2-121">選取將 **HTTPS 複製 URL** 複製到剪貼簿的按鈕，並儲存該 URL 供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="196a2-121">Select the button to copy the **HTTPS clone url** to the clipboard, and save the URL for later use.</span></span>
4. <span data-ttu-id="196a2-122">選取 GitHub 右上角的設定檔影像，然後選取 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="196a2-122">Select the profile image in the upper-right corner of GitHub, and select **Settings**.</span></span>
5. <span data-ttu-id="196a2-123">在左側的 [個人設定] 功能表上，選取 [個人存取權杖]。</span><span class="sxs-lookup"><span data-stu-id="196a2-123">In the **Personal settings** menu on the left, select **Personal access tokens**.</span></span>
6. <span data-ttu-id="196a2-124">選取 [產生新的權杖] 。</span><span class="sxs-lookup"><span data-stu-id="196a2-124">Select **Generate new token**.</span></span>
7. <span data-ttu-id="196a2-125">在 [新增個人存取權杖] 頁面上，輸入 [權杖描述]、接受 [選取範圍] 中的預設項目，然後選擇 [產生權杖]。</span><span class="sxs-lookup"><span data-stu-id="196a2-125">On the **New personal access token** page, enter a **Token description**, accept the default items in the **Select scopes**, and then choose **Generate Token**.</span></span>
8. <span data-ttu-id="196a2-126">儲存產生的權杖，因為您稍後需要用到。</span><span class="sxs-lookup"><span data-stu-id="196a2-126">Save the generated token as you need it later.</span></span>
9. <span data-ttu-id="196a2-127">您現在可以關閉 GitHub。</span><span class="sxs-lookup"><span data-stu-id="196a2-127">You can close GitHub now.</span></span>   
10. <span data-ttu-id="196a2-128">繼續 [將您的實驗室連接至存放庫](#connect-your-lab-to-the-repository) 一節。</span><span class="sxs-lookup"><span data-stu-id="196a2-128">Continue to the [Connect your lab to the repository](#connect-your-lab-to-the-repository) section.</span></span>

### <a name="get-the-visual-studio-team-services-repository-clone-url-and-personal-access-token"></a><span data-ttu-id="196a2-129">取得 Visual Studio Team Services 儲存機制複製 URL 和個人存取權杖</span><span class="sxs-lookup"><span data-stu-id="196a2-129">Get the Visual Studio Team Services repository clone URL and personal access token</span></span>
<span data-ttu-id="196a2-130">若要取得 Visual Studio Team Services 儲存機制複製 URL 和個人存取權杖，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="196a2-130">To get the Visual Studio Team Services repository clone URL and personal access token, follow these steps:</span></span>

1. <span data-ttu-id="196a2-131">開啟您的小組集合首頁 (例如 `https://contoso-web-team.visualstudio.com`)，然後選取專案。</span><span class="sxs-lookup"><span data-stu-id="196a2-131">Open the home page of your team collection (for example, `https://contoso-web-team.visualstudio.com`), and then select your project.</span></span>
2. <span data-ttu-id="196a2-132">在專案首頁上，選取 [程式碼] 。</span><span class="sxs-lookup"><span data-stu-id="196a2-132">On the project home page, select **Code**.</span></span>
3. <span data-ttu-id="196a2-133">若要檢視複製 URL，可在專案 [程式碼] 頁面上，選取 [複製]。</span><span class="sxs-lookup"><span data-stu-id="196a2-133">To view the clone URL, on the project **Code** page, select **Clone**.</span></span>
4. <span data-ttu-id="196a2-134">儲存 URL，因為在本教學課程稍後將需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="196a2-134">Save the URL as you need it later in this tutorial.</span></span>
5. <span data-ttu-id="196a2-135">若要建立個人存取權杖，可從使用者帳戶下拉式功能表中選取 [我的設定檔]  。</span><span class="sxs-lookup"><span data-stu-id="196a2-135">To create a Personal Access Token, select **My profile** from the user account drop-down menu.</span></span>
6. <span data-ttu-id="196a2-136">在 [設定檔資訊] 頁面上，選取 [安全性] 。</span><span class="sxs-lookup"><span data-stu-id="196a2-136">On the profile information page, select **Security**.</span></span>
7. <span data-ttu-id="196a2-137">在 [安全性] 索引標籤上，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="196a2-137">On the **Security** tab, select **Add**.</span></span>
8. <span data-ttu-id="196a2-138">在 [建立個人存取權杖]  頁面中：</span><span class="sxs-lookup"><span data-stu-id="196a2-138">In the **Create a personal access token** page:</span></span>

   * <span data-ttu-id="196a2-139">輸入權杖的 **描述** 。</span><span class="sxs-lookup"><span data-stu-id="196a2-139">Enter a **Description** for the token.</span></span>
   * <span data-ttu-id="196a2-140">從 [到期日] 清單中選取 [180 天]。</span><span class="sxs-lookup"><span data-stu-id="196a2-140">Select **180 days** from the **Expires In** list.</span></span>
   * <span data-ttu-id="196a2-141">從 [帳戶] 清單中選擇 [所有可存取的帳戶]。</span><span class="sxs-lookup"><span data-stu-id="196a2-141">Choose **All accessible accounts** from the **Accounts** list.</span></span>
   * <span data-ttu-id="196a2-142">選擇 [所有範圍]  選項。</span><span class="sxs-lookup"><span data-stu-id="196a2-142">Choose the **All scopes** option.</span></span>
   * <span data-ttu-id="196a2-143">選擇 [建立權杖] 。</span><span class="sxs-lookup"><span data-stu-id="196a2-143">Choose **Create Token**.</span></span>
9. <span data-ttu-id="196a2-144">完成時，新的權杖會出現在 [個人存取權杖]  清單中。</span><span class="sxs-lookup"><span data-stu-id="196a2-144">When finished, the new token appears in the **Personal Access Tokens** list.</span></span> <span data-ttu-id="196a2-145">選取 [複製權杖] ，然後儲存權杖值供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="196a2-145">Select **Copy Token**, and then save the token value for later use.</span></span>
10. <span data-ttu-id="196a2-146">繼續 [將您的實驗室連接至存放庫](#connect-your-lab-to-the-repository) 一節。</span><span class="sxs-lookup"><span data-stu-id="196a2-146">Continue to the [Connect your lab to the repository](#connect-your-lab-to-the-repository) section.</span></span>

## <a name="connect-your-lab-to-the-repository"></a><span data-ttu-id="196a2-147">將實驗室連接至存放庫</span><span class="sxs-lookup"><span data-stu-id="196a2-147">Connect your lab to the repository</span></span>
1. <span data-ttu-id="196a2-148">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="196a2-148">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="196a2-149">選取 [更多服務]，然後從清單中選取 [DevTest Labs]。</span><span class="sxs-lookup"><span data-stu-id="196a2-149">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="196a2-150">從實驗室清單中，選取所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="196a2-150">From the list of labs, select the desired lab.</span></span>   
4. <span data-ttu-id="196a2-151">在左窗格中，選取 [組態和原則]。</span><span class="sxs-lookup"><span data-stu-id="196a2-151">On the left panel, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="196a2-152">在實驗室的 [組態和原則] 區域上，選取 [存放庫]。</span><span class="sxs-lookup"><span data-stu-id="196a2-152">On the lab's **Configuration and policies** area, select **Repositories**.</span></span>
6. <span data-ttu-id="196a2-153">在 [存放庫] 區域上，選取 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="196a2-153">On the **Repositories** area, select **+ Add**.</span></span>

    ![[新增存放庫] 按鈕](./media/devtest-lab-add-repo/devtestlab-add-repo.png)
7. <span data-ttu-id="196a2-155">在第二個 [存放庫] 頁面上，指定下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="196a2-155">On the second **Repositories** page, specify the following information:</span></span>

   * <span data-ttu-id="196a2-156">**名稱** - 輸入儲存機制的名稱。</span><span class="sxs-lookup"><span data-stu-id="196a2-156">**Name** - Enter a name for the repository.</span></span>
   * <span data-ttu-id="196a2-157">**Git 複製 URL** - 輸入您先前從 GitHub 或 Visual Studio Team Services 複製的 Git HTTPS 複製 URL。</span><span class="sxs-lookup"><span data-stu-id="196a2-157">**Git Clone Url** - Enter the Git HTTPS clone URL that you copied earlier from either GitHub or Visual Studio Team Services.</span></span>
   * <span data-ttu-id="196a2-158">分支 - 輸入取得定義的分支。</span><span class="sxs-lookup"><span data-stu-id="196a2-158">**Branch** - Enter the branch to get your definitions.</span></span>
   * <span data-ttu-id="196a2-159">**個人存取權杖** - 輸入您先前從 GitHub 或 Visual Studio Team Services 取得的個人存取權杖。</span><span class="sxs-lookup"><span data-stu-id="196a2-159">**Personal Access Token** - Enter the personal access token you obtained earlier from either GitHub or Visual Studio Team Services.</span></span>
   * <span data-ttu-id="196a2-160">資料夾路徑 - 輸入至少與複製 URL 相關的一個資料夾路徑，其中包含構件或 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="196a2-160">**Folder Paths** - Enter at least one folder path relative to the clone URL that contains your artifact or Azure Resource Manager template definitions.</span></span> <span data-ttu-id="196a2-161">指定子目錄時，請確定資料夾路徑中包含斜線。</span><span class="sxs-lookup"><span data-stu-id="196a2-161">When specifying a subdirectory, make sure to include the forward slash in the folder path.</span></span>

     ![存放庫區域](./media/devtest-lab-add-repo/devtestlab-repo-blade.png)
8. <span data-ttu-id="196a2-163">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="196a2-163">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="196a2-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="196a2-164">Next steps</span></span>
<span data-ttu-id="196a2-165">建立私人 Git 存放庫之後，您可以執行下列一或兩個動作，視您的需求而定︰</span><span class="sxs-lookup"><span data-stu-id="196a2-165">After you have created your private Git repository, you can do one or both of the following, depending on your needs:</span></span>
* <span data-ttu-id="196a2-166">儲存您的 [自訂構件](devtest-lab-artifact-author.md)，您可以在稍後用來建立新的 VM。</span><span class="sxs-lookup"><span data-stu-id="196a2-166">Store your [custom artifacts](devtest-lab-artifact-author.md), which you can use later to create new VMs.</span></span>
* <span data-ttu-id="196a2-167">[透過 Azure Resource Manager 範本建立多個 VM 環境和 PaaS 資源](devtest-lab-create-environment-from-arm.md)，並將範本儲存在您的私人存放庫。</span><span class="sxs-lookup"><span data-stu-id="196a2-167">[Create multi-VM environments and PaaS resources with Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md) and then store the templates in your private repo.</span></span>

<span data-ttu-id="196a2-168">建立 VM 時，您可以確認構件或範本已新增至 Git存放庫。</span><span class="sxs-lookup"><span data-stu-id="196a2-168">When you create a VM, you can verify that the artifacts or templates are added to your Git repository.</span></span> <span data-ttu-id="196a2-169">它們會立即出現在構件或範本清單，您的私人存放庫名稱會顯示在欄位中，藉此顯示其來源。</span><span class="sxs-lookup"><span data-stu-id="196a2-169">They are available immediately in the list of artifacts or templates, with the name of your private repo shown in the column that specifies the source.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="related-blog-posts"></a><span data-ttu-id="196a2-170">相關部落格文章</span><span class="sxs-lookup"><span data-stu-id="196a2-170">Related blog posts</span></span>
* [<span data-ttu-id="196a2-171">如何在 Azure DevTest Labs 疑難排解失敗的構件</span><span class="sxs-lookup"><span data-stu-id="196a2-171">How to troubleshoot failing Artifacts in Azure DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* <span data-ttu-id="196a2-172">[Join a VM to existing AD Domain using a resource manager template in Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs) (在 Azure DevTest Labs 使用 Resource Manager 範本將 VM 加入至現有 AD 網域)</span><span class="sxs-lookup"><span data-stu-id="196a2-172">[Join a VM to existing AD Domain using a resource manager template in Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)</span></span>
