當您不再需要的資料磁碟附加的 tooa 虛擬機器時，您可以輕易地中斷。 卸離磁碟 hello 磁碟移除 hello 虛擬機器，但不會從 hello Azure 儲存體帳戶刪除 hello 磁碟。

若要再次 toouse hello 現有資料 hello 磁碟上的，您可以將它重新附加 toohello 相同的虛擬機器或另一個。  

> [!NOTE]
> toodetach 作業系統磁碟，您必須先 toodelete hello 虛擬機器。
>

## <a name="find-hello-disk"></a>找不到 hello 磁碟
如果您不知道 hello 名稱 hello 磁碟，或想 tooverify 它然後再卸離資料庫，請遵循下列步驟。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。

2. 按一下**虛擬機器**，，然後選取 hello 適當的 VM。

3. 按一下**磁碟**沿著 hello 左邊緣的 hello 虛擬機器儀表板下方**設定**。

 hello 虛擬機器儀表板列出 hello 名稱和類型的所有連接的磁碟。 例如，此畫面會顯示虛擬機器及一個作業系統 (OS) 磁碟和一個資料磁碟：

    ![尋找資料磁碟](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-hello-disk"></a>卸離 hello 磁碟
1. 從 hello Azure 入口網站，按一下 **虛擬機器**，然後按一下hello hello 具有您想 toodetach hello 資料磁碟的虛擬機器的名稱。

2. 按一下**磁碟**沿著 hello 左邊緣的 hello 虛擬機器儀表板下方**設定**。

3. 按一下您想 toodetach 的 hello 磁碟。

  ![識別 hello 磁碟 toodetach](./media/howto-detach-disk-windows-linux/disklist.png)

4. 在 hello 命令列中，按一下**卸離**。

  ![找出 hello 卸離命令](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. 在 hello 確認視窗中，按一下 **是**toodetach hello 磁碟。

  ![確認中斷連接的 hello 磁碟](./media/howto-detach-disk-windows-linux/confirmdetach.png)

hello 磁碟留在儲存體，但已不再附加的 tooa 虛擬機器。
