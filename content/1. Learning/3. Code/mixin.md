## Mixin là gì?

Mixin là cách tái sử dụng một nhóm CSS trong SCSS/Sass.

```scss
@mixin flex-center {
  display: flex;
  justify-content: center;
  align-items: center;
}

.card {
  @include flex-center;
}

.modal {
  @include flex-center;
}
```


Mixin có tham số:
```scss
@mixin button($bg-color, $text-color) {
  background: $bg-color;
  color: $text-color;
  padding: 8px 16px;
  border-radius: 8px;
}

.primaryButton {
  @include button(#1677ff, white);
}

.dangerButton {
  @include button(#ff4d4f, white);
}
```

Mixin với media query
```scss
@mixin respond($breakpoint) {
  @if $breakpoint == tablet {
    @media (min-width: 768px) {
      @content;
    }
  }

  @if $breakpoint == desktop {
    @media (min-width: 1024px) {
      @content;
    }
  }
}

.card {
  width: 100%;

  @include respond(tablet) {
    width: 50%;
  }

  @include respond(desktop) {
    width: 25%;
  }
}
```
