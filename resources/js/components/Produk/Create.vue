<script setup>
    import { onMounted, ref } from 'vue';
    import { useRouter } from 'vue-router';

    const router = useRouter()

    let form = ref([])

    onMounted(async () => {
        createForm()
    })

    const createForm = async () => {
        let response = await axios.get('/api/produk_form')
        //console.log('form', form.data)
        form.value = response.data
    }

    const onSave = async () => {
        const formData = new FormData()
        formData.append('api_produk', form.value.produk)
        formData.append('api_price', form.value.price)
        formData.append('api_stock', form.value.stock)

        axios.post('/api/produk', formData)
        router.push('/produk_vue')
    }

    const onBack = () => {
        router.push('/produk_vue')
    }
</script>
<template>
    <h1>Create Produk</h1>
    <hr>
    <table>
        <tr>
            <td>Produk</td>
            <td><input type="text" v-model="form.produk" required></td>
        </tr>
        <tr>
            <td>Price</td>
            <td><input type="number" v-model="form.price" required></td>
        </tr>
        <tr>
            <td>Stock</td>
            <td><input type="number" v-model="form.stock" required></td>
        </tr>
        <tr>
            <td>
                <button @click="onSave">Save</button>
            </td>
            <td>
                <button @click="onBack">Back</button>
            </td>
        </tr>
    </table>
</template>