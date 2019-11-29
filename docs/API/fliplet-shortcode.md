# Shortcode JS APIs

<p class="warning">You are browsing an early private spec of this feature.</p>

## Register a shortcode

`Fliplet.Shortcode(name, definition)`


```js
Fliplet.Shortcode('welcome', {
  data: {
    name: 'John'
  }
});
```

```html
{! start welcome !}
  <p>Hi {! name !}, how are you?</p>
{! end welcome }
```

### Attributes

#### Passing attributes to a shortcode

```js
Fliplet.Shortcode('welcome', {
  data: {
    first_name: 'John'
  }
});
```

### Templates

```html
{! start welcome last_name="Doe" !}
  <p>Hi {! first_name !} {! attr.last_name}, how are you?</p>
{! end welcome }
```

#### Defining a custom template

```js
Fliplet.Shortcode('welcome', {
  template: '<p>Hi {! first_name !} {! attr.last_name}, how are you?</p>'
  data: {
    first_name: 'John'
  }
});
```

```html
{! welcome last_name="Doe" !}
```

#### Defining an outer template

Use the `<slot></slot>` tag to serve as distribution outlets for content.

```js
Fliplet.Shortcode('welcome', {
  template: '<p>How are you? <slot></slot></p>'
  data: {
    first_name: 'John'
  }
});
```

```html
{! start welcome first_name="John" !}
  <span>I am <i>good</i> because my name is {! first_name !}!</span>
{! end welcome !}
```

Output:

```
<p>
  How are you?
  <span>I am <i>good</i> because my name is John!</span>
</p>
```

### Nested shortcodes

#### Register a nested shortcode

Pass the `child: true` attribute in the shortcode definition to register the shortcode as a nested shortcode for other components.

```js
Fliplet.Shortcode('greet', {
  template: '<p>Hi {! first_name !} {! attr.last_name !}</p>'
  data: {
    first_name: 'John'
  },
  child: true
});

Fliplet.Shortcode('profile', {});
```

```html
{! start welcome !}
  <h1>Welcome to the app!</h1>
  {! greet last_name="Doe" !}
{! end welcome }
```

<script>
window.isBetaFeature = true;
</script>