<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a>tooinstall 透過 Windows PowerShell for StorSimple 的維護模式 hotfix
> [!IMPORTANT]
> 在維護模式中，您在一個控制器上第一次需要 tooapply hello hotfix，然後在 hello 另一個控制器。
> 
> 

1. 將 hello 裝置放入維護模式。 請參閱[步驟 2： 輸入的維護模式](../articles/storsimple/storsimple-update-device.md#step2)如需有關指示 tooenter 維護模式。
2. 型別 tooapply hello hotfix:
   
     `Start-HcsHotfix` 
3. 出現提示時，提供 hello 路徑 toohello 網路共用的資料夾，其中包含 hello hotfix 檔案。
4. 系統將提示您進行確認。 型別**Y** tooproceed hello hotfix 安裝。
5. 之後您 hello hotfix 控制器上套用一個，登入 toohello 另一個控制器。 如同 hello 先前控制站，請套用 hello hotfix。
6. 套用 hello hotfixes 之後，請退出維護模式。 如需相關指示，請參閱[步驟 4：結束維護模式](../articles/storsimple/storsimple-update-device.md#step4)。

