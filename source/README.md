## hexo-starter-plus

A enhanced starter for hexo with two branch.

## How to use

1. git clone

```shell
git clone https://github.com/cogons/hexo-starter-plus.git
cd hexo-starter-plus
```

2. config

```shell
sed -i'' "s~/cogons/hexo-starter-plus~{{your name/your repo}}~" _config.yml
```

or manual edit the deploy repo in _config.yml 

3. deploy

```shell
hexo generate --deploy
```