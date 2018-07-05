<template>
    <div id="login">
        ????????????????????
        <button v-on:click="naverLoginBtnClick">Add!!</button>
    </div>
</template>
<script>
console.log('login');
export default {
    name: 'login'
    ,data() {
        return {
            msg: 'Login'
        }
    }
    ,methods: {
        naverLoginBtnClick: function (e) {
            var clientId = "클라이언트ID";
            var redirectURI = "http://localhost:3000/weight-management/login/naver/callback";
            var state = "STATE";
            var api_url = 'https://nid.naver.com/oauth2.0/authorize?response_type=code&client_id=' + clientId + '&redirect_uri=' + redirectURI + '&state=' + state;
            this.$http.get(`${api_url}`)
            .then((result) => {
                console.log(result)
                this.posts = result.data
            })
        }
    }
}
</script>