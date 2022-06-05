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
ikebe@ikebe:~/pgm_map_data (add/ikebe-pgm-map)$ git commit
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

一番上にコメントを追加します。

一番最初は大文字にしましょう。commitの内容についてコメントすれば良いです。


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

いよいよ`git push`です。

まだ今回作成したブランチは`GitHub`上に無いので`git push`
すると、以下のような文が出力されます。

```
ikebe@ikebe:~/pgm_map_data (add/ikebe-pgm-map)$ git push
fatal: The current branch add/ikebe-pgm-map has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin add/ikebe-pgm-map
```

出力された文の通りに実行すると`push`できます。

ファイル制限のワーニングが出ていますが。
pushできてるのでヨシッ！（なんで、ヨシっていったんですか。。）

```
ikebe@ikebe:~/pgm_map_data (add/ikebe-pgm-map)$ git push --set-upstream origin add/ikebe-pgm-map
Enumerating objects: 16, done.
Counting objects: 100% (16/16), done.
Delta compression using up to 8 threads
Compressing objects: 100% (15/15), done.
Writing objects: 100% (15/15), 2.71 MiB | 1.16 MiB/s, done.
Total 15 (delta 3), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (3/3), completed with 1 local object.
remote: warning: See http://git.io/iEPt8g for more information.
remote: warning: File ikebe/tsukuba/localization/map_tsukuba.pgm is 63.63 MB; this is larger than GitHub's recommended maximum file size of 50.00 MB
remote: warning: File ikebe/tsukuba/navigation/map_tsukuba.pgm is 63.63 MB; this is larger than GitHub's recommended maximum file size of 50.00 MB
remote: warning: GH001: Large files detected. You may want to try Git Large File Storage - https://git-lfs.github.com.
remote: 
remote: Create a pull request for 'add/ikebe-pgm-map' on GitHub by visiting:
remote:      https://github.com/CIT-Autonomous-Robot-Lab/pgm_map_data/pull/new/add/ikebe-pgm-map
remote: 
To github.com:CIT-Autonomous-Robot-Lab/pgm_map_data.git
 * [new branch]      add/ikebe-pgm-map -> add/ikebe-pgm-map
Branch 'add/ikebe-pgm-map' set up to track remote branch 'add/ikebe-pgm-map' from 'origin'.
```

8. GitHub上でブランチが追加されていることを確認

[CIT-Autonomous-Robot-Lab/pgm_map_data](https://github.com/CIT-Autonomous-Robot-Lab/pgm_map_data)

[![Image from Gyazo](https://i.gyazo.com/f97372656bf25195ea3958c0d88dd4c0.png)](https://gyazo.com/f97372656bf25195ea3958c0d88dd4c0)

9. PRを作成する

[![Image from Gyazo](https://i.gyazo.com/2192eca9d205f70bc0bca0eb460af1e2.png)](https://gyazo.com/2192eca9d205f70bc0bca0eb460af1e2)

[![Image from Gyazo](https://i.gyazo.com/ebc0c7f9b9a87b979d5938fbf3f3ebba.png)](https://gyazo.com/ebc0c7f9b9a87b979d5938fbf3f3ebba)

10. squash mergeを行う

[![Image from Gyazo](https://i.gyazo.com/a013ec4518e1d3e9bc7d84348da78c9e.png)](https://gyazo.com/a013ec4518e1d3e9bc7d84348da78c9e)

[![Image from Gyazo](https://i.gyazo.com/e5e28d8a6d1838437250a0907054c943.png)](https://gyazo.com/e5e28d8a6d1838437250a0907054c943)

[![Image from Gyazo](https://i.gyazo.com/3b70eacb8ebc9bcccbf3178159ac155a.png)](https://gyazo.com/3b70eacb8ebc9bcccbf3178159ac155a)

11. ブランチを削除する

[![Image from Gyazo](https://i.gyazo.com/7ce3a3f776c093b7ed6fc06a8f2fbb9d.png)](https://gyazo.com/7ce3a3f776c093b7ed6fc06a8f2fbb9d)

12. でけた！

[![Image from Gyazo](https://i.gyazo.com/27206427c76e8c54d1282c31f4dd39a7.png)](https://gyazo.com/27206427c76e8c54d1282c31f4dd39a7)

13. masterブランチを更新する

これで完了。と思いましたか？

まだ手元にあるPCの方の`master`ブランチは更新されていません。

せっかくなので次に修正や追加する時のために`git pull`をして更新をしましょう。

まずは`master`ブランチに移動します。

```
ikebe@ikebe:~/pgm_map_data (add/ikebe-pgm-map)$ git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.

ikebe@ikebe:~/pgm_map_data (master)$
```

`master`に切り替えることができました。
ということで`git pull`をして更新します。

```
ikebe@ikebe:~/pgm_map_data (master)$ git pull
remote: Enumerating objects: 16, done.
remote: Counting objects: 100% (16/16), done.
remote: Compressing objects: 100% (12/12), done.
remote: Total 15 (delta 3), reused 14 (delta 3), pack-reused 0
Unpacking objects: 100% (15/15), 2.71 MiB | 1.99 MiB/s, done.
From github.com:CIT-Autonomous-Robot-Lab/pgm_map_data
   40af2ae..aa37fe0  master     -> origin/master
Updating 40af2ae..aa37fe0
Fast-forward
 ikebe/tsudanuma/localization/map_tsudanuma.pgm  | 1183 +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
 ikebe/tsudanuma/localization/map_tsudanuma.yaml |    7 +
 ikebe/tsudanuma/navigation/map_tsudanuma.pgm    | 1158 +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
 ikebe/tsudanuma/navigation/map_tsudanuma.yaml   |    7 +
 ikebe/tsukuba/localization/map_tsukuba.pgm      |  302 ++++++++++++++++++
 ikebe/tsukuba/localization/map_tsukuba.yaml     |    7 +
 ikebe/tsukuba/navigation/map_tsukuba.pgm        |  286 +++++++++++++++++
 ikebe/tsukuba/navigation/map_tsukuba.yaml       |    7 +
 8 files changed, 2957 insertions(+)
 create mode 100644 ikebe/tsudanuma/localization/map_tsudanuma.pgm
 create mode 100644 ikebe/tsudanuma/localization/map_tsudanuma.yaml
 create mode 100644 ikebe/tsudanuma/navigation/map_tsudanuma.pgm
 create mode 100644 ikebe/tsudanuma/navigation/map_tsudanuma.yaml
 create mode 100755 ikebe/tsukuba/localization/map_tsukuba.pgm
 create mode 100755 ikebe/tsukuba/localization/map_tsukuba.yaml
 create mode 100755 ikebe/tsukuba/navigation/map_tsukuba.pgm
 create mode 100755 ikebe/tsukuba/navigation/map_tsukuba.yaml
```

更新できました。ということで以上が基本的なgit、GitHubでの開発フローです。

まだまだ、`git`や`GitHub`には色んな機能があるので気になったら調べると良いです。

ちなみに、以前PRに使用した同じブランチで別のPRを出すと面倒くさいことになるので、
名前は被らないようにすると良いです。