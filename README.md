<p align="center">
    <img src="logo.png">
</p>

[![Used By](https://img.shields.io/badge/dynamic/json?color=success&label=used+by&query=repositories_humanize&logo=hugo&style=flat-square&url=https://api.razonyang.com/v1/github/dependents/hugomods/hugopress)](https://github.com/hugomods/hugopress/network/dependents)
![Hugo Requirements](https://img.shields.io/badge/dynamic/json?color=important&label=requirements&query=requirements&logo=hugo&style=flat-square&url=https://api.razonyang.com/v1/hugo/modules/github.com/hugomods/hugopress)
[![License](https://img.shields.io/github/license/hugomods/hugopress?style=flat-square)](https://github.com/hugomods/hugopress/blob/main/LICENSE)
[![Version](https://img.shields.io/github/v/tag/hugomods/hugopress?label=version&style=flat-square)](https://github.com/hugomods/hugopress/tags)

Pluggable and UI less [Hugo](https://gohugo.io/) modules framework, which defines several functions and partials to load and render Hugo modules automatically.
The main advantage is that once the theme support HugoPress, their users have the ability to install the modules without requesting new features to the theme.

## Principle

There are two key concepts: `attributes` and `hooks`.

### Attributes

The `attributes` are used to append attributes to HTML tags.

| Name | Description
|---|---
| `document` | The attributes will be appended into the `<html>` tag.
| `body` | The attributes will be appended into the `<body>` tag.

The attributes partial should return key-value pairs.

```html
{{- return dict
  "lang" .Page.Lang
  "data-foo" "bar"
  "data-hello" "world"
}}
```

#### Attributes Parameters

| Name | Type | Default | Description
|---|:-:|:-:|---
| `cacheable` | Boolean | `false` | Whether to cache the attributes.

#### Attributes Context

The context (aka the `.`) of attributes' partial.

| Name | Type | Description
|---|---|---
| `Page` | [Page](https://gohugo.io/variables/page/) | Current page.

### Hooks

The `hooks` are used to render HTML of the module in a specific place, such as `<head>`, `<body>`.

| Name | Description
|---|---
| `head-begin` | At the beginning of the `<head>` tag.
| `head-end` | Before the `<head>` end.
| `body-begin` | At the beginning of the `<body>` tag.
| `body-end` | Before the `<body>` end.

#### Hooks Parameters

| Name | Type | Default | Description
|---|:-:|:-:|---
| `cacheable` | Boolean | `false` | Whether to cache the hooks.

#### Hooks Context

The context (aka the `.`) of hook partial.

| Name | Type | Description
|---|---|---
| `Total` | Number | The number of modules in the current hook.
| `Index` | Number | The index number of current module.
| `HasPrev` | Boolean | Whether there are modules(s) before the current.
| `HasNext` | Boolean | Whether there are modules(s) after the current.
| `Page` | [Page](https://gohugo.io/variables/page/) | Current page.

## Guide

### Create a HugoPress Theme

Modify your `baseof.html` as following for getting much more flexible, and then override the `theme` blocks.

```go
{{/* layouts/_default/baseof.html */}}
<!DOCTYPE html>
<html {{ partial "hugopress/document-attributes" . | safeHTMLAttr -}}>
  <head>
    {{- partial "hugopress/head-begin.html" . }}
    {{/* Theme head block begin. */}}
    <title>{{- block "title" . -}}{{ .Title }}{{- end -}}</title>
    {{/* Theme head block end. */}}
    {{- partial "hugopress/head-end.html" . }}
  </head>
  <body {{ partial "hugopress/body-attributes" . | safeHTMLAttr -}}>
    {{- partial "hugopress/body-begin.html" . }}
    {{/* Theme body block begin. */}}
    {{- block "main" . }}{{- end }}
    {{/* Theme body block end. */}}
    {{- partial "hugopress/body-end.html" . }}
  </body>
</html>
```

### Create a HugoPress Modules

Let's take the `hello` module as an example, which

1. Append `data-hello="world"` into the `<html>` tag.
1. Generate `<meta name="hello" content="world">` inside the `<head>` tag.
1. Print `Hello world.` at the beginning of `<body>` tag.

#### Initialize Module

```
$ mkdir hugo-mod-hello
$ cd hugo-mod-hello
$ hugo mod init github.com/user/hugo-mod-hello
```

#### Modules Configuration

```toml
[params.hugopress.modules.hello.attributes.document]
[params.hugopress.modules.hello.hooks.head-end]
[params.hugopress.modules.hello.hooks.body-begin]
```

We need to specify the attributes and hooks used by the module in `config.toml`.

#### Modules Architecture

```
$ tree layouts/partials/hugopress/modules/hello
├── attributes
│   └── document.html
└── hooks
    ├── body-begin.html
    └── head-end.html
```

The module files should be placed under the `layouts/partials/hugopress/modules` folder.

> The source code can be found at [hello module files](exampleSite/layouts/partials/hugopress/modules/hello).

#### Disable Module

```toml
[params.hugopress.modules.hello]
disabled = true
```

#### Cacheable Attributes and Hooks

```toml
[params.hugopress.modules.hello.attributes.document]
cacheable = true

[params.hugopress.modules.hello.hooks.body-begin]
cacheable = true
```

#### Hooks Weight

Lower weight gets higher precedence.

```toml
[params.hugopress.modules.hello.hooks.body-begin]
weight = 1
```

## Functions

| Name | Description
|---|---
| `{{ partial "hugopress/functions/has-modules" $hookName }}` | Indicate if there are modules associate to the specified hook.
| `{{ partial "hugopress/functions/exists" $moduleName }}` | Indicate whether the module exists.
| `{{ partial "hugopress/functions/is-disabled" $moduleName }}` | Indicate whether the module was disabled, `false` if module doesn't exist.
