<template>

    <div v-if="data.length > 1">
        <div v-for="(item) in data" v-bind:key="item">
            <p> {{ item.value }} </p>
        </div>
    </div>

    <div v-else class="login-box">
        

        <form @submit.prevent="addTodo()">
            <h2> Add Your First Note! </h2>
            <div class="user-box">
                <input type="text" autocomplete="off" name="title" required="">
                <label>Title</label>
            </div>
            <div class="user-box">
                <input v-model="newItem"
                        name="newTodo"
                        autocomplete="off"
                        required="">
                <label>Your Note</label>
            </div>
            <a @click="addItem()">
                <span></span>
                <span></span>
                <span></span>
                <span></span>
                Add Note 
            </a>
        </form>
        
    </div>
</template>

<script>

import { ref } from 'vue';

export default {
    name: "Notes",
    setup() {
        const newItem = ref('');
        const defaultData = [{
            done: false,
            value: "Hmmm... There should be a reality show where flat-earthers have to find the edge of the world."
        }]
        const data = JSON.parse(localStorage.getItem('items')) || defaultData;
        console.log(data.length);
        const items = ref(data);

        const addItem = () => {
            if (newItem.value) {
                items.value.push({
                    done: false,
                    conntent: newItem.value
                });
                newItem.value = "";
            }saveItem();
        }

        const doneItem = (item) => {
            item.done = true;
            saveItem();
        }

        const removeItem = (index) => {
            items.value.splice(index, 1)
            saveItem();
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

.login-box form a {
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

.login-box a:hover {
  background: #ceb3ff;
  color: #fff;
  border-radius: 5px;
  box-shadow: 0 0 5px #ceb3ff,
              0 0 25px #ceb3ff,
              0 0 50px #ceb3ff,
              0 0 100px #ceb3ff;
}

.login-box a span {
  position: absolute;
  display: block;
}

.login-box a span:nth-child(1) {
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

.login-box a span:nth-child(2) {
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

.login-box a span:nth-child(3) {
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

.login-box a span:nth-child(4) {
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