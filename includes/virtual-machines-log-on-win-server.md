1. 按一下 [連接]  建立並下載 [遠端桌面通訊協定] 檔案 (.rdp file)。 按一下**開啟**toouse 這個檔案。
2. 您會收到警告該 hello.rdp 取自未知的發行者。 這是正常現象。 在 hello 遠端桌面視窗中，按一下 **連接**toocontinue。
   
    ![未知發行者相關警告的螢幕擷取畫面。](./media/virtual-machines-log-on-win-server/rdp-warn.png)
3. 在 hello **Windows 安全性**視窗中，輸入 hello 虛擬機器上的 hello 帳戶的認證，然後再按一下**確定**。
   
     **本機帳戶**-這通常是 hello 本機帳戶使用者名稱和密碼，在建立時指定 hello 虛擬機器。 在此情況下，hello 定義域是 hello hello 虛擬機器名稱，而且會輸入為*vmname*&#92;*使用者名稱*。  
   
    **已加入網域的 VM** -如果 hello VM 所屬 tooa 網域 hello 格式輸入 hello 使用者名稱*網域*&#92;*使用者名稱*。 hello 帳戶也必須 tooeither hello administrators 群組或已被授與遠端存取權限 toohello VM。
   
    **網域控制站**-如果 hello VM 是網域控制站、 輸入 hello 的使用者名稱和該網域的網域系統管理員帳戶的密碼。
4. 按一下**是**tooverify hello hello 虛擬機器的身分識別，並完成登入。
   
   ![螢幕擷取畫面顯示一則訊息緊鄰驗證 hello VM hello 識別。](./media/virtual-machines-log-on-win-server/cert-warning.png)

