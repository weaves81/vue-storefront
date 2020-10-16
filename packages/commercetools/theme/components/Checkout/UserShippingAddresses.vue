<template>
  <div>
    <SfAddressPicker
      :value="currentAddressId"
      @input="setCurrentAddress($event)"
      class="shipping__addresses"
    >
      <SfAddress
        v-for="shippingAddress in shippingAddresses"
        :key="userShippingGetters.getId(shippingAddress)"
        :name="String(userShippingGetters.getId(shippingAddress))"
      >
        <span
          >{{ userShippingGetters.getFirstName(shippingAddress) }} {{ userShippingGetters.getLastName(shippingAddress) }}</span
        >
        <span
          >{{ userShippingGetters.getStreetName(shippingAddress) }}
          {{ userShippingGetters.getApartmentNumber(shippingAddress) }}</span
        >
        <span>{{ userShippingGetters.getPostCode(shippingAddress) }}</span>
        <span
          >{{ userShippingGetters.getCity(shippingAddress)
          }}{{ userShippingGetters.getProvince(shippingAddress) ? `, ${userShippingGetters.getProvince(shippingAddress)}` : '' }}</span
        >
        <span>{{ userShippingGetters.getCountry(shippingAddress)}}</span>
        <span>{{ userShippingGetters.getPhone(shippingAddress) }}</span>
      </SfAddress>
    </SfAddressPicker>
    <SfCheckbox
      data-cy="shipping-details-checkbox_isDefault"
      :selected="setAsDefault"
      @change="$emit('changeSetAsDefault', $event)"
      name="setAsDefault"
      label="Use this address as my default one."
      class="shipping-address-setAsDefault"
    />
  </div>
</template>

<script>
import {
  SfCheckbox
} from '@storefront-ui/vue';
import SfAddressPicker from '~/components/temp/SfAddressPicker';
import { userShippingGetters } from '@vue-storefront/commercetools';

export default {
  name: 'UserShippingAddresses',
  props: {
    currentAddressId: {
      type: Number,
      required: true
    },
    setAsDefault: {
      type: Boolean,
      required: true
    },
    shippingAddresses: {
      type: Array,
      required: true
    }
  },
  components: {
    SfCheckbox,
    SfAddressPicker
  },
  setup (_, { emit }) {
    const setCurrentAddress = $event => emit('setCurrentAddress', $event);

    return {
      setCurrentAddress,
      userShippingGetters
    };
  }
};
</script>

<style lang="scss">
@import "~@storefront-ui/shared/styles/variables";

  .shipping__addresses {
    @include for-desktop {
      display: grid;
      grid-template-columns: 1fr 1fr;
    }
    margin-bottom: var(--spacer-xl);
    .sf-address {
      margin-bottom: var(--spacer-sm);
    }
  }

  .shipping-address-setAsDefault, .form__action-button--margin-bottom {
    margin-bottom: var(--spacer-xl);
  }
</style>
