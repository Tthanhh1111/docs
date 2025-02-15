---
title: プルリクエストのマージについて
intro: 'You can [merge pull requests](/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/merging-a-pull-request) by retaining all the commits in a feature branch, squashing all commits into a single commit, or by rebasing individual commits from the `head` branch onto the `base` branch.'
redirect_from:
  - /github/collaborating-with-issues-and-pull-requests/incorporating-changes-from-a-pull-request/about-pull-request-merges
  - /articles/about-pull-request-merge-squashing
  - /articles/about-pull-request-merges
  - /github/collaborating-with-issues-and-pull-requests/about-pull-request-merges
  - /github/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/about-pull-request-merges
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
topics:
  - Pull requests
---

## Merge your commits

{% data reusables.pull_requests.default_merge_option %}

## Squash and merge your commits

{% data reusables.pull_requests.squash_and_merge_summary %}

### squash マージのマージメッセージ

{% ifversion default-merge-squash-commit-message %}
When you squash and merge, {% data variables.product.prodname_dotcom %} generates a default commit message, which you can edit. Depending on how the repository is configured and the number of commits in the pull request, not including merge commits, this message may include the pull request title, pull request description, or information about the commits.
{% else %}
When you squash and merge, {% data variables.product.prodname_dotcom %} generates a default commit message, which you can edit. The default message depends on the number of commits in the pull request, not including merge commits.

| コミット数   | 概要                                      | 説明                                   |
| ------- | --------------------------------------- | ------------------------------------ |
| 単一のコミット | 単一のコミットのコミットメッセージのタイトルと、その後に続くプルリクエスト番号 | 単一のコミットのコミットメッセージの本文テキスト             |
| 複数のコミット | プルリクエストのタイトルと、その後に続くプルリクエスト番号           | squash されたすべてのコミットのコミットメッセージの日付順のリスト |
{% endif %}

| コミット数   | 概要                                      | 説明                                   |
| ------- | --------------------------------------- | ------------------------------------ |
| 単一のコミット | 単一のコミットのコミットメッセージのタイトルと、その後に続くプルリクエスト番号 | 単一のコミットのコミットメッセージの本文テキスト             |
| 複数のコミット | プルリクエストのタイトルと、その後に続くプルリクエスト番号           | squash されたすべてのコミットのコミットメッセージの日付順のリスト |

{% ifversion default-merge-squash-commit-message %}
People with maintainer or admin access to a repository can configure their repository's default merge message for all squashed commits to use the pull request title, the pull request title and commit details, or the pull request title and description. For more information, see "[Configure commit squashing](/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/configuring-commit-squashing-for-pull-requests)".{% endif %}

{% ifversion ghes = 3.6 %}
People with admin access to a repository can configure the repository to use the title of the pull request as the default merge message for all squashed commits. For more information, see "[Configure commit squashing](/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/configuring-commit-squashing-for-pull-requests)".
{% endif %}

### 長時間にわたるブランチを squash してマージする

プルリクエストがマージされた後、プルリクエストの [head ブランチ](/github/getting-started-with-github/github-glossary#head-branch)で作業を継続する場合は、プルリクエストを squash してマージしないことをお勧めします。

プルリクエストを作成すると、{% data variables.product.prodname_dotcom %} は、head ブランチと[ベースブランチ](/github/getting-started-with-github/github-glossary#base-branch)の両方にある最新のコミット、つまり共通の先祖のコミットを識別します。 プルリクエストを squash してマージすると、{% data variables.product.prodname_dotcom %} は、共通の先祖のコミット以降に head ブランチで行ったすべての変更を含むコミットをベースブランチに作成します。

このコミットはベースブランチのみで行われ、head ブランチでは行われないため、2 つのブランチの共通の先祖は変更されません。 head ブランチでの作業を続行し、2 つのブランチ間に新しいプルリクエストを作成すると、プルリクエストには、共通の先祖以降のすべてのコミットが含まれます。これには、前のプルリクエストで squash してマージしたコミットも含まれます。 コンフリクトがない場合は、これらのコミットを安全にマージできます。 ただし、このワークフローでは高確率でマージコンフリクトが発生します。 長時間にわたる head ブランチのプルリクエストを squash してマージし続ける場合は、同じコンフリクトを繰り返し解決する必要があります。

## Rebase and merge your commits

{% data reusables.pull_requests.rebase_and_merge_summary %}

以下の場合、{% data variables.product.product_location %}上で自動的にリベースおよびマージすることはできません:
- プルリクエストにマージコンフリクトがある。
- ベースブランチからヘッドブランチへのコミットのリベースでコンフリクトが生じる。
- たとえば、マージコンフリクトなしにリベースできるものの、マージとは異なる結果が生成されるような場合、コミットのリベースは「安全ではない」と考えられます。

それでもコミットをリベースしたいにもかかわらず、{% data variables.product.product_location %} 上で自動的にリベースとマージが行えない場合、以下のようにしなければなりません:
- トピックブランチ (あるいは head ブランチ) をベースブランチにローカルでコマンドラインからリベースする
- [コマンドライン上でマージコンフリクトを解決する](/articles/resolving-a-merge-conflict-using-the-command-line/)
- リベースされたコミットをプルリクエストのトピックブランチ (あるいはリモートの head ブランチ) にフォースプッシュする。

リポジトリに書き込み権限を持つ人は、続いて{% data variables.product.product_location %}上のリベース及びマージボタンを使って[変更をマージ](/articles/merging-a-pull-request/)できます。

## 参考リンク

- [プルリクエストについて](/articles/about-pull-requests/)
- [マージコンフリクトへの対処](/github/collaborating-with-pull-requests/addressing-merge-conflicts)
