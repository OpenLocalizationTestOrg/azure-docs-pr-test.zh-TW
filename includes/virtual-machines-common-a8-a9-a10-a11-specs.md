

## <a name="deployment-considerations"></a>部署考量
* **Azure 訂用帳戶**– toodeploy 多個少數的大量計算執行個體，請考慮隨用隨付訂用帳戶或其他購買選項。 如果您使用 [Azure 免費帳戶](https://azure.microsoft.com/free/)，您只能使用有限數目的 Azure 計算核心。

* **價格與可用性**-只有在 hello 標準定價層中提供這些 VM 大小。 如需了解 Azure 區域中的可用性，請查看 [依區域提供的產品] (https://azure.microsoft.com/regions/services/)。 
* **核心配額**– 您可能需要 tooincrease hello 核心配額，在您的 Azure 訂閱 hello 預設值。 您的訂閱也可能會限制 hello 特定 VM 大小系列，包括 hello H 序列中，您可以部署的核心數目。 toorequest 配額增加[開啟線上客戶支援要求](../articles/azure-supportability/how-to-create-azure-support-request.md)不收費。 (預設限制會視您的訂用帳戶類別而有所不同。)
  
  > [!NOTE]
  > 如果您有大規模的容量需求，請連絡 Azure 支援。 Azure 配額為信用額度，而不是容量保證。 無論您的配額有多少，您只需針對您使用的核心付費。
  > 
  > 
* **虛擬網路**-Azure 的[虛擬網路](https://azure.microsoft.com/documentation/services/virtual-network/)是不必要的 toouse hello 大量計算執行個體。 不過，在許多部署中，您需要至少一個雲端型 Azure 虛擬網路，或站對站連線，如果您需要 tooaccess 內部資源。 需要時，請建立新的虛擬網路 toodeploy hello 執行個體。 不支援在同質群組中加入需要大量計算 Vm tooa 虛擬網路。
* **調整大小**– 由於其特殊的硬體，您也可以只調整大量計算執行個體中 hello 大小相同系列 （H 數列或需要大量計算 A 系列）。 比方說，您可以只調整一個 H 數列大小 tooanother 從 H 系列 VM。 此外，不支援從非大量計算大小 tooa 需要大量計算的大小調整大小。  
