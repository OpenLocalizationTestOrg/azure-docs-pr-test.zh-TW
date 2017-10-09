---
title: "Azure 環境中的 Oracle 嚴重損壞修復案例的 aaaOverview |Microsoft 文件"
description: "Azure 環境中 Oracle Database 12c 資料庫的災害復原案例"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/2/2017
ms.author: rclaus
ms.openlocfilehash: 1fa69e1ba044b46b27695fec92fd9ca82df796f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a>Azure 環境中 Oracle Database 12c 資料庫的災害復原

## <a name="assumptions"></a>假設

- 您已了解 Oracle Data Guard 的設計和 Azure 環境。


## <a name="goals"></a>目標
- 設計 hello 拓撲和組態，您的需求災害復原 (DR)。

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a>案例 1：Azure 上的主要和 DR 站台

客戶擁有 Oracle 資料庫設定 hello 主要站台上。 DR 站台位於不同的區域中。 hello 客戶可使用 Oracle 資料保護這些站台間快速復原。 hello 主要站台也會有次要資料庫以進行報告和其他用途。 

### <a name="topology"></a>拓撲

Hello Azure 安裝程式的摘要如下：

- 兩個站台 (主要站台和 DR 站台)
- 兩個虛擬網路
- 兩個具有 Data Guard 的 Oracle 資料庫 (主要和待命)
- 兩個具有 Golden Gate 或 Data Guard 的 Oracle 資料庫 (僅限主要站台)
- 兩個應用程式服務，一個主要，一個 hello DR 網站上
- *可用性設定組，*用 hello 主要站台上的資料庫和應用程式服務
- 在每個站台，這會限制存取 toohello 私人網路，並只讓登入系統管理員一個 jumpbox
- Jumpbox、應用程式服務、資料庫和 VPN 閘道位於不同的子網路
- 對應用程式和資料庫子網路強制執行 NSG

![Hello DR 拓樸 頁面的螢幕擷取畫面](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a>案例 2：內部部署環境的主要站台和 Azure 上的 DR 站台

客戶具有內部部署 Oracle 資料庫設定 (主要站台)。 DR 站台是在 Azure 上。 Oracle Data Guard 用於這些站台間的快速復原。 hello 主要站台也會有次要資料庫以進行報告和其他用途。 

這項設定有兩種方法。

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-hello-firewall"></a>方法 1： 在內部部署與 Azure，需要 hello 防火牆上的開啟 TCP 連接埠之間的直接連接 

我們不建議直接連接，因為其會公開外部 world hello TCP 連接埠 toohello。

#### <a name="topology"></a>拓撲

以下是 hello Azure 安裝程式的摘要：

- 一個 DR 站台 
- 一個虛擬網路
- 一個具有 Data Guard 的 Oracle 資料庫 (使用中)
- Hello DR 網站上的一個應用程式服務
- 一個 jumpbox，這會限制存取 toohello 私人網路，並只讓登入系統管理員
- Jumpbox、應用程式服務、資料庫和 VPN 閘道位於不同的子網路
- 對應用程式和資料庫子網路強制執行 NSG
- NSG 規則原則/tooallow 輸入 TCP 連接埠 1521年 （或使用者定義的連接埠）
- NSG 規則原則/toorestrict 只有 hello IP 位址/位址在內部部署 （資料庫或應用程式） tooaccess hello 虛擬網路

![Hello DR 拓樸 頁面的螢幕擷取畫面](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a>方法 2：站對站 VPN
站對站 VPN 是更好的方法。 如需設定 VPN 的詳細資訊，請參閱[使用 CLI 建立具有站對站 VPN 連線的虛擬網路](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli)。

#### <a name="topology"></a>拓撲

以下是 hello Azure 安裝程式的摘要：

- 一個 DR 站台 
- 一個虛擬網路 
- 一個具有 Data Guard 的 Oracle 資料庫 (使用中)
- Hello DR 網站上的一個應用程式服務
- 一個 jumpbox，這會限制存取 toohello 私人網路，並只讓登入系統管理員
- Jumpbox、應用程式服務、資料庫和 VPN 閘道位於不同的子網路
- 對應用程式和資料庫子網路強制執行 NSG
- 內部部署與 Azure 之間的站對站 VPN 連線

![Hello DR 拓樸 頁面的螢幕擷取畫面](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a>其他閱讀資料

- [在 Azure 上設計和實作 Oracle 資料庫](oracle-design.md)
- [設定 Oracle Data Guard](configure-oracle-dataguard.md)
- [設定 Oracle Golden Gate](configure-oracle-golden-gate.md)
- [Oracle 備份和復原](oracle-backup-recovery.md)


## <a name="next-steps"></a>後續步驟

- [教學課程︰建立高可用性 VM](../../linux/create-cli-complete.md)
- [瀏覽 VM 部署 Azure CLI 範例](../../linux/cli-samples.md)
