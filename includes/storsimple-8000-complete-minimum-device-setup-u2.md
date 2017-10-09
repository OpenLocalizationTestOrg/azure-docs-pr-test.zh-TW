<!--author=alkohli last changed: 01/12/17-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>toocomplete hello 最小 StorSimple 裝置設定

   > [!NOTE]
   > Hello 最低裝置設定完成之後，您無法變更 hello 裝置名稱。
   
1. 從 hello 表格清單中的裝置 hello**裝置**刀鋒視窗中，選取，然後按一下您的裝置。 hello 裝置處於**已 tooset 準備註冊**狀態。 hello**設定裝置**刀鋒視窗會開啟。

     ![StorSimple 最小裝置設定網路介面](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig1.png)

2. 在 hello**設定裝置**刀鋒視窗中：
   
   1. 為裝置提供 [易記名稱]  。 hello 預設裝置名稱會反映 hello 裝置型號和序號等資訊。 您可以指派的易記名稱總 too64 字元 toomanage 您的裝置。
   2. 設定 hello**時區**根據裝置正在部署中的 hello hello 地理位置。 裝置將針對所有排程作業使用這個時區。
   3. 在 hello **DATA 0 設定**:

       1. 您的 DATA 0 網路介面會顯示以 hello 啟用網路設定 IP、 子網路 （閘道） 透過 hello 安裝精靈設定。 也會針對雲端以及 iSCSI 將 DATA 0 自動啟用。

       2. 提供 hello 固定 IP 位址，控制器 0 及控制器 1。 **hello 控制器固定 IP 位址需要 toobe 釋放 Ip hello 可存取的子網路內 hello 裝置的 IP 位址。** 如果 hello DATA 0 介面設定了 IPv4，hello 固定 IP 位址需要 toobe hello IPv4 格式提供。 如果您提供 IPv6 設定的前置詞，hello 固定 IP 位址會自動填入這些欄位中。

            ![StorSimple 最小裝置設定網路介面](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig2.png)

            hello 固定 hello 控制站的 IP 位址可用來服務 hello 更新 toohello 裝置。 因此，hello 固定 Ip 必須可路由傳送，而且要能 tooconnect toohello 網際網路。 您可以檢查您控制器固定的 Ip 可路由傳送使用 hello [Test-hcsmconnection] [ Test] cmdlet。 下列範例顯示固定控制器 Ip 路由的 toohello 網際網路並且可以存取的 hello hello Microsoft Update servers。

            ![Test-HcsmConnection 顯示可路由傳送 IP](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig3.png)

1. 按一下 [確定] 。 hello 裝置設定啟動。 Hello 裝置設定完成時，會通知您。 hello 裝置狀態變更太**線上**在 hello**裝置**刀鋒視窗。

    ![StorSimple 最小裝置設定網路介面](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig4.png)

<!--Link reference-->
[Test]: https://technet.microsoft.com/library/dn715782(v=wps.630).aspx
