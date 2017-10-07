---
title: "aaaOverview 與 SAP HANA 的架構在 Azure （大型執行個體） 上 |Microsoft 文件"
description: "架構概觀 tooDeploy Azure （大型執行個體） 上的 SAP HANA。"
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
ms.openlocfilehash: e3ee6864af37ac322635eaef43e3c20101e3a769
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-overview-and-architecture-on-azure"></a>Azure 上的 SAP HANA (大型執行個體) 概觀和架構

## <a name="what-is-sap-hana-on-azure-large-instances"></a>什麼是 SAP HANA on Azure (大型執行個體)？

在 Azure （大型執行個體） 上的 SAP HANA 是獨特的解決方案 tooAzure。 此外 tooproviding 部署和執行 SAP HANA，Azure 的 hello 用途的 Azure 虛擬機器提供 hello 可能性 toorun，屬於客戶的專用的 tooyou 祼機伺服器上部署 SAP HANA。 指派 tooyou 客戶的非共用主機/伺服器裸機硬體上，建置 hello SAP HANA Azure （大型執行個體） 解決方案。 hello 伺服器硬體會內嵌在較大的戳記包含計算/伺服器、 網路和儲存體基礎結構。 而這樣的組合已通過 HANA TDI 認證。 hello Azure （大型執行個體） 上的 SAP HANA 的服務供應項目會提供各種不同的伺服器 Sku 或開始在 72 個 Cpu 的單位，768 GB 記憶體 toounits 具有 960 個 Cpu 和 20 TB 的記憶體大小。

在租用戶的詳細資料中看起來像執行 hello 基礎結構戳記 hello 客戶隔離：

- 網路功能：透過每個客戶指派的租用戶所獲得的虛擬網路，在基礎結構堆疊內區隔客戶。 租用戶指派 tooa 單一客戶。 但一個客戶可以擁有多個租用戶。 hello 網路隔離的租用戶禁止 hello 基礎結構戳記層級中的租用戶之間的網路通訊。 即使租用戶隸屬 toohello 同一位客戶。
- 儲存元件： 透過程儲存虛擬機器存放磁碟區指派 tooit。 Tooone 存放虛擬機器只可以指派儲存體磁碟區。 儲存體的虛擬機器會指派以獨佔方式 tooone 單一租用戶 hello SAP HANA TDI 通過認證的基礎結構堆疊中。 如此一來一個特定及相關的租用戶只可以存取指派 tooa 存放虛擬機器的存放磁碟區。 是不可見 hello 不同部署租用戶之間。
- 伺服器或主機：伺服器或主機單位無法讓不同客戶或不同租用戶共用。 在伺服器或主機部署 tooa 客戶，會指派 tooone 單一租用戶的不可部分完成的裸機計算單位。 您**無法**使用任何硬體分割或軟體分割方式來讓身為客戶的您與其他客戶共用主機或伺服器。 指派的 hello 特定租用戶 toohello 存放虛擬機器的存放磁碟區會掛接的 toosuch 伺服器。 租用戶可以有一個 toomany 伺服器單位以獨佔方式指派的不同 Sku。
- 在 Azure （大型執行個體） 基礎結構的戳記上的 SAP HANA，許多不同的租用戶部署，而且透過網路、 儲存體和計算層級上的 hello 租用戶概念互相隔離上。 


這些裸機伺服器單位是支援的 toorun 向只 SAP HANA。 hello SAP 應用程式層或工作負載中介軟體層是 Microsoft Azure 虛擬機器中執行。 在 Azure （大型執行個體） 上執行 hello SAP HANA 的 hello 基礎結構戳記單位是連接的 toohello Azure 網路 backbone，因此，在 Azure （大型執行個體） 單位上的 SAP HANA 與 Azure 虛擬機器之間的低延遲連線所提供。

本文件是其中一個涵蓋 Azure （大型執行個體） 上的 SAP HANA hello 主題的五個文件。 在本文件中，我們透過 hello 基本架構、 責任、 提供，服務和高階，透過 hello 解決方案的功能。 對於大多數的 hello 區域，例如網路和連接，hello 其他四個文件涵蓋詳細資料和向下切入清單。 Azure （大型執行個體） 上的 SAP HANA 的 hello 文件未涵蓋的 SAP NetWeaver 安裝層面或部署在 Azure Vm 中的 SAP NetWeaver。 此主題涵蓋在個別的文件中找到 hello 相同文件容器。 


hello 五個部分，本指南涵蓋下列主題中的 hello:

- [Azure 上 SAP HANA (大型執行個體) 的概觀和架構](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Azure 上 SAP HANA (大型執行個體) 的基礎結構和連接](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [如何 tooinstall 及設定 Azure 上 SAP HANA （大型執行個體）](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Azure 上 SAP Hana (大型執行個體) 的高可用性和災害復原](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Azure 上 SAP HANA (大型執行個體) 疑難排解和監視](troubleshooting-monitoring.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="definitions"></a>定義

數個常見的定義都廣泛利用 hello 架構和技術的部署指南中。 請注意 hello 下列詞彙和其意義：

- **IaaS：**基礎結構即服務
- **PaaS：**平台即服務
- **SaaS：**軟體即服務
- **SAP 元件︰**個別的 SAP 應用程式，例如 ECC、BW、Solution Manager 或 EP。 SAP 元件可以傳統 ABAP 或 Java 技術為基礎，或以非 NetWeaver 應用程式 (例如商務物件) 為基礎。
- **SAP 環境：**一或多個 SAP 元件以邏輯方式分組 tooperform 商務功能，例如開發、 QAS、 訓練、 DR 或生產環境。
- **SAP 版圖：**是指您的 IT 環境中 toohello 整個 SAP 資產。 hello SAP 版圖包括所有生產和非生產環境。
- **SAP 系統：** hello DBMS 層和應用程式層的 SAP ERP 開發系統、 SAP BW 測試系統、 SAP CRM 生產系統等的組合。Azure 部署不支援在內部部署與 Azure 之間分割這兩個層。 表示 SAP 系統可以在內部部署或在 Azure 部署。 不過，您可以部署至 Azure 或內部部署 SAP 版圖的 hello 不同系統。 例如，您可以部署 hello SAP CRM 開發和測試系統在 Azure 中，同時 hello SAP CRM 生產系統在內部部署。 Azure （大型執行個體） 上的 SAP hana，它是裝載在 Azure Vm 中的 SAP 系統的 hello SAP 應用程式層，hello 相關的單位 hello HANA 大型執行個體戳記上的 SAP HANA 執行個體。
- **大型執行個體戳記：**硬體基礎結構堆疊是 SAP HANA TDI 認證和專用 toorun SAP HANA 的執行個體在 Azure 中。
- **在 Azure （大型執行個體） 上的 SAP HANA:** Azure toorun HANA 中的執行個體上 SAP HANA TDI 認證的硬體，部署在不同的 Azure 區域中的大型執行個體戳記中的 hello 優惠的正式名稱。 hello 相關詞彙**HANA 大型執行個體**是短的 Azure （大型執行個體） 上的 SAP HANA，廣泛使用此技術的部署指南。
- **跨單位：**說明的案例，其中 Vm 是已部署的 tooan Azure 訂用帳戶具有站台對站台、 多站台或 ExpressRoute hello 在內部部署資料中心與 Azure 之間的連線能力。 在一般 Azure 文件中，這類部署也會描述為跨單位案例。 hello hello 連線的原因是 tooextend 在內部部署網域、 在內部部署 Active Directory/OpenLDAP 和內部部署 DNS 至 Azure。 hello 內部橫向是擴充的 toohello hello Azure 訂閱的 Azure 資產。 透過這樣延伸，hello Vm 可以是 hello 在內部部署網域的一部分。 Hello 在內部部署網域的網域使用者可以存取 hello 伺服器，並且可以執行服務那些 Vm （例如 DBMS 服務）。 但無法在內部部署的 VM 和 Azure 部署的 VM 之間進行通訊和名稱解析。 這類是 hello 中的大部分 SAP 資產部署的典型案例。 請參閱的 hello 指南[規劃和設計 VPN 閘道](../../../vpn-gateway/vpn-gateway-plan-design.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)和[使用 hello Azure 入口網站的站對站連接建立 VNet](../../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)如需詳細資訊。
- **租用戶：**部署於 HANA 大型執行個體戳記的客戶回隔離到「租用戶」中。 租用戶會隔離在 hello 網路、 儲存和計算層來自其他租用戶。 因此，該儲存體和計算的單位 toohello 指派不同的租用戶無法看到彼此，或在 hello 與對方進行通訊 HANA 大型執行個體戳記層級。 客戶可以選擇 toohave 部署到不同的租用戶。 即使如此，是沒有 hello HANA 大型執行個體戳記層級上的租用戶之間的通訊。

有各種不同的已發佈的部署 Microsoft Azure 公用雲端上的 SAP 工作負載的 hello 主題的其他資源。 強烈建議規劃與執行的 SAP HANA 部署在 Azure 中的任何人是有經驗和了解 Azure IaaS hello 主體與 hello 部署在 Azure IaaS 上 SAP 工作負載。 hello 下列資源提供詳細的資訊並繼續前所應參考：


- [在 Microsoft Azure 虛擬機器上使用 SAP 解決方案](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="certification"></a>認證

除了 hello NetWeaver 憑證，SAP 特定基礎結構，例如 Azure IaaS 上 SAP HANA toosupport SAP HANA 需要特殊的憑證。

hello 核心 NetWeaver 和 tooa 程度 SAP HANA 憑證上的 SAP 附註是[SAP 附註 #1928533 – Azure 上的 SAP 應用程式： 支援產品與 Azure VM 類型](https://launchpad.support.sap.com/#/notes/1928533)。

這個 [SAP 附註 #2316233 - SAP HANA on Microsoft Azure (大型執行個體)](https://launchpad.support.sap.com/#/notes/2316233/E) 也很重要。 它涵蓋在本指南中所述的 hello 解決方案。 此外，您也支援的 toorun hello GS5 VM 類型的 Azure 中 SAP HANA。 [此案例的資訊在 hello SAP 網站上發行](http://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html)。

hello Azure （大型執行個體） 方案上的 SAP HANA tooin SAP 附註 #2316233 會提供 Microsoft 和參考 SAP 客戶 hello 能力 toodeploy 大型 SAP Business Suite、 SAP Business 倉儲 (BW)、 S/4 HANA、 BW/4HANA 或在 Azure 中的其他 SAP HANA 工作負載。 hello 方案以 hello SAP HANA 認證專用的硬體戳記為基礎 ([SAP HANA 量身訂做的資料中心整合 – TDI](https://scn.sap.com/docs/DOC-63140))。 SAP HANA TDI 以執行設定的解決方案為您提供的了解所有 SAP HANA 的應用程式 （包括在 SAP HANA SAP Business Suite、 SAP Business 倉儲 (BW) 上 SAP HANA、 S4/HANA 和 BW4/HANA） hello 上，都將 toowork hello 信心硬體基礎結構。

比較的 toorunning SAP HANA Azure 虛擬機器中此解決方案有一項優點，它會提供更大的記憶體磁碟區。 如果您要 tooenable 此方案，有一些重要層面 toounderstand:

- hello SAP 應用程式層和非 SAP 應用程式執行在 Azure 虛擬機器 (Vm) 所裝載的 hello 一般 Azure 硬體戳記。
- 客戶內部部署基礎結構，資料中心和應用程式部署為連線的 toohello Microsoft Azure 雲端平台透過 Azure ExpressRoute （建議選項） 或虛擬私人網路 (VPN)。 Active Directory (AD) 和 DNS 也會延伸到 Azure。
- 在 Azure （大型執行個體） 上的 SAP HANA 執行 HANA 工作負載的 hello SAP HANA 資料庫執行個體。 hello 大型執行個體戳記連接至 Azure 網路，讓 Azure Vm 中執行的軟體可以互動 HANA 大型執行個體中執行的 hello HANA 執行個體。
- SAP HANA on Azure (大型執行個體) 的硬體是已預先安裝 SUSE Linux Enterprise Server 或 Red Hat Enterprise Linux 的「基礎結構即服務」(IaaS) 中所提供的專用硬體。 使用 Azure 虛擬機器中，取得進一步的更新和維護 toohello 作業系統是您的責任。
- HANA 或單位 HANA 大型執行個體上的任何其他元件所需 toorun SAP HANA 安裝您要負責，是所有各自持續進行的作業，以進行管理的 Azure 上 SAP HANA。
- 除了此處所述的 toohello 解決方案，您可以安裝其他元件連接 tooSAP HANA Azure （大型執行個體） 上您 Azure 訂用帳戶中。  例如，啟用與通訊及/或直接 toohello SAP HANA 資料庫中的元件 （跳躍伺服器、 RDP 伺服器 SAP HANA Studio 中，SAP BI 的情況下，SAP 資料服務或網路監視解決方案）。
- 與在 Azure 中一樣，HANA 大型執行個體也會提供支援高可用性和災害復原功能。

## <a name="architecture"></a>架構

高階 hello Azure （大型執行個體） 方案上的 SAP HANA 具有 hello SAP 應用程式層位於 Azure Vm 和 hello SAP TDI 設定硬體，位在大型執行個體中的戳記上的資料庫層級 hello 連接的相同 Azure 區域tooAzure IaaS。

> [!NOTE]
> 您需要在 hello toodeploy hello SAP 應用程式層與 hello SAP DBMS 層相同 Azure 區域。 此規則在已發佈的 Azure 上 SAP 工作負載的相關資訊中有詳細記載。 

hello Azure （大型執行個體） 上的 SAP HANA 的整體架構提供 SAP TDI 通過認證的硬體組態 （非虛擬化、 bare metal、 高效能伺服器 hello SAP HANA 資料庫） 和 hello 和功能的 Azure tooscale 彈性資源 hello SAP 應用程式層 toomeet 您的需求。

![SAP HANA on Azure (大型執行個體) 的架構概觀](./media/hana-overview-architecture/image1-architecture.png)

顯示 hello 架構分為三個區段：

- **右邊：**一個執行資料中心內不同應用程式的內部部署基礎結構，其中使用者會存取 LOB 應用程式 (例如 SAP)。 在理想情況下，這在內部部署基礎結構就會連接與 Azure tooAzure [ExpressRoute](https://azure.microsoft.com/services/expressroute/)。

- **Center:**顯示 Azure IaaS 而且，在此情況下，使用 Azure Vm toohost SAP 的 DBMS 系統為使用 SAP HANA 其他應用程式。 在 Azure Vm 中部署與 hello 記憶體 Azure Vm 的函式提供較小 HANA 執行個體以及其應用程式層。 深入了解[虛擬機器](https://azure.microsoft.com/services/virtual-machines/)。
<br />Azure 網路是使用的 toogroup SAP 系統，以及其他應用程式到 Azure 虛擬網路 (Vnet)。 這些 Vnet 連接 tooon 內部部署系統以及 tooSAP HANA Azure （大型執行個體） 上。
<br />SAP NetWeaver 應用程式和資料庫的 Microsoft Azure 支援 toorun，請參閱[SAP 支援附註 #1928533 – Azure 上的 SAP 應用程式： 支援產品與 Azure VM 類型](https://launchpad.support.sap.com/#/notes/1928533)。 如需在 Azure 上部署 SAP 解決方案的相關文件，請檢閱：

  -  [在 Windows 虛擬機器 (VM) 上使用 SAP](../../virtual-machines-windows-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
  -  [在 Microsoft Azure 虛擬機器上使用 SAP 解決方案](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

- **左：**顯示 hello SAP HANA TDI 認證 hello Azure 大型執行個體戳記中的硬體。 hello HANA 大型執行個體單位是連接的 toohello Azure Vnet 的訂用帳戶使用相同的技術為 hello 連線從內部部署至 Azure 的 hello。

hello Azure 大型執行個體戳記本身結合了下列元件的 hello:

- **運算：**為基礎，提供 hello 必要的運算能力，而且認證的 SAP HANA 的 Intel Xeon E7 8890v3 或 Intel Xeon E7 8890v4 處理器的伺服器。
- **網路：** A 統一的高速網路網狀架構連接 hello 運算、 儲存和區域網路元件。
- **儲存體：**可透過整合式網路網狀架構存取的儲存體基礎結構。 特定儲存容量是提供根據 hello 正在部署 Azure （大型執行個體） 」 設定特定的 SAP HANA （更多儲存容量是可在其他每月成本）。

中的 hello 大型執行個體戳記 hello 多租用戶基礎結構，客戶會部署為隔離的租用戶。 在 hello 租用戶部署，您需要在您的 Azure 註冊內 tooname Azure 訂用帳戶。 此持續 toobe hello Azure 訂用帳戶，hello HANA 大型執行個體正在 toobe 針對計費。 這些租用戶有 1:1 關聯性 toohello Azure 訂用帳戶。 網路明智很可能 tooaccess HANA 大型執行個體單位在不同的 Azure Vnet，屬於 toodifferent 從一個 Azure 區域中的一個租用戶部署 Azure 訂用帳戶。 但這些 Azure 訂用帳戶需要 toobelong toohello 相同 Azure 註冊。 

與 Azure VM 一樣，在多個 Azure 區域中都有提供 SAP HANA on Azure (大型執行個體)。 在順序 toooffer 災害復原功能，您可以選擇在 tooopt。 一個地理政治區域內的不同大型執行個體戳記是連接的 tooeach 其他。 例如，透過的 DR 複寫 hello 用途的專用的網路連結連接 HANA 大型執行個體中的戳記美國西部和美國東部。 

就像使用「Azure 虛擬機器」時您可以在不同的 VM 類型之間做選擇一樣，您也可以從針對不同 SAP HANA 工作負載類型量身打造的不同「HANA 大型執行個體」SKU 中做選擇。 SAP 適用於層代的 Intel 處理器 hello 基礎的各種工作負載的記憶體 tooprocessor 通訊端比例 — 有四個不同的 SKU 類型提供：

自七月 2017 Azure （大型執行個體） 上的 SAP HANA 有數種設定 hello Azure 區域的美國西部和美國東部、 澳洲東部、 澳洲東南部、 西歐、 和北歐：

| SAP 解決方案 | CPU | 記憶體 | 儲存體 | Availability |
| --- | --- | --- | --- | --- |
| 已針對 OLAP 最佳化：SAP BW、BW/4HANA<br /> 或 SAP HANA (一般 OLAP 工作負載) | SAP HANA on Azure S72<br /> – 2 x Intel® Xeon® Processor E7-8890 v3<br /> 36 個 CPU 核心和 72 個 CPU 執行緒 |  768 GB |  3 TB | 可用 |
| --- | SAP HANA on Azure S144<br /> – 4 x Intel® Xeon® Processor E7-8890 v3<br /> 72 個 CPU 核心和 144 個 CPU 執行緒 |  1.5 TB |  6 TB | 不再提供 |
| --- | SAP HANA on Azure S192<br /> – 4 x Intel® Xeon® Processor E7-8890 v4<br /> 96 個 CPU 核心和 192 個 CPU 執行緒 |  2.0 TB |  8 TB | 可用 |
| --- | SAP HANA on Azure S384<br /> – 8 x Intel® Xeon® Processor E7-8890 v4<br /> 192 個 CPU 核心和 384 個 CPU 執行緒 |  4.0 TB |  16 TB | 準備好 tooOrder |
| 已針對 OLTP 最佳化：SAP Business Suite<br /> on SAP HANA 或 S/4HANA (OLTP)<br /> (一般 OLTP) | SAP HANA on Azure S72m<br /> – 2 x Intel® Xeon® Processor E7-8890 v3<br /> 36 個 CPU 核心和 72 個 CPU 執行緒 |  1.5 TB |  6 TB | 可用 |
|---| SAP HANA on Azure S144m<br /> – 4 x Intel® Xeon® Processor E7-8890 v3<br /> 72 個 CPU 核心和 144 個 CPU 執行緒 |  3.0 TB |  12 TB | 不再提供 |
|---| SAP HANA on Azure S192m<br /> – 4 x Intel® Xeon® Processor E7-8890 v4<br /> 96 個 CPU 核心和 192 個 CPU 執行緒  |  4.0 TB |  16 TB | 可用 |
|---| SAP HANA on Azure S384m<br /> – 8 x Intel® Xeon® Processor E7-8890 v4<br /> 192 個 CPU 核心和 384 個 CPU 執行緒 |  6.0 TB |  18 TB | 準備好 tooOrder |
|---| SAP HANA on Azure S384xm<br /> – 8 x Intel® Xeon® Processor E7-8890 v4<br /> 192 個 CPU 核心和 384 個 CPU 執行緒 |  8.0 TB |  22 TB |  準備好 tooOrder |
|---| SAP HANA on Azure S576<br /> – 12 x Intel® Xeon® Processor E7-8890 v4<br /> 288 個 CPU 核心和 576 個 CPU 執行緒 |  12.0 TB |  28 TB | 準備好 tooOrder |
|---| SAP HANA on Azure S768<br /> – 16 x Intel® Xeon® Processor E7-8890 v4<br /> 384 個 CPU 核心和 768 個 CPU 執行緒 |  16.0 TB |  36 TB | 準備好 tooOrder |
|---| SAP HANA on Azure S960<br /> – 20 x Intel® Xeon® Processor E7-8890 v4<br /> 480 個 CPU 核心和 960 個 CPU 執行緒 |  20.0 TB |  46 TB | 準備好 tooOrder |

- CPU 核心 = 非-超執行緒 hello 總和 hello 伺服器單元 hello 處理器的 CPU 核心數的總和。
- CPU 執行緒 = 計算執行緒超執行緒 hello 總和 hello 伺服器單元 hello 處理器的 CPU 核心數所提供的總和。 所有單元可以都設定預設 toouse 超執行緒。


hello 不同組態上述可用或 '，不會提供不再' 中參考[SAP 支援附註 #2316233 – Microsoft Azure （大型執行個體） 上的 SAP HANA](https://launchpad.support.sap.com/#/notes/2316233/E)。 hello 設定，這會標示為 '準備 tooOrder' 很快就會發現其項目插入 hello SAP 附註。 這些執行個體的 Sku 可以排序已 hello 六個不同 Azure 區域 hello HANA 大型執行個體服務為可用。

hello 選擇特定的組態均依存於工作負載、 CPU 資源，以及所需的記憶體。 您可針對 OLTP 工作負載 tooleverage hello Sku，OLAP 工作負載最佳化。 

所有 hello 供應項目的基底的 hello 硬體是 SAP HANA TDI 認證。 不過，我們來區分兩個不同的類別，用來分割成 hello Sku 的硬體：

- S72、 S72m、 S144、 S144m、 S192 和 S192m 我們 tooas hello '我類別的 Type' 的 Sku。
- S384、 S384m、 S384xm、 S576、 S768 及我們的 S960 tooas hello 'Type II class' 的 Sku。

它是完整的 HANA 大型執行個體戳記以獨佔方式不會配置給單一客戶 &#39; 的重要 toonote s 使用。 這項事實適用於透過網路網狀架構也部署在 Azure 中連接的運算和存放裝置資源的 toohello 機架。 HANA 大型執行個體的基礎結構，例如 Azure、 部署不同的客戶&quot;租用戶&quot;，會在下列三個層級的 hello 與另一個隔離：

- 透過 hello HANA 大型執行個體戳記內的虛擬網路的網路： 隔離。
- 儲存體：透過已獲派存放磁碟區的存放虛擬機器來區隔，以及在租用戶之間隔開存放磁碟區。
- 計算： 專用伺服器單位 tooa 單一租用戶的指派。 不對伺服器單位進行硬體分割或軟體分割。 不在租用戶之間共用單一伺服器或主機單位。 

因此，hello 部署 HANA 大型執行個體之間的單位不同的租用戶不可見 tooeach 其他。 也可以 HANA 部署在不同的租用戶大型執行個體單位彼此直接 hello HANA 大型執行個體戳記層級上。 只有 HANA 大型執行個體單位內一個租用戶可以通訊 tooeach 其他 hello HANA 大型執行個體戳記層級上。
Hello 大型執行個體戳記中的已部署租用戶指派計費明智 tooone Azure 訂用帳戶。 不過，它可以從 Azure Vnet 中的其他 Azure 訂用帳戶存取網路明智 hello 相同 Azure 註冊。 如果您使用另一個 Azure 訂用帳戶中 hello 部署相同 Azure 區域，您也可以選擇 tooask 分隔 HANA 大型執行個體租用戶。

在「HANA 大型執行個體」上執行 SAP HANA 與在於 Azure 中部署的 Azure VM 上執行 SAP HANA 之間有顯著的不同：

- SAP HANA on Azure (大型執行個體) 沒有虛擬化層。 取得 hello hello 基礎裸機硬體效能時。
- 不同於 Azure、 Azure （大型執行個體） 的伺服器上的 SAP HANA hello 是專用的 tooa 特定客戶。 您無法對伺服器單位或主機進行硬體分割或軟體分割。 如此一來，HANA 大型執行個體單位當做整個 tooa 租用戶身分與該客戶的 tooyou 指派。 重新開機或關機的 hello 伺服器不會導致自動 toohello 作業系統與在另一部伺服器上部署的 SAP HANA。 (類型 I 類別 Sku，hello 唯一的例外是，如果伺服器可能會遇到問題，並重新部署需要 toobe 另一部伺服器上執行。)
- 不同於 Azure 中，其中的 hello 最佳的效能比選取類型主機的處理器，選擇 Azure （大型執行個體） 上的 SAP hana hello 處理器的類型是 hello hello Intel E7v3 和 E7v4 處理器線條的最高執行。


### <a name="running-multiple-sap-hana-instances-on-one-hana-large-instance-unit"></a>在一個 HANA 大型執行個體單位上執行多個 SAP HANA 執行個體
很可能 toohost 多個一個作用中的 SAP HANA 執行個體 hello HANA 大型執行個體單元上。 為了 toostill 提供的儲存體的快照集的 hello 功能和嚴重損壞修復，這種組態中需要設定每個執行個體的磁碟區。 目前，hello HANA 大型執行個體單位可以再細分，如下所示：

- S72、 S72m S144、 S192： 在以 256 GB hello 最小的增量為 256 GB 啟動單位。 Hello 單位的 hello 記憶體結合的 toohello 最多可以像 256 GB，512 GB，依此類推，不同的遞增。
- S144m 和 S192m: 512GB hello 最小單位的增量為 256 GB。 不同的增量，像 512 GB、 768 GB，依此類推，可以結合的 toohello 最大值為 hello 單位的 hello 記憶體。
- 輸入第二部分類別： 以 hello 啟動單元 2 TB 的最小為 512 GB 增量。 Hello 單位的 hello 記憶體結合的 toohello 最多可以不同的增量，像 512 GB、 1 TB，1.5 TB，等等。

有一些執行多個 SAP HANA 執行個體的範例看起來如下：

| SKU | 記憶體大小 | 儲存體大小 | 具有多個資料庫的大小 |
| --- | --- | --- | --- |
| S72 | 768 GB | 3 TB | 1x768 GB HANA 執行個體<br /> 或 1x512 GB 執行個體 + 1x256 GB 執行個體<br /> 或 3x256 GB 執行個體 | 
| S72m | 768 GB | 3 TB | 3x512GB HANA 執行個體<br />或 1x512 GB 執行個體 + 1x1 TB 執行個體<br />或 6x256 GB 執行個體<br />或 1x1.5 TB 執行個體 | 
| S192m | 4 TB | 16 TB | 8x512 GB 執行個體<br />或 4x1 TB 執行個體<br />或 4x512 GB 執行個體 + 2x1 TB 執行個體<br />或 4x768 GB 執行個體 + 2x512 GB 執行個體<br />或 1x4 TB 執行個體 |
| S384xm | 8 TB | 22 TB | 4x2 TB 執行個體<br />或 2x4 TB 執行個體<br />或 2x3 TB 執行個體 + 1x2 TB 執行個體<br />或 2x2.5 TB 執行個體 + 1x3 TB 執行個體<br />或 1x8 TB 執行個體 |


您收到 hello 概念。 當然還有其他變化形式。 


## <a name="operations-model-and-responsibilities"></a>作業模型和職責

提供與 Azure （大型執行個體） 上的 SAP HANA 的 hello 服務與 Azure IaaS 服務對齊。 您會獲得一個「HANA 大型執行個體」執行個體，其中已安裝針對 SAP HANA 最佳化的作業系統。 與 Azure IaaS Vm，大部分的 hello 工作強化 hello 的作業系統上，安裝其他軟體需要安裝 HANA 的操作 hello OS 和 HANA，以及更新 hello OS 和 HANA 是您的責任。 Microsoft 不會強制您進行 OS 更新或 HANA 更新。

![SAP HANA on Azure (大型執行個體) 的職責](./media/hana-overview-architecture/image2-responsibilities.png)

您可以看到在 hello 圖中，在 Azure （大型執行個體） 上的 SAP HANA 是基礎結構的多租用戶的服務優惠。 如此一來，hello 地分隔責任位於 hello OS 基礎結構的界限，hello 大部分的一部分。 Microsoft 會負責 hello 服務 hello 作業系統 hello 行底下的所有層面，同時您有責任 hello 線條，包括 hello 作業系統上方。 因此最新的內部方法可能會採用您相容性、 安全性、 應用程式管理、 為基礎，以及 OS 管理可以繼續使用 toobe。 hello 系統出現就是您網路中所有的相關事宜。

不過，此服務已最佳化 SAP hana，因此有的區域，您與 Microsoft 需要 toowork 一起 toouse hello 基礎基礎結構功能為獲得最佳結果。

hello 下列清單提供有關每個 hello 圖層與您的責任的更多詳細資料：

**網路功能：**所有 hello stamp hello 大型執行個體執行 SAP HANA，其存取 toohello 儲存體，hello （適用於向外延展和其他函式） 的執行個體、 連線 toohello 橫向和連線之間的連線的內部網路tooAzure hello SAP 應用程式層裝載在 Azure 虛擬機器。 它也包含用於「災害復原」用途複寫的「Azure 資料中心」間 WAN 連線。 所有網路都分割 hello 租用戶，並套用 QOS。

**儲存體：** hello 虛擬化的資料分割的儲存體 hello SAP HANA 伺服器所需的所有磁碟區以及快照集。 

**伺服器：** hello 專用實體伺服器 toorun hello 分派 tootenants SAP HANA 資料庫使用。 hello 伺服器 hello 我類別的類型的 Sku 是抽象的硬體。 使用這些類型的伺服器，而 hello 伺服器設定需要收集及維護可移動從一個實體硬體 tooanother 實體硬體設定檔中。 這類 （手動） 移動設定檔的作業可以進行比較的位元 tooAzure 服務修復後依然存在。 hello 伺服器 hello Type II 類別 Sku 不提供這類功能。

**SDDC:** hello 管理軟體，是使用的 toomanage 資料中心做軟體定義的實體。 它可讓 Microsoft toopool 資源的規模、 可用性和效能的考量。

**O/S:** hello （SUSE Linux 或 Red Hat Linux），您選擇的 OS hello 伺服器上執行。 會為您提供的 hello OS 映像與 hello 個別 Linux 廠商 tooMicrosoft 所提供的 hello 目的是要執行 SAP HANA 的 hello 映像。 您會需要的 toohave hello 特定 SAP HANA 最佳化映像的 hello Linux 廠商的訂用帳戶。 您的責任包括向 hello OS 廠商 hello 映像。 從 microsoft 移 hello 點，您必須也負責 hello Linux 作業系統的任何進一步修補。 這項修補動作也包含可能是成功的 SAP HANA 安裝所需的其他套件 （請參閱 tooSAP 的 HANA 安裝文件集和 SAP 附註） 和其中有尚未包含在其 SAP HANA hello 特定 Linux 廠商最佳化 OS 映像。 hello hello 客戶責任也包含的是相關的 toomalfunction/最佳化 hello OS 和其驅動程式相關的 toohello 特定的伺服器硬體的 hello OS 修補程式。 任何安全性或功能的 hello OS 修補程式。 客戶也要負責監視和容量規劃︰

- CPU 資源耗用量
- 記憶體耗用量
- 磁碟區相關 toofree 空間、 IOPS 和延遲
- 「HANA 大型執行個體」與 SAP 應用程式層之間的網路磁碟區流量

hello HANA 大型執行個體的基礎結構提供備份和還原 hello OS 磁碟區的功能。 使用這項功能也是您的職責所在。

**中介軟體：**主要 hello SAP HANA 執行個體。 管理、操作及監視是您的職責。 沒有功能，可讓您 toouse 儲存體的快照集備份/還原和災害復原用途提供。 Hello 基礎結構會提供這些功能。 不過，您的職責還包括使用這些功能來設計高可用性或災害復原、利用它們，以及監視儲存體快照集是否已順利執行。

**資料：**您受 SAP HANA 管理的資料，以及其他位於磁碟區或檔案共用上的資料 (例如備份檔案)。 您的責任包括監視磁碟可用空間以及管理 hello hello 的磁碟區上的內容和監視 hello 順利執行備份的磁碟區與儲存快照集。 不過，成功執行的站台的複寫 tooDR 資料是 Microsoft hello 責任。

**應用程式：** hello SAP 應用程式執行個體或發生非 SAP 應用程式，這些應用程式的 hello 應用程式層。 您的責任包括部署、 管理、 作業和監視這些應用程式的相關 toocapacity 規劃的 CPU 資源耗用量、 記憶體耗用量、 Azure 儲存體耗用量和內耗用網路頻寬Azure Vnet，以及從 Azure Vnet tooSAP HANA Azure （大型執行個體） 上。

**Wan:** hello 您建立從內部 tooAzure 部署工作負載的連線。 所有具有 HANA 大型執行個體的客戶都會使用 Azure ExpressRoute 連線。 此連線不 hello SAP HANA Azure （大型執行個體） 方案的一部分，因此您必須負責此連線的 hello 安裝程式。

**封存：**您可能會偏好 tooarchive 份資料儲存體帳戶中使用您自己的方法。 封存需要管理、合規性、成本及操作。 您需負責在 Azure 上產生封存複本和備份，並以符合規範的方式儲存它們。

請參閱 hello [Azure （大型執行個體） 上的 SAP hana SLA](https://azure.microsoft.com/support/legal/sla/sap-hana-large/v1_0/)。

## <a name="sizing"></a>調整大小

「HANA 大型執行個體」的大小調整與 HANA 的大小調整大致上沒有差別。 現有的部署的系統，以及您想從其他 RDBMS tooHANA toomove，SAP 提供數個現有的 SAP 系統執行的報告。 如果移動的 tooHANA hello 資料庫，這些報告檢查 hello 資料並計算 hello HANA 執行個體的記憶體需求。 閱讀下列 SAP 附註 tooget hello 上 toorun 這些報告的方式的詳細資訊及如何 tooobtain 其最新修補程式/版本：

- [SAP 附註 #1793345 - SAP Suite on HANA 的大小調整 (英文)](https://launchpad.support.sap.com/#/notes/1793345)
- [SAP 附註 #1872170 - Suite on HANA 與 S/4 HANA 大小調整報告 (英文)](https://launchpad.support.sap.com/#/notes/1872170)
- [SAP 附註 #2121330 - 常見問題集：SAP BW on HANA 大小調整報告 (英文)](https://launchpad.support.sap.com/#/notes/2121330)
- [SAP 附註 #1736976 - BW on HANA 的大小調整報告 (英文)](https://launchpad.support.sap.com/#/notes/1736976)
- [SAP 附註 #2296290 - 新的 BW on HANA 大小調整報告 (英文)](https://launchpad.support.sap.com/#/notes/2296290)

綠色欄位實作 SAP 快速 Sizer 是 SAP HANA 之上的軟體 hello 實作可用 toocalculate 記憶體需求。

隨著資料量增加 hana 的記憶體需求，因此您想 toobe 注意現在 hello 記憶體耗用量，是無法 toopredict 它是在進入 toobe hello 未來。 根據 hello 記憶體需求，您便可以對應您指定成一個 hello HANA 大型執行個體 Sku。

## <a name="requirements"></a>需求

此清單彙編了執行 SAP HANA on Azure (大型執行個體) 的需求。

**Microsoft Azure：**

- 可以是 Azure 訂用帳戶連結 tooSAP HANA Azure （大型執行個體） 上。
- Microsoft 頂級支援合約。 請參閱[SAP 支援附註 #2015553-Microsoft Azure 上的 SAP： 支援必要條件](https://launchpad.support.sap.com/#/notes/2015553)對於特定資訊與相關 toorunning Azure 中 SAP。 使用 HANA 大型執行個體單位 384 和更多的 Cpu，您也需要 tooextend hello Premier Support 合約 tooinclude Azure 快速回應 (ARR)。
- 感知的 hello HANA 大型執行個體 SAP 的 Sku，您需要執行調整大小之後運用。

**網路連線︰**

- Azure ExpressRoute 之間內部 tooAzure: tooconnect 您在內部部署資料中心 tooAzure，請確定 tooorder 速度至少 1 Gbps 連線從您的 ISP。 

**作業系統︰**

- SUSE Linux Enterprise Server 12 for SAP Applications 的授權。

> [!NOTE] 
> hello 由 Microsoft 提供的作業系統未向 SUSE，也不連接 SMT 執行個體。

- 部署在 Azure VM 上 Azure 中的 SUSE Linux Subscription Management Tool (SMT)。 這提供 hello 能力 SAP hana Azure （大型執行個體） toobe 註冊並分別由更新 SUSE （因為沒有 HANA 大型執行個體資料中心內沒有網際網路存取）。 
- Red Hat Enterprise Linux for SAP HANA 6.7 或 7.2 的授權。

> [!NOTE]
> hello 由 Microsoft 提供的作業系統未向 Red Hat，也不是 it 連接 tooa Red Hat 訂用帳戶管理員執行個體。

- 部署在 Azure VM 上 Azure 中的 Red Hat Subscription Manager。 hello Red Hat 訂用帳戶管理員註冊並分別由更新 Red Hat （因為沒有直接網際網路存取從 hello Azure 大型執行個體戳記上部署的 hello 租用戶內） 的 Azure （大型執行個體） toobe SAP hana 提供 hello 能力。
- SAP 需要的 toohave 您 Linux 提供者的支援合約。 這項需求不會清除 HANA 大型執行個體或 hello 事實的 hello 解決方案，您在 Azure 中的執行的 Linux。 不同於某些 hello Linux Azure 資源庫映像，hello 服務費用不隨附於 hello 方案提供的 HANA 大型執行個體。 它是 SAP 的您在客戶 toofulfill hello 需求支援合約與 hello Linux 散發者。   
   - SUSE linux，查詢的支援需求合約中的 hello [SAP 附註 #1984787 SUSE LINUX Enterprise Server 12： 安裝注意事項](https://launchpad.support.sap.com/#/notes/1984787)和[SAP 附註 #1056161-SUSE 優先順序支援的 SAP 應用程式](https://launchpad.support.sap.com/#/notes/1056161).
   - Red Hat linux，您需要 toohave hello 正確的訂用帳戶層級，包括支援及服務 （更新 toohello 作業系統 HANA 大型執行個體。 Red Hat 建議取得「RHEL for SAP 商務應用程式」訂用帳戶。 如需支援與服務的詳細資訊，請查看 [SAP 附註 #2002167 - Red Hat Enterprise Linux 7.x：安裝和升級](https://launchpad.support.sap.com/#/notes/2002167) \(英文\) 和 [SAP 附註 #1496410 - Red Hat Enterprise Linux 6.x：安裝和升級](https://launchpad.support.sap.com/#/notes/1496410) \(英文\)。

**資料庫：**

- SAP HANA (平台或企業版) 的授權和軟體安裝元件。

**應用程式︰**

- 授權和任何連接 tooSAP HANA 和相關的 SAP 支援合約的 SAP 應用程式的軟體安裝元件。
- 授權與任何非 SAP 應用程式的軟體安裝元件關聯 tooSAP HANA Azure （大型執行個體） 環境中使用，以及相關支援合約。

**技能︰**

- Azure IaaS 及其元件的相關經驗與知識。
- 在 Azure 中部署 SAP 工作負載的相關經驗與知識。
- 合格的 SAP HANA 安裝人員。
- SAP 架構設計人員技能 toodesign 高可用性和 SAP HANA 周圍的災害復原。

**SAP：**

- 預期您是 SAP 客戶且與 SAP 有支援合約
- 特別是針對 hello HANA 大型執行個體 Sku 的 Type II 類別上實作，強烈建議 tooconsult 與 SAP 版本的 SAP HANA 和最終大小的大型向上延展硬體上的組態。


## <a name="storage"></a>儲存體

hello Azure （大型執行個體） 上的 SAP hana 的儲存配置設定上透過建議的指導方針，記載於 hello SAP 的 Azure 服務管理的 SAP HANA [SAP HANA 存放裝置需求](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html)技術白皮書。

hello HANA 大型執行個體的 hello 我類別的型別會隨附四次 hello 記憶體磁碟區做為存放磁碟區。 Hello 類型 HANA 大型執行個體單位的第二部分類別，hello 儲存體不會進入 toobe 更四次。 hello 單位隨附適用於儲存 HANA 交易記錄備份的磁碟區。 尋找更多詳細資料中的[如何 tooinstall 及設定 Azure 上 SAP HANA （大型執行個體）](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

請參閱下表根據存放裝置配置 hello。 hello 表格列出大約 hello hello hello 不同 HANA 大型執行個體單位所提供的不同磁碟區容量。

| HANA 大型執行個體 SKU | hana/data | hana/log | hana/shared | hana/log/backup |
| --- | --- | --- | --- | --- |
| S72 | 1280 GB | 512 GB | 768 GB | 512 GB |
| S72m | 3328 GB | 768 GB |1280 GB | 768 GB |
| S192 | 4608 GB | 1024 GB | 1536 GB | 1024 GB |
| S192m | 11,520 GB | 1536 GB | 1792 GB | 1536 GB |
| S384 | 11,520 GB | 1536 GB | 1792 GB | 1536 GB |
| S384m | 12,000 GB | 2050 GB | 2050 GB | 2040 GB |
| S384xm | 16,000 GB | 2050 GB | 2050 GB | 2040 GB |
| S576 | 20,000 GB | 3100 GB | 2050 GB | 3100 GB |
| S768 | 28,000 GB | 3100 GB | 2050 GB | 3100 GB |
| S960 | 36,000 GB | 4100 GB | 2050 GB | 4100 GB |


實際部署的磁碟區可能會因位元上部署和使用的 tooshow hello 磁碟區大小的工具。

如果您要細分 HANA 大型執行個體 SKU，以下提供一些可能的劃分片段範例：

| 記憶體磁碟分割，以 GB 為單位 | hana/data | hana/log | hana/shared | hana/log/backup |
| --- | --- | --- | --- | --- |
| 256 | 400 GB | 160 GB | 304 GB | 160 GB |
| 512 | 768 GB | 384 GB | 512 GB | 384 GB |
| 768 | 1280 GB | 512 GB | 768 GB | 512 GB |
| 1024 | 1792 GB | 640 GB | 1024 GB | 640 GB |
| 1536 | 3328 GB | 768 GB | 1280 GB | 768 GB |


這些大小會粗略的磁碟區數字，可能會稍微依據部署工具在和使用 toolook hello 磁碟區。 此外，還有其他的磁碟分割大小可納入考量，例如 2.5 TB。 以上述的 hello 資料分割所使用的類似公式會計算這些存放區大小。 hello 詞彙 'partitions' 不表示，hello 作業系統、 記憶體或 CPU 資源會以任何方式進行資料分割。 它只表示儲存體的資料分割的單一 HANA 大型執行個體單元您其中一個上的 toodeploy hello 不同 HANA 執行個體。 

您為一個客戶可能會有需要的更多存放裝置，您必須 hello 可能性 tooadd 儲存體 toopurchase 額外的存放裝置以 1 TB 為單位。 此額外的存放裝置可以加入額外的磁碟區，也可使用的 tooextend 一或多個 hello 現有磁碟區。 它不可能 toodecrease hello hello 磁碟區大小一開始部署和大部分 hello 資料表上面所記載。 它也不是 hello 磁碟區可能 toochange hello 名稱或掛接的名稱。 hello 存放磁碟區 （如上所述） 是附加的 toohello HANA 大型執行個體單位為 NFS4 磁碟區。

您的客戶可以選擇 toouse 儲存體的快照集備份/還原和災害復原用途。 如需有關此主題的更多詳細資料，請參閱 [Azure 上 SAP Hana (大型執行個體) 的高可用性和災害復原](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

### <a name="encryption-of-data-at-rest"></a>待用資料加密
hello HANA 大型執行個體所用的儲存體允許 hello 資料透明加密儲存在 hello 磁碟上。 HANA 大型執行個體單位的部署階段，在您擁有 hello 選項 toohave 這種加密已啟用。 您也可以選擇 toochange tooencrypted 磁碟區已 hello 部署之後。 從非加密 tooencrypted 磁碟區的 hello 移動是透明的而且不需要停機時間。 

以 hello 我類別 hello LUN 的所在的磁碟區 hello 開機的 Sku 的型別會加密。 發生 hello 類型的 Sku 的 HANA 大型執行個體的第二部分類別，您需要使用 OS 方法 tooencrypt hello 開機 LUN。 


## <a name="networking"></a>網路

Azure 網路的 hello 架構是重要元件 toosuccessful 部署的 SAP HANA 大型執行個體上的應用程式。 一般而言，SAP HANA on Azure (大型執行個體) 部署具有較大的 SAP 架構，其中包含數個擁有不同資料庫大小、CPU 資源耗用量及記憶體使用量的不同 SAP 解決方案。 很可能不是那些所有的 SAP 系統都是以 SAP HANA 為基礎，因此您的 SAP 架構可能是使用下列各項的混合式架構：

- 部署在內部部署環境中的 SAP 系統。 由於 tootheir 大小，這些系統無法目前裝載於 Azure。典型的範例是 Microsoft SQL Server 上執行 （與 hello 資料庫） 需要更多 CPU 的實際執行 SAP ERP 系統，或可以提供 Azure Vm 的記憶體資源。
- 部署在內部部署環境中以 SAP HANA 為基礎的 SAP 系統。
- 部署在 Azure VM 中的 SAP 系統。 這些系統可能是開發、 測試、 沙箱，或生產環境的 hello SAP NetWeaver 型應用程式，才能成功部署在 Azure 中 （上的 Vm)，根據資源耗用量和記憶體需求的任何執行個體。 這些系統也可利用資料庫為根據，例如 SQL Server (請參閱 [SAP 支援附註 #1928533 - Azure 上的 SAP 應用程式︰支援的產品和 Azure VM 類型](https://launchpad.support.sap.com/#/notes/1928533/E) \(英文\)) 或 SAP HANA (請參閱 [SAP HANA 認證的 IaaS 平台](http://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html) \(英文\))。
- 部署在 Azure (在 VM 上) 中並利用「Azure 大型執行個體」戳記中 SAP HANA on Azure (大型執行個體) 的 SAP 應用程式伺服器。

儘管混合式 SAP 架構 (含有四個以上的不同部署案例) 為典型架構，還是有許多在 Azure 中完成 SAP 架構執行的客戶案例。 為 Microsoft Azure Vm 變得更強大了，會增加客戶在 Azure 上移動他們的所有 SAP 解決方案的 hello 數目。

Azure 網路中的 SAP 系統部署在 Azure 中的 hello 內容並不複雜。 它根據下列準則的 hello:

- Azure 虛擬網路 (Vnet) 需要 tooon 內部部署網路連線的連線 toobe toohello Azure ExpressRoute 電路。
- ExpressRoute 電路連線在內部部署 tooAzure 通常應該為 1 Gbps 以上的頻寬。 這個最少的頻寬可讓您有足夠的頻寬在內部部署系統和 Azure Vm （以及從使用者的內部連接 tooAzure 系統） 上執行的系統之間傳送資料。
- 在 Azure Vnet toocommunicate 彼此設定 Azure 需要 toobe 中的所有 SAP 系統。
- 裝載於內部部署環境中的 Active Directory 與 DNS 會透過 ExpressRoute 從內部部署環境延伸到 Azure。


> [!NOTE] 
> 從計費的觀點，只能有單一的 Azure 訂閱可以連結只 tooone 單一租用戶在大型執行個體中的戳記特定的 Azure 地區，而且必須相反的單一大型執行個體戳記租用戶可連結 tooone Azure 訂用帳戶。 這項事實是一樣的 tooany Azure 中的其他計費物件

部署在多個不同的 Azure 地區的 Azure （大型執行個體） 上的 SAP HANA，結果在不同的租用戶 toobe 部署在 hello 大型執行個體的戳記。 不過，您可以執行兩下 hello 相同 Azure 訂用帳戶只要這些執行個體屬於 hello 相同 SAP 版圖。 

> [!IMPORTANT] 
> 使用 SAP HANA on Azure (大型執行個體) 時，僅支援「Azure 資源管理」部署。

 

### <a name="additional-azure-vnet-information"></a>其他 Azure VNet 資訊

在順序 tooconnect Azure VNet tooExpressRoute，您必須建立 Azure 的閘道 (請參閱[需 ExpressRoute 的虛擬網路閘道](../../../expressroute/expressroute-about-virtual-network-gateways.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))。 可以使用 Azure 的閘道與 ExpressRoute tooan 基礎結構外 Azure （或 tooan Azure 大型執行個體戳記），或 Azure Vnet 之間 tooconnect (請參閱[讓資源管理員使用 PowerShell 設定 VNet 對 VNet 連線](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). 只要這些連接來自不同的 MS 企業邊緣 (MSEE) 路由器，您可以連接 hello Azure 閘道 tooa 最多四個不同的 ExpressRoute 連線。  如需詳細資料，請參閱 [Azure 上 SAP HANA (大型執行個體) 的基礎結構和連接](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 

> [!NOTE] 
> hello Azure 閘道所提供的輸送量是不同的同時使用案例 (請參閱[有關 VPN 閘道](../../../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))。 hello 與 VNet 閘道，我們可以達到的最大輸送量是 10 Gbps，使用 ExpressRoute 連線。 請記住，Azure VM 中 Azure VNet 和系統之間複製檔案在內部部署 （單一複本資料流的形式） 不會無法達成的 hello 不同的閘道 Sku hello 輸送量。 tooleverage hello 完整的頻寬 hello VNet 閘道，您必須使用多個資料流或複製不同檔案中的單一檔案的平行資料流。


### <a name="networking-architecture-for-hana-large-instances"></a>適用於 HANA 大型執行個體的網路架構
hello HANA 大型執行個體的網路架構如下所示，工作可以分割分為四個不同的部分：

- 在內部部署網路和 ExpressRoute 連線 tooAzure。 這是 hello 客戶網域和透過 ExpressRoute 連接的 tooAzure。 這是在 hello 右下角 hello 圖形下方的 hello 部分。
- Azure 網路，如同上述對於 Azure VNet 的簡短討論，再次提醒，其中具有閘道。 這是您需要 toofind hello 適當設計您的應用程式需求、 安全性和法規遵循需求的區域。 使用 HANA 大型執行個體是從 Vnet 和 Azure 閘道 Sku toochoose 數量考量的另一個點。 這是在 hello 右上方的 hello 圖形中的 hello 部分。
- HANA 大型執行個體透過 ExpressRoute 技術連線至 Azure。 這部分已部署且會由 Microsoft 來處理。 您只需要 toodo 因為客戶 tooprovide 一些 IP 位址範圍，而且您資產 HANA 大型執行個體連接的 hello 部署後 hello ExpressRoute 電路 toohello Azure VNet(s) (請參閱[SAP HANA （大型執行個體） 基礎結構和在 Azure 上的連線能力](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))。 
- HANA 大型執行個體中的網路功能，對於身為客戶的您而言，大部分是透明的。

![Azure VNet 連接 tooSAP HANA Azure （大型執行個體） 和內部部署上](./media/hana-overview-architecture/image3-on-premises-infrastructure.png)

您使用 HANA 大型執行個體的 hello 事實不會變更您在內部部署資產連接透過 ExpressRoute tooAzure hello 需求 tooget。 它也不會變更 hello 需求有一或多個連接單位 HANA 大型執行個體所裝載的 toohello HANA 執行個體的主機 hello 應用程式層級執行 hello Azure Vm 的 Vnet。 

在純 hello 差異 tooSAP 部署 Azure 中，隨附 hello 事實的：

- 您的客戶租用戶的 hello HANA 大型執行個體單位互相連線到 Azure VNet(s) 透過另一個 ExpressRoute 電路。 在訂單 tooseparate 負載情況下，Vnet ExpressRoute 連結和 Azure Vnet 和 HANA 大型執行個體之間的連結就不會共用 hello 內部 tooAzure hello 相同路由器。
- hello hello SAP 應用程式層與 hello HANA 執行個體之間的工作負載設定檔是許多小型要求不同的性質，以及資料的高載從 SAP HANA 傳送 （結果集），到 hello 應用程式層。
- hello SAP 應用程式架構是更為敏感 toonetwork 延遲比在內部部署與 Azure 之間交換資料取得的典型案例。
- hello VNet 閘道可以在至少兩個 ExpressRoute 連線，而且這兩個連接共用 hello hello VNet 閘道的內送資料的最大頻寬。

Azure Vm 和 HANA 大型執行個體單位之間有經驗的 hello 網路延遲可能會高於一般的 VM-VM 網路來回延遲時間。 相依於 hello Azure 地區，測量 hello 值可以超過 hello 0.7 ms 來回延遲低於平均分類[SAP 附註 #1100926 常見問題集： 網路效能](https://launchpad.support.sap.com/#/notes/1100926/E)。 不過，客戶很順利在 SAP HANA 大型執行個體上部署以 SAP HANA 為基礎的生產環境 SAP 應用程式。 部署的 hello 客戶所執行的 SAP 應用程式上使用大型執行個體 HANA 單位的 SAP HANA 報告優越改良。 不過，您應該在 Azure HANA 大型執行個體中徹底測試您的商務程序。
 
在 Azure Vm 和 HANA 大型執行個體之間的順序 tooprovide 具決定性的網路延遲，hello Azure VNet 的閘道 SKU hello 選擇是不可或缺的。 不同於在內部部署與 Azure Vm 之間的 hello 流量模式，hello Azure Vm 和 HANA 大型執行個體之間的流量模式可以開發小型但較高的要求，以及傳輸的資料磁碟區 toobe 暴增。 順序 toohave 中，處理這類暴增我們強烈建議 hello 的 hello UltraPerformance 閘道 SKU 的使用方式。 Hello HANA 大型執行個體 Sku 的型別第二部分類別，hello 使用量的 hello UltraPerformance 閘道 SKU 為 Azure VNet 閘道是必要的。  

> [!IMPORTANT] 
> 指定的 hello hello SAP 應用程式和資料庫層之間的整體網路流量只 hello 高效能的分散式或支援 UltraPerformance 閘道 Sku vnet 連接 tooSAP HANA Azure （大型執行個體） 上。 Hello UltraPerformance 閘道 SKU HANA 大型執行個體類型 II Sku，支援為 Azure VNet 閘道。



### <a name="single-sap-system"></a>單一 SAP 系統

如上所示的 hello 在內部部署基礎結構透過 ExpressRoute 連接到 Azure，而 hello ExpressRoute 電路連接到 Microsoft 企業邊緣路由器 (MSEE) (請參閱[ExpressRoute 技術概觀](../../../expressroute/expressroute-introduction.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))。 一旦建立，該路由會連接到 hello Microsoft Azure 中樞，並可存取所有 Azure 地區。

> [!NOTE] 
> 在 Azure 中執行 SAP 環境，則連接 toohello MSEE 最接近 toohello hello SAP 環境中的 Azure 區域。 Azure 在大型執行個體戳記是透過專用 MSEE 裝置 toominimize 之間的網路延遲在 Azure IaaS 和大型執行個體戳記中的 Azure Vm 中連接。

hello hello 裝載 SAP 應用程式執行個體，Azure Vm 的 VNet 閘道連接的 toothat ExpressRoute 電路，而 hello 相同的 VNet 連接的 tooa 個別專用 MSEE 路由器 tooconnecting tooLarge 執行個體戳記。

這是單一的 SAP 系統，其中 hello SAP 應用程式層裝載於 Azure hello SAP HANA 資料庫並執行 Azure （大型執行個體） 上的 SAP HANA 的簡單範例。 hello 假設是 2 Gbps 的 hello VNet 閘道頻寬，或 10 Gbps 輸送量不是瓶頸。

### <a name="multiple-sap-systems-or-large-sap-systems"></a>多個 SAP 系統或大型 SAP 系統

如果多個 SAP 系統或大型的 SAP 系統部署連接 tooSAP HANA Azure （大型執行個體），它 &#39; s 合理 tooassume hello 輸送量 hello VNet 閘道可能成為瓶頸。 在這種情況下，您需要多個 Azure Vnet toosplit hello 應用程式層級。 它也可能是時 toocreate 特殊 Vnet 連接 tooHANA 大型執行個體，如案例：

- 執行備份直接從 hello HANA 執行個體中 HANA 大型執行個體 tooa VM 在 Azure 中裝載的 NFS 共用
- 大型備份或其他檔案複製從 HANA 大型執行個體在 Azure 中管理的單位 toodisk 空間。

使用個別的 Vnet 主機管理 hello 儲存體的 Vm 可避免影響大型檔案，或從 HANA 大型執行個體 tooAzure 傳送 hello 做執行 hello SAP 應用程式層的 hello Vm 的 VNet 閘道上的資料。 

讓網路架構更具彈性：

- 針對單一的較大 SAP 應用程式層，運用多個 Azure VNet。
- 部署一個個別 Azure VNet，每個 SAP 系統部署，比較 toocombining 底下的個別子網路中的這些 SAP 系統 hello 相同的 VNet。

 適用於 SAP HANA on Azure (大型執行個體) 的更有彈性網路架構：

![跨多個 Azure VNet 部署 SAP 應用程式層](./media/hana-overview-architecture/image4-networking-architecture.png)

多個 Azure Vnet，如上所示，透過部署 hello SAP 應用程式層或元件，引進無可避免之延遲裝載在這些 Azure Vnet 中的 hello 應用程式間進行通訊時所發生的額外負荷。 根據預設，hello Azure Vm 之間的網路流量位於不同的 Vnet 路由透過 hello MSEE 路由器，在此設定。 不過，自 2016 年 9 月起，可將這個路由傳送最佳化。 hello 方式 toooptimize 和減少兩個之間的通訊中的 hello 延遲 hello 內的對等互連 Azure Vnet 的 Vnet 是相同的區域。 即使那些 VNet 在不同的訂用帳戶中也一樣。 使用 Azure VNet 對等互連，在兩個不同的 Azure Vnet 中的 Vm 之間的 hello 通訊可以使用 hello Azure 網路骨幹 toodirectly 與對方進行通訊。 藉此顯示類似延遲如同 hello Vm 可能會在 hello 相同的 VNet。 而定址經由 hello Azure VNet 閘道連線的 IP 位址範圍的流量都會透過路由傳送 hello 個別的 hello VNet 的 VNet 閘道。 您可以取得有關 Azure VNet 的詳細資料 hello 文件中的對等互連[對等互連的 VNet](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview)。


### <a name="routing-in-azure"></a>Azure 中的路由

SAP HANA on Azure (大型執行個體) 有兩個重要的網路路由考量：

1. 在 Azure （大型執行個體） 上的 SAP HANA 只能由 Azure Vm 存取在專用的 hello ExpressRoute 連線;不是直接從內部部署。 某些管理用戶端及任何應用程式需要直接存取，例如執行內部部署 SAP Solution Manager 無法連線 toohello SAP HANA 資料庫。

2. 在 Azure （大型執行個體） 單位上的 SAP HANA 有指派的 IP 位址從 hello 伺服器的 IP 集區位址範圍您送出 hello 客戶 (請參閱[SAP HANA （大型執行個體） 基礎結構和在 Azure 上的連線能力](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)如需詳細資訊)。  此 IP 位址是透過 hello Azure 訂用帳戶和 ExpressRoute 連接 Azure Vnet tooHANA Azure （大型執行個體） 上的。 hello 超出該伺服器的 IP 集區位址範圍指派 IP 位址直接指派 toohello 硬體單元，且不 NAT'ed 因為這是在 hello 第一個部署此解決方案中的 hello 案例。 

> [!NOTE] 
> 如果您需要在 tooconnect tooSAP Azure （大型執行個體） 上的 HANA_資料倉儲_案例中，其中應用程式和 （或） 使用者需要 tooconnect toohello SAP HANA 資料庫 （直接執行），必須是另一個網路元件使用： 反向 proxy tooroute 資料、 從 tooand。 例如，搭配部署在 Azure 中作為虛擬防火牆/流量路由解決方案之「流量管理員」的 F5 BIG-IP、NGINX。

### <a name="internet-connectivity-of-hana-large-instances"></a>HANA 大型執行個體的網際網路連線
「HANA 大型執行個體」無法直接連線到網際網路。 這會限制您能力，例如註冊 hello OS 映像，直接與 hello OS 廠商。 因此，您可能需要 toowork 與本機 SLES SMT 伺服器或 RHEL 訂用帳戶管理員

### <a name="data-encryption-between-azure-vms-and-hana-large-instances"></a>Azure VM 與 HANA 大型執行個體之間的資料加密
「HANA 大型執行個體」與 Azure VM 之間的資料傳輸並未加密。 不過，純粹 hello 之間的交換 hello HANA DBMS 方面和 JDBC/ODBC 為基礎的應用程式，您可以啟用加密的流量。 請參考 [SAP 提供的這份文件](http://help-legacy.sap.com/saphelp_hanaplatform/helpdata/en/db/d3d887bb571014bf05ca887f897b99/content.htm?frameset=/en/dd/a2ae94bb571014a48fc3b22f8e919e/frameset.htm&current_toc=/en/de/ec02ebbb57101483bdf3194c301d2e/plain.htm&node_id=20&show_children=false) \(英文\)

### <a name="using-hana-large-instance-units-in-multiple-regions"></a>在多個區域中使用 HANA 大型執行個體單位

多個 Azure 區域的詳細資訊，除了災害復原中，您可能有其他原因 toodeploy Azure （大型執行個體） 上的 SAP HANA。 也許您想從每個 hello Vm 部署在 hello tooaccess HANA 大型執行個體不同的 Vnet hello 區域中。 因為 hello IP 位址指派不同的 toohello HANA 大型執行個體單位不會傳送 hello （直接連線到其閘道 toohello 個執行個體） 的 Azure Vnet 之外，還有稍微變更 toohello 上面介紹的 VNet 設計：Azure VNet 閘道所能處理四個不同 MSEEs，從不同的 ExpressRoute 電路，而且是已連接的 tooone hello 大型執行個體戳記的每個 VNet 可以是另一個 Azure 區域中的連接的 toohello 大型執行個體戳記。

![Azure Vnet 連線中不同的 Azure 地區 tooAzure 大型執行個體戳記](./media/hana-overview-architecture/image8-multiple-regions.png)

如上圖 hello 如何 hello 不同 Azure Vnet 中區域是一種連線的 tootwo 不同的 ExpressRoute 電路位於兩個 Azure 區域使用的 tooconnect tooSAP HANA Azure （大型執行個體） 上。 新引入的 hello 連線是 hello 矩形紅線。 使用這些連接，超出 hello Azure Vnet，執行其中一個這些 Vnet 中的 hello Vm 可以存取每個 hello hello 兩個區域部署不同 HANA 大型執行個體單位。 您看到上述 hello 圖形中，它會假設您有兩個 ExpressRoute 連線，從內部部署 toohello 兩個 Azure 地區。基於災害復原考量，建議使用。

> [!IMPORTANT] 
> 如果使用多個 ExpressRoute 電路，AS 路徑前面加上和本機喜好設定 BGP 設定應該使用的 tooensure 適當的流量路由。


