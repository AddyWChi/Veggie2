<template>
  <div class="hello">
  <h1>{{ errMsg }}</h1>

  <b-container fluid="md">
    <b-row>
      <b-col>
        <input type="number" inputmode="numeric" class="form-control item-count"
              v-model="payment" 
              @input="onInputPayment()" 
              @click="onClickSelect()"
              @focus="onFocusSelect()"/>
      </b-col>
      <b-col><strong>${{ totalItemCount }}</strong></b-col>
    </b-row>
    <b-row>
      <b-col>payment</b-col>
      <b-col><strong>${{ payment - totalAmount }}</strong></b-col>
    </b-row>
    <b-row>
      <b-col>一共</b-col>
      <b-col><strong>{{ totalItemCount }} 項</strong></b-col>
      <b-col>總額</b-col>
      <b-col><strong>${{ totalAmount }}</strong></b-col>
    </b-row>
    <b-row v-for="o in orderItems" :key="o.id">
      <b-col> ${{ o.amount }} x  </b-col>
      <b-col>
        <input type="number" inputmode="numeric" class="form-control item-count"
              :id="'amountInput_' + o.amount" 
              v-model="o.count" 
              @input="onInput(o.amount, $event)" 
              @click="onClick(o.amount, $event)"
              @focus="onFocus(o.amount, $event)"/>
      </b-col>
      <b-col>
            = ${{ o.amount * o.count }}
      </b-col>
      <b-col> 
        <button type="button" class="item-btn"
                @click="purchaseCount(o.amount, 1)">
            + 
        </button>
      </b-col>
      <b-col> 
        <button type="button" class="item-btn"
                @click="purchaseCount(o.amount, -1)">
            -
        </button>
      </b-col>
    </b-row>
  </b-container>

 </div>
</template>

<script>

export default {
  name: 'OrderMenu',
  props: {
    'menuItems': {
      type: [Array, Number],
      required: true,
      default: () => [],
      validator: (value) => {
        const isValid = Array.isArray(value) && value.every(item => typeof item === 'number' && item > 0);
        if (!isValid) {
          console.error('Invalid prop: menuItems must be an array of positive numbers.');
        }

        return isValid;
      }
    }
  },
  data() {
    return {
      // https://railsdrop.com/2025/11/07/browser-storage-mechanisms-explained-with-vue-js-examples/
      errMsg: '',
      orderItems: [],
      payment: 0,
      adjustAmount: 0,
      adjustSign: true,  // Set true if it's a plus sign. Set false if it's a minus sign.
      changeAmount: 0,
    }
  },
  computed: {
    totalAmount() {
      const total = this.orderItems.reduce((sum, item) => sum + (item.amount * item.count), 0);
      
      return total;
    },
    totalItemCount() {
      const totalCount = this.orderItems.reduce((sum, item) => sum + item.count, 0);
      this.$emit('evt-total-item-count', totalCount);

      return totalCount;
    },
  },
  methods: {
    sendEvent(evtName, evtMsg) {
      console.log(`call sendEvent: eventName: ${evtName}, msg: ${evtMsg}`);
      this.$emit(evtName, evtMsg);
    },

    purchaseCount(amount, count) {
      console.log(`call: purchaseCount(amount: ${amount}, count: ${count})`);
      const item = this.orderItems.find((i) => i.amount == amount);
      if (item) {
        item.count = (item.count + count) <= 0 ? 0 : item.count + count;
      } else {
        this.errMsg = `Item with amount ${amount} not found.`;
      }
    },

    onInput(amount, event) {
      console.log(`call: onInput(amount: ${amount}, input value: ${event.target.value})`);
      const item = this.orderItems.find((i) => i.amount === amount)
      const raw = event.target.value;
      // If empty string or user input '-', set count to 0
      if (raw === '' || raw === '-') {
        this.payment = 0;
        return;
      }
      const parsed = Number(raw);
      if (!Number.isNaN(parsed)) {
        item.count = parsed;
      }
      return;
    },

    onClick(amount, event) {
      console.log(`call: onClick(amount: ${amount}, old input event: ${event.target.value})`);
      event.target.select(); 
    },

    onFocus(amount, event) {
      console.log(`call: onFocus(amount: ${amount}, old input event: ${event.target.value})`);
      event.target.select(); 
    },

    // const total = computed(() =>
      // items.value.reduce((sum, item) => sum + item.amount * item.value, 0))
    // const payment = ref(0)
    // const change = computed(() => payment.value - total.value)

    onInputPayment(event) {
      console.log(`call: onInputPayment(input value: ${event.target.value})`);
      const raw = event.target.value;
      // If empty string or user input '-', set count to 0
      if (raw === '' || raw === '-') {
        event.target.value = 0;
        return;
      }
      const parsedValue = Number(raw);
      if (Number.isNaN(parsedValue)) {
        event.target.value = 0;
      }
      return;
    },

    onClickSelect(event) {
      console.log(`call: onClickSelectSelect(input event: ${event.target.value})`);
      event.target.select(); 
    },

    onFocusSelect(event) {
      console.log(`call: onFocusSelect(input event: ${event.target.value})`);
      event.target.select(); 
    },

    formatCurrency(value) {
      return new Intl.NumberFormat('en-US', {
        style: 'currency',
        currency: 'USD',
        minimumFractionDigits: 0,
        maximumFractionDigits: 2,
      }).format(value)
    },

    rowSum(item) {
      return item.amount * item.value
    },

    removeItem(id) {
      this.orderItems = this.orderItems.filter((item) => item.id !== id)
    }
  },  
  // Before app is fully initialized 
  beforeCreate() {
    console.log('call: beforeCreate');
    return;
  },
  
  created() {
    console.log('call: created');
    return;
  },

  beforeMount() {
    console.log('call: beforeMount');
    return;
  },

  mounted() {
    console.log('call: mounted');
    let id = 0;
    console.log(`menuItems: ${this.menuItems}`);
    for (let i = 0; i < this.menuItems.length; i++) {
      this.orderItems.push({
        id: id++,
        amount: this.menuItems[i],
        count: 0
      });
    }
    return;
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
