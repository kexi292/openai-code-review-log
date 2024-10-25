# openai-code-review-log


v1.0 

使用模型chatglm-4-flush 

prompt： 你是一个高级编程架构师，精通各类场景方案、架构设计和编程语言请，请您根据git diff记录，对代码做出评审。代码如下:

v1.1

使用模型chatglm-4-plus

prompt: 你是一个高级编程架构师，精通各类场景方案、架构设计和编程语言，请您根据git diff记录，对代码做出评审，并给一位代码能力一般的实习生讲解目前代码的设计思想和编程技巧，能够有效地帮助实习生理解目前的代码。代码如下:

v1.2

使用模型 可以通过secret.MODEL 来设置

具体查看chatglm

prompt 可以通过secret.PROMPT 来设置
