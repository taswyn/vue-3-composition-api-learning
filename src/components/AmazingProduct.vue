<template>
    <p>
        <h3>{{name}}</h3>
       {{priceFormatted}}
       <input type="text" v-model="priceFormatted" />
               <button @click="addToCart">Add to Cart</button>
    </p>
</template>

<script>

import { computed, ref } from "vue"

export default {
    props: {
        name: String,
        price: Number,
    },
    setup(props, {emit}) {
        // context does not receive reactive data, so can be destructured
        // into attrs, slots, emit, including just individually

        const addToCart = () => emit("addToCart", props.name)

        //const priceFormatted = computed(() => `$${props.price.toFixed(2)}`)

        /* const priceFormatted = computed({
            get() {
                return `$${props.price.toFixed(2)}`
            },
            set(price) {
                props.price = price
                // this will fail as props are read-only,
                // would need to have made a ref and then used that

                // see following below
            }
        }) */

        const priceRef = ref(props.price)

        const priceFormatted = computed({
            get() {
                return `$${priceRef.value.toFixed(2)}`
            },
            set(price) {
                const dropFormatting = (numericString) => {
                    // cheat to end up with a proper number
                    const regex=/[^0-9\.]/g
                    return Number(numericString.replaceAll(regex, ''))
                }
                priceRef.value = dropFormatting(price)

                if (priceRef.value < props.price) {
                    priceRef.value = props.price
                    console.log("sorry, you can't pick a lower price!")
                }

            }
        })

        console.log({ "name": props.name, "price": props.price })

        return { addToCart, priceFormatted }
    },
}
</script>