<!--author=alkohli last changed: 08/16/2016-->

#### <a name="toocreate-a-volume"></a>toocreate 磁碟區
1. Hello 裝置上**快速入門**頁面上，按一下**加入磁碟區**toostart hello 新增磁碟區精靈。
2. 在 [hello 新增磁碟區精靈] 中，在**基本設定**:
   
   1. 輸入磁碟區的 [名稱]  。
   2. 在 hello 下拉式清單中，選取 hello**使用類型**磁碟區。 需要本機保證、低延遲，以及高效能的工作負載，請選取 [固定在本機]  磁碟區。 針對所有其他資料，請選取 [分層]  磁碟區。 如果您將此磁碟區用於封存資料，請核取 [將此磁碟區用於較不常存取的封存資料] 核取方塊。 
      
       本機固定磁碟區以佈建，並確保維持本機 toohello 裝置 hello hello 磁碟區上的主要資料，並不 spill toohello 雲端。  如果您建立本機固定磁碟區，hello 裝置檢查 hello 本機層上的可用空間的 hello tooprovision hello 大量要求的大小。 建立本機固定磁碟區的 hello 作業可能會溢出 hello 裝置 toohello 雲端的現有資料並採取 toocreate hello 磁碟區的 hello 時間可能較長。 hello 總時間取決於 hello 大小 hello 佈建磁碟區、 可用的網路頻寬及裝置上的 hello 資料。 
      
       分層磁碟區已精簡佈建，而且可以快速地建立。 選取**對於不常存取的封存資料，使用此磁碟區**封存資料變更 hello 重複資料刪除區塊大小的磁碟區為目標的階層式磁碟區 too512 KB。 如果未核取此欄位，hello 對應的階層式磁碟區會使用 64 KB 的區塊大小。 較大的重複資料刪除區塊大小可讓大型的封存資料 toohello 雲端的 hello 裝置 tooexpedite hello 傳輸。
   3. 指定 hello**佈建的容量**磁碟區。 記下的 hello 容量可根據選取的 hello 磁碟區類型。 hello 指定磁碟區大小不能超過 hello 可用空間。
      
       您可以佈建本機固定磁碟區總 too8.5 TB 或向上 too200 TB hello 8100 裝置上的階層式磁碟區。 您可以在較大 8600 裝置 hello，佈建本機固定磁碟區總 too22.5 TB 或分層的磁碟區總 too500 TB。 因為 hello 裝置上的本機空間是必要的 toohost hello 工作組的階層式磁碟區，建立本機固定磁碟區會影響 hello 空間可供佈建分層磁碟區。 因此，如果您建立固定在本機的磁碟區，建立分層磁碟區的可用空間就會縮小。 同樣地，如果建立為分層磁碟區時，就會降低 hello 的可用空間來建立本機固定磁碟區。
      
       8100 裝置上佈建 8.5 TB （最大容許大小） 的本機固定磁碟區，如果您已耗盡所有 hello 本機上的可用空間 hello 裝置。 您不會無法 toocreate 從任何階層式磁碟區及更新版本有點是沒有 hello 裝置 toohost hello 工作集 hello 上的本機空間分層磁碟區。 現有的階層式磁碟區也會影響 hello 的可用空間。 例如，如果您的 8100 裝置已經有大約 106 TB 的分層磁碟區，則固定在本機的磁碟區僅只有 4 TB 的可用空間。
      
       hello 下列影像顯示 hello**基本設定**本機固定磁碟區 對話方塊。
      
        ![新增本機磁碟區](./media/storsimple-create-volume-u2/add-local-volume-include.png)
      
       hello 下列影像顯示 hello**基本設定**階層式磁碟區 對話方塊。
      
        ![新增本機磁碟區](./media/storsimple-create-volume-u2/add-tiered-volume-include.png)
   
   1. 按一下 [hello] 箭號圖示 ![arrow-icon](./media/storsimple-create-volume-u2/HCS_ArrowIcon-include.png) toogo toohello 下一個頁面。
3. 在 hello**其他設定**對話方塊中，新增新的存取控制記錄 (ACR):
   
   1. 提供 ACR 的 [名稱]  。
   2. 在下**iSCSI 啟動器名稱**，提供 hello iSCSI 合格名稱 (IQN) 的 Windows 主機。 如果您沒有 hello IQN，請移至太[Get hello Windows Server 主機的 IQN](#get-the-iqn-of-a-windows-server-host)。
   3. 在下**此磁碟區的預設備份？**，選取 hello**啟用**核取方塊。 hello 預設備份會建立在 22:30 （裝置時間） 的每一天執行，並建立此磁碟區的雲端快照的原則。
      
      > [!NOTE]
      > Hello 備份在此處啟用後，即無法回復。 您需要 tooedit hello 磁碟區 toomodify 這項設定。
      > 
      > 
      
      ![新增磁碟區](./media/storsimple-create-volume-u2/AddVolumeAdditionalSettings1.png)
4. 按一下 [hello] 核取圖示 ![核取圖示](./media/storsimple-create-volume-u2/HCS_CheckIcon-include.png). 以指定的 hello 建立磁碟區設定。

