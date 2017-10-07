---
title: "aaaDeploying 應用程式 tooAzure 應用程式服務"
description: "了解 tooDeploy 應用程式 tooApp 服務如何運作"
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
ms.openlocfilehash: 925341e12daf3cb05b25199f5c5218e82f062f70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-deployment-overview"></a><span data-ttu-id="609e7-104">Azure App Service 部署概觀</span><span class="sxs-lookup"><span data-stu-id="609e7-104">Azure App Service Deployment Overview</span></span>
<span data-ttu-id="609e7-105">Azure App Service 提供豐富並整合的功能集 toosupport 建立功能強大且彈性的部署工作流程。</span><span class="sxs-lookup"><span data-stu-id="609e7-105">Azure App Service provides a rich and integrated feature set toosupport creating powerful and flexible deployment workflows.</span></span> <span data-ttu-id="609e7-106">部署應用程式可以利用的選項包括連續整合或本機來源控制發佈、WebDeploy 和 FTP。</span><span class="sxs-lookup"><span data-stu-id="609e7-106">App deployment can leverage options that include continuous integration or local source control publishing, WebDeploy, and FTP.</span></span> <span data-ttu-id="609e7-107">hello 建議的部署位置交換的實際執行應用程式部署方法。</span><span class="sxs-lookup"><span data-stu-id="609e7-107">hello recommended method for production app deployment is deployment slot swap.</span></span> <span data-ttu-id="609e7-108">部署位置代表與生產應用程式相關聯的臨時區域與整合環境。</span><span class="sxs-lookup"><span data-stu-id="609e7-108">Deployment slots represent staging and integration environments associated with production apps.</span></span> <span data-ttu-id="609e7-109">部署位置可設定與驗證的 web 流量的目標和流量可以切依需求對部署 tooproduction，而不需要停機，並自動準備。</span><span class="sxs-lookup"><span data-stu-id="609e7-109">Deployment slots can be configured and targeted with web traffic for validation, and traffic can be swapped on demand for deployment tooproduction with no down time and automated warm-up.</span></span> <span data-ttu-id="609e7-110">透過發行管理產品，例如 Visual Studio Release Management，可以輕鬆地自動化 hello 步驟部署工作流程。</span><span class="sxs-lookup"><span data-stu-id="609e7-110">hello steps of a deployment workflow can be easily automated via release management products such as Visual Studio Release Management.</span></span> <span data-ttu-id="609e7-111">對於協調與其他解決方案資源 (例如資料存放區)、循環和跨多個單位部署的複寫而言，這很實用。</span><span class="sxs-lookup"><span data-stu-id="609e7-111">This is useful for coordination with other solution resources (e.g. data store), recurrence, and replication across multiple units of deployment.</span></span> 

[!INCLUDE [app-service-blueprint-deployment](../../includes/app-service-blueprint-deployment.md)]

