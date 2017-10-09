
1. <span data-ttu-id="474ad-101">登入 tooyour 使用 hello 步驟中所列的 Azure 訂用帳戶[從 hello Azure CLI 1.0 連接 tooAzure](../articles/xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="474ad-101">Sign in tooyour Azure subscription using hello steps listed in [Connect tooAzure from hello Azure CLI 1.0](../articles/xplat-cli-connect.md).</span></span>

2. <span data-ttu-id="474ad-102">請確定您已在 hello 傳統部署模式下，如下所示：</span><span class="sxs-lookup"><span data-stu-id="474ad-102">Make sure you are in hello Classic deployment mode as follows:</span></span>

    ```azurecli
    azure config mode asm
    ```

3. <span data-ttu-id="474ad-103">找出 hello Linux 映像的 hello 可用的映像從 tooload，如下所示：</span><span class="sxs-lookup"><span data-stu-id="474ad-103">Find out hello Linux image that you want tooload from hello available images as follows:</span></span>

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    <span data-ttu-id="474ad-104">在 Windows 命令提示字元視窗中，請使用 **find** ，而不要使用 grep。</span><span class="sxs-lookup"><span data-stu-id="474ad-104">In a Windows command-prompt window, use **find** instead of grep.</span></span>
   
4. <span data-ttu-id="474ad-105">使用`azure vm create`toocreate 具有 hello 上述清單中的 hello Linux 映像的 VM。</span><span class="sxs-lookup"><span data-stu-id="474ad-105">Use `azure vm create` toocreate a VM with hello Linux image from hello previous list.</span></span> <span data-ttu-id="474ad-106">這個步驟會建立雲端服務及儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="474ad-106">This step creates a cloud service and storage account.</span></span> <span data-ttu-id="474ad-107">您也無法連接此 VM tooan 現有雲端服務與`-c`選項。</span><span class="sxs-lookup"><span data-stu-id="474ad-107">You could also connect this VM tooan existing cloud service with a `-c` option.</span></span> <span data-ttu-id="474ad-108">建立具有 hello toohello Linux 虛擬機器中的 SSH 端點 toolog`-e`選項。</span><span class="sxs-lookup"><span data-stu-id="474ad-108">Create an SSH endpoint toolog in toohello Linux virtual machine with hello `-e` option.</span></span> <span data-ttu-id="474ad-109">hello 下列範例會建立名為的 VM`myVM`使用 hello`Ubuntu-14_04_4-LTS`映像中 hello`West US`位置，並將使用者名稱`ops`:</span><span class="sxs-lookup"><span data-stu-id="474ad-109">hello following example creates a VM named `myVM` using hello `Ubuntu-14_04_4-LTS` image in hello `West US` location, and adds a user name `ops`:</span></span>
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    <span data-ttu-id="474ad-110">hello 輸出是 toohello 類似下列範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="474ad-110">hello output is similar toohello following example:</span></span>

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
   > <span data-ttu-id="474ad-111">針對 Linux 虛擬機器，您必須提供 hello`-e`選項`vm create`。</span><span class="sxs-lookup"><span data-stu-id="474ad-111">For a Linux virtual machine, you must provide hello `-e` option in `vm create`.</span></span> <span data-ttu-id="474ad-112">建立 hello 虛擬機器之後，它就不可能 tooenable SSH。</span><span class="sxs-lookup"><span data-stu-id="474ad-112">It is not possible tooenable SSH after hello virtual machine has been created.</span></span> <span data-ttu-id="474ad-113">如需 SSH 的詳細資訊，請參閱[如何透過在 Azure 上的 Linux SSH tooUse](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="474ad-113">For more details on SSH, read [How tooUse SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

5. <span data-ttu-id="474ad-114">您可以確認 hello VM hello 屬性使用 hello`azure vm show`命令。</span><span class="sxs-lookup"><span data-stu-id="474ad-114">You can verify hello attributes of hello VM by using hello `azure vm show` command.</span></span> <span data-ttu-id="474ad-115">hello 下列範例會列出資訊的 hello 名為 VM `myVM`:</span><span class="sxs-lookup"><span data-stu-id="474ad-115">hello following example lists information for hello VM named `myVM`:</span></span>

    ```azurecli   
    azure vm show myVM
    ```

6. <span data-ttu-id="474ad-116">啟動您的 VM 以 hello`azure vm start`命令，如下所示：</span><span class="sxs-lookup"><span data-stu-id="474ad-116">Start your VM with hello `azure vm start` command as follows:</span></span>

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="474ad-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="474ad-117">Next steps</span></span>
<span data-ttu-id="474ad-118">如需所有這些命令的 Azure CLI 1.0 虛擬機器的詳細資訊，請閱讀 hello [hello 傳統部署 API 的使用 hello Azure CLI 1.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="474ad-118">For details on all these Azure CLI 1.0 virtual machine commands, read hello [Using hello Azure CLI 1.0 with hello Classic deployment API](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

