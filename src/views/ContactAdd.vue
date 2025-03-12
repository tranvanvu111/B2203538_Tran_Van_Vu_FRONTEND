<template>
    <div class="page">
        <h4>Tạo Liên Hệ Mới</h4>
        <ContactForm :contact="contact" @submit:contact="createContact" />
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
    data() {
        return {
            contact: { name: "", email: "", address: "", phone: "", favorite: false },
            message: "",
        };
    },
    methods: {
        async createContact(data) {
            try {
                await ContactService.create(data);
                this.message = "Liên hệ được tạo thành công.";
                    this.$router.push({ name: "contactbook" });
            } catch (error) {
                console.error("Lỗi khi tạo liên hệ:", error);
            }
        },
    },
    created() {
        this.message = "";
    },
};
</script>
