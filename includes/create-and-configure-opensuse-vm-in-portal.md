1. 登入 toohello [Azure 傳統入口網站](http://manage.windowsazure.com)。  
2. 在 hello 在 hello hello 視窗底部的命令列中按一下**新增**。
3. 在 [計算] 下，依序按一下 [虛擬機器] 及 [從映像庫]。
   
    ![建立新的虛擬機器][Image1]
4. 在 hello **SUSE**群組，選取 OpenSUSE 虛擬機器映像，然後按一下hello 箭號 toocontinue。
5. 在 hello 上第一個**虛擬機器組態**頁面：
   
   * 輸入 **虛擬機器名稱** (如 "testlinuxvm")。 hello 名稱必須介於 3 到 15 個字元，可以包含字母、 數字和連字號，並且必須以字母開頭和結尾以字母或數字。
   * 確認 hello**層**並挑選**大小**。 hello 層會決定您可以選擇從 hello 大小。 hello 大小會影響 hello 成本使用它，以及組態選項，例如多少資料磁碟，您可以將附加。 如需詳細資訊，請參閱 [虛擬機器的大小](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
   * 輸入**新的使用者名稱**，或接受 hello 預設**azureuser**。 這個名稱會加入 toohello Sudoers 清單檔案。
   * 決定哪一種類型**驗證**toouse。 如需一般密碼指導方針，請參閱 [字串密碼](http://msdn.microsoft.com/library/ms161962.aspx)。
6. 在 hello 下一步**虛擬機器組態**頁面：
   
   * 使用預設的 hello**建立新的雲端服務**。
   * 在 hello **DNS 名稱**方塊中，輸入唯一的 DNS 名稱 toouse hello 位址，例如"testlinuxvm 」 的一部分。
   * 在 hello**區域/同質群組/虛擬網路**方塊中，選取將託管這個虛擬映像的區域。
   * 在下**端點**，保留 hello SSH 的端點。 您可以現在，加入其他人或新增、 變更或 hello 虛擬機器建立後加以刪除。
     
     > [!NOTE]
     > 如果您想要虛擬機器 toouse 虛擬網路，您**必須**指定 hello 虛擬網路，當您建立 hello 虛擬機器。 建立 hello 虛擬機器之後，您無法將虛擬機器 tooa 虛擬網路。 如需詳細資訊，請參閱[虛擬網路概觀](../articles/virtual-network/virtual-networks-overview.md)。
     > 
     > 
7. 在 hello 上最後一個**虛擬機器組態**頁面上，保留 hello 預設設定，然後按一下hello 核取記號 toofinish。

hello 網站列出下 hello 新虛擬機器**虛擬機器**。 雖然 hello 狀態報告為**（佈建）**，設定 hello 虛擬機器。 當 hello 狀態報告為**執行**，您可以移 toohello 下一個步驟。

## <a name="connect-toohello-virtual-machine"></a>連接 toohello 虛擬機器
您將使用 SSH 或 PuTTY tooconnect toohello 虛擬機器，視您要從連接的 hello 電腦上的 hello 作業系統而定：

* 請從執行 Linux 的電腦使用 SSH。 在 hello 命令提示字元中輸入：
  
    `$ ssh newuser@testlinuxvm.cloudapp.net -o ServerAliveInterval=180`
  
    輸入 hello 使用者的密碼。
* 請從執行 Windows 的電腦使用 PuTTY。 如果您沒有安裝它，從 hello 下載[PuTTY 下載頁面][PuTTYDownload]。
  
    儲存**putty.exe** tooa 目錄，在您的電腦上。 開啟命令提示字元，瀏覽 toothat 資料夾，並執行**putty.exe**。
  
    輸入 hello 主機名稱，例如"testlinuxvm.cloudapp.net 」，然後輸入"22"hello**連接埠**。
  
    ![PuTTY 畫面][Image6]  

## <a name="update-hello-virtual-machine-optional"></a>更新 hello 虛擬機器 （選擇性）
1. 在連接的 toohello 虛擬機器之後，您可以選擇性地安裝系統更新和修補程式。 型別 toorun hello 更新：
   
    `$ sudo zypper update`
2. 選取**軟體**，然後**線上更新**toolist 可用的更新。 選取**接受**toostart hello 安裝，並套用所有新可用的修補程式 （除了 hello 選擇性的)。
3. 安裝完成之後，選取 [ **完成**]。  系統現在是 toodate 組成。

[PuTTYDownload]: http://www.puttyssh.org/download.html

[Image1]: ./media/create-and-configure-opensuse-vm-in-portal/CreateVM.png

[Image6]: ./media/create-and-configure-opensuse-vm-in-portal/putty.png
