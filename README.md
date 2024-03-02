
# Create
```
mkdir your-project-name
cd your-project-name
npm init -y
npm install typescript webpack webpack-cli ts-loader html-webpack-plugin webpack-dev-server
 copy-webpack-plugin --save-dev
npx tsc --init
touch webpack.config.js
mkdir src
touch src/index.ts src/styles.css index.html
```

# Dependencies
```
npm i --save-dev @types/cytoscape
```

# Dev - Build - Start
npm run dev         # Compile in development mode
npm run start       # Start the development server
npm run build       # Build for production