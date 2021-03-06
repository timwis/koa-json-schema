# koa-json-schema

[![CircleCI](https://circleci.com/gh/zorro-del-caribe/koa-json-schema.svg?style=svg)](https://circleci.com/gh/zorro-del-caribe/koa-json-schema)

[json schema](http://json-schema.org/) validation middleware for [koajs](http://koajs.com/) using [AJV](https://github.com/epoberezkin/ajv).

## install

`` npm install --save koa-json-schema``

## usage

validate input as

```Javascript

const input = Object.assign({},this.request.query, this.request.body,this.params);

```

```Javascript

const koa=require('koa')
const validator = require('koa-json-schema')

koa()
    .use(validator(schema, options))
    .use(function * (){
       // do something with safe input
    });
```

* schema: a valid json schema
* options: options to pass to AJV

if the input is not valid 422 error is thrown. the validation errors can be found as error.error_description

```Javascript

koa()
    .use(function * (next){
        try {
            yield *next;
        } catch(e){
           if(e.status === 422){
                console.log(e.error_description);
           }
        }
    })
    .use(validator(schema, options))
    .use(function * (){
       // do something with safe input
    });

```
