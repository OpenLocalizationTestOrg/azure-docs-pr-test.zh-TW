<span data-ttu-id="8b8df-101">hello 步驟 toounregister 處理序伺服器與 hello 伺服器組態及其連接狀態而有所不同。</span><span class="sxs-lookup"><span data-stu-id="8b8df-101">hello steps toounregister a process server differs depending on its connection status with hello Configuration Server.</span></span>

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a><span data-ttu-id="8b8df-102">取消註冊處於已連線狀態的處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="8b8df-102">Unregister a process server that is in a connected state</span></span>

1. <span data-ttu-id="8b8df-103">遠端 hello 處理序伺服器系統管理員身分登入。</span><span class="sxs-lookup"><span data-stu-id="8b8df-103">Remote into hello process server as an Administrator.</span></span>
2. <span data-ttu-id="8b8df-104">啟動 hello**控制台**並開啟**程式 > 解除安裝程式**</span><span class="sxs-lookup"><span data-stu-id="8b8df-104">Launch hello **Control Panel** and open **Programs > Uninstall a program**</span></span>
3. <span data-ttu-id="8b8df-105">解除安裝程式以 hello 名稱**Microsoft Azure 站台復原設定/處理序伺服器**</span><span class="sxs-lookup"><span data-stu-id="8b8df-105">Uninstall a program by hello name **Microsoft Azure Site Recovery Configuration/Process Server**</span></span>
4. <span data-ttu-id="8b8df-106">完成步驟 3 後，您就可以解除安裝 **Microsoft Azure Site Recovery Configuration/Process Server 相依項目**</span><span class="sxs-lookup"><span data-stu-id="8b8df-106">Once step 3 is completed, you can uninstall **Microsoft Azure Site Recovery Configuration/Process Server Dependencies**</span></span>

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a><span data-ttu-id="8b8df-107">取消註冊處於已中斷連線狀態的處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="8b8df-107">Unregister a process server that is in a disconnected state</span></span>

> [!WARNING]
> <span data-ttu-id="8b8df-108">如果處理序伺服器已安裝哪些 hello 沒有方法 toorevive hello 虛擬機器，則應該使用下列步驟使用 hello。</span><span class="sxs-lookup"><span data-stu-id="8b8df-108">Use hello below steps should be used if there is no way toorevive hello virtual machine on which hello Process Server was installed.</span></span>

1. <span data-ttu-id="8b8df-109">系統管理員身分登入 tooyour 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="8b8df-109">Log on tooyour configuration server as an Administrator.</span></span>
2. <span data-ttu-id="8b8df-110">開啟 系統管理命令提示字元並瀏覽 toohello 目錄`%ProgramData%\ASR\home\svsystems\bin`。</span><span class="sxs-lookup"><span data-stu-id="8b8df-110">Open an Administrative command prompt and browse toohello directory `%ProgramData%\ASR\home\svsystems\bin`.</span></span>
3. <span data-ttu-id="8b8df-111">現在執行 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="8b8df-111">Now run hello command.</span></span>

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. <span data-ttu-id="8b8df-112">這將從 hello 系統清除 hello hello 處理序伺服器詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8b8df-112">This will purge hello details of hello process server from hello system.</span></span>
