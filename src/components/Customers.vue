<template>
  <div class="customers container">
    <Alert v-if="alert" v-bind:message="alert" />
    <h1 class="page-header">Manage Customers</h1>
    <input class="form-control" placeholder="Enter Last Name" v-model="searchInput">
    <br />
    <table class="table table-striped">
        <thead>
          <tr>
            <th>First Name</th>
            <th>Last Name</th>
            <th>Email</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="customer in customers" :key="customer._id">
            <td>{{customer.firstName}}</td>
            <td>{{customer.lastName}}</td>
            <td>{{customer.email}}</td>
            <td><router-link class="btn btn-default" v-bind:to="'/customer/'+customer._id">View</router-link></td>
          </tr>
        </tbody>
    </table>
  </div>
</template>

<script>
  import Alert from './Alert';
  import axios from 'axios';
  export default {
    name: 'customers',
    data () {
      return {
        customers: [],
        alert:'',
        searchInput: ''
      }
    },
    methods: {
      fetchCustomers(){
        axios.get("https://radiuss.herokuapp.com/api/customers")
          .then((response) => {
            this.customers = response.data
          })
      }
    },
    created(){
      if(this.$route.query.alert){
        this.alert = this.$route.query.alert;
      }
      this.fetchCustomers();
    },
    // updated: function(){
    //   this.fetchCustomers();
    // },
    components: {
      Alert
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
