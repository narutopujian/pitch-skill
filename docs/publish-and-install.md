# 老师发布与学生安装

## 老师只做一次：发布到 GitHub

1. 在 GitHub 新建一个 **Public** 空仓库，名称建议使用 `founder-pitch-studio-skill`。
2. 不要勾选自动创建 README、`.gitignore` 或 License。
3. 在本地仓库运行：

```bash
git remote add origin https://github.com/narutopujian/founder-pitch-studio-skill.git
git push -u origin main
```

4. 确认根目录 `README.md` 中的安装地址指向当前公开仓库。

## 学生安装

在 Codex 中输入：

```text
$skill-installer install https://github.com/narutopujian/founder-pitch-studio-skill/tree/main/skills/founder-pitch-studio
```

安装完成后重启 Codex。

## 学生使用

1. 用 Codex 打开自己的项目文件夹。
2. 输入：

```text
$founder-pitch-studio 请读取我的项目，生成最终 Founder Pitch。
```

3. Skill 会展示十种风格；学生只需回复 `1` 到 `10`。
4. 等待它连续生成材料清单、MD 大纲、HTML、三种演讲稿和投资人问答。

如果老师希望全班统一风格，可以让学生直接输入：

```text
$founder-pitch-studio 我选择第 1 种风格：Studio 编辑部白。请读取我的项目，生成最终 Founder Pitch。
```

这样整个过程不再询问问题。

## 生成结果

结果统一保存在学生项目根目录的 `founder-pitch-output/`：

- `01_发布大纲.md`
- `02_Founder_Pitch.html`
- `03_演讲稿_5分钟逐字版.md`
- `04_演讲稿_3分钟精简版.md`
- `05_演讲稿_关键词提示卡.md`
- `06_投资人问答准备.md`

HTML 固定为 16:9，可用键盘方向键、页面按钮或鼠标右键翻页。

## 课堂前检查

- 每台电脑已经安装并重启 Codex。
- 每名学生都用 Codex 打开了自己的项目根目录。
- 学生项目里有当前代码、项目说明和进度记录。
- 浏览器可以正常打开本地 HTML 文件。
- 第一次安装时电脑可以访问 GitHub。
