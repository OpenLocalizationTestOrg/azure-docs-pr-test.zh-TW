<!--author=SharS last changed: 9/17/15-->

#### <a name="toomount-initialize-and-format-a-volume"></a>toomount、 初始化及格式化磁碟區
1. 啟動 hello Microsoft iSCSI 啟動器。
2. 在 hello **iSCSI 啟動器屬性**視窗的 hello**探索**索引標籤上，按一下 **探索入口網站**。
3. 在 hello**探索目標入口網站**對話方塊中，提供啟用 iSCSI 的網路介面，hello IP 位址，然後按一下**確定**。 
4. 在 hello **iSCSI 啟動器屬性**視窗的 hello**目標**索引標籤上，找出 hello**探索目標**。 hello 裝置狀態應顯示為**Inactive**。
5. 選取 hello 目標裝置，然後按一下**連接**。 Hello 裝置連線之後，應該也變更 hello 狀態**Connected**。 (如需有關使用 hello Microsoft iSCSI 啟動器的詳細資訊，請參閱[安裝和設定 Microsoft iSCSI 啟動器][1])。
6. 在 Windows 主機上，按 hello Windows 爦羆坫 + X、，然後按一下**執行**。 
7. 在 [hello**執行**] 對話方塊中，輸入**Diskmgmt.msc**。 按一下**確定**，和 hello**磁碟管理**對話方塊隨即出現。 hello 右窗格會顯示 hello 磁碟區在主機上。
8. 在 hello**磁碟管理**，hello 掛接的磁碟區將會出現視窗 hello 下列圖例所示。 以滑鼠右鍵按一下探索到的 hello 磁碟區 （按一下 hello 磁碟名稱），然後按一下**線上**。
   
     ![初始化格式化磁碟區](./media/storsimple-8000-mount-initialize-format-volume/step7initializeformatvolume.png) 
9. 以滑鼠右鍵按一下 hello 磁碟區 （按一下 hello 磁碟名稱），然後按一下**初始化**。
10. tooformat 簡單磁碟區中，執行下列步驟的 hello:
    
    1. 選取 hello 磁碟區，以滑鼠右鍵按一下 （按一下 hello 右側區域），然後按一下**新增簡單磁碟區**。
    2. 在 hello 新增簡單磁碟區精靈中，指定 hello 磁碟區大小和磁碟機代號並設定 hello 磁碟區為 NTFS 檔案系統。
    3. 指定 64 KB 的配置單位大小。 此配置單位大小適用於使用 hello StorSimple 解決方案中的 hello 重複資料刪除演算法。
    4. 執行快速格式化。

<!--Link references-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx
