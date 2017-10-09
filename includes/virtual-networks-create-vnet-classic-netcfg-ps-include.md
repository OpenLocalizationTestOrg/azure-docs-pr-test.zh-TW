## <a name="how-toocreate-a-virtual-network-using-a-network-config-file-from-powershell"></a><span data-ttu-id="5094a-101">如何 toocreate 虛擬網路使用網路組態檔從 PowerShell</span><span class="sxs-lookup"><span data-stu-id="5094a-101">How toocreate a virtual network using a network config file from PowerShell</span></span>
<span data-ttu-id="5094a-102">Azure 會使用 xml 檔案 toodefine 所有虛擬網路可用 tooa 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5094a-102">Azure uses an xml file toodefine all virtual networks available tooa subscription.</span></span> <span data-ttu-id="5094a-103">您可以下載此檔案並加以編輯 toomodify 或刪除現有的虛擬網路，然後建立新的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5094a-103">You can download this file, edit it toomodify or delete existing virtual networks, and create new virtual networks.</span></span> <span data-ttu-id="5094a-104">在此教學課程中，您學習如何 toodownload 這個檔案，稱為 tooas 網路組態 （或 netcfg） 檔案，並編輯 toocreate 新的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5094a-104">In this tutorial, you learn how toodownload this file, referred tooas network configuration (or netcfg) file, and edit it toocreate a new virtual network.</span></span> <span data-ttu-id="5094a-105">toolearn 進一步了解 hello 網路組態檔，請參閱 hello [Azure 虛擬網路組態結構描述](https://msdn.microsoft.com/library/azure/jj157100.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5094a-105">toolearn more about hello network configuration file, see hello [Azure virtual network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

<span data-ttu-id="5094a-106">toocreate netcfg 檔案，使用 PowerShell，完成下列步驟的 hello 與虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="5094a-106">toocreate a virtual network with a netcfg file using PowerShell, complete hello following steps:</span></span>

1. <span data-ttu-id="5094a-107">如果您從未使用過 Azure PowerShell，完成 hello 步驟 hello[如何 tooInstall 和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)發行項，然後登入 tooAzure，並選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5094a-107">If you have never used Azure PowerShell, complete hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article, then sign in tooAzure and select your subscription.</span></span>
2. <span data-ttu-id="5094a-108">從 hello Azure PowerShell 主控台中，使用 hello **Get AzureVnetConfig** cmdlet toodownload hello 網路組態檔 tooa 目錄，以執行下列命令的 hello 電腦上：</span><span class="sxs-lookup"><span data-stu-id="5094a-108">From hello Azure PowerShell console, use hello **Get-AzureVnetConfig** cmdlet toodownload hello network configuration file tooa directory on your computer by running hello following command:</span></span> 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="5094a-109">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="5094a-109">Expected output:</span></span>
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. <span data-ttu-id="5094a-110">開啟您儲存在步驟 2 使用任何 XML 或文字編輯器應用程式中的 hello 檔並尋找 hello  **<VirtualNetworkSites>** 項目。</span><span class="sxs-lookup"><span data-stu-id="5094a-110">Open hello file you saved in step 2 using any XML or text editor application, and look for hello **<VirtualNetworkSites>** element.</span></span> <span data-ttu-id="5094a-111">如果您已建立網路，每個網路都會顯示為其自身的 **<VirtualNetworkSite>** 項目。</span><span class="sxs-lookup"><span data-stu-id="5094a-111">If you have any networks already created, each network is displayed as its own **<VirtualNetworkSite>** element.</span></span>
4. <span data-ttu-id="5094a-112">toocreate hello 虛擬網路所述，在此案例中，加入下列 XML 下方 hello hello  **<VirtualNetworkSites>** 項目：</span><span class="sxs-lookup"><span data-stu-id="5094a-112">toocreate hello virtual network described in this scenario, add hello following XML just under hello **<VirtualNetworkSites>** element:</span></span>

   ```xml
        <VirtualNetworkSite name="TestVNet" Location="East US">
          <AddressSpace>
            <AddressPrefix>192.168.0.0/16</AddressPrefix>
          </AddressSpace>
          <Subnets>
            <Subnet name="FrontEnd">
              <AddressPrefix>192.168.1.0/24</AddressPrefix>
            </Subnet>
            <Subnet name="BackEnd">
              <AddressPrefix>192.168.2.0/24</AddressPrefix>
            </Subnet>
          </Subnets>
        </VirtualNetworkSite>
   ```
   
5. <span data-ttu-id="5094a-113">儲存 hello 網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="5094a-113">Save hello network configuration file.</span></span>
6. <span data-ttu-id="5094a-114">從 hello Azure PowerShell 主控台中，使用 hello**組 AzureVnetConfig** cmdlet tooupload hello 網路組態檔執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="5094a-114">From hello Azure PowerShell console, use hello **Set-AzureVnetConfig** cmdlet tooupload hello network configuration file by running hello following command:</span></span> 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="5094a-115">傳回的輸出︰</span><span class="sxs-lookup"><span data-stu-id="5094a-115">Returned output:</span></span>
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   <span data-ttu-id="5094a-116">如果**OperationStatus**不*Succeeded*在 hello 傳回輸出，檢查錯誤並完成步驟 6 的 hello xml 檔案一次。</span><span class="sxs-lookup"><span data-stu-id="5094a-116">If **OperationStatus** is not *Succeeded* in hello returned output, check hello xml file for errors and complete step 6 again.</span></span>

7. <span data-ttu-id="5094a-117">從 hello Azure PowerShell 主控台中，使用 hello **Get AzureVnetSite** hello 新網路的 cmdlet tooverify 已於執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="5094a-117">From hello Azure PowerShell console, use hello **Get-AzureVnetSite** cmdlet tooverify that hello new network was added by running hello following command:</span></span> 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   <span data-ttu-id="5094a-118">hello 傳回 （縮寫） 的輸出包含下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="5094a-118">hello returned (abbreviated) output includes hello following text:</span></span>
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
