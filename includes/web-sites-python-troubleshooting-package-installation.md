在 Azure 上執行時，有些封裝可能無法使用 PIP 安裝。  也可能只是 hello 套件並不適用於 hello Python 封裝索引。  它可能需要的編譯器 （編譯器並不適用於 hello 機器執行 hello web 應用程式在 Azure App Service 中）。

在本節中，我們將探討這個問題的方式 toodeal。

### <a name="request-wheels"></a>要求 Wheel
如果 hello 套件安裝需要編譯器，您應該嘗試連絡 hello 封裝擁有者 toorequest 滾輪供 hello 套件。

Hello 的最新的可用性與[Microsoft Visual c + + 編譯器的 Python 2.7][Microsoft Visual C++ Compiler for Python 2.7]，它現在是原生程式碼的 Python 2.7 toobuild 封裝更容易。

### <a name="build-wheels-requires-windows"></a>建置 Wheel (需要 Windows)
注意： 使用此選項時，請使用符合 hello 平台/結構/版本上 hello Azure App Service 中的 web 應用程式所使用的 Python 環境的確定 toocompile hello 封裝 （Windows/32-bit/2.7 或 3.4）。

如果 hello 封裝未安裝，因為它需要編譯器，您可以在本機電腦上安裝 hello 編譯器和建置 hello 封裝，您會在您的儲存機制中包含的是滾輪。

Mac/Linux 使用者： 如果您沒有存取 tooa Windows 電腦，請參閱[建立虛擬機器執行 Windows] [ Create a Virtual Machine Running Windows]如何 toocreate Azure 上的 VM。  您可以使用 toobuild hello 車輪、 將它們加入 toohello 儲存機制，而捨棄 hello VM，如果您想。 

您可以安裝 Python 2.7 [Microsoft Visual c + + 編譯器的 Python 2.7][Microsoft Visual C++ Compiler for Python 2.7]。

您可以安裝 Python 3.4 [Microsoft Visual c + + 2010 Express][Microsoft Visual C++ 2010 Express]。

toobuild 滾輪，您將需要 hello 滾輪封裝：

    env\scripts\pip install wheel

您將使用`pip wheel`toocompile 相依性：

    env\scripts\pip wheel azure==0.8.4

這會建立 hello \wheelhouse 資料夾.whl 檔案。  加入 hello \wheelhouse 資料夾和滾輪檔案 tooyour 儲存機制。

編輯您 requirements.txt tooadd hello `--find-links` hello 頂端的選項。 這會告訴 pip toolook hello 的本機資料夾，再進行 toohello python 封裝索引中完全相符。

    --find-links wheelhouse
    azure==0.8.4

如果您想的 tooinclude hello \wheelhouse 資料夾並不使用 hello python 封裝中的所有相依性的所有索引，您可以藉由新增強制 pip tooignore hello 封裝索引`--no-index`toohello 您 requirements.txt 頂端。

    --no-index

### <a name="customize-installation"></a>自訂安裝
您可以自訂 hello 部署指令碼 tooinstall hello 使用替代安裝程式，例如簡單的虛擬環境中的封裝\_安裝。  如需已標成註解的範例，請參閱 deploy.cmd。請確定這類封裝未列出的 requirements.txt，tooprevent pip 安裝它們。

加入這個 toohello 部署指令碼：

    env\scripts\easy_install somepackage

您也可以輕鬆無法 toouse\_exe 安裝程式的安裝 tooinstall (有些 zip 相容，因此容易\_安裝支援這些)。  加入 hello installer tooyour 儲存機制，並叫用簡單\_傳遞 hello 路徑 toohello 可執行檔來安裝。

加入這個 toohello 部署指令碼：

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-hello-virtual-environment-in-hello-repository-requires-windows"></a>包含 hello （需要 Windows） 的儲存機制中的 hello 虛擬環境
注意： 使用此選項時，請確定 toouse 符合 hello 平台/結構/版本上 hello Azure App Service 中的 web 應用程式所使用的虛擬環境 （Windows/32-bit/2.7 或 3.4）。

如果您包含虛擬環境的 hello hello 儲存機制中，您可以藉由建立空的檔案執行在 Azure 上的虛擬環境管理防止 hello 部署指令碼：

    .skipPythonDeployment

我們建議您刪除 hello 現有的虛擬環境的 hello 應用程式，從 tooprevent 剩餘檔案，自動管理虛擬環境的 hello 時。

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
