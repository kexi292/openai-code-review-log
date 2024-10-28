### 代码评审与讲解

#### 1. `pom.xml` 文件变更
**变更内容：**
```xml
+        <dependency>
+            <groupId>com.alibaba</groupId>
+            <artifactId>fastjson</artifactId>
+            <version>2.0.28</version>
+        </dependency>
```
**讲解：**
- **依赖添加**：新增了 `fastjson` 依赖，这是一个阿里巴巴提供的 JSON 处理库，用于简化 JSON 的序列化和反序列化操作。
- **用途**：在后续代码中可以看到，`fastjson` 被用于解析和处理 JSON 数据，提高了代码的简洁性和效率。

#### 2. `OpenAiSession.java` 接口变更
**变更内容：**
```java
+    CompletableFuture<String> chatCompletions(ChatCompletionRequest chatCompletionRequest) throws InterruptedException, JsonProcessingException;
```
**讲解：**
- **新增方法**：增加了一个返回 `CompletableFuture<String>` 的 `chatCompletions` 方法，用于异步处理聊天请求。
- **异步编程**：使用 `CompletableFuture` 可以让调用者异步获取结果，提高系统的响应性和吞吐量。
- **异常处理**：方法声明抛出 `InterruptedException` 和 `JsonProcessingException`，分别用于处理中断异常和 JSON 处理异常。

#### 3. `DefaultOpenAiSession.java` 类变更
**变更内容：**
```java
+    @Override
+    public CompletableFuture<String> chatCompletions(ChatCompletionRequest chatCompletionRequest) throws InterruptedException, JsonProcessingException {
+        // 用于执行异步任务并获取结果
+        CompletableFuture<String> future = new CompletableFuture<>();
+        StringBuilder dataBuffer = new StringBuilder();
+
+        chatCompletions(chatCompletionRequest,new EventSourceListener() {
+            @Override
+            public void onEvent(EventSource eventSource,String id,String type,String data) {
+                if ("[DONE]".equalsIgnoreCase(data)) {
+                    onClosed(eventSource);
+                    future.complete(dataBuffer.toString());
+                }
+
+                ChatCompletionResponse chatCompletionResponse = JSON.parseObject(data, ChatCompletionResponse.class);
+                List<ChatChoice> choices = chatCompletionResponse.getChoices();
+                for(ChatChoice chatChoice : choices) {
+                    Message delta = chatChoice.getDelta();
+                    if (Constants.Role.ASSISTANT.getCode().equals(delta.getRole())) continue;
+
+                    String finishReason = chatChoice.getFinishReason();
+                    if ("stop".equalsIgnoreCase(finishReason)) {
+                        onClosed(eventSource);
+                        return;
+                    }
+
+                    dataBuffer.append(delta.getContent());
+                }
+            }
+
+            @Override
+            public void onClosed(EventSource eventSource) {
+                future.complete(dataBuffer.toString());
+            }
+
+            @Override
+            public void onFailure(EventSource eventSource,Throwable t,Response response) {
+                future.completeExceptionally(new RuntimeException("Request closed before completion"));
+            }
+        });
+
+        return future;
+    }
```
**讲解：**
- **异步处理**：方法内部创建了一个 `CompletableFuture` 对象 `future`，用于存储异步结果。
- **事件监听**：通过 `EventSourceListener` 监听 SSE（Server-Sent Events）事件，处理流式响应。
- **JSON 解析**：使用 `fastjson` 解析响应数据，提取 `ChatCompletionResponse` 对象。
- **数据拼接**：将每次事件中的有效数据拼接到 `dataBuffer` 中，最终在事件完成时返回完整结果。
- **异常处理**：在 `onFailure` 方法中处理异常，确保异步任务能够正确反馈错误。

#### 4. `ApiTest.java` 测试类变更
**变更内容：**
```java
+    @Test
+    public void test_chat_completions_future() throws JsonProcessingException, InterruptedException, ExecutionException {
+        ChatCompletionRequest chatCompletion = ChatCompletionRequest
+                .builder()
+                .stream(true)
+                .messages(Collections.singletonList(Message.builder().role(Constants.Role.USER).content("java 冒泡排序").build()))
+                .model(ChatCompletionRequest.Model.GPT_3_5_TURBO.getCode())
+                .maxTokens(1024)
+                .build();
+
+        log.info("测试开始：请等待调用结果");
+
+        CompletableFuture<String> future = openAiSession.chatCompletions(chatCompletion);
+
+        log.info("测试结果：{}", future.get());
+    }
```
**讲解：**
- **新增测试方法**：`test_chat_completions_future` 用于测试新增的异步 `chatCompletions` 方法。
- **请求构建**：使用 `ChatCompletionRequest.Builder` 构建请求参数，设置流式响应和聊天内容。
- **异步调用**：调用 `chatCompletions` 方法并获取 `CompletableFuture` 对象。
- **结果获取**：通过 `future.get()` 阻塞等待异步结果，并打印测试结果。

### 编程技巧与设计思想
1. **异步编程**：使用 `CompletableFuture` 处理异步任务，提高系统响应性和吞吐量。
2. **事件监听**：通过 `EventSourceListener` 处理流式响应，实时处理数据。
3. **JSON 处理**：利用 `fastjson` 简化 JSON 的序列化和反序列化操作，提高代码简洁性。
4. **Builder 模式**：使用 `Builder` 模式构建复杂对象，提高代码可读性和易用性。
5. **单元测试**：通过单元测试验证功能正确性，确保代码质量。

### 对实习生的建议
- **理解异步编程**：学习 `CompletableFuture` 的使用，理解异步编程的优势和应用场景。
- **掌握 JSON 处理**：熟悉 `fastjson` 的基本用法，了解其在项目中的应用。
- **事件驱动编程**：了解 `EventSourceListener` 的工作原理，掌握事件驱动编程的基本概念。
- **编写单元测试**：学习编写单元测试，确保代码的正确性和稳定性。

通过以上讲解和技巧分享，希望你能更好地理解当前代码的设计思想和编程技巧，进一步提升自己的编码能力。如果有任何疑问，随时提问！