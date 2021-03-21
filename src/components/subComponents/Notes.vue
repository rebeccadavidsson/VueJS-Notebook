<template>

    <div v-if="data.length > 0" class="notes-wrapper">
        <div v-for="(item) in data" v-bind:key="item">
            <div class="item">
              <checkmark :item=item />
              <p> {{ item.value }} </p>
            </div>
        </div>

        <div class="add-wrapper">
          <form @submit.prevent="addItem()">
            <div class="add">
              <input 
              v-model="newItem"
              name="newItem"
              autocomplete="off"
              required=""
              type="text" 
              placeholder="Thought...">
              <span @click="addItem()" class="addBtn">Add</span>
            </div>
          </form>
        </div>

        <a @click="removeItem()" class="mainbutton center-bottom"> 
            <span></span>
            <span></span>
            <span></span>
            <span></span>
            Remove active thoughts 
        </a>
  
    </div>

    <div v-else class="login-box">
      <form @submit.prevent="addTodo()">
          <h2> Add Your First Thought! </h2>
          <div class="user-box">
              <input type="text" autocomplete="off" name="title" required="">
              <label>Title</label>
          </div>
          <div class="user-box">
              <input v-model="newItem"
                      name="newTodo"
                      autocomplete="off"
                      required="">
              <label>Your Thought</label>
          </div>
          <a @click="addItem()" class="mainbutton"> 
              <span></span>
              <span></span>
              <span></span>
              <span></span>
              Add Thought 
          </a>
      </form>
        
    </div>
</template>

<script>

import { ref } from 'vue';
import checkmark from './checkMark'

export default {
    name: "Notes",
    components: {
      checkmark,
    },

    setup() {
        const newItem = ref('');
        const defaultData = [{
            done: false,
            value: "Hmmm... There should be a reality show where flat-earthers have to find the edge of the world."
        }]
        const data = JSON.parse(localStorage.getItem('items')) || defaultData;

        let items = ref(data);

        const addItem = () => {
            if (newItem.value) {
                items.value.push({
                    done: false,
                    value: newItem.value
                });
                newItem.value = "";
            }saveItem();
        }

        const doneItem = (item) => {
            item.done = true;
            saveItem();
        }

        const removeItem = () => {
            let filteredItems = items.value.filter(item => item.done === false);
            filteredItems = JSON.parse(JSON.stringify(filteredItems));
            localStorage.setItem("items", JSON.stringify(filteredItems))
            items = filteredItems;
        }
        
        const saveItem = () => { localStorage.setItem("items", JSON.stringify(items.value)) }

        return {
            items, 
            newItem, 
            addItem, 
            doneItem, 
            removeItem, 
            saveItem,
            data
        }

    }

}
</script>

<style scoped>
  .item {
    background-color: #b6a4d636;
    border-radius: 7px;
    padding: 1em 2em;
    margin-bottom: 1em;
    display: grid;
    grid-template-columns: 3.5em auto;
    grid-column-gap: 1em;
    align-items: center;
  }

.notes-wrapper {
    position: relative;
    height: 100%;
}

.add {
  display: flex;
}

.add-wrapper {
    background-color: #6561848c;
    padding: 1em;
    border-radius: 7px;
}

input {
  margin: 0;
  border: none;
  width: 75%;
  padding: 10px;
  float: left;
  font-size: 16px;
  padding-left: 1.5em;
  border-top-left-radius: 4px;
  border-bottom-left-radius: 4px;
}

/* Style the "Add" button */
.addBtn {
  padding: 10px;
  width: 25%;
  background: #d9d9d9;
  color: #555;
  float: left;
  text-align: center;
  font-size: 16px;
  cursor: pointer;
  transition: 0.3s;
  border-top-right-radius: 4px;
  border-bottom-right-radius: 4px;
}

.addBtn:hover {
  background-color: #bbb;
}

.login-box {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 400px;
  padding: 40px;
  transform: translate(-50%, -50%);
  background: rgba(0,0,0,.5);
  box-sizing: border-box;
  box-shadow: 0 15px 25px rgba(0,0,0,.6);
  border-radius: 10px;
}

.login-box h2 {
  margin: 0 0 30px;
  padding: 0;
  color: #fff;
  text-align: center;
}

.login-box .user-box {
  position: relative;
}

.login-box .user-box input {
  width: 100%;
  padding: 10px 0;
  font-size: 16px;
  color: #fff;
  margin-bottom: 30px;
  border: none;
  border-bottom: 1px solid #fff;
  outline: none;
  background: transparent;
}
.login-box .user-box label {
  position: absolute;
  top:0;
  left: 0;
  padding: 10px 0;
  font-size: 16px;
  color: #fff;
  pointer-events: none;
  transition: .5s;
}

.login-box .user-box input:focus ~ label,
.login-box .user-box input:valid ~ label {
  top: -20px;
  left: 0;
  color: #ceb3ff;
  font-size: 12px;
}

.mainbutton {
  position: relative;
  display: inline-block;
  padding: 10px 20px;
  color: #ceb3ff;
  font-size: 16px;
  text-decoration: none;
  text-transform: uppercase;
  overflow: hidden;
  transition: .5s;
  margin-top: 40px;
  letter-spacing: 4px
}
.center-bottom {
  width: calc(100% - 2.5em);
  text-align: center;
  position: absolute;
  bottom: 0;
  margin-bottom: 4em;
}

.mainbutton:hover {
  background: #ceb3ff;
  color: #fff;
  border-radius: 5px;
  cursor: pointer;
  box-shadow: 0 0 5px #ceb3ff,
              0 0 25px #ceb3ff,
              0 0 50px #ceb3ff,
              0 0 100px #ceb3ff;
}

.mainbutton span {
  position: absolute;
  display: block;
}

.mainbutton span:nth-child(1) {
  top: 0;
  left: -100%;
  width: 100%;
  height: 2px;
  background: linear-gradient(90deg, transparent, #ceb3ff);
  animation: btn-anim1 1s linear infinite;
}

@keyframes btn-anim1 {
  0% {
    left: -100%;
  }
  50%,100% {
    left: 100%;
  }
}

.mainbutton span:nth-child(2) {
  top: -100%;
  right: 0;
  width: 2px;
  height: 100%;
  background: linear-gradient(180deg, transparent, #ceb3ff);
  animation: btn-anim2 1s linear infinite;
  animation-delay: .25s
}

@keyframes btn-anim2 {
  0% {
    top: -100%;
  }
  50%,100% {
    top: 100%;
  }
}

.mainbutton span:nth-child(3) {
  bottom: 0;
  right: -100%;
  width: 100%;
  height: 2px;
  background: linear-gradient(270deg, transparent, #ceb3ff);
  animation: btn-anim3 1s linear infinite;
  animation-delay: .5s
}

@keyframes btn-anim3 {
  0% {
    right: -100%;
  }
  50%,100% {
    right: 100%;
  }
}

.mainbutton span:nth-child(4) {
  bottom: -100%;
  left: 0;
  width: 2px;
  height: 100%;
  background: linear-gradient(360deg, transparent, #ceb3ff);
  animation: btn-anim4 1s linear infinite;
  animation-delay: .75s
}

@keyframes btn-anim4 {
  0% {
    bottom: -100%;
  }
  50%,100% {
    bottom: 100%;
  }
}


</style>