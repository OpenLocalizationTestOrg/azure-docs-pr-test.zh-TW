#### <a name="toocreate-a-new-service"></a>toocreate 新的服務

1.  使用您的 Microsoft 帳戶認證，登入 toohello 此 URL 在 Azure 入口網站： <https://portal.azure.com/>。 如果部署政府入口網站中的 hello 裝置，請登入： <https://portal.azure.us/>

2.  在 hello Azure 入口網站，按一下  **+ 新增** &gt; **儲存體** &gt; **StorSimple 虛擬數列**。

    ![建立新的服務](./media/storsimple-virtual-array-create-new-service/createnewservice2.png) 

3.  在 hello **StorSimple 裝置管理員**刀鋒視窗，開啟，請勿遵循 hello:

    1.  為服務提供唯一的**資源名稱** 。 hello 資源名稱是易記的名稱可能是使用 tooidentify hello 服務。 hello 名稱只能有 2 到 50 個字元，可以是字母、 數字和連字號。 hello 名稱必須啟動，並以字母或數字結尾。

    2.  選擇**訂用帳戶**hello 下拉式清單中。 計費帳戶連結的 tooyour hello 訂用帳戶。 如果您只擁有一個訂用帳戶，則此欄位不存在。

    3.  針對**資源群組**，選取現有群組或建立新的群組。 如需詳細資訊，請參閱 [Azure 資源群組](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/)。

    4.  提供服務的 [位置]  。 如需各區域可用服務的詳細資訊，請參閱 [Azure 區域](https://azure.microsoft.com/regions/#services)。 一般情況下，選擇**位置**最接近您希望 toodeploy 裝置 toohello 地理區域。 您也可以在 hello 下列 toofactor:

        -   如果您有現有的工作負載，您也想 toodeploy 與您的 StorSimple 裝置的 Azure 中，我們建議您先使用該資料中心。

        -   您的 StorSimple 裝置管理員和 Azure 儲存體可以分別位於兩個不同的位置。 在這種情況下，您會需要的 toocreate hello StorSimple 裝置管理員和 Azure 儲存體帳戶分開。 toocreate Azure 儲存體帳戶，請移 toohello hello Azure 入口網站中的 Azure 儲存體服務，並依照中的 hello 步驟[建立 Azure 儲存體帳戶](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/#create-a-storage-account)。 建立此帳戶之後，將它加入 toohello StorSimple 裝置 Manager 服務中的 hello 步驟[設定新的儲存體帳戶 hello 服務](https://azure.microsoft.com/en-us/documentation/articles/storsimple-deployment-walkthrough/#configure-a-new-storage-account-for-the-service)。

        -   如果部署 hello hello 政府入口網站中的虛擬裝置，hello StorSimple 裝置管理員服務提供了美國稍後和美國維吉尼亞位置。

    5.  選取**建立新的 Azure 儲存體帳戶**tooautomatically 與 hello 服務建立儲存體帳戶。 指定**儲存體帳戶名稱**。 如果您需要將資料放在不同的位置，取消核取此方塊。

    6.  請檢查**Pin toodashboard**如果您想要快速連結 toothis 服務儀表板上。

    7.  按一下**建立**toocreate hello StorSimple 裝置管理員。

        ![建立新的服務](./media/storsimple-virtual-array-create-new-service/createnewservice4.png)  

會導向的 toohello**服務**登陸頁面。 hello 服務建立作業需要幾分鐘的時間。 已成功建立 hello 服務將會適當通知您 hello hello 服務狀態也會變更後，**Active**。


