tkato_module
============

作成したライブラリの寄せ集め


# バージョンまとめ

| ライブラリ名            | 最新バージョン | ライセンス | 更新日      |
| --------------------- | ------------ | -------- | ---------- |
| Android               |              |          |            |
| GeneralModule_Android | 1.0.0        | MIT      | 2019/11/26 |


# ライブラリまとめ

## Android

Android のライブラリを使用する際は、まず `repositories` を追記し、それから各ライブラリの `implementation` を設定してください。

```build.gradle
repositories {
    maven { url "https://tkato-89024.github.io/tkato_module/repository" }
}
```

### GeneralModule_Android

汎用ライブラリ。
`GeneralModule_iOS`と等価になる（予定）。
```build.gradle
dependencies {
    implementation ("jp.co.model.tkato:general_module:${versions.general_module}")
}
```
