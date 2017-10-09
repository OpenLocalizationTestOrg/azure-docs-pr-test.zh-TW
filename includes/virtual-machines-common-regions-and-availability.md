# <a name="regions-and-availability-for-virtual-machines-in-azure"></a>Azure 中虛擬機器的區域和可用性
Azure hello 世界各地的多個資料中心運作。 這些資料中心中分組 toogeographic 區域，讓您彈性選擇 where toobuild 應用程式。 如何和在 Azure 中，您的虛擬機器 (Vm) 作業以及您的選項 toomaximize 效能、 可用性和備援位置，很重要的 toounderstand。 本文章會提供您的 hello 可用性概觀與 Azure 的備援功能。

## <a name="what-are-azure-regions"></a>什麼是 Azure 區域？
您可以在定義的地理區域 (例如「美國西部」、「北歐」或「東南亞」) 中建立 Azure 資源。 您可以檢閱 hello[地區的清單以及其位置](https://azure.microsoft.com/regions/)。 在每個區域中，多個資料中心存在 tooprovide 的備援和可用性。 這種方法可讓您彈性當您設計應用程式 toocreate Vm 最接近 tooyour 使用者和 toomeet 任何合法的相容性，或稅務等不同目的。

## <a name="special-azure-regions"></a>特殊 Azure 區域
Azure 有建置出您的應用程式相容性或法律用途時，您可能希望 toouse 某些特殊區域。 這些特殊區域包括：

* **美國維吉尼亞州政府**和**美國愛荷華州政府**
  * 由經篩選的美國人士所操作、適用於美國政府機構及其合作夥伴的實體與邏輯網路隔離 Azure 執行個體。 包含其他法規遵循認證，例如 [FedRAMP](https://www.microsoft.com/en-us/TrustCenter/Compliance/FedRAMP) 和 [DISA](https://www.microsoft.com/en-us/TrustCenter/Compliance/DISA)。 深入了解 [Azure Government](https://azure.microsoft.com/features/gov/)。
* **中國東部**和**中國北部**
  * 這些區域皆可透過 Microsoft 21Vianet，因此 Microsoft 不會直接維護 hello 資料中心之間的唯一合作關係。 深入了解 [位於中國的 Microsoft Azure](http://www.windowsazure.cn/)。
* **德國中部**和**德國東北部**
  * 這些區域可以透過資料信任者模型，讓客戶資料會保留在德國受控制的 T 系統、 Deutsche Telekom 公司，做為 hello 德文的資料信任者使用。

## <a name="region-pairs"></a>區域配對
每個 Azure 區域搭配 hello 內的另一個區域 （例如美國、 歐洲、 或亞洲） 相同的地理位置。 這種方法可讓 hello 複寫的資源，例如 VM 存放到應該降低 hello 可能性自然災害、 動盪、 電源中斷或同時影響這兩個區域的實體網路中斷的地理位置。 區域配對的其他優點包括：

* 在較寬的 Azure 中斷的 hello 事件中，一個區域已設定優先權，超出每一對 toohelp 減少 hello 時間 toorestore 應用程式。 
* 規劃 Azure，都會回復更新 toopaired 區，一個在時間 toominimize 停機時間和應用程式中斷的風險。
* 資料會繼續 tooreside 內 hello 做為其配對 （除了巴西南部） 進行稅金和法律強制管轄區相同的地理位置。

區域配對的範例包括：

| 主要 | 次要 |
|:--- |:--- |
| 美國西部 |美國東部 |
| 北歐 |西歐 |
| 東南亞 |東亞 |

您可以看到完整的 hello[這裡配對的地區清單](../articles/best-practices-availability-paired-regions.md#what-are-paired-regions)。

## <a name="feature-availability"></a>功能可用性
有些服務或 VM 功能只有在特定區域提供，例如特定的 VM 大小或儲存體類型。 另外還有一些通用的 Azure 服務不需要您 tooselect 特定區域，例如[Azure Active Directory](../articles/active-directory/active-directory-whatis.md)， [Traffic Manager](../articles/traffic-manager/traffic-manager-overview.md)，或[Azure DNS](../articles/dns/dns-overview.md)。 tooassist 您在設計您的應用程式環境，您可以檢查 hello[跨每個區域的 Azure 服務的可用性](https://azure.microsoft.com/regions/#services)。 

## <a name="storage-availability"></a>儲存體可用性
了解 Azure 區域與地理位置變得很重要時考慮 hello 可用的存放裝置複寫選項。 根據 hello 存放裝置類型，您會有不同的複寫選項。

**Azure 受控磁碟**
* 本機備援儲存體 (LRS)
  * 複寫三次 hello 區域，您可以在其中建立儲存體帳戶中的資料。

**儲存體帳戶型磁碟**
* 本機備援儲存體 (LRS)
  * 複寫三次 hello 區域，您可以在其中建立儲存體帳戶中的資料。
* 區域備援儲存體 (ZRS)
  * 您會將資料複寫三次到兩個 toothree 設備，在單一區域或跨兩個區域。
* 異地備援儲存體 (GRS)
  * 會將複寫您資料 tooa 次要區域相隔數百英哩 hello 主要區域。
* 讀取權限異地備援儲存體 (RA-GRS)
  * 在使用 GRS 時，複寫您的資料 tooa 次要區域，但也提供唯讀存取 toohello 資料 hello 次要位置。

hello 下表提供 hello hello 儲存體複寫類型之間的差異的快速概觀：

| 複寫策略 | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| 可跨多個設備複寫資料。 |否 |是 |是 |是 |
| 可以讀取資料，從 hello 次要位置，並從 hello 主要位置。 |否 |否 |否 |是 |
| 可在不同的節點上維護的資料副本數量。 |3 |3 |6 |6 |

您可以 [在這裡深入了解 Azure 儲存體複寫選項](../articles/storage/common/storage-redundancy.md)。 如需受控磁碟的詳細資訊，請參閱 [Azure 受控磁碟概觀](../articles/virtual-machines/windows/managed-disks-overview.md)。

### <a name="storage-costs"></a>儲存成本
價格是根據 hello 儲存類型，以及您所選取的可用性而有所不同。

**Azure 受控磁碟**
* 進階受控磁碟是由固態硬碟 (SSD) 所支援，標準受控磁碟則是由一般轉動式磁碟所支援。 Premium 和 Standard 的管理磁碟負責根據佈建的 hello hello 磁碟容量。

**非受控磁碟**
* 高階儲存體揭開 Solid-State 磁碟機 (Ssd)，並負責根據 hello hello 磁碟容量。
* 標準儲存體受到一般微調磁碟負責根據 hello 中使用的容量和所需儲存體可用性。
  * RA-GRS，會複寫該資料 tooanother Azure 地區的 hello 頻寬額外地理複寫資料傳輸費用。

請參閱[Azure 儲存體定價](https://azure.microsoft.com/pricing/details/storage/)價格 hello 不同的存放裝置類型和可用性選項的詳細資訊。

## <a name="availability-sets"></a>可用性集合
可用性設定組是 Vm 的邏輯群組，可讓 Azure toounderstand 您的應用程式如何建置 tooprovide 的備援和可用性。 我們建議的高可用性的應用程式和 toomeet hello 可用性集 tooprovide 內，系統會建立兩個或多個 Vm [99.95%Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/)。 當正在使用單一 VM [Azure 高階儲存體](../articles/storage/common/storage-premium-storage.md)，hello 非計劃性的維護事件適用於 Azure SLA。 

可用性設定組由兩個其他群組，防止硬體故障並允許的更新 toosafely 會組成套用-故障網域 (Fd) 和更新網域 (Ud)。

![Hello 更新網域和故障網域組態的概念圖](./media/virtual-machines-common-regions-and-availability/ud-fd-configuration.png)

您可以深入了解如何 toomanage hello 的可用性[Linux Vm](../articles/virtual-machines/linux/manage-availability.md)或[Windows Vm](../articles/virtual-machines/windows/manage-availability.md)。

### <a name="fault-domains"></a>容錯網域
容錯網域是共用一般電力來源的基礎硬體的邏輯群組和網路交換器，在內部部署資料中心內的類似 tooa 機架。 當您建立可用性設定組內的 Vm，hello Azure 平台會自動將您的 Vm 分散到這些容錯網域。 這個方法會限制 hello 潛在的實體硬體故障、 網路中斷或電源中斷的影響。

### <a name="update-domains"></a>更新網域
更新網域是基礎硬體，可以進行維護或重新啟動在 hello 的邏輯群組相同的時間。 當您建立可用性設定組內的 Vm，hello Azure 平台會自動發佈您的 Vm 之間這些更新網域。 這個方法可確保您的應用程式至少一個執行個體一定會保持為 hello Azure 平台會經歷定期維護時執行。 正在重新啟動可能不會繼續循序計劃性的維護期間的更新網域，但只能有一個更新網域的 hello 順序已重新啟動一次。

### <a name="managed-disk-fault-domains"></a>受控磁碟容錯網域
若 VM 使用 [Azure 受控磁碟](../articles/virtual-machines/windows/faq-for-disks.md)，VM 會在使用受管理的可用性設定組時配合使用受控磁碟容錯網域。 此連接可確保所有 hello 受管理的磁碟附加的 tooa VM 位於 hello 相同的受管理的磁碟容錯網域。 在受管理的可用性設定組中只能建立使用受控磁碟的 VM。 受管理的磁碟容錯網域的 hello 數目會因區域-每個區域的兩個或三個受管理的磁碟故障網域。

![受控磁碟 FD](./media/virtual-machines-common-manage-availability/md-fd.png)

> [!IMPORTANT]
> hello 受管理的可用性設定組的容錯網域數目會因區域-兩個或三個每個區域。 hello 下表顯示 hello 數目每個區域

[!INCLUDE [managed-disks-common-fault-domain-region-list](managed-disks-common-fault-domain-region-list.md)]

## <a name="next-steps"></a>後續步驟
您現在可以啟動 toouse 這些可用性和備援功能 toobuild Azure 環境。 如需最佳作法資訊，請參閱 [Azure 可用性最佳作法](../articles/best-practices-availability-checklist.md)。

