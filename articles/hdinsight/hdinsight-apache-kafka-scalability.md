---
title: "Apache Kafka 提高級別 - Azure HDInsight | Microsoft Docs"
description: "了解如何設定在 Azure HDInsight 上 Apache Kafka 叢集的受控磁碟來提高延展性。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/14/2017
ms.author: larryfr
ms.openlocfilehash: 880a186a3d9a23b013294b0121e8265270d160cc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a><span data-ttu-id="5f110-103">在 HDInsight 上設定 Apache Kafka 的儲存體和延展性</span><span class="sxs-lookup"><span data-stu-id="5f110-103">Configure storage and scalability for Apache Kafka on HDInsight</span></span>

<span data-ttu-id="5f110-104">了解如何設定 Apache Kafka 在 HDInsight 上所使用的受控磁碟數目。</span><span class="sxs-lookup"><span data-stu-id="5f110-104">Learn how to configure the number of managed disks used by Apache Kafka on HDInsight.</span></span>

<span data-ttu-id="5f110-105">HDInsight 上的 Kafka 會在 HDInsight 叢集中使用虛擬機器的本機磁碟。</span><span class="sxs-lookup"><span data-stu-id="5f110-105">Kafka on HDInsight uses the local disk of the virtual machines in the HDInsight cluster.</span></span> <span data-ttu-id="5f110-106">由於 Kafka 的 I/O 非常大量，因此會使用 [Azure 受控磁碟](../virtual-machines/windows/managed-disks-overview.md)來提供高輸送量，並提供每個節點更多儲存空間。</span><span class="sxs-lookup"><span data-stu-id="5f110-106">Since Kafka is very I/O heavy, [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) is used to provide high throughput and provide more storage per node.</span></span> <span data-ttu-id="5f110-107">如果將傳統的虛擬硬碟 (VHD) 用於 Kafka，每個節點就會限制為 1 TB。</span><span class="sxs-lookup"><span data-stu-id="5f110-107">If traditional virtual hard drives (VHD) were used for Kafka, each node is limited to 1 TB.</span></span> <span data-ttu-id="5f110-108">使用受控磁碟時，您可以利用多個磁碟在叢集中的每個節點達到 16 TB。</span><span class="sxs-lookup"><span data-stu-id="5f110-108">With managed disks, you can use multiple disks to achieve 16 TB for each node in the cluster.</span></span>

<span data-ttu-id="5f110-109">下圖提供 HDInsight 上的 Kafka 採用受控磁碟之前與 HDInsight 上的 Kafka 採用受控磁碟之間的比較：</span><span class="sxs-lookup"><span data-stu-id="5f110-109">The following diagram provides a comparison between Kafka on HDInsight before managed disks, and Kafka on HDInsight with managed disks:</span></span>

![圖表顯示 HDInsight 上的 Kafka 每個 VM 使用單一 VHD 與每個 VM 使用多個受控磁碟](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a><span data-ttu-id="5f110-111">設定受控磁碟：Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5f110-111">Configure managed disks: Azure portal</span></span>

1. <span data-ttu-id="5f110-112">請遵循[建立 HDInsight 叢集](hdinsight-hadoop-create-linux-clusters-portal.md)中的步驟，了解使用入口網站建立叢集的一般步驟。</span><span class="sxs-lookup"><span data-stu-id="5f110-112">Follow the steps in the [Create an HDInsight cluster](hdinsight-hadoop-create-linux-clusters-portal.md) to understand the common steps to create a cluster using the portal.</span></span> <span data-ttu-id="5f110-113">請勿完成入口網站建立程序。</span><span class="sxs-lookup"><span data-stu-id="5f110-113">Do not complete the portal creation process.</span></span>

2. <span data-ttu-id="5f110-114">從 [叢集大小] 刀鋒視窗中，使用 [每個背景工作角色節點的磁碟] 欄位來設定磁碟的數目。</span><span class="sxs-lookup"><span data-stu-id="5f110-114">From the __Cluster size__ blade, use the __Disks per worker node__ field to configure the number of disks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f110-115">受控磁碟的類型可以是__標準__ (HDD) 或__進階__ (SSD)。</span><span class="sxs-lookup"><span data-stu-id="5f110-115">The type of managed disk can be either __Standard__ (HDD) or __Premium__ (SSD).</span></span> <span data-ttu-id="5f110-116">進階磁碟會與 DS 和 GS 系列搭配使用。</span><span class="sxs-lookup"><span data-stu-id="5f110-116">Premium disks are used with DS and GS series VMs.</span></span> <span data-ttu-id="5f110-117">所有其他的 VM 類型是使用標準磁碟。</span><span class="sxs-lookup"><span data-stu-id="5f110-117">All other VM types use standard.</span></span>

    ![叢集大小刀鋒視窗中的映像，每個背景工作角色節點的磁碟以反白顯示](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a><span data-ttu-id="5f110-119">設定受控磁碟：Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="5f110-119">Configure managed disks: Resource Manager template</span></span>

<span data-ttu-id="5f110-120">若要控制背景工作角色節點在 Kafka 叢集中所使用的磁碟數目，請使用下列區段的範本：</span><span class="sxs-lookup"><span data-stu-id="5f110-120">To control the number of disks used by the worker nodes in a Kafka cluster, use the following section of the template:</span></span>

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

<span data-ttu-id="5f110-121">您可以在 [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json) 找到示範如何設定受控磁碟的完整範本。</span><span class="sxs-lookup"><span data-stu-id="5f110-121">You can find a complete template that demonstrates how to configure managed disks at [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f110-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5f110-122">Next steps</span></span>

<span data-ttu-id="5f110-123">如需使用 HDInsight 上 Kafka 的詳細資訊，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="5f110-123">For more information on working with Kafka on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="5f110-124">使用 MirrorMaker 建立 Apache Kafka on HDInsight 複本</span><span class="sxs-lookup"><span data-stu-id="5f110-124">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="5f110-125">使用 Apache Storm 搭配 HDInsight 上的 Kafka</span><span class="sxs-lookup"><span data-stu-id="5f110-125">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="5f110-126">使用 Apache Spark 搭配 Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f110-126">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="5f110-127">透過 Azure 虛擬網路連線至 Kafka</span><span class="sxs-lookup"><span data-stu-id="5f110-127">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [<span data-ttu-id="5f110-128">使用 Kafka 之受控磁碟的 HDInsight 部落格</span><span class="sxs-lookup"><span data-stu-id="5f110-128">HDInsight blog on managed disks with Kafka</span></span>](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)