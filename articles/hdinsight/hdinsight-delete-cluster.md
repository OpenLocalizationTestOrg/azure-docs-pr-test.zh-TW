---
title: "aaaHow toodelete 的 HDInsight 叢集的 Azure |Microsoft 文件"
description: "Hello，您可以刪除 HDInsight 叢集的各種方式的資訊。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 55f7838b-9786-47ff-96db-1b64437bd0bb
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 5b9d9a09eecfdcfaed7a1f5ebab440e13bd358b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-hello-azure-cli"></a>刪除您的瀏覽器、 PowerShell 或 hello Azure CLI 所使用的 HDInsight 叢集

一旦建立叢集，並停止刪除 hello 叢集時，就會開始 HDInsight 叢集計費。 計費是以每分鐘按比例計算，因此不再使用時，請一律刪除您的叢集。 在本文件中，您學會如何叢集使用 toodelete hello Azure 入口網站、 Azure PowerShell 和 hello Azure CLI 1.0。

> [!IMPORTANT]
> 刪除 HDInsight 叢集不會刪除 hello Azure 儲存體帳戶，或與 hello 叢集相關聯的資料湖存放區。 您可以重複使用這些服務，在未來的 hello 中儲存的資料。

## <a name="azure-portal"></a>Azure 入口網站

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)並選取您的 HDInsight 叢集。 如果您的 HDInsight 叢集不是已釘選的 toohello 儀表板，您可以使用 hello 搜尋欄位來依據名稱搜尋它。
   
    ![入口網站搜尋](./media/hdinsight-delete-cluster/navbar.png)

2. 一旦 hello 刀鋒視窗中開啟 hello 叢集時，請選取 hello**刪除**圖示。 出現提示時，選取**是**toodelete hello 叢集。
   
    ![刪除圖示](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a>Azure PowerShell

從 PowerShell 提示中，使用下列命令 toodelete hello 叢集 hello:

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

取代**CLUSTERNAME** hello 名稱，為您的 HDInsight 叢集。

## <a name="azure-cli-10"></a>Azure CLI 1.0

在提示字元中使用下列 toodelete hello 叢集 hello:

    azure hdinsight cluster delete CLUSTERNAME

取代**CLUSTERNAME** hello 名稱，為您的 HDInsight 叢集。

> [!NOTE]
> Azure CLI 2.0 目前不支援刪除 HDInsight 叢集 (2017 年 7 月 31 日)。