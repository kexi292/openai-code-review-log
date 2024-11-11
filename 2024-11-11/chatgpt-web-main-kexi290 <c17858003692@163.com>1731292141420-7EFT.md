这段代码主要包括以下几个方面的更新：

1. 新增了`.gitignore`文件，用于指定哪些文件或文件夹需要被Git忽略。

2. 新增了`.idea`文件夹下的`ChatGPT-web.iml`文件，该文件是IDEA项目的配置文件，用于配置项目模块信息。

3. 修改了`src/apis/index.tsx`文件，主要更新了API接口的请求地址，并新增了获取请求头的方法`getHeaders`，用于从状态管理中获取token并设置到请求头中。

4. 新增了`src/app/icons/weixin.jpg`文件，这是微信的图标图片。

5. 新增了`src/app/pages/auth`目录及相关的`auth.tsx`和`auth.module.scss`文件，用于实现登录认证页面。

6. 修改了`src/app/pages/home/home.tsx`文件，增加了根据用户是否已登录来决定显示登录页面还是主界面的逻辑。

7. 新增了`src/app/store/access.ts`文件，用于实现访问控制的状态管理，包括token、验证码等。

8. 修改了`src/app/store/chat-store.ts`文件，主要是增加了一些权限校验的逻辑，如当接口返回特定错误码时跳转到登录页面。

这些更新主要是新增了登录认证相关的页面和逻辑，以及修改了部分API接口的请求地址和请求头设置。