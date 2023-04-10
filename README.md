## References
- https://hibbard.eu/rails-react-crud-app/


## Create a rails app with esbuild
- $ rails new charlean-ism -j esbuild -d postgresql -T
- $ cd charlean-ism
- $ gst
- $ ga .
- $ gcmsg "created rails app with javascript esbuild"
- $ git branch -M main
- $ git remote add origin https://github.com/SunkissedQueen/my-quotes.git
- $ git push -u origin main
- $ rails db:create
- $ bin/dev

## Add react to the rails app
- $ gst
- $ gco -b react
- $ yarn add react react-dom
- $ code .
- Modify package.json
  - Add loader:.js=jsx to tell esbuild to allow JSX syntax in .js files.
  - Add another script to watch the app/javascript directory for changes and to rebundle everything when any are detected.
```json
  "scripts": {
    "build": "esbuild app/javascript/*.* --bundle --sourcemap --outdir=app/assets/builds --public-path=assets --loader:.js=jsx",
    "watch": "esbuild app/javascript/*.* --watch --bundle --outdir=app/assets/builds --public-path=assets --loader:.js=jsx"
  }
```
- Modify Procfile.dev
`web: bin/rails server -p 3000`

## Add react components
branch: components
The React app will be served from app/views/home/index.html.erb
- $ rails generate controller Home index
```html
  <div id="root"></div>
```
Create app/javascript/components/App.js  
In app/javascript/application.js, import a App component and render it in the div element from the home views 
```js
  import React from 'react';
  import { createRoot } from 'react-dom/client';
  import App from './components/App';

  const container = document.getElementById('root');
  const root = createRoot(container);

  document.addEventListener('DOMContentLoaded', () => {
    root.render(<App name="World" />);
  })
```
Create a functional component in App.js
```js
  import React from "react"

  const App = ({name}) => {
    return (
      <>
        <h1>Hello, {name}!</h1>
      </>
    )
  }

  export default App
```  
Add root route to config/routes.rb
`root to: 'home#index'`
Should see "Hello, World!" on http://localhost:3000/
