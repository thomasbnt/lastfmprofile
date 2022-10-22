[![Make with VueJS](https://img.shields.io/badge/-Make%20with%20Vue.js-4fc08d?&logo=vuedotjs&logoColor=white)](https://vuejs.org/)
![GitHub last commit](https://img.shields.io/github/last-commit/thomasbnt/lastfmprofile)
[![Discord](https://img.shields.io/discord/367753345575944221?color=%237289DA&label=Discord%20server&logo=discord&logoColor=white)](https://thomasbnt.dev/discord)
[![Twitter Follow](https://img.shields.io/twitter/follow/Thomasbnt_?color=%231DA1F2&label=Follow%20me&logo=Twitter&logoColor=white)](https://twitter.com/Thomasbnt_)
[![Last.fm profile](https://img.shields.io/badge/follow%20me%20on-Last.fm-af0000)](https://www.last.fm/user/thomasbnt)

# Getting data

An example to get your data from the API of **Last.fm**. Work with **VueJS**, **fetch** and the **[API of Last.fm](https://www.last.fm/api)**.

> **Note**
>
> [See the preview of this project here →](https://lastfmprofile.netlify.app/)

[![Preview of this project](https://user-images.githubusercontent.com/14293805/197307013-a8faf54f-99f9-4aee-94a1-05f0767e5168.png)](https://lastfmprofile.netlify.app/)


> **Note**
>
> More projects like that ?  [Check this list](https://github.com/stars/thomasbnt/lists/created-api-stuff).
>
> [![See the list of awesome projects with an API](https://img.shields.io/badge/See%20the%20list%20of%20awesome%20projects%20with%20an%20API%20→-informational?style=for-the-badge)](https://github.com/stars/thomasbnt/lists/created-api-stuff)


## How to setup the project ?

Edit the [`.env.example`](.env.example) into `.env` and add your **Last.fm API key**.

```bash
# .env
VITE_USERNAME=thomasbnt
# Caution : VITE_ prefix is required, and he show to the client your key.
VITE_LASTFM_KEY=YOUR_API_KEY
```

### And how to get the Last.fm API key ?

You can get your **Last.fm API key** [here](https://www.last.fm/api/account/create).


## The behind the scene

This project use **Vue.js** and **Vite**. Also, a bit of **SASS**, and **[Lucide](https://lucide.dev/)** for icons.
The font family is [Lato](https://fonts.google.com/specimen/Lato).
____
## How to develop this project

### Project setup
```bash
yarn install
```

### Compiles and hot-reloads for development
```bash
yarn serve
```

### Compiles and minifies for production
```bash
yarn build
```

### Lints and fixes files
```bash
yarn lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
