---
title: "以 Linux 為基礎的 HDInsight 叢集-Azure aaaConfigure OS 修補排程 |Microsoft 文件"
description: "了解如何 tooconfigure OS 修補排程以 Linux 為基礎的 HDInsight 叢集。"
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
ms.openlocfilehash: 1598d64e594d7e8a68573fc63dd86051a5a9d025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="os-patching-for-hdinsight"></a><span data-ttu-id="5284c-103">HDInsight 的作業系統修補</span><span class="sxs-lookup"><span data-stu-id="5284c-103">OS patching for HDInsight</span></span> 
<span data-ttu-id="5284c-104">為 managed Hadoop 服務時，會負責 HDInsight 修補 hello 作業系統的 HDInsight 叢集所使用的基礎 Vm hello。</span><span class="sxs-lookup"><span data-stu-id="5284c-104">As a managed Hadoop service, HDInsight takes care of patching hello OS of hello underlying VMs used by HDInsight clusters.</span></span> <span data-ttu-id="5284c-105">從 2016 年 8 月 1 日開始，我們已用於以 Linux 為基礎的 HDInsight 叢集 （版本 3.4 或更新版本） 的 hello 客體 OS 修補原則。</span><span class="sxs-lookup"><span data-stu-id="5284c-105">As of August 1, 2016, we have changed hello guest OS patching policy for Linux-based HDInsight clusters (version 3.4 or greater).</span></span> <span data-ttu-id="5284c-106">hello hello 新的原則目標是 toosignificantly 減少重新開機次數 hello 到期 toopatching。</span><span class="sxs-lookup"><span data-stu-id="5284c-106">hello goal of hello new policy is toosignificantly reduce hello number of reboots due toopatching.</span></span> <span data-ttu-id="5284c-107">hello 新的原則將會繼續在 Linux 上的 toopatch 虛擬機器 (Vm) 叢集的每個星期一或星期四上午 12 utc，以交錯方式啟動任何指定的叢集節點之間。</span><span class="sxs-lookup"><span data-stu-id="5284c-107">hello new policy will continue toopatch virtual machines (VMs) on Linux clusters every Monday or Thursday starting at 12AM UTC in a staggered fashion across nodes in any given cluster.</span></span> <span data-ttu-id="5284c-108">不過，任何指定的 VM 會只重新開機一次每 30 天到期 tooguest OS 修補程式。</span><span class="sxs-lookup"><span data-stu-id="5284c-108">However, any given VM will only reboot at most once every 30 days due tooguest OS patching.</span></span> <span data-ttu-id="5284c-109">此外，新建立的叢集 hello 第一次重新開機不會發生更快地從 hello 叢集建立日期的 30 天前。</span><span class="sxs-lookup"><span data-stu-id="5284c-109">In addition, hello first reboot for a newly created cluster will not happen sooner than 30 days from hello cluster creation date.</span></span> <span data-ttu-id="5284c-110">Hello Vm 重新開機後，修補程式就會生效。</span><span class="sxs-lookup"><span data-stu-id="5284c-110">Patches will be effective once hello VMs are rebooted.</span></span>

## <a name="how-tooconfigure-hello-os-patching-schedule-for-linux-based-hdinsight-clusters"></a><span data-ttu-id="5284c-111">如何 tooconfigure hello 以 Linux 為基礎的 HDInsight 叢集的 OS 修補排程</span><span class="sxs-lookup"><span data-stu-id="5284c-111">How tooconfigure hello OS patching schedule for Linux-based HDInsight clusters</span></span>
<span data-ttu-id="5284c-112">hello HDInsight 叢集中的虛擬機器需要 toobe 以便可以安裝重要的安全性修補程式偶爾重新開機。</span><span class="sxs-lookup"><span data-stu-id="5284c-112">hello virtual machines in an HDInsight cluster need toobe rebooted occasionally so that important security patches can be installed.</span></span> <span data-ttu-id="5284c-113">從 2016 年 8 月 1 日開始新 Linux 為基礎的 HDInsight 叢集 （版本 3.4 或更多，） 會重新開機，使用下列排程 hello:</span><span class="sxs-lookup"><span data-stu-id="5284c-113">As of August 1, 2016, new Linux-based HDInsight clusters (version 3.4 or greater,) are rebooted using hello following schedule:</span></span>

1. <span data-ttu-id="5284c-114">Hello 叢集中的虛擬機器可以只重新開機的修補程式最多 30 天期間內一次。</span><span class="sxs-lookup"><span data-stu-id="5284c-114">A virtual machine in hello cluster can only reboot for patches at most, once within a 30-day period.</span></span>
2. <span data-ttu-id="5284c-115">hello 重新開機，就會發生在上午 12 UTC 開始。</span><span class="sxs-lookup"><span data-stu-id="5284c-115">hello reboot occurs starting at 12AM UTC.</span></span>
3. <span data-ttu-id="5284c-116">hello 重新開機程序被階段性跨 hello 叢集中的虛擬機器，因此 hello 叢集 hello 重新開機程序期間仍然可以使用。</span><span class="sxs-lookup"><span data-stu-id="5284c-116">hello reboot process is staggered across virtual machines in hello cluster, so hello cluster is still available during hello reboot process.</span></span>
4. <span data-ttu-id="5284c-117">hello 新建的叢集的第一次重新開機不會更快地 hello 叢集建立日期後的 30 天前發生。</span><span class="sxs-lookup"><span data-stu-id="5284c-117">hello first reboot for a newly created cluster will not happen sooner than 30 days after hello cluster creation date.</span></span>

<span data-ttu-id="5284c-118">使用本文中所述的 hello 指令碼動作時，您就可以修改 hello OS 修補排程，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5284c-118">Using hello script action described in this article, you can modify hello OS patching schedule as follows:</span></span>
1. <span data-ttu-id="5284c-119">啟用或停用自動重新開機</span><span class="sxs-lookup"><span data-stu-id="5284c-119">Enable or disable automatic reboots</span></span>
2. <span data-ttu-id="5284c-120">組 hello 頻率的重新開機 （重新開機之間的天數）</span><span class="sxs-lookup"><span data-stu-id="5284c-120">Set hello frequency of reboots (days between reboots)</span></span>
3. <span data-ttu-id="5284c-121">設定 hello 星期幾 hello 發生重新開機</span><span class="sxs-lookup"><span data-stu-id="5284c-121">Set hello day of hello week when a reboot occurs</span></span>

> [!NOTE]
> <span data-ttu-id="5284c-122">此指令碼動作只適用於在 2016 年 8 月 1 日之後建立的以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="5284c-122">This script action will only work with Linux-based HDInsight clusters created after August 1st, 2016.</span></span> <span data-ttu-id="5284c-123">VM 重新開機後，修補才會生效。</span><span class="sxs-lookup"><span data-stu-id="5284c-123">Patches will be effective only when VMs are rebooted.</span></span> 
>

## <a name="how-toouse-hello-script"></a><span data-ttu-id="5284c-124">如何 toouse hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="5284c-124">How toouse hello script</span></span> 

<span data-ttu-id="5284c-125">當使用這個指令碼需要下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="5284c-125">When using this script requires hello following information:</span></span>
1. <span data-ttu-id="5284c-126">hello 指令碼位置： https://hdiconfigactions.blob.core.windows.net/linuxospatchingrebootconfigv01/os-patching-reboot-config.sh。HDInsight 會使用此 URI toofind 和 hello 叢集中的所有 hello 虛擬機器上執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5284c-126">hello script location: https://hdiconfigactions.blob.core.windows.net/linuxospatchingrebootconfigv01/os-patching-reboot-config.sh.  HDInsight uses this URI toofind and run hello script on all hello virtual machines in hello cluster.</span></span>
  
2. <span data-ttu-id="5284c-127">hello hello 指令碼套用至叢集節點型別： 叢集前端節點，workernode，動物園管理員。</span><span class="sxs-lookup"><span data-stu-id="5284c-127">hello cluster node types that hello script is applied to: headnode, workernode, zookeeper.</span></span> <span data-ttu-id="5284c-128">此指令碼必須套用的 tooall hello 叢集中的節點型別。</span><span class="sxs-lookup"><span data-stu-id="5284c-128">This script must be applied tooall node types in hello cluster.</span></span> <span data-ttu-id="5284c-129">如果不是套用的 tooa 節點型別，則 hello 虛擬機器，該節點型別會繼續 toouse hello 先前修補排程。</span><span class="sxs-lookup"><span data-stu-id="5284c-129">If it is not applied tooa node type, then hello virtual machines for that node type will continue toouse hello previous patching schedule.</span></span>


3.  <span data-ttu-id="5284c-130">參數︰此指令碼接受三個數值參數︰</span><span class="sxs-lookup"><span data-stu-id="5284c-130">Parameter: This script accepts three numeric parameters:</span></span>

    | <span data-ttu-id="5284c-131">參數</span><span class="sxs-lookup"><span data-stu-id="5284c-131">Parameter</span></span> | <span data-ttu-id="5284c-132">定義</span><span class="sxs-lookup"><span data-stu-id="5284c-132">Definition</span></span> |
    | --- | --- |
    | <span data-ttu-id="5284c-133">啟用/停用自動重新開機</span><span class="sxs-lookup"><span data-stu-id="5284c-133">Enable/disable automatic reboots</span></span> |<span data-ttu-id="5284c-134">0 或 1。</span><span class="sxs-lookup"><span data-stu-id="5284c-134">0 or 1.</span></span> <span data-ttu-id="5284c-135">值為 0 會停用自動重新開機，1 則會啟用自動重新開機。</span><span class="sxs-lookup"><span data-stu-id="5284c-135">A value of 0 disables automatic reboots while 1 enables automatic reboots.</span></span> |
    | <span data-ttu-id="5284c-136">頻率</span><span class="sxs-lookup"><span data-stu-id="5284c-136">Frequency</span></span> |<span data-ttu-id="5284c-137">7 too90 （含）。</span><span class="sxs-lookup"><span data-stu-id="5284c-137">7 too90 (inclusive).</span></span> <span data-ttu-id="5284c-138">hello 天 toowait 之前重新開機 hello 修補程式需要重新開機的虛擬機器數目。</span><span class="sxs-lookup"><span data-stu-id="5284c-138">hello number of days toowait before rebooting hello virtual machines for patches that require a reboot.</span></span> |
    | <span data-ttu-id="5284c-139">星期幾</span><span class="sxs-lookup"><span data-stu-id="5284c-139">Day of week</span></span> |<span data-ttu-id="5284c-140">1 too7 （含）。</span><span class="sxs-lookup"><span data-stu-id="5284c-140">1 too7 (inclusive).</span></span> <span data-ttu-id="5284c-141">值為 1 表示 hello 重新開機應該會發生在星期一，7 表示 Sunday.For 範例中，使用參數 1 60 2 個導致自動重新啟動每隔 60 天 （最多） 個星期二。</span><span class="sxs-lookup"><span data-stu-id="5284c-141">A value of 1 indicates hello reboot should occur on a Monday, and 7 indicates a Sunday.For example, using parameters of 1 60 2 results in automatic reboots every 60 days (at most) on Tuesday.</span></span> |
    | <span data-ttu-id="5284c-142">持續性</span><span class="sxs-lookup"><span data-stu-id="5284c-142">Persistence</span></span> |<span data-ttu-id="5284c-143">當套用指令碼動作 tooan 現有叢集，您可以將 hello 指令碼標示為保存。</span><span class="sxs-lookup"><span data-stu-id="5284c-143">When applying a script action tooan existing cluster, you can mark hello script as persisted.</span></span> <span data-ttu-id="5284c-144">加入新 workernodes toohello 叢集透過調整規模作業時，會套用保存的指令碼。</span><span class="sxs-lookup"><span data-stu-id="5284c-144">Persisted scripts are applied when new workernodes are added toohello cluster through scaling operations.</span></span> |

> [!NOTE]
> <span data-ttu-id="5284c-145">您必須將此指令碼標示為保存套用 tooan 現有叢集時。</span><span class="sxs-lookup"><span data-stu-id="5284c-145">You must mark this script as persisted when applying tooan existing cluster.</span></span> <span data-ttu-id="5284c-146">否則，任何透過調整作業建立新的節點將使用 hello 預設修補排程。</span><span class="sxs-lookup"><span data-stu-id="5284c-146">Otherwise, any new nodes created through scaling      operations will use hello default patching schedule.</span></span>
<span data-ttu-id="5284c-147">如果您套用 hello 指令碼做為 hello 叢集建立程序的一部分，它會自動保存。</span><span class="sxs-lookup"><span data-stu-id="5284c-147">If you apply hello script as part of hello cluster creation process, it is persisted automatically.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="5284c-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5284c-148">Next steps</span></span>

<span data-ttu-id="5284c-149">針對特定的步驟，需使用 hello 指令碼動作，請參閱下列各節中 hello hello[使用指令碼動作以自訂 Linuz 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md):</span><span class="sxs-lookup"><span data-stu-id="5284c-149">For specific steps on using hello script action, see hello following sections in hello [Customize Linuz-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md):</span></span>

* [<span data-ttu-id="5284c-150">在建立叢集期間使用指令碼動作</span><span class="sxs-lookup"><span data-stu-id="5284c-150">Use a script action during cluster creation</span></span>](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation)
* [<span data-ttu-id="5284c-151">適用於執行叢集的指令碼動作 tooa</span><span class="sxs-lookup"><span data-stu-id="5284c-151">Apply a script action tooa running cluster</span></span>](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster)
