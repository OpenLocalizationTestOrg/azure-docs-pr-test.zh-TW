#### <a name="toocreate-a-virtual-device"></a>toocreate 虛擬裝置
1. 在 hello Azure 入口網站，移 toohello **StorSimple Manager**服務。
2. 移 toohello**裝置**頁面。 按一下**建立虛擬裝置**底部 hello hello**裝置**頁面。
3. 在 hello**對話方塊中建立虛擬裝置**，指定下列詳細資料的 hello。
   
    ![StorSimple 建立虛擬裝置](./media/storsimple-create-virtual-device-u2/CreatePremiumsva1.png)
   
   1. **名稱** - 虛擬裝置的唯一名稱。
   2. **模型**-選擇 hello hello 虛擬裝置的模型。 只有當您執行 Update 2 或更新版本時，此欄位才會出現。 8010 裝置型號提供 30 TB 的標準儲存體， 而 8020 提供 64 TB 的進階儲存體。 指定 8010
   3. 從備份 toodeploy 項目層級抓取狀況。 選取 8020 toodeploy 高效能、 低延遲工作負載，或做為災害復原的次要裝置。
   4. **版本**-選擇 hello 虛擬裝置 hello 版本。 如果選取 8020 裝置型號，然後 hello 版本欄位不會提供 toohello 使用者。 這個選項不存在如果所有 hello 實體裝置向此服務會執行 Update 1 （或更新版本）。 此欄位會顯示只有前更新 1 的混用，而且 Update 1 實體裝置向 hello 相同服務。 指定的 hello hello 虛擬裝置的版本，可決定哪些實體裝置，您可以容錯移轉或再製從，很重要，您會建立適當版本的 hello 虛擬裝置。 選取：
      
      * 如果您將容錯移轉或從執行 Update 0.3 或更舊版本的實體裝置進行 DR，則為 Update 0.3 版本。 
      * 如果您從執行 Update 1 (或更新版本) 的實體裝置容錯移轉或複製，則為 Update 1 版本。 
   5. **虛擬網路**– 指定您想 toouse 要與此虛擬裝置的虛擬網路。 如果使用進階儲存體 (Update 2 或更新版本)，您必須選取支援以 hello 高階儲存體帳戶的虛擬網路。 hello 不支援的虛擬網路將灰色 hello 下拉式清單中。 如果您選取不支援的虛擬網路，系統會警告您。 
   6. **建立虛擬裝置的儲存體帳戶**– 在佈建期間選取 hello 虛擬裝置的儲存體帳戶 toohold hello 映像。 這個儲存體帳戶應該在 hello 與 hello 虛擬裝置和虛擬網路相同的區域。 它不應儲存資料實體的 hello 或 hello 虛擬裝置。 根據預設，將基於此用途建立新的儲存體帳戶。 不過，如果您知道您已經是適合此用途的儲存體帳戶，您可以從清單中選取 hello。 如果建立高階虛擬裝置，hello 下拉式清單中只會顯示高階儲存體帳戶。 
      
      > [!NOTE]
      > hello Azure 儲存體帳戶只能處理 hello 虛擬裝置。 Hello StorSimple 虛擬裝置不支援其他雲端服務提供者例如 Amazon、 HP、 以及 OpenStack （也就被支援 hello 實體裝置）。
      > 
      > 
   7. 按一下您了解，hello 資料儲存在 hello 虛擬裝置將託管於 Microsoft 資料中心的 hello 核取記號 tooindicate。 若您只使用實體裝置，加密金鑰就會與裝置放在一起。因此，Microsoft 無法將它解密。 
      
       當您使用虛擬裝置時，hello 加密金鑰和 hello 解密金鑰會儲存在 Microsoft Azure。 如需詳細資訊，請參閱[使用虛擬裝置的安全性考量](../articles/storsimple/storsimple-security.md#storsimple-virtual-device-security)。
   8. 按一下 hello 核取圖示 toocreate hello 虛擬裝置。 hello 裝置可能需要約 30 分鐘 toobe 佈建。
      
      ![StorSimple 虛擬裝置建立中階段](./media/storsimple-create-virtual-device-u2/StorSimple_VirtualDeviceCreating1M.png)

