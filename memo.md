# メモ

## WSL で学習する

WSLが開かない場合の対処  
[WSL2のUbuntuを初期化する](https://www.evernote.com/shard/s503/nl/87526629/15f1d39b-a324-45ec-9a51-cb5e8539d59e?title=WSL2%E3%81%AEUbuntu%E3%82%92%E5%88%9D%E6%9C%9F%E5%8C%96%E3%81%99%E3%82%8B)

``` bash
# [設定] > [アプリ]を選択。
# [アプリと設定]を選択。
# リセットしたいLinuxのディストリビューションを選択し、[詳細オプション]をクリック。
# [リセット]をクリック。
# パソコンを再起動した後、powershell を開いてWSLコマンドを実行
WSL
```

``` bash
# バージョンの確認
wsl -l -v 
```


## P17 : 環境とmanの日本語化 

パッケージのインストール

```bash
sudo apt update
sudo apt install manpages-ja
sudo apt install manpages-ja-dev

sudo apt install language-pack-ja

# 端末を立ち上げなおす
# 日本語になっていることを確認する
man ls 
```

## P18 : grep -A 1 

マッチした行のあとの1行も出力するというオプション

``` bash
man ls | grep -A 1 '^  *-a'
```

``` bash
       -a, --all
              . で始まる要素を無視しない
```

### P20 : ゾロ目を取得

``` bash
# (.) は任意の一文字、取得した値を\1で繰り返す
# ^ をつけることで"先頭の"となるので100は対象外になる
# xargs は横に並べるためだけに使用
seq 100 | grep -E '^(.)\1$' | xargs
```

``` bash
11 22 33 44 55 66 77 88 99
```