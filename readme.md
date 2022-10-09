# vite-plugin-react-require

[![npm](https://img.shields.io/npm/v/vite-plugin-react-require.svg)](https://www.npmjs.com/package/vite-plugin-react-require)

> can let vite react projects to support `require` [vite-plugin-react-require](https://www.npmjs.com/package/vite-plugin-react-require)

Install and use to achieve painless support `require` with React App

&nbsp;

## Install

```
npm i vite-plugin-react-require | yarn add vite-plugin-react-require
```

## Usage

```ts
import vitePluginRequire from "vite-plugin-react-require";

export default {
	plugins: [
		vitePluginRequire({
			// @fileRegex RegExp
			// optional：default file processing rules are as follows
			// fileRegex:/(.jsx?|.tsx?)$/
		}),
	],
};
```

## Where is the root directory？

The entire project directory is the root directory。
It doesn't matter how you quote it.

## Demo

Suppose there are app.jsx and imgs folders in the src directory

```jsx
function App() {
    // The variable must be placed on the top   变量必须放置到最上面
    // Do not use string templates  不可以使用字符串模板

    const img2 = "./img/1.png";
    const img3_1 = "./img/";
    const img3_2 = "./1/";

    return (
        <div>
            <!-- Will actually convert to: "src/imgs/logo.png" -->
            <img src={require("./imgs/logo.png")} alt="logo1" />
            <!-- You can use variables --> 
            <img src={require(img2)} alt="logo1" />
            <!-- You can use String splicing -->
            <img src={require(img3_1 + img3_2 + ".png")} alt="logo1" /> 
        </div>
    );
}
export default App;
```

Other deeper subdirectories

file path: `src/views/Page1/index.jsx`

```jsx
function Page() {
    return (
        <div>
            <!-- Will actually convert to: "src/imgs/logo.png" -->
            <img src={require("../../../imgs/logo.png")} alt="logo1" />
            
            <!-- Will actually convert to: "/src/views/Page1/imgs/logo.png" -->
			<img src={require("./imgs/logo.png")} alt="logo1" /> 
        </div>
    );
}
export default Page;
```
