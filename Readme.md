## 使用方法
オブジェクトにつけて、Animatorの参照を設定する  
Animatorがないと動かないので注意  
Animatorの位置はスクリプトと同じでなくてもOK  

## Animatorを非アクティブに(軽くなる)
```
_animation.DisActive();
```
※SerializeFieldの_isActiveStartをfalseにすると、起動時(Startのタイミング)にanimatorはUpdateされなくなる
animatorがenableである必要がある操作をしたいときは、Awakeでやるといいかも  
ここは派生前提なので、派生先でStartをカジュアルに使えるようにするため、設計を変更するかも  

## 再生(割込み可)
```
_animation.Play("open");
```

## 再生しつつ次の予約もする
```
_animation.Play("open");
_animation.PlayQueue("loop");
```

## 再生が終わったときにコールバックもらう
```
_animation.Play("close");
_animation.SetPlaybackDelegate(() =>
{
    _isActive = false;
    _animation.DisActive();
});
```

## 今後の修正予定
- アニメーションブレンドを想定した派生クラスのサンプルを作成
- コールバックとキュー再生は、Updateを使用せず、コルーチンにする
- その他こまごまとした設計の整理
