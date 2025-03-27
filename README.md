# ToastModoki
"Toast" replacement for GameJolt FNF Integration, running on Psych Engine v0.7.3

(All texts filled in in English are from texts translated by DeepL translations.)

# (+ === JP texts === +) (EN is below)
Psych Engine v0.7.3でGameJolt FNF Integrationを実装したい？

なら、Toastの代わりにこれを使ってみて！

## はじめに
まず、これは[TentaRJ](https://github.com/TentaRJ)氏が提供している[GameJolt FNF Integration](https://github.com/TentaRJ/GameJolt-FNF-Integration)に搭載されている、**Toast**なる代物をPsych Engine v0.7.3でそれっぽく実装するために作成されたものです。

（まぁ別にどんな用途でも使える代物ではありますが）

なので、このREADME.mdではPsych Engine v0.7.3に[GameJolt FNF Integration](https://github.com/TentaRJ/GameJolt-FNF-Integration)を実装する方法も含めて使用方法を説明いたします。

興味ない人は **「これのつかいかた」** まで飛ばして構いません！

## Null Object Referenceとかいう悪魔
[GameJolt FNF Integration](https://github.com/TentaRJ/GameJolt-FNF-Integration)をぶち込むこと自体は、そっちのREADME.mdを翻訳してぱぱーっとやれば可能です。

なのでそっちの説明は省きますが、きっとそうした後にゲームをビルドしたら、開始直後に「Null Object Reference」というエラーが発生して訳も分からずソフトが強制終了してしまうと思います。

<ins>まず、それの原因はToastのせいです。</ins>

**解決方法：`Gamejolt.hx`の、`Main.gjToastManager.createToast`というコードはコメントアウトしておき、その他のToastに関連する全てのコードは消してください。もし、`Main.hx`にToastに関連するコードを追加していたならば、それも消してください。**

これで、ゲームが起動できるはずです。

実は、これでGamejoltにゲームを連携させるプロセス（下準備）はもうこれでほぼ完了しています。もう、GamejoltのAPIを使う際に大きな邪魔になるものはほとんどありません。

……しかし、それでもまだ足りない部分があります。それこそが、 **Toast** です。

![VS  Camellia 2025_03_26 17_20_06](https://github.com/user-attachments/assets/ea3df435-f4b9-44fd-b852-44a3ab3abe86)

VS Camelliaを遊んだことありますか？あれでGamejoltにログインすると、こういう感じでGamejoltに関するなんかそういう文章がにゅ～んと出てくるんですが……

**……あれがToastです。** そうです。Toastは、あのにゅ～んって文章を右上に出すアレのことなのです。

トースターでパン焼いたら、焼けたパンがポンと出てくるでしょ？多分それが名前の由来なんだと思います（知らんけど）。

だから、 **Toastが無くてもGamejoltのアレ自体は搭載できるんです、完璧に。**

なぜなら、Toastそのものはただ文章を右上ににゅ～んと出すだけの代物だから。

ぶっちゃけ無くても明確に困ることはほとんど無いし、Toast以外になんかポップアップする手段があるならそれで構わないのです！！！

おぶじぇくとのりふぁれんすがぬるぬるしてソフトが心臓麻痺起こして使えないなら、別に使わなくたって何も問題ない代物ではあるのです。

……ん？　**ポップアップする手段があるならそれで構わない……？**

そうだ！　せっかくPsych Engine使ってるんだし、 **あの実績達成した時に出てくるポップアップで代用しよう！！！！！**
<br/>
<br/>
<br/>
という経緯で出来上がったのがこれというわけなんですよね～～～ **やはり先人は偉大なり……**

というわけで、そんなPsych Engine v0.7.3では使えなくなってしまったToastの代わりとなるオブジェクト、ToastModokiの使い方をここからちゃんと説明致します。

**これであなたも、Toast(のようなもの)まで実装したGamejolt連携機能搭載のFNFMODを、晴れて制作することができます！！！！！** やったね

## これのつかいかた

(1): 中に`assets`フォルダと`source`フォルダがありますね？それをあなたのFNFプロジェクトのフォルダにそのままぶち込んでください。

(2): ToastModokiを使いたい場合は、そのhxファイルの最初の部分にまずこれを書いてください。
```
import objects.ToastModoki;
```
(3): ToastModokiを使いたい場所で以下のコードを書けば無事ToastModokiが右上に表示されるはずです。
```
new ToastModoki(achieve:String, achiName:String, achiDesc:String, onFinish:Void->Void);
```
> `achieve:String`: 表示する画像の名前。`assets/shared/images/toastmodoki`フォルダの画像を参照しています。
> `achiName:String`: 表示したい文章の上側。
> `achiDesc:String`: 表示したい文章の下側。
> `onFinish:Void->Void`: わからん `null`って書いといて

……えー、まじでこれだけです。

あとはいくらでも自由に使えると思います。

おすきにどうぞ

## その他`Gamejolt.hx`に必要そうな改造まとめ

これを行えばもう完全かつ完璧に[GameJolt FNF Integration](https://github.com/TentaRJ/GameJolt-FNF-Integration)の実装をPsych Engine v0.7.3で行えると思います。
ぐっどらっく

(1): 最初の部分に`import states.MainMenuState;`を書いてください。

(2): `FlxG.switchState(new GameJoltLogin());`を以下のコードに変更してください。（変更しないと2回目のログイン画面で退出した際におぶじぇくとのりふぁれんすがぬるぬるする）
```
MusicBeatState.switchState(new MainMenuState());
```
(3): `authDaUser`のログインに成功した際のコードにある`startSession();`の真下にこのコードを書いてください。（無いとログイン画面に行かない限りスコアを反映するかどうかのフラグがfalseのままになる）
```
                        if (FlxG.save.data.lbToggle != null)
                            {
                                GameJoltAPI.leaderboardToggle = FlxG.save.data.lbToggle;
                            }
                        trace("score submit: " + GameJoltAPI.leaderboardToggle);
```
(4): 先ほどコメントアウトしていた`Main.gjToastManager.createToast`の部分に、以下のコードたちを参考にそれっぽくToastModokiを入れてください。（`import objects.ToastModoki;`を忘れずに！）
```
new ToastModoki('yes_icon', 'Signed in!', 'User: '+in1, null);
new ToastModoki('not_icon', 'Not Signed in!', 'Sign in to save GameJolt Trophies and Leaderboard Scores!', null);
new ToastModoki('yes_icon', 'Score submitted!', 'Score: '+score+"\n"+extraData, null);
new ToastModoki('not_icon', 'Score not submitted!', 'Score: '+score+"\n"+extraData, null);
new ToastModoki((GameJoltAPI.leaderboardToggle ? 'yes_icon':'not_icon'), 'Score submitting:', (GameJoltAPI.leaderboardToggle ? "Enabled":"Disabled"), null);
```
>　`#if debug`とか書かれてる部分のToastには多分いらないと思います
(5): ついでに、`tokenBox.passwordMode = true;`を`tokenBox = new FlxUIInputText`とか書かれてる場所の真下に書いといてください。Tokenを書く欄のテキストがパスワード風になって、うかつに覗けなくなります。配信者にやさしいね
>
(6):あ、`MainMenuState`に`GameJoltLogin`へ移動できるメニューのアレを追加しないと、ログイン画面に行く手段がありません！なんかそれっぽく追加しておいてください。

(7):~~そろそろ書くのめんどくさくなってきたな……~~ 実際にGamejoltの実績やスコアボードに対応させるコードを書くのは、ここまでいろいろ書いてコーディングしてプログラムを理解してきた人なら割と苦じゃないだろうと思いますが、一応私が他にコーディングしたあれこれを参考程度に載せておきます。

```
var gjsbid:Int = gjScoreboardID(daSong);
/*
trace('Rating: ' + Std.int(CoolUtil.floorDecimal(rating * 10000000, 0)));
trace('Score: ' + score);
trace('Login: ' + GameJoltAPI.getStatus());
trace('Table ID: ' + gjsbid);
*/
if (GameJoltAPI.getStatus()){
  if (gjsbid != 0) GameJoltAPI.addScore(Std.int(CoolUtil.floorDecimal(rating * 10000000, 0)), gjsbid, '(${score}) - ${fc}');
}
```
```
static function gjScoreboardID(songname:String):Int
{
	if (songname == 'welcome-to-000-hard') return 222222 
		else if (songname == 'welcome-to-000-ecstasy') return 222222 
		else if (songname == 'electro-chubby-hard') return 222222 
		else if (songname == 'electro-chubby-ecstasy') return 222222 
		else if (songname == 'empty-hard') return 222222
		else if (songname == 'empty-ecstasy') return 222222 
			else return 0;
}
```
> `Highscore.hx`の`saveScore`に書いてたコードの一部です。いろいろ改変してる箇所がありますが、まぁ大体どんな感じかわかればいいと思うので……


# (+ === EN texts === +)
Want to implement GameJolt FNF Integration with Psych Engine v0.7.3?
Then try this instead of Toast!
