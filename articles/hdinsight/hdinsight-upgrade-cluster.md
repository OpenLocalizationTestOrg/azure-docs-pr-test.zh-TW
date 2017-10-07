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
# <a name="upgrade-hdinsight-cluster-tooa-newer-version"></a>HDInsight 叢集 tooa 較新版本升級
tootake 利用 hello 最新的 HDInsight 功能，我們建議您的 HDInsight 叢集是升級的 toolatest 版本。 請遵循下列指導方針 tooupgrade hello 您的 HDInsight 叢集版本。

> [!NOTE]
> HDInsight 叢集版本 3.2 與 3.3 已接近淘汰日期。 如需支援之 HDInsight 版本的詳細資訊，請參閱 [HDInsight 元件版本](hdinsight-component-versioning.md#supported-hdinsight-versions)。
>
>

## <a name="upgrade-tasks"></a>升級工作
hello 工作流程 tooupgrade HDInsight 叢集如下所示。

![升級工作流程圖表](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. 讀取這份文件的每個區段 toounderstand 變更時，可能會需要升級您的 HDInsight 叢集。
2. 將叢集建立為測試/品質保證環境。 如需有關如何建立叢集的詳細資訊，請參閱[深入了解如何 toocreate 以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)
3. 現有的作業、 資料來源和接收器 toohello 新環境的複本。 請參閱[複製資料 tooTest 環境](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment)如需詳細資訊。
4. 執行驗證測試 toomake 確定您作業的工作，如預期般 hello 新叢集上。


一旦您已確認一切運作正常，排程 hello 移轉停機的時間。 在這個停機時間，下列動作 hello:

1.  備份儲存在本機 hello 叢集節點上的任何暫時性資料。 例如，如果您的資料是直接儲存在前端節點上。
2.  刪除 hello 現有叢集。
3.  建立叢集 hello 中相同的 VNET 子網路具有最新的 （或支援的） HDI 版本使用 hello 相同預設資料存放區的 hello 先前使用的叢集。 這可讓 hello 針對現有的實際執行資料新叢集 toocontinue。
4.  匯入任何已備份的暫時性資料。
5.  開始作業/仍會繼續處理使用 hello 新叢集。

## <a name="next-steps"></a>後續步驟
* [了解如何 toocreate 以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)
* [連接 tooHDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)
* [使用 Ambari 管理 Linux 型叢集](hdinsight-hadoop-manage-ambari.md)

