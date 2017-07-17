<template>
	<div>
		<template v-for="item in routes">
			<router-link class='submenu-item' v-if="!item.hidden&&item.noDropdown&&item.children.length>0" :to="item.path+'/'+item.children[0].path">
				<span :index="item.path+'/'+item.children[0].path">
					<icon-svg v-if='item.icon' :icon-class="item.icon"></icon-svg><span class='submenu-title-noDropdown'>{{item.children[0].name}}</span>
				</span>
			</router-link>

			<el-submenu class='submenu-item' :index="item.name" v-if="!item.noDropdown&&!item.hidden">
				<template slot="title">
					<icon-svg v-if='item.icon' :icon-class="item.icon"></icon-svg><span class='submenu-title'>{{item.name}}</span>
				</template>
				<template v-for="child in item.children" v-if='!child.hidden'>
					<sidebar-item class='menu-indent' v-if='child.children&&child.children.length>0' :routes='[child]'> </sidebar-item>
					<router-link  v-else class="menu-indent" :to="item.path+'/'+child.path">
						<span :index="item.path+'/'+child.path">
							{{child.name}}
						</span>
					</router-link>
				</template>
			</el-submenu>
		</template>
	</div>
</template>

<script>
  export default {
    name: 'SidebarItem',
    props: {
      routes: {
        type: Array
      }
    }
  }
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
	.svg-icon {
		margin-right: 15px;
	}

	.hideSidebar .menu-indent {
		display: block;
		text-indent: 10px;
	}
</style>

