---
title: "aaaInfrastructure 和連線 tooSAP Azure （大型執行個體） 上的 HANA |Microsoft 文件"
description: "Azure （大型執行個體） 上設定必要的連線基礎結構 toouse SAP HANA。"
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0af34fbd82413bf63981036a76eaa264d8299ec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-infrastructure-and-connectivity-on-azure"></a>Azure 上 SAP HANA (大型執行個體) 的基礎結構和連接 

閱讀本指南之前請先了解某些預先定義。 我們在 [Azure 上 SAP HANA (大型執行個體) 的概觀和架構](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)中引進了兩種不同類別的 HANA 大型執行個體單位：

- S72、 S72m、 S144、 S144m、 S192 和 S192m 我們 tooas hello '我類別的 Type' 的 Sku。
- S384、 S384m、 S384xm、 S576、 S768 及我們的 S960 tooas hello 'Type II class' 的 Sku。

hello 類別規範會將 toobe 整個 hello toodifferent 功能與根據 HANA 大型執行個體 Sku 的需求，請參閱文件 tooeventually HANA 大型執行個體使用。

其他常用定義包括：
- **大型執行個體戳記：**硬體基礎結構堆疊是 SAP HANA TDI 認證和專用 toorun SAP HANA 的執行個體在 Azure 中。
- **在 Azure （大型執行個體） 上的 SAP HANA:** Azure toorun HANA 中的執行個體上 SAP HANA TDI 認證的硬體，部署在不同的 Azure 區域中的大型執行個體戳記中的 hello 優惠的正式名稱。 hello 相關詞彙**HANA 大型執行個體**是短的 Azure （大型執行個體） 上的 SAP HANA，廣泛使用此技術的部署指南。
 

您與 Microsoft 企業帳戶小組 hello 間完成 Azure （大型執行個體） 上的 SAP HANA hello 購買之後，hello 下列為所需的資訊 Microsoft toodeploy HANA 大型執行個體單位：

- 客戶名稱
- 業務連絡人資訊 (包括電子郵件地址和電話號碼)
- 技術連絡人資訊 (包括電子郵件地址和電話號碼)
- 技術網路連絡人資訊 (包括電子郵件地址和電話號碼)
- Azure 部署區域 (自 7 月起：美國西部、美國東部、澳洲東部、澳洲東南部、西歐和北歐) 
- 2017)
- 確認 SAP HANA on Azure (大型執行個體) SKU (組態)
- 已經針對 HANA 大型執行個體詳細 hello 概觀和架構文件中，為要部署到每個 Azure 區域：
    - / 29 Azure Vnet tooHANA 大型執行個體連接的增 P2P 連線的 IP 位址範圍
    - Hello HANA 大型執行個體伺服器的 IP 集區使用的 / 24 CIDR 區塊
- 中的每個連接 toohello HANA 大型執行個體的 Azure VNet 的 hello VNet 位址空間屬性所用的 hello IP 位址範圍值
- 每個「HANA 大型執行個體」系統的資料：
  - 所需的主機名稱 - 最好是完整的網域名稱。
  - 所需的 IP 位址超出伺服器的 IP 集區位址範圍-hello hello HANA 大型執行個體單位記住該 hello hello 位址範圍保留供內部使用 HANA 大型執行個體中伺服器的 IP 集區中的前 30 個 IP 位址
  - SAP HANA SID hello SAP HANA 執行個體 （需要的 toocreate hello 所需的 SAP HANA 相關磁碟區） 的名稱。 hello HANA SID 做是為了建立 hello 的權限<sidadm>hello NFS 磁碟區，這會取得附加的 toohello HANA 大型執行個體單位。 也會使用它做為其中一個 hello hello 取得掛接的磁碟區的名稱元件。 如果您想 toorun hello 單元上的多個 HANA 執行個體，您需要 toolist 多個 HANA Sid。 每一個都會分別指派一組磁碟區。
  - hello groupid hello hana sidadm 使用者擁有 hello Linux 作業系統中是必要的 toocreate hello 所需的 SAP HANA 相關磁碟區。 hello SAP HANA 安裝通常會建立為 1001年的群組識別碼 hello sapsys 群組。 hello hana sidadm 使用者是該群組的一部分
  - hello userid hello hana sidadm 使用者擁有 hello Linux 作業系統中是必要的 toocreate hello 所需的 SAP HANA 相關磁碟區。 如果您正在執行多個 HANA 執行個體 hello 單位上，您需要所有 hello 的 toolist <sid>adm 使用者 
- Azure 訂用帳戶識別碼 hello Azure 訂用帳戶 toowhich Azure HANA 大型執行個體上的 SAP HANA 即將 toobe 直接連接。 此訂用帳戶 ID 參考 hello Azure 訂用帳戶，即將 toobe 以 hello HANA 大型執行個體的單位收費。

之後您提供 hello 的詳細資訊，Microsoft 會佈建 Azure （大型執行個體） 上的 SAP HANA，並會傳回 hello 資訊必要 toolink 您 Azure Vnet tooHANA 大型執行個體和 tooaccess hello HANA 大型執行個體單位。

## <a name="connecting-azure-vms-toohana-large-instances"></a>連接 Azure Vm tooHANA 大型執行個體

如先前所述在[SAP HANA （大型執行個體） 的概觀和架構，在 Azure 上的](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)hello 最小部署 HANA 大型執行個體的 hello SAP 應用程式層中 Azure 看起來像：

![Azure VNet 連接 tooSAP HANA Azure （大型執行個體） 和內部部署上](./media/hana-overview-architecture/image3-on-premises-infrastructure.png)

我們更仔細 hello Azure VNet 端上，請了解 hello 需要：

- hello Azure VNet 的持續使用 toobe toodeploy hello Vm 到 hello SAP 應用程式層的定義。
- 這會自動表示預設子網路中定義 Azure Vnet 的真正 hello 一個使用的 toodeploy hello Vm 到 hello。
- hello Azure VNet 建立需要 toohave 至少一個 VM 子網路和一個 ExpressRoute 閘道子網路。 這些子網路應該被指派為指定和 hello 下列各節所述的 hello IP 位址範圍。

因此，讓我們來仔細的位元到 hello HANA 大型執行個體的 Azure VNet 建立

### <a name="creating-hello-azure-vnet-for-hana-large-instances"></a>針對 HANA 大型執行個體建立 hello Azure VNet

>[!Note]
>必須使用 hello Azure Resource Manager 部署模型可建立 hello Azure VNet HANA 大型執行個體。 hello 舊 Azure 部署的模型，通常稱為傳統部署模型不支援以 hello HANA 大型執行個體的解決方案。

hello VNet 可由使用 hello Azure 入口網站、 PowerShell、 Azure 範本或 Azure CLI (請參閱[建立虛擬網路使用 Azure 入口網站 hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))。 在下列範例的 hello，我們查看透過 hello Azure 入口網站建立 VNet。

如果我們查看的 hello Azure 入口網站透過 Azure VNet 的 hello 定義，讓我們來看一些 hello 定義與那些彼此如何關聯 toowhat 我們的不同 IP 位址範圍清單。 如我們所說的 hello**位址空間**，是指允許 toouse hello Azure VNet 的 hello 位址空間。 這個位址空間也是 hello hello VNet 使用 BGP 路由 」 傳播的位址範圍。 您可以在下列位置看到此「位址空間」：

![Hello Azure 入口網站的 Azure VNet 位址空間顯示](./media/hana-overview-connectivity/image1-azure-vnet-address-space.png)

在前面，10.16.0.0/16，與 hello 案例 hello Azure VNet 指定，而是大型和寬 IP 位址範圍 toouse。 表示所有後續的子網路，此 VNet 中的 hello IP 位址範圍不得其範圍內的位址空間。 通常針對 Azure 中的單一 VNet，我們並不建議使用這麼大的位址範圍。 但是，取得進一步的步驟，讓我們來看至 hello hello Azure VNet 中定義的子網路：

![Azure VNet 子網路及其 IP 位址範圍](./media/hana-overview-connectivity/image2b-vnet-subnets.png)

如您所見，我們看到的是含有第一個 VM 子網路 (這裡稱為 'default') 和稱為 'GatewaySubnet' 之子網路的 VNet。
我們在 hello 下列區段，請參閱 toohello IP 位址範圍的 hello 子網路，進而在 hello 圖形中做為 'default' 呼叫**Azure VM 子網路 IP 位址範圍**。 我們在下列各節的 hello，請參閱 toohello IP 位址範圍的 hello 閘道子網路為**VNet 閘道子網路 IP 位址範圍**。 

在上述的 hello 兩個圖形所示範的 hello 情況下，您會看到該 hello **VNet 位址空間**涵蓋兩者 hello **Azure VM 子網路 IP 位址範圍**和 hello **VNet 閘道子網路 IP 位址範圍**。 

在您需要 tooconserve 或與您的 IP 位址範圍是特定其他情況下，您可以限制 hello **VNet 位址空間**的每個子網路正在使用 VNet 的 toohello 特定範圍。 在此情況下，您可以定義 hello **VNet 位址空間**VNet 的多個特定的範圍如下所示：

![含有兩個空間的「Azure VNet 位址空間」](./media/hana-overview-connectivity/image3-azure-vnet-address-space_alternate.png)

在此情況下，hello **VNet 位址空間**已定義的兩個空格。 這些兩個空格，相同 toohello IP 位址範圍定義為**Azure VM 子網路 IP 位址範圍**和 hello **VNet 閘道子網路 IP 位址範圍。**

您可以將您喜歡的任何命名標準用於這些租用戶子網路 (VM 子網路)。 不過，**都必須只有一個閘道子網路的每個 VNet**連接 toohello SAP HANA 在 Azure （大型執行個體） ExpressRoute 電路。 和**這個閘道子網路必須一律為"GatewaySubnet"** tooensure 的 hello ExpressRoute 閘道的適當位置。

> [!WARNING] 
> 很重要的 hello 閘道子網路一律名為"GatewaySubnet。 」

您可以使用多個 VM 子網路，甚至是使用非連續的位址範圍。 但如先前所述，這些位址範圍必須涵蓋 hello **VNet 位址空間**hello VNet 的方法，在彙總形式或清單中的 hello 可以確切 hello VM 子網路的範圍，以及 hello 閘道子網路。

摘要 hello Azure VNet 連接 tooHANA 大型執行個體有關的重要事實：

- 您需要 toosubmit tooMicrosoft hello **VNet 位址空間**執行 HANA 大型執行個體的初始部署時。 
- hello **VNet 位址空間**可以是一個較大的範圍涵蓋 Azure VM 子網路 IP 位址範圍和 hello VNet 閘道子網路 IP 位址範圍的 hello 範圍。
- 您可以送出或者**VNet 位址空間**多個範圍，其中涵蓋 hello 不同的 IP 位址的 VM 子網路 IP 位址範圍與 hello VNet 閘道子網路 IP 位址範圍的範圍。
- 定義 hello **VNet 位址空間**是使用的 BGP 路由傳播。
- hello hello 閘道子網路名稱必須是： **"GatewaySubnet。 」**
- hello **VNet 位址空間**做 hello HANA 大型執行個體端 tooallow 篩選使用，或是不允許從 Azure 流量 toohello HANA 大型執行個體的單位。 如果 hello hello Azure VNet 的 BGP 路由資訊和 hello IP 位址範圍設定篩選 hello HANA 大型執行個體端不相符，可能會發生連線問題。
- 有一些詳細 hello 閘道子網路的討論 '連接 VNet tooHANA 大型執行個體 ExpressRoute' 區段中進一步向下



### <a name="different-ip-address-ranges-toobe-defined"></a>不同的 IP 位址範圍定義 toobe 

我們已介紹一些 hello IP 位址範圍必要 toodeploy HANA 前面章節中的大型執行個體。 但仍有一些其他重要的 IP 位址。 讓我們來瀏覽一些進一步的詳細資料。 hello 下列的 IP 位址都不是所有需要 toobe 提交 tooMicrosoft 需要 toobe 定義，再傳送要求的初始部署：

- **VNet 位址空間：**已經導入稍早，是或 hello IP 位址範圍您已指派 （或計劃 tooassign） tooyour 位址空間中的參數 hello Azure 虛擬網路 (VNet) 連接 toohello SAP HANA 大型執行個體環境。 建議這個位址空間參數是多行值組成 hello Azure VM 子網路範圍和 hello Azure 閘道子網路範圍 hello 圖形中稍早所示。 此範圍「不得」與您的內部部署或伺服器 IP 集區或 ER-P2P 位址範圍重疊。 如何 tooget 這個或這些 IP 位址範圍？ 您的公司網路小組或服務提供者應該提供一或多個網路內未使用的 IP 位址範圍。 範例： 如果您的 Azure VM 子網路 （請參閱稍早） 是 10.0.1.0/24，而 Azure 閘道子網路 （請參閱下列） 10.0.2.0/28，然後您 Azure VNet 的位址空間建議 toobe 兩行，10.0.1.0/24 和 10.0.2.0/28。 雖然 hello 位址空間的值可以彙總，建議其比對的子網路範圍 toohello tooavoid 意外重複使用的未使用的 IP 位址範圍中較大的位址空間，在未來的 hello 其他位置中您的網路。 **hello VNET 位址空間是 IP 位址範圍，要求的初始部署時，哪些需求 toobe 提交 tooMicrosoft**

- **Azure 的 VM 子網路 IP 位址範圍：**此 IP 位址範圍，已經稍早所述為的 hello 其中一個已指派 （或計劃 tooassign） Azure VNET 連接 toohello SAP HANA 大型執行個體環境中 toohello Azure VNet 子網路的參數. 此 IP 位址範圍是使用的 tooassign IP 位址 tooyour Azure Vm。 tooconnect tooyour SAP HANA 大型執行個體的伺服器允許 hello 超出此範圍的 IP 位址。 如果需要，可以使用多個 Azure VM 子網路。 Microsoft 建議為每個「Azure VM 子網路」指定 /24 CIDR 區塊。 這個位址範圍必須是 hello Azure VNet 位址空間中所使用的 hello 值的一部分。 如何 tooget 這個 IP 位址範圍？ 您的公司網路小組或服務提供者應該提供一個目前網路內未使用的 IP 位址範圍。

- **VNet 閘道子網路 IP 位址範圍：** hello 根據您計劃 toouse，hello 功能建議的大小為：
   - 強效 ExpressRoute 閘道：/26 位址區塊 - 類型 II 類別的 SKU
   - 與使用高效能 ExpressRoute 閘道 (或更小) 的 VPN 和 ExpressRoute 共存：/27 位址區塊
   - 所有其他情況：/28 位址區塊。 這個位址範圍必須是 hello [VNet 位址空間] 值中所使用的 hello 值的一部分。 這個位址範圍必須是您需要 toosubmit tooMicrosoft hello Azure VNet 位址空間的值中所使用的 hello 值的一部分。 如何 tooget 這個 IP 位址範圍？ 您的公司網路小組或服務提供者應該提供一個目前網路內未使用的 IP 位址範圍。 

- **位址範圍 ER P2P 連線：**此範圍是 SAP HANA 大型執行個體 ExpressRoute 增距 P2P 連線的 hello IP 範圍。 此 IP 位址範圍必須是 /29 CIDR IP 位址範圍。 此範圍「不得」與您的內部部署或其他 Azure IP 位址範圍重疊。 此 IP 位址範圍是使用的 tooset hello ER 連線從您 Azure VNet ExpressRoute 閘道 toohello SAP HANA 大型執行個體的伺服器上。 如何 tooget 這個 IP 位址範圍？ 您的公司網路小組或服務提供者應該提供一個目前網路內未使用的 IP 位址範圍。 **此範圍是 IP 位址範圍，要求的初始部署時，哪些需求 toobe 提交 tooMicrosoft**
  
- **伺服器的 IP 集區位址範圍：**這個 IP 位址範圍是使用的 tooassign hello 個別 IP 位址 tooHANA 大型執行個體的伺服器。 hello 建議的子網路大小是 / 24 CIDR 區塊-但如果需要它可以是提供 64 個 IP 位址的較小 tooa 最小值。 此範圍中，從 hello 前 30 個 IP 位址已保留供 microsoft。 請確定此事實會將它計時選擇 hello hello 範圍大小。 此範圍「不得」與您的內部部署或其他 Azure IP 位址重疊。 如何 tooget 這個 IP 位址範圍？ 您的公司網路小組或服務提供者應該提供一個目前網路內未使用的「IP 位址範圍」。 / 24 （建議選項） 唯一的 CIDR 區塊 toobe 用來指派 hello Azure （大型執行個體） 上的 SAP hana 所需特定 IP 位址。 **此範圍是 IP 位址範圍，要求的初始部署時，哪些需求 toobe 提交 tooMicrosoft**
 
您需要 toodefine，並計劃 hello 上述的 IP 位址範圍，但它們不是所有需要 toobe 傳輸 tooMicrosoft。 toosummarize hello 以上版本，您會需要的 tooname tooMicrosoft hello IP 位址範圍為：

- Azure VNet 位址空間
- 用於 ER-P2P 連線的位址範圍
- 伺服器 IP 集區位址範圍

新增其他 Vnet 需要 tooconnect tooHANA 大型執行個體，需要您 toosubmit hello que quiera tooMicrosoft 新的 Azure VNet 位址空間。 

下列是 hello 不同範圍和某些範例範圍的範例，以及您需要 tooconfigure 最終提供 tooMicrosoft。 如您所見，hello hello Azure VNet 位址空間的值不會在 hello 第一個範例中，彙總，但從 hello 範圍 hello 第一個 Azure VM 子網路的 IP 位址範圍和 hello VNet 閘道子網路 IP 位址範圍定義。 使用 hello Azure VNet 中的多個 VM 子網路會工作據此設定，並送出 hello 其他 IP 位址範圍的 hello 其他的 VM 子網路，做為 hello Azure VNet 位址空間的一部分。

![SAP HANA on Azure (大型執行個體) 最基本部署中所需的 IP 位址範圍](./media/hana-overview-connectivity/image4b-ip-addres-ranges-necessary.png)

您也可以彙總 hello 資料提交 tooMicrosoft hello 可能性。 在此情況下，hello hello Azure VNet 位址空間只會包含一個空格。 使用 hello hello 範例中稍早所使用的 IP 位址範圍。 此彙總的 VNet 位址空間可能看起來像這樣：

![SAP HANA on Azure (大型執行個體) 最基本部署中所需 IP 位址範圍的第二個可能性](./media/hana-overview-connectivity/image5b-ip-addres-ranges-necessary-one-value.png)

您可以看到以上版本，而不是定義 hello hello Azure VNet 位址空間的兩個較小範圍我們有一個較大的範圍涵蓋 4096 的 IP 位址。 這類大型的定義 hello 位址空間會保留未使用某些相當大的範圍。 因為 hello VNet 位址空間的值使用 BGP 路由傳播，使用方式的 hello 範圍未使用內部部署或其他地方網路中可能造成路由問題。 因此，建議的 tookeep hello 位址空間緊密配合 hello 所用的實際子網路位址空間。 如有需要而不會產生停機時間上 hello VNet，您可以稍後新增新的位址空間值。
 
> [!IMPORTANT] 
> 每個 IP 位址範圍的增-P2P，伺服器的 IP 集區，Azure VNet 位址空間必須**不**彼此重疊或使用您網路中的其他地方的任何其他範圍; 每個必須是離散和較早的顯示，可能不是以 hello 兩個圖形子網路的任何其他範圍。 如果發生重疊情況範圍之間，hello Azure VNet 可能連線 toohello ExpressRoute 電路。

### <a name="next-steps-after-address-ranges-have-been-defined"></a>定義位址範圍之後的後續步驟
Hello IP 位址範圍定義之後，hello 下列活動需要 toohappen:

1. 提交 Azure VNet 位址空間、 hello ER P2P 連接性和伺服器的 IP 集區位址範圍，hello IP 位址範圍，以及其他 hello hello 從文件開頭列出的資料。 在此時間點，您也無法啟動 toocreate hello VNet 與 hello VM 子網路。 
2. Express Route 電路會建立 Microsoft Azure 訂用帳戶之間 hello HANA 大型執行個體的戳記。
3. Microsoft 是 hello 大型執行個體戳記上建立租用戶網路。
4. Microsoft 會設定 Azure （大型執行個體） 基礎結構 tooaccept 上的 SAP HANA hello 中的網路 IP 位址，從 Azure VNet 位址空間進行通訊與 HANA 大型執行個體。
5. 根據特定的 SAP HANA Azure （大型執行個體） sku 購買的 hello，Microsoft 會指派租用戶網路的計算單位、 配置和裝載存放裝置，並安裝 hello 作業系統 （SUSE 或 Red Hat Linux）。 這些單元的 IP 位址會超出伺服器的 IP 集區位址範圍提交 tooMicrosoft hello。

在 hello hello 部署程序結尾，Microsoft 會提供下列資料 tooyou hello:
- 需要 tooconnect 您 Azure VNet(s) toohello ExpressRoute 電路連接 Azure Vnet tooHANA 大型執行個體的資訊：
     - 授權金鑰
     - ExpressRoute PeerID
- 之後您的資料 tooaccess HANA 大型執行個體建立 ExpressRoute 電路，Azure VNet。

您也可以尋找 HANA 大型執行個體連接 hello 文件中的 hello 一連串[結束 tooEnd 對 SAP HANA 大型執行個體的安裝程式](https://azure.microsoft.com/resources/sap-hana-on-azure-large-instances-setup/)。 許多 hello 步驟所示的範例部署，在該文件中。 


## <a name="connecting-a-vnet-toohana-large-instance-expressroute"></a>連線 VNet tooHANA 大型執行個體 ExpressRoute

當您定義所有 hello IP 位址範圍，並立即從 Microsoft 回收到 hello 資料，可以開始連接 hello tooHANA 大型執行個體之前所建立的 VNet。 一次建立 Azure VNet 的 hello，ExpressRoute 閘道必須在建立 hello VNet toolink hello VNet toohello 連接 toohello hello 大型執行個體戳記上的客戶租用戶的 ExpressRoute 電路。

> [!NOTE] 
> 因為 hello 指定 Azure 訂用帳戶中建立 hello 新的閘道，並已連線的 toohello 指定 Azure VNet too30 分鐘 toocomplete，可能需要此步驟。

如果閘道已經存在，請檢查它是否是 ExpressRoute 閘道。 否則，必須刪除並重新建立 ExpressRoute 閘道為 hello 閘道。 如果已經建立 ExpressRoute 閘道，因為 hello Azure VNet 已連線在內部部署連線的 toohello ExpressRoute 電路，繼續 toohello 連結的 Vnet 的下一節。

- 使用任一個 hello （新） [Azure 入口網站](https://portal.azure.com/)，或 PowerShell toocreate ExpressRoute 的 VPN 閘道連線 tooyour VNet。
  - 如果您使用 hello Azure 入口網站，加入新**虛擬網路閘道**，然後選取  **ExpressRoute** hello 閘道類型。
  - 如果您改為選擇 PowerShell，請先下載並使用最新的 hello [Azure PowerShell SDK](https://azure.microsoft.com/downloads/) tooensure 最佳的經驗。 下列命令的 hello 建立 ExpressRoute 閘道。 hello 文字前面加上 _$_ 更新您的專屬資訊的需要 toobe 是使用者定義變數。

```PowerShell
# These Values should already exist, update toomatch your environment
$myAzureRegion = "eastus"
$myGroupName = "SAP-East-Coast"
$myVNetName = "VNet01"

# These values are used toocreate hello gateway, update for how you wish hello GW components toobe named
$myGWName = "VNet01GW"
$myGWConfig = "VNet01GWConfig"
$myGWPIPName = "VNet01GWPIP"
$myGWSku = "HighPerformance" # Supported values for HANA Large Instances are: HighPerformance or UltraPerformance

# These Commands create hello Public IP and ExpressRoute Gateway
$vnet = Get-AzureRmVirtualNetwork -Name $myVNetName -ResourceGroupName $myGroupName
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
New-AzureRmPublicIpAddress -Name $myGWPIPName -ResourceGroupName $myGroupName `
-Location $myAzureRegion -AllocationMethod Dynamic
$gwpip = Get-AzureRmPublicIpAddress -Name $myGWPIPName -ResourceGroupName $myGroupName
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $myGWConfig -SubnetId $subnet.Id `
-PublicIpAddressId $gwpip.Id

New-AzureRmVirtualNetworkGateway -Name $myGWName -ResourceGroupName $myGroupName -Location $myAzureRegion `
-IpConfigurations $gwipconfig -GatewayType ExpressRoute `
-GatewaySku $myGWSku -VpnType PolicyBased -EnableBgp $true
```

在此範例中，使用 hello HighPerformance 閘道 SKU。 您的選項是高效能的分散式或 UltraPerformance hello Azure （大型執行個體） 上的 SAP hana 支援的閘道 Sku。

> [!IMPORTANT]
> 如 HANA 大型執行個體的 hello SKU 類型 S384、 S384m、 S384xm、 S576、 S768 和 S960 （輸入第二部分類別 Sku），hello hello UltraPerformance 閘道 SKU 的使用方式是強制性。

### <a name="linking-vnets"></a>連結 VNet

既然 hello Azure VNet 有 ExpressRoute 閘道，您可以使用 Microsoft tooconnect hello ExpressRoute 閘道 toohello SAP HANA Azure （大型執行個體） ExpressRoute 電路建立此連接上所提供的 hello 授權資訊。 可以使用 hello Azure 入口網站或 PowerShell 執行此步驟。 建議 hello 入口網站，但 PowerShell 的指示，如下所示。 

- 您執行下列命令，每個 VNet 閘道為每個連線使用不同的 AuthGUID hello。 hello hello 指令碼下列所示的前兩個項目來自 Microsoft 所提供的 hello 資訊。 此外，hello AuthGUID 是針對每個 VNet 和其閘道。 表示，如果您想 tooadd 另一個 Azure VNet，您需要 tooget 另一個 AuthID 為您連接至 Azure 的 HANA 大型執行個體的 ExpressRoute 電路。 

```PowerShell
# Populate with information provided by Microsoft Onboarding team
$PeerID = "/subscriptions/9cb43037-9195-4420-a798-f87681a0e380/resourceGroups/Customer-USE-Circuits/providers/Microsoft.Network/expressRouteCircuits/Customer-USE01"
$AuthGUID = "76d40466-c458-4d14-adcf-3d1b56d1cd61"

# Your ExpressRoute Gateway Information
$myGroupName = "SAP-East-Coast"
$myGWName = "VNet01GW"
$myGWLocation = "East US"

# Define hello name for your connection
$myConnectionName = "VNet01GWConnection"

# Create a new connection between hello ER Circuit and your Gateway using hello Authorization
$gw = Get-AzureRmVirtualNetworkGateway -Name $myGWName -ResourceGroupName $myGroupName
    
New-AzureRmVirtualNetworkGatewayConnection -Name $myConnectionName `
-ResourceGroupName $myGroupName -Location $myGWLocation -VirtualNetworkGateway1 $gw `
-PeerId $PeerID -ConnectionType ExpressRoute -AuthorizationKey $AuthGUID
```

如果您想 tooconnect hello 閘道 toomultiple ExpressRoute 電路的訂用帳戶相關聯，您可能需要 tooexecute 此步驟一次以上。 例如，您可能將 tooconnect hello 相同 VNet 閘道 toohello 的 ExpressRoute 電路 hello VNet tooyour 內部網路連線。

## <a name="adding-more-ip-addresses-or-subnets"></a>新增更多 IP 位址或子網路

新增多個 IP 位址或子網路時，請使用其中一個 hello Azure 入口網站、 PowerShell 或 CLI。

在此情況下，hello 建議 tooadd hello 新 IP 位址範圍為新範圍 toohello VNet 位址空間而非產生新的彙總的範圍。 在任一情況下，您需要 toosubmit 此變更 tooMicrosoft tooallow 連接超出該新 IP 位址範圍 toohello HANA 大型執行個體的單位中您的用戶端。 您可以開啟 Azure 支援人員要求 tooget hello 新 VNet 位址空間新增。 您會收到確認訊息之後，執行 hello 接下來的步驟。

toocreate hello Azure 入口網站，從其他子網路，請參閱 「 hello 文章[建立虛擬網路使用 Azure 入口網站 hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，和 toocreate 從 PowerShell，請參閱[建立虛擬網路使用 PowerShell](../../../virtual-network/virtual-networks-create-vnet-arm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="adding-vnets"></a>新增 VNet

初始連接之後一或多個 Azure Vnet，您可能想 tooadd 存取 SAP HANA Azure （大型執行個體） 上的其他項目。 首先，提交 Azure 支援要求，請在該要求中包含 hello 的特定資訊識別 hello 特定 Azure 部署和 hello hello Azure VNet 位址空間的 IP 位址空間範圍。 Azure 服務管理上的 SAP HANA 提供 hello 必要的資訊，您需要 tooconnect hello 其他 Vnet 和 ExpressRoute。 每個 VNet，您需要唯一的授權金鑰 tooconnect toohello ExpressRoute 電路 tooHANA 大型執行個體。

Tooadd 新的 Azure VNet 的步驟：

1. 完成 hello hello 上架程序中的第一個步驟，請參閱 hello_建立 Azure VNet_ > 一節。
2. 完成 hello hello 上架程序中的第二個步驟，請參閱 hello_建立閘道子網路_> 一節。
3. tooconnect 其他 Vnet toohello HANA 大型執行個體 ExpressRoute 循環中，開啟 Azure 支援要求的資訊上 hello 新的 VNet，並要求新的授權金鑰。
4. 當收到 hello 授權已完成，請使用 toocomplete hello 第三個步驟 hello 上架程序中的 hello Microsoft 提供的授權資訊，請參閱 hello_連結的 Vnet_ > 一節。

## <a name="increasing-expressroute-circuit-bandwidth"></a>增加 ExpressRoute 線路頻寬

請洽詢「SAP HANA on Azure 服務管理」。 如果您是在 Azure （大型執行個體） ExpressRoute 電路的 hello SAP HANA 的建議使用的 tooincrease hello 頻寬，建立 Azure 的支援要求。 （您可要求增加總 tooa 最多 10 gbps 以上的單一電路頻寬）。接著，您收到通知之後 hello 作業已完成。其他需要不採取任何動作 tooenable 這個較高的速度，在 Azure 中。

## <a name="adding-an-additional-expressroute-circuit"></a>新增額外的 ExpressRoute 線路

如果建議您會需要額外的 ExpressRoute 電路，讓 Azure 支援人員要求 toocreate 新 ExpressRoute 循環 （tooget 授權資訊 tooconnect tooit），請洽詢 SAP HANA Azure 服務管理。 SAP hana 對 Azure 服務管理 tooprovide 授權的順序進行 hello 要求之前，必須定義 Vnet 的 hello 用於即將 hello 位址空間。

一旦建立 hello 新電路和 Azure 服務管理組態上的 SAP HANA hello 已完成，您將需要 tooproceed hello 資訊 tooreceive 通知。 請遵循上面提供建立及連接 hello 新 VNet toothis 其他循環的 hello 步驟。 您不能 tooconnect Azure Vnet toothis 其他電路如果他們已經連接在 hello Azure （大型執行個體） ExpressRoute 電路上的 SAP HANA tooanother 相同 Azure 區域。

## <a name="deleting-a-subnet"></a>刪除子網路

可以使用 tooremove VNet 子網路，可能是 hello Azure 入口網站、 PowerShell 或 CLI。 如果您的 Azure VNet IP 位址範圍/Azure VNet 位址空間是一個彙總的範圍，後續就沒有需要追蹤 Microsoft 的事項。 除了該 hello VNet 仍將傳播時包含 hello 刪除子網路的 BGP 路由位址空間。 如果您為多個 IP 位址範圍定義 hello Azure VNet 的 IP 位址範圍/Azure VNet 位址空間的哪一個已指派的 tooyour 刪除子網路，您應該刪除，您的 VNet 位址空間不足，並接著通知 Azure 服務管理上的 SAP HANA從 hello 範圍 Azure （大型執行個體） 上的 SAP HANA tooremove 允許與 toocommunicate。

雖然沒有特定的專用 Azure.com 指引移除子網路，來移除子網路的 hello 程序是 hello 會反轉 hello 程序將它們加入。 請參閱 hello 文章[建立虛擬網路使用 Azure 入口網站 hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)如需有關建立子網路。

## <a name="deleting-a-vnet"></a>刪除 VNet

刪除 VNet 時，請使用其中一個 hello Azure 入口網站、 PowerShell 或 CLI。 Azure 服務管理上的 SAP HANA 移除 hello Azure （大型執行個體） ExpressRoute 電路上的 SAP HANA hello 上現有的授權，並移除 hello Azure VNet 的 IP 位址範圍/Azure VNet 位址空間的 hello 通訊 HANA 大型執行個體。

一旦移除 hello VNet，請開啟 Azure 支援人員要求 tooprovide hello IP 位址空間範圍 toobe 移除。

雖然沒有特定的專用 Azure.com 指引移除 Vnet，來移除 Vnet hello 程序是 hello 會反轉 hello 加入它們，這上面所述的程序。 請參閱 hello 文章[建立虛擬網路使用 Azure 入口網站 hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)和[建立虛擬網路使用 PowerShell](../../../virtual-network/virtual-networks-create-vnet-arm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)如需建立 Vnet 的詳細資訊。

tooensure 移除所有項目時，會刪除下列項目 hello:

- hello ExpressRoute 連線，VNet 閘道 VNet 閘道的公用 IP 與 VNet

## <a name="deleting-an-expressroute-circuit"></a>刪除 ExpressRoute 線路

tooremove 額外的 SAP HANA Azure （大型執行個體） ExpressRoute 電路上使用 Azure 服務管理上的 SAP HANA 開啟 Azure 支援要求，並要求應該刪除的 hello 循環。 內 hello Azure 訂用帳戶，您可能會刪除，或保留 hello 視 VNet。 不過，您必須刪除 hello hello HANA 大型執行個體 ExpressRoute 循環之間的連線，而且 hello 連結 VNet 閘道。

如果您也想 tooremove VNet，請遵循 hello 指引，以刪除上述 hello 一節中的 VNet。


