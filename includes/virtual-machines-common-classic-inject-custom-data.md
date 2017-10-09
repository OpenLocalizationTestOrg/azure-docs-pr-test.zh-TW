


本主題將說明如何：

* 將資料插入正在佈建的 Azure 虛擬機器 (VM)
* 針對 Windows 和 Linux 進行擷取。
* 使用某些系統 toodetect 上可用的特殊工具和自訂資料會自動處理。

> [!NOTE]
> 本文說明如何自訂資料可插入所使用的 hello Azure 服務管理 API 以建立 VM。 如何 toouse hello Azure 資源管理 API，請參閱的 toosee [hello 範例範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata)。
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a>將自訂資料插入 Azure 虛擬機器
這項功能目前只支援 hello [Azure 命令列介面](https://github.com/Azure/azure-xplat-cli)。 我們在這裡建立`custom-data.txt`檔案，其中包含我們的資料，然後插入，在 toohello VM 佈建期間。 雖然您可以使用任何 hello 選項 hello`azure vm create`命令 hello 以下示範非常基本的其中一個方法：

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-hello-virtual-machine"></a>在 hello 虛擬機器中使用自訂資料
* 如果您的 Azure VM 都是 windows VM，則 hello 自訂的資料檔會儲存太`%SYSTEMDRIVE%\AzureData\CustomData.bin`。 雖然它是 base64 編碼 tootransfer hello 本機電腦 toohello 從新的 VM，它會自動解碼，可開啟或立即使用。
  
  > [!NOTE]
  > 如果 hello 檔案存在，則會覆寫。 hello hello 目錄安全性設定得**System： 完全控制**和**Administrators： 完全控制**。
  > 
  > 
* 如果 Azure VM 都是 linux VM，然後 hello 自訂資料檔案將位於 hello 下列其中一種將視您 distro 而定。 hello 資料可能會以 base64 編碼，因此您可能需要 toodecode hello 資料第一次：
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a>Azure 上的 Cloud-Init
如果您的 Azure VM 從 Ubuntu 或 CoreOS 映像，您可以使用 CustomData toosend 雲端組態 toocloud init。 或者，如果您的自訂資料檔案是指令碼，則 cloud-init 只能執行它。

### <a name="ubuntu-cloud-images"></a>Ubuntu 雲端映像
在大部分的 Azure Linux 映像，您會編輯 「 / etc/waagent.conf"tooconfigure hello 暫存資源的磁碟和交換檔。 如需詳細資訊，請參閱[Azure Linux 代理程式使用者指南](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

不過，hello Ubuntu 雲端映像，您必須使用雲端 init tooconfigure hello 資源磁碟 （也就是 hello 「 暫時 」 磁碟），並切換資料分割。 請參閱 hello 遵循頁面上 hello Ubuntu wiki，如需詳細資訊： [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions)。

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps-using-cloud-init"></a>後續步驟：使用 cloud-init
如需詳細資訊，請參閱 hello [Ubuntu 雲端初始化文件](https://help.ubuntu.com/community/CloudInit)。

<!--Link references-->
[加入角色服務管理 REST API 參考](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[Azure 命令列介面](https://github.com/Azure/azure-xplat-cli)

