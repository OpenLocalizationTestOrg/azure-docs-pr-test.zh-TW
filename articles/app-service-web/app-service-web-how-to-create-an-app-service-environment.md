---
title: "aaaHow tooCreate App Service 環境 v1"
description: "App Service 環境 v1 的建立流程說明"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 81bd32cf-7ae5-454b-a0d2-23b57b51af47
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 95feb33854eee5bac02fa68b066e2fc10eb3fede
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-app-service-environment-v1"></a>如何 tooCreate App Service 環境 v1 

> [!NOTE]
> 這篇文章是關於 hello App Service 環境 v1。 沒有 hello App Service 環境更容易 toouse 且功能更強大的基礎結構上執行較新版本。 有關 hello 新版本的詳細資訊以 hello 開頭的 toolearn[簡介 toohello App Service 環境](../app-service/app-service-environment/intro.md)。
> 

### <a name="overview"></a>概觀
hello 應用程式服務環境 (ASE) 是 Azure 應用程式服務，可提供 hello 多租用戶戳記中不提供增強的組態功能的高階服務選項。 hello ASE 功能基本上會將部署 hello Azure 應用程式服務，在客戶的虛擬網路。 應用程式服務環境的 hello 功能更深入瞭解提供的 toogain 讀取 hello[何謂 App Service 環境][ WhatisASE]文件。

### <a name="before-you-create-your-ase"></a>建立 ASE 之前
重要 toobe 留意 hello 項目，您無法變更它。 建立後，您無法變更 ASE 的相關層面是：

* 位置
* 訂閱
* 資源群組
* 使用的 VNet
* 使用的子網路 
* 子網路大小

當挑選 VNet，然後指定子網路，請確定它是夠大 tooaccomodate 任何未來的成長。 

### <a name="creating-an-app-service-environment-v1"></a>建立 App Service 環境 v1
toocreate 需要 toosearch App Service 環境 v1 hello Azure Marketplace 中的***App Service 環境 v1***，或透過 新增-> Web + 行動裝置版-> App Service 環境。 toocreate ASEv1:

1. 提供您 ASE hello 名稱。 指定的 hello ASE hello 名稱將用於 hello hello ASE 中建立的應用程式。 如果名稱 hello ASE 是 appsvcenvdemo hello 子網域名稱就是。*appsvcenvdemo.p.azurewebsites.net*。 如果您因此建立名為 *mytestapp* 的應用程式，則可定址於 *mytestapp.appsvcenvdemo.p.azurewebsites.net*。 您無法在您 ASE hello 名稱中使用空白字元。 如果您在 hello 名稱中使用大寫字元，hello 網域名稱會 hello 總小寫的版本名稱。 如果您使用 ILB，則 ASE 名稱不會用於您的子網域中，但是會在 ASE 建立期間明確指定
   
    ![][1]
2. 選取您的訂用帳戶。 用您 ASE hello 訂用帳戶也是 hello 其中一個會使用建立該 ASE 中的所有應用程式。 您無法將 ASE 放在另一個訂用帳戶中的 VNet
3. 選取或指定新的資源群組。 用於您 ASE hello 資源群組必須 hello 用於 VNet 的相同。 如果您選取預先存在的 VNet，然後針對您 ASE hello 資源群組的選擇將會更新的 tooreflect 的 VNet。
   
    ![][2]
4. 請選取您的虛擬網路及位置選項。 您可以選擇 toocreate 新的 VNet，或選取現有的 VNet。 如果您選取新的 VNet，則可以指定名稱和位置。 hello 新的 VNet 必須 hello 位址範圍 192.168.250.0/23 和名為的子網路**預設**，定義為 192.168.250.0/24。 您也可以僅選取既有的傳統或 Resource Manager VNet。 hello VIP 類型選取項目可讓您判斷是否可以從 hello 直接存取您 ASE 網際網路 （外部），或者如果它會使用內部負載平衡 (ILB)。 詳細資訊，請閱讀 toolearn [App Service 環境中使用內部負載平衡器][ILBASE]。 如果您選取的外部 VIP 類型可以選取多少外部 IP 位址 hello 系統會透過 IPSSL 用途。 如果您選擇 [內部] 您需要將會使用您 ASE toospecify hello 子網域。 ASE 可以部署到使用公用位址範圍*或* RFC1918 位址空間 (也就是私人位址) 的虛擬網路。 在順序 toouse 具有公用位址範圍的虛擬網路，您必須事先 toocreate hello VNet。 當您選取預先存在的 VNet 時您 ASE 建立期間需要 toocreate 新的子網路。 **您無法在 hello 入口網站中使用的預先建立的子網路。如果您使用 Resource Manager 範本建立 ASE，則可以使用既有的子網路建立 ASE。** 從範本 toocreate ase 中的，請使用 hello 資訊，[從範本建立 App Service 環境][ ILBAseTemplate]並在這裡， [範本，建立ILBAppService環境][ASEfromTemplate].

### <a name="details"></a>詳細資料
一個 ASE 是使用 2 個前端和 2 個背景工作角色建立。 hello 前端做為 hello HTTP/HTTPS 端點，並且將流量傳送 toohello 工作者都是 hello 角色裝載您的應用程式。 您可以調整 hello 數量 ASE 建立之後，且可以甚至是設定這些資源集區上的自動調整規模規則。 如需詳細資訊，手動調整，App Service 環境的管理和監視這裡：[如何 tooconfigure App Service 環境][ASEConfig] 

Hello 一個 ASE 可以存在於 hello hello ASE 所使用的子網路。 hello 子網路不能用於 hello ASE 以外的任何項目

### <a name="after-app-service-environment-v1-creation"></a>在 App Service 環境 v1 建立之後
建立 ASE 之後，您可以調整：

* 前端的數量 (最小值：2)
* 背景工作的數量 (最小值：2)
* IP SSL 可用的 IP 位址數目
* 計算 hello 前端 」 或 「 背景工作所使用的資源大小 （前端大小下限是 P2）

有手動縮放比例、 管理和監視的應用程式服務環境這裡周圍的更多詳細資料：[如何 tooconfigure App Service 環境][ASEConfig] 

如需自動調整資訊沒有的指南：[如何 tooconfigure 自動調整規模的 App Service 環境][ASEAutoscale]

有沒有可用的自訂，例如 hello 資料庫和儲存體的其他相依性。 這些是由 Azure 處理，而且隨附 hello 系統。 向上 too500 GB hello 系統儲存體支援 hello 整個 App Service 環境並在 hello 資料庫會調整 azure hello 小數位數 hello 系統所需。

## <a name="getting-started"></a>開始使用
所有發行項以及-的應用程式服務環境的 hello[讀我檔案的應用程式服務環境](../app-service/app-service-app-service-environments-readme.md)。

請參閱 < 開始使用 App Service 環境 v1 tooget[簡介 toohello App Service 環境 v1][WhatisASE]

如需 hello Azure 應用程式服務平台的詳細資訊，請參閱[Azure App Service][AzureAppService]。

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-basecreateblade.png
[2]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-vnetcreation.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ILBASE]: http://azure.microsoft.com/documentation/articles/app-service-environment-with-internal-load-balancer/
[ILBAseTemplate]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-create/
[ASEfromTemplate]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-create-ilb-ase-resourcemanager/
