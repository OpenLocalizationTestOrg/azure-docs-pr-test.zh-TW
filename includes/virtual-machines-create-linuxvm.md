
1. 登入 tooyour 使用 hello 步驟中所列的 Azure 訂用帳戶[從 hello Azure CLI 1.0 連接 tooAzure](../articles/xplat-cli-connect.md)。

2. 請確定您已在 hello 傳統部署模式下，如下所示：

    ```azurecli
    azure config mode asm
    ```

3. 找出 hello Linux 映像的 hello 可用的映像從 tooload，如下所示：

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    在 Windows 命令提示字元視窗中，請使用 **find** ，而不要使用 grep。
   
4. 使用`azure vm create`toocreate 具有 hello 上述清單中的 hello Linux 映像的 VM。 這個步驟會建立雲端服務及儲存體帳戶。 您也無法連接此 VM tooan 現有雲端服務與`-c`選項。 建立具有 hello toohello Linux 虛擬機器中的 SSH 端點 toolog`-e`選項。 hello 下列範例會建立名為的 VM`myVM`使用 hello`Ubuntu-14_04_4-LTS`映像中 hello`West US`位置，並將使用者名稱`ops`:
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    hello 輸出是 toohello 類似下列範例程式碼：

    ```azurecli
    info:    Executing command vm create
    + Looking up image b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB
    + Looking up cloud service
    info:    cloud service myVM not found.
    + Creating cloud service
    + Retrieving storage accounts
    + Creating VM
    info:    vm create command OK
    ```
   
   > [!NOTE]
   > 針對 Linux 虛擬機器，您必須提供 hello`-e`選項`vm create`。 建立 hello 虛擬機器之後，它就不可能 tooenable SSH。 如需 SSH 的詳細資訊，請參閱[如何透過在 Azure 上的 Linux SSH tooUse](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

5. 您可以確認 hello VM hello 屬性使用 hello`azure vm show`命令。 hello 下列範例會列出資訊的 hello 名為 VM `myVM`:

    ```azurecli   
    azure vm show myVM
    ```

6. 啟動您的 VM 以 hello`azure vm start`命令，如下所示：

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a>後續步驟
如需所有這些命令的 Azure CLI 1.0 虛擬機器的詳細資訊，請閱讀 hello [hello 傳統部署 API 的使用 hello Azure CLI 1.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)。

