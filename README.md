# react-native-lahk-marquee-label
> A react-native marquee label component.

If you need a vertical marquee label, please use [react-native-lahk-marquee-label-vertical](https://github.com/cheng-kang/react-native-lahk-marquee-label-vertical).

[![npm version](https://badge.fury.io/js/react-native-lahk-marquee-label.svg)](https://badge.fury.io/js/react-native-lahk-marquee-label)

## Anchors

1. [Desc](#desc)
2. [Install](#install)
3. [Usage](#usage)
4. [Props](#props)
5. [Update Log](#update-log)
6. [中文介绍](#中文介绍)

## Desc

[Skip this part, go to **#Install**](#install)

I needed a marquee label in one of my recent project and I didn't find a good one online, so I decided to create my own marquee label component.

I intended to make it work well on both iOS and Android, still there remains one thing in iOS which I cannot fix. I found that in **iOS**, when you use `View` component to wrap child components and don't explicitly set the parent `View` component width (e.g. use `flex`), the parent `View` component will have the same width as it's child. 

It becomes a problem in this custom component because I use a child `View` component to wrap `Text` component in order to make the text expand and show in one line. I **set the text containner `View` component size to be bigger than the `Text` so that it will not have multiple lines nor have the overflow text replaced by ellipsis.** The default value of text container width is 1000, which is usually larger than the actual label width. This results in the problem mentioned above, the wrapper `View` width becomes 1000 also.

```js
<View class="marquee-label">
  <View class="marquee-label-text-container">
    <Text class="marquee-label-text">{text}</Text>
  </View>
</View>
```

**Note:**

- In Andorid, you can use both `width` or `flex` to layout the view.
- In iOS, use `width` to layout the view. `flex` layout is not supported.


## Install

```sh
npm install --save react-native-lahk-marquee-label
```

## Usage

1. Import

```js
import MarqueeLabel from 'react-native-lahk-marquee-label';
```

2. Use

```js
<MarqueeLabel
  duration={8000}
  text={'This is a Marquee Label.'}
  textStyle={{ fontSize: 13, color: 'white' }}
/>
```

or

```js
<MarqueeLabel
  speed={250}
  textStyle={{ fontSize: 13, color: 'white' }}
>
  This is a Marquee Label.
</MarqueeLabel>
```

## Props

- `children`: string, the text to show in the marquee. Alternative to `text`.
- `text`: string, the text to show in the marquee. Alternative to `children`.
- `duration`: number(unit: millisecond), the duration for the marquee to run one round. e.g. 6000 (for 6 seconds a round). Alternative to `speed`.
- `speed`: number(unit: px/s, px per second), the speed of the marquee. Alternative to `duration`.
- `bgViewStyle`: stylesheet object, background view component custom styles.
- `textStyle`: stylesheet object, text component custom styles.
- `textContainerWidth`: number, text container component width. If the text is not shown in one line, increase this value.
- `textContainerHeight`: number, text container component height. If the text is not shown in one line, increase this value.
- `textContainerStyle`: stylesheet object, not recommended to use, text containner component custom style.

## Update Log

### 2017.08.21 `Version 1.1.0`

- Dynamic Text Support: now you can use dynamic text with this component :D

## 中文介绍

[跳转到 **#install**](#install)

我在一个项目中需要用到跑马灯，但是在网上没找到好用的。所以我就自己写了一个跑马灯的组件。

本来打算让它可以在 iOS 和 Android 平台上都好用的，不过还是在 iOS 平台上存在一个问题没法解决。

我发现在 iOS 平台上，当使用 `View` 组件来包裹子组件的时候，如果没有显示设置父级 `View` 组件的宽度（width 样式）（比如用 `flex` 布局），那么父级 `View` 组件的宽度会被自动设置成子组件的宽度。（至少当子组件比父组件宽度大时是这样的，另外一种情况我没有做试验。）

我的跑马灯组件中的问题在于，我用了一个子级 `View` 组件来包裹 `Text` 组件以保证文字是在一行全部显示。**通过将 text container 的宽度设置得比 `Text` 组件宽度大，保证了文字不会换行，也不会用省略号替换溢出文字。** text container 默认宽度为 1000，这比一般的跑马灯标签实际宽度要大。而这也就导致了上述的问题，最外层的 `View` 的宽度也变成了 1000。

```js
<View class="marquee-label">
  <View class="marquee-label-text-container">
    <Text class="marquee-label-text">{text}</Text>
  </View>
</View>
```

**因此要注意：**

- 在 Android 平台上，通过 `width` 或者 `flex` 布局来设置最外层 `View` 的样式都没问题。
- 在 iOS 平台上，请使用并且只能使用 `width` 来设置样式。
