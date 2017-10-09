
如果這份文件中並未提及您的 Azure 問題，請瀏覽 hello [MSDN 和堆疊溢位上的 Azure 論壇](https://azure.microsoft.com/support/forums/)。 您可以在這些論壇張貼您的問題或too@AzureSupportTwitter 上。 此外，您可以藉由選取檔案 Azure 支援人員要求**取得支援**上 hello [Azure 支援](https://azure.microsoft.com/support/options/)站台。

## <a name="general-troubleshooting-steps"></a>一般疑難排解步驟
### <a name="troubleshoot-common-allocation-failures-in-hello-classic-deployment-model"></a>Hello 傳統部署模型中的一般配置失敗進行疑難排解
這些步驟可協助解決虛擬機器中的許多配置失敗：

* 調整大小 hello VM tooa 其他 VM 大小。<br>
    按一下 [全部瀏覽] > [虛擬機器 (傳統)] > 您的虛擬機器 > [設定] > [大小]。 如需詳細步驟，請參閱[調整 hello 虛擬機器大小](https://msdn.microsoft.com/library/dn168976.aspx)。
* 刪除所有的 Vm 從 hello 雲端服務並重新建立 Vm。<br>
    按一下 [全部瀏覽] > [虛擬機器 (傳統)] > 您的虛擬機器 > [刪除]。 然後，按一下 [新增]  >  [計算] > [虛擬機器映像]。

### <a name="troubleshoot-common-allocation-failures-in-hello-azure-resource-manager-deployment-model"></a>Hello Azure Resource Manager 部署模型中的一般配置失敗進行疑難排解
這些步驟可協助解決虛擬機器中的許多配置失敗：

* 停止 （取消配置） hello 同一個可用性設定，然後重新啟動每個中的所有 Vm。<br>
    toostop： 按一下**資源群組**> 資源群組 >**資源**> 您的可用性設定組 >**虛擬機器**> 您的虛擬機器 > **停止**。
  
    選取所有 Vm 都停止之後，hello 第一個 VM 按一下**啟動**。

## <a name="background-information"></a>背景資訊
### <a name="how-allocation-works"></a>配置的運作方式
在 Azure 資料中心的 hello 伺服器會分割成叢集。 一般來說，配置要求會嘗試在多個叢集，但您可從 hello 配置要求的特定條件約束，強制 hello Azure 平台 tooattempt hello 要求中只能有一個叢集。 我們將在本文中參照 toothis 為 「 已釘選的 tooa 叢集 」。 下面圖 1 說明 hello 嘗試多個群集中的一般配置的大小寫。 圖 2 說明 hello 發生配置的情況下，已釘選 tooCluster 2，因為這是裝載 hello 現有雲端服務 CS_1 或可用性設定組的位置。
![配置圖表](./media/virtual-machines-common-allocation-failure/Allocation1.png)

### <a name="why-allocation-failures-happen"></a>配置失敗的原因
已釘選的 tooa 叢集配置要求時，有更高版本可能會失敗 toofind 釋出資源，因為 hello 可用的資源集區是較小。 此外，如果您配置的要求是已釘選的 tooa 叢集但 hello 您要求的資源類型不支援該叢集，您的要求將會失敗，hello 叢集在沒有可用的資源。 圖 3 說明 hello 案例，其中已釘選的配置失敗，因為 hello 只有候選叢集沒有可用的資源。 圖 4 說明其中釘選的配置失敗，因為只有候選群集 hello 不支援的 hello 情況 hello 即使 hello 叢集已釋放資源，請要求 VM 大小。

![釘選配置失敗](./media/virtual-machines-common-allocation-failure/Allocation2.png)

## <a name="detailed-troubleshoot-steps-specific-allocation-failure-scenarios-in-hello-classic-deployment-model"></a>詳細的疑難排解 hello 傳統部署模型中的步驟特定配置失敗案例
以下是導致釘選配置要求 toobe 的一般配置狀況。 我們將在本文稍後深入探討每一個案例。

* 調整 VM 的大小，或加入 Vm 或角色執行個體 tooan 現有雲端服務
* 重新啟動已部分停止 (已取消配置) 的 VM
* 重新啟動已完全停止 (已取消配置) 的 VM
* 預備/生產部署 (僅適用於平台即服務)
* 同質群組 (VM/服務鄰近性)
* 同質群組式虛擬網路

當您收到配置錯誤時，請參閱是否套用任何 hello 狀況說明 tooyour 錯誤。 使用 hello Azure 平台 tooidentify hello 對應案例所傳回的 hello 配置錯誤。 如果您的要求已釘選，移除一些 hello 釘選的條件約束 tooopen 要求 toomore 叢集，藉此增加 hello 配置成功機率。

一般情況下，只要 hello 錯誤並不表示 「 hello 要求的 VM 大小不支援 」，您可以永遠重試期間之後，如足夠的資源可能已在 hello 叢集 tooaccommodate 釋放您的要求。 如果該 hello 要求不支援 VM 大小 hello 問題，請嘗試不同的 VM 大小。 否則，hello 唯一的選擇是 tooremove hello 釘選條件約束。

兩個常見的失敗案例是相關的 tooaffinity 群組。 在 hello 過去，同質群組使用的 tooprovide 的非常接近 tooVMs/服務執行個體，或是已使用的 tooenable hello 建立虛擬網路。 Hello 介紹地區虛擬網路，使用同質群組就不再需要的 toocreate 虛擬網路。 Hello 縮短網路延遲，在 Azure 基礎結構中，為已變更 VM/服務相近的 hello 建議 toouse 同質群組。

圖 5 顯示 hello 分類的 hello (pin) 配置的案例。
![釘選配置分類](./media/virtual-machines-common-allocation-failure/Allocation3.png)

> [!NOTE]
> 列出每個配置案例中的 hello 錯誤是簡短形式。 請參閱 toohello[錯誤字串查詢](#Error string lookup)詳細的錯誤字串。
> 
> 

## <a name="allocation-scenario-resize-a-vm-or-add-vms-or-role-instances-tooan-existing-cloud-service"></a>配置的案例： 調整 VM 的大小，或加入 Vm 或角色執行個體 tooan 現有的雲端服務
**錯誤**

Upgrade_VMSizeNotSupported 或 GeneralError

**叢集釘選的原因**

A 要求 tooresize VM，或加入 VM 或角色執行個體 tooan 現有雲端服務有 toobe 嘗試裝載 hello 現有的雲端服務的 hello 原始叢集中。 建立新的雲端服務，可讓 hello Azure 平台 toofind 已釋放資源，或支援 hello 您要求的 VM 大小的另一個叢集。

**因應措施**

如果 hello 錯誤 Upgrade_VMSizeNotSupported *，請嘗試不同的 VM 大小。 如果使用不同的 VM 大小不是可行，但如果是可接受 toouse 不同的虛擬 IP 位址 (VIP)，建立新的雲端服務 toohost hello 新的 VM，並加入 hello 新雲端服務 toohello 區域虛擬網路位置 hello 現有 Vm 正在執行。 如果您現有的雲端服務不會使用區域虛擬網路，您可以仍然建立 hello 新的雲端服務，新的虛擬網路，然後再連線您[現有虛擬網路 toohello 新的虛擬網路](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/)。 深入了解 [區域虛擬網路](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/)。

如果 hello 錯誤 GeneralError *，很可能 hello 叢集所支援的資源 （例如特定的 VM 大小） 的 hello 類型，但在 hello 時刻 hello 叢集沒有釋出資源。 類似 toohello 上述案例中，新增所需的 hello 計算資源，透過建立新的雲端服務 （請注意 hello 新雲端服務有 toouse 不同 VIP），並使用區域虛擬網路 tooconnect 雲端服務。

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>配置案例：重新啟動已部分停止 (已取消配置) 的 VM
**錯誤**

GeneralError*

**叢集釘選的原因**

部分解除配置表示您已停止 (已取消配置) 雲端服務中的一或多部 VM，而不是所有 VM。 當您停止 （取消配置） VM 時，相關聯的 hello 並釋出資源。 因此，重新啟動已停止 (已取消配置) 的 VM 是一項新的配置要求。 部分已取消配置的雲端服務中重新啟動 Vm 是對等 tooadding Vm tooan 現有雲端服務。 hello 配置要求有 toobe 嘗試裝載 hello 現有的雲端服務的 hello 原始叢集中。 建立不同的雲端服務，可讓 hello Azure 平台 toofind 另一個叢集可用的資源或支援 hello 您要求的 VM 大小。

**因應措施**

如果可接受 toouse 不同的 VIP，刪除 hello 停止 （取消配置） Vm （但保持相關聯的 hello 磁碟），並新增回透過不同的雲端服務的 hello Vm。 使用區域虛擬網路 tooconnect 雲端服務：

* 如果您現有的雲端服務會使用區域虛擬網路，只要加入新雲端服務 toohello hello 相同虛擬網路。
* 如果您現有的雲端服務不會使用區域虛擬網路，建立新的虛擬網路的 hello 新的雲端服務，然後[您現有虛擬網路 toohello 新虛擬網路連線](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/)。 深入了解 [區域虛擬網路](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/)。

## <a name="allocation-scenario-restart-fully-stopped-deallocated-vms"></a>配置案例：重新啟動已完全停止 (已取消配置) 的 VM
**錯誤**

GeneralError*

**叢集釘選的原因**

完整取消配置表示您已停止 (已取消配置) 雲端服務上的所有 VM。 hello 分派要求的 toorestart 這些 Vm 有 toobe 嘗試裝載 hello 雲端服務的 hello 原始叢集中。 建立新的雲端服務，可讓 hello Azure 平台 toofind 已釋放資源，或支援 hello 您要求的 VM 大小的另一個叢集。

**因應措施**

如果它是可接受 toouse 不同的 VIP 時，刪除 hello 原始停止 （取消配置） Vm （但保持相關聯的 hello 磁碟），並刪除 hello 對應的雲端服務已釋放資源，當您停止 （取消配置） 時 （相關聯的 hello 計算hello Vm)。 重新建立新的雲端服務 tooadd hello Vm。

## <a name="allocation-scenario-stagingproduction-deployments-platform-as-a-service-only"></a>配置案例：預備/生產環境部署 (僅適用於平台即服務)
**錯誤**

New_General* 或 New_VMSizeNotSupported*

**叢集釘選的原因**

預備部署和雲端服務的 hello 生產環境部署的 hello 裝載於 hello 相同叢集中。 當您新增第二個部署的 hello 時，hello 對應配置要求將會嘗試在相同的叢集，主控 hello 第一次部署的 hello。

**因應措施**

刪除第一次部署的 hello 與 hello 原始的雲端服務，然後重新部署 hello 雲端服務。 此動作可能登陸 hello 第一次部署在叢集中具有足夠的可用資源 toofit 這兩個部署或在叢集中可支援您所要求的 hello VM 大小。

## <a name="allocation-scenario-affinity-group-vmservice-proximity"></a>配置案例：同質群組 (VM/服務鄰近性)
**錯誤**

New_General* 或 New_VMSizeNotSupported*

**叢集釘選的原因**

任何指派的 tooan 同質群組的計算資源繫結 tooone 叢集。 新的計算資源要求，在該同質群組來嘗試的 hello 相同叢集 hello 現有資源的裝載位置。 透過新的雲端服務或透過現有的雲端服務的 hello 新資源建立是否為 true。

**因應措施**

如果同質群組不是必要的，請勿使用同質群組或將計算資源分組為多個同質群組。

## <a name="allocation-scenario-affinity-group-based-virtual-network"></a>配置案例：同質群組式虛擬網路
**錯誤**

New_General* 或 New_VMSizeNotSupported*

**叢集釘選的原因**

引進區域虛擬網路之前，您都需要的 tooassociate 虛擬網路與同質群組。 如此一來，放置到同質群組的計算資源由繫結 hello hello 中所述的相同的條件約束 」 配置案例： 同質群組 （VM/服務相近） 」 一節。 繫結的 tooone 叢集的 hello 計算資源。

**因應措施**

如果您不需要同質群組，建立新的地區虛擬網路的 hello 您要加入，新的資源，然後[您現有虛擬網路 toohello 新虛擬網路連線](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/)。 深入了解 [區域虛擬網路](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/)。

或者，您可以[將同質群組為基礎的虛擬網路 tooa 地區虛擬網路移轉](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/)，然後再次新增 hello 所需的資源。

## <a name="detailed-troubleshooting-steps-specific-allocation-failure-scenarios-in-hello-azure-resource-manager-deployment-model"></a>詳細的疑難排解步驟的特定配置失敗案例在 hello Azure Resource Manager 部署模型
以下是導致釘選配置要求 toobe 的一般配置狀況。 我們將在本文稍後深入探討每一個案例。

* 調整 VM 的大小，或加入 Vm 或角色執行個體 tooan 現有雲端服務
* 重新啟動已部分停止 (已取消配置) 的 VM
* 重新啟動已完全停止 (已取消配置) 的 VM

當您收到配置錯誤時，請參閱是否套用任何 hello 狀況說明 tooyour 錯誤。 使用 hello Azure 平台 tooidentify hello 對應案例所傳回的 hello 配置錯誤。 如果您的要求已釘選的 tooan 現有的叢集中，移除一些 hello 釘選的條件約束 tooopen 要求 toomore 叢集，藉此增加 hello 配置成功機率。

一般情況下，只要 hello 錯誤並不表示 「 hello 要求的 VM 大小不支援 」，您可以永遠重試期間之後，如足夠的資源可能已在 hello 叢集 tooaccommodate 釋放您的要求。 如果 hello 問題是該 hello 要求不支援 VM 大小，請參閱下文的因應措施。

## <a name="allocation-scenario-resize-a-vm-or-add-vms-tooan-existing-availability-set"></a>配置的案例： 調整大小的 VM，或加入 Vm tooan 現有可用性設定組
**錯誤**

Upgrade_VMSizeNotSupported* 或 GeneralError*

**叢集釘選的原因**

A 要求 tooresize VM，或加入現有的可用性設定組 VM tooan 具有 toobe 嘗試 hello 原始叢集裝載 hello 現有可用性設定組。 建立新的可用性設定組可讓 hello Azure 平台 toofind 已釋放資源，或支援 hello 您要求的 VM 大小的另一個叢集。

**因應措施**

如果 hello 錯誤 Upgrade_VMSizeNotSupported *，請嘗試不同的 VM 大小。 如果使用不同的 VM 大小不是一個選項，停止 hello 可用性設定組中的所有 Vm。 接著，您可以變更 hello hello 將配置支援 hello 的 hello VM tooa 叢集的虛擬機器大小所需的 VM 大小。

如果 hello 錯誤 GeneralError *，很可能 hello 叢集所支援的資源 （例如特定的 VM 大小） 的 hello 類型，但在 hello 時刻 hello 叢集沒有釋出資源。 如果 hello VM 可以不同的可用性集的一部分，在不同的可用性設定組中建立新的 VM (hello 中相同的區域)。 這個新的 VM 可 toohello 新增相同的虛擬網路。  

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>配置案例：重新啟動已部分停止 (已取消配置) 的 VM
**錯誤**

GeneralError*

**叢集釘選的原因**

部分解除配置表示您已停止 (已取消配置) 可用性設定組中的一或多部 VM，而不是所有 VM。 當您停止 （取消配置） VM 時，相關聯的 hello 並釋出資源。 因此，重新啟動已停止 (已取消配置) 的 VM 是一項新的配置要求。 重新啟動 Vm 的部分已取消配置的可用性設定組是相當 tooadding Vm tooan 現有可用性設定。 hello 配置要求有 toobe 嘗試 hello 原始叢集裝載 hello 現有可用性設定組。

**因應措施**

Hello 可用性設定組重新啟動 hello 第一個之前停止所有 Vm。 如此可確保執行新的配置嘗試，而且可以選取有容量可用的新叢集。

## <a name="allocation-scenario-restart-fully-stopped-deallocated"></a>配置案例：重新啟動已完全停止 (已取消配置)
**錯誤**

GeneralError*

**叢集釘選的原因**

完整取消配置表示您已停止 (已取消配置) 可用性設定組中的所有 VM。 這些 Vm 將目標支援的所有叢集 hello 分派要求 toorestart hello 所需的大小。

**因應措施**

選取新的 VM 大小 tooallocate。 如果仍無法解決問題，請稍後再試。

## <a name="error-string-lookup"></a>錯誤字串查詢
**New_VMSizeNotSupported***

"hello VM 大小 （或 VM 大小的組合） 這個部署所需，無法佈建由於 toodeployment 要求條件約束。 可能的話，請嘗試放寬條件約束，例如虛擬網路繫結、 部署 tooa 託管服務中沒有其他部署和 tooa 不同同質群組或不含同質群組或再試一次部署 tooa 不同的區域。 」

**New_General***

「 配置失敗。在要求中無法 toosatisfy 條件約束。 hello 要求新的服務部署繫結的 tooan 同質群組，或它的目標虛擬網路，或有現有的部署這個託管服務底下。 這些條件會限制新部署 toospecific hello Azure 資源。 請稍後再重試，或嘗試減少 hello VM 大小或角色執行個體數目。 或者，可能的話，請移除 hello 上述條件約束，或嘗試部署 tooa 不同區域。 」

**Upgrade_VMSizeNotSupported***

「 無法 tooupgrade hello 部署。 hello 要求的 VM 大小 XXX 可能無法支援 hello 現有部署的 hello 資源中。 請稍後再試、嘗試使用不同的 VM 大小或較少的角色執行個體，或在空的託管服務下以建立新的同質群組或沒有同質群組繫結來建立部署。」

**GeneralError***

「 hello 伺服器發生內部錯誤。 請重試 hello 要求。 」 或者 「 失敗 tooproduce hello 服務的配置。 」

