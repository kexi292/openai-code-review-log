经过对代码变更记录的分析，以下是主要的改动点以及相应的代码设计思路和编程技巧：

1. **依赖引入**：在`pom.xml`文件中新增了`oapi-java-sdk`依赖，用于支持ChatGLM服务。

2. **配置类新增**：在`ChatGPT-data-app`模块下，新增了`ChatGLMSDKConfig`和`ChatGLMSDKConfigProperties`类，用于配置和获取ChatGLM服务的API密钥。

3. **配置文件修改**：在`application-dev.yml`文件中新增了ChatGLM服务的API密钥配置。

4. **测试类修改**：在`ChatServiceTest`类中新增了测试ChatGLM服务的测试方法。

5. **领域模型修改**：在`ChatProcessAggregate`类中新增了获取渠道的方法。

6. **服务类修改**：在`AbstractChatService`类中，将消息处理逻辑抽象为接口`OpenAiGroupService`，并新增了`ChatGLMService`和`ChatGPTService`两个实现类。同时，将渠道判断逻辑从服务类中提取到枚举`OpenAiChannel`中。

7. **新增枚举**：在`OpenAiChannel`枚举中，定义了ChatGPT和ChatGLM两个渠道，并提供了根据模型名称获取渠道的方法。

以上改动采用了以下编程技巧：

- **依赖管理**：通过`pom.xml`管理第三方库依赖。
- **配置分离**：通过Spring Boot的`@ConfigurationProperties`注解实现配置与代码的分离。
- **接口抽象**：通过抽象接口`OpenAiGroupService`将不同渠道的处理逻辑分离。
- **枚举使用**：通过枚举`OpenAiChannel`简化了渠道的判断逻辑。
- **单一职责**：每个服务类只负责一个渠道的处理，实现了单一职责原则。

这些改动提高了代码的扩展性和可维护性。通过这些设计思路和技巧，可以有效地帮助实习生理解目前的代码。