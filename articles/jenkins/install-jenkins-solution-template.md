---
title: "在 Azure 上的 Jenkins 伺服器 aaaCreate"
description: "Jenkins Azure Linux 虛擬機器上安裝從 hello Jenkins 解決方案範本和建置範例的 Java 應用程式。"
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 82ab2ac52594acba131414b449b608978591d4b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-hello-azure-portal"></a><span data-ttu-id="29279-103">從 Azure 入口網站 hello Azure Linux VM 上建立 Jenkins 伺服器</span><span class="sxs-lookup"><span data-stu-id="29279-103">Create a Jenkins server on an Azure Linux VM from hello Azure portal</span></span>

<span data-ttu-id="29279-104">本快速入門示範如何 tooinstall [Jenkins](https://jenkins.io) hello 工具和外掛程式設定 toowork Ubuntu Linux VM，使用 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="29279-104">This quickstart shows how tooinstall [Jenkins](https://jenkins.io) on an Ubuntu Linux VM with hello tools and plug-ins configured toowork with Azure.</span></span> <span data-ttu-id="29279-105">當您完成時，您可讓在 Azure 中執行的 Jenkins 伺服器從 [GitHub](https://github.com) 建置範例 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="29279-105">When you're finished, you have a Jenkins server running in Azure building a sample Java app from [GitHub](https://github.com).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29279-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="29279-106">Prerequisites</span></span>

* <span data-ttu-id="29279-107">Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="29279-107">An Azure subscription</span></span>
* <span data-ttu-id="29279-108">電腦的命令列上的存取 tooSSH (例如 hello 撞殼層或[PuTTY](http://www.putty.org/))</span><span class="sxs-lookup"><span data-stu-id="29279-108">Access tooSSH on your computer's command line (such as hello Bash shell or [PuTTY](http://www.putty.org/))</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-jenkins-vm-from-hello-solution-template"></a><span data-ttu-id="29279-109">建立 hello Jenkins VM 從 hello 方案範本</span><span class="sxs-lookup"><span data-stu-id="29279-109">Create hello Jenkins VM from hello solution template</span></span>

<span data-ttu-id="29279-110">開啟 hello [marketplace 映像的 Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview)在 web 瀏覽器，然後選取**現在取得 IT**從左邊 hello 頁面 hello。</span><span class="sxs-lookup"><span data-stu-id="29279-110">Open hello [marketplace image for Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) in your web browser and select  **GET IT NOW** from hello left-hand side of hello page.</span></span> <span data-ttu-id="29279-111">檢閱 hello 定價詳細資料，然後選取**繼續**，然後選取**建立**tooconfigure hello Jenkins 伺服器 hello Azure 入口網站中的。</span><span class="sxs-lookup"><span data-stu-id="29279-111">Review hello pricing details and select **Continue**, then select **Create** tooconfigure hello Jenkins server in hello Azure portal.</span></span> 
   
![Azure 入口網站對話方塊](./media/install-jenkins-solution-template/ap-create.png)

<span data-ttu-id="29279-113">在 hello**設定基本設定**索引標籤上，填寫下列欄位的 hello:</span><span class="sxs-lookup"><span data-stu-id="29279-113">In hello **Configure basic settings** tab, fill in hello following fields:</span></span>

![設定基本設定](./media/install-jenkins-solution-template/ap-basic.png)

* <span data-ttu-id="29279-115">使用 **Jenkins** 作為 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="29279-115">Use **Jenkins** for **Name**.</span></span>
* <span data-ttu-id="29279-116">輸入 [使用者名稱]。</span><span class="sxs-lookup"><span data-stu-id="29279-116">Enter a **User name**.</span></span> <span data-ttu-id="29279-117">hello 使用者名稱必須符合[特定需求](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm)。</span><span class="sxs-lookup"><span data-stu-id="29279-117">hello user name must meet [specific requirements](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span></span>
* <span data-ttu-id="29279-118">選取**密碼**為 hello**驗證類型**並輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="29279-118">Select **Password** as hello **Authentication type** and enter a password.</span></span> <span data-ttu-id="29279-119">hello 密碼必須包含大寫字元、 數字和一個特殊字元。</span><span class="sxs-lookup"><span data-stu-id="29279-119">hello password must have an upper case character, a number, and one special character.</span></span>
* <span data-ttu-id="29279-120">使用**myJenkinsResourceGroup** hello**資源群組**。</span><span class="sxs-lookup"><span data-stu-id="29279-120">Use **myJenkinsResourceGroup** for hello **Resource Group**.</span></span>
* <span data-ttu-id="29279-121">選擇 hello**美國東部** [Azure 地區](https://azure.microsoft.com/regions/)從 hello**位置**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="29279-121">Choose hello **East US** [Azure region](https://azure.microsoft.com/regions/) from hello **Location** drop-down.</span></span>

<span data-ttu-id="29279-122">選取**確定**tooproceed toohello**設定額外選項** 索引標籤。請輸入唯一的網域名稱 tooidentify hello Jenkins 伺服器並選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="29279-122">Select **OK** tooproceed toohello **Configure additional options** tab. Enter a unique domain name tooidentify hello Jenkins server and select **OK**.</span></span>

![設定其他選項](./media/install-jenkins-solution-template/ap-addtional.png)  

 <span data-ttu-id="29279-124">一旦驗證通過時，選取**確定**再次從 hello**摘要** 索引標籤。最後，選取**購買**toocreate hello Jenkins VM。</span><span class="sxs-lookup"><span data-stu-id="29279-124">Once validation passes, select **OK** again from hello **Summary** tab. Finally, select **Purchase** toocreate hello Jenkins VM.</span></span> <span data-ttu-id="29279-125">準備您的伺服器時，您會收到 hello Azure 入口網站中的通知：</span><span class="sxs-lookup"><span data-stu-id="29279-125">When your server is ready, you get a notification in hello Azure portal:</span></span>   

![Jenkins 已就緒通知](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-toojenkins"></a><span data-ttu-id="29279-127">連接 tooJenkins</span><span class="sxs-lookup"><span data-stu-id="29279-127">Connect tooJenkins</span></span>

<span data-ttu-id="29279-128">在網頁瀏覽器中，瀏覽 tooyour 虛擬機器 (例如，http://jenkins2517454.eastus.cloudapp.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="29279-128">Navigate tooyour virtual machine (for example, http://jenkins2517454.eastus.cloudapp.azure.com/) in  your web browser.</span></span> <span data-ttu-id="29279-129">hello Jenkins 主控台是無法透過不安全的 HTTP 存取，因此 hello 頁面 tooaccess hello Jenkins 主控台上安全地從您的電腦使用 SSH 通道會提供指示。</span><span class="sxs-lookup"><span data-stu-id="29279-129">hello Jenkins console is inaccessible through unsecured HTTP so instructions are provided on hello page tooaccess hello Jenkins console securely from your computer using an SSH tunnel.</span></span>

![將 Jenkins 解除鎖定](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

<span data-ttu-id="29279-131">設定使用 hello hello 通道`ssh`命令在 hello 頁面上，從 hello 命令列取代`username`hello hello hello 虛擬機器設定從 hello 方案範本時，請選擇先前的虛擬機器系統管理員使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="29279-131">Set up hello tunnel using hello `ssh` command on hello page from hello command line, replacing `username` with hello name of hello virtual machine admin user chosen earlier when setting up hello virtual machine from hello solution template.</span></span>

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

<span data-ttu-id="29279-132">啟動 hello 通道後，瀏覽 toohttp://localhost:8080 / 在本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="29279-132">After you have started hello tunnel, navigate toohttp://localhost:8080/ on your local machine.</span></span> 

<span data-ttu-id="29279-133">執行下列命令，透過 SSH toohello Jenkins VM 連線時，hello 命令列中的 hello 取得 hello 初始密碼。</span><span class="sxs-lookup"><span data-stu-id="29279-133">Get hello initial password by running hello following command in hello command line while connected through SSH toohello Jenkins VM.</span></span>

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

<span data-ttu-id="29279-134">解除鎖定 hello hello 的 Jenkins 儀表板第一次使用此初始密碼。</span><span class="sxs-lookup"><span data-stu-id="29279-134">Unlock hello Jenkins dashboard for hello first time using this initial password.</span></span>

![將 Jenkins 解除鎖定](./media/install-jenkins-solution-template/jenkins-unlock.png)

<span data-ttu-id="29279-136">選取**安裝建議的外掛程式**hello 在下一個頁面上，然後再建立 Jenkins 管理使用者使用 tooaccess hello Jenkins 儀表板。</span><span class="sxs-lookup"><span data-stu-id="29279-136">Select **Install suggested plugins** on hello next page and then create a Jenkins admin user used tooaccess hello Jenkins dashboard.</span></span>

![Jenkins 已就緒！](./media/install-jenkins-solution-template/jenkins-welcome.png)

<span data-ttu-id="29279-138">hello Jenkins 伺服器現在是準備 toobuild 程式碼。</span><span class="sxs-lookup"><span data-stu-id="29279-138">hello Jenkins server is now ready toobuild code.</span></span>

## <a name="create-your-first-job"></a><span data-ttu-id="29279-139">建立您的第一個作業</span><span class="sxs-lookup"><span data-stu-id="29279-139">Create your first job</span></span>

<span data-ttu-id="29279-140">選取**建立新的作業**從 hello Jenkins 主控台，然後命名**mySampleApp**選取**Freestyle 專案**，然後選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="29279-140">Select **Create new jobs** from hello Jenkins console, then name it **mySampleApp** and select **Freestyle project**, then select **OK**.</span></span>

![建立新的作業](./media/install-jenkins-solution-template/jenkins-new-job.png) 

<span data-ttu-id="29279-142">選取 hello**原始程式碼管理**索引標籤上，啟用**Git**，並輸入下列 URL 中的 hello**儲存機制 URL**欄位：`https://github.com/spring-guides/gs-spring-boot.git`</span><span class="sxs-lookup"><span data-stu-id="29279-142">Select hello **Source Code Management** tab, enable **Git**, and enter hello following URL in **Repository URL**  field: `https://github.com/spring-guides/gs-spring-boot.git`</span></span>

![定義 hello Git 儲存機制](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

<span data-ttu-id="29279-144">選取 hello**建置**索引標籤，然後選取**加入建置步驟**，**叫用的 Gradle 指令碼**。</span><span class="sxs-lookup"><span data-stu-id="29279-144">Select hello **Build** tab, then select **Add build step**, **Invoke Gradle script**.</span></span> <span data-ttu-id="29279-145">選取 [使用 Gradle 包裝函式]，然後在 [包裝函式位置] 中輸入 `complete` 並輸入 `build` 作為 [工作]。</span><span class="sxs-lookup"><span data-stu-id="29279-145">Select **Use Gradle Wrapper**, then enter `complete` in **Wrapper location** and `build` for **Tasks**.</span></span>

![使用 hello Gradle 包裝函式 toobuild](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

<span data-ttu-id="29279-147">選取 [進階...]</span><span class="sxs-lookup"><span data-stu-id="29279-147">Select **Advanced..**</span></span> <span data-ttu-id="29279-148">然後輸入`complete`在 hello**根建置指令碼**欄位。</span><span class="sxs-lookup"><span data-stu-id="29279-148">and then enter `complete` in hello **Root Build script** field.</span></span> <span data-ttu-id="29279-149">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="29279-149">Select **Save**.</span></span>

![在 hello Gradle 包裝函式建置步驟中設定進階的設定](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-hello-code"></a><span data-ttu-id="29279-151">建置 hello 的程式碼</span><span class="sxs-lookup"><span data-stu-id="29279-151">Build hello code</span></span>

<span data-ttu-id="29279-152">選取**現在建置**toocompile hello 程式碼和套件 hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="29279-152">Select **Build Now** toocompile hello code and package hello sample app.</span></span> <span data-ttu-id="29279-153">您的組建完成時，選取 hello**工作區**hello 專案的連結。</span><span class="sxs-lookup"><span data-stu-id="29279-153">When your build completes, select hello **Workspace** link for hello project.</span></span>

![瀏覽 toohello 區 tooget hello JAR 檔案從 hello 組建](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

<span data-ttu-id="29279-155">瀏覽過`complete/build/libs`，並確定 hello`gs-spring-boot-0.1.0.jar`有 tooverify 組建是否成功。</span><span class="sxs-lookup"><span data-stu-id="29279-155">Navigate too`complete/build/libs` and ensure hello `gs-spring-boot-0.1.0.jar` is there tooverify that your build was successful.</span></span> <span data-ttu-id="29279-156">您 Jenkins 伺服器現在已準備好 toobuild 自己在 Azure 中的專案。</span><span class="sxs-lookup"><span data-stu-id="29279-156">Your Jenkins server is now ready toobuild your own projects in Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29279-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="29279-157">Next Steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="29279-158">新增 Azure VM 作為 Jenkins 代理程式</span><span class="sxs-lookup"><span data-stu-id="29279-158">Add Azure VMs as Jenkins agents</span></span>](jenkins-azure-vm-agents.md)
