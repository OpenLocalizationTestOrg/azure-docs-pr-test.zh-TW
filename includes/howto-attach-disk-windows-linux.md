


## <a name="attach-an-empty-disk"></a>連接空的磁碟
連接空磁碟是簡單的方式 tooadd 資料磁碟，因為 Azure 會為您建立 hello.vhd 檔案，並將它儲存在 hello 儲存體帳戶。

1. 按一下**虛擬機器 （傳統）**，，然後選取 hello 適當的 VM。

2. 在 hello 設定 功能表，按一下 **磁碟**。

   ![連接新的空磁碟](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. Hello 命令列上，按一下**附加新**。  
    hello**附加新磁碟** 對話方塊隨即出現。

    ![附加新的磁碟](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    填寫下列資訊的 hello:
    - 在**檔案名稱**、 接受 hello 預設名稱，或輸入另一種用於 hello.vhd 檔案。 hello 資料磁碟會使用自動產生的名稱，即使您輸入 hello.vhd 檔案的另一個名稱。
    - 選取 hello**類型**hello 資料磁碟。 所有虛擬機器皆支援標準磁碟。 許多虛擬機器也支援進階磁碟。
    - 選取 hello**大小 (GB)** hello 資料磁碟。
    - 在 [主機快取] 中選擇 [無] 或 [唯讀]。
    - 按一下 [確定] toofinish。

4. Hello 資料磁碟會建立並附加之後，它被列在 hello VM hello 磁碟 區段中。

   ![成功連結新的空白資料磁碟](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> 新增資料磁碟之後，您會需要 toolog toohello VM 上的，並使其可以用於初始化 hello 磁碟。

## <a name="how-to-attach-an-existing-disk"></a>做法：連接現有磁碟
連接現有磁碟要求您在儲存體帳戶中需要有可用的 .vhd。 使用 hello [Add-azurevhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet tooupload hello.vhd 檔案 toohello 儲存體帳戶。 在您建立並上傳 hello.vhd 檔案之後，您可以將它附加 tooa VM。

1. 按一下**虛擬機器 （傳統）**，，然後選取 hello 適當的虛擬機器。

2. 在 hello 設定 功能表，按一下 **磁碟**。

3. Hello 命令列上，按一下**附加現有**。

    ![連結資料磁碟](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. 按一下 [位置]。 顯示 hello 可用儲存體帳戶。 接下來，從所列帳戶中選取適當的儲存體帳戶。

    ![提供磁碟儲存體帳戶](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. **儲存體帳戶**會保有一或多個包含磁碟機 (VHD) 的容器。 選取所列出 hello 適當的容器。

    ![提供 virtual-machines-windows 的容器](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. hello **vhd**窗格會列出保留在 hello 容器中的 hello 磁碟機。 按一下其中一個 hello 磁碟，然後按一下選取。

    ![提供 virtual-machines-windows 的磁碟映像](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. hello**將現有磁碟**面板同樣地，會顯示以 hello 位置包含 hello 儲存體帳戶、 容器和選取的硬碟 (vhd) tooadd toohello 虛擬機器。

  設定**主機快取**toonone 或讀取，然後按一下 [確定]。

    ![成功連接資料磁碟](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
