# GitHubで開発する準備
## 前準備
- GitHubアカウントを作成する。
- テスト用にリポジトリを作っておく。
- ローカルでGitが使えるようにインストールしておく。

Gitで以下の設定をすると今後ログに表示されるはず。
```
git config --global user.name "ユーザ名"
git config --global user.email "メール"
```

## SSHの設定
一人で開発する分には不要かもしれないが、クローンするのにSSH設定しておく。
- `~/.ssh`フォルダを作製し移動してSSH鍵を生成する
```
cd ~/.ssh
ssh-keygen -t rsa -C xxxxx@xxxxx.com
```

生成時に質問されるのでいくつか設定
```
- 鍵の名前
  id_git_rsa(デフォルトにすると上書きされる事があるのでGit用で名前を変えておく)
- パスフレーズ
  パスワードのようなもの、任意
```

`id_git_rsa`と`id_git_rsa.pub`の2つの鍵が生成される。

- id_git_rsa.pub（公開鍵）の中身をGitLab側のSSHの設定に利用する。
後ろのメールアドレスは要らない

- ファイル名を変えている場合、そのままでは接続できない。
※通常、id_rsaというファイルがデフォルトのファイルになっているため。
configファイルを作製して以下を設定を行う必要がある

```
Host gitlab gitlab.com
  HostName gitlab.com
  IdentityFile ~/.ssh/id_git_rsa #ここに自分の鍵のファイル名
  User git
```

- GitLabからSSHのパスをコピーしてきてクローン実施
```
git clone [GitLabでコピーしたSSHパス]
```

## その他
SSHを使わない場合は以下の様な感じ。
```
git clone [GitLabでコピーしたhttpsパス]
```
gitlabのアカウントとパスワードですぐクローンする事ができるが、
業務ではSSH鍵を採用する方がよい。

