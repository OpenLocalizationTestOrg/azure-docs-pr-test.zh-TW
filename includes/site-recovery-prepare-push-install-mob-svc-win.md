### <a name="prepare-for-a-push-installation-on-a-windows-computer"></a>準備在 Windows 電腦上推送安裝

1. 請確認有 hello Windows 電腦和 hello 處理序伺服器之間的網路連線。
2. 建立該 hello 處理序伺服器可以使用 tooaccess hello 電腦帳戶。 hello 帳戶應擁有系統管理員權限 （本機或網域）。 （使用此帳戶僅針對 hello 推入安裝和代理程式更新時）。

   > [!NOTE]
   > 如果您不使用網域帳戶，停用 hello 本機電腦上的遠端使用者存取控制。 toodisable 遠端使用者存取控制，hello HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System 登錄機碼下新增新的 DWORD: **LocalAccountTokenFilterPolicy**。 設定 hello 值太**1**。 toodo 這在命令提示字元中，執行下列命令的 hello:  
   `REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`
   >
   >
2. Hello 電腦上的 Windows 防火牆中您想選取 tooprotect**允許的應用程式或功能通過防火牆**。 啟用 [檔案及印表機共用] 和 [Windows Management Instrumentation (WMI)]。 對於屬於 tooa 網域的電腦，您可以使用群組原則物件 (GPO) 設定 hello 防火牆設定。

   ![防火牆設定](./media/site-recovery-prepare-push-install-mob-svc-win/mobility1.png)

3. 新增 hello CSPSConfigtool 中建立的帳戶。
    1.  登入 tooyour 組態伺服器。
    2.  開啟 **cspsconfigtool.exe**。 （它是可當做捷徑 hello 桌面上和 hello %ProgramData%\home\svsystems\bin 資料夾中）。
    3.  在 hello**管理帳戶**索引標籤上，選取**新增帳戶**。
    4.  加入您所建立的 hello 帳戶。
    5.  輸入您為電腦啟用時，您使用的 hello 認證。
