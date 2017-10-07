---
title: "aaaHow tooScale App Service 環境中的應用程式"
description: "在 App Service 環境中調整應用程式"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: jimbe
ms.assetid: 78eb1e49-4fcd-49e7-b3c7-f1906f0f22e3
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: ccompy
ms.openlocfilehash: 08916eac056c46bf8cb6edffbf96285317b32062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-apps-in-an-app-service-environment"></a>在 App Service 環境中調整應用程式
Hello Azure App Service 中有正常三件事您可以調整：

* 定價方案
* 背景工作角色大小 
* 執行個體數目。

在 ase 中沒有定價計劃需要 tooselect 或變更 hello。  就功能而言，它已經是 Premium 定價功能層級。  

尊重 tooworker 大小、 使用 hello ASE 系統管理員可以指派 hello hello 計算資源 toobe 用於每個背景工作集區大小。  這表示您可以有具 P4 計算資源的背景工作集區 1，以及具 P1 計算資源的背景工作集區 2 (如有需要的話)。  它們並沒有 toobe 大小的順序。  如周圍 hello 大小和其定價的詳細資訊，請參閱 hello 文件[Azure 應用程式服務定價][AppServicePricing]。  這會使擴充選項中的 App Service 環境 toobe web 應用程式和應用程式服務方案的 hello:

* 背景工作集區選取
* 執行個體數目

變更項目透過 hello 完成適當的顯示您 ASE 裝載應用程式服務方案的 UI。  

![][1]

您無法向上擴充您 ASP 是中的 hello 背景工作集區中的可執行的運算資源的 hello 數目超過您 ASP。  如果您需要計算該背景工作集區中的資源則需要 tooget 您 ASE 管理員 tooadd 它們。  資訊重新設定您 ASE 閱讀這裡 hello 資訊：[如何 tooConfigure App Service 環境][HowtoConfigureASE]。  您也可以 tootake hello ASE 自動調整規模功能 tooadd 容量根據排程或度量的優點。  設定自動調整規模的 hello ASE 環境本身的更多詳細資料請參閱的 tooget[如何 tooconfigure 自動調整規模的 App Service 環境][ASEAutoscale]。

您可以建立多個應用程式服務方案使用不同的背景工作集區，從運算資源，或者您可以使用 hello 相同的背景工作集區。  範例如果您在背景工作 (10) 的可執行的運算資源集區 1，則您可以選擇 toocreate 一個應用程式服務計劃使用 (6) 的計算資源，且第二個應用程式服務計劃，則會使用 (4) 的計算資源。

### <a name="scaling-hello-number-of-instances"></a>調整執行個體的 hello 數目
當您初次在 App Service 環境中建立 Web 應用程式時，它會從 1 個執行個體開始。  接著，您可以向外延展 tooadditional 執行個體 tooprovide 其他運算資源應用程式。   

如果 ASE 有足夠的容量，這就很簡單。  您移 tooyour App Service 方案保存您想 tooscale 和選取標尺的 hello 站台。  這會開啟 hello 其中您可以手動設定您的 ASP hello 比例或您 asp 設定自動調整規模規則的 UI。  只要設定您的應用程式的 toomanually 標尺***縮放***太***手動輸入執行個體計數***。  從這裡拖曳 hello 滑桿 toohello 預期數量或是輸入 hello 方塊下一步 toohello 滑桿。  

![][2] 

如同通常是 ASP 在 ASE 工作中的 hello 自動調整規模規則 hello 相同。  您可以選取 [調整依據] 下方的 [CPU 百分比]，根據 CPU 百分比建立 ASP 的自動調整規則，或使用 [排程和效能規則] 建立更複雜的規則。  toosee 更完成詳細資料，設定自動調整規模使用 hello 指南此處[調整 Azure App Service 中的應用程式][AppScale]。 

### <a name="worker-pool-selection"></a>背景工作集區選取
如前文所述，從 hello ASP UI 存取 hello 背景工作集區選取範圍。  開啟 hello ASP tooscale 並選取 背景工作集區的 hello 刀鋒視窗。  您會看到所有您已設定您的 App Service 環境中的 hello 背景工作集區。  如果您有只有一個背景工作集區然後您只會看到列出 hello 一個集區。  toochange 哪些背景工作集區您 ASP 中，您只需選取您想要您 App Service 方案 toomove hello 背景工作集區。  

![][3]

從一個背景工作集區 tooanother 移動您 ASP 之前很重要 toomake 確定您將必須針對您 ASP 適當的容量。  在 hello 清單中的背景工作集區，不只列出 hello 背景工作集區名稱，但您也可以查看多少的背景工作的背景工作集區中可用。  請確定有足夠的執行個體可用 toocontain 您 App Service 方案。  如果您需要更多計算 hello 背景工作集區中的資源您想要然後取得您 ASE 管理員 tooadd toomove 它們。  

> [!NOTE]
> 移動 ASP 從一個背景工作集區會導致冷啟動 hello 該 ASP 應用程式。  這可能會導致要求 toorun 緩時變您的應用程式是冷啟動 hello 新的計算資源。  hello 冷啟動可以避免使用 hello[熱機功能的應用程式][ AppWarmup] Azure App Service 中。  hello hello 文章所述的應用程式初始化模組也適用於冷啟動因為 hello 初始化處理程序也會叫用應用程式時冷啟動新的計算資源。 
> 
> 

## <a name="getting-started"></a>開始使用
tooget 開始使用應用程式服務環境中，請參閱[如何 tooCreate App Service 環境][HowtoCreateASE]

如需 hello Azure 應用程式服務平台的詳細資訊，請參閱[Azure App Service][AzureAppService]。

<!--Image references-->
[1]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-aspblade.png
[2]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-manualscale.png
[3]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-sizescale.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ScaleWebapp]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[CreateWebappinASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-a-web-app-in-an-ase/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[AppScale]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[AppWarmup]: http://ruslany.net/2015/09/how-to-warm-up-azure-web-app-during-deployment-slots-swap/
