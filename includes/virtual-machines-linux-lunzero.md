當加入資料磁碟 tooa Linux VM，如果磁碟不存在的 LUN 0 可能會發生錯誤。 如果您要新增磁碟，以手動方式使用 hello`azure vm disk attach-new`命令，並指定 LUN (`--lun`) 而不是允許 hello Azure 平台 toodetermine hello 適當的 LUN，請特別注意，磁碟已存在 / 端 LUN 0 將會存在。 

請考慮下列範例顯示 hello 輸出的程式碼片段的 hello `lsscsi`:

```bash
[5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc 
[5:0:0:1]    disk    Msft     Virtual Disk     1.0   /dev/sdd 
```

hello 兩個資料磁碟存在於 LUN 0 和 LUN 1 (hello hello 第一個資料行`lsscsi`輸出詳細資料`[host:channel:target:lun]`)。 這兩個磁碟都 accessbile 從 hello VM 內。 如果您已手動指定 hello 增加 LUN 1 與 LUN 2 hello 第二個磁碟第一個磁碟 toobe，您可能無法看見 hello 磁碟正確從 VM 內。

> [!NOTE]
> hello Azure`host`值為 5，在這些範例中，但這會根據您選取的儲存體的 hello 類型而有所不同。
> 
> 

此磁碟行為不是 Azure 的問題，而 hello 方法中的 hello Linux 核心遵循 hello SCSI 規格。 Hello Linux 核心掃描 hello SCSI 匯流排，附加的裝置，裝置必須位於 LUN 0 hello 系統 toocontinue 掃描其他裝置的順序。 如以上所述，因此︰

* 檢閱的 hello 輸出`lsscsi`之後加入資料磁碟 tooverify LUN 0 具有磁碟。
* 如果磁碟在 VM 內未正確顯示，請確認 LUN 0 有磁碟。

