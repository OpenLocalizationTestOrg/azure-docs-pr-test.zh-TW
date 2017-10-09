---
title: "移轉的 IaaS 資源從資源管理員的傳統 tooAzure aaaPlanning |Microsoft 文件"
description: "規劃移轉的 IaaS 資源從傳統 tooAzure 資源管理員"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 78492a2c-2694-4023-a7b8-c97d3708dcb7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/01/2017
ms.author: kasing
ms.openlocfilehash: 53c6f640425b69cae2ef10afb8c92b8ac4394267
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="planning-for-migration-of-iaas-resources-from-classic-tooazure-resource-manager"></a>規劃移轉的 IaaS 資源從傳統 tooAzure 資源管理員
而 Azure 資源管理員提供許多令人讚嘆的功能，它是關鍵 tooplan 出您移轉之旅 toomake 確定事情順利進行。 詳細規劃可確保您在執行移轉活動期間不會遇到問題。 

> [!NOTE] 
> 下列指導方針的 hello 已大量佔多少的 tooby hello Azure 客戶諮詢團隊和雲端方案架構設計人員與客戶合作移轉大型 enviornments 上。 因此本文件將會繼續 tooget 更新成功的新模式出現時，所以請從時間 tootime toosee 是否有任何新的建議。

有四個一般階段 hello 移轉作業：

![移轉階段](../media/virtual-machines-windows-migration-classic-resource-manager/plan-labtest-migrate-beyond.png)

## <a name="plan"></a>規劃

### <a name="technical-considerations-and-tradeoffs"></a>技術考量和取捨

根據您的技術需求大小、 地理位置和操作作法，您可能想 tooconsider:

1. 為什麼您的組織需要 Azure Resource Manager？  移轉的 hello 商業理由為何？
2. Hello 技術原因的 Azure 資源管理員有哪些？  功能 （如果有的話） 其他 Azure 服務您像 tooleverage 嗎？
3. 哪些應用程式 （或虛擬機器的設定） 隨附於 hello 移轉？
4. Hello 移轉應用程式開發介面支援的案例？  檢閱 hello[不支援的功能和設定](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#unsupported-features-and-configurations)。
5. 您的作業團隊目前支援傳統和 Azure Resource Manager 中的應用程式/VM 嗎？
6. Azure Resource Manager 如何變更您的 VM 部署、管理、監視和報告處理程序 (如果有的話)？  部署指令碼需要 toobe 更新嗎？
7. 什麼是 hello 通訊計劃 tooalert 專案關係人 （使用者、 應用程式擁有者，以及基礎結構擁有者）？
8. 根據 hello 環境的 hello 複雜度，應該會有維護期間 hello 應用程式，其中是使用者無法使用 tooend 和 tooapplication 擁有者嗎？  如果是這樣，該期間需要多久？
9. 什麼是 hello 訓練計劃 tooensure 專案關係人是知識和非常熟悉 Azure 資源管理員中？
10. Hello 程式管理或 hello 移轉專案管理計劃是什麼？
11. 什麼是 hello 砸下的大筆花費 hello Azure 資源管理員移轉，以及其他相關技術路段圖地圖？  它們之間的配合是否理想？

### <a name="patterns-of-success"></a>成功的模式

成功的客戶有詳細的計畫，其中討論、 記錄和控管 hello 上述問題。  請確定 hello 移轉計劃會廣泛地溝通的 toosponsors 和專案關係人。  讓自己具備有關移轉選項的知識；強烈建議您閱讀以下的移轉文件集。

* [平台支援移轉的 IaaS 資源從傳統 tooAzure 資源管理員概觀](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [技術的深入剖析平台支援移轉從傳統 tooAzure 資源管理員](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [規劃移轉的 IaaS 資源從傳統 tooAzure 資源管理員](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [使用傳統 tooAzure 資源管理員的 PowerShell toomigrate IaaS 資源](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [使用 CLI toomigrate IaaS 資源從傳統 tooAzure 資源管理員](migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [社群工具，用以協助移轉的 IaaS 資源從傳統 tooAzure 資源管理員](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [檢閱最常見的移轉錯誤](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [檢閱 hello 最常見問題集從傳統 tooAzure 資源管理員移轉的 IaaS 資源](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="pitfalls-tooavoid"></a>陷阱 tooavoid

- 失敗 tooplan。  hello 此移轉技術步驟已通過驗證，且可預測 hello 結果。
- 假設 hello 平台支援移轉應用程式開發介面會說明所有案例。 讀取 hello[不支援的功能和設定](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#unsupported-features-and-configurations)toounderstand 支援案例。
- 未針對使用者規劃潛在的應用程式中斷。  規劃足夠的緩衝區 tooadequately 警告使用者，可能無法使用應用程式時間。


## <a name="lab-test"></a>實驗室測試 

**複寫您的環境並執行測試移轉**
  > [!NOTE]
  > 現有環境的確切複寫是使用 Microsoft 支援服務未正式支援的社群貢獻工具來執行。 因此，它是**選擇性**步驟，但它是 hello 最佳方式 toofind 但沒有碰觸實際執行環境的問題。 如果使用社群貢獻的工具不是可行，然後閱讀 hello 下方的驗證/準備 Abort 乾執行建議。
  >
  
  測試您確切 （運算、 網路及存放裝置） 時實驗室是案例的最佳方式 tooensure hello 移轉作業能順利。 這將有助於確保：

  - 完全獨立的實驗室或現有的非生產環境 tootest。 我們建議使用可以重複移轉且可透過破壞性方式修改的完全獨立實驗室。  以下列出 hello 真實訂用帳戶中的指令碼 toocollect/hydrate 中繼資料。
  - 它是個不錯的主意 toocreate hello 實驗室個別訂用帳戶中。 hello 的原因是 hello 實驗室將被清除重複，而且需要個別，隔離的訂用帳戶將會減少 hello 的機率，實際的項目會被意外刪除。

  這可以使用 hello AsmMetadataParser 工具完成。 [在這裡深入了解此工具](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

### <a name="patterns-of-success"></a>成功的模式

hello 下列已發現的許多 hello 較大的移轉問題。 這不是獨占清單，您應該參閱 toohello[不支援的功能和設定](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#unsupported-features-and-configurations)如需詳細資訊。 您可能會或可能不會發生這些技術問題，但如果您確實在嘗試移轉之前解決這些問題，將可確保獲得更順暢的體驗。

- **執行 驗證/準備 Abort 乾執行**-這可能是 hello 最重要步驟 tooensure 傳統 tooAzure 資源管理員移轉是否成功。 hello 移轉應用程式開發介面有三個主要步驟： 驗證、 準備和認可。 驗證會讀取傳統環境的 hello 狀態，並傳回結果的所有問題。 不過，由於一些問題可能在於 hello Azure Resource Manager 堆疊中，驗證將不會攔截所有項目。 hello 移轉程序中的下一個步驟，準備有助於公開 （expose） 這些問題。 準備將移動 hello 傳統 tooAzure 資源管理員 中，從中繼資料，但將不認可 hello 移動，並將會移除或變更 hello 傳統端上的任何項目。 hello 乾執行牽涉到準備 hello 移轉，則中止 (**未認可**) hello 移轉的準備。 驗證/準備/abort 乾執行 hello 目標是 toosee hello Azure Resource Manager 堆疊中的 hello 中繼資料的所有檢查它 (*以程式設計方式或在網站中*)，並確認所有項目移轉是否正確，並透過技術問題。  它也會讓您大致了解移轉時間，以便規劃停機時間。  驗證/準備/abort 不會造成任何使用者的停機時間者;因此，它是不中斷 tooapplication 用法。
  - 以下項目 hello 需要 toobe 解決之前 hello 乾執行，但乾執行測試，會安全地也清除這些準備步驟如果他們遺失。 企業在移轉期間，我們找到 hello 乾執行 toobe 安全且有用的方式 tooensure 移轉整備。
  - 當準備執行的，hello 控制平面 （Azure 的管理作業） 將鎖定 hello 整個虛擬網路，因此不能變更 tooVM 中繼資料期間驗證/準備/abort。  但另一方面，任何應用程式功能 (RD、VM 使用量等) 將不會受到影響。  Hello Vm 的使用者將不會知道該 hello 乾執行正在執行。

- **ExpressRoute 線路和 VPN**。 目前具有授權連結的 ExpressRoute 閘道，無法在沒有停機時間的情況下進行移轉。 Hello 因應措施，請參閱[移轉 ExpressRoute 電路和相關聯的虛擬網路與 hello 傳統 toohello Resource Manager 部署模型](../../expressroute/expressroute-migration-classic-resource-manager.md)。

- **VM 擴充功能**-虛擬機器擴充功能可能是其中一種 hello 執行中 Vm 最大障礙 toomigrating。 VM 擴充功能的修復可能需要多達 1-2 天，因此請適當地進行規劃。  可運作的 Azure 代理程式是執行中的 Vm 所需的 tooreport 後 VM 擴充功能狀態。 如果 hello 狀態恢復為已損毀的執行中的 VM，這將會暫止移轉。 hello 代理程式本身不需要 toobe 在工作順序 tooenable 移轉中，但如果擴充功能存在於 hello VM，然後向前移轉 toomove 時需要這兩個工作代理程式 （具有 DNS) 和連出網際網路連線。
  - 如果在移轉期間，所有的 VM 擴充功能，除了 BGInfo v1 失去連線 tooa DNS 伺服器。\*需要 toofirst 會從每個 VM 之前移轉的準備和後續重新加入後 toohello VM 在 Azure 資源管理員移轉之後。  **這僅適用於執行中的 VM。**  如果 hello Vm 都已停止解除配置 VM 擴充功能不需要移除 toobe。 **注意：**許多擴充功能 (例如 Azure 診斷和資訊安全中心監視) 在移轉之後將會自行重新安裝，因此移除這些功能不是問題。
  - 此外，請確定網路安全性群組不會限制輸出網際網路存取。 某些網路安全性群組組態可能會發生此情況。 用於 VM 擴充功能需要的對外網際網路存取 （或 DNS） toobe 移轉 tooAzure 資源管理員。 
  - 有兩個版本的 hello BGInfo 擴充功能： v1 和 v2。  如果使用 hello 傳統入口網站或 PowerShell 建立 hello VM，hello VM 將可能有 hello v1 延伸模組。 此延伸模組不需要移除 toobe，並將 （沒有移轉） 略過由 hello 移轉應用程式開發介面。 不過，如果 hello 新版 Azure 入口網站建立 hello 傳統 VM 時，它可能需要 hello JSON 型 v2 BGInfo，版本可能會移轉的 tooAzure hello 代理程式可運作，且有傳出網際網路存取 （DNS） 提供資源管理員。 
  - **修復選項 1**。 如果您知道您的 Vm 不會有傳出網際網路存取，請使用 DNS 服務，然後 hello Vm 上使用 Azure 代理程式，再解除安裝所有 VM 擴充功能之前準備 hello 移轉過程中，然後重新 hello VM 擴充功能安裝在移轉之後。 
  - **修復選項 2**。 如果 VM 擴充功能而言太大的障礙，另一個選項是 tooshutdown/解除配置之前移轉的所有 Vm。 移轉 hello 解除配置 Vm，然後重新啟動它們 hello Azure Resource Manager 端上。 hello 好處是 VM 擴充功能將會移轉。 hello 選項的缺點是將會遺失所有公開虛擬 Ip （這可能都是非入門），而顯然 hello Vm 將會關閉工作應用程式上造成更大的影響。

    > [!NOTE] 
    > 如果 Azure 資訊安全中心原則針對 hello 執行移轉 Vm，hello 安全性原則需要 toobe 移除擴充功能之前，先停止，否則 hello 安全性監視功能延伸模組將會重新安裝會自動在 hello 之後的 VM將它移除。

- **可用性設定組**-如果要讓虛擬網路 (vNet) toobe 移轉 tooAzure 資源管理員、 hello 傳統部署 （也就是雲端服務） 所包含的 Vm 必須是在一個可用性設定組，或 hello Vm 都不能在任何可用性設定組。 有一個以上的可用性設定組中 hello 雲端服務不相容的 Azure 資源管理員，將會暫止的移轉。  此外，不能有一些 VM 在可用性設定組中，而一些 VM 則不在可用性設定組中。 tooresolve，您將需要 tooremediate 或 reshuffle 您的雲端服務。  因為這可能會耗費大量時間，請詳細規劃。 

- **Web/背景工作角色部署**-雲端服務包含 web 和背景工作角色無法移轉 tooAzure 資源管理員。 開始移轉之前 hello web/背景工作角色必須先移除從 hello 虛擬網路。  一般的解決方案是 toojust 移動 web/背景工作角色執行個體 tooa 個別傳統虛擬網路，同時也是連結的 tooan ExpressRoute 循環或 toomigrate hello 程式碼 toonewer PaaS 應用程式服務 （此討論已超出本文件 hello 範圍）。 Hello 前者在重新部署案例、 建立新的傳統虛擬網路，移動/重新部署 hello web/背景工作角色 toothat 新的虛擬網路，然後從 hello 正在移動的虛擬網路刪除 hello 部署。 不需要變更程式碼。 新的 hello[虛擬網路對等互連](../../virtual-network/virtual-network-peering-overview.md)功能可以使用的 toopeer 一起 hello 傳統虛擬網路包含 hello web/背景工作角色，而且在其他虛擬網路 hello 例如 hello 虛擬網路位於同一個 Azure 地區移轉 (**無法移轉後所以虛擬網路完成虛擬網路的移轉後**)，因此提供 hello 相同的功能不會降低效能，任何延遲/頻寬負面影響。 指定的 hello 加法[虛擬網路對等互連](../../virtual-network/virtual-network-peering-overview.md)，web/背景工作角色部署現在輕鬆地降低，而不會封鎖 hello 移轉 tooAzure 資源管理員。

- **Azure Resource Manager 配額** - Azure 區域對於傳統和 Azure Resource Manager 有個別的配額/限制。 即使新的硬體不被取用的移轉案例中*（我們要交換傳統 tooAzure 資源管理員中的現有 Vm）*，Azure 資源管理員配額仍然需要 toobe 之前足夠容量的就地可以進行移轉。 以下列出 hello 我們已看到的主要限制會造成問題。  開啟配額支援票證 tooraise hello 限制。 

    > [!NOTE]
    > 這些限制需要 toobe 中引發目前的環境 toobe 移轉後 hello 相同的區域。
    >

    - 網路介面
    - 負載平衡器
    - 公用 IP
    - 靜態公用 IP
    - 核心
    - 網路安全性群組
    - 路由表

    您可以檢查您目前的 Azure 資源管理員配額，使用下列命令與 hello Azure CLI 2.0 最新版本的 hello。

    **計算** *(核心，可用性設定組)*

    ```bash
    az vm list-usage -l <azure-region> -o jsonc 
    ```

    **網路** *(虛擬網路、靜態公用 IP、公用 IP、網路安全性群組、網路介面、負載平衡器、路由表)*
    
    ```bash
    az network list-usages -l <azure-region> -o jsonc
    ```

    **儲存體** *(儲存體帳戶)*
    
    ```bash
    az storage account show-usage
    ```

- **Azure Resource Manager API 節流限制** - 如果您有一個夠大的環境 (例如， > 400 Vm 在 VNET 中)，您可能會遇到 hello 預設 API 節流限制為寫入 (目前**1200年寫入/小時**) 在 [Azure 資源管理員] 中。 開始移轉之前, 您應該要引發的支援票證 tooincrease 這項限制您訂用帳戶。

- **佈建已逾時 VM 狀態**-如果任何 VM 已 hello 狀態**佈建已逾時**，這個需求 toobe 解決移轉前。 hello 的唯一方式 toodo 這是停機的情況下解除佈建/重新佈建 hello VM （刪除它，保持 hello 磁碟並重新建立 hello VM）。 

- **RoleStateUnknown VM 狀態**-移轉中止，因為如果 tooa**角色狀態未知的**錯誤訊息，請檢查 hello VM 使用 hello 入口網站，並確保它正在執行。 此錯誤通常會在幾分鐘之後自行消失 (不需補救)，而且是虛擬機器**啟動**、**停止**、**重新啟動**作業期間經常會看到的暫時性類型。 **建議做法：**幾分鐘後再重試移轉。 

- **Fabric 叢集不存在** - 在某些情況下，某些 VM 由於各種奇怪的原因而無法移轉。 這些已知的情況下的其中一個就是 hello VM 最近才建立 （在上週 hello 左右），並且發生 tooland Azure 叢集概略尚無法針對 Azure 資源管理員工作負載。  您會收到錯誤指出**網狀架構叢集不存在**和 hello VM 無法移轉。 依照 hello 叢集很快就會取得 Azure 資源管理員啟用，等待幾天將通常會解決此特定問題。 不過，一個直接的因應措施太`stop-deallocate`hello VM，然後再繼續移轉，並啟動 hello VM 備份 Azure 資源管理員中，在移轉之後。

### <a name="pitfalls-tooavoid"></a>陷阱 tooavoid

- 請勿使用快捷並且省略 hello 驗證/準備/abort 乾執行移轉。
- 最，如果不是全部，您可能會發生的問題就會出現在 hello 驗證/準備/abort 步驟。

## <a name="migration"></a>移轉

### <a name="technical-considerations-and-tradeoffs"></a>技術考量和取捨

現在您已準備好因為您已透過 hello 您環境的已知問題。

Hello 實際移轉，您可能想 tooconsider:

1. 計劃和排程 hello 虛擬網路 （最小單位移轉），以增加優先順序。  首先，請勿 hello 簡單的虛擬網路，並以更多的 hello 進行複雜的虛擬網路。
2. 大部分客戶會有非生產環境和生產環境。  最後才對生產環境進行排程。
3. **(選擇性)** 排程維護停機時間，並加上許多緩衝時間，以因應非預期的問題發生。
4. 萬一發生問題，請連絡並配合您的支援團隊。

### <a name="patterns-of-success"></a>成功的模式

從 hello 實驗室測試上面 hello 技術的指導方針考慮，並降低先前 tooa 實際移轉。  使用適當的測試，hello 移轉是實際上不是事件。  實際執行環境，可能很有幫助 toohave 其他支援，例如受信任的 Microsoft 合作夥伴或 Microsoft Premier 服務。

### <a name="pitfalls-tooavoid"></a>陷阱 tooavoid

未完整測試，可能會造成問題，hello 移轉的延遲時間。  

## <a name="beyond-migration"></a>移轉之外

### <a name="technical-considerations-and-tradeoffs"></a>技術考量和取捨

既然您已在 [Azure 資源管理員] 中，最大化 hello 平台。  讀取 hello [Azure 資源管理員概觀](../../azure-resource-manager/resource-group-overview.md)toofind 出需額外的好處。

項目 tooconsider:

- 結合在一起的其他活動與 hello 移轉。  大部分客戶會選擇應用程式維護期間。  因此，您可能想 toouse 這個停機時間 tooenable 若其他 Azure 資源管理員功能，例如加密和移轉 tooManaged 磁碟。
- 再次瀏覽 hello 技術和商業理由的 Azure 資源管理員中。啟用 hello 其他服務，只有在 Azure 資源管理員中提供適用於 tooyour 環境。
- 利用 PaaS 服務現代化您的環境。

### <a name="patterns-of-success"></a>成功的模式

是故意上何種服務現在想 tooenable Azure 資源管理員中。  許多客戶發現以下的 Azure 環境的 hello:

- [角色型存取控制](../../azure-resource-manager/resource-group-overview.md#access-control)。
- [Azure Resource Manager 範本使得部署更容易且更受控制](../../azure-resource-manager/resource-group-overview.md#template-deployment)。
- [標籤](../../azure-resource-manager/resource-group-using-tags.md)。
- [活動控制](../../azure-resource-manager/resource-group-audit.md)
- [資源原則](../../azure-resource-manager/resource-manager-policy.md)

### <a name="pitfalls-tooavoid"></a>陷阱 tooavoid

請記住您啟動這個傳統 tooAzure 資源管理員移轉作業的原因。  Hello 原始商業用途為何？ 您未達到 hello 的商業原因？


## <a name="next-steps"></a>後續步驟

* [平台支援移轉的 IaaS 資源從傳統 tooAzure 資源管理員概觀](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [技術的深入剖析平台支援移轉從傳統 tooAzure 資源管理員](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [規劃移轉的 IaaS 資源從傳統 tooAzure 資源管理員](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [使用傳統 tooAzure 資源管理員的 PowerShell toomigrate IaaS 資源](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [社群工具，用以協助移轉的 IaaS 資源從傳統 tooAzure 資源管理員](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [檢閱最常見的移轉錯誤](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [檢閱 hello 最常見問題集從傳統 tooAzure 資源管理員移轉的 IaaS 資源](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
