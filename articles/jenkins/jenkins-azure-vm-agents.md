---
title: "與 Jenkins 連續整合 aaaUse Azure VM 代理程式。"
description: "Azure VM 代理程式作為 Jenkins 從屬。"
services: multiple
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 2388e6919d0280372166fbd325d80dafb00d7550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a><span data-ttu-id="566fd-103">使用 Azure VM 代理程式與 Jenkins 持續整合。</span><span class="sxs-lookup"><span data-stu-id="566fd-103">Use Azure VM agents for continuous integration with Jenkins.</span></span>

<span data-ttu-id="566fd-104">本快速入門示範如何 toouse 會 hello Jenkins Azure VM 代理程式外掛程式 toocreate 隨 Linux (Ubuntu) 代理程式在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="566fd-104">This quickstart shows how toouse hello Jenkins Azure VM Agents plugin toocreate an on-demand Linux (Ubuntu) agent in Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="566fd-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="566fd-105">Prerequisites</span></span>

<span data-ttu-id="566fd-106">toocomplete 本快速入門：</span><span class="sxs-lookup"><span data-stu-id="566fd-106">toocomplete this quickstart:</span></span>

* <span data-ttu-id="566fd-107">如果您還沒有 Jenkins master，就可以開始 hello[方案範本](install-jenkins-solution-template.md)</span><span class="sxs-lookup"><span data-stu-id="566fd-107">If you do not already have a Jenkins master, you can start with hello [Solution Template](install-jenkins-solution-template.md)</span></span> 
* <span data-ttu-id="566fd-108">請參閱太[使用 Azure CLI 2.0 建立 Azure 服務主體](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json)如果您還沒有 Azure 服務主體。</span><span class="sxs-lookup"><span data-stu-id="566fd-108">Refer too[Create an Azure Service principal with Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) if you do not already have an Azure service principal.</span></span>

## <a name="install-azure-vm-agents-plugin"></a><span data-ttu-id="566fd-109">安裝 Azure VM 代理程式外掛程式</span><span class="sxs-lookup"><span data-stu-id="566fd-109">Install Azure VM Agents plugin</span></span>

<span data-ttu-id="566fd-110">如果您從 hello 啟動[方案範本](install-jenkins-solution-template.md)，會安裝在 hello Jenkins master 中的 hello Azure VM 代理程式外掛程式。</span><span class="sxs-lookup"><span data-stu-id="566fd-110">If you start from hello [Solution Template](install-jenkins-solution-template.md), hello Azure VM Agent plugin is installed in hello Jenkins master.</span></span>

<span data-ttu-id="566fd-111">否則，安裝 hello **Azure VM 代理程式**hello Jenkins 儀表板中的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="566fd-111">Otherwise, install hello **Azure VM Agents** plugin from within hello Jenkins dashboard.</span></span>

## <a name="configure-hello-plugin"></a><span data-ttu-id="566fd-112">設定 hello 外掛程式</span><span class="sxs-lookup"><span data-stu-id="566fd-112">Configure hello plugin</span></span>

* <span data-ttu-id="566fd-113">在 hello Jenkins 儀表板內，按一下**管理 Jenkins-> 設定系統->** 。</span><span class="sxs-lookup"><span data-stu-id="566fd-113">Within hello Jenkins dashboard, click **Manage Jenkins -> Configure System ->**.</span></span> <span data-ttu-id="566fd-114">捲動 toohello hello 頁面的底部，找出與 hello 下拉式清單中的 hello 區段**加入新的雲端**。</span><span class="sxs-lookup"><span data-stu-id="566fd-114">Scroll toohello bottom of hello page and find hello section with hello dropdown **Add new cloud**.</span></span> <span data-ttu-id="566fd-115">從 [hello] 功能表中，選取**Microsoft Azure VM 代理程式**</span><span class="sxs-lookup"><span data-stu-id="566fd-115">From hello menu, select **Microsoft Azure VM Agents**</span></span>
* <span data-ttu-id="566fd-116">從 hello Azure 認證下拉式清單中選取現有的帳戶。</span><span class="sxs-lookup"><span data-stu-id="566fd-116">Select an existing account from hello Azure Credentials dropdown.</span></span>  <span data-ttu-id="566fd-117">新的 tooadd **Microsoft Azure 服務主體，**輸入 hello 下列值： 訂用帳戶 ID、 用戶端識別碼、 用戶端密碼和 OAuth 2.0 權杖端點。</span><span class="sxs-lookup"><span data-stu-id="566fd-117">tooadd a new **Microsoft Azure Service Principal,** enter hello following values: Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span>

![Azure 認證](./media/jenkins-azure-vm-agents/service-principal.png)

* <span data-ttu-id="566fd-119">按一下**確認組態**toomake hello 設定檔設定是否正確。</span><span class="sxs-lookup"><span data-stu-id="566fd-119">Click **Verify configuration** toomake sure that hello profile configuration is correct.</span></span>
* <span data-ttu-id="566fd-120">儲存 hello 組態，並繼續 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="566fd-120">Save hello configuration, and continue toohello next step.</span></span>

## <a name="template-configuration"></a><span data-ttu-id="566fd-121">範本設定</span><span class="sxs-lookup"><span data-stu-id="566fd-121">Template configuration</span></span>

### <a name="general-configuration"></a><span data-ttu-id="566fd-122">一般設定</span><span class="sxs-lookup"><span data-stu-id="566fd-122">General configuration</span></span>
<span data-ttu-id="566fd-123">接著，設定使用 toodefine Azure VM 代理程式的範本。</span><span class="sxs-lookup"><span data-stu-id="566fd-123">Next, configure a template for use toodefine an Azure VM agent.</span></span> 

* <span data-ttu-id="566fd-124">按一下**新增**tooadd 範本。</span><span class="sxs-lookup"><span data-stu-id="566fd-124">Click **Add** tooadd a template.</span></span> 
* <span data-ttu-id="566fd-125">提供新範本的名稱。</span><span class="sxs-lookup"><span data-stu-id="566fd-125">Provide a name for your new template.</span></span> 
* <span data-ttu-id="566fd-126">為 hello 標籤，請輸入"ubuntu。 」</span><span class="sxs-lookup"><span data-stu-id="566fd-126">For hello label, enter  "ubuntu."</span></span> <span data-ttu-id="566fd-127">此標籤還可用於 hello 工作設定。</span><span class="sxs-lookup"><span data-stu-id="566fd-127">This label is used during hello job configuration.</span></span>
* <span data-ttu-id="566fd-128">從 hello 下拉式方塊中選取 hello 所需的區域。</span><span class="sxs-lookup"><span data-stu-id="566fd-128">Select hello desired region from hello combo box.</span></span>
* <span data-ttu-id="566fd-129">選取 hello 所需的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="566fd-129">Select hello desired VM size.</span></span>
* <span data-ttu-id="566fd-130">指定 hello Azure 儲存體帳戶名稱，或保持空白 toouse hello 預設名稱 「 jenkinsarmst。 」</span><span class="sxs-lookup"><span data-stu-id="566fd-130">Specify hello Azure Storage account name or leave it blank toouse hello default name "jenkinsarmst."</span></span>
* <span data-ttu-id="566fd-131">指定以分鐘為單位的 hello 保留時間。</span><span class="sxs-lookup"><span data-stu-id="566fd-131">Specify hello retention time in minutes.</span></span> <span data-ttu-id="566fd-132">此設定會定義 hello Jenkins 可以自動刪除閒置的代理程式之前等待的分鐘數。</span><span class="sxs-lookup"><span data-stu-id="566fd-132">This setting defines hello number of minutes Jenkins can wait before automatically deleting an idle agent.</span></span> <span data-ttu-id="566fd-133">如果您不想自動刪除閒置的代理程式 toobe，指定為 0。</span><span class="sxs-lookup"><span data-stu-id="566fd-133">Specify 0 if you do not want idle agents toobe deleted automatically.</span></span>

![一般設定](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a><span data-ttu-id="566fd-135">映像設定</span><span class="sxs-lookup"><span data-stu-id="566fd-135">Image configuration</span></span>

<span data-ttu-id="566fd-136">toocreate Linux (Ubuntu) 代理程式中，選取**映像參考**並使用 hello 遵循組態的範例。</span><span class="sxs-lookup"><span data-stu-id="566fd-136">toocreate a Linux (Ubuntu) agent, select **Image reference** and use hello following configuration as an example.</span></span> <span data-ttu-id="566fd-137">請參閱太[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) hello 最新的 Azure 支援映像。</span><span class="sxs-lookup"><span data-stu-id="566fd-137">Refer too[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) for hello latest Azure supported images.</span></span>

* <span data-ttu-id="566fd-138">映像發佈者︰Canonical</span><span class="sxs-lookup"><span data-stu-id="566fd-138">Image Publisher: Canonical</span></span>
* <span data-ttu-id="566fd-139">映像提供：UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="566fd-139">Image Offer: UbuntuServer</span></span>
* <span data-ttu-id="566fd-140">映像 Sku：14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="566fd-140">Image Sku: 14.04.5-LTS</span></span>
* <span data-ttu-id="566fd-141">映像版本：最新</span><span class="sxs-lookup"><span data-stu-id="566fd-141">Image version: latest</span></span>
* <span data-ttu-id="566fd-142">OS 類型：Linux</span><span class="sxs-lookup"><span data-stu-id="566fd-142">OS Type: Linux</span></span>
* <span data-ttu-id="566fd-143">啟動方法：SSH</span><span class="sxs-lookup"><span data-stu-id="566fd-143">Launch method: SSH</span></span>
* <span data-ttu-id="566fd-144">提供管理員認證</span><span class="sxs-lookup"><span data-stu-id="566fd-144">Provide an admin credentials</span></span>
* <span data-ttu-id="566fd-145">針對 VM 初始化指令碼，請輸入：</span><span class="sxs-lookup"><span data-stu-id="566fd-145">For VM initialization script, enter:</span></span>
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![映像設定](./media/jenkins-azure-vm-agents/image-config.png)

* <span data-ttu-id="566fd-147">按一下**驗證範本**tooverify hello 組態。</span><span class="sxs-lookup"><span data-stu-id="566fd-147">Click **Verify Template** tooverify hello configuration.</span></span>
* <span data-ttu-id="566fd-148">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="566fd-148">Click **Save**.</span></span>

## <a name="create-a-job-in-jenkins"></a><span data-ttu-id="566fd-149">在 Jenkins 中建立作業</span><span class="sxs-lookup"><span data-stu-id="566fd-149">Create a job in Jenkins</span></span>

* <span data-ttu-id="566fd-150">在 hello Jenkins 儀表板內，按一下**新項目**。</span><span class="sxs-lookup"><span data-stu-id="566fd-150">Within hello Jenkins dashboard, click **New Item**.</span></span> 
* <span data-ttu-id="566fd-151">輸入名稱並選取 [Freestyle 專案]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="566fd-151">Enter a name and select **Freestyle project** and click **OK**.</span></span>
* <span data-ttu-id="566fd-152">在 hello**一般**索引標籤、 選取"限制可以執行專案"和"ubuntu"標籤運算式中的型別。</span><span class="sxs-lookup"><span data-stu-id="566fd-152">In hello **General** tab, select "Restrict where project can be run" and type "ubuntu" in Label Expression.</span></span> <span data-ttu-id="566fd-153">現在，您會看到 「 ubuntu"hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="566fd-153">You now see "ubuntu" in hello dropdown.</span></span>
* <span data-ttu-id="566fd-154">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="566fd-154">Click **Save**.</span></span>

![設定作業](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a><span data-ttu-id="566fd-156">建置新專案</span><span class="sxs-lookup"><span data-stu-id="566fd-156">Build your new project</span></span>

* <span data-ttu-id="566fd-157">返回 toohello Jenkins 儀表板。</span><span class="sxs-lookup"><span data-stu-id="566fd-157">Go back toohello Jenkins dashboard.</span></span>
* <span data-ttu-id="566fd-158">Hello 新工作時，以滑鼠右鍵按一下您建立群組，然後按一下 **現在就建置**。</span><span class="sxs-lookup"><span data-stu-id="566fd-158">Right-click hello new job you created, then click **Build now**.</span></span> <span data-ttu-id="566fd-159">隨即開始建置。</span><span class="sxs-lookup"><span data-stu-id="566fd-159">A build is kicked off.</span></span> 
* <span data-ttu-id="566fd-160">Hello 建置完成之後，請跳過**主控台輸出**。</span><span class="sxs-lookup"><span data-stu-id="566fd-160">Once hello build is complete, go too**Console output**.</span></span> <span data-ttu-id="566fd-161">您會看到 hello 建置在 Azure 上已從遠端執行。</span><span class="sxs-lookup"><span data-stu-id="566fd-161">You see that hello build was performed remotely on Azure.</span></span>

![主控台輸出](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a><span data-ttu-id="566fd-163">參考</span><span class="sxs-lookup"><span data-stu-id="566fd-163">Reference</span></span>

* <span data-ttu-id="566fd-164">Azure 星期五視訊：[使用 Azure VM 代理程式與 Jenkins 持續整合](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span><span class="sxs-lookup"><span data-stu-id="566fd-164">Azure Friday video: [Continuous Integration with Jenkins using Azure VM agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span></span>
* <span data-ttu-id="566fd-165">支援資訊和設定選項：[Azure VM 代理程式 Jenkins 外掛程式 Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span><span class="sxs-lookup"><span data-stu-id="566fd-165">Support information and configuration options:  [Azure VM Agent Jenkins Plugin Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span></span> 

