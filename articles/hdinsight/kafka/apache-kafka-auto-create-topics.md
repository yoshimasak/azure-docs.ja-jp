---
title: Apache Kafka での自動トピック作成を有効にする - Azure HDInsight
description: トピックを自動的に作成するように HDInsight 上の Apache Kafka を構成する方法を説明します。 Ambari を使用して、あるいは PowerShell または Resource Manager テンプレートでクラスターを作成するときに、auto.create.topics.enable を true に設定することによって、Kafka を構成できます。
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 10/25/2019
ms.openlocfilehash: 7ec7d15806927306b12624962facbafddf2ce08b
ms.sourcegitcommit: 3486e2d4eb02d06475f26fbdc321e8f5090a7fac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2019
ms.locfileid: "73242361"
---
# <a name="how-to-configure-apache-kafka-on-hdinsight-to-automatically-create-topics"></a>トピックを自動的に作成するように HDInsight 上の Apache Kafka を構成する方法

既定では、HDInsight 上の [Apache Kafka](https://kafka.apache.org/) では、自動的にトピックは作成されません。 [Apache Ambari](https://ambari.apache.org/) を使って、既存のクラスターでの自動トピック作成を有効にすることができます。 Azure Resource Manager テンプレートを使って新しい Kafka クラスターを作成するときに、自動トピック作成を有効にすることもできます。

## <a name="apache-ambari-web-ui"></a>Apache Ambari Web UI

Ambari Web UI を使って既存のクラスターでトピックの自動作成を有効にするには、次の手順のようにします。

1. [Azure portal](https://portal.azure.com) 上で、ご自身の Kafka クラスターを選択します。

1. **クラスター ダッシュボード**上で **[Ambari ホーム]** を選択します。

    ![クラスター ダッシュボードが選ばれたポータルの画像](./media/apache-kafka-auto-create-topics/azure-portal-cluster-dashboard-ambari.png)

    認証を求められたら、クラスターのログイン (管理者) 資格情報を使用して認証を行います。 または、`https://CLUSTERNAME.azurehdinsight.net/` から直接 Amabri に接続することもできます。その際、`CLUSTERNAME` はご自身の Kafka クラスターの名前になります。

1. ページの左側にある一覧で Kafka サービスを選びます。

    ![Apache Ambari のサービス一覧タブ](./media/apache-kafka-auto-create-topics/hdinsight-service-list.png)

1. ページ中央の [Configs]\(構成\) を選択します。

    ![Apache Ambari のサービス構成タブ](./media/apache-kafka-auto-create-topics/hdinsight-service-config.png)

1. [フィルター] フィールドに値「`auto.create`」を入力します。

    ![Apache Ambari の検索フィルター フィールド](./media/apache-kafka-auto-create-topics/hdinsight-filter-field.png)

    プロパティの一覧にフィルターが適用されて `auto.create.topics.enable` 設定が表示されます。

1. `auto.create.topics.enable` の値を `true` に変更して、 **[保存]** を選択します。 ノートを追加して、もう一度 **[保存]** を選択します。

    ![auto.create.topics.enable エントリの画像](./media/apache-kafka-auto-create-topics/auto-create-topics-enable.png)

1. Kafka サービスを選び、 __[Restart]\(再起動\)__ を選んで、 __[Restart all affected]\(影響を受けるものをすべて再起動\)__ を選びます。 メッセージが表示されたら、 __[Confirm restart all]\(すべて再起動\)__ を選択します。

    ![Apache Ambari の影響を受けるものをすべて再起動](./media/apache-kafka-auto-create-topics/restart-all-affected.png)

> [!NOTE]  
> Ambari REST API を使って Ambari の値を設定することもできます。 現在の構成の取得やその変更のために複数の REST 呼び出しを行う必要があるため、通常はこの方法の方が困難です。詳細については、[Apache Ambari REST API を使用した HDInsight クラスターの管理](../hdinsight-hadoop-manage-ambari-rest-api.md)に関するページを参照してください。

## <a name="resource-manager-templates"></a>Resource Manager テンプレート

Azure Resource Manager テンプレートを使って Kafka クラスターを作成するときに、`kafka-broker` に追加することによって、`auto.create.topics.enable` を直接設定できます。 次の JSON スニペットでは、この値を `true` に設定する方法を示します。

```json
"clusterDefinition": {
    "kind": "kafka",
    "configurations": {
    "gateway": {
        "restAuthCredential.isEnabled": true,
        "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
        "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
    },
    "kafka-broker": {
        "auto.create.topics.enable": "true"
    }
}
```

## <a name="next-steps"></a>次の手順

このドキュメントでは、HDInsight 上の Apache Kafka でトピックの自動作成を有効にする方法を説明しました。 Kafka の使用について詳しくは、次のリンクをご覧ください。

* [Apache Kafka ログを分析する](apache-kafka-log-analytics-operations-management.md)
* [Apache Kafka クラスター間でデータをレプリケートする](apache-kafka-mirroring.md)
