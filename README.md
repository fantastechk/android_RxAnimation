<p align="center"><img src="/preview/header.png"></p>

<img src="/preview/title.gif" alt="title" title="title" width="300" height="87.8" />

This is an Android library to make a simple way to animate your views on Android with Rx.

<a href="https://play.google.com/store/apps/details?id=com.fantastechk.lopspower">
  <img alt="Android app on Google Play" src="https://developer.android.com/images/brand/en_app_rgb_wo_45.png" />
</a>

USAGE
-----

Add RxAnimation library under **Rx3** with Gradle:

```groovy
implementation 'com.fantastechk:rxanimation:2.0.0'
```

:warning: If you use **Rx2** you need to implement the following version:


```groovy
implementation 'com.fantastechk:rxanimation:1.0.0'
```

KOTLIN
-----

<img src="/preview/0.gif" alt="sample" title="sample" width="250" height="160" align="right" />

-   Animate your views and handle it in [Completable](http://reactivex.io/RxJava/3.x/javadoc/io/reactivex/rxjava3/core/Completable.html). For example **`alpha()`** and **`resize()`**:

```kotlin
view1.alpha(1f)
    .andThen(view2.resize(100, 100))
```

<br/>

<img src="/preview/1.gif" alt="sample" title="sample" width="250" height="160" align="right" />

-   If you want to apply animation in the same time you can used **`RxAnimation.together()`**:

```kotlin
RxAnimation.together(
    view1.fadeIn(),
    view1.translation(20f, 30f),
    view2.backgroundColor(
        ContextCompat.getColor(this, R.color.accent),
        ContextCompat.getColor(this, R.color.primary)
    ),
    view2.resize(100, 100)
)
```

<img src="/preview/2.gif" alt="sample" title="sample" width="250" height="160" align="right" />

-   If you want to apply animation one by one you can used **`RxAnimation.sequentially()`** instead of multi `andThen()`:

```kotlin
RxAnimation.sequentially(
    view1.fadeIn(),
    view1.translation(20f, 30f),
    view2.backgroundColor(
        ContextCompat.getColor(this, R.color.accent),
        ContextCompat.getColor(this, R.color.primary)
    ),
    view2.resize(100, 100)
)
```

<img src="/preview/3.gif" alt="sample" title="sample" width="250" height="160" align="right" />

-   You can also used **`RxAnimation.from(view)`** if you want to update multi properties one by one in the same view:

```kotlin
RxAnimation.from(view)
    .fadeIn()
    .translation(20f, 30f)
    .backgroundColor(
        ContextCompat.getColor(this, R.color.accent),
        ContextCompat.getColor(this, R.color.primary)
    )
    .resize(100, 100)
```

<img src="/preview/4.gif" alt="sample" title="sample" width="250" height="160" align="right" />

-   You can also use the **`range()`** function to animate a change on a custom property:

```kotlin
(4f to 20f).rangeFloatToCompletable { 
    circularImageView.borderWidth = it 
}

// or

RxAnimation.from(circularImageView)
    .rangeFloat(4f, 20f) { circularImageView?.borderWidth = it }
```

-   Use `reverse` properties to back to the initial value in all methods:

```kotlin
view.fadeIn(reverse = true)
```

-   If you want to repeat an animation you can use the native method [`repeat`](http://reactivex.io/documentation/operators/repeat.html) from Rx like this:

```kotlin
RxAnimation.from(view)
    .fadeIn()
    .shake()
    .fadeOut()
    .repeat(NB_REPEAT)
    .subscribe()
```

ALL PROPERTIES
-----

### Default

| Properties           | View to Completable | RxAnimation.from(view) |
| -------------------- | ------------------- | ---------------------- |
| alpha                | alpha               | alpha                  |
| translationX         | translationX        | translationX           |
| translationY         | translationY        | translationY           |
| translation X + Y    | translation(X, Y)   | translation(X, Y)      |
| scaleX               | scaleX              | scaleX                 |
| scaleY               | scaleY              | scaleY                 |
| scale X = Y          | scale               | scale                  |
| rotation             | rotation            | rotation               |
| rotationX            | rotationX           | rotationX              |
| rotationY            | rotationY           | rotationY              |
| X                    | x                   | x                      |
| Y                    | y                   | y                      |
| Z                    | z                   | z                      |
| X + Y + Z            | xyz                 | xyz                    |
| backgroundColor      | backgroundColor     | backgroundColor        |
| width                | width               | width                  |
| height               | height              | height                 |
| width + height       | resize              | resize                 |
| ValueAnimator        | start               | startValueAnimator     |
| ViewPropertyAnimator | animate             | -                      |

### Custom Properties

| View to Completable     | RxAnimation.from(view) |
| ----------------------- | ---------------------- |
| rangeFloatToCompletable | rangeFloat             |
| rangeIntToCompletable   | rangeInt               |

### Smart function

| Animation | View to Completable | RxAnimation.from(view) |
| --------- | ------------------- | ---------------------- |
| alpha=1f  | fadeIn              | fadeIn                 |
| alpha=0f  | fadeOut             | fadeOut                |
| shake     | shake               | shake                  |
| press     | press               | press                  |
| text      | text                | text                   |

:information_source: All the functions have `duration: Long`, `interpolator: TimeInterpolator`, `startDelay: Long` and `reverse: Boolean` properties.