# ios-licence-auto-make-demo
OSSライセンスを設定画面に自動生成するサンプル<br><br>

![screen shot 2017-04-14 at 13 11 07](https://cloud.githubusercontent.com/assets/9479568/25032971/e3a24706-2113-11e7-98f6-650d61386b27.png)

## 手順
### 1. Podfileに下記を追加する
対象のプロジェクト名に変更すること

```
post_install do | installer |
require 'fileutils'
FileUtils.cp_r('Pods/Target Support Files/Pods-<プロジェクト名>/Pods-<プロジェクト名>-Acknowledgements.plist', '<プロジェクト名>/Settings.bundle/Acknowledgements.plist', :remove_destination => true)
end
```

### 2. Settings.bundleのRoot.plistを編集する

File > New > File > Resource > Settings Bundleを選択し、Settings.bundleを作成する。　<br>
Root.plistを下記のように変更する。<br>

<img width="206" alt="2017-04-14 13 07 28" src="https://cloud.githubusercontent.com/assets/9479568/25032927/6387d964-2113-11e7-9b44-f97c80d1cc4c.png">

```:Root.plist
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>StringsTable</key>
	<string>Root</string>
	<key>PreferenceSpecifiers</key>
	<array>
		<dict>
			<key>Type</key>
			<string>PSGroupSpecifier</string>
			<key>Title</key>
			<string>サポート</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSChildPaneSpecifier</string>
			<key>Title</key>
			<string>Acknowledgements</string>
			<key>File</key>
			<string>Acknowledgements</string>
		</dict>
	</array>
</dict>
</plist>
```

### 3. Acknowledgements.plistを作成する
Root.plistをコピーし、Acknowledgements.plistにリネイムする。<br>
Acknowledgements.plistの中身は、空にする

### 4. pod install or pod updateを実行する

### 参考記事
http://mzgk.github.io/blog/2014/cocoapods-license-auto-make/
