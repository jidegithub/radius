<template>
  <div class="details container">
    <router-link to="/">Back</router-link>
    <h1 class="page-header">{{customer.firstName}} {{customer.lastName}}
      <span class="pull-right">
        <router-link class="btn btn-primary" v-bind:to="'/edit/'+customer._id">Edit</router-link>
        <button class="btn btn-danger" v-on:click="deleteCustomer(customer._id)">Delete</button>
      </span>
    </h1>
    <ul class="list-group">
      <li class="list-group-item"><span class="glyphicon glyphicon-phone" aria-hidden="true"></span> {{customer.phone}}</li>
      <li class="list-group-item"><span class="glyphicon glyphicon-envelope" aria-hidden="true"></span> {{customer.email}}</li>
    </ul>

    <ul class="list-group">
      <li class="list-group-item"> {{customer.address}}</li>
      <li class="list-group-item">{{customer.city}}</li>
      <li class="list-group-item">{{customer.state}}</li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'customerdetails',
  data () {
    return {
      customer: {},
    }
  },
  methods:{
    fetchCustomer(id){
      axios.get('https://radiuss.herokuapp.com/api/customers/'+id)
      .then((response) => {
        this.customer = response.data;
      });
    },
    deleteCustomer(id){
      axios.delete('https://radiuss.herokuapp.com/api/customers/delete/'+id)
      .then((response) => {
        this.$router.push({path: '/', query: {alert: 'Customer Deleted'}});
      });
    }
  },
  created(){
    this.fetchCustomer(this.$route.params.id);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
