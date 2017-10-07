---
title: "aaaAzure Advisor 效能建議 |Microsoft 文件"
description: "使用您的 Azure 部署的 Advisor toooptimize hello 效能。"
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
ms.openlocfilehash: eb3d928664717f6f322132ac740f42015f56b76e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-performance-recommendations"></a>建議程式效能建議

Azure Advisor 效能建議可協助改善 hello 速度和業務關鍵應用程式的回應性。 您可以從建議程式取得效能建議上 hello**效能**hello Advisor 儀表板 索引標籤。

![建議程式效能索引標籤](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a>使用 SQL DB Advisor 來改善資料庫效能

建議程式可針對所有的 Azure 資源提供一致的合併建議檢視。 它可以整合與 SQL Database Advisor toobring 您改善您的 SQL Azure database 的 hello 效能的建議。 SQL Database Advisor 會透過 SQL Azure 資料庫的 hello 效能分析您的使用記錄。 然後，它會提供最適合用於執行 hello 資料庫的一般工作負載的建議。 

> [!NOTE]
> tooget 建議資料庫還需要大約一週的使用方式，而且該星期內必須是某個一致的活動。 相較於隨機蹦出的活動，一致的查詢模式更有利於 SQL Database Advisor 最佳化。

如需 SQL Database Advisor 的詳細資訊，請參閱 [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/)。

![SQL Database 建議](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a>改善 Redis 快取的效能和可靠性

Advisor 會識別高記憶體使用量、伺服器負載、網路頻寬或大量用戶端連線會對其效能造成負面影響的 Redis 快取執行個體。 Advisor 也會提供最佳做法建議 toohelp 避免潛在的問題。 如需 Redis 快取建議的詳細資訊，請參閱 [Redis 快取建議程式](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor)。


## <a name="improve-app-service-performance-and-reliability"></a>改善 App Service 的效能和可靠性

Azure 建議程式整合了最佳作法建議，以供提升應用程式服務體驗和探索相關的平台功能。 應用程式服務建議的範例如下︰
* 偵測應用程式執行階段與緩和選項已耗盡記憶體或 CPU 資源的執行個體。
* 偵測共置資源 (如 Web 應用程式和資料庫) 可改善效能並降低成本的執行個體。 

如需應用程式服務建議的詳細資訊，請參閱 [Azure App Service 的最佳作法](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/)。
![應用程式服務建議](./media/advisor-performance-recommendations/advisor-performance-app-service.png)

## <a name="how-tooaccess-performance-recommendations-in-advisor"></a>如何 tooaccess Advisor 中的效能建議

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。

2. 在 hello 左窗格中，按一下 **更多服務**。

3. 在 hello 服務功能表窗格底下**監視及管理**，按一下  **Azure Advisor**。  
 hello Advisor 儀表板會顯示。

4. 在 hello Advisor 儀表板上按一下 hello**效能** 索引標籤。

5. 選取 hello 訂用帳戶，您想 tooreceive 建議，然後按一下**取得建議**。

> [!NOTE]
> tooaccess Advisor 的建議，您必須先*註冊您的訂閱*與 Advisor。 已經註冊訂閱時*訂用帳戶擁有者*啟動 hello Advisor 儀表板，並按一下 hello**取得建議** 按鈕。 此作業「只需要執行一次」。 Hello 訂用帳戶註冊之後，您可以存取 Advisor 的建議做為*擁有者*，*參與者*，或*讀取器*訂用帳戶，資源群組，或特定的資源。

## <a name="next-steps"></a>後續步驟

toolearn 深入了解 Advisor 的建議，請參閱：

* [簡介 tooAdvisor](advisor-overview.md)
* [開始使用建議程式](advisor-get-started.md)
* [建議程式成本建議](advisor-performance-recommendations.md)
* [建議程式高可用性建議](advisor-high-availability-recommendations.md)
* [建議程式安全性建議](advisor-security-recommendations.md)

