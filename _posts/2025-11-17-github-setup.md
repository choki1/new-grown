---
title: "个人github搭建"
layout: default
---

## github搭建的具体流程

---

### 配置 Git 与 GitHub

1. **安装并配置 Git**  

    使用以下命令设置用户名和邮箱：

    ```
    git config --global user.name "名字"
    git config --global user.email "邮箱"
    ```
2. **配置 SSH 免密登录 GitHUb**  

    生成 SSH Key:

    ```
    ssh-keygen -t ed25519 -C "邮箱"
    ```

    将生成的公钥添加到 GitHub 设置中的 SSH Keys。
    测试使用以下命令：

    ```
    ssh -T git@github.com
    ```

    输出"Hi xxx!"为成功。

3. **将已创建的博客仓库 Clone 到本地文件夹**

    在选定的文件夹中的Git Bash执行：

    ```
    git clone git@github.com:你的用户名/你的仓库名.git
    ```
    成功后会在当前文件夹生成一个完整的仓库文件夹。  
    以后所有改动在此文件夹中进行。

4. **初始化博客主题和目录结构** 

    本博客选择使用 Jekyll 中的 Modernist 主题:

    1. 安装RubyInstaller
    2. 启动ridk: `` ridk enable ``
    3. 安装 Jekyll和 Bundler: `` gem install jekyll bundler`` (gem 是 Ruby 的包管理器。)
    4. 在文件夹中生成完成 Jekyll 博客结构:jekyll new . --force
    5. 安装依赖: bundle install
    6. 选用 Modernist 主题:
        1. 将以下内容添加到 `` _config.yml ``:
        ```
        remote_theme: pages-themes/modernist@v0.2.0
        plugins:
        - jekyll-remote-theme
        ```
        2. 如果想在电脑上预览网站，将以下内容添加到 `` Gemfile `` 
        ```
        gem "github-pages", group: :jekyll_plugins
        ```

    7. 启动本地预览服务器  
        运行: `` bundle exec jekyll serve ``  
        访问地址为 http://localhost:4000/

5. **在``_posts``中创建文章**

    文章必须放在``_posts``文件夹中，并且命名格式为  ``年-月-日-标题.md``。  
    文件保存编码必须为 UTF-8。

    在 markdown 文件中的最顶部需要 YAML 部分，用于定义文件的元数据：作者、创建日期、标签等。
    YAML的示例：
    ```
    ---
    title: "欢迎来到我的博客"
    layout: default
    date: 2025-11-17
    tags: [Jekyll, GitHub, 学习]
    ---
    这里是文章内容，Markdown 格式。

    ```

6. **编辑首页文件**

    创建或修改``index.md``，使博客首页进行显示文章列表：
    ```
    ---
    layout: defalut
    title: 欢迎来到我的博客
    ---

    ## 最新文章

    <ul>
    {% for post in site.posts %}
        <li>
        <a href="{{ post.url }}">{{ post.title }}</a> - {{ post.date | date: "%Y-%m-%d" }}
        </li>
    {% endfor %}
    </ul>

    ```