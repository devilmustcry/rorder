<template lang="html">
  <div class="">
    <h1 class="subtitle is-2">Pre Order</h1>
    <div class="field">
      <label class="label">Restaurant / Shop</label>
      <p class="control">
        <input v-model="formData.restaurantName" class="input is-large" type="text" placeholder="">
      </p>
    </div>

    <div class="field">
      <label class="label">
        Recommend
      </label>
      <div v-for="(menu, index) in formData.menus" class="field has-addons">
        <p class="control">
          <input v-model="menu.menu" class="input is-large" type="text" placeholder="">
        </p>
        <p v-if="menu.menu !== '' && index < formData.menus.length - 1" class="control">
          <a @click="removeMenuAtIndex(index)" class="button is-large is-danger">
            <b-icon icon="close"></b-icon>
          </a>
        </p>
        <p v-if="menu.menu !== '' && index === formData.menus.length - 1" class="control">
          <a @click="addMoreMenu" class="button is-large">
            <b-icon icon="add"></b-icon>
          </a>
        </p>
      </div>
    </div>
    <div class="field">
      <label class="label">
        Valid Until
      </label>
      <flat-pickr
          v-model="formData.closedDate"
          placeholder="Select date"
          :config="configTimePicker"
          :required="true"                
          input-class="form-control custom-input-class"                
          name="date">
      </flat-pickr>
    </div>

    <br>

    <a @click="createPreOrder(formData)" class="button is-large is-success">Create</a>

  </div>
</template>

<script>
import { mapActions } from 'vuex'
import flatPickr from 'vue-flatpickr-component'
import 'flatpickr/dist/flatpickr.css'

export default {
  data () {
    return {
      configTimePicker: {
        disableMobile: true,
        enableTime: true,
        time_24hr: true,
        dateFormat: 'd/m/Y H:i'
      },
      formData: {
        restaurantName: '',
        menus: [{
          menu: ''
        }],
        closedDate: ''
      }
    }
  },
  methods: {
    ...mapActions([
      'createPreOrder'
    ]),
    addMoreMenu () {
      this.formData.menus.push({menu: ''})
    },
    removeMenuAtIndex (index) {
      this.formData.menus.splice(index, 1)
    }
  },
  components: {
    flatPickr
  }
}
</script>

<style lang="css">
</style>
