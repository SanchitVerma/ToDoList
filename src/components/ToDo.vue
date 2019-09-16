<template>
  <div class="hello">
    <div class="holder">

      <form @submit.prevent="addToDos">
      <input type="test" placeholder="Enter a To Do item" v-model="ToDos" v-validate="'min:5'" name="ToDos">
      
      <transition name="alert-in" enter-active-class="animated flipInx" leave-active-class="animated flipOutx">
      <p class="alert" v-if= "errors.has('ToDos')"> {{errors.first('ToDos')}}</p>
      </transition>
      </form>

      <ul>
        <transition-group name="list" enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown">
          <li v-for="(data, index) in ToDo" :key='index'>
            {{data.ToDos}}
            <i class="fa fa-minus-circle" v-on:click="remove(index)"></i>
          </li>
        </transition-group>
      </ul>

      <p> These are your To Do items.</p>
    </div>
  </div>  
</template>

<script>
export default {
  name: 'ToDo',
  data() {
    return {
      ToDos:'',
      ToDo: [
        {"ToDos": "Do Laundry"},
        {"ToDos": "Do Assignment 1 of Enterprise Arch"},
        {"ToDos": "Prepare For Career Fair "}
      ]
    }
  },
  methods:{
    addToDos(){
      this.$validator.validateAll().then((result)=> {
        if (result) {
            this.ToDo.push({ToDos: this.ToDos})
            this.ToDos='';
        }
      })
    },
    remove(id) {
      this.ToDo.splice(id,1);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";
@import "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css";
  .holder {
    background: #fff;
  }

  ul {
    margin: 0;
    padding: 0;
    list-style-type: none;
  }
  
  ul li {
    padding: 20px;
    font-size: 1.3em;
    background-color: #E0EDF4;
    border-left: 5px solid #3EB3F6;
    margin-bottom: 2px;
    color: #3E5252;
  }

  p {
    text-align:center;
    padding: 30px 0;
    color: gray;
  }

  .container {
    box-shadow: 0px 0px 40px lightgray;
  }
  input{

    width: calc(100% - 40px);
    border: 0;
    padding: 20px;
    font-size: 1.3em;
    background-color: #323733;
    color: #689F7F;
  }
    .alert {
    background: #fdf2ce;
    font-weight: bold;
    display: inline-block;
    padding: 5px;
    margin-top: -20px;
  }

  .alert-in-enter-active{
    animation: bounce-in .5s;
  }

  .alert-in-leave-active{
    animation: bounce-in .5s reverse;
  }
  @keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(1);
  }
}
i {
  float:right;
}
</style>
