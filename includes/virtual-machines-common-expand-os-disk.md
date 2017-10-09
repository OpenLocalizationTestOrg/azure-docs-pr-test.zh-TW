## <a name="overview"></a>概觀
當您建立新的虛擬機器 (VM) 的資源群組中的部署映像從[Azure Marketplace](https://azure.microsoft.com/marketplace/)，hello 預設作業系統磁碟機是 127 GB。 即使它可能 tooadd 資料磁碟 toohello VM （hello SKU 多少根據您選擇），此外建議的 tooinstall 應用程式和在這些增補磁碟上的 CPU 密集型工作負載會有時候客戶必須 tooexpand hello OS磁碟機 toosupport 特定案例，例如下列：

1. 支援將元件安裝在作業系統磁碟機上的舊型應用程式。
2. 從具有較大作業系統磁碟機的內部部署移轉實體電腦或虛擬機器。

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種：資源管理員和傳統。 本文件涵蓋使用 hello 資源管理員的模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。
> 
> 

## <a name="resize-hello-os-drive"></a>調整 hello 作業系統磁碟機
本文章中我們將完成的調整大小 hello 作業系統磁碟機使用的資源管理員模組 hello 工作[Azure Powershell](/powershell/azureps-cmdlets-docs)。 在系統管理模式中開啟您的 Powershell ISE 或 Powershell 視窗，並依照下列步驟執行 hello:

1. 登入 tooyour Microsoft Azure 帳戶中資源管理模式，並選取您的訂用帳戶，如下所示：
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. 設定資源群組名稱和 VM 名稱，如下所示：
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. 取得參考 tooyour VM，如下所示：
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. 停止 hello VM，然後再調整 hello 磁碟大小，如下所示：
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. 與以下是我們所期待的 hello 目前 ！ 設定 hello hello OS 磁碟 toohello 預期值的大小及更新 hello VM，如下所示：
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > hello 新大小應該大於 hello 現有的磁碟大小。 hello 允許最大值為 1023 GB。
   > 
   > 
6. 更新 hello VM 可能需要幾秒鐘的時間。 一旦 hello 命令完成執行後，重新啟動 hello VM，如下所示：
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

這樣就大功告成了！ 現在 RDP 到 hello VM，開啟 電腦管理 （或磁碟管理），並展開 hello 磁碟機使用 hello 新配置的空間。

## <a name="summary"></a>摘要
在本文中，我們會使用 Azure 資源管理員的 Powershell tooexpand hello IaaS 虛擬機器的作業系統磁碟機的模組。 重現下面是供您參考 hello 完整的指令碼：

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a>後續步驟
在本文中，我們會著重於擴充的 hello VM hello OS 磁碟，但 hello 開發的指令碼也可用擴充 hello 資料磁碟附加的 toohello VM，藉由變更一行程式碼。 例如，tooexpand hello 第一個資料磁碟附加的 toohello VM，取代 hello```OSDisk```物件```StorageProfile```與```DataDisks```陣列並使用數值索引 tooobtain 參考 toofirst 附加的資料磁碟，如下所示：

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
同樣地，您便可以參考其他資料磁碟附加的 toohello VM，如上所示，使用索引上，或者 hello ```Name``` hello 磁碟，如下所示的屬性：

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

如果您想 toofind 出 tooattach 磁碟 tooan Azure 資源管理員 VM 的方式，請檢查這[文章](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

