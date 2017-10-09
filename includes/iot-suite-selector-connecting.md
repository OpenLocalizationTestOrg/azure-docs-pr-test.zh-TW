> [!div class="op_single_selector"]
> * [Windows 上的 C](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [Linux 上的 C](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [Node.js](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a>案例概觀
在此案例中，您會建立傳送嗨遵循遙測 toohello 遠端監視的裝置[預先設定的解決方案][lnk-what-are-preconfig-solutions]:

* 外部溫度
* 內部溫度
* 溼度

為了簡單起見，hello hello 裝置上的程式碼會產生範例值，但我們鼓勵您 tooextend hello 範例實際感應器 tooyour 裝置連接和傳送實際的遙測。

hello 裝置也是可以 toorespond toomethods hello 方案儀表板從叫用，且想要設定 hello 方案儀表板中的屬性值。

toocomplete 本教學課程中，您需要使用中的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資訊，請參閱 [Azure 免費試用][lnk-free-trial]。

## <a name="before-you-start"></a>開始之前
在您為裝置撰寫任何程式碼之前，您必須先佈建遠端監視預先設定解決方案，並在該解決方案中佈建新的自訂裝置。

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a>佈建遠端監視預先設定解決方案
您在本教學課程中建立的 hello 裝置傳送嗨資料 tooan 執行個體[遠端監視][ lnk-remote-monitoring]預先設定的解決方案。 如果您沒有已佈建 hello 遠端監視您的 Azure 帳戶中預先設定的解決方案，使用下列步驟的 hello:

1. 在 hello <https://www.azureiotsuite.com/>頁面上，按一下 **+**  toocreate 方案。
2. 按一下**選取**上 hello**遠端監視**面板 toocreate 您的方案。
3. 在 hello**建立遠端監視解決方案**頁面上，輸入**方案名稱**您選擇的選取 hello**區域**toodeploy，再選取 hello Azure訂用帳戶 toowant toouse。 按一下 [建立解決方案] 。
4. 等待直到 hello 佈建程序完成。

> [!WARNING]
> 預先設定的 hello 解決方案會使用可計費的 Azure 服務。 請務必 tooremove hello 預先設定的方案，從您的訂用帳戶，當您在與其 tooavoid 任何不必要的費用。 您可以完整移除預先設定的方案從您的訂用帳戶瀏覽 hello <https://www.azureiotsuite.com/>頁面。
> 
> 

Hello 佈建 hello 遠端監視解決方案的程序完成時，請按一下**啟動**tooopen hello 方案儀表板在您的瀏覽器中。

![解決方案儀表板][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a>佈建您的裝置 hello 遠端監視解決方案中
> [!NOTE]
> 如果您已經在解決方案中佈建裝置，則可以略過此步驟。 當您建立 hello 用戶端應用程式時，您會需要 tooknow hello 裝置認證。
> 
> 

提供裝置 tooconnect toohello 預先設定的解決方案，它必須將自己識別 tooIoT 集線器使用有效的認證。 您可以擷取 hello 裝置認證從 hello 方案儀表板。 您稍後在本教學課程中，用戶端應用程式包含 hello 裝置認證。

tooadd 裝置 tooyour 遠端監視解決方案，下列的完整 hello hello 方案儀表板中的步驟：

1. 在 hello 左下角的 hello 儀表板，按一下 **新增裝置**。
   
   ![新增裝置][1]
2. 在 hello**自訂裝置** 面板中，按一下 **新增**。
   
   ![新增自訂裝置][2]
3. 選擇 [讓我定義自己的裝置識別碼]。 輸入裝置識別碼，例如**mydevice**，按一下 **檢查識別碼**tooverify 還未在使用中，該名稱，然後按一下**建立**tooprovision hello 裝置。
   
   ![新增裝置識別碼][3]
4. 請注意 hello 裝置認證 （裝置識別碼、 IoT 中樞的主機名稱、 和裝置金鑰）。 用戶端應用程式需要這些值 tooconnect toohello 遠端監視解決方案。 然後按一下 [完成]。
   
    ![檢視裝置認證][4]
5. Hello hello 方案儀表板中的裝置清單中選取您的裝置。 然後，在 hello**裝置詳細資料**] 面板中，按一下 [**啟用裝置**。 您的裝置 hello 狀態現在是**執行**。 hello 遠端監視解決方案現在可以從您的裝置接收遙測，並叫用 hello 裝置上的方法。

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/