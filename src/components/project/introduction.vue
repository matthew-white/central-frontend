<!--
Copyright 2017 ODK Central Developers
See the NOTICE file at the top-level directory of this distribution and at
https://github.com/getodk/central-frontend/blob/master/NOTICE.

This file is part of ODK Central. It is subject to the license terms in
the LICENSE file found in the top-level directory of this distribution and at
https://www.apache.org/licenses/LICENSE-2.0. No part of ODK Central,
including this file, may be copied, modified, propagated, or distributed
except according to the terms contained in the LICENSE file.
-->
<template>
  <modal :state="state" backdrop hideable @hide="$emit('hide')">
    <template slot="title">Introducing Projects</template>
    <template slot="body">
      <div class="modal-introduction">
        <p>ODK Central Beta v0.4 introduced <strong>Projects</strong>.</p>
        <p>
          Projects group <strong>Forms</strong> and <strong>App Users</strong>
          together to make them easier to organize and manage, both on this
          website and on your data collection device.
        </p>
        <p>
          For more information, please see
          <doc-link to="central-projects/">this help article</doc-link>.
        </p>
      </div>
      <div class="modal-actions">
        <button type="button" class="btn btn-primary" @click="$emit('hide')">
          Okay
        </button>
      </div>
    </template>
  </modal>
</template>

<script>
import DocLink from '../doc-link.vue';
import Modal from '../modal.vue';

export default {
  name: 'ProjectIntroduction',
  components: { DocLink, Modal },
  props: {
    state: {
      type: Boolean,
      default: false
    }
  }
};
</script>
