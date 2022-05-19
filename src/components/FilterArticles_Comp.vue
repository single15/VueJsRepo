<script setup>
    import { ref, onMounted, computed, defineProps } from 'vue'

    const props = defineProps(['title']);
    const searchValue = ref('');
    const list = ref([]);

    onMounted(() => {
        fetch('https://fakestoreapi.com/products')
        .then(res=>res.json())
        .then(l=> {
            list.value = l;
        });
    })

    const filteredItems = computed(() => {
        return list.value.filter(item => {
            return item.title.toLowerCase().indexOf(searchValue.value.toLowerCase()) > -1
        })
    });
</script>

<template>
  <div class="filter-article-section">
    <h1>{{ props.title }}</h1>
    <section>
        <input type="text" v-model="searchValue" @change="(e) => filterArticles(e.target.value)">
    </section>
    <section>
        <button>Reset</button>
    </section>
    <section>
        <div class="found-number">Showing {{ filteredItems.length }} results for "{{ searchValue }}"</div>
        <div class="list-section">
            <div v-if="!filteredItems.length" style="text-align: left">Loading...</div>
            <div v-else class="list-item" v-for="item in filteredItems" :key="item.id">
                <div>
                    {{item.title}}
                </div>
            </div>
        </div>
    </section>
  </div>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.filter-article-section {
    width: 40%;
    margin: auto;
}


h3 {
  margin: 40px 0 0;
}

input {
    margin-bottom: 24px;
    border: 2px solid darkcyan;
    padding: 10px;
    border-radius: 3px;
    outline: none;
}

button {
    margin-bottom: 20px;
}

.found-number {
    text-align: right;
}

.list-section {
    padding-top: 20px;
    height: 300px;
    overflow-y: scroll;
}

.list-section::-webkit-scrollbar {
    width: 5px;
}

.list-item {
    padding: 15px;
    border: 1px solid #ccc;
    border-bottom: none;    
}

.list-item:last-child {
    border-bottom: 1px solid #ccc;
}

</style>
