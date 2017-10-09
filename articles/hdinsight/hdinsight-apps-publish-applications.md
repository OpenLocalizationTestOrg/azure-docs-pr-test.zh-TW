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
# <a name="publish-hdinsight-applications-into-hello-azure-marketplace"></a>發行到 hello Azure Marketplace 的 HDInsight 應用程式
HDInsight 應用程式是使用者可以在以 Linux 為基礎的 HDInsight 叢集上安裝的應用程式。 Microsoft 獨立軟體廠商 (ISV) 或您可以自己開發這些應用程式。 在本文中，您將學習如何 toopublish hello Azure Marketplace 將 HDInsight 應用程式。  如需身分資料發佈至 hello Azure Marketplace 的一般資訊，請參閱[發佈供應項目 toohello Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md)。

HDInsight 應用程式使用 hello*攜帶您自己授權 (BYOL)*模型，其中應用程式提供者會負責授權 hello 應用程式 tooend 位使用者，而使用者只需要付費 azure hello 資源它們建立，例如 hello HDInsight 叢集和 Vm/節點。 目前，計費 hello 應用程式本身不是透過 Azure。

其他 HDInsight 應用程式相關文章︰

* [安裝的應用程式 HDInsight](hdinsight-apps-install-applications.md)： 了解如何 tooinstall HDInsight 應用程式 tooyour 叢集。
* [安裝自訂 HDInsight 應用程式](hdinsight-apps-install-custom-applications.md)： 了解如何 tooinstall 和測試自訂 HDInsight 應用程式。

## <a name="prerequisites"></a>必要條件
toosubmit 您自訂的應用程式的 toohello marketplace，您必須已建立並測試自訂應用程式。 請參閱下列文章 hello:

* [安裝自訂 HDInsight 應用程式](hdinsight-apps-install-custom-applications.md)： 了解如何 tooinstall 和測試自訂 HDInsight 應用程式。

您還必須註冊開發人員帳戶。 請參閱[發佈供應項目 toohello Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md)和[建立 Microsoft 開發人員帳戶](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md)。

## <a name="define-application"></a>定義應用程式
有兩個步驟來發行應用程式 toohello Azure Marketplace。  先定義**createUiDef.json**檔案 tooindicate 的叢集，您的應用程式與; 相容，而且您應發佈 hello Azure 入口網站中的 hello 範本。 下列章節的 hello 是範例 createUiDef.json 檔案。

    {
        "handler": "Microsoft.HDInsight",
        "version": "0.0.1-preview",
        "clusterFilters": {
            "types": ["Hadoop", "HBase", "Storm", "Spark"],
            "tiers": ["Standard", "Premium"],
            "versions": ["3.4"]
        }
    }


| 欄位 | 描述 | 可能的值 |
| --- | --- | --- |
| types |hello 叢集 hello 應用程式是與相容的類型。 |Hadoop、HBase、Storm、Spark (或這些類型的任意組合) |
| tiers |hello hello 應用程式為相容於叢集層。 |Standard、Premium (或兩者) |
| versions |hello hello 應用程式是與相容的 HDInsight 叢集類型。 |3.4 |

## <a name="application-install-script"></a>應用程式安裝指令碼
每當應用程式已安裝在叢集上 （為現有或新的），建立邊緣節點和 hello 應用程式安裝指令碼在其上執行。
  > [!IMPORTANT]
  > 以下列格式的 hello，hello 名稱 hello 應用程式安裝指令碼名稱必須是特定叢集的唯一的。
  > 
  > name": "[concat('hue-install-v0','-' ,uniquestring(‘applicationName’)]"
  > 
  > 請注意有三個部分 toohello 指令碼名稱：
  > 
  > 1. 指令碼名稱前置詞，都應該包括 hello 應用程式名稱相關 toohello 應用程式。
  > 2. "-" 以方便閱讀。
  > 3. Hello 應用程式名稱為 hello 參數的唯一字串的函式。
  > 
  > 例如，上述的 hello 最後會變得： 色調-安裝-v0-4wkahss55hlas hello 中保存的指令碼動作清單。 如需 JSON 承載的範例，請參閱 [https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json](https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json)。
  > 
hello 安裝指令碼必須具有下列特性的 hello:
1. 請確定 hello 指令碼具有等冪性。 Toohello 指令碼應該會產生多個呼叫 hello 相同的結果。
2. hello 指令碼應該是正確版本。 當您升級或測試變更，讓客戶嘗試 tooinstall hello 應用程式不會受到影響，請使用不同的位置 hello 指令碼。 
3. 新增適當的記錄 toohello 指令碼，在每個點。 通常 hello 指令碼記錄檔是唯一的方式 toodebug hello 應用程式安裝問題。
4. 請確定呼叫 tooexternal 服務或資源有足夠的重試以便 hello 安裝不會受到暫時性網路問題。
5. 如果您的指令碼 hello 節點上啟動服務，請確定會監視和設定會自動發生節點重新開機時 toostart hello 服務。

## <a name="package-application"></a>封裝應用程式
建立 zip 檔案，其中包含安裝 HDInsight 應用程式時的所有必要檔案。 您需要 hello zip 檔案中的[發行應用程式](#publish-application)。

* [createUiDefinition.json](#define-application)。
* mainTemplate.json。 請參閱[安裝自訂 HDInsight 應用程式](hdinsight-apps-install-custom-applications.md)中的範例。
* 所有必要的指令碼。

> [!NOTE]
> hello 應用程式檔案 （如果有的話，包含 web 應用程式檔案） 可以位於任何可公開存取的端點。
> 

## <a name="publish-application"></a>發佈應用程式
請遵循下列步驟 toopublish HDInsight 應用程式的 hello:

1. 登入 toohello [Azure 發行入口網站](https://publish.windowsazure.com/)。
2. 按一下**解決方案範本**從 hello 左 toocreate 新的方案範本。
3. 輸入標題，然後按一下建立新的方案範本。
4. 按一下**建立開發人員中心帳戶和聯結 hello Azure 程式**tooregister 公司如果您尚未這樣做。  請參閱 [建立 Microsoft 開發人員帳戶](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md)。
5. 按一下**定義一些拓撲 tooget 已啟動**。 方案範本是 「 父 」 tooall 其拓撲。 您可以在一個供應項目/解決方案範本中定義多個拓撲。 當 toostaging 推入的供應項目時，它是推入與所有其拓撲。 
6. 輸入拓撲名稱，，，然後按一下hello 加號。
7. 輸入新的版本，，然後按一下hello 加號。
8. 上傳 hello zip 檔案中準備[應用程式封裝](#package-application)。  
9. 按一下 [要求認證]。 hello Microsoft 認證小組將檢閱 hello 檔案，並證實 hello 拓撲。

## <a name="next-steps"></a>後續步驟
* [安裝的應用程式 HDInsight](hdinsight-apps-install-applications.md)： 了解如何 tooinstall HDInsight 應用程式 tooyour 叢集。
* [安裝自訂 HDInsight 應用程式](hdinsight-apps-install-custom-applications.md)： 了解如何 toodeploy 未發行的 HDInsight 應用程式 tooHDInsight。
* [自訂使用指令碼動作以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)： 了解如何 toouse 指令碼動作 tooinstall 其他應用程式。
* [使用 Azure Resource Manager 範本 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集](hdinsight-hadoop-create-linux-clusters-arm-templates.md)： 了解如何 toocall 資源管理員範本 toocreate HDInsight 叢集。
* [使用 HDInsight 中的空白邊緣節點](hdinsight-apps-use-edge-node.md)： 了解如何 toouse 空白邊緣節點存取 HDInsight 叢集、 測試 HDInsight 應用程式，以及裝載 HDInsight 應用程式。

