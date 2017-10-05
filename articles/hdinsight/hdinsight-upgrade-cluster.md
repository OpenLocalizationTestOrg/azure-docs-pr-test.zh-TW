---
title: "將 HDInsight 叢集升級為較新的版本 - Azure | Microsoft Docs"
description: "了解如何將 HDInsight 叢集升級為較新的版本。"
services: hdinsight
documentationcenter: 
author: bhanupr
manager: asadk
editor: bhanupr
ms.assetid: 60eb573c-e639-4815-9fc6-ea8b106d8dbc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: bhanupr
ms.openlocfilehash: fa2e37bd922690322ccc3d8f68128180d013b701
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-hdinsight-cluster-to-a-newer-version"></a><span data-ttu-id="df0ca-103">將 HDInsight 叢集升級為更新的版本</span><span class="sxs-lookup"><span data-stu-id="df0ca-103">Upgrade HDInsight cluster to a newer version</span></span>
<span data-ttu-id="df0ca-104">若要充分利用最新的 HDInsight 功能，建議您將 HDInsight 叢集升級到最新的版本。</span><span class="sxs-lookup"><span data-stu-id="df0ca-104">To take advantage of the latest HDInsight features, we recommend that HDInsight clusters be upgraded to latest version.</span></span> <span data-ttu-id="df0ca-105">依照下面的指導方針升級您的 HDInsight 叢集版本。</span><span class="sxs-lookup"><span data-stu-id="df0ca-105">Follow the below guidelines to upgrade your HDInsight cluster versions.</span></span>

> [!NOTE]
> <span data-ttu-id="df0ca-106">HDInsight 叢集版本 3.2 與 3.3 已接近淘汰日期。</span><span class="sxs-lookup"><span data-stu-id="df0ca-106">HDInsight clusters version 3.2 and 3.3 are nearing retirement date.</span></span> <span data-ttu-id="df0ca-107">如需支援之 HDInsight 版本的詳細資訊，請參閱 [HDInsight 元件版本](hdinsight-component-versioning.md#supported-hdinsight-versions)。</span><span class="sxs-lookup"><span data-stu-id="df0ca-107">For information on supported version of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>
>
>

## <a name="upgrade-tasks"></a><span data-ttu-id="df0ca-108">升級工作</span><span class="sxs-lookup"><span data-stu-id="df0ca-108">Upgrade tasks</span></span>
<span data-ttu-id="df0ca-109">升級 HDInsight 叢集的工作流程如下。</span><span class="sxs-lookup"><span data-stu-id="df0ca-109">The workflow to upgrade HDInsight Cluster is as follows.</span></span>

![升級工作流程圖表](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. <span data-ttu-id="df0ca-111">閱讀此文件的每一節，以了解在升級 HDInsight 叢集時，可能需要進行的變更。</span><span class="sxs-lookup"><span data-stu-id="df0ca-111">Read each section of this document to understand changes that may be required when upgrading your HDInsight cluster.</span></span>
2. <span data-ttu-id="df0ca-112">將叢集建立為測試/品質保證環境。</span><span class="sxs-lookup"><span data-stu-id="df0ca-112">Create a cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="df0ca-113">如需建立叢集的詳細資訊，請參閱[了解如何建立 Linux 型 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="df0ca-113">For more information on creating a cluster, see [Learn how to create Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
3. <span data-ttu-id="df0ca-114">將現有的作業、資料來源與接收複製到新的環境。</span><span class="sxs-lookup"><span data-stu-id="df0ca-114">Copy existing jobs, data sources, and sinks to the new environment.</span></span> <span data-ttu-id="df0ca-115">請參閱[將資料複製到測試環境](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment)以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="df0ca-115">See [Copy Data To Test Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span></span>
4. <span data-ttu-id="df0ca-116">執行驗證測試以確保您的工作在新叢集上會如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="df0ca-116">Perform validation testing to make sure that your jobs work as expected on the new cluster.</span></span>


<span data-ttu-id="df0ca-117">當您已驗證一切都會如預期般運作之後，請為移轉排定停機時間。</span><span class="sxs-lookup"><span data-stu-id="df0ca-117">Once you have verified that everything works as expected, schedule downtime for the migration.</span></span> <span data-ttu-id="df0ca-118">在此停機期間，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="df0ca-118">During this downtime, do the following actions:</span></span>

1.  <span data-ttu-id="df0ca-119">備份所有儲存在本機叢集節點上的暫時性資料。</span><span class="sxs-lookup"><span data-stu-id="df0ca-119">Back up any transient data stored locally on the cluster nodes.</span></span> <span data-ttu-id="df0ca-120">例如，如果您的資料是直接儲存在前端節點上。</span><span class="sxs-lookup"><span data-stu-id="df0ca-120">For example, if you have data stored directly on a head node.</span></span>
2.  <span data-ttu-id="df0ca-121">刪除現有的叢集。</span><span class="sxs-lookup"><span data-stu-id="df0ca-121">Delete the existing cluster.</span></span>
3.  <span data-ttu-id="df0ca-122">使用與先前叢集所使用之預設資料存放區相同的資料存放區，在具有最新 (或受支援) 之 HDI 版本的 VNET 子網路中建立叢集。</span><span class="sxs-lookup"><span data-stu-id="df0ca-122">Create a cluster in the same VNET subnet with latest (or supported) HDI version using the same default data store that the previous cluster used.</span></span> <span data-ttu-id="df0ca-123">這將能允許新叢集針對現有的生產資料繼續運作。</span><span class="sxs-lookup"><span data-stu-id="df0ca-123">This allows the new cluster to continue working against your existing production data.</span></span>
4.  <span data-ttu-id="df0ca-124">匯入任何已備份的暫時性資料。</span><span class="sxs-lookup"><span data-stu-id="df0ca-124">Import any transient data you backed up.</span></span>
5.  <span data-ttu-id="df0ca-125">使用新叢集啟動工作/繼續處理。</span><span class="sxs-lookup"><span data-stu-id="df0ca-125">Start jobs/continue processing using the new cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df0ca-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="df0ca-126">Next Steps</span></span>
* [<span data-ttu-id="df0ca-127">了解如何建立 Linux 型 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="df0ca-127">Learn how to create Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="df0ca-128">使用 SSH 連線到 HDInsight</span><span class="sxs-lookup"><span data-stu-id="df0ca-128">Connect to HDInsight using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="df0ca-129">使用 Ambari 管理 Linux 型叢集</span><span class="sxs-lookup"><span data-stu-id="df0ca-129">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

