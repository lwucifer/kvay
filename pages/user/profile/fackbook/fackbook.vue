<template>
    <view>
<!--        <web-view :src="url"></web-view>-->
<!--        <a :href="url" target="_blank" class="btn">Login with facebook</a>-->
        <iframe :target="_top" src="https://vn.dotconnect.io/authorize_api/getDatasourcePageUrl?website=facebook&report_task_token=0162f58fb7dc491485aeadb6cba61bdc&api_key=5a6114f08251412da5a2dc5c0ce03087&client_url=aHR0cDovL2FwaS5raG92YXkuY29tL2FwaS9hY3QvbWluZS9jbC9jc3RnL2NvbXBsZXRlQ2VydGlmaWNhdGlvbi5odG0/dXNlcklkPTQxMjg5JnR5cGU9U09DSUF&Mredirect_uri=true" style="width:100%; height:100%;"></iframe>
    </view>
</template>

<script>
    import {
        mapState,
        mapMutations
    } from 'vuex'

    import util from '@/util/util.js'
    import appService from '@/services/application.js'
    import userService from '@/services/user.js'

    export default {
        data() {
            return {
                type: 'SOCIAL',
                client: util.getClient(),
                url: "pages/loading/loading"
            }
        },
        components: {
        },
        computed: {
            ...mapState(["userId", "auth"])
        },
        methods: {
            ...mapMutations(["pageAuth"]),
            onInit() {
                var that = this;
                if (that.auth.faceState == '10') {
                    appService.confirmdatas({...that.$data, userId: that.userId}, function (obj, msg, code) {
                        if (!util.isEmpty(obj.url)) {
                            that.url = obj.url;
                            //window.open(obj.url, '_blank');
                        }
                    });
                } else {
                    //window.history.back();
                }
            }
        },
        onLoad: function () {
            var that = this;
        },
        onShow: function () {
            var that = this;
            that.pageAuth({ callback: that.onInit });
        }
    }
</script>
<style>
</style>

