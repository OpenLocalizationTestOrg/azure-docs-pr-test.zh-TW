## <a name="view-hello-solution-dashboard"></a>檢視 hello 方案儀表板

hello 方案儀表板可讓您 toomanage hello 部署方案。 例如，您可以檢視遙測、新增裝置及叫用方法。

1. 當 hello 佈建已完成，且您預先設定的解決方案 hello 磚指出**準備**，選擇**啟動**tooopen 遠端監視方案入口網站中的新索引標籤。

    ![啟動 hello 預先設定的解決方案][img-launch-solution]

1. 根據預設，hello 方案入口網站會顯示 hello*儀表板*。 您可以瀏覽 tooother hello 方案入口網站左側 hello hello 頁面使用 hello 功能表區域。

    ![遠端監視預先設定解決方案儀表板][img-menu]

## <a name="add-a-device"></a>新增裝置

提供裝置 tooconnect toohello 預先設定的解決方案，它必須將自己識別 tooIoT 集線器使用有效的認證。 您可以擷取 hello 裝置認證從 hello 方案儀表板。 您稍後在本教學課程中，用戶端應用程式包含 hello 裝置認證。

如果您尚未這樣做，請加入自訂裝置 tooyour 遠端監視解決方案。 完成下列步驟 hello 方案儀表板中的 hello:

1. 在 hello 左下角的 hello 儀表板，按一下 **新增裝置**。

   ![新增裝置][1]

1. 在 hello**自訂裝置** 面板中，按一下 **新增**。

   ![新增自訂裝置][2]

1. 選擇 [讓我定義自己的裝置識別碼]。 輸入裝置識別碼，例如**rasppi**，按一下 **檢查識別碼**tooverify 您您尚未使用您在方案中 hello 名稱，然後按一下**建立**tooprovision hello 裝置。

   ![新增裝置識別碼][3]

1. 請注意 hello 裝置認證 (**裝置識別碼**， **IoT 中樞的主機名稱**，和**裝置金鑰**)。 用戶端應用程式上 hello 覆盆子 Pi 需要這些值 tooconnect toohello 遠端監視解決方案。 然後按一下 [完成]。

    ![檢視裝置認證][4]

1. Hello hello 方案儀表板中的裝置清單中選取您的裝置。 然後，在 hello**裝置詳細資料**] 面板中，按一下 [**啟用裝置**。 您的裝置 hello 狀態現在是**執行**。 hello 遠端監視解決方案現在可以從您的裝置接收遙測，並叫用 hello 裝置上的方法。

[img-launch-solution]: media/iot-suite-raspberry-pi-kit-view-solution/launch.png
[img-menu]: media/iot-suite-raspberry-pi-kit-view-solution/menu.png
[1]: media/iot-suite-raspberry-pi-kit-view-solution/suite0.png
[2]: media/iot-suite-raspberry-pi-kit-view-solution/suite1.png
[3]: media/iot-suite-raspberry-pi-kit-view-solution/suite2.png
[4]: media/iot-suite-raspberry-pi-kit-view-solution/suite3.png