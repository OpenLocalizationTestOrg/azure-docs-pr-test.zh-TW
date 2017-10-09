<!--author=SharS last changed: 12/01/15-->

### <a name="step-1-authorize-a-device-toochange-hello-service-data-encryption-key-in-hello-azure-classic-portal"></a>步驟 1： 授權裝置 toochange hello 服務資料加密金鑰在 hello Azure 傳統入口網站
一般而言，hello 裝置系統管理員會要求該 hello 服務系統管理員授權裝置 toochange 服務資料加密金鑰。 然後 hello 服務系統管理員將授權 hello 裝置 toochange hello 機碼。

Hello Azure 傳統入口網站中，會執行此步驟。 hello 服務系統管理員可以從顯示授權的合格 toobe hello 裝置的清單中選取裝置。 hello 裝置處於已授權的 toostart hello 服務資料加密金鑰變更程序。

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a>哪些裝置可以被授權 toochange 服務資料加密金鑰？
裝置必須符合下列準則，它可以是授權的 tooinitiate 服務資料加密金鑰變更之前的 hello:

* hello 裝置必須是線上 toobe 適合服務資料加密金鑰變更授權。
* 您可以授權的 hello 相同裝置一次在 30 分鐘後如果 hello 金鑰變更未起始。
* 您可以授權另一個裝置，前提 hello 金鑰變更未起始 hello 先前授權的裝置。 已獲授權 hello 新裝置之後，hello 舊裝置無法起始 hello 變更。
* Hello hello 服務資料加密金鑰變換正在進行時，您無法授權裝置。
* 某些 hello hello 服務中註冊的裝置已變換 hello 加密而其他裝置尚未時，您可以授權裝置。 在這種情況下，hello 合格裝置為 hello 已完成 hello 服務資料加密金鑰變更。

> [!NOTE]
> StorSimple 虛擬裝置不會顯示在 hello 可能是裝置清單中的 hello Azure 傳統入口網站，在權限 toostart hello 金鑰變更。
> 
> 

執行下列步驟 tooselect hello，並授權裝置 tooinitiate hello 服務資料加密金鑰變更。

#### <a name="tooauthorize-a-device-toochange-hello-key"></a>tooauthorize 裝置 toochange hello 金鑰
1. 在 hello 服務儀表板頁面上，按一下 **變更服務資料加密金鑰**。
   
    ![變更服務加密金鑰](./media/storsimple-change-data-encryption-key/HCS_ChangeServiceDataEncryptionKey-include.png)
2. 在 hello**變更服務資料加密金鑰**對話方塊方塊中，選取並授權裝置 tooinitiate hello 服務資料加密金鑰變更。 hello 下拉式清單具有所有可授權 hello 合格裝置。
3. 按一下 [hello] 核取圖示 ![核取圖示](./media/storsimple-change-data-encryption-key/HCS_CheckIcon-include.png).

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a>步驟 2： 使用 Windows PowerShell for StorSimple tooinitiate hello 服務資料加密金鑰變更
StorSimple 介面上 hello 授權 StorSimple 裝置的 hello Windows PowerShell 會執行此步驟。

> [!NOTE]
> Hello 金鑰變換完成之前，可以在 hello Azure 傳統入口網站，您的 StorSimple Manager 服務中不執行任何作業。
> 
> 

如果您使用 hello 裝置序列主控台 tooconnect toohello Windows PowerShell 介面，執行下列步驟的 hello。

#### <a name="tooinitiate-hello-service-data-encryption-key-change"></a>tooinitiate hello 服務資料加密金鑰變更
1. 選取選項 1 toolog 上，具有完整存取權。
2. 在 hello 命令提示字元中輸入：
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. Hello cmdlet 順利完成之後，您會得到新的服務資料加密金鑰。 複製並儲存此金鑰，以供此程序的步驟 3 使用。 此金鑰將會使用所有剩餘 hello StorSimple Manager 服務註冊裝置的 hello tooupdate。
   
   > [!NOTE]
   > 此程序必須在授權 StorSimple 裝置後的四個小時內起始。
   > 
   > 
   
   這個新的金鑰，然後會傳送 toohello 服務推入 toobe tooall hello 登錄的裝置與 hello 服務。 Hello 服務儀表板上，即會出現警示。 hello 服務將會停用所有 hello hello 註冊裝置上的作業，hello 裝置系統管理員將必須 tooupdate hello 服務資料加密金鑰 hello 上的其他裝置。 不過，hello I/o （傳送資料 toohello 雲端的主機） 不會被中斷。
   
   如果您有單一裝置註冊 tooyour 服務 hello 變換程序現在已完成，可以略過 hello 下一個步驟。 如果您有多個裝置已註冊的 tooyour 服務時，繼續 toostep 3。

### <a name="step-3-update-hello-service-data-encryption-key-on-other-storsimple-devices"></a>步驟 3： 更新其他 StorSimple 裝置上的 hello 服務資料加密金鑰
如果您有多個裝置已註冊的 tooyour StorSimple Manager 服務，必須在您的 StorSimple 裝置 hello Windows PowerShell 介面中執行這些步驟。 您在步驟 2 中取得的 hello 金鑰： 使用 Windows PowerShell for StorSimple tooinitiate hello 服務資料加密金鑰變更必須使用的 tooupdate 所有 hello 剩餘 StorSimple 裝置向 StorSimple Manager 服務的 hello。

執行下列步驟 tooupdate hello 服務資料加密在裝置上的 hello。

#### <a name="tooupdate-hello-service-data-encryption-key"></a>tooupdate hello 服務資料加密金鑰
1. 使用 Windows PowerShell for StorSimple tooconnect toohello 主控台。 選取選項 1 toolog 上，具有完整存取權。
2. 在 hello 命令提示字元中輸入：
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. 提供 hello 服務資料加密金鑰，您在取得[步驟 2： 使用 Windows PowerShell for StorSimple tooinitiate hello 服務資料加密金鑰變更](#to-initiate-the-service-data-encryption-key-change)。

