<template>
    <div class="main">
        <el-container>
            <el-aside>
                <new-left/>
            </el-aside>
            <el-main >
                <transition enter-active-class="animated fadeIn" class="trans">
                    <router-view></router-view>
                </transition>
            </el-main>
        </el-container>
    </div>
</template>
<script>
import LeftNav from "./leftNav.vue";
import UserDetails from "./User/UserDetails.vue";
import NewLeft from "./NewLeft.vue";
export default {
    data() {
        return {
            Data: {}
        };
    },
    components: {
        LeftNav,
        UserDetails,
        NewLeft
    },
    methods: {
        test() {
            this.$axios
                .get("/api/v1.0/allworks")
                .then(res => {
                    this.Data = res.data;
                    console.log(res.data.allworks);

                    //this.check()
                })
                .catch(() => {
                    console.log("调用失败");
                });
        },
        check() {
            this.Data = this.Data.replace(/\'/g, '"');
            console.log(this.Data);
        }
    }
};
</script>
<style scoped>
.trans {
    animation-duration: 0.5s;
}
.aside {
    flex: none;
    width: 220px;
}
.main {
    /* flex: auto; */
    background:#F2F2F2;
}
.content {
    flex: auto;
    display: flex;
}
.box{
    justify-content: center
}
</style>
