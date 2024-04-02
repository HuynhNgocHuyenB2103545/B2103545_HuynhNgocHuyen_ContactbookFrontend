<template>
    <div>
        <div class="page">
            <h4>Thêm Liên hệ</h4>
            <ContactFrom :contact="contact" @submit:contact="addContact" />
        </div>
    </div>
</template>

<script>
import ContactService from "@/services/contact.service";
import ContactFrom from "@/components/ContactForm.vue";
import { reactive } from "vue";
export default {
    components: {
        ContactFrom,
    },
    setup() {
        const contact = reactive({
            name: "",
            phone: "",
            email: "",
            address: "",
        });
        const message = reactive({
            value: "",
        });
        async function addContact(data) {
            try {
                await ContactService.create(data);
                message.value = "Liên hệ được thêm thành công.";
                console.log(message.value);
            } catch (error) {
                console.log(error);
            }
        }
        return { contact, message, addContact };
    },
};
</script>


<!-- <template>
    <div v-if="contact" class="page">
        <h4>Thêm Liên hệ</h4>
        <ContactForm
            :contact="contact"
            @submit:contact="postContact"
        />
        <p>{{ message }}</p>
    </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
    components: {
        ContactForm,
    },
    props: {
        id: { type: String, required: true },
    },
    data() {
        return {
            contact: null,
            message: "",
        };
    },
    methods: {
        async getContact(id) {
            try {
                this.contact = await ContactService.get(id);
            } catch (error) {
                console.log(error);
                // Chuyển sang trang NotFound đồng thời giữ cho URL không đổi
                this.$router.push({
                    name: "notfound",
                    params: {
                        pathMatch: this.$route.path.split("/").slice(1)
                    },
                query: this.$route.query,
                hash: this.$route.hash,
            });
        }
    },

    async postContact(data) {
        try {
            await ContactService.post(this.contact, data);
            this.message = "Liên hệ được thêm thành công.";
        } catch (error) {
            console.log(error);
        }
    },
},
    created() {
        this.getContact(this.id);
        this.message = "";
    },
};
</script> -->


