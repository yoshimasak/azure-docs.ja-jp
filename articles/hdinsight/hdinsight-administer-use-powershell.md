---
title: PowerShell を使用して Apache Hadoop クラスターを管理する - Azure HDInsight
description: Azure PowerShell を使用して HDInsight の Apache Hadoop クラスターに対する管理タスクを実行する方法について説明します。
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: conceptual
ms.custom: hdinsightactive
ms.date: 12/09/2019
ms.openlocfilehash: e37571b0078b4966aab9f505ddf88c2edb353197
ms.sourcegitcommit: f4f626d6e92174086c530ed9bf3ccbe058639081
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75435624"
---
# <a name="manage-apache-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a>Azure PowerShell を使用して HDInsight の Apache Hadoop クラスターを管理する

[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Azure PowerShell を使用して、Azure のワークロードのデプロイと管理を制御し自動化することができます。 この記事では、Azure PowerShell Az モジュールを使用して Azure HDInsight の [Apache Hadoop](https://hadoop.apache.org/) クラスターを管理する方法について説明します。 HDInsight PowerShell コマンドレットの一覧については、[Az.HDInsight リファレンス](https://docs.microsoft.com/powershell/module/az.hdinsight)を参照してください。

Azure サブスクリプションがない場合は、開始する前に[無料アカウント](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)を作成してください。

## <a name="prerequisites"></a>前提条件

[!INCLUDE [updated-for-az](../../includes/updated-for-az.md)]

インストール済みの PowerShell [Az モジュール](https://docs.microsoft.com/powershell/azure/overview)。

## <a name="create-clusters"></a>クラスターの作成

[Azure PowerShell を使用した HDInsight の Linux ベースのクラスターの作成](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)

## <a name="list-clusters"></a>クラスターを一覧表示する

現在のサブスクリプションにあるクラスターすべてを一覧表示するには次のコマンドを使用します。

```powershell
Get-AzHDInsightCluster
```

## <a name="show-cluster"></a>クラスターの表示

現在のサブスクリプションにある特定のクラスターの詳細を表示するには次のコマンドを使用します。

```powershell
Get-AzHDInsightCluster -ClusterName <Cluster Name>
```

## <a name="delete-clusters"></a>クラスターの削除

クラスターを削除するには、次のコマンドを使用します。

```powershell
Remove-AzHDInsightCluster -ClusterName <Cluster Name>
```

クラスターが含まれるリソース グループを削除して、クラスターを削除することもできます。 リソース グループを削除すると、既定のストレージ アカウントを含め、グループ内のすべてのリソースが削除されます。

```powershell
Remove-AzResourceGroup -Name <Resource Group Name>
```

## <a name="scale-clusters"></a>クラスターのスケール

クラスターのスケール設定機能を使用すると、Azure HDInsight で実行しているクラスターによって使用される worker ノードの数を、クラスターを再作成することなく、変更できます。 Azure PowerShell を使用して Hadoop クラスターのサイズを変更するには、クライアント コンピューターから次のコマンドを実行します。

```powershell
Set-AzHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>
```

 クラスターのスケーリングの詳細については、[HDInsight クラスターのスケーリング](./hdinsight-scaling-best-practices.md)に関するページを参照してください。

## <a name="grantrevoke-access"></a>アクセス権の付与/取り消し

HDInsight クラスターには、以下の HTTP Web サービスがあります (これらすべてのサービスには、REST ベースのエンドポイントがあります)。

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

既定では、これらのサービスへのアクセス許可が付与されます。 アクセス許可を取り消す/付与することができます。 取り消するには、次を実行します。

```powershell
Revoke-AzHDInsightHttpServicesAccess -ClusterName <Cluster Name>
```

許可するには、次を実行します。

```powershell
$clusterName = "<HDInsight Cluster Name>"

# Credential option 1
$hadoopUserName = "admin"
$hadoopUserPassword = '<Enter the Password>'
$hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
$credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

# Credential option 2
#$credential = Get-Credential -Message "Enter the HTTP username and password:" -UserName "admin"

Grant-AzHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential
```

> [!NOTE]  
> アクセス許可を付与するか、取り消すことで、クラスターのユーザー名とパスワードがリセットされます。

アクセス許可の付与および取り消しは、ポータルを使用して行うこともできます。 「[Azure portal を使用して HDInsight の Apache Hadoop クラスターを管理する](hdinsight-administer-use-portal-linux.md)」を参照してください。

## <a name="update-http-user-credentials"></a>HTTP ユーザーの資格情報の更新

HTTP アクセスの付与/取り消しと同じ手順です。 クラスターに HTTP アクセスが許可されている場合は、まずそれを取り消す必要があります。  次に、新しい HTTP ユーザーの資格情報を使用してアクセス許可を付与してください。

## <a name="find-the-default-storage-account"></a>既定のストレージ アカウントの検索

次の PowerShell スクリプトでは、既定のストレージ アカウント名と関連情報を取得する方法を示します。

```powershell
#Connect-AzAccount
$clusterName = "<HDInsight Cluster Name>"

$clusterInfo = Get-AzHDInsightCluster -ClusterName $clusterName
$storageInfo = $clusterInfo.DefaultStorageAccount.split('.')
$defaultStoreageType = $storageInfo[1]
$defaultStorageName = $storageInfo[0]

echo "Default Storage account name: $defaultStorageName"
echo "Default Storage account type: $defaultStoreageType"

if ($defaultStoreageType -eq "blob")
{
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

    echo "Default Blob container name: $defaultBlobContainerName"
    echo "Default Storage account key: $defaultStorageAccountKey"
}
```

## <a name="find-the-resource-group"></a>リソース グループの検索

Resource Manager モードでは、各 HDInsight クラスターは Azure リソース グループに属しています。  リソース グループを検索するには:

```powershell
$clusterName = "<HDInsight Cluster Name>"

$cluster = Get-AzHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $cluster.ResourceGroup
```

## <a name="submit-jobs"></a>ジョブの送信

**MapReduce ジョブを送信するには**

「[HDInsight に含まれる MapReduce サンプルを実行する](hadoop/apache-hadoop-run-samples-linux.md)」を参照してください。

**Apache Hive ジョブを送信するには**

「[PowerShell を使用して Apache Hive クエリを実行する](hadoop/apache-hadoop-use-hive-powershell.md)」を参照してください。

**Apache Sqoop ジョブを送信するには**

[HDInsight での Apache Sqoop の使用](hadoop/hdinsight-use-sqoop.md)に関するページを参照してください。

**Apache Oozie ジョブを送信するには**

「[HDInsight での Oozie と Hadoop を使用したワークフローの定義と実行](hdinsight-use-oozie-linux-mac.md)」を参照してください。

## <a name="upload-data-to-azure-blob-storage"></a>Azure BLOB ストレージにデータをアップロードする

[HDInsight へのデータのアップロード](hdinsight-upload-data.md)に関するページを参照してください。

## <a name="see-also"></a>参照

* [Az.HDInsight コマンドレット](https://docs.microsoft.com/powershell/module/az.hdinsight/?view=azps-3.1.0#hdinsight)
* [Azure portal を使用して HDInsight の Apache Hadoop クラスターを管理する](hdinsight-administer-use-portal-linux.md)
* [コマンド ライン インターフェイスを使用した HDInsight の管理](hdinsight-administer-use-command-line.md)
* [HDInsight クラスターの作成](hdinsight-hadoop-provision-linux-clusters.md)
* [プログラムによる Apache Hadoop ジョブの送信](hadoop/submit-apache-hadoop-jobs-programmatically.md)
* [Azure HDInsight の概要](hadoop/apache-hadoop-linux-tutorial-get-started.md)
