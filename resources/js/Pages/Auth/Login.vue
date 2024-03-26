<script setup>
import { Head, Link, useForm } from '@inertiajs/vue3';
import AuthenticationCard from '@/Components/AuthenticationCard.vue';
import AuthenticationCardLogo from '@/Components/AuthenticationCardLogo.vue';
import Checkbox from '@/Components/Checkbox.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { useDark } from '@vueuse/core';
import { Button } from '@/Components/ui/button';
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from '@/Components/ui/card';
import { Input } from '@/Components/ui/input';
import { Label } from '@/Components/ui/label';

defineProps({
    canResetPassword: Boolean,
    status: String,
});

const isDark = useDark();

const form = useForm({
    email: '',
    password: '',
    remember: true,
});

const submit = () => {
    form.transform(data => ({
        ...data,
        remember: form.remember ? 'on' : '',
    })).post(route('login'), {
        onFinish: () => form.reset('password'),
    });
};
</script>

<template>

    <Head title="Log in" />
    <div class="flex min-h-screen items-center justify-center">
        <Card class="mx-auto max-w-md">
            <CardHeader>
                <CardTitle class="text-2xl">
                    Login
                </CardTitle>
                <CardDescription>
                    Enter your email below to login to your account
                </CardDescription>
            </CardHeader>
            <CardContent>
                <form @submit.prevent="submit" class="grid gap-4">
                    <div class="grid gap-2">
                        <Label for="email">Email</Label>
                        <Input id="email" v-model="form.email" type="email" placeholder="m@example.com" required
                            autofocus autocomplete="username" />
                        <InputError class="mt-2" :message="form.errors.email" />
                    </div>
                    <div class="grid gap-2">
                        <div class="flex items-center">
                            <Label for="password">Password</Label>
                            <Link v-if="canResetPassword" :href="route('password.request')"
                                class="ml-auto inline-block text-sm underline">
                            Forgot your password?
                            </Link>
                        </div>
                        <Input id="password" v-model="form.password" type="password" required
                            autocomplete="current-password" />
                        <InputError class="mt-2" :message="form.errors.password" />
                    </div>
                    <Button type="submit" class="w-full" :class="{ 'opacity-25': form.processing }"
                        :disabled="form.processing">
                        Login
                    </Button>
                </form>
                <Button variant="outline" class="w-full my-4">
                    Login with Google
                </Button>
                <div class="mt-4 text-center text-sm">
                    Don't have an account?
                    <Link :href="route('register')" class="underline">
                    Sign up
                    </Link>
                </div>
            </CardContent>
        </Card>
    </div>
    <!-- <AuthenticationCard>
        <template #logo>
            <AuthenticationCardLogo />
        </template>

<div v-if="status" class="mb-4 font-medium text-sm text-green-600 dark:text-green-400">
    {{ status }}
</div>

<form @submit.prevent="submit">
    <div>
        <InputLabel for="email" value="Email" />
        <TextInput id="email" v-model="form.email" type="email" class="mt-1 block w-full" required autofocus
            autocomplete="username" />
        <InputError class="mt-2" :message="form.errors.email" />
    </div>

    <div class="mt-4">
        <InputLabel for="password" value="Password" />
        <TextInput id="password" v-model="form.password" type="password" class="mt-1 block w-full" required
            autocomplete="current-password" />
        <InputError class="mt-2" :message="form.errors.password" />
    </div>

    <div class="block mt-4">
        <label class="flex items-center">
            <Checkbox v-model:checked="form.remember" name="remember" />
            <span class="ms-2 text-sm text-gray-600 dark:text-gray-400">Remember me</span>
        </label>
    </div>

    <div class="flex items-center justify-end mt-4">
        <Link v-if="canResetPassword" :href="route('password.request')"
            class="underline text-sm text-gray-600 dark:text-gray-400 hover:text-gray-900 dark:hover:text-gray-100 rounded-md focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 dark:focus:ring-offset-gray-800">
        Forgot your password?
        </Link>

        <PrimaryButton class="ms-4" :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
            Log in
        </PrimaryButton>
    </div>
</form>
</AuthenticationCard> -->
</template>
