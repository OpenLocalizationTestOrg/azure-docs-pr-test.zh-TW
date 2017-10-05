---
title: "開始使用 Microsoft Power BI Embedded"
description: "對於 Power BI Embedded，將互動式 Power BI 報告加入至您的商務智慧應用程式"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 4787cf44-5d1c-4bc3-b3fd-bf396e5c1176
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 4afa8d2c7f8ec1942521ba5fa131967dfd581c91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a>開始使用 Microsoft Power BI Embedded

**Power BI Embedded** 是一項 Azure 服務，可讓應用程式開發人員將互動式 Power BI 報告加入至自己的應用程式。 **Power BI Embedded** 會與現有的應用程式一同運作，而不需要重新設計或變更使用者登入的方式。

**Microsoft Power BI Embedded** 的資源也是透過 [Azure ARM API](https://msdn.microsoft.com/library/mt712306.aspx)佈建。 在此情況下，您佈建的資源是 **Power BI 工作區集合**。

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a>建立工作區集合

**工作區集合** 是最上層的 Azure 資源，而內容的容器將會內嵌在您的應用程式中。 建立 **工作區集合** 的方式有兩種︰

* 以手動方式使用 Azure 入口網站
* 以程式設計方式使用 Azure Resource Manager (ARM) API

讓我們逐步解說使用 Azure 入口網站建立 **工作區集合** 的步驟。

1. 開啟並登入 **Azure 入口網站**： [http://portal.azure.com](http://portal.azure.com)。
2. 按一下頂端面板上的 [+ 新增]  。
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. 按一下 [資料 + 分析] 之下的 [Power BI Embedded]。
4. 在 [工作區集合] 刀鋒視窗上輸入必要資訊。 如需**價格**，請參閱 [Power BI Embedded 價格](http://go.microsoft.com/fwlink/?LinkID=760527)。
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. 按一下 [建立] 。

**工作區集合** 會花費一些時間來佈建。 完成後，您將會進入 [工作區集合刀鋒視窗] 。

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

[建立刀鋒視窗]  包含呼叫 API 所需的資訊，以建立工作區並將內容部署到這些工作區。

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a>檢視 Power BI API 存取金鑰

呼叫 Power BI REST API 所需的其中一項最重要資訊是**存取金鑰**。 這些存取金鑰用來產生**應用程式權杖**，而這些權杖用來驗證 API 要求。 若要檢視您的**存取金鑰**，請按一下 [設定刀鋒視窗] 上的 [存取金鑰]。 若要深入了解**應用程式權杖**，請參閱 [使用 Power BI Embedded 驗證和授權](power-bi-embedded-app-token-flow.md)。

   ![](media/power-bi-embedded-get-started/access-keys.png)

您會發現您有兩個金鑰。

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

複製這些金鑰並將它們安全地儲存在您的應用程式中。 請務必如同密碼一樣處理這些金鑰，因為這些金鑰可供存取您的 **工作區集合**中的所有內容。

雖已列出兩個金鑰，但特定時間只需要一個金鑰。 系統會提供第二個金鑰，以便您定期重新產生金鑰，而不需中斷對服務的存取。

您現在已有應用程式的 Power BI 執行個體以及 **存取金鑰**，您可以將報告匯入自己的應用程式中。 在了解如何匯入報告之前，下一節說明如何建立要內嵌到應用程式中的 Power BI 資料集和報告。

## <a name="working-with-workspaces"></a>使用工作區

建立工作區集合之後，您必須建立將存放報告和資料集的工作區。 若要建立工作區，您必須使用 [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx)。

## <a name="create-power-bi-datasets-and-reports-to-embed-into-an-app-using-power-bi-desktop"></a>使用 Power BI Desktop 建立要內嵌到應用程式中的 Power BI 資料集和報告

您現已為您的應用程式建立 Power BI 執行個體，而且有 **存取金鑰**，您必須建立想要內嵌的 Power BI 資料集和報告。 使用 **Power BI Desktop**可以建立資料集和報告。 您可以下載 [免費的 Power BI Desktop](https://go.microsoft.com/fwlink/?LinkId=521662)。 或者，若要快速開始，您可以下載 [零售分析範例 PBIX](http://go.microsoft.com/fwlink/?LinkID=780547)。

> [!NOTE]
> 若要深入了解如何使用 **Power BI Desktop**，請參閱[開始使用 Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop)。

透過 **Power BI Desktop**，將資料複本匯入 **Power BI Desktop** 或使用 **DirectQuery** 直接連接到資料來源，即可連接到資料來源。

以下是使用 **Import** 和 **DirectQuery** 之間的差異。

| Import | DirectQuery |
| --- | --- |
| 資料表、資料行和資料  會匯入或複製到 **Power BI Desktop**中。 當您使用視覺效果時， **Power BI Desktop** 會查詢資料的複本。 若要查看基礎資料所發生的任何變更，您必須重新整理或再次匯入完整的目前資料集。 |只有資料表和資料行  會匯入或複製到 **Power BI Desktop**中。 當您使用視覺效果時， **Power BI Desktop** 會查詢基礎資料來源，這表示您一直在檢視目前的資料。 |

如需有關連接到資料來源的詳細資訊，請參閱 [連接到資料來源](power-bi-embedded-connect-datasource.md)。

在 **Power BI Desktop**中儲存您的工作之後，會建立一個 PBIX 檔案。 此檔案包含您的報告。 此外，如果您匯入資料，則 PBIX 會包含完整的資料集，或如果您使用 **DirectQuery**，則 PBIX 只包含資料集結構描述。 您會使用 [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx)，以程式設計方式將 PBIX 部署到您工作區。

> [!NOTE]
> **Power BI Embedded** 有其他 API 可變更您的資料集所指向的伺服器和資料庫，以及設定資料集將用來連接到您的資料庫的服務帳戶認證。 請參閱 [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) 和 [Patch 閘道資料來源](https://msdn.microsoft.com/library/mt711498.aspx)。

## <a name="create-power-bi-datasets-and-reports-using-apis"></a>使用 API 建立 Power BI 資料集和報告

### <a name="datsets"></a>資料集

您可以使用 REST API 在 Power BI Embedded 內建立資料集。 接著，將資料推送至資料集。 這可讓您不需要 Power BI Desktop 即可處理資料。 如需詳細資訊，請參閱[公佈資料集](https://msdn.microsoft.com/library/azure/mt778875.aspx)。

### <a name="reports"></a>報告

您可以使用 JavaScript API，直接在應用程式中從資料集建立報告。 如需詳細資訊，請參閱[在 Power BI Embedded 中從資料集建立新的報告](power-bi-embedded-create-report-from-dataset.md)。

## <a name="see-also"></a>另請參閱

[開始使用範例](power-bi-embedded-get-started-sample.md)  
[在 Power BI Embedded 中驗證和授權](power-bi-embedded-app-token-flow.md)  
[內嵌報告](power-bi-embedded-embed-report.md)  
[在 Power BI Embedded 中從資料集建立新的報告](power-bi-embedded-create-report-from-dataset.md)
[儲存報告](power-bi-embedded-save-reports.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript 內嵌範例](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
有其他疑問？ [試用 Power BI 社群](http://community.powerbi.com/)

