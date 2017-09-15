<span data-ttu-id="f34ed-101">取消註冊處理序伺服器的步驟，隨著其與設定伺服器的連線狀態而有所不同。</span><span class="sxs-lookup"><span data-stu-id="f34ed-101">The steps to unregister a process server differs depending on its connection status with the Configuration Server.</span></span>

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a><span data-ttu-id="f34ed-102">取消註冊處於已連線狀態的處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="f34ed-102">Unregister a process server that is in a connected state</span></span>

1. <span data-ttu-id="f34ed-103">以系統管理員身分遠端登入處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="f34ed-103">Remote into the process server as an Administrator.</span></span>
2. <span data-ttu-id="f34ed-104">啟動 [控制台] 並開啟 [程式集] > [解除安裝程式]</span><span class="sxs-lookup"><span data-stu-id="f34ed-104">Launch the **Control Panel** and open **Programs > Uninstall a program**</span></span>
3. <span data-ttu-id="f34ed-105">解除安裝名為 **Microsoft Azure Site Recovery Configuration/Process Server** 的程式</span><span class="sxs-lookup"><span data-stu-id="f34ed-105">Uninstall a program by the name **Microsoft Azure Site Recovery Configuration/Process Server**</span></span>
4. <span data-ttu-id="f34ed-106">完成步驟 3 後，您就可以解除安裝 **Microsoft Azure Site Recovery Configuration/Process Server 相依項目**</span><span class="sxs-lookup"><span data-stu-id="f34ed-106">Once step 3 is completed, you can uninstall **Microsoft Azure Site Recovery Configuration/Process Server Dependencies**</span></span>

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a><span data-ttu-id="f34ed-107">取消註冊處於已中斷連線狀態的處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="f34ed-107">Unregister a process server that is in a disconnected state</span></span>

> [!WARNING]
> <span data-ttu-id="f34ed-108">如果沒辦法恢復處理序伺服器安裝所在的虛擬機器，使用下列步驟應很有用。</span><span class="sxs-lookup"><span data-stu-id="f34ed-108">Use the below steps should be used if there is no way to revive the virtual machine on which the Process Server was installed.</span></span>

1. <span data-ttu-id="f34ed-109">以系統管理員身分登入設定伺服器。</span><span class="sxs-lookup"><span data-stu-id="f34ed-109">Log on to your configuration server as an Administrator.</span></span>
2. <span data-ttu-id="f34ed-110">開啟系統管理命令提示字元並瀏覽至目錄 `%ProgramData%\ASR\home\svsystems\bin`。</span><span class="sxs-lookup"><span data-stu-id="f34ed-110">Open an Administrative command prompt and browse to the directory `%ProgramData%\ASR\home\svsystems\bin`.</span></span>
3. <span data-ttu-id="f34ed-111">現在執行命令。</span><span class="sxs-lookup"><span data-stu-id="f34ed-111">Now run the command.</span></span>

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. <span data-ttu-id="f34ed-112">這將會從系統清除處理序伺服器的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f34ed-112">This will purge the details of the process server from the system.</span></span>
