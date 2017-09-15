<span data-ttu-id="d808f-101">在此步驟中，您會使用在相同網路上執行的用戶端應用程式來測試可用性群組接聽程式。</span><span class="sxs-lookup"><span data-stu-id="d808f-101">In this step, you test the availability group listener by using a client application that's running on the same network.</span></span>

<span data-ttu-id="d808f-102">用戶端連線能力具有下列需求：</span><span class="sxs-lookup"><span data-stu-id="d808f-102">Client connectivity has the following requirements:</span></span>

* <span data-ttu-id="d808f-103">對接聽程式的用戶端連線必須來自位於與裝載 AlwaysOn 可用性複本的機器不同雲端服務的機器。</span><span class="sxs-lookup"><span data-stu-id="d808f-103">Client connections to the listener must come from machines that reside in a different cloud service than the one that hosts the Always On availability replicas.</span></span>
* <span data-ttu-id="d808f-104">如果 Always On 複本位於其他子網路中，用戶端必須在連接字串中指定 *MultisubnetFailover=True* 。</span><span class="sxs-lookup"><span data-stu-id="d808f-104">If the Always On replicas are in different subnets, clients must specify *MultisubnetFailover=True* in the connection string.</span></span> <span data-ttu-id="d808f-105">此狀況會導致對各種子網路中的複本進行平行連線嘗試。</span><span class="sxs-lookup"><span data-stu-id="d808f-105">This condition results in parallel connection attempts to replicas in the various subnets.</span></span> <span data-ttu-id="d808f-106">此案例包含跨區域的 Always On 可用性群組部署。</span><span class="sxs-lookup"><span data-stu-id="d808f-106">This scenario includes a cross-region Always On availability group deployment.</span></span>

<span data-ttu-id="d808f-107">其中一個範例是從相同 Azure 虛擬網路中的其中一部 VM (但不是裝載複本的 VM) 連線到接聽程式。</span><span class="sxs-lookup"><span data-stu-id="d808f-107">One example is to connect to the listener from one of the VMs in the same Azure virtual network (but not one that hosts a replica).</span></span> <span data-ttu-id="d808f-108">完成這項測試的簡單方法是嘗試將 SQL Server Management Studio 連線到可用性群組接聽程式。</span><span class="sxs-lookup"><span data-stu-id="d808f-108">An easy way to complete this test is to try to connect SQL Server Management Studio to the availability group listener.</span></span> <span data-ttu-id="d808f-109">另一種簡單的方法是執行 [SQLCMD.exe](https://technet.microsoft.com/library/ms162773.aspx)，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d808f-109">Another simple method is to run [SQLCMD.exe](https://technet.microsoft.com/library/ms162773.aspx), as follows:</span></span>

    sqlcmd -S "<ListenerName>,<EndpointPort>" -d "<DatabaseName>" -Q "select @@servername, db_name()" -l 15

> [!NOTE]
> <span data-ttu-id="d808f-110">如果 EndpointPort 值為 1433，則不需要在呼叫中指定。</span><span class="sxs-lookup"><span data-stu-id="d808f-110">If the EndpointPort value is *1433*, you are not required to specify it in the call.</span></span> <span data-ttu-id="d808f-111">前一個呼叫也假設用戶端電腦已加入相同的網域，而且已使用 Windows 驗證授與呼叫端對資料庫的權限。</span><span class="sxs-lookup"><span data-stu-id="d808f-111">The previous call also assumes that the client machine is joined to the same domain and that the caller has been granted permissions on the database by using Windows authentication.</span></span>
> 
> 

<span data-ttu-id="d808f-112">測試接聽程式時，請務必容錯移轉可用性群組，以確定用戶端可以跨容錯移轉連線至接聽程式。</span><span class="sxs-lookup"><span data-stu-id="d808f-112">When you test the listener, be sure to fail over the availability group to make sure that clients can connect to the listener across failovers.</span></span>

