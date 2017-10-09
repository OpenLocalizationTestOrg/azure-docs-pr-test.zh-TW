hello Azure CLI 2.0 可讓您 toocreate 和管理您的 Azure 資源上 macOS、 Linux 及 Windows。 這篇文章詳細說明一些最常見命令 toocreate hello 和管理虛擬機器 (Vm)。

這篇文章需要 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooupgrade，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli)。 您也可以在瀏覽器中使用 [Cloud Shell](/azure/cloud-shell/quickstart)。

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a>Azure CLI 中的基本 Azure Resource Manager 命令
如需詳細說明使用特定的命令列參數和選項，您可以使用 hello 線上命令說明和選項輸入`az <command> <subcommand> --help`。

### <a name="create-vms"></a>建立 VM
| 工作 | Azure CLI 命令 |
| --- | --- |
| 建立資源群組 | `az group create --name myResourceGroup --location eastus` |
| 建立 Linux VM | `az vm create --resource-group myResourceGroup --name myVM --image ubuntults` |
| 建立 Windows VM | `az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter` |

### <a name="manage-vm-state"></a>管理 VM 狀態
| 工作 | Azure CLI 命令 |
| --- | --- |
| 啟動 VM | `az vm start --resource-group myResourceGroup --name myVM` |
| 停止 VM | `az vm stop --resource-group myResourceGroup --name myVM` |
| 解除配置 VM | `az vm deallocate --resource-group myResourceGroup --name myVM` |
| 重新啟動 VM | `az vm restart --resource-group myResourceGroup --name myVM` |
| 重新部署 VM | `az vm redeploy --resource-group myResourceGroup --name myVM` |
| 刪除 VM | `az vm delete --resource-group myResourceGroup --name myVM` |

### <a name="get-vm-info"></a>取得 VM 資訊
| 工作 | Azure CLI 命令 |
| --- | --- |
| 列出 VM | `az vm list` |
| 取得 VM 的相關資訊 | `az vm show --resource-group myResourceGroup --name myVM` |
| 取得 VM 資源的使用量 | `az vm list-usage --location eastus` |
| 取得所有可用的 VM 大小 | `az vm list-sizes --location eastus` |

## <a name="disks-and-images"></a>磁碟和映像
| 工作 | Azure CLI 命令 |
| --- | --- |
| 新增資料磁碟 tooa VM | `az vm disk attach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk --size-gb 128 --new ` |
| 從 VM 移除資料磁碟 | `az vm disk detach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk` |
| 調整磁碟大小 | `az disk update --resource-group myResourceGroup --name myDataDisk --size-gb 256` |
| 製作磁碟的快照集 | `az snapshot create --resource-group myResourceGroup --name mySnapshot --source myDataDisk` |
| 建立 VM 的映像 | `az image create --resource-group myResourceGroup --source myVM --name myImage` |
| 從映像建立 VM | `az vm create --resource-group myResourceGroup --name myNewVM --image myImage` |


## <a name="next-steps"></a>後續步驟
如需其他 hello CLI 命令的範例，請參閱 hello[建立和管理 Linux Vm 以 hello Azure CLI](../articles/virtual-machines/linux/tutorial-manage-vm.md)教學課程。

