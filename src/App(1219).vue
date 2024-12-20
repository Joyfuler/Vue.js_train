<template>
  <div>
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
        <div v-show="hasError" style = "color: red;">
          cannot be empty
        </div>
      <button class = "btn btn-primary m-1" type = "submit"
        @click="clickEvent"
      >버튼입니다 </button>    
      <div class = "card mt-2" v-if="todos.length == 0">
        <div class = "card-body">
          내용이 없습니다.
        </div>
      </div>
        <div class = "card mt-2" v-for = "(todo, index) in todos" :key="todo.id" v-show="!isDelete">
          <div class = "card-body d-flex">
            <!-- d-flex를 사용하여 그리드화. 줄바꾸기 대신 옆으로 정렬된다 -->            
            <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault" @change="changeStatus" v-model="todo.completed">
            <label class="form-check-label flex-grow-1" for="flexCheckDefault" :class="{
              done: todo.completed}">              
            {{todo.subject}}
            </label>
            <div>
              <button class = "btn btn-danger btn-sm m-1" type = "button"
                @click="deleteThis(index)">삭제 
              </button>    
            </div>  
          </div>        
        </div>                            
      </div>      
    </form>    
  </div>  
  </div>
</template>

<script>
  import { ref } from 'vue'
  // reactive : object / 배열에 사용. json등
  
  export default {
    setup(){      
      let hasError = ref(false)
      let colorName = ref('colorBlue')
      let isDelete = ref(false)
      let todo = ref("")
      let todos = ref([])
      // let todo2 = reactive({
      //   id : 1,
      //   name : "todo2"
      // })

      const onSubmit = () =>{
        if (todo.value){
            todos.value.push({
            id : Date.now(), // 현재시간
            subject : todo.value,
            completed : false
          })

        todo.value = ''
        hasError.value = false
        
        } else {
          hasError.value = true
          alert('값을 입력해주세요!')
        }

      }

      const deleteThis = index => {
        todos.value.splice(index, 1)
        // 해당 인덱스에서 1개만 지움
        console.log(index)

      }


     
      // 옵저버. 추적하다가 상태변화시알림
      // ref는 객체이므로 name대신 그 value를 가져와 출력해야 한다

      return{
        // 변수
        todo, todos, hasError, colorName, isDelete, 
        // 함수
        onSubmit, deleteThis
      }
    }
  }

</script>

<style>
  div h1{
    color: red;
  }

  .notDone{
    color: red;
  }

  .done{
    color: gray;
    text-decoration: aqua;
  }

  *{
    margin:10px;
  }
</style>
