## Setting Up React With Typescript From Scratch

1. Create project folder `mkdir <project-name> && cd <project-name>`.
2. Initial npm project, `npm init` and follow the prompts.
3. Install dev dependencies

```bash
npm install --save-dev \
  @babel/core \
  @babel/preset-env \
  @babel/preset-react \
  @babel/preset-typescript \
  @types/node \
  @types/react \
  @types/react-dom \
  babel-loader \
  css-loader \
  html-webpack-plugin \
  react \
  react-dom \
  style-loader \
  ts-loader \
  typescript \
  webpack \
  webpack-cli \
  webpack-dev-server
```

4. Update scripts block in your `package.json` file.
   
```json
"scripts": {
  "start": "webpack serve --hot --open",
  "build": "webpack --mode production"
},
```

5. Create `webpack.config.js` with `touch webpack.config.js`.

```javascript
module.exports = {
  const path = require('path');
  const HTMLWebpackPlugin = require('html-webpack-plugin');

  module.exports = {
    entry: './src/index.tsx',
    output: {
      path: path.join(__dirname, '/dist'),
      filename: 'index.bundle.js'
    },
    mode: process.env.NODE_ENV || "development",
    resolve: {
      extensions: [ '.tsx', '.ts', '.js' ],
    },
    devServer: {
      port: 8080
    },
    plugins: [
      new HTMLWebpackPlugin({
        template: path.join(__dirname, 'src', 'index.html')
      })
    ],
    module: {
      rules: [
        {
          test: /\.(js|jsx)$/,
          exclude: /node_modules/,
          use: ["babel-loader"],
        },
        {
          test: /\.(ts|tsx)$/,
          exclude: /node_modules/,
          use: ["ts-loader"],
        },
        {
          test: /\.(css|scss)$/,
          use: ["style-loader", "css-loader"],
        },
        {
          test: /\.(jpg|jpeg|png|gif|mp3|svg)$/,
          use: ["file-loader"],
        },
      ]
    },
  }
}

```
6. Create your `.babelrc` file

```
{
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react", 
    "@babel/preset-typescript" 
  ],
  "plugins": [
    "@babel/plugin-proposal-class-properties"
  ]
}
```
7. Create your `tsconfig.json` file.
```
{
  "compilerOptions": {
    "target": "es5",
    "lib": [
      "dom",
      "dom.iterable",
      "esnext"
    ],
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "noFallthroughCasesInSwitch": true,
    "module": "esnext",
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": false,
    "jsx": "react-jsx"
  },
  "include": [
    "src"
  ]
}
```
8. Create `src` directory for your source code, `mkdir src`
9. Create your `index.html`, `index.tsx`, and `App.tsx` files, `touch src/index.html src/index.ts src/App.tsx`.

**src/index.html**
```html
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE-edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>React Without Create React App</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```

**src/index.tsx**
```typescript
import React from "react";
import ReactDOM from "react-dom";
//Import App
import App from "./App";

ReactDOM.render(<App />, document.querySelector("#root"));
```

**src/App.tsx**
```typescript
import React from 'react';

interface Props {

}

const App: React.FC<Props> = () => {
  return (
    <>
      <h1>Hello World</h1>
      <p>React Without create-react-app</p>
    </>
  );
};

export default App;
```

10. Start development server with `npm start`
