<template>
  <div class="pizza-orders">
    <h1>{{ heading }}</h1>
    <div class="container">
      <table class="table table-bordered m-5 p-5 .thead-dark">
        <thead>
        <tr>
          <th>Customer Name</th>
          <th>Quantity</th>
          <th>Amount</th>
          <th>Status</th>
          <th>Actions</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="(order, index) in orders" :key="index">
          <td>{{ order.customer_name }}</td>
          <td>{{ order.quantity }}</td>
          <td>{{ '$' + order.amount }}</td>
          <td :class="getTextClass(order.status)">
            {{ order.status }}
          </td>
          <td>
            <button class="btn btn-sm btn-primary mb-2" @click="updateStatus(index,order.status)">Change Status
            </button>
            <button class="btn btn-sm btn-danger ml-3" @click="resetOrder(index)">Reset
            </button>
          </td>
        </tr>
        </tbody>
      </table>
      <button class="btn btn-sm btn-danger" @click="reset">Reset All Orders</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'OrdersList',
  data() {
    return {
      heading: 'Pizza Orders',
      orders: [],
    }
  },
  mounted() {
    this.seedDefaultData();
  },
  methods: {
    seedDefaultData() {
      let orderId = 1;
      while (orderId <= 10) {
        this.orders.push({
          customer_name: 'Customer ' + orderId,
          quantity: orderId,
          amount: orderId * 100,
          status: 'Order Received',
        });
        orderId++;
      }
    },
    updateStatus(index, status) {
      let updatedStatus = false;
      if (status === 'Order Received') {
        updatedStatus = 'Preparing';
      }
      if (status === 'Preparing') {
        updatedStatus = 'Ready To Serve';
      }
      if (updatedStatus) {
        this.orders[index].status = updatedStatus;
      }
    },
    resetOrder(index) {
      this.orders[index].status = 'Order Received';
    },
    getTextClass(status) {
      if (status === 'Preparing') {
        return 'text-warning';
      }
      if (status === 'Ready To Serve') {
        return 'text-success';
      }
    },
    reset() {
      this.orders = [];
      this.seedDefaultData();
    }
  }
}
</script>
