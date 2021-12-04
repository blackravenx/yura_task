<template>
    <div class="product-card">
        <img class="product-image" :src="product.image"
            width="200" :alt="product.title">
        <div>
            <p class="product-meta">Название: <span class="product-meta-info">{{product.title}}</span></p>
            <p class="product-meta">Цена: <span class="product-meta-info">{{product.price}}</span></p>
            <button @click="deleteProductHandler(product.id)" class="delete-button">Удалить</button>
        </div>
    </div>
</template>

<script>
    import AXIOS from '@/plugins/axios';
    export default {
        props: {
            product: Object
        },
        methods: {
            deleteProductHandler(id) {
                console.log("ID: "+id)
                AXIOS.delete('products/' + id).then((response) => {
                    if (response.status == 200) {
                        window.alert('Товар удален. Перезагрузите страницу')
                    } else {
                        window.alert('Товар не удален')
                    }
                }).catch(e => {console.log(e); window.alert('Исключение: '+e.message)})
            }
        }
    }
</script>

<style>
    .product-card {
        width: 200px;
        min-width: 200px;
        flex-wrap: wrap;
        height: 300px;
        margin: 20px 10px;
        box-shadow: 4px 4px 13px 4px #e2e2e2;
        border-radius: 10px;
        padding: 10px 10px;
    }

    .product-image {
        margin: 10px;
    }

    .product-meta {
        font-weight: 600;
    }

    .product-meta-info {
        font-weight: 400;
    }

    .delete-button {
        font-weight: 600;
        background-color: #ff3333;
        padding: 10px 30px;
        color: #ffffff;
        border-radius: 10px;
        border: none;
    }

    /* псевдо класс для стилизации при наведении */
    .delete-button:hover {
        background-color: #a50000;
    }
</style>