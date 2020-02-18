---
layout: post
comments: true
date: 2020-02-18 10:56:18
title: "Node.js 에서 Sequelize 설치 및 간단한 사용 방법"
description: "Sequelize 설치 및 간단한 사용 방법"
subject: blog
categories: [ nodejs ]
tags: [ nodejs, mysql, sequelize ]
---

# Sequelize 설치

mysql 과 sequelize 를 설치해요.

```bash
npm install --save sequelize
npm install --save mysql2
```

sequelize-cli 를 설치하면 기본 설정들을 손쉽게 할 수 있어요.

저는 설치 없이 진행 할게요.

```bash
npm install -g sequelize-cli
```

## sequelize-cli 맛보기

기본 설정 파일을 config 폴더로 다운 받아요.

```bash
sequelize init:config --config config/sequelize.json
```

아래와 같이 세팅할 수 있는 파일이 생겨요.

```json
{
    "development": {
        "username": "root",
        "password": null,
        "database": "database_development",
        "host": "127.0.0.1",
        "dialect": "mysql",
        "operatorsAliases": false
    },
    "test": {
        "username": "root",
        "password": null,
        "database": "database_test",
        "host": "127.0.0.1",
        "dialect": "mysql",
        "operatorsAliases": false
    },
    "production": {
        "username": "root",
        "password": null,
        "database": "database_production",
        "host": "127.0.0.1",
        "dialect": "mysql",
        "operatorsAliases": false
    }
}
```

이번엔 기본 `models` 폴더를 세팅 해 볼게요.

```bash
sequelize init:models
```

사용하는 방법에 대한 코드가 나와 있어서 참고하면 좋을 것 같아요.

```javascript
'use strict';

const fs = require('fs');
const path = require('path');
const Sequelize = require('sequelize');
const basename = path.basename(__filename);
const env = process.env.NODE_ENV || 'development';
const config = require(__dirname + '/../config/config.json')[env];
const db = {};

let sequelize;
if (config.use_env_variable) {
    sequelize = new Sequelize(process.env[config.use_env_variable], config);
} else {
    sequelize = new Sequelize(config.database, config.username, config.password, config);
}

fs
.readdirSync(__dirname)
.filter(file => {
    return (file.indexOf('.') !== 0) && (file !== basename) && (file.slice(-3) === '.js');
})
.forEach(file => {
    const model = sequelize['import'](path.join(__dirname, file));
    db[model.name] = model;
});

Object.keys(db).forEach(modelName => {
    if (db[modelName].associate) {
        db[modelName].associate(db);
    }
});

db.sequelize = sequelize;
db.Sequelize = Sequelize;

module.exports = db;
```

# Sequelize 사용법

SQL 문과 함께 보면 이해가 더 쉽겠죠?

## INSERT INTO

```sql
insert into user ( uuid, content ) values ( 1, "TEXT" );
```

```javascript
// mysql pool 사용
pool.query( "insert into user ( uuid, content ) values ( ?, ? )", [ 1, "TEXT" ], (err, rows)=>{
    if ( err ) {
        console.error( err );
        return;
    }

    if (rows.length > 0) {
        // 
    } else {
        // 
    }
});
```

```javascript
const addData = await models.user.create({
    uuid: 1,
    content: "TEXT"
});
```

Sequelize 에서 다중 INSERT 문은 `bulkCreate` 를 사용해요.

```sql
insert into user values ( 1, "TEXT1" ), ( 2, "TEXT2" ), ( 3, "TEXT3" );
```

```javascript
const addData = await models.user.bulkCreate([{
    uuid: 1,
    content: "TEXT1"
}, {
    uuid: 2,
    content: "TEXT2"
}, {
    uuid: 3,
    content: "TEXT3"
}]);
```

정해진 fields 에만 들어가게 할 때는 fields 를 명시해줘요.

```sql
insert into user ( uuid, content ) values ( 1, "TEXT1" ), ( 2, "TEXT2" ), ( 3, "TEXT3" );
```

```javascript
const addData = await models.user.bulkCreate([{
    uuid: 1,
    content: "TEXT1"
}, {
    uuid: 2,
    content: "TEXT2"
}, {
    uuid: 3,
    content: "TEXT3"
}], {
    fields: [ uuid, content ]
});
```

## SELECT FROM

전체 데이터 가져오기

```sql
select * from user;
```

```javascript
// user 데이터 모두 가져오기
const userData = await models.user.findAll({});

// userData.length 로 비어있는지 체크한다.
if ( userData.length > 0 ) {} else {}
```

필요한 데이터 1개만 가져오기

```sql
select * from user where uuid = 1;
```

```javascript
// uuid 가 1 인 user 의 데이터 가져오기
const userData = await models.user.findOne({
    where: {
        uuid: 1
    }
});

// userData 로 체크한다.
if ( userData ) {} else {}
```

## UPDATE SET

```sql
update user set content = "WELCOME" where uuid = 1;
```

```javascript
// uuid 가 1 인 user 의 content 데이터 수정
await models.user.update({
    content: "WELCOME"
}, {
    where: {
        uuid: 1
    }
});
```

## DELETE FROM

```sql
delete from user where uuid = 1;
```

```javascript
// uuid 가 1 인 user 의 데이터 삭제
await models.user.destroy({
    where: {
        uuid: 1
    }
});
```

# Sequelize 응용

## WHERE

- 공식 문서: <https://sequelize.org/master/manual/model-querying-basics.html>

### WHERE AND

```sql
select * from user where uuid = 1 and phone = "01012345678";
```

```javascript
const userData = await models.user.findOne({
    where: {
        uuid: 1,
        phone: "01012345678"
    }
});
```

```javascript
const userData = await models.user.findOne({
    where: {
        [ Op.and ]: [{
            uuid: 1
        }, {
            phone: "01012345678"
        }]
    }
});
```

### WHERE AND | NOT

```sql
select * from user where uuid = 1 and phone = "01012345678" and type != "new";
```

```javascript
const userData = await models.user.findOne({
    where: {
        uuid: 1,
        phone: "01012345678",
        type: {
            [ Op.ne ]: "new"
        }
    }
});
```

### WHERE OR

2가지 방법 모두 가능해요.

```sql
select * from user where uuid = 1 or uuid = 2;
```

```javascript
const userData = await models.user.findOne({
    where: {
        uuid: {
            [ Op.or ]: [ 1, 2 ]
        }
    }
});
```

```javascript
const userData = await models.user.findOne({
    where: {
        [ Op.or ]: [{
            uuid: 1
        }, {
            uuid: 2
        }]
    }
});
```

## ATTRIBUTE

```sql
select uuid from user;
```

```javascript
const userData = await models.user.findAll({
    attributes: [ "uuid" ]
});
```

## ORDER

```sql
select * from user order by uuid desc;
```

```javascript
const userData = await models.user.findAll({
    order: [ "uuid", "DESC" ]
});
```

## LIMIT

```sql
select * from user limit 5;
```

```javascript
const userData = await models.user.findAll({
    limit: 5
});
```

## ORDER

```sql
select * from user order by uuid desc;
```

```javascript
const userData = await models.user.findAll({
    order: [ "uuid", "DESC" ]
});
```