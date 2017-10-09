### <a name="troubleshoot-azure-diagnostics"></a>針對 Azure 診斷進行疑難排解

如果您收到下列錯誤訊息的 hello，hello Microsoft.insights 資源提供者未註冊：

`Failed tooupdate diagnostics for 'resource'. {"code":"Forbidden","message":"Please register hello subscription 'subscription id' with Microsoft.Insights."}`

tooregister hello 資源提供者，執行下列步驟在 hello Azure 入口網站中的 hello:

1.  Hello hello 左側瀏覽窗格中按一下*訂用帳戶*
2.  選取識別 hello 錯誤訊息中的 hello 訂用帳戶
3.  按一下 [資源提供者]
4.  尋找 hello *Microsoft.insights*提供者
5.  按一下 hello*註冊*連結

![註冊 microsoft.insights 資源提供者](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

一次 hello *Microsoft.insights*資源提供者註冊，請重試設定診斷。


在 PowerShell 中，如果您收到下列錯誤訊息： hello 您您的 PowerShell 版本需要 tooupdate:

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

更新您的 PowerShell toohello 版本年 11 月 2016 (v2.3.0)，或更新版本中，釋放使用中 hello hello 指示[開始使用 Azure PowerShell cmdlet](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)發行項。
