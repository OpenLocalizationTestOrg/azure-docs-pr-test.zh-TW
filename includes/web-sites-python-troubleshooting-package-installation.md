<span data-ttu-id="97e36-101">在 Azure 上執行時，有些封裝可能無法使用 PIP 安裝。</span><span class="sxs-lookup"><span data-stu-id="97e36-101">Some packages may not install using pip when run on Azure.</span></span>  <span data-ttu-id="97e36-102">這可能只是因為在 Python 封裝索引上無法使用該封裝。</span><span class="sxs-lookup"><span data-stu-id="97e36-102">It may simply be that the package is not available on the Python Package Index.</span></span>  <span data-ttu-id="97e36-103">這可能是需要有編譯器 (在 Azure App Service 中執行 Web 應用程式的電腦上無法使用編譯器)。</span><span class="sxs-lookup"><span data-stu-id="97e36-103">It could be that a compiler is required (a compiler is not available on the machine running the web app in Azure App Service).</span></span>

<span data-ttu-id="97e36-104">在本節中，我們將探討如何處理這個問題。</span><span class="sxs-lookup"><span data-stu-id="97e36-104">In this section, we'll look at ways to deal with this issue.</span></span>

### <a name="request-wheels"></a><span data-ttu-id="97e36-105">要求 Wheel</span><span class="sxs-lookup"><span data-stu-id="97e36-105">Request wheels</span></span>
<span data-ttu-id="97e36-106">如果封裝安裝需要編譯器，您應該嘗試連絡封裝擁有者，要求提供適用於封裝的 Wheel。</span><span class="sxs-lookup"><span data-stu-id="97e36-106">If the package installation requires a compiler, you should try contacting the package owner to request that wheels be made available for the package.</span></span>

<span data-ttu-id="97e36-107">新的可用性[Microsoft Visual c + + 編譯器的 Python 2.7][Microsoft Visual C++ Compiler for Python 2.7]，現在是您更輕鬆地建置具有原生程式碼的 Python 2.7 的封裝。</span><span class="sxs-lookup"><span data-stu-id="97e36-107">With the recent availability of [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], it is now easier to build packages that have native code for Python 2.7.</span></span>

### <a name="build-wheels-requires-windows"></a><span data-ttu-id="97e36-108">建置 Wheel (需要 Windows)</span><span class="sxs-lookup"><span data-stu-id="97e36-108">Build wheels (requires Windows)</span></span>
<span data-ttu-id="97e36-109">注意：使用此選項時，請務必使用符合 Azure App Service 中 Web 應用程式上使用之平台/架構/版本 (Windows/32 位元/2.7 或 3.4) 的 Python 環境編譯封裝。</span><span class="sxs-lookup"><span data-stu-id="97e36-109">Note: When using this option, make sure to compile the package using a Python environment that matches the platform/architecture/version that is used on the web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="97e36-110">如果封裝因為需要編譯器而無法安裝，您可以在本機電腦上安裝編譯器，並建置封裝的 Wheel，然後將其包含在您的儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="97e36-110">If the package doesn't install because it requires a compiler, you can install the compiler on your local machine and build a wheel for the package, which you will then include in your repository.</span></span>

<span data-ttu-id="97e36-111">Mac/Linux 使用者： 如果您沒有存取權的 Windows 電腦，請參閱[建立虛擬機器執行 Windows] [ Create a Virtual Machine Running Windows]如何在 Azure 上建立 VM。</span><span class="sxs-lookup"><span data-stu-id="97e36-111">Mac/Linux Users: If you don't have access to a Windows machine, see [Create a Virtual Machine Running Windows][Create a Virtual Machine Running Windows] for how to create a VM on Azure.</span></span>  <span data-ttu-id="97e36-112">您可以使用該虛擬機器建置 Wheel、將它們加入至儲存機制，以及在您想要捨棄虛擬機器時捨棄。</span><span class="sxs-lookup"><span data-stu-id="97e36-112">You can use it to build the wheels, add them to the repository, and discard the VM if you like.</span></span> 

<span data-ttu-id="97e36-113">您可以安裝 Python 2.7 [Microsoft Visual c + + 編譯器的 Python 2.7][Microsoft Visual C++ Compiler for Python 2.7]。</span><span class="sxs-lookup"><span data-stu-id="97e36-113">For Python 2.7, you can install [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span></span>

<span data-ttu-id="97e36-114">您可以安裝 Python 3.4 [Microsoft Visual c + + 2010 Express][Microsoft Visual C++ 2010 Express]。</span><span class="sxs-lookup"><span data-stu-id="97e36-114">For Python 3.4, you can install [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span></span>

<span data-ttu-id="97e36-115">若要建置 Wheel，您需要有 Wheel 封裝：</span><span class="sxs-lookup"><span data-stu-id="97e36-115">To build wheels, you'll need the wheel package:</span></span>

    env\scripts\pip install wheel

<span data-ttu-id="97e36-116">您將使用 `pip wheel` 編譯相依性：</span><span class="sxs-lookup"><span data-stu-id="97e36-116">You'll use `pip wheel` to compile a dependency:</span></span>

    env\scripts\pip wheel azure==0.8.4

<span data-ttu-id="97e36-117">這會在 \wheelhouse 資料夾中建立一個 .whl 檔。</span><span class="sxs-lookup"><span data-stu-id="97e36-117">This creates a .whl file in the \wheelhouse folder.</span></span>  <span data-ttu-id="97e36-118">將 \wheelhouse 資料夾與 Wheel 檔案加入至您的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="97e36-118">Add the \wheelhouse folder and wheel files to your repository.</span></span>

<span data-ttu-id="97e36-119">編輯 requirements.txt 以便在頂端加入 `--find-links` 選項。</span><span class="sxs-lookup"><span data-stu-id="97e36-119">Edit your requirements.txt to add the `--find-links` option at the top.</span></span> <span data-ttu-id="97e36-120">這會告訴 PIP 尋找本機資料夾中完全相符的項目，才能進入 Python 封裝索引。</span><span class="sxs-lookup"><span data-stu-id="97e36-120">This tells pip to look for an exact match in the local folder before going to the python package index.</span></span>

    --find-links wheelhouse
    azure==0.8.4

<span data-ttu-id="97e36-121">如果您想要在 \wheelhouse 資料夾中包含所有相依性，而且完全不使用 Python 封裝索引，您可以將 `--no-index` 加入至 requirements.txt 的頂端，以強制 PIP 忽略封裝索引。</span><span class="sxs-lookup"><span data-stu-id="97e36-121">If you want to include all your dependencies in the \wheelhouse folder and not use the python package index at all, you can force pip to ignore the package index by adding `--no-index` to the top of your requirements.txt.</span></span>

    --no-index

### <a name="customize-installation"></a><span data-ttu-id="97e36-122">自訂安裝</span><span class="sxs-lookup"><span data-stu-id="97e36-122">Customize installation</span></span>
<span data-ttu-id="97e36-123">您可以自訂部署指令碼，以使用替代的安裝程式 (例如 easy\_install) 在虛擬環境中安裝套件。</span><span class="sxs-lookup"><span data-stu-id="97e36-123">You can customize the deployment script to install a package in the virtual environment using an alternate installer, such as easy\_install.</span></span>  <span data-ttu-id="97e36-124">如需已標成註解的範例，請參閱 deploy.cmd。</span><span class="sxs-lookup"><span data-stu-id="97e36-124">See deploy.cmd for an example that is commented out.</span></span>  <span data-ttu-id="97e36-125">請確定這類封裝未列在 requirements.txt 中，以避免 PIP 安裝這類封裝。</span><span class="sxs-lookup"><span data-stu-id="97e36-125">Make sure that such packages aren't listed in requirements.txt, to prevent pip from installing them.</span></span>

<span data-ttu-id="97e36-126">將以下加入至部署指令碼：</span><span class="sxs-lookup"><span data-stu-id="97e36-126">Add this to the deployment script:</span></span>

    env\scripts\easy_install somepackage

<span data-ttu-id="97e36-127">您也可以使用 easy\_install，從 exe 安裝程式 (某些與 zip 相容，因此 easy\_install 支援它們) 安裝。</span><span class="sxs-lookup"><span data-stu-id="97e36-127">You may also be able to use easy\_install to install from an exe installer (some are zip compatible, so easy\_install supports them).</span></span>  <span data-ttu-id="97e36-128">將安裝程式新增至您的儲存機制，並傳遞可執行檔的路徑以叫用 easy\_install。</span><span class="sxs-lookup"><span data-stu-id="97e36-128">Add the installer to your repository, and invoke easy\_install by passing the path to the executable.</span></span>

<span data-ttu-id="97e36-129">將以下加入至部署指令碼：</span><span class="sxs-lookup"><span data-stu-id="97e36-129">Add this to the deployment script:</span></span>

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-the-virtual-environment-in-the-repository-requires-windows"></a><span data-ttu-id="97e36-130">在儲存機制中包含虛擬環境 (需要有 Windows)</span><span class="sxs-lookup"><span data-stu-id="97e36-130">Include the virtual environment in the repository (requires Windows)</span></span>
<span data-ttu-id="97e36-131">注意：使用此選項時，請務必使用符合 Azure App Service 中 Web 應用程式上使用之平台/架構/版本 (Windows/32 位元/2.7 或 3.4) 的虛擬環境。</span><span class="sxs-lookup"><span data-stu-id="97e36-131">Note: When using this option, make sure to use a virtual environment that matches the platform/architecture/version that is used on the web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="97e36-132">如果您在儲存機制中包含虛擬環境，可以防止部署指令碼透過建立空白檔案，在 Azure 上管理虛擬環境：</span><span class="sxs-lookup"><span data-stu-id="97e36-132">If you include the virtual environment in the repository, you can prevent the deployment script from doing virtual environment management on Azure by creating an empty file:</span></span>

    .skipPythonDeployment

<span data-ttu-id="97e36-133">建議您刪除應用程式上現有的虛擬環境，以防止在自動管理虛擬環境時遺留檔案。</span><span class="sxs-lookup"><span data-stu-id="97e36-133">We recommend that you delete the existing virtual environment on the app, to prevent leftover files from when the virtual environment was managed automatically.</span></span>

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
