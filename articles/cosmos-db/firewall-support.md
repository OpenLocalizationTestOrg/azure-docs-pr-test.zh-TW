---
title: "Azure Cosmos DB 防火牆支援和 IP 存取控制 | Microsoft Docs"
description: "了解如何使用 IP 存取控制原則進行 Azure Cosmos DB 資料庫帳戶上的防火牆支援。"
keywords: "IP 存取控制，防火牆支援"
services: cosmos-db
author: shahankur11
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: c1b9ede0-ed93-411a-ac9a-62c113a8e887
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/02/2018
ms.author: ankshah
ms.openlocfilehash: 85f5e0e076f92afc79ed8f4ce652bb0f31923113
ms.sourcegitcommit: 9ea2edae5dbb4a104322135bef957ba6e9aeecde
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/03/2018
---
# <a name="azure-cosmos-db-firewall-support"></a>Azure Cosmos DB 防火牆支援
為了保護 Azure Cosmos DB 資料庫帳戶中所儲存的資料，Azure Cosmos DB 已支援利用強式雜湊式訊息驗證碼 (HMAC) 的密碼型[授權模型](https://msdn.microsoft.com/library/azure/dn783368.aspx)。 現在，除了密碼型授權模型之外，Azure Cosmos DB 還支援使用原則驅動的 IP 型存取控制來進行輸入防火牆支援。 此模型與傳統資料庫系統的防火牆規則相類似，且可為 Azure Cosmos DB 資料庫帳戶提供額外的安全性層級。 您現在可以使用這個模型，設定只能從一組核准的電腦和 (或) 雲端服務存取 Azure Cosmos DB 資料庫帳戶。 透過這些核准的電腦和服務組合來存取 Azure Cosmos DB 資源，仍然需要呼叫者呈現有效的授權權杖。

## <a name="ip-access-control-overview"></a>IP 存取控制概觀
只要要求伴隨有效的授權權杖，預設就可以從公用網際網路存取 Azure Cosmos DB 資料庫帳戶。 若要設定 IP 原則型存取控制，使用者必須以 CIDR 形式提供這組 IP 位址或 IP 位址範圍，以作為指定資料庫帳戶的允許用戶端 IP 清單。 一旦套用此設定時，伺服器會封鎖來自此允許清單外機器的所有要求。  下圖說明 IP 型存取控制的連線處理流程：

![顯示 IP 型存取控制之連接程序的圖表](./media/firewall-support/firewall-support-flow.png)

## <a id="configure-ip-policy"></a> 設定 IP 存取控制原則
可以設定 IP 存取控制原則，在 Azure 入口網站，或以程式設計方式透過[Azure CLI](cli-samples.md)， [Azure Powershell](powershell-samples.md)，或[REST API](/rest/api/documentdb/)藉由更新**ipRangeFilter**屬性。 

若要設定 IP 存取控制原則，在 Azure 入口網站，瀏覽至 [Azure Cosmos DB 帳戶] 頁面中，按一下**防火牆**導覽功能表，然後變更**啟用 IP 存取控制**值**ON**。 

![顯示如何在 Azure 入口網站中開啟 [防火牆] 頁面的螢幕擷取畫面](./media/firewall-support/azure-portal-firewall.png)

一旦 IP 存取控制在之後，入口網站會提供參數以啟用存取 Azure 入口網站、 其他 Azure 服務，以及目前的 IP。 下列各節會提供有關這些參數的其他資訊。

![顯示如何在 Azure 入口網站中進行防火牆設定的螢幕擷取畫面](./media/firewall-support/azure-portal-firewall-configure.png)

> [!NOTE]
> 啟用 Azure Cosmos DB 資料庫帳戶的 IP 存取控制原則，即會封鎖所設定之允許 IP 位址範圍清單外部的電腦對您 Azure Cosmos DB 資料庫帳戶的所有存取。 透過這個模型，也會封鎖從入口網站瀏覽資料平面作業，確保存取控制的完整性。

## <a name="connections-from-the-azure-portal"></a>從 Azure 入口網站的連線 

當您以程式設計方式啟用 IP 存取控制原則時，您需要加入在 Azure 入口網站的 IP 位址**ipRangeFilter**維護存取的屬性。 入口網站 IP 位址是：

|區域|IP 位址|
|------|----------|
|所有區域 (下面指定的區域除外)|104.42.195.92、40.76.54.131、52.176.6.30、52.169.50.45、52.187.184.26|
|德國|51.4.229.218|
|中國|139.217.8.252|
|US Gov|52.244.48.71|

若要啟用存取 Azure 入口網站，透過 Azure 入口網站中，將**允許存取 Azure 入口網站**值設定為**ON**在 Azure 入口網站 (**啟用 IP 存取控制**值必須設定為**ON**來檢視和變更**允許存取 Azure 入口網站**值)。

![顯示如何啟用 Azure 入口網站存取螢幕擷取畫面](./media/firewall-support/enable-azure-portal.png)

## <a name="connections-from-other-azure-paas-services"></a>來自其他 Azure PaaS 服務連線 
在 Azure 中，以 Azure Cosmos DB 搭配使用 Azure Stream analytics、 Azure 函式和 Azure App Service 等的 PaaS 服務。 若要啟用存取 Azure Cosmos DB 資料庫從其 IP 位址還無法使用這些服務的帳戶新增到允許清單，以程式設計的方式，與您的 Azure Cosmos DB 資料庫帳戶相關聯的 IP 位址的 IP 位址 0.0.0.0 或設定**允許存取 Azure 服務**Azure 入口網站中的值設為 ON (**啟用 IP 存取控制**值必須設定為**ON**來檢視和變更**允許存取 Azure 服務**值)。 這可確保 Azure PaaS 服務可以存取 Azure Cosmos DB 帳戶。 

![顯示如何在 Azure 入口網站中開啟 [防火牆] 頁面的螢幕擷取畫面](./media/firewall-support/enable-azure-services.png)

## <a name="connections-from-your-current-ip"></a>從目前的 IP 連線

為了簡化開發工作，Azure 入口網站可協助您識別用戶端電腦的 IP 並新增至允許清單，讓您電腦上執行的應用程式可以存取 Azure Cosmos DB 帳戶。 此處的用戶端 IP 位址是入口網站所偵測到的。 它可能是您電腦的用戶端 IP 位址，但也可能是網路閘道的 IP 位址。 移至生產環境之前，別忘記移除它。

![螢幕擷取畫面顯示如何設定防火牆設定為目前的 IP](./media/firewall-support/enable-current-ip.png)

## <a name="connections-from-cloud-services"></a>從雲端服務的連接
在 Azure 中，雲端服務是使用 Azure Cosmos DB 裝載中介層服務邏輯的常見方式。 若要從雲端服務存取 Azure Cosmos DB 資料庫帳戶，必須[設定 IP 存取控制原則](#configure-ip-policy)，以將雲端服務的公用 IP 位址新增至與 Azure Cosmos DB 資料庫帳戶相關聯的允許 IP 位址清單。  這確保雲端服務的所有角色執行個體都能存取您的 Azure Cosmos DB 資料庫帳戶。 您可以在 Azure 入口網站中擷取雲端服務的 IP 位址，如下列螢幕擷取畫面所示：

![這個螢幕擷取畫面顯示 Azure 入口網站中所顯示雲端服務的公用 IP 位址](./media/firewall-support/public-ip-addresses.png)

當您新增其他角色執行個體來相應放大雲端服務時，那些新的執行個體將可自動存取 Azure Cosmos DB 資料庫帳戶，因為它們是相同雲端服務的一部分。

## <a name="connections-from-virtual-machines"></a>從虛擬機器的連接
您也可以使用[虛擬機器](https://azure.microsoft.com/services/virtual-machines/)或[虛擬機器擴展集](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)，透過 Azure Cosmos DB 裝載中介層服務。  若要設定允許從虛擬機器存取 Azure Cosmos DB 資料庫帳戶，必須[設定 IP 存取控制原則](#configure-ip-policy)，以將虛擬機器和 (或) 虛擬機器擴展集的公用 IP 位址設定為 Azure Cosmos DB 資料庫帳戶的其中一個允許 IP 位址。 您可以在 Azure 入口網站中擷取虛擬機器的 IP 位址，如下列螢幕擷取畫面所示。

![這個螢幕擷取畫面顯示 Azure 入口網站中所顯示虛擬機器的公用 IP 位址](./media/firewall-support/public-ip-addresses-dns.png)

當您將其他虛擬機器執行個體新增至群組時，它們即可自動存取您的 Azure Cosmos DB 資料庫帳戶。

## <a name="connections-from-the-internet"></a>從網際網路的連接
從網際網路上的電腦存取 Azure Cosmos DB 資料庫帳戶時，必須將電腦的用戶端 IP 位址或 IP 位址範圍新增至 Azure Cosmos DB 資料庫帳戶的允許 IP 位址清單。 

## <a name="troubleshooting-the-ip-access-control-policy"></a>針對 IP 存取控制原則進行疑難排解
### <a name="portal-operations"></a>入口網站作業
啟用 Azure Cosmos DB 資料庫帳戶的 IP 存取控制原則，即會封鎖所設定之允許 IP 位址範圍清單外部的電腦對您 Azure Cosmos DB 資料庫帳戶的所有存取。 因此如果您想要啟用入口網站的資料平面作業，例如瀏覽集合和查詢文件，您需要明確地允許存取 Azure 入口網站使用**防火牆**入口網站中的頁面。 

![顯示如何允許存取 Azure 入口網站的螢幕擷取畫面](./media/firewall-support/enable-azure-portal.png)

### <a name="sdk--rest-api"></a>SDK & Rest API
基於安全性考量，如果從電腦透過 SDK 或 REST API 的存取不在允許清單上，則會傳回沒有其他詳細資料的一般「404 找不到」回應。 請確認您針對 Azure Cosmos DB 資料庫帳戶設定的 IP 允許清單，以確保會將正確的原則組態套用至您的 Azure Cosmos DB 資料庫帳戶。

## <a name="next-steps"></a>後續步驟
如需網路相關的效能提示的資訊，請參閱[效能祕訣](performance-tips.md)。

