---
title: "aaaApache Kafka 增加小數位數-Azure HDInsight |Microsoft 文件"
description: "了解如何 tooconfigure 管理 Azure HDInsight tooincrease 延展性 Apache Kafka 叢集的磁碟。"
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
ms.openlocfilehash: b51114b33359f2c385f057a7a7a5b134cad27e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a><span data-ttu-id="8397b-103">在 HDInsight 上設定 Apache Kafka 的儲存體和延展性</span><span class="sxs-lookup"><span data-stu-id="8397b-103">Configure storage and scalability for Apache Kafka on HDInsight</span></span>

<span data-ttu-id="8397b-104">了解如何 tooconfigure hello 數目受管理的磁碟使用 Apache Kafka HDInsight 上。</span><span class="sxs-lookup"><span data-stu-id="8397b-104">Learn how tooconfigure hello number of managed disks used by Apache Kafka on HDInsight.</span></span>

<span data-ttu-id="8397b-105">HDInsight 上的 Kafka hello HDInsight 叢集中使用 hello hello 虛擬機器的本機磁碟。</span><span class="sxs-lookup"><span data-stu-id="8397b-105">Kafka on HDInsight uses hello local disk of hello virtual machines in hello HDInsight cluster.</span></span> <span data-ttu-id="8397b-106">因為 Kafka 是非常 I/O， [Azure 受管理磁碟](../virtual-machines/windows/managed-disks-overview.md)使用的 tooprovide 高輸送量，並提供每個節點的更多儲存空間。</span><span class="sxs-lookup"><span data-stu-id="8397b-106">Since Kafka is very I/O heavy, [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) is used tooprovide high throughput and provide more storage per node.</span></span> <span data-ttu-id="8397b-107">如果 Kafka 用於傳統的虛擬硬碟 (VHD)，每個節點是有限的 too1 TB。</span><span class="sxs-lookup"><span data-stu-id="8397b-107">If traditional virtual hard drives (VHD) were used for Kafka, each node is limited too1 TB.</span></span> <span data-ttu-id="8397b-108">受管理的磁碟，您可以使用多個磁碟 tooachieve 16 TB hello 叢集中的每個節點。</span><span class="sxs-lookup"><span data-stu-id="8397b-108">With managed disks, you can use multiple disks tooachieve 16 TB for each node in hello cluster.</span></span>

<span data-ttu-id="8397b-109">hello 下列圖表提供 Kafka HDInsight 之前受管理的磁碟上和 Kafka 之間的比較在 HDInsight 上使用受管理的磁碟：</span><span class="sxs-lookup"><span data-stu-id="8397b-109">hello following diagram provides a comparison between Kafka on HDInsight before managed disks, and Kafka on HDInsight with managed disks:</span></span>

![圖表顯示 HDInsight 上的 Kafka 每個 VM 使用單一 VHD 與每個 VM 使用多個受控磁碟](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a><span data-ttu-id="8397b-111">設定受控磁碟：Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8397b-111">Configure managed disks: Azure portal</span></span>

1. <span data-ttu-id="8397b-112">Hello 中的 hello 步驟[建立的 HDInsight 叢集](hdinsight-hadoop-create-linux-clusters-portal.md)toounderstand hello 通用步驟 toocreate 使用 hello 入口網站的叢集。</span><span class="sxs-lookup"><span data-stu-id="8397b-112">Follow hello steps in hello [Create an HDInsight cluster](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand hello common steps toocreate a cluster using hello portal.</span></span> <span data-ttu-id="8397b-113">不會完成 hello 入口網站的建立程序。</span><span class="sxs-lookup"><span data-stu-id="8397b-113">Do not complete hello portal creation process.</span></span>

2. <span data-ttu-id="8397b-114">從 hello__叢集大小__刀鋒視窗中，使用 hello__磁碟每個背景工作節點__欄位磁碟 tooconfigure hello 數目。</span><span class="sxs-lookup"><span data-stu-id="8397b-114">From hello __Cluster size__ blade, use hello __Disks per worker node__ field tooconfigure hello number of disks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8397b-115">hello 的受管理的磁碟類型可以是__標準__(HDD) 或__Premium__ (SSD)。</span><span class="sxs-lookup"><span data-stu-id="8397b-115">hello type of managed disk can be either __Standard__ (HDD) or __Premium__ (SSD).</span></span> <span data-ttu-id="8397b-116">進階磁碟會與 DS 和 GS 系列搭配使用。</span><span class="sxs-lookup"><span data-stu-id="8397b-116">Premium disks are used with DS and GS series VMs.</span></span> <span data-ttu-id="8397b-117">所有其他的 VM 類型是使用標準磁碟。</span><span class="sxs-lookup"><span data-stu-id="8397b-117">All other VM types use standard.</span></span>

    ![Hello 叢集大小刀鋒視窗中的每個反白顯示的背景工作節點 hello 磁碟的映像](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a><span data-ttu-id="8397b-119">設定受控磁碟：Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="8397b-119">Configure managed disks: Resource Manager template</span></span>

<span data-ttu-id="8397b-120">toocontrol hello 磁碟數目 Kafka 叢集中，使用 hello 遵循 hello 範本區段中的 hello 背景工作節點使用：</span><span class="sxs-lookup"><span data-stu-id="8397b-120">toocontrol hello number of disks used by hello worker nodes in a Kafka cluster, use hello following section of hello template:</span></span>

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

<span data-ttu-id="8397b-121">您可以找到完整的範本示範如何 tooconfigure 管理磁碟在[https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json)。</span><span class="sxs-lookup"><span data-stu-id="8397b-121">You can find a complete template that demonstrates how tooconfigure managed disks at [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8397b-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8397b-122">Next steps</span></span>

<span data-ttu-id="8397b-123">與 HDInsight 上 Kafka 需使用詳細資訊，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="8397b-123">For more information on working with Kafka on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="8397b-124">在 HDInsight 上使用 MirrorMaker toocreate Kafka 的複本</span><span class="sxs-lookup"><span data-stu-id="8397b-124">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="8397b-125">使用 Apache Storm 搭配 HDInsight 上的 Kafka</span><span class="sxs-lookup"><span data-stu-id="8397b-125">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="8397b-126">使用 Apache Spark 搭配 Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="8397b-126">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="8397b-127">透過 Azure 虛擬網路連線 tooKafka</span><span class="sxs-lookup"><span data-stu-id="8397b-127">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [<span data-ttu-id="8397b-128">使用 Kafka 之受控磁碟的 HDInsight 部落格</span><span class="sxs-lookup"><span data-stu-id="8397b-128">HDInsight blog on managed disks with Kafka</span></span>](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)