---
title: 教程 - 了解 Visual Studio 中的 Django，步骤 5
description: Visual Studio 项目上下文中 Django 基础知识的演练，具体介绍了 Django Web 项目模板提供的身份验证功能。
ms.date: 04/25/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: tutorial
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
ms.openlocfilehash: e2c5f9461eafa83551ba15c36d8ef212922a52ff
ms.sourcegitcommit: 56018fb1f52f17bf35ae2ce71c50c763486e6173
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="tutorial-step-5-authenticate-users-in-django"></a>教程步骤 5：在 Django 中对用户进行身份验证

上一步：[使用完整的 Django Web 项目模板](learn-django-in-visual-studio-step-04-full-django-project-template.md)

身份验证是 Web 应用的常见需求，因此“Django Web 项目”模板包含基本的身份验证流。 （本教程步骤 6 中讨论的“投票 Django Web 项目”模板也包括相同的流。）在使用任意 Django 项目模板时，Visual Studio 包含 Django 项目的 `settings.py` 中身份验证所需的所有模块。

在此步骤中，你将了解：

> [!div class="checklist"]
> - 如何使用 Visual Studio 模板中提供的身份验证流（步骤 5-1）

## <a name="step-5-1-use-the-authentication-flow"></a>步骤 5-1 使用身份验证流

以下步骤执行身份验证流，并介绍所涉及项目的各个部分：

1. 如果还没有遵循项目根目录 `readme.html` 文件中的说明来创建超级用户（管理员）帐户，请现在执行此操作。

1. 使用“调试” > “启动调试”(F5)，从 Visual Studio 运行应用。 当应用出现在浏览器中时，观察“登录”是否显示在导航栏右上方。

    ![Django Web 项目应用页上的登录控件](media/django/step05-login-control.png)

1. 打开 `templates/app/layout.html`，并观察 `<div class="navbar ...>` 元素是否包含标记 `{% include app/loginpartial.html %}`。 `{% include %}` 标记指示 Django 的模板化系统在包含模板中此时所含的文件内容中进行拉取。

1. 打开 `templates/app/loginpartial.html` 并观察它如何使用条件标记 `{% if user.is_authenticated %}` 与 `{% else %}` 标记来呈现不同的 UI 元素，具体取决于是否已对用户进行身份验证：

    ```html
    {% if user.is_authenticated %}
    <form id="logoutForm" action="/logout" method="post" class="navbar-right">
        {% csrf_token %}
        <ul class="nav navbar-nav navbar-right">
            <li><span class="navbar-brand">Hello {{ user.username }}!</span></li>
            <li><a href="javascript:document.getElementById('logoutForm').submit()">Log off</a></li>
        </ul>
    </form>

    {% else %}

    <ul class="nav navbar-nav navbar-right">
        <li><a href="{% url 'login' %}">Log in</a></li>
    </ul>

    {% endif %}
    ```

1. 由于首次启动应用时未对任何用户进行身份验证，因此该模板代码仅呈现指向相对路径“login”的“登录”链接。 正如 `urls.py` 中所指定的那样（如前一部分所示），该路由映射到提供有以下数据的 `django.contrib.auth.views.login` 视图：

    ```python
    {
        'template_name': 'app/login.html',
        'authentication_form': app.forms.BootstrapAuthenticationForm,
        'extra_context':
        {
            'title': 'Log in',
            'year': datetime.now().year,
        }
    }
    ```

    在这里，`template_name` 标识登录页模板，在本例中为 `templates/app/login.html`。 `extra_context` 属性被添加到提供给模板的默认上下文数据中。 最后，`authentication_form` 指定用于登录的窗体类，它在模板中显示为 `form` 对象。 默认值为 `AuthenticationForm`（来自 `django.contrib.auth.views`）；Visual Studio 项目模板改为使用在应用 `forms.py` 文件中定义的窗体：

    ```python
    from django import forms
    from django.contrib.auth.forms import AuthenticationForm
    from django.utils.translation import ugettext_lazy as _

    class BootstrapAuthenticationForm(AuthenticationForm):
        """Authentication form which uses boostrap CSS."""
        username = forms.CharField(max_length=254,
                                   widget=forms.TextInput({
                                       'class': 'form-control',
                                       'placeholder': 'User name'}))
        password = forms.CharField(label=_("Password"),
                                   widget=forms.PasswordInput({
                                       'class': 'form-control',
                                       'placeholder':'Password'}))
    ```

    如你所见，此窗体类派生自 `AuthenticationForm` 且专门替代用户名和密码字段来添加占位符文本。 Visual Studio 模板包括此显式代码，前提是你可能需要自定义窗体，比如添加密码强度验证。

1. 导航到登录页时，应用随即会显示 `login.html` 模板。 变量 `{{ form.username }}` 和 `{{ form.password }}` 呈现来自 `BootstrapAuthenticationForm` 的 `CharField` 窗体。 还有一个内置部分用于显示验证错误，如果选择添加这些服务，会有一个用于社交登录的现成元素。

    ```html
    {% extends "app/layout.html" %}

    {% block content %}

    <h2>{{ title }}</h2>
    <div class="row">
        <div class="col-md-8">
            <section id="loginForm">
                <form action="." method="post" class="form-horizontal">
                    {% csrf_token %}
                    <h4>Use a local account to log in.</h4>
                    <hr />
                    <div class="form-group">
                        <label for="id_username" class="col-md-2 control-label">User name</label>
                        <div class="col-md-10">
                            {{ form.username }}
                        </div>
                    </div>
                    <div class="form-group">
                        <label for="id_password" class="col-md-2 control-label">Password</label>
                        <div class="col-md-10">
                            {{ form.password }}
                        </div>
                    </div>
                    <div class="form-group">
                        <div class="col-md-offset-2 col-md-10">
                            <input type="hidden" name="next" value="/" />
                            <input type="submit" value="Log in" class="btn btn-default" />
                        </div>
                    </div>
                    {% if form.errors %}
                    <p class="validation-summary-errors">Please enter a correct user name and password.</p>
                    {% endif %}
                </form>
            </section>
        </div>
        <div class="col-md-4">
            <section id="socialLoginForm"></section>
        </div>
    </div>

    {% endblock %}
    ```

1. 在提交表单时，Django 会尝试对你所提供的凭据（如超级用户凭据）进行身份验证。 如果身份验证失败，你仍处于同一页面上，但 `form.errors` 将设置为 true。 如果身份验证成功，Django 将导航到“下一步”字段中的相对 URL `<input type="hidden" name="next" value="/" />`，在本例中为主页 (`/`)。

1. 现在，当主页再次呈现，`user.is_authenticated` 属性会在呈现 `loginpartial.html` 模板时设为“true”。 因此，你将看到“Hello (用户名)”消息和“注销”。 可以在应用其他部分中使用 `user.is_authenticated` 来检查身份验证。

    ![Django Web 项目应用页上的 Hello 消息和注销控件](media/django/step05-logoff-control.png)

1. 若要确定经过身份验证的用户是否有权访问特定资源，需要从该用户的数据库中检索用户特定的权限。 有关更多详细信息，请参阅[使用 Django 身份验证系统](https://docs.djangoproject.com/en/2.0/topics/auth/default/#permissions-and-authorization)（Django 文档）。

1. 特别需要指出的是，超级用户或管理员有权访问内置 Django 管理员界面，方法是使用相对 URL“/admin/”和“/admin/doc/”。 若要启用这些界面，请打开 Django 项目的 `urls.py` 并删除以下条目的注释：

    ```python
    from django.conf.urls import include
    from django.contrib import admin
    admin.autodiscover()

    # ...
    urlpatterns = [
        # ...
        url(r'^admin/doc/', include('django.contrib.admindocs.urls')),
        url(r'^admin/', include(admin.site.urls)),
    ]
    ```

    重新启动应用时，可以导航到“/admin/”和“/admin/doc/”并执行任务，如创建其他用户帐户。

    ![Django 管理员界面](media/django/step05-administrator-interface.png)

1. 身份验证流的最后一部分是注销。 正如 `loginpartial.html` 中所示，注销链接只需对相对 URL“/login”执行 POST 操作，这由内置视图 `django.contrib.auth.views.logout` 处理。 此视图不显示任何 UI，只需导航到主页（如“^logout$”模式 `urls.py` 中所示）。 若要显示注销页，首先按照下面的方式更改 URL，添加“template_name”属性并删除“next_page”属性：

    ```python
    url(r'^logout$',
        django.contrib.auth.views.logout,
        {
            'template_name': 'app/loggedoff.html',
            # 'next_page': '/',
        },
        name='logout')
    ```

    然后使用下面的（最小）内容创建 `templates/app/loggedoff.html`：

    ```html
    {% extends "app/layout.html" %}
    {% block content %}
    <h3>You have been logged off</h3>
    {% endblock %}
    ```

    结果如下所示：

    ![添加的注销页](media/django/step05-logged-off-page.png)

1. 完成所有操作后，停止服务器，并再次将所做的更改提交到源代码管理。

### <a name="question-what-is-the-purpose-of-the--crsftoken--tag-that-appears-in-the-form-elements"></a>问：\<form\> 元素中显示的 {% crsf_token %} 标记的用途是什么？

答：`{% crsf_token %}` 标记包含 Django 的内置[跨网站请求伪造 (crsf) 保护](https://docs.djangoproject.com/en/2.0/ref/csrf/)（Django 文档）。 通常将此标记添加到涉及 POST、PUT 或 DELETE 请求方法的任何元素（如窗体），模板呈现函数 (`render`) 会插入必要的保护。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用投票 Django Web 项目模板](learn-django-in-visual-studio-step-06-polls-django-web-project-template.md)

## <a name="going-deeper"></a>深入了解

- [Django 中的用户身份验证](https://docs.djangoproject.com/en/2.0/topics/auth/) (docs.djangoproject.com)
- GitHub 上的教程源代码：[Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django)