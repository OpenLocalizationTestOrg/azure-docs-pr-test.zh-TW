---
title: "App Service 概觀：Azure Stack | Microsoft Docs"
description: "Azure Stack 上的 App Service 概觀"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: anwestg
ms.openlocfilehash: 1d763f592212b3a2dcc2f03ebe317eed84e9e2de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-on-azure-stack-overview"></a>Azure Stack 概觀上的 App Service

Azure 堆疊上的 azure App Service 為 hello Azure 帶來的供應項目 tooAzure 堆疊。 hello 應用程式服務在 Azure 堆疊安裝程式會建立下列角色的執行個體的 hello:

*  Controller
*  管理 (會建立兩個執行個體)
*  FrontEnd
*  發佈者
*  背景工作 (處於共用模式)

此外，hello 應用程式服務在 Azure 堆疊安裝程式會建立檔案伺服器。
    
## <a name="whats-new-in-hello-first-release-candidate-of-app-service-on-azure-stack"></a>什麼是 hello 第一個發行候選版本的 Azure 堆疊上的應用程式服務的新功能？
![Hello Azure 堆疊入口網站中的應用程式服務][1]

hello 第一個發行候選版本的 Azure 堆疊上的應用程式服務建置在 hello 第三個 preview 之上，並使新的功能與改良功能：

* 以 Active Directory 同盟服務為基礎之 Azure Stack 環境中的 Azure Functions 
* 單一登入支援 hello 函式的入口網站和 hello 進階開發人員工具 (Kudu)
* 適用於 Web、行動裝置版和 API 應用程式的 Java 支援
* 背景工作層的虛擬機器規模管理服務系統管理員設定 tooimprove 擴充功能
* 當地語系化的 hello 系統管理員體驗
* Hello 服務的更高的穩定性
* 租用戶入口網站體驗更新及安裝程序更新

## <a name="limitations-of-hello-technical-preview"></a>Hello technical preview 的限制

雖然我們不要監視 hello Azure 堆疊 MSDN 論壇沒有 hello 應用程式服務在 Azure 堆疊預覽版本中，支援。 請勿將生產工作負載放在此預覽版本上。 Azure Stack 上的 App Service 預覽版本之間也沒有任何升級。 hello 這些預覽版本的主要目的是 tooshow 什麼我們提供和 tooobtain 意見反應。 

## <a name="what-is-an-app-service-plan"></a>什麼是 App Service 方案？

hello 應用程式服務資源提供者會使用相同的程式碼，會使用 Azure App Service 的 hello。 因此，有些通用概念值得一提。 在應用程式服務定價應用程式容器中的 hello 稱為 hello 應用程式服務方案。 它代表使用專用的虛擬機器 toohold hello 組您的應用程式。 在指定訂用帳戶內，您可以有多個 App Service 方案。 

在 Azure 中，有共用和專用背景工作。 共用背景工作支援裝載高密度的多租用戶應用程式，而且只有一組共用背景工作。 專用伺服器只可供一個租用戶使用且分成三種大小：小型、中型和大型。 在內部部署客戶的 hello 需求永遠無法使用這些詞彙所述。 在 Azure 堆疊上的應用程式服務，資源提供者系統管理員可以定義他們想要使用 toomake hello 背景工作層。 系統管理員可以根據其獨特的裝載需求，來定義多組共用背景工作或不同的專用背景工作組。 透過使用這些背景工作層定義，他們接著就能定義自己的定價 SKU。

## <a name="portal-features"></a>入口網站功能

Azure 堆疊上的應用程式服務會使用相同的 UI，Azure 應用程式服務所使用，如為 true 以 hello 回結束的 hello。 某些功能已停用且無法在 Azure Stack 中運作。 hello Azure 特有的期望，或服務，這些功能都需要尚無法使用 Azure 堆疊中。 

## <a name="next-steps"></a>後續步驟

- [開始使用 Azure Stack 上的 App Service 之前](azure-stack-app-service-before-you-get-started.md)
- [安裝 hello 應用程式服務資源提供者](azure-stack-app-service-deploy.md)

您也可以嘗試出其他[平台即服務 (PaaS) 服務](azure-stack-tools-paas-services.md)，像是 hello [SQL Server 資源提供者](azure-stack-sql-resource-provider-deploy.md)和 hello [MySQL 資源提供者](azure-stack-mysql-resource-provider-deploy.md)。

<!--Image references-->
[1]: ./media/azure-stack-app-service-overview/AppService_Portal.png
