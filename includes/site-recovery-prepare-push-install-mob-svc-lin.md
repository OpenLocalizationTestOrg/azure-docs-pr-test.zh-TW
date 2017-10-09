### <a name="prepare-for-a-push-installation-on-a-linux-server"></a>準備在 Linux 伺服器上推送安裝

1. 請確認有 hello Linux 電腦和 hello 處理序伺服器之間的網路連線。
2. 建立該 hello 處理序伺服器可以使用 tooaccess hello 電腦帳戶。 hello 帳戶應為**根**hello 來源 Linux 伺服器上的使用者。 （使用此帳戶僅針對 hello 推入安裝和更新時）。
3. 請檢查該 hello 來源伺服器具有與所有網路介面卡相關聯的 hello 本機主機名稱 tooIP 位址對應的項目 Linux 上的 hello /etc/hosts 檔案。
4. 您想 tooreplicate hello 電腦上安裝 hello 最新的 openssh、 openssh 伺服器和 openssl 封裝。
5. 請確定安全殼層 (SSH) 已啟用且正在連接埠 22 上執行。
6. 啟用 SFTP 子系統和密碼驗證 hello sshd_config 檔案中：
  1.  以 **root** 的身分登入。
  2.  在 hello 檔案等/ssh/sshd_config 檔案 hello 線尋找開頭為**PasswordAuthentication**。
  3.  Hello 行取消註解，也變更 hello 值**是**。
  4.  尋找 hello 行開頭為**子系統**和 hello 行取消註解。

     ![Linux](./media/site-recovery-prepare-push-install-mob-svc-lin/mobility2.png)
  5. 重新啟動 hello **sshd**服務。

7. 新增 hello CSPSConfigtool 中建立的帳戶。
    1.  登入 tooyour 組態伺服器。
    2.  開啟 **cspsconfigtool.exe**。 （它是可當做捷徑 hello 桌面上和 hello %ProgramData%\home\svsystems\bin 資料夾中）。
    3.  在 hello**管理帳戶**索引標籤上，按一下 **新增帳戶**。
    4.  加入您所建立的 hello 帳戶。 
    5.  輸入您為電腦啟用時，您使用的 hello 認證。
