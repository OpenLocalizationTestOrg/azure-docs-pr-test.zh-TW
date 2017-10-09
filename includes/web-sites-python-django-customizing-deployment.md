如果以下條件成立 ，Azure 將會確定您的應用程式使用 Python：

* requirements.txt hello 根資料夾中的檔案
* hello 根資料夾中的任何.py 檔案或指定 python 的 runtime.txt

Hello 案例時，它會使用執行 hello 的檔案，以及其他的 Python 作業，例如標準同步處理的 Python 特定部署指令碼：

* 自動管理虛擬環境
* 使用 PIP 安裝列在 requirements.txt 中的封裝
* 建立根據 hello hello 適當 web.config 選取 Python 版本。
* 收集適用於 Django 應用程式的靜態檔案

您可以控制 hello 預設的部署步驟的某些層面，而不需要 toocustomize hello 指令碼。

如果您想 tooskip Python 特定部署的所有步驟，您可以建立此空白檔案：

    \.skipPythonDeployment

如果您想 tooskip 靜態檔案的集合，如 Django 應用程式：

    \.skipDjango 

如需更多控制部署的詳細資訊，您都可以建立下列檔案的 hello 來覆寫 hello 預設部署指令碼：

    \.deployment
    \deploy.cmd

您可以使用 hello [Azure 命令列介面][ Azure command-line interface] toocreate hello 檔案。  從您的專案資料夾中使用此命令：

    azure site deploymentscript --python

當這些檔案不存在時，Azure 會建立一個暫存的部署指令碼，並執行該指令碼。  您使用上述的 hello 命令建立的相同 toohello 它。

[Azure command-line interface]: http://azure.microsoft.com/downloads/
