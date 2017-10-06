---
title: "開始使用 Microsoft Power BI Embedded aaaGet"
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
ms.openlocfilehash: ebb550cb4eba761dde3c23e4dd0314fc885817e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a>開始使用 Microsoft Power BI Embedded

**Power BI Embedded**互動式 Power BI 報表到其自身應用程式，可讓應用程式開發人員 tooadd 是一項 Azure 服務。 **Power BI Embedded**可搭配現有的應用程式，而不需要重新設計，或變更 hello 方式使用者登入。

資源**Microsoft Power BI Embedded**經由 hello [Azure ARM Api](https://msdn.microsoft.com/library/mt712306.aspx)。 在此情況下，您佈建的 hello 資源是**Power BI 工作區集合**。

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a>建立工作區集合

A**工作區集合**是 hello 最上層的 Azure 資源和會內嵌在應用程式中的 hello 內容的容器。 建立 **工作區集合** 的方式有兩種︰

* 使用手動 hello Azure 入口網站
* 以程式設計方式使用 hello Azure 資源 Manager(ARM) Api

讓我們逐步解說 hello 步驟 toobuild**工作區集合**使用 hello Azure 入口網站。

1. 開啟並登入 **Azure 入口網站**： [http://portal.azure.com](http://portal.azure.com)。
2. 按一下**+ 新增**hello 上方面板上。
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. 按一下 [資料 + 分析] 之下的 [Power BI Embedded]。
4. 在 hello**刀鋒視窗中的工作區集合**，輸入 hello 所需的資訊。 如需**價格**，請參閱 [Power BI Embedded 價格](http://go.microsoft.com/fwlink/?LinkID=760527)。
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. 按一下 [建立] 。

hello**工作區集合**需要幾分鐘的時間 tooprovision。 完成時，您將會進入 toohello**刀鋒視窗中的工作區集合**。

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

hello**刀鋒視窗中建立**包含需要 toocall hello Api，建立工作區和部署內容 toothem hello 資訊。

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a>檢視 Power BI API 存取金鑰

其中一個最重要的部分所需的資訊 toocall hello Power BI REST Api 的 hello 是 hello**便捷鍵**。 這些是使用的 toogenerate hello**應用程式權杖**所使用的 tooauthenticate API 要求。 tooview 您**便捷鍵**，按一下 [**便捷鍵**上 hello**設定] 刀鋒視窗**。 若要深入了解**應用程式權杖**，請參閱 [使用 Power BI Embedded 驗證和授權](power-bi-embedded-app-token-flow.md)。

   ![](media/power-bi-embedded-get-started/access-keys.png)

您會發現您有兩個金鑰。

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

複製這些金鑰並將它們安全地儲存在您的應用程式中。 它是非常重要，您這些機碼平常一樣處理密碼，因為它們會提供存取 tooall hello 內容，在您**工作區集合**。

雖已列出兩個金鑰，但特定時間只需要一個金鑰。 hello 第二個主要被為了讓您可以不需中斷存取 toohello 服務會定期重新產生金鑰。

您現在已有應用程式的 Power BI 執行個體以及 **存取金鑰**，您可以將報告匯入自己的應用程式中。 之前，您學習如何 tooimport 的報表，hello 下一節會說明建立 Power BI 資料集和報表 tooembed 到應用程式。

## <a name="working-with-workspaces"></a>使用工作區

建立您的工作區集合之後，您將需要 toocreate 將裝載您的報表和資料集的工作區。 toocreate 工作區，您將需要 toouse hello [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx)。

## <a name="create-power-bi-datasets-and-reports-tooembed-into-an-app-using-power-bi-desktop"></a>建立 Power BI 資料集和報表 tooembed 到應用程式中使用 Power BI Desktop

既然您已經建立您的應用程式的 Power BI 執行個體，且有**便捷鍵**，您將需要 toocreate hello Power BI 資料集和您想 tooembed 的報表。 使用 **Power BI Desktop**可以建立資料集和報告。 您可以下載 [免費的 Power BI Desktop](https://go.microsoft.com/fwlink/?LinkId=521662)。 或者，tooquickly 開始，您可以下載 hello[零售分析範例 PBIX](http://go.microsoft.com/fwlink/?LinkID=780547)。

> [!NOTE]
> 深入了解如何 toolearn toouse **Power BI Desktop**，請參閱[開始使用 Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop)。

與**Power BI Desktop**，您藉由匯入到 hello 資料的複本連接 tooyour 資料來源**Power BI Desktop**或直接連接 toohello 資料來源使用**DirectQuery**.

以下是使用的 hello 差異**匯入**和**DirectQuery**。

| Import | DirectQuery |
| --- | --- |
| 資料表、資料行和資料  會匯入或複製到 **Power BI Desktop**中。 當您使用的視覺效果， **Power BI Desktop**查詢 hello 資料的複本。 toosee 發生的 toohello 基礎資料的任何變更，您必須重新整理，或匯入完成，目前資料集一次。 |只有資料表和資料行  會匯入或複製到 **Power BI Desktop**中。 當您使用的視覺效果， **Power BI Desktop**查詢 hello 基礎資料來源，這表示您一定要檢視目前的資料。 |

如需有關連接 tooa 資料來源，請參閱[連接 tooa 資料來源](power-bi-embedded-connect-datasource.md)。

在 **Power BI Desktop**中儲存您的工作之後，會建立一個 PBIX 檔案。 此檔案包含您的報告。 此外，如果您匯入資料 hello PBIX 包含 hello 完整資料集，或如果您使用**DirectQuery**，hello PBIX 包含只資料集的結構描述。 您以程式設計方式部署到您工作區中使用 hello hello PBIX [Power BI 匯入 API](https://msdn.microsoft.com/library/mt711504.aspx)。

> [!NOTE]
> **Power BI Embedded**有其他應用程式開發介面 toochange hello 伺服器和資料庫，您的資料集指 tooand 組 hello 資料集的服務帳戶認證將會使用 tooconnect tooyour 資料庫。 請參閱 [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) 和 [Patch 閘道資料來源](https://msdn.microsoft.com/library/mt711498.aspx)。

## <a name="create-power-bi-datasets-and-reports-using-apis"></a>使用 API 建立 Power BI 資料集和報告

### <a name="datsets"></a>資料集

您可以建立 Power BI Embedded 使用 hello REST API 資料集。 接著，將資料推送至資料集。 這可讓您 toowork 而 hello 需要在 Power BI Desktop 的資料。 如需詳細資訊，請參閱[公佈資料集](https://msdn.microsoft.com/library/azure/mt778875.aspx)。

### <a name="reports"></a>報告

您可以直接在您使用 hello JavaScript API 的應用程式中，從資料集建立報表。 如需詳細資訊，請參閱[在 Power BI Embedded 中從資料集建立新的報告](power-bi-embedded-create-report-from-dataset.md)。

## <a name="see-also"></a>另請參閱

[開始使用範例](power-bi-embedded-get-started-sample.md)  
[在 Power BI Embedded 中驗證和授權](power-bi-embedded-app-token-flow.md)  
[內嵌報告](power-bi-embedded-embed-report.md)  
[在 Power BI Embedded 中從資料集建立新的報告](power-bi-embedded-create-report-from-dataset.md)
[儲存報告](power-bi-embedded-save-reports.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript 內嵌範例](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
有其他疑問？ [再試一次 hello Power BI 社群](http://community.powerbi.com/)

