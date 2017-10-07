---
title: "aaaAzure Advisor 成本建議 |Microsoft 文件"
description: "使用您的 Azure 部署的 Azure Advisor toooptimize hello 成本。"
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 50f70c33a17f550c8753795435cdfddd51e409f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-cost-recommendations"></a>建議程式成本建議

建議程式可找出閒置和未充分利用的資源，協助您最佳化並減少 Azure 整體費用。 您可以取得成本建議 hello**成本**hello Advisor 儀表板上的索引標籤。

![Advisor [成本] 索引標籤](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a>將未充分利用的執行個體調整大小以最佳化虛擬機器費用 
雖然某些應用程式的情況下可能會導致低使用率所設計，您通常可以藉由管理您的虛擬機器的 hello 大小與數目來節省成本。 Advisor 可監視 14 天的虛擬機器使用量，然後找出低使用率的虛擬機器。 CPU 使用率等於或低於 5% 且網路使用量等於或低於 7 MB 長達 4 天 (含) 以上的虛擬機器，會被視為低使用率虛擬機器。

Advisor 顯示，讓您可以選擇的 tooshut 它向下或調整其大小，hello 再 toorun 繼續您的虛擬機器的估計的成本。  

![調整虛擬機器大小的建議程式成本建議](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-toomanage-performance-goals-of-multiple-sql-databases"></a>使用多個 SQL database 的成本效益的解決方案 toomanage 效能目標
建議程式會找出可受益於建立彈性資料庫集區的 SQL Server 執行個體。 彈性資料庫集區提供簡單且符合成本效益的解決方案 toomanage hello 效能目標的多個具有不同的使用方式模式的資料庫。 如需 Azure 彈性集區的詳細資訊，請參閱[什麼是 Azure 彈性集區？](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/)。

![彈性資料庫集區的建議程式成本建議](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-tooaccess-cost-recommendations-in-azure-advisor"></a>Tooaccess 成本中 Azure Advisor 建議的方式

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。

2. 在 hello 左窗格中，按一下 **更多服務**。

3. 在 hello 服務功能表窗格底下**監視及管理**，按一下  **Azure Advisor**。  
 hello Advisor 儀表板會顯示。

4. 在 hello Advisor 儀表板上按一下 hello**成本** 索引標籤。

5. 選取 hello 訂用帳戶，您想 tooreceive 建議，然後按一下**取得建議**。

> [!NOTE]
> tooaccess Advisor 的建議，您必須先*註冊您的訂閱*與 Advisor。 已經註冊訂閱時*訂用帳戶擁有者*啟動 hello Advisor 儀表板，並按一下 hello**取得建議** 按鈕。 此作業「只需要執行一次」。 Hello 訂用帳戶註冊之後，您可以存取 Advisor 的建議做為*擁有者*，*參與者*，或*讀取器*訂用帳戶，資源群組，或特定的資源。

## <a name="next-steps"></a>後續步驟

toolearn 深入了解 Advisor 的建議，請參閱：
* [簡介 tooAdvisor](advisor-overview.md)
* [開始使用](advisor-get-started.md)
* [建議程式效能建議](advisor-cost-recommendations.md)
* [建議程式高可用性建議](advisor-cost-recommendations.md)
* [建議程式安全性建議](advisor-cost-recommendations.md)
