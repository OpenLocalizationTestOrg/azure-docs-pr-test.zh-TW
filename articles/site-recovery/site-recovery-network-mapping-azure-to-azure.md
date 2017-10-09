---
title: "Azure Site Recovery 中的兩個 Azure 區域之間的 aaaNetwork 對應 |Microsoft 文件"
description: "Azure Site Recovery 會協調 hello 複寫、 容錯移轉和復原的虛擬機器和實體伺服器。 深入了解容錯移轉 tooAzure 或次要資料中心。"
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 4f80c44e3f94eaf446bc01a7041d91fe34aa78d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="network-mapping-between-two-azure-regions"></a>兩個 Azure 區域間的網路對應


本文說明如何 toomap Azure 虛擬網路的兩個彼此的 Azure 區域。 網路對應可確保當 hello 目標 Azure 區域中建立複寫的虛擬機器時，它會建立 hello 是對應的 toovirtual hello 來源虛擬機器網路的虛擬網路上。  

## <a name="prerequisites"></a>必要條件
對應網路之前，請確定您已在來源和目標 Azure 區域中建立 [Azure 虛擬網路](../virtual-network/virtual-networks-overview.md)。

## <a name="map-networks"></a>對應網路

toomap 一個 Azure 區域 tooanother 虛擬網路在其他區域中，移 tooSite Recovery 基礎結構中的 Azure 虛擬網路]-> [網路對應 （適用於 Azure 虛擬機器），並建立網路對應。

![網路對應](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


在 hello 例會我的虛擬機器在東亞地區執行，而且正在複寫 tooSoutheast 亞洲。

選取 hello 來源和目標網路，然後按一下確定 toocreate 東亞 tooSoutheast 亞洲的網路對應。

![網路對應](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


請勿 hello 同一件事 toocreate 東南亞 tooEast 亞洲的網路對應。  
![網路對應](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a>啟用複寫時對應網路

如果您要將虛擬機器的 hello 第一次表單一個 Azure 區域 tooanother 複寫時未完成網路對應，然後您可以選擇目標網路一部分 hello 相同的程序。 站台復原會在從來源區域 tootarget 地區和這個選取的目標地區 toosource 區域建立網路對應。   

![網路對應](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

根據預設，站台復原會建立網路是相同的 toohello 來源網路的 hello 目標區域中，並加上 '-asr' 後置詞 toohello hello 來源網路的名稱。 您可以按一下 [自訂] 選擇已建立的網路。

![網路對應](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


如果已完成 hello 網路對應，您無法啟用複寫時變更 hello 目標虛擬網路。 toochange，修改現有的網路對應。  

![網路對應](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![網路對應](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> 如果您修改區域 1 tooregion-2 的網路對應，請確定您修改區域 2 tooregion-1 以及從 hello 網路對應。
>
>


## <a name="subnet-selection"></a>子網路選取項目
Hello 目標虛擬機器的子網路，選取上 hello hello hello 來源虛擬機器的子網路名稱。 Hello 的子網路是否名稱相同的 hello hello 目標網路，在可用的來源虛擬機器則可替 hello 目標虛擬機器。 如果沒有 hello 的子網路名稱相同 hello 目標網路，然後選擇依字母順序的第一個子網路是因為 hello 目標子網路。 您可以修改此子網路移 tooCompute 和 hello 虛擬機器的網路設定。

![修改子網路](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a>IP 位址

選擇每個 hello hello 目標虛擬機器網路介面的 IP 位址，如下所示：

### <a name="dhcp"></a>DHCP
如果 hello hello 來源虛擬機器網路介面使用 DHCP，然後 hello 目標虛擬機器的網路介面也會設為 DHCP。

### <a name="static-ip"></a>靜態 IP
如果 hello 網路介面的 hello 來源虛擬機器使用靜態 IP，然後 hello 目標虛擬機器的網路介面也會設 toouse 靜態 IP。 選擇靜態 IP 的方式如下所示：

#### <a name="same-address-space"></a>相同的位址空間

如果 hello 來源子網路和 hello 目標子網路有 hello 相同，則目標 IP 已設定相同的 hello hello 來源虛擬機器網路介面的 hello IP 位址空間。 如果找不到相同的 IP，然後其他可用的 IP 會設定為 hello 目標 IP。

#### <a name="different-address-space"></a>不同的位址空間

如果 hello 來源的子網路和 hello 目標子網路具有不同的位址空間，做為 hello 目標子網路中任何可用的 IP 設定目標 IP。

您可以修改每個網路介面上的 hello 目標 IP 移 tooCompute 和 hello 虛擬機器的網路設定。

## <a name="next-steps"></a>後續步驟

- 深入了解[複寫 Azure VM 的網路指引](site-recovery-azure-to-azure-networking-guidance.md)。
