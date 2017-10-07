---
title: "aaaConnect tooAzure 資料湖存放區從 Vnet |Microsoft 文件"
description: "從 Azure Vnet 連接 tooAzure 資料湖存放區"
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 683fcfdc-cf93-46c3-b2d2-5cb79f5e9ea5
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c695dcf49fe4e1a87a90729cf085a938f3b51fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-data-lake-store-from-vms-within-an-azure-vnet"></a>從 Azure VNET 內的 VM 存取 Azure Data Lake Store
Azure Data Lake Store 使用公用網際網路 IP 位址執行的 PaaS 服務。 通常可以連接 toohello 公用網際網路可以任何伺服器連接 tooAzure Data Lake Store 端點。 根據預設，Azure Vnet 中的所有 Vm 可以存取 hello 網際網路，並且因此可存取 Azure 資料湖存放區。 不過，很可能 tooconfigure Vm 在 VNET toonot 有存取 toohello 網際網路。 對於這類的 Vm，存取 tooAzure 資料湖存放區也會是受限制。 封鎖公用網際網路存取 Azure Vnet 中的 Vm，才可以使用任何 hello 遵循方法。

* 藉由設定網路安全性群組 (NSG)
* 藉由設定使用者定義路由 (UDR)
* 藉由交換路由 BGP （業界標準動態路由通訊協定） 透過 ExpressRoute 使用該區塊時存取 toohello 網際網路

在本文中，您將學習 tooenable 如何從 Azure Vm 已經限制的 tooaccess 上面所列的其中一種 hello 三種方法使用的資源存取 toohello Azure 資料湖存放區。

## <a name="enabling-connectivity-tooazure-data-lake-store-from-vms-with-restricted-connectivity"></a>使用受限制的連線啟用連線 tooAzure Vm 所傳來的資料湖存放區
tooaccess Azure 資料湖存放區從這類 Vm，您必須設定這些 tooaccess hello Azure Data Lake Store 帳戶所在的 hello IP 位址。 您也可以解決您的帳戶 hello DNS 名稱的 Data Lake Store 帳戶識別 hello IP 位址 (`<account>.azuredatalakestore.net`)。 對此您可以使用 **nslookup** 之類的工具。 開啟您的電腦上的命令提示字元並執行下列命令的 hello。

    nslookup mydatastore.azuredatalakestore.net

hello 輸出看起來像下列 hello。 hello 根據值**位址**屬性是 hello Data Lake Store 帳戶相關聯的 IP 位址。

    Non-authoritative answer:
    Name:    1434ceb1-3a4b-4bc0-9c69-a0823fd69bba-mydatastore.projectcabostore.net
    Address:  104.44.88.112
    Aliases:  mydatastore.azuredatalakestore.net


### <a name="enabling-connectivity-from-vms-restricted-by-using-nsg"></a>使用 NSG 從受限制的 VM 啟用連線
當 NSG 規則為內部使用 tooblock 會存取 toohello 網際網路，那麼您可以建立另一個 NSG 可存取 toohello 資料湖存放區的 IP 位址。 NSG 規則的詳細資訊位於[什麼是網路安全性群組？](../virtual-network/virtual-networks-nsg.md)。 如需有關如何查看 toocreate Nsg 指示[toomanage Nsg 使用 hello Azure 入口網站的方式](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)。

### <a name="enabling-connectivity-from-vms-restricted-by-using-udr-or-expressroute"></a>使用 UDR 或 ExpressRoute 從受限制的 VM 啟用連線
使用的 tooblock 存取 toohello 網際網路 UDRs 或 BGP 交換路由的路由時，特殊的路由必須 toobe 設定，讓這類的子網路中的 Vm 可以存取資料湖存放區的端點。 如需詳細資訊，請參閱[什麼是使用者定義路由？](../virtual-network/virtual-networks-udr-overview.md)。 如需建立 UDR 的指示，請參閱[在 Resource Manager 中建立 UDR](../virtual-network/virtual-network-create-udr-arm-ps.md)。

### <a name="enabling-connectivity-from-vms-restricted-by-using-expressroute"></a>使用 ExpressRoute 從受限制的 VM 啟用連線
當設定 ExpressRoute 電路時，hello 在內部部署伺服器可以存取資料湖存放區透過公用互連。 如需針對公用互連設定 ExpressRoute 的詳細資訊，請參閱 [ExpressRoute 常見問題集](../expressroute/expressroute-faqs.md)。

## <a name="see-also"></a>另請參閱
* [Azure 資料湖儲存區概觀](data-lake-store-overview.md)
* [保護儲存在 Azure Data Lake Store 中的資料](data-lake-store-security-overview.md)

