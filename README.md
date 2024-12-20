1、创建项目及子模块

```js
// 根目录
npm init -y

// 创建子模块
npm init -w packages/core -y
npm init -w packages/cli -y
```

2、cli 包添加 core 包为依赖

```js
  npm install core --workspace cli
```

3、修改 package.json 包名，加上 scope

修改完成后，重新 npm install

4、安装 ts

```js
npm install --save-dev typescript @types/node
```

5、在 core 和 cli 包下创建 tsconfig.json

```js
npm exec --workspace @qx-npm/cli -- npx tsc --init
```

在所有 workspace 下执行命令
```js
npm exec --workspaces -- npx tsc --init
```

6、core 模块下添加代码

添加后、编译
```js
npm exec --workspace @qx-npm/core -- npx tsc

```

7、cli 模块下添加依赖

```js
npm install --workspace @qx-npm/cli chalk commander
```

添加代码

8、编译全部模块

```js
npm exec --workspaces -- npx tsc
```

9、测试执行

```js
npm exec --workspace @qx-npm/cli -- node ./dist/index.js add 1 2
npm exec --workspace @qx-npm/cli -- node ./dist/index.js minus 1 2
```

10、cli 内 配置 bin

```js
"bin": {
  "num-calc": "./dist/index.js"
},
```

11、使用 charset 发布

```js
npm install --save-dev @changesets/cli prettier-plugin-organize-imports prettier-plugin-packagejson

npx changeset init
```

12、初始化 git
```js
git init

git add .

git commit -m 'first commit'
```

13、发布

  13.1 提交变化信息

  ```js
    npx changeset add
  ```

  13.2 生成版本

  ```js
    npx changeset version
  ```

  13.3 发布到仓库
  ```js
    git add .
    git commit -m 'second commit'

    npx changeset publish
  ```

14、测试

```js
npx @qx-npm/cli minus 3 4
npx @qx-npm/cli add 3 4

```