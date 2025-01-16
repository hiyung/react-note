# Component Auto Import Setting

> 컴포넌트를 직접 import 하지 않고 자동으로 import 인식하는 방법...

## Install
```
yarn add -D vite-plugin-components
```

## Setting
```javascript
//vite.config.js
import ViteComponents from 'vite-plugin-components';

export default defineConfig({
  plugins [
    //추가 코드
    ViteComponents({
      dirs: ['src/components],
      extensions: ['jsx'],
      deep: true,
    }),
  ],
});
```

## EsLint Setting
```javascript
//eslint.config.js
{
  "rules": {
    //추가 코드
    "import/no-unresolved": "off",
    "react/jsx-uses-vars": "off"
  }
}
```
