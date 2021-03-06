---
title: Azure Notebooks プレビューで Azure Machine Learning を使用する
description: Azure Notebooks プレビューで使用できる Azure Machine Learning 用のサンプル ノートブックの概要。
ms.topic: how-to
ms.date: 12/04/2018
ms.openlocfilehash: 435abca83255221d438d530b63c237c08bb0b672
ms.sourcegitcommit: 12a26f6682bfd1e264268b5d866547358728cd9a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75860573"
---
# <a name="use-azure-machine-learning-in-azure-notebooks-preview"></a>Azure Notebooks プレビューで Azure Machine Learning を使用する

Azure Notebooks は、[Azure Machine Learning](/azure/machine-learning/) と連動するために必要な環境で事前構築されています。 サンプル プロジェクトを自分の Notebooks アカウントに複製し、さまざまな機械学習シナリオを試すことが簡単にできます。

[!INCLUDE [notebooks-status](../../includes/notebooks-status.md)]

## <a name="clone-the-sample-into-your-account"></a>サンプルを自分のアカウントに複製する

1. [Azure Notebooks](https://notebooks.azure.com/) にサインインします。
1. **[マイ プロジェクト]** を選択し、プロジェクト ダッシュボードに移動します。
1. **[Upload GitHub Repo]\(GitHub リポジトリのアップロード\)** (上向き矢印) ボタンを選択し、 **[Upload GitHub Repository]\(GitHub リポジトリのアップロード\)** ポップアップを開きます。
1. このポップアップで、 **[GitHub リポジトリ]** に「`Azure/MachineLearningNotebooks`」と入力し、 **[プロジェクト名]** でプロジェクトの名前を指定し ("Azure Machine Learning" など)、 **[プロジェクト ID]** で識別子を指定し、必要であれば **[公開]** を選択解除して、 **[インポート]** を選択します。

    ![Azure Machine Learning Notebook サンプルを自分の Notebooks アカウントにインポートする](media/azureml-import-project.png)

1. 数分後、Azure Notebooks から新しいプロジェクトのダッシュボードに自動的に移動します。

## <a name="run-a-sample-notebook"></a>サンプル ノートブックを実行する

1. **[00 - configuration.ipynb]** を選択し、ノートブックの構成セクションを開始し、ノートブックの構成セクションを開始し、その指示に従って Azure Machine Learning ワークスペースを作成します。

    - Azure Notebooks には必要な Python パッケージが既に含まれているため、前提条件の手順 2 でコード スニペットを実行するだけで Azure ML SDK のバージョンを確認できます。

1. 構成の完了後、 **[01.getting-started]** を選択し、13 個の異なるサンプル ノートブックが含まれるフォルダーを開きます。このサンプル ノートブックはいずれも、見れば内容がわかるようになっています。

## <a name="next-steps"></a>次のステップ

Azure Machine Learning ドキュメントにはその他の各種リソースが含まれています。このリソースによって、ノートブック内で Machine Learning を段階的に進めることができます。

- [クイック スタート:Python を使用して Azure Machine Learning の利用を開始する](https://docs.microsoft.com/azure/machine-learning/how-to-configure-environment#local)
- [チュートリアル 1: Azure Machine Learning でイメージ分類モデルをトレーニングする](https://docs.microsoft.com/azure/machine-learning/tutorial-train-models-with-aml)」を参照してください
- [チュートリアル #2: Azure Container Instances (ACI) に画像分類モデルをデプロイする](https://docs.microsoft.com/azure/machine-learning/tutorial-deploy-models-with-aml)
- [チュートリアル:Azure Machine Learning において、自動機械学習で分類モデルをトレーニングする](https://docs.microsoft.com/azure/machine-learning/tutorial-auto-train-models)

[Azure Machine Learning SDK for Python](https://docs.microsoft.com/python/api/overview/azure/ml/intro?view=azure-ml-py) 用のドキュメントも参照してください。
