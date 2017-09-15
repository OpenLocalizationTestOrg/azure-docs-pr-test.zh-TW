
1. <span data-ttu-id="44d8c-101">使用[從 Azure CLI 1.0 連接到 Azure](../articles/xplat-cli-connect.md) 中列出的步驟登入 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="44d8c-101">Sign in to your Azure subscription using the steps listed in [Connect to Azure from the Azure CLI 1.0](../articles/xplat-cli-connect.md).</span></span>

2. <span data-ttu-id="44d8c-102">請確定您處於傳統部署模式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="44d8c-102">Make sure you are in the Classic deployment mode as follows:</span></span>

    ```azurecli
    azure config mode asm
    ```

3. <span data-ttu-id="44d8c-103">找出您想要從可用映像載入的 Linux 映像，如下所示：</span><span class="sxs-lookup"><span data-stu-id="44d8c-103">Find out the Linux image that you want to load from the available images as follows:</span></span>

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    <span data-ttu-id="44d8c-104">在 Windows 命令提示字元視窗中，請使用 **find** ，而不要使用 grep。</span><span class="sxs-lookup"><span data-stu-id="44d8c-104">In a Windows command-prompt window, use **find** instead of grep.</span></span>
   
4. <span data-ttu-id="44d8c-105">使用 `azure vm create` 並搭配先前清單中的 Linux 映像建立 VM。</span><span class="sxs-lookup"><span data-stu-id="44d8c-105">Use `azure vm create` to create a VM with the Linux image from the previous list.</span></span> <span data-ttu-id="44d8c-106">這個步驟會建立雲端服務及儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="44d8c-106">This step creates a cloud service and storage account.</span></span> <span data-ttu-id="44d8c-107">您也可以利用 `-c` 選項將此 VM 連接到現有的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="44d8c-107">You could also connect this VM to an existing cloud service with a `-c` option.</span></span> <span data-ttu-id="44d8c-108">建立 SSH 端點以利用 `-e` 選項登入 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="44d8c-108">Create an SSH endpoint to log in to the Linux virtual machine with the `-e` option.</span></span> <span data-ttu-id="44d8c-109">下列範例會建立名為 `myVM` 的 VM，方法是使用 `West US` 位置中的 `Ubuntu-14_04_4-LTS` 映像，並且新增使用者名稱 `ops`：</span><span class="sxs-lookup"><span data-stu-id="44d8c-109">The following example creates a VM named `myVM` using the `Ubuntu-14_04_4-LTS` image in the `West US` location, and adds a user name `ops`:</span></span>
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    <span data-ttu-id="44d8c-110">輸出類似於下列範例：</span><span class="sxs-lookup"><span data-stu-id="44d8c-110">The output is similar to the following example:</span></span>

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
   > <span data-ttu-id="44d8c-111">針對 Linux 虛擬機器，您必須在 `vm create` 中提供 `-e`。</span><span class="sxs-lookup"><span data-stu-id="44d8c-111">For a Linux virtual machine, you must provide the `-e` option in `vm create`.</span></span> <span data-ttu-id="44d8c-112">建立虛擬機器後，就無法啟用 SSH。</span><span class="sxs-lookup"><span data-stu-id="44d8c-112">It is not possible to enable SSH after the virtual machine has been created.</span></span> <span data-ttu-id="44d8c-113">如需 SSH 的詳細資料，請參閱[如何在 Azure 上搭配使用 SSH 和 Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="44d8c-113">For more details on SSH, read [How to Use SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

5. <span data-ttu-id="44d8c-114">您可以使用 `azure vm show` 命令來確認 VM 的屬性。</span><span class="sxs-lookup"><span data-stu-id="44d8c-114">You can verify the attributes of the VM by using the `azure vm show` command.</span></span> <span data-ttu-id="44d8c-115">下列範例會列出名為 `myVM` 的 VM 的資訊：</span><span class="sxs-lookup"><span data-stu-id="44d8c-115">The following example lists information for the VM named `myVM`:</span></span>

    ```azurecli   
    azure vm show myVM
    ```

6. <span data-ttu-id="44d8c-116">使用 `azure vm start` 命令啟動您的 VM，如下所示：</span><span class="sxs-lookup"><span data-stu-id="44d8c-116">Start your VM with the `azure vm start` command as follows:</span></span>

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="44d8c-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="44d8c-117">Next steps</span></span>
<span data-ttu-id="44d8c-118">如需所有 Azure CLI 1.0 虛擬機器命令的詳細資料，請參閱[搭配使用 Azure CLI 1.0 和傳統部署 API](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="44d8c-118">For details on all these Azure CLI 1.0 virtual machine commands, read the [Using the Azure CLI 1.0 with the Classic deployment API](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

