### <a name="troubleshoot-azure-diagnostics"></a><span data-ttu-id="cc986-101">針對 Azure 診斷進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="cc986-101">Troubleshoot Azure Diagnostics</span></span>

<span data-ttu-id="cc986-102">如果您收到下列錯誤訊息的 hello，hello Microsoft.insights 資源提供者未註冊：</span><span class="sxs-lookup"><span data-stu-id="cc986-102">If you receive hello following error message, hello Microsoft.insights resource provider is not registered:</span></span>

`Failed tooupdate diagnostics for 'resource'. {"code":"Forbidden","message":"Please register hello subscription 'subscription id' with Microsoft.Insights."}`

<span data-ttu-id="cc986-103">tooregister hello 資源提供者，執行下列步驟在 hello Azure 入口網站中的 hello:</span><span class="sxs-lookup"><span data-stu-id="cc986-103">tooregister hello resource provider, perform hello following steps in hello Azure portal:</span></span>

1.  <span data-ttu-id="cc986-104">Hello hello 左側瀏覽窗格中按一下*訂用帳戶*</span><span class="sxs-lookup"><span data-stu-id="cc986-104">In hello navigation pane on hello left, click *Subscriptions*</span></span>
2.  <span data-ttu-id="cc986-105">選取識別 hello 錯誤訊息中的 hello 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cc986-105">Select hello subscription identified in hello error message</span></span>
3.  <span data-ttu-id="cc986-106">按一下 [資源提供者]</span><span class="sxs-lookup"><span data-stu-id="cc986-106">Click *Resource Providers*</span></span>
4.  <span data-ttu-id="cc986-107">尋找 hello *Microsoft.insights*提供者</span><span class="sxs-lookup"><span data-stu-id="cc986-107">Find hello *Microsoft.insights* provider</span></span>
5.  <span data-ttu-id="cc986-108">按一下 hello*註冊*連結</span><span class="sxs-lookup"><span data-stu-id="cc986-108">Click hello *Register* link</span></span>

![註冊 microsoft.insights 資源提供者](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

<span data-ttu-id="cc986-110">一次 hello *Microsoft.insights*資源提供者註冊，請重試設定診斷。</span><span class="sxs-lookup"><span data-stu-id="cc986-110">Once hello *Microsoft.insights* resource provider is registered, retry configuring diagnostics.</span></span>


<span data-ttu-id="cc986-111">在 PowerShell 中，如果您收到下列錯誤訊息： hello 您您的 PowerShell 版本需要 tooupdate:</span><span class="sxs-lookup"><span data-stu-id="cc986-111">In PowerShell, if you receive hello following error message, you need tooupdate your version of PowerShell:</span></span>

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

<span data-ttu-id="cc986-112">更新您的 PowerShell toohello 版本年 11 月 2016 (v2.3.0)，或更新版本中，釋放使用中 hello hello 指示[開始使用 Azure PowerShell cmdlet](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)發行項。</span><span class="sxs-lookup"><span data-stu-id="cc986-112">Update your version of PowerShell toohello November 2016 (v2.3.0), or later, release using hello instructions in hello [Get started with Azure PowerShell cmdlets](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) article.</span></span>
