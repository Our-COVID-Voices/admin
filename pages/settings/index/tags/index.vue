<template>
  <div>
    <gov-heading-m>Tags</gov-heading-m>

    <gov-body>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Commodi,
      voluptate. Quae eius, fuga excepturi enim quam veritatis quidem nesciunt
      omnis aliquam dicta provident laboriosam alias suscipit? Soluta ducimus
      incidunt delectus?
    </gov-body>

    <gov-button type="button" @click="onAddTag">Add tag</gov-button>

    <custom-loader v-if="loadingTags" />

    <!-- Parent tags -->
    <gov-list v-else bullet>
      <li
        v-for="(parentTag, parentIndex) in tags"
        :key="`page::settings::tags::parentTag::${parentIndex}`"
      >
        <gov-link
          :url="{
            name: 'settings-index-tags-id',
            params: { id: parentTag.id }
          }"
          no-visited-state
        >
          {{ parentTag.name }}
        </gov-link>

        <!-- Chil tags -->
        <gov-list v-if="parentTag.children !== undefined" bullet>
          <li
            v-for="(childTag, childIndex) in parentTag.children"
            :key="
              `page::settings::tags::parentTag::${parentIndex}::childTag::${childIndex}`
            "
          >
            <gov-link
              :url="{
                name: 'settings-index-tags-id',
                params: { id: childTag.id }
              }"
              no-visited-state
            >
              {{ childTag.name }}
            </gov-link>
          </li>
        </gov-list>
      </li>
    </gov-list>
  </div>
</template>

<script>
import CustomLoader from '~/components/custom/Loader.vue'
import GovBody from '~/components/gov/Body.vue'
import GovButton from '~/components/gov/Button.vue'
import GovHeadingM from '~/components/gov/HeadingM.vue'
import GovLink from '~/components/gov/Link.vue'
import GovList from '~/components/gov/List.vue'
import Tag from '~/models/Tag'

export default {
  authenticated: true,

  components: {
    CustomLoader,
    GovBody,
    GovButton,
    GovHeadingM,
    GovLink,
    GovList
  },

  data() {
    return {
      loadingTags: false,
      tags: null
    }
  },

  created() {
    this.fetchTags()
  },

  methods: {
    async fetchTags() {
      this.loadingTags = true

      this.tags = await Tag.hierarchy()

      this.loadingTags = false
    },

    onAddTag() {
      this.$router.push({ name: 'settings-index-tags-create' })
    }
  }
}
</script>
