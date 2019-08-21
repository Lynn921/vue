<template>
  <a-layout id="components-layout-demo-top-side-2">
    <a-layout-sider :style="setStyle">
      <a-menu :defaultSelectedKeys="['/project/analysys']" theme="dark">
        <!--<template v-for="item in menus">-->
          <!--<a-menu-item v-if="!item.children" :key="item.path">-->
            <!--<a-icon type="pie-chart" />-->
            <!--<span>{{item.title}}</span>-->
          <!--</a-menu-item>-->
          <!--<sub-menu v-else :menu-info="item" :key="item.key"/>-->
        <!--</template>-->
        <a-menu-item key="/project/analysys">
          <a-icon type="home" />
          <span>首页</span>
          </a-menu-item>
      </a-menu>
    </a-layout-sider>
    <a-layout style="padding: 0 24px 24px">
      <a-layout-content :style="{ background: '#fff', padding: '24px', margin: 0, minHeight: '280px' }">
        <div class="home_content_header">
          <a-radio-group :value="size" @change="handleSizeChange">
            <a-radio-button value="project">项目</a-radio-button>
            <a-radio-button value="projectGroup">项目群</a-radio-button>
          </a-radio-group>
        </div>
        <div class="home_content">
          <div class="project_card">
            <div class="card_header">
              <div class="header-left">
                <a-icon type="slack" class="iconfont_card" />
                <span>D - 软件研发类</span>
              </div>
              <div class="header-right">
                <span>活跃</span>
              </div>
            </div>
            <div class="card_content">
              <p>CMDB</p>
              <p @click="enterProject">cmdb</p>
            </div>
          </div>
        </div>
        <div class="project_table">
          <el-table  :data="dataSource" style="width: 100%" :header-row-style="headerStyle" :row-style="rowStyle">
            <el-table-column prop="code" label="项目编号"></el-table-column>
            <el-table-column prop="name" label="项目名称"></el-table-column>
            <el-table-column prop="type" label="项目类型"></el-table-column>
            <el-table-column prop="state" label="状态"></el-table-column>
          </el-table>
        </div>
      </a-layout-content>
    </a-layout>
  </a-layout>
</template>

<script>
  import SideMenu from '@/components/menu/SideMenu'
  import { mixin, mixinDevice } from '@/utils/mixin.js'
  import { mapState, mapActions } from 'vuex'
  import ALayoutSider from 'ant-design-vue/es/layout/Sider'

  export default {
    name: "Analysis",
    components: {
      ALayoutSider,
      SideMenu
    },
    mixins: [mixin, mixinDevice],
    computed: {
      ...mapState({
        // 主路由
        mainRouters: state => state.permission.addRouters,
        // 后台菜单
        permissionMenuList: state => state.user.permissionList
      }),
      setStyle () {
        let style = {
          'height': document.body.clientHeight - 59 + 'px'
        }
        return style
      }
    },
    data() {
      return {
        menus: [],
        size: 'project',
        dataSource: [{
          id: 1,
          code: 'cmdb',
          name: 'cmdb',
          type: 'D-软件研发类',
          state: '活跃',
          stateCode: '1'
        }]
      }
    },
    created() {
      // this.menus = this.permissionMenuList
      this.menus.push(this.permissionMenuList[0])
    },
    methods: {
      ...mapActions(['changeProject']),
      headerStyle () {
        let style = {
          'font-size': '12px',
          'color': '#909399'
        }
        return style
      },
      rowStyle () {
        let style = {
          'font-size': '12px',
          'color': '#606266'
        }
        return style
      },
      handleSizeChange (e) {
        this.size = e.target.value
      },
      enterProject () {
        this.$router.push({name: 'dashboard', query:{id: 11111111}})
      }
    }
  }
</script>

<style lang="scss" scoped>
  .home_content_header {
    margin-bottom: 20px;
  }
  .home_content {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    .project_card {
      width: 360px;
      height: 200px;
      border-radius: 6px;
      overflow: hidden;
      background: #778899;
      margin: 0 20px 20px 0;
      .card_header {
        height: 50px;
        border-bottom: 1px solid #fff;
        color: #fff;
        font: 16px/50px '';
        display: flex;
        justify-content: space-between;
        justify-items: center;
        padding: 0 20px;
        .header-left {
          .iconfont_card {
            font-size: 28px;
            vertical-align: middle;
            margin: -3px 8px 0 0;
          }
        }
      }
      .card_content {
        padding: 20px;
        p {
          color: #fff;
          margin: 0;
          &:first-child {
            font: 18px/36px '';
            margin-bottom: 14px;
          }
          &:last-child {
            font: 800 28px/28px '';
            cursor: pointer;
          }
        }
      }
    }
  }
  .project_table {
    padding-top: 20px;
  }
</style>