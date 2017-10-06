---
title: "aaaCustomize Hadoop 叢集以提供 hello 資料科學的小組流程 |Microsoft 文件"
description: "自訂 Azure HDInsight Hadoop 叢集中提供熱門 Python 模組。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0c115dca-2565-4e7a-9536-6002af5c786a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e192542dd39f71bccbb5163382b4050d0f12ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-hello-team-data-science-process"></a>自訂 hello 小組資料科學程序的 Azure HDInsight Hadoop 叢集
本文說明如何安裝 64 位元 Anaconda (Python 2.7) toocustomize HDInsight Hadoop 叢集每個節點上 hello 叢集佈建為 HDInsight 服務時。 它也會示範如何 tooaccess hello toosubmit 自訂工作 toohello 叢集中前端節點。 這項自訂許多熱門 Python 模組，隨附於 Anaconda，方便用於使用者定義的函數 (Udf) 是設計 tooprocess hello 叢集中的 Hive 記錄。 在此案例中使用的 hello 程序的指示，請參閱[如何 toosubmit Hive 查詢](machine-learning-data-science-move-hive-tables.md#submit)。

hello 下列功能表連結，說明如何設定 hello tooset 各種資料科學環境使用 hello tootopics[小組資料科學程序 (TDSP)](data-science-process-overview.md)。

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <a name="customize"></a>自訂 Azure HDInsight Hadoop 叢集
toocreate 自訂 HDInsight Hadoop 叢集中，啟動登入太[**Azure 傳統入口網站**](https://manage.windowsazure.com/)，按一下 **新增**hello 留在底端的角，，，然後選取 [資料服務-> [HDINSIGHT]-> [**自訂建立**向上 hello toobring**叢集詳細資料**視窗。 

![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

輸入 hello hello 叢集 toobe 組態頁面 1，建立名稱，並接受預設值為 hello 其他欄位。 按一下 hello 箭號 toogo toohello 下一個組態頁面。 

![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

在組態 頁面 2 輸入 hello 數目**資料節點**，選取 hello**地區/虛擬網路**，選取 hello 大小的 hello**前端節點**和 hello **資料節點**。 按一下 hello 箭號 toogo toohello 下一個組態頁面。

> [!NOTE]
> hello**地區/虛擬網路**具有 toobe hello 相同為 hello hello 即將 toobe hello HDInsight Hadoop 叢集中使用的儲存體帳戶的區域。 否則，在 hello 第四個組態頁面中，hello 儲存體帳戶不會出現在下拉式清單中的 hello**帳戶名稱**。
> 
> 

![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

在設定第 3 頁，提供使用者名稱和密碼 hello HDInsight Hadoop 叢集。 **不這麼做**選取 hello *Enter hello Hive/Oozie 中繼存放區*。 然後，按一下 hello 箭號 toogo toohello 下一個組態頁面。 

![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

設定第 4 頁，指定 hello 儲存體帳戶名稱，hello HDInsight Hadoop 叢集中的 hello 預設容器。 如果您選取*建立預設容器*在 hello**預設容器**下拉式清單中，以 hello 容器相同的名稱，將會建立 hello 叢集。 按一下 hello 箭號 toogo toohello 最後一個組態頁面。

![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

在最終的 hello**指令碼動作**組態] 頁面上，按一下 [**加入指令碼動作**按鈕，然後填入下列值的 hello 的 hello 文字欄位。

* **名稱**-hello 名稱，此指令碼動作的任何字串
* **節點類型** - 選取 [所有節點]
* **指令碼 URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1* 
  * *publicscripts*是 hello 儲存體帳戶中的公用容器 
  * *getgoing*我們在 Azure 中使用 tooshare PowerShell 指令碼檔案 toofacilitate 使用者的工作
* **PARAMETERS** - (保留空白)

最後，按一下 hello 核取記號 toostart hello 建立自訂的 hello HDInsight Hadoop 叢集。 

![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <a name="headnode"></a>存取 hello 的 Hadoop 叢集前端節點
您可以透過 RDP 存取 hello hello Hadoop 叢集前端節點之前，您必須啟用 Azure 中的遠端存取 toohello Hadoop 叢集。 

1. 登入 toohello [ **Azure 傳統入口網站**](https://manage.windowsazure.com/)，選取**HDInsight** hello 左側從 hello 群集清單選取 Hadoop 叢集，請按一下 hello **組態**索引標籤，然後再按一下 [hello**啟用遠端**在 hello hello 頁面底部的圖示。
   
    ![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. 在 hello**設定遠端桌面**視窗中，輸入 hello 使用者名稱和密碼欄位，並選取 遠端存取的 hello 到期日。 然後按一下 hello 核取記號 tooenable hello 遠端存取 toohello 前端節點的 hello Hadoop 叢集。
   
    ![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> hello 使用者名稱和密碼 hello 遠端存取的不 hello 使用者名稱和密碼，讓您用於建立 hello Hadoop 叢集時。 這是另一組個別的認證。 同時，hello 的 hello 遠端存取的到期日必須 toobe 7 天內從 hello 目前的日期。
> 
> 

啟用遠端存取之後，請按一下**連接**底部 hello hello 頁面 tooremote hello 前端節點。 您輸入您稍早指定的 hello 遠端存取使用者的 hello 認證登入 toohello hello Hadoop 叢集前端節點。

![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

hello hello 進階分析程序中的下一個步驟中的對應 hello[小組資料科學程序 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) ，而且可能包括將資料移入 HDInsight，然後處理以及它那里範例中學習 hello 資料的準備步驟使用 Azure Machine Learning 中。

請參閱[如何 toosubmit Hive 查詢](machine-learning-data-science-move-hive-tables.md#submit)如需有關如何 tooaccess hello Anaconda 中包含從 hello 中使用者定義函數 (Udf 所使用的 tooprocess) 的 hello 叢集前端節點的 Python 模組指示 hive 控制檔儲存的記錄hello 叢集中。

