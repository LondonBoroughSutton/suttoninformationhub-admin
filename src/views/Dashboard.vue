<template>
  <gov-width-container>
    <vue-headful title="Sutton Information Hub - Dashboard" />

    <gov-main-wrapper>
      <gov-grid-row>
        <gov-grid-column width="two-thirds">
          <gov-heading size="xl">
            Welcome to the Sutton Information Hub admin portal
          </gov-heading>

          <gov-body size="l">
            From here, you can add and edit your pages on Sutton Information
            Hub, as well as manage referrals into your service. For any support,
            contact
            <gov-link :href="`mailto:${contactEmail}`">
              {{ contactEmail }}
            </gov-link>
            or view our
            <gov-link :to="{ name: 'help-index' }">help videos</gov-link>
          </gov-body>
        </gov-grid-column>
      </gov-grid-row>

      <gov-section-break size="l" />

      <gov-grid-row>
        <gov-grid-column width="one-half">
          <gov-heading size="l">Services</gov-heading>
          <gov-body>Add or edit your pages on Sutton Information Hub.</gov-body>
          <gov-button start :to="{ name: 'services-index' }">
            Go to services
          </gov-button>
          <gov-section-break size="m" />
        </gov-grid-column>

        <gov-grid-column width="one-half">
          <gov-heading size="l">Locations</gov-heading>
          <gov-body>View and edit service locations in the Borough.</gov-body>
          <gov-button start :to="{ name: 'locations-index' }">
            Go to locations
          </gov-button>
          <gov-section-break size="m" />
        </gov-grid-column>

        <gov-grid-column width="one-half">
          <gov-heading size="l">Referrals</gov-heading>
          <gov-body>View and respond to referrals to your service(s).</gov-body>
          <gov-button start :to="{ name: 'referrals-index' }">
            Go to referrals
          </gov-button>
          <gov-section-break size="m" />
        </gov-grid-column>

        <gov-grid-column width="one-half" v-if="auth.isGlobalAdmin">
          <gov-heading size="l">Organisations</gov-heading>
          <gov-body
            >Add or edit organisations on Sutton Information Hub.</gov-body
          >
          <gov-button start :to="{ name: 'organisations-index' }">
            Go to organisations
          </gov-button>
          <gov-section-break size="m" />
        </gov-grid-column>

        <gov-grid-column width="one-half">
          <gov-heading size="l">Users</gov-heading>
          <gov-body>View, add and edit users in your organisation.</gov-body>
          <gov-button start :to="{ name: 'users-index' }">
            Go to users
          </gov-button>
          <gov-section-break size="m" />
        </gov-grid-column>

        <gov-grid-column width="one-half" v-if="auth.isGlobalAdmin">
          <gov-heading size="l">Reports</gov-heading>
          <gov-body>
            Download reports of activity on Sutton Information Hub.
          </gov-body>
          <gov-button start :to="{ name: 'reports-index' }">
            Go to reports
          </gov-button>
          <gov-section-break size="m" />
        </gov-grid-column>

        <gov-grid-column width="one-half" v-if="auth.isGlobalAdmin">
          <gov-heading size="l">Pages</gov-heading>
          <gov-body>Manage pages on the platform.</gov-body>
          <gov-button start :to="{ name: 'pages-index' }">
            Go to pages
          </gov-button>
        </gov-grid-column>

        <gov-grid-column width="one-half" v-if="auth.isGlobalAdmin">
          <gov-heading size="l">Admin</gov-heading>
          <gov-body>Admin tools for maintaining the site.</gov-body>
          <gov-button start :to="{ name: 'admin-index' }">
            Go to admin
          </gov-button>
        </gov-grid-column>

        <gov-grid-column width="one-half" v-if="auth.isGlobalAdmin">
          <gov-heading size="l">Update Requests</gov-heading>
          <gov-body>View, approve and reject update requests.</gov-body>
          <gov-button start :to="{ name: 'update-requests-index' }">
            Go to update requests
          </gov-button>
        </gov-grid-column>
      </gov-grid-row>
    </gov-main-wrapper>
  </gov-width-container>
</template>

<script>
import Auth from '@/classes/Auth'

export default {
  name: 'Dashboard',

  data() {
    return {
      auth: Auth,
    }
  },
}
</script>
