<script setup>
import httpService from '@/services/HttpService';
import { reactive, onMounted } from 'vue';
import { useRoute, useRouter } from 'vue-router';

const route = useRoute();
const router = useRouter();

const state = reactive({
    memo: {
        id: 0,
        title: '',
        content: '',
        createdAt: ''
    }
});

onMounted(async () => {
  const id = route.params.id;
  const data = await httpService.findById(id);
  state.memo = data.resultData;
});

const moveToForm = () => {
  const json = JSON.stringify(state.memo); // Object to JSON (직렬화)
  router.push({
    path: '/memo/add',
    state: {
      data: json
    }
  });
}

</script>

<template> 
  <div class="mb-3">
    등록일시: {{ state.memo.createdAt }}
  </div>
  <div class="mb-3">
    제목: {{ state.memo.title }}      
  </div>
  <div class="mb-3">
    내용: {{ state.memo.content }}
  </div>  
  <button type="button" class="btn btn-primary w-100 py-3" @click="moveToForm">수정</button>  
</template>

<style scoped>
</style>