# Changelog

## [0.5.2](https://github.com/hugomods/hugopress/compare/v0.5.1...v0.5.2) (2026-01-07)


### Bug Fixes 🐞

* do not print multiple attributes on the &lt;html&gt; tag ([3188c32](https://github.com/hugomods/hugopress/commit/3188c32742ad01aa705339ac7d33542f7a8528c7))

## [0.5.1](https://github.com/hugomods/hugopress/compare/v0.5.0...v0.5.1) (2026-01-07)


### Bug Fixes 🐞

* avoid printing duplicate attributes ([#80](https://github.com/hugomods/hugopress/issues/80)) ([2aa6f48](https://github.com/hugomods/hugopress/commit/2aa6f48e483f51c0dff4545dcdce8a8b4c8a12b5))

## [0.5.0](https://github.com/hugomods/hugopress/compare/v0.4.1...v0.5.0) (2024-06-16)


### Features ✨

* allow using page store key as cache key by setting `cache_store_key` for hooks ([eac2547](https://github.com/hugomods/hugopress/commit/eac25471bb6bb7a1bbcf041961e17875f8566ba9))

## [0.4.1](https://github.com/hugomods/hugopress/compare/v0.4.0...v0.4.1) (2024-06-14)


### Performance Improvements ⚡️

* allow specifying a `partial` to directly include the desired template, using the current page as the context ([#60](https://github.com/hugomods/hugopress/issues/60)) ([4ea2769](https://github.com/hugomods/hugopress/commit/4ea27690b5dc7c891fdf8ea4deafe78ade97b070))
* avoid using merge function to generate context for hooks ([8541aa8](https://github.com/hugomods/hugopress/commit/8541aa880c50402489aa017fd79328714c8847d2))
* calculate Index, HasPrev, HasNext for hooks in advance ([#58](https://github.com/hugomods/hugopress/issues/58)) ([8541aa8](https://github.com/hugomods/hugopress/commit/8541aa880c50402489aa017fd79328714c8847d2))

## [0.4.0](https://github.com/hugomods/hugopress/compare/v0.3.0...v0.4.0) (2024-06-01)


### Features ✨

* add the cache_site_param_key to cache partial against site parameter ([#53](https://github.com/hugomods/hugopress/issues/53)) ([e12cdbc](https://github.com/hugomods/hugopress/commit/e12cdbceea6ca4652177aa08d9d68743641739d0))

## [0.3.0](https://github.com/hugomods/hugopress/compare/v0.2.3...v0.3.0) (2024-06-01)


### Features ✨

* add the cache_key parameter ([c92d66a](https://github.com/hugomods/hugopress/commit/c92d66a19c0eae2c221cfd9cfb9b82be97b453ab))
* add the cache_param_key parameter to cache partials by page params ([#50](https://github.com/hugomods/hugopress/issues/50)) ([fc51904](https://github.com/hugomods/hugopress/commit/fc51904b8082c38c9de6def196bbf5c32c4c9c60))

## [0.2.3](https://github.com/hugomods/hugopress/compare/v0.2.2...v0.2.3) (2023-12-22)


### Bug Fixes 🐞

* appending instead overriding attribute values ([#41](https://github.com/hugomods/hugopress/issues/41)) ([89f34c4](https://github.com/hugomods/hugopress/commit/89f34c471af4b149f65980a67472b8935dbd3c94))

## [0.2.2](https://github.com/hugomods/hugopress/compare/v0.2.1...v0.2.2) (2023-10-31)


### Bug Fixes 🐞

* adjust to accommodate Hugo v0.120.0 changes ([#36](https://github.com/hugomods/hugopress/issues/36)) ([16af083](https://github.com/hugomods/hugopress/commit/16af0830717f27d8785748081c8c61551d76b764))

## [0.2.1](https://github.com/hugomods/hugopress/compare/v0.2.0...v0.2.1) (2023-07-21)


### Performance Improvements ⚡️

* avoid checking the partials each time render the hooks and attributes ([f814b91](https://github.com/hugomods/hugopress/commit/f814b91b7e0ea30575e73992e97758266370acc2))

## [0.2.0](https://github.com/hugomods/hugopress/compare/v0.1.0...v0.2.0) (2023-06-16)


### Features

* add the debug parameter to enable verbose logs ([9ab073e](https://github.com/hugomods/hugopress/commit/9ab073ea6355f1d6fa2f3d1e370ac3d35d81351d))
* check if the attribute and hook partials exist ([79f5401](https://github.com/hugomods/hugopress/commit/79f5401f5cd6bfd3c4eb40d433ce963669de401d)), closes [#22](https://github.com/hugomods/hugopress/issues/22)
