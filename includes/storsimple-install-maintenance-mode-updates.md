<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>透過 Windows PowerShell for StorSimple tooinstall 維護模式更新
1. 如果還沒有這麼做，請存取 hello 裝置序列主控台，然後選取選項 1，**登入的完整存取**。 
2. 型別 hello 密碼。 hello 預設密碼為**Password1**。
3. 在 hello 命令提示字元中輸入：
   
     `Get-HcsUpdateAvailability` 
4. 如果有可用更新時，是否 hello 更新具有干擾性或非干擾性，將會通知您。 tooapply 更新具有干擾性，您會需要 tooput hello 裝置進入維護模式。 如需相關指示，請參閱[步驟 2：進入維護模式](../articles/storsimple/storsimple-update-device.md#step2)。
5. 當您的裝置處於維護模式，在 hello 命令提示字元中輸入：`Start-HcsUpdate`
6. 系統將提示您進行確認。 確認 hello 更新之後，它們將會安裝在您目前正在存取的 hello 控制站上。 Hello 更新安裝之後，hello 控制器將會重新啟動。 
7. 監視 hello 狀態更新。 輸入：
   
    `Get-HcsUpdateStatus`
   
    如果 hello`RunInProgress`是`True`，hello 更新是仍在進行中。 如果`RunInProgress`是`False`，它會指出該 hello 更新已完成。  
8. 當 hello 目前的控制器上安裝 hello 更新並已重新啟動時，連接 toohello 另一個控制器，然後執行步驟 1 到 6。
9. 更新這兩個控制站之後，結束維護模式。 如需相關指示，請參閱[步驟 4：結束維護模式](../articles/storsimple/storsimple-update-device.md#step4)。

