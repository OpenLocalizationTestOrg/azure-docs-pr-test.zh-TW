---
title: "Azure 資料科學虛擬機器做為 IPython 筆記型電腦伺服器 aaaProvision |Microsoft 文件"
description: "使用支援的工具，將資料科學虛擬機器佈建為 IPython Notebook 伺服器。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 95e1fa87-794a-4d03-80a4-af4f3f3ac31e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 7c0abcbcb822918332f76a9f16690a72b90f4b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="provision-azure-data-science-virtual-machines-as-ipython-notebook-servers"></a>將 Azure 資料科學虛擬機器佈建為 IPython Notebook 伺服器
這裡描述係指示如何 tooset Azure VM 和 Azure VM 與 SQL 服務做為 IPython 筆記型電腦伺服器。 hello Windows 虛擬機器設定有支援 IPython 筆記型電腦、 Azure 儲存體總管 中，和 AzCopy，以及其他公用程式可用於資料科學專案之類的工具。 Azure 儲存體總管和 AzCopy，比方說，提供方便的方式從您的本機電腦或 toodownload tooupload 資料 tooAzure 儲存它 tooyour 從儲存體的本機電腦。 

這個功能表連結，說明如何設定 hello tooset 各種資料科學環境使用 hello tootopics[小組資料科學程序 (TDSP)](data-science-process-overview.md)。

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

Azure 虛擬機器的數種可以佈建，而且設定 toobe 做為雲端架構資料科學環境的一部分。 hello 決定哪一個類別的虛擬機器的相關 toouse，取決於 hello 類型和數量的資料 toobe 模型化機器學習，與該資料 hello 雲端中的 hello 目標目的地。 

* 如需 hello 問題 tooconsider 時進行這項決策的指引，請參閱[計劃 Azure 機器學習資料科學環境](machine-learning-data-science-plan-your-environment.md)。 
* 針對某些狀況 hello 進行進階的分析時，可能會遇到的目錄，請參閱[案例 hello 進階分析程序和 Azure Machine Learning 中的技術](machine-learning-data-science-plan-sample-scenarios.md)

提供兩組指示：

* [將 Azure 虛擬機器設定進階分析的 IPython 筆記型電腦伺服器](machine-learning-data-science-setup-virtual-machine.md)tooprovision IPython 筆記型電腦及其他工具與 Azure 虛擬機器的情況使用 toodo 資料科學的方式會顯示一種 SQL 以外的 Azure 儲存體可以是使用的 toostore hello 資料。
* [Azure SQL Server 虛擬機器設定為執行進階分析 IPython 筆記型電腦伺服器](machine-learning-data-science-setup-sql-server-virtual-machine.md)tooprovision IPython 筆記型電腦及其他工具與 Azure SQL Server 虛擬機器的情況使用 toodo 資料科學的方式會顯示 SQL 資料庫可以是使用的 toostore hello 資料。

一旦佈建和設定，這些虛擬機器做為 IPython 筆記型電腦伺服器 hello 瀏覽和處理的資料，以及與 Azure 機器學習和 hello 小組資料科學程序 (TDSP) 搭配使用所需的其他工作就可供使用。 hello hello 資料科學程序中的下一個步驟中的對應 hello [TDSP 學習路徑](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)，而且可能包括移動到 SQL Server 或 HDInsight 的資料處理和範例並準備學習 hello 資料與 Azure 中的步驟機器學習。

> [!NOTE]
> Azure 虛擬機器的定價策略是「 **只針對您使用的項目進行付費**」。 不會的 tooensure 時不使用虛擬機器，則需要付費，它具有 toobe 中的 hello**已停止 （取消配置）**狀態從 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)。 如需逐步指示或如何 toodeallocate 您虛擬機器，請參閱[關閉及取消配置虛擬機器在不使用時](machine-learning-data-science-setup-virtual-machine.md#shutdown)
> 
> 

