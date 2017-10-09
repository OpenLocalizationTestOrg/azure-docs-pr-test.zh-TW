<!--author=alkohli last changed:01/14/2016-->


#### <a name="toocreate-a-new-service"></a>toocreate 新的服務
1. 使用您的 Microsoft 帳戶認證，登入 toohello 此 URL 在 Azure 傳統入口網站： [https://manage.windowsazure.com/](https://manage.windowsazure.com/)。
2. 在 hello Azure 傳統入口網站，按一下 **新增** > **Data Services** > **StorSimple Manager** > **快速建立**。
3. 在顯示 hello 表單中，請勿 hello 遵循：
   
   1. 為服務提供唯一的 [名稱]  。 這是易記的名稱可能是使用 tooidentify hello 服務。 hello 名稱只能有 2 到 50 個字元，可以是字母、 數字和連字號。 hello 名稱必須啟動，並以字母或數字結尾。
   2. 提供服務的 [位置]  。 一般情況下，選擇位置最靠近 toohello 地理區域 toodeploy 希望您的裝置。 您也可以在 hello 下列 toofactor: 
      
      * 如果您有現有的工作負載，您也想 toodeploy 與您的 StorSimple 裝置的 Azure 中，您應該使用該資料中心。
      * 您的 StorSimple Manager 服務和 Azure 儲存體可以位於兩個不同的位置。 在這種情況下，您會需要的 toocreate hello StorSimple Manager 和 Azure 儲存體帳戶分開。 toocreate Azure 儲存體帳戶，請移 toohello hello Azure 傳統入口網站中的 Azure 儲存體服務，並依照中的 hello 步驟[建立 Azure 儲存體帳戶](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account)。 建立此帳戶之後，將它加入 toohello StorSimple Manager 服務中的 hello 步驟[設定新的儲存體帳戶 hello 服務](../articles/storsimple/storsimple-deployment-walkthrough.md#configure-a-new-storage-account-for-the-service)。
   3. 選擇**訂用帳戶**hello 下拉式清單中。 計費帳戶連結的 tooyour hello 訂用帳戶。 如果您只擁有一個訂用帳戶，則此欄位不存在。
   4. 選取**建立新的儲存體帳戶**tooautomatically 與 hello 服務建立儲存體帳戶。 這個儲存體帳戶將具有一個特殊名稱，例如 "storsimplebwv8c6dcnf"。 如果您需要將資料放在不同的位置，取消核取此方塊。 
   5. 按一下**建立 StorSimple Manager** toocreate hello 服務。
   
   ![建立 StorSimple Manager](./media/storsimple-create-new-service/HCS_CreateAService-include.png)
   
   您將會導向的 toohello**服務**登陸頁面。 hello 服務建立將需要幾分鐘的時間。 已成功建立 hello 服務將會適當通知您 hello hello 服務狀態也會變更後，**Active**。
   
   ![服務建立](./media/storsimple-create-new-service/HCS_StorSimpleManagerServicePage-include.png)

![提供的影片](./media/storsimple-create-new-service/Video_icon.png) **提供的影片**

toowatch 的視訊示範，如何 toocreate 新的 StorSimple Manager 服務，按一下[這裡](https://azure.microsoft.com/documentation/videos/create-a-storsimple-manager-service/)。

