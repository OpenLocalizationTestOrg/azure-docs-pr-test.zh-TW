<!--author=SharS last changed: 11/18/16-->

#### <a name="tooinstall-regular-updates-via-windows-powershell-for-storsimple"></a>透過 Windows PowerShell for StorSimple tooinstall 定期更新
1. 開啟 hello 裝置序列主控台，然後選取選項 1，**登入的完整存取**。 型別 hello 密碼。 hello 預設密碼為*Password1*。 
2. 在 hello 命令提示字元中輸入：
   
     `Get-HcsUpdateAvailability`
   
    如果有可用更新時，是否 hello 更新具有干擾性或非干擾性，將會通知您。
3. 在 hello 命令提示字元中輸入：
   
     `Start-HcsUpdate`
   
    hello 更新程序將會啟動。

> [!IMPORTANT]
> * 此命令只會套用 tooregular 更新。 您只需在某一個控制站上執行此命令，就會更新這兩個控制站。 
> * 您可能會發現控制器容錯移轉期間 hello 更新程序。不過，hello 容錯移轉不會影響系統可用性或運作。
> 
> 

