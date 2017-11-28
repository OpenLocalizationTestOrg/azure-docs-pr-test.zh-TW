<span data-ttu-id="10840-101">開始這項設定之前，您必須登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="10840-101">Before beginning this configuration, you must log in to your Azure account.</span></span> <span data-ttu-id="10840-102">cmdlet 會提示您 Azure 帳戶的登入認證。</span><span class="sxs-lookup"><span data-stu-id="10840-102">The cmdlet prompts you for the login credentials for your Azure account.</span></span> <span data-ttu-id="10840-103">登入之後，它會下載您的帳戶設定以供 Azure PowerShell 使用。</span><span class="sxs-lookup"><span data-stu-id="10840-103">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span></span> <span data-ttu-id="10840-104">如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與 Resource Manager](../articles/powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="10840-104">For more information, see [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="10840-105">若要登入，請以提高的權限開啟 PowerShell 主控台並連線至您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="10840-105">To log in, open your PowerShell console with elevated privileges, and connect to your account.</span></span> <span data-ttu-id="10840-106">使用下列範例來協助您連接：</span><span class="sxs-lookup"><span data-stu-id="10840-106">Use the following example to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="10840-107">如果您有多個 Azure 訂用帳戶，請檢查帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="10840-107">If you have multiple Azure subscriptions, check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="10840-108">指定您要使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="10840-108">Specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```