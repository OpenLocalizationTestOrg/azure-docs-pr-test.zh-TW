---
title: "預備雲端服務部署 (Node.js) | Microsoft Docs"
description: "了解如何將 Azure 應用程式部署至預備環境，然後使用虛擬 IP (VIP) 交換來部署至生產環境。"
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
ms.openlocfilehash: b3000ed769e8c60eccb21e26f53ce7ccb7e68d7f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="staging-an-application-in-azure"></a>在 Azure 中預備應用程式
將封裝的應用程式移至生產環境供網際網路存取之前，可先將應用程式部署到 Azure 中的預備環境來進行測試。 預備環境與生產環境完全相同，差別在於您只能以 Azure 產生的隱藏 URL 來存取預備應用程式。 在確認應用程式可正常運作之後，就可以執行虛擬 IP (VIP) 交換將它部署至生產環境。

> [!NOTE]
> 本文中的步驟僅適用於以 Azure 雲端服務的形式受到代管的節點應用程式。
> 
> 

## <a name="step-1-stage-an-application"></a>步驟 1：預備應用程式
此工作涵蓋如何使用 **Microsoft Azure PowerShell**來預備應用程式。

1. 發佈服務時，只要將 **-Slot** 參數傳給 **Publish-AzureServiceProject** Cmdlet 即可。
   
   ```powershell
   Publish-AzureServiceProject -Slot staging
   ```
2. 登入 [Azure 傳統入口網站]，並選取 [雲端服務]。 當雲端服務已建立且 [預備] 欄狀態更新為 [正在執行] 之後，按一下服務名稱。
   
   ![portal displaying a running service][cloud-service]
3. 選取 [儀表板]，然後選取 [預備]。
   
   ![cloud service dashboard][cloud-service-dashboard]
4. 請注意右邊的 [網站 URL]  項目中的值。 DNS 名稱是 Azure 產生的隱藏內部識別碼。
   
    ![site url][cloud-service-staging-url]

現在，您可以利用預備網站 URL，驗證應用程式在預備環境中可正常運作。

## <a name="step-2-upgrade-an-application-in-production-by-swapping-vips"></a>步驟 2：交換 VIP 將應用程式升級至生產環境
在預備環境中驗證應用程式的升級版本之後，您可以交換預備和生產環境的虛擬 IP (VIP)，快速將應用程式移至生產環境。

> [!NOTE]
> 此步驟假設您已將應用程式部署至生產環境，也已預備應用程式的升級版本。
> 
> 

1. 登入 [Azure 傳統入口網站]，按一下 [雲端服務]，然後選取服務名稱。
2. 從 [儀表板] 中，選取 [預備]，然後按一下頁面底部的 [交換]。 這樣會開啟 [VIP 交換] 對話方塊。
   
   ![vip swap dialog][vip-swap-dialog]
3. 檢閱資訊，然後按一下 [確定] 。 兩個部署開始更新，預備部署會切換至生產環境，而生產部署會切換至預備環境。

您已與預備中的部署交換 IP，順利預備部署並升級生產部署。

## <a name="additional-resources"></a>其他資源
* [如何在 Azure 中交換 VIP 將服務升級部署至生產環境]

[Azure 傳統入口網站]: http://manage.windowsazure.com
[cloud-service]: ./media/cloud-services-nodejs-stage-application/staging-cloud-service-running.png
[cloud-service-dashboard]: ./media/cloud-services-nodejs-stage-application/cloud-service-dashboard-staging.png
[cloud-service-staging-url]: ./media/cloud-services-nodejs-stage-application/cloud-service-staging-url.png
[vip-swap-dialog]: ./media/cloud-services-nodejs-stage-application/vip-swap-dialog.png
[如何在 Azure 中交換 VIP 將服務升級部署至生產環境]: cloud-services-how-to-manage.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
