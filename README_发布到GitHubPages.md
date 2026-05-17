# 发布到 GitHub Pages（手把手清单）

> 你的博客工程目录：`myblog/`
>
> 你现在只需要按下面步骤做，就能上线到：`https://<你的GitHub用户名>.github.io`

## 1. 先改 1 个配置（非常重要）
打开 `myblog/_config.yml`，找到这一行：

```yml
url: https://example.github.io  # 部署前把 example 改成你的 GitHub 用户名
```

把它改成你的真实用户名，例如你叫 `octocat`：

```yml
url: https://octocat.github.io
```

`root: /` 保持不动（用户站点一般就是 `/`）。

## 2. 在 GitHub 创建仓库（用户站点仓库）
1) 打开 GitHub → New repository  
2) 仓库名必须是：`<你的GitHub用户名>.github.io`  
3) 建议选择 Public → Create repository

## 3. 打开 Pages 的 Actions 发布方式
进入仓库：
- Settings → Pages  
- Build and deployment → Source 选择 **GitHub Actions**

（工程里我已经放好了工作流：`myblog/.github/workflows/pages.yml`）

## 4. 把本地工程推送到 GitHub
在你电脑终端进入 `myblog/`，执行：

```bash
git init
git add .
git commit -m "init hexo blog"
git branch -M main
git remote add origin https://github.com/<你的GitHub用户名>/<你的GitHub用户名>.github.io.git
git push -u origin main
```

### 如果提示需要登录/权限
常见做法二选一：
1) **HTTPS + Personal Access Token（推荐小白）**  
   - GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)  
   - 生成一个 token（勾选 repo 相关权限即可）  
   - 之后 `git push` 时把 token 当“密码”用
2) SSH（更偏进阶）：配置 SSH key 再推送

## 5. 等待自动部署完成
1) 打开仓库 → Actions  
2) 看到 “Deploy Hexo to GitHub Pages” 这条 workflow 变绿 ✅  
3) 回到 Settings → Pages，能看到你的站点地址  
4) 访问：`https://<你的GitHub用户名>.github.io`

> 首次部署可能要等几分钟；如果一直没出来，优先看 Actions 的失败日志。

## 6. 以后你写文章的日常流程（最常用）
在 `myblog/` 目录：

```bash
# 新建文章
npx hexo new post "标题"

# 本地预览（可选）
npx hexo server

# 写完就推送（触发自动部署）
git add .
git commit -m "update"
git push
```

## 7. 常见问题（你遇到就对照）
### 7.1 页面能打开但没样式 / 资源 404
- 90% 是 `myblog/_config.yml` 的 `url` 没改对（必须是你真实的 `https://用户名.github.io`）

### 7.2 Actions 报错 `npm ci` 失败
- 确认仓库里有 `package-lock.json`（本工程默认有）
- 或把 workflow 里 `npm ci` 改成 `npm install`（不推荐，但能救急）

git init
git add .
git commit -m "init hexo blog"
git branch -M main
git remote add origin https://github.com/a-sheng02/a-sheng02.github.io.git
git push -u origin main