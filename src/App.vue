<script setup>
import { ref } from 'vue';
import { computed } from 'vue';

  const products = ref([
    {
      id: 1,
      name: 'IPhone 14',
      date: '25.11.2024',
      count: 10,
      price: 999
    },
    {
      id: 2,
      name: 'Samsung',
      date: '24.11.2024',
      count: 3,
      price: 899
    },
    {
      id: 3,
      name: 'Xiaomi 11',
      date: '20.11.2024',
      count: 15,
      price: 699
    },
    {
      id: 4,
      name: 'Huawei Mate 10',
      date: '19.11.2024',
      count: 8,
      price: 799
    }

    ]);

const name = ref('');
const date = ref('');
const count = ref(1);
const price = ref(0);

const addProduct = () => {
  if (name.value && date.value && count.value && price.value) {
    products.value.push(
      {
      id: Date.now(),
      name: name.value,
      date: date.value,
      count: count.value,
      price: price.value,
    }
    );
  }
}

const removeProduct = (id) => {
  products.value = products.value.filter((product) => product.id != id);
}

const totalSum =  computed(() => {
  return products.value.reduce((sum, product) => sum + (product.price * product.count), 0)
});

</script>

<template>

  <div class="container">
    <div class="row">
      <div class="col">
        <h1 class="text-center mt-4">Учёт товаров</h1>
        <form action="">
          <div class="mb-3">
            <label for="name" class="form-label">Название</label>
            <input type="text" class="form-control" id="name" :class="{'is-invalid': !name}" v-model="name">
            <div class="invalid-feedback">
              Заполните название
            </div>
          </div>
          <div class="mb-3">
            <label for="date" class="form-label">Дата приема товара</label>
            <input type="date" class="form-control" id="date" :class="{'is-invalid': !date}" v-model="date">
            <div class="invalid-feedback">
              Заполните дату
            </div>
          </div>
          <div class="mb-3">
            <label for="count" class="form-label">Количество</label>
            <input type="number" class="form-control" id="count" :class="{'is-invalid': !count}" v-model="count">
            <div class="invalid-feedback">
              Заполните количество
            </div>
          </div>
          <div class="mb-3">
            <label for="price" class="form-label">Цена</label>
            <input type="number" class="form-control" id="price" :class="{'is-invalid': !price}" v-model="price">
            <div class="invalid-feedback">
              Заполните цену
            </div>
          </div>
          <div class="mb-2 text-center">
            <button type="button" @click="addProduct" class="btn btn-outline-success">Добавить</button>
          </div>
        </form>
      </div>
    </div>



    <div class="row row-cols-1 row-cols-md-3 g-4">
  <div class="col" v-for="product in products" :key="product.id">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">{{ product.name }}</h5>
        <p class="card-text">{{ product.date }}</p>
        <p class="card-text">{{ product.price }}$</p>
        <p class="card-text">x{{ product.count }}</p>
      </div>
      <div class="card-footer">
        <button class="btn btn-outline-danger" @click="removeProduct(product.id)">Удалить</button>
      </div>
    </div>
  </div>

</div>
<div class="row my-4">
    <div class="col">
      <h3 class="text-end">Общая сумма: {{ totalSum }}$</h3>
    </div>
  </div>
  </div>
</template>

<style></style>
