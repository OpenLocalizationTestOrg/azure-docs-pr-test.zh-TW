<!--author=alkohli last changed: 9/17/15-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>toocomplete hello 最小 StorSimple 裝置設定
1. 選取 hello 裝置，然後按一下 **快速入門**。 按一下**完成裝置設定**toostart hello 設定裝置精靈。
2. Hello 設定裝置精靈**基本設定**對話方塊方塊中，執行下列 hello:
   
   1. 為裝置提供 [易記名稱]  。 hello 預設裝置名稱會反映 hello 裝置型號和序號等資訊。 您可以指派的易記名稱總 too64 字元 toomanage 您的裝置。
   2. 設定 hello**時區**根據裝置正在部署中的 hello hello 地理位置。 裝置將針對所有排程的操作使用這個時區。
   3. 在 [DNS 設定] 下方，提供 [次要 DNS 伺服器] 的位址。 如果您使用 IPv6 時，會根據 hello hello Windows PowerShell 介面中提供的 IPv6 首碼填入 hello 欄位。 
      如果未設定次要 DNS 伺服器 hello，則不會允許 toosave 裝置組態。
   4. 在啟用 iSCSI 的介面下方，至少啟用一個適用於 iSCSI 的網路。 至少一個網路介面必須 toobe 具備雲端功能，且有一個介面具有 toobe iSCSI 功能。 DATA 0 會自動具備雲端功能。
      
      ![StorSimple 最小裝置設定基本設定](./media/storsimple-complete-minimum-device-setup-u1/HCS_MinDeviceSetupBasicSettings1-include.png)
3. 按一下 hello 箭號圖示。 ![StorSimple 箭頭圖示](./media/storsimple-complete-minimum-device-setup/HCS_ArrowIcon-include.png)
4. 在 hello**網路介面**對話方塊方塊中，提供 hello 固定 IP 位址，控制器 0 及控制器 1。 **hello 控制器固定 IP 位址需要 toobe 釋放 Ip hello 可存取的子網路內 hello 裝置的 IP 位址。** 如果 hello DATA 0 介面設定了 IPv4，hello 固定 IP 位址需要 toobe hello IPv4 格式提供。 如果您提供 IPv6 設定的前置詞，hello 固定 IP 位址會自動填入這些欄位中。

    ![StorSimple 最小裝置設定網路介面](./media/storsimple-complete-minimum-device-setup-u1/HCS_MinDeviceSetupNetworkInterfaces2-include.png)

    hello 固定 hello 控制站的 IP 位址用於服務 hello 更新 toohello 裝置，並因此 hello 固定 Ip 必須可路由傳送，而且要能 tooconnect toohello 網際網路。 您可以檢查您控制器固定的 Ip 可路由傳送使用 hello [Test-hcsmconnection] [ Test] cmdlet。 下列範例顯示固定控制器 Ip 路由的 toohello 網際網路並且可以存取的 hello hello Microsoft Update servers。 

     ![Test-HcsmConnection 顯示可路由傳送 IP](./media/storsimple-complete-minimum-device-setup-u1/Test-HcsmConnectionOutputRegisteredDevice.png)

1. 按一下核取圖示，hello ![StorSimple 核取圖示](./media/storsimple-complete-minimum-device-setup/HCS_CheckIcon-include.png)。
   您將會傳回 toohello 裝置**快速入門**頁面。
   
   > [!NOTE]
   > 您可以修改所有 hello 其他裝置設定隨時藉由存取 hello**設定**頁面。
   > 
   > 

<!--Link reference-->
[Test]: https://technet.microsoft.com/library/dn715782(v=wps.630).aspx