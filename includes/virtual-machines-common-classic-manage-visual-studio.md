在 Visual Studio 中使用 [伺服器總管]，即可在 Azure 中建立虛擬機器。

## <a name="create-an-azure-virtual-machine-in-server-explorer"></a>在伺服器總管中建立 Azure 虛擬機器
雖然您可以建立虛擬機器在 hello [Azure 管理入口網站](http://go.microsoft.com/fwlink/?LinkID=253103)，您也可以建立在 Azure 中虛擬機器，使用伺服器總管 中的命令。 虛擬機器可以使用，例如 tooprovide 前端最後一般負載平衡公用端點之後。

### <a name="toocreate-a-new-virtual-machine"></a>toocreate 新的虛擬機器
1. 在 伺服器總管 中，開啟 hello **Azure**節點，然後按一下**虛擬機器**。
2. Hello 操作功能表上，按一下 **建立虛擬機器**。
   
    hello**建立新的虛擬機器**精靈 隨即出現。
   
    ![hello 建立虛擬機器命令](./media/virtual-machines-common-classic-create-manage-visual-studio/IC718342.png)
3. 在 hello**選擇訂用帳戶**頁面上，選取訂用帳戶 toouse 建立 hello 虛擬機器時，然後按一下**下一步**。
   
    如果您未登入 tooAzure，按一下**登入**toosign 中的。 如果尚未選取，然後選取 hello 下拉式清單方塊中 Azure 訂用帳戶。
4. 在 hello**選取虛擬機器映像**頁面上，選取影像類型在 hello**影像類型**下拉式清單方塊，，，然後選取 hello 中的 虛擬機器映像**映像名稱**清單方塊。 完成後，按 [下一步] 。
   
    ![選取虛擬機器映像頁面](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744137.png)
   
    您可以選擇下列影像類型 hello。
   
   *  可列出作業系統和伺服器軟體 (例如 Windows Server 和 SQL Server) 的虛擬機器映像。
   * **MSDN 映像**列出的 軟體可用 tooMSDN 訂閱者，例如 Visual Studio 和 Microsoft Dynamics 的虛擬機器映像。
   *  可列出您已建立的特殊和一般虛擬機器映像。
     
     toolearn 大約的特殊化和一般化虛擬機器，請參閱[VM 映像](https://azure.microsoft.com/blog/2014/04/14/vm-image-blog-post/)。 請參閱[如何 tooCapture 做為範本的 Windows 虛擬機器 tooUse](https://azure.microsoft.com/documentation/articles/virtual-machines-capture-image-windows-server/)如需有關如何成範本，您可以使用 tooquickly 虛擬機器建立新的 tooturn 預先設定的虛擬機器資訊。
     
     您可以按一下虛擬機器映像名稱 toosee hello 影像資訊 hello 右側的 hello 頁面。
     
     > [!NOTE]
     > 您無法將虛擬機器映像 toohello**公用映像**或**MSDN 映像**列出，因為它們是唯讀狀態。 您所建立的所有虛擬機器會都新增 toohello**私人映像**清單。
     > 
     > 
     
     如果您是具有 Visual Studio 層級訂用帳戶的 MSDN 訂閱者，您可以建立一個預先建置的 Azure 虛擬機器，其中包含 Visual Studio 以及其他數個映像。 如需詳細資訊，請參閱[使用映像在 Visual Studio 中建立虛擬機器、MSDN 訂閱者的 Visual Studio 2013 資源庫映像](http://visualstudio2013msdngalleryimage.azurewebsites.net)和 [MSDN 訂閱](https://www.visualstudio.com/products/msdn-subscriptions-vs)。|
5. 在 hello**虛擬機器基本設定**頁面上，輸入電腦名稱，然後新增 hello 規格 hello 虛擬機器，包括 hello 大小，以及使用者名稱和密碼。 完成後，按 [下一步] 。
   
    您將使用 hello 新名稱和密碼 toolog hello 機器使用遠端桌面，因此它是個不錯的主意 toowrite 它們向下的情況下，您忘記。 Visual Studio 中建立 Azure 虛擬機器之後，您可以變更其大小和其他設定，在 hello [Azure 管理入口網站](http://go.microsoft.com/fwlink/?LinkID=253103)。
   
   > [!NOTE]
   > 如果您選擇的 hello 虛擬機器大小比較大，可能會套用額外的費用。 如需詳細資訊，請參閱 [虛擬機器定價詳細資料](https://azure.microsoft.com/pricing/details/virtual-machines/) 。
   > 
   > 
6. 在 Visual Studio 中建立的虛擬機器需要雲端服務。 在 hello**雲端服務設定**頁面上，選取雲端服務的 hello 虛擬機器，或按一下**< 建立新...>** hello 下拉式清單，如果您還沒有雲端服務，或想要新 toouse 中其中一個。 也是必要的儲存體帳戶，因此選擇儲存體帳戶 （或建立新的儲存體帳戶） 中 hello**儲存體帳戶**下拉式清單方塊。 請參閱[簡介 tooMicrosoft Azure 儲存體](../articles/storage/common/storage-introduction.md)如需詳細資訊。
7. 如果您想 toospecify 虛擬網路 （這是選擇性的），請在 hello 虛擬網路和子網路下拉式清單方塊中選取。
   
    成員的可用性設定組的虛擬機器是部署的 toodifferent 容錯網域。 如需詳細資訊，請參閱 [Azure 虛擬網路](https://azure.microsoft.com/services/virtual-network/) 。
8. 如果您想要您虛擬機器 toobelong tooan 可用性設定組 （亦為選用），選取 hello**指定可用性設定組**核取方塊，然後選擇 可用性設定組 hello 下拉式清單方塊中。 當您完成時，選擇 hello**下一步** 按鈕。
   
    新增虛擬機器 tooan 可用性設定組可協助您保持可用狀態網路失敗、 本機磁碟硬體故障和任何規劃的停機期間的應用程式。 您需要 toouse hello [Azure 管理入口網站](http://go.microsoft.com/fwlink/?LinkID=253103)toocreate 虛擬網路、 子網路和可用性設定。 請參閱[管理 hello 虛擬機器可用性](https://azure.microsoft.com/documentation/articles/manage-availability-virtual-machines/)如需詳細資訊。
9. 在 hello**端點**頁面上，指定您想要的虛擬機器的可用 toousers hello 公用端點。 例如，您可能會選擇 tooenable HTTP (連接埠 80) 此外 toohello 遠端桌面和 PowerShell 端點，其中預設會啟用。 tooadd 的端點，請選擇其中一個在 hello**連接埠名稱**下拉式清單方塊，然後選擇 [hello**新增**] 按鈕。 將端點，tooremove 選擇紅色 hello **X** hello 端點清單中的下一個 toohello 名稱。
   
    ![hello 虛擬機器精靈中的 hello 端點頁面。](./media/virtual-machines-common-classic-create-manage-visual-studio/IC718351.png)
   
    hello 端點可用取決於您所選取虛擬機器的 hello 雲端服務。 如需詳細資訊，請參閱 [Azure 服務端點](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/) 。
   
   > [!NOTE]
   > 啟用公用端點讓服務在您的虛擬機器可用 toohello 網際網路。 要確定 tooinstall 和 hello 端點和服務在上正確設定您的虛擬機器，例如 hello 端點設定存取控制清單 (Acl)。 請參閱[如何 tooSet 端點 tooa 虛擬機器](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/)如需詳細資訊。
   > 
   > 
10. 您完成設定 hello 虛擬機器設定之後，請選擇 hello**建立**按鈕 toocreate hello 虛擬機器。
    
     當 Azure 建立 hello 虛擬機器，hello **Azure 活動記錄檔**顯示 hello hello 虛擬機器建立作業的進度。
    
     ![虛擬機器活動記錄 - 進行中。](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744138.png)
    
     tooview 唯一的虛擬機器資訊中，選擇 hello**虛擬機器** 索引標籤中 hello **Azure 活動記錄檔**。
    
     ![虛擬機器活動記錄 - 已完成。](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744139.png)
    
     如果 hello 作業順利完成，hello 新的虛擬機器會出現 hello**虛擬機器**在伺服器總管 中的節點。 您可以登入，依序按一下 hello**使用遠端桌面連線**捷徑。
    
     ![出現在 [伺服器總管] 中的虛擬機器。](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744140.png)

## <a name="manage-your-virtual-machines"></a>管理虛擬機器
在 hello 虛擬機器組態 頁面上，除了 tooshutting 向下的、 連接、 重新整理，以及新增檢查點 toohello 選取虛擬機器，您也可以檢視或變更 hello 虛擬機器的設定。 您可以：

* 變更 hello 虛擬機器大小。
* 選取 hello 可用性設定組 toouse 與 hello 虛擬機器。
* 新增、移除或變更公用端點的設定。
* 新增、移除或設定虛擬機器擴充功能。
* 檢視有關 hello hello 虛擬機器相關聯的磁碟資訊。

### <a name="view-or-change-virtual-machine-settings"></a>檢視或變更虛擬機器設定
1. 在 [伺服器總管] 中，選擇您的虛擬機器在 hello **Azure 虛擬機器**節點。
2. Hello 快顯功能表上，選擇**設定**tooview hello 虛擬機器組態 頁面。
   
    ![hello Azure 虛擬機器組態 頁面](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744141.png)
3. 檢視 hello 虛擬機器資訊或變更它。

### <a name="save-or-restore-hello-status-of-your-virtual-machine"></a>儲存或還原虛擬機器的 hello 狀態
當您設定虛擬機器，並在其上安裝軟體，藉由建立虛擬機器檢查點是個不錯的主意 tooregularly 儲存您的進度。 快照集或映像，hello 目前狀態的虛擬機器的檢查點。 如果出錯 hello 虛擬機器，或您想要 tooreconfigure hello 虛擬機器，您可以將它還原 tooa 先前的檢查點狀態，而不是從頭來節省時間。

### <a name="toocreate-a-virtual-machine-checkpoint"></a>toocreate 虛擬機器檢查點
1. 在 [伺服器總管] 中，選擇您的虛擬機器在 hello **Azure 虛擬機器**節點。
2. Hello 快顯功能表上，選擇**設定**tooview hello 虛擬機器組態 頁面。
3. 在 hello 組態頁面上，選擇 [hello**擷取映像**] 按鈕。
   
    ![Azure 組態頁面擷取按鈕](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744142.png)
   
    hello**擷取虛擬機器**對話方塊隨即出現。
   
    ![Azure 擷取虛擬機器對話方塊](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744143.png)
4. 提供映像標籤和描述。 系統會提供預設標籤和描述，但您可以用自己的標籤和描述加以覆寫。
5. 如果您已經有這部虛擬機器上執行 Sysprep，選取 hello**我已經在 hello 虛擬機器上執行 Sysprep**方塊。
   
    Sysprep 是一種工具，，以及其他項目，從 hello 虛擬機器的版本的 Windows，讓其他人使用的範本移除系統特定資料。 請參閱[如何 tooCapture 做為範本的 Windows 虛擬機器 tooUse](https://azure.microsoft.com/documentation/articles/virtual-machines-capture-image-windows-server/)如需詳細資訊。 執行 Sysprep 之前先備份 hello VM。
6. 您完成設定 hello 擷取設定值之後，請選擇 hello**擷取**按鈕 toocreate hello 檢查點。
   
    當 Azure 建立 hello 檢查點，hello **Azure 活動記錄檔**顯示 hello hello 作業的進度。
   
    ![擷取虛擬機器檢查點](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744144.png)
   
    Hello 檢查點作業完成時，會看到在 hello **Azure 活動記錄檔**。
   
    ![已完成檢查點作業](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744145.png)

## <a name="toomanage-virtual-machine-checkpoints"></a>toomanage 虛擬機器檢查點
### <a name="toorestore-a-virtual-machine-tooa-previously-saved-state"></a>虛擬機器 tooa toorestore 先前儲存的狀態
* 中所述步驟 hello[逐步： 執行雲端還原的 Microsoft Azure 虛擬機器使用 PowerShell-第 2 部分](http://blogs.technet.com/b/keithmayer/archive/2014/02/04/step-by-step-perform-cloud-restores-of-windows-azure-virtual-machines-using-powershell-part-2.aspx)。

### <a name="toodelete-a-checkpoint"></a>toodelete 檢查點
1. 移 toohello [Azure 管理入口網站](http://go.microsoft.com/fwlink/?LinkID=253103)。
2. 在 hello 虛擬機器組態 頁面上，選擇 hello**映像**hello 頁面頂端的 hello 索引標籤。
3. 選擇您想 toodelete，，然後選擇 hello 的 hello 檢查點**刪除**在 hello hello 頁面底部的按鈕。

## <a name="shut-down-your-virtual-machine"></a>關閉虛擬機器
1. 在 [伺服器總管] 中，選擇您想在 hello 向 tooshut hello 虛擬機器**Azure 虛擬機器**節點。
2. 在 [hello] 快顯功能表上選擇 [hello**關機**命令，或選擇**設定**tooview hello 虛擬機器組態] 頁面，然後選擇 [hello**關機**] 按鈕。

## <a name="next-steps"></a>後續步驟
toolearn 進一步了解建立虛擬機器，請參閱[建立執行 Linux 之虛擬機器](../articles/virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)和[建立執行 Windows hello Azure preview 入口網站中的虛擬機器](../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

