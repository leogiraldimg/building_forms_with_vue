<template>
  <div>
    <h3>Payment</h3>
    <form novalidate @submit.prevent="onSave">
      <div class="row">
        <div class="col-md-6">
          <div><strong>Shipping Information</strong></div>
          <div class="form-group">
            <label for="name">Name</label>
            <input
              id="name"
              type="text"
              class="form-control"
              placeholder="Your Name"
              v-model="payment.fullName"
            />
          </div>
          <div class="form-group">
            <label for="company">Company Name</label>
            <input
              id="company"
              type="text"
              class="form-control"
              placeholder="Company"
              v-model="payment.company"
            />
          </div>
          <div class="form-group">
            <label for="address1">Address</label>
            <input
              id="address1"
              type="text"
              class="form-control"
              placeholder="Street Address"
              v-model="payment.address1"
            />
          </div>
          <div class="form-group">
            <label for="address2">Suite/Apartment #</label>
            <input
              id="address2"
              type="text"
              class="form-control"
              placeholder=""
              v-model="payment.address2"
            />
          </div>
          <div class="form-row">
            <div class="form-group col-md-6">
              <label for="cityTown">City</label>
              <input
                id="cityTown"
                type="text"
                class="form-control"
                placeholder="e.g. New York"
                v-model="payment.cityTown"
              />
            </div>
            <div class="form-group col-md-3">
              <label for="stateProvince">State</label>
              <select
                id="stateProvince"
                class="form-control"
                v-model="payment.stateProvince"
              >
                <option
                  v-for="s in states"
                  :key="s.abbreviation"
                  :value="s.abbreviation"
                >
                  {{ stateFormat(s) }}
                </option
                >
              </select>
            </div>
            <div class="form-group col-md-3">
              <label for="postalCode">Zipcode</label>
              <input
                id="postalCode"
                type="text"
                class="form-control"
                placeholder="e.g. 10101"
                v-model="zipcode"
              />
            </div>
            <div class="form-group">
              <input type="submit" value="Next" class="btn btn-success" />
            </div>
          </div>
        </div>
        <div class="col-md-6">
          <div><strong>Billing Information</strong></div>
        </div>
      </div>
    </form>
    <div>
      <pre>{{ payment }}</pre>
    </div>
  </div>
</template>

<script>
import { ref, computed } from "vue";
import states from "@/lookup/states";
import formatters from "@/formatters";

export default {
  setup() {
    const payment = ref({
      fullName: "Shawn",
      postalCode: "12345",
    });

    function onSave() {
      alert("We can't save yet");
    }

    const zipcode = computed({
      get: () => payment.value.postalCode,
      set: (val) => {
        if (val && typeof val === "string") {
          if (val.length <= 5 || val.indexOf("-") > -1) {
            payment.value.postalCode = val;
          } else {
            payment.value.postalCode = `${val.substring(0,5)}-${val.substring(5)}`
          }
        }
      }
    });

    return {
      payment,
      states,
      onSave,
      ...formatters,
      zipcode
    };
  },
};
</script>
