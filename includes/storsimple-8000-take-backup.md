<!--author=alkohli last changed: 01/12/17-->

### <a name="tootake-a-backup"></a>tootake 備份

1. 移 tooyour StorSimple 裝置管理員服務。 從 hello 表格清單中的裝置，選取並按一下您的裝置，然後按一下**所有設定**。 在 hello**設定**刀鋒視窗中，跳過**設定 > 管理 > 備份原則**。

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu1.png)

2. 在 hello**備份原則**刀鋒視窗中，按一下  **+ 加入原則**。

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu2.png)

3. 在 hello**建立備份原則**刀鋒視窗中，提供包含 3 到 150 個字元，備份原則的名稱。

4. 選取備份的 hello 磁碟區 toobe。 如果您選取多個磁碟區，這些磁碟區會分組在一起 toocreate 損毀一致備份。

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu4.png)

5. 在 [新增第一個排程] 刀鋒視窗中︰

    1. 選取備份 hello 類型。 針對更快速的還原，請選取 [本機] 快照集。 針對資料復原，請選取 [雲端] 快照集。
    2. 指定分鐘、 小時、 天或週中的 hello 備份頻率。
    3. 選取保留時間。 hello 保留選項取決於 hello 備份頻率。 比方說，每日原則的 hello 保留可以指定在數週，而每月原則的保留是以月為單位。
    4. 選取 hello 啟動 hello 備份原則的日期和時間。
    5. 按一下**確定**toocreate hello 備份原則。

        ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. 按一下**建立**toostart hello 建立備份原則。 已成功建立 hello 備份原則時，會通知您。 hello 備份原則清單也會更新。
      
      ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      您現在擁有的備份原則會建立磁碟區資料的排程備份。




