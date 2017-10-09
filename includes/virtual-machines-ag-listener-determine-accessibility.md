有兩種方式 tooconfigure 可用性群組接聽程式在 Azure 中的重要 toorealize 它。 hello 方式的差異在於建立 hello 接聽程式時所使用的 Azure 負載平衡器的 hello 型別。 下表中的 hello 說明 hello 差異：

| 負載平衡器類型 | 實作 | 使用時機： |
| --- | --- | --- |
| **外部** |使用 hello*公用虛擬 IP 位址*hello 雲端服務裝載 hello 虛擬機器 (Vm)。 |您必須從外部 hello 虛擬網路，包括從 hello 網際網路 tooaccess hello 接聽程式。 |
| **內部** |使用*內部負載平衡器*與 hello 接聽程式的私人位址。 |您可以存取 hello 接聽程式只能從 hello 內相同的虛擬網路。 此存取包括混合案例中的站對站 VPN。 |

> [!IMPORTANT]
> 接聽程式，使用 hello 雲端服務的公用 VIP （外部負載平衡器），只要 hello 用戶端、 接聽程式和資料庫位於 hello 相同 Azure 區域，您將不會產生輸出費用。 否則，任何資料透過傳回 hello 接聽程式被視為輸出容量，而且收費標準資料傳送速率。 
> 
> 

ILB 只可以在具有區域範圍的虛擬網路上設定。 已針對同質群組設定的現有虛擬網路無法使用 ILB。 如需詳細資訊，請參閱[內部負載平衡器概觀](../articles/load-balancer/load-balancer-internal-overview.md)。

