<template>
    <ion-button
    color="light"
    expand="block"
    v-if="info"
    @click="$emit('clear-info')" >Clear
        
    </ion-button>
  
</template>

<script>
// @ is an alias to /src


export default {
    name: "ClearInfo",
    props: ['info']
}
</script>
