您可以使用之前 hello Azure CLI 與資源管理員命令和範本 toodeploy Azure 資源和工作負載使用資源群組，您必須使用 Azure 帳戶。 如果您沒有帳戶，可以取得 [此處免費試用的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)。

如果您尚未安裝 hello Azure CLI 連線的 tooyour 訂用帳戶，請參閱[安裝 hello Azure CLI](../articles/cli-install-nodejs.md)太設定 hello 模式`arm`與`azure config mode arm`，並以 hello 連接 tooAzure`azure login`命令。

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作
您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

- Azure CLI 10 – 我們 CLI hello 傳統和資源管理部署模型 （此文件）
- [Azure CLI 2.0](../articles/virtual-machines/linux/cli-manage.md) -hello 資源管理部署模型我們下一個層代 CLI

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a>Azure CLI 中的基本 Azure Resource Manager 命令
本文涵蓋基本的命令，您會想要使用 Azure CLI toomanage toouse 並與其互動您 Azure 訂用帳戶中的資源 (主要 Vm)。  如需詳細說明使用特定的命令列參數和選項，您可以使用 hello 線上命令說明和選項輸入`azure <command> <subcommand> --help`或`azure help <command> <subcommand>`。

> [!NOTE]
> 這些範例不包含以範本為基礎的作業，這些作業一般建議在資源管理員中針對 VM 部署使用。 資訊，請參閱[使用 hello Azure CLI 與 Azure 資源管理員](../articles/xplat-cli-azure-resource-manager.md)和[部署和管理虛擬機器使用的 Azure Resource Manager 範本和 hello Azure CLI](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
> 
> 

| Task | Resource Manager |
| --- | --- | --- |
| 建立 hello 最基本的 VM |`azure vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password>`<br/><br/>(取得 hello`image-urn`從 hello`azure vm image list`命令。 如需範例，請參閱[這篇文章](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。) |
| 建立 Linux VM |`azure  vm create [options] <resource-group> <name> <location> -y "Linux"` |
| 建立 Windows VM |`azure  vm create [options] <resource-group> <name> <location> -y "Windows"` |
| 列出 VM |`azure  vm list [options]` |
| 取得 VM 的相關資訊 |`azure  vm show [options] <resource_group> <name>` |
| 啟動 VM |`azure vm start [options] <resource_group> <name>` |
| 停止 VM |`azure vm stop [options] <resource_group> <name>` |
| 解除配置 VM |`azure vm deallocate [options] <resource-group> <name>` |
| 重新啟動 VM |`azure vm restart [options] <resource_group> <name>` |
| 刪除 VM |`azure vm delete [options] <resource_group> <name>` |
| 擷取 VM |`azure vm capture [options] <resource_group> <name>` |
| 從使用者映像建立 VM |`azure  vm create [options] –q <image-name> <resource-group> <name> <location> <os-type>` |
| 從特殊化磁碟建立 VM |`azue  vm create [options] –d <os-disk-vhd> <resource-group> <name> <location> <os-type>` |
| 新增資料磁碟 tooa VM |`azure  vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]` |
| 從 VM 移除資料磁碟 |`azure  vm disk detach [options] <resource-group> <vm-name> <lun>` |
| 加入泛型擴充 tooa VM |`azure  vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>` |
| 新增 VM 存取延伸 tooa VM |`azure vm reset-access [options] <resource-group> <name>` |
| 將 Docker 擴充功能 tooa VM |`azure  vm docker create [options] <resource-group> <name> <location> <os-type>` |
| 移除 VM 延伸模組 |`azure  vm extension set [options] –u <resource-group> <vm-name> <name> <publisher-name> <version>` |
| 取得 VM 資源的使用量 |`azure vm list-usage [options] <location>` |
| 取得所有可用的 VM 大小 |`azure vm sizes [options]` |

## <a name="next-steps"></a>後續步驟
* 除了基本 VM 管理之外的 hello CLI 命令的其他範例，請參閱[使用 hello Azure CLI 與 Azure 資源管理員](../articles/virtual-machines/azure-cli-arm-commands.md)。
