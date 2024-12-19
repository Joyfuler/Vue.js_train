<template>
  <div class = "container">
    <h2>To do List</h2>
    <form>
      <input type = "text">
      <h1 :class = "colorName">
        <!-- h1의 클래스가 변화에 연동되도록 v-bind를 걸었음. 아래 변경될 시 반응한다-->
        {{ name2.name }} Hello, World
      </h1>  
      <h2>
        {{fnc(name2.name)}}
      </h2>
      <button class = "btn btn-primary" 
        @click="clickEvent"
      >버튼입니다 </button>
      <button class = "btn btn-primary"
        @click="typeShift"
      >ADD</button>
    <!-- vue에서는 v-on: 태그를 사용하여 이벤트 처리-->
      <div>
      <br>      
      <input v-bind:type="name2.type" v-model="name2.name">
      <!-- v-model을 사용하여 간단하게 양방향 reactive 기능 구현이 가능. input 값이 변경되면 h1이 변경, h1이 변경되면 input값이 변경된다-->
      </div>      
    </form>  
    </div>  
</template>

<script>
  import { ref, reactive } from 'vue'
  // reactive : object / 배열에 사용. json등
  
  export default {
    setup(){
      let name = ref("Joyfuler")
      let name2 = reactive({
        id : 1,
        name : "Joyfuler",
        type : "text"
      })

      let colorName = ref("colorBlue")

      
      // 옵저버. 추적하다가 상태변화시알림
      // ref는 객체이므로 name대신 그 value를 가져와 출력해야 한다

      const fnc = temp => {
        return 'Hello, ' + temp 
      }

      const clickEvent = () => {
        name.value = "newJoyfuler"
        name2.name = "newJoyfuler"
        //alert(name.value)
        if (colorName.value == 'colorRed'){
          colorName.value = 'colorBlue'
        } else {
          colorName.value = 'colorRed'
        }        
      }

      const typeShift = () =>{
        name2.type = "number"
        name2.name = "1"
      }



      return{
        name, name2, fnc, clickEvent, colorName, typeShift
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
