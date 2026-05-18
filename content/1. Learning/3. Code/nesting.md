## Nesting trong SCSS

Nesting cho phép viết CSS lồng nhau theo cấu trúc component.
```scss
.card {
  padding: 16px;

  .title {
    font-size: 20px;
  }

  .description {
    color: gray;
  }
}
```

### Dùng &
& đại diện cho selector cha.

```scss
.button {
  background: blue;

  &:hover {
    background: darkblue;
  }

  &.disabled {
    opacity: 0.5;
  }
}
```
