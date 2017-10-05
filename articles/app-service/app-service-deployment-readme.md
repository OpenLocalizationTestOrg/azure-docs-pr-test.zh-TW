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
# <a name="azure-app-service-deployment-overview"></a><span data-ttu-id="ee614-104">Azure App Service 部署概觀</span><span class="sxs-lookup"><span data-stu-id="ee614-104">Azure App Service Deployment Overview</span></span>
<span data-ttu-id="ee614-105">Azure App Service 提供豐富且整合的功能集，可支援建立功能強大且靈活的部署工作流程。</span><span class="sxs-lookup"><span data-stu-id="ee614-105">Azure App Service provides a rich and integrated feature set to support creating powerful and flexible deployment workflows.</span></span> <span data-ttu-id="ee614-106">部署應用程式可以利用的選項包括連續整合或本機來源控制發佈、WebDeploy 和 FTP。</span><span class="sxs-lookup"><span data-stu-id="ee614-106">App deployment can leverage options that include continuous integration or local source control publishing, WebDeploy, and FTP.</span></span> <span data-ttu-id="ee614-107">生產應用程式部署的建議方法是部署位置交換。</span><span class="sxs-lookup"><span data-stu-id="ee614-107">The recommended method for production app deployment is deployment slot swap.</span></span> <span data-ttu-id="ee614-108">部署位置代表與生產應用程式相關聯的臨時區域與整合環境。</span><span class="sxs-lookup"><span data-stu-id="ee614-108">Deployment slots represent staging and integration environments associated with production apps.</span></span> <span data-ttu-id="ee614-109">可以設定部署位置並以 Web 流量為目標以進行驗證，並且可以依部署至生產環境的需求而交換流量，而不需停機及自動準備。</span><span class="sxs-lookup"><span data-stu-id="ee614-109">Deployment slots can be configured and targeted with web traffic for validation, and traffic can be swapped on demand for deployment to production with no down time and automated warm-up.</span></span> <span data-ttu-id="ee614-110">透過發行管理產品 (例如 Visual Studio 發行管理)，可以輕鬆地自動化部署工作流程的步驟。</span><span class="sxs-lookup"><span data-stu-id="ee614-110">The steps of a deployment workflow can be easily automated via release management products such as Visual Studio Release Management.</span></span> <span data-ttu-id="ee614-111">對於協調與其他解決方案資源 (例如資料存放區)、循環和跨多個單位部署的複寫而言，這很實用。</span><span class="sxs-lookup"><span data-stu-id="ee614-111">This is useful for coordination with other solution resources (e.g. data store), recurrence, and replication across multiple units of deployment.</span></span> 

[!INCLUDE [app-service-blueprint-deployment](../../includes/app-service-blueprint-deployment.md)]

