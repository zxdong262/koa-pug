# koa-pug-global

a fork of `koa-pug`, which add all locals props to `locals._global`

# How to use
visit https://github.com/chrisyip/koa-pug for more, it is all the same

```bash
npm install koa-pug-global --save
```

```js
const koa = require('koa')
const app = koa()

const Pug = require('koa-pug-global')
const pug = new Pug({
  viewPath: './views',
  debug: false,
  pretty: false,
  compileDebug: false,
  locals: global_locals_for_all_pages,
  basedir: 'path/for/pug/extends',
  helperPath: [
    'path/to/pug/helpers',
    { random: 'path/to/lib/random.js' },
    { _: require('lodash') }
  ],
  app: app // equals to pug.use(app) and app.use(pug.middleware)
})

pug.locals.someKey = 'some value'

app.use(async function (ctx) {
  ctx.render('index', {title: 'what'})
})
```

```pug
//index.pug
p #{title} === #{_global.title}
```


