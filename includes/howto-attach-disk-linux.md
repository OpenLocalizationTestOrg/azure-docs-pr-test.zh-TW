
如需有關磁碟的詳細資訊，請參閱[關於虛擬機器的磁碟和 VHD](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

<a id="attachempty"></a>

## <a name="attach-an-empty-disk"></a>連接空的磁碟
1. 開啟 Azure CLI 1.0 和[連接 tooyour Azure 訂用帳戶](../articles/xplat-cli-connect.md)。 確定處於 Azure 服務管理模式 (`azure config mode asm`)。
2. 輸入`azure vm disk attach-new`toocreate 並附加新的磁碟，hello 下列範例所示。 取代*myVM* hello 同名的 Linux 虛擬機器，並指定 hello hello 磁碟大小以 gb 為單位是*100 GB*在此範例中：

    ```azurecli
    azure vm disk attach-new myVM 100
    ```

3. Hello 資料磁碟會建立並附加之後，它會列在 hello 輸出`azure vm disk list <virtual-machine-name>`hello 下列範例所示：
   
    ```azurecli
    azure vm disk list TestVM
    ```

    hello 輸出是 toohello 類似下列範例程式碼：

    ```bash
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        myVM-2645b8030676c8f8.vhd  Linux
     data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

<a id="attachexisting"></a>

## <a name="attach-an-existing-disk"></a>連接現有磁碟
連接現有磁碟要求您在儲存體帳戶中需要有可用的 .vhd。

1. 開啟 Azure CLI 1.0 和[連接 tooyour Azure 訂用帳戶](../articles/xplat-cli-connect.md)。 確定處於 Azure 服務管理模式 (`azure config mode asm`)。
2. 檢查是否 hello tooattach 已經是您想要的 VHD 上傳 tooyour Azure 訂用帳戶：
   
    ```azurecli
    azure vm disk list
    ```

    hello 輸出是 toohello 類似下列範例程式碼：

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
     data:    Name                                          OS
     data:    --------------------------------------------  -----
     data:    myTestVhd                                     Linux
     data:    TestVM-ubuntuVMasm-0-201508060029150744  Linux
     data:    TestVM-ubuntuVMasm-0-201508060040530369
     info:    vm disk list command OK
    ```

3. 如果找不到 hello 磁碟 toouse，可能會使用上傳本機的 VHD tooyour 訂用帳戶`azure vm disk create`或`azure vm disk upload`。 舉例來說，`disk create`會如 hello 下列範例所示：
   
    ```azurecli
    azure vm disk create myVhd .\TempDisk\test.VHD -l "East US" -o Linux
    ```

    hello 輸出是 toohello 類似下列範例程式碼：

    ```azurecli
    info:    Executing command vm disk create
    + Retrieving storage accounts
    info:    VHD size : 10 GB
    info:    Uploading 10485760.5 KB
    Requested:100.0% Completed:100.0% Running:   0 Time:   25s Speed:    82 KB/s
    info:    Finishing computing MD5 hash, 16% is complete.
    info:    https://mystorageaccount.blob.core.windows.net/disks/myVHD.vhd was
    uploaded successfully
    info:    vm disk create command OK
    ```
   
   您也可以使用`azure vm disk upload`tooupload VHD tooa 特定儲存體帳戶。 閱讀有關 hello 命令 toomanage 您 Azure 虛擬機器的資料磁碟[在這裡](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)。

4. 現在您附加 hello 預期 VHD tooyour 虛擬機器：
   
    ```azurecli
    azure vm disk attach myVM myVhd
    ```
   
   請確定 tooreplace *myVM* hello 名稱，為您的虛擬機器和*myVHD*與您想要的 VHD。

5. 您可以確認 hello 磁碟是虛擬機器附加的 toohello `azure vm disk list <virtual-machine-name>`:
   
    ```azurecli
    azure vm disk list myVM
    ```

    hello 輸出是 toohello 類似下列範例程式碼：

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        TestVM-2645b8030676c8f8.vhd  Linux
     data:    1    10        test.VHD
     data:    0    100        TestVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

> [!NOTE]
> 新增資料磁碟之後，您將需要 toolog toohello 虛擬機器上的，並因此 hello 虛擬機器可以使用 hello 磁碟儲存體初始化 hello 磁碟 （請參閱下列 hello 步驟的詳細資訊 toodo 如何初始化 hello 磁碟上）。
> 
> 

