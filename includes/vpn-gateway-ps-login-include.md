<span data-ttu-id="eaa86-101">開始之前這項設定，您必須登入 tooyour Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="eaa86-101">Before beginning this configuration, you must log in tooyour Azure account.</span></span> <span data-ttu-id="eaa86-102">hello cmdlet 會提示您輸入您的 Azure 帳戶的 hello 登入認證。</span><span class="sxs-lookup"><span data-stu-id="eaa86-102">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="eaa86-103">登入之後，它會下載您的帳戶設定，這樣就可以使用 tooAzure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="eaa86-103">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span> <span data-ttu-id="eaa86-104">如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與 Resource Manager](../articles/powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="eaa86-104">For more information, see [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="eaa86-105">toolog 中，使用提高的權限開啟 PowerShell 主控台，並連接 tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="eaa86-105">toolog in, open your PowerShell console with elevated privileges, and connect tooyour account.</span></span> <span data-ttu-id="eaa86-106">使用下列範例 toohelp 您連接的 hello:</span><span class="sxs-lookup"><span data-stu-id="eaa86-106">Use hello following example toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="eaa86-107">如果您有多個 Azure 訂用帳戶，請檢查 hello hello 帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="eaa86-107">If you have multiple Azure subscriptions, check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="eaa86-108">指定您想 toouse hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="eaa86-108">Specify hello subscription that you want toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```