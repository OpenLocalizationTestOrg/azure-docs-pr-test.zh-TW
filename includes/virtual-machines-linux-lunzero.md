<span data-ttu-id="94066-101">當加入資料磁碟 tooa Linux VM，如果磁碟不存在的 LUN 0 可能會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="94066-101">When adding data disks tooa Linux VM, you may encounter errors if a disk does not exist at LUN 0.</span></span> <span data-ttu-id="94066-102">如果您要新增磁碟，以手動方式使用 hello`azure vm disk attach-new`命令，並指定 LUN (`--lun`) 而不是允許 hello Azure 平台 toodetermine hello 適當的 LUN，請特別注意，磁碟已存在 / 端 LUN 0 將會存在。</span><span class="sxs-lookup"><span data-stu-id="94066-102">If you are adding a disk manually using hello `azure vm disk attach-new` command and you specify a LUN (`--lun`) rather than allowing hello Azure platform toodetermine hello appropriate LUN, take care that a disk already exists / will exist at LUN 0.</span></span> 

<span data-ttu-id="94066-103">請考慮下列範例顯示 hello 輸出的程式碼片段的 hello `lsscsi`:</span><span class="sxs-lookup"><span data-stu-id="94066-103">Consider hello following example showing a snippet of hello output from `lsscsi`:</span></span>

```bash
[5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc 
[5:0:0:1]    disk    Msft     Virtual Disk     1.0   /dev/sdd 
```

<span data-ttu-id="94066-104">hello 兩個資料磁碟存在於 LUN 0 和 LUN 1 (hello hello 第一個資料行`lsscsi`輸出詳細資料`[host:channel:target:lun]`)。</span><span class="sxs-lookup"><span data-stu-id="94066-104">hello two data disks exist at LUN 0 and LUN 1 (hello first column in hello `lsscsi` output details `[host:channel:target:lun]`).</span></span> <span data-ttu-id="94066-105">這兩個磁碟都 accessbile 從 hello VM 內。</span><span class="sxs-lookup"><span data-stu-id="94066-105">Both disks should be accessbile from within hello VM.</span></span> <span data-ttu-id="94066-106">如果您已手動指定 hello 增加 LUN 1 與 LUN 2 hello 第二個磁碟第一個磁碟 toobe，您可能無法看見 hello 磁碟正確從 VM 內。</span><span class="sxs-lookup"><span data-stu-id="94066-106">If you had manually specified hello first disk toobe added at LUN 1 and hello second disk at LUN 2, you may not see hello disks correctly from within your VM.</span></span>

> [!NOTE]
> <span data-ttu-id="94066-107">hello Azure`host`值為 5，在這些範例中，但這會根據您選取的儲存體的 hello 類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="94066-107">hello Azure `host` value is 5 in these examples, but this may vary depending on hello type of storage you select.</span></span>
> 
> 

<span data-ttu-id="94066-108">此磁碟行為不是 Azure 的問題，而 hello 方法中的 hello Linux 核心遵循 hello SCSI 規格。</span><span class="sxs-lookup"><span data-stu-id="94066-108">This disk behavior is not an Azure problem, but hello way in which hello Linux kernel follows hello SCSI specifications.</span></span> <span data-ttu-id="94066-109">Hello Linux 核心掃描 hello SCSI 匯流排，附加的裝置，裝置必須位於 LUN 0 hello 系統 toocontinue 掃描其他裝置的順序。</span><span class="sxs-lookup"><span data-stu-id="94066-109">When hello Linux kernel scans hello SCSI bus for attached devices, a device must be found at LUN 0 in order for hello system toocontinue scanning for additional devices.</span></span> <span data-ttu-id="94066-110">如以上所述，因此︰</span><span class="sxs-lookup"><span data-stu-id="94066-110">As such:</span></span>

* <span data-ttu-id="94066-111">檢閱的 hello 輸出`lsscsi`之後加入資料磁碟 tooverify LUN 0 具有磁碟。</span><span class="sxs-lookup"><span data-stu-id="94066-111">Review hello output of `lsscsi` after adding a data disk tooverify that you have a disk at LUN 0.</span></span>
* <span data-ttu-id="94066-112">如果磁碟在 VM 內未正確顯示，請確認 LUN 0 有磁碟。</span><span class="sxs-lookup"><span data-stu-id="94066-112">If your disk does not show up correctly within your VM, verify a disk exists at LUN 0.</span></span>

