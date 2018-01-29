---
title: "在 Azure 中設定資料科學環境 | Microsoft Docs"
description: "在 Azure 上設定用於 Team Data Science Process 中的資料科學環境。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: cgronlun
editor: cgronlun
ms.assetid: 481cfa6a-7ea3-46ac-b0f9-2e3982c37153
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2017
ms.author: bradsev
ms.openlocfilehash: 96139523cd2440c801230b62abf9c9b56ec15e83
ms.sourcegitcommit: 5a6e943718a8d2bc5babea3cd624c0557ab67bd5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="set-up-data-science-environments-for-use-in-the-team-data-science-process"></a>設定用於 Team Data Science Process 中的資料科學環境
Team Data Science Process 使用各種資料科學環境來儲存、處理和分析資料。 他們包含 Azure Blob 儲存體、數種類型的 Azure 虛擬機器、HDInsight (Hadoop) 叢集，以及 Azure Machine Learning 工作區。 要使用哪一個環境，取決於要進行模型化的資料類型和數量，以及該資料在雲端中的目標目的地。 

* 如需進行這項決策時要考量之問題的指引，請參閱[規劃您的 Azure Machine Learning 資料科學環境](plan-your-environment.md)。 
* 如需在進行進階分析時可能會遇到的部分案例目錄，請參閱 [適用於 Team Data Science Process 的案例](plan-sample-scenarios.md)

此功能表所連結的主題會說明如何設定 Team Data Science Process 所用的各種資料科學環境。

[!INCLUDE [data-science-environment-setup](../../../includes/cap-setup-environments.md)]

**Microsoft 資料科學虛擬機器 (DSVM)** 也以 Azure 虛擬機器 (VM) 映像形式提供。 此 VM 會預先安裝並且以數個常用於資料分析和機器學習服務的熱門工具進行設定。 DSVM 可用於 Windows 和 Linux。 如需進一步資訊，請參閱[適用於 Linux 和 Windows 的雲端型資料科學虛擬機器簡介](../data-science-virtual-machine/overview.md)。

