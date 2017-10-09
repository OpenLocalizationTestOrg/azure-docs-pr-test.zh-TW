<span data-ttu-id="f377a-101">儲存體 Blob 中的每個 Blob 必須位於一個容器中。</span><span class="sxs-lookup"><span data-stu-id="f377a-101">Every blob in Azure storage must reside in a container.</span></span> <span data-ttu-id="f377a-102">hello 的 hello blob 名稱的容器表單組件。</span><span class="sxs-lookup"><span data-stu-id="f377a-102">hello container forms part of hello blob name.</span></span> <span data-ttu-id="f377a-103">例如， `mycontainer` hello 容器，這些範例 blob Uri 中的 hello 名稱：</span><span class="sxs-lookup"><span data-stu-id="f377a-103">For example, `mycontainer` is hello name of hello container in these sample blob URIs:</span></span>

    https://storagesample.blob.core.windows.net/mycontainer/blob1.txt
    https://storagesample.blob.core.windows.net/mycontainer/photos/myphoto.jpg

<span data-ttu-id="f377a-104">容器名稱必須是有效的 DNS 名稱，符合 toohello 下列命名規則：</span><span class="sxs-lookup"><span data-stu-id="f377a-104">A container name must be a valid DNS name, conforming toohello following naming rules:</span></span>

1. <span data-ttu-id="f377a-105">容器名稱必須以字母或數字開頭，而且只能包含字母、 數字和 hello 虛線 （-） 字元。</span><span class="sxs-lookup"><span data-stu-id="f377a-105">Container names must start with a letter or number, and can contain only letters, numbers, and hello dash (-) character.</span></span>
2. <span data-ttu-id="f377a-106">每個虛線 (-) 字元前後必須立即接著字母或數字；容器名稱中不允許連續虛線。</span><span class="sxs-lookup"><span data-stu-id="f377a-106">Every dash (-) character must be immediately preceded and followed by a letter or number; consecutive dashes are not permitted in container names.</span></span>
3. <span data-ttu-id="f377a-107">容器名稱的所有字母必須都是小寫。</span><span class="sxs-lookup"><span data-stu-id="f377a-107">All letters in a container name must be lowercase.</span></span>
4. <span data-ttu-id="f377a-108">容器名稱必須介於 3 至 63 個字元長。</span><span class="sxs-lookup"><span data-stu-id="f377a-108">Container names must be from 3 through 63 characters long.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f377a-109">請注意該 hello 的容器名稱必須一律是小寫。</span><span class="sxs-lookup"><span data-stu-id="f377a-109">Note that hello name of a container must always be lowercase.</span></span> <span data-ttu-id="f377a-110">如果您在輸入容器名稱中包含一個大寫字母或違反 hello 容器命名規則，您可能會收到 400 的錯誤 （不正確的要求）。</span><span class="sxs-lookup"><span data-stu-id="f377a-110">If you include an upper-case letter in a container name, or otherwise violate hello container naming rules, you may receive a 400 error (Bad Request).</span></span> 
> 
> 

