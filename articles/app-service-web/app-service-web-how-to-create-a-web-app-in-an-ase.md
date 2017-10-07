---
title: "aaaCreate App Service 環境 v1 中的 web 應用程式"
description: "了解如何 toocreate web 應用程式和 App Service 環境 v1 中的 app service 方案"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 983ba055-e9e4-495a-9342-fd3708dcc9ac
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 322ef344517c54247b102fb4920e35645986ef98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-an-app-service-environment-v1"></a>在 App Service 環境 v1 中建立 Web 應用程式

> [!NOTE]
> 這篇文章是關於 hello App Service 環境 v1。  沒有 hello App Service 環境更容易 toouse 且功能更強大的基礎結構上執行較新版本。 有關 hello 新版本的詳細資訊以 hello 開頭的 toolearn[簡介 toohello App Service 環境](../app-service/app-service-environment/intro.md)。
> 

## <a name="overview"></a>概觀
本教學課程示範如何 toocreate web 應用程式和應用程式服務計劃中[App Service 環境 v1](app-service-app-service-environment-intro.md) (ASE)。 

> [!NOTE]
> 如果您想如何 toolearn toocreate web 應用程式，但不需要 toodo 它在應用程式服務環境中，請參閱[建立.NET web 應用程式](app-service-web-get-started-dotnet.md)或其中一個 hello 相關的其他語言和架構教學課程。
> 
> 

## <a name="prerequisites"></a>必要條件
本教學課程假設您已建立 App Service 環境。 如果尚未建立，請參閱 [建立 App Service 環境](app-service-web-how-to-create-an-app-service-environment.md)。 

## <a name="create-a-web-app"></a>建立 Web 應用程式
1. 在 hello [Azure 入口網站](https://portal.azure.com/)，按一下 **新增 > Web + 行動 > Web 應用程式**。 
   
    ![][1]
2. 選取您的訂用帳戶。  
   
    如果您有多個訂用帳戶請注意該 toocreate App Service 環境中的應用程式中，您需要 toouse hello 建立 hello 環境時所使用的相同訂用帳戶。 
3. 選取或建立資源群組。
   
    *資源群組*您 toomanage 做為一個單位相關的 Azure 資源，有助於建立時啟用*角色型存取控制*(RBAC) 規則，您的應用程式。 如需詳細資訊，請參閱 [Azure Resource Manager概觀][ResourceGroups]。 
4. 選取或建立 App Service 方案。
   
     是受管理的 Web 應用程式集。  通常當您選取定價，hello 價格收費是套用的 toohello 應用程式服務方案而不是 toohello 個別的應用程式。 在 ase 中，您需支付 hello 計算執行個體配置 toohello ASE 而不是已列出您 asp。  您的應用程式服務方案的 hello 執行個體向上延展 tooscale hello 數字的 web 應用程式的執行個體而且會影響所有 hello web 應用程式在該計劃中。  某些功能，例如網站位置或 VNET 整合也有 hello 計劃中的數量限制。  如需詳細資訊，請參閱 [Azure App Service 方案概觀](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)
   
    您可以查看 hello 位置記下 hello 計劃名稱，您 ASE 中識別應用程式服務計劃的 hello。  
   
    ![][5]
   
    如果您想 toouse App Service 方案已存在您的 App Service 環境中，選取該計劃。 如果您想 toocreate 新的 App Service 方案，請參閱 hello 遵循此教學課程中，區段[App Service 環境中建立 App Service 方案](#createplan)。
5. 輸入 hello web 應用程式的名稱，然後按一下**建立**。 
   
    如果您 ASE 在 ase 中使用外部 VIP hello 應用程式的 URL 是: [*sitename*]。 [*的 App Service 環境名稱*]。 p.azurewebsites.net 而不是 [*sitename*]。 名稱是.azurewebsites.net
   
    如果您 ASE ASE 是，請使用內部 VIP 然後 hello 應用程式的 URL: [*sitename*]。 [*ASE 建立期間所指定的子網域*]   
    您可以選取您 ASP ASE 建立期間之後，您會看到更新以下的 hello 子網域**名稱**

## <a name="createplan"></a> 建立 App Service 方案
當您在 App Service 環境中建立 App Service 方案時，您的背景工作角色選擇會因為在 ASE 中沒有共用的背景工作角色而有所不同。  您有 toouse hello 工作者是 hello 的已配置 toohello ASE hello 系統管理員。這表示該 toocreate 新計劃，您在所有您已在該背景工作集區的計劃需要 toohave 多個工作者配置 tooyour ASE 背景工作集區的執行個體的 hello 總數比。  如果您沒有足夠的背景工作中您 ASE 背景工作集區 toocreate 您計劃，您會需要使用它們加入您 ASE admin tooget toowork。

App Service 環境所裝載的應用程式服務計劃與另一項差異是 hello 缺乏定價選取項目。  當您 App Service 環境您支付 hello 系統所使用的計算資源，並且在該環境中沒有加入的費用 hello 計劃。  當您建立 App Service 方案時，您通常會選取決定費率的價格方案。  App Service 環境基本上是您可以在其中建立內容的私人位置。  您需支付 hello 環境與不 toohost 您的內容。

hello 下列指示說明 toocreate 應用程式服務計劃建立 hello hello 教學課程的上一節中所述的 web 應用程式時。

1. 按一下**新建**在 hello 計劃選擇 UI，並提供您計劃的名稱，就像平常一樣 ASE 之外。
2. 選取您想 toouse，從您位置選擇器的 hello ASE。
   
    因為 App Service 環境基本上是專用部署位置，所以它會顯示在 [位置] 下。 
   
    ![][2]
   
    在選擇器中的位置 hello ase 中的選取範圍之後, hello 應用程式服務計劃建立 UI 更新。  hello 位置現在會顯示 hello hello ASE 系統名稱與 hello 區域，而且要更換 hello 定價計劃選擇器使用背景工作集區選取器。  
   
    ![][3]

### <a name="selecting-a-worker-pool"></a>選取背景工作集區
通常 Azure App Service 中和外部 App Service 環境中，有 3 hello 選取範圍的固定的價格計劃中的可用的運算大小。  以類似的方式，為 ase 中可以定義總 too3 集區的背景工作，並且指定 hello 運算大小所使用的背景工作集區。  這表示租用戶的 hello ASE 是而不需要選取與您的應用程式服務方案的運算大小的定價方案，您要選取的名為*背景工作集區*。  

hello 背景工作集區選取 UI 會顯示 hello 運算大小 hello 名稱下方的背景工作集區使用。  hello 可用數量是指 toohow 許多計算執行個體可供該集區中使用。  hello 總集區實際上可能會有比這個數字的多個執行個體，但此值是指 toosimply 多少未處於使用中。  如果您需要 tooadjust App Service 環境 tooadd 更多計算資源，請參閱[設定 App Service 環境](app-service-web-configure-an-app-service-environment.md)。

![][4]

在此範例中，您只會看到兩個可用的背景工作集區。 這是因為 hello ASE 系統管理員只能組成的兩個背景工作集區配置的主機。  hello 第三步會顯示配置到其中的 Vm 時。  

## <a name="after-web-app-creation"></a>建立 Web 應用程式之後
有幾個考量執行 web 應用程式及管理應用程式服務計劃在 ase 中需要 toobe 列入考量。  

如前文所述，hello ASE hello 擁有者會負責 hello hello 系統大小，因此它們也是負責確保足夠的容量 toohost hello 預期應用程式服務方案的。 如果沒有可用的背景工作，將不會無法 toocreate 應用程式服務方案。  這也是 true tooscaling 設定您的 web 應用程式。  如果您需要更多執行個體，則您會有 tooget 您 App Service 環境管理 tooadd 更多背景工作。

建立您的 web 應用程式和應用程式服務方案之後，它是個不錯的主意 tooscale 它。  在 ase 中您一律需要應用程式服務計劃 tooprovide 容錯能力的 toohave 至少 2 個應用程式。  調整應用程式服務計劃在 ase 中是正常透過 hello 應用程式服務方案 UI hello 相同。  如需有關調整[如何 tooscale App Service 環境中的 web 應用程式](app-service-web-scale-a-web-app-in-an-app-service-environment.md)

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspnewwebapp.png
[2]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createasplocation.png
[3]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspselected.png
[4]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspworkerpool.png
[5]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/selectaspinase.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoScale]: http://azure.microsoft.com/documentation/articles/app-service-web-scale-a-web-app-in-an-app-service-environment
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment
[ResourceGroups]: ../azure-resource-manager/resource-group-overview.md
[AzurePowershell]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
