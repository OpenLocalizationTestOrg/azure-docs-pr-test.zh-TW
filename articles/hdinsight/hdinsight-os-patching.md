---
title: "為以 Linux 為基礎的 HDInsight 叢集設定作業系統修補排程 - Azure | Microsoft Docs"
description: "了解如何為以 Linux 為基礎的 HDInsight 叢集設定作業系統修補排程。"
services: hdinsight
documentationcenter: 
author: bprakash
manager: asadk
editor: bprakash
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: bhanupr
ms.openlocfilehash: af3c5a19ae8e2e606e4b0506f9f6dddb41192e40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="os-patching-for-hdinsight"></a><span data-ttu-id="646e8-103">HDInsight 的作業系統修補</span><span class="sxs-lookup"><span data-stu-id="646e8-103">OS patching for HDInsight</span></span> 
<span data-ttu-id="646e8-104">HDInsight 作為受管理的 Hadoop 服務，會負責修補 HDInsight 叢集所使用之基礎 VM 的作業系統。</span><span class="sxs-lookup"><span data-stu-id="646e8-104">As a managed Hadoop service, HDInsight takes care of patching the OS of the underlying VMs used by HDInsight clusters.</span></span> <span data-ttu-id="646e8-105">自 2016 年 8 月 1 日起，我們已變更以 Linux 為基礎之 HDInsight 叢集 (3.4 版或更新版本) 的客體 OS 修補原則。</span><span class="sxs-lookup"><span data-stu-id="646e8-105">As of August 1, 2016, we have changed the guest OS patching policy for Linux-based HDInsight clusters (version 3.4 or greater).</span></span> <span data-ttu-id="646e8-106">新原則的目標是大幅減少因為修補而產生的重新開機次數。</span><span class="sxs-lookup"><span data-stu-id="646e8-106">The goal of the new policy is to significantly reduce the number of reboots due to patching.</span></span> <span data-ttu-id="646e8-107">新的原則將會在每個星期一或星期四 UTC 上午 12 時開始，以交錯方式在任何指定叢集的節點之間，繼續修補 Linux 叢集上的虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="646e8-107">The new policy will continue to patch virtual machines (VMs) on Linux clusters every Monday or Thursday starting at 12AM UTC in a staggered fashion across nodes in any given cluster.</span></span> <span data-ttu-id="646e8-108">不過，任何指定的 VM 每隔 30 天只會因為客體 OS 修補而最多重新開機一次。</span><span class="sxs-lookup"><span data-stu-id="646e8-108">However, any given VM will only reboot at most once every 30 days due to guest OS patching.</span></span> <span data-ttu-id="646e8-109">此外，新建立的叢集在叢集建立之後，也不會在 30 天內第一次重新開機。</span><span class="sxs-lookup"><span data-stu-id="646e8-109">In addition, the first reboot for a newly created cluster will not happen sooner than 30 days from the cluster creation date.</span></span> <span data-ttu-id="646e8-110">VM 重新開機後，修補便會生效。</span><span class="sxs-lookup"><span data-stu-id="646e8-110">Patches will be effective once the VMs are rebooted.</span></span>

## <a name="how-to-configure-the-os-patching-schedule-for-linux-based-hdinsight-clusters"></a><span data-ttu-id="646e8-111">如何為以 Linux 為基礎的 HDInsight 叢集設定作業系統修補排程</span><span class="sxs-lookup"><span data-stu-id="646e8-111">How to configure the OS patching schedule for Linux-based HDInsight clusters</span></span>
<span data-ttu-id="646e8-112">HDInsight 叢集中的虛擬機器有時候需要重新開機，以便系統可以安裝重要的安全性修補程式。</span><span class="sxs-lookup"><span data-stu-id="646e8-112">The virtual machines in an HDInsight cluster need to be rebooted occasionally so that important security patches can be installed.</span></span> <span data-ttu-id="646e8-113">自 2016 年 8 月 1 日起，新式的以 Linux 為基礎的 HDInsight 叢集 (3.4 版或更新版本) 會使用下列排程來重新開機︰</span><span class="sxs-lookup"><span data-stu-id="646e8-113">As of August 1, 2016, new Linux-based HDInsight clusters (version 3.4 or greater,) are rebooted using the following schedule:</span></span>

1. <span data-ttu-id="646e8-114">在 30 天的期間內，叢集中的虛擬機器最多只能為了修補而重新開機一次。</span><span class="sxs-lookup"><span data-stu-id="646e8-114">A virtual machine in the cluster can only reboot for patches at most, once within a 30-day period.</span></span>
2. <span data-ttu-id="646e8-115">重新開機作業會於 12AM UTC 開始。</span><span class="sxs-lookup"><span data-stu-id="646e8-115">The reboot occurs starting at 12AM UTC.</span></span>
3. <span data-ttu-id="646e8-116">叢集中的虛擬機器會錯開進行重新開機程序，因此在重新開機程序進行期間，叢集仍可供使用。</span><span class="sxs-lookup"><span data-stu-id="646e8-116">The reboot process is staggered across virtual machines in the cluster, so the cluster is still available during the reboot process.</span></span>
4. <span data-ttu-id="646e8-117">新建立之叢集的第一次重新開機，最快要在叢集建立日期的 30 天之後才會發生。</span><span class="sxs-lookup"><span data-stu-id="646e8-117">The first reboot for a newly created cluster will not happen sooner than 30 days after the cluster creation date.</span></span>

<span data-ttu-id="646e8-118">您可以使用本文所述的指令碼動作來修改作業系統修補排程，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="646e8-118">Using the script action described in this article, you can modify the OS patching schedule as follows:</span></span>
1. <span data-ttu-id="646e8-119">啟用或停用自動重新開機</span><span class="sxs-lookup"><span data-stu-id="646e8-119">Enable or disable automatic reboots</span></span>
2. <span data-ttu-id="646e8-120">設定重新開機頻率 (重新開機間隔天數)</span><span class="sxs-lookup"><span data-stu-id="646e8-120">Set the frequency of reboots (days between reboots)</span></span>
3. <span data-ttu-id="646e8-121">設定要在星期幾重新開機</span><span class="sxs-lookup"><span data-stu-id="646e8-121">Set the day of the week when a reboot occurs</span></span>

> [!NOTE]
> <span data-ttu-id="646e8-122">此指令碼動作只適用於在 2016 年 8 月 1 日之後建立的以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="646e8-122">This script action will only work with Linux-based HDInsight clusters created after August 1st, 2016.</span></span> <span data-ttu-id="646e8-123">VM 重新開機後，修補才會生效。</span><span class="sxs-lookup"><span data-stu-id="646e8-123">Patches will be effective only when VMs are rebooted.</span></span> 
>

## <a name="how-to-use-the-script"></a><span data-ttu-id="646e8-124">如何使用指令碼</span><span class="sxs-lookup"><span data-stu-id="646e8-124">How to use the script</span></span> 

<span data-ttu-id="646e8-125">使用此指令碼時需要下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="646e8-125">When using this script requires the following information:</span></span>
1. <span data-ttu-id="646e8-126">指令碼位置︰https://hdiconfigactions.blob.core.windows.net/linuxospatchingrebootconfigv01/os-patching-reboot-config.sh。</span><span class="sxs-lookup"><span data-stu-id="646e8-126">The script location: https://hdiconfigactions.blob.core.windows.net/linuxospatchingrebootconfigv01/os-patching-reboot-config.sh.</span></span>
    <span data-ttu-id="646e8-127">HDInsight 會使用此 URI 在叢集中的所有虛擬機器上尋找和執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="646e8-127">HDInsight uses this URI to find and run the script on all the virtual machines in the cluster.</span></span>
  
2. <span data-ttu-id="646e8-128">指令碼會套用到的叢集節點類型︰headnode、workernode、zookeeper。</span><span class="sxs-lookup"><span data-stu-id="646e8-128">The cluster node types that the script is applied to: headnode, workernode, zookeeper.</span></span> <span data-ttu-id="646e8-129">此指令碼必須套用至叢集中的所有節點類型。</span><span class="sxs-lookup"><span data-stu-id="646e8-129">This script must be applied to all node types in the cluster.</span></span> <span data-ttu-id="646e8-130">如果未套用至某個節點類型，則該節點類型的虛擬機器會繼續使用先前的修補排程。</span><span class="sxs-lookup"><span data-stu-id="646e8-130">If it is not applied to a node type, then the virtual machines for that node type will continue to use the previous patching schedule.</span></span>


3.  <span data-ttu-id="646e8-131">參數︰此指令碼接受三個數值參數︰</span><span class="sxs-lookup"><span data-stu-id="646e8-131">Parameter: This script accepts three numeric parameters:</span></span>

    | <span data-ttu-id="646e8-132">參數</span><span class="sxs-lookup"><span data-stu-id="646e8-132">Parameter</span></span> | <span data-ttu-id="646e8-133">定義</span><span class="sxs-lookup"><span data-stu-id="646e8-133">Definition</span></span> |
    | --- | --- |
    | <span data-ttu-id="646e8-134">啟用/停用自動重新開機</span><span class="sxs-lookup"><span data-stu-id="646e8-134">Enable/disable automatic reboots</span></span> |<span data-ttu-id="646e8-135">0 或 1。</span><span class="sxs-lookup"><span data-stu-id="646e8-135">0 or 1.</span></span> <span data-ttu-id="646e8-136">值為 0 會停用自動重新開機，1 則會啟用自動重新開機。</span><span class="sxs-lookup"><span data-stu-id="646e8-136">A value of 0 disables automatic reboots while 1 enables automatic reboots.</span></span> |
    | <span data-ttu-id="646e8-137">頻率</span><span class="sxs-lookup"><span data-stu-id="646e8-137">Frequency</span></span> |<span data-ttu-id="646e8-138">7 到 90 (含)。</span><span class="sxs-lookup"><span data-stu-id="646e8-138">7 to 90 (inclusive).</span></span> <span data-ttu-id="646e8-139">需要重新開機的修補程式在將虛擬機器重新開機之前所要等候的天數。</span><span class="sxs-lookup"><span data-stu-id="646e8-139">The number of days to wait before rebooting the virtual machines for patches that require a reboot.</span></span> |
    | <span data-ttu-id="646e8-140">星期幾</span><span class="sxs-lookup"><span data-stu-id="646e8-140">Day of week</span></span> |<span data-ttu-id="646e8-141">1 到 7 (含)。</span><span class="sxs-lookup"><span data-stu-id="646e8-141">1 to 7 (inclusive).</span></span> <span data-ttu-id="646e8-142">值為 1 表示虛擬機器應該在星期一重新開機，7 則表示星期日。例如，使用參數 1 60 2，會導致虛擬機器每隔 60 天 (最多) 就會在星期二自動重新開機。</span><span class="sxs-lookup"><span data-stu-id="646e8-142">A value of 1 indicates the reboot should occur on a Monday, and 7 indicates a Sunday.For example, using parameters of 1 60 2 results in automatic reboots every 60 days (at most) on Tuesday.</span></span> |
    | <span data-ttu-id="646e8-143">持續性</span><span class="sxs-lookup"><span data-stu-id="646e8-143">Persistence</span></span> |<span data-ttu-id="646e8-144">對現有叢集套用指令碼動作時，您可以將指令碼標示為持續性。</span><span class="sxs-lookup"><span data-stu-id="646e8-144">When applying a script action to an existing cluster, you can mark the script as persisted.</span></span> <span data-ttu-id="646e8-145">持續性指令碼會在透過調整作業將新的 workernode 新增至叢集時套用。</span><span class="sxs-lookup"><span data-stu-id="646e8-145">Persisted scripts are applied when new workernodes are added to the cluster through scaling operations.</span></span> |

> [!NOTE]
> <span data-ttu-id="646e8-146">在對現有叢集套用此指令碼時，您必須將其標示為持續性。</span><span class="sxs-lookup"><span data-stu-id="646e8-146">You must mark this script as persisted when applying to an existing cluster.</span></span> <span data-ttu-id="646e8-147">否則，透過調整作業所建立的新節點會使用預設的修補排程。</span><span class="sxs-lookup"><span data-stu-id="646e8-147">Otherwise, any new nodes created through scaling      operations will use the default patching schedule.</span></span>
<span data-ttu-id="646e8-148">如果您在進行叢集建立程序時套用指令碼，該指令碼會自動成為持續性狀態。</span><span class="sxs-lookup"><span data-stu-id="646e8-148">If you apply the script as part of the cluster creation process, it is persisted automatically.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="646e8-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="646e8-149">Next steps</span></span>

<span data-ttu-id="646e8-150">如需使用指令碼動作的特定步驟，請參閱[使用指令碼動作來自訂以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)中的以下章節：</span><span class="sxs-lookup"><span data-stu-id="646e8-150">For specific steps on using the script action, see the following sections in the [Customize Linuz-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md):</span></span>

* [<span data-ttu-id="646e8-151">在建立叢集期間使用指令碼動作</span><span class="sxs-lookup"><span data-stu-id="646e8-151">Use a script action during cluster creation</span></span>](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation)
* [<span data-ttu-id="646e8-152">將指令碼動作套用到執行中的叢集</span><span class="sxs-lookup"><span data-stu-id="646e8-152">Apply a script action to a running cluster</span></span>](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster)
