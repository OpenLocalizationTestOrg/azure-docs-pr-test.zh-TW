<!--author=alkohli last changed: 9/17/15-->

### <a name="tootake-a-backup"></a>tootake 備份
1. Hello 裝置上**快速入門**頁面上，按一下**新增備份原則**。 這樣會啟動 hello 新增備份原則精靈。 
2. 在 hello**定義備份原則**頁面：
   
   1. 為備份原則提供包含 3 到 150 個字元的名稱。
   2. 選取備份的 hello 磁碟區 toobe。 如果您選取多個磁碟區，這些磁碟區將會分組在一起 toocreate 損毀一致備份。
   3. 按一下 [hello] 箭號圖示 ![arrow-icon](./media/storsimple-take-backup/HCS_ArrowIcon-include.png)。 
      
      ![Add-backup-policy](./media/storsimple-take-backup/HCS_AddBackupPolicyWizard1M-include.png)
3. 在 hello**定義排程**頁面：
   
   1. 從 hello 下拉式清單中選取備份 hello 的類型。 針對更快速的還原，選取 [本機快照] 。 針對資料恢復功能，選取 [雲端快照] 。
   2. 指定分鐘、 小時、 天或週中的 hello 備份頻率。
   3. 選取保留時間。 hello 保留選項取決於 hello 備份頻率。 比方說，每日原則的 hello 保留可以指定在數週，而每月原則的保留是以月為單位。
   4. 選取 hello 啟動 hello 備份原則的日期和時間。
   5. 選取 hello**啟用**核取方塊 tooenable hello 備份原則。 
   6. 按一下 [hello] 核取圖示 ![核取圖示](./media/storsimple-take-backup/HCS_CheckIcon-include.png) toosave hello 原則。
      
      ![Add-backup-policy](./media/storsimple-take-backup/HCS_AddBackupPolicyWizard2M-include.png)
      
      您現在擁有的備份原則將會建立磁碟區資料的排程備份。

您已完成 hello 裝置組態。 

![提供的影片](./media/storsimple-take-backup/Video_icon.png) **提供的影片**

toowatch 的視訊示範，如何 tootake StorSimple 備份時，按一下[這裡](https://azure.microsoft.com/documentation/videos/take-a-storsimple-backup/)。

