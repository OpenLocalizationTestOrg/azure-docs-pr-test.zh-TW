---
title: "aaaHow toouse hello Azure 從屬外掛程式與 Hudson 連續整合 |Microsoft 文件"
description: "描述如何 toouse hello Azure 從屬外掛程式與 Hudson 連續整合。"
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
ms.openlocfilehash: cd6e67ad71c208aa56746aa8b70ba507da20bee9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-slave-plug-in-with-hudson-continuous-integration"></a><span data-ttu-id="daeb6-103">如何 toouse hello Azure 從屬外掛程式與 Hudson 連續整合</span><span class="sxs-lookup"><span data-stu-id="daeb6-103">How toouse hello Azure slave plug-in with Hudson Continuous Integration</span></span>
<span data-ttu-id="daeb6-104">hello Azure 從屬 Hudson 外掛程式可讓您在 Azure 上的 tooprovision 從屬節點時執行分散式組建。</span><span class="sxs-lookup"><span data-stu-id="daeb6-104">hello Azure slave plug-in for Hudson enables you tooprovision slave nodes on Azure when running distributed builds.</span></span>

## <a name="install-hello-azure-slave-plug-in"></a><span data-ttu-id="daeb6-105">安裝 hello Azure 從屬外掛程式</span><span class="sxs-lookup"><span data-stu-id="daeb6-105">Install hello Azure Slave plug-in</span></span>
1. <span data-ttu-id="daeb6-106">在 hello Hudson 儀表板，按一下 **管理 Hudson**。</span><span class="sxs-lookup"><span data-stu-id="daeb6-106">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="daeb6-107">在 hello**管理 Hudson**頁面上，按一下**管理外掛程式**。</span><span class="sxs-lookup"><span data-stu-id="daeb6-107">In hello **Manage Hudson** page, click on **Manage Plugins**.</span></span>
3. <span data-ttu-id="daeb6-108">按一下 hello**可用** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="daeb6-108">Click hello **Available** tab.</span></span>
4. <span data-ttu-id="daeb6-109">按一下**搜尋**和型別**Azure** toolimit hello 清單 toorelevant 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="daeb6-109">Click **Search** and type **Azure** toolimit hello list toorelevant plug-ins.</span></span>
   
    <span data-ttu-id="daeb6-110">如果您選擇 tooscroll 透過 hello 可用的外掛程式清單，您會發現 hello Azure 從屬外掛程式在 hello**叢集管理和散佈建置**> 一節中 hello**其他** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="daeb6-110">If you opt tooscroll through hello list of available plug-ins, you will find hello Azure slave plug-in under hello **Cluster Management and Distributed Build** section in hello **Others** tab.</span></span>
5. <span data-ttu-id="daeb6-111">選取 hello 核取方塊**Azure 從屬 Plugin**。</span><span class="sxs-lookup"><span data-stu-id="daeb6-111">Select hello checkbox for **Azure Slave Plugin**.</span></span>
6. <span data-ttu-id="daeb6-112">按一下 [Install] 。</span><span class="sxs-lookup"><span data-stu-id="daeb6-112">Click **Install**.</span></span>
7. <span data-ttu-id="daeb6-113">重新啟動 Hudson。</span><span class="sxs-lookup"><span data-stu-id="daeb6-113">Restart Hudson.</span></span>

<span data-ttu-id="daeb6-114">現在已安裝該外掛程式的 hello，hello 下一個步驟是 tooconfigure hello 與您的 Azure 訂用帳戶設定檔的範本，可用於建立 hello 從屬節點的 VM hello toocreate 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="daeb6-114">Now that hello plug-in is installed, hello next steps would be tooconfigure hello plug-in with your Azure subscription profile and toocreate a template that will be used in creating hello VM for hello slave node.</span></span>

## <a name="configure-hello-azure-slave-plug-in-with-your-subscription-profile"></a><span data-ttu-id="daeb6-115">使用您的訂用帳戶設定檔設定 hello Azure 從屬外掛程式</span><span class="sxs-lookup"><span data-stu-id="daeb6-115">Configure hello Azure Slave plug-in with your subscription profile</span></span>
<span data-ttu-id="daeb6-116">訂用帳戶設定檔，也參考的 tooas 發行設定，是包含安全認證，以及一些額外的資訊，您將需要使用 Azure toowork 開發環境中的 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="daeb6-116">A subscription profile, also referred tooas publish settings, is an XML file that contains secure credentials and some additional information you'll need toowork with Azure in your development environment.</span></span> <span data-ttu-id="daeb6-117">tooconfigure hello Azure 從屬外掛程式，您需要：</span><span class="sxs-lookup"><span data-stu-id="daeb6-117">tooconfigure hello Azure slave plug-in, you need:</span></span>

* <span data-ttu-id="daeb6-118">訂用帳戶 ID</span><span class="sxs-lookup"><span data-stu-id="daeb6-118">Your subscription id</span></span>
* <span data-ttu-id="daeb6-119">訂用帳戶的管理憑證</span><span class="sxs-lookup"><span data-stu-id="daeb6-119">A management certificate for your subscription</span></span>

<span data-ttu-id="daeb6-120">您可以在 [訂用帳戶設定檔]中找到這些資訊。</span><span class="sxs-lookup"><span data-stu-id="daeb6-120">These can be found in your [subscription profile].</span></span> <span data-ttu-id="daeb6-121">以下是訂用帳戶設定檔的範例。</span><span class="sxs-lookup"><span data-stu-id="daeb6-121">Below is an example of a subscription profile.</span></span>

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

<span data-ttu-id="daeb6-122">您的訂用帳戶設定檔之後，請遵循這些步驟 tooconfigure hello Azure 從屬外掛程式。</span><span class="sxs-lookup"><span data-stu-id="daeb6-122">Once you have your subscription profile, follow these steps tooconfigure hello Azure slave plug-in.</span></span>

1. <span data-ttu-id="daeb6-123">在 hello Hudson 儀表板，按一下 **管理 Hudson**。</span><span class="sxs-lookup"><span data-stu-id="daeb6-123">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="daeb6-124">按一下 [ **設定系統**]。</span><span class="sxs-lookup"><span data-stu-id="daeb6-124">Click **Configure System**.</span></span>
3. <span data-ttu-id="daeb6-125">捲動 hello 頁面 toofind hello**雲端**> 一節。</span><span class="sxs-lookup"><span data-stu-id="daeb6-125">Scroll down hello page toofind hello **Cloud** section.</span></span>
4. <span data-ttu-id="daeb6-126">按一下 [新增雲端 > Microsoft Azure]。</span><span class="sxs-lookup"><span data-stu-id="daeb6-126">Click **Add new cloud > Microsoft Azure**.</span></span>
   
    ![新增雲端][add new cloud]
   
    <span data-ttu-id="daeb6-128">這會顯示您的訂用帳戶詳細資料，您需要 tooenter hello 欄位。</span><span class="sxs-lookup"><span data-stu-id="daeb6-128">This will show hello fields where you need tooenter your subscription details.</span></span>
   
    ![設定設定檔][configure profile]
5. <span data-ttu-id="daeb6-130">複製您的訂用帳戶設定檔中的 hello 訂用帳戶識別碼和管理憑證，並將它們貼 hello 適當的欄位。</span><span class="sxs-lookup"><span data-stu-id="daeb6-130">Copy hello subscription id and management certificate from your subscription profile and paste them in hello appropriate fields.</span></span>
   
    <span data-ttu-id="daeb6-131">當複製 hello 訂用帳戶識別碼和管理憑證，**不**包含 hello 引號括住 hello 值。</span><span class="sxs-lookup"><span data-stu-id="daeb6-131">When copying hello subscription id and management certificate, **do not** include hello quotes that enclose hello values.</span></span>
6. <span data-ttu-id="daeb6-132">按一下 [ **驗證組態**]。</span><span class="sxs-lookup"><span data-stu-id="daeb6-132">Click on **Verify configuration**.</span></span>
7. <span data-ttu-id="daeb6-133">當成功驗證 hello 的設定時，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="daeb6-133">When hello configuration is verified successfully, click **Save**.</span></span>

## <a name="set-up-a-virtual-machine-template-for-hello-azure-slave-plug-in"></a><span data-ttu-id="daeb6-134">設定虛擬機器範本的 hello Azure 從屬外掛程式</span><span class="sxs-lookup"><span data-stu-id="daeb6-134">Set up a virtual machine template for hello Azure Slave plug-in</span></span>
<span data-ttu-id="daeb6-135">虛擬機器範本可定義 hello 參數 hello 外掛程式會在 Azure 上使用 toocreate 從屬節點。</span><span class="sxs-lookup"><span data-stu-id="daeb6-135">A virtual machine template defines hello parameters hello plug-in will use toocreate a slave node on Azure.</span></span> <span data-ttu-id="daeb6-136">在下列步驟的 hello 我們將建立範本的 Ubuntu vm。</span><span class="sxs-lookup"><span data-stu-id="daeb6-136">In hello following steps we'll be creating template for an Ubuntu VM.</span></span>

1. <span data-ttu-id="daeb6-137">在 hello Hudson 儀表板，按一下 **管理 Hudson**。</span><span class="sxs-lookup"><span data-stu-id="daeb6-137">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="daeb6-138">按一下 [ **設定系統**]。</span><span class="sxs-lookup"><span data-stu-id="daeb6-138">Click on **Configure System**.</span></span>
3. <span data-ttu-id="daeb6-139">捲動 hello 頁面 toofind hello**雲端**> 一節。</span><span class="sxs-lookup"><span data-stu-id="daeb6-139">Scroll down hello page toofind hello **Cloud** section.</span></span>
4. <span data-ttu-id="daeb6-140">Hello 內**雲端**區段中，尋找**加入 Azure 虛擬機器範本**按一下 hello**新增** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="daeb6-140">Within hello **Cloud** section, find **Add Azure Virtual Machine Template** and click hello **Add** button.</span></span>
   
    ![新增 VM 範本][add vm template]
5. <span data-ttu-id="daeb6-142">指定雲端服務名稱在 hello**名稱**欄位。</span><span class="sxs-lookup"><span data-stu-id="daeb6-142">Specify a cloud service name in hello **Name** field.</span></span> <span data-ttu-id="daeb6-143">如果您指定的 hello 名稱參考 tooan 現有雲端服務，hello VM 將會佈建該服務中。</span><span class="sxs-lookup"><span data-stu-id="daeb6-143">If hello name you specify refers tooan existing cloud service, hello VM will be provisioned in that service.</span></span> <span data-ttu-id="daeb6-144">否則，Azure 會建立一個新的。</span><span class="sxs-lookup"><span data-stu-id="daeb6-144">Otherwise, Azure will create a new one.</span></span>
6. <span data-ttu-id="daeb6-145">在 hello**描述**欄位中，輸入您要建立 hello 範本的描述文字。</span><span class="sxs-lookup"><span data-stu-id="daeb6-145">In hello **Description** field, enter text that describes hello template you are creating.</span></span> <span data-ttu-id="daeb6-146">此資訊僅供記錄之用，並不會用於佈建 VM。</span><span class="sxs-lookup"><span data-stu-id="daeb6-146">This information is only for documentary purposes and is not used in provisioning a VM.</span></span>
7. <span data-ttu-id="daeb6-147">在 hello**標籤**欄位中，輸入**linux**。</span><span class="sxs-lookup"><span data-stu-id="daeb6-147">In hello **Labels** field, enter **linux**.</span></span> <span data-ttu-id="daeb6-148">此標籤是您要建立使用的 tooidentify hello 範本時，則後續使用的 tooreference hello 範本建立 Hudson 作業。</span><span class="sxs-lookup"><span data-stu-id="daeb6-148">This label is used tooidentify hello template you are creating and is subsequently used tooreference hello template when creating a Hudson job.</span></span>
8. <span data-ttu-id="daeb6-149">選取建立 hello VM 所在的區域。</span><span class="sxs-lookup"><span data-stu-id="daeb6-149">Select a region where hello VM will be created.</span></span>
9. <span data-ttu-id="daeb6-150">選取 hello 適當的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="daeb6-150">Select hello appropriate VM size.</span></span>
10. <span data-ttu-id="daeb6-151">指定 hello VM 將會建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="daeb6-151">Specify a storage account where hello VM will be created.</span></span> <span data-ttu-id="daeb6-152">請確定它是在 hello 與 hello 雲端服務，您將使用相同的區域。</span><span class="sxs-lookup"><span data-stu-id="daeb6-152">Make sure that it is in hello same region as hello cloud service you'll be using.</span></span> <span data-ttu-id="daeb6-153">如果您想建立新的儲存體 toobe，您可以將此欄位保留空白。</span><span class="sxs-lookup"><span data-stu-id="daeb6-153">If you want new storage toobe created, you can leave this field blank.</span></span>
11. <span data-ttu-id="daeb6-154">保留時間指定 hello Hudson 刪除閒置的從屬版本之前的分鐘數。</span><span class="sxs-lookup"><span data-stu-id="daeb6-154">Retention time specifies hello number of minutes before Hudson deletes an idle slave.</span></span> <span data-ttu-id="daeb6-155">將此設定保留 hello 預設值為 60。</span><span class="sxs-lookup"><span data-stu-id="daeb6-155">Leave this at hello default value of 60.</span></span>
12. <span data-ttu-id="daeb6-156">在**使用量**，將會使用這個從屬節點時，選取 hello 適當的條件。</span><span class="sxs-lookup"><span data-stu-id="daeb6-156">In **Usage**, select hello appropriate condition when this slave node will be used.</span></span> <span data-ttu-id="daeb6-157">就目前的情況，請選取 [ **盡可能利用此節點**]。</span><span class="sxs-lookup"><span data-stu-id="daeb6-157">For now, select **Utilize this node as much as possible**.</span></span>
    
     <span data-ttu-id="daeb6-158">此時，您的表單看起來可能有點像 toothis:</span><span class="sxs-lookup"><span data-stu-id="daeb6-158">At this point, your form would look somewhat similar toothis:</span></span>
    
     ![範本設定][template config]
13. <span data-ttu-id="daeb6-160">在**映像系列或識別碼**您有 toospecify 哪些系統映像將會安裝在您的 VM。</span><span class="sxs-lookup"><span data-stu-id="daeb6-160">In **Image Family or Id** you have toospecify what system image will be installed on your VM.</span></span> <span data-ttu-id="daeb6-161">您可以從映像系列清單中進行選取，或指定自訂映像。</span><span class="sxs-lookup"><span data-stu-id="daeb6-161">You can either select from a list of image families or specify a custom image.</span></span>
    
     <span data-ttu-id="daeb6-162">如果您想 tooselect 從映像系列的清單，請輸入 hello 第一個字元 （區分大小寫） 的 hello 映像系列名稱。</span><span class="sxs-lookup"><span data-stu-id="daeb6-162">If you want tooselect from a list of image families, enter hello first character (case-sensitive) of hello image family name.</span></span> <span data-ttu-id="daeb6-163">例如，輸入 **U** 將會顯示 Ubuntu Server 系列的清單。</span><span class="sxs-lookup"><span data-stu-id="daeb6-163">For instance, typing **U** will bring up a list of Ubuntu Server families.</span></span> <span data-ttu-id="daeb6-164">一旦您選取從 hello 清單，Jenkins 將會使用該系統映像，從該系列 hello 最新版本，佈建 VM 時。</span><span class="sxs-lookup"><span data-stu-id="daeb6-164">Once you select from hello list, Jenkins will use hello latest version of that system image from that family when provisioning your VM.</span></span>
    
     ![作業系統系列清單][OS family list]
    
     <span data-ttu-id="daeb6-166">如果您想 toouse 改用自訂影像，請輸入 hello 該自訂映像名稱。</span><span class="sxs-lookup"><span data-stu-id="daeb6-166">If you have a custom image that you want toouse instead, enter hello name of that custom image.</span></span> <span data-ttu-id="daeb6-167">自訂映像名稱不會顯示在清單中讓您擁有 hello 名稱的 tooensure 輸入正確。</span><span class="sxs-lookup"><span data-stu-id="daeb6-167">Custom image names are not shown in a list so you have tooensure that hello name is entered correctly.</span></span>    
    
     <span data-ttu-id="daeb6-168">此教學課程中，輸入**U** Ubuntu 映像，然後選取清單 toobring **Ubuntu Server 14.04 LTS**。</span><span class="sxs-lookup"><span data-stu-id="daeb6-168">For this tutorial, type **U** toobring up a list of Ubuntu images and select **Ubuntu Server 14.04 LTS**.</span></span>
14. <span data-ttu-id="daeb6-169">在 [啟動方法] 中，選取 [SSH]。</span><span class="sxs-lookup"><span data-stu-id="daeb6-169">For **Launch method**, select **SSH**.</span></span>
15. <span data-ttu-id="daeb6-170">複製下列 hello 指令碼並貼上 hello**初始化指令碼**欄位。</span><span class="sxs-lookup"><span data-stu-id="daeb6-170">Copy hello script below and paste in hello **Init script** field.</span></span>
    
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
    
     <span data-ttu-id="daeb6-171">hello**初始化指令碼**hello 建立 VM 之後將會執行。</span><span class="sxs-lookup"><span data-stu-id="daeb6-171">hello **Init script** will be executed after hello VM is created.</span></span> <span data-ttu-id="daeb6-172">在此範例中，hello 指令碼安裝 Java、 git、 以及 ant。</span><span class="sxs-lookup"><span data-stu-id="daeb6-172">In this example, hello script installs Java, git, and ant.</span></span>
16. <span data-ttu-id="daeb6-173">在 hello **Username**和**密碼**欄位中，輸入您慣用的值會在您的 VM 中建立的 hello 系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="daeb6-173">In hello **Username** and **Password** fields, enter your preferred values for hello administrator account that will be created on your VM.</span></span>
17. <span data-ttu-id="daeb6-174">按一下**驗證範本**toocheck，如果您指定的 hello 參數都有效。</span><span class="sxs-lookup"><span data-stu-id="daeb6-174">Click on **Verify Template** toocheck if hello parameters you specified are valid.</span></span>
18. <span data-ttu-id="daeb6-175">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="daeb6-175">Click on **Save**.</span></span>

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a><span data-ttu-id="daeb6-176">建立在 Azure 的從屬節點上執行的 Hudson 工作</span><span class="sxs-lookup"><span data-stu-id="daeb6-176">Create a Hudson job that runs on a slave node on Azure</span></span>
<span data-ttu-id="daeb6-177">在本節中，您將建立在 Azure 的從屬節點上執行的 Hudson 工作。</span><span class="sxs-lookup"><span data-stu-id="daeb6-177">In this section, you'll be creating a Hudson task that will run on a slave node on Azure.</span></span>

1. <span data-ttu-id="daeb6-178">在 hello Hudson 儀表板，按一下 **新工作**。</span><span class="sxs-lookup"><span data-stu-id="daeb6-178">In hello Hudson dashboard, click **New Job**.</span></span>
2. <span data-ttu-id="daeb6-179">輸入您要建立 hello 工作的名稱。</span><span class="sxs-lookup"><span data-stu-id="daeb6-179">Enter a name for hello job you are creating.</span></span>
3. <span data-ttu-id="daeb6-180">Hello 作業類型 選取**組建可用樣式軟體工作**。</span><span class="sxs-lookup"><span data-stu-id="daeb6-180">For hello job type, select **Build a free-style software job**.</span></span>
4. <span data-ttu-id="daeb6-181">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="daeb6-181">Click **OK**.</span></span>
5. <span data-ttu-id="daeb6-182">在 hello 工作組態頁面上，選取 **限制可以執行這個專案**。</span><span class="sxs-lookup"><span data-stu-id="daeb6-182">In hello job configuration page, select **Restrict where this project can be run**.</span></span>
6. <span data-ttu-id="daeb6-183">選取**節點和標籤功能表**選取**linux** （hello 上一節中建立 hello 虛擬機器範本時，我們指定此標籤）。</span><span class="sxs-lookup"><span data-stu-id="daeb6-183">Select **Node and label menu** and select **linux** (we specified this label when creating hello virtual machine template in hello previous section).</span></span>
7. <span data-ttu-id="daeb6-184">在 hello**建置**區段中，按一下**加入建置步驟**選取**執行殼層**。</span><span class="sxs-lookup"><span data-stu-id="daeb6-184">In hello **Build** section, click **Add build step** and select **Execute shell**.</span></span>
8. <span data-ttu-id="daeb6-185">編輯下列指令碼、 取代 hello **{您 github 帳戶名稱}**， **{project name}**，和**{您的專案目錄}**與適當的值，並貼上 hello編輯指令碼中出現的 hello 文字區域。</span><span class="sxs-lookup"><span data-stu-id="daeb6-185">Edit hello following script, replacing **{your github account name}**, **{your project name}**, and **{your project directory}** with appropriate values, and paste hello edited script in hello text area that appears.</span></span>
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory tooproject
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. <span data-ttu-id="daeb6-186">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="daeb6-186">Click on **Save**.</span></span>
10. <span data-ttu-id="daeb6-187">在 hello Hudson 儀表板，找出您剛才建立的 hello 作業，然後按一下 hello**排程組建**圖示。</span><span class="sxs-lookup"><span data-stu-id="daeb6-187">In hello Hudson dashboard, find hello job you just created and click on hello **Schedule a build** icon.</span></span>

<span data-ttu-id="daeb6-188">Hudson 接著會建立使用 hello 範本建立 hello 前一節中的從屬節點，並執行這項工作中的 hello 建置步驟中所指定的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="daeb6-188">Hudson will then create a slave node using hello template created in hello previous section and execute hello script you specified in hello build step for this task.</span></span>

## <a name="next-steps"></a><span data-ttu-id="daeb6-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="daeb6-189">Next Steps</span></span>
<span data-ttu-id="daeb6-190">如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]。</span><span class="sxs-lookup"><span data-stu-id="daeb6-190">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[訂用帳戶設定檔]: http://go.microsoft.com/fwlink/?LinkID=396395

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

