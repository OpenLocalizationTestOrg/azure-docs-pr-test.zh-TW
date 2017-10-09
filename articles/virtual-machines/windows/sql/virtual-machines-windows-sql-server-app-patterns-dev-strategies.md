---
title: "在 Vm 上的伺服器應用程式模式 aaaSQL |Microsoft 文件"
description: "這篇文章涵蓋適用於 Azure VM 上的 SQL Server 應用程式模式。 它們可為解決方案架構師和開發人員提供基礎良好的應用程式架構和設計。"
services: virtual-machines-windows
documentationcenter: na
author: ninarn
manager: jhubbard
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 41863c8d-f3a3-4584-ad86-b95094365e05
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: ninarn
ms.openlocfilehash: e18597598fdf9fe534ed07331d6f531d4dca0601
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-patterns-and-development-strategies-for-sql-server-in-azure-virtual-machines"></a>Azure 虛擬機器中的 SQL Server 應用程式模式和開發策略
[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="summary"></a>摘要：
決定哪些應用程式模式或模式 toouse 您在 Azure 中 SQL Server 為基礎的應用程式的環境是重要的設計決策而且需要充分了解 SQL Server 和 Azure 的每一個基礎結構元件如何一起運作. 透過 Azure 基礎結構服務中的 SQL Server，您可以輕鬆地移轉、 維護及監視您的現有 SQL Server 應用程式建置在 Windows Server toovirtual 機器 Azure。

這篇文章的 hello 目標是 tooprovide 方案架構設計人員和良好的應用程式架構和設計，他們可以遵循移轉現有的應用程式 tooAzure 做為基礎的開發人員也為開發新的應用程式在 Azure 中。

針對每個應用程式模式中，您會發現在內部部署案例中，其分別具備雲端功能的方案，以及 hello 相關的技術建議。 此外，hello 篇文章會討論 Azure 特定開發策略，讓您可以正確地設計您的應用程式。 到期 toohello 許多可能的應用程式模式，建議架構設計人員和開發人員應該選擇 hello 最適合的模式，為其應用程式和使用者。

**技術參與者：** Luis Carlos Vargas Herring、Madhan Arumugam Ramakrishnan

**技術審稿人員：** Corey Sanders、Drew McDaniel、Narayan Annamalai、Nir Mashkowski、Sanjay Mishra、Silvano Coriani、Stefan Schackow、Tim Hickey、Tim Wieman、Xin Jin

## <a name="introduction"></a>簡介
您可以將 hello 元件在不同電腦上以及不同元件的 hello 不同的應用程式層級的分隔，開發許多類型的多層式架構應用程式。 例如，您可以在放置 hello 用戶端應用程式和商務規則元件中其中一部電腦、 前端 web 層和資料存取層元件，另一部電腦，並在另一部電腦中的後端資料庫層。 這種結構有助於分離各個層。 如果您變更資料來自何處，您不需要 toochange hello 用戶端或 web 應用程式，但只有 hello 資料存取層元件。

一般*多層式架構*hello 展示層、 hello 商業層和 hello 資料層應用程式包含了：

| 層 | 說明 |
| --- | --- |
| **展示** |hello*展示層*（web 層，前端層） 是使用者與應用程式的互動的 hello 圖層。 |
| **商務** |hello*商業層*（中介層） 是 hello 層該 hello 展示層和 hello 資料層使用 toocommunicate 彼此，並包含 hello 系統 hello 核心功能。 |
| **資料** |hello*資料層*基本上是儲存應用程式資料 （例如，執行 SQL Server 的伺服器） 的 hello 伺服器。 |

應用程式分層可說明 hello 的 hello 功能和元件的應用程式; 中的邏輯群組而層則說明 hello hello 功能和元件的實體分佈在不同的實體伺服器、 電腦、 網路或遠端位置上。 hello 應用程式分層可能位於 hello 相同實體電腦 (hello 同一層) 或可能分佈在不同的電腦 （多層式架構），和 hello 與透過妥善定義之介面的其他圖層中的元件通訊的每個圖層中的元件。 您可以將 hello 詞彙層做為參考 toophysical 分佈模式，例如兩層、 三層和多層式架構。 **2 層應用程式模式** 包含兩個應用程式層：應用程式伺服器和資料庫伺服器。 hello 互相直接聯繫 hello 應用程式伺服器和 hello 資料庫伺服器。 hello 應用程式伺服器包含 web 層和商業層元件。 在**3 層應用程式模式**，有三個應用程式層級： 網頁伺服器、 應用程式伺服器，其中包含 hello 的商務邏輯層和 （或） 商業層資料存取元件，與 hello 資料庫伺服器。 hello hello 網頁伺服器與 hello 資料庫伺服器之間的通訊發生在 hello 應用程式伺服器。 如需應用程式層和各層的詳細資訊，請參閱 [Microsoft 應用程式架構指南](https://msdn.microsoft.com/library/ff650706.aspx)。

在開始閱讀本文之前，您應了解的 SQL Server 和 Azure 的 hello 基本概念。 如需相關資訊，請參閱 [SQL Server 線上叢書](https://msdn.microsoft.com/library/bb545450.aspx)、[Azure 虛擬機器中的 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md) 以及 [Azure.com](https://azure.microsoft.com/)。

本文說明幾種可以是適用於您的簡單應用程式以及 hello 複雜度高的企業應用程式的應用程式模式。 之前詳述每個模式，我們建議，您應該熟悉 hello 可用的資料儲存體服務在 Azure 中，例如[Azure 儲存體](../../../storage/common/storage-introduction.md)， [Azure SQL Database](../../../sql-database/sql-database-technical-overview.md)，和[Azure 虛擬機器中的 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md)。 toomake hello 最佳設計決策，您的應用程式，了解何時 toouse 清楚服務的資料儲存體。

### <a name="choose-sql-server-in-an-azure-virtual-machine-when"></a>若有下列情況，請選擇使用 Azure 虛擬機器中的 SQL Server：
* 您需要控制 SQL Server 和 Windows。 比方說，這可能包括 SQL Server 版本的 hello、 特殊的 hotfix、 效能設定等。
* 您需要與 SQL Server 內部的完整相容性，且想要為 toomove 現有應用程式 tooAzure-是。
* 您想要的 hello Azure 環境 tooleverage hello 功能，但 Azure SQL Database 不支援應用程式所需的所有 hello 功能。 這可能包含下列區域的 hello:
  
  * **資料庫大小**： 次 hello 這篇文章更新時，SQL Database 支援資料庫總 too1 TB 的資料。 如果您的應用程式需要超過 1 TB 的資料，且您不想 tooimplement 自訂分區化解決方案，建議您使用 SQL Server 在 Azure 虛擬機器。 Hello 最新的資訊，請參閱[向外擴充 Azure SQL Database](https://msdn.microsoft.com/library/azure/dn495641.aspx)和[Azure SQL Database 服務層和效能層級](../../../sql-database/sql-database-service-tiers.md)。
  * **HIPAA 法規遵循**：醫療保健產業的客戶和獨立軟體廠商 (ISV) 可以選擇使用 [Azure 虛擬機器中 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md) 而不是 [Azure SQL Database](../../../sql-database/sql-database-technical-overview.md)，因為 HIPAA 業務合作協議 (BAA) 已涵蓋 Azure 虛擬機器中的 SQL Server。 如需法規遵循的資訊，請參閱 [Microsoft Azure 信任中心：法規遵循](https://azure.microsoft.com/support/trust-center/compliance/)。
  * **執行個體層級功能**： 在此階段中，SQL Database 不支援即時 hello 資料庫外部的功能 （例如連結的伺服器，代理程式作業，FileStream、 Service Broker 等。）。 如需詳細資訊，請參閱 [Azure SQL Database 方針和限制](https://msdn.microsoft.com/library/azure/ff394102.aspx)。

## <a name="1-tier-simple-single-virtual-machine"></a>1 層 (簡單)：單一虛擬機器
在應用程式模式中，您可以部署您的 SQL Server 應用程式和在 Azure 中資料庫 tooa 獨立虛擬機器。 hello 相同的虛擬機器包含用戶端 /web 應用程式、 商業元件、 資料存取分層和 hello 資料庫伺服器。 hello 簡報、 商務和資料存取程式碼會以邏輯方式分隔，但實際上位於單一伺服器電腦。 大部分的客戶開始使用此應用程式模式，然後，而向外擴充新增多個 web 角色或虛擬機器 tootheir 系統。

若有下列情況，此應用程式模式會很適用：

* 您想 tooperform 簡單的移轉 tooAzure 平台 tooevaluate hello 平台解答您的應用程式需求，或不。
* 您想要所有 hello 裝載的應用程式層的 tookeep 在 hello 相同虛擬機器在 hello 相同 Azure 資料中心各層之間 tooreduce hello 延遲。
* 您想 tooquickly 佈建開發和測試環境的短時間內。
* 您想 tooperform 壓力測試不同的工作負載層級，但在相同的時間，您不想 tooown 與維護許多實體機器 hello world hello。

hello 圖說明簡易內部部署案例及如何部署在 Azure 中的單一虛擬機器的雲端功能的方案。

![1 層應用程式模式](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728008.png)

部署 （商務邏輯和資料存取元件）： hello 商務圖層上 hello 同一個實體層 hello 展示層可以最大化應用程式效能，除非您必須使用不同的層，因為 tooscalability 或安全性的考量。

由於這是很常見的模式 toostart 使用時，您可能會發現下列移轉對移動您資料 tooyour SQL Server VM 上的文章 hello:[移轉資料庫 tooSQL Azure VM 上的 Server](virtual-machines-windows-migrate-sql.md)。

## <a name="3-tier-simple-multiple-virtual-machines"></a>3 層 (簡單)：多個虛擬機器
在此應用程式模式中，您會將每個應用程式層放在不同的虛擬機器中，以在 Azure 中部署 3 層應用程式。 這麼做可提供彈性的環境，以便輕鬆地向上和向外延展案例。 當一部虛擬機器包含您的用戶端 /web 應用程式時，另一個 hello 裝載您的商務元件和 hello 其他一個主機 hello 資料庫伺服器。

若有下列情況，此應用程式模式會很適用：

* 您想 tooperform 複雜的資料庫應用程式 tooAzure 虛擬機器的移轉。
* 您想要不同的應用程式層 toobe 裝載於不同的區域。 比方說，您可能會共用部署的 toomultiple 區域報表所需的資料庫。
* 您想要從內部 toomove 企業應用程式虛擬化平台 tooAzure 虛擬機器。 如需企業應用程式的詳細討論，請參閱 [企業應用程式是什麼](https://msdn.microsoft.com/library/aa267045.aspx)。
* 您想 tooquickly 佈建開發和測試環境的短時間內。
* 您想 tooperform 壓力測試不同的工作負載層級，但在相同的時間，您不想 tooown 與維護許多實體機器 hello world hello。

hello 圖示範如何將每個應用程式層放在不同的虛擬機器在 Azure 中將簡單的 3 層應用程式。

![3 層應用程式模式](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728009.png)

在此應用程式模式中，每一層只有一個虛擬機器 (VM)。 如果您在 Azure 中有多個 VM，我們建議您設定虛擬網路。 [Azure 虛擬網路](../../../virtual-network/virtual-networks-overview.md)建立受信任的安全性界限，並可允許透過 hello 私人 IP 位址的 Vm toocommunicate 本身。 此外，請務必確定所有的網際網路連線只會順著 toohello 展示層。 遵循此應用程式模式，當管理 hello 網路安全性群組規則 toocontrol 存取。 如需詳細資訊，請參閱[允許外部存取 tooyour VM 使用 hello Azure 入口網站](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

Hello 圖表中的網際網路通訊協定可以是 TCP、 UDP、 HTTP 或 HTTPS。

> [!NOTE]
> 在 Azure 中設定虛擬網路是免費的。 不過，您必須支付連接 tooon 內部部署的 hello VPN 閘道。 這筆費用根據 hello 連線會佈建和可用的時間量。
> 
> 

## <a name="2-tier-and-3-tier-with-presentation-tier-scale-out"></a>展示層向外延展的 2 層和 3 層
在應用程式模式中，您會將每個應用程式層放在不同的虛擬機器部署 2 層或 3 層資料庫應用程式 tooAzure 虛擬機器。 此外，您向外延展 hello 展示層，由於內送的用戶端要求的 tooincreased 數量。

若有下列情況，此應用程式模式會很適用：

* 您想要從內部 toomove 企業應用程式虛擬化平台 tooAzure 虛擬機器。
* 您想 tooscale 出 hello 展示層，由於內送的用戶端要求的 tooincreased 數量。
* 您想 tooquickly 佈建開發和測試環境的短時間內。
* 您想 tooperform 壓力測試不同的工作負載層級，但在相同的時間，您不想 tooown 與維護許多實體機器 hello world hello。
* 您想 tooown 可視需要向上和向下擴充的基礎結構環境。

hello 圖說明如何向外延展 hello 展示層，由於內送的用戶端要求的 tooincreased 數量在 Azure 中的多部虛擬機器放置 hello 應用程式層。 Hello 圖表所示，Azure 負載平衡器負責將流量分散到多部虛擬機器，也決定所至的 web 伺服器 tooconnect。 有多個負載平衡器後方的 hello 網頁伺服器執行個體，可確保 hello 的 hello 展示層的高可用性。

![應用程式模式 - 展示層向外延展](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728010.png)

### <a name="best-practices-for-2-tier-3-tier-or-n-tier-patterns-that-have-multiple-vms-in-one-tier"></a>一層內有多個 VM 之 2 層、3 層或多層式架構模式的最佳作法
建議您將屬於相同層中相同的雲端服務，並在 hello 相同的 hello toohello hello 虛擬機器 hello 可用性設定組。 例如，將一組 Web 伺服器放在 **CloudService1** 和 **AvailabilitySet1**，然後將一組資料庫伺服器放在 **CloudService2** 和 **AvailabilitySet2**。 在 Azure 中設定的可用性可讓您 tooplace hello 高可用性節點到不同的容錯網域和升級網域。

tooleverage 多個 VM 執行個體的層，您需要應用程式層之間 tooconfigure Azure 負載平衡器。 在每個層級，tooconfigure 負載平衡器負載平衡的端點在每一層 Vm 上分別建立。 對於特定一層，先建立 Vm 在 hello 相同雲端服務。 這可確保他們已擁有 hello 相同的公開虛擬 IP 位址。 接下來，在其中 hello 該層上的虛擬機器上建立端點。 然後，指派 hello 相同端點 toohello 進行負載平衡該層上的其他虛擬機器。 藉由建立一組負載平衡，您會將流量分散到多部虛擬機器，而且也允許 hello 負載平衡器 toodetermine 哪些節點 tooconnect 後, 端 VM 節點失敗時。 例如，負載平衡器後方的 hello 網頁伺服器的多個執行個體可確保 hello 的 hello 展示層的高可用性。

最佳做法，請務必確定所有的網際網路連線先前往 toohello 展示層。 hello 展示分層會存取 hello 商業層，然後再 hello 商業層存取 hello 資料層。 如需有關如何 tooallow 存取 toohello 展示層的詳細資訊，請參閱[允許外部存取 tooyour VM 使用 hello Azure 入口網站](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

請注意，hello Azure 中的負載平衡器在內部部署環境中運作類似 tooload 平衡器。 如需詳細資訊，請參閱 [Azure 基礎結構服務的負載平衡](../tutorial-load-balancer.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

此外，我們建議您使用 Azure 虛擬網路，為虛擬機器設定私人網路。 這可讓它們彼此之間的 toocommunicate 透過 hello 私人 IP 位址。 如需詳細資訊，請參閱 [Azure 虛擬網路](../../../virtual-network/virtual-networks-overview.md)。

## <a name="2-tier-and-3-tier-with-business-tier-scale-out"></a>商務層向外延展的 2 層和 3 層
在應用程式模式中，您會將每個應用程式層放在不同的虛擬機器部署 2 層或 3 層資料庫應用程式 tooAzure 虛擬機器。 此外，您可能想 toodistribute hello 應用程式伺服器元件 toomultiple 虛擬機器因為 toohello 應用程式的複雜度。

若有下列情況，此應用程式模式會很適用：

* 您想要從內部 toomove 企業應用程式虛擬化平台 tooAzure 虛擬機器。
* 您要 toodistribute hello 應用程式伺服器元件 toomultiple 虛擬機器因為 toohello 應用程式的複雜度。
* 您想 toomove 商務邏輯大量在內部部署 LOB （的營運） 應用程式 tooAzure 虛擬機器。 LOB 應用程式是一組重要 toorunning 企業中，例如會計、 人力資源 (HR)、 薪資、 供應鏈管理和資源規劃應用程式的重要電腦應用程式。
* 您想 tooquickly 佈建開發和測試環境的短時間內。
* 您想 tooperform 壓力測試不同的工作負載層級，但在相同的時間，您不想 tooown 與維護許多實體機器 hello world hello。
* 您想 tooown 可視需要向上和向下擴充的基礎結構環境。

下列圖表中的 hello 示範內部部署案例，以及其雲端功能的方案。 在此案例中，您會透過向外延展 hello 商業層，其中包含 hello 的商務邏輯層和資料存取元件放置在 Azure 中的多個虛擬機器中的 hello 應用程式層。 Hello 圖表所示，Azure 負載平衡器負責將流量分散到多部虛擬機器，也決定所至的 web 伺服器 tooconnect。 有多個負載平衡器後方的 hello 應用程式伺服器執行個體，可確保 hello 的 hello 商業層的高可用性。 如需詳細資訊，請參閱 [一層內有多個虛擬機器之 2 層、3 層或多層式架構模式的最佳作法](#best-practices-for-2-tier-3-tier-or-n-tier-patterns-that-have-multiple-vms-in-one-tier)。

![商務層向外延展的應用程式模式](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728011.png)

## <a name="2-tier-and-3-tier-with-presentation-and-business-tiers-scale-out-and-hadr"></a>展示層和商務層向外延展的 2 層和 3 層以及 HADR
在應用程式模式中，您在部署虛擬機器的 2 層或 3 層資料庫應用程式 tooAzure 分散 hello 展示層 （web 伺服器） 及 hello 商業層 （應用程式伺服器） 元件 toomultiple 虛擬機器。 此外，您會針對 Azure 虛擬機器中的資料庫，實作高可用性和災害復原解決方案。

若有下列情況，此應用程式模式會很適用：

* 您想要從虛擬化平台在內部部署 tooAzure toomove 企業應用程式實作 SQL Server 高可用性和災害復原功能。
* 您想 tooscale 出 hello 展示層和到期 tooincreased 磁碟區的內送的用戶端要求，以及應用程式的 hello 複雜度 hello 商業層。
* 您想 tooquickly 佈建開發和測試環境的短時間內。
* 您想 tooperform 壓力測試不同的工作負載層級，但在相同的時間，您不想 tooown 與維護許多實體機器 hello world hello。
* 您想 tooown 可視需要向上和向下擴充的基礎結構環境。

下列圖表中的 hello 示範內部部署案例，以及其雲端功能的方案。 在此案例中，您向外延展 hello 展示層和在 Azure 中的多個虛擬機器中的 hello 商業層元件。 此外，您會針對 Azure 中的 SQL Server 資料庫，實作高可用性和災害復原 (HADR) 技術。

請在不同的 VM 中執行應用程式的多個複本，確認可以負載平衡它們的要求。 當您有多個虛擬機器時，您會需要 toomake 確定您的 Vm 會存取且正在執行一個一點時間。 如果您設定負載平衡，Azure 負載平衡器追蹤 hello Vm 的健全狀況，並正確指示連入呼叫 toohello 狀況良好運作的 VM 節點。 如需詳細資訊 tooset 設定負載平衡的 hello 虛擬機器，請參閱[Azure 基礎結構服務部署的負載平衡](../tutorial-load-balancer.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 有多個 web 和應用程式負載平衡器後方的伺服器執行個體可確保 hello 高可用性的 hello 展示層和商業層。

![向外延展和高可用性](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728012.png)

### <a name="best-practices-for-application-patterns-requiring-sql-hadr"></a>需要 SQL HADR 之應用程式模式的最佳作法
當您在 Azure 虛擬機器中設定 SQL Server 高可用性和災害復原解決方案時，必須使用 [Azure 虛擬網路](../../../virtual-network/virtual-networks-overview.md) 為您的虛擬機器設定虛擬網路。  虛擬網路內的虛擬機器會有一個穩定的私人 IP 位址即使在服務停止運作，因此您可以避免 hello DNS 名稱解析所需的更新時間。 此外，hello 虛擬網路可讓您 tooextend 您內部網路 tooAzure 並建立信任的安全性界限。 例如，如果您的應用程式具有公司網域限制 (如 Windows 驗證、Active Directory)，則必須設定 [Azure 虛擬網路](../../../virtual-network/virtual-networks-overview.md) 。

大部分在 Azure 上執行實際程式碼的客戶，都會在 Azure 中保留主要和次要複本。

如需高可用性和災害復原技術的完整資訊及教學課程，請參閱 [Azure 虛擬機器中的 SQL Server 高可用性和嚴重損壞修復](virtual-machines-windows-sql-high-availability-dr.md)。

## <a name="2-tier-and-3-tier-using-azure-vms-and-cloud-services"></a>使用 Azure VM 和雲端服務的 2 層和 3 層
在應用程式模式中，您必須部署 tooAzure 2 層或 3 層應用程式同時使用[Azure 雲端服務](../../../cloud-services/cloud-services-choose-me.md#tellmecs)（web 和背景工作角色-平台即服務 (PaaS)） 和[Azure 虛擬機器](../overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)(基礎結構即服務 (IaaS)）。 使用[Azure 雲端服務](https://azure.microsoft.com/documentation/services/cloud-services/)hello 展示層/商業層和中的 SQL Server [Azure 虛擬機器](../overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)hello 資料層會有幫助，大部分的應用程式在 Azure 上執行。 hello 原因是，雲端服務上執行的計算執行個體，可提供便於管理、 部署、 監視和向外延展。

與雲端服務 Azure 會為您維護 hello 基礎結構、 執行例行維護、 修補程式 hello 的作業系統，而且嘗試 toorecover 從服務和硬體失敗。 當您的應用程式需要向外延展時，自動和手動向外延展選項可供雲端服務專案藉由增加或減少 hello 或您的應用程式所使用的虛擬機器執行個體數目。 此外，您可以使用內部部署 Visual Studio toodeploy 應用程式 tooa 雲端服務專案在 Azure 中。

總而言之，如果您不要 hello 展示/商業層 tooown 廣泛的管理工作，而且您的應用程式不需要任何複雜的軟體或 hello 作業系統設定，使用 Azure 雲端服務。 如果 Azure SQL Database 不支援您所需的所有 hello 功能，使用 SQL Server 在 Azure 虛擬機器中的 hello 資料層。 Azure 雲端服務上執行應用程式，並將資料儲存在 Azure 虛擬機器會結合這兩項服務的 hello 優點。 詳細的比較，請參閱本主題中的 hello 一節，在[比較在 Azure 中的開發策略](#comparing-web-development-strategies-in-azure)。

在此應用程式模式，hello 展示層包含 web 角色，這在 hello Azure 執行環境中執行的雲端服務元件，它會在 IIS 和 ASP.NET 支援之 web 應用程式設計為自訂。 hello 商業或後端層包含背景工作角色，這 hello Azure 執行環境中執行的雲端服務元件，並適用於一般開發，及可為 web 角色執行背景處理。 hello 資料庫層位於 Azure 中的 SQL Server 虛擬機器。 hello hello 展示層與 hello 資料庫層之間的通訊會發生直接或透過 hello 商業層 – 背景工作角色元件。

若有下列情況，此應用程式模式會很適用：

* 您想要從虛擬化平台在內部部署 tooAzure toomove 企業應用程式實作 SQL Server 高可用性和災害復原功能。
* 您想 tooown 可視需要向上和向下擴充的基礎結構環境。
* Azure SQL Database 不支援您的應用程式或資料庫所需的所有 hello 功能。
* 您想 tooperform 壓力測試不同的工作負載層級，但在相同的時間，您不想 tooown 與維護許多實體機器 hello world hello。

下列圖表中的 hello 示範內部部署案例，以及其雲端功能的方案。 在此案例中，您將放在 web 角色中的 hello 展示層時，背景工作角色中的 hello 商業層，但在 Azure 中的虛擬機器中的 hello 資料層。 這些可在不同的 web 角色中執行多份 hello 展示層確保 tooload 平衡要求。 當您將「Azure 雲端服務」與「Azure 虛擬機器」結合時，建議您一併設定 [Azure 虛擬網路](../../../virtual-network/virtual-networks-overview.md) 。 與[Azure 虛擬網路](../../../virtual-network/virtual-networks-overview.md)，您可以擁有穩定，而且持續性私人 IP 位址相同雲端服務中的 hello 內 hello 雲端。 一旦您定義虛擬網路的虛擬機器和雲端服務時，他們可以啟動透過 hello 私人 IP 位址相互聯繫。 此外，具有虛擬機器和 Azure web/背景工作角色在 hello 相同[Azure 虛擬網路](../../../virtual-network/virtual-networks-overview.md)提供低延遲、 更安全的連接。 如需詳細資訊，請參閱 [什麼是雲端服務](../../../cloud-services/cloud-services-choose-me.md)。

Hello 圖表所示，Azure 負載平衡器將流量分散到多部虛擬機器，並決定哪個 web 伺服器或應用程式伺服器至 tooconnect。 有多個負載平衡器後方的 hello web 和應用程式伺服器執行個體，可確保 hello 的 hello 展示層和 hello 商業層的高可用性。 如需詳細資訊，請參閱 [需要 SQL HADR 之應用程式模式的最佳作法](#best-practices-for-application-patterns-requiring-sql-hadr)。

![應用程式模式搭配雲端服務](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728013.png)

此應用程式模式是 toouse hello 下列所示，包含展示層和商業層元件的整合式的 web 角色的另一個方法 tooimplement 圖表。 如果應用程式需要可設定狀態的設計，此應用程式模式就很實用。 由於 Azure web 和背景工作角色提供無狀態的計算節點，建議您實作使用其中一種下列技術的 hello 邏輯 toostore 工作階段狀態： [Azure 快取](https://azure.microsoft.com/documentation/services/redis-cache/)， [Azure 資料表儲存體](../../../cosmos-db/table-storage-how-to-use-dotnet.md)或[Azure SQL Database](../../../sql-database/sql-database-technical-overview.md)。

![應用程式模式搭配雲端服務](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728014.png)

## <a name="pattern-with-azure-vms-azure-sql-database-and-azure-app-service-web-apps"></a>Azure VM、Azure SQL Database 和 Azure App Service (Web Apps) 的模式
此應用程式模式 hello 主要目標是 tooshow 您如何 toocombine Azure 基礎結構即服務 (IaaS) 元件與 (Azure 平台做為服務 PaaS) 元件在方案中。 此模式著重於關聯式資料存放區的 Azure SQL Database。 它不包含 SQL Server 在 Azure 的虛擬機器，這是 hello Azure 基礎結構即服務所提供的部分。

在應用程式模式中，您部署資料庫應用程式 tooAzure 放入 hello 簡報和商務層中的 hello 相同的虛擬機器和存取 Azure SQL Database (SQL Database) 伺服器中的資料庫。 您可以使用傳統的 IIS 型 web 方案，以實作 hello 展示層。 或者，您可以使用 [Azure Web Apps](https://azure.microsoft.com/documentation/services/app-service/web/)，實作結合的展示層和商業層。

若有下列情況，此應用程式模式會很適用：

* 您已經在 Azure 中設定現有的 SQL 資料庫伺服器，您希望 tootest 應用程式快速。
* 您想 tootest Azure 環境的 hello 功能。
* 您想 tooquickly 佈建開發和測試環境的短時間內。
* 您的商務邏輯和資料存取元件可以獨立在 Web 應用程式內。

下列圖表中的 hello 示範內部部署案例，以及其雲端功能的方案。 在此案例中，您要放置在單一虛擬機器 Azure 及存取資料，在 Azure SQL Database 中的 hello 應用程式層。

![混合應用程式模式](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728015.png)

如果您選擇 tooimplement 結合的 web 和應用程式層使用 Azure Web 應用程式，我們建議您讓 hello 中介層或應用程式層保持為 hello 內容 web 應用程式中的動態連結程式庫 (Dll)。

此外，檢閱 在 hello hello 建議[比較在 Azure 中的 web 開發策略](#comparing-web-development-strategies-in-azure)hello 這個深入了解程式設計技術的文章 toolearn 結尾 > 一節。

## <a name="n-tier-hybrid-application-pattern"></a>多層式架構混合式應用程式模式
在多層式架構混合式應用程式模式中，您會在分散於內部部署和 Azure 間的多個層中，實作應用程式。 因此，您建立的彈性和可重複使用的混合式系統，您可以修改或新增特定一層而不需要變更 hello 其他層。 tooextend 公司網路 toohello 雲端，您使用[Azure 虛擬網路](../../../virtual-network/virtual-networks-overview.md)服務。

若有下列情況，此混合式應用程式模式會很適用：

* 要執行 hello 雲端中的部分，部分在內部 toobuild 應用程式。
* 您想 toomigrate 的現有內部部署應用程式 toohello 雲端的部分或所有項目。
* 您想要從內部部署虛擬化平台 tooAzure toomove 企業應用程式。
* 您想 tooown 可視需要向上和向下擴充的基礎結構環境。
* 您想 tooquickly 佈建開發和測試環境的短時間內。
* 要符合成本效益的方式 tootake 備份企業資料庫應用程式。

下列圖表中的 hello 示範跨越內部部署和 Azure 的多層式架構混合應用程式模式。 Hello 圖表所示，在內部部署基礎結構包含[Active Directory 網域服務](https://technet.microsoft.com/library/hh831484.aspx)網域控制站 toosupport 使用者驗證與授權。 請注意該 hello 圖表示範的案例，hello 資料層的某些部分居住在內部部署資料中心而存在於 Azure 的 hello 資料層的某些部分。 您可以根據應用程式的需求，實作數個其他混合式案例。 比方說，您可能會在內部部署環境，但 hello 資料層放在 Azure 中保留 hello 展示層和 hello 商務層。

![多層式架構的應用程式模式](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728016.png)

在 Azure 中，您可以使用 Active Directory 做為貴組織的獨立雲端目錄，或者您也可以將現有的內部部署 Active Directory 與 [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)整合。 Hello 圖表所示，hello 商業層元件可以存取 toomultiple 資料來源，例如太[在 Azure 中的 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md)透過私人內部 IP 位址，透過 tooon 內部部署 SQL Server [Azure虛擬網路](../../../virtual-network/virtual-networks-overview.md)，或太[SQL Database](../../../sql-database/sql-database-technical-overview.md)使用 hello.NET Framework 資料提供者技術。 在此圖中，Azure SQL Database 是選用的資料儲存體服務。

在多層式架構混合應用程式模式中，您可以實作下列工作流程中指定的 hello 順序的 hello:

1. 識別企業資料庫應用程式需要使用 hello 移 toocloud toobe [Microsoft Assessment and Planning (MAP) Toolkit](http://microsoft.com/map)。 hello MAP Toolkit 從您考慮虛擬化的電腦收集清查和效能資料，並提供容量和評估規劃的建議。
2. 規劃 hello 資源，並且在 hello Azure 平台，例如儲存體帳戶和虛擬機器所需的設定。
3. 設定 hello 公司網路內部部署之間的網路連線和[Azure 虛擬網路](../../../virtual-network/virtual-networks-overview.md)。 tooset hello hello 公司網路內部部署與 Azure 中虛擬機器之間的連線使用下列兩種方法的 hello 的其中一個：
   
   1. 透過 Azure 虛擬機器上的公用端點，建立內部部署與 Azure 之間的連線。 這個方法會提供簡單設定，並讓您 toouse 虛擬機器中的 SQL Server 驗證。 此外，設定您網路安全性群組規則 toocontrol 公用流量 toohello VM。 如需詳細資訊，請參閱[允許外部存取 tooyour VM 使用 hello Azure 入口網站](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
   2. 透過 Azure 虛擬私人網路 (VPN) 通道，在內部部署與 Azure 之間建立連線。 這個方法可讓您 tooextend 網域原則 tooa 虛擬機器在 Azure 中。 此外，您可以設定防火牆規則，並在虛擬機器中使用 Windows 驗證。 Azure 目前支援安全的網站間 VPN 和點對站 VPN 連線：
      
      * 您可以透過安全的網站間連線，在內部部署網路與 Azure 虛擬網路之間建立網路連線。 建議您連接內部部署資料中心環境 tooAzure。
      * 您可以透過安全的點對站連線，在 Azure 虛擬網路與在任何一處執行的電腦之間，建立網路連線。 此方法多半建議用於開發和測試。
      
      如需詳細資訊 tooconnect tooSQL 伺服器在 Azure 中，請參閱[連接 tooa 在 Azure 上的 SQL Server 虛擬機器](virtual-machines-windows-sql-connect.md)。
4. 設定排定的工作和警示，以在 Azure 的虛擬機器磁碟中備份內部部署資料。 如需詳細資訊，請參閱 [SQL Server 備份及還原與 Azure Blob 儲存體服務](https://msdn.microsoft.com/library/jj919148.aspx)和 [Azure 虛擬機器中的 SQL Server 備份和還原](virtual-machines-windows-sql-backup-recovery.md)。
5. 根據您的應用程式的需求，您可以實作一個 hello 下列三種常見案例：
   
   1. 您可以將您的網頁伺服器、 應用程式伺服器和不區分大小寫的資料在 Azure 中的資料庫伺服器而保留 hello 機密資料的內部。
   2. 您可以將您的 web 伺服器和應用程式伺服器內部而在 Azure 中的虛擬機器中的 hello 資料庫伺服器。
   3. 您可以將您的資料庫伺服器、 網頁伺服器和應用程式伺服器內部而 hello 資料庫複本保持在 Azure 虛擬機器。 此設定可讓 hello 內部 web 伺服器或報表的應用程式 tooaccess hello Azure 中的資料庫複本。 因此，您也可以達到 toolower hello 工作負載，在內部部署資料庫中。 我們建議您針對讀取密集的工作負載和開發用途，實作此案例。 如需在 Azure 中建立資料庫複本的資訊，請參閱 [Azure 虛擬機器中的 SQL Server 高可用性和災害復原](virtual-machines-windows-sql-high-availability-dr.md)中的「AlwaysOn 可用性群組」。

## <a name="comparing-web-development-strategies-in-azure"></a>比較 Azure 中的 Web 開發策略
tooimplement 和部署多層式 SQL Server 為基礎的應用程式在 Azure 中，您可以使用下列兩種程式設計方法 hello 的其中一個：

* 在 Azure 中設定傳統 Web 伺服器 (IIS - 網際網路資訊服務)，並存取位於 Azure 虛擬機器中 SQL Server 內的資料庫。
* 實作和部署雲端服務 tooAzure。 然後請確定此雲端服務可以存取 Azure 虛擬機器中 SQL Server 內的資料庫。 雲端服務可以包含多個 Web 角色和背景工作角色。

hello 下表提供傳統 web 開發與 Azure 雲端服務和 Azure Web 應用程式與尊重 tooSQL 伺服器在 Azure 虛擬機器的比較。 hello 資料表包含 Azure Web 應用程式，因為它是可能 toouse Azure VM 中 SQL Server 做為 Azure Web 應用程式的資料來源透過其公用虛擬 IP 位址或 DNS 名稱。

|  | Azure 虛擬機器中的傳統 Web 開發 | Azure 中的雲端服務 | 虛擬主機與 Azure Web Apps |
| --- | --- | --- | --- |
| **從內部部署進行應用程式移轉** |現有的應用程式維持不變。 |應用程式需要 Web 角色和背景工作角色。 |現有的應用程式維持不變，但仍適用於需要快速擴充的獨立式 Web 應用程式和 Web 服務。 |
| **開發和部署** |Visual Studio、WebMatrix、Visual Web Developer、WebDeploy、FTP、TFS、IIS Manager，PowerShell。 |Visual Studio、Azure SDK、TFS，PowerShell。 每個雲端服務都有兩個您可以部署您的服務封裝和組態的環境 toowhich： 預備和生產環境。 您可以部署雲端服務 toohello 暫存環境 tootest 前 tooproduction 升級。 |Visual Studio、WebMatrix、Visual Web Developer、FTP、GIT、BitBucket、CodePlex、DropBox、GitHub、Mercurial、TFS、Web Deploy、PowerShell。 |
| **系統管理和設定** |您必須負責 hello 應用程式、 資料、 防火牆規則、 虛擬網路，以及作業系統上的系統管理工作。 |您必須負責 hello 應用程式、 資料、 防火牆規則，以及虛擬網路上的系統管理工作。 |您必須負責 hello 應用程式和僅限資料上的系統管理工作。 |
| **高可用性和災害復原 (HADR)** |我們建議您將虛擬機器放在同一個可用性設定，並在 hello 相同的 hello 雲端服務。 將 Vm 放 hello 相同可用性設定組可讓 Azure tooplace hello 高可用性節點不同的容錯網域和升級網域。 同樣地，將 Vm 放在 hello 相同雲端服務可啟用負載平衡，Vm 可以透過 hello Azure 資料中心內的本機網路直接與彼此通訊。<br/><br/>您必須負責實作高可用性和災害復原方案的 SQL Server 在 Azure 虛擬機器 tooavoid 任何停機時間。 如需支援的 HADR 技術，請參閱 [Azure 虛擬機器中的 SQL Server 高可用性和災害復原](virtual-machines-windows-sql-high-availability-dr.md)。<br/><br/>您需負責備份自己的資料和應用程式。<br/><br/>Azure 可以移動虛擬機器，如果 hello hello 資料中心內的主機電腦因為 toohardware 問題而失敗。 此外，有可能是您 VM 的計劃的停機 hello 主機電腦的安全性或軟體更新時的更新。 因此，我們建議您在每個應用程式層級 tooensure hello 連續可用性維護兩個以上的 Vm。 Azure 沒有為單一虛擬機器提供 SLA。 如需詳細資訊，請參閱 [Azure 復原技術指導](../../../resiliency/resiliency-technical-guidance.md)。 |Azure 管理 hello hello 基礎硬體或作業系統軟體造成的失敗。 我們建議您實作多個 web 或背景工作角色 tooensure hello 高可用性應用程式的執行個體。 如需資訊，請參閱[雲端服務、虛擬機器和虛擬網路服務等級協定](http://www.microsoft.com/download/details.aspx?id=38427)和 [Azure 應用程式的災害復原及高可用性](../../../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)<br/><br/>您需負責備份自己的資料和應用程式。<br/><br/>對於位於 Azure VM 中 SQL Server 資料庫的資料庫，您必須負責實作高可用性和災害復原方案 tooavoid 任何停機時間項目。 如需支援的 HDAR 技術，請參閱 Azure 虛擬機器中的 SQL Server 高可用性和災害復原。<br/><br/>**SQL Server 資料庫鏡像**：與 Azure 雲端服務 (web/背景工作角色) 搭配使用。 SQL Server Vm 和雲端服務專案可以是在 hello 相同 Azure 虛擬網路。 如果 SQL Server VM 不在 hello 相同虛擬網路，您需要 toocreate SQL Server 的 SQL Server 別名 tooroute 通訊 toohello 執行個體。 此外，hello 別名名稱必須符合 hello SQL Server 名稱。 |高可用性是繼承自 Azure 背景工作角色、Azure Blob 儲存體和 Azure SQL Database。 例如，Azure 儲存體會維護所有 Blob、資料表和佇列資料的三個複本。 不論何時，Azure SQL Database 都會保留三個執行中的資料複本—一個主要複本和兩個次要複本。 如需詳細資訊，請參閱 [Azure 儲存體](https://azure.microsoft.com/documentation/services/storage/) 和 [Azure SQL Database](../../../sql-database/sql-database-technical-overview.md)。<br/><br/>使用 Azure VM 中的 SQL Server 當做 Azure Web Apps 的資料來源時，請記住，Azure Web Apps 不支援 Azure 虛擬網路。 換句話說，所有從 Azure Web Apps tooSQL Server Vm 在 Azure 中的連接必須通過虛擬機器的公用端點。 這可能會對高可用性和災害復原案例造成一些限制。 例如，hello Azure Web 應用程式使用資料庫鏡像連接 tooSQL Server VM 上的用戶端應用程式不會無法 tooconnect toohello 新的主要伺服器為資料庫鏡像會要求您設定 Azure 虛擬網路中的 SQL Server 主機 Vm 之間Azure。 因此，目前不支援 **SQL Server 資料庫鏡像**與 Azure Web 應用程式搭配使用。<br/><br/>**SQL Server AlwaysOn 可用性群組**︰當使用 Azure 中的 SQL Server VM 搭配 Azure Web 應用程式時，您可以設定 AlwaysOn 可用性群組。 但是，您需要 tooconfigure AlwaysOn 可用性群組接聽程式 tooroute hello 通訊 toohello 主要複本透過公用負載平衡的端點。 |
| **跨單位連線** |您可以使用 Azure 虛擬網路 tooconnect tooon 內部。 |您可以使用 Azure 虛擬網路 tooconnect tooon 內部。 |支援 Azure 虛擬網路。 如需詳細資訊，請參閱 [Web Apps Virtual Network Integration (Web Apps 虛擬網路整合)](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/)。 |
| **延展性** |向上延展，請增加 hello 虛擬機器大小，或新增更多磁碟。 如需關於虛擬機器大小的詳細資訊，請參閱 [Azure 的虛擬機器大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。<br/><br/>**資料庫伺服器**︰向外延展可透過資料庫資料分割技術和 SQL Server AlwaysOn 可用性群組提供。<br/><br/>對於大量讀取工作負載，您可以在多個次要節點以及 SQL Server 複寫上使用 [AlwaysOn 可用性群組](https://msdn.microsoft.com/library/hh510230.aspx)。<br/><br/>針對大量寫入的工作負載，您可以跨多個實體伺服器 tooprovide 應用程式向外延展實作水平資料分割。<br/><br/>此外，您可以使用 [SQL Server 與資料相依路由](https://technet.microsoft.com/library/cc966448.aspx)來實作向外延展。 使用資料依存路由 (DDR)，您需要資料分割機制 hello 用戶端應用程式，通常是在商業層 hello tooimplement hello、 tooroute hello 資料庫要求已超過 toomultiple SQL Server 節點。 hello 商業層包含對應 toohow hello 資料分割和哪個節點包含 hello 資料。<br/><br/>您可以為執行虛擬機器的應用程式調整規模。 如需詳細資訊，請參閱[如何 tooScale 應用程式](../../../cloud-services/cloud-services-how-to-scale.md)。<br/><br/>**重要事項**: hello**自動調整規模**在 Azure 中的功能可讓您 tooautomatically 增加或減少 hello 您的應用程式所使用的虛擬機器。 這項功能可保證在尖峰期間，不影響 hello 使用者體驗造成負面，Vm 會關閉 hello 需求很低。 建議您確認您未設定 hello 自動調整規模選項為您的雲端服務包括 SQL Server Vm。 hello 原因是該 hello 自動調整 」 功能可讓虛擬機器上的 Azure tooturn hello 在該 VM 的 CPU 使用率高於時某些臨界值，並關閉虛擬機器 tooturn hello CPU 使用量低於時。 hello 自動調整 」 功能可用於無狀態應用程式，例如 web 伺服器，其中任何 VM 都可以管理 hello 工作負載不含任何參考 tooany 先前的狀態。 不過，不是適用於可設定狀態的應用程式，例如 SQL Server，其中只允許一個執行個體寫入 toohello 資料庫 hello 自動調整 」 功能。 |透過使用多個 Web 角色和背景工作角色來相應增加。 如需 Web 角色和背景工作角色之虛擬機器大小的詳細資訊，請參閱[設定雲端服務的大小](../../../cloud-services/cloud-services-sizes-specs.md)。<br/><br/>當使用**雲端服務**，您可以定義多個角色 toodistribute 處理及得以彈性調整您的應用程式。 每個雲端服務包含一或多個 Web 角色和/或背景工作角色，且各有自己的應用程式檔案和組態。 您可以向上延展的雲端服務藉由增加為某個角色部署的 hello 角色執行個體 （虛擬機器） 數目和向下調整雲端服務藉由降低 hello 角色執行個體數目。 如需詳細資訊，請參閱 [Azure 執行模型](../../../cloud-services/cloud-services-choose-me.md)。<br/><br/>向外延展可透過[雲端服務、虛擬機器和虛擬網路服務等級協定](http://www.microsoft.com/download/details.aspx?id=38427)和負載平衡器，透過內建的 Azure 高可用性支援提供使用。<br/><br/>多層式應用程式中，我們建議您連接 web/背景工作角色應用程式 toodatabase 伺服器透過 Azure 虛擬網路的 Vm。 此外，Azure 提供的負載平衡的 Vm 中 hello 相同雲端服務，在它們之間分配使用者要求。 以這種方式連接的虛擬機器可以彼此直接透過 Azure 資料中心內的 hello 本機網路。<br/><br/>您可以設定**自動調整規模**hello Azure 入口網站，以及 hello 排程時間。 如需詳細資訊，請參閱[tooconfigure 自動調整 hello 入口網站中的雲端服務如何](../../../cloud-services/cloud-services-how-to-scale-portal.md)。 |**向上和向下調整**： 您可以增加/減少 hello hello 執行個體 (VM) 為您的網站保留的大小。<br/><br/>相應放大︰您可以為您的網站新增更多保留的執行個體 (VM)。<br/><br/>您可以設定**自動調整規模**hello 入口網站，以及 hello 排程時間。 如需詳細資訊，請參閱[如何 tooScale Web 應用程式](../../../app-service-web/web-sites-scale.md)。 |

如需如何選擇這些程式設計方法的詳細資訊，請參閱[Azure Web 應用程式、 雲端服務和 Vm： 當 toouse 其中](../../../app-service-web/choose-web-site-cloud-service-vm.md)。

## <a name="next-steps"></a>後續步驟
如需在 Azure 虛擬機器中執行 SQL Server 的詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](virtual-machines-windows-sql-server-iaas-overview.md)。

