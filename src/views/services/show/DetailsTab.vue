<template>
  <div>
    <gov-heading size="l">Details</gov-heading>
    <gov-table>
      <template slot="body">
        <gov-table-row>
          <gov-table-header top scope="row"
            >Name of {{ service.type }}</gov-table-header
          >
          <gov-table-cell>{{ service.name }}</gov-table-cell>
        </gov-table-row>
        <gov-table-row>
          <gov-table-header top scope="row"
            >Organisation for {{ service.type }}</gov-table-header
          >
          <gov-table-cell>{{ service.organisation.name }}</gov-table-cell>
        </gov-table-row>
        <gov-table-row>
          <gov-table-header top scope="row"
            >{{ service.type | ucfirst }} website address</gov-table-header
          >
          <gov-table-cell break>{{ service.url }}</gov-table-cell>
        </gov-table-row>
        <gov-table-row>
          <gov-table-header top scope="row"
            >{{ service.type | ucfirst }} logo</gov-table-header
          >
          <gov-table-cell>
            <img
              :src="
                apiUrl(
                  `/services/${service.id}/logo.png?v=${service.updated_at}`
                )
              "
              :alt="`${service.type} logo`"
              class="ck-logo"
            />
          </gov-table-cell>
        </gov-table-row>
        <gov-table-row>
          <gov-table-header top scope="row"
            >Summary of {{ service.type }}</gov-table-header
          >
          <gov-table-cell>{{ service.intro }}</gov-table-cell>
        </gov-table-row>
        <gov-table-row>
          <gov-table-header top scope="row"
            >{{ service.type | ucfirst }} description</gov-table-header
          >
          <gov-table-cell v-html="toHtml(service.description)" />
        </gov-table-row>
        <gov-table-row>
          <gov-table-header top scope="row">Offerings</gov-table-header>
          <gov-table-cell>
            <gov-list v-if="service.offerings.length > 0" bullet>
              <li
                v-for="{ offering, order } in service.offerings"
                :key="`ServiceOffering::${order}`"
              >
                {{ offering }}
              </li>
            </gov-list>
            <template v-else>None</template>
          </gov-table-cell>
        </gov-table-row>
        <gov-table-row>
          <gov-table-header top scope="row">Status</gov-table-header>
          <gov-table-cell
            v-html="service.status === 'active' ? 'Enabled' : 'Disabled'"
          />
        </gov-table-row>
        <gov-table-row>
          <gov-table-header top scope="row"
            >Gallery items ({{ imageUrls.length }})</gov-table-header
          >
          <gov-table-cell style="width: 50%;">
            <ck-carousel v-if="imageUrls.length > 0" :image-urls="imageUrls" />
            <gov-body v-else>-</gov-body>
          </gov-table-cell>
        </gov-table-row>
        <gov-table-row>
          <gov-table-header top scope="row">Tags</gov-table-header>
          <gov-table-cell>
            <gov-list v-if="service.tags.length > 0" bullet>
              <li
                v-for="(tag, index) in service.tags"
                :key="`ServiceTag::${index}`"
              >
                {{ tag.label }}
              </li>
            </gov-list>
            <template v-else>None</template>
          </gov-table-cell>
        </gov-table-row>
      </template>
    </gov-table>
  </div>
</template>

<script>
import CkCarousel from '@/components/Ck/CkCarousel'

export default {
  name: 'DetailsTab',

  components: { CkCarousel },

  props: {
    service: {
      type: Object,
      required: true,
    },
  },

  computed: {
    imageUrls() {
      return this.service.gallery_items.map(galleryItem => galleryItem.url)
    },
  },
}
</script>
