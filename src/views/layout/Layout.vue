<template>
	<div class="app-wrapper" :class="{hideSidebar:!sidebar.opened}">
			<sidebar class="sidebar-wrapper"></sidebar>

		<div class="main-container">
			<navbar></navbar>
			<app-main></app-main>
		</div>
	</div>
</template>

<script>
  import { Navbar, Sidebar, AppMain } from 'views/layout';

  export default {
    name: 'layout',
    components: {
      Navbar,
      Sidebar,
      AppMain
    },
    computed: {
      sidebar() {
        return this.$store.state.app.sidebar;
      }
    }
  }
</script>

<style rel="stylesheet/scss" lang="scss">
@import "src/styles/mixin.scss";
.app-wrapper {
	@include clearfix;
	position: relative;
	height: 100%;
	width: 100%;
	&.hideSidebar {
		.sidebar-wrapper {
			// transform: translate(-140px, 0);
			width: 50px;
			.el-icon-arrow-down {
				// display: none!important;
				opacity: 0;
			}
			&:hover {
				transform: translate(0, 0);
			}
			.submenu-title,
			.submenu-title-noDropdown {
				display: none!important;
			}
			.el-menu{
				height: 0px;
				display: none;
			}
		}
		.submenu-item {

			&:hover {

				.submenu-title-noDropdown {
					display: block!important;
					background: #1f2d3d;
					position: absolute;
					left: 50px;
					top: 0px;
					padding: 0px 20px;
				}
				.el-menu {
					display: block!important;
					position: absolute;
					height: auto;
					left: 50px;
					top: 0px;
					overflow: hidden;
				}
				&.el-submenu{
					.el-submenu{
						.submenu-title{
							display: block!important;
						}
						.el-icon-arrow-down{
							opacity: 1;
						}
						.el-menu{
							height: 0px;
							position: relative;
							left: 0;
						}
						&.is-opened{
								.el-menu{
										height: auto;
										display: block!important;
								}
						}
					}
				}
			}
		}
		.main-container {
			margin-left: 40px;
		}
	}
	.submenu-item {
	display: block;
	position: relative;
	}
	.sidebar-wrapper {
		width: 180px;
		position: fixed;
		top: 0;
		bottom: 0;
		left: 0;
		z-index: 1001; // overflow: hidden;
		transition: all .28s ease-out;
	}
	.main-container {
		min-height: 100%;
		transition: all .28s ease-out;
		margin-left: 180px;
	}
}

</style>
