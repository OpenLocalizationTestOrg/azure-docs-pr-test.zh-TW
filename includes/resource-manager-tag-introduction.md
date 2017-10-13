<span data-ttu-id="34700-101">將標籤套用 tooyour Azure 資源 toologically 組織這些類別。</span><span class="sxs-lookup"><span data-stu-id="34700-101">You apply tags tooyour Azure resources toologically organize them by categories.</span></span> <span data-ttu-id="34700-102">每個標記都是由一個名稱和一個值所組成。</span><span class="sxs-lookup"><span data-stu-id="34700-102">Each tag consists of a name and a value.</span></span> <span data-ttu-id="34700-103">例如，您可以套用 hello 名稱 「 環境 」 和 hello 值 「 生產 」 tooall hello 資源在生產環境中。</span><span class="sxs-lookup"><span data-stu-id="34700-103">For example, you can apply hello name "Environment" and hello value "Production" tooall hello resources in production.</span></span> <span data-ttu-id="34700-104">若沒有此標記，您可能難以識別資源主要是用於開發、測試或生產環境。</span><span class="sxs-lookup"><span data-stu-id="34700-104">Without this tag, you might have difficulty identifying whether a resource is intended for development, test, or production.</span></span> <span data-ttu-id="34700-105">不過，「環境」和「生產」只是範例。</span><span class="sxs-lookup"><span data-stu-id="34700-105">However, "Environment" and "Production" are just examples.</span></span> <span data-ttu-id="34700-106">您定義 hello 名稱和值，讓 hello 最適合組織您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="34700-106">You define hello names and values that make hello most sense for organizing your subscription.</span></span>

<span data-ttu-id="34700-107">套用標籤之後，您可以在您的訂用帳戶具有該標記名稱和值中擷取 hello 的所有資源。</span><span class="sxs-lookup"><span data-stu-id="34700-107">After you apply tags, you can retrieve all hello resources in your subscription with that tag name and value.</span></span> <span data-ttu-id="34700-108">您 tooretrieve 相關聯的資源位於不同的資源群組中的標記啟用。</span><span class="sxs-lookup"><span data-stu-id="34700-108">Tags enable you tooretrieve related resources that reside in different resource groups.</span></span> <span data-ttu-id="34700-109">當您的計費或管理需要 tooorganize 資源時，這個方法是很有幫助。</span><span class="sxs-lookup"><span data-stu-id="34700-109">This approach is helpful when you need tooorganize resources for billing or management.</span></span>

<span data-ttu-id="34700-110">hello 下列限制適用於 tootags:</span><span class="sxs-lookup"><span data-stu-id="34700-110">hello following limitations apply tootags:</span></span>

* <span data-ttu-id="34700-111">每個資源或資源群組最多都可以有 15 個標記名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="34700-111">Each resource or resource group can have a maximum of 15 tag name/value pairs.</span></span> <span data-ttu-id="34700-112">這項限制適用於只有直接套用 tootags toohello 資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="34700-112">This limitation applies only tootags directly applied toohello resource group or resource.</span></span> <span data-ttu-id="34700-113">資源群組可以包含許多資源，其各自有 15 個標記名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="34700-113">A resource group can contain many resources that each have 15 tag name/value pairs.</span></span> 
* <span data-ttu-id="34700-114">hello 標記名稱為有限的 too512 個字元，而且 hello 標記值為有限的 too256 個字元。</span><span class="sxs-lookup"><span data-stu-id="34700-114">hello tag name is limited too512 characters, and hello tag value is limited too256 characters.</span></span> <span data-ttu-id="34700-115">儲存體帳戶的 hello 標記名稱為有限的 too128 個字元，而且 hello 標記值為有限的 too256 個字元。</span><span class="sxs-lookup"><span data-stu-id="34700-115">For storage accounts, hello tag name is limited too128 characters, and hello tag value is limited too256 characters.</span></span>
* <span data-ttu-id="34700-116">套用標籤 toohello 資源群組不會繼承該資源群組中的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="34700-116">Tags applied toohello resource group are not inherited by hello resources in that resource group.</span></span> 

<span data-ttu-id="34700-117">如果您有超過 15 的值，您需要 tooassociate 與資源，請使用 JSON 字串 hello 標記值。</span><span class="sxs-lookup"><span data-stu-id="34700-117">If you have more than 15 values that you need tooassociate with a resource, use a JSON string for hello tag value.</span></span> <span data-ttu-id="34700-118">hello JSON 字串可以包含許多值所套用的 tooa 單一標籤名稱。</span><span class="sxs-lookup"><span data-stu-id="34700-118">hello JSON string can contain many values that are applied tooa single tag name.</span></span> <span data-ttu-id="34700-119">這篇文章會顯示指派的 JSON 字串 toohello 標記範例。</span><span class="sxs-lookup"><span data-stu-id="34700-119">This article shows an example of assigning a JSON string toohello tag.</span></span>