---
title: "aaaPublish HDInsight 應用程式-Azure |Microsoft 文件"
description: "深入了解如何 toocreate 和發行 HDInsight 應用程式。"
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
ms.openlocfilehash: 7da0aa53828563e50ef372df901e1ba541fb40be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-hdinsight-applications-into-hello-azure-marketplace"></a><span data-ttu-id="2940c-103">發行到 hello Azure Marketplace 的 HDInsight 應用程式</span><span class="sxs-lookup"><span data-stu-id="2940c-103">Publish HDInsight applications into hello Azure Marketplace</span></span>
<span data-ttu-id="2940c-104">HDInsight 應用程式是使用者可以在以 Linux 為基礎的 HDInsight 叢集上安裝的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2940c-104">An HDInsight application is an application that users can install on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="2940c-105">Microsoft 獨立軟體廠商 (ISV) 或您可以自己開發這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="2940c-105">These applications can be developed by Microsoft, independent software vendors (ISV) or by yourself.</span></span> <span data-ttu-id="2940c-106">在本文中，您將學習如何 toopublish hello Azure Marketplace 將 HDInsight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2940c-106">In this article, you learn how toopublish an HDInsight application into hello Azure Marketplace.</span></span>  <span data-ttu-id="2940c-107">如需身分資料發佈至 hello Azure Marketplace 的一般資訊，請參閱[發佈供應項目 toohello Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="2940c-107">For general information about publishing into hello Azure Marketplace, see [publish an offer toohello Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="2940c-108">HDInsight 應用程式使用 hello*攜帶您自己授權 (BYOL)*模型，其中應用程式提供者會負責授權 hello 應用程式 tooend 位使用者，而使用者只需要付費 azure hello 資源它們建立，例如 hello HDInsight 叢集和 Vm/節點。</span><span class="sxs-lookup"><span data-stu-id="2940c-108">HDInsight applications use hello *Bring Your Own License (BYOL)* model, where application provider is responsible for licensing hello application tooend-users, and end-users are only charged by Azure for hello resources they create, such as hello HDInsight cluster and its VMs/nodes.</span></span> <span data-ttu-id="2940c-109">目前，計費 hello 應用程式本身不是透過 Azure。</span><span class="sxs-lookup"><span data-stu-id="2940c-109">Currently, billing for hello application itself is not done through Azure.</span></span>

<span data-ttu-id="2940c-110">其他 HDInsight 應用程式相關文章︰</span><span class="sxs-lookup"><span data-stu-id="2940c-110">Other HDInsight application-related article:</span></span>

* <span data-ttu-id="2940c-111">[安裝的應用程式 HDInsight](hdinsight-apps-install-applications.md)： 了解如何 tooinstall HDInsight 應用程式 tooyour 叢集。</span><span class="sxs-lookup"><span data-stu-id="2940c-111">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how tooinstall an HDInsight application tooyour clusters.</span></span>
* <span data-ttu-id="2940c-112">[安裝自訂 HDInsight 應用程式](hdinsight-apps-install-custom-applications.md)： 了解如何 tooinstall 和測試自訂 HDInsight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2940c-112">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): Learn how tooinstall and test custom HDInsight applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2940c-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="2940c-113">Prerequisites</span></span>
<span data-ttu-id="2940c-114">toosubmit 您自訂的應用程式的 toohello marketplace，您必須已建立並測試自訂應用程式。</span><span class="sxs-lookup"><span data-stu-id="2940c-114">toosubmit your custom application toohello marketplace, you must have created and tested your custom application.</span></span> <span data-ttu-id="2940c-115">請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="2940c-115">See hello following articles:</span></span>

* <span data-ttu-id="2940c-116">[安裝自訂 HDInsight 應用程式](hdinsight-apps-install-custom-applications.md)： 了解如何 tooinstall 和測試自訂 HDInsight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2940c-116">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): Learn how tooinstall and test custom HDInsight applications.</span></span>

<span data-ttu-id="2940c-117">您還必須註冊開發人員帳戶。</span><span class="sxs-lookup"><span data-stu-id="2940c-117">You must also have registered your developer account.</span></span> <span data-ttu-id="2940c-118">請參閱[發佈供應項目 toohello Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md)和[建立 Microsoft 開發人員帳戶](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="2940c-118">See [publish an offer toohello Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md) and [Create a Microsoft Developer account](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).</span></span>

## <a name="define-application"></a><span data-ttu-id="2940c-119">定義應用程式</span><span class="sxs-lookup"><span data-stu-id="2940c-119">Define application</span></span>
<span data-ttu-id="2940c-120">有兩個步驟來發行應用程式 toohello Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="2940c-120">There are two steps involved for publishing applications toohello Azure Marketplace.</span></span>  <span data-ttu-id="2940c-121">先定義**createUiDef.json**檔案 tooindicate 的叢集，您的應用程式與; 相容，而且您應發佈 hello Azure 入口網站中的 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="2940c-121">First you define a **createUiDef.json** file tooindicate which clusters your application is compatible with; and then you publish hello template from hello Azure portal.</span></span> <span data-ttu-id="2940c-122">下列章節的 hello 是範例 createUiDef.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="2940c-122">hello following section is a sample createUiDef.json file.</span></span>

    {
        "handler": "Microsoft.HDInsight",
        "version": "0.0.1-preview",
        "clusterFilters": {
            "types": ["Hadoop", "HBase", "Storm", "Spark"],
            "tiers": ["Standard", "Premium"],
            "versions": ["3.4"]
        }
    }


| <span data-ttu-id="2940c-123">欄位</span><span class="sxs-lookup"><span data-stu-id="2940c-123">Field</span></span> | <span data-ttu-id="2940c-124">描述</span><span class="sxs-lookup"><span data-stu-id="2940c-124">Description</span></span> | <span data-ttu-id="2940c-125">可能的值</span><span class="sxs-lookup"><span data-stu-id="2940c-125">Possible values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2940c-126">types</span><span class="sxs-lookup"><span data-stu-id="2940c-126">types</span></span> |<span data-ttu-id="2940c-127">hello 叢集 hello 應用程式是與相容的類型。</span><span class="sxs-lookup"><span data-stu-id="2940c-127">hello cluster types that hello application is compatible with.</span></span> |<span data-ttu-id="2940c-128">Hadoop、HBase、Storm、Spark (或這些類型的任意組合)</span><span class="sxs-lookup"><span data-stu-id="2940c-128">Hadoop, HBase, Storm, Spark, (or any combination of these)</span></span> |
| <span data-ttu-id="2940c-129">tiers</span><span class="sxs-lookup"><span data-stu-id="2940c-129">tiers</span></span> |<span data-ttu-id="2940c-130">hello hello 應用程式為相容於叢集層。</span><span class="sxs-lookup"><span data-stu-id="2940c-130">hello cluster tiers that hello application is compatible with.</span></span> |<span data-ttu-id="2940c-131">Standard、Premium (或兩者)</span><span class="sxs-lookup"><span data-stu-id="2940c-131">Standard, Premium, (or both)</span></span> |
| <span data-ttu-id="2940c-132">versions</span><span class="sxs-lookup"><span data-stu-id="2940c-132">versions</span></span> |<span data-ttu-id="2940c-133">hello hello 應用程式是與相容的 HDInsight 叢集類型。</span><span class="sxs-lookup"><span data-stu-id="2940c-133">hello HDInsight cluster types that hello application is compatible with.</span></span> |<span data-ttu-id="2940c-134">3.4</span><span class="sxs-lookup"><span data-stu-id="2940c-134">3.4</span></span> |

## <a name="application-install-script"></a><span data-ttu-id="2940c-135">應用程式安裝指令碼</span><span class="sxs-lookup"><span data-stu-id="2940c-135">Application install script</span></span>
<span data-ttu-id="2940c-136">每當應用程式已安裝在叢集上 （為現有或新的），建立邊緣節點和 hello 應用程式安裝指令碼在其上執行。</span><span class="sxs-lookup"><span data-stu-id="2940c-136">Whenever an application is installed on a cluster (either an existing one or a new one), an edge node is created and hello application install script is run on it.</span></span>
  > [!IMPORTANT]
  > <span data-ttu-id="2940c-137">以下列格式的 hello，hello 名稱 hello 應用程式安裝指令碼名稱必須是特定叢集的唯一的。</span><span class="sxs-lookup"><span data-stu-id="2940c-137">hello name of hello application install script names must be unique for a particular cluster with hello following format.</span></span>
  > 
  > <span data-ttu-id="2940c-138">name": "[concat('hue-install-v0','-' ,uniquestring(‘applicationName’)]"</span><span class="sxs-lookup"><span data-stu-id="2940c-138">name": "[concat('hue-install-v0','-' ,uniquestring(‘applicationName’)]"</span></span>
  > 
  > <span data-ttu-id="2940c-139">請注意有三個部分 toohello 指令碼名稱：</span><span class="sxs-lookup"><span data-stu-id="2940c-139">Note there are three parts toohello script name:</span></span>
  > 
  > 1. <span data-ttu-id="2940c-140">指令碼名稱前置詞，都應該包括 hello 應用程式名稱相關 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2940c-140">A script name prefix, which shall include either hello application name or a name relevant toohello application.</span></span>
  > 2. <span data-ttu-id="2940c-141">"-" 以方便閱讀。</span><span class="sxs-lookup"><span data-stu-id="2940c-141">A "-" for readability.</span></span>
  > 3. <span data-ttu-id="2940c-142">Hello 應用程式名稱為 hello 參數的唯一字串的函式。</span><span class="sxs-lookup"><span data-stu-id="2940c-142">A unique string function with hello application name as hello parameter.</span></span>
  > 
  > <span data-ttu-id="2940c-143">例如，上述的 hello 最後會變得： 色調-安裝-v0-4wkahss55hlas hello 中保存的指令碼動作清單。</span><span class="sxs-lookup"><span data-stu-id="2940c-143">An example is hello above ends up becoming: hue-install-v0-4wkahss55hlas in hello persisted script action list.</span></span> <span data-ttu-id="2940c-144">如需 JSON 承載的範例，請參閱 [https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json](https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="2940c-144">For a sample JSON payload, see [https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json](https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json).</span></span>
  > 
<span data-ttu-id="2940c-145">hello 安裝指令碼必須具有下列特性的 hello:</span><span class="sxs-lookup"><span data-stu-id="2940c-145">hello installation script must have hello following characteristics:</span></span>
1. <span data-ttu-id="2940c-146">請確定 hello 指令碼具有等冪性。</span><span class="sxs-lookup"><span data-stu-id="2940c-146">Ensure that hello script is idempotent.</span></span> <span data-ttu-id="2940c-147">Toohello 指令碼應該會產生多個呼叫 hello 相同的結果。</span><span class="sxs-lookup"><span data-stu-id="2940c-147">Multiple calls toohello script should produce hello same result.</span></span>
2. <span data-ttu-id="2940c-148">hello 指令碼應該是正確版本。</span><span class="sxs-lookup"><span data-stu-id="2940c-148">hello script should be properly versioned.</span></span> <span data-ttu-id="2940c-149">當您升級或測試變更，讓客戶嘗試 tooinstall hello 應用程式不會受到影響，請使用不同的位置 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="2940c-149">Use a different location for hello script when you are upgrading or testing out changes so that customers that are trying tooinstall hello application are not affected.</span></span> 
3. <span data-ttu-id="2940c-150">新增適當的記錄 toohello 指令碼，在每個點。</span><span class="sxs-lookup"><span data-stu-id="2940c-150">Add adequate logging toohello scripts at each point.</span></span> <span data-ttu-id="2940c-151">通常 hello 指令碼記錄檔是唯一的方式 toodebug hello 應用程式安裝問題。</span><span class="sxs-lookup"><span data-stu-id="2940c-151">Usually hello script logs are hello only way toodebug application installation issues.</span></span>
4. <span data-ttu-id="2940c-152">請確定呼叫 tooexternal 服務或資源有足夠的重試以便 hello 安裝不會受到暫時性網路問題。</span><span class="sxs-lookup"><span data-stu-id="2940c-152">Ensure that calls tooexternal services or resources have adequate retries so that hello installation is not affected by transient network issues.</span></span>
5. <span data-ttu-id="2940c-153">如果您的指令碼 hello 節點上啟動服務，請確定會監視和設定會自動發生節點重新開機時 toostart hello 服務。</span><span class="sxs-lookup"><span data-stu-id="2940c-153">If your script is starting services on hello nodes, ensure that hello services are monitored and configured toostart automatically in case of node reboots.</span></span>

## <a name="package-application"></a><span data-ttu-id="2940c-154">封裝應用程式</span><span class="sxs-lookup"><span data-stu-id="2940c-154">Package application</span></span>
<span data-ttu-id="2940c-155">建立 zip 檔案，其中包含安裝 HDInsight 應用程式時的所有必要檔案。</span><span class="sxs-lookup"><span data-stu-id="2940c-155">Create a zip file that contains all required files for installing your HDInsight applications.</span></span> <span data-ttu-id="2940c-156">您需要 hello zip 檔案中的[發行應用程式](#publish-application)。</span><span class="sxs-lookup"><span data-stu-id="2940c-156">You need hello zip file in [Publish application](#publish-application).</span></span>

* <span data-ttu-id="2940c-157">[createUiDefinition.json](#define-application)。</span><span class="sxs-lookup"><span data-stu-id="2940c-157">[createUiDefinition.json](#define-application).</span></span>
* <span data-ttu-id="2940c-158">mainTemplate.json。</span><span class="sxs-lookup"><span data-stu-id="2940c-158">mainTemplate.json.</span></span> <span data-ttu-id="2940c-159">請參閱[安裝自訂 HDInsight 應用程式](hdinsight-apps-install-custom-applications.md)中的範例。</span><span class="sxs-lookup"><span data-stu-id="2940c-159">See a sample at [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span></span>
* <span data-ttu-id="2940c-160">所有必要的指令碼。</span><span class="sxs-lookup"><span data-stu-id="2940c-160">All required scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="2940c-161">hello 應用程式檔案 （如果有的話，包含 web 應用程式檔案） 可以位於任何可公開存取的端點。</span><span class="sxs-lookup"><span data-stu-id="2940c-161">hello application files (including web application files if there is any) can be located on any publicly accessible endpoint.</span></span>
> 

## <a name="publish-application"></a><span data-ttu-id="2940c-162">發佈應用程式</span><span class="sxs-lookup"><span data-stu-id="2940c-162">Publish application</span></span>
<span data-ttu-id="2940c-163">請遵循下列步驟 toopublish HDInsight 應用程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="2940c-163">Follow hello following steps toopublish an HDInsight application:</span></span>

1. <span data-ttu-id="2940c-164">登入 toohello [Azure 發行入口網站](https://publish.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="2940c-164">Sign on toohello [Azure Publishing portal](https://publish.windowsazure.com/).</span></span>
2. <span data-ttu-id="2940c-165">按一下**解決方案範本**從 hello 左 toocreate 新的方案範本。</span><span class="sxs-lookup"><span data-stu-id="2940c-165">Click **Solution templates** from hello left toocreate a new solution template.</span></span>
3. <span data-ttu-id="2940c-166">輸入標題，然後按一下建立新的方案範本。</span><span class="sxs-lookup"><span data-stu-id="2940c-166">Enter a title, and then click **Create a new solution template**.</span></span>
4. <span data-ttu-id="2940c-167">按一下**建立開發人員中心帳戶和聯結 hello Azure 程式**tooregister 公司如果您尚未這樣做。</span><span class="sxs-lookup"><span data-stu-id="2940c-167">Click **Create Dev Center account and join hello Azure program** tooregister your company if you haven't done so.</span></span>  <span data-ttu-id="2940c-168">請參閱 [建立 Microsoft 開發人員帳戶](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="2940c-168">See [Create a Microsoft Developer account](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).</span></span>
5. <span data-ttu-id="2940c-169">按一下**定義一些拓撲 tooget 已啟動**。</span><span class="sxs-lookup"><span data-stu-id="2940c-169">Click **Define some Topologies tooget Started**.</span></span> <span data-ttu-id="2940c-170">方案範本是 「 父 」 tooall 其拓撲。</span><span class="sxs-lookup"><span data-stu-id="2940c-170">A solution template is a "parent" tooall its topologies.</span></span> <span data-ttu-id="2940c-171">您可以在一個供應項目/解決方案範本中定義多個拓撲。</span><span class="sxs-lookup"><span data-stu-id="2940c-171">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="2940c-172">當 toostaging 推入的供應項目時，它是推入與所有其拓撲。</span><span class="sxs-lookup"><span data-stu-id="2940c-172">When an offer is pushed toostaging, it is pushed with all its topologies.</span></span> 
6. <span data-ttu-id="2940c-173">輸入拓撲名稱，，，然後按一下hello 加號。</span><span class="sxs-lookup"><span data-stu-id="2940c-173">Enter a topology name, and then click hello plus sign.</span></span>
7. <span data-ttu-id="2940c-174">輸入新的版本，，然後按一下hello 加號。</span><span class="sxs-lookup"><span data-stu-id="2940c-174">Enter a new version, and then click hello Plus sign.</span></span>
8. <span data-ttu-id="2940c-175">上傳 hello zip 檔案中準備[應用程式封裝](#package-application)。</span><span class="sxs-lookup"><span data-stu-id="2940c-175">Upload hello zip file prepared in [Package application](#package-application).</span></span>  
9. <span data-ttu-id="2940c-176">按一下 [要求認證]。</span><span class="sxs-lookup"><span data-stu-id="2940c-176">Click **Request Certification**.</span></span> <span data-ttu-id="2940c-177">hello Microsoft 認證小組將檢閱 hello 檔案，並證實 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="2940c-177">hello Microsoft certification team will review hello files and certify hello topology.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2940c-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2940c-178">Next steps</span></span>
* <span data-ttu-id="2940c-179">[安裝的應用程式 HDInsight](hdinsight-apps-install-applications.md)： 了解如何 tooinstall HDInsight 應用程式 tooyour 叢集。</span><span class="sxs-lookup"><span data-stu-id="2940c-179">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how tooinstall an HDInsight application tooyour clusters.</span></span>
* <span data-ttu-id="2940c-180">[安裝自訂 HDInsight 應用程式](hdinsight-apps-install-custom-applications.md)： 了解如何 toodeploy 未發行的 HDInsight 應用程式 tooHDInsight。</span><span class="sxs-lookup"><span data-stu-id="2940c-180">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): learn how toodeploy an unpublished HDInsight application tooHDInsight.</span></span>
* <span data-ttu-id="2940c-181">[自訂使用指令碼動作以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)： 了解如何 toouse 指令碼動作 tooinstall 其他應用程式。</span><span class="sxs-lookup"><span data-stu-id="2940c-181">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): learn how toouse Script Action tooinstall additional applications.</span></span>
* <span data-ttu-id="2940c-182">[使用 Azure Resource Manager 範本 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集](hdinsight-hadoop-create-linux-clusters-arm-templates.md)： 了解如何 toocall 資源管理員範本 toocreate HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="2940c-182">[Create Linux-based Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md): learn how toocall Resource Manager templates toocreate HDInsight clusters.</span></span>
* <span data-ttu-id="2940c-183">[使用 HDInsight 中的空白邊緣節點](hdinsight-apps-use-edge-node.md)： 了解如何 toouse 空白邊緣節點存取 HDInsight 叢集、 測試 HDInsight 應用程式，以及裝載 HDInsight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2940c-183">[Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md): learn how toouse an empty edge node for accessing HDInsight cluster, testing HDInsight applications, and hosting HDInsight applications.</span></span>

