<script setup>
import { GoogleLogin, decodeCredential } from 'vue3-google-login'
import { ref } from 'vue';
import { Button } from '@/Components/ui/button';
import AppLayout from '@/Layouts/AppLayout.vue';
import MainLayout from '@/Layouts/MainLayout.vue';
import Welcome from '@/Components/Welcome.vue';

import {
    Dialog,
    DialogClose,
    DialogContent,
    DialogFooter,
    DialogHeader,
    DialogTitle,
    DialogTrigger,
} from '@/Components/ui/dialog';
import {
    Tabs,
    TabsContent,
    TabsList,
    TabsTrigger,
} from '@/Components/ui/tabs';
import { Toggle } from '@/Components/ui/toggle';
import { Archive } from 'lucide-vue-next';

const selectedService = ref(null);
const selectedTab = ref('pick');

const selectService = (index) => {
    if (selectedService.value === index) {
        selectedService.value = null;
        return;
    }
    selectedService.value = index;
    selectedTab.value = 'configure';
};

const resetModal = (isOpen) => {
    if (!isOpen) {
        selectedService.value = null;
        selectedTab.value = 'pick';
    }
};

const callback = (response) => {
    const userData = decodeCredential(response.credential)
    console.log("Handle the userData", userData)
}
</script>

<template>
    <MainLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight">
                Dashboard
            </h2>
        </template>
        <div class="flex flex-1 items-center justify-center rounded-lg border border-dashed shadow-sm">
            <div class="flex flex-col items-center gap-1 text-center">
                <h3 class="text-2xl font-bold tracking-tight">
                    You have no services set up.
                </h3>
                <p class="text-sm text-muted-foreground">
                    You can start by adding a new service provider to your account.
                </p>

                <Dialog @update:open="resetModal">
                    <DialogTrigger as-child>
                        <Button class="mt-4">
                            Add Service
                        </Button>
                    </DialogTrigger>
                    <DialogContent class="w-full max-w-4xl">
                        <DialogHeader>
                            <DialogTitle>
                                Select Service
                            </DialogTitle>
                            <div class="mt-8">
                                <Tabs v-model="selectedTab" default-value="account" class="w-full">
                                    <TabsList class="grid w-full grid-cols-2">
                                        <TabsTrigger value="pick">
                                            Pick a service
                                        </TabsTrigger>
                                        <TabsTrigger :disabled="selectedService === null" value="configure">
                                            Service Configuration
                                        </TabsTrigger>
                                    </TabsList>
                                    <TabsContent class="flex justify-center flex-wrap gap-4 my-8" value="pick">
                                        <Toggle v-model="selectedService" v-for="i in 24" :key="i"
                                            :pressed="selectedService === i" @update:pressed="selectService(i)"
                                            variant="outline" class="size-20">
                                            <Archive class="size-12" />
                                        </Toggle>
                                    </TabsContent>
                                    <TabsContent value="configure">
                                        <GoogleLogin :callback="callback"
                                            client-id="780366128506-u9h5j7dok0dgj4uf0l8ntlc6fg2tap2j.apps.googleusercontent.com" />
                                    </TabsContent>
                                </Tabs>
                            </div>
                        </DialogHeader>

                        <DialogFooter>
                            <DialogClose as-child>
                                <Button variant="outline" class="mr-2">Cancel</Button>
                            </DialogClose>
                            <Button class="mr-2">
                                Create Service
                            </Button>
                        </DialogFooter>
                    </DialogContent>
                </Dialog>
            </div>
        </div>
    </MainLayout>
</template>
