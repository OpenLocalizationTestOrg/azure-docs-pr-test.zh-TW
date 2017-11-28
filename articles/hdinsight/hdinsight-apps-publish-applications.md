---
title: "發行 HDInsight 應用程式 - Azure | Microsoft Docs"
description: "了解如何建立和發佈 HDInsight 應用程式。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 14aef891-7a37-4cf1-8f7d-ca923565c783
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 6aa66cac35bc317fc87003e6c3d824544c53de88
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="publish-hdinsight-applications-into-the-azure-marketplace"></a><span data-ttu-id="d18e2-103">將 HDInsight 應用程式發佈到 Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="d18e2-103">Publish HDInsight applications into the Azure Marketplace</span></span>
<span data-ttu-id="d18e2-104">HDInsight 應用程式是使用者可以在以 Linux 為基礎的 HDInsight 叢集上安裝的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d18e2-104">An HDInsight application is an application that users can install on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="d18e2-105">Microsoft 獨立軟體廠商 (ISV) 或您可以自己開發這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="d18e2-105">These applications can be developed by Microsoft, independent software vendors (ISV) or by yourself.</span></span> <span data-ttu-id="d18e2-106">在此文章中，您會學習如何將 HDInsight 應用程式發佈到 Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="d18e2-106">In this article, you learn how to publish an HDInsight application into the Azure Marketplace.</span></span>  <span data-ttu-id="d18e2-107">如需發佈到 Azure Marketplace 的一般資訊，請參閱[將提供項目發佈到 Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="d18e2-107">For general information about publishing into the Azure Marketplace, see [publish an offer to the Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="d18e2-108">HDInsight 應用程式採用「自備授權 (BYOL)」模型，其中的應用程式提供者負責將應用程式授權給一般使用者，而 Azure 只會向一般使用者收取其所建資源的費用，例如 HDInsight 叢集與其 VM/節點。</span><span class="sxs-lookup"><span data-stu-id="d18e2-108">HDInsight applications use the *Bring Your Own License (BYOL)* model, where application provider is responsible for licensing the application to end-users, and end-users are only charged by Azure for the resources they create, such as the HDInsight cluster and its VMs/nodes.</span></span> <span data-ttu-id="d18e2-109">目前，Azure 不經手應用程式本身的計費。</span><span class="sxs-lookup"><span data-stu-id="d18e2-109">Currently, billing for the application itself is not done through Azure.</span></span>

<span data-ttu-id="d18e2-110">其他 HDInsight 應用程式相關文章︰</span><span class="sxs-lookup"><span data-stu-id="d18e2-110">Other HDInsight application-related article:</span></span>

* <span data-ttu-id="d18e2-111">[安裝 HDInsight 應用程式](hdinsight-apps-install-applications.md)︰了解如何將 HDInsight 應用程式安裝到您的叢集。</span><span class="sxs-lookup"><span data-stu-id="d18e2-111">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how to install an HDInsight application to your clusters.</span></span>
* <span data-ttu-id="d18e2-112">[安裝自訂 HDInsight 應用程式](hdinsight-apps-install-custom-applications.md)︰了解如何安裝和測試自訂 HDInsight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d18e2-112">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): Learn how to install and test custom HDInsight applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d18e2-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="d18e2-113">Prerequisites</span></span>
<span data-ttu-id="d18e2-114">若要將自訂應用程式提交至 Marketplace，您必須建立並測試您的自訂應用程式。</span><span class="sxs-lookup"><span data-stu-id="d18e2-114">To submit your custom application to the marketplace, you must have created and tested your custom application.</span></span> <span data-ttu-id="d18e2-115">請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="d18e2-115">See the following articles:</span></span>

* <span data-ttu-id="d18e2-116">[安裝自訂 HDInsight 應用程式](hdinsight-apps-install-custom-applications.md)︰了解如何安裝和測試自訂 HDInsight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d18e2-116">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): Learn how to install and test custom HDInsight applications.</span></span>

<span data-ttu-id="d18e2-117">您還必須註冊開發人員帳戶。</span><span class="sxs-lookup"><span data-stu-id="d18e2-117">You must also have registered your developer account.</span></span> <span data-ttu-id="d18e2-118">請參閱[將提供項目發佈到 Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md) 和[建立 Microsoft 開發人員帳戶](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="d18e2-118">See [publish an offer to the Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md) and [Create a Microsoft Developer account](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).</span></span>

## <a name="define-application"></a><span data-ttu-id="d18e2-119">定義應用程式</span><span class="sxs-lookup"><span data-stu-id="d18e2-119">Define application</span></span>
<span data-ttu-id="d18e2-120">將應用程式發佈至 Azure Marketplace 涉及兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="d18e2-120">There are two steps involved for publishing applications to the Azure Marketplace.</span></span>  <span data-ttu-id="d18e2-121">首先，定義 **createUiDef.json** 檔，以指出與您的應用程式相容的叢集，然後從 Azure 入口網站發佈範本。</span><span class="sxs-lookup"><span data-stu-id="d18e2-121">First you define a **createUiDef.json** file to indicate which clusters your application is compatible with; and then you publish the template from the Azure portal.</span></span> <span data-ttu-id="d18e2-122">下一節是範例 createUiDef.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="d18e2-122">The following section is a sample createUiDef.json file.</span></span>

    {
        "handler": "Microsoft.HDInsight",
        "version": "0.0.1-preview",
        "clusterFilters": {
            "types": ["Hadoop", "HBase", "Storm", "Spark"],
            "tiers": ["Standard", "Premium"],
            "versions": ["3.4"]
        }
    }


| <span data-ttu-id="d18e2-123">欄位</span><span class="sxs-lookup"><span data-stu-id="d18e2-123">Field</span></span> | <span data-ttu-id="d18e2-124">描述</span><span class="sxs-lookup"><span data-stu-id="d18e2-124">Description</span></span> | <span data-ttu-id="d18e2-125">可能的值</span><span class="sxs-lookup"><span data-stu-id="d18e2-125">Possible values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d18e2-126">types</span><span class="sxs-lookup"><span data-stu-id="d18e2-126">types</span></span> |<span data-ttu-id="d18e2-127">與應用程式相容的叢集類型。</span><span class="sxs-lookup"><span data-stu-id="d18e2-127">The cluster types that the application is compatible with.</span></span> |<span data-ttu-id="d18e2-128">Hadoop、HBase、Storm、Spark (或這些類型的任意組合)</span><span class="sxs-lookup"><span data-stu-id="d18e2-128">Hadoop, HBase, Storm, Spark, (or any combination of these)</span></span> |
| <span data-ttu-id="d18e2-129">tiers</span><span class="sxs-lookup"><span data-stu-id="d18e2-129">tiers</span></span> |<span data-ttu-id="d18e2-130">與應用程式相容的叢集層。</span><span class="sxs-lookup"><span data-stu-id="d18e2-130">The cluster tiers that the application is compatible with.</span></span> |<span data-ttu-id="d18e2-131">Standard、Premium (或兩者)</span><span class="sxs-lookup"><span data-stu-id="d18e2-131">Standard, Premium, (or both)</span></span> |
| <span data-ttu-id="d18e2-132">versions</span><span class="sxs-lookup"><span data-stu-id="d18e2-132">versions</span></span> |<span data-ttu-id="d18e2-133">與應用程式相容的 HDInsight 叢集類型。</span><span class="sxs-lookup"><span data-stu-id="d18e2-133">The HDInsight cluster types that the application is compatible with.</span></span> |<span data-ttu-id="d18e2-134">3.4</span><span class="sxs-lookup"><span data-stu-id="d18e2-134">3.4</span></span> |

## <a name="application-install-script"></a><span data-ttu-id="d18e2-135">應用程式安裝指令碼</span><span class="sxs-lookup"><span data-stu-id="d18e2-135">Application install script</span></span>
<span data-ttu-id="d18e2-136">每當應用程式安裝在 (現有或新的) 叢集上，就會在叢集上安裝邊緣節點並執行應用程式安裝指令碼。</span><span class="sxs-lookup"><span data-stu-id="d18e2-136">Whenever an application is installed on a cluster (either an existing one or a new one), an edge node is created and the application install script is run on it.</span></span>
  > [!IMPORTANT]
  > <span data-ttu-id="d18e2-137">應用程式安裝指令碼的名稱必須是特定叢集中唯一的名稱 (採用以下的格式)。</span><span class="sxs-lookup"><span data-stu-id="d18e2-137">The name of the application install script names must be unique for a particular cluster with the following format.</span></span>
  > 
  > <span data-ttu-id="d18e2-138">name": "[concat('hue-install-v0','-' ,uniquestring(‘applicationName’)]"</span><span class="sxs-lookup"><span data-stu-id="d18e2-138">name": "[concat('hue-install-v0','-' ,uniquestring(‘applicationName’)]"</span></span>
  > 
  > <span data-ttu-id="d18e2-139">請注意，指令碼名稱有三個部分︰</span><span class="sxs-lookup"><span data-stu-id="d18e2-139">Note there are three parts to the script name:</span></span>
  > 
  > 1. <span data-ttu-id="d18e2-140">指令碼名稱前置應該包含應用程式名稱或與該應用程式相關的名稱。</span><span class="sxs-lookup"><span data-stu-id="d18e2-140">A script name prefix, which shall include either the application name or a name relevant to the application.</span></span>
  > 2. <span data-ttu-id="d18e2-141">"-" 以方便閱讀。</span><span class="sxs-lookup"><span data-stu-id="d18e2-141">A "-" for readability.</span></span>
  > 3. <span data-ttu-id="d18e2-142">唯一的字串函數，並以應用程式名稱做為參數。</span><span class="sxs-lookup"><span data-stu-id="d18e2-142">A unique string function with the application name as the parameter.</span></span>
  > 
  > <span data-ttu-id="d18e2-143">範例如上，結果為在保存的指令碼動作清單中的 hue-install-v0-4wkahss55hlas。</span><span class="sxs-lookup"><span data-stu-id="d18e2-143">An example is the above ends up becoming: hue-install-v0-4wkahss55hlas in the persisted script action list.</span></span> <span data-ttu-id="d18e2-144">如需 JSON 承載的範例，請參閱 [https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json](https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="d18e2-144">For a sample JSON payload, see [https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json](https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json).</span></span>
  > 
<span data-ttu-id="d18e2-145">安裝指令碼必須具有下列特性：</span><span class="sxs-lookup"><span data-stu-id="d18e2-145">The installation script must have the following characteristics:</span></span>
1. <span data-ttu-id="d18e2-146">確定指令碼具有等冪性。</span><span class="sxs-lookup"><span data-stu-id="d18e2-146">Ensure that the script is idempotent.</span></span> <span data-ttu-id="d18e2-147">指令碼的多個呼叫應產生相同的結果。</span><span class="sxs-lookup"><span data-stu-id="d18e2-147">Multiple calls to the script should produce the same result.</span></span>
2. <span data-ttu-id="d18e2-148">指令碼必須是正確版本。</span><span class="sxs-lookup"><span data-stu-id="d18e2-148">The script should be properly versioned.</span></span> <span data-ttu-id="d18e2-149">當您升級或測試變更時，請為指令碼使用不同位置，以便嘗試安裝應用程式的客戶不會受到影響。</span><span class="sxs-lookup"><span data-stu-id="d18e2-149">Use a different location for the script when you are upgrading or testing out changes so that customers that are trying to install the application are not affected.</span></span> 
3. <span data-ttu-id="d18e2-150">在每個點的指令碼中加入適當的記錄。</span><span class="sxs-lookup"><span data-stu-id="d18e2-150">Add adequate logging to the scripts at each point.</span></span> <span data-ttu-id="d18e2-151">指令碼記錄檔通常是對應用程式安裝問題進行偵錯的唯一方法。</span><span class="sxs-lookup"><span data-stu-id="d18e2-151">Usually the script logs are the only way to debug application installation issues.</span></span>
4. <span data-ttu-id="d18e2-152">確定外部服務或資源的呼叫有足夠的重試次數，讓安裝不會受到暫時性網路問題的影響。</span><span class="sxs-lookup"><span data-stu-id="d18e2-152">Ensure that calls to external services or resources have adequate retries so that the installation is not affected by transient network issues.</span></span>
5. <span data-ttu-id="d18e2-153">如果您的指令碼在節點上啟動服務，請確定服務受到監視並設定為在節點重新開機時自動啟動。</span><span class="sxs-lookup"><span data-stu-id="d18e2-153">If your script is starting services on the nodes, ensure that the services are monitored and configured to start automatically in case of node reboots.</span></span>

## <a name="package-application"></a><span data-ttu-id="d18e2-154">封裝應用程式</span><span class="sxs-lookup"><span data-stu-id="d18e2-154">Package application</span></span>
<span data-ttu-id="d18e2-155">建立 zip 檔案，其中包含安裝 HDInsight 應用程式時的所有必要檔案。</span><span class="sxs-lookup"><span data-stu-id="d18e2-155">Create a zip file that contains all required files for installing your HDInsight applications.</span></span> <span data-ttu-id="d18e2-156">您需要[發佈應用程式](#publish-application)中的 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="d18e2-156">You need the zip file in [Publish application](#publish-application).</span></span>

* <span data-ttu-id="d18e2-157">[createUiDefinition.json](#define-application)。</span><span class="sxs-lookup"><span data-stu-id="d18e2-157">[createUiDefinition.json](#define-application).</span></span>
* <span data-ttu-id="d18e2-158">mainTemplate.json。</span><span class="sxs-lookup"><span data-stu-id="d18e2-158">mainTemplate.json.</span></span> <span data-ttu-id="d18e2-159">請參閱[安裝自訂 HDInsight 應用程式](hdinsight-apps-install-custom-applications.md)中的範例。</span><span class="sxs-lookup"><span data-stu-id="d18e2-159">See a sample at [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span></span>
* <span data-ttu-id="d18e2-160">所有必要的指令碼。</span><span class="sxs-lookup"><span data-stu-id="d18e2-160">All required scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="d18e2-161">應用程式檔案 (包括 Web 應用程式檔案 (若有的話)) 可以位於任何可公開存取的端點上。</span><span class="sxs-lookup"><span data-stu-id="d18e2-161">The application files (including web application files if there is any) can be located on any publicly accessible endpoint.</span></span>
> 

## <a name="publish-application"></a><span data-ttu-id="d18e2-162">發佈應用程式</span><span class="sxs-lookup"><span data-stu-id="d18e2-162">Publish application</span></span>
<span data-ttu-id="d18e2-163">請遵循下列步驟來發佈 HDInsight 應用程式︰</span><span class="sxs-lookup"><span data-stu-id="d18e2-163">Follow the following steps to publish an HDInsight application:</span></span>

1. <span data-ttu-id="d18e2-164">登入 [Azure 發佈入口網站](https://publish.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="d18e2-164">Sign on to the [Azure Publishing portal](https://publish.windowsazure.com/).</span></span>
2. <span data-ttu-id="d18e2-165">按一下左邊的 [方案範本]  來建立新的方案範本。</span><span class="sxs-lookup"><span data-stu-id="d18e2-165">Click **Solution templates** from the left to create a new solution template.</span></span>
3. <span data-ttu-id="d18e2-166">輸入標題，然後按一下 [建立新的方案範本]。</span><span class="sxs-lookup"><span data-stu-id="d18e2-166">Enter a title, and then click **Create a new solution template**.</span></span>
4. <span data-ttu-id="d18e2-167">按一下 [建立開發人員中心帳戶並加入 Azure 方案]  以註冊您的公司 (如果尚未這麼做)。</span><span class="sxs-lookup"><span data-stu-id="d18e2-167">Click **Create Dev Center account and join the Azure program** to register your company if you haven't done so.</span></span>  <span data-ttu-id="d18e2-168">請參閱 [建立 Microsoft 開發人員帳戶](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="d18e2-168">See [Create a Microsoft Developer account](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).</span></span>
5. <span data-ttu-id="d18e2-169">按一下 [定義一些拓撲以便開始使用] 。</span><span class="sxs-lookup"><span data-stu-id="d18e2-169">Click **Define some Topologies to get Started**.</span></span> <span data-ttu-id="d18e2-170">方案範本是所有其拓撲的「父項」。</span><span class="sxs-lookup"><span data-stu-id="d18e2-170">A solution template is a "parent" to all its topologies.</span></span> <span data-ttu-id="d18e2-171">您可以在一個供應項目/解決方案範本中定義多個拓撲。</span><span class="sxs-lookup"><span data-stu-id="d18e2-171">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="d18e2-172">當供應項目推送到預備環境時，它的所有拓撲也會一起推入。</span><span class="sxs-lookup"><span data-stu-id="d18e2-172">When an offer is pushed to staging, it is pushed with all its topologies.</span></span> 
6. <span data-ttu-id="d18e2-173">輸入拓撲名稱，然後按一下加號。</span><span class="sxs-lookup"><span data-stu-id="d18e2-173">Enter a topology name, and then click the plus sign.</span></span>
7. <span data-ttu-id="d18e2-174">輸入新的版本，然後按一下加號。</span><span class="sxs-lookup"><span data-stu-id="d18e2-174">Enter a new version, and then click the Plus sign.</span></span>
8. <span data-ttu-id="d18e2-175">上傳在[封裝應用程式](#package-application)中準備的 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="d18e2-175">Upload the zip file prepared in [Package application](#package-application).</span></span>  
9. <span data-ttu-id="d18e2-176">按一下 [要求認證]。</span><span class="sxs-lookup"><span data-stu-id="d18e2-176">Click **Request Certification**.</span></span> <span data-ttu-id="d18e2-177">Microsoft 認證團隊會檢閱檔案並認證拓撲。</span><span class="sxs-lookup"><span data-stu-id="d18e2-177">The Microsoft certification team will review the files and certify the topology.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d18e2-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d18e2-178">Next steps</span></span>
* <span data-ttu-id="d18e2-179">[安裝 HDInsight 應用程式](hdinsight-apps-install-applications.md)︰了解如何將 HDInsight 應用程式安裝到您的叢集。</span><span class="sxs-lookup"><span data-stu-id="d18e2-179">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how to install an HDInsight application to your clusters.</span></span>
* <span data-ttu-id="d18e2-180">[安裝自訂 HDInsight 應用程式](hdinsight-apps-install-custom-applications.md)︰了解如何將未發佈的 HDInsight 應用程式部署到 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="d18e2-180">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): learn how to deploy an unpublished HDInsight application to HDInsight.</span></span>
* <span data-ttu-id="d18e2-181">[使用指令碼動作自訂以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)：了解如何使用指令碼動作來安裝其他應用程式。</span><span class="sxs-lookup"><span data-stu-id="d18e2-181">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): learn how to use Script Action to install additional applications.</span></span>
* <span data-ttu-id="d18e2-182">[使用 Azure Resource Manager 範本在 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集](hdinsight-hadoop-create-linux-clusters-arm-templates.md)︰了解如何呼叫 Resource Manager 範本來建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="d18e2-182">[Create Linux-based Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md): learn how to call Resource Manager templates to create HDInsight clusters.</span></span>
* <span data-ttu-id="d18e2-183">[在 HDInsight 中使用空白邊緣節點](hdinsight-apps-use-edge-node.md)︰了解如何使用空白邊緣節點來存取 HDInsight 叢集、測試 HDInsight 應用程式，以及裝載 HDInsight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d18e2-183">[Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md): learn how to use an empty edge node for accessing HDInsight cluster, testing HDInsight applications, and hosting HDInsight applications.</span></span>

