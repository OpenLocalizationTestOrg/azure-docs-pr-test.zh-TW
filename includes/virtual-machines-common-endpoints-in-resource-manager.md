hello 方法 tooAzure 端點的運作方式稍有不同 hello 傳統和資源管理員部署模型之間。 在 hello 資源管理員部署模型中，您現在可以 hello 彈性 toocreate 網路篩選條件可控制 hello 流量的流量進出您的 Vm。 這些篩選器可讓您 toocreate 複雜網路的環境之外的簡單的端點，如同 hello 傳統部署模型。 這篇文章提供網路安全性群組的概觀，以及它們與使用傳統端點、建立篩選規則和範例部署案例有何不同。

## <a name="overview-of-resource-manager-deployments"></a>Resource Manager 部署的概觀
Hello 傳統部署模型中的端點會取代網路安全性群組，和存取控制清單 (ACL) 規則。 實作網路安全性群組 ACL 規則的快速步驟如下︰

* 建立網路安全性群組。
* tooallow 或拒絕流量，請定義您的網路安全性群組 ACL 規則。
* 您的網路安全性群組 tooa 網路介面或虛擬網路子網路指派。

如果您會想 tooalso 執行連接埠轉送，您需要在您的 VM 前面 tooplace 負載平衡器使用 NAT 規則。 實作負載平衡器和 NAT 規則的快速步驟應如下所示︰

* 建立負載平衡器。
* 建立後端集區並加入您的 Vm toohello 集區。
* 定義您所需的 hello 連接埠轉送的 NAT 規則。
* 將您的 NAT 規則指派 tooyour Vm。

## <a name="network-security-group-overview"></a>網路安全性群組概觀
網路安全性群組可提供您 tooallow 特定連接埠的安全性層級和子網路 tooaccess Vm。 您通常都有提供此 Vm 之間 hello world 以外的安全性層級網路安全性群組。 套用的 tooa 虛擬網路子網路或 VM 的特定網路介面，可以是網路安全性群組。 不是建立端點 ACL 規則，您現在會建立網路安全性群組 ACL 規則。 這些 ACL 規則可提供比只給定的通訊埠建立端點 tooforward 多更好的控制。 如需詳細資訊，請參閱[什麼是網路安全性群組？](../articles/virtual-network/virtual-networks-nsg.md)

> [!TIP]
> 您可以指定網路安全性群組 toomultiple 子網路或網路介面。 沒有 1:1 對應。 您可以建立網路安全性群組與一組常用的 ACL 規則，並套用 toomultiple 子網路或網路介面。 此外，網路安全性小組可能會套用的 tooresources 訂用帳戶 (根據[角色型存取控制](../articles/active-directory/role-based-access-control-what-is.md)。

## <a name="load-balancers-overview"></a>負載平衡器概觀
在 hello 傳統部署模型中，Azure 會執行所有 hello 網路位址轉譯 (NAT) 與連接埠為您的雲端服務上的轉送。 建立端點時，您可以指定 hello 外部連接埠 tooexpose 以及 hello 內部連接埠 toodirect 流量。 網路安全性群組本身不會執行這個相同的 NAT 和連接埠轉送。 

tooallow 您 toocreate NAT 規則的這類的連接埠轉送，Azure 負載平衡器中建立資源群組。 同樣地，hello 負載平衡器是細微足夠 tooonly 套用 toospecific Vm，視。 hello Azure 負載平衡器 NAT 規則的運作與網路安全性群組 ACL 規則 tooprovide 一起更多的彈性和控制比已達到使用雲端服務端點。 如需詳細資訊，請參閱 hello[負載平衡器概觀](../articles/load-balancer/load-balancer-overview.md)。

## <a name="network-security-group-acl-rules"></a>網路安全性群組 ACL 規則
ACL 規則可讓您根據特定的連接埠、連接埠範圍或通訊協定，定義可以進出您 VM 的流量。 Tooindividual Vm 或 tooa 子網路指派規則。 下列螢幕擷取畫面的 hello 是常見的 web 伺服器上的 ACL 規則的範例：

![網路安全性群組 ACL 規則的清單](./media/virtual-machines-common-endpoints-in-resource-manager/example-acl-rules.png)

ACL 規則會套用根據優先順序度量資訊會指定-hello hello 值越高，hello hello 優先順序。 每個網路安全性群組具有三個預設規則所設計的 Azure 網路流量，其明確的 toohandle hello 流程`DenyAllInbound`hello 最終的規則。 預設 ACL 規則會指定低優先順序 toonot 會影響您建立的規則。

## <a name="assigning-network-security-groups"></a>指派網路安全性群組
您指定網路安全性群組 tooa 子網路或網路介面。 這種方法可讓您 toobe 精細視時套用您的 ACL 規則 tooonly 特定 VM，或確保一組常用的 ACL 規則會套用的 tooall Vm 子網路的一部分：

![套用 Nsg toonetwork 介面或子網路](./media/virtual-machines-common-endpoints-in-resource-manager/apply-nsg-to-resources.png)

網路安全性群組 hello hello 行為不會變更根據指派 tooa 子網路或網路介面。 常見的部署案例都有的 hello 網路安全性群組指派 tooa 子網路 tooensure 相容性的所有 Vm 附加的 toothat 子網路。 如需詳細資訊，請參閱[套用網路安全性群組 tooresources](../articles/virtual-network/virtual-networks-nsg.md#associating-nsgs)。

## <a name="default-behavior-of-network-security-groups"></a>網路安全性群組的預設行為
根據如何及何時建立您的網路安全性群組，預設的規則可能會建立 TCP 連接埠 3389 上的 Windows Vm toopermit RDP 存取。 Linux VM 的預設規則會在 TCP 連接埠 22 上允許 SSH 存取。 Hello 下列條件下會建立這些自動的 ACL 規則：

* 如果您建立透過 hello 入口網站的 Windows VM，並接受 hello 預設動作 toocreate 網路安全性群組，會建立 ACL 規則 tooallow TCP 連接埠 3389 (RDP)。
* 如果您建立 Linux VM 透過 hello 入口網站，並接受 hello 預設動作 toocreate 網路安全性群組，會建立 ACL 規則 tooallow TCP 連接埠 22 (SSH)。

在所有其他情況下，不會建立這些預設 ACL 規則。 您無法連接 tooyour VM 而不需要建立 hello 適當的 ACL 規則。 這些條件包括 hello 下列常見的動作：

* 為個別的動作 toocreating hello VM 建立透過 hello 入口網站的網路安全性群組。
* 透過 PowerShell、Azure CLI、Rest API 等以程式設計方式建立網路安全性群組。
* 建立 VM，並將其指派現有的網路安全性群組，該群組已經沒有 hello tooan 適當的 ACL 規則定義。

在所有 hello 上述情況下，您 VM tooallow hello 適當的遠端管理連線需要 toocreate ACL 規則。

## <a name="default-behavior-of-a-vm-without-a-network-security-group"></a>沒有網路安全性群組的 VM 的預設行為
您可以建立 VM，而不建立網路安全性群組。 在這些情況下，您可以連接 tooyour VM 使用 RDP 或 SSH 而不建立任何 ACL 規則。 同樣地，如果您在連接埠 80 上安裝 Web 服務，該服務會自動可從遠端存取。 hello VM 已開啟的所有連接埠。

> [!NOTE]
> 您仍然需要 toohave 公用 IP 位址指派 tooa VM 順序進行任何遠端連接。 沒有 hello 子網路或網路介面的網路安全性群組不會公開 hello VM tooany 外部流量。 建立 VM，以透過 hello 入口網站時，hello 預設動作是 toocreate 新的公用 IP。 對於建立 VM 的所有其他形式，例如 PowerShell、Azure CLI 或 Resource Manager 範本，除非明確要求，否則不會自動建立公用 IP。 hello 預設動作，透過 hello 入口網站也是 toocreate 網路安全性群組。 預設動作表示您不應該在沒有網路篩選器就緒的公開 VM 情況下結束。

## <a name="understanding-load-balancers-and-nat-rules"></a>了解負載平衡器及 NAT 規則
在 hello 傳統部署模型中，您可以建立端點，也會執行連接埠轉送。 當您建立 VM 在 hello 傳統部署模型時，會自動建立 RDP 或 SSH 的 ACL 規則。 這些規則會公開 TCP 連接埠 3389 或 TCP 連接埠 22 分別 toohello 外部世界。 相反地，高價值的 TCP 連接埠會公開對應 toohello 適當的內部連接埠。 您也可以建立您自己的 ACL 規則，以類似的方式，例如公開 web 伺服器上的 TCP 連接埠 4280 toohello 外部世界。 您可以看到這些 ACL 規則和連接埠對應 hello hello 傳統入口網站中的下列螢幕擷取畫面中：

![使用傳統端點的連接埠轉送](./media/virtual-machines-common-endpoints-in-resource-manager/classic-endpoints-port-forwarding.png)

利用網路安全性群組，該連接埠轉送功能是由負載平衡器處理。 如需詳細資訊，請參閱 [Azure 中的負載平衡器](../articles/load-balancer/load-balancer-overview.md)。 hello 下列範例顯示具有負載平衡器 NAT 規則 tooperform 連接埠轉送 TCP 連接埠 4222 toohello 內部 TCP 通訊埠 22 VM:

![連接埠轉送的負載平衡器 NAT 規則](./media/virtual-machines-common-endpoints-in-resource-manager/load-balancer-nat-rules.png)

> [!NOTE]
> 當您實作負載平衡器時，您通常不指派 hello VM 本身的公用 IP 位址。 相反地，hello 負載平衡器有公用的 IP 位址指派 tooit。 您仍然需要 toocreate 您的網路安全性群組和 ACL 規則 toodefine hello 流量的流量進出您的 VM。 hello 負載平衡器 NAT 規則是只要 toodefine 透過 hello 負載平衡器和他們取得分散 hello 後端 Vm 允許哪些連接埠。 因此，您需要透過 hello 負載平衡器的流量 tooflow toocreate NAT 規則。 tooallow hello 流量 tooreach hello VM、 建立網路安全性群組 ACL 規則。
