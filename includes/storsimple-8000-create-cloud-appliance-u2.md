#### <a name="toocreate-a-cloud-appliance"></a>toocreate 雲端應用裝置

1. 在 hello Azure 入口網站，移 toohello **StorSimple 裝置管理員**服務。
2. 移 toohello**裝置**刀鋒視窗。 在 hello 命令列在 hello 服務摘要] 刀鋒視窗中，按一下 [**建立雲端應用裝置**。
    ![StorSimple 建立雲端設備](./media/storsimple-8000-create-cloud-appliance-u2/sca-create1.png)
3. 在 hello**建立雲端應用裝置**刀鋒視窗中，指定下列詳細資料的 hello。
   
    ![StorSimple 建立雲端設備](./media/storsimple-8000-create-cloud-appliance-u2/sca-create2m.png)
   
   1. **名稱** - 雲端設備的唯一名稱。
   2. **模型**-選擇 hello 雲端應用裝置 hello 模型。 8010 裝置提供 30 TB 的標準儲存體，而 8020 提供 64 TB 的進階儲存體。 指定從備份 8010 toodeploy 項目層級抓取狀況。 選取 8020 toodeploy 高效能、 低延遲工作負載，或做為災害復原的次要裝置。
   3. **版本**-選擇 hello 雲端應用裝置 hello 版本。 hello 版本對應 toohello 版本是使用的 toocreate hello 雲端應用裝置 hello 虛擬磁碟映像。 指定的 hello 雲端 hello 版本應用裝置會決定哪一個實體裝置容錯移轉，或複製，請務必建立 hello 雲端應用裝置的適當版本。
   4. **虛擬網路**– 指定您想 toouse 要與這個雲端應用裝置的虛擬網路。 如果使用進階儲存體，您必須選取支援以 hello 高階儲存體帳戶的虛擬網路。 灰色 hello 不支援的虛擬網路在 hello 下拉式清單中。 如果您選取不支援的虛擬網路，系統會警告您。
   5. **子網路**-根據選取的 hello 虛擬網路，hello 下拉式清單會顯示 hello 相關聯的子網路。 將指定的子網路 tooyour 雲端應用裝置。
   6. **儲存體帳戶**– 在佈建期間選取 hello 雲端應用裝置的儲存體帳戶 toohold hello 映像。 這個儲存體帳戶應該在 hello 與 hello 雲端應用裝置和虛擬網路相同的區域。 它不應儲存資料的實體 hello 或 hello 雲端應用裝置。 根據預設，會就此用途建立新的儲存體帳戶。 不過，如果您知道您已經是適合此用途的儲存體帳戶，您可以從清單中選取 hello。 如果建立高階的雲端應用裝置，hello 下拉式清單中只會顯示高階儲存體帳戶。
      
      > [!NOTE]
      > hello 雲端應用裝置，只可與 hello Azure 儲存體帳戶。
    
   7. 選取您了解，儲存在 hello 雲端應用裝置上的 hello 資料裝載於 Microsoft 資料中心的 hello 核取方塊 tooindicate。
       * 若您只使用實體裝置，加密金鑰就會與裝置放在一起。因此，Microsoft 無法將它解密。

       * 當您使用雲端應用裝置時，hello 加密金鑰和 hello 解密金鑰會儲存在 Microsoft Azure。 如需詳細資訊，請參閱[使用雲端設備的安全性考量](../articles/storsimple/storsimple-security.md#storsimple-virtual-device-security)。
   8. 按一下**建立**tooprovision hello 雲端應用裝置。 hello 裝置可能需要約 30 分鐘 toobe 佈建。 已成功建立 hello 雲端應用裝置時，會通知您。 移 tooDevices 刀鋒視窗中，以及裝置 hello 清單重新整理 toodisplay hello 雲端應用裝置。 hello 應用裝置 hello 狀態是**已 tooset 準備註冊**。
      
      ![設定 StorSimple 雲端應用裝置準備好 tooset](./media/storsimple-8000-create-cloud-appliance-u2/sca-create3.png)

