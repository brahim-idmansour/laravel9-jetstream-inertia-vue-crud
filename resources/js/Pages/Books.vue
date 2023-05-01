<template>
    <app-layout>
        <!-- header -->
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Books List
            </h2>
        </template>
        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div
                    class="bg-white overflow-hidden shadow-xl sm:rounded-lg px-4 py-4"
                >
                    <button
                        @click="openForm()"
                        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded my-3"
                    >
                        Create New Book
                    </button>

                    <!-- table -->
                    <table class="table-fixed w-full posts-table">
                        <thead>
                            <tr class="bg-gray-100">
                                <th class="px-4 py-2 w-20">No.</th>
                                <th class="px-4 py-2">Title</th>
                                <th class="px-4 py-2">Author</th>
                                <th class="px-4 py-2">Image</th>
                                <th class="px-4 py-2">Action</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="item in data.data">
                                <td class="px-4 py-2 border">{{ item.id }}</td>
                                <td class="px-4 py-2 border">
                                    {{ item.title }}
                                </td>
                                <td class="px-4 py-2 border">
                                    {{ item.author }}
                                </td>
                                <td class="px-4 py-2 border"><!-- image --></td>
                                <td class="border px-4 py-2">
                                    <button
                                        @click="openForm(item)"
                                        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
                                    >
                                        Edit
                                    </button>
                                    <button
                                        @click="deleteItem()"
                                        class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded"
                                    >
                                        Delete
                                    </button>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                    <Pagination :links="data.links"></Pagination>
                    <book-form
                        :isOpen="isFormOpen"
                        :isEdit="isFormEdit"
                        :form="formObject"
                        @formsave="saveItem"
                        @formclose="closeModal"
                    ></book-form>
                </div>
            </div>
        </div>
    </app-layout>
</template>

<script>
const defaultFormObject = {
    title: null,
    author: null,
    image: null,
};
import AppLayout from "./../Layouts/AppLayout.vue";
import Pagination from "../Components/Pagination.vue";
import BookForm from "./../Components/Book/Form.vue";

export default {
    props: ["data"],
    components: {
        AppLayout,
        Pagination,
        BookForm,
    },
    data() {
        return {
            isFormOpen: false,
            isFormEdit: false,
            formObject: defaultFormObject,
        };
    },
    methods: {
        saveItem(item) {
            console.log(item);
        },
        closeModal() {
            this.isFormOpen = false;
        },
        openForm(item) {
            this.isFormOpen = true;
            this.isFormEdit = !!item;
            this.formObject = item ? item : defaultFormObject;
        },
        deleteItem(item) {
            console.log(item.id);
        },
    },
};
</script>
