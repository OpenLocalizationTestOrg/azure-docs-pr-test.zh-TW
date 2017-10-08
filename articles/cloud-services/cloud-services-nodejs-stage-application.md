---
title: "aaaStage 雲端服務部署 (Node.js) |Microsoft 文件"
description: "深入了解如何 toodeploy 您的 Azure 應用程式 tooa 預備環境，然後將使用虛擬 IP (VIP) 交換 tooa 生產環境部署。"
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d65d26a6-b424-49cd-a88c-7ef46bb112a8
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 0656c84ac444a10f152f441265f85141347bf1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="staging-an-application-in-azure"></a>在 Azure 中預備應用程式
已封裝應用程式可以是已部署的 toohello 預備環境中 Azure toobe 移動 toohello 生產環境之前，測試的環境中的 hello 應用程式是在 hello 網際網路上存取。 預備環境是與 hello 生產環境中，完全相同，不同之處在於您只能存取 hello 分段混亂格式的 url，也就由 Azure 產生的應用程式。 確認您的應用程式正常運作之後，它可以部署的 toohello 實際執行環境所執行的虛擬 IP (VIP) 交換。

> [!NOTE]
> hello 本文章中的步驟僅適用於 toonode 應用程式裝載為 Azure 雲端服務。
> 
> 

## <a name="step-1-stage-an-application"></a>步驟 1：預備應用程式
這項工作涵蓋 toostage 使用應用程式如何 hello **Microsoft Azure PowerShell**。

1. 當發行服務，只需傳遞 hello **-插槽**hello 參數**發行 AzureServiceProject** cmdlet。
   
   ```powershell
   Publish-AzureServiceProject -Slot staging
   ```
2. 登入 toohello [Azure 傳統入口網站]選取**雲端服務**。 建立 hello 雲端服務之後，與 hello**臨時**也更新資料行狀態**執行**，按一下 hello 服務名稱。
   
   ![portal displaying a running service][cloud-service]
3. 選取 hello**儀表板**，然後選取**臨時**。
   
   ![cloud service dashboard][cloud-service-dashboard]
4. 請注意在 hello hello 值**網站 URL**項目 toohello 權限。 hello DNS 名稱是 Azure 產生模糊化內部識別碼。
   
    ![site url][cloud-service-staging-url]

現在您可以確認 hello 應用程式中使用預備網站 URL 的 hello 預備環境的 hello 正常運作。

## <a name="step-2-upgrade-an-application-in-production-by-swapping-vips"></a>步驟 2：交換 VIP 將應用程式升級至生產環境
驗證的應用程式在預備環境的 hello 升級的版本之後，您可以快速地使其可用於生產交換 hello hello 預備與生產環境的虛擬 Ip (Vip)。

> [!NOTE]
> 這個步驟假設您有已部署應用程式 tooproduction 和設置的 hello 升級的版本的應用程式。
> 
> 

1. 登入 hello [Azure 傳統入口網站]，按一下 **雲端服務**，然後選取 hello 服務名稱。
2. 從 hello**儀表板**，選取**臨時**，然後按一下**交換**hello hello 頁底端。 這會開啟 hello VIP 交換對話方塊。
   
   ![vip swap dialog][vip-swap-dialog]
3. 檢閱 hello 資訊，然後按一下**確定**。 兩個部署的 hello 開始更新預備部署交換器 tooproduction 和 hello 生產部署交換器 toostaging hello 做。

您已成功暫置部署，而且升級生產環境部署在預備環境中的 hello 部署交換 Vip。

## <a name="additional-resources"></a>其他資源
* [如何在 Azure 中的交換 Vip 的服務升級 tooProduction tooDeploy]

[Azure 傳統入口網站]: http://manage.windowsazure.com
[cloud-service]: ./media/cloud-services-nodejs-stage-application/staging-cloud-service-running.png
[cloud-service-dashboard]: ./media/cloud-services-nodejs-stage-application/cloud-service-dashboard-staging.png
[cloud-service-staging-url]: ./media/cloud-services-nodejs-stage-application/cloud-service-staging-url.png
[vip-swap-dialog]: ./media/cloud-services-nodejs-stage-application/vip-swap-dialog.png
[如何在 Azure 中的交換 Vip 的服務升級 tooProduction tooDeploy]: cloud-services-how-to-manage.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
