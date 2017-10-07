---
title: "aaaWhat 是 Microsoft Power BI Embedded？"
description: "Power BI Embedded 可讓您 toointegrate Power BI 報表到您的 web 或行動應用程式讓您不需要 toobuild 自訂解決方案。"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 03649b72-b7d7-40ca-b077-12356d72d4f3
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/20/2017
ms.author: asaxton
ms.openlocfilehash: 0353938b6cdd9bb58b123b250f45f76b8cc7abe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-microsoft-power-bi-embedded"></a>何謂 Microsoft Power BI Embedded？
運用 **Power BI Embedded**，您可以將 Power BI 報告整合至您的 Web 應用程式或行動應用程式。

![](media/powerbi-embedded-whats-is/what-is.png)

Power BI Embedded 是**Azure 服務**，可讓 Isv 和其應用程式中的應用程式開發人員 toosurface Power BI 資料經驗。 身為開發人員，您已建置應用程式，這些應用程式有它們自己的使用者和個別的功能集。 這些應用程式也會發生一些內建資料元素，如圖表和報表現在可透過 Microsoft Power BI Embedded 電源 toohave。 您不需要 Power BI 帳戶 toouse 您的應用程式。 您可以繼續 toosign 之前，像是 tooyour 應用程式中，檢視並與其互動 hello Power BI 報表體驗而不需要任何額外的授權。

## <a name="licensing-for-microsoft-power-bi-embedded"></a>Microsoft Power BI Embedded 授權
在 hello **Microsoft Power BI Embedded**使用量模型，Power BI 不 hello 責任 hello 使用者授權。  相反地，**工作階段**購買 hello 會耗用 hello 視覺效果、 hello 應用程式的開發人員和負責 toohello 訂用帳戶擁有這些資源。 其他資訊可以在 hello 找到[定價頁面](https://azure.microsoft.com/en-us/pricing/details/power-bi-embedded/)。

## <a name="microsoft-power-bi-embedded-conceptual-model"></a>Microsoft Power BI Embedded 概念模型

![](media/powerbi-embedded-whats-is/model.png)

其他任何服務一樣在 Azure 中，適用於 Power BI Embedded 資源經由 hello [Azure 資源管理員 Api](https://msdn.microsoft.com/library/mt712306.aspx)。 在此情況下，您佈建的 hello 資源是**Power BI 工作區集合**。

## <a name="workspace-collection"></a>工作區集合
A**工作區集合**是 hello 最上層 Azure 容器資源包含 0 或多個**工作區**。  A**工作區****集合**擁有所有的 hello 標準 Azure 屬性，為 hello 下列：

* **存取金鑰**– 安全地呼叫時使用的索引鍵 hello Power BI 應用程式開發介面 （稍後的章節中所述）。
* **使用者**– Azure Active Directory (AAD) 的使用者具有系統管理員權限 toomanage hello hello Azure 入口網站或 Azure 資源管理員 API 透過 Power BI 工作區集合。
* **區域**的佈建一部分**工作區集合**，您可以選取地區 toobe 中佈建。 如需詳細資訊，請參閱 [Azure 地區](https://azure.microsoft.com/regions/)。

## <a name="workspace"></a>工作區
**工作區**是 Power BI 內容的容器，可包括資料集和報告。 **工作區** 在第一次建立時是空白的。 您會撰寫使用 Power BI Desktop 的內容，以及您要以程式設計方式在 hello PBIX 部署到您工作區中使用 hello [Power BI 匯入 API](https://msdn.microsoft.com/library/mt711504.aspx)。 您也可以透過程式設計方式建立資料集，然後在應用程式內建立報告，而不是使用 Power BI Desktop 來建立。

## <a name="using-workspace-collections-and-workspaces"></a>使用工作區集合和工作區
**工作區集合**和**工作區**是容器的使用和組織在何種最佳方式適合 hello 設計，您要建置的 hello 應用程式的內容。 會有許多不同的方式，您可以排列中的 hello 內容。 您可以選擇 tooput 一個工作區中的所有內容，然後使用更新版本的應用程式權杖 toofurther 細分 hello 在您的客戶之間的內容。 您也可以選擇 tooput 所有客戶不同的工作區中，使其沒有兩者之間的某些分隔。 或者，您可以選擇依區域，而不是由客戶 tooorganize 使用者。 此彈性的設計可讓您 toochoose hello 最佳方式 tooorganize 內容。

## <a name="cached-datasets"></a>快取的資料集
您可以使用快取的資料集。  但是，在資料已載入 **Microsoft Power BI Embedded** 之後，您無法重新整理快取的資料。 快取的資料集，表示您匯入 Power BI Desktop 的 hello 資料，而不是使用 DirectQuery。

## <a name="authentication-and-authorization-with-app-tokens"></a>應用程式權杖中的驗證與授權
**Microsoft Power BI Embedded** tooyour 應用程式 tooperform 會延後，所有 hello 必要的使用者驗證和授權。 並沒有明確要求您的使用者必須是 Azure Active Directory (Azure AD) 的客戶。  相反地，您的應用程式表示太**Microsoft Power BI Embedded**授權 toorender 使用 Power BI 報表**應用程式驗證權杖 （應用程式語彙基元）**。  這些**應用程式權杖**視您的應用程式想 toorender 報表時建立。

![](media/powerbi-embedded-whats-is/app-tokens.png)

**應用程式驗證權杖 （應用程式語彙基元）**會針對使用的 tooauthenticate **Microsoft Power BI Embedded**。  應用程式權杖 有三種類型：

1. 佈建權杖 - 將新的「工作區」佈建到「工作區集合」時使用
2. 開發語彙基元-使用當進行直接呼叫 toohello **Power BI REST Api**
3. 內嵌語彙基元-呼叫 toorender 時所使用的報表中 hello 內嵌 iframe

這些語彙基元會用於 hello 與互動的各階段**Microsoft Power BI Embedded**。  hello 語彙基元的設計可讓您可以從您的應用程式 tooPower BI 委派權限。 如需詳細資訊，請參閱 [應用程式權杖流程](power-bi-embedded-app-token-flow.md)。

## <a name="create-or-edit-reports-within-your-application"></a>在應用程式內建立或編輯報告

您可以現在編輯存在報表，或直接在您的應用程式中建立新的報表，而不需要 toouse Power BI Desktop。 這需要工作區內已存在資料集。

## <a name="see-also"></a>另請參閱

[Microsoft Power BI Embedded 常見案例](power-bi-embedded-scenarios.md)  
[開始使用 Microsoft Power BI Embedded](power-bi-embedded-get-started.md)  
[開始使用範例](power-bi-embedded-get-started-sample.md)  
[內嵌報告](power-bi-embedded-embed-report.md)  
[在 Power BI Embedded 中驗證和授權](power-bi-embedded-app-token-flow.md)  
[JavaScript 內嵌範例](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[PowerBI-CSharp Git 存放庫](https://github.com/Microsoft/PowerBI-CSharp)  
[PowerBI-Node Git存放庫](https://github.com/Microsoft/PowerBI-Node)  
有其他疑問？ [再試一次 hello Power BI 社群](http://community.powerbi.com/)
