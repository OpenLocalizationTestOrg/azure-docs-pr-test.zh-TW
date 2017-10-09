當您不再需要的資料磁碟附加的 tooa 虛擬機器 (VM) 時，您可以輕易地中斷。 當您從中斷連接磁碟 hello VM 時，hello 磁碟不是從儲存體移除它。 若要再次 toouse hello 現有資料 hello 磁碟上的，您可以將它重新附加 toohello 相同的 VM 或另一個。  

> [!NOTE]
> Azure 中的 VM 使用不同類型的磁碟 - 作業系統磁碟、本機暫存磁碟，以及選擇性的資料磁碟。 如需詳細資訊，請參閱[有關虛擬機器的磁碟和 VHD](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 除非您也可以刪除 hello VM，您無法卸離作業系統磁碟。

## <a name="find-hello-disk"></a>找不到 hello 磁碟
您可以卸離來自 VM 的磁碟必須先 toofind 出 hello 識別碼 hello 磁碟 toobe 卸離的 LUN 編號。 toodo，請遵循下列步驟：

1. 開啟 Azure CLI 和[連接 tooyour Azure 訂用帳戶](../articles/xplat-cli-connect.md)。 確定處於 Azure 服務管理模式 (`azure config mode asm`)。
2. 找出哪些磁碟在附加的 tooyour VM。 hello 下列範例會列出 hello 名為 VM 磁碟`myVM`:

    ```azurecli
    azure vm disk list myVM
    ```

    hello 輸出是 toohello 類似下列範例程式碼：

    ```azurecli
    * Fetching disk images
    * Getting virtual machines
    * Getting VM disks
      data:    Lun  Size(GB)  Blob-Name                         OS
      data:    ---  --------  --------------------------------  -----
      data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
      data:    0    30        myDataDisk.vhd
      info:    vm disk list command OK
    ```

3. 請注意 hello LUN 或 hello**邏輯單元編號**想 toodetach hello 磁碟。

## <a name="remove-operating-system-references-toohello-disk"></a>移除作業系統參考 toohello 磁碟
卸離 hello 磁碟中的 hello Linux 客體之前, 您應該確定 hello 磁碟上的所有磁碟分割不在使用中。 請確定該 hello 作業系統不會嘗試 tooremount 它們之後重新開機。 下列步驟復原可能時所建立的 hello 組態[附加](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)hello 磁碟。

1. 使用 hello`lsscsi`命令 toodiscover hello 磁碟識別碼。 您可透過 `yum install lsscsi` (Red Hat 式散發) 或 `apt-get install lsscsi`(Debian 式散發) 來安裝 `lsscsi`。 您可以找到您要使用的 LUN 編號 hello 尋找 hello 磁碟識別碼。 hello hello tuple 中每個資料列中的最後一個號碼為 hello LUN。 在下列範例從 hello `lsscsi`，LUN 0 太對應  */開發/sdc*

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. 使用`fdisk -l <disk>`toodiscover hello 磁碟分割與 hello 磁碟 toobe 卸離相關聯。 hello 下列範例顯示 hello 輸出`/dev/sdc`:

    ```bash
    Disk /dev/sdc: 1098.4 GB, 1098437885952 bytes, 2145386496 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x5a1d2a1a
    
        Device Boot      Start         End      Blocks   Id  System
    /dev/sdc1            2048  2145386495  1072692224   83  Linux
    ```

3. 取消掛接 hello 磁碟列出每個資料分割。 hello 下例取消掛接`/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

4. 使用 hello`blkid`命令 toodiscovery hello Uuid 之所有資料分割。 hello 輸出是 toohello 類似下列範例程式碼：

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. 移除項目在 hello **/etc/hosts fstab**與 hello 裝置路徑或 Uuid hello 磁碟 toobe 卸離的所有資料分割相關聯的檔案。  此範例中的項目可能是︰

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    或
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-hello-disk"></a>卸離 hello 磁碟
您找出 hello LUN 數目 hello 磁碟和移除的 hello 作業系統參考之後，您便準備好 toodetach 它：

1. 從卸離 hello 選取的磁碟 hello 虛擬機器執行 hello 命令`azure vm disk detach
   <virtual-machine-name> <LUN>`。 hello 下列範例會卸離 LUN `0` hello 名為 VM 從`myVM`:
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. 您可以檢查是否 hello 磁碟已卸離執行`azure vm disk list`一次。 下列範例會檢查 hello hello 名為 VM `myVM`:
   
    ```azurecli
    azure vm disk list myVM
    ```

    hello 輸出類似 toohello 之後，範例中，會顯示 hello 資料磁碟已不再連接：

    ```azurecli
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
     info:    vm disk list command OK
    ```

hello 卸離磁碟留在儲存體，但已不再附加的 tooa 虛擬機器。

