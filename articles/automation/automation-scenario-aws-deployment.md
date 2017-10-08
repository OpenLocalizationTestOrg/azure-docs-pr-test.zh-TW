---
title: "aaaAutomating Amazon Web Services 中的 VM 部署 |Microsoft 文件"
description: "本文示範如何 toouse 將 tooautomate 建立 Azure 自動化的 Amazon Web 服務的 VM"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 1d85c01a-d795-4523-8194-84fc15b53838
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/14/2017
ms.author: tiandert; bwren
ms.openlocfilehash: dd1f3af47d8700ced85a3ee5a406dde1c1311990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---provision-an-aws-virtual-machine"></a><span data-ttu-id="2d68a-103">Azure 自動化案例 - 佈建 AWS 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2d68a-103">Azure Automation scenario - provision an AWS virtual machine</span></span>
<span data-ttu-id="2d68a-104">在本文中，我們將示範如何利用 Azure 自動化 tooprovision Amazon Web 服務 (AWS) 訂用帳戶中的虛擬機器，並提供特定名稱 – 該 VM 的 AWS 指的是 「 標記 」 hello VM tooas。</span><span class="sxs-lookup"><span data-stu-id="2d68a-104">In this article, we demonstrate how you can leverage Azure Automation tooprovision a virtual machine in your Amazon Web Service (AWS) subscription and give that VM a specific name – which AWS refers tooas “tagging” hello VM.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d68a-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="2d68a-105">Prerequisites</span></span>
<span data-ttu-id="2d68a-106">基於 hello 這篇文章，您會需要 toohave Azure 自動化帳戶和 AWS 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2d68a-106">For hello purposes of this article, you need toohave an Azure Automation account and an AWS subscription.</span></span> <span data-ttu-id="2d68a-107">如需設定 Azure 自動化帳戶以及使用 AWS 訂用帳戶認證進行設定的詳細資訊，請檢閱[使用 Amazon Web Services 設定驗證](automation-configure-aws-account.md)。</span><span class="sxs-lookup"><span data-stu-id="2d68a-107">For more information on setting up an Azure Automation account and configuring it with your AWS subscription credentials, review [Configure Authentication with Amazon Web Services](automation-configure-aws-account.md).</span></span>  <span data-ttu-id="2d68a-108">此帳戶應該建立或更新以 AWS 訂用帳戶認證之前，我們會參考此帳戶在 hello 執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="2d68a-108">This account should be created or updated with your AWS subscription credentials before proceeding, as we will reference this account in hello steps below.</span></span>

## <a name="deploy-amazon-web-services-powershell-module"></a><span data-ttu-id="2d68a-109">部署 Amazon Web Services PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="2d68a-109">Deploy Amazon Web Services PowerShell Module</span></span>
<span data-ttu-id="2d68a-110">我們 VM 佈建 runbook 將會利用 hello AWS PowerShell 模組 toodo 其工作。</span><span class="sxs-lookup"><span data-stu-id="2d68a-110">Our VM provisioning runbook will leverage hello AWS PowerShell module toodo its work.</span></span> <span data-ttu-id="2d68a-111">執行下列步驟 tooadd hello 模組 tooyour 自動化帳戶已設有 AWS 訂用帳戶認證的 hello。</span><span class="sxs-lookup"><span data-stu-id="2d68a-111">Perform hello following steps tooadd hello module tooyour Automation account that is configured with your AWS subscription credentials.</span></span>  

1. <span data-ttu-id="2d68a-112">開啟網頁瀏覽器並瀏覽 toohello [PowerShell 資源庫](http://www.powershellgallery.com/packages/AWSPowerShell/)，然後按一下 hello**部署 tooAzure 自動化按鈕**。</span><span class="sxs-lookup"><span data-stu-id="2d68a-112">Open your web browser and navigate toohello [PowerShell Gallery](http://www.powershellgallery.com/packages/AWSPowerShell/) and click on hello **Deploy tooAzure Automation button**.</span></span><br><br> <span data-ttu-id="2d68a-113">![AWS PS 模組匯入](./media/automation-scenario-aws-deployment/powershell-gallery-download-awsmodule.png)</span><span class="sxs-lookup"><span data-stu-id="2d68a-113">![AWS PS Module Import](./media/automation-scenario-aws-deployment/powershell-gallery-download-awsmodule.png)</span></span>
2. <span data-ttu-id="2d68a-114">即會進入 toohello Azure 登入頁面，並驗證之後，將路由的 toohello Azure 入口網站，並顯示以 hello 遵循刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2d68a-114">You are taken toohello Azure login page and after authenticating, you will be routed toohello Azure Portal and presented with hello following blade.</span></span><br><br> ![匯入模組刀鋒視窗](./media/automation-scenario-aws-deployment/deploy-aws-powershell-module-parameters.png)
3. <span data-ttu-id="2d68a-116">選取 hello 資源群組從 hello**資源群組**下拉式清單，並在 hello 參數刀鋒視窗中，提供下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="2d68a-116">Select hello Resource Group from hello **Resource Group** drop-down list and on hello Parameters blade, provide hello following information:</span></span>
   
   * <span data-ttu-id="2d68a-117">從 hello**新的或現有的自動化帳戶 （字串）**下拉式清單中，選取**現有**。</span><span class="sxs-lookup"><span data-stu-id="2d68a-117">From hello **New or Existing Automation Account (string)** drop-down list select **Existing**.</span></span>  
   * <span data-ttu-id="2d68a-118">在 hello**自動化帳戶名稱 （字串）**方塊中，輸入 hello 完整名稱中的 hello 自動化帳戶，其中包含 hello AWS 訂用帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="2d68a-118">In hello **Automation Account Name (string)** box, type in hello exact name of hello Automation account that includes hello credentials for your AWS subscription.</span></span>  <span data-ttu-id="2d68a-119">例如，如果您建立名為的專用的帳戶**AWSAutomation**，則您在 [hello] 方塊中輸入的內容。</span><span class="sxs-lookup"><span data-stu-id="2d68a-119">For example, if you created a dedicated account named **AWSAutomation**, then that is what you type in hello box.</span></span>
   * <span data-ttu-id="2d68a-120">選取 hello 適當區域從 hello**自動化帳戶位置**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="2d68a-120">Select hello appropriate region from hello **Automation Account Location** drop-down list.</span></span>
4. <span data-ttu-id="2d68a-121">當您完成輸入 hello 所需的資訊時，請按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="2d68a-121">When you have completed entering hello required information, click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2d68a-122">雖然匯入至 Azure 自動化的 PowerShell 模組，它也擷取 hello cmdlet 且 hello 模組完全完成匯入和擷取 hello cmdlet 之前，不會出現這些活動。</span><span class="sxs-lookup"><span data-stu-id="2d68a-122">While importing a PowerShell module into Azure Automation, it is also extracting hello cmdlets and these activities will not appear until hello module has completely finished importing and extracting hello cmdlets.</span></span> <span data-ttu-id="2d68a-123">此程序需要數分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="2d68a-123">This  process can take a few minutes.</span></span>  
   > <br>
   > 
   > 
5. <span data-ttu-id="2d68a-124">在 hello Azure 入口網站，開啟您在步驟 3 中所參考的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="2d68a-124">In hello Azure Portal, open your Automation account referenced in step 3.</span></span>
6. <span data-ttu-id="2d68a-125">按一下 hello**資產**磚和 hello**資產**刀鋒視窗中，選取 hello**模組**磚。</span><span class="sxs-lookup"><span data-stu-id="2d68a-125">Click on hello **Assets** tile and on hello **Assets** blade, select hello **Modules** tile.</span></span>
7. <span data-ttu-id="2d68a-126">在 hello**模組**刀鋒視窗，您會看到 hello **AWSPowerShell** hello 清單中的模組。</span><span class="sxs-lookup"><span data-stu-id="2d68a-126">On hello **Modules** blade you will see hello **AWSPowerShell** module in hello list.</span></span>

## <a name="create-aws-deploy-vm-runbook"></a><span data-ttu-id="2d68a-127">建立 AWS 部署 VM Runbook</span><span class="sxs-lookup"><span data-stu-id="2d68a-127">Create AWS deploy VM runbook</span></span>
<span data-ttu-id="2d68a-128">一次 AWS PowerShell 模組已部署的 hello，我們現在可以製作 runbook tooautomate 佈建 AWS 使用 PowerShell 指令碼中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2d68a-128">Once hello AWS PowerShell Module has been deployed, we can now author a runbook tooautomate provisioning a virtual machine in AWS using a PowerShell script.</span></span> <span data-ttu-id="2d68a-129">hello 執行下列步驟將示範如何 tooleverage 原生 PowerShell 指令碼在 Azure 自動化中。</span><span class="sxs-lookup"><span data-stu-id="2d68a-129">hello steps below will demonstrate how tooleverage native PowerShell script in Azure Automation.</span></span>  

> [!NOTE]
> <span data-ttu-id="2d68a-130">如需進一步的選項和此指令碼的相關資訊，請造訪 hello [PowerShell 資源庫](https://www.powershellgallery.com/packages/New-AwsVM/DisplayScript)。</span><span class="sxs-lookup"><span data-stu-id="2d68a-130">For further options and information regarding this script, please visit hello [PowerShell Gallery](https://www.powershellgallery.com/packages/New-AwsVM/DisplayScript).</span></span>
> 

1. <span data-ttu-id="2d68a-131">從 hello PowerShell 資源庫下載 hello PowerShell 指令碼新增 AwsVM，請開啟 PowerShell 工作階段，然後輸入 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="2d68a-131">Download hello PowerShell script New-AwsVM from hello PowerShell Gallery by opening a PowerShell session and typing hello following:</span></span><br>
   ```
   Save-Script -Name New-AwsVM -Path <path>
   ```
   <br>
2. <span data-ttu-id="2d68a-132">從 hello Azure 入口網站，開啟您的自動化帳戶，然後按一下 hello **Runbook**磚。</span><span class="sxs-lookup"><span data-stu-id="2d68a-132">From hello Azure Portal, open your Automation account and click hello  **Runbooks** tile.</span></span>  
3. <span data-ttu-id="2d68a-133">從 hello **Runbook**刀鋒視窗中，選取**新增 runbook**。</span><span class="sxs-lookup"><span data-stu-id="2d68a-133">From hello **Runbooks** blade, select **Add a runbook**.</span></span>
4. <span data-ttu-id="2d68a-134">在 hello**新增 runbook**刀鋒視窗中，選取**快速建立**（建立新的 runbook）。</span><span class="sxs-lookup"><span data-stu-id="2d68a-134">On hello **Add a runbook** blade, select **Quick Create** (Create a new runbook).</span></span>
5. <span data-ttu-id="2d68a-135">在 [hello **Runbook**屬性刀鋒視窗中，輸入 hello 名稱] 方塊中的名稱為您的 runbook 與 hello **Runbook 類型**下拉式清單中，選取**PowerShell**，然後按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="2d68a-135">On hello **Runbook** properties blade, type a name in hello Name box for your runbook and from hello **Runbook type** drop-down list select **PowerShell**, and then click **Create**.</span></span><br><br> <span data-ttu-id="2d68a-136">![匯入模組刀鋒視窗](./media/automation-scenario-aws-deployment/runbook-quickcreate-properties.png)</span><span class="sxs-lookup"><span data-stu-id="2d68a-136">![Import Module Blade](./media/automation-scenario-aws-deployment/runbook-quickcreate-properties.png)</span></span>
6. <span data-ttu-id="2d68a-137">Hello 編輯 PowerShell Runbook 刀鋒視窗出現時，請複製並貼入 hello runbook 製作畫布中的 hello PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="2d68a-137">When hello Edit PowerShell Runbook blade appears, copy and paste hello PowerShell script into hello runbook authoring canvas.</span></span><br><br> ![Runbook PowerShell 指令碼](./media/automation-scenario-aws-deployment/runbook-powershell-script.png)<br>
   
    > [!NOTE]
    > <span data-ttu-id="2d68a-139">請使用 hello 範例 PowerShell 指令碼時，注意 hello 下列事項：</span><span class="sxs-lookup"><span data-stu-id="2d68a-139">Please note hello following when working with hello example PowerShell script:</span></span>
    > 
    > * <span data-ttu-id="2d68a-140">hello runbook 包含預設參數值的數目。</span><span class="sxs-lookup"><span data-stu-id="2d68a-140">hello runbook contains a number of default parameter values.</span></span> <span data-ttu-id="2d68a-141">請評估所有預設值，並且視需要更新。</span><span class="sxs-lookup"><span data-stu-id="2d68a-141">Please evaluate all default values and update where necessary.</span></span>
    > * <span data-ttu-id="2d68a-142">如果您有儲存 AWS 認證認證資產名稱不同於**AWScred**，您必須在行 57 toomatch tooupdate hello 指令碼據此。</span><span class="sxs-lookup"><span data-stu-id="2d68a-142">If you have stored your AWS credentials as a credential asset named differently than **AWScred**, you will need tooupdate hello script on line 57 toomatch accordingly.</span></span>  
    > * <span data-ttu-id="2d68a-143">當使用 hello AWS CLI 命令在 PowerShell 中，特別是此範例 runbook，您必須指定 hello AWS 區域。</span><span class="sxs-lookup"><span data-stu-id="2d68a-143">When working with hello AWS CLI commands in PowerShell, especially with this example runbook, you must specify hello AWS region.</span></span> <span data-ttu-id="2d68a-144">否則，hello 指令程式將會失敗。</span><span class="sxs-lookup"><span data-stu-id="2d68a-144">Otherwise, hello cmdlets will fail.</span></span>  <span data-ttu-id="2d68a-145">檢視 AWS 主題[指定 AWS 區域](http://docs.aws.amazon.com/powershell/latest/userguide/pstools-installing-specifying-region.html)hello AWS 工具，以取得詳細資料的 PowerShell 文件中。</span><span class="sxs-lookup"><span data-stu-id="2d68a-145">View AWS topic [Specify AWS Region](http://docs.aws.amazon.com/powershell/latest/userguide/pstools-installing-specifying-region.html) in hello AWS Tools for PowerShell document for further details.</span></span>  
    >

7. <span data-ttu-id="2d68a-146">tooretrieve 一份您 AWS 訂用帳戶，從映像名稱啟動 PowerShell ISE，並匯入 hello AWS PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="2d68a-146">tooretrieve a list of image names from your AWS subscription, launch PowerShell ISE and import hello AWS PowerShell Module.</span></span>  <span data-ttu-id="2d68a-147">將 ISE 環境中的 **Get-AutomationPSCredential** 取代為 **AWScred = Get-Credential**，以驗證 AWS。</span><span class="sxs-lookup"><span data-stu-id="2d68a-147">Authenticate against AWS by replacing **Get-AutomationPSCredential** in your ISE environment with **AWScred = Get-Credential**.</span></span>  <span data-ttu-id="2d68a-148">這會提示您輸入您的認證，而且您可以提供您**存取金鑰識別碼**hello 使用者名稱和**秘密便捷鍵**hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="2d68a-148">This will prompt you for your credentials and you can provide your **Access Key ID** for hello username and **Secret Access Key** for hello password.</span></span>  <span data-ttu-id="2d68a-149">請參閱以下的 hello 範例：</span><span class="sxs-lookup"><span data-stu-id="2d68a-149">See hello example below:</span></span>  

        #Sample tooget hello AWS VM available images
        #Please provide hello path where you have downloaded hello AWS PowerShell module
        Import-Module AWSPowerShell
        $AwsRegion = "us-west-2"
        $AwsCred = Get-Credential
        $AwsAccessKeyId = $AwsCred.UserName
        $AwsSecretKey = $AwsCred.GetNetworkCredential().Password
   
        # Set up hello environment tooaccess AWS
        Set-AwsCredentials -AccessKey $AwsAccessKeyId -SecretKey $AwsSecretKey -StoreAs AWSProfile
        Set-DefaultAWSRegion -Region $AwsRegion
   
        Get-EC2ImageByName -ProfileName AWSProfile

    <span data-ttu-id="2d68a-150">hello 會傳回下列輸出：</span><span class="sxs-lookup"><span data-stu-id="2d68a-150">hello following output is returned:</span></span><br><br><span data-ttu-id="2d68a-151">
   ![取得 AWS 映像](./media/automation-scenario-aws-deployment/powershell-ise-output.png)</span><span class="sxs-lookup"><span data-stu-id="2d68a-151">
![Get AWS images](./media/automation-scenario-aws-deployment/powershell-ise-output.png)</span></span><br>  
8. <span data-ttu-id="2d68a-152">複製並貼上的其中一個 hello 映像名稱 hello hello runbook 中參考的自動化變數**$InstanceType**。</span><span class="sxs-lookup"><span data-stu-id="2d68a-152">Copy and paste hello one of hello image names in an Automation variable as referenced in hello runbook as **$InstanceType**.</span></span> <span data-ttu-id="2d68a-153">在此範例中我們使用 hello 可用 AWS 分層訂用帳戶，因為我們將使用**t2.micro** runbook 範例。</span><span class="sxs-lookup"><span data-stu-id="2d68a-153">Since in this example we are using hello free AWS tiered subscription, we'll use **t2.micro** for our runbook example.</span></span>  
9. <span data-ttu-id="2d68a-154">儲存 hello runbook，然後按一下 **發行**toopublish hello runbook，然後**是**出現提示時。</span><span class="sxs-lookup"><span data-stu-id="2d68a-154">Save hello runbook, then click **Publish** toopublish hello runbook and then **Yes** when prompted.</span></span>

### <a name="testing-hello-aws-vm-runbook"></a><span data-ttu-id="2d68a-155">測試 hello AWS VM runbook</span><span class="sxs-lookup"><span data-stu-id="2d68a-155">Testing hello AWS VM runbook</span></span>
<span data-ttu-id="2d68a-156">我們繼續測試 hello runbook 之前，我們需要 tooverify 幾件事。</span><span class="sxs-lookup"><span data-stu-id="2d68a-156">Before we proceed with testing hello runbook, we need tooverify a few things.</span></span> <span data-ttu-id="2d68a-157">具體而言：</span><span class="sxs-lookup"><span data-stu-id="2d68a-157">Specifically:</span></span>  

* <span data-ttu-id="2d68a-158">驗證 AWS 資產建立呼叫**AWScred**或 hello 指令碼已更新的 tooreference hello 認證資產名稱。</span><span class="sxs-lookup"><span data-stu-id="2d68a-158">An asset for authenticating against AWS has been created called **AWScred** or hello script has been updated tooreference hello name of your credential asset.</span></span>    
* <span data-ttu-id="2d68a-159">已匯入 Azure 自動化中的 hello AWS PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="2d68a-159">hello AWS PowerShell module has been imported in Azure Automation</span></span>  
* <span data-ttu-id="2d68a-160">已建立新的 Runbook，已驗證參數值並且視需要更新</span><span class="sxs-lookup"><span data-stu-id="2d68a-160">A new runbook has been created and parameter values have been verified and updated where necessary</span></span>  
* <span data-ttu-id="2d68a-161">**記錄詳細資訊記錄**並選擇性地**記錄進度記錄**hello runbook 設定下**記錄與追蹤**設定得**上**。</span><span class="sxs-lookup"><span data-stu-id="2d68a-161">**Log verbose records** and optionally **Log progress records** under hello runbook setting **Logging and tracing** have been set too**On**.</span></span><br><br> <span data-ttu-id="2d68a-162">![Runbook 記錄和追蹤](./media/automation-scenario-aws-deployment/runbook-settings-logging-and-tracing.png)</span><span class="sxs-lookup"><span data-stu-id="2d68a-162">![Runbook Logging and Tracing](./media/automation-scenario-aws-deployment/runbook-settings-logging-and-tracing.png)</span></span>  

1. <span data-ttu-id="2d68a-163">我們想 toostart hello runbook，因此請按**啟動**，然後按一下**確定**hello 啟動 Runbook 刀鋒視窗開啟時。</span><span class="sxs-lookup"><span data-stu-id="2d68a-163">We want toostart hello runbook, so click **Start** and then click **OK** when hello Start Runbook blade opens.</span></span>
2. <span data-ttu-id="2d68a-164">在 hello 啟動 Runbook 刀鋒視窗中，提供**VMname**。</span><span class="sxs-lookup"><span data-stu-id="2d68a-164">On hello Start Runbook blade, provide a **VMname**.</span></span>  <span data-ttu-id="2d68a-165">您稍早預先 hello 指令碼中的其他參數接受 hello hello 的預設值。</span><span class="sxs-lookup"><span data-stu-id="2d68a-165">Accept hello default values for hello other parameters that you preconfigured in hello script earlier.</span></span>  <span data-ttu-id="2d68a-166">按一下**確定**toostart hello runbook 工作。</span><span class="sxs-lookup"><span data-stu-id="2d68a-166">Click **OK** toostart hello runbook job.</span></span><br><br> <span data-ttu-id="2d68a-167">![啟動 New-AwsVM Runbook](./media/automation-scenario-aws-deployment/runbook-start-job-parameters.png)</span><span class="sxs-lookup"><span data-stu-id="2d68a-167">![Start New-AwsVM runbook](./media/automation-scenario-aws-deployment/runbook-start-job-parameters.png)</span></span>
3. <span data-ttu-id="2d68a-168">工作窗格會開啟供 hello 剛才所建立的 runbook 工作。</span><span class="sxs-lookup"><span data-stu-id="2d68a-168">A job pane is opened for hello runbook job that we just created.</span></span> <span data-ttu-id="2d68a-169">關閉此窗格。</span><span class="sxs-lookup"><span data-stu-id="2d68a-169">Close this pane.</span></span>
4. <span data-ttu-id="2d68a-170">我們可以檢視進度 hello 工作和檢視輸出**資料流**選取 hello**所有記錄檔**磚的 hello runbook 作業 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2d68a-170">We can view progress of hello job and view output **Streams** by selecting hello **All Logs** tile from hello runbook job blade.</span></span><br><br> <span data-ttu-id="2d68a-171">![串流輸出](./media/automation-scenario-aws-deployment/runbook-job-streams-output.png)</span><span class="sxs-lookup"><span data-stu-id="2d68a-171">![Stream output](./media/automation-scenario-aws-deployment/runbook-job-streams-output.png)</span></span>
5. <span data-ttu-id="2d68a-172">如果您目前未登入，tooconfirm hello 正在佈建 VM，登入 hello AWS 管理主控台。</span><span class="sxs-lookup"><span data-stu-id="2d68a-172">tooconfirm hello VM is being provisioned, log into hello AWS Management Console if you are not currently logged in.</span></span><br><br> ![AWS 主控台部署 VM](./media/automation-scenario-aws-deployment/aws-instances-status.png)

## <a name="next-steps"></a><span data-ttu-id="2d68a-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2d68a-174">Next steps</span></span>
* <span data-ttu-id="2d68a-175">tooget 開始使用圖形化 runbook，請參閱[我的第一個圖形化 runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="2d68a-175">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="2d68a-176">tooget 開始使用 PowerShell 工作流程 runbook，請參閱[我的第一個 PowerShell 工作流程 runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="2d68a-176">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="2d68a-177">tooknow 深入了解 runbook 類型、 其優點和限制，請參閱[Azure 自動化 runbook 類型](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="2d68a-177">tooknow more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>
* <span data-ttu-id="2d68a-178">如需 PowerShell 指令碼支援功能的詳細資訊，請參閱 [Azure 自動化中的原生 PowerShell 指令碼支援](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)</span><span class="sxs-lookup"><span data-stu-id="2d68a-178">For more information on PowerShell script support feature, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)</span></span>

