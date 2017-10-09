

建立 Azure 的 Web 應用程式專案時，您可以在 Azure 中佈建虛擬機器。 您可以再設定 hello 虛擬機器與其他軟體，或使用 hello 虛擬機器進行診斷或偵錯。

toocreate 虛擬機器，當您建立 web 應用程式，請遵循下列步驟：

1. 在 Visual Studio 中，按一下 **檔案** > **新增** > **專案** > **Web**，然後選擇 **ASP.NET Web 應用程式**(下 hello **Visual C#**或**Visual Basic**節點)。
2. 在 hello**新增 ASP.NET 專案**對話方塊中，選取 hello 類型 web 應用程式，並在 hello Azure hello 對話方塊 （位於 hello 右下角） 區段，請確定該 hello **hello 雲端中的主機**選取核取方塊 (此核取方塊會標示為**建立遠端資源**某些安裝中)。
   
    ![][0]
3. 此範例中，在 Microsoft Azure 的 hello 下拉式清單中選擇 [**虛擬機器 (v1)**，然後按一下hello**確定**] 按鈕。
4. 登入 tooAzure 如果系統提示您輸入。 hello**建立虛擬機器** 對話方塊隨即出現。
   
    ![][2]
5. 在 hello **DNS 名稱**方塊中，輸入 hello 虛擬機器的名稱。 hello DNS 名稱必須是在 Azure 中是唯一的。 如果您輸入的 hello 名稱無法使用，則會出現紅色驚嘆號。
6. 在 hello**映像**清單中，選擇您想要讓 toobase hello 虛擬機器的 hello 映像。 您可以選擇任何 hello 標準 Azure 虛擬機器映像或您已上傳 tooAzure 的映像。
7. 保留 hello**啟用 IIS 和 Web Deploy**選取除非您計劃 tooinstall 不同的網頁伺服器的核取方塊。 如果您停用 Web Deploy，將無法從 Visual Studio 無法 toopublish。 您可以新增 IIS 和 Web Deploy tooany hello 封裝 Windows Server 映像，包括您自己的自訂映像。
8. 在 hello**大小**清單中，選擇 hello hello 虛擬機器大小。
9. 指定 hello 登入此虛擬機器的認證。 請記下它們，因為您需要它們 tooaccess hello 透過遠端桌面的電腦。
10. 在 hello**位置**清單中，選擇 hello 區域 toohost hello 虛擬機器。
11. 按一下 hello**確定**按鈕 toostart 建立 hello 的虛擬機器。 您可以依照 hello 作業進度的 hello 在 hello**輸出**視窗。
    
    ![][3]
12. Hello 虛擬機器已佈建時，會建立已發行的指令碼中**PublishScripts**方案中的節點。 hello 已發行的指令碼執行和佈建虛擬機器在 Azure 中。 hello**輸出** 視窗會顯示 hello 狀態。 hello 指令碼會執行下列動作 tooset hello 虛擬機器的 hello:
    
    * 如果不存在，請建立 hello 虛擬機器。
    * 建立儲存體帳戶名稱的開頭與`devtest`，但前提是已經沒有儲存體帳戶 hello 指定區域中。
    * 建立雲端服務，為容器的 hello 虛擬機器，並建立 hello web 應用程式的 web 角色。
    * Hello 虛擬機器上，會設定 Web Deploy。
    * 設定 IIS 和 ASP.NET hello 虛擬機器上。
    
    ![][4]
13. （選擇性）您可以連接 toohello 新的虛擬機器。 在**伺服器總管**，依序展開 hello**虛擬機器**節點，選擇 hello 節點 hello 您所建立的虛擬機器和其捷徑功能表上，選擇**使用遠端桌面連線**. 或者，在**Cloud Explorer**您可以選擇**在入口網站中開啟**hello 快顯功能表且 toohello 虛擬機器連線。
    
    ![][5]

## <a name="next-steps"></a>後續步驟
如果您想 toocustomize hello 已發行的指令碼在建立時，讀取在深入資訊[使用 Windows PowerShell 指令碼 tooPublish tooDev 和測試環境](http://msdn.microsoft.com/library/dn642480.aspx)。

[0]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_NewProject.PNG
[1]: ./media/dotnet-visual-studio-create-virtual-machine/CreateVM_SignIn.PNG
[2]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_CreateVM.PNG
[3]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_Provisioning.png
[4]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_SolutionExplorer.png
[5]: ./media/virtual-machines-common-classic-web-app-visual-studio/VS_Create_VM_Connect.png
