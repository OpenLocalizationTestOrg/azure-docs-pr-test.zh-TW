<!--author=alkohli last changed: 07/19/2017-->

#### <a name="toocreate-a-volume"></a>toocreate 磁碟區
1. 從 hello 表格清單中的 hello 裝置 hello**裝置**刀鋒視窗中，選取您的裝置。 按一下 [+ 新增磁碟區]。

    ![新增磁碟區](./media/storsimple-8000-create-volume-u2/step5createvol1.png)

2. 在 hello**加入磁碟區**刀鋒視窗中：
   
   1. hello**選取裝置**欄位會自動填入您目前的裝置。

   2. 從 hello 下拉式清單中，選取 hello 磁碟區容器，您需要 tooadd 磁碟區。 

   3.  輸入磁碟區的 [名稱]  。 一旦建立 hello 磁碟區之後，您無法重新命名磁碟區。

   4. 在 hello 下拉式清單中，選取 hello**類型**磁碟區。 需要本機保證、低延遲，以及高效能的工作負載，請選取 [固定在本機]  磁碟區。 針對所有其他資料，請選取 [分層]  磁碟區。 如果您將此磁碟區用於封存資料，請核取 [將此磁碟區用於較不常存取的封存資料] 核取方塊。
      
       分層磁碟區已精簡佈建，而且可以快速地建立。 選取**對於不常存取的封存資料，使用此磁碟區**封存資料變更 hello 重複資料刪除區塊大小的磁碟區為目標的階層式磁碟區 too512 KB。 如果未核取此欄位，hello 對應的階層式磁碟區會使用 64 KB 的區塊大小。 較大的重複資料刪除區塊大小可讓大型的封存資料 toohello 雲端的 hello 裝置 tooexpedite hello 傳輸。
       
       本機固定磁碟區以佈建，並確保維持本機 toohello 裝置 hello hello 磁碟區上的主要資料，並不 spill toohello 雲端。  如果您建立本機固定磁碟區，hello 裝置檢查 hello 本機層上的可用空間的 hello tooprovision hello 大量要求的大小。 建立本機固定磁碟區的 hello 作業可能會溢出 hello 裝置 toohello 雲端的現有資料並採取 toocreate hello 磁碟區的 hello 時間可能較長。 hello 總時間取決於 hello 大小 hello 佈建磁碟區、 可用的網路頻寬及裝置上的 hello 資料。

   5. 指定 hello**佈建的容量**磁碟區。 記下的 hello 容量可根據選取的 hello 磁碟區類型。 hello 指定磁碟區大小不能超過 hello 可用空間。
      
       您可以佈建本機固定磁碟區總 too8.5 TB 或向上 too200 TB hello 8100 裝置上的階層式磁碟區。 您可以在較大 8600 裝置 hello，佈建本機固定磁碟區總 too22.5 TB 或分層的磁碟區總 too500 TB。 因為 hello 裝置上的本機空間是必要的 toohost hello 工作組的階層式磁碟區，建立本機固定磁碟區會影響 hello 空間可供佈建分層磁碟區。 因此，如果您建立固定在本機的磁碟區，建立分層磁碟區的可用空間就會縮小。 同樣地，如果建立為分層磁碟區時，就會降低 hello 的可用空間來建立本機固定磁碟區。
      
       8100 裝置上佈建 8.5 TB （最大容許大小） 的本機固定磁碟區，如果您已耗盡所有 hello 本機上的可用空間 hello 裝置。 您無法建立任何階層式磁碟區從該點以後 hello 裝置 toohost hello 工作集 hello 上沒有本機空間分層磁碟區。 現有的階層式磁碟區也會影響 hello 的可用空間。 例如，如果您的 8100 裝置已經有大約 106 TB 的分層磁碟區，則固定在本機的磁碟區僅只有 4 TB 的可用空間。

    6. 在 hello**連線主機**欄位中，按一下 hello 箭號。 

        ![已連線的主機](./media/storsimple-8000-create-volume-u2/step5createvol2.png)

    7. 在 hello**連線主機**刀鋒視窗中，選擇現有的 ACR，或新增 ACR，藉由執行下列步驟的 hello:

       1. 提供 ACR 的 [名稱]  。
       2. 在下**iSCSI 啟動器名稱**，提供 hello iSCSI 合格名稱 (IQN) 的 Windows 主機。 如果您沒有 hello IQN，請移至太[Get hello Windows Server 主機的 IQN](#get-the-iqn-of-a-windows-server-host)。

    9. 按一下 [建立] 。 以指定的 hello 建立磁碟區設定。

        ![Click Create](./media/storsimple-8000-create-volume-u2/step5createvol3.png)

        > [!NOTE]
        > 請注意 hello 這裡，您已建立的磁碟區未受保護。 您將需要 toocreate 和關聯的備份原則與此磁碟區 tootake 排程備份。 

