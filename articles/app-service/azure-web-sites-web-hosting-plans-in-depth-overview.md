---
title: "aaaAzure App Service 方案深入概觀 |Microsoft 文件"
description: "了解 Azure App Service 之應用程式服務方案的運作方式，以及在管理經驗上帶來的效益。"
keywords: "App Service, Azure App Service, 級別, 可調整, App Service方案, App Service 成本"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: b384790d9e69b234ca69ac591164c48a4b6ed210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a>Azure App Service 方案深入概觀

應用程式服務計劃代表 hello 集合，其使用的實體資源 toohost 的應用程式。

App Service 方案可定義：

- 區域 (美國西部、美國東部等)
- 級別計數 (一、二、三個執行個體等)
- 執行個體大小 (小型、中型、大型)
- SKU (免費、共用、基本、標準、進階)

[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) 中的 Web Apps、Mobile Apps、Function Apps (或 Functions) 全部都在 App Service 方案中執行。  應用程式在 hello 相同的地區和訂用帳戶，可以共用 App Service 方案。 

所有應用程式指派 tooan **App Service 方案**共用 hello 它所定義的資源。 這可讓您在單一 App Service 方案中託管多個應用程式時，能夠節省成本。

您**App Service 方案**範圍，小從**免費**和**共用**Sku 太**基本**，**標準**，和**Premium** Sku 讓您存取 toomore 資源和沿著 hello 功能的方式。

如果您的應用程式服務方案設定太**基本**SKU 或更高版本，則您可以控制 hello**大小**和調整 hello Vm 的計數。

比方說，如果您計劃設定的 toouse 兩 hello standard 服務層中的 「 小型 」 執行個體，與該方案有關聯的所有應用程式在兩個執行個體上執行。 應用程式也可以存取 toohello standard 服務層功能。 應用程式在其上執行的方案執行個體完全受管理且高度可用。

> [!IMPORTANT]
> hello **SKU**和**標尺**的 hello 應用程式服務計劃可決定 hello 成本不 hello 數目及託管於該應用程式。

這篇文章探討 hello 主要特性，例如層和應用程式服務方案的小數位數以及它們如何進入播放時管理您的應用程式。

## <a name="apps-and-app-service-plans"></a>應用程式和 App Service 方案

在任何指定時間，應用程式服務方案中的一個應用程式只能與一個應用程式服務方案產生關聯。

應用程式和方案都包含在**資源群組**中。 資源群組可做為它在每個資源的 hello 生命週期界限。 您可以使用資源群組 toomanage 應用程式所有 hello 項目放在一起。

由於單一資源群組只能有多個應用程式服務計劃，您可以配置不同的應用程式 toodifferent 實體資源。

例如，您可以將資源分隔為開發、測試和生產環境。 將生產和開發/測試的環境分開可讓您隔離資源。 如此一來，負載測試針對您的應用程式的新版本並不會競用 hello 相同您實際執行的應用程式，實際客戶服務和資源。

當您在單一資源群組中有多個方案時，您也可以定義一個跨越地理區域的應用程式。

例如，在兩個區域中執行的高度可用應用程式包括至少兩個方案，每個區域一個方案，而一個應用程式則與每個方案相關聯。 在這種情況下，hello 應用程式的所有 hello 副本然後都包含在單一資源群組。 具有多個計劃和多個應用程式的資源群組可輕鬆 toomanage、 控制和檢視 hello hello 應用程式健全狀況。

## <a name="create-an-app-service-plan-or-use-existing-one"></a>建立 App Service 方案或使用現有的方案

在建立應用程式時，請考慮建立資源群組。 在 hello 相反地，如果此應用程式是較大型應用程式的元件，並建立 hello 配置給該較大的應用程式的資源群組中。

是否 hello 應用程式是完全新的應用程式或更大的一個部分，您可以選擇 toouse 現有的計劃 toohost 它或另外新建一個。 這項決定其實是容量和預期負載方面的問題。

如果有下列情況，建議將您的應用程式隔離至新的 App Service 方案中：

- 應用程式會耗用大量資源。
- 應用程式有不同的縮放比例 hello 從裝載於現有的方案中其他應用程式。
- 應用程式需要不同地理區域中的資源。

這樣可讓您為應用程式配置一組新的資源，更充分掌控您的應用程式。

## <a name="create-an-app-service-plan"></a>建立應用程式服務方案

> [!TIP]
> 如果您有 App Service 環境，您可以檢閱 hello 文件特定 tooApp 服務環境這裡： [App Service 環境中建立 App Service 方案](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)

從應用程式服務計劃的瀏覽經驗 hello 或做為應用程式建立的一部分，您可以建立空白的應用程式服務方案。

在 hello [Azure 入口網站](https://portal.azure.com)，按一下 **新增** > **Web + 行動**，然後選取**Web 應用程式**或其他應用程式服務應用程式類型。

![在 hello Azure 入口網站中建立應用程式。][createWebApp]

然後，您可以選取或建立 hello hello 新應用程式的應用程式服務計劃。

 ![建立 App Service 方案。][createASP]

toocreate App Service 方案中，按一下**[+] 建立新**，型別 hello **App Service 方案**名稱，然後再選取 適當**位置**。 按一下**定價層**，然後選取適當的定價層 hello 服務。 選取**檢視所有**tooview 多定價選項，例如**免費**和**共用**。 您已選取 hello 定價層之後，請按一下 hello**選取** 按鈕。

## <a name="move-an-app-tooa-different-app-service-plan"></a>移動應用程式 tooa 不同 App Service 方案

您可以移動應用程式 tooa 不同 App Service 方案中 hello [Azure 入口網站](https://portal.azure.com)。 您可以計劃之間移動應用程式，只要 hello 計劃已 hello 相同的資源群組和地理區域。

toomove 的應用程式 tooanother 計劃：

- 瀏覽您想 toomove toohello 應用程式。
- 在 hello**功能表**，尋找 hello **App Service 方案**> 一節。
- 選取**變更應用程式服務方案**toostart hello 程序。

**變更應用程式服務方案**開啟 hello **App Service 方案**選取器。 此時，您可以挑選現有的計劃 toomove 到此應用程式。

> [!IMPORTANT]
> hello 選取應用程式服務方案 UI 會依下列準則的 hello 進行篩選：
> - 存在於 hello 相同資源群組
> - 存在於 hello 相同地理區域
> - 存在於 hello 相同網路空間
>
> 網路空間是 App Service 內的邏輯結構，會定義伺服器資源的群組。 地理區域 （例如美國西部） 包含許多網路空間中使用應用程式服務的訂單 tooallocate 客戶。 目前應用程式服務的資源不能 toobe 網路空間之間移動。
>

![App Service 方案選取器。][change]

每個方案都有其專屬定價層。 例如，將站台從免費層 tooa 標準層，可讓指派 tooit toouse hello 功能和資源 hello 標準層的所有應用程式。

## <a name="clone-an-app-tooa-different-app-service-plan"></a>複製應用程式 tooa 不同 App Service 方案

如果您想 toomove hello 應用程式 tooa 不同的區域，一種替代方法是應用程式複製。 複製會在任何區域中的新或現有 App Service 方案中產生您應用程式的複本。

您可以找到**複製應用程式**在 hello**開發工具**hello 功能表區段。

> [!IMPORTANT]
> 複製具有某些限制，若要深入了解，請閱讀 [使用 Azure 入口網站的 Azure App Service 應用程式複製](../app-service-web/app-service-web-app-cloning-portal.md)。

## <a name="scale-an-app-service-plan"></a>調整 App Service 方案

有三種方式 tooscale 計劃：

- **變更 hello 計劃的定價層**。 Hello 基本層中的計畫可以是轉換後的 tooStandard 和所有應用程式指派 tooit toouse hello hello 標準層功能。
- **變更 hello 計劃的執行個體大小**。 例如，hello 使用小型執行個體的基本層中的計畫可以是已變更的 toouse 大型執行個體。 現在與該方案相關聯之所有應用程式可以使用 hello 額外的記憶體和 CPU 資源，hello 較大的執行個體大小優惠。
- **變更 hello 計劃的執行個體計數**。 比方說，向外延展 toothree 執行個體的標準方案可以調整的 too10 執行個體。 高階計劃可以向外延展 too20 執行個體 (主體 tooavailability)。 現在與該方案相關聯之所有應用程式可以使用 hello 額外的記憶體和 CPU 資源，hello 較大的執行個體計數優惠。

您可以變更定價層和執行個體的大小，依序按一下 hello hello**向上延展**hello 應用程式或 hello 應用程式服務方案設定下的項目。 變更會套用 toohello App Service 方案，並會影響它所主控的所有應用程式。

 ![設定值 tooscale 備份應用程式。][pricingtier]

## <a name="app-service-plan-cleanup"></a>App Service 方案清除

> [!IMPORTANT]
> **應用程式服務計劃**具有沒有相關聯的應用程式 toothem，仍會產生費用，因為它們繼續 tooreserve hello 計算容量。

tooavoid 未預期的費用，刪除 hello 裝載應用程式服務計劃中的最後一個應用程式時，hello 產生空白的應用程式服務計劃也會一併刪除。

## <a name="summary"></a>摘要

應用程式服務方案代表可跨應用程式共用的一組特性和功能。 應用程式服務計劃提供 hello 彈性 tooallocate 特定應用程式 tooa 組的資源，並進一步最佳化 Azure 資源使用率。 如此一來，如果您想 toosave 金錢在測試環境中，您可以共用一個計劃跨多個應用程式。 透過延展到多個區域和方案，也可以最大化生產環境的輸送量。

## <a name="whats-changed"></a>變更的項目

- 從網站 tooApp 服務指南 toohello 變更，請參閱： [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
