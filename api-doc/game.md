# ゲーム機能application

## マッチング管理

### マッチング開始
#### 通信方向
Unity->Node

#### Request
```js
{
  "type":"start_match",
   "device_id":"Test_IijimaYun_Id", 
   "user_name":"Test_IijimaYun" 
}
```

### マッチングキャンセル
#### 通信方向
Unity->Node

#### Request
```js
{
   "type":"cancel_match", 
   "device_id":"" 
}
```

### マッチング完了
#### 通信方向
Node->Unity

#### Request
```js
{
  "type":"complete_match",
  "room_id":"084cb070-81ca-11e7-b3a1-b5e7d451bac9",
  "enemy":{
    "device_id":"Test_IijimaYun_Id"
    "login_key":"LOGINKEY"
    "room_id":"084cb070-81ca-11e7-b3a1-b5e7d451bac9"
    "score":0
    "socket_id":"-6ZivjwH0SDg2ypnAAAB"
    "user_name":"Test_IijimaYun"
      "rank":""  
  }
}
```

### マッチング失敗
#### 通信方向
Node->Unity

#### Request
```js
{
  <!-- "type":"faild_match",
  "error_code":001,
  "message":"" -->
}
```


## ゲーム進行管理

### ゲーム開始
#### 通信方向
Node->Unity

#### Request
```js
{
  "type":"game_start",
  "room_id":"084cb070-81ca-11e7-b3a1-b5e7d451bac9"
}
```

### ゲーム終了
#### 通信方向
Unity->Node->Unity

#### Request
```js
// Unity->Node の段階
{
  "type":"game_finish",
  "device_id":"Test_SuzukazeAoba_Id"
}
```

#### Response
```js
// Node->Unity の段階（Unicast）
{
  "type":"game_finish",
  "device_id":"Test_SuzukazeAoba_Id",
  "win": true
  "enemy":{
    "device_id":"Test_IijimaYun_Id",
    "login_key":"LOGINKEY",
    "room_id":"084cb070-81ca-11e7-b3a1-b5e7d451bac9",
    "score":50,
    "socket_id":"-6ZivjwH0SDg2ypnAAAB",
    "user_name":"Test_IijimaYun"
  },
  "you":{
    "device_id":"Test_SuzukazeAoba_Id",
    "login_key":"LOGINKEY",
    "room_id":"084cb070-81ca-11e7-b3a1-b5e7d451bac9",
    "score":100,
    "socket_id":"Pmbb55kvnZb-mb1MAAAC",
    "user_name":"Test_SuzukazeAoba"
  }
}
```

## ゲームプレイ

### 水をかける動作をする
#### 通信方向
Unity->Node->Unity

#### Request
```js
// 横流しする
{
  "type":"splash_water",
  "device_id":"",
}
```

### 水を相手に当てた
#### 通信方向
Unity->Node->Unity

#### Request
```js
// Unity->Node の段階
{
  "type":"hit_water",
  "device_id":"Test_IijimaYun_Id",
  "score": 50
}
```

#### Response
```js
// Node->Unity の段階（Broadcast）
{
  "type":"hit_water",
  "device_id":"Test_IijimaYun_Id",
  "room_id":"084cb070-81ca-11e7-b3a1-b5e7d451bac9",
  "you": {
    "device_id":"Test_IijimaYun_Id",
    "score":50,
    "user_name":"Test_IijimaYun"
  },
  "enemy":{
    "device_id":"Test_SuzukazeAoba_Id",
    "score":0,
    "user_name":"Test_SuzukazeAoba"
  },
}
```

### 自機移動
Unity->Node->Unity

#### Request
```js
// 横流しする
{
  "type":"move",
  "device_id":"Test_IijimaYun_Id",
  "position": {
    "x": 3,
    "y": 7
  },
  "angle": {
    "r": 10
  }
}
```

## リザルト機能

### スコア送信

#### 通信方向
Node->Rails

#### エンドポイント
/gameresult

#### Request
```js
{
  "scores":[
    {
      "device_id":"",
      "score":""
    },
    {
      "device_id":"",
      "score":""
    }
  ]
}
```

#### Response
```js
{
  "status":"ok"
}
```
