<span data-ttu-id="441d5-101">在 Azure 上執行時，有些封裝可能無法使用 PIP 安裝。</span><span class="sxs-lookup"><span data-stu-id="441d5-101">Some packages may not install using pip when run on Azure.</span></span>  <span data-ttu-id="441d5-102">也可能只是 hello 套件並不適用於 hello Python 封裝索引。</span><span class="sxs-lookup"><span data-stu-id="441d5-102">It may simply be that hello package is not available on hello Python Package Index.</span></span>  <span data-ttu-id="441d5-103">它可能需要的編譯器 （編譯器並不適用於 hello 機器執行 hello web 應用程式在 Azure App Service 中）。</span><span class="sxs-lookup"><span data-stu-id="441d5-103">It could be that a compiler is required (a compiler is not available on hello machine running hello web app in Azure App Service).</span></span>

<span data-ttu-id="441d5-104">在本節中，我們將探討這個問題的方式 toodeal。</span><span class="sxs-lookup"><span data-stu-id="441d5-104">In this section, we'll look at ways toodeal with this issue.</span></span>

### <a name="request-wheels"></a><span data-ttu-id="441d5-105">要求 Wheel</span><span class="sxs-lookup"><span data-stu-id="441d5-105">Request wheels</span></span>
<span data-ttu-id="441d5-106">如果 hello 套件安裝需要編譯器，您應該嘗試連絡 hello 封裝擁有者 toorequest 滾輪供 hello 套件。</span><span class="sxs-lookup"><span data-stu-id="441d5-106">If hello package installation requires a compiler, you should try contacting hello package owner toorequest that wheels be made available for hello package.</span></span>

<span data-ttu-id="441d5-107">Hello 的最新的可用性與[Microsoft Visual c + + 編譯器的 Python 2.7][Microsoft Visual C++ Compiler for Python 2.7]，它現在是原生程式碼的 Python 2.7 toobuild 封裝更容易。</span><span class="sxs-lookup"><span data-stu-id="441d5-107">With hello recent availability of [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], it is now easier toobuild packages that have native code for Python 2.7.</span></span>

### <a name="build-wheels-requires-windows"></a><span data-ttu-id="441d5-108">建置 Wheel (需要 Windows)</span><span class="sxs-lookup"><span data-stu-id="441d5-108">Build wheels (requires Windows)</span></span>
<span data-ttu-id="441d5-109">注意： 使用此選項時，請使用符合 hello 平台/結構/版本上 hello Azure App Service 中的 web 應用程式所使用的 Python 環境的確定 toocompile hello 封裝 （Windows/32-bit/2.7 或 3.4）。</span><span class="sxs-lookup"><span data-stu-id="441d5-109">Note: When using this option, make sure toocompile hello package using a Python environment that matches hello platform/architecture/version that is used on hello web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="441d5-110">如果 hello 封裝未安裝，因為它需要編譯器，您可以在本機電腦上安裝 hello 編譯器和建置 hello 封裝，您會在您的儲存機制中包含的是滾輪。</span><span class="sxs-lookup"><span data-stu-id="441d5-110">If hello package doesn't install because it requires a compiler, you can install hello compiler on your local machine and build a wheel for hello package, which you will then include in your repository.</span></span>

<span data-ttu-id="441d5-111">Mac/Linux 使用者： 如果您沒有存取 tooa Windows 電腦，請參閱[建立虛擬機器執行 Windows] [ Create a Virtual Machine Running Windows]如何 toocreate Azure 上的 VM。</span><span class="sxs-lookup"><span data-stu-id="441d5-111">Mac/Linux Users: If you don't have access tooa Windows machine, see [Create a Virtual Machine Running Windows][Create a Virtual Machine Running Windows] for how toocreate a VM on Azure.</span></span>  <span data-ttu-id="441d5-112">您可以使用 toobuild hello 車輪、 將它們加入 toohello 儲存機制，而捨棄 hello VM，如果您想。</span><span class="sxs-lookup"><span data-stu-id="441d5-112">You can use it toobuild hello wheels, add them toohello repository, and discard hello VM if you like.</span></span> 

<span data-ttu-id="441d5-113">您可以安裝 Python 2.7 [Microsoft Visual c + + 編譯器的 Python 2.7][Microsoft Visual C++ Compiler for Python 2.7]。</span><span class="sxs-lookup"><span data-stu-id="441d5-113">For Python 2.7, you can install [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span></span>

<span data-ttu-id="441d5-114">您可以安裝 Python 3.4 [Microsoft Visual c + + 2010 Express][Microsoft Visual C++ 2010 Express]。</span><span class="sxs-lookup"><span data-stu-id="441d5-114">For Python 3.4, you can install [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span></span>

<span data-ttu-id="441d5-115">toobuild 滾輪，您將需要 hello 滾輪封裝：</span><span class="sxs-lookup"><span data-stu-id="441d5-115">toobuild wheels, you'll need hello wheel package:</span></span>

    env\scripts\pip install wheel

<span data-ttu-id="441d5-116">您將使用`pip wheel`toocompile 相依性：</span><span class="sxs-lookup"><span data-stu-id="441d5-116">You'll use `pip wheel` toocompile a dependency:</span></span>

    env\scripts\pip wheel azure==0.8.4

<span data-ttu-id="441d5-117">這會建立 hello \wheelhouse 資料夾.whl 檔案。</span><span class="sxs-lookup"><span data-stu-id="441d5-117">This creates a .whl file in hello \wheelhouse folder.</span></span>  <span data-ttu-id="441d5-118">加入 hello \wheelhouse 資料夾和滾輪檔案 tooyour 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="441d5-118">Add hello \wheelhouse folder and wheel files tooyour repository.</span></span>

<span data-ttu-id="441d5-119">編輯您 requirements.txt tooadd hello `--find-links` hello 頂端的選項。</span><span class="sxs-lookup"><span data-stu-id="441d5-119">Edit your requirements.txt tooadd hello `--find-links` option at hello top.</span></span> <span data-ttu-id="441d5-120">這會告訴 pip toolook hello 的本機資料夾，再進行 toohello python 封裝索引中完全相符。</span><span class="sxs-lookup"><span data-stu-id="441d5-120">This tells pip toolook for an exact match in hello local folder before going toohello python package index.</span></span>

    --find-links wheelhouse
    azure==0.8.4

<span data-ttu-id="441d5-121">如果您想的 tooinclude hello \wheelhouse 資料夾並不使用 hello python 封裝中的所有相依性的所有索引，您可以藉由新增強制 pip tooignore hello 封裝索引`--no-index`toohello 您 requirements.txt 頂端。</span><span class="sxs-lookup"><span data-stu-id="441d5-121">If you want tooinclude all your dependencies in hello \wheelhouse folder and not use hello python package index at all, you can force pip tooignore hello package index by adding `--no-index` toohello top of your requirements.txt.</span></span>

    --no-index

### <a name="customize-installation"></a><span data-ttu-id="441d5-122">自訂安裝</span><span class="sxs-lookup"><span data-stu-id="441d5-122">Customize installation</span></span>
<span data-ttu-id="441d5-123">您可以自訂 hello 部署指令碼 tooinstall hello 使用替代安裝程式，例如簡單的虛擬環境中的封裝\_安裝。</span><span class="sxs-lookup"><span data-stu-id="441d5-123">You can customize hello deployment script tooinstall a package in hello virtual environment using an alternate installer, such as easy\_install.</span></span>  <span data-ttu-id="441d5-124">如需已標成註解的範例，請參閱 deploy.cmd。請確定這類封裝未列出的 requirements.txt，tooprevent pip 安裝它們。</span><span class="sxs-lookup"><span data-stu-id="441d5-124">See deploy.cmd for an example that is commented out.  Make sure that such packages aren't listed in requirements.txt, tooprevent pip from installing them.</span></span>

<span data-ttu-id="441d5-125">加入這個 toohello 部署指令碼：</span><span class="sxs-lookup"><span data-stu-id="441d5-125">Add this toohello deployment script:</span></span>

    env\scripts\easy_install somepackage

<span data-ttu-id="441d5-126">您也可以輕鬆無法 toouse\_exe 安裝程式的安裝 tooinstall (有些 zip 相容，因此容易\_安裝支援這些)。</span><span class="sxs-lookup"><span data-stu-id="441d5-126">You may also be able toouse easy\_install tooinstall from an exe installer (some are zip compatible, so easy\_install supports them).</span></span>  <span data-ttu-id="441d5-127">加入 hello installer tooyour 儲存機制，並叫用簡單\_傳遞 hello 路徑 toohello 可執行檔來安裝。</span><span class="sxs-lookup"><span data-stu-id="441d5-127">Add hello installer tooyour repository, and invoke easy\_install by passing hello path toohello executable.</span></span>

<span data-ttu-id="441d5-128">加入這個 toohello 部署指令碼：</span><span class="sxs-lookup"><span data-stu-id="441d5-128">Add this toohello deployment script:</span></span>

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-hello-virtual-environment-in-hello-repository-requires-windows"></a><span data-ttu-id="441d5-129">包含 hello （需要 Windows） 的儲存機制中的 hello 虛擬環境</span><span class="sxs-lookup"><span data-stu-id="441d5-129">Include hello virtual environment in hello repository (requires Windows)</span></span>
<span data-ttu-id="441d5-130">注意： 使用此選項時，請確定 toouse 符合 hello 平台/結構/版本上 hello Azure App Service 中的 web 應用程式所使用的虛擬環境 （Windows/32-bit/2.7 或 3.4）。</span><span class="sxs-lookup"><span data-stu-id="441d5-130">Note: When using this option, make sure toouse a virtual environment that matches hello platform/architecture/version that is used on hello web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="441d5-131">如果您包含虛擬環境的 hello hello 儲存機制中，您可以藉由建立空的檔案執行在 Azure 上的虛擬環境管理防止 hello 部署指令碼：</span><span class="sxs-lookup"><span data-stu-id="441d5-131">If you include hello virtual environment in hello repository, you can prevent hello deployment script from doing virtual environment management on Azure by creating an empty file:</span></span>

    .skipPythonDeployment

<span data-ttu-id="441d5-132">我們建議您刪除 hello 現有的虛擬環境的 hello 應用程式，從 tooprevent 剩餘檔案，自動管理虛擬環境的 hello 時。</span><span class="sxs-lookup"><span data-stu-id="441d5-132">We recommend that you delete hello existing virtual environment on hello app, tooprevent leftover files from when hello virtual environment was managed automatically.</span></span>

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
