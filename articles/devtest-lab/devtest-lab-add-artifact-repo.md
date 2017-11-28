---
title: "aaaAdd Azure DevTest 實驗室中的 Git 儲存機制 tooa 實驗室 |Microsoft 文件"
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
ms.openlocfilehash: e590559ffb2d497e39823e35c3f66974f42f13c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-git-repository-toostore-custom-artifacts-and-azure-resource-manager-templates"></a><span data-ttu-id="d4ee5-103">加入 Git 儲存機制 toostore 自訂成品和 Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="d4ee5-103">Add a Git repository toostore custom artifacts and Azure Resource Manager templates</span></span>

<span data-ttu-id="d4ee5-104">如果您想太[建立自訂的成品](devtest-lab-artifact-author.md)hello Vm 在實驗室中，或[使用 Azure Resource Manager 範本 toocreate 自訂測試環境](devtest-lab-create-environment-from-arm.md)，您也必須加入私用 Git 儲存機制 tooinclude您的小組所建立的 Azure Resource Manager 範本或 hello 成品。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-104">If you want too[create custom artifacts](devtest-lab-artifact-author.md) for hello VMs in your lab, or [use Azure Resource Manager templates toocreate a custom test environment](devtest-lab-create-environment-from-arm.md), you must also add a private Git repository tooinclude hello artifacts or Azure Resource Manager templates that your team creates.</span></span> <span data-ttu-id="d4ee5-105">hello 儲存機制可裝載於[GitHub](https://github.com)或在[Visual Studio Team Services (VSTS)](https://visualstudio.com)。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-105">hello repository can be hosted on [GitHub](https://github.com) or on [Visual Studio Team Services (VSTS)](https://visualstudio.com).</span></span>

<span data-ttu-id="d4ee5-106">我們提供[構件的 Github 存放庫](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts)，您可以為您的實驗室依原樣部署為自行自訂。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-106">We have provided a [Github repository of artifacts](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts) that you can deploy as-is or customize for your labs.</span></span> <span data-ttu-id="d4ee5-107">當您自訂或建立成品時，無法將其儲存在 hello 公用儲存機制中，您必須建立您自己的私用儲存機制。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-107">When you customize or create an artifact, you cannot store them in hello public repository – you must create your own private repo.</span></span> 

<span data-ttu-id="d4ee5-108">當您建立 VM 時，您可以儲存 hello Azure Resource Manager 範本，如果您想要，然後使用它來自訂稍後 tooeasily 建立多個 Vm。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-108">When you create a VM, you can save hello Azure Resource Manager template, customize it if you want, and then use it later tooeasily create more VMs.</span></span> <span data-ttu-id="d4ee5-109">您必須建立您自己的私用儲存機制 toostore 自訂的 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-109">You must create your own private repository toostore your custom Azure Resource Manager templates.</span></span>  

* <span data-ttu-id="d4ee5-110">如何 toocreate GitHub 儲存機制中，請參閱的 toolearn [GitHub Bootcamp](https://help.github.com/categories/bootcamp/)。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-110">toolearn how toocreate a GitHub repository, see [GitHub Bootcamp](https://help.github.com/categories/bootcamp/).</span></span>
* <span data-ttu-id="d4ee5-111">如何 toocreate Team Services 專案使用 Git 儲存機制，請參閱的 toolearn[連接 tooVisual Studio Team Services](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online)。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-111">toolearn how toocreate a Team Services project with a Git Repository, see [Connect tooVisual Studio Team Services](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online).</span></span>

<span data-ttu-id="d4ee5-112">hello 下列螢幕擷取畫面顯示在 GitHub 中包含的成品儲存機制可能外觀的範例：</span><span class="sxs-lookup"><span data-stu-id="d4ee5-112">hello following screen shot shows an example of how a repository containing artifacts might look in GitHub:</span></span>  
![GitHub 構件儲存機制範例](./media/devtest-lab-add-repo/devtestlab-github-artifact-repo-home.png)

## <a name="get-hello-repository-information-and-credentials"></a><span data-ttu-id="d4ee5-114">取得 hello 儲存機制資訊和認證</span><span class="sxs-lookup"><span data-stu-id="d4ee5-114">Get hello repository information and credentials</span></span>
<span data-ttu-id="d4ee5-115">tooadd 儲存機制 tooyour 實驗室，您必須先取得特定資訊，以從您的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-115">tooadd a repository tooyour lab, you must first get certain information from your repository.</span></span> <span data-ttu-id="d4ee5-116">hello 下列各節將引導您完成取得這項資訊儲存機制裝載於 GitHub 和 Visual Studio Team Services。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-116">hello following sections guide you through getting this information for repositories hosted on GitHub and Visual Studio Team Services.</span></span>

### <a name="get-hello-github-repository-clone-url-and-personal-access-token"></a><span data-ttu-id="d4ee5-117">取得 hello GitHub 儲存機制複製品 URL 和個人存取權杖</span><span class="sxs-lookup"><span data-stu-id="d4ee5-117">Get hello GitHub repository clone URL and personal access token</span></span>
<span data-ttu-id="d4ee5-118">tooget hello GitHub 儲存機制複製品 URL 和個人存取權杖，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d4ee5-118">tooget hello GitHub repository clone URL and personal access token, follow these steps:</span></span>

1. <span data-ttu-id="d4ee5-119">瀏覽 toohello 首頁 hello GitHub 儲存機制包含 hello 成品或 Azure 資源管理員範本定義。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-119">Browse toohello home page of hello GitHub repository that contains hello artifact or Azure Resource Manager template definitions.</span></span>
2. <span data-ttu-id="d4ee5-120">選取 [複製或下載] 。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-120">Select **Clone or download**.</span></span>
3. <span data-ttu-id="d4ee5-121">選取 hello 按鈕 toocopy hello **HTTPS 複製 url** toohello 剪貼簿，並儲存供稍後使用 hello URL。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-121">Select hello button toocopy hello **HTTPS clone url** toohello clipboard, and save hello URL for later use.</span></span>
4. <span data-ttu-id="d4ee5-122">在 GitHub，hello 右上角選取 hello 設定檔影像，然後選取**設定**。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-122">Select hello profile image in hello upper-right corner of GitHub, and select **Settings**.</span></span>
5. <span data-ttu-id="d4ee5-123">在 hello**個人設定**功能表靠左、 hello 選取**個人存取權杖**。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-123">In hello **Personal settings** menu on hello left, select **Personal access tokens**.</span></span>
6. <span data-ttu-id="d4ee5-124">選取 [產生新的權杖] 。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-124">Select **Generate new token**.</span></span>
7. <span data-ttu-id="d4ee5-125">Hello 上**新的個人存取權杖**頁面上，輸入**語彙基元描述**，接受 hello 預設項目在 hello**選取範圍**，然後選擇 **產生語彙基元**。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-125">On hello **New personal access token** page, enter a **Token description**, accept hello default items in hello **Select scopes**, and then choose **Generate Token**.</span></span>
8. <span data-ttu-id="d4ee5-126">視需要更新版本，請儲存 hello 產生語彙基元。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-126">Save hello generated token as you need it later.</span></span>
9. <span data-ttu-id="d4ee5-127">您現在可以關閉 GitHub。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-127">You can close GitHub now.</span></span>   
10. <span data-ttu-id="d4ee5-128">繼續 toohello[連接您的實驗室 toohello 儲存機制](#connect-your-lab-to-the-repository)> 一節。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-128">Continue toohello [Connect your lab toohello repository](#connect-your-lab-to-the-repository) section.</span></span>

### <a name="get-hello-visual-studio-team-services-repository-clone-url-and-personal-access-token"></a><span data-ttu-id="d4ee5-129">取得 hello Visual Studio Team Services 的儲存機制複製品 URL 和個人存取權杖</span><span class="sxs-lookup"><span data-stu-id="d4ee5-129">Get hello Visual Studio Team Services repository clone URL and personal access token</span></span>
<span data-ttu-id="d4ee5-130">tooget hello Visual Studio Team Services 的儲存機制複製品 URL 和個人存取權杖，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d4ee5-130">tooget hello Visual Studio Team Services repository clone URL and personal access token, follow these steps:</span></span>

1. <span data-ttu-id="d4ee5-131">開啟 hello 首頁上的 team 集合 (例如， `https://contoso-web-team.visualstudio.com`)，然後選取您的專案。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-131">Open hello home page of your team collection (for example, `https://contoso-web-team.visualstudio.com`), and then select your project.</span></span>
2. <span data-ttu-id="d4ee5-132">在 hello 專案首頁上，選取 **程式碼**。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-132">On hello project home page, select **Code**.</span></span>
3. <span data-ttu-id="d4ee5-133">tooview hello 複製 URL，hello 專案**程式碼**頁面上，選取**複製**。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-133">tooview hello clone URL, on hello project **Code** page, select **Clone**.</span></span>
4. <span data-ttu-id="d4ee5-134">視需要稍後在本教學課程，請儲存 hello URL。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-134">Save hello URL as you need it later in this tutorial.</span></span>
5. <span data-ttu-id="d4ee5-135">選取 個人存取權杖，toocreate**我的設定檔**從 hello 使用者帳戶下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-135">toocreate a Personal Access Token, select **My profile** from hello user account drop-down menu.</span></span>
6. <span data-ttu-id="d4ee5-136">在 hello 設定檔資訊 頁面上，選取 **安全性**。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-136">On hello profile information page, select **Security**.</span></span>
7. <span data-ttu-id="d4ee5-137">在 hello**安全性**索引標籤上，選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-137">On hello **Security** tab, select **Add**.</span></span>
8. <span data-ttu-id="d4ee5-138">在 hello**建立個人存取權杖**頁面：</span><span class="sxs-lookup"><span data-stu-id="d4ee5-138">In hello **Create a personal access token** page:</span></span>

   * <span data-ttu-id="d4ee5-139">輸入**描述**hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-139">Enter a **Description** for hello token.</span></span>
   * <span data-ttu-id="d4ee5-140">選取**180 天**從 hello **到期日**清單。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-140">Select **180 days** from hello **Expires In** list.</span></span>
   * <span data-ttu-id="d4ee5-141">選擇**可存取的所有帳戶**從 hello**帳戶**清單。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-141">Choose **All accessible accounts** from hello **Accounts** list.</span></span>
   * <span data-ttu-id="d4ee5-142">選擇 hello**所有領域**選項。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-142">Choose hello **All scopes** option.</span></span>
   * <span data-ttu-id="d4ee5-143">選擇 [建立權杖] 。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-143">Choose **Create Token**.</span></span>
9. <span data-ttu-id="d4ee5-144">Hello 新語彙基元完成時，會出現在 hello**個人存取權杖**清單。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-144">When finished, hello new token appears in hello **Personal Access Tokens** list.</span></span> <span data-ttu-id="d4ee5-145">選取**Token 複製**，然後儲存供稍後使用 hello 語彙基元值。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-145">Select **Copy Token**, and then save hello token value for later use.</span></span>
10. <span data-ttu-id="d4ee5-146">繼續 toohello[連接您的實驗室 toohello 儲存機制](#connect-your-lab-to-the-repository)> 一節。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-146">Continue toohello [Connect your lab toohello repository](#connect-your-lab-to-the-repository) section.</span></span>

## <a name="connect-your-lab-toohello-repository"></a><span data-ttu-id="d4ee5-147">連接您的實驗室 toohello 儲存機制</span><span class="sxs-lookup"><span data-stu-id="d4ee5-147">Connect your lab toohello repository</span></span>
1. <span data-ttu-id="d4ee5-148">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-148">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="d4ee5-149">選取**更服務**，然後選取**DevTest Labs**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-149">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="d4ee5-150">從 hello 清單的實驗室中，選取 hello 所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-150">From hello list of labs, select hello desired lab.</span></span>   
4. <span data-ttu-id="d4ee5-151">在 hello 左面板中，選取 **組態和原則**。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-151">On hello left panel, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="d4ee5-152">在 hello 實驗室**組態和原則**區域中，選取**儲存機制**。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-152">On hello lab's **Configuration and policies** area, select **Repositories**.</span></span>
6. <span data-ttu-id="d4ee5-153">在 hello**儲存機制**區域中，選取**+ 加**。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-153">On hello **Repositories** area, select **+ Add**.</span></span>

    ![[新增存放庫] 按鈕](./media/devtest-lab-add-repo/devtestlab-add-repo.png)
7. <span data-ttu-id="d4ee5-155">在 hello 第二個**儲存機制**頁面上，指定下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="d4ee5-155">On hello second **Repositories** page, specify hello following information:</span></span>

   * <span data-ttu-id="d4ee5-156">**名稱**-輸入 hello 儲存機制的名稱。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-156">**Name** - Enter a name for hello repository.</span></span>
   * <span data-ttu-id="d4ee5-157">**Git 複製 Url** -輸入 hello Git HTTPS 複製 URL，您之前複製從 GitHub 或 Visual Studio Team Services。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-157">**Git Clone Url** - Enter hello Git HTTPS clone URL that you copied earlier from either GitHub or Visual Studio Team Services.</span></span>
   * <span data-ttu-id="d4ee5-158">**分支**-輸入 hello 分支 tooget 惡意程式碼定義。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-158">**Branch** - Enter hello branch tooget your definitions.</span></span>
   * <span data-ttu-id="d4ee5-159">**個人存取權杖**-輸入您稍早取得的 GitHub 或 Visual Studio Team Services hello 個人存取權杖。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-159">**Personal Access Token** - Enter hello personal access token you obtained earlier from either GitHub or Visual Studio Team Services.</span></span>
   * <span data-ttu-id="d4ee5-160">**資料夾路徑**-輸入最少一個資料夾路徑相對 toohello 複製 URL，其中包含您成品或 Azure 資源管理員範本定義。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-160">**Folder Paths** - Enter at least one folder path relative toohello clone URL that contains your artifact or Azure Resource Manager template definitions.</span></span> <span data-ttu-id="d4ee5-161">當指定子目錄，請確定 tooinclude hello 正斜線 hello 資料夾路徑中。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-161">When specifying a subdirectory, make sure tooinclude hello forward slash in hello folder path.</span></span>

     ![存放庫區域](./media/devtest-lab-add-repo/devtestlab-repo-blade.png)
8. <span data-ttu-id="d4ee5-163">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-163">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4ee5-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d4ee5-164">Next steps</span></span>
<span data-ttu-id="d4ee5-165">建立私用 Git 儲存機制之後，您可以一或兩個 hello 下列程式碼，根據您的需求：</span><span class="sxs-lookup"><span data-stu-id="d4ee5-165">After you have created your private Git repository, you can do one or both of hello following, depending on your needs:</span></span>
* <span data-ttu-id="d4ee5-166">存放區您[自訂成品](devtest-lab-artifact-author.md)，而您可以使用更新版本的 toocreate 新 Vm。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-166">Store your [custom artifacts](devtest-lab-artifact-author.md), which you can use later toocreate new VMs.</span></span>
* <span data-ttu-id="d4ee5-167">[使用 Azure Resource Manager 範本建立環境多部 VM 和 PaaS 資源](devtest-lab-create-environment-from-arm.md)然後將 hello 範本儲存在您的私用儲存機制。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-167">[Create multi-VM environments and PaaS resources with Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md) and then store hello templates in your private repo.</span></span>

<span data-ttu-id="d4ee5-168">當您建立 VM 時，您可以確認 hello 成品或範本加入 tooyour Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-168">When you create a VM, you can verify that hello artifacts or templates are added tooyour Git repository.</span></span> <span data-ttu-id="d4ee5-169">欄位屬性可立即在 hello 成品或範本的清單，以您指定 hello 來源的 hello 資料行所示的私用儲存機制的 hello 名稱中。</span><span class="sxs-lookup"><span data-stu-id="d4ee5-169">They are available immediately in hello list of artifacts or templates, with hello name of your private repo shown in hello column that specifies hello source.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="related-blog-posts"></a><span data-ttu-id="d4ee5-170">相關部落格文章</span><span class="sxs-lookup"><span data-stu-id="d4ee5-170">Related blog posts</span></span>
* [<span data-ttu-id="d4ee5-171">如何 tootroubleshoot 失敗 Azure DevTest Labs 中的成品</span><span class="sxs-lookup"><span data-stu-id="d4ee5-171">How tootroubleshoot failing Artifacts in Azure DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* [<span data-ttu-id="d4ee5-172">加入 VM tooexisting Azure DevTest 實驗室中使用資源管理員範本的 AD 網域</span><span class="sxs-lookup"><span data-stu-id="d4ee5-172">Join a VM tooexisting AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)
