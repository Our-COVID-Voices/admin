<template>
  <gov-width-container>
    <gov-breadcrumbs :items="breadcrumbs" />

    <gov-main-wrapper>
      <gov-grid-row>
        <gov-grid-column-two-thirds>
          <gov-heading-l>Settings</gov-heading-l>

          <gov-body>
            MODERATORS: please do not alter any of the setting below without
            being authorised to do so by National Voices.
          </gov-body>
        </gov-grid-column-two-thirds>
      </gov-grid-row>

      <gov-grid-row>
        <gov-grid-column-full>
          <gov-tabs :tabs="tabs">
            <nuxt-child />
          </gov-tabs>
        </gov-grid-column-full>
      </gov-grid-row>
    </gov-main-wrapper>
  </gov-width-container>
</template>

<script>
import GovBody from '~/components/gov/Body.vue'
import GovBreadcrumbs from '~/components/gov/Breadcrumbs.vue'
import GovGridColumnFull from '~/components/gov/GridColumnFull.vue'
import GovGridColumnTwoThirds from '~/components/gov/GridColumnTwoThirds.vue'
import GovGridRow from '~/components/gov/GridRow.vue'
import GovHeadingL from '~/components/gov/HeadingL.vue'
import GovMainWrapper from '~/components/gov/MainWrapper.vue'
import GovTabs from '~/components/gov/Tabs.vue'
import GovWidthContainer from '~/components/gov/WidthContainer.vue'

export default {
  authenticated: true,

  components: {
    GovBody,
    GovBreadcrumbs,
    GovGridColumnFull,
    GovGridColumnTwoThirds,
    GovGridRow,
    GovHeadingL,
    GovMainWrapper,
    GovTabs,
    GovWidthContainer
  },

  data() {
    return {
      breadcrumbs: [
        {
          text: 'Dashboard',
          url: { name: 'index' }
        },
        {
          text: 'Settings'
        }
      ],
      tabs: [
        {
          text: 'Notifications',
          url: { name: 'settings-index-notifications' }
        },
        {
          text: 'Tags',
          url: { name: 'settings-index-tags' }
        },
        {
          text: 'Audit Logs',
          url: { name: 'settings-index-audit-logs' }
        },
        {
          text: 'CMS',
          url: { name: 'settings-index-cms' }
        }
      ]
    }
  },

  watch: {
    $route: {
      immediate: true,
      deep: true,
      /* eslint-disable object-shorthand */
      /* eslint-disable prettier/prettier */
      handler: function (to) {
        if (to.name === 'settings') {
          this.$router.push({ name: 'settings-index-notifications' })
        }
      }
      /* eslint-enable object-shorthand */
      /* eslint-enable prettier/prettier */
    }
  }
}
</script>
