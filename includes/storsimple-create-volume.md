<!--author=SharS last changed: 02/04/2016-->

#### <a name="toocreate-a-volume"></a>toocreate 磁碟區
1. Hello 裝置上**快速入門**頁面上，按一下**加入磁碟區**。 這樣會啟動 hello 新增磁碟區精靈。
2. 在 [hello 新增磁碟區精靈] 中，在**基本設定**，不要遵循 hello:
   
   1. 輸入磁碟區的 [名稱]  。
   2. 指定 hello**佈建的容量**以 GB 或 TB 磁碟區。 hello 磁碟區容量必須介於 1 GB 到 64 TB 之間的實體裝置。
   3. 在 hello 下拉式清單中，選取 hello**使用類型**磁碟區。 
   4. 如果您使用此磁碟區的封存資料，請選取 hello**對於不常存取的封存資料，使用此磁碟區**核取方塊。 對於所有其他使用案例，只需選取 [ **階層式磁碟區**]。 (階層式磁碟區之前稱為主要磁碟區)。
      
        ![新增磁碟區](./media/storsimple-create-volume/ScreenshotUpdate1VolumeFlow.png)
      
      1. 按一下 [hello] 箭號圖示 ![arrow-icon](./media/storsimple-create-volume/HCS_ArrowIcon-include.png) toogo toohello 下一個頁面。
3. 在 hello**其他設定**對話方塊中，新增新的存取控制記錄 (ACR):
   
   1. 提供 ACR 的 [名稱]  。
   2. 在下**iSCSI 啟動器名稱**，提供 hello iSCSI 合格名稱 (IQN) 的 Windows 主機。 如果您沒有 hello IQN，請移至太[Get hello Windows Server 主機的 IQN](#get-the-iqn-of-a-windows-server-host)。
   3. 我們建議您藉由選取 hello 啟用預設備份**啟用此磁碟區的預設備份**核取方塊。 hello 預設備份會建立原則，在 22:30 （裝置時間） 的每一天執行，並建立此磁碟區的雲端快照。
      
      > [!NOTE]
      > Hello 備份在此處啟用後，即無法回復。 您將需要 tooedit hello 磁碟區 toomodify 這項設定。
      > 
      > 
      
        ![新增磁碟區](./media/storsimple-create-volume/AddVolume2-include.png)
4. 按一下 [hello] 核取圖示 ![核取圖示](./media/storsimple-create-volume/HCS_CheckIcon-include.png). 將指定的 hello 與建立磁碟區設定。

![提供的影片](./media/storsimple-create-volume/Video_icon.png) **提供的影片**

toowatch 的視訊示範，如何 toocreate StorSimple 磁碟區，按一下[這裡](https://azure.microsoft.com/documentation/videos/create-a-storsimple-volume/)。

