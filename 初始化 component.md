```
.
└── src
    └── runtime-core
```

```
.
└── example
    └── helloworld
        ├── App.js
        ├── index.html
        └── main.js
```

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="app"></div>
    <script src="./main.js" type="module"></script>
</body>

</html>
```

```js
// main.js
import { App } from "./App";

createApp(App).mount("#app");
```

```js
export const App = {
  render() {
    return h("div", "hi, " + this.msg);
  },
  setup() {
    return {
      msg: "mini-vue",
    };
  },
};
```

[[createApp]]