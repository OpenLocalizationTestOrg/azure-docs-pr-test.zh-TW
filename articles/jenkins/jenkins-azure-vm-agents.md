---
title: "使用 Azure VM 代理程式與 Jenkins 持續整合。"
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
ms.openlocfilehash: 0b22a559fbc03158a6d4398603d1a7d2874d7b67
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a><span data-ttu-id="b1d23-103">使用 Azure VM 代理程式與 Jenkins 持續整合。</span><span class="sxs-lookup"><span data-stu-id="b1d23-103">Use Azure VM agents for continuous integration with Jenkins.</span></span>

<span data-ttu-id="b1d23-104">本快速入門示範如何在 Azure 中使用 Jenkins Azure VM 代理程式外掛程式來建立隨選 Linux (Ubuntu) 代理程式。</span><span class="sxs-lookup"><span data-stu-id="b1d23-104">This quickstart shows how to use the Jenkins Azure VM Agents plugin to create an on-demand Linux (Ubuntu) agent in Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1d23-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="b1d23-105">Prerequisites</span></span>

<span data-ttu-id="b1d23-106">若要完成本快速入門：</span><span class="sxs-lookup"><span data-stu-id="b1d23-106">To complete this quickstart:</span></span>

* <span data-ttu-id="b1d23-107">如果您還沒有 Jenkins Master，可以開始使用[解決方案範本](install-jenkins-solution-template.md)</span><span class="sxs-lookup"><span data-stu-id="b1d23-107">If you do not already have a Jenkins master, you can start with the [Solution Template](install-jenkins-solution-template.md)</span></span> 
* <span data-ttu-id="b1d23-108">如果您還沒有 Azure 服務主體，請參閱[使用 Azure CLI 2.0 建立 Azure 服務主體](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b1d23-108">Refer to [Create an Azure Service principal with Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) if you do not already have an Azure service principal.</span></span>

## <a name="install-azure-vm-agents-plugin"></a><span data-ttu-id="b1d23-109">安裝 Azure VM 代理程式外掛程式</span><span class="sxs-lookup"><span data-stu-id="b1d23-109">Install Azure VM Agents plugin</span></span>

<span data-ttu-id="b1d23-110">如果您是從[解決方案範本](install-jenkins-solution-template.md)開始，Azure VM 代理程式會安裝在 Jenkins Master 中。</span><span class="sxs-lookup"><span data-stu-id="b1d23-110">If you start from the [Solution Template](install-jenkins-solution-template.md), the Azure VM Agent plugin is installed in the Jenkins master.</span></span>

<span data-ttu-id="b1d23-111">否則，從 Jenkins 儀表板內安裝 **Azure VM 代理程式**外掛程式。</span><span class="sxs-lookup"><span data-stu-id="b1d23-111">Otherwise, install the **Azure VM Agents** plugin from within the Jenkins dashboard.</span></span>

## <a name="configure-the-plugin"></a><span data-ttu-id="b1d23-112">設定外掛程式</span><span class="sxs-lookup"><span data-stu-id="b1d23-112">Configure the plugin</span></span>

* <span data-ttu-id="b1d23-113">在 Jenkins 儀表板中，按一下 [管理 Jenkins] -> [設定系統] ->。</span><span class="sxs-lookup"><span data-stu-id="b1d23-113">Within the Jenkins dashboard, click **Manage Jenkins -> Configure System ->**.</span></span> <span data-ttu-id="b1d23-114">捲動到頁面底部，並尋找包含 [新增雲端] 下拉式清單的區段。</span><span class="sxs-lookup"><span data-stu-id="b1d23-114">Scroll to the bottom of the page and find the section with the dropdown **Add new cloud**.</span></span> <span data-ttu-id="b1d23-115">從功能表中，選取 **Microsoft Azure VM 代理程式**</span><span class="sxs-lookup"><span data-stu-id="b1d23-115">From the menu, select **Microsoft Azure VM Agents**</span></span>
* <span data-ttu-id="b1d23-116">從 Azure 認證下拉式清單中選取現有的帳戶。</span><span class="sxs-lookup"><span data-stu-id="b1d23-116">Select an existing account from the Azure Credentials dropdown.</span></span>  <span data-ttu-id="b1d23-117">若要新增新的 **Microsoft Azure 服務主體，**請輸入下列值：訂用帳戶識別碼、用戶端識別碼、用戶端密碼和 OAuth 2.0 權杖端點。</span><span class="sxs-lookup"><span data-stu-id="b1d23-117">To add a new **Microsoft Azure Service Principal,** enter the following values: Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span>

![Azure 認證](./media/jenkins-azure-vm-agents/service-principal.png)

* <span data-ttu-id="b1d23-119">按一下 [確認設定]，確定設定檔設定是否正確。</span><span class="sxs-lookup"><span data-stu-id="b1d23-119">Click **Verify configuration** to make sure that the profile configuration is correct.</span></span>
* <span data-ttu-id="b1d23-120">儲存設定，然後繼續下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="b1d23-120">Save the configuration, and continue to the next step.</span></span>

## <a name="template-configuration"></a><span data-ttu-id="b1d23-121">範本設定</span><span class="sxs-lookup"><span data-stu-id="b1d23-121">Template configuration</span></span>

### <a name="general-configuration"></a><span data-ttu-id="b1d23-122">一般設定</span><span class="sxs-lookup"><span data-stu-id="b1d23-122">General configuration</span></span>
<span data-ttu-id="b1d23-123">接著，設定用來定義 Azure VM 代理程式的範本。</span><span class="sxs-lookup"><span data-stu-id="b1d23-123">Next, configure a template for use to define an Azure VM agent.</span></span> 

* <span data-ttu-id="b1d23-124">按一下 [新增]可新增範本。</span><span class="sxs-lookup"><span data-stu-id="b1d23-124">Click **Add** to add a template.</span></span> 
* <span data-ttu-id="b1d23-125">提供新範本的名稱。</span><span class="sxs-lookup"><span data-stu-id="b1d23-125">Provide a name for your new template.</span></span> 
* <span data-ttu-id="b1d23-126">針對標籤，請輸入 "ubuntu"。</span><span class="sxs-lookup"><span data-stu-id="b1d23-126">For the label, enter  "ubuntu."</span></span> <span data-ttu-id="b1d23-127">會在作業設定期間使用此標籤。</span><span class="sxs-lookup"><span data-stu-id="b1d23-127">This label is used during the job configuration.</span></span>
* <span data-ttu-id="b1d23-128">從下拉式方塊中選取所需的區域。</span><span class="sxs-lookup"><span data-stu-id="b1d23-128">Select the desired region from the combo box.</span></span>
* <span data-ttu-id="b1d23-129">選取所需的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="b1d23-129">Select the desired VM size.</span></span>
* <span data-ttu-id="b1d23-130">指定 Azure 儲存體帳戶名稱或保持空白，就會使用預設名稱 "jenkinsarmst"。</span><span class="sxs-lookup"><span data-stu-id="b1d23-130">Specify the Azure Storage account name or leave it blank to use the default name "jenkinsarmst."</span></span>
* <span data-ttu-id="b1d23-131">指定保留時間 (以分鐘為單位)。</span><span class="sxs-lookup"><span data-stu-id="b1d23-131">Specify the retention time in minutes.</span></span> <span data-ttu-id="b1d23-132">此設定會定義自動刪除閒置的代理程式之前，Jenkins 可以等待的分鐘數。</span><span class="sxs-lookup"><span data-stu-id="b1d23-132">This setting defines the number of minutes Jenkins can wait before automatically deleting an idle agent.</span></span> <span data-ttu-id="b1d23-133">如果您不想要自動刪除閒置的代理程式，可以指定 0。</span><span class="sxs-lookup"><span data-stu-id="b1d23-133">Specify 0 if you do not want idle agents to be deleted automatically.</span></span>

![一般設定](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a><span data-ttu-id="b1d23-135">映像設定</span><span class="sxs-lookup"><span data-stu-id="b1d23-135">Image configuration</span></span>

<span data-ttu-id="b1d23-136">若要建立 Linux (Ubuntu) 代理程式，請選取 [映像參考]，並使用下列設定作為範例。</span><span class="sxs-lookup"><span data-stu-id="b1d23-136">To create a Linux (Ubuntu) agent, select **Image reference** and use the following configuration as an example.</span></span> <span data-ttu-id="b1d23-137">請參閱 [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) 以取得最新版的 Azure 支援映像。</span><span class="sxs-lookup"><span data-stu-id="b1d23-137">Refer to [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) for the latest Azure supported images.</span></span>

* <span data-ttu-id="b1d23-138">映像發佈者︰Canonical</span><span class="sxs-lookup"><span data-stu-id="b1d23-138">Image Publisher: Canonical</span></span>
* <span data-ttu-id="b1d23-139">映像提供：UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="b1d23-139">Image Offer: UbuntuServer</span></span>
* <span data-ttu-id="b1d23-140">映像 Sku：14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="b1d23-140">Image Sku: 14.04.5-LTS</span></span>
* <span data-ttu-id="b1d23-141">映像版本：最新</span><span class="sxs-lookup"><span data-stu-id="b1d23-141">Image version: latest</span></span>
* <span data-ttu-id="b1d23-142">OS 類型：Linux</span><span class="sxs-lookup"><span data-stu-id="b1d23-142">OS Type: Linux</span></span>
* <span data-ttu-id="b1d23-143">啟動方法：SSH</span><span class="sxs-lookup"><span data-stu-id="b1d23-143">Launch method: SSH</span></span>
* <span data-ttu-id="b1d23-144">提供管理員認證</span><span class="sxs-lookup"><span data-stu-id="b1d23-144">Provide an admin credentials</span></span>
* <span data-ttu-id="b1d23-145">針對 VM 初始化指令碼，請輸入：</span><span class="sxs-lookup"><span data-stu-id="b1d23-145">For VM initialization script, enter:</span></span>
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![映像設定](./media/jenkins-azure-vm-agents/image-config.png)

* <span data-ttu-id="b1d23-147">按一下 [驗證範本] 以確認設定。</span><span class="sxs-lookup"><span data-stu-id="b1d23-147">Click **Verify Template** to verify the configuration.</span></span>
* <span data-ttu-id="b1d23-148">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b1d23-148">Click **Save**.</span></span>

## <a name="create-a-job-in-jenkins"></a><span data-ttu-id="b1d23-149">在 Jenkins 中建立作業</span><span class="sxs-lookup"><span data-stu-id="b1d23-149">Create a job in Jenkins</span></span>

* <span data-ttu-id="b1d23-150">在 Jenkins 儀表板中，按一下 [新增項目] 。</span><span class="sxs-lookup"><span data-stu-id="b1d23-150">Within the Jenkins dashboard, click **New Item**.</span></span> 
* <span data-ttu-id="b1d23-151">輸入名稱並選取 [Freestyle 專案]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b1d23-151">Enter a name and select **Freestyle project** and click **OK**.</span></span>
* <span data-ttu-id="b1d23-152">在 [一般] 索引標籤中，選取 [限制可執行專案的位置] 並在標籤運算式中輸入 "ubuntu"。</span><span class="sxs-lookup"><span data-stu-id="b1d23-152">In the **General** tab, select "Restrict where project can be run" and type "ubuntu" in Label Expression.</span></span> <span data-ttu-id="b1d23-153">現在，您會在下拉式清單中看到 "ubuntu"。</span><span class="sxs-lookup"><span data-stu-id="b1d23-153">You now see "ubuntu" in the dropdown.</span></span>
* <span data-ttu-id="b1d23-154">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b1d23-154">Click **Save**.</span></span>

![設定作業](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a><span data-ttu-id="b1d23-156">建置新專案</span><span class="sxs-lookup"><span data-stu-id="b1d23-156">Build your new project</span></span>

* <span data-ttu-id="b1d23-157">返回 Jenkins 儀表板。</span><span class="sxs-lookup"><span data-stu-id="b1d23-157">Go back to the Jenkins dashboard.</span></span>
* <span data-ttu-id="b1d23-158">以滑鼠右鍵按一下您所建立的新作業，然後按一下 [立即建置]。</span><span class="sxs-lookup"><span data-stu-id="b1d23-158">Right-click the new job you created, then click **Build now**.</span></span> <span data-ttu-id="b1d23-159">隨即開始建置。</span><span class="sxs-lookup"><span data-stu-id="b1d23-159">A build is kicked off.</span></span> 
* <span data-ttu-id="b1d23-160">當建置完成之後，請移至 [主控台輸出]。</span><span class="sxs-lookup"><span data-stu-id="b1d23-160">Once the build is complete, go to **Console output**.</span></span> <span data-ttu-id="b1d23-161">您會看到在 Azure 上看到建置在遠端執行。</span><span class="sxs-lookup"><span data-stu-id="b1d23-161">You see that the build was performed remotely on Azure.</span></span>

![主控台輸出](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a><span data-ttu-id="b1d23-163">參考</span><span class="sxs-lookup"><span data-stu-id="b1d23-163">Reference</span></span>

* <span data-ttu-id="b1d23-164">Azure 星期五視訊：[使用 Azure VM 代理程式與 Jenkins 持續整合](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span><span class="sxs-lookup"><span data-stu-id="b1d23-164">Azure Friday video: [Continuous Integration with Jenkins using Azure VM agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span></span>
* <span data-ttu-id="b1d23-165">支援資訊和設定選項：[Azure VM 代理程式 Jenkins 外掛程式 Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span><span class="sxs-lookup"><span data-stu-id="b1d23-165">Support information and configuration options:  [Azure VM Agent Jenkins Plugin Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span></span> 

