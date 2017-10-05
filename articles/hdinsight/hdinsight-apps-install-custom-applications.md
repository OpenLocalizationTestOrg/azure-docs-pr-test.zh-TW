---
title: "在 Azure HDInsight 上安裝您自己的 Hadoop 應用程式 | Microsoft Docs"
description: "了解如何在 HDInsight 應用程式上安裝 HDInsight 應用程式。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e556b29c-8176-4bc5-a90b-aa01abfd3aee
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ebec29dea9f5dc1767f47a53d9da03347a51de28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="install-custom-hadoop-applications-on-azure-hdinsight"></a><span data-ttu-id="67894-103">在 Azure HDInsight 上安裝自訂 Hadoop 應用程式</span><span class="sxs-lookup"><span data-stu-id="67894-103">Install custom Hadoop applications on Azure HDInsight</span></span>

<span data-ttu-id="67894-104">在本文中，您將學習如何在 Azure HDInsight 上安裝尚未發佈至 Azure 入口網站的 Hadoop 應用程式。</span><span class="sxs-lookup"><span data-stu-id="67894-104">In this article, you will learn how to install a Hadoop application on Azure HDInsight, which has not been published to the Azure portal.</span></span> <span data-ttu-id="67894-105">在本文中，您將安裝的應用程式是 [Hue](http://gethue.com/)。</span><span class="sxs-lookup"><span data-stu-id="67894-105">The application you will install in this article is [Hue](http://gethue.com/).</span></span>

<span data-ttu-id="67894-106">HDInsight 應用程式是使用者可以在以 Linux 為基礎的 HDInsight 叢集上安裝的應用程式。</span><span class="sxs-lookup"><span data-stu-id="67894-106">An HDInsight application is an application that users can install on a Linux-based HDInsight cluster.</span></span>  <span data-ttu-id="67894-107">Microsoft 獨立軟體廠商 (ISV) 或您可以自己開發這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="67894-107">These applications can be developed by Microsoft, independent software vendors (ISV) or by yourself.</span></span>  

<span data-ttu-id="67894-108">如需其他相關文章，請參閱：</span><span class="sxs-lookup"><span data-stu-id="67894-108">Other related articles:</span></span>

* <span data-ttu-id="67894-109">[安裝 HDInsight 應用程式](hdinsight-apps-install-applications.md)︰了解如何將 HDInsight 應用程式安裝到您的叢集。</span><span class="sxs-lookup"><span data-stu-id="67894-109">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how to install an HDInsight application to your clusters.</span></span>
* <span data-ttu-id="67894-110">[發佈 HDInsight 應用程式](hdinsight-apps-publish-applications.md)︰了解如何將自訂 HDInsight 應用程式發佈至 Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="67894-110">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how to publish your custom HDInsight applications to Azure Marketplace.</span></span>
* <span data-ttu-id="67894-111">[MSDN：安裝 HDInsight 應用程式](https://msdn.microsoft.com/library/mt706515.aspx)︰了解如何定義 HDInsight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="67894-111">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how to define HDInsight applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67894-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="67894-112">Prerequisites</span></span>
<span data-ttu-id="67894-113">如果您想要在現有的 HDInsight 叢集上安裝 HDInsight 應用程式，您必須有 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="67894-113">If you want to install HDInsight applications on an existing HDInsight cluster, you must have an HDInsight cluster.</span></span> <span data-ttu-id="67894-114">若要建立叢集，請參閱 [建立叢集](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster)。</span><span class="sxs-lookup"><span data-stu-id="67894-114">To create one, see [Create clusters](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span> <span data-ttu-id="67894-115">您也可以在建立 HDInsight 叢集時安裝 HDInsight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="67894-115">You can also install HDInsight applications when you create an HDInsight cluster.</span></span>

## <a name="install-hdinsight-applications"></a><span data-ttu-id="67894-116">安裝 HDInsight 應用程式</span><span class="sxs-lookup"><span data-stu-id="67894-116">Install HDInsight applications</span></span>
<span data-ttu-id="67894-117">HDInsight 應用程式可以在您建立叢集時安裝，或安裝至現有的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="67894-117">HDInsight applications can be installed when you create a cluster or to an existing HDInsight cluster.</span></span> <span data-ttu-id="67894-118">如需定義 Azure Resource Manager 範本，請參閱 [MSDN：安裝 HDInsight 應用程式](https://msdn.microsoft.com/library/mt706515.aspx)。</span><span class="sxs-lookup"><span data-stu-id="67894-118">For defining Azure Resource Manager templates, see [MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx).</span></span>

<span data-ttu-id="67894-119">部署此應用程式 (Hue) 所需的檔案︰</span><span class="sxs-lookup"><span data-stu-id="67894-119">The files needed for deploying this application (Hue):</span></span>

* <span data-ttu-id="67894-120">[azuredeploy.json](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/azuredeploy.json)：可供安裝 HDInsight 應用程式的 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="67894-120">[azuredeploy.json](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/azuredeploy.json): The Resource Manager template for installing HDInsight application.</span></span> <span data-ttu-id="67894-121">如需開發您自己的 Resource Manager 範本，請參閱 [MSDN：安裝 HDInsight 應用程式](https://msdn.microsoft.com/library/mt706515.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="67894-121">See [MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx) for developing your own Resource Manager template.</span></span>
* <span data-ttu-id="67894-122">[hue-install_v0.sh](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/scripts/Hue-install_v0.sh)：Resource Manager 範本為了設定邊緣節點所呼叫的指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="67894-122">[hue-install_v0.sh](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/scripts/Hue-install_v0.sh): The Script action being called by the Resource Manager template for configuring the edge node.</span></span>
* <span data-ttu-id="67894-123">[hue-binaries.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz)︰從 hui-install_v0.sh 呼叫的 Hue 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="67894-123">[hue-binaries.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): The hue binary file being called from hui-install_v0.sh.</span></span>
* <span data-ttu-id="67894-124">[hue-binaries-14-04.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz)︰從 hui-install_v0.sh 呼叫的 Hue 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="67894-124">[hue-binaries-14-04.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): The hue binary file being called from hui-install_v0.sh.</span></span>
* <span data-ttu-id="67894-125">[webwasb-tomcat.tar.gz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/webwasb-tomcat.tar.gz)：從 hui-install_v0.sh 呼叫的範例 Web 應用程式 (Tomcat)。</span><span class="sxs-lookup"><span data-stu-id="67894-125">[webwasb-tomcat.tar.gz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/webwasb-tomcat.tar.gz): A sample web application (Tomcat) being called from hui-install_v0.sh.</span></span>

<span data-ttu-id="67894-126">**將 Hue 安裝至現有的 HDInsight 叢集**</span><span class="sxs-lookup"><span data-stu-id="67894-126">**To install Hue to an existing HDInsight cluster**</span></span>

1. <span data-ttu-id="67894-127">按一下以下影像，在 Azure 入口網站中登入 Azure 並開啟 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="67894-127">Click the following image to sign in to Azure and open the Resource Manager template in the Azure Portal.</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2FIaas-Applications%2Fmaster%2FHue%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy to Azure"></a>

    <span data-ttu-id="67894-128">此按鈕會在 Azure 入口網站上開啟 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="67894-128">This button opens a Resource Manager template on the Azure portal.</span></span>  <span data-ttu-id="67894-129">Resource Manager 範本位於 [https://github.com/hdinsight/Iaas-Applications/tree/master/Hue](https://github.com/hdinsight/Iaas-Applications/tree/master/Hue)。</span><span class="sxs-lookup"><span data-stu-id="67894-129">The Resource Manager template is located at [https://github.com/hdinsight/Iaas-Applications/tree/master/Hue](https://github.com/hdinsight/Iaas-Applications/tree/master/Hue).</span></span>  <span data-ttu-id="67894-130">若要了解如何撰寫此 Resource Manager 範本，請參閱 [MSDN：安裝 HDInsight 應用程式](https://msdn.microsoft.com/library/mt706515.aspx)。</span><span class="sxs-lookup"><span data-stu-id="67894-130">To learn how to write this Resource Manager template, see [MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx).</span></span>
2. <span data-ttu-id="67894-131">從 [參數]  刀鋒視窗，輸入下列項目：</span><span class="sxs-lookup"><span data-stu-id="67894-131">From the **Parameters** blade, enter the following:</span></span>

   * <span data-ttu-id="67894-132">**ClusterName**：輸入您要安裝應用程式的叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="67894-132">**ClusterName**: Enter the name of the cluster where you want to install the application.</span></span> <span data-ttu-id="67894-133">此叢集必須是現有的叢集。</span><span class="sxs-lookup"><span data-stu-id="67894-133">This cluster must be an existing cluster.</span></span>
3. <span data-ttu-id="67894-134">按一下 [確定]  儲存參數。</span><span class="sxs-lookup"><span data-stu-id="67894-134">Click **OK** to save the parameters.</span></span>
4. <span data-ttu-id="67894-135">從 [自訂部署] 刀鋒視窗，輸入 [資源群組]。</span><span class="sxs-lookup"><span data-stu-id="67894-135">From the **Custom deployment** blade, enter **Resource group**.</span></span>  <span data-ttu-id="67894-136">資源群組是聚集叢集、相依儲存體帳戶和其他資源的容器。</span><span class="sxs-lookup"><span data-stu-id="67894-136">The resource group is a container that groups the cluster, the dependent storage account and other resources.</span></span> <span data-ttu-id="67894-137">必須使用與叢集相同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="67894-137">It is required to use the same resource group as the cluster.</span></span>
5. <span data-ttu-id="67894-138">按一下 [法律條款]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="67894-138">Click **Legal terms**, and then click **Create**.</span></span>
6. <span data-ttu-id="67894-139">確認已選取 [釘選到儀表板] 核取方塊，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="67894-139">Verify the **Pin to dashboard** checkbox is selected, and then click **Create**.</span></span> <span data-ttu-id="67894-140">您可以從釘選到入口網站儀表板和入口網站通知的圖格查看安裝狀態 (按一下入口網站頂端的鈴鐺圖示)。</span><span class="sxs-lookup"><span data-stu-id="67894-140">You can see the installation status from the tile pinned to the portal dashboard and the portal notification (click the bell icon on the top of the portal).</span></span>  <span data-ttu-id="67894-141">安裝此應用程式需要 10 分鐘左右。</span><span class="sxs-lookup"><span data-stu-id="67894-141">It takes about 10 minutes to install the application.</span></span>

<span data-ttu-id="67894-142">**在建立叢集時安裝 Hue**</span><span class="sxs-lookup"><span data-stu-id="67894-142">**To install Hue while creating a cluster**</span></span>

1. <span data-ttu-id="67894-143">按一下以下影像，在 Azure 入口網站中登入 Azure 並開啟 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="67894-143">Click the following image to sign in to Azure and open the Resource Manager template in the Azure Portal.</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhdinsightapps%2Fcreate-linux-based-hadoop-cluster-in-hdinsight.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy to Azure"></a>

    <span data-ttu-id="67894-144">此按鈕會在 Azure 入口網站上開啟 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="67894-144">This button opens a Resource Manager template on the Azure portal.</span></span>  <span data-ttu-id="67894-145">Resource Manager 範本位於 [https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json](https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json)。</span><span class="sxs-lookup"><span data-stu-id="67894-145">The Resource Manager template is located at [https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json](https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json).</span></span>  <span data-ttu-id="67894-146">若要了解如何撰寫此 Resource Manager 範本，請參閱 [MSDN：安裝 HDInsight 應用程式](https://msdn.microsoft.com/library/mt706515.aspx)。</span><span class="sxs-lookup"><span data-stu-id="67894-146">To learn how to write this Resource Manager template, see [MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx).</span></span>
2. <span data-ttu-id="67894-147">請依照指示來建立叢集和安裝 Hue。</span><span class="sxs-lookup"><span data-stu-id="67894-147">Follow the instruction to create cluster and install Hue.</span></span> <span data-ttu-id="67894-148">如需建立 HDInsight 叢集的詳細資訊，請參閱 [在 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="67894-148">For more information on creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="67894-149">除了 Azure 入口網站，您也可以使用 [Azure PowerShell](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-powershell) 和 [Azure CLI](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-cli) 來呼叫 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="67894-149">In addition to the Azure portal, you can also use [Azure PowerShell](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-powershell) and [Azure CLI](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-cli) to call Resource Manager templates.</span></span>

## <a name="validate-the-installation"></a><span data-ttu-id="67894-150">驗證安裝</span><span class="sxs-lookup"><span data-stu-id="67894-150">Validate the installation</span></span>
<span data-ttu-id="67894-151">您可以在 Azure 入口網站上檢查應用程式狀態以驗證應用程式安裝。</span><span class="sxs-lookup"><span data-stu-id="67894-151">You can check the application status on the Azure portal to validate the application installation.</span></span> <span data-ttu-id="67894-152">此外，您也可以驗證所有如預期般出現的 HTTP 端點及網頁 (如果有的話)︰</span><span class="sxs-lookup"><span data-stu-id="67894-152">In addition, you can also validate all HTTP endpoints came up as expected and the webpage if there is one:</span></span>

<span data-ttu-id="67894-153">**開啟 Hue 入口網站**</span><span class="sxs-lookup"><span data-stu-id="67894-153">**To open the Hue portal**</span></span>

1. <span data-ttu-id="67894-154">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="67894-154">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="67894-155">按一下左側功能表中的 [HDInsight 叢集]  。</span><span class="sxs-lookup"><span data-stu-id="67894-155">Click **HDInsight Clusters** in the left menu.</span></span>  <span data-ttu-id="67894-156">如果沒有看到該功能表，請按一下 [瀏覽]，然後按一下 [HDInsight 叢集]。</span><span class="sxs-lookup"><span data-stu-id="67894-156">If you don't see it, click **Browse**, and then click **HDInsight Clusters**.</span></span>
3. <span data-ttu-id="67894-157">按一下您已安裝應用程式的叢集。</span><span class="sxs-lookup"><span data-stu-id="67894-157">Click the cluster where you installed the application.</span></span>
4. <span data-ttu-id="67894-158">在 [設定] 刀鋒視窗中，按一下 [一般] 類別之下的 [應用程式]。</span><span class="sxs-lookup"><span data-stu-id="67894-158">From the **Settings** blade, click **Applications** under the **General** category.</span></span> <span data-ttu-id="67894-159">您應該會看到 **Hue** 列在 [已安裝的應用程式] 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="67894-159">You shall see **hue** listed in the **Installed Apps** blade.</span></span>
5. <span data-ttu-id="67894-160">按一下清單中的 **Hue** 以列出相關屬性。</span><span class="sxs-lookup"><span data-stu-id="67894-160">Click **hue** from the list to list the properties.</span></span>  
6. <span data-ttu-id="67894-161">按一下 [網頁] 連結來驗證網站；在瀏覽器中開啟 HTTP 端點以驗證 Hue Web UI，使用 SSH 開啟 SSH 端點。</span><span class="sxs-lookup"><span data-stu-id="67894-161">Click the Webpage link to validate the website; open the HTTP endpoint in a browser to validate the Hue web UI, open the SSH endpoint using SSH.</span></span> <span data-ttu-id="67894-162">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="67894-162">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="troubleshoot-the-installation"></a><span data-ttu-id="67894-163">安裝疑難排解</span><span class="sxs-lookup"><span data-stu-id="67894-163">Troubleshoot the installation</span></span>
<span data-ttu-id="67894-164">您可以從入口網站通知檢查應用程式安裝狀態 (按一下入口網站頂端的鈴鐺圖示)。</span><span class="sxs-lookup"><span data-stu-id="67894-164">You can check the application installation status from the portal notification (Click the bell icon on the top of the portal).</span></span>

<span data-ttu-id="67894-165">如果應用程式安裝失敗，您可以從 3 個地方查看錯誤訊息和偵錯資訊︰</span><span class="sxs-lookup"><span data-stu-id="67894-165">If an application installation failed, you can see the error messages and debug information from 3 places:</span></span>

* <span data-ttu-id="67894-166">HDInsight 應用程式︰一般錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="67894-166">HDInsight Applications: general error information.</span></span>

    <span data-ttu-id="67894-167">從入口網站中開啟叢集，然後從 [設定] 刀鋒視窗按一下 [應用程式]︰</span><span class="sxs-lookup"><span data-stu-id="67894-167">Open the cluster from the portal, and click Applications from the Settings blade:</span></span>

    ![hdinsight 應用程式的應用程式安裝錯誤](./media/hdinsight-apps-install-applications/hdinsight-apps-error.png)
* <span data-ttu-id="67894-169">HDInsight 指令碼動作︰如果 HDInsight 應用程式的錯誤訊息指出指令碼動作失敗，則 [指令碼動作] 窗格會顯示指令碼失敗的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="67894-169">HDInsight script action: If the HDInsight Applications' error message indicates a script action failure, more details about the script failure will be presented in the script actions pane.</span></span>

    <span data-ttu-id="67894-170">從 [設定] 刀鋒視窗按一下 [指令碼動作]。</span><span class="sxs-lookup"><span data-stu-id="67894-170">Click Script Action from the Settings blade.</span></span> <span data-ttu-id="67894-171">指令碼動作歷程記錄會顯示錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="67894-171">Script action history shows the error messages</span></span>

    ![hdinsight 應用程式的指令碼動作錯誤](./media/hdinsight-apps-install-applications/hdinsight-apps-script-action-error.png)
* <span data-ttu-id="67894-173">Ambari Web UI︰如果安裝指令碼是失敗的原因，請使用 Ambari Web UI 來檢查有關安裝指令碼的完整記錄檔。</span><span class="sxs-lookup"><span data-stu-id="67894-173">Ambari Web UI: If the install script was the cause of the failure, use Ambari Web UI to check full logs about the install scripts.</span></span>

    <span data-ttu-id="67894-174">如需詳細資訊，請參閱 [疑難排解](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)。</span><span class="sxs-lookup"><span data-stu-id="67894-174">For more information, see [Troubleshooting](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting).</span></span>

## <a name="remove-hdinsight-applications"></a><span data-ttu-id="67894-175">移除 HDInsight 應用程式</span><span class="sxs-lookup"><span data-stu-id="67894-175">Remove HDInsight applications</span></span>
<span data-ttu-id="67894-176">有幾種方式可以刪除 HDInsight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="67894-176">There are several ways to delete HDInsight applications.</span></span>

### <a name="use-portal"></a><span data-ttu-id="67894-177">使用入口網站</span><span class="sxs-lookup"><span data-stu-id="67894-177">Use portal</span></span>
<span data-ttu-id="67894-178">**使用入口網站移除應用程式**</span><span class="sxs-lookup"><span data-stu-id="67894-178">**To remove an application using the portal**</span></span>

1. <span data-ttu-id="67894-179">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="67894-179">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="67894-180">按一下左側功能表中的 [HDInsight 叢集]  。</span><span class="sxs-lookup"><span data-stu-id="67894-180">Click **HDInsight Clusters** in the left menu.</span></span>  <span data-ttu-id="67894-181">如果沒有看到該功能表，請按一下 [瀏覽]，然後按一下 [HDInsight 叢集]。</span><span class="sxs-lookup"><span data-stu-id="67894-181">If you don't see it, click **Browse**, and then click **HDInsight Clusters**.</span></span>
3. <span data-ttu-id="67894-182">按一下您已安裝應用程式的叢集。</span><span class="sxs-lookup"><span data-stu-id="67894-182">Click the cluster where you installed the application.</span></span>
4. <span data-ttu-id="67894-183">在 [設定] 刀鋒視窗中，按一下 [一般] 類別之下的 [應用程式]。</span><span class="sxs-lookup"><span data-stu-id="67894-183">From the **Settings** blade, click **Applications** under the **General** category.</span></span> <span data-ttu-id="67894-184">您應該會看到已安裝的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="67894-184">You shall see a list of installed application.</span></span> <span data-ttu-id="67894-185">在此教學課程中，**hue** 列在 [已安裝的應用程式] 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="67894-185">For this tutorial, **hue** listed in the **Installed Apps** blade.</span></span>
5. <span data-ttu-id="67894-186">以滑鼠右鍵按一下您想要移除的應用程式，然後按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="67894-186">Right-click the application you want to remove, and then click **Delete**.</span></span>
6. <span data-ttu-id="67894-187">按一下 [ **是** ] 以確認。</span><span class="sxs-lookup"><span data-stu-id="67894-187">Click **Yes** to confirm.</span></span>

<span data-ttu-id="67894-188">在入口網站中，您也可以刪除叢集，或刪除包含應用程式的資源群組。</span><span class="sxs-lookup"><span data-stu-id="67894-188">From the portal, you can also delete the cluster or delete the resource group which contains the application.</span></span>

### <a name="use-azure-powershell"></a><span data-ttu-id="67894-189">使用 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="67894-189">Use Azure PowerShell</span></span>
<span data-ttu-id="67894-190">使用 Azure PowerShell，您就可以刪除叢集或刪除資源群組。</span><span class="sxs-lookup"><span data-stu-id="67894-190">Using Azure PowerShell, you can delete the cluster or delete the resource group.</span></span> <span data-ttu-id="67894-191">請參閱 [使用 Azure PowerShell 刪除叢集](hdinsight-administer-use-powershell.md#delete-clusters)。</span><span class="sxs-lookup"><span data-stu-id="67894-191">See [Delete clusters by using Azure PowerShell](hdinsight-administer-use-powershell.md#delete-clusters).</span></span>

### <a name="use-azure-cli"></a><span data-ttu-id="67894-192">使用 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="67894-192">Use Azure CLI</span></span>
<span data-ttu-id="67894-193">使用 Azure CLI，您就可以刪除叢集或刪除資源群組。</span><span class="sxs-lookup"><span data-stu-id="67894-193">Using Azure CLI, you can delete the cluster or delete the resource group.</span></span> <span data-ttu-id="67894-194">請參閱 [使用 Azure CLI 刪除叢集](hdinsight-administer-use-command-line.md#delete-clusters)。</span><span class="sxs-lookup"><span data-stu-id="67894-194">See [Delete clusters by using Azure CLI](hdinsight-administer-use-command-line.md#delete-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="67894-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="67894-195">Next steps</span></span>
* <span data-ttu-id="67894-196">[MSDN：安裝 HDInsight 應用程式](https://msdn.microsoft.com/library/mt706515.aspx)︰了解如何開發 Resource Manager 範本以供部署 HDInsight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="67894-196">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): learn how to develop Resource Manager templates for deploying HDInsight applications.</span></span>
* <span data-ttu-id="67894-197">[安裝 HDInsight 應用程式](hdinsight-apps-install-applications.md)︰了解如何將 HDInsight 應用程式安裝到您的叢集。</span><span class="sxs-lookup"><span data-stu-id="67894-197">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how to install an HDInsight application to your clusters.</span></span>
* <span data-ttu-id="67894-198">[發佈 HDInsight 應用程式](hdinsight-apps-publish-applications.md)︰了解如何將自訂 HDInsight 應用程式發佈至 Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="67894-198">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how to publish your custom HDInsight applications to Azure Marketplace.</span></span>
* <span data-ttu-id="67894-199">[使用指令碼動作自訂以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)：了解如何使用指令碼動作來安裝其他應用程式。</span><span class="sxs-lookup"><span data-stu-id="67894-199">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): learn how to use Script Action to install additional applications.</span></span>
* <span data-ttu-id="67894-200">[使用 Resource Manager 範本在 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集](hdinsight-hadoop-create-linux-clusters-arm-templates.md)︰了解如何呼叫 Resource Manager 範本來建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="67894-200">[Create Linux-based Hadoop clusters in HDInsight using Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md): learn how to call Resource Manager templates to create HDInsight clusters.</span></span>
* <span data-ttu-id="67894-201">[在 HDInsight 中使用空白邊緣節點](hdinsight-apps-use-edge-node.md)︰了解如何使用空白邊緣節點來存取 HDInsight 叢集、測試 HDInsight 應用程式，以及裝載 HDInsight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="67894-201">[Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md): learn how to use an empty edge node for accessing HDInsight cluster, testing HDInsight applications, and hosting HDInsight applications.</span></span>
