---
title: "使用指令碼動作-Azure aaaCustomize HDInsight 叢集 |Microsoft 文件"
description: "新增自訂元件，使用指令碼動作 tooLinux 為基礎的 HDInsight 叢集。 指令碼動作是 Bash 指令碼可使用的 toocustomize hello 叢集組態或新增其他服務和公用程式，例如色調、 Solr 或。"
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
ms.openlocfilehash: ff22680a8a50b21985f6941f1edaf1dcf863d13f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="f3833-104">使用指令碼動作自訂 Linux 型 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="f3833-104">Customize Linux-based HDInsight clusters using Script Action</span></span>

<span data-ttu-id="f3833-105">HDInsight 提供設定選項，呼叫**指令碼動作**自訂 hello 叢集中的自訂指令碼會叫用。</span><span class="sxs-lookup"><span data-stu-id="f3833-105">HDInsight provides a configuration option called **Script Action** that invokes custom scripts that customize hello cluster.</span></span> <span data-ttu-id="f3833-106">這些指令碼會使用的 tooinstall 其他元件和變更組態設定。</span><span class="sxs-lookup"><span data-stu-id="f3833-106">These scripts are used tooinstall additional components and change configuration settings.</span></span> <span data-ttu-id="f3833-107">叢集建立期間或叢集建立之後，可以使用指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="f3833-107">Script actions can be used during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f3833-108">hello 能力 toouse 正在執行的叢集上的指令碼動作只適用於以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f3833-108">hello ability toouse script actions on an already running cluster is only available for Linux-based HDInsight clusters.</span></span>
>
> <span data-ttu-id="f3833-109">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="f3833-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f3833-110">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="f3833-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="f3833-111">指令碼動作也可以為 HDInsight 應用程式是已發行的 toohello Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="f3833-111">Script actions can also be published toohello Azure Marketplace as an HDInsight application.</span></span> <span data-ttu-id="f3833-112">有些這份文件中的 hello 範例顯示如何安裝使用指令碼動作命令，從 PowerShell 和.NET SDK hello 的 HDInsight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3833-112">Some of hello examples in this document show how you can install an HDInsight application using script action commands from PowerShell and hello .NET SDK.</span></span> <span data-ttu-id="f3833-113">如需 HDInsight 應用程式的詳細資訊，請參閱[hello Azure Marketplace 應用程式發行 HDInsight](hdinsight-apps-publish-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="f3833-113">For more information on HDInsight applications, see [Publish HDInsight applications into hello Azure Marketplace](hdinsight-apps-publish-applications.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="f3833-114">權限</span><span class="sxs-lookup"><span data-stu-id="f3833-114">Permissions</span></span>

<span data-ttu-id="f3833-115">如果您使用已加入網域的 HDInsight 叢集，有兩個使用指令碼動作與 hello 叢集時所需的 Ambari 權限：</span><span class="sxs-lookup"><span data-stu-id="f3833-115">If you are using a domain-joined HDInsight cluster, there are two Ambari permissions that are required when using script actions with hello cluster:</span></span>

* <span data-ttu-id="f3833-116">**AMBARI。執行\_自訂\_命令**: hello Ambari 系統管理員角色預設具有此權限。</span><span class="sxs-lookup"><span data-stu-id="f3833-116">**AMBARI.RUN\_CUSTOM\_COMMAND**: hello Ambari Administrator role has this permission by default.</span></span>
* <span data-ttu-id="f3833-117">**叢集。執行\_自訂\_命令**： 兩者 hello HDInsight 叢集系統管理員和 Ambari 管理員預設擁有此權限。</span><span class="sxs-lookup"><span data-stu-id="f3833-117">**CLUSTER.RUN\_CUSTOM\_COMMAND**: Both hello HDInsight Cluster Administrator and Ambari Administrator have this permission by default.</span></span>

<span data-ttu-id="f3833-118">如需使用已加入網域之 HDInsight 權限的詳細資訊，請參閱[管理已加入網域的 HDInsight 叢集](hdinsight-domain-joined-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="f3833-118">For more information on working with permissions with domain-joined HDInsight, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="f3833-119">存取控制</span><span class="sxs-lookup"><span data-stu-id="f3833-119">Access control</span></span>

<span data-ttu-id="f3833-120">如果您不是 hello 管理員/擁有者的 Azure 訂用帳戶，您的帳戶必須至少有**參與者**存取 toohello 資源群組含有 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f3833-120">If you are not hello administrator/owner of your Azure subscription, your account must have at least **Contributor** access toohello resource group that contains hello HDInsight cluster.</span></span>

<span data-ttu-id="f3833-121">此外，如果您建立的 HDInsight 叢集，具備至少**參與者**存取 toohello Azure 訂用帳戶必須先前已登錄 hello HDInsight 的提供者。</span><span class="sxs-lookup"><span data-stu-id="f3833-121">Additionally, if you are creating an HDInsight cluster, someone with at least **Contributor** access toohello Azure subscription must have previously registered hello provider for HDInsight.</span></span> <span data-ttu-id="f3833-122">提供者註冊會在使用者與參與者存取 toohello 訂用帳戶建立時的資源，hello 第一次 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3833-122">Provider registration happens when a user with Contributor access toohello subscription creates a resource for hello first time on hello subscription.</span></span> <span data-ttu-id="f3833-123">透過[使用 REST 註冊提供者](https://msdn.microsoft.com/library/azure/dn790548.aspx)，也可以不需要建立資源就完成註冊作業。</span><span class="sxs-lookup"><span data-stu-id="f3833-123">It can also be accomplished without creating a resource by [registering a provider using REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span></span>

<span data-ttu-id="f3833-124">如需有關使用存取管理的詳細資訊，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="f3833-124">For more information on working with access management, see hello following documents:</span></span>

* [<span data-ttu-id="f3833-125">開始使用 hello Azure 入口網站中存取管理</span><span class="sxs-lookup"><span data-stu-id="f3833-125">Get started with access management in hello Azure portal</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="f3833-126">使用角色指派 toomanage 存取 tooyour Azure 訂用帳戶資源</span><span class="sxs-lookup"><span data-stu-id="f3833-126">Use role assignments toomanage access tooyour Azure subscription resources</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a><span data-ttu-id="f3833-127">了解指令碼動作</span><span class="sxs-lookup"><span data-stu-id="f3833-127">Understanding Script Actions</span></span>

<span data-ttu-id="f3833-128">指令碼動作只是一個您會提供 URI 和參數的 Bash 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-128">A Script Action is simply a Bash script that you provide a URI to, and parameters for.</span></span> <span data-ttu-id="f3833-129">在 hello HDInsight 叢集節點上執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-129">hello script runs on nodes in hello HDInsight cluster.</span></span> <span data-ttu-id="f3833-130">hello 以下是特性與功能的指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="f3833-130">hello following are characteristics and features of script actions.</span></span>

* <span data-ttu-id="f3833-131">必須儲存在可從 hello HDInsight 叢集存取的 URI。</span><span class="sxs-lookup"><span data-stu-id="f3833-131">Must be stored on a URI that is accessible from hello HDInsight cluster.</span></span> <span data-ttu-id="f3833-132">hello 以下是可能的儲存體位置：</span><span class="sxs-lookup"><span data-stu-id="f3833-132">hello following are possible storage locations:</span></span>

    * <span data-ttu-id="f3833-133">**Azure Data Lake Store** hello HDInsight 叢集可以存取的帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3833-133">An **Azure Data Lake Store** account that is accessible by hello HDInsight cluster.</span></span> <span data-ttu-id="f3833-134">如需使用 Azure Data Lake Store 與 HDInsight 的相關資訊，請參閱[建立使用 Data Lake Store 的 HDInsight 叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="f3833-134">For information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

        <span data-ttu-id="f3833-135">使用儲存在資料湖存放區中的指令碼，hello URI 格式時`adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`。</span><span class="sxs-lookup"><span data-stu-id="f3833-135">When using a script stored in Data Lake Store, hello URI format is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span></span>

        > [!NOTE]
        > <span data-ttu-id="f3833-136">hello 服務主體 HDInsight 使用 tooaccess 資料湖存放區必須有讀取權限 toohello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-136">hello service principal HDInsight uses tooaccess Data Lake Store must have read access toohello script.</span></span>

    * <span data-ttu-id="f3833-137">中的 blob **Azure 儲存體帳戶**也就是說 hello HDInsight 叢集的任一個 hello 主要或其他儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3833-137">A blob in an **Azure Storage account** that is either hello primary or additional storage account for hello HDInsight cluster.</span></span> <span data-ttu-id="f3833-138">HDInsight 是在叢集建立期間，授與存取 tooboth 這些類型的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3833-138">HDInsight is granted access tooboth of these types of storage accounts during cluster creation.</span></span>

    * <span data-ttu-id="f3833-139">公用檔案共用服務，例如 Azure Blob、GitHub、OneDrive、Dropbox 等。</span><span class="sxs-lookup"><span data-stu-id="f3833-139">A public file sharing service such as Azure Blob, GitHub, OneDrive, Dropbox, etc.</span></span>

        <span data-ttu-id="f3833-140">Uri，例如看到 hello[範例指令碼動作的指令碼](#example-script-action-scripts)> 一節。</span><span class="sxs-lookup"><span data-stu-id="f3833-140">For example URIs, see hello [Example script action scripts](#example-script-action-scripts) section.</span></span>

        > [!WARNING]
        > <span data-ttu-id="f3833-141">HDInsight 僅支援__一般用途__的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3833-141">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="f3833-142">它目前不支援 hello __Blob 儲存體__帳戶類型。</span><span class="sxs-lookup"><span data-stu-id="f3833-142">It does not currently support hello __Blob storage__ account type.</span></span>

* <span data-ttu-id="f3833-143">也可以限制太**只有特定節點型別上執行**，範例前端節點或背景工作節點。</span><span class="sxs-lookup"><span data-stu-id="f3833-143">Can be restricted too**run on only certain node types**, for example head nodes or worker nodes.</span></span>

  > [!NOTE]
  > <span data-ttu-id="f3833-144">HDInsight Premium 搭配使用時，您可以指定應透過 hello 邊緣節點上 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-144">When used with HDInsight Premium, you can specify that hello script should be used on hello edge node.</span></span>

* <span data-ttu-id="f3833-145">可以是**持續性**或**臨時性**。</span><span class="sxs-lookup"><span data-stu-id="f3833-145">Can be **persisted** or **ad hoc**.</span></span>

    <span data-ttu-id="f3833-146">**保存**hello 指令碼執行後指令碼都是套用的 tooworker 節點加入的 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="f3833-146">**Persisted** scripts are applied tooworker nodes added toohello cluster after hello script runs.</span></span> <span data-ttu-id="f3833-147">例如，當向上擴充 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="f3833-147">For example, when scaling up hello cluster.</span></span>

    <span data-ttu-id="f3833-148">保存的指令碼也可能會套用變更 tooanother 節點類型，例如前端節點。</span><span class="sxs-lookup"><span data-stu-id="f3833-148">A persisted script might also apply changes tooanother node type, such as a head node.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="f3833-149">持續性指令碼動作必須有唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="f3833-149">Persisted script actions must have a unique name.</span></span>

    <span data-ttu-id="f3833-150">**臨時性**指令碼不會持續留存。</span><span class="sxs-lookup"><span data-stu-id="f3833-150">**Ad hoc** scripts are not persisted.</span></span> <span data-ttu-id="f3833-151">它們不是套用的 tooworker 節點加入的 toohello 叢集之後 hello 指令碼已執行。</span><span class="sxs-lookup"><span data-stu-id="f3833-151">They are not applied tooworker nodes added toohello cluster after hello script has ran.</span></span> <span data-ttu-id="f3833-152">您可以接著升級臨機操作指令碼 tooa 保存指令碼，或降級保存的指令碼 tooan 臨機操作指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-152">You can subsequently promote an ad hoc script tooa persisted script, or demote a persisted script tooan ad hoc script.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="f3833-153">建立叢集期間使用的指令碼動作會自動保存下來。</span><span class="sxs-lookup"><span data-stu-id="f3833-153">Script actions used during cluster creation are automatically persisted.</span></span>
  >
  > <span data-ttu-id="f3833-154">即使您特別指出應予保存，仍然不會保存失敗的指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-154">Scripts that fail are not persisted, even if you specifically indicate that they should be.</span></span>

* <span data-ttu-id="f3833-155">可以接受**參數**所使用的 hello 指令碼執行期間。</span><span class="sxs-lookup"><span data-stu-id="f3833-155">Can accept **parameters** that are used by hello script during execution.</span></span>
* <span data-ttu-id="f3833-156">使用執行**根層級權限**hello 叢集節點上。</span><span class="sxs-lookup"><span data-stu-id="f3833-156">Run with **root level privileges** on hello cluster nodes.</span></span>
* <span data-ttu-id="f3833-157">可以用於透過 hello **Azure 入口網站**， **Azure PowerShell**， **Azure CLI**，或**HDInsight.NET SDK**</span><span class="sxs-lookup"><span data-stu-id="f3833-157">Can be used through hello **Azure portal**, **Azure PowerShell**, **Azure CLI**, or **HDInsight .NET SDK**</span></span>

<span data-ttu-id="f3833-158">hello 叢集會保留所有已執行的指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-158">hello cluster keeps a history of all scripts that have been ran.</span></span> <span data-ttu-id="f3833-159">hello 歷程記錄時，您需要升級或降級作業的指令碼的 toofind hello 識別碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-159">hello history is useful when you need toofind hello ID of a script for promotion or demotion operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f3833-160">沒有任何自動的方式 tooundo hello 指令碼動作所做的變更。</span><span class="sxs-lookup"><span data-stu-id="f3833-160">There is no automatic way tooundo hello changes made by a script action.</span></span> <span data-ttu-id="f3833-161">請手動反轉 hello 變更，或提供的指令碼，將其序列反轉。</span><span class="sxs-lookup"><span data-stu-id="f3833-161">Either manually reverse hello changes or provide a script that reverses them.</span></span>


### <a name="script-action-in-hello-cluster-creation-process"></a><span data-ttu-id="f3833-162">Hello 叢集建立程序中的指令碼動作</span><span class="sxs-lookup"><span data-stu-id="f3833-162">Script Action in hello cluster creation process</span></span>

<span data-ttu-id="f3833-163">在叢集建立期間使用的指令碼動作與在現有叢集上執行的指令碼動作稍微不同︰</span><span class="sxs-lookup"><span data-stu-id="f3833-163">Script Actions used during cluster creation are slightly different from script actions ran on an existing cluster:</span></span>

* <span data-ttu-id="f3833-164">hello 指令碼是**自動保存**。</span><span class="sxs-lookup"><span data-stu-id="f3833-164">hello script is **automatically persisted**.</span></span>
* <span data-ttu-id="f3833-165">A**失敗**hello 在指令碼可能會導致 hello 叢集建立程序 toofail。</span><span class="sxs-lookup"><span data-stu-id="f3833-165">A **failure** in hello script can cause hello cluster creation process toofail.</span></span>

<span data-ttu-id="f3833-166">hello 下列圖表說明 hello 建立程序期間執行指令碼動作時：</span><span class="sxs-lookup"><span data-stu-id="f3833-166">hello following diagram illustrates when Script Action is executed during hello creation process:</span></span>

<span data-ttu-id="f3833-167">![HDInsight 叢集自訂和叢集建立期間的階段][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="f3833-167">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="f3833-168">正在設定 HDInsight 時，就會執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-168">hello script runs while HDInsight is being configured.</span></span> <span data-ttu-id="f3833-169">在這個階段，hello 指令碼會以平行方式在所有 hello hello 叢集和 hello 節點上執行的根權限與指定的節點。</span><span class="sxs-lookup"><span data-stu-id="f3833-169">At this stage, hello script runs in parallel on all hello specified nodes in hello cluster, and runs with root privileges on hello nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="f3833-170">因為 hello 指令碼是 hello 叢集節點上執行的根層級權限，您可以執行作業，例如停止和啟動服務，包括 Hadoop 相關服務。</span><span class="sxs-lookup"><span data-stu-id="f3833-170">Because hello script runs with root level privilege on hello cluster nodes, you can perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="f3833-171">如果您停止服務，您必須確定確認 hello Ambari 服務與其他相關的 Hadoop 服務已啟動並執行 hello 指令碼完成執行之前完成。</span><span class="sxs-lookup"><span data-stu-id="f3833-171">If you stop services, you must ensure that hello Ambari service and other Hadoop-related services are up and running before hello script finishes running.</span></span> <span data-ttu-id="f3833-172">這些服務所需 toosuccessfully 判斷 hello 健全狀況和狀態的 hello 叢集在建立時。</span><span class="sxs-lookup"><span data-stu-id="f3833-172">These services are required toosuccessfully determine hello health and state of hello cluster while it is being created.</span></span>


<span data-ttu-id="f3833-173">在叢集建立期間，您可以同時使用多個指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="f3833-173">During cluster creation, you can use multiple script actions at once.</span></span> <span data-ttu-id="f3833-174">這些指令碼會叫用 hello 所指定的順序。</span><span class="sxs-lookup"><span data-stu-id="f3833-174">These scripts are invoked in hello order in which they were specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f3833-175">指令碼動作必須在 60 分鐘內完成，否則就會逾時。</span><span class="sxs-lookup"><span data-stu-id="f3833-175">Script actions must complete within 60 minutes, or timeout.</span></span> <span data-ttu-id="f3833-176">在叢集佈建，hello 指令碼會執行與其他安裝及設定處理程序。</span><span class="sxs-lookup"><span data-stu-id="f3833-176">During cluster provisioning, hello script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="f3833-177">競爭資源，例如 CPU 時間和網路頻寬可能會導致 hello 指令碼 tootake 長 toofinish 不同於您的開發環境。</span><span class="sxs-lookup"><span data-stu-id="f3833-177">Competition for resources such as CPU time or network bandwidth may cause hello script tootake longer toofinish than it does in your development environment.</span></span>
>
> <span data-ttu-id="f3833-178">toominimize hello 次採用 toorun hello 指令碼，例如下載及編譯來源的應用程式的工作。</span><span class="sxs-lookup"><span data-stu-id="f3833-178">toominimize hello time it takes toorun hello script, avoid tasks such as downloading and compiling applications from source.</span></span> <span data-ttu-id="f3833-179">先行編譯應用程式，並儲存在 Azure 儲存體中的 hello 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="f3833-179">Pre-compile applications and store hello binary in Azure Storage.</span></span>


### <a name="script-action-on-a-running-cluster"></a><span data-ttu-id="f3833-180">執行中叢集上的指令碼動作</span><span class="sxs-lookup"><span data-stu-id="f3833-180">Script action on a running cluster</span></span>

<span data-ttu-id="f3833-181">不同於正在執行的叢集執行的叢集建立期間，指令碼中的失敗動作的指令碼並不會自動導致 hello 叢集 toochange tooa 失敗狀態。</span><span class="sxs-lookup"><span data-stu-id="f3833-181">Unlike script actions used during cluster creation, a failure in a script ran on an already running cluster does not automatically cause hello cluster toochange tooa failed state.</span></span> <span data-ttu-id="f3833-182">指令碼完成之後，hello 叢集應該會傳回 tooa 「 執行 」 狀態。</span><span class="sxs-lookup"><span data-stu-id="f3833-182">Once a script completes, hello cluster should return tooa "running" state.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f3833-183">即使 hello 叢集的 「 執行中 」 狀態，hello 失敗的指令碼可能會有中斷作業。</span><span class="sxs-lookup"><span data-stu-id="f3833-183">Even if hello cluster has a 'running' state, hello failed script may have broken things.</span></span> <span data-ttu-id="f3833-184">例如，指令碼無法刪除 hello 叢集所需的檔案。</span><span class="sxs-lookup"><span data-stu-id="f3833-184">For example, a script could delete files needed by hello cluster.</span></span>
>
> <span data-ttu-id="f3833-185">根權限，因此您應該確定您了解指令碼會執行之後才套用 tooyour 叢集執行指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="f3833-185">Scripts actions run with root privileges, so you should make sure that you understand what a script does before applying it tooyour cluster.</span></span>

<span data-ttu-id="f3833-186">當套用指令碼 tooa 叢集，hello 叢集狀態變更 toofrom**執行**太**接受**，然後**HDInsight 組態**，以及最後回太**執行**成功的指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-186">When applying a script tooa cluster, hello cluster state changes toofrom **Running** too**Accepted**, then **HDInsight configuration**, and finally back too**Running** for successful scripts.</span></span> <span data-ttu-id="f3833-187">hello 指令碼狀態來登入 hello 指令碼動作記錄，而且您可以使用此資訊 toodetermine hello 指令碼成功或失敗。</span><span class="sxs-lookup"><span data-stu-id="f3833-187">hello script status is logged in hello script action history, and you can use this information toodetermine whether hello script succeeded or failed.</span></span> <span data-ttu-id="f3833-188">例如，hello `Get-AzureRmHDInsightScriptActionHistory` PowerShell 指令程式可以使用的 tooview hello 狀態的指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-188">For example, hello `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet can be used tooview hello status of a script.</span></span> <span data-ttu-id="f3833-189">它會傳回資訊的類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="f3833-189">It returns information similar toohello following text:</span></span>

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> <span data-ttu-id="f3833-190">如果您變更 hello 叢集使用者 (admin) 密碼建立 hello 叢集之後，動作執行對此叢集的指令碼可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="f3833-190">If you have changed hello cluster user (admin) password after hello cluster was created, script actions ran against this cluster may fail.</span></span> <span data-ttu-id="f3833-191">如果您有任何保存的指令碼動作的目標背景工作節點，這些指令碼可能會失敗，當您擴充 hello 叢集時。</span><span class="sxs-lookup"><span data-stu-id="f3833-191">If you have any persisted script actions that target worker nodes, these scripts may fail when you scale hello cluster.</span></span>

## <a name="example-script-action-scripts"></a><span data-ttu-id="f3833-192">範例指令碼動作指令碼</span><span class="sxs-lookup"><span data-stu-id="f3833-192">Example Script Action scripts</span></span>

<span data-ttu-id="f3833-193">指令碼動作的指令碼可以用於透過下列公用程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="f3833-193">Script Action scripts can be used through hello following utilities:</span></span>

* <span data-ttu-id="f3833-194">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f3833-194">Azure portal</span></span>
* <span data-ttu-id="f3833-195">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3833-195">Azure PowerShell</span></span>
* <span data-ttu-id="f3833-196">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f3833-196">Azure CLI</span></span>
* <span data-ttu-id="f3833-197">HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="f3833-197">HDInsight .NET SDK</span></span>

<span data-ttu-id="f3833-198">HDInsight 提供下列元件在 HDInsight 叢集上的指令碼 tooinstall hello:</span><span class="sxs-lookup"><span data-stu-id="f3833-198">HDInsight provides scripts tooinstall hello following components on HDInsight clusters:</span></span>

| <span data-ttu-id="f3833-199">名稱</span><span class="sxs-lookup"><span data-stu-id="f3833-199">Name</span></span> | <span data-ttu-id="f3833-200">指令碼</span><span class="sxs-lookup"><span data-stu-id="f3833-200">Script</span></span> |
| --- | --- |
| <span data-ttu-id="f3833-201">**新增 Azure 儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="f3833-201">**Add an Azure Storage account**</span></span> |<span data-ttu-id="f3833-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh。請參閱[新增額外的儲存體 tooan HDInsight 叢集](hdinsight-hadoop-add-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="f3833-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. See [Add additional storage tooan HDInsight cluster](hdinsight-hadoop-add-storage.md).</span></span> |
| <span data-ttu-id="f3833-203">**安裝色調**</span><span class="sxs-lookup"><span data-stu-id="f3833-203">**Install Hue**</span></span> |<span data-ttu-id="f3833-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh。請參閱 [在 HDInsight 叢集上安裝及使用色調](hdinsight-hadoop-hue-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="f3833-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. See [Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> |
| <span data-ttu-id="f3833-205">**安裝 Presto**</span><span class="sxs-lookup"><span data-stu-id="f3833-205">**Install Presto**</span></span> |<span data-ttu-id="f3833-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh。請參閱[在 HDInsight 叢集上安裝和使用 Presto](hdinsight-hadoop-install-presto.md)。</span><span class="sxs-lookup"><span data-stu-id="f3833-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. See [Install and use Presto on HDInsight clusters](hdinsight-hadoop-install-presto.md).</span></span> |
| <span data-ttu-id="f3833-207">**安裝 Solr**</span><span class="sxs-lookup"><span data-stu-id="f3833-207">**Install Solr**</span></span> |<span data-ttu-id="f3833-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh。請參閱 [在 HDInsight 叢集上安裝及使用 Solr](hdinsight-hadoop-solr-install-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="f3833-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> |
| <span data-ttu-id="f3833-209">**安裝 Giraph**</span><span class="sxs-lookup"><span data-stu-id="f3833-209">**Install Giraph**</span></span> |<span data-ttu-id="f3833-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh。請參閱 [在 HDInsight 叢集上安裝及使用 Giraph](hdinsight-hadoop-giraph-install-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="f3833-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> |
| <span data-ttu-id="f3833-211">**預先載入 Hive 程式庫**</span><span class="sxs-lookup"><span data-stu-id="f3833-211">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="f3833-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh。請參閱 [在 HDInsight 叢集上新增 Hive 程式庫](hdinsight-hadoop-add-hive-libraries.md)。</span><span class="sxs-lookup"><span data-stu-id="f3833-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md).</span></span> |
| <span data-ttu-id="f3833-213">**安裝或更新 Mono**</span><span class="sxs-lookup"><span data-stu-id="f3833-213">**Install or update Mono**</span></span> | <span data-ttu-id="f3833-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash。</span><span class="sxs-lookup"><span data-stu-id="f3833-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span></span> <span data-ttu-id="f3833-215">請參閱[在 HDInsight 上安裝或更新 Mono](hdinsight-hadoop-install-mono.md)。</span><span class="sxs-lookup"><span data-stu-id="f3833-215">See [Install or update Mono on HDInsight](hdinsight-hadoop-install-mono.md).</span></span> |

## <a name="use-a-script-action-during-cluster-creation"></a><span data-ttu-id="f3833-216">在建立叢集期間使用指令碼動作</span><span class="sxs-lookup"><span data-stu-id="f3833-216">Use a Script Action during cluster creation</span></span>

<span data-ttu-id="f3833-217">本節提供範例 hello 不同的方式，建立的 HDInsight 叢集時，您可以使用指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="f3833-217">This section provides examples on hello different ways you can use script actions when creating an HDInsight cluster.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-hello-azure-portal"></a><span data-ttu-id="f3833-218">使用指令碼動作在叢集建立 hello Azure 入口網站的期間</span><span class="sxs-lookup"><span data-stu-id="f3833-218">Use a Script Action during cluster creation from hello Azure portal</span></span>

1. <span data-ttu-id="f3833-219">依[在 HDInsight 建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)中的描述開始建立叢集。</span><span class="sxs-lookup"><span data-stu-id="f3833-219">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="f3833-220">在到達 hello 時停止__叢集摘要__> 一節。</span><span class="sxs-lookup"><span data-stu-id="f3833-220">Stop when you reach hello __Cluster summary__ section.</span></span>

2. <span data-ttu-id="f3833-221">從 hello__叢集摘要__區段中，選取 hello__編輯__連結__進階設定__。</span><span class="sxs-lookup"><span data-stu-id="f3833-221">From hello __Cluster summary__ section, select hello __edit__ link for __Advanced settings__.</span></span>

    ![[Advanced settings] \(進階設定\) 連結](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. <span data-ttu-id="f3833-223">從 hello__進階設定__區段中，選取__編寫指令碼動作__。</span><span class="sxs-lookup"><span data-stu-id="f3833-223">From hello __Advanced settings__ section, select __Script actions__.</span></span> <span data-ttu-id="f3833-224">從 hello__編寫指令碼動作__區段中，選取__+ 新送出__</span><span class="sxs-lookup"><span data-stu-id="f3833-224">From hello __Script actions__ section, select __+ Submit new__</span></span>

    ![送出新的指令碼動作](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. <span data-ttu-id="f3833-226">使用 hello__選取指令碼__項目 tooselect 預先製作的指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-226">Use hello __Select a script__ entry tooselect a pre-made script.</span></span> <span data-ttu-id="f3833-227">toouse 自訂指令碼中，選取__自訂__，然後提供 hello__名稱__和__撞指令碼 URI__指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-227">toouse a custom script, select __Custom__ and then provide hello __Name__ and __Bash script URI__ for your script.</span></span>

    ![Hello 選取指令碼表單中加入指令碼](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="f3833-229">hello 下表描述 hello 表單上的 hello 元素：</span><span class="sxs-lookup"><span data-stu-id="f3833-229">hello following table describes hello elements on hello form:</span></span>

    | <span data-ttu-id="f3833-230">屬性</span><span class="sxs-lookup"><span data-stu-id="f3833-230">Property</span></span> | <span data-ttu-id="f3833-231">值</span><span class="sxs-lookup"><span data-stu-id="f3833-231">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="f3833-232">選取指令碼</span><span class="sxs-lookup"><span data-stu-id="f3833-232">Select a script</span></span> | <span data-ttu-id="f3833-233">toouse 自己的指令碼，選取__自訂__。</span><span class="sxs-lookup"><span data-stu-id="f3833-233">toouse your own script, select __Custom__.</span></span> <span data-ttu-id="f3833-234">否則，請選取其中一個提供的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-234">Otherwise, select one of hello provided scripts.</span></span> |
    | <span data-ttu-id="f3833-235">名稱</span><span class="sxs-lookup"><span data-stu-id="f3833-235">Name</span></span> |<span data-ttu-id="f3833-236">指定 hello 指令碼動作的名稱。</span><span class="sxs-lookup"><span data-stu-id="f3833-236">Specify a name for hello script action.</span></span> |
    | <span data-ttu-id="f3833-237">Bash 指令碼 URI</span><span class="sxs-lookup"><span data-stu-id="f3833-237">Bash script URI</span></span> |<span data-ttu-id="f3833-238">指定 hello URI toohello 指令碼會叫用的 toocustomize hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="f3833-238">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> |
    | <span data-ttu-id="f3833-239">Head/Worker/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="f3833-239">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="f3833-240">指定 hello 節點 (**Head**，**工作者**，或**動物園管理員**) 執行哪些 hello 自訂指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-240">Specify hello nodes (**Head**, **Worker**, or **ZooKeeper**) on which hello customization script is run.</span></span> |
    | <span data-ttu-id="f3833-241">參數</span><span class="sxs-lookup"><span data-stu-id="f3833-241">Parameters</span></span> |<span data-ttu-id="f3833-242">指定 hello 參數，如果 hello 指令碼所需。</span><span class="sxs-lookup"><span data-stu-id="f3833-242">Specify hello parameters, if required by hello script.</span></span> |

    <span data-ttu-id="f3833-243">使用 hello__保存此指令碼動作__hello 指令碼的項目 tooensure 縮放作業期間套用。</span><span class="sxs-lookup"><span data-stu-id="f3833-243">Use hello __Persist this script action__ entry tooensure that hello script is applied during scaling operations.</span></span>

5. <span data-ttu-id="f3833-244">選取__建立__toosave hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-244">Select __Create__ toosave hello script.</span></span> <span data-ttu-id="f3833-245">然後您可以使用__+ 送出新__tooadd 另一個指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-245">You can then use __+ Submit new__ tooadd another script.</span></span>

    ![多個指令碼動作](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    <span data-ttu-id="f3833-247">當您完成新增指令碼時，使用 hello__選取__按鈕，然後再 hello__下一步__按鈕 tooreturn toohello__叢集摘要__> 一節。</span><span class="sxs-lookup"><span data-stu-id="f3833-247">When you are done adding scripts, use hello __Select__ button, and then hello __Next__ button tooreturn toohello __Cluster summary__ section.</span></span>

3. <span data-ttu-id="f3833-248">toocreate hello 叢集上，選取__建立__從 hello__叢集摘要__選取項目。</span><span class="sxs-lookup"><span data-stu-id="f3833-248">toocreate hello cluster, select __Create__ from hello __Cluster summary__ selection.</span></span>

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a><span data-ttu-id="f3833-249">從 Azure 資源管理員範本使用指令碼動作</span><span class="sxs-lookup"><span data-stu-id="f3833-249">Use a Script Action from Azure Resource Manager templates</span></span>

<span data-ttu-id="f3833-250">本節中的 hello 範例示範如何 toouse 指令碼動作的 Azure 資源管理員範本。</span><span class="sxs-lookup"><span data-stu-id="f3833-250">hello examples in this section demonstrate how toouse script actions with Azure Resource Manager templates.</span></span>

#### <a name="before-you-begin"></a><span data-ttu-id="f3833-251">開始之前</span><span class="sxs-lookup"><span data-stu-id="f3833-251">Before you begin</span></span>

* <span data-ttu-id="f3833-252">設定工作站 toorun HDInsight Powershell cmdlet 的相關資訊，請參閱[安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="f3833-252">For information about configuring a workstation toorun HDInsight Powershell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="f3833-253">如需有關指示 toocreate 範本，請參閱[撰寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="f3833-253">For instructions on how toocreate templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="f3833-254">如果您之前未曾搭配使用Azure PowerShell 與資源管理員，請參閱 [將 Azure PowerShell 與 Azure 資源管理員搭配使用](../azure-resource-manager/powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="f3833-254">If you have not previously used Azure PowerShell with Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

#### <a name="create-clusters-using-script-action"></a><span data-ttu-id="f3833-255">使用指令碼動作建立叢集</span><span class="sxs-lookup"><span data-stu-id="f3833-255">Create clusters using Script Action</span></span>

1. <span data-ttu-id="f3833-256">複製下列範本 tooa 位置在電腦上的 hello。</span><span class="sxs-lookup"><span data-stu-id="f3833-256">Copy hello following template tooa location on your computer.</span></span> <span data-ttu-id="f3833-257">此範本安裝 Giraph hello 叢集中的 hello headnodes 和背景工作節點上。</span><span class="sxs-lookup"><span data-stu-id="f3833-257">This template installs Giraph on hello headnodes and worker nodes in hello cluster.</span></span> <span data-ttu-id="f3833-258">您也可以確認 hello JSON 範本是否有效。</span><span class="sxs-lookup"><span data-stu-id="f3833-258">You can also verify if hello JSON template is valid.</span></span> <span data-ttu-id="f3833-259">將您的範本內容貼至 [JSONLint](http://jsonlint.com/)，這是一個線上 JSON 驗證器工具。</span><span class="sxs-lookup"><span data-stu-id="f3833-259">Paste your template content into [JSONLint](http://jsonlint.com/), an online JSON validation tool.</span></span>

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
2. <span data-ttu-id="f3833-260">啟動 Azure PowerShell，並登入 tooyour Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3833-260">Start Azure PowerShell and Log in tooyour Azure account.</span></span> <span data-ttu-id="f3833-261">提供您的認證之後，hello 命令會傳回您的帳戶相關的資訊。</span><span class="sxs-lookup"><span data-stu-id="f3833-261">After providing your credentials, hello command returns information about your account.</span></span>

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. <span data-ttu-id="f3833-262">如果您有多個訂用帳戶，提供 hello 訂用帳戶 ID 想 toouse 部署。</span><span class="sxs-lookup"><span data-stu-id="f3833-262">If you have multiple subscriptions, provide hello subscription ID you wish toouse for deployment.</span></span>

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > <span data-ttu-id="f3833-263">您可以使用`Get-AzureRmSubscription`tooget 與您的帳戶，其中包含針對每個 hello 訂用帳戶 ID 相關聯的所有訂閱的清單。</span><span class="sxs-lookup"><span data-stu-id="f3833-263">You can use `Get-AzureRmSubscription` tooget a list of all subscriptions associated with your account, which includes hello subscription ID for each one.</span></span>

4. <span data-ttu-id="f3833-264">如果您沒有現有資源群組，請建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f3833-264">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="f3833-265">提供 hello 名稱 hello 資源群組及您需要為您的方案的位置。</span><span class="sxs-lookup"><span data-stu-id="f3833-265">Provide hello name of hello resource group and location that you need for your solution.</span></span> <span data-ttu-id="f3833-266">會傳回 hello 新資源群組的摘要。</span><span class="sxs-lookup"><span data-stu-id="f3833-266">A summary of hello new resource group is returned.</span></span>

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

5. <span data-ttu-id="f3833-267">部署您的資源群組，執行 hello toocreate**新增 AzureRmResourceGroupDeployment**命令，並提供 hello 必要參數。</span><span class="sxs-lookup"><span data-stu-id="f3833-267">toocreate a deployment for your resource group, run hello **New-AzureRmResourceGroupDeployment** command and provide hello necessary parameters.</span></span> <span data-ttu-id="f3833-268">hello 參數包括下列資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="f3833-268">hello parameters include hello following data:</span></span>

    * <span data-ttu-id="f3833-269">部署的名稱</span><span class="sxs-lookup"><span data-stu-id="f3833-269">A name for your deployment</span></span>
    * <span data-ttu-id="f3833-270">hello 的資源群組的名稱</span><span class="sxs-lookup"><span data-stu-id="f3833-270">hello name of your resource group</span></span>
    * <span data-ttu-id="f3833-271">hello 路徑或 URL toohello 範本所建立。</span><span class="sxs-lookup"><span data-stu-id="f3833-271">hello path or URL toohello template you created.</span></span>

  <span data-ttu-id="f3833-272">如果您的範本需要任何參數，您也必須傳遞這些參數。</span><span class="sxs-lookup"><span data-stu-id="f3833-272">If your template requires any parameters, you must pass those parameters as well.</span></span> <span data-ttu-id="f3833-273">在此情況下，hello 指令碼動作 tooinstall R hello 叢集上的不需要任何參數。</span><span class="sxs-lookup"><span data-stu-id="f3833-273">In this case, hello script action tooinstall R on hello cluster does not require any parameters.</span></span>

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    <span data-ttu-id="f3833-274">您會提示的 tooprovide hello 範本中定義的 hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="f3833-274">You are prompted tooprovide values for hello parameters defined in hello template.</span></span>

1. <span data-ttu-id="f3833-275">當已部署 hello 資源群組時，則會顯示 hello 部署的摘要。</span><span class="sxs-lookup"><span data-stu-id="f3833-275">When hello resource group has been deployed, a summary of hello deployment is displayed.</span></span>

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. <span data-ttu-id="f3833-276">如果您的部署失敗，您可以使用下列 cmdlet tooget 資訊有關 hello 失敗 hello。</span><span class="sxs-lookup"><span data-stu-id="f3833-276">If your deployment fails, you can use hello following cmdlets tooget information about hello failures.</span></span>

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a><span data-ttu-id="f3833-277">在建立叢集期間從 Azure PowerShell 使用指令碼動作</span><span class="sxs-lookup"><span data-stu-id="f3833-277">Use a Script Action during cluster creation from Azure PowerShell</span></span>

<span data-ttu-id="f3833-278">在本節中，我們使用 hello[新增 AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx)使用指令碼動作 toocustomize 叢集 cmdlet tooinvoke 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-278">In this section, we use hello [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet tooinvoke scripts by using Script Action toocustomize a cluster.</span></span> <span data-ttu-id="f3833-279">在繼續之前，請確認您已安裝和設定 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f3833-279">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="f3833-280">設定工作站 toorun HDInsight PowerShell cmdlet 的相關資訊，請參閱[安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="f3833-280">For information about configuring a workstation toorun HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="f3833-281">hello 下列指令碼示範如何 tooapply script 動作時使用 PowerShell 建立叢集：</span><span class="sxs-lookup"><span data-stu-id="f3833-281">hello following script demonstrates how tooapply a script action when creating a cluster using PowerShell:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

<span data-ttu-id="f3833-282">可能需要幾分鐘後才建立 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="f3833-282">It can take several minutes before hello cluster is created.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-hello-hdinsight-net-sdk"></a><span data-ttu-id="f3833-283">使用指令碼動作在叢集建立時，從 hello HDInsight.NET SDK</span><span class="sxs-lookup"><span data-stu-id="f3833-283">Use a Script Action during cluster creation from hello HDInsight .NET SDK</span></span>

<span data-ttu-id="f3833-284">hello HDInsight.NET SDK 提供可讓您更輕鬆 toowork 與 HDInsight.NET 應用程式的用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="f3833-284">hello HDInsight .NET SDK provides client libraries that makes it easier toowork with HDInsight from a .NET application.</span></span> <span data-ttu-id="f3833-285">如需程式碼範例，請參閱[建立 linux 叢集使用 HDInsight 中的 hello.NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)。</span><span class="sxs-lookup"><span data-stu-id="f3833-285">For a code sample, see [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span></span>

## <a name="apply-a-script-action-tooa-running-cluster"></a><span data-ttu-id="f3833-286">適用於執行叢集的指令碼動作 tooa</span><span class="sxs-lookup"><span data-stu-id="f3833-286">Apply a Script Action tooa running cluster</span></span>

<span data-ttu-id="f3833-287">這一節，了解如何 tooapply 指令碼動作 tooa 執行叢集。</span><span class="sxs-lookup"><span data-stu-id="f3833-287">In this section, learn how tooapply script actions tooa running cluster.</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-portal"></a><span data-ttu-id="f3833-288">適用於執行叢集 hello Azure 入口網站從指令碼動作 tooa</span><span class="sxs-lookup"><span data-stu-id="f3833-288">Apply a Script Action tooa running cluster from hello Azure portal</span></span>

1. <span data-ttu-id="f3833-289">從 hello [Azure 入口網站](https://portal.azure.com)，選取您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f3833-289">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="f3833-290">從 hello HDInsight 叢集的概觀，請選取 hello**指令碼動作**磚。</span><span class="sxs-lookup"><span data-stu-id="f3833-290">From hello HDInsight cluster overview, select hello **Script Actions** tile.</span></span>

    ![指令碼動作磚](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="f3833-292">您也可以選取**所有設定**，然後選取 [**指令碼動作**從 hello 設定] 區段。</span><span class="sxs-lookup"><span data-stu-id="f3833-292">You can also select **All settings** and then select **Script Actions** from hello Settings section.</span></span>

3. <span data-ttu-id="f3833-293">從 hello hello 指令碼動作 區段頂端，選取**送出新**。</span><span class="sxs-lookup"><span data-stu-id="f3833-293">From hello top of hello Script Actions section, select **Submit new**.</span></span>

    ![新增指令碼 tooa 執行叢集](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. <span data-ttu-id="f3833-295">使用 hello__選取指令碼__項目 tooselect 預先製作的指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-295">Use hello __Select a script__ entry tooselect a pre-made script.</span></span> <span data-ttu-id="f3833-296">toouse 自訂指令碼中，選取__自訂__，然後提供 hello__名稱__和__撞指令碼 URI__指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-296">toouse a custom script, select __Custom__ and then provide hello __Name__ and __Bash script URI__ for your script.</span></span>

    ![Hello 選取指令碼表單中加入指令碼](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="f3833-298">hello 下表描述 hello 表單上的 hello 元素：</span><span class="sxs-lookup"><span data-stu-id="f3833-298">hello following table describes hello elements on hello form:</span></span>

    | <span data-ttu-id="f3833-299">屬性</span><span class="sxs-lookup"><span data-stu-id="f3833-299">Property</span></span> | <span data-ttu-id="f3833-300">值</span><span class="sxs-lookup"><span data-stu-id="f3833-300">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="f3833-301">選取指令碼</span><span class="sxs-lookup"><span data-stu-id="f3833-301">Select a script</span></span> | <span data-ttu-id="f3833-302">toouse 自己的指令碼，選取__自訂__。</span><span class="sxs-lookup"><span data-stu-id="f3833-302">toouse your own script, select __custom__.</span></span> <span data-ttu-id="f3833-303">否則，請選取提供的指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-303">Otherwise, select a provided script.</span></span> |
    | <span data-ttu-id="f3833-304">名稱</span><span class="sxs-lookup"><span data-stu-id="f3833-304">Name</span></span> |<span data-ttu-id="f3833-305">指定 hello 指令碼動作的名稱。</span><span class="sxs-lookup"><span data-stu-id="f3833-305">Specify a name for hello script action.</span></span> |
    | <span data-ttu-id="f3833-306">Bash 指令碼 URI</span><span class="sxs-lookup"><span data-stu-id="f3833-306">Bash script URI</span></span> |<span data-ttu-id="f3833-307">指定 hello URI toohello 指令碼會叫用的 toocustomize hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="f3833-307">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> |
    | <span data-ttu-id="f3833-308">Head/Worker/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="f3833-308">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="f3833-309">指定 hello 節點 (**Head**，**工作者**，或**動物園管理員**) 執行哪些 hello 自訂指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-309">Specify hello nodes (**Head**, **Worker**, or **ZooKeeper**) on which hello customization script is run.</span></span> |
    | <span data-ttu-id="f3833-310">參數</span><span class="sxs-lookup"><span data-stu-id="f3833-310">Parameters</span></span> |<span data-ttu-id="f3833-311">指定 hello 參數，如果 hello 指令碼所需。</span><span class="sxs-lookup"><span data-stu-id="f3833-311">Specify hello parameters, if required by hello script.</span></span> |

    <span data-ttu-id="f3833-312">使用 hello__保存此指令碼動作__縮放作業期間套用項目 toomake 確定 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-312">Use hello __Persist this script action__ entry toomake sure hello script is applied during scaling operations.</span></span>

5. <span data-ttu-id="f3833-313">最後，使用 hello**建立**按鈕 tooapply hello 指令碼 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="f3833-313">Finally, use hello **Create** button tooapply hello script toohello cluster.</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-azure-powershell"></a><span data-ttu-id="f3833-314">適用於執行叢集從 Azure PowerShell 指令碼動作 tooa</span><span class="sxs-lookup"><span data-stu-id="f3833-314">Apply a Script Action tooa running cluster from Azure PowerShell</span></span>

<span data-ttu-id="f3833-315">在繼續之前，請確認您已安裝和設定 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f3833-315">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="f3833-316">設定工作站 toorun HDInsight PowerShell cmdlet 的相關資訊，請參閱[安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="f3833-316">For information about configuring a workstation toorun HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="f3833-317">hello 下列範例會示範如何 tooapply 指令碼動作 tooa 執行叢集：</span><span class="sxs-lookup"><span data-stu-id="f3833-317">hello following example demonstrates how tooapply a script action tooa running cluster:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

<span data-ttu-id="f3833-318">Hello 作業完成之後，您會收到下列文字的資訊類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="f3833-318">Once hello operation completes, you receive information similar toohello following text:</span></span>

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-cli"></a><span data-ttu-id="f3833-319">適用於執行叢集 hello Azure CLI 從指令碼動作 tooa</span><span class="sxs-lookup"><span data-stu-id="f3833-319">Apply a Script Action tooa running cluster from hello Azure CLI</span></span>

<span data-ttu-id="f3833-320">繼續之前，請確定您已安裝並設定 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="f3833-320">Before proceeding, make sure you have installed and configured hello Azure CLI.</span></span> <span data-ttu-id="f3833-321">如需詳細資訊，請參閱[安裝 hello Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="f3833-321">For more information, see [Install hello Azure CLI](../cli-install-nodejs.md).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="f3833-322">tooswitch tooAzure Resource Manager 模式會使用下列命令在 hello 命令列的 hello:</span><span class="sxs-lookup"><span data-stu-id="f3833-322">tooswitch tooAzure Resource Manager mode, use hello following command at hello command line:</span></span>

        azure config mode arm

2. <span data-ttu-id="f3833-323">使用下列 tooauthenticate tooyour Azure 訂用帳戶的 hello。</span><span class="sxs-lookup"><span data-stu-id="f3833-323">Use hello following tooauthenticate tooyour Azure subscription.</span></span>

        azure login

3. <span data-ttu-id="f3833-324">使用下列命令 tooapply 執行叢集的指令碼動作 tooa hello</span><span class="sxs-lookup"><span data-stu-id="f3833-324">Use hello following command tooapply a script action tooa running cluster</span></span>

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    <span data-ttu-id="f3833-325">如果省略這個命令的參數，系統會提示您使用。</span><span class="sxs-lookup"><span data-stu-id="f3833-325">If you omit parameters for this command, you are prompted for them.</span></span> <span data-ttu-id="f3833-326">如果您使用指定的指令碼的 hello`-u`接受參數，您可以指定它們使用 hello`-p`參數。</span><span class="sxs-lookup"><span data-stu-id="f3833-326">If hello script you specify with `-u` accepts parameters, you can specify them using hello `-p` parameter.</span></span>

    <span data-ttu-id="f3833-327">有效的節點類型為 `headnode``workernode` 和 `zookeeper`。</span><span class="sxs-lookup"><span data-stu-id="f3833-327">Valid node types are `headnode`, `workernode`, and `zookeeper`.</span></span> <span data-ttu-id="f3833-328">如果 hello 指令碼應該套用的 toomultiple 節點型別，指定以分隔 hello 類型 ';'。</span><span class="sxs-lookup"><span data-stu-id="f3833-328">If hello script should be applied toomultiple node types, specify hello types separated by a ';'.</span></span> <span data-ttu-id="f3833-329">例如： `-n headnode;workernode`。</span><span class="sxs-lookup"><span data-stu-id="f3833-329">For example, `-n headnode;workernode`.</span></span>

    <span data-ttu-id="f3833-330">toopersist hello 指令碼中，加入 hello `--persistOnSuccess`。</span><span class="sxs-lookup"><span data-stu-id="f3833-330">toopersist hello script, add hello `--persistOnSuccess`.</span></span> <span data-ttu-id="f3833-331">您可以也保存 hello 指令碼稍後使用`azure hdinsight script-action persisted set`。</span><span class="sxs-lookup"><span data-stu-id="f3833-331">You can also persist hello script later by using `azure hdinsight script-action persisted set`.</span></span>

    <span data-ttu-id="f3833-332">一旦 hello 作業完成時，您會收到下列文字的輸出類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="f3833-332">Once hello job completes, you receive output similar toohello following text:</span></span>

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-tooa-running-cluster-using-rest-api"></a><span data-ttu-id="f3833-333">適用於執行叢集使用 REST API 的指令碼動作 tooa</span><span class="sxs-lookup"><span data-stu-id="f3833-333">Apply a Script Action tooa running cluster using REST API</span></span>

<span data-ttu-id="f3833-334">請參閱 [在執行中的叢集執行指令碼動作](https://msdn.microsoft.com/library/azure/mt668441.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f3833-334">See [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-hdinsight-net-sdk"></a><span data-ttu-id="f3833-335">適用於從 hello HDInsight.NET SDK 執行叢集的指令碼動作 tooa</span><span class="sxs-lookup"><span data-stu-id="f3833-335">Apply a Script Action tooa running cluster from hello HDInsight .NET SDK</span></span>

<span data-ttu-id="f3833-336">如需使用 hello.NET SDK tooapply 指令碼 tooa 叢集的範例，請參閱[https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action)。</span><span class="sxs-lookup"><span data-stu-id="f3833-336">For an example of using hello .NET SDK tooapply scripts tooa cluster, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

## <a name="view-history-promote-and-demote-script-actions"></a><span data-ttu-id="f3833-337">檢視歷程記錄、升級和降級指令碼動作</span><span class="sxs-lookup"><span data-stu-id="f3833-337">View history, promote, and demote Script Actions</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="f3833-338">使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f3833-338">Using hello Azure portal</span></span>

1. <span data-ttu-id="f3833-339">從 hello [Azure 入口網站](https://portal.azure.com)，選取您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f3833-339">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="f3833-340">從 hello HDInsight 叢集的概觀，請選取 hello**指令碼動作**磚。</span><span class="sxs-lookup"><span data-stu-id="f3833-340">From hello HDInsight cluster overview, select hello **Script Actions** tile.</span></span>

    ![指令碼動作磚](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="f3833-342">您也可以選取**所有設定**，然後選取 [**指令碼動作**從 hello 設定] 區段。</span><span class="sxs-lookup"><span data-stu-id="f3833-342">You can also select **All settings** and then select **Script Actions** from hello Settings section.</span></span>

4. <span data-ttu-id="f3833-343">對此叢集的指令碼的歷程記錄會顯示在 hello 指令碼動作 > 一節。</span><span class="sxs-lookup"><span data-stu-id="f3833-343">A history of scripts for this cluster is displayed on hello Script Actions section.</span></span> <span data-ttu-id="f3833-344">此資訊包含持續性指令碼清單。</span><span class="sxs-lookup"><span data-stu-id="f3833-344">This information includes a list of persisted scripts.</span></span> <span data-ttu-id="f3833-345">在 hello 以下螢幕擷取畫面，您可以看到此叢集執行的指令碼已的 Solr 該 hello。</span><span class="sxs-lookup"><span data-stu-id="f3833-345">In hello screenshot below, you can see that hello Solr script has been ran on this cluster.</span></span> <span data-ttu-id="f3833-346">hello 螢幕擷取畫面不會顯示任何持續性的指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-346">hello screenshot does not show any persisted scripts.</span></span>

    ![指令碼動作區段](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. <span data-ttu-id="f3833-348">選取指令碼從 hello 歷程記錄顯示 hello 這個指令碼的內容 > 一節。</span><span class="sxs-lookup"><span data-stu-id="f3833-348">Selecting a script from hello history displays hello Properties section for this script.</span></span> <span data-ttu-id="f3833-349">從 hello 囉 」 畫面頂端，您可以重新執行 hello 指令碼，或將它升級。</span><span class="sxs-lookup"><span data-stu-id="f3833-349">From hello top of hello screen, you can rerun hello script or promote it.</span></span>

    ![指令碼動作屬性](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. <span data-ttu-id="f3833-351">您也可以使用 hello **...** toohello 方 hello 指令碼動作 > 一節 tooperform 動作上的項目。</span><span class="sxs-lookup"><span data-stu-id="f3833-351">You can also use hello **...** toohello right of entries on hello Script Actions section tooperform actions.</span></span>

    ![指令碼動作...使用情況](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a><span data-ttu-id="f3833-353">使用 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3833-353">Using Azure PowerShell</span></span>

| <span data-ttu-id="f3833-354">使用下列 hello...</span><span class="sxs-lookup"><span data-stu-id="f3833-354">Use hello following...</span></span> | <span data-ttu-id="f3833-355">太...</span><span class="sxs-lookup"><span data-stu-id="f3833-355">too...</span></span> |
| --- | --- |
| <span data-ttu-id="f3833-356">Get-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="f3833-356">Get-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="f3833-357">擷取持續性指令碼動作的資訊</span><span class="sxs-lookup"><span data-stu-id="f3833-357">Retrieve information on persisted script actions</span></span> |
| <span data-ttu-id="f3833-358">Get-AzureRmHDInsightScriptActionHistory</span><span class="sxs-lookup"><span data-stu-id="f3833-358">Get-AzureRmHDInsightScriptActionHistory</span></span> |<span data-ttu-id="f3833-359">擷取指令碼動作套用 toohello 叢集或特定的指令碼的詳細資料的歷程記錄</span><span class="sxs-lookup"><span data-stu-id="f3833-359">Retrieve a history of script actions applied toohello cluster, or details for a specific script</span></span> |
| <span data-ttu-id="f3833-360">Set-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="f3833-360">Set-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="f3833-361">升級特定指令碼動作 tooa 保存的指令碼動作</span><span class="sxs-lookup"><span data-stu-id="f3833-361">Promotes an ad hoc script action tooa persisted script action</span></span> |
| <span data-ttu-id="f3833-362">Remove-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="f3833-362">Remove-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="f3833-363">將保存的指令碼動作 tooan 臨機操作動作降級</span><span class="sxs-lookup"><span data-stu-id="f3833-363">Demotes a persisted script action tooan ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="f3833-364">使用`Remove-AzureRmHDInsightPersistedScriptAction`不復原 hello 指令碼所執行的動作。</span><span class="sxs-lookup"><span data-stu-id="f3833-364">Using `Remove-AzureRmHDInsightPersistedScriptAction` does not undo hello actions performed by a script.</span></span> <span data-ttu-id="f3833-365">此 cmdlet 只會移除 hello 保存旗標。</span><span class="sxs-lookup"><span data-stu-id="f3833-365">This cmdlet only removes hello persisted flag.</span></span>

<span data-ttu-id="f3833-366">下列範例指令碼的 hello 示範如何使用 hello cmdlet toopromote，然後再降級指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-366">hello following example script demonstrates using hello cmdlets toopromote, then demote a script.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-hello-azure-cli"></a><span data-ttu-id="f3833-367">使用 Azure CLI hello</span><span class="sxs-lookup"><span data-stu-id="f3833-367">Using hello Azure CLI</span></span>

| <span data-ttu-id="f3833-368">使用下列 hello...</span><span class="sxs-lookup"><span data-stu-id="f3833-368">Use hello following...</span></span> | <span data-ttu-id="f3833-369">太...</span><span class="sxs-lookup"><span data-stu-id="f3833-369">too...</span></span> |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |<span data-ttu-id="f3833-370">擷取保存的指令碼動作清單</span><span class="sxs-lookup"><span data-stu-id="f3833-370">Retrieve a list of persisted script actions</span></span> |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |<span data-ttu-id="f3833-371">擷取特定的保存指令碼動作資訊</span><span class="sxs-lookup"><span data-stu-id="f3833-371">Retrieve information on a specific persisted script action</span></span> |
| `azure hdinsight script-action history list <clustername>` |<span data-ttu-id="f3833-372">擷取指令碼動作套用 toohello 叢集歷程的記錄</span><span class="sxs-lookup"><span data-stu-id="f3833-372">Retrieve a history of script actions applied toohello cluster</span></span> |
| `azure hdinsight script-action history show <clustername> <scriptname>` |<span data-ttu-id="f3833-373">擷取特定指令碼動作的資訊</span><span class="sxs-lookup"><span data-stu-id="f3833-373">Retrieve information on a specific script action</span></span> |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |<span data-ttu-id="f3833-374">升級特定指令碼動作 tooa 保存的指令碼動作</span><span class="sxs-lookup"><span data-stu-id="f3833-374">Promotes an ad hoc script action tooa persisted script action</span></span> |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |<span data-ttu-id="f3833-375">將保存的指令碼動作 tooan 臨機操作動作降級</span><span class="sxs-lookup"><span data-stu-id="f3833-375">Demotes a persisted script action tooan ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="f3833-376">使用`azure hdinsight script-action persisted delete`不復原 hello 指令碼所執行的動作。</span><span class="sxs-lookup"><span data-stu-id="f3833-376">Using `azure hdinsight script-action persisted delete` does not undo hello actions performed by a script.</span></span> <span data-ttu-id="f3833-377">此 cmdlet 只會移除 hello 保存旗標。</span><span class="sxs-lookup"><span data-stu-id="f3833-377">This cmdlet only removes hello persisted flag.</span></span>

### <a name="using-hello-hdinsight-net-sdk"></a><span data-ttu-id="f3833-378">使用 hello HDInsight.NET SDK</span><span class="sxs-lookup"><span data-stu-id="f3833-378">Using hello HDInsight .NET SDK</span></span>

<span data-ttu-id="f3833-379">如需使用 hello.NET SDK tooretrieve 從叢集的指令碼記錄的範例，請升級或降級指令碼，請參閱[https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action)。</span><span class="sxs-lookup"><span data-stu-id="f3833-379">For an example of using hello .NET SDK tooretrieve script history from a cluster, promote or demote scripts, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

> [!NOTE]
> <span data-ttu-id="f3833-380">此範例也示範如何 tooinstall HDInsight 應用程式使用 hello.NET SDK。</span><span class="sxs-lookup"><span data-stu-id="f3833-380">This example also demonstrates how tooinstall an HDInsight application using hello .NET SDK.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="f3833-381">支援在 HDInsight 叢集上使用開放原始碼軟體</span><span class="sxs-lookup"><span data-stu-id="f3833-381">Support for open-source software used on HDInsight clusters</span></span>

<span data-ttu-id="f3833-382">hello Microsoft Azure HDInsight 服務會使用開放原始碼技術 Hadoop 周圍形成的生態系統。</span><span class="sxs-lookup"><span data-stu-id="f3833-382">hello Microsoft Azure HDInsight service uses an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="f3833-383">Microsoft Azure 可為開放原始碼技術提供一般層級的支援。</span><span class="sxs-lookup"><span data-stu-id="f3833-383">Microsoft Azure provides a general level of support for open-source technologies.</span></span> <span data-ttu-id="f3833-384">如需詳細資訊，請參閱 hello**支援範圍**區段 hello [Azure 支援常見問題集網站，](https://azure.microsoft.com/support/faq/)。</span><span class="sxs-lookup"><span data-stu-id="f3833-384">For more information, see hello **Support Scope** section of hello [Azure Support FAQ website](https://azure.microsoft.com/support/faq/).</span></span> <span data-ttu-id="f3833-385">hello HDInsight 服務的內建的元件，提供一層額外的支援。</span><span class="sxs-lookup"><span data-stu-id="f3833-385">hello HDInsight service provides an additional level of support for built-in components.</span></span>

<span data-ttu-id="f3833-386">有兩種可用在 hello HDInsight 服務的開放原始碼元件類型：</span><span class="sxs-lookup"><span data-stu-id="f3833-386">There are two types of open-source components that are available in hello HDInsight service:</span></span>

* <span data-ttu-id="f3833-387">**內建元件**-HDInsight 叢集上已預先安裝這些元件，並提供 hello 叢集的核心功能。</span><span class="sxs-lookup"><span data-stu-id="f3833-387">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of hello cluster.</span></span> <span data-ttu-id="f3833-388">例如，YARN ResourceManager、 hello Hive 查詢語言 (HiveQL) 及 hello 砲象兵程式庫屬於 toothis 類別目錄。</span><span class="sxs-lookup"><span data-stu-id="f3833-388">For example, YARN ResourceManager, hello Hive query language (HiveQL), and hello Mahout library belong toothis category.</span></span> <span data-ttu-id="f3833-389">叢集元件的完整清單位於[hello HDInsight 所提供的 Hadoop 叢集版本的新](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="f3833-389">A full list of cluster components is available in [What's new in hello Hadoop cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
* <span data-ttu-id="f3833-390">**自訂元件**-您為 hello 叢集的使用者可以安裝或使用您的工作負載中用於 hello 社群或您所建立的任何元件。</span><span class="sxs-lookup"><span data-stu-id="f3833-390">**Custom components** - You, as a user of hello cluster, can install or use in your workload any component available in hello community or created by you.</span></span>

> [!WARNING]
> <span data-ttu-id="f3833-391">完全支援元件時附上 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f3833-391">Components provided with hello HDInsight cluster are fully supported.</span></span> <span data-ttu-id="f3833-392">Microsoft 支援服務可協助 tooisolate，並解決問題的相關的 toothese 元件。</span><span class="sxs-lookup"><span data-stu-id="f3833-392">Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="f3833-393">自訂元件會收到盡商業上合理支援 toohelp 您 toofurther hello 問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="f3833-393">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="f3833-394">Microsoft 支援服務可能無法 tooresolve hello 問題，或它們可能會要求您 tooengage 可用頻道 hello 開放原始碼技術，找到深層的專業知識，針對該項技術。</span><span class="sxs-lookup"><span data-stu-id="f3833-394">Microsoft support may be able tooresolve hello issue OR they may ask you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="f3833-395">例如，有許多社群網站可以使用，像是：[HDInsight 的 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)、[http://stackoverflow.com](http://stackoverflow.com)。另外，Apache 專案在 [http://apache.org](http://apache.org) 上有專案網站，例如 [Hadoop](http://hadoop.apache.org/)。</span><span class="sxs-lookup"><span data-stu-id="f3833-395">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

<span data-ttu-id="f3833-396">hello HDInsight 服務提供數種方式 toouse 自訂元件。</span><span class="sxs-lookup"><span data-stu-id="f3833-396">hello HDInsight service provides several ways toouse custom components.</span></span> <span data-ttu-id="f3833-397">hello 套用相同層級支援，無論是使用還是 hello 叢集上安裝元件。</span><span class="sxs-lookup"><span data-stu-id="f3833-397">hello same level of support applies, regardless of how a component is used or installed on hello cluster.</span></span> <span data-ttu-id="f3833-398">hello 下列清單將描述 hello 最常見方式，可以使用自訂元件的 HDInsight 叢集上：</span><span class="sxs-lookup"><span data-stu-id="f3833-398">hello following list describes hello most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="f3833-399">提交作業-Hadoop 或其他類型的執行，或使用自訂元件的工作可以提交的 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="f3833-399">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted toohello cluster.</span></span>

2. <span data-ttu-id="f3833-400">叢集自訂-叢集建立期間，您可以指定其他設定及自訂 hello 叢集節點已安裝的元件。</span><span class="sxs-lookup"><span data-stu-id="f3833-400">Cluster customization - During cluster creation, you can specify additional settings and custom components that are installed on hello cluster nodes.</span></span>

3. <span data-ttu-id="f3833-401">範例-常用的自訂元件、 Microsoft 和其他人可能會提供如何使用這些元件在 hello HDInsight 叢集上的範例。</span><span class="sxs-lookup"><span data-stu-id="f3833-401">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on hello HDInsight clusters.</span></span> <span data-ttu-id="f3833-402">提供這些範例，但是沒有支援。</span><span class="sxs-lookup"><span data-stu-id="f3833-402">These samples are provided without support.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f3833-403">疑難排解</span><span class="sxs-lookup"><span data-stu-id="f3833-403">Troubleshooting</span></span>

<span data-ttu-id="f3833-404">您可以使用指令碼動作所記錄的 Ambari web UI tooview 資訊。</span><span class="sxs-lookup"><span data-stu-id="f3833-404">You can use Ambari web UI tooview information logged by script actions.</span></span> <span data-ttu-id="f3833-405">如果 hello 指令碼無法在叢集建立期間，hello 記錄檔也會提供 hello 與 hello 叢集相關聯的預設儲存體帳戶中的。</span><span class="sxs-lookup"><span data-stu-id="f3833-405">If hello script fails during cluster creation, hello logs are also available in hello default storage account associated with hello cluster.</span></span> <span data-ttu-id="f3833-406">本節提供資訊 tooretrieve hello 記錄使用這兩個選項的方式。</span><span class="sxs-lookup"><span data-stu-id="f3833-406">This section provides information on how tooretrieve hello logs using both these options.</span></span>

### <a name="using-hello-ambari-web-ui"></a><span data-ttu-id="f3833-407">使用 hello Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="f3833-407">Using hello Ambari Web UI</span></span>

1. <span data-ttu-id="f3833-408">在瀏覽器中瀏覽 toohttps://CLUSTERNAME.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="f3833-408">In your browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="f3833-409">CLUSTERNAME 取代 hello 的 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="f3833-409">Replace CLUSTERNAME with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="f3833-410">出現提示時，輸入 hello 叢集 hello 管理帳戶名稱 （管理員） 和密碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-410">When prompted, enter hello admin account name (admin) and password for hello cluster.</span></span> <span data-ttu-id="f3833-411">Web 表單中，您可能必須 tooreenter hello 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="f3833-411">You may have tooreenter hello admin credentials in a web form.</span></span>

2. <span data-ttu-id="f3833-412">在 hello 頁面頂端的 hello hello 列中，選取 hello **ops**項目。</span><span class="sxs-lookup"><span data-stu-id="f3833-412">From hello bar at hello top of hello page, select hello **ops** entry.</span></span> <span data-ttu-id="f3833-413">會顯示目前和舊版上執行的作業透過 Ambari hello 叢集清單。</span><span class="sxs-lookup"><span data-stu-id="f3833-413">A list of current and previous operations performed on hello cluster through Ambari is displayed.</span></span>

    ![Ambari Web UI 列與選取的 ops](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. <span data-ttu-id="f3833-415">尋找 hello 的項目**執行\_customscriptaction**在 hello**作業**資料行。</span><span class="sxs-lookup"><span data-stu-id="f3833-415">Find hello entries that have **run\_customscriptaction** in hello **Operations** column.</span></span> <span data-ttu-id="f3833-416">Hello 指令碼動作執行時，會建立這些項目。</span><span class="sxs-lookup"><span data-stu-id="f3833-416">These entries are created when hello Script Actions run.</span></span>

    ![作業的螢幕擷取畫面](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    <span data-ttu-id="f3833-418">tooview hello STDOUT 和 STDERR 輸出選取 hello run\customscriptaction 項目，然後向下鑽研 hello 連結。</span><span class="sxs-lookup"><span data-stu-id="f3833-418">tooview hello STDOUT and STDERR output, select hello run\customscriptaction entry and drill down through hello links.</span></span> <span data-ttu-id="f3833-419">Hello 指令碼執行時，不會產生此輸出，而且可能包含有用的資訊。</span><span class="sxs-lookup"><span data-stu-id="f3833-419">This output is generated when hello script runs, and may contain useful information.</span></span>

### <a name="access-logs-from-hello-default-storage-account"></a><span data-ttu-id="f3833-420">從 hello 預設儲存體帳戶的存取記錄檔</span><span class="sxs-lookup"><span data-stu-id="f3833-420">Access logs from hello default storage account</span></span>

<span data-ttu-id="f3833-421">如果 hello 叢集建立失敗，因為 tooa 指令碼動作錯誤，可以從 hello 叢集儲存體帳戶存取 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f3833-421">If hello cluster creation fails due tooa script action error, hello logs can be accessed from hello cluster storage account.</span></span>

* <span data-ttu-id="f3833-422">hello 儲存體記錄位於`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`。</span><span class="sxs-lookup"><span data-stu-id="f3833-422">hello storage logs are available at `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span></span>

    ![作業的螢幕擷取畫面](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    <span data-ttu-id="f3833-424">在此目錄中，hello 記錄檔會分別叢集前端節點、 workernode，和動物園管理員節點組織。</span><span class="sxs-lookup"><span data-stu-id="f3833-424">Under this directory, hello logs are organized separately for headnode, workernode, and zookeeper nodes.</span></span> <span data-ttu-id="f3833-425">部分範例如下：</span><span class="sxs-lookup"><span data-stu-id="f3833-425">Some examples are:</span></span>

    * <span data-ttu-id="f3833-426">**前端節點** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="f3833-426">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="f3833-427">**背景工作節點** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="f3833-427">**Worker node** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="f3833-428">**Zookeeper 節點** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="f3833-428">**Zookeeper node** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span></span>

* <span data-ttu-id="f3833-429">所有 stdout 和 stderr 的 hello 對應主機都是上傳 toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3833-429">All stdout and stderr of hello corresponding host is uploaded toohello storage account.</span></span> <span data-ttu-id="f3833-430">每個指令碼動作分別有一個 **output-\*.txt** 和 **errors-\*.txt**。</span><span class="sxs-lookup"><span data-stu-id="f3833-430">There is one **output-\*.txt** and **errors-\*.txt** for each script action.</span></span> <span data-ttu-id="f3833-431">hello 輸出 *.txt 檔案包含 hello URI 中的 hello 收到 hello 主機執行的指令碼資訊。</span><span class="sxs-lookup"><span data-stu-id="f3833-431">hello output-*.txt file contains information about hello URI of hello script that got run on hello host.</span></span> <span data-ttu-id="f3833-432">例如</span><span class="sxs-lookup"><span data-stu-id="f3833-432">For example</span></span>

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* <span data-ttu-id="f3833-433">您可使用 hello 重複建立指令碼動作叢集相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="f3833-433">It's possible that you repeatedly create a script action cluster with hello same name.</span></span> <span data-ttu-id="f3833-434">在這種情況下，您可以區分 hello hello 日期資料夾名稱為基礎的相關記錄。</span><span class="sxs-lookup"><span data-stu-id="f3833-434">In such case, you can distinguish hello relevant logs based on hello DATE folder name.</span></span> <span data-ttu-id="f3833-435">例如，hello 資料夾結構上不同的日期所建立的叢集 (mycluster) 會出現類似 toohello 下列記錄項目：</span><span class="sxs-lookup"><span data-stu-id="f3833-435">For example, hello folder structure for a cluster (mycluster) created on different dates appears similar toohello following log entries:</span></span>

    <span data-ttu-id="f3833-436">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span><span class="sxs-lookup"><span data-stu-id="f3833-436">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span></span>

* <span data-ttu-id="f3833-437">如果您以 hello 建立指令碼動作叢集名稱相同的 hello 相同天，您可以使用 hello 唯一的前置詞 tooidentify hello 相關記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f3833-437">If you create a script action cluster with hello same name on hello same day, you can use hello unique prefix tooidentify hello relevant log files.</span></span>

* <span data-ttu-id="f3833-438">如果您建立叢集附近上午 12:00 （午夜），很可能 hello 記錄檔跨越兩天。</span><span class="sxs-lookup"><span data-stu-id="f3833-438">If you create a cluster near 12:00AM (midnight), it's possible that hello log files span across two days.</span></span> <span data-ttu-id="f3833-439">在這種情況下，您會看到兩個不同的日期資料夾 hello 相同叢集中。</span><span class="sxs-lookup"><span data-stu-id="f3833-439">In such cases, you see two different date folders for hello same cluster.</span></span>

* <span data-ttu-id="f3833-440">正在上傳記錄檔 toohello 預設容器可能會佔用 too5 分鐘，特別是針對大型叢集。</span><span class="sxs-lookup"><span data-stu-id="f3833-440">Uploading log files toohello default container can take up too5 mins, especially for large clusters.</span></span> <span data-ttu-id="f3833-441">因此，如果您想 tooaccess hello 記錄檔，您不應該立即刪除 hello 叢集的指令碼動作失敗時。</span><span class="sxs-lookup"><span data-stu-id="f3833-441">So, if you want tooaccess hello logs, you should not immediately delete hello cluster if a script action fails.</span></span>

### <a name="ambari-watchdog"></a><span data-ttu-id="f3833-442">Ambari 看門狗</span><span class="sxs-lookup"><span data-stu-id="f3833-442">Ambari watchdog</span></span>

> [!WARNING]
> <span data-ttu-id="f3833-443">請勿變更 hello hello Ambari 監視 (hdinsightwatchdog) 以 Linux 為基礎的 HDInsight 叢集上的密碼。</span><span class="sxs-lookup"><span data-stu-id="f3833-443">Do not change hello password for hello Ambari Watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="f3833-444">變更此帳戶的 hello 密碼中斷 hello 能力 toorun 新指令碼動作在 hello HDInsight 叢集上。</span><span class="sxs-lookup"><span data-stu-id="f3833-444">Changing hello password for this account breaks hello ability toorun new script actions on hello HDInsight cluster.</span></span>

### <a name="cant-import-name-blobservice"></a><span data-ttu-id="f3833-445">無法匯入名稱 BlobService</span><span class="sxs-lookup"><span data-stu-id="f3833-445">Can't import name BlobService</span></span>

<span data-ttu-id="f3833-446">__徵兆__: hello 指令碼動作會失敗。</span><span class="sxs-lookup"><span data-stu-id="f3833-446">__Symptoms__: hello script action fails.</span></span> <span data-ttu-id="f3833-447">當您檢視 Ambari hello 作業時，會顯示文字類似 toohello 下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="f3833-447">Text similar toohello following error is displayed when you view hello operation in Ambari:</span></span>

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

<span data-ttu-id="f3833-448">__可能的原因__： 如果您升級 hello Python Azure 儲存體用戶端所包含的 hello HDInsight 叢集，就會發生這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="f3833-448">__Cause__: This error occurs if you upgrade hello Python Azure Storage client that is included with hello HDInsight cluster.</span></span> <span data-ttu-id="f3833-449">HDInsight 需要 Azure 儲存體用戶端 0.20.0。</span><span class="sxs-lookup"><span data-stu-id="f3833-449">HDInsight expects Azure Storage client 0.20.0.</span></span>

<span data-ttu-id="f3833-450">__解析__: tooresolve 這個錯誤，請手動連接 tooeach 叢集節點使用`ssh`並使用 hello 遵循命令 tooreinstall hello 正確的儲存體用戶端版本：</span><span class="sxs-lookup"><span data-stu-id="f3833-450">__Resolution__: tooresolve this error, manually connect tooeach cluster node using `ssh` and use hello following command tooreinstall hello correct storage client version:</span></span>

```
sudo pip install azure-storage==0.20.0
```

<span data-ttu-id="f3833-451">透過 SSH 的連接 toohello 叢集上的資訊，請參閱[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="f3833-451">For information on connecting toohello cluster with SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a><span data-ttu-id="f3833-452">歷程記錄不會顯示在叢集建立期間使用的指令碼</span><span class="sxs-lookup"><span data-stu-id="f3833-452">History doesn't show scripts used during cluster creation</span></span>

<span data-ttu-id="f3833-453">如果您在 2016 年 3 月 15 日之前建立叢集，您可能不會在動作歷程記錄中看到任何項目。</span><span class="sxs-lookup"><span data-stu-id="f3833-453">If your cluster was created before March 15, 2016, you may not see an entry in Script Action history.</span></span> <span data-ttu-id="f3833-454">如果您在 2016 年 3 月 15 日之後調整 hello 叢集 hello 在叢集建立期間使用的指令碼出現的歷程記錄會套用 toonew hello 一部分的 hello 叢集中節點的調整大小作業。</span><span class="sxs-lookup"><span data-stu-id="f3833-454">If you resize hello cluster after March 15, 2016, hello scripts using during cluster creation appear in history as they are applied toonew nodes in hello cluster as part of hello resize operation.</span></span>

<span data-ttu-id="f3833-455">有兩種例外狀況：</span><span class="sxs-lookup"><span data-stu-id="f3833-455">There are two exceptions:</span></span>

* <span data-ttu-id="f3833-456">如果您的叢集在 2015 年 9 月 1 日之前建立。</span><span class="sxs-lookup"><span data-stu-id="f3833-456">If your cluster was created before September 1, 2015.</span></span> <span data-ttu-id="f3833-457">此日期是引進指令碼動作的日期。</span><span class="sxs-lookup"><span data-stu-id="f3833-457">This date is when Script Actions were introduced.</span></span> <span data-ttu-id="f3833-458">在此日期之前建立的任何叢集可能都未使用指令碼動作建立叢集。</span><span class="sxs-lookup"><span data-stu-id="f3833-458">Any cluster created before this date could not have used Script Actions for cluster creation.</span></span>

* <span data-ttu-id="f3833-459">如果您使用多個指令碼動作在叢集建立期間，並使用相同名稱的多個指令碼，或 hello 的 hello 名稱相同，但不同參數的多個指令碼的相同 URI。</span><span class="sxs-lookup"><span data-stu-id="f3833-459">If you used multiple Script Actions during cluster creation, and used hello same name for multiple scripts, or hello same name, same URI, but different parameters for multiple scripts.</span></span> <span data-ttu-id="f3833-460">在這些情況下，您會收到下列錯誤 hello:</span><span class="sxs-lookup"><span data-stu-id="f3833-460">In these cases, you receive hello following error:</span></span>

    <span data-ttu-id="f3833-461">動作可以是任何新指令碼已 tooconflicting 指令碼名稱，在現有的指令碼因為此叢集上不執行。</span><span class="sxs-lookup"><span data-stu-id="f3833-461">No new script actions can be ran on this cluster due tooconflicting script names in existing scripts.</span></span> <span data-ttu-id="f3833-462">建立叢集時所提供的指令碼名稱全都必須是唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="f3833-462">Script names provided at cluster create must be all unique.</span></span> <span data-ttu-id="f3833-463">既有的指令碼會在調整大小時執行。</span><span class="sxs-lookup"><span data-stu-id="f3833-463">Existing scripts are ran on resize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3833-464">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f3833-464">Next steps</span></span>

* [<span data-ttu-id="f3833-465">開發 HDInsight 的指令碼動作指令碼</span><span class="sxs-lookup"><span data-stu-id="f3833-465">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions-linux.md)
* [<span data-ttu-id="f3833-466">在 HDInsight 叢集上安裝及使用 Solr</span><span class="sxs-lookup"><span data-stu-id="f3833-466">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="f3833-467">在 HDInsight 叢集上安裝及使用 Giraph</span><span class="sxs-lookup"><span data-stu-id="f3833-467">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="f3833-468">新增額外的儲存體 tooan HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="f3833-468">Add additional storage tooan HDInsight cluster</span></span>](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "叢集建立期間的階段"
