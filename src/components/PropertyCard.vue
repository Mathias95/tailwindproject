<template>
    <div>
        <div class="relative pb-5/6">
            <img class="absolute inset-0 rounded-lg shadow-md h-full w-full object-cover" :src="property.imageUrl" alt="">
        </div>
        <div class="px-4 -mt-16 relative">
            <div class="bg-white rounded-lg px-4 py-4 shadow-lg">
                <div class="flex items-center">
                    <span class="inline-block px-2 py-1 leading-none bg-teal-200 text-teal-800 font-semibold rounded-full uppercase tracking-wide text-xs">Plus</span>
                    <div class="ml-2 text-xs text-gray-600 font-semibold uppercase tracking-wide">
                        {{property.beds}} {{property.beds === 1 ? 'bed' : 'beds '}} &bull; {{property.baths}} {{property.baths === 1 ? 'bath' : 'baths '}}
                    </div>
                </div>
                <h4 class="mt-1 text-gray-900 font-semibold text-lg">{{property.title}}</h4>
                <div class="mt-1">
                    <span class="text-gray-900">{{formattedPrice}}</span>
                    <span class="ml-1 text-sm text-gray-600">/wk</span>
                </div>
                <div class="mt-2 flex items-center text-sm text-gray-600">
                    <svg v-for="i in 5" class="h-4 w-4 fill-current" :class="property.rating >= i ? 'text-teal-500' : 'text-gray-400'" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                        <path d="M8.128 19.825a1.586 1.586 0 0 1-1.643-.117 1.543 1.543 0 0 1-.53-.662 1.515 1.515 0 0 1-.096-.837l.736-4.247-3.13-3a1.514 1.514 0 0 1-.39-1.569c.09-.271.254-.513.475-.698.22-.185.49-.306.776-.35L8.66 7.73l1.925-3.862c.128-.26.328-.48.577-.633a1.584 1.584 0 0 1 1.662 0c.25.153.45.373.577.633l1.925 3.847 4.334.615c.29.042.562.162.785.348.224.186.39.43.48.704a1.514 1.514 0 0 1-.404 1.58l-3.13 3 .736 4.247c.047.282.014.572-.096.837-.111.265-.294.494-.53.662a1.582 1.582 0 0 1-1.643.117l-3.865-2-3.865 2z"/>
                    </svg>
                    <span class="ml-2">{{property.reviewCount }} reviews</span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['property'],
    computed: {
        formattedPrice(){
            const formatter = new Intl.NumberFormat('en-US',{
                style: 'currency',
                currency: 'USD',
            })
            return formatter.format(this.property.price / 100)
        }
    }
}
</script>