<template>
  <div class="hello"  style="height:100%;">
    <nav>
      <div class="nav-wrapper">
        <a class="brand-logo left" style="cursor: default;"><b>Upload Image</b></a>
        <ul id="nav-mobile" class="right hide-on-med-and-down">
          <li style="margin-right:25px;" @click='goToRegister' v-if='checkStorage() == false'><a>Register</a></li>
          <li class="modal-trigger" data-target="modal1" style="margin-right:25px;" @click='' v-if='checkStorage() == true'><a>Add Image</a></li>
          <li style="margin-right:25px;" @click='' v-if='checkStorage() == true' @click='logout'><a>Logout</a></li>
        </ul>
      </div>
    </nav>

    <!-- Modal -->
    <div id="modal1" class="modal">
      <div class="container">
      	<ul class="tabs teal">
      		<li class="tab" style="width:100%;"><b>Add new Todo</b></li>
      	</ul>
      	<div id="login" class="col s12">
      		<form class="col s12">
      			<div class="form-container">
      				<div class="row">
                <br>
      					<div class="input-field col s12">
                  <textarea id="textarea1" class="materialize-textarea" v-model='newTodo.newActivity'></textarea>
      						<label for="text">New Activity</label>
      					</div>
      				</div>
      				<br>
      				<center>
                <a class="btn modal-action modal-close waves-effect waves-light teal" style="margin-right:5px;" @click='reset()'>Cancel</a>
      					<button class="btn waves-effect waves-light teal" @click='datetest'>Submit</button>
      					<br>
      				</center>
      			</div>
      		</form>
      	</div>
      </div>
    </div>

  </div>
</template>

<script>

export default {
  created () {
    this.checkStorage()
  },
  data () {
    return {
      newTodo: {
        newActivity: '',
        Deadline: ''
      },
      date: ''
    }
  },
  methods: {
    goToRegister () {
      this.$router.push('register')
    },
    checkStorage () {
      if (!localStorage.hasOwnProperty('authorization')) {
        return false
      } else {
        return true
      }
    },
    datetest () {
      console.log(this.newToDo);
    },
    addTodo(event){
      event.preventDefault()

      const token = localStorage.getItem('authorization')
      const todo  = {
        activity: this.newTodo.newActivity,
        deadline: this.newTodo.Deadline,
        token
      }

      axios({
        method: 'post',
        url: 'http://localhost:3000/todo/add',
        data: todo
      })
      .then(() => {
        this.newToDo = ''
        this.getTodo()
      })
      .catch(err => {
        console.log(err);
      })
    },
    reset () {
      this.newTodo.newActivity = ''
      this.newTodo.Deadline = ''
    },
    logout () {
      localStorage.clear();
      this.$router.push('/')
    }
  }
}
</script>

<style scoped>
ul {
  list-style-type: none;
  padding: 0;
}
a {
  color: #dfe6e9;
}
nav {
    -webkit-transform: none;
    transform: none;
    text-align: left;
    background-color: #2d3436;
    font-family: sans-serif;
    padding-left: 15px;
}

.modal {
width: 40%;
height: 100%;
margin-top: 0px;
padding: 0 0 0 0;
}

h5
{
font-weight: 400;
}

.container{
margin: 0 0 0 0;
width: 100%;
height: 100%;
}

.tabs .indicator
{
background-color: #1e2121;
opacity: 0.3;
}

.form-container
{
padding: 40px;
padding-top: 10px;
}

.confirmation-tabs-btn
{
position: absolute;
}
</style>
