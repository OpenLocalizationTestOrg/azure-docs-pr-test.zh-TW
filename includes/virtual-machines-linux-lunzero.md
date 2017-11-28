<span data-ttu-id="73aa6-101">將資料磁碟新增到 Linux VM 時，如果 LUN 0 沒有磁碟，可能會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="73aa6-101">When adding data disks to a Linux VM, you may encounter errors if a disk does not exist at LUN 0.</span></span> <span data-ttu-id="73aa6-102">如果您是藉由使用 `azure vm disk attach-new` 命令並指定 LUN (`--lun`) 來手動新增磁碟，而不是讓 Azure 平台判斷適當的 LUN，則請注意，LUN 0 已經有磁碟或將會有磁碟。</span><span class="sxs-lookup"><span data-stu-id="73aa6-102">If you are adding a disk manually using the `azure vm disk attach-new` command and you specify a LUN (`--lun`) rather than allowing the Azure platform to determine the appropriate LUN, take care that a disk already exists / will exist at LUN 0.</span></span> 

<span data-ttu-id="73aa6-103">請思考一下以下範例，此範例顯示來自 `lsscsi`之輸出的程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="73aa6-103">Consider the following example showing a snippet of the output from `lsscsi`:</span></span>

```bash
[5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc 
[5:0:0:1]    disk    Msft     Virtual Disk     1.0   /dev/sdd 
```

<span data-ttu-id="73aa6-104">兩個資料磁碟存在於 LUN 0 和 LUN 1 (`lsscsi` 輸出中的第 1 欄輸出了詳細資料 `[host:channel:target:lun]`)。</span><span class="sxs-lookup"><span data-stu-id="73aa6-104">The two data disks exist at LUN 0 and LUN 1 (the first column in the `lsscsi` output details `[host:channel:target:lun]`).</span></span> <span data-ttu-id="73aa6-105">兩個磁碟應該都要是可從 VM 內存取的磁碟。</span><span class="sxs-lookup"><span data-stu-id="73aa6-105">Both disks should be accessbile from within the VM.</span></span> <span data-ttu-id="73aa6-106">如果您已手動指定要在 LUN 1 新增第一個磁碟及在 LUN 2 新增第二個磁碟，則從您的 VM 內可能無法正確看見這些磁碟。</span><span class="sxs-lookup"><span data-stu-id="73aa6-106">If you had manually specified the first disk to be added at LUN 1 and the second disk at LUN 2, you may not see the disks correctly from within your VM.</span></span>

> [!NOTE]
> <span data-ttu-id="73aa6-107">在這些範例中，Azure `host` 值為 5，但這可能會依據您選取的儲存體類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="73aa6-107">The Azure `host` value is 5 in these examples, but this may vary depending on the type of storage you select.</span></span>
> 
> 

<span data-ttu-id="73aa6-108">此磁碟行為不是 Azure 問題，而是 Linux 核心遵循 SCSI 規格的方式。</span><span class="sxs-lookup"><span data-stu-id="73aa6-108">This disk behavior is not an Azure problem, but the way in which the Linux kernel follows the SCSI specifications.</span></span> <span data-ttu-id="73aa6-109">當 Linux 核心掃描 SCSI 匯流排是否有已連接的裝置時，必須在 LUN 0 找到裝置，系統才能繼續掃描是否有其他裝置。</span><span class="sxs-lookup"><span data-stu-id="73aa6-109">When the Linux kernel scans the SCSI bus for attached devices, a device must be found at LUN 0 in order for the system to continue scanning for additional devices.</span></span> <span data-ttu-id="73aa6-110">如以上所述，因此︰</span><span class="sxs-lookup"><span data-stu-id="73aa6-110">As such:</span></span>

* <span data-ttu-id="73aa6-111">在新增資料磁碟之後，請檢閱 `lsscsi` 的輸出，以確認 LUN 0 有磁碟。</span><span class="sxs-lookup"><span data-stu-id="73aa6-111">Review the output of `lsscsi` after adding a data disk to verify that you have a disk at LUN 0.</span></span>
* <span data-ttu-id="73aa6-112">如果磁碟在 VM 內未正確顯示，請確認 LUN 0 有磁碟。</span><span class="sxs-lookup"><span data-stu-id="73aa6-112">If your disk does not show up correctly within your VM, verify a disk exists at LUN 0.</span></span>

