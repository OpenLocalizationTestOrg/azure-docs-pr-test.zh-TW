1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。

2. 從開始 hello 左上方，按一下**新增 > 計算 > Windows Server 2016 Datacenter**。

    ![瀏覽 toohello hello 入口網站中的 Azure VM 映像](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. 在 Windows Server 2016 Datacenter hello，選取 hello 傳統部署模型。 按一下 [建立]。

    ![顯示可用在 hello 入口網站中的 hello Azure VM 映像的螢幕擷取畫面](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a>1.基本概念刀鋒視窗

刀鋒視窗中的基本概念 hello 要求 hello 虛擬機器的系統管理資訊。

1. 輸入**名稱**hello 虛擬機器。 在 hello 範例_HeroVM_ hello hello 虛擬機器名稱。 hello 名稱必須是 1 到 15 個字元，而且它不能包含特殊字元。

2. 輸入**使用者名**和強式**密碼**所使用的 toocreate hello VM 上的本機帳戶。 hello 使用本機帳戶是在 tooand toosign 管理 hello VM。 在 hello 範例_azureuser_是 hello 的使用者名稱。

 hello 密碼必須介於 8 123 個字元並符合個 hello 四個下列複雜性需求的三種： 一個小寫字元、 一個大寫字元、 一個數字和一個特殊字元。 進一步了解 [使用者名稱和密碼需求](../articles/virtual-machines/windows/faq.md)。

3. hello**訂用帳戶**是選擇性的。 一個常見的設定是「隨用隨付」。

4. 選取現有**資源群組**或新的型別 hello 名稱。 在 hello 範例_HeroVMRG_ hello hello 資源群組名稱。

5. 選取 Azure 資料中心**位置**想 hello VM toorun。 在 hello 範例**美國東部**hello 位置。

6. 當您完成之後時，按一下 [**下一步**toocontinue toohello 下一步] 刀鋒視窗。

    ![顯示 hello 設定 hello 設定 Azure VM 的基本概念 刀鋒視窗的螢幕擷取畫面](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a>2.大小刀鋒視窗

hello 大小刀鋒視窗可識別 hello VM，hello 設定詳細資料，並列出包含作業系統、 處理器數目、 磁碟儲存體類型及預估每月的使用成本的各種選項。  

選擇 VM 大小，然後按一下**選取**toocontinue。 在此範例中， _DS1_\__V2 標準_是 hello 的 VM 大小。

  ![顯示 hello Azure VM 大小，您可以選取的 hello 大小刀鋒視窗的螢幕擷取畫面](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a>3.設定刀鋒視窗

hello 設定 刀鋒視窗會要求儲存體和網路的選項。 您可以接受 hello 預設設定。 Azure 會視需要建立適當的項目。

如果您選取支援的虛擬機器大小，就能藉由選取 [磁碟類型] 中的 [進階 (SSD)]，嘗試使用 Azure 進階儲存體。

當您完成變更時，請按一下 [確定] 。

## <a name="4-summary-blade"></a>4.摘要刀鋒視窗

hello 摘要刀鋒視窗會列出 hello hello 先前刀鋒視窗中指定的設定。 按一下**確定**當您準備好 toomake hello 映像。

 ![刀鋒視窗中摘要報表中，提供指定 hello 虛擬機器的設定](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

Hello 入口網站建立 hello 虛擬機器之後，會列出下 hello 新虛擬機器**所有資源**，並顯示 hello 虛擬機器的並排顯示 hello 儀表板上。 hello 對應雲端服務和儲存體帳戶也會建立並列出。 Hello 虛擬機器和雲端服務會自動啟動，而其狀態會列為**執行**。

 ![設定 VM 代理程式 」 和 「 hello hello 虛擬機器端點](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
