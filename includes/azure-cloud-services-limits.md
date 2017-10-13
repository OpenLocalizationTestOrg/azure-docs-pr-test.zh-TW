| <span data-ttu-id="4d8ee-101">資源</span><span class="sxs-lookup"><span data-stu-id="4d8ee-101">Resource</span></span> | <span data-ttu-id="4d8ee-102">預設限制</span><span class="sxs-lookup"><span data-stu-id="4d8ee-102">Default Limit</span></span> | <span data-ttu-id="4d8ee-103">上限</span><span class="sxs-lookup"><span data-stu-id="4d8ee-103">Maximum Limit</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4d8ee-104">[每一部署的 Web 背景工作角色](../articles/cloud-services/cloud-services-choose-me.md)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="4d8ee-104">[Web/worker roles per deployment](../articles/cloud-services/cloud-services-choose-me.md)<sup>1</sup></span></span> |<span data-ttu-id="4d8ee-105">25</span><span class="sxs-lookup"><span data-stu-id="4d8ee-105">25</span></span> |<span data-ttu-id="4d8ee-106">25</span><span class="sxs-lookup"><span data-stu-id="4d8ee-106">25</span></span> |
| <span data-ttu-id="4d8ee-107">[執行個體輸入端點](http://msdn.microsoft.com/library/gg557552.aspx#InstanceInputEndpoint) </span><span class="sxs-lookup"><span data-stu-id="4d8ee-107">[Instance Input Endpoints](http://msdn.microsoft.com/library/gg557552.aspx#InstanceInputEndpoint) per deployment</span></span> |<span data-ttu-id="4d8ee-108">25</span><span class="sxs-lookup"><span data-stu-id="4d8ee-108">25</span></span> |<span data-ttu-id="4d8ee-109">25</span><span class="sxs-lookup"><span data-stu-id="4d8ee-109">25</span></span> |
| <span data-ttu-id="4d8ee-110">[輸入端點](http://msdn.microsoft.com/library/gg557552.aspx#InputEndpoint) </span><span class="sxs-lookup"><span data-stu-id="4d8ee-110">[Input Endpoints](http://msdn.microsoft.com/library/gg557552.aspx#InputEndpoint) per deployment</span></span> |<span data-ttu-id="4d8ee-111">25</span><span class="sxs-lookup"><span data-stu-id="4d8ee-111">25</span></span> |<span data-ttu-id="4d8ee-112">25</span><span class="sxs-lookup"><span data-stu-id="4d8ee-112">25</span></span> |
| <span data-ttu-id="4d8ee-113">[內部端點](http://msdn.microsoft.com/library/gg557552.aspx#InternalEndpoint) </span><span class="sxs-lookup"><span data-stu-id="4d8ee-113">[Internal Endpoints](http://msdn.microsoft.com/library/gg557552.aspx#InternalEndpoint) per deployment</span></span> |<span data-ttu-id="4d8ee-114">25</span><span class="sxs-lookup"><span data-stu-id="4d8ee-114">25</span></span> |<span data-ttu-id="4d8ee-115">25</span><span class="sxs-lookup"><span data-stu-id="4d8ee-115">25</span></span> |

<span data-ttu-id="4d8ee-116"><sup>1</sup>具有背景工作角色的每個雲端服務均可有兩個部署，一個供生產環境使用，另一個供接移環境使用。</span><span class="sxs-lookup"><span data-stu-id="4d8ee-116"><sup>1</sup>Each Cloud Service with Web/Worker roles can have two deployments, one for production and one for staging.</span></span> <span data-ttu-id="4d8ee-117">也請注意，這項限制是指 toohello 數不同的角色 （設定） 和不 hello 的每個角色 （調整） 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="4d8ee-117">Also note that this limit refers toohello number of distinct roles (configuration) and not hello number of instances per role (scaling).</span></span>
