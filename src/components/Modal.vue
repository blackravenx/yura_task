<template>
    <transition name="modal-fade">
        <div class="modal-backdrop">
            <div class="modal" role="dialog" aria-labelledby="modalTitle" aria-describedby="modalDescription">
                <header class="modal-header" id="modalTitle">
                    Создание товара
                    <button type="button" class="btn-close" @click="close">
                        X
                    </button>
                </header>
                <section class="modal-body" id="modalDescription">
                    <form style=" display: flex;
                        -ms-flex-wrap: wrap;
                        flex-wrap: wrap;
                        flex-direction: column;">
                        <div>
                            <label for="name">Название товара</label>
                            <input type="text" id="name" v-model="product.name">
                        </div>

                        <label for="image">Изображение товара (URL)</label>
                        <input type="text" id="image" v-model="product.image">
                        <label for="cost">Цена товара</label>
                        <input type="number" id="cost" v-model="product.cost">
                    </form>
                </section>

                <footer class="modal-footer">
                    <button type="button" class="btn-green" @click="close">
                        Закрыть
                    </button>
                    <button type="button" class="btn-red" @click="createButtonHandler">
                        Создать
                    </button>
                </footer>
            </div>
        </div>
    </transition>
</template>

<script>
    import AXIOS from "@/plugins/axios";
    export default {
        name: 'Modal',
        data() {
            return {
                product: {
                }
            }
        },
        methods: {
            close() {
                this.$emit('close');
            },
            createButtonHandler() {
                AXIOS.post('/products', this.product).then((response) => {
                    if (response.status) {
                        window.alert('Товар создан')
                    } else {
                        window.alert('Товар не создан')
                    }
                }).catch(e => {
                    window.alert("Исключение: " + e.message)
                })
            }
        },

    };
</script>
<style>
    .modal-backdrop {
        position: fixed;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        background-color: rgba(0, 0, 0, 0.3);
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .modal {
        background: #FFFFFF;
        box-shadow: 2px 2px 20px 1px;
        overflow-x: auto;
        display: flex;
        flex-direction: column;
    }

    .modal-header,
    .modal-footer {
        padding: 15px;
        display: flex;
        align-content: space-between;
    }

    .modal-header {
        position: relative;
        border-bottom: 1px solid #eeeeee;
        color: #4AAE9B;
        justify-content: space-between;
    }

    .modal-footer {
        border-top: 1px solid #eeeeee;
        flex-direction: row;

    }

    .modal-body {
        position: relative;
        padding: 20px 10px;
    }

    .btn-close {
        position: absolute;
        top: 0;
        right: 0;
        border: none;
        font-size: 20px;
        padding: 10px;
        cursor: pointer;
        font-weight: bold;
        color: #4AAE9B;
        background: transparent;
    }

    .btn-red,
    .btn-green {
        color: white;
        border-radius: 2px;
        font-weight: 600;
        width: 100px;
    }

    .btn-green {
        background: #4AAE9B;
        border: 1px solid #4AAE9B;
    }

    .btn-red {
        background: #e60f00;
        border: 1px solid #e60f00;

    }
</style>