---
Title: rsync
Description: |
  rsync はファイルやディレクトリをローカル⇄ローカルやローカル⇄リモート間で効率よく同期・転送できるツール。

  主な特徴：
    - 差分転送（変更があった部分だけコピー）
    - 再開可能（転送途中で止まってもやり直せる）
    - 圧縮転送（帯域節約）
    - パーミッションやシンボリックリンク保持可能
    - 進捗表示もできる

  注：
    - rsync はデフォルトで SSH を使用する（22番ポート）
    - 転送元パスの末尾に / をつけるかどうかで挙動が変わる（つけるとディレクトリごとではなく中身を持ってくる挙動になる）

  よく使うオプション:
    - -a: アーカイブモード（再帰・パーミッション・シンボリックリンク等を保持）
    - -v: 詳細表示（verbose）
    - -z: 圧縮して転送（ネットワークの帯域節約。ただしCPU負荷はUP）
    - --progress: 転送中の進行状況を表示
    - --delete: 転送元にないファイルを転送先から削除（同期用途）
    - --partial: 中断されたファイルを一部保持（大きなファイルの転送の途中で失敗しても、そのファイルの途中から再開出来る）
    - -P: --partial --progressと同じ
    - -e "ssh": 通信にSSHを使用（デフォルトで使われるが明示的にも書ける）
Tags:
  - linux
  - file
---

```bash
// ローカルからリモートへ：ディレクトリそのものを送る
rsync -avzP dir user@remote:/dest
→ /dest/dir/

// ローカルからリモートへ：ディレクトリの中身だけ送る
rsync -avzP dir/ user@remote:/dest
→ /dest/(中身だけ)

// リモートからローカルへ：ディレクトリごと持ってくる
rsync -avzP user@remote:/path/to/dir /local/destination
```
