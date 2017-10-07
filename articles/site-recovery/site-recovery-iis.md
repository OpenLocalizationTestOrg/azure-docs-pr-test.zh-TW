---
title: "aaaReplicate 多層式 IIS 型 web 應用程式使用 Azure Site Recovery |Microsoft 文件"
description: "本文說明如何 tooreplicate IIS web 伺服陣列使用 Azure Site Recovery 的虛擬機器。"
services: site-recovery
documentationcenter: 
author: nsoneji
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: nisoneji
ms.openlocfilehash: 1974265b3cb05f6dc57049876306d2e08424bb97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-iis-based-web-application-using-azure-site-recovery"></a>使用 Azure Site Recovery 複寫多層式 IIS 型 web 應用程式

## <a name="overview"></a>概觀


應用程式軟體是在組織中的商務產能的 hello 引擎。 各種 web 應用程式可在組織提供不同的用途。 這些其中一部分，例如處理薪資、財務應用程式和客戶面向的網站可能對組織是最重要的。 它對於 hello 組織 toohave 向上以及在任何時候 tooprevent 降低產能執行重要而且更重要的是防止 hello 組織的任何損害 toohello 品牌映像。

重要的 web 應用程式通常是做為 hello web、 資料庫與應用程式在不同的層上的多層式應用程式設定。 除了會分散在各層，hello 應用程式也可以使用多部伺服器中每個層 tooload hello 流量平衡。 此外，hello hello 網頁伺服器與各層之間的對應可能會根據靜態 IP 位址。 在容錯移轉時，部分對應必須 toobe 更新，特別是，當您擁有 hello web 伺服器上設定的多個網站。 如果使用 SSL 的 web 應用程式，需要 toobe 更新憑證繫結。

傳統的非複寫根據的修復方法牽涉到不同的設定檔、 登錄設定、 繫結、 自訂元件 （COM 或.NET）、 內容和也憑證和復原 hello 檔案透過手動步驟一組的備份。 這些技術顯然都很麻煩，很容易出錯且不可調整。 它是，例如，輕鬆地讓您 tooforget 備份憑證而且沒有選項但 toobuy hello 伺服器的新憑證在容錯移轉之後。

理想的災害復原解決方案，應該上方複雜的應用程式架構允許 hello 周圍的復原方案的模型，而且也具有 hello 能力 tooadd 自訂步驟 toohandle 應用程式之間的對應因此提供的各層單鍵確定 hello 開頭 tooa 災害事件中擷取畫面方案降低 RTO。


本文說明如何 tooprotect IIS 型 web 應用程式使用[Azure Site Recovery](site-recovery-overview.md)。 IIS 型 web 應用程式 tooAzure、 告訴您如何進行災害復原訓練，和如何容錯移轉 hello 應用程式 tooAzure，本文將討論複寫三層的最佳作法。


## <a name="prerequisites"></a>必要條件

開始之前，請確定您了解 hello 下列：

1. [複寫虛擬機器 tooAzure](site-recovery-vmware-to-azure.md)
1. 如何太[設計與復原網路](site-recovery-network-design.md)
1. [執行測試容錯移轉 tooAzure](./site-recovery-test-failover-to-azure.md)
1. [執行容錯移轉 tooAzure](site-recovery-failover.md)
1. 如何太[複寫的網域控制站](site-recovery-active-directory.md)
1. 如何太[複寫 SQL Server](site-recovery-sql.md)

## <a name="deployment-patterns"></a>部署模式
為基礎的 IIS web 應用程式通常會遵循 hello 下列部署模式的其中一個：

**部署模式 1 ** 具有應用程式要求路由 (ARR)、IIS 伺服器與 Microsoft SQL Server 的 IIS 型 web 伺服陣列。

![部署模式](./media/site-recovery-iis/deployment-pattern1.png)

**部署模式 2** 具有應用程式要求路由 (ARR)、IIS 伺服器、應用程式伺服器與 Microsoft SQL Server 的 IIS 型 web 伺服陣列。


![部署模式](./media/site-recovery-iis/deployment-pattern2.png)

## <a name="site-recovery-support"></a>Site Recovery 支援

Hello 目的是要使用 IIS 伺服器上 Windows Server 2012 R2 Enterprise 版本 7.5 建立此發行項的 VMware 虛擬機器所使用。 站台復原複寫與應用程式無關，hello 建議提供以下是預期的 toohold 在下列的情況下，不同版本的 IIS。

### <a name="source-and-target"></a>來源與目標

**案例** | **tooa 次要站台** | **tooAzure**
--- | --- | ---
**Hyper-V** | 是 | 是
**VMware** | 是 | 是
**實體伺服器** | 否 | 是

## <a name="replicate-virtual-machines"></a>複寫虛擬機器

請遵循[本指南](site-recovery-vmware-to-azure.md)toostart 複寫所有 hello IIS web 伺服陣列的虛擬機器 tooAzure。

如果您使用靜態 ip 位址，則指定您想 hello hello 中的虛擬機器 tootake hello IP [**目標 IP** ](./site-recovery-replicate-vmware-to-azure.md#view-and-manage-vm-properties)運算和網路設定中設定。

![目標 IP](./media/site-recovery-active-directory/dns-target-ip.png)


## <a name="creating-a-recovery-plan"></a>建立復原計劃

復原計劃可讓您排序 hello 容錯移轉維護應用程式一致性是多層式應用程式，因此，在各層。 建立多層式 web 應用程式的復原計劃時，請遵循下面的步驟 hello。  [深入了解如何建立復原計劃](./site-recovery-create-recovery-plans.md)。

### <a name="adding-virtual-machines-toofailover-groups"></a>新增虛擬機器 toofailover 群組
SQL 虛擬機器、 hello constituted IIS 伺服器的 web 層和應用程式層的資料庫層將會包含一般的多層式 IIS web 應用程式。 所有這些虛擬機器 toodifferent 基礎加入群組層做為下面。 [深入了解自訂復原方案](site-recovery-runbook-automation.md#customize-the-recovery-plan)。

1. 建立復原計畫。 新增群組 1 tooensure 它們最後會關機並帶出第一個下 hello 資料庫在階層虛擬機器。

1. 它們會帶出 hello 資料庫層啟動之後，請加入 hello 應用程式層群組 2 底下的虛擬機器。

1. 新增群組 3 hello web 層的虛擬機器，使得 hello 應用程式層啟動之後，它們會帶出。

1. 使 hello web 層啟動之後，它們會帶出，群組 4 中新增虛擬機器負載平衡。


### <a name="adding-scripts-toohello-recovery-plan"></a>加入指令碼 toohello 復原計劃
您可能需要 toodo hello Azure 虛擬機器後測試容錯移轉/容錯移轉 toomake IIS web 伺服陣列函式的某些作業正確。 您可以自動化 hello post 容錯移轉作業，例如更新 DNS 項目，變更 網站繫結、 變更連接字串中加入對應的指令碼，如下所示的 hello 復原方案中。 [深入了解新增指令碼復原計劃](./site-recovery-create-recovery-plans.md#add-scripts)。

#### <a name="dns-update"></a>DNS 更新
如果 hello DNS 針對動態 DNS 更新設定，然後虛擬機器通常更新 hello DNS hello 新 IP 之後啟動。 如果您想 tooadd 以 hello 明確步驟 tooupdate DNS 新 hello 虛擬機器的 Ip 再新增這[指令碼在 DNS 中的 tooupdate IP](https://aka.ms/asr-dns-update)作為復原計畫群組後動作。  

#### <a name="connection-string-in-an-applications-webconfig"></a>在應用程式 web.config 中的連接字串
hello 連接字串會指定與 hello 網站的 hello 資料庫通訊。

如果 hello 連接字串會帶來 hello hello 資料庫虛擬機器名稱，再執行任何步驟將會容錯移轉所需的後，hello 應用程式將無法 tooautomatically 通訊 toohello DB。 此外，如果 hello hello 資料庫虛擬機器的 IP 位址會保留下來，它不會需要 tooupdate hello 連接字串。 如果 hello 連接字串是指 toohello 資料庫虛擬機器使用的 IP 位址，它將需要容錯移轉後 toobe 更新。 例如 下列連接字串 hello 點 toohello ip 127.0.1.2 DB

        <?xml version="1.0" encoding="utf-8"?>
        <configuration>
        <connectionStrings>
        <add name="ConnStringDb1" connectionString="Data Source= 127.0.1.2\SqlExpress; Initial Catalog=TestDB1;Integrated Security=False;" />
        </connectionStrings>
        </configuration>

您可以藉由新增更新 hello 連接字串中的 web 層[IIS 連接更新指令碼](https://aka.ms/asr-update-webtier-script-classic)hello 復原計劃中的群組 3 之後。

#### <a name="site-bindings-for-hello-application"></a>Hello 應用程式的站台繫結
每個站台繫結資訊，包括 hello 繫結型別、 hello 的 hello IIS 伺服器接聽 toohello 要求 hello 站台、 hello 連接埠號碼 hello hello 網站的主機名稱的 IP 位址所組成。 在容錯移轉的 hello 階段，這些繫結可能需要 toobe 更新 hello 與其相關聯的 IP 位址變更時。

> [!NOTE]
>
> 如果您已標記為 'all unassigned' hello 站台繫結，如下列的 hello 範例所示，您將不需要 tooupdate 此繫結 post 容錯移轉。 此外，如果 hello 與網站相關聯的 IP 位址不會變更 post 容錯移轉，hello 網站繫結需要不會更新 （hello 網路架構取決於保留期 hello IP 位址和子網路指派 toohello 主要和復原站台，因此可能會或可能不會將為您的組織。）

![SSL 繫結](./media/site-recovery-iis/sslbinding.png)

如果您擁有 hello IP 位址關聯站台，您將需要 tooupdate hello 新 IP 位址的所有站台繫結。 您可以加入[IIS Web 層更新指令碼](https://aka.ms/asr-web-tier-update-runbook-classic)之後復原計劃 toochange hello 站台繫結中的群組 3。


#### <a name="update-load-balancer-ip-address"></a>更新負載平衡器 IP 位址
如果您有應用程式要求路由的虛擬機器，新增[IIS ARR 容錯移轉指令碼](https://aka.ms/asr-iis-arrtier-failover-script-classic)群組 4 tooupdate hello IP 位址之後。

#### <a name="hello-ssl-cert-binding-for-an-https-connection"></a>hello SSL 憑證繫結進行 https 連接
網站可以有相關聯的 SSL 憑證，可協助確保 hello 網頁伺服器與 hello 使用者的瀏覽器之間安全通訊。 如果 hello 網站有一個 https 連線和相關聯的 https 網站繫結 toohello IP 位址的 SSL 憑證繫結 hello IIS 伺服器，新的站台繫結必須 toobe 加入 hello 憑證以 hello hello IIS 虛擬機器的 IP 張貼容錯移轉。

hello SSL 憑證可以發行對-

hello 網站 a) hello 完整的網域名稱<br>
hello 伺服器 b) hello 名稱<br>
c） 萬用字元憑證 hello 網域名稱<br>
d） IP 位址 – 如果 hello IIS 伺服器 hello IP 對發出 hello SSL 憑證，另一個 SSL 憑證需求 toobe hello hello IP 位址對 hello Azure 站台上的 IIS 伺服器發出額外的 SSL 繫結此憑證必須 toobe 建立。 因此，它是針對 IP 所核發的 SSL 憑證的建議 toonot 使用。 這是較不常用的選項，而且很快就會根據新的 CA/瀏覽器論壇變更而取代。

#### <a name="update-hello-dependency-between-hello-web-and-hello-application-tier"></a>更新 hello hello web 和 hello 應用程式層之間的相依性
如果您有根據 hello hello 虛擬機器的 IP 位址的特定相依性的應用程式，您需要 tooupdate 此相依性 post 容錯移轉。

## <a name="doing-a-test-failover"></a>執行測試容錯移轉
請遵循[本指南](site-recovery-test-failover-to-azure.md)toodo 測試容錯移轉。

1.  移 tooAzure 入口網站，然後選取您的復原服務保存庫。
1.  按一下 建立 IIS web 伺服陣列的 hello 復原計劃。
1.  按一下 [測試容錯移轉]。
1.  選取的復原點和 Azure 虛擬網路 toostart hello 測試容錯移轉程序。
1.  一旦 hello 次要環境已啟動，您可以執行您的驗證。
1.  Hello 驗證完成後，您可以選取 '完成驗證'，並將清除 hello 測試容錯移轉環境。

## <a name="doing-a-failover"></a>執行容錯移轉
當您在進行容錯移轉時，請依照[本指引](site-recovery-failover.md)。

1.  移 tooAzure 入口網站，然後選取您的復原服務保存庫。
1.  按一下 建立 IIS web 伺服陣列的 hello 復原計劃。
1.  按一下 [容錯移轉]。
1.  選取的復原點 toostart hello 容錯移轉程序。

## <a name="next-steps"></a>後續步驟
您可以使用站台復原深入了解[複寫其他應用程式](site-recovery-workload.md)。
