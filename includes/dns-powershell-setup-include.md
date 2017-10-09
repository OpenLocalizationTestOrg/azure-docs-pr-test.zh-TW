## <a name="set-up-azure-powershell-for-azure-dns"></a>針對 Azure DNS 設定 Azure PowerShell SDK

### <a name="before-you-begin"></a>開始之前

確認您擁有 hello 開始您的組態之前，下列項目。

* Azure 訂用帳戶。 如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial/)。
* 您需要 tooinstall hello 最新版本的 hello Azure 資源管理員 PowerShell cmdlet。 如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)。

### <a name="sign-in-tooyour-azure-account"></a>Azure 帳戶登入 tooyour

開啟 PowerShell 主控台並連接 tooyour 帳戶。 如需詳細資訊，請參閱[搭配使用 PowerShell 與 Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md)。

```powershell
Login-AzureRmAccount
```

### <a name="select-hello-subscription"></a>選取 hello 訂用帳戶
 
請檢查 hello hello 帳戶的訂用帳戶。

```powershell
Get-AzureRmSubscription
```

選擇 Azure 訂用帳戶 toouse。

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a>建立資源群組

Azure Resource Manager 需要所有的資源群組指定一個位置。 此位置用於 hello 預設位置為該資源群組。 不過，因為所有的 DNS 資源全域，不是地區，hello 所選擇的資源群組位置沒有任何影響 Azure DNS。

如果您使用現有的資源群組，則可略過此步驟。

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a>註冊資源提供者

hello Azure DNS 服務是由 hello Microsoft.Network 資源提供者管理。 您的 Azure 訂用帳戶必須是已註冊的 toouse 這個資源提供者才能使用 Azure DNS。 每個訂用帳戶只需執行一次此作業。

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```