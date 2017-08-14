<template>
    <el-row class = "container">
        <el-col span="24" class=" header grid-content bg-purple-dark">
            <el-col span="10" class="logo" :class="collapsed?logo-collapsed-width:logo-width">
                {{collapsed?'':sysName}}
            </el-col>
            <el-col :span="20">
                <div class="tools" @click.prevent="collapsed">
                    <i class="fa fa-align-justify"></i>
                </div>
            </el-col>

            <el-col :span="10">
                    <i class="fa fa-align-justify"></i>
                    <i class="el-icon-edit" color="bule"></i>
                    <i class="el-icon-share"></i>
                    <i class="el-icon-delete"></i>
                    <el-button type="primary" icon="search" v-on:click="getBlog">测试</el-button>
                </div>
            </el-col>
        </el-col>
    </el-row>
</template>
<script>
    export default{
        data() {
            return {
                sysName:'VUEADMIN',
                collapsed:false,
                sysUserName: '',
                sysUserAvatar: '',
                form: {
                    name: '',
                    region: '',
                    date1: '',
                    date2: '',
                    delivery: false,
                    type: [],
                    resource: '',
                    desc: ''
                }
            }
        },
        methods: {
            methords:{
                getBlog(){
                    alert("test");
                }
            },
            onSubmit() {
                console.log('submit!');
            },
            handleopen() {
                //console.log('handleopen');
            },
            handleclose() {
                //console.log('handleclose');
            },
            handleselect: function (a, b) {
            },
            //退出登录
            logout: function () {
                var _this = this;
                this.$confirm('确认退出吗?', '提示', {
                    //type: 'warning'
                }).then(() => {
                    sessionStorage.removeItem('user');
                    _this.$router.push('/login');
                }).catch(() => {

                });


            },
            //折叠导航栏
            collapse:function(){
                this.collapsed=!this.collapsed;
            },
            showMenu(i,status){
                this.$refs.menuCollapsed.getElementsByClassName('submenu-hook-'+i)[0].style.display=status?'block':'none';
            }
        },
        mounted() {
            var user = sessionStorage.getItem('user');
            if (user) {
                user = JSON.parse(user);
                this.sysUserName = user.name || '';
                this.sysUserAvatar = user.avatar || '';
            }

        }
    }
</script>

<style scope lang="scss">
    @import '~scss_vars';
    @import url("//unpkg.com/element-ui/lib/theme-default/index.css");

    .container{
        position:absolute;
        top:0px;
        bottom:0px;
        width:100%;
        .header{
            height: 60px;
            line-height: 60px;
            background: $color-primary;
            color:#fff;
            .logo {
                height:60px;
                font-size: 22px;
                padding-left:20px;
                padding-right:20px;
                border-color: rgba(238,241,146,0.3);
                border-right-width: 1px;
                border-right-style: solid;
                img {
                    width: 40px;
                    float: left;
                    margin: 10px 10px 10px 18px;
                }
                .txt {
                    color:#fff;
                }
            }
            .logo-width{
                width:230px;
            }
            .logo-collapse-width{
                width:60px
            }
            .tools{
                 padding: 0px 23px;
                 width:14px;
                 height: 60px;
                 line-height: 60px;
                 cursor: pointer;
             }
        }
        .grid-content {
            border-radius: 4px;
            min-height: 60px;
        }
        .bg-purple-dark {
            background: #99a9bf;
        }
    }
</style>