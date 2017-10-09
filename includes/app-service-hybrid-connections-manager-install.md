
1. 在 hello**混合式連線**刀鋒視窗中，按一下您剛 hello 混合式連接建立，然後按一下 **接聽程式的安裝程式**。
   
    ![Click Listener Setup](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. hello**混合式連接屬性**刀鋒視窗隨即開啟。 在下**在內部部署混合式連線管理員**，選擇**手動下載及設定**，儲存下載的 hello HybridConnectionManager.msi 封裝，並將複製 hello 閘道連接字串。
   
    ![按一下這裡 tooinstall](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. 系統管理員命令提示字元中，輸入下列命令 toostart hello installer hello:
   
        start HybridConnectionManager.msi
4. Hello 之後執行安裝程式中，按一下**現在不要**，然後瀏覽 toohello %ProgramFiles%\Microsoft\HybridConnectionManager 資料夾中，執行 HCMConfigWizard.exe 並按一下**是**在 hello**使用者帳戶控制**對話方塊。
5. 貼上您之前複製的 hello 混合式連接字串，然後按一下**確定**。 
   
    ![安裝](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. Hello 安裝完成時，按一下**關閉**。
   
    ![Click Close](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    在 hello**混合式連線**刀鋒視窗，hello**狀態**資料行現在會顯示**已連接**。 
   
    ![Connected Status](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

