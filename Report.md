#概要
一週間の勉強した内容を一般的に説明する記事です。
勉強したことはAlexaVoiceService（AVS）とAlexaSkill、AWS　Iot、CakePhp、Cです。

## Alexa Voice Service - AVS
AVSでAlexa搭載製品を開発できて、どこからでもAlexaを呼び出せます。
AVSデバイスSDKを利用して自分の製品にAlexaを実装することができます・

### AVSをインストールし目見る
####Windowsで

- MSYS2をインストールします。
- チュートリアルのサンプルコンフィグスクリプトファイルを利用して実施します。
- AlexaCloudでプロダクトを作成します。
- SecurityProfileを作成します。
- サンプルアプリを開いて、認証するためAmazonでログインします。
- Alexaを楽しみにします。

Windows Sub-Linux Systemでインストールしてみましたけど、Wslはまだ機能が足りないのでできなかったです。

####Raspberry Piで

- AmazonDeveloperPortalでAlexaデバイスを作成します。レスポンスUrlを設定します。
- オーディオデバイスをRaspberryPiに接続します。
- 先ほど設定したUrlに接続して、作成したデバイスのcredentialsを入力します。
- サンプルアプリを使ってAlexaを利用します。

さらに、サンプルアプリのソースコードを見て、AVSドキュメントを読んで、プロダクトでのAlexaを修正できます。
例えばAlexaはいろいろの機能があり（Alarms, Music,..）、FocusManagerを利用して各機能の優先度を設定できます。

## Alexa Skills
簡単に言うとAlexaSkillsはAlexaの機能です。

### Alexa Skills Kit - ASK
ASkを利用してAlexaの新しい機能を作成できます。
スキルを作成するためにクラウドでホスト必要です。Alexaサービスは受信するリクエストを適切なサービスにルーティングします。

####CustomSkill-カスタムスキルを作成して見る
カスタムスキルを作成するのは２つの方法があります。

- ウエブサービスを開発する。（自分でホストすることが必要です）
- AWSのLambda関数。（サーバー管理必要がないですが、Node.js, Java, Python, C#,Goだけ使用できます。）

上の両方は同じことを担当します。Alexaはユーザーから命令を基づいてリクエストをAWSLambdaまたはウエブサービスのサーバーに送ります。
それから、AWSLambdaのコードあるいはウエブサービスはそのリクエストを処理して、レスポンスを戻します。

サーバーコードとAWSLambdaコードを書くとき、二つのスタイルがあり：

- AlexaのJSONリクエストを読み込んで、処理して、レスポンスのJSONを作成してAlexaに返します。
- ASKのSDKを利用します。

一番目のスタイルはどんな言語でも開発できます。だから、一応Goで１のスキルを作成しました。
二番目のスタイルはもっと楽になるけど、NodeJs、Java、Pythonだけ利用できます。

カスタムスキルの作成：

- ヴォイスユーザインタフェースを設計します。（対話の流れ）
- AlexaDeveloperConsoleで新しスキルを作成して、モデルを設定します。
- ウエブサービスまたはLambdaコードを作成します。
- スキルをテストします。

##### ASK SDKを利用してLambdaのコードを作る
Trash-outというスキルを作成しました。このスキルはユーザーに今日はだれがごみを捨てしなければならないかをリマインドします。
ユーザはヴォイスで人を追加でき（DynamoDbに保存）、削除でき、ごみを捨てたことをAlexaに言った後turnは他人に交わります。

