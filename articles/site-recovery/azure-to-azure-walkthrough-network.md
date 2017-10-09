---
title: "網路功能與 Site Recovery 的 VMware tooAzure 複寫 aaaPlan |Microsoft 文件"
description: "本文討論使用 Azure Site Recovery 將 Azure VM 複寫至 Azure 時所需的網路規劃"
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
ms.date: 08/01/2017
ms.author: sujayt
ms.openlocfilehash: e4036351ca707bd4966cf2a855d4a162f88153e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-networking-for-azure-vm-replication"></a>步驟 3：規劃 Azure VM 複寫的網路服務

我們已經確認 hello 之後[部署必要條件](azure-to-azure-walkthrough-prerequisites.md)，閱讀此文章 toounderstand hello 網路複寫，以及從一個 Azure 區域 tooanother 復原 Azure 虛擬機器 (Vm) 時的考量使用 helloAzure Site Recovery 服務。 

- 當您完成 hello 發行項時，您應該有明確的了解如何向上輸出 tooset 存取的 Azure Vm 您想 tooreplicate，及如何從您內部 tooconnect 網站 toothose Vm。
- 張貼於 hello 下方的本文中，任何註解或詢問問題中 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

>[!NOTE]
> Site Recovery 的 Azure VM 複寫目前為預覽狀態。



## <a name="network-overview"></a>網路概觀

通常您的 Azure Vm 位於 Azure 虛擬網路/子網路，而且沒有從您在內部部署站台 tooAzure 使用 Azure ExpressRoute 或 VPN 連線的連接。

通常會使用防火牆和/或網路安全性群組 (NSG) 來保護網路。 防火牆可以使用 URL 為基礎以 IP 為主的 list，toocontrol 網路連線。 NSG 會使用以 IP 範圍為基礎的規則。 


站台復原 toowork 預期，您需要 toomake 傳出的網路連線，從您想 tooreplicate Vm 中的某些變更。 Site Recovery 並不支援使用驗證 proxy toocontrol 網路連線。 如果您有驗證 Proxy，就無法啟用複寫。 


hello 下列圖表描述一般的 Azure Vm 上執行的應用程式環境。

![客戶環境](./media/azure-to-azure-walkthrough-network/source-environment.png)

**Azure VM 環境**

您可能也必須設定您的內部部署網站，從連接 tooAzure 使用 Azure ExpressRoute 或 VPN 連線。 

![客戶環境](./media/azure-to-azure-walkthrough-network/source-environment-expressroute.png)

**在內部部署連線 tooAzure**



## <a name="outbound-connectivity-for-urls"></a>URL 的輸出連線能力

如果您使用的 URL 為基礎的防火牆 proxy toocontrol 輸出連線，請確定您允許這些 Site Recovery 所使用的 Url

**URL** | **詳細資料**  
--- | ---
*.blob.core.windows.net | 可讓資料 toobe 寫入 hello VM，hello 來源範圍中的 toohello 快取儲存體帳戶。
login.microsoftonline.com | 提供授權和驗證 tooSite Recovery 服務 Url。
*.hypervrecoverymanager.windowsazure.com | 允許以 hello hello VM 從 Site Recovery 服務通訊。
*.servicebus.windows.net | 需要如此 hello 站台復原監視和診斷資料可以寫入從 hello VM。

## <a name="outbound-connectivity-for-ip-address-ranges"></a>IP 位址範圍的輸出連線能力

- 您可以自動建立所需的 hello 規則 hello NSG 上下載並執行[此指令碼](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702)。
- 我們建議您在測試 NSG，建立所需的 hello NSG 規則，並確認沒有任何問題，您建立 hello 規則實際執行 NSG 之前。
- toocreate hello 必要數目 NSG 規則，確保您的訂閱是在允許清單中。 請連絡客戶支援 tooincrease hello NSG 規則限制在您的訂用帳戶。
如果您使用任何 IP 型防火牆 proxy 或 NSG 規則 toocontrol 輸出連線，hello 下列 IP 範圍需要 toobe 白名單，根據 hello hello 虛擬機器的來源和目標位置：

    - 所有 IP 位址範圍對應 toohello 來源位置。 下載 hello[範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)。)允許清單是必要項目，因此可以將資料寫入 toohello 快取儲存體帳戶從 hello VM。
    - 所有的 IP 範圍對應 tooOffice 365[驗證和身分識別的 IP V4 端點](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity)。 如果新的 Ip 加入 tooOffice 365 IP 範圍，您需要 toocreate 新 NSG 規則。
-     Site Recovery 服務端點 IP 位址 ([XML 檔案中提供](https://aka.ms/site-recovery-public-ips))，取決於您的目標位置： 

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

## <a name="example-nsg-configuration"></a>範例 NSG 設定

本節說明 tooconfigure NSG 規則的方式，以便複寫適用於 VM。 如果您要使用 NSG 規則 toocontrol 輸出連線，使用 「 允許 HTTPS 輸出 」 規則的所有必要的 hello IP 範圍。

在此範例中，hello VM 來源位置會是 「 美國東部"。 美國中部的 hello 複寫目標位置。


### <a name="example"></a>範例

#### <a name="east-us"></a>美國東部

1. 建立規則，以對應太[East US IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)。 這是必要的以便資料可以從 hello VM 寫入 toohello 快取儲存體帳戶。
2. 建立規則的所有 IP 範圍對應 tooOffice 365[驗證和身分識別的 IP V4 端點](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity)。
3. 建立對應 toohello 目標位置的規則：

   **位置** | **Site Recovery 服務 IP** |  **Site Recovery 監視 IP**
    --- | --- | ---
   美國中部 | 40.69.144.231</br>40.69.167.116 | 52.165.34.144

#### <a name="central-us"></a>美國中部

使複寫可以從 hello 目標區域 toohello 來源區域，啟用容錯移轉之後，這些規則是必要的。

1. 建立規則，以對應太[中央美國 IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)。
2. 建立規則的所有 IP 範圍對應 tooOffice 365[驗證和身分識別的 IP V4 端點](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity)。
3. 建立對應 toohello 來源位置的規則：

   **位置** | **Site Recovery 服務 IP** |  **Site Recovery 監視 IP**
    --- | --- | ---
   美國東部 | 13.82.88.226</br>40.71.38.173 | 104.45.147.24


## <a name="existing-on-premises-connection"></a>現有的內部部署連線

如果您有內部部署網站與 Azure 中的 hello 來源位置之間 ExpressRoute 或 VPN 連線，請遵循這些指導方針：

**組態** | **詳細資料**
--- | ---
**強制通道** | 通常預設路由 (0.0.0.0/0) 會強制傳出網際網路流量 tooflow 透過 hello 在內部部署位置。 不建議這樣做。 複寫流量及 Site Recovery 通訊應該留在 Azure 中。<br/><br/> 做為方案中，將使用者定義的路由 (UDRs) 新增為[這些 IP 範圍](#outbound-connectivity-for-azure-site-recovery-ip-ranges)，如此 hello 流量不會傳送在內部部署。
**連線能力** | 如果應用程式需要 tooconnect tooon 內部部署機器，或在內部部署用戶端透過 VPN/ExpressRoute 透過內部部署連接 toohello 應用程式，請確定您已至少[站對站連線](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)之間 hello 目標 Azure 地區和hello 在內部部署站台。<br/><br/> 如果高 hello 目標 Azure 地區和 hello 在內部部署站台間流量磁碟區，請建立另一個[ExpressRoute 連線](../expressroute/expressroute-introduction.md)、 hello 目標區域與內部部署之間。<br/><br/> 如果您想要 tooretain Ip Vm 容錯移轉之後，保留 hello 目標區域的站台至站台/ExpressRoute 連線在中斷連線的狀態。 這可確保有 hello 來源和目標 IP 位址範圍之間沒有範圍衝突。
**ExpressRoute** | 在 hello 中來源與目標地區建立 ExpressRoute 電路。<br/><br/> 建立 hello 來源網路] 和 [hello ExpressRoute 循環，以及 hello 目標網路與 hello 循環之間的連接。<br/><br/> 建議您在來源和目標區域中使用不同的 IP 範圍。 hello 循環不會無法 tooconnect toomore 比一個 Azure 網路 hello 相同 IP 範圍，在 hello 相同的時間。<br/><br/> 您可以建立虛擬網路以 hello 相同的 IP 範圍在這兩個區域中，與在兩個區域中建立 ExpressRoute 電路。 容錯移轉，則中斷 hello 電路 hello 來源的虛擬網路，然後連接 hello 目標虛擬網路中的 hello 循環。<br/><br/> Hello hello 主要區域是否完全關閉，中斷連接作業可能會失敗。 在此情況下，hello 目標虛擬網路不會取得 ExpressRoute 連線能力。
**ExpressRoute Premium** | 您可以在 hello 建立電路相同地理政治區域。<br/><br/> 在不同的地理政治區域 toocreate 電路，您需要 Azure ExpressRoute Premium。<br/><br/> Premium hello 成本是累加的。 如果您已經在使用它，就不需要額外成本。<br/><br/> 深入了解[位置](../expressroute/expressroute-locations.md#azure-regions-to-expressroute-locations-within-a-geopolitical-region)和[定價](https://azure.microsoft.com/pricing/details/expressroute/)。



## <a name="next-steps"></a>後續步驟

跳過[步驟 4： 建立保存庫](azure-to-azure-walkthrough-vault.md)

