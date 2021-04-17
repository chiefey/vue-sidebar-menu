<template>
  <div
    id="demo"
    :class="[{'collapsed' : collapsed}, {'onmobile' : isOnMobile}]"
  >
    <div class="demo">
      <div class="container">
        <router-view />
      </div>
      <sidebar-menu
        :menu="menu"
        :collapsed="collapsed"
        :theme="selectedTheme"
        :show-one-child="true"
        @toggle-collapse="onToggleCollapse"
        @item-click="onItemClick"
      />
      <div
        v-if="isOnMobile && !collapsed"
        class="sidebar-overlay"
        @click="collapsed = true"
      />
    </div>
  </div>
</template>

<script>
const separator = {
  template: `<hr style="border-color: rgba(0, 0, 0, 0.1); margin: 20px;">`
}

export default {
  name: 'App',
  data () {
    return {
      menu: [
        {
          header: true,
          title: 'Title Header',
          hiddenOnCollapse: true
        },
        {
          href: '/',
          title: 'Static Item 1',
          icon: 'fa fa-download'
        },
        {
          href: '/about',
          title: 'Static Item 2',
          icon: 'fa fa-code'
        },
        {
          href: '/page1',
          title: 'Dropdown 1',
          icon: 'fa fa-list-ul',
          child: [
            {
              href: '/page1/sub-page-1',
              title: 'Sub Page 01',
              icon: 'fa fa-file-alt'
            },
            {
              href: '/page1/sub-page-2',
              title: 'Sub Page 02',
              icon: 'fa fa-file-alt'
            },
            {
              href: '/page1/sub-page-3',
              title: 'Sub Page 01',
              icon: 'fa fa-file-alt'
            },
            {
              href: '/page1/sub-page-4',
              title: 'Sub Page 02',
              icon: 'fa fa-file-alt'
            },
            {
              href: '/page1/sub-page-5',
              title: 'Sub Page 01',
              icon: 'fa fa-file-alt'
            },
            {
              href: '/page1/sub-page-6',
              title: 'Sub Page 02',
              icon: 'fa fa-file-alt'
            },
            {
              href: '/page1/sub-page-7',
              title: 'Sub Page 01',
              icon: 'fa fa-file-alt'
            },
            {
              href: '/page1/sub-page-8',
              title: 'Sub Page 02',
              icon: 'fa fa-file-alt'
            },
            {
              href: '/page1/sub-page-9',
              title: 'Sub Page 01',
              icon: 'fa fa-file-alt'
            },
            {
              href: '/page1/sub-page-10',
              title: 'Sub Page 02',
              icon: 'fa fa-file-alt'
            },
            {
              href: '/page1/sub-page-11',
              title: 'Sub Page 01',
              icon: 'fa fa-file-alt'
            },
            {
              href: '/page1/dashboard',
              title: 'Dashboard',
              icon: 'fa fa-file-alt'
            },
            {
              href: '/page1/sub-page-13',
              title: 'Sub Page 01',
              icon: 'fa fa-file-alt'
            }
          ]
        },
        {
          href: '/page2',
          title: 'Dropdown 2',
          icon: 'fa fa-list-ul',
          child: [
            {
              href: '/page2/sub-page-1',
              title: 'Sub Page 01',
              icon: 'fa fa-file-alt'
            },
            {
              href: '/page2/sub-page-2',
              title: 'Sub Page 02',
              icon: 'fa fa-file-alt'
            },
             {
              href: '/page2/sub-page-3',
              title: 'Sub Page 01',
              icon: 'fa fa-file-alt'
            },
            {
              href: '/page2/sub-page-4',
              title: 'Sub Page 02',
              icon: 'fa fa-file-alt'
            },
             {
              href: '/page2/sub-page-5',
              title: 'Sub Page 01',
              icon: 'fa fa-file-alt'
            },
            {
              href: '/page2/sub-page-6',
              title: 'Sub Page 02',
              icon: 'fa fa-file-alt'
            },
             {
              href: '/page2/sub-page-7',
              title: 'Sub Page 01',
              icon: 'fa fa-file-alt'
            },
            {
              href: '/page2/sub-page-8',
              title: 'Sub Page 02',
              icon: 'fa fa-file-alt'
            }
          ]
        },
        {
          href: '/page3',
          title: 'Dropdown 3',
          icon: 'fa fa-list-ul',
          child: [
            {
              href: '/page3/sub-page-1',
              title: 'Sub Page 01',
              icon: 'fa fa-file-alt'
            },
            {
              href: '/page3/sub-page-2',
              title: 'Sub Page 02',
              icon: 'fa fa-file-alt'
            }
          ]
        },
      ],
      collapsed: false,
      themes: [
        {
          name: 'Default theme',
          input: ''
        },
        {
          name: 'White theme',
          input: 'white-theme'
        }
      ],
      selectedTheme: 'Default theme',
      isOnMobile: false
    }
  },
  mounted () {
    this.onResize()
    window.addEventListener('resize', this.onResize)
  },
  methods: {
    onToggleCollapse (collapsed) {
      console.log(collapsed)
      this.collapsed = collapsed
    },
    onItemClick (event, item, node) {
      console.log('onItemClick')
      // console.log(event)
      // console.log(item)
      // console.log(node)
    },
    onResize () {
      if (window.innerWidth <= 767) {
        this.isOnMobile = true
        this.collapsed = true
      } else {
        this.isOnMobile = false
        this.collapsed = false
      }
    }
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Source+Sans+Pro:400,600');

body,
html {
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Source Sans Pro', sans-serif;
  font-size: 18px;
  background-color: #f2f4f7;
  color: #262626;
}

#demo {
  padding-left: 350px;
  transition: 0.3s ease;
}
#demo.collapsed {
  padding-left: 50px;
}
#demo.onmobile {
  padding-left: 50px;
}

.sidebar-overlay {
  position: fixed;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  background-color: #000;
  opacity: 0.5;
  z-index: 900;
}

.demo {
  padding: 20px;
}

.container {
  max-width: 900px;
}

pre {
  font-family: Consolas, monospace;
  color: #000;
  background: #fff;
  border-radius: 2px;
  padding: 15px;
  line-height: 1.5;
  overflow: auto;
}
</style>
