---
title: "使用指令碼動作來自訂 HDInsight 叢集 - Azure | Microsoft Docs"
description: "使用指令碼動作在以 Linux 為基礎的 HDInsight 叢集上新增自訂元件。 指令碼動作是 Bash 指令碼，可用來自訂叢集設定，或新增其他服務和公用程式，如 Hue、Solr 或 R。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 0c5d00b6cb9f68a1a0e474f81c969eb1b5654c67
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="5a80f-104">使用指令碼動作自訂 Linux 型 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="5a80f-104">Customize Linux-based HDInsight clusters using Script Action</span></span>

<span data-ttu-id="5a80f-105">HDInsight 提供一個稱為 [指令碼動作]  的組態選項，此指令碼動作可叫用用於自訂叢集的自訂指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a80f-105">HDInsight provides a configuration option called **Script Action** that invokes custom scripts that customize the cluster.</span></span> <span data-ttu-id="5a80f-106">這些指令碼可用來安裝其他元件和變更組態設定。</span><span class="sxs-lookup"><span data-stu-id="5a80f-106">These scripts are used to install additional components and change configuration settings.</span></span> <span data-ttu-id="5a80f-107">叢集建立期間或叢集建立之後，可以使用指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="5a80f-107">Script actions can be used during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a80f-108">只有以 Linux 為基礎的 HDInsight 叢集能夠在已在執行中的叢集上使用指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="5a80f-108">The ability to use script actions on an already running cluster is only available for Linux-based HDInsight clusters.</span></span>
>
> <span data-ttu-id="5a80f-109">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="5a80f-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5a80f-110">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="5a80f-111">指令碼動作也可以發佈到 Azure Marketplace 做為 HDInsight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5a80f-111">Script actions can also be published to the Azure Marketplace as an HDInsight application.</span></span> <span data-ttu-id="5a80f-112">本文件中的部分範例將示範如何使用 PowerShell 和 .NET SDK 的指令碼動作命令來安裝 HDInsight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5a80f-112">Some of the examples in this document show how you can install an HDInsight application using script action commands from PowerShell and the .NET SDK.</span></span> <span data-ttu-id="5a80f-113">如需 HDInsight 應用程式的詳細資訊，請參閱 [將 HDInsight 應用程式發佈到 Azure Marketplace](hdinsight-apps-publish-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-113">For more information on HDInsight applications, see [Publish HDInsight applications into the Azure Marketplace](hdinsight-apps-publish-applications.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="5a80f-114">權限</span><span class="sxs-lookup"><span data-stu-id="5a80f-114">Permissions</span></span>

<span data-ttu-id="5a80f-115">如果您要使用已加入網域的 HDInsight 叢集，則在對叢集使用指令碼動作時必須有兩個 Ambari 權限︰</span><span class="sxs-lookup"><span data-stu-id="5a80f-115">If you are using a domain-joined HDInsight cluster, there are two Ambari permissions that are required when using script actions with the cluster:</span></span>

* <span data-ttu-id="5a80f-116">**AMBARI.RUN\_CUSTOM\_COMMAND**：依預設，Ambari 系統管理員角色會具有此權限。</span><span class="sxs-lookup"><span data-stu-id="5a80f-116">**AMBARI.RUN\_CUSTOM\_COMMAND**: The Ambari Administrator role has this permission by default.</span></span>
* <span data-ttu-id="5a80f-117">**CLUSTER.RUN\_CUSTOM\_COMMAND**：依預設，HDInsight 叢集系統管理員和 Ambari 系統管理員會具有此權限。</span><span class="sxs-lookup"><span data-stu-id="5a80f-117">**CLUSTER.RUN\_CUSTOM\_COMMAND**: Both the HDInsight Cluster Administrator and Ambari Administrator have this permission by default.</span></span>

<span data-ttu-id="5a80f-118">如需使用已加入網域之 HDInsight 權限的詳細資訊，請參閱[管理已加入網域的 HDInsight 叢集](hdinsight-domain-joined-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-118">For more information on working with permissions with domain-joined HDInsight, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="5a80f-119">存取控制</span><span class="sxs-lookup"><span data-stu-id="5a80f-119">Access control</span></span>

<span data-ttu-id="5a80f-120">如果您不是 Azure 訂用帳戶的系統管理員/擁有者，您的帳戶必須至少有包含 HDInsight 叢集之資源群組的**參與者**存取權。</span><span class="sxs-lookup"><span data-stu-id="5a80f-120">If you are not the administrator/owner of your Azure subscription, your account must have at least **Contributor** access to the resource group that contains the HDInsight cluster.</span></span>

<span data-ttu-id="5a80f-121">此外，如果您要建立 HDInsight 叢集，至少具備 Azure 訂用帳戶之**參與者**存取權的某人，必須已在先前註冊 HDInsight 的提供者。</span><span class="sxs-lookup"><span data-stu-id="5a80f-121">Additionally, if you are creating an HDInsight cluster, someone with at least **Contributor** access to the Azure subscription must have previously registered the provider for HDInsight.</span></span> <span data-ttu-id="5a80f-122">具有訂用帳戶之參與者存取權的使用者第一次在訂用帳戶上建立資源時，便會註冊提供者。</span><span class="sxs-lookup"><span data-stu-id="5a80f-122">Provider registration happens when a user with Contributor access to the subscription creates a resource for the first time on the subscription.</span></span> <span data-ttu-id="5a80f-123">透過[使用 REST 註冊提供者](https://msdn.microsoft.com/library/azure/dn790548.aspx)，也可以不需要建立資源就完成註冊作業。</span><span class="sxs-lookup"><span data-stu-id="5a80f-123">It can also be accomplished without creating a resource by [registering a provider using REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span></span>

<span data-ttu-id="5a80f-124">如需使用存取管理的詳細資訊，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="5a80f-124">For more information on working with access management, see the following documents:</span></span>

* [<span data-ttu-id="5a80f-125">開始在 Azure 入口網站中使用存取管理</span><span class="sxs-lookup"><span data-stu-id="5a80f-125">Get started with access management in the Azure portal</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="5a80f-126">使用角色指派來管理 Azure 訂用帳戶資源的存取權</span><span class="sxs-lookup"><span data-stu-id="5a80f-126">Use role assignments to manage access to your Azure subscription resources</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a><span data-ttu-id="5a80f-127">了解指令碼動作</span><span class="sxs-lookup"><span data-stu-id="5a80f-127">Understanding Script Actions</span></span>

<span data-ttu-id="5a80f-128">指令碼動作只是一個您會提供 URI 和參數的 Bash 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a80f-128">A Script Action is simply a Bash script that you provide a URI to, and parameters for.</span></span> <span data-ttu-id="5a80f-129">該指令碼會在 HDInsight 叢集節點上執行。</span><span class="sxs-lookup"><span data-stu-id="5a80f-129">The script runs on nodes in the HDInsight cluster.</span></span> <span data-ttu-id="5a80f-130">以下是指令碼動作的特性和功能。</span><span class="sxs-lookup"><span data-stu-id="5a80f-130">The following are characteristics and features of script actions.</span></span>

* <span data-ttu-id="5a80f-131">必須儲存在可從 HDInsight 叢集存取的 URI 上。</span><span class="sxs-lookup"><span data-stu-id="5a80f-131">Must be stored on a URI that is accessible from the HDInsight cluster.</span></span> <span data-ttu-id="5a80f-132">以下是可能的儲存位置：</span><span class="sxs-lookup"><span data-stu-id="5a80f-132">The following are possible storage locations:</span></span>

    * <span data-ttu-id="5a80f-133">HDInsight 叢集可存取的 **Azure Data Lake Store** 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a80f-133">An **Azure Data Lake Store** account that is accessible by the HDInsight cluster.</span></span> <span data-ttu-id="5a80f-134">如需使用 Azure Data Lake Store 與 HDInsight 的相關資訊，請參閱[建立使用 Data Lake Store 的 HDInsight 叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-134">For information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

        <span data-ttu-id="5a80f-135">使用 Data Lake Store 中儲存的指令碼時，URI 格式為 `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`。</span><span class="sxs-lookup"><span data-stu-id="5a80f-135">When using a script stored in Data Lake Store, the URI format is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span></span>

        > [!NOTE]
        > <span data-ttu-id="5a80f-136">用來存取 Data Lake Store 的服務主體 HDInsight 必須具有指令碼的讀取權限。</span><span class="sxs-lookup"><span data-stu-id="5a80f-136">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span></span>

    * <span data-ttu-id="5a80f-137">本身是 HDInsight 叢集主要或其他儲存體帳戶之 **Azure 儲存體帳戶**中的 Blob。</span><span class="sxs-lookup"><span data-stu-id="5a80f-137">A blob in an **Azure Storage account** that is either the primary or additional storage account for the HDInsight cluster.</span></span> <span data-ttu-id="5a80f-138">在建立叢集期間，已將這兩種儲存體帳戶的存取權都授與 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="5a80f-138">HDInsight is granted access to both of these types of storage accounts during cluster creation.</span></span>

    * <span data-ttu-id="5a80f-139">公用檔案共用服務，例如 Azure Blob、GitHub、OneDrive、Dropbox 等。</span><span class="sxs-lookup"><span data-stu-id="5a80f-139">A public file sharing service such as Azure Blob, GitHub, OneDrive, Dropbox, etc.</span></span>

        <span data-ttu-id="5a80f-140">如需範例 URI，請參閱[範例指令碼動作指令碼](#example-script-action-scripts)一節。</span><span class="sxs-lookup"><span data-stu-id="5a80f-140">For example URIs, see the [Example script action scripts](#example-script-action-scripts) section.</span></span>

        > [!WARNING]
        > <span data-ttu-id="5a80f-141">HDInsight 僅支援__一般用途__的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a80f-141">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="5a80f-142">目前不支援 __Blob 儲存體__帳戶類型。</span><span class="sxs-lookup"><span data-stu-id="5a80f-142">It does not currently support the __Blob storage__ account type.</span></span>

* <span data-ttu-id="5a80f-143">可以限制為**只在特定節點類型上執行**，例如前端節點或背景工作節點。</span><span class="sxs-lookup"><span data-stu-id="5a80f-143">Can be restricted to **run on only certain node types**, for example head nodes or worker nodes.</span></span>

  > [!NOTE]
  > <span data-ttu-id="5a80f-144">與 HDInsight Premium 搭配使用時，您可以指定指令碼應該在邊緣節點上使用。</span><span class="sxs-lookup"><span data-stu-id="5a80f-144">When used with HDInsight Premium, you can specify that the script should be used on the edge node.</span></span>

* <span data-ttu-id="5a80f-145">可以是**持續性**或**臨時性**。</span><span class="sxs-lookup"><span data-stu-id="5a80f-145">Can be **persisted** or **ad hoc**.</span></span>

    <span data-ttu-id="5a80f-146">指令碼執行後，**持續性**指令碼會套用至新增至叢集的背景工作角色節點。</span><span class="sxs-lookup"><span data-stu-id="5a80f-146">**Persisted** scripts are applied to worker nodes added to the cluster after the script runs.</span></span> <span data-ttu-id="5a80f-147">例如，在向上調整叢集的規模時。</span><span class="sxs-lookup"><span data-stu-id="5a80f-147">For example, when scaling up the cluster.</span></span>

    <span data-ttu-id="5a80f-148">持續性指令碼也可能會將變更套用至另一個節點類型，例如前端節點。</span><span class="sxs-lookup"><span data-stu-id="5a80f-148">A persisted script might also apply changes to another node type, such as a head node.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5a80f-149">持續性指令碼動作必須有唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="5a80f-149">Persisted script actions must have a unique name.</span></span>

    <span data-ttu-id="5a80f-150">**臨時性**指令碼不會持續留存。</span><span class="sxs-lookup"><span data-stu-id="5a80f-150">**Ad hoc** scripts are not persisted.</span></span> <span data-ttu-id="5a80f-151">在指令碼執行後，它們不會套用至新增至叢集的背景工作角色節點。</span><span class="sxs-lookup"><span data-stu-id="5a80f-151">They are not applied to worker nodes added to the cluster after the script has ran.</span></span> <span data-ttu-id="5a80f-152">您可以在之後將臨時性指令碼升階為持續性指令碼，或將持續性指令碼降階為臨時性指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a80f-152">You can subsequently promote an ad hoc script to a persisted script, or demote a persisted script to an ad hoc script.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5a80f-153">建立叢集期間使用的指令碼動作會自動保存下來。</span><span class="sxs-lookup"><span data-stu-id="5a80f-153">Script actions used during cluster creation are automatically persisted.</span></span>
  >
  > <span data-ttu-id="5a80f-154">即使您特別指出應予保存，仍然不會保存失敗的指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a80f-154">Scripts that fail are not persisted, even if you specifically indicate that they should be.</span></span>

* <span data-ttu-id="5a80f-155">可以接受指令碼在執行期間所使用的**參數**。</span><span class="sxs-lookup"><span data-stu-id="5a80f-155">Can accept **parameters** that are used by the script during execution.</span></span>
* <span data-ttu-id="5a80f-156">在叢集節點上以**根層級權限**執行。</span><span class="sxs-lookup"><span data-stu-id="5a80f-156">Run with **root level privileges** on the cluster nodes.</span></span>
* <span data-ttu-id="5a80f-157">可以透過 **Azure 入口網站**、**Azure PowerShell**、**Azure CLI** 或 **HDInsight .NET SDK** 使用。</span><span class="sxs-lookup"><span data-stu-id="5a80f-157">Can be used through the **Azure portal**, **Azure PowerShell**, **Azure CLI**, or **HDInsight .NET SDK**</span></span>

<span data-ttu-id="5a80f-158">叢集會保留所有已執行指令碼的歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="5a80f-158">The cluster keeps a history of all scripts that have been ran.</span></span> <span data-ttu-id="5a80f-159">當您需要尋找升級或降級作業之指令碼的識別碼時，歷程記錄就很有用。</span><span class="sxs-lookup"><span data-stu-id="5a80f-159">The history is useful when you need to find the ID of a script for promotion or demotion operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a80f-160">沒有任何自動方式可復原指令碼動作所做的變更。</span><span class="sxs-lookup"><span data-stu-id="5a80f-160">There is no automatic way to undo the changes made by a script action.</span></span> <span data-ttu-id="5a80f-161">請手動回復變更，或提供可回復變更的指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a80f-161">Either manually reverse the changes or provide a script that reverses them.</span></span>


### <a name="script-action-in-the-cluster-creation-process"></a><span data-ttu-id="5a80f-162">叢集建立程序中的指令碼動作</span><span class="sxs-lookup"><span data-stu-id="5a80f-162">Script Action in the cluster creation process</span></span>

<span data-ttu-id="5a80f-163">在叢集建立期間使用的指令碼動作與在現有叢集上執行的指令碼動作稍微不同︰</span><span class="sxs-lookup"><span data-stu-id="5a80f-163">Script Actions used during cluster creation are slightly different from script actions ran on an existing cluster:</span></span>

* <span data-ttu-id="5a80f-164">此指令碼會**自動保存**。</span><span class="sxs-lookup"><span data-stu-id="5a80f-164">The script is **automatically persisted**.</span></span>
* <span data-ttu-id="5a80f-165">指令碼中若發生**失敗**，可能會導致叢集建立程序失敗。</span><span class="sxs-lookup"><span data-stu-id="5a80f-165">A **failure** in the script can cause the cluster creation process to fail.</span></span>

<span data-ttu-id="5a80f-166">下圖說明在建立程序期間執行指令碼動作的時間：</span><span class="sxs-lookup"><span data-stu-id="5a80f-166">The following diagram illustrates when Script Action is executed during the creation process:</span></span>

<span data-ttu-id="5a80f-167">![HDInsight 叢集自訂和叢集建立期間的階段][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="5a80f-167">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="5a80f-168">設定 HDInsight 時會執行此指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a80f-168">The script runs while HDInsight is being configured.</span></span> <span data-ttu-id="5a80f-169">在此階段，指令碼會以平行方式在叢集中所有指定的節點上執行，並且在節點上以根權限執行。</span><span class="sxs-lookup"><span data-stu-id="5a80f-169">At this stage, the script runs in parallel on all the specified nodes in the cluster, and runs with root privileges on the nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="5a80f-170">因為指令碼是以根層級權限在叢集節點上執行，所以您可以執行作業，例如停止和啟動服務，包括 Hadoop 相關服務。</span><span class="sxs-lookup"><span data-stu-id="5a80f-170">Because the script runs with root level privilege on the cluster nodes, you can perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="5a80f-171">如果您停止服務，您必須在指令碼完成執行之前，確定 Ambari 服務及其他 Hadoop 相關服務已啟動並且正在執行。</span><span class="sxs-lookup"><span data-stu-id="5a80f-171">If you stop services, you must ensure that the Ambari service and other Hadoop-related services are up and running before the script finishes running.</span></span> <span data-ttu-id="5a80f-172">這些服務必須在叢集建立時，成功地判斷叢集的健康情況和狀態。</span><span class="sxs-lookup"><span data-stu-id="5a80f-172">These services are required to successfully determine the health and state of the cluster while it is being created.</span></span>


<span data-ttu-id="5a80f-173">在叢集建立期間，您可以同時使用多個指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="5a80f-173">During cluster creation, you can use multiple script actions at once.</span></span> <span data-ttu-id="5a80f-174">這些指令碼會以指定的順序叫用。</span><span class="sxs-lookup"><span data-stu-id="5a80f-174">These scripts are invoked in the order in which they were specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a80f-175">指令碼動作必須在 60 分鐘內完成，否則就會逾時。</span><span class="sxs-lookup"><span data-stu-id="5a80f-175">Script actions must complete within 60 minutes, or timeout.</span></span> <span data-ttu-id="5a80f-176">在叢集佈建期間，同時執行指令碼與其他安裝和組態程序。</span><span class="sxs-lookup"><span data-stu-id="5a80f-176">During cluster provisioning, the script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="5a80f-177">與在您開發環境中的執行時間相較，爭用 CPU 時間和網路頻寬等資源可能會導致指令碼需要較長的時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="5a80f-177">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span></span>
>
> <span data-ttu-id="5a80f-178">若要讓執行指令碼所花費的時間降到最低，請避免從原始程式碼下載和編譯應用程式之類的工作。</span><span class="sxs-lookup"><span data-stu-id="5a80f-178">To minimize the time it takes to run the script, avoid tasks such as downloading and compiling applications from source.</span></span> <span data-ttu-id="5a80f-179">預先編譯應用程式，並在 Azure 儲存體中儲存二進位檔。</span><span class="sxs-lookup"><span data-stu-id="5a80f-179">Pre-compile applications and store the binary in Azure Storage.</span></span>


### <a name="script-action-on-a-running-cluster"></a><span data-ttu-id="5a80f-180">執行中叢集上的指令碼動作</span><span class="sxs-lookup"><span data-stu-id="5a80f-180">Script action on a running cluster</span></span>

<span data-ttu-id="5a80f-181">不同於在叢集建立期間使用的指令碼動作，在執行中叢集上執行的指令碼發生失敗並不會自動導致叢集變更為失敗的狀態。</span><span class="sxs-lookup"><span data-stu-id="5a80f-181">Unlike script actions used during cluster creation, a failure in a script ran on an already running cluster does not automatically cause the cluster to change to a failed state.</span></span> <span data-ttu-id="5a80f-182">指令碼完成後，叢集應該會回到「執行中」狀態。</span><span class="sxs-lookup"><span data-stu-id="5a80f-182">Once a script completes, the cluster should return to a "running" state.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a80f-183">即使叢集狀態為「執行中」，失敗的指令碼仍可能已造成問題。</span><span class="sxs-lookup"><span data-stu-id="5a80f-183">Even if the cluster has a 'running' state, the failed script may have broken things.</span></span> <span data-ttu-id="5a80f-184">例如，指令碼可能會刪除叢集所需的檔案。</span><span class="sxs-lookup"><span data-stu-id="5a80f-184">For example, a script could delete files needed by the cluster.</span></span>
>
> <span data-ttu-id="5a80f-185">指令碼動作會以根權限執行，因此您應該先確定您了解指令碼的作用，再將它套用到您的叢集。</span><span class="sxs-lookup"><span data-stu-id="5a80f-185">Scripts actions run with root privileges, so you should make sure that you understand what a script does before applying it to your cluster.</span></span>

<span data-ttu-id="5a80f-186">將指令碼套用到叢集時，如果指令碼執行成功，叢集狀態會從 [執行中] 變更為 [已接受]，再變更為 [HDInsight 設定]，最後回到 [執行中]。</span><span class="sxs-lookup"><span data-stu-id="5a80f-186">When applying a script to a cluster, the cluster state changes to from **Running** to **Accepted**, then **HDInsight configuration**, and finally back to **Running** for successful scripts.</span></span> <span data-ttu-id="5a80f-187">指令碼狀態會記錄在指令碼動作歷程記錄中，您可以使用此資訊來判斷指令碼是成功或失敗。</span><span class="sxs-lookup"><span data-stu-id="5a80f-187">The script status is logged in the script action history, and you can use this information to determine whether the script succeeded or failed.</span></span> <span data-ttu-id="5a80f-188">例如， `Get-AzureRmHDInsightScriptActionHistory` PowerShell Cmdlet 可用來檢視指令碼的狀態。</span><span class="sxs-lookup"><span data-stu-id="5a80f-188">For example, the `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet can be used to view the status of a script.</span></span> <span data-ttu-id="5a80f-189">它會傳回類似以下文字的資訊：</span><span class="sxs-lookup"><span data-stu-id="5a80f-189">It returns information similar to the following text:</span></span>

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> <span data-ttu-id="5a80f-190">如果您在叢集建立後變更叢集使用者 (管理員) 密碼，針對此叢集執行的指令碼動作可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="5a80f-190">If you have changed the cluster user (admin) password after the cluster was created, script actions ran against this cluster may fail.</span></span> <span data-ttu-id="5a80f-191">如果您有任何以背景工作角色節點為目標的持續性指令碼動作，當您調整叢集的規模時，這些指令碼動作可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="5a80f-191">If you have any persisted script actions that target worker nodes, these scripts may fail when you scale the cluster.</span></span>

## <a name="example-script-action-scripts"></a><span data-ttu-id="5a80f-192">範例指令碼動作指令碼</span><span class="sxs-lookup"><span data-stu-id="5a80f-192">Example Script Action scripts</span></span>

<span data-ttu-id="5a80f-193">指令碼動作的指令碼可以透過下列公用程式使用：</span><span class="sxs-lookup"><span data-stu-id="5a80f-193">Script Action scripts can be used through the following utilities:</span></span>

* <span data-ttu-id="5a80f-194">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5a80f-194">Azure portal</span></span>
* <span data-ttu-id="5a80f-195">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a80f-195">Azure PowerShell</span></span>
* <span data-ttu-id="5a80f-196">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5a80f-196">Azure CLI</span></span>
* <span data-ttu-id="5a80f-197">HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="5a80f-197">HDInsight .NET SDK</span></span>

<span data-ttu-id="5a80f-198">HDInsight 提供一些指令碼以在 HDInsight 叢集上安裝下列元件：</span><span class="sxs-lookup"><span data-stu-id="5a80f-198">HDInsight provides scripts to install the following components on HDInsight clusters:</span></span>

| <span data-ttu-id="5a80f-199">名稱</span><span class="sxs-lookup"><span data-stu-id="5a80f-199">Name</span></span> | <span data-ttu-id="5a80f-200">指令碼</span><span class="sxs-lookup"><span data-stu-id="5a80f-200">Script</span></span> |
| --- | --- |
| <span data-ttu-id="5a80f-201">**新增 Azure 儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="5a80f-201">**Add an Azure Storage account**</span></span> |<span data-ttu-id="5a80f-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh。請參閱[在 HDInsight 叢集新增儲存體](hdinsight-hadoop-add-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. See [Add additional storage to an HDInsight cluster](hdinsight-hadoop-add-storage.md).</span></span> |
| <span data-ttu-id="5a80f-203">**安裝色調**</span><span class="sxs-lookup"><span data-stu-id="5a80f-203">**Install Hue**</span></span> |<span data-ttu-id="5a80f-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh。請參閱 [在 HDInsight 叢集上安裝及使用色調](hdinsight-hadoop-hue-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. See [Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> |
| <span data-ttu-id="5a80f-205">**安裝 Presto**</span><span class="sxs-lookup"><span data-stu-id="5a80f-205">**Install Presto**</span></span> |<span data-ttu-id="5a80f-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh。請參閱[在 HDInsight 叢集上安裝和使用 Presto](hdinsight-hadoop-install-presto.md)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. See [Install and use Presto on HDInsight clusters](hdinsight-hadoop-install-presto.md).</span></span> |
| <span data-ttu-id="5a80f-207">**安裝 Solr**</span><span class="sxs-lookup"><span data-stu-id="5a80f-207">**Install Solr**</span></span> |<span data-ttu-id="5a80f-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh。請參閱 [在 HDInsight 叢集上安裝及使用 Solr](hdinsight-hadoop-solr-install-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> |
| <span data-ttu-id="5a80f-209">**安裝 Giraph**</span><span class="sxs-lookup"><span data-stu-id="5a80f-209">**Install Giraph**</span></span> |<span data-ttu-id="5a80f-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh。請參閱 [在 HDInsight 叢集上安裝及使用 Giraph](hdinsight-hadoop-giraph-install-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> |
| <span data-ttu-id="5a80f-211">**預先載入 Hive 程式庫**</span><span class="sxs-lookup"><span data-stu-id="5a80f-211">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="5a80f-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh。請參閱 [在 HDInsight 叢集上新增 Hive 程式庫](hdinsight-hadoop-add-hive-libraries.md)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md).</span></span> |
| <span data-ttu-id="5a80f-213">**安裝或更新 Mono**</span><span class="sxs-lookup"><span data-stu-id="5a80f-213">**Install or update Mono**</span></span> | <span data-ttu-id="5a80f-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash。</span><span class="sxs-lookup"><span data-stu-id="5a80f-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span></span> <span data-ttu-id="5a80f-215">請參閱[在 HDInsight 上安裝或更新 Mono](hdinsight-hadoop-install-mono.md)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-215">See [Install or update Mono on HDInsight](hdinsight-hadoop-install-mono.md).</span></span> |

## <a name="use-a-script-action-during-cluster-creation"></a><span data-ttu-id="5a80f-216">在建立叢集期間使用指令碼動作</span><span class="sxs-lookup"><span data-stu-id="5a80f-216">Use a Script Action during cluster creation</span></span>

<span data-ttu-id="5a80f-217">本節提供建立 HDInsight 叢集時以不同的方式使用指令碼動作的範例。</span><span class="sxs-lookup"><span data-stu-id="5a80f-217">This section provides examples on the different ways you can use script actions when creating an HDInsight cluster.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-the-azure-portal"></a><span data-ttu-id="5a80f-218">在建立叢集期間從 Azure 入口網站使用指令碼動作</span><span class="sxs-lookup"><span data-stu-id="5a80f-218">Use a Script Action during cluster creation from the Azure portal</span></span>

1. <span data-ttu-id="5a80f-219">依[在 HDInsight 建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)中的描述開始建立叢集。</span><span class="sxs-lookup"><span data-stu-id="5a80f-219">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="5a80f-220">進行至 [叢集摘要] 區段時停止。</span><span class="sxs-lookup"><span data-stu-id="5a80f-220">Stop when you reach the __Cluster summary__ section.</span></span>

2. <span data-ttu-id="5a80f-221">在 [叢集摘要] 區段中，選取 [進階設定] 的 [編輯] 連結。</span><span class="sxs-lookup"><span data-stu-id="5a80f-221">From the __Cluster summary__ section, select the __edit__ link for __Advanced settings__.</span></span>

    ![[Advanced settings] \(進階設定\) 連結](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. <span data-ttu-id="5a80f-223">從 [進階設定] 區段中，選取 [指令碼動作]。</span><span class="sxs-lookup"><span data-stu-id="5a80f-223">From the __Advanced settings__ section, select __Script actions__.</span></span> <span data-ttu-id="5a80f-224">從 [指令碼動作] 區段中，選取 [+ 送出新的]</span><span class="sxs-lookup"><span data-stu-id="5a80f-224">From the __Script actions__ section, select __+ Submit new__</span></span>

    ![送出新的指令碼動作](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. <span data-ttu-id="5a80f-226">使用 [Select a script] \(選取指令碼\) 項目選取預先製作的指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a80f-226">Use the __Select a script__ entry to select a pre-made script.</span></span> <span data-ttu-id="5a80f-227">若要使用自訂指令碼，請選取 [Custom] \(自訂\)，然後為您的指令碼提供 [Name] \(名稱\) 和 [Bash script URI] \(Bash 指令碼 URI\)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-227">To use a custom script, select __Custom__ and then provide the __Name__ and __Bash script URI__ for your script.</span></span>

    ![在選取指令碼表單中加入指令碼](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="5a80f-229">下表說明表單上的元素：</span><span class="sxs-lookup"><span data-stu-id="5a80f-229">The following table describes the elements on the form:</span></span>

    | <span data-ttu-id="5a80f-230">屬性</span><span class="sxs-lookup"><span data-stu-id="5a80f-230">Property</span></span> | <span data-ttu-id="5a80f-231">值</span><span class="sxs-lookup"><span data-stu-id="5a80f-231">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="5a80f-232">選取指令碼</span><span class="sxs-lookup"><span data-stu-id="5a80f-232">Select a script</span></span> | <span data-ttu-id="5a80f-233">若要使用自己的指令碼，請選取 [自訂]。</span><span class="sxs-lookup"><span data-stu-id="5a80f-233">To use your own script, select __Custom__.</span></span> <span data-ttu-id="5a80f-234">或是選取其中一個提供的指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a80f-234">Otherwise, select one of the provided scripts.</span></span> |
    | <span data-ttu-id="5a80f-235">名稱</span><span class="sxs-lookup"><span data-stu-id="5a80f-235">Name</span></span> |<span data-ttu-id="5a80f-236">指定指令碼動作的名稱。</span><span class="sxs-lookup"><span data-stu-id="5a80f-236">Specify a name for the script action.</span></span> |
    | <span data-ttu-id="5a80f-237">Bash 指令碼 URI</span><span class="sxs-lookup"><span data-stu-id="5a80f-237">Bash script URI</span></span> |<span data-ttu-id="5a80f-238">對自訂叢集所叫用的指令碼指定 URI。</span><span class="sxs-lookup"><span data-stu-id="5a80f-238">Specify the URI to the script that is invoked to customize the cluster.</span></span> |
    | <span data-ttu-id="5a80f-239">Head/Worker/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="5a80f-239">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="5a80f-240">指定執行自訂指令碼的節點 (**Head**、**Worker** 或 **ZooKeeper**)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-240">Specify the nodes (**Head**, **Worker**, or **ZooKeeper**) on which the customization script is run.</span></span> |
    | <span data-ttu-id="5a80f-241">參數</span><span class="sxs-lookup"><span data-stu-id="5a80f-241">Parameters</span></span> |<span data-ttu-id="5a80f-242">如果指令碼要求，請指定參數。</span><span class="sxs-lookup"><span data-stu-id="5a80f-242">Specify the parameters, if required by the script.</span></span> |

    <span data-ttu-id="5a80f-243">使用 [保存此指令碼動作] 項目，可確保在執行規模調整作業時套用此指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a80f-243">Use the __Persist this script action__ entry to ensure that the script is applied during scaling operations.</span></span>

5. <span data-ttu-id="5a80f-244">選取 [Create] \(建立\) 以儲存指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a80f-244">Select __Create__ to save the script.</span></span> <span data-ttu-id="5a80f-245">您可以接著使用 [+ Submit new] \(+ 送出新的\) 以加入另一個指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a80f-245">You can then use __+ Submit new__ to add another script.</span></span>

    ![多個指令碼動作](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    <span data-ttu-id="5a80f-247">當您完成加入指令碼後，使用 [選取] 按鈕，然後使用 [下一步] 按鈕返回 [叢集摘要] 區段。</span><span class="sxs-lookup"><span data-stu-id="5a80f-247">When you are done adding scripts, use the __Select__ button, and then the __Next__ button to return to the __Cluster summary__ section.</span></span>

3. <span data-ttu-id="5a80f-248">若要建立叢集，請從 [叢集摘要] 區段選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="5a80f-248">To create the cluster, select __Create__ from the __Cluster summary__ selection.</span></span>

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a><span data-ttu-id="5a80f-249">從 Azure 資源管理員範本使用指令碼動作</span><span class="sxs-lookup"><span data-stu-id="5a80f-249">Use a Script Action from Azure Resource Manager templates</span></span>

<span data-ttu-id="5a80f-250">本節中的範例展示要如何透過 Azure Resource Manager 範本使用指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="5a80f-250">The examples in this section demonstrate how to use script actions with Azure Resource Manager templates.</span></span>

#### <a name="before-you-begin"></a><span data-ttu-id="5a80f-251">開始之前</span><span class="sxs-lookup"><span data-stu-id="5a80f-251">Before you begin</span></span>

* <span data-ttu-id="5a80f-252">如需設定工作站以執行 HDInsight Powershell Cmdlet 的相關資訊，請參閱 [安裝並設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-252">For information about configuring a workstation to run HDInsight Powershell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="5a80f-253">如需如何建立範本的指示，請參閱 [編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-253">For instructions on how to create templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="5a80f-254">如果您之前未曾搭配使用Azure PowerShell 與資源管理員，請參閱 [將 Azure PowerShell 與 Azure 資源管理員搭配使用](../azure-resource-manager/powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-254">If you have not previously used Azure PowerShell with Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

#### <a name="create-clusters-using-script-action"></a><span data-ttu-id="5a80f-255">使用指令碼動作建立叢集</span><span class="sxs-lookup"><span data-stu-id="5a80f-255">Create clusters using Script Action</span></span>

1. <span data-ttu-id="5a80f-256">將下列範本複製到您的電腦上的位置。</span><span class="sxs-lookup"><span data-stu-id="5a80f-256">Copy the following template to a location on your computer.</span></span> <span data-ttu-id="5a80f-257">此範本會在前端節點和叢集的背景工作角色節點上安裝 Giraph。</span><span class="sxs-lookup"><span data-stu-id="5a80f-257">This template installs Giraph on the headnodes and worker nodes in the cluster.</span></span> <span data-ttu-id="5a80f-258">您也可以確認 JSON 範本是否有效。</span><span class="sxs-lookup"><span data-stu-id="5a80f-258">You can also verify if the JSON template is valid.</span></span> <span data-ttu-id="5a80f-259">將您的範本內容貼至 [JSONLint](http://jsonlint.com/)，這是一個線上 JSON 驗證器工具。</span><span class="sxs-lookup"><span data-stu-id="5a80f-259">Paste your template content into [JSONLint](http://jsonlint.com/), an online JSON validation tool.</span></span>

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. <span data-ttu-id="5a80f-260">啟動 Azure PowerShell 並且登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a80f-260">Start Azure PowerShell and Log in to your Azure account.</span></span> <span data-ttu-id="5a80f-261">提供您的認證之後，命令會傳回您的帳戶的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5a80f-261">After providing your credentials, the command returns information about your account.</span></span>

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. <span data-ttu-id="5a80f-262">如果您有多個訂用帳戶，請提供您想要用於部署的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="5a80f-262">If you have multiple subscriptions, provide the subscription ID you wish to use for deployment.</span></span>

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > <span data-ttu-id="5a80f-263">您可以使用 `Get-AzureRmSubscription` 來取得與您帳戶關聯的所有訂用帳戶清單，其中會包含每個訂用帳戶的訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="5a80f-263">You can use `Get-AzureRmSubscription` to get a list of all subscriptions associated with your account, which includes the subscription ID for each one.</span></span>

4. <span data-ttu-id="5a80f-264">如果您沒有現有資源群組，請建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="5a80f-264">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="5a80f-265">提供您的解決方案所需的資源群組名稱和位置。</span><span class="sxs-lookup"><span data-stu-id="5a80f-265">Provide the name of the resource group and location that you need for your solution.</span></span> <span data-ttu-id="5a80f-266">隨即傳回新資源群組的摘要。</span><span class="sxs-lookup"><span data-stu-id="5a80f-266">A summary of the new resource group is returned.</span></span>

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. <span data-ttu-id="5a80f-267">若要建立資源群組的部署，請執行 **New-AzureRmResourceGroupDeployment** 命令，並提供必要的參數。</span><span class="sxs-lookup"><span data-stu-id="5a80f-267">To create a deployment for your resource group, run the **New-AzureRmResourceGroupDeployment** command and provide the necessary parameters.</span></span> <span data-ttu-id="5a80f-268">這些參數包含下列資料：</span><span class="sxs-lookup"><span data-stu-id="5a80f-268">The parameters include the following data:</span></span>

    * <span data-ttu-id="5a80f-269">部署的名稱</span><span class="sxs-lookup"><span data-stu-id="5a80f-269">A name for your deployment</span></span>
    * <span data-ttu-id="5a80f-270">資源群組的名稱</span><span class="sxs-lookup"><span data-stu-id="5a80f-270">The name of your resource group</span></span>
    * <span data-ttu-id="5a80f-271">您建立之範本的路徑或 URL。</span><span class="sxs-lookup"><span data-stu-id="5a80f-271">The path or URL to the template you created.</span></span>

  <span data-ttu-id="5a80f-272">如果您的範本需要任何參數，您也必須傳遞這些參數。</span><span class="sxs-lookup"><span data-stu-id="5a80f-272">If your template requires any parameters, you must pass those parameters as well.</span></span> <span data-ttu-id="5a80f-273">在此案例中，用來在叢集上安裝 R 的指令碼動作不需要任何參數。</span><span class="sxs-lookup"><span data-stu-id="5a80f-273">In this case, the script action to install R on the cluster does not require any parameters.</span></span>

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    <span data-ttu-id="5a80f-274">系統會提示您針對範本中定義的參數提供值。</span><span class="sxs-lookup"><span data-stu-id="5a80f-274">You are prompted to provide values for the parameters defined in the template.</span></span>

1. <span data-ttu-id="5a80f-275">部署資源群組之後，便會顯示部署摘要。</span><span class="sxs-lookup"><span data-stu-id="5a80f-275">When the resource group has been deployed, a summary of the deployment is displayed.</span></span>

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. <span data-ttu-id="5a80f-276">如果您的部署失敗，您可以使用下列 Cmdlet 來取得失敗的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5a80f-276">If your deployment fails, you can use the following cmdlets to get information about the failures.</span></span>

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a><span data-ttu-id="5a80f-277">在建立叢集期間從 Azure PowerShell 使用指令碼動作</span><span class="sxs-lookup"><span data-stu-id="5a80f-277">Use a Script Action during cluster creation from Azure PowerShell</span></span>

<span data-ttu-id="5a80f-278">本節中，我們使用 [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) Cmdlet，使用指令碼動作叫用指令碼以自訂叢集。</span><span class="sxs-lookup"><span data-stu-id="5a80f-278">In this section, we use the [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet to invoke scripts by using Script Action to customize a cluster.</span></span> <span data-ttu-id="5a80f-279">在繼續之前，請確認您已安裝和設定 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="5a80f-279">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="5a80f-280">如需設定工作站以執行 HDInsight PowerShell Cmdlet 的相關資訊，請參閱 [安裝並設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-280">For information about configuring a workstation to run HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="5a80f-281">下列指令碼示範使用 PowerShell 建立叢集時如何套用指令碼動作：</span><span class="sxs-lookup"><span data-stu-id="5a80f-281">The following script demonstrates how to apply a script action when creating a cluster using PowerShell:</span></span>

<span data-ttu-id="5a80f-282">[!code-powershell[主要](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]</span><span class="sxs-lookup"><span data-stu-id="5a80f-282">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]</span></span>

<span data-ttu-id="5a80f-283">建立叢集可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="5a80f-283">It can take several minutes before the cluster is created.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-the-hdinsight-net-sdk"></a><span data-ttu-id="5a80f-284">在建立叢集期間從 HDInsight .NET SDK 使用指令碼動作</span><span class="sxs-lookup"><span data-stu-id="5a80f-284">Use a Script Action during cluster creation from the HDInsight .NET SDK</span></span>

<span data-ttu-id="5a80f-285">HDInsight .NET SDK 提供用戶端程式庫，讓您輕鬆地從 .NET 應用程式使用 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="5a80f-285">The HDInsight .NET SDK provides client libraries that makes it easier to work with HDInsight from a .NET application.</span></span> <span data-ttu-id="5a80f-286">如需程式碼範例，請參閱 [在 HDInsight 中使用 .NET SDK 建立以 Linux 為基礎的叢集](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-286">For a code sample, see [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span></span>

## <a name="apply-a-script-action-to-a-running-cluster"></a><span data-ttu-id="5a80f-287">將指令碼動作套用到執行中的叢集</span><span class="sxs-lookup"><span data-stu-id="5a80f-287">Apply a Script Action to a running cluster</span></span>

<span data-ttu-id="5a80f-288">在本節中，了解如何套用指令碼動作至執行中的叢集。</span><span class="sxs-lookup"><span data-stu-id="5a80f-288">In this section, learn how to apply script actions to a running cluster.</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-the-azure-portal"></a><span data-ttu-id="5a80f-289">從 Azure 入口網站將指令碼動作套用到執行中的叢集</span><span class="sxs-lookup"><span data-stu-id="5a80f-289">Apply a Script Action to a running cluster from the Azure portal</span></span>

1. <span data-ttu-id="5a80f-290">從 [Azure 入口網站](https://portal.azure.com)，選取您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="5a80f-290">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="5a80f-291">從 HDInsight 叢集概觀中，選取 [指令碼動作] 磚。</span><span class="sxs-lookup"><span data-stu-id="5a80f-291">From the HDInsight cluster overview, select the **Script Actions** tile.</span></span>

    ![指令碼動作磚](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="5a80f-293">您也可以從 [設定] 區段中，依序選取 [所有設定] 和 [指令碼動作]。</span><span class="sxs-lookup"><span data-stu-id="5a80f-293">You can also select **All settings** and then select **Script Actions** from the Settings section.</span></span>

3. <span data-ttu-id="5a80f-294">從 [指令碼動作] 區段的頂端，選取 [送出新的]。</span><span class="sxs-lookup"><span data-stu-id="5a80f-294">From the top of the Script Actions section, select **Submit new**.</span></span>

    ![將指令碼加入執行中的叢集](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. <span data-ttu-id="5a80f-296">使用 [Select a script] \(選取指令碼\) 項目選取預先製作的指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a80f-296">Use the __Select a script__ entry to select a pre-made script.</span></span> <span data-ttu-id="5a80f-297">若要使用自訂指令碼，請選取 [Custom] \(自訂\)，然後為您的指令碼提供 [Name] \(名稱\) 和 [Bash script URI] \(Bash 指令碼 URI\)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-297">To use a custom script, select __Custom__ and then provide the __Name__ and __Bash script URI__ for your script.</span></span>

    ![在選取指令碼表單中加入指令碼](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="5a80f-299">下表說明表單上的元素：</span><span class="sxs-lookup"><span data-stu-id="5a80f-299">The following table describes the elements on the form:</span></span>

    | <span data-ttu-id="5a80f-300">屬性</span><span class="sxs-lookup"><span data-stu-id="5a80f-300">Property</span></span> | <span data-ttu-id="5a80f-301">值</span><span class="sxs-lookup"><span data-stu-id="5a80f-301">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="5a80f-302">選取指令碼</span><span class="sxs-lookup"><span data-stu-id="5a80f-302">Select a script</span></span> | <span data-ttu-id="5a80f-303">若要使用自己的指令碼，請選取 [自訂]。</span><span class="sxs-lookup"><span data-stu-id="5a80f-303">To use your own script, select __custom__.</span></span> <span data-ttu-id="5a80f-304">否則，請選取提供的指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a80f-304">Otherwise, select a provided script.</span></span> |
    | <span data-ttu-id="5a80f-305">名稱</span><span class="sxs-lookup"><span data-stu-id="5a80f-305">Name</span></span> |<span data-ttu-id="5a80f-306">指定指令碼動作的名稱。</span><span class="sxs-lookup"><span data-stu-id="5a80f-306">Specify a name for the script action.</span></span> |
    | <span data-ttu-id="5a80f-307">Bash 指令碼 URI</span><span class="sxs-lookup"><span data-stu-id="5a80f-307">Bash script URI</span></span> |<span data-ttu-id="5a80f-308">對自訂叢集所叫用的指令碼指定 URI。</span><span class="sxs-lookup"><span data-stu-id="5a80f-308">Specify the URI to the script that is invoked to customize the cluster.</span></span> |
    | <span data-ttu-id="5a80f-309">Head/Worker/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="5a80f-309">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="5a80f-310">指定執行自訂指令碼的節點 (**Head**、**Worker** 或 **ZooKeeper**)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-310">Specify the nodes (**Head**, **Worker**, or **ZooKeeper**) on which the customization script is run.</span></span> |
    | <span data-ttu-id="5a80f-311">參數</span><span class="sxs-lookup"><span data-stu-id="5a80f-311">Parameters</span></span> |<span data-ttu-id="5a80f-312">如果指令碼要求，請指定參數。</span><span class="sxs-lookup"><span data-stu-id="5a80f-312">Specify the parameters, if required by the script.</span></span> |

    <span data-ttu-id="5a80f-313">使用 [保存此指令碼動作] 項目，可確保在執行規模調整作業時套用此指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a80f-313">Use the __Persist this script action__ entry to make sure the script is applied during scaling operations.</span></span>

5. <span data-ttu-id="5a80f-314">最後，使用 [建立] 按鈕將指令碼套用到叢集。</span><span class="sxs-lookup"><span data-stu-id="5a80f-314">Finally, use the **Create** button to apply the script to the cluster.</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-azure-powershell"></a><span data-ttu-id="5a80f-315">從 Azure PowerShell 將指令碼動作套用到執行中的叢集</span><span class="sxs-lookup"><span data-stu-id="5a80f-315">Apply a Script Action to a running cluster from Azure PowerShell</span></span>

<span data-ttu-id="5a80f-316">在繼續之前，請確認您已安裝和設定 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="5a80f-316">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="5a80f-317">如需設定工作站以執行 HDInsight PowerShell Cmdlet 的相關資訊，請參閱 [安裝並設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-317">For information about configuring a workstation to run HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="5a80f-318">下列範例示範如何將指令碼動作套用至執行中的叢集：</span><span class="sxs-lookup"><span data-stu-id="5a80f-318">The following example demonstrates how to apply a script action to a running cluster:</span></span>

<span data-ttu-id="5a80f-319">[!code-powershell[主要](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]</span><span class="sxs-lookup"><span data-stu-id="5a80f-319">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]</span></span>

<span data-ttu-id="5a80f-320">作業完成後，您會收到類似以下的訊息：</span><span class="sxs-lookup"><span data-stu-id="5a80f-320">Once the operation completes, you receive information similar to the following text:</span></span>

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-to-a-running-cluster-from-the-azure-cli"></a><span data-ttu-id="5a80f-321">從 Azure CLI 將指令碼動作套用到執行中的叢集</span><span class="sxs-lookup"><span data-stu-id="5a80f-321">Apply a Script Action to a running cluster from the Azure CLI</span></span>

<span data-ttu-id="5a80f-322">在繼續之前，請確認您已安裝和設定 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="5a80f-322">Before proceeding, make sure you have installed and configured the Azure CLI.</span></span> <span data-ttu-id="5a80f-323">如需詳細資訊，請參閱 [安裝 Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-323">For more information, see [Install the Azure CLI](../cli-install-nodejs.md).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="5a80f-324">若要切換至 Azure Resource Manager 模式，請於命令列使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="5a80f-324">To switch to Azure Resource Manager mode, use the following command at the command line:</span></span>

        azure config mode arm

2. <span data-ttu-id="5a80f-325">使用下列命令來驗證您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a80f-325">Use the following to authenticate to your Azure subscription.</span></span>

        azure login

3. <span data-ttu-id="5a80f-326">使用下列命令將指令碼動作套用至執行中的叢集</span><span class="sxs-lookup"><span data-stu-id="5a80f-326">Use the following command to apply a script action to a running cluster</span></span>

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    <span data-ttu-id="5a80f-327">如果省略這個命令的參數，系統會提示您使用。</span><span class="sxs-lookup"><span data-stu-id="5a80f-327">If you omit parameters for this command, you are prompted for them.</span></span> <span data-ttu-id="5a80f-328">如果您以 `-u` 指定的指令碼接受參數，您可以使用 `-p` 參數來指定它們。</span><span class="sxs-lookup"><span data-stu-id="5a80f-328">If the script you specify with `-u` accepts parameters, you can specify them using the `-p` parameter.</span></span>

    <span data-ttu-id="5a80f-329">有效的節點類型為 `headnode``workernode` 和 `zookeeper`。</span><span class="sxs-lookup"><span data-stu-id="5a80f-329">Valid node types are `headnode`, `workernode`, and `zookeeper`.</span></span> <span data-ttu-id="5a80f-330">如果指令碼應該要套用到多個節點類型，請指定以 ';' 分隔類型。</span><span class="sxs-lookup"><span data-stu-id="5a80f-330">If the script should be applied to multiple node types, specify the types separated by a ';'.</span></span> <span data-ttu-id="5a80f-331">例如： `-n headnode;workernode`。</span><span class="sxs-lookup"><span data-stu-id="5a80f-331">For example, `-n headnode;workernode`.</span></span>

    <span data-ttu-id="5a80f-332">若要保留指令碼，請新增 `--persistOnSuccess`。</span><span class="sxs-lookup"><span data-stu-id="5a80f-332">To persist the script, add the `--persistOnSuccess`.</span></span> <span data-ttu-id="5a80f-333">您之後也可以使用 `azure hdinsight script-action persisted set` 來保存指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a80f-333">You can also persist the script later by using `azure hdinsight script-action persisted set`.</span></span>

    <span data-ttu-id="5a80f-334">作業完成後，您會收到類似下列文字的輸出：</span><span class="sxs-lookup"><span data-stu-id="5a80f-334">Once the job completes, you receive output similar to the following text:</span></span>

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-to-a-running-cluster-using-rest-api"></a><span data-ttu-id="5a80f-335">使用 REST API 將指令碼動作套用到執行中的叢集</span><span class="sxs-lookup"><span data-stu-id="5a80f-335">Apply a Script Action to a running cluster using REST API</span></span>

<span data-ttu-id="5a80f-336">請參閱 [在執行中的叢集執行指令碼動作](https://msdn.microsoft.com/library/azure/mt668441.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-336">See [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-the-hdinsight-net-sdk"></a><span data-ttu-id="5a80f-337">從 HDInsight .NET SDK 將指令碼動作套用到執行中的叢集</span><span class="sxs-lookup"><span data-stu-id="5a80f-337">Apply a Script Action to a running cluster from the HDInsight .NET SDK</span></span>

<span data-ttu-id="5a80f-338">如需使用 .NET SDK 將指令碼套用到叢集的範例，請參閱 [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-338">For an example of using the .NET SDK to apply scripts to a cluster, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

## <a name="view-history-promote-and-demote-script-actions"></a><span data-ttu-id="5a80f-339">檢視歷程記錄、升級和降級指令碼動作</span><span class="sxs-lookup"><span data-stu-id="5a80f-339">View history, promote, and demote Script Actions</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="5a80f-340">使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5a80f-340">Using the Azure portal</span></span>

1. <span data-ttu-id="5a80f-341">從 [Azure 入口網站](https://portal.azure.com)，選取您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="5a80f-341">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="5a80f-342">從 HDInsight 叢集概觀中，選取 [指令碼動作] 磚。</span><span class="sxs-lookup"><span data-stu-id="5a80f-342">From the HDInsight cluster overview, select the **Script Actions** tile.</span></span>

    ![指令碼動作磚](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="5a80f-344">您也可以從 [設定] 區段中，依序選取 [所有設定] 和 [指令碼動作]。</span><span class="sxs-lookup"><span data-stu-id="5a80f-344">You can also select **All settings** and then select **Script Actions** from the Settings section.</span></span>

4. <span data-ttu-id="5a80f-345">此叢集的指令碼歷程記錄會顯示在 [指令碼動作] 區段。</span><span class="sxs-lookup"><span data-stu-id="5a80f-345">A history of scripts for this cluster is displayed on the Script Actions section.</span></span> <span data-ttu-id="5a80f-346">此資訊包含持續性指令碼清單。</span><span class="sxs-lookup"><span data-stu-id="5a80f-346">This information includes a list of persisted scripts.</span></span> <span data-ttu-id="5a80f-347">在以下的螢幕擷取畫面中，您可以看到 Solr 指令碼已在此叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="5a80f-347">In the screenshot below, you can see that the Solr script has been ran on this cluster.</span></span> <span data-ttu-id="5a80f-348">此螢幕擷取畫面不會顯示任何持續性指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a80f-348">The screenshot does not show any persisted scripts.</span></span>

    ![指令碼動作區段](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. <span data-ttu-id="5a80f-350">選取歷程記錄中的指令碼，便會顯示此指令碼的 [屬性] 區段。</span><span class="sxs-lookup"><span data-stu-id="5a80f-350">Selecting a script from the history displays the Properties section for this script.</span></span> <span data-ttu-id="5a80f-351">從視窗的頂端，您可以重新執行指令碼或將其升階。</span><span class="sxs-lookup"><span data-stu-id="5a80f-351">From the top of the screen, you can rerun the script or promote it.</span></span>

    ![指令碼動作屬性](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. <span data-ttu-id="5a80f-353">您也可以使用 [指令碼動作] 區段上項目右邊的 **...** 來執行動作。</span><span class="sxs-lookup"><span data-stu-id="5a80f-353">You can also use the **...** to the right of entries on the Script Actions section to perform actions.</span></span>

    ![指令碼動作...使用情況](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a><span data-ttu-id="5a80f-355">使用 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a80f-355">Using Azure PowerShell</span></span>

| <span data-ttu-id="5a80f-356">使用下列...</span><span class="sxs-lookup"><span data-stu-id="5a80f-356">Use the following...</span></span> | <span data-ttu-id="5a80f-357">來 ...</span><span class="sxs-lookup"><span data-stu-id="5a80f-357">To ...</span></span> |
| --- | --- |
| <span data-ttu-id="5a80f-358">Get-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="5a80f-358">Get-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="5a80f-359">擷取持續性指令碼動作的資訊</span><span class="sxs-lookup"><span data-stu-id="5a80f-359">Retrieve information on persisted script actions</span></span> |
| <span data-ttu-id="5a80f-360">Get-AzureRmHDInsightScriptActionHistory</span><span class="sxs-lookup"><span data-stu-id="5a80f-360">Get-AzureRmHDInsightScriptActionHistory</span></span> |<span data-ttu-id="5a80f-361">擷取已套用到叢集的指令碼動作歷程記錄，或特定指令碼的詳細資料</span><span class="sxs-lookup"><span data-stu-id="5a80f-361">Retrieve a history of script actions applied to the cluster, or details for a specific script</span></span> |
| <span data-ttu-id="5a80f-362">Set-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="5a80f-362">Set-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="5a80f-363">將臨時性指令碼動作升級為持續性指令碼動作</span><span class="sxs-lookup"><span data-stu-id="5a80f-363">Promotes an ad hoc script action to a persisted script action</span></span> |
| <span data-ttu-id="5a80f-364">Remove-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="5a80f-364">Remove-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="5a80f-365">將持續性指令碼動作降級為臨時性指令碼動作</span><span class="sxs-lookup"><span data-stu-id="5a80f-365">Demotes a persisted script action to an ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="5a80f-366">使用 `Remove-AzureRmHDInsightPersistedScriptAction` 無法復原指令碼執行的動作。</span><span class="sxs-lookup"><span data-stu-id="5a80f-366">Using `Remove-AzureRmHDInsightPersistedScriptAction` does not undo the actions performed by a script.</span></span> <span data-ttu-id="5a80f-367">此 Cmdlet 只會移除持續性旗標。</span><span class="sxs-lookup"><span data-stu-id="5a80f-367">This cmdlet only removes the persisted flag.</span></span>

<span data-ttu-id="5a80f-368">下列範例指令碼示範如何使用 Cmdlet 來升級而後降級指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a80f-368">The following example script demonstrates using the cmdlets to promote, then demote a script.</span></span>

<span data-ttu-id="5a80f-369">[!code-powershell[主要](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]</span><span class="sxs-lookup"><span data-stu-id="5a80f-369">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]</span></span>

### <a name="using-the-azure-cli"></a><span data-ttu-id="5a80f-370">使用 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5a80f-370">Using the Azure CLI</span></span>

| <span data-ttu-id="5a80f-371">使用下列...</span><span class="sxs-lookup"><span data-stu-id="5a80f-371">Use the following...</span></span> | <span data-ttu-id="5a80f-372">來 ...</span><span class="sxs-lookup"><span data-stu-id="5a80f-372">To ...</span></span> |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |<span data-ttu-id="5a80f-373">擷取保存的指令碼動作清單</span><span class="sxs-lookup"><span data-stu-id="5a80f-373">Retrieve a list of persisted script actions</span></span> |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |<span data-ttu-id="5a80f-374">擷取特定的保存指令碼動作資訊</span><span class="sxs-lookup"><span data-stu-id="5a80f-374">Retrieve information on a specific persisted script action</span></span> |
| `azure hdinsight script-action history list <clustername>` |<span data-ttu-id="5a80f-375">擷取已套用到叢集的指令碼動作歷程記錄</span><span class="sxs-lookup"><span data-stu-id="5a80f-375">Retrieve a history of script actions applied to the cluster</span></span> |
| `azure hdinsight script-action history show <clustername> <scriptname>` |<span data-ttu-id="5a80f-376">擷取特定指令碼動作的資訊</span><span class="sxs-lookup"><span data-stu-id="5a80f-376">Retrieve information on a specific script action</span></span> |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |<span data-ttu-id="5a80f-377">將臨時性指令碼動作升級為持續性指令碼動作</span><span class="sxs-lookup"><span data-stu-id="5a80f-377">Promotes an ad hoc script action to a persisted script action</span></span> |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |<span data-ttu-id="5a80f-378">將持續性指令碼動作降級為臨時性指令碼動作</span><span class="sxs-lookup"><span data-stu-id="5a80f-378">Demotes a persisted script action to an ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="5a80f-379">使用 `azure hdinsight script-action persisted delete` 無法復原指令碼執行的動作。</span><span class="sxs-lookup"><span data-stu-id="5a80f-379">Using `azure hdinsight script-action persisted delete` does not undo the actions performed by a script.</span></span> <span data-ttu-id="5a80f-380">此 Cmdlet 只會移除持續性旗標。</span><span class="sxs-lookup"><span data-stu-id="5a80f-380">This cmdlet only removes the persisted flag.</span></span>

### <a name="using-the-hdinsight-net-sdk"></a><span data-ttu-id="5a80f-381">使用 HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="5a80f-381">Using the HDInsight .NET SDK</span></span>

<span data-ttu-id="5a80f-382">如需使用 .NET SDK 從叢集擷取指令碼歷程記錄、升級或降級指令碼的範例，請參閱 [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-382">For an example of using the .NET SDK to retrieve script history from a cluster, promote or demote scripts, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

> [!NOTE]
> <span data-ttu-id="5a80f-383">這個範例也示範如何使用 .NET SDK 安裝 HDInsight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5a80f-383">This example also demonstrates how to install an HDInsight application using the .NET SDK.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="5a80f-384">支援在 HDInsight 叢集上使用開放原始碼軟體</span><span class="sxs-lookup"><span data-stu-id="5a80f-384">Support for open-source software used on HDInsight clusters</span></span>

<span data-ttu-id="5a80f-385">Microsoft Azure HDInsight 服務使用以 Hadoop 為中心的開放原始碼技術生態系統。</span><span class="sxs-lookup"><span data-stu-id="5a80f-385">The Microsoft Azure HDInsight service uses an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="5a80f-386">Microsoft Azure 可為開放原始碼技術提供一般層級的支援。</span><span class="sxs-lookup"><span data-stu-id="5a80f-386">Microsoft Azure provides a general level of support for open-source technologies.</span></span> <span data-ttu-id="5a80f-387">如需詳細資訊，請參閱 [Azure 支援常見問題集網站](https://azure.microsoft.com/support/faq/)中的**支援範圍**一節。</span><span class="sxs-lookup"><span data-stu-id="5a80f-387">For more information, see the **Support Scope** section of the [Azure Support FAQ website](https://azure.microsoft.com/support/faq/).</span></span> <span data-ttu-id="5a80f-388">HDInsight 服務針對內建元件提供額外等級的支援。</span><span class="sxs-lookup"><span data-stu-id="5a80f-388">The HDInsight service provides an additional level of support for built-in components.</span></span>

<span data-ttu-id="5a80f-389">HDInsight 服務中有兩種類型的開放原始碼元件可用：</span><span class="sxs-lookup"><span data-stu-id="5a80f-389">There are two types of open-source components that are available in the HDInsight service:</span></span>

* <span data-ttu-id="5a80f-390">**內建元件** - 這些元件預先安裝在 HDInsight 叢集上，並且提供叢集的核心功能。</span><span class="sxs-lookup"><span data-stu-id="5a80f-390">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of the cluster.</span></span> <span data-ttu-id="5a80f-391">例如，YARN ResourceManager、Hive 查詢語言 (HiveQL) 及 Mahout 程式庫都屬於這個類別。</span><span class="sxs-lookup"><span data-stu-id="5a80f-391">For example, YARN ResourceManager, the Hive query language (HiveQL), and the Mahout library belong to this category.</span></span> <span data-ttu-id="5a80f-392">叢集元件的完整清單可於 [HDInsight 所提供 Hadoop 叢集版本的新功能](hdinsight-component-versioning.md)中取得。</span><span class="sxs-lookup"><span data-stu-id="5a80f-392">A full list of cluster components is available in [What's new in the Hadoop cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
* <span data-ttu-id="5a80f-393">**自訂元件** - 身為叢集使用者的您可以安裝社群中可用或是您建立的任何元件，或者在工作負載中使用。</span><span class="sxs-lookup"><span data-stu-id="5a80f-393">**Custom components** - You, as a user of the cluster, can install or use in your workload any component available in the community or created by you.</span></span>

> [!WARNING]
> <span data-ttu-id="5a80f-394">對隨 HDInsight 叢集提供的元件會有完整支援。</span><span class="sxs-lookup"><span data-stu-id="5a80f-394">Components provided with the HDInsight cluster are fully supported.</span></span> <span data-ttu-id="5a80f-395">Microsoft 支援服務可協助隔離和解決這些元件的相關問題。</span><span class="sxs-lookup"><span data-stu-id="5a80f-395">Microsoft Support helps to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="5a80f-396">自訂元件則獲得商務上合理的支援，協助您進一步疑難排解問題。</span><span class="sxs-lookup"><span data-stu-id="5a80f-396">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="5a80f-397">Microsoft 支援服務可能可以解決問題，也可能要求您利用可用的開放原始碼技術管道，找到該技術的深度專業知識。</span><span class="sxs-lookup"><span data-stu-id="5a80f-397">Microsoft support may be able to resolve the issue OR they may ask you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="5a80f-398">例如，有許多社群網站可以使用，像是：[HDInsight 的 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)、[http://stackoverflow.com](http://stackoverflow.com)。另外，Apache 專案在 [http://apache.org](http://apache.org) 上有專案網站，例如 [Hadoop](http://hadoop.apache.org/)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-398">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

<span data-ttu-id="5a80f-399">HDInsight 服務提供數種方式以使用自訂元件。</span><span class="sxs-lookup"><span data-stu-id="5a80f-399">The HDInsight service provides several ways to use custom components.</span></span> <span data-ttu-id="5a80f-400">無論元件如何使用或如何安裝在叢集上，都適用相同層級的支援。</span><span class="sxs-lookup"><span data-stu-id="5a80f-400">The same level of support applies, regardless of how a component is used or installed on the cluster.</span></span> <span data-ttu-id="5a80f-401">下列清單描述自訂元件可用於 HDInsight 叢集之最常見方式：</span><span class="sxs-lookup"><span data-stu-id="5a80f-401">The following list describes the most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="5a80f-402">工作提交 - Hadoop 或其他類型的工作，執行或使用可以提交給叢集的自訂元件。</span><span class="sxs-lookup"><span data-stu-id="5a80f-402">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted to the cluster.</span></span>

2. <span data-ttu-id="5a80f-403">叢集自訂 - 在叢集建立期間，您可以指定額外設定以及會安裝在叢集節點上的自訂元件。</span><span class="sxs-lookup"><span data-stu-id="5a80f-403">Cluster customization - During cluster creation, you can specify additional settings and custom components that are installed on the cluster nodes.</span></span>

3. <span data-ttu-id="5a80f-404">範例 - 對於熱門自訂元件，Microsoft 和其他提供者可能會提供如何在 HDInsight 叢集上使用這些元件的範例。</span><span class="sxs-lookup"><span data-stu-id="5a80f-404">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on the HDInsight clusters.</span></span> <span data-ttu-id="5a80f-405">提供這些範例，但是沒有支援。</span><span class="sxs-lookup"><span data-stu-id="5a80f-405">These samples are provided without support.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5a80f-406">疑難排解</span><span class="sxs-lookup"><span data-stu-id="5a80f-406">Troubleshooting</span></span>

<span data-ttu-id="5a80f-407">您可以使用 Ambari Web UI 來檢視指令碼動作所記錄的資訊。</span><span class="sxs-lookup"><span data-stu-id="5a80f-407">You can use Ambari web UI to view information logged by script actions.</span></span> <span data-ttu-id="5a80f-408">如果指令碼在叢集建立期間失敗，則與該叢集相關聯的預設儲存體帳戶中也會有記錄檔。</span><span class="sxs-lookup"><span data-stu-id="5a80f-408">If the script fails during cluster creation, the logs are also available in the default storage account associated with the cluster.</span></span> <span data-ttu-id="5a80f-409">本節提供關於如何使用這兩個選項擷取記錄檔的資訊。</span><span class="sxs-lookup"><span data-stu-id="5a80f-409">This section provides information on how to retrieve the logs using both these options.</span></span>

### <a name="using-the-ambari-web-ui"></a><span data-ttu-id="5a80f-410">使用 Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="5a80f-410">Using the Ambari Web UI</span></span>

1. <span data-ttu-id="5a80f-411">在瀏覽器中，瀏覽至 https://CLUSTERNAME.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="5a80f-411">In your browser, navigate to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="5a80f-412">將 CLUSTERNAME 取代為 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="5a80f-412">Replace CLUSTERNAME with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="5a80f-413">出現提示時，輸入管理帳戶名稱 (admin) 和叢集的密碼。</span><span class="sxs-lookup"><span data-stu-id="5a80f-413">When prompted, enter the admin account name (admin) and password for the cluster.</span></span> <span data-ttu-id="5a80f-414">您可能必須在 Web 表單中重新輸入系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="5a80f-414">You may have to reenter the admin credentials in a web form.</span></span>

2. <span data-ttu-id="5a80f-415">在頁面頂端的列中，選取 **ops** 項目。</span><span class="sxs-lookup"><span data-stu-id="5a80f-415">From the bar at the top of the page, select the **ops** entry.</span></span> <span data-ttu-id="5a80f-416">隨即顯示透過 Ambari 在叢集上執行的目前和先前作業的清單。</span><span class="sxs-lookup"><span data-stu-id="5a80f-416">A list of current and previous operations performed on the cluster through Ambari is displayed.</span></span>

    ![Ambari Web UI 列與選取的 ops](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. <span data-ttu-id="5a80f-418">尋找在 [作業] 欄位中有 **run\_customscriptaction** 的項目。</span><span class="sxs-lookup"><span data-stu-id="5a80f-418">Find the entries that have **run\_customscriptaction** in the **Operations** column.</span></span> <span data-ttu-id="5a80f-419">這些項目是在執行指令碼動作時建立的。</span><span class="sxs-lookup"><span data-stu-id="5a80f-419">These entries are created when the Script Actions run.</span></span>

    ![作業的螢幕擷取畫面](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    <span data-ttu-id="5a80f-421">若要檢視 STDOUT 和 STDERR 輸出，請選取 run\customscriptaction 項目，並向下鑽研連結。</span><span class="sxs-lookup"><span data-stu-id="5a80f-421">To view the STDOUT and STDERR output, select the run\customscriptaction entry and drill down through the links.</span></span> <span data-ttu-id="5a80f-422">執行指令碼時會產生此輸出，其中可能包含實用的資訊。</span><span class="sxs-lookup"><span data-stu-id="5a80f-422">This output is generated when the script runs, and may contain useful information.</span></span>

### <a name="access-logs-from-the-default-storage-account"></a><span data-ttu-id="5a80f-423">從預設的儲存體帳戶存取記錄檔</span><span class="sxs-lookup"><span data-stu-id="5a80f-423">Access logs from the default storage account</span></span>

<span data-ttu-id="5a80f-424">如果叢集建立因指令碼動作錯誤而失敗，您可以從叢集存放區帳戶存取記錄。</span><span class="sxs-lookup"><span data-stu-id="5a80f-424">If the cluster creation fails due to a script action error, the logs can be accessed from the cluster storage account.</span></span>

* <span data-ttu-id="5a80f-425">儲存體記錄檔位於 `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`。</span><span class="sxs-lookup"><span data-stu-id="5a80f-425">The storage logs are available at `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span></span>

    ![作業的螢幕擷取畫面](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    <span data-ttu-id="5a80f-427">在此目錄下，記錄檔會個別針對前端節點、背景工作節點和 Zookeeper 節點進行組織。</span><span class="sxs-lookup"><span data-stu-id="5a80f-427">Under this directory, the logs are organized separately for headnode, workernode, and zookeeper nodes.</span></span> <span data-ttu-id="5a80f-428">部分範例如下：</span><span class="sxs-lookup"><span data-stu-id="5a80f-428">Some examples are:</span></span>

    * <span data-ttu-id="5a80f-429">**前端節點** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="5a80f-429">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="5a80f-430">**背景工作節點** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="5a80f-430">**Worker node** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="5a80f-431">**Zookeeper 節點** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="5a80f-431">**Zookeeper node** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span></span>

* <span data-ttu-id="5a80f-432">對應主機的所有 stdout 和 stderr 都會上傳至儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a80f-432">All stdout and stderr of the corresponding host is uploaded to the storage account.</span></span> <span data-ttu-id="5a80f-433">每個指令碼動作分別有一個 **output-\*.txt** 和 **errors-\*.txt**。</span><span class="sxs-lookup"><span data-stu-id="5a80f-433">There is one **output-\*.txt** and **errors-\*.txt** for each script action.</span></span> <span data-ttu-id="5a80f-434">output-*.txt 檔案包含在主機上執行之指令碼的 URI 相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5a80f-434">The output-*.txt file contains information about the URI of the script that got run on the host.</span></span> <span data-ttu-id="5a80f-435">例如</span><span class="sxs-lookup"><span data-stu-id="5a80f-435">For example</span></span>

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* <span data-ttu-id="5a80f-436">您有可能重複建立具有相同名稱的指令碼動作叢集。</span><span class="sxs-lookup"><span data-stu-id="5a80f-436">It's possible that you repeatedly create a script action cluster with the same name.</span></span> <span data-ttu-id="5a80f-437">在這種情況下，您可以根據 DATE 資料夾名稱來區分相關的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="5a80f-437">In such case, you can distinguish the relevant logs based on the DATE folder name.</span></span> <span data-ttu-id="5a80f-438">例如，在不同的日期為叢集 (mycluster) 建立的資料夾結構會類似下列記錄檔項目：</span><span class="sxs-lookup"><span data-stu-id="5a80f-438">For example, the folder structure for a cluster (mycluster) created on different dates appears similar to the following log entries:</span></span>

    <span data-ttu-id="5a80f-439">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span><span class="sxs-lookup"><span data-stu-id="5a80f-439">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span></span>

* <span data-ttu-id="5a80f-440">如果您在同一天建立具有相同名稱的指令碼動作叢集，您可以使用唯一的前置詞來識別相關的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="5a80f-440">If you create a script action cluster with the same name on the same day, you can use the unique prefix to identify the relevant log files.</span></span>

* <span data-ttu-id="5a80f-441">如果您在接近 12:00 AM (午夜) 時建立叢集，記錄檔可能會橫跨兩天。</span><span class="sxs-lookup"><span data-stu-id="5a80f-441">If you create a cluster near 12:00AM (midnight), it's possible that the log files span across two days.</span></span> <span data-ttu-id="5a80f-442">在這種情況下，您會看到相同的叢集有兩個不同的日期資料夾。</span><span class="sxs-lookup"><span data-stu-id="5a80f-442">In such cases, you see two different date folders for the same cluster.</span></span>

* <span data-ttu-id="5a80f-443">將記錄檔上傳至預設容器可能需要 5 分鐘，特別是大型叢集。</span><span class="sxs-lookup"><span data-stu-id="5a80f-443">Uploading log files to the default container can take up to 5 mins, especially for large clusters.</span></span> <span data-ttu-id="5a80f-444">因此，如果您想要存取記錄檔，則不應在指令碼動作失敗時立即刪除叢集。</span><span class="sxs-lookup"><span data-stu-id="5a80f-444">So, if you want to access the logs, you should not immediately delete the cluster if a script action fails.</span></span>

### <a name="ambari-watchdog"></a><span data-ttu-id="5a80f-445">Ambari 看門狗</span><span class="sxs-lookup"><span data-stu-id="5a80f-445">Ambari watchdog</span></span>

> [!WARNING]
> <span data-ttu-id="5a80f-446">請勿變更以 Linux 為基礎之 HDInsight 叢集上的 Ambari 看門狗 (hdinsightwatchdog) 密碼。</span><span class="sxs-lookup"><span data-stu-id="5a80f-446">Do not change the password for the Ambari Watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="5a80f-447">變更此帳戶的密碼會破壞在 HDInsight 叢集上執行新指令碼動作的能力。</span><span class="sxs-lookup"><span data-stu-id="5a80f-447">Changing the password for this account breaks the ability to run new script actions on the HDInsight cluster.</span></span>

### <a name="cant-import-name-blobservice"></a><span data-ttu-id="5a80f-448">無法匯入名稱 BlobService</span><span class="sxs-lookup"><span data-stu-id="5a80f-448">Can't import name BlobService</span></span>

<span data-ttu-id="5a80f-449">__徵兆__：指令碼動作失敗。</span><span class="sxs-lookup"><span data-stu-id="5a80f-449">__Symptoms__: The script action fails.</span></span> <span data-ttu-id="5a80f-450">在 Ambari 中檢視作業時，會顯示類似下列錯誤的訊息：</span><span class="sxs-lookup"><span data-stu-id="5a80f-450">Text similar to the following error is displayed when you view the operation in Ambari:</span></span>

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

<span data-ttu-id="5a80f-451">__原因__︰如果您升級隨附於 HDInsight 叢集的 Python Azure 儲存體用戶端，就會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="5a80f-451">__Cause__: This error occurs if you upgrade the Python Azure Storage client that is included with the HDInsight cluster.</span></span> <span data-ttu-id="5a80f-452">HDInsight 需要 Azure 儲存體用戶端 0.20.0。</span><span class="sxs-lookup"><span data-stu-id="5a80f-452">HDInsight expects Azure Storage client 0.20.0.</span></span>

<span data-ttu-id="5a80f-453">__解決方案__︰若要解決這個錯誤，請使用 `ssh` 以手動方式連線到每個叢集節點，然後使用下列命令重新安裝正確的儲存體用戶端版本︰</span><span class="sxs-lookup"><span data-stu-id="5a80f-453">__Resolution__: To resolve this error, manually connect to each cluster node using `ssh` and use the following command to reinstall the correct storage client version:</span></span>

```
sudo pip install azure-storage==0.20.0
```

<span data-ttu-id="5a80f-454">如需使用 SSH 連線到叢集的相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="5a80f-454">For information on connecting to the cluster with SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a><span data-ttu-id="5a80f-455">歷程記錄不會顯示在叢集建立期間使用的指令碼</span><span class="sxs-lookup"><span data-stu-id="5a80f-455">History doesn't show scripts used during cluster creation</span></span>

<span data-ttu-id="5a80f-456">如果您在 2016 年 3 月 15 日之前建立叢集，您可能不會在動作歷程記錄中看到任何項目。</span><span class="sxs-lookup"><span data-stu-id="5a80f-456">If your cluster was created before March 15, 2016, you may not see an entry in Script Action history.</span></span> <span data-ttu-id="5a80f-457">如果您在 2016 年 3 月 15 日之後調整該叢集大小，在叢集建立期間使用的指令碼會出現在歷程記錄中，因為這些指令碼在調整大小作業過程中會套用到叢集中的新節點。</span><span class="sxs-lookup"><span data-stu-id="5a80f-457">If you resize the cluster after March 15, 2016, the scripts using during cluster creation appear in history as they are applied to new nodes in the cluster as part of the resize operation.</span></span>

<span data-ttu-id="5a80f-458">有兩種例外狀況：</span><span class="sxs-lookup"><span data-stu-id="5a80f-458">There are two exceptions:</span></span>

* <span data-ttu-id="5a80f-459">如果您的叢集在 2015 年 9 月 1 日之前建立。</span><span class="sxs-lookup"><span data-stu-id="5a80f-459">If your cluster was created before September 1, 2015.</span></span> <span data-ttu-id="5a80f-460">此日期是引進指令碼動作的日期。</span><span class="sxs-lookup"><span data-stu-id="5a80f-460">This date is when Script Actions were introduced.</span></span> <span data-ttu-id="5a80f-461">在此日期之前建立的任何叢集可能都未使用指令碼動作建立叢集。</span><span class="sxs-lookup"><span data-stu-id="5a80f-461">Any cluster created before this date could not have used Script Actions for cluster creation.</span></span>

* <span data-ttu-id="5a80f-462">如果您在叢集建立期間使用了多個指令碼動作，並將相同的名稱、相同的 URI 使用於多個指令碼，但將不同的參數使用於多個指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a80f-462">If you used multiple Script Actions during cluster creation, and used the same name for multiple scripts, or the same name, same URI, but different parameters for multiple scripts.</span></span> <span data-ttu-id="5a80f-463">在這些情況下，您會收到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="5a80f-463">In these cases, you receive the following error:</span></span>

    <span data-ttu-id="5a80f-464">由於現有指令碼的指令碼名稱發生衝突，所以無法在此叢集上執行任何新的指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="5a80f-464">No new script actions can be ran on this cluster due to conflicting script names in existing scripts.</span></span> <span data-ttu-id="5a80f-465">建立叢集時所提供的指令碼名稱全都必須是唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="5a80f-465">Script names provided at cluster create must be all unique.</span></span> <span data-ttu-id="5a80f-466">既有的指令碼會在調整大小時執行。</span><span class="sxs-lookup"><span data-stu-id="5a80f-466">Existing scripts are ran on resize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a80f-467">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a80f-467">Next steps</span></span>

* [<span data-ttu-id="5a80f-468">開發 HDInsight 的指令碼動作指令碼</span><span class="sxs-lookup"><span data-stu-id="5a80f-468">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions-linux.md)
* [<span data-ttu-id="5a80f-469">在 HDInsight 叢集上安裝及使用 Solr</span><span class="sxs-lookup"><span data-stu-id="5a80f-469">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="5a80f-470">在 HDInsight 叢集上安裝及使用 Giraph</span><span class="sxs-lookup"><span data-stu-id="5a80f-470">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="5a80f-471">在 HDInsight 叢集新增儲存體</span><span class="sxs-lookup"><span data-stu-id="5a80f-471">Add additional storage to an HDInsight cluster</span></span>](hdinsight-hadoop-add-storage.md)

<span data-ttu-id="5a80f-472">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "叢集建立期間的階段"</span><span class="sxs-lookup"><span data-stu-id="5a80f-472">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Stages during cluster creation"</span></span>
