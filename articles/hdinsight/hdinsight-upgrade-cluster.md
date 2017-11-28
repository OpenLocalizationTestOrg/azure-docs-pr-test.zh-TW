---
title: "aaaUpgrade HDInsight 叢集 tooa 較新版本的 Azure |Microsoft 文件"
description: "了解如何 tooUpgrade HDInsight 叢集 tooa 較新版本。"
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
ms.openlocfilehash: 5fff3c9bc88dfbcbc1ccb0188accdfbbec3a62f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hdinsight-cluster-tooa-newer-version"></a><span data-ttu-id="9232a-103">HDInsight 叢集 tooa 較新版本升級</span><span class="sxs-lookup"><span data-stu-id="9232a-103">Upgrade HDInsight cluster tooa newer version</span></span>
<span data-ttu-id="9232a-104">tootake 利用 hello 最新的 HDInsight 功能，我們建議您的 HDInsight 叢集是升級的 toolatest 版本。</span><span class="sxs-lookup"><span data-stu-id="9232a-104">tootake advantage of hello latest HDInsight features, we recommend that HDInsight clusters be upgraded toolatest version.</span></span> <span data-ttu-id="9232a-105">請遵循下列指導方針 tooupgrade hello 您的 HDInsight 叢集版本。</span><span class="sxs-lookup"><span data-stu-id="9232a-105">Follow hello below guidelines tooupgrade your HDInsight cluster versions.</span></span>

> [!NOTE]
> <span data-ttu-id="9232a-106">HDInsight 叢集版本 3.2 與 3.3 已接近淘汰日期。</span><span class="sxs-lookup"><span data-stu-id="9232a-106">HDInsight clusters version 3.2 and 3.3 are nearing retirement date.</span></span> <span data-ttu-id="9232a-107">如需支援之 HDInsight 版本的詳細資訊，請參閱 [HDInsight 元件版本](hdinsight-component-versioning.md#supported-hdinsight-versions)。</span><span class="sxs-lookup"><span data-stu-id="9232a-107">For information on supported version of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>
>
>

## <a name="upgrade-tasks"></a><span data-ttu-id="9232a-108">升級工作</span><span class="sxs-lookup"><span data-stu-id="9232a-108">Upgrade tasks</span></span>
<span data-ttu-id="9232a-109">hello 工作流程 tooupgrade HDInsight 叢集如下所示。</span><span class="sxs-lookup"><span data-stu-id="9232a-109">hello workflow tooupgrade HDInsight Cluster is as follows.</span></span>

![升級工作流程圖表](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. <span data-ttu-id="9232a-111">讀取這份文件的每個區段 toounderstand 變更時，可能會需要升級您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="9232a-111">Read each section of this document toounderstand changes that may be required when upgrading your HDInsight cluster.</span></span>
2. <span data-ttu-id="9232a-112">將叢集建立為測試/品質保證環境。</span><span class="sxs-lookup"><span data-stu-id="9232a-112">Create a cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="9232a-113">如需有關如何建立叢集的詳細資訊，請參閱[深入了解如何 toocreate 以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="9232a-113">For more information on creating a cluster, see [Learn how toocreate Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
3. <span data-ttu-id="9232a-114">現有的作業、 資料來源和接收器 toohello 新環境的複本。</span><span class="sxs-lookup"><span data-stu-id="9232a-114">Copy existing jobs, data sources, and sinks toohello new environment.</span></span> <span data-ttu-id="9232a-115">請參閱[複製資料 tooTest 環境](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9232a-115">See [Copy Data tooTest Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span></span>
4. <span data-ttu-id="9232a-116">執行驗證測試 toomake 確定您作業的工作，如預期般 hello 新叢集上。</span><span class="sxs-lookup"><span data-stu-id="9232a-116">Perform validation testing toomake sure that your jobs work as expected on hello new cluster.</span></span>


<span data-ttu-id="9232a-117">一旦您已確認一切運作正常，排程 hello 移轉停機的時間。</span><span class="sxs-lookup"><span data-stu-id="9232a-117">Once you have verified that everything works as expected, schedule downtime for hello migration.</span></span> <span data-ttu-id="9232a-118">在這個停機時間，下列動作 hello:</span><span class="sxs-lookup"><span data-stu-id="9232a-118">During this downtime, do hello following actions:</span></span>

1.  <span data-ttu-id="9232a-119">備份儲存在本機 hello 叢集節點上的任何暫時性資料。</span><span class="sxs-lookup"><span data-stu-id="9232a-119">Back up any transient data stored locally on hello cluster nodes.</span></span> <span data-ttu-id="9232a-120">例如，如果您的資料是直接儲存在前端節點上。</span><span class="sxs-lookup"><span data-stu-id="9232a-120">For example, if you have data stored directly on a head node.</span></span>
2.  <span data-ttu-id="9232a-121">刪除 hello 現有叢集。</span><span class="sxs-lookup"><span data-stu-id="9232a-121">Delete hello existing cluster.</span></span>
3.  <span data-ttu-id="9232a-122">建立叢集 hello 中相同的 VNET 子網路具有最新的 （或支援的） HDI 版本使用 hello 相同預設資料存放區的 hello 先前使用的叢集。</span><span class="sxs-lookup"><span data-stu-id="9232a-122">Create a cluster in hello same VNET subnet with latest (or supported) HDI version using hello same default data store that hello previous cluster used.</span></span> <span data-ttu-id="9232a-123">這可讓 hello 針對現有的實際執行資料新叢集 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="9232a-123">This allows hello new cluster toocontinue working against your existing production data.</span></span>
4.  <span data-ttu-id="9232a-124">匯入任何已備份的暫時性資料。</span><span class="sxs-lookup"><span data-stu-id="9232a-124">Import any transient data you backed up.</span></span>
5.  <span data-ttu-id="9232a-125">開始作業/仍會繼續處理使用 hello 新叢集。</span><span class="sxs-lookup"><span data-stu-id="9232a-125">Start jobs/continue processing using hello new cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9232a-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9232a-126">Next Steps</span></span>
* [<span data-ttu-id="9232a-127">了解如何 toocreate 以 Linux 為基礎的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="9232a-127">Learn how toocreate Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="9232a-128">連接 tooHDInsight 使用 SSH</span><span class="sxs-lookup"><span data-stu-id="9232a-128">Connect tooHDInsight using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="9232a-129">使用 Ambari 管理 Linux 型叢集</span><span class="sxs-lookup"><span data-stu-id="9232a-129">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

