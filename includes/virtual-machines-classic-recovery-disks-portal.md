如果您在 Azure 中的虛擬機器 (VM) 會發生開機或磁碟錯誤，您可能需要 tooperform 疑難排解 hello 虛擬硬碟上本身的步驟。 常見範例是防止 hello VM 成功開機失敗的應用程式更新。 本文說明如何 toouse Azure 入口網站 tooconnect 您的虛擬硬碟 tooanother VM toofix 任何錯誤，然後重新建立原始 VM。

## <a name="recovery-process-overview"></a>復原程序概觀
hello 疑難排解程序如下所示：

1. 刪除 hello 發生問題的 VM，但保留 hello 虛擬硬碟。
2. 附加和掛接 hello 虛擬硬碟 tooanother VM 進行疑難排解。
3. 連接 toohello 疑難排解 VM。 編輯檔案，或在 hello 原始虛擬硬碟上執行工具 toofix 錯誤。
4. 取消掛接並卸離 hello 虛擬硬碟從 hello 疑難排解 VM。
5. 使用 hello 原始虛擬硬碟建立 VM。

## <a name="delete-hello-original-vm"></a>刪除 hello 原始 VM
虛擬硬碟和 VM 在 Azure 中是兩個不同的資源。 虛擬硬碟是存放 hello 作業系統、 應用程式和組態的位置。 hello VM 不只是中繼資料，來定義 hello 大小或位置，會參考資源，例如虛擬硬碟或虛擬網路介面卡 (NIC)。 每個虛擬硬碟取得該磁碟已附加的 tooa VM 時指定的租用。 雖然可以附加和卸離 hello VM 正在執行時，即使資料磁碟，除非刪除 hello VM 資源無法中斷 hello 作業系統磁碟。 hello 租用會繼續 tooassociate hello OS 磁碟 tooa VM，即使該 VM 是處於已停止和取消配置狀態。

hello 第一個步驟 toorecovering VM 是 toodelete hello VM 資源本身。 刪除 hello VM 離開您的儲存體帳戶中的 hello 虛擬硬碟。 刪除 VM hello 之後, 您可以附加 hello 虛擬硬碟 tooanother VM tootroubleshoot，並解決 hello 錯誤。 

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。 
2. 在左邊為 hello hello 功能表上，按一下**虛擬機器 （傳統）**。
3. VM 具有 hello 問題，請按一下 選取 hello**磁碟**，然後識別 hello hello 虛擬硬碟的名稱。 
4. 選取 hello 作業系統虛擬硬碟，並檢查 hello**位置**tooidentify hello 儲存體帳戶，其中包含虛擬硬碟。 在下列範例的 hello，hello 字串前面 「。 account>.blob.core.windows.net 」 是 hello 儲存體帳戶名稱。

    ```
    https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd
    ```

    ![VM 的位置相關的 hello 映像](./media/virtual-machines-classic-recovery-disks-portal/vm-location.png)

5. Hello VM 上按一下滑鼠右鍵，然後選取**刪除**。 請確定當您刪除 hello VM 時未選取 hello 磁碟。
6. 建立新的復原 VM。 此 VM 必須在 hello 相同區域或資源群組 （雲端服務） 稱為 hello 問題 VM。
7. 選取 hello 修復 VM，然後選取**磁碟** > **附加現有**。
8. tooselect 現有虛擬硬碟，按一下  **VHD 檔案**:

    ![瀏覽現有 VHD](./media/virtual-machines-classic-recovery-disks-portal/select-vhd-location.png)

9. 選取 hello 儲存體帳戶 > VHD 容器 > hello 虛擬硬碟，請按一下 hello**選取**按鈕 tooconfirm 您的選擇。

    ![選取現有 VHD](./media/virtual-machines-classic-recovery-disks-portal/select-vhd.png)

10. 您現在已選取的 VHD，然後選取 **確定**tooattach hello 現有虛擬硬碟。
11. 幾秒之後，hello**磁碟**vm 的窗格會顯示您現有虛擬硬碟連接當做資料磁碟：

    ![現有虛擬硬碟已連結為資料磁碟](./media/virtual-machines-classic-recovery-disks-portal/attached-disk.png)

## <a name="fix-issues-on-hello-original-virtual-hard-disk"></a>Hello 原始虛擬硬碟上修正問題
當已裝載 hello 現有虛擬硬碟時，您現在可以執行任何維護和疑難排解步驟，視需要。 一旦解決 hello 問題之後，繼續進行步驟 hello。

## <a name="unmount-and-detach-hello-original-virtual-hard-disk"></a>取消掛接並卸離 hello 原始虛擬硬碟
一旦解決的任何錯誤，取消掛接並卸離 hello 現有虛擬硬碟從您疑難排解的 VM。 釋放連接 hello 疑難排解 VM 的虛擬硬碟 toohello hello 租用之前，您無法使用您連同任何其他 VM 的虛擬硬碟。  

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。 
2. 在左邊為 hello hello 功能表上，選取**虛擬機器 （傳統）**。
3. 找出 hello 修復 VM。 選取磁碟，以滑鼠右鍵按一下 hello 磁碟，然後再選取**卸離**。

## <a name="create-a-vm-from-hello-original-hard-disk"></a>從原始硬碟 hello 建立 VM

toocreate 原始虛擬硬碟，從 VM 使用[Azure 傳統入口網站](https://manage.windowsazure.com)。

1. 登入 [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. 在 hello hello 入口網站底部，選取**新增** > **計算** > **虛擬機器** > **從組件庫**.
3. 在 hello**選擇映像**區段中，選取**我的磁碟**，，然後選取 hello 原始虛擬硬碟。 請檢查 hello 位置資訊。 這是 hello hello VM 必須部署所在的區域。 選取 hello 下一步 按鈕。
4. 在 hello**虛擬機器組態**區段中，輸入 hello VM 名稱，然後選取 hello VM 的大小。
