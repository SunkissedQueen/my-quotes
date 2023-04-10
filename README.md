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
```dev
```