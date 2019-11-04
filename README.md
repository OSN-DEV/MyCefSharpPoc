# MyCefSharpPoc
WPF環境で標準のWebBrowserは卒業したいと思いネットで探して見つけたCefSharp。これが自分の開発で使えるのかを検証するための試作です。

Microsoft Visual Studio Community 2019  
Version 16.3.5  
.NET Framework 4.7.2


## 参考
* [WPFでCefSharp（Chromiumの.NET向け実装）を使う - 1](https://qiita.com/GHKEN/items/d2d8b0745ef2622a2bbc)
* [stack overflow](https://stackoverflow.com/questions/52394485/how-to-get-cefsharp-to-work-with-configuration-anycpu-in-vs-common-library)
* [CefSharp/CefSharp.Wpf.Example](https://github.com/cefsharp/CefSharp/tree/master/CefSharp.Wpf.Example)
* [CefSharpでAnyCPU対応に苦慮した話3](https://www.valuestar.work/news/archives/38)

## CefSharpの導入
* [ツール] - [NuGet パッケージマネージャー] - [ソリューションの NuGet パッケージ管理]
* [参照]タブを選択
* "CefSharp"で検索
* "CefShapr.Wpfを選択してインストール


## CefShapr使用の準備(失敗しました)
プロジェクトファイル(.csproj)をテキストエディタで開いて最初の `PropertyGroup` の先頭に以下の情報を追加
```
<CefSharpAnyCpuSupport>true</CefSharpAnyCpuSupport>
```

デフォルトではCefSharpはAny CPUに対応していないらしいので、それに対応するための処置。

x86、x64のどちらかで使用する前提なら不要。一応Any CPU対応にしてみたけど、いい加減x64一本で良いんじゃないかなぁという気がしなくもない。

Windowsの64bit OSってXPの頃からあったような気がするのだが。そういう問題ではなんですかね、、
↑
ビルドは通ったのですが、実行するとconnectionIdのパース失敗やBadImageFormatExceptionなどに遭遇しました。  
頑張るなら https://www.valuestar.work/news/archives/38 のように色々と頑張る必要があるっぽい。ここまで頑張る必要性が思い浮かばなのかっのでx64の環境を使用することにしました。。


## XAMLに配置
以下のような感じで名前空間の宣言を追加
```
xmlns:cs="clr-namespace:CefSharp.Wpf;assembly=CefSharp.Wpf"
```

* crl → clr
* ～.Wpf:assenbyly～ → ～.Wpf;assenbyly～
* ～.WPF → * ～.Wpf

のように誤字があったりするので手入力よりコピペ → 修正が望ましいかも。特に初回導入時は。。。(体験談))

