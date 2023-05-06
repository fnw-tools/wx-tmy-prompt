# wx-tmy-prompt
Room and prompt definition for chatGPT in WeChat.

[跳至 GitHub Pages 静态托管主页安装聊天室](https://www.fn-share.com/github_bridge?path=index.html)

&nbsp;

### 关于本项目

本项目定义 2 间 chatGPT 聊天室，这些聊天室适合在微信公众号 "填密语" 中使用。

其中 "旅游服务" 聊天室定义如下：

<pre><code class="tmy-room">
{
  "room_ver": 1,
  "room_name": "旅游服务",
  "room_desc": "本聊天室提供旅行服务，可以让机器人介绍景点、介绍当地特产、翻译外文等。",
  
  "system_role": "你是一个友善的导游",
  "context_size": 1,
  "temperature": 0.7,
  "max_tokens": 600,
  
  "globals": {"where":"北京故宫"},
  "magic_rules": {
    "介绍":[["景点名","set","{where}"], "*"],
    "特产":["*"],
    "翻译":["*"]
  },
  "prompts": {
    "介绍":{ "ask":"我提供一个景点名称，你将介绍该景点的特色、人文背景、历史典故，简短些。请介绍景点：{where} 。", "context_size":3, "temperature":0 },
    "特产":{ "ask":"请问 {where} 景点有什么特产？", "context_size":5, "temperature":0},
    "翻译":{ "prefix": [
      {"ask":"我希望你同时扮演中文翻译、拼写纠正和改进者角色。我会以任何语言与你交谈，你会检测语言，翻译它，并用更为优美、高雅的高级中文词汇和句子来回答我的文本，保持意义相同，但使它们更具文学性，请只回复更正和改进，不要写解释。","answer":"好的"}, 
      {"ask":"istanbulu cok seviyom burada olmak cok guzel","answer":"我非常喜欢伊斯坦布尔，在这里很愉快。"}],
      "ask":"",
      "max_tokens":1000, "temperature":1.2,
      "context_size":0, "reset_context":true
    }
  },
  "hint_magics": ["介绍","特产","翻译"],
  "state_desc": "({where})"
}
</code></pre>

特别说明：以上聊天室定义不追求实用性，它用作样例，为配合 “TMY 规则引擎使用手册” 方便讲解而设置。

&nbsp;

其中 "中英互译" 聊天室定义如下：

<pre><code class="tmy-room">
{
  "room_ver": 1,
  "room_name": "中英互译",
  "room_desc": "输中文译英文，输英文译中文。",
  
  "system_role": "你是一个友善的翻译员",
  "context_size": 0,
  "temperature": 0,
  "max_tokens": 600,
  
  "check_chinese": true,
  "globals": {},
  "magic_rules": {"*":["*"]},
  "prompts": {
    "*":{
      "ask":"'请将如下文字翻译成英文：' if {IS_CN!r} else '请将如下文字翻译成中文：'",
      "context_size":0, "temperature":0, "reset_context":true, "max_tokens":1000
    }
  },
  "hint_magics": [],
  "state_desc": ""
}
</code></pre>

&nbsp;

### 您还可以 fork 本项目自定聊天室规格

在 github 网站将本项目 fork 到自己名下，通过配置 Github Pages 实现静态页托管，您将收获自主配置的聊天室定义。

您也可以在一个 repo 中定义多间聊天室，详情请参考 [TMY 规则引擎使用手册](https://fnw-tools.github.io/tmy-rule-engine/index.html) 。
