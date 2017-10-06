---
title: "Azure App Service：調整 App Service 應用程式"
description: "了解 hello 內外的應用程式服務中調整應用程式。"
keywords: "App Service, Azure App Service, 級別, 可調整, App Service方案, App Service 成本"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: f403c971-4450-432b-8cea-3eeb426c0147
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: byvinyal
ms.openlocfilehash: d8cd12f73915a916a75d46da2f751a40d567b189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a>Azure App Service：調整 App Service 應用程式
在 Azure App Service 中裝載的應用程式可以達到最大規模 [Canadian Broadcasting Corporation/Radio-Canada leverage Azure for smooth election coverage (加拿大廣播公司/加拿大廣播電台運用 Azure 處理大選新聞)](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/)。
不過，調整應用程式是很複雜的問題，沒有所謂的「一體適用」方案。 toocorrectly 調整應用程式有 3 會導致 tooyour 應用程式成功的主要區域：

1. 了解您的應用程式架構和其缺點。
   * 您的應用程式是否可設定狀態？ 沒有狀態？
   * 應用程式的所有 hello 元件有哪些都？
     * Hello 應用程式中的 hello 瓶頸哪裡？
   * 套用的 tooyour 應用程式負載時，功能將會中斷第一個項目？
2. 了解 hello 預期負載和效能需求。
   * Hello 應用程式需要 tooserve 一千使用者嗎？或一百萬嗎？
   * 流量是來自單一地區或全球？
   * 是否有季節性變化及流量尖峰？
   * 應該多快回應 hello 應用程式？ 1 秒？ 1 毫秒？
3. 了解及正確運用 hello 平台裝載您的應用程式。
   * 功能的應該我運用 tooachieve 我小數位數的目標嗎？

本章節將協助您了解所有 hello 因素以及協助您設計策略，會利用 hello 必要應用程式服務功能 tooachieve 延展性目標。

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

