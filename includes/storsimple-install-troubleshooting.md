<!--author=alkohli last changed: 03/17/16-->

## <a name="troubleshooting-update-failures"></a>更新失敗的疑難排解
**如果您看到通知，hello 升級前檢查失敗？**

如果前置檢查失敗，請確定您具有查看在 hello hello 頁面底部的 hello 詳細的通知列。 這會提供指引 toowhich 前置檢查失敗。 hello 下圖顯示這類通知會顯示執行個體。 在此情況下，hello 控制器健康情況檢查和硬體元件健全狀況檢查已失敗。 在 hello**硬體狀態**區段中，您所見，兩者**控制器 0**和**控制器 1**元件需要注意。

  ![前置檢查失敗](./media/storsimple-install-troubleshooting/HCS_PreUpdateCheckFailed-include.png)

您必須確定兩個控制器都處於狀況良好和線上 toomake。 您也需要 toomake 確定 hello StorSimple 裝置中的所有 hello 硬體元件的都顯示 toobe 狀況良好 hello 維護 頁面上。 然後，您可以嘗試 tooinstall 更新。 如果您不能 toofix hello 硬體元件發生問題，您會取得後續步驟需要 toocontact Microsoft 支援服務。

**如果您收到 「 無法安裝的更新 」 的錯誤訊息，並 hello 建議是 toorefer toohello 更新疑難排解指南 toodetermine hello 失敗原因的 hello？**

可能的原因可能是您沒有連線 toohello Microsoft Update servers。 這是需要 toobe 執行手動檢查。 如果您失去連線能力 toohello 更新伺服器，更新作業會失敗。 您可以執行 hello hello 您的 StorSimple 裝置的 Windows PowerShell 介面中的下列 cmdlet 來檢查 hello 連線：

 `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter>`

兩個控制器上執行 hello 指令程式。

如果您已確認 hello 連線存在，而且您繼續 toosee 此問題，請連絡 Microsoft 支援以取得後續步驟。

**如果更新您的裝置 tooUpdate 4 時，請參閱更新失敗，這兩個 hello 控制站都執行更新 4 嗎？**

如果兩個 hello 控制器執行 hello 相同的軟體版本，而且如果沒有更新失敗，請從更新 4，，hello 控制站不會進入修復模式。 可能會發生這種情況下，如果 hello 裝置軟體 hotfix （第 1 個訂單更新） 會套用的 tooboth hello 控制站，但其他 hotfix 已成功 （第 2 個順序和第 3 個訂單） 是尚未套用 toobe。 從更新 4，hello 控制站將會進入修復模式才 hello 兩個控制器都在執行不同的軟體版本。 

如果 hello 使用者會看到更新失敗，這兩個控制器都在執行更新 4 時，我們建議它們稍候幾分鐘，然後重試更新。 如果 hello 重試不成功，它們應該連絡 Microsoft 支援。
