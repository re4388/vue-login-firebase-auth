# Vue-auth

## original author and source
1. fork from: [Atanda1/vue-auth](https://github.com/Atanda1/vue-auth)
2. tutorial: [Tackling Authentication With Vue Using RESTful APIs | CSS-Tricks](https://css-tricks.com/tackling-authentication-with-vue-using-restful-apis/)


## Learning Points:
1. Commonet Evnet flow: Event(click in .vue) -dispatch-> actions (store.js) -commi-> mutation(store.js) -change-> state(store.js)
2. log inside your store.js action funciton, like logout, 除了 commit mutaiton外，還需要清楚資料（這裡是放在local storage）和route到logout的頁面（這裡用vue-router的指令：router.replace('/')）
3. 也在store.js設定了一個ifAuthenticated變數，讓header.vue可以透過computed去條件渲染要顯示已經登入和還沒登入的不同選項。
4. welcome組件很簡單，就是透過router link可以轉到登入和註冊兩個組件，註冊組件(signup)有input form，可輸入mail, name, pass，可以submit, 然後dispath`singup` with payload 到store.js。登入組件也是一個form，也上註冊類似，dispatch表單到store.js.
5. 後端透過firebase SDK，像是sinup action, 先發post with API key, 拿到回傳的user id和token, 存到local storage，轉到登入後應該到的頁面。sign in action和singup基本上是一樣的，用axios拿post拿到回傳的toekn和id, 後續是存到本機，然後轉入頁面。
6. 另外也有做auto login的功能。會去拿拿看local storage是否有token, 沒有就不會autologin, 有的話，就也拿user id然後登入。
7. 最後router那邊有個處理要留意。要進入login的人才可以進入的區域前，這邊是dashboard, 要用before enter，這個call back主要是再轉入這個路徑前，先確認store.js的狀態是否有token, 有的話才讓你進入。


## 後端相關知識學習
1.1 https://firebase.google.com/docs/auth
1.2 https://stackoverflow.com/questions/17000835/token-authentication-vs-cookies
1.3 https://zhuanlan.zhihu.com/p/38942172
1.4 https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/546417/
1.5 https://blog.yorkxin.org/2013/09/30/oauth2-1-introduction.html
