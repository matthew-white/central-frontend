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
  <div v-if="form != null" id="form-settings">
    <div class="row">
      <div class="col-xs-6">
        <div class="panel panel-simple">
          <div class="panel-heading">
            <h1 class="panel-title">Form State</h1>
          </div>
          <div class="panel-body">
            <p>
              To set this Form&rsquo;s state, please visit the Project
              <router-link :to="projectPath('form-access')">
                <!-- eslint-disable-next-line vue/multiline-html-element-content-newline -->
                Form Access settings</router-link>.
            </p>
          </div>
        </div>
      </div>
      <div class="col-xs-6">
        <div class="panel panel-simple-danger">
          <div class="panel-heading">
            <h1 class="panel-title">Danger Zone</h1>
          </div>
          <div class="panel-body">
            <p>
              <button type="button" class="btn btn-danger"
                @click="showModal('deleteForm')">
                Delete this Form&hellip;
              </button>
            </p>
          </div>
        </div>
      </div>
    </div>
    <form-delete v-bind="deleteForm" @hide="hideModal('deleteForm')"
      @success="afterDelete"/>
  </div>
</template>

<script>
import FormDelete from './delete.vue';
import modal from '../../mixins/modal';
import routes from '../../mixins/routes';
import validateData from '../../mixins/validate-data';
import { requestData } from '../../store/modules/request';

export default {
  name: 'FormSettings',
  components: { FormDelete },
  mixins: [modal(), routes(), validateData()],
  data() {
    return {
      deleteForm: {
        state: false
      }
    };
  },
  // The component does not assume that this data will exist when the component
  // is created.
  computed: requestData(['form']),
  methods: {
    afterDelete(form) {
      this.$router.push(this.projectPath(), () => {
        this.$alert().success(`The Form "${form.nameOrId()}" was deleted.`);
      });
    }
  }
};
</script>

<style lang="scss">
#form-settings .panel-simple-danger .panel-body p {
  margin-bottom: 15px;
  margin-top: 10px;
  text-align: center;
}
</style>
