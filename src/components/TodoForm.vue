<template>
    <div>
      <form class = "d-flex" @submit.prevent="onSubmit">            
      <!-- 기존 form 이벤트를 방지하고 onSubmit을 실행함 -->
      <div class = "flex-grow-1">      
        <input class = "form-control" type = "text"
      v-model="todo">
        <div v-show="hasError" style = "color: red;">
          cannot be empty
        </div>
      <button class = "btn btn-primary m-1" type = "submit"        
      >버튼입니다 </button>  
      </div>      
    </form>    
    </div>   
</template>
 <script>       
  import { ref } from 'vue'  
  export default {          
    setup(prop, context){      
      let hasError = ref(false)
      let colorName = ref('colorBlue')
      let isDelete = ref(false)
      let todo = ref("")      
      // let todo2 = reactive({
      //   id : 1,
      //   name : "todo2"
      // })

      const onSubmit = () =>{
        if (todo.value){
            context.emit('appTodo', {
            id : Date.now(), // 현재시간
            subject : todo.value,
            completed : false
          })
          //자녀 element를 부모 app.vue로 보낸다

        todo.value = ''
        hasError.value = false
        
        } else {
          hasError.value = true
          alert('값을 입력해주세요!')
        }

      }

      // 옵저버. 추적하다가 상태변화시알림
      // ref는 객체이므로 name대신 그 value를 가져와 출력해야 한다

      return{
        // 변수
        todo, hasError, colorName, isDelete, 
        // 함수
        onSubmit
      }
    }
  }

    </script>        
    <style>
    </style>    