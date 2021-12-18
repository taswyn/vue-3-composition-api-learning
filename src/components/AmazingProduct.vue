<template>
    <p>
        <h3>{{name}}</h3>
       ${{price}}
        <button @click="addToCart">Add to Cart</button>
    </p>
</template>

<script>import { useAttrs } from "@vue/runtime-core"

export default {
    props: {
        name: String,
        price: Number,
    },
    setup(props, {emit}) {
        // context does not receive reactive data, so can be destructured
        // into attrs, slots, emit, including just individually

        const addToCart = () => emit("addToCart", props.name)

        console.log({ "name": props.name, "price": props.price })

        return { addToCart }
    },
}
</script>