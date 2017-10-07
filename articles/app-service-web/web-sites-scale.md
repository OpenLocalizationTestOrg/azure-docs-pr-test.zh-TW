---
title: "設定應用程式的 Azure 中的 aaaScale |Microsoft 文件"
description: "深入了解如何設定應用程式的 Azure App Service tooadd 容量和功能 中的 tooscale。"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: f7091b25-b2b6-48da-8d4a-dcf9b7baccab
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2016
ms.author: cephalin
ms.openlocfilehash: 97f46f77aeef95aec90d38e8396a023820e3caeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-up-an-app-in-azure"></a>在 Azure 中相應增加應用程式的規模
本文章將示範如何 tooscale Azure App Service 中的應用程式。 有了縮放、 小數位數的兩個工作流程，並向外的延展和這篇文章說明 hello 調整工作流程。

* [相應增加](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling)︰取得更多的 CPU、記憶體、磁碟空間和額外的功能，例如專用虛擬機器 (VM)、自訂網域和憑證、預備位置，以及自動調整等等。 向上擴充藉由變更定價層應用程式服務計劃您的應用程式所屬的 hello。
* [向外延展](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): hello 執行您的應用程式的 VM 執行個體數目增加。
  您可以向外延展 tooas 許多與 20 的執行個體，視您的定價層而定。 [應用程式服務環境](../app-service/app-service-app-service-environments-readme.md)中**Premium**層會進一步增加您的向外延展計數 too50 執行個體。 如需相應放大的詳細資訊，請參閱[手動或自動調整執行個體計數](../monitoring-and-diagnostics/insights-how-to-scale.md)。 您會發現那里 out 方式 toouse 自動調整，也就是 tooscale 執行個體計數會自動根據預先定義的規則和排程。

hello 小數位數設定採用唯一秒 tooapply 和會影響所有的應用程式在您[App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。
它們不需要您 toochange 您的程式碼或重新部署應用程式。

Hello 價格和功能的個別的應用程式服務方案的相關資訊，請參閱[應用程式服務定價詳細資料](https://azure.microsoft.com/pricing/details/web-sites/)。  

> [!NOTE]
> 切換 hello 從 App Service 方案之前**免費**層，您必須先移除 hello[消費限制](https://azure.microsoft.com/pricing/spending-limits/)備妥您的 Azure 訂用帳戶。 Microsoft Azure 應用程式服務訂用帳戶，tooview 或變更選項，請參閱[Microsoft Azure 訂用帳戶][azuresubscriptions]。
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a>相應增加您的定價層
1. 在瀏覽器中，開啟 hello [Azure 入口網站][portal]。
2. 在應用程式的刀鋒視窗中，按一下 所有設定，然後按一下相應增加。
   
    ![瀏覽 tooscale 備份您的 Azure 應用程式。][ChooseWHP]
3. 選擇您的定價層，然後按一下選取 。
   
    hello**通知** 索引標籤將會閃爍綠色**成功**hello 作業完成之後。

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a>調整相關資源
如果您的應用程式相依於其他服務 (如 Azure SQL Database 或 Azure 儲存體)，您也可以根據需求相應增加這些服務。 這些資源不會縮放以 hello App Service 方案，因此必須分別擴充。

1. 在**Essentials**，按一下 hello**資源群組**連結。
   
    ![相應增加 Azure 應用程式的相關資源](./media/web-sites-scale/RGEssentialsLink.png)
2. 在 hello**摘要**屬於 hello**資源群組**刀鋒視窗中，按一下您想 tooscale 資源。 hello 下列螢幕擷取畫面會顯示 SQL Database 資源和 Azure 儲存體資源。
   
    ![瀏覽 tooresource 群組刀鋒視窗 tooscale 備份您的 Azure 應用程式](./media/web-sites-scale/ResourceGroup.png)
3. SQL Database 資源，請按一下**設定** > **定價層**tooscale hello 定價層。
   
    ![向上擴充 hello SQL Database 的後端 Azure 應用程式](./media/web-sites-scale/ScaleDatabase.png)
   
    您也可以針對 SQL 資料庫執行個體開啟 [異地複寫](../sql-database/sql-database-geo-replication-overview.md) 。
   
    Azure 儲存體資源，請按一下**設定** > **組態**tooscale 儲存體選項。
   
    ![向上擴充 hello Azure 應用程式所使用的 Azure 儲存體帳戶](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a>了解開發人員功能
根據 hello 定價層，hello 開發人員導向的可用功能如下：

### <a name="bitness"></a>位元
* hello**基本**，**標準**，和**Premium**層支援 64 位元和 32 位元應用程式。
* hello**免費**和**共用**層支援 32 位元應用程式只計劃。

### <a name="debugger-support"></a>偵錯工具支援
* 偵錯工具支援適用於 hello**免費**，**共用**，和**基本**在每個應用程式服務方案的單一連接模式。
* 偵錯工具支援適用於 hello**標準**和**Premium**在每個應用程式服務方案的五個並行連線的模式。

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a>了解其他功能
* 如需所有 hello 剩餘 hello App Service 中的功能的詳細資訊計劃，包括定價和功能感興趣 tooall 使用者 （包括開發人員），請參閱[應用程式服務定價詳細資料](https://azure.microsoft.com/pricing/details/web-sites/)。

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務已啟動，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡，無需承諾。
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a>後續步驟
* tooget 開始使用 Azure，請參閱[Microsoft Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* 如需定價、 支援和 SLA 資訊，請造訪下列連結查看 hello。
  
    [資料傳輸定價詳細資料](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [Microsoft Azure 支援方案](https://azure.microsoft.com/support/plans/)
  
    [服務等級協定](https://azure.microsoft.com/support/legal/sla/)
  
    [SQL Database 定價詳細資料](https://azure.microsoft.com/pricing/details/sql-database/)
  
    [Microsoft Azure 的虛擬機器和雲端服務大小][vmsizes]
  
    [App Service 定價詳細資料](https://azure.microsoft.com/pricing/details/app-service/)
  
    [App Service 定價詳細資料 - SSL 連線](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* 如需 Azure App Service 最佳作法 (包括建置可調整且具彈性的架構) 的詳細資訊，請參閱 [最佳作法：Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx)。
* 調整 App Service 應用程式的相關影片，請參閱下列資源的 hello:
  
  * [當 Azure 網站-Stefan Schackow tooScale](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [自動調整 Azure 網站、CPU 或排程 - Stefan Schackow](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [如何調整 Azure 網站 - Stefan Schackow](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

<!-- LINKS -->
[vmsizes]:/pricing/details/app-service/
[SQLaccountsbilling]:http://go.microsoft.com/fwlink/?LinkId=234930
[azuresubscriptions]:http://go.microsoft.com/fwlink/?LinkID=235288
[portal]: https://portal.azure.com/

<!-- IMAGES -->
[ChooseWHP]: ./media/web-sites-scale/scale1ChooseWHP.png
[ChooseBasicInstances]: ./media/web-sites-scale/scale2InstancesBasic.png
[SaveButton]: ./media/web-sites-scale/05SaveButton.png
[BasicComplete]: ./media/web-sites-scale/06BasicComplete.png
[ScaleStandard]: ./media/web-sites-scale/scale3InstancesStandard.png
[Autoscale]: ./media/web-sites-scale/scale4AutoScale.png
[SetTargetMetrics]: ./media/web-sites-scale/scale5AutoScaleTargetMetrics.png
[SetFirstRule]: ./media/web-sites-scale/scale6AutoScaleFirstRule.png
[SetSecondRule]: ./media/web-sites-scale/scale7AutoScaleSecondRule.png
[SetThirdRule]: ./media/web-sites-scale/scale8AutoScaleThirdRule.png
[SetRulesFinal]: ./media/web-sites-scale/scale9AutoScaleFinal.png
[ResourceGroup]: ./media/web-sites-scale/scale10ResourceGroup.png
[ScaleDatabase]: ./media/web-sites-scale/scale11SQLScale.png
[GeoReplication]: ./media/web-sites-scale/scale12SQLGeoReplication.png
