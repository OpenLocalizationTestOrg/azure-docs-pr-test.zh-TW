開始之前這項設定，您必須登入 tooyour Azure 帳戶。 hello cmdlet 會提示您輸入您的 Azure 帳戶的 hello 登入認證。 登入之後，它會下載您的帳戶設定，這樣就可以使用 tooAzure PowerShell。 如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與 Resource Manager](../articles/powershell-azure-resource-manager.md)。

toolog 中，使用提高的權限開啟 PowerShell 主控台，並連接 tooyour 帳戶。 使用下列範例 toohelp 您連接的 hello:

```powershell
Login-AzureRmAccount
```

如果您有多個 Azure 訂用帳戶，請檢查 hello hello 帳戶的訂用帳戶。

```powershell
Get-AzureRmSubscription
```

指定您想 toouse hello 訂用帳戶。

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```