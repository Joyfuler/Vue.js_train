<template>
  <div v-show="toggle">true</div>
  <div v-show="!toggle">false</div>

  <div v-if="toggle">
    ttrue
  </div>  
  <div v-else>
    ffalse
  </div>  

  <div class = "container">
    <h2>Todo List</h2>
    <form class = "d-flex" @submit.prevent="onSubmit()">            
      <!-- 기존 form 이벤트를 방지하고 onSubmit을 실행함 -->
      <div class = "flex-grow-1">      
        <input class = "form-control" type = "text"
      v-model="todo">
      <button class = "btn btn-primary m-1" type = "submit"
        @click="clickEvent"
      >버튼입니다 </button>
      <button class = "btn btn-primary ms-1" type = "button"
        @click="onToggle"
      >토글버튼</button><br>      
        <div class = "card mt-2" v-for = "todo in todos" :key="todo.id">
          <div class = "card-body">
            <!-- for문 사용시 :key를 반드시 입력할 것 -->
            {{todo.subject}}
          </div>        
        </div>  
      </div>      
    </form>    
  </div>  
</template>

<script>
  import { ref } from 'vue'
  // reactive : object / 배열에 사용. json등
  
  export default {
    setup(){
      let toggle = ref(false)
      let todo = ref("")
      let todos = ref([
        {
          id: 1,
          subject: 'test1'
        },
        {
          id: 2,
          subject: 'test2'
        }
      ])
      // let todo2 = reactive({
      //   id : 1,
      //   name : "todo2"
      // })

      const onSubmit = () =>{
        todos.value.push({
          id : Date.now(), // 현재시간
          subject : todo.value
        })
      }

      const onToggle = () => {
        toggle.value = !toggle.value
      }
      
      // 옵저버. 추적하다가 상태변화시알림
      // ref는 객체이므로 name대신 그 value를 가져와 출력해야 한다

      return{
        // 변수
        todo, todos, toggle,
        // 함수
        onSubmit, onToggle
      }
    }
  }

</script>

<style>
  div h1{
    color: red;
  }

  .colorRed{
    color: red;
  }

  .colorBlue{
    color: blue;
  }

  *{
    margin:10px;
  }
</style>
