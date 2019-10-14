# 源码分析

## 文件结构

``` bash
├── actions
|  ├── abstract.action.ts
|  ├── add.action.ts
|  ├── build.action.ts
|  ├── generate.action.ts
|  ├── index.ts
|  ├── info.action.ts
|  ├── new.action.ts
|  ├── start.action.ts
|  └── update.action.ts
├── bin
|  └── nest.ts - 注册入口文件，将commander模块传入commands/index.ts的load方法。
├── commands
|  ├── abstract.command.ts
|  ├── add.command.ts
|  ├── build.command.ts
|  ├── command.input.ts
|  ├── command.loader.ts
|  ├── generate.command.ts
|  ├── index.ts
|  ├── info.command.ts
|  ├── new.command.ts
|  ├── start.command.ts
|  └── update.command.ts
├── e2e - 集成测试相关
├── gulpfile.js
├── lib
|  ├── compiler
|  |  ├── assets-manager.ts
|  |  ├── compiler.ts
|  |  ├── defaults
|  |  |  └── webpack-defaults.ts
|  |  ├── helpers
|  |  |  ├── append-extension.ts
|  |  |  ├── get-value-or-default.ts
|  |  |  └── tsconfig-provider.ts
|  |  ├── hooks
|  |  |  └── tsconfig-paths.hook.ts
|  |  ├── plugins-loader.ts
|  |  ├── watch-compiler.ts
|  |  ├── webpack-compiler.ts
|  |  └── workspace-utils.ts
|  ├── configuration
|  |  ├── configuration.loader.ts
|  |  ├── configuration.ts
|  |  ├── defaults.ts
|  |  ├── index.ts
|  |  └── nest-configuration.loader.ts
|  ├── dependency-managers
|  |  ├── index.ts
|  |  └── nest.dependency-manager.ts
|  ├── package-managers
|  |  ├── abstract.package-manager.ts
|  |  ├── index.ts
|  |  ├── npm.package-manager.ts
|  |  ├── package-manager-commands.ts
|  |  ├── package-manager.factory.ts
|  |  ├── package-manager.ts
|  |  ├── project.dependency.ts
|  |  └── yarn.package-manager.ts
|  ├── questions
|  |  └── questions.ts
|  ├── readers
|  |  ├── file-system.reader.ts
|  |  ├── index.ts
|  |  └── reader.ts
|  ├── runners
|  |  ├── abstract.runner.ts
|  |  ├── git.runner.ts
|  |  ├── index.ts
|  |  ├── npm.runner.ts
|  |  ├── runner.factory.ts
|  |  ├── runner.ts
|  |  ├── schematic.runner.ts
|  |  └── yarn.runner.ts
|  ├── schematics
|  |  ├── abstract.collection.ts
|  |  ├── collection.factory.ts
|  |  ├── collection.ts
|  |  ├── custom.collection.ts
|  |  ├── index.ts
|  |  ├── nest.collection.ts
|  |  └── schematic.option.ts
|  ├── ui
|  |  ├── banner.ts
|  |  ├── emojis.ts
|  |  ├── errors.ts
|  |  ├── index.ts
|  |  ├── messages.ts
|  |  └── prefixes.ts
|  └── utils
|     ├── is-error.ts
|     └── remaining-flags.ts
├── scripts
|  └── check-version.js
├── tools
|  └── gulp
|     ├── config.ts
|     ├── gulpfile.ts
|     ├── tasks
|     |  └── clean.ts
|     ├── tsconfig.json
|     └── util
|        └── task-helpers.ts
├── tsconfig.json
├── tslint.json
└── yarn.lock
```

## 外部模块依赖

[过于复杂，参加](http://npm.broofa.com/?q=@nestjs/cli)

## 内部模块依赖


## 逐个文件分析

### bin/nest.ts

注册入口文件，基于commander模块，将模块内容传入commands/index.ts提供的load方法。

默认没参数则输出帮助help。





---


<p align="center">
  <a href="http://nestjs.com/" target="blank"><img src="https://nestjs.com/img/logo_text.svg" width="320" alt="Nest Logo" /></a>
</p>

  <p align="center">A progressive <a href="http://nodejs.org" target="blank">Node.js</a> framework for building efficient and scalable server-side applications, heavily inspired by <a href="https://angular.io" target="blank">Angular</a>.</p>
    <p align="center">
<a href="https://www.npmjs.com/~nestjscore"><img src="https://img.shields.io/npm/v/@nestjs/cli.svg" alt="NPM Version" /></a>
<a href="https://www.npmjs.com/~nestjscore"><img src="https://img.shields.io/npm/l/@nestjs/cli.svg" alt="Package License" /></a>
<a href="https://www.npmjs.com/~nestjscore"><img src="https://img.shields.io/npm/dm/@nestjs/cli.svg" alt="NPM Downloads" /></a>
  <a href="https://travis-ci.org/nestjs/nest"><img src="https://api.travis-ci.org/nestjs/nest.svg?branch=master" alt="Travis" /></a>
<a href="https://travis-ci.org/nestjs/nest"><img src="https://img.shields.io/travis/nestjs/nest/master.svg?label=linux" alt="Linux" /></a>
<a href="https://coveralls.io/github/nestjs/nest?branch=master" target="_blank"><img src="https://coveralls.io/repos/github/nestjs/nest/badge.svg?branch=master#9" alt="Coverage" /></a>
<a href="https://discord.gg/G7Qnnhy" target="_blank"><img src="https://img.shields.io/badge/discord-online-brightgreen.svg" alt="Discord"/></a>
<a href="https://opencollective.com/nest#backer" target="_blank"><img src="https://opencollective.com/nest/backers/badge.svg" alt="Backers on Open Collective" /></a>
<a href="https://opencollective.com/nest#sponsor" target="_blank"><img src="https://opencollective.com/nest/sponsors/badge.svg" alt="Sponsors on Open Collective" /></a>
  <a href="https://paypal.me/kamilmysliwiec" target="_blank"><img src="https://img.shields.io/badge/Donate-PayPal-ff3f59.svg"/></a>
  <a href="https://twitter.com/nestframework" target="_blank"><img src="https://img.shields.io/twitter/follow/nestframework.svg?style=social&label=Follow"></a>

## Description

In order to help people manage their projects, the CLI tool has been created. It helps on many grounds at once, from scaffolding the project to build well-structured applications. The Nest CLI is based on the [@angular-devkit](https://github.com/angular/devkit) package. Also, there're special schematics that are dedicated to the Nest development [@nestjs/schematics](https://github.com/nestjs/schematics).


## Installation
### NPM:

```
$ npm install -g @nestjs/cli
```

### Docker:
```
$ docker pull nestjs/cli[:version]
$ docker run -it --rm -p 3000:3000 -v `pwd`:/workspace nestjs/cli[:version]
```

### GIT:
```
$ git clone https://github.com/nestjs/nest-cli.git <project>
$ cd <project>
```

With your Node runtime:
```
$ npm install
$ npm run build
$ npm link
```

With Docker:

```
$ docker build -t nestjs/cli .
```

## Usage

Learn more in the [official documentation](https://docs.nestjs.com/cli/overview).

## Stay in touch

* CLI Author - [Thomas Ricart](https://github.com/ThomRick)
* Website - [https://nestjs.com](https://nestjs.com/)
* Twitter - [@nestframework](https://twitter.com/nestframework)
