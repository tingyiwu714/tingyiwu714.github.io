---
title: Build personal blog with Hexo and GitHub
date: 2019-06-13 01:39:46
categories:
  - Tutorials
tags:
  - Git
  - Hexo
toc: true
---

This article is a step by step instruction on creating a personal website using Hexo framework on GitHub pages with custom domain.

<!-- more -->

---

## What is Hexo?
Hexo is a simple yet powerful static blog framework powered by Node.js.

---

## Setup and Installation
### GitHub
1. Create a [GitHub account](https://github.com/)

2. Create a new repository named `<github_username>.github.io`

### Git	
1. Install [Git](https://git-scm.com/downloads)

2. Configure your Git username/email
	- Open the Git Bash
	- Set your username:
```
git config --global user.name <github_username>
```
	- Set your email address:
```
git config --global user.email <github_email>
```


3. Generate SSH Key and add to GitHub
	- From Git Bash, generate SSH key
```
ssh-keygen -t rsa -C <github_email>
```
	- Copy the SSH key from the id_rsa.pub file, and paste to [GitHub SSH key setting page](https://github.com/settings/keys)

	- From Git Bash, check if the setting is successful. 
```
ssh git@github.com
```

### Node.js	
1. Install [Node.js](https://nodejs.org/en/download/)

2. From Git Bash, check if Node.js install successfully. 
```
node -v
```

3. Check if npm install successfully.
```
npm -v
```

### Hexo
Install Hexo with npm
```
npm install -g hexo-cli
```

---

## Start Blogging
1. Initialize the blog in current directory
```
hexo init
```

2. Create a new article
```
hexo new <title>
```

3. Edit the markdown file under `/source/_posts`


4. Generate static file
```
hexo generate
```

5. Start local server
```
hexo server
```

6. Check the blog at http://localhost:4000

---

## Change Theme
1. Choose [theme](https://hexo.io/themes/)


2. Clone the theme to `/themes` folder
```
git clone <github_repo>
```


3. Edit the `_config.yml` file in root directory to use the new theme
```
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: <theme_name>
```


4. Follow the instructions of the new theme for further setting.


5. Start local server
```
hexo server
```


6. Check the blog at http://localhost:4000

---

## Deploy GitHub Pages
1. Edit the `_config.yml` file in root directory
```
deploy:
	type: git
	repo: <repository_url>
	branch: master
```


2. Install hexo deployer plugin
```
npm install hexo-deployer-git --save
```


3. Deploy the site
```
hexo clean && hexo generate && hexo deploy
```


4. Check the blog at `http://<github_username>.github.io`

---

## Front-matter and Other Setting
- Enable table of contents
```
toc: true
```


- Apply categories and tags
```
categories:
  - <categoriy_name>

tags:
  - <tag_name>
```


- Enable read more
```
<!-- more -->
```

---

## Use Custom Domain

---

## Backup and Recover Raw Files on GitHub
- Backup Files
	- Setup new branch for the raw files and push to GitHub

		1. Delete the `.gitignore` file and the `.git folder` in the theme folder.

		2. Push the raw files to the branch called `hexo`.
```
git init .
git checkout -b hexo		# new branch
git add .
git commit -m '<commit messae>'
git remote add origin <repository_url>
git push --set-upstream origin hexo
```

	- Continue push new update to GitHub
```
git add -a
git commit -m "<commit messae>"
git push origin hexo
```

- Recover Files
```
git clone <repository_url>
cd <github_username>.github.io/
git checkout hexo
npm install
hexo server
```

---
