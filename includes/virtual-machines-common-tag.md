


## <a name="tagging-a-virtual-machine-through-templates"></a>透過範本標記虛擬機器
首先，我們來看一下透過範本進行標記。 [此範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags)標記置於 hello 下列資源： 運算 （虛擬機器）、 儲存體 （儲存體帳戶） 和網路 （公用 IP 位址、 虛擬網路，以及網路介面）。 這個範本適用於 Windows VM，但也可改寫成適用於 Linux VM。

按一下 hello**部署 tooAzure**按鈕 hello[範本連結](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags)。 這會瀏覽 toohello [Azure 入口網站](https://portal.azure.com/)您可以在其中部署此範本。

![使用標記的簡單部署](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

此範本包含下列標記的 hello:*部門*，*應用程式*，和*建立者*。 您可以新增/編輯直接在 hello 範本中的這些標記如果您想要不同的標記名稱。

![範本中的 Azure 標記](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

如您所見，hello 標記會定義為索引鍵/值組，以冒號 （:） 分隔。 hello 標記必須先定義格式如下：

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

在您完成編輯您所選擇的 hello 標記後，請儲存 hello 範本檔案。

接下來，在 hello**編輯參數** 區段中，您可以填寫 hello 值的標籤。

![在 Azure 入口網站中編輯標記](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

按一下**建立**toodeploy 標記值與此範本。

## <a name="tagging-through-hello-portal"></a>標記透過 hello 入口網站
建立您的資源具有標記之後, 您可以檢視、 新增和刪除 hello 入口網站中的標記。

選取 hello 標記圖示 tooview 標記：

![Azure 入口網站中的標記圖示](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

透過 hello 入口網站的新標記新增定義您自己的索引鍵/值組，並將其儲存。

![在 Azure 入口網站中新增標記](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

您的新標籤現在應該會出現在 hello 清單中的資源標記。

![Azure 入口網站中儲存的新標記](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

