本次代码更改涉及以下几个方面：

1. **依赖项更新**：在`package.json`中新增了`@hello-pangea/dnd`依赖项，这是一个用于React拖拽的库。在`package-lock.json`中新增了该依赖项的详细信息。

2. **组件重命名**：将`DialogItem`组件重命名为`DialogListItem`，以与列表项的功能更加匹配。同时，更新了对应的`scss`文件和组件文件名称。

3. **新增组件**：
    - `DialogMessageInput`：用于对话消息输入的组件。
    - `DialogMessageItem`：用于展示单个消息的组件。
    - `DialogMessage`：用于展示整个对话消息的组件。

4. **路由调整**：
    - 在`Chat`页面中使用了`Outlet`组件，用于嵌套路由。
    - 在`Home`页面的路由配置中，为`Chat`页面添加了嵌套路由，通过`:id`参数匹配不同的对话消息页面。

5. **类型定义**：在`chat.ts`类型文件中，新增了消息相关的类型定义，包括消息类型`MessageType`和消息方向`MessageDirection`。

6. **图片资源**：新增了`runny-nose.png`图片资源。

这些更改主要是为了新增对话消息的展示功能，并调整了部分组件的名称和结构。其中，路由的调整使得可以通过不同的URL访问不同的对话消息页面。类型定义的更新为后续开发提供了便利。整体上，这些更改使得应用的功能更加完善。