1. 執行 hello 整合安裝程式安裝檔案。
2. 在**在您開始前**，選取**hello 組態伺服器與處理序伺服器安裝**。

    ![開始之前](./media/site-recovery-add-configuration-server/combined-wiz1.png)

3. 在**第三方軟體授權**，按一下 **我接受**toodownload 並安裝 MySQL。

    ![協力廠商軟體](./media/site-recovery-add-configuration-server/combined-wiz2.png)
4. 在**註冊**，選取您下載 hello 保存庫中的 hello 註冊金鑰。

    ![註冊](./media/site-recovery-add-configuration-server/combined-wiz3.png)
5. 在**網際網路設定**，指定如何在 hello 組態伺服器上執行的提供者透過連接 tooAzure Site Recovery 的 hello hello 網際網路。

   a. 如果您想 tooconnect 要與目前在 hello 機器設定的 hello proxy 時，選取**連線使用 proxy 伺服器的站台復原 tooAzure**。

   b. 若要直接 hello 提供者 tooconnect，選取**直接連接不使用 proxy 伺服器的站台復原 tooAzure**。

   c. 如果 hello 現有 proxy 需要驗證，或是您想要 hello 提供者連接 toouse 自訂 proxy，請選取**使用自訂 proxy 設定連線**。

     * 如果您使用自訂 proxy，您需要 toospecify hello 位址、 連接埠，以及認證。
     * 如果您使用 proxy，您應該已經允許 hello Url 中所述[必要條件](#prerequisites)。

     ![防火牆](./media/site-recovery-add-configuration-server/combined-wiz4.png)
6. 在**必要條件檢查**，安裝程式會執行檢查 toomake 確定，可以執行安裝。 如果出現有關 hello 警告**通用時間同步處理檢查**，驗證 hello 系統時鐘的 hello 時間 (**日期和時間**設定) hello 相同與 hello 時區。

    ![必要條件](./media/site-recovery-add-configuration-server/combined-wiz5.png)
7. 在**MySQL 組態**，建立記錄 toohello MySQL 伺服器執行個體上已安裝的認證。

    ![MySQL](./media/site-recovery-add-configuration-server/combined-wiz6.png)
8. 在**環境詳細資料**，選取是否要 tooreplicate VMware Vm。 如果是的話，安裝程式就會檢查是否已安裝 PowerCLI 6.0。

    ![MySQL](./media/site-recovery-add-configuration-server/combined-wiz7.png)

9. 在**安裝位置**，選取您想 tooinstall hello 二進位檔和 hello 快取儲存。 您選取的 hello 磁碟機必須有至少 5 GB 的可用磁碟空間，但我們建議至少 600 GB 的可用空間的快取磁碟機。

    ![安裝位置](./media/site-recovery-add-configuration-server/combined-wiz8.png)
10. 在**網路選取項目**、 指定 hello 接聽程式 （網路介面卡和 SSL 連接埠） 上的 hello 組態伺服器傳送及接收複寫資料。 連接埠 9443 hello 預設連接埠，用來傳送和接收複寫流量，但您可以修改此連接埠號碼 toosuit 您環境的需求。 在加法 toohello 連接埠 9443，我們也會開啟 web 伺服器 tooorchestrate 複寫作業所使用的連接埠 443。 請勿使用連接埠 443 來傳送或接收複寫流量。

    ![網路選擇](./media/site-recovery-add-configuration-server/combined-wiz9.png)


11. 在**摘要**，檢閱 hello 資訊，然後按一下**安裝**。 安裝完成時，會產生複雜密碼。 在您啟用複寫時會需要它，所以請將它複製並保存在安全的位置。

    ![摘要](./media/site-recovery-add-configuration-server/combined-wiz10.png)

Hello 伺服器註冊完成之後，會顯示在 hello**設定** > **伺服器**hello 保存庫中的刀鋒視窗。
