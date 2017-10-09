---
title: "aaaSpecifying 虛擬網路組態檔中的 DNS 設定 |Microsoft 文件"
description: "如何使用虛擬網路組態的虛擬網路中的 toochange DNS 伺服器設定檔案中 hello 傳統部署模型"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a8905927-92ac-42b5-8c33-8e42c000692c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: d53a658773e1c930b5a28a701db0be9edd26565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a>指定虛擬網路組態檔中的 DNS 設定
網路組態檔有兩個項目，您可以使用 toospecify 網域名稱系統 (DNS) 設定： **DnsServers**和**DnsServerRef**。 您可以藉由指定其 IP 位址新增的 DNS 伺服器清單，並參考名稱 toohello **DnsServers**項目。 然後您可以使用**DnsServerRef**元素 toospecify hello DnsServers 元素從哪一個 DNS 伺服器項目用於您的虛擬網路內的不同網站。

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

本文涵蓋 hello 傳統部署模型。

hello 網路組態檔可能包含下列項目 hello。 每個項目的 hello 標題為連結的 tooa 頁面，提供其他有關 hello 元素值設定。

> [!IMPORTANT]
> 如需如何 tooconfigure hello 網路組態檔的資訊，請參閱[設定虛擬網路使用網路組態檔](virtual-networks-using-network-configuration-file.md)。 如需 hello 網路組態檔中所包含的每個項目的資訊，請參閱[Azure 虛擬網路組態結構描述](https://msdn.microsoft.com/library/azure/jj157100.aspx)。
> 
> 

[Dns 項目](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> hello**名稱**中 hello 屬性**DnsServer**項目只用來做為參考 hello **DnsServerRef**項目。 它不代表 hello hello DNS 伺服器的主機名稱。 每個**DnsServer**屬性值必須是唯一的 hello 整個 Microsoft Azure 訂用帳戶
> 
> 

[Virtual Network Sites 項目](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> 在順序 toospecify hello Virtual Network Sites 項目這項設定，它必須先在 hello DNS 項目中定義。 hello DnsServerRef*名稱*在 hello Virtual Network Sites 項目必須參考 tooa 名稱值 hello DNS 元素中指定的 DnsServer*名稱*。
> 
> 

## <a name="next-steps"></a>後續步驟
* 了解 hello [Azure 虛擬網路組態結構描述](http://go.microsoft.com/fwlink/?LinkId=248093)。
* 了解 hello [Azure 服務組態結構描述](https://msdn.microsoft.com/library/windowsazure/ee758710)。
* [使用網路組態檔設定虛擬網路](virtual-networks-using-network-configuration-file.md)

