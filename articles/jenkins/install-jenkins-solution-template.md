---
title: "在 Azure 上建立 Jenkins 伺服器"
description: "從 Jenkins 方案範本在 Azure Linux 虛擬機器上安裝 Jenkins，並建置範例 Java 應用程式。"
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 7bb74f297d52fb25171817175cce64187b397c38
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-the-azure-portal"></a><span data-ttu-id="9294d-103">從 Azure 入口網站在 Azure Linux VM 上建立 Jenkins 伺服器</span><span class="sxs-lookup"><span data-stu-id="9294d-103">Create a Jenkins server on an Azure Linux VM from the Azure portal</span></span>

<span data-ttu-id="9294d-104">本快速入門示範如何在 Ubuntu Linux VM 上安裝 [Jenkins](https://jenkins.io)，以及設定為使用 Azure 的工具和外掛程式。</span><span class="sxs-lookup"><span data-stu-id="9294d-104">This quickstart shows how to install [Jenkins](https://jenkins.io) on an Ubuntu Linux VM with the tools and plug-ins configured to work with Azure.</span></span> <span data-ttu-id="9294d-105">當您完成時，您可讓在 Azure 中執行的 Jenkins 伺服器從 [GitHub](https://github.com) 建置範例 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9294d-105">When you're finished, you have a Jenkins server running in Azure building a sample Java app from [GitHub](https://github.com).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9294d-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="9294d-106">Prerequisites</span></span>

* <span data-ttu-id="9294d-107">Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9294d-107">An Azure subscription</span></span>
* <span data-ttu-id="9294d-108">在您電腦的命令列上存取SSH (例如 Bash 殼層或 [PuTTY](http://www.putty.org/))</span><span class="sxs-lookup"><span data-stu-id="9294d-108">Access to SSH on your computer's command line (such as the Bash shell or [PuTTY](http://www.putty.org/))</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-the-jenkins-vm-from-the-solution-template"></a><span data-ttu-id="9294d-109">從方案範本建立 Jenkins VM</span><span class="sxs-lookup"><span data-stu-id="9294d-109">Create the Jenkins VM from the solution template</span></span>

<span data-ttu-id="9294d-110">在 Web 瀏覽器中開啟 [Jenkins 的 Marketplace 映像](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview)，然後從頁面左側選取 [立即取得]。</span><span class="sxs-lookup"><span data-stu-id="9294d-110">Open the [marketplace image for Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) in your web browser and select  **GET IT NOW** from the left-hand side of the page.</span></span> <span data-ttu-id="9294d-111">檢閱價格詳細資料並選取 [繼續]，然後選取 [建立] 以在 Azure 入口網站中設定 Jenkins 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9294d-111">Review the pricing details and select **Continue**, then select **Create** to configure the Jenkins server in the Azure portal.</span></span> 
   
![Azure 入口網站對話方塊](./media/install-jenkins-solution-template/ap-create.png)

<span data-ttu-id="9294d-113">在 [設定基本設定] 索引標籤中，填妥下列欄位：</span><span class="sxs-lookup"><span data-stu-id="9294d-113">In the **Configure basic settings** tab, fill in the following fields:</span></span>

![設定基本設定](./media/install-jenkins-solution-template/ap-basic.png)

* <span data-ttu-id="9294d-115">使用 **Jenkins** 作為 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="9294d-115">Use **Jenkins** for **Name**.</span></span>
* <span data-ttu-id="9294d-116">輸入 [使用者名稱]。</span><span class="sxs-lookup"><span data-stu-id="9294d-116">Enter a **User name**.</span></span> <span data-ttu-id="9294d-117">使用者名稱必須符合[特定需求](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm)。</span><span class="sxs-lookup"><span data-stu-id="9294d-117">The user name must meet [specific requirements](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span></span>
* <span data-ttu-id="9294d-118">選取 [密碼] 作為 [驗證類型] 並輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="9294d-118">Select **Password** as the **Authentication type** and enter a password.</span></span> <span data-ttu-id="9294d-119">密碼必須包含大寫字元、數字和一個特殊字元。</span><span class="sxs-lookup"><span data-stu-id="9294d-119">The password must have an upper case character, a number, and one special character.</span></span>
* <span data-ttu-id="9294d-120">使用 **myJenkinsResourceGroup** 作為 [資源群組]。</span><span class="sxs-lookup"><span data-stu-id="9294d-120">Use **myJenkinsResourceGroup** for the **Resource Group**.</span></span>
* <span data-ttu-id="9294d-121">從 [位置] 下拉式清單選擇 [美國東部] [Azure 地區](https://azure.microsoft.com/regions/)。</span><span class="sxs-lookup"><span data-stu-id="9294d-121">Choose the **East US** [Azure region](https://azure.microsoft.com/regions/) from the **Location** drop-down.</span></span>

<span data-ttu-id="9294d-122">選取 [確定] 繼續前往 [設定其他選項] 索引標籤。輸入唯一的網域名稱，以識別 Jenkins 伺服器並選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="9294d-122">Select **OK** to proceed to the **Configure additional options** tab. Enter a unique domain name to identify the Jenkins server and select **OK**.</span></span>

![設定其他選項](./media/install-jenkins-solution-template/ap-addtional.png)  

 <span data-ttu-id="9294d-124">一旦通過驗證，再次從 [摘要] 索引標籤選取 [確定]。最後，選取 [購買] 以建立 Jenkins VM。</span><span class="sxs-lookup"><span data-stu-id="9294d-124">Once validation passes, select **OK** again from the **Summary** tab. Finally, select **Purchase** to create the Jenkins VM.</span></span> <span data-ttu-id="9294d-125">當您的伺服器準備就緒時，您會在 Azure 入口網站中收到通知：</span><span class="sxs-lookup"><span data-stu-id="9294d-125">When your server is ready, you get a notification in the Azure portal:</span></span>   

![Jenkins 已就緒通知](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-to-jenkins"></a><span data-ttu-id="9294d-127">連線到 Jenkins</span><span class="sxs-lookup"><span data-stu-id="9294d-127">Connect to Jenkins</span></span>

<span data-ttu-id="9294d-128">在網頁瀏覽器中，瀏覽至您的虛擬機器 (例如，http://jenkins2517454.eastus.cloudapp.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="9294d-128">Navigate to your virtual machine (for example, http://jenkins2517454.eastus.cloudapp.azure.com/) in  your web browser.</span></span> <span data-ttu-id="9294d-129">Jenkins 主控台無法透過不安全的 HTTP 存取，因此頁面上會提供指示，以便從您的電腦使用 SSH 通道安全地存取 Jenkins 主控台。</span><span class="sxs-lookup"><span data-stu-id="9294d-129">The Jenkins console is inaccessible through unsecured HTTP so instructions are provided on the page to access the Jenkins console securely from your computer using an SSH tunnel.</span></span>

![將 Jenkins 解除鎖定](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

<span data-ttu-id="9294d-131">在頁面從命令列使用 `ssh` 命令設定通道，並以先前從方案範本設定虛擬機器時選擇的虛擬機器系統管理員的使用者名稱取代 `username`。</span><span class="sxs-lookup"><span data-stu-id="9294d-131">Set up the tunnel using the `ssh` command on the page from the command line, replacing `username` with the name of the virtual machine admin user chosen earlier when setting up the virtual machine from the solution template.</span></span>

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

<span data-ttu-id="9294d-132">啟動您的通道後，在本機電腦上瀏覽至 http://localhost:8080/。</span><span class="sxs-lookup"><span data-stu-id="9294d-132">After you have started the tunnel, navigate to http://localhost:8080/ on your local machine.</span></span> 

<span data-ttu-id="9294d-133">透過 SSH 連線到 Jenkins VM 時，在命令列中執行下列命令，以取得初始密碼。</span><span class="sxs-lookup"><span data-stu-id="9294d-133">Get the initial password by running the following command in the command line while connected through SSH to the Jenkins VM.</span></span>

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

<span data-ttu-id="9294d-134">第一次使用此初始密碼時，請將 Jenkins 儀表板解除鎖定。</span><span class="sxs-lookup"><span data-stu-id="9294d-134">Unlock the Jenkins dashboard for the first time using this initial password.</span></span>

![將 Jenkins 解除鎖定](./media/install-jenkins-solution-template/jenkins-unlock.png)

<span data-ttu-id="9294d-136">在下一個頁面上選取 [安裝建議的外掛程式]，然後建立用來存取 Jenkins 儀表板的 Jenkins 系統管理使用者。</span><span class="sxs-lookup"><span data-stu-id="9294d-136">Select **Install suggested plugins** on the next page and then create a Jenkins admin user used to access the Jenkins dashboard.</span></span>

![Jenkins 已就緒！](./media/install-jenkins-solution-template/jenkins-welcome.png)

<span data-ttu-id="9294d-138">Jenkins 伺服器現在已準備要建置程式碼。</span><span class="sxs-lookup"><span data-stu-id="9294d-138">The Jenkins server is now ready to build code.</span></span>

## <a name="create-your-first-job"></a><span data-ttu-id="9294d-139">建立您的第一個作業</span><span class="sxs-lookup"><span data-stu-id="9294d-139">Create your first job</span></span>

<span data-ttu-id="9294d-140">從 Jenkins 主控台選取 [建立新的作業]，然後將它命名為 **mySampleApp** 並選取 [自由樣式專案]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="9294d-140">Select **Create new jobs** from the Jenkins console, then name it **mySampleApp** and select **Freestyle project**, then select **OK**.</span></span>

![建立新的作業](./media/install-jenkins-solution-template/jenkins-new-job.png) 

<span data-ttu-id="9294d-142">選取 [原始程式碼管理] 索引標籤，啟用 [Git]，並且在 [存放庫 URL] 欄位中輸入下列 URL：`https://github.com/spring-guides/gs-spring-boot.git`</span><span class="sxs-lookup"><span data-stu-id="9294d-142">Select the **Source Code Management** tab, enable **Git**, and enter the following URL in **Repository URL**  field: `https://github.com/spring-guides/gs-spring-boot.git`</span></span>

![建立 Git 存放庫](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

<span data-ttu-id="9294d-144">選取 [建置] 索引標籤，然後選取 [新增建置步驟]、[叫用 Gradle 指令碼]。</span><span class="sxs-lookup"><span data-stu-id="9294d-144">Select the **Build** tab, then select **Add build step**, **Invoke Gradle script**.</span></span> <span data-ttu-id="9294d-145">選取 [使用 Gradle 包裝函式]，然後在 [包裝函式位置] 中輸入 `complete` 並輸入 `build` 作為 [工作]。</span><span class="sxs-lookup"><span data-stu-id="9294d-145">Select **Use Gradle Wrapper**, then enter `complete` in **Wrapper location** and `build` for **Tasks**.</span></span>

![使用要建置的 Gradle 包裝函式](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

<span data-ttu-id="9294d-147">選取 [進階...]</span><span class="sxs-lookup"><span data-stu-id="9294d-147">Select **Advanced..**</span></span> <span data-ttu-id="9294d-148">然後在 [根組建指令碼] 欄位中輸入 `complete`。</span><span class="sxs-lookup"><span data-stu-id="9294d-148">and then enter `complete` in the **Root Build script** field.</span></span> <span data-ttu-id="9294d-149">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="9294d-149">Select **Save**.</span></span>

![在 Gradle 包裝函式建置步驟中設定進階設定](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-the-code"></a><span data-ttu-id="9294d-151">建置程式碼</span><span class="sxs-lookup"><span data-stu-id="9294d-151">Build the code</span></span>

<span data-ttu-id="9294d-152">選取 [立即建置] 以編譯程式碼和封裝範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="9294d-152">Select **Build Now** to compile the code and package the sample app.</span></span> <span data-ttu-id="9294d-153">當您的組建完成時，選取專案的 [工作區] 連結。</span><span class="sxs-lookup"><span data-stu-id="9294d-153">When your build completes, select the **Workspace** link for the project.</span></span>

![瀏覽至可從組建取得 JAR 檔案的工作區](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

<span data-ttu-id="9294d-155">瀏覽至 `complete/build/libs`，並確定 `gs-spring-boot-0.1.0.jar` 在那裡以確認您的組建成功。</span><span class="sxs-lookup"><span data-stu-id="9294d-155">Navigate to `complete/build/libs` and ensure the `gs-spring-boot-0.1.0.jar` is there to verify that your build was successful.</span></span> <span data-ttu-id="9294d-156">您的 Jenkins 伺服器現在已準備要在 Azure 中建置自己的專案。</span><span class="sxs-lookup"><span data-stu-id="9294d-156">Your Jenkins server is now ready to build your own projects in Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9294d-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9294d-157">Next Steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9294d-158">新增 Azure VM 作為 Jenkins 代理程式</span><span class="sxs-lookup"><span data-stu-id="9294d-158">Add Azure VMs as Jenkins agents</span></span>](jenkins-azure-vm-agents.md)
