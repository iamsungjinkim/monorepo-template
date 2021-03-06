# monorepo-template

> with yarn berry workspace

## ๐ ๋ชฉ์ฐจ

1. [๐ yarn berry ์์ํ๊ธฐ](#-yarn-berry-์์ํ๊ธฐ)
2. [๐  yarn workspace ์ค์ ํ๊ธฐ](#-yarn-workspace-์ค์ ํ๊ธฐ)
3. [๐ญ Next.js ํจํค์ง ์ถ๊ฐํ๊ธฐ](#-nextjs-ํจํค์ง-์ถ๊ฐํ๊ธฐ)
4. [โจ typescript ์ค์ ํ๊ธฐ](#-typescript-์ค์ ํ๊ธฐ)
5. [๐งณ ์ฌ๋ฌ ํจํค์ง์ ์คํฌ๋ฆฝํธ ํ๋ฒ์ ์คํ์ํค๊ธฐ](#-์ฌ๋ฌ-ํจํค์ง์-์คํฌ๋ฆฝํธ-ํ๋ฒ์-์คํ์ํค๊ธฐ)
6. [๐ commitlint, commitizen ์ค์ ํ๊ธฐ](#-commitlint-commitizen-์ค์ ํ๊ธฐ)
7. [๐ฅ  cypress ์ค์ ํ๊ธฐ](#-cypress-์ค์ ํ๊ธฐ)
   <br>
   <br>

## ๐ yarn berry ์์ํ๊ธฐ

```bash
yarn set version berry
yarn -v
yarn init
```

ํ๋ก์ ํธ์ rootํด๋์์ yarn berry๋ก ์ค์  ๋ฐ ๋ฒ์  ํ์ธํ๊ณ  ํ๋ก์ ํธ๋ฅผ ์์  
<br>

## ๐  yarn workspace ์ค์ ํ๊ธฐ

```json
{
  "name": "monorepo-template",
  "private": true,
  "workspaces": {
    "packages": ["package/*"]
  },
  "packageManager": "yarn@3.2.1"
  //...
}
```

yarn workspace๋ฅผ ์ฌ์ฉํ๊ธฐ ์ํด, packageํด๋(๋ค๋ฅธ ์ด๋ฆ์ ์ฌ์ฉํด๋ ๋๋ค)๋ฅผ ๋ง๋ค๊ณ  ์์ ๊ฐ์ด ์ค์ ํ๋ค.  
์์ผ๋ก ์ถ๊ฐํ  ํจํค์ง๋ค์ packageํด๋์ ํ์์ ๊ตฌ์ฑํ๋ฉด ๋๋ค.  
<br>

## ๐ญ Next.js ํจํค์ง ์ถ๊ฐํ๊ธฐ

```bash
cd package
yarn create next-app --typescript
```

packageํด๋๋ก ์ด๋ํ์ฌ Next.js ํ๋ก์ ํธ๋ฅผ ์์ฑํ๋ค.

```bash
โโโ package
โ   โโโ next-web
โ       โโโ //...
โ       โโโ tsconfig.json
โ       โโโ package.json
โโโ package.json
```

๋๋ต ์์ ๊ฐ์ ๊ตฌ์กฐ๊ฐ ๋  ๊ฒ์ด๋ค.

```json
{
  //...
  "script": {
    "next-web": "yarn workspaces next-web"
  }
  //...
}
```

root์ package.json์ script๋ฅผ ์ถ๊ฐํ์ฌ, root๊ฒฝ๋ก์์ ํจํค์ง์ script๋ฅผ ์คํ์ํฌ ์ ์๋ค.  
<br>

## โจ Typescript ์ค์ ํ๊ธฐ

```bash
yarn add -D typescript prettier eslint
```

ํจํค์ง ์ ์ฒด์ ๊ณตํต์ผ๋ก ์ ์ฉํ  ๋ด์ฉ์ root์ ์ค์ ํด์ฃผ๊ณ , ๊ฐ ํจํค์ง๋ณ ๊ฐ๋ณ์ ์ผ๋ก ๊ด๋ฆฌ๊ฐ ํ์ํ ์ค์ ์ ๋ถ๋ฆฌํ์ฌ ๊ฐ ํจํค์ง์ ์ค์ ํด์ฃผ๋ฉด ๋๋ค.  
์ฐ์ , root์ ๊ณตํต ์ค์ ์ ํด์ค๋ค.  
<br>

> โ vscode๋ฅผ ์ฌ์ฉํ๋ค๋ฉด yarn berry์ ๋ง์ถฐ [sdk์ค์ ](https://yarnpkg.com/getting-started/editor-sdks#vscode)์ ํด์ค์ผํ๋ค.
>
> ```bash
> yarn dlx @yarnpkg/sdks vscode
> ```
>
> sdk๋ฅผ ์ค์นํ ๋ค, command pallette์์ `Typescript: Select Typescript Version`์ ์ ํํ์ฌ `Use Workspace Version`์ ์ ํํ๋ค.

<br>

```json
// package/next-web/tsconfig.json
{
  "extends": "../../tsconfig.json",
  "include": ["next-env.d.ts", "src/**/*"],
  "exclude": ["node_modules"]
}
```

์ด์  ๊ฐ๋ณ ํจํค์ง์ typescript ์ค์ ์ ์ ์ฉํ์.  
root์ ๊ณตํต ์ค์ ์ ๋ถ๋ฌ์ค๊ณ , ๊ฐ๋ณ์ ์ผ๋ก ์ค์ ์ ์ถ๊ฐํ  ์ ์๋ค.

์ถ๊ฐ์ ์ผ๋ก ํจํค์ง์ eslint๋ฅผ ์ ์ฉํ๊ธฐ ์ํด์ ๋ค์๊ณผ ๊ฐ์ด ์ค์ ์ ์ถ๊ฐํด์ค๋ค.

```js
// .eslintrc.js
module.exports = {
  // ...
  overrides: [
    // ...
    {
      files: [
        'package/next-web/src/**/*.ts?(x)',
        'package/next-web/src/**/*.js?(x)',
      ],
      settings: {
        'import/resolver': {
          typescript: {
            project: path.resolve(
              `${__dirname}/package/next-web/tsconfig.json`
            ),
          },
        },
      },
    },
    // ...
  ],
};
```

<br>

## ๐งณ ์ฌ๋ฌ ํจํค์ง์ ์คํฌ๋ฆฝํธ ํ๋ฒ์ ์คํ์ํค๊ธฐ

ํจํค์ง๋ค์ ์ํํ๋ฉฐ ์คํฌ๋ฆฝํธ๋ฅผ ์คํ์ํค๊ธฐ ์ํด์๋ plugin์ ์ค์นํด์ค์ผ ํ๋ค.

```bash
yarn plugin import plugin-workspace-tools
```

plugin์ ์ค์นํ๋ค๋ฉด, root์ package.json์ scprit๋ฅผ ์ถ๊ฐํด์ค๋ค.

```json
{
  // ...
  "scripts": {
    // ...
    "build:packages": "yarn workspaces foreach run build",
    "test:all": "yarn workspaces foreach --parallel run test"
  }
  // ...
}
```

`foreach`๋ฅผ ์ฌ์ฉํ์ฌ, ํจํค์ง๋ฅผ ์ํํ๋ฉฐ ์คํฌ๋ฆฝํธ๋ฅผ ์คํํ  ์ ์๋ค.  
<br>

## ๐ commitlint, commitizen ์ค์ ํ๊ธฐ

```bash
yarn add -D @commitlint/cli @commitlint/config-conventional
```

```js
// commitlint.config.js
module.exports = {
  extends: ['@commitlint/config-conventional'],
};
```

root์ commitlint๋ฅผ ์ค์นํ ๋ค, `commitlint.config.js`์ ์ค์ ์ ์ถ๊ฐํ๋ค.

์ด์  commit์ด ์คํ๋ ๋ ์๋์ผ๋ก lint๋ฅผ ๊ฒ์ฌํ๋๋ก ์ค์ ํ์.

```bash
yarn add -D husky
yarn husky install
yarn husky add .husky/commit-msg 'yarn commitlint --edit "$1"'
```

์ด์  [husky](https://github.com/typicode/husky)์ ๋์์ผ๋ก, git hook์ ์ด์ฉํ์ฌ ์ปค๋ฐ ๋ฉ์ธ์ง์ ํ์์ ๊ฒ์ฌํ  ์ ์๊ฒ ๋์๋ค.  
ํ์ง๋ง ํ์ ์ปค๋ฐ ๋ฉ์ธ์ง ์ปจ๋ฒค์์ ์์ ํ ์ธ์ฐ์ง ์์๋ค๋ฉด, ์ปค๋ฐ๊ท์น์ ํ์ธํด์ผํ๋ ๊ฒฝ์ฐ๊ฐ ์ข์ข ๋ฐ์ํ๋ค.  
`commitizen`์ ๋์์ ๋ฐ์์, ์์ ๋ฌธ์ ๋ฅผ ํด๊ฒฐํ  ์ ์๋ค.

```bash
yarn add -D commitizen cz-conventional-changelog
```

```json
{
  // ...
  "scripts": {
    // ...
    "commit": "cz"
  },
  "devDependencies": {
    // ...
    "commitizen": "^4.2.4",
    "cz-conventional-changelog": "^3.3.0"
  },
  "config": {
    "commitizen": {
      "path": "cz-conventional-changelog"
    }
  }
  // ...
}
```

`commitizen`์ ์ค์นํ๊ณ , `cz-conventional-changelog` ์ด๋ํฐ๋ฅผ ์ค์ ํ์๋ค.  
ํ์ง๋ง ์ฌ์ค ์์ ๊ฐ์ด ์ค์ ํ๋ฉด ์ค์นํ `cz-conventional-changelog`๊ฐ ์ ์ฉ๋์ง ์๊ณ , ๋ค๋ฅธ ๋ฒ์ ์ ์ด๋ํฐ๊ฐ ์ ์ฉ๋๋ค.  
์ด๋ฅผ ํด๊ฒฐํ๊ธฐ ์ํด์๋ ์ด๋ํฐ๋ฅผ `unplug`ํด์ผ ํ๋ค.

```bash
yarn unplug cz-conventional-changelog
```

`.yarn/unplugged/cz-conventional-changelog-npm-3.3.0-46c1d2629a`ํด๋๊ฐ ์๊ฒผ๋ค.  
์ด์  ๊ฒฝ๋ก๋ฅผ ๋ค์ ์ก์์ฃผ๋ฉด ๋๋ค.

```json
{
  // ...
  "scripts": {
    // ...
    "commit": "cz"
  },
  "devDependencies": {
    // ...
    "commitizen": "^4.2.4",
    "cz-conventional-changelog": "^3.3.0"
  },
  "config": {
    "commitizen": {
      "path": ".yarn/unplugged/cz-conventional-changelog-npm-3.3.0-46c1d2629a/node_modules/cz-conventional-changelog"
    }
  },
  "dependenciesMeta": {
    "cz-conventional-changelog@3.3.0": {
      "unplugged": true
    }
  }
  // ...
}
```

์ด์  ์ค์นํด์ค ์ด๋ํฐ๊ฐ ์ ์์ ์ผ๋ก ์ ์ฉ๋๋ค.  
<br>

## ๐ฅ  cypress ์ค์ ํ๊ธฐ
