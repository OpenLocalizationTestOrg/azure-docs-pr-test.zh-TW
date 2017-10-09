<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-regular-hotfixes-via-windows-powershell-for-storsimple"></a>透過 Windows PowerShell for StorSimple tooinstall 定期 hotfix
1. Toohello 裝置序列主控台連線。 如需詳細資訊，請參閱[步驟 1: toohello 序列主控台連接](../articles/storsimple/storsimple-update-device.md#step1)。
2. 在 hello 序列主控台功能表中，選取選項 1，**登入的完整存取**。 型別 hello 密碼。 hello 預設密碼為**Password1**。
3. 在 hello 命令提示字元中輸入：
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > 此命令適用於僅 tooregular hotfix。 您只需在某一個控制站上執行此命令，就會更新這兩個控制站。
    > 您可能會發現控制器容錯移轉期間 hello 更新程序。不過，hello 容錯移轉不會影響系統可用性或運作。

4. 出現提示時，提供 hello 路徑 toohello 網路共用的資料夾，其中包含 hello hotfix 檔案。
5. 系統將提示您進行確認。 型別**Y** tooproceed hello hotfix 安裝。

