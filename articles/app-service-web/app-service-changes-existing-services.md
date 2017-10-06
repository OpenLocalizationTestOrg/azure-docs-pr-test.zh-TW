---
title: "aaaAzure 應用程式服務，它對現有的 Azure 服務的影響"
description: "說明如何 hello 新的 Azure 應用程式服務和其功能會影響在 Azure 中現有的服務。"
services: app-service
documentationcenter: 
author: yochay
manager: nirma
editor: 
ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
ms.author: yochaykk
ms.openlocfilehash: a831a88fee38465e5b0b7c2c2340cf8a0d64c864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a>Azure App Service 和現有的 Azure 服務
本文概述 Azure 服務的 hello 變更 toobring 一起一部分到數個 Azure 服務的 hello 變更 tooexisting [Azure App Service](https://azure.microsoft.com/services/app-service/)，新的整合式供應項目。

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a>概觀
[Azure App Service](https://azure.microsoft.com/services/app-service/)是新的且唯一的雲端服務，可讓開發人員 toocreate web 和行動應用程式的任何平台和任何裝置。 應用程式服務是設計的整合式的解決方案 toostreamline 重複程式碼撰寫函式、 整合企業和 SaaS 系統並自動化商務程序，同時滿足您需求的安全性、 可靠性和延展性。

結合 hello 遵循現有的 Azure 應用程式服務。 服務-[網站](https://azure.microsoft.com/services/websites/)，[行動服務](https://azure.microsoft.com/services/mobile-services/)，和[Biztalk 服務](https://azure.microsoft.com/services/biztalk-services/)到單一組合服務時加入功能強大的新功能。  應用程式服務可讓您 toohost hello 下列應用程式類型：

* Web Apps
* Mobile Apps
* API Apps
* Logic Apps

hello 下表說明如何在現有的 Azure 服務對應 tooApp Service 和 hello 應用程式類型中可用。

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%">現有 Azure 服務</th>
<th align="left", style="width:10%">Azure App Service</th>
<th align="left", style="width:80%">變更內容</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Azure 網站</td>
<td align="left">Web Apps</td>
<td align="left"><li>Azure 網站的應用程式服務是嚴格限制的 toochanging hello 名稱網站 tooWeb 應用程式。
<p><li>所有您的現有網站執行個體現在都是 App Service 中的 Web Apps。</p>
<p><li>您可以存取您現有的網站，透過 hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure 入口網站</a>，其中您會發現下的所有現有站台<em>Web 應用程式</em>。</p>
<p><li><em>Web 主控方案</em>現在<em>App Service 方案</em>。 <em>App Service 方案</em>可以裝載 App Service 類型的任何應用程式，例如 Web、行動、邏輯或 API 應用程式。</p>
<p><li>Azure App Service Web Apps 已正式推出。</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/web/">深入了解 Web 應用程式</a>。</p></td>
</tr>
<tr class="even">
<td align="left">Azure 行動服務</td>
<td align="left">Mobile Apps</td>
<td align="left"><p><li>行動服務繼續 toobe 可用為獨立服務，並保留完整支援。</p>
<p><li>行動應用程式是在應用程式服務中，以便將所有的行動服務等等的 hello 功能整合的應用程式類型。</p>
<p><li>它也很簡單<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">從行動服務 tooMobile 應用程式移轉</a>。</p>
<p><li>由於隸屬於 App Service，Mobile Apps 可以取得行動服務以外的新功能，例如與內部部署和 SaaS 系統整合、預備位置、更好的縮放選項，以及其他。</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/mobile/">深入了解行動應用程式</a>。</p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">API 應用程式</td>
<td align="left">
<p><li>應用程式開發介面應用程式是在應用程式服務，可讓您輕鬆地建立和使用 hello 雲端中的應用程式開發介面中的新應用程式類型。</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/api/">深入了解 API Apps</a>。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">Logic Apps</td>
<td align="left">
<p><li>Logic Apps 是 App Service 中的新應用程式類型，可讓您輕鬆地自動化商務程序。</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/logic/">深入了解 Logic Apps</a>。</p></td>
</tr>
<tr class="odd">
<td align="left">Azure BizTalk 服務</td>
<td align="left">BizTalk API 應用程式</td>
<td align="left">
<li><p>BizTalk 服務繼續 toobe 可用為獨立服務，並保留完整支援。</p>
<li><p>API 應用程式啟用使用者 tooperform 企業應用程式整合以及 B2B 整合案例的任何 App Service 中的 hello 應用程式類型，所有的 BizTalk 服務的 hello 功能已整合到應用程式服務。</p>
<li><p>您現在可以使用邏輯應用程式，自動化商務程序使用視覺化設計體驗 toocreate 工作流程。</p></td>
</tr>
</tbody>
</table>

toolearn 詳細資訊，請瀏覽[應用程式服務文件](https://azure.microsoft.com/documentation/services/app-service/)。

