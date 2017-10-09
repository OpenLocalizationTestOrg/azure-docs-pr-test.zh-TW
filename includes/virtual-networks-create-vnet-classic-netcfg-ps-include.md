## <a name="how-toocreate-a-virtual-network-using-a-network-config-file-from-powershell"></a>如何 toocreate 虛擬網路使用網路組態檔從 PowerShell
Azure 會使用 xml 檔案 toodefine 所有虛擬網路可用 tooa 訂用帳戶。 您可以下載此檔案並加以編輯 toomodify 或刪除現有的虛擬網路，然後建立新的虛擬網路。 在此教學課程中，您學習如何 toodownload 這個檔案，稱為 tooas 網路組態 （或 netcfg） 檔案，並編輯 toocreate 新的虛擬網路。 toolearn 進一步了解 hello 網路組態檔，請參閱 hello [Azure 虛擬網路組態結構描述](https://msdn.microsoft.com/library/azure/jj157100.aspx)。

toocreate netcfg 檔案，使用 PowerShell，完成下列步驟的 hello 與虛擬網路：

1. 如果您從未使用過 Azure PowerShell，完成 hello 步驟 hello[如何 tooInstall 和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)發行項，然後登入 tooAzure，並選取您的訂用帳戶。
2. 從 hello Azure PowerShell 主控台中，使用 hello **Get AzureVnetConfig** cmdlet toodownload hello 網路組態檔 tooa 目錄，以執行下列命令的 hello 電腦上： 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   預期的輸出：
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. 開啟您儲存在步驟 2 使用任何 XML 或文字編輯器應用程式中的 hello 檔並尋找 hello  **<VirtualNetworkSites>** 項目。 如果您已建立網路，每個網路都會顯示為其自身的 **<VirtualNetworkSite>** 項目。
4. toocreate hello 虛擬網路所述，在此案例中，加入下列 XML 下方 hello hello  **<VirtualNetworkSites>** 項目：

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
   
5. 儲存 hello 網路組態檔。
6. 從 hello Azure PowerShell 主控台中，使用 hello**組 AzureVnetConfig** cmdlet tooupload hello 網路組態檔執行下列命令的 hello: 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   傳回的輸出︰
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   如果**OperationStatus**不*Succeeded*在 hello 傳回輸出，檢查錯誤並完成步驟 6 的 hello xml 檔案一次。

7. 從 hello Azure PowerShell 主控台中，使用 hello **Get AzureVnetSite** hello 新網路的 cmdlet tooverify 已於執行下列命令的 hello: 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   hello 傳回 （縮寫） 的輸出包含下列文字的 hello:
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
