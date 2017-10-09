# <a name="common-errors-during-classic-tooazure-resource-manager-migration"></a><span data-ttu-id="0ae51-101">在傳統 tooAzure 資源管理員移轉期間的常見錯誤</span><span class="sxs-lookup"><span data-stu-id="0ae51-101">Common errors during Classic tooAzure Resource Manager migration</span></span>
<span data-ttu-id="0ae51-102">此文件類別目錄會從 Azure 傳統部署模型 toohello Azure Resource Manager 堆疊的 IaaS 資源 hello 移轉期間 hello 最常見的錯誤和防護功能。</span><span class="sxs-lookup"><span data-stu-id="0ae51-102">This article catalogs hello most common errors and mitigations during hello migration of IaaS resources from Azure classic deployment model toohello Azure Resource Manager stack.</span></span>

## <a name="list-of-errors"></a><span data-ttu-id="0ae51-103">錯誤清單</span><span class="sxs-lookup"><span data-stu-id="0ae51-103">List of errors</span></span>
| <span data-ttu-id="0ae51-104">錯誤字串</span><span class="sxs-lookup"><span data-stu-id="0ae51-104">Error string</span></span> | <span data-ttu-id="0ae51-105">緩和</span><span class="sxs-lookup"><span data-stu-id="0ae51-105">Mitigation</span></span> |
| --- | --- |
| <span data-ttu-id="0ae51-106">內部伺服器錯誤</span><span class="sxs-lookup"><span data-stu-id="0ae51-106">Internal server error</span></span> |<span data-ttu-id="0ae51-107">在某些情況下，這是隨著重試消失的暫時性錯誤。</span><span class="sxs-lookup"><span data-stu-id="0ae51-107">In some cases, this is a transient error that goes away with a retry.</span></span> <span data-ttu-id="0ae51-108">如果持續 toopersist，[連絡 Azure 支援](../articles/azure-supportability/how-to-create-azure-support-request.md)依其需要調查平台的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0ae51-108">If it continues toopersist, [contact Azure support](../articles/azure-supportability/how-to-create-azure-support-request.md) as it needs investigation of platform logs.</span></span> <br><br> <span data-ttu-id="0ae51-109">**注意：**修訂 hello 事件是由 hello 支援小組，請不要嘗試任何自我補救這可能會有您的環境中預期的結果。</span><span class="sxs-lookup"><span data-stu-id="0ae51-109">**NOTE:** Once hello incident is tracked by hello support team, please do not attempt any self-mitigation as this might have unintended consequences on your environment.</span></span> |
| <span data-ttu-id="0ae51-110">移轉不支援 HostedService {hosted-service-name} 中的部署 {deployment-name}，因為它是 PaaS 部署 (Web/背景工作角色)。</span><span class="sxs-lookup"><span data-stu-id="0ae51-110">Migration is not supported for Deployment {deployment-name}  in HostedService {hosted-service-name} because it is a PaaS deployment (Web/Worker).</span></span> |<span data-ttu-id="0ae51-111">這會在部署包含 Web/背景工作角色時發生。</span><span class="sxs-lookup"><span data-stu-id="0ae51-111">This happens when a deployment contains a web/worker role.</span></span> <span data-ttu-id="0ae51-112">因為僅支援虛擬機器的移轉，請移除 hello 部署的 hello web/背景工作角色，然後再試一次移轉。</span><span class="sxs-lookup"><span data-stu-id="0ae51-112">Since migration is only supported for Virtual Machines, please remove hello web/worker role from hello deployment and try migration again.</span></span> |
| <span data-ttu-id="0ae51-113">範本 {template-name} 部署失敗。</span><span class="sxs-lookup"><span data-stu-id="0ae51-113">Template {template-name} deployment failed.</span></span> <span data-ttu-id="0ae51-114">相互關聯識別碼 = {guid}</span><span class="sxs-lookup"><span data-stu-id="0ae51-114">CorrelationId={guid}</span></span> |<span data-ttu-id="0ae51-115">在 hello 後端中的 移轉服務，我們可以使用 Azure Resource Manager 範本 toocreate 資源 hello Azure Resource Manager 堆疊中。</span><span class="sxs-lookup"><span data-stu-id="0ae51-115">In hello backend of migration service, we use Azure Resource Manager templates toocreate resources in hello Azure Resource Manager stack.</span></span> <span data-ttu-id="0ae51-116">範本是具有等冪性，因為通常您可以安全地重試一次 hello 移轉作業 tooget 忽略錯誤。</span><span class="sxs-lookup"><span data-stu-id="0ae51-116">Since templates are idempotent, usually you can safely retry hello migration operation tooget past this error.</span></span> <span data-ttu-id="0ae51-117">如果此錯誤持續 toopersist，請[連絡 Azure 支援](../articles/azure-supportability/how-to-create-azure-support-request.md)授與他們 hello 的相互關聯識別碼。</span><span class="sxs-lookup"><span data-stu-id="0ae51-117">If this error continues toopersist, please [contact Azure support](../articles/azure-supportability/how-to-create-azure-support-request.md) and give them hello CorrelationId.</span></span> <br><br> <span data-ttu-id="0ae51-118">**注意：**修訂 hello 事件是由 hello 支援小組，請不要嘗試任何自我補救這可能會有您的環境中預期的結果。</span><span class="sxs-lookup"><span data-stu-id="0ae51-118">**NOTE:** Once hello incident is tracked by hello support team, please do not attempt any self-mitigation as this might have unintended consequences on your environment.</span></span> |
| <span data-ttu-id="0ae51-119">hello 虛擬網路 {虛擬-網路-名稱} 不存在。</span><span class="sxs-lookup"><span data-stu-id="0ae51-119">hello virtual network {virtual-network-name} does not exist.</span></span> |<span data-ttu-id="0ae51-120">如果您在 hello 新版 Azure 入口網站中建立 hello 虛擬網路，也可能會發生。</span><span class="sxs-lookup"><span data-stu-id="0ae51-120">This can happen if you created hello Virtual Network in hello new Azure portal.</span></span> <span data-ttu-id="0ae51-121">hello 實際虛擬網路名稱遵循 hello 模式 」 群組 * <VNET name>"</span><span class="sxs-lookup"><span data-stu-id="0ae51-121">hello actual Virtual Network name follows hello pattern "Group * <VNET name>"</span></span> |
| <span data-ttu-id="0ae51-122">HostedService {hosted-service-name} 中的 VM {vm-name} 包含擴充 {extension-name}，在 Azure Resource Manager 中不支援。</span><span class="sxs-lookup"><span data-stu-id="0ae51-122">VM {vm-name} in HostedService {hosted-service-name} contains Extension {extension-name} which is not supported in Azure Resource Manager.</span></span> <span data-ttu-id="0ae51-123">建議 toouninstall 從 hello VM，再繼續進行移轉。</span><span class="sxs-lookup"><span data-stu-id="0ae51-123">It is recommended toouninstall it from hello VM before continuing with migration.</span></span> |<span data-ttu-id="0ae51-124">XML 擴充，例如 BGInfo 1.*，在 Azure Resource Manager 中不支援。</span><span class="sxs-lookup"><span data-stu-id="0ae51-124">XML extensions such as BGInfo 1.* are not supported in Azure Resource Manager.</span></span> <span data-ttu-id="0ae51-125">因此，這些擴充功能不能移轉。</span><span class="sxs-lookup"><span data-stu-id="0ae51-125">Therefore, these extensions cannot be migrated.</span></span> <span data-ttu-id="0ae51-126">如果這些擴充功能左邊的已安裝在 hello 虛擬機器，它們會自動解除安裝之前完成 hello 移轉。</span><span class="sxs-lookup"><span data-stu-id="0ae51-126">If these extensions are left installed on hello virtual machine, they are automatically uninstalled before completing hello migration.</span></span> |
| <span data-ttu-id="0ae51-127">HostedService {hosted-service-name} 中的 VM {vm-name} 包含擴充 VMSnapshot/VMSnapshotLinux，目前不支援移轉。</span><span class="sxs-lookup"><span data-stu-id="0ae51-127">VM {vm-name} in HostedService {hosted-service-name} contains Extension VMSnapshot/VMSnapshotLinux, which is currently not supported for Migration.</span></span> <span data-ttu-id="0ae51-128">從 hello VM 解除安裝，並將它傳回 hello 移轉已完成之後，使用 Azure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="0ae51-128">Uninstall it from hello VM and add it back using Azure Resource Manager after hello Migration is Complete</span></span> |<span data-ttu-id="0ae51-129">這是 hello 案例 hello 虛擬機器設定 Azure 備份的位置。</span><span class="sxs-lookup"><span data-stu-id="0ae51-129">This is hello scenario where hello virtual machine is configured for Azure Backup.</span></span> <span data-ttu-id="0ae51-130">由於這是目前不支援的案例，請遵循在 https://aka.ms/vmbackupmigration hello 因應措施</span><span class="sxs-lookup"><span data-stu-id="0ae51-130">Since this is currently an unsupported scenario, please follow hello workaround at https://aka.ms/vmbackupmigration</span></span> |
| <span data-ttu-id="0ae51-131">VM {vm-名稱} {裝載-服務-名稱} 託管服務中的包含其狀態不從 hello VM 所報告的副檔名 {擴充功能-名稱}。</span><span class="sxs-lookup"><span data-stu-id="0ae51-131">VM {vm-name} in HostedService {hosted-service-name} contains Extension {extension-name} whose Status is not being reported from hello VM.</span></span> <span data-ttu-id="0ae51-132">因此，無法移轉此 VM。</span><span class="sxs-lookup"><span data-stu-id="0ae51-132">Hence, this VM cannot be migrated.</span></span> <span data-ttu-id="0ae51-133">請確定該 hello 延伸模組狀態報告或從 hello VM 解除安裝 hello 延伸模組，然後重試移轉。</span><span class="sxs-lookup"><span data-stu-id="0ae51-133">Ensure that hello Extension status is being reported or uninstall hello extension from hello VM and retry migration.</span></span> <br><br> <span data-ttu-id="0ae51-134">HostedService {hosted-service-name} 中的 VM {vm-name} 包含擴充 {extension-name}，報告處理常式狀態：{handler-status}。</span><span class="sxs-lookup"><span data-stu-id="0ae51-134">VM {vm-name} in HostedService {hosted-service-name} contains Extension {extension-name} reporting Handler Status: {handler-status}.</span></span> <span data-ttu-id="0ae51-135">因此，無法移轉 hello VM。</span><span class="sxs-lookup"><span data-stu-id="0ae51-135">Hence, hello VM cannot be migrated.</span></span> <span data-ttu-id="0ae51-136">請確認 hello 延伸模組處理常式狀態報告 {處理常式 status} 或從 hello VM 解除安裝然後重試移轉。</span><span class="sxs-lookup"><span data-stu-id="0ae51-136">Ensure that hello Extension handler status being reported is {handler-status} or uninstall it from hello VM and retry migration.</span></span> <br><br> <span data-ttu-id="0ae51-137">VM {vm-名稱} {裝載-服務-名稱} 託管服務中的 VM 代理程式回報 hello 整體的代理程式狀態為未就緒。</span><span class="sxs-lookup"><span data-stu-id="0ae51-137">VM Agent for VM {vm-name} in HostedService {hosted-service-name} is reporting hello overall agent status as Not Ready.</span></span> <span data-ttu-id="0ae51-138">因此，hello VM 可能不會移轉，是否可移轉的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="0ae51-138">Hence, hello VM may not be migrated, if it has a migratable extension.</span></span> <span data-ttu-id="0ae51-139">請確定該 hello VM 代理程式報告為已備妥代理程式的整體狀態。</span><span class="sxs-lookup"><span data-stu-id="0ae51-139">Ensure that hello VM Agent is reporting overall agent status as Ready.</span></span> <span data-ttu-id="0ae51-140">請參閱 toohttps://aka.ms/classiciaasmigrationfaqs。</span><span class="sxs-lookup"><span data-stu-id="0ae51-140">Refer toohttps://aka.ms/classiciaasmigrationfaqs.</span></span> |<span data-ttu-id="0ae51-141">Azure 客體代理程式和 VM 延伸模組需要傳出網際網路存取 toohello VM 儲存體帳戶 toopopulate 及其狀態。</span><span class="sxs-lookup"><span data-stu-id="0ae51-141">Azure guest agent & VM Extensions need outbound internet access toohello VM storage account toopopulate their status.</span></span> <span data-ttu-id="0ae51-142">狀態失敗的常見原因包括</span><span class="sxs-lookup"><span data-stu-id="0ae51-142">Common causes of status failure include</span></span> <li> <span data-ttu-id="0ae51-143">網路安全性群組會封鎖 toohello 對外存取網際網路</span><span class="sxs-lookup"><span data-stu-id="0ae51-143">a Network Security Group that blocks outbound access toohello internet</span></span> <li> <span data-ttu-id="0ae51-144">如果 hello VNET 具有內部 DNS 伺服器及 DNS 連線已遺失</span><span class="sxs-lookup"><span data-stu-id="0ae51-144">If hello VNET has on-prem DNS servers and DNS connectivity is lost</span></span> <br><br> <span data-ttu-id="0ae51-145">如果您繼續 toosee 不支援的狀態，您可以解除安裝 hello 延伸 tooskip 這項檢查，然後繼續進行移轉。</span><span class="sxs-lookup"><span data-stu-id="0ae51-145">If you continue toosee an unsupported status, you can uninstall hello extensions tooskip this check and move forward with migration.</span></span> |
| <span data-ttu-id="0ae51-146">移轉不支援 HostedService {hosted-service-name} 中的部署 {deployment-name}，因為它有多個可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="0ae51-146">Migration is not supported for Deployment {deployment-name} in HostedService {hosted-service-name} because it has multiple Availability Sets.</span></span> |<span data-ttu-id="0ae51-147">目前，只能移轉具有 1 或更少可用性設定組的託管服務。</span><span class="sxs-lookup"><span data-stu-id="0ae51-147">Currently, only hosted services that have 1 or less Availability sets can be migrated.</span></span> <span data-ttu-id="0ae51-148">toowork 解決這個問題，請將移 hello 其他可用性設定組和虛擬機器在不同的可用性集 tooa 託管服務。</span><span class="sxs-lookup"><span data-stu-id="0ae51-148">toowork around this problem, please move hello additional Availability sets and Virtual machines in those Availability sets tooa different hosted service.</span></span> |
| <span data-ttu-id="0ae51-149">不支援移轉託管服務中的部署 {部署-名稱} {裝載的服務名稱因為它有不屬於可用性設定組的 hello，即使 hello 託管服務包含一個 Vm。</span><span class="sxs-lookup"><span data-stu-id="0ae51-149">Migration is not supported for Deployment {deployment-name} in HostedService {hosted-service-name because it has VMs that are not part of hello Availability Set even though hello HostedService contains one.</span></span> |<span data-ttu-id="0ae51-150">此案例中的 hello 因應措施是 tooeither 移動到單一可用性所有 hello 虛擬機器設定，或移除的 hello hello 託管服務中的可用性設定組中的所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0ae51-150">hello workaround for this scenario is tooeither move all hello virtual machines into a single Availability set or remove all Virtual machines from hello Availability set in hello hosted service.</span></span> |
| <span data-ttu-id="0ae51-151">儲存體帳戶/託管服務/虛擬網路 {虛擬-網路-名稱} 處於 hello 進行移轉，因此無法變更</span><span class="sxs-lookup"><span data-stu-id="0ae51-151">Storage account/HostedService/Virtual Network {virtual-network-name} is in hello process of being migrated and hence cannot be changed</span></span> |<span data-ttu-id="0ae51-152">Hello 資源 hello 「 準備 」 移轉作業已完成，而使得變更 toohello 資源的作業觸發時，會發生這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="0ae51-152">This error happens when hello "Prepare" migration operation has been completed on hello resource and an operation that would make a change toohello resource is triggered.</span></span> <span data-ttu-id="0ae51-153">「 準備 」 作業之後的 hello 管理平面 hello 鎖定，因為任何變更 toohello 資源會遭到封鎖。</span><span class="sxs-lookup"><span data-stu-id="0ae51-153">Because of hello lock on hello management plane after "Prepare" operation, any changes toohello resource are blocked.</span></span> <span data-ttu-id="0ae51-154">toounlock hello 管理平面，您可以執行 hello 「 認可 」 移轉作業 toocomplete 移轉或 hello 「 中止 」 移轉作業 tooroll 回 hello 「 準備 」 作業。</span><span class="sxs-lookup"><span data-stu-id="0ae51-154">toounlock hello management plane, you can run hello "Commit" migration operation toocomplete migration or hello "Abort" migration operation tooroll back hello "Prepare" operation.</span></span> |
| <span data-ttu-id="0ae51-155">HostedService {hosted-service-name} 不允許移轉，因為它有 VM {vm-name} 處於下列「狀態」：RoleStateUnknown。</span><span class="sxs-lookup"><span data-stu-id="0ae51-155">Migration is not allowed for HostedService {hosted-service-name} because it has VM {vm-name} in State: RoleStateUnknown.</span></span> <span data-ttu-id="0ae51-156">只有當 hello VM 處於 hello 下列其中一種狀態-執行、 已停止的停止取消配置允許移轉。</span><span class="sxs-lookup"><span data-stu-id="0ae51-156">Migration is allowed only when hello VM is in one of hello following states - Running, Stopped, Stopped Deallocated.</span></span> |<span data-ttu-id="0ae51-157">hello VM 可能會開始進行透過狀態轉換，這通常發生在 hello 託管服務，例如重新啟動電腦上的更新作業期間，擴充功能安裝等等。建議的 hello 更新作業 toocomplete hello 託管服務上才會嘗試移轉。</span><span class="sxs-lookup"><span data-stu-id="0ae51-157">hello VM might be undergoing through a state transition, which usually happens when during an update operation on hello HostedService such as a reboot, extension installation etc. It is recommended for hello update operation toocomplete on hello HostedService before trying migration.</span></span> |
| <span data-ttu-id="0ae51-158">部署託管服務 {裝載-服務-名稱} {部署-名稱} {vm-名稱} VM 包含了其實體 blob 的大小 {size-of-the-vhd-blob-backing-the-data-disk} 位元組與 hello VM 資料磁碟的邏輯大小 {不相符的資料磁碟 {資料-磁碟-名稱}size-of-the-data-disk-specified-in-the-vm-api} 個位元組。</span><span class="sxs-lookup"><span data-stu-id="0ae51-158">Deployment {deployment-name} in HostedService {hosted-service-name} contains a VM {vm-name} with Data Disk {data-disk-name} whose physical blob size {size-of-the-vhd-blob-backing-the-data-disk} bytes does not match hello VM Data Disk logical size {size-of-the-data-disk-specified-in-the-vm-api} bytes.</span></span> <span data-ttu-id="0ae51-159">移轉會繼續執行，而不指定 hello hello Azure 資源管理員 VM 的資料磁碟的大小。</span><span class="sxs-lookup"><span data-stu-id="0ae51-159">Migration will proceed without specifying a size for hello data disk for hello Azure Resource Manager VM.</span></span> | <span data-ttu-id="0ae51-160">如果您不更新 hello VM API 模型中的 hello 大小調整 hello VHD blob，則會發生這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="0ae51-160">This error happens if you've resized hello VHD blob without updating hello size in hello VM API model.</span></span> <span data-ttu-id="0ae51-161">詳細的緩和步驟說明[如下](#vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-the-vm-data-disk-logical-size-bytes)。</span><span class="sxs-lookup"><span data-stu-id="0ae51-161">Detailed mitigation steps are outlined [below](#vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-the-vm-data-disk-logical-size-bytes).</span></span>|
| <span data-ttu-id="0ae51-162">驗證具有雲端服務 {Cloud Service name} 中 VM {VM name} 之媒體連結 {data disk Uri} 的資料磁碟 {data disk name} 時發生儲存體例外狀況。</span><span class="sxs-lookup"><span data-stu-id="0ae51-162">A storage exception occurred while validating data disk {data disk name} with media link {data disk Uri} for VM {VM name} in Cloud Service {Cloud Service name}.</span></span> <span data-ttu-id="0ae51-163">請確定該 hello VHD 媒體連結可存取此虛擬機器</span><span class="sxs-lookup"><span data-stu-id="0ae51-163">Please ensure that hello VHD media link is accessible for this virtual machine</span></span> | <span data-ttu-id="0ae51-164">如果 hello hello 磁碟 VM 已被刪除或不再可存取，可能會發生這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="0ae51-164">This error can happen if hello disks of hello VM have been deleted or are not accessible anymore.</span></span> <span data-ttu-id="0ae51-165">請先確定 hello 磁碟 hello VM 存在。</span><span class="sxs-lookup"><span data-stu-id="0ae51-165">Please make sure hello disks for hello VM exist.</span></span>|
| <span data-ttu-id="0ae51-166">HostedService {cloud-service-name} 中的 VM {vm-name} 包含 Disk with MediaLink {vhd-uri}，其具有 Azure Resource Manager 不支援的 blob 名稱 {vhd-blob-name}。</span><span class="sxs-lookup"><span data-stu-id="0ae51-166">VM {vm-name} in HostedService {cloud-service-name} contains Disk with MediaLink {vhd-uri} which has blob name {vhd-blob-name}  that is not supported in Azure Resource Manager.</span></span> | <span data-ttu-id="0ae51-167">"/"中不支援的計算資源提供者目前 hello hello blob 名稱時，就會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="0ae51-167">This error occurs when hello name of hello blob has a "/" in it which is not supported in Compute Resource Provider currently.</span></span> |
| <span data-ttu-id="0ae51-168">移轉不會允許部署託管服務 {雲端-服務-名稱} {部署-名稱}，因為它不是處於 hello 區域範圍內。</span><span class="sxs-lookup"><span data-stu-id="0ae51-168">Migration is not allowed for Deployment {deployment-name} in HostedService {cloud-service-name} as it is not in hello regional scope.</span></span> <span data-ttu-id="0ae51-169">請參閱 toohttp://aka.ms/regionalscope 移動這個部署 tooregional 範圍。</span><span class="sxs-lookup"><span data-stu-id="0ae51-169">Please refer toohttp://aka.ms/regionalscope for moving this deployment tooregional scope.</span></span> | <span data-ttu-id="0ae51-170">在 2014 中，Azure 宣布的網路功能資源會從叢集層級範圍 tooregional 範圍移動。</span><span class="sxs-lookup"><span data-stu-id="0ae51-170">In 2014, Azure announced that networking resources will move from a cluster level scope tooregional scope.</span></span> <span data-ttu-id="0ae51-171">請參閱 [http://aka.ms/regionalscope] 以取得詳細資訊 (http://aka.ms/regionalscope)。</span><span class="sxs-lookup"><span data-stu-id="0ae51-171">See [http://aka.ms/regionalscope] for more details (http://aka.ms/regionalscope).</span></span> <span data-ttu-id="0ae51-172">Hello 部署移轉何時未於更新作業，會自動移 tooa 區域範圍內，就會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="0ae51-172">This error happens when hello deployment being migrated has not had an update operation, which automatically moves it tooa regional scope.</span></span> <span data-ttu-id="0ae51-173">最佳的解決方法是 tooeither 新增端點 tooa VM，或資料磁碟 toohello VM，然後重試移轉。</span><span class="sxs-lookup"><span data-stu-id="0ae51-173">Best workaround is tooeither add an endpoint tooa VM or a data disk toohello VM and then retry migration.</span></span> <br> <span data-ttu-id="0ae51-174">請參閱[如何 Azure 中的傳統 Windows 虛擬機器上的端點上 tooset](../articles/virtual-machines/windows/classic/setup-endpoints.md#create-an-endpoint)或[附加資料磁碟 tooa 建立 Windows 虛擬機器與 hello 傳統部署模型](../articles/virtual-machines/windows/classic/attach-disk.md)</span><span class="sxs-lookup"><span data-stu-id="0ae51-174">See [How tooset up endpoints on a classic Windows virtual machine in Azure](../articles/virtual-machines/windows/classic/setup-endpoints.md#create-an-endpoint) or [Attach a data disk tooa Windows virtual machine created with hello classic deployment model](../articles/virtual-machines/windows/classic/attach-disk.md)</span></span>|


## <a name="detailed-mitigations"></a><span data-ttu-id="0ae51-175">詳細的緩和措施</span><span class="sxs-lookup"><span data-stu-id="0ae51-175">Detailed mitigations</span></span>

### <a name="vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-hello-vm-data-disk-logical-size-bytes"></a><span data-ttu-id="0ae51-176">與資料磁碟之實體 blob 的大小位元組的 VM 不符合 hello VM 資料磁碟的邏輯大小位元組。</span><span class="sxs-lookup"><span data-stu-id="0ae51-176">VM with Data Disk whose physical blob size bytes does not match hello VM Data Disk logical size bytes.</span></span>

<span data-ttu-id="0ae51-177">這會 hello 資料磁碟的邏輯大小可以取得 hello 實際的 VHD blob 大小與同步處理。</span><span class="sxs-lookup"><span data-stu-id="0ae51-177">This happens when hello Data disk logical size can get out of sync with hello actual VHD blob size.</span></span> <span data-ttu-id="0ae51-178">可以輕鬆地驗證使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="0ae51-178">This can be easily verified using hello following commands:</span></span>

#### <a name="verifying-hello-issue"></a><span data-ttu-id="0ae51-179">正在驗證 hello 問題</span><span class="sxs-lookup"><span data-stu-id="0ae51-179">Verifying hello issue</span></span>

```PowerShell
# Store hello VM details in hello VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

# Display hello data disk properties
# NOTE hello data disk LogicalDiskSizeInGB below which is 11GB. Also note hello MediaLink Uri of hello VHD blob as we'll use this in hello next step
$vm.VM.DataVirtualHardDisks


HostCaching         : None
DiskLabel           : 
DiskName            : coreosvm-coreosvm-0-201611230636240687
Lun                 : 0
LogicalDiskSizeInGB : 11
MediaLink           : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
SourceMediaLink     : 
IOType              : Standard
ExtensionData       : 

# Now get hello properties of hello blob backing hello data disk above
# NOTE hello size of hello blob is about 15 GB which is different from LogicalDiskSizeInGB above
$blob = Get-AzureStorageblob -Blob "coreosvm-dd1.vhd" -Container vhds 

$blob

ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudPageBlob
BlobType          : PageBlob
Length            : 16106127872
ContentType       : application/octet-stream
LastModified      : 11/23/2016 7:16:22 AM +00:00
SnapshotTime      : 
ContinuationToken : 
Context           : Microsoft.WindowsAzure.Commands.Common.Storage.AzureStorageContext
Name              : coreosvm-dd1.vhd
```

#### <a name="mitigating-hello-issue"></a><span data-ttu-id="0ae51-180">緩和 hello 問題</span><span class="sxs-lookup"><span data-stu-id="0ae51-180">Mitigating hello issue</span></span>

```PowerShell
# Convert hello blob size in bytes tooGB into a variable which we'll use later
$newSize = [int]($blob.Length / 1GB)

# See hello calculated size in GB
$newSize

15

# Store hello disk name of hello data disk as we'll use this tooidentify hello disk toobe updated
$diskName = $vm.VM.DataVirtualHardDisks[0].DiskName

# Identify hello LUN of hello data disk tooremove
$lunToRemove = $vm.VM.DataVirtualHardDisks[0].Lun

# Now remove hello data disk from hello VM so that hello disk isn't leased by hello VM and it's size can be updated
Remove-AzureDataDisk -LUN $lunToRemove -VM $vm | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       213xx1-b44b-1v6n-23gg-591f2a13cd16   Succeeded  

# Verify we have hello right disk that's going toobe updated
Get-AzureDisk -DiskName $diskName

AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : 
Location             : East US
DiskSizeInGB         : 11
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 0c56a2b7-a325-123b-7043-74c27d5a61fd
OperationStatus      : Succeeded

# Now update hello disk toohello new size
Update-AzureDisk -DiskName $diskName -ResizedSizeInGB $newSize -Label $diskName

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureDisk     cv134b65-1b6n-8908-abuo-ce9e395ac3e7 Succeeded 

# Now verify that hello "DiskSizeInGB" property of hello disk matches hello size of hello blob 
Get-AzureDisk -DiskName $diskName


AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : coreosvm-coreosvm-0-201611230636240687
Location             : East US
DiskSizeInGB         : 15
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 1v53bde5-cv56-5621-9078-16b9c8a0bad2
OperationStatus      : Succeeded

# Now we'll add hello disk back toohello VM as a data disk. First we need tooget an updated VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

Add-AzureDataDisk -Import -DiskName $diskName -LUN 0 -VM $vm -HostCaching ReadWrite | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       b0ad3d4c-4v68-45vb-xxc1-134fd010d0f8 Succeeded      
```

### <a name="moving-a-vm-tooa-different-subscription-after-completing-migration"></a><span data-ttu-id="0ae51-181">移動 VM tooa 不同訂用帳戶完成移轉之後</span><span class="sxs-lookup"><span data-stu-id="0ae51-181">Moving a VM tooa different subscription after completing migration</span></span>

<span data-ttu-id="0ae51-182">Hello 移轉程序完成之後，您可能想 toomove hello VM tooanother 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0ae51-182">After you complete hello migration process, you may want toomove hello VM tooanother subscription.</span></span> <span data-ttu-id="0ae51-183">不過，如果您有密碼/憑證參考的金鑰保存庫資源，hello 的 VM 移的 hello 目前不支援。</span><span class="sxs-lookup"><span data-stu-id="0ae51-183">However, if you have a secret/certificate on hello VM that references a Key Vault resource, hello move is currently not supported.</span></span> <span data-ttu-id="0ae51-184">下面的指示 hello 可讓您 tooworkaround hello 問題。</span><span class="sxs-lookup"><span data-stu-id="0ae51-184">hello below instructions will allow you tooworkaround hello issue.</span></span> 

#### <a name="powershell"></a><span data-ttu-id="0ae51-185">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ae51-185">PowerShell</span></span>
```powershell
$vm = Get-AzureRmVM -ResourceGroupName "MyRG" -Name "MyVM"
Remove-AzureRmVMSecret -VM $vm
Update-AzureRmVM -ResourceGroupName "MyRG" -VM $vm
```
#### <a name="azure-cli-20"></a><span data-ttu-id="0ae51-186">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0ae51-186">Azure CLI 2.0</span></span>

```bash
az vm update -g "myrg" -n "myvm" --set osProfile.Secrets=[]
```
