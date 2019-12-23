tkato_module
============

作成したライブラリの寄せ集め


# バージョンまとめ

| ライブラリ名               | 最新バージョン | ライセンス | 更新日      |
| ------------------------ | ------------ | -------- | ---------- |
| Android                  |              |          |            |
| GeneralModule_Android    | 1.0.1        | MIT      | 2019/12/23 |
| BaseDialogModule_Android | 1.0.0        | MIT      | 2019/12/05 |
| PSFluxModule_Android     | 1.0.0        | MIT      | 2019/12/23 |
| PSFluxModule_Generator   | 1.0.0        | MIT      | 2019/12/23 |


# ライブラリまとめ

## Android

Android のライブラリを使用する際は、まず `repositories` を追記し、それから各ライブラリの `implementation` を設定してください。

```build.gradle
repositories {
    maven { url "https://tkato-89024.github.io/tkato_module/repository" }
}
```

### GeneralModule_Android
[https://github.com/tkato-89024/GeneralModule_Android](https://github.com/tkato-89024/GeneralModule_Android)

汎用ライブラリ。
`GeneralModule_iOS`と等価になる（予定）。
```build.gradle
dependencies {
    implementation ("jp.co.model.tkato:general-module:${versions.general_module}")
}
```

### BaseDialogModule_Android
[https://github.com/tkato-89024/BaseDialogModule_Android](https://github.com/tkato-89024/BaseDialogModule_Android)

汎用ダイアログライブラリ。
端末を回転させても、ダイアログそのものや、ボタンのリスナーが死なないように改良したもの。
```build.gradle
dependencies {
    implementation ("jp.co.model.tkato:basedialog-module:${versions.basedialog_module}")
}
```
```java
// FragmentActivity にて

@Override
protected void onCreate(@Nullable Bundle savedInstanceState) {
    BaseDialogFragment
        .use(this, "ダイアログIDを文字列指定", (activity, newDialogFragment) -> {
            // ダイアログをまだ作成していない場合の初期設定
            newDialogFragment.setElement(new DilaogElement(
                R.string.dialog_title,
                R.string.dialog_message,
                new DialogButtonElement("Positive", isDismiss,    activity),
                new DialogButtonElement("Negative", isDismiss,    activity),
                new DialogButtonElement("Neutral",  isNotDismiss, activity),
            ))
            // Element ではない、メソッドチェーンによる設定も可能
        })
        .show(this)
    ;
}

// BaseDialogFragment.OnClickListener は Activity か Fragment に実装したものでないと、画面回転時に復帰できないため
// それ以外のクラスに実装すると例外が発生する
@Override
public void onClick(BaseDialogFragment.OnClickListener self, @NonNull String identifier, BaseDialogFragment.ListenerType listenerType, @NonNull DialogInterface dialog) {
    if ("ダイアログIDを文字列指定".equals(identifier)) {
        switch (listenerType) {
        case Positive: break;
        case Negative: break;
        case Neutral:  break;
        }
    }
}
```
### PSFluxModule_Android
[https://github.com/tkato-89024/PSFluxModule_Android](https://github.com/tkato-89024/PSFluxModule_Android)

Publish-Subscribe 方式に則った Flux 実装補助モジュール。
`RxJava2`、`RxAndroid` を使用している。
```build.gradle
dependencies {
    implementation ("jp.co.model.tkato:psflux-module:${versions.psflux_module}")
}
```

## その他

### PSFluxModule_Generator
[https://github.com/tkato-89024/PSFluxModule_Generator](https://github.com/tkato-89024/PSFluxModule_Generator)

PSFluxModule を使用する際、Action / ActionCreator / Store のサブクラスを簡易生成するためのジェネレーター。
PSFluxModule を使用する場合に、ジェネレーターを使う。

python ファイルから実行する。
```sh
$ python3 psflux_model_generator_for_android
```
