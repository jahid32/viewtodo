 <template>
 <div class="composer">
    <form @submit.prevent="$emit('onEnter')"> 
    <input 
    type="text"  
    placeholder="Type and hit enter..." 
    :value="modelValue" 
    @input="$emit('update:modelValue', $event.target.value)"
    class="composer__input" />
    </form>
  </div>
  </template>
  <script>
 export default{
     props: {
         modelValue: {
             type: String,
             default: '',
         },
     },
      emits: ['update:modelValue']
 }
  </script>
  