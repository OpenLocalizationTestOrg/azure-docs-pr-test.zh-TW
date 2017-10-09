<!--author=alkohli last changed:02/10/2017-->


#### <a name="toocreate-a-new-service"></a>toocreate 新的服務

1. 使用您的 Microsoft 帳戶認證 toolog toohello [Azure 入口網站](https://portal.azure.com/)。

2. 在 hello Azure 入口網站，按一下   **+**  ，然後在 hello marketplace 按一下**查看所有**。

    ![建立 StorSimple 裝置管理員](./media/storsimple-8000-create-new-service/createssdevman1.png)

    搜尋 [StorSimple 實體]。 選取並按一下 StorSimple 實體裝置系列，然後按一下建立。 或者，在 hello Azure 入口網站中按一下 **+**  ，然後在**儲存體**，按一下  **StorSimple 實體裝置系列**。

    ![建立 StorSimple 裝置管理員](./media/storsimple-8000-create-new-service/createssdevman11.png)

3. 在 hello **StorSimple 裝置管理員**刀鋒視窗中，執行下列步驟 hello:
   
   1. 為服務提供唯一的**資源名稱** 。 這個名稱是易記的名稱可能是使用 tooidentify hello 服務。 hello 名稱只能有 2 到 50 個字元，可以是字母、 數字和連字號。 hello 名稱必須啟動，並以字母或數字結尾。

   2. 選擇**訂用帳戶**hello 下拉式清單中。 計費帳戶連結的 tooyour hello 訂用帳戶。 如果您只擁有一個訂用帳戶，則此欄位不存在。

   3. 針對**資源群組**，**使用現有群組**或**建立新的群組**。 如需詳細資訊，請參閱 [Azure 資源群組](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/)。
   
   4. 提供服務的 [位置]  。 一般情況下，選擇位置最靠近 toohello 地理區域 toodeploy 希望您的裝置。 您也可以在下列考量 hello toofactor: 
      
      * 如果您有現有的工作負載，您也想 toodeploy 與您的 StorSimple 裝置的 Azure 中，您應該使用該資料中心。
      * 您的 StorSimple 裝置管理員服務和 Azure 儲存體可以位於兩個不同的位置。 在這種情況下，您會需要的 toocreate hello StorSimple 裝置管理員和 Azure 儲存體帳戶分開。 toocreate Azure 儲存體帳戶，請移 toohello hello Azure 入口網站中的 Azure 儲存體服務，並依照中的 hello 步驟[建立 Azure 儲存體帳戶](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account)。 建立此帳戶之後，將它加入 toohello StorSimple 裝置 Manager 服務中的 hello 步驟[設定新的儲存體帳戶 hello 服務](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#configure-a-new-storage-account-for-the-service)。

   5. 選取**建立新的儲存體帳戶**tooautomatically 與 hello 服務建立儲存體帳戶。 指定此儲存體帳戶的名稱。 如果您需要將資料放在不同的位置，取消核取此方塊。

   6. 請檢查**Pin toodashboard**如果您想要快速連結 toothis 服務儀表板上。
      
   7. 按一下**建立**toocreate hello StorSimple 裝置管理員。

       ![建立 StorSimple 裝置管理員](./media/storsimple-8000-create-new-service/createssdevman2.png)
   
hello 服務建立作業需要幾分鐘的時間。 已成功建立 hello 服務之後，您會看到通知，而且 hello 新服務刀鋒視窗會開啟。
   
![建立 StorSimple 裝置管理員](./media/storsimple-8000-create-new-service/createssdevman5.png)


