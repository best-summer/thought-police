# ゲーム機能application

## マッチング管理

### マッチング開始
#### 通信方向
Unity->Node

#### Request
```js
{
  "type":"start_match",
  "device_id":"",
  "user_name":""
}
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
  "room_id":"",
  "enemy":{
    "device_id":"",
    "user_name":"",
    "remain_natsuyasumi":"",
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
  "type":"faild_match",
  "error_code":001,
  "message":""
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
  "room_id":""
}
```

### ゲーム終了
#### 通信方向
Node->Unity

#### Request
```js
{
  "type":"game_finish",
  "room_id":""
}
```

## ゲームプレイ

### 水をかける動作をする
#### 通信方向
Unity->Node->Unity

#### Request
```js
{
  "type":"splash_water",
  "device_id":"",
  "room_id":"",
}
```

### 水を相手に当てた
#### 通信方向
Unity->Node->Unity

#### Request
```js
{
  "type":"hit_water",
  "device_id":"",
  "room_id":"",
  "score": ""
}
```

### 自機移動
Unity->Node->Unity

#### Request
```js
{
  "type":"move",
  "device_id":"",
  "room_id":"",
  "position": {
    "x": "",
    "y": ""
  },
  "angle": {
    "r": ""
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
