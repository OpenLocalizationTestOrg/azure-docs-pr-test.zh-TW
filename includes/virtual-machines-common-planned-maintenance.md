Azure 會定期執行更新 tooimprove hello 可靠性、 效能及 hello 主機基礎結構安全性的虛擬機器。 這些更新的範圍從修補程式的軟體元件 hello 裝載環境 （如作業系統、 hypervisor 和各種 hello 主機上部署的代理程式），在升級網路元件，toohardware 解除委任。 hello 的大部分這些更新會執行沒有任何影響 toohello 裝載虛擬機器。 不過，更新在某些情況下確實會造成影響：

- 如果 hello 維護不需要重新開機，Azure 會在更新 hello 主機時使用就地移轉 toopause hello VM。

- 維護需要重新開機，如果您已規劃 hello 維護時出現的通知。 在這些情況下，您也將提供的時間窗口開始 hello 維護您自己，適用於您一次。

本頁面說明 Microsoft Azure 如何執行這兩種類型的維護。 未計劃的事件 （中斷） 的詳細資訊，請參閱管理 hello 可用性的虛擬機器，適用於 [Windows] (.../ articles/virtual-machines/windows/manage-availability.md) 或[Linux](../articles/virtual-machines/linux/manage-availability.md)。

虛擬機器中執行的應用程式可以使用的未來更新的蒐集資訊 hello Azure 中繼資料服務進行[Windows](../articles/virtual-machines/windows/instance-metadata-service.md)或 [Linux] (.../ articles/virtual-machines/linux/instance-metadata-service.md)。

## <a name="in-place-vm-migration"></a>就地 VM 移轉

當更新不需要完整重新開機時，則會使用就地即時移轉。 Hello 更新期間 hello 虛擬機器已經暫停大約 30 秒，而裝載環境的 hello 適用於 hello 必要更新和修補程式保留在 RAM 而 hello 記憶體。 hello 虛擬機器再繼續執行，而且 hello 時鐘 hello 虛擬機器的自動同步處理。

對於可用性設定組中的 VM，更新網域會一次更新一個。 暫停、 更新，然後繼續進行之前計劃性的維護移 toohello 上一個更新網域 (UD) 中的所有 Vm UD 下一步。

這些類型的更新會對某些應用程式造成影響。 執行處理，例如媒體串流處理或轉碼或高輸送量網路案例中，即時事件的應用程式可能不是設計的 tootolerate 暫停 30 秒。 <!-- sooooo, what should they do? --> 


## <a name="maintenance-requiring-a-reboot"></a>維護需要重新開機

當 Vm 需要 toobe 計劃性維護重新開機時，就會事先通知。 規劃的維護有兩個階段： hello 自助服務 視窗和排程的維護期間。

hello**自助視窗**可讓您起始 hello 維護您的 Vm 上。 在此期間，您可以查詢每個 VM toosee 其狀態，並檢查您的最後一個維護要求 hello 結果。

當您啟動自助服務維護時，您的 VM 是移動的 tooa 節點已經更新，然後開啟電源時它傳回。 Hello VM 重新開機，因為 hello 暫存磁碟遺失，且會更新虛擬網路介面相關聯的動態 IP 位址。

如果您啟動自助服務維護，而且 hello 程序期間沒有錯誤，hello 作業已停止，hello VM 不會更新，它也會移除從 hello 計劃的維護反覆項目。 您會在與新的排程更新的時間內連絡並提供新商機 toodo 自助服務維護。 

經過 hello 自助服務視窗之後，hello**排程的維護期間**開始。 這段期間，您可以仍然 hello 維護視窗，請查詢，但不再能 toostart hello 維護自己。

## <a name="availability-considerations-during-planned-maintenance"></a>規劃維護期間的可用性考量 

如果您決定 toowait，直到 hello 計劃的維護期間，有幾件事 tooconsider 維護 hello 最高可用性 Vm。 

### <a name="paired-regions"></a>配對的區域

每個 Azure 區域搭配另一個地區內 hello 相同的地理位置，同時讓地區組。 計劃在維護期間，Azure 只會更新 hello 單一區域的區域配對中的 Vm。 例如，在更新 hello 美國中北部的虛擬機器時，Azure 不會更新在美國中南部任何虛擬機器在 hello 相同的時間。 不過，其他地區為北歐可以進行維護在 hello 相同時間為美國東部。 了解區域配對的運作方式可協助您將 VM 更妥善地分散於各區域。 如需詳細資訊，請參閱 [Azure 區域配對](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)。

### <a name="availability-sets-and-scale-sets"></a>可用性設定組和擴展集

在部署 Azure Vm 上的工作負載時，您可以建立可用性集 tooprovide 高可用性 tooyour 應用程式中的 hello Vm。 這可確保在中斷或維護事件期間，至少有一部虛擬機器可供使用。

在可用性設定組，個別的 Vm 會散佈 too20 升級網域 (Ud) 組成。 在規劃維護期間，在任何指定時間只有單一更新網域受影響。 請注意，受到影響的更新網域的 hello 順序不一定會以循序方式。 

虛擬機器擴展集都可讓您的 Azure 計算資源 toodeploy 和管理一組相同的 Vm 為單一資源。 更新網域，例如可用性設定組中的 Vm 之間，會自動部署 hello 規模集。 就如同可用性設定組，使用擴展集，在任何指定時間只有單一更新網域受影響。

如需設定您的虛擬機器的高可用性的詳細資訊，請參閱 < 管理 hello 可用性的虛擬機器適用於 Windows (../ articles/virtual-machines/windows/manage-availability.md) 或[Linux](../articles/virtual-machines/linux/manage-availability.md)。
