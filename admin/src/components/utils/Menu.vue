<template>
    <div class='util-menu'>
        <el-menu class="el-menu-vertical-demo" router :unique-opened='true' :default-active='$route.path'>
            <el-submenu v-for='menu in menus' :key='menu.id' :index='menu.url'>
                <template slot="title"><i :class="menu.icon || 'fa fa-circle'"></i><span>{{menu.name}}</span></template>
                <el-menu-item v-for='child in menu.childs' :key='child.id' 
                    :index='child.url' 
                    :route='{path: child.url}'>
                    <i class='fa fa-circle'></i>{{child.name}}
                </el-menu-item>
            </el-submenu>
        </el-menu>
    </div>
</template>

<script type="text/javascript">
import Request from '@/common/Request'
import Common from '@/common/Common'
export default {
    data() {
        return {
            menus: {},
        }
    }, 
    created() {
        var url= Request.createApi('/admin/menus')
        Request.get(url, res => {
            this.menus  = res['list']
        })
    }
}
</script>

<style lang="scss" scoped="" type="text/css">
.el-submenu .fa {
    vertical-align: middle;
    margin-right: 5px;
    width: 24px;
    text-align: center;
    font-size: 18px;
    margin-top: 2px;
}
.el-menu-item .fa {
    font-size: 14px;
    margin-top: -2px;
    width: 20px;
    // color: $--color-primary;
}
</style>
