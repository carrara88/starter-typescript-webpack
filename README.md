# TypeScript and Webpack

## Step 1: Setting Up the Development Environment

First, we'll create a new project folder and initialize it with npm, Node.js's package manager. This step sets up the groundwork for managing our project's dependencies.

```bash
mkdir <my-project-name>
cd <my-project-name>
```

## Step 2: Installing Dependencies

Next, we install TypeScript, Webpack, and other necessary development tools. TypeScript is a superset of JavaScript that allows for static typing, while Webpack is a powerful module bundler that helps in bundling your assets, scripts, images, and styles.

```bash
npm init -y
npm install typescript webpack webpack-cli ts-loader html-webpack-plugin webpack-dev-server
 copy-webpack-plugin --save-dev
```

## Step 3: Configuring TypeScript and Webpack

After installing the necessary tools, we'll set up TypeScript and Webpack. This involves creating configuration files that define how our TypeScript code is compiled and how our project is bundled.

```bash
npx tsc --init
touch webpack.config.js
```

Edit TypeScript configuration file `tsconfig.json`

```json
{
  "compilerOptions": {
    /* Language and Environment */
    "target": "es2016", /* Set the JavaScript language version for emitted JavaScript and include compatible library declarations. */
    /* Modules */
    "module": "commonjs", /* Specify what module code is generated. */
    "esModuleInterop": true, /* Emit additional JavaScript to ease support for importing CommonJS modules. This enables 'allowSyntheticDefaultImports' for type compatibility. */
    "forceConsistentCasingInFileNames": true, /* Ensure that casing is correct in imports. */
    /* Type Checking */
    "strict": true, /* Enable all strict type-checking options. */
    /* Completeness */
    "skipLibCheck": true /* Skip type checking all .d.ts files. */
  }
}
```

Create `webpack.config.js`

```bash
touch webpack.config.js
```

Now, edit `webpack.config.js` in the root of your project and input the following configuration:

```javascript
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const CopyWebpackPlugin = require('copy-webpack-plugin');

module.exports = {
  entry: './src/index.ts',
  mode: 'development', // 'production'
  module: {
    rules: [
      {
        test: /\.tsx?$/,
        use: 'ts-loader',
        exclude: /node_modules/,
      },
      {
        test: /\.css$/i,
        use: ['style-loader', 'css-loader'],
      },
    ],
  },
  resolve: {
    extensions: ['.tsx', '.ts', '.js'],
  },
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist'),
  },
  devServer: {
    static: {
      directory: path.join(__dirname, 'dist'),
    },
    compress: true,
    port: 9001,
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: 'index.html',
    }),
    new CopyWebpackPlugin({
        patterns: [
            { from: 'assets', to: 'assets', force: true },
        ],
      })
  ],
};

```

## Step 4: Organizing the Project Structure

Organizing your project's directory structure is crucial for maintainability and scalability. We'll set up a basic structure with a source directory for our TypeScript code, a distribution directory for the bundled output, and an HTML file to serve our project.

```bash
mkdir src
mkdir assets
touch src/index.ts assets/styles.css index.html
```

Edit `index.html` and `assets/styles.css` as follows:

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title><my-project-name></title>
    <link rel="stylesheet" href="assets/style.css">
</head>
<body>

</body>
</html>
```

```css
/* assets/styles.css */
body { 
    font: 11px helvetica neue, helvetica, arial, sans-serif;
}
```

Edit `src/index.ts` as follow:

```typescript
/* src/index.ts */
document.addEventListener('DOMContentLoaded', function () {
  document.body.innerHTML = "<my-project-name> project is compiled";
});
```


## Step 5: Configuring Scripts in `package.json`

To streamline our development workflow, we'll add custom scripts to our `package.json`. These scripts will allow us to start a development server, compile our project in development mode, and build our project for production with simple commands.

```json
{
  "name": "<my-project-name>",
  "version": "0.0.1",
  "description": "<my-project-name> project",
  "main": "dist/bundle.js",
  "scripts": {
    "dev": "webpack serve --mode=development --open",
    "start": "webpack serve --mode=production --open",
    "build": "webpack --mode=production"
  },
  "keywords": [
    "starter",
    "typescript",
    "webpack"
  ],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "copy-webpack-plugin": "^12.0.2",
    "html-webpack-plugin": "^5.6.0",
    "ts-loader": "^9.5.1",
    "typescript": "^5.3.3",
    "webpack": "^5.90.3",
    "webpack-cli": "^5.1.4",
    "webpack-dev-server": "^5.0.2"
  }
}

```

## Step 6: Running the Project

Finally, we'll test our setup by running our project.
This includes starting the development server to preview our project in real-time, compiling our project in development mode to test changes, and building our project for production deployment.

```bash
npm run start       # Start the development server
npm run dev         # Compile in development mode
npm run build       # Build for production
```

