---
title: "aaaAzure Cosmos DB 防火牆支援與 IP 存取控制 |Microsoft 文件"
description: "了解防火牆 toouse IP 存取控制原則如何支援 Azure Cosmos DB 資料庫帳戶。"
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
ms.date: 05/22/2017
ms.author: ankshah
ms.openlocfilehash: b5cdbdb28e9d7ee0fd0ea54aad277167b699929f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-firewall-support"></a>Azure Cosmos DB 防火牆支援
toosecure 資料儲存在 Azure Cosmos DB 資料庫帳戶，Azure Cosmos 資料庫提供支援為基礎的密碼[授權模型](https://msdn.microsoft.com/library/azure/dn783368.aspx)，利用強式雜湊式訊息驗證碼 (HMAC)。 現在，此外 toohello 密碼型授權模型，Azure Cosmos DB 支援原則導向的連入的防火牆支援 IP 為基礎的存取控制項。 此模型是非常類似傳統的資料庫系統的 toohello 防火牆規則，並提供額外一層的安全性 toohello Azure Cosmos DB 資料庫帳戶。 使用這個模型，您可以現在設定 Azure Cosmos DB 資料庫帳戶 toobe 只能從機器的核准設定組和/或雲端服務。 從這些已核准的機器和服務集合的存取 tooAzure Cosmos DB 資源仍然需要 hello 呼叫端 toopresent 有效的授權權杖。

## <a name="ip-access-control-overview"></a>IP 存取控制概觀
根據預設，Azure Cosmos DB 資料庫帳戶是可從公用網際網路存取，只要 hello 要求伴隨著有效的授權權杖。 tooconfigure IP 以原則為基礎的存取控制，hello 使用者必須提供 hello 組 IP 位址或 CIDR 形式 toobe 包含做為 hello 允許指定的資料庫帳戶的用戶端 Ip 清單中的 IP 位址範圍。 一旦套用此設定時，源自於此的允許清單外機器的所有要求將會都封鎖 hello 伺服器。  hello 下列圖表中所述的處理 hello IP 為基礎的存取控制流程的 hello 連接。

![顯示 hello 連線程序以 IP 為基礎的存取控制的圖表](./media/firewall-support/firewall-support-flow.png)

## <a name="connections-from-cloud-services"></a>從雲端服務的連接
在 Azure 中，雲端服務是使用 Azure Cosmos DB 裝載中介層服務邏輯的極常見方式。 tooenable 存取 tooan Azure Cosmos DB 資料庫帳戶從雲端服務，hello 雲端服務的 hello 公用 IP 位址必須是允許清單與您的 Azure Cosmos DB 資料庫帳戶所關聯的 IP 位址加入的 toohello[設定hello IP 存取控制原則](#configure-ip-policy)。  這可確保雲端服務的所有角色執行個體都有存取 tooyour Azure Cosmos DB 資料庫帳戶。 Hello 下列螢幕擷取畫面所示，您可以擷取 hello Azure 入口網站中的雲端服務的 IP 位址。

![螢幕擷取畫面顯示 hello Azure 入口網站中的雲端服務的 hello 公用 IP 位址](./media/firewall-support/public-ip-addresses.png)

當您藉由加入其他角色執行個體擴展您的雲端服務時，這些新的執行個體就會自動擁有存取 toohello Azure Cosmos DB 資料庫帳戶因為它們屬於 hello 的相同雲端服務。

## <a name="connections-from-virtual-machines"></a>從虛擬機器的連接
[虛擬機器](https://azure.microsoft.com/services/virtual-machines/)或[虛擬機器擴展集](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)也可以使用的 toohost 使用 Azure Cosmos DB 的中介層服務。  tooconfigure hello Azure Cosmos DB 資料庫帳戶 tooallow 存取的虛擬機器、 虛擬機器和/或虛擬機器規模集的公用 IP 位址必須設定為其中一個允許的 IP 位址，依您 Azure Cosmos DB 資料庫帳戶的 hello[設定 hello IP 存取控制原則](#configure-ip-policy)。 Hello 下列螢幕擷取畫面所示，您可以擷取 hello Azure 入口網站中的虛擬機器的 IP 位址。

![螢幕擷取畫面顯示 hello Azure 入口網站中的虛擬機器的公用 IP 位址](./media/firewall-support/public-ip-addresses-dns.png)

當您新增其他虛擬機器執行個體 toohello 群組時，它們會自動提供存取 tooyour Azure Cosmos DB 資料庫帳戶。

## <a name="connections-from-hello-internet"></a>從連線 hello 網際網路
當您存取 Azure Cosmos DB 資料庫的電腦帳戶 hello 網際網路時，hello 用戶端 IP 位址或 IP 位址範圍的 hello 機器必須加入的 toohello 允許 hello Azure Cosmos DB 資料庫帳戶的 IP 位址的清單。 

## <a id="configure-ip-policy"></a>設定 hello IP 存取控制原則
hello IP 存取控制原則可以設定在 hello Azure 入口網站，或以程式設計方式透過[Azure CLI](cli-samples.md)， [Azure Powershell](powershell-samples.md)，或使用 hello [REST API](/rest/api/documentdb/)藉由更新 hello `ipRangeFilter`屬性。 IP 位址/範圍必須以逗號分隔，而且不得包含任何空格。 範例："13.91.6.132,13.91.6.1/24"。 在更新資料庫帳戶時透過這些方法，是確定 toopopulate 所有 hello 屬性 tooprevent 重設 toodefault 設定。

> [!NOTE]
> 藉由啟用您的 Azure Cosmos DB 資料庫帳戶 IP 存取控制原則，所有存取 tooyour 外 hello 設定機器 Azure Cosmos DB 資料庫帳戶都允許的 IP 位址範圍清單遭到封鎖。 由於此模型中，瀏覽 hello 資料平面作業從 hello 入口網站也會封鎖的 tooensure hello 完整性的存取控制。

toosimplify 開發 hello Azure 入口網站可協助您識別及新增的允許清單中，您用戶端機器 toohello hello IP，以便執行您的電腦的應用程式可以存取 hello Azure Cosmos DB 帳戶。 請注意看見 hello 入口網站偵測到 hello 用戶端 IP 位址。 它可能是您的電腦，hello 用戶端 IP 位址，但也可能是您的網路閘道 hello IP 位址。 不要忘記 tooremove 進行 tooproduction 前面。

tooset hello IP 存取控制原則 hello Azure 入口網站中的瀏覽 toohello Azure Cosmos DB 帳戶 刀鋒視窗中，按一下**防火牆**hello 瀏覽功能表中，然後按一下**ON** 

![顯示如何 tooopen hello hello Azure 入口網站中的防火牆刀鋒視窗的螢幕擷取畫面](./media/firewall-support/azure-portal-firewall.png)

在 hello 新窗格中，指定是否 hello Azure 入口網站可以存取 hello 帳戶和其他位址和範圍視需要加入，然後按一下**儲存**。  

> [!NOTE]
> 當您啟用 IP 存取控制原則時，您會需要 hello Azure 入口網站 toomaintain 存取 tooadd hello IP 位址。 hello 入口網站的 IP 位址為：
> |區域|IP 位址|
> |------|----------|
> |所有區域 (下面指定的區域除外)| 104.42.195.92|
> |德國|51.4.229.218|
> |中國|139.217.8.252|
> |美國政府亞利桑那州|52.244.48.71|
>

![螢幕擷取畫面顯示如何 tooconfigure hello Azure 入口網站中的防火牆設定](./media/firewall-support/azure-portal-firewall-configure.png)

## <a name="troubleshooting-hello-ip-access-control-policy"></a>疑難排解 hello IP 存取控制原則
### <a name="portal-operations"></a>入口網站作業
藉由啟用您的 Azure Cosmos DB 資料庫帳戶 IP 存取控制原則，所有存取 tooyour 外 hello 設定機器 Azure Cosmos DB 資料庫帳戶都允許的 IP 位址範圍清單遭到封鎖。 因此如果您想 tooenable 入口網站的資料平面作業，例如瀏覽集合和查詢文件時，您需要 tooexplicitly 允許使用 hello Azure 入口網站存取**防火牆**hello 入口網站中的刀鋒視窗。 

![螢幕擷取畫面顯示如何 tooenable 存取 toohello Azure 入口網站](./media/firewall-support/azure-portal-access-firewall.png)

### <a name="sdk--rest-api"></a>SDK & Rest API
安全性考量，不能在允許清單的 hello 機器透過 SDK 或 REST API 存取將傳回泛型 404 找不到具有回應沒有其他詳細資料。 請確認 hello IP 允許清單中您的 Azure Cosmos DB 資料庫帳戶 tooensure hello 正確的原則組態設定會套用的 tooyour Azure Cosmos DB 資料庫帳戶。

## <a name="next-steps"></a>後續步驟
如需網路相關效能秘訣的相關資訊，請參閱[效能秘訣](performance-tips.md)。

