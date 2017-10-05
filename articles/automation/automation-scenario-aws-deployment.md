---
title: "自動化 Amazon Web Services 中 VM 的部署 | Microsoft Docs"
description: "本文示範如何使用 Azure 自動化來自動化 Amazon Web 服務 VM 的建立"
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
ms.openlocfilehash: e0b784006b4933fe986890c09afa965934511784
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---provision-an-aws-virtual-machine"></a><span data-ttu-id="d99ff-103">Azure 自動化案例 - 佈建 AWS 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d99ff-103">Azure Automation scenario - provision an AWS virtual machine</span></span>
<span data-ttu-id="d99ff-104">在本文中，我們會示範如何利用 Azure 自動化在 Amazon Web Service (AWS) 訂用帳戶中佈建虛擬機器，並且提供該 VM 的特定名稱 (AWS 稱為「標記」VM)。</span><span class="sxs-lookup"><span data-stu-id="d99ff-104">In this article, we demonstrate how you can leverage Azure Automation to provision a virtual machine in your Amazon Web Service (AWS) subscription and give that VM a specific name – which AWS refers to as “tagging” the VM.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d99ff-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="d99ff-105">Prerequisites</span></span>
<span data-ttu-id="d99ff-106">基於本文的目的，您需要擁有 Azure 自動化帳戶和 AWS 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d99ff-106">For the purposes of this article, you need to have an Azure Automation account and an AWS subscription.</span></span> <span data-ttu-id="d99ff-107">如需設定 Azure 自動化帳戶以及使用 AWS 訂用帳戶認證進行設定的詳細資訊，請檢閱[使用 Amazon Web Services 設定驗證](automation-configure-aws-account.md)。</span><span class="sxs-lookup"><span data-stu-id="d99ff-107">For more information on setting up an Azure Automation account and configuring it with your AWS subscription credentials, review [Configure Authentication with Amazon Web Services](automation-configure-aws-account.md).</span></span>  <span data-ttu-id="d99ff-108">繼續之前，應該使用您的 AWS 訂用帳戶認證來建立或更新此帳戶，因為我們將在下列步驟中參考此帳戶。</span><span class="sxs-lookup"><span data-stu-id="d99ff-108">This account should be created or updated with your AWS subscription credentials before proceeding, as we will reference this account in the steps below.</span></span>

## <a name="deploy-amazon-web-services-powershell-module"></a><span data-ttu-id="d99ff-109">部署 Amazon Web Services PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="d99ff-109">Deploy Amazon Web Services PowerShell Module</span></span>
<span data-ttu-id="d99ff-110">我們的 VM 佈建 Runbook 將會利用 AWS PowerShell 模組來執行其工作。</span><span class="sxs-lookup"><span data-stu-id="d99ff-110">Our VM provisioning runbook will leverage the AWS PowerShell module to do its work.</span></span> <span data-ttu-id="d99ff-111">執行下列步驟，將模組新增至使用 AWS 訂用帳戶認證所設定的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="d99ff-111">Perform the following steps to add the module to your Automation account that is configured with your AWS subscription credentials.</span></span>  

1. <span data-ttu-id="d99ff-112">開啟網頁瀏覽器，並瀏覽至 [PowerShell 資源庫](http://www.powershellgallery.com/packages/AWSPowerShell/)，然後按一下 [部署至 Azure 自動化] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d99ff-112">Open your web browser and navigate to the [PowerShell Gallery](http://www.powershellgallery.com/packages/AWSPowerShell/) and click on the **Deploy to Azure Automation button**.</span></span><br><br> <span data-ttu-id="d99ff-113">![AWS PS 模組匯入](./media/automation-scenario-aws-deployment/powershell-gallery-download-awsmodule.png)</span><span class="sxs-lookup"><span data-stu-id="d99ff-113">![AWS PS Module Import](./media/automation-scenario-aws-deployment/powershell-gallery-download-awsmodule.png)</span></span>
2. <span data-ttu-id="d99ff-114">系統會帶您前往 Azure 登入頁面，而在驗證之後，則會帶您到 Azure 入口網站，並出現下列刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d99ff-114">You are taken to the Azure login page and after authenticating, you will be routed to the Azure Portal and presented with the following blade.</span></span><br><br> ![匯入模組刀鋒視窗](./media/automation-scenario-aws-deployment/deploy-aws-powershell-module-parameters.png)
3. <span data-ttu-id="d99ff-116">從 [資源群組]  下拉式清單中選取資源群組，並在 [參數] 刀鋒視窗上提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="d99ff-116">Select the Resource Group from the **Resource Group** drop-down list and on the Parameters blade, provide the following information:</span></span>
   
   * <span data-ttu-id="d99ff-117">從 [新增或現有自動化帳戶 (字串)] 下拉式清單中，選取 [現有]。</span><span class="sxs-lookup"><span data-stu-id="d99ff-117">From the **New or Existing Automation Account (string)** drop-down list select **Existing**.</span></span>  
   * <span data-ttu-id="d99ff-118">在 [自動化帳戶名稱 (字串)] 方塊中，輸入包括 AWS 訂用帳戶認證的確切自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="d99ff-118">In the **Automation Account Name (string)** box, type in the exact name of the Automation account that includes the credentials for your AWS subscription.</span></span>  <span data-ttu-id="d99ff-119">例如，如果您已建立名為 **AWSAutomation** 的專用帳戶，則這是您在此方塊中輸入的名稱。</span><span class="sxs-lookup"><span data-stu-id="d99ff-119">For example, if you created a dedicated account named **AWSAutomation**, then that is what you type in the box.</span></span>
   * <span data-ttu-id="d99ff-120">從 [自動化帳戶位置]  下拉式清單中，選取適當的區域。</span><span class="sxs-lookup"><span data-stu-id="d99ff-120">Select the appropriate region from the **Automation Account Location** drop-down list.</span></span>
4. <span data-ttu-id="d99ff-121">輸入完所需的資訊後，請按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d99ff-121">When you have completed entering the required information, click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d99ff-122">將 PowerShell 模組匯入 Azure 自動化時，也會擷取 Cmdlet，而且在模組完全完成匯入並擷取 Cmdlet 之前不會出現這些活動。</span><span class="sxs-lookup"><span data-stu-id="d99ff-122">While importing a PowerShell module into Azure Automation, it is also extracting the cmdlets and these activities will not appear until the module has completely finished importing and extracting the cmdlets.</span></span> <span data-ttu-id="d99ff-123">此程序需要數分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="d99ff-123">This  process can take a few minutes.</span></span>  
   > <br>
   > 
   > 
5. <span data-ttu-id="d99ff-124">在 Azure 入口網站中，開啟步驟 3 中所參考的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="d99ff-124">In the Azure Portal, open your Automation account referenced in step 3.</span></span>
6. <span data-ttu-id="d99ff-125">按一下 [資產] 圖格，然後在 [資產] 刀鋒視窗上選取 [模組] 圖格。</span><span class="sxs-lookup"><span data-stu-id="d99ff-125">Click on the **Assets** tile and on the **Assets** blade, select the **Modules** tile.</span></span>
7. <span data-ttu-id="d99ff-126">在 [模組] 刀鋒視窗上，您將會在清單中看到 **AWSPowerShell** 模組。</span><span class="sxs-lookup"><span data-stu-id="d99ff-126">On the **Modules** blade you will see the **AWSPowerShell** module in the list.</span></span>

## <a name="create-aws-deploy-vm-runbook"></a><span data-ttu-id="d99ff-127">建立 AWS 部署 VM Runbook</span><span class="sxs-lookup"><span data-stu-id="d99ff-127">Create AWS deploy VM runbook</span></span>
<span data-ttu-id="d99ff-128">部署 AWS PowerShell 模組之後，我們現在可以製作 Runbook，以使用 PowerShell 指令碼自動在 AWS 中佈建虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d99ff-128">Once the AWS PowerShell Module has been deployed, we can now author a runbook to automate provisioning a virtual machine in AWS using a PowerShell script.</span></span> <span data-ttu-id="d99ff-129">下面的步驟將示範如何在 Azure 自動化中利用原生 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="d99ff-129">The steps below will demonstrate how to leverage native PowerShell script in Azure Automation.</span></span>  

> [!NOTE]
> <span data-ttu-id="d99ff-130">如需進一步選項以及此指令碼的相關資訊，請瀏覽 [PowerShell 資源庫](https://www.powershellgallery.com/packages/New-AwsVM/DisplayScript)。</span><span class="sxs-lookup"><span data-stu-id="d99ff-130">For further options and information regarding this script, please visit the [PowerShell Gallery](https://www.powershellgallery.com/packages/New-AwsVM/DisplayScript).</span></span>
> 

1. <span data-ttu-id="d99ff-131">開啟 PowerShell 工作階段並且輸入下列指令，以從 PowerShell 資源庫下載 PowerShell 指令碼 New-AwsVM：</span><span class="sxs-lookup"><span data-stu-id="d99ff-131">Download the PowerShell script New-AwsVM from the PowerShell Gallery by opening a PowerShell session and typing the following:</span></span><br>
   ```
   Save-Script -Name New-AwsVM -Path <path>
   ```
   <br>
2. <span data-ttu-id="d99ff-132">從 Azure 入口網站中，開啟您的自動化帳戶，然後按一下 [Runbook] 圖格。</span><span class="sxs-lookup"><span data-stu-id="d99ff-132">From the Azure Portal, open your Automation account and click the  **Runbooks** tile.</span></span>  
3. <span data-ttu-id="d99ff-133">從 [Runbook] 刀鋒視窗中，選取 [新增 Runbook]。</span><span class="sxs-lookup"><span data-stu-id="d99ff-133">From the **Runbooks** blade, select **Add a runbook**.</span></span>
4. <span data-ttu-id="d99ff-134">在 [新增 Runbook] 刀鋒視窗上，選取 [快速建立] \(建立新的 Runbook)。</span><span class="sxs-lookup"><span data-stu-id="d99ff-134">On the **Add a runbook** blade, select **Quick Create** (Create a new runbook).</span></span>
5. <span data-ttu-id="d99ff-135">在 [Runbook] 屬性刀鋒視窗上，於 Runbook 的 [名稱] 方塊中輸入名稱，並從 [Runbook 類型] 下拉式清單中選取 [PowerShell]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="d99ff-135">On the **Runbook** properties blade, type a name in the Name box for your runbook and from the **Runbook type** drop-down list select **PowerShell**, and then click **Create**.</span></span><br><br> <span data-ttu-id="d99ff-136">![匯入模組刀鋒視窗](./media/automation-scenario-aws-deployment/runbook-quickcreate-properties.png)</span><span class="sxs-lookup"><span data-stu-id="d99ff-136">![Import Module Blade](./media/automation-scenario-aws-deployment/runbook-quickcreate-properties.png)</span></span>
6. <span data-ttu-id="d99ff-137">[編輯 PowerShell Runbook] 刀鋒視窗出現時，將 PowerShell 指令碼複製並貼入 Runbook 撰寫畫布。</span><span class="sxs-lookup"><span data-stu-id="d99ff-137">When the Edit PowerShell Runbook blade appears, copy and paste the PowerShell script into the runbook authoring canvas.</span></span><br><br> ![Runbook PowerShell 指令碼](./media/automation-scenario-aws-deployment/runbook-powershell-script.png)<br>
   
    > [!NOTE]
    > <span data-ttu-id="d99ff-139">使用範例 PowerShell 指令碼時，請注意下列事項：</span><span class="sxs-lookup"><span data-stu-id="d99ff-139">Please note the following when working with the example PowerShell script:</span></span>
    > 
    > * <span data-ttu-id="d99ff-140">Runbook 包含一些預設參數值。</span><span class="sxs-lookup"><span data-stu-id="d99ff-140">The runbook contains a number of default parameter values.</span></span> <span data-ttu-id="d99ff-141">請評估所有預設值，並且視需要更新。</span><span class="sxs-lookup"><span data-stu-id="d99ff-141">Please evaluate all default values and update where necessary.</span></span>
    > * <span data-ttu-id="d99ff-142">如果您已將 AWS 認證儲存為名稱與 **AWScred**不同的認證資產，則需要更新指令碼的第 57 行，使其相符。</span><span class="sxs-lookup"><span data-stu-id="d99ff-142">If you have stored your AWS credentials as a credential asset named differently than **AWScred**, you will need to update the script on line 57 to match accordingly.</span></span>  
    > * <span data-ttu-id="d99ff-143">在 PowerShell 中使用 AWS CLI 命令 (特別是使用此範例 Runbook) 時，您必須指定 AWS 區域。</span><span class="sxs-lookup"><span data-stu-id="d99ff-143">When working with the AWS CLI commands in PowerShell, especially with this example runbook, you must specify the AWS region.</span></span> <span data-ttu-id="d99ff-144">否則，Cmdlet 會失敗。</span><span class="sxs-lookup"><span data-stu-id="d99ff-144">Otherwise, the cmdlets will fail.</span></span>  <span data-ttu-id="d99ff-145">如需進一步詳細資訊，請檢視 AWS Tools for PowerShell 文件中的 AWS 主題： [指定 AWS 區域](http://docs.aws.amazon.com/powershell/latest/userguide/pstools-installing-specifying-region.html) 。</span><span class="sxs-lookup"><span data-stu-id="d99ff-145">View AWS topic [Specify AWS Region](http://docs.aws.amazon.com/powershell/latest/userguide/pstools-installing-specifying-region.html) in the AWS Tools for PowerShell document for further details.</span></span>  
    >

7. <span data-ttu-id="d99ff-146">若要從 AWS 訂用帳戶擷取映像名稱清單，請啟動 PowerShell ISE 並匯入 AWS PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="d99ff-146">To retrieve a list of image names from your AWS subscription, launch PowerShell ISE and import the AWS PowerShell Module.</span></span>  <span data-ttu-id="d99ff-147">將 ISE 環境中的 **Get-AutomationPSCredential** 取代為 **AWScred = Get-Credential**，以驗證 AWS。</span><span class="sxs-lookup"><span data-stu-id="d99ff-147">Authenticate against AWS by replacing **Get-AutomationPSCredential** in your ISE environment with **AWScred = Get-Credential**.</span></span>  <span data-ttu-id="d99ff-148">這將會提示您輸入認證，您可以提供您的**存取金鑰識別碼**和**祕密存取金鑰**做為使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="d99ff-148">This will prompt you for your credentials and you can provide your **Access Key ID** for the username and **Secret Access Key** for the password.</span></span>  <span data-ttu-id="d99ff-149">請參閱下面的範例：</span><span class="sxs-lookup"><span data-stu-id="d99ff-149">See the example below:</span></span>  

        #Sample to get the AWS VM available images
        #Please provide the path where you have downloaded the AWS PowerShell module
        Import-Module AWSPowerShell
        $AwsRegion = "us-west-2"
        $AwsCred = Get-Credential
        $AwsAccessKeyId = $AwsCred.UserName
        $AwsSecretKey = $AwsCred.GetNetworkCredential().Password
   
        # Set up the environment to access AWS
        Set-AwsCredentials -AccessKey $AwsAccessKeyId -SecretKey $AwsSecretKey -StoreAs AWSProfile
        Set-DefaultAWSRegion -Region $AwsRegion
   
        Get-EC2ImageByName -ProfileName AWSProfile

    <span data-ttu-id="d99ff-150">會傳回下列輸出：</span><span class="sxs-lookup"><span data-stu-id="d99ff-150">The following output is returned:</span></span><br><br><span data-ttu-id="d99ff-151">
   ![取得 AWS 映像](./media/automation-scenario-aws-deployment/powershell-ise-output.png)</span><span class="sxs-lookup"><span data-stu-id="d99ff-151">
![Get AWS images](./media/automation-scenario-aws-deployment/powershell-ise-output.png)</span></span><br>  
8. <span data-ttu-id="d99ff-152">在自動化變數中複製並貼上其中一個映像名稱，在 Runbook 中參考為 **$InstanceType**。</span><span class="sxs-lookup"><span data-stu-id="d99ff-152">Copy and paste the one of the image names in an Automation variable as referenced in the runbook as **$InstanceType**.</span></span> <span data-ttu-id="d99ff-153">因為我們在此範例中使用免費 AWS 層訂用帳戶，所以將使用 **t2.micro** 作為 Runbook 範例。</span><span class="sxs-lookup"><span data-stu-id="d99ff-153">Since in this example we are using the free AWS tiered subscription, we'll use **t2.micro** for our runbook example.</span></span>  
9. <span data-ttu-id="d99ff-154">儲存 Runbook，然後按一下 [發佈] 來發佈 Runbook，並在出現提示時按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="d99ff-154">Save the runbook, then click **Publish** to publish the runbook and then **Yes** when prompted.</span></span>

### <a name="testing-the-aws-vm-runbook"></a><span data-ttu-id="d99ff-155">測試 AWS VM Runbook</span><span class="sxs-lookup"><span data-stu-id="d99ff-155">Testing the AWS VM runbook</span></span>
<span data-ttu-id="d99ff-156">繼續測試 Runbook 之前，需要驗證一些事項。</span><span class="sxs-lookup"><span data-stu-id="d99ff-156">Before we proceed with testing the runbook, we need to verify a few things.</span></span> <span data-ttu-id="d99ff-157">具體而言：</span><span class="sxs-lookup"><span data-stu-id="d99ff-157">Specifically:</span></span>  

* <span data-ttu-id="d99ff-158">驗證 AWS 的資產已建立並命名為 **AWScred** ，或指令碼已更新成參考您認證資產的名稱。</span><span class="sxs-lookup"><span data-stu-id="d99ff-158">An asset for authenticating against AWS has been created called **AWScred** or the script has been updated to reference the name of your credential asset.</span></span>    
* <span data-ttu-id="d99ff-159">AWS PowerShell 模組已匯入 Azure 自動化</span><span class="sxs-lookup"><span data-stu-id="d99ff-159">The AWS PowerShell module has been imported in Azure Automation</span></span>  
* <span data-ttu-id="d99ff-160">已建立新的 Runbook，已驗證參數值並且視需要更新</span><span class="sxs-lookup"><span data-stu-id="d99ff-160">A new runbook has been created and parameter values have been verified and updated where necessary</span></span>  
* <span data-ttu-id="d99ff-161">Runbook 設定 [記錄和追蹤] 下的 [記錄詳細資訊記錄] 和選擇性的 [記錄進度記錄] 已設為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="d99ff-161">**Log verbose records** and optionally **Log progress records** under the runbook setting **Logging and tracing** have been set to **On**.</span></span><br><br> <span data-ttu-id="d99ff-162">![Runbook 記錄和追蹤](./media/automation-scenario-aws-deployment/runbook-settings-logging-and-tracing.png)</span><span class="sxs-lookup"><span data-stu-id="d99ff-162">![Runbook Logging and Tracing](./media/automation-scenario-aws-deployment/runbook-settings-logging-and-tracing.png)</span></span>  

1. <span data-ttu-id="d99ff-163">我們想要啟動 Runbook，因此按一下 [啟動]，然後在 [啟動 Runbook] 刀鋒視窗開啟時按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="d99ff-163">We want to start the runbook, so click **Start** and then click **OK** when the Start Runbook blade opens.</span></span>
2. <span data-ttu-id="d99ff-164">在 [啟動 Runbook] 刀鋒視窗上，提供 **VMname**。</span><span class="sxs-lookup"><span data-stu-id="d99ff-164">On the Start Runbook blade, provide a **VMname**.</span></span>  <span data-ttu-id="d99ff-165">接受您稍早已在指令碼中為其他參數預先設定的預設值。</span><span class="sxs-lookup"><span data-stu-id="d99ff-165">Accept the default values for the other parameters that you preconfigured in the script earlier.</span></span>  <span data-ttu-id="d99ff-166">按一下 [確定] 啟動 Runbook 工作。</span><span class="sxs-lookup"><span data-stu-id="d99ff-166">Click **OK** to start the runbook job.</span></span><br><br> <span data-ttu-id="d99ff-167">![啟動 New-AwsVM Runbook](./media/automation-scenario-aws-deployment/runbook-start-job-parameters.png)</span><span class="sxs-lookup"><span data-stu-id="d99ff-167">![Start New-AwsVM runbook](./media/automation-scenario-aws-deployment/runbook-start-job-parameters.png)</span></span>
3. <span data-ttu-id="d99ff-168">工作窗格會開啟我們剛剛建立的 Runbook 工作。</span><span class="sxs-lookup"><span data-stu-id="d99ff-168">A job pane is opened for the runbook job that we just created.</span></span> <span data-ttu-id="d99ff-169">關閉此窗格。</span><span class="sxs-lookup"><span data-stu-id="d99ff-169">Close this pane.</span></span>
4. <span data-ttu-id="d99ff-170">從 Runbook 工作刀鋒視窗中選取 [所有記錄檔] 圖格，即可檢視工作進度以及檢視輸出**串流**。</span><span class="sxs-lookup"><span data-stu-id="d99ff-170">We can view progress of the job and view output **Streams** by selecting the **All Logs** tile from the runbook job blade.</span></span><br><br> <span data-ttu-id="d99ff-171">![串流輸出](./media/automation-scenario-aws-deployment/runbook-job-streams-output.png)</span><span class="sxs-lookup"><span data-stu-id="d99ff-171">![Stream output](./media/automation-scenario-aws-deployment/runbook-job-streams-output.png)</span></span>
5. <span data-ttu-id="d99ff-172">請登入 AWS 管理主控台 (如果目前尚未登入)，以確認正在佈建 VM。</span><span class="sxs-lookup"><span data-stu-id="d99ff-172">To confirm the VM is being provisioned, log into the AWS Management Console if you are not currently logged in.</span></span><br><br> ![AWS 主控台部署 VM](./media/automation-scenario-aws-deployment/aws-instances-status.png)

## <a name="next-steps"></a><span data-ttu-id="d99ff-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d99ff-174">Next steps</span></span>
* <span data-ttu-id="d99ff-175">若要開始使用圖形化 Runbook，請參閱 [我的第一個圖形化 Runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="d99ff-175">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="d99ff-176">若要開始使用 PowerShell 工作流程 Runbook，請參閱 [我的第一個 PowerShell 工作流程 Runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="d99ff-176">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="d99ff-177">若要深入了解 Runbook 類型、其優點和限制，請參閱 [Azure 自動化 Runbook 類型](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="d99ff-177">To know more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>
* <span data-ttu-id="d99ff-178">如需 PowerShell 指令碼支援功能的詳細資訊，請參閱 [Azure 自動化中的原生 PowerShell 指令碼支援](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)</span><span class="sxs-lookup"><span data-stu-id="d99ff-178">For more information on PowerShell script support feature, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)</span></span>

