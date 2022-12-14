# Maybe(Monad) {#maybe-api}

此处阅读到的 Maybe 可能与其他函数式语言（如 Haskell）中的 Data Maybe 并不相同。PureEval 中的 Maybe 是一个 Data Maybe 与 Class Monad 的融合。

## Maybe {#maybe}

Maybe 类型内包含一个不确定的值。

`undefined` 与 `null` 值都将被认为 [Nothing](#Noting)。

- **Type**

$$Data\ Maybe\ a=Just\ a\ |\ Nothing$$

### Maybe.lift() {#lift}

将一个值提升为 $Maybe$ 类型。

- **Type**

$$a\rightarrow Maybe\ a$$

- **Example**

```js
Maybe.lift(1);//Just 1
Maybe.lift(null);//Nothing
```

### Maybe.is() {#is}

判断一个值是否为 $Maybe$ 类型。

- **Type**

$$*\rightarrow Bool$$

- **Example**

```js
Maybe.is(Just(1));//true
Maybe.is(Nothing);//true
```

### Maybe.isNothing() {#isnothing}

判断该 $Maybe$ 是否为 $Nothing$。

- **Type**

$$\overline{Maybe\ a}\rightarrow Bool$$

- **Example**

```js
Just(1).isNothing();//false
Just(null).isNothing();//true
```

### Maybe.map() {#map}

- **Type**

$$\overline{Maybe\ a}\rightarrow (a\rightarrow b)\rightarrow Maybe\ b$$

- **Example**

```js
Just(1).map(add(114513));//Just 114514
```

### Maybe.chain() {#chain}

- **Type**

$$\overline{Maybe\ a}\rightarrow (a\rightarrow b)\rightarrow b$$

- **Example**

```js
Just(1).chain(add(114513));//114514
```

### Maybe.fold() {#fold}

将函数应用到 $Maybe\ a$ 中的 $a$。

传入两个单元函数参数，分别代表 $Maybe\ a$ 为 $Nothing$ 与 $Maybe$ 不为 $Nothing$ 的处理情况。

当匹配到 $Maybe\ a$ 时，对应函数将会应用到 $a$ 上，其函数值将作为返回值。


- **Type**

$$\overline{Maybe\ a}\rightarrow (Nothing\rightarrow b)\rightarrow (a\rightarrow b)\rightarrow b$$

- **Example**

```js
Just("The body next door").fold(
    () => "Nothing", 
    common
); //"The body next door"
```

## Just() {#just}

$Maybe$ 类型的构造函数。

实际同

- **Type**

$$a\rightarrow Maybe\ a$$

- **Example**

```js
Just(1);//Just 1
```

## Nothing {#Nothing}

$Maybe$ 类型的构造函数。