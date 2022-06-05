# pgm_map_data
自己位置推定やナビゲーションに使用するpgm形式のマップを集約するためのリポジトリ。

## ディレクトリ構成について

以下のようなディレクトリ構成で集約していきます。

追加する場合は参考にしてください。

```
 pgm_map_data
 ├── LICENSE
 ├── README.md
 └── ikebe  (アップロードする人の名前)
      ├── tsudanuma   (マッピングした場所)
      │   ├── localization　  (自己位置推定用)
      │   │   ├── map_tsudanuma.pgm
      │   │   └── map_tsudanuma.yaml
      │   └── navigation　　　(ナビゲーション用)　　
      │       ├── map_tsudanuma.pgm
      │       └── map_tsudanuma.yaml
      └── tsukuba
         ├── localization
         │   ├── map_tsukuba.pgm
         │   └── map_tsukuba.yaml
         └── navigation
             ├── map_tsukuba.pgm
             └── map_tsukuba.yaml
```

## 追加&修正の手順について
基本的に直接pushではなくて、ブランチを切ってPRでmergeするようにしてください。

またmergeについては、squash mergeでお願いします。

### 具体的な手順
実際に池邉が追加した時の例を交えて手順について説明します。

1. このリポジトリをクローン(sshでクローンするようにしましょう)

```
git clone git@github.com:CIT-Autonomous-Robot-Lab/pgm_map_data.git
```

2. 追加 & 修正をする

上記のディレクトリ構成のように追加を行いました。

3. `git checkout -b hoge/hoge`でブランチを切る
池邉は現在のブランチを表示できるようにしています。
cloneしたばかりだとmasterブランチ(あるいはmain)です。

```
ikebe@ikebe:~/pgm_map_data (master)$
```

ブランチを切ってみます

```
ikebe@ikebe:~/pgm_map_data (master)$ git checkout -b add/ikebe-pgm-map
ikebe@ikebe:~/pgm_map_data (add/ikebe-pgm-map)$
```

無事`master`ブランチから`add/ikebe-pgm-map`ブランチに切ることができました。
表示して無い場合はわからないと思います。その場合は`git branch`で見ることができます。

```
ikebe@ikebe:~/pgm_map_data (add/ikebe-pgm-map)$ git branch
* add/ikebe-pgm-map
  master
```

`git checkout -b`以降の`add/ikebe-pgm-map`ってなんだよって思った人がいると思います。
だいたい、`追加理由/追加内容`って感じです。
例えば、日本語を喋る機能を追加したのであれば`feature/speak-japanese`、修正したのであれば`fix/speak-japanese`、アップデートしたのであれば`update/speak-japanese`、削除したのであれば`delete/speak-japanese`です。

4. `git status`で変更内容を確認(とりあえず)
このコマンドは割と使います。
現在の修正内容やインデックスに上がってるファイルを知ることが出来ます。

とりあえず打ってみます。
```
ikebe@ikebe:~/pgm_map_data (add/ikebe-pgm-map)$ git status
ブランチ add/ikebe-pgm-map
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)

追跡されていないファイル:
  (use "git add <file>..." to include in what will be committed)
        ikebe/

no changes added to commit (use "git add" and/or "git commit -a")
```

新しく追加した`ikebe/`というディレクトリは、まだ`git`で追跡されていないようです。
これから追跡するようにやります。

5. `git add .`あるいは`git add hoge hogehoge hogegege`で変更内容をインデックスに追加

先ほど確認したディレクトリを追跡してくれるようにします。
まずはインデックスに追加します。

```
ikebe@ikebe:~/pgm_map_data (add/ikebe-pgm-map)$ git add ikebe
```

追加出来たのか`git status`で確認します。

```
ikebe@ikebe:~/pgm_map_data$ git status
ブランチ add/ikebe-pgm-map
コミット予定の変更点:
  (use "git restore --staged <file>..." to unstage)
        new file:   ikebe/tsudanuma/localization/map_tsudanuma.pgm
        new file:   ikebe/tsudanuma/localization/map_tsudanuma.yaml
        new file:   ikebe/tsudanuma/navigation/map_tsudanuma.pgm
        new file:   ikebe/tsudanuma/navigation/map_tsudanuma.yaml
        new file:   ikebe/tsukuba/localization/map_tsukuba.pgm
        new file:   ikebe/tsukuba/localization/map_tsukuba.yaml
        new file:   ikebe/tsukuba/navigation/map_tsukuba.pgm
        new file:   ikebe/tsukuba/navigation/map_tsukuba.yaml
```

追加出来てそうです。

6. `git commit`で変更内容をgitに登録(vimでcommitしたい場合は`git config --global core.editor vim`)

デフォルトだと`git commit`時にnanoエディタが立ち上がってしまいます。

お好きなエディタを登録すると良いです。ちなみにvimがオススメです。(エディタ戦争がはじまる)

インデックスに追加した内容をcommitします。

```
ikebe@ikebe:~/pgm_map_data$ git commit
```

すると以下のような文字がずらっと出てきます。

```

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# ブランチ add/ikebe-pgm-map
# コミット予定の変更点:
#       new file:   ikebe/tsudanuma/localization/map_tsudanuma.pgm
#       new file:   ikebe/tsudanuma/localization/map_tsudanuma.yaml
#       new file:   ikebe/tsudanuma/navigation/map_tsudanuma.pgm
#       new file:   ikebe/tsudanuma/navigation/map_tsudanuma.yaml
#       new file:   ikebe/tsukuba/localization/map_tsukuba.pgm
#       new file:   ikebe/tsukuba/localization/map_tsukuba.yaml
#       new file:   ikebe/tsukuba/navigation/map_tsukuba.pgm
#       new file:   ikebe/tsukuba/navigation/map_tsukuba.yaml
#
# Changes not staged for commit:
#       modified:   README.md
```

```
Add ikebe pgm map
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# ブランチ add/ikebe-pgm-map
# コミット予定の変更点:
#       new file:   ikebe/tsudanuma/localization/map_tsudanuma.pgm
#       new file:   ikebe/tsudanuma/localization/map_tsudanuma.yaml
#       new file:   ikebe/tsudanuma/navigation/map_tsudanuma.pgm
#       new file:   ikebe/tsudanuma/navigation/map_tsudanuma.yaml
#       new file:   ikebe/tsukuba/localization/map_tsukuba.pgm
#       new file:   ikebe/tsukuba/localization/map_tsukuba.yaml
#       new file:   ikebe/tsukuba/navigation/map_tsukuba.pgm
#       new file:   ikebe/tsukuba/navigation/map_tsukuba.yaml
#
# Changes not staged for commit:
#       modified:   README.md
```

7. `git push --set-upstream origin hoge/hoge`でGitHubにpush

8. GitHub上でブランチが追加されていることを確認

9. PRを作成する

10. squash mergeを行う

11. ブランチを削除する

12. masterブランチを更新する