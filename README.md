# Vue-Vuex-login-firebase-auth

## original author and source
1. fork from: [Atanda1/vue-auth](https://github.com/Atanda1/vue-auth)
2. tutorial: [Tackling Authentication With Vue Using RESTful APIs | CSS-Tricks](https://css-tricks.com/tackling-authentication-with-vue-using-restful-apis/)


## 學習綱要
- 使用firebase auth / username password
- Vue 整合fireabase auth SDK and Vuex 實現login, logout, routing, autologin, localstorage


## Learning Points:
1. Commonet Evnet flow: Event(click in .vue) -dispatch-> actions (store.js) -commit-> mutation(store.js) -change-> state(store.js)
2. For example, inside store.js action funciton, like `logout`, 除了 commit `mutaiton` 外，還需要清理資料（這裡是放在local storage）和 route到logout的頁面（這裡用vue-router的指令：router.replace('/')）
3. 也在store.js設定了一個`ifAuthenticated`變數，讓`header.vue`可透computed去條件渲染要顯示已經登入和還沒登入的不同選項。
4. `welcome.vue`很簡單，就是透過router link 轉到登入和註冊兩個組件，註冊組件(signup)有 input form，可輸入mail, name, pass，可submit, 然後dispath`singup` with payload 到store.js。登入組件也是一個form，操作和註冊一樣.
5. 後端透過firebase SDK，像是sinup action, 先發post with API key, 拿到回傳的user id和token, 存到local storage，轉到登入後應該到的頁面。signin action和singup基本上是一樣的，用axios拿post拿到回傳的toekn和id, 後續是存到本機，然後轉入頁面。
6. 另外也有做auto login的功能。確認local storage是否有token, 沒有就return, 有的話，就拿user id然後登入。
7. 最後router那邊有個處理。用before enter，這個call back主要是再轉入這個路徑前，先確認store.js的狀態是否有token, 有的話才讓你進入。


## 後端相關知識學習
1. [Cookies vs. Tokens: The Definitive Guide - DZone Integration](https://dzone.com/articles/cookies-vs-tokens-the-definitive-guide)
2. [Token Authentication vs. Cookies](https://stackoverflow.com/questions/17000835/token-authentication-vs-cookies)
3. [不要用JWT替代session管理（上）：全面了解Token,JWT,OAuth,SAML,SSO](https://zhuanlan.zhihu.com/p/38942172)
