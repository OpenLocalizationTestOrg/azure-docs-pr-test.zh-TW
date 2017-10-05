---
title: "將應用程式部署至 Azure App Service"
description: "了解如何將應用程式部署到 App Service 的工作"
keywords: "app service, azure app service, 部署中, 部署"
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: 
ms.assetid: de12cd6e-e124-4e48-90bc-c3a3801305da
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 347e8b5177eac8e08ab0dea701b736b86d23904a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-deployment-overview"></a>Azure App Service 部署概觀
Azure App Service 提供豐富且整合的功能集，可支援建立功能強大且靈活的部署工作流程。 部署應用程式可以利用的選項包括連續整合或本機來源控制發佈、WebDeploy 和 FTP。 生產應用程式部署的建議方法是部署位置交換。 部署位置代表與生產應用程式相關聯的臨時區域與整合環境。 可以設定部署位置並以 Web 流量為目標以進行驗證，並且可以依部署至生產環境的需求而交換流量，而不需停機及自動準備。 透過發行管理產品 (例如 Visual Studio 發行管理)，可以輕鬆地自動化部署工作流程的步驟。 對於協調與其他解決方案資源 (例如資料存放區)、循環和跨多個單位部署的複寫而言，這很實用。 

[!INCLUDE [app-service-blueprint-deployment](../../includes/app-service-blueprint-deployment.md)]

