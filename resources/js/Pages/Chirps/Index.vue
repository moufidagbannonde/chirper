<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import InputError from '@/Components/InputError.vue';
import Chirp from '@/Components/Chirp.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import { useForm, Head } from '@inertiajs/vue3';
 
 defineProps(['chirps']);
const form = useForm({
    message: '',
});
</script>
 
<template>
    <Head title="Chirps" />
 
    <AuthenticatedLayout>
        <div class="max-w-2xl mx-auto p-4 sm:p-6 lg:p-8">
            <form action="{{route("todo.store")}}" method="post">
                @csrf
                <label for="name" class="form-label mt-4">Nom</label>
                <!-- mt-4 = margin 4 -->
                <input type="text" name="name" class="form-control" id="">
                <div class="text-danger">
                    @error('name')
                        {{$message}}
                    @enderror
                </div>
                <label for="description" class="form-label mt-4">Contenu</label>
                <textarea name="description" class="form-control" id="" cols="30" rows="6"></textarea>
                <div class="text-danger">
                    @error('description')
                        {{$message}}
                    @enderror
                </div>
                <label for="author" class="form-label mt-4">Auteur</label>
                <input type="text" name="author" class="form-control" id="">
                <div class="text-danger">
                    @error('author')
                        {{$message}}
                    @enderror
                </div>
                <label for="date" class="form-label mt-4"> Date</label>
                <input type="date" name="date" class="form-control" id="">
                <div class="text-danger">
                    @error('date')
                        {{$message}}
                    @enderror
                </div>
                <button class="btn btn-primary btn-lg mt-4">Ajouter une tâche</button>
            </form>
            <div class="mt-6 bg-white shadow-sm rounded-lg divide-y">
                <Chirp
                    v-for="chirp in chirps"
                    :key="chirp.id"
                    :chirp="chirp"
                />
            </div>
        </div>
    </AuthenticatedLayout>
</template>