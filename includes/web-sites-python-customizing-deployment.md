<span data-ttu-id="60608-101">如果以下條件成立 ，Azure 將會確定您的應用程式使用 Python：</span><span class="sxs-lookup"><span data-stu-id="60608-101">Azure will determine that your application uses Python **if both of these conditions are true**:</span></span>

* <span data-ttu-id="60608-102">根資料夾中有 requirements.txt 檔案</span><span class="sxs-lookup"><span data-stu-id="60608-102">requirements.txt file in the root folder</span></span>
* <span data-ttu-id="60608-103">根資料夾中有任何 .py 檔案，或擁有指定 Python 的 runtime.txt</span><span class="sxs-lookup"><span data-stu-id="60608-103">any .py file in the root folder OR a runtime.txt that specifies python</span></span>

<span data-ttu-id="60608-104">若是如此，它將使用 Python 專屬的部署指令碼，此指令碼可執行檔案的標準同步處理，以及其他 Python 作業，例如：</span><span class="sxs-lookup"><span data-stu-id="60608-104">When that's the case, it will use a Python specific deployment script, which performs the standard synchronization of files, as well as additional Python operations such as:</span></span>

* <span data-ttu-id="60608-105">自動管理虛擬環境</span><span class="sxs-lookup"><span data-stu-id="60608-105">Automatic management of virtual environment</span></span>
* <span data-ttu-id="60608-106">使用 PIP 安裝列在 requirements.txt 中的封裝</span><span class="sxs-lookup"><span data-stu-id="60608-106">Installation of packages listed in requirements.txt using pip</span></span>
* <span data-ttu-id="60608-107">根據選取的 Python 版本建立適當的 web.config。</span><span class="sxs-lookup"><span data-stu-id="60608-107">Creation of the appropriate web.config based on the selected Python version.</span></span>
* <span data-ttu-id="60608-108">收集適用於 Django 應用程式的靜態檔案</span><span class="sxs-lookup"><span data-stu-id="60608-108">Collect static files for Django applications</span></span>

<span data-ttu-id="60608-109">您可以控制某些方面的預設部署步驟，而不需要自訂指令碼。</span><span class="sxs-lookup"><span data-stu-id="60608-109">You can control certain aspects of the default deployment steps without having to customize the script.</span></span>

<span data-ttu-id="60608-110">如果您想要略過所有 Python 專屬的部署步驟，可以建立此空白檔案：</span><span class="sxs-lookup"><span data-stu-id="60608-110">If you want to skip all Python specific deployment steps, you can create this empty file:</span></span>

    \.skipPythonDeployment

<span data-ttu-id="60608-111">若要更能掌控部署，您可以建立以下檔案來覆寫預設的部署指令碼：</span><span class="sxs-lookup"><span data-stu-id="60608-111">For more control over deployment, you can override the default deployment script by creating the following files:</span></span>

    \.deployment
    \deploy.cmd

<span data-ttu-id="60608-112">您可以使用[Azure 命令列介面][ Azure command-line interface] ，建立檔案。</span><span class="sxs-lookup"><span data-stu-id="60608-112">You can use the [Azure command-line interface][Azure command-line interface] to create the files.</span></span>  <span data-ttu-id="60608-113">從您的專案資料夾中使用此命令：</span><span class="sxs-lookup"><span data-stu-id="60608-113">Use this command from your project folder:</span></span>

    azure site deploymentscript --python

<span data-ttu-id="60608-114">當這些檔案不存在時，Azure 會建立一個暫存的部署指令碼，並執行該指令碼。</span><span class="sxs-lookup"><span data-stu-id="60608-114">When these files don't exist, Azure creates a temporary deployment script and runs it.</span></span>  <span data-ttu-id="60608-115">它與您使用上述命令建立的指令碼完全相同。</span><span class="sxs-lookup"><span data-stu-id="60608-115">It is identical to the one you create with the command above.</span></span>

[Azure command-line interface]: http://azure.microsoft.com/downloads/
