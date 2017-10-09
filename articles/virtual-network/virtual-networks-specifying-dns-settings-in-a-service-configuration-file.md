---
title: "aaaSpecifying 服務組態檔中的 DNS 設定 |Microsoft 文件"
description: "使用虛擬網路的服務組態檔指定自訂的 DNS 設定"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 467a4b99-8691-40b3-b640-e25e49675c71
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/24/2016
ms.author: jdial
ms.openlocfilehash: f192e33566dd8e669da04e6378a0c8e4b0b35ecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a>指定服務組態檔中的 DNS 設定
## <a name="dns-elements"></a>DNS 項目
服務組態檔可能包含 DnsServers 元素與 hello hello 服務將使用的網域名稱系統 (DNS) 伺服器的 IPv4 位址的清單。 Hello 服務組態檔中的設定優先於 hello 網路組態檔中設定。 如需詳細資訊，請參閱 [Azure 服務組態結構描述 (.cscfg 檔)](https://msdn.microsoft.com/library/azure/ee758710.aspx)。

**NetworkConfiguration 項目**

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> hello**名稱**中 hello 屬性**DnsServer**項目作為參考名稱。 它不代表 hello hello DNS 伺服器的主機名稱。 每個**DnsServer**屬性值必須是唯一的 hello 整個 Microsoft Azure 訂用帳戶。
> 
> 

## <a name="see-also"></a>另請參閱
[Azure 服務組態結構描述 (.cscfg)](https://msdn.microsoft.com/library/windowsazure/ee758710)

[Azure 虛擬網路組態結構描述](http://go.microsoft.com/fwlink/?LinkId=248093)

[使用網路組態檔設定虛擬網路](http://go.microsoft.com/fwlink/?LinkId=248094)

[關於 hello 管理入口網站中的虛擬網路設定](http://go.microsoft.com/fwlink/?LinkId=248092)

