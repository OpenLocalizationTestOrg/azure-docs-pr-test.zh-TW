#### <a name="toocreate-public-endpoints-on-hello-cloud-appliance"></a>toocreate hello 雲端應用裝置上的公用端點

1. 登入 toohello Azure 入口網站。
2. 跳過**虛擬機器**，然後選取並按一下 hello 作為您的雲端應用裝置的虛擬機器。
    
3. 您需要 toocreate 網路安全性 (nsg) 規則 toocontrol hello 流量的流量進出虛擬機器。 執行下列步驟 toocreate NSG 規則 hello。
    1. 選擇 [網路安全性群組]。
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. 按一下 hello 預設網路安全性小組呈現。
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. 選取 [輸入安全性規則]。
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. 按一下**+ 加**toocreate 連入的安全性規則。
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        在 [hello 新增連入的安全性規則] 刀鋒視窗：

        1. Hello**名稱**，輸入 hello 下列命名 hello 端點： WinRMHttps。
        
        2. Hello**優先順序**，選取的數字小於 1000年 （即 hello hello 預設規則的優先順序）。 Hello 值越高，hello 優先順序。

        3. 設定 hello**來源**太**任何**。

        4. Hello**服務**，選取**WinRM**。 hello**通訊協定**會自動設定太**TCP**和 hello**連接埠範圍**設定得**5986**。

        5. 按一下**確定**toocreate hello 規則。

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. 最後一個步驟是的 tooassociate 群組與子網路或特定的網路介面的網路安全性。 執行下列步驟 tooassociate hello 您與子網路的網路安全性群組。
    1. 跳過**子網路**。
    2. 按一下 [+ 關聯]。
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. 選取您的虛擬網路，然後選取 hello 適當的子網路。
    4. 按一下**確定**toocreate hello 規則。

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

建立 hello 規則之後，您可以檢視其詳細資料 toodetermine hello 公用虛擬 IP (VIP) 位址。 請記下此位址。


