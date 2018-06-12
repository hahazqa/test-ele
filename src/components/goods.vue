<template>
  <div class="goods">
      <div class="menu-wrapper" >
          <ul>
              <li></li>
          </ul>
      </div>
      <div class="foods-wrapper">

      </div>
  </div>
</template>

<script>
    export default {
        name:'goods',
        data (){
            return {
              goods:[],
              listHeight:[],
              scrollY:0,
              selectedFood:{}
            }
        },
        computed:{},
        created() {
            this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
            
        }
    }
</script>