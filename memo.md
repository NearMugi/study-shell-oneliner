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

## P19 : sed

```bash
word=クロロメチルエチルエーテル
echo $word 

# エチルを2回繰り返す方法
# & は検索対象の文字を指している
echo $word | sed -E 's/エチル/&&/'

# メチルとエチルを逆にする
# \1, \2 は後方参照。()で括ったものを順番に番号が与えられている
echo $word | sed -E 's/(メチル)(エチル)/\2\1/'

# メチルとエチルを逆にする
# echo $word | sed -E 's/(クロロ).*(エチル)/\2\1/'
# ではダメ
# ↓こうする
echo $word | sed -E 's/(クロロ).*(エチル)/\2メチル\1/'

```

## P20 : ゾロ目を取得

``` bash
# (.) は任意の一文字、取得した値を\1で繰り返す
# ^ をつけることで"先頭の"となるので100は対象外になる
# xargs は横に並べるためだけに使用
seq 100 | grep -E '^(.)\1$' | xargs
```

出力結果

``` bash
11 22 33 44 55 66 77 88 99
```

## P21 : grepによる切り出し

オプションの```-o```は一致するものを切り出す指定

```bash
word="中村 山田 田代 上田"
# [^ ]田 はスペースではない１文字の後ろに田が付くという意味
echo $word | grep -o "[^ ]田"
```

出力結果

```bash
山田
上田
```

## P23 : gawkのインストール

```bash
sudo apt install gawk
```

## P23 : awk

``` bash
# 1~5
seq 5
# 1~5 を表示
seq 5 | awk '{print "value:" $1}'

# 1~5 のうち、2,4を出力する
seq 5 | awk '/[24]/'
seq 5 | awk '$1%2==0'
seq 5 | awk '$1%2==0{print $1,"偶数"}'
seq 5 | awk '$1%2==0{printf("%s 偶数\n", $1)}'

# 偶数、奇数で出力を変える
seq 5 | awk '$1%2==0{print $1,"偶数"} $1%2==1{print $1,"奇数"}'
# 合計も出力する
seq 5 | awk 'BEGIN{a=0} $1%2==0{print $1,"偶数"} $1%2==1{print $1,"奇数"} {a+=$1} END {print "合計",a}'
# BEGIN で行っているaの初期化は省略できる
seq 5 | awk '$1%2==0{print $1,"偶数"} $1%2==1{print $1,"奇数"} {a+=$1} END {print "合計",a}'


```

