### <a name="troubleshoot-azure-diagnostics"></a><span data-ttu-id="2f2cd-101">針對 Azure 診斷進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="2f2cd-101">Troubleshoot Azure Diagnostics</span></span>

<span data-ttu-id="2f2cd-102">如果您收到下列錯誤訊息，則未註冊 Microsoft.insights 資源提供者︰</span><span class="sxs-lookup"><span data-stu-id="2f2cd-102">If you receive the following error message, the Microsoft.insights resource provider is not registered:</span></span>

`Failed to update diagnostics for 'resource'. {"code":"Forbidden","message":"Please register the subscription 'subscription id' with Microsoft.Insights."}`

<span data-ttu-id="2f2cd-103">若要註冊資源提供者，請在 Azure 入口網站中執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2f2cd-103">To register the resource provider, perform the following steps in the Azure portal:</span></span>

1.  <span data-ttu-id="2f2cd-104">在左側的導覽窗格中，按一下 [訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="2f2cd-104">In the navigation pane on the left, click *Subscriptions*</span></span>
2.  <span data-ttu-id="2f2cd-105">選取錯誤訊息中識別的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="2f2cd-105">Select the subscription identified in the error message</span></span>
3.  <span data-ttu-id="2f2cd-106">按一下 [資源提供者]</span><span class="sxs-lookup"><span data-stu-id="2f2cd-106">Click *Resource Providers*</span></span>
4.  <span data-ttu-id="2f2cd-107">尋找 Microsoft.insights 提供者</span><span class="sxs-lookup"><span data-stu-id="2f2cd-107">Find the *Microsoft.insights* provider</span></span>
5.  <span data-ttu-id="2f2cd-108">按一下 [註冊] 連結</span><span class="sxs-lookup"><span data-stu-id="2f2cd-108">Click the *Register* link</span></span>

![註冊 microsoft.insights 資源提供者](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

<span data-ttu-id="2f2cd-110">註冊 Microsoft.insights 資源提供者後，請重試設定診斷。</span><span class="sxs-lookup"><span data-stu-id="2f2cd-110">Once the *Microsoft.insights* resource provider is registered, retry configuring diagnostics.</span></span>


<span data-ttu-id="2f2cd-111">在 PowerShell 中，如果您收到下列錯誤訊息，則需要更新 PowerShell 版本︰</span><span class="sxs-lookup"><span data-stu-id="2f2cd-111">In PowerShell, if you receive the following error message, you need to update your version of PowerShell:</span></span>

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

<span data-ttu-id="2f2cd-112">使用[開始使用 Azure PowerShell Cmdlet](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) 一文中的指示，將 PowerShell 版本更新至 2016 年 11 月 (v2.3.0) 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="2f2cd-112">Update your version of PowerShell to the November 2016 (v2.3.0), or later, release using the instructions in the [Get started with Azure PowerShell cmdlets](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) article.</span></span>
