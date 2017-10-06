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
# <a name="os-patching-for-hdinsight"></a>HDInsight 的作業系統修補 
為 managed Hadoop 服務時，會負責 HDInsight 修補 hello 作業系統的 HDInsight 叢集所使用的基礎 Vm hello。 從 2016 年 8 月 1 日開始，我們已用於以 Linux 為基礎的 HDInsight 叢集 （版本 3.4 或更新版本） 的 hello 客體 OS 修補原則。 hello hello 新的原則目標是 toosignificantly 減少重新開機次數 hello 到期 toopatching。 hello 新的原則將會繼續在 Linux 上的 toopatch 虛擬機器 (Vm) 叢集的每個星期一或星期四上午 12 utc，以交錯方式啟動任何指定的叢集節點之間。 不過，任何指定的 VM 會只重新開機一次每 30 天到期 tooguest OS 修補程式。 此外，新建立的叢集 hello 第一次重新開機不會發生更快地從 hello 叢集建立日期的 30 天前。 Hello Vm 重新開機後，修補程式就會生效。

## <a name="how-tooconfigure-hello-os-patching-schedule-for-linux-based-hdinsight-clusters"></a>如何 tooconfigure hello 以 Linux 為基礎的 HDInsight 叢集的 OS 修補排程
hello HDInsight 叢集中的虛擬機器需要 toobe 以便可以安裝重要的安全性修補程式偶爾重新開機。 從 2016 年 8 月 1 日開始新 Linux 為基礎的 HDInsight 叢集 （版本 3.4 或更多，） 會重新開機，使用下列排程 hello:

1. Hello 叢集中的虛擬機器可以只重新開機的修補程式最多 30 天期間內一次。
2. hello 重新開機，就會發生在上午 12 UTC 開始。
3. hello 重新開機程序被階段性跨 hello 叢集中的虛擬機器，因此 hello 叢集 hello 重新開機程序期間仍然可以使用。
4. hello 新建的叢集的第一次重新開機不會更快地 hello 叢集建立日期後的 30 天前發生。

使用本文中所述的 hello 指令碼動作時，您就可以修改 hello OS 修補排程，如下所示：
1. 啟用或停用自動重新開機
2. 組 hello 頻率的重新開機 （重新開機之間的天數）
3. 設定 hello 星期幾 hello 發生重新開機

> [!NOTE]
> 此指令碼動作只適用於在 2016 年 8 月 1 日之後建立的以 Linux 為基礎的 HDInsight 叢集。 VM 重新開機後，修補才會生效。 
>

## <a name="how-toouse-hello-script"></a>如何 toouse hello 指令碼 

當使用這個指令碼需要下列資訊的 hello:
1. hello 指令碼位置： https://hdiconfigactions.blob.core.windows.net/linuxospatchingrebootconfigv01/os-patching-reboot-config.sh。HDInsight 會使用此 URI toofind 和 hello 叢集中的所有 hello 虛擬機器上執行 hello 指令碼。
  
2. hello hello 指令碼套用至叢集節點型別： 叢集前端節點，workernode，動物園管理員。 此指令碼必須套用的 tooall hello 叢集中的節點型別。 如果不是套用的 tooa 節點型別，則 hello 虛擬機器，該節點型別會繼續 toouse hello 先前修補排程。


3.  參數︰此指令碼接受三個數值參數︰

    | 參數 | 定義 |
    | --- | --- |
    | 啟用/停用自動重新開機 |0 或 1。 值為 0 會停用自動重新開機，1 則會啟用自動重新開機。 |
    | 頻率 |7 too90 （含）。 hello 天 toowait 之前重新開機 hello 修補程式需要重新開機的虛擬機器數目。 |
    | 星期幾 |1 too7 （含）。 值為 1 表示 hello 重新開機應該會發生在星期一，7 表示 Sunday.For 範例中，使用參數 1 60 2 個導致自動重新啟動每隔 60 天 （最多） 個星期二。 |
    | 持續性 |當套用指令碼動作 tooan 現有叢集，您可以將 hello 指令碼標示為保存。 加入新 workernodes toohello 叢集透過調整規模作業時，會套用保存的指令碼。 |

> [!NOTE]
> 您必須將此指令碼標示為保存套用 tooan 現有叢集時。 否則，任何透過調整作業建立新的節點將使用 hello 預設修補排程。
如果您套用 hello 指令碼做為 hello 叢集建立程序的一部分，它會自動保存。
>

## <a name="next-steps"></a>後續步驟

針對特定的步驟，需使用 hello 指令碼動作，請參閱下列各節中 hello hello[使用指令碼動作以自訂 Linuz 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md):

* [在建立叢集期間使用指令碼動作](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation)
* [適用於執行叢集的指令碼動作 tooa](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster)
