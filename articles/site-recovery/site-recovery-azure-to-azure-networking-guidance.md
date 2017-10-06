---
title: "aaaAzure Site Recovery 從 Azure tooAzure 複寫虛擬機器的網路指引 |Microsoft 文件"
description: "複寫 Azure 虛擬機器的網路指引"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/13/2017
ms.author: sujayt
ms.openlocfilehash: 3a3391b8c3512932d243458fd17d2a2b39248448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="networking-guidance-for-replicating-azure-virtual-machines"></a>複寫 Azure 虛擬機器的網路指引

>[!NOTE]
> Azure 虛擬機器的 Site Recovery 複寫目前為預覽狀態。

本文詳細說明 hello Azure Site Recovery 的網路功能指南，當您使用複寫，從一個區域 tooanother 區域復原 Azure 虛擬機器。 如需 Azure Site Recovery 需求相關資訊，請參閱 hello[必要條件](site-recovery-prereq.md)發行項。

## <a name="site-recovery-architecture"></a>Site Recovery 架構

站台復原提供簡單輕鬆的方式 tooreplicate 應用程式上執行 Azure 虛擬機器 tooanother Azure 區域，讓它們可以 hello 主要區域中的中斷時復原。 深入了解[此案例和 Site Recovery 架構](site-recovery-azure-to-azure-architecture.md)。

## <a name="your-network-infrastructure"></a>網路基礎結構

hello 下列圖表描述 hello 一般 Azure 的環境的 Azure 虛擬機器上執行的應用程式：

![客戶環境](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

如果您使用 Azure ExpressRoute 或 VPN 連線從內部部署網路 tooAzure，hello 環境看起來像這樣：

![客戶環境](./media/site-recovery-azure-to-azure-architecture/source-environment-expressroute.png)

一般而言，客戶會使用防火牆和/或網路安全性群組 (NSG) 保護網路。 hello 防火牆可用來控制網路連線以 URL 為基礎或以 IP 為主的允許清單。 Nsg 可讓規則使用 IP 範圍 toocontrol 網路連線。

>[!IMPORTANT]
> 如果您使用驗證的 proxy toocontrol 網路連線能力，不支援，並無法啟用站台復原的複寫。 

hello 下列各節討論需要從 Azure 虛擬機器的 Site Recovery 複寫 toowork hello 網路的傳出連線變更。

## <a name="outbound-connectivity-for-azure-site-recovery-urls"></a>Azure Site Recovery URL 的輸出連線能力

如果您使用的任何 URL 型防火牆 proxy toocontrol 輸出連線，是確定 toowhitelist 這些需要 Azure Site Recovery 服務 Url:


**URL** | **用途**  
--- | ---
*.blob.core.windows.net | 需要如此可以將資料寫入 toohello 快取儲存體帳戶 hello 來源範圍中從 hello VM。
login.microsoftonline.com | 所需的授權和驗證 toohello Site Recovery 服務 Url。
*.hypervrecoverymanager.windowsazure.com | 必要的以便從 hello VM 進行 hello Site Recovery 服務通訊。
*.servicebus.windows.net | 需要如此 hello 站台復原監視和診斷資料可以寫入從 hello VM。

## <a name="outbound-connectivity-for-azure-site-recovery-ip-ranges"></a>Azure Site Recovery IP 範圍輸出連線能力

>[!NOTE]
> tooautomatically hello 網路安全性群組上建立所需的 hello NSG 規則，您可以[下載並使用此指令碼](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702)。

>[!IMPORTANT]
> * 我們建議您在測試網路安全性群組上建立所需的 hello NSG 規則，並有沒有問題之前先確認您在生產環境網路安全性小組建立 hello 規則。
> * toocreate hello 必要數目 NSG 規則，確保您的訂閱是在允許清單中。 請連絡客戶支援 tooincrease hello NSG 規則限制在您的訂用帳戶。

如果您使用任何 IP 型防火牆 proxy 或 NSG 規則 toocontrol 輸出連線，hello 下列 IP 範圍需要 toobe 白名單，根據 hello hello 虛擬機器的來源和目標位置：

- 所有 IP 範圍對應 toohello 來源位置。 (您可以下載 hello [IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)。)需要允許清單，以便資料可以從 hello VM 寫入 toohello 快取儲存體帳戶。

- 所有的 IP 範圍對應 tooOffice 365[驗證和身分識別的 IP V4 端點](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity)。

    >[!NOTE]
    > 如果新的 Ip 在未來的 hello 加入 tooOffice 365 IP 範圍，您需要 toocreate 新 NSG 規則。
    
- Site Recovery 服務端點 IP ([XML 檔案中提供](https://aka.ms/site-recovery-public-ips))，取決於您的目標位置： 

   **目標位置** | **Site Recovery 服務 IP** |  **Site Recovery 監視 IP**
   --- | --- | ---
   東亞 | 52.175.17.132</br>40.83.121.61 | 13.94.47.61
   東南亞 | 52.187.58.193</br>52.187.169.104 | 13.76.179.223
   印度中部 | 52.172.187.37</br>52.172.157.193 | 104.211.98.185
   印度南部 | 52.172.46.220</br>52.172.13.124 | 104.211.224.190
   美國中北部 | 23.96.195.247</br>23.96.217.22 | 168.62.249.226
   北歐 | 40.69.212.238</br>13.74.36.46 | 52.169.18.8
   西歐 | 52.166.13.64</br>52.166.6.245 | 40.68.93.145
   美國東部 | 13.82.88.226</br>40.71.38.173 | 104.45.147.24
   美國西部 | 40.83.179.48</br>13.91.45.163 | 104.40.26.199
   美國中南部 | 13.84.148.14</br>13.84.172.239 | 104.210.146.250
   美國中部 | 40.69.144.231</br>40.69.167.116 | 52.165.34.144
   美國東部 2 | 52.184.158.163</br>52.225.216.31 | 40.79.44.59
   日本東部 | 52.185.150.140</br>13.78.87.185 | 138.91.1.105
   日本西部 | 52.175.146.69</br>52.175.145.200 | 138.91.17.38
   巴西南部 | 191.234.185.172</br>104.41.62.15 | 23.97.97.36
   澳洲東部 | 104.210.113.114</br>40.126.226.199 | 191.239.64.144
   澳大利亞東南部 | 13.70.159.158</br>13.73.114.68 | 191.239.160.45
   加拿大中部 | 52.228.36.192</br>52.228.39.52 | 40.85.226.62
   加拿大東部 | 52.229.125.98</br>52.229.126.170 | 40.86.225.142
   美國中西部 | 52.161.20.168</br>13.78.230.131 | 13.78.149.209
   美國西部 2 | 52.183.45.166</br>52.175.207.234 | 13.66.228.204
   英國西部 | 51.141.3.203</br>51.140.226.176 | 51.141.14.113
   英國南部 | 51.140.43.158</br>51.140.29.146 | 51.140.189.52

## <a name="sample-nsg-configuration"></a>範例 NSG 組態
本節說明 hello 步驟 tooconfigure NSG 規則，讓站台復原複寫可以在虛擬機器上運作。 如果您要使用 NSG 規則 toocontrol 輸出連線，使用 「 允許 HTTPS 輸出 」 規則的所有必要的 hello IP 範圍。

>[!Note]
> tooautomatically hello 網路安全性群組上建立所需的 hello NSG 規則，您可以[下載並使用此指令碼](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702)。

例如，如果 VM 的來源位置是 「 美國東部"，而且您在複寫目標位置是"Central US"，請遵循 hello 下兩節中的 hello 步驟。

>[!IMPORTANT]
> * 我們建議您在測試網路安全性群組上建立所需的 hello NSG 規則，並有沒有問題之前先確認您在生產環境網路安全性小組建立 hello 規則。
> * toocreate hello 必要數目 NSG 規則，確保您的訂閱是在允許清單中。 請連絡客戶支援 tooincrease hello NSG 規則限制在您的訂用帳戶。 

### <a name="nsg-rules-on-hello-east-us-network-security-group"></a>NSG 規則 hello 美國東部網路安全性群組

* 建立規則，以對應太[East US IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)。 這是必要的以便資料可以從 hello VM 寫入 toohello 快取儲存體帳戶。

* 建立規則的所有 IP 範圍對應 tooOffice 365[驗證和身分識別的 IP V4 端點](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity)。

* 建立對應 toohello 目標位置的規則：

   **位置** | **Site Recovery 服務 IP** |  **Site Recovery 監視 IP**
    --- | --- | ---
   美國中部 | 40.69.144.231</br>40.69.167.116 | 52.165.34.144

### <a name="nsg-rules-on-hello-central-us-network-security-group"></a>NSG 規則 hello 美國中部網路安全性群組

這些規則是必要的使複寫可以從 hello 目標區域 toohello 來源區域的容錯移轉後啟用：

* 規則對應太[中央美國 IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)。 這些是必要的如此可以將資料寫入 toohello 快取儲存體帳戶從 hello VM。

* 規則的所有 IP 範圍對應 tooOffice 365[驗證和身分識別的 IP V4 端點](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity)。

* 對應 toohello 來源位置的規則：

   **位置** | **Site Recovery 服務 IP** |  **Site Recovery 監視 IP**
    --- | --- | ---
   美國東部 | 13.82.88.226</br>40.71.38.173 | 104.45.147.24


## <a name="guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration"></a>適用於現有 Azure 對內部部署 ExpressRoute/VPN 組態的指導方針

如果您有內部部署與 hello 之間 ExpressRoute 或 VPN 連接的來源在 Azure 中的位置，請遵循本節中的 hello 指導方針。

### <a name="forced-tunneling-configuration"></a>強制通道設定

常見的客戶設定是 toodefine 強制傳出網際網路流量 tooflow 透過 hello 在內部部署位置的預設路由 (0.0.0.0/0)。 我們不建議這麼做。 hello 複寫流量及 Site Recovery 服務通訊不應該將 hello Azure 的界限。 hello 解決方案是 tooadd 使用者定義的路由 (UDRs)[這些 IP 範圍](#outbound-connectivity-for-azure-site-recovery-ip-ranges)以便 hello 複寫流量不會傳送在內部部署。

### <a name="connectivity-between-hello-target-and-on-premises-location"></a>Hello 目標和內部部署位置之間的連線

Hello 目標位置之間 hello 在內部部署位置，請遵循這些指導方針來連線：
- 如果您的應用程式需要 tooconnect toohello 在內部部署機器，或從內部部署連線 toohello 應用程式，透過 VPN/ExpressRoute 的用戶端，確定您已至少[站對站連線](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)之間目標 Azure 地區和 hello 內部部署資料中心。

- 如果您預期您的目標 Azure 區域與 hello 在內部部署資料中心之間的流量 tooflow 很多，您應該建立另一個[ExpressRoute 連線](../expressroute/expressroute-introduction.md)hello 目標 Azure 地區和 hello 內部部署資料中心之間。

- 如果您想要 tooretain Ip hello 虛擬機器在容錯移轉之後，，保留 hello 目標區域的站台至站台/ExpressRoute 連線在中斷連線的狀態。 這是 toomake 確定 hello 來源區域的 IP 範圍和目標區域的 IP 範圍之間沒有範圍衝突。

### <a name="best-practices-for-expressroute-configuration"></a>ExpressRoute 組態的最佳做法
請遵循 ExpressRoute 組態的下列最佳做法：

- 您需要 toocreate ExpressRoute 電路這兩個 hello 來源和目標區域中。 然後您需要 toocreate 之間的連線：
  - hello 來源虛擬網路與 hello ExpressRoute 電路。
  - hello 目標虛擬網路與 hello ExpressRoute 電路。

- ExpressRoute 標準的一部分，您可以建立電路 hello 中相同的地理政治區域。 在不同的地理政治區域 toocreate ExpressRoute 電路，Azure ExpressRoute Premium 為必要項，其中牽涉到的遞增成本。 (如果您已經使用 ExpressRoute Premium，則不需要額外的成本。)如需詳細資訊，請參閱 hello [ExpressRoute 位置文件](../expressroute/expressroute-locations.md#azure-regions-to-expressroute-locations-within-a-geopolitical-region)和[ExpressRoute 定價](https://azure.microsoft.com/pricing/details/expressroute/)。

- 建議您在來源和目標區域中使用不同的 IP 範圍。 hello ExpressRoute 電路都將無法再使用兩個 Azure 虛擬網路的 hello tooconnect 相同的 IP 範圍在 hello 相同的時間。

- 您可以建立虛擬網路以 hello 相同 IP 兩個區域的範圍，然後建立兩個區域中的 ExpressRoute 電路。 在容錯移轉事件 hello 情況下，中斷 hello 電路 hello 來源的虛擬網路，然後連接 hello 目標虛擬網路中的 hello 循環。

 >[!IMPORTANT]
 > Hello hello 主要區域是否完全關閉，中斷連接作業可能會失敗。 可讓 hello 目標虛擬網路取得 ExpressRoute 連線能力。

## <a name="next-steps"></a>後續步驟
[複寫 Azure 虛擬機器](site-recovery-azure-to-azure.md)來開始保護您的工作負載。
