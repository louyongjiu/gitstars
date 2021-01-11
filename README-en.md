[中文文档](https://github.com/znlbwo/gitstars)

As the developer's first social platform, github has countless outstanding open source projects that bring great convenience to work and study. Projects that you need or love are just a click away from Star.

Star is easy, but with stars repositories growing and passing, it's hard to remember what it takes to use a project. Github provides only a simple search, find the target star repositorie actually has become a minor troublesome thing.

So having your own github stars repositories manager is a must-have for developers.

Previously used github stars repositories manager on the market, such as [Astral](https://app.astralapp.com), although it can be used, but always feel awkward, not easy to use.

Gitstars was born. 🎉

Pure front-end implementation, no server and database, your github is everything.

# Gitstars

[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)
[![GitHub license](https://img.shields.io/github/license/znlbwo/gitstars.svg)](https://github.com/znlbwo/gitstars/blob/master/LICENSE)

> Github stars repositories manager, which every developer owns.

Welcome to [https://znlbwo.github.io/gitstars/](https://znlbwo.github.io/gitstars/) to enjoy the fun, more welcome to provide advice in the [Issues](https://github.com/znlbwo/gitstars/issues) after the experience.

![gitstars](http://oh8wftuto.bkt.clouddn.com/gitstars-v2.0.0.jpg)

_Thanks to [imsun](https://github.com/imsun) for get access token service_

## Technology stack

- [Vue](https://cn.vuejs.org/)
- [Vuex](https://vuex.vuejs.org/)
- [Element-UI](http://element-cn.eleme.io/2.0/#/zh-CN)
- [Axios](https://github.com/axios/axios)
- [Github API v3](https://developer.github.com/v3/)

Extensive use of Flex layout, so please do not use on IE.

The project release version using Vue development, source [dev branch](https://github.com/znlbwo/gitstars/tree/dev). There is also a React development version, source in [react-dev branch](https://github.com/znlbwo/gitstars/tree/react-dev), just for practice.

Welcome to read the source code, make comments.

## Introduction

Interface style mimics [Astral](https://app.astralapp.com), support Chinese and English switch.

You may be curious, there is no database, where is the tag management data stored? Please see below:

![gitstars-gists-gitstars-json](http://oh8wftuto.bkt.clouddn.com/gitstars-gist-v2.0.0.jpg)

When you first visit gitstars, a gist project with the file `gitstars.json` will be created within your github gists (There are two on the map because the development needs, as a user, you will only have one).

All your tag management data is stored in the `gitstars.json` file, meaning that all your tag management operations are modifying the file, no database, everything on github and yours.

However, every time you use the github API to get the management data relatively slowly, and the data you get from the github API has a 60-second cache (check the Response Header Cache-Control field). Which means you refresh the page after you've modified the management data will find that the data is still before the amendment, for which I have e-mail asking github how to cancel the cache, the reply is unable to cancel ...

![github-api-replay-cache-control](http://oh8wftuto.bkt.clouddn.com/github-api-replay-cache-control.jpg)

So in order to solve the experiential problem here, it reminds me of an optimization that should be done without the above problem:

**Synchronize management data in localStorage**

This is necessary, gitstars not only did, and also done a perfect exception / error rollback processing, which you do not need to care about. Not only your management data, and also some other immutable data will be stored in the localStorage as well, avoiding getting the content from the github API each time it is opened, which also speeds up page content loading.

Synchronization of management data stored in localStorage can cause a problem: **Multi-client data is not synchronized**

So for the data to be correct, must obtain the data remotely from each visit to gitstars and then compare it with the local data. Lastly, change the time value, updating the local data to the remote data only if the remote data time value is greater than the local time value.

## LICENSE

MIT
