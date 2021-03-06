<template lang="pug">
  v-navigation-drawer(
    app
    v-model="appDrawer"
    :disable-route-watcher="!routeWatcher"
  )
    div.pa-5.text-xs-center
      v-avatar(size="68" tile).mb-5
        img(src="/static/v.png" alt="Logo")
      img(
        src="https://vuetifyjs.com/static/doc-images/backers/lmax-exchange.png"
        alt="Sponsor"
        width="80%"
      )
    v-container(fluid)
      v-select(
        :items="['pre-release 0.16.0']"
        value="pre-release 0.16.0"
        solo
      ).mb-4
      v-select(
        autocomplete
        solo
        append-icon="search"
      ).mb-5
    v-list(dense)
      template(v-for="item in items")
        v-list-group(v-if="item.items" v-bind:group="item.group" no-action)
          v-list-tile(slot="item" ripple)
            v-list-tile-content
              v-list-tile-title {{ item.title }}
          v-list-tile(
            v-for="subItem in item.items" v-bind:key="subItem.title"
            v-bind="{ \
              to: !subItem.target ? subItem.href : null, \
              href: subItem.target && subItem.href \
            }"
            ripple
            v-bind:disabled="subItem.disabled"
            v-bind:target="subItem.target"
          )
            v-list-tile-content.pl-3
              v-list-tile-title {{ subItem.title }}
            v-list-tile-action(v-if="subItem.action")
              v-icon(dark :class="[subItem.actionClass || 'success--text']") {{ subItem.action }}
        v-subheader(v-else-if="item.header" dark) {{ item.header }}
        v-divider(v-else-if="item.divider")
        v-list-tile(
          v-bind="{ \
            to: !item.target ? item.href : null, \
            href: item.target && item.href \
          }"
          ripple
          v-bind:disabled="item.disabled"
          v-bind:target="item.target"
          rel="noopener"
          v-else
        )
          v-list-tile-content
            v-list-tile-title {{ item.title }}
          v-list-tile-action(v-if="item.subAction")
            v-icon(dark class="success--text") {{ item.subAction }}
          v-chip(
            v-else-if="item.chip"
            label
            small
            class="caption blue lighten-2 white--text mx-0"
          ) {{ item.chip }}
</template>

<script>
  import { mapState } from 'vuex'

  export default {
    data: () => ({
      items: [
        {
          title: 'Getting Started',
          group: '/getting-started',
          items: [
            { href: '/getting-started/quick-start', title: 'Quick Start' },
            { href: '/getting-started/starter-templates', title: 'Starter Templates' },
            { href: '/getting-started/why-vuetify', title: 'Why Vuetify?' },
            { href: '/getting-started/frequently-asked-questions', title: 'Frequently asked questions' },
            { href: '/getting-started/sponsors-and-backers', title: 'Sponsors and backers' },
            { href: '/getting-started/contributing', title: 'Contributing' },
            { href: '/getting-started/roadmap', title: 'Roadmap' }
          ]
        },
        {
          title: 'Application Layout',
          group: 'layout',
          items: [
            { href: '/layout/pre-defined', title: 'Pre-defined', action: 'star', actionClass: 'white--text' },
            { href: '/layout/grid', title: 'Grid & breakpoints' },
            { href: '/layout/spacing', title: 'Spacing' },
            { href: '/layout/alignment', title: 'Alignment' },
            { href: '/layout/display', title: 'Display' },
            { href: '/layout/elevation', title: 'Elevation' },
            { href: '/layout/sandbox', title: 'Sandbox' }
          ]
        },
        {
          title: 'Base Styles',
          group: '/style',
          items: [
            { href: '/style/colors', title: 'Colors' },
            { href: '/style/theme', title: 'Theme' },
            { href: '/style/typography', title: 'Typography' },
            { href: '/style/content', title: 'Content' }
          ]
        },
        {
          title: 'Motion & Transitions',
          group: 'motion',
          items: [
            { href: '/motion/transitions', title: 'Transitions' }
          ]
        },
        {
          title: 'UI Components',
          group: '/components',
          items: [
            { href: '/components/alerts', title: 'Alerts' },
            {
              title: 'Form Components',
              group: '/components/form-components',
              items: [
                { href: '/components/form-components/forms', title: 'Forms' }
              ]
            }
          ]
        }
      ]
    }),
    computed: {
      ...mapState({
        routeWatcher: state => state.routeWatcher
      }),
      appDrawer: {
        get (state) {
          return this.$store.state.appDrawer
        },
        set (val) {
          this.$store.commit('app:drawer', val)
        }
      }
    }
  }
</script>
