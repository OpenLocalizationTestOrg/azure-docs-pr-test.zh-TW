---
title: "如何搭配使用 Azure 從屬外掛程式與 Hudson 連續整合 | Microsoft Docs"
description: "說明如何搭配使用 Azure 從屬外掛程式與 Hudson 連續整合。"
services: virtual-machines-linux
documentationcenter: 
author: rmcmurray
manager: wpickett
editor: 
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: c11b59f8ea432075b147a391de4b7bd3331e639e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-azure-slave-plug-in-with-hudson-continuous-integration"></a><span data-ttu-id="cdcfe-103">如何搭配使用 Azure 從屬外掛程式與 Hudson 連續整合</span><span class="sxs-lookup"><span data-stu-id="cdcfe-103">How to use the Azure slave plug-in with Hudson Continuous Integration</span></span>
<span data-ttu-id="cdcfe-104">適用於 Hudson 的 Azure 從屬外掛程式可讓您在執行分散式組建時在 Azure 上佈建從屬節點。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-104">The Azure slave plug-in for Hudson enables you to provision slave nodes on Azure when running distributed builds.</span></span>

## <a name="install-the-azure-slave-plug-in"></a><span data-ttu-id="cdcfe-105">安裝 Azure 從屬外掛程式</span><span class="sxs-lookup"><span data-stu-id="cdcfe-105">Install the Azure Slave plug-in</span></span>
1. <span data-ttu-id="cdcfe-106">在 Hudson 儀表板中，按一下 [ **管理 Hudson**]。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-106">In the Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="cdcfe-107">在 [管理 Hudson] 頁面中，按一下 [管理外掛程式]。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-107">In the **Manage Hudson** page, click on **Manage Plugins**.</span></span>
3. <span data-ttu-id="cdcfe-108">按一下 [Available]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-108">Click the **Available** tab.</span></span>
4. <span data-ttu-id="cdcfe-109">按一下 [搜尋] 並輸入 **Azure**，讓清單只顯示相關外掛程式。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-109">Click **Search** and type **Azure** to limit the list to relevant plug-ins.</span></span>
   
    <span data-ttu-id="cdcfe-110">如果您選擇透過捲動來查看可用的外掛程式清單，您會在 [其他] 索引標籤的 [叢集管理和分散式組建] 區段下找到 Azure 從屬外掛程式。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-110">If you opt to scroll through the list of available plug-ins, you will find the Azure slave plug-in under the **Cluster Management and Distributed Build** section in the **Others** tab.</span></span>
5. <span data-ttu-id="cdcfe-111">選取 [ **Azure 從屬外掛程式**] 的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-111">Select the checkbox for **Azure Slave Plugin**.</span></span>
6. <span data-ttu-id="cdcfe-112">按一下 [Install] 。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-112">Click **Install**.</span></span>
7. <span data-ttu-id="cdcfe-113">重新啟動 Hudson。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-113">Restart Hudson.</span></span>

<span data-ttu-id="cdcfe-114">現在外掛程式已安裝完畢，接下來的步驟是使用您的 Azure 訂用帳戶設定檔來設定外掛程式，以及建立為從屬節點建立 VM 時將使用的範本。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-114">Now that the plug-in is installed, the next steps would be to configure the plug-in with your Azure subscription profile and to create a template that will be used in creating the VM for the slave node.</span></span>

## <a name="configure-the-azure-slave-plug-in-with-your-subscription-profile"></a><span data-ttu-id="cdcfe-115">使用您的訂用帳戶設定檔來設定 Azure 從屬外掛程式</span><span class="sxs-lookup"><span data-stu-id="cdcfe-115">Configure the Azure Slave plug-in with your subscription profile</span></span>
<span data-ttu-id="cdcfe-116">訂用帳戶設定檔也稱為發佈設定，它是一個 XML 檔案，內含要與開發環境中的 Azure 搭配運作時所需的安全認證和一些額外資訊。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-116">A subscription profile, also referred to as publish settings, is an XML file that contains secure credentials and some additional information you'll need to work with Azure in your development environment.</span></span> <span data-ttu-id="cdcfe-117">若要設定 Azure 從屬外掛程式，您需要：</span><span class="sxs-lookup"><span data-stu-id="cdcfe-117">To configure the Azure slave plug-in, you need:</span></span>

* <span data-ttu-id="cdcfe-118">訂用帳戶 ID</span><span class="sxs-lookup"><span data-stu-id="cdcfe-118">Your subscription id</span></span>
* <span data-ttu-id="cdcfe-119">訂用帳戶的管理憑證</span><span class="sxs-lookup"><span data-stu-id="cdcfe-119">A management certificate for your subscription</span></span>

<span data-ttu-id="cdcfe-120">您可以在 [訂用帳戶設定檔]中找到這些資訊。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-120">These can be found in your [subscription profile].</span></span> <span data-ttu-id="cdcfe-121">以下是訂用帳戶設定檔的範例。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-121">Below is an example of a subscription profile.</span></span>

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

<span data-ttu-id="cdcfe-122">有了訂用帳戶設定檔後，請依照下列步驟來設定 Azure 從屬外掛程式。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-122">Once you have your subscription profile, follow these steps to configure the Azure slave plug-in.</span></span>

1. <span data-ttu-id="cdcfe-123">在 Hudson 儀表板中，按一下 [ **管理 Hudson**]。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-123">In the Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="cdcfe-124">按一下 [ **設定系統**]。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-124">Click **Configure System**.</span></span>
3. <span data-ttu-id="cdcfe-125">向下捲動頁面來找出 [ **雲端** ] 區段。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-125">Scroll down the page to find the **Cloud** section.</span></span>
4. <span data-ttu-id="cdcfe-126">按一下 [新增雲端 > Microsoft Azure]。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-126">Click **Add new cloud > Microsoft Azure**.</span></span>
   
    ![新增雲端][add new cloud]
   
    <span data-ttu-id="cdcfe-128">這會顯示一些欄位，您必須在其中輸入訂用帳戶的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-128">This will show the fields where you need to enter your subscription details.</span></span>
   
    ![設定設定檔][configure profile]
5. <span data-ttu-id="cdcfe-130">從訂用帳戶設定檔中複製訂用帳戶 ID 和管理憑證，然後貼到適當的欄位。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-130">Copy the subscription id and management certificate from your subscription profile and paste them in the appropriate fields.</span></span>
   
    <span data-ttu-id="cdcfe-131">複製訂用帳戶 ID 和管理憑證時，請「勿」  將括住值的引號也包括進來。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-131">When copying the subscription id and management certificate, **do not** include the quotes that enclose the values.</span></span>
6. <span data-ttu-id="cdcfe-132">按一下 [ **驗證組態**]。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-132">Click on **Verify configuration**.</span></span>
7. <span data-ttu-id="cdcfe-133">成功驗證組態後，按一下 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-133">When the configuration is verified successfully, click **Save**.</span></span>

## <a name="set-up-a-virtual-machine-template-for-the-azure-slave-plug-in"></a><span data-ttu-id="cdcfe-134">設定 Azure 從屬外掛程式的虛擬機器範本</span><span class="sxs-lookup"><span data-stu-id="cdcfe-134">Set up a virtual machine template for the Azure Slave plug-in</span></span>
<span data-ttu-id="cdcfe-135">虛擬機器範本會定義外掛程式用來在 Azure 上建立從屬節點的參數。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-135">A virtual machine template defines the parameters the plug-in will use to create a slave node on Azure.</span></span> <span data-ttu-id="cdcfe-136">在下列步驟中，我們將會建立 Ubuntu VM 的範本。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-136">In the following steps we'll be creating template for an Ubuntu VM.</span></span>

1. <span data-ttu-id="cdcfe-137">在 Hudson 儀表板中，按一下 [ **管理 Hudson**]。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-137">In the Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="cdcfe-138">按一下 [ **設定系統**]。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-138">Click on **Configure System**.</span></span>
3. <span data-ttu-id="cdcfe-139">向下捲動頁面來找出 [ **雲端** ] 區段。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-139">Scroll down the page to find the **Cloud** section.</span></span>
4. <span data-ttu-id="cdcfe-140">在 [雲端] 區段內，找到 [新增 Azure 虛擬機器範本]，然後按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-140">Within the **Cloud** section, find **Add Azure Virtual Machine Template** and click the **Add** button.</span></span>
   
    ![新增 VM 範本][add vm template]
5. <span data-ttu-id="cdcfe-142">在 [ **名稱** ] 欄位中，指定雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-142">Specify a cloud service name in the **Name** field.</span></span> <span data-ttu-id="cdcfe-143">如果您指定的名稱參照現有雲端服務，便會在該服務中佈建 VM。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-143">If the name you specify refers to an existing cloud service, the VM will be provisioned in that service.</span></span> <span data-ttu-id="cdcfe-144">否則，Azure 會建立一個新的。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-144">Otherwise, Azure will create a new one.</span></span>
6. <span data-ttu-id="cdcfe-145">在 [ **說明** ] 欄位中，輸入您要建立之範本的說明文字。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-145">In the **Description** field, enter text that describes the template you are creating.</span></span> <span data-ttu-id="cdcfe-146">此資訊僅供記錄之用，並不會用於佈建 VM。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-146">This information is only for documentary purposes and is not used in provisioning a VM.</span></span>
7. <span data-ttu-id="cdcfe-147">在 [標籤] 欄位中，輸入 **linux**。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-147">In the **Labels** field, enter **linux**.</span></span> <span data-ttu-id="cdcfe-148">此標籤可用來識別您要建立的範本，而且後續會用來在建立 Hudson 工作時參照範本。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-148">This label is used to identify the template you are creating and is subsequently used to reference the template when creating a Hudson job.</span></span>
8. <span data-ttu-id="cdcfe-149">選取將要建立 VM 的區域。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-149">Select a region where the VM will be created.</span></span>
9. <span data-ttu-id="cdcfe-150">選取適當的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-150">Select the appropriate VM size.</span></span>
10. <span data-ttu-id="cdcfe-151">指定將要建立 VM 的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-151">Specify a storage account where the VM will be created.</span></span> <span data-ttu-id="cdcfe-152">請確定它與您將要使用的雲端服務位在相同的區域中。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-152">Make sure that it is in the same region as the cloud service you'll be using.</span></span> <span data-ttu-id="cdcfe-153">如果您想要建立新的儲存體，可以將此欄位保留空白。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-153">If you want new storage to be created, you can leave this field blank.</span></span>
11. <span data-ttu-id="cdcfe-154">保留時間會指定 Hudson 要等待幾分鐘的時間才將閒置的從屬節點刪除。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-154">Retention time specifies the number of minutes before Hudson deletes an idle slave.</span></span> <span data-ttu-id="cdcfe-155">請讓此欄位保持使用預設值 60。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-155">Leave this at the default value of 60.</span></span>
12. <span data-ttu-id="cdcfe-156">在 [ **使用量**] 中，選取將會使用此從屬節點的適當條件。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-156">In **Usage**, select the appropriate condition when this slave node will be used.</span></span> <span data-ttu-id="cdcfe-157">就目前的情況，請選取 [ **盡可能利用此節點**]。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-157">For now, select **Utilize this node as much as possible**.</span></span>
    
     <span data-ttu-id="cdcfe-158">到目前為止，您的表單應該會與下圖類似：</span><span class="sxs-lookup"><span data-stu-id="cdcfe-158">At this point, your form would look somewhat similar to this:</span></span>
    
     ![範本設定][template config]
13. <span data-ttu-id="cdcfe-160">在 [ **映像系列或識別碼** ] 中，您必須指定要在您的 VM 上安裝的系統映像。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-160">In **Image Family or Id** you have to specify what system image will be installed on your VM.</span></span> <span data-ttu-id="cdcfe-161">您可以從映像系列清單中進行選取，或指定自訂映像。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-161">You can either select from a list of image families or specify a custom image.</span></span>
    
     <span data-ttu-id="cdcfe-162">如果您想從映像系列清單中進行選取，請輸入映像系列名稱的第一個字元 (需區分大小寫)。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-162">If you want to select from a list of image families, enter the first character (case-sensitive) of the image family name.</span></span> <span data-ttu-id="cdcfe-163">例如，輸入 **U** 將會顯示 Ubuntu Server 系列的清單。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-163">For instance, typing **U** will bring up a list of Ubuntu Server families.</span></span> <span data-ttu-id="cdcfe-164">在從清單中進行選取後，Jenkins 將會在佈建 VM 時使用該系列的該系統映像的最新版本。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-164">Once you select from the list, Jenkins will use the latest version of that system image from that family when provisioning your VM.</span></span>
    
     ![作業系統系列清單][OS family list]
    
     <span data-ttu-id="cdcfe-166">如果您想要改用自訂映像，請輸入該自訂映像的名稱。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-166">If you have a custom image that you want to use instead, enter the name of that custom image.</span></span> <span data-ttu-id="cdcfe-167">清單中不會顯示自訂映像名稱，因此您必須確實輸入正確的名稱。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-167">Custom image names are not shown in a list so you have to ensure that the name is entered correctly.</span></span>    
    
     <span data-ttu-id="cdcfe-168">針對此教學課程，請輸入 **U** 來顯示 Ubuntu 映像的\`清單，並選取 [Ubuntu Server 14.04 LTS]。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-168">For this tutorial, type **U** to bring up a list of Ubuntu images and select **Ubuntu Server 14.04 LTS**.</span></span>
14. <span data-ttu-id="cdcfe-169">在 [啟動方法] 中，選取 [SSH]。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-169">For **Launch method**, select **SSH**.</span></span>
15. <span data-ttu-id="cdcfe-170">複製下列指令碼並貼到 [ **Init 指令碼** ] 欄位。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-170">Copy the script below and paste in the **Init script** field.</span></span>
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     <span data-ttu-id="cdcfe-171">[ **Init 指令碼** ] 就會在 VM 建立好之後執行。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-171">The **Init script** will be executed after the VM is created.</span></span> <span data-ttu-id="cdcfe-172">在此範例中，指令碼會安裝 Java、git 和 ant。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-172">In this example, the script installs Java, git, and ant.</span></span>
16. <span data-ttu-id="cdcfe-173">在 [使用者名稱] 和 [密碼] 欄位中，針對將在 VM 上建立的系統管理員帳戶輸入偏好使用的值。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-173">In the **Username** and **Password** fields, enter your preferred values for the administrator account that will be created on your VM.</span></span>
17. <span data-ttu-id="cdcfe-174">按一下 [ **驗證範本** ] 以檢查所指定的參數是否有效。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-174">Click on **Verify Template** to check if the parameters you specified are valid.</span></span>
18. <span data-ttu-id="cdcfe-175">按一下 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-175">Click on **Save**.</span></span>

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a><span data-ttu-id="cdcfe-176">建立在 Azure 的從屬節點上執行的 Hudson 工作</span><span class="sxs-lookup"><span data-stu-id="cdcfe-176">Create a Hudson job that runs on a slave node on Azure</span></span>
<span data-ttu-id="cdcfe-177">在本節中，您將建立在 Azure 的從屬節點上執行的 Hudson 工作。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-177">In this section, you'll be creating a Hudson task that will run on a slave node on Azure.</span></span>

1. <span data-ttu-id="cdcfe-178">在 Hudson 儀表板中，按一下 [ **新增工作**]。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-178">In the Hudson dashboard, click **New Job**.</span></span>
2. <span data-ttu-id="cdcfe-179">輸入要建立之工作的名稱。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-179">Enter a name for the job you are creating.</span></span>
3. <span data-ttu-id="cdcfe-180">針對工作類型選取 [ **建置自由樣式的軟體作業**]。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-180">For the job type, select **Build a free-style software job**.</span></span>
4. <span data-ttu-id="cdcfe-181">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-181">Click **OK**.</span></span>
5. <span data-ttu-id="cdcfe-182">在工作組態頁面中，選取 [ **限制可以執行這個專案的位置**]。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-182">In the job configuration page, select **Restrict where this project can be run**.</span></span>
6. <span data-ttu-id="cdcfe-183">選取 [節點和標籤功能表]，然後選取 [linux]\(上一節在建立虛擬機器範本時，我們指定了這個標籤)。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-183">Select **Node and label menu** and select **linux** (we specified this label when creating the virtual machine template in the previous section).</span></span>
7. <span data-ttu-id="cdcfe-184">在 [組件] 區段中，按一下 [新增組件步驟]，然後選取 [執行殼層]。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-184">In the **Build** section, click **Add build step** and select **Execute shell**.</span></span>
8. <span data-ttu-id="cdcfe-185">編輯下列指令碼，將 **GitHub 帳戶名稱}**、**{專案名稱}** 和 **{專案目錄}** 替換為適當值，並在出現的文字區域中貼上編輯過的指令碼。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-185">Edit the following script, replacing **{your github account name}**, **{your project name}**, and **{your project directory}** with appropriate values, and paste the edited script in the text area that appears.</span></span>
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory to project
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. <span data-ttu-id="cdcfe-186">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-186">Click on **Save**.</span></span>
10. <span data-ttu-id="cdcfe-187">在 Hudson 儀表板中，找到您剛才建立的工作，然後按一下 [ **排程組建** ] 圖示。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-187">In the Hudson dashboard, find the job you just created and click on the **Schedule a build** icon.</span></span>

<span data-ttu-id="cdcfe-188">Hudson 就會使用上一節建立的範本建立從屬節點，並執行您針對這項工作指定於組建步驟中的指令碼。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-188">Hudson will then create a slave node using the template created in the previous section and execute the script you specified in the build step for this task.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdcfe-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cdcfe-189">Next Steps</span></span>
<span data-ttu-id="cdcfe-190">如需如何搭配使用 Azure 與 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心]。</span><span class="sxs-lookup"><span data-stu-id="cdcfe-190">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="cdcfe-191">[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="cdcfe-191">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="cdcfe-192">[訂用帳戶設定檔]: http://go.microsoft.com/fwlink/?LinkID=396395</span><span class="sxs-lookup"><span data-stu-id="cdcfe-192">[subscription profile]: http://go.microsoft.com/fwlink/?LinkID=396395</span></span>

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

