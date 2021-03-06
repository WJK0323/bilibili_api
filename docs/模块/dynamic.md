# dynamic 模块

获取动态信息，发送动态，操作动态等。

## 通用名词解释

dynamic_id: 动态ID，标识动态的唯一数字ID。https://t.bilibili.com/ 后面接的一串很长的数字就是。

**如无特殊说明，获取动态信息，操作动态均需要提供dynamic_id，发送动态不用**

## 方法

### send_dynamic

智能判断动态类型发送动态。

| 参数名      | 类型              | 必须提供 | 默认  | 释义                      |
| ----------- | ----------------- | -------- | ----- | ------------------------- |
| text        | str               | True     | False | 动态文字内容              |
| images_path | list              | False    | None  | 动态图片路径列表，最多9张 |
| send_time   | datetime.datetime | False    | None  | 动态发送时间              |

如何智能判断？如果你只提供 text ，则立即发送纯文本动态，如果还提供了send_time，则发送定时动态，如果提供 images_path，图片会自动上传并发送。b站的动态API很麻烦，但是我这里已经封装好了直接调用就行了。

**注意**，如果需要@人，请在文本中用以下格式“@UID ”，注意最后有个空格，不管是在文中还是文末都请加上，否则无法识别。

### get_schedules_list

获取待发定时动态列表。需要登录。

### send_schedule_now

立即发送定时动态。

| 参数名   | 类型 | 必须提供 | 默认 | 释义           |
| -------- | ---- | -------- | ---- | -------------- |
| draft_id | int  | True     | -    | 定时动态草稿ID |

选择发送定时动态后，定时动态会有个草稿ID：draft_id，可以用上一个方法来获取到。

### delete_schedule

删除定时动态。

| 参数名   | 类型 | 必须提供 | 默认 | 释义           |
| -------- | ---- | -------- | ---- | -------------- |
| draft_id | int  | True     | -    | 定时动态草稿ID |

本来还有个修改定时动态内容的API，但是因为是程序操作，直接删除后再发一个新的是一样的。

### get_info

获取动态信息。

### get_reposts_raw

低层级API获取转发信息。

| 参数名 | 类型 | 必须提供 | 默认 | 释义                     |
| ------ | ---- | -------- | ---- | ------------------------ |
| offset | str  | False    | 0    | 下一条转发信息dynamic_id |

### get_reposts

自动循环获取转发信息

参照：[循环获取数据参数说明][循环获取数据参数说明]

**注意**，由于b站限制，最多只能获取560条左右，如果你用这个方法来抽奖，动态转发数量超过了限制，那么请考虑抽奖公平性。

### set_like

设置动态点赞状态。

| 参数名 | 类型 | 必须提供 | 默认 | 释义 |
| ------ | ---- | -------- | ---- | ---- |
| status | bool | False    | True | 状态 |

### delete

删除动态。

### repost

转发动态

| 参数名 | 类型 | 必须提供 | 默认     | 释义     |
| ------ | ---- | -------- | -------- | -------- |
| text   | str  | False    | 转发动态 | 动态内容 |

### 评论相关

参见 [评论信息和操作](/bilibili_api/docs/通用解释#评论信息和操作)，id传入dynamic_id。







[循环获取数据参数说明]: /bilibili_api/docs/通用解释#循环获取数据参数说明