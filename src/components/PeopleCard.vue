<script setup lang='ts'>
import { useRouter } from 'vue-router';
import { PropType } from 'vue';
import type People from "@/types/People";

const props = defineProps({
   person: {
      type: Object as PropType<People>,
      required: true
   }
});

const router = useRouter();

const navigateToPerson = () => {
   router.push(`/emberek/${props.person.id}`);
}

</script>

<template>
   <td>{{ person.id }}</td>
   <td>
      <img @click="navigateToPerson" 
         style="
               cursor: pointer; 
               width: 50px; 
               height: 50px; 
               border-radius: 50%;
               " 
         :src="person.avatar" 
         alt="avatar" 
         />
   </td>
   <td @click="navigateToPerson"
       style="cursor: pointer;"
       >
         {{ person.first_name }}
   </td>
   <td @click="navigateToPerson"
       style="cursor: pointer;"
       >
         {{ person.last_name }}
   </td>
   <td>{{ person.email }}</td>
</template>


<style scoped>

</style>