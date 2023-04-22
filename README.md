### 关于 wx-tmy-prompt

本项目由微信公众号 “填密语” 官方提供，主要用来定义填密语公众号对接 chatGPT 聊天室的 prompt 规格。

填密语公众号是一个多聊天室机器人问答系统，公众号里设置多个房间（room），不同房间提供不同主题的问答服务。本项目定义聊天室 room 的规格，一个 room 中可定义多个触发词 magics，每个触发词都对应一项动作，动作包含用于 chatGPT 聊天的 prompt 定义。

&nbsp;

### 快速入门

第一步：关注微信公众号 “填密语”，可以在微信中搜索找到。关注成功后，系统会自动为您创建两个房间：“GPT” 与 “翻译”，在公众号中点 “主页” 及 “配置” 按钮系统将跳到相关页指导初学者如何使用本工具。

第二步：进入本公众号的 “GPT” 房间，将如下二维码拍照（如果当前您正用手机访问本网页，将下面二维码截屏），然后把照片或截屏图片在公众号中发送。公众号随即自动导入一个 room 定义。

（图片）

第三步，在公众号中输入 "？"，您将发现 “可换房间” 列表多了一项 “工具房” ，切换到工具房后，输入 "天气"，chatGPT 将反馈当前您指定城市的天气信息。

上面扫二维码实质是将本项目的 "sample_prompt_v1.json" 文件地址告诉公众号，这个 json 文件正是工具房的 room 定义。

&nbsp;

### 自定义聊天室

下文介绍如何自定义一间可在填密语公众号中使用的聊天室，拿上面介绍的工具房举例。

先讲最简情形，比方，如何查询深圳当前天气，定义 room 如下：

``` json
{
  "room_ver": 1,
  "room_desc": "工具房",
  
  "magic_rules": {
    "天气":["*"]
  },
  "prompts": {
    "天气":{"ask":"帮我查一下当前 深圳 天气。"}
  },
  "magics": ["天气"]
}
```

这里，room_ver 是填密语公众号要求的 room 规格版本号，当前固定填 1，以后若有更高版本规格推出，可以改填 "2, 3" 等，所有官方发布的历代 room_ver 版本号，在本公众号都会一直兼容下去。

room_desc 是聊天室名称，输入类似 "换房间 工具房" 指令时，room_desc 会用到。

magic_rules 定义聊天指令触发词，与机器人正常聊天时不会孤立的输入触发词，触发词就像一句魔咒，你喊一声，咒语匹配后，机器人就会执行你指定的命令。上面例子中，我们定义了一个触发词 "天气"，触发后，系统就会执行在 prompt 预定义的一句问话，如 "帮我查一下当前 深圳 天气。"。

在 magic_rules 中定义触发词都有捕获触发能力，但并不是所有触发词都在用户输入 "?" 后打印帮助信息中显示，只有在 magics 列表项中指定触发词才打印。所以，在 room 定义中，magic_rules 项目个数可能多于在 magics 中指定的，这意味着，提供 room 定义的作者，可以有意隐藏某些触发词的，隐藏的触发词就真成咒语了，修成大法才念得出来。

上面 magic_rules 定义 "天气" 时列出 "*"，表明对应 prompt 问话触发时，将在问话尾部附加一些描述。比如，用户输入："天气  今起三天"，GPT 将反馈未来三天的天气预报。

&nbsp;

### 给 room 增加变量定义

&nbsp;
