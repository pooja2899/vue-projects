<template>
  <div class="card has-text-left">
    <div class="card has-background-link-light p-5">
      <p class="title is-4">
        {{ $t("list-business-title") }}
      </p>
      <p class="subtitle is-6">
        {{ $t("list-business-sub-title") }}
      </p>      
      <form @submit.prevent="businessSubmit">
        <div class="columns">
          <div class="column is-9">
            <div class="control has-icons-left has-icons-right">
              <input
                :class="{
                  'is-danger': $v.business.businessName.$error,
                  input: true,
                }"
                type="text"
                placeholder="Business Name"
                v-model="business.businessName"
              />
              <span class="icon is-small is-left">
                <i class="fas fa-building"></i>
              </span>
              <span
                v-if="$v.business.businessName.$error"
                class="icon is-small is-right"
              >
                <i class="fas fa-exclamation-circle has-text-danger"></i>
              </span>
            </div>
            <p v-if="$v.business.businessName.$error" class="help is-danger">
              Business Name is Required
            </p>
          </div>
        </div>
        <div class="columns">
          <div class="column is-6">
            <div class="control">
              <div class="select">
                <select
                  @change="business.category = $event.target.value"
                  :class="{
                    'is-danger': $v.business.category.$error,
                    input: true,
                  }"
                >
                  <option disabled selected>Business Category</option>
                  <option
                    :key="key"
                    v-for="(c, key) in busCat.cat"
                    :value="c.cat"
                  >
                    {{ c.cat }}
                  </option>
                </select>
              </div>
              <i
                v-if="$v.business.category.$error"
                class="fas fa-exclamation-circle has-text-danger mt-3 ml-2"
              ></i>
              <p v-if="$v.business.category.$error" class="help is-danger">
                Business Category is required
              </p>
            </div>
          </div>
          <div class="column is-6">
            <div class="control">
              <div class="select">
                <select
                  @change="business.subCategory = $event.target.value"
                  :class="{
                    'is-danger': $v.business.subCategory.$error,
                    input: true,
                  }"
                >
                  <option disabled selected>Sub Category</option>
                  <option :key="c.scat" v-for="c in busCat.subCat">
                    {{ c.scat }}
                  </option>
                </select>
              </div>
              <i
                v-if="$v.business.subCategory.$error"
                class="fas fa-exclamation-circle has-text-danger mt-3 ml-2"
              ></i>
              <p v-if="$v.business.subCategory.$error" class="help is-danger">
                Sub Category is required
              </p>
            </div>
          </div>
        </div>
        <div class="columns">
          <div class="column is-6">
            <div class="control has-icons-left has-icons-right">
              <input
                :class="{
                  'is-danger': $v.business.firstName.$error,
                  input: true,
                }"
                type="text"
                placeholder="Contact First Name"
                v-model="business.firstName"
              />
              <span class="icon is-small is-left">
                <i class="fas fa-user"></i>
              </span>
              <span
                class="icon is-small is-right"
                v-if="$v.business.firstName.$error"
              >
                <i class="fas fa-exclamation-circle has-text-danger"></i>
              </span>
            </div>
            <p v-if="$v.business.firstName.$error" class="help is-danger">
              Contact First Name is required
            </p>
          </div>
          <div class="column is-6">
            <div class="control has-icons-left has-icons-right">
              <input
                :class="{
                  'is-danger': $v.business.lastName.$error,
                  input: true,
                }"
                type="text"
                placeholder="Contact Last Name"
                v-model="business.lastName"
              />
              <span class="icon is-small is-left">
                <i class="fas fa-user"></i>
              </span>
              <span
                v-if="$v.business.lastName.$error"
                class="icon is-small is-right"
              >
                <i class="fas fa-exclamation-circle has-text-danger"></i>
              </span>
            </div>
            <p v-if="$v.business.lastName.$error" class="help is-danger">
              Contact Last Name is required
            </p>
          </div>
        </div>
        <div class="columns">
          <div class="column is-6">
            <div class="control has-icons-left has-icons-right">
              <input
                :class="{
                  'is-danger': $v.business.email.$error,
                  input: true,
                }"
                type="text"
                placeholder="Email"
                v-model="business.email"
              />
              <span class="icon is-small is-left">
                <i class="fas fa-envelope"></i>
              </span>
              <span
                v-if="$v.business.email.$error"
                class="icon is-small is-right"
              >
                <i class="fas fa-exclamation-circle has-text-danger"></i>
              </span>
            </div>
            <p v-if="$v.business.email.$error" class="help is-danger">
              Email is invalid
            </p>
          </div>

          <div class="column is-6">
            <div class="field is-horizontal">
              <div class="field-body">
                <div class="field is-expanded">
                  <div class="field has-addons">
                    <p class="control">
                      <a class="button is-static">+91</a>
                    </p>
                    <div class="control is-expanded has-icons-right">
                      <input
                        :class="{
                          'is-danger': $v.business.phone.$error,
                          input: true,
                        }"
                        type="tel"
                        placeholder="Phone Number"
                        v-model="business.phone"
                      />
                      <span
                        v-if="$v.business.phone.$error"
                        class="icon is-small is-right"
                      >
                        <i
                          class="fas fa-exclamation-circle has-text-danger"
                        ></i>
                      </span>
                      <p v-if="$v.business.phone.$error" class="help is-danger">
                        Phone number is invalid
                      </p>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="columns">
          <div class="column is-12">
            <div class="control has-icons-left has-icons-right">
              <input
                :class="{
                  'is-danger': $v.business.address.$error,
                  input: true,
                }"
                type="text"
                placeholder="Address"
                v-model="business.address"
              />
              <span class="icon is-small is-left">
                <i class="fas fa-envelope"></i>
              </span>
              <span
                v-if="$v.business.address.$error"
                class="icon is-small is-right"
              >
                <i class="fas fa-exclamation-circle has-text-danger"></i>
              </span>
            </div>
            <p v-if="$v.business.address.$error" class="help is-danger">
              Address is required
            </p>
          </div>
        </div>
        <div class="columns">
          <div class="column is-6">
            <div v-if="!isDisabled" class="is-flex">
              <VSelect
                placeholder="Select City"
                :options="world"
                label="city"
                v-model="business.city"
                @input="process($event)"
              >
                <template #search="{ attributes, events }">
                  <input
                    @click="citySuggest('city', 'a')"
                    @input="citySuggest('city', $event.target.value)"
                    class="vs__search"
                    v-bind="attributes"
                    v-on="events"
                  />
                </template>
                <template #no-options="{}"><div></div> </template>
              </VSelect>
              <div v-if="$v.business.city.$error">
                <i
                  class="fas fa-exclamation-circle has-text-danger mt-2 ml-2"
                ></i>
              </div>
            </div>

            <p v-if="$v.business.city.$error" class="help is-danger">
              City is required
            </p>
          </div>
          <div class="column is-6">
            <div v-if="business.city != null" class="control">
              <input
                class="input"
                type="text"
                v-model="business.state"
                disabled
              />
            </div>
            <div v-if="business.city == null && !isDisabled" class="is-flex">
              <VSelect
                placeholder="Select State"
                :options="states"
                label="title"
                v-model="business.state"
                @input="process({ state: $event })"
              >
                <template #search="{ attributes, events }">
                  <input
                    @click="citySuggest('state', 'a')"
                    @input="citySuggest('state', $event.target.value)"
                    class="vs__search"
                    v-bind="attributes"
                    v-on="events"
                  />
                </template>
                <template #no-options="{}"><div></div> </template>
              </VSelect>
              <div v-if="$v.business.state.$error">
                <i
                  class="fas fa-exclamation-circle has-text-danger mt-2 ml-2"
                ></i>
              </div>
            </div>
            <p v-if="$v.business.state.$error" class="help is-danger">
              State is required
            </p>
          </div>
        </div>
        <div class="columns">
          <div class="column is-6">
            <div
              v-if="business.city != null || business.state != null"
              class="control"
            >
              <input
                class="input"
                type="text"
                v-model="business.country"
                disabled
              />
            </div>
            <div>
              <div
                v-if="business.city == null && business.state == null"
                class="is-flex"
              >
                <VSelect
                  placeholder="Select Country"
                  :options="countries"
                  label="country"
                  v-model="business.country"
                  @input="process({ country: $event })"
                >
                  <template #search="{ attributes, events }">
                    <input
                      @click="citySuggest('state', 'a')"
                      @input="citySuggest('country', $event.target.value)"
                      class="vs__search"
                      v-bind="attributes"
                      v-on="events"
                    />
                  </template>
                  <template #no-options="{}"><div></div> </template>
                </VSelect>
                <country-flag country='in' size='normal'/>
                <div v-if="$v.business.country.$error">
                  <i
                    class="fas fa-exclamation-circle has-text-danger mt-2 ml-2"
                  ></i>
                </div>
              </div>
              <p v-if="$v.business.country.$error" class="help is-danger">
                Country is required
              </p>
            </div>
          </div>
          <div class="column is-6">
            <div class="control has-icons-left has-icons-right">
              <input
                :class="{
                  'is-danger': $v.business.zip.$error,
                  input: true,
                }"
                type="text"
                placeholder="ZIP/PIN Code"
                v-model="business.zip"
              />
              <span class="icon is-small is-left">
                <i class="fas fa-envelope"></i>
              </span>
              <span
                v-if="$v.business.zip.$error"
                class="icon is-small is-right"
              >
                <i class="fas fa-exclamation-circle has-text-danger"></i>
              </span>
            </div>
            <p v-if="$v.business.zip.$error" class="help is-danger">
              ZIP Code is invalid
            </p>
          </div>
        </div>
        <div class="field-is-horizontal">
          <div class="field is-inline-block-desktop">
            <div class="field-body">
              <div class="field-label is-normal">
                <label class="label">From</label>
              </div>              
              <div class="field">            
                <p class="control is-expanded has-icons-left">
                  <Time @getTime="business.start=$event" :label="'Select Start Time'" :error="$v.business.start.$error" />
                </p>
              </div>
              <div class="field-label is-normal">
                <label class="label">To</label>
              </div>              
              <div class="field">
                <p class="control is-expanded has-icons-left">
                  <Time @getTime="business.end=$event" :label="'Select End Time'" :error="$v.business.end.$error" />
                </p>
              </div>
            </div>
          </div>
        </div>
        <div class="field is-grouped-left">
          <p class="control">
            <button class="button is-primary">{{ $t("save") }}</button>
          </p>
        </div>
      </form>     
    </div>
  </div>
</template>
<script>
import axios from "axios";
import { required, email, numeric } from "vuelidate/lib/validators";
import VSelect from "vue-select";
import cat from "@/views/business/categories.json";
import Time from "../../components/Time";
import CountryFlag from 'vue-country-flag';

export default {
  name: "Form",
  components: {
    VSelect,
    Time,
    CountryFlag
  },
  data() {
    return {
      timeInput: false,
      isDisabled: false,
      world: [],
      cities: [],
      states: [],
      countries: [],
      busCat: cat,
      business: {
        businessName: null,
        firstName: null,
        lastName: null,
        category: null,
        subCategory: null,
        email: null,
        city: null,
        state: null,
        country: null,
        address: null,
        phone: null,
        zip: null,
        cityId: null,
        start: null,
        end: null,
      },
    };
  },
  validations: {
    business: {
      businessName: { required },
      firstName: { required },
      lastName: { required },
      email: { required, email },
      category: { required },
      subCategory: { required },
      city: { required },
      state: { required },
      country: { required },
      address: { required },
      phone: { required },
      zip: { required, numeric },
      start: {required},
      end: {required},
    },
  },
  methods: {
    businessSubmit() {
      this.$v.$touch();
      if (this.$v.$invalid) {
        console.log("ERROR!! :-)\n\n" + JSON.stringify(this.business));
      } else {
        console.log("SUCCESS!! :-)\n\n" + JSON.stringify(this.business));
      }
    },
    citySuggest(place, query) {
      if (query !== null && query !== undefined && query !== "") {
        const url = this.$store.state.base_url + "city";
        axios
          .post(url, { place: place, query: query })
          .then((res) => {
            this.world = res.data;
            this.cities = [...new Set(res.data.map((a) => a["city"]))];
            this.states = [...new Set(res.data.map((a) => a["state"]))];
            this.countries = [...new Set(res.data.map((a) => a["country"]))];
            // console.log(this.cities);
            // console.log(this.states);
            // console.log(this.countries);
          })
          .catch((error) => {
            console.error(error);
          });
      } else {
        this.business.state = null;
        this.business.country = null;
      }
    },
    process(e) {
      if (e.state) {
        this.business.state = e.state;
        this.business.country = this.world.find((a) => (a.state = e.state))[
          "country"
        ];
        if (!this.world.find((a) => (a.state = e.state))["city"]) {
          this.isDisabled = true;
        } else {
          this.isDisabled = false;
        }
        console.log(e.country);
      } else if (e.country && !e.state) {
        this.isDisabled = true;
      } else {
        this.isDisabled = false;
      }
    },
  },
 
};
</script>
<style lang="scss">
@import "vue-select/src/scss/vue-select.scss";
.v-select {
  width: 80%;
}
</style>