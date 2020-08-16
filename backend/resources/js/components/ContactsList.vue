<template>
    <div class="contacts-list">
        <ul>
            <li v-for="(contact, index) in sortedContacts" :key="contact.id" @click="selectContact(index, contact)" :class="{'selected' : index == selected}">
                <div class="avatar">
                    <img :src="contact.avatar">
                </div>
                <div class="contact">
                    <p class="name">{{ contact.name}}</p>
                    <p class="email">{{ contact.email}}</p>
                </div>
                <span class="unread" v-if="contact.unread">{{ contact.unread }}</span>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                selected: 0
            }
        },
        methods: {
            selectContact(index, contact){
                this.selected = index;

                this.$emit('selected', contact)
            }
        },
        props: {
            contacts: {
                type: Array,
                default: []
            }
        },
        computed: {
            sortedContacts(){
                return _.sortBy(this.contacts, [(contact) => {
                    return contact.unread;
                }]).reverse();
            }
        },
    }
</script>

<style scoped>

</style>
