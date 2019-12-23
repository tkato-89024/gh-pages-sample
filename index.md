tkato_module
============

作成したライブラリの寄せ集め


# バージョンまとめ

| ライブラリ名               | 最新バージョン | ライセンス | 更新日      |
| ------------------------ | ------------ | -------- | ---------- |
| Android                  |              |          |            |
| GeneralModule_Android    | 1.0.1        | MIT      | 2019/12/23 |
| BaseDialogModule_Android | 1.0.0        | MIT      | 2019/12/05 |


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

### BaseDialogModule_Android

汎用ダイアログライブラリ。
端末を回転させても、ダイアログそのものや、ボタンのリスナーが死なないように改良したもの。
```build.gradle
dependencies {
    implementation ("jp.co.model.tkato:basedialog_module:${versions.general_module}")
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
