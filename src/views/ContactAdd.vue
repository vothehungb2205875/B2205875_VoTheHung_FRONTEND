<template>
    <div class="page">
        <h4>Thêm Liên hệ</h4>
        <ContactForm :contact="contact" @submit:contact="addContact" />
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
            // Dữ liệu ban đầu rỗng
            contact: {
                name: "",
                email: "",
                address: "",
                phone: "",
                favorite: false,
            },
            message: "",
        };
    },
    methods: {
        async addContact(data) {
            try {
                await ContactService.create(data);
                alert("Liên hệ được thêm thành công!");
                this.$router.push({ name: "contactbook" });
            } catch (error) {
                console.log(error);
                this.message = "Có lỗi xảy ra khi thêm liên hệ.";
            }
        },
    },
};
</script>

<style scoped>
.page {
    max-width: 600px;
    margin: auto;
}
</style>
  
