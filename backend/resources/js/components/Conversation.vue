<template>
    <div class="conversation">
        <h1>{{ contact ? contact.name : 'Select a Contact'}}</h1>
        <MessagesFeed :contact="contact" :messages="messages"/>
        <MessageComposer @send="sendText"/>
    </div>
</template>

<script>
    import MessagesFeed from './MessagesFeed';
    import MessageComposer from './MessageComposer'
    export default {
        props: {
            contact: {
                type: Object,
                default: null
            },
            messages: {
                type: Array,
                default: []
            },
        },
        methods: {
            sendText(text){
                if(!this.contact){
                    return;
                }

                axios.post('/convrsation/send', {
                    contact_id: this.contact.id,
                    text: text
                }).then((res) => {
                    this.$emit('new', res.data);
                })
            }
        },
        components: {
            MessagesFeed,
            MessageComposer
        },
    }
</script>

<style scoped>

</style>
