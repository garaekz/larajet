<script setup>
import { router } from '@inertiajs/vue3';
import { useDark, useToggle } from '@vueuse/core';
import { Button } from '@/Components/ui/button';
import { DropdownMenu, DropdownMenuContent, DropdownMenuItem, DropdownMenuLabel, DropdownMenuSeparator, DropdownMenuTrigger } from '@/Components/ui/dropdown-menu';
import { Input } from '@/Components/ui/input';
import MobileMenu from '@/Components/Main/MobileMenu.vue';
import { CircleUser, Eclipse, Search } from 'lucide-vue-next';

defineProps({
    user: Object,
});

const isDark = useDark();
const toggleDark = useToggle(isDark);

const logout = () => {
    router.post(route('logout'));
};
</script>
<template>
    <header class="flex h-14 items-center gap-4 border-b bg-muted/40 px-4 lg:h-[60px] lg:px-6">
        <MobileMenu />
        <div class="w-full flex-1">
            <form>
                <div class="relative">
                    <Search class="absolute left-2.5 top-2.5 h-4 w-4 text-muted-foreground" />
                    <Input type="search" placeholder="Search products..."
                        class="w-full appearance-none bg-background pl-8 shadow-none md:w-2/3 lg:w-1/3" />
                </div>
            </form>
        </div>
        <Button @click="toggleDark()" variant="outline" size="icon" class="ml-auto h-8 w-8">
            <Eclipse class="h-4 w-4" />
            <span class="sr-only">Toggle dark mode</span>
        </Button>
        <DropdownMenu>
            <DropdownMenuTrigger as-child>
                <Button variant="secondary" size="icon" class="rounded-full">
                    <CircleUser class="h-5 w-5" />
                    <span class="sr-only">Toggle user menu</span>
                </Button>
            </DropdownMenuTrigger>
            <DropdownMenuContent align="end">
                <DropdownMenuLabel>
                    <div class="flex flex-col">
                        {{ user.name }}
                        <span class="text-sm text-muted-foreground">{{ user.email }}</span>
                    </div>
                </DropdownMenuLabel>
                <DropdownMenuSeparator />
                <DropdownMenuItem>Settings</DropdownMenuItem>
                <DropdownMenuItem>Support</DropdownMenuItem>
                <DropdownMenuSeparator />
                <DropdownMenuItem class="cursor-pointer" @click="logout">
                    Logout
                </DropdownMenuItem>
            </DropdownMenuContent>
        </DropdownMenu>
    </header>
</template>